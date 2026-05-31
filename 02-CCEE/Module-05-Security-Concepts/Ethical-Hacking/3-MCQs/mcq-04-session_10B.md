# 📡 MCQ Set — Session 10B

**Module:** Security Concepts — Ethical Hacking
**Coverage:** Network/Port/Vulnerability Scanning · TCP Handshake · All TCP Scan Types ·
UDP Scanning · Nessus & CVSS · Burp Suite · Attack Surface Mapping
**Total Questions:** 30
**Format:** Foundation + Fundamental + Basic Concepts only

---

## 📋 Table of Contents

- [Questions — Q1 to Q30](#questions)
- [Answers & Explanations](#answers--explanations)
- [Quick Answer Key](#quick-answer-key)
- [Topic Coverage Map](#topic-coverage-map)

---

## Questions

---

**Q1.** What is the CORRECT sequence of scanning operations during Phase 2
(Scanning & Enumeration)?

- A) Vulnerability Scan → Port Scan → Network Scan → Service Detection
- B) Port Scan → Network Scan → Vulnerability Scan → Service Detection
- C) Network Scan → Port Scan → Service Detection → Vulnerability Scan
- D) Service Detection → Network Scan → Port Scan → Vulnerability Scan

---

**Q2.** A Network Scan (Host Discovery) answers which specific question?

- A) What services are running on each host?
- B) Which hosts are ALIVE and reachable on the network?
- C) Which ports have known vulnerabilities?
- D) What operating system is each host running?

---

**Q3.** During port scanning, a port responds with a SYN-ACK packet. What is
the state of this port?

- A) Closed
- B) Filtered
- C) Open
- D) Unfiltered

---

**Q4.** A port scan probe receives NO response at all after the timeout period.
What is the MOST LIKELY port state?

- A) Open
- B) Closed
- C) Filtered
- D) Unfiltered

---

**Q5.** Which statement CORRECTLY describes the relationship between an open
port and a vulnerability?

- A) Every open port is a confirmed vulnerability that must be remediated
- B) An open port means a service exists — but it is NOT necessarily vulnerable
- C) Open ports are safe as long as they are below port number 1024
- D) Filtered ports are more dangerous than open ports

---

**Q6.** In the TCP three-way handshake, what is the CORRECT sequence of
packets exchanged to establish a connection?

- A) ACK → SYN → SYN-ACK
- B) SYN → ACK → SYN-ACK
- C) SYN → SYN-ACK → ACK
- D) SYN-ACK → SYN → ACK

---

**Q7.** What does the TCP RST (Reset) flag indicate when received?

- A) The server is requesting more data before proceeding
- B) The connection should be terminated immediately — no graceful close
- C) The handshake has been successfully completed
- D) The packet contains urgent data that must be processed first

---

**Q8.** A client sends a SYN packet to a server on port 9999 where NO service
is running. What does the server send back?

- A) SYN-ACK — accepting the connection attempt
- B) No response — the port silently drops the packet
- C) RST-ACK — indicating the port is closed but the host is alive
- D) ICMP Time Exceeded — informing the client of an error

---

**Q9.** Which TCP scan type completes the FULL three-way handshake and does
NOT require root/admin privileges?

- A) SYN Scan
- B) TCP Connect Scan
- C) FIN Scan
- D) XMAS Scan

---

**Q10.** Why is the TCP Connect Scan considered the NOISIEST scan type?

- A) It sends packets with all TCP flags set simultaneously
- B) It completes the full handshake — causing BOTH the OS kernel AND the
   application to log the connection
- C) It sends fragmented packets that trigger multiple IDS alerts
- D) It uses ICMP packets which are always logged by firewalls

---

**Q11.** In a SYN Scan (Half-Open Scan), what does the scanner send AFTER
receiving a SYN-ACK from an open port?

- A) ACK — completing the three-way handshake
- B) FIN — gracefully closing the connection
- C) RST — tearing down the half-open connection without completing it
- D) Another SYN — to confirm the port is open

---

**Q12.** Why does the SYN Scan require ROOT privileges to execute?

- A) Root is needed to access the vulnerability database for CVSS scoring
- B) Root is needed to create RAW TCP packets with manually crafted headers
- C) Root is needed to read the application logs on the target system
- D) Root is needed to install Nessus plugins on the scanning system

---

**Q13.** The FIN, NULL, and XMAS scans all exploit a rule defined in which RFC?

- A) RFC 791 (Internet Protocol)
- B) RFC 793 (Transmission Control Protocol)
- C) RFC 2616 (HTTP/1.1)
- D) RFC 1918 (Private IP Address Ranges)

---

**Q14.** In a FIN scan, a tester sends a FIN packet to an OPEN port on a
Linux server. What response does the tester receive?

- A) SYN-ACK
- B) RST-ACK
- C) No response
- D) ICMP Port Unreachable

---

**Q15.** Which TCP flags are set in an XMAS scan packet — giving it the name
"Christmas Tree" scan?

- A) SYN + ACK + FIN
- B) FIN + PSH + URG
- C) SYN + PSH + RST
- D) ACK + URG + FIN

---

**Q16.** FIN, NULL, and XMAS scans all share a critical limitation. Which
operating system do these scans NOT work reliably against?

- A) Linux
- B) macOS
- C) FreeBSD
- D) Windows

---

**Q17.** For FIN, NULL, and XMAS scans — when an OPEN port gives NO response
and a FILTERED port also gives NO response, NMAP reports the port state as:

- A) Open
- B) Closed
- C) Filtered
- D) Open|Filtered

---

**Q18.** In an IDLE (Zombie) scan, the scanner's IP address:

- A) Appears in the target's logs alongside the zombie's IP
- B) NEVER appears in the target's logs — only the zombie's IP is seen
- C) Is encrypted using SSL so the target cannot read it
- D) Is replaced with a random IP address generated by NMAP

---

**Q19.** During an IDLE scan, the scanner measures the zombie's IP ID counter.
If the IP ID incremented by 2 between the baseline and measurement probes,
what does this indicate?

- A) The target port is CLOSED — the zombie did not send any extra packets
- B) The target port is OPEN — the zombie received a SYN-ACK and responded
   with a RST (one extra packet sent)
- C) The target port is FILTERED — the zombie received no response
- D) The scan failed — the zombie host is not suitable

---

**Q20.** Why is UDP scanning significantly SLOWER than TCP scanning?

- A) UDP packets are larger than TCP packets and take longer to transmit
- B) The OS rate-limits ICMP Port Unreachable messages — often to 1 per second
- C) UDP requires a three-way handshake that takes longer than TCP's
- D) UDP scanners must wait for application-layer responses on every port

---

**Q21.** Which well-known port is used by SMB (Windows file sharing) and is
commonly targeted for attacks like EternalBlue?

- A) Port 22
- B) Port 143
- C) Port 445
- D) Port 3389

---

**Q22.** What is a Nessus Plugin?

- A) A hardware adapter that connects Nessus to the target network
- B) A small program written in NASL that tests for ONE specific vulnerability
- C) A browser extension that integrates Nessus with Burp Suite
- D) A firewall rule template generated by Nessus scan results

---

**Q23.** How many MORE vulnerabilities does a CREDENTIALED Nessus scan
typically find compared to an UNCREDENTIALED scan?

- A) About the same — credentials don't significantly change results
- B) About 50% more findings
- C) 300–500% more findings
- D) 1000% more findings

---

**Q24.** A vulnerability is scored CVSS 9.8. What severity category does this
fall into?

- A) Medium
- B) High
- C) Critical
- D) Low

---

**Q25.** CVE-2021-44228 (Log4Shell) received a CVSS score of 10.0. Which
combination of CVSS base metrics produced this perfect score?

- A) Attack Vector: Local · Attack Complexity: High · Privileges Required: High
- B) Attack Vector: Network · Attack Complexity: Low · Privileges Required: None ·
   User Interaction: None · CIA Impact: High/High/High
- C) Attack Vector: Adjacent · Attack Complexity: Low · Privileges Required: Low
- D) Attack Vector: Physical · Attack Complexity: High · Privileges Required: None

---

**Q26.** Burp Suite fundamentally operates as which type of tool?

- A) A network vulnerability scanner like Nessus
- B) An intercepting HTTP/HTTPS proxy between the browser and the web server
- C) A port scanner like NMAP
- D) An intrusion detection system monitoring network traffic

---

**Q27.** Burp Suite can intercept and read HTTPS (encrypted) traffic through
a technique called SSL Bumping. What must a tester install in their browser
for this to work?

- A) The target website's SSL private key
- B) A VPN client that decrypts all traffic automatically
- C) Burp Suite's CA certificate as a trusted root certificate
- D) A special browser extension that disables HTTPS encryption

---

**Q28.** Which Burp Suite tool is described as the MOST IMPORTANT for manual
testing — allowing a tester to replay, modify, and resend individual HTTP
requests?

- A) Intruder
- B) Scanner
- C) Repeater
- D) Sequencer

---

**Q29.** An NMAP user wants to make their scan as slow and stealthy as possible
to avoid IDS detection. Which timing template should they use?

- A) `-T5` (Insane)
- B) `-T3` (Normal)
- C) `-T0` (Paranoid)
- D) `-T4` (Aggressive)

---

**Q30.** Which of the following is a key challenge specific to scanning CLOUD
environments (AWS, Azure, GCP) compared to traditional on-premises networks?

- A) Cloud environments do not have IP addresses, making scanning impossible
- B) Cloud providers require prior approval before scanning — unauthorized
   scanning can result in account suspension
- C) Cloud environments cannot run vulnerability scanners due to OS restrictions
- D) Cloud systems are immune to all known CVE vulnerabilities

---
&nbsp;

&nbsp;

&nbsp;

---

## Answers & Explanations

---

**Q1. Correct Answer: C) Network Scan → Port Scan → Service Detection →
Vulnerability Scan** ✅

**Explanation:**
The scanning phase follows a strict logical sequence — each step builds on the
output of the previous one:
1. **Network Scan** — Find which hosts are ALIVE
2. **Port Scan** — Find which PORTS are OPEN on alive hosts
3. **Service Detection** — Identify WHAT SERVICE/VERSION runs on each open port
4. **Vulnerability Scan** — Check those services against CVE databases

You don't scan for vulnerabilities on a service you haven't identified, on a port
you haven't discovered, on a host you don't know is alive.

- **A)** — ❌ Starts with vulnerability scan — you can't check for CVEs before
  knowing what services exist
- **B)** — ❌ Port scan before network scan — scanning ports on a dead host wastes time
- **C)** — ✅ Correct sequence: alive hosts → open ports → services → vulnerabilities
- **D)** — ❌ Service detection before knowing which hosts are alive — backwards

---

**Q2. Correct Answer: B) Which hosts are ALIVE and reachable on the network?** ✅

**Explanation:**
A **Network Scan** (also called Host Discovery or Ping Sweep) has ONE purpose:
identify which IP addresses in a given range are currently active and reachable.
It does NOT identify services, ports, or vulnerabilities — those are subsequent
scanning steps.

- **A)** — ❌ Service identification = Port Scanning + Service Detection (steps 2 & 3)
- **B)** — ✅ Network scan answers: "Who is alive?"
- **C)** — ❌ Known vulnerabilities = Vulnerability Scanning (step 4)
- **D)** — ❌ OS identification = OS Detection (part of Service Detection — step 3)

---

**Q3. Correct Answer: C) Open** ✅

**Explanation:**
A **SYN-ACK** response means the target is acknowledging the connection request
(SYN → SYN-ACK) — a service IS actively listening on that port and is willing
to accept the connection. This is the definitive signal that a port is **OPEN**.

- **A) Closed** — ❌ A closed port responds with **RST-ACK** (Reset — connection refused)
- **B) Filtered** — ❌ A filtered port gives **no response** (firewall drops the packet)
- **C) Open** — ✅ SYN-ACK = service is listening = port is OPEN
- **D) Unfiltered** — ❌ Unfiltered is a state from ACK scans — not from SYN probes

---

**Q4. Correct Answer: C) Filtered** ✅

**Explanation:**
When a probe receives **no response** after the timeout period, the most likely
explanation is that a **firewall or ACL is silently dropping the packet** before
it reaches the target port. The scanner cannot determine whether the port is open
or closed behind the firewall — only that something is blocking the probe.

- **A) Open** — ❌ An open port responds with SYN-ACK (for SYN probes) — it doesn't
  stay silent
- **B) Closed** — ❌ A closed port actively responds with RST-ACK — silence is not
  the response for closed ports
- **C) Filtered** — ✅ No response = firewall blocking = filtered state
- **D) Unfiltered** — ❌ Unfiltered means reachable but state indeterminate — typically
  from ACK scans, not from silence

> **Exception:** For FIN/NULL/XMAS scans, no response means `open|filtered` because
> BOTH open ports AND filtered ports give no response in those scan types.

---

**Q5. Correct Answer: B) An open port means a service exists — but it is NOT
necessarily vulnerable** ✅

**Explanation:**
An **open port** indicates that a service is actively listening — like an open door
in a building. A **vulnerability** is when that service has a specific weakness that
can be exploited — like a broken lock on the open door. Open ≠ vulnerable. A fully
patched, properly configured service on an open port may have zero exploitable
vulnerabilities.

- **A)** — ❌ Open ports are NOT automatically vulnerabilities — they may be necessary
  and properly secured services
- **B)** — ✅ Open port = door exists. Vulnerability = door has a broken lock. Separate concepts.
- **C)** — ❌ Port number has no bearing on safety — port 22 (SSH) below 1024 can be
  vulnerable, port 8080 above 1024 can be secure
- **D)** — ❌ Filtered ports are LESS accessible than open ports — the firewall is
  protecting them

---

**Q6. Correct Answer: C) SYN → SYN-ACK → ACK** ✅

**Explanation:**
The TCP three-way handshake establishes a reliable connection in exactly three steps:
1. **Client → SYN** — "I want to connect. My sequence starts at X."
2. **Server → SYN-ACK** — "Received your SYN. I'm ready. My sequence starts at Y."
3. **Client → ACK** — "Got your SYN-ACK. Connection ESTABLISHED."

This sequence must complete in this exact order for a TCP connection to be established.

- **A)** — ❌ ACK cannot come first — there's nothing to acknowledge yet
- **B)** — ❌ ACK before SYN-ACK is out of order — server must respond to SYN first
- **C)** — ✅ SYN → SYN-ACK → ACK — the correct and only valid sequence
- **D)** — ❌ SYN-ACK cannot come first — it is a RESPONSE to a SYN

---

**Q7. Correct Answer: B) The connection should be terminated immediately — no
graceful close** ✅

**Explanation:**
The **RST (Reset)** flag means: "Stop everything. Terminate this connection
immediately." Unlike FIN (which gracefully closes by finishing data transmission),
RST is an abrupt, immediate termination. Common scenarios: connection to a closed
port, firewall interruption, application error, or scanner deliberately tearing
down a half-open connection (as in SYN scan).

- **A)** — ❌ Requesting more data is handled by normal data flow — not RST
- **B)** — ✅ RST = immediate termination — no graceful closing negotiation
- **C)** — ❌ Handshake completion is signaled by the final ACK — not RST
- **D)** — ❌ Urgent data is indicated by the URG flag — not RST

---

**Q8. Correct Answer: C) RST-ACK — indicating the port is closed but the host
is alive** ✅

**Explanation:**
When a SYN arrives at a port where **no service is listening**, the TCP/IP stack
responds with **RST-ACK** — "Nothing is here. Connection refused." This is valuable
intelligence: even though the port is closed, the RST-ACK confirms the host itself
IS alive and reachable.

- **A)** — ❌ SYN-ACK means a service IS listening — the scenario states no service
  is running
- **B)** — ❌ Silent drop (no response) indicates a firewall filtering the packet —
  not a closed port with no firewall
- **C)** — ✅ RST-ACK = closed port + host is alive
- **D)** — ❌ ICMP Time Exceeded is sent when TTL expires at a router (traceroute) —
  not related to port state

---

**Q9. Correct Answer: B) TCP Connect Scan** ✅

**Explanation:**
**TCP Connect Scan** (`nmap -sT`) uses the operating system's standard network
stack to complete the FULL three-way handshake (SYN → SYN-ACK → ACK). Because it
uses the standard socket API — not raw packets — it does NOT require root/admin
privileges. All other scan types (SYN, FIN, NULL, XMAS, IDLE) create raw packets
with custom headers, which requires root.

- **A) SYN Scan** — ❌ Requires root — crafts raw SYN packets outside the OS stack
- **B) TCP Connect** — ✅ Uses standard OS socket API — no root needed — completes
  full handshake
- **C) FIN Scan** — ❌ Requires root — sends raw FIN-only packets
- **D) XMAS Scan** — ❌ Requires root — sends raw FIN+PSH+URG packets

---

**Q10. Correct Answer: B) It completes the full handshake — causing BOTH the
OS kernel AND the application to log the connection** ✅

**Explanation:**
TCP Connect Scan is the noisiest because it completes the FULL three-way handshake.
When a TCP connection is fully established:
1. The **OS kernel** records the connection in its connection table
2. The **application** (e.g., Apache, SSH) logs the incoming connection attempt

Two separate logging systems capture the scan activity — making it easily detectable
by any monitoring system.

- **A)** — ❌ Sending all flags simultaneously is the XMAS scan concept — not TCP Connect
- **B)** — ✅ Full handshake completion → OS log + application log = two detection points
- **C)** — ❌ Fragmented packets are an evasion technique (`-f`) — not related to
  TCP Connect scan behavior
- **D)** — ❌ TCP Connect uses TCP packets — not ICMP

---

**Q11. Correct Answer: C) RST — tearing down the half-open connection without
completing it** ✅

**Explanation:**
This is the defining characteristic of the SYN Scan:
- TCP Connect: SYN → SYN-ACK → **ACK** (completes connection)
- SYN Scan: SYN → SYN-ACK → **RST** (tears down before completion)

By sending RST instead of ACK, the handshake is NEVER completed. The target OS
does not record a completed connection — only a "half-open" that was reset. This
is why it's called the "Half-Open" or "Stealth" scan.

- **A) ACK** — ❌ Sending ACK would complete the handshake — that's TCP Connect scan
- **B) FIN** — ❌ FIN gracefully closes — but there's no established connection to close
- **C) RST** — ✅ Immediately tears down the half-open connection — no completion log
- **D) Another SYN** — ❌ Sending a second SYN would be invalid and confuse the connection

---

**Q12. Correct Answer: B) Root is needed to create RAW TCP packets with manually
crafted headers** ✅

**Explanation:**
Standard applications use the OS network stack's socket API for TCP connections
(no special privileges needed). SYN scan BYPASSES the OS network stack entirely —
it crafts RAW TCP packets with manually set flags (SYN only, then RST). Creating
raw packets requires **root/admin** privileges because it gives direct access to
the network interface — a capability the OS restricts for security reasons.
NMAP uses **libpcap** for this raw packet crafting.

- **A)** — ❌ CVSS scoring is unrelated to packet crafting — Nessus handles that
- **B)** — ✅ Raw packet creation bypasses the OS stack — requires root privileges
- **C)** — ❌ Reading target application logs is irrelevant — SYN scan avoids those logs
- **D)** — ❌ Nessus plugins are unrelated to why NMAP needs root for SYN scan

---

**Q13. Correct Answer: B) RFC 793 (Transmission Control Protocol)** ✅

**Explanation:**
**RFC 793** is the original TCP specification. It defines a rule that FIN, NULL,
and XMAS scans all exploit: when an unexpected packet (one without SYN or ACK in
the context of an established connection) arrives at an **open port**, the host
should **silently discard** it. When it arrives at a **closed port**, the host
**MUST respond with RST**. This behavioral difference is what reveals port state.

- **A) RFC 791** — ❌ RFC 791 defines the Internet Protocol (IP) — not TCP behavior
- **B) RFC 793** — ✅ The TCP specification — defines the rule these scans exploit
- **C) RFC 2616** — ❌ RFC 2616 defines HTTP/1.1 — application layer, not TCP behavior
- **D) RFC 1918** — ❌ RFC 1918 defines private IP address ranges — unrelated to scanning

---

**Q14. Correct Answer: C) No response** ✅

**Explanation:**
According to **RFC 793**: when a FIN packet arrives at an **OPEN port** with no
established connection, the host should **silently discard** it. The service is
listening, but the FIN is unexpected and meaningless (there's no connection to
finish) — so the host simply ignores it.

If the port were CLOSED, the host would respond with RST-ACK.

- **A) SYN-ACK** — ❌ SYN-ACK is the response to a SYN packet — not to a FIN
- **B) RST-ACK** — ❌ RST-ACK indicates a CLOSED port — not an open one
- **C) No response** — ✅ Open port silently discards unexpected FIN per RFC 793
- **D) ICMP Port Unreachable** — ❌ ICMP Port Unreachable is a UDP closed port response —
  not TCP

> This is counterintuitive — "no response = open" — but it's a critical concept for
> understanding RFC exploitation scans.

---

**Q15. Correct Answer: B) FIN + PSH + URG** ✅

**Explanation:**
The **XMAS Scan** sets three flags simultaneously: **FIN + PSH + URG**. In the TCP
flag field visualization, three "lights" are ON — resembling a Christmas tree with
lights lit up. This combination is completely illogical in normal TCP operations —
no legitimate system would ever send a packet with this flag combination outside
an established connection.
- URG PSH RST SYN FIN ACK 1 1 0 0 1 0 ← XMAS scan (3 lights on)

- **A) SYN + ACK + FIN** — ❌ This combination is not the XMAS scan
- **B) FIN + PSH + URG** — ✅ The three "Christmas tree" flags
- **C) SYN + PSH + RST** — ❌ Not the XMAS scan flag combination
- **D) ACK + URG + FIN** — ❌ ACK is not part of XMAS — PSH is

---

**Q16. Correct Answer: D) Windows** ✅

**Explanation:**
FIN, NULL, and XMAS scans rely on RFC 793's rule for handling unexpected packets.
**Windows does NOT strictly follow RFC 793** for these edge cases — it sends
**RST-ACK for BOTH open AND closed ports**, making it impossible to distinguish
between them. These scans only work reliably on **RFC-compliant systems** like
Linux, FreeBSD, macOS, and other UNIX-based operating systems.

- **A) Linux** — ❌ Linux follows RFC 793 strictly — these scans WORK on Linux
- **B) macOS** — ❌ macOS (BSD-based) follows RFC 793 — these scans work
- **C) FreeBSD** — ❌ FreeBSD follows RFC 793 — these scans work
- **D) Windows** — ✅ Windows sends RST-ACK for both open AND closed — scans fail

---

**Q17. Correct Answer: D) Open|Filtered** ✅

**Explanation:**
For FIN, NULL, and XMAS scans, the response to both OPEN and FILTERED ports is
the same: **no response**. NMAP cannot distinguish between the two scenarios:
- Open port → silently discards invalid packet → no response
- Filtered port → firewall drops packet → no response

Since NMAP cannot determine which case it is, it reports the ambiguous state
**open|filtered**. Only a closed port gives a definitive RST-ACK response.

- **A) Open** — ❌ NMAP cannot confirm it's open — could also be filtered
- **B) Closed** — ❌ Closed ports give RST-ACK — a definitive response
- **C) Filtered** — ❌ NMAP cannot confirm it's filtered — could also be open
- **D) Open|Filtered** — ✅ Ambiguous — no response could be either state

---

**Q18. Correct Answer: B) NEVER appears in the target's logs — only the
zombie's IP is seen** ✅

**Explanation:**
The IDLE (Zombie) scan is the **most anonymous** scan technique. The scanner sends
a SYN packet to the target with the **source IP spoofed as the zombie's IP**. The
target responds to the ZOMBIE — not to the scanner. The scanner's real IP address
NEVER appears in any packet that reaches the target. The target's logs only show
traffic from the zombie host.

- **A)** — ❌ The scanner's IP does NOT appear alongside the zombie's — it is
  completely absent from target logs
- **B)** — ✅ Scanner IP never touches target — only zombie IP appears in target logs
- **C)** — ❌ SSL encryption is irrelevant — the anonymity comes from IP spoofing,
  not encryption
- **D)** — ❌ The source IP is specifically the zombie's real IP — not random

---

**Q19. Correct Answer: B) The target port is OPEN — the zombie received a
SYN-ACK and responded with a RST (one extra packet sent)** ✅

**Explanation:**
IDLE scan IP ID logic:
- **Baseline probe:** Scanner checks zombie's IP ID (e.g., 5000)
- **Spoofed SYN sent to target**
- If port is OPEN: target sends SYN-ACK to zombie → zombie sends RST back to
  target (1 extra packet) → zombie's IP ID increments by 1 for that RST
- **Measurement probe:** Scanner checks zombie's IP ID again
- Increment of **2** = baseline probe RST (1) + target response RST (1) = **port OPEN**
- Increment of **1** = baseline probe RST only (1) + nothing from target = **port CLOSED**

- **A)** — ❌ IP ID +2 means the zombie DID send an extra packet — indicating an open port
- **B)** — ✅ IP ID increased by 2 → zombie sent one extra RST to target → port is OPEN
- **C)** — ❌ Filtered would result in IP ID +1 (same as closed — no response from target)
- **D)** — ❌ IP ID +2 is a valid, expected result — not a scan failure

---

**Q20. Correct Answer: B) The OS rate-limits ICMP Port Unreachable messages —
often to 1 per second** ✅

**Explanation:**
UDP scanning is inherently slow because the primary signal for a **closed** UDP port
is an **ICMP Port Unreachable** message. Operating systems **rate-limit** these ICMP
responses to prevent ICMP flooding — Linux defaults to approximately 1 ICMP
Port Unreachable message per second. Scanning all 65,535 UDP ports at this rate
would take **18+ hours**. This is why professional scans target only common UDP
ports (top 100 or top 1000).

- **A)** — ❌ UDP packets are NOT inherently larger than TCP — often they are smaller
  because UDP has a simpler header
- **B)** — ✅ ICMP rate limiting is the primary bottleneck for UDP scanning speed
- **C)** — ❌ UDP is connectionless — it has NO handshake at all (that's TCP)
- **D)** — ❌ Many UDP services don't respond to arbitrary probes — waiting for
  application-layer responses is unreliable, not the primary speed bottleneck

---

**Q21. Correct Answer: C) Port 445** ✅

**Explanation:**
**Port 445** is used by **SMB (Server Message Block)** — the Windows file sharing
protocol. It is one of the most commonly targeted ports in penetration testing
because SMB has been the attack vector for major exploits including **EternalBlue**
(MS17-010, used by WannaCry ransomware in 2017) and is frequently targeted for
password attacks and lateral movement.

- **A) Port 22** — ❌ Port 22 = SSH (Secure Shell) — remote terminal access
- **B) Port 143** — ❌ Port 143 = IMAP — email access protocol
- **C) Port 445** — ✅ SMB — Windows file sharing — EternalBlue target
- **D) Port 3389** — ❌ Port 3389 = RDP (Remote Desktop Protocol) — also commonly
  attacked but not the SMB port

---

**Q22. Correct Answer: B) A small program written in NASL that tests for ONE
specific vulnerability** ✅

**Explanation:**
A **Nessus Plugin** is a small program written in **NASL (Nessus Attack Scripting
Language)** that tests for exactly ONE specific vulnerability or configuration issue.
Each plugin contains: a unique Plugin ID, the CVE IDs it checks, a CVSS score,
a description, a solution/remediation, and vendor advisory references. Nessus has
**230,000+ plugins** as of 2026 — each testing a different specific vulnerability.

- **A)** — ❌ A Nessus plugin is software — not hardware
- **B)** — ✅ NASL program testing for one specific vulnerability
- **C)** — ❌ Burp Suite integration is not what a Nessus plugin does
- **D)** — ❌ Plugins are vulnerability tests — they don't generate firewall rules

---

**Q23. Correct Answer: C) 300–500% more findings** ✅

**Explanation:**
**Credentialed scanning** provides Nessus with login credentials to LOG INTO the
target system and scan from the INSIDE — checking installed patch levels, local
configurations, user permissions, software inventory, and internal services that
are not visible from outside. This internal view reveals **300–500% more
vulnerabilities** than an uncredentialed (external) scan which can only see what's
accessible without authentication.

The analogy: uncredentialed = inspector checking the building from the street.
Credentialed = inspector with a key walking through every room.

- **A)** — ❌ The difference is dramatic — not negligible
- **B)** — ❌ 50% understates the difference significantly
- **C)** — ✅ 3–5× more findings — the standard estimate across industry
- **D)** — ❌ 1000% (10×) overstates the typical difference

---

**Q24. Correct Answer: C) Critical** ✅

**Explanation:**
CVSS severity ratings:

| Score Range | Severity |
|---|---|
| 0.0 | None |
| 0.1–3.9 | Low |
| 4.0–6.9 | Medium |
| 7.0–8.9 | High |
| **9.0–10.0** | **Critical** |

A score of 9.8 falls squarely in the **Critical** range (9.0–10.0). Critical
vulnerabilities should be remediated FIRST and with highest priority.

- **A) Medium** — ❌ Medium = 4.0–6.9
- **B) High** — ❌ High = 7.0–8.9 — 9.8 exceeds this range
- **C) Critical** — ✅ 9.0–10.0 = Critical severity
- **D) Low** — ❌ Low = 0.1–3.9

---

**Q25. Correct Answer: B) Attack Vector: Network · Attack Complexity: Low ·
Privileges Required: None · User Interaction: None · CIA Impact: High/High/High** ✅

**Explanation:**
**CVE-2021-44228 (Log4Shell)** achieved the maximum possible CVSS score of 10.0
because EVERY metric was at its WORST possible value:
- **Network** attack vector — remotely exploitable from anywhere
- **Low** attack complexity — just send a crafted string
- **None** privileges required — no authentication needed
- **None** user interaction — victim doesn't need to click or do anything
- **Changed** scope — affects systems beyond the vulnerable component
- **High/High/High** CIA impact — complete loss of confidentiality, integrity,
  and availability

Every metric at its worst = 10.0 = global emergency.

- **A)** — ❌ Local attack vector and high complexity would REDUCE the score
- **B)** — ✅ All metrics at worst possible values = CVSS 10.0
- **C)** — ❌ Adjacent vector and low privileges would lower the score
- **D)** — ❌ Physical attack vector would dramatically lower the score

---

**Q26. Correct Answer: B) An intercepting HTTP/HTTPS proxy between the browser
and the web server** ✅

**Explanation:**
At its core, **Burp Suite** is an **intercepting proxy** — it sits between the
tester's browser and the target web server. All HTTP and HTTPS traffic flows
THROUGH Burp, allowing the tester to inspect, modify, replay, and drop any
request or response. While Burp has many additional tools (scanner, intruder,
sequencer), the proxy is the foundational component upon which everything else
is built.

- **A)** — ❌ Nessus is the network vulnerability scanner — Burp is a web proxy
- **B)** — ✅ Intercepting HTTP/HTTPS proxy — Burp's core function
- **C)** — ❌ NMAP is the port scanner — Burp operates at the HTTP application layer
- **D)** — ❌ An IDS monitors traffic for threats — Burp is a testing tool, not a
  monitoring tool

---

**Q27. Correct Answer: C) Burp Suite's CA certificate as a trusted root
certificate** ✅

**Explanation:**
HTTPS traffic is encrypted — Burp cannot read it without intervention. Burp uses
**SSL Bumping**: it generates a FAKE certificate for each HTTPS site, signed by
its own Certificate Authority (CA). Normally, the browser would reject this fake
cert. By installing **Burp's CA certificate** as a trusted root in the browser/OS,
the browser trusts Burp-generated certificates — allowing Burp to decrypt, read,
modify, and re-encrypt all HTTPS traffic transparently.

- **A)** — ❌ The target's private key is secret and inaccessible — Burp doesn't need
  it because it creates its OWN certificates
- **B)** — ❌ VPN doesn't decrypt HTTPS — VPN encrypts the transport tunnel, not
  the application-layer TLS
- **C)** — ✅ Burp's CA cert installed as trusted root → browser accepts Burp's
  generated certificates
- **D)** — ❌ No extension "disables" HTTPS — Burp performs proper TLS interception
  through certificate substitution

---

**Q28. Correct Answer: C) Repeater** ✅

**Explanation:**
**Repeater** is described as the MOST IMPORTANT Burp tool for manual testing.
It allows the tester to take any captured HTTP request and:
- Manually modify any part (headers, parameters, cookies, body)
- Resend it to the server
- See the full response
- Modify again → resend → see new response

This iterative test cycle — "What happens if I change THIS parameter?" — is the
foundation of manual web application security testing.

- **A) Intruder** — ❌ Intruder automates attacks with payloads (brute force, fuzzing) —
  not for individual manual request modification
- **B) Scanner** — ❌ Scanner is automated vulnerability detection — not manual testing
- **C) Repeater** — ✅ Manual request modification and replay — most important for
  manual testing
- **D) Sequencer** — ❌ Sequencer analyzes randomness of session tokens — specialized
  statistical tool

---

**Q29. Correct Answer: C) `-T0` (Paranoid)** ✅

**Explanation:**
NMAP timing templates range from T0 (slowest) to T5 (fastest):

| Template | Name | Use |
|---|---|---|
| `-T0` | **Paranoid** | Slowest — one probe per 5 minutes — maximum stealth |
| `-T1` | Sneaky | Very slow — designed to evade IDS |
| `-T2` | Polite | Slow — low bandwidth consumption |
| `-T3` | Normal | Default — balanced speed/stealth |
| `-T4` | Aggressive | Fast — for reliable networks |
| `-T5` | Insane | Fastest — may miss results on slow networks |

For maximum stealth to avoid IDS detection, `-T0` (Paranoid) is the correct choice.

- **A) `-T5`** — ❌ Insane = fastest = most easily detected — opposite of stealthy
- **B) `-T3`** — ❌ Normal = default balanced mode — detectable by modern IDS
- **C) `-T0`** — ✅ Paranoid = slowest = maximum stealth
- **D) `-T4`** — ❌ Aggressive = fast = easily detected

---

**Q30. Correct Answer: B) Cloud providers require prior approval before scanning —
unauthorized scanning can result in account suspension** ✅

**Explanation:**
Unlike traditional on-premises networks where you control all infrastructure,
**cloud environments** (AWS, Azure, GCP) are shared infrastructure owned by the
cloud provider. Each provider has **scanning policies** that require prior approval
before conducting vulnerability or port scans. Scanning without approval violates
the provider's Terms of Service and can result in **account suspension**, resource
termination, or legal action — even if you own the cloud instances being scanned.

- **A)** — ❌ Cloud environments DO have IP addresses — public IPs for internet-facing
  resources and private IPs for internal resources
- **B)** — ✅ Provider approval required — unauthorized scanning = account suspension risk
- **C)** — ❌ Vulnerability scanners run perfectly fine on cloud systems — the restriction
  is policy-based, not technical
- **D)** — ❌ Cloud systems are absolutely NOT immune to CVEs — they run the same
  software with the same vulnerabilities as on-premises systems

---

## Quick Answer Key

| Q | Answer | Q | Answer | Q | Answer |
|---|---|---|---|---|---|
| Q1 | C | Q11 | C | Q21 | C |
| Q2 | B | Q12 | B | Q22 | B |
| Q3 | C | Q13 | B | Q23 | C |
| Q4 | C | Q14 | C | Q24 | C |
| Q5 | B | Q15 | B | Q25 | B |
| Q6 | C | Q16 | D | Q26 | B |
| Q7 | B | Q17 | D | Q27 | C |
| Q8 | C | Q18 | B | Q28 | C |
| Q9 | B | Q19 | B | Q29 | C |
| Q10 | B | Q20 | B | Q30 | B |

---

## Topic Coverage Map

| Q | Section | Concept Tested |
|---|---|---|
| Q1 | Section 1 | Scanning sequence — correct order of operations |
| Q2 | Section 1 | Network Scan — purpose and question answered |
| Q3 | Section 1 | Port states — SYN-ACK = Open |
| Q4 | Section 1 | Port states — no response = Filtered |
| Q5 | Section 1 | Open port ≠ vulnerable — critical distinction |
| Q6 | Section 2 | TCP three-way handshake — exact sequence |
| Q7 | Section 2 | TCP flags — RST meaning |
| Q8 | Section 2 | Closed port response — RST-ACK |
| Q9 | Section 3 | TCP Connect Scan — full handshake, no root needed |
| Q10 | Section 3 | TCP Connect Scan — why it is noisy |
| Q11 | Section 3 | SYN Scan — RST after SYN-ACK (half-open) |
| Q12 | Section 3 | SYN Scan — why root is required (raw packets) |
| Q13 | Section 3 | FIN/NULL/XMAS — RFC 793 exploitation |
| Q14 | Section 3 | FIN Scan — open port response (no response) |
| Q15 | Section 3 | XMAS Scan — flag combination (FIN+PSH+URG) |
| Q16 | Section 3 | FIN/NULL/XMAS — Windows limitation |
| Q17 | Section 3 | FIN/NULL/XMAS — open\|filtered ambiguity |
| Q18 | Section 3 | IDLE Scan — scanner IP anonymity |
| Q19 | Section 3 | IDLE Scan — IP ID increment logic (+2 = open) |
| Q20 | Section 3 | UDP Scanning — ICMP rate limiting bottleneck |
| Q21 | Foundation | Well-known ports — SMB port 445 |
| Q22 | Section 4 | Nessus plugin — definition (NASL, one vuln per plugin) |
| Q23 | Section 4 | Credentialed vs uncredentialed — findings difference |
| Q24 | Section 4 | CVSS severity — score ranges |
| Q25 | Section 4 | CVSS base metrics — Log4Shell 10.0 breakdown |
| Q26 | Section 5 | Burp Suite — core function (intercepting proxy) |
| Q27 | Section 5 | Burp Suite — SSL bumping (CA certificate install) |
| Q28 | Section 5 | Burp Suite tools — Repeater (manual testing) |
| Q29 | Section 7 | Evasion — NMAP timing templates (T0 = Paranoid) |
| Q30 | Section 7 | Cloud scanning — provider approval requirement |

---