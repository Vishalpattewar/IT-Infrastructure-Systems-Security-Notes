# VLAN (Virtual Local Area Network)
## Module: Fundamentals of Networks

---

## 1. Introduction

A **VLAN (Virtual Local Area Network)** is a logical subdivision of a physical switched network that groups devices into separate broadcast domains regardless of their physical location. Devices within the same VLAN communicate as if they are connected to the same physical switch, even when they are spread across different floors, buildings, or geographic locations — and devices in different VLANs cannot communicate directly without a Layer 3 device (router or Layer 3 switch).

### The Exact Problem It Solves
In a traditional flat switched network, every device is in the same broadcast domain. This creates three major problems:
1. **Broadcast storms**: A single broadcast (e.g., ARP) reaches every device on the network — wasting bandwidth and CPU on unrelated devices.
2. **Security weakness**: All devices can potentially "see" each other's traffic, making lateral movement trivial in a security breach.
3. **No logical segmentation**: You cannot separate HR from Engineering from Servers at Layer 2 without buying separate physical switches for each group.

VLANs solve all three: they split one physical switch into multiple virtual switches, each with its own broadcast domain, logical separation, and security boundary.

### Where It Fits in the OSI and TCP/IP Models
- **OSI Layer 2 — Data Link Layer**: VLANs are a Layer 2 technology. VLAN membership is enforced at Layer 2 by switches, using **802.1Q tagging** in Ethernet frames.
- **OSI Layer 3 — Network Layer (for inter-VLAN routing)**: Communication between VLANs requires a Layer 3 device. The VLAN itself is a Layer 2 construct, but routing between VLANs happens at Layer 3.
- The IEEE standard governing VLANs is **IEEE 802.1Q**, which defines the frame tagging mechanism that carries VLAN identity across trunk links.

### Why This Topic Is Foundational
- VLANs are the **cornerstone of modern enterprise network design**. Nearly every enterprise switch deployment uses VLANs.
- Without VLANs, large networks are unmanageable, insecure, and inefficient.
- Understanding VLANs is prerequisite knowledge for: inter-VLAN routing, STP, trunking, QoS, VoIP deployment, and network security segmentation.
- **Every** switch configuration exam question assumes VLAN knowledge.

---

## 2. Core Concepts & Detailed Explanation

### 2.1 What Is a Broadcast Domain?
A **broadcast domain** is the set of all devices that receive a broadcast frame (destination MAC: FF:FF:FF:FF:FF:FF) sent by any one of them. In a flat switched network, all devices are in one broadcast domain. VLANs create **separate broadcast domains at Layer 2** — a broadcast in VLAN 10 is never seen by a device in VLAN 20.

### 2.2 How VLANs Work — The Core Principle
A switch port is assigned to a VLAN. When a frame arrives on a port, the switch associates that frame with the port's VLAN membership. The switch **only forwards the frame to other ports in the same VLAN** — ensuring Layer 2 isolation between VLANs.

### 2.3 VLAN Membership Methods
There are two ways a port is assigned to a VLAN:

| Method | Description | Common Use |
|--------|-------------|-----------|
| **Static (Port-based)** | Administrator manually assigns each switch port to a VLAN | Most common; used in enterprise environments |
| **Dynamic** | VLAN assigned based on device MAC address, using a **VMPS (VLAN Membership Policy Server)** | Rare; largely obsolete |

In modern networks, **static port-based VLAN assignment** is the industry standard.

### 2.4 Access Ports
An **access port** (also called an **untagged port**) is a switch port assigned to a single VLAN. It carries traffic for only one VLAN. Devices connected to access ports (PCs, printers, IP phones) are unaware of VLANs — the switch handles VLAN membership transparently.

- Frames entering an access port are **untagged** (normal Ethernet frames).
- The switch internally **tags** the frame with the VLAN ID when processing it.
- Frames leaving an access port are **untagged** again (tag is stripped before delivery to the end device).

### 2.5 Trunk Ports
A **trunk port** is a switch port that carries traffic for **multiple VLANs simultaneously** between switches, between a switch and a router, or between a switch and a server. Trunk ports use **802.1Q tagging** to identify which VLAN each frame belongs to.

- Frames on a trunk link are **tagged** with a 4-byte 802.1Q header inserted into the Ethernet frame.
- The exception is the **native VLAN** — frames belonging to the native VLAN are sent **untagged** on trunk links by default.
- Trunk ports are used for **switch-to-switch** and **switch-to-router** links.

### 2.6 IEEE 802.1Q Frame Tagging
**IEEE 802.1Q** (published 1998, updated regularly) is the standard for VLAN tagging on Ethernet networks. It defines a **4-byte (32-bit) tag** inserted into the Ethernet frame between the Source MAC address and the EtherType/Length field.

```
Standard Ethernet Frame:
| Dest MAC (6B) | Src MAC (6B) | EtherType (2B) | Payload | FCS (4B) |

802.1Q Tagged Frame:
| Dest MAC (6B) | Src MAC (6B) | 802.1Q Tag (4B) | EtherType (2B) | Payload | FCS (4B) |
```

**802.1Q Tag Structure (4 bytes = 32 bits):**

```
|<-------- 4 bytes (32 bits) -------->|
| TPID (16 bits) | PCP (3) | DEI (1) | VID (12 bits) |
```

| Field | Size | Value | Purpose |
|-------|------|-------|---------|
| **TPID** (Tag Protocol ID) | 16 bits | 0x8100 | Identifies this as an 802.1Q tagged frame |
| **PCP** (Priority Code Point) | 3 bits | 0–7 | IEEE 802.1p class of service / QoS priority |
| **DEI** (Drop Eligible Indicator) | 1 bit | 0 or 1 | Formerly CFI; indicates if frame can be dropped under congestion |
| **VID** (VLAN Identifier) | 12 bits | 0–4095 | The VLAN ID; 12 bits allows 4096 values (0–4095) |

> The **12-bit VID** field is why the VLAN ID range is **0–4095** (2¹² = 4096 values), giving **4094 usable VLANs** (IDs 0 and 4095 are reserved).

### 2.7 Native VLAN
The **native VLAN** is the VLAN whose frames are sent **untagged** on a trunk link. When a trunk port receives an untagged frame, it assigns that frame to the native VLAN.

- **Default native VLAN on Cisco switches: VLAN 1**
- Both ends of a trunk link **must agree** on the native VLAN — a mismatch causes a **native VLAN mismatch** error and frames may be misassigned.
- The native VLAN is a potential **security vulnerability** (VLAN hopping attack) if left as the default VLAN 1 — best practice is to change the native VLAN to an unused VLAN ID.
- Configured on Cisco IOS with: `switchport trunk native vlan [vlan-id]`

### 2.8 VLAN Trunking Protocol (VTP)
**VTP (VLAN Trunking Protocol)** is a **Cisco proprietary** Layer 2 protocol that propagates VLAN configuration across all switches in a VTP domain, so administrators don't have to manually configure VLANs on every switch.

**VTP Modes:**

| Mode | Creates VLANs | Accepts Updates | Forwards Updates | Saves to NVRAM |
|------|--------------|----------------|-----------------|---------------|
| **Server** | Yes | Yes | Yes | Yes |
| **Client** | No | Yes | Yes | No |
| **Transparent** | Yes (local only) | No | Yes (passes through) | Yes |
| **Off** | Yes (local only) | No | No | Yes |

**VTP Versions:**

| Feature | VTPv1 | VTPv2 | VTPv3 |
|---------|-------|-------|-------|
| Extended VLAN support (1006–4094) | No | No | Yes |
| Private VLAN support | No | No | Yes |
| Transparent mode token ring | No | Yes | Yes |
| Authentication | MD5 | MD5 | SHA-2 |
| Primary/secondary server | No | No | Yes |

> **VTP Danger**: A new switch with a higher VTP revision number can **wipe out** all VLANs on a network when connected. Always reset VTP revision number before connecting a used switch to a production network.

### 2.9 Inter-VLAN Routing
Devices in different VLANs cannot communicate at Layer 2 — a Layer 3 device must route between them. There are three methods:

**Method 1 — Traditional (Legacy): Router with separate physical interface per VLAN.**
- One physical router interface connected to one switch port per VLAN.
- Requires a separate physical interface and switch port for each VLAN.
- Does not scale — impractical for many VLANs.

**Method 2 — Router on a Stick (ROAS):**
- One physical router interface divided into **sub-interfaces**, each assigned to one VLAN.
- The router-switch link is configured as a trunk.
- Single physical connection carries traffic for all VLANs.
- Each sub-interface has an IP address serving as the default gateway for its VLAN.
- Cisco IOS syntax: `interface GigabitEthernet0/0.10` → `encapsulation dot1Q 10` → `ip address 192.168.10.1 255.255.255.0`

**Method 3 — Layer 3 Switch (SVI — Switched Virtual Interface):**
- A **Layer 3 switch** (also called a multilayer switch) performs routing internally.
- An **SVI** is a virtual interface created for each VLAN on the Layer 3 switch.
- Each SVI acts as the default gateway for its VLAN.
- Much faster than ROAS — routing is done in hardware (ASIC).
- Cisco IOS syntax: `interface vlan 10` → `ip address 192.168.10.1 255.255.255.0`

### 2.10 Private VLANs (PVLANs)
**Private VLANs** (defined in **RFC 5517**, implemented per IEEE 802.1Q) allow further isolation **within** a single VLAN. Devices in the same VLAN can be isolated from each other at Layer 2.

**PVLAN Port Types:**

| Port Type | Can communicate with | Use case |
|-----------|---------------------|----------|
| **Promiscuous** | All ports in the PVLAN | Router/gateway port |
| **Isolated** | Promiscuous port only | Servers that must not talk to each other |
| **Community** | Community members + Promiscuous | Servers that share a function (e.g., web farm) |

**PVLAN VLAN Types:**
- **Primary VLAN**: The outer VLAN that contains the secondary VLANs.
- **Isolated VLAN**: Secondary VLAN; ports can only talk to promiscuous port.
- **Community VLAN**: Secondary VLAN; ports can talk to each other and to promiscuous port.

### 2.11 Voice VLANs
Modern switches support a **Voice VLAN** (also called **auxiliary VLAN**) on access ports connected to IP phones. This allows a single physical port to carry both data traffic (PC) and voice traffic (IP phone) in separate VLANs:

- The IP phone connects to the switch port.
- The PC connects to the PC port on the back of the IP phone.
- The switch port sends voice frames tagged with the **Voice VLAN ID**.
- The switch port sends data frames untagged in the **data VLAN** (access VLAN).
- Voice traffic receives QoS priority (PCP = 5 in the 802.1Q tag) for quality.

Cisco IOS configuration:
```
switchport mode access
switchport access vlan 10        (data VLAN for PC)
switchport voice vlan 20         (voice VLAN for IP phone)
```

---

## 3. Key Components / Types / Categories

### 3.1 VLAN ID Ranges — Complete Breakdown

| Range | Name | Description |
|-------|------|-------------|
| **0** | Reserved | Cannot be used; reserved by IEEE 802.1Q |
| **1** | Default VLAN | Factory default; all ports assigned here; also default native VLAN; cannot be deleted |
| **2 – 1001** | Normal Range VLANs | Standard usable VLANs; stored in **vlan.dat** (Flash); propagated by VTP |
| **1002** | fddi-default | Reserved for FDDI (Fiber Distributed Data Interface); cannot be deleted |
| **1003** | token-ring-default | Reserved for Token Ring; cannot be deleted |
| **1004** | fddinet-default | Reserved for FDDI Net; cannot be deleted |
| **1005** | trnet-default | Reserved for Token Ring Net; cannot be deleted |
| **1006 – 4094** | Extended Range VLANs | Used in large networks and service providers; stored in **running-config**; require VTP transparent or VTPv3; not propagated by VTPv1/v2 |
| **4095** | Reserved | Cannot be used; reserved by IEEE 802.1Q |

> **Total usable VLANs**: 1–4094 = **4094 VLANs** (0 and 4095 are reserved by IEEE).
> **Normal range usable**: 2–1001 = **1000 VLANs** (VLAN 1 exists but has restrictions; 1002–1005 reserved for legacy).
> **Extended range usable**: 1006–4094 = **3089 VLANs**.

### 3.2 VLAN Types by Purpose

| VLAN Type | Description | Example |
|-----------|-------------|---------|
| **Default VLAN** | VLAN 1; all ports start here; cannot be renamed or deleted | Factory-fresh switch |
| **Data VLAN** | Carries user-generated data traffic | HR VLAN, Engineering VLAN |
| **Native VLAN** | Untagged VLAN on a trunk link; default is VLAN 1; should be changed for security | Trunk links between switches |
| **Management VLAN** | VLAN used to access/manage the switch via SSH/Telnet/SNMP; typically not VLAN 1 | Admin VLAN (e.g., VLAN 99) |
| **Voice VLAN** | Dedicated VLAN for IP phone traffic; applies QoS | VoIP deployment |
| **Black Hole VLAN** | An unused VLAN to which unused ports are assigned; a security best practice | Unused ports → VLAN 999 |

### 3.3 Trunk Encapsulation Protocols

| Protocol | Standard | Status | Notes |
|----------|---------|--------|-------|
| **IEEE 802.1Q** | IEEE 802.1Q | Industry standard | 4-byte tag; supports native VLAN; used by all vendors |
| **ISL (Inter-Switch Link)** | Cisco proprietary | Deprecated | Encapsulates entire frame; 26-byte header + 4-byte trailer; no native VLAN concept; Cisco-only |

> **ISL vs. 802.1Q**: ISL is completely deprecated. All modern Cisco switches use **802.1Q only**. Some older exam questions reference ISL — it adds a 30-byte overhead (encapsulates the entire frame), while 802.1Q inserts only 4 bytes into the frame.

### 3.4 Dynamic Trunking Protocol (DTP)
**DTP** is a **Cisco proprietary** protocol that automatically negotiates trunk formation between Cisco switches.

| DTP Mode | Behavior |
|----------|----------|
| **Dynamic Auto** | Willing to become a trunk if the other side initiates; does NOT actively negotiate |
| **Dynamic Desirable** | Actively tries to become a trunk; will negotiate with Auto or Desirable |
| **Trunk** | Always a trunk; sends DTP frames; will form trunk with any mode |
| **Access** | Never a trunk; ignores DTP frames |
| **Nonegotiate** | Forces trunk but disables DTP; no DTP frames sent; used with non-Cisco devices |

**DTP Negotiation Results:**

| Switch A | Switch B | Result |
|----------|----------|--------|
| Trunk | Trunk | Trunk |
| Trunk | Dynamic Auto | Trunk |
| Trunk | Dynamic Desirable | Trunk |
| Dynamic Desirable | Dynamic Desirable | Trunk |
| Dynamic Desirable | Dynamic Auto | Trunk |
| Dynamic Auto | Dynamic Auto | **Access** (no trunk) |
| Access | Any | Access |

> **Security best practice**: Disable DTP on all access ports with `switchport nonegotiate` and `switchport mode access` to prevent VLAN hopping attacks.

---

## 4. How It Works — Step by Step

### 4.1 How a Frame Travels Within a VLAN (Access Port to Access Port)

```
[PC-A: VLAN 10]          [Switch SW1]               [Switch SW2]         [PC-B: VLAN 10]
192.168.10.10            Fa0/1 (access, VLAN 10)    Fa0/1 (access, VLAN 10)  192.168.10.20
     |                   Gi0/1 (trunk)               Gi0/1 (trunk)
     |                        |                           |
     |                        |                           |
```

**Step 1:** PC-A sends an untagged Ethernet frame destined for PC-B.

**Step 2:** Frame arrives at SW1's Fa0/1 (access port, VLAN 10). SW1 internally associates the frame with **VLAN 10**.

**Step 3:** SW1 checks its MAC address table. PC-B's MAC is reachable via the trunk port Gi0/1. SW1 **inserts the 802.1Q tag** (VLAN ID = 10) into the frame and forwards it out the trunk port Gi0/1.

**Step 4:** SW2 receives the tagged frame on its trunk port Gi0/1. It reads the 802.1Q tag: **VLAN 10**.

**Step 5:** SW2 checks its MAC table for PC-B's MAC within VLAN 10 — found on Fa0/1 (access port, VLAN 10). SW2 **strips the 802.1Q tag** and forwards the now-untagged frame out Fa0/1.

**Step 6:** PC-B receives a normal, untagged Ethernet frame — completely unaware that VLANs were involved.

### 4.2 How a Frame Travels Between VLANs (Inter-VLAN Routing via Router on a Stick)

```
[PC-A: VLAN 10]    [SW1]     [Trunk Link]    [Router R1]
192.168.10.10   ---Fa0/1-->  ---Gi0/1-----> G0/0.10 (encap dot1Q 10, IP: 192.168.10.1)
                                             G0/0.20 (encap dot1Q 20, IP: 192.168.20.1)
[PC-B: VLAN 20]    [SW1]
192.168.20.10  ---Fa0/2-->
```

**Step 1:** PC-A (192.168.10.10) wants to reach PC-B (192.168.20.10). Different subnet → sends frame to its **default gateway**: 192.168.10.1 (Router R1's sub-interface G0/0.10).

**Step 2:** SW1 receives frame on Fa0/1 (access, VLAN 10). Tags it VLAN 10. Forwards tagged frame up the trunk to Router R1.

**Step 3:** Router R1 receives tagged frame on G0/0. The **802.1Q tag (VLAN 10)** matches sub-interface G0/0.10. Router strips the tag, processes the IP packet.

**Step 4:** Router performs Layer 3 routing. Destination 192.168.20.10 is on the 192.168.20.0/24 network — reachable via sub-interface G0/0.20.

**Step 5:** Router sends the packet back down to SW1, **tagged with VLAN 20** (because G0/0.20 is configured with `encapsulation dot1Q 20`).

**Step 6:** SW1 receives the frame tagged VLAN 20 on the trunk. Finds PC-B's MAC in VLAN 20 on Fa0/2. Strips tag. Delivers untagged frame to PC-B.

### 4.3 VLAN Configuration on a Cisco Switch — Step by Step

**Step 1: Create the VLAN in the VLAN database.**
```
SW1(config)# vlan 10
SW1(config-vlan)# name Engineering
SW1(config-vlan)# exit

SW1(config)# vlan 20
SW1(config-vlan)# name HR
SW1(config-vlan)# exit
```

**Step 2: Assign access ports to VLANs.**
```
SW1(config)# interface FastEthernet 0/1
SW1(config-if)# switchport mode access
SW1(config-if)# switchport access vlan 10
SW1(config-if)# exit
```

**Step 3: Configure a trunk port (to another switch or router).**
```
SW1(config)# interface GigabitEthernet 0/1
SW1(config-if)# switchport trunk encapsulation dot1q     (required on some older switches)
SW1(config-if)# switchport mode trunk
SW1(config-if)# switchport trunk native vlan 99          (change native VLAN from default 1)
SW1(config-if)# switchport trunk allowed vlan 10,20,99   (restrict which VLANs traverse trunk)
SW1(config-if)# exit
```

**Step 4: Verify VLAN configuration.**
```
SW1# show vlan brief                    (shows all VLANs and port assignments)
SW1# show interfaces trunk              (shows trunk ports, allowed VLANs, native VLAN)
SW1# show interfaces Fa0/1 switchport   (shows detailed port VLAN info)
```

### 4.4 VLAN Hopping Attack — How It Works

**Attack Type 1 — Switch Spoofing:**
```
[Attacker PC] --- sends DTP frames ---> [Switch]
Switch negotiates trunk with attacker → Attacker gains access to ALL VLANs
```
An attacker configures their NIC to send DTP frames, causing the switch to form a trunk. The attacker then tags frames with any VLAN ID to access traffic from any VLAN.

**Prevention**: Disable DTP on all access ports (`switchport mode access` + `switchport nonegotiate`).

**Attack Type 2 — Double Tagging:**
```
[Attacker in Native VLAN] sends frame with TWO 802.1Q tags:
Outer tag: Native VLAN (e.g., 1) → stripped by first switch (untagged on native)
Inner tag: Target VLAN (e.g., 10) → forwarded as VLAN 10 by second switch
```
Works only when attacker is in the **native VLAN**. The outer tag is stripped by the first switch (native VLAN = untagged), and the inner VLAN 10 tag carries the frame to VLAN 10 on the next switch.

**Prevention**: Change native VLAN to an unused VLAN ID (not VLAN 1). Tag native VLAN traffic explicitly using `vlan dot1q tag native` (Cisco global command).

---

## 5. Critical Numbers & Key Values

| Name | Value / Range | Purpose / Notes |
|------|--------------|-----------------|
| VLAN ID minimum (IEEE) | 0 | Reserved by IEEE 802.1Q; cannot be used |
| VLAN ID maximum (IEEE) | 4095 | Reserved by IEEE 802.1Q; cannot be used |
| Total VLAN IDs (802.1Q VID field) | 4096 (0–4095) | 12-bit field → 2¹² = 4096 values |
| Total usable VLAN IDs | 4094 (1–4094) | Excluding reserved 0 and 4095 |
| Default VLAN | 1 | All ports assigned here by default; cannot be deleted or renamed (Cisco) |
| Native VLAN (default) | 1 | Untagged VLAN on trunk links; Cisco default; should be changed |
| Normal range VLANs | 2 – 1001 | Standard usable VLANs; stored in vlan.dat |
| Reserved legacy VLANs | 1002 – 1005 | FDDI, Token Ring; cannot be deleted on Cisco |
| Extended range VLANs | 1006 – 4094 | Requires VTP transparent mode or VTPv3 |
| Reserved VLAN (upper) | 4095 | Reserved by IEEE; cannot be used |
| 802.1Q tag size | 4 bytes (32 bits) | Inserted into Ethernet frame |
| 802.1Q TPID value | 0x8100 | Identifies 802.1Q tagged frame |
| VID field size | 12 bits | Allows 4096 VLAN IDs (0–4095) |
| PCP field size | 3 bits | 8 priority levels (0–7) for QoS (802.1p) |
| DEI field size | 1 bit | Drop Eligible Indicator |
| ISL header size | 26 bytes header + 4 byte trailer | Deprecated Cisco-proprietary trunking |
| ISL total overhead | 30 bytes | vs. 802.1Q's 4 bytes |
| Maximum frame size with 802.1Q tag | 1522 bytes | Standard 1518 + 4-byte 802.1Q tag |
| VTP domain modes | Server, Client, Transparent, Off | VTP version 3 adds Off mode |
| VoIP QoS priority (PCP) | 5 | 802.1p PCP value for voice traffic |
| VLAN 1 characteristics | Default, Native, Cannot delete/rename | Multiple special roles — a common exam trap |

---

## 6. Important Terms & Definitions

| Term | Definition |
|------|-----------|
| **VLAN (Virtual LAN)** | A logical grouping of network devices into a separate broadcast domain, independent of physical location, implemented at Layer 2 |
| **Broadcast Domain** | The set of all devices that receive a broadcast frame sent by any one device in that domain; VLANs create separate broadcast domains |
| **IEEE 802.1Q** | The IEEE standard for VLAN tagging on Ethernet networks; defines the 4-byte tag inserted into Ethernet frames on trunk links |
| **VLAN ID (VID)** | The 12-bit identifier in the 802.1Q tag that specifies which VLAN a frame belongs to; ranges from 0 to 4095 |
| **Access Port** | A switch port assigned to a single VLAN; carries untagged frames to/from end devices; strips and adds tags transparently |
| **Trunk Port** | A switch port that carries traffic for multiple VLANs simultaneously using 802.1Q tagging; used for switch-to-switch and switch-to-router links |
| **Native VLAN** | The VLAN whose frames are sent untagged on a trunk link; default is VLAN 1 on Cisco; must match on both ends of the trunk |
| **Default VLAN** | VLAN 1; the VLAN to which all switch ports belong before any configuration; cannot be deleted or renamed on Cisco switches |
| **802.1Q Tag** | The 4-byte field (TPID + PCP + DEI + VID) inserted into an Ethernet frame between the Source MAC and EtherType to carry VLAN membership information |
| **TPID (Tag Protocol ID)** | A 16-bit field with value 0x8100 that identifies an Ethernet frame as 802.1Q tagged |
| **PCP (Priority Code Point)** | A 3-bit field in the 802.1Q tag providing 8 levels (0–7) of QoS priority per IEEE 802.1p; VoIP uses priority 5 |
| **VTP (VLAN Trunking Protocol)** | A Cisco proprietary protocol that propagates VLAN configuration from a VTP server to all VTP clients in the same domain |
| **DTP (Dynamic Trunking Protocol)** | A Cisco proprietary protocol that automatically negotiates trunk links between Cisco switches |
| **ISL (Inter-Switch Link)** | A deprecated Cisco proprietary trunking protocol that encapsulates the entire Ethernet frame with a 26-byte header and 4-byte trailer |
| **Inter-VLAN Routing** | The process of routing traffic between different VLANs using a Layer 3 device (router or Layer 3 switch) |
| **Router on a Stick (ROAS)** | An inter-VLAN routing method using a single physical router interface divided into sub-interfaces, each handling one VLAN via a trunk link |
| **SVI (Switched Virtual Interface)** | A virtual Layer 3 interface on a Layer 3 switch created for a VLAN; serves as the default gateway for devices in that VLAN |
| **Sub-interface** | A logical division of a physical router interface; each sub-interface handles one VLAN with a specific 802.1Q encapsulation and IP address |
| **VLAN Hopping** | A network attack where an attacker sends frames that appear to belong to a different VLAN, bypassing VLAN isolation |
| **Double Tagging** | A VLAN hopping attack where the attacker inserts two 802.1Q tags; the outer tag (native VLAN) is stripped by the first switch, leaving the inner tag to deliver the frame to the target VLAN |
| **Private VLAN (PVLAN)** | A VLAN feature providing further Layer 2 isolation within a single VLAN, using promiscuous, isolated, and community port types |
| **Voice VLAN** | A dedicated VLAN for IP phone traffic on an access port; allows a single port to carry both data and voice in separate VLANs |
| **Management VLAN** | A dedicated VLAN used only for switch management traffic (SSH, Telnet, SNMP); separate from user data VLANs for security |
| **Black Hole VLAN** | An unused VLAN to which all unused switch ports are assigned, preventing unauthorized access to active VLANs |
| **vlan.dat** | The file stored in a Cisco switch's Flash memory containing the VLAN database (VLANs 1–1005) |

---

## 7. Key Facts to Remember (Exam-Critical)

1. **VLAN IDs range from 0 to 4095** — but 0 and 4095 are **reserved by IEEE 802.1Q** and cannot be used. Usable range: **1–4094**.
2. **VLAN 1 is the default VLAN** on all Cisco switches — all ports belong to VLAN 1 by default. It **cannot be deleted, renamed, or have its operation disabled**.
3. **The native VLAN is VLAN 1 by default** on Cisco trunk ports — frames in the native VLAN are sent **untagged** on trunk links. The native VLAN **must match** on both ends of a trunk or a mismatch error occurs.
4. **VLANs 1002–1005 are reserved** for legacy technologies (FDDI, Token Ring) on Cisco switches — they **cannot be deleted**.
5. **Normal range VLANs (2–1001)** are stored in **vlan.dat** in Flash memory and can be propagated by **VTPv1 and VTPv2**.
6. **Extended range VLANs (1006–4094)** require **VTP transparent mode** (or VTPv3) — they are stored in **running-config**, not vlan.dat, and are NOT propagated by VTPv1/v2.
7. **The 802.1Q tag is 4 bytes** inserted into the Ethernet frame; the **TPID is always 0x8100**; the **VID field is 12 bits** (which is why there are 4096 possible VLAN IDs).
8. **Maximum Ethernet frame size with 802.1Q tagging is 1522 bytes** (standard 1518 + 4-byte tag).
9. **ISL is deprecated** — Cisco's older proprietary trunking protocol adds 30 bytes of overhead vs. 802.1Q's 4 bytes. All modern Cisco switches use 802.1Q only.
10. **Inter-VLAN routing requires a Layer 3 device** — VLANs are isolated at Layer 2; a router or Layer 3 switch is needed for devices in different VLANs to communicate.
11. **Router on a Stick uses sub-interfaces** — one physical interface, multiple logical sub-interfaces; each uses `encapsulation dot1Q [vlan-id]` and has its own IP address.
12. **VTP Server mode** is the default VTP mode on Cisco switches. A switch with a **higher VTP revision number** will overwrite VLAN databases of lower-revision switches when connected — a major operational risk.
13. **VLAN hopping prevention**: Change native VLAN from VLAN 1 to an unused VLAN; disable DTP on access ports (`switchport mode access` + `switchport nonegotiate`); explicitly define allowed VLANs on trunk ports.
14. **Voice VLAN** uses PCP priority **5** in the 802.1Q tag to ensure voice quality over data traffic.
15. **`show vlan brief`** displays all VLANs and their assigned ports; **`show interfaces trunk`** displays trunk ports, their native VLAN, and allowed VLANs.

---

## 8. Common Comparisons & Differences

### 8.1 Access Port vs. Trunk Port

| Feature | Access Port | Trunk Port |
|---------|------------|-----------|
| VLANs carried | One | Multiple |
| Frame tagging | Untagged (tag added/stripped by switch) | Tagged (802.1Q) for all VLANs except native |
| Connected to | End devices (PCs, phones, printers) | Other switches, routers, servers |
| Native VLAN concept | N/A (only one VLAN) | Yes — untagged VLAN on trunk |
| DTP behavior | Should be `switchport mode access` | `switchport mode trunk` |
| Configuration command | `switchport access vlan [id]` | `switchport mode trunk` |

### 8.2 802.1Q vs. ISL

| Feature | 802.1Q | ISL |
|---------|--------|-----|
| Standard | IEEE (industry standard) | Cisco proprietary |
| Status | Active; current standard | Deprecated |
| Overhead | 4 bytes (inserted into frame) | 30 bytes (encapsulates entire frame) |
| Native VLAN | Yes (untagged VLAN on trunk) | No (all frames encapsulated) |
| Max frame size | 1522 bytes | Original frame + 30 bytes |
| Vendor support | All vendors | Cisco only |
| Max VLANs | 4094 | 1000 |

### 8.3 VTP Modes Compared

| Feature | Server | Client | Transparent | Off |
|---------|--------|--------|-------------|-----|
| Create/modify VLANs | Yes | No | Yes (local only) | Yes (local only) |
| Receive VTP updates | Yes | Yes | No | No |
| Forward VTP updates | Yes | Yes | Yes (passes through) | No |
| Save VLANs to NVRAM | Yes (vlan.dat) | No | Yes (running-config) | Yes (running-config) |
| Affects VTP domain | Yes | Yes | No | No |

### 8.4 Inter-VLAN Routing Methods

| Feature | Legacy (Separate Interfaces) | Router on a Stick (ROAS) | Layer 3 Switch (SVI) |
|---------|----------------------------|------------------------|---------------------|
| Physical connections | One per VLAN | One (trunk) | Internal |
| Scalability | Very poor | Moderate | Excellent |
| Performance | Limited by router | Limited by router + single link | High (hardware ASIC) |
| Cost | High (many interfaces/cables) | Low (one link) | Moderate (L3 switch) |
| Configuration | Separate interfaces | Sub-interfaces + encapsulation | SVIs (`interface vlan X`) |
| Use case | Legacy / lab | Small networks | Enterprise standard |

### 8.5 Normal Range vs. Extended Range VLANs

| Feature | Normal Range (1–1001) | Extended Range (1006–4094) |
|---------|----------------------|--------------------------|
| VLAN IDs | 1–1001 | 1006–4094 |
| Storage | vlan.dat (Flash) | running-config |
| VTP propagation | VTPv1, v2, v3 | VTPv3 only (or transparent mode) |
| VTP mode required | Server or Client | Transparent or VTPv3 server |
| Use case | Standard enterprise | ISP / large enterprise |

### 8.6 VLAN ID Special Values

| VLAN ID | Status | Description |
|---------|--------|-------------|
| 0 | Reserved (IEEE) | Cannot be assigned; used internally for 802.1p priority tagging without VLAN |
| 1 | Default / Special | Default VLAN; native VLAN default; cannot be deleted/renamed |
| 2–1001 | Normal range | Standard usable VLANs |
| 1002–1005 | Reserved (Cisco legacy) | FDDI/Token Ring; cannot be deleted |
| 1006–4094 | Extended range | Large-scale use; VTP transparent or VTPv3 |
| 4095 | Reserved (IEEE) | Cannot be assigned; internal use |

---

## 9. Commonly Confused Concepts — Danger Zone ⚠️

**1. Native VLAN vs. Default VLAN**
Students confuse these because both default to VLAN 1 on Cisco switches. The key difference is: the **default VLAN (VLAN 1)** is the VLAN to which all ports are assigned when the switch is new — it is a concept that applies to **access ports**; the **native VLAN** is the VLAN whose frames travel **untagged on trunk links** — it is a concept that applies specifically to **trunk ports**. They happen to both be VLAN 1 by default, but they are distinct concepts. Best practice is to change the native VLAN away from VLAN 1 while VLAN 1 remains the default access VLAN unless ports are reassigned.

**2. Normal Range (1–1001) vs. Extended Range (1006–4094) VLANs**
Students confuse these because they look like one continuous range. The key difference is: **normal range VLANs (2–1001)** are stored in **vlan.dat** in Flash and can be distributed by **VTPv1 and VTPv2**; **extended range VLANs (1006–4094)** are stored in **running-config**, require **VTP transparent mode or VTPv3**, and are NOT propagated by VTPv1/v2. Also note: VLANs 1002–1005 sit between the ranges and are **reserved** — they are not part of either the usable normal or extended range.

**3. 802.1Q Tagging vs. ISL Encapsulation**
Students confuse these because both are trunking protocols. The key difference is: **802.1Q inserts a 4-byte tag** into the existing Ethernet frame (modifying it); **ISL encapsulates the entire original Ethernet frame** inside a new frame with a 26-byte header and 4-byte trailer (the original frame is unchanged inside). ISL is deprecated and Cisco-only. 802.1Q is the universal standard and supports a native VLAN (untagged); ISL has no native VLAN concept (every frame is encapsulated).

**4. Access Port vs. Trunk Port Native VLAN**
Students get confused about where tags are added and removed. The key distinction is: **access ports** always deal with **untagged frames** — the switch adds the VLAN tag internally for processing and strips it before forwarding to the device; **trunk ports** forward tagged frames for all VLANs **except** the native VLAN, which is forwarded untagged. A mismatch in native VLAN on a trunk creates a serious problem where frames get silently reassigned to the wrong VLAN.

**5. VTP Server vs. VTP Transparent Mode**
Students confuse these because both can create VLANs locally. The key difference is: a **VTP Server** creates VLANs that are **propagated to all other switches** in the VTP domain — changes on a server affect the entire network; **VTP Transparent** creates VLANs that remain **local only** — they are not advertised to other switches (though the transparent switch still forwards VTP advertisements it receives, without applying them). Transparent mode is the safe choice in most production environments.

**6. Router on a Stick Sub-interface vs. SVI**
Students confuse these because both provide inter-VLAN routing IP addresses. The key difference is: a **ROAS sub-interface** (e.g., `G0/0.10`) is configured on an **external router** connected via a trunk — routing is done in software on the router, and all traffic must physically leave the switch, go to the router, and come back; an **SVI** (`interface vlan 10`) is configured on a **Layer 3 switch** — routing is done internally in hardware (ASIC), with no external link required, making SVIs far faster and more scalable.

---

## 10. Real-World Analogy

### The Office Building Floor Plan Analogy

Imagine a large office building where **all departments share the same floor** (one physical switched network). Without any separation, anyone can walk to any desk and overhear any conversation — HR salaries, engineering blueprints, executive strategies are all visible to everyone (broadcast domain = entire floor).

**VLANs are like installing invisible glass walls** that divide the floor into separate, sealed rooms — one for Engineering (VLAN 10), one for HR (VLAN 20), one for Finance (VLAN 30). People in Engineering can talk freely to each other but cannot hear HR conversations and cannot walk into HR's room. The rooms are **virtual** — the physical desks and cables don't move, but the logical groupings are enforced by the building's management system (the switch).

- **Access ports** are the **doors into each room** — when you walk in (connect your PC), you're placed in that room's VLAN automatically.
- **Trunk ports** are like **internal corridors or elevator shafts** that connect multiple floors (switches) — labeled packages (802.1Q tagged frames) travel through the corridor, each with a sticker showing which room (VLAN) they belong to.
- **The native VLAN** is like the **building lobby** — packages without a sticker are assumed to belong to the lobby (VLAN 1). This is why you should change the native VLAN — you don't want unlabeled packages accidentally going to the wrong room.
- **Inter-VLAN routing** is like the **reception desk (router)** — if Engineering needs to send a document to HR, they give it to reception (the router/Layer 3 switch), which reads the destination room number and officially delivers it to HR (different VLAN). You can't bypass reception and walk directly from Engineering to HR.
- **VTP** is like the **building management system** — when facilities (VTP server) adds a new room (VLAN), the update is automatically broadcast to all floors (switches) so everyone knows the new room exists.

**In networking terms, this maps to:** VLANs create logical network segments within a single physical switch infrastructure, controlling broadcast domains and isolating Layer 2 traffic. Trunk links carry multi-VLAN traffic between switches using 802.1Q tags, while Layer 3 routing enables controlled communication between VLANs just as a receptionist enables inter-department communication.

---

## 11. Quick Revision Summary

- **VLANs logically segment** a physical switched network into separate broadcast domains — devices in different VLANs cannot communicate at Layer 2 without routing.
- **VLAN ID range: 0–4095** (12-bit field); **usable: 1–4094**; 0 and 4095 are IEEE-reserved; VLAN 1 is the default; 1002–1005 are Cisco-reserved for legacy technologies.
- **Normal range VLANs (2–1001)** stored in vlan.dat; **extended range (1006–4094)** stored in running-config and require VTP transparent or VTPv3.
- **IEEE 802.1Q** is the universal trunking standard — inserts a **4-byte tag** (TPID 0x8100 + PCP 3 bits + DEI 1 bit + VID 12 bits) into Ethernet frames on trunk links.
- **Native VLAN (default: VLAN 1)** frames travel **untagged** on trunk links; must match on both ends; should be changed to an unused VLAN for security.
- **Access ports** carry one VLAN; **trunk ports** carry multiple VLANs using 802.1Q tags between switches and routers.
- **Inter-VLAN routing** requires Layer 3 — either **Router on a Stick** (sub-interfaces on external router) or **Layer 3 Switch SVIs** (faster, internal hardware routing).
- **VTP** propagates VLAN configuration across switches; modes are Server, Client, Transparent, Off — Transparent is safest in production.
- **VLAN hopping attacks** (switch spoofing, double tagging) are prevented by disabling DTP on access ports and changing the native VLAN from VLAN 1.
- **Security best practices**: separate management VLAN from data VLAN, assign unused ports to a black hole VLAN, explicitly define allowed VLANs on all trunk links, disable unused ports.
