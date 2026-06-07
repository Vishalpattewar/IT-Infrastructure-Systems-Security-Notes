# MCQ Set — Session 14: Viruses, Worms & Antivirus Evasion 🦠

> 28 MCQs · 4 options each · Full explanations · Covers core + extra notes

---

## 📑 Table of Contents

- [Questions 01–10 — Virus Types & Lifecycle](#questions-0110--virus-types--lifecycle)
- [Questions 11–18 — AV Evasion Techniques](#questions-1118--av-evasion-techniques)
- [Questions 19–24 — Detection Methods](#questions-1924--detection-methods)
- [Questions 25–28 — Extra Notes & Real-World](#questions-2528--extra-notes--real-world)
- [Answer Key](#answer-key)

---

## Questions 01–10 — Virus Types & Lifecycle

---

### Q01

**Which of the following is the MOST precise technical distinction between a virus and a worm?**

- A) A virus damages files; a worm does not
- B) A worm requires a host file to spread; a virus does not
- C) ✅ A virus requires a host file and human execution; a worm is self-replicating and needs neither
- D) A virus spreads over networks; a worm spreads via physical media

**Explanation:**

- **A** is incorrect — both viruses and worms can carry destructive payloads. Damage is not the defining distinction.
- **B** is the exact reverse of the correct answer — this is the most common MCQ trap on this topic. The **virus** needs a host file; the **worm** does not.
- **C** ✅ is correct — a virus attaches to a host file and requires the user to execute that infected file to activate and spread. A worm is a standalone, self-replicating program that spreads automatically by exploiting network vulnerabilities — no host file, no user action required.
- **D** is incorrect — viruses can also spread over networks (network viruses). The transport medium is not the defining distinction.

---

### Q02

**A virus is present on a system but is not yet causing any damage. It is waiting for April 26th to activate. Which phase of the virus lifecycle is this?**

- A) Propagation Phase
- B) Execution Phase
- C) Triggering Phase
- D) ✅ Dormant Phase

**Explanation:**

- **A** is incorrect — the propagation phase is when the virus actively copies itself into other files or sectors.
- **B** is incorrect — the execution phase is when the payload actually runs and causes damage.
- **C** is incorrect — the triggering phase is the moment the activation condition is *met*, not the waiting period before it is met.
- **D** ✅ is correct — the dormant phase is when the virus is present but completely inactive, waiting for a trigger condition (specific date, event, counter value) to be met. The CIH/Chernobyl virus is the classic example — it waited in dormancy until April 26th before executing its payload.

---

### Q03

**Which type of virus infects the Master Boot Record and is capable of loading into memory BEFORE the operating system boots — making it active before any antivirus software can initialize?**

- A) File Infector Virus
- B) Multipartite Virus
- C) Stealth Virus
- D) ✅ Boot Sector Virus

**Explanation:**

- **A** is incorrect — a file infector attaches to executable files (.exe, .com) and activates when those files are run. It has no involvement with the MBR or pre-OS execution.
- **B** is incorrect — a multipartite virus infects *both* the boot sector *and* executable files. The question specifically focuses on MBR infection and pre-OS loading, which is the defining characteristic of a boot sector virus specifically.
- **C** is incorrect — a stealth virus hides its presence using OS call interception. It is not defined by where it resides at boot time.
- **D** ✅ is correct — boot sector viruses reside in the MBR or VBR. BIOS reads the MBR before loading the OS, which means the boot sector virus executes before the OS initializes — and before any AV software loads. This is why they are particularly dangerous and why they survive OS reinstallation if the MBR is not explicitly wiped.

---

### Q04

**The Melissa virus is the classic textbook example of which virus type?**

- A) Boot Sector Virus
- B) ✅ Macro Virus
- C) Polymorphic Virus
- D) Network Virus

**Explanation:**

- **A** is incorrect — boot sector viruses infect the MBR. Melissa spread through Microsoft Word documents, not boot sectors.
- **B** ✅ is correct — Melissa (1999) is a VBA macro virus that spread by emailing infected Word documents to the first 50 contacts in the victim's Microsoft Outlook address book. It infected Microsoft Word's Normal.dot global template, causing all new documents to be infected. Author David L. Smith was sentenced to 20 months federal prison.
- **C** is incorrect — Melissa did not use a mutation engine, encryption, or code rewriting to evade detection. Polymorphism was not its characteristic.
- **D** is incorrect — a network virus spreads via network shares but still requires a host file and user execution. Melissa's defining property is that it was embedded in an Office document as a VBA macro.

---

### Q05

**A virus intercepts operating system file-read requests and returns the original, clean version of a file to any process that tries to read it — including the antivirus scanner. What type of virus is this?**

- A) Tunneling Virus
- B) Armored Virus
- C) Cavity Virus
- D) ✅ Stealth Virus

**Explanation:**

- **A** is incorrect — a tunneling virus bypasses AV by going directly to BIOS/DOS interrupt handlers *underneath* the OS call layer, not by intercepting and spoofing the results of file-read requests.
- **B** is incorrect — an armored virus uses anti-disassembly and anti-debugging techniques to resist researcher analysis, not OS call interception.
- **C** is incorrect — a cavity virus fills empty sections inside executables to avoid increasing file size. It does not interact with OS read calls.
- **D** ✅ is correct — a stealth virus actively hides its presence by hooking OS interrupt handlers. When any process (including AV) requests to read an infected file, the stealth virus intercepts the request and returns the original, unmodified version — making the infection completely invisible to the scanner. The virus must be active in memory for this to work; booting from clean media exposes it.

---

### Q06

**Which two characteristics together DEFINE a multipartite virus?**

- A) Encrypts payload AND mutates decryption stub per infection
- B) Spreads via email AND infects macro-enabled documents
- C) ✅ Infects both the boot sector AND executable files simultaneously
- D) Infects files selectively AND uses date-based triggers

**Explanation:**

- **A** is incorrect — encrypting payload and mutating the decryptor defines a **polymorphic** virus.
- **B** is incorrect — email spreading and macro infection describe a **macro virus** (e.g., Melissa).
- **C** ✅ is correct — a multipartite virus has a dual infection vector: it attacks both the boot sector (MBR/VBR) and executable files simultaneously. This dual-vector strategy makes it extremely difficult to remove — cleaning the files without cleaning the boot sector results in re-infection on next boot, and vice versa.
- **D** is incorrect — selective infection describes a **sparse infector**; date-based triggers describe the virus lifecycle triggering phase — neither combination defines multipartite.

---

### Q07

**The CIH (Chernobyl) virus is best classified as which type, and what made its payload uniquely destructive beyond typical viruses?**

- A) Polymorphic virus — it mutated its signature with every infection to avoid detection
- B) Boot sector virus — it overwrote the MBR making the system unbootable
- C) ✅ Cavity (space-filler) virus — it filled empty PE file sections without increasing file size, and overwrote BIOS flash memory causing hardware-level damage
- D) Stealth virus — it intercepted disk read operations to hide its presence from AV scanners

**Explanation:**

- **A** is incorrect — CIH was not polymorphic. It did not use a mutation engine or encryption/decryptor mechanism.
- **B** is incorrect — CIH targeted empty sections in PE executable files, not the MBR specifically. Boot sector viruses define themselves by MBR/VBR infection.
- **C** ✅ is correct — CIH is the canonical cavity virus. It inserted itself into empty (slack space) regions of Portable Executable files without increasing their size — defeating file-size-based detection. Its destructive payload, triggered on April 26 (Chernobyl disaster anniversary), overwrote the BIOS flash chip — causing hardware-level damage that rendered machines physically unbootable, requiring chip replacement on some motherboards.
- **D** is incorrect — CIH did not use OS call interception as its mechanism; that defines stealth viruses.

---

### Q08

**A virus modifies the File Allocation Table (FAT) directory entries so that all execution requests are redirected through the virus code first — but the actual contents of executable files are never touched. Which type is this?**

- A) Overwriting Virus
- B) Sparse Infector Virus
- C) Cavity Virus
- D) ✅ Cluster Virus

**Explanation:**

- **A** is incorrect — an overwriting virus replaces the actual file content with its own code, destroying the original. The question explicitly states file contents are NOT modified.
- **B** is incorrect — a sparse infector selectively infects files based on criteria like file size or access counter. It does not manipulate directory entries or FAT structures.
- **C** is incorrect — a cavity virus places itself in empty sections within a PE file. It modifies the file itself — not the directory entries pointing to it.
- **D** ✅ is correct — a cluster virus (also called a file system virus) manipulates FAT or directory table entries to redirect all execution through the virus code without touching the actual file content. Only one copy of the virus exists on disk, pointed to by all infected directory entries — making it appear as a single infection while effectively affecting every executable.

---

### Q09

**Which virus type deliberately infects only every nth file it encounters, or only files meeting specific size criteria — specifically to reduce its detection probability?**

- A) Armored Virus
- B) Tunneling Virus
- C) Metamorphic Virus
- D) ✅ Sparse Infector Virus

**Explanation:**

- **A** is incorrect — armored viruses resist analysis using anti-debugging and anti-disassembly techniques. Their evasion strategy is about resisting researcher analysis, not reducing infection frequency.
- **B** is incorrect — tunneling viruses bypass AV monitors by going directly to BIOS/DOS interrupts. Infection frequency is not their evasion mechanism.
- **C** is incorrect — metamorphic viruses rewrite their entire code body on each infection to evade signature detection. They do not selectively limit infection frequency.
- **D** ✅ is correct — a sparse infector deliberately limits how often it infects to reduce its footprint. By infecting only every nth file accessed, or only files above a certain size, it generates fewer file system changes, making it harder for heuristic and behavioural monitoring to notice unusual activity patterns.

---

### Q10

**An analyst notices that a specific virus infects prepends code to `.exe` files — increasing their size — but also uses a technique where the virus code fills empty slack regions inside PE files on some infections without increasing file size. Which TWO virus types does this analyst have evidence of?**

- A) Stealth Virus and Tunneling Virus
- B) Multipartite Virus and Armored Virus
- C) ✅ File Infector Virus (prepending) and Cavity Virus (space-filling)
- D) Cluster Virus and Overwriting Virus

**Explanation:**

- **A** is incorrect — stealth viruses hide via OS call interception; tunneling viruses bypass AV interrupt hooks. Neither is defined by prepending code or filling empty sections.
- **B** is incorrect — multipartite targets boot sector + files; armored resists analysis. Neither matches the described mechanisms.
- **C** ✅ is correct — **prepending code to .exe and increasing file size** = classic **file infector virus** (prepending variant). **Filling empty PE sections without increasing file size** = **cavity (space-filler) virus**. The analyst is observing two distinct infection mechanisms, possibly from the same virus using different techniques on different targets.
- **D** is incorrect — a cluster virus modifies directory entries without touching file content; an overwriting virus destroys original content. Neither involves prepending code or cavity filling.

---

## Questions 11–18 — AV Evasion Techniques

---

### Q11

**An attacker uses UPX to compress a malware executable so that the original binary signature is no longer detectable by AV scanners. A small stub decompresses the original code in memory at runtime. Which evasion technique is this?**

- A) Process Injection
- B) Code Obfuscation
- C) Metamorphism
- D) ✅ Packing / Compression

**Explanation:**

- **A** is incorrect — process injection involves inserting malicious code into the memory space of a legitimate running process. It does not involve compressing the executable file itself.
- **B** is incorrect — code obfuscation transforms code structure (variable renaming, dead code insertion, string splitting) without producing a compressed binary with a runtime decompression stub.
- **C** is incorrect — metamorphism rewrites the entire virus code on each infection using code transformation techniques. It operates at the instruction level, not as file-level compression.
- **D** ✅ is correct — packing uses a compression tool (UPX, MPRESS, ASPack, or custom packers) to produce a compressed binary. A small decompression stub unpacks and executes the original code in memory at runtime. The on-disk binary has a completely different byte signature from the original — AV signature database has no match.

---

### Q12

**Which of the following BEST and MOST precisely distinguishes polymorphic evasion from metamorphic evasion?**

- A) Polymorphic viruses rewrite their entire code per infection; metamorphic viruses only encrypt their payload
- B) ✅ Polymorphic viruses encrypt the payload and mutate the decryption stub per infection; metamorphic viruses rewrite their entire code body without using encryption
- C) Polymorphic viruses use anti-VM techniques; metamorphic viruses use runtime packers
- D) Polymorphic and metamorphic are different terms for the same code mutation technique

**Explanation:**

- **A** is the exact reversal of the correct answer — the most common trap on this topic. Polymorphic mutates the decryptor stub; metamorphic rewrites the full code.
- **B** ✅ is correct — in a **polymorphic** virus, the payload is encrypted and a mutation engine changes the decryption stub on each infection, producing a different binary signature every time while the underlying behaviour is identical. In a **metamorphic** virus, no encryption is used at all — the virus rewrites its entire code body using code transposition, instruction substitution, dead code insertion, and register renaming. There is no decryption stub to detect.
- **C** is incorrect — anti-VM and runtime packers are separate evasion techniques completely unrelated to the polymorphic/metamorphic distinction.
- **D** is incorrect — these are fundamentally different mechanisms. Polymorphic is encryption-based mutation; metamorphic is structural code rewriting. Metamorphic is significantly harder to detect.

---

### Q13

**A malware sample checks for the registry key `HKLM\SOFTWARE\VMware, Inc.\VMware Tools` and the MAC address prefix `00:0C:29` at startup. If either is detected, it exits without executing its payload. Which evasion technique does this represent?**

- A) Timing-Based Evasion
- B) Rootkit Integration
- C) File Extension Spoofing
- D) ✅ Anti-VM / Anti-Debugging Technique

**Explanation:**

- **A** is incorrect — timing-based evasion involves the malware sleeping for a long period to outlast sandbox analysis time limits. It does not check for VM-specific registry keys or MAC addresses.
- **B** is incorrect — rootkit integration hides the malware from the OS by hooking kernel functions. The malware described is not hiding itself — it is detecting its analysis environment.
- **C** is incorrect — file extension spoofing involves disguising a malicious file as a different file type. Unrelated to environment detection.
- **D** ✅ is correct — checking for VMware-specific registry keys, the VMware OUI MAC prefix `00:0C:29`, VirtualBox driver files, sandbox-specific usernames, or analysis tool processes are all classic anti-VM techniques. The malware behaves benignly when it detects an analysis environment and only executes its real payload on a genuine victim machine — defeating sandbox-based detection.

---

### Q14

**Which evasion technique uses the Unicode Right-to-Left Override character (U+202E) to make a malicious executable appear to have a harmless `.jpg` extension when displayed in Windows Explorer?**

- A) Process Injection
- B) Code Obfuscation
- C) Packing
- D) ✅ File Extension Spoofing

**Explanation:**

- **A** is incorrect — process injection runs malicious code inside a legitimate process's memory space. It has no involvement with filename manipulation.
- **B** is incorrect — code obfuscation makes the internal code of malware harder to analyze. It does not affect how the filename appears to users.
- **C** is incorrect — packing compresses the binary to hide its signature from AV scanners. It has no effect on the displayed filename.
- **D** ✅ is correct — the Unicode RLO character (U+202E) reverses the display direction of all following characters. A file named `photo_[RLO]gpj.exe` displays as `photo_exe.jpg` in Windows Explorer — making a dangerous executable appear as a harmless JPEG image to the user, who then double-clicks it expecting to see a photo.

---

### Q15

**A malware sample injects its shellcode into the `explorer.exe` process so that all its network connections appear to originate from a legitimate Windows shell process. Which evasion technique is this?**

- A) Rootkit Integration
- B) Tunneling Virus Technique
- C) Metamorphism
- D) ✅ Process Injection

**Explanation:**

- **A** is incorrect — rootkit integration hides files, processes, and registry entries from the OS by hooking kernel functions at the driver level. The technique described injects into an existing process rather than hiding at kernel level.
- **B** is incorrect — tunneling (in the virus context) means a virus bypasses AV interceptors by going directly to BIOS/DOS interrupt handlers. It is completely unrelated to injecting shellcode into a running process.
- **C** is incorrect — metamorphism is a code rewriting technique applied to the virus body on each infection cycle. It is not a runtime technique for hiding inside a legitimate process.
- **D** ✅ is correct — process injection inserts malicious code into the memory space of a legitimate, trusted process (here `explorer.exe`). All activity — including network connections — then appears to originate from that trusted process. Security tools and network monitoring see only the legitimate process name, not the malicious code running within it.

---

### Q16

**The RDTSC (Read Time-Stamp Counter) x86 instruction is used by malware authors for which specific evasion purpose?**

- A) To encrypt the malware payload before writing it to disk
- B) To check whether the host operating system is Windows or Linux
- C) ✅ To detect virtual machine environments by measuring execution timing differences between bare metal and hypervisor-hosted execution
- D) To read registry keys and identify which antivirus product is installed

**Explanation:**

- **A** is incorrect — RDTSC reads the CPU's hardware timestamp counter register. It has no encryption functionality whatsoever.
- **B** is incorrect — OS type detection uses OS-specific API calls, file system paths, or environment variables. RDTSC has nothing to do with OS identification.
- **C** ✅ is correct — code executing inside a virtual machine runs noticeably slower than on bare hardware for timing-sensitive operations, because the hypervisor must intercept and translate hardware instructions. Malware executes RDTSC at two points in rapid succession and measures the elapsed clock cycles. If the delta is unusually large (indicating VM overhead), the malware concludes it is being analyzed in a sandbox and exits cleanly.
- **D** is incorrect — registry key enumeration uses Windows API calls like `RegOpenKeyEx` or `RegQueryValueEx`. RDTSC is a CPU timing instruction with no registry access capability.

---

### Q17

**Which evasion technique involves a virus bypassing resident AV monitors by directly invoking BIOS INT 13h (disk I/O interrupt) rather than going through the standard OS interrupt layer where AV hooks are installed?**

- A) Armored Virus Technique
- B) Stealth Virus Technique
- C) ✅ Tunneling Virus Technique
- D) Rootkit Integration

**Explanation:**

- **A** is incorrect — armored virus techniques use anti-debugging traps, misleading disassembly, and complex control flow to resist reverse engineering and analysis. They do not specifically bypass OS interrupt hooks.
- **B** is incorrect — stealth viruses intercept OS calls to *hide their presence* by returning clean data to scanners. Tunneling viruses *bypass the OS call layer entirely*. These are opposite approaches.
- **C** ✅ is correct — a tunneling virus specifically "tunnels" beneath the AV-monitored OS interrupt layer by directly invoking BIOS INT 13h (disk read/write) or DOS INT 21h. AV products install hooks at the OS interrupt level — if the virus bypasses this layer entirely, those hooks never fire and the virus operates undetected.
- **D** is incorrect — rootkit integration hides files and processes at the kernel driver level using SSDT hooks or DKOM (Direct Kernel Object Manipulation). This is a different mechanism from bypassing interrupt handlers.

---

### Q18

**What is the PRIMARY technical limitation of using simple encryption as an antivirus evasion technique — and what development did this limitation directly lead to?**

- A) Encryption increases file size significantly, making encrypted malware trivially detectable by size-based scanning
- B) Encrypted malware cannot execute because the operating system cannot load encrypted code into memory
- C) ✅ The decryption stub must remain in plaintext to execute — it becomes a stable, detectable signature — directly leading to the development of polymorphism to mutate the stub
- D) Encryption is computationally expensive, causing noticeable system slowdown that triggers behavioural detection

**Explanation:**

- **A** is incorrect — while encryption does add a small stub, file size alone is not the reason simple encryption fails. Many detection methods do not rely on file size.
- **B** is incorrect — the malware handles its own decryption. A small plaintext decryption stub runs first, decrypts the payload into memory, and executes it. The OS is not involved in decryption.
- **C** ✅ is correct — when a virus encrypts its payload with a fixed key and a fixed decryption routine, that decryption stub (which must always be stored in plaintext) becomes a consistent, extractable byte signature. AV vendors extract this stub and add it to their database — all copies of the virus are then detected via the stub's signature. Polymorphism was developed specifically to solve this: by mutating the decryption stub on every infection, no two copies share the same stub signature.
- **D** is incorrect — the computational cost of simple XOR or RC4 encryption is negligible and does not produce detectable system slowdown in any meaningful sense.

---

## Questions 19–24 — Detection Methods

---

### Q19

**Which virus detection method requires a known-clean baseline snapshot and detects infections by periodically recalculating file hashes and comparing them against stored values — regardless of the malware type responsible for any change?**

- A) Signature-Based Detection
- B) Behavior-Based Detection
- C) Heuristic-Based Detection
- D) ✅ Integrity Checking / Checksumming

**Explanation:**

- **A** is incorrect — signature-based detection compares file content against a database of known malware byte patterns. It does not compute or compare baseline hashes of system files.
- **B** is incorrect — behavior-based detection monitors live runtime actions of executing programs. It does not compare file states before and after.
- **C** is incorrect — heuristic detection analyzes code structure or emulates execution to find suspicious patterns. It does not require a clean baseline.
- **D** ✅ is correct — integrity checking (also called change detection) computes cryptographic hashes (SHA-256) of critical files at a known-clean state, stores them in a secure baseline database, then periodically recomputes and compares. Any deviation indicates unauthorized modification. It cannot identify *which* malware caused the change, but it reliably detects *any* unauthorized modification regardless of malware type — including zero-day and polymorphic threats that evade signature scanning.

---

### Q20

**A corporate email gateway runs suspicious attachments in a full isolated virtual machine, monitors all file system writes, registry changes, process creations, and network connections during execution, then flags the file as malicious if dangerous behaviour is observed. Which detection method is this?**

- A) Signature-Based Detection
- B) Heuristic Static Analysis
- C) Integrity Checking
- D) ✅ Sandboxing / Dynamic Analysis

**Explanation:**

- **A** is incorrect — signature-based detection compares file bytes against known signatures without executing the file.
- **B** is incorrect — heuristic static analysis examines code structure without running it. The scenario explicitly involves executing the file inside a virtual machine and monitoring live behaviour.
- **C** is incorrect — integrity checking compares file hashes against a clean baseline. It does not involve executing suspicious files.
- **D** ✅ is correct — sandboxing executes a suspicious file inside a fully isolated virtual machine environment. All system activity during execution is recorded and analyzed — file writes, registry changes, process creation, network connections, memory modifications. If malicious behaviour patterns are observed, the file is flagged. This is the definition of sandbox-based dynamic analysis as deployed in email gateways (e.g., Proofpoint, FireEye, Symantec).

---

### Q21

**Which AV detection method has the HIGHEST false positive rate, and what is the correct technical reason?**

- A) Signature-based detection — signatures can accidentally match partial content of legitimate files
- B) Integrity checking — any legitimate software update triggers a hash mismatch alert
- C) ✅ Heuristic and behavior-based detection — legitimate programs may exhibit code patterns or runtime behaviors that resemble malicious activity
- D) Cloud/reputation-based detection — new enterprise software has no established reputation score

**Explanation:**

- **A** is incorrect — signature-based detection is highly precise with a very low false positive rate because it matches exact known byte patterns from confirmed malware samples.
- **B** is a valid operational concern but not the detection method with the highest FP rate in terms of AV accuracy. Software updates trigger integrity alerts by design — this is a known workflow issue, not a detection accuracy limitation.
- **C** ✅ is correct — heuristic analysis flags code that *looks* suspicious based on structural patterns, and behavior-based detection flags actions that *resemble* malicious activity. Legitimate software that self-modifies, packs itself, hooks APIs, opens network connections, or modifies the registry may all trigger heuristic/behavioral alerts — even when completely benign. This is the well-established trade-off: better unknown threat detection at the cost of higher false positive rates.
- **D** is a valid concern — new software may have low reputation — but reputation systems include developer certificate trust and file metadata, keeping FP rates manageable. It is not the primary method associated with high FP rates.

---

### Q22

**An antivirus engine runs a suspicious executable inside a lightweight software-simulated CPU — executing its instructions step by step in a controlled environment to observe what API calls are made — without running it on the actual host system. Which specific detection method is this?**

- A) On-Access Scanning
- B) Behavior-Based Runtime Detection
- C) Integrity Checking
- D) ✅ Dynamic Heuristic Detection (Emulation)

**Explanation:**

- **A** is incorrect — on-access scanning intercepts file access requests in real time and checks the file before allowing execution. It does not simulate a CPU or step through instructions.
- **B** is incorrect — behavior-based runtime detection monitors actual program execution on the real host system. The question specifies a software-simulated CPU environment, not the real system.
- **C** is incorrect — integrity checking compares file hashes against a baseline. It does not execute or simulate code.
- **D** ✅ is correct — dynamic heuristic detection via emulation runs suspicious code inside a lightweight virtual CPU (software-based instruction emulator) built directly into the AV engine. This is distinct from full sandboxing (which uses a complete VM). The emulator executes the first N thousand instructions, observing what the code attempts to do — including unpacking encrypted payloads and detecting polymorphic decryption routines.

---

### Q23

**Against which threat category does signature-based detection COMPLETELY fail, and what is the precise reason?**

- A) Boot sector viruses — because they load before the AV engine can initialize
- B) Macro viruses — because they are written in interpreted VBA, not compiled binary
- C) ✅ Zero-day malware — because no signature exists for it yet in any AV database
- D) Worms — because worms do not produce a static file that can be scanned

**Explanation:**

- **A** is incorrect — boot sector viruses *can* have known signatures. AV tools can scan the MBR and VBR for known viral signatures. The timing challenge (before OS load) is a separate issue from signature availability.
- **B** is incorrect — AV tools have specific signatures for known VBA macro patterns and can scan Office document macro content. Macro viruses are regularly detected by signature-based AV.
- **C** ✅ is correct — signature-based detection requires a pre-existing entry in the AV signature database for the specific malware. For zero-day malware — newly created, previously undiscovered malware — no signature exists anywhere yet. No AV vendor has analyzed it, no signature has been generated, and no database entry exists. The scanner has literally nothing to match against.
- **D** is incorrect — worms produce executable code that exists as files on infected systems and can be scanned. Known worms have well-documented signatures in AV databases.

---

### Q24

**What is the precise operational difference between on-demand scanning and on-access scanning in antivirus software?**

- A) On-demand scanning uses signatures; on-access scanning uses heuristics exclusively
- B) On-access scanning only monitors network traffic; on-demand scanning covers local files
- C) On-demand scanning runs automatically on every file access; on-access scanning requires user initiation
- D) ✅ On-demand scanning runs when triggered by the user or a schedule; on-access scanning intercepts and scans every file at the moment it is accessed or executed — before it is allowed to run

**Explanation:**

- **A** is incorrect — both scanning modes can use signatures, heuristics, behavioral analysis, or any combination. The detection methods used are not what distinguishes them.
- **B** is incorrect — on-access scanning operates on the local file system by hooking into the OS file system driver. It is not limited to network traffic.
- **C** is the exact reversal of the correct answer — a very common MCQ trap. On-demand is user/scheduler-triggered. On-access fires automatically on every file access.
- **D** ✅ is correct — on-demand scanning scans files when a user manually initiates it or a scheduled task triggers it. On-access (real-time) scanning hooks into the OS kernel file system driver and intercepts every file open/execute request, scanning the file before it is allowed to execute. This provides the strongest protection — nothing executes without being scanned first.

---

## Questions 25–28 — Extra Notes & Real-World

---

### Q25

**Which of the following MOST accurately and completely describes the EICAR Standard Anti-Virus Test File?**

- A) A live but contained malware sample used in isolated lab environments to test AV removal and disinfection capability
- B) ✅ A harmless 68-byte file with zero malicious code that all compliant AV products must detect — used to verify AV is correctly installed and actively scanning without requiring real malware
- C) A file containing encoded shellcode used by penetration testers to verify sandbox escape capability
- D) A BIOS firmware image used by security researchers to test whether AV can detect boot sector infections

**Explanation:**

- **A** is incorrect — the EICAR test file is explicitly *not* malware of any kind. It is completely inert and harmless. It cannot damage, infect, or modify any system component.
- **B** ✅ is correct — EICAR (European Institute for Computer Antivirus Research) created a 68-byte file that all compliant AV vendors are contractually required to detect and flag. It is a `.com` file that, if executed as a DOS program, simply prints a string. It is used universally to verify AV installation, test email gateway filtering, and confirm AV is actively scanning — without using any real malware on any production system.
- **C** is incorrect — it contains no shellcode, no exploit code, no encoding for security testing, and no sandbox escape capability.
- **D** is incorrect — it has no relationship to BIOS firmware, boot sector testing, or hardware-level security testing of any kind.

---

### Q26

**The Dark Avenger's Mutation Engine (MtE), released in 1991, was historically significant because:**

- A) It was the first worm to propagate across the internet without any human intervention required
- B) It introduced the concept of encrypting malware payloads for the first time in history
- C) It was the first kernel-mode rootkit to hide processes from the Windows NT operating system
- D) ✅ It was the first widely released standalone polymorphic engine that any virus author could attach to their virus to instantly make it polymorphic — without needing to implement mutation logic themselves

**Explanation:**

- **A** is incorrect — the first internet worm was the Morris Worm in 1988, three years before MtE, and it had nothing to do with polymorphism.
- **B** is incorrect — encrypted virus payloads existed before MtE (e.g., Cascade in 1986 used simple encryption). MtE's innovation was *mutating the decryption routine*, not inventing payload encryption.
- **C** is incorrect — MtE was a DOS-era tool from 1991. Windows NT kernel-mode rootkits emerged significantly later in a completely different technical context.
- **D** ✅ is correct — MtE was a reusable, standalone polymorphic engine released to the underground. Any virus author could attach it to their existing virus binary, and MtE would automatically generate a new, unique-looking decryption stub with each infection — making previously simple, detectable viruses instantly polymorphic. This forced the entire AV industry to develop heuristic and emulation-based detection methods.

---

### Q27

**A worm author pre-compiles a list of 50,000 known vulnerable IP addresses by scanning the internet before releasing the worm. When released, the worm attacks this pre-compiled list first before switching to random scanning. Which propagation model describes the initial phase?**

- A) Random Scanning
- B) Topological Scanning
- C) Permutation Scanning
- D) ✅ Hit-List Scanning

**Explanation:**

- **A** is incorrect — random scanning probes random IP addresses from the entire IPv4 address space. It is slow in early stages because most probed IPs may not be vulnerable or even active.
- **B** is incorrect — topological scanning uses information found on the already-infected host itself (email contacts, ARP tables, browser history, network share lists) to identify next targets. It does not use a pre-compiled external list.
- **C** is incorrect — permutation scanning distributes the IP address space across all infected worm instances using a shared pseudo-random permutation, preventing duplicate scanning. It is a cooperative multi-instance strategy, not a pre-compiled list approach.
- **D** ✅ is correct — hit-list scanning uses a pre-compiled list of known vulnerable targets assembled by the attacker before worm release. By starting with confirmed vulnerable machines, the worm achieves explosive initial spread. Code Red II employed a variant of this technique. Hit-list scanning produces the fastest initial infection growth rate of any propagation model.

---

### Q28

**A malware analyst reports: "The sample rewrites its own entire instruction set on each execution cycle using register renaming, semantically equivalent opcode substitution, and junk code insertion — producing a completely different binary every time with no encryption or decryption stub present." Which classification is MOST accurate?**

- A) Polymorphic malware using a mutation engine to mutate its decryption stub
- B) Armored malware using anti-disassembly tricks to confuse security researchers
- C) Packed malware using a custom runtime decompression stub
- D) ✅ Metamorphic malware rewriting its entire code body using code transformation techniques

**Explanation:**

- **A** is incorrect — polymorphic malware encrypts its payload and mutates the *decryption stub*. The report explicitly states there is **no encryption or decryption stub present**. The entire code body rewrites itself — this is the definitional characteristic of metamorphic, not polymorphic.
- **B** is incorrect — armored malware uses anti-debugging traps and misleading disassembly to *resist analysis by researchers*. It does not produce a completely different binary on each execution cycle through code transformation.
- **C** is incorrect — packed malware uses a compression wrapper with a decompression stub. The report explicitly states no stub is present, and the technique described (register renaming, opcode substitution, junk code insertion) is code transformation, not compression.
- **D** ✅ is correct — register renaming, semantically equivalent instruction substitution, dead/junk code insertion, and code transposition are all definitional metamorphic transformation techniques. Metamorphic malware rewrites its entire code body on each generation, producing a functionally identical but structurally unique binary every time — with no encryption, no decryption stub, and no consistent byte-level pattern for signature detection to match against.

---

## Answer Key

| Q# | Answer | Topic Area |
|---|---|---|
| Q01 | C | Virus vs Worm — core definitional distinction |
| Q02 | D | Virus lifecycle — dormant phase |
| Q03 | D | Boot sector virus — MBR, pre-OS execution |
| Q04 | B | Macro virus — Melissa, VBA, Normal.dot |
| Q05 | D | Stealth virus — OS call interception |
| Q06 | C | Multipartite virus — dual vector definition |
| Q07 | C | CIH Chernobyl — cavity virus + BIOS overwrite |
| Q08 | D | Cluster virus — FAT/directory manipulation |
| Q09 | D | Sparse infector — selective infection |
| Q10 | C | File infector (prepending) + Cavity virus |
| Q11 | D | Packing / compression evasion — UPX |
| Q12 | B | Polymorphic vs metamorphic — precise distinction |
| Q13 | D | Anti-VM / Anti-debugging — environment detection |
| Q14 | D | File extension spoofing — RLO character |
| Q15 | C | Process injection — legitimate process abuse |
| Q16 | C | RDTSC timing — VM detection technique |
| Q17 | C | Tunneling virus — BIOS interrupt bypass |
| Q18 | C | Encryption limitation leading to polymorphism |
| Q19 | D | Integrity checking / checksumming |
| Q20 | D | Sandboxing / dynamic analysis |
| Q21 | C | False positive rate — heuristic vs signature |
| Q22 | D | Dynamic heuristic emulation vs full sandboxing |
| Q23 | C | Signature detection vs zero-day — complete failure |
| Q24 | D | On-demand vs on-access scanning |
| Q25 | B | EICAR test file — purpose and properties |
| Q26 | D | MtE — Dark Avenger — historical significance |
| Q27 | D | Hit-list worm propagation — fastest initial spread |
| Q28 | D | Metamorphic malware — full code rewriting |

---