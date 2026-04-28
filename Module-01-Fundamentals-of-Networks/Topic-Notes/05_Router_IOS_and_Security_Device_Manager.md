# Router IOS & Security Device Manager
## Module: Fundamentals of Networks

---

## 1. Introduction

### What Is Cisco IOS?
**Cisco IOS** (Internetwork Operating System) is the **proprietary operating system** that runs on Cisco routers and switches. Just as Windows runs on a PC or Android runs on a smartphone, IOS is the software that gives a Cisco router its intelligence — enabling it to route packets, apply security policies, manage interfaces, and be configured by network administrators.

IOS is a **command-line driven** operating system. Every configuration — from setting an IP address to enabling routing protocols — is done through typed commands in what is known as the **IOS CLI (Command Line Interface)**.

### What Is the Security Device Manager (SDM)?
**Cisco SDM** (Security Device Manager) is a **web-based GUI (Graphical User Interface)** tool that allows network administrators to configure and monitor Cisco routers **without needing to know CLI commands**. It runs directly on the router and is accessed through a web browser.

SDM was designed to make router configuration more accessible, particularly for:
- Security configurations (firewalls, VPNs, ACLs)
- Routing configurations
- Interface setup
- Basic network monitoring

### What Problem Do They Solve?
- **IOS** provides the full power of a Cisco router — every feature, every protocol, every security mechanism is accessible through IOS CLI
- **SDM** lowers the barrier to entry — administrators unfamiliar with CLI commands can still configure routers correctly through a guided, wizard-based interface

### Where They Fit in the Bigger Picture
IOS and SDM are the **management and control plane** of a Cisco router. Before a router can route a single packet, an administrator must configure it through IOS (CLI) or SDM (GUI). Understanding IOS is fundamental to every router-related topic: interfaces, routing protocols, NAT, ACLs, VLANs, and security.

---

## 2. Core Concepts & Detailed Explanation

### 2.1 Cisco IOS — Architecture and Access

#### How IOS Is Stored on a Router
A Cisco router stores IOS and configuration data in four types of memory:

| Memory Type | Contents | Volatile? |
|------------|---------|----------|
| **ROM** (Read-Only Memory) | Bootstrap program, POST (Power-On Self Test), ROM Monitor (ROMmon), Mini-IOS | No — permanent |
| **Flash** | Full IOS image (the operating system file) | No — retains on power off |
| **RAM** (Random Access Memory) | Running configuration, routing tables, ARP cache, packet buffers | **Yes** — lost on power off |
| **NVRAM** (Non-Volatile RAM) | Startup configuration (startup-config) | No — retains on power off |

**Critical distinction:**
- **Running-config** = the configuration currently active in RAM — **lost if router is powered off without saving**
- **Startup-config** = the saved configuration in NVRAM — **loaded when router boots**
- To save: `copy running-config startup-config` (or `write memory` / `wr`)

---

#### How to Access IOS CLI
There are multiple ways to connect to the IOS CLI:

| Access Method | Description | Requires Network? |
|--------------|-------------|-----------------|
| **Console Port** | Direct physical connection using a rollover (console) cable to the router's **console port** → laptop serial/USB port | **No** — out-of-band, works even if network is down |
| **Telnet** | Remote access over the network — **unencrypted**, sends all data including passwords in plaintext | Yes |
| **SSH** (Secure Shell) | Remote access over the network — **encrypted** — preferred method for remote access | Yes |
| **AUX Port** | Auxiliary port — used for dial-up modem access; rarely used today | No |

**Console access is always the starting point** for initial router configuration — before any network interfaces are configured.

---

### 2.2 IOS CLI — Modes of Operation

IOS operates in a **hierarchical mode structure**. Each mode has specific commands available and a specific **prompt** that identifies it.

#### Mode Hierarchy (Top to Bottom Access)

```
ROMMON Mode
    │
    ▼
User EXEC Mode         → Router>
    │
    ▼  (enable / en)
Privileged EXEC Mode   → Router#
    │
    ▼  (configure terminal / conf t)
Global Configuration   → Router(config)#
    │
    ├──► Interface Config    → Router(config-if)#
    ├──► Router Config       → Router(config-router)#
    ├──► Line Config         → Router(config-line)#
    └──► VLAN Config         → Router(config-vlan)#
```

---

#### Mode 1 — User EXEC Mode
**Prompt:** `Router>`

- **First mode** entered when connecting to a router
- **Very limited access** — only basic monitoring commands
- Cannot make any configuration changes
- Key commands: `ping`, `traceroute`, `show version` (limited), `enable`
- To exit: type `logout` or `exit`

---

#### Mode 2 — Privileged EXEC Mode (Enable Mode)
**Prompt:** `Router#`

- Accessed by typing `enable` (or `en`) from User EXEC mode
- **Full monitoring access** — can view all show commands
- Can **erase, copy, and manage** configurations
- **Cannot make interface/protocol configurations** directly — must enter Global Config for that
- Key commands: `show running-config`, `show startup-config`, `copy`, `debug`, `reload`, `erase`
- Protected by **enable password** or **enable secret** (encrypted)
- To exit back to User EXEC: `disable`

---

#### Mode 3 — Global Configuration Mode
**Prompt:** `Router(config)#`

- Accessed by typing `configure terminal` (or `conf t`) from Privileged EXEC
- Changes made here **affect the entire router globally**
- Used to set hostname, passwords, routing protocols, static routes, etc.
- Key commands: `hostname`, `ip route`, `router rip`, `no ip domain-lookup`, `banner motd`
- To exit: `end` (returns to Privileged EXEC) or `Ctrl+Z`

---

#### Mode 4 — Interface Configuration Mode
**Prompt:** `Router(config-if)#`

- Accessed from Global Config by typing `interface [type] [number]`
- Example: `interface GigabitEthernet0/0` or `interface fa0/0`
- Used to configure specific router interfaces (IP address, speed, duplex, shutdown/no shutdown)
- Key commands: `ip address`, `no shutdown`, `description`, `speed`, `duplex`, `encapsulation`
- To exit to Global Config: `exit`; To exit all the way: `end` or `Ctrl+Z`

---

#### Mode 5 — Router Configuration Mode
**Prompt:** `Router(config-router)#`

- Accessed from Global Config by typing `router [protocol]`
- Example: `router rip`, `router ospf 1`, `router eigrp 100`
- Used to configure dynamic routing protocols
- Key commands: `network`, `version`, `passive-interface`, `default-information originate`

---

#### Mode 6 — Line Configuration Mode
**Prompt:** `Router(config-line)#`

- Accessed from Global Config by typing `line [type] [number]`
- Examples: `line console 0`, `line vty 0 4`
- Used to configure access lines — console, Telnet/SSH (VTY lines)
- Key commands: `password`, `login`, `transport input ssh`, `exec-timeout`

---

#### Mode 7 — ROMMON Mode (ROM Monitor)
**Prompt:** `rommon >`

- Special low-level mode accessed when IOS fails to boot or during password recovery
- Used for **password recovery**, **IOS recovery** from flash, and changing the **configuration register**
- Accessed by: interrupting the boot sequence (usually `Ctrl+Break` during first 60 seconds of boot)
- Key commands: `confreg 0x2142` (bypass startup-config), `boot`, `dir flash:`

---

### 2.3 Essential IOS Commands — Reference

#### System Information Commands (Privileged EXEC)
| Command | Purpose |
|---------|---------|
| `show version` | IOS version, hardware info, uptime, configuration register |
| `show running-config` | Current active configuration in RAM |
| `show startup-config` | Saved configuration in NVRAM |
| `show interfaces` | Status and statistics for all interfaces |
| `show ip interface brief` | Quick summary of all interfaces — IP, status, protocol |
| `show ip route` | Routing table |
| `show ip protocols` | Active routing protocols and their configuration |
| `show arp` | ARP table (IP-to-MAC mappings) |
| `show cdp neighbors` | Directly connected Cisco devices (CDP) |
| `show flash` | Contents of flash memory (IOS image files) |
| `show processes cpu` | CPU utilization |
| `show memory` | Memory usage |

#### Configuration Commands (Global Config)
| Command | Purpose |
|---------|---------|
| `hostname [name]` | Set router hostname |
| `enable secret [password]` | Set encrypted Privileged EXEC password |
| `enable password [password]` | Set unencrypted Privileged EXEC password (legacy) |
| `service password-encryption` | Encrypts all plaintext passwords in config |
| `no ip domain-lookup` | Stops router from trying to DNS-resolve mistyped commands |
| `banner motd # [message] #` | Sets Message of the Day banner |
| `ip route [network] [mask] [next-hop]` | Add a static route |
| `no shutdown` | Enables an interface (interfaces are shutdown by default on routers) |

#### Saving and Managing Configuration
| Command | Purpose |
|---------|---------|
| `copy running-config startup-config` | Save RAM config to NVRAM |
| `write memory` / `wr` | Same as above (shorthand) |
| `copy startup-config running-config` | Load saved config into RAM |
| `erase startup-config` | Delete NVRAM configuration |
| `reload` | Reboot the router |

---

### 2.4 IOS Password Security

There are multiple levels of password protection in IOS:

| Password Type | Command | Stored as | Protects |
|--------------|---------|----------|---------|
| **Console password** | `line console 0` → `password [pw]` → `login` | Plaintext (unless service password-encryption) | Console port access |
| **VTY password** | `line vty 0 4` → `password [pw]` → `login` | Plaintext (unless encrypted) | Telnet/SSH access |
| **Enable password** | `enable password [pw]` | **Plaintext** in config | Privileged EXEC access |
| **Enable secret** | `enable secret [pw]` | **MD5 encrypted** always | Privileged EXEC access |

> **Key Rule:** If both `enable password` and `enable secret` are configured, **enable secret takes precedence** and enable password is ignored.

> **Best Practice:** Always use `enable secret` over `enable password`. Always use `service password-encryption` to encrypt all stored plaintext passwords.

---

### 2.5 Configuration Register

The **configuration register** is a 16-bit value stored in NVRAM that controls how the router boots.

| Value | Meaning |
|-------|---------|
| `0x2102` | **Normal boot** — load IOS from flash, load startup-config from NVRAM (default) |
| `0x2142` | **Bypass startup-config** — used during **password recovery** (loads IOS but ignores NVRAM config) |
| `0x2100` | Boot into **ROMMON mode** |
| `0x2101` | Boot from **Mini-IOS** in ROM |

To view: `show version` (last line shows "Configuration register is 0x2102")
To change: `config-register 0x2142` (Global Config mode)

---

### 2.6 Cisco SDM — Security Device Manager

#### What Is SDM?
**SDM** is a **Java-based, browser-accessible web GUI** for configuring Cisco routers. It was Cisco's primary GUI tool for IOS-based routers before being largely succeeded by **Cisco Configuration Professional (CCP)** and later **Cisco DNA Center**.

SDM is embedded directly in the router's flash memory and accessed via a web browser at the router's IP address (typically `http://192.168.1.1` or the router's interface IP).

#### Key Features of SDM
- **Wizards** for common configurations — no CLI knowledge required
- **Security Audit Wizard** — scans router configuration and identifies security weaknesses
- **VPN Wizard** — step-by-step IPSec VPN configuration
- **Firewall Wizard** — configures ACL-based firewall rules
- **Routing Configuration** — configure static/dynamic routes
- **Interface Configuration** — assign IP addresses, set speed/duplex
- **NAT Configuration** — configure Network Address Translation
- **Real-time monitoring** — view interface statistics, CPU, memory, routing table

#### How SDM Works
1. Router must have an **IP address configured on an interface**
2. Router must have **HTTP or HTTPS server enabled**: `ip http server` / `ip https server`
3. Administrator opens a browser and navigates to the router's IP address
4. SDM loads a Java applet — authentication with router's username/password
5. Administrator uses wizards and GUI panels to configure router features
6. SDM **translates GUI actions into IOS CLI commands** and pushes them to the router

#### SDM vs CLI Comparison

| Feature | SDM (GUI) | IOS CLI |
|---------|-----------|---------|
| Interface | Graphical (browser-based) | Text-based (command line) |
| Ease of use | Easy — wizard-driven | Requires command knowledge |
| Speed | Slower (multiple clicks) | Faster (for experienced admins) |
| Flexibility | Limited to SDM features | Full access to all IOS features |
| Security audit | Built-in Security Audit Wizard | Manual review of config |
| VPN setup | Guided wizard | Manual commands |
| Real-time monitoring | Yes | Via show commands |
| Required knowledge | Basic networking | IOS command syntax |

---

## 3. Key Components / Types / Categories

### 3.1 IOS File Naming Convention

IOS image files stored in flash follow a naming convention:
```
c2900-universalk9-mz.SPA.151-4.M4.bin
```

| Part | Meaning |
|------|---------|
| `c2900` | Hardware platform (Cisco 2900 series router) |
| `universalk9` | Feature set (universal + crypto/encryption support) |
| `mz` | File location (m = runs from RAM; z = compressed) |
| `SPA` | Digitally signed image |
| `151-4.M4` | IOS version (15.1(4)M4) |
| `.bin` | Binary executable file |

---

### 3.2 IOS Feature Sets (Trains/Packages)

| Feature Set | Description |
|------------|-------------|
| **IP Base** | Basic IP routing, RIP, OSPF, EIGRP |
| **Security** | Firewall, IDS/IPS, VPN, SSH |
| **Data** | Advanced routing, MPLS, BGP |
| **Universal** | All features in one image (most modern IOS versions) |
| **k9** suffix | Includes cryptography/encryption (required for SSH, VPN) |

---

### 3.3 Router Interface Types

| Interface Type | Description |
|--------------|-------------|
| **FastEthernet (Fa)** | 100 Mbps — e.g., `FastEthernet0/0` |
| **GigabitEthernet (Gi/Gig)** | 1 Gbps — e.g., `GigabitEthernet0/0` |
| **Serial (Se)** | WAN connections — e.g., `Serial0/0/0` |
| **Loopback (Lo)** | Virtual/logical interface — e.g., `Loopback0` — always up, used for testing |
| **Tunnel** | Virtual interface for VPN tunnels |
| **Null0** | Virtual interface — packets routed here are discarded (used as black hole) |

---

### 3.4 Interface Status Combinations

The `show ip interface brief` command shows two status columns:

| Status | Protocol | Meaning |
|--------|----------|---------|
| up | up | Interface is **fully operational** ✅ |
| up | down | Layer 1 OK, Layer 2 problem (encapsulation mismatch, keepalive failure) |
| down | down | Layer 1 problem — cable unplugged, other end shut down |
| administratively down | down | Interface has been manually shut down with `shutdown` command |

---

## 4. How It Works — Step by Step

### 4.1 Router Boot Sequence

```
Power On
    │
    ▼
Step 1 — POST (Power-On Self Test)
    Runs from ROM
    Tests CPU, memory, interfaces
    │
    ▼
Step 2 — Load Bootstrap Program
    Runs from ROM
    Determines where to find and load IOS
    │
    ▼
Step 3 — Locate and Load IOS
    Checks configuration register
    Typically loads IOS from FLASH memory
    Decompresses IOS into RAM
    │
    ▼
Step 4 — Locate and Load Configuration
    Looks for startup-config in NVRAM
    If found → loads it as running-config
    If NOT found → enters Setup Mode (initial config dialog)
    │
    ▼
Step 5 — Ready
    Router is operational
    Prompt appears: Router>
```

---

### 4.2 Initial Router Configuration — Step by Step

```
Step 1: Connect console cable (rollover cable)
        Router console port → PC COM/USB port
        Open terminal emulator (PuTTY/TeraTerm)
        Settings: 9600 baud, 8 data bits, no parity, 1 stop bit, no flow control

Step 2: Enter Privileged EXEC
        Router> enable
        Router#

Step 3: Enter Global Configuration
        Router# configure terminal
        Router(config)#

Step 4: Set hostname
        Router(config)# hostname R1
        R1(config)#

Step 5: Set enable secret (encrypted)
        R1(config)# enable secret cisco123

Step 6: Configure console line password
        R1(config)# line console 0
        R1(config-line)# password consolepass
        R1(config-line)# login
        R1(config-line)# exit

Step 7: Configure VTY lines (Telnet/SSH)
        R1(config)# line vty 0 4
        R1(config-line)# password vtypass
        R1(config-line)# login
        R1(config-line)# exit

Step 8: Encrypt all plaintext passwords
        R1(config)# service password-encryption

Step 9: Configure interface
        R1(config)# interface GigabitEthernet0/0
        R1(config-if)# ip address 192.168.1.1 255.255.255.0
        R1(config-if)# no shutdown
        R1(config-if)# exit

Step 10: Save configuration
        R1# copy running-config startup-config
        Destination filename [startup-config]? [Enter]
        Building configuration... [OK]
```

---

### 4.3 Password Recovery Procedure (IOS Router)

```
Step 1: Power off router, then power on
Step 2: Within 60 seconds of boot, press Ctrl+Break
        → Enters ROMMON mode (rommon>)
Step 3: Change config register to bypass startup-config
        rommon> confreg 0x2142
Step 4: Reload router
        rommon> reset
Step 5: Router boots without startup-config → no passwords
        Router> enable  (no password required)
        Router#
Step 6: Copy startup-config to running-config to restore settings
        Router# copy startup-config running-config
Step 7: Change the password
        Router(config)# enable secret newpassword
Step 8: Restore config register to normal boot
        Router(config)# config-register 0x2102
Step 9: Save configuration
        Router# copy running-config startup-config
Step 10: Reload router — now boots normally with new password
        Router# reload
```

---

### 4.4 Accessing SDM — Step by Step

```
Step 1: Ensure router has an IP address on an interface (e.g., 192.168.1.1)

Step 2: Enable HTTP/HTTPS server on the router (CLI)
        Router(config)# ip http server
        Router(config)# ip http secure-server
        Router(config)# ip http authentication local

Step 3: Create a local username and password
        Router(config)# username admin privilege 15 secret adminpass

Step 4: From admin PC (connected to router's LAN)
        Open web browser
        Navigate to: https://192.168.1.1

Step 5: Accept SSL certificate warning (if any)

Step 6: Log in with configured username/password

Step 7: SDM loads — use wizards or panels to configure:
        - Basic Setup (hostname, IP, routing)
        - Firewall Wizard
        - VPN Wizard
        - Security Audit
        - Monitoring Dashboard
```

---

## 5. Critical Numbers, Port Numbers & Key Values

| Name | Value | Purpose / Notes |
|------|-------|----------------|
| Console baud rate | **9600 bps** | Default speed for console connection |
| Console data bits | **8** | Standard serial setting |
| Console stop bits | **1** | Standard serial setting |
| Console parity | **None** | Standard serial setting |
| Config register (normal) | **0x2102** | Standard boot — loads IOS + startup-config |
| Config register (recovery) | **0x2142** | Bypasses startup-config for password recovery |
| Config register (ROMmon) | **0x2100** | Forces boot to ROMMON |
| VTY lines | **0–4** (5 lines) | Allows up to 5 simultaneous Telnet/SSH sessions (default) |
| VTY lines (extended) | **0–15** (16 lines) | Some platforms support up to 16 concurrent sessions |
| HTTP port | **80** | SDM access via HTTP |
| HTTPS port | **443** | SDM access via HTTPS (recommended) |
| Enable secret encryption | **MD5** | Algorithm used to hash enable secret password |
| service password-encryption | **Type 7** | Weak Vigenère cipher — encrypts console/VTY/enable passwords |
| Enable secret | **Type 5** | MD5 hash — much stronger than Type 7 |
| Privilege level (admin) | **15** | Highest privilege level in IOS (full access) |
| Privilege level (user) | **1** | Default lowest level (User EXEC) |
| Privilege levels range | **0–15** | 16 levels total |
| Loopback interface | **Lo0** | Always up/up — never goes down unless manually shut |
| IOS stored in | **Flash** | Non-volatile; retains IOS image after power off |
| Running config stored in | **RAM** | Volatile; lost after power off if not saved |
| Startup config stored in | **NVRAM** | Non-volatile; survives power off |

---

## 6. Important Terms & Definitions

| Term | Definition |
|------|-----------|
| **IOS** | Internetwork Operating System — Cisco's proprietary OS for routers and switches |
| **CLI** | Command Line Interface — text-based interface for entering IOS commands |
| **SDM** | Security Device Manager — Cisco's web-based GUI for router configuration |
| **User EXEC Mode** | Initial CLI mode (Router>) — limited read-only commands |
| **Privileged EXEC Mode** | Full monitoring mode (Router#) — accessed via `enable` |
| **Global Configuration Mode** | Mode for router-wide changes (Router(config)#) — accessed via `configure terminal` |
| **Interface Config Mode** | Mode for configuring a specific interface (Router(config-if)#) |
| **ROMMON** | ROM Monitor — low-level recovery mode used for password/IOS recovery |
| **Running-config** | Active configuration stored in RAM — lost on power off without saving |
| **Startup-config** | Saved configuration in NVRAM — loaded at boot |
| **Flash Memory** | Non-volatile storage holding the IOS image file |
| **NVRAM** | Non-Volatile RAM — stores startup-config; retains data without power |
| **Configuration Register** | 16-bit value controlling router boot behavior |
| **Console Port** | Physical port for direct out-of-band management access |
| **VTY Lines** | Virtual Terminal Lines — used for Telnet and SSH remote access |
| **Enable Secret** | MD5-encrypted password protecting Privileged EXEC mode |
| **Enable Password** | Plaintext (legacy) password for Privileged EXEC — overridden by enable secret |
| **service password-encryption** | Global command that encrypts all plaintext passwords using Type 7 |
| **no shutdown** | Command to bring an interface up (enable it) |
| **Loopback Interface** | Virtual interface — always in up/up state; used for testing and routing |
| **Privilege Level** | Access permission level (0–15); 15 = full admin access |
| **POST** | Power-On Self Test — hardware diagnostic run during router boot |
| **Bootstrap** | Program in ROM that locates and loads the IOS image |
| **Rollover Cable** | Flat cable used for console access — pins are reversed end-to-end |
| **Wizard** | Step-by-step guided configuration process in SDM |

---

## 7. Key Facts to Remember (Exam-Critical)

1. **IOS** stands for **Internetwork Operating System** — Cisco's proprietary router/switch OS
2. IOS is stored in **Flash memory**; running-config in **RAM**; startup-config in **NVRAM**
3. The **four memory types**: ROM (bootstrap/POST), Flash (IOS), RAM (running-config), NVRAM (startup-config)
4. **RAM is volatile** — running-config is lost on power off unless saved
5. Default console settings: **9600 baud, 8 data bits, no parity, 1 stop bit**
6. CLI mode hierarchy: **User EXEC (>) → Privileged EXEC (#) → Global Config (config#) → Sub-modes**
7. Enter Privileged EXEC: `enable`; Exit: `disable`
8. Enter Global Config: `configure terminal`; Exit all the way: `end` or `Ctrl+Z`
9. **enable secret** is always **MD5 encrypted** (Type 5); **enable password** is **plaintext** (unless service password-encryption)
10. If both **enable secret and enable password** are set, **enable secret always wins**
11. **service password-encryption** uses **Type 7** (weak cipher) — protects against casual shoulder surfing, not serious attacks
12. Save config command: `copy running-config startup-config` OR `write memory` (`wr`)
13. **Config register 0x2102** = normal boot; **0x2142** = skip startup-config (password recovery)
14. Password recovery requires entering **ROMMON mode** via **Ctrl+Break** during boot
15. **no shutdown** is required to bring up a router interface — router interfaces are **shutdown by default**
16. **SDM** requires: IP address on interface + `ip http server` enabled + local username configured
17. SDM translates GUI actions into **IOS CLI commands** — it does not bypass IOS
18. **VTY lines 0–4** allow **up to 5 simultaneous** remote (Telnet/SSH) sessions by default
19. `show ip interface brief` — most useful single command to check all interface statuses at once
20. **Loopback interface** is always **up/up** — never goes down; used for stable routing IDs and testing

---

## 8. Common Comparisons & Differences

### 8.1 IOS CLI vs SDM

| Feature | IOS CLI | SDM |
|---------|---------|-----|
| Interface type | Text-based command line | Web browser GUI |
| Access method | Console, Telnet, SSH | HTTP / HTTPS (browser) |
| Ease of use | Requires command knowledge | Wizard-driven — user friendly |
| Speed (experienced admin) | Fast | Slower (multiple steps) |
| Full feature access | Yes — every IOS feature | No — limited to SDM features |
| Security audit | Manual | Built-in Security Audit Wizard |
| VPN configuration | Manual commands | Guided VPN wizard |
| Real-time monitoring | `show` commands | Dashboard with graphs |
| Network requirement | Console = no network needed | **Requires network access to router** |

---

### 8.2 Running-Config vs Startup-Config

| Feature | Running-Config | Startup-Config |
|---------|---------------|---------------|
| Storage location | **RAM** | **NVRAM** |
| Volatile? | **Yes** — lost on power off | **No** — survives power off |
| Loaded when? | Active immediately when changed | Loaded at boot |
| View command | `show running-config` | `show startup-config` |
| Modify | Direct configuration commands | Only via `copy running startup` |

---

### 8.3 Enable Password vs Enable Secret

| Feature | Enable Password | Enable Secret |
|---------|----------------|--------------|
| Encryption | **Plaintext** (unless service password-encryption) | Always **MD5 encrypted** (Type 5) |
| Strength | Weak | Strong |
| Recommended? | No — legacy | **Yes — always use this** |
| Priority | Overridden by enable secret | **Takes precedence** |
| Type number | Type 0 (plain) or Type 7 (encrypted) | Type 5 (MD5) |

---

### 8.4 Console vs Telnet vs SSH Access

| Feature | Console | Telnet | SSH |
|---------|---------|--------|-----|
| Encryption | N/A (physical) | **None** — plaintext | **Encrypted** |
| Requires network? | **No** | Yes | Yes |
| Physical cable needed? | Yes (rollover cable) | No | No |
| Security level | High (physical access) | Low | High |
| Recommended for remote? | No | No | **Yes** |
| Port | N/A | **23** | **22** |
| IOS requirement | None | Basic IOS | IOS with **k9** (crypto) feature set |

---

## 9. Commonly Confused Concepts — Danger Zone ⚠️

1. **RAM vs NVRAM — which stores which config:**
   Students regularly swap these. Remember: **RAM = Running** (active, volatile, lost on reboot); **NVRAM = Not Volatile = startup** (saved, permanent). A helpful trick: **R**AM = **R**unning; **N**VRAM = **N**ot volatile = startup.

2. **enable password vs enable secret — which one is used:**
   If only `enable password` is configured → it is used. If only `enable secret` is configured → it is used. If **both are configured → enable secret always takes precedence** and enable password is completely ignored. MCQs love to ask which password is prompted when both exist.

3. **service password-encryption encrypts ALL passwords — but weakly:**
   Type 7 (used by service password-encryption) is easily reversible with freely available tools online. It only hides passwords from casual viewing of the config. Enable secret (Type 5/MD5) is genuinely strong. Do not assume service password-encryption provides strong security.

4. **no shutdown — router interfaces are shutdown by default:**
   Unlike switch ports (which are up by default), **router interfaces are administratively shutdown by default**. A common mistake is configuring an IP address and forgetting `no shutdown` — the interface will show "administratively down" and will not pass traffic.

5. **Ctrl+Z vs exit — different behavior:**
   `exit` — moves back **one level** in the CLI hierarchy. `end` (or `Ctrl+Z`) — jumps **all the way back** to Privileged EXEC mode from any sub-mode. Confusing these wastes time in configurations.

6. **SDM requires network connectivity to the router:**
   SDM is browser-based — it requires the admin's PC to reach the router's IP address over the network. Console access does not require any network connectivity. A router with no configured interfaces cannot be managed via SDM.

7. **Config register 0x2142 does not erase the startup-config:**
   During password recovery, setting the register to 0x2142 causes the router to **ignore** (not load) the startup-config. The startup-config is still in NVRAM. That is why the procedure copies startup-config to running-config **after** bypassing it — to restore all other settings while only changing the password.

8. **Flash stores IOS — not the configuration:**
   Flash memory holds the **IOS image file** (.bin). The **configuration** is NOT stored in flash. Startup-config goes to NVRAM; running-config lives in RAM. MCQs often mix up which memory holds what.

---

## 10. Real-World Analogy

**IOS is the Operating System of a Router — like Windows on a PC:**

Think of a Cisco router like a specialized computer:
- **ROM** = the BIOS on a motherboard — runs first, tests hardware, starts the boot process
- **Flash** = the hard drive / SSD — stores the operating system (IOS image)
- **RAM** = the working memory — where IOS runs and where your active documents (running-config) live
- **NVRAM** = a USB stick plugged in permanently — saves your important document (startup-config) even when the computer is off

When you **turn on your PC**, the BIOS (ROM) runs first, then loads Windows (IOS) from the hard drive (Flash) into RAM, and then loads your user profile/settings (startup-config from NVRAM). If you make changes but don't save — they vanish when you reboot (running-config lost from RAM).

**SDM** is like the **Control Panel or Settings app** on Windows — it provides a friendly GUI so you don't need to type commands directly into a terminal. The underlying changes still happen in the OS (IOS), but the interface shields you from the complexity.

**In networking terms:** Just as Windows manages your PC's hardware through a graphical interface while Command Prompt gives you full raw control, IOS CLI gives full raw router control while SDM provides a guided graphical alternative for common tasks.

---

## 11. Quick Revision Summary

- **Cisco IOS** is the proprietary OS running on Cisco routers and switches — all configuration is done through its **CLI** or via **SDM**
- Four memory types: **ROM** (bootstrap/POST), **Flash** (IOS image), **RAM** (running-config, volatile), **NVRAM** (startup-config, non-volatile)
- CLI mode hierarchy: **User EXEC (>)** → `enable` → **Privileged EXEC (#)** → `configure terminal` → **Global Config (config#)** → sub-modes
- **enable secret** (MD5, Type 5) is always preferred over **enable password** (plaintext); if both exist, **secret wins**
- `copy running-config startup-config` or `write memory` saves configuration to NVRAM
- **Router interfaces are shutdown by default** — always use `no shutdown` to activate them
- Console access settings: **9600 baud, 8N1** — works without any network connectivity
- **Config register 0x2102** = normal boot; **0x2142** = bypass startup-config (password recovery via ROMMON)
- **SDM** is a browser-based GUI wizard tool requiring HTTP/HTTPS server + local auth on the router
- `show ip interface brief` = fastest way to see all interface IPs and status in one view
- **SSH** (port 22, encrypted) is always preferred over **Telnet** (port 23, plaintext) for remote management
- VTY lines **0–4** support up to **5 simultaneous** remote management sessions by default
