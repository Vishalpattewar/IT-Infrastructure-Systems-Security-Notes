# MCQ Set — Session 15: Sniffing, ARP Poisoning, MAC Flooding & DNS Attacks 🔍

> 28 MCQs · 4 options each · Full explanations · Covers core + extra notes

---

## 📑 Table of Contents

- [Questions 01–07 — Sniffing Fundamentals & Protocols](#questions-0107--sniffing-fundamentals--protocols)
- [Questions 08–14 — ARP Poisoning](#questions-0814--arp-poisoning)
- [Questions 15–19 — MAC Flooding](#questions-1519--mac-flooding)
- [Questions 20–24 — DNS Attacks](#questions-2024--dns-attacks)
- [Questions 25–28 — Wireshark & Extra Notes](#questions-2528--wireshark--extra-notes)
- [Answer Key](#answer-key)

---

## Questions 01–07 — Sniffing Fundamentals & Protocols

---

### Q01

**Which of the following MOST precisely defines the technical difference between passive sniffing and active sniffing?**

- A) Passive sniffing reads encrypted traffic; active sniffing reads only cleartext traffic
- B) Passive sniffing requires root privileges; active sniffing works without them
- C) ✅ Passive sniffing captures traffic without sending any packets and works on shared media; active sniffing sends forged packets to force traffic through the attacker on switched networks
- D) Passive sniffing only captures TCP traffic; active sniffing captures all protocols

**Explanation:**

- **A** is incorrect — neither passive nor active sniffing is defined by whether traffic is encrypted or cleartext. Encryption affects what the attacker can READ from captured traffic, not the sniffing mechanism itself.
- **B** is incorrect — both forms of sniffing typically require elevated privileges to place the NIC in promiscuous mode or to send forged packets. Privilege level is not the defining distinction.
- **C** ✅ is correct — passive sniffing places the NIC in promiscuous mode and captures all traffic on shared media (hubs, Wi-Fi) without generating any additional network packets — making it nearly undetectable. Active sniffing sends forged packets (ARP replies, random MAC frames) to manipulate network devices (ARP caches, switch CAM tables) so traffic flows through the attacker on switched networks where passive sniffing cannot work.
- **D** is incorrect — neither sniffing type is limited by protocol type. Both capture all traffic passing through the interface regardless of Layer 4 protocol.

---

### Q02

**A network administrator has replaced all hubs with managed switches throughout the office. An attacker still wants to sniff traffic between two workstations. Which statement is CORRECT?**

- A) The attacker cannot sniff traffic on a switched network under any circumstances
- B) The attacker can still use passive sniffing by placing the NIC in promiscuous mode
- C) Switches broadcast all traffic to all ports — passive sniffing still works
- D) ✅ The attacker must use active sniffing techniques such as ARP poisoning or MAC flooding to capture traffic on a switched network

**Explanation:**

- **A** is incorrect — switched networks prevent passive sniffing but do NOT make all sniffing impossible. Active sniffing techniques specifically exist to overcome this limitation.
- **B** is incorrect — placing the NIC in promiscuous mode on a switched network only allows the attacker to capture broadcast traffic and traffic specifically addressed to their own port. Traffic between two OTHER workstations on dedicated switch ports is NOT visible to them — promiscuous mode alone is insufficient.
- **C** is incorrect — this describes hub behaviour. Switches forward frames only to the specific port where the destination MAC is connected — they do NOT broadcast unicast traffic to all ports (except when the destination MAC is unknown in the CAM table).
- **D** ✅ is correct — on a switched network, the attacker must use active techniques. ARP poisoning manipulates the ARP caches of victim machines to redirect traffic through the attacker. MAC flooding overflows the switch CAM table, causing the switch to flood traffic to all ports like a hub — enabling passive capture.

---

### Q03

**Which of the following protocols exposes EVERY KEYSTROKE typed by the user — including passwords character by character — as separate cleartext TCP packets that can be captured by a sniffer?**

- A) FTP
- B) HTTP
- C) SNMP v2c
- D) ✅ Telnet

**Explanation:**

- **A** is incorrect — FTP does transmit credentials in cleartext and is vulnerable to sniffing, but it transmits data in larger chunks — not necessarily character by character in separate packets. Also, FTP credentials are sent during the login phase, not every keystroke of the session.
- **B** is incorrect — HTTP transmits form data, cookies, and content in cleartext, but it operates at the HTTP request/response level — not keystroke by keystroke in real time.
- **C** is incorrect — SNMP v1/v2c transmits community strings (passwords) in cleartext, but these are management protocol messages, not interactive session keystrokes.
- **D** ✅ is correct — Telnet is an interactive terminal protocol. Every single keystroke typed by the user — including each character of a password as it is typed — is transmitted as a separate TCP packet in cleartext. A sniffer can reconstruct the entire session keystroke by keystroke, including passwords typed character by character. This is why SSH was developed as a secure replacement.

---

### Q04

**SNMP v1 and v2c are vulnerable to sniffing because they transmit which element in cleartext in every packet?**

- A) The encryption key used for session management
- B) The full routing table of the managed device
- C) ✅ The community string, which functions as an authentication password
- D) The SNMP version negotiation header

**Explanation:**

- **A** is incorrect — SNMP v1/v2c do not use session-level encryption keys. There is no encryption in these versions — the community string IS the only authentication mechanism.
- **B** is incorrect — while routing tables can be retrieved via SNMP, the routing table itself is not embedded in every SNMP packet. It is retrieved via specific OID queries.
- **C** ✅ is correct — SNMP v1 and v2c use community strings as their sole authentication mechanism. The community string (typically "public" for read access, "private" for write access) is transmitted in plaintext in every single SNMP packet. A sniffer capturing SNMP traffic immediately obtains the community string — gaining full read (and potentially write) access to all SNMP-managed network devices. SNMPv3 was introduced with proper authentication (HMAC-MD5/SHA) and encryption (DES/AES).
- **D** is incorrect — version negotiation headers are not the authentication-sensitive element being transmitted in cleartext. The community string is.

---

### Q05

**An attacker is on a Wi-Fi network and wants to capture traffic between other wireless clients and the access point. Which NIC mode must the wireless adapter be placed in to capture raw 802.11 frames from all wireless clients — NOT just those addressed to the attacker's MAC?**

- A) Promiscuous mode
- B) ✅ Monitor mode
- C) Ad-hoc mode
- D) Infrastructure mode

**Explanation:**

- **A** is incorrect — promiscuous mode is a wired Ethernet concept. It causes the NIC to accept all Ethernet frames regardless of destination MAC. On wireless adapters, promiscuous mode still operates within the 802.11 association — it captures all frames within the BSS but requires association with the AP. Monitor mode is the correct wireless equivalent and is more powerful.
- **B** ✅ is correct — monitor mode (also called RFMON mode) places the wireless adapter in a state where it captures ALL 802.11 frames in radio range — including management frames (beacons, probe requests), control frames, and data frames from ALL wireless clients — without being associated with any access point. This is the wireless equivalent of promiscuous mode on wired networks and is used by tools like airodump-ng and Wireshark in wireless capture mode.
- **C** is incorrect — ad-hoc mode configures the wireless adapter for peer-to-peer wireless networking (no AP). It has nothing to do with capturing all wireless traffic from other clients.
- **D** is incorrect — infrastructure mode is the normal operating mode where the adapter connects to an access point. It only processes frames addressed to the adapter's own MAC (or broadcast) — the opposite of what is needed for sniffing.

---

### Q06

**A security auditor discovers that a legacy system is using a protocol where file transfer credentials are transmitted in cleartext on TCP port 21. Which protocol is this, and what is its secure replacement?**

- A) Telnet — replace with SSH on port 22
- B) HTTP — replace with HTTPS on port 443
- C) SMTP — replace with SMTPS on port 465
- D) ✅ FTP — replace with SFTP or SCP, both operating over SSH on port 22

**Explanation:**

- **A** is incorrect — Telnet operates on TCP port 23, not port 21. Telnet → SSH is a correct pairing but the port 21 identification is wrong.
- **B** is incorrect — HTTP operates on TCP port 80. HTTP → HTTPS is correct but port 21 is not HTTP.
- **C** is incorrect — SMTP operates on TCP port 25 (or 587 with STARTTLS). Port 21 is not SMTP.
- **D** ✅ is correct — FTP (File Transfer Protocol) uses TCP port 21 for the control channel and TCP port 20 for active data transfer. Both the control connection (including username and password) and the data connection are transmitted in cleartext. SFTP (SSH File Transfer Protocol) and SCP (Secure Copy) both run over SSH on TCP port 22, providing full encryption of authentication and data transfer. FTPS (FTP over TLS) on port 990 is another secure alternative.

---

### Q07

**Which of the following CORRECTLY describes what happens when a network interface card is placed in promiscuous mode?**

- A) The NIC encrypts all outgoing traffic to prevent sniffing by other devices
- B) The NIC only accepts traffic from devices with matching IP subnets
- C) The NIC stops all outgoing traffic and only processes incoming frames
- D) ✅ The NIC disables its MAC address filter and passes ALL received frames to the operating system — regardless of the destination MAC address

**Explanation:**

- **A** is incorrect — promiscuous mode has nothing to do with encrypting outgoing traffic. It is purely a receive-side configuration change affecting which frames are passed up to the OS.
- **B** is incorrect — the NIC operates at Layer 2 (MAC addresses), not Layer 3 (IP subnets). IP-level filtering is performed by the OS networking stack, not the NIC's promiscuous mode setting.
- **C** is incorrect — promiscuous mode does not affect outgoing traffic in any way. The NIC continues to transmit normally. Only the receive-side filtering behaviour changes.
- **D** ✅ is correct — normally, a NIC compares the destination MAC address of every received frame against its own MAC address and the broadcast address (FF:FF:FF:FF:FF:FF). Frames addressed to other MACs are discarded at the hardware level before the OS ever sees them. In promiscuous mode, this MAC address filtering is disabled — the NIC passes ALL received frames (regardless of destination MAC) to the operating system, allowing sniffing tools like Wireshark and tcpdump to capture all traffic on the segment.

---

## Questions 08–14 — ARP Poisoning

---

### Q08

**What fundamental design flaw in the ARP protocol makes ARP poisoning attacks possible?**

- A) ARP uses a weak 16-bit transaction ID that can be guessed by brute force
- B) ARP only operates at Layer 3 — it cannot verify Layer 2 MAC addresses
- C) ARP requires broadcast storms to resolve addresses — creating a DoS vulnerability
- D) ✅ ARP is stateless and unauthenticated — hosts accept and cache ARP replies even without sending a prior ARP request, with no verification of the sender's identity

**Explanation:**

- **A** is incorrect — 16-bit transaction ID guessing describes the DNS cache poisoning vulnerability (Kaminsky attack), not ARP. ARP does not use transaction IDs in the same way.
- **B** is incorrect — ARP specifically maps Layer 3 IP addresses to Layer 2 MAC addresses. The flaw is not about which layer it operates at but about its lack of authentication.
- **C** is incorrect — ARP uses targeted broadcast for requests and unicast for replies. ARP does not inherently create broadcast storms, and this is not the vulnerability exploited by ARP poisoning.
- **D** ✅ is correct — ARP was designed for efficiency in small, trusted networks — not for security. It is completely stateless: a host that receives an ARP reply updates its ARP cache immediately, whether or not it ever sent an ARP request for that IP. There is no authentication mechanism — no cryptographic signature, no challenge-response, no trusted third party. Any host on the segment can claim any IP→MAC mapping and all other hosts will believe it.

---

### Q09

**In an ARP poisoning MITM attack, why must the attacker poison BOTH the victim's ARP cache AND the gateway's ARP cache?**

- A) Poisoning both caches prevents the switch from detecting the attack
- B) Poisoning only the gateway is sufficient — victim traffic automatically follows
- C) ✅ Poisoning only the victim redirects outbound traffic to the attacker but return traffic from the gateway still goes directly to the victim — poisoning both ensures bidirectional traffic interception
- D) Poisoning both caches is required to prevent ARP cache timeout on the victim

**Explanation:**

- **A** is incorrect — switch-level detection is a separate concern. The reason for poisoning both is about traffic flow, not detection evasion.
- **B** is incorrect — poisoning only the gateway would redirect return traffic (from gateway to victim) through the attacker, but outbound traffic (from victim to gateway) would still go directly. Interception would be incomplete and asymmetric.
- **C** ✅ is correct — for a full bidirectional MITM position: the victim must believe the gateway's IP is at the attacker's MAC (so outbound traffic goes to attacker), AND the gateway must believe the victim's IP is at the attacker's MAC (so return traffic goes to attacker). Without both being poisoned, traffic flows asymmetrically — the attacker sees only one direction of the conversation, making interception incomplete and analysis difficult.
- **D** is incorrect — while ARP cache entries do expire, that is a maintenance concern (why the attacker must continuously re-send poisoned replies), not the reason for poisoning both endpoints.

---

### Q10

**An attacker runs arpspoof and successfully poisons the ARP caches of a victim and the default gateway. The victim immediately loses all internet connectivity. What critical step did the attacker most likely forget?**

- A) The attacker forgot to set the NIC to promiscuous mode
- B) The attacker forgot to poison the DNS server's ARP cache
- C) ✅ The attacker forgot to enable IP forwarding on the attacking machine
- D) The attacker forgot to run Wireshark before starting arpspoof

**Explanation:**

- **A** is incorrect — promiscuous mode affects what the attacker can capture, not whether victim connectivity is maintained. Even without promiscuous mode, the missing step causing loss of connectivity is different.
- **B** is incorrect — DNS cache poisoning is a separate attack. The immediate connectivity loss is caused by the traffic reaching the attacker's machine and not being forwarded — not by DNS.
- **C** ✅ is correct — when ARP poisoning redirects traffic to the attacker's machine, that machine becomes responsible for forwarding packets to their real destinations. By default, Linux and Windows do NOT forward IP packets between interfaces (IP forwarding is disabled). All packets arriving at the attacker's machine are dropped — the victim's traffic hits a black hole — causing complete connectivity loss. Enabling IP forwarding (`echo 1 > /proc/sys/net/ipv4/ip_forward` on Linux) makes the attack transparent — packets are forwarded to their real destinations while the attacker reads them.
- **D** is incorrect — Wireshark is the capture tool but has no effect on network connectivity. Not running Wireshark means the attacker misses the capture opportunity — it does not cause the victim to lose connectivity.

---

### Q11

**What is a gratuitous ARP, and how do attackers specifically abuse it for ARP poisoning?**

- A) A gratuitous ARP is an error message generated when an ARP request times out — attackers intercept these to learn active IP addresses
- B) ✅ A gratuitous ARP is an unsolicited ARP reply sent without any prior ARP request — attackers send forged gratuitous ARPs claiming a gateway IP is at the attacker's MAC to poison all hosts that receive it
- C) A gratuitous ARP is a special ARP packet used only during network device initialization — attackers cannot forge these without physical device access
- D) A gratuitous ARP is a broadcast ARP request used to detect duplicate IP addresses — attackers flood the network with them to cause ARP storms

**Explanation:**

- **A** is incorrect — gratuitous ARP is not an error message or timeout notification. It is a proactively sent announcement.
- **B** ✅ is correct — a gratuitous ARP is an ARP reply sent by a host to announce its own IP→MAC mapping without being asked. Legitimate uses include network announcements after boot, VM live migration updates, and duplicate IP detection. Attackers abuse the fact that hosts accept these unsolicited replies and update their ARP cache immediately — by sending a forged gratuitous ARP claiming "192.168.1.1 (gateway) is at [attacker's MAC]", all hosts that receive it update their ARP cache — poisoning the entire broadcast domain without needing to target each host individually.
- **C** is incorrect — gratuitous ARPs can be sent by any host at any time, not only during initialization. They are trivially forgeable using tools like arpspoof, Ettercap, or Scapy.
- **D** is incorrect — while gratuitous ARPs ARE used for duplicate IP detection (send gratuitous ARP for your own IP — if someone replies, there's a conflict), they are standard ARP replies, not special broadcast requests. Flooding them is not their normal abuse pattern.

---

### Q12

**Which Wireshark display filter correctly identifies ONLY gratuitous ARP packets — the specific packet type used in ARP poisoning attacks?**

- A) `arp.opcode == 1`
- B) `arp.opcode == 2`
- C) `eth.dst == ff:ff:ff:ff:ff:ff`
- D) ✅ `arp.isgratuitous == 1`

**Explanation:**

- **A** is incorrect — `arp.opcode == 1` filters ARP Requests (broadcast "who has IP X?"). Gratuitous ARPs are technically ARP Replies (opcode 2) or sometimes Requests where sender IP equals target IP — opcode 1 alone does not specifically identify gratuitous ARPs.
- **B** is incorrect — `arp.opcode == 2` filters ALL ARP Replies, including legitimate ones in response to ARP requests. This would include massive amounts of normal ARP traffic, not just gratuitous ARPs.
- **C** is incorrect — `eth.dst == ff:ff:ff:ff:ff:ff` filters all Ethernet broadcast frames — this includes all ARP requests plus DHCP broadcasts and many other broadcast protocols. Not specific to gratuitous ARP.
- **D** ✅ is correct — `arp.isgratuitous == 1` is Wireshark's specific display filter for gratuitous ARP packets. Wireshark identifies a gratuitous ARP when the sender IP address equals the target IP address in the ARP packet — the hallmark of an unsolicited self-announcement. An equivalent manual filter is `arp.src.proto_ipv4 == arp.dst.proto_ipv4`. This filter is the fastest way to spot ARP poisoning activity in a capture.

---

### Q13

**Which of the following is the MOST effective network-level countermeasure against ARP poisoning, and what prerequisite must be configured first?**

- A) Port Security — requires 802.1X authentication to be enabled first
- B) VLAN segmentation — requires private VLANs to be configured first
- C) ✅ Dynamic ARP Inspection (DAI) — requires DHCP Snooping to be enabled first
- D) MAC address filtering — requires static IP assignment to be configured first

**Explanation:**

- **A** is incorrect — Port Security limits the number of MAC addresses per port and is the primary countermeasure for MAC flooding, not ARP poisoning. Port Security does not validate ARP packet content. Its prerequisite is not 802.1X.
- **B** is incorrect — VLAN segmentation limits the broadcast domain (reducing the number of hosts affected by ARP poisoning) but does not prevent ARP poisoning within a VLAN. It is a risk reduction measure, not a direct prevention.
- **C** ✅ is correct — Dynamic ARP Inspection (DAI) is a Cisco IOS switch feature that inspects every ARP packet and validates the IP→MAC→port mapping against the DHCP Snooping binding table. ARP packets with IP→MAC mappings that do not match the binding table are dropped. DHCP Snooping MUST be enabled first — it builds and maintains the binding table of legitimate IP→MAC→switch port mappings that DAI uses as its ground truth.
- **D** is incorrect — static MAC address filtering is a form of port security but does not validate ARP packet content or IP→MAC mappings. It prevents unauthorized devices from connecting but does not stop an authorized device from sending forged ARP replies.

---

### Q14

**An attacker is in a MITM position via ARP poisoning and intercepts a victim's HTTPS connection to their bank. The attacker uses sslstrip to downgrade the connection. What does sslstrip do and what is the PRIMARY countermeasure?**

- A) sslstrip decrypts TLS using brute force — countermeasure is using longer TLS keys
- B) sslstrip breaks the TLS certificate chain — countermeasure is certificate pinning only
- C) sslstrip forges a valid TLS certificate — countermeasure is two-factor authentication
- D) ✅ sslstrip downgrades HTTPS to HTTP by rewriting redirect responses — the victim connects over cleartext HTTP while sslstrip maintains the HTTPS connection to the server — countermeasure is HSTS

**Explanation:**

- **A** is incorrect — sslstrip does not brute-force TLS encryption. Brute-forcing modern TLS is computationally infeasible. sslstrip works by preventing TLS from being established in the first place.
- **B** is incorrect — sslstrip does not break the certificate chain. It avoids TLS certificate validation entirely by preventing the client from ever establishing a TLS connection — serving HTTP to the client instead.
- **C** is incorrect — sslstrip does not forge TLS certificates. It eliminates the need for certificates on the client side by intercepting the HTTP→HTTPS redirect and serving the page over HTTP.
- **D** ✅ is correct — sslstrip works by intercepting the HTTP 301/302 redirect that tells the browser to use HTTPS. Instead of passing this redirect to the victim, sslstrip rewrites it to serve HTTP content — the victim's browser connects via HTTP (cleartext) while sslstrip maintains the legitimate HTTPS connection to the real server. The victim may not notice if they don't check the address bar carefully. HSTS (HTTP Strict Transport Security) is the primary countermeasure — it causes the browser to remember that a site must ALWAYS use HTTPS and refuse HTTP even if served it, defeating sslstrip.

---

## Questions 15–19 — MAC Flooding

---

### Q15

**What is the root cause vulnerability in network switches that MAC flooding attacks exploit?**

- A) Switches transmit all frames to all ports by default — similar to a hub
- B) Switches do not verify source MAC addresses — allowing any device to claim any MAC
- C) ✅ The switch CAM table has a finite memory capacity — when overflowed with random MAC entries, the switch cannot learn new legitimate entries and resorts to flooding unknown destination traffic to all ports
- D) Switches use cleartext management protocols — attackers inject false MAC entries via SNMP

**Explanation:**

- **A** is incorrect — this describes hub behaviour, not switch behaviour. Switches specifically exist to avoid broadcasting all frames to all ports. Flooding only occurs for frames with unknown destination MACs.
- **B** is incorrect — while switches do not cryptographically verify source MAC addresses (enabling MAC spoofing), this is not the specific vulnerability MAC flooding exploits. MAC flooding targets the CAM table capacity limit, not source MAC authentication.
- **C** ✅ is correct — the CAM (Content Addressable Memory) table has a finite size — typically 4,000–16,000 entries depending on switch model. The macof tool generates random source MAC addresses at extremely high rates (155,000+ frames per minute). When the CAM table fills completely, the switch cannot store new entries. Any frame with a destination MAC not already in the (overflowed) CAM table triggers unknown unicast flooding — the frame is sent to ALL ports — effectively making the switch behave like a hub for unknown destinations.
- **D** is incorrect — MAC flooding does not use SNMP to inject entries. It exploits CAM table overflow through high-rate frame injection on the physical network.

---

### Q16

**What is the PRIMARY and MOST DIRECT countermeasure for MAC flooding attacks on a managed switch?**

- A) Dynamic ARP Inspection (DAI)
- B) DNSSEC
- C) VLAN segmentation
- D) ✅ Port Security with a maximum MAC address limit per port and violation action set to shutdown

**Explanation:**

- **A** is incorrect — Dynamic ARP Inspection validates ARP packet content against the DHCP snooping binding table. It prevents ARP poisoning attacks. While useful, it does not directly limit the number of MAC addresses learned per port and does not prevent CAM table overflow.
- **B** is incorrect — DNSSEC is a DNS security extension for cryptographic signing of DNS records. It has no relevance to MAC flooding attacks at Layer 2.
- **C** is incorrect — VLAN segmentation limits the blast radius of a MAC flooding attack (the overflow only affects the flooded VLAN) but does not prevent the attack within a VLAN. It reduces impact rather than preventing the attack.
- **D** ✅ is correct — Port Security is the direct and primary countermeasure. Configuring a maximum of 1 or 2 MAC addresses per switch port means that when a MAC flooding tool attempts to register thousands of random MACs from a single port, the limit is immediately exceeded. The violation action "shutdown" disables the port immediately — neutralizing the attack within milliseconds. The "restrict" mode drops excess MAC frames and logs violations. The "protect" mode drops excess MAC frames silently. "Shutdown" is the most effective for active attack prevention.

---

### Q17

**The macof tool is used in MAC flooding attacks. Which toolkit does macof belong to, and what is its specific mechanism of attack?**

- A) Metasploit framework — macof sends crafted TCP SYN packets to overflow the switch routing table
- B) Aircrack-ng suite — macof floods wireless channels with deauthentication frames
- C) ✅ dsniff suite — macof generates Ethernet frames with random source and destination MAC addresses at extremely high rates to overflow the switch CAM table
- D) Nmap — macof sends ICMP probes with random MAC addresses to discover active hosts

**Explanation:**

- **A** is incorrect — macof is not part of Metasploit. It does not send TCP SYN packets and does not target routing tables — it targets the switch CAM table using Ethernet frames.
- **B** is incorrect — macof is not part of Aircrack-ng and has nothing to do with wireless deauthentication attacks.
- **C** ✅ is correct — macof is part of the **dsniff** suite developed by Dug Song. It generates Ethernet frames with completely random source MAC addresses and random destination MAC addresses at line rate (155,000+ frames per minute is commonly cited). Each frame causes the switch to attempt to add a new entry to its CAM table — mapping the random source MAC to the attacker's port. The table fills within seconds, triggering the unknown unicast flooding behaviour that enables sniffing.
- **D** is incorrect — macof is not part of Nmap and does not send ICMP probes. Nmap is a port scanner and host discovery tool — completely different purpose.

---

### Q18

**After a successful MAC flooding attack overflows a switch's CAM table, what SPECIFIC behaviour change occurs in the switch that enables the attacker to sniff traffic?**

- A) The switch begins dropping all packets — creating a denial of service
- B) The switch sends all frames directly to the attacker's MAC address
- C) The switch disables all port security and broadcasts its ARP cache
- D) ✅ The switch floods all frames with unknown destination MACs to ALL ports — including the attacker's port — making the switch behave like a hub for those destinations

**Explanation:**

- **A** is incorrect — the switch does not drop all packets. The flooding behaviour maintains connectivity for existing CAM table entries — only new/unknown destinations are flooded rather than dropped.
- **B** is incorrect — the switch does not specifically target the attacker's MAC. The flooding is indiscriminate — all frames for unknown destinations go to ALL ports simultaneously.
- **C** is incorrect — the switch does not broadcast its ARP cache (switches don't maintain ARP caches — that's a host-level function). Port security violations may trigger other actions, but broadcasting an ARP cache is not the switch's flooding behaviour.
- **D** ✅ is correct — this is the precise technical behaviour: when a frame arrives with a destination MAC address not found in the CAM table (because the table is full and cannot store legitimate entries), the switch applies its unknown unicast flooding policy — forwarding the frame out ALL ports except the incoming port. The attacker's NIC in promiscuous mode receives these flooded frames — capturing traffic that was previously isolated to specific ports. Existing CAM table entries still forward normally; only frames for unknown destinations are flooded.

---

### Q19

**A network engineer runs the following command on a Cisco switch interface. What does it accomplish and what attack does it specifically prevent?**

    switchport port-security maximum 2
    switchport port-security violation shutdown

- A) It limits the switch to 2 VLANs per port — preventing VLAN hopping attacks
- B) It allows only 2 simultaneous TCP connections per port — preventing SYN flood attacks
- C) ✅ It limits the number of MAC addresses learned on the port to 2 and shuts the port down if more than 2 MACs are detected — directly preventing MAC flooding attacks
- D) It limits the port to 2 Mbps bandwidth — preventing bandwidth exhaustion attacks

**Explanation:**

- **A** is incorrect — VLAN limits are configured with `switchport trunk allowed vlan` and similar commands, not `port-security maximum`. This command counts MAC addresses, not VLANs.
- **B** is incorrect — TCP connection limits are managed by the OS or firewall at Layer 4. Switch port security operates at Layer 2 (MAC addresses) — it has no concept of TCP connections.
- **C** ✅ is correct — `switchport port-security maximum 2` tells the switch to learn and allow a maximum of 2 MAC addresses on this port. `switchport port-security violation shutdown` configures the switch to administratively shut down the port (err-disabled state) if a third MAC address is detected. Since macof generates thousands of random MAC addresses per second, the 3rd random MAC triggers immediate port shutdown — completely neutralizing the MAC flooding attack.
- **D** is incorrect — bandwidth limitations are configured with QoS policies and police/shape commands, not port-security. Port security counts MAC addresses, not bandwidth.

---

## Questions 20–24 — DNS Attacks

---

### Q20

**What is the critical technical difference between DNS spoofing targeting a single victim and DNS cache poisoning targeting a DNS resolver?**

- A) DNS spoofing uses UDP; DNS cache poisoning uses TCP — making it harder to filter
- B) DNS spoofing requires physical access to the network; DNS cache poisoning works remotely
- C) DNS spoofing modifies the victim's hosts file; DNS cache poisoning modifies the victim's ARP cache
- D) ✅ DNS spoofing forges replies to a single victim's query in real time; DNS cache poisoning injects false records into a recursive resolver's cache — redirecting ALL users of that resolver for the TTL duration

**Explanation:**

- **A** is incorrect — both DNS spoofing and cache poisoning primarily use UDP port 53. The protocol used is not the defining distinction between these two attacks.
- **B** is incorrect — DNS spoofing in a MITM context requires local network position (usually via ARP poisoning), but DNS cache poisoning can be attempted remotely against a resolver without local network access.
- **C** is incorrect — DNS spoofing does not modify the hosts file (that is a local file modification attack by malware). DNS cache poisoning does not touch the ARP cache (that is ARP poisoning).
- **D** ✅ is correct — DNS spoofing (in MITM context) intercepts and forges a DNS response to a SINGLE victim's query in real time — one victim is redirected. DNS cache poisoning injects a malicious record into a RECURSIVE RESOLVER's cache — every user who queries that resolver for the poisoned hostname receives the attacker's IP until the TTL expires. One successful cache poisoning can redirect thousands or millions of users of a major ISP resolver.

---

### Q21

**A penetration tester runs the following command and receives a dump of all DNS records for a domain:**

    dig axfr @ns1.target.com target.com

**What attack technique is being demonstrated and what is the security risk?**

- A) DNS cache poisoning — the tester is injecting false records into the resolver
- B) DNS amplification — the tester is using the DNS server as a DDoS amplifier
- C) ✅ DNS zone transfer (AXFR) abuse — the tester is retrieving the complete DNS zone, exposing all subdomains, IP addresses, and internal network topology
- D) DNS tunneling — the tester is encoding data inside DNS queries to bypass firewalls

**Explanation:**

- **A** is incorrect — AXFR requests retrieve existing DNS records — they do not inject false records into a resolver's cache.
- **B** is incorrect — DNS amplification uses small queries to generate large responses directed at a victim's IP address. AXFR is a zone transfer between authoritative servers, not an amplification technique.
- **C** ✅ is correct — AXFR (Authoritative Zone Transfer) is a DNS mechanism for transferring complete zone data from a primary nameserver to secondary nameservers. When improperly configured to allow requests from any IP, an attacker can retrieve all DNS records for the domain — including all A records, MX records, CNAME records, and critically all subdomains and their IP addresses. This provides a complete map of the target's network infrastructure — highly valuable reconnaissance. Zone transfers should be restricted to trusted secondary nameserver IPs only.
- **D** is incorrect — DNS tunneling encodes data inside DNS query subdomains and response TXT/CNAME records for C2 communication or exfiltration. It is not related to AXFR zone transfers.

---

### Q22

**Dan Kaminsky's 2008 DNS cache poisoning attack was significantly more dangerous than previous DNS poisoning techniques because:**

- A) It used TCP instead of UDP — bypassing all existing firewall rules for DNS
- B) It exploited a buffer overflow in all DNS resolver implementations simultaneously
- C) It required the attacker to be on the same network segment as the DNS resolver
- D) ✅ It poisoned the zone's NS (nameserver) record rather than a single hostname — giving the attacker control over ALL DNS resolution for an entire domain, and it forced rapid queries to exploit the 16-bit transaction ID space efficiently

**Explanation:**

- **A** is incorrect — the Kaminsky attack used UDP (standard DNS). Its innovation was in the attack methodology — not the transport protocol.
- **B** is incorrect — it was not a buffer overflow vulnerability. It was a protocol-level design flaw in the 16-bit transaction ID space combined with a novel zone-level poisoning technique.
- **C** is incorrect — one of the properties that made Kaminsky's attack so concerning was that it could be conducted remotely — the attacker did not need local network access to the resolver.
- **D** ✅ is correct — Kaminsky's key innovation was two-fold: (1) instead of targeting a specific hostname, he forced the resolver to make many queries for random subdomains of the target domain — generating many poisoning opportunities rapidly. (2) The forged responses included not just the A record for the random subdomain but the NS record for the entire zone — so a single successful poisoning gave the attacker control over ALL DNS resolution for the target domain. The fix required source port randomization, which combined with the 16-bit transaction ID creates ~4 billion possible combinations instead of just 65,536.

---

### Q23

**DNS tunneling tools like dnscat2 and Iodine are primarily used for which malicious purpose, and why is this technique effective at bypassing security controls?**

- A) Performing DNS cache poisoning attacks at high speed by tunneling through firewalls
- B) Amplifying DDoS traffic by tunneling attack traffic through legitimate DNS resolvers
- C) ✅ Establishing covert C2 channels and exfiltrating data by encoding information inside DNS queries and responses — which typically bypass firewalls that allow unrestricted DNS egress traffic
- D) Cracking DNS server authentication by tunneling brute-force attempts through legitimate-looking DNS traffic

**Explanation:**

- **A** is incorrect — DNS tunneling is not used for cache poisoning. They are separate attack categories. DNS tunneling is about encoding non-DNS data inside DNS protocol messages.
- **B** is incorrect — DNS amplification DDoS uses open DNS resolvers as amplifiers, sending small queries with spoofed source IPs. DNS tunneling encodes data within DNS — completely different mechanism and purpose.
- **C** ✅ is correct — DNS tunneling encodes arbitrary data (C2 commands, exfiltrated data, VPN traffic) inside DNS query subdomains and DNS response records (TXT, CNAME, NULL records). For example, `c2command_base64encoded.attacker.com` carries a C2 command in the subdomain. This bypasses firewalls because most organizations allow unrestricted outbound DNS traffic (UDP port 53) to enable normal internet browsing. Blocking DNS entirely breaks internet access. Detection requires DNS traffic analysis for anomalies (high query volume, long subdomain names, unusual record types, high entropy subdomains).
- **D** is incorrect — DNS tunneling is not used for credential brute-forcing. Authentication cracking uses completely different tools and protocols.

---

### Q24

**Which combination of DNS security mechanisms provides the MOST comprehensive protection against DNS cache poisoning AND DNS query interception?**

- A) AXFR restriction + DNS rate limiting
- B) Short TTL values + DNS load balancing
- C) Disabling recursive DNS + split DNS architecture
- D) ✅ DNSSEC (cryptographic record signing) + DNS over HTTPS or DNS over TLS (encrypted query transport)

**Explanation:**

- **A** is incorrect — AXFR restriction prevents unauthorized zone transfers (reconnaissance). DNS rate limiting mitigates amplification DDoS. Neither prevents cache poisoning of resolver caches or query interception by on-path attackers.
- **B** is incorrect — short TTLs reduce the window during which poisoned records remain cached but do not prevent poisoning. DNS load balancing is a reliability mechanism with no security benefit against poisoning or interception.
- **C** is incorrect — disabling recursion on authoritative servers prevents them from being used for amplification but does not protect recursive resolvers (which users actually query) from poisoning. Split DNS separates internal and external DNS views but doesn't prevent cache poisoning or query interception.
- **D** ✅ is correct — DNSSEC adds cryptographic signatures to all DNS records. Any tampering with signed records is detected by the resolver — preventing cache poisoning of DNSSEC-signed zones. DoH (DNS over HTTPS, port 443) and DoT (DNS over TLS, port 853) encrypt DNS queries between client and resolver — preventing on-path attackers from reading or forging DNS responses in transit. Together they address both cache poisoning (DNSSEC) and query interception (DoH/DoT) — the two primary DNS attack categories.

---

## Questions 25–28 — Wireshark & Extra Notes

---

### Q25

**What is the critical operational difference between a Wireshark capture filter and a display filter — and what happens to packets that do NOT match each type?**

- A) Capture filters use Wireshark syntax; display filters use BPF syntax — both permanently delete non-matching packets
- B) ✅ Capture filters (BPF syntax) are applied before capture — non-matching packets are never recorded; display filters (Wireshark syntax) are applied to existing captures — non-matching packets are hidden but remain in the capture file
- C) Capture filters only work on wired interfaces; display filters work on both wired and wireless
- D) Capture filters are applied after capture for performance optimization; display filters are applied during capture for real-time analysis

**Explanation:**

- **A** is incorrect — the syntax assignment is reversed (capture filters use BPF; display filters use Wireshark's own language), and critically, display filters do NOT delete packets — they only hide them from view.
- **B** ✅ is correct — capture filters use **BPF (Berkeley Packet Filter)** syntax (same as tcpdump) and are configured before starting capture. Packets that do not match are never written to memory or disk — they are discarded at the capture engine level. This reduces capture file size and focuses collection. Display filters use **Wireshark's own filter language** and are applied to already-captured traffic. Non-matching packets are hidden from the packet list view but remain fully in the capture file — they can be revealed by removing or changing the display filter. This is a frequently tested distinction.
- **C** is incorrect — both filter types work with any interface type that Wireshark supports, including wired, wireless, USB, and virtual interfaces.
- **D** is the exact reversal of the correct answer — capture filters are set BEFORE capture; display filters are applied AFTER capture.

---

### Q26

**A security analyst wants to investigate a captured session and find all HTTP POST requests that contain the string "password" in their payload. Which Wireshark display filter correctly identifies these packets?**

- A) `tcp.port == 80 and payload contains "password"`
- B) `http.method == POST and frame contains password`
- C) ✅ `http.request.method == "POST" and http contains "password"`
- D) `port 80 and http contains "password"`

**Explanation:**

- **A** is incorrect — `payload` is not a valid Wireshark display filter field. The correct field for content searching is the protocol name followed by `contains`. Also, BPF-style `port 80` syntax works in capture filters, not display filters.
- **B** is incorrect — `http.method` is not the correct Wireshark field name. The correct field is `http.request.method`. Also, `frame contains password` searches all bytes in the frame which is overly broad, and `password` without quotes may not work correctly in all Wireshark versions.
- **C** ✅ is correct — `http.request.method == "POST"` correctly filters for HTTP POST requests using Wireshark's display filter field notation. `http contains "password"` searches within the HTTP protocol layer for the string "password" in any field or payload. Combining with `and` gives precisely HTTP POST requests containing the password string — useful for credential extraction from captured traffic.
- **D** is incorrect — `port 80` is BPF capture filter syntax — it does not work as a Wireshark display filter. The correct Wireshark display filter equivalent would be `tcp.port == 80`.

---

### Q27

**The tool Antisniff was developed specifically for which purpose, and which technique does it use to identify machines running in promiscuous mode?**

- A) Antisniff prevents ARP poisoning by detecting forged ARP replies on the network segment
- B) Antisniff blocks MAC flooding by monitoring CAM table utilization on managed switches
- C) ✅ Antisniff detects machines running in promiscuous mode by sending probe packets with incorrect destination MACs and monitoring for responses — normal NICs discard such frames at hardware level but promiscuous NICs pass them to the OS which may respond
- D) Antisniff prevents DNS cache poisoning by monitoring resolver transaction IDs for anomalies

**Explanation:**

- **A** is incorrect — Antisniff is specifically a promiscuous mode detection tool, not an ARP poisoning prevention tool. ARP monitoring is done by Arpwatch, XArp, and DAI.
- **B** is incorrect — CAM table monitoring is a function of switch management interfaces (SNMP monitoring, syslog alerts for port security violations), not Antisniff.
- **C** ✅ is correct — Antisniff was developed by L0pht Heavy Industries (L0pht Research) specifically to detect sniffers on a network segment. Its primary technique involves sending packets with incorrect/non-existent destination MAC addresses but valid IP addresses to potential sniffer machines. A normal NIC discards frames at the hardware level when the destination MAC doesn't match — the OS never sees the packet and cannot respond. A NIC in promiscuous mode passes ALL frames to the OS regardless of MAC — if the OS processes the packet and sends a response (e.g., ICMP reply), Antisniff detects this anomalous response and identifies the machine as running in promiscuous mode.
- **D** is incorrect — DNS transaction ID monitoring for cache poisoning anomalies is a DNS server/resolver function, not what Antisniff does.

---

### Q28

**Which statement CORRECTLY describes the ARP protocol's layer classification and the security implication of its position in the network stack?**

- A) ARP is a pure Layer 3 protocol — it is fully protected by IP-layer security mechanisms like IPSec
- B) ARP is a pure Layer 2 protocol — it is only used within a single subnet and cannot cross routers
- C) ARP is a Layer 4 protocol — it operates above IP and can be filtered by stateful firewalls
- D) ✅ ARP operates between Layer 2 and Layer 3 — it maps Layer 3 IP addresses to Layer 2 MAC addresses; because it operates below IP, it is not protected by IP-level security mechanisms like IPSec, making it vulnerable to poisoning attacks that IPSec cannot prevent

**Explanation:**

- **A** is incorrect — ARP is NOT protected by IPSec. IPSec operates at Layer 3 (IP level) and above. ARP operates BELOW IP — it is used to build the Ethernet frames that carry IP packets. ARP poisoning redirects traffic before IP-level security can apply. IPSec can prevent an attacker from READING the content of intercepted packets but cannot prevent the traffic from being redirected via ARP poisoning in the first place.
- **B** is incorrect — while ARP does operate within a single subnet (it is a broadcast-based protocol limited by router boundaries), saying it is a "pure Layer 2 protocol" oversimplifies its role. ARP's defining function is BRIDGING Layer 2 and Layer 3 — it exists specifically to map between the two address spaces.
- **C** is incorrect — ARP operates BELOW IP (Layer 3), not above it. Layer 4 protocols (TCP, UDP) are above IP. Stateful firewalls operate at Layer 3 and above — they cannot inspect or filter ARP poisoning attacks at Layer 2.
- **D** ✅ is correct — ARP is accurately classified as Layer 2.5 (or operating at the boundary between Layer 2 and Layer 3). Its function is to resolve Layer 3 IP addresses into Layer 2 MAC addresses so that Ethernet frames can be properly addressed. Because it operates below the IP layer, security mechanisms that operate at or above IP (IPSec, TLS, VPN tunnels) cannot prevent ARP poisoning — they can only protect the content of traffic that is redirected, not prevent the redirection itself. This is why Layer 2 countermeasures (DAI, static ARP) are required.

---

## Answer Key

| Q# | Answer | Topic Area |
|---|---|---|
| Q01 | C | Passive vs Active sniffing — core distinction |
| Q02 | D | Active sniffing necessity on switched networks |
| Q03 | D | Telnet — keystroke-level cleartext exposure |
| Q04 | C | SNMP v1/v2c — community string cleartext |
| Q05 | B | Monitor mode vs promiscuous mode — wireless |
| Q06 | D | FTP port 21 — SFTP/SCP as secure replacement |
| Q07 | D | Promiscuous mode — NIC MAC filter bypass |
| Q08 | D | ARP stateless + unauthenticated design flaw |
| Q09 | C | ARP poisoning — bidirectional poisoning requirement |
| Q10 | C | IP forwarding — attacker must enable for transparent MITM |
| Q11 | B | Gratuitous ARP — definition and attacker abuse |
| Q12 | D | Wireshark display filter for gratuitous ARP |
| Q13 | C | DAI — primary ARP poisoning countermeasure + DHCP Snooping prerequisite |
| Q14 | D | sslstrip mechanism and HSTS countermeasure |
| Q15 | C | CAM table finite capacity — MAC flooding root cause |
| Q16 | D | Port Security — primary MAC flooding countermeasure |
| Q17 | C | macof — dsniff suite — random MAC flooding mechanism |
| Q18 | D | Switch behaviour after CAM overflow — unknown unicast flooding |
| Q19 | C | Port Security command — MAC limit + violation shutdown |
| Q20 | D | DNS spoofing vs DNS cache poisoning — scope difference |
| Q21 | C | AXFR zone transfer abuse — reconnaissance |
| Q22 | D | Kaminsky attack — zone-level NS poisoning |
| Q23 | C | DNS tunneling — C2/exfil via DNS — firewall bypass |
| Q24 | D | DNSSEC + DoH/DoT — comprehensive DNS protection |
| Q25 | B | Capture filter (BPF) vs display filter (Wireshark) distinction |
| Q26 | C | Wireshark display filter — HTTP POST + password string |
| Q27 | C | Antisniff — promiscuous mode detection tool and technique |
| Q28 | D | ARP layer classification — Layer 2.5 — IPSec limitation |

---