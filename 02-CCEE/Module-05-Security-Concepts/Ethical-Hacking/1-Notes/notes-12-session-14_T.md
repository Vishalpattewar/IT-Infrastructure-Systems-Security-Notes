# Session 14 — Viruses, Worms & Antivirus Evasion 🦠

> Personal study notes | Ethical Hacking Module | CCEE Prep

---

## 📑 Table of Contents

- [🗺️ Where This Session Fits](#️-where-this-session-fits)
- [⚠️ Exam Traps & Misconceptions](#️-exam-traps--misconceptions)
- [🧱 Foundation Knowledge](#-foundation-knowledge)
- [Section 1 — Virus vs Worm vs Trojan](#section-1--virus-vs-worm-vs-trojan)
  - [1.1 The Core Distinction](#11-the-core-distinction)
  - [1.2 Three-Way Comparison](#12-three-way-comparison)
  - [1.3 Hybrid Threats](#13-hybrid-threats)
- [Section 2 — How a Virus Works — Lifecycle](#section-2--how-a-virus-works--lifecycle)
  - [2.1 The Four Phases](#21-the-four-phases)
  - [2.2 Infection Mechanisms](#22-infection-mechanisms)
- [Section 3 — Types of Viruses](#section-3--types-of-viruses)
  - [3.1 Boot Sector Virus](#31-boot-sector-virus)
  - [3.2 File Infector Virus](#32-file-infector-virus)
  - [3.3 Macro Virus](#33-macro-virus)
  - [3.4 Network Virus](#34-network-virus)
  - [3.5 Stealth Virus](#35-stealth-virus)
  - [3.6 Polymorphic Virus](#36-polymorphic-virus)
  - [3.7 Metamorphic Virus](#37-metamorphic-virus)
  - [3.8 Multipartite Virus](#38-multipartite-virus)
  - [3.9 Cluster Virus](#39-cluster-virus)
  - [3.10 Sparse Infector Virus](#310-sparse-infector-virus)
  - [3.11 Overwriting Virus](#311-overwriting-virus)
  - [3.12 Cavity (Space-filler) Virus](#312-cavity-space-filler-virus)
  - [3.13 Tunneling Virus](#313-tunneling-virus)
  - [3.14 Armored Virus](#314-armored-virus)
- [Section 4 — Worms](#section-4--worms)
  - [4.1 How Worms Work](#41-how-worms-work)
  - [4.2 Worm Propagation Models](#42-worm-propagation-models)
  - [4.3 Worm Components](#43-worm-components)
- [Section 5 — Antivirus Evasion Techniques](#section-5--antivirus-evasion-techniques)
  - [5.1 Encryption](#51-encryption)
  - [5.2 Polymorphism](#52-polymorphism)
  - [5.3 Metamorphism](#53-metamorphism)
  - [5.4 Code Obfuscation](#54-code-obfuscation)
  - [5.5 Packing / Compression](#55-packing--compression)
  - [5.6 Rootkit Integration](#56-rootkit-integration)
  - [5.7 Timing-Based Evasion](#57-timing-based-evasion)
  - [5.8 Anti-Debugging / Anti-VM Techniques](#58-anti-debugging--anti-vm-techniques)
  - [5.9 File Extension Spoofing](#59-file-extension-spoofing)
  - [5.10 Process Injection](#510-process-injection)
- [Section 6 — Virus Detection Methods](#section-6--virus-detection-methods)
  - [6.1 Signature-Based Detection](#61-signature-based-detection)
  - [6.2 Heuristic-Based Detection](#62-heuristic-based-detection)
  - [6.3 Behavior-Based Detection](#63-behavior-based-detection)
  - [6.4 Integrity Checking / Checksumming](#64-integrity-checking--checksumming)
  - [6.5 Scanning — On-Demand vs On-Access](#65-scanning--on-demand-vs-on-access)
  - [6.6 Interception / Activity Monitoring](#66-interception--activity-monitoring)
  - [6.7 Cloud-Based / Reputation-Based Detection](#67-cloud-based--reputation-based-detection)
  - [6.8 Sandboxing / Dynamic Analysis](#68-sandboxing--dynamic-analysis)
- [📌 Extra Notes](#-extra-notes)
  - [E1 — Mutation Engines — The Arms Race Catalyst](#e1--mutation-engines--the-arms-race-catalyst)
  - [E2 — Famous Real-World Viruses & Worms Timeline](#e2--famous-real-world-viruses--worms-timeline)
  - [E3 — EICAR Test File](#e3--eicar-test-file)
  - [E4 — AV Engine Internal Architecture](#e4--av-engine-internal-architecture)
  - [E5 — False Positive vs False Negative](#e5--false-positive-vs-false-negative)
  - [E6 — Virus Construction Kits](#e6--virus-construction-kits)
  - [E7 — Predecessor / Successor Chains](#e7--predecessor--successor-chains)
  - [E8 — Terminology Traps](#e8--terminology-traps)
  - [E9 — Current Landscape 2026](#e9--current-landscape-2026)
  - [E10 — Indian Legal Context](#e10--indian-legal-context)
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
                            ├── Sessions 6–9 : Concepts, Principles, Hacker Classes 
                            ├── Sessions 10–11 : Recon, Scanning, Enumeration, Passwords, DDoS 
                            ├── Session 12A : Password Countermeasures · Keyloggers · Spyware 
                            ├── Session 12B : Trojans · Backdoors · Types · Reverse Shells 
                            ├── Session 13 : Trojan Construction Kits · Wrapping · Evasion 
                            ├── ▶ SESSION 14 : Viruses · Worms · AV Evasion · Detection Methods 
                            │                                                        ← YOU ARE HERE 
                            └── Sessions 15–20 : Sniffing, DoS, Hijacking, Web Attacks, Malware RE
```


**Phase position:** Session 14 opens the self-replicating malware
sub-phase. While Session 13 covered Trojans (disguise + human
execution), Session 14 introduces autonomous spread — malware that
propagates without the attacker's continued involvement. This is the
fundamental leap from targeted tools to epidemic threats.
After Session 14, the module moves to Sniffing and ARP Poisoning
(Session 15).

---

## ⚠️ Exam Traps & Misconceptions

| ❌ Misconception | ✅ Reality |
|---|---|
| A worm needs a host file to spread | A worm is STANDALONE — it does NOT need a host file. This is the #1 definitional distinction. The VIRUS needs a host file. |
| Polymorphic and metamorphic are the same | Polymorphic encrypts payload + mutates DECRYPTOR STUB. Metamorphic REWRITES ITS ENTIRE CODE — no encryption, no stub. Fundamentally different mechanisms. |
| A stealth virus hides by not infecting many files | Stealth viruses hide by INTERCEPTING OS CALLS — when AV queries the infected file, the virus intercepts the call and returns the clean version. Hiding via reduced infection is a SPARSE INFECTOR. |
| A multipartite virus infects multiple file types | Multipartite infects BOTH BOOT SECTOR AND FILES SIMULTANEOUSLY — not just multiple file types. |
| Signature-based AV catches polymorphic viruses | Signature-based AV FAILS against polymorphic viruses — because no two copies share the same signature. This is the entire purpose of polymorphism. |
| An overwriting virus and a cavity virus both modify file contents | An overwriting virus DESTROYS the original content. A cavity virus fills EMPTY SPACES — the original content is PRESERVED. |
| Heuristic AV has fewer false positives than signature AV | It is the OPPOSITE — heuristic AV has a HIGHER false positive rate because it flags suspicious-LOOKING code that may be legitimate. |
| A cluster virus modifies executable file contents | A cluster virus modifies DIRECTORY ENTRIES — not file contents. The actual files are untouched. |
| Sandboxing is the same as dynamic heuristic emulation | Sandboxing uses a full VIRTUAL MACHINE. Dynamic emulation uses a lightweight VIRTUAL CPU built into the AV engine. Different resource levels. |
| EICAR is a real virus used for AV testing | EICAR is a HARMLESS 68-byte file — not a virus. No malicious code. It triggers AV by agreement among AV vendors as a compliance test. |

---

## 🧱 Foundation Knowledge

<details>
<summary>Click to expand — Must-know before this session</summary>

**How Executable Files Are Structured (PE Format)**

- PE = Portable Executable — format for `.exe`, `.dll`, `.sys`, `.com`
- Contains: DOS header → PE header → Section headers → Sections
- Key sections:
  - `.text` — executable code
  - `.data` — initialized data
  - `.rsrc` — embedded resources (icons, strings)
  - `.reloc` — relocation table
- AV scanners examine `.text` section bytes for signatures
- Boot sector viruses target the MBR — outside the PE format entirely

**Interrupt Handling — Relevant to Virus Types**

- BIOS INT 13h — disk read/write interrupt
- DOS INT 21h — general file I/O interrupt
- Stealth viruses hook these interrupts to intercept disk reads
- Tunneling viruses bypass AV hooks by going DIRECTLY to these interrupts
- Understanding interrupt layers explains why certain viruses survive
  OS reinstallation and why certain detection methods fail

**Cryptographic Hashes — File Identity**

- Same file = same hash always (deterministic)
- Any change to file = completely different hash (avalanche effect)
- MD5 (128-bit) — fast — broken for collision resistance — used only for ID
- SHA-1 (160-bit) — deprecated
- SHA-256 (256-bit) — current standard
- AV vendors share malware IOCs as SHA-256 hashes

**MITRE ATT&CK Reference**

- T1204.002 — User Execution: Malicious File (virus activation)
- T1027.002 — Software Packing (packers)
- T1027 — Obfuscated Files or Information
- T1027.010 — Obfuscate via Polymorphism/Metamorphism
- T1497 — Virtualization/Sandbox Evasion
- T1055 — Process Injection
- T1210 — Exploitation of Remote Services (worm propagation)

</details>

---

## Section 1 — Virus vs Worm vs Trojan

### 1.1 The Core Distinction

**WHAT:**
These are the three primary malware categories. Their distinctions
are based on three axes: whether they need a host file, whether
they self-replicate, and whether they need human action to spread.

**WHY this matters:**
MCQs constantly mix and invert these properties. Every single
MCQ on this topic is testing whether you know the precise
technical definition — not a vague description.

**The One-Line Test:**
VIRUS → needs a host file + needs human to execute it → then spreads WORM → no host file + no human action needed → spreads automatically TROJAN → disguised as something legitimate → does NOT self-replicate



**Analogy:**
- **Virus** = flu virus. It needs a human host body to exist
  and spread. Someone has to cough near you (execute the infected
  file) for you to catch it. It cannot travel on its own.
- **Worm** = a rumour spreading in school. Once started, it
  travels from person to person on its own — nobody needs to
  actively pass it along. It just spreads through the network
  of people.
- **Trojan** = the Trojan Horse from Greek mythology. It looks
  like a gift (game, installer, tool) — it does NOT make copies
  of itself — but once inside the gates, it lets the attackers in.

---

### 1.2 Three-Way Comparison

| Property | Virus | Worm | Trojan |
|---|---|---|---|
| **Self-replicating?** | ✅ Yes | ✅ Yes | ❌ No |
| **Needs host file?** | ✅ Yes | ❌ No | ✅ (disguised as legit) |
| **Spreads automatically?** | ❌ Needs user action | ✅ Yes | ❌ Needs user to install |
| **Primary intent** | Infect + spread | Spread + consume resources | Provide backdoor access |
| **Contains payload?** | Usually | Sometimes | Always |
| **Propagation medium** | Executable files, boot sectors, macros | Network, OS vulnerabilities | Social engineering |
| **Attacker involvement post-deploy** | None needed | None needed | Ongoing (C2) |
| **Classic example** | CIH/Chernobyl | Morris Worm | Back Orifice |

> [!IMPORTANT]
> The most commonly reversed MCQ trap:
> **"A worm requires a host file"** → FALSE. That's the VIRUS.
> **"A virus spreads automatically"** → FALSE. It needs user execution.

---

### 1.3 Hybrid Threats

Modern malware often combines properties of multiple categories:

| Hybrid | Example | Properties Combined |
|---|---|---|
| **Worm + Virus** | ILOVEYOU | Spreads like a worm (email) + infects files like a virus |
| **Worm + Trojan** | Conficker | Self-replicates like a worm + installs backdoor like a Trojan |
| **Worm + Ransomware** | WannaCry | Self-propagates like a worm + encrypts like ransomware |
| **Virus + Rootkit** | Rustock | File infector + kernel-level hiding |

> [!NOTE]
> In exams, when a hybrid is described, identify the PRIMARY
> classification based on its DOMINANT characteristic —
> propagation method (virus/worm) or intent (Trojan/ransomware).

---

## Section 2 — How a Virus Works — Lifecycle

### 2.1 The Four Phases

**WHAT:**
Every virus goes through a predictable lifecycle. Understanding
these phases explains when and why viruses become detectable,
when they cause damage, and which phase certain AV methods target.

**WHY:**
Phase-based MCQs ask: "A virus is present but causing no damage —
which phase?" or "When does the payload execute?"
```
[ DORMANT PHASE ] 
      ↓ 
Virus is on the system — inactive Waiting for a trigger condition to be met (Specific date, counter value, system event) Not all viruses have this phase 
      ↓ 
[ PROPAGATION PHASE ] 
      ↓ 
Virus actively copies itself into: → Other executable files → Boot sectors → Network shares → Removable media Replication continues regardless of payload trigger 
      ↓ 
[ TRIGGERING PHASE ] 
      ↓ 
Trigger condition met: → Specific date (Friday 13th virus) → File access count reached → Specific program executed → System event (boot count) Virus transitions from passive to active 
      ↓ 
[ EXECUTION PHASE ] 
      ↓ 
Payload runs: → File deletion / corruption → Encryption (ransomware behaviour) → Display message → BIOS overwrite (CIH) → Data exfiltration → System crash
```


| Phase | Key MCQ Fact |
|---|---|
| **Dormant** | Present but inactive — not all viruses have this phase |
| **Propagation** | Virus replicates — damage has NOT yet occurred |
| **Triggering** | Activation condition met — distinct from execution |
| **Execution** | Payload runs — actual damage occurs here |

> [!NOTE]
> Time-bomb viruses (e.g., CIH triggering April 26th) exploit the
> DORMANT phase — they spread widely during dormancy and then
> execute simultaneously when the date arrives.

---

### 2.2 Infection Mechanisms

How viruses actually infect files — three approaches:

| Mechanism | How It Works | File Size Change? | Original File? |
|---|---|---|---|
| **Prepending** | Viral code inserted at START of file — jumps to original after running | ✅ Increases | ✅ Preserved |
| **Appending** | Viral code added to END of file — entry point redirected | ✅ Increases | ✅ Preserved |
| **Overwriting** | Viral code REPLACES original content at start | ❌ May not change | ❌ Destroyed |
| **Cavity (Space-filling)** | Viral code fills EMPTY SECTIONS in PE structure | ❌ No change | ✅ Preserved |

> [!IMPORTANT]
> Cavity viruses are the hardest to detect by file-size monitoring
> because they do NOT increase the file size. CIH (Chernobyl) is
> the canonical example of a cavity virus.

---

## Section 3 — Types of Viruses

### 3.1 Boot Sector Virus

**WHAT:**
Infects the **Master Boot Record (MBR)** or **Volume Boot Record (VBR)**
— the first sector of the storage device that the BIOS reads to start
the OS boot process.

**WHY it's dangerous:**
The MBR executes BEFORE the operating system loads — and therefore
before any AV software can initialize. The virus is running with full
hardware access before any defence is active.

**HOW:**
BIOS → reads first sector of disk (MBR) → MBR virus code runs (in memory before OS) → Virus loads original MBR to another sector → Chains to original MBR to boot normally → User sees normal boot — virus is resident in memory → Any disk accessed → virus copies itself to new media



**Spread vector:** Infected bootable media (floppy disks historically,
USB drives today). User boots from infected media — MBR is replaced.

**Survival:** Boot sector viruses SURVIVE OS reinstallation
if the MBR is not explicitly wiped. A new OS installation does
not overwrite the MBR by default.

**Removal:** Requires low-level disk tools:
- Windows: `bootrec /fixmbr` (overwrites MBR with clean code)
- Windows XP: `fdisk /MBR`
- Linux: `dd if=/dev/zero of=/dev/sda bs=446 count=1`

**Examples:** Michelangelo, Stoned, Elk Cloner (Apple II), Brain (first PC virus)

> [!WARNING]
> Brain (1986) was the first IBM PC virus. It was a boot sector virus
> that also used stealth — intercepting disk reads to hide itself.
> It was written by two Pakistani brothers (Basit and Amjad Farooq
> Alvi) — reportedly to track piracy of their medical software.

**MITRE ATT&CK:** T1542.003 — Pre-OS Boot: Bootkit

---

### 3.2 File Infector Virus

**WHAT:**
Attaches itself to **executable files** — `.exe`, `.com`, `.sys`,
`.dll` — and activates when the infected file is executed.

**Types of file infectors:**

| Sub-type | Mechanism |
|---|---|
| **Prepending infector** | Adds viral code at START of file |
| **Appending infector** | Adds viral code at END of file |
| **Overwriting infector** | Replaces original file content |
| **Companion virus** | Creates a new file with same name but different extension (e.g., `notepad.com` alongside `notepad.exe`) — `.com` executes first in DOS |

**Spread:** Every time the infected executable is run,
the virus checks other executables in accessible directories
and infects them. Spreads via shared drives, email attachments,
downloaded software.

**Examples:** Jerusalem (Friday the 13th), Vienna, Cascade

**Most common virus type overall** — forms the basis for most
textbook virus discussions.

---

### 3.3 Macro Virus

**WHAT:**
Infects **macro-enabled documents** — primarily Microsoft Office files
(`.doc`, `.docm`, `.xls`, `.xlsm`, `.ppt`) — by embedding malicious
**VBA (Visual Basic for Applications)** macros.

**WHY it was so effective:**
- Documents are shared constantly via email and network shares
- People DO run documents — unlike random `.exe` files
- Macro language (VBA) is powerful — full file system + network access
- Cross-platform — same infected Word doc works on Windows and macOS

**HOW:**
Victim opens infected Word document → Document has auto-execute macro (AutoOpen, Document_Open) → Macro runs automatically on document open → Macro infects Normal.dot (global template) → ALL future documents opened become infected → Macro sends infected documents to email contacts (Melissa — first 50 contacts) → Payload executes (file corruption, further propagation)



**Key details:**
- **Normal.dot** = Word's global template — infecting it means
  every new Word document created is infected
- **AutoOpen** and **Document_Open** are VBA event handlers that
  auto-execute when document opens — no manual macro run needed
- Microsoft disabled macros by default in 2022 for internet-
  downloaded files — but macro viruses still spread via
  internal networks and trusted document shares

**Examples:** Melissa (1999), Concept (1995 — first macro virus),
Cap, Wazzu

> [!TIP]
> Melissa is the textbook macro virus MCQ example. Know:
> - Type: Macro virus (VBA)
> - Target: Microsoft Word documents
> - Year: 1999
> - Spread: Emailed infected .doc to first 50 Outlook contacts
> - Author: David L. Smith — sentenced to 20 months federal prison

**MITRE ATT&CK:** T1566.001 — Spearphishing Attachment (delivery)
T1059.005 — Visual Basic (execution)

---

### 3.4 Network Virus

**WHAT:**
Spreads across **network shares and mapped drives** — replicates
by copying itself to accessible network locations.

**HOW:**
Virus on infected machine scans network shares → finds accessible drives → copies itself to executable files on those shares → when other users access and run those files → they become infected.

**Key distinction from worm:**
A network virus STILL NEEDS A HOST FILE and STILL NEEDS USER
EXECUTION. It uses the network as a TRANSPORT MEDIUM — not as
an autonomous exploitation mechanism. This is the most common
MCQ trap involving network viruses.

| | Network Virus | Worm |
|---|---|---|
| Needs host file? | ✅ Yes | ❌ No |
| Needs user execution? | ✅ Yes | ❌ No |
| Uses network? | ✅ Yes | ✅ Yes |

---

### 3.5 Stealth Virus

**WHAT:**
Actively **hides its own presence** from the OS and AV software
by intercepting OS/BIOS calls that would expose the infection.

**WHY:**
AV software detects viruses by reading files and comparing to
known signatures. If the virus intercepts those read operations
and returns the clean, original version — the AV sees nothing.

**HOW:**
Normal scenario (no stealth): AV requests → OS → reads infected file → AV sees viral code → DETECTED

Stealth virus scenario: AV requests → OS → VIRUS INTERCEPTS REQUEST → virus returns original, clean version of file → AV sees clean content → NOT DETECTED



**Two stealth levels:**

| Level | What It Hides |
|---|---|
| **Full stealth** | Hides file size increase AND file content changes |
| **Partial stealth** | Hides only file content changes — file size change still visible |

**Critical weakness:**
Stealth viruses MUST BE ACTIVE IN MEMORY to intercept calls.
If you boot from a **clean, write-protected boot disk** and scan —
the virus is NOT loaded into memory — the interceptor is not running —
the infected files are visible in their real state.

**Examples:** Brain (1986 — first stealth), 4096 (Frodo),
Number of the Beast

> [!NOTE]
> This is why early AV vendors always instructed users to boot
> from a clean floppy disk before scanning. The same principle
> applies today — offline scanning from a bootable AV USB drive
> bypasses in-memory stealth mechanisms.

---

### 3.6 Polymorphic Virus

**WHAT:**
Changes its own **encryption key and decryption stub** with each
new infection — while keeping the original payload functionality
identical — producing a different binary signature every time.

**WHY:**
Signature-based AV detects a virus by matching specific byte
patterns. If every copy of the virus has a different signature —
the AV database cannot contain a signature that matches any of them.

**HOW:**
Original payload (malicious code) ↓ Encrypted with Key-A → produces Variant 1 Variant 1 = [Encrypted Payload-A] + [Decryptor Stub Version 1]

Next infection: Original payload encrypted with Key-B → produces Variant 2 Variant 2 = [Encrypted Payload-B] + [Decryptor Stub Version 2]

Variant 1 signature ≠ Variant 2 signature ≠ Variant 3 signature → No single AV signature can match all variants → Millions of infections, millions of unique signatures



**What stays the same:** Underlying malicious BEHAVIOUR
**What changes:** The ENCRYPTION KEY and the DECRYPTION STUB code

**Tools used:** **Mutation Engine (MtE)** — a reusable module
that generates new decryption stubs for each infection.

**Examples:** Cascade, Tequila, Storm Worm, Virut

**MITRE ATT&CK:** T1027.010 — Obfuscate via Polymorphism

---

### 3.7 Metamorphic Virus

**WHAT:**
Goes further than polymorphic — **rewrites its ENTIRE CODE** on
each infection using code transformation techniques — without
any encryption. The code does the same thing but the instructions
are structurally different every time.

**WHY:**
Polymorphic viruses still have a decryption stub — and even a
mutating stub eventually shows patterns that AV can detect.
Metamorphic viruses eliminate encryption entirely — there is no
stub, no consistent structure, no stable pattern at all.

**HOW — Code Transformation Techniques:**

| Technique | Example |
|---|---|
| **Code transposition** | Reorder independent instructions without changing logic |
| **Instruction substitution** | Replace `MOV EAX, 0` with `XOR EAX, EAX` (same effect) |
| **Dead code insertion** | Add `NOP`, random pushes/pops that do nothing |
| **Register renaming** | Use EBX instead of EAX for the same variable |
| **Subroutine reordering** | Change the order of function definitions |
| **Equivalent code substitution** | Replace `ADD EAX, 1` with `INC EAX` |
Infection 1: MOV EAX, 5 ADD EAX, 3 PUSH EAX

Infection 2 (same logic, different code): XOR EBX, EBX ADD EBX, 8 NOP PUSH EBX



**What stays the same:** Functional OUTCOME (result = 8, pushed)
**What changes:** Every instruction, every register, every order

**Examples:** Zmist (most complex), Simile (W32/Evol), W32/Evol

> [!IMPORTANT]
> **The single most important exam distinction:**
>
> | | Polymorphic | Metamorphic |
> |---|---|---|
> | Encryption used? | ✅ Yes | ❌ No |
> | What changes? | Decryption stub | Entire code body |
> | Stub needed? | ✅ Yes | ❌ No |
> | Harder to detect? | Moderate | Very hard |

---

### 3.8 Multipartite Virus

**WHAT:**
Infects **BOTH** the boot sector **AND** executable files
simultaneously — a dual-vector infection strategy.

**WHY it's harder to remove:**
If you clean only the infected files but not the boot sector —
the boot sector re-infects the files on next boot.
If you clean only the boot sector but not the files —
an infected file re-infects the boot sector when executed.
Both vectors must be cleaned simultaneously.

**Analogy:**
Multipartite virus = a house fire that starts in both the kitchen
AND the roof simultaneously. Putting out only the kitchen fire
while the roof burns means the fire returns. Both must be
extinguished together.

**Examples:** Ghostball (first multipartite virus, 1989),
Invader, Tequila, Junkie

---

### 3.9 Cluster Virus

**WHAT:**
Also called **file system virus**. Does NOT modify file contents —
instead modifies **FAT (File Allocation Table) or directory entries**
to redirect execution through the virus code first.

**HOW:**
Normal execution: Directory entry for notepad.exe → points to notepad.exe start → notepad.exe runs

Cluster virus infection: Directory entry for notepad.exe → REDIRECTED to virus code location → Virus code runs first → then chains to original notepad.exe → User sees notepad running — virus has executed



**Key property:**
The original files are UNTOUCHED. A file integrity check on the
actual executable finds no modification. Only a directory/FAT
examination reveals the infection.

**One copy:** Because it works via directory redirection, only ONE
copy of the virus code exists on disk — pointed to by all infected
directory entries. Appears to have one infection; effectively affects
every executable.

---

### 3.10 Sparse Infector Virus

**WHAT:**
Infects **selectively** — not every executable it encounters.
Reduces its own infection frequency to limit detection probability.

**Criteria used to decide whether to infect:**
- Every nth file accessed (e.g., every 10th execution)
- Only files above/below a certain size
- Only on specific dates or times
- Random probability (10% chance per file accessed)

**WHY:**
AV behavioural monitoring and heuristics look for unusual
patterns — a virus that infects every file is noisy.
Sparse infection means fewer changes, fewer triggers, longer
time before detection.

**Examples:** Trivial.88.D, W95/Tenrobot

---

### 3.11 Overwriting Virus

**WHAT:**
Writes its own code directly OVER the beginning of a file,
**destroying the original content** permanently.

**Characteristics:**
- Infected files NO LONGER FUNCTION — they crash or produce errors
- Easy to detect — broken files are obvious
- Cannot disinfect — original code is gone — file must be deleted
- Simplest virus type to write — no need for infection logic

**Examples:** Trivial.88.D, W95/HPS (partially overwriting)

> [!NOTE]
> Overwriting viruses are the least sophisticated and easiest to
> detect because the original program stops working — users notice
> immediately. Compare to cavity viruses — which preserve the
> original program and are far harder to notice.

---

### 3.12 Cavity (Space-filler) Virus

**WHAT:**
Inserts itself into **empty sections and slack space** within
executable files — without increasing the file size.

**HOW:**
PE (Portable Executable) files frequently contain sections with
empty (zero-filled) regions — gaps between sections, unused
space at end of sections. The cavity virus maps its code into
these gaps.
Original file structure: [PE Header][.text section][00 00 00 00 00][.data section] ^^^^^^^^^^^^ Empty cavity space

After cavity virus infection: [PE Header][.text section][VIRUS CODE ][.data section]



**Key property:**
File size does NOT change — any detection method based on
file size comparison is defeated.

**The canonical example:**
**CIH (Chernobyl Virus):**
- Year: 1998
- Author: Chen Ing-hau (Taiwan)
- Type: Cavity file infector
- Trigger: April 26 (anniversary of Chernobyl disaster)
- Payload: Overwrote first 1MB of hard disk AND attempted
  to overwrite BIOS flash chip — rendering machine completely
  unbootable (hardware damage requiring BIOS chip replacement
  in early systems)
- Impact: ~$250 million in damage, millions of machines affected

> [!IMPORTANT]
> CIH is the only virus in this syllabus that caused
> **hardware-level damage** (BIOS overwrite). This is always
> an MCQ distractor — "which virus damaged hardware?"

**MITRE ATT&CK:** T1027.005 — Indicator Removal from Tools

---

### 3.13 Tunneling Virus

**WHAT:**
Attempts to **bypass AV interceptors** by going directly to
underlying BIOS or DOS interrupt handlers — tunneling beneath
the OS call layer where AV monitors operate.

**HOW:**
AV monitors hook OS-level interrupts: INT 21h (DOS file I/O) → AV sees every file access INT 13h (BIOS disk I/O) → AV sees every disk access

Normal virus: File access request → OS interrupt → AV hook fires → DETECTED

Tunneling virus: File access request → BYPASSES OS interrupt → Goes directly to BIOS INT 13h → AV hook on OS interrupt NEVER FIRES → Virus reads/writes disk → NOT DETECTED



**Challenge:**
Countering tunneling viruses requires AV tools to also hook
at the BIOS level — significantly more complex and
OS-version-dependent.

---

### 3.14 Armored Virus

**WHAT:**
Uses **protective techniques** to make the virus code difficult
to reverse engineer, disassemble, and analyze — protecting
the virus from AV researcher analysis.

**Techniques used:**

| Technique | How It Works |
|---|---|
| **Misleading disassembly** | Code contains junk bytes that cause disassemblers to produce incorrect output |
| **Anti-debugging traps** | Code that crashes or alters behaviour when a debugger is attached |
| **Encrypted internal logic** | Key sections of virus code are encrypted — analyst must fully reverse to understand |
| **Self-modification** | Code modifies itself during execution — static analysis is always incomplete |
| **Complex control flow** | Deeply nested jumps, indirect calls, opaque predicates |

**Goal:** Not to evade AV detection during infection — but to
slow down AV researchers analyzing the virus — delaying signature
creation and countermeasure development.

**Example:** Whale virus (1990) — famous for its extreme complexity,
defeating early analysis tools completely for weeks

---

## Section 4 — Worms

### 4.1 How Worms Work

**WHAT:**
A worm is a self-contained, self-replicating malicious program
that spreads across networks by **exploiting vulnerabilities**
in operating systems, network services, or applications —
without requiring a host file or human execution.

**WHY worms are epidemic threats:**
Once one machine is infected, the worm scans for other vulnerable
machines and infects them — which then scan for more — exponential
growth with no attacker involvement required after initial release.

**Analogy:**
A worm is like a biological virus with airborne transmission.
The flu virus needs a host (virus = infected file). A truly
airborne pathogen like measles requires NO physical contact —
just proximity to the network. One infected person in a room
infects everyone present automatically.

**HOW — Generic Worm Operation:**
```
Initial infection (one vulnerable machine): 
Worm code executes on Machine A 
            ↓ 
Worm scans network for other vulnerable targets (Checks specific port, sends probe, checks OS version) 
            ↓ 
Finds Machine B (vulnerable) 
            ↓ 
Exploits vulnerability → copies itself to Machine B 
            ↓  
Machine B now infected → also starts scanning 
            ↓ 
Machine A + Machine B now both scanning → exponential spread 
            ↓ 
Optional payload: Drop Trojan backdoor, launch DDoS, encrypt files, consume bandwidth
```


**Key capabilities worms exploit:**
- Buffer overflow vulnerabilities (Morris Worm, Code Red, Blaster)
- Email system vulnerabilities (Sobig, Sasser)
- Network file sharing (Conficker)
- Web application vulnerabilities (Code Red — IIS)
- Default credentials (Mirai botnet — IoT devices)

---

### 4.2 Worm Propagation Models

> [!NOTE]
> Propagation models are studied in network security literature
> and tested in MCQs about which model achieves fastest spread.

| Model | How It Works | Speed | Detectability |
|---|---|---|---|
| **Random Scanning** | Worm probes random IP addresses from entire IPv4 space | Slow initially | High (noisy — many probes) |
| **Sequential Scanning** | Worm scans IPs sequentially from its own IP outward | Predictable | Medium |
| **Topological Scanning** | Uses data on infected host (email contacts, ARP table, browser history) to find next targets | Targeted | Low |
| **Hit-list Scanning** | Pre-compiled list of known vulnerable targets — attacks list first | **Fastest initial spread** | Low initially |
| **Permutation Scanning** | All infected worm instances share a pseudo-random permutation of IP space — no duplicate scanning | Fast + efficient | Low |

> [!IMPORTANT]
> **Hit-list scanning** produces the fastest initial explosive growth
> because the worm starts with confirmed vulnerable targets.
> Code Red II used a variant of this. The hit-list is compiled by
> the attacker BEFORE releasing the worm.
>
> **Topological scanning** produces the most targeted infections
> with the lowest network noise — hardest to detect via traffic analysis.

---

### 4.3 Worm Components

A fully featured worm consists of distinct functional modules:

| Component | Function |
|---|---|
| **Reconnaissance module** | Scan for vulnerable targets — port scanning, service probing |
| **Exploit module** | Exploit the specific vulnerability to gain execution on target |
| **Propagation module** | Copy worm code from infected host to new target |
| **Payload module** | Deliver intended damage — DDoS, backdoor, ransomware, spamming |
| **Persistence module** | Ensure worm survives reboots — registry keys, scheduled tasks |
| **C2 module** | Contact attacker's command server — receive updated instructions |
| **Self-update module** | Download updated versions of worm from C2 — patch against removal |

---

## Section 5 — Antivirus Evasion Techniques

### 5.1 Encryption

**WHAT:**
Virus encrypts its payload using a key — only the small
**decryption stub** (plaintext) is visible. AV sees encrypted
data + small stub — no signature match.

**HOW:**
```
Plaintext malicious payload 
      ↓ 
encrypted with Key-X Encrypted blob (no signature) + Small decryption stub (plaintext — runs first) 
      ↓ 
At runtime: stub decrypts blob in memory → executes payload 
      ↓ 
AV scans disk → sees encrypted blob + small stub → no match
```



**Limitation:**
The decryption stub ITSELF becomes a consistent, detectable
signature — AV vendors extract it. This leads to polymorphism.

---

### 5.2 Polymorphism

**WHAT:**
Mutation engine changes the **decryption stub** on every
infection — so no two copies share the same decryptor signature.

**Evasion achieved:**
Signature database cannot contain a signature that matches
all variants — would require infinite database entries.
Forces AV vendors toward heuristic/behaviour-based detection.

**Deep dive:** See Section 3.6 above.

---

### 5.3 Metamorphism

**WHAT:**
Entire code **rewrites itself** using code transformation —
no encryption, no stub, no consistent structure at all.

**Evasion achieved:**
Even heuristic engines that look for patterns in decryption
stubs find nothing — there is no stub. Every instruction
may be different. Requires ML-based or behaviour-based
detection to catch.

**Deep dive:** See Section 3.7 above.

---

### 5.4 Code Obfuscation

**WHAT:**
Transforms code to be difficult to read and analyze — without
changing its functionality.

**Techniques:**

| Technique | How It Works |
|---|---|
| **Variable/function renaming** | Replace meaningful names (`downloadPayload`) with noise (`_x3f7a`) |
| **Dead code insertion** | Add NOP sleds, meaningless calculations, unreachable branches |
| **String splitting** | `"cmd.exe"` → `"cm" + "d" + ".exe"` decoded at runtime |
| **Base64 encoding** | Commands encoded in Base64 — decoded at runtime |
| **XOR encoding** | Strings XOR'd with a key — decoded at runtime |
| **Control flow flattening** | Replace if/else logic with complex switch/dispatch tables |
| **Opaque predicates** | Conditions that always evaluate same way but look complex to analyzer |

**Obfuscation is NOT encryption:**
- No key required
- Trivially reversible with deobfuscation tools
- Increases ANALYSIS TIME — does not provide strong confidentiality
- Often used in PowerShell scripts for fileless attack delivery

---

### 5.5 Packing / Compression

**WHAT:**
Executable is **compressed** using a packer. A small stub
decompresses the original code in memory at runtime.
The on-disk binary is completely different from the original.

**HOW:**
```
Original virus.exe → known AV signature → DETECTED 
              ↓ 
UPX packer applied 
              ↓  
packed_virus.exe → different bytes entirely → NO SIGNATURE MATCH 
              ↓ 
At runtime: UPX stub decompresses → original code runs in memory
```


**Common packers:**

| Packer | Notes |
|---|---|
| **UPX** (Ultimate Packer for eXecutables) | Open-source, legitimate — most abused packer historically |
| **MPRESS** | Less common — slightly better AV bypass than UPX |
| **ASPack** | Commercial packer — abused in malware |
| **Custom packers** | Attacker-written — most effective — no known signature |

> [!NOTE]
> AV tools now detect UPX-packed malware specifically.
> Modern malware uses CUSTOM packers or stacked packers
> (packed with packer A, then packed again with packer B)
> to defeat AV unpackers.

**MITRE ATT&CK:** T1027.002 — Software Packing

---

### 5.6 Rootkit Integration

**WHAT:**
Malware installs a **rootkit** to hide its own processes, files,
and registry entries from the operating system itself.

**HOW:**
Without rootkit: AV asks OS: "List all files in C:\Windows\System32" OS returns: [all files including virus.exe] AV finds: virus.exe → DETECTED

With rootkit: Rootkit hooks OS kernel function (SSDT hook) AV asks OS: "List all files in C:\Windows\System32" OS → rootkit intercepts → removes virus.exe from list AV receives: [all files EXCEPT virus.exe] AV finds: nothing → NOT DETECTED



**Detection of rootkits:**
- Compare kernel view vs raw disk view (RootkitRevealer)
- Boot from clean media — rootkit not loaded
- Memory forensics (Volatility)
- Cross-view detection tools (GMER)

---

### 5.7 Timing-Based Evasion

**WHAT:**
Malware **delays execution** to outlast sandbox analysis windows
— or waits for specific conditions before activating.

**HOW:**
```
Sandbox analysis: typical runtime = 2–5 minutes 
            ↓ 
Malware detects it is being analyzed: → Calls Sleep(600000) → sleeps 10 minutes → Sandbox times out → reports "no malicious behaviour" → Malware passes analysis → delivered to victim → After 10 minutes → payload executes on real system
```


**Other timing techniques:**
- Wait for specific system uptime (sandboxes freshly boot each sample)
- Check system date — only execute after specific date
- Execute only between specific hours (business hours)
- Wait for user input (mouse movement, keypress) before activating

---

### 5.8 Anti-Debugging / Anti-VM Techniques

**WHAT:**
Malware detects whether it is running inside a debugger,
virtual machine, or sandbox — and behaves differently
(or exits cleanly) when analysis environment is detected.

**Detection methods:**

| Technique | What It Detects | How |
|---|---|---|
| **IsDebuggerPresent()** | Windows debugger | Win32 API call — returns TRUE if debugger attached |
| **NtQueryInformationProcess** | Debugger (advanced) | Lower-level check — harder to patch |
| **RDTSC timing** | VM/emulator (slower execution) | Measure time between two RDTSC reads — large delta = VM |
| **VMware registry keys** | VMware VM | Check `HKLM\SOFTWARE\VMware, Inc.\VMware Tools` |
| **VirtualBox drivers** | VirtualBox VM | Check for `VBoxGuest.sys`, `VBoxMouse.sys` |
| **MAC address prefix** | VMware (`00:0C:29`), VirtualBox (`08:00:27`) | Known OUI assignments for virtual NICs |
| **Sandbox usernames** | Cuckoo, Any.Run | Check username for "sandbox", "maltest", "virus" |
| **Sandbox file paths** | Known sandbox artefacts | Check for specific analysis tool paths |
| **CPUID hypervisor bit** | Any hypervisor | CPUID instruction returns hypervisor present bit |
| **Screen resolution** | Automated sandbox | Most sandboxes run 800×600 or 1024×768 |
| **Running processes** | Analysis tools | Check for Wireshark, Procmon, OllyDbg, IDA Pro |

> [!TIP]
> `00:0C:29` is VMware's MAC address OUI (Organizationally Unique
> Identifier). Malware checks network adapter MAC addresses for
> this prefix to detect VMware environments. When building
> analysis VMs, change MAC address prefix to avoid this detection.

**MITRE ATT&CK:** T1497 — Virtualization/Sandbox Evasion

---

### 5.9 File Extension Spoofing

**WHAT:**
Malware disguises itself as a legitimate, harmless file type
by manipulating how its filename appears to users.

**Methods:**

**Method 1 — Double extension:**
`invoice.pdf.exe`
→ Windows hides known extensions by default
→ Appears as `invoice.pdf` in Explorer
→ User double-clicks thinking it's a PDF → executes malware

**Method 2 — Unicode RLO (Right-to-Left Override):**
The Unicode character U+202E reverses the display direction
of following characters.
Filename on disk: photo_[RLO]gpj.exe Displayed to user: photo_exe.jpg

→ User sees a .jpg filename → double-clicks → executes .exe

**Method 3 — Homoglyph attack:**
Replace letters with visually identical Unicode characters:
`paypal.com` → `paypa|.com` (pipe vs lowercase L)
`microsoft.com` → `mіcrosoft.com` (Cyrillic і vs Latin i)

> [!WARNING]
> Windows Explorer hides known file extensions by default.
> This is a long-standing security weakness that enables
> double-extension spoofing. Best practice: configure
> Explorer to show all file extensions.
> `Folder Options → View → Uncheck "Hide extensions for known file types"`

---

### 5.10 Process Injection

**WHAT:**
Malicious code **injects itself into a legitimate, trusted
process** — running inside that process's memory space.

**WHY:**
AV tools and security products whitelist known-good processes
like `explorer.exe`, `svchost.exe`, `notepad.exe`. If malware
runs inside one of these processes, security tools see only
the trusted process — not the malicious code.

**Types of Process Injection:**

| Type | Mechanism |
|---|---|
| **DLL Injection** | Write malicious DLL path to target process → call LoadLibrary → DLL loaded into target |
| **Process Hollowing** | Create legitimate process in suspended state → hollow out its code → replace with malicious code → resume |
| **Thread Hijacking** | Suspend a thread in target process → overwrite instruction pointer → resume — thread now executes malicious code |
| **Reflective DLL Injection** | DLL loads itself from memory without touching disk — no LoadLibrary trace |
| **APC Injection** | Queue Asynchronous Procedure Call to target thread — executes malicious shellcode |

**Detection:**
Process Explorer (Sysinternals) — shows if a process has
unexpected DLLs loaded or unusual memory regions marked executable.

**MITRE ATT&CK:** T1055 — Process Injection

---

## Section 6 — Virus Detection Methods

### 6.1 Signature-Based Detection

**WHAT:**
AV maintains a **database of known malware signatures** — specific
byte sequences, hash values, or byte patterns unique to known
malware — and compares every scanned file against this database.

**HOW:**
```
AV database: { "68 65 6C 6C" = Virus.X, "4D 5A 90 00" + "60 BE" = Virus.Y, ... } 
↓ 
Scanned file bytes: [ ... 68 65 6C 6C ... ] 
↓ 
Match found: Virus.X → ALERT
```


**Characteristics:**

| Property | Detail |
|---|---|
| **Speed** | Fast — simple byte comparison |
| **False positive rate** | Low — exact match only |
| **False negative rate** | High for new/modified malware |
| **Requires updates?** | Yes — constantly — new signatures daily |
| **Catches zero-day?** | ❌ No |
| **Catches polymorphic?** | ❌ No |
| **Catches metamorphic?** | ❌ No |

> [!IMPORTANT]
> Signature-based detection is the **oldest, most common, and most
> limited** AV method. It is always correct for what it knows —
> but completely blind to what it doesn't know yet.

---

### 6.2 Heuristic-Based Detection

**WHAT:**
Analyzes code for **suspicious characteristics** without needing
a known signature — looks for code patterns that RESEMBLE malware
behaviour without being a known malware sample.

**Two forms:**

**Static Heuristics:**
- Examines code structure WITHOUT executing it
- Looks for: suspicious API call sequences, self-modification code,
  encrypted sections, unusual PE header values, known packer signatures
- Fast — no execution needed
- Can be fooled by obfuscation

**Dynamic Heuristics (Emulation):**
- Runs code inside a lightweight VIRTUAL CPU built into the AV engine
- Observes what instructions execute, what API calls are made
- Limits emulation to a few thousand instructions (performance constraint)
- Can unpack packed malware and detect the real payload underneath
- Can be fooled by anti-emulation (long sleep, environment check)

**Characteristics:**

| Property | Detail |
|---|---|
| **False positive rate** | Higher than signature-based |
| **Catches new malware?** | Partially — if it resembles known patterns |
| **Catches polymorphic?** | Dynamic form can unpack and detect |
| **Catches zero-day?** | Partially — novel malware may not trigger heuristics |

---

### 6.3 Behavior-Based Detection

**WHAT:**
Monitors **actual runtime actions** of programs on the live
system — flags anything that exhibits malicious behaviour
patterns regardless of what the file looks like.

**HOW:**
```
Program executes on real system 
          ↓ 
Behaviour monitor watches: → File system: Is it modifying system files? → Registry: Is it adding autostart keys? → Network: Is it connecting to suspicious IPs? → Processes: Is it injecting into other processes? → Privilege: Is it attempting to escalate? 
          ↓    
If suspicious threshold exceeded → ALERT / BLOCK
```


**Characteristics:**

| Property | Detail |
|---|---|
| **Catches zero-day?** | ✅ Yes — if behaviour is malicious |
| **Catches polymorphic?** | ✅ Yes — behaviour doesn't change |
| **When does it trigger?** | AFTER execution begins — some damage possible |
| **False positive rate** | Medium — legitimate programs may behave similarly |

> [!NOTE]
> Behaviour-based detection is the basis for modern **EDR
> (Endpoint Detection and Response)** platforms — they monitor
> continuous telemetry from every process and alert on suspicious
> behavioural chains.

---

### 6.4 Integrity Checking / Checksumming

**WHAT:**
Calculates **cryptographic hashes** of critical system files at
a known-clean baseline state, then periodically recalculates
and compares — any change indicates possible infection.

**HOW:**
```
Phase 1 (clean system): Hash svchost.exe → SHA256: A1B2C3... Hash explorer.exe → SHA256: D4E5F6... Store hashes in secure baseline database 
            ↓ 
Phase 2 (after suspected infection): Rehash svchost.exe → SHA256: X7Y8Z9... ← DIFFERENT → ALERT Rehash explorer.exe → SHA256: D4E5F6... ← Same → OK
```


**Characteristics:**

| Property | Detail |
|---|---|
| **Detects any modification?** | ✅ Yes — regardless of malware type |
| **Can identify specific malware?** | ❌ No — only detects change |
| **Requires clean baseline?** | ✅ Yes — cannot work without one |
| **Catches zero-day?** | ✅ Yes — if it modifies tracked files |
| **Defeats stealth virus?** | ❌ If stealth virus intercepts hash reads |

---

### 6.5 Scanning — On-Demand vs On-Access

**On-Demand Scanning:**
- User or scheduler triggers a scan
- Scans all specified files/directories
- Finds existing infections
- Common use: scheduled nightly full scan

**On-Access (Real-Time) Scanning:**
- AV hooks into OS file system driver
- Intercepts EVERY file open/execute request
- Scans file BEFORE allowing execution
- Catches threats AT THE POINT OF EXECUTION
- Strongest protection — nothing executes without being scanned first

| | On-Demand | On-Access |
|---|---|---|
| Triggered by | User / scheduler | Any file access |
| When it runs | Periodically | Continuously |
| Finds existing infections? | ✅ Yes | ✅ Yes |
| Prevents new execution? | ❌ No | ✅ Yes |
| Resource usage | Burst (during scan) | Continuous (small overhead) |

> [!IMPORTANT]
> On-access scanning is the STRONGER protection because it prevents
> execution of malicious files. On-demand scanning finds existing
> infections but cannot prevent initial execution.

---

### 6.6 Interception / Activity Monitoring

**WHAT:**
AV hooks into **OS interrupt handlers and system calls** to monitor
all file I/O, network connections, process creation, and registry
writes — intercepting suspicious operations in real time.

**HOW:**
System call interceptor active: Any program → tries to write to system file → Interceptor fires → checks if operation is authorised → If unexpected program modifying system file → BLOCK + ALERT



**This is the basis for:**
- Real-time AV protection
- HIPS (Host-based Intrusion Prevention Systems)
- Windows Defender's real-time protection engine

---

### 6.7 Cloud-Based / Reputation-Based Detection

**WHAT:**
File's SHA-256 hash sent to a **cloud threat intelligence service**
— checked against a global database of known malware hashes and
reputation scores compiled from millions of endpoints worldwide.

**HOW:**
```
Unknown file encountered on endpoint 
      ↓ 
AV agent computes SHA-256 hash 
      ↓ 
Hash sent to cloud service 
      ↓ 
Cloud checks: "Have 0 other machines ever seen this hash?" → If 0 machines seen it → low/no reputation → SUSPICIOUS → If 10M machines seen it + no malware flag → HIGH TRUST → If 50K machines seen it + flagged malicious → BLOCK
```


**Characteristics:**

| Property | Detail |
|---|---|
| **Requires internet?** | ✅ Yes |
| **Catches zero-day?** | Partially — new file = low reputation = flagged |
| **False positive risk?** | Custom enterprise software (seen on few machines) |
| **Update speed?** | Near-real-time — database updated constantly |

---

### 6.8 Sandboxing / Dynamic Analysis

**WHAT:**
Suspicious file executed inside a **full isolated virtual machine**
— all system activity monitored — file flagged if malicious
behaviour observed.

**HOW:**
```
Suspicious file enters system (email gateway, download)
      ↓ 
File sent to sandbox (isolated VM with monitoring) 
      ↓ 
File executed inside VM: → All file system changes logged → All registry changes logged → All network connections logged → All process creations logged → All memory writes logged 
      ↓ 
Sandbox engine analyzes behaviour: If malicious patterns → QUARANTINE + ALERT If clean → deliver to user
```


**Sandbox products:**

| Tool | Type | Notes |
|---|---|---|
| **Cuckoo Sandbox** | Open-source | Most widely used open-source sandbox |
| **Any.Run** | Cloud / Interactive | Interactive analysis — user can click in the sandbox |
| **Joe Sandbox** | Commercial | Deep analysis — anti-evasion technology |
| **Hybrid Analysis** | Cloud | Free — powered by Payload Security |
| **VirusTotal** | Cloud | Multi-engine + basic dynamic analysis |

**AV response actions after detection:**

| Action | What Happens |
|---|---|
| **Quarantine** | File isolated in protected location — not deleted — reversible if false positive |
| **Disinfection** | AV attempts to remove viral code from infected file and restore original |
| **Deletion** | File permanently removed — used when disinfection impossible |
| **Alert only** | File flagged but not acted upon — analyst decision required |

---

## 📌 Extra Notes

### E1 — Mutation Engines — The Arms Race Catalyst

> [!NOTE]
> Mutation engines are standalone components that virus authors
> reuse across different viruses. Understanding them explains
> the history of polymorphism and the AV arms race.

**What is a mutation engine:**
A mutation engine (also called a polymorphic engine or mutating
engine) is a reusable code module that generates a new, functionally
equivalent but structurally different decryption stub for each
virus infection. The virus author attaches the mutation engine
to their virus — and instantly gains polymorphic evasion without
needing to implement it themselves.

**Famous mutation engines:**

| Engine | Year | Author | Significance |
|---|---|---|---|
| **MtE** (Dark Avenger's Mutation Engine) | 1991 | Dark Avenger (Bulgaria) | First widely released standalone polymorphic engine — changed everything |
| **DAME** (Dark Angel's Multiple Encryptor) | 1992 | Dark Angel | Supported multiple encryption algorithms |
| **TPE** (Trident Polymorphic Engine) | 1992 | Masud Khafir | Complex mutation — harder to detect than MtE |
| **NED** (Nuke Encryption Device) | 1992 | - | Combined with various viruses |
| **SMEG** (Simulated Metamorphic Encryption Generator) | 1994 | - | Used in Pathogen and Queeg viruses |

**The historical impact of MtE:**
Before MtE: AV vendors could reliably detect known viruses
by signature. After MtE: Any virus could be plugged into MtE
and instantly produce millions of unique signatures. AV vendors
were forced to develop heuristic and emulation-based detection —
MtE forced the entire AV industry to evolve.

---

### E2 — Famous Real-World Viruses & Worms Timeline

> [!NOTE]
> MCQs frequently reference specific historical examples.
> Know the year, type, key mechanism, and what made each notable.

**Case Study 1 — Morris Worm (1988):**
- **Author:** Robert Tappan Morris (Cornell University student)
- **Year:** November 2, 1988
- **Type:** Worm — first major internet worm
- **Propagation:** Exploited Unix sendmail debug feature,
  fingerd buffer overflow, rsh/rexec trust relationships,
  and weak password cracking
- **Impact:** Crashed approximately 6,000 machines (~10% of
  internet at the time). Estimated $100,000–$10M in damages.
- **Legal outcome:** Morris convicted under CFAA (Computer
  Fraud and Abuse Act) — first conviction under CFAA.
  Sentenced to 3 years probation, 400 hours community service,
  $10,050 fine.
- **Lesson:** A worm can spread exponentially with no ongoing
  attacker involvement. Morris claimed it was an experiment
  gone wrong — the reinfection bug caused unintended DoS.

**Case Study 2 — CIH / Chernobyl (1998):**
- **Author:** Chen Ing-hau (student, Taiwan)
- **Year:** 1998 — triggered April 26, 1999
- **Type:** Cavity file infector virus
- **Trigger:** April 26 — anniversary of Chernobyl nuclear disaster
- **Payload:**
  - Overwrote first 1MB of hard disk with null bytes
    → OS unbootable, data lost
  - Attempted to overwrite BIOS flash chip
    → Physical hardware damage on motherboards with
    flashable BIOSes (common in 1998–1999)
- **Impact:** ~$250 million damage estimate. Millions of machines.
  South Korea and many Asian countries heavily affected.
- **Lesson:** Hardware-level payload (BIOS overwrite) was
  unprecedented. Represents maximum destructive payload —
  beyond data loss to physical component damage.

**Case Study 3 — ILOVEYOU Worm (2000):**
- **Author:** Onel de Guzman (Philippines)
- **Year:** May 4–5, 2000
- **Type:** VBScript worm (often classified as virus/worm hybrid)
- **Delivery:** Email with subject "ILOVEYOU", attachment
  `LOVE-LETTER-FOR-YOU.TXT.vbs`
- **Payload:**
  - Overwrote images, music, and documents
  - Copied itself to all email contacts using Outlook
  - Downloaded password-stealing Trojan
- **Impact:** 10–50 million infections within 10 days.
  Estimated $5.5–15 billion in damage.
  Infected Pentagon, CIA, British Parliament.
- **Legal outcome:** No conviction — Philippines had no
  cybercrime law at the time. Led directly to passage of
  Philippines e-Commerce Act 2000.
- **Lesson:** Social engineering ("ILOVEYOU") was more
  effective than technical sophistication. Legal gaps
  allowed prosecution escape. Led to global cybercrime
  law harmonisation efforts.

**Complete Timeline Reference:**

| Name | Year | Type | Key Fact |
|---|---|---|---|
| Elk Cloner | 1982 | Boot sector virus | First in-the-wild virus (Apple II) |
| Brain | 1986 | Boot sector virus + stealth | First IBM PC virus — stealth technique |
| Ghostball | 1989 | Multipartite | First multipartite virus |
| Morris Worm | 1988 | Worm | First internet worm — first CFAA conviction |
| Michelangelo | 1991 | Boot sector virus | Trigger: March 6 (Michelangelo's birthday) |
| Melissa | 1999 | Macro virus | Spread via Word — first 50 Outlook contacts |
| CIH / Chernobyl | 1998 | Cavity file virus | BIOS overwrite — trigger April 26 |
| ILOVEYOU | 2000 | VBScript worm | $5.5–15B damage — no conviction |
| Code Red | 2001 | Worm | IIS buffer overflow — defaced whitehouse.gov copy |
| Nimda | 2001 | Multi-vector worm | Spread via email, web, file shares, IIS |
| Blaster (MSBlast) | 2003 | Worm | Exploited Windows RPC (MS03-026) |
| Sasser | 2004 | Worm | Exploited LSASS — no user interaction needed |
| Conficker | 2008 | Worm | MS08-067 — estimated 9–15 million infections |
| Stuxnet | 2010 | Worm | SCADA/ICS sabotage — Iran nuclear centrifuges |
| Flame | 2012 | Worm + espionage | Most complex malware at time — ~20MB |
| WannaCry | 2017 | Ransomware worm | EternalBlue (NSA exploit) — NHS, global impact |
| NotPetya | 2017 | Destructive wiper worm | EternalBlue — disguised as ransomware — $10B |

---

### E3 — EICAR Test File

> [!NOTE]
> The EICAR test file is tested in MCQs about AV compliance
> testing, AV functionality verification, and safe testing.

**What is EICAR:**
**EICAR** = **European Institute for Computer Antivirus Research**

The **EICAR Standard Anti-Virus Test File** is a harmless,
68-byte file that all compliant AV products MUST detect and
flag as a virus — even though it contains ZERO malicious code
and cannot cause any harm to any system.

**Why it exists:**
Security teams need to verify that AV is installed correctly
and actively scanning — without using real malware. EICAR
provides a safe, universal, standardised test artifact.

**Technical details:**
- Size: 68 bytes exactly
- Extension: `.com` (valid DOS executable)
- What it does if run: Prints string `EICAR-STANDARD-ANTIVIRUS-TEST-FILE!`
- What it does NOT do: Anything else — completely inert

**File content (68 bytes):**
X5O!P%@AP[4\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*



**How AV vendors handle it:**
Every major AV vendor has a hard-coded detection rule for EICAR's
exact byte sequence. When AV detects it, it reports it as
`EICAR-Test-File` or similar — indicating AV is functional.

**Use cases:**
- Verify AV scanner is active on a new system
- Test email gateway filtering — send EICAR as attachment
- Test proxy scanning — download EICAR via HTTP
- Compliance verification — confirm AV is scanning all access points

**Download:** `https://www.eicar.org/download-anti-malware-testfile/`

---

### E4 — AV Engine Internal Architecture

> [!NOTE]
> Understanding AV internals explains "why does method X fail
> against virus type Y" — a common MCQ pattern.

```
File Access / Download / Execution Request 
          ↓ 
[ Filter Driver / On-Access Hook ] Intercepts at OS kernel level 
          ↓ 
[ Unpacker / Decompressor ] Detects and unpacks known packers (UPX, MPRESS, ASPack) If packed: unpacks in memory → feeds to scanner 
          ↓ 
[ Signature Scanner ] Compares bytes against signature database Hash comparison against known malware hash DB 
          ↓ 
[ Static Heuristic Engine ] Examines code structure, PE header anomalies, suspicious patterns 
          ↓ 
[ Emulator / Virtual CPU ] Runs code in lightweight virtual CPU Observes first N instructions Unpacks encrypted content if decryptor runs 
          ↓ 
[ Machine Learning Engine ] Feature extraction → model scoring Trained on millions of malware/clean samples 
          ↓ 
[ Cloud Reputation Lookup ] Sends hash to cloud intelligence Returns reputation score + community flags   
          ↓ 
[ Behaviour Monitor ] Ongoing runtime monitoring of executing process Triggers on suspicious behavioural patterns 
          ↓ 
DECISION: Allow / Quarantine / Block / Alert
```


**AV response hierarchy:**
Quarantine → Disinfect → Delete → Alert Only (preferred) (if possible) (last resort) (MSSP environments)



---

### E5 — False Positive vs False Negative

> [!NOTE]
> These four terms (TP, FP, TN, FN) apply identically in AV,
> IDS, firewalls, and any detection system. Learn once — apply
> everywhere across all security topics.

| Term | What It Means | AV Context | Impact |
|---|---|---|---|
| **True Positive (TP)** | Malware correctly detected | AV flags actual virus | ✅ Desired |
| **True Negative (TN)** | Clean file correctly cleared | AV passes clean file | ✅ Desired |
| **False Positive (FP)** | Clean file flagged as malware | AV quarantines legitimate software | Operational disruption |
| **False Negative (FN)** | Malware not detected | AV misses real virus | Security breach |

**Which detection methods have high FP / FN rates:**

| Method | FP Rate | FN Rate | Notes |
|---|---|---|---|
| Signature-based | LOW | HIGH (for new malware) | Precise for known — blind for unknown |
| Heuristic | MEDIUM-HIGH | MEDIUM | Suspicious patterns ≠ definitely malicious |
| Behaviour-based | MEDIUM | LOW | Catches actual malicious actions — legitimate software may trigger |
| Sandbox | LOW-MEDIUM | LOW-MEDIUM | Anti-sandbox evasion increases FN |
| Reputation | LOW | MEDIUM | New software = low reputation = FP risk |

> [!IMPORTANT]
> From a DEFENDER perspective:
> - **False Negatives are worse** — malware gets through
> - **False Positives are costly** — legitimate tools blocked, productivity lost
> - The AV industry tuning challenge: maximize TP, minimize both FP and FN simultaneously

---

### E6 — Virus Construction Kits

> [!NOTE]
> Virus construction kits for self-replicating malware are
> analogous to RAT builders covered in Session 13. The concept
> is the same — lower skill barrier through automation.

**WHAT:**
Ready-made tools that allow non-technical users to CREATE
viruses without any coding knowledge — by filling in
options and clicking generate.

**Notable virus construction kits:**

| Kit | Year | Notable For |
|---|---|---|
| **VCL** (Virus Creation Laboratory) | 1992 | First major virus construction kit — MS-DOS |
| **PS-MPC** (Phalcon/Skism Mass Code Generator) | 1992 | Highly configurable — multiple payload options |
| **G2** (Phalcon/Skism) | 1992 | Generated assembly source code |
| **IVP** (Instant Virus Production) | 1992 | Very simple — fill-in-the-blank GUI |
| **NGVCK** (Next Generation Virus Construction Kit) | 2001 | Win32 viruses — more modern target |

**Options typically configurable in a virus kit:**
- Target file type (.exe, .com, .dll)
- Infection method (prepend, append, cavity)
- Payload (display message, delete files, format drive)
- Trigger condition (date, counter, random)
- Stealth capability (on/off)
- Encryption (on/off, algorithm)

**Legal status:**
Possession and use of virus construction kit output to attack
any system without authorisation is a criminal offence in
virtually every jurisdiction. In India: IT Act 2000 Section 66.

---

### E7 — Predecessor / Successor Chains

> [!NOTE]
> Predecessor/successor chains show how threats evolved —
> and how defences forced attackers to innovate.

**Virus Evasion Evolution:**
```
Simple file infectors (1980s) — no evasion 
        ↓ 
Encrypted payloads (1987 — Cascade was early encryptor)     
        ↓ 
Stealth viruses (1986 — Brain used disk read interception) 
        ↓ 
Polymorphic viruses via MtE (1991 — Dark Avenger) 
        ↓ 
Metamorphic viruses (1998 — Zmist, full code rewriting)     
        ↓ 
Rootkit integration (2000s — hiding from OS entirely) 
        ↓ 
Packers + crypters (2000s — UPX, then custom) 
        ↓ 
Fileless / in-memory execution (2012+) 
        ↓ 
LotL / LOLBins (2014+ — no malware file at all) 
        ↓ 
AI-generated polymorphic variants (2023+)
```


**AV Detection Evolution (response to above):**
```
Simple signature scanning (1987 — first AV tools) 
      ↓ 
Integrity checking / checksums (1988) 
      ↓ 
Heuristic analysis (1991 — response to MtE) 
      ↓  
Behavioural monitoring (1995+) 
      ↓ 
Virtual CPU emulation (1997+) 
      ↓ 
Sandboxing / full VM analysis (2005+) 
      ↓ 
Cloud reputation + community intelligence (2008+) 
      ↓ 
ML-based classification (2012+) 
      ↓ 
EDR with continuous telemetry (2013+) 
      ↓ 
AI/ML adversarial detection (2023+)
```


**Worm history chain:**
```
Morris Worm (1988) — single vulnerability exploitation 
        ↓ 
Melissa / ILOVEYOU (1999–2000) — email as propagation vector 
        ↓ 
Code Red / Nimda (2001) — multi-vector, web exploitation 
        ↓ 
Blaster / Sasser (2003–2004) — OS vulnerabilities, no user action 
        ↓ 
Conficker (2008) — DGA for C2 resilience 
        ↓ 
Stuxnet (2010) — nation-state, SCADA targeting, 4 zero-days 
        ↓ 
WannaCry / NotPetya (2017) — NSA exploit + ransomware payload 
        ↓ 
IoT worms / Mirai successors (2020+) — billions of devices
```


---

### E8 — Terminology Traps

| Term | Trap | Clarification |
|---|---|---|
| **Virus vs Worm** | "Worm needs a host file" | FALSE — the VIRUS needs a host file. The worm is standalone. This is reversed in almost every MCQ distractor. |
| **Polymorphic vs Metamorphic** | "Both change their code" | PARTIAL. Polymorphic changes the DECRYPTOR STUB (the payload code itself stays same, just encrypted differently). Metamorphic changes THE ACTUAL CODE. |
| **Stealth vs Sparse Infector** | "Stealth virus avoids detection by infecting fewer files" | FALSE. Stealth avoids detection by INTERCEPTING OS CALLS. SPARSE INFECTOR avoids detection by infecting FEWER FILES. |
| **Cavity vs Overwriting** | "Both modify file content" | OVERWRITING destroys original content. CAVITY fills empty space — PRESERVES original content. |
| **On-demand vs On-access scanning** | "On-access scanning is triggered by user" | FALSE — on-ACCESS fires on any file ACCESS automatically. On-DEMAND is triggered by user or scheduler. |
| **Heuristic detection high FP** | "Heuristic has fewer false positives than signature" | FALSE — heuristic has HIGHER FP rate because it flags suspicious-looking legitimate code. Signature-based is most precise for known malware. |
| **EICAR is real malware** | "Use EICAR only in isolated environments" | FALSE — EICAR is HARMLESS. It can be used anywhere. It is not a virus. It contains zero malicious code. |
| **Sandboxing vs Emulation** | "Sandbox and emulator are the same" | Different scale. Emulation uses a lightweight virtual CPU inside the AV engine. Sandboxing uses a full isolated VM. |
| **MBR vs VBR** | "Boot sector virus only infects MBR" | Boot sector viruses infect either MBR (Master Boot Record — first sector of entire disk) OR VBR (Volume Boot Record — first sector of a partition). |
| **Multipartite "multiple types"** | "Multipartite means it infects multiple file types" | FALSE — multipartite means it infects BOTH BOOT SECTOR AND EXECUTABLE FILES simultaneously. The "multi" refers to infection LOCATION not file TYPE. |

---

### E9 — Current Landscape 2026

> [!NOTE]
> Current developments relevant to viruses, worms, and AV evasion.

**AI-Generated Polymorphic Malware (2023–2025):**
- Tools like WormGPT and dark web LLM services generate unique malware
  variants on demand. Each generated sample has different obfuscation,
  encoding, instruction sequences, and variable names. Functionally
  identical — structurally unique — defeating signature AV at scale
  with zero manual effort from the attacker.
- Polymorphism that previously required expert mutation engine
  development now requires a single API call to a dark web LLM.

**Living-off-the-Land Worms (2023–2025):**
- Modern worm variants increasingly use LOLBins (PowerShell, WMI,
  certutil) for propagation rather than dropped executables.
  No malware binary is written to disk — traditional AV has no file
  to scan. Propagation looks like legitimate admin activity.

**EternalBlue Still Active (2024–2026):**
- CVE-2017-0144 (EternalBlue — SMB RCE) remains weaponised in
  active attacks. WannaCry and NotPetya used it in 2017. As of
  2025, unpatched Windows 7, Windows Server 2008 machines on
  internal networks remain vulnerable. Many industrial/OT
  environments run unpatched legacy Windows.

**Recent CVEs — Virus/Worm Relevant:**
- **CVE-2024-38112 (Windows MSHTML — 2024):** Zero-day used to
  deliver malware via specially crafted URL files — triggered
  Internet Explorer rendering engine invisibly.
  CVSS 7.5. Exploited before July 2024 patch.
- **CVE-2023-23397 (Outlook zero-click — 2023):** Worm-like
  propagation potential — calendar invite triggers NTLM hash
  theft without user opening email. Used by APT28.
  No user interaction required — worm characteristic.
- **CVE-2022-30190 (Follina MSDT — 2022):** Executed malware
  via Word document without macros — Office URI scheme abuse.
  Used in multiple APT campaigns for Trojan delivery.

**IoT Worm Landscape:**
- Mirai successors continue to evolve targeting IP cameras,
  routers, NAS devices, smart TVs. Devices run embedded Linux
  with no AV capability. Default credentials or unpatched
  CVEs used for propagation. Infected devices recruited into
  botnets for DDoS (Tbps-scale attacks now possible).

---

### E10 — Indian Legal Context

> [!NOTE]
> Indian law specifically applicable to virus/worm creation,
> distribution, and damage.

| Law | Section | Offence | Penalty |
|---|---|---|---|
| **IT Act 2000** | **S.43(c)** | Introducing virus/malware to any computer or network | Civil compensation up to ₹1 crore |
| **IT Act 2000** | **S.66** | Creating/deploying virus or worm causing unauthorised damage | Up to 3 years imprisonment + ₹5 lakh fine |
| **IT Act 2000** | **S.66F** | Deploying virus/worm against critical infrastructure (power, banking, defence) with intent to threaten sovereignty/security | **Life imprisonment** |
| **IT Act 2000** | **S.43(b)** | Downloading/copying data via virus/worm | Civil compensation up to ₹1 crore |
| **IPC** | **S.426** | Mischief — damage caused by destructive virus (wiper, data-destroying virus) | Up to 3 months + fine |
| **IPC** | **S.268** | Public nuisance — worm causing widespread network disruption | Fine |
| **DPDPA 2023** | — | Personal data exfiltrated by worm/virus from an organisation | Penalty up to ₹250 crore |
| **DPDPA 2023** | — | Failure to notify affected parties of breach caused by malware | Penalty up to ₹200 crore |

> [!IMPORTANT]
> **Section 66F** is the highest penalty provision in Indian cyber law —
> **life imprisonment** — and applies specifically when a virus or worm
> targets critical national infrastructure. This is always an MCQ trap
> option when questions ask about maximum penalties.

---

## Abbreviations Table

| Abbreviation | Full Form | One-Line Technical Meaning |
|---|---|---|
| **AV** | Antivirus | Software detecting/preventing/removing malware |
| **BIOS** | Basic Input/Output System | Firmware initializing hardware before OS boots |
| **COM** | Command/Component Object | Executable format in DOS — executes before .exe |
| **CPUID** | CPU Identification Instruction | x86 instruction — returns CPU features including hypervisor bit |
| **DGA** | Domain Generation Algorithm | Algorithm generating rotating C2 domains for worm resilience |
| **EDR** | Endpoint Detection and Response | Continuous endpoint threat monitoring + automated response |
| **EICAR** | European Institute for Computer Antivirus Research | Organisation — created harmless 68-byte AV test file |
| **FAT** | File Allocation Table | Legacy filesystem structure — cluster virus manipulation target |
| **FIM** | File Integrity Monitoring | Continuous monitoring of file changes against baseline |
| **FN** | False Negative | Malware incorrectly cleared as safe — missed detection |
| **FP** | False Positive | Clean file incorrectly flagged as malware |
| **HIPS** | Host-based Intrusion Prevention System | Host-level system monitoring + blocking suspicious activity |
| **ICS** | Industrial Control System | Industrial automation systems — Stuxnet target category |
| **IOC** | Indicator of Compromise | Artefact confirming compromise (hash, IP, registry key, domain) |
| **LotL** | Living off the Land | Using legitimate OS tools for malicious purposes |
| **MBR** | Master Boot Record | First sector of storage device — boot sector virus target |
| **ML** | Machine Learning | AI technique — used in modern AV classification engines |
| **MtE** | Mutation Engine (Dark Avenger's) | First widely released standalone polymorphic engine (1991) |
| **NOP** | No Operation | Assembly instruction that does nothing — used in dead code insertion |
| **OUI** | Organizationally Unique Identifier | First 3 bytes of MAC address — identifies NIC manufacturer |
| **PE** | Portable Executable | Windows executable file format (.exe, .dll, .sys) |
| **RDTSC** | Read Time-Stamp Counter | x86 instruction reading CPU clock cycles — used for VM timing detection |
| **RLO** | Right-to-Left Override | Unicode U+202E character — reverses text display direction |
| **SCADA** | Supervisory Control and Data Acquisition | Industrial process monitoring system — Stuxnet target |
| **SHA** | Secure Hash Algorithm | Cryptographic hash family — SHA-256 current standard |
| **TN** | True Negative | Clean file correctly identified as safe |
| **TP** | True Positive | Malware correctly identified as malicious |
| **UPX** | Ultimate Packer for eXecutables | Legitimate open-source packer — widely abused by malware |
| **VBA** | Visual Basic for Applications | Microsoft macro language — primary macro virus language |
| **VBR** | Volume Boot Record | Boot record for a specific partition — also boot sector virus target |
| **VT** | VirusTotal | Online multi-engine malware scanning service (70+ AV engines) |
| **WMI** | Windows Management Instrumentation | Windows admin framework — abused for fileless worm persistence |

---

## 🔑 Keywords + Concept Map

**Core Keywords:**
Virus · Worm · Trojan · Host File · Self-Replicating · Boot Sector ·
MBR · VBR · File Infector · Macro Virus · VBA · Normal.dot ·
Network Virus · Stealth Virus · Polymorphic · Metamorphic ·
Mutation Engine · MtE · Multipartite · Cluster Virus · FAT ·
Sparse Infector · Overwriting · Cavity · CIH · Tunneling ·
Armored · Worm Propagation · Hit-list Scanning · Topological ·
Random Scanning · Signature Detection · Heuristic · Behaviour ·
Integrity Checking · On-demand · On-access · Sandboxing · EICAR ·
Quarantine · Disinfection · False Positive · False Negative ·
UPX · Packing · Obfuscation · Anti-VM · RDTSC · Process Injection ·
T1027 · T1497 · T1055 · T1210

**Concept Map:**
```
VIRUSES, WORMS & AV EVASION
│
├── MALWARE TAXONOMY
│   ├── Virus ────────── Needs host file + human execution → then spreads
│   ├── Worm ─────────── No host + no human action → spreads automatically
│   └── Trojan ───────── Disguised → no self-replication → backdoor
│
├── VIRUS LIFECYCLE
│   ├── Dormant ──────── Present, inactive, waiting for trigger
│   ├── Propagation ──── Replicating into other files/sectors
│   ├── Triggering ───── Activation condition met
│   └── Execution ────── Payload runs (damage occurs here)
│
├── VIRUS TYPES
│   ├── By target ──────────── Boot sector (MBR/VBR) | File infector | Macro
│   ├── By evasion ─────────── Stealth | Polymorphic | Metamorphic | Tunneling | Armored
│   ├── By infection style ─── Overwriting (destroys) | Cavity (preserves, no size change)
│   ├── By spread method ───── Network virus | Sparse infector
│   └── By vector combo ────── Multipartite (boot + files) | Cluster (directory entries)
│
├── WORMS
│   ├── Characteristics ────── No host file, self-replicating, exploits vulnerabilities
│   ├── Components ─────────── Recon + Exploit + Propagate + Payload + Persist + C2
│   └── Propagation models ─── Random | Sequential | Topological | Hit-list | Permutation
│
├── AV EVASION
│   ├── Code-level ─────────── Obfuscation | Encoding | Polymorphism | Metamorphism
│   ├── Binary-level ───────── Packing (UPX) | Crypters (runtime)
│   ├── Runtime-level ──────── Process injection | Rootkit | Fileless
│   └── Analysis-evasion ───── Anti-VM | Anti-debug | Timing delays | Canary checks
│
└── DETECTION METHODS
    ├── Signature ──────────── Fast, low FP, blind to unknown/polymorphic
    ├── Heuristic ──────────── Static (code patterns) | Dynamic (emulation)
    ├── Behaviour ──────────── Runtime monitoring — catches zero-day post-execution
    ├── Integrity check ────── Baseline hash comparison — detects ANY modification
    ├── On-demand ──────────── User/scheduler triggered — finds existing infections
    ├── On-access ──────────── Real-time intercept — prevents execution
    ├── Sandboxing ─────────── Full VM execution + behaviour observation
    └── Cloud/Reputation ───── Hash + reputation score from global intelligence
```


---

## ⚡ Quick Reference Cheatsheet

### 🦠 Virus Types — One-Line Exam Reference

| Virus Type | One-Line ID | Key MCQ Fact |
|---|---|---|
| Boot Sector | Infects MBR/VBR — runs before OS | Survives OS reinstall; remove with `bootrec /fixmbr` |
| File Infector | Attaches to .exe/.com — runs on execution | Most common type overall |
| Macro | Infects Office docs via VBA | Melissa = first 50 Outlook contacts |
| Network | Spreads via network shares — still needs host | Still needs host file + user execution |
| Stealth | Hides by intercepting OS calls | Must be memory-resident to intercept |
| Polymorphic | Encrypts payload + mutates decryptor per infection | Defeats signature AV — same behaviour |
| Metamorphic | Rewrites entire code per infection | No encryption, no stub — hardest to detect |
| Multipartite | Infects BOTH boot sector AND executable files | Must clean both vectors simultaneously |
| Cluster | Modifies directory/FAT entries — not file content | One copy affects all directory entries |
| Sparse Infector | Infects selectively (every nth file) | Reduces detection probability |
| Overwriting | Overwrites original — destroys host file | Infected files stop working — easy to detect |
| Cavity/Space-filler | Fills empty file sections — no size increase | CIH example — BIOS overwrite payload |
| Tunneling | Goes direct to BIOS/DOS interrupts — bypasses AV hooks | Defeats interrupt-hook-based AV |
| Armored | Anti-disassembly + anti-debug to resist analysis | Slows researcher analysis — delays signatures |

---

### 🔬 Virus Type Cross-Reference Table

| Type | Modifies File Content? | Increases File Size? | Hides Presence? | Classic Example |
|---|---|---|---|---|
| Boot Sector | ❌ (MBR, not files) | N/A | Partial | Brain, Michelangelo |
| File Infector (append) | ✅ Yes | ✅ Yes | ❌ | Jerusalem |
| Macro | ✅ Yes (adds macro) | ✅ Yes | ❌ | Melissa |
| Stealth | ✅ Yes (but intercepts reads) | ✅ (hidden) | ✅ Yes | Brain, 4096 |
| Polymorphic | ✅ Yes | ✅ Yes | Partial | Cascade, Tequila |
| Metamorphic | ✅ Yes | ✅ Yes | Partial | Zmist, Simile |
| Multipartite | ✅ Yes + MBR | ✅ Yes | ❌ | Ghostball |
| Cluster | ❌ (modifies FAT) | ❌ | ❌ | — |
| Sparse Infector | ✅ Yes | ✅ Yes | Partial | — |
| Overwriting | ✅ Yes (destroys) | ❌ | ❌ | Trivial.88.D |
| Cavity | ✅ Yes (fills gaps) | ❌ | ❌ | CIH/Chernobyl |
| Tunneling | ✅ Yes | ✅ Yes | Partial | — |
| Armored | ✅ Yes | ✅ Yes | ❌ (resists analysis) | Whale |

---

### 🆚 Polymorphic vs Metamorphic — Full Comparison

| Property | Polymorphic | Metamorphic |
|---|---|---|
| Encryption used? | ✅ Yes | ❌ No |
| What changes per infection? | Decryption stub + encryption key | Entire code body |
| Payload behaviour changes? | ❌ No | ❌ No (same outcome) |
| Decryption stub present? | ✅ Yes (but mutated) | ❌ No stub at all |
| Requires mutation engine? | ✅ Yes | ✅ Yes (more complex) |
| Detection difficulty | High | Very high |
| Classic example | Cascade, Tequila, Storm | Zmist, Simile |

---

### 🛡️ Detection Method vs What It Catches

| Detection Method | ✅ Catches | ❌ Misses |
|---|---|---|
| Signature-Based | Known malware exactly | Zero-day, polymorphic, metamorphic, packed |
| Heuristic (Static) | Modified known malware, suspicious patterns | Advanced obfuscation, novel patterns |
| Heuristic (Dynamic/Emulation) | Packed malware, some polymorphic | Anti-emulation, long sleep, anti-VM |
| Behavior-Based | Zero-day, polymorphic, post-exec | Damage possible before trigger |
| Integrity Checking | Any file modification — regardless of type | Cannot identify specific malware |
| Sandboxing | Unknown/packed/new malware | Anti-VM, delayed execution, user interaction check |
| Cloud/Reputation | New malware seen globally | Targeted zero-day (never seen before) |

---

### ⚔️ AV Evasion — What Each Technique Defeats

| Evasion Technique | What It Defeats | How |
|---|---|---|
| Encryption | Signature scanning | Payload hidden in encrypted blob |
| Polymorphism | Signature scanning | No stable signature across infections |
| Metamorphism | Signature + some heuristic | No consistent code structure |
| Obfuscation | Static heuristic, analysis | Increases analysis difficulty |
| Packing (UPX etc.) | Signature scanning | Different binary on disk |
| Custom packers | Signature + generic unpackers | No known unpacking routine |
| Rootkit | OS-level AV queries | Hides from OS — AV sees nothing |
| Timing delays | Sandbox (time limit) | Outlasts sandbox execution window |
| Anti-VM | Sandboxing | Detects VM — behaves cleanly |
| File extension spoofing | User (not AV) | User fooled — executes malware willingly |
| Process injection | Process-level monitoring | Malicious code runs inside trusted process |

---

### 🌐 Worm Propagation Models

| Model | Speed | Noise | Best For | Example |
|---|---|---|---|---|
| Random Scanning | Slow initially | High | Large-scale, any target | Morris Worm |
| Sequential Scanning | Medium | Medium | Geographic concentration | — |
| Topological | Targeted | Low | High-value targeted spread | Stuxnet |
| Hit-list Scanning | **Fastest** | Low initially | Maximum initial explosive growth | Code Red II |
| Permutation Scanning | Fast + efficient | Low | Coordinated multi-instance | Witty Worm |

---

### 📅 Famous Malware Quick Reference

| Name | Year | Type | Key Fact |
|---|---|---|---|
| Elk Cloner | 1982 | Boot virus | First in-the-wild virus (Apple II) |
| Brain | 1986 | Boot virus + stealth | First IBM PC virus — stealth |
| Morris Worm | 1988 | Worm | First internet worm — first CFAA conviction |
| Ghostball | 1989 | Multipartite | First multipartite virus |
| Michelangelo | 1991 | Boot sector virus | Trigger: March 6 |
| Melissa | 1999 | Macro virus | Word + first 50 Outlook contacts |
| CIH / Chernobyl | 1998 | Cavity file virus | BIOS overwrite — April 26 trigger |
| ILOVEYOU | 2000 | VBScript worm | $5.5–15B damage — no conviction (Philippines) |
| Code Red | 2001 | Worm | IIS buffer overflow |
| Blaster | 2003 | Worm | Windows RPC MS03-026 |
| Conficker | 2008 | Worm | MS08-067 — DGA C2 |
| Stuxnet | 2010 | Worm | SCADA/ICS — 4 zero-days — Iran |
| WannaCry | 2017 | Ransomware worm | EternalBlue — NHS — global |
| NotPetya | 2017 | Wiper worm | EternalBlue — disguised as ransomware — $10B |

---

### ⚖️ Indian Legal Reference

| Law | Section | Offence | Penalty |
|---|---|---|---|
| IT Act 2000 | S.43(c) | Introducing virus/malware | Civil ₹1 crore |
| IT Act 2000 | S.66 | Creating/deploying virus/worm | 3 yrs + ₹5L |
| IT Act 2000 | **S.66F** | Malware on critical infrastructure | **Life imprisonment** |
| IPC | S.426 | Damage via destructive virus | 3 months + fine |
| DPDPA 2023 | — | Data breach via malware | ₹250 crore |
| DPDPA 2023 | — | Failure to notify breach | ₹200 crore |

---

## ✅ Session Revision Snapshot

### ⚡ TL;DR — 5 Bullets

1. **Virus needs host file + human execution; Worm is standalone +
   self-replicating with no human action needed** — this single
   distinction drives half of all MCQs on this topic. Every distractor
   reverses it. Know it cold.

2. **Polymorphic = encrypts payload + mutates decryptor stub per
   infection; Metamorphic = rewrites ENTIRE CODE per infection — no
   encryption, no stub** — polymorphic has a detectable stub even if
   mutating; metamorphic has NO consistent structure whatsoever.
   Metamorphic is significantly harder to detect.

3. **14 virus types — each has a specific mechanism MCQs test:**
   cavity fills empty sections without size increase (CIH), stealth
   intercepts OS calls, cluster modifies FAT not files, multipartite
   infects BOTH boot sector AND files, sparse infector is selective.
   Know the defining property of each.

4. **Signature-based detection fails against zero-day, polymorphic,
   and metamorphic viruses — but has the LOWEST false positive rate.
   Heuristic has HIGHER false positive rate but catches more unknowns.
   Behaviour-based catches zero-day but triggers only after execution.**
   These trade-offs are always tested together.

5. **Worm propagation models: Hit-list scanning = fastest explosive
   initial spread (pre-compiled vulnerable target list). Topological
   scanning = most targeted and lowest noise (uses data found on
   infected host). Random scanning = slowest but most common historically.**

---

### 🎯 MCQ-Likely Concepts

- [ ] Virus vs Worm — which needs host, which self-replicates
- [ ] Virus lifecycle — four phases, what happens in each
- [ ] Polymorphic vs Metamorphic — stub vs full rewrite
- [ ] Boot sector virus — MBR vs VBR, runs before OS, survives reinstall
- [ ] Macro virus — VBA language, Normal.dot infection, Melissa
- [ ] Stealth virus — OS call interception, must be memory-resident
- [ ] CIH Chernobyl — cavity virus, BIOS overwrite, April 26
- [ ] Cavity vs Overwriting — file size change, content preservation
- [ ] Multipartite — BOTH boot sector AND files
- [ ] Cluster virus — FAT/directory modification, not file content
- [ ] Sparse infector — selective infection to reduce detection
- [ ] Signature-based — what it catches, what it misses (FN for new malware)
- [ ] Heuristic — static vs dynamic emulation, higher FP rate
- [ ] Behaviour-based — zero-day detection, post-execution trigger
- [ ] On-demand vs On-access scanning — which prevents execution
- [ ] Sandboxing — full VM, tools (Cuckoo, Any.Run), anti-VM evasion
- [ ] EICAR — 68-byte harmless file, compliance test, all AV must detect
- [ ] MtE — Dark Avenger, 1991, first standalone polymorphic engine
- [ ] Morris Worm — 1988, first internet worm, first CFAA conviction
- [ ] Stuxnet — SCADA/ICS, worm, 4 zero-days, Iran nuclear
- [ ] WannaCry — ransomware worm, EternalBlue, 2017
- [ ] Hit-list scanning — fastest initial worm spread
- [ ] False Positive vs False Negative — definitions, which method has higher FP
- [ ] AV response: Quarantine vs Disinfection vs Deletion
- [ ] RDTSC — VM timing detection in anti-VM technique
- [ ] Process injection — types, hides in legitimate process
- [ ] IT Act S.66F — life imprisonment for malware on critical infrastructure
- [ ] Worm components — recon + exploit + propagate + payload + persist

---

### 💼 Interview-Likely

- What is the precise technical difference between a virus and a worm?
- Explain polymorphic vs metamorphic malware with a technical example.
- Why does signature-based AV fail against polymorphic viruses?
- What is the CIH virus notable for beyond being a cavity infector?
- What was the historical significance of the MtE (Dark Avenger's
  Mutation Engine)?
- What is the EICAR test file and why does it exist?
- Explain hit-list scanning — why does it produce the fastest initial
  worm spread?
- What is the difference between on-demand and on-access AV scanning?
- Why is behaviour-based detection considered a better approach for
  zero-day threats despite triggering after execution?
- What happened with the ILOVEYOU case legally and what was the impact?

---

## Next Session Bridge

Session 14 completes the self-replicating malware sub-phase — covering
how viruses spread, self-replicate, evade detection, and how AV detects
them. The progression so far has been: disguise without replication
(Trojan) → self-replication with host (Virus) → self-replication
without host (Worm).

Session 15 moves the attack surface from the endpoint to the network
layer — introducing **Sniffing, ARP Poisoning, MAC Flooding, and DNS
Spoofing**. Where viruses and worms attack the system directly, sniffing
attacks the communication channel — intercepting and manipulating
traffic that the target believes is private. The attacker becomes a
silent, invisible observer of all network traffic — then an active
manipulator of it.

---

<details>
<summary>📖 Glossary</summary>

| Term | Definition |
|---|---|
| **Antivirus (AV)** | Software that detects, prevents, and removes malware using signatures, heuristics, or behaviour |
| **Armored Virus** | Virus using anti-disassembly and anti-debugging techniques to resist researcher analysis |
| **AutoOpen** | VBA event handler in Microsoft Word that auto-executes macro on document open |
| **Behaviour-based Detection** | AV method monitoring live runtime actions of executing programs for malicious patterns |
| **Boot Sector Virus** | Virus infecting MBR or VBR — executes before OS loads |
| **Cavity Virus** | Virus inserting itself into empty sections of PE files without increasing file size |
| **CIH / Chernobyl** | Cavity file virus (1998) — triggered April 26 — overwrote BIOS flash chip |
| **Cluster Virus** | Virus modifying directory/FAT entries to redirect execution — does not modify file contents |
| **Code Red** | Worm (2001) exploiting IIS buffer overflow — propagated via HTTP |
| **Companion Virus** | File infector creating same-named .com file alongside target .exe — .com executes first in DOS |
| **Conficker** | Worm (2008) exploiting MS08-067 — used DGA for C2 resilience |
| **CPUID** | x86 instruction returning CPU identification and feature flags including hypervisor presence bit |
| **DAME** | Dark Angel's Multiple Encryptor — early polymorphic engine (1992) |
| **Dead Code Insertion** | Obfuscation technique adding meaningless NOP-equivalent instructions to change binary signature |
| **EICAR** | European Institute for Computer Antivirus Research — produced harmless 68-byte AV test file |
| **Elk Cloner** | First in-the-wild virus (1982) — infected Apple II computers via boot sector |
| **False Negative (FN)** | Malware not detected by AV — security breach risk |
| **False Positive (FP)** | Clean file flagged as malware by AV — operational disruption |
| **File Infector Virus** | Virus attaching to executable files — activates when infected file executed |
| **Ghostball** | First multipartite virus (1989) |
| **Heuristic Detection** | AV analysis of suspicious code patterns without requiring known signatures |
| **Hit-list Scanning** | Worm propagation using pre-compiled list of known vulnerable targets — fastest initial spread |
| **Hybrid Malware** | Malware combining properties of multiple categories (e.g., worm + ransomware) |
| **Integrity Checking** | AV/FIM method comparing current file hashes to known-clean baseline hashes |
| **ILOVEYOU** | VBScript worm (2000) — $5.5–15B damage — spread via email — no conviction |
| **Jerusalem** | File infector virus — also called Friday the 13th virus |
| **Macro Virus** | Virus embedded in Office document macros (VBA) — spreads when documents shared |
| **Master Boot Record (MBR)** | First physical sector of storage device — boot code + partition table — boot virus target |
| **Melissa** | Macro virus (1999) — spread via Word documents to first 50 Outlook contacts |
| **Metamorphic Virus** | Virus rewriting its entire code body per infection — no encryption, no stub |
| **Michelangelo** | Boot sector virus — trigger date March 6 (Michelangelo's birthday) |
| **Morris Worm** | First internet worm (1988) — first CFAA conviction — crashed ~6000 machines |
| **MtE** | Dark Avenger's Mutation Engine (1991) — first standalone polymorphic engine |
| **Multipartite Virus** | Virus infecting BOTH boot sector AND executable files simultaneously |
| **Mutation Engine** | Reusable code module generating new decryption stubs for each virus infection |
| **Network Virus** | Virus spreading via network shares — still requires host file and user execution |
| **Normal.dot** | Microsoft Word global template — macro virus infection point — all new documents affected |
| **NotPetya** | Destructive wiper worm (2017) — disguised as ransomware — $10B damage |
| **On-Access Scanning** | AV scanning every file at the moment of access/execution — real-time protection |
| **On-Demand Scanning** | AV scanning triggered by user or scheduler — finds existing infections |
| **OUI** | Organizationally Unique Identifier — first 3 bytes of MAC address — identifies manufacturer |
| **Overwriting Virus** | Virus replacing original file content — permanently destroys original |
| **Permutation Scanning** | Worm propagation model using shared pseudo-random IP permutation across instances |
| **Polymorphic Virus** | Virus encrypting payload + mutating decryption stub per infection |
| **Process Injection** | Technique injecting malicious code into memory of legitimate running processes |
| **Quarantine** | AV action isolating suspected malware — not deleted — reversible if false positive |
| **RDTSC** | Read Time-Stamp Counter — x86 instruction used by malware to detect VM timing differences |
| **Reputation-Based Detection** | AV method using global file hash database + reputation scores for malware identification |
| **RLO** | Unicode U+202E Right-to-Left Override — used to reverse displayed filename for spoofing |
| **Sandboxing** | AV method executing suspicious file in isolated VM and observing behaviour |
| **Sasser** | Worm (2004) exploiting LSASS vulnerability — spread with no user interaction |
| **Signature-Based Detection** | AV method matching file bytes against database of known malware signatures |
| **Simile** | Metamorphic virus — one of the most studied examples of full code rewriting |
| **Sparse Infector** | Virus infecting selectively to reduce detection probability |
| **Static Heuristics** | Heuristic analysis of code structure without executing it |
| **Stealth Virus** | Virus intercepting OS calls to return clean file versions to AV — hides in memory |
| **Stuxnet** | Worm (2010) targeting Iranian nuclear SCADA — used 4 zero-day exploits |
| **TPE** | Trident Polymorphic Engine — early DOS-era polymorphic engine (1992) |
| **Tunneling Virus** | Virus bypassing AV hooks by going directly to BIOS/DOS interrupt handlers |
| **VBA** | Visual Basic for Applications — macro language in Office — primary macro virus language |
| **VBR** | Volume Boot Record — boot record for a specific partition |
| **Volume Boot Record (VBR)** | First sector of a disk partition — secondary boot sector virus infection target |
| **WannaCry** | Ransomware worm (2017) — spread via EternalBlue SMB exploit — global impact |
| **Whale Virus** | Armored virus (1990) — famous for extreme complexity defeating early analysis tools |
| **Zmist** | One of the most sophisticated metamorphic viruses — full code integration rewriting |

</details>

---
