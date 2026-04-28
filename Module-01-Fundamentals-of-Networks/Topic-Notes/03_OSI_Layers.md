# OSI Layers
## Module: Fundamentals of Networks

---

## 1. Introduction

The **OSI Model** (Open Systems Interconnection Model) is a conceptual framework developed by the **International Organization for Standardization (ISO)** in **1984** that standardizes how different computer systems communicate over a network — regardless of their underlying architecture, hardware, or software.

### What Problem Does It Solve?
Before the OSI model, networking was vendor-specific. A device from IBM could not communicate with one from DEC (Digital Equipment Corporation) because each company used its own proprietary protocols. The OSI model solved this by creating a **universal language** — a set of rules that any vendor or developer could follow to ensure interoperability.

### Where It Fits in the Bigger Picture
The OSI model is the **theoretical backbone** of all network communication. Every protocol, device, and technology you encounter in networking — Ethernet, TCP/IP, routers, switches, firewalls — maps to one or more layers of OSI. It is the reference model against which all other models (including TCP/IP) are compared.

### Why It Is Foundational
- It provides a **structured troubleshooting framework** — network engineers isolate faults layer by layer
- It defines **clear responsibilities** for each part of the communication process
- It enables **modular design** — changes in one layer do not affect others
- Understanding OSI is a prerequisite for understanding every other networking topic

---

## 2. Core Concepts & Detailed Explanation

### The 7 Layers — Overview

The OSI model divides network communication into **7 distinct layers**, numbered **1 (bottom) to 7 (top)**. Each layer:
- Performs a **specific, well-defined function**
- Communicates only with the layer **directly above and below** it
- Adds or removes a **header (and sometimes trailer)** to the data — a process called **encapsulation** (going down) and **decapsulation** (going up)

The 7 layers from top to bottom:

| # | Layer Name | Key Role |
|---|-----------|---------|
| 7 | Application | Interface between network and user applications |
| 6 | Presentation | Data translation, encryption, compression |
| 5 | Session | Opens, manages, and closes sessions |
| 4 | Transport | End-to-end delivery, segmentation, reliability |
| 3 | Network | Logical addressing, routing between networks |
| 2 | Data Link | Physical addressing (MAC), error detection on a link |
| 1 | Physical | Raw bit transmission over physical medium |

### Memory Aid
> **"All People Seem To Need Data Processing"** (top → bottom: 7 to 1)
> **"Please Do Not Throw Sausage Pizza Away"** (bottom → top: 1 to 7)

---

### Layer 7 — Application Layer

**Function:** The topmost layer. It provides **network services directly to end-user applications**. It is NOT the application itself (e.g., Chrome, Outlook) — it is the interface layer that these applications use to access network resources.

**Key responsibilities:**
- Identifying communication partners
- Determining resource availability
- Synchronizing communication

**Protocols at this layer:** HTTP (port 80), HTTPS (port 443), FTP (port 21), SMTP (port 25), DNS (port 53), DHCP (port 67/68), Telnet (port 23), SSH (port 22), SNMP (port 161), POP3 (port 110), IMAP (port 143)

**Data unit:** **Data** (also called a message)

---

### Layer 6 — Presentation Layer

**Function:** The **translator** of the OSI model. It ensures that data sent by the application layer of one system is readable by the application layer of another — regardless of differences in data representation.

**Key responsibilities:**
- **Translation:** Converts data between formats (e.g., EBCDIC ↔ ASCII)
- **Encryption/Decryption:** Secures data for transmission (e.g., SSL/TLS operates here)
- **Compression/Decompression:** Reduces data size for efficient transmission

**Formats handled:** JPEG, MPEG, GIF, PNG, ASCII, EBCDIC, Unicode, MP3, MP4

**Data unit:** **Data**

---

### Layer 5 — Session Layer

**Function:** The **session manager**. It establishes, maintains, synchronizes, and terminates communication sessions between two devices.

**Key responsibilities:**
- **Session establishment:** Opens and manages a dialogue between systems
- **Synchronization:** Adds **checkpoints** (synchronization points) into data streams so that if a transfer fails midway, only the data after the last checkpoint needs to be retransmitted — not the entire file
- **Session termination:** Gracefully closes sessions

**Protocols:** NetBIOS, RPC (Remote Procedure Call), PPTP, L2TP, PAP, SOCKS

**Data unit:** **Data**

---

### Layer 4 — Transport Layer

**Function:** Responsible for **end-to-end communication** between processes on source and destination hosts. This layer ensures complete data transfer.

**Key responsibilities:**
- **Segmentation and Reassembly:** Breaks large data into smaller **segments** and reassembles them at the destination
- **Port Addressing:** Uses **port numbers** to direct data to the correct application process
- **Connection Control:** Provides either **connection-oriented** (TCP) or **connectionless** (UDP) communication
- **Flow Control:** Uses mechanisms like the **sliding window** to prevent the sender from overwhelming the receiver
- **Error Control:** Detects and retransmits lost or corrupted segments (TCP only)
- **Multiplexing:** Allows multiple applications to use the network simultaneously

**Key Protocols:**
- **TCP (Transmission Control Protocol):** Reliable, connection-oriented, uses 3-way handshake (SYN → SYN-ACK → ACK)
- **UDP (User Datagram Protocol):** Unreliable, connectionless, no handshake, faster

**Data unit:** **Segment** (TCP) / **Datagram** (UDP)

---

### Layer 3 — Network Layer

**Function:** Responsible for **logical addressing** and **routing** — determining the best path to deliver packets from source to destination across multiple networks.

**Key responsibilities:**
- **Logical Addressing:** Assigns **IP addresses** (IPv4 or IPv6) to identify devices across networks
- **Routing:** Determines the optimal path from source to destination using **routing protocols** (RIP, OSPF, EIGRP, BGP)
- **Packet Forwarding:** Moves packets hop-by-hop through routers
- **Fragmentation:** Breaks packets into smaller units if required by the MTU of a network link

**Devices:** **Router** (primary Layer 3 device), Layer 3 switch

**Key Protocols:** IP (IPv4, IPv6), ICMP, ARP (considered Layer 2/3 boundary), OSPF, RIP, EIGRP, BGP

**Data unit:** **Packet**

---

### Layer 2 — Data Link Layer

**Function:** Provides **node-to-node delivery** of data within the same network segment. It handles **physical (MAC) addressing** and ensures error-free delivery between directly connected devices.

**Key responsibilities:**
- **Framing:** Packages raw bits from the Physical layer into structured **frames**
- **Physical Addressing:** Uses **MAC addresses** (48-bit hardware addresses) to identify devices on the same network
- **Error Detection:** Uses **CRC (Cyclic Redundancy Check)** in the frame trailer to detect transmission errors
- **Flow Control:** Manages data flow between adjacent nodes
- **Access Control:** Determines who gets to use the shared medium (**MAC — Media Access Control**)

**Sub-layers (IEEE 802 divides Layer 2 into two):**
- **LLC (Logical Link Control) — upper sub-layer:** Provides an interface to the Network layer; handles flow control and error notification
- **MAC (Media Access Control) — lower sub-layer:** Controls hardware addressing and media access

**Devices:** **Switch**, **Bridge** (primary Layer 2 devices)

**Protocols/Standards:** Ethernet (IEEE 802.3), Wi-Fi (IEEE 802.11), PPP, HDLC, Frame Relay, ARP

**Data unit:** **Frame**

---

### Layer 1 — Physical Layer

**Function:** Deals with the **raw transmission of bits** (0s and 1s) over a physical medium. It defines the electrical, mechanical, and functional specifications for physical connections.

**Key responsibilities:**
- Defines **voltage levels**, **bit rate**, **cable types**, **connector types**, **modulation** schemes
- Manages **bit synchronization** — ensures sender and receiver use the same clock
- Defines **transmission mode:** simplex, half-duplex, full-duplex
- Handles **network topology** at the physical level (bus, star, ring, mesh)

**Devices:** **Hub**, **Repeater**, Network cables, Connectors, Modems

**Standards:** RS-232, RJ-45, RJ-11, DSL, ISDN, USB, IEEE 802.3 (Ethernet physical specs)

**Data unit:** **Bit**

---

## 3. Key Components / Types / Categories

### 3.1 Layer Classification — Upper vs Lower

| Group | Layers | Focus |
|-------|--------|-------|
| **Upper Layers** (Host layers) | 7, 6, 5 | Application-oriented; concern software and user interaction |
| **Lower Layers** (Media layers) | 4, 3, 2, 1 | Network-oriented; concern data transport and physical transmission |

*(Note: Layer 4 — Transport — is the boundary and bridge between upper and lower groups)*

---

### 3.2 Data Units Per Layer (PDU — Protocol Data Unit)

| Layer | PDU Name |
|-------|---------|
| 7 — Application | Data |
| 6 — Presentation | Data |
| 5 — Session | Data |
| 4 — Transport | Segment (TCP) / Datagram (UDP) |
| 3 — Network | Packet |
| 2 — Data Link | Frame |
| 1 — Physical | Bit |

---

### 3.3 Devices Per Layer

| Layer | Primary Device(s) |
|-------|-----------------|
| 7 — Application | Proxy server, Application gateway, Firewall (L7) |
| 6 — Presentation | — (handled by software) |
| 5 — Session | — (handled by software) |
| 4 — Transport | Firewall (stateful), Load balancer |
| 3 — Network | **Router**, Layer 3 Switch |
| 2 — Data Link | **Switch**, Bridge, NIC |
| 1 — Physical | **Hub**, Repeater, Cables, Modem |

---

### 3.4 Protocols Per Layer

| Layer | Key Protocols |
|-------|-------------|
| 7 | HTTP, HTTPS, FTP, SMTP, DNS, DHCP, Telnet, SSH, SNMP, POP3, IMAP |
| 6 | SSL, TLS, JPEG, MPEG, ASCII, EBCDIC |
| 5 | NetBIOS, RPC, PPTP, L2TP, SOCKS |
| 4 | TCP, UDP, SCTP |
| 3 | IP (v4/v6), ICMP, ARP, OSPF, RIP, EIGRP, BGP |
| 2 | Ethernet (802.3), Wi-Fi (802.11), PPP, HDLC, Frame Relay |
| 1 | RS-232, DSL, ISDN, IEEE 802.3 physical, Bluetooth physical |

---

## 4. How It Works — Step by Step

### 4.1 Encapsulation (Sending Data — Layers 7 → 1)

When a user sends data (e.g., a web request), it travels **down** the OSI layers on the **sender's side**, with each layer adding its own **header** (and Layer 2 adds a **trailer**):

```
USER DATA
   │
   ▼ Layer 7 — Application
[ L7 Header | DATA ]
   │
   ▼ Layer 6 — Presentation (encrypts/compresses)
[ L6 Header | L7 Header | DATA ]
   │
   ▼ Layer 5 — Session
[ L5 Header | L6 Header | L7 Header | DATA ]
   │
   ▼ Layer 4 — Transport (adds port numbers, seq numbers)
[ L4 Header | L5+L6+L7 Headers | DATA ]  ← SEGMENT
   │
   ▼ Layer 3 — Network (adds IP addresses)
[ L3 Header | SEGMENT ]  ← PACKET
   │
   ▼ Layer 2 — Data Link (adds MAC addresses + trailer/CRC)
[ L2 Header | PACKET | L2 Trailer ]  ← FRAME
   │
   ▼ Layer 1 — Physical
Converts frame to RAW BITS (0s and 1s) → transmitted over wire/air
```

---

### 4.2 Decapsulation (Receiving Data — Layers 1 → 7)

On the **receiver's side**, the process is reversed. Each layer **strips off its own header** and passes the remaining data up:

```
RAW BITS received
   │
   ▼ Layer 1 → passes bits to Layer 2
FRAME (L2 checks MAC address, verifies CRC, strips L2 header/trailer)
   │
   ▼ Layer 2 → passes packet to Layer 3
PACKET (L3 checks IP address, strips L3 header)
   │
   ▼ Layer 3 → passes segment to Layer 4
SEGMENT (L4 checks port, reassembles, strips L4 header)
   │
   ▼ Layer 4 → passes data to Layer 5 → 6 → 7
DATA reaches the Application
```

---

### 4.3 Peer-to-Peer Communication

Each layer on the sender communicates **logically** (not physically) with the **same layer on the receiver**. For example, Layer 3 on Sender A communicates with Layer 3 on Receiver B — using headers that only that layer understands.

```
Sender                          Receiver
┌─────────────┐                ┌─────────────┐
│ Layer 7 App │◄──────────────►│ Layer 7 App │
│ Layer 6 Pre │◄──────────────►│ Layer 6 Pre │
│ Layer 5 Ses │◄──────────────►│ Layer 5 Ses │
│ Layer 4 Trn │◄──────────────►│ Layer 4 Trn │
│ Layer 3 Net │◄──────────────►│ Layer 3 Net │
│ Layer 2 DL  │◄──────────────►│ Layer 2 DL  │
│ Layer 1 Phy │────────────────│ Layer 1 Phy │
└─────────────┘   Physical     └─────────────┘
                  Medium
```

(Arrows for Layers 2–7 represent **logical** communication; only Layer 1 is truly **physical**)

---

## 5. Critical Numbers, Port Numbers & Key Values

| Name | Value / Range | Purpose / Notes |
|------|--------------|-----------------|
| HTTP | Port **80** | Web browsing (unencrypted) |
| HTTPS | Port **443** | Secure web browsing (SSL/TLS) |
| FTP Data | Port **20** | File transfer — data channel |
| FTP Control | Port **21** | File transfer — control channel |
| SSH | Port **22** | Secure remote login |
| Telnet | Port **23** | Unsecure remote login (plaintext) |
| SMTP | Port **25** | Sending email |
| DNS | Port **53** | Domain Name resolution (UDP/TCP) |
| DHCP Server | Port **67** | Server listens here |
| DHCP Client | Port **68** | Client listens here |
| POP3 | Port **110** | Receiving email (downloads, deletes from server) |
| SNMP | Port **161** | Network management protocol |
| IMAP | Port **143** | Receiving email (stays on server) |
| MAC Address | **48 bits** (6 bytes) | Physical address at Layer 2 |
| IPv4 Address | **32 bits** (4 bytes) | Logical address at Layer 3 |
| IPv6 Address | **128 bits** (16 bytes) | Logical address at Layer 3 |
| OSI Layers | **7** | Total number of layers |
| TCP 3-way Handshake | SYN → SYN-ACK → ACK | Layer 4 connection establishment |
| Ethernet MTU | **1500 bytes** | Maximum Transmission Unit (Layer 2/3) |
| CRC | Layer **2** trailer | Cyclic Redundancy Check — error detection |
| IEEE 802.3 | Ethernet standard | Layer 1 & 2 |
| IEEE 802.11 | Wi-Fi standard | Layer 1 & 2 |

---

## 6. Important Terms & Definitions

| Term | Definition |
|------|-----------|
| **OSI Model** | A 7-layer conceptual framework by ISO for standardizing network communication |
| **Encapsulation** | The process of adding headers (and a trailer at L2) as data moves down the OSI layers |
| **Decapsulation** | The removal of headers as data moves up the OSI layers on the receiving side |
| **PDU (Protocol Data Unit)** | The name given to the data unit at each layer (Bit, Frame, Packet, Segment, Data) |
| **MAC Address** | A 48-bit hardware address burned into a NIC; used for Layer 2 (same-network) delivery |
| **IP Address** | A logical 32-bit (IPv4) or 128-bit (IPv6) address used for Layer 3 (cross-network) delivery |
| **Port Number** | A 16-bit number used at Layer 4 to identify the specific application/process |
| **Segment** | The PDU at Layer 4 (Transport); specifically the TCP PDU |
| **Packet** | The PDU at Layer 3 (Network); contains source/destination IP addresses |
| **Frame** | The PDU at Layer 2 (Data Link); contains source/destination MAC addresses + CRC |
| **CRC** | Cyclic Redundancy Check — an error-detection code added to Layer 2 frames |
| **LLC** | Logical Link Control — upper sub-layer of Data Link; interfaces with Network layer |
| **MAC Sub-layer** | Lower sub-layer of Data Link; handles hardware addressing and media access |
| **3-Way Handshake** | TCP's connection setup: SYN → SYN-ACK → ACK |
| **Flow Control** | Mechanism to prevent sender from overwhelming receiver (e.g., sliding window at L4) |
| **Routing** | The Layer 3 process of selecting the best path for packets across networks |
| **Peer-to-Peer Communication** | Logical communication between the same layers on two different systems |
| **Synchronization Point** | A checkpoint added by Session layer for recovery in long data transfers |
| **Full-Duplex** | Data flows in both directions simultaneously (defined at Layer 1) |
| **Half-Duplex** | Data flows in both directions, but only one direction at a time |

---

## 7. Key Facts to Remember (Exam-Critical)

1. The OSI model has **7 layers** — developed by **ISO** in **1984**
2. Layer numbering goes **1 (Physical) to 7 (Application)** — bottom to top
3. Data units: **Bit** (L1) → **Frame** (L2) → **Packet** (L3) → **Segment** (L4) → **Data** (L5/6/7)
4. **Router** is the primary Layer 3 device; **Switch** is Layer 2; **Hub** is Layer 1
5. **TCP** (L4) is connection-oriented and reliable; **UDP** (L4) is connectionless and fast
6. **MAC addresses** are used at Layer 2 (48-bit); **IP addresses** at Layer 3 (32-bit IPv4)
7. The **Data Link layer** has two sub-layers: **LLC** (upper) and **MAC** (lower)
8. **Encapsulation** = adding headers while going DOWN the layers (sending)
9. **Decapsulation** = stripping headers while going UP the layers (receiving)
10. Layer 6 (Presentation) is responsible for **encryption, compression, and translation**
11. Layer 5 (Session) adds **synchronization checkpoints** to enable recovery mid-transfer
12. **CRC** (error detection) is added at **Layer 2** in the frame **trailer** — not header
13. The **Transport layer** uses **port numbers** to identify applications
14. **ARP (Address Resolution Protocol)** maps IP addresses to MAC addresses — sits at Layer 2/3 boundary
15. **ICMP** (used by ping and traceroute) operates at **Layer 3**
16. The **Physical layer** converts bits to electrical/optical/radio signals — it has no concept of addresses
17. **SSL/TLS** operates at **Layer 6** (Presentation)
18. **HTTP** = port 80; **HTTPS** = port 443; **FTP** = ports 20 (data) and 21 (control)

---

## 8. Common Comparisons & Differences

### 8.1 OSI vs TCP/IP Model

| Feature | OSI Model | TCP/IP Model |
|---------|----------|-------------|
| Layers | 7 | 4 |
| Developed by | ISO | DARPA / US DoD |
| Year | 1984 | 1970s |
| Purpose | Theoretical / Reference | Practical / Implementation |
| Application layer | Layers 5, 6, 7 separate | Merged into single Application layer |
| Transport layer | Layer 4 | Layer 3 (Transport) |
| Network layer | Layer 3 | Layer 2 (Internet) |
| Data Link + Physical | Separate (L1 & L2) | Merged into Network Access layer |
| Used in practice? | As a reference/teaching model | Yes — actual internet runs on TCP/IP |

---

### 8.2 TCP vs UDP (Layer 4)

| Feature | TCP | UDP |
|---------|-----|-----|
| Type | Connection-oriented | Connectionless |
| Reliability | Reliable (acknowledges delivery) | Unreliable (no acknowledgement) |
| Speed | Slower | Faster |
| Handshake | 3-way (SYN, SYN-ACK, ACK) | None |
| Use case | HTTP, FTP, SMTP, SSH | DNS, DHCP, VoIP, streaming, gaming |
| Header size | 20 bytes (minimum) | 8 bytes |
| Error correction | Yes | No |
| Flow control | Yes (sliding window) | No |

---

### 8.3 Layer 2 vs Layer 3 Devices

| Feature | Switch (Layer 2) | Router (Layer 3) |
|---------|-----------------|-----------------|
| Address used | MAC address | IP address |
| Scope | Within a single network (LAN) | Between different networks |
| Reads up to | Data Link layer | Network layer |
| Creates | Collision domains | Broadcast domains |
| Routing table | No | Yes |

---

### 8.4 Hub vs Switch vs Router

| Feature | Hub (L1) | Switch (L2) | Router (L3) |
|---------|----------|------------|------------|
| OSI Layer | 1 | 2 | 3 |
| Addressing | None | MAC | IP |
| Intelligence | None | Moderate | High |
| Forwards to | All ports (broadcast) | Specific port (unicast) | Best path |
| Collision domain | 1 shared | Per port | Per port |
| Broadcast domain | 1 | 1 (unless VLAN) | Per interface |

---

## 9. Commonly Confused Concepts — Danger Zone ⚠️

1. **Layer 2 (Data Link) vs Layer 3 (Network) addressing:**
   Students confuse MAC and IP addresses because both identify devices. The key difference is: **MAC addresses are used for delivery within the same network (node-to-node)**; **IP addresses are used for delivery between networks (end-to-end)**. A router strips the Layer 2 frame at every hop and creates a new one — but the Layer 3 packet (with original source/destination IP) remains unchanged.

2. **Segment vs Packet vs Frame:**
   These are often used interchangeably in casual language but have precise meanings. **Segment** = Layer 4 PDU; **Packet** = Layer 3 PDU; **Frame** = Layer 2 PDU. MCQs test this constantly. The header added at each layer defines the PDU name.

3. **Application Layer (L7) vs the actual application:**
   The Application layer is NOT your browser or email client. It is the **protocol interface** (HTTP, SMTP, FTP) through which those applications access the network. This is a very common misconception.

4. **SSL/TLS — Layer 4 or Layer 6?**
   SSL/TLS is commonly associated with TCP (Layer 4) because it runs over TCP, but its function — **encryption and data transformation** — is a **Layer 6 (Presentation)** responsibility. In OSI terms, it maps to Layer 6.

5. **ARP — is it Layer 2 or Layer 3?**
   ARP (Address Resolution Protocol) resolves IP addresses to MAC addresses. It uses **IP addresses (L3 concept)** to find **MAC addresses (L2 concept)**, so it is said to sit at the **Layer 2/3 boundary**. In TCP/IP model terms, it lives in the Network Access layer.

6. **Hub vs Switch — both connect devices, what's different?**
   A Hub broadcasts all incoming data to **every port** — it has no intelligence. A Switch learns MAC addresses and forwards frames only to the **specific port** where the destination device lives. This distinction is critical: switches reduce collisions, hubs do not.

7. **Data Link Layer sub-layers (LLC vs MAC):**
   LLC (upper) talks to the **Network layer above** — it provides error notification and flow control. MAC (lower) talks to the **Physical layer below** — it controls access to the medium and handles hardware addressing. MCQs sometimes describe one function and ask which sub-layer performs it.

---

## 10. Real-World Analogy

**Sending a letter through an international postal system:**

Imagine you want to send a letter (your data) from your home in India to a friend in the USA.

- **Layer 7 (Application):** You write the letter — this is your message/content.
- **Layer 6 (Presentation):** You translate it from Hindi to English so your friend can understand it. You may also seal it in an envelope (encryption).
- **Layer 5 (Session):** You arrange the communication — agree on a time to exchange correspondence (session management).
- **Layer 4 (Transport):** If your message is too long, the postal service splits it into multiple envelopes, numbers them (1 of 3, 2 of 3…), and ensures all parts arrive (segmentation and reassembly).
- **Layer 3 (Network):** The postal service looks at the **country/city address** (IP address) to determine which country and city to route the package to.
- **Layer 2 (Data Link):** The local postman uses the **house/door number** (MAC address) to deliver it to the exact house on that street.
- **Layer 1 (Physical):** The actual vehicle — truck, plane, motorcycle — carrying the physical envelope.

**In networking terms:** Each layer of the postal system maps to an OSI layer. The letter travels through each "system" as it moves from sender to receiver, each layer adding its own processing and addressing to ensure correct, complete delivery.

---

## 11. Quick Revision Summary

- The **OSI model** is a 7-layer framework by **ISO (1984)** that standardizes network communication
- Layers 1–7: **Physical → Data Link → Network → Transport → Session → Presentation → Application**
- **Data units:** Bit (L1), Frame (L2), Packet (L3), Segment (L4), Data (L5–L7)
- **Encapsulation** = headers added going DOWN (sending); **Decapsulation** = headers removed going UP (receiving)
- Key devices: **Hub** (L1), **Switch** (L2), **Router** (L3)
- **MAC address** (48-bit) used at Layer 2 for same-network delivery; **IP address** (32-bit IPv4) at Layer 3 for cross-network delivery
- **TCP** (reliable, connection-oriented) and **UDP** (fast, connectionless) both operate at **Layer 4**
- The **Data Link layer** is divided into **LLC** (upper) and **MAC** (lower) sub-layers
- **Layer 6** handles encryption (SSL/TLS), compression, and format translation
- **Layer 5** manages sessions and adds synchronization checkpoints for data recovery
- Every protocol maps to a layer — HTTP/HTTPS/FTP/DNS/DHCP are **Layer 7**; IP/ICMP are **Layer 3**; Ethernet is **Layer 2**
