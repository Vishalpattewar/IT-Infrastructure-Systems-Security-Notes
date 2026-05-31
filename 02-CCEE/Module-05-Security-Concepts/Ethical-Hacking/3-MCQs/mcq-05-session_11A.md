# 🔬 MCQ Set — Session 11A

**Module:** Security Concepts — Ethical Hacking
**Coverage:** TCP Flags Deep Dive · Banner Grabbing · OS Fingerprinting ·
Proxy Servers in Attacks · HTTP Tunneling · DNS Tunneling · Domain Fronting
**Total Questions:** 28
**Format:** Foundation + Fundamental + Basic Concepts only

---

## 📋 Table of Contents

- [Questions — Q1 to Q28](#questions)
- [Answers & Explanations](#answers--explanations)
- [Quick Answer Key](#quick-answer-key)
- [Topic Coverage Map](#topic-coverage-map)

---

## Questions

---

**Q1.** In the TCP header, the control flags field contains six original flags.
Which of the following lists ALL six in their correct bit-order?

- A) SYN, ACK, FIN, RST, PSH, URG
- B) URG, ACK, PSH, RST, SYN, FIN
- C) ACK, SYN, FIN, RST, URG, PSH
- D) SYN, FIN, RST, ACK, URG, PSH

---

**Q2.** When an attacker sends thousands of SYN packets with spoofed source
IP addresses to exhaust a server's connection table, this is called:

- A) SYN Scan
- B) SYN Flood Attack
- C) TCP Connect Scan
- D) XMAS Scan

---

**Q3.** What does the TCP PSH (Push) flag instruct the receiving host to do?

- A) Reset the TCP connection immediately
- B) Buffer the data until the entire stream is received
- C) Pass the data immediately to the application layer without buffering
- D) Prioritize this packet over all other queued data using the Urgent Pointer

---

**Q4.** An attacker sends a bare ACK packet (ACK flag only, no prior SYN) to
a target port. The target responds with RST. What does this tell the attacker?

- A) The port is OPEN and a service is listening
- B) The port is CLOSED and no service is available
- C) The port is UNFILTERED — reachable through the firewall
- D) The port is FILTERED — blocked by a firewall

---

**Q5.** Why do stateless firewalls sometimes allow bare ACK packets through
while stateful firewalls block them?

- A) Stateless firewalls inspect the full TCP payload while stateful do not
- B) Stateless firewalls assume bare ACK is part of an established connection
   because they do not track connection state
- C) Stateful firewalls cannot distinguish between ACK and SYN packets
- D) Stateless firewalls use deep packet inspection to verify ACK legitimacy

---

**Q6.** During graceful TCP connection termination, how many steps (packets)
are exchanged in the four-way FIN handshake?

- A) 2 — FIN from client, ACK from server
- B) 3 — FIN, FIN-ACK, ACK
- C) 4 — FIN-ACK, ACK, FIN-ACK, ACK
- D) 5 — FIN, ACK, FIN, ACK, RST

---

**Q7.** What is the PRIMARY difference between RST and FIN in TCP connection
termination?

- A) RST is used by clients only; FIN is used by servers only
- B) FIN closes gracefully allowing data to finish; RST terminates immediately
   discarding all queued data
- C) RST is encrypted; FIN is not encrypted
- D) FIN can only be sent once per connection; RST can be sent multiple times

---

**Q8.** Every received SYN causes the target to allocate a Transmission Control
Block (TCB) entry consuming approximately how much kernel memory?

- A) 28 bytes
- B) 280 bytes
- C) 2,800 bytes
- D) 28,000 bytes

---

**Q9.** A tester connects to port 22 on a target using Netcat and receives the
response: `SSH-2.0-OpenSSH_7.4`. What technique was just performed?

- A) OS Fingerprinting
- B) Vulnerability Scanning
- C) Banner Grabbing
- D) Port Scanning

---

**Q10.** Which of the following statements about banner grabbing is CORRECT?

- A) Banners are only available on HTTP port 80 — other services do not
   send banners
- B) Almost every service broadcasts a banner — FTP (21), SSH (22), SMTP (25),
   POP3 (110), IMAP (143), and more
- C) Banners only reveal the service name — never the software version or OS
- D) Banner grabbing requires exploiting a vulnerability to extract the information

---

**Q11.** A defender configures Apache with `ServerSignature Off` and
`ServerTokens Prod`. What is the effect of this configuration?

- A) Apache stops serving web pages entirely until signatures are re-enabled
- B) The Server header shows only "Apache" — without version number or OS details
- C) Apache begins encrypting all traffic with TLS automatically
- D) Apache blocks all banner grabbing attempts at the network level

---

**Q12.** A penetration tester uses Shodan to look up service banners for a
target's IP range WITHOUT connecting to the target directly. What type of
banner grabbing is this?

- A) Active Banner Grabbing
- B) Passive Banner Grabbing
- C) Hybrid Banner Grabbing
- D) Enumeration

---

**Q13.** A banner grab reveals: `Apache httpd 2.4.49`. The tester searches the
NVD and finds CVE-2021-41773 (Path Traversal + RCE, CVSS 7.5). What is this
process of mapping a banner to a specific vulnerability called?

- A) Port Scanning
- B) Banner → CVE Mapping
- C) OS Fingerprinting
- D) Proxy Chaining

---

**Q14.** OS fingerprinting exploits differences in how operating systems
implement the TCP/IP stack. Which of the following is the DEFAULT initial
TTL value for Linux systems?

- A) 32
- B) 64
- C) 128
- D) 255

---

**Q15.** A packet captured by Wireshark shows an initial TTL of 128. Based on
default TTL values, this packet MOST LIKELY originated from which operating
system?

- A) Linux
- B) Cisco IOS
- C) Windows
- D) macOS

---

**Q16.** An analyst observes a packet with TTL=118 and estimates approximately
10 network hops between source and their capture point. What was the MOST
LIKELY initial TTL, and what OS does this suggest?

- A) Initial TTL=128 → Windows
- B) Initial TTL=64 → Linux
- C) Initial TTL=255 → Cisco IOS
- D) Initial TTL=64 → macOS

---

**Q17.** When Windows receives a FIN, NULL, or XMAS scan probe on an OPEN port,
how does it respond — and how is this different from Linux?

- A) Windows silently drops the packet (same as Linux)
- B) Windows sends RST regardless of port state; Linux silently drops on open
   ports and sends RST on closed ports (per RFC 793)
- C) Both Windows and Linux send RST on open ports
- D) Windows sends SYN-ACK; Linux sends RST

---

**Q18.** Which tool performs PASSIVE OS fingerprinting by analyzing TCP SYN
characteristics of existing traffic — completely invisible to the target?

- A) NMAP with `-O` flag
- B) Nessus
- C) p0f
- D) Netcat

---

**Q19.** JA3 fingerprinting passively identifies TLS clients by hashing specific
fields from which TLS message?

- A) ServerHello
- B) Certificate
- C) ClientHello
- D) Finished

---

**Q20.** Which proxy type operates at Layer 5 (Session layer), is
protocol-agnostic, supports BOTH TCP and UDP (in version 5), and can handle
SSH, FTP, SMTP, and DNS traffic?

- A) HTTP Proxy
- B) Transparent Proxy
- C) Anonymous Proxy
- D) SOCKS Proxy

---

**Q21.** In proxy chaining, an attacker routes traffic through proxies in the
USA, Russia, and Brazil before reaching the target. What does the TARGET see
as the source IP?

- A) The attacker's real IP address
- B) The IP of the FIRST proxy (USA)
- C) The IP of the LAST proxy (Brazil)
- D) A randomly generated IP address

---

**Q22.** In ProxyChains configuration, which mode uses proxies in a RANDOM
order for each connection — providing maximum unpredictability?

- A) `strict_chain`
- B) `dynamic_chain`
- C) `round_robin_chain`
- D) `random_chain`

---

**Q23.** What is HTTP Tunneling?

- A) A technique to speed up HTTP connections by compressing all web traffic
- B) Encapsulating non-HTTP protocol traffic inside HTTP requests to bypass
   firewalls that only permit port 80/443
- C) A method to block all non-HTTP traffic at the firewall level
- D) An encryption standard that replaces TLS for HTTP connections

---

**Q24.** DNS tunneling encodes data in DNS queries through port 53. Why is this
technique particularly dangerous for defenders?

- A) DNS traffic uses strong encryption that cannot be inspected
- B) DNS traffic is rarely inspected by security tools because it is considered
   essential infrastructure traffic
- C) DNS queries cannot be logged by any firewall or SIEM system
- D) DNS uses TCP exclusively, which makes it immune to packet inspection

---

**Q25.** Which of the following is a tool specifically designed for DNS tunneling?

- A) Burp Suite
- B) ProxyChains
- C) iodine
- D) Wireshark

---

**Q26.** Domain fronting abuses CDN infrastructure to hide C2 traffic. In this
technique, the TLS connection appears to go to a TRUSTED CDN domain, but the
actual HTTP Host header inside the encrypted connection routes traffic to:

- A) The CDN's administrative control panel
- B) A random legitimate website hosted on the same CDN
- C) The attacker's C2 server
- D) The target's internal network directly

---

**Q27.** Which NMAP flag is used for active OS fingerprinting — sending
specially crafted probes and matching responses against 5,700+ OS fingerprints?

- A) `-sV`
- B) `-sS`
- C) `-O`
- D) `-sn`

---

**Q28.** A SIEM analyst notices an internal host sending HTTP POST requests to
an unusual external domain at exactly 30-second intervals, with Base64-encoded
data in the request body. Each request uses the same User-Agent string. What
does this pattern MOST LIKELY indicate?

- A) A user browsing a slow-loading website with auto-refresh enabled
- B) A legitimate software update check running on schedule
- C) HTTP tunneling used for C2 communication — malware beaconing to an
   attacker's server
- D) A failed DNS resolution causing repeated HTTP retry attempts

---
&nbsp;

&nbsp;

&nbsp;

---

## Answers & Explanations

---

**Q1. Correct Answer: B) URG, ACK, PSH, RST, SYN, FIN** ✅

**Explanation:**
The six original TCP flags in their correct **bit-order** within the TCP header's
control field (bits 1 through 6) are:
**URG → ACK → PSH → RST → SYN → FIN**

This is the order as defined in **RFC 793**. The order matters because when reading
a raw TCP header or Wireshark capture, the flag bits appear in this exact sequence.

- **A)** — ❌ Starts with SYN — SYN is bit 5, not bit 1
- **B)** — ✅ URG (bit 1), ACK (bit 2), PSH (bit 3), RST (bit 4), SYN (bit 5),
  FIN (bit 6) — correct RFC 793 order
- **C)** — ❌ Starts with ACK — ACK is bit 2, not bit 1
- **D)** — ❌ Incorrect order throughout

---

**Q2. Correct Answer: B) SYN Flood Attack** ✅

**Explanation:**
A **SYN Flood Attack** is a Denial-of-Service attack where the attacker sends
thousands of SYN packets with **spoofed source IP addresses**. The target allocates
a Transmission Control Block (TCB) entry (~280 bytes of kernel memory) for each SYN
received and waits for the ACK that never comes. The connection table fills up and
legitimate users cannot establish new connections.

- **A) SYN Scan** — ❌ SYN scan is a reconnaissance technique that sends SYN packets
  to determine port state — it does NOT use spoofed IPs and does NOT aim to
  exhaust resources
- **B) SYN Flood** — ✅ DoS attack using mass spoofed SYN packets to exhaust
  connection resources
- **C) TCP Connect Scan** — ❌ Completes full handshakes for port scanning — not a DoS
- **D) XMAS Scan** — ❌ Sends FIN+PSH+URG for stealth port scanning — not a flood

---

**Q3. Correct Answer: C) Pass the data immediately to the application layer
without buffering** ✅

**Explanation:**
The **PSH (Push)** flag tells the receiving TCP stack: "Don't buffer this data in the
receive buffer — send it immediately to the application layer." Without PSH, TCP may
wait to accumulate data before passing it up. PSH is commonly set in interactive
applications like SSH and Telnet where each keystroke needs immediate delivery.

- **A)** — ❌ Resetting the connection is the RST flag's function
- **B)** — ❌ PSH does the OPPOSITE of buffering — it forces immediate delivery
- **C)** — ✅ PSH = push data to application immediately, skip buffering
- **D)** — ❌ Processing data out of order using the Urgent Pointer is the URG flag's
  function — PSH delivers in-order but immediately

---

**Q4. Correct Answer: C) The port is UNFILTERED — reachable through the firewall** ✅

**Explanation:**
An **ACK scan** does NOT determine whether a port is open or closed. It determines
**firewall rules** — whether the port is reachable through the firewall or blocked.

- If the target responds with **RST** → the ACK packet reached the target →
  port is **UNFILTERED** (firewall allows traffic through)
- If **no response** → the ACK was dropped before reaching target →
  port is **FILTERED** (firewall blocked it)

- **A)** — ❌ ACK scans do not reveal if a port is open — RST is sent to bare ACK
  regardless of whether a service is listening
- **B)** — ❌ RST to bare ACK does not indicate closed — it simply means the packet
  reached the host
- **C)** — ✅ RST response = packet reached the target = UNFILTERED by firewall
- **D)** — ❌ Filtered would produce NO response — the firewall dropped the ACK

---

**Q5. Correct Answer: B) Stateless firewalls assume bare ACK is part of an
established connection because they do not track connection state** ✅

**Explanation:**
**Stateless firewalls** inspect each packet individually with no memory of previous
packets. When they see a packet with the ACK flag set, they assume it's part of an
already-established TCP connection and allow it through — they have no way to verify
whether a matching SYN was ever seen.

**Stateful firewalls** maintain a connection state table. They track every SYN that
initiated a connection. If an ACK arrives with no matching SYN entry in the state
table, the stateful firewall drops it as invalid.

- **A)** — ❌ Reversed — stateful firewalls do more inspection, not stateless
- **B)** — ✅ Stateless has no state table → assumes ACK = established traffic
- **C)** — ❌ Stateful firewalls absolutely can distinguish ACK from SYN — that's
  their core function
- **D)** — ❌ Deep packet inspection is a Layer 7 capability — stateless firewalls
  operate at Layer 3/4 without DPI

---

**Q6. Correct Answer: C) 4 — FIN-ACK, ACK, FIN-ACK, ACK** ✅

**Explanation:**
TCP connection termination uses a **four-way handshake** because each side closes
independently:
1. **Client → FIN-ACK** — "I'm done sending data"
2. **Server → ACK** — "Acknowledged your FIN" (server may still send data)
3. **Server → FIN-ACK** — "I'm also done sending data"
4. **Client → ACK** — "Acknowledged. Connection fully closed."

Each side must explicitly signal it is finished, and each signal must be acknowledged.

- **A)** — ❌ Only 2 packets would not allow both sides to close independently
- **B)** — ❌ 3 packets is the connection ESTABLISHMENT handshake, not termination
- **C)** — ✅ 4 packets — each side sends FIN-ACK and receives ACK
- **D)** — ❌ 5 packets with RST is incorrect — RST is for abrupt termination, not
  part of the graceful four-way close

---

**Q7. Correct Answer: B) FIN closes gracefully allowing data to finish; RST
terminates immediately discarding all queued data** ✅

**Explanation:**
**FIN** = "I am finished sending data. Complete the four-way termination handshake."
Both sides have the opportunity to finish sending remaining data before the
connection closes.

**RST** = "Abort immediately. Discard all queued data. No response needed. No
negotiation." The connection is instantly torn down with no opportunity for pending
data to be delivered.

- **A)** — ❌ Both FIN and RST can be sent by either client or server
- **B)** — ✅ FIN = graceful close with data completion · RST = immediate abort
- **C)** — ❌ Neither RST nor FIN involves encryption — they are plain TCP control flags
- **D)** — ❌ Both FIN and RST can be sent multiple times in edge cases — this is not
  the distinguishing difference

---

**Q8. Correct Answer: B) 280 bytes** ✅

**Explanation:**
Every received SYN packet causes the target's TCP/IP stack to allocate a
**Transmission Control Block (TCB)** entry — a data structure storing the connection
state information. Each TCB consumes approximately **280 bytes** of kernel memory.
At 100,000 SYN packets per second (common in SYN flood attacks), that's approximately
28MB/sec of kernel memory consumption — which is why SYN flooding can exhaust
server resources and cause denial of service.

- **A) 28 bytes** — ❌ Too small — TCB must store sequence numbers, window sizes,
  timers, and socket info
- **B) 280 bytes** — ✅ Approximate TCB size per SYN connection entry
- **C) 2,800 bytes** — ❌ Too large — 10× the actual value
- **D) 28,000 bytes** — ❌ Far too large — would exhaust memory even faster

---

**Q9. Correct Answer: C) Banner Grabbing** ✅

**Explanation:**
**Banner Grabbing** is the technique of connecting to an open port and reading
the identification string (banner) that the service sends before any authentication.
`SSH-2.0-OpenSSH_7.4` is a classic SSH banner revealing the protocol version (2.0)
and software version (OpenSSH 7.4). Netcat (`nc`) is one of the primary tools for
active banner grabbing.

- **A) OS Fingerprinting** — ❌ OS fingerprinting determines the operating system,
  not the specific service software version
- **B) Vulnerability Scanning** — ❌ Vulnerability scanning checks against CVE
  databases — banner grabbing only reads the service identification
- **C) Banner Grabbing** — ✅ Reading the service's self-identification string
- **D) Port Scanning** — ❌ Port scanning determines if a port is open/closed/filtered
  — it doesn't read service identification strings

---

**Q10. Correct Answer: B) Almost every service broadcasts a banner — FTP (21),
SSH (22), SMTP (25), POP3 (110), IMAP (143), and more** ✅

**Explanation:**
Banner grabbing is NOT limited to HTTP. Almost every network service sends an
identification banner upon connection — many because their protocol specifications
(RFCs) mandate it. FTP RFC 959 and SMTP RFC 5321 both require a 220 greeting upon
connection. SSH always sends its protocol/version string. POP3 sends a `+OK` greeting.
Vendors include version info by default for troubleshooting, and most admins don't
remove it.

- **A)** — ❌ Banners are available on virtually every service type — not just HTTP
- **B)** — ✅ Correct — banners exist across FTP, SSH, SMTP, POP3, IMAP, HTTP, and more
- **C)** — ❌ Banners typically reveal software name, exact version, AND sometimes OS
- **D)** — ❌ No exploitation is needed — banners are freely sent before authentication

---

**Q11. Correct Answer: B) The Server header shows only "Apache" — without
version number or OS details** ✅

**Explanation:**
Apache's `ServerTokens` directive controls how much information appears in the
`Server:` HTTP header:
- `ServerTokens Full` → `Apache/2.4.41 (Ubuntu) OpenSSL/1.1.1 PHP/7.4`
- `ServerTokens Prod` → `Apache` (product name only — no version, no OS)

`ServerSignature Off` removes Apache version from error pages (404, 500, etc.).

Combined, these reduce the intelligence an attacker can extract from banner grabbing.

- **A)** — ❌ These directives control banner display — they do not stop Apache from
  serving pages
- **B)** — ✅ ServerTokens Prod shows only "Apache" — no version or OS details
- **C)** — ❌ TLS configuration is separate — these directives only affect headers
- **D)** — ❌ These directives modify the banner content — they don't block network
  connections

---

**Q12. Correct Answer: B) Passive Banner Grabbing** ✅

**Explanation:**
**Passive Banner Grabbing** extracts service information without directly connecting
to the target. Shodan continuously scans the public internet and indexes all service
banners in its database. When a tester queries Shodan, they're accessing Shodan's
pre-collected data — no packets are sent to the target. The target has no way of
knowing their banners were looked up.

- **A) Active** — ❌ Active banner grabbing requires direct connection to the target
  (Netcat, Telnet, NMAP -sV)
- **B) Passive** — ✅ Querying Shodan's database — no packets reach the target
- **C) Hybrid** — ❌ Not a standard classification in the active/passive model
- **D) Enumeration** — ❌ Enumeration extracts users, shares, and services via
  protocols like NetBIOS/SNMP — different from banner grabbing

---

**Q13. Correct Answer: B) Banner → CVE Mapping** ✅

**Explanation:**
**Banner → CVE Mapping** is the critical process where a tester:
1. Grabs a banner revealing exact software and version
2. Searches the NVD (National Vulnerability Database) or similar for that version
3. Finds specific CVE identifiers with CVSS scores
4. Determines if the vulnerability is exploitable on the target

This converts a simple banner string into an actionable attack path. In the case of
Apache 2.4.49 + CVE-2021-41773, this single mapping led to Remote Code Execution.

- **A) Port Scanning** — ❌ Port scanning identifies open ports — not vulnerabilities
- **B) Banner → CVE Mapping** — ✅ Mapping a banner to a specific vulnerability
- **C) OS Fingerprinting** — ❌ OS fingerprinting identifies the operating system
- **D) Proxy Chaining** — ❌ Proxy chaining is an anonymity technique — unrelated

---

**Q14. Correct Answer: B) 64** ✅

**Explanation:**
Default initial TTL values are a fundamental OS fingerprinting indicator:

| OS | Default TTL |
|---|---|
| **Linux** | **64** |
| **Windows** | **128** |
| **Cisco IOS** | **255** |
| macOS | 64 |
| FreeBSD | 64 |

Linux defaults to TTL=64 across virtually all distributions and kernel versions.

- **A) 32** — ❌ No modern OS uses 32 as default TTL
- **B) 64** — ✅ Linux default initial TTL
- **C) 128** — ❌ 128 is the Windows default
- **D) 255** — ❌ 255 is the Cisco IOS default

---

**Q15. Correct Answer: C) Windows** ✅

**Explanation:**
An initial TTL of **128** is the default for **Windows** operating systems. Since
TTL decrements by 1 at each router hop, observing TTL=128 means the packet was
captured with zero hops (same network segment) or the source system uses 128 as
its initial TTL — which is Windows.

- **A) Linux** — ❌ Linux default TTL = 64
- **B) Cisco IOS** — ❌ Cisco IOS default TTL = 255
- **C) Windows** — ✅ Windows default TTL = 128
- **D) macOS** — ❌ macOS default TTL = 64 (BSD-based)

---

**Q16. Correct Answer: A) Initial TTL=128 → Windows** ✅

**Explanation:**
The formula is: `Initial TTL = Observed TTL + Number of Hops`

Observed TTL = 118 · Estimated hops ≈ 10

118 + 10 = **128** → the initial TTL was 128 → **Windows**

If the initial TTL had been 64 (Linux), with 10 hops the observed TTL would be
64 - 10 = 54, not 118.

- **A)** — ✅ 118 + 10 = 128 → Windows
- **B)** — ❌ Initial TTL 64 with 10 hops would show TTL=54, not 118
- **C)** — ❌ Initial TTL 255 with 10 hops would show TTL=245, not 118
- **D)** — ❌ macOS uses initial TTL 64, not matching this calculation

---

**Q17. Correct Answer: B) Windows sends RST regardless of port state; Linux
silently drops on open ports and sends RST on closed ports (per RFC 793)** ✅

**Explanation:**
This is one of the most critical behavioral differences in OS fingerprinting:

- **Linux/Unix (RFC 793 compliant):** FIN/NULL/XMAS on OPEN port → **silently drops**.
  On CLOSED port → **sends RST**.
- **Windows (NOT RFC 793 compliant for these edge cases):** Sends **RST to ALL ports
  regardless** of whether they are open or closed.

This is why FIN, NULL, and XMAS scans do NOT work reliably on Windows — and why
this behavior itself is an OS fingerprinting indicator.

- **A)** — ❌ Windows does NOT silently drop — it sends RST for both open and closed
- **B)** — ✅ Windows = RST always · Linux = RFC 793 (drop on open, RST on closed)
- **C)** — ❌ Linux does NOT send RST on open ports — it silently drops per RFC 793
- **D)** — ❌ Windows never sends SYN-ACK to FIN/NULL/XMAS probes

---

**Q18. Correct Answer: C) p0f** ✅

**Explanation:**
**p0f** is the standard tool for **passive OS fingerprinting**. It operates by
analyzing TCP SYN characteristics (window size, TTL, DF bit, TCP options) of
traffic that ALREADY exists on the network — it sends ZERO packets. The target
cannot detect p0f because it generates no traffic. It is completely invisible.

- **A) NMAP -O** — ❌ NMAP -O is ACTIVE OS fingerprinting — it sends 16 specially
  crafted probes to the target, which is detectable
- **B) Nessus** — ❌ Nessus is a vulnerability scanner — not an OS fingerprinting tool
- **C) p0f** — ✅ Passive OS fingerprinting — observes existing traffic, sends nothing
- **D) Netcat** — ❌ Netcat is used for active banner grabbing — it connects to the
  target directly

---

**Q19. Correct Answer: C) ClientHello** ✅

**Explanation:**
**JA3 fingerprinting** creates a hash from specific fields in the TLS **ClientHello**
message — the very first message a client sends when initiating a TLS connection.
The fields hashed include: TLS version, accepted cipher suites, extensions, elliptic
curves, and elliptic curve point formats. Different browsers, operating systems, and
malware produce different JA3 hashes because their TLS library implementations differ.

- **A) ServerHello** — ❌ ServerHello is the server's response — JA3 fingerprints the
  CLIENT, not the server (JA3S fingerprints the server)
- **B) Certificate** — ❌ The Certificate message contains the server's X.509 cert —
  not used for JA3 fingerprinting
- **C) ClientHello** — ✅ JA3 hashes fields from the TLS ClientHello message
- **D) Finished** — ❌ The Finished message completes the handshake — too late in the
  process for fingerprinting purposes

---

**Q20. Correct Answer: D) SOCKS Proxy** ✅

**Explanation:**
**SOCKS (Socket Secure)** proxy operates at **Layer 5 (Session layer)** and is
**protocol-agnostic** — it can forward ANY type of TCP traffic (and UDP in SOCKS5).
This includes SSH, FTP, SMTP, DNS, and any other protocol — not just HTTP.

SOCKS4 supports TCP only with no authentication. SOCKS5 adds TCP+UDP support,
authentication, and IPv6 support.

- **A) HTTP Proxy** — ❌ HTTP proxy operates at Layer 7 (Application) and handles
  ONLY HTTP/HTTPS traffic
- **B) Transparent Proxy** — ❌ Transparent proxy intercepts traffic without client
  awareness — it is a deployment model, not a protocol type
- **C) Anonymous Proxy** — ❌ Anonymous proxy is a privacy level classification —
  it still only handles HTTP traffic
- **D) SOCKS Proxy** — ✅ Layer 5, protocol-agnostic, TCP+UDP (v5)

---

**Q21. Correct Answer: C) The IP of the LAST proxy (Brazil)** ✅

**Explanation:**
In a proxy chain, each proxy only knows the IP of the node immediately before it
and the node immediately after it. The target only receives traffic from the LAST
proxy in the chain:
Attacker (India) → Proxy 1 (USA) → Proxy 2 (Russia) → Proxy 3 (Brazil) → TARGET


The TARGET sees traffic from **Proxy 3 (Brazil)** — the last hop. It has no
knowledge of Proxy 1, Proxy 2, or the attacker's real IP.

- **A)** — ❌ The attacker's real IP is hidden — the whole point of proxy chaining
- **B)** — ❌ Only Proxy 1 sees the attacker's real IP — the target never sees Proxy 1
- **C)** — ✅ Target sees the LAST proxy in the chain only
- **D)** — ❌ Proxy chains use real proxy IPs — not randomly generated ones

---

**Q22. Correct Answer: D) `random_chain`** ✅

**Explanation:**
ProxyChains supports three routing modes:

| Mode | Behavior |
|---|---|
| `strict_chain` | Proxies used in exact listed order — all must be online |
| `dynamic_chain` | Skips dead proxies — uses whatever is alive, in order |
| `random_chain` | Proxies used in RANDOM order each connection — maximum unpredictability |

`random_chain` provides the highest unpredictability because each new connection
takes a different path through the proxy list.

- **A) `strict_chain`** — ❌ Fixed order — predictable and all proxies must be online
- **B) `dynamic_chain`** — ❌ Sequential but skips dead proxies — still ordered
- **C) `round_robin_chain`** — ❌ Not a standard ProxyChains mode
- **D) `random_chain`** — ✅ Random order per connection — maximum unpredictability

---

**Q23. Correct Answer: B) Encapsulating non-HTTP protocol traffic inside HTTP
requests to bypass firewalls that only permit port 80/443** ✅

**Explanation:**
**HTTP Tunneling** wraps non-HTTP traffic (SSH, RDP, C2 commands, exfiltrated data)
inside standard HTTP request/response messages. Corporate firewalls that only allow
outbound ports 80 (HTTP) and 443 (HTTPS) cannot distinguish the encapsulated traffic
from legitimate web browsing — the tunnel bypasses the firewall's port-based
filtering entirely.

- **A)** — ❌ HTTP tunneling is not about compression — it's about encapsulating
  different protocols inside HTTP
- **B)** — ✅ Encapsulating non-HTTP traffic in HTTP to bypass port-based firewalls
- **C)** — ❌ HTTP tunneling is used to BYPASS firewalls — not to block traffic
- **D)** — ❌ HTTP tunneling is a bypass technique — not an encryption standard

---

**Q24. Correct Answer: B) DNS traffic is rarely inspected by security tools
because it is considered essential infrastructure traffic** ✅

**Explanation:**
DNS (port 53) is considered essential infrastructure — every network application
needs DNS to function. Because of this, DNS is:
- Almost never blocked by firewalls (blocking DNS breaks everything)
- Rarely subjected to deep packet inspection
- Often overlooked in security monitoring

Attackers exploit this by encoding data into DNS query strings (e.g.,
`[base64_data].tunnel.attacker.com`). The OilRig APT group used DNS tunneling
for months undetected because the target organizations were not inspecting DNS
content.

- **A)** — ❌ Standard DNS is NOT encrypted (DNS-over-HTTPS/DNS-over-TLS exist but
  are not universal) — the issue is that DNS isn't INSPECTED, not that it can't be
- **B)** — ✅ DNS is rarely inspected because it's essential infrastructure — making
  it a blind spot
- **C)** — ❌ DNS queries absolutely CAN be logged by firewalls and SIEM — most
  organizations simply don't do it thoroughly
- **D)** — ❌ DNS primarily uses UDP (port 53) — not TCP exclusively

---

**Q25. Correct Answer: C) iodine** ✅

**Explanation:**
**iodine** is a purpose-built DNS tunneling tool that creates IP-over-DNS tunnels.
It encodes network traffic into DNS queries and responses, allowing full TCP/IP
connectivity through environments where only DNS traffic is permitted.

Other DNS tunneling tools include: **dnscat2** and **dns2tcp**.

- **A) Burp Suite** — ❌ Burp Suite is an HTTP intercepting proxy for web app testing
  — not DNS tunneling
- **B) ProxyChains** — ❌ ProxyChains routes traffic through SOCKS/HTTP proxy chains
  — not DNS tunnels
- **C) iodine** — ✅ Purpose-built DNS tunneling tool
- **D) Wireshark** — ❌ Wireshark is a packet capture and analysis tool — it can
  DETECT DNS tunneling but does not perform it

---

**Q26. Correct Answer: C) The attacker's C2 server** ✅

**Explanation:**
**Domain Fronting** exploits CDN infrastructure:
1. Malware establishes a TLS connection to a **legitimate CDN domain**
   (e.g., `legit-cdn.amazonaws.com`)
2. The firewall sees HTTPS traffic to a trusted CDN — allows it through
3. INSIDE the encrypted TLS tunnel, the HTTP **Host header** specifies
   `c2.attacker.com`
4. The CDN reads the Host header and forwards the request to the attacker's
   C2 server

The firewall cannot see the Host header because it's inside the encrypted TLS
connection.

- **A)** — ❌ The traffic does not route to CDN admin panels
- **B)** — ❌ The traffic is specifically directed by the Host header — not random
- **C)** — ✅ The Host header inside TLS routes traffic to the attacker's C2 server
- **D)** — ❌ Domain fronting routes through the CDN to the attacker — it does not
  provide direct internal network access

---

**Q27. Correct Answer: C) `-O`** ✅

**Explanation:**
`sudo nmap -O [target]` enables **active OS fingerprinting**. NMAP sends up to
16 specially crafted TCP, UDP, and ICMP probes to the target — analyzing responses
against its database of 5,700+ OS fingerprints. It requires root privileges
(raw packet crafting) and needs at least one OPEN and one CLOSED port for accurate
results.

- **A) `-sV`** — ❌ Service VERSION detection — identifies software on open ports,
  not the OS
- **B) `-sS`** — ❌ SYN scan — port scanning technique, not OS detection
- **C) `-O`** — ✅ OS fingerprinting — crafted probes matched against 5,700+ fingerprints
- **D) `-sn`** — ❌ Ping scan / host discovery — no port scanning or OS detection

---

**Q28. Correct Answer: C) HTTP tunneling used for C2 communication — malware
beaconing to an attacker's server** ✅

**Explanation:**
This pattern exhibits multiple indicators of HTTP tunneling C2:
1. **Regular intervals (30 seconds)** — legitimate browsing is irregular/human-paced;
   C2 beacons use precise, automated intervals
2. **Base64-encoded data in POST body** — legitimate web forms use readable parameters;
   C2 encodes commands and exfiltrated data in Base64
3. **Same User-Agent string every time** — malware uses a fixed UA; real browsers
   update their UA across sessions
4. **Single unusual external domain** — C2 traffic goes to one destination repeatedly

These indicators collectively represent classic C2 beaconing behavior — malware
checking in with its command server at regular intervals.

- **A)** — ❌ Auto-refresh would show variable content and normal HTML — not Base64
  POST data at precise 30-second intervals
- **B)** — ❌ Software updates are infrequent (hours/days apart) and use known update
  domains — not Base64 POST every 30 seconds to an unknown domain
- **C)** — ✅ All four indicators (timing, encoding, fixed UA, single domain) match
  classic C2 beaconing
- **D)** — ❌ DNS resolution failures would generate DNS traffic — not HTTP POST
  requests with encoded data

---

## Quick Answer Key

| Q | Answer | Q | Answer | Q | Answer |
|---|---|---|---|---|---|
| Q1 | B | Q11 | B | Q21 | C |
| Q2 | B | Q12 | B | Q22 | D |
| Q3 | C | Q13 | B | Q23 | B |
| Q4 | C | Q14 | B | Q24 | B |
| Q5 | B | Q15 | C | Q25 | C |
| Q6 | C | Q16 | A | Q26 | C |
| Q7 | B | Q17 | B | Q27 | C |
| Q8 | B | Q18 | C | Q28 | C |
| Q9 | C | Q19 | C | | |
| Q10 | B | Q20 | D | | |

---

## Topic Coverage Map

| Q | Section | Concept Tested |
|---|---|---|
| Q1 | Section 1 | TCP flags — correct bit-order (RFC 793) |
| Q2 | Section 1 | SYN flag — SYN Flood vs SYN Scan distinction |
| Q3 | Section 1 | PSH flag — push data to application immediately |
| Q4 | Section 1 | ACK scan — unfiltered vs filtered determination |
| Q5 | Section 1 | Stateless vs stateful firewalls — ACK handling |
| Q6 | Section 1 | TCP termination — four-way FIN handshake |
| Q7 | Section 1 | RST vs FIN — immediate vs graceful termination |
| Q8 | Section 1 | SYN resource allocation — TCB size (~280 bytes) |
| Q9 | Section 2 | Banner grabbing — definition and identification |
| Q10 | Section 2 | Banner grabbing — services that send banners |
| Q11 | Section 2 | Banner manipulation — Apache ServerTokens Prod |
| Q12 | Section 2 | Passive banner grabbing — Shodan |
| Q13 | Section 2 | Banner → CVE Mapping — process |
| Q14 | Section 3 | OS fingerprinting — Linux default TTL (64) |
| Q15 | Section 3 | OS fingerprinting — Windows default TTL (128) |
| Q16 | Section 3 | OS fingerprinting — TTL calculation with hops |
| Q17 | Section 3 | OS fingerprinting — Windows vs Linux RFC 793 behavior |
| Q18 | Section 3 | Passive OS fingerprinting — p0f tool |
| Q19 | Section 3 | JA3 fingerprinting — TLS ClientHello |
| Q20 | Section 4 | Proxy types — SOCKS proxy (Layer 5, protocol-agnostic) |
| Q21 | Section 4 | Proxy chaining — what target sees (last proxy IP) |
| Q22 | Section 4 | ProxyChains — random_chain mode |
| Q23 | Section 5 | HTTP tunneling — definition |
| Q24 | Section 5 | DNS tunneling — why it is dangerous |
| Q25 | Section 5 | DNS tunneling — iodine tool |
| Q26 | Section 7 | Domain fronting — CDN abuse for C2 |
| Q27 | Section 3 | NMAP -O — active OS fingerprinting flag |
| Q28 | Section 5 | HTTP tunneling detection — C2 beaconing indicators |

---