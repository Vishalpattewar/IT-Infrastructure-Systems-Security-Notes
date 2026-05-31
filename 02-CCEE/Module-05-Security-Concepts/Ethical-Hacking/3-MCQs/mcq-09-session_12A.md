🔐 MCQ Set — Session 12A

Module: Security Concepts — Ethical Hacking
Coverage: Password Attack Classification · Password Cracking Countermeasures · Keyloggers · Spyware Technologies
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

Q1. What hashing algorithm does Windows use to compute the NT Hash?

A) MD5
B) SHA-1
C) MD4
D) bcrypt

---

Q2. Which Hashcat mode number is used to crack NT Hashes?

A) -m 5600
B) -m 1800
C) -m 3200
D) -m 1000

---

Q3. What is the MITRE ATT&CK technique ID specifically assigned to Keylogging?

A) T1040
B) T1056.001
C) T1113
D) T1055

---

Q4. Which password hashing function won the Password Hashing Competition (PHC) in 2015 and is considered the current best practice?

A) bcrypt
B) scrypt
C) Argon2
D) SHA-512

---

Q5. Which Windows Event ID is generated when a user account is locked out?

A) 4625
B) 4624
C) 4776
D) 4740

---

Q6. What does LAPS stand for in the context of Windows security?

A) Local Access Password System
B) Local Administrator Password Solution
C) Lightweight Admin Password Service
D) Local Authentication Protection Standard

---

Q7. Which OTP standard generates a time-based one-time password that rotates every 30 seconds?

A) HOTP
B) FIDO2
C) SMS OTP
D) TOTP

---

Q8. Which open-source tool released by Amnesty International is specifically used to detect Pegasus spyware indicators on mobile devices?

A) Cuckoo
B) MobSF
C) MVT
D) Wireshark

---

Q9. Which Windows Event ID records a failed logon attempt?

A) 4624
B) 4648
C) 4625
D) 4771

---

Q10. Which Windows API function do API-based software keyloggers commonly use to intercept keystrokes?

A) CreateRemoteThread()
B) VirtualAllocEx()
C) RegSetValueEx()
D) SetWindowsHookEx()

---

Q11. Which organisation developed the Pegasus spyware?

A) Citizen Lab
B) NSO Group
C) FinFisher Group
D) Hacking Team

---

Q12. What is rockyou.txt and what is its origin?

A) A Hashcat rule file used to mangle passwords
B) A Linux system configuration file from 2005
C) A wordlist derived from the 2009 RockYou breach containing 32 million plaintext passwords
D) A rainbow table precomputed for MD5 hashes

---

Q13. Why does account lockout NOT protect against offline password cracking attacks?

A) Because lockout only applies to standard user accounts, not admin accounts
B) Because the attacker works on a local copy of the stolen hash file — the target account is never contacted
C) Because offline cracking tools can automatically reset lockout counters remotely
D) Because Windows does not apply lockout policies to hash-based authentication

---

Q14. What is the fundamental difference between a brute force attack and a password spraying attack?

A) Brute force uses GPU acceleration; password spraying does not
B) Brute force is always offline; password spraying is always online
C) Brute force tries many passwords against one account; spraying tries one password against many accounts
D) Brute force uses a wordlist; password spraying generates passwords algorithmically

---

Q15. What makes bcrypt significantly more resistant to offline cracking compared to SHA-256?

A) bcrypt produces a longer hash output that is harder to store
B) bcrypt is memory-hard and physically cannot run on GPUs
C) bcrypt has a configurable cost factor making it intentionally slow — processing ~6–25 hashes per second versus billions per second for SHA-256
D) bcrypt automatically rotates the stored hash every 90 days

---

Q16. Why is a form-grabbing keylogger considered particularly dangerous?

A) It can activate the device microphone without user knowledge
B) It intercepts browser form data before HTTPS encryption is applied, bypassing TLS entirely
C) It installs itself as a kernel driver that survives OS reinstallation
D) It spreads automatically across the network like a worm

---

Q17. What is the primary security advantage of a hardware keylogger over a software keylogger?

A) Hardware keyloggers can intercept wireless network traffic simultaneously
B) Hardware keyloggers leave no software footprint and are completely invisible to antivirus tools
C) Hardware keyloggers can automatically exfiltrate captured data over the internet
D) Hardware keyloggers work across all operating systems without configuration

---

Q18. What specific attack does adding a user to the Windows Protected Users group primarily prevent?

A) SQL injection against domain-joined applications
B) DNS spoofing against the domain controller
C) Pass-the-Hash and credential caching attacks by disabling NTLM authentication
D) Kerberoasting attacks against service account SPNs

---

Q19. What is the primary purpose of adding a salt to a password before hashing it?

A) To increase the computational speed of the hashing process
B) To extend the length of the final stored hash value
C) To ensure two users with the same password produce different hash values, defeating rainbow table attacks
D) To encrypt the hash using a secret application-level key

---

Q20. Which category of password attack generates absolutely zero failed login attempts on the target authentication system?

A) Brute force attack
B) Password spraying attack
C) Credential stuffing attack
D) Offline cracking attack

---

Q21. The Uber security breach in 2022 involved an attacker obtaining valid employee credentials and then repeatedly sending push notifications until the employee approved one. What is this attack technique called?

A) SIM swapping
B) SS7 interception
C) MFA fatigue or push bombing
D) TOTP token cloning

---

Q22. What does a kernel-level software keylogger require that an API-based software keylogger typically does not?

A) An active internet connection to a C2 server
B) Physical access to install a hardware component
C) Administrator or root privileges to install a kernel-mode driver
D) The target user to be actively logged in during installation

---

Q23. According to NIST SP 800-63B, which traditional password practice is explicitly no longer recommended?

A) Enforcing a minimum password length
B) Allowing users to paste passwords into login fields
C) Checking submitted passwords against known breached password databases
D) Mandatory periodic password rotation unless a compromise is suspected

---

Q24. What is credential stuffing and what distinguishes it from a standard dictionary attack?

A) Credential stuffing targets hash files offline; dictionary attacks target live systems
B) Credential stuffing uses real leaked username and password pairs from previous breaches and replays them against other services
C) Credential stuffing generates passwords using grammar-based mangling rules
D) Credential stuffing requires GPU acceleration while dictionary attacks do not

---

Q25. Which of the following correctly ranks MFA methods from weakest to strongest?

A) FIDO2 → TOTP App → Push Notification → SMS OTP
B) SMS OTP → TOTP App → Push Notification → FIDO2
C) TOTP App → SMS OTP → FIDO2 → Push Notification
D) Push Notification → FIDO2 → SMS OTP → TOTP App

---

Q26. Which of the following password storage methods is the MOST resistant to offline GPU-based cracking?

A) MD5 with salt
B) SHA-256 without salt
C) NT Hash (MD4)
D) Argon2id with tuned parameters

---

Q27. A SIEM alert fires showing a single IP address attempting to authenticate against 300 different user accounts using the password "Summer2024!" within a 10-minute window. What type of attack is this?

A) Brute force attack
B) Credential stuffing attack
C) Password spraying attack
D) Offline dictionary attack

---

Q28. Which of the following correctly describes the difference between spyware and a keylogger?

A) Keyloggers are always hardware devices; spyware is always software-based
B) Keyloggers focus specifically on capturing keystrokes; spyware provides broader surveillance including screen capture, audio, GPS, and file exfiltration
C) Spyware only targets mobile devices; keyloggers only target desktop systems
D) Keyloggers transmit data to a C2 server; spyware only stores captured data locally

---

Q29. Under the Indian IT Act 2000, installing a keylogger on another person's computer system without authorisation primarily falls under which section?

A) Section 67
B) Section 66F
C) Section 66E
D) Section 66

---

Q30. What is the CVE identifier for the Log4Shell vulnerability and what CVSS score was it assigned?

A) CVE-2024-3094, CVSS 10.0
B) CVE-2023-41064, CVSS 9.8
C) CVE-2021-44228, CVSS 10.0
D) CVE-2021-34527, CVSS 8.8




---




---




---

## Answers & Explanations

---

Q1. Correct Answer: C) MD4 ✅

Explanation: Windows computes the NT Hash using the MD4 algorithm applied to the UTF-16-LE encoded password — written as MD4(UTF-16-LE(password)). It is unsalted, making it fast to crack at scale.

A) MD5 — ❌ MD5 is used in other contexts but NOT for NT Hash computation.
B) SHA-1 — ❌ SHA-1 is not used in Windows NTLM password hashing.
C) MD4 — ✅ Correct. NT Hash = MD4(UTF-16-LE(password)).
D) bcrypt — ❌ bcrypt is a modern password hashing function — Windows does not use it for NT Hash.

---

Q2. Correct Answer: D) -m 1000 ✅

Explanation: Hashcat mode -m 1000 targets NT Hash (NTLM). This is a heavily tested key fact. The other modes are: -m 5600 = NTLMv2, -m 1800 = sha512crypt (Linux), -m 3200 = bcrypt.

A) -m 5600 — ❌ This is the mode for NTLMv2 (captured challenge-response hashes via Responder).
B) -m 1800 — ❌ This is sha512crypt used in Linux /etc/shadow files.
C) -m 3200 — ❌ This is bcrypt — intentionally the slowest mode.
D) -m 1000 — ✅ Correct. NT Hash = Hashcat -m 1000.

---

Q3. Correct Answer: B) T1056.001 ✅

Explanation: MITRE ATT&CK T1056 is Input Capture (the parent technique). T1056.001 is the specific sub-technique for Keylogging. T1113 is Screen Capture, T1040 is Network Sniffing, T1055 is Process Injection.

A) T1040 — ❌ T1040 is Network Sniffing — a different credential access technique.
B) T1056.001 — ✅ Correct. This is the specific MITRE ID for Keylogging.
C) T1113 — ❌ T1113 is Screen Capture — a spyware capability, not keylogging specifically.
D) T1055 — ❌ T1055 is Process Injection — used for evasion, not keylogging classification.

---

Q4. Correct Answer: C) Argon2 ✅

Explanation: Argon2 won the Password Hashing Competition (PHC) in 2015. The recommended variant is Argon2id. It is memory-hard and tunable — making it the current best practice for password storage. bcrypt (1999) and scrypt (2009) are strong but older.

A) bcrypt — ❌ bcrypt (1999) is strong and still acceptable but predates the PHC and did not win it.
B) scrypt — ❌ scrypt (2009) is memory-hard and strong but was not the PHC winner.
C) Argon2 — ✅ Correct. PHC winner 2015 — current best practice.
D) SHA-512 — ❌ SHA-512 is a general-purpose hash function — not designed for password storage and not the PHC winner.

---

Q5. Correct Answer: D) 4740 ✅

Explanation: Windows Event ID 4740 is generated when an account is locked out. Key Event IDs: 4624 = successful logon, 4625 = failed logon, 4776 = NTLM authentication attempt, 4771 = Kerberos pre-auth failure.

A) 4625 — ❌ 4625 is failed logon — not account lockout. Both are related but distinct events.
B) 4624 — ❌ 4624 is successful logon.
C) 4776 — ❌ 4776 is an NTLM authentication attempt (success or failure).
D) 4740 — ✅ Correct. Account locked out.

---

Q6. Correct Answer: B) Local Administrator Password Solution ✅

Explanation: LAPS = Local Administrator Password Solution. It is a Microsoft tool that automatically generates and rotates unique local administrator passwords per machine, storing them in Active Directory. This directly blocks Pass-the-Hash lateral movement since the same hash cannot be reused across machines.

A) Local Access Password System — ❌ This is a fabricated expansion.
B) Local Administrator Password Solution — ✅ Correct full form.
C) Lightweight Admin Password Service — ❌ Fabricated expansion.
D) Local Authentication Protection Standard — ❌ Fabricated expansion.

---

Q7. Correct Answer: D) TOTP ✅

Explanation: TOTP = Time-based One-Time Password (RFC 6238). It generates a new 6-digit code every 30 seconds based on the current time and a shared secret. HOTP is counter-based (not time-based). FIDO2 uses hardware keys. SMS OTP is carrier-delivered.

A) HOTP — ❌ HOTP = HMAC-based OTP (RFC 4226) — counter-based, not time-based.
B) FIDO2 — ❌ FIDO2 is a hardware security key standard — not a time-based OTP.
C) SMS OTP — ❌ SMS OTP is delivered via text message — not a rotating time-based code.
D) TOTP — ✅ Correct. Time-based, 30-second rotation, RFC 6238.

---

Q8. Correct Answer: C) MVT ✅

Explanation: MVT = Mobile Verification Toolkit, developed and released by Amnesty International's Security Lab. It analyses iOS backups and Android filesystems for Pegasus indicators of compromise (IOCs). It is the forensic standard for detecting Pegasus on targeted devices.

A) Cuckoo — ❌ Cuckoo is an automated malware sandbox — used for dynamic malware analysis, not mobile Pegasus detection.
B) MobSF — ❌ MobSF = Mobile Security Framework — used for mobile app security testing, not Pegasus IOC detection.
C) MVT — ✅ Correct. Amnesty International tool specifically for Pegasus detection.
D) Wireshark — ❌ Wireshark is a network protocol analyser — not a mobile spyware forensics tool.

---

Q9. Correct Answer: C) 4625 ✅

Explanation: Windows Event ID 4625 = failed logon attempt. This is the primary event monitored in SIEM for brute force and spraying detection. 4624 = successful logon, 4740 = account locked out, 4771 = Kerberos pre-auth failed.

A) 4624 — ❌ 4624 is successful logon — the opposite event.
B) 4648 — ❌ 4648 is logon with explicit credentials (RunAs) — not a failed logon.
C) 4625 — ✅ Correct. Failed logon.
D) 4771 — ❌ 4771 is Kerberos pre-authentication failure — related but Kerberos-specific.

---

Q10. Correct Answer: D) SetWindowsHookEx() ✅

Explanation: API-based software keyloggers use the Windows API function SetWindowsHookEx() to install a low-level keyboard hook in user space. This intercepts keystrokes before they reach the target application. It is the most common and easiest keylogger implementation — and also the easiest for AV to detect.

A) CreateRemoteThread() — ❌ Used for process injection — not keyboard hooking specifically.
B) VirtualAllocEx() — ❌ Used for allocating memory in a remote process — part of injection techniques, not keylogging.
C) RegSetValueEx() — ❌ Used to write to the Windows Registry — commonly used for persistence, not keylogging.
D) SetWindowsHookEx() — ✅ Correct. The standard Windows API for installing keyboard hooks.

---

Q11. Correct Answer: B) NSO Group ✅

Explanation: Pegasus spyware was developed by NSO Group, an Israeli surveillance technology company. The 2021 Pegasus Project investigation by Citizen Lab and Forbidden Stories revealed its use against journalists, activists, and heads of state in 45+ countries. Citizen Lab investigated it but did not develop it.

A) Citizen Lab — ❌ Citizen Lab is the research group that investigated and exposed Pegasus — they did not create it.
B) NSO Group — ✅ Correct. Israeli company — developer of Pegasus.
C) FinFisher Group — ❌ FinFisher (Gamma Group) developed FinSpy — a different commercial spyware product.
D) Hacking Team — ❌ Hacking Team developed the Remote Control System (RCS/Galileo) — a different commercial spyware.

---

Q12. Correct Answer: C) A wordlist derived from the 2009 RockYou breach containing 32 million plaintext passwords ✅

Explanation: rockyou.txt originated from the 2009 RockYou data breach where approximately 32 million user passwords were stored in plaintext and leaked. It became the most widely used wordlist for password cracking. The expanded version (RockYou2021) contains 8.4 billion entries.

A) A Hashcat rule file used to mangle passwords — ❌ rockyou.txt is a wordlist, not a rule file. Hashcat rule files have a .rule extension.
B) A Linux system configuration file from 2005 — ❌ Entirely fabricated — no such file exists.
C) A wordlist derived from the 2009 RockYou breach containing 32 million plaintext passwords — ✅ Correct.
D) A rainbow table precomputed for MD5 hashes — ❌ rockyou.txt is a plaintext wordlist — not a rainbow table.

---

Q13. Correct Answer: B) Because the attacker works on a local copy of the stolen hash file — the target account is never contacted ✅

Explanation: This is one of the most important exam concepts. In offline cracking, the attacker first steals the hash file (SAM, NTDS.dit, /etc/shadow) and then cracks it locally using Hashcat or John the Ripper. The target system is never contacted during cracking. Account lockout only triggers on live authentication attempts — which never happen in offline attacks.

A) Because lockout only applies to standard user accounts, not admin accounts — ❌ Lockout can be applied to any account — this is not the reason it fails against offline attacks.
B) Because the attacker works on a local copy of the stolen hash file — the target account is never contacted — ✅ Correct. No authentication attempt = no lockout trigger.
C) Because offline cracking tools can automatically reset lockout counters remotely — ❌ No such capability exists in standard cracking tools.
D) Because Windows does not apply lockout policies to hash-based authentication — ❌ This is false — Windows lockout applies to all authentication attempts.

---

Q14. Correct Answer: C) Brute force tries many passwords against one account; spraying tries one password against many accounts ✅

Explanation: This distinction is critical for both exam and SIEM detection questions. Brute force = high volume against one account = triggers lockout quickly. Password spraying = low volume per account across many accounts = stays under lockout threshold on every account. Completely different attack signatures.

A) Brute force uses GPU acceleration; password spraying does not — ❌ GPU acceleration is relevant to offline cracking, not this distinction.
B) Brute force is always offline; password spraying is always online — ❌ Brute force can be both online and offline. This is not the defining difference.
C) Brute force tries many passwords against one account; spraying tries one password against many accounts — ✅ Correct. This is the defining distinction.
D) Brute force uses a wordlist; password spraying generates passwords algorithmically — ❌ Both can use wordlists — this is not the defining difference.

---

Q15. Correct Answer: C) bcrypt has a configurable cost factor making it intentionally slow — processing ~6–25 hashes per second versus billions per second for SHA-256 ✅

Explanation: The cost factor (work factor) in bcrypt is deliberately designed to make each hash computation slow. At cost factor 12, a single GPU processes approximately 6 hashes per second. Compare this to SHA-256 which processes ~20 billion hashes per second on the same hardware. This computational gap makes bcrypt exponentially harder to crack offline.

A) bcrypt produces a longer hash output that is harder to store — ❌ Hash output length is irrelevant to cracking resistance — what matters is computation speed.
B) bcrypt is memory-hard and physically cannot run on GPUs — ❌ bcrypt is slow on GPUs but can run on them. Argon2 and scrypt are the memory-hard algorithms.
C) bcrypt has a configurable cost factor making it intentionally slow — ✅ Correct. Intentional slowness is the security feature.
D) bcrypt automatically rotates the stored hash every 90 days — ❌ bcrypt does not auto-rotate hashes. This is a fabricated feature.

---

Q16. Correct Answer: B) It intercepts browser form data before HTTPS encryption is applied, bypassing TLS entirely ✅

Explanation: Form-grabbing keyloggers hook into the browser process and capture form submissions — username and password fields — at the point where the browser processes them, which is before the data is encrypted by HTTPS/TLS. This is why HTTPS offers no protection once the endpoint is compromised. This technique was used in Zeus and TrickBot banking trojans.

A) It can activate the device microphone without user knowledge — ❌ Microphone activation is a spyware capability, not specific to form-grabbing keyloggers.
B) It intercepts browser form data before HTTPS encryption is applied, bypassing TLS entirely — ✅ Correct. Pre-encryption interception is the key danger.
C) It installs itself as a kernel driver that survives OS reinstallation — ❌ Form grabbers operate at the browser/application level, not kernel level.
D) It spreads automatically across the network like a worm — ❌ Self-propagation is a worm characteristic — not a form-grabbing keylogger property.

---

Q17. Correct Answer: B) Hardware keyloggers leave no software footprint and are completely invisible to antivirus tools ✅

Explanation: A hardware keylogger (e.g., USB inline device) is a physical component — it has no software process, no files on disk, and generates no system calls. Antivirus tools scan software — they cannot detect a physical device plugged between the keyboard and the USB port. This is both their greatest strength and the reason physical security is the only countermeasure.

A) Hardware keyloggers can intercept wireless network traffic simultaneously — ❌ Hardware keyloggers capture keystrokes — not network traffic. That is a different attack entirely.
B) Hardware keyloggers leave no software footprint and are completely invisible to antivirus tools — ✅ Correct.
C) Hardware keyloggers can automatically exfiltrate data over the internet — ❌ Basic USB inline hardware keyloggers store data locally — the attacker must physically retrieve the device to read the log.
D) Hardware keyloggers work across all operating systems without configuration — ❌ While they are OS-agnostic at the hardware level, this is not their primary security advantage.

---

Q18. Correct Answer: C) Pass-the-Hash and credential caching attacks by disabling NTLM authentication ✅

Explanation: The Windows Protected Users security group enforces strict authentication policies on its members: NTLM authentication is disabled (Kerberos only), credentials are not cached on the device, DES and RC4 are not used, and Kerberos delegation is restricted. This directly blocks Pass-the-Hash (which requires NTLM) and prevents credential dumping from cache.

A) SQL injection against domain-joined applications — ❌ SQL injection is an application-layer attack — not addressed by Windows authentication group membership.
B) DNS spoofing against the domain controller — ❌ DNS spoofing is a network attack — not mitigated by Protected Users group.
C) Pass-the-Hash and credential caching attacks by disabling NTLM authentication — ✅ Correct.
D) Kerberoasting attacks against service account SPNs — ❌ Kerberoasting is mitigated by strong service account passwords and AES encryption — not by Protected Users group membership.

---

Q19. Correct Answer: C) To ensure two users with the same password produce different hash values, defeating rainbow table attacks ✅

Explanation: Without salting, hash("password123") produces the same value for every user who uses that password. An attacker with a precomputed rainbow table instantly finds the plaintext. With a unique random salt per user, even identical passwords produce different hashes — forcing the attacker to crack each hash individually rather than using a lookup table.

A) To increase the computational speed of the hashing process — ❌ Salting does not affect speed. Intentional slowness is the role of bcrypt/Argon2 cost factors.
B) To extend the length of the final stored hash value — ❌ The salt may affect input length but the output hash size is determined by the algorithm, not the salt.
C) To ensure two users with the same password produce different hash values, defeating rainbow table attacks — ✅ Correct.
D) To encrypt the hash using a secret application-level key — ❌ That describes peppering, not salting. A salt is not a secret — it is stored alongside the hash.

---

Q20. Correct Answer: D) Offline cracking attack ✅

Explanation: In an offline cracking attack, the attacker already possesses the hash file and cracks it entirely on local hardware. There are zero interactions with the target authentication system — no login attempts, no network packets to the target, no logs generated on the target. This is why it is the hardest class of attack to detect and why strong password hashing is the only effective countermeasure.

A) Brute force attack — ❌ Online brute force generates many failed login attempts (Event ID 4625) — highly visible in logs.
B) Password spraying attack — ❌ Spraying sends authentication attempts to the live service — it generates login events, just spread across many accounts.
C) Credential stuffing attack — ❌ Credential stuffing also contacts the live authentication service — it generates successful and failed login logs.
D) Offline cracking attack — ✅ Correct. No target contact = zero authentication logs.

---

Q21. Correct Answer: C) MFA fatigue or push bombing ✅

Explanation: The 2022 Uber breach involved an attacker who obtained an employee's credentials and then sent continuous MFA push notification requests to the employee's phone. After receiving numerous requests late at night, the fatigued employee eventually approved one — granting the attacker full access. This attack technique is called MFA fatigue or push bombing and specifically targets push-based MFA systems.

A) SIM swapping — ❌ SIM swapping involves convincing a carrier to transfer a phone number — not applicable here. No SIM transfer occurred in the Uber breach.
B) SS7 interception — ❌ SS7 attacks intercept SMS at the telecom protocol level — not relevant to push notification abuse.
C) MFA fatigue or push bombing — ✅ Correct. The defining characteristic of this attack.
D) TOTP token cloning — ❌ TOTP cloning would require access to the shared secret — not what happened in the Uber case.

---

Q22. Correct Answer: C) Administrator or root privileges to install a kernel-mode driver ✅

Explanation: A kernel-level keylogger runs in ring 0 (kernel space) and must be installed as a Windows kernel driver or Linux kernel module. This requires administrator or root privileges. In contrast, an API-based keylogger using SetWindowsHookEx() runs in user space and does not require elevated privileges for basic operation — making it accessible to unprivileged malware.

A) An active internet connection to a C2 server — ❌ Neither keylogger type requires an internet connection for installation — exfiltration is separate from installation.
B) Physical access to install a hardware component — ❌ Physical access is required for hardware keyloggers — software keyloggers (both API and kernel) are installed remotely or via malware.
C) Administrator or root privileges to install a kernel-mode driver — ✅ Correct.
D) The target user to be actively logged in during installation — ❌ Not a distinguishing requirement between the two software types.

---

Q23. Correct Answer: D) Mandatory periodic password rotation unless a compromise is suspected ✅

Explanation: NIST SP 800-63B (2017, revised 2023) explicitly states that mandatory periodic password rotation — the traditional 30/60/90-day change policy — should NOT be enforced unless a compromise is suspected. Research showed this practice leads to predictable patterns (Password1! → Password2!) that weaken security. NIST now recommends rotation only on evidence of compromise.

A) Enforcing a minimum password length — ❌ NIST SP 800-63B still recommends minimum length (8 characters minimum, 15+ for sensitive accounts). This was NOT removed.
B) Allowing users to paste passwords into login fields — ❌ NIST SP 800-63B explicitly requires that paste functionality be allowed — blocking it was the old (bad) practice.
C) Checking submitted passwords against known breached password databases — ❌ NIST SP 800-63B added this requirement — it was not in traditional policies.
D) Mandatory periodic password rotation unless a compromise is suspected — ✅ Correct. This is the most well-known reversal in NIST SP 800-63B.

---

Q24. Correct Answer: B) Credential stuffing uses real leaked username and password pairs from previous breaches and replays them against other services ✅

Explanation: Credential stuffing relies on the fact that users reuse passwords across multiple services. Attackers take username:password pairs from a known breach (e.g., LinkedIn 2012) and test them against other services (e.g., banking, email). A dictionary attack, by contrast, uses generic wordlists of likely passwords — not real pairs from a specific breach. Credential stuffing is more efficient because the passwords are already known to be real user choices.

A) Credential stuffing targets hash files offline; dictionary attacks target live systems — ❌ Both can target live systems. The key difference is the source of the credential list.
B) Credential stuffing uses real leaked username and password pairs from previous breaches and replays them against other services — ✅ Correct.
C) Credential stuffing generates passwords using grammar-based mangling rules — ❌ That describes rule-based attacks in Hashcat — not credential stuffing.
D) Credential stuffing requires GPU acceleration while dictionary attacks do not — ❌ Neither attack type is defined by GPU usage — this is irrelevant to the distinction.

---

Q25. Correct Answer: B) SMS OTP → TOTP App → Push Notification → FIDO2 ✅

Explanation: MFA strength ranking from weakest to strongest: SMS OTP (vulnerable to SIM swapping and SS7 attacks) → TOTP App (stronger — requires physical device access but code can be phished) → Push Notification (convenient but vulnerable to MFA fatigue/push bombing) → FIDO2/WebAuthn hardware keys (strongest — phishing-resistant, hardware-bound, cannot be intercepted remotely).

A) FIDO2 → TOTP App → Push Notification → SMS OTP — ❌ This is the reverse of correct — strongest listed first.
B) SMS OTP → TOTP App → Push Notification → FIDO2 — ✅ Correct. Weakest to strongest.
C) TOTP App → SMS OTP → FIDO2 → Push Notification — ❌ Incorrect ordering — SMS is weaker than TOTP, and FIDO2 is the strongest.
D) Push Notification → FIDO2 → SMS OTP → TOTP App — ❌ Incorrect ordering on multiple positions.

---

Q26. Correct Answer: D) Argon2id with tuned parameters ✅

Explanation: Argon2id is the Password Hashing Competition winner (2015) and the current best practice. It is memory-hard and CPU-hard with tunable parameters — meaning the cost can be set to require significant memory and time per hash. This makes GPU-based parallel cracking extremely inefficient. MD5, SHA-256, and NT Hash (MD4) are general-purpose fast hashes — never suitable for password storage.

A) MD5 with salt — ❌ Even salted MD5 processes ~60 billion hashes/second on a GPU — completely broken for password storage.
B) SHA-256 without salt — ❌ SHA-256 without salt is vulnerable to rainbow tables AND processes ~20 billion hashes/second — doubly unsuitable.
C) NT Hash (MD4) — ❌ NT Hash processes ~164 billion hashes/second on a modern GPU — the fastest to crack of the options listed.
D) Argon2id with tuned parameters — ✅ Correct. Memory-hard, PHC winner, current best practice.

---

Q27. Correct Answer: C) Password spraying attack ✅

Explanation: The defining signature of password spraying is: one (or few) passwords tested against a large number of different accounts from the same source within a short time window. Here — one password "Summer2024!" against 300 accounts in 10 minutes — is a textbook spraying pattern. Brute force would show hundreds of attempts against one specific account.

A) Brute force attack — ❌ Brute force targets one account with many passwords — here many accounts are targeted with one password.
B) Credential stuffing attack — ❌ Credential stuffing uses unique username:password pairs per account — not one password across all accounts.
C) Password spraying attack — ✅ Correct. One password, many accounts, short window.
D) Offline dictionary attack — ❌ An offline attack involves no live authentication attempts — it cannot generate SIEM authentication alerts.

---

Q28. Correct Answer: B) Keyloggers focus specifically on capturing keystrokes; spyware provides broader surveillance including screen capture, audio, GPS, and file exfiltration ✅

Explanation: A keylogger is a specific tool with a narrow purpose — capturing what is typed. Spyware is a broader surveillance category covering screen capture (T1113), audio recording (T1123), video/webcam (T1125), clipboard (T1115), GPS tracking, file exfiltration, and more. A keylogger may be one component within a larger spyware package, but the two are not equivalent.

A) Keyloggers are always hardware devices; spyware is always software-based — ❌ Keyloggers include both hardware and software variants. Spyware is software-based but this is not the defining distinction.
B) Keyloggers focus specifically on capturing keystrokes; spyware provides broader surveillance — ✅ Correct. Scope is the key difference.
C) Spyware only targets mobile devices; keyloggers only target desktop systems — ❌ Both target all platforms including desktop and mobile.
D) Keyloggers transmit data to a C2 server; spyware only stores data locally — ❌ This is reversed — most spyware exfiltrates to C2 servers. Some keyloggers store locally and require physical retrieval.

---

Q29. Correct Answer: D) Section 66 ✅

Explanation: IT Act 2000, Section 66 covers dishonest or fraudulent acts referred to in Section 43 — including unauthorised access to and use of a computer system. Installing a keylogger on another person's system without consent constitutes unauthorised access. Penalty: Up to 3 years imprisonment + fine of up to ₹5 lakh. Section 66E (privacy violation by capturing private images) may additionally apply for webcam-capable keyloggers/spyware.

A) Section 67 — ❌ Section 67 covers publishing or transmitting obscene material in electronic form — not applicable to keylogging.
B) Section 66F — ❌ Section 66F is cyber terrorism — applicable when attacks threaten national security or critical infrastructure — not standard keylogging.
C) Section 66E — ❌ Section 66E covers violation of privacy through capturing and transmitting private images — a secondary charge possible for webcam spyware but not the primary applicable section for keylogging.
D) Section 66 — ✅ Correct. Unauthorised computer access. 3 years + ₹5 lakh.

---

Q30. Correct Answer: C) CVE-2021-44228, CVSS 10.0 ✅

Explanation: Log4Shell is identified as CVE-2021-44228, assigned a CVSS score of 10.0 (Critical — the maximum). It is a remote code execution vulnerability in the Apache Log4j Java logging library. It is the highest-profile vulnerability of recent years and appears in multiple sessions as a benchmark example of a CVSS 10.0 critical CVE.

A) CVE-2024-3094, CVSS 10.0 — ❌ CVE-2024-3094 is the XZ Utils backdoor (2024) — a different critical vulnerability, also CVSS 10.0, but not Log4Shell.
B) CVE-2023-41064, CVSS 9.8 — ❌ CVE-2023-41064 is BLASTPASS — the zero-click iMessage exploit used for Pegasus delivery — not Log4Shell.
C) CVE-2021-44228, CVSS 10.0 — ✅ Correct. Log4Shell. Maximum CVSS score.
D) CVE-2021-34527, CVSS 8.8 — ❌ CVE-2021-34527 is PrintNightmare — a Windows Print Spooler RCE vulnerability — not Log4Shell.

---

## Quick Answer Key

| Q | Answer | Q | Answer | Q | Answer |
|---|---|---|---|---|---|
| Q1 | C | Q11 | B | Q21 | C |
| Q2 | D | Q12 | C | Q22 | C |
| Q3 | B | Q13 | B | Q23 | D |
| Q4 | C | Q14 | C | Q24 | B |
| Q5 | D | Q15 | C | Q25 | B |
| Q6 | B | Q16 | B | Q26 | D |
| Q7 | D | Q17 | B | Q27 | C |
| Q8 | C | Q18 | C | Q28 | B |
| Q9 | C | Q19 | C | Q29 | D |
| Q10 | D | Q20 | D | Q30 | C |

---

## Topic Coverage Map

| Q | Section | Concept Tested |
|---|---|---|
| Q1 | Section 1.3 | NT Hash algorithm (MD4) |
| Q2 | Section 1.3 | Hashcat mode for NT Hash |
| Q3 | Section 3.1 | MITRE ATT&CK ID for Keylogging |
| Q4 | Section 2.4 | Password Hashing Competition winner — Argon2 |
| Q5 | Section 2.6 | Windows Event ID — account lockout |
| Q6 | Section 2.5 | LAPS full form and purpose |
| Q7 | Section 2.3 | TOTP standard — time-based OTP |
| Q8 | Section 4.5 | MVT — Pegasus detection tool |
| Q9 | Section 2.6 | Windows Event ID — failed logon |
| Q10 | Section 3.4 | API-based keylogger — SetWindowsHookEx |
| Q11 | Section 4.2 | Pegasus developer — NSO Group |
| Q12 | Section 1.3 | rockyou.txt origin |
| Q13 | Section 2.2 | Account lockout vs offline attacks |
| Q14 | Section 1.1 | Brute force vs password spraying |
| Q15 | Section 2.4 | bcrypt cost factor — cracking resistance |
| Q16 | Section 3.4 | Form-grabbing keylogger — HTTPS bypass |
| Q17 | Section 3.3 | Hardware keylogger — AV invisibility |
| Q18 | Section 2.5 | Protected Users Group — PtH prevention |
| Q19 | Section 2.4 | Purpose of password salting |
| Q20 | Section 1.3 | Offline attacks — zero authentication logs |
| Q21 | Section 2.3 | MFA fatigue — Uber 2022 |
| Q22 | Section 3.4 | Kernel keylogger — privilege requirement |
| Q23 | Extra Notes | NIST SP 800-63B — deprecated practices |
| Q24 | Section 1.1 | Credential stuffing vs dictionary attack |
| Q25 | Section 2.3 | MFA strength ranking |
| Q26 | Section 2.4 | Most resistant password hashing — Argon2id |
| Q27 | Section 1.1 | Password spraying SIEM detection pattern |
| Q28 | Section 4.1 | Keylogger vs Spyware — scope difference |
| Q29 | Extra Notes | IT Act 2000 S.66 — keylogger legal context |
| Q30 | Extra Notes | Log4Shell — CVE-2021-44228 — CVSS 10.0 |

---