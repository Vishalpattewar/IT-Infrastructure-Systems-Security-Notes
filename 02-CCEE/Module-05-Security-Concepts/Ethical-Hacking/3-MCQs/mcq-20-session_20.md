# MCQ Set — Session 20: Malware Types · Malicious Code Families · Malware Analysis 🔬

> 28 MCQs · 4 options each · Full explanations · Covers core + extra notes

---

## 📑 Table of Contents

- [Questions 01–06 — Malware Types & Families](#questions-0106--malware-types--families)
- [Questions 07–11 — Ransomware & Advanced Malware](#questions-0711--ransomware--advanced-malware)
- [Questions 12–16 — Static Analysis](#questions-1216--static-analysis)
- [Questions 17–22 — Dynamic Analysis & Sandboxing](#questions-1722--dynamic-analysis--sandboxing)
- [Questions 23–26 — Anti-Analysis Techniques](#questions-2326--anti-analysis-techniques)
- [Questions 27–28 — Extra Notes & Real-World](#questions-2728--extra-notes--real-world)
- [Answer Key](#answer-key)

---

## Questions 01–06 — Malware Types & Families

---

### Q01

**A piece of malware is discovered on a corporate network. It does not replicate itself, it does not attach to other files, and it does not encrypt any data. However, it silently records every keystroke typed by the user including banking passwords and sends them to a remote server every hour. Which malware category MOST precisely describes this?**

- A) Worm — because it spreads across the network to other machines automatically
- B) Ransomware — because it captures financial credentials for monetary gain
- C) Virus — because it attaches to user activity (keystrokes) and propagates behavior
- D) ✅ Spyware / Keylogger — it silently collects user data (keystrokes) and exfiltrates it without user knowledge — no replication, no encryption, no host file dependency

**Explanation:**

- **A** is incorrect — a worm self-replicates and spreads to other machines autonomously without needing a host file. The malware described does not replicate or spread — it stays on the infected machine and records keystrokes. No worm behavior is present.
- **B** is incorrect — ransomware encrypts files or systems and demands payment for decryption. Capturing credentials is a MEANS to financial gain — but the malware itself does not encrypt anything or demand ransom. Credential theft malware is spyware/infostealer — not ransomware.
- **C** is incorrect — a virus attaches to executable host files and replicates when those files are executed. Recording keystrokes is not virus behavior. The malware does not attach to files or self-replicate — these are the defining virus characteristics.
- **D** ✅ is correct — **Spyware** is malware that silently collects information about users without their knowledge and transmits it to a remote party. **Keyloggers** are a specific type of spyware that records keystroke sequences. The described malware exhibits all spyware/keylogger characteristics: **(1)** Silent operation — user is unaware. **(2)** Data collection — keystrokes including passwords. **(3)** Exfiltration — periodic transmission to attacker's server. **(4)** No replication, no file infection, no encryption — pure surveillance. This category also includes infostealers (RedLine, Raccoon) that harvest browser credentials, cryptocurrency wallets, and session cookies.

---

### Q02

**What is the precise technical distinction between a logic bomb and a backdoor — and what property do they share that distinguishes both from immediately active malware?**

- A) Logic bombs use encryption; backdoors use cleartext communication — the distinction is cryptographic
- B) Logic bombs target Linux; backdoors target Windows — the distinction is the target operating system
- C) Logic bombs are created by external attackers; backdoors are created by insiders — the distinction is attacker identity
- D) ✅ A logic bomb remains dormant and executes its payload ONLY when a specific trigger condition is met (date, counter, file existence, user login); a backdoor provides persistent covert remote access bypassing normal authentication; both share the property of initially appearing benign — neither causes immediate visible damage on infection

**Explanation:**

- **A** is incorrect — neither logic bombs nor backdoors are defined by their use of encryption. Both can use encrypted or unencrypted communications depending on implementation. The defining characteristics are their triggering mechanism and purpose — not cryptographic properties.
- **B** is incorrect — both logic bombs and backdoors exist across all operating systems (Windows, Linux, macOS, embedded systems). The distinction is not platform-specific. Cross-platform versions of both categories are well-documented in malware research.
- **C** is incorrect — both logic bombs and backdoors can be planted by external attackers (via malware delivery) OR by malicious insiders. Logic bombs ARE disproportionately associated with insider threats (disgruntled employees planting time-triggered payloads) but are not exclusively insider tools. The identity of the creator is not the technical distinction.
- **D** ✅ is correct — precise technical distinction: **Logic bomb**: executes a payload only when a predetermined condition is triggered. Common triggers: specific date/time ("activate on April 1"), counter-based ("after 100 executions"), event-based ("when user account is deleted"), file existence check ("if cleanup_file.txt not present"). Until trigger fires: appears benign, may be embedded in legitimate software. After trigger: destructive payload (delete files, encrypt disk, crash system, exfiltrate data). **Backdoor**: provides persistent covert remote access mechanism — listening on a port, connecting to C2, accepting commands — bypassing normal authentication. Provides ongoing access rather than a one-time payload detonation. **Shared property**: both initially appear harmless — neither causes immediate visible damage upon installation — making them particularly dangerous for detection.

---

### Q03

**A security analyst investigates a compromised Windows server and finds that the malware running in memory has no corresponding file on the hard disk. Process Monitor shows PowerShell executing encoded commands, and Wireshark shows encrypted outbound connections to a domain generated algorithmically. Which malware category does this describe and which Windows security feature is the primary defense?**

- A) Rootkit — the malware hides its files using kernel hooks; primary defense is rkhunter
- B) Worm — the malware spreads to other machines leaving no files; primary defense is network segmentation
- C) Trojan — the malware disguises itself as PowerShell; primary defense is application whitelisting
- D) ✅ Fileless malware — executes entirely in memory using legitimate OS tools (PowerShell/LOLBins) leaving no disk artifact — primary defense is AMSI (Antimalware Scan Interface) which scans script content before execution regardless of obfuscation

**Explanation:**

- **A** is incorrect — rootkits hide their presence using kernel hooks but typically have files on disk (the kernel module itself, supporting libraries). The defining characteristic described is NO DISK FILE at all — memory-only execution. Rootkits hide from file system queries — fileless malware never writes to the file system. rkhunter checks for known rootkit signatures in files — ineffective against memory-only execution.
- **B** is incorrect — worms self-replicate and spread to other machines. The described malware shows no spreading behavior — it runs in memory on one machine, uses PowerShell for execution, and communicates with a DGA-generated C2. Network segmentation limits worm spread — it does not address in-memory execution.
- **C** is incorrect — a Trojan is disguised as legitimate software to trick users into running it. PowerShell itself is a legitimate tool — the malware is using it (LotL — Living off the Land) rather than disguising itself AS it. Application whitelisting would prevent unauthorized executables — but PowerShell is whitelisted on most systems (defeating this control for LotL attacks).
- **D** ✅ is correct — **fileless malware** characteristics all present: **(1)** No corresponding disk file — memory-only execution. **(2)** PowerShell encoded commands — obfuscated LotL technique using a built-in OS tool. **(3)** DGA (Domain Generation Algorithm) generated C2 domains — provides resilient C2 infrastructure. **AMSI** (Antimalware Scan Interface) is Windows 10+'s primary defense: it intercepts script execution (PowerShell, VBScript, JScript) and submits the CONTENT (after de-obfuscation) to registered security products for inspection — even if the script is Base64-encoded or obfuscated, AMSI scans the decoded content before execution. Attackers target AMSI bypass as a first step in fileless attacks.

---

### Q04

**Which of the following CORRECTLY describes the technical mechanism that makes a rootkit fundamentally different from other malware that simply hides files using file attributes (hidden attribute, `.` prefix on Linux)?**

- A) Rootkits use stronger encryption — AES-256 encrypted files cannot be found by file system scanners
- B) Rootkits operate via network protocols — they hide on remote servers rather than locally
- C) Rootkits only affect the Windows registry — Linux systems cannot be infected by rootkits
- D) ✅ Rootkits hook kernel-level functions (sys_call_table on Linux, SSDT on Windows) so that even OS-level queries return falsified results — the hiding is enforced at the OS kernel layer, not at the application layer, making detection impossible using standard OS tools running above the kernel

**Explanation:**

- **A** is incorrect — file encryption is not the rootkit mechanism. Encrypting files would protect their contents from reading — but a filesystem scanner would still see the encrypted files present. Rootkits make files INVISIBLE to scanners — not unreadable. The hiding is achieved through system call interception, not cryptography.
- **B** is incorrect — rootkits run locally on the compromised machine — they do not operate via network protocols or reside on remote servers. Some rootkits DO communicate with remote C2 servers, but their HIDING mechanism is local kernel manipulation — not remote operation.
- **C** is incorrect — rootkits exist for all major operating systems. Linux LKM (Loadable Kernel Module) rootkits are well-documented — hooking sys_call_table in the Linux kernel. Windows rootkits hook the SSDT (System Service Descriptor Table) or use kernel object manipulation (DKOM). macOS rootkits exist as kernel extensions.
- **D** ✅ is correct — rootkit hiding mechanism: **(1)** Normal filesystem hiding (hidden attribute, dot-prefix): the file exists in kernel data structures — any scan that bypasses the attribute check (e.g., `ls -a`, `dir /ah`) reveals it. The OS kernel knows the file exists. **(2)** Rootkit kernel hooking: the rootkit REPLACES kernel function pointers (e.g., `sys_getdents64` on Linux — used to list directory contents) with its own functions. When ANY program (including AV software) calls the system function to list files, the rootkit's function runs instead — it filters out its own files from the results before returning to the caller. The OS kernel itself returns falsified data. No standard tool running above the kernel can detect the hidden files because they all use the same compromised kernel interface. **Detection requires**: running from clean boot media (rootkit not loaded), cross-view tools comparing kernel-reported data vs raw disk data, or kernel integrity monitoring (LKRG on Linux, Kernel Patch Protection on Windows).

---

### Q05

**A malware sample is described as a "dropper." What is its specific function in a multi-stage malware attack and how does it differ from the final payload?**

- A) A dropper is the final stage of malware — it drops the decryption key needed for ransomware
- B) A dropper is a network relay — it drops (forwards) traffic between the victim and C2 server
- C) A dropper and the final payload are the same thing — "dropper" is an older term for any malware
- D) ✅ A dropper is a FIRST-STAGE malware component whose sole purpose is to install (drop) additional malware onto the system — the dropper itself may be small and benign-looking, evades initial AV detection, then downloads or extracts and executes the actual payload (RAT, ransomware, infostealer) once on the target system

**Explanation:**

- **A** is incorrect — a dropper is the FIRST stage, not the final stage. It installs OTHER malware — it is not the payload itself. The concept of "dropping a decryption key" is unrelated to the dropper malware category definition.
- **B** is incorrect — a dropper does not relay network traffic. Network relay functionality is associated with proxy bots or tunnel malware — not droppers. A dropper's function is specifically the installation of other software on the local system.
- **C** is incorrect — dropper and payload are distinct components with different purposes. Using "dropper" as a synonym for any malware loses the important architectural distinction. Multi-stage malware specifically separates delivery (dropper/loader) from capability (payload) to improve evasion and modularity.
- **D** ✅ is correct — **dropper architecture**: **(1)** Dropper arrives via phishing attachment, drive-by download, or removable media — typically small, may appear as legitimate document or installer. **(2)** Dropper's ONLY job: establish a foothold on the system and install the actual malware. Methods: download from C2 ("downloader" variant), or contain the payload embedded/encrypted within itself ("dropper" strict definition). **(3)** Final payload: the actual malicious capability — RAT providing remote access, ransomware for encryption, infostealer for credential theft, cryptominer for CPU abuse. **(4)** Separation purpose: the dropper is designed to bypass initial AV detection (small, less suspicious) — the actual payload is downloaded after the initial security layer is bypassed. Emotional (banking Trojan) and TrickBot used sophisticated multi-stage dropper architectures — the initial document macro was just a dropper for the real banking malware.

---

### Q06

**The malware family known as "wiper" malware represents a specific destructive category. What distinguishes a wiper from ransomware — and what does this imply about the attacker's motivation?**

- A) Wipers encrypt data like ransomware but also delete the decryption key — the distinction is key management
- B) Wipers only target Linux systems; ransomware only targets Windows — the distinction is OS targeting
- C) Wipers and ransomware are functionally identical — both prevent data access — the distinction is only marketing
- D) ✅ Wiper malware permanently and irreversibly destroys data (overwrites with zeros/random bytes, destroys MBR, corrupts filesystem structures) with NO ransom demand and NO recovery mechanism — the attacker's motivation is sabotage/destruction, not financial gain — wipers are typically nation-state or hacktivist tools deployed for geopolitical objectives

**Explanation:**

- **A** is incorrect — wipers do not use encryption that could theoretically be reversed with a key. Wipers overwrite data with zeros, random bytes, or corrupt filesystem structures — the data is physically gone. There is no key to manage — the destruction is irreversible by design. If a decryption key exists somewhere, it is ransomware, not a wiper.
- **B** is incorrect — wipers and ransomware both exist for Linux and Windows. NotPetya (2017) targeted Windows. Shamoon targeted Windows in Middle Eastern oil infrastructure. Linux wipers have been deployed against Ukrainian systems. The platform targeting is not the distinguishing characteristic.
- **C** is incorrect — while both prevent data access temporarily, the KEY difference is intentionality and reversibility. Ransomware INTENDS for the victim to recover data — after payment. Recovery is the point (leverage for payment). Wipers INTEND for data to be permanently lost — there is no path to recovery. The attacker's motivation (financial vs destructive) is fundamentally different.
- **D** ✅ is correct — **wiper characteristics**: **(1) Irreversible destruction**: overwrites file contents, MBR (preventing boot), partition tables, filesystem metadata. Even forensic recovery is impossible after thorough wiping. **(2) No ransom demand**: the attacker gains nothing financial — destruction IS the objective. **(3) Motivation**: sabotage (disable competitor's operations), geopolitical (nation-state attacking adversary infrastructure), insider revenge (disgruntled employee destroying employer's data). **(4) Examples**: Shamoon (2012, 2016, 2018 — Saudi Aramco), NotPetya (2017 — disguised as ransomware, actually a wiper — $10B damage), HermeticWiper (2022 — Ukraine), CaddyWiper (2022 — Ukraine). NotPetya is the canonical example — appeared to be ransomware but deliberately destroyed data with no genuine recovery path — attributed to Russian GRU.

---

## Questions 07–11 — Ransomware & Advanced Malware

---

### Q07

**What is "double extortion" in modern ransomware operations — and why was this innovation necessary from the attacker's perspective after organizations improved their backup strategies?**

- A) Double extortion means charging victims twice — once to decrypt files and once to remove themselves from victim's network
- B) Double extortion refers to ransomware that attacks both the victim organization and their customers simultaneously
- C) Double extortion means the ransomware encrypts files twice with different keys — making decryption twice as difficult
- D) ✅ Double extortion combines file encryption (traditional ransomware) with DATA EXFILTRATION before encryption — attackers threaten to publicly publish stolen sensitive data if ransom is not paid — this defeats the "restore from backup" countermeasure because backups do not prevent the PUBLICATION of already-stolen data

**Explanation:**

- **A** is incorrect — double extortion does not refer to a two-payment scheme for the same service. It refers to TWO SEPARATE THREATS: encryption (restore access) and publication (prevent disclosure). Some groups do offer staged payments but the "double" in double extortion refers to the two distinct leverage mechanisms.
- **B** is incorrect — while some ransomware attacks have downstream effects on customers, double extortion specifically refers to the attacker's leverage strategy against the TARGET organization — not simultaneous attacks on multiple parties. The "double" refers to the two pressure mechanisms against the same victim.
- **C** is incorrect — double encryption (nested encryption) is a separate technique used by some ransomware groups (e.g., two affiliates encrypting the same victim) creating decryption complexity. This is technically different from double extortion, which combines encryption with data theft threats.
- **D** ✅ is correct — **double extortion evolution**: **(1) Traditional ransomware** (pre-2019): encrypt files → demand payment → decrypt. **Victim countermeasure**: restore from offline backup → no payment needed → ransomware threat defeated. **(2) Attacker adaptation**: if backups eliminate payment incentive, add a second threat. **(3) Double extortion** (Maze ransomware pioneered 2019): BEFORE encrypting, exfiltrate sensitive data to attacker's servers → THEN encrypt. Now victim faces TWO threats: files encrypted (operational disruption) AND sensitive data stolen (regulatory breach, reputational damage, DPDPA liability). Restoring from backup fixes the encryption — but does NOT undo the data theft. The threat to publish customer PII, financial records, or trade secrets creates independent pressure to pay regardless of backup status. **(4) Triple extortion** (further evolution): add DDoS attack on victim's infrastructure as a third lever. Groups: Maze (pioneered), REvil, Conti, LockBit, BlackCat/ALPHV all use double/triple extortion.

---

### Q08

**The Ransomware-as-a-Service (RaaS) model has transformed the ransomware ecosystem. What does RaaS mean technically and operationally — and why does it make ransomware attacks harder to attribute and prevent?**

- A) RaaS means ransomware is deployed via cloud services — attackers rent AWS/Azure infrastructure for distribution
- B) RaaS means ransomware is automatically deployed as soon as a vulnerability is discovered — no human operator involved
- C) RaaS means only one organization (the RaaS operator) is responsible for all ransomware attacks using their platform
- D) ✅ RaaS is a criminal business model where ransomware developers license their malware to affiliates — affiliates conduct the attacks and keep 70–80% of ransom revenue — the developer maintains the encryption code, payment portal, and negotiation infrastructure — this separates technical development from attack execution, creating attribution difficulty and expanding attack scale beyond any single group's capacity

**Explanation:**

- **A** is incorrect — RaaS refers to the CRIMINAL BUSINESS MODEL (analogous to legitimate SaaS) — not to the cloud infrastructure used for delivery. While RaaS operators may use cloud infrastructure, the "as-a-Service" designation describes the subscription/affiliate relationship between malware developers and operators — not the delivery mechanism.
- **B** is incorrect — RaaS attacks require significant human operator involvement. Affiliates must: gain initial access (phishing, exploiting vulnerabilities, purchasing access from initial access brokers), move laterally within the network, identify and exfiltrate valuable data, and deploy the ransomware. Full automation is not the model — human expertise is still required for the attack execution phase.
- **C** is incorrect — attribution to a SINGLE organization is what RaaS makes DIFFICULT. The RaaS developer and their potentially dozens or hundreds of affiliates are separate criminal entities. An attack attributed to "LockBit" may have been executed by any of hundreds of affiliates who purchased access to the LockBit platform — not by the core LockBit developers themselves.
- **D** ✅ is correct — **RaaS business model**: **(1) Developer role**: creates and maintains ransomware code, encryption implementation, payment portal (Tor .onion site), decryption key management, victim support (negotiation chat), leak site for double extortion. **(2) Affiliate role**: purchases access to RaaS platform (subscription or profit share), handles attack execution — reconnaissance, initial access, lateral movement, data exfiltration, ransomware deployment. **(3) Revenue split**: typically 70–80% to affiliate, 20–30% to developer. **(4) Attribution complexity**: an attack may be technically attributable to "LockBit 3.0" malware but the human operators are anonymous affiliates — potentially in different countries than developers. Law enforcement must identify both developers AND affiliates separately. **(5) Scale**: RaaS enables dozens of simultaneous campaigns by different affiliates using the same ransomware — dramatically increasing attack frequency beyond what a single group could execute.

---

### Q09

**The SolarWinds supply chain attack (2020) is considered one of the most sophisticated cyberattacks in history. What specific supply chain technique made it so difficult to detect and prevented standard security controls from blocking it?**

- A) SolarWinds attackers used a zero-day in Windows Update — all Windows machines automatically installed the backdoor
- B) SolarWinds attackers sent phishing emails to all 18,000 affected organizations simultaneously
- C) SolarWinds attackers exploited a vulnerability in firewall firmware — the attack bypassed network inspection entirely
- D) ✅ Attackers compromised the SolarWinds software BUILD PROCESS — inserting the SUNBURST backdoor into legitimate, digitally-signed SolarWinds Orion software updates — organizations installed it themselves as a trusted vendor update, bypassing all security controls that whitelist software from trusted vendors

**Explanation:**

- **A** is incorrect — the SolarWinds attack was NOT distributed via Windows Update. It was distributed through SolarWinds' own software update mechanism for their Orion IT monitoring platform. Windows Update was not involved. The attack targeted the SolarWinds build/delivery pipeline specifically.
- **B** is incorrect — the SolarWinds attack was NOT a phishing campaign. No phishing emails were sent to the 18,000 affected organizations. The attack was entirely supply chain based — victims installed the malware themselves as a routine software update. Phishing is an active attack requiring victim interaction with a malicious message — this was passive installation of a compromised update.
- **C** is incorrect — firewall firmware was not the attack vector. The attackers compromised SolarWinds' internal software development/build environment — not network infrastructure. The attack targeted the software supply chain — the process by which SolarWinds compiled and signed their product updates.
- **D** ✅ is correct — **SUNBURST supply chain attack**: **(1)** Attackers (attributed to Russian SVR / Cozy Bear / APT29) compromised SolarWinds' software build environment in 2019. **(2)** Malicious code (SUNBURST backdoor) was inserted into the Orion software build process — the backdoor compiled into the legitimate product binary. **(3)** SolarWinds' code-signing process signed the malicious binary — the digital signature was AUTHENTIC — from SolarWinds' legitimate certificate. **(4)** The compromised update was distributed to ~18,000 SolarWinds Orion customers as a routine, recommended software update. **(5)** Security controls that typically block unknown software — application whitelisting, AV signatures, firewall rules — all whitelisted the update because it came from a trusted vendor, had a valid digital signature, and was a legitimate product update. **(6)** SUNBURST lay dormant for 12–14 days after installation before activating — defeating automated sandbox analysis (typical sandbox timeout 2–5 minutes).

---

### Q10

**What is the CVE-2024-3094 / XZ Utils backdoor and why did it represent a particularly sophisticated supply chain attack different from SolarWinds?**

- A) XZ Utils was attacked via a DNS poisoning attack that redirected download servers to serve backdoored packages
- B) XZ Utils was a ransomware attack targeting Linux servers through a misconfigured SSH port
- C) XZ Utils was automatically patched by all major Linux distributions within 24 hours — no systems were affected
- D) ✅ A malicious contributor (Jia Tan) spent approximately TWO YEARS building trust and credibility in the XZ Utils open-source project before inserting a backdoor into the compression library — the backdoor targeted SSH authentication on systemd-linked distributions — representing the first documented long-term social engineering of an open-source project maintainer

**Explanation:**

- **A** is incorrect — XZ Utils was not compromised via DNS poisoning. The attacker directly contributed malicious code to the legitimate source code repository after establishing trust as a project contributor. DNS poisoning redirects downloads — this attack modified the ACTUAL SOURCE CODE of the project itself.
- **B** is incorrect — XZ Utils is a data compression library — not ransomware. The backdoor targeted SSH authentication (specifically OpenSSH linked against systemd, which in turn linked against the backdoored liblzma/XZ library) — enabling unauthorized remote authentication bypass. No ransomware was involved.
- **C** is incorrect — while the backdoor WAS discovered before widespread deployment (discovered by Andres Freund in February 2024 while investigating unusual SSH performance) and patched quickly, the near-miss was significant precisely because it almost went undetected. The attack was sophisticated enough that it reached the release candidate stage of several major Linux distributions (Fedora Rawhide, some Debian unstable builds).
- **D** ✅ is correct — XZ Utils attack timeline (2021–2024): **(1)** "Jia Tan" (pseudonym — likely state actor) begins contributing legitimate bug fixes and improvements to XZ Utils in 2021. **(2)** Over ~2 years: builds a reputation as a valuable contributor, gains maintainer trust, eventually receives commit access. **(3)** Gradually introduces complexity: scripts, build system changes — each individually innocuous. **(4)** Early 2024: inserts backdoor in the build system (not directly in source code — in the build scripts that generate the distributed binary) — targeting OpenSSH authentication on systems using systemd. **(5)** Detected by Andres Freund (Microsoft) who noticed 500ms SSH login delays on Debian Sid and investigated. **(6)** Significance: demonstrates that open-source supply chains are vulnerable to years-long social engineering of maintainers — not just code injection. Attribution: likely nation-state (based on sophistication and targeting scope).

---

### Q11

**USB Pratirodh and AppSamvid are specifically mentioned in the syllabus as tools for system security. What are they and which Indian government organization developed them?**

- A) USB Pratirodh is a hardware firewall device; AppSamvid is a network monitoring platform — both developed by IIT Bombay
- B) USB Pratirodh is an antivirus scanner; AppSamvid is a backup solution — both developed by NASSCOM
- C) USB Pratirodh monitors USB network traffic; AppSamvid monitors application network traffic — both developed by CERT-In
- D) ✅ USB Pratirodh controls and restricts USB device access on computers (preventing unauthorized USB data exfiltration and malware introduction); AppSamvid is an application whitelisting solution (only approved applications can execute); both were developed by CDAC (Centre for Development of Advanced Computing) under the NCIIPC (National Critical Information Infrastructure Protection Centre) initiative

**Explanation:**

- **A** is incorrect — USB Pratirodh is not a hardware firewall — it is a software-based USB device control tool. AppSamvid is not a network monitoring platform — it is an application execution control (whitelisting) tool. IIT Bombay was not the developing organization.
- **B** is incorrect — USB Pratirodh does not perform antivirus scanning — it controls which USB devices are permitted to connect. AppSamvid is not a backup solution — it is application whitelisting. NASSCOM is an industry association — not a government technology development organization producing security tools.
- **C** is incorrect — USB Pratirodh controls device ACCESS (which physical USB devices can connect) — it does not monitor network traffic. AppSamvid controls APPLICATION EXECUTION — not network traffic. CERT-In is India's national incident response team — while it certifies and recommends tools, it is not the developer of these specific tools.
- **D** ✅ is correct — **USB Pratirodh**: **(1)** Developed by CDAC under NCIIPC direction. **(2)** Controls which USB storage devices can be connected to government/critical infrastructure computers. **(3)** Prevents: autorun malware introduction via USB, unauthorized data exfiltration via USB drives. **(4)** Features: device whitelisting by serial number/vendor, encryption enforcement, audit logging. **AppSamvid**: **(1)** Also developed by CDAC under NCIIPC. **(2)** Application whitelisting — only pre-approved, registered applications can execute. **(3)** Prevents: execution of unauthorized software, zero-day malware, fileless attacks that use approved interpreters are harder but not impossible to block. **(4)** Particularly effective against: drive-by downloads, phishing payload execution, removable media malware. Both are part of India's indigenously developed cybersecurity toolkit for critical infrastructure protection.

---

## Questions 12–16 — Static Analysis

---

### Q12

**A malware analyst receives a suspicious executable and begins static analysis. The FIRST step is to compute a cryptographic hash of the file. What is the specific purpose of hashing at this stage — and which hash algorithm is the current standard for malware identification?**

- A) Hashing decrypts the malware — encrypted malware must be hashed before it can be analyzed
- B) Hashing compresses the malware file for efficient storage in the malware sample database
- C) Hashing verifies the analyst's copy is unmodified compared to what the victim reported — file integrity only
- D) ✅ Hashing generates a unique file fingerprint (SHA-256 is the current standard) — used to: (1) search VirusTotal and threat intelligence platforms for known malware identification, (2) create an IOC for sharing with other defenders, (3) establish a reference hash before analysis begins for evidence integrity, and (4) quickly identify if the same sample appears in other incidents

**Explanation:**

- **A** is incorrect — hashing does not decrypt anything. Cryptographic hash functions are one-way — they cannot be reversed. If malware is encrypted/packed, the hash is of the PACKED binary — analyzing packed malware requires unpacking first (a separate static or dynamic analysis step). Hashing has no relationship to encryption/decryption of the malware content.
- **B** is incorrect — hash functions produce a fixed-size digest (SHA-256 = 256 bits = 32 bytes) regardless of input size. A 5MB malware binary produces a 32-byte hash — this is not compression of the file itself. The hash is a fingerprint — not a compressed representation of the content.
- **C** is incorrect — while evidence integrity is ONE use of hashing in forensic contexts (establishing chain of custody), it is not the PRIMARY purpose in malware analysis. The more operationally important uses are identification (VirusTotal lookup), IOC generation, and cross-incident correlation — which this option omits entirely.
- **D** ✅ is correct — malware hash analysis workflow: **(1) VirusTotal lookup**: submit SHA-256 hash to VirusTotal → 70+ AV engines report whether this exact binary is known malware. Known malware → immediate identification, known family, previous reports. Unknown hash → potential zero-day or novel sample → requires deeper analysis. **(2) Threat intelligence**: hash lookups in MISP, OpenCTI, IBM X-Force, AlienVault OTX — find associated C2 IPs, campaign names, TTPs. **(3) IOC sharing**: SHA-256 hash is the primary IOC for sharing with other SOCs and security teams — "block this hash" — precise, unambiguous identification. **(4) Evidence integrity**: recording the hash at evidence acquisition ensures the sample analyzed is identical to what was found on the victim machine — critical for legal proceedings. **SHA-256** is the current standard — MD5 and SHA-1 are still used for compatibility but have collision vulnerabilities making them unsuitable for security-critical hash identification.

---

### Q13

**An analyst runs the `strings` command on a malware binary and finds the following output among others:**

    C:\Windows\System32\cmd.exe
    /c powershell -enc
    SOFTWARE\Microsoft\Windows\CurrentVersion\Run
    api.github.com
    Mozilla/5.0

**What does each string artifact suggest about the malware's behavior during static analysis?**

- A) The strings are false positives — cmd.exe and PowerShell strings appear in all Windows executables and are not meaningful
- B) The strings reveal the malware's source code — strings output is equivalent to decompilation
- C) The strings suggest the malware was compiled on a Windows XP system based on the System32 path format
- D) ✅ cmd.exe + PowerShell -enc suggests command execution with encoded (obfuscated) commands; the registry Run key path indicates persistence mechanism; api.github.com indicates C2 or payload download potentially using GitHub for hosting; Mozilla/5.0 User-Agent suggests HTTP communication mimicking legitimate browser traffic

**Explanation:**

- **A** is incorrect — while cmd.exe and PowerShell may appear in some legitimate executables, the COMBINATION with `-enc` (encoded command flag), a persistence registry key path, and a specific C2 domain creates a meaningful behavioral picture. Context matters — analysts assess strings in combination, not isolation. The registry Run key path and encoded PowerShell flags are particularly significant.
- **B** is incorrect — strings output reveals LITERAL STRING CONSTANTS embedded in the binary (function names, URL strings, file paths, registry paths, error messages). It is NOT equivalent to decompilation — it shows text fragments without the logic connecting them. Decompilation (IDA Pro, Ghidra, Ghidra decompiler) reconstructs pseudocode from binary logic. Strings gives fragments; decompilation gives structure.
- **C** is incorrect — the `C:\Windows\System32\cmd.exe` path is the standard Windows path format across ALL modern Windows versions (XP through 11). It does not indicate the compilation environment. Compilation environment is typically identified from PE header details (linker version, compiler signatures identified by PEiD) — not from file path strings.
- **D** ✅ is correct — string-by-string analysis: **(1) `C:\Windows\System32\cmd.exe` + `/c powershell -enc`**: the malware invokes cmd.exe to run PowerShell with the `-enc` (EncodedCommand) flag — indicating obfuscated PowerShell execution. A common technique to hide PowerShell payload from basic string inspection. **(2) `SOFTWARE\Microsoft\Windows\CurrentVersion\Run`**: standard Windows autorun registry key — the malware achieves PERSISTENCE by adding itself to this key — executes on every Windows login. **(3) `api.github.com`**: malware using GitHub API as C2 channel or for payload delivery — leverages trusted domain reputation to bypass URL reputation filtering. **(4) `Mozilla/5.0`**: custom HTTP User-Agent header mimicking Firefox/Chrome — HTTP traffic to C2 appears to be legitimate browser traffic, defeating simple User-Agent-based network monitoring.

---

### Q14

**A malware sample identified as packed with UPX shows very few strings in the `strings` output and minimal imports in the PE header. An analyst uses PEiD and confirms "UPX 3.95" packing. What is the CORRECT analysis approach to examine the actual malware payload?**

- A) Submit the packed sample to VirusTotal — VirusTotal automatically unpacks and analyzes the inner payload
- B) Disassemble the packed binary directly with IDA Pro — packing does not affect disassembly accuracy
- C) The packed sample cannot be analyzed — packers permanently destroy the original binary
- D) ✅ Unpack the binary using `upx -d malware.exe` (UPX decompressor) to recover the original executable, then re-run strings and PE analysis on the unpacked binary — OR use dynamic analysis (run in sandbox) to let the packer stub decompress the payload in memory, then dump the unpacked executable from memory

**Explanation:**

- **A** is incorrect — while VirusTotal does run multiple AV engines that may detect packed malware, VirusTotal does not return an "unpacked binary" for download. It returns detection results (known/unknown). For analysis of the inner payload structure, the analyst must unpack locally. VirusTotal is a detection tool — not an unpacking/analysis platform (though some engines detect the inner payload after unpacking internally).
- **B** is incorrect — disassembling a packed binary directly produces meaningless output. The packed binary's code section contains compressed/encrypted data — not actual instructions. IDA Pro would disassemble the UPX STUB (the small decompressor) correctly, but the malware payload section would appear as unintelligible data until unpacked. Direct disassembly of the packed section is not productive.
- **C** is incorrect — packers do NOT permanently destroy the original binary. Packing is a reversible transformation — the packer's stub decompresses the original binary in memory at runtime. The original binary is preserved (compressed/encrypted) within the packed file. Unpacking recovers the original. This is precisely how packers work — and why anti-packing tools and memory dumping techniques exist.
- **D** ✅ is correct — two valid approaches for UPX-packed malware: **(1) Static unpacking**: `upx -d malware.exe` — UPX has a built-in decompressor. Run this command → the packed binary is replaced with the original uncompressed executable. Re-run `strings`, PE header analysis, import table analysis on the recovered binary. **(2) Dynamic unpacking** (when packer is custom or unknown): run the malware in a controlled sandbox — at runtime, the packer stub decompresses the payload into memory. Use a debugger (x64dbg, OllyDbg) to set a breakpoint at the unpacking stub's final `JMP` instruction (the "OEP" — Original Entry Point) → the original code is now in memory → dump the memory to disk using a tool like Process Hacker or OllyDump → analyze the dumped unpacked binary. Dynamic unpacking is required when the packer is custom (PEiD shows "unknown packer") and no static unpacking tool exists.

---

### Q15

**Ghidra was released by the NSA in 2019 as an open-source alternative to IDA Pro. What specific capability does a disassembler/decompiler like Ghidra provide in malware analysis that strings analysis and PE header examination CANNOT provide?**

- A) Ghidra automatically removes all obfuscation and packing — producing clean, readable source code instantly
- B) Ghidra connects to the internet to cross-reference the binary against a global malware database
- C) Ghidra executes the malware in a sandboxed environment — it is a dynamic analysis tool
- D) ✅ Ghidra disassembles binary machine code into assembly language and decompiles it into pseudocode — revealing the LOGIC and CONTROL FLOW of the malware: conditional branches (if/else), loop structures, function calls, cryptographic algorithm identification, and the actual sequence of operations — which strings and headers cannot show

**Explanation:**

- **A** is incorrect — Ghidra does not automatically "clean" obfuscated or packed code. If the binary is packed, Ghidra disassembles the PACKER STUB — not the packed payload (same limitation as any disassembler on packed code). Obfuscated code is disassembled as-is — the analyst must manually trace obfuscation logic. Ghidra's decompiler produces pseudocode approximations — not original source code.
- **B** is incorrect — Ghidra is a local, offline analysis tool (by default). It does not connect to internet databases. While Ghidra can be extended with plugins (some of which might query external services), the core tool performs LOCAL analysis of the provided binary. Cross-referencing with external databases is done through separate tools (VirusTotal, MISP) — not by Ghidra itself.
- **C** is incorrect — Ghidra is a STATIC analysis tool. It does not execute code. It analyzes binary files without running them. Dynamic analysis (execution in sandbox) is performed by separate tools (Cuckoo, Any.Run, debuggers). Ghidra cannot observe runtime behavior because it never runs the malware.
- **D** ✅ is correct — **disassembly/decompilation vs strings/headers**: Strings analysis: reveals WHAT data the malware contains (URLs, file paths, registry keys, error messages). PE header analysis: reveals STRUCTURE (imports — what functions it calls, sections, compilation metadata). **Ghidra decompilation**: reveals HOW the malware works — the logic: **(1)** Conditional execution: "if registry key X exists, skip anti-sandbox checks" — string analysis cannot show this logic. **(2)** Encryption algorithm: identify AES, XOR, or custom cipher by examining the decompiled cryptographic loops. **(3)** C2 protocol: how C2 communication is structured, encrypted, how commands are parsed. **(4)** Persistence mechanism: exactly HOW and WHERE the registry key is written. **(5)** Anti-analysis techniques: identify IsDebuggerPresent() calls, CPUID checks — with source-like pseudocode context. Ghidra transforms an opaque binary into something approaching readable code — enabling deep behavioral understanding without execution.

---

### Q16

**During PE (Portable Executable) header analysis of a malware sample, an analyst notes that the Import Address Table (IAT) contains only THREE imports: `LoadLibrary`, `GetProcAddress`, and `VirtualAlloc`. What does this minimal import table strongly indicate?**

- A) The malware is a very small utility — simple tools only need three API calls
- B) The malware is a legitimate Windows system file — system files use minimal imports for performance
- C) The malware was compiled with an old compiler that only supports three Windows API calls
- D) ✅ A minimal IAT with only LoadLibrary, GetProcAddress, and VirtualAlloc strongly indicates a PACKED or ENCRYPTED executable — these three functions are the minimum required by a packer stub to: allocate memory (VirtualAlloc), load additional libraries (LoadLibrary), and resolve function addresses at runtime (GetProcAddress) — the actual malware's full import table is hidden inside the packed payload

**Explanation:**

- **A** is incorrect — simple utility programs (even ping.exe, notepad.exe) have dozens or hundreds of imports. A FUNCTIONAL malware that does anything meaningful — network communication, file operations, registry access, process manipulation — requires many API calls. Three imports is anomalously minimal — not an indicator of simplicity.
- **B** is incorrect — legitimate Windows system files (svchost.exe, explorer.exe, ntoskrnl.exe) have extensive import tables with many functions. "Minimal imports for performance" is not a real design principle in Windows development. Core Windows binaries have large import tables because they use many Windows subsystem functions.
- **C** is incorrect — no modern or legacy compiler generates code that "only supports three API calls." The number of imports is determined by what the code DOES — not by compiler capabilities. All compilers targeting Windows support the full Windows API. The minimal import count is about what the visible layer of the binary REVEALS — not compiler limitations.
- **D** ✅ is correct — the **minimal IAT packer signature**: **(1)** `VirtualAlloc`: allocates a new memory region — where the packer will decompress/decrypt the packed malware payload. **(2)** `LoadLibrary`: dynamically loads DLLs that the actual malware needs — circumventing the static import table which would otherwise reveal capabilities. **(3)** `GetProcAddress`: dynamically resolves function addresses from loaded DLLs — allows the actual malware to call any Windows API function without those calls appearing in the static IAT. **Implication**: the real malware functionality — network stack (WinSock), registry access (RegOpenKey), process injection (CreateRemoteThread) — is hidden. An analyst looking at this IAT sees only three harmless-looking functions — the actual capabilities are invisible until unpacking. This is the primary reason packers are used for AV evasion: they transform a detectable malware with obvious imports into an innocuous-looking binary with minimal imports.

---

## Questions 17–22 — Dynamic Analysis & Sandboxing

---

### Q17

**A malware analyst sets up dynamic analysis in a VM. Before executing the malware, they use Regshot to take a "first shot" of the registry. After executing the malware for 60 seconds, they take a "second shot" and click "Compare." The comparison shows a new value added to:**

    HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon
    Key: Userinit
    Value: C:\Windows\system32\userinit.exe, C:\malware\svchost32.exe

**What does this finding reveal about the malware's behavior?**

- A) The malware installed a new Windows login screen — Winlogon changes affect the visual appearance of the login UI
- B) The malware corrupted the Windows user initialization process — Winlogon changes indicate a destructive wiper
- C) The malware modified a screensaver setting — Winlogon controls screen locking behavior
- D) ✅ The malware established PERSISTENCE via the Winlogon Userinit registry key — this key specifies programs executed at user login — adding the malware path here ensures it executes every time any user logs in to the system alongside the legitimate userinit.exe

**Explanation:**

- **A** is incorrect — Winlogon registry changes do not affect the visual appearance of the login screen. Winlogon DOES manage the login process, but the `Userinit` key specifically controls what processes are launched after successful authentication — not the visual UI rendering.
- **B** is incorrect — adding a path to Userinit is NOT destructive — it is additive persistence. The legitimate `userinit.exe` is preserved (still listed, comma-separated) alongside the malware path. This is a STEALTH persistence technique — the system continues to function normally while the malware launches silently at every login.
- **C** is incorrect — screensaver settings are controlled by different registry keys under `HKCU\Control Panel\Desktop` (ScreenSaverActive, SCRNSAVE.EXE, ScreenSaveTimeout). The Winlogon key is not related to screen locking or screensaver behavior.
- **D** ✅ is correct — **Winlogon Userinit persistence**: The `HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Userinit` registry value specifies programs that Windows runs IMMEDIATELY after a user successfully authenticates. The original value is `C:\Windows\system32\userinit.exe,`. The malware appended `, C:\malware\svchost32.exe` — both programs now execute at login. The malware chose a deceptive name (`svchost32.exe` mimicking legitimate `svchost.exe`). **Impact**: every time ANY user logs into this machine, the malware automatically executes — persistent access even after reboot. **Regshot value**: this finding would appear in the Regshot comparison as a MODIFIED key value — the original value changed to include the malware path. This is MITRE ATT&CK T1547.004 — Boot or Logon Autostart Execution: Winlogon Helper DLL.

---

### Q18

**Process Monitor (ProcMon) is running during dynamic malware analysis. An analyst filters for `Operation is WriteFile` and `Path contains System32`. They observe the malware writing a file named `svch0st.exe` (zero instead of letter O) to `C:\Windows\System32\`. What TWO behavioral conclusions can be drawn from this single observation?**

- A) The malware is a legitimate Windows update — System32 file writes are always authorized system processes
- B) The malware is a wiper — writing to System32 always indicates destructive intent
- C) ✅ (1) The malware is attempting to MASQUERADE as a legitimate Windows process (typosquatting on svchost.exe) to avoid detection; (2) it is dropping a SECOND-STAGE component to disk — indicating a multi-stage infection where this dropped binary will be executed separately for persistence or additional capability
- D) The malware is performing backup operations — System32 writes indicate the malware is protecting Windows files

**Explanation:**

- **A** is incorrect — Process Monitor identifies the PROCESS making the write. If the writing process is a suspicious executable (not a legitimate Windows Update service with proper digital signatures), this is not a legitimate update operation. Legitimate Windows updates write to System32 through authorized Windows Update processes with digital signatures — not arbitrary processes being analyzed for malware behavior.
- **B** is incorrect — writing a FILE to System32 is not inherently destructive. Wipers overwrite existing files with zeros or corrupt partition structures — they destroy data. Writing a NEW file (like a dropped second-stage payload) to System32 is a persistence/installation technique — not data destruction.
- **C** ✅ is correct — two distinct behavioral conclusions: **(1) Masquerading (MITRE T1036)**: `svch0st.exe` with a zero (0) instead of the letter "o" is a typosquatting technique — the filename looks almost identical to the legitimate `svchost.exe` when viewed quickly. Located in System32 — a trusted directory. This is designed to blend in with legitimate system processes in task manager listings and security tool reports. **(2) Dropper/multi-stage behavior**: the malware writing an executable to disk indicates it is a DROPPER — its current execution is dropping a SECOND-STAGE payload. The dropped `svch0st.exe` will likely be executed separately (via registry persistence, service creation, or direct execution) — providing the actual malicious capabilities while the initial dropper may delete itself. Process Monitor revealing this write is crucial for identifying the complete infection chain — not just the initial sample.
- **D** is incorrect — malware writing a suspicious executable to System32 is not performing backup operations. Backup software writes backup archives to designated backup locations — not executable files to System32 with typosquatted names.

---

### Q19

**Wireshark is capturing network traffic during dynamic malware analysis in a sandbox. The analyst observes the malware making DNS queries for the following domains:**

    a3f9b2c1kx8p.evil.com
    7d2e5f1m9q4r.evil.com
    x8p3n6b2t7v1.evil.com

**Each domain name appears to be randomly generated 12-character strings. What malware technique does this indicate and what is its purpose?**

- A) The malware is performing DNS zone transfers — the random subdomains are attempting to enumerate the evil.com zone
- B) The malware is DNS tunneling — the random subdomains encode stolen data being exfiltrated via DNS queries
- C) The malware is performing a DNS amplification DDoS attack — random subdomains increase DNS response size
- D) ✅ This is a Domain Generation Algorithm (DGA) — the malware generates pseudo-random C2 domain names using an algorithm seeded with a date or other value — the attacker pre-registers only ONE of the daily generated domains — this defeats static C2 domain blacklisting since the list of future domains is computationally unpredictable without the algorithm

**Explanation:**

- **A** is incorrect — DNS zone transfers use the AXFR record type and target a specific nameserver for a domain. The pattern shown — multiple random subdomain queries to the same parent domain — is not zone transfer behavior. Zone transfers attempt to download the entire DNS zone database from a nameserver — not generate random subdomains.
- **B** is incorrect — while DNS tunneling DOES use subdomains to encode data, the PATTERN matters. DNS tunneling for data exfiltration generates subdomains containing encoded data (typically Base64 or Base32 fragments of the stolen data). The domains would encode data in a structured way. DGA-generated domains look random — they are not encoding any specific data content — they are navigation (C2 beacon attempts), not data exfiltration. The two techniques can both produce random-looking subdomains but serve different purposes.
- **C** is incorrect — DNS amplification DDoS uses open resolvers to reflect large DNS responses toward a victim — the attacker spoofs the victim's IP. A malware sample making DNS queries from within a sandbox is not performing amplification DDoS — it is performing outbound queries to find its C2, not using a resolver as an amplification reflector against a third party.
- **D** ✅ is correct — **DGA (Domain Generation Algorithm)**: **(1)** The malware contains an algorithm that generates a list of domain names based on a seed (today's date, a hardcoded constant). **(2)** Every day (or week/month), the algorithm generates a new list of hundreds of domains. **(3)** The attacker registers ONLY ONE (or a few) of these algorithmically generated domains — their C2 server. **(4)** The malware queries all generated domains — when it gets a valid DNS response (the registered one), it connects to C2. **(5)** Defenders cannot blacklist C2 domains in advance — without the algorithm, the list of future domains is unknown. **(6)** If defenders take down today's C2 domain, the malware switches to tomorrow's generated domain. **Countermeasure**: reverse engineer the DGA algorithm from malware code → precompute the entire domain list → proactively register or sinkhole all generated domains. Tools: DGArchive, DGA detection in network monitoring (high-entropy subdomains, NX domain response pattern).

---

### Q20

**Volatility is used for memory forensics during malware analysis. An analyst dumps the memory of a compromised Windows system and runs:**

    volatility -f memory.dmp --profile=Win10x64 pslist
    volatility -f memory.dmp --profile=Win10x64 psscan

**The `pslist` output shows 42 processes. The `psscan` output shows 43 processes — with one PID present in psscan but absent from pslist. What does this discrepancy indicate?**

- A) psscan found a zombie process that crashed — crashed processes appear in psscan but not pslist
- B) pslist missed a process due to a Volatility version incompatibility — update Volatility to fix the discrepancy
- C) The extra process in psscan is a system idle process — idle processes are excluded from pslist by design
- D) ✅ A process hidden by a DKOM (Direct Kernel Object Manipulation) rootkit — pslist walks the kernel's doubly-linked EPROCESS list (which the rootkit unlinked the process from) while psscan scans raw memory for EPROCESS structures — the discrepancy reveals a process the rootkit made invisible to OS-level queries

**Explanation:**

- **A** is incorrect — crashed/zombie processes in Windows have specific cleanup procedures — they do not typically persist as invisible processes. A crashed process that completed termination would not appear in psscan as a running EPROCESS structure. Volatility's psscan detects ACTIVE process structures in memory — not crash artifacts.
- **B** is incorrect — while Volatility version and profile compatibility matters, a systematic one-process discrepancy between pslist and psscan is a well-known forensic indicator of rootkit activity — not a tool bug. If it were a tool incompatibility, the discrepancy would typically affect many processes or produce errors — not precisely one hidden process.
- **C** is incorrect — the System Idle Process (PID 0) is a special process representing idle CPU cycles. It IS listed in pslist and psscan — it does not cause one-count discrepancies. There is no "idle process exclusion" in pslist by design.
- **D** ✅ is correct — **DKOM rootkit detection via cross-view analysis**: **(1) `pslist`**: Volatility enumerates processes by traversing the `PsActiveProcessHead` doubly-linked list of EPROCESS structures in the kernel. A DKOM rootkit unlinks its process from this list — the process is invisible to any tool using this standard OS data structure (Task Manager, Process Explorer, ps commands). **(2) `psscan`**: Volatility scans the ENTIRE physical memory for EPROCESS structure signatures — regardless of list linkage. A process unlinked from the active process list still has its EPROCESS structure in memory (the process is still running) — psscan finds it by pattern matching. **(3) Discrepancy = rootkit indicator**: one process in psscan not in pslist = that process's EPROCESS was deliberately unlinked from the active process list by a rootkit while the process continued running. The analyst can then examine the hidden process: its executable path, loaded DLLs, network connections, parent process, and memory regions — extracting IOCs despite the rootkit's attempt at concealment.

---

### Q21

**Cuckoo Sandbox is the most widely deployed open-source automated malware analysis platform. Which of the following CORRECTLY describes what Cuckoo collects during a malware analysis run — and how this differs from running the malware in a standard VM without Cuckoo?**

- A) Cuckoo collects only network traffic — it is a network-focused tool equivalent to running Wireshark alone
- B) Cuckoo only analyzes files statically — it does not execute malware and does not observe runtime behavior
- C) Cuckoo and a standard VM provide identical visibility — the difference is only in report formatting
- D) ✅ Cuckoo instruments the analysis VM with monitoring agents that automatically collect: all API calls made by the malware (hooking Windows APIs), file system changes, registry modifications, network traffic (PCAP), screenshots, memory dumps, and behavioral signatures — compiled into a structured JSON/HTML report — far exceeding manual VM observation

**Explanation:**

- **A** is incorrect — Cuckoo's network traffic capture (via tcpdump/PCAP) is ONE component of a comprehensive collection framework. Cuckoo also captures API calls, file operations, registry changes, process activity, memory content, and screenshots — network traffic alone is a fraction of what Cuckoo collects.
- **B** is incorrect — Cuckoo is fundamentally a DYNAMIC analysis platform. Its primary function is EXECUTING malware in an isolated VM and observing its behavior. Static analysis plugins exist in Cuckoo (PE analysis, VirusTotal hash lookup) as supplementary features — but execution and behavioral monitoring are Cuckoo's core capability.
- **C** is incorrect — a standard VM provides NO automatic instrumentation. A human analyst must manually run Process Monitor, Wireshark, Regshot — each separately — observe manually, take manual notes, and compile findings manually. Cuckoo's monitoring agent inside the VM automatically instruments all Windows API calls, automatically captures all activity simultaneously, automatically generates structured reports — providing far deeper and more comprehensive visibility than manual VM analysis.
- **D** ✅ is correct — **Cuckoo's instrumented analysis**: **(1) API monitoring**: Cuckoo hooks Windows API functions (using a monitoring DLL injected into the malware process) — records EVERY API call with parameters and return values. CreateFile, RegSetValue, socket, VirtualAlloc, CreateProcess — all captured with arguments. **(2) File system**: all files created, modified, deleted — with content samples. **(3) Registry**: all keys read, written, deleted. **(4) Network**: full PCAP of all network traffic — DNS queries, HTTP requests, raw TCP/UDP connections. **(5) Screenshots**: periodic screenshots showing malware UI elements or error dialogs. **(6) Memory dump**: process memory snapshots for offline analysis. **(7) Behavioral signatures**: comparison against known malware behavior patterns — classifies behavior as botnet, ransomware, infostealer, etc. **(8) Structured output**: JSON/HTML report with all findings organized for human review and automated processing.

---

### Q22

**An analyst submits a malware sample to Any.Run (interactive cloud sandbox) instead of Cuckoo. What specific capability does Any.Run provide that Cuckoo (automated) does not — and which category of malware particularly requires this capability?**

- A) Any.Run analyzes Linux malware; Cuckoo only analyzes Windows malware — platform support is the difference
- B) Any.Run is faster — the difference is processing speed, not capability
- C) Any.Run provides better network signatures — Cuckoo cannot identify C2 protocols
- D) ✅ Any.Run provides INTERACTIVE analysis — the analyst can click buttons, enter text, close dialog boxes, and interact with the running malware in real time — this is essential for malware that requires user interaction before executing its payload (e.g., macros requiring "Enable Content" click, installers requiring "Next" button, decoy documents requiring user actions)

**Explanation:**

- **A** is incorrect — both Any.Run and Cuckoo primarily support Windows malware analysis (with Linux support also available in both platforms). The platform support difference is not the distinguishing capability between interactive and automated analysis.
- **B** is incorrect — processing speed is not the meaningful capability difference. Both platforms analyze malware within similar timeframes. The interaction model (automated vs interactive) is the fundamental difference — not speed.
- **C** is incorrect — network signature identification is a capability both platforms provide through network traffic analysis. Cuckoo's network analysis (via integrated IDS signatures — Suricata integration) can identify C2 protocols, malware families from network behavior, and protocol anomalies. Any.Run also provides network analysis. Network signatures are not the differentiating capability.
- **D** ✅ is correct — **interactive vs automated analysis**: **Cuckoo (automated)**: submits malware → VM executes it automatically → monitors for defined timeout period → generates report. No human interaction possible. **Limitation**: malware that requires user interaction (clicking "Enable Macros", responding to UAC prompts, entering a password to decrypt an archive, clicking through an installer) will NOT execute its payload in automated mode — Cuckoo reports "no significant behavior" when the malware is waiting for human input. **Any.Run (interactive)**: analyst views the running VM in a browser → can click buttons, type text, dismiss dialogs, interact with the running system in real time. **Particularly needed for**: **(1)** Office macro malware requiring "Enable Content" click. **(2)** Decoy document attacks requiring the user to "open the attachment to view". **(3)** Installers with multi-step wizards. **(4)** Malware with decoy UI that requires interaction before the malicious payload activates. **(5)** User-interaction checks (anti-sandbox technique) — Any.Run defeats this by providing real user interaction.

---

## Questions 23–26 — Anti-Analysis Techniques

---

### Q23

**A malware sample behaves completely benignly in Cuckoo Sandbox — no malicious network activity, no file drops, no registry modifications. The same sample on a real victim machine causes full system compromise. The analyst suspects an anti-sandbox technique. Which of the following anti-sandbox mechanisms is MOST likely responsible — and what is the technical indicator that would confirm it?**

- A) The malware uses AES encryption — Cuckoo cannot decrypt AES-encrypted payloads
- B) The malware only targets Windows XP — modern sandbox VMs run Windows 10 preventing execution
- C) The malware requires a GPU for rendering — Cuckoo VMs lack GPUs causing execution failure
- D) ✅ The malware uses a TIME-DELAY anti-sandbox technique — it calls Sleep() for 10+ minutes before executing its payload — Cuckoo's default analysis window (2–5 minutes) expires before the payload activates — confirmed by checking the malware's import table for Sleep/WaitForSingleObject calls and examining Cuckoo's process API log for long sleep durations

**Explanation:**

- **A** is incorrect — AES encryption protects the PAYLOAD during transmission or storage. If the malware is executing on the system, its own decryption routine runs — the malware decrypts its payload in memory and executes it. Cuckoo's API monitoring would capture the decryption calls (CryptDecrypt, custom XOR loop) AND the subsequent malicious behavior after decryption. Encryption of the payload does not prevent observation of the decrypted behavior.
- **B** is incorrect — malware targeting only Windows XP in 2025–2026 would be effectively useless as an attack tool — XP has negligible market share. Modern malware targets current Windows versions. Cuckoo supports multiple Windows profiles (Win7, Win10, Win11) — analysts select appropriate profiles. OS version incompatibility would typically cause an error/crash — not silent benign behavior.
- **C** is incorrect — while GPU detection IS used by some sophisticated malware to detect virtual environments (most VMs lack physical GPUs — they have virtual display adapters), this is a less common anti-sandbox technique than timing-based evasion. GPU absence typically causes different behavior (visual rendering difference) rather than complete behavioral silence across all activity categories.
- **D** ✅ is correct — **timing-based anti-sandbox** is one of the most common and effective anti-analysis techniques: **(1)** Malware calls `Sleep(600000)` (10 minutes in milliseconds) or `WaitForSingleObject(hEvent, 600000)` immediately on execution. **(2)** Cuckoo's default analysis window: 120–300 seconds (2–5 minutes). **(3)** The malware sleeps 10 minutes → Cuckoo timeout fires → analysis ends → "no malicious behavior detected." **(4)** On a real victim machine: the user's computer runs continuously → after 10 minutes, sleep ends → payload executes. **Confirmation indicators**: **(1)** PE import table contains `Sleep`, `WaitForSingleObject`, `NtDelayExecution`. **(2)** Cuckoo API log shows a very long `Sleep()` call near the beginning of execution. **(3)** Extend Cuckoo analysis timeout to 15–20 minutes → behavior appears. **(4)** Advanced countermeasure: accelerate VM clock (NtSetSystemTime) or patch the Sleep calls in memory before execution.

---

### Q24

**A malware sample checks the following at startup:**

    1. Registry key: HKLM\SOFTWARE\VMware, Inc.\VMware Tools
    2. Running process list for: vmtoolsd.exe, vboxservice.exe, wireshark.exe, procmon.exe
    3. MAC address prefix: 00:0C:29 (VMware) or 08:00:27 (VirtualBox)
    4. CPUID instruction — checks hypervisor present bit

**If ANY check returns a positive result, the malware exits without executing its payload. What category of anti-analysis technique is this — and what are TWO specific countermeasures analysts use?**

- A) Anti-debugging — the malware detects debugger attachment; countermeasures are disabling breakpoints and running as administrator
- B) Code obfuscation — the malware hides its check logic; countermeasures are deobfuscation and decompilation
- C) Timing evasion — the malware delays execution; countermeasures are extending sandbox timeout and patching sleep calls
- D) ✅ Anti-VM / Anti-sandbox detection — countermeasures are (1) configuring the analysis VM to remove VMware artifacts (change MAC address, rename processes, delete VMware registry keys, use bare-metal analysis) and (2) patching the malware binary in memory to NOP out the detection checks so it continues execution regardless of environment detection results

**Explanation:**

- **A** is incorrect — anti-debugging detects a DEBUGGER process attached to the malware process (using IsDebuggerPresent(), NtQueryInformationProcess, etc.). The checks described (VMware registry keys, specific process names, MAC address prefixes, CPUID hypervisor bit) are specifically VM/sandbox detection — not debugger detection. The countermeasures for anti-debugging (disabling breakpoints) are irrelevant here.
- **B** is incorrect — code obfuscation hides the malware's code structure from static analysis. The described technique actively RUNS checks against the live environment — this is runtime environment detection, not code structure hiding. Deobfuscation is a static analysis countermeasure — not a response to runtime VM detection.
- **C** is incorrect — timing evasion uses Sleep() to outlast sandbox timeouts. The described technique uses IMMEDIATE checks and exits immediately if a VM is detected — there is no time delay involved. Extending sandbox timeout would not help if the malware exits in the first second upon detecting VMware registry keys.
- **D** ✅ is correct — **anti-VM / anti-sandbox technique** using multiple detection vectors: **(1) Registry artifact check**: VMware Tools installation creates specific registry keys — malware checks their presence. **(2) Process list check**: known analysis tool processes (Wireshark, ProcMon) and VMware guest service processes (vmtoolsd.exe, vboxservice.exe) are visible in the process list. **(3) MAC address check**: VMware and VirtualBox assign network adapters with specific MAC OUI prefixes. **(4) CPUID hypervisor bit**: Intel/AMD CPUs set a specific CPUID bit when running under a hypervisor — detectable with a single instruction. **Countermeasures**: **(1) VM hardening**: remove VMware Tools (eliminates registry keys and vmtoolsd.exe), change MAC address to a non-VM OUI (`ip link set wlan0 address`), rename or hide analysis tool processes, use VirtualBox with "VBoxHardenedLoader" to hide hypervisor bit. Use bare-metal analysis for critical samples. **(2) Binary patching**: in a debugger (x64dbg, OllyDbg), locate the detection code, replace the conditional JMP instruction with NOP (no operation) — the detection check runs but its result is ignored — execution continues to the malicious payload regardless of what the check found. This is the most reliable approach when VM hardening is incomplete.

---

### Q25

**What is the AMSI (Antimalware Scan Interface) — and why do fileless malware and PowerShell-based attacks specifically target AMSI bypass as a FIRST STEP before executing their payload?**

- A) AMSI is a Windows firewall component — bypassing it allows malware to make outbound network connections
- B) AMSI is a file system filter driver — bypassing it allows malware to write files to protected directories
- C) AMSI is a Windows process isolation feature — bypassing it allows malware to inject into other processes
- D) ✅ AMSI is a Windows API interface that allows AV engines to scan SCRIPT CONTENT before execution — even obfuscated, Base64-encoded, or dynamically generated scripts — bypassing AMSI is the first step because otherwise the AV engine connected to AMSI would detect and block the malicious PowerShell/VBScript payload regardless of obfuscation

**Explanation:**

- **A** is incorrect — AMSI has no relationship to network firewall functionality. Network connections are governed by Windows Firewall (filtering service), WFP (Windows Filtering Platform), and application-layer restrictions. AMSI operates at the scripting engine level — before script content is executed.
- **B** is incorrect — AMSI does not function as a file system filter driver. File system access controls are handled by NTFS permissions, EFS, and kernel-level file filter drivers (used by AV for on-access scanning). AMSI specifically targets SCRIPT CONTENT submitted to Windows scripting engines — not file system operations.
- **C** is incorrect — process isolation and injection controls are governed by separate Windows mechanisms (Protected Processes, CFG — Control Flow Guard, Code Integrity policies). AMSI does not mediate process injection — it mediates script content evaluation. Process injection attacks bypass different security boundaries.
- **D** ✅ is correct — **AMSI architecture and bypass motivation**: **(1)** AMSI is a Windows 10+ interface allowing AV products to register as AMSI providers. **(2)** When PowerShell (or VBScript, JavaScript, WMI scripts) prepares to execute content, it submits the DECODED content to AMSI — AFTER de-obfuscation, AFTER Base64 decoding, AFTER string concatenation. **(3)** The AV engine receives the PLAINTEXT malicious script and detects it — even if the original script was heavily obfuscated. **(4)** WITHOUT AMSI bypass: a heavily obfuscated PowerShell reverse shell is decoded by PowerShell → submitted to AMSI → AV detects malicious content → execution blocked. **(5)** WITH AMSI bypass: attacker first runs a small AMSI bypass technique (patching amsi.dll in memory, corrupting the AMSI scan buffer, using reflection to disable the AMSI provider) → then runs the obfuscated payload → AMSI scan never fires → malicious content executes. Common AMSI bypasses: `[Ref].Assembly.GetType('System.Management.Automation.AmsiUtils').GetField('amsiInitFailed','NonPublic,Static').SetValue($null,$true)` — sets AMSI initialization failure flag, disabling all subsequent scans.

---

### Q26

**During malware analysis, an analyst discovers that the malware checks the screen resolution of the system before executing its payload — specifically, it exits if the screen resolution is 800×600 or 1024×768. What specific anti-analysis technique does this represent and why are these specific resolutions targeted?**

- A) The malware requires high resolution for its GUI — low resolution causes rendering failures
- B) The malware targets gaming systems — 800×600 is used by games and the malware waits for gaming sessions
- C) The malware is checking monitor age — older monitors use lower resolutions and the malware avoids legacy hardware
- D) ✅ This is an anti-sandbox technique — automated sandbox VMs commonly run at 800×600 or 1024×768 (low default display resolutions for performance/compatibility) while real user workstations almost universally run at 1920×1080 or higher — the malware detects sandbox environments by checking for these characteristic low resolutions

**Explanation:**

- **A** is incorrect — malware designed for credential theft, persistence, or remote access does not require any GUI at all — it operates silently in the background. A resolution check that TERMINATES the malware if resolution is below threshold is specifically designed to DETECT analysis environments — not to ensure rendering quality. If rendering were the concern, the malware would simply fail to render UI elements — not exit its entire execution.
- **B** is incorrect — 800×600 is not specifically associated with gaming. Gaming systems typically use high resolutions (1080p, 1440p, 4K). The correlation between 800×600/1024×768 and sandbox VMs is well-documented in malware analysis literature — these resolutions are the historical defaults for VMware, VirtualBox, and automated analysis platforms.
- **C** is incorrect — monitor age detection is not a meaningful anti-analysis signal. Modern sandboxes running virtualized Windows 10 with default video settings would present as "newer" systems in all other respects. The resolution check specifically targets the characteristic low resolutions of AUTOMATED SANDBOX configurations — not hardware vintage.
- **D** ✅ is correct — **screen resolution anti-sandbox logic**: **(1)** Automated malware analysis sandboxes (Cuckoo, cloud-based sandboxes) historically run with minimal virtual display adapters configured at 800×600 or 1024×768 — these resolutions require minimal GPU resources for the virtual machine. **(2)** Real user workstations in 2024: essentially 100% run at 1920×1080 (Full HD) or higher. A system running at 800×600 is almost certainly a VM or legacy test environment. **(3)** Resolution check: `GetSystemMetrics(SM_CXSCREEN)` returns 800 → `exit(0)`. **(4)** Countermeasure**: configure sandbox VMs to 1920×1080 resolution. In VMware: VM Settings → Display → specify 1920×1080. This is a simple sandbox hardening step that defeats many resolution-based detection techniques. More sophisticated malware also checks number of monitors (sandboxes typically have one virtual monitor), mouse cursor position changes over time (automated sandboxes have no mouse movement), and click counts (no user clicking in automated analysis).

---

## Questions 27–28 — Extra Notes & Real-World

---

### Q27

**A malware analyst completes analysis of a ransomware sample and prepares an IOC (Indicator of Compromise) report for sharing with other organizations. Which combination of artifacts constitutes a COMPLETE and operationally useful IOC set for this ransomware?**

- A) Only the SHA-256 hash of the ransomware executable — hashes are the only reliable IOC type
- B) Only the ransom note filename — the note is the most visible artifact defenders can search for
- C) Only the C2 IP address — network blocking is the most effective defensive action
- D) ✅ Complete IOC set: SHA-256 hash (file identification), C2 domains/IPs (network blocking), mutex name (detect running instance), registry persistence key path and value (remediation), dropped file paths and names, YARA rule (detect variants), and behavioral signatures (process injection technique, encryption file extension pattern)

**Explanation:**

- **A** is incorrect — a hash alone is an incomplete IOC set. Hashes identify ONLY the exact binary — a slightly modified variant (even a single byte changed) has a different hash and evades hash-based detection. Modern malware families use polymorphism to generate unique binaries per infection — hashes are point-in-time identifiers, not family-level detectors. A complete IOC set includes multiple indicator types at different abstraction levels.
- **B** is incorrect — the ransom note filename alone is insufficient for complete detection and response. The ransom note IS a useful IOC but: (1) it only appears AFTER encryption is complete — too late to prevent damage, (2) trivially changed between variants, (3) provides no network detection capability, (4) provides no persistence remediation path. A single IOC type cannot support detection, containment, and remediation simultaneously.
- **C** is incorrect — C2 IPs alone are an incomplete IOC set. IP addresses change (attackers use bulletproof hosting, rotate infrastructure) — what was a valid C2 last week may be taken down and reassigned to legitimate users. Network blocking is valuable but a complete IOC set enables detection at multiple stages of the kill chain — before, during, and after network communication.
- **D** ✅ is correct — **complete multi-layer IOC set**: **(1) SHA-256 hash**: exact file identification — VirusTotal lookup, file system blocking. **(2) C2 domains/IPs**: network blocking at firewall/DNS level — prevent command communication. **(3) Mutex name**: malware often creates a named mutex to prevent double-infection — detecting the mutex in memory confirms active infection without needing the file hash. **(4) Registry persistence paths**: specific keys for remediation — removing persistence after detection. **(5) File paths/names**: locations where malware drops files — scan targets. **(6) YARA rule**: pattern-based detection that catches variants beyond exact hash matching — detects the malware FAMILY even when binary is slightly modified. **(7) Behavioral signatures**: process injection techniques, encryption patterns (extension changes like `.locked`, specific file header magic bytes destroyed) — enables behavior-based detection in EDR. IOC sharing formats: STIX/TAXII (automated sharing), MISP (threat intelligence platform), simple CSV for firewall imports.

---

### Q28

**YARA is described as a "pattern matching tool for malware researchers." A security analyst writes the following YARA rule:**

    rule Suspicious_PowerShell_Dropper {
        meta:
            description = "Detects PowerShell dropper with base64 encoded payload"
            author = "Analyst"
        strings:
            $ps1 = "powershell" nocase
            $enc1 = "-EncodedCommand" nocase
            $enc2 = "-enc" nocase
            $b64 = /[A-Za-z0-9+\/]{100,}={0,2}/ wide ascii
        condition:
            $ps1 and ($enc1 or $enc2) and $b64
    }

**What does this YARA rule detect and why is the `condition` structured with AND/OR logic rather than requiring all four strings?**

- A) This rule detects any file containing Base64 strings — the condition is an error and should require all four strings
- B) This rule only runs on Linux systems — the `wide ascii` modifier indicates Linux-specific encoding
- C) This rule detects files containing PowerShell strings only — the Base64 pattern is a comment and is ignored
- D) ✅ This rule detects files containing "powershell" AND EITHER "-EncodedCommand" OR "-enc" AND a Base64 string of 100+ characters — the OR logic covers both full and abbreviated forms of the encoding flag — this combination targets the specific technique of running obfuscated PowerShell payloads while avoiding false positives from files with only individual components

**Explanation:**

- **A** is incorrect — the condition `$ps1 and ($enc1 or $enc2) and $b64` requires ALL of: the PowerShell string AND an encoded command flag AND a Base64 string. A file with ONLY a Base64 string does NOT match — `$ps1` and `($enc1 or $enc2)` must also be present. The rule does NOT trigger on arbitrary Base64 content alone.
- **B** is incorrect — `wide ascii` is a YARA string modifier indicating the pattern should be searched as both ASCII (single-byte) and wide/Unicode (UTF-16LE, two bytes per character) encoding. It applies to Windows Unicode strings — not Linux. This makes the rule effective against PowerShell scripts that may store strings in Unicode format (common in Windows environments). YARA runs cross-platform.
- **C** is incorrect — all four strings (`$ps1`, `$enc1`, `$enc2`, `$b64`) are active pattern definitions — they are NOT comments. In YARA, comments use `//` or `/* */` syntax. The `$b64` string with the regex pattern `[A-Za-z0-9+\/]{100,}={0,2}` is a fully active YARA regex matching Base64 strings of 100+ characters with optional padding.
- **D** ✅ is correct — YARA rule analysis: **(1) `$ps1 = "powershell" nocase`**: matches "powershell" in any case (PowerShell, POWERSHELL, etc.) — identifies files referencing PowerShell. **(2) `$enc1 = "-EncodedCommand" nocase`** and **`$enc2 = "-enc" nocase`**: match both the full form and the common abbreviation of PowerShell's encoded command flag. Using OR (`$enc1 or $enc2`) ensures both variants are caught — attackers sometimes use `-enc` to avoid detection by rules matching the full form. **(3) `$b64 = /[A-Za-z0-9+\/]{100,}={0,2}/`**: YARA regex matching Base64-encoded strings of at least 100 characters (the `{100,}` quantifier) — short Base64 strings (like image data) are excluded; 100+ character Base64 is characteristic of encoded PowerShell payloads. **(4) Condition logic**: `$ps1 AND ($enc1 OR $enc2) AND $b64` — requires all three components present together: the PowerShell reference, the encoding flag (either form), and a substantial Base64 payload. This combination specifically targets the `powershell -enc BASE64PAYLOAD` technique used extensively in fileless malware droppers — while avoiding false positives from files that contain only individual components.

---

## Answer Key

| Q# | Answer | Topic Area |
|---|---|---|
| Q01 | D | Spyware/keylogger — silent data collection — no replication/encryption |
| Q02 | D | Logic bomb vs backdoor — trigger condition vs persistent access — shared dormancy |
| Q03 | D | Fileless malware — PowerShell LotL — AMSI primary defense |
| Q04 | D | Rootkit — kernel-level sys_call_table hooks — standard tools defeated |
| Q05 | D | Dropper — first-stage installer — multi-stage malware architecture |
| Q06 | D | Wiper malware — irreversible destruction — no ransom — sabotage motivation |
| Q07 | D | Double extortion — exfiltration before encryption — defeats backup strategy |
| Q08 | D | RaaS model — developer/affiliate split — attribution difficulty |
| Q09 | D | SolarWinds SUNBURST — build process compromise — trusted signed update |
| Q10 | D | XZ Utils CVE-2024-3094 — two-year maintainer social engineering |
| Q11 | D | USB Pratirodh + AppSamvid — CDAC/NCIIPC — Indian government security tools |
| Q12 | D | File hashing — SHA-256 standard — VirusTotal lookup — IOC generation |
| Q13 | D | Strings analysis — cmd.exe/PowerShell -enc, Run key, DGA C2, browser UA |
| Q14 | D | UPX unpacking — `upx -d` static OR dynamic memory dump |
| Q15 | D | Ghidra decompilation — logic and control flow — beyond strings/headers |
| Q16 | D | Minimal IAT — LoadLibrary/GetProcAddress/VirtualAlloc — packer signature |
| Q17 | D | Regshot — Winlogon Userinit persistence — registry modification detection |
| Q18 | C | ProcMon WriteFile — masquerading (typosquatting) + dropper second-stage |
| Q19 | D | DGA — pseudo-random C2 domains — defeats static blacklisting |
| Q20 | D | Volatility pslist vs psscan — DKOM rootkit — hidden process detection |
| Q21 | D | Cuckoo — comprehensive API/file/registry/network instrumentation |
| Q22 | D | Any.Run interactive — user interaction for macros/installers — vs automated Cuckoo |
| Q23 | D | Time-delay anti-sandbox — Sleep() beyond Cuckoo timeout |
| Q24 | D | Anti-VM detection — VMware registry/process/MAC/CPUID checks — VM hardening + NOP patching |
| Q25 | D | AMSI — script content scanning before execution — fileless bypass necessity |
| Q26 | D | Screen resolution anti-sandbox — 800×600/1024×768 VM default detection |
| Q27 | D | Complete IOC set — hash + C2 + mutex + registry + YARA + behavioral |
| Q28 | D | YARA rule analysis — PowerShell encoded command dropper detection logic |

---