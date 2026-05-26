# 🔬 Cybersecurity Study Notes — Session 11A

Personal notes I'm maintaining while studying ethical hacking and cybersecurity concepts.
This session covers TCP flag mechanics in depth, banner grabbing, OS fingerprinting, proxy servers in attacks, and HTTP tunneling techniques.

> [!NOTE]
> Session 11A is the bridge between "scanning" and "knowing what you found." Session 10B taught HOW to send scans. Session 11A explains WHY those scans produce those responses — then uses that knowledge for banner grabbing, OS fingerprinting, and hiding activity through proxies and tunnels.

---

## 📚 Table of Contents

- [Where This Session Fits](#-where-this-session-fits)
- [Foundation Knowledge — TCP Header & Flags](#-foundation-knowledge)
- [Things to Remember](#things-to-remember)
- [Section 1 — TCP Communication Flag Types (Deep Dive)](#section-1--tcp-communication-flag-types--deep-dive)
  - [Why TCP Flags Matter](#11-why-tcp-flags-matter)
  - [The Six Core TCP Flags — Complete Reference](#12-the-six-core-tcp-flags)
  - [Flag Combinations — Scan Types Revisited](#13-flag-combinations--scan-types-revisited)
  - [The Three-Way Handshake — Complete State Machine](#14-the-three-way-handshake--complete-state-machine)
  - [TCP Connection Termination — Four-Way Handshake](#15-tcp-connection-termination)
- [Section 2 — Banner Grabbing](#section-2--banner-grabbing)
  - [What is Banner Grabbing?](#21-what-is-banner-grabbing)
  - [Active Banner Grabbing](#22-active-banner-grabbing)
  - [Passive Banner Grabbing](#23-passive-banner-grabbing)
  - [Banner → CVE Mapping (The Attack Chain)](#24-banner--cve-mapping)
  - [Banner Manipulation — Defender Strategy](#25-banner-manipulation--defender-strategy)
- [Section 3 — OS Fingerprinting](#section-3--os-fingerprinting)
  - [What is OS Fingerprinting?](#31-what-is-os-fingerprinting)
  - [Active OS Fingerprinting](#32-active-os-fingerprinting)
  - [Passive OS Fingerprinting](#33-passive-os-fingerprinting)
- [Section 4 — Proxy Servers in Attacks](#section-4--proxy-servers-in-attacks)
  - [Why Attackers Use Proxies](#41-why-attackers-use-proxies)
  - [Types of Proxies](#42-types-of-proxies)
  - [Proxy Chaining](#43-proxy-chaining)
  - [Burp Suite as Intercept Proxy](#44-burp-suite-as-intercept-proxy)
- [Section 5 — HTTP Tunneling Techniques](#section-5--http-tunneling-techniques)
  - [What is HTTP Tunneling?](#51-what-is-http-tunneling)
  - [Technical Mechanics](#52-how-http-tunneling-works)
  - [Attack Scenarios](#53-attack-scenarios)
  - [Detecting HTTP Tunneling — DPI](#54-detecting-http-tunneling--deep-packet-inspection)
- [Section 6 — MITRE ATT&CK Mapping](#section-6--mitre-attck-mapping)
- [Section 7 — 2026 Context](#section-7--2026-context)
  - [AI-Assisted Scanning & Fingerprinting](#71-ai-assisted-scanning-and-fingerprinting)
  - [HTTP Tunneling & Proxy Evolution](#72-http-tunneling-and-proxy-evolution)
- [Key Takeaways](#-session-11a--key-takeaways)
- [Glossary](#-session-11a--glossary)

---

## 🗺️ Where This Session Fits

```
  SESSIONS 6-9         SESSION 10           SESSIONS 11-12    SESSIONS 13+
  [FOUNDATIONS]    →   [RECON &        →    [ACTIVE PROBING  → [EXPLOITATION
  Ethics, Laws,        SCANNING]            & ENUMERATION]     & POST-EXPLOIT]
  Hacker Types,        OSINT, WHOIS,        ← YOU ARE HERE
  Attack Phases        NMAP, Nessus,        TCP Flags,
                       Burp Suite           Banner Grab,
                                            OS Fingerprint,
                                            Proxies, Tunnels
```

Within Phase 2–3 — Enumeration:

| Step | Topic | Where |
|---|---|---|
| 1 | TCP flag mechanics that make scanning possible | **11A Section 1** |
| 2 | Banner Grabbing — extract service/version info | **11A Section 2** |
| 3 | OS Fingerprinting — identify target's OS | **11A Section 3** |
| 4 | Proxies — hide identity while enumerating | **11A Section 4** |
| 5 | HTTP Tunneling — bypass firewalls during enumeration | **11A Section 5** |
| 6 | IP Spoofing, NetBIOS, SNMP, LDAP, DNS Enumeration | Session 11B |

---

## 📌 Foundation Knowledge

<details>
<summary>🔧 The TCP Header — Control Flags Field</summary>

Every TCP packet carries a header with a 6-bit **control flags** field (code bits). These six bits are what Session 11A is built around.

**The six original flags (in order):**

| Position | Flag | Full Name | One-Line Purpose |
|---|---|---|---|
| Bit 1 | **URG** | Urgent | Prioritize this data — process immediately |
| Bit 2 | **ACK** | Acknowledgement | "I received your last packet" |
| Bit 3 | **PSH** | Push | Don't buffer — send to application layer now |
| Bit 4 | **RST** | Reset | Abort this connection immediately |
| Bit 5 | **SYN** | Synchronize | Initiate a new connection |
| Bit 6 | **FIN** | Finish | I am done sending data — close connection |

**Modern TCP additional flags:**

| Flag | Purpose |
|---|---|
| CWR | Congestion Window Reduced — signals network congestion |
| ECE | ECN Echo — Explicit Congestion Notification |

**Key references:** RFC 793 (original TCP spec, 1981) · RFC 3168 (ECN additions, 2001)

**Port number ranges:**

| Range | Type |
|---|---|
| 0–1023 | Well-Known Ports (assigned by IANA) |
| 1024–49151 | Registered Ports (applications register these) |
| 49152–65535 | Dynamic/Ephemeral Ports (temporary client ports) |

</details>

---

## Things to Remember

| Misconception | Reality |
|---|---|
| "I ran SYN scans in 10B. I already know TCP flags." | 10B showed WHICH flags to set. 11A explains WHY those flags produce those responses — the full TCP state machine, RST behavior, half-open connections, and what happens at each stage. |
| "Banner grabbing just reads a welcome message" | Banners reveal software name, exact version, and sometimes OS. One banner → one CVE → full compromise is not uncommon. |
| "OS fingerprinting requires special expensive tools" | NMAP (-O flag) is free and uses 5,700+ OS fingerprints. Netcat ships with every Linux distro. |
| "If I use a proxy, I'm completely anonymous" | Most proxies maintain logs. One subpoena reveals the original IP. Even multi-hop chains can be correlated through timing attacks. |
| "HTTP tunneling is only used by attackers" | Corporate VPNs, ngrok, Cloudflare Tunnel, and reverse SSH over HTTP all use the same principles. The technique is neutral; the use determines legality. |
| "Active and passive OS fingerprinting achieve the same thing" | Active SENDS crafted packets (detectable). Passive OBSERVES existing traffic (invisible to IDS/IPS). |
| "Banner grabbing only works on web servers (port 80)" | Almost every service broadcasts a banner: FTP (21), SSH (22), SMTP (25), POP3 (110), IMAP (143), Telnet (23), RDP (3389). |

---

## Section 1 — TCP Communication Flag Types — Deep Dive

### 1.1 Why TCP Flags Matter

TCP flags are single-bit fields in the TCP header's control section. Each flag is either SET (1) or NOT SET (0). The combination of flags defines the **meaning and purpose** of that packet within a TCP connection.

**Why it matters to ethical hackers:**

RFC 793 defines what a host SHOULD do when it receives each flag combination. But different operating systems handle **undefined combinations** differently. These behavioral differences are the foundation of:
- OS fingerprinting (passive + active)
- Stealth scanning (FIN, NULL, XMAS scans)
- Firewall evasion
- Session hijacking

---

### 1.2 The Six Core TCP Flags

For every flag I need to understand: What does it mean when set? What does the receiver do? When is it legitimately set? How does an attacker abuse it?

---

#### 🔵 FLAG 1: SYN — Synchronize

| Aspect | Detail |
|---|---|
| **Meaning** | "I want to start a new TCP connection. Here is my Initial Sequence Number (ISN)." |
| **Receiver action (port OPEN)** | Replies with SYN+ACK, allocates resources, assigns its own ISN |
| **Receiver action (port CLOSED)** | Replies with RST+ACK |
| **Receiver action (FILTERED)** | No response (firewall drops silently) |
| **Legitimate use** | First packet of every TCP connection — every web page, SSH session, DB connection |
| **Attacker abuse — SYN Scan** | Send SYN → receive SYN+ACK → send RST before completing handshake → never logged by application layer |
| **Attacker abuse — SYN Flood** | Thousands of SYN packets with spoofed source IPs → target's connection table exhausted → legitimate users can't connect |

> [!NOTE]
> **Resource implication:** Every received SYN causes the target to allocate a Transmission Control Block (TCB) entry — ~280 bytes of kernel memory. At 100,000 SYN/sec, that's ~28MB/sec of kernel memory consumption. This is why SYN flooding works.

---

#### 🟢 FLAG 2: ACK — Acknowledgement

| Aspect | Detail |
|---|---|
| **Meaning** | "The acknowledgment number field is valid. I confirm receipt of all data up to sequence number X." |
| **Receiver action** | Almost always set in established connections. Bare ACK to port with no connection → Linux sends RST |
| **Legitimate use** | Second and third packets of handshake. Every data acknowledgement in established sessions. |
| **Attacker abuse — ACK Scan** | Send bare ACK packets to probe **firewall rules** (not port state). RST back = UNFILTERED (reachable through firewall). No response = FILTERED. ACK scan reveals firewall rules, not whether ports are open/closed. |

> [!TIP]
> Some stateless firewalls PASS ACK packets through because they assume it's "established traffic." This is why stateful firewalls are critical.

---

#### 🔴 FLAG 3: FIN — Finish

| Aspect | Detail |
|---|---|
| **Meaning** | "I have finished sending data. Initiating graceful connection close." |
| **On ESTABLISHED connection** | Sends FIN+ACK → begins four-way termination |
| **FIN on CLOSED port (RFC 793)** | Send RST |
| **FIN on OPEN port (RFC 793)** | Drop silently — port has no connection for this FIN |
| **Legitimate use** | Graceful connection termination |
| **Attacker abuse — FIN Scan** | FIN to CLOSED → RST (port is closed). FIN to OPEN → silence (port is open). Bypasses some firewalls that only inspect SYN packets. |

> [!WARNING]
> **Windows exception:** Windows sends RST for FIN to BOTH open AND closed ports. FIN scans are unreliable against Windows — but this behavior itself is an OS fingerprinting indicator.

---

#### ⚫ FLAG 4: RST — Reset

| Aspect | Detail |
|---|---|
| **Meaning** | "This connection is being immediately aborted. Discard all queued data. No response needed." |
| **Receiver action** | Immediately terminates connection state. Releases all resources. Does NOT send any ACK back. |
| **Legitimate use** | Connection refused (port not listening), application crash, firewall rejection, keepalive failure |
| **Attacker abuse — RST Injection** | If attacker can predict the sequence number of an established TCP session → forge RST packet → target terminates what it believes is a legitimate connection → knocks users offline |
| **In scanning** | RST responses confirm port is CLOSED and host is ALIVE. Absence of RST after FIN/NULL/XMAS → port is open. |

---

#### 🟡 FLAG 5: PSH — Push

| Aspect | Detail |
|---|---|
| **Meaning** | "Don't buffer — send immediately to the application layer." |
| **Receiver action** | Passes data directly to application without waiting for buffer to fill |
| **Legitimate use** | Interactive apps (SSH, Telnet, RDP) where each keystroke needs immediate delivery |
| **Attacker abuse** | PSH+ACK is common in C2 traffic — ensures commands sent through backdoors are immediately processed. Unusual PSH patterns on non-interactive ports can indicate injected traffic or protocol tunneling. |

---

#### 🟠 FLAG 6: URG — Urgent

| Aspect | Detail |
|---|---|
| **Meaning** | "The Urgent Pointer field is valid. Data at that offset must be processed immediately, out of order." |
| **Receiver action** | Delivers urgent data to application immediately, bypassing normal queue |
| **Legitimate use** | Telnet Ctrl+C (interrupt signal). Out-of-band control signals in legacy protocols. Rarely used in modern networking. |
| **Attacker abuse** | Part of XMAS scan (URG+PSH+FIN). Some IDS systems mishandle the urgent pointer and skip payload inspection — used for evasion. |

---

### 1.3 Flag Combinations — Scan Types Revisited

Now I understand WHY each scan produces its responses:

| SYN | ACK | FIN | RST | PSH | URG | Scan Type | Why This Combination |
|---|---|---|---|---|---|---|---|
| 1 | 0 | 0 | 0 | 0 | 0 | **SYN Scan** | Initiates handshake; RST=closed, SYN+ACK=open |
| 0 | 0 | 1 | 0 | 0 | 0 | **FIN Scan** | No open connection flag; RST=closed, silence=open |
| 0 | 0 | 0 | 0 | 0 | 0 | **NULL Scan** | Zero flags — undefined per RFC 793; RST=closed, silence=open |
| 0 | 0 | 1 | 0 | 1 | 1 | **XMAS Scan** | FIN+PSH+URG all set; undefined combo; RST=closed, silence=open |
| 1 | 1 | 0 | 0 | 0 | 0 | **SYN+ACK** (sent by attacker) | Appears to be response to existing conn; bypasses stateless firewalls |
| 0 | 1 | 0 | 0 | 0 | 0 | **ACK Scan** | Maps firewall rules; RST=unfiltered, silence=filtered |

---

### 1.4 The Three-Way Handshake — Complete State Machine

```
CLIENT (initiator)                    SERVER (port OPEN)
     |                                      |
     |--- SYN (seq=1000) ----------------->|
     |    "I want to connect.               |
     |     My seq number is 1000"           |
     |                                      | (allocates TCB, selects ISN=5000)
     |<-- SYN+ACK (seq=5000, ack=1001) ----|
     |    "OK. My seq is 5000.              |
     |     I expect 1001 next from you"     |
     |                                      |
     |--- ACK (seq=1001, ack=5001) -------->|
     |    "Connection ESTABLISHED."          |
     |                                      |
     |====== DATA TRANSFER BEGINS ==========|
```

**Connection Refused (port CLOSED):**

```
CLIENT                                SERVER (port CLOSED)
     |--- SYN (seq=1000) ----------------->|
     |<-- RST+ACK -------------------------|
     |    "Nothing listening. Refused."      |
```

**Filtered Port (firewall drops):**

```
CLIENT                                FIREWALL
     |--- SYN (seq=1000) ----------------->|
     |                        [silently dropped]
     |    [timeout — no response]           |
```

**The Half-Open Connection (SYN Scan Mechanism):**

```
SCANNER                               TARGET (port OPEN)
     |--- SYN --------------------------->  |
     |<-- SYN+ACK ----------------------- |
     |--- RST --------------------------->  |  ← kills half-open connection
     |                                      |    (never fully established)
     |                                      |    (app layer NEVER logs this)
```

**Why it works:** Application-level logs (Apache, IIS, nginx) only log COMPLETED connections. SYN scans stay below application radar. Kernel-level IDS (Snort, Suricata) CAN detect SYN scan patterns.

---

#### Defender Actions for TCP Flag Attacks

| Action | How |
|---|---|
| Deploy **stateful firewalls** | Track TCP state → reject ACK packets with no matching SYN entry |
| Snort/Suricata rules | Detect NULL scans, XMAS scans, SYN floods, RST injection |
| Enable TCP SYN cookies | `sysctl -w net.ipv4.tcp_syncookies=1` on Linux — mitigates SYN flooding |
| Rate limit SYN packets | At perimeter firewall or load balancer |
| SIEM correlation | Alert on >500 unique destination ports probed from one source in 60 seconds |

---

### 1.5 TCP Connection Termination

**Four-Way FIN Handshake:**

```
CLIENT (done sending)                 SERVER
     |--- FIN+ACK ---------------------->   | Client done sending.
     |<-- ACK -----------------------------|  Server acknowledges.
     |                                      | (Server may still send data)
     |<-- FIN+ACK -------------------------|  Server done sending.
     |--- ACK --------------------------->   | Client acknowledges.
     CONNECTION FULLY CLOSED
```

**Why termination matters for scanning:**
- RST terminates IMMEDIATELY (no four-way handshake)
- FIN terminates GRACEFULLY
- Attackers send RST mid-session to: abort connections during SYN scans, inject RST to disrupt legitimate sessions, clean up half-open connections during mass scanning

---

## Section 2 — Banner Grabbing

### 2.1 What is Banner Grabbing?

Connecting to a service on an open port and reading the identification string (banner) the service sends **before any authentication occurs**.

A banner typically contains:
- **Service name** — Apache, OpenSSH, Microsoft IIS, vsftpd
- **Software version** — Apache/2.4.41, OpenSSH_7.4
- **Operating system** — Ubuntu 18.04 LTS, Win32
- **Protocol version** — SSH-2.0, HTTP/1.1
- Sometimes: admin contact, hostname, build date

**Why it matters:** Without version info, I can't look up known CVEs for that exact version. Banner grabbing converts an IP + open port into actionable intelligence. A single CVE lookup can reveal a path to full compromise.

Services send banners because:
- Protocol specs require it (FTP RFC 959, SMTP RFC 5321 mandate 220 greeting)
- Software vendors include it by default for troubleshooting
- Admins don't bother removing it

---

### 2.2 Active Banner Grabbing

Initiating a connection to the target service and reading the response. Generates detectable traffic.

#### Tool: Netcat

```bash
nc -vn [target_IP] [port]
# -v = verbose  -n = no DNS resolution (faster)
```

#### Common Ports and Typical Banners

| Port | Service | Typical Banner | Reveals |
|---|---|---|---|
| 21 | FTP | `220 (vsFTPd 3.0.3)` | FTP server type and version |
| 22 | SSH | `SSH-2.0-OpenSSH_7.4` | SSH protocol + software version |
| 25 | SMTP | `220 mail.example.com ESMTP Postfix 3.5.13` | Mail server software, version, hostname |
| 80 | HTTP | `Server: Apache/2.4.41 (Ubuntu)` | Web server, version, OS |
| 110 | POP3 | `+OK Dovecot ready` | Mail server software |
| 143 | IMAP | `* OK [CAPABILITY IMAP4rev1] Dovecot ready` | IMAP server with capability list |

#### Tool: Telnet (for HTTP banner)

```bash
telnet [target_IP] 80
HEAD / HTTP/1.0
# Press Enter twice — returns Server: header without page content
```

#### Tool: NMAP Service Version Detection

```bash
nmap -sV -p 21,22,25,80 [target_IP]
# -sV = Service version detection (10,000+ service fingerprints)
# --version-intensity 0 (lightest) to 9 (most aggressive)
```

**Example output:**

```
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
22/tcp open  ssh     OpenSSH 7.4 (protocol 2.0)
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
```

---

### 2.3 Passive Banner Grabbing

Extracts service information **without directly connecting to the target**. Invisible to the target because no packets are sent TO it.

| Method | How It Works | Tool |
|---|---|---|
| **Traffic Sniffing** | Capture traffic on the same network segment. Banners appear whenever any legitimate client connects. | Wireshark, tcpdump |
| **Shodan** | Continuously scans the entire public internet and indexes all service banners. Query the database — no packets to target. | [shodan.io](https://shodan.io) |
| **Censys.io / ZoomEye** | Similar to Shodan. Censys focuses on certificate transparency and TLS data. | [censys.io](https://censys.io) |

**Wireshark filters for banners:**

| Filter | Catches |
|---|---|
| `tcp contains "Server:"` | HTTP server banners |
| `tcp contains "SSH-"` | SSH banners |
| `tcp contains "220 "` | FTP/SMTP banners |

---

### 2.4 Banner → CVE Mapping

This is the critical step — why banners matter:

| Step | Action | Result |
|---|---|---|
| 1 | Banner grab reveals | "Apache httpd 2.4.49" |
| 2 | Search NVD (nvd.nist.gov) | Find CVE-2021-41773 |
| 3 | Read CVE | Path Traversal + RCE, CVSS 7.5 (HIGH) |
| 4 | Verify exploitability | Check if mod_cgi is enabled |
| 5 | Result | Remote Code Execution achieved |

**Real-World Case — Apache CVE-2021-41773 (October 2021):**
Within 24 hours of disclosure, threat actors deployed mass-scanning tools that grabbed HTTP banners, identified Apache 2.4.49 specifically, and attempted exploitation automatically. Shodan showed over 100,000 internet-facing hosts running this version. Thousands of servers compromised across government, healthcare, and education sectors.

**Lesson:** Default server banners are a roadmap for automated mass exploitation.

---

### 2.5 Banner Manipulation — Defender Strategy

Defenders can modify banners to remove version info or replace it with false info (honeypot technique).

| Service | Configuration | Result |
|---|---|---|
| **Apache** | `ServerSignature Off` + `ServerTokens Prod` in security.conf | Banner shows just "Apache" — no version |
| **OpenSSH** | `Banner /etc/ssh/banner_message` in sshd_config | Custom text. Note: SSH-2.0 protocol version cannot be hidden (required by spec). |
| **nginx** | `server_tokens off;` in nginx.conf | Banner shows "nginx" — no version |
| **ProFTPD** | `ServerIdent off` in proftpd.conf | Removes identification |

> [!IMPORTANT]
> Banner modification reduces speed of automated attacks but does NOT prevent a determined attacker from fingerprinting the service through behavioral analysis. It's a layer of defense, not a complete solution.

#### Defender Checklist for Banner Grabbing

- Remove version information from all service banners
- Deploy a WAF to strip Server: and X-Powered-By: headers at the WAF layer
- SIEM alert on multiple rapid connections to different ports from one source (classic banner-grab pattern)
- Keep all services patched — even if banner reveals version, patched version has no exploitable CVEs
- Consider honeypot banners on unused ports (fake "vsftpd 2.3.4" on port 21 attracts exploitation attempts and alerts you)

---

## Section 3 — OS Fingerprinting

### 3.1 What is OS Fingerprinting?

Determining the operating system running on a target host by analyzing the characteristics of packets it sends. These characteristics come from differences in how each OS implements the TCP/IP stack.

**Why it matters:** Different OSes have different default security configs, kernel vulnerabilities, installed software stacks, patch cycles, and exploitable misconfigs.

| Open Ports Found | + OS Identified | = Attack Path |
|---|---|---|
| 135, 139, 445 | Windows | SMB vulnerability path (EternalBlue, PrintNightmare) |
| 22, 80, 3306 | Linux | Apache/MySQL LAMP stack attack path |

---

### 3.2 Active OS Fingerprinting

**Sends specially crafted packets** to the target and analyzes responses. **Detectable** because it generates inbound traffic.

#### Key TCP/IP Behavioral Differences Exploited

**Difference 1 — Initial Sequence Number (ISN) Generation:**

| OS | ISN Pattern |
|---|---|
| Linux 4.x+ | Random (unpredictable) |
| Windows 10/11 | Random (modern) |
| Older Solaris | Time-based (predictable — exploitable) |
| OpenBSD | Random with cryptographic quality |

**Difference 2 — TCP Window Size:**

| OS | Typical Window Size |
|---|---|
| Linux (various) | 5840, 14600, 29200 bytes |
| Windows 10 | 8192 (initial), 65535 (scaled) |
| macOS | 65535 bytes |
| FreeBSD | 65535 bytes |
| Windows Server | 8192 (initial) |

**Difference 3 — Don't Fragment (DF) Bit:**
Most modern OSes set DF (supports Path MTU Discovery). Windows always sets DF on outbound. Some legacy systems never set DF.

**Difference 4 — TTL Initial Value:**

| Operating System | Default TTL |
|---|---|
| **Windows** | **128** |
| **Linux** | **64** |
| **Cisco IOS** | **255** |
| FreeBSD | 64 |
| Solaris | 255 |
| macOS | 64 |

> [!TIP]
> TTL decrements by 1 at each router hop. So: `observed_TTL = initial_TTL - number_of_hops`
>
> If I observe TTL=118 and know hops ≈ 10 → initial was ~128 → **Windows**
> If I observe TTL=54 and know hops ≈ 10 → initial was ~64 → **Linux**

**Difference 5 — Response to Illegal Flag Combinations:**

| OS | Response to NULL/XMAS/FIN on OPEN port | Response on CLOSED port |
|---|---|---|
| Linux/Unix (RFC compliant) | Silently drops | Sends RST |
| Windows | Sends RST regardless | Sends RST |

This single behavioral difference **reliably distinguishes** Windows from Unix/Linux.

**Difference 6 — ICMP Behavior:**
Different OSes include different amounts of the original packet in ICMP error messages and rate-limit ICMP differently.

---

#### Tool: NMAP OS Detection

```bash
sudo nmap -O -v [target_IP]
# -O = Enable OS detection (requires root — needs raw packets)
```

**Process:** Sends up to 16 specially crafted TCP/UDP/ICMP probes to open AND closed ports → analyzes against 5,700+ OS fingerprints → returns matched OS with confidence %.

**Example output:**

```
Running: Linux 4.X|5.X
OS details: Linux 4.15 - 5.6
Aggressive OS guesses: Linux 4.15 (97%), Linux 5.0 (96%), Linux 5.4 (94%)
```

**Requirements:** Needs at least one OPEN and one CLOSED port · Less accurate through NAT/firewalls · Requires root privileges

---

### 3.3 Passive OS Fingerprinting

Analyzes network traffic that **already exists** without sending any packets. Attacker is **completely invisible** to the target.

#### Tool: p0f

```bash
p0f -i eth0 -o /tmp/p0f_output.txt
# -i = network interface  -o = output file
```

**p0f example output:**

```
.-[ 192.168.1.45/50234 -> 192.168.1.1/80 (syn) ]-
| client   = 192.168.1.45
| os       = Windows 7 or 8
| dist     = 0
| raw_sig  = 4:128+0:0:65535:mss*44,0:mss,nop,nop,sackOK:df,id+:0
```

**What passive fingerprinting analyzes from observed traffic:**
- TCP SYN characteristics (window size, TTL, DF bit, options)
- HTTP User-Agent strings
- DHCP request patterns
- DNS query patterns (Windows sends NBNS queries; Linux does not)
- TLS client hello fingerprints (**JA3 signatures**)

---

#### JA3 Fingerprinting (2026 Relevant)

JA3 passively fingerprints TLS clients by hashing specific fields from the TLS ClientHello message: TLS version, cipher suites, extensions, elliptic curves, elliptic curve formats.

Different browsers and OSes produce **different JA3 hashes** because their TLS library implementations differ. Chrome 120 on Windows ≠ Chrome 120 on Linux.

| Use | How |
|---|---|
| **Attacker** | Malware produces unique JA3 signatures — security teams detect C2 even when destination IP is unknown |
| **Defender** | IDS rules match JA3 hashes of known malware families. Zeek generates JA3 hashes for all TLS traffic automatically. |

---

#### Defender Checklist for OS Fingerprinting

- Normalize TTL values at perimeter firewall — removes OS fingerprint info from outbound traffic
- Network segmentation — attacker on one segment can't observe traffic from others (eliminates passive fingerprinting)
- IDS signatures: Snort SID 1228 (NMAP OS fingerprint attempt), SID 1917 (OS fingerprinting probe)
- Consider network deception platforms that inject **false OS fingerprints** into traffic

---

## Section 4 — Proxy Servers in Attacks

### 4.1 Why Attackers Use Proxies

A proxy server is an intermediary that forwards requests on behalf of clients. Target sees the proxy's IP, not the attacker's.

| Reason | Detail |
|---|---|
| **IP Hiding** | Target logs show proxy IP, not attacker IP |
| **Geolocation Bypass** | Route through a country with no MLAT (no law enforcement cooperation) |
| **Firewall Bypass** | Some firewalls allow traffic from certain proxy IP ranges |
| **Rate Limit Bypass** | Multiple proxies distribute requests across different IPs |
| **Content Filter Bypass** | Bypass corporate filters blocking certain categories |

---

### 4.2 Types of Proxies

| Type | Layer | Description | Notes |
|---|---|---|---|
| **HTTP Proxy** | Layer 7 (Application) | Only handles HTTP/HTTPS traffic. Easy setup. | Most proxy logging happens here. E.g., Squid |
| **SOCKS Proxy** | Layer 5 (Session) | Protocol-agnostic — forwards ANY TCP/UDP (SSH, FTP, SMTP, DNS). More powerful. | SOCKS4: TCP only, no auth. SOCKS5: TCP+UDP, auth, IPv6. |
| **Transparent Proxy** | — | Client doesn't know it's being proxied. | Used by ISPs/corporations for content filtering |
| **Anonymous Proxy** | — | Hides client IP but adds X-Forwarded-For header — can still reveal original IP. | Less anonymous than claimed |
| **Elite (High-Anonymity) Proxy** | — | Does NOT add X-Forwarded-For. Target has no indication proxy is in use. | Most difficult to detect. Expensive/unreliable. |
| **Tor Network** | — | Onion routing through 3+ encrypted relay nodes. Each relay only knows previous and next hop. | Exit node traffic is unencrypted. Slow. Some targets block Tor exits. Traffic analysis can de-anonymize. |

**NMAP through SOCKS5 proxy:**

```bash
proxychains nmap -sT -p 80,443 [target]
```

---

### 4.3 Proxy Chaining

Routes traffic through **multiple proxies** in sequence. Each proxy only knows the IP before it and after it.

```
ATTACKER IP → PROXY 1 → PROXY 2 → PROXY 3 → TARGET
(India)       (USA)      (Russia)  (Brazil)
```

| Who | Sees |
|---|---|
| Target | PROXY 3's IP (Brazil) |
| PROXY 3 | PROXY 2's IP (Russia) |
| PROXY 2 | PROXY 1's IP (USA) |
| PROXY 1 | Attacker's real IP (India) |

Each jurisdiction boundary adds legal complexity to trace-back.

#### Tool: ProxyChains

Configuration: `/etc/proxychains4.conf`

```
socks5 192.168.1.10 1080
socks4 10.0.0.1 1080
http   172.16.0.1 8080
```

```bash
proxychains nmap -sT [target]
proxychains firefox
proxychains sqlmap -u "http://target/page.php?id=1"
```

| Mode | Behavior |
|---|---|
| `strict_chain` | Use proxies exactly in listed order (all must be online) |
| `dynamic_chain` | Skip dead proxies — use whatever is alive |
| `random_chain` | Use proxies in random order each connection (maximum unpredictability) |

**Real-World Case — APT28 (Fancy Bear) Proxy Infrastructure (2016–2023):**
Russian state-sponsored group built proxy infrastructure across compromised home routers in the US, Europe, and Asia. Thousands of routers formed a distributed proxy chain that law enforcement couldn't dismantle without disrupting consumer internet. Multiple NATO government networks compromised. Attribution delayed by years. **Lesson:** The most effective proxy chains use **compromised systems** as nodes — no logs, no billing records, no entity to subpoena.

---

### 4.4 Burp Suite as Intercept Proxy

In addition to anonymizing proxies, attackers use **intercept proxies** to sit between browser and target — capturing, modifying, and replaying every HTTP/HTTPS request.

```
┌─────────────┐      ┌──────────────┐      ┌─────────────┐
│  Attacker's │      │  Burp Suite  │      │   Target    │
│   Browser   │ ←──→ │  (Proxy on   │ ←──→ │  Web App    │
│             │      │ 127.0.0.1:   │      │             │
└─────────────┘      │   8080)      │      └─────────────┘
                     └──────────────┘
```

**Not the same as anonymizing proxy:**

| Type | Purpose |
|---|---|
| Anonymizing proxy | Hides attacker's IP from target |
| Intercept proxy (Burp) | Gives attacker visibility and control over every HTTP message |

---

#### Defender Checklist for Proxy Detection

- Analyze inbound HTTP headers for X-Forwarded-For presence
- Use threat intel feeds of known Tor exit nodes, open proxies, VPN exit ranges — block or alert
- IP reputation scoring in WAF/SIEM — data center IPs warrant scrutiny
- Correlate behavioral patterns rather than IPs — if source IPs rotate but browser fingerprint (User-Agent, JA3 hash) stays identical → single user rotating proxies
- GeoIP restrictions for critical systems — if user base is India-only, block/challenge connections from outside India

---

## Section 5 — HTTP Tunneling Techniques

### 5.1 What is HTTP Tunneling?

Encapsulating non-HTTP protocol traffic within HTTP request/response messages to **bypass firewalls** that only permit HTTP (port 80) or HTTPS (port 443).

**Why firewalls create this vulnerability:**
Many corporate firewalls use "default deny" outbound, allowing only:
- Port 80 (HTTP) — web browsing is a business need
- Port 443 (HTTPS) — secure web browsing
- Port 53 (DNS) — name resolution required

All other outbound ports (SSH, RDP, custom C2) are blocked. If you can make ANY traffic look like HTTP, you bypass the firewall completely.

---

### 5.2 How HTTP Tunneling Works

**Basic Architecture:**

```
COMPROMISED HOST → [FAKE HTTP REQUESTS] → CORPORATE FIREWALL
                    (real payload inside)         ↓
                                          (allows port 80)
                                                  ↓
                                       ATTACKER'S HTTP SERVER
                                       (unwraps HTTP, sees payload)
```

#### Payload Encoding Methods

| Method | How |
|---|---|
| **Query String Encoding** | Command encoded in URL: `GET /?cmd=bHMgLWxh HTTP/1.1` (Base64 in URL parameter) |
| **POST Body Encoding** | Real traffic encoded in POST body disguised as file upload |
| **HTTP Headers** | Custom headers carry payload: `X-Session-Data: [base64 payload]` |
| **Chunked Transfer Abuse** | HTTP/1.1 chunked transfer fragments payloads into small pieces that reassemble at tunnel endpoint |

---

### 5.3 Attack Scenarios

#### Scenario 1 — C2 Through HTTP Tunnel

Corporate firewall blocks all outbound except 80/443. Malware communicates via:

| Step | What Happens | Looks Like |
|---|---|---|
| 1 | Malware sends HTTP GET to C2 server | Normal web browsing |
| 2 | C2 responds with HTTP 200 (command encoded in Base64 body) | Normal web response |
| 3 | Malware executes command, captures output | — |
| 4 | Malware sends output via HTTP POST | Normal web form submission |

**Tools:** Cobalt Strike (malleable HTTP profiles) · Metasploit meterpreter/reverse_http · Empire framework HTTP C2

---

#### Scenario 2 — SSH Over HTTP

Developer SSHs into home server from corporate network that blocks port 22:

| Where | What |
|---|---|
| Home server | `httptunnel_server --port 80` (HTTP server that tunnels SSH) |
| Corporate machine | `httptunnel_client http://home.server.com:80` then `ssh -p [local_port] localhost` |
| Corporate firewall sees | Outbound HTTP to port 80. Actual traffic: SSH session. |

---

#### Scenario 3 — DNS Tunneling

Firewall blocks HTTP but allows DNS queries (port 53).

| Step | What Happens |
|---|---|
| 1 | Attacker registers domain, runs custom DNS server |
| 2 | Malware encodes data into DNS query: `[base64_data].tunnel.attacker.com → A record?` |
| 3 | Attacker's DNS server receives query, decodes data, processes, returns response encoded as IP |
| 4 | Malware decodes IP as data |

**Tools:** iodine, dnscat2, dns2tcp

**Real-World Case — OilRig APT DNS Tunneling (2019–2022):**
Iranian state-sponsored group used custom DNS tunneling tool "DNSExfiltrator" to exfiltrate data from Middle Eastern organizations. Data split into DNS query labels (max 63 chars each). Exfiltration went undetected for months because DNS traffic was not inspected. **Lesson:** DNS traffic must be inspected — high query volumes to a single domain or unusually long domain names are key indicators.

---

### 5.4 Detecting HTTP Tunneling — Deep Packet Inspection

DPI examines packet **content (payload)**, not just headers. Basic firewalls check source/destination IP and port. DPI checks: does the content actually look like HTTP?

#### Indicators of HTTP Tunneling

| Indicator | Legitimate HTTP | Tunneled HTTP |
|---|---|---|
| **Request patterns** | Short URLs, recognized paths, proper User-Agent, Referrer | Long random strings in params, missing/suspicious User-Agent, no Referrer, binary/Base64 body |
| **Timing** | Irregular (human-paced browsing), different URLs | Regular intervals (every 30 sec exactly), identical repeated requests |
| **Size** | Variable, asymmetric (more downloaded than uploaded) | Large POST volumes to single destination with no corresponding web app |
| **DNS tunneling indicators** | — | Abnormally long subdomain labels (>50 chars), high query rate to single domain, newly registered domain, no web presence |

---

#### Defender Checklist for HTTP Tunneling

- Deploy NGFW with DPI — analyze application layer content. Alert on large POSTs to unknown domains, regular-interval polling.
- Implement SSL/TLS inspection at perimeter — decrypt HTTPS, inspect, re-encrypt. Required to see into HTTPS tunnels.
- Monitor DNS query volumes per host — alert if any host sends >100 queries/min to a single external domain
- DNS security: DNSSEC, block newly registered domains (<30 days old), log all DNS to SIEM
- Proxy-based internet access — all HTTP/HTTPS through corporate proxy. Direct port 80/443 blocked. Forces tunneled traffic through inspection.
- Snort/Suricata rule for DNS tunneling:

```
alert dns any any -> any 53 (
  msg:"Possible DNS tunnel - Long subdomain";
  pcre:"/[a-zA-Z0-9+\/=]{50,}\.[a-z]{2,6}$/";
  classtype:trojan-activity;
  sid:9000001; rev:1;
)
```

---

## Section 6 — MITRE ATT&CK Mapping

### Tactic: TA0043 — Reconnaissance

| Tech ID | Technique | Session 11A Mapping | Tool |
|---|---|---|---|
| T1595.001 | Active Scanning: IP Blocks | TCP flag-based port scanning (SYN, FIN, NULL, XMAS, ACK) | NMAP |
| T1592.001 | Gather Victim Host Info: Hardware | Active/passive OS fingerprinting | NMAP -O, p0f |
| T1592.004 | Gather Victim Host Info: Client Configs | Banner grabbing from network services | Netcat, Telnet, NMAP -sV |
| T1596.005 | Search Open Technical DBs: Scan Databases | Passive banner grabbing via pre-indexed data | Shodan.io, Censys.io |

### Tactic: TA0011 — Command and Control

| Tech ID | Technique | Session 11A Mapping | Tool |
|---|---|---|---|
| T1090.001 | Proxy: Internal Proxy | Proxy servers to route attack traffic | ProxyChains, Tor |
| T1090.003 | Proxy: Multi-hop Proxy | Proxy chaining across jurisdictions | ProxyChains (random_chain) |
| T1572 | Protocol Tunneling | HTTP tunneling — encapsulating non-HTTP in HTTP/HTTPS | HTTunnel, Cobalt Strike HTTP |
| T1071.001 | Application Layer Protocol: Web | HTTP as transport for C2 communication | Metasploit reverse_http, Cobalt Strike |
| T1071.004 | Application Layer Protocol: DNS | DNS tunneling for C2 and data exfiltration | iodine, dnscat2, dns2tcp |

> [!IMPORTANT]
> **Cross-tactic insight:** Session 11A techniques span BOTH Reconnaissance (TA0043) AND Command and Control (TA0011). The same knowledge of TCP flags, tunneling, and proxies used to RECON targets is also used to MAINTAIN ACCESS after compromise.
>
> **For SIEM rule writers:** An internal host showing both banner grabbing behavior (T1592.004) AND regular HTTP requests to an unusual domain (T1071.001) exhibits both Reconnaissance AND C2 patterns — could indicate a compromised machine conducting further internal recon.

---

## Section 7 — 2026 Context

### 7.1 AI-Assisted Scanning and Fingerprinting

| Development | Detail |
|---|---|
| **AI-Powered Scanning** | ML models predict which ports are most likely open on specific OS/service combos → maximizes info per probe, minimizes total probes. Shodan Trends + AI allows asking "what ports are commonly open on AWS EC2 Ubuntu 22.04?" before sending a single packet. |
| **ML-Based Passive OS Fingerprinting** | 2025 Georgia Tech research: ML-based system achieved 98.5% accuracy on **encrypted traffic** (HTTPS/TLS) by analyzing packet timing and size distributions alone. HTTPS does NOT protect against OS fingerprinting with ML. |
| **AI Banner Exploitation Pipeline** | Takes banner grab outputs → auto-identifies versions → queries multiple CVE DBs → generates prioritized exploitation plan → suggests Metasploit modules. Time from "banner grabbed" to "exploitation ready" collapsed from hours to **under 60 seconds**. |
| **Commercial NDR** | Vectra AI, Darktrace use ML fingerprinting to build behavioral baselines of every device, alerting on TCP/IP behavior changes (OS migration or rootkit activity). |

> [!WARNING]
> **Implication for defenders:** The window between a service being discoverable and being targeted by automated exploitation has collapsed from days to minutes. Patch management SLAs must be measured in **HOURS** for critical CVEs, not days.

---

### 7.2 HTTP Tunneling and Proxy Evolution

#### HTTPS-Based C2 (Dominant in 2025–2026)

Near-universal adoption of HTTPS (port 443) for C2 by advanced threat actors:
- **Encrypted** — content can't be inspected without TLS interception
- **Legitimate certs** — Let's Encrypt provides free valid certs for C2 domains in minutes
- **Blends in** — most enterprise traffic is HTTPS
- **Domain Fronting** — CDN abuse (see below)

#### Domain Fronting

```
Malware → connects to: legit-cdn.amazonaws.com (TLS)
       → HTTP Host header inside TLS: c2.attacker.com
CDN forwards to attacker's C2 server.
Firewall sees: HTTPS to amazonaws.com (trusted, allowed)
Actual destination: attacker's C2.
```

**2025 status:** AWS, Google, Microsoft have taken steps to prevent domain fronting (check that SNI matches Host header). Not all CDN providers enforce this, and attackers have found bypasses.

#### India-Specific Legal Context

| Law | Relevance |
|---|---|
| **DPDPA 2023 Section 8(6)** | Data fiduciary must notify Data Protection Board of any personal data breach — HTTP tunneling C2 represents a data exfiltration risk under breach notification requirements |
| **DPDPA 2023 Section 8(7)** | Must take prompt action to mitigate breach consequences |
| **IT Act 2000 Section 43A** | Corporate body handling sensitive data that fails "reasonable security practices" is liable for compensation. Failing to deploy DPI to detect HTTP tunneling could be argued as failure to implement reasonable security. |

---

### ✅ Session 11A — Key Takeaways

- [x] TCP control flags (SYN, ACK, FIN, RST, PSH, URG) are single bits defining every packet's meaning
- [x] Three-way handshake (SYN → SYN+ACK → ACK) establishes connection; RST terminates immediately; FIN closes gracefully via four-way handshake
- [x] SYN scans exploit the half-open connection state — RST sent after SYN+ACK prevents application-layer logging
- [x] Windows does NOT follow RFC 793 for FIN/NULL/XMAS — sends RST to ALL ports regardless of state (making these scans unreliable but revealing Windows OS)
- [x] Banner grabbing reads self-identification strings from open ports — reveals software name, version, OS → enables direct CVE lookup
- [x] Active banner grabbing (Netcat, NMAP -sV) is detectable; passive (Shodan, Censys, sniffing) is invisible
- [x] OS fingerprinting exploits TCP/IP stack differences: TTL (Windows=128, Linux=64, Cisco=255), window size, ISN generation, flag response behavior
- [x] Active OS fingerprinting (NMAP -O) sends crafted probes and is detectable; passive (p0f) is completely invisible
- [x] JA3 TLS fingerprinting passively identifies clients and malware C2 from TLS ClientHello even when content is encrypted
- [x] Proxies hide attacker IP but most maintain logs — not true anonymity. Proxy chaining adds legal complexity but requires all nodes to be log-free
- [x] HTTP tunneling encapsulates non-HTTP traffic inside HTTP to bypass firewalls allowing only port 80/443 — used for C2, SSH bypass, data exfiltration
- [x] DNS tunneling encodes data in DNS query strings through port 53 — dangerous because DNS is rarely inspected
- [x] In 2026: AI-assisted scanning, HTTPS C2 with domain fronting, and ML-based traffic fingerprinting require DPI, SSL inspection, and behavioral AI detection

---

<details>
<summary>📖 Session 11A — Glossary</summary>

| Term | Definition |
|---|---|
| TCP Flag | 1-bit control field in TCP header signaling connection state (SYN, ACK, FIN, RST, PSH, URG, ECE, CWR) |
| SYN Flag | Synchronize — initiates TCP connection; first packet in handshake |
| ACK Flag | Acknowledgement — confirms receipt of prior segment |
| FIN Flag | Finish — graceful connection termination request |
| RST Flag | Reset — abrupt connection termination |
| PSH Flag | Push — pass data immediately to application layer |
| URG Flag | Urgent — data at offset should be processed immediately |
| ECE Flag | ECN-Echo — signals network congestion (RFC 3168) |
| CWR Flag | Congestion Window Reduced — confirms sender reduced congestion window |
| Three-Way Handshake | SYN → SYN-ACK → ACK connection establishment |
| Banner | Text string transmitted by a service upon connection, revealing app name/version/OS |
| Banner Grabbing | Connecting to open port and reading service identification string |
| Active Banner Grab | Direct connection to target — leaves logs. Tools: Netcat, Telnet, Nmap -sV |
| Passive Banner Grab | Intercepting banners from existing traffic. Tools: Wireshark, Shodan |
| OS Fingerprinting | Determining remote host's OS by analyzing TCP/IP stack behavior |
| Active Fingerprinting | Sending crafted packets to determine OS. Detectable. Tool: Nmap -O |
| Passive Fingerprinting | Analyzing existing traffic. Undetectable. Tool: p0f |
| TTL (Time To Live) | IP header field decremented per hop. Linux=64, Windows=128, Cisco=255 |
| Window Size | TCP field specifying receivable bytes before ACK. Default differs by OS. |
| JA3 Fingerprinting | Passive TLS client fingerprinting by hashing ClientHello fields |
| Proxy Server | Intermediary forwarding requests on behalf of clients, hiding original IP |
| Forward Proxy | Receives client requests, forwards to target on client's behalf |
| Reverse Proxy | Placed in front of servers. Clients connect to proxy, which routes to backend. |
| Transparent Proxy | Intercepts traffic without client configuration |
| Proxy Chaining | Routing through sequential proxies in multiple countries for anonymity |
| Tor (The Onion Router) | Anonymity network routing through 3+ encrypted relay nodes |
| HTTP Tunneling | Encapsulating non-HTTP data within HTTP packets to bypass firewalls |
| HTTPS Tunneling | HTTP tunneling over port 443 with TLS. Bypasses DPI without SSL inspection. |
| DNS Tunneling | Encoding data in DNS query/response packets for C2/exfiltration through port 53 |
| ICMP Tunneling | Encapsulating data in ICMP Echo Request/Reply packets |
| Covert Channel | Communication path not designed for info transfer, used to bypass security |
| DPI (Deep Packet Inspection) | Firewall/IDS capability to inspect packet payload beyond headers |
| Domain Fronting | Routing HTTPS through trusted CDN while actual destination is attacker C2 |
| CONNECT Method | HTTP method instructing proxy to establish TCP tunnel to target host |
| Httptunnel | Tool creating bidirectional HTTP tunnel (hts=server, htc=client) |
| p0f | Passive OS fingerprinting tool — identifies OS without sending probes |
| ServerMask | Commercial tool to alter/remove HTTP Server headers |
| T1592 | MITRE ATT&CK ID for "Gather Victim Host Information" |
| T1071.001 | MITRE ATT&CK ID for "Application Layer Protocol: Web Protocols" |
| T1090.003 | MITRE ATT&CK ID for "Proxy: Multi-hop Proxy" |
| T1071.004 | MITRE ATT&CK ID for "Application Layer Protocol: DNS" |
| T1572 | MITRE ATT&CK ID for "Protocol Tunneling" |
| TA0011 | MITRE ATT&CK Tactic for "Command and Control" |
| TA0007 | MITRE ATT&CK Tactic for "Discovery" |

</details>

---

**What's next — Session 11B** covers IP spoofing techniques, enumeration (NetBIOS, SNMP, LDAP, DNS), SMB redirection and relay MITM attacks, and NetBIOS DoS attacks. Session 11A identified WHAT is running and the OS present. Session 11B uses that intelligence offensively against Windows-specific attack paths.

---