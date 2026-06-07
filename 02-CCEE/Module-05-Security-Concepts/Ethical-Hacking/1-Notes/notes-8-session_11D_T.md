# 💥 Cybersecurity Study Notes — Session 11D

Personal notes on DDoS architecture, botnet mechanics, attack categories, and countermeasures. This session completes the Session 11 attack chain — the machines I've owned in 11A–11C now become weapons in a distributed attack infrastructure.

> [!NOTE]
> Sessions 11A–11C were about **precision** — targeting specific systems, stealing specific credentials, gaining specific access. Session 11D is about **destruction of availability**. The goal shifts from "own one target" to "make a service unusable for everyone." And increasingly, DDoS is used as a **smoke screen** — occupying the SOC while the real intrusion runs quietly elsewhere.

---

## 📚 Table of Contents

- [Where This Session Fits](#-where-this-session-fits)
- [Foundation Knowledge — TCP Half-Open State](#-foundation-knowledge--tcp-half-open-state)
- [Common Misconceptions](#-common-misconceptions)
- [Section 1 — DDoS Architecture](#section-1--ddos-architecture)
  - [DoS vs DDoS](#11-dos-vs-ddos)
  - [The Six Components](#12-the-six-components)
- [Section 2 — Botnet Mechanics](#section-2--botnet-mechanics)
  - [Botnet Lifecycle](#21-botnet-lifecycle)
  - [C2 Communication Models](#22-c2-communication-models)
- [Section 3 — DDoS Attack Categories](#section-3--ddos-attack-categories)
  - [Category 1 — Volumetric Attacks](#31-category-1--volumetric-attacks-bandwidth-exhaustion)
  - [Category 2 — Protocol Attacks](#32-category-2--protocol-attacks-state-table-exhaustion)
  - [Category 3 — Application Layer Attacks](#33-category-3--application-layer-attacks-resource-exhaustion)
- [Section 4 — DDoS Countermeasures](#section-4--ddos-countermeasures)
  - [Network-Level Defenses](#41-network-level-defenses)
  - [Application-Level Defenses](#42-application-level-defenses)
  - [Complete Defender Checklist](#43-complete-defender-checklist)
- [Section 5 — MITRE ATT&CK Mapping](#section-5--mitre-attck-mapping)
- [Section 6 — 2026 Context](#section-6--2026-context)
  - [AI-Powered Adaptive Botnets](#61-ai-powered-adaptive-botnets)
  - [IoT Botnets — The Growing Army](#62-iot-botnets--the-growing-army)
  - [DDoS-for-Ransom (RDoS)](#63-ddos-for-ransom-rdos)
- [Key Takeaways](#-key-takeaways)
- [Glossary](#-glossary)

---

## 🗺️ Where This Session Fits

```
  SESSIONS 6-9          SESSION 10          SESSION 11          SESSIONS 12-20
  [FOUNDATIONS]    →    [RECON &       →    [ACTIVE ATTACK  →  [EXPLOITATION
  Laws, Concepts,       SCANNING]           TECHNIQUES]        & PERSISTENCE]
  Ethics                OSINT, Nmap,        ← YOU ARE HERE
                        Vuln Scan           (Session 11D)
```

Within Session 11 — The Four-Part Attack Chain:

| Sub-Session | Layer | What It Answers |
|---|---|---|
| **11A** | Reconnaissance | What is running? What OS? How to hide? |
| **11B** | Enumeration | Who is there? Whose credentials can I intercept? |
| **11C** | Credential Attack | How do I convert hashes → cleartext? How do I use PtH? |
| **11D** ← HERE | Disruption | How are DDoS attacks built, launched, and defended? How do compromised machines become bots? |

**The critical connection:** Machines compromised through 11A–11C become the **bots**. Each one is a node in a DDoS army. This session shows how that army is organized, commanded, and unleashed — or used as a distraction while the real data theft happens elsewhere.

---

## 🏗️ Foundation Knowledge — TCP Half-Open State

<details>
<summary>🔧 Why SYN Floods Work — The Backlog Queue Problem</summary>

When a client sends a SYN, the server responds with SYN-ACK and enters a **half-open state**. It allocates a **TCB (Transmission Control Block)** in memory to track this pending connection and waits for the final ACK.

If the ACK never arrives:
- The server keeps the half-open connection in memory
- A timer runs (typically **75 seconds** by default)
- After timeout, the TCB is discarded and memory is freed
- BUT during that 75-second window, the memory is **consumed**

Every OS has a **finite backlog queue** for half-open connections:
- **Linux default:** 128 (`net.ipv4.tcp_max_syn_backlog`)
- **Windows default:** varies (~1024)

Once the backlog is **full**, the server cannot accept new connections — even from legitimate users. This is the foundation of SYN Flood attacks: fill the queue faster than entries time out.

</details>

---

## ⚠️ Common Misconceptions

| Misconception | Reality |
|---|---|
| "DDoS is just a lot of traffic. Nothing technical about it." | DDoS is engineered. Different categories target different layers — bandwidth, state tables, or application resources. Sophisticated attacks combine all three simultaneously, each needing a different defense. |
| "A firewall protects me from DDoS." | A firewall doesn't add bandwidth. A 10 Gbps volumetric flood saturates a 1 Gbps link *before* traffic even reaches the firewall. Volumetric defense requires **upstream** mitigation. |
| "Botnets are built by manually installing malware on thousands of machines." | Modern botnets are self-propagating. Mirai (2016) scanned the entire IPv4 space for IoT devices with default credentials and self-installed on 600,000+ devices within weeks. The attacker never touched 99.99% of them. |
| "DDoS only affects websites." | DDoS targets any network-accessible service: DNS servers (Dyn 2016), VPN gateways, API endpoints, game servers, financial platforms. An internal DDoS from a compromised host can take down AD domain controllers. |
| "Amplification just means 'large volume.'" | Amplification has a specific meaning: attacker sends a **small** request to a reflector with the **victim's spoofed IP**. The reflector sends a **much larger** response to the victim. Memcached: 51,000× amplification. A 1 Mbps attacker can generate 51 Gbps on the victim. |
| "SYN Floods are old and don't work anymore." | SYN Floods account for ~55% of all L3/L4 DDoS attacks in 2024 (Cloudflare data). SYN Cookies mitigate basic floods, but high-rate variants can overwhelm even cookie computation capacity. |
| "I need thousands of servers to DDoS someone." | DDoS-as-a-Service (booters/stressers) let anyone rent botnet capacity for $10–$50 per attack from a web interface. Zero technical skill required. |
| "DDoS attackers are untraceable because of spoofed IPs." | Botnet operators leave traces through C2 server registrations, payment records, and C2 protocol analysis. The Mirai operators were identified and prosecuted through C2 infrastructure forensics, ISP cooperation, and FBI investigation. |

---

## Section 1 — DDoS Architecture

### 1.1 DoS vs DDoS

| | DoS | DDoS |
|---|---|---|
| **Sources** | ONE attacker machine | MANY (thousands to millions) |
| **Defense** | Block the single source IP → done | Blocking individual IPs is impractical — each bot sends "normal" amounts |
| **Why it matters** | Trivially stopped by a firewall rule | Requires fundamentally different defenses (upstream scrubbing, anycast) |

**The fundamental equation:**
```
DDoS succeeds when:  ATTACK TRAFFIC  >  TARGET CAPACITY (bandwidth, state, CPU)
Defense succeeds when: FILTERING CAPACITY  >  ATTACK TRAFFIC
```

---

### 1.2 The Six Components

Every DDoS attack infrastructure has six distinct parts. Defenders can intervene at each one.

**Component 1 — The Attacker (Botmaster)**
The human operator. Selects target, configures parameters, issues commands. **Never sends attack traffic directly** — their personal IP never touches the victim's network.

**Component 2 — Command & Control (C2) Server**
The brain. Relays commands from attacker to bots, collects status reports, may host a management web interface. (C2 models covered in [Section 2.2](#22-c2-communication-models))

**Component 3 — Handlers (Optional Middle Tier)**
Intermediate relay servers for large botnets (100,000+ bots). Creates a hierarchy: C2 → handlers → bots. Each handler manages a subset (~1,000 bots each). Like regional managers between the CEO and employees.

**Component 4 — Bots (Zombies)**
The compromised machines that generate attack traffic. Each runs a small agent that connects to C2, receives commands, and sends flood traffic. Modern botnets: 10,000 to 10,000,000+ bots. What becomes a bot: PCs, servers, IoT devices, routers, cloud VMs, mobile phones.

**Component 5 — Reflectors (For Amplification Attacks)**
Legitimate third-party servers (DNS resolvers, NTP servers, Memcached instances) that **unwittingly** amplify traffic. They are NOT compromised — they respond normally to spoofed requests aimed at the victim's IP. This is why BCP38 source address validation at ISPs is critical.

**Component 6 — The Victim (Target)**
What's actually attacked varies — and each requires a different defense:
- The **network link** (bandwidth exhaustion)
- The **firewall/IDS state table** (connection tracking exhausted)
- The **server's TCP stack** (backlog queue full)
- The **application itself** (processing capacity exhausted)

**Complete architecture visual:**

```
ATTACKER (Botmaster)
     |
     | (issues command via C2 protocol)
     ↓
┌─────────────┐
│ C2 SERVER   │ (or P2P mesh / DGA domains)
└──────┬──────┘
       |
 ┌─────┼──────┐
 ↓     ↓      ↓
HANDLER HANDLER HANDLER  (optional — for large botnets)
 |      |       |
 ↓      ↓      ↓
BOT    BOT     BOT       (100,000+ compromised machines)
 |      |       |
 |      |       |  (some bots send spoofed requests to reflectors)
 ↓      ↓       ↓
REFLECTOR REFLECTOR REFLECTOR  (innocent DNS/NTP/Memcached servers)
      |         |         |
      └────┬────┘─────────┘
           |  (amplified responses all directed at victim)
           ↓
┌─────────────┐
│   VICTIM    │ ← receives flood from bots + reflectors simultaneously
└─────────────┘
```

---

## Section 2 — Botnet Mechanics

### 2.1 Botnet Lifecycle

**Stage 1 — Initial Infection (Seeding)**
Bot malware is deployed to the first machines via:
- Phishing emails with malicious attachments (most common for PC botnets — Emotet, TrickBot)
- Drive-by downloads from compromised websites
- Default credential scanning for IoT (Telnet brute force — the Mirai method)
- Supply chain compromise (malicious updates — SolarWinds-style)
- Exploit kits targeting browser/plugin vulnerabilities

**Stage 2 — Rallying (C2 Connection)**
The bot contacts C2 to register — sends its IP, OS version, bandwidth capacity, uptime. C2 responds with an ID and configuration. The bot is now **online and awaiting commands**. If C2 is unavailable, the bot retries on a schedule. Advanced bots use DGA to find alternate C2 domains.

**Stage 3 — Propagation (Self-Replication)**
The bot scans for other vulnerable targets and infects them automatically:
- **Mirai:** Scanned TCP/23 and TCP/2323 with 62 default credential pairs
- **Conficker:** Exploited MS08-067 (Windows SMB vuln), spread via USB and network shares
- **Emotet:** Sent phishing emails FROM infected machines using the victim's own contacts

Growth is exponential: 1 → 10 → 100 → 1,000 → within days, potentially millions.

**Stage 4 — Weaponization (Attack Command)**
The botmaster issues a command via C2:
```
!attack [TARGET_IP] [PORT] [TYPE] [DURATION] [THREADS]
Example: !attack 203.0.113.50 80 HTTP_FLOOD 3600 100
```
All bots execute simultaneously. Combined bandwidth creates a devastating flood.

**Stage 5 — Maintenance & Evasion**
- Updates bot malware to evade new AV signatures
- Rotates C2 domains/IPs to avoid takedowns
- Sometimes patches the vulnerability used for initial infection — to prevent *rival* botnets from taking over
- Rents out excess capacity as DDoS-as-a-Service

---

### 2.2 C2 Communication Models

**Model 1 — Centralized (Client-Server)**

All bots connect to one or a few central C2 servers. Commands flow: Botmaster → C2 → All Bots.

| Attribute | Detail |
|---|---|
| Protocols | IRC (classic, 1999–2010), HTTP/HTTPS (modern — blends with normal traffic) |
| Advantage | Simple, fast command propagation, real-time visibility |
| Weakness | **Single point of failure** — seize the C2 server and the botnet dies |

---

**Model 2 — Peer-to-Peer (P2P)**

No central server. Each bot knows a list of peer bots. Commands propagate through the mesh — injected at any point, they eventually reach everyone. Like a game of telephone with redundant paths.

| Attribute | Detail |
|---|---|
| Used by | GameOver Zeus, Hajime |
| Advantage | **No single point of failure** — removing nodes doesn't disrupt the network |
| Weakness | Slower command propagation, more complex to build, can be disrupted by Sybil attacks (injecting fake nodes) |

---

**Model 3 — Domain Generation Algorithm (DGA)**

Both bot and botmaster run the same algorithm that generates a list of pseudo-random domain names daily. The botmaster registers **one** of them as the active C2. The bot tries each domain until it finds the live one.

| Attribute | Detail |
|---|---|
| Used by | Conficker, Necurs, Dyre |
| Advantage | Extremely hard to preemptively block — thousands of new domains per day |
| Weakness | Once the DGA is reverse-engineered, all future domains can be predicted and sinkholed. High DNS query volume from bots is anomalous and detectable. |

**Real-World Case — Conficker (2008–2009):**
Conficker's DGA generated **50,000 domains per day** across 110 TLDs. ICANN and security researchers formed the "Conficker Working Group" to preemptively register/block all 50,000 daily domains — an unprecedented coordination effort costing millions of dollars.

**C2 Models — Comparison:**

| Attribute | Centralized | P2P | DGA |
|---|---|---|---|
| Resilience | LOW — single point of failure | HIGH — no central node | MEDIUM — new domains daily |
| Detection Difficulty | MODERATE — convergent traffic to C2 | HARD — looks like normal P2P | MODERATE — anomalous DNS queries |
| Takedown Difficulty | EASY — seize C2 server | VERY HARD — no central target | HARD — must reverse DGA + register all domains daily |
| Command Speed | FAST — direct push | SLOW — multi-hop propagation | MODERATE — bot must find active domain |
| Modern Usage (2026) | HTTP/HTTPS C2 still common | Advanced botnets (Hajime) | Most modern banking trojans |

---

## Section 3 — DDoS Attack Categories

### 3.1 Category 1 — Volumetric Attacks (Bandwidth Exhaustion)

**Goal:** Consume ALL available bandwidth. The pipe is full, nothing else gets through.
**Measured in:** Gbps / Tbps
**Typical scale:** 100 Gbps to 3.4+ Tbps

---

#### Attack Type 1 — UDP Flood

Sends massive volumes of UDP packets to **random ports** on the victim. The victim must check if any application is listening on each port — and if not, generate an ICMP "Destination Unreachable" response for each one.

**Why UDP:** Connectionless — no handshake needed. The attacker fires packets at wire speed. Trivially spoofable since there's no connection state to verify.

```
BOTS                                      VICTIM
  |                                          |
  |--- UDP to port 53412 ─────────────────→  |
  |--- UDP to port 8891  ─────────────────→  |  For each packet:
  |--- UDP to port 12044 ─────────────────→  |  1. App listening? NO
  |    (millions/sec, random ports,          |  2. Generate ICMP Unreachable
  |     spoofed source IPs)                  |  3. Consumes CPU + outbound BW
```

**Defense:** Rate-limit ICMP Unreachable generation at OS level. Upstream blackhole routing. Cloud DDoS scrubbing.

---

#### Attack Type 2 — DNS Amplification

Exploits **open DNS resolvers** as reflectors to amplify traffic by 28–54×.

```
ATTACKER                    OPEN RESOLVER               VICTIM
   |                             |                         |
   |-- DNS Query (60 bytes) --→  |                         |
   |   SRC: [VICTIM_IP]         |                         |
   |   Query: ANY isc.org       |                         |
   |                             |                         |
   |                             |-- DNS Response ───────→ |
   |                             |   (~3000 bytes, 50×)    |
   |                             |   DST: [VICTIM_IP]      |
   |                             |                         |
   | (Attacker never receives    | (Resolver thinks the    |
   |  anything back)             |  victim sent the query) |
```

**The math:**
Attacker sends 1 Mbps of spoofed DNS queries → 50× amplification → victim receives 50 Mbps. With 1,000 reflectors: **50 Gbps flood** from a 1 Gbps attacker.

As of 2024, approximately **2–3 million open resolvers** remain on the internet (Shadowserver Foundation data).

**Defense:** DNS operators disable recursion for external queries. ISPs deploy BCP38/uRPF. Victims use cloud-based DNS (Cloudflare, Route53) to absorb amplification at the provider's edge.

---

#### Attack Type 3 — Memcached Amplification

Exploits Memcached instances exposed on **UDP port 11211** for extreme amplification — up to **51,000×**.

1. Attacker pre-loads data into an exposed Memcached server (e.g., 1 MB value)
2. Sends a 15-byte `get [key]` request with victim's spoofed IP
3. Memcached responds with the full 1 MB value → directed at the victim
4. Amplification: 1,000,000 / 15 = **66,666×** for a single key

**Real-World Case — GitHub DDoS (February 2018):**
Memcached amplification peaked at **1.35 Tbps** — at the time, the largest DDoS ever recorded. GitHub was intermittently unavailable for ~10 minutes before Akamai Prolexic absorbed the attack. After this incident, ISPs and cloud providers aggressively blocked UDP 11211 inbound — reducing exposed Memcached instances by 90%+ within months.

---

#### Amplification Factor Reference

| Protocol | Port | Amplification Factor |
|---|---|---|
| **Memcached** | UDP 11211 | 10,000 – 51,000× |
| **NTP Monlist** | UDP 123 | 556× |
| **CharGEN** | UDP 19 | 358× |
| **CLDAP** | UDP 389 | 56 – 70× |
| **TFTP** | UDP 69 | 60× |
| **DNS (ANY query)** | UDP 53 | 28 – 54× |
| **SSDP / UPnP** | UDP 1900 | 30× |
| **SNMP** | UDP 161 | 6× |

---

### 3.2 Category 2 — Protocol Attacks (State Table Exhaustion)

**Goal:** Exhaust the connection state tables of firewalls, load balancers, and servers. NOT about bandwidth — about **connection tracking resources**.
**Measured in:** Packets per second (pps) and concurrent connections
**Typical scale:** 1–10 Mpps

---

#### Attack Type 1 — SYN Flood

Sends massive volumes of TCP SYN packets with **spoofed source IPs**. The server allocates a TCB for each half-open connection. The final ACK never arrives. The backlog queue fills up. Legitimate connections are refused.

> [!IMPORTANT]
> SYN Floods are **protocol** attacks, not volumetric. Each SYN is only ~40–60 bytes — minimal bandwidth. The damage is to the TCP state table. A 100 Mbps SYN flood can overwhelm a server with a 10 Gbps link because the bottleneck is **state entries**, not bandwidth.

```
ATTACKER (spoofed IPs)                      TARGET SERVER
      |                                           |
      |--- SYN (src: 1.2.3.4) ─────────────────→ |
      |    (source IP is spoofed)                 |
      |                                     [Allocates TCB]
      |                                     [Sends SYN-ACK → 1.2.3.4]
      |                                           |
      |                       1.2.3.4 (real owner): "I never sent a SYN."
      |                       → SYN-ACK ignored or RST sent
      |                                           |
      |                                     [Server WAITS for ACK]
      |                                     [75-second timeout, TCB held]
      |                                           |
      |--- SYN (src: 5.6.7.8) ─────────────────→ |
      |--- SYN (src: 9.10.11.12) ──────────────→ |
      |    (thousands/sec, all spoofed)           |
      |                                           |
      |                                     [BACKLOG QUEUE FULL]
      |                                     [Legitimate SYNs DROPPED]
```

**Why spoofing is critical:**
Without spoofing, the attacker's real IP receives the SYN-ACK and the OS auto-sends RST — freeing the backlog slot instantly. Attack fails. With spoofing, the SYN-ACK goes to a random IP that never responds — the server holds the slot for 75 seconds.

**Defense — SYN Cookies:**
The server does NOT allocate a TCB when it receives a SYN. Instead:
1. Constructs a special ISN encoding: timestamp, MSS, client IP/port, and a secret key — all hashed together
2. Sends SYN-ACK with this crafted ISN
3. **Forgets about the connection** — zero state stored
4. When the legitimate client sends the final ACK (containing ISN+1), the server **reconstructs** the connection state from the ISN and verifies it's valid
5. Only THEN does it allocate a TCB

Spoofed SYNs: the final ACK never arrives → no state is ever allocated → attack has **zero effect**.

```bash
# Enable on Linux (usually default):
sysctl -w net.ipv4.tcp_syncookies=1
```

> [!NOTE]
> SYN Cookies have minor limitations — some TCP options (window scaling, SACK) can't be encoded in the ISN, slightly reducing performance for legitimate connections during an active flood. Very high-rate floods (100+ Mpps) can also overwhelm the CPU performing cookie computation itself.

---

#### Attack Type 2 — ACK Flood

Sends massive volumes of TCP ACK packets. The server must look up each ACK in its connection table. Since none match any existing connection, the server wastes CPU processing and discarding them. Stateful firewalls are particularly vulnerable.

**Why it bypasses SYN Cookies:** SYN Cookies defend a different code path. ACK Floods target the established-connection lookup mechanism — a completely separate resource.

**Defense:** Stateless ACL filtering (drop ACKs to ports with no established connections). Rate-limit ACK packets per source IP.

---

#### Attack Type 3 — Smurf Attack (Historical — Largely Mitigated)

ICMP-based amplification using **directed broadcast addresses**.

```
ATTACKER                 BROADCAST NETWORK             VICTIM
   |                    (200 hosts)                       |
   |                         |                            |
   |-- ICMP Echo Req ──→     |                            |
   |   DST: 192.168.1.255   |                            |
   |   SRC: [VICTIM_IP]     |                            |
   |                         |                            |
   |              Host 1 → ICMP Echo Reply ────────────→  |
   |              Host 2 → ICMP Echo Reply ────────────→  |
   |              ...                                     |
   |              Host 200 → ICMP Echo Reply ──────────→  |
   |                         |                            |
   |                         |     [VICTIM receives 200   |
   |                         |      replies from 1 ping]  |
```

**Why it's largely dead:**
RFC 2644 (1999) mandated that routers **must not** forward directed broadcasts by default. Cisco IOS: `no ip directed-broadcast` has been default since IOS 12.0 (1998). It only works on networks that have explicitly re-enabled directed broadcast forwarding — extremely rare.

**Why it's still worth knowing:** Smurf illustrates the **fundamental concept** of amplification and reflection — the exact same principle that powers modern DNS, NTP, and Memcached amplification. Understanding Smurf is the foundation for understanding all reflection attacks.

---

### 3.3 Category 3 — Application Layer Attacks (Resource Exhaustion)

**Goal:** Exhaust the application's processing capacity — CPU, memory, database connections, disk I/O.
**Measured in:** Requests per second (rps)
**Typical scale:** 10,000 – 50,000,000 rps

> [!WARNING]
> Application-layer attacks are the **hardest to defend** because the traffic looks like normal user requests. Valid HTTP, valid SQL. Low bandwidth — doesn't trigger volumetric alerts. Passes through firewalls, IDS, and WAFs as "legitimate." Can't be blocked by simple IP blacklisting when bots use residential proxies.

---

#### Attack Type 1 — HTTP Flood (GET/POST)

Sends valid HTTP requests at high rates to **resource-intensive pages**:
- Search pages with wildcard queries: `/search?q=*a*b*c*` (expensive full-text DB scan)
- Report generation endpoints: `/report/generate?id=12345` (CPU-intensive rendering)
- Login pages: `/login` (ironically, bcrypt hashing makes each attempt CPU-expensive)
- Unprotected API endpoints: `/api/v1/users?page=1` (DB queries per call)

**Defense:** WAF with rate limiting per IP/session/URL. CAPTCHA challenges. JavaScript challenges (bots typically can't execute JS). Behavioral analysis — block clients that never load CSS/JS/images.

---

#### Attack Type 2 — Slowloris

Opens many HTTP connections and keeps them **open indefinitely** by sending partial headers very slowly — never completing the request. Each open connection holds a server thread. When all threads are consumed, no new connections can be served.

**How it works:**
```
Step 1: Open TCP connection to port 80/443
Step 2: Send: "GET / HTTP/1.1\r\nHost: target.com\r\n"
Step 3: Server WAITS for the rest of the headers (\r\n\r\n to end)
Step 4: Every 10–15 seconds, send ONE more header: "X-Custom: value\r\n"
        (keeps connection alive — prevents timeout)
Step 5: Repeat across thousands of connections
Step 6: ALL server connection slots consumed by partial requests
Step 7: Legitimate users → "Connection refused" or timeout
```

**Why Slowloris is elegant:**
- Requires **< 1 Mbps** total bandwidth
- A **single machine** can take down an Apache server
- Traffic looks like normal HTTP — just very slow
- Doesn't trigger volumetric detection

**Vulnerable vs. Not Vulnerable:**

| Server | Status | Why |
|---|---|---|
| **Apache** | ✅ Vulnerable | Thread-per-connection model — each slow connection permanently holds one thread |
| **IIS** | ⚠️ Partially vulnerable | Connection limits help but don't fully prevent |
| **Nginx** | ❌ NOT vulnerable | Event-driven model — handles millions of idle connections with minimal resources |

**Defense:** Use Nginx as a reverse proxy in front of Apache. Set aggressive header timeouts (`RequestReadTimeout header=10-20` in Apache). Limit concurrent connections per IP (`iptables connlimit`). Deploy a CDN that absorbs Slowloris before it reaches the origin.

---

#### Attack Type 3 — R-U-Dead-Yet (RUDY)

Similar to Slowloris but targets **POST bodies** instead of headers. Sends a POST with a huge `Content-Length` (e.g., 1,000,000 bytes) then transmits the body **one byte at a time**.

The server has committed to receiving 1 MB (as declared by Content-Length). At 1 byte per 10 seconds, that's 10 million seconds = **~115 days** holding that connection slot open.

**Defense:** Aggressive body read timeouts. Limit maximum `Content-Length` for POST requests. Rate-limit POST requests per source IP.

---

#### Master Comparison — All Three DDoS Categories

| Attribute | Volumetric | Protocol | Application |
|---|---|---|---|
| **Target** | Bandwidth (network pipe) | State tables (TCP stack, firewall) | Application resources (CPU, memory, DB) |
| **Layer** | L3/L4 | L3/L4 | L7 |
| **Measurement** | Gbps / Tbps | Mpps (packets/sec) | Requests/sec |
| **Bandwidth Required** | VERY HIGH | LOW–MODERATE | VERY LOW |
| **Detection Difficulty** | EASY (massive traffic spike) | MODERATE (anomalous packet ratios) | HARD (looks like normal users) |
| **Examples** | UDP Flood, DNS Amp, NTP Amp, Memcached Amp | SYN Flood, ACK Flood, Smurf | HTTP Flood, Slowloris, RUDY |
| **Primary Defense** | Upstream scrubbing, anycast, cloud DDoS | SYN Cookies, rate limiting, stateless ACLs, BCP38 | WAF, CAPTCHA, behavioral analysis, CDN |
| **Single Machine?** | Possible via amplification (reflectors) | YES — SYN flood with spoofing | YES — Slowloris from one IP |

**Real-World Case — Dyn DNS DDoS (October 2016 — Mirai Botnet):**
~100,000 IoT devices (cameras, DVRs, routers) infected by Mirai via default credential brute force launched a multi-vector attack against Dyn, a major DNS provider. Peak: **~1.2 Tbps** combining DNS flood + SYN flood + ACK flood. Impact: Twitter, Netflix, Reddit, GitHub, PayPal, Spotify, and dozens of other major services were unreachable for **6+ hours** across North America and Europe. Estimated economic impact: hundreds of millions of dollars.
Lesson: IoT devices with default credentials are the largest untapped DDoS weapon in existence.

---

## Section 4 — DDoS Countermeasures

### 4.1 Network-Level Defenses

#### Countermeasure 1 — BCP38 / uRPF (Source Address Validation)

ISPs verify that packets leaving their network have source IPs belonging to their assigned ranges. uRPF (Unicast Reverse Path Forwarding) is the router mechanism:

```
Router: "Does the source IP of this outgoing packet belong to a customer on this interface?"
  YES → forward normally
  NO  → DROP (spoofed source IP)
```

**Defends against:** ALL reflection/amplification attacks — they all depend on spoofing. If spoofing is blocked at the ISP, spoofed packets never reach reflectors.

**Limitation:** Requires ISP cooperation. As of 2024, only ~75% of ASes globally implement BCP38 (MANRS data). The remaining 25% still allow spoofed packets out. Does NOT help against direct floods from bots using their real IPs.

---

#### Countermeasure 2 — Rate Limiting & Traffic Shaping

Limiting specific traffic types per source IP / protocol / port. Examples:
- **ICMP rate limit:** max 10 pings/sec per source (Smurf, ping floods)
- **SYN rate limit:** max 100 SYNs/sec per source (non-spoofed SYN flood)
- **DNS Response Rate Limiting (RRL):** max 5 identical responses/sec to same destination (DNS amplification at the reflector)

**Limitation:** Can't distinguish legitimate burst traffic from attacks with the same profile. Aggressive limits may block users during flash sales or viral content. Ineffective when each bot individually stays below the threshold.

---

#### Countermeasure 3 — Blackhole Routing (RTBH)

Instructs upstream routers to **drop ALL traffic** destined for the victim's IP. Attack traffic is discarded at the ISP edge before it reaches the victim's link.

> [!WARNING]
> **Last resort only.** Blackhole routing drops legitimate traffic too. The victim's service is still unavailable. The attacker effectively wins — the service is offline either way. Used only when the attack threatens to overwhelm upstream infrastructure (ISP routers, peering links) and collateral damage to other customers must be prevented.

---

#### Countermeasure 4 — Anycast Diffusion

Same IP address announced from servers in **multiple geographic locations**. BGP routes each client to the nearest instance. Attack traffic is naturally **distributed** across all instances — each absorbing a fraction.

A 500 Gbps attack against a Cloudflare-protected site → distributed across 200+ PoPs → each handles ~2.5 Gbps → well within scrubbing capacity.

**Used by:** Cloudflare (200+ data centers), AWS CloudFront, Google Cloud CDN, DNS root servers (all 13 root server letters use anycast).

**Limitation:** Requires global infrastructure — must use a CDN/DDoS provider. Enterprise DDoS protection: $3,000–$100,000+/month.

---

#### Countermeasure 5 — Upstream Scrubbing Centers

Dedicated facilities (Akamai Prolexic, Cloudflare Magic Transit, AWS Shield Advanced) that receive ALL traffic destined for the victim, filter out attack traffic, and forward only clean traffic to the origin.

```
Normal:       Internet → Victim
During attack: Internet → Scrubbing Center → [FILTER] → Victim
Redirection:  BGP re-announcement, DNS change, or GRE tunnel
```

Scrubbing centers have **multi-Tbps capacity** and specialized hardware for packet analysis. They separate attack from legitimate traffic using packet signatures, rate analysis, behavioral patterns, reputation databases, and ML models.

---

### 4.2 Application-Level Defenses

#### Countermeasure 6 — Web Application Firewall (WAF)

Inspects HTTP/HTTPS at Layer 7 and applies rules:
- Rate limiting per IP / session / URL path
- CAPTCHA insertion for suspicious patterns
- Bot detection via JavaScript challenges and fingerprinting
- Geographic blocking
- Request pattern analysis (block clients with no referrer, no cookies, no JS execution)

**Options:** Cloud WAF (Cloudflare, AWS WAF, Akamai Kona) or on-premise (ModSecurity, F5 ASM, Imperva).

---

### 4.3 Complete Defender Checklist

- **UPSTREAM:** Contract a DDoS mitigation provider (Cloudflare, Akamai, AWS Shield) **before** an attack. Establish BGP-based traffic redirection. Test quarterly.
- **NETWORK:** Implement BCP38/uRPF on all border routers — prevent YOUR infrastructure from being used as a reflector.
- **PROTOCOL:** Enable SYN Cookies on all servers. Tune TCP backlog queue sizes. Deploy stateless ACLs.
- **APPLICATION:** WAF with rate limiting, JS challenges, CAPTCHA triggers. Rate-limit all API endpoints. Connection timeouts for slow clients.
- **DNS:** Use multiple DNS providers for redundancy. Enable DNS Response Rate Limiting (RRL) on authoritative servers.
- **MONITORING:** NetFlow/sFlow analysis on border routers. Alert on: traffic volume > 2× baseline, SYN:SYN-ACK ratio > 10:1 (SYN flood indicator), ICMP volume spikes.
- **INCIDENT RESPONSE:** DDoS playbook with provider contacts, BGP community strings for blackhole routing, pre-built rate-limiting profiles, communication templates for customers/stakeholders.

---

## Section 5 — MITRE ATT&CK Mapping

**Primary Tactic: TA0040 — Impact**

| Tech ID | Technique Name | Session 11D Mapping | Tool |
|---|---|---|---|
| **T1498** | Network Denial of Service | All volumetric + protocol DDoS attacks | hping3, LOIC, botnets |
| **T1498.001** | Network DoS: Direct Network Flood | UDP Flood, SYN Flood, ACK Flood — bots send traffic directly | hping3, botnets |
| **T1498.002** | Network DoS: Reflection Amplification | DNS Amp, NTP Monlist, Memcached Amp, Smurf — spoofed requests to reflectors | scapy, hping3 |
| **T1499** | Endpoint Denial of Service | All application-layer DDoS | slowloris.py, GoldenEye, HULK |
| **T1499.001** | Endpoint DoS: OS Exhaustion | SYN Flood targeting server TCP backlog queue | hping3 `--flood -S` |
| **T1499.002** | Endpoint DoS: Service Exhaustion | HTTP Flood targeting connection pools and thread limits | GoldenEye, slowhttptest |
| **T1499.003** | Endpoint DoS: Application Exhaustion | Slowloris, RUDY — slow HTTP attacks holding connections | slowloris.py, r-u-dead-yet |
| **T1583.005** | Acquire Infrastructure: Botnet | Attacker builds or rents botnet | Mirai variants, booter services |
| **T1584.005** | Compromise Infrastructure: Botnet | Adding machines compromised via 11A–11C to botnet | Bot agent post-exploitation |

> [!IMPORTANT]
> **Detection key — T1498 vs T1499:**
>
> The split between Network DoS (T1498) and Endpoint DoS (T1499) determines which **playbook** to activate:
> - **High bandwidth + normal request rate** = T1498 (volumetric) → activate upstream scrubbing
> - **Normal bandwidth + high connection count + low completion rate** = T1499.003 (Slowloris-type) → restart Apache, deploy Nginx reverse proxy, reduce timeouts
>
> Misclassification leads to wrong defenses. Deploying WAF rules against a volumetric flood does nothing. Activating upstream scrubbing against a Slowloris attack wastes money — the low-bandwidth traffic passes through as "clean."

---

## Section 6 — 2026 Context

### 6.1 AI-Powered Adaptive Botnets

**The evolution:**

| Era | Behavior |
|---|---|
| 2010–2020 | Static attack patterns. Bots send the same traffic at the same rate. Defense: identify pattern → deploy filter → done. |
| 2024–2026 | AI-adaptive botnets that **change attack vectors in real-time** based on defense response. |

What 2026 adaptive botnets do:
- If volumetric flood is scrubbed → **switch** to application-layer
- If HTTP flood is rate-limited → **switch** to Slowloris
- If Slowloris detected → rotate to random HTTP GETs with varied User-Agents, referrers, and timing jitter
- AI generates traffic that **mimics real user behavior** — mouse movements, page navigation, realistic timing

**Implication for defenders:**
Static rules no longer cut it. Defense in 2026 requires ML-based anomaly detection, behavioral analysis at the session level (not just packet level), real-time adaptive rate limiting, and DDoS providers with AI-powered scrubbing at the edge.

---

### 6.2 IoT Botnets — The Growing Army

By 2026, approximately **18–20 billion IoT devices** are internet-connected. The majority of consumer IoT:
- Ships with default credentials (`admin/admin`, `root/root`)
- Has no automatic update mechanism
- Runs stripped-down Linux with known vulnerabilities
- Has no firewall or IDS capability

**Post-Mirai botnets (2020–2026):**

| Botnet | Year | Method | Scale |
|---|---|---|---|
| **Mozi** | 2019–2023 | Exploited Netgear, D-Link, Huawei router vulns. P2P C2. | 1.5 million bots |
| **Mēris** | 2021 | Exploited MikroTik router firmware bugs | 21.8 million HTTP rps against Yandex — record app-layer DDoS |
| **InfectedSlurs** | 2023 | Exploited zero-days in multiple IoT brands. Mirai variant. | Updated credential list + new exploits |

**Indian context:**
India is the second-largest IoT market by device count. Jio Fiber routers, Airtel Xstream devices, government CCTV deployments (Smart Cities Mission), and industrial IoT — all represent potential botnet recruitment targets. CERT-In has issued multiple advisories (CIAD-2023-0024, CIAD-2024-0011) warning about IoT botnet risks in Indian infrastructure.

---

### 6.3 DDoS-for-Ransom (RDoS)

The attacker sends a ransom demand before or during a DDoS: *"Pay X Bitcoin or we continue/escalate."*

**2024–2026 trends:**
- **"Anonymous Sudan" (2023–2024):** Attacked Microsoft Outlook, OneDrive, and Azure Portal. Peaked at 1.5+ Tbps using custom tools ("Skynet", "InfraShutdown"). Two members indicted by US DOJ in October 2024.
- **Indian financial sector:** Multiple banks and payment gateways received RDoS threats in 2023–2024. RBI Circular CSITE.CO.No.1762 (2024) mandated DDoS mitigation capabilities for all scheduled commercial banks.

**Legal context:**

| Law | Relevance |
|---|---|
| **IT Act 2000, S. 66** | Computer-related offenses. DDoS = unauthorized access + resource consumption. Up to 3 years imprisonment. |
| **IT Act 2000, S. 66F** | **Cyberterrorism.** DDoS against critical infrastructure (power grid, banking, defense) → imprisonment up to **life**. |
| **IT Act 2000, S. 43** | Civil liability for damage caused by DDoS — compensation determined by adjudicating officer (no upper limit for commercial damages). |

> [!WARNING]
> Every technique in this session requires **explicit written authorization** before execution. DDoS testing is legally distinct from vulnerability scanning — it can affect upstream infrastructure, ISP peering, and third-party services. Coordination with the ISP is mandatory before any DDoS simulation.

---

## ✅ Key Takeaways

- [x] DoS = single source. DDoS = many sources. The "distributed" part makes blocking fundamentally harder — filtering one IP is trivial, filtering 100,000 simultaneously is not.
- [x] DDoS architecture has six components: attacker, C2, handlers, bots, reflectors, victim. Defenders can intervene at each point.
- [x] Three C2 models: Centralized (easy to take down, single point of failure), P2P (nearly impossible to take down), DGA (requires reverse engineering the algorithm).
- [x] Three DDoS categories target different layers: **volumetric** (bandwidth), **protocol** (state tables), **application** (CPU/memory). Each requires a DIFFERENT defense.
- [x] SYN Flood fills the TCP backlog queue with half-open connections. **SYN Cookies** eliminate state storage for unverified connections — encoding state in the ISN instead.
- [x] Amplification attacks exploit reflectors using spoofed source IPs. Memcached: 51,000×. DNS: 28–54×. BCP38/uRPF at ISP level prevents spoofing and kills all amplification attacks.
- [x] Smurf (ICMP + broadcast + spoofing) is dead since RFC 2644 (1999), but its principle — amplification via reflection — is the foundation for all modern DDoS amplification.
- [x] Application-layer attacks (HTTP Flood, Slowloris, RUDY) are the **hardest to detect** — valid HTTP at low bandwidth, indistinguishable from legitimate traffic.
- [x] Slowloris can down Apache from a **single machine** at < 1 Mbps. Nginx is NOT vulnerable (event-driven architecture). Reverse proxying Apache behind Nginx is an effective defense.
- [x] Upstream scrubbing centers (Cloudflare, Akamai, AWS Shield) are the primary volumetric defense — they have the bandwidth individual organizations lack.
- [x] Anycast distributes attack traffic across global PoPs, each absorbing a fraction. This is how CDNs protect millions of sites from multi-Tbps attacks.
- [x] GitHub Memcached DDoS (2018, 1.35 Tbps) proved amplification generates terabit-scale attacks from minimal attacker bandwidth. Dyn/Mirai (2016, 1.2 Tbps) proved IoT botnets are the largest DDoS weapon.
- [x] AI-powered adaptive botnets in 2026 switch attack vectors in real-time based on defense responses — requiring ML-based detection, not static rules.
- [x] DDoS against Indian critical infrastructure = cyberterrorism under IT Act 2000 S. 66F — imprisonment up to life. RBI mandates DDoS mitigation for all scheduled commercial banks.
- [x] Machines compromised in 11A–11C become bots. The attack chain from reconnaissance to disruption is a continuous pipeline — each session builds on the last.

---

<details>
<summary>📖 Glossary</summary>

| Term | Definition |
|---|---|
| **DoS** | Denial of Service — attack from a single source. Blocked by filtering one IP. |
| **DDoS** | Distributed Denial of Service — attack from many sources. Cannot be blocked by filtering individual IPs. |
| **Botnet** | Network of compromised machines controlled remotely by a botmaster via C2 infrastructure. |
| **Bot (Zombie)** | A compromised machine running agent software that executes C2 commands — typically without the owner's knowledge. |
| **Botmaster** | The human operator controlling the botnet. Issues commands via C2. Never sends attack traffic from their own IP. |
| **C2 (Command & Control)** | Communication infrastructure through which the botmaster issues commands and receives bot status reports. |
| **Handler** | Intermediate relay server between C2 and bots in large botnets. Creates hierarchical command distribution. |
| **Reflector** | Legitimate third-party server that unwittingly amplifies attack traffic by responding to spoofed requests aimed at the victim. |
| **Amplification Factor** | Ratio of response size to request size in a reflection attack. DNS: 28–54×. Memcached: 10,000–51,000×. |
| **Volumetric Attack** | DDoS targeting bandwidth. Goal: saturate the link. Measured in Gbps/Tbps. Examples: UDP Flood, DNS Amp, Memcached Amp. |
| **Protocol Attack** | DDoS targeting state tables in network equipment. Goal: exhaust connection tracking. Measured in pps. Examples: SYN Flood, ACK Flood. |
| **Application Layer Attack** | DDoS targeting L7 resources (CPU, memory, DB). Goal: exhaust processing capacity. Measured in rps. Examples: HTTP Flood, Slowloris, RUDY. |
| **UDP Flood** | Volumetric attack sending massive UDP packets to random ports. Victim wastes CPU generating ICMP Unreachable. |
| **DNS Amplification** | Reflection attack via open DNS resolvers. Spoofed "ANY" query → 28–54× larger response to victim. |
| **NTP Monlist** | Reflection attack via NTP `MON_GETLIST` command. Returns list of last 600 clients. 556× amplification. |
| **Memcached Amplification** | Reflection via exposed Memcached on UDP 11211. Extreme amplification up to 51,000×. GitHub 2018: 1.35 Tbps. |
| **SYN Flood** | Protocol attack filling the TCP backlog queue with half-open connections using spoofed SYNs. |
| **Half-Open Connection** | TCP connection in SYN_RECEIVED state — SYN received, SYN-ACK sent, final ACK not yet received. Consumes a backlog queue slot. |
| **TCB** | Transmission Control Block — kernel data structure storing TCP connection state. One per connection or half-open SYN. |
| **Backlog Queue** | Kernel buffer holding half-open connections waiting for the final ACK. Linux default: 128. When full, new SYNs are dropped. |
| **SYN Cookie** | Kernel defense encoding connection state in the SYN-ACK ISN. No state consumed until final ACK verified. `net.ipv4.tcp_syncookies=1`. |
| **ACK Flood** | Protocol attack sending unsolicited ACKs. Server/firewall wastes CPU looking up nonexistent connections. |
| **Smurf Attack** | ICMP amplification via directed broadcast. Spoofed ping to broadcast → all hosts reply to victim. Mitigated by RFC 2644 (1999). |
| **Directed Broadcast** | IP broadcast targeting all hosts on a specific subnet (e.g., 192.168.1.255). Forwarding disabled by default since 1998. |
| **HTTP Flood** | App-layer attack sending valid HTTP requests at high rate to expensive endpoints. Hard to distinguish from legitimate traffic. |
| **Slowloris** | App-layer attack holding HTTP connections open via partial headers. Exhausts Apache threads from a single machine. Nginx is immune. |
| **RUDY** | R-U-Dead-Yet — Slowloris variant targeting POST bodies. Declares large Content-Length, sends body one byte at a time. |
| **BCP38** | RFC 2827 — ISPs verify source IPs of outgoing packets belong to their assigned ranges. Prevents spoofing at ISP level. |
| **uRPF** | Unicast Reverse Path Forwarding — router mechanism implementing BCP38. Drops packets with spoofed source IPs. |
| **RTBH** | Remotely Triggered Black Hole routing — drops ALL traffic to victim IP at ISP edge. Last resort — service is still down. |
| **Anycast** | Same IP announced from multiple geographic locations. Traffic routed to nearest. DDoS distributed across all locations. |
| **Scrubbing Center** | Facility that receives, filters, and forwards only clean traffic to origin. Operated by Cloudflare, Akamai, AWS Shield, etc. |
| **WAF** | Web Application Firewall — inspects HTTP at L7. Rate limiting, CAPTCHA, bot detection, behavioral analysis. |
| **DGA** | Domain Generation Algorithm — bots generate pseudo-random domains daily to find active C2. Defeats static domain blocking. |
| **Mirai** | IoT botnet (2016). 600,000+ devices via default credentials. Attacked Dyn DNS (1.2 Tbps). Source code publicly released. Variants active in 2026. |
| **Mēris** | Botnet (2021) exploiting MikroTik routers. 21.8 million HTTP rps against Yandex — record app-layer DDoS at the time. |
| **DDoS-as-a-Service** | Booter/stresser services — rent botnet capacity for $10–$50 per attack. Zero technical skill required. |
| **RDoS** | Ransom DDoS — extortion combining DDoS with ransom demand in cryptocurrency. |
| **T1498** | MITRE ATT&CK: Network Denial of Service — all L3/L4 DDoS. |
| **T1498.001** | Sub-technique: Direct Network Flood — bots send traffic directly. |
| **T1498.002** | Sub-technique: Reflection Amplification — spoofed requests to reflectors. |
| **T1499** | MITRE ATT&CK: Endpoint Denial of Service — all L7 DDoS. |
| **T1499.003** | Sub-technique: Application Exhaustion — Slowloris, RUDY, slow-rate attacks. |
| **T1583.005** | Acquire Infrastructure: Botnet — attacker builds or rents botnet. |
| **TA0040** | MITRE ATT&CK Tactic: Impact — the tactic under which all DDoS techniques fall. |

</details>

---

**Upcoming Topics — Session 12A**
Session 12A shifts to a defense-aware perspective: password cracking **countermeasures** (what stops everything I learned in 11C), active online attacks (Hydra against live SSH/FTP/RDP), passive online attacks (sniffing credentials in transit), and **keyloggers/spyware** — which capture the password *as the user types it*, before hashing ever occurs, bypassing every cryptographic defense.

**The complete chain:**
- 11A: Find the targets
- 11B: Understand the targets
- 11C: Own the targets
- 11D: Use owned targets to attack others
- **12A: Understand what stops cracking + capture credentials before they're hashed**