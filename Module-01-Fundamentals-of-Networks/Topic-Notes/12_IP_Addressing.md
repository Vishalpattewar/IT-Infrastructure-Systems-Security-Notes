# IP Addressing
## Module: Fundamentals of Networks

---

## 1. Introduction

**IP Addressing** is the system by which every device on a network is assigned a unique numerical label — called an **IP address** — so that data can be sent to and received from the correct destination. Think of it as a postal address system for the internet and local networks.

### The Exact Problem It Solves
Without IP addresses, routers and switches would have no way to identify where a packet should be delivered. Just as physical mail requires a house number and street name, network packets require a source and destination IP address to be routed correctly across local networks and across the internet.

### Where It Fits in the OSI and TCP/IP Models
- **OSI Layer 3 — Network Layer**: IP addressing operates at Layer 3. This is the layer responsible for logical addressing and path determination (routing).
- **TCP/IP Layer 2 — Internet Layer**: In the TCP/IP model, IP addressing belongs to the Internet layer, implemented by the **Internet Protocol (IP)**.
- IP addresses are embedded in the **IP header** of every packet. Routers read the destination IP address at Layer 3 to forward packets hop-by-hop toward the destination.

### Why This Topic Is Foundational
- Without IP addressing, **routing is impossible** — routers have nothing to base forwarding decisions on.
- Without subnetting, networks cannot be divided into logical segments, making large networks unmanageable and insecure.
- Without understanding address classes, CIDR, and private/public ranges, network engineers cannot design, configure, or troubleshoot any network.
- IP addressing underpins **every** protocol in the TCP/IP suite: DNS, HTTP, SMTP, FTP, and all others rely on IP to deliver their packets.

---

## 2. Core Concepts & Detailed Explanation

### 2.1 What Is an IP Address?
An **IP address** (Internet Protocol address) is a 32-bit (IPv4) or 128-bit (IPv6) number assigned to a network interface of a device. It serves two primary purposes:
1. **Host identification** — uniquely identifies a device on a network.
2. **Location addressing** — encodes where the device is in the network topology so packets can be routed to it.

This document focuses on **IPv4**, the dominant addressing system still in wide use.

### 2.2 IPv4 Address Structure
An **IPv4 address** is a **32-bit binary number**, typically written in **dotted-decimal notation**: four groups of 8 bits (called **octets**), each converted to a decimal number, separated by dots.

```
Binary:   11000000.10101000.00000001.00000001
Decimal:  192      .168     .1       .1
```

- Each **octet** ranges from 0 to 255 in decimal (00000000 to 11111111 in binary).
- Total possible IPv4 addresses: **2³² = 4,294,967,296** (approximately 4.3 billion).

### 2.3 Network Portion vs. Host Portion
Every IPv4 address is divided into two parts:

| Portion | Meaning |
|---------|---------|
| **Network portion** | Identifies which network the device belongs to |
| **Host portion** | Identifies the specific device within that network |

The **subnet mask** (or **prefix length**) determines how many bits belong to the network portion and how many belong to the host portion.

### 2.4 Subnet Mask
A **subnet mask** is a 32-bit number that uses a sequence of **1s** (network bits) followed by a sequence of **0s** (host bits). It is applied using a bitwise AND operation to the IP address to extract the **network address**.

```
IP Address:   192.168.1.1    = 11000000.10101000.00000001.00000001
Subnet Mask:  255.255.255.0  = 11111111.11111111.11111111.00000000
Network Addr: 192.168.1.0    = 11000000.10101000.00000001.00000000
```

### 2.5 CIDR Notation (Classless Inter-Domain Routing)
**CIDR** (defined in **RFC 4632**) replaces the old classful addressing system. Instead of fixed class boundaries, CIDR uses a **prefix length** written as a slash followed by the number of network bits:

```
192.168.1.0/24   → 24 network bits, 8 host bits
10.0.0.0/8       → 8 network bits, 24 host bits
172.16.0.0/16    → 16 network bits, 16 host bits
```

This allows flexible allocation of address blocks of any size, unlike the rigid Class A/B/C system.

### 2.6 Address Classes (Classful Addressing)
Before CIDR, IPv4 addresses were divided into fixed **classes** based on the value of the first octet. This system (defined in **RFC 791**) is now deprecated but still tested extensively.

| Class | First Octet Range | Default Mask | Default Prefix | Network/Host Bits | Purpose |
|-------|------------------|-------------|----------------|------------------|---------|
| **A** | 1 – 126 | 255.0.0.0 | /8 | 8 net / 24 host | Large organizations |
| **B** | 128 – 191 | 255.255.0.0 | /16 | 16 net / 16 host | Medium organizations |
| **C** | 192 – 223 | 255.255.255.0 | /24 | 24 net / 8 host | Small organizations |
| **D** | 224 – 239 | N/A | N/A | N/A | Multicast |
| **E** | 240 – 255 | N/A | N/A | N/A | Experimental/Reserved |

> **Note:** 127.x.x.x is reserved for **loopback** (not Class A for routing). 0.x.x.x is reserved for default network routing.

### 2.7 Private IP Address Ranges (RFC 1918)
**RFC 1918** defines three ranges of IP addresses reserved for **private** (non-routable on the public internet) use. Any organization can use these freely in their internal networks.

| Class | Private Range | CIDR | Block Size |
|-------|--------------|------|-----------|
| A | 10.0.0.0 – 10.255.255.255 | 10.0.0.0/8 | 16,777,216 addresses |
| B | 172.16.0.0 – 172.31.255.255 | 172.16.0.0/12 | 1,048,576 addresses |
| C | 192.168.0.0 – 192.168.255.255 | 192.168.0.0/16 | 65,536 addresses |

These addresses are **not routed on the internet**. NAT (Network Address Translation) is used to allow devices with private IPs to communicate on the internet.

### 2.8 Special IP Addresses
| Address / Range | Purpose |
|----------------|---------|
| 0.0.0.0 | Default route / unspecified address |
| 127.0.0.0/8 (commonly 127.0.0.1) | Loopback — packet stays on local device |
| 169.254.0.0/16 | APIPA (Automatic Private IP Addressing) — assigned when DHCP fails (RFC 3927) |
| 255.255.255.255 | Limited broadcast — sent to all hosts on local network |
| x.x.x.255 (in a /24) | Directed broadcast — sent to all hosts in a specific subnet |
| x.x.x.0 (host bits = all 0s) | Network address — identifies the subnet itself |

### 2.9 Subnetting
**Subnetting** is the process of dividing a single network into smaller sub-networks (**subnets**) by borrowing bits from the host portion of the address. This allows:
- More efficient use of IP address space.
- Logical segmentation of a network (by department, floor, function).
- Improved security (traffic isolation between subnets).
- Reduced broadcast domain size.

**Key Subnetting Formulas:**
- **Number of subnets** = 2^(borrowed bits)
- **Number of usable hosts per subnet** = 2^(host bits) − 2
  - Subtract 2 for: network address (all host bits = 0) and broadcast address (all host bits = 1)
- **Block size** = 256 − subnet mask value in the relevant octet

### 2.10 Variable Length Subnet Masking (VLSM)
**VLSM** (defined in **RFC 1009**) allows different subnets within the same network to use different prefix lengths. This enables efficient address allocation — small subnets for point-to-point links (/30 = 2 hosts), large subnets for user networks (/24 = 254 hosts).

### 2.11 Supernetting / Route Summarization
**Supernetting** (also called **route aggregation** or **summarization**) is the opposite of subnetting — it combines multiple smaller networks into a single, larger network advertisement. This reduces the number of routing table entries, improving router performance.

---

## 3. Key Components / Types / Categories

### 3.1 Types of IPv4 Addresses by Communication Method

| Type | Description | Example |
|------|-------------|---------|
| **Unicast** | One sender to one receiver | 192.168.1.1 → 10.0.0.5 |
| **Broadcast** | One sender to all hosts in a network | 192.168.1.255 (directed) / 255.255.255.255 (limited) |
| **Multicast** | One sender to a group of receivers (subscribed) | 224.0.0.0 – 239.255.255.255 (Class D) |

### 3.2 Address Categories: Public vs. Private

| Feature | Public IP | Private IP |
|---------|-----------|-----------|
| Routable on internet | Yes | No |
| Assigned by | ISP / IANA | Network admin (freely) |
| Defined by | IANA | RFC 1918 |
| Uniqueness | Globally unique | Unique only within local network |
| Example | 8.8.8.8 | 192.168.1.1 |

### 3.3 Classful vs. Classless Addressing

| Feature | Classful | Classless (CIDR) |
|---------|---------|-----------------|
| Standard | RFC 791 (1981) | RFC 4632 (2006) |
| Subnet mask | Fixed per class | Variable (any prefix length) |
| Flexibility | Low | High |
| Address waste | High (Class B = 65,534 hosts) | Low |
| Routing table size | Large | Smaller (via aggregation) |
| Still used? | Conceptually yes, practically replaced | Industry standard |

### 3.4 CIDR Block Sizes

| Prefix | Subnet Mask | Total Addresses | Usable Hosts |
|--------|------------|----------------|-------------|
| /8 | 255.0.0.0 | 16,777,216 | 16,777,214 |
| /16 | 255.255.0.0 | 65,536 | 65,534 |
| /24 | 255.255.255.0 | 256 | 254 |
| /25 | 255.255.255.128 | 128 | 126 |
| /26 | 255.255.255.192 | 64 | 62 |
| /27 | 255.255.255.224 | 32 | 30 |
| /28 | 255.255.255.240 | 16 | 14 |
| /29 | 255.255.255.248 | 8 | 6 |
| /30 | 255.255.255.252 | 4 | 2 |
| /31 | 255.255.255.254 | 2 | 0* |
| /32 | 255.255.255.255 | 1 | 1 (host route) |

**/31** is a special case used for point-to-point links (RFC 3021) — no network/broadcast address convention, both addresses usable.

---

## 4. How It Works — Step by Step

### 4.1 How a Packet Is Addressed and Routed

```
[Source Device]                [Router A]               [Router B]              [Destination]
192.168.1.10                  Gateway                  Internet                 8.8.8.8
     |                             |                        |                       |
     |  (1) App creates data       |                        |                       |
     |  (2) Transport adds TCP/UDP header                   |                       |
     |  (3) IP adds source IP (192.168.1.10)                |                       |
     |       & destination IP (8.8.8.8)                     |                       |
     |                             |                        |                       |
     |-- Ethernet frame ---------> |                        |                       |
     |  Dest MAC = Router A MAC    |                        |                       |
     |  Source MAC = Host MAC      |                        |                       |
     |  IP Dst = 8.8.8.8 (unchanged throughout)            |                       |
     |                             |                        |                       |
     |                    (4) Router A reads IP dst         |                       |
     |                        consults routing table        |                       |
     |                        forwards to Router B -------> |                       |
     |                                                      |                       |
     |                                             (5) Router B forwards ---------> |
     |                                                                      (6) Dest receives packet
```

**Step-by-Step:**
1. The source application generates data and passes it down the TCP/IP stack.
2. The Transport layer (TCP/UDP) adds a header with source/destination **port numbers**.
3. The **Network layer** adds an **IP header** containing:
   - Source IP address (192.168.1.10)
   - Destination IP address (8.8.8.8)
   - TTL (Time to Live), protocol, checksum
4. The packet is encapsulated in an **Ethernet frame** with MAC addresses for the **next hop** (not final destination).
5. Each router along the path reads the **destination IP address**, performs a longest-prefix match in its routing table, and forwards the packet — changing the MAC addresses at each hop but **never changing the IP addresses**.
6. The destination device receives the packet and de-encapsulates it up the stack.

### 4.2 How Subnetting Works — Step by Step

**Scenario:** Subnet the network 192.168.1.0/24 into 4 equal subnets.

**Step 1: Determine bits to borrow.**
- Need 4 subnets → 2² = 4 → borrow **2 bits**

**Step 2: New prefix length.**
- /24 + 2 = **/26**
- New subnet mask: 255.255.255.**192** (11000000)

**Step 3: Block size.**
- Block size = 256 − 192 = **64 addresses per subnet**

**Step 4: List subnets.**

| Subnet | Network Address | First Host | Last Host | Broadcast |
|--------|----------------|-----------|----------|-----------|
| Subnet 1 | 192.168.1.0 | 192.168.1.1 | 192.168.1.62 | 192.168.1.63 |
| Subnet 2 | 192.168.1.64 | 192.168.1.65 | 192.168.1.126 | 192.168.1.127 |
| Subnet 3 | 192.168.1.128 | 192.168.1.129 | 192.168.1.190 | 192.168.1.191 |
| Subnet 4 | 192.168.1.192 | 192.168.1.193 | 192.168.1.254 | 192.168.1.255 |

**Step 5: Usable hosts per subnet.**
- 2^6 − 2 = **62 hosts** per subnet

### 4.3 How CIDR Supernetting Works

**Scenario:** Summarize four /24 networks into one route.
- 192.168.0.0/24
- 192.168.1.0/24
- 192.168.2.0/24
- 192.168.3.0/24

**Step 1:** Convert to binary (look at where bits diverge):
```
192.168.00000000.0
192.168.00000001.0
192.168.00000010.0
192.168.00000011.0
          ^^^^^^ — last 2 bits of 3rd octet differ
```
**Step 2:** Common prefix = first 22 bits → **192.168.0.0/22**

**Step 3:** This one route summarizes all four /24 networks.

---

## 5. Critical Numbers & Key Values

| Name | Value / Range | Purpose / Notes |
|------|--------------|-----------------|
| IPv4 address length | 32 bits | Total size of an IPv4 address |
| Total IPv4 addresses | 4,294,967,296 (2³²) | Maximum theoretical address space |
| Octet range | 0 – 255 | Each of 4 octets in dotted-decimal |
| Class A range | 1.0.0.0 – 126.255.255.255 | First octet 1–126; default /8 |
| Class B range | 128.0.0.0 – 191.255.255.255 | First octet 128–191; default /16 |
| Class C range | 192.0.0.0 – 223.255.255.255 | First octet 192–223; default /24 |
| Class D range | 224.0.0.0 – 239.255.255.255 | Multicast; no subnet mask |
| Class E range | 240.0.0.0 – 255.255.255.255 | Experimental/reserved |
| Loopback address | 127.0.0.1 (block: 127.0.0.0/8) | Local device self-test; never routed |
| RFC 1918 Class A private | 10.0.0.0 – 10.255.255.255 (/8) | 16,777,216 addresses |
| RFC 1918 Class B private | 172.16.0.0 – 172.31.255.255 (/12) | 1,048,576 addresses |
| RFC 1918 Class C private | 192.168.0.0 – 192.168.255.255 (/16) | 65,536 addresses |
| APIPA range | 169.254.0.0/16 | Auto-assigned when DHCP unavailable (RFC 3927) |
| Limited broadcast | 255.255.255.255 | All hosts on local network segment |
| Default route | 0.0.0.0/0 | Matches all destinations; lowest prefix length |
| /30 subnet | 4 addresses, 2 usable | Standard for point-to-point WAN links |
| /31 subnet | 2 addresses, 2 usable (RFC 3021) | Point-to-point, no broadcast/network reserved |
| /32 subnet | 1 address | Host route; loopback interfaces |
| Class A default mask | 255.0.0.0 | 8 network bits, 24 host bits |
| Class B default mask | 255.255.0.0 | 16 network bits, 16 host bits |
| Class C default mask | 255.255.255.0 | 24 network bits, 8 host bits |
| Usable hosts formula | 2^(host bits) − 2 | Subtract network + broadcast addresses |
| Subnets formula | 2^(borrowed bits) | Number of subnets created by borrowing |
| Block size formula | 256 − subnet mask octet value | Address increment between subnets |

---

## 6. Important Terms & Definitions

| Term | Definition |
|------|-----------|
| **IP Address** | A 32-bit (IPv4) numerical label assigned to each device connected to a network, used for identification and routing |
| **Octet** | An 8-bit group; IPv4 has 4 octets separated by dots, each ranging from 0 to 255 |
| **Subnet Mask** | A 32-bit number (series of 1s followed by 0s) that defines which portion of an IP address is the network and which is the host |
| **CIDR (Classless Inter-Domain Routing)** | A method of IP address allocation using variable-length prefix notation (e.g., /24) instead of fixed class boundaries; defined in RFC 4632 |
| **Prefix Length** | The number of network bits in an IP address, written after a slash (e.g., /24 means 24 bits are network bits) |
| **Network Address** | The first address in a subnet (host bits all zero); identifies the subnet itself; not assignable to a host |
| **Broadcast Address** | The last address in a subnet (host bits all one); used to send data to all hosts in that subnet; not assignable to a host |
| **Subnetting** | Dividing a network into smaller subnetworks by borrowing bits from the host portion of the IP address |
| **VLSM (Variable Length Subnet Masking)** | Allows subnets within the same network to use different subnet masks, enabling efficient address allocation |
| **Supernetting / Route Summarization** | Combining multiple contiguous network addresses into a single, larger network advertisement to reduce routing table size |
| **RFC 1918** | The RFC that defines three private IP address ranges (10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16) reserved for internal networks |
| **Loopback Address** | The address 127.0.0.1 (range 127.0.0.0/8), used to test the TCP/IP stack of the local device without sending data to the network |
| **APIPA (Automatic Private IP Addressing)** | The process by which a device self-assigns an IP from 169.254.0.0/16 when a DHCP server is unavailable (RFC 3927) |
| **Unicast** | A one-to-one communication where a packet is addressed to a single specific destination IP address |
| **Broadcast** | A one-to-all communication within a subnet; uses the subnet's broadcast address |
| **Multicast** | A one-to-many communication to a group of subscribed receivers using Class D addresses (224.0.0.0–239.255.255.255) |
| **Default Route** | The route 0.0.0.0/0, which matches any destination and is used as a gateway of last resort |
| **Dotted-Decimal Notation** | The human-readable representation of an IPv4 address as four decimal octets separated by periods (e.g., 192.168.1.1) |
| **Host Bits** | The portion of an IP address that identifies a specific device within a subnet; determined by the subnet mask |
| **NAT (Network Address Translation)** | A mechanism that translates private IP addresses to a public IP address, allowing private hosts to communicate on the internet |

---

## 7. Key Facts to Remember (Exam-Critical)

1. **IPv4 is 32 bits**, written in dotted-decimal notation as four octets, each 0–255.
2. **Class A** first octet: 1–126; **Class B**: 128–191; **Class C**: 192–223; **Class D** (multicast): 224–239; **Class E** (experimental): 240–255.
3. **127.x.x.x is loopback** — NOT a valid Class A network range for routing. The commonly used loopback address is **127.0.0.1**.
4. **RFC 1918 private ranges**: 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 — these are **not routed on the internet**.
5. **Usable hosts per subnet = 2^(host bits) − 2** — always subtract 2 for network address and broadcast address.
6. **Number of subnets = 2^(borrowed bits)** — borrowing bits from the host portion creates subnets.
7. **A /30 subnet has 4 total addresses and 2 usable hosts** — the standard for point-to-point WAN links.
8. **A /32 is a host route** — used for loopback interfaces and specific host entries in routing tables.
9. **Block size = 256 − subnet mask value** in the interesting octet. For /26 (mask 255.255.255.192): block size = 256 − 192 = **64**.
10. **Network address = first address in subnet** (host bits all 0s); **Broadcast = last address** (host bits all 1s). Neither can be assigned to a host.
11. **APIPA range is 169.254.0.0/16** — automatically assigned when DHCP fails; indicates a DHCP problem.
12. **CIDR (RFC 4632) replaced classful addressing** — allows flexible prefix lengths instead of fixed /8, /16, /24 boundaries.
13. **0.0.0.0/0 is the default route** — matches every destination; installed as the gateway of last resort.
14. **255.255.255.255 is the limited broadcast** — reaches all hosts on the local segment; routers do not forward it.
15. **The /31 prefix** (RFC 3021) is used for point-to-point links and has **no wasted addresses** (no network/broadcast reserved).

---

## 8. Common Comparisons & Differences

### 8.1 Address Classes Compared

| Feature | Class A | Class B | Class C | Class D | Class E |
|---------|---------|---------|---------|---------|---------|
| First octet | 1–126 | 128–191 | 192–223 | 224–239 | 240–255 |
| Default mask | /8 | /16 | /24 | None | None |
| Network bits | 8 | 16 | 24 | N/A | N/A |
| Host bits | 24 | 16 | 8 | N/A | N/A |
| Max hosts | 16,777,214 | 65,534 | 254 | N/A | N/A |
| Purpose | Large orgs | Medium orgs | Small orgs | Multicast | Experimental |

### 8.2 Public vs. Private IP

| Feature | Public IP | Private IP |
|---------|-----------|-----------|
| Internet routable | Yes | No |
| Defined by | IANA allocation | RFC 1918 |
| Cost | Leased from ISP | Free to use internally |
| Uniqueness | Globally unique | Unique only locally |
| Requires NAT | No | Yes (to reach internet) |
| Example | 8.8.8.8 | 10.0.0.1 |

### 8.3 Classful vs. CIDR (Classless) Addressing

| Feature | Classful | CIDR |
|---------|---------|------|
| Standard | RFC 791 (1981) | RFC 4632 (2006) |
| Mask flexibility | Fixed (/8, /16, /24) | Any prefix /0–/32 |
| Address waste | High | Low |
| Supports VLSM | No | Yes |
| Routing table | Larger | Smaller (via aggregation) |
| Still used | Conceptually | Industry standard |

### 8.4 Unicast vs. Broadcast vs. Multicast

| Feature | Unicast | Broadcast | Multicast |
|---------|---------|-----------|-----------|
| Recipients | One specific host | All hosts in subnet | Group of subscribed hosts |
| Address range | Any valid host IP | x.x.x.255 or 255.255.255.255 | 224.0.0.0–239.255.255.255 |
| Router forwarding | Yes | No (limited broadcast) | With multicast routing |
| Bandwidth efficient | Moderate | Low | High (for group delivery) |
| Example use | Web request | ARP, DHCP discovery | Video streaming, OSPF hellos |

### 8.5 Subnet Mask vs. CIDR Notation

| Subnet Mask | CIDR | Host Bits | Usable Hosts |
|------------|------|-----------|-------------|
| 255.0.0.0 | /8 | 24 | 16,777,214 |
| 255.255.0.0 | /16 | 16 | 65,534 |
| 255.255.255.0 | /24 | 8 | 254 |
| 255.255.255.128 | /25 | 7 | 126 |
| 255.255.255.192 | /26 | 6 | 62 |
| 255.255.255.224 | /27 | 5 | 30 |
| 255.255.255.240 | /28 | 4 | 14 |
| 255.255.255.248 | /29 | 3 | 6 |
| 255.255.255.252 | /30 | 2 | 2 |

### 8.6 Network Address vs. Broadcast Address vs. Host Address

| Feature | Network Address | Broadcast Address | Host Address |
|---------|----------------|------------------|--------------|
| Host bits | All 0s | All 1s | Mixed |
| Assignable to device | No | No | Yes |
| Example (/24) | 192.168.1.0 | 192.168.1.255 | 192.168.1.1–.254 |
| Purpose | Identifies subnet | Reaches all hosts in subnet | Identifies a specific device |

---

## 9. Commonly Confused Concepts — Danger Zone ⚠️

**1. Network Address vs. Broadcast Address**
Students confuse these because both are non-assignable "special" addresses in a subnet. The key difference is: the **network address** has ALL host bits set to **0** and is the FIRST address in the subnet; the **broadcast address** has ALL host bits set to **1** and is the LAST address. For 192.168.1.0/24: network = 192.168.1.**0**, broadcast = 192.168.1.**255**.

**2. Subnet Mask vs. Wildcard Mask**
Students confuse these because both are 32-bit numbers used with IP addresses. The key difference is: a **subnet mask** uses 1s for network bits and 0s for host bits (255.255.255.0); a **wildcard mask** (used in ACLs and OSPF) is the **inverse** — 0s for network bits and 1s for host bits (0.0.0.255). They are bitwise complements of each other.

**3. Loopback (127.0.0.1) vs. APIPA (169.254.x.x)**
Students confuse these because both appear on a device without normal network connectivity. The key difference is: **loopback (127.0.0.1)** is manually/always configured for testing the TCP/IP stack of the device itself; **APIPA (169.254.x.x)** is auto-assigned by the OS when a DHCP server cannot be reached — it indicates a DHCP failure and the device cannot communicate outside its local link.

**4. /30 vs. /31 vs. /32**
Students confuse these small subnets because they're all "point-to-point." The key differences are: **/30** has 4 addresses, 2 usable (conventional WAN link); **/31** (RFC 3021) has 2 addresses, both usable — no network/broadcast reserved (used between routers); **/32** is a single host route — represents one specific device (used for loopback interfaces, host entries in routing tables).

**5. Class D (Multicast) vs. Class E (Experimental)**
Students confuse these because both are in the upper IP range and not for regular host use. The key difference is: **Class D (224–239.x.x.x)** is actively used for multicast group communications (e.g., OSPF uses 224.0.0.5, video streaming); **Class E (240–255.x.x.x)** is completely reserved for experimental/future use and has no deployed application.

**6. Limited Broadcast vs. Directed Broadcast**
Students confuse these because both "broadcast." The key difference is: **limited broadcast (255.255.255.255)** is sent to all hosts on the **local network segment** and is **never forwarded by routers**; **directed broadcast (e.g., 192.168.1.255)** is addressed to all hosts in a **specific subnet** and can theoretically be routed (though routers typically block it for security — RFC 2644).

---

## 10. Real-World Analogy

### The City Postal System Analogy

Imagine a country divided into **cities** (networks), each city divided into **streets** (subnets), and each house on a street having a **house number** (host address).

- The **country** is the internet — vast, with billions of addresses.
- Each **city** has a unique **city code** (network portion of the IP address) — just like a city name or ZIP code prefix.
- Each **street** within a city has its own range of **house numbers** (host portion of the IP address).
- The **postal worker (router)** looks at the **city code first** to determine which city (network) to send the letter to, then the **street and house number** to find the exact recipient.
- **Private addresses** are like internal office building room numbers — they're unique inside the building but meaningless and invisible to the outside postal system. The building's **reception desk (NAT/gateway)** translates these to the building's public street address when sending mail outside.
- **Subnetting** is like dividing a large city district into smaller neighborhoods — each neighborhood (subnet) has its own range of house numbers, and only houses in the same neighborhood can be reached without going through the main postal hub (router).
- The **subnet mask** is like the rule that says "the first X digits of the house number identify the neighborhood; the remaining digits identify the house."
- A **broadcast** is like putting a flyer under every door in one neighborhood.

**In networking terms, this maps to:** IP addressing uses a hierarchical system where the network portion (city code) gets a packet to the right network, the host portion (house number) delivers it to the right device, subnet masks define the neighborhood boundaries, and routers act as the postal sorting offices that read the address and forward packets toward their destination.

---

## 11. Quick Revision Summary

- **IPv4 addresses are 32-bit numbers** written as four octets in dotted-decimal notation (e.g., 192.168.1.1), with each octet ranging from 0–255.
- **Address classes (RFC 791):** Class A (1–126, /8), Class B (128–191, /16), Class C (192–223, /24), Class D (224–239, multicast), Class E (240–255, experimental).
- **127.0.0.0/8 is loopback** (not a routable Class A); **169.254.0.0/16 is APIPA** (self-assigned when DHCP fails).
- **RFC 1918 private ranges:** 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16 — not routable on the internet; require NAT to reach the internet.
- **CIDR (RFC 4632)** uses prefix notation (/24, /26, etc.) and allows variable-length subnet masks — replaced rigid classful addressing.
- **Subnetting formulas:** subnets = 2^(borrowed bits); usable hosts = 2^(host bits) − 2; block size = 256 − mask octet value.
- **Network address** = first address in subnet (all host bits = 0); **Broadcast address** = last address (all host bits = 1) — both non-assignable.
- **/30 = 2 usable hosts** (WAN links); **/31 = 2 usable hosts, no reserved** (RFC 3021); **/32 = single host route**.
- **Subnetting divides** a network into smaller segments; **supernetting/summarization** aggregates multiple networks into one route to reduce routing table entries.
- **VLSM** allows different subnets within the same IP space to use different prefix lengths, maximizing address efficiency.
