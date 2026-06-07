# Session 15 — Sniffing, ARP Poisoning, MAC Flooding & DNS Attacks 🔍

> Personal study notes | Ethical Hacking Module | CCEE Prep

---

## 📑 Table of Contents

- [🗺️ Where This Session Fits](#️-where-this-session-fits)
- [⚠️ Exam Traps & Misconceptions](#️-exam-traps--misconceptions)
- [🧱 Foundation Knowledge](#-foundation-knowledge)
- [Section 1 — Sniffing Fundamentals](#section-1--sniffing-fundamentals)
  - [1.1 What Is Sniffing](#11-what-is-sniffing)
  - [1.2 Passive Sniffing](#12-passive-sniffing)
  - [1.3 Active Sniffing](#13-active-sniffing)
  - [1.4 Passive vs Active — Full Comparison](#14-passive-vs-active--full-comparison)
- [Section 2 — Protocols Susceptible to Sniffing](#section-2--protocols-susceptible-to-sniffing)
  - [2.1 Why Some Protocols Are Vulnerable](#21-why-some-protocols-are-vulnerable)
  - [2.2 Vulnerable Protocols — Full Reference](#22-vulnerable-protocols--full-reference)
  - [2.3 Secure Alternatives](#23-secure-alternatives)
- [Section 3 — ARP Poisoning](#section-3--arp-poisoning)
  - [3.1 ARP Fundamentals](#31-arp-fundamentals)
  - [3.2 How ARP Poisoning Works](#32-how-arp-poisoning-works)
  - [3.3 ARP Poisoning Attack Flow](#33-arp-poisoning-attack-flow)
  - [3.4 What an Attacker Can Do After ARP Poisoning](#34-what-an-attacker-can-do-after-arp-poisoning)
  - [3.5 ARP Poisoning Tools](#35-arp-poisoning-tools)
  - [3.6 ARP Poisoning Countermeasures](#36-arp-poisoning-countermeasures)
- [Section 4 — MAC Flooding](#section-4--mac-flooding)
  - [4.1 How Switches Work — Foundation](#41-how-switches-work--foundation)
  - [4.2 MAC Flooding Attack](#42-mac-flooding-attack)
  - [4.3 MAC Flooding Attack Flow](#43-mac-flooding-attack-flow)
  - [4.4 MAC Flooding Tools](#44-mac-flooding-tools)
  - [4.5 MAC Flooding Countermeasures](#45-mac-flooding-countermeasures)
- [Section 5 — DNS Spoofing and DNS Hacking](#section-5--dns-spoofing-and-dns-hacking)
  - [5.1 DNS Fundamentals](#51-dns-fundamentals)
  - [5.2 DNS Spoofing](#52-dns-spoofing)
  - [5.3 DNS Cache Poisoning](#53-dns-cache-poisoning)
  - [5.4 DNS Hacking Techniques](#54-dns-hacking-techniques)
  - [5.5 DNS Attack Tools](#55-dns-attack-tools)
  - [5.6 DNS Attack Countermeasures](#56-dns-attack-countermeasures)
- [Section 6 — Wireshark / Ethereal Capture and Display Filters](#section-6--wireshark--ethereal-capture-and-display-filters)
  - [6.1 Wireshark Overview](#61-wireshark-overview)
  - [6.2 Capture Filters](#62-capture-filters)
  - [6.3 Display Filters](#63-display-filters)
  - [6.4 Practical Sniffing Workflow](#64-practical-sniffing-workflow)
- [Section 7 — Sniffing Countermeasures](#section-7--sniffing-countermeasures)
  - [7.1 Encryption-Based Countermeasures](#71-encryption-based-countermeasures)
  - [7.2 Network-Level Countermeasures](#72-network-level-countermeasures)
  - [7.3 Detection of Sniffing](#73-detection-of-sniffing)
  - [7.4 Organisational Countermeasures](#74-organisational-countermeasures)
- [📌 Extra Notes](#-extra-notes)
  - [E1 — How Ethernet Works at the Frame Level](#e1--how-ethernet-works-at-the-frame-level)
  - [E2 — Hub vs Switch vs Router — Sniffing Implications](#e2--hub-vs-switch-vs-router--sniffing-implications)
  - [E3 — MITM Attack — Full Picture](#e3--mitm-attack--full-picture)
  - [E4 — ARP Protocol Deep Dive](#e4--arp-protocol-deep-dive)
  - [E5 — Gratuitous ARP](#e5--gratuitous-arp)
  - [E6 — DNS Protocol Deep Dive](#e6--dns-protocol-deep-dive)
  - [E7 — Kaminsky DNS Cache Poisoning Attack](#e7--kaminsky-dns-cache-poisoning-attack)
  - [E8 — Promiscuous Mode Detection](#e8--promiscuous-mode-detection)
  - [E9 — Predecessor / Successor Chains](#e9--predecessor--successor-chains)
  - [E10 — Terminology Traps](#e10--terminology-traps)
  - [E11 — Current Landscape 2026](#e11--current-landscape-2026)
  - [E12 — Indian Legal Context](#e12--indian-legal-context)
- [Abbreviations Table](#abbreviations-table)
- [🔑 Keywords + Concept Map](#-keywords--concept-map)
- [⚡ Quick Reference Cheatsheet](#-quick-reference-cheatsheet)
- [✅ Session Revision Snapshot](#-session-revision-snapshot)
- [Next Session Bridge](#next-session-bridge)
- [📖 Glossary](#-glossary)

---

## 🗺️ Where This Session Fits

```text
Module 05 — Security Concepts
└── Part B — Ethical Hacking (Sessions 6–20)
    ├── Sessions 6–9 : Concepts, Principles, Hacker Classes
    ├── Sessions 10–11 : Recon, Scanning, Enumeration, Passwords, DDoS
    ├── Session 12A : Password Countermeasures · Keyloggers · Spyware
    ├── Session 12B : Trojans · Backdoors · Types · Reverse Shells
    ├── Session 13 : Trojan Construction Kits · Wrapping · Evasion
    ├── Session 14 : Viruses · Worms · AV Evasion · Detection Methods
    ├── ▶ SESSION 15 : Sniffing · ARP Poisoning · MAC Flooding
    │                  DNS Spoofing · DNS Hacking · Countermeasures
    │                  ← YOU ARE HERE
    └── Sessions 16–20 : DoS/DDoS, Session Hijacking, Web Attacks,
                         Wireless Hacking, IDS, Physical Security, Malware RE
```

**Phase position:** Session 15 shifts the attack surface from the
endpoint (viruses, Trojans) to the **network communication channel**.
Where previous sessions attacked systems directly, sniffing attacks
the **traffic flowing between systems** — intercepting and manipulating
communication that participants believe is private.

This session introduces the **MITM (Man-in-the-Middle)** class of
attacks at the network layer. ARP poisoning and MAC flooding are the
mechanisms that make active sniffing possible on switched networks.
DNS attacks extend the principle — manipulating name resolution to
redirect victims to attacker-controlled destinations.

---

## ⚠️ Exam Traps & Misconceptions

| ❌ Misconception | ✅ Reality |
|---|---|
| Sniffing only works on hub-based networks | Passive sniffing works on hub networks. On SWITCHED networks, the attacker needs ACTIVE sniffing (ARP poisoning, MAC flooding) to capture traffic not destined for them. |
| ARP poisoning and MAC flooding achieve the same thing | They work differently. MAC flooding exploits SWITCH CAM table overflow → switch degrades to hub behaviour. ARP poisoning sends fake ARP replies to poison endpoint ARP caches directly. Both enable sniffing on switched networks but via completely different mechanisms. |
| ARP poisoning requires the attacker to respond to ARP requests | ARP is STATELESS — a host will accept an ARP reply even if it NEVER SENT AN ARP REQUEST. Attackers send UNSOLICITED (gratuitous) ARP replies to poison caches without waiting for a query. |
| DNS spoofing and DNS cache poisoning are different attacks | DNS spoofing is the general technique of providing false DNS responses. DNS CACHE POISONING is a specific sub-technique where the false records are stored in the DNS resolver's cache — affecting ALL users of that resolver, not just one victim. |
| Wireshark capture filters and display filters work the same way | Capture filters are applied AT CAPTURE TIME using BPF syntax — they determine what traffic is recorded. Display filters are applied to ALREADY CAPTURED traffic using Wireshark's own filter language. Different syntax, different timing, different purpose. |
| A NIC in promiscuous mode means the machine is being attacked | Promiscuous mode simply means the NIC captures ALL frames, not just those addressed to it. It is also set legitimately by network monitoring tools, IDS sensors, and administrators performing diagnostics. |
| Switching to a switched network prevents all sniffing | Switched networks prevent PASSIVE sniffing. Active sniffing techniques (ARP poisoning, MAC flooding, DHCP spoofing) enable sniffing on switched networks. |
| Ethereal and Wireshark are different tools | Ethereal was renamed to **Wireshark** in 2006. They are the same tool. Exam questions may use either name — treat them as identical. |
| DNSSEC prevents DNS spoofing completely | DNSSEC signs DNS records cryptographically — making record tampering detectable. However, DNSSEC adoption is incomplete globally, and misconfigurations can still leave gaps. |
| ARP operates at Layer 3 (Network Layer) | ARP operates between Layer 2 and Layer 3 — it maps Layer 3 IP addresses to Layer 2 MAC addresses. It is often classified as Layer 2.5 or as part of the Data Link layer in practice. |

---

## 🧱 Foundation Knowledge

<details>
<summary>Click to expand — Must-know before this session</summary>

**OSI Model — Relevant Layers for This Session**

| Layer | Name | Relevant Protocol/Concept |
|---|---|---|
| Layer 2 | Data Link | MAC addresses, Ethernet frames, ARP, switches, CAM table |
| Layer 3 | Network | IP addresses, routing, ARP resolution |
| Layer 4 | Transport | TCP/UDP ports — used in Wireshark filters |
| Layer 7 | Application | DNS, HTTP, FTP, Telnet — cleartext protocols |

**MAC Address Structure**
- 48-bit hardware address burned into NIC
- Format: `XX:XX:XX:XX:XX:XX` (hexadecimal)
- First 3 bytes = OUI (Organizationally Unique Identifier — manufacturer)
- Last 3 bytes = device-specific identifier
- Broadcast MAC: `FF:FF:FF:FF:FF:FF` — received by ALL devices on segment
- Local MAC: specific device address — only that NIC processes the frame

**How a Switch Forwards Frames**
- Switch maintains a **CAM (Content Addressable Memory) table**
  also called MAC address table or forwarding table
- CAM table maps: `MAC address → port number`
- When frame arrives: switch checks source MAC → adds to CAM table
- Destination lookup: if MAC found → forward to that port only
- If MAC NOT found → **flood** frame to ALL ports (like a hub)
- This flooding on unknown MAC is what MAC flooding exploits

**How ARP Works — Basics**
- ARP = Address Resolution Protocol
- Purpose: resolve IP address → MAC address on local network
- Operation: broadcast "Who has IP X? Tell me, IP Y"
  → target replies: "IP X is at MAC AA:BB:CC:DD:EE:FF"
- ARP cache: each host stores recent IP→MAC mappings
- ARP is STATELESS — accepts replies without requiring a prior request

**DNS Resolution — Basics**
- DNS = Domain Name System — resolves hostnames to IP addresses
- Client asks resolver: "What is the IP of www.example.com?"
- Resolver asks root → TLD → authoritative NS → gets answer
- Resolver caches answer for TTL duration
- Client receives IP → connects to that IP

**MITRE ATT&CK Reference**
- T1040 — Network Sniffing
- T1557 — Adversary-in-the-Middle
- T1557.002 — ARP Cache Poisoning
- T1498 — Network Denial of Service (MAC flooding aspect)
- T1584.002 — DNS (infrastructure for DNS attacks)
- T1071.004 — Application Layer Protocol: DNS

</details>

---

## Section 1 — Sniffing Fundamentals

### 1.1 What Is Sniffing

**WHAT:**
Network sniffing (also called packet sniffing, network eavesdropping,
or wire sniffing) is the technique of **capturing and analyzing network
packets** as they travel across a network segment — including packets
not addressed to the attacker's machine.

**WHY it works:**
Ethernet was designed for efficiency and connectivity — not
confidentiality. In its original form, every device on a shared
network segment receives every frame transmitted. The NIC was
designed to filter frames by MAC address and discard those not
addressed to it — but this filtering can be disabled.

**Legitimate uses of sniffing:**
- Network troubleshooting and diagnostics
- Performance monitoring and capacity planning
- Intrusion detection (IDS sensors sniff all traffic)
- Protocol analysis and development
- Security assessments and penetration testing

**Malicious uses of sniffing:**
- Capturing credentials (username/password) from cleartext protocols
- Session token theft (HTTP cookies)
- Email content interception (POP3, IMAP, SMTP without TLS)
- VoIP call interception
- Database query capture
- Reconnaissance — topology mapping

**Analogy:**
Network sniffing is like standing at a busy postal sorting office.
All letters (packets) pass through the same conveyor belt. A
legitimate postal worker reads only letters addressed to their
delivery area. A sniffing attacker reads every letter on the
belt — including those addressed to someone else — just by
putting their hands in and grabbing them.

**MITRE ATT&CK:** T1040 — Network Sniffing

---

### 1.2 Passive Sniffing

**WHAT:**
Passive sniffing captures network traffic **without sending any
additional packets** — the attacker's machine simply listens.
The NIC is placed in **promiscuous mode** — causing it to accept
ALL frames on the network segment, not just those addressed to
its own MAC address.

**WHY it works (and where):**
Passive sniffing exploits the shared nature of certain network
architectures — specifically **hub-based (shared Ethernet) networks**.

On a hub:

```text
Device A sends packet to Device B
        ↓
Hub receives packet → broadcasts to ALL ports
        ↓
Device B, Device C, Device D, Attacker — ALL receive the frame
        ↓
Device B, C, D: NIC sees MAC ≠ its own → discards frame
Attacker: NIC in promiscuous mode → accepts ALL frames → sniffs
```

**Where passive sniffing works:**
- Hub-based networks (rare today — hubs are obsolete)
- Wireless networks (Wi-Fi — radio waves broadcast to all)
- Network segments with port mirroring (SPAN port) configured
- Virtual switch environments with promiscuous port configured

**Characteristics:**

| Property | Detail |
|---|---|
| Traffic generated | ❌ None — purely passive |
| Detectability | Very difficult — attacker generates no traffic |
| Requires network modification | ❌ No |
| Works on switched networks | ❌ No (without additional techniques) |
| Works on hub/wireless | ✅ Yes |

> [!NOTE]
> Passive sniffing is the **most stealthy** sniffing method because
> the attacker generates zero additional network traffic. There is
> nothing to detect on the wire. However, it only works on shared
> media (hubs, Wi-Fi) or with physical/logical access to all traffic.

---

### 1.3 Active Sniffing

**WHAT:**
Active sniffing uses **attack techniques to force network traffic
through the attacker's machine** on a switched network — where
passive sniffing cannot work because switches isolate traffic
to individual ports.

**WHY it's needed:**
On switched networks, the switch only sends frames to the specific
port where the destination MAC is connected. The attacker's port
receives only broadcast traffic and traffic addressed to the
attacker's own MAC. Without active intervention, there is
nothing to sniff.

**Active sniffing techniques:**

| Technique | How It Forces Traffic to Attacker |
|---|---|
| **ARP Poisoning / ARP Spoofing** | Sends fake ARP replies → poisons victims' ARP caches → traffic sent to attacker's MAC |
| **MAC Flooding** | Floods switch CAM table → switch fails open → broadcasts all traffic like a hub |
| **DHCP Spoofing** | Attacker acts as rogue DHCP server → configures victims to use attacker as gateway |
| **DNS Spoofing** | Redirects victims to attacker-controlled IPs via false DNS responses |
| **ICMP Redirect** | Sends ICMP redirect messages → victims update routing tables → traffic sent via attacker |
| **Port Stealing** | Sends frames with victim's source MAC → switch maps victim's MAC to attacker's port |

**Characteristics:**

| Property | Detail |
|---|---|
| Traffic generated | ✅ Yes — sends forged packets |
| Detectability | Higher — generates anomalous traffic patterns |
| Requires network modification | ✅ Yes — manipulates ARP/CAM/DNS |
| Works on switched networks | ✅ Yes — this is the entire purpose |

---

### 1.4 Passive vs Active — Full Comparison

| Property | Passive Sniffing | Active Sniffing |
|---|---|---|
| **Traffic sent by attacker** | ❌ None | ✅ Yes — forged packets |
| **Works on hubs** | ✅ Yes | ✅ Yes (not needed but works) |
| **Works on switches** | ❌ No | ✅ Yes |
| **Works on wireless** | ✅ Yes | ✅ Yes |
| **Detectability** | Very low | Medium-High |
| **Techniques** | NIC in promiscuous mode | ARP poisoning, MAC flooding, DHCP spoofing |
| **ARP cache affected** | ❌ No | ✅ Yes (in ARP poisoning) |
| **Switch CAM affected** | ❌ No | ✅ Yes (in MAC flooding) |
| **Skill required** | Low | Medium-High |
| **Example tools** | Wireshark (listen only) | Ettercap, arpspoof, Cain & Abel |

> [!IMPORTANT]
> The most commonly tested distinction:
> **Passive sniffing = no packets sent = works on hubs**
> **Active sniffing = packets sent = works on switches**
> This single distinction drives most MCQs on sniffing type.

---

## Section 2 — Protocols Susceptible to Sniffing

### 2.1 Why Some Protocols Are Vulnerable

**WHAT:**
Protocols that transmit data in **cleartext (plaintext)** — without
encryption — are fully susceptible to sniffing. Any attacker
capturing those packets can read the complete content — including
usernames, passwords, session tokens, emails, and file contents.

**WHY they still exist:**
Many of these protocols were designed in the 1970s–1980s when
internet security was not a design priority. Networks were small,
trusted, and academic. These protocols were never redesigned for
security — they are simply still in use due to legacy compatibility.

**Analogy:**
A cleartext protocol is like sending your bank account password
on a postcard. Anyone handling the postcard between sender and
recipient can read it with zero effort. An encrypted protocol
is like sending it in a locked safe — intercepting it yields
nothing useful.

---

### 2.2 Vulnerable Protocols — Full Reference

| Protocol | Port | Layer | What Is Exposed |
|---|---|---|---|
| **HTTP** | TCP 80 | Application | URLs, form data, cookies, session tokens, full page content |
| **FTP** | TCP 21 (control), 20 (data) | Application | Username, password, file contents in cleartext |
| **Telnet** | TCP 23 | Application | Full session — every keystroke including passwords |
| **SMTP** | TCP 25 | Application | Email content, sender/recipient, attachments (without TLS) |
| **POP3** | TCP 110 | Application | Email username, password, email content |
| **IMAP** | TCP 143 | Application | Email username, password, email content, folder structure |
| **DNS** | UDP/TCP 53 | Application | DNS queries and responses — reveals browsing patterns |
| **SNMP v1/v2c** | UDP 161/162 | Application | Community strings (effectively passwords), device config |
| **NFS** | TCP/UDP 2049 | Application | File content, directory structure |
| **RIP** | UDP 520 | Network | Routing table updates — no authentication |
| **TFTP** | UDP 69 | Application | File transfers in cleartext — no authentication |
| **rlogin / rsh / rexec** | TCP 513/514/512 | Application | Full session, credentials — BSD r-commands |
| **IRC** | TCP 6667 | Application | Chat content, channel membership |
| **LDAP** | TCP 389 | Application | Directory queries, credentials (without TLS) |

> [!WARNING]
> **Telnet** is the most extreme case — every single keystroke
> typed by the user (including passwords character by character)
> is transmitted as a separate TCP packet in cleartext. A sniffer
> can reconstruct the entire session keystroke by keystroke.
> Telnet should NEVER be used for remote administration.

> [!IMPORTANT]
> **SNMP v1 and v2c** use community strings as authentication —
> these are effectively passwords transmitted in cleartext in every
> SNMP packet. An attacker sniffing SNMP traffic captures the
> community string and gains full read (and potentially write)
> access to all SNMP-managed network devices.
> **SNMP v3** introduced proper authentication and encryption.

---

### 2.3 Secure Alternatives

| Vulnerable Protocol | Secure Alternative | Port | Protection Added |
|---|---|---|---|
| HTTP | **HTTPS** | TCP 443 | TLS encryption — all content encrypted |
| FTP | **SFTP / FTPS / SCP** | TCP 22 / 990 / 22 | Encrypted transport |
| Telnet | **SSH** | TCP 22 | Full session encryption + host authentication |
| SMTP | **SMTP + STARTTLS / SMTPS** | TCP 587 / 465 | TLS encryption of email in transit |
| POP3 | **POP3S** | TCP 995 | TLS encryption |
| IMAP | **IMAPS** | TCP 993 | TLS encryption |
| SNMP v1/v2c | **SNMPv3** | UDP 161 | Authentication + encryption |
| LDAP | **LDAPS / LDAP + STARTTLS** | TCP 636 / 389 | TLS encryption of directory queries |
| DNS | **DNS over HTTPS (DoH) / DNS over TLS (DoT)** | TCP 443 / 853 | Encrypted DNS queries |

---

## Section 3 — ARP Poisoning

### 3.1 ARP Fundamentals

**WHAT:**
ARP (Address Resolution Protocol) is a Layer 2 protocol that
maps **IP addresses to MAC addresses** within a local network
segment. When a host needs to send a packet to an IP address
on the same subnet, it must first resolve that IP to a MAC
address to construct the Ethernet frame.

**Normal ARP operation:**

```text
Host A wants to send to IP 192.168.1.5:
        ↓
Host A checks ARP cache → IP 192.168.1.5 not found
        ↓
Host A broadcasts ARP Request:
  "Who has 192.168.1.5? Tell 192.168.1.10 (MAC: AA:BB:CC:11:22:33)"
  ARP Request sent to FF:FF:FF:FF:FF:FF (broadcast)
        ↓
All devices on segment receive the broadcast
        ↓
Host B (IP 192.168.1.5, MAC: DD:EE:FF:44:55:66) responds:
  "192.168.1.5 is at DD:EE:FF:44:55:66" (unicast reply to Host A)
        ↓
Host A updates ARP cache: 192.168.1.5 → DD:EE:FF:44:55:66
        ↓
Host A constructs Ethernet frame with dest MAC DD:EE:FF:44:55:66
```

**ARP Cache:**
Every host maintains a local ARP cache — a temporary table of
IP→MAC mappings. Cache entries expire after a timeout (typically
2 minutes on Windows, 20 minutes on Linux by default).

**View ARP cache:**
```bash
# Windows
arp -a

# Linux
arp -n
ip neigh show
```

**Critical ARP weakness:** ARP is stateless and unauthenticated — a host accepts and caches any ARP reply it receives, even if it never sent an ARP request. There is no verification that the replying host actually owns the IP address it is claiming. This is the root vulnerability that makes ARP poisoning possible.

---

### 3.2 How ARP Poisoning Works

**WHAT:** ARP poisoning (also called ARP spoofing or ARP cache poisoning) is an attack where the attacker sends forged (spoofed) ARP reply packets to associate their own MAC address with the IP address of another legitimate host — causing victims to send traffic intended for that host to the attacker instead.

**WHY it works:** Because ARP is stateless — hosts accept unsolicited ARP replies and update their ARP cache immediately without any verification.

**Attacker's goal — MITM position:**

```text
Normal traffic flow:
Host A (192.168.1.10) ←————————————→ Gateway (192.168.1.1)

After ARP poisoning:
Host A → [thinks gateway MAC = Attacker MAC] → sends to Attacker
Attacker → [forwards to real Gateway] → Gateway
Gateway → [thinks Host A MAC = Attacker MAC] → sends to Attacker
Attacker → [forwards to Host A] → Host A
The attacker sits invisibly in the middle — reading, modifying, or dropping all traffic between the two victims.
```

---

### 3.3 ARP Poisoning Attack Flow

Step-by-step:

```text
SETUP:
  Attacker IP:  192.168.1.100  MAC: AT:TA:CK:ER:MA:CC
  Victim A:     192.168.1.10   MAC: VI:CT:IM:AA:AA:AA
  Gateway:      192.168.1.1    MAC: GA:TE:WA:YY:YY:YY

STEP 1 — Poison Victim A's ARP cache:
  Attacker sends to Victim A (unicast or broadcast):
  ARP Reply: "192.168.1.1 is at AT:TA:CK:ER:MA:CC"
  (Lying — claiming to be the Gateway)
        ↓
  Victim A's ARP cache updated:
  192.168.1.1 → AT:TA:CK:ER:MA:CC  ← POISONED

STEP 2 — Poison Gateway's ARP cache:
  Attacker sends to Gateway (unicast or broadcast):
  ARP Reply: "192.168.1.10 is at AT:TA:CK:ER:MA:CC"
  (Lying — claiming to be Victim A)
        ↓
  Gateway's ARP cache updated:
  192.168.1.10 → AT:TA:CK:ER:MA:CC  ← POISONED

STEP 3 — Enable IP forwarding on attacker machine:
  echo 1 > /proc/sys/net/ipv4/ip_forward
  (Forward intercepted packets to real destination — 
   maintains connectivity so victims don't notice)

STEP 4 — Traffic flows through attacker:
  Victim A → [uses poisoned ARP cache] → sends to Attacker
  Attacker → reads/modifies → forwards to Gateway
  Gateway → [uses poisoned ARP cache] → sends to Attacker
  Attacker → reads/modifies → forwards to Victim A

STEP 5 — Maintain poisoning:
  Attacker continuously re-sends poisoned ARP replies
  (ARP cache entries expire — must be refreshed constantly)
```

> [!IMPORTANT]
> IP forwarding is critical. If the attacker does not enable IP forwarding, they become a black hole — all packets sent to them are dropped. This causes network outage for the victim, which immediately reveals the attack. Enabling IP forwarding makes the attack transparent — victims experience normal connectivity while all traffic is intercepted.

---

### 3.4 What an Attacker Can Do After ARP Poisoning

| Attack | What Happens |
|---|---|
| Passive sniffing (MITM) | Read all cleartext traffic — credentials, emails, HTTP content |
| Session hijacking | Steal session cookies from HTTP traffic — impersonate user |
| SSL stripping | Downgrade HTTPS to HTTP — read "encrypted" traffic |
| DNS spoofing | Intercept DNS queries — return fake responses |
| Credential harvesting | Extract usernames/passwords from FTP, Telnet, HTTP POST |
| Traffic modification | Alter packet contents in transit (inject code into HTTP responses) |
| Denial of Service | Drop all packets — disconnect victim from network |
| VoIP interception | Capture and reconstruct VoIP (SIP/RTP) calls |

---

### 3.5 ARP Poisoning Tools

| Tool | Platform | Notes |
|---|---|---|
| arpspoof (dsniff suite) | Linux | Classic — sends forged ARP replies continuously |
| Ettercap | Linux/Windows | Full MITM framework — ARP poisoning + sniffing + filters |
| Cain & Abel | Windows | GUI tool — ARP poisoning + credential sniffing + cracking |
| Bettercap | Linux/Windows | Modern — successor to Ettercap — active development |
| scapy | Python (cross-platform) | Craft and send arbitrary ARP packets — flexible |
| MITMf | Linux | Man-in-the-Middle Framework — multiple attack modules |

**arpspoof example (dsniff):**

```bash
# Enable IP forwarding first
echo 1 > /proc/sys/net/ipv4/ip_forward

# Poison victim's ARP cache — tell victim that gateway is at attacker
arpspoof -i eth0 -t 192.168.1.10 192.168.1.1

# Poison gateway's ARP cache — tell gateway that victim is at attacker
arpspoof -i eth0 -t 192.168.1.1 192.168.1.10
```

---

### 3.6 ARP Poisoning Countermeasures

| Countermeasure | How It Works | Where Applied |
|---|---|---|
| Dynamic ARP Inspection (DAI) | Switch validates ARP packets against DHCP snooping binding table — drops spoofed replies | Layer 2 switch feature |
| Static ARP entries | Manually configure IP→MAC mappings — cannot be overwritten by spoofed replies | Host / router |
| DHCP Snooping | Switch tracks IP→MAC→port mappings from DHCP — feeds DAI | Layer 2 switch |
| ARP Spoofing Detection tools | Monitor ARP traffic — alert on same IP appearing with different MACs | Host-based / network |
| Port Security | Limit number of MACs per switch port — limits MAC flooding too | Switch port config |
| Encrypted protocols | HTTPS, SSH, TLS — even if traffic is intercepted, content is encrypted | All hosts |
| VPNs | All traffic encrypted at VPN layer — sniffed packets unreadable | Host / network |
| XArp | Windows/Linux ARP monitoring tool — alerts on ARP cache changes | Host |
| Arpwatch | Linux daemon — monitors ARP traffic — alerts on MAC/IP pairing changes | Network monitoring |

> [!TIP]
> Dynamic ARP Inspection (DAI) is the most effective network-level countermeasure. It requires DHCP Snooping to be enabled first — DAI uses the DHCP snooping binding table as its ground truth for valid IP→MAC mappings. Any ARP reply not matching this table is dropped at the switch level.

---

## Section 4 — MAC Flooding

### 4.1 How Switches Work — Foundation

**WHAT:** A network switch forwards Ethernet frames based on a CAM table (Content Addressable Memory) — also called a MAC address table or forwarding table. This table maps MAC addresses to the physical switch port where that MAC was last seen.

**Normal switch operation:**

```text
Frame arrives on Port 1 from MAC AA:BB:CC:11:22:33
        ↓
Switch records: AA:BB:CC:11:22:33 → Port 1 (in CAM table)
        ↓
Switch checks destination MAC in frame
        ↓
Case 1 — Destination MAC FOUND in CAM table:
  Forward frame to that specific port only
  → Only destination device receives it

Case 2 — Destination MAC NOT FOUND in CAM table:
  FLOOD frame to ALL ports (except incoming port)
  → All devices receive it — including attacker
  → This is called an "unknown unicast flood"
```

**CAM table limitations:** The CAM table has a fixed memory size — typically storing 4,000–16,000 MAC entries depending on switch model. When the table is full, the switch has no room to add new entries. This is the vulnerability that MAC flooding exploits.

---

### 4.2 MAC Flooding Attack

**WHAT:** MAC flooding is an attack where the attacker sends thousands of Ethernet frames with random, forged source MAC addresses at high speed — filling the switch's CAM table completely.

**WHY:** When the CAM table is full, the switch can no longer learn new MAC addresses. Any frames with destination MACs not already in the (overflowed) CAM table are flooded to all ports — the switch effectively degrades from intelligent switching to hub-like behaviour. The attacker's machine — in promiscuous mode — receives all flooded frames.

**HOW:**

```text
Normal CAM table (has space):
  MAC_A → Port 1
  MAC_B → Port 2
  MAC_C → Port 3
  [entries in use: 3 / capacity: 8000]

Attacker floods random MACs:
  11:11:11:11:11:01 → Port 4 (attacker's port)
  11:11:11:11:11:02 → Port 4
  11:11:11:11:11:03 → Port 4
  ... [thousands of entries per second]
  [entries in use: 8000 / capacity: 8000 — FULL]

New legitimate frame arrives (destination: MAC_D):
  Switch checks CAM table: MAC_D not found
  Switch FLOODS to ALL ports
  Attacker on Port 4 receives this frame
  Attacker captures it → reads content
```

> [!NOTE]
> The CAM table overflow does NOT erase existing legitimate entries immediately — entries have TTL and age out. In practice, the attacker floods fast enough to keep filling new slots as old ones expire, maintaining the overflow state continuously.

---

### 4.3 MAC Flooding Attack Flow

```text
STEP 1 — Attacker places NIC in promiscuous mode
  (to capture frames not addressed to attacker's own MAC)

STEP 2 — Attacker runs flooding tool (e.g., macof)
  macof floods random MAC addresses at line rate
  Typical rate: 155,000+ frames per minute
  Each frame has: random source MAC, random destination MAC
  → Switch CAM table fills within seconds

STEP 3 — CAM table overflows
  Switch cannot store new legitimate MAC entries
  Unknown unicast flooding begins
  ALL frames for unknown destinations → ALL ports

STEP 4 — Attacker captures traffic
  Attacker's promiscuous NIC captures ALL flooded frames
  Includes inter-host traffic not meant for attacker

STEP 5 — Attacker analyzes captured data
  Extracts credentials, session tokens, content
  Using Wireshark or similar tool
```

---

### 4.4 MAC Flooding Tools

| Tool | Notes |
|---|---|
| macof (part of dsniff suite) | Classic MAC flooding tool — generates random MACs at high rate |
| Yersinia | Multi-protocol attack tool — supports MAC flooding, DHCP attacks, STP attacks |
| Ettercap | Can perform MAC flooding alongside ARP poisoning |
| scapy | Python library — craft custom MAC flood frames |

**macof command:**

```bash
# Flood all interfaces with random MACs
macof

# Flood specific interface
macof -i eth0

# Flood with specific destination
macof -i eth0 -d 192.168.1.1
```

---

### 4.5 MAC Flooding Countermeasures

| Countermeasure | How It Works |
|---|---|
| Port Security | Configure switch to allow maximum N MAC addresses per port. Excess MACs → port shutdown / restrict / protect mode. Most effective countermeasure. |
| Port Security — Sticky MAC | Switch dynamically learns first N MACs per port and locks them — no new MACs allowed. |
| 802.1X Port Authentication | Authenticate devices before allowing network access — unauthorized device never gets to flood. |
| VLAN Segmentation | Limit blast radius — MAC flooding only affects the VLAN of the flooding device. |
| Private VLANs | Isolate switch ports — devices cannot communicate directly — reduces flooding impact. |
| Switch monitoring | Detect sudden spike in CAM table entries or unknown unicast flooding rate. |
| Rate limiting | Limit frames per second per port — flooding tool limited in effectiveness. |

**Port Security configuration (Cisco IOS example):**

```text
Switch(config)# interface FastEthernet0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport port-security
Switch(config-if)# switchport port-security maximum 2
Switch(config-if)# switchport port-security violation shutdown
Switch(config-if)# switchport port-security mac-address sticky
```

> [!IMPORTANT]
> Port Security is the primary and most direct countermeasure for MAC flooding. Setting maximum 1 or maximum 2 per port means a flooding tool generating thousands of random MACs will trigger port shutdown immediately — neutralizing the attack within milliseconds.

---

## Section 5 — DNS Spoofing and DNS Hacking

### 5.1 DNS Fundamentals

**WHAT:** DNS (Domain Name System) is the internet's distributed hierarchical naming system — it translates human-readable hostnames (www.google.com) into machine-routable IP addresses (142.250.80.46).

**DNS Resolution Chain:**

```text
User types: www.example.com in browser
        ↓
OS checks local hosts file (/etc/hosts or C:\Windows\System32\drivers\etc\hosts)
  → If found: use that IP (no DNS query)
        ↓
OS checks local DNS cache
  → If found and not expired: use cached IP
        ↓
OS sends query to configured DNS Resolver (Recursive Resolver)
  → Usually ISP's DNS or 8.8.8.8 (Google), 1.1.1.1 (Cloudflare)
        ↓
Resolver checks its own cache
  → If found: return cached answer to client
        ↓
Resolver queries Root Nameserver (.)
  → Root returns address of .com TLD nameserver
        ↓
Resolver queries .com TLD Nameserver
  → TLD returns address of example.com Authoritative Nameserver
        ↓
Resolver queries example.com Authoritative Nameserver
  → Returns IP for www.example.com
        ↓
Resolver caches answer for TTL duration
Resolver returns IP to client
        ↓
Client connects to that IP
```

**DNS Record Types:**

| Record | Purpose |
|---|---|
| A | Maps hostname → IPv4 address |
| AAAA | Maps hostname → IPv6 address |
| MX | Mail server for a domain |
| CNAME | Canonical name — alias to another hostname |
| NS | Nameserver for a domain |
| PTR | Reverse DNS — IP → hostname |
| TXT | Text records — SPF, DKIM, domain verification |
| SOA | Start of Authority — zone info |

DNS uses UDP port 53 for normal queries (responses ≤ 512 bytes). DNS uses TCP port 53 for large responses and zone transfers.

---

### 5.2 DNS Spoofing

**WHAT:** DNS spoofing is the technique of providing false DNS responses to a victim — causing them to resolve a legitimate hostname to an attacker-controlled IP address instead of the real one.

**WHY:** DNS is the foundation of internet navigation. If an attacker controls what IP a hostname resolves to, they control where the victim connects — even if the victim types the correct URL.

**Analogy:** DNS spoofing is like replacing every copy of a city phone directory with a fake one where your competitor's phone number is listed under your business name. Everyone who looks up your business gets redirected to the competitor — without knowing they were tricked.

**How it works in an ARP-poisoned MITM scenario:**

```text
Attacker is already in MITM position (via ARP poisoning)
        ↓
Victim types: www.bank.com
        ↓
DNS query goes to attacker (traffic routed through attacker)
        ↓
Attacker intercepts DNS query (UDP/53)
        ↓
Attacker responds with fake DNS reply:
  "www.bank.com → 10.0.0.99" (attacker's phishing server)
        ↓
Victim browser connects to 10.0.0.99
  → Attacker's phishing page serves fake bank login
        ↓
Victim enters credentials → captured by attacker
```

**DNS Spoofing requires MITM position:** To intercept and forge DNS replies in real time, the attacker must be positioned between the victim and the DNS server — achieved via ARP poisoning on local networks.

---

### 5.3 DNS Cache Poisoning

**WHAT:** DNS cache poisoning is a more powerful variant where the attacker injects malicious DNS records into a DNS resolver's cache — rather than just spoofing responses to a single victim.

**WHY it's more damaging:** If a DNS resolver's cache is poisoned, every user who queries that resolver for the poisoned hostname receives the fake IP — potentially thousands or millions of users per poisoned resolver.

**How it works:**

```text
Target: Recursive DNS Resolver (e.g., ISP's DNS server)
        ↓
Attacker sends rapid stream of forged DNS response packets to resolver
Each response claims: "www.bank.com → 10.0.0.99"
Each has a different transaction ID guessing the valid one
        ↓
Resolver is currently processing a legitimate query for www.bank.com
  from a user
        ↓
If attacker's forged response arrives with:
  - Correct transaction ID (guessed)
  - Before the real authoritative response
        ↓
Resolver accepts forged response → caches it:
  www.bank.com → 10.0.0.99 (cached for TTL duration)
        ↓
ALL users querying this resolver for www.bank.com
  → receive 10.0.0.99 (attacker's server)
  → until TTL expires
```

**Transaction ID vulnerability:** Original DNS used a 16-bit transaction ID (0–65535). Attacker could guess the ID by sending 65,536 rapid responses. The Kaminsky Attack (2008) dramatically improved this — see Extra Notes E7.

---

### 5.4 DNS Hacking Techniques

**WHAT:** DNS hacking is a broader category of attacks targeting the DNS infrastructure itself — beyond just spoofing responses.

| Technique | Description | Impact |
|---|---|---|
| DNS Cache Poisoning | Inject false records into resolver cache | Redirects all users of that resolver |
| DNS Hijacking | Compromise DNS server or registrar account → change authoritative records | Redirects all traffic for entire domain |
| DNS Zone Transfer Abuse (AXFR) | Unauthorized AXFR request reveals entire DNS zone — all subdomains and IPs | Full network topology disclosure — reconnaissance |
| DNS Amplification DDoS | Use open DNS resolvers as amplifiers — small query → large response → DDoS victim | Volumetric DDoS — amplification factor up to 70× |
| DNS Tunneling | Encode C2 data / exfiltrate data inside DNS queries and responses | Exfiltration / C2 bypassing firewalls |
| NXDOMAIN Attack | Flood DNS with queries for non-existent domains → resolver resources exhausted | DNS DoS |
| BGP Hijacking (DNS impact) | Hijack BGP routes to intercept traffic to DNS servers | Large-scale traffic interception |
| Domain Hijacking | Social engineering / credential theft against domain registrar account | Attacker takes over domain — changes NS records |
| Hosts File Modification | Trojan modifies local hosts file to redirect specific domains | Local DNS override — affects single machine |

**DNS Zone Transfer (AXFR) — Reconnaissance Detail:**

```bash
# Query DNS zone transfer (attacker recon tool)
host -t AXFR example.com ns1.example.com
dig axfr @ns1.example.com example.com

# If zone transfer is improperly permitted — attacker receives:
# ALL A records, MX records, CNAME records, subdomains
# Full internal network map revealed
```

> [!WARNING]
> Zone transfers should ONLY be permitted between authoritative DNS servers (primary → secondary) and only from specific trusted IP addresses. Open zone transfers are a critical misconfiguration — revealing complete DNS topology to anyone.

**DNS Tunneling:**

```text
Normal DNS query: "What is the IP of api.example.com?"
DNS Tunnel query: "What is the IP of c2data_encoded_base64.evil.com?"
                                     ^^^^^^^^^^^^^^^^^^^
                                     Encoded C2 command in subdomain

DNS response: TXT record containing encoded response from C2 server
DNS tunneling tools: Iodine, dnscat2, dns2tcp
```

---

### 5.5 DNS Attack Tools

| Tool | Purpose | Notes |
|---|---|---|
| dnsspoof (dsniff suite) | DNS spoofing — forge DNS replies in MITM position | Classic tool |
| Ettercap + dns_spoof plugin | DNS spoofing via MITM | Integrated with ARP poisoning |
| Bettercap | DNS spoofing + ARP poisoning + MITM | Modern active development |
| dnschef | DNS proxy for spoofing — intercept and modify DNS | Used in penetration testing |
| Metasploit — auxiliary/spoof/dns | DNS spoofing auxiliary module | Part of Metasploit framework |
| dnscat2 | DNS tunneling C2 | Encrypted C2 over DNS |
| Iodine | DNS tunneling — IP over DNS | Bypass firewall with DNS egress |
| dig | DNS query tool — AXFR zone transfer testing | Built-in Linux |
| nslookup | DNS query tool — Windows/Linux | Built-in |
| host | DNS query tool — zone transfer testing | Linux |

---

### 5.6 DNS Attack Countermeasures

| Countermeasure | What It Prevents | How |
|---|---|---|
| DNSSEC | Cache poisoning, spoofing | Cryptographic signing of DNS records — tampering detectable |
| DNS over HTTPS (DoH) | Query interception, spoofing | Encrypts DNS queries in HTTPS — invisible to on-path attacker |
| DNS over TLS (DoT) | Query interception, spoofing | Encrypts DNS queries in TLS — port 853 |
| Disable open recursion | DNS amplification DDoS | Resolver only answers queries from authorised clients |
| Zone transfer restriction | AXFR reconnaissance | Allow AXFR only from specific secondary NS IPs |
| TTL management | Extends poisoning window | Short TTL = faster expiry of poisoned records |
| Randomise source port | Cache poisoning (harder to guess) | Port randomisation + random transaction IDs |
| Patching (Kaminsky) | 2008 Kaminsky-style attacks | Patch to source port randomisation |
| Hosts file monitoring | Hosts file modification by malware | FIM monitoring of /etc/hosts and Windows hosts file |
| Reputation-based DNS filtering | Malware C2 via DNS | Blocks known malicious domains at resolver level |

---

## Section 6 — Wireshark / Ethereal Capture and Display Filters

### 6.1 Wireshark Overview

**WHAT:** Wireshark is the world's most widely used open-source network protocol analyzer (packet sniffer). It captures packets from network interfaces and provides deep protocol dissection, filtering, and analysis capabilities.

**History:**
- Originally called Ethereal — created by Gerald Combs in 1998
- Renamed to Wireshark in 2006 due to trademark issues
- For exams: Ethereal = Wireshark — same tool, old name

**What Wireshark can capture:**
- All packets on any accessible network interface
- Wired Ethernet, Wi-Fi (with monitor mode), Bluetooth, USB
- Live capture or read from saved .pcap / .pcapng files

**Key features:**
- Deep packet inspection — dissects 2000+ protocols
- Real-time capture with live filtering
- Follow TCP/UDP stream — reconstruct full application sessions
- Export objects (HTTP files, images, credentials)
- Colour coding of protocol types
- Statistics and graphing

**Capture file format:** .pcap (classic), .pcapng (modern)

**Launch Wireshark with elevated privileges:**

```bash
# Linux — requires root or wireshark group membership
sudo wireshark
# OR add user to wireshark group
sudo usermod -aG wireshark $USER
```

---

### 6.2 Capture Filters

**WHAT:** Capture filters are applied at capture time — they determine which packets are recorded by Wireshark. Packets that do not match the capture filter are never written to memory or disk.

**Syntax:** BPF (Berkeley Packet Filter) syntax

**Purpose:** Reduce capture volume — focus on relevant traffic, avoid capturing everything on a busy network.

**Important capture filter syntax:**

```text
# Capture only traffic to/from specific IP
host 192.168.1.10

# Capture only traffic to specific IP (destination)
dst host 192.168.1.10

# Capture only traffic from specific IP (source)
src host 192.168.1.10

# Capture only specific port
port 80

# Capture only specific protocol
tcp
udp
icmp
arp
dns

# Capture specific port AND protocol
tcp port 443

# Capture traffic between two hosts
host 192.168.1.10 and host 192.168.1.1

# Capture traffic NOT from specific IP
not host 192.168.1.5

# Capture specific port range
portrange 1-1024

# Capture specific network subnet
net 192.168.1.0/24

# Capture only HTTP and HTTPS
port 80 or port 443

# Capture only DNS traffic
port 53

# Capture ARP packets
arp

# Combination — TCP to specific host on port 80
tcp and dst host 192.168.1.10 and port 80
```

> [!IMPORTANT]
> Capture filters use BPF syntax — the same syntax as tcpdump. Capture filters are set in Wireshark's capture interface dialog BEFORE starting capture. They CANNOT be changed while capturing.

---

### 6.3 Display Filters

**WHAT:** Display filters are applied to already captured packets — they show or hide packets from the captured set without deleting them. Display-filtered packets are still in the capture file — the filter just controls what you see.

**Syntax:** Wireshark's own display filter language — different from capture filter BPF syntax.

**Important display filter syntax:**

```text
# Filter by IP address (source OR destination)
ip.addr == 192.168.1.10

# Filter by source IP
ip.src == 192.168.1.10

# Filter by destination IP
ip.dst == 192.168.1.1

# Filter by protocol
http
dns
tcp
udp
arp
icmp
ftp
telnet
smtp
ssl
tls

# Filter by TCP/UDP port
tcp.port == 80
udp.port == 53
tcp.dstport == 443
tcp.srcport == 21

# Filter HTTP methods
http.request.method == "GET"
http.request.method == "POST"

# Filter HTTP response codes
http.response.code == 200
http.response.code == 404

# Filter DNS queries
dns.qry.name == "www.google.com"
dns.flags.response == 0     (DNS questions only)
dns.flags.response == 1     (DNS responses only)

# Filter ARP
arp.opcode == 1    (ARP Request)
arp.opcode == 2    (ARP Reply)

# Filter TCP flags
tcp.flags.syn == 1
tcp.flags.rst == 1
tcp.flags.fin == 1

# Filter by MAC address
eth.addr == aa:bb:cc:dd:ee:ff
eth.src == aa:bb:cc:dd:ee:ff
eth.dst == ff:ff:ff:ff:ff:ff

# Exclude specific host
!(ip.addr == 192.168.1.1)

# Combine filters with AND / OR
ip.src == 192.168.1.10 && tcp.port == 80
http || dns

# Filter by content (contains string)
http contains "password"
tcp contains "login"

# Filter by frame length
frame.len > 1000

# ICMP type
icmp.type == 8    (Echo Request — ping)
icmp.type == 0    (Echo Reply)
```

> [!TIP]
> Follow TCP Stream (Right-click packet → Follow → TCP Stream) reconstructs the entire application-layer conversation between two hosts — showing the full HTTP session, FTP commands, Telnet keystrokes, or SMTP email exchange as human-readable text. This is the fastest way to extract credentials from captured traffic.

---

### 6.4 Practical Sniffing Workflow

**Typical attacker workflow using Wireshark in MITM scenario:**

```text
STEP 1 — Establish MITM position
  arpspoof to poison victim and gateway ARP caches
  Enable IP forwarding to maintain connectivity

STEP 2 — Start Wireshark capture
  Select interface (eth0)
  Apply capture filter (optional): host 192.168.1.10
  Start capture

STEP 3 — Wait for interesting traffic
  Victim browses web, logs into services, sends email

STEP 4 — Apply display filters to find credentials
  Filter: http contains "password"
  Filter: ftp
  Filter: telnet
  Filter: smtp

STEP 5 — Extract credentials
  Follow TCP stream → see login form POST data
  Username: admin
  Password: secretpass123

STEP 6 — Save capture file
  File → Save as → victim_session.pcap
  Share with team / analyze offline
```

**tcpdump — Command Line Alternative:**

```bash
# Capture all traffic on eth0 to file
tcpdump -i eth0 -w capture.pcap

# Capture only HTTP traffic
tcpdump -i eth0 port 80 -w http_capture.pcap

# Capture and display in terminal
tcpdump -i eth0 -A port 80

# Read saved capture file
tcpdump -r capture.pcap

# Verbose output with full packet content
tcpdump -i eth0 -vvv -X port 21
```

---

## Section 7 — Sniffing Countermeasures

### 7.1 Encryption-Based Countermeasures

**WHAT:** The most fundamental and effective countermeasure against sniffing is encrypting all network communications — so that intercepted packets contain only unintelligible ciphertext.

| Measure | Replaces | Protects |
|---|---|---|
| HTTPS (TLS) | HTTP | Web browsing, web app credentials, cookies |
| SSH | Telnet, rlogin, rsh | Remote administration, file transfer (SCP/SFTP) |
| TLS/SSL | Cleartext protocols | Email (IMAPS, POP3S, SMTPS), LDAPS |
| VPN (IPSec / OpenVPN / WireGuard) | Unencrypted network traffic | All traffic — tunnels through encrypted channel |
| SNMPv3 | SNMPv1/v2c | Network management traffic |
| WPA3 | WEP, WPA, WPA2 (older) | Wireless traffic encryption |
| DoH / DoT | DNS (cleartext) | DNS query privacy |
| S/MIME / PGP | Plaintext email | End-to-end email encryption |

> [!IMPORTANT]
> Encryption makes sniffing irrelevant for protected traffic — the attacker captures packets but cannot read their content. This is the preferred approach — address the root cause (cleartext transmission) rather than try to prevent interception.

---

### 7.2 Network-Level Countermeasures

| Countermeasure | What It Prevents | Notes |
|---|---|---|
| Dynamic ARP Inspection (DAI) | ARP poisoning | Requires DHCP snooping — validates ARP packets at switch |
| Port Security | MAC flooding | Limits MACs per port — shuts port on violation |
| DHCP Snooping | Rogue DHCP / supports DAI | Tracks legitimate IP→MAC→port mappings |
| 802.1X | Unauthorized device access | Authentication before network access granted |
| VLAN segmentation | Limits broadcast domain | Reduces scope of passive sniffing and ARP attacks |
| Private VLANs | Inter-host sniffing | Isolates ports — devices cannot directly communicate |
| Switches instead of hubs | Passive sniffing | Switches isolate traffic — passive sniffing fails |
| SSL/TLS inspection | Encrypted C2 | NGFW decrypts and inspects TLS — detects malware in HTTPS |

---

### 7.3 Detection of Sniffing

**Detecting Promiscuous Mode:**

A NIC in promiscuous mode processes ALL frames — this can be detected using several techniques:

| Detection Method | How It Works |
|---|---|
| Ping test | Send ICMP ping to non-existent MAC address (valid IP). Normal NIC discards at Layer 2. Promiscuous NIC forwards to OS — machine responds. Response = promiscuous mode suspected. |
| ARP test | Send ARP request with fake MAC but valid IP. Normal hosts ignore (MAC mismatch). Promiscuous host may respond. |
| DNS test | Send non-broadcast packet to decoy IP. Sniffing host may attempt DNS reverse lookup — DNS query reveals active sniffer. |
| Latency test | Flood network with garbage traffic — sniffing machine processing all frames has higher CPU load — increased response time. |
| Network IDS | Snort/Suricata signatures detect ARP poisoning patterns, ARP storm, duplicate IP/MAC pairs. |

**Detecting ARP Poisoning:**

```bash
# Check ARP cache for duplicate MACs (two IPs same MAC = poisoning)
arp -a | sort

# Arpwatch daemon — monitors ARP traffic and alerts on changes
arpwatch -i eth0

# XArp — GUI tool for ARP monitoring (Windows/Linux)
```

**Detecting MAC Flooding:**
- Monitor switch CAM table size via SNMP
- Alert on CAM table near-capacity
- Detect high rate of unknown unicast flooding on switch ports
- Port security violation counter alerts

---

### 7.4 Organisational Countermeasures

| Countermeasure | What It Addresses |
|---|---|
| Security awareness training | Educate users not to use cleartext protocols — recognise phishing redirects from DNS spoofing |
| Acceptable use policy | Prohibit use of unsecured protocols (Telnet, FTP) for sensitive work |
| Network segmentation | Separate sensitive networks — finance, HR — from general network |
| Regular audits | Scan for promiscuous mode NICs, rogue DHCP servers, ARP anomalies |
| Physical security | Prevent attackers from gaining physical network access to plant sniffing devices |
| Patch management | Patch DNS servers against cache poisoning vulnerabilities |

---

## 📌 Extra Notes

### E1 — How Ethernet Works at the Frame Level

> [!NOTE]
> Understanding Ethernet frame structure explains WHY sniffing works and why promiscuous mode is the mechanism.

**Ethernet Frame Structure:**

```text
| Preamble (7B) | SFD (1B) | Dest MAC (6B) | Src MAC (6B) |
| EtherType (2B) | Payload (46-1500B) | FCS (4B) |
```

**Normal NIC operation:**
- NIC receives every Ethernet frame on its segment
- NIC checks Destination MAC in frame header
- If Dest MAC == NIC's own MAC or FF:FF:FF:FF:FF:FF → pass to OS
- Otherwise → discard at hardware level — OS never sees it

**Promiscuous mode operation:**
- NIC receives every Ethernet frame on its segment
- Promiscuous flag set — NIC skips MAC address filtering
- ALL frames → passed to OS regardless of destination MAC
- Sniffing tool (Wireshark/tcpdump) reads from OS → captures all

This hardware-level filtering bypass is what makes sniffing possible.

---

### E2 — Hub vs Switch vs Router — Sniffing Implications

> [!NOTE]
> The network device type determines which sniffing approach works. This is always MCQ-relevant when questions describe a network topology.

| Device | How It Forwards | Sniffing Method |
|---|---|---|
| Hub | Repeats ALL frames to ALL ports — no intelligence | Passive sniffing — any connected host captures everything |
| Switch | Forwards only to destination port (unicast) — floods unknowns | Active sniffing needed (ARP poisoning, MAC flooding) |
| Router | Routes between networks — forwards by IP | Sniffing requires compromise of router or segment access |
| Wireless AP | Broadcasts radio frames — all clients in range receive all frames | Passive sniffing with wireless adapter in monitor mode |

**Wi-Fi Passive Sniffing:** Wireless frames are transmitted as radio signals — they are broadcast by nature. Any wireless adapter in monitor mode (different from promiscuous mode — captures raw 802.11 frames) can capture all Wi-Fi traffic in range.

```bash
# Enable monitor mode on wireless interface
airmon-ng start wlan0

# Capture wireless traffic with airodump-ng
airodump-ng wlan0mon

# Capture specific channel
airodump-ng -c 6 wlan0mon

# Capture with Wireshark in monitor mode
wireshark -i wlan0mon
```

**Key distinction:**
- **Promiscuous mode** — used on wired Ethernet — captures all Ethernet frames regardless of destination MAC
- **Monitor mode** — used on wireless — captures raw 802.11 frames including management and control frames — used for Wi-Fi sniffing

---

### E3 — MITM Attack — Full Picture

> [!NOTE]
> MITM is the umbrella attack class that ARP poisoning, DNS spoofing, and SSL stripping all enable. Understanding the full picture prevents confusion between the enabling technique and the outcome.

**MITM (Man-in-the-Middle) Attack:**

```text
Without MITM:
Client ←—————————————————→ Server

With MITM:
Client ←——→ Attacker ←——→ Server
```

The attacker intercepts, reads, and optionally modifies ALL communication between client and server — while both parties believe they are communicating directly with each other.

**How MITM is established — technique comparison:**

| Technique | Layer | Where It Works | What It Poisons |
|---|---|---|---|
| ARP Poisoning | Layer 2 | Local LAN segment | ARP cache on endpoints |
| MAC Flooding | Layer 2 | Local LAN segment | Switch CAM table |
| DHCP Spoofing | Layer 3 | Local LAN segment | Default gateway + DNS server config |
| ICMP Redirect | Layer 3 | Local LAN segment | Host routing table |
| DNS Spoofing | Layer 7 | Local or internet-wide | DNS cache (resolver or client) |
| BGP Hijacking | Routing | Internet-scale | BGP routing tables at ISP level |
| SSL Stripping | Layer 7 | Requires MITM first | Downgrades HTTPS to HTTP |

**SSL Stripping (sslstrip) — Important Extra:** Once in MITM position, the attacker can launch SSL stripping:

```text
Client → "I want HTTPS to bank.com" → Attacker
Attacker → [upgrades connection to HTTPS with bank.com]
Attacker → [serves HTTP to client] ← cleartext visible to attacker
Client → [enters password over "HTTP"] → Attacker reads it
Attacker → [forwards over HTTPS to bank.com]
```

The client sees http:// in the browser bar (if not checking) and the attacker reads all traffic in cleartext.

**Tool:** sslstrip (Moxie Marlinspike)
**Countermeasure:** HSTS (HTTP Strict Transport Security) — browser remembers that a site should only be accessed via HTTPS — rejects HTTP even if MITM tries to serve it.

**MITRE ATT&CK:** T1557 — Adversary-in-the-Middle

---

### E4 — ARP Protocol Deep Dive

> [!NOTE]
> ARP details frequently tested — operation codes, packet structure, broadcast vs unicast behaviour.

**ARP Packet Structure:**

| Field | Size | Content |
|---|---|---|
| Hardware Type | 2B | 1 = Ethernet |
| Protocol Type | 2B | 0x0800 = IPv4 |
| Hardware Address Length | 1B | 6 (MAC address = 6 bytes) |
| Protocol Address Length | 1B | 4 (IPv4 = 4 bytes) |
| Operation | 2B | 1 = ARP Request, 2 = ARP Reply |
| Sender MAC | 6B | Attacker's MAC (real or spoofed) |
| Sender IP | 4B | Attacker's IP (real or spoofed) |
| Target MAC | 6B | 00:00:00:00:00:00 in Request / Victim MAC in Reply |
| Target IP | 4B | IP being resolved |

> [!IMPORTANT]
> ARP Operation codes are MCQ-tested:
> - Opcode 1 = ARP Request (broadcast — who has this IP?)
> - Opcode 2 = ARP Reply (unicast or broadcast — I have this IP)
> - In Wireshark: `arp.opcode == 1` (requests) / `arp.opcode == 2` (replies)

**ARP Request vs ARP Reply delivery:**

| | ARP Request | ARP Reply |
|---|---|---|
| Destination MAC | FF:FF:FF:FF:FF:FF (broadcast) | Unicast to requester |
| Who receives it | All hosts on segment | Only the requesting host |
| Sender IP | Real sender IP | Attacker claims victim's IP |

---

### E5 — Gratuitous ARP

> [!NOTE]
> Gratuitous ARP is the mechanism that makes ARP poisoning so effective — attackers send UNSOLICITED ARP replies.

**What is Gratuitous ARP:** A gratuitous ARP is an ARP reply sent without being in response to any ARP request — the sender is announcing its own IP→MAC mapping to the network without being asked.

**Legitimate uses:**
- Network device announces its MAC after booting
- Virtual machine live migration updates ARP caches
- Network interface change (failover) announces new MAC
- Duplicate IP detection (send gratuitous ARP → if reply received → duplicate IP exists)

**How attackers abuse it:**

```text
Attacker sends (unsolicited):
ARP Reply: "192.168.1.1 (Gateway IP) is at AT:TA:CK:ER:MA:CC"
→ All hosts that receive this → update ARP cache immediately
→ All hosts now send gateway-destined traffic to attacker

No ARP request was made — the reply is simply accepted
This is the stateless vulnerability of ARP
```

**Gratuitous ARP in Wireshark:**
- Display filter: `arp.isgratuitous == 1`
- OR: `arp.src.proto_ipv4 == arp.dst.proto_ipv4` (sender IP equals target IP — hallmark of gratuitous ARP)

---

### E6 — DNS Protocol Deep Dive

> [!NOTE]
> DNS packet structure and transaction ID details explain why cache poisoning is possible and how Kaminsky improved it.

**DNS Packet Structure (relevant fields):**

| Field | Details |
|---|---|
| Transaction ID | 16-bit random identifier — must match between query and response |
| Flags | QR (query/response), Opcode, AA, TC, RD, RA, RCODE |
| Questions | The DNS query being asked |
| Answers | Resource records answering the query |
| Authority | NS records for the zone |
| Additional | Additional records (glue records) |

**Transaction ID vulnerability:**
- 16-bit = 65,536 possible values
- Early DNS resolvers used predictable (sequential) transaction IDs
- Attacker could guess the next transaction ID and forge a response
- Randomized transaction IDs improved security but 65,536 is still a small space — Kaminsky showed this was insufficient

**DNS Resolver Port:**
- Traditional DNS: resolver uses a fixed source port (53) for queries
- Fixed port = attacker needs to guess only 16-bit transaction ID (65,536 possibilities)
- Source port randomization: resolver uses random source port for each query
- Attacker now needs to guess BOTH transaction ID (16-bit) AND source port (16-bit)
- Combined space: 65,536 × 65,536 ≈ 4 billion possibilities — much harder

---

### E7 — Kaminsky DNS Cache Poisoning Attack

> [!NOTE]
> The Kaminsky attack (2008) is one of the most significant DNS vulnerabilities in history — always referenced in DNS security discussions and potentially MCQ-tested.

**Who:** Dan Kaminsky (security researcher)
**Year:** 2008 (discovered early 2008, disclosed July 2008 after coordinated patching across all major DNS vendors)

**The Core Insight:** Previous DNS cache poisoning required guessing the transaction ID for a SPECIFIC query. Kaminsky's insight: instead of waiting for the victim resolver to query a specific hostname, the attacker can force the resolver to make many queries by asking for random subdomains — and inject not just the answer record but the NS (nameserver) record for the entire zone in the additional section.

**Attack flow:**

```text
STEP 1 — Attacker asks resolver to resolve random subdomains:
  resolver.isp.com: "What is rand1.victim.com?"
  resolver.isp.com: "What is rand2.victim.com?"
  resolver.isp.com: "What is rand3.victim.com?"
  ... (triggers queries to authoritative server)

STEP 2 — For each query, attacker floods forged responses:
  Forged response claims:
  "rand1.victim.com → attacker's IP"
  AND in authority section:
  "victim.com NS ns1.attacker.com"  ← ZONE-LEVEL POISONING
  
  Attacker floods with all 65,536 transaction ID guesses
  Before real authoritative server responds

STEP 3 — If one forged response is accepted:
  Resolver caches: victim.com NS → ns1.attacker.com
  ALL future queries for ANY subdomain of victim.com
  → resolver asks attacker's nameserver
  → attacker controls ALL DNS for victim.com domain
  
  One successful poisoning = entire domain taken over
```

**Why it was severe:**
- Previous attacks: needed to poison specific hostname records
- Kaminsky: poisons the zone authority — entire domain compromised
- Effect persists for hours/days (NS record TTL)
- Millions of users affected by single poisoning of major resolver

**Fix:** Source port randomization — implemented in July 2008 across all major DNS implementations simultaneously. Combined with transaction ID randomization → 2³² ≈ 4 billion combinations instead of 65,536.

---

### E8 — Promiscuous Mode Detection

> [!NOTE]
> Several MCQs ask how to detect sniffers on a network. These specific techniques are exam-relevant.

**Technique 1 — Ping Method:**

```text
Send ICMP Echo to non-broadcast MAC but valid IP:
  Destination MAC: AA:BB:CC:DD:EE:FF (wrong — doesn't belong to target IP)
  Destination IP:  192.168.1.10 (victim)

Normal NIC: discards at Layer 2 (MAC mismatch) — no ICMP reply
Promiscuous NIC: accepts frame anyway → passes to IP stack
  → OS processes ICMP Echo → sends ICMP Reply
  → ICMP reply = evidence of promiscuous mode
```

**Technique 2 — ARP Method:**

```text
Send ARP with non-broadcast MAC but valid IP:
  ARP packet dest: 00:00:00:00:00:01 (non-broadcast, not victim's MAC)
  ARP target IP: 192.168.1.10 (victim)

Normal host: ARP packet ignored (not addressed to it)
Promiscuous host: may respond to ARP → reveals promiscuous mode
```

**Technique 3 — DNS Method:**

```text
Send packets to a decoy/honeypot IP on the network
Monitor DNS server:
  If any host attempts DNS reverse lookup for the decoy IP
  → That host is sniffing (it saw the packet — normal host wouldn't)
  → DNS query reveals the sniffer's IP
```

**Technique 4 — ifconfig/ip Detection (local):**

```bash
# Check local interface flags — PROMISC flag indicates promiscuous mode
ifconfig eth0 | grep PROMISC
ip link show eth0 | grep PROMISC

# Check all interfaces
ip link show | grep PROMISC
```

**Tool:** Antisniff — dedicated promiscuous mode detection tool developed by L0pht Research (Lopht Heavy Industries) — sends various probe packets and analyzes responses to detect sniffers.

---

### E9 — Predecessor / Successor Chains

> [!NOTE]
> Understanding evolution of sniffing and DNS attacks places current techniques in historical context.

**Sniffing Tool Evolution:**

```text
Packet sniffers (1980s — network monitoring tools — benign)
        ↓
dsniff suite (1999 — Dug Song) — first offensive sniffing toolkit
(arpspoof, macof, dnsspoof, urlsnarf, mailsnarf)
        ↓
Ethereal (1998) → renamed Wireshark (2006)
        ↓
Ettercap (2001) — integrated MITM + sniffing + filtering framework
        ↓
Cain & Abel (2001–2014) — Windows GUI — ARP poisoning + credential recovery
        ↓
Bettercap (2015–present) — modern replacement for Ettercap
        ↓
Network traffic analysis in cloud/SDN (2020+)
```

**ARP Attack Evolution:**

```text
ARP protocol designed (1982 — RFC 826)
        ↓
ARP spoofing attacks documented (1988 — Morris Worm exploited trust)
        ↓
dsniff arpspoof (1999) — first widely available ARP poisoning tool
        ↓
Ettercap ARP poisoning (2001)
        ↓
Dynamic ARP Inspection (DAI) — Cisco IOS countermeasure (2003)
        ↓
IPv6 NDP (Neighbor Discovery Protocol) — replaces ARP in IPv6
NDP has similar vulnerabilities — NDPMon, SeND as countermeasures
        ↓
ARP poisoning on wireless networks (2005+)
        ↓
ARP poisoning in cloud VMs / SDN (2015+) — different threat model
```

**DNS Security Evolution:**

```text
DNS designed (1983 — RFC 882/883) — no security
        ↓
DNS cache poisoning attacks documented (1990s)
        ↓
DNSSEC designed (1997 — RFC 2065) — cryptographic signing
        ↓
Kaminsky Attack (2008) — source port randomization fix
        ↓
DNSSEC deployment (gradual — still not universal as of 2026)
        ↓
DNS over TLS — DoT (2016 — RFC 7858)
        ↓
DNS over HTTPS — DoH (2018 — RFC 8484)
        ↓
DoH enabled by default in Firefox (2020), Chrome (2022)
        ↓
DNS over QUIC — DoQ (2022 — RFC 9250)
```

---

### E10 — Terminology Traps

| Term | Trap | Clarification |
|---|---|---|
| Passive vs Active Sniffing | "Passive sniffing works on all networks" | FALSE — passive only works on SHARED media (hubs, Wi-Fi). SWITCHED networks require ACTIVE sniffing. |
| ARP Poisoning vs MAC Flooding | "Both work the same way" | DIFFERENT mechanisms. ARP poisoning poisons ENDPOINT ARP CACHES. MAC flooding overflows SWITCH CAM TABLE. Both result in traffic reaching attacker, via different paths. |
| Gratuitous ARP | "Gratuitous ARP is always malicious" | FALSE — gratuitous ARP has many LEGITIMATE uses (network announcements, duplicate IP detection, failover). Attackers abuse it for poisoning. |
| Ethereal vs Wireshark | "These are different tools" | FALSE — Ethereal was RENAMED to Wireshark in 2006. Same tool. Both names appear in exams — treat identically. |
| Capture filter vs Display filter | "Display filters remove packets from capture" | FALSE — display filters only HIDE packets from view. They remain in the capture file. Capture filters PREVENT recording. |
| DNS Spoofing vs DNS Cache Poisoning | "Different attacks" | DNS spoofing is the GENERAL technique. Cache poisoning is a SPECIFIC form where records are stored in resolver cache — affecting ALL users of that resolver. |
| Promiscuous mode = promiscuous NIC = attacker | "Promiscuous mode = malicious" | FALSE — promiscuous mode is used legitimately by IDS sensors, network monitoring tools, and administrators. Context determines legitimacy. |
| ARP operates at Layer 3 | "ARP is a Layer 3 protocol" | PARTIALLY correct — ARP maps Layer 3 addresses (IP) to Layer 2 addresses (MAC). It is functionally Layer 2.5 — below IP, used by IP to construct Ethernet frames. |
| DNS only uses UDP 53 | "DNS = UDP port 53" | DNS uses UDP 53 for normal queries. DNS uses TCP 53 for large responses (>512 bytes) and zone transfers (AXFR). Both UDP AND TCP on port 53. |
| DNSSEC prevents all DNS attacks | "Implement DNSSEC — DNS is secure" | FALSE — DNSSEC prevents record tampering and forgery (signs records). It does NOT prevent DDoS against DNS servers, DNS tunneling, domain hijacking, or NXDOMAIN attacks. |

---

### E11 — Current Landscape 2026

> [!NOTE]
> Current developments in sniffing, ARP attacks, and DNS security.

**ARP Attacks in Modern Environments:**

- **Cloud VPC networks:** AWS, Azure, GCP implement ARP isolation at the hypervisor level — ARP poisoning between tenants is blocked. ARP poisoning risk is now primarily intra-VPC between attacker-controlled VMs or compromised instances.
- **SDN (Software Defined Networking):** Centralized controllers manage MAC→IP mappings — ARP is handled at controller level. Traditional ARP poisoning fails in full SDN environments.
- **Container networks:** Docker/Kubernetes default networking uses virtual bridges — ARP poisoning possible between containers on same bridge. Container network policies (Calico, Cilium) enforce identity-based security instead of ARP.

**DNS Security in 2026:**

- **DoH adoption:** Mozilla Firefox uses DoH by default (Cloudflare 1.1.1.1). Google Chrome DoH enabled since 2022. Most major browsers now support DoH — significantly reduces ISP-level DNS interception capability.
- **DNSSEC adoption:** As of 2025, approximately 25–35% of domains have DNSSEC configured. Major TLDs (.com, .net, .org) are signed. Many second-level domains remain unsigned.
- **DNS over QUIC (DoQ):** RFC 9250 (2022) — DNS over QUIC protocol (faster than DoT, more reliable than DoH) — gaining adoption in mobile environments.
- **NextDNS, 1.1.1.1, 8.8.8.8:** Public encrypted DNS resolvers now handle billions of queries — privacy-preserving by default.

**Recent CVEs — Sniffing/DNS Relevant:**

- **CVE-2024-1709** (ConnectWise ScreenConnect — 2024): Path traversal leading to credential theft — related to cleartext credential transmission. CVSS 10.0.
- **CVE-2023-50387** (KeyTrap — DNSSEC DoS — 2024): Specially crafted DNSSEC-signed response could cause resolver CPU exhaustion — one packet causes resolver to process for hours. Affected all major DNS resolver implementations. Patched February 2024.
- **CVE-2024-3400** (PAN-OS command injection — 2024): Palo Alto Networks firewall — exploited in the wild — could enable attacker to position for network-level attacks including traffic interception.

**Wi-Fi Sniffing in 2026:**

- **WPA3 Personal:** Uses SAE (Simultaneous Authentication of Equals) — each session uses unique encryption keys. Even if passphrase is known, previously captured traffic cannot be decrypted. Defeats offline Wi-Fi traffic decryption.
- **WPA3 Enterprise:** Uses 192-bit security suite — significantly stronger than WPA2 Enterprise.
- **Evil twin attacks:** Still highly effective — create fake AP with same SSID — clients connect — all traffic flows through attacker. Countermeasure: 802.1X mutual authentication.

---

### E12 — Indian Legal Context

> [!NOTE]
> Indian law applicable to sniffing, interception, and DNS attacks.

I should know this cold — unauthorized interception isn't a grey area under Indian law.

| Law | Section | Offence | Penalty |
|---|---|---|---|
| IT Act 2000 | S.43(a) | Unauthorized access to computer/network (sniffing unauthorized systems) | Civil compensation up to ₹1 crore |
| IT Act 2000 | S.66 | Unauthorized interception of data — criminal | Up to 3 years + ₹5 lakh fine |
| IT Act 2000 | S.66B | Receiving stolen/intercepted data (credentials, emails) | Up to 3 years + ₹1 lakh fine |
| IT Act 2000 | S.69B | Unauthorized monitoring of network traffic by individual/organization | Up to 3 years + ₹5 lakh fine |
| IT Act 2000 | S.43(b) | Downloading/extracting data via ARP poisoning / MITM sniffing | Civil compensation up to ₹1 crore |
| Indian Telegraph Act 1885 | S.26 | Intercepting telegraph/electronic communications (broadened to include network interception) | Imprisonment up to 3 years |
| IT Act 2000 | S.66F | Sniffing/intercepting communications of critical infrastructure (banking, defence, power) | Life imprisonment |
| DPDPA 2023 | — | Organization suffers breach due to unencrypted network → personal data exposed via sniffing | Penalty up to ₹250 crore |
| IPC | S.419/420 | Fraud via DNS spoofing / phishing (cheating by impersonation via redirected domain) | Up to 7 years + fine |

> [!IMPORTANT]
> Section 69B specifically covers unauthorized monitoring of network traffic — directly applicable to illegal sniffing. Government is authorized to monitor under specific conditions — private individuals sniffing without authorization face criminal penalties under S.69B and S.66.

---

## Abbreviations Table

| Abbreviation | Full Form | One-Line Technical Meaning |
|---|---|---|
| ARP | Address Resolution Protocol | Maps IP addresses to MAC addresses on local network segments |
| AXFR | Authoritative Zone Transfer | DNS mechanism transferring complete zone data between nameservers |
| BPF | Berkeley Packet Filter | Filtering syntax used by tcpdump and Wireshark capture filters |
| CAM | Content Addressable Memory | Switch memory storing MAC→port mappings for frame forwarding |
| DAI | Dynamic ARP Inspection | Switch feature validating ARP packets against DHCP snooping binding table |
| DHCP | Dynamic Host Configuration Protocol | Protocol auto-assigning IP addresses, gateway, DNS to clients |
| DNS | Domain Name System | Hierarchical distributed naming system resolving hostnames to IP addresses |
| DNSSEC | DNS Security Extensions | Cryptographic signing of DNS records to detect tampering |
| DoH | DNS over HTTPS | Encrypted DNS queries transported inside HTTPS — port 443 |
| DoQ | DNS over QUIC | Encrypted DNS over QUIC transport protocol — RFC 9250 |
| DoT | DNS over TLS | Encrypted DNS queries transported inside TLS — port 853 |
| DPDPA | Digital Personal Data Protection Act | India's data protection law — 2023 |
| FCS | Frame Check Sequence | 4-byte CRC at end of Ethernet frame for error detection |
| FTP | File Transfer Protocol | Cleartext file transfer — port 21 (control) / 20 (data) |
| HSTS | HTTP Strict Transport Security | Browser policy forcing HTTPS — prevents SSL stripping |
| ICMP | Internet Control Message Protocol | Network diagnostic protocol — ping, traceroute |
| IMAP | Internet Message Access Protocol | Email retrieval protocol — cleartext port 143, encrypted port 993 |
| IP | Internet Protocol | Layer 3 addressing and routing protocol |
| LAN | Local Area Network | Network confined to small geographic area — ARP operates within LAN |
| MAC | Media Access Control | Layer 2 hardware address — 48-bit identifier for network interfaces |
| MITM | Man-in-the-Middle | Attack where attacker intercepts communication between two parties |
| NDP | Neighbor Discovery Protocol | IPv6 equivalent of ARP — uses ICMPv6 |
| NIC | Network Interface Card | Hardware providing network connectivity — can be set to promiscuous mode |
| NS | Name Server (DNS record) | DNS record identifying authoritative nameserver for a domain |
| OUI | Organizationally Unique Identifier | First 3 bytes of MAC — identifies NIC manufacturer |
| pcap | Packet Capture | File format for saved network captures (.pcap / .pcapng) |
| POP3 | Post Office Protocol v3 | Email retrieval — cleartext port 110, encrypted port 995 |
| PTR | Pointer Record (DNS) | Reverse DNS record — maps IP address to hostname |
| SAE | Simultaneous Authentication of Equals | WPA3 key exchange mechanism — replaces WPA2 PSK |
| SFD | Start Frame Delimiter | 1-byte Ethernet field marking start of frame content |
| SMTP | Simple Mail Transfer Protocol | Email transmission — cleartext port 25/587, encrypted port 465 |
| SNMP | Simple Network Management Protocol | Network device management — v1/v2c cleartext, v3 encrypted |
| SPAN | Switched Port Analyzer | Switch port mirroring — copies traffic to monitoring port |
| SSH | Secure Shell | Encrypted remote access — replaces Telnet — port 22 |
| SSL | Secure Sockets Layer | Deprecated predecessor to TLS — still used as term generically |
| TLS | Transport Layer Security | Cryptographic protocol encrypting network communications |
| TTL | Time to Live | DNS record field — how long resolver caches the record (seconds) |
| UDP | User Datagram Protocol | Connectionless Layer 4 protocol — DNS uses UDP 53 by default |
| VPN | Virtual Private Network | Encrypted tunnel for all network traffic |
| WPA3 | Wi-Fi Protected Access 3 | Latest Wi-Fi security standard — uses SAE — resists sniffing |

---

## 🔑 Keywords + Concept Map

**Core Keywords:**

Sniffing · Passive Sniffing · Active Sniffing · Promiscuous Mode · Monitor Mode · Hub · Switch · CAM Table · ARP · ARP Poisoning · ARP Spoofing · ARP Cache · Gratuitous ARP · MAC Flooding · macof · arpspoof · Ettercap · Bettercap · Wireshark · Ethereal · tcpdump · Capture Filter · Display Filter · BPF · DNS · DNS Spoofing · DNS Cache Poisoning · Kaminsky Attack · DNSSEC · DoH · DoT · AXFR · DNS Tunneling · MITM · SSL Stripping · sslstrip · HSTS · DAI · DHCP Snooping · Port Security · Arpwatch · T1040 · T1557 · T1557.002

**Concept Map:**

```text
SNIFFING, ARP POISONING, MAC FLOODING & DNS ATTACKS
│
├── SNIFFING
│   ├── Passive ─────── No packets sent | Hub/Wi-Fi only | Promiscuous mode
│   └── Active ──────── Packets sent | Switched networks | Multiple techniques
│       ├── ARP Poisoning ── Poison endpoint ARP caches → MITM
│       ├── MAC Flooding ─── Overflow switch CAM table → hub behaviour
│       ├── DHCP Spoofing ── Rogue DHCP → control gateway + DNS
│       └── ICMP Redirect ── Modify routing table → traffic via attacker
│
├── VULNERABLE PROTOCOLS
│   ├── Credentials ────── FTP (21) | Telnet (23) | HTTP (80) | POP3 (110)
│   │                      IMAP (143) | SMTP (25) | SNMP v1/v2c (161)
│   └── Secure alts ────── SSH (22) | HTTPS (443) | IMAPS (993) | SNMPv3
│
├── ARP POISONING
│   ├── Root cause ─── ARP stateless + unauthenticated → accepts unsolicited replies
│   ├── Attack ──────── Forge ARP replies → poison victim + gateway ARP caches
│   ├── Result ──────── MITM position → sniff/modify/drop all traffic
│   ├── Tools ───────── arpspoof | Ettercap | Bettercap | Cain & Abel
│   └── Countermeasures DAI | Static ARP | Arpwatch | Encrypted protocols
│
├── MAC FLOODING
│   ├── Root cause ─── CAM table finite size → overflow → unknown unicast flood
│   ├── Attack ──────── macof floods random MACs → CAM full → switch = hub
│   ├── Result ──────── All traffic flooded → passive sniffing works on switch
│   ├── Tools ───────── macof | Yersinia | Ettercap
│   └── Countermeasures Port Security | 802.1X | VLAN segmentation
│
├── DNS ATTACKS
│   ├── DNS Spoofing ────── Forge DNS replies in MITM → redirect single victim
│   ├── Cache Poisoning ─── Inject false records in resolver cache → all users affected
│   ├── Kaminsky (2008) ─── Zone-level poisoning via transaction ID guessing
│   ├── Zone Transfer ───── AXFR → full topology disclosure (reconnaissance)
│   ├── DNS Tunneling ───── C2/exfil via DNS subdomains
│   ├── Amplification ───── Open resolvers → DDoS amplification
│   ├── Tools ───────────── dnsspoof | Ettercap dns_spoof | dnschef | dnscat2
│   └── Countermeasures ─── DNSSEC | DoH | DoT | Disable open recursion | Restrict AXFR
│
├── WIRESHARK / ETHEREAL
│   ├── Capture filters ── BPF syntax | Applied at capture time | Cannot change during capture
│   └── Display filters ── Wireshark syntax | Applied to existing captures | Non-destructive
│
├── MITM OUTCOMES
│   ├── Credential theft ── Cleartext protocols → immediate capture
│   ├── Session hijacking ─ Steal HTTP cookies → impersonate user
│   ├── SSL stripping ───── Downgrade HTTPS → HTTP → read "encrypted" traffic
│   └── DNS control ──────── Control all name resolution → redirect anywhere
│
└── COUNTERMEASURES
    ├── Encryption ────── HTTPS | SSH | TLS | VPN | WPA3 (root fix)
    ├── Network ───────── DAI | Port Security | DHCP Snooping | 802.1X | VLAN
    ├── Detection ─────── Arpwatch | Antisniff | Ping test | DNS test | IDS
    └── DNS-specific ──── DNSSEC | DoH | DoT | Restrict AXFR | Patch resolvers
```

---

## ⚡ Quick Reference Cheatsheet

### 🔍 Passive vs Active Sniffing

| Property | Passive | Active |
|---|---|---|
| Packets sent | ❌ None | ✅ Yes |
| Works on hubs | ✅ Yes | ✅ Yes |
| Works on switches | ❌ No | ✅ Yes |
| Works on Wi-Fi | ✅ Yes (monitor mode) | ✅ Yes |
| Detectability | Very low | Medium-High |
| NIC mode needed | Promiscuous | Promiscuous + attack tool |
| Examples | Wireshark listen | arpspoof + Wireshark |

### 🧪 Vulnerable Protocols Reference

| Protocol | Port | Exposed Data | Secure Replacement | Port |
|---|---|---|---|---|
| HTTP | TCP 80 | Full content, cookies, credentials | HTTPS | TCP 443 |
| FTP | TCP 21/20 | Username, password, files | SFTP/SCP | TCP 22 |
| Telnet | TCP 23 | Everything — keystrokes | SSH | TCP 22 |
| SMTP | TCP 25 | Email content | SMTP+STARTTLS | TCP 587 |
| POP3 | TCP 110 | Email credentials + content | POP3S | TCP 995 |
| IMAP | TCP 143 | Email credentials + content | IMAPS | TCP 993 |
| SNMP v1/v2c | UDP 161 | Community strings, device config | SNMPv3 | UDP 161 |
| DNS | UDP/TCP 53 | Query content, browsing patterns | DoH/DoT | 443/853 |
| LDAP | TCP 389 | Directory credentials | LDAPS | TCP 636 |

### 🎭 ARP Poisoning vs MAC Flooding

| Property | ARP Poisoning | MAC Flooding |
|---|---|---|
| What is attacked | Endpoint ARP caches | Switch CAM table |
| Mechanism | Fake ARP replies to victims | Random MACs → CAM overflow |
| Result | Traffic redirected via attacker | Switch degrades to hub |
| Primary tool | arpspoof, Ettercap | macof, Yersinia |
| Countermeasure | DAI, Static ARP | Port Security |
| Stealth | Moderate | Low (very noisy) |
| Persistence | Must continuously re-send | Must continuously flood |
| Works after ARP cache expires? | No — must re-poison | Yes — switch stays flooded |

### 🌐 DNS Attack Types

| Attack | Scope | Mechanism | Impact |
|---|---|---|---|
| DNS Spoofing | Single victim | Forge reply in MITM position | One user redirected |
| Cache Poisoning | All resolver users | Inject false record in cache | Thousands of users affected |
| Zone Transfer (AXFR) | Reconnaissance | Unauthorized AXFR request | Full topology disclosed |
| DNS Amplification | DDoS victim | Open resolver + spoofed source | Volumetric DDoS |
| DNS Tunneling | Data exfil / C2 | Encode data in DNS queries | Bypasses firewalls |
| Domain Hijacking | Entire domain | Compromise registrar account | Full domain control |
| Hosts File Modification | Single machine | Malware edits hosts file | Local DNS override |

### 📡 Wireshark Filter Quick Reference

**Capture Filters (BPF syntax — before capture):**

```text
host 192.168.1.10          # All traffic to/from IP
port 80                    # Traffic on port 80
tcp port 443               # HTTPS traffic
arp                        # ARP traffic only
port 53                    # DNS traffic
not host 192.168.1.1       # Exclude gateway
net 192.168.1.0/24         # Entire subnet
port 21 or port 23         # FTP or Telnet
```

**Display Filters (Wireshark syntax — after capture):**

```text
ip.addr == 192.168.1.10    # Traffic to/from IP
ip.src == 192.168.1.10     # From specific IP
http                        # All HTTP
http.request.method == "POST"   # HTTP POST only
dns                         # All DNS
dns.qry.name == "bank.com" # DNS for specific domain
arp.opcode == 1            # ARP Requests
arp.opcode == 2            # ARP Replies
arp.isgratuitous == 1      # Gratuitous ARP (poisoning indicator)
tcp.port == 21             # FTP
telnet                     # Telnet
ftp                        # FTP
http contains "password"   # HTTP with "password" in content
tcp.flags.syn == 1         # SYN packets
!(ip.addr == 192.168.1.1)  # Exclude gateway
```

### 🛡️ Countermeasures Summary

| Attack | Primary Countermeasure | Secondary Countermeasure |
|---|---|---|
| Passive Sniffing | Use switches (not hubs) | Encrypt all traffic (TLS/SSH/VPN) |
| Active Sniffing (general) | Encrypt all traffic | Network segmentation + monitoring |
| ARP Poisoning | Dynamic ARP Inspection (DAI) | Static ARP entries + Arpwatch |
| MAC Flooding | Port Security (max MACs/port) | 802.1X authentication |
| DNS Spoofing | DNSSEC + DoH/DoT | Encrypted protocols (HTTPS) |
| DNS Cache Poisoning | Source port randomization | DNSSEC deployment |
| DNS Zone Transfer | Restrict AXFR to trusted IPs | Monitor DNS logs |
| SSL Stripping | HSTS (HTTP Strict Transport Security) | HTTPS Everywhere |
| Wi-Fi Sniffing | WPA3 (SAE) | 802.1X Enterprise |

### ⚖️ Indian Legal Reference

| Law | Section | Offence | Penalty |
|---|---|---|---|
| IT Act 2000 | S.43(a) | Unauthorized network access / sniffing | Civil ₹1 crore |
| IT Act 2000 | S.66 | Criminal interception of data | 3 yrs + ₹5L |
| IT Act 2000 | S.66B | Receiving intercepted/stolen data | 3 yrs + ₹1L |
| IT Act 2000 | S.69B | Unauthorized network traffic monitoring | 3 yrs + ₹5L |
| IT Act 2000 | S.66F | Interception of critical infrastructure | Life imprisonment |
| Indian Telegraph Act | S.26 | Intercepting electronic communications | Up to 3 yrs |
| IPC | S.419/420 | Fraud via DNS spoofing/phishing | Up to 7 yrs + fine |
| DPDPA 2023 | — | Data breach via unencrypted network | ₹250 crore |

---

## ✅ Session Revision Snapshot

### ⚡ TL;DR — 5 Bullets

- Passive sniffing = no packets sent = works on hubs and Wi-Fi only; Active sniffing = packets sent = works on switched networks via ARP poisoning (poisons endpoint ARP caches) or MAC flooding (overflows switch CAM table → switch behaves like a hub). This distinction drives most sniffing MCQs.

- ARP is stateless and unauthenticated — it accepts unsolicited ARP replies (gratuitous ARP) without any verification. Attackers exploit this by sending forged ARP replies to both victim and gateway → traffic flows through attacker → MITM position established. DAI (Dynamic ARP Inspection) is the primary countermeasure at the switch level.

- MAC flooding uses macof to flood random MACs → CAM table overflows → switch cannot learn new entries → floods all traffic to all ports → passive sniffing now works on a switched network. Port Security (limiting MACs per port with violation = shutdown) is the direct countermeasure.

- DNS cache poisoning injects false records into a resolver's cache — affecting ALL users of that resolver. The Kaminsky Attack (2008) exploited 16-bit transaction IDs to achieve zone-level poisoning — fixed by source port randomization. DNSSEC, DoH, and DoT are the current countermeasures. DNS zone transfer (AXFR) abuse reveals full network topology — must be restricted to trusted secondary NS IPs only.

- Wireshark capture filters (BPF syntax) are applied before capture and determine what is recorded. Display filters (Wireshark syntax) are applied to existing captures and only control visibility — they do not delete packets. Ethereal is the old name for Wireshark (renamed 2006). Follow TCP Stream reconstructs full application sessions from captures.

---

### 🎯 MCQ-Likely Concepts

- [ ] Passive vs Active sniffing — which needs packets sent, which works on switches
- [ ] Promiscuous mode — what it is, when it is legitimate
- [ ] Monitor mode vs promiscuous mode — wireless vs wired difference
- [ ] ARP stateless vulnerability — accepts unsolicited replies (gratuitous ARP)
- [ ] ARP poisoning attack flow — both victim AND gateway must be poisoned
- [ ] IP forwarding — why attacker must enable it to avoid detection
- [ ] Gratuitous ARP — definition, legitimate uses, attacker abuse
- [ ] ARP operation codes — 1 = Request, 2 = Reply
- [ ] MAC flooding — macof tool, CAM overflow, switch → hub behaviour
- [ ] Port Security — primary countermeasure for MAC flooding
- [ ] Dynamic ARP Inspection (DAI) — requires DHCP Snooping
- [ ] Protocols susceptible to sniffing — Telnet, FTP, HTTP, SNMP v1/v2c, POP3, IMAP
- [ ] Secure replacements — SSH (replaces Telnet), SFTP (replaces FTP), HTTPS (replaces HTTP)
- [ ] DNS cache poisoning vs DNS spoofing — scope difference
- [ ] Kaminsky Attack — year (2008), mechanism (transaction ID guessing), fix (source port randomization)
- [ ] AXFR zone transfer — reconnaissance, must be restricted
- [ ] DNS tunneling — tools (dnscat2, Iodine) — C2/exfil over DNS
- [ ] DNSSEC — prevents tampering via cryptographic signing
- [ ] DoH port (443), DoT port (853)
- [ ] Wireshark capture filter syntax (BPF) vs display filter syntax (Wireshark)
- [ ] Ethereal = Wireshark — renamed 2006
- [ ] Follow TCP Stream — reconstructs application-layer sessions
- [ ] `arp.opcode == 1` (Request) / `arp.opcode == 2` (Reply) display filter
- [ ] Antisniff — promiscuous mode detection tool
- [ ] Ping test / DNS test / ARP test — promiscuous mode detection methods
- [ ] SSL stripping — sslstrip tool, HSTS countermeasure
- [ ] IT Act S.69B — unauthorized network monitoring
- [ ] IT Act S.66F — critical infrastructure interception = life imprisonment
- [ ] SNMP v1/v2c community strings — cleartext — SNMPv3 is the fix

---

### 💼 Interview-Likely

- Explain the difference between passive and active sniffing with a network topology example.
- Why does ARP poisoning work — what fundamental design flaw does it exploit?
- What is a gratuitous ARP and how do attackers abuse it?
- Walk me through an ARP poisoning attack step by step.
- What is the difference between MAC flooding and ARP poisoning?
- Why must an attacker enable IP forwarding during an ARP poisoning MITM attack?
- What is the Kaminsky DNS cache poisoning attack and how was it fixed?
- What is the difference between a DNS capture filter and a display filter in Wireshark?
- Name five protocols susceptible to sniffing and their secure alternatives.
- What is DNSSEC and what does it NOT protect against?
- How would you detect if someone is running a sniffer on your network segment?
- What is Dynamic ARP Inspection and what does it require to function?

---

## Next Session Bridge

Session 15 completes the network interception sub-phase — covering how attackers position themselves to intercept and manipulate network traffic at the Layer 2 and DNS levels. The progression: endpoint attacks (Trojans, viruses) → endpoint-to-network attacks (sniffing, ARP, DNS) → now network-level flooding and volume attacks.

Session 16 moves to DoS (Denial of Service) and Session Hijacking. Where sniffing is passive interception of sessions, session hijacking is active takeover of established sessions. And where ARP poisoning redirects traffic, DoS/DDoS simply overwhelms and kills it — targeting availability rather than confidentiality or integrity. The TCP/IP knowledge from this session (SYN flags, sequence numbers, session state) directly applies to understanding SYN flooding and TCP session hijacking in Session 16.

---

<details>
<summary>📖 Glossary</summary>

| Term | Definition |
|---|---|
| 802.1X | IEEE standard for port-based network access control — authenticates devices before network access |
| Antisniff | Tool by L0pht Research for detecting promiscuous mode NICs on a network segment |
| ARP | Address Resolution Protocol — maps Layer 3 IP addresses to Layer 2 MAC addresses |
| ARP Cache | Host-maintained table of IP→MAC mappings from recent ARP exchanges |
| ARP Poisoning | Attack sending forged ARP replies to update victim ARP caches with attacker's MAC |
| ARP Request | Broadcast ARP packet asking "who has IP X?" — opcode 1 |
| ARP Reply | Unicast ARP response "IP X is at MAC Y" — opcode 2 |
| Arpwatch | Linux daemon monitoring ARP traffic and alerting on IP→MAC pairing changes |
| AXFR | DNS zone transfer request — transfers all DNS records from primary to secondary NS |
| Bettercap | Modern open-source framework for network attacks including ARP poisoning and DNS spoofing |
| BPF | Berkeley Packet Filter — filter syntax used by tcpdump and Wireshark capture filters |
| CAM Table | Content Addressable Memory table — maps MAC addresses to switch port numbers |
| Cain & Abel | Windows-based password recovery and network attack tool supporting ARP poisoning |
| DAI | Dynamic ARP Inspection — switch feature validating ARP packets against DHCP snooping table |
| DHCP Snooping | Switch feature tracking valid IP→MAC→port mappings from DHCP exchanges |
| dnscat2 | DNS tunneling tool providing encrypted C2 channel over DNS protocol |
| dnschef | DNS proxy tool for spoofing DNS responses — used in penetration testing |
| DNSSEC | DNS Security Extensions — adds cryptographic signatures to DNS records |
| DoH | DNS over HTTPS — encrypts DNS queries inside HTTPS — port 443 |
| DoQ | DNS over QUIC — encrypts DNS over QUIC transport protocol — port 853 |
| DoT | DNS over TLS — encrypts DNS queries inside TLS — port 853 |
| Ettercap | Open-source MITM framework supporting ARP poisoning, DNS spoofing, traffic filtering |
| Ethereal | Original name of Wireshark — renamed in 2006 |
| Gratuitous ARP | Unsolicited ARP reply announcing own IP→MAC mapping — abused for ARP poisoning |
| HSTS | HTTP Strict Transport Security — browser policy requiring HTTPS only — blocks SSL stripping |
| Iodine | DNS tunneling tool encoding IP traffic inside DNS queries |
| Kaminsky Attack | 2008 DNS cache poisoning technique by Dan Kaminsky — zone-level poisoning via transaction ID guessing |
| macof | Tool generating random MAC addresses at high rate for MAC flooding attacks |
| MITM | Man-in-the-Middle — attack positioning attacker between two communicating parties |
| Monitor Mode | Wireless NIC mode capturing all 802.11 frames regardless of destination — for Wi-Fi sniffing |
| NDP | Neighbor Discovery Protocol — IPv6 replacement for ARP using ICMPv6 |
| OUI | Organizationally Unique Identifier — first 3 bytes of MAC address identifying manufacturer |
| pcap | Packet capture file format (.pcap / .pcapng) used by Wireshark and tcpdump |
| Promiscuous Mode | NIC mode accepting all frames regardless of destination MAC — enables passive sniffing |
| Port Security | Switch feature limiting MAC addresses per port — primary MAC flooding countermeasure |
| SAE | Simultaneous Authentication of Equals — WPA3 key exchange — resists offline attacks |
| SPAN Port | Switch Port Analyzer — copies traffic from multiple ports to a monitoring port |
| sslstrip | Tool downgrading HTTPS connections to HTTP in MITM scenarios |
| tcpdump | Command-line packet capture tool using BPF filters |
| Wireshark | World's most widely used open-source network protocol analyzer — renamed from Ethereal in 2006 |
| XArp | Windows/Linux ARP monitoring tool — alerts on ARP cache changes |
| Yersinia | Network attack tool supporting MAC flooding, DHCP attacks, STP manipulation |
| Zone Transfer | DNS mechanism (AXFR) copying complete zone data — abused for reconnaissance if unrestricted |

</details>

---