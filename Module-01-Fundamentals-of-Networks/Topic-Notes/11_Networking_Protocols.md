# Networking Protocols
## Module: Fundamentals of Networks

---

## 1. Introduction

A **networking protocol** is a standardized set of rules that defines how data is formatted, transmitted, received, and acknowledged between devices on a network. Protocols ensure that different devices — regardless of manufacturer, operating system, or hardware — can communicate reliably and predictably.

### The Exact Problem It Solves
Without protocols, two devices would have no agreed-upon language for communication. One device might send data in chunks of 512 bytes while another expects 1024; one might use error-checking while another does not. Protocols solve this by pre-defining every aspect of communication: packet structure, addressing, sequencing, error detection, flow control, and session management — so that any compliant device can exchange data with any other.

### Where It Fits in the OSI and TCP/IP Models
Networking protocols operate across **multiple layers** of the OSI model, each protocol serving the function of its respective layer:

| OSI Layer | Layer Name | Example Protocols |
|-----------|-----------|------------------|
| 7 | Application | HTTP, HTTPS, FTP, SMTP, DNS, DHCP, SNMP, Telnet, SSH |
| 6 | Presentation | SSL/TLS, JPEG, MPEG, ASCII |
| 5 | Session | NetBIOS, RPC, PPTP |
| 4 | Transport | TCP, UDP |
| 3 | Network | IP, ICMP, OSPF, EIGRP, ARP (debate: Layer 2/3) |
| 2 | Data Link | Ethernet (802.3), PPP, HDLC, Frame Relay |
| 1 | Physical | RS-232, 802.11 (physical), DSL |

In the **TCP/IP model**, most application protocols sit at the **Application layer**, while TCP and UDP sit at the **Transport layer**, and IP at the **Internet layer**.

### Why This Topic Is Foundational
- Every network service — web browsing, email, file transfer, name resolution, remote access — depends on a specific protocol.
- Understanding protocols means understanding **how the internet actually works** at every level.
- **Port numbers** are how a single IP address can run dozens of services simultaneously; knowing them is essential for firewall configuration, network troubleshooting, and security.
- Protocol knowledge underpins ACL (Access Control List) writing, packet capture analysis, and network design.

---

## 2. Core Concepts & Detailed Explanation

### 2.1 What Is a Port Number?
A **port number** is a 16-bit integer (0–65535) that identifies a specific **process or service** running on a device. While an IP address identifies the device, the port number identifies the application on that device. Together, an IP address and port number form a **socket** (e.g., 192.168.1.1:80).

When a web browser connects to a web server:
- The **destination port** is **80** (HTTP) — telling the server "this is a web request."
- The **source port** is an **ephemeral port** (randomly chosen from 1024–65535 by the client OS) — used to track the specific connection session.

### 2.2 Port Number Ranges

| Range | Name | Description |
|-------|------|-------------|
| **0 – 1023** | Well-Known Ports (System Ports) | Assigned by IANA; reserved for standard, widely-used services |
| **1024 – 49151** | Registered Ports | Registered by IANA for specific applications; less strictly controlled |
| **49152 – 65535** | Dynamic / Private / Ephemeral Ports | Used by client OSes as temporary source ports for outbound connections |

> Defined and maintained by **IANA (Internet Assigned Numbers Authority)** per **RFC 6335**.

### 2.3 TCP vs. UDP — The Two Transport Protocols
Every application protocol runs on top of either **TCP** or **UDP** at the Transport layer (OSI Layer 4). Understanding which one each protocol uses is critical.

**TCP (Transmission Control Protocol):**
- **Connection-oriented**: Establishes a connection via the **3-way handshake** (SYN → SYN-ACK → ACK) before data transfer.
- **Reliable**: Guarantees delivery using acknowledgments (ACKs), sequence numbers, and retransmission of lost packets.
- **Ordered**: Data arrives in the correct sequence.
- **Flow control**: Uses sliding window to prevent overwhelming the receiver.
- **Overhead**: Higher (connection setup, acknowledgment traffic).
- **Best for**: Applications where data integrity matters — web, email, file transfer.

**UDP (User Datagram Protocol):**
- **Connectionless**: No handshake; data is sent immediately.
- **Unreliable**: No guarantee of delivery, ordering, or duplicate prevention.
- **Low overhead**: Minimal header (8 bytes vs. TCP's 20 bytes).
- **Best for**: Applications where speed matters more than reliability — DNS queries, video streaming, VoIP, online gaming, DHCP.

### 2.4 How Port Numbers Enable Multiplexing
A single server with one IP address can simultaneously serve hundreds of clients across multiple services because each service listens on a **different port**:

```
Client A → 192.168.1.100:80   (HTTP web request)
Client B → 192.168.1.100:443  (HTTPS web request)
Client C → 192.168.1.100:25   (SMTP email)
Client D → 192.168.1.100:22   (SSH admin session)
```

The server's OS uses the destination port to deliver each incoming packet to the correct application process.

### 2.5 Protocol Data Units (PDUs) at the Transport Layer
- TCP sends data as **segments**.
- UDP sends data as **datagrams**.
- At Layer 3 (IP), these become **packets**.
- At Layer 2 (Ethernet), these become **frames**.

### 2.6 RFC Standards
Every major protocol is defined in a **Request for Comments (RFC)** document published by the **IETF (Internet Engineering Task Force)**. RFCs are the authoritative specifications for all internet protocols.

---

## 3. Key Components / Types / Categories

### 3.1 Application Layer Protocols — Full Reference

#### Web Protocols

| Protocol | Full Name | Port(s) | Transport | RFC | Description |
|----------|-----------|---------|-----------|-----|-------------|
| **HTTP** | HyperText Transfer Protocol | 80 | TCP | RFC 2616 / 9110 | Transfers web pages between browser and server; stateless |
| **HTTPS** | HTTP Secure | 443 | TCP | RFC 2818 | HTTP encrypted with TLS/SSL; secure web browsing |
| **HTTP/2** | HTTP version 2 | 443 | TCP | RFC 7540 | Multiplexed, compressed HTTP over TLS |
| **HTTP/3** | HTTP version 3 | 443 | UDP (QUIC) | RFC 9114 | HTTP over QUIC protocol; faster than TCP-based HTTP |

#### Email Protocols

| Protocol | Full Name | Port(s) | Transport | RFC | Description |
|----------|-----------|---------|-----------|-----|-------------|
| **SMTP** | Simple Mail Transfer Protocol | 25 (server-to-server), 587 (client submission), 465 (SMTPS) | TCP | RFC 5321 | Sends/relays email from client to server and between mail servers |
| **POP3** | Post Office Protocol v3 | 110 (plain), 995 (SSL) | TCP | RFC 1939 | Downloads email from server to client; deletes from server by default |
| **IMAP** | Internet Message Access Protocol | 143 (plain), 993 (SSL) | TCP | RFC 3501 | Accesses email on server; email stays on server; supports folders |
| **IMAP4** | IMAP version 4 | 143 / 993 | TCP | RFC 3501 | Current version of IMAP |

#### File Transfer Protocols

| Protocol | Full Name | Port(s) | Transport | RFC | Description |
|----------|-----------|---------|-----------|-----|-------------|
| **FTP** | File Transfer Protocol | 21 (control), 20 (data – active mode) | TCP | RFC 959 | Transfers files; uses two separate connections; no encryption |
| **FTPS** | FTP Secure | 990 (implicit), 21 (explicit) | TCP | RFC 4217 | FTP with SSL/TLS encryption |
| **SFTP** | SSH File Transfer Protocol | 22 | TCP | IETF draft | File transfer over SSH; completely different protocol from FTP |
| **TFTP** | Trivial File Transfer Protocol | 69 | UDP | RFC 1350 | Simple, lightweight file transfer; no authentication; used for booting network devices, transferring IOS images |

#### Remote Access Protocols

| Protocol | Full Name | Port(s) | Transport | RFC | Description |
|----------|-----------|---------|-----------|-----|-------------|
| **SSH** | Secure Shell | 22 | TCP | RFC 4251 | Encrypted remote terminal access and file transfer; replaced Telnet |
| **Telnet** | Teletype Network | 23 | TCP | RFC 854 | Unencrypted remote terminal access; legacy; should not be used in production |
| **RDP** | Remote Desktop Protocol | 3389 | TCP (and UDP) | Microsoft | Graphical remote desktop access; used on Windows |

#### Name Resolution Protocols

| Protocol | Full Name | Port(s) | Transport | RFC | Description |
|----------|-----------|---------|-----------|-----|-------------|
| **DNS** | Domain Name System | 53 | UDP (queries), TCP (zone transfers & large responses) | RFC 1034/1035 | Resolves domain names to IP addresses; hierarchical distributed database |

#### Network Management Protocols

| Protocol | Full Name | Port(s) | Transport | RFC | Description |
|----------|-----------|---------|-----------|-----|-------------|
| **SNMP** | Simple Network Management Protocol | 161 (agent), 162 (trap) | UDP | RFC 3411 | Monitors and manages network devices; collects stats, sends alerts |
| **Syslog** | System Logging Protocol | 514 | UDP | RFC 5424 | Sends log messages from devices to a central log server |
| **NTP** | Network Time Protocol | 123 | UDP | RFC 5905 | Synchronizes clocks across network devices; critical for logging, auth, certificates |

#### IP Address Assignment

| Protocol | Full Name | Port(s) | Transport | RFC | Description |
|----------|-----------|---------|-----------|-----|-------------|
| **DHCP** | Dynamic Host Configuration Protocol | 67 (server), 68 (client) | UDP | RFC 2131 | Automatically assigns IP address, subnet mask, default gateway, DNS to clients |
| **BOOTP** | Bootstrap Protocol | 67 / 68 | UDP | RFC 951 | Predecessor to DHCP; static IP assignment via MAC address |

#### Directory & Authentication

| Protocol | Full Name | Port(s) | Transport | RFC | Description |
|----------|-----------|---------|-----------|-----|-------------|
| **LDAP** | Lightweight Directory Access Protocol | 389 (plain), 636 (LDAPS) | TCP | RFC 4511 | Queries and modifies directory services (e.g., Active Directory) |
| **RADIUS** | Remote Authentication Dial-In User Service | 1812 (auth), 1813 (accounting) | UDP | RFC 2865 | AAA protocol for network access authentication |
| **TACACS+** | Terminal Access Controller Access-Control System Plus | 49 | TCP | Cisco proprietary | Cisco AAA protocol; separates authentication, authorization, accounting |
| **Kerberos** | Kerberos Authentication | 88 | UDP / TCP | RFC 4120 | Network authentication protocol using tickets; used in Windows domains |

#### Voice & Multimedia

| Protocol | Full Name | Port(s) | Transport | RFC | Description |
|----------|-----------|---------|-----------|-----|-------------|
| **SIP** | Session Initiation Protocol | 5060 (plain), 5061 (TLS) | UDP / TCP | RFC 3261 | Establishes, modifies, terminates VoIP calls and multimedia sessions |
| **RTP** | Real-time Transport Protocol | 16384–32767 (dynamic) | UDP | RFC 3550 | Carries actual audio/video data in VoIP and streaming |

#### Other Key Protocols

| Protocol | Full Name | Port(s) | Transport | RFC | Description |
|----------|-----------|---------|-----------|-----|-------------|
| **ICMP** | Internet Control Message Protocol | No port (Layer 3) | IP Protocol 1 | RFC 792 | Error reporting and diagnostics (ping, traceroute); no port number |
| **BGP** | Border Gateway Protocol | 179 | TCP | RFC 4271 | Internet routing protocol between Autonomous Systems |
| **OSPF** | Open Shortest Path First | No port (IP Proto 89) | IP Protocol 89 | RFC 2328 | Link-state IGP routing protocol |
| **EIGRP** | Enhanced IGRP | No port (IP Proto 88) | IP Protocol 88 | RFC 7868 | Cisco advanced distance-vector routing protocol |
| **SMB** | Server Message Block | 445 (direct), 139 (NetBIOS) | TCP | Microsoft | Windows file and printer sharing; also used by Samba on Linux |
| **NetBIOS** | Network Basic I/O System | 137 (name), 138 (datagram), 139 (session) | UDP/TCP | RFC 1001/1002 | Legacy Windows name resolution and session service |

---

## 4. How It Works — Step by Step

### 4.1 DNS Resolution — Step by Step

```
[Browser] → [Local Cache] → [Recursive Resolver (ISP)] → [Root Server] → [TLD Server] → [Authoritative Server]
```

**Scenario:** User types `www.example.com` in browser.

1. **Browser cache check**: Browser checks its own DNS cache. If found, uses that IP. Done.
2. **OS cache check**: OS checks its local DNS cache and the `hosts` file. If found, uses that IP. Done.
3. **Recursive resolver query**: OS sends a DNS query (UDP, port 53) to the configured **recursive resolver** (typically the ISP's DNS server or a public resolver like 8.8.8.8).
4. **Recursive resolver cache**: If the resolver has the answer cached, it replies immediately.
5. **Root server query**: Resolver queries a **Root Name Server** (13 root server clusters, labeled A–M). Root server responds with the address of the **.com TLD name server**.
6. **TLD server query**: Resolver queries the **.com TLD server**, which responds with the address of **example.com's authoritative name server**.
7. **Authoritative server query**: Resolver queries the **authoritative name server** for example.com, which responds with the IP address for `www.example.com`.
8. **Response to client**: Resolver returns the IP address to the client's OS, caching the result for the duration of the **TTL (Time To Live)** in the DNS record.
9. **Browser connects**: Browser uses the resolved IP to open a TCP connection to port 80 (HTTP) or 443 (HTTPS).

### 4.2 HTTP Request — Step by Step

```
Client (Browser)                          Web Server (port 80)
      |                                         |
      |---TCP SYN --------------------------->  |  (3-way handshake)
      |<--TCP SYN-ACK -----------------------  |
      |---TCP ACK --------------------------->  |
      |                                         |
      |---HTTP GET /index.html HTTP/1.1 ----->  |  (HTTP request)
      |   Host: www.example.com                 |
      |                                         |
      |<--HTTP/1.1 200 OK -------------------  |  (HTTP response)
      |   Content-Type: text/html               |
      |   <html>...</html>                      |
      |                                         |
      |---TCP FIN --------------------------->  |  (connection teardown)
      |<--TCP FIN-ACK -----------------------  |
```

1. Browser performs DNS resolution to get the server IP.
2. Browser initiates a **TCP 3-way handshake** to port 80 of the web server.
3. Browser sends an **HTTP GET request** with the requested resource path and headers.
4. Web server processes the request and sends an **HTTP response** with status code (200 OK, 404 Not Found, etc.) and the requested content.
5. Browser renders the received HTML/CSS/JS content.
6. Connection is closed with **TCP 4-way teardown** (FIN/FIN-ACK sequence).

### 4.3 DHCP Process — DORA (Step by Step)

```
Client                                    DHCP Server
  |                                            |
  |---DHCP DISCOVER (broadcast) ------------>  |  UDP src:68, dst:67, IP src:0.0.0.0, IP dst:255.255.255.255
  |                                            |
  |<--DHCP OFFER (broadcast/unicast) --------  |  Server offers an IP address
  |                                            |
  |---DHCP REQUEST (broadcast) ------------->  |  Client formally requests the offered IP
  |                                            |
  |<--DHCP ACK (broadcast/unicast) ----------  |  Server confirms; client configures IP
```

**DORA stands for: Discover → Offer → Request → Acknowledge**

1. **Discover**: Client (no IP yet) broadcasts a DHCP Discover message on UDP port 67 (server) from port 68 (client), source IP 0.0.0.0, destination 255.255.255.255.
2. **Offer**: DHCP server responds with a DHCP Offer containing a proposed IP address, subnet mask, default gateway, DNS server, and lease duration.
3. **Request**: Client broadcasts a DHCP Request selecting the offered configuration (there may be multiple DHCP servers; broadcast informs all of them which offer was accepted).
4. **Acknowledge**: Server sends DHCP ACK confirming the assignment. Client configures its network interface with the provided settings.

### 4.4 FTP — Active vs. Passive Mode

**Active Mode (PORT):**
```
Client (random high port N)    Server (port 21 control, port 20 data)
  |---Control connection -----> Port 21   (client initiates)
  |<--Server opens data ------  Port 20→N (SERVER initiates data back to client)
```
- Client tells server its IP and port via PORT command.
- Server initiates the data connection from port 20 to the client. **Problematic with firewalls** (inbound connection to client blocked).

**Passive Mode (PASV):**
```
Client (random high ports)     Server (port 21 control, random high port data)
  |---Control connection -----> Port 21   (client initiates)
  |---Data connection --------> Random port  (CLIENT initiates data connection)
```
- Client sends PASV command; server responds with its IP and a random high port.
- Client initiates BOTH connections. **Firewall-friendly** (all connections initiated by client).

### 4.5 SMTP Email Delivery — Step by Step

```
[Email Client] --SMTP:587--> [Sender's Mail Server] --SMTP:25--> [Recipient's Mail Server] --IMAP:143/POP3:110--> [Recipient Client]
```

1. User composes email in client (Outlook, Thunderbird, etc.).
2. Client submits email to sender's **mail server** via **SMTP port 587** (with authentication).
3. Sender's mail server does a **DNS MX record lookup** to find recipient's mail server.
4. Sender's mail server delivers email to recipient's mail server via **SMTP port 25**.
5. Recipient's mail server stores the email.
6. Recipient's email client retrieves it via **IMAP (port 143)** or **POP3 (port 110)**.

---

## 5. Critical Numbers & Key Values

| Protocol | Port Number(s) | Transport | Notes |
|----------|---------------|-----------|-------|
| FTP (data) | 20 | TCP | Active mode data channel |
| FTP (control) | 21 | TCP | Command/control channel; both modes |
| SSH | 22 | TCP | Encrypted remote access; also SFTP |
| Telnet | 23 | TCP | Unencrypted; legacy |
| SMTP | 25 | TCP | Server-to-server email delivery |
| DNS | 53 | UDP (queries) / TCP (zone transfers) | Both transports; same port |
| DHCP (server) | 67 | UDP | Server listens on port 67 |
| DHCP (client) | 68 | UDP | Client sends from port 68 |
| TFTP | 69 | UDP | Trivial file transfer; no auth |
| HTTP | 80 | TCP | Unencrypted web traffic |
| Kerberos | 88 | UDP / TCP | Authentication tickets |
| POP3 | 110 | TCP | Email download (plain) |
| NetBIOS Name | 137 | UDP | Windows name resolution |
| NetBIOS Datagram | 138 | UDP | Windows connectionless session |
| NetBIOS Session | 139 | TCP | Windows file sharing (legacy) |
| IMAP | 143 | TCP | Email access (plain); stays on server |
| SNMP (agent) | 161 | UDP | Network device monitoring |
| SNMP (trap) | 162 | UDP | Unsolicited alerts from devices |
| LDAP | 389 | TCP | Directory services (plain) |
| HTTPS | 443 | TCP | Encrypted web traffic (TLS) |
| SMB | 445 | TCP | Windows file/printer sharing (direct) |
| SMTP (submission) | 587 | TCP | Client-to-server email (authenticated) |
| LDAPS | 636 | TCP | LDAP over SSL |
| IMAP over SSL | 993 | TCP | IMAP with encryption |
| POP3 over SSL | 995 | TCP | POP3 with encryption |
| RADIUS (auth) | 1812 | UDP | AAA authentication |
| RADIUS (accounting) | 1813 | UDP | AAA accounting |
| NTP | 123 | UDP | Time synchronization |
| BGP | 179 | TCP | Inter-AS routing |
| RIP | 520 | UDP | Distance-vector IGP |
| TACACS+ | 49 | TCP | Cisco AAA protocol |
| SIP | 5060 / 5061 | UDP / TCP | VoIP signaling (5061 = TLS) |
| RDP | 3389 | TCP | Windows remote desktop |
| Syslog | 514 | UDP | Central log collection |
| SMTPS | 465 | TCP | SMTP over SSL (legacy; 587 preferred) |
| FTPS (implicit) | 990 | TCP | FTP over SSL |
| OSPF | IP Protocol 89 | — | No port; directly over IP |
| EIGRP | IP Protocol 88 | — | No port; directly over IP |
| ICMP | IP Protocol 1 | — | No port; ping, traceroute |
| Well-known port range | 0 – 1023 | — | IANA-assigned system ports |
| Registered port range | 1024 – 49151 | — | IANA-registered app ports |
| Ephemeral port range | 49152 – 65535 | — | Dynamic client source ports |
| Total port numbers | 65535 (16-bit) | — | 0 is reserved; 1–65535 usable |

---

## 6. Important Terms & Definitions

| Term | Definition |
|------|-----------|
| **Protocol** | A standardized set of rules governing the format, timing, sequencing, and error control of data exchanged between devices |
| **Port Number** | A 16-bit integer (0–65535) that identifies a specific application or service on a device; allows multiple services to share one IP address |
| **Socket** | The combination of an IP address and a port number (e.g., 192.168.1.1:443) that uniquely identifies a communication endpoint |
| **Well-Known Port** | A port in the range 0–1023, reserved by IANA for standard, widely-used services (e.g., 80 for HTTP, 443 for HTTPS) |
| **Ephemeral Port** | A temporary, dynamically assigned source port (49152–65535) used by a client for an outbound connection session |
| **TCP (Transmission Control Protocol)** | A connection-oriented, reliable transport protocol that guarantees delivery, ordering, and error-checking of data segments |
| **UDP (User Datagram Protocol)** | A connectionless, unreliable transport protocol offering low overhead and speed, with no guarantee of delivery or order |
| **3-Way Handshake** | TCP's connection establishment process: SYN → SYN-ACK → ACK between client and server |
| **DNS (Domain Name System)** | A hierarchical distributed naming system that translates human-readable domain names into IP addresses; uses port 53 |
| **HTTP (HyperText Transfer Protocol)** | The stateless application-layer protocol for transferring web pages; uses port 80 |
| **HTTPS** | HTTP secured with TLS/SSL encryption; uses port 443; protects data confidentiality and integrity in transit |
| **SMTP (Simple Mail Transfer Protocol)** | The protocol used to send and relay email between mail servers; uses port 25 (server-to-server) and 587 (client submission) |
| **IMAP (Internet Message Access Protocol)** | An email retrieval protocol that keeps mail on the server; supports multiple device access and folder management; port 143 |
| **POP3 (Post Office Protocol v3)** | An email retrieval protocol that downloads mail to the client and (by default) deletes it from the server; port 110 |
| **FTP (File Transfer Protocol)** | A protocol for transferring files using two channels: port 21 (control) and port 20 (data, active mode); no encryption |
| **SSH (Secure Shell)** | An encrypted protocol for secure remote command-line access and file transfer (SFTP); uses port 22 |
| **Telnet** | An unencrypted remote access protocol; deprecated in favor of SSH; uses port 23 |
| **DHCP (Dynamic Host Configuration Protocol)** | Automatically assigns IP addresses and network configuration to clients using the DORA process; ports 67/68 |
| **TFTP (Trivial File Transfer Protocol)** | A simple, lightweight, unauthenticated file transfer protocol using UDP port 69; used for network device booting and IOS image transfer |
| **SNMP (Simple Network Management Protocol)** | A protocol for monitoring and managing network devices; agents listen on port 161; traps sent to port 162 |
| **NTP (Network Time Protocol)** | Synchronizes clocks on network devices to a time source; uses UDP port 123 |
| **ICMP (Internet Control Message Protocol)** | A Layer 3 protocol used for error reporting and diagnostics (ping uses ICMP Echo Request/Reply); no port number |
| **RADIUS** | A AAA (Authentication, Authorization, Accounting) protocol for network access control; ports 1812/1813 |
| **TACACS+** | Cisco's AAA protocol that separates authentication, authorization, and accounting into independent processes; TCP port 49 |
| **TLS/SSL** | Transport Layer Security / Secure Sockets Layer — cryptographic protocols that encrypt application-layer data; successor is TLS |
| **DORA** | The four-step DHCP process: Discover, Offer, Request, Acknowledge |
| **MX Record** | Mail Exchanger DNS record that specifies the mail server responsible for receiving email for a domain |
| **IANA** | Internet Assigned Numbers Authority — the organization that assigns and manages port numbers, IP addresses, and protocol parameters |

---

## 7. Key Facts to Remember (Exam-Critical)

1. **HTTP uses port 80 (TCP); HTTPS uses port 443 (TCP)** — HTTPS is HTTP encrypted with TLS/SSL.
2. **DNS uses port 53** — UDP for standard queries, TCP for zone transfers and responses exceeding 512 bytes.
3. **FTP uses TWO ports**: port **21** for control (commands) and port **20** for data (active mode only). Passive mode uses a random high port for data.
4. **SSH uses port 22 (TCP)** — encrypted; also used for SFTP. Telnet uses port **23 (TCP)** — unencrypted.
5. **SMTP ports**: 25 (server-to-server relay), 587 (client submission with auth), 465 (legacy SMTPS). POP3 = 110, IMAP = 143.
6. **DHCP uses UDP ports 67 (server) and 68 (client)** — the DORA process; client broadcasts with source IP 0.0.0.0.
7. **TFTP uses UDP port 69** — no authentication, no encryption; used for network device booting and IOS image transfer.
8. **SNMP uses UDP port 161** (agent/polling) and **162** (traps — unsolicited alerts from device to manager).
9. **NTP uses UDP port 123** — time synchronization is critical for certificates, Kerberos authentication, and log correlation.
10. **RADIUS uses UDP 1812 (auth) and 1813 (accounting)**; **TACACS+ uses TCP port 49** — Cisco proprietary.
11. **ICMP has no port number** — it operates at Layer 3 directly over IP (Protocol 1); used by ping and traceroute.
12. **Well-known ports are 0–1023**, registered ports 1024–49151, ephemeral ports 49152–65535.
13. **RDP uses TCP port 3389** — Windows Remote Desktop Protocol; also uses UDP 3389 for some functions.
14. **SIP uses port 5060 (plain) and 5061 (TLS)** for VoIP call signaling; **RTP** carries the actual voice/video data on dynamic UDP ports.
15. **BGP uses TCP port 179** — the only EGP protocol; runs between Autonomous Systems.

---

## 8. Common Comparisons & Differences

### 8.1 TCP vs. UDP

| Feature | TCP | UDP |
|---------|-----|-----|
| Connection type | Connection-oriented (handshake) | Connectionless |
| Reliability | Guaranteed delivery (ACKs + retransmit) | No guarantee |
| Ordering | In-order delivery (sequence numbers) | No ordering |
| Error checking | Yes (checksum + retransmission) | Checksum only (no retransmit) |
| Speed | Slower (overhead) | Faster (minimal overhead) |
| Header size | 20 bytes minimum | 8 bytes |
| Flow control | Yes (sliding window) | No |
| Use cases | HTTP, HTTPS, FTP, SSH, SMTP, Telnet | DNS, DHCP, TFTP, SNMP, NTP, VoIP, streaming |

### 8.2 HTTP vs. HTTPS

| Feature | HTTP | HTTPS |
|---------|------|-------|
| Port | 80 | 443 |
| Encryption | None | TLS/SSL |
| Data visibility | Plain text (sniffable) | Encrypted |
| Certificate required | No | Yes (SSL/TLS certificate) |
| URL prefix | http:// | https:// |
| RFC | RFC 9110 | RFC 2818 |
| Use case | Legacy / internal / development | All production web traffic |

### 8.3 FTP vs. SFTP vs. FTPS vs. TFTP

| Feature | FTP | SFTP | FTPS | TFTP |
|---------|-----|------|------|------|
| Port | 21 (ctrl), 20 (data) | 22 | 990 (implicit) / 21 (explicit) | 69 |
| Transport | TCP | TCP | TCP | UDP |
| Encryption | None | Yes (SSH) | Yes (TLS) | None |
| Authentication | Username/password | SSH key or password | Certificate/password | None |
| Related to FTP? | Yes (base protocol) | No (different protocol over SSH) | Yes (FTP + TLS) | No (different, simpler) |
| Use case | Legacy file transfer | Secure file transfer | Secure FTP | Network device booting |

### 8.4 SMTP vs. POP3 vs. IMAP

| Feature | SMTP | POP3 | IMAP |
|---------|------|------|------|
| Purpose | Send email | Download email from server | Access email on server |
| Port (plain) | 25 / 587 | 110 | 143 |
| Port (SSL) | 465 | 995 | 993 |
| Transport | TCP | TCP | TCP |
| Email location after access | On server (forwarded) | Downloaded, deleted from server (default) | Stays on server |
| Multi-device support | N/A (sending only) | Poor (email removed from server) | Excellent (email stays on server) |
| RFC | RFC 5321 | RFC 1939 | RFC 3501 |

### 8.5 SSH vs. Telnet

| Feature | SSH | Telnet |
|---------|-----|--------|
| Port | 22 | 23 |
| Encryption | Yes (full session encrypted) | No (all data in plain text) |
| Authentication | Password or public key | Password (plain text) |
| Security | Secure — production standard | Insecure — legacy only |
| Transport | TCP | TCP |
| RFC | RFC 4251 | RFC 854 |
| Use case | All remote device management | Legacy / lab environments only |

### 8.6 RADIUS vs. TACACS+

| Feature | RADIUS | TACACS+ |
|---------|--------|---------|
| Developer | Livingston Enterprises / IETF | Cisco (proprietary) |
| Port | UDP 1812 (auth), 1813 (acct) | TCP 49 |
| Transport | UDP | TCP |
| Encryption | Password only (partial) | Full packet encryption |
| AAA separation | Combined (auth + authz) | Separate (each can be different server) |
| Use case | Network access (Wi-Fi, VPN, dial-up) | Cisco device administration |
| RFC | RFC 2865 | No RFC (Cisco proprietary) |

### 8.7 SNMP Versions

| Feature | SNMPv1 | SNMPv2c | SNMPv3 |
|---------|--------|---------|--------|
| RFC | RFC 1157 | RFC 1901 | RFC 3411 |
| Authentication | Community string | Community string | Username/password |
| Encryption | None | None | Yes (AES/DES) |
| Security | Very weak | Weak | Strong |
| Use in production | No | Common (legacy) | Recommended |

---

## 9. Commonly Confused Concepts — Danger Zone ⚠️

**1. FTP Port 20 vs. Port 21**
Students confuse these because FTP is described as "using port 21" but it actually uses two ports. The key difference is: **port 21** is the **control/command channel** — used for all FTP commands (login, directory listing, file names) and is always active; **port 20** is the **data channel** — used only in **active mode** to transfer actual file data. In **passive mode**, a random high port is used for data instead of 20. The exam often asks specifically which port is which.

**2. POP3 vs. IMAP**
Students confuse these because both retrieve email from a server. The key difference is: **POP3 (port 110)** downloads email to the client and **removes it from the server** by default — suited for a single device; **IMAP (port 143)** keeps email on the server and **synchronizes** it across multiple devices — suited for modern multi-device usage (phone + laptop + tablet all see the same inbox).

**3. SMTP Port 25 vs. Port 587**
Students confuse these because both are SMTP. The key difference is: **port 25** is for **server-to-server** email relay (Mail Transfer Agents communicating directly) — not for client submission; **port 587** is the **client submission** port — used by email clients (Outlook, Thunderbird) to submit outgoing mail to their outgoing mail server with authentication. Port 25 is often blocked by ISPs to prevent spam from client machines.

**4. DNS Uses UDP AND TCP**
Students assume DNS only uses UDP. The key difference is: **DNS uses UDP port 53** for normal queries and responses (fast, low overhead — most DNS traffic fits in one packet); **DNS uses TCP port 53** for **zone transfers** (full DNS database replication between servers) and for responses exceeding 512 bytes (or 4096 bytes with EDNS0). Both use the same port number (53) but different transport protocols.

**5. SNMP Port 161 vs. Port 162**
Students confuse these because both are SNMP. The key difference is: **port 161** is the port on which the **SNMP agent** (the managed device, e.g., a router) listens for polling requests from the SNMP manager; **port 162** is the port on which the **SNMP manager** listens for **traps** — unsolicited alerts that devices send when something notable happens (e.g., interface goes down). The direction is reversed: 161 = manager asks device, 162 = device tells manager.

**6. RADIUS vs. TACACS+**
Students confuse these because both are AAA protocols. The key differences are: **RADIUS uses UDP** (1812/1813) and combines authentication and authorization into one process; **TACACS+ uses TCP port 49**, encrypts the entire packet (not just the password), and separates authentication, authorization, and accounting into independent functions — giving more granular control. RADIUS is standard/vendor-neutral; TACACS+ is Cisco proprietary.

**7. SSH Port 22 vs. SFTP**
Students assume SFTP is FTP with SSH layered on, using a different port. The key clarification is: **SFTP is not FTP** — it is a completely separate protocol (SSH File Transfer Protocol) that runs entirely within an **SSH session on port 22**. It has no connection to FTP commands, modes, or ports. FTPS is FTP with TLS and does use port 990 or 21.

---

## 10. Real-World Analogy

### The Post Office + Phone System Analogy

Think of a busy city with both a **post office** (for sending packages/letters) and a **phone exchange** (for real-time calls).

- The **IP address** is the building's street address — it gets you to the right building.
- **Port numbers** are like **extension numbers** inside the building — the building (server) has one street address, but inside, department 80 handles web inquiries, department 443 handles secure inquiries, department 25 handles incoming mail, and department 22 handles private executive calls.
- **TCP** is like **registered mail** — you get a confirmation of delivery, a tracking number, and the postal service will resend if the package is lost. It takes a bit longer because of all the paperwork.
- **UDP** is like **dropping a flyer** through every letterbox — fast, no confirmation, some may be lost, but it doesn't matter because you're broadcasting to many people and speed is more important than confirmation.
- **DNS** is the **phone directory** — you know the name (www.example.com) but need to look up the number (IP address) before you can call. You ask the operator (recursive resolver), who checks various directories (root → TLD → authoritative server) to find the number.
- **DHCP** is like the **hotel front desk** — when you check in (connect to the network), the desk automatically assigns you a room number (IP address), gives you a key card (subnet mask), tells you where the exits are (default gateway), and points you to the hotel directory (DNS server).
- **HTTPS vs. HTTP** is like the difference between a **sealed, tamper-evident envelope** (HTTPS) versus a **postcard** (HTTP) — anyone handling the postcard can read it; the sealed envelope keeps the contents private.

**In networking terms, this maps to:** Protocols define the rules for every type of communication, port numbers direct traffic to the correct application on a server, TCP ensures reliable delivery while UDP prioritizes speed, and higher-level protocols like DNS and DHCP provide foundational services that every other protocol depends on.

---

## 11. Quick Revision Summary

- **Port numbers** (0–65535) identify specific services on a device; well-known ports (0–1023) are IANA-assigned for standard services.
- **TCP = reliable, connection-oriented** (handshake, ACKs, ordering); **UDP = fast, connectionless** (no guarantees) — knowing which protocol uses which transport is exam-critical.
- **Key port pairs to memorize**: FTP 20/21, SSH 22, Telnet 23, SMTP 25, DNS 53, DHCP 67/68, TFTP 69, HTTP 80, POP3 110, IMAP 143, SNMP 161/162, HTTPS 443, SMB 445, SMTP submission 587, RDP 3389.
- **DNS uses port 53** — UDP for queries, TCP for zone transfers and large responses.
- **FTP uses port 21** (control, always) and **port 20** (data, active mode only); passive mode uses a random high port for data.
- **SMTP 25** = server-to-server relay; **587** = client-to-server submission (with auth); **POP3 110** downloads/deletes mail; **IMAP 143** keeps mail on server.
- **DHCP DORA**: Discover (client→broadcast) → Offer (server) → Request (client→broadcast) → Acknowledge (server); uses UDP 67/68.
- **SNMP 161** = manager polls agent; **SNMP 162** = agent sends trap (unsolicited alert) to manager.
- **RADIUS (UDP 1812/1813)** = standard AAA for network access; **TACACS+ (TCP 49)** = Cisco AAA for device administration.
- **ICMP has no port number** — it operates directly at Layer 3 (IP Protocol 1); used by ping and traceroute.
