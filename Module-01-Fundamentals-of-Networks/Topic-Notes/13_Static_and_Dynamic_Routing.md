# Static & Dynamic Routing
## Module: Fundamentals of Networks

---

## 1. Introduction

**Routing** is the process by which a router determines the best path for a packet to travel from its source to its destination across one or more networks. A router maintains a **routing table** — a database of known networks and the paths to reach them — and uses this table to make forwarding decisions on a per-packet basis.

### The Exact Problem It Solves
Without routing, packets could only travel within a single network. Routing allows packets to cross **multiple networks** (from your laptop → home router → ISP → internet → a web server in another country). Without routing protocols or static route configuration, routers would have no knowledge of networks beyond their directly connected interfaces and every inter-network communication would fail.

### Where It Fits in the OSI and TCP/IP Models
- **OSI Layer 3 — Network Layer**: Routing is a core function of Layer 3. Routers operate at Layer 3, reading IP headers to make forwarding decisions.
- **TCP/IP Layer 2 — Internet Layer**: In the TCP/IP stack, routing is the responsibility of the Internet layer, implemented by routers running the **Internet Protocol (IP)** and one or more routing protocols.
- Routing protocols themselves may use **UDP** (Layer 4) or operate directly over IP at Layer 3, depending on the protocol.

### Why This Topic Is Foundational
- **Without routing, the internet does not exist.** Routing is the mechanism that connects all networks together.
- Static routing is fundamental for small networks, stub networks, and default route configuration.
- Dynamic routing protocols allow networks to **automatically adapt** to failures, topology changes, and new links — essential for large-scale enterprise and ISP networks.
- Understanding **Administrative Distance (AD)**, **metrics**, **timers**, and **convergence** is critical for designing reliable, loop-free networks.

---

## 2. Core Concepts & Detailed Explanation

### 2.1 The Routing Table
A **routing table** (also called the **Routing Information Base, RIB**) is a data structure stored in a router's memory that contains entries mapping destination networks to next-hop addresses or exit interfaces. Every router maintains its own routing table.

Each routing table entry contains:
- **Destination network** (e.g., 192.168.2.0/24)
- **Subnet mask / prefix length**
- **Next-hop IP address** or **exit interface**
- **Administrative Distance (AD)**
- **Metric** (cost to reach the destination)
- **Route source** (connected, static, OSPF, EIGRP, etc.)
- **Timestamp** (how long the route has been known)

### 2.2 Directly Connected Routes
When a router interface is configured with an IP address and is active (up/up), the router **automatically adds** the connected network to its routing table. These routes have an **AD of 0** and a metric of 0 — they are the most trusted routes because the router is directly attached to that network.

### 2.3 Administrative Distance (AD)
**Administrative Distance** is a value (0–255) that represents the **trustworthiness** of the source of a routing update. When a router learns about the same destination network from multiple sources (e.g., both OSPF and EIGRP), it uses AD to select which route to install in the routing table.

**Lower AD = More trusted = Preferred route.**

- AD 255 means the route is **completely untrusted** and will never be installed.
- AD 0 means the route is **absolutely trusted** (directly connected).
- AD is a **local** value — it is not shared between routers. Each router applies its own AD values.

**Complete AD Table (Cisco IOS):**

| Route Source | Administrative Distance |
|-------------|------------------------|
| Directly Connected | 0 |
| Static Route | 1 |
| EIGRP Summary Route | 5 |
| External BGP (eBGP) | 20 |
| Internal EIGRP | 90 |
| IGRP (deprecated) | 100 |
| OSPF | 110 |
| IS-IS | 115 |
| RIP | 120 |
| EGP (deprecated) | 140 |
| ODR (On-Demand Routing) | 160 |
| External EIGRP | 170 |
| Internal BGP (iBGP) | 200 |
| Unknown / Untrusted | 255 |

### 2.4 Metric
A **metric** is the value a routing protocol uses to determine the **best path** among multiple paths to the same destination learned via the **same routing protocol**. Different routing protocols use different metric types.

- AD is used to compare routes from **different protocols**.
- Metric is used to compare routes from the **same protocol**.
- A **lower metric = better path** (for most protocols; BGP uses highest LOCAL_PREF).

### 2.5 Convergence
**Convergence** is the process by which all routers in a network reach a consistent, agreed-upon view of the network topology after a change (link failure, new link, router added). During convergence, some routes may be temporarily unavailable. **Fast convergence** is a key design goal.

### 2.6 Routing Protocol Classification

Routing protocols are classified along two axes:

**Axis 1 — Operation Scope:**
- **IGP (Interior Gateway Protocol)**: Operates within a single **Autonomous System (AS)** — the routing domain controlled by one organization. Examples: RIP, OSPF, EIGRP, IS-IS.
- **EGP (Exterior Gateway Protocol)**: Operates **between** Autonomous Systems — used on the internet between ISPs. Example: BGP.

**Axis 2 — Algorithm Type:**
- **Distance Vector**: Routers share their routing table with directly connected neighbors. Routers know the distance (metric) to destinations but not the full topology. Examples: RIP, EIGRP (advanced distance vector / hybrid).
- **Link State**: Routers share information about their directly connected links with ALL routers in the area. Each router builds a complete map of the topology and runs Dijkstra's SPF algorithm. Examples: OSPF, IS-IS.
- **Path Vector**: Tracks the full path (sequence of ASes) to destinations. Used in BGP.

### 2.7 Static Routing
A **static route** is a manually configured entry in the routing table. The administrator explicitly defines the destination network, subnet mask, and next-hop address or exit interface.

**Static Route Syntax (Cisco IOS):**
```
ip route [destination_network] [subnet_mask] [next-hop-IP | exit-interface] [AD]
```
Example:
```
ip route 192.168.2.0 255.255.255.0 10.0.0.2
```

**Types of Static Routes:**

| Type | Description | Example Use |
|------|-------------|------------|
| **Standard Static** | Specific destination network and next hop | Remote office network |
| **Default Static Route** | 0.0.0.0/0 — catch-all for unknown destinations | Gateway of last resort |
| **Summary Static Route** | One route represents multiple networks | Consolidating routes |
| **Floating Static Route** | Higher AD than a dynamic route — acts as backup | Redundancy/failover |
| **Recursive Static Route** | Next hop is not directly connected; router must look up the next hop | Multi-hop paths |
| **Directly Attached Static Route** | Uses exit interface instead of next-hop IP | Point-to-point links |

### 2.8 Dynamic Routing
**Dynamic routing protocols** automatically discover networks, calculate best paths, and update routing tables in response to topology changes — without manual administrator intervention on each router.

---

## 3. Key Components / Types / Categories

### 3.1 RIP — Routing Information Protocol

**RIP** is one of the oldest distance-vector IGPs, defined in **RFC 2453** (RIPv2). It uses **hop count** as its sole metric.

| Feature | RIPv1 | RIPv2 |
|---------|-------|-------|
| Standard | RFC 1058 | RFC 2453 |
| Classful/Classless | Classful | Classless (supports VLSM/CIDR) |
| Subnet mask in updates | No | Yes |
| Authentication | No | Yes (MD5) |
| Update method | Broadcast (255.255.255.255) | Multicast (224.0.0.9) |
| Max hop count | 15 | 15 |
| Metric | Hop count | Hop count |
| Update timer | 30 seconds | 30 seconds |
| Invalid timer | 180 seconds | 180 seconds |
| Hold-down timer | 180 seconds | 180 seconds |
| Flush timer | 240 seconds | 240 seconds |
| AD | 120 | 120 |
| Auto-summary | Yes (default) | Yes (default, can disable) |

### 3.2 OSPF — Open Shortest Path First

**OSPF** is a link-state IGP defined in **RFC 2328** (OSPFv2 for IPv4) and **RFC 5340** (OSPFv3 for IPv6). It uses **cost** (based on bandwidth) as its metric and runs Dijkstra's **Shortest Path First (SPF)** algorithm.

| Feature | Value / Detail |
|---------|---------------|
| Standard | RFC 2328 (v2), RFC 5340 (v3) |
| Algorithm | Dijkstra SPF |
| Metric | Cost = Reference bandwidth / Interface bandwidth |
| Default reference bandwidth | 100 Mbps |
| Hello interval (point-to-point / broadcast) | 10 seconds |
| Hello interval (NBMA networks) | 30 seconds |
| Dead interval | 4 × Hello interval (default: 40 seconds) |
| LSA flooding interval | 30 minutes (LSA refresh) |
| AD | 110 |
| Multicast address (all OSPF routers) | 224.0.0.5 |
| Multicast address (DR/BDR) | 224.0.0.6 |
| Transport protocol | IP Protocol 89 (directly over IP, not TCP/UDP) |
| Areas | Supports hierarchical areas; Area 0 = backbone |
| DR/BDR election | Required on broadcast/multi-access networks |

**OSPF Cost Calculation:**
```
Cost = Reference Bandwidth / Interface Bandwidth
Default Reference = 100,000,000 bps (100 Mbps)

FastEthernet (100 Mbps):  Cost = 100,000,000 / 100,000,000 = 1
GigabitEthernet (1 Gbps): Cost = 100,000,000 / 1,000,000,000 = 1 (rounds to minimum 1)
Serial (1.544 Mbps T1):   Cost = 100,000,000 / 1,544,000 = 64
```

> Note: Because GigabitEthernet and FastEthernet both calculate to 1 with the default reference bandwidth, the reference bandwidth is often increased on modern networks (e.g., `auto-cost reference-bandwidth 1000` for Gbps networks).

### 3.3 EIGRP — Enhanced Interior Gateway Routing Protocol

**EIGRP** is Cisco's proprietary advanced distance-vector (hybrid) protocol, standardized in **RFC 7868** (2016). It uses the **DUAL (Diffusing Update Algorithm)** to guarantee loop-free paths and fast convergence.

| Feature | Value / Detail |
|---------|---------------|
| Standard | RFC 7868 (previously Cisco proprietary) |
| Algorithm | DUAL (Diffusing Update Algorithm) |
| Metric | Composite: Bandwidth + Delay (default); also considers Load and Reliability |
| Hello interval (LAN) | 5 seconds |
| Hello interval (WAN/NBMA) | 60 seconds |
| Hold time (LAN) | 15 seconds |
| Hold time (WAN) | 180 seconds |
| AD (Internal) | 90 |
| AD (External) | 170 |
| AD (Summary) | 5 |
| Multicast address | 224.0.0.10 |
| Transport | RTP (Reliable Transport Protocol) over IP Protocol 88 |
| Max hop count | 100 (default); configurable up to 255 |
| Partial updates | Yes — only sends changes, not full table |
| Load balancing | Equal-cost AND unequal-cost (via variance) |

**EIGRP Metric Formula (Classic):**
```
Metric = [K1 × Bandwidth + (K2 × Bandwidth)/(256 − Load) + K3 × Delay] × [K5/(Reliability + K4)]

Default K values: K1=1, K2=0, K3=1, K4=0, K5=0
Simplified default formula:
Metric = (10^7 / Minimum_Bandwidth_kbps + Sum_of_Delays_in_tens_of_microseconds) × 256
```

**EIGRP Key Terms:**
- **Successor**: The best path to a destination (installed in routing table).
- **Feasible Successor (FS)**: A backup path that satisfies the **Feasibility Condition** (FC): the neighbor's reported distance must be less than the current Feasible Distance. Installed in the topology table, not routing table, but instantly available if the successor fails.
- **Feasible Distance (FD)**: The best metric from this router to the destination.
- **Reported Distance (RD)** / Advertised Distance (AD): The metric from a neighbor to the destination.

### 3.4 BGP — Border Gateway Protocol

**BGP** is the **EGP** that runs the internet. Defined in **RFC 4271**, it is a path-vector protocol that exchanges routing information between Autonomous Systems.

| Feature | eBGP (External BGP) | iBGP (Internal BGP) |
|---------|--------------------|--------------------|
| Between | Different ASes | Same AS |
| AD | 20 | 200 |
| TTL | 1 (directly connected peers by default) | 255 |
| Next-hop behavior | Changed to self | Unchanged |
| Transport | TCP port 179 | TCP port 179 |
| Metric (primary) | AS_PATH length (fewer ASes = better) | LOCAL_PREF (higher = better) |
| Full mesh required | No | Yes (or use route reflectors) |

### 3.5 IS-IS — Intermediate System to Intermediate System

**IS-IS** is a link-state IGP defined in **ISO 10589**, extended for IP in **RFC 1195**. Widely used by ISPs. Uses Dijkstra's SPF algorithm like OSPF.

| Feature | Value |
|---------|-------|
| Standard | ISO 10589, RFC 1195 |
| Metric | Cost (default: 10 per link; narrow metric max: 1023) |
| Hello interval | 10 seconds (default) |
| Hold time | 30 seconds (3 × hello) |
| AD | 115 |
| Runs directly over | Layer 2 (Data Link) — not IP |

### 3.6 Comparison of All Major Routing Protocols

| Feature | RIP | OSPF | EIGRP | IS-IS | BGP |
|---------|-----|------|-------|-------|-----|
| Type | Distance Vector | Link State | Advanced DV (Hybrid) | Link State | Path Vector |
| Scope | IGP | IGP | IGP | IGP | EGP |
| Standard | RFC 2453 | RFC 2328 | RFC 7868 | ISO 10589 | RFC 4271 |
| AD | 120 | 110 | 90 (int) / 170 (ext) | 115 | 20 (eBGP) / 200 (iBGP) |
| Metric | Hop count | Cost (bandwidth) | Composite (BW + Delay) | Cost | AS_PATH / LOCAL_PREF |
| Max hops | 15 | Unlimited | 100 (default) | Unlimited | Unlimited |
| Algorithm | Bellman-Ford | Dijkstra SPF | DUAL | Dijkstra SPF | Path selection |
| Hello interval | 30s | 10s (LAN) | 5s (LAN) | 10s | 60s (default) |
| Convergence | Slow | Fast | Very Fast | Fast | Slow |
| Scalability | Low | High | High | Very High | Internet-scale |
| Supports VLSM | RIPv2: Yes | Yes | Yes | Yes | Yes |
| Transport | UDP 520 | IP Proto 89 | IP Proto 88 | Layer 2 | TCP 179 |

---

## 4. How It Works — Step by Step

### 4.1 Static Routing — How a Packet Is Forwarded

```
[PC-A]           [Router R1]              [Router R2]           [PC-B]
192.168.1.10     Fa0/0: 192.168.1.1       Fa0/0: 10.0.0.2       192.168.2.10
                 Fa0/1: 10.0.0.1          Fa0/1: 192.168.2.1

Static route on R1: ip route 192.168.2.0 255.255.255.0 10.0.0.2
Static route on R2: ip route 192.168.1.0 255.255.255.0 10.0.0.1
```

**Step 1:** PC-A (192.168.1.10) sends a packet destined for 192.168.2.10. It determines the destination is on a different network and forwards it to its default gateway: R1 (192.168.1.1).

**Step 2:** R1 receives the packet. It examines the destination IP (192.168.2.10) and performs a **longest-prefix match** in its routing table.

**Step 3:** R1 finds the static route: `192.168.2.0/24 via 10.0.0.2`. It forwards the packet out Fa0/1 toward R2.

**Step 4:** R2 receives the packet. It performs a longest-prefix match and finds 192.168.2.10 is on its directly connected network (Fa0/1: 192.168.2.1/24).

**Step 5:** R2 delivers the packet directly to PC-B (192.168.2.10) using ARP to resolve the MAC address.

### 4.2 OSPF — Dynamic Routing Process (Step by Step)

```
Phase 1: Neighbor Discovery
Phase 2: Database Exchange (LSA flooding)
Phase 3: SPF Calculation
Phase 4: Routing Table Population
Phase 5: Ongoing Hello / Keepalive
```

**Phase 1 — Neighbor Discovery:**
1. Router sends **Hello packets** every 10 seconds (broadcast/P2P) to multicast **224.0.0.5**.
2. Hello contains: Router ID, Area ID, Hello/Dead intervals, network mask, neighbor list, DR/BDR info.
3. Two routers become **neighbors** when they agree on: Area ID, Hello/Dead intervals, subnet mask, authentication, stub area flag.

**Phase 2 — Database Exchange:**
1. Neighbors elect a **Master/Slave** relationship and exchange **DBD (Database Description)** packets listing their LSA headers.
2. Routers send **LSR (Link State Request)** for LSAs they don't have.
3. Neighbor responds with **LSU (Link State Update)** containing full LSA data.
4. Receiver sends **LSAck (Link State Acknowledgment)** to confirm receipt.
5. Both routers now have identical **LSDB (Link State Database)**.

**Phase 3 — SPF Calculation:**
1. Each router independently runs **Dijkstra's SPF algorithm** on the LSDB.
2. SPF builds a shortest-path tree rooted at the local router to every other router/network.

**Phase 4 — Routing Table Population:**
1. Best paths from the SPF tree are installed in the routing table with the calculated **cost** as the metric.

**Phase 5 — Ongoing:**
1. Routers continue sending Hello packets every 10 seconds to maintain neighbor adjacencies.
2. If a Hello is not received within the **Dead interval (40 seconds)**, the neighbor is declared down and SPF is recalculated.

### 4.3 EIGRP — DUAL Algorithm (Step by Step)

```
State: All routes calculated, Successor and FS identified

Event: Successor link goes down

Step 1: Router checks topology table for a Feasible Successor (FS)
Step 2a: FS found → Instantly promote FS to Successor (sub-second convergence)
Step 2b: No FS found → Enter ACTIVE state, send QUERY to all neighbors
Step 3: Neighbors reply with REPLY packets (their distance to destination)
Step 4: Router recalculates best path from REPLY data
Step 5: New Successor installed, route returns to PASSIVE state
```

**EIGRP Feasibility Condition (FC):**
```
A route qualifies as a Feasible Successor if:
Neighbor's Reported Distance (RD) < Local Feasible Distance (FD)

This guarantees the neighbor is closer to the destination → no routing loop possible
```

### 4.4 RIP — Distance Vector Operation

```
  [R1]----10.0.0.0/24----[R2]----20.0.0.0/24----[R3]----30.0.0.0/24----[R4]
```

1. **Initialization**: Each router knows only its directly connected networks (hop count = 0).
2. **First update (t=30s)**: Each router sends its full routing table to neighbors.
   - R1 learns 20.0.0.0/24 is 1 hop via R2.
   - R2 learns 30.0.0.0/24 is 1 hop via R3, etc.
3. **Second update (t=60s)**: Updates propagate further.
   - R1 learns 30.0.0.0/24 is 2 hops via R2.
4. This continues until all routers know all routes (convergence).
5. **Maximum hop count**: If a route reaches 16 hops, it is considered **unreachable** (infinity = 16).

**RIP Loop Prevention Mechanisms:**
- **Split Horizon**: Do not advertise a route back out the interface from which it was learned.
- **Route Poisoning**: When a route fails, advertise it with metric 16 (infinity) to immediately signal failure.
- **Poison Reverse**: Advertise the failed route back toward the source with metric 16 (overrides split horizon).
- **Hold-down Timer**: After receiving a route failure, ignore updates about that route for 180 seconds to allow the network to stabilize.
- **Triggered Updates**: Send immediate update when a route changes (don't wait for 30-second timer).

---

## 5. Critical Numbers & Key Values

| Name | Value / Range | Purpose / Notes |
|------|--------------|-----------------|
| AD — Directly Connected | 0 | Most trusted; router is on the network |
| AD — Static Route | 1 | Second most trusted |
| AD — EIGRP Summary | 5 | EIGRP summary routes |
| AD — eBGP | 20 | External BGP; between different ASes |
| AD — EIGRP Internal | 90 | Routes learned within the same EIGRP AS |
| AD — IGRP | 100 | Deprecated Cisco protocol |
| AD — OSPF | 110 | Open Shortest Path First |
| AD — IS-IS | 115 | Intermediate System to Intermediate System |
| AD — RIP | 120 | Routing Information Protocol |
| AD — External EIGRP | 170 | Routes redistributed into EIGRP from another protocol |
| AD — iBGP | 200 | Internal BGP; within the same AS |
| AD — Unknown/Untrusted | 255 | Route never installed in routing table |
| RIP max hop count | 15 | Route with 16 hops = unreachable (infinity) |
| RIP infinity metric | 16 | Signals unreachable destination |
| RIP update timer | 30 seconds | Full routing table sent every 30s |
| RIP invalid timer | 180 seconds | Route marked invalid if no update received |
| RIP hold-down timer | 180 seconds | Ignore updates about failed route for stability |
| RIP flush timer | 240 seconds | Route removed from table after 240s without update |
| RIPv1 multicast/broadcast | 255.255.255.255 | RIPv1 uses broadcast |
| RIPv2 multicast | 224.0.0.9 | RIPv2 uses multicast |
| RIP UDP port | 520 | Transport layer port for RIP |
| OSPF hello interval (LAN/P2P) | 10 seconds | Sent to 224.0.0.5 |
| OSPF hello interval (NBMA) | 30 seconds | On non-broadcast multi-access networks |
| OSPF dead interval (LAN) | 40 seconds | 4 × hello; neighbor declared down if expired |
| OSPF dead interval (NBMA) | 120 seconds | 4 × 30s hello |
| OSPF LSA refresh interval | 30 minutes (1800s) | LSAs re-flooded even without changes |
| OSPF reference bandwidth | 100 Mbps (default) | Used to calculate cost; adjustable |
| OSPF cost (FastEthernet) | 1 | 100Mbps / 100Mbps |
| OSPF cost (Serial/T1) | 64 | 100Mbps / 1.544Mbps |
| OSPF cost (Ethernet 10Mbps) | 10 | 100Mbps / 10Mbps |
| OSPF multicast (all routers) | 224.0.0.5 | Hello packets sent here |
| OSPF multicast (DR/BDR) | 224.0.0.6 | Updates sent to DR/BDR |
| OSPF IP protocol number | 89 | OSPF runs directly over IP |
| EIGRP hello (LAN) | 5 seconds | Fast hello for LAN links |
| EIGRP hello (WAN/NBMA) | 60 seconds | Slower hello for WAN links |
| EIGRP hold time (LAN) | 15 seconds | 3 × hello; neighbor declared down if expired |
| EIGRP hold time (WAN) | 180 seconds | 3 × hello |
| EIGRP max hop count (default) | 100 | Configurable up to 255 |
| EIGRP multicast | 224.0.0.10 | EIGRP hello and update multicast |
| EIGRP IP protocol number | 88 | EIGRP runs directly over IP |
| EIGRP AD (internal) | 90 | Internal EIGRP routes |
| EIGRP AD (external) | 170 | Redistributed routes |
| BGP TCP port | 179 | BGP uses TCP for reliable session |
| BGP hold time (default) | 180 seconds | Session drops if no BGP message in 180s |
| BGP keepalive interval | 60 seconds | Sent every 60s to maintain session |
| BGP AD (eBGP) | 20 | External BGP |
| BGP AD (iBGP) | 200 | Internal BGP |
| IS-IS hello interval | 10 seconds | Default |
| IS-IS hold time | 30 seconds | 3 × hello |
| IS-IS AD | 115 | Between OSPF (110) and RIP (120) |
| Floating static route AD | > dynamic protocol AD | Set higher than dynamic AD to act as backup |

---

## 6. Important Terms & Definitions

| Term | Definition |
|------|-----------|
| **Routing Table** | A data structure in a router listing known destination networks, the next-hop address or interface to reach them, and associated metrics and AD values |
| **Administrative Distance (AD)** | A value (0–255) representing the trustworthiness of a routing information source; lower = more preferred; used to choose between routes learned from different protocols |
| **Metric** | The value a routing protocol uses to determine the best path among multiple paths learned from the same protocol; lower is better (except BGP LOCAL_PREF) |
| **Static Route** | A manually configured routing table entry specifying the exact path to a destination network; does not adapt automatically to topology changes |
| **Default Route** | A static or dynamic route matching 0.0.0.0/0 — used when no more specific route exists; the "gateway of last resort" |
| **Floating Static Route** | A static route configured with a higher AD than a dynamic protocol, so it only becomes active if the dynamic route fails |
| **Dynamic Routing Protocol** | Software that automatically discovers networks, calculates best paths, and updates routing tables in response to topology changes |
| **IGP (Interior Gateway Protocol)** | A routing protocol used within a single Autonomous System; examples: RIP, OSPF, EIGRP, IS-IS |
| **EGP (Exterior Gateway Protocol)** | A routing protocol used between Autonomous Systems on the internet; example: BGP |
| **Distance Vector** | A routing algorithm where each router shares its full routing table with directly connected neighbors; routers know the distance (metric) to destinations but not the full topology |
| **Link State** | A routing algorithm where each router floods information about its directly connected links to all routers in the area; each router builds a complete topology map and runs SPF |
| **Convergence** | The process by which all routers in a network reach a consistent, synchronized view of the network topology after a change |
| **Hop Count** | The number of routers a packet must pass through to reach a destination; the metric used by RIP (max 15) |
| **Cost (OSPF)** | OSPF's metric, calculated as reference bandwidth divided by interface bandwidth; lower cost = faster link = better path |
| **DUAL (Diffusing Update Algorithm)** | EIGRP's loop-free convergence algorithm; guarantees loop-free paths at every instant using Feasibility Condition |
| **Successor** | In EIGRP, the neighbor providing the best (lowest metric) path to a destination; its route is installed in the routing table |
| **Feasible Successor** | In EIGRP, a backup neighbor whose Reported Distance is less than the current Feasible Distance; provides instant failover without re-querying |
| **Feasible Distance (FD)** | In EIGRP, the best total metric from the local router to a destination via the Successor |
| **Reported Distance (RD)** | In EIGRP, the metric a neighbor reports for reaching a destination (the neighbor's FD) |
| **SPF (Shortest Path First)** | Dijkstra's algorithm used by OSPF and IS-IS to calculate the shortest path tree from each router to all destinations |
| **LSA (Link State Advertisement)** | The information packet flooded by OSPF routers describing their directly connected links and states; stored in the LSDB |
| **LSDB (Link State Database)** | The complete database of LSAs maintained by each OSPF router; all routers in an area have identical LSDBs |
| **Autonomous System (AS)** | A collection of networks under the administrative control of a single organization, sharing a common routing policy |
| **Split Horizon** | A loop-prevention rule stating a router should not advertise a route back out the interface from which it was learned |
| **Route Poisoning** | Advertising a failed route with an infinite metric (16 for RIP) to immediately signal to neighbors that the route is unreachable |

---

## 7. Key Facts to Remember (Exam-Critical)

1. **AD is used to compare routes from different sources** (protocols); metric is used to compare routes from the same protocol.
2. **Lower AD = more preferred**: Connected (0) → Static (1) → eBGP (20) → EIGRP internal (90) → OSPF (110) → IS-IS (115) → RIP (120) → External EIGRP (170) → iBGP (200).
3. **RIP maximum hop count is 15**; a route with 16 hops is considered **unreachable** (metric = infinity).
4. **RIP sends full routing table every 30 seconds** (update timer); routes go invalid after **180 seconds**, are held down for **180 seconds**, and flushed at **240 seconds**.
5. **OSPF uses cost as its metric** = reference bandwidth (default 100 Mbps) / interface bandwidth. FastEthernet and Gigabit both calculate to cost 1 with default reference bandwidth.
6. **OSPF hello interval is 10 seconds** (LAN/P2P) and **30 seconds** (NBMA); dead interval is **4 × hello** (40s LAN, 120s NBMA).
7. **OSPF uses multicast 224.0.0.5** (all OSPF routers) and **224.0.0.6** (DR/BDR only); runs over IP Protocol 89.
8. **EIGRP uses composite metric** (bandwidth + delay by default); has AD of **90 (internal)** and **170 (external)**.
9. **EIGRP hello is 5 seconds (LAN) and 60 seconds (WAN)**; hold time is 3 × hello (15s LAN, 180s WAN).
10. **EIGRP Feasible Successor** provides instant failover (no re-convergence needed) when the Successor fails, as long as the Feasibility Condition is satisfied.
11. **BGP uses TCP port 179** and is the only EGP in common use; eBGP AD = 20, iBGP AD = 200.
12. **A floating static route** has its AD manually set higher than the dynamic routing protocol it backs up (e.g., `ip route 0.0.0.0 0.0.0.0 10.0.0.2 210` with AD 210 backs up iBGP's AD 200).
13. **IS-IS AD is 115** — between OSPF (110) and RIP (120); preferred over RIP, less preferred than OSPF on Cisco.
14. **AD 255 means "never install"** — this route will never appear in the routing table regardless of how it is learned.
15. **Directly connected routes have AD 0** — they are always the most trusted because the router is physically attached to that network.

---

## 8. Common Comparisons & Differences

### 8.1 Static vs. Dynamic Routing

| Feature | Static Routing | Dynamic Routing |
|---------|---------------|----------------|
| Configuration | Manual on every router | Automatic via protocol |
| Adapts to failures | No — admin must reconfigure | Yes — automatically reconverges |
| Administrative overhead | High (large networks) | Low (auto-discovery) |
| Resource usage | Very low (no CPU/RAM for protocol) | Higher (protocol processes, tables) |
| Security | More secure (no routing updates to intercept) | Less (updates can be spoofed without auth) |
| Best for | Small/stub networks, default routes | Large, complex, or changing networks |
| Convergence | Instant (no recalculation) | Varies by protocol |

### 8.2 Distance Vector vs. Link State vs. Path Vector

| Feature | Distance Vector | Link State | Path Vector |
|---------|----------------|-----------|------------|
| Topology knowledge | Partial (neighbors only) | Full (entire area) | AS paths |
| Update shared | Full routing table | LSAs (link info) | AS_PATH attributes |
| Algorithm | Bellman-Ford | Dijkstra SPF | Path selection rules |
| Convergence | Slower | Fast | Slow |
| Loop prevention | Split horizon, hold-down | SPF (inherently loop-free) | AS_PATH loop detection |
| Scalability | Low | High | Internet-scale |
| Examples | RIP, EIGRP (hybrid) | OSPF, IS-IS | BGP |

### 8.3 RIP vs. OSPF vs. EIGRP

| Feature | RIP | OSPF | EIGRP |
|---------|-----|------|-------|
| Type | Distance Vector | Link State | Advanced DV (Hybrid) |
| Metric | Hop count | Cost (bandwidth) | BW + Delay composite |
| Max hops | 15 | Unlimited | 100 (default) |
| AD | 120 | 110 | 90 |
| Hello timer | 30s | 10s (LAN) | 5s (LAN) |
| Convergence | Slow | Fast | Very fast |
| Standard | RFC 2453 | RFC 2328 | RFC 7868 |
| Transport | UDP 520 | IP Proto 89 | IP Proto 88 |
| Best for | Small/legacy | Enterprise | Cisco enterprise |

### 8.4 OSPF Hello Timers by Network Type

| Network Type | Hello Interval | Dead Interval |
|-------------|---------------|--------------|
| Point-to-Point | 10 seconds | 40 seconds |
| Broadcast (Ethernet) | 10 seconds | 40 seconds |
| NBMA (Frame Relay) | 30 seconds | 120 seconds |
| Point-to-Multipoint | 30 seconds | 120 seconds |

### 8.5 EIGRP Hello/Hold Timers by Link Type

| Link Type | Hello Interval | Hold Time |
|-----------|---------------|----------|
| LAN (Ethernet, etc.) | 5 seconds | 15 seconds |
| WAN / NBMA (T1 or slower) | 60 seconds | 180 seconds |

### 8.6 AD Values for Exam — Quick Reference

| Ranking | Protocol | AD |
|---------|---------|-----|
| 1st (best) | Directly Connected | 0 |
| 2nd | Static | 1 |
| 3rd | EIGRP Summary | 5 |
| 4th | eBGP | 20 |
| 5th | EIGRP Internal | 90 |
| 6th | OSPF | 110 |
| 7th | IS-IS | 115 |
| 8th | RIP | 120 |
| 9th | External EIGRP | 170 |
| 10th | iBGP | 200 |
| Worst | Unknown | 255 |

---

## 9. Commonly Confused Concepts — Danger Zone ⚠️

**1. Administrative Distance vs. Metric**
Students confuse these because both are "numbers that determine the best route." The key difference is: **AD** compares routes from **different protocols** (e.g., OSPF vs. RIP for the same destination) — lower AD wins; **Metric** compares routes from the **same protocol** (e.g., two OSPF paths to the same destination) — lower metric wins. AD is checked first; metric is only compared if AD values are equal.

**2. EIGRP Internal AD (90) vs. EIGRP External AD (170)**
Students confuse these because both are EIGRP. The key difference is: **internal EIGRP (AD 90)** applies to routes that originated within the EIGRP autonomous system; **external EIGRP (AD 170)** applies to routes that were **redistributed** into EIGRP from another protocol (e.g., a static route or OSPF route imported into EIGRP). External routes are less trusted because they came from outside EIGRP.

**3. RIP Invalid Timer (180s) vs. Hold-Down Timer (180s) vs. Flush Timer (240s)**
Students confuse these because they share similar values. The key differences are: **Invalid timer (180s)** — if no update for a route is received for 180s, the route is marked as invalid (metric set to 16) but stays in the table; **Hold-down timer (180s)** — after a route goes invalid, the router ignores any NEW updates about that route for 180s to prevent bad routes from being accepted too quickly; **Flush timer (240s)** — after 240s total without an update, the route is completely removed from the routing table.

**4. Successor vs. Feasible Successor (EIGRP)**
Students confuse these because both are EIGRP "backup" concepts. The key difference is: the **Successor** is the primary best path and IS installed in the routing table; the **Feasible Successor** is a pre-validated backup path stored in the EIGRP topology table (NOT the routing table) that can be instantly promoted without querying neighbors — but only if it exists. If no FS exists, EIGRP enters ACTIVE state and must query neighbors.

**5. OSPF 224.0.0.5 vs. 224.0.0.6**
Students confuse these because both are OSPF multicast addresses. The key difference is: **224.0.0.5** is the "All OSPF Routers" address — **every** OSPF router listens here and Hello packets are sent to this address; **224.0.0.6** is the "All DR/BDR Routers" address — only the **DR and BDR** on a broadcast network listen here, and DROther routers send LSU updates to this address (not to 224.0.0.5).

**6. eBGP (AD 20) vs. iBGP (AD 200)**
Students confuse these because both are BGP. The key difference is: **eBGP (external BGP, AD 20)** runs between routers in **different** Autonomous Systems — highly trusted because the information comes from a peer outside your organization; **iBGP (internal BGP, AD 200)** runs between routers in the **same** AS — given a very high AD because the routing information is considered less authoritative within the local network (IGPs like OSPF at 110 are preferred for internal routing).

---

## 10. Real-World Analogy

### The GPS Navigation System Analogy

Imagine a **city road network** and two types of drivers:

**Static routing** is like a **driver who memorizes a fixed route** before leaving home: "Turn left on Main Street, right on Oak Avenue, then take Highway 5." They know exactly where they're going and the route is fast and efficient — but if there's a road closure, they're stuck unless someone calls them and gives them a new route manually.

**Dynamic routing** is like a **driver using GPS with real-time traffic updates**: The GPS (routing protocol) automatically monitors all roads (links), calculates the best route based on current conditions (metric), and instantly reroutes when there's an accident (link failure). The GPS "talks" to other GPS units (routing protocol updates) to share traffic information.

**Administrative Distance** is like the driver's **trust in different navigation sources**: They trust the in-car GPS (AD 20) more than a stranger's verbal directions (AD 120), but trust their own eyes on a direct road they can see (AD 0) more than anything else.

**Metric** is like the GPS's **route scoring**: It calculates routes by fastest time, shortest distance, or fewest tolls — choosing the best path among alternatives offered by the same GPS system.

**Convergence** is the time it takes for **all GPS units in the city to agree** that a road is closed and find new routes — during which some drivers may temporarily take suboptimal paths.

**In networking terms, this maps to:** Routers use routing protocols (GPS) to automatically discover the best paths (routes) to destinations (cities). Administrative Distance determines which "navigation source" (protocol) to trust when multiple options conflict. Metrics score the available paths within a single protocol. When a link fails (road closure), dynamic protocols reconverge to find alternative paths, while static routes require manual reconfiguration.

---

## 11. Quick Revision Summary

- **Routing** is the Layer 3 process by which routers forward packets toward their destination by maintaining and consulting a routing table.
- **Static routes** are manually configured; they don't adapt to failures but use minimal resources and are most trusted (AD = 1).
- **Dynamic routing protocols** automatically discover networks and update routing tables; classified as IGP (RIP, OSPF, EIGRP, IS-IS) or EGP (BGP).
- **Administrative Distance (AD)**: Connected=0, Static=1, eBGP=20, EIGRP internal=90, OSPF=110, IS-IS=115, RIP=120, EIGRP external=170, iBGP=200, Unknown=255. Lower = more trusted.
- **RIP**: hop count metric, max 15 hops (16 = unreachable), updates every 30s, AD=120; RIPv2 uses multicast 224.0.0.9.
- **OSPF**: cost metric (bandwidth-based), hello=10s/dead=40s (LAN), multicast 224.0.0.5/224.0.0.6, IP Protocol 89, AD=110.
- **EIGRP**: composite metric (BW+Delay), hello=5s/hold=15s (LAN), uses DUAL algorithm with Successor + Feasible Successor for fast convergence, IP Protocol 88, AD=90 internal / 170 external.
- **BGP**: path-vector EGP between ASes, TCP port 179, eBGP AD=20 / iBGP AD=200; metric primarily based on AS_PATH length.
- **Floating static route**: static route with higher AD than a dynamic protocol, used as a backup route that only activates when the dynamic route fails.
- **Convergence speed** from fastest to slowest: EIGRP (sub-second with FS) → OSPF (seconds) → RIP (minutes) → BGP (minutes to hours).
