# 🔐 Cybersecurity Study Notes — Session 12A
# Password Cracking Countermeasures · Attack Types · Keyloggers · Spyware

> [!NOTE]
> Session 12A directly continues from Session 11C (password cracking techniques,
> NT/LM hashes, Responder, Pass-the-Hash). This session covers how to STOP those
> attacks (countermeasures), how attacks are formally classified (active/passive/offline),
> and introduces two major post-access surveillance tools: keyloggers and spyware.

---

## 📚 Table of Contents

- [🗺️ Where This Session Fits](#-where-this-session-fits)
- [📌 Prerequisites Self-Check](#-prerequisites-self-check)
- [⚠️ Exam Traps & Misconceptions](#-exam-traps--misconceptions)
- [🧱 Foundation Knowledge](#-foundation-knowledge)
- [Section 1 — Classification of Password Attacks](#section-1--classification-of-password-attacks)
  - [1.1 Online Active Attacks](#11-online-active-attacks)
  - [1.2 Online Passive Attacks](#12-online-passive-attacks)
  - [1.3 Offline Attacks](#13-offline-attacks)
  - [1.4 Non-Electronic Attacks](#14-non-electronic-attacks)
- [Section 2 — Password Cracking Countermeasures](#section-2--password-cracking-countermeasures)
  - [2.1 Password Policy Controls](#21-password-policy-controls)
  - [2.2 Account Lockout & Throttling](#22-account-lockout--throttling)
  - [2.3 Multi-Factor Authentication](#23-multi-factor-authentication)
  - [2.4 Secure Password Storage](#24-secure-password-storage)
  - [2.5 Privileged Account Protections](#25-privileged-account-protections)
  - [2.6 Monitoring & Detection Controls](#26-monitoring--detection-controls)
- [Section 3 — Keyloggers](#section-3--keyloggers)
  - [3.1 What Is a Keylogger](#31-what-is-a-keylogger)
  - [3.2 Types of Keyloggers](#32-types-of-keyloggers)
  - [3.3 Hardware Keyloggers](#33-hardware-keyloggers)
  - [3.4 Software Keyloggers](#34-software-keyloggers)
  - [3.5 Keylogger Deployment & Evasion](#35-keylogger-deployment--evasion)
  - [3.6 Keylogger Countermeasures](#36-keylogger-countermeasures)
- [Section 4 — Spyware Technologies](#section-4--spyware-technologies)
  - [4.1 What Is Spyware](#41-what-is-spyware)
  - [4.2 Types of Spyware](#42-types-of-spyware)
  - [4.3 How Spyware Spreads](#43-how-spyware-spreads)
  - [4.4 Spyware Capabilities & Techniques](#44-spyware-capabilities--techniques)
  - [4.5 Spyware Countermeasures](#45-spyware-countermeasures)
- [📌 Extra Notes](#-extra-notes)
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
    ├── Sessions 6–9   : Concepts, Principles, Hacker Classes
    ├── Sessions 10–11 : Reconnaissance, Scanning, Enumeration,
    │                    Password Attacks, DDoS
    ├── ▶ SESSION 12A  : Password Countermeasures · Attack Classes
    │                    Keyloggers · Spyware          ← YOU ARE HERE
    ├── Session 12B    : Trojans & Backdoors
    └── Sessions 13–20 : Trojans, Viruses, Sniffing, DoS, Web Attacks...


**Phase position:** Post-exploitation surveillance begins here.
After cracking credentials (11C), attackers maintain persistence and
monitor targets using keyloggers and spyware — this session covers both
the defences against cracking AND the surveillance tools that come next.

---

## ⚠️ Exam Traps & Misconceptions

| ❌ Misconception | ✅ Reality |
|---|---|
| Account lockout stops offline attacks | Lockout ONLY stops online attacks. Offline attacks happen on a copy of the hash — the account is never touched. |
| Salting prevents cracking | Salting prevents **precomputed (rainbow table)** attacks. A strong GPU can still crack a salted hash — salting just forces per-hash cracking. |
| MFA stops password cracking | MFA stops **authentication with a cracked password**, not the cracking itself. The attacker can still crack the hash offline. |
| Keyloggers are always software | Hardware keyloggers exist — they plug between keyboard and USB port, require zero software installation, and are invisible to AV. |
| Spyware and adware are the same | Adware shows ads. Spyware **silently** collects data. Some adware includes spyware components — they are not the same category. |
| Passive attacks are always safer to detect | Passive attacks (sniffing, shoulder surfing) generate **zero network noise** — they are HARDER to detect than active attacks. |
| bcrypt is just a hashing algorithm | bcrypt is a **password hashing function with built-in salting and cost factor** — different from general-purpose hash functions like SHA-256. |

---

## 🧱 Foundation Knowledge

<details>
<summary>Click to expand — Must-know before this session</summary>

**Password Hash Basics**
- A hash is a one-way function: password → fixed-length digest
- Same input always produces same output (deterministic)
- Cannot mathematically reverse a hash — must crack by guessing

**Hash Types Recap (from Session 11C)**
- LM Hash: splits password into two 7-char chunks, DES-encrypted — extremely weak
- NT Hash: MD4(UTF-16-LE(password)) — no salt — fast to compute — crackable at scale
- NTLMv2: challenge-response — captured over network via Responder

**Why Cracking Works**
- Attackers obtain hash (from SAM, NTDS.dit, /etc/shadow, network capture)
- Cracking = generating candidate passwords, hashing them, comparing to stolen hash
- Offline = no network contact, no lockout, no logs on target system

**Three-Factor Authentication Principle**
- Something you KNOW (password, PIN)
- Something you HAVE (token, phone, smart card)
- Something you ARE (fingerprint, retina, face)
- MFA = at least two of the three factors

**MITRE ATT&CK Tactic Reference**
- TA0006 = Credential Access (all password and credential theft techniques)
- TA0003 = Persistence (keyloggers and spyware used here)
- TA0005 = Defense Evasion (keylogger hiding, AV bypass)

</details>

---

## Section 1 — Classification of Password Attacks

### 1.1 Online Active Attacks

**WHAT:**
Online active attacks are attempts to authenticate to a **live system** by
submitting password guesses directly to the authentication interface —
login pages, SSH prompts, RDP, APIs, or any live service.

**WHY:**
Attackers use these when they cannot obtain the hash file and must interact
with the real authentication mechanism. They are noisier but require no
prior access to credential stores.

**HOW:**
```
Attacker → sends credentials → live authentication service
         → if correct   → access granted
         → if wrong     → error returned (and possibly logged)
```

**Types of Online Active Attacks:**

| Attack Type | Mechanism | Tool Example |
|---|---|---|
| **Brute Force** | Try every possible character combination | Hydra, Medusa |
| **Dictionary Attack** | Try words from a wordlist | Hydra with -P rockyou.txt |
| **Password Spraying** | One password tried against many accounts | Spray, Ruler |
| **Credential Stuffing** | Use leaked username:password pairs from breaches | Snipr, Sentry MBA |
| **Rule-Based Attack** | Apply mangling rules to wordlist (add numbers, caps) | Hashcat with rules |

**MITRE ATT&CK:**
- T1110 — Brute Force
- T1110.001 — Password Guessing
- T1110.003 — Password Spraying
- T1110.004 — Credential Stuffing

**🔴 Attacker Perspective:**
Password spraying is preferred over brute force in corporate environments.
Brute forcing one account triggers lockout quickly. Spraying one common
password (`Winter2024!`) across 500 accounts avoids per-account lockout
thresholds while maximising success probability.

**🔵 Defender Perspective:**
Detect spraying by monitoring for: same password tried across many accounts
in a short window. Also monitor login attempts from single IPs against
multiple usernames — this is a classic spraying signature in SIEM alerts.

**Real-World Case 1 — Citrix Password Spray (2019)**
- **Year:** 2019
- **Technique:** Password spraying against Citrix ADC (NetScaler) portal
- **Attacker:** IRIDIUM (Iran-linked APT)
- **Impact:** Credential compromise at Citrix — ~6TB of data potentially
  accessed over months
- **Lesson:** Password spraying bypasses lockout and can persist undetected
  for weeks if SIEM alerting for spray patterns is absent

---

### 1.2 Online Passive Attacks

**WHAT:**
Passive attacks involve **observing or intercepting** authentication traffic
without actively sending login attempts. The attacker monitors the network
or the user's session — they do not touch the authentication service directly.

**WHY:**
Passive attacks generate **zero authentication noise** on the target server.
No failed login attempts. No lockout. No rate-limit trigger. This makes them
harder to detect than active attacks.

**HOW:**
```
Legitimate user → sends credentials/hash over network
Attacker (on same network segment) → intercepts traffic
                                   → captures hash/token
                                   → uses offline or relay later
```

**Types of Online Passive Attacks:**

| Attack Type | Mechanism | MITRE ID |
|---|---|---|
| **Network Sniffing** | Capture plaintext credentials (FTP, Telnet, HTTP) | T1040 |
| **Hash Capture (Responder)** | LLMNR/NBNS poisoning → capture NTLMv2 | T1557.001 |
| **Man-in-the-Middle** | ARP poison → sit between user and server | T1557 |
| **Shoulder Surfing** | Physically observe password entry | T1056.002 |
| **Replay Attack** | Capture and retransmit valid auth token | T1550 |

**🔴 Attacker Perspective:**
Responder (session 11C) is the classic passive-then-active hybrid — it
passively poisons LLMNR/NBNS responses and captures NTLMv2 hashes without
any active login attempt against the target. The hash is then cracked offline.

**🔵 Defender Perspective:**
- Disable LLMNR and NBNS via GPO (as covered in 11C)
- Enforce HTTPS everywhere — eliminates plaintext credential exposure
- Use network segmentation — limits who can sit in the same broadcast domain
- 802.1X port authentication — prevents rogue devices from joining the LAN

---

### 1.3 Offline Attacks

**WHAT:**
Offline attacks are performed on a **local copy of stolen hashes** — entirely
disconnected from the target system. The attacker cracks the hash on their own
hardware. No network connection to the target is involved after the hash theft.

**WHY:**
This is the most powerful class of attack. No lockout. No rate limiting.
No detection on the target. The attacker can run billions of guesses per
second using GPUs — for as long as they want.

**HOW:**
```
Phase 1: Steal hash file (SAM, NTDS.dit, /etc/shadow, PCAP)
Phase 2: Transfer to cracking rig (air-gapped if careful)
Phase 3: Run Hashcat/John the Ripper against hash file
Phase 4: Recovered plaintext → used to authenticate
```

**Types of Offline Attacks:**

| Attack Type | Mechanism | Tool |
|---|---|---|
| **Dictionary Attack** | Hash every word in wordlist, compare | Hashcat -a 0 |
| **Brute Force** | Hash every combination up to N chars | Hashcat -a 3 |
| **Rule-Based** | Apply transformations to wordlist | Hashcat -a 0 -r rules |
| **Rainbow Table** | Precomputed hash→plaintext chains — fast lookup | RainbowCrack, rtgen |
| **Hybrid Attack** | Dictionary + brute force mixed | Hashcat -a 6 or -a 7 |
| **AI/ML Attack (2024+)** | GAN-generated candidates (PassGAN) | PassGAN |

**Key Numbers:**
- Hashcat `-m 1000` = NT Hash
- Hashcat `-m 5600` = NTLMv2
- Hashcat `-m 1800` = sha512crypt (Linux)
- Hashcat `-m 3200` = bcrypt (very slow to crack — by design)

**MITRE ATT&CK:**
- T1110.002 — Password Cracking

**🔴 Attacker Perspective:**
Modern cracking rigs use multiple GPUs in parallel. A single RTX 4090 can
compute ~164 billion MD5 hashes per second. NT Hash (MD4) is even faster.
An 8-character password using upper+lower+number = cracked in minutes.
bcrypt with cost factor 12 = ~25 hashes/second on same GPU — that is the
entire point of bcrypt.

**🔵 Defender Perspective:**
The only effective defence against offline attacks is making the hash
computationally expensive to crack: use bcrypt, Argon2, or scrypt.
These are **intentionally slow** — that is a feature, not a bug.

**Real-World Case 2 — LinkedIn Breach (2012)**
- **Year:** 2012 (breach) / 2016 (full scope revealed)
- **Technique:** Offline cracking of stolen SHA-1 hashed passwords
- **Impact:** 117 million accounts. SHA-1 with **no salt** — the same
  password produced the same hash across all users. Cracked en masse
  using rainbow tables within days of the dump appearing online.
- **Lesson:** Unsalted hashes are catastrophic. SHA-1/MD5 are
  **not** password hashing functions — use bcrypt/Argon2.

---

### 1.4 Non-Electronic Attacks

**WHAT:**
Password attacks that require **no technology** — exploiting the human
element rather than the cryptographic or technical layer.

| Method | Description |
|---|---|
| **Shoulder Surfing** | Physically watch someone type their password |
| **Dumpster Diving** | Recover written passwords from discarded paper/sticky notes |
| **Social Engineering** | Trick the user into revealing their password (phishing, vishing) |
| **Rubber Hose Cryptanalysis** | Coercive means — legally/ethically significant in forensics context |

> [!TIP]
> Non-electronic attacks are covered under **human-side of InfoSec** (Session 6/7).
> In exam context: if a question says "attacker watched the user type their PIN"
> → that is **shoulder surfing** → that is a **non-electronic passive** attack.

---

## Section 2 — Password Cracking Countermeasures

### 2.1 Password Policy Controls

**WHAT:**
Organisational rules governing what constitutes an acceptable password —
length, complexity, age, history, and reuse restrictions.

**WHY:**
Weak passwords are the single largest factor enabling successful cracking.
A policy forces baseline credential strength across all users.

**HOW — Key Policy Parameters:**

| Parameter | Recommended Value | Why |
|---|---|---|
| Minimum length | 12–16 characters | Length is the strongest factor against brute force |
| Complexity | Upper + lower + digit + symbol | Expands keyspace exponentially |
| Maximum age | 90 days (traditional) / Passphrase model (modern) | Limits window for cracked credential use |
| Password history | Last 10–24 passwords | Prevents cycling (Password1! → Password2!) |
| No dictionary words | Enforce via checker | Closes dictionary attack vector |
| Passphrase support | Encourage long phrases | `correct-horse-battery-staple` beats `P@ss1` in strength |

> [!IMPORTANT]
> NIST SP 800-63B (2017, revised 2023) **reversed** traditional advice:
> - ❌ Mandatory periodic rotation unless compromise suspected
> - ❌ Complexity rules forcing `P@ssw0rd` type patterns
> - ✅ Minimum 8 chars (15+ recommended for sensitive accounts)
> - ✅ Check against breached password lists (HaveIBeenPwned API)
> - ✅ Allow long passphrases

---

### 2.2 Account Lockout & Throttling

**WHAT:**
Mechanisms that temporarily or permanently disable an account or slow
down authentication after a defined number of failed attempts.

**WHY:**
Limits the rate of online active brute force and password spraying.
Makes exhaustive online guessing computationally infeasible in practice.

**HOW:**

| Mechanism | How It Works | Limitation |
|---|---|---|
| **Account Lockout** | Lock account after N failures (e.g. 5) | Enables DoS — attacker can lock out all accounts |
| **Progressive Delay** | Increase wait time after each failure | Slows attacker without causing lockout DoS |
| **CAPTCHA** | Challenge-response after failures | Stops automated tools, not manual attacks |
| **IP-Based Throttling** | Rate-limit login attempts per IP | Bypassed via botnet (distributed IPs) |
| **Geo-blocking** | Block logins from unexpected countries | Bypassed via VPN/proxy |

> [!WARNING]
> Account lockout does **NOT** protect against offline attacks.
> The attacker has the hash file locally — the account is never touched
> during offline cracking. Lockout only affects live authentication.

**🔴 Attacker Perspective:**
Password spraying specifically exploits lockout thresholds. If lockout
triggers after 5 failures, spray only 3 attempts per account across
all accounts — stays under threshold on every account while covering
the entire organisation.

**🔵 Defender Perspective:**
Implement SIEM rules to detect spraying patterns: alert when the same
source IP attempts authentication against more than 20 unique accounts
within any 10-minute window.

---

### 2.3 Multi-Factor Authentication

**WHAT:**
Requiring two or more authentication factors from different categories
(know / have / are) before granting access.

**WHY:**
Even if an attacker successfully cracks or steals a password, MFA
prevents them from authenticating without the second factor.

**HOW — MFA Factor Types:**

| Factor Type | Category | Examples |
|---|---|---|
| Password / PIN | Something you KNOW | Windows login, ATM PIN |
| OTP (TOTP/HOTP) | Something you HAVE | Google Authenticator, Authy |
| Hardware Token | Something you HAVE | YubiKey, RSA SecurID |
| SMS Code | Something you HAVE | Bank OTP SMS |
| Biometric | Something you ARE | Fingerprint, Face ID |
| Smart Card + PIN | HAVE + KNOW | CAC cards (US military) |

**MFA Protocols:**
- **TOTP** (Time-based OTP) — RFC 6238 — 30-second rotating code
- **HOTP** (HMAC-based OTP) — RFC 4226 — counter-based
- **FIDO2/WebAuthn** — phishing-resistant hardware key standard

> [!IMPORTANT]
> SMS-based MFA is the **weakest** MFA form — vulnerable to:
> - SIM swapping (attacker takes over phone number)
> - SS7 protocol attacks (intercept SMS at telecom level)
> Hardware keys (FIDO2/YubiKey) are the **strongest** MFA form.

**MITRE ATT&CK — MFA Bypass Techniques:**
- T1111 — Multi-Factor Authentication Interception
- T1621 — MFA Request Generation (MFA Fatigue / Push Bombing)

**Real-World Case — Uber MFA Fatigue Attack (2022)**
- **Year:** 2022
- **Technique:** Attacker obtained employee credentials, then bombarded
  the employee with MFA push notifications until the exhausted employee
  approved one (MFA fatigue / push bombing)
- **Impact:** Full internal network access, Slack, HackerOne access
- **Lesson:** Push-based MFA without number matching is vulnerable to
  fatigue attacks. Number matching or FIDO2 hardware keys prevent this.

---

### 2.4 Secure Password Storage

**WHAT:**
The cryptographic methods used to store passwords in a way that
protects them even if the credential database is stolen.

**WHY:**
Databases get breached. If passwords are stored as plaintext or with
weak hashing, every user credential is immediately exposed.
Proper storage makes offline cracking computationally expensive.

**HOW — Storage Methods Compared:**

| Method | Salted? | Speed | Resistance | Verdict |
|---|---|---|---|---|
| Plaintext | — | N/A | None | ❌ Never use |
| MD5 | No | ~60B/s (GPU) | None | ❌ Broken |
| SHA-1 | No | ~40B/s (GPU) | None | ❌ Broken |
| SHA-256 (unsalted) | No | ~20B/s (GPU) | None | ❌ Not for passwords |
| SHA-256 (salted) | Yes | ~20B/s (GPU) | Rainbow only | ❌ Still too fast |
| bcrypt (cost 10) | Yes (built-in) | ~25/s (GPU) | Strong | ✅ Acceptable |
| bcrypt (cost 12) | Yes (built-in) | ~6/s (GPU) | Very Strong | ✅ Recommended |
| Argon2id | Yes (built-in) | Tunable | Best | ✅ Current best practice |
| scrypt | Yes (built-in) | Tunable | Memory-hard | ✅ Strong |

**What Salting Does:**
```
Without salt:  hash("password123") = X  ← same for every user with same password
With salt:     hash("password123" + "a7f3k") = Y  ← unique per user
               hash("password123" + "q9m2z") = Z  ← different user, different result
```
Salt = random unique value stored alongside the hash.
Prevents rainbow table attacks AND prevents two users with the same
password from having the same hash.

**MITRE ATT&CK:**
- T1110.002 — Password Cracking (what these defences mitigate)

---

### 2.5 Privileged Account Protections

**WHAT:**
Specific controls targeting high-value accounts (Domain Admins,
local admins, service accounts) which are the primary targets
of credential attacks.

**Controls:**

| Control | What It Does | Relevance |
|---|---|---|
| **LAPS** (Local Admin Password Solution) | Unique, rotating local admin password per machine | Blocks Pass-the-Hash lateral movement |
| **Protected Users Group** | Disables NTLM, forces Kerberos, no credential caching | Blocks PtH, Responder, credential cache attacks |
| **Privileged Access Workstations (PAW)** | Dedicated hardened machines for admin tasks only | Reduces keylogger/spyware risk on admin sessions |
| **Just-In-Time (JIT) Access** | Admin rights granted only for specific time window | Limits exposure window |
| **Credential Guard** | Isolates LSASS in Hyper-V container | Prevents Mimikatz-style credential dumping |
| **Service Account Controls** | No interactive login, strong passwords, rotate regularly | Limits service account abuse |

> [!NOTE]
> **LAPS** and **Protected Users Group** are the two most heavily tested
> countermeasures for PtH attacks — know both by name and function.

---

### 2.6 Monitoring & Detection Controls

**WHAT:**
Continuous monitoring mechanisms that detect credential attack patterns
in real time or near-real time.

| Control | Detects |
|---|---|
| **SIEM Alerting** | Failed login spikes, spray patterns, off-hours logins |
| **Windows Event IDs** | 4625 (failed logon) · 4771 (Kerberos pre-auth fail) · 4776 (NTLM auth) |
| **Honeypot Accounts** | Fake admin accounts — any login attempt = alert |
| **HaveIBeenPwned Integration** | Flag users whose passwords appear in breach databases |
| **UBA/UEBA** | Behavioural baseline — alert on anomalous login patterns |
| **Privileged Identity Management (PIM)** | Audit and alert on all privileged account activity |

**Key Windows Event IDs for Exam:**

| Event ID | Meaning |
|---|---|
| 4624 | Successful logon |
| 4625 | Failed logon |
| 4648 | Logon with explicit credentials (RunAs) |
| 4771 | Kerberos pre-authentication failed |
| 4776 | NTLM authentication attempt |
| 4740 | Account locked out |

---

## Section 3 — Keyloggers

### 3.1 What Is a Keylogger

**WHAT:**
A keylogger is a surveillance tool — hardware or software — that
records every keystroke typed on a target device without the user's
knowledge. Every password, message, search query, and command typed
is captured and stored or transmitted to the attacker.

**WHY:**
Keyloggers bypass encryption entirely. It does not matter if the
password is hashed in transit, stored with bcrypt, or protected by
TLS — the keylogger captures it **at the moment of typing**, before
any of those protections apply. This makes them extremely effective
even against hardened systems.

**HOW:**
User types password → keylogger intercepts at OS/hardware level → stores keystroke log locally → OR transmits to attacker C2 server Attacker → retrieves log → extracts credentials


**Analogy:**
Imagine you have a highly secure vault with a combination lock.
Encryption and hashing protect the vault.
A keylogger is someone watching over your shoulder as you dial in
the combination — the vault's security is irrelevant once they
see the numbers.

**MITRE ATT&CK:**
- TA0006 — Credential Access
- TA0003 — Persistence (keylogger installed as persistent agent)
- T1056 — Input Capture
- T1056.001 — Keylogging

---

### 3.2 Types of Keyloggers

Two primary categories: **Hardware** and **Software**.
Software keyloggers are further divided by the layer at which
they intercept keystrokes.

| Category | Type | Layer |
|---|---|---|
| Hardware | USB/PS2 inline device | Physical — between keyboard and computer |
| Hardware | Firmware-based | Keyboard BIOS/firmware |
| Hardware | Wireless keyboard sniffer | RF signal interception |
| Software | API-based | Windows API (SetWindowsHookEx) |
| Software | Kernel/Driver-based | Kernel space — deepest level |
| Software | Form-grabbing | Browser — intercepts before HTTPS encryption |
| Software | Acoustic | Analyses sound of keystrokes |
| Software | Electromagnetic | Captures EM emissions from keyboard cable |

---

### 3.3 Hardware Keyloggers

**WHAT:**
Physical devices that sit between the keyboard and the computer,
or are embedded inside the keyboard itself, and record all keystrokes
to internal storage (flash memory).

**WHY attackers use them:**
- Zero software footprint — antivirus cannot detect them
- Survive OS reinstalls, disk wipes, factory resets
- No network traffic generated — impossible to detect via IDS/SIEM
- Require physical access to install AND to retrieve

**Types:**

**1. USB Inline Keylogger**
- Small dongle plugged between USB keyboard and USB port
- Stores keystrokes in internal flash (up to 16GB+)
- Attacker retrieves device later and reads stored log
- Looks like a USB extender — visually inconspicuous

**2. PS/2 Inline Keylogger**
- Same concept but for older PS/2 keyboard connectors
- Less common today but still found in industrial/legacy systems

**3. Acoustic Keylogger**
- Records sound of keystrokes using microphone
- Different keys produce slightly different sound profiles
- Statistical analysis recovers typed content with ~90%+ accuracy
- Requires no physical device on the machine

**4. Electromagnetic Keylogger**
- Every keyboard cable emits EM radiation when keystrokes are transmitted
- Specialised antenna captures and decodes EM leakage
- Effective up to several metres
- Based on TEMPEST research (NSA/NATO classified — now partially public)

**5. Wireless Keyboard Sniffer**
- Many wireless keyboards (non-Bluetooth) transmit on 27 MHz RF unencrypted
- Attacker with RF receiver can intercept keystrokes from up to 100 feet
- Bluetooth keyboards are somewhat safer but have their own vulnerabilities

**🔴 Attacker Perspective:**
Hardware keyloggers are the preferred tool for physical-access scenarios
(rogue insider, cleaning staff with brief access, supply chain attack).
A 30-second window at an unattended workstation is enough to install one.
No admin privileges required. No software to execute.

**🔵 Defender Perspective:**
Physical security is the only effective countermeasure:
- Locked server rooms and workstation areas
- Regular physical inspection of ports — especially in public-facing machines
- Kensington locks on keyboards if needed
- Video surveillance on server room entry points
- Asset management — any unrecognised USB device = incident

---

### 3.4 Software Keyloggers

**WHAT:**
Programs that intercept keystrokes at the operating system or
application level, capturing input before it reaches the target
application or network stack.

**Types in detail:**

**1. API-Based Keylogger (User-Space)**

**HOW:**
Uses Windows API function `SetWindowsHookEx()` to install a
low-level keyboard hook. Every keystroke triggers the hook
procedure before the keystroke reaches the application.
User types → Windows keyboard hook fires → Hook procedure logs keystroke → Passes keystroke to application as normal Application sees normal input — user sees no change

- Easiest to write — common in commodity RATs
- Easiest to detect — AV looks for SetWindowsHookEx calls
- Requires user-space execution (no admin needed for basic use)

**2. Kernel-Level Keylogger (Driver-Based)**

**HOW:**
Installs as a Windows kernel driver or Linux kernel module.
Intercepts keystrokes at the lowest level — before the OS
keyboard subsystem processes them.

- Invisible to most AV solutions (runs in ring 0 — kernel space)
- Requires admin/root privileges to install
- Survives user-level security tools entirely
- Modern Windows 10/11 Driver Signing requirements make this harder
  (Secure Boot + Driver Signature Enforcement must be bypassed)

**MITRE ATT&CK:** T1547.006 — Kernel Modules and Extensions

**3. Form-Grabbing Keylogger**

**HOW:**
Hooks into browser processes (Chrome, Firefox, IE) and intercepts
form data **before it is encrypted by HTTPS/TLS** — capturing
username + password fields at the browser level.
User fills login form → browser processes form data Form grabber intercepts HERE ← before TLS encryption Browser sends encrypted HTTPS request → server


- Bypasses HTTPS entirely
- Cannot be detected by network monitoring (data never leaves unencrypted)
- Used heavily in banking trojans (Zeus, SpyEye, TrickBot)

**MITRE ATT&CK:** T1185 — Browser Session Hijacking

**4. Acoustic Keylogger (Software-Based)**

**HOW:**
Uses the device microphone (or nearby microphone) to record
keyboard sounds. Each key has a slightly different acoustic
signature based on position and key travel distance.
ML algorithms trained on keyboard profiles reconstruct text.

- **2023 Research:** Deep learning model achieved 95% accuracy
  recovering keystrokes from Zoom call audio — no physical access needed
- No malware required if device microphone is already compromised

**Real-World Case — British Study on Acoustic Keylogging (2023)**
- **Year:** 2023
- **Research:** University of Surrey
- **Technique:** Trained CNN on MacBook Pro keypress recordings
- **Impact:** 95% accuracy on local recording, 93% over Zoom audio
- **Lesson:** Microphone access = potential keystroke recovery.
  Sensitive typing should not occur during video calls on compromised
  or untrusted devices.

---

### 3.5 Keylogger Deployment & Evasion

**HOW attackers deploy keyloggers:**

| Vector | Method |
|---|---|
| Phishing email | Malicious attachment drops keylogger |
| Drive-by download | Browser exploit installs silently |
| Physical access | Hardware device planted directly |
| Trojan dropper | Keylogger bundled inside legitimate-looking software |
| Malicious USB | Autorun or HID spoofing installs on insertion |
| Supply chain | Pre-installed in hardware/software before delivery |

**Evasion Techniques:**

| Technique | How It Evades Detection |
|---|---|
| Process injection | Keylogger code injected into legitimate process (explorer.exe) |
| Rootkit combination | Hides keylogger files and process from OS |
| Fileless operation | Runs only in memory — no file on disk for AV to scan |
| Timestomping | Modifies file creation/modification timestamps |
| Anti-VM check | Keylogger terminates if running in sandbox/VM |
| Log encryption | Encrypts captured keystrokes — prevents content inspection |

**MITRE ATT&CK:**
- T1055 — Process Injection
- T1070 — Indicator Removal
- T1497 — Virtualization/Sandbox Evasion

---

### 3.6 Keylogger Countermeasures

**For Organisations:**

| Countermeasure | What It Addresses |
|---|---|
| Endpoint Detection & Response (EDR) | Detects suspicious hook installation, process injection |
| Application whitelisting | Prevents unauthorised executables from running |
| Physical port controls | USB port blocking prevents hardware keyloggers |
| Regular physical inspection | Hardware keylogger detection |
| Privileged Access Workstations (PAW) | Reduces keylogger exposure on admin machines |
| Driver Signature Enforcement | Blocks unsigned kernel-level keylogger drivers |
| Secure Boot | Prevents boot-level keylogger persistence |

**For Users:**

| Countermeasure | What It Addresses |
|---|---|
| Virtual keyboard (on-screen keyboard) | Bypasses API-based keyloggers (mouse clicks, not keystrokes) |
| Password manager autofill | Prevents keystrokes for passwords — fills programmatically |
| Anti-keylogger software (KeyScrambler) | Encrypts keystrokes at driver level before hook capture |
| MFA | Even with captured password — second factor still needed |

> [!TIP]
> Password managers (Bitwarden, 1Password) significantly reduce keylogger
> risk for password fields — autofill injects credentials programmatically
> rather than via keyboard input.

---

## Section 4 — Spyware Technologies

### 4.1 What Is Spyware

**WHAT:**
Spyware is malicious software that **silently monitors and collects**
information about a user's activities — browsing habits, credentials,
communications, location, files — without their knowledge or consent,
and transmits this data to the attacker or a third party.

**WHY:**
Unlike keyloggers which specifically target keystrokes, spyware provides
a **broader surveillance capability** — it can capture screenshots,
record audio/video, track location, steal files, monitor clipboard
contents, and exfiltrate data continuously over time.

**Difference from Keylogger:**

| | Keylogger | Spyware |
|---|---|---|
| Scope | Keystrokes only | Broad — screen, audio, files, location, comms |
| Primary use | Credential theft | Surveillance, espionage, data collection |
| Target | Specific input | Everything on the device |
| Complexity | Simple to complex | Generally more complex |
| Example | Simple hook-based logger | Pegasus, FinFisher, DarkComet RAT |

**MITRE ATT&CK:**
- TA0003 — Persistence
- TA0009 — Collection
- TA0010 — Exfiltration
- T1113 — Screen Capture
- T1123 — Audio Capture
- T1125 — Video Capture
- T1115 — Clipboard Data

---

### 4.2 Types of Spyware

| Type | What It Does | Example |
|---|---|---|
| **Adware-Spyware** | Tracks browsing to serve targeted ads; also reports behaviour | Gator, Claria |
| **System Monitor** | Full activity monitoring — keystrokes, screenshots, emails, chat | Spector Pro |
| **Tracking Cookies** | Persistent browser cookies tracking cross-site behaviour | Third-party ad cookies |
| **Stalkerware** | Commercial monitoring apps marketed for parental control / partner tracking | mSpy, FlexiSPY |
| **Commercial Spyware (Govware)** | Nation-state grade — full device compromise | Pegasus (NSO Group), FinFisher |
| **Banking Spyware** | Monitors banking sessions, intercepts OTPs, steals credentials | Zeus, TrickBot |
| **Mobile Spyware** | Targets Android/iOS — access to calls, SMS, GPS, camera, mic | Pegasus, Cerberus |

---

### 4.3 How Spyware Spreads

| Vector | Method |
|---|---|
| **Bundled software** | Installed silently alongside legitimate freeware (classic adware model) |
| **Drive-by download** | Browser exploit auto-installs from malicious/compromised website |
| **Phishing** | Malicious email attachment or link delivers spyware dropper |
| **Zero-click exploit** | No user interaction required — exploits OS/app vulnerability |
| **Malvertising** | Malicious ads on legitimate sites trigger drive-by install |
| **Physical access** | Attacker installs directly on unlocked device |
| **Fake apps** | Spyware disguised as utility app in third-party app store |
| **USB drop attack** | Found USB device auto-executes spyware on connection |

**Real-World Case — Pegasus Spyware (2021, NSO Group)**
- **Year:** 2021 (Project Pegasus investigation by Citizen Lab / Forbidden Stories)
- **Technique:** Zero-click exploit targeting WhatsApp, iMessage, and
  Apple Mail — no user interaction required whatsoever
- **Impact:** Phones of journalists, activists, heads of state, and
  business executives compromised in 45+ countries. Full access:
  messages, calls, camera, microphone, GPS, files.
- **Lesson:** Zero-click spyware from nation-state vendors operates
  entirely silently. Standard user-awareness training is useless
  against zero-click. Patch velocity and device segmentation are the
  only meaningful controls.

---

### 4.4 Spyware Capabilities & Techniques

**What advanced spyware can do:**

| Capability | Technical Mechanism | MITRE ID |
|---|---|---|
| Screenshot capture | GDI/DirectX API calls — periodic screen dump | T1113 |
| Webcam access | Direct camera driver API | T1125 |
| Microphone recording | Audio API — continuous or trigger-based | T1123 |
| Clipboard monitoring | Windows Clipboard API hook | T1115 |
| File exfiltration | Targeted file search + upload to C2 | T1020 |
| Browser history theft | SQLite database access (Chrome: History file) | T1217 |
| SMS/Call interception | Mobile baseband API / accessibility service abuse | T1430 |
| GPS tracking | Mobile location API | T1430 |
| Encrypted C2 communication | HTTPS, Tor, DNS tunnelling for exfiltration | T1041 |
| Self-deletion | Removes itself after exfiltration to avoid forensic recovery | T1070 |

**How Spyware Maintains Persistence:**

| Persistence Method | Platform | MITRE ID |
|---|---|---|
| Registry Run key | Windows | T1547.001 |
| Scheduled Task | Windows | T1053.005 |
| Startup folder | Windows | T1547.001 |
| Launch Daemon/Agent | macOS | T1543.004 |
| Cron job | Linux | T1053.003 |
| Accessibility service abuse | Android | T1626 |
| Profile/MDM abuse | iOS | T1098 |

---

### 4.5 Spyware Countermeasures

**Technical Controls:**

| Control | What It Addresses |
|---|---|
| Endpoint Detection & Response (EDR) | Behavioural detection of data collection and exfiltration patterns |
| Anti-spyware tools (Malwarebytes, SpyBot) | Signature + behaviour-based spyware detection |
| Application permission controls | Restrict camera, microphone, location access per-app |
| Network monitoring / DLP | Detect unusual outbound data flows — potential exfiltration |
| Email filtering | Block spyware dropper attachments |
| Browser isolation | Contain drive-by download attempts |
| Patch management | Close zero-day vectors — Pegasus exploited unpatched iMessage/WhatsApp |
| Mobile Device Management (MDM) | Enforce device policies, detect unauthorised apps |

**Operational Controls:**

| Control | What It Addresses |
|---|---|
| Principle of least privilege | Limits spyware capability if user has low privileges |
| Regular AV/AS scans | Detect known spyware signatures |
| Cover camera/microphone when not in use | Physical countermeasure against activated surveillance |
| Jailbreak/root detection | Mobile spyware often requires rooted device |
| User awareness training | Phishing and fake-app recognition |

> [!WARNING]
> Nation-state spyware (Pegasus, FinFisher) **cannot be detected or removed**
> by standard consumer anti-spyware tools. These operate at kernel level
> using zero-day exploits. The only reliable countermeasure is:
> device replacement, air-gapped operations, or commercial forensic
> analysis (Citizen Lab methodology / Amnesty Tech MVT tool).

**Amnesty International MVT (Mobile Verification Toolkit):**
- Open-source tool released specifically to detect Pegasus indicators
- Analyses iOS backup and Android filesystem for IOCs
- Used by journalists and human rights organisations

---
---

## 📌 Extra Notes

### Framework Comparisons

**NIST SP 800-63B vs Traditional Password Policy**

| Aspect | Traditional (Pre-2017) | NIST SP 800-63B (Current) |
|---|---|---|
| Rotation | Every 30/60/90 days | Only on suspected compromise |
| Complexity | Mandatory symbols + numbers | Not mandatory — length preferred |
| Min length | 8 characters | 8 minimum, 15+ recommended |
| Hints/security Qs | Allowed | ❌ Prohibited |
| Breached password check | Not mentioned | ✅ Required |
| Paste in password field | Often blocked | ✅ Must be allowed |

> [!NOTE]
> NIST SP 800-63B is the current gold standard for password policy.
> Exam questions may contrast old vs new guidance — know both sides.

---

### Predecessor / Successor Chains

**Password Hashing Evolution:**
DES (LM Hash) → MD4 (NT Hash) → MD5 → SHA-1 → SHA-256 → bcrypt (1999) → scrypt (2009) → Argon2 (2015, PHC winner) ↑ Current best practice

**Spyware Evolution:**
Early adware (1990s) → Gator/GAIN (2000s) → Zeus banking trojan (2007) → FinFisher/FinSpy (2011) → Pegasus (2016–present) → Commercial stalkerware ecosystem (2018–present)


---

### 🌐 Current Landscape (2026)

**AI Tools Changing the Attack Surface:**
- **PassGAN (2023):** GAN trained on RockYou2021 dataset (8.4 billion
  passwords). Generates statistically likely password candidates.
  Cracked 51% of common passwords in under 1 minute in benchmark tests.
- **LLM-assisted social engineering:** GPT-class models used to craft
  highly personalised phishing lures that install spyware droppers —
  dramatically lowering the skill floor for spyware deployment.
- **AI-enhanced acoustic keylogging:** CNN models (2023 Surrey research)
  achieving 95% accuracy on Zoom call audio — passive microphone access
  now constitutes a credential theft vector.

**Cloud Challenges:**
- Cloud-hosted workloads present new keylogging surfaces:
  hypervisor-level keystroke capture is theoretically possible in
  shared-tenant environments (mitigated by modern isolation but
  remains a research area)
- SaaS credential theft via browser-based form grabbers increasingly
  common — HTTPS provides no protection once the browser is compromised
- Cloud access logs (AWS CloudTrail, Azure Monitor) are critical for
  detecting post-spyware credential use — on-premises SIEM integration
  is now mandatory for hybrid environments

**Current CVEs (2024–2026):**
- **CVE-2023-41064 / CVE-2023-41061 (BLASTPASS — 2023):**
  Zero-click iMessage exploit used to deliver Pegasus.
  CVSS 9.8. Patched in iOS 16.6.1. Demonstrates zero-click
  spyware delivery still active in 2023–2024.
- **CVE-2024-3094 (XZ Utils backdoor — 2024):**
  Supply chain attack — malicious code inserted into XZ Utils
  compression library. Would have enabled remote code execution
  on Linux systems — a perfect spyware delivery vector.
  Discovered before widespread deployment. CVSS 10.0.
- **CVE-2024-38112 (Windows MSHTML — 2024):**
  Zero-day exploited in the wild to deploy info-stealer/spyware
  via malicious .url files. Patched July 2024 Patch Tuesday.

**Indian Legal Context:**
- **IT Act 2000 — Section 66:** Using a keylogger or spyware to
  access another person's computer constitutes unauthorised access.
  Penalty: Up to 3 years imprisonment + ₹5 lakh fine.
- **IT Act 2000 — Section 66E:** Violation of privacy by capturing,
  transmitting or publishing private images without consent.
  Penalty: Up to 3 years + ₹2 lakh fine.
  (Webcam spyware falls squarely under this section.)
- **IT Act 2000 — Section 43:** Unauthorised access/damage to computer
  systems. Compensation up to ₹1 crore.
- **DPDPA 2023:** Organisations that suffer data breaches due to
  spyware-enabled exfiltration must notify the Data Protection Board
  and affected individuals. Penalty for failure to notify:
  Up to ₹200 crore. Penalty for data breach: Up to ₹250 crore.
- **Stalkerware legal status in India:** Installing monitoring software
  on a partner's device without consent = potential IPC Section 354C
  (voyeurism) + IT Act 66E violation. Not a grey area.

---

### Terminology Traps

| Term | Trap | Clarification |
|---|---|---|
| **Keylogger vs RAT** | Keyloggers are often called RATs | RAT = Remote Access Trojan (broader). A keylogger is ONE component a RAT may include. Not all keyloggers are RATs. |
| **Spyware vs Stalkerware** | Often used interchangeably | Stalkerware = commercial spyware marketed for monitoring known individuals (partners, employees). Spyware = broader malicious category. |
| **Salting vs Peppering** | Both add data to password before hashing | Salt = random, unique per user, STORED in database alongside hash. Pepper = secret value, NOT stored in database, same for all users, stored in application config. Both used together for maximum protection. |
| **MFA vs 2FA** | Often used interchangeably | 2FA = exactly 2 factors. MFA = 2 or more factors. 2FA is a subset of MFA. |
| **Anti-spyware vs AV** | Treated as the same | AV = primarily targets viruses, worms, trojans by signature. Anti-spyware = tuned for tracking cookies, adware, spyware behaviour. Modern suites combine both. |
| **Passive attack = undetectable** | Assumed true | Passive attacks are HARDER to detect but not impossible. Network traffic analysis, UEBA baselines, and honeypots can surface passive activity. |
| **Password spraying = brute force** | Often confused | Brute force = many passwords against one account. Spraying = one password against many accounts. Completely different detection profile and lockout behaviour. |

---

## Abbreviations Table

| Abbreviation | Full Form | One-Line Meaning |
|---|---|---|
| AV | Antivirus | Software detecting/removing malware by signature or behaviour |
| API | Application Programming Interface | Set of functions an OS/application exposes for use by other programs |
| C2 | Command and Control | Attacker-controlled server receiving data from/sending commands to malware |
| CAPTCHA | Completely Automated Public Turing test to tell Computers and Humans Apart | Challenge to distinguish human from bot |
| CVE | Common Vulnerabilities and Exposures | Standardised identifier for publicly known security vulnerabilities |
| CVSS | Common Vulnerability Scoring System | Numerical score (0–10) rating vulnerability severity |
| DLP | Data Loss Prevention | Tools preventing unauthorised data exfiltration |
| EDR | Endpoint Detection and Response | Security tool monitoring endpoints for threats in real time |
| EM | Electromagnetic | Radiation emitted by electronic devices — exploitable in TEMPEST attacks |
| FIDO2 | Fast IDentity Online 2 | Open authentication standard using hardware security keys |
| GAN | Generative Adversarial Network | ML architecture where two networks compete — used in PassGAN |
| GPO | Group Policy Object | Windows policy applied across domain to enforce settings |
| GPU | Graphics Processing Unit | Parallel processor — used in password cracking rigs |
| HID | Human Interface Device | USB device class — keyboards, mice (also used in USB attack tools) |
| HOTP | HMAC-based One-Time Password | Counter-based OTP standard (RFC 4226) |
| IOC | Indicator of Compromise | Artefact indicating system may be compromised |
| JIT | Just-In-Time | Access provisioned only for specific time window |
| LAPS | Local Administrator Password Solution | Microsoft tool generating unique local admin passwords per machine |
| LM | LAN Manager | Legacy Windows hash algorithm — extremely weak |
| MDM | Mobile Device Management | Platform managing and enforcing policy on mobile devices |
| MFA | Multi-Factor Authentication | Authentication using 2+ factors from different categories |
| MITRE | MITRE Corporation | Non-profit maintaining ATT&CK framework |
| MVT | Mobile Verification Toolkit | Amnesty International tool detecting Pegasus IOCs |
| NIST | National Institute of Standards and Technology | US agency producing cybersecurity standards including SP 800-63B |
| NT | New Technology | Windows NT — basis for modern Windows OS line |
| OTP | One-Time Password | Single-use password valid for one session or time window |
| PAW | Privileged Access Workstation | Hardened machine used exclusively for admin tasks |
| PHC | Password Hashing Competition | Competition that selected Argon2 as winner in 2015 |
| PIM | Privileged Identity Management | Platform auditing and controlling privileged account activity |
| RAT | Remote Access Trojan | Malware giving attacker remote control of compromised system |
| RF | Radio Frequency | Electromagnetic spectrum used in wireless communications |
| SIEM | Security Information and Event Management | Platform aggregating and correlating security logs |
| SMS | Short Message Service | Text messaging — weakest MFA second factor |
| SS7 | Signalling System No. 7 | Telecom protocol vulnerable to SMS interception |
| TOTP | Time-based One-Time Password | 30-second rotating OTP standard (RFC 6238) |
| TLS | Transport Layer Security | Cryptographic protocol securing network communications |
| UEBA | User and Entity Behaviour Analytics | Baseline + anomaly detection for user activity |

---

## 🔑 Keywords + Concept Map

**Core Keywords:**
Online Active Attack · Online Passive Attack · Offline Attack ·
Non-Electronic Attack · Brute Force · Dictionary Attack ·
Password Spraying · Credential Stuffing · Rainbow Table ·
Salt · Pepper · bcrypt · Argon2 · NT Hash · LM Hash ·
Account Lockout · Throttling · MFA · TOTP · FIDO2 ·
LAPS · Protected Users Group · Credential Guard ·
Keylogger · API Hook · Kernel Keylogger · Form Grabber ·
Acoustic Keylogger · Hardware Keylogger · TEMPEST ·
Spyware · Stalkerware · Pegasus · Zero-Click · PassGAN ·
EDR · Anti-spyware · MVT · DPDPA 2023

**Concept Map:**

```
PASSWORD ATTACKS
├── Online Active ──────── Brute Force / Spraying / Stuffing
│                          └── Countermeasure: Lockout / Throttle / MFA
├── Online Passive ─────── Sniffing / Responder / MITM
│                          └── Countermeasure: LLMNR off / HTTPS / 802.1X
├── Offline ────────────── Hashcat / Rainbow / PassGAN
│                          └── Countermeasure: bcrypt / Argon2 / Salting
└── Non-Electronic ──────── Shoulder Surf / Dumpster Dive / SE

POST-CREDENTIAL SURVEILLANCE
├── Keylogger
│   ├── Hardware ────────── USB inline / Acoustic / EM / RF
│   └── Software ────────── API hook / Kernel / Form grabber
│                          └── Countermeasure: EDR / PAW / Password Manager
└── Spyware
    ├── Types ───────────── Adware / Banking / Stalkerware / Govware
    ├── Spread ──────────── Phishing / Drive-by / Zero-click / USB drop
    └── Countermeasure ──── EDR / MDM / Patch / MVT (Pegasus)
```


---

## ⚡ Quick Reference Cheatsheet

### Password Attack Classification

| Attack Class | Live System? | Network Needed? | Lockout Risk? | Detection Difficulty |
|---|---|---|---|---|
| Online Active | ✅ Yes | ✅ Yes | ✅ High | Low — generates logs |
| Online Passive | ✅ Yes (observing) | ✅ Yes | ❌ None | High — no auth noise |
| Offline | ❌ No | ❌ No | ❌ None | Very High — no contact |
| Non-Electronic | ❌ No | ❌ No | ❌ None | Very High — human layer |

### Password Hashing Quick Reference

| Algorithm | Salted | GPU Speed (approx) | Use For Passwords? |
|---|---|---|---|
| MD5 | ❌ | ~60 billion/s | ❌ Never |
| SHA-1 | ❌ | ~40 billion/s | ❌ Never |
| SHA-256 | ❌ (normally) | ~20 billion/s | ❌ Not for passwords |
| NT Hash (MD4) | ❌ | ~164 billion/s | ❌ Never (legacy only) |
| bcrypt (cost 10) | ✅ | ~25/s | ✅ Acceptable |
| bcrypt (cost 12) | ✅ | ~6/s | ✅ Recommended |
| Argon2id | ✅ | Tunable | ✅ Current best practice |
| scrypt | ✅ | Tunable (memory-hard) | ✅ Strong |

### Hashcat Mode Reference

| Mode (-m) | Hash Type |
|---|---|
| 1000 | NT Hash (NTLM) |
| 5600 | NTLMv2 |
| 1800 | sha512crypt (Linux /etc/shadow) |
| 3200 | bcrypt |
| 0 | MD5 |
| 100 | SHA-1 |
| 1400 | SHA-256 |

### Keylogger Type Quick Reference

| Type | Physical Access Required? | AV Detectable? | Survives OS Wipe? |
|---|---|---|---|
| USB Inline Hardware | ✅ Yes | ❌ No | ✅ Yes |
| API-Based Software | ❌ No | ✅ Usually | ❌ No |
| Kernel-Level Software | ❌ No | ⚠️ Difficult | ❌ No |
| Form Grabber | ❌ No | ⚠️ Difficult | ❌ No |
| Acoustic | ❌ No (mic needed) | ❌ No | ✅ Yes |

### Key Windows Event IDs

| Event ID | Meaning |
|---|---|
| 4624 | Successful logon |
| 4625 | Failed logon |
| 4648 | Logon with explicit credentials |
| 4740 | Account locked out |
| 4771 | Kerberos pre-auth failed |
| 4776 | NTLM authentication attempt |

### MFA Factor Strength (Weakest → Strongest)

SMS OTP → Email OTP → TOTP App → Push Notification → Hardware Token (RSA SecurID) → FIDO2/WebAuthn (YubiKey)


### Key Penalty / Notification Reference

| Regulation | Relevant Rule | Amount / Timeframe |
|---|---|---|
| DPDPA 2023 | Data breach penalty | Up to ₹250 crore |
| DPDPA 2023 | Failure to notify | Up to ₹200 crore |
| IT Act 2000 S.66 | Unauthorised computer access | 3 years + ₹5 lakh |
| IT Act 2000 S.66E | Privacy violation (webcam spyware) | 3 years + ₹2 lakh |
| GDPR | Breach notification window | 72 hours |
| CERT-In | Incident notification window | 6 hours |

---

## ✅ Session Revision Snapshot

**5-Bullet TL;DR:**

1. **Password attacks fall into 4 classes** — Online Active (lockout risk),
   Online Passive (no noise), Offline (no contact — hardest to stop),
   Non-Electronic (human layer) — each needs different countermeasures.

2. **Offline attacks are stopped only by making hashing expensive** —
   bcrypt/Argon2 with salting. Lockout, MFA, and network controls
   are irrelevant once the attacker has the hash file locally.

3. **Keyloggers operate at multiple layers** — hardware (invisible to AV,
   survives wipes), API-level (easy to write, easy to detect), kernel-level
   (hardest to detect), and form-grabbers (bypass HTTPS entirely).

4. **Spyware is broader than a keylogger** — screen, audio, video, GPS,
   files, clipboard. Nation-state spyware (Pegasus) uses zero-click exploits
   and cannot be removed by standard AV — MVT tool is the forensic response.

5. **LAPS + Protected Users Group** are the two key privileged account
   countermeasures for Pass-the-Hash — know both by name, function, and
   what specific attack each blocks.

> 🎯 **MCQ-likely:** bcrypt vs SHA-256, Hashcat mode numbers, account lockout
> vs offline attacks, LAPS function, MFA fatigue attack name, Pegasus delivery
> method, DPDPA penalty amounts, Windows Event IDs.

> 💼 **Interview-likely:** Explain why account lockout doesn't stop offline
> attacks. What is salting and why does it matter. Difference between
> keylogger and spyware. What is LAPS and what attack does it prevent.
> Why is SMS the weakest MFA form.

---

## Next Session Bridge

Session 12A established that **after credentials are stolen, attackers
maintain post-access persistence** using keyloggers and spyware.
Session 12B continues this post-access phase by introducing a more
powerful persistence mechanism: **Trojans and Backdoors** — how attackers
embed persistent remote access into compromised systems using overt/covert
channels, reverse-connecting trojans, and Netcat-based backdoors.
The surveillance capability of keyloggers + spyware pairs directly with
the remote control capability of trojans — together they form the core
of an attacker's post-exploitation toolkit.

---

<details>
<summary>📖 Glossary</summary>

| Term | Definition |
|---|---|
| Account Lockout | Security control that disables an account after N failed login attempts |
| Acoustic Keylogger | Keystroke capture using sound analysis of keyboard key presses |
| Adware | Software displaying unwanted advertisements — may include spyware components |
| Argon2id | Memory-hard password hashing function — winner of PHC 2015 — current best practice |
| bcrypt | Password hashing function with built-in salt and configurable cost factor |
| Brute Force | Exhaustively trying all possible password combinations |
| Credential Stuffing | Using leaked username:password pairs from one breach against other services |
| Dictionary Attack | Password guessing using a wordlist of common/known passwords |
| EDR | Endpoint Detection and Response — real-time endpoint monitoring and threat response |
| FIDO2 | Open standard for hardware security key authentication — phishing resistant |
| Form Grabber | Keylogger variant intercepting browser form data before HTTPS encryption |
| GPU Cracking | Using graphics processors to compute billions of hash candidates per second |
| Hardware Keylogger | Physical device recording keystrokes at the hardware level — AV-invisible |
| HOTP | HMAC-based One-Time Password — counter-based OTP (RFC 4226) |
| LAPS | Local Administrator Password Solution — unique rotating local admin password per machine |
| MFA Fatigue | Attack bombarding user with push MFA requests until they approve one in frustration |
| MVT | Mobile Verification Toolkit by Amnesty International — detects Pegasus IOCs |
| NT Hash | MD4 hash of UTF-16-LE encoded password — used in Windows authentication — unsalted |
| Offline Attack | Password cracking performed on a local copy of stolen hashes — no target contact |
| Online Active Attack | Live authentication attempts against a running service |
| Online Passive Attack | Intercepting credentials without actively authenticating |
| Passphrase | Long password composed of multiple words — strong entropy, easy to remember |
| PassGAN | GAN-based password candidate generator trained on real-world password datasets |
| Password Spraying | Testing one common password across many accounts to avoid per-account lockout |
| Pegasus | NSO Group commercial spyware — zero-click delivery — nation-state grade |
| Pepper | Secret per-application value added to password before hashing — stored separately from DB |
| Protected Users Group | Windows security group disabling NTLM and credential caching for members |
| Rainbow Table | Precomputed hash-to-plaintext lookup table — defeated by salting |
| Salt | Random unique value added to each password before hashing — prevents rainbow tables |
| Shoulder Surfing | Physically observing someone enter their password |
| Spyware | Malware silently collecting and exfiltrating user data and activities |
| Stalkerware | Commercial monitoring software installed on device without subject's knowledge |
| TEMPEST | NATO/NSA standard addressing EM emanation leakage from electronic devices |
| TOTP | Time-based One-Time Password — 30-second rotating code (RFC 6238) |

</details>

---
