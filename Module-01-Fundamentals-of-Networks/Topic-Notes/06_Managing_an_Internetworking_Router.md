# Managing an Internetworking Router
## Module: Fundamentals of Networks

---

## 1. Introduction

### What Is Router Management?
**Managing an internetworking router** refers to the complete set of tasks a network administrator performs to **configure, monitor, maintain, troubleshoot, and secure** a Cisco router so it can correctly interconnect multiple networks and route traffic between them.

A router that is physically installed but not properly managed is useless — it will not route packets, apply security policies, or participate in the network. Router management is the bridge between hardware and a functioning, optimized network.

### What Problem Does It Solve?
Without structured router management:
- Interfaces remain inactive (no IP addressing, no activation)
- No routing decisions can be made (no routing table entries)
- Remote management is impossible (no Telnet/SSH configured)
- Security vulnerabilities remain open (default/no passwords)
- Network changes cannot be tracked or recovered from (no backups)
- Faults cannot be diagnosed (no monitoring in place)

### Where It Fits in the Bigger Picture
Router management sits at the intersection of **every networking topic** — it is the hands-on operational layer that ties together IOS knowledge, IP addressing, routing protocols, security, and troubleshooting. Topics 5 through 13 in this syllabus all depend on understanding how to manage a router properly.

### The Three Planes of Router Management
| Plane | Description | Examples |
|-------|------------|---------|
| **Data Plane** | Actual forwarding of packets based on routing table | IP packet forwarding, CEF |
| **Control Plane** | Building and maintaining routing tables | RIP, OSPF, EIGRP, static routes |
| **Management Plane** | Administrative access and configuration | CLI, SSH, SNMP, Syslog, NTP |

---

## 2. Core Concepts & Detailed Explanation

### 2.1 Interface Management

Interfaces are the physical and logical ports of a router. Managing them is the first step in making a router operational.

#### Interface Naming Convention
| Interface Type | Short Form | Example |
|--------------|-----------|---------|
| FastEthernet | Fa | Fa0/0, Fa0/1 |
| GigabitEthernet | Gi or G | Gi0/0, Gi0/0/0 |
| Serial | Se or S | Se0/0/0, Se0/1/0 |
| Loopback | Lo | Lo0, Lo1 |
| Tunnel | Tu | Tu0 |

#### Configuring an Interface — Full Sequence
```
Router(config)# interface GigabitEthernet0/0
Router(config-if)# description Link_to_LAN_Network       ← Label for documentation
Router(config-if)# ip address 192.168.1.1 255.255.255.0  ← Assign IP and subnet mask
Router(config-if)# no shutdown                            ← Activate interface
Router(config-if)# exit
```

#### Verifying Interface Status
```
Router# show interfaces GigabitEthernet0/0
Router# show ip interface brief                  ← Best overview of all interfaces
Router# show ip interface GigabitEthernet0/0     ← Detailed IP-related status
```

#### Interface Status Meanings
| Line Status | Protocol Status | Meaning | Cause |
|------------|----------------|---------|-------|
| up | up | **Fully operational** ✅ | Working normally |
| up | down | Layer 1 OK, Layer 2 issue | Encapsulation mismatch, keepalive fail |
| down | down | Layer 1 failure | Cable unplugged, hardware fault, other end is down |
| administratively down | down | Manually disabled | `shutdown` command was applied |

---

### 2.2 IP Address Management on a Router

Each router **interface** that connects to a network must have an IP address assigned to it. A router is a **multi-homed device** — it has multiple interfaces, each connected to a different network, each with its own IP address.

#### Key Rules for Router IP Addressing
- Each interface IP address must belong to the **subnet of the network it connects to**
- **No two interfaces** on the same router should be in the **same subnet**
- The IP address assigned to a router interface typically serves as the **default gateway** for hosts on that subnet

#### Example — Router with Three Interfaces
```
          Network A                    Network B                    Network C
       192.168.1.0/24              172.16.0.0/16               10.0.0.0/8
            │                            │                           │
   ┌────────┴─────────────────────────────┴───────────────────────────┴────────┐
   │  Fa0/0: 192.168.1.1/24    Fa0/1: 172.16.0.1/16    Se0/0/0: 10.0.0.1/8   │
   │                          ROUTER R1                                         │
   └─────────────────────────────────────────────────────────────────────────  ┘
```

#### Secondary IP Addresses
A single interface can have **multiple IP addresses** — one primary and one or more secondary:
```
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# ip address 192.168.2.1 255.255.255.0 secondary
```

---

### 2.3 Routing Table Management

The **routing table** is the core data structure of a router — it contains all the known networks and how to reach them. The router consults this table for every single packet it forwards.

#### Viewing the Routing Table
```
Router# show ip route
```

#### Routing Table Output — Reading It
```
Router# show ip route

Codes: C - connected, S - static, R - RIP, O - OSPF, D - EIGRP, B - BGP
       * - candidate default, U - per-user static route

Gateway of last resort is 0.0.0.0 to network 0.0.0.0

C    192.168.1.0/24 is directly connected, GigabitEthernet0/0
C    10.0.0.0/8 is directly connected, Serial0/0/0
S    172.16.0.0/16 [1/0] via 10.0.0.2
R    192.168.2.0/24 [120/1] via 10.0.0.2, 00:00:23, Serial0/0/0
O    10.10.0.0/24 [110/20] via 10.0.0.2, 00:05:11, Serial0/0/0
S*   0.0.0.0/0 [1/0] via 203.0.113.1
```

#### Routing Table Code Meanings
| Code | Protocol | Default AD |
|------|---------|-----------|
| **C** | Connected (directly attached network) | 0 |
| **L** | Local (interface IP itself) | 0 |
| **S** | Static route (manually configured) | 1 |
| **R** | RIP (Routing Information Protocol) | 120 |
| **D** | EIGRP (Enhanced IGRP) | 90 (internal) / 170 (external) |
| **O** | OSPF (Open Shortest Path First) | 110 |
| **B** | BGP (Border Gateway Protocol) | 20 (eBGP) / 200 (iBGP) |
| **I** | IGRP | 100 |
| **EX** | EIGRP external | 170 |

#### Understanding [AD/Metric] in Routing Table
Format: `[Administrative Distance / Metric]`
- **Administrative Distance (AD):** Trustworthiness of the routing source — **lower = more trusted**
- **Metric:** Cost to reach the destination within that routing protocol — **lower = better path**

Example: `[120/1]` means AD=120 (RIP), Metric=1 (1 hop away)

---

### 2.4 Administrative Distance (AD) — Complete Table

| Route Source | Administrative Distance |
|-------------|------------------------|
| Directly Connected | **0** |
| Static Route | **1** |
| EIGRP Summary Route | **5** |
| eBGP (External BGP) | **20** |
| EIGRP (Internal) | **90** |
| IGRP | **100** |
| OSPF | **110** |
| IS-IS | **115** |
| RIP | **120** |
| EIGRP (External) | **170** |
| iBGP (Internal BGP) | **200** |
| Unknown / Unreachable | **255** (never used) |

> **Memory Rule:** "Can Some Engineers Do It Right?" = Connected(0), Static(1), EIGRP(90), EIGRP-ext(170)... Lower is always better.

---

### 2.5 Static Routing

**Static routes** are manually configured routes — the administrator tells the router explicitly how to reach a specific network.

#### When to Use Static Routes
- Small networks with few routers
- Stub networks (networks with only one path out)
- Default route configuration
- Security-sensitive routes (no dynamic protocol advertising)

#### Static Route Command Syntax
```
Router(config)# ip route [destination-network] [subnet-mask] [next-hop-IP | exit-interface]
```

#### Types of Static Routes
```
1. Standard Static Route:
   Router(config)# ip route 192.168.2.0 255.255.255.0 10.0.0.2
   (Send packets for 192.168.2.0/24 to next-hop 10.0.0.2)

2. Default Route (Gateway of Last Resort):
   Router(config)# ip route 0.0.0.0 0.0.0.0 203.0.113.1
   (Send ALL unknown destinations to 203.0.113.1 — typically toward the Internet)

3. Floating Static Route (Backup Route):
   Router(config)# ip route 192.168.2.0 255.255.255.0 10.0.0.2 200
   (AD set to 200 — only used if primary route with lower AD disappears)

4. Summary Static Route:
   Router(config)# ip route 10.0.0.0 255.0.0.0 10.1.1.1
   (Summarizes multiple /24 networks into one /8 route)
```

#### Verifying Static Routes
```
Router# show ip route static
Router# show ip route 192.168.2.0
```

---

### 2.6 Cisco Discovery Protocol (CDP)

**CDP** is a **Cisco proprietary Layer 2 protocol** that allows Cisco devices to discover information about directly connected Cisco neighbors — automatically, without any IP configuration.

#### CDP Key Facts
- Operates at **Layer 2** — works even if no IP is configured
- Sends CDP advertisements every **60 seconds** by default
- CDP hold time: **180 seconds** (3x hello interval)
- Enabled by default on all Cisco interfaces
- Useful for **network topology discovery and documentation**

#### CDP Commands
```
Router# show cdp neighbors           → Lists directly connected Cisco devices
Router# show cdp neighbors detail    → Shows IP addresses, IOS version, platform
Router# show cdp                     → CDP timer and hold-time settings
Router# show cdp interface           → CDP status per interface
Router(config)# no cdp run           → Disable CDP globally
Router(config-if)# no cdp enable     → Disable CDP on specific interface
```

#### CDP Output Example
```
Router# show cdp neighbors
Device ID    Local Intrfce   Holdtme   Capability  Platform   Port ID
Switch1      Gig 0/0          150         S        WS-C2960   Fas 0/1
Router2      Ser 0/0/0        170         R        CISCO2901  Ser 0/0/0
```

---

### 2.7 Remote Management — Telnet and SSH

#### Configuring Telnet (VTY Lines)
```
Router(config)# line vty 0 4
Router(config-line)# password telnetpass
Router(config-line)# login
Router(config-line)# transport input telnet
Router(config-line)# exec-timeout 10 0        ← Timeout after 10 minutes idle
Router(config-line)# exit
```

#### Configuring SSH (Secure Remote Management)
SSH requires the IOS image to include crypto support (k9 feature set).

```
Step 1: Set domain name (required for key generation)
Router(config)# ip domain-name example.com

Step 2: Generate RSA key pair
Router(config)# crypto key generate rsa
How many bits in the modulus [512]: 1024   ← 1024 minimum; 2048 recommended

Step 3: Create local username and password
Router(config)# username admin privilege 15 secret securepass123

Step 4: Configure VTY lines for SSH only
Router(config)# line vty 0 4
Router(config-line)# login local               ← Use local username database
Router(config-line)# transport input ssh       ← Allow SSH only (block Telnet)
Router(config-line)# exec-timeout 5 0          ← Auto-logout after 5 minutes

Step 5: Set SSH version 2 (more secure)
Router(config)# ip ssh version 2

Step 6: Verify SSH
Router# show ip ssh
Router# show ssh
```

#### SSH Version 1 vs Version 2
| Feature | SSH v1 | SSH v2 |
|---------|--------|--------|
| Security | Weaker — known vulnerabilities | Stronger — redesigned protocol |
| Authentication | Limited | Improved key exchange |
| Recommended | No | **Yes** |
| IOS command | `ip ssh version 1` | `ip ssh version 2` |

---

### 2.8 SNMP — Simple Network Management Protocol

**SNMP** is used for **automated network monitoring and management**. It allows a central **Network Management System (NMS)** to query and configure network devices remotely.

#### SNMP Components
| Component | Role |
|----------|------|
| **NMS (Network Management Station)** | Central server that polls and receives data from devices |
| **SNMP Agent** | Software running on the managed device (router/switch) |
| **MIB (Management Information Base)** | Database of all manageable objects on a device |
| **OID (Object Identifier)** | Unique numerical identifier for each object in the MIB |

#### SNMP Versions
| Version | Security | Notes |
|---------|---------|-------|
| **SNMPv1** | No encryption, community string only | Legacy — insecure |
| **SNMPv2c** | Community string (plaintext) | Most widely deployed |
| **SNMPv3** | **Authentication + Encryption** | Recommended — secure |

#### SNMP Operations
| Operation | Direction | Description |
|----------|----------|------------|
| **GET** | NMS → Agent | Request specific variable value |
| **GET-NEXT** | NMS → Agent | Walk through MIB tree |
| **GET-BULK** | NMS → Agent | Retrieve large data blocks (v2+) |
| **SET** | NMS → Agent | Change a variable on device |
| **TRAP** | Agent → NMS | Unsolicited alert when event occurs |
| **INFORM** | Agent → NMS | Like TRAP but requires acknowledgment (v2+) |

#### SNMP Ports
- SNMP Agent listens: **UDP port 161**
- SNMP Trap receiver: **UDP port 162**

#### Configuring SNMPv2c on a Router
```
Router(config)# snmp-server community public RO         ← Read-Only community string
Router(config)# snmp-server community private RW        ← Read-Write community string
Router(config)# snmp-server host 10.0.0.100 version 2c public   ← NMS server IP
Router(config)# snmp-server enable traps                ← Enable trap notifications
```

---

### 2.9 Syslog — System Logging

**Syslog** is the standard protocol for collecting and storing **log messages** generated by network devices. Every event on a router (interface state change, authentication failure, config change) generates a syslog message.

#### Syslog Severity Levels (0–7)
| Level | Name | Description | Memory Aid |
|-------|------|-------------|-----------|
| 0 | **Emergencies** | System unusable | Every |
| 1 | **Alerts** | Immediate action required | Admin |
| 2 | **Critical** | Critical conditions | Can |
| 3 | **Errors** | Error conditions | See |
| 4 | **Warnings** | Warning conditions | What |
| 5 | **Notifications** | Normal but significant | Network |
| 6 | **Informational** | Informational messages | Issues |
| 7 | **Debugging** | Debug-level messages | Develop |

> Memory Aid: **"Every Admin Can See What Network Issues Develop"** (0–7)

#### Syslog Message Format
```
%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0, changed state to up
 │         │ │
 │         │ └── Message text
 │         └──── Severity level (5 = Notifications)
 └────────────── Facility (LINEPROTO = Line Protocol subsystem)
```

#### Configuring Syslog
```
Router(config)# logging 10.0.0.200              ← Send logs to syslog server IP
Router(config)# logging trap warnings           ← Send level 4 (warnings) and above
Router(config)# logging buffered 64000          ← Buffer 64KB of logs in RAM
Router(config)# service timestamps log datetime ← Add timestamp to log messages
Router# show logging                            ← View log buffer
```

---

### 2.10 NTP — Network Time Protocol

**NTP** synchronizes the clocks of network devices to a **common time source**. Accurate time is critical for:
- **Log correlation** — matching syslog events across multiple devices
- **Certificate validity** — SSL/TLS certificates are time-sensitive
- **Authentication protocols** — Kerberos requires time sync within 5 minutes

#### NTP Hierarchy — Stratum Levels
| Stratum | Source |
|---------|-------|
| **Stratum 0** | Atomic clock, GPS clock — the primary time reference (not a network device) |
| **Stratum 1** | NTP server directly connected to Stratum 0 source |
| **Stratum 2** | Syncs from Stratum 1 |
| **Stratum 3** | Syncs from Stratum 2 |
| ... | (up to Stratum 15) |
| **Stratum 16** | Unsynchronized device |

#### NTP Configuration on Cisco Router
```
Router(config)# ntp server 216.239.35.0        ← Configure NTP server IP
Router(config)# ntp update-calendar            ← Sync hardware calendar with NTP time
Router# show ntp status                         ← View synchronization status
Router# show ntp associations                   ← View NTP peers
Router# show clock                              ← Display current time
```

#### Manual Clock Setting (without NTP)
```
Router# clock set 14:30:00 28 April 2026
```

---

### 2.11 Backup and Restore — Configuration Management

#### Backing Up Configuration to TFTP
```
Router# copy running-config tftp
Address or name of remote host []? 10.0.0.100
Destination filename [router-confg]? R1-backup-config
!!
1012 bytes copied in 0.200 secs
```

#### Restoring Configuration from TFTP
```
Router# copy tftp running-config
Address or name of remote host []? 10.0.0.100
Source filename []? R1-backup-config
Destination filename [running-config]?
!!
1012 bytes copied in 0.300 secs
```

#### Backing Up IOS Image to TFTP
```
Router# copy flash tftp
Source filename []? c2900-universalk9-mz.SPA.151-4.M4.bin
Address or name of remote host []? 10.0.0.100
Destination filename? c2900-universalk9-mz.SPA.151-4.M4.bin
!!!!!!!!!!!!
```

#### Restoring IOS from TFTP (from ROMMON if IOS is corrupted)
```
rommon> IP_ADDRESS=192.168.1.1
rommon> IP_SUBNET_MASK=255.255.255.0
rommon> DEFAULT_GATEWAY=192.168.1.254
rommon> TFTP_SERVER=192.168.1.100
rommon> TFTP_FILE=c2900-universalk9-mz.SPA.151-4.M4.bin
rommon> tftpdnld
```

---

### 2.12 Access Control Lists (ACLs) — Basic Management

**ACLs** are ordered sets of rules that **permit or deny traffic** based on criteria like source/destination IP, protocol, or port numbers. They are applied to router interfaces to control traffic flow.

#### ACL Types
| Type | Number Range | Filters Based On |
|------|-------------|-----------------|
| **Standard ACL** | 1–99, 1300–1999 | Source IP address only |
| **Extended ACL** | 100–199, 2000–2699 | Source IP, Destination IP, Protocol, Port |
| **Named ACL** | Any name | Same as numbered but identified by name |

#### Standard ACL — Configuration
```
Router(config)# access-list 10 permit 192.168.1.0 0.0.0.255
Router(config)# access-list 10 deny any

Router(config)# interface GigabitEthernet0/1
Router(config-if)# ip access-group 10 in          ← Apply inbound on interface
```

#### Extended ACL — Configuration
```
Router(config)# access-list 110 permit tcp 192.168.1.0 0.0.0.255 any eq 80
Router(config)# access-list 110 permit tcp 192.168.1.0 0.0.0.255 any eq 443
Router(config)# access-list 110 deny ip any any

Router(config)# interface GigabitEthernet0/0
Router(config-if)# ip access-group 110 out        ← Apply outbound on interface
```

#### ACL Rules — Critical
- Rules are processed **top to bottom** — first match wins
- Every ACL ends with an **implicit deny any** — even if not written
- **Standard ACLs** — place **close to the destination**
- **Extended ACLs** — place **close to the source**
- `in` = traffic entering the interface; `out` = traffic leaving the interface

#### Verifying ACLs
```
Router# show access-lists
Router# show ip interface GigabitEthernet0/0     ← Shows which ACL is applied
```

---

### 2.13 Troubleshooting Tools

#### Ping
Tests basic **Layer 3 reachability** between two IP addresses using ICMP Echo Request/Reply.
```
Router# ping 192.168.2.1
Router# ping 192.168.2.1 repeat 100 size 1500    ← Extended ping
```
Output symbols: `!` = success, `.` = timeout, `U` = unreachable, `?` = unknown

#### Traceroute
Shows the **hop-by-hop path** packets take to reach a destination and latency at each hop.
```
Router# traceroute 8.8.8.8
```
Uses **TTL incrementing** — sends packets with TTL=1, TTL=2, etc. to reveal each hop.

#### Debug Commands
Provides **real-time packet and event information** — used carefully as it consumes CPU.
```
Router# debug ip routing          ← Watch routing table updates
Router# debug ip rip              ← Watch RIP updates
Router# debug ip ospf events      ← Watch OSPF events
Router# no debug all              ← ALWAYS turn off debug after use
Router# undebug all               ← Same as above
```
> ⚠️ **Warning:** Debug on a production router can cause high CPU and outages. Use with caution.

#### Telnet as a Connectivity Test
```
Router# telnet 192.168.1.1 80     ← Test if TCP port 80 is open on destination
```

---

## 3. Key Components / Types / Categories

### 3.1 Router Management Tasks — Categorized

| Category | Tasks |
|---------|------|
| **Interface Management** | Assign IPs, activate interfaces, set descriptions, verify status |
| **Routing Management** | Configure static routes, default routes, verify routing table |
| **Security Management** | Passwords, SSH, ACLs, disable unused services |
| **Remote Access Management** | VTY lines, Telnet, SSH, privilege levels |
| **Monitoring** | CDP, SNMP, Syslog, NTP, debug, show commands |
| **Backup/Recovery** | TFTP backup/restore, password recovery, config register |

---

### 3.2 Show Commands — Quick Reference

| Command | What It Shows |
|---------|-------------|
| `show version` | IOS version, uptime, hardware, config register |
| `show running-config` | Full active configuration |
| `show startup-config` | Saved NVRAM configuration |
| `show ip interface brief` | All interfaces — IP, status, protocol (best overview) |
| `show interfaces` | Detailed stats for all interfaces |
| `show ip route` | Full routing table |
| `show ip route static` | Only static routes |
| `show ip protocols` | Running routing protocols |
| `show cdp neighbors` | Directly connected Cisco devices |
| `show cdp neighbors detail` | Neighbor IP, platform, IOS version |
| `show arp` | ARP table |
| `show access-lists` | All ACLs and match counts |
| `show ip ssh` | SSH status and version |
| `show ntp status` | NTP sync status |
| `show logging` | Syslog buffer |
| `show flash` | Flash memory contents |
| `show users` | Active console and VTY sessions |
| `show processes cpu` | CPU utilization |

---

## 4. How It Works — Step by Step

### 4.1 Complete Router Setup — From Unboxed to Fully Managed

```
PHASE 1 — Physical Setup
─────────────────────────
1. Mount router in rack / place on desk
2. Connect console cable (rollover) from router console port to PC
3. Open terminal emulator: 9600 baud, 8N1, no flow control
4. Power on router — observe boot sequence

PHASE 2 — Basic Configuration
───────────────────────────────
5. Enter Privileged EXEC:  Router> enable
6. Enter Global Config:    Router# configure terminal
7. Set hostname:           Router(config)# hostname HQ-R1
8. Set enable secret:      HQ-R1(config)# enable secret StrongPass!1
9. Disable DNS lookup:     HQ-R1(config)# no ip domain-lookup
10. Set MOTD banner:       HQ-R1(config)# banner motd # Authorized Access Only #

PHASE 3 — Interface Configuration
────────────────────────────────────
11. Configure LAN interface:
    HQ-R1(config)# interface GigabitEthernet0/0
    HQ-R1(config-if)# description LAN_Network
    HQ-R1(config-if)# ip address 192.168.1.1 255.255.255.0
    HQ-R1(config-if)# no shutdown

12. Configure WAN interface:
    HQ-R1(config)# interface Serial0/0/0
    HQ-R1(config-if)# description WAN_Link_to_ISP
    HQ-R1(config-if)# ip address 203.0.113.1 255.255.255.252
    HQ-R1(config-if)# no shutdown

PHASE 4 — Routing
───────────────────
13. Add default route to Internet:
    HQ-R1(config)# ip route 0.0.0.0 0.0.0.0 203.0.113.2

PHASE 5 — Remote Access (SSH)
───────────────────────────────
14. HQ-R1(config)# ip domain-name company.com
15. HQ-R1(config)# crypto key generate rsa modulus 2048
16. HQ-R1(config)# ip ssh version 2
17. HQ-R1(config)# username admin privilege 15 secret AdminPass!1
18. HQ-R1(config)# line vty 0 4
    HQ-R1(config-line)# login local
    HQ-R1(config-line)# transport input ssh
    HQ-R1(config-line)# exec-timeout 10 0

PHASE 6 — Monitoring Setup
────────────────────────────
19. Configure NTP:   HQ-R1(config)# ntp server 216.239.35.0
20. Configure syslog: HQ-R1(config)# logging 10.0.0.200
21. Configure SNMP:  HQ-R1(config)# snmp-server community public RO

PHASE 7 — Save Configuration
──────────────────────────────
22. HQ-R1# copy running-config startup-config

PHASE 8 — Verify Everything
─────────────────────────────
23. HQ-R1# show ip interface brief       ← All interfaces up/up?
24. HQ-R1# show ip route                 ← Routing table correct?
25. HQ-R1# ping 203.0.113.2              ← WAN gateway reachable?
26. HQ-R1# show version                  ← Config register = 0x2102?
```

---

### 4.2 How the Routing Decision Is Made — Packet Flow

```
Packet arrives at router interface
             │
             ▼
Is destination IP in the routing table?
             │
    ┌────────┴────────┐
   YES                NO
    │                  │
    ▼                  ▼
Is there a          Is there a default route (0.0.0.0/0)?
longest match?          │
    │              ┌───┴───┐
    │             YES      NO
    ▼              │       │
Forward via        │       ▼
best match         │  Send ICMP "Destination Unreachable"
(lowest AD,        │  back to sender — DROP packet
then metric)       │
                   ▼
             Forward via default route
```

---

## 5. Critical Numbers, Port Numbers & Key Values

| Name | Value | Purpose / Notes |
|------|-------|----------------|
| CDP Hello timer | **60 seconds** | How often CDP sends advertisements |
| CDP Hold timer | **180 seconds** | How long to keep neighbor info (3x hello) |
| SSH port | **22** | Remote management (encrypted) |
| Telnet port | **23** | Remote management (unencrypted — avoid) |
| SNMP GET/SET port | **UDP 161** | Agent listens here |
| SNMP Trap port | **UDP 162** | NMS trap receiver |
| TFTP port | **UDP 69** | Used for config/IOS backup and restore |
| NTP port | **UDP 123** | Time synchronization |
| Syslog port | **UDP 514** | Log message receiver |
| Syslog levels | **0–7** | 0 = most severe, 7 = debug (least severe) |
| AD — Connected | **0** | Most trusted |
| AD — Static | **1** | Second most trusted |
| AD — EIGRP | **90** | |
| AD — OSPF | **110** | |
| AD — RIP | **120** | |
| AD — Unknown | **255** | Never used for routing |
| RSA key (minimum) | **1024 bits** | For SSH; 2048 recommended |
| SSH version | **2** | Preferred; version 1 is insecure |
| VTY lines | **0–4** (5 lines) | Default concurrent remote sessions |
| exec-timeout default | **10 minutes** | Default VTY/console session idle timeout |
| Standard ACL range | **1–99** | Filters source IP only |
| Extended ACL range | **100–199** | Filters src IP, dst IP, protocol, port |
| Floating static AD | Any value **> primary route AD** | Used as backup route |
| Default route network | **0.0.0.0/0** | Matches any destination — gateway of last resort |
| NTP Stratum 0 | Atomic/GPS clock | Primary reference — not a network device |
| NTP Stratum 16 | **Unsynchronized** | Device has no valid time source |
| Config register (normal) | **0x2102** | Normal boot |
| Config register (recovery) | **0x2142** | Skip startup-config |

---

## 6. Important Terms & Definitions

| Term | Definition |
|------|-----------|
| **Routing Table** | Database in RAM listing all known networks and how to reach them |
| **Administrative Distance (AD)** | Rating of trustworthiness of a routing source — lower = more preferred |
| **Metric** | Cost used by a routing protocol to compare paths to the same destination |
| **Default Route** | A route (0.0.0.0/0) used when no more specific match exists — gateway of last resort |
| **Static Route** | A manually configured route that does not change unless an admin modifies it |
| **Floating Static Route** | A static route with a high AD — acts as backup to a dynamic route |
| **CDP** | Cisco Discovery Protocol — proprietary Layer 2 protocol to discover Cisco neighbors |
| **SSH** | Secure Shell — encrypted remote management protocol (port 22) |
| **Telnet** | Unencrypted remote management protocol (port 23) — avoid in production |
| **SNMP** | Simple Network Management Protocol — used for monitoring and management |
| **NMS** | Network Management Station — SNMP server that collects device data |
| **MIB** | Management Information Base — database of manageable objects on a device |
| **SNMP Trap** | Unsolicited alert sent from agent to NMS when an event occurs |
| **Syslog** | Standard logging protocol — collects and forwards device event messages |
| **NTP** | Network Time Protocol — synchronizes clocks across network devices |
| **Stratum** | NTP hierarchy level — Stratum 0 is the reference clock; higher = less accurate |
| **TFTP** | Trivial File Transfer Protocol — used for IOS/config backup (UDP, port 69) |
| **ACL** | Access Control List — ordered rules permitting or denying traffic on an interface |
| **Standard ACL** | Filters based on source IP address only (numbered 1–99) |
| **Extended ACL** | Filters based on source/destination IP, protocol, and port (numbered 100–199) |
| **Implicit Deny** | Hidden last rule in every ACL that denies all traffic not explicitly permitted |
| **Debug** | IOS command for real-time diagnostics — CPU-intensive, use sparingly |
| **Ping** | ICMP-based tool to test Layer 3 reachability between two devices |
| **Traceroute** | Tool to trace the hop-by-hop path of packets to a destination |
| **No Shutdown** | Interface command to administratively enable an interface |
| **exec-timeout** | Line configuration command setting the idle session timeout period |

---

## 7. Key Facts to Remember (Exam-Critical)

1. Router interfaces are **administratively shutdown by default** — always require `no shutdown`
2. **AD 0** = directly connected; **AD 1** = static; **AD 90** = EIGRP; **AD 110** = OSPF; **AD 120** = RIP
3. **Lower AD = more trusted** route; **lower metric = better path** within the same protocol
4. If **two routes** have the same AD, the one with the **lower metric** wins
5. The **routing table** is stored in **RAM** — rebuilt every time the router reboots
6. Default route syntax: `ip route 0.0.0.0 0.0.0.0 [next-hop]` — called **Gateway of Last Resort**
7. **CDP** is a **Layer 2**, **Cisco proprietary** protocol — hello every **60s**, hold time **180s**
8. **SSH requires**: domain name + RSA key + k9 IOS feature set + local authentication
9. **SSH version 2** is always preferred over version 1 — configured with `ip ssh version 2`
10. **SNMP** uses **UDP 161** (queries) and **UDP 162** (traps)
11. **Syslog levels 0–7**: 0=Emergency (most severe), 7=Debug (least severe)
12. **NTP Stratum 0** = atomic/GPS clock (not a network device); Stratum 16 = unsynced
13. **TFTP uses UDP port 69** — used for backing up and restoring IOS images and configs
14. **Standard ACL** (1–99) — filter by **source IP only** — place **near destination**
15. **Extended ACL** (100–199) — filter by src/dst IP + protocol + port — place **near source**
16. Every ACL has an invisible **implicit deny all** at the end — unmatched traffic is dropped
17. ACL rules processed **top to bottom** — **first match wins**, no further processing
18. **`show ip interface brief`** is the single most useful command for interface status overview
19. `copy running-config startup-config` saves config to **NVRAM**; if not saved, config lost on reload
20. **Floating static route** has a manually set high AD (e.g., 200) to act as a **backup route**

---

## 8. Common Comparisons & Differences

### 8.1 Static Routing vs Dynamic Routing

| Feature | Static Routing | Dynamic Routing |
|---------|--------------|----------------|
| Configuration | Manual by administrator | Automatic via routing protocol |
| Scalability | Poor — doesn't scale | Good — scales to large networks |
| Convergence | Immediate (no recalculation) | Takes time to converge after topology change |
| Overhead | None — no protocol traffic | Some — routing protocol updates consume bandwidth |
| Adaptability | None — fixed paths | Adapts automatically to topology changes |
| Use case | Small networks, stub networks, default routes | Medium to large networks |
| Admin overhead | High — manual updates for every change | Low — self-managing |

---

### 8.2 Standard ACL vs Extended ACL

| Feature | Standard ACL | Extended ACL |
|---------|-------------|-------------|
| Number range | 1–99, 1300–1999 | 100–199, 2000–2699 |
| Filters | Source IP only | Source IP, Destination IP, Protocol, Port |
| Granularity | Low | High |
| Placement | Near **destination** | Near **source** |
| Use case | Block entire host/subnet | Block specific service/protocol |

---

### 8.3 SNMP Versions

| Feature | SNMPv1 | SNMPv2c | SNMPv3 |
|---------|--------|---------|--------|
| Security | Community string only | Community string (plaintext) | Authentication + Encryption |
| Bulk transfer | No | Yes (GET-BULK) | Yes |
| Error handling | Basic | Improved | Improved |
| Encryption | No | No | **Yes** |
| Recommended | No | Widely used | **Yes — most secure** |

---

### 8.4 Ping vs Traceroute

| Feature | Ping | Traceroute |
|---------|------|-----------|
| Protocol | ICMP Echo Request/Reply | ICMP + UDP (or ICMP only) |
| Purpose | Test reachability | Trace hop-by-hop path |
| Information | Yes/No + latency | Each router hop + latency |
| OSI Layer | Layer 3 | Layer 3 |
| Use for | Quick connectivity test | Path analysis and fault isolation |

---

## 9. Commonly Confused Concepts — Danger Zone ⚠️

1. **AD vs Metric — they are not the same:**
   AD compares **different routing sources** (static vs OSPF vs RIP) — router uses the source with the lowest AD first. Metric compares **paths within the same routing protocol** — lower metric = better path. MCQs frequently describe one and ask for the other.

2. **Standard ACL near destination; Extended ACL near source:**
   Standard ACLs can only filter by source IP — if placed near the source, they might block traffic unnecessarily for ALL destinations. Extended ACLs specify exact destination and service, so placing them near the source stops unwanted traffic before it traverses the network.

3. **Implicit deny all — the invisible rule:**
   Every ACL automatically ends with `deny ip any any` even if you never write it. A common exam scenario: an ACL permits certain traffic but all other traffic is mysteriously being dropped — the implicit deny is the cause.

4. **CDP is Layer 2 — it does NOT need IP:**
   Because CDP operates at Layer 2, it works even on unconfigured interfaces with no IP address. This is why `show cdp neighbors` can reveal a neighbor's IP address even before you have configured routing between the devices.

5. **SNMP Trap vs SNMP GET — direction matters:**
   GET is initiated by the **NMS** → goes **to** the agent (polling). TRAP is initiated by the **agent** → goes **to** the NMS (unsolicited alert). MCQs ask about which direction specific operations travel.

6. **Syslog level 0 is the MOST severe — not level 7:**
   Many students assume higher number = more severe because that is intuitive. The opposite is true — level **0 (Emergency)** is the most critical; level **7 (Debug)** is the least. When you configure `logging trap warnings`, you receive levels 0 through 4 (warnings and above = more severe).

7. **`copy running startup` vs `copy startup running`:**
   `copy running-config startup-config` = **SAVES** current config (RAM → NVRAM). `copy startup-config running-config` = **RESTORES** saved config into RAM — does NOT replace running-config but **merges** it. Fully replacing requires an erase + reload.

8. **Default route is NOT the same as a default network:**
   `ip route 0.0.0.0 0.0.0.0 [next-hop]` = **default route** (matches any unknown destination). `ip default-network` = a different command for classful routing protocols. MCQs sometimes present both and ask which one is the Gateway of Last Resort mechanism.

---

## 10. Real-World Analogy

**Managing a router is like managing a post office distribution hub:**

A large post office hub (the router) receives packages (packets) from multiple delivery vans (interfaces), each van arriving from a different neighborhood (network/subnet).

- **Routing Table** = the sorting directory on the wall — tells staff which conveyor belt (outgoing interface) sends packages toward which ZIP code (destination network).
- **Static Route** = a handwritten instruction: "All packages for ZIP 10001 always go on Belt 3." Simple, fixed, and requires manual updating if ZIP codes change.
- **Default Route** = a catch-all bin: "If we don't know where it goes, send it to the central national hub." — the Gateway of Last Resort.
- **ACL** = a security checkpoint at the entrance: "Accept packages from residential areas, reject packages from unknown senders, check if the package is a letter (TCP 25) or a large parcel (HTTP)."
- **SNMP** = a CCTV monitoring system — the regional manager (NMS) watches all hub activity from headquarters, gets instant alerts (traps) when a conveyor belt (interface) breaks down.
- **Syslog** = the hub's incident log book — every event (package rejected, belt failure, staff login) is recorded with a timestamp and severity.
- **SSH** = the manager calling in securely from home — encrypted phone line so no one can eavesdrop on configuration instructions.

**In networking terms:** Every management function on a router has a direct operational equivalent — configuration, routing decisions, security enforcement, monitoring, and secure remote access all work together to make the hub (router) a reliable, secure, and observable piece of the network.

---

## 11. Quick Revision Summary

- **Router management** covers interface config, routing, remote access, monitoring, security, and backup/recovery
- Router interfaces are **shutdown by default** — activate with `no shutdown` after assigning IP
- The **routing table** (in RAM) determines how every packet is forwarded — built from connected, static, and dynamic routes
- **AD** ranks route sources (lower = better): Connected=0, Static=1, EIGRP=90, OSPF=110, RIP=120
- **Default route** `0.0.0.0/0` is the gateway of last resort — used when no specific match exists
- **CDP** (Layer 2, Cisco proprietary) discovers neighbors — hello 60s, hold 180s — no IP needed
- **SSH** (port 22, encrypted) is always preferred over **Telnet** (port 23, plaintext) for remote access
- **SNMP** uses UDP 161 (queries) and UDP 162 (traps) — SNMPv3 is the only secure version
- **Syslog** levels 0–7: 0=Emergency (worst), 7=Debug — `logging trap warnings` sends level 0–4
- **NTP** synchronizes time across devices — Stratum 0=atomic clock, Stratum 16=unsynced
- **TFTP (UDP 69)** is used to backup/restore configs and IOS images to/from a TFTP server
- **ACLs**: Standard (1–99, source IP only, near destination) vs Extended (100–199, full filter, near source) — every ACL ends with **implicit deny all**
- Always save: `copy running-config startup-config` — unsaved changes are lost on reboot
- `show ip interface brief` and `show ip route` are the two most essential verification commands
