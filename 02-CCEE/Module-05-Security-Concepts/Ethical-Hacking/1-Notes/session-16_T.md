# Session 16A — DoS, DDoS, BOTs, BOTNETs, Smurf & SYN Flooding 💥

> Personal study notes | Ethical Hacking Module | CCEE Prep

---

## 📑 Table of Contents

- [🗺️ Where This Session Fits](#️-where-this-session-fits)
- [⚠️ Exam Traps & Misconceptions](#️-exam-traps--misconceptions)
- [🧱 Foundation Knowledge](#-foundation-knowledge)
- [Section 1 — Denial of Service Fundamentals](#section-1--denial-of-service-fundamentals)
  - [1.1 What Is DoS](#11-what-is-dos)
  - [1.2 DoS vs DDoS — Core Distinction](#12-dos-vs-ddos--core-distinction)
  - [1.3 The CIA Triad Context](#13-the-cia-triad-context)
- [Section 2 — Types of DoS Attacks](#section-2--types-of-dos-attacks)
  - [2.1 Volume-Based Attacks](#21-volume-based-attacks)
  - [2.2 Protocol Attacks](#22-protocol-attacks)
  - [2.3 Application Layer Attacks](#23-application-layer-attacks)
  - [2.4 Full DoS Attack Classification Table](#24-full-dos-attack-classification-table)
- [Section 3 — How DDoS Attacks Work](#section-3--how-ddos-attacks-work)
  - [3.1 DDoS Architecture](#31-ddos-architecture)
  - [3.2 DDoS Attack Flow](#32-ddos-attack-flow)
  - [3.3 DDoS Attack Categories](#33-ddos-attack-categories)
  - [3.4 Amplification Attacks](#34-amplification-attacks)
- [Section 4 — BOTs and BOTNETs](#section-4--bots-and-botnets)
  - [4.1 What Is a BOT](#41-what-is-a-bot)
  - [4.2 What Is a BOTNET](#42-what-is-a-botnet)
  - [4.3 BOTNET Architecture](#43-botnet-architecture)
  - [4.4 How a BOTNET Is Built](#44-how-a-botnet-is-built)
  - [4.5 BOTNET Uses Beyond DDoS](#45-botnet-uses-beyond-ddos)
  - [4.6 BOTNET Countermeasures](#46-botnet-countermeasures)
- [Section 5 — Smurf Attack](#section-5--smurf-attack)
  - [5.1 What Is a Smurf Attack](#51-what-is-a-smurf-attack)
  - [5.2 Smurf Attack Flow](#52-smurf-attack-flow)
  - [5.3 Fraggle Attack — Smurf Variant](#53-fraggle-attack--smurf-variant)
  - [5.4 Smurf Countermeasures](#54-smurf-countermeasures)
- [Section 6 — SYN Flooding](#section-6--syn-flooding)
  - [6.1 TCP Three-Way Handshake — Foundation](#61-tcp-three-way-handshake--foundation)
  - [6.2 SYN Flood Attack Mechanism](#62-syn-flood-attack-mechanism)
  - [6.3 SYN Flood Attack Flow](#63-syn-flood-attack-flow)
  - [6.4 SYN Flood Countermeasures](#64-syn-flood-countermeasures)
- [Section 7 — DoS and DDoS Countermeasures](#section-7--dos-and-ddos-countermeasures)
  - [7.1 Network-Level Countermeasures](#71-network-level-countermeasures)
  - [7.2 Host-Level Countermeasures](#72-host-level-countermeasures)
  - [7.3 ISP and Cloud-Level Countermeasures](#73-isp-and-cloud-level-countermeasures)
- [📌 Extra Notes](#-extra-notes)
  - [E1 — DoS Attack Taxonomy — Full Tree](#e1--dos-attack-taxonomy--full-tree)
  - [E2 — Famous Real-World DDoS Attacks](#e2--famous-real-world-ddos-attacks)
  - [E3 — Mirai Botnet — Case Study](#e3--mirai-botnet--case-study)
  - [E4 — SYN Cookies — Deep Dive](#e4--syn-cookies--deep-dive)
  - [E5 — Amplification Factor Reference](#e5--amplification-factor-reference)
  - [E6 — Low and Slow Attacks](#e6--low-and-slow-attacks)
  - [E7 — IRC vs HTTP vs P2P Botnet C2](#e7--irc-vs-http-vs-p2p-botnet-c2)
  - [E8 — Predecessor / Successor Chains](#e8--predecessor--successor-chains)
  - [E9 — Terminology Traps](#e9--terminology-traps)
  - [E10 — Current Landscape 2026](#e10--current-landscape-2026)
  - [E11 — Indian Legal Context](#e11--indian-legal-context)
- [Abbreviations Table](#abbreviations-table)
- [🔑 Keywords + Concept Map](#-keywords--concept-map)
- [⚡ Quick Reference Cheatsheet](#-quick-reference-cheatsheet)
- [✅ Session Revision Snapshot](#-session-revision-snapshot)
- [Next Session Bridge](#next-session-bridge)
- [📖 Glossary](#-glossary)

---

## 🗺️ Where This Session Fits

    Module 05 — Security Concepts
    └── Part B — Ethical Hacking (Sessions 6–20)
        ├── Sessions 6–9    : Concepts, Principles, Hacker Classes
        ├── Sessions 10–11  : Recon, Scanning, Enumeration, Passwords
        ├── Session 12A     : Password Countermeasures · Keyloggers
        ├── Session 12B     : Trojans · Backdoors · Reverse Shells
        ├── Session 13      : Trojan Construction · Wrapping · Evasion
        ├── Session 14      : Viruses · Worms · AV Evasion
        ├── Session 15      : Sniffing · ARP Poisoning · DNS Attacks
        ├── ▶ SESSION 16A   : DoS Types · DDoS · BOTs/BOTNETs
        │                     Smurf Attacks · SYN Flooding
        │                                          ← YOU ARE HERE
        ├── Session 16B     : Spoofing vs Hijacking · Session Hijacking
        └── Sessions 17–20  : Web Attacks · Wireless · IDS · Physical · Malware RE

**Phase position:** Session 16A focuses on **availability attacks**
— the third pillar of the CIA triad. Where Sessions 12–15 targeted
confidentiality (sniffing, credential theft) and integrity (ARP/DNS
manipulation), DoS and DDoS attacks target **availability** — making
systems and services unreachable for legitimate users.

This session establishes the volume and protocol attack landscape.
Session 16B continues with session hijacking — where the attacker
moves from disruption to active takeover of established sessions.

---

## ⚠️ Exam Traps & Misconceptions

| ❌ Misconception | ✅ Reality |
|---|---|
| DoS and DDoS are the same attack | DoS originates from a SINGLE source. DDoS originates from MULTIPLE sources (botnet) simultaneously — scale and mitigation difficulty are fundamentally different. |
| A Smurf attack directly targets the victim | A Smurf attack uses AMPLIFICATION — attacker sends a small packet to a BROADCAST ADDRESS with the victim's IP as source. The amplifier network (not the attacker) floods the victim. |
| SYN flooding requires a botnet | SYN flooding can be performed from a SINGLE machine using IP spoofing. A botnet amplifies scale but is not required. |
| DDoS attacks only consume bandwidth | DDoS includes VOLUME attacks (bandwidth), PROTOCOL attacks (exhaust state tables, firewalls, load balancers), and APPLICATION attacks (HTTP floods exhausting web server resources). |
| A BOT is always malicious | BOT simply means an automated software agent. BOTs are widely used legitimately (search engine crawlers, chat bots, monitoring agents). Malicious BOTs are called MALBOTs or zombie bots. |
| Botnets are detected easily because of high traffic | Modern botnets use SLOW, LOW-VOLUME beaconing (e.g., ping C2 every 30 minutes with small packets) — specifically designed to evade threshold-based detection. |
| SYN cookies eliminate all risk from SYN floods | SYN cookies eliminate the half-open connection table exhaustion. However, they introduce CPU overhead — very high SYN flood rates can still cause CPU exhaustion even with SYN cookies enabled. |
| A Fraggle attack is the same as a Smurf attack | Fraggle is a VARIANT of Smurf. Smurf uses ICMP Echo requests. Fraggle uses UDP packets (typically port 7 — echo or port 19 — chargen). Same amplification concept, different protocol. |
| DoS attacks require sophisticated malware | Many DoS attacks (SYN flood, UDP flood, ping flood) can be executed with simple tools like hping3, nping, or even basic scripts. Sophistication is in scale, not the attack packet itself. |
| Amplification attacks only work with DNS | DNS amplification has the highest amplification factor for well-known protocols, but NTP (556×), Memcached (51,000×), SSDP (30×), and SNMP also provide significant amplification. |

---

## 🧱 Foundation Knowledge

<details>
<summary>Click to expand — Must-know before this session</summary>

**TCP/IP Protocol Stack — Relevant for This Session**

| Layer | Protocol | Relevance |
|---|---|---|
| Layer 3 | IP, ICMP | Smurf attack (ICMP), IP spoofing |
| Layer 4 | TCP, UDP | SYN flooding (TCP), UDP flood, Fraggle (UDP) |
| Layer 7 | HTTP, DNS, NTP | Application-layer DDoS, amplification attacks |

**TCP Three-Way Handshake — Essential**

    Client          Server
      |                |
      |---- SYN ------>|   Client sends SYN (seq=x)
      |                |   Server allocates half-open connection entry
      |<-- SYN-ACK ----|   Server responds SYN-ACK (seq=y, ack=x+1)
      |                |   Server waits for ACK (in SYN_RCVD state)
      |---- ACK ------>|   Client sends ACK (ack=y+1)
      |                |   Connection fully established
      |   [DATA]       |

**Half-open connection:** After server sends SYN-ACK, it stores the
connection in a half-open connection table (backlog queue) and waits
for the final ACK. This table has a fixed size — SYN flooding fills it.

**ICMP — Relevant Packet Types**

| Type | Name | DoS Relevance |
|---|---|---|
| 0 | Echo Reply | Smurf amplification response |
| 8 | Echo Request | Smurf attack packet / Ping flood |
| 3 | Destination Unreachable | Used in some DoS scenarios |

**IP Spoofing — Foundation**
- IP source address in packet header can be freely set by attacker
- Routers historically did not verify that source IP matched
  the originating network (lack of ingress filtering)
- Enables: SYN floods (hide real source), Smurf attacks
  (forge victim's IP as source), amplification attacks
- Countermeasure: BCP38 (ingress filtering) — ISPs filter packets
  with source IPs not belonging to their customers

**ICMP Broadcast Behaviour**
- ICMP Echo Request sent to subnet BROADCAST address
- All hosts on that subnet respond with ICMP Echo Reply
- If source IP is forged (victim's IP), all replies go to victim
- This is the Smurf amplification mechanism

**MITRE ATT&CK Reference**
- T1498 — Network Denial of Service
- T1498.001 — Direct Network Flood
- T1498.002 — Reflection Amplification
- T1499 — Endpoint Denial of Service
- T1499.001 — OS Exhaustion Flood (SYN flood)
- T1583.005 — Botnet (resource acquisition)
- T1584.005 — Botnet (compromise infrastructure)

</details>

---

## Section 1 — Denial of Service Fundamentals

### 1.1 What Is DoS

**WHAT:**
A Denial of Service (DoS) attack is any attack that makes a system,
service, or network resource **unavailable to its legitimate users**
— by overwhelming it with requests, exploiting protocol weaknesses,
or consuming its critical resources until it can no longer respond.

**WHY it matters:**
Availability is one of the three pillars of the CIA triad. A system
that is unreachable — even if confidential and unmodified — has
failed its users. DoS attacks are often used:
- As standalone attacks (extortion, activism, competition disruption)
- As cover for other attacks (distract security team while breach occurs)
- As part of multi-stage attacks (DoS the authentication server →
  bypass authentication on another system)

**What attackers target:**

| Resource Targeted | How Exhausted | Example |
|---|---|---|
| **Bandwidth** | Flood with more traffic than the pipe can carry | UDP flood, DNS amplification |
| **Connection state tables** | Fill TCP half-open connection table | SYN flood |
| **CPU** | Force CPU-intensive operations | SSL handshake flood, hash collision |
| **Memory** | Exhaust RAM with connection/session state | Slowloris, connection flood |
| **Application resources** | Exhaust thread pool, database connections | HTTP flood, Slowloris |
| **Disk I/O** | Fill disk with logs or session data | Log flooding |

**Analogy:**
A DoS attack is like a flash mob blocking the entrance to a store.
The store (server) is perfectly functional. The merchandise
(data/service) is intact. But no legitimate customer can get in
because the entrance is physically blocked by an overwhelming crowd.
The store owners (admins) can't remove the crowd faster than it
re-forms.

---

### 1.2 DoS vs DDoS — Core Distinction

**DoS — Single Source:**

    Single Attacker Machine
           |
           | Flood of traffic / requests
           ↓
        Target (victim server)
        → Overwhelmed → service unavailable

**DDoS — Distributed Multiple Sources:**

    Bot 1 ──────────────┐
    Bot 2 ──────────────┤
    Bot 3 ──────────────┤──→ Target (victim server)
    Bot 4 ──────────────┤   → Overwhelmed from thousands of sources
    ...                 │   → Cannot block single IP
    Bot N ──────────────┘   → Service unavailable

| Property | DoS | DDoS |
|---|---|---|
| **Source count** | Single machine | Thousands/millions of bots |
| **Traffic volume** | Limited by one machine | Terabits per second possible |
| **IP blocking** | ✅ Block one IP — attack stopped | ❌ Blocking one IP is useless |
| **Traceability** | Easier | Very hard — bots are victims too |
| **Requires botnet?** | ❌ No | ✅ Yes (typically) |
| **Mitigation complexity** | Moderate | Very high |
| **Examples** | Ping of Death, Teardrop | Mirai DDoS, GitHub 2018 |

> [!IMPORTANT]
> The most fundamental distinction: **DoS = one source, DDoS = many
> sources.** In DDoS, the attacking machines are typically compromised
> victims (bots) — the real attacker is the botnet operator sending
> commands, not the bots themselves. This makes attribution extremely
> difficult and IP-based blocking completely ineffective.

---

### 1.3 The CIA Triad Context

| CIA Pillar | Attack Type | Example |
|---|---|---|
| **Confidentiality** | Sniffing, credential theft | ARP poisoning + Wireshark |
| **Integrity** | Data modification, DNS poisoning | MITM packet modification |
| **Availability** | DoS, DDoS | SYN flood, Smurf, DDoS botnet |

> [!NOTE]
> DoS/DDoS attacks target the **Availability** pillar exclusively.
> The attacker does not need to read or modify data — simply
> preventing access to it achieves the attack goal.
> In exam questions: "Which CIA pillar does a DoS attack violate?"
> → **Availability only.**

---

## Section 2 — Types of DoS Attacks

### 2.1 Volume-Based Attacks

**WHAT:**
Volume-based (or volumetric) attacks overwhelm the target's
**network bandwidth** — flooding the pipe with more traffic than
it can carry. The target is unreachable because its internet
connection is saturated — not because the server itself fails.

**Measured in:** Gbps (gigabits per second) or Tbps

| Attack | Protocol | Mechanism |
|---|---|---|
| **UDP Flood** | UDP | Flood random UDP ports → server sends ICMP Unreachable → both exhaust resources |
| **ICMP Flood (Ping Flood)** | ICMP | Overwhelm with ICMP Echo Requests → bandwidth consumed |
| **DNS Amplification** | UDP/DNS | Small DNS query → large response → directed at victim (using spoofed source IP) |
| **NTP Amplification** | UDP/NTP | MONLIST command → response up to 556× query size → directed at victim |
| **Smurf Attack** | ICMP | Broadcast amplification — see Section 5 |
| **Fraggle Attack** | UDP | UDP version of Smurf |
| **HTTP Flood** | TCP/HTTP | Millions of legitimate-looking HTTP requests — exhausts web server |

**UDP Flood detail:**
The attacker sends UDP packets to random ports on the target.
The target attempts to find the application listening on each port.
Finding none, it sends back ICMP "Destination Unreachable" for each.
Both the incoming flood AND the outgoing ICMP responses consume
bandwidth — double exhaustion.

---

### 2.2 Protocol Attacks

**WHAT:**
Protocol attacks exploit **weaknesses in Layer 3 and Layer 4
protocols** to consume server resources — specifically
connection state tables, CPU, and memory — rather than bandwidth.

**Measured in:** PPS (packets per second) or number of connections

| Attack | Protocol | Mechanism |
|---|---|---|
| **SYN Flood** | TCP | Half-open connections fill backlog queue → new connections refused — see Section 6 |
| **ACK Flood** | TCP | Flood with ACK packets → server must check each against connection table |
| **RST Flood** | TCP | Flood with RST packets → tear down legitimate connections |
| **Ping of Death** | ICMP | Oversized ICMP packet (>65,535 bytes) → OS buffer overflow on reassembly |
| **Teardrop Attack** | IP fragmentation | Overlapping fragment offsets → OS crash on reassembly |
| **Land Attack** | TCP | SYN packet with same source and destination IP/port → OS processing loop |
| **Fragmentation Flood** | IP | Flood with fragmented packets → reassembly table exhaustion |

**Ping of Death:**

    Normal max IP packet: 65,535 bytes
    ICMP header overhead: 8 bytes
    Max ICMP payload:     65,527 bytes

    Ping of Death sends ICMP payload > 65,527 bytes
    Split across fragments → appears valid during transit
    On reassembly at target: buffer overflow → crash/reboot

> [!NOTE]
> Ping of Death affected older OSes (Windows 95, NT, early Linux).
> Modern operating systems are patched against it. However, it
> remains MCQ-relevant as a classic protocol attack example.

**Teardrop Attack:**

    IP fragmentation uses offset values to reassemble fragments:
    Fragment 1: offset=0,  length=200 → bytes 0–199
    Fragment 2: offset=80, length=200 → bytes 80–279  ← OVERLAP

    Normal: offset=200 (start after fragment 1)
    Teardrop: offset=80 (overlapping with fragment 1)
    Reassembly algorithm confused by overlap → kernel panic/crash

---

### 2.3 Application Layer Attacks

**WHAT:**
Application layer (Layer 7) attacks target **specific application
resources** — web server thread pools, database connections, session
state, and application logic — using traffic that appears completely
legitimate to network-level defences.

**Measured in:** RPS (requests per second)

| Attack | Target | Mechanism |
|---|---|---|
| **HTTP Flood (GET/POST)** | Web server | Millions of valid HTTP requests → thread pool exhausted |
| **Slowloris** | Web server | Hold connections open with slow partial HTTP headers → connection limit exhausted |
| **Slow POST (RUDY)** | Web server | Send POST body one byte at a time → server waits → connection held |
| **SSL Exhaustion** | SSL/TLS terminator | Force repeated SSL handshakes → CPU intensive for server |
| **DNS Query Flood** | DNS server | Flood with valid DNS queries → resolver CPU/memory exhausted |
| **XML/JSON Bomb** | API server | Deeply nested XML/JSON → exponential parsing time |
| **Search Engine Flood** | Search/DB backend | Complex search queries → database CPU exhaustion |

**Slowloris detail:**
Slowloris (tool by Robert Hansen "RSnake") opens many HTTP
connections to the target web server and keeps them open by
sending partial HTTP request headers — adding a new header
line every few seconds to prevent timeout.

    GET / HTTP/1.1\r\n
    Host: target.com\r\n
    X-Custom-Header: 1\r\n     ← sent slowly, every 10 seconds
    X-Custom-Header: 2\r\n     ← another header to prevent timeout
    [never sends final \r\n to complete the request]

Apache has a default maximum concurrent connections limit.
Slowloris holds all of them open with incomplete requests —
legitimate users cannot get a connection.
Nginx is resistant (event-driven, not thread-per-connection).

> [!TIP]
> Application layer attacks are the most difficult to mitigate
> because each individual request appears completely legitimate.
> A single HTTP GET to a website's homepage looks identical
> whether it comes from a genuine user or an attacker in an HTTP
> flood. Mitigation requires rate limiting, behavioural analysis,
> and CAPTCHA challenges.

---

### 2.4 Full DoS Attack Classification Table

| Attack | Layer | Type | Amplification? | Spoofing Needed? |
|---|---|---|---|---|
| UDP Flood | 4 | Volume | ❌ | Optional |
| ICMP Flood | 3 | Volume | ❌ | Optional |
| DNS Amplification | 7 | Volume | ✅ (up to 70×) | ✅ Yes |
| NTP Amplification | 7 | Volume | ✅ (up to 556×) | ✅ Yes |
| Smurf Attack | 3 | Volume | ✅ (broadcast) | ✅ Yes |
| Fraggle Attack | 4 | Volume | ✅ (broadcast) | ✅ Yes |
| SYN Flood | 4 | Protocol | ❌ | ✅ Yes |
| Ping of Death | 3 | Protocol | ❌ | ❌ |
| Teardrop | 3 | Protocol | ❌ | ❌ |
| Land Attack | 4 | Protocol | ❌ | ✅ Yes |
| ACK Flood | 4 | Protocol | ❌ | Optional |
| HTTP Flood | 7 | Application | ❌ | ❌ |
| Slowloris | 7 | Application | ❌ | ❌ |
| SSL Exhaustion | 7 | Application | ❌ | ❌ |

---

## Section 3 — How DDoS Attacks Work

### 3.1 DDoS Architecture

**WHAT:**
A DDoS attack uses a **distributed infrastructure of compromised
machines** (botnet) to generate attack traffic simultaneously from
thousands or millions of sources — overwhelming any single-point
mitigation attempt.

**Three-tier DDoS architecture:**

    TIER 1 — Attacker (Bot Herder / Operator)
    Single person / group — sends commands
    Controls entire botnet from safe distance
             |
             | C2 commands (IRC, HTTP, P2P, encrypted)
             ↓
    TIER 2 — C2 Servers / Handlers
    Intermediate command-and-control servers
    Relay commands to bots — often bulletproof hosting
    May be compromised servers (attacker has no direct link to bots)
             |
             | "Attack target X with method Y at rate Z"
             ↓
    TIER 3 — Bots (Zombies) — thousands to millions
    Compromised victim machines running bot malware
    Execute attack commands — generate actual traffic
             |
             | Flood traffic from all bots simultaneously
             ↓
         TARGET (Victim)
         Overwhelmed from thousands of directions
         Cannot block — sources are distributed globally

---

### 3.2 DDoS Attack Flow

    PHASE 1 — Botnet Recruitment (weeks/months before attack):
      Attacker distributes bot malware (via phishing, exploits, drive-by)
      Infected machines silently join botnet
      Bots beacon to C2 periodically — await commands
      Attacker builds army of thousands/millions of bots

    PHASE 2 — Attack Preparation:
      Attacker selects target (IP, domain, service)
      Selects attack type (UDP flood, HTTP flood, SYN flood)
      Sets attack parameters (rate, duration, target port)

    PHASE 3 — Command Dissemination:
      Attacker sends command to C2 infrastructure
      C2 servers push attack command to all bots
      All bots receive: "Attack 203.0.113.1 port 80 with GET floods"

    PHASE 4 — Attack Execution:
      All bots begin sending attack traffic simultaneously
      Traffic volume: sum of all bot bandwidths
      (10,000 bots × 100Mbps each = 1 Tbps potential)
      Target overwhelmed — service unavailable

    PHASE 5 — Post-Attack:
      Attacker stops command — bots return to dormant beacon
      Bots remain compromised for future use
      Attacker is never identified — bots are the visible attackers

---

### 3.3 DDoS Attack Categories

| Category | Description | Example Attacks |
|---|---|---|
| **Volumetric** | Saturate bandwidth — measured in Gbps/Tbps | UDP flood, DNS amp, NTP amp |
| **Protocol** | Exhaust connection state — measured in PPS | SYN flood, ACK flood, fragmentation |
| **Application** | Exhaust app resources — measured in RPS | HTTP flood, Slowloris, SSL exhaustion |
| **Multi-vector** | Multiple attack types simultaneously | Volumetric + application flood |
| **Reflected** | Attacker uses third-party servers to reflect traffic at victim | DNS/NTP/SNMP amplification |
| **Pulsed / Burst** | Short intense bursts — harder to detect with sustained thresholds | Pulse wave DDoS |

---

### 3.4 Amplification Attacks

**WHAT:**
Amplification attacks exploit protocols that return a response
**significantly larger than the request** — combined with IP spoofing
to direct amplified responses at the victim.

**HOW:**

    STEP 1: Attacker spoofs source IP = Victim's IP
    STEP 2: Attacker sends small request to open amplifier server
            (DNS resolver, NTP server, Memcached server)
    STEP 3: Amplifier sends LARGE response to VICTIM's IP
            (because victim's IP is the source in the spoofed packet)
    STEP 4: Victim receives massive amplified traffic
            from thousands of innocent amplifier servers

**Amplification factor:** How many bytes of attack traffic are
generated per byte of attacker traffic.

    Attacker sends: 1 byte query
    Amplifier responds: 100 bytes to victim
    Amplification factor: 100×

| Protocol | Attack | Max Amplification Factor |
|---|---|---|
| DNS | DNS Amplification | ~70× |
| NTP | NTP MONLIST | ~556× |
| Memcached | Memcached UDP | ~51,000× |
| SNMP | SNMP GetBulk | ~650× |
| SSDP | SSDP Amplification | ~30× |
| CharGen | CharGen Flood | ~358× |
| LDAP | LDAP Amplification | ~55× |

> [!IMPORTANT]
> **Memcached amplification** (2018 — GitHub attack) achieved
> 51,000× amplification — the highest ever recorded. The GitHub
> attack peaked at 1.35 Tbps, then the record was broken days
> later at 1.7 Tbps — all from Memcached servers.

**NTP MONLIST command:**
The `MONLIST` command in older NTP servers returns the last 600
clients that communicated with the server — a large response
to a tiny request. Attacker spoofs victim IP, sends MONLIST
to thousands of NTP servers → all send large lists to victim.

---

## Section 4 — BOTs and BOTNETs

### 4.1 What Is a BOT

**WHAT:**
A BOT (short for robot) is a software program that performs
automated tasks over the internet. In the cybersecurity context,
a **malicious bot** (zombie bot / malbot) is a malware-infected
machine that has been compromised and is remotely controlled by
an attacker — executing commands without the owner's knowledge.

**Legitimate vs Malicious BOTs:**

| Category | Examples | Purpose |
|---|---|---|
| **Legitimate** | Googlebot, Bingbot | Web indexing for search engines |
| **Legitimate** | Uptime monitoring bots | Check service availability |
| **Legitimate** | Chatbots | Customer service automation |
| **Malicious** | Zombie bots in botnets | DDoS, spam, credential stuffing |
| **Malicious** | Web scraping bots | Competitive intelligence, data theft |
| **Malicious** | Click fraud bots | Fraudulent ad clicks for revenue |

**Key bot characteristics (malicious):**
- Runs silently in background — victim machine owner unaware
- Consumes minimal resources when idle — avoids detection
- Beacons to C2 periodically for new commands
- Can receive updates — malware upgrades silently
- Participates in attacks on command — then goes dormant again

---

### 4.2 What Is a BOTNET

**WHAT:**
A BOTNET (BOT network) is a **network of compromised machines
(bots)** under centralized control of a single attacker (bot
herder / bot master). The botnet collectively executes coordinated
tasks — most commonly DDoS attacks, spam campaigns, credential
harvesting, and click fraud.

**Scale of modern botnets:**

| Botnet | Peak Size | Notable Activity |
|---|---|---|
| Mirai | ~600,000 bots | Record DDoS — targeted Dyn DNS — 2016 |
| Conficker | ~10–15 million bots | Largest botnet by infected machines — 2008 |
| Bredolab | ~30 million bots | Spam distribution |
| Cutwail | ~1.5–2 million bots | Spam — 74 billion spam emails/day at peak |
| ZeroAccess | ~1.9 million bots | Click fraud — $2.7M/day revenue |
| Necurs | ~9 million bots | Ransomware + spam delivery |

---

### 4.3 BOTNET Architecture

**IRC-based (Classic):**

    Bot Herder
        |
        | connects to IRC channel
        ↓
    IRC Server (C2)
        |
        | bots join same IRC channel
        ↓
    All Bots
    Listen to channel for commands

- Simple, easy to implement
- Single point of failure — take down IRC server → botnet offline
- Modern defenders monitor IRC for botnet command patterns

**HTTP-based (Web C2):**

    Bot Herder
        |
        | sends commands via web panel
        ↓
    HTTP C2 Server (web server)
        |
        | bots poll HTTP server regularly (looks like web browsing)
        ↓
    All Bots
    GET requests to C2 URL → receive encoded commands

- Traffic blends with normal web traffic
- Harder to detect — HTTP port 80/443 rarely blocked
- More resilient than IRC (multiple C2 domains via DGA)

**P2P-based (Decentralized):**

    Bot Herder
        |
        | sends command to any bot in network
        ↓
    Bots propagate commands peer-to-peer
    (Each bot knows a subset of other bots)
        ↓
    All Bots eventually receive command

- No single C2 server — extremely resilient
- Taking down one bot/server does not kill the botnet
- Harder to infiltrate and map
- Examples: Storm Worm, Waledac, ZeroAccess

---

### 4.4 How a BOTNET Is Built

    STEP 1 — Initial Infection Vector:
      Phishing email with malware attachment
      Drive-by download (exploit kit via compromised website)
      Malicious advertising (malvertising)
      Vulnerability exploitation (unpatched OS/software)
      IoT default credential exploitation (Mirai)
      Social engineering (fake software update)

    STEP 2 — Bot Malware Installs:
      Dropped onto victim machine
      Establishes persistence (registry, scheduled task, service)
      Disables security tools if possible
      Generates unique bot ID

    STEP 3 — C2 Registration (Beaconing):
      Bot connects to C2 server
      Registers: Bot ID, victim IP, OS, capabilities, bandwidth
      Receives initial configuration
      Enters dormant state — waits for commands

    STEP 4 — Botnet Grows:
      Each bot may scan for and infect new victims
      (Worm-like spreading for self-propagating botnets)
      Bot herder also runs separate recruitment campaigns

    STEP 5 — Command and Control:
      Herder sends attack command to C2
      C2 propagates to all bots
      Bots execute: DDoS, spam, credential stuffing, etc.

---

### 4.5 BOTNET Uses Beyond DDoS

| Use Case | Description |
|---|---|
| **DDoS Attacks** | Flood target with traffic from all bots simultaneously |
| **Spam Campaigns** | Send billions of spam/phishing emails per day |
| **Credential Stuffing** | Test stolen username/password pairs at high speed |
| **Click Fraud** | Generate fraudulent ad clicks — earn pay-per-click revenue |
| **Cryptomining** | Use bot CPU resources to mine cryptocurrency |
| **Ransomware Delivery** | Deploy ransomware payload to all bots simultaneously |
| **Proxy Networks** | Route attacker's traffic through bots — anonymization |
| **CAPTCHA Solving** | Farm bots solve CAPTCHAs for credential attacks |
| **Data Exfiltration** | Steal and exfiltrate data from bot machines |
| **Brute Force** | Distributed password brute-forcing |

> [!NOTE]
> Modern botnets are multi-purpose. A botnet operator may use the
> same infrastructure for DDoS, spam, and credential stuffing —
> or rent different capabilities to different customers simultaneously
> through a Botnet-as-a-Service model on dark web markets.

---

### 4.6 BOTNET Countermeasures

| Countermeasure | What It Does |
|---|---|
| **DNS Sinkholing** | ISP/security vendor redirects C2 domain to a sinkhole server — bots connect to sinkhole instead of real C2 — neutralizes botnet |
| **Takedown operations** | Law enforcement seizes C2 servers / arrests bot herders |
| **Patch management** | Close vulnerabilities used for initial bot infection |
| **Email security** | Block phishing/malware delivery — prevent recruitment |
| **Network traffic analysis** | Detect botnet beaconing patterns — regular interval C2 callbacks |
| **BGP blackholing** | ISP drops all traffic from/to known botnet C2 IP ranges |
| **Botnet infiltration** | Security researchers join botnet (sinkhole) — map infected machines |
| **BCP38 ingress filtering** | ISPs filter spoofed IPs — reduces amplification attack effectiveness |
| **Endpoint protection** | EDR detects bot malware behavior — prevents initial infection |

---

## Section 5 — Smurf Attack

### 5.1 What Is a Smurf Attack

**WHAT:**
A Smurf attack is an ICMP-based **amplification and reflection DoS
attack** where the attacker sends a spoofed ICMP Echo Request to
a network's broadcast address — causing all hosts on that network
to simultaneously send ICMP Echo Replies to the spoofed source
IP (the victim) — flooding the victim with amplified traffic.

**Named after:** The Smurf.c exploit tool released in 1997.

**Key components:**
- **Attacker:** Sends the initial forged packet
- **Amplifier network:** Network that responds to broadcast pings
  (the "Smurf amplifier" — an unwitting third party)
- **Victim:** Receives the flood of ICMP replies

**Why it's an amplification attack:**
If the amplifier network has 200 hosts, one ICMP Echo Request
packet from the attacker generates 200 ICMP Echo Reply packets
directed at the victim. Amplification factor = number of hosts
on the amplifier network.

---

### 5.2 Smurf Attack Flow

    SETUP:
      Attacker IP:        10.0.0.100
      Victim IP:          203.0.113.5  (spoofed as source)
      Amplifier network:  192.168.1.0/24  (has 200 hosts)
      Amplifier broadcast: 192.168.1.255

    STEP 1 — Attacker constructs ICMP Echo Request:
      Source IP:      203.0.113.5  (FORGED — victim's IP)
      Destination IP: 192.168.1.255 (amplifier broadcast address)
      Type:           ICMP Echo Request (Type 8)

    STEP 2 — Packet hits amplifier network:
      All 200 hosts receive the broadcast ICMP Echo Request
      "Someone at 203.0.113.5 is pinging us — reply to them"

    STEP 3 — All 200 hosts send ICMP Echo Reply to victim:
      200 × ICMP Echo Reply packets → 203.0.113.5 (victim)
      Amplification: 1 packet → 200 packets (200× amplification)

    STEP 4 — Attacker repeats rapidly:
      At 100 packets/sec → 20,000 ICMP replies/sec at victim
      Victim's bandwidth saturated → service unavailable

    STEP 5 — Victim cannot respond — overwhelmed
      Victim has no idea it is being attacked or from where
      (replies appear to come from 200 innocent hosts)

> [!IMPORTANT]
> In a Smurf attack, the victim NEVER SENT any ICMP Echo Requests.
> The victim receives thousands of unsolicited ICMP Echo Replies
> because its IP was forged as the source in the attacker's broadcast
> packets. The amplifier network is an innocent third party.

---

### 5.3 Fraggle Attack — Smurf Variant

**WHAT:**
Fraggle is a UDP-based variant of the Smurf attack — it uses
UDP packets (typically to port 7 — echo service, or port 19 —
chargen service) instead of ICMP, sent to the broadcast address
with the victim's spoofed IP as source.

| Property | Smurf | Fraggle |
|---|---|---|
| Protocol | ICMP | UDP |
| Packet type | ICMP Echo Request (Type 8) | UDP to echo port 7 / chargen port 19 |
| Amplification | Broadcast ICMP replies | Broadcast UDP responses |
| Same concept | ✅ Yes | ✅ Yes |

> [!NOTE]
> Fraggle is less commonly used than Smurf in modern attacks because
> UDP echo and chargen services are typically disabled by default on
> modern operating systems. Both attacks rely on the same broadcast
> amplification concept — just different protocols.

---

### 5.4 Smurf Countermeasures

| Countermeasure | Implementation | What It Prevents |
|---|---|---|
| **Disable directed broadcasts** | Router: `no ip directed-broadcast` (Cisco IOS) | Prevents ICMP broadcast amplification — primary fix |
| **BCP38 ingress filtering** | ISP filters packets where source IP doesn't match originating network | Prevents IP spoofing — eliminates attack source |
| **Block broadcast pings at firewall** | Firewall rule dropping ICMP to broadcast addresses | Secondary prevention |
| **Rate limiting ICMP** | Limit ICMP responses per second on network interfaces | Limits amplification effect |
| **IDS/IPS rules** | Detect ICMP flood patterns — alert/block | Detection |

**Primary Cisco IOS countermeasure:**

    Router(config)# interface GigabitEthernet0/0
    Router(config-if)# no ip directed-broadcast

This single command on every network-facing router interface
disables directed broadcast — preventing the router from
forwarding broadcast packets to the local subnet — eliminating
the amplification capability.

> [!TIP]
> `no ip directed-broadcast` has been the **default setting** on
> Cisco IOS since version 12.0 (1997). However, older devices
> may still have it enabled — especially legacy infrastructure.
> This is frequently tested in MCQs: "What command prevents
> Smurf attacks on a Cisco router?"

---

## Section 6 — SYN Flooding

### 6.1 TCP Three-Way Handshake — Foundation

**Normal TCP connection establishment:**

    Client                          Server
       |                               |
       |------ SYN (seq=x) ---------->|  Client initiates
       |                               |  Server allocates TCB entry
       |                               |  Server enters SYN_RCVD state
       |<----- SYN-ACK (seq=y,ack=x+1)|  Server responds
       |                               |  Server waits for ACK
       |------ ACK (ack=y+1) -------->|  Client acknowledges
       |                               |  Connection ESTABLISHED
       |       [DATA TRANSFER]         |

**TCB — Transmission Control Block:**
For every half-open connection (after server sends SYN-ACK, before
receiving final ACK), the server allocates a **TCB entry** in its
**connection backlog queue** (half-open connection table).

This queue has a **fixed size** — determined by the OS parameter:
- Linux: `net.ipv4.tcp_max_syn_backlog` (default: 1024)
- Windows: configurable via registry

The server sets a **SYN timeout** — if no ACK arrives within
the timeout period (typically 75 seconds by default), the entry
is removed. But if new SYN packets arrive faster than they time
out — the queue fills completely.

---

### 6.2 SYN Flood Attack Mechanism

**WHAT:**
A SYN flood attack exploits the TCP three-way handshake by sending
a large number of **SYN packets with spoofed source IP addresses**
— causing the server to allocate half-open connection entries
and send SYN-ACK packets to spoofed IPs that never complete the
handshake — filling the backlog queue until new legitimate
connections are refused.

**WHY spoofed IPs are used:**
If the attacker uses their real IP, the server sends SYN-ACK to
the attacker — and the attacker's OS automatically sends RST
(reset) — which clears the half-open entry from the server.
By using SPOOFED IPs, no RST is ever sent → entries persist until
timeout → queue fills faster.

**WHY it works:**
The server is designed to trust the initial SYN — it immediately
allocates resources (TCB entry) before the handshake completes.
This optimistic resource allocation is the vulnerability.

---

### 6.3 SYN Flood Attack Flow

    SETUP:
      Attacker: 10.0.0.100
      Target server: 203.0.113.5 port 80
      Spoofed IPs: random (192.0.2.1, 192.0.2.2, 192.0.2.3, ...)

    STEP 1 — Attacker sends SYN flood:
      SYN → server (source: 192.0.2.1 — SPOOFED)
      SYN → server (source: 192.0.2.2 — SPOOFED)
      SYN → server (source: 192.0.2.3 — SPOOFED)
      ... thousands per second

    STEP 2 — Server processes each SYN:
      Allocates TCB entry in backlog queue
      Sends SYN-ACK to spoofed IP (192.0.2.1, 192.0.2.2, ...)
      Enters SYN_RCVD state for each
      Waits up to 75 seconds for ACK

    STEP 3 — No ACKs arrive:
      Spoofed IPs either do not exist or are real machines
      that receive unexpected SYN-ACK and send RST
      (If spoofed IPs are non-existent, no response ever)
      Backlog queue fills with SYN_RCVD entries

    STEP 4 — Backlog queue full:
      Server cannot accept new connections
      Legitimate user tries to connect → SYN sent → NO SYN-ACK
      → Connection timeout → Service appears down

    STEP 5 — Service denial:
      All legitimate TCP connections refused
      Server is otherwise healthy — just cannot accept new connections

**hping3 SYN flood example (for authorized testing only):**

    hping3 -S -p 80 --flood --rand-source 203.0.113.5

    -S        = SYN flag
    -p 80     = target port 80
    --flood   = send as fast as possible
    --rand-source = use random spoofed source IPs

---

### 6.4 SYN Flood Countermeasures

| Countermeasure | Mechanism | Effectiveness |
|---|---|---|
| **SYN Cookies** | Server does not allocate TCB until handshake complete — encodes state in SYN-ACK sequence number | ✅ High — eliminates backlog overflow |
| **Increase backlog queue size** | Increase `tcp_max_syn_backlog` | ⚠️ Buys time — does not solve problem |
| **Reduce SYN timeout** | Shorter timeout = faster cleanup of half-open entries | ⚠️ Partial — very fast floods still overwhelm |
| **Firewall SYN rate limiting** | Firewall limits SYN packets per second per source IP | ✅ Effective against single-source floods |
| **BCP38 ingress filtering** | ISP filters spoofed IPs — attacker cannot spoof | ✅ High — if universally deployed |
| **IDS/IPS detection** | Detect SYN flood pattern — block/alert | ✅ Detection |
| **DDoS mitigation services** | CloudFlare, Akamai scrubbing centers — absorb/filter | ✅ High for large-scale attacks |
| **TCP SYN Proxy (firewall)** | Firewall completes handshake on behalf of server — only forwards verified connections | ✅ High |

**SYN Cookies — Key Mechanism:**

Without SYN cookies:

    Client SYN → Server allocates TCB immediately → vulnerable

With SYN cookies:

    Client SYN →
    Server computes cookie = hash(src IP, src port, dst IP, dst port, timestamp)
    Server encodes cookie in SYN-ACK sequence number
    Server does NOT allocate TCB entry yet

    If legitimate client sends ACK:
    Server extracts cookie from ACK number
    Validates cookie → allocates TCB → connection established

    If spoofed client (no ACK received):
    No TCB was ever allocated → no memory consumed → no queue overflow

> [!IMPORTANT]
> **SYN Cookies** is the most important and widely deployed
> countermeasure for SYN flood attacks. Enabled in Linux with:
>
>     sysctl -w net.ipv4.tcp_syncookies=1
>
> The server never allocates connection state until the three-way
> handshake is complete — eliminating the half-open queue exhaustion
> vulnerability entirely.

---

## Section 7 — DoS and DDoS Countermeasures

### 7.1 Network-Level Countermeasures

| Countermeasure | What It Prevents |
|---|---|
| **Ingress filtering (BCP38)** | IP spoofing — prevents Smurf, SYN flood with spoofed IPs, amplification attacks |
| **Rate limiting** | Limits packets/requests per second from any source — throttles flood |
| **Null routing / Blackholing** | Route victim IP to null — traffic dropped at network edge — stops volumetric floods |
| **BGP remotely triggered blackhole (RTBH)** | Signal upstream ISPs to drop traffic to victim IP at their routers |
| **Access Control Lists (ACL)** | Block traffic matching attack signatures at router level |
| **Firewall SYN proxy** | Complete TCP handshake before forwarding to server — SYN flood protection |
| **QoS prioritization** | Prioritize legitimate traffic types over flood traffic |
| **Disable directed broadcasts** | `no ip directed-broadcast` — prevents Smurf amplification |
| **Disable unused UDP services** | Disable echo (7), chargen (19) — prevents Fraggle attacks |

---

### 7.2 Host-Level Countermeasures

| Countermeasure | Implementation |
|---|---|
| **SYN Cookies** | `sysctl net.ipv4.tcp_syncookies=1` (Linux) |
| **Increase backlog queue** | `sysctl net.ipv4.tcp_max_syn_backlog=4096` |
| **Reduce SYN timeout** | `sysctl net.ipv4.tcp_synack_retries=2` |
| **Limit ICMP responses** | `sysctl net.ipv4.icmp_echo_ignore_broadcasts=1` |
| **Resource limits** | Limit concurrent connections per IP at application level |
| **Web server timeout tuning** | Short connection timeouts — defeats Slowloris |
| **Patch OS and applications** | Patch against Ping of Death, Teardrop, Land attack |
| **Reverse proxy / Load balancer** | Absorbs application-layer flood before reaching origin server |

---

### 7.3 ISP and Cloud-Level Countermeasures

| Service | Provider Examples | Mechanism |
|---|---|---|
| **DDoS Scrubbing Centers** | Akamai, Cloudflare, Radware | Traffic routed through scrubbing — attack traffic removed — clean traffic forwarded |
| **Anycast Diffusion** | Cloudflare, Fastly | Attack traffic distributed across global PoPs — no single point overwhelmed |
| **Upstream BGP blackholing** | ISP | ISP drops all traffic to victim IP at their routers |
| **Content Delivery Network (CDN)** | Cloudflare, Akamai, CloudFront | Absorb and distribute traffic — massive capacity |
| **Cloud DDoS protection** | AWS Shield, Azure DDoS Protection | Auto-detect and mitigate in cloud environments |

---

## 📌 Extra Notes

### E1 — DoS Attack Taxonomy — Full Tree

> [!NOTE]
> A comprehensive taxonomy helps answer "which category does
> attack X belong to" — a very common MCQ pattern.

    DoS Attacks
    ├── Flooding Attacks
    │   ├── Volume-Based
    │   │   ├── UDP Flood
    │   │   ├── ICMP Flood (Ping Flood)
    │   │   ├── Smurf (ICMP broadcast amplification)
    │   │   └── Fraggle (UDP broadcast amplification)
    │   └── Protocol-Based
    │       ├── SYN Flood
    │       ├── ACK Flood
    │       ├── RST Flood
    │       └── Fragmentation Flood
    ├── Amplification / Reflection Attacks
    │   ├── DNS Amplification
    │   ├── NTP Amplification (MONLIST)
    │   ├── Memcached Amplification
    │   ├── SNMP Amplification
    │   └── SSDP Amplification
    ├── Protocol Exploitation Attacks
    │   ├── Ping of Death (ICMP oversized)
    │   ├── Teardrop (IP fragment overlap)
    │   ├── Land Attack (same src/dst IP)
    │   └── Bonk/Boink (fragmentation variants)
    ├── Application Layer Attacks
    │   ├── HTTP GET/POST Flood
    │   ├── Slowloris (slow headers)
    │   ├── RUDY / Slow POST (slow body)
    │   ├── SSL Exhaustion
    │   └── DNS Query Flood
    └── Distributed (DDoS)
        ├── All above attacks scaled with botnet
        └── Multi-vector (simultaneous attack types)

---

### E2 — Famous Real-World DDoS Attacks

> [!NOTE]
> Real-world case studies are directly referenced in MCQs —
> know the year, target, method, and scale for each.

**Case Study 1 — Mirai DDoS on Dyn DNS (October 2016):**
- **Target:** Dyn — major DNS provider for Twitter, Netflix, GitHub,
  Spotify, Reddit, CNN, PayPal
- **Attacker:** Mirai botnet — ~600,000 IoT devices (cameras, DVRs,
  routers) compromised via default credentials
- **Method:** DNS query flood + UDP flood against Dyn's DNS
  infrastructure — prevented clients from resolving domain names
- **Impact:** Major US and European internet disruption for hours.
  Twitter, Netflix, Spotify, Reddit inaccessible to millions.
- **Peak traffic:** ~1.2 Tbps
- **Significance:** First major attack demonstrating IoT botnet
  scale. Source code released publicly — spawned dozens of
  variants.

**Case Study 2 — GitHub DDoS (February 2018):**
- **Target:** GitHub.com
- **Method:** Memcached amplification — attackers sent 1-byte
  queries to ~50,000 Memcached servers with GitHub's IP spoofed
  as source. Servers sent large responses (up to 51,000× amplification).
- **Peak traffic:** **1.35 Tbps** — largest DDoS in history at the time
- **Duration:** ~20 minutes — mitigated by Akamai Prolexic
- **Significance:** Demonstrated Memcached as the most powerful
  amplification vector ever recorded (51,000×).

**Case Study 3 — AWS DDoS (February 2020):**
- **Target:** AWS customer (unnamed)
- **Method:** CLDAP (Connectionless LDAP) reflection amplification
- **Peak traffic:** **2.3 Tbps** — largest DDoS ever recorded at time
- **Duration:** 3 days
- **Mitigated by:** AWS Shield

**Complete Timeline:**

| Year | Target | Method | Peak | Notable |
|---|---|---|---|---|
| 2000 | Yahoo, CNN, Amazon | ICMP/UDP flood | ~1 Gbps | First major commercial DDoS wave |
| 2007 | Estonia (national infrastructure) | Botnet flood | ~90 Mbps | First nation-state-level DDoS |
| 2012 | US banks (OpAbabil) | Itsoknoproblembro botnet | ~70 Gbps | High-bandwidth sustained attack |
| 2013 | Spamhaus | DNS amplification | 300 Gbps | Record at time |
| 2016 | Dyn DNS (Mirai) | IoT UDP/DNS flood | 1.2 Tbps | IoT botnet first major use |
| 2018 | GitHub | Memcached amplification | 1.35 Tbps | Highest amplification factor |
| 2020 | AWS customer | CLDAP reflection | 2.3 Tbps | Largest ever at time |
| 2022 | Microsoft Azure | UDP flood (7 Tbps burst) | 3.47 Tbps | Current record |

---

### E3 — Mirai Botnet — Case Study

> [!NOTE]
> The Mirai botnet is explicitly referenced in the syllabus
> self-learning section — know it in detail.

**Background:**
Mirai (Japanese: "future") was a malware strain first discovered
in August 2016 — authored by three US college students (Paras Jha,
Josiah White, Dalton Norman) — originally created to knock Minecraft
servers offline for competitive advantage.

**How Mirai worked:**

    STEP 1 — Scanning:
      Mirai scanned the entire IPv4 internet randomly
      Looking for IoT devices (cameras, DVRs, routers) on common ports
      Port 23 (Telnet) — primary target
      Port 2323 (Telnet alternative)

    STEP 2 — Credential Brute Force:
      Tried 61 hardcoded default username/password combinations
      "admin/admin", "root/root", "admin/password", etc.
      IoT devices almost universally use default credentials
      Never changed by consumers

    STEP 3 — Infection:
      Successful login → download Mirai binary via wget/tftp
      Execute → bot joins Mirai botnet
      Erase itself from disk — runs entirely in memory
      (Reboot clears infection — but Mirai re-scans and re-infects)

    STEP 4 — C2 Communication:
      Bot connects to Mirai C2 servers
      Reports capabilities and bandwidth
      Awaits attack commands

    STEP 5 — Attack:
      C2 sends: "UDP flood target 8.8.8.8 port 53 for 60 seconds"
      All 600,000 bots execute simultaneously
      Target overwhelmed with Tbps-scale traffic

**Why Mirai was unprecedented:**
- IoT devices have always-on internet connections
- High bandwidth (broadband connected)
- No security software — no AV, no EDR, no logging
- Rebooting clears infection BUT device is immediately re-infected
  (Mirai scanner finds it again within minutes)
- Manufacturers used same default credentials across millions of devices

**Legal outcome:**
Paras Jha, Josiah White, Dalton Norman pleaded guilty (2017).
Given probation + community service (helped FBI investigate other
cybercrime) — no prison time due to cooperation.
Mirai source code was publicly released — spawned: Satori, Okiru,
Masuta, Reaper, JenX, Moobot, and dozens of other IoT botnets.

---

### E4 — SYN Cookies — Deep Dive

> [!NOTE]
> SYN Cookies is the most important countermeasure for SYN flooding
> — understand the cryptographic mechanism for MCQs.

**Inventor:** Daniel J. Bernstein and Eric Schenk (1996)

**The Problem:**
Server must allocate TCB memory BEFORE knowing if the client
is legitimate. Server can be exhausted with spoofed SYN packets.

**The Solution:**
Encode connection state in the SYN-ACK sequence number itself —
so no memory allocation is needed until the handshake completes.

**Cookie calculation:**

    cookie = MSB32(HMAC(
        t || src_ip || src_port || dst_ip || dst_port,
        secret_key
    ))
    where t = timestamp (current time / 64 seconds)

**Sequence:**

    SYN arrives:
      Server computes cookie (hash of 5-tuple + timestamp)
      Server sends SYN-ACK with seq = cookie
      Server discards all state — nothing stored

    ACK arrives (ack = cookie + 1):
      Server recomputes expected cookie
      If ack - 1 == expected cookie → legitimate client
      → Allocate TCB → establish connection
      If mismatch → spoofed/invalid → discard

**Limitation of SYN Cookies:**
- TCP options (window scaling, SACK) cannot be preserved in
  cookie-based connections — connection performance degraded
- Modern implementations encode limited TCP options in lower
  bits of the cookie
- Extremely high SYN rates can still cause CPU exhaustion
  from cookie computation — but vastly better than queue overflow

---

### E5 — Amplification Factor Reference

> [!NOTE]
> Amplification factors are directly tested in MCQs —
> know the relative ranking and the record holder.

| Protocol | Attack Name | Command/Method | Max Amplification |
|---|---|---|---|
| Memcached | Memcached UDP Amplification | UDP get request | **51,000×** |
| NTP | NTP MONLIST | MONLIST command | **556×** |
| SNMP | SNMP GetBulk | GetBulk request | **650×** |
| DNS | DNS Amplification | ANY/TXT query | **70×** |
| CharGen | CharGen Amplification | UDP port 19 | **358×** |
| LDAP | CLDAP Amplification | CLDAP request | **55×** |
| SSDP | SSDP Amplification | M-SEARCH request | **30×** |
| BitTorrent | BitTorrent Amplification | BT handshake | **4×** |

> [!IMPORTANT]
> Ranking for MCQs (highest to lowest):
> **Memcached (51,000×) > SNMP (650×) > NTP (556×) > CharGen
> (358×) > DNS (70×) > LDAP (55×) > SSDP (30×)**
>
> Memcached was completely unexpected as a DDoS vector — it was
> designed for internal caching, never meant to be internet-exposed.
> GitHub 2018 was the first major Memcached DDoS.

---

### E6 — Low and Slow Attacks

> [!NOTE]
> Low and slow attacks are an important application-layer DoS
> category not always covered in basic syllabus material.

**WHAT:**
Low and slow attacks use **minimal bandwidth** and send traffic
at rates far below DDoS detection thresholds — but still exhaust
server resources by holding connections open for long periods.

**Why they evade detection:**
- Traffic volume is low — no bandwidth alert triggers
- Each request is valid HTTP — no malformed packet signatures
- Source IPs may be legitimate (not bot traffic)
- Standard DDoS mitigation tools look for high volume — miss these

**Slowloris:**
- Opens many connections — sends partial HTTP headers very slowly
- Server waits for complete request (never comes)
- Holds connection open indefinitely
- Tool: slowloris.py by RSnake

**RUDY (R-U-Dead-Yet):**
- Sends legitimate HTTP POST requests
- Declares large Content-Length in header
- Sends POST body one byte every few seconds
- Server waits for complete body (never comes)
- Tool: RUDY

**Slow Read Attack:**
- Client advertises tiny TCP receive window (near zero)
- Server sends data — client acknowledges tiny chunks slowly
- Server holds connection buffers open indefinitely

**Countermeasures:**
- Set minimum request rate thresholds (reject too-slow clients)
- Set maximum connection time limits
- Nginx reverse proxy (event-driven — resistant to thread exhaustion)
- ModSecurity with RequestReadTimeout (Apache module)

---

### E7 — IRC vs HTTP vs P2P Botnet C2

> [!NOTE]
> Botnet C2 architecture comparison is frequently tested when
> MCQs ask about botnet resilience and detectability.

| Property | IRC C2 | HTTP C2 | P2P C2 |
|---|---|---|---|
| **Architecture** | Centralized (IRC server) | Centralized (web server) | Decentralized |
| **Single point of failure** | ✅ Yes | ✅ Yes | ❌ No |
| **Takedown difficulty** | Easy (seize IRC server) | Moderate (seize web server) | Very hard (no central server) |
| **Detection** | Easier (IRC traffic patterns) | Moderate (HTTP blends with normal) | Hard (P2P traffic common) |
| **Bot traffic** | IRC port 6667 — unusual | HTTP port 80/443 — normal | Various ports |
| **Resilience** | Low | Moderate (DGA helps) | Very high |
| **Historical use** | Classic botnets (1990s–2000s) | 2005–2015 | 2010s–present |
| **Examples** | EggDrop, classic bots | Zeus, SpyEye | Storm Worm, ZeroAccess |

**DGA — Domain Generation Algorithm:**
Modern HTTP botnets use DGA to generate hundreds of C2 domain names
daily. Even if defenders take down one C2 domain, the botnet
automatically moves to the next generated domain. The bot herder
only needs to register one of the generated domains each day.

---

### E8 — Predecessor / Successor Chains

> [!NOTE]
> Understanding how DoS attacks evolved helps contextualize
> modern threats and countermeasures.

**DoS/DDoS Evolution:**

    ICMP Flood / Ping Flood (1990s) — simple volume attacks
            ↓
    Smurf attack (1997) — broadcast amplification
            ↓
    TFN / TFN2K (1999) — first distributed DoS tools (DDoS)
            ↓
    Trinoo / Stacheldraht (1999) — hierarchical DDoS infrastructure
            ↓
    Mstream / Shaft (2000) — improved DDoS toolkits
            ↓
    Code Red / Nimda worm DDoS (2001) — worm-driven DDoS
            ↓
    Botnet-driven DDoS (2003+) — IRC botnet armies
            ↓
    DNS/NTP amplification (2013+) — reflection amplification
            ↓
    Mirai IoT botnet (2016) — IoT device exploitation
            ↓
    Memcached amplification (2018) — 51,000× amplification
            ↓
    Multi-vector DDoS (2019+) — simultaneous volumetric + app layer
            ↓
    AI-optimized DDoS (2024+) — adaptive attacks evading ML mitigations

**SYN Flood Countermeasure Evolution:**

    SYN flood attacks emerge (1996)
            ↓
    SYN Cookies invented — Bernstein/Schenk (1996)
            ↓
    Implemented in Linux kernel (2.2)
            ↓
    Firewall SYN proxy (mid-2000s)
            ↓
    Cloud-based SYN flood mitigation (2010s)
            ↓
    Anycast + SYN proxy at network edge (2015+)

---

### E9 — Terminology Traps

| Term | Trap | Clarification |
|---|---|---|
| **DoS vs DDoS** | "DDoS is just a bigger DoS" | STRUCTURALLY different. DDoS uses distributed BOTNET sources — not just higher volume. Mitigation approaches are completely different. |
| **Smurf uses victim's machine** | "The victim sends the ICMP broadcasts" | FALSE. The ATTACKER sends broadcast ICMP to amplifier network with VICTIM's IP spoofed as source. Victim only receives the amplified replies. |
| **SYN flood needs botnet** | "SYN flood requires DDoS infrastructure" | FALSE. SYN flood works from a SINGLE machine using IP spoofing. Botnet amplifies scale but is not required. |
| **BOT = malicious** | "All bots are malware" | FALSE. BOT means automated software agent. Search engine crawlers, monitoring bots, chatbots are all legitimate bots. Malicious bots are zombie/malware bots in botnets. |
| **Fraggle vs Smurf** | "Fraggle and Smurf are identical" | SAME CONCEPT, DIFFERENT PROTOCOL. Smurf = ICMP. Fraggle = UDP (echo port 7 / chargen port 19). |
| **SYN cookies eliminate all DoS risk** | "Enable SYN cookies = SYN-flood proof" | PARTIAL. SYN cookies eliminate backlog queue exhaustion. Very high SYN rates can still cause CPU exhaustion from cookie computation overhead. |
| **Slowloris is a bandwidth attack** | "Slowloris floods the network" | FALSE. Slowloris uses MINIMAL bandwidth — it exhausts SERVER CONNECTION SLOTS by holding connections open with slow partial requests. |
| **BCP38 prevents all DDoS** | "Implement BCP38 = DDoS prevention" | FALSE. BCP38 prevents IP SPOOFING — which helps against Smurf, SYN flood, and amplification attacks. It does NOT prevent botnet DDoS where bots use their REAL IPs. |
| **Land attack uses broadcast** | "Land attack is like Smurf" | FALSE. Land attack sends a SYN with SAME source AND destination IP — causes processing loop. Smurf uses broadcast amplification. |
| **Null routing protects the server** | "Blackholing protects availability" | PARTIAL. Null routing / blackholing stops the attack traffic from reaching the server but also stops ALL traffic to the victim IP — including legitimate users. The service is still unavailable, but downstream infrastructure is protected. |

---

### E10 — Current Landscape 2026

> [!NOTE]
> Current state of DoS/DDoS threats in 2025–2026.

**Record DDoS Attacks (2022–2025):**
- **2022 — Microsoft Azure: 3.47 Tbps** — UDP flood from approximately
  10,000 sources across Asia. Mitigated in 15 minutes by Azure
  DDoS Protection. Current record for peak bandwidth.
- **2023 — HTTP/2 Rapid Reset (CVE-2023-44487):**
  Novel application-layer DDoS exploiting HTTP/2 stream
  cancellation. Attackers open and immediately cancel HTTP/2
  streams — each cancel requires server-side processing but
  requires minimal attacker bandwidth. Reached 398 million
  requests per second (RPS) — previous record was 71 million.
  Affected Cloudflare, Google, AWS simultaneously.
- **2024 — Hyper-volumetric attacks become routine:**
  1 Tbps+ attacks now considered "mid-tier" — scrubbing centers
  routinely handle 3–5 Tbps sustained floods.

**IoT Botnet Evolution (2023–2026):**
- Mirai successors (Moobot, Dark Mirai, Reaper) continue targeting
  IoT devices. Growing attack surface: smart TVs, industrial sensors,
  medical devices, EV charging stations.
- Botnet sizes increasingly measured in millions. Estimated 15–20
  million compromised IoT devices active in botnets as of 2025.

**AI-Assisted DDoS (2024–2025):**
- ML-optimized attack patterns adapt in real time to mitigation
  responses — when a scrubbing center blocks an attack vector,
  the botnet automatically shifts to a different attack type.
- AI-generated attack traffic mimics legitimate user behaviour
  patterns — defeats statistical anomaly detection.

**Relevant CVEs:**
- **CVE-2023-44487 (HTTP/2 Rapid Reset — 2023):**
  HTTP/2 protocol implementation flaw. Affects nginx, Apache,
  Node.js, Envoy and most HTTP/2 implementations.
  Patched October 2023 with coordinated disclosure.
  CVSS 7.5. Actively exploited at massive scale before patching.
- **CVE-2024-2169 (UDP Amplification — TFTP — 2024):**
  Trivial File Transfer Protocol implementations susceptible
  to amplification attacks. Amplification factor up to 60×.

---

### E11 — Indian Legal Context

> [!NOTE]
> Indian law applicable to DoS/DDoS attacks and botnet operation.

| Law | Section | Offence | Penalty |
|---|---|---|---|
| **IT Act 2000** | **S.43(f)** | Denial of service — charging/damaging a computer by denial of legitimate access | Civil compensation up to ₹1 crore |
| **IT Act 2000** | **S.66** | Knowingly causing DoS to any computer or network | Up to 3 years + ₹5 lakh fine |
| **IT Act 2000** | **S.66F** | DoS/DDoS against critical national infrastructure (power grid, banking, defence, telecoms) with intent to threaten national security | **Life imprisonment** |
| **IT Act 2000** | **S.43(a)** | Unauthorized access via botnet C2 to victim machines | Civil ₹1 crore |
| **IPC** | **S.268** | Public nuisance — DDoS causing widespread disruption of public services | Fine + imprisonment |
| **IPC** | **S.425/426** | Mischief / damage — DDoS causing damage to computer systems | Up to 3 months + fine |
| **DPDPA 2023** | — | DDoS causes unavailability of systems holding personal data → data breach | Penalty up to ₹250 crore |

> [!IMPORTANT]
> **Section 43(f)** directly addresses DoS as a civil offence —
> "denial of service" is explicitly named. This is the specific
> provision for DoS attacks in Indian law. Combined with Section 66
> for criminal prosecution — both provisions apply simultaneously.

---

## Abbreviations Table

| Abbreviation | Full Form | One-Line Technical Meaning |
|---|---|---|
| **ACK** | Acknowledgement | TCP flag confirming receipt of data |
| **BCP38** | Best Current Practice 38 | RFC standard for ISP ingress filtering to prevent IP spoofing |
| **BGP** | Border Gateway Protocol | Internet routing protocol — used in DDoS blackholing |
| **BOT** | Robot (automated agent) | Automated software — malicious bots form botnets |
| **BOTNET** | BOT Network | Network of compromised machines under centralized attacker control |
| **C2** | Command and Control | Attacker infrastructure for managing botnet |
| **CAPTCHA** | Completely Automated Public Turing test to tell Computers and Humans Apart | Challenge-response test differentiating humans from bots |
| **CDN** | Content Delivery Network | Distributed network of servers — absorbs DDoS traffic |
| **CHARGEN** | Character Generator (protocol) | Legacy UDP service generating character data — Fraggle/amplification target |
| **CIA** | Confidentiality Integrity Availability | Security triad — DoS attacks target Availability |
| **CLDAP** | Connectionless LDAP | UDP-based LDAP — used in reflection amplification attacks |
| **DDoS** | Distributed Denial of Service | DoS attack from multiple distributed sources (botnet) |
| **DGA** | Domain Generation Algorithm | Algorithm generating rotating C2 domains for botnet resilience |
| **DoS** | Denial of Service | Attack making systems/services unavailable to legitimate users |
| **EDR** | Endpoint Detection and Response | Endpoint security platform detecting bot malware |
| **Gbps** | Gigabits per second | Unit measuring DDoS attack bandwidth |
| **ICMP** | Internet Control Message Protocol | Network diagnostic protocol — used in Smurf, ping flood, ping of death |
| **IoT** | Internet of Things | Internet-connected embedded devices — primary Mirai botnet target |
| **IRC** | Internet Relay Chat | Chat protocol — originally used for botnet C2 |
| **ISP** | Internet Service Provider | Network provider — implements BCP38 and BGP blackholing |
| **Mbps** | Megabits per second | Unit measuring network bandwidth |
| **NTP** | Network Time Protocol | Time synchronization protocol — MONLIST command enables amplification |
| **P2P** | Peer-to-Peer | Decentralized network architecture — most resilient botnet C2 model |
| **PoP** | Point of Presence | CDN/cloud network location — anycast diffusion uses many PoPs |
| **PPS** | Packets per Second | Unit measuring protocol-layer DoS attack rate |
| **RPS** | Requests per Second | Unit measuring application-layer DoS attack rate |
| **RST** | Reset | TCP flag forcibly closing a connection |
| **RTBH** | Remotely Triggered Black Hole | BGP signaling to drop attack traffic at upstream routers |
| **RUDY** | R-U-Dead-Yet | Slow POST attack tool — application-layer DoS |
| **SNMP** | Simple Network Management Protocol | Network management — GetBulk used in amplification |
| **SSDP** | Simple Service Discovery Protocol | UPnP discovery — used in amplification attacks |
| **SYN** | Synchronize | TCP flag initiating connection — exploited in SYN flooding |
| **Tbps** | Terabits per second | Unit for largest DDoS attacks |
| **TCB** | Transmission Control Block | OS data structure for each TCP connection — SYN flood exhausts these |
| **TFN** | Tribe Flood Network | Early DDoS tool (1999) — first major DDoS framework |
| **TTL** | Time to Live | IP packet field / DNS cache duration |
| **UDP** | User Datagram Protocol | Connectionless transport protocol — primary amplification attack vector |

---

## 🔑 Keywords + Concept Map

**Core Keywords:**

`DoS` · `DDoS` · `Botnet` · `Bot` · `Zombie` · `C2` · `Bot Herder` ·
`Volume Attack` · `Protocol Attack` · `Application Attack` ·
`SYN Flood` · `SYN Cookies` · `TCP Backlog` · `Half-open Connection` ·
`Smurf Attack` · `Fraggle Attack` · `ICMP Broadcast` · `Amplification` ·
`Reflection` · `IP Spoofing` · `BCP38` · `Ping of Death` · `Teardrop` ·
`Land Attack` · `UDP Flood` · `ICMP Flood` · `HTTP Flood` · `Slowloris` ·
`DNS Amplification` · `NTP Amplification` · `Memcached` · `Mirai` ·
`DGA` · `IRC C2` · `P2P Botnet` · `DNS Sinkholing` · `BGP Blackholing` ·
`hping3` · `macof` · `macof` · `RTBH` · `Scrubbing Center` ·
`T1498` · `T1499` · `T1583.005`

---

**Concept Map:**

    DoS / DDoS ATTACKS
    │
    ├── CLASSIFICATION
    │   ├── By Source ─────── DoS (single) | DDoS (distributed botnet)
    │   ├── By Layer ──────── Volume (L3/4) | Protocol (L3/4) | Application (L7)
    │   └── By Mechanism ──── Direct flood | Amplification/Reflection | Exploitation
    │
    ├── VOLUME ATTACKS
    │   ├── UDP Flood ──────── Random ports → ICMP unreachable flood back
    │   ├── ICMP Flood ─────── Ping flood — raw bandwidth saturation
    │   ├── Smurf ──────────── ICMP broadcast + IP spoof → amplified replies to victim
    │   ├── Fraggle ────────── UDP broadcast + IP spoof (variant of Smurf)
    │   └── Amplification ──── Spoof victim IP → send small query to amplifier
    │       ├── DNS (70×)
    │       ├── NTP (556×)
    │       └── Memcached (51,000×)  ← record
    │
    ├── PROTOCOL ATTACKS
    │   ├── SYN Flood ──────── Fill TCP backlog queue → new connections refused
    │   │   └── Fix: SYN Cookies — no state until handshake complete
    │   ├── Ping of Death ──── Oversized ICMP → buffer overflow on reassembly
    │   ├── Teardrop ───────── Overlapping IP fragments → crash on reassembly
    │   └── Land Attack ────── Same src/dst IP in SYN → processing loop
    │
    ├── APPLICATION ATTACKS
    │   ├── HTTP Flood ─────── Valid requests exhaust web server threads
    │   ├── Slowloris ──────── Slow headers hold connections open
    │   └── SSL Exhaustion ─── Repeated handshakes exhaust CPU
    │
    ├── BOTNETS
    │   ├── Components ─────── Herder → C2 → Bots → Target
    │   ├── C2 Models ──────── IRC (simple) | HTTP (stealthy) | P2P (resilient)
    │   ├── Recruitment ────── Phishing | Exploits | Default creds (IoT) | Drive-by
    │   ├── Uses ───────────── DDoS | Spam | Credential stuffing | Cryptomining
    │   └── Mirai example ──── IoT default creds → 600K bots → 1.2 Tbps
    │
    └── COUNTERMEASURES
        ├── Network ────────── BCP38 | Rate limiting | Blackholing | RTBH
        ├── Host ───────────── SYN Cookies | Reduce timeout | Backlog increase
        ├── Amplification ──── Disable directed broadcast | Disable MONLIST
        └── DDoS scale ─────── Scrubbing centers | CDN | Anycast | Cloud DDoS

---

## ⚡ Quick Reference Cheatsheet

### ⚔️ DoS Attack Type Reference

| Attack | Layer | Type | Spoofing | Amplification | Classic Tool |
|---|---|---|---|---|---|
| UDP Flood | 4 | Volume | Optional | ❌ | hping3, nping |
| ICMP Flood | 3 | Volume | Optional | ❌ | ping, hping3 |
| Smurf | 3 | Volume | ✅ Required | ✅ Broadcast | smurf.c |
| Fraggle | 4 | Volume | ✅ Required | ✅ Broadcast | — |
| DNS Amplification | 7 | Volume | ✅ Required | ✅ 70× | — |
| NTP Amplification | 7 | Volume | ✅ Required | ✅ 556× | ntpdc |
| Memcached Amp | 7 | Volume | ✅ Required | ✅ 51,000× | — |
| SYN Flood | 4 | Protocol | ✅ Required | ❌ | hping3 |
| Ping of Death | 3 | Protocol | ❌ | ❌ | ping -s 65510 |
| Teardrop | 3 | Protocol | ❌ | ❌ | teardrop.c |
| Land Attack | 4 | Protocol | ✅ Required | ❌ | land.c |
| ACK Flood | 4 | Protocol | Optional | ❌ | hping3 |
| HTTP Flood | 7 | Application | ❌ | ❌ | LOIC, HOIC |
| Slowloris | 7 | Application | ❌ | ❌ | slowloris.py |
| SSL Exhaustion | 7 | Application | ❌ | ❌ | THC-SSL-DOS |

---

### 🤖 Botnet C2 Architecture Comparison

| Property | IRC | HTTP | P2P |
|---|---|---|---|
| Central server? | ✅ Yes | ✅ Yes | ❌ No |
| Single point of failure? | ✅ Yes | ✅ Yes | ❌ No |
| Takedown ease | Easy | Moderate | Very hard |
| Traffic detectability | High | Low | Medium |
| Resilience | Low | Medium (DGA) | Very high |
| Port | 6667 | 80/443 | Various |
| Examples | Classic bots | Zeus, SpyEye | Storm, ZeroAccess |

---

### 🦟 Amplification Factor Ranking

| Rank | Protocol | Max Amplification |
|---|---|---|
| 1 | **Memcached** | **51,000×** |
| 2 | **SNMP** | **650×** |
| 3 | **NTP** | **556×** |
| 4 | **CharGen** | **358×** |
| 5 | **DNS** | **70×** |
| 6 | **LDAP/CLDAP** | **55×** |
| 7 | **SSDP** | **30×** |

---

### 🛡️ SYN Flood Countermeasures

| Countermeasure | Effectiveness | Notes |
|---|---|---|
| SYN Cookies | ✅ High | Primary fix — eliminates backlog overflow |
| Firewall SYN Proxy | ✅ High | Completes handshake on behalf of server |
| BCP38 ingress filter | ✅ High | Prevents IP spoofing at ISP level |
| Increase backlog | ⚠️ Partial | Buys time only |
| Reduce SYN timeout | ⚠️ Partial | Partial relief |
| Rate limiting (firewall) | ✅ Good | Per-source rate limiting |
| DDoS scrubbing | ✅ High | For large-scale distributed SYN floods |

---

### 🌊 Smurf Attack Components

| Component | Role | IP Used |
|---|---|---|
| Attacker | Sends forged ICMP broadcast | Real attacker IP (hidden by spoof) |
| Amplifier network | Hosts that respond to broadcast ping | Amplifier network broadcast |
| Victim | Receives amplified ICMP replies | Victim IP (spoofed as source) |

**Primary Cisco countermeasure:**

    Router(config-if)# no ip directed-broadcast

---

### ⚖️ Indian Legal Reference

| Law | Section | Offence | Penalty |
|---|---|---|---|
| IT Act 2000 | S.43(f) | Denial of service (civil) | ₹1 crore |
| IT Act 2000 | S.66 | Criminal DoS | 3 yrs + ₹5L |
| IT Act 2000 | S.66F | DoS on critical infrastructure | Life imprisonment |
| IPC | S.425/426 | Damage via DDoS | 3 months + fine |
| DPDPA 2023 | — | Data breach via DoS-caused outage | ₹250 crore |

---

### 📅 Famous DDoS Attacks Timeline

| Year | Target | Method | Peak |
|---|---|---|---|
| 2000 | Yahoo, CNN, Amazon | Botnet flood | ~1 Gbps |
| 2007 | Estonia | Botnet | 90 Mbps |
| 2013 | Spamhaus | DNS amplification | 300 Gbps |
| 2016 | Dyn DNS | Mirai IoT UDP flood | 1.2 Tbps |
| 2018 | GitHub | Memcached (51,000×) | 1.35 Tbps |
| 2020 | AWS customer | CLDAP reflection | 2.3 Tbps |
| 2022 | Azure customer | UDP flood | 3.47 Tbps |
| 2023 | Cloudflare/Google/AWS | HTTP/2 Rapid Reset | 398M RPS |

---

## ✅ Session Revision Snapshot

### ⚡ TL;DR — 5 Bullets

1. **DoS = single source; DDoS = multiple botnet sources simultaneously.**
   DDoS is not just "bigger DoS" — it is structurally different.
   IP blocking defeats DoS but is useless against DDoS.
   The CIA triad pillar targeted by both is **Availability only**.

2. **Smurf attack = IP spoofing + ICMP broadcast amplification.**
   Attacker forges victim's IP as source → sends ICMP Echo to
   broadcast address → ALL hosts on amplifier network reply to victim.
   Fix: `no ip directed-broadcast` on every router interface.
   Fraggle = same concept with UDP instead of ICMP.

3. **SYN flood exploits TCP's optimistic resource allocation.**
   Server allocates TCB entry after every SYN before handshake
   completes. Spoofed SYNs fill the backlog — no final ACK arrives
   — queue full — new connections refused. Fix: **SYN Cookies** —
   server encodes state in sequence number — no memory allocation
   until handshake complete.

4. **Botnets have three-tier architecture: Herder → C2 → Bots.**
   C2 can be IRC (simple, detectable), HTTP (stealthy, common),
   or P2P (resilient, hardest to take down). Mirai infected 600K
   IoT devices via 61 default credential pairs — reached 1.2 Tbps
   against Dyn DNS. Memcached amplification achieves 51,000× —
   the highest amplification factor ever recorded.

5. **Three DoS categories: Volume (bandwidth), Protocol (state tables),
   Application (resources).** Amplification attacks require IP
   spoofing and exploit protocols returning large responses to
   small queries. BCP38 ingress filtering at ISPs is the primary
   countermeasure against spoofing-based attacks (Smurf, SYN flood,
   amplification). SYN Cookies address protocol-level SYN floods.

---

### 🎯 MCQ-Likely Concepts

- [ ] DoS vs DDoS — single vs multiple sources
- [ ] CIA triad — DoS attacks target Availability only
- [ ] Smurf attack — components, mechanism, amplifier role
- [ ] `no ip directed-broadcast` — Smurf countermeasure (Cisco)
- [ ] Fraggle — UDP variant of Smurf
- [ ] SYN flood — TCP backlog queue exhaustion mechanism
- [ ] SYN Cookies — how they work, Linux command to enable
- [ ] Half-open connection — SYN_RCVD state, TCB entry
- [ ] Why spoofed IPs are used in SYN flooding
- [ ] Botnet three-tier architecture — Herder → C2 → Bots
- [ ] IRC vs HTTP vs P2P C2 — resilience comparison
- [ ] Mirai botnet — IoT devices, 61 default credentials, Dyn DNS attack
- [ ] Memcached amplification — 51,000× — record amplification factor
- [ ] NTP MONLIST — 556× amplification
- [ ] DNS amplification — 70× amplification
- [ ] Amplification factor ranking — Memcached > SNMP > NTP > DNS
- [ ] DDoS categories — volumetric (Gbps) | protocol (PPS) | application (RPS)
- [ ] Ping of Death — oversized ICMP → buffer overflow
- [ ] Teardrop — overlapping IP fragments → crash
- [ ] Land Attack — same source and destination IP in SYN
- [ ] Slowloris — slow HTTP headers — minimal bandwidth
- [ ] BCP38 — ingress filtering — prevents IP spoofing
- [ ] DNS Sinkholing — botnet C2 neutralization
- [ ] BGP RTBH — remote triggered blackholing
- [ ] hping3 — SYN flood testing tool
- [ ] IT Act S.43(f) — DoS as civil offence
- [ ] IT Act S.66F — DoS on critical infrastructure = life imprisonment
- [ ] GitHub 2018 DDoS — Memcached — 1.35 Tbps

---

### 💼 Interview-Likely

- Explain the difference between DoS and DDoS with a technical example.
- Walk me through how a Smurf attack works step by step.
- Why are spoofed IP addresses used in SYN flooding?
- What are SYN cookies and how do they prevent SYN flooding?
- Explain the three-tier architecture of a DDoS botnet.
- How did Mirai achieve such unprecedented DDoS scale?
- What is amplification factor and which protocol holds the record?
- Compare IRC, HTTP, and P2P botnet C2 — which is most resilient and why?
- What is BCP38 and why hasn't it been universally adopted?
- Explain the difference between volumetric, protocol, and application-layer DDoS.

---

## Next Session Bridge

Session 16A covered availability attacks — specifically the techniques
that overwhelm, exhaust, or flood systems and networks into
unavailability. The key thread was resource exhaustion: bandwidth
(volumetric), state tables (protocol), and application resources.

Session 16B moves from disruption to **takeover** — specifically
**session hijacking**. Where DoS prevents access to services,
session hijacking allows an attacker to actively TAKE OVER an
existing, authenticated session. The TCP sequence number knowledge
from SYN flooding directly applies here — TCP session hijacking
exploits predictable sequence numbers to inject packets into an
established connection. Spoofing vs hijacking is also a critical
distinction: spoofing fakes an identity for a transaction, hijacking
steals an ongoing authenticated session.

---

<details>
<summary>📖 Glossary</summary>

| Term | Definition |
|---|---|
| **ACK Flood** | DDoS attack flooding target with TCP ACK packets — forces connection table lookups |
| **Amplification Attack** | DDoS technique using protocols that return large responses to small queries — with victim's IP spoofed as source |
| **Anycast** | Network addressing where same IP announced from multiple locations — used by CDNs to distribute DDoS |
| **BCP38** | Best Current Practice 38 — RFC 2827 — ISP ingress filtering to block spoofed source IPs |
| **BGP Blackholing** | Routing protocol signaling to drop all traffic to a specific IP prefix |
| **Bot** | Automated software agent — malicious bot is a compromised machine in a botnet |
| **Bot Herder** | Attacker who controls and operates a botnet |
| **Botnet** | Network of compromised machines (bots/zombies) under centralized attacker control |
| **C2** | Command and Control — infrastructure through which attacker manages botnet |
| **CharGen** | Character Generator Protocol — UDP port 19 — used in amplification attacks |
| **DDoS** | Distributed Denial of Service — DoS attack from multiple distributed sources |
| **DGA** | Domain Generation Algorithm — generates rotating C2 domain names for botnet resilience |
| **Directed Broadcast** | IP broadcast directed at specific network subnet — used in Smurf attacks |
| **DoS** | Denial of Service — any attack making systems unavailable to legitimate users |
| **Fraggle** | UDP variant of Smurf attack — broadcasts to UDP echo/chargen services |
| **GitHub DDoS 2018** | 1.35 Tbps Memcached amplification attack — record at time |
| **Half-open Connection** | TCP connection where server has sent SYN-ACK but not yet received final ACK |
| **hping3** | Network packet crafting tool — used for SYN flood testing |
| **HTTP Flood** | Application-layer DDoS sending millions of valid HTTP requests |
| **Land Attack** | DoS attack sending SYN with identical source and destination IP/port |
| **Memcached** | In-memory caching system — when internet-exposed, achieves 51,000× DDoS amplification |
| **Mirai** | IoT botnet (2016) — exploited default credentials — 600K bots — 1.2 Tbps DDoS against Dyn |
| **MONLIST** | NTP command returning last 600 clients — enables 556× amplification |
| **NTP** | Network Time Protocol — MONLIST command enables amplification DDoS |
| **Null Routing** | Routing attack traffic to null interface — packets dropped — stops volumetric floods |
| **Ping of Death** | DoS attack using oversized ICMP packet causing buffer overflow on reassembly |
| **P2P Botnet** | Decentralized botnet where bots communicate peer-to-peer — most resilient architecture |
| **RTBH** | Remotely Triggered Black Hole — BGP mechanism to signal upstream traffic dropping |
| **RUDY** | R-U-Dead-Yet — slow POST attack tool — sends HTTP body one byte at a time |
| **Scrubbing Center** | Network facility that absorbs DDoS traffic, removes attack packets, forwards clean traffic |
| **Slowloris** | Low-bandwidth DoS tool holding HTTP connections open with slow partial headers |
| **Smurf Attack** | ICMP broadcast amplification DoS — forged source IP directs amplified replies to victim |
| **SSDP** | Simple Service Discovery Protocol — used in UPnP — enables 30× DDoS amplification |
| **SYN Cookie** | TCP countermeasure encoding connection state in sequence number — prevents backlog exhaustion |
| **SYN Flood** | TCP DoS attack filling server connection backlog with spoofed SYN packets |
| **SYN_RCVD** | TCP state after server sends SYN-ACK — awaiting final ACK — half-open state |
| **TCB** | Transmission Control Block — OS data structure allocated per TCP connection |
| **Teardrop** | DoS attack using overlapping IP fragment offsets causing crash on reassembly |
| **TFN** | Tribe Flood Network — early DDoS tool (1999) — first hierarchical DDoS framework |
| **UDP Flood** | Volumetric DDoS sending UDP packets to random ports — target sends ICMP unreachable |
| **Zombie** | Compromised bot machine in a botnet — executes attacker commands unknowingly |

</details>

---