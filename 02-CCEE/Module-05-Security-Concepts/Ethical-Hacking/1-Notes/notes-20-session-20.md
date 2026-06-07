# Session 20 — Malware Types · Malicious Code Families · Latest Trends · Static & Dynamic Analysis 🔬

> Personal study notes | Ethical Hacking Module | CCEE Prep

---

## 📑 Table of Contents

- [🗺️ Where This Session Fits](#️-where-this-session-fits)
- [⚠️ Exam Traps & Misconceptions](#️-exam-traps--misconceptions)
- [🧱 Foundation Knowledge](#-foundation-knowledge)
- [Section 1 — Malware Types](#section-1--malware-types)
  - [1.1 Virus](#11-virus)
  - [1.2 Worm](#12-worm)
  - [1.3 Trojan Horse](#13-trojan-horse)
  - [1.4 Ransomware](#14-ransomware)
  - [1.5 Spyware](#15-spyware)
  - [1.6 Adware](#16-adware)
  - [1.7 Rootkit](#17-rootkit)
  - [1.8 Bootkit](#18-bootkit)
  - [1.9 Keylogger](#19-keylogger)
  - [1.10 Backdoor](#110-backdoor)
  - [1.11 Dropper and Downloader](#111-dropper-and-downloader)
  - [1.12 Fileless Malware](#112-fileless-malware)
  - [1.13 Logic Bomb](#113-logic-bomb)
  - [1.14 Bot / Zombie](#114-bot--zombie)
  - [1.15 Wiper / Destructive Malware](#115-wiper--destructive-malware)
- [Section 2 — Malicious Code Families](#section-2--malicious-code-families)
  - [2.1 What Is a Malware Family](#21-what-is-a-malware-family)
  - [2.2 Banking Trojans](#22-banking-trojans)
  - [2.3 RAT Families](#23-rat-families)
  - [2.4 Ransomware Families](#24-ransomware-families)
  - [2.5 Infostealer Families](#25-infostealer-families)
  - [2.6 Botnet Malware Families](#26-botnet-malware-families)
  - [2.7 Rootkit Families](#27-rootkit-families)
- [Section 3 — Latest Trends in Malware](#section-3--latest-trends-in-malware)
  - [3.1 Ransomware-as-a-Service (RaaS)](#31-ransomware-as-a-service-raas)
  - [3.2 Supply Chain Attacks](#32-supply-chain-attacks)
  - [3.3 Living-off-the-Land (LotL)](#33-living-off-the-land-lotl)
  - [3.4 AI-Generated and AI-Enhanced Malware](#34-ai-generated-and-ai-enhanced-malware)
  - [3.5 Infostealer + Session Cookie Theft](#35-infostealer--session-cookie-theft)
  - [3.6 Mobile Malware Trends](#36-mobile-malware-trends)
  - [3.7 IoT and OT/ICS Malware](#37-iot-and-otics-malware)
  - [3.8 Double and Triple Extortion Ransomware](#38-double-and-triple-extortion-ransomware)
- [Section 4 — Malware Analysis Overview](#section-4--malware-analysis-overview)
  - [4.1 Goals of Malware Analysis](#41-goals-of-malware-analysis)
  - [4.2 Analysis Environment Setup](#42-analysis-environment-setup)
  - [4.3 Analysis Workflow](#43-analysis-workflow)
- [Section 5 — Static Malware Analysis](#section-5--static-malware-analysis)
  - [5.1 What Is Static Analysis](#51-what-is-static-analysis)
  - [5.2 File Identification](#52-file-identification)
  - [5.3 Hashing](#53-hashing)
  - [5.4 String Extraction](#54-string-extraction)
  - [5.5 PE File Analysis](#55-pe-file-analysis)
  - [5.6 Packer Detection](#56-packer-detection)
  - [5.7 Import / Export Analysis](#57-import--export-analysis)
  - [5.8 Disassembly and Decompilation](#58-disassembly-and-decompilation)
  - [5.9 YARA Rules](#59-yara-rules)
  - [5.10 Static Analysis Tools Reference](#510-static-analysis-tools-reference)
- [Section 6 — Dynamic Malware Analysis](#section-6--dynamic-malware-analysis)
  - [6.1 What Is Dynamic Analysis](#61-what-is-dynamic-analysis)
  - [6.2 Sandbox Analysis](#62-sandbox-analysis)
  - [6.3 Process Monitoring](#63-process-monitoring)
  - [6.4 File System Monitoring](#64-file-system-monitoring)
  - [6.5 Registry Monitoring](#65-registry-monitoring)
  - [6.6 Network Traffic Analysis](#66-network-traffic-analysis)
  - [6.7 Memory Analysis](#67-memory-analysis)
  - [6.8 API Monitoring and Hooking](#68-api-monitoring-and-hooking)
  - [6.9 Dynamic Analysis Tools Reference](#69-dynamic-analysis-tools-reference)
- [Section 7 — Indicators of Compromise (IOCs)](#section-7--indicators-of-compromise-iocs)
  - [7.1 What Are IOCs](#71-what-are-iocs)
  - [7.2 IOC Types and Examples](#72-ioc-types-and-examples)
  - [7.3 IOC Sharing Formats](#73-ioc-sharing-formats)
- [📌 Extra Notes](#-extra-notes)
  - [E1 — Static vs Dynamic Analysis Comparison](#e1--static-vs-dynamic-analysis-comparison)
  - [E2 — Anti-Analysis Techniques Malware Uses](#e2--anti-analysis-techniques-malware-uses)
  - [E3 — PE File Format Deep Dive](#e3--pe-file-format-deep-dive)
  - [E4 — Malware Naming Conventions](#e4--malware-naming-conventions)
  - [E5 — USB Pratirodh and AppSamvid — Syllabus Note](#e5--usb-pratirodh-and-appsamvid--syllabus-note)
  - [E6 — Famous Malware Case Studies](#e6--famous-malware-case-studies)
  - [E7 — Malware Analysis Lab Setup](#e7--malware-analysis-lab-setup)
  - [E8 — Predecessor / Successor Chains](#e8--predecessor--successor-chains)
  - [E9 — Terminology Traps](#e9--terminology-traps)
  - [E10 — Current Landscape 2026](#e10--current-landscape-2026)
  - [E11 — Indian Legal Context](#e11--indian-legal-context)
- [Abbreviations Table](#abbreviations-table)
- [🔑 Keywords + Concept Map](#-keywords--concept-map)
- [⚡ Quick Reference Cheatsheet](#-quick-reference-cheatsheet)
- [✅ Session Revision Snapshot](#-session-revision-snapshot)
- [Module Completion Note](#module-completion-note)
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
        ├── Session 14      : Viruses · Worms · AV Evasion · Detection
        ├── Session 15      : Sniffing · ARP Poisoning · DNS Attacks
        ├── Session 16A     : DoS · DDoS · BOTs/BOTNETs · SYN Flood
        ├── Session 16B     : Spoofing vs Hijacking · Session Hijacking
        ├── Session 17A     : Web Server Hacking · Web App Vulnerabilities
        ├── Session 17B     : Wireless Hacking · WEP/WPA · SSID/MAC
        ├── Session 18      : Backdoors · DDoS Advanced · Biometrics · IDS
        ├── Session 19      : Physical Security · Penetration Testing
        └── ▶ SESSION 20    : Malware Types · Malicious Code Families
                              Latest Trends · Static + Dynamic Analysis
                                                         ← YOU ARE HERE
                                                    ← FINAL SESSION

**Phase position:** Session 20 is the capstone session — bringing
together malware knowledge from throughout the module and providing
the analytical methodology (static and dynamic analysis) to examine
malware from the defender's perspective.

Where Sessions 12–14 covered how malware is built, deployed, and evades
detection (attacker perspective), Session 20 covers how malware is
dissected, understood, and attributed (analyst perspective). The evasion
techniques from Session 13 (packing, obfuscation, anti-VM) are now
examined from the reverse engineering side — learning to defeat them.

This session also covers the latest trends that connect everything:
RaaS, supply chain attacks, LotL, and AI-generated malware — tying
directly into Sessions 8 (cyber crime), 16A (DDoS/botnets), 17A (web
attacks), and 18 (backdoors).

---

## ⚠️ Exam Traps & Misconceptions

| ❌ Misconception | ✅ Reality |
|---|---|
| Static analysis runs the malware to observe its behaviour | Static analysis examines the malware FILE WITHOUT EXECUTING IT. Dynamic analysis runs the malware in a controlled environment. |
| Dynamic analysis is always safer than static analysis | Static analysis is SAFER — no execution risk. Dynamic analysis requires isolation (sandboxes, VMs) because the malware actually runs. |
| Ransomware encrypts the entire operating system | Ransomware typically encrypts USER FILES (documents, images, databases) — not OS files needed to boot and display the ransom note. Some ransomware (Petya/NotPetya) encrypts the MBR — but encrypting ALL OS files would prevent ransom payment. |
| A dropper and a downloader are the same thing | A DROPPER contains the malware payload embedded within itself and drops it. A DOWNLOADER contains no payload — it connects to a remote URL and downloads the malware. Different mechanisms, same functional outcome. |
| Fileless malware leaves absolutely no trace | Fileless malware leaves NO FILE ON DISK but leaves traces in: memory (RAM), Windows Event Logs, PowerShell Script Block Logs, WMI repository, registry, network logs. It is not truly traceless. |
| A logic bomb is a type of ransomware | A logic bomb is a TRIGGER-BASED payload — it executes a destructive action when a specific condition is met (date, event, file deletion). It is not inherently related to ransomware — it predates ransomware by decades. |
| Wiper malware and ransomware have the same goal | Ransomware ENCRYPTS and demands payment — files are recoverable with key. Wiper malware PERMANENTLY DESTROYS data — no recovery possible, no ransom demanded. NotPetya was disguised as ransomware but was actually a wiper. |
| Static analysis always produces definitive malware identification | Packed, encrypted, or obfuscated malware may reveal very little during static analysis — requiring dynamic analysis or advanced reverse engineering to understand behaviour. Static analysis has significant limitations against well-obfuscated samples. |
| YARA rules detect malware by its behaviour | YARA rules match STATIC PATTERNS (byte sequences, strings, PE structure) in files — they are a STATIC ANALYSIS tool. Behaviour-based detection is done by EDR/SIEM — not YARA. |
| All malware samples from the same family are identical | Within a malware family, each VARIANT may have different compilation timestamps, different C2 addresses, different encryption keys, different packer layers — but share core CODE LOGIC that identifies family membership. |

---

## 🧱 Foundation Knowledge

<details>
<summary>Click to expand — Must-know before this session</summary>

**Malware Knowledge Recap from Previous Sessions**

| Session | Malware Content | Connects to Session 20 |
|---|---|---|
| Session 12B | Trojans, backdoors, reverse shells | Trojan family analysis |
| Session 13 | Packing, obfuscation, anti-VM | Anti-analysis techniques |
| Session 14 | Viruses, worms, AV evasion | Virus/worm static analysis |
| Session 16A | Botnets, C2 infrastructure | Botnet malware families |
| Session 18 | Rootkits, LKM hooks | Rootkit analysis |

**Windows Process and Memory Basics**

- Every running program is a PROCESS — has PID, memory space, handles
- Processes have: virtual memory space, heap, stack, loaded DLLs
- Malware injects into: explorer.exe, svchost.exe, lsass.exe
- Key process tools: Process Explorer, Process Hacker, Procmon

**PE (Portable Executable) File Format**

    DOS Header → PE Signature → PE Header → Section Headers → Sections
    Sections: .text (code), .data (data), .rsrc (resources), .reloc (reloc)
    Import Address Table (IAT): lists DLLs and functions the PE uses
    Export Table: functions the PE exposes to other modules

**Windows Registry — Persistence Locations**

    HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
    HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
    HKLM\SYSTEM\CurrentControlSet\Services
    HKCU\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon

**Key Analysis Concepts**
- **Hash**: SHA-256 fingerprint uniquely identifies a specific file version
- **IOC**: Indicator of Compromise — hash, IP, domain, registry key
- **TTPs**: Tactics, Techniques, Procedures — attacker behavioural patterns
- **C2**: Command and Control — server malware calls home to

**MITRE ATT&CK Reference**
- T1204 — User Execution (initial execution)
- T1059 — Command and Scripting Interpreter
- T1055 — Process Injection
- T1027 — Obfuscated Files or Information
- T1497 — Virtualization/Sandbox Evasion
- T1041 — Exfiltration Over C2 Channel
- T1486 — Data Encrypted for Impact (ransomware)
- T1485 — Data Destruction (wiper)

</details>

---

## Section 1 — Malware Types

### 1.1 Virus

**WHAT:** Self-replicating malware that attaches to a host file and
spreads when that file is executed — requires human action to propagate.

**Key properties:**
- Needs a host file to exist
- Requires user execution of infected file to spread
- Payload varies: file corruption, data theft, display messages
- Types: boot sector, file infector, macro, polymorphic, metamorphic

**Deep coverage:** Session 14 — refer for full lifecycle and types.

---

### 1.2 Worm

**WHAT:** Self-replicating malware that spreads AUTONOMOUSLY across
networks by exploiting vulnerabilities — requires NO human action
and NO host file.

**Key properties:**
- Standalone executable — no host file needed
- Spreads automatically via network vulnerabilities
- Payload: DDoS, backdoor installation, file deletion
- Examples: Morris Worm, WannaCry, Conficker

**Deep coverage:** Session 14.

---

### 1.3 Trojan Horse

**WHAT:** Malware disguised as a legitimate, useful program — does
not self-replicate but provides unauthorized access or data theft.

**Key properties:**
- Social engineering delivery — user voluntarily installs
- No self-replication — must be deployed by attacker
- Payloads: RAT, backdoor, credential stealer, banking fraud
- Examples: Zeus, Emotet (early), DarkComet

**Deep coverage:** Sessions 12B, 13.

---

### 1.4 Ransomware

**WHAT:** Malware that encrypts victim's files and demands payment
(typically cryptocurrency) for the decryption key.

**Mechanism:**

    Delivery (phishing, exploit, RDP brute force)
            ↓
    Initial execution — often via dropper
            ↓
    Reconnaissance — enumerate files, network shares, backups
            ↓
    Shadow copy deletion:
      vssadmin delete shadows /all /quiet
      wmic shadowcopy delete
            ↓
    Encryption:
      Generate symmetric key (AES-256) per file or per session
      Encrypt each targeted file
      Encrypt symmetric key with attacker's RSA public key
      (Attacker holds RSA private key — required to recover AES key)
            ↓
    Ransom note dropped — instructions for payment
            ↓
    Optional: data exfiltration BEFORE encryption (double extortion)

**File extension changes:** `.locky`, `.cerber`, `.ryuk`, `.wannacry`

**Why shadow copies are deleted first:**
VSS (Volume Shadow Copy Service) creates point-in-time snapshots —
victims could restore from snapshots without paying. Deleting shadows
eliminates this free recovery option — forces payment decision.

**Cryptocurrency preference:**
- Bitcoin: pseudonymous, widely accepted — but blockchain is traceable
- Monero (XMR): privacy coin — fully anonymous — increasingly preferred
- RaaS affiliates typically pay operators 20–30% of ransom proceeds

> [!IMPORTANT]
> Modern ransomware uses **hybrid encryption**:
> Fast symmetric cipher (AES-256) encrypts FILE CONTENTS.
> Slow asymmetric cipher (RSA-2048 or ECC) encrypts the AES KEY.
> This means: even if you capture the malware sample and extract the
> hardcoded public key — you cannot decrypt files without the attacker's
> private key. Decryption requires either paying the ransom, finding
> the private key in a takedown, or having backups.

---

### 1.5 Spyware

**WHAT:** Malware that secretly monitors user activity and transmits
collected information to the attacker — without the user's knowledge.

**What spyware collects:**
- Keystrokes (keylogging component)
- Screenshots at intervals
- Browser history and saved passwords
- Email content
- Webcam and microphone activation
- GPS location (mobile spyware)
- Banking credentials during web sessions

**Commercial vs malicious spyware:**
Some spyware is sold commercially as "monitoring software" (parental
controls, employee monitoring) — legality depends on consent and
jurisdiction. Malicious deployment without consent is criminal.

**Notable examples:**
- **Pegasus** (NSO Group): state-sponsored iOS/Android spyware —
  zero-click exploits — accessed journalists, activists, world leaders
- **FinFisher/FinSpy**: commercial surveillance tool — used by governments
- **FlexiSPY, mSpy**: commercial mobile spyware marketed for parental use

---

### 1.6 Adware

**WHAT:** Software that displays unwanted advertisements — often
bundled with legitimate free software.

**Characteristics:**
- Usually not destructive — revenue generation model
- May redirect browser searches, inject ads into web pages
- Can degrade system performance significantly
- Often collects browsing data for targeted advertising
- Spectrum: grey area between PUP (Potentially Unwanted Program) and malware

**Grey area:** Some adware is disclosed in end-user license agreements
(EULAs) that no one reads — technically "consented to" — but
functionally malicious in effect.

---

### 1.7 Rootkit

**WHAT:** Malware designed to gain and MAINTAIN privileged (root/admin)
access while hiding its own presence from the operating system and
security tools.

**Rootkit types:**

| Type | Where It Operates | Persistence | Detection Difficulty |
|---|---|---|---|
| **User-mode** | User space — hooks Win32 API | Moderate | Moderate |
| **Kernel-mode (LKM)** | OS kernel — hooks sys_call_table | High | High |
| **Bootkit** | MBR/VBR/UEFI — pre-OS | Very High | Very High |
| **Hypervisor rootkit** | Below OS — Type-1 hypervisor | Extreme | Extreme |
| **Memory rootkit** | RAM only — no disk persistence | Rebooted away | Moderate |

**What rootkits hide:**
- Malicious processes (from `ps`, Task Manager)
- Malicious files (from `ls`, Explorer)
- Network connections (from `netstat`)
- Registry keys (from regedit)
- Loaded kernel modules (from `lsmod`)

**Detection methods:**
- Cross-view detection (compare hooked vs unhooked results)
- Boot from clean media (rootkit not loaded)
- Memory forensics (Volatility — reads raw memory structures)
- rkhunter, chkrootkit, GMER

**Deep coverage:** Session 18.

---

### 1.8 Bootkit

**WHAT:** A specialized rootkit that infects the Master Boot Record (MBR),
Volume Boot Record (VBR), or UEFI firmware — executing before the
operating system loads.

**Why bootkits are particularly dangerous:**
- Execute before OS — before any AV or security software initializes
- Survive OS reinstallation (MBR/UEFI persists independently of OS drive)
- Can subvert the entire OS boot process
- UEFI bootkits survive hard drive replacement

**Notable examples:**
- **Mebroot/Sinowal**: MBR bootkit — banking fraud (2007)
- **TDL4 (TDSS)**: bootkit — 4.5M+ infections (2010–2011)
- **LoJax**: first in-the-wild UEFI rootkit — APT28 (2018)
- **MoonBounce**: sophisticated UEFI bootkit — Winnti/APT41 (2022)

---

### 1.9 Keylogger

**WHAT:** Malware that records keystrokes typed by the user —
capturing credentials, credit card numbers, personal messages,
and anything typed on the keyboard.

**Implementation types:**

| Type | Mechanism | Stealthiness |
|---|---|---|
| **Software (API-based)** | Hooks Windows SetWindowsHookEx for keyboard events | Moderate — detectable by AV |
| **Software (kernel)** | Kernel driver intercepts keyboard driver | High |
| **Software (form grabbing)** | Hooks browser API — captures form data before submission | High — bypasses HTTPS |
| **Hardware (USB inline)** | Physical device between keyboard and computer | Very High — invisible to software |
| **Acoustic** | Records keyboard sound — ML decodes keystrokes | Very High |
| **Electromagnetic** | Captures radiation from keyboard cable | Specialist — nation-state |

**Form grabbing detail:**
Zeus (banking Trojan) used form grabbing — hooking browser submit functions
to capture credentials AFTER the user types them and BEFORE they are
encrypted by HTTPS. This bypasses TLS entirely — the data is captured
in plaintext at the browser API level.

**Deep coverage:** Session 12A.

---

### 1.10 Backdoor

**WHAT:** Malware that provides persistent unauthorized remote access
to a compromised system — bypassing normal authentication.

**Types:**
- **Bind shell**: opens a listening port — attacker connects inbound
- **Reverse shell**: victim connects outbound to attacker — bypasses firewall
- **Web shell**: PHP/ASP/JSP script on web server — HTTP-based access
- **Hardware backdoor**: firmware or hardware implant — Session 18

**Persistence mechanisms:**
- Registry Run keys
- Scheduled tasks
- Windows services
- DLL hijacking
- WMI subscriptions
- Cron jobs (Linux)
- Startup folder entries

**Deep coverage:** Sessions 12B, 13, 18.

---

### 1.11 Dropper and Downloader

**WHAT — Dropper:**
A dropper contains the malware payload EMBEDDED within itself.
When executed, it extracts and deploys (drops) the payload onto
the target system — then typically deletes itself.

    Dropper.exe → extracts → payload.exe → executes payload → dropper self-deletes

**WHAT — Downloader:**
A downloader contains NO embedded payload. When executed,
it connects to a remote URL/C2 server and downloads the actual
malware — then executes the downloaded component.

    Downloader.exe → HTTP GET https://attacker.com/payload → downloads + executes

**Why the distinction matters:**
- Droppers: entire payload is in the initial file — AV scanning can
  detect the embedded payload if unencrypted
- Downloaders: initial file is small, minimal, often clean-looking —
  payload is delivered after execution from a URL that can be
  changed or rotated (avoids static detection)
- Modern malware often chains: dropper → downloader → final payload

**Examples:**
- **Emotet** (later versions): acting as downloader delivering TrickBot,
  Ryuk ransomware
- **GuLoader**: downloader hosting encrypted payloads on legitimate
  cloud services (Google Drive, OneDrive)

---

### 1.12 Fileless Malware

**WHAT:** Malware that executes entirely in memory — no malicious
file is written to disk — evading file-based antivirus detection.

**Execution methods:**

    Method 1 — PowerShell in-memory:
      Malicious macro in Word document
              ↓
      VBA runs: PowerShell -EncodedCommand <base64>
              ↓
      PowerShell downloads shellcode from C2 (stays in memory)
              ↓
      Shellcode injected into svchost.exe
              ↓
      No file written to disk at any stage

    Method 2 — WMI persistence:
      Malware registers WMI event subscription:
      ON [event] DO EXECUTE [PowerShell command]
      Command stored in WMI repository (not a standard file)
      AV scans disk — finds nothing

    Method 3 — Registry persistence:
      Malicious PowerShell script stored in registry value
      Encoded: HKCU\...\Run = "powershell -EncodedCommand <payload>"

**Why it evades traditional AV:**
AV primarily scans FILES on disk. If no malicious file exists on disk,
signature-based scanning finds nothing. Only AMSI (scans scripts
before execution), EDR (behavioral monitoring), and memory forensics
detect fileless threats.

**Traces fileless malware DOES leave:**
- Windows Event Log ID 4104 (PowerShell Script Block Logging)
- Network connections to C2
- WMI repository modifications
- Registry modifications
- Process memory (volatile — lost on reboot)
- AMSI scan logs

**Deep coverage:** Session 13 (Section 3.8).

---

### 1.13 Logic Bomb

**WHAT:** Malicious code embedded in a legitimate or malicious program
that executes a destructive payload when a specific trigger condition
is met — and remains dormant until triggered.

**Trigger types:**
- Specific date or time (time bomb)
- Specific user login (or absence of login — dead man's switch)
- File presence or absence
- Network connectivity event
- Counter value reached

**Classic scenario:**

    Disgruntled employee embeds logic bomb in payroll system:
    IF current_date == '2024-01-01' AND employee_id NOT IN active_employees:
        DELETE FROM employee_records
        FORMAT C:\
    END IF

    Employee is fired → removed from active_employees list
    On new year's day → logic bomb triggers → destructive payload executes

**Detection challenges:**
- Logic bomb may appear in legitimate code — hard to distinguish from
  normal conditional logic during code review
- Dormant period means AV behavioral analysis may not trigger it
- Static analysis of the condition may reveal suspicious triggers

---

### 1.14 Bot / Zombie

**WHAT:** A compromised machine running bot malware that is remotely
controlled by a botnet operator (bot herder) — executing commands
without the machine owner's knowledge.

**Bot capabilities:**
- DDoS participation
- Spam email relay
- Credential stuffing
- Cryptomining
- Click fraud
- Proxy routing
- Ransomware delivery
- Lateral movement

**Deep coverage:** Session 16A (Section 4).

---

### 1.15 Wiper / Destructive Malware

**WHAT:** Malware designed to PERMANENTLY DESTROY data and render
systems inoperable — with no recovery mechanism and no ransom demand.
Typically deployed in cyberwarfare and nation-state attacks.

**Destruction methods:**
- Overwrite file contents with random data or zeros
- Delete or corrupt the MBR — system cannot boot
- Overwrite partition tables
- Destroy UEFI firmware (bricking)
- Corrupt RAID configurations
- Delete backups and shadow copies

**Distinguished from ransomware:**

| Property | Ransomware | Wiper |
|---|---|---|
| **Goal** | Financial gain | Destruction / disruption |
| **Encryption** | ✅ Reversible with key | ❌ Irreversible overwrite |
| **Recovery possible** | ✅ With key or backup | ❌ No recovery |
| **Ransom demanded** | ✅ Yes | ❌ No |
| **Attribution** | Cybercriminal | Nation-state / hacktivist |

**Notable examples:**
- **Shamoon (Disttrack)**: destroyed 35,000 Saudi Aramco workstations (2012)
- **NotPetya (2017)**: disguised as ransomware — actual wiper —
  caused $10B+ damage globally — attributed to Sandworm (Russia)
- **HermeticWiper**: deployed against Ukraine hours before
  Russian invasion (February 2022)
- **WhisperGate**: Ukraine-targeted wiper (January 2022)

> [!IMPORTANT]
> NotPetya is the most important wiper case study for exams.
> It appeared to be ransomware (Petya variant) but the "ransom"
> payment mechanism was non-functional — it was pure destruction.
> $10 billion in damages. Maersk, FedEx, Merck, hospitals affected.
> Attributed to Russian GRU Sandworm unit by US/UK governments.

---

## Section 2 — Malicious Code Families

### 2.1 What Is a Malware Family

**WHAT:**
A malware family is a group of related malware samples that share
common code, architecture, infrastructure, or campaign origin —
despite having different hashes (due to recompilation, packing, or
minor modifications).

**Family identification criteria:**
- Shared code sections (detected by YARA rules)
- Common C2 infrastructure
- Same encryption routines or custom algorithms
- Same persistence mechanisms
- Same obfuscation/packing techniques
- Attribution to same threat actor

**Naming conventions:**
Vendors independently name families — different AV vendors may
call the same malware by different names (see E4 — Malware Naming).

---

### 2.2 Banking Trojans

Banking Trojans are the most financially motivated malware family —
specifically targeting online banking credentials and financial fraud.

| Family | Active Period | Notable Techniques |
|---|---|---|
| **Zeus (Zbot)** | 2007–present | Form grabbing, Man-in-the-Browser, config file |
| **SpyEye** | 2009–2012 | Zeus competitor — merged with Zeus code |
| **Dridex** | 2012–present | Macro delivery, P2P C2, form grabbing |
| **TrickBot** | 2016–2022 | Modular, credential theft, lateral movement, Ryuk delivery |
| **Qakbot (QBot)** | 2007–2023 | Email thread hijacking, ransomware delivery |
| **IcedID (BokBot)** | 2017–present | Webinject, ransomware delivery |
| **Emotet** | 2014–present | Initially banking Trojan → evolved to dropper/loader |

**Zeus (Zbot) — Key Facts:**
- Source code leaked in 2011 → spawned dozens of variants
- Used Man-in-the-Browser attacks — hooking Firefox/IE API
- Config file defined which banking sites to target
- Form grabbing bypassed HTTPS
- Estimated $100M+ in financial fraud before takedown
- Zeus + SpyEye merger → Gameover Zeus (P2P botnet)

---

### 2.3 RAT Families

Remote Access Trojans provide full remote control of compromised systems.

| RAT | Origin | Notable Use |
|---|---|---|
| **Back Orifice** | Cult of the Dead Cow (1998) | First widely known RAT — Windows |
| **Sub7 (SubSeven)** | 1999 | Script kiddie RAT — 1990s/2000s |
| **Poison Ivy** | 2005 | APT campaigns — Chinese espionage |
| **DarkComet** | 2008–2012 | Syrian government use against activists |
| **njRAT (Bladabindi)** | 2013 | Middle East/North Africa APT |
| **AsyncRAT** | 2019–present | Open source — active 2024–2025 |
| **QuasarRAT** | 2014–present | Open source .NET — GitHub hosted |
| **Cobalt Strike (Beacon)** | 2012–present | Commercial C2 — red team + APT |
| **Meterpreter** | Metasploit | In-memory — extensible — pentest standard |

---

### 2.4 Ransomware Families

| Family | Year | Notable Features |
|---|---|---|
| **CryptoLocker** | 2013 | First major modern ransomware — RSA-2048 |
| **WannaCry** | 2017 | EternalBlue self-propagation — NHS impact |
| **Petya / NotPetya** | 2016/2017 | MBR encryption / wiper disguised as ransomware |
| **Ryuk** | 2018–2021 | Manual deployment — hospitals, governments |
| **REvil (Sodinokibi)** | 2019–2022 | RaaS — $70M Kaseya demand |
| **LockBit** | 2019–present | Most active RaaS — LockBit 3.0 (2022) |
| **BlackCat (ALPHV)** | 2021–2024 | Rust-based — cross-platform — triple extortion |
| **Clop** | 2019–present | Mass exploitation (MOVEit, GoAnywhere zero-days) |
| **Conti** | 2020–2022 | RaaS — healthcare focus — internal docs leaked |
| **Akira** | 2023–present | Targets VMware ESXi — double extortion |

---

### 2.5 Infostealer Families

Infostealers focus on credential and session data theft — sold on dark web markets.

| Stealer | Active | Targets |
|---|---|---|
| **RedLine** | 2020–present | Browser credentials, crypto wallets, session cookies |
| **Raccoon Stealer** | 2019–present | Browser data, email clients, FTP clients |
| **Vidar** | 2018–present | Browser data, Telegram, 2FA apps |
| **Lumma Stealer** | 2022–present | Browser cookies, extensions, crypto |
| **AZORult** | 2016–2019 | Credentials, crypto wallets |
| **FormBook** | 2016–present | Form grabbing, keylogging |
| **Agent Tesla** | 2014–present | Keylogging, credentials, clipboard |

**How infostealers operate:**

    Delivery (phishing, cracked software, malvertising)
            ↓
    Execute on victim machine
            ↓
    Locate browser profile directories:
      Chrome: %APPDATA%\Local\Google\Chrome\User Data\Default\
      Firefox: %APPDATA%\Roaming\Mozilla\Firefox\Profiles\
            ↓
    Decrypt browser credential database (SQLite)
    Decrypt cookies (using Windows DPAPI + local state key)
            ↓
    Collect: credentials, session cookies, autofill, crypto wallets
            ↓
    Archive + exfiltrate to attacker's server or Telegram bot
            ↓
    Self-delete (remove forensic artifacts)

---

### 2.6 Botnet Malware Families

| Botnet | Peak | Method | Notable Use |
|---|---|---|---|
| **Conficker** | 2008–2012 | MS08-067 RPC exploit | 9–15M infections — DGA C2 |
| **Zeus/GameOver** | 2011–2014 | Banking Trojan recruitment | P2P botnet — DGA |
| **Mirai** | 2016–present | IoT default credentials | 1.2 Tbps Dyn DDoS |
| **Emotet** | 2014–2021 | Email phishing | Loader for TrickBot/Ryuk — takedown Jan 2021 |
| **Necurs** | 2012–2020 | Spam distribution | 9M bots — Dridex/Locky delivery |
| **Mēris** | 2021 | MikroTik router exploit | 21.8M RPS record DDoS |

---

### 2.7 Rootkit Families

| Rootkit | Type | Notable Features |
|---|---|---|
| **NTRootkit** | User-mode (Windows) | First publicly released Windows rootkit |
| **Hacker Defender** | User-mode (Windows) | Classic 2000s rootkit — API hooking |
| **FU Rootkit** | Kernel-mode (Windows) | DKOM (Direct Kernel Object Manipulation) |
| **TDL4 (TDSS)** | Bootkit | MBR infection — 4.5M bots |
| **Necurs rootkit** | Kernel + bootkit | Protected Necurs botnet communications |
| **LoJax** | UEFI | First UEFI rootkit in the wild — APT28 |
| **CosmicStrand** | UEFI | Persistent UEFI implant — Chinese APT |

---

## Section 3 — Latest Trends in Malware

### 3.1 Ransomware-as-a-Service (RaaS)

**WHAT:**
RaaS is the commercialization of ransomware — modeled on Software-
as-a-Service — where ransomware operators provide fully managed
ransomware infrastructure (encryptor, C2, payment portal, negotiation
support) to affiliates who handle target selection and deployment.

**RaaS business model:**

    Ransomware Operators (Developers):
      Build and maintain ransomware code
      Provide C2 infrastructure
      Manage payment portals
      Handle victim decryption after payment
      Provide affiliate dashboard
              ↓
    Affiliates (Attackers):
      Select and compromise targets
      Deploy ransomware
      Negotiate ransoms
      Receive 70–80% of ransom proceeds
      Operators receive 20–30% royalty

**Why RaaS democratized ransomware:**
Technical barrier to entry dropped to near zero. Affiliates need only
know how to gain initial access (phishing, RDP brute force, exploiting
known CVEs) — all technical ransomware infrastructure is provided.
This explains the explosive growth in ransomware attacks 2019–2025.

**Notable RaaS operations:**
LockBit (most active 2022–2024), REvil/Sodinokibi, BlackCat/ALPHV,
Conti, Cl0p, Hive, BlackBasta, Akira.

---

### 3.2 Supply Chain Attacks

**WHAT:**
Supply chain attacks compromise a target INDIRECTLY by first
compromising a trusted vendor, software provider, or hardware
supplier — then using that trust relationship to reach the
intended victims at scale.

**Why supply chain attacks are devastating:**
- A single compromise of a widely-used vendor reaches thousands of customers
- Victims trust and install updates/software from the compromised vendor
- Traditional perimeter defenses do not protect against trusted supplier compromise

**Key examples:**

    SolarWinds SUNBURST (2020):
      Attacker (APT29 — Russia): compromised SolarWinds build system
      Malicious code inserted into SolarWinds Orion update package
      ~18,000 organizations installed the trojanized update
      Including: US Treasury, State Dept, DoD, FireEye, Microsoft
      Impact: nation-state espionage campaign — 9 months undetected

    3CX Supply Chain (2023):
      North Korean Lazarus Group compromised 3CX VoIP software
      Trojanized 3CX desktop application
      Delivered via 3CX's own update mechanism
      Notably: 3CX was itself infected via a prior supply chain attack
      (compromised X_TRADER financial software)

    Polyfill.io (2024):
      CDN domain purchased by Chinese company
      ~100,000 websites using polyfill.js served malware to visitors

---

### 3.3 Living-off-the-Land (LotL)

**WHAT:**
LotL attacks use legitimate, pre-installed OS tools (LOLBins — Living
off the Land Binaries) for malicious purposes — avoiding dropping
custom malware files that AV might detect.

**Common LOLBins and abuse:**

| Binary | Malicious Use |
|---|---|
| powershell.exe | Download/execute payloads, AMSI bypass |
| certutil.exe | Download files, base64 decode malware |
| mshta.exe | Execute remote HTA scripts |
| regsvr32.exe | Squiblydoo — execute remote scriptlets |
| wmic.exe | Lateral movement, WMI subscriptions |
| msiexec.exe | Install remote MSI payloads |
| rundll32.exe | Execute malicious DLLs |
| bitsadmin.exe | Background download of malware |

**Why LotL is difficult to detect:**
These are LEGITIMATE tools used by administrators daily. Blocking
them breaks legitimate functionality. Detection requires behavioral
context — PowerShell downloading from an unusual domain at 3 AM
from a machine that never uses PowerShell is suspicious. Normal
PowerShell usage is not.

**Detection:** PowerShell Script Block Logging (Event 4104),
AMSI, EDR behavioral rules for suspicious LOLBin usage patterns.

**Deep coverage:** Session 13 (Section 3.7).

---

### 3.4 AI-Generated and AI-Enhanced Malware

**Latest developments (2023–2026):**

**AI-generated phishing (operational):**
LLMs generate perfectly grammatical, contextually aware phishing
emails in any language — eliminating the spelling/grammar mistakes
that previously helped users identify phishing. Success rates
significantly higher than traditional templates.

**WormGPT / FraudGPT (2023):**
Uncensored LLMs sold on dark web — trained to assist with malware
creation, phishing email writing, and vulnerability research without
safety guardrails.

**AI-generated polymorphic malware (2024–2025):**
Tools generate functionally identical but structurally unique malware
variants on demand — each with different obfuscation, encoding, and
instruction sequences. Defeats signature-based detection at scale
with zero manual effort. Every generated sample has a unique hash.

**AI-assisted sandbox evasion (2025):**
ML models trained on sandbox behavioral profiles generate timing
patterns and user simulation signals that fool behavior-based
sandboxes into classifying malware as benign.

**AMSI bypass generation (2024):**
LLM-assisted tools automatically generate novel AMSI bypass scripts
by mutating known bypass techniques until the AMSI hook fails to fire —
reducing AMSI bypass from expert skill to automated trial-and-error.

---

### 3.5 Infostealer + Session Cookie Theft

**The dominant credential theft method in 2023–2026:**
Modern infostealers specifically target browser-stored session cookies —
post-authentication tokens that bypass MFA completely.

**Why session cookies defeat MFA:**
MFA protects the LOGIN process. A stolen session cookie represents
ALREADY AUTHENTICATED access — presenting it to the server gives
access without re-authentication. MFA is irrelevant.

**AiTM (Adversary-in-the-Middle) phishing kits:**
Evilginx2, Modlishka — act as reverse proxies — victim authenticates
(including MFA) through the AiTM proxy — proxy captures the
authenticated session cookie — attacker uses cookie for persistent access.

**Dark web markets:**
Genesis Market (seized FBI 2023), Russian Market — sell complete
browser "fingerprint bundles": cookies + user agent + screen resolution +
installed plugins — making stolen sessions indistinguishable from
the real user's browser.

---

### 3.6 Mobile Malware Trends

**Android:**
- Open ecosystem — sideloading — higher malware risk
- Malicious apps in Play Store (despite scanning)
- Banking Trojans with overlay attacks (fake login screens)
- SMS-based 2FA interception (OTP-stealing malware)
- Pegasus-class spyware on rooted devices

**iOS:**
- Closed ecosystem — limited malware due to App Store review
- Zero-click exploits (Pegasus — no user interaction required)
- MDM (Mobile Device Management) profile abuse
- Jailbreak-based malware

**Notable mobile malware:**
- **FluBot**: Android banking Trojan — SMS phishing delivery (2020–2022)
- **SharkBot**: Android banking Trojan — accessibility service abuse
- **Joker**: adware/spyware — repeated Play Store appearances
- **Pegasus**: iOS/Android — state-sponsored — zero-click exploitation

---

### 3.7 IoT and OT/ICS Malware

**IoT Malware:**
- Mirai and successors: exploit default credentials on cameras, routers, DVRs
- Primarily recruited for DDoS botnets
- Limited malware capabilities due to minimal-resource embedded OS
- Growing attack surface: 15–20 billion IoT devices estimated 2025

**OT/ICS (Operational Technology / Industrial Control Systems) Malware:**
Targets industrial systems — power grids, water treatment, manufacturing.

| Malware | Year | Target | Impact |
|---|---|---|---|
| **Stuxnet** | 2010 | Iranian nuclear centrifuges | Physical destruction of ~1,000 centrifuges |
| **Industroyer/Crashoverride** | 2016 | Ukrainian power grid | Kiev blackout — 1 hour |
| **TRITON/TRISIS** | 2017 | Saudi oil refinery Safety Instrumented Systems | Attempted physical safety system sabotage |
| **Industroyer2** | 2022 | Ukrainian power substation | Prevented before execution |
| **FrostyGoop** | 2024 | Ukrainian district heating Modbus devices | Heating disruption in winter |

**Why OT/ICS malware is uniquely dangerous:**
ICS/SCADA systems control physical processes — power generation,
water treatment, nuclear reactors, gas pipelines. Malware-induced
failure can cause physical damage, environmental hazard, and
loss of human life — not just data loss.

---

### 3.8 Double and Triple Extortion Ransomware

**Single extortion (traditional):**
Encrypt files → demand payment for decryption key.

**Double extortion (Maze — 2019, now universal):**
Exfiltrate data BEFORE encrypting → demand payment for:
(1) Decryption key + (2) Not publishing stolen data on leak site.

Victim now has TWO reasons to pay: restore operations + avoid
reputational/regulatory damage from data publication.

**Triple extortion:**
Single + Double + Third pressure:
(3) DDoS attack on victim's public website (operational disruption)
OR notify victim's customers/partners that their data was stolen
OR contact victim's regulators directly (GDPR, DPDPA violations)

**Leak sites:**
Most major RaaS groups operate ".onion" leak sites on Tor —
"name and shame" portals listing victims who have not paid,
with countdown timers and sample data as proof.

**Examples:** LockBit Leak Site, ALPHV/BlackCat Leak Site,
Cl0p Mass Exfil (MOVEit — 2023 — data published without ransom demand)

---

## Section 4 — Malware Analysis Overview

### 4.1 Goals of Malware Analysis

**Primary goals:**

| Goal | Description | Enables |
|---|---|---|
| **Understand behaviour** | What does the malware do? File changes, network calls, registry? | Incident response, scope assessment |
| **Extract IOCs** | Hashes, C2 IPs/domains, registry keys, file paths | Threat hunting, detection rules |
| **Determine capabilities** | What can it do? Keylog, ransomware, lateral movement? | Impact assessment |
| **Attribution** | Who wrote it? Which threat actor? Which campaign? | Intelligence, law enforcement |
| **Develop signatures** | Create AV/YARA/SIEM detection rules | Prevent future infections |
| **Find decryption keys** | Recover encryption keys from ransomware (if possible) | Victim recovery |

---

### 4.2 Analysis Environment Setup

**Critical requirement: ISOLATION**

A malware analysis environment MUST be isolated from:
- Production networks
- The internet (in most cases — some analysis requires limited internet)
- Other analysis VMs (malware may spread)

**Standard setup:**

    Physical Host (clean OS)
            ↓
    Hypervisor (VMware Workstation, VirtualBox, or Hyper-V)
            ↓
    Isolated Virtual Network (host-only or NAT with monitoring)
            ↓
    Analysis VM (Windows 10 — fresh snapshot):
      - Snapshots taken before each analysis
      - INetSim or FakeNet-NG: simulate internet services (DNS, HTTP, SMTP)
      - Analysis tools pre-installed
      - AV disabled (would interfere with execution)
            ↓
    Monitoring VM (REMnux or SIFT) on same isolated network:
      - Wireshark: capture all network traffic from analysis VM
      - Inetsim: respond to DNS/HTTP/SMTP queries
      - Collect logs and artifacts

**Why snapshots are essential:**
After each analysis, REVERT to pre-analysis snapshot — clean state
for next sample. If malware escapes detection and infects the analysis
VM, reverting restores clean state in seconds.

---

### 4.3 Analysis Workflow

    STEP 1 — Safe sample handling:
      Receive sample in password-protected ZIP (password: "infected" or "malware")
      Never double-click a sample outside an isolated environment
      Calculate hash immediately for identification

    STEP 2 — Static analysis first:
      Examine file without executing
      File type, hash, strings, imports, packer detection, disassembly
      Objective: understand as much as possible without risk

    STEP 3 — Baseline snapshot:
      Take clean VM snapshot
      Record: running processes, open ports, registry state, file system state
      Tools: Regshot (registry baseline), Wireshark (start capture)

    STEP 4 — Dynamic analysis:
      Execute malware in isolated VM with monitoring active
      Observe: process creation, file changes, registry changes,
               network connections, API calls

    STEP 5 — Memory analysis:
      Dump process memory for injected code analysis
      Use Volatility to examine memory artifacts

    STEP 6 — IOC extraction:
      Compile all identified indicators
      C2 IPs/domains, file hashes, registry keys, mutex names, file paths

    STEP 7 — Reporting:
      Document behaviour, capabilities, IOCs
      Develop YARA rules and SIEM detection logic

---

## Section 5 — Static Malware Analysis

### 5.1 What Is Static Analysis

**WHAT:**
Static analysis examines a malware sample **without executing it** —
analyzing the file's structure, content, code, and metadata to
understand its purpose and behaviour.

**Advantages:**
- Safe — no execution risk
- Reproducible — same file produces same results
- Complete — can analyze all code paths (including rarely executed ones)
- No anti-analysis evasion (anti-VM, anti-debug don't apply)

**Limitations:**
- Packed/encrypted malware reveals very little
- Cannot observe runtime behaviour (network connections, process injection)
- Complex obfuscation can make code analysis extremely difficult
- Requires significant expertise for assembly-level analysis

---

### 5.2 File Identification

**Purpose:** Determine true file type — regardless of extension.

**Magic bytes (file signatures):**
The first few bytes of a file identify its true type — independent of
the extension the attacker may have changed.

| File Type | Magic Bytes (Hex) | ASCII |
|---|---|---|
| PE executable (.exe, .dll) | 4D 5A | MZ |
| PDF | 25 50 44 46 | %PDF |
| ZIP | 50 4B 03 04 | PK.. |
| JPEG | FF D8 FF | ... |
| PNG | 89 50 4E 47 | .PNG |
| ELF (Linux executable) | 7F 45 4C 46 | .ELF |
| Office DOCX/XLSX | 50 4B 03 04 | PK.. (ZIP-based) |

**Commands:**

    # Linux file command
    file suspicious_sample

    # Output example:
    suspicious_sample: PE32 executable (GUI) Intel 80386, for MS Windows, UPX compressed

    # xxd — view hex dump
    xxd suspicious_sample | head -5

**ExeinfoPE / PEiD:**
Windows tools that identify PE file type, compiler used, and packer
detected — more detailed than `file` command for Windows executables.

---

### 5.3 Hashing

**Purpose:** Uniquely identify a specific file version — enable
lookups in threat intelligence databases.

**Hash commands:**

    # Windows PowerShell
    Get-FileHash malware.exe -Algorithm SHA256
    Get-FileHash malware.exe -Algorithm MD5

    # Linux
    sha256sum malware.exe
    md5sum malware.exe

    # CertUtil (Windows)
    certutil -hashfile malware.exe SHA256

**VirusTotal lookup:**
Submit SHA-256 hash to VirusTotal → 70+ AV engines check it.
Known malware: immediate positive results with family name.
Unknown malware (zero-day or custom): "clean" result — but clean ≠ safe.

**Fuzzy hashing (ssdeep):**
Standard cryptographic hashes change completely with any file modification.
ssdeep generates a similarity hash — two variants from the same family
may have similar ssdeep hashes even if SHA-256 differs completely.
Useful for: finding related samples, tracking family evolution.

    ssdeep -r malware_samples/ > hashes.txt
    ssdeep -m hashes.txt unknown_sample.exe

---

### 5.4 String Extraction

**Purpose:** Extract readable text from the binary — often reveals
C2 URLs, IP addresses, registry keys, file paths, error messages,
and embedded credentials.

**Commands:**

    # Linux strings command
    strings malware.exe

    # Minimum string length 8 characters
    strings -n 8 malware.exe

    # Both ASCII and Unicode strings
    strings -a -el malware.exe

    # FLOSS (FireEye Labs Obfuscated String Solver)
    floss malware.exe
    # Extracts: plain strings + decoded obfuscated strings
    # Finds strings that simple 'strings' misses (encoded/XOR'd)

**What strings typically reveal:**

    Registry keys:
      SOFTWARE\Microsoft\Windows\CurrentVersion\Run

    File paths:
      C:\Users\%USERNAME%\AppData\Roaming\svchost.exe

    URLs / C2 infrastructure:
      http://192.168.1.100:4444/beacon
      https://update.legitimate-looking-domain.com/check

    Mutex names:
      Global\{GUID-like-mutex-name}
      (mutex prevents double-infection of same host)

    Error messages:
      "Failed to connect to C2"
      "Encryption complete"

    Encryption artifacts:
      Base64 encoded strings
      Hardcoded XOR keys
      RSA public key blocks (-----BEGIN PUBLIC KEY-----)

> [!TIP]
> **FLOSS** (FLARE Obfuscated String Solver by Mandiant/Google)
> is significantly more powerful than `strings` — it automatically
> decodes common string obfuscation techniques including XOR encoding,
> stack strings, and simple ciphers — extracting strings that
> `strings` alone would miss.

---

### 5.5 PE File Analysis

**Purpose:** Analyze the internal structure of Windows PE
(Portable Executable) files to understand compiler info,
section characteristics, embedded resources, and timestamps.

**Key PE header fields:**

| Field | Location | Analysis Value |
|---|---|---|
| **TimeDateStamp** | PE header | Compilation time (may be spoofed) |
| **Machine** | PE header | Target architecture (x86, x64, ARM) |
| **NumberOfSections** | PE header | Section count (unusual count → suspicious) |
| **Subsystem** | Optional header | GUI vs Console vs driver |
| **Characteristics** | Optional header | DLL? Stripped of symbols? |

**Section analysis:**

    Normal PE sections:
      .text  — executable code
      .data  — initialized data
      .rdata — read-only data (strings, constants)
      .rsrc  — embedded resources
      .reloc — relocation table

    Suspicious indicators:
      Section with high entropy (>7.0) → encrypted/packed content
      Executable AND writable section → possible self-modifying code
      Non-standard section names (.UPX0, .UPX1 → UPX packer)
      Very small .text section + large .data → unpacking stub pattern

**Tools:**

    PEview — lightweight PE header viewer
    PE-bear — interactive PE analysis
    CFF Explorer — detailed PE editing and viewing
    pestudio — malware-focused PE analysis
    dumpbin (Visual Studio) — command-line PE analysis
      dumpbin /headers malware.exe
      dumpbin /imports malware.exe

---

### 5.6 Packer Detection

**Purpose:** Identify if malware is packed or encrypted — and
which packer was used — to determine if unpacking is needed
before deeper analysis.

**Entropy analysis:**
Packed/encrypted sections have HIGH ENTROPY (close to 8.0) —
compressed or encrypted data approaches maximum randomness.
Normal executable code has entropy of ~5.5–6.5.

**Tools:**

    # pestudio — shows section entropy graphically
    # Detect It Easy (DIE) — identifies packers and compilers
    # ExeinfoPE — packer identification
    # PEiD — classic packer detector

    # Python entropy calculation
    import math
    def entropy(data):
        if not data: return 0
        freq = [data.count(chr(i)) for i in range(256)]
        return -sum(f/len(data) * math.log2(f/len(data))
                    for f in freq if f)

**Common packers:**
UPX, MPRESS, ASPack, Themida, VMProtect, custom packers.

**Unpacking:**
- Known packers (UPX): `upx -d packed_malware.exe`
- Unknown/custom packers: run in sandbox → dump unpacked code
  from memory using Process Hacker or OllyDumpEx
- Manual unpacking: debug until OEP (Original Entry Point), dump

---

### 5.7 Import / Export Analysis

**Purpose:** The Import Address Table (IAT) reveals which Windows
API functions the malware uses — revealing its capabilities
without executing it.

**Suspicious API imports by capability:**

| Capability | Windows APIs Imported |
|---|---|
| **Process injection** | VirtualAllocEx, WriteProcessMemory, CreateRemoteThread |
| **Privilege escalation** | AdjustTokenPrivileges, OpenProcessToken |
| **File operations** | CreateFile, WriteFile, DeleteFile, MoveFile |
| **Registry persistence** | RegOpenKey, RegSetValue, RegCreateKey |
| **Network communication** | WSAStartup, connect, send, recv, InternetOpen |
| **Keylogging** | SetWindowsHookEx (WH_KEYBOARD), GetAsyncKeyState |
| **Screenshot** | BitBlt, GetDC, CreateCompatibleBitmap |
| **Anti-analysis** | IsDebuggerPresent, CheckRemoteDebuggerPresent, GetTickCount |
| **Crypto operations** | CryptEncrypt, CryptGenKey, CryptAcquireContext |
| **Service installation** | OpenSCManager, CreateService, StartService |

**Commands:**

    # Linux objdump
    objdump -d malware.exe | grep "call"

    # dumpbin
    dumpbin /imports malware.exe

    # pestudio — visual IAT analysis with threat scoring

**Import obfuscation:**
Sophisticated malware resolves API imports dynamically at runtime:
    LoadLibrary("kernel32.dll")
    GetProcAddress(kernel32, "VirtualAlloc")
This hides capabilities from static IAT analysis — dynamic analysis needed.

---

### 5.8 Disassembly and Decompilation

**Disassembly:** Convert binary machine code → assembly language
**Decompilation:** Convert binary machine code → pseudo-C/C++ code

**Tools:**

| Tool | Type | Notes |
|---|---|---|
| **IDA Pro** | Disassembler + decompiler | Industry standard — expensive — Hex-Rays decompiler |
| **Ghidra** | Disassembler + decompiler | NSA open-source — free — excellent decompiler |
| **Binary Ninja** | Disassembler + decompiler | Modern API — scripting focused |
| **Radare2** | Disassembler | Open-source — command-line — steep learning curve |
| **x64dbg / OllyDbg** | Debugger | Dynamic disassembly — step through execution |

**Key analysis tasks:**

    1. Identify main function — entry point analysis
    2. Trace execution flow — understand control flow graph
    3. Identify encryption routines — look for XOR loops, AES operations
    4. Find C2 communication — look for socket/HTTP functions
    5. Locate persistence mechanisms — registry/file write with Run key paths
    6. Identify anti-analysis checks — IsDebuggerPresent, CPUID

---

### 5.9 YARA Rules

**WHAT:**
YARA is a pattern matching tool used to identify and classify malware
samples based on STATIC CHARACTERISTICS — byte patterns, strings,
PE structure, and boolean conditions.

**YARA rule structure:**

    rule MalwareFamilyName {
        meta:
            description = "Detects Example Banking Trojan"
            author = "Analyst Name"
            date = "2025-01-15"
            hash = "sha256:abcdef..."

        strings:
            $str1 = "C:\\Users\\%USERNAME%\\AppData\\evil.exe"
            $str2 = "http://c2.attacker.com/beacon"
            $str3 = { 4D 5A 90 00 03 00 00 00 }  // MZ header bytes
            $xor_key = { 41 42 43 }               // hex byte pattern
            $re1 = /[A-Za-z0-9+/]{20,}={0,2}/    // base64 regex

        condition:
            uint16(0) == 0x5A4D  // MZ header check (PE file)
            and filesize < 1MB
            and 2 of ($str*)
            or $str2
    }

**Running YARA:**

    # Scan single file
    yara rule.yar malware.exe

    # Scan directory recursively
    yara -r rule.yar /path/to/samples/

    # Scan running processes
    yara -p rule.yar

**YARA rule repositories:**
- **YARA-Rules** (GitHub): community-maintained public rules
- **Florian Roth's signature-base**: high-quality APT detection rules
- **CAPE Sandbox**: auto-generates YARA from dynamic analysis
- **MalwareBazaar**: samples with community YARA rules

---

### 5.10 Static Analysis Tools Reference

| Tool | Platform | Primary Use |
|---|---|---|
| **strings** | Linux | Extract ASCII/Unicode strings from binary |
| **FLOSS** | Cross-platform | Extract + decode obfuscated strings |
| **file** | Linux | Identify file type via magic bytes |
| **xxd / hexdump** | Linux | Hex dump for manual inspection |
| **pestudio** | Windows | Malware-focused PE analysis — threat scoring |
| **PEview / PE-bear** | Windows | PE header structure visualization |
| **DIE (Detect It Easy)** | Cross-platform | Packer/compiler identification |
| **ExeinfoPE** | Windows | Packer detection + PE info |
| **CFF Explorer** | Windows | PE editing and detailed analysis |
| **dumpbin** | Windows | Command-line PE import/export analysis |
| **ssdeep** | Cross-platform | Fuzzy hash for sample similarity |
| **IDA Pro** | Cross-platform | Professional disassembler + decompiler |
| **Ghidra** | Cross-platform | NSA open-source disassembler + decompiler |
| **YARA** | Cross-platform | Pattern-based malware classification |
| **VirusTotal** | Web | Multi-AV + community intelligence lookup |
| **MalwareBazaar** | Web | Sample repository + hash lookup |

---

## Section 6 — Dynamic Malware Analysis

### 6.1 What Is Dynamic Analysis

**WHAT:**
Dynamic analysis executes the malware in a CONTROLLED, ISOLATED
environment and monitors its behaviour in real time — observing
all actions it takes: files created, registry changes, network
connections, processes spawned, API calls made.

**Advantages over static analysis:**
- Bypasses obfuscation — malware must unpack itself to run
- Reveals actual runtime behaviour — not just code paths
- Captures network C2 communications
- Works even when code is impossible to statically analyze
- Reveals anti-analysis triggers (then analyst can bypass them)

**Limitations:**
- Execution risk — requires isolated environment
- Time-limited — sandboxes typically run 2–5 minutes
- Anti-analysis evasion: malware may detect sandbox and not execute
- Non-deterministic — malware may behave differently on re-execution
- C2-dependent malware may not fully execute if C2 is unavailable

---

### 6.2 Sandbox Analysis

**WHAT:**
A sandbox is an isolated virtual environment that automatically
executes malware, monitors all activity, and produces a structured
behaviour report — without requiring manual analyst interaction.

**Online sandboxes:**

| Sandbox | URL | Features |
|---|---|---|
| **Any.Run** | any.run | Interactive — analyst can click in VM — real-time |
| **Joe Sandbox** | joesandbox.com | Deep analysis — anti-evasion technology |
| **Cuckoo Sandbox** | Open-source | Self-hosted — customizable — most widely used |
| **Hybrid Analysis** | hybrid-analysis.com | Free — Payload Security powered |
| **VirusTotal** | virustotal.com | Basic dynamic + community analysis |
| **CAPE Sandbox** | Open-source | Cuckoo fork — config extraction — YARA generation |

**Cuckoo Sandbox — key components:**

    Host Machine (analysis controller)
            ↓
    Guest VM (Windows — with Cuckoo agent)
            ↓
    Malware executed in Guest VM
    Agent monitors and reports all activity to Host
            ↓
    Report generated:
      - Process tree
      - File system operations
      - Registry operations
      - Network connections
      - API calls log
      - Screenshots
      - Memory dumps
      - PCAP file

**Sandbox evasion awareness:**
Sophisticated malware detects sandbox environments (VM artifacts,
analysis tool processes, timing discrepancies) and does not execute
its payload. Analyst must be aware of this and may need to modify
the VM environment to defeat evasion (see E2).

---

### 6.3 Process Monitoring

**Purpose:** Observe what processes malware creates, modifies,
or injects into — revealing execution chain and lateral movement.

**Key observations:**
- Parent-child process relationships (abnormal chains)
- Process injection (malicious code in svchost.exe)
- Process hollowing (legitimate process replaced with malware)
- Child processes spawned (cmd.exe, powershell.exe from Word)

**Tools:**

    Process Monitor (Procmon) — Sysinternals:
      Real-time file, registry, network, process activity
      Filters to show only malware-relevant activity:
        Process Name contains malware.exe
        Operation contains WriteFile
        Path contains AppData\Roaming

    Process Explorer — Sysinternals:
      Shows full process tree
      Highlights injected DLLs (different color)
      Shows process strings (can reveal malware paths)
      VirusTotal integration — submit hashes directly

    Process Hacker:
      Open-source alternative to Process Explorer
      Memory dump capability — dump injected code
      Network connections per process

**Suspicious process indicators:**

    Normal: Word.exe → (no children)
    Malicious: Word.exe → cmd.exe → powershell.exe → wscript.exe

    Normal: svchost.exe (parent: services.exe)
    Malicious: svchost.exe (parent: malware.exe) → injection

---

### 6.4 File System Monitoring

**Purpose:** Track all file system changes made by malware —
what files are created, modified, deleted, or renamed.

**Key observations:**
- Malware dropped to disk (where? what name?)
- Configuration files created
- Files encrypted (ransomware indicator)
- Log files deleted (anti-forensics)
- Autostart entries created

**Tools:**

    Process Monitor (Procmon) — filter by Operation: WriteFile
    WinMerge — compare directory snapshots before/after execution
    Regshot — can compare both file system AND registry

**Typical malware file system activity:**

    Create: C:\Users\User\AppData\Roaming\microsoft\svchost32.exe
    Create: C:\ProgramData\{GUID}\config.bin
    Modify: C:\Windows\System32\drivers\etc\hosts (hosts file poisoning)
    Delete: C:\Users\User\Documents\*.docx (ransomware encryption)
    Create: C:\Users\User\Documents\*.LOCKED (ransomware encrypted)
    Create: C:\Users\User\Desktop\README_DECRYPT.txt (ransom note)

---

### 6.5 Registry Monitoring

**Purpose:** Track registry changes — most commonly persistence
mechanisms and configuration storage.

**Key registry locations to monitor:**

    Persistence (run at startup):
    HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
    HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run

    Service installation:
    HKLM\SYSTEM\CurrentControlSet\Services\[malware_service]

    Browser hijacking:
    HKCU\SOFTWARE\Microsoft\Internet Explorer\Main\Start Page

    Credential storage:
    HKLM\SECURITY\Policy\Secrets (LSA secrets)

**Tools:**

    Regshot:
      Take registry snapshot before execution (shot1)
      Execute malware
      Take registry snapshot after execution (shot2)
      Compare: shows all added, deleted, modified registry values

    Process Monitor (Procmon):
      Real-time registry monitoring
      Filter by Operation: RegSetValue, RegCreateKey
      Filter by Process Name: malware.exe

---

### 6.6 Network Traffic Analysis

**Purpose:** Capture all network communications made by malware —
C2 server IPs/domains, data exfiltration, download URLs, protocol used.

**Setup:**

    INetSim (Linux) or FakeNet-NG (Windows):
      Simulates internet services on the isolated network:
      DNS: responds to ALL queries with analyst's IP
      HTTP/HTTPS: returns 200 OK with dummy content
      SMTP: accepts all email (captures exfiltrated data)
      IRC: accepts connections (for IRC-based botnets)

      Without INetSim:
        Malware DNS query fails → may not execute C2 communications
        DNS response captures would be empty

    Wireshark:
      Capture everything on the isolated network interface
      Filter: ip.src == [malware VM IP]
      Filter: dns to see all DNS queries (reveals C2 domains)
      Follow HTTP stream: see full C2 HTTP request/response

**What network analysis reveals:**

    DNS queries:
      update.c2domain.com → attacker's C2 (or DGA-generated domain)

    HTTP C2 beaconing:
      GET /check HTTP/1.1 Host: c2server.com
      (regular interval — bot checking for commands)

    Data exfiltration:
      POST /upload HTTP/1.1 [large body = stolen credentials/files]

    Ransomware key exchange:
      HTTPS POST to C2 — sends victim ID + encrypted symmetric key

---

### 6.7 Memory Analysis

**Purpose:** Extract malware artifacts from RAM — including
injected code, unpacked payloads, encryption keys, and C2
configurations that never touch disk.

**Why memory analysis is essential:**
- Packed malware unpacks itself in memory → RAM contains the real code
- Injected processes contain malicious code in the target process's memory
- Fileless malware exists only in memory
- Encryption keys may be in memory during or after encryption

**Volatility — memory forensics framework:**

    # List running processes
    vol.py -f memory.dmp windows.pslist

    # List processes with hidden/unlinked processes (rootkit detection)
    vol.py -f memory.dmp windows.psscan

    # Show process DLLs (find injected DLLs)
    vol.py -f memory.dmp windows.dlllist --pid 1234

    # Dump process memory to file
    vol.py -f memory.dmp windows.memmap --pid 1234 --dump

    # Find injected code in processes (different PE sections)
    vol.py -f memory.dmp windows.malfind

    # Extract network connections
    vol.py -f memory.dmp windows.netstat

    # Scan for YARA patterns in memory
    vol.py -f memory.dmp windows.yarascan --yara-rules rule.yar

**Taking a memory dump:**

    # Windows (requires elevated privileges)
    # Using RAMMap, NotMyFault, or WinPmem:
    winpmem_mini_x64.exe memory.dmp

    # Linux
    LiME (Linux Memory Extractor) — kernel module approach
    insmod lime.ko "path=/tmp/memory.dmp format=lime"

**`malfind` plugin:**
Specifically designed to identify process injection — scans all
process memory for regions that are: executable, not backed by
a file on disk, and contain a PE header — classic signs of
injected shellcode or process hollowing.

---

### 6.8 API Monitoring and Hooking

**Purpose:** Intercept and log Windows API calls made by malware —
revealing behaviour at a granular level that static import analysis
cannot provide (including dynamically resolved APIs).

**Tools:**

| Tool | Type | Notes |
|---|---|---|
| **API Monitor** | Windows GUI | Intercepts and logs API calls — user selects which APIs |
| **frida** | Cross-platform scripting | Dynamic instrumentation — hook any function |
| **x64dbg with ScyllaHide** | Debugger | Stealth debugging — anti-anti-debug |
| **OllyDbg** | Legacy debugger | Classic dynamic analysis (32-bit) |
| **WinAPIOverride** | Windows | Comprehensive API monitoring |

**frida example — hook CreateFile:**

    import frida, sys

    script = session.create_script("""
    var createFile = Module.getExportByName('kernel32.dll', 'CreateFileW');
    Interceptor.attach(createFile, {
        onEnter: function(args) {
            console.log('CreateFileW: ' + args[0].readUtf16String());
        }
    });
    """)

**What API monitoring reveals:**
- Exact files opened (including temp files not visible in Procmon)
- Exact registry keys read/written
- Network socket creation and data sent
- Cryptographic operations (keys, algorithms)
- Anti-debug API calls (IsDebuggerPresent returns TRUE → bypass)

---

### 6.9 Dynamic Analysis Tools Reference

| Tool | Platform | Primary Use |
|---|---|---|
| **Cuckoo Sandbox** | Linux host | Automated malware analysis sandbox |
| **Any.Run** | Web | Interactive online sandbox |
| **Process Monitor (Procmon)** | Windows | Real-time file/registry/process monitoring |
| **Process Explorer** | Windows | Process tree, DLL inspection, VT integration |
| **Process Hacker** | Windows | Process analysis + memory dump |
| **Regshot** | Windows | Registry + file system snapshot comparison |
| **Wireshark** | Cross-platform | Network traffic capture and analysis |
| **INetSim** | Linux | Simulate internet services for isolated analysis |
| **FakeNet-NG** | Windows | Windows-based internet simulation |
| **API Monitor** | Windows | API call interception and logging |
| **x64dbg** | Windows | Modern debugger for 32/64-bit |
| **OllyDbg** | Windows | Classic 32-bit debugger |
| **Volatility** | Cross-platform | Memory forensics framework |
| **WinPmem / LiME** | Windows/Linux | Memory acquisition |
| **frida** | Cross-platform | Dynamic instrumentation and hooking |

---

## Section 7 — Indicators of Compromise (IOCs)

### 7.1 What Are IOCs

**WHAT:**
Indicators of Compromise (IOCs) are artifacts — technical evidence —
that indicate a system has been compromised or is communicating
with malicious infrastructure. IOCs are the OUTPUT of malware
analysis and the INPUT to threat hunting and detection.

**IOC lifecycle:**

    Malware Analysis
            ↓
    IOCs Extracted (hashes, IPs, domains, registry keys)
            ↓
    IOCs Shared (STIX/TAXII, ISACs, VirusTotal, threat intel feeds)
            ↓
    IOCs Deployed (firewall blocks, SIEM rules, EDR signatures)
            ↓
    Threat Hunting (search historical logs for IOC matches)
            ↓
    Detection of past or active compromise

---

### 7.2 IOC Types and Examples

| IOC Type | Example | Where Found |
|---|---|---|
| **File hash (MD5/SHA1/SHA256)** | `abc123...` | Malware sample, dropped files |
| **File name / path** | `C:\ProgramData\svchost32.exe` | File system monitoring |
| **File size** | 482,304 bytes | Static analysis |
| **IP address** | `185.220.101.45` | Network capture, C2 |
| **Domain / hostname** | `update.evil-c2.com` | DNS queries |
| **URL** | `http://c2.evil.com/beacon?id=12345` | HTTP capture |
| **Email address** | `attacker@phish.com` | Phishing analysis |
| **Email subject** | "Invoice #2024-001 Payment Required" | Phishing |
| **Registry key** | `HKCU\...\Run\svchost32` | Registry monitoring |
| **Mutex name** | `Global\{GUID}` | Process analysis |
| **User agent string** | `Mozilla/5.0 (custom_C2_agent)` | HTTP headers |
| **SSL certificate hash** | `sha256/abc...` | TLS inspection |
| **YARA rule match** | Rule detects specific byte pattern | Static analysis |
| **Behavioural pattern** | Word → PowerShell → network connection | Dynamic analysis |

**IOC quality spectrum:**

    Low quality: IP addresses (change frequently), file names (trivially changed)
    Medium quality: File hashes (per-variant), domains (rotate but less often)
    High quality: Mutex names, YARA byte patterns, behavioural TTPs (persistent across campaigns)

---

### 7.3 IOC Sharing Formats

| Format | Full Name | Use |
|---|---|---|
| **STIX** | Structured Threat Information eXpression | Comprehensive threat intelligence standard |
| **TAXII** | Trusted Automated eXchange of Intelligence Information | Protocol for sharing STIX data |
| **OpenIOC** | Open Indicators of Compromise | Mandiant XML-based IOC format |
| **MISP** | Malware Information Sharing Platform | Open-source threat intelligence platform |
| **YARA** | Yet Another Recursive Acronym | File-based pattern matching |
| **Sigma** | Generic SIEM rule format | Translate to Splunk/ELK/QRadar queries |
| **CSV/JSON** | Simple lists | Basic hash/IP/domain sharing |

**MISP (Malware Information Sharing Platform):**
Open-source threat intelligence platform for sharing, storing,
and correlating IOCs between organizations, ISACs (Information
Sharing and Analysis Centers), and CERTs.

---

## 📌 Extra Notes

### E1 — Static vs Dynamic Analysis Comparison

> [!NOTE]
> The static vs dynamic distinction is the most heavily MCQ-tested
> concept in this session — know every property precisely.

| Property | Static Analysis | Dynamic Analysis |
|---|---|---|
| **Malware executed?** | ❌ No | ✅ Yes |
| **Safety** | ✅ Safe — no execution | ❌ Requires isolated VM |
| **Packed malware** | ❌ Reveals little | ✅ Unpacks in memory |
| **Anti-debug evasion** | ❌ Not applicable | ✅ Applies — must bypass |
| **Anti-VM evasion** | ❌ Not applicable | ✅ Applies — may not execute |
| **Network behaviour** | ❌ Cannot observe | ✅ Captures C2 comms |
| **Runtime APIs** | ❌ Only static imports | ✅ All dynamic API calls |
| **Memory-only payloads** | ❌ Not visible | ✅ Visible in memory dump |
| **Complete coverage** | ✅ All code paths | ❌ Only executed paths |
| **Reproducibility** | ✅ Deterministic | ❌ May vary per execution |
| **Complexity** | High (requires assembly knowledge) | Moderate (tools do heavy lifting) |
| **Time required** | Hours to days (manual RE) | Minutes to hours |
| **Tools** | IDA, Ghidra, YARA, strings | Cuckoo, Procmon, Wireshark, Volatility |

---

### E2 — Anti-Analysis Techniques Malware Uses

> [!NOTE]
> Understanding anti-analysis techniques enables analysts to
> defeat them — directly relevant to dynamic analysis labs.

**Anti-Debugging:**

    IsDebuggerPresent() API:
      Returns TRUE if process is being debugged
      Malware checks → debugger detected → alters/stops execution
      Bypass: patch the return value, use ScyllaHide plugin

    CheckRemoteDebuggerPresent():
      Checks for remote debugger attachment
      Bypass: same patching approach

    Timing checks (RDTSC):
      Measure time between two points — much longer in debugger
      If delta > threshold → debugger detected

    NtQueryInformationProcess:
      Lower-level debug detection — harder to bypass

**Anti-VM / Sandbox Detection:**

    VMware registry key:
      HKLM\SOFTWARE\VMware, Inc.\VMware Tools
      Check → if present → VM detected → benign behaviour

    CPUID hypervisor bit:
      CPUID instruction returns hypervisor present flag in VMs

    MAC address check:
      VMware: 00:0C:29, VirtualBox: 08:00:27
      Check NIC MAC prefix → VM detected

    Sandbox artifacts:
      Username: "sandbox", "maltest", "virus"
      Process list: Wireshark, Procmon, OllyDbg → analysis environment
      Screen resolution: 800×600 or 1024×768 → typical sandbox

    Sleep/delay evasion:
      Sleep(600000) → 10 minutes → sandbox times out (usually 2–5 min)
      After sleep: malware executes on real system

    User interaction check:
      Wait for mouse movement, keyboard press
      Sandboxes are automated — no user interaction → not executing

**Anti-Disassembly:**

    Junk code insertion: meaningless instructions confuse disassembler
    Overlapping instructions: bytes that decode differently depending on entry point
    Indirect calls: call [register] — disassembler cannot determine target
    Self-modifying code: code changes itself during execution

---

### E3 — PE File Format Deep Dive

> [!NOTE]
> PE format details are tested in static analysis MCQs —
> know the structure, section names, and what each reveals.

**Complete PE structure:**

    Offset 0:   DOS Header (64 bytes)
                  - Magic: 4D 5A ("MZ")
                  - e_lfanew: offset to PE header
    Offset varies: DOS Stub (prints "This program cannot be run in DOS mode")
    Offset e_lfanew: PE Signature ("PE\0\0")
    PE Header:
        COFF File Header:
          Machine (0x014C = i386, 0x8664 = x86-64)
          NumberOfSections
          TimeDateStamp  ← compilation time (forensic value, often spoofed)
          SizeOfOptionalHeader
          Characteristics
        Optional Header:
          Magic (0x010B = PE32, 0x020B = PE32+/64-bit)
          AddressOfEntryPoint  ← where execution begins
          ImageBase
          SectionAlignment
          Subsystem (GUI=2, Console=3, Native=1, Driver)
    Section Headers (array):
      .text:  VirtualAddress, VirtualSize, RawOffset, Characteristics (EXEC|READ)
      .data:  Characteristics (READ|WRITE)
      .rsrc:  Embedded resources
    Sections (raw data)
    Import Directory  ← IAT — which DLLs/functions are imported
    Export Directory  ← which functions this PE exports
    Resources         ← embedded icons, strings, manifests, other PE files

**High-entropy section analysis:**
Normal entropy: 5.0–6.5 (code), 3.0–5.0 (data)
Encrypted/packed: 7.0–8.0 → indicator of obfuscation

**Overlay data:**
Data appended after the last section — not part of PE structure.
Malware sometimes stores: encrypted payload, configuration data,
additional PE files in overlay. Binwalk and foremost can extract it.

---

### E4 — Malware Naming Conventions

> [!NOTE]
> AV vendors use inconsistent naming — understanding conventions
> prevents confusion when analyzing reports from multiple vendors.

**Standard naming convention (many vendors):**

    Type.Platform.FamilyName.Variant!Modifier

    Examples:
    Trojan.Win32.Zeus.B        → Trojan, 32-bit Windows, Zeus family, variant B
    Worm.Win32.WannaCry.A      → Worm, 32-bit Windows, WannaCry, variant A
    Ransom.Win64.LockBit.Gen   → Ransomware, 64-bit Windows, LockBit, generic
    Backdoor.Linux.Mirai.C     → Backdoor, Linux, Mirai, variant C

**Platform codes:**
Win32, Win64, Linux, Android, MacOS, iOS, JS (JavaScript), PHP

**Type codes:**
Trojan, Worm, Virus, Ransom, Backdoor, Spyware, Adware, Rootkit,
Dropper, Downloader, Infostealer, Exploit, PUA (Potentially Unwanted App)

**The inconsistency problem:**
Different AV vendors name the same malware differently:
- Kaspersky: Backdoor.Win32.DarkComet.A
- Microsoft: Backdoor:Win32/DarkComet.A
- Symantec: Backdoor.DarkComet
- ESET: Win32/DarkComet.A

**Solution:** Use SHA-256 hash as the DEFINITIVE identifier —
hashes are vendor-independent and unambiguous for specific variants.
Malware Bazaar, VirusTotal use hashes as primary keys.

---

### E5 — USB Pratirodh and AppSamvid — Syllabus Note

> [!NOTE]
> The syllabus specifically mentions USB Pratirodh and AppSamvid
> as tools for system security in the Session 20 context.
> These are Indian government security tools.

**USB Pratirodh:**
- Developed by: C-DAC (Centre for Development of Advanced Computing), India
- Purpose: USB device access control for Windows systems
- Function: Allows organizations to whitelist specific USB devices
  (by manufacturer ID, product ID, serial number) — block all others
- Prevents: malware delivery via USB, data theft via USB drives
- Deployment: enterprise endpoints, government workstations
- Relevance to malware: directly prevents USB-based malware delivery
  (USB Rubber Ducky, malicious USB drives, hardware keyloggers)

**AppSamvid:**
- Developed by: C-DAC, India
- Purpose: Application whitelisting solution for Windows
- Function: Allows only pre-approved (whitelisted) applications
  to execute — blocks ALL unauthorized executables
- Prevents: malware execution (even zero-day — if not whitelisted,
  it cannot run regardless of signature absence)
- Mechanism: application hash + certificate verification
- Relevance to malware: the single most effective malware prevention
  technique — a malware sample that is not on the whitelist
  simply cannot execute — defeating all malware types

**Why application whitelisting is the strongest malware prevention:**
Unlike antivirus (detects known bad), whitelisting uses
DEFAULT-DENY — everything not explicitly permitted is blocked.
New malware, zero-day malware, polymorphic malware — none can
execute if they are not on the approved list.

---

### E6 — Famous Malware Case Studies

> [!NOTE]
> Case studies tie together malware types with real-world impact —
> frequently referenced in MCQs.

**Case Study 1 — Stuxnet (2010):**
- **Type:** Worm + rootkit + PLC attack malware
- **Target:** Siemens S7-315/317 PLCs controlling Iranian uranium centrifuges
- **Delivery:** USB drive (air-gapped network)
- **Mechanism:** Exploited 4 zero-day vulnerabilities simultaneously
  (unprecedented). Modified PLC speed while reporting normal to operators.
  ~1,000 centrifuges physically destroyed over months.
- **Attribution:** USA + Israel (NSA/Unit 8200) — Stuxnet's complexity
  implied nation-state resources
- **Significance:** First publicly known cyberweapon causing physical
  infrastructure destruction. Demonstrated ICS/SCADA as attack surface.

**Case Study 2 — WannaCry (2017):**
- **Type:** Ransomware worm
- **Propagation:** EternalBlue (CVE-2017-0144) — NSA-developed SMB exploit
  leaked by Shadow Brokers
- **Scope:** 230,000+ computers in 150 countries in 72 hours
- **Impact:** NHS (UK National Health Service) — cancelled surgeries,
  ambulance diversions. Nissan, FedEx, Telefónica.
- **Kill switch:** Security researcher Marcus Hutchins registered
  an unregistered domain hardcoded in WannaCry — malware checked
  if domain existed — if yes → stop spreading. Domain registration
  halted the worm.
- **Attribution:** Lazarus Group (North Korea)
- **Significance:** First ransomware with self-propagating worm component.

**Case Study 3 — NotPetya (2017):**
- **Type:** Wiper disguised as ransomware
- **Delivery:** Trojanized Ukrainian accounting software update (M.E.Doc)
- **Propagation:** EternalBlue + credential harvesting (Mimikatz) +
  legitimate Windows admin tools (psexec, wmic)
- **Impact:** $10 billion+ global damages. Maersk (shipping) — all systems
  wiped globally. FedEx TNT division. Merck pharmaceutical. Hospitals.
- **Why wiper not ransomware:** Ransom payment mechanism was broken
  — the ID used to decrypt was random, not tied to any key stored
  with attacker — no decryption was ever possible.
- **Attribution:** Sandworm (GRU — Russian military intelligence)

**Case Study 4 — SolarWinds SUNBURST (2020):**
- **Type:** Supply chain attack → backdoor
- **Delivery:** Trojanized SolarWinds Orion IT monitoring software update
- **Duration:** ~9 months undetected (March–December 2020)
- **Scope:** ~18,000 organizations installed update; ~100 deeply
  compromised including US government agencies
- **Sophistication:** Extremely advanced — binary lived dormant 2 weeks
  before activating; checked for analysis environment; used
  DGA for C2; disguised traffic as legitimate Orion telemetry
- **Attribution:** APT29 (Cozy Bear — Russian SVR)

---

### E7 — Malware Analysis Lab Setup

> [!NOTE]
> The syllabus specifically requires a malware analysis lab.
> This section covers the exact tools and setup for the practical.

**Recommended Lab Environment:**

    HOST: Windows 10/11 or Ubuntu 22.04
    HYPERVISOR: VMware Workstation Pro or VirtualBox

    VM 1 — Windows Analysis VM:
      Windows 10 (fresh install — no updates for consistency)
      Tools installed:
        - Process Monitor (Procmon) — Sysinternals
        - Process Explorer — Sysinternals
        - Process Hacker
        - Wireshark
        - Regshot
        - x64dbg
        - pestudio
        - DIE (Detect It Easy)
        - API Monitor
        - CFF Explorer
      AV disabled (would interfere)
      Network: Host-only or isolated NAT
      Snapshots: "Clean Baseline" — revert after each analysis

    VM 2 — REMnux / Analysis Linux VM:
      REMnux (Ubuntu-based malware analysis distro)
      Pre-installed: strings, FLOSS, file, Volatility, Wireshark,
                     INetSim, YARA, ssdeep, Ghidra, radare2
      Network: Same isolated network as Windows VM
      INetSim running: simulates DNS/HTTP/SMTP for Windows VM

**Sample sources (legal and safe):**
- MalwareBazaar (bazaar.abuse.ch): community-submitted samples
- ANY.RUN: downloadable samples from public analyses
- VirusTotal Intelligence (paid): sample download
- theZoo (GitHub): educational samples in password-protected ZIPs

> [!WARNING]
> NEVER analyze malware on a production machine.
> NEVER analyze malware outside an isolated VM.
> NEVER run malware samples received via email "for analysis"
> unless from a trusted source and in proper isolation.
> Always use password-protected ZIPs (password: "infected")
> when storing/transferring malware samples.

---

### E8 — Predecessor / Successor Chains

> [!NOTE]
> Understanding malware evolution maps technical history to
> current threats.

**Ransomware Evolution:**

    PC Cyborg / AIDS Trojan (1989) — first ransomware — floppy disk
    Symmetric encryption — key derivable from code
            ↓
    Gpcode (2004–2010) — RSA encryption — early modern ransomware
            ↓
    CryptoLocker (2013) — RSA-2048 + Bitcoin — template for all modern ransomware
            ↓
    CTB-Locker (2014) — ECC encryption — Tor for C2
            ↓
    Locky (2016) — massive spam campaigns — Necurs delivery
            ↓
    WannaCry (2017) — self-propagating worm + ransomware
            ↓
    GandCrab (2018–2019) — first major successful RaaS model
    → Retired — estimated $2B in ransoms collected
            ↓
    REvil/Sodinokibi, Ryuk, Maze (2019–2020) — double extortion era
            ↓
    LockBit 2.0, 3.0, Conti, BlackCat (2021–2023) — enterprise RaaS maturity
            ↓
    Akira, Play, RansomHub (2023–2025) — post-takedown replacements

**Banking Trojan Evolution:**

    Back Orifice (1998) — first widely known RAT
            ↓
    Sub7 (1999) — script kiddie RAT
            ↓
    Zeus (Zbot) (2007) — banking Trojan — form grabbing
    Zeus source code leaked (2011) → dozens of variants
            ↓
    Citadel, IceIX, Gameover Zeus (2011–2014) — Zeus variants
            ↓
    Dridex (2014) — macro delivery — replaced Zeus
            ↓
    TrickBot (2016) — modular — evolved to ransomware delivery vehicle
            ↓
    Emotet takedown (Jan 2021) — law enforcement — Europol
    Emotet re-emerged (Nov 2021) → continues as malware loader
            ↓
    Qakbot takedown (Aug 2023) — FBI Operation Duck Hunt
    Qakbot activity resumed within months

**Malware Analysis Tool Evolution:**

    OllyDbg (2001) — classic 32-bit debugger — still used
            ↓
    IDA Pro commercial (1991–present) — industry standard
            ↓
    Cuckoo Sandbox (2011) — first open-source automated sandbox
            ↓
    Volatility (2007) — memory forensics framework
            ↓
    YARA (2013) — pattern matching by Victor Alvarez (VirusTotal)
            ↓
    Ghidra (2019) — NSA releases as open source — free IDA alternative
            ↓
    x64dbg — modern replacement for OllyDbg — 32/64-bit
            ↓
    FLOSS / CAPA (Mandiant/Google) — automated capability analysis
            ↓
    AI-assisted analysis (2024+) — LLM-based code explanation

---

### E9 — Terminology Traps

| Term | Trap | Clarification |
|---|---|---|
| **Static analysis = safe, dynamic = dangerous** | "Both are equally risky" | Static = NO EXECUTION = safe. Dynamic = MALWARE RUNS = requires isolation. Static is always safer. |
| **Dropper = Downloader** | "Both deliver malware the same way" | DROPPER contains embedded payload — drops it. DOWNLOADER fetches payload from remote URL. Different mechanisms, same goal. |
| **Ransomware encrypts the OS** | "Ransomware destroys the operating system" | Ransomware encrypts USER DATA files — it must leave the OS functional so the victim can see the ransom note and pay. Encrypting the OS would prevent payment. |
| **NotPetya was ransomware** | "NotPetya is a ransomware case study" | NotPetya LOOKED like ransomware but was a WIPER — payment was impossible by design. It is a cyberwarfare/destructive malware case study. |
| **Fileless malware = no traces** | "Fileless is undetectable" | Fileless = no FILE ON DISK. Traces exist in: memory, event logs, WMI, registry, network logs. Memory forensics and PowerShell logging detect it. |
| **YARA = behavioural detection** | "YARA detects malware by its actions" | YARA matches STATIC PATTERNS in files or memory — byte sequences, strings, PE structure. Behavioural detection is done by EDR and sandboxes. |
| **All packed malware is malicious** | "High entropy = malware" | Many LEGITIMATE programs (installers, self-extracting archives, compressed executables) are packed. High entropy is suspicious and warrants further analysis — not proof of malice. |
| **Same hash = same malware family** | "Different hash = different family" | Hash uniquely identifies a SPECIFIC FILE VERSION. Two files from the SAME FAMILY have DIFFERENT hashes (due to recompilation, packing). Family identification requires YARA rules and code analysis — not hash matching alone. |
| **Logic bomb = time bomb** | "Logic bomb always triggers on a date" | A logic bomb is triggered by ANY condition — date/time is ONE type (called time bomb). Other triggers: file deletion, user login/logout, counter values, network events. Time bomb is a SUBTYPE of logic bomb. |
| **Bootkit = boot sector virus** | "Bootkits and boot sector viruses are the same" | Boot sector VIRUSES infect MBR to SPREAD to other media. BOOTKITS are a rootkit subtype — they infect MBR/VBR/UEFI to MAINTAIN PERSISTENCE and hide from the OS — different goals. |

---

### E10 — Current Landscape 2026

> [!NOTE]
> Current state of malware threats as of 2025–2026.

**Ransomware landscape:**
Despite multiple law enforcement takedowns (LockBit — February 2024,
ALPHV/BlackCat exit scam — March 2024), new groups immediately fill
vacuums. RansomHub emerged as dominant group post-LockBit takedown —
recruiting displaced affiliates. Ransomware total payments in 2023:
$1.1 billion (record — Chainalysis). 2024 estimated higher despite
some hesitation after Conti and LockBit disruptions.

**Notable 2023–2025 attacks:**
- **MOVEit (Cl0p — June 2023)**: Mass exploitation of MOVEit Transfer
  zero-day (CVE-2023-34362). ~2,700 organizations, ~95 million records.
  No encryption — pure data theft extortion. BBC, British Airways,
  Boots, US federal agencies.
- **Change Healthcare (ALPHV — February 2024)**: US healthcare payment
  processor. $22 million ransom paid (then ALPHV disappeared with it —
  exit scam). Disrupted US healthcare payments for months.
- **CDK Global (BlackSuit — June 2024)**: Auto dealership software.
  $25 million ransom. 15,000+ dealerships impacted.
- **Snowflake data theft campaign (2024)**: Infostealer-compromised
  credentials used to access cloud data platforms — Ticketmaster,
  AT&T, Santander. No ransomware — pure data extortion.

**2025–2026 trends:**
- **AI-powered malware analysis evasion**: ML models generate samples
  that specifically defeat ML-based detection systems
- **Cloud-native attacks**: Malware targeting cloud management APIs,
  serverless functions, container orchestration
- **Quantum threat on horizon**: Post-quantum cryptography migration
  concern — ransomware could theoretically use quantum-resistant
  encryption making decryption even more impossible

**Relevant CVEs (malware delivery):**
- **CVE-2023-34362 (MOVEit SQL injection — 2023)**: Zero-day used
  by Cl0p for mass data theft
- **CVE-2024-3400 (PAN-OS — 2024)**: CVSS 10.0 — used for initial access
  then malware deployment
- **CVE-2024-21887 (Ivanti Connect Secure — 2024)**: Exploited for
  persistent malware implants on VPN appliances

---

### E11 — Indian Legal Context

> [!NOTE]
> Indian law applicable to malware creation, distribution, and attacks.

| Law | Section | Offence | Penalty |
|---|---|---|---|
| **IT Act 2000** | **S.43(c)** | Introducing computer contaminant (virus/malware) into any system | Civil compensation up to ₹1 crore |
| **IT Act 2000** | **S.66** | Creating/deploying malware causing unauthorized damage | Up to 3 years + ₹5 lakh fine |
| **IT Act 2000** | **S.66B** | Receiving data stolen via malware (credential databases, etc.) | Up to 3 years + ₹1 lakh fine |
| **IT Act 2000** | **S.66C** | Identity theft via malware-captured credentials | Up to 3 years + ₹1 lakh fine |
| **IT Act 2000** | **S.66F** | Deploying malware against critical infrastructure (power, banking, defence, telecom) with national security intent | **Life imprisonment** |
| **IT Act 2000** | **S.43(g)** | Destroying data via wiper malware | Civil ₹1 crore |
| **IPC** | **S.420** | Financial fraud enabled by banking Trojans/infostealers | Up to 7 years + fine |
| **IPC** | **S.426** | Mischief causing damage via destructive malware | Up to 3 months + fine |
| **DPDPA 2023** | — | Organization breached via malware → personal data exposed | Penalty up to ₹250 crore |
| **DPDPA 2023** | — | Failure to notify affected individuals after malware breach | Penalty up to ₹200 crore |

**CERT-In obligations:**
Organizations must report malware incidents to CERT-In (cert-in.org.in)
within 6 hours of detection under the CERT-In directions of April 2022.
Failure to report is itself a violation.

**Ransomware payment legality in India:**
There is no explicit law prohibiting ransomware payment in India (unlike
some US regulatory frameworks for OFAC sanctions). However:
- Payments to sanctioned entities (terrorist groups, sanctioned nations)
  could violate other laws
- Payments may constitute proceeds of crime in some interpretations
- Organizations are encouraged to involve law enforcement before paying

---

## Abbreviations Table

| Abbreviation | Full Form | One-Line Technical Meaning |
|---|---|---|
| **AMSI** | Antimalware Scan Interface | Windows API allowing AV to scan scripts before execution |
| **AV** | Antivirus | Software detecting malware by signature, heuristic, or behaviour |
| **C2** | Command and Control | Attacker infrastructure managing compromised systems |
| **CAPE** | Configuration And Payload Extraction | Cuckoo fork — extracts malware configs automatically |
| **CERT-In** | Computer Emergency Response Team India | National cybersecurity incident response agency |
| **CFG** | Control Flow Graph | Visual representation of all execution paths in code |
| **CRC** | Cyclic Redundancy Check | Error detection algorithm — CRC-32 used (incorrectly) in WEP |
| **DIE** | Detect It Easy | Packer and compiler identification tool |
| **DKOM** | Direct Kernel Object Manipulation | Rootkit technique modifying kernel data structures directly |
| **ECC** | Elliptic Curve Cryptography | Asymmetric cryptography — used in modern ransomware |
| **EDR** | Endpoint Detection and Response | Behavioral endpoint security platform |
| **ELF** | Executable and Linkable Format | Linux/Unix executable file format |
| **FakNet** | FakeNet-NG | Windows tool simulating internet services for malware analysis |
| **FLOSS** | FLARE Obfuscated String Solver | Mandiant tool extracting decoded strings from malware |
| **IAT** | Import Address Table | PE structure listing imported DLLs and functions |
| **ICMP** | Internet Control Message Protocol | Network diagnostic — ping — used in some malware C2 |
| **ICS** | Industrial Control System | Industrial automation systems — Stuxnet target |
| **INetSim** | Internet Services Simulator | Linux tool simulating internet services for isolated analysis |
| **IOC** | Indicator of Compromise | Technical artifact indicating compromise |
| **LKM** | Loadable Kernel Module | Linux kernel extension — rootkit delivery mechanism |
| **LOLBin** | Living off the Land Binary | Legitimate OS binary abused for malicious purposes |
| **LotL** | Living off the Land | Using legitimate OS tools for malicious purposes |
| **MaaS** | Malware-as-a-Service | Dark web subscription malware services |
| **MISP** | Malware Information Sharing Platform | Open-source threat intelligence sharing platform |
| **MZ** | Mark Zbikowski | DOS executable magic bytes — first two bytes of PE files |
| **OEP** | Original Entry Point | Real entry point of packed malware — visible after unpacking |
| **OT** | Operational Technology | Industrial control and automation systems |
| **PAC** | Protected Access Credential | EAP-FAST credential — also pre-auth context in iOS |
| **PCAP** | Packet Capture | Network traffic capture file format |
| **PE** | Portable Executable | Windows executable file format (.exe, .dll, .sys) |
| **PLC** | Programmable Logic Controller | Industrial hardware controlling physical processes |
| **PTH** | Pass the Hash | NTLM authentication with hash instead of plaintext |
| **RaaS** | Ransomware-as-a-Service | Subscription ransomware infrastructure for affiliates |
| **RAT** | Remote Access Trojan | Malware providing full remote control of compromised system |
| **RCE** | Remote Code Execution | Vulnerability enabling attacker to run code on target |
| **SCADA** | Supervisory Control and Data Acquisition | Industrial monitoring and control system |
| **SIEM** | Security Information and Event Management | Log aggregation and correlation platform |
| **Sigma** | Sigma Rules | Generic SIEM detection rule format |
| **STIX** | Structured Threat Information eXpression | Standard format for threat intelligence |
| **TAXII** | Trusted Automated eXchange of Intelligence Information | Protocol for sharing STIX data |
| **TTP** | Tactics, Techniques, and Procedures | Attacker behavioural patterns — MITRE ATT&CK framework |
| **UPX** | Ultimate Packer for eXecutables | Common open-source executable packer |
| **VBS** | Visual Basic Script | Scripting language — common malware delivery mechanism |
| **VSS** | Volume Shadow Copy Service | Windows point-in-time file backup — deleted by ransomware |
| **WMI** | Windows Management Instrumentation | Windows admin framework — abused for fileless persistence |
| **XOR** | Exclusive OR | Bitwise operation — common simple encryption in malware |
| **YARA** | Yet Another Recursive Acronym | Pattern matching language for malware identification |

---

## 🔑 Keywords + Concept Map

**Core Keywords:**

`Virus` · `Worm` · `Trojan` · `Ransomware` · `Spyware` · `Adware` ·
`Rootkit` · `Bootkit` · `Keylogger` · `Backdoor` · `Dropper` ·
`Downloader` · `Fileless Malware` · `Logic Bomb` · `Wiper` ·
`Banking Trojan` · `Zeus` · `Emotet` · `LockBit` · `WannaCry` ·
`NotPetya` · `Stuxnet` · `RaaS` · `Supply Chain Attack` · `LotL` ·
`LOLBins` · `Double Extortion` · `Static Analysis` · `Dynamic Analysis` ·
`YARA` · `Strings` · `FLOSS` · `PE Analysis` · `Entropy` ·
`Import Table` · `Packer Detection` · `IDA Pro` · `Ghidra` ·
`Cuckoo Sandbox` · `Procmon` · `Regshot` · `Volatility` · `Wireshark` ·
`INetSim` · `malfind` · `IOC` · `STIX` · `TAXII` · `MISP` ·
`USB Pratirodh` · `AppSamvid` · `T1486` · `T1485`

---

**Concept Map:**

    MALWARE ANALYSIS
    │
    ├── MALWARE TYPES
    │   ├── Self-replicating ── Virus (needs host) | Worm (standalone)
    │   ├── Deception ──────── Trojan | Dropper | Downloader
    │   ├── Financial ──────── Ransomware | Banking Trojan | Infostealer
    │   ├── Persistence ────── Rootkit | Bootkit | Backdoor
    │   ├── Surveillance ───── Spyware | Keylogger | Adware
    │   ├── Destruction ────── Wiper | Logic Bomb
    │   └── Infrastructure ─── Bot/Zombie | Fileless
    │
    ├── MALWARE FAMILIES
    │   ├── Banking Trojans ── Zeus → Dridex → TrickBot → IcedID
    │   ├── RATs ────────────── Poison Ivy → DarkComet → AsyncRAT → Cobalt Strike
    │   ├── Ransomware ─────── CryptoLocker → WannaCry → LockBit → Akira
    │   ├── Infostealers ───── RedLine | Raccoon | Lumma
    │   └── Botnets ─────────── Mirai | Emotet | Necurs
    │
    ├── LATEST TRENDS
    │   ├── RaaS ─────────────── Operators + Affiliates → democratized ransomware
    │   ├── Supply chain ─────── Compromise vendor → reach thousands (SolarWinds)
    │   ├── LotL ─────────────── LOLBins → no custom malware files
    │   ├── Double extortion ─── Exfil + Encrypt → pay or data published
    │   └── AI-enhanced ─────── Polymorphic generation | AMSI bypass automation
    │
    ├── STATIC ANALYSIS (no execution)
    │   ├── File ID ─── magic bytes, file command
    │   ├── Hashing ─── SHA-256, ssdeep (fuzzy)
    │   ├── Strings ─── strings, FLOSS (obfuscated strings)
    │   ├── PE analysis ── sections, imports, entropy, timestamps
    │   ├── Packer detection ── DIE, ExeinfoPE, entropy
    │   ├── Disassembly ── IDA Pro, Ghidra
    │   └── YARA ── pattern matching → family identification
    │
    ├── DYNAMIC ANALYSIS (malware runs in isolated VM)
    │   ├── Sandbox ─── Cuckoo, Any.Run → automated report
    │   ├── Process ─── Procmon, Process Explorer → parent-child tree
    │   ├── File ────── Procmon filter WriteFile → dropped files
    │   ├── Registry ── Regshot → persistence keys
    │   ├── Network ─── Wireshark + INetSim → C2 comms
    │   ├── Memory ──── Volatility malfind → injected code
    │   └── API ─────── API Monitor, frida → dynamic API calls
    │
    └── IOCs
        ├── Hash | IP | Domain | URL → threat intelligence feeds
        ├── Registry key | Mutex | File path → SIEM rules
        └── STIX/TAXII/MISP → sharing formats

---

## ⚡ Quick Reference Cheatsheet

### 🦠 Malware Types — One-Line Reference

| Type | Key Property | Primary Goal |
|---|---|---|
| Virus | Needs host file + human execution | Spread + damage |
| Worm | Self-replicating, no host needed | Spread + payload |
| Trojan | Disguised as legitimate software | Backdoor/theft |
| Ransomware | Encrypts files + demands payment | Financial extortion |
| Spyware | Silent monitoring | Data collection |
| Adware | Unwanted advertisements | Revenue generation |
| Rootkit | Hides presence at system level | Persistent access |
| Bootkit | Pre-OS rootkit (MBR/UEFI) | Maximum persistence |
| Keylogger | Records keystrokes | Credential theft |
| Backdoor | Persistent remote access | Ongoing access |
| Dropper | Contains + deploys embedded payload | Deliver malware |
| Downloader | Downloads + executes remote payload | Deliver malware |
| Fileless | Memory-only execution | AV evasion |
| Logic Bomb | Trigger-based destructive payload | Sabotage |
| Wiper | Permanently destroys data | Destruction |
| Bot | Remote-controlled compromised machine | DDoS/spam/fraud |

---

### 🔬 Static vs Dynamic Analysis

| | Static | Dynamic |
|---|---|---|
| Execute malware? | ❌ No | ✅ Yes |
| Safety | ✅ Safe | ❌ Needs isolated VM |
| Packed malware | ❌ Limited | ✅ Unpacks in memory |
| Network behaviour | ❌ No | ✅ Yes |
| Anti-VM applies | ❌ No | ✅ Yes |
| Primary tools | IDA, Ghidra, YARA, strings, pestudio | Cuckoo, Procmon, Wireshark, Volatility |

---

### 🛠️ Key Analysis Tools Quick Reference

**Static Analysis:**

    sha256sum malware.exe                    # Hash
    file malware.exe                         # File type
    strings -a -el malware.exe              # String extraction
    floss malware.exe                        # Obfuscated strings
    yara rule.yar malware.exe               # YARA pattern match
    upx -d packed.exe                        # UPX unpack

**Dynamic Analysis:**

    vol.py -f mem.dmp windows.pslist         # Process list
    vol.py -f mem.dmp windows.malfind        # Injected code
    vol.py -f mem.dmp windows.netstat        # Network connections
    vol.py -f mem.dmp windows.psscan         # Hidden processes

**Procmon filters for malware analysis:**

    Process Name | is | malware.exe
    Operation    | contains | WriteFile
    Path         | contains | AppData\Roaming
    Operation    | contains | RegSetValue

---

### 📊 Malware Family Timeline

| Year | Family | Type | Significance |
|---|---|---|---|
| 1989 | PC Cyborg | Ransomware | First ransomware ever |
| 1998 | Back Orifice | RAT | First widely known RAT |
| 2007 | Zeus | Banking Trojan | Defined banking malware era |
| 2010 | Stuxnet | ICS worm | First cyberweapon |
| 2013 | CryptoLocker | Ransomware | Modern ransomware template |
| 2016 | Mirai | IoT botnet | IoT DDoS paradigm |
| 2017 | WannaCry | Ransomware worm | EternalBlue — NHS |
| 2017 | NotPetya | Wiper | $10B — disguised ransomware |
| 2020 | SolarWinds | Supply chain | 18K orgs — APT29 |
| 2021 | Emotet takedown | Law enforcement | Europol operation |
| 2023 | MOVEit (Cl0p) | Data extortion | 2,700 orgs — no encryption |
| 2024 | LockBit takedown | Law enforcement | NCA/FBI operation |

---

### ⚖️ Indian Legal Reference

| Law | Section | Offence | Penalty |
|---|---|---|---|
| IT Act 2000 | S.43(c) | Introducing malware | Civil ₹1 crore |
| IT Act 2000 | S.66 | Creating/deploying malware | 3 yrs + ₹5L |
| IT Act 2000 | S.66F | Malware on critical infrastructure | Life imprisonment |
| IPC | S.426 | Damage via destructive malware | 3 months + fine |
| DPDPA 2023 | — | Data breach via malware | ₹250 crore |

---

## ✅ Session Revision Snapshot

### ⚡ TL;DR — 5 Bullets

1. **Malware taxonomy: Virus (needs host + execution), Worm (self-replicating,
   no host), Trojan (disguised, no replication), Ransomware (encrypts data,
   demands payment), Rootkit (hides at kernel level), Spyware (silent data
   collection), Botnet (remote-controlled zombie network), Fileless (memory-only,
   no disk artifact).** Modern malware combines multiple categories — WannaCry
   is simultaneously a worm, ransomware, and exploit kit. Classification by
   PRIMARY behavior for exam purposes.

2. **Static analysis examines malware WITHOUT executing it — file hashing
   (VirusTotal), strings extraction, PE header analysis (PEiD, ExeinfoPE),
   disassembly (IDA Pro, Ghidra), decompilation.** Defeated by packing,
   encryption, and obfuscation — but reveals structure, imports, and
   embedded strings. Fast and safe — no sandbox required.

3. **Dynamic analysis executes malware in a controlled environment and
   observes behavior — process monitoring (Process Monitor), network capture
   (Wireshark), registry changes (Regshot), memory analysis (Volatility),
   full sandbox (Cuckoo, Any.Run).** Defeated by anti-VM, timing delays,
   and environment detection — but reveals actual runtime behavior including
   C2 communication, file drops, and registry persistence.

4. **Anti-analysis techniques are the malware author's response to analysis
   methods — anti-debugging (IsDebuggerPresent), anti-VM (VMware registry
   checks, CPUID hypervisor bit, RDTSC timing), anti-sandbox (sleep delays,
   user interaction checks, canary files), code obfuscation, packing, and
   polymorphism/metamorphism.** Know which technique defeats which analysis
   method — this is heavily MCQ-tested.

5. **Latest malware trends: AI-generated polymorphic variants (WormGPT),
   Living-off-the-Land (LOLBins — certutil, PowerShell, mshta), fileless
   execution (AMSI target), Ransomware-as-a-Service (LockBit, BlackCat/ALPHV),
   supply chain attacks (SolarWinds, XZ Utils), IoT malware (Mirai successors),
   and cloud-native malware targeting Lambda/containers.** USB Pratirodh and
   AppSamvid are the Indian government tools specifically mentioned in the
   syllabus for system security.

---

### 🎯 MCQ-Likely Concepts

- [ ] Virus vs Worm vs Trojan — host dependency and replication
- [ ] Ransomware — encryption of files, double extortion, RaaS model
- [ ] Rootkit — kernel-level hiding — LKM hooks sys_call_table
- [ ] Fileless malware — PowerShell in-memory — no disk artifact — AMSI target
- [ ] Botnet — Herder → C2 → Zombie architecture
- [ ] Spyware vs Adware — data theft vs ad injection
- [ ] Logic bomb — triggered by condition (date, event, counter)
- [ ] Backdoor — persistent remote access — survives reboot
- [ ] Keylogger — hardware vs software — captures keystrokes
- [ ] Static analysis — no execution — file hash, strings, PE analysis
- [ ] Dynamic analysis — execution in sandbox — behavior observation
- [ ] VirusTotal — multi-engine hash/file submission — IOC lookup
- [ ] Strings command — extract printable strings from binary
- [ ] PEiD / ExeinfoPE — detect packer, compiler, protector
- [ ] Cuckoo Sandbox — open-source automated malware analysis
- [ ] Any.Run — interactive cloud sandbox — user can click
- [ ] Process Monitor — real-time file/registry/process activity
- [ ] Regshot — snapshot registry before/after execution — diff
- [ ] Wireshark — capture malware network traffic in sandbox
- [ ] Volatility — memory forensics — extract artifacts from RAM dump
- [ ] IDA Pro — industry-standard disassembler/debugger
- [ ] Ghidra — NSA open-source reverse engineering framework
- [ ] Anti-debugging — IsDebuggerPresent() — NtQueryInformationProcess
- [ ] Anti-VM — VMware registry keys, 00:0C:29 MAC, CPUID hypervisor bit
- [ ] Anti-sandbox — sleep delays, user interaction checks, canary files
- [ ] EICAR test file — 68-byte harmless AV compliance test
- [ ] USB Pratirodh — Indian govt tool — controls USB device access
- [ ] AppSamvid — Indian govt tool — application whitelisting
- [ ] LockBit — prolific RaaS — self-spreading ransomware
- [ ] SolarWinds — supply chain attack — SUNBURST backdoor — 2020
- [ ] AMSI — Antimalware Scan Interface — scans scripts before execution
- [ ] Mirai — IoT botnet — default credentials — Dyn DDoS 2016
- [ ] IT Act S.43(c) — introducing malware — civil ₹1 crore
- [ ] IT Act S.66F — malware on critical infrastructure — life imprisonment
- [ ] DPDPA 2023 — data breach via malware — ₹250 crore

---

### 💼 Interview-Likely

- What is the difference between static and dynamic malware analysis — when would you use each?
- Explain three anti-analysis techniques a malware author might use and what they detect.
- What is fileless malware and why is it difficult to detect with traditional AV?
- What is double extortion in ransomware — how does it differ from traditional ransomware?
- What is a supply chain attack — give a real-world example.
- Explain how a LKM rootkit hides processes using sys_call_table hooks.
- What does the Volatility framework extract from a memory dump?
- What is Cuckoo Sandbox and what artifacts does it collect during dynamic analysis?
- What is the difference between a logic bomb and a backdoor?
- What are USB Pratirodh and AppSamvid — what Indian government initiative produced them?
- Walk me through a complete malware analysis workflow from initial sample receipt to final IOC report.

---

## Next Session Bridge

Session 20 is the FINAL session of the Ethical Hacking module.
Malware reverse engineering closes the complete attack-defense cycle:
- Sessions 6–9: Concepts, hacker mindset, attack phases
- Sessions 10–11: Reconnaissance and scanning
- Sessions 12–16: Specific attack techniques (credentials, trojans, viruses, sniffing, DoS, hijacking)
- Sessions 17–18: Advanced attacks (web, wireless, backdoors, Linux, IDS)
- Session 19: Physical security and professional methodology
- Session 20: Malware analysis — examining the artifacts of all previous attacks

After completing Session 20, the remaining deliverables are:
**5 full practice sets (set-01 through set-05) — 40 MCQs each — 200
unique questions covering the entire Ethical Hacking module from
Sessions 6 through 20.** These sets integrate all topics and
are the final preparation artifact before the CCEE exam.

---

<details>
<summary>📖 Glossary</summary>

| Term | Definition |
|---|---|
| **Adware** | Malware displaying unwanted advertisements — often bundled with free software |
| **AMSI** | Antimalware Scan Interface — Windows API scanning scripts before execution — fileless defense |
| **Any.Run** | Interactive cloud-based malware sandbox — user can interact with running sample |
| **AppSamvid** | Indian government application whitelisting tool — developed by CDAC under NCIIPC |
| **APT** | Advanced Persistent Threat — sophisticated, long-term targeted attack, usually nation-state |
| **Backdoor** | Persistent covert remote access mechanism bypassing normal authentication |
| **Behavioral IOC** | Indicator of Compromise based on actions performed — process injection, registry changes |
| **BlackCat/ALPHV** | Rust-written RaaS group — triple extortion model — active 2021–2024 |
| **Botnet** | Network of compromised machines (zombies) under centralized attacker control |
| **C2** | Command and Control — attacker infrastructure managing botnet or RAT |
| **Canary file** | File placed in specific path by sandbox environments — malware checks for its presence |
| **CDAC** | Centre for Development of Advanced Computing — Indian government technology organization |
| **CERT-In** | Indian Computer Emergency Response Team — national cybersecurity incident response |
| **Cobalt Strike** | Commercial penetration testing C2 framework — widely abused by threat actors |
| **Code cave** | Empty space in PE file sections used by cavity viruses to insert malicious code |
| **Cryptominer** | Malware using victim's CPU/GPU to mine cryptocurrency for attacker |
| **Cuckoo Sandbox** | Open-source automated malware analysis sandbox — most widely deployed |
| **DEP** | Data Execution Prevention — hardware/OS feature preventing code execution from data pages |
| **Disassembler** | Tool converting binary machine code to human-readable assembly language |
| **Double extortion** | Ransomware tactic combining file encryption with threat to publish stolen data |
| **Dropper** | Malware that installs other malware on the system — typically first stage |
| **Dynamic analysis** | Malware analysis by executing sample in controlled environment and observing behavior |
| **EICAR** | European Institute for Computer Antivirus Research — produced harmless 68-byte AV test file |
| **ExeinfoPE** | PE analysis tool detecting packers and protectors in Windows executables |
| **Fileless malware** | Malware executing entirely in memory — no file written to disk |
| **Ghidra** | NSA open-source software reverse engineering framework — released 2019 |
| **Hash** | Cryptographic fingerprint of a file — MD5/SHA-1/SHA-256 — primary malware IOC |
| **HKLM** | HKEY_LOCAL_MACHINE — Windows registry hive containing system-wide configuration |
| **Honeypot** | Decoy system designed to attract and study attacker behavior |
| **IDA Pro** | Industry-standard interactive disassembler and debugger for malware analysis |
| **IOC** | Indicator of Compromise — artifact indicating system compromise (hash, IP, domain, registry key) |
| **IsDebuggerPresent** | Windows API call returning TRUE if debugger attached — anti-debugging check |
| **Keylogger** | Malware capturing keystrokes — hardware (physical device) or software (kernel/user mode) |
| **LKRG** | Linux Kernel Runtime Guard — kernel integrity protection module |
| **LockBit** | Prolific RaaS group — self-spreading ransomware — largest affiliate network |
| **Logic bomb** | Malware remaining dormant until specific condition met — then executes payload |
| **LOLBins** | Living off the Land Binaries — legitimate OS tools abused for malicious purposes |
| **LotL** | Living off the Land — technique using built-in OS tools to avoid malware detection |
| **Malware** | Malicious software — umbrella term covering all hostile code categories |
| **Meterpreter** | Advanced Metasploit payload — in-memory — extensible post-exploitation |
| **Mirai** | IoT botnet exploiting default credentials — source of 2016 Dyn DDoS |
| **NCIIPC** | National Critical Information Infrastructure Protection Centre — Indian government |
| **NtQueryInformationProcess** | Windows native API used for advanced anti-debugging checks |
| **OllyDbg** | Windows 32-bit debugger — popular for malware analysis |
| **PE** | Portable Executable — Windows executable format (.exe, .dll, .sys) |
| **PEiD** | Tool detecting packers, cryptors, and compilers in PE files |
| **Persistence** | Techniques ensuring malware survives system reboot |
| **Polymorphic** | Malware mutating its encryption key/stub per infection to change signature |
| **Process Hollowing** | Code injection technique — legitimate process created suspended, hollowed, replaced |
| **Process Monitor** | Sysinternals tool showing real-time file, registry, process, and network activity |
| **RAT** | Remote Access Trojan — provides complete remote control of victim system |
| **Ransomware** | Malware encrypting victim files and demanding payment for decryption key |
| **RaaS** | Ransomware-as-a-Service — subscription model for ransomware deployment |
| **RDTSC** | Read Time-Stamp Counter — x86 instruction used to detect VM timing differences |
| **Regshot** | Tool taking registry snapshots before/after malware execution — shows changes |
| **Reverse engineering** | Process of analyzing compiled code to understand its logic and behavior |
| **Rootkit** | Malware hiding its presence at kernel or firmware level |
| **Sandbox** | Isolated execution environment for safely running and observing malware behavior |
| **SIGMA** | Generic signature format for SIEM detection rules — shared threat intelligence |
| **SolarWinds** | 2020 supply chain attack — SUNBURST backdoor — 18,000 organizations affected |
| **Spyware** | Malware silently collecting user data — keystrokes, screenshots, browsing history |
| **Static analysis** | Malware analysis without execution — examining binary structure and strings |
| **Stuxnet** | Nation-state worm targeting Iranian nuclear SCADA systems — 2010 |
| **SUNBURST** | Backdoor delivered via SolarWinds Orion supply chain compromise — 2020 |
| **Triple extortion** | Ransomware tactic adding DDoS threat to encryption + data theft threats |
| **Trojan** | Malware disguised as legitimate software — does not self-replicate |
| **USB Pratirodh** | Indian government tool controlling USB device access — prevents unauthorized USB |
| **VirusTotal** | Google-owned multi-engine file/URL/hash scanning service — 70+ AV engines |
| **Volatility** | Open-source memory forensics framework — extracts artifacts from RAM dumps |
| **Wiper** | Destructive malware permanently destroying data — no recovery possible |
| **WormGPT** | Dark web LLM used to generate malware and phishing content |
| **x64dbg** | Open-source Windows debugger for 32-bit and 64-bit malware analysis |
| **XZ Utils** | 2024 supply chain backdoor in Linux compression library — CVE-2024-3094 |
| **YARA** | Pattern matching language for malware identification and classification |
| **Zero-day** | Previously unknown vulnerability with no available patch at time of exploitation |

</details>

---