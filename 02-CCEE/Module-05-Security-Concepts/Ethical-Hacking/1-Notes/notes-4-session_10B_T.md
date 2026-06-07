# 📡 Cybersecurity Study Notes — Session 10B

Personal notes I'm maintaining while studying ethical hacking and cybersecurity concepts.
This session covers port/network/vulnerability scanning, TCP three-way handshake, all scan types (SYN, Connect, FIN, NULL, XMAS, IDLE), Nessus internals, Burp Suite proxy mechanics, and attack surface mapping.

> [!NOTE]
> Session 10B is about **Phase 2 — Scanning & Enumeration**. Session 10A built the map (what exists, where it is). Session 10B explores the map (what's open, what's vulnerable).

---

## 📚 Table of Contents

- [Where This Session Fits](#-where-this-session-fits)
- [Foundation Knowledge — TCP, UDP, Ports](#-foundation-knowledge)
- [Things to Remember About Scanning](#things-to-remember-about-scanning)
- [Section 1 — The Three Types of Scanning](#section-1--the-three-types-of-scanning)
  - [Network Scanning — Who Is Alive?](#12-network-scanning--who-is-alive)
  - [Port Scanning — What Services Are Running?](#13-port-scanning--what-services-are-running)
  - [Vulnerability Scanning — What Is Broken?](#14-vulnerability-scanning--what-is-broken)
- [Section 2 — TCP Three-Way Handshake](#section-2--tcp-three-way-handshake)
  - [TCP Flags — The Vocabulary](#22-tcp-flags)
  - [The Handshake — Step by Step](#23-the-three-way-handshake--step-by-step)
  - [Closed Port Response](#24-what-happens-when-port-is-closed)
  - [Filtered Port Response](#25-what-happens-when-port-is-filtered)
- [Section 3 — TCP Scan Types](#section-3--tcp-scan-types)
  - [TCP Connect Scan](#32-tcp-connect-scan--the-full-handshake-scan)
  - [SYN Scan (Stealth Scan)](#33-syn-scan--the-stealth-scan)
  - [FIN Scan](#34-fin-scan)
  - [NULL Scan](#35-null-scan)
  - [XMAS Scan](#36-xmas-scan)
  - [FIN vs NULL vs XMAS Summary](#37-fin-vs-null-vs-xmas--comparison)
  - [IDLE / Zombie Scan](#38-idle-scan-zombie-scan)
  - [Complete Scan Type Comparison](#39-complete-scan-type-comparison-table)
  - [UDP Scanning](#310-udp-scanning)
- [Section 4 — Vulnerability Scanning & Nessus](#section-4--vulnerability-scanning--nessus-deep-dive)
  - [What is Nessus?](#41-what-is-nessus)
  - [How Nessus Works Internally](#42-how-nessus-works-internally--plugin-architecture)
  - [Nessus Scan Types](#43-nessus-scan-types)
  - [Understanding CVSS](#44-understanding-cvss)
  - [Credentialed vs Uncredentialed](#45-credentialed-vs-uncredentialed-scanning)
- [Section 5 — Burp Suite](#section-5--burp-suite)
  - [What is Burp Suite?](#51-what-is-burp-suite)
  - [How HTTP Proxy Interception Works](#52-how-http-proxy-interception-works)
  - [How Burp Handles HTTPS (SSL Bumping)](#53-how-burp-handles-https)
  - [Burp Suite Tools](#54-burp-suite-tools)
  - [Spidering / Crawling](#55-spidering--crawling)
  - [Attack Surface Mapping](#56-attack-surface-mapping)
- [Section 6 — MITRE ATT&CK Mapping](#section-6--mitre-attck-mapping--scanning-phase)
- [Section 7 — 2026 Context: Evolution of Scanning](#section-7--2026-context)
  - [AI-Assisted Scanning](#71-ai-assisted-scanning)
  - [Cloud Scanning Challenges](#72-cloud-scanning-challenges)
  - [Evasion Techniques](#73-evasion-techniques)
- [Key Takeaways](#-session-10b--key-takeaways)
- [Glossary](#-session-10b--glossary)

---

## 🗺️ Where This Session Fits

```
  PHASE 1            PHASE 2                    PHASE 3      PHASE 4    PHASE 5
  RECONNAISSANCE  →  SCANNING & ENUMERATION  →  GAINING  →  MAINTAIN → COVER
  (Session 10A)      (Session 10B) ← HERE       ACCESS      ACCESS     TRACKS
```

Within Phase 2 — Scanning:

| Step | What It Does | Question Answered |
|---|---|---|
| 1. Network Scanning | Find LIVE HOSTS | Who is online? |
| 2. Port Scanning | Find OPEN PORTS on live hosts | What's running? |
| 3. Service Detection | Identify SERVICES on those ports | What version? |
| 4. Vulnerability Scan | Find WEAKNESSES in those services | What's broken? |
| 5. Attack Surface Map | Compile COMPLETE picture for Phase 3 | Where do I attack? |

---

## 📌 Foundation Knowledge

<details>
<summary>🔧 TCP vs UDP — Must Know Before Scanning</summary>

| | TCP | UDP |
|---|---|---|
| **Type** | Connection-oriented | Connectionless |
| **Delivery** | Guaranteed — acknowledgement required | No guarantee — fire and forget |
| **Handshake** | Yes — establishes connection before data | No handshake — sends immediately |
| **Used by** | HTTP, HTTPS, SSH, FTP, SMTP, RDP | DNS, DHCP, VoIP, video streaming, gaming |
| **Analogy** | Registered letter — confirmed delivery | Postcard — sent but no confirmation |

</details>

<details>
<summary>🔢 Well-Known Port Numbers — Must Memorize</summary>

| Port | Service | Notes |
|---|---|---|
| 20/21 | FTP | File Transfer Protocol |
| 22 | SSH | Secure Shell — remote terminal |
| 23 | Telnet | Insecure remote terminal — **never use** |
| 25 | SMTP | Sending email |
| 53 | DNS | Domain Name System |
| 80 | HTTP | Web traffic (unencrypted) |
| 110 | POP3 | Receiving email |
| 143 | IMAP | Email access |
| 443 | HTTPS | Web traffic (encrypted) |
| 445 | SMB | Windows file sharing |
| 3306 | MySQL | Database |
| 3389 | RDP | Remote Desktop Protocol (Windows) |
| 5432 | PostgreSQL | Database |
| 8080 | HTTP Alternate | Often development/proxy |
| 8443 | HTTPS Alternate | — |

**Key concept:** IP address = identifies the MACHINE (house address). Port number = identifies the SERVICE (apartment number in the house). Together: `192.168.1.1:80` = machine at 192.168.1.1, web server on port 80.

</details>

---

## Things to Remember About Scanning

| Misconception | Reality |
|---|---|
| "Port scanning and network scanning are the same thing" | Network scanning finds WHICH HOSTS ARE ALIVE. Port scanning finds WHICH PORTS ARE OPEN on those hosts. Two different operations. |
| "A port being open means the service is vulnerable" | Open port = door exists. Vulnerability = door has a broken lock. Open ≠ vulnerable. |
| "SYN scan is undetectable" | SYN scan is STEALTHIER than full connect scan — but NOT invisible. Good IDS/SIEM systems detect SYN scans in 2026. |
| "XMAS scan works on all systems" | XMAS, NULL, and FIN scans do NOT work reliably on Windows. Windows doesn't follow RFC 793 strictly for these edge cases. |
| "Vulnerability scanners find all vulnerabilities" | They find KNOWN vulnerabilities (CVEs). They miss business logic flaws, chained vulns, zero-days, and context-specific weaknesses. |
| "Burp Suite is only for web application testing" | Burp is fundamentally a PROXY — it can intercept ANY HTTP/HTTPS traffic including mobile apps, APIs, IoT web interfaces. |
| "I should run vulnerability scans before port scans" | Correct sequence is ALWAYS: Network Scan → Port Scan → Service Detection → Vuln Scan |

---

## Section 1 — The Three Types of Scanning

### 1.1 The Scanning Phase — Why It Exists

After footprinting (Phase 1), I know WHAT EXISTS. Scanning tells me the STATE of what exists. Three increasingly specific questions:

| Question | Scanning Type | Analogy |
|---|---|---|
| Which hosts are ALIVE and reachable? | **Network Scanning** | Which buildings have LIGHTS ON? (who's home?) |
| Which SERVICES are running on those hosts? | **Port Scanning** | Which DOORS AND WINDOWS are open in those buildings? |
| Which services have KNOWN WEAKNESSES? | **Vulnerability Scanning** | Which open doors have BROKEN LOCKS? |

The sequence exists for **efficiency and precision** — don't check for broken locks before confirming the building exists.

---

### 1.2 Network Scanning — "Who Is Alive?"

Identifies which IP addresses in a given range are currently active. Also called: Host Discovery, Ping Sweep, Live Host Identification.

**Why:** A typical org might own 256 IP addresses. Not all are in use. Scanning a dead host for open ports = wasted time and unnecessary noise.

#### Host Discovery Methods

| Method | How It Works | Pros | Cons |
|---|---|---|---|
| **ICMP Echo Request (Ping)** | Send ICMP Echo Request → alive host sends Echo Reply | Simple, fast | Modern firewalls often block ICMP — no reply ≠ host is down |
| **TCP SYN Ping** | Send TCP SYN to common port (80, 443) → alive host responds with SYN-ACK or RST | Works through many firewalls that block ICMP | Some hosts block all TCP too |
| **ARP Ping** *(local network only)* | ARP works at Layer 2 — every connected device MUST respond | Most reliable on local networks | Cannot cross routers |
| **UDP Ping** | Send UDP packet → closed port returns ICMP Port Unreachable (host alive!) | Useful when TCP/ICMP blocked | Less reliable |

**NMAP Host Discovery Options:**

| Flag | Method |
|---|---|
| `-sn` | Ping scan only (no port scan) — host discovery only |
| `-PE` | ICMP Echo Request ping |
| `-PS` | TCP SYN ping (specify ports: `-PS80,443`) |
| `-PA` | TCP ACK ping |
| `-PU` | UDP ping |
| `-PR` | ARP ping (local network) |

---

### 1.3 Port Scanning — "What Services Are Running?"

Probes specific ports on known alive hosts to determine if services are listening.

**Why each open port matters:**

| Open Port | What It Means | Attack Potential |
|---|---|---|
| 22 (SSH) | Remote terminal access | Brute-force credentials? SSH exploits? |
| 80/443 (HTTP/S) | Web application | Run web app tests? |
| 445 (SMB) | Windows file sharing | EternalBlue? Password attacks? |
| 3389 (RDP) | Remote Desktop | Credential attacks? BlueKeep? |
| 3306 (MySQL) | Exposed database | SQL auth attacks? |

Each open port is a **potential attack vector**.

#### Port States — The Responses

| State | Meaning | Action |
|---|---|---|
| **OPEN** | Service IS actively listening. Port accepted the connection. | Identify service + version → attack planning |
| **CLOSED** | No service listening. Host is reachable but port not in use. | Still useful — confirms host is alive, OS may be detectable |
| **FILTERED** | Firewall/ACL preventing probe packets from reaching port. Can't tell if open or closed. | Try different probe type (TCP vs UDP vs ICMP). Most annoying result. |
| **UNFILTERED** | Reachable but state indeterminate. Typically from ACK scans. | — |
| **OPEN\|FILTERED** | Can't determine — typically from FIN, NULL, XMAS scans on non-responding ports. | — |

---

### 1.4 Vulnerability Scanning — "What Is Broken?"

Takes the list of open ports/services from port scanning and checks each against a **database of known vulnerabilities (CVEs)**.

**The difference:**

| Knowledge | Value |
|---|---|
| "Port 80 is open running Apache 2.4.49" | Useful |
| "Apache 2.4.49 has CVE-2021-41773 — path traversal RCE with CVSS 9.8" | **ACTIONABLE** |

#### How Vulnerability Scanners Work Internally

| Step | What Happens |
|---|---|
| 1 — Service Detection | Identify exactly which service/version on each port (banner grabbing, fingerprinting) |
| 2 — CVE Database Lookup | Check vulnerability database for the identified version |
| 3 — Verification Probes | Send specific probes to VERIFY the vuln is actually present and exploitable |
| 4 — Risk Scoring | Rate severity using CVSS (0.0–10.0) |
| 5 — Report Generation | Consolidate into prioritized report with CVE ID, CVSS, description, remediation |

#### What Scanners Find vs Miss

| ✅ Finds | ❌ Misses |
|---|---|
| Outdated software with known CVEs | Zero-day vulnerabilities |
| Default credentials (admin/admin) | Business logic flaws |
| Misconfigured services (anon FTP, open SMTP relay) | Chained vulnerabilities |
| Missing patches and updates | Auth bypass via application logic |
| Weak crypto configs (SSL/TLS issues) | IDOR |
| Open/unnecessary services | Context-specific misconfigs |
| | Social engineering / physical weaknesses |

> [!IMPORTANT]
> Vulnerability scanners are a **floor** — the minimum acceptable testing. Manual penetration testing is required for comprehensive coverage. Best practice: automated scanner first → manual validation and expansion.

---

## Section 2 — TCP Three-Way Handshake

### 2.1 Why I Must Understand This Before Any Scan Type

Every TCP scan type is a **modification or interruption** of the three-way handshake. Understanding the handshake = understanding ALL TCP scan types.

---

### 2.2 TCP Flags

TCP packets have a flags field containing 6 control bits. Each is either ON (1) or OFF (0).

| Flag | Symbol | Purpose |
|---|---|---|
| **SYN** | S | **Synchronize** — "I want to start a connection." Used in first step of handshake. |
| **ACK** | A | **Acknowledge** — "I received what you sent." Present in most packets after initial SYN. |
| **FIN** | F | **Finish** — "I'm done sending data. Close connection." Normal termination. |
| **RST** | R | **Reset** — "Stop. Close this connection immediately." Sent on refusal/error. |
| **PSH** | P | **Push** — "Process this data immediately, don't buffer." |
| **URG** | U | **Urgent** — "This data is high priority." Rarely used in modern networking. |

**Notation used in scan types:**

| Packet | Flags |
|---|---|
| SYN packet | `[S]` |
| SYN-ACK | `[S,A]` |
| ACK | `[A]` |
| FIN | `[F]` |
| RST | `[R]` |
| FIN+PSH+URG | `[F,P,U]` ← **XMAS scan** |
| No flags | `[ ]` ← **NULL scan** |

---

### 2.3 The Three-Way Handshake — Step by Step

Client wants to establish TCP connection with Server on port 80.

```
CLIENT                                    SERVER (port 80)
  |                                              |
  |------- SYN [SEQ=1000] ------------------>   |
  |   "Hello, I want to connect.                |
  |    My sequence starts at 1000"              |
  |                                              |
  |   <------ SYN-ACK [SEQ=5000,ACK=1001] ---  |
  |   "Hello back. I'm ready.                   |
  |    My sequence starts at 5000.              |
  |    I received your 1000 — next I expect 1001"|
  |                                              |
  |------- ACK [ACK=5001] ------------------>   |
  |   "Got it. CONNECTION ESTABLISHED."          |
  |                                              |
  |======== DATA FLOWS BOTH WAYS ============== |
```

| Step | Who Sends | Flags | What It Means |
|---|---|---|---|
| **Step 1 — SYN** | Client | `[S]` SEQ=1000 | "I want to connect. My first sequence number is 1000." |
| **Step 2 — SYN-ACK** | Server | `[S,A]` SEQ=5000, ACK=1001 | "Received your SYN. I'm ready. My sequence starts at 5000. I expect byte 1001 next from you." |
| **Step 3 — ACK** | Client | `[A]` ACK=5001 | "Received your SYN-ACK. Connection is now ESTABLISHED." |

> [!TIP]
> **Key insight:** The ACK number is ALWAYS one more than the received SEQ. This is how TCP confirms exactly which byte was received.

**What is a Sequence Number?** Every byte of TCP data has a sequence number, allowing the receiver to reassemble data in correct order even if packets arrive out of order. Initial sequence number is randomly chosen (security measure).

**Connection Termination:** FIN → FIN-ACK → FIN → FIN-ACK (four steps — each side closes independently). Or RST → immediate termination (abrupt, no graceful goodbye).

---

### 2.4 What Happens When Port is Closed

```
CLIENT                                    SERVER (port 9999 — CLOSED)
  |                                              |
  |------- SYN [SEQ=1000] ------------------>   |
  |   <------- RST-ACK [SEQ=0,ACK=1001] -----  |
  |   "Nothing is listening on port 9999.        |
  |    Connection REFUSED."                       |
```

**RST-ACK response = port is CLOSED but HOST IS ALIVE.** This is valuable — confirms host exists even without SYN-ACK.

---

### 2.5 What Happens When Port is Filtered

```
CLIENT                                    FIREWALL → SERVER
  |                                              |
  |------- SYN [SEQ=1000] ------------------>   |
  |                        [FIREWALL DROPS IT]  |
  |   (no response at all — timeout occurs)     |
  |   (Port is FILTERED)                         |
```

**No response = filtered = firewall is blocking.** Attacker knows a firewall is protecting this port, but doesn't know if a service is behind it.

---

## Section 3 — TCP Scan Types

### 3.1 Framework for Understanding Any Scan

For every scan type, I need to understand:

1. **What packets are sent?** (Which flags?)
2. **What responses are expected?** (Open vs Closed vs Filtered)
3. **Why was this scan created?** (What problem does it solve?)
4. **Advantages?** (Stealth? Speed? Bypass firewalls?)
5. **Limitations?** (What doesn't it work against?)

---

### 3.2 TCP Connect Scan — The Full Handshake Scan

**Also called:** Full Open Scan, Full TCP Connect Scan · **NMAP:** `nmap -sT [target]`

**What's sent:** Complete three-way handshake → then RST-ACK to close

```
OPEN PORT:                                CLOSED PORT:
SCANNER           TARGET (port 80)        SCANNER           TARGET (port 9999)
  |--- SYN ----->   |                       |--- SYN ----->   |
  |<-- SYN-ACK --   |                       |<-- RST-ACK --   |
  |--- ACK ----->   | ← ESTABLISHED         |  (CLOSED)        |
  |--- RST-ACK ->   | ← Close               |                   |

FILTERED PORT:
SCANNER           FIREWALL
  |--- SYN ----->   |
  |  (no response — timeout)
  |  (FILTERED)
```

| | Detail |
|---|---|
| **Why created** | Original, most straightforward method. Uses OS network stack — no special privileges. |
| **Advantages** | ✔ No root needed · ✔ Most reliable results · ✔ Works on ALL OSes |
| **Limitations** | ✘ VERY NOISY — most easily detected · ✘ OS logs the completed connection · ✘ Application logs the attempt · ✘ IDS/SIEM flags immediately |
| **When used** | When stealth is NOT required. When running without root. When you need absolutely reliable results. Rarely used in professional pentests — SYN scan preferred. |

**Why it's noisy:** When full TCP connect completes, the target OS kernel records it in its connection log. The application (e.g., Apache) also logs it. Two separate log systems record the activity.

---

### 3.3 SYN Scan — The Stealth Scan

**Also called:** Half-Open Scan, Stealth Scan · **NMAP:** `sudo nmap -sS [target]`

**What's sent:** SYN → SYN-ACK (if open) → **RST** (scanner sends reset — does NOT complete handshake)

```
OPEN PORT:                                CLOSED PORT:
SCANNER           TARGET (port 80)        SCANNER           TARGET (port 9999)
  |--- SYN ----->   |                       |--- SYN ----->   |
  |<-- SYN-ACK --   |                       |<-- RST-ACK --   |
  |--- RST ----->   | ← NEVER completed     |  (CLOSED)        |
  | (port is OPEN)  |                       |                   |
```

**Why it's called "half-open":**

| Traditional TCP | SYN Scan |
|---|---|
| SYN → SYN-ACK → **ACK** (3 steps = complete) | SYN → SYN-ACK → **RST** (interrupted at step 2) |

Only the FIRST HALF of the handshake completes.

| | Detail |
|---|---|
| **Why created** | TCP Connect completes handshake → OS logs it. SYN scan NEVER completes → OS never records a completed connection. RST tears down the half-open connection silently. |
| **Advantages** | ✔ Stealthier than Connect scan · ✔ Faster · ✔ Most widely used in professional pentests · ✔ Definitive results |
| **Limitations** | ✘ Requires ROOT (raw packet manipulation) · ✘ Good IDS detects incomplete handshakes · ✘ Stateful firewalls track SYN-RST patterns |
| **When used** | Default and preferred scan type in professional engagements |

> [!WARNING]
> **What "stealthy" really means in 2026:** In the early 2000s, SYN scan was genuinely hard to detect. In 2026, modern SIEM/EDR/IDS (Suricata, Snort, CrowdStrike, SentinelOne, Microsoft Sentinel) all detect SYN scan patterns. "Stealth" now means: harder to detect than full connect scan and doesn't leave application-level logs. NOT completely invisible.

**Why does it need root?** Standard TCP connect uses the OS network stack (no special access). SYN scan sends RAW TCP packets with manually crafted headers. Raw packet creation requires root/admin privileges. NMAP uses libpcap for this.

**For TRUE stealth in 2026:** Slow the scan down (`-T0`) · Use random port ordering · Use decoy addresses (`-D`) · Fragment packets (`-f`) · Use IDLE scan

---

### 3.4 FIN Scan

**Also called:** Stealth FIN Scan · **NMAP:** `sudo nmap -sF [target]`

**What's sent:** TCP FIN packet with no prior connection — "I'm finished" when there IS no connection.

```
OPEN PORT:                                CLOSED PORT:
SCANNER           TARGET (port 80)        SCANNER           TARGET (port 9999)
  |--- FIN ----->   |                       |--- FIN ----->   |
  |  (NO RESPONSE)  |  ← port is OPEN       |<-- RST-ACK --   |
  |                  |                       |  (CLOSED)        |
```

**Why it works — RFC 793 rule:**

| Scenario | RFC 793 Says | Result |
|---|---|---|
| Unexpected packet arrives at **OPEN** port | "Discard it silently" | **No reply** = port is OPEN |
| Unexpected packet arrives at **CLOSED** port | "Response MUST be RST" | **RST-ACK** = port is CLOSED |

| | Detail |
|---|---|
| **Advantages** | ✔ Bypasses some firewalls that only filter SYN packets · ✔ Stealthier than SYN against simple firewalls · ✔ No connection logs |
| **Limitations** | ✘ **Does NOT work on Windows** (sends RST-ACK for both open AND closed) · ✘ Open ports return no response = ambiguous (`open|filtered`) · ✘ Modern IDS detects unusual FIN without prior SYN |

---

### 3.5 NULL Scan

**NMAP:** `sudo nmap -sN [target]`

**What's sent:** TCP packet with **NO FLAGS SET** at all — completely empty flag field.

```
TCP Flags: [ ] (empty — all bits = 0)
```

**Why it works:** Same RFC 793 principle as FIN scan. A flagless packet is completely invalid. No legitimate system would ever send one.

| Response | Meaning |
|---|---|
| No reply | Port is OPEN (silently discarded the invalid packet) |
| RST-ACK | Port is CLOSED |

| | Detail |
|---|---|
| **Advantages** | ✔ Can bypass older stateful firewalls · ✔ Completely invalid packet — some IDS miss it · ✔ No application logs |
| **Limitations** | ✘ Does NOT work on Windows · ✘ Results are `open|filtered` (ambiguous) · ✘ Modern IDS detects flagless packets · ✘ Requires root |

---

### 3.6 XMAS Scan

**Also called:** Christmas Tree Scan · **NMAP:** `sudo nmap -sX [target]`

**What's sent:** TCP packet with THREE FLAGS set simultaneously: **FIN + PSH + URG** = `[F,P,U]`

**Why it's called XMAS:**

```
TCP Flag Field:
  URG PSH RST SYN FIN ACK
   1   1   0   0   1   0    ← XMAS scan (3 lights on = Christmas tree)
   0   0   0   1   0   0    ← SYN scan (only SYN lit)
   0   0   0   0   0   0    ← NULL scan (no lights)
   0   0   0   0   1   0    ← FIN scan (only FIN lit)
```

With three flags "lit up," it looks like a Christmas tree with lights on.

**Same RFC 793 exploitation:** FIN+PSH+URG is completely illogical and invalid. No legitimate TCP implementation would create this combination.

| Response | Meaning |
|---|---|
| No reply | Port is OPEN |
| RST-ACK | Port is CLOSED |

| | Detail |
|---|---|
| **Advantages** | ✔ Bypasses some legacy firewall rules · ✔ Unusual flag combo may confuse simplistic IDS · ✔ Minimal logging |
| **Limitations** | ✘ Does NOT work on Windows · ✘ `open|filtered` results · ✘ Modern IDS flags invalid flag combos immediately · ✘ Requires root |

---

### 3.7 FIN vs NULL vs XMAS — Comparison

All three are from the same family — **RFC exploitation scans**. They differ only in which flags are set.

| Scan Type | Flags Sent | Open Response | Closed Response |
|---|---|---|---|
| **FIN** | `[F]` only | No response | RST-ACK |
| **NULL** | `[ ]` no flags | No response | RST-ACK |
| **XMAS** | `[F,P,U]` | No response | RST-ACK |

**All three:**
- ✅ Work on RFC-compliant UNIX/Linux systems
- ❌ Do NOT work on Windows
- ✅ Bypass SYN-filtering firewalls
- ❌ Detected by modern IDS
- Show open ports as `open|filtered`

**Why three scans with the same result?** Different flag combinations bypass DIFFERENT specific firewall rules:

| Firewall Rule | Use Instead |
|---|---|
| "Block all FIN packets" | NULL or XMAS |
| "Block empty flag packets" | FIN or XMAS |
| "Block URG+PSH packets" | FIN or NULL |

Three variants = flexibility to bypass specific rules.

---

### 3.8 IDLE Scan (Zombie Scan)

**Also called:** Zombie Scan, IP ID Idle Scan · **NMAP:** `sudo nmap -sI [zombie_ip] [target]`

> [!IMPORTANT]
> This is the most complex scan technique — and the **most anonymous**. My IP address NEVER appears in the target's logs. The target only sees traffic from the zombie's IP.

**What is a Zombie Host?** Any internet-connected machine that:
1. Is relatively idle (low traffic)
2. Uses **predictable, incrementing IP ID numbers**
3. Is reachable by both scanner AND target

**What is IP ID?** Every IP packet has a 16-bit IP ID field — most systems increment this counter by 1 for each new packet. By watching these increments from outside, you can COUNT how many packets the zombie sent between your measurements.

---

#### How IDLE Scan Works — Step by Step

**Step 1 — Baseline:** Check zombie's current IP ID

```
Scanner → SYN-ACK to Zombie (no connection exists)
Zombie  → RST back (with IP ID = 5000)
Scanner records: "Zombie's IP ID = 5000"
```

**Step 2 — Probe:** Send forged SYN to target (spoofed as zombie's IP)

| If TARGET PORT is OPEN | If TARGET PORT is CLOSED |
|---|---|
| Target sends SYN-ACK to Zombie | Target sends RST-ACK to Zombie |
| Zombie gets unexpected SYN-ACK → sends RST to target | Zombie gets RST-ACK → does nothing |
| Zombie's IP ID **increments by 1** | Zombie's IP ID **does NOT increment** |

**Step 3 — Measurement:** Check zombie's new IP ID

| IP ID Change | Meaning |
|---|---|
| Incremented by **2** (5000 → 5002) | Zombie sent one packet (RST to target) → **PORT IS OPEN** |
| Incremented by **1** (5000 → 5001) | Zombie sent zero packets → **PORT IS CLOSED/FILTERED** |

---

#### Visual Diagrams

**Open Port:**

```
SCANNER                ZOMBIE (IP ID=5000)         TARGET
  |                          |                         |
  | SYN-ACK to Zombie -----> |                         |
  | <---- RST (IP ID=5000) - |                         |
  | RECORD: IP ID = 5000     |                         |
  |                          |                         |
  | SYN to Target (spoofed)  |  <--- SYN-ACK (open)   |
  |                          | ------ RST -----------> | IP ID → 5001
  |                          |                         |
  | SYN-ACK to Zombie -----> |                         |
  | <---- RST (IP ID=5002) - | (jumped by 2!)          |
  | PORT IS OPEN                                        |
```

**Closed Port:**

```
SCANNER                ZOMBIE (IP ID=5000)         TARGET
  |                          |                         |
  | SYN-ACK to Zombie -----> |                         |
  | <---- RST (IP ID=5000) - |                         |
  |                          |                         |
  | SYN to Target (spoofed)  |  <--- RST-ACK (closed) |
  |                          | (zombie ignores RST-ACK)|
  |                          |                         |
  | SYN-ACK to Zombie -----> |                         |
  | <---- RST (IP ID=5001) - | (incremented by 1 only) |
  | PORT IS CLOSED                                      |
```

| | Detail |
|---|---|
| **Advantages** | ✔ Your IP NEVER appears in target's logs · ✔ Most anonymous scan technique · ✔ Can bypass some firewall rules · ✔ Can identify trust relationships |
| **Limitations** | ✘ Requires finding a suitable zombie (idle + predictable IP ID) · ✘ Modern OS randomizes IP ID → harder in 2026 · ✘ Very SLOW (3 exchanges per port) · ✘ Inaccurate if zombie is not actually idle |
| **Finding zombies in 2026** | Old printers, legacy network devices, some IoT devices. NMAP OS detection can identify potential zombies. |

> [!NOTE]
> **Ethical consideration:** IDLE scan uses an innocent third party as a proxy. Even if the target is authorized, using a zombie WITHOUT the zombie owner's authorization raises legal/ethical questions. Discuss with client in professional engagements.
>
> **Side-channel insight:** The idle scan exploits a *side channel* — information leaked through a secondary system (IP ID counter). The same principle is used in timing attacks on encryption, power analysis on hardware, and Spectre/Meltdown on CPUs.

---

### 3.9 Complete Scan Type Comparison Table

| Scan Type | Packets | Root? | Open | Closed | Filtered | Works on Windows? |
|---|---|---|---|---|---|---|
| **TCP Connect** | SYN→SYN-ACK→ACK | NO | SYN-ACK | RST-ACK | No response | ✅ YES |
| **SYN (Stealth)** | SYN→SYN-ACK→RST | YES | SYN-ACK | RST-ACK | No response | ✅ YES |
| **FIN** | FIN only | YES | No response | RST-ACK | No response | ❌ NO |
| **NULL** | No flags | YES | No response | RST-ACK | No response | ❌ NO |
| **XMAS** | FIN+PSH+URG | YES | No response | RST-ACK | No response | ❌ NO |
| **IDLE (Zombie)** | Spoofed SYN via zombie | YES | IP ID +2 | IP ID +1 | IP ID +1 | ✅ YES |

---

### 3.10 UDP Scanning

**NMAP:** `sudo nmap -sU [target]` · **Combined:** `sudo nmap -sS -sU [target]`

UDP is connectionless — no handshake. Much harder to scan.

| UDP Port State | Response | Certainty |
|---|---|---|
| **Open** | Application may respond (DNS responds to DNS queries) OR says nothing | Ambiguous — no response could mean open OR filtered |
| **Closed** | OS sends ICMP Port Unreachable (Type 3, Code 3) | **Definitive** — port is closed |
| **Filtered** | Firewall drops packet → no ICMP response | Ambiguous |

**Why UDP scanning is SLOW:**
- OS rate-limits ICMP Port Unreachable messages
- Linux default: max 1 ICMP per second
- 65535 ports × 1 second = **18+ hours** to scan all UDP ports
- Solution: Scan only most common ports (top 100 or 1000)

**Important UDP Ports Attackers Target:**

| Port | Service | Attack Potential |
|---|---|---|
| 53 | DNS | Zone transfer, cache poisoning |
| 67 | DHCP | DHCP starvation, rogue DHCP |
| 69 | TFTP | Often unauthenticated file transfer — high risk |
| 161 | SNMP | Community string brute force, info disclosure |
| 500 | IKE | VPN reconnaissance |
| 4500 | IPSec | VPN attacks |

---

## Section 4 — Vulnerability Scanning & Nessus Deep Dive

### 4.1 What is Nessus?

The world's most widely deployed vulnerability scanner. Created by Tenable. First released 1998, now version 10.x.

| Edition | Details |
|---|---|
| **Nessus Essentials** | Free — up to 16 IPs. Sufficient for labs. |
| **Nessus Professional** | Paid — unlimited IPs, compliance checks |
| **Tenable.io** | Cloud-based enterprise version |

**Why Nessus specifically:** Largest plugin library (230,000+ plugins as of 2026). Each plugin tests for ONE specific vulnerability. Industry standard. Comprehensive CVSS scoring and compliance auditing.

---

### 4.2 How Nessus Works Internally — Plugin Architecture

**What is a Nessus Plugin?** A small program (written in NASL — Nessus Attack Scripting Language) that tests for ONE specific vulnerability or configuration issue.

Each plugin has: Unique Plugin ID · CVE IDs it checks · CVSS score · Description · Solution/remediation · Vendor advisory references

#### Nessus Scan Phases

| Phase | What It Does | Output |
|---|---|---|
| **1 — Host Discovery** | Identify alive hosts (ICMP, TCP SYN, UDP, ARP ping) | List of live hosts |
| **2 — Port Scanning** | Scan all/specified ports per host (SYN, TCP connect, UDP) | Open ports per host |
| **3 — Service Detection** | Determine exactly what service is running per port (banner grab, fingerprint) | "Port 80: Apache httpd 2.4.49" |
| **4 — OS Detection** | Determine OS and version (TCP/IP stack fingerprinting, TTL analysis) | "Ubuntu 22.04 LTS" |
| **5 — Plugin Execution** | Load ALL relevant plugins for detected services. Run each test in parallel. | Vulnerability findings |
| **6 — Credentialed Checks** *(optional)* | Log INTO system with provided creds, check from inside. Missing patches, local configs, user issues. | **Much more thorough** |
| **7 — Report Generation** | Compile into organized report: Critical / High / Medium / Low / Info | Prioritized vulnerability report |

---

### 4.3 Nessus Scan Types

| Scan Type | Description |
|---|---|
| **Basic Network Scan** | No credentials. Finds open ports, services, unauthenticated vulns. Good starting point. |
| **Credentialed Scan** | Provides login creds for deep scanning. Finds missing patches, software inventory, local misconfigs. **Most thorough.** |
| **Compliance Audit** | Checks against specific standard: PCI DSS, ISO 27001, CIS Benchmarks, HIPAA. Maps vulns to compliance controls. |
| **Targeted Scan** | Scans for specific CVE IDs. E.g., "Scan only for Log4Shell." Used when specific vuln is suspected. |
| **Web Application Scan** | OWASP Top 10 checks, SQLi, XSS. Less thorough than manual/Burp Suite testing. |

---

### 4.4 Understanding CVSS

**CVSS** (Common Vulnerability Scoring System) — industry-standard method for rating vulnerability severity. Current: v3.1 (v4.0 also in use 2024+). Score: 0.0–10.0.

| Score | Severity |
|---|---|
| 0.0 | None (informational) |
| 0.1–3.9 | Low |
| 4.0–6.9 | Medium |
| 7.0–8.9 | High |
| 9.0–10.0 | **Critical** |

#### CVSS Base Metrics

| Metric | Options | Impact on Score |
|---|---|---|
| **Attack Vector (AV)** | Network (N) · Adjacent (A) · Local (L) · Physical (P) | Network = highest risk |
| **Attack Complexity (AC)** | Low (L) · High (H) | Low = easy to exploit |
| **Privileges Required (PR)** | None (N) · Low (L) · High (H) | None = most dangerous |
| **User Interaction (UI)** | None (N) · Required (R) | None = attacker acts alone |
| **Scope (S)** | Unchanged (U) · Changed (C) | Changed = affects other components |
| **CIA Impact** | None (N) · Low (L) · High (H) for each of C, I, A | High across all = worst |

#### Real Example — CVE-2021-44228 (Log4Shell) — CVSS: 10.0

| Metric | Value | Why |
|---|---|---|
| Attack Vector | Network (N) | Remotely exploitable |
| Attack Complexity | Low (L) | Just send a crafted string |
| Privileges Required | None (N) | No auth needed |
| User Interaction | None (N) | Victim doesn't need to do anything |
| Scope | Changed (C) | Affects more than just the vulnerable system |
| CIA Impact | High / High / High | Complete loss of all three |

**Every metric at its worst possible value.** This is why Log4Shell caused global panic in December 2021.

#### Reading a Nessus Finding

```
Plugin ID  : 155999
Severity   : CRITICAL
CVE        : CVE-2021-44228
CVSS v3.1  : 10.0
Description: Apache Log4j2 2.0-beta9 through 2.14.1 — JNDI endpoint vulnerability
Solution   : Upgrade to Log4j 2.15.0 or later
```

**How to use this:** Note CVE ID → look up in NVD · Note CVSS score → prioritize 9.0+ first · Read solution → plan remediation · Check "Plugin Output" → shows evidence from your system

---

### 4.5 Credentialed vs Uncredentialed Scanning

| | Uncredentialed (External) | Credentialed (Authenticated) |
|---|---|---|
| **Approach** | Outsider — no login | Logs INTO the system |
| **Finds** | Open ports, service versions, unauthenticated vulns, default creds, exposed interfaces | **EVERYTHING** — including missing OS patches, software vulns, local misconfigs, user permission issues |
| **Misses** | Installed patches, local user config, internal services, patch levels | Very little |
| **Findings** | Baseline | **300–500% MORE** than uncredentialed |
| **Analogy** | Inspector checking outside of building — only sees what's visible from the street | Inspector with a key — walks through every room |

**Credentials to provide:**

| System | Credential |
|---|---|
| Linux/Mac | SSH username + password OR SSH private key |
| Windows | Domain/local admin username + password |
| Database | Database admin credentials |
| Web App | Application admin credentials |

> [!TIP]
> **ALWAYS use credentialed scanning when possible.** Uncredentialed = external attacker perspective. Credentialed = insider/post-exploitation perspective. Combined = complete picture.

---

## Section 5 — Burp Suite

### 5.1 What is Burp Suite?

A comprehensive web application security testing platform by PortSwigger. At its core: an **intercepting proxy** that sits between browser and web server, allowing inspection, modification, and replay of every HTTP/HTTPS request and response.

| Edition | Details |
|---|---|
| **Community** | Free — covers fundamentals (use for labs) |
| **Professional** | $449/year — adds automation, scanner |
| **Enterprise** | Automated scanning at scale for organizations |

**Why Burp matters:** Web apps are the #1 attack surface in 2026 (43% of breaches per Verizon DBIR 2025). Burp is the industry standard — required for OSCP, CEH, eWPT, BSCP certifications.

---

### 5.2 How HTTP Proxy Interception Works

**Without Proxy:**
```
Browser → HTTPS Request → Internet → Web Server
Browser ← HTTPS Response ← Internet ← Web Server
(You see: just the rendered webpage)
```

**With Burp Suite as Proxy:**
```
Browser → HTTPS Request → BURP SUITE → Internet → Web Server
Browser ← HTTPS Response ← BURP SUITE ← Internet ← Web Server
```

Burp is now IN THE MIDDLE. It sees EVERYTHING. With intercept ON, it can:
- **READ** the full request before it's sent
- **MODIFY** any field (headers, parameters, cookies, body)
- **FORWARD** it to server (send modified request)
- **DROP** it (block the request entirely)
- **STORE** complete history of every request and response

> [!NOTE]
> This is a legitimate MITM. The difference from malicious MITM: you OWN the browser, you OWN the testing environment, you HAVE authorization. Malicious MITM intercepts others' traffic without consent. Burp intercepts YOUR OWN traffic.

---

### 5.3 How Burp Handles HTTPS

**The Problem:** Web traffic is encrypted with SSL/TLS. How can Burp read it?

**The Solution — SSL Bumping / TLS Interception:**

| Step | What Happens |
|---|---|
| 1 | Browser connects to Burp's proxy port (127.0.0.1:8080) |
| 2 | Browser requests HTTPS to target.com |
| 3 | Burp creates a **FAKE CERTIFICATE** for target.com (signed by Burp's own CA) |
| 4 | Browser receives Burp's fake cert instead of real target cert |
| 5 | Browser establishes SSL with BURP (not with target) |
| 6 | Burp establishes REAL SSL with target.com |
| 7 | Burp decrypts browser's traffic → reads/modifies → re-encrypts → sends to target |

**Result:**
```
Browser ←[SSL with Burp cert]→ BURP ←[SSL with real cert]→ Server
Burp can READ AND MODIFY all HTTPS traffic in plaintext.
```

**Why doesn't the browser reject the fake cert?** Normally it would. You must **install Burp's CA certificate** into your browser/OS as a trusted root certificate. Then the browser trusts Burp's generated certificates.

> [!TIP]
> This is EXACTLY how corporate web filtering/monitoring works. Your company's proxy does the same SSL interception. Understanding Burp helps you understand corporate monitoring.

---

### 5.4 Burp Suite Tools

| Tool | What It Does | Key Use |
|---|---|---|
| **Proxy** | Core interception engine. Captures all HTTP/HTTPS traffic. Intercept ON = hold each request for inspect/modify. OFF = pass through (records in history). | Foundation for all other tools |
| **HTTP History / Site Map** | Complete log of ALL requests/responses seen by Burp. Builds a site map as you browse. | Complete attack surface map |
| **Scanner** *(Pro only)* | Automated web app vuln scanner. Sends crafted payloads to all discovered parameters. Detects SQLi, XSS, path traversal, etc. | Saves time on large apps. Misses logic flaws. |
| **Intruder** | Automated, customizable attack tool. Mark positions (params to attack), send payloads (wordlists, patterns) systematically. | Password brute force, username enumeration, fuzzing. Community version is rate-limited. |
| **Repeater** | Manually replay and modify individual HTTP requests. Send → modify → send → see response. | **Most important tool for manual testing.** Test hypotheses: "What if I change this parameter?" |
| **Decoder** | Encode/decode data: URL encoding, Base64, HTML entities, Hex, ASCII, etc. | Understanding encoded values for attacks and bypasses |
| **Comparer** | Visually compare two items (requests or responses). Highlights differences. | "Is the response different when logged in vs not?" |
| **Sequencer** | Analyzes randomness of session tokens. Collects many tokens → statistical analysis. | Predictable tokens = session hijacking risk |

---

### 5.5 Spidering / Crawling

Automatically discovering ALL pages, endpoints, and functionality of a web application by following links and analyzing content systematically.

**Why:** Can't test functionality I don't know exists. Large apps have hundreds/thousands of pages.

#### Two Methods in Burp

| Method | How | Advantage | Limitation |
|---|---|---|---|
| **Passive Discovery** (HTTP History) | Browse app normally while Burp proxy is active. Every page visited is captured. | Very accurate — you control what's included | Only discovers pages you actually visit |
| **Active Crawl** *(Burp Pro)* | Burp automatically follows links and submits forms | More comprehensive discovery | May trigger rate limits, spam forms, send unintended requests. **Always check scope.** |

**What Spidering Discovers:**
- All pages and URLs (GET endpoints)
- Form submission endpoints (POST)
- URL parameters (GET and POST)
- Hidden pages not in main navigation
- API endpoints referenced in JavaScript
- HTML comments revealing dev info
- Input fields and their names (attack targets)
- File upload endpoints, auth endpoints, admin interfaces, error pages

---

### 5.6 Attack Surface Mapping

Systematic identification of ALL potential entry points into an application.

#### Web Application Attack Surface — 5 Categories

**Category 1 — Input Vectors (where data enters):**
- URL parameters (`?id=1`, `?search=term`)
- Form fields (login, search, registration, contact)
- HTTP headers (User-Agent, Referer, X-Forwarded-For, Cookie)
- JSON/XML request bodies (API endpoints)
- File upload, WebSocket messages, GraphQL queries

**Category 2 — Authentication Surfaces:**
- Login pages (brute force, injection)
- Password reset flows (token generation, email enumeration)
- Session management (token predictability, fixation)
- OAuth flows (redirect_uri manipulation, state bypass)
- API auth (JWT, API keys, Bearer tokens), MFA bypass

**Category 3 — Authorization Surfaces:**
- Object references in URLs (`/user/123/profile` → try `/user/124/profile`)
- Role-based access (does regular user reach admin functions?)
- Function-level access control (API endpoints without auth check)
- Horizontal privilege escalation

**Category 4 — Third-Party Integrations:**
- Payment processors, SSO/SAML, external API calls (SSRF potential), CDN layers, third-party JS libraries

**Category 5 — Client-Side Attack Surface:**
- JavaScript source code (may contain API keys, endpoints)
- DOM manipulation (DOM XSS sources and sinks)
- Browser storage (localStorage, sessionStorage, cookies)
- HTML comments, hidden form fields

#### How Professionals Use the Site Map

| Step | Action |
|---|---|
| 1 | Browse entire app as normal user |
| 2 | Review Site Map for complete coverage |
| 3 | Sort by Parameter Count → high param count = most attack surface |
| 4 | Sort by File Extension → find .php, .asp, .aspx pages |
| 5 | Look for /admin/, /backup/, /api/, /debug/, /test/ directories |
| 6 | Review JavaScript files → often contain undocumented API endpoints |
| 7 | Right-click interesting endpoints → Send to Intruder/Repeater |
| 8 | Begin systematic testing |

> [!TIP]
> **Free resource:** PortSwigger's [Web Security Academy](https://portswigger.net/web-security) is the BEST free resource for web app security. Includes browser-based labs. Used by OSCP, BSCP, and CEH candidates worldwide.

---

## Section 6 — MITRE ATT&CK Mapping — Scanning Phase

| Tactic | ID | Use |
|---|---|---|
| **TA0043** — Reconnaissance | Pre-attack scanning | |
| **TA0007** — Discovery | Post-access internal scanning | |

| Tech ID | Technique | What It Maps To | Tool |
|---|---|---|---|
| T1595.001 | Active Scanning: IP Blocks | Network scanning for live hosts | NMAP `-sn` |
| T1595.002 | Active Scanning: Vulnerability Scanning | Running Nessus/OpenVAS against hosts | Nessus, OpenVAS |
| T1595.003 | Active Scanning: Wordlist Scanning | Port scanning with various TCP techniques | NMAP `-sS`, `-sF`, `-sX` etc. |
| T1046 | Network Service Discovery | Identifying services on open ports (post-access internal) | NMAP `-sV` |
| T1592.002 | Gather Victim Host Info: Software | Service version detection during external scanning | NMAP `-sV`, Shodan, Netcraft |
| T1190 | Exploit Public-Facing Application | Using vuln scan results to exploit CVEs (Phase 3 — but scanning enables it) | — |

**Defender use:** When SIEM alerts on a pattern matching T1595.001 → "This is network scanning in progress." Check if it's an authorized scan → if not, block and investigate immediately.

---

## Section 7 — 2026 Context

### 7.1 AI-Assisted Scanning

| Capability | Traditional | AI-Powered | Tools |
|---|---|---|---|
| **Vulnerability Prioritization** | Nessus gives 500 findings — where to start? | ML analyzes your environment, attack paths, asset criticality to rank findings | Tenable.io AI Exposure Score, Qualys TruRisk |
| **Attack Path Analysis** | Manually chain vulns to see attack paths | Auto-chain: "Vuln A + Vuln B = Path to Crown Jewels" | XM Cyber, Skybox, Tenable Attack Path |
| **LLM-Assisted Recon** | Manually run NMAP → analyze output | LLM analyzes output and suggests attack paths, relevant CVEs | AI-integrated NMAP wrappers |
| **Predictive Scanning** | Scan everything equally | AI predicts which systems are LIKELY vulnerable — focuses resources | — |
| **Smart Fuzzing** | Wordlist-based | AI-generated test cases based on app purpose and input context | — |

---

### 7.2 Cloud Scanning Challenges

| Challenge | Why It's Different |
|---|---|
| **Cloud Provider Policies** | AWS, Azure, GCP all have scanning policies. AWS requires prior approval. Scanning without approval = potential account suspension. |
| **Shared Infrastructure** | Cloud instances may share physical hardware. Aggressive scanning could affect OTHER customers. |
| **Serverless Functions** | Lambda, Azure Functions have NO persistent IP. Traditional port scanning won't find them. Need application-level discovery. |
| **Auto-Scaling** | Target might have 5 servers during scan but 50 under load. Results may not reflect full attack surface. |
| **CDN Masking** | Most cloud sites sit behind CloudFront/CloudFlare. Scanning CDN IP ≠ scanning actual app server. Must find origin IP. |

**Cloud-Specific Tools (2026):**

| Tool | Purpose |
|---|---|
| ScoutSuite | Multi-cloud security auditing |
| Pacu | AWS exploitation framework |
| Prowler | AWS/Azure/GCP security assessment |
| CloudSploit | Cloud misconfig scanner |
| CNAPP tools | Cloud-Native Application Protection Platforms |

---

### 7.3 Evasion Techniques

Understanding evasion = understanding detection. Red team engagements test whether detection works.

| Technique | How It Works | NMAP Flag |
|---|---|---|
| **Slow Scan (Timing)** | One probe per 5 minutes instead of 1000/second | `-T0` (Paranoid) or `-T1` (Sneaky) |
| **Fragmented Packets** | Split TCP packets into tiny fragments — too small for IDS signatures | `-f` |
| **Decoy Scanning** | Send packets appearing from MULTIPLE fake source IPs. Analyst must find the real one. | `-D RND:10` (10 random decoys) |
| **IDLE/Zombie Scan** | Your IP never appears in logs (Section 3.8) | `-sI [zombie]` |
| **Source Port Manipulation** | Firewalls may allow port 53 (DNS) or 80 (HTTP). Craft packets from those. | `--source-port 53` |
| **Randomized Port Order** | Sequential scanning is easy to detect. Random order disrupts IDS patterns. | `--randomize-hosts` |
| **Bandwidth Throttling** | Limit speed to blend with normal background traffic | `--max-rate 10` |

**How Blue Team detects evasion attempts (even slow scans):**
- NetFlow data — traffic analysis over longer periods
- Firewall logs — accumulated connection attempts
- UEBA tools — behavioral anomaly detection
- Modern SIEM with ML — correlate port probes over 24–48hr windows, baseline analysis, Geo-IP analysis

---

### ✅ Session 10B — Key Takeaways

- [x] Three distinct scanning types: Network Scan → who is alive · Port Scan → what's open · Vulnerability Scan → what's broken
- [x] TCP Three-Way Handshake (SYN → SYN-ACK → ACK) is the foundation — every TCP scan is a modification of this
- [x] SYN scan interrupts handshake BEFORE completion → no OS log
- [x] TCP Connect scan completes handshake → OS AND app log created
- [x] FIN, NULL, XMAS scans exploit RFC 793 — work on Linux, NOT Windows
- [x] IDLE scan is the most anonymous — my IP NEVER reaches the target
- [x] Open port on FIN/NULL/XMAS = NO RESPONSE (counterintuitive but critical)
- [x] Closed port on FIN/NULL/XMAS = RST-ACK response
- [x] UDP scanning is slow due to ICMP rate limiting — scan only common ports
- [x] Nessus works via 230,000+ plugins, each testing ONE specific vulnerability
- [x] Credentialed scans find 3–5x more vulnerabilities than uncredentialed
- [x] CVSS 9.0–10.0 = Critical → always remediate first
- [x] Log4Shell (CVE-2021-44228) had CVSS 10.0 — perfect storm of risk factors
- [x] Burp Suite is an intercepting proxy — sits between browser and server
- [x] Burp handles HTTPS via SSL bumping — requires installing its CA cert
- [x] Spidering builds the complete attack surface map before testing
- [x] Attack surface = ALL entry points: input vectors, auth flows, authorization boundaries, third-party integrations, client-side code
- [x] AI is transforming scanning: prioritization, attack path analysis, predictive identification
- [x] Cloud scanning requires provider approval — different rules apply

---

<details>
<summary>📖 Session 10B — Glossary</summary>

| Term | Definition |
|---|---|
| Network Scanning | Identifying which hosts are alive in a network range |
| Port Scanning | Identifying which ports are open on a live host |
| Vulnerability Scanning | Finding known CVEs in identified services/software |
| TCP Handshake | SYN → SYN-ACK → ACK connection establishment process |
| SYN Flag | Synchronize — initiates TCP connection |
| ACK Flag | Acknowledge — confirms receipt of previous packet |
| FIN Flag | Finish — signals end of data transmission |
| RST Flag | Reset — abruptly terminates connection |
| PSH Flag | Push — send data immediately without buffering |
| URG Flag | Urgent — marks data as high priority |
| Port State Open | A service is actively listening on this port |
| Port State Closed | No service listening — host reachable — RST response |
| Port State Filtered | Firewall blocking — cannot determine open/closed |
| TCP Connect Scan | Full handshake scan — noisy — no root needed |
| SYN Scan | Half-open scan — interrupts handshake — root needed |
| FIN Scan | Sends FIN only — exploits RFC 793 — Linux only |
| NULL Scan | No flags set — exploits RFC 793 — Linux only |
| XMAS Scan | FIN+PSH+URG flags — "lit-up" packet — Linux only |
| IDLE/Zombie Scan | Most anonymous scan — spoofs zombie IP — uses IP ID |
| IP ID | 16-bit counter in IP header — increments per packet |
| RFC 793 | The TCP specification — defines protocol behavior |
| CVSS | Common Vulnerability Scoring System (0–10 scale) |
| CVE | Common Vulnerabilities and Exposures — vuln identifier |
| NVD | National Vulnerability Database — official CVE database |
| Nessus Plugin | Individual test program for one specific vulnerability |
| Credentialed Scan | Vulnerability scan with login credentials — more thorough |
| Burp Suite | Web application security testing platform/proxy |
| Intercepting Proxy | Sits between browser and server — sees all traffic |
| SSL Bumping | Burp's method for decrypting HTTPS traffic |
| Burp CA Certificate | Burp's root cert — must be installed for HTTPS intercept |
| Spidering/Crawling | Automated discovery of all pages and endpoints |
| Site Map | Burp's visual representation of discovered application |
| Attack Surface | All possible entry points into a system or application |
| Intruder | Burp tool for automated, customizable attacks |
| Repeater | Burp tool for manually replaying and modifying requests |
| Sequencer | Burp tool for analyzing session token randomness |
| Decoy Scanning | Sending scans from multiple fake source IPs |
| T0–T5 Timing | NMAP timing templates — T0=slowest, T5=fastest |
| `-Pn` Flag | NMAP flag — skip host discovery, treat host as alive |
| UDP Scan | Port scan for UDP services — slower than TCP scanning |
| ICMP Rate Limiting | OS limits ICMP responses (~1/sec) — slows UDP scan |
| Banner Grabbing | Reading service banner to identify software and version |

</details>

---

**What's next — Session 11A** covers TCP flag deep dive, banner grabbing, OS fingerprinting, proxy servers in attacks, and HTTP tunneling techniques.

---