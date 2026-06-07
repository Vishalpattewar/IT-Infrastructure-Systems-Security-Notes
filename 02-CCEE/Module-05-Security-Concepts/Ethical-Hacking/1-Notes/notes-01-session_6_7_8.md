# 🛡️ Cybersecurity Study Notes — Sessions 6, 7 & 8

Personal notes I'm maintaining while studying ethical hacking and cybersecurity concepts.
Covering security management, wireless/mobile security, cyber law, and ethical hacking fundamentals.

---

## 📚 Table of Contents

- [Session 6 — Security Management & The Human Side](#session-6--security-management--the-human-side)
  - [What is Information Security](#1-what-is-information-security)
  - [Key Security Management Concepts](#2-key-security-management-concepts)
  - [Frameworks & Standards](#3-information-security-frameworks--standards)
  - [Information Assurance](#4-information-assurance-ia)
  - [Threat Intelligence Lifecycle](#5-threat-intelligence-lifecycle)
  - [Why Humans Are the Weakest Link](#6-why-humans-are-the-weakest-link)
  - [Insider Threats](#7-insider-threats)
  - [Social Engineering](#8-social-engineering--the-human-attack)
  - [Psychology of Social Engineering](#9-psychology-of-social-engineering)
  - [Security Awareness Training](#10-security-awareness-training)
  - [Information Classification](#11-classification-of-information)
  - [Threats Classification](#12-threats-to-information-systems--classification)
  - [Threat Actors in 2026](#13-threat-actors-in-2026)
  - [Types of Attacks](#14-types-of-attacks--classification)
  - [Incident Management](#15-incident-management-overview)
  - [Session 6 Key Takeaways](#-session-6--key-takeaways)
  - [Session 6 Glossary](#-session-6--glossary)
- [Session 7 — Protecting Info Systems, Wireless & Mobile Security](#session-7--protecting-info-systems-wireless--mobile-security)
  - [Layered Protection Model](#1-layered-protection-model)
  - [Network Security Controls](#2-network-security-controls)
  - [Mobile Security Landscape](#3-mobile-security-landscape-2026)
  - [Mobile Threats](#4-mobile-threats)
  - [Wireless Security](#5-wireless-security)
  - [Credit Card Fraud Types](#6-credit-card-fraud-types)
  - [PCI DSS v4.0](#7-payment-card-industry-data-security-standard-pci-dss-v40)
  - [Mobile Payment Security](#8-mobile-payment-security)
  - [ISMS](#9-information-security-management-system-isms)
  - [SOC 2026](#10-security-operations-center-soc--2026)
  - [BCP & DR](#11-business-continuity-planning-bcp--disaster-recovery-dr)
  - [Cryptography Fundamentals](#12-cryptography-fundamentals)
  - [Authentication Mechanisms](#13-authentication-mechanisms)
  - [Access Control Models](#14-access-control-models)
  - [Session 7 Key Takeaways](#-session-7--key-takeaways)
  - [Session 7 Glossary](#-session-7--glossary)
- [Session 8 — Cyber Crimes & Introduction to Ethical Hacking](#session-8--cyber-crimes--introduction-to-ethical-hacking)
  - [Definition of Cybercrime](#1-definition-of-cybercrime)
  - [Types of Cybercrimes](#2-types-of-cybercrimes-2026)
  - [Cybercrime & the Internet](#3-cybercrime-in-context-of-the-internet)
  - [Legal Aspects of Open Communications](#4-legal-aspects-of-open-communications)
  - [IT Act 2000](#5-information-technology-act-2000-it-act)
  - [IPC Sections](#6-indian-penal-code-ipc-sections-applicable-to-cybercrime)
  - [DPDPA 2023](#7-digital-personal-data-protection-act-2023-dpdpa)
  - [Fraud, Hacking, Mischief](#8-fraud-hacking-mischief-in-cyber-law)
  - [International Cyber Law](#9-international-cyber-law-framework)
  - [Jurisdiction Challenges](#10-jurisdiction-challenges-in-cyber-law)
  - [Obscenity Laws](#11-obscenity-and-pornography-on-the-internet)
  - [What is Ethical Hacking](#12-what-is-ethical-hacking)
  - [Ethical Hacking Terminology](#13-ethical-hacking-terminology)
  - [Types of Hackers](#14-types-of-hackers--comprehensive-classification)
  - [Hacking Technologies](#15-identifying-different-types-of-hacking-technologies)
  - [Five Phases of Ethical Hacking](#16-the-five-phases-of-ethical-hacking)
  - [Session 8 Key Takeaways](#-session-8--key-takeaways)
  - [Session 8 Glossary](#-session-8--glossary)
- [Topics Coming Up](#-topics-coming-up)
- [Tools & Practice Platforms](#-tools--practice-platforms)
- [Certifications Pathway](#-certifications-pathway)

---

## Session 6 — Security Management & The Human Side

### 1. What is Information Security

Information Security (InfoSec) is the practice of protecting information and information systems from unauthorized access, use, disclosure, disruption, modification, or destruction.

The three core pillars are the **CIA Triad**:

| Pillar | Definition | Example |
|---|---|---|
| **Confidentiality** | Info accessible only to authorized users | Encrypted emails, ACLs |
| **Integrity** | Accuracy and completeness of data maintained | Hash verification (MD5, SHA-256) |
| **Availability** | Systems and data accessible when needed | Load balancers, backups, DDoS protection |

**Extended Model (2026 — Beyond CIA Triad):**

| Property | Description |
|---|---|
| Authentication | Verifying identity of user or system |
| Non-Repudiation | Cannot deny having performed an action (digital signatures) |
| Authorization | Granting appropriate permissions post-authentication |
| Accountability | Tracing actions back to individuals (audit logs) |
| Privacy | Protecting personal data (DPDPA 2023, GDPR) |

---

### 2. Key Security Management Concepts

#### a) Risk Management

```
Risk = Threat × Vulnerability × Asset Value
```

**Risk Assessment:** Identify → Analyze → Evaluate → Treat → Monitor

**Risk Treatment Options:**

| Option | When to Use |
|---|---|
| **Accept** | Low impact — live with the risk |
| **Mitigate** | Reduce risk with controls |
| **Transfer** | Insurance, outsourcing |
| **Avoid** | Stop the risky activity entirely |

---

#### b) Security Policies

- **Organizational Security Policy** — High-level directives from management
- **System Security Policy** — Rules for specific systems
- **Issue-Specific Policy** — Password policy, email policy, BYOD policy
- **Acceptable Use Policy (AUP)** — Rules on how systems may be used

---

#### c) Security Controls

| Type | Examples |
|---|---|
| **Preventive** | Firewalls, encryption, access controls |
| **Detective** | IDS, audit logs, SIEM alerts |
| **Corrective** | Patch management, incident response |
| **Deterrent** | Warning banners, security cameras, penalties |
| **Compensating** | Backup controls when primary controls fail |
| **Recovery** | Backups, disaster recovery plans (DRP) |

---

#### d) Defense in Depth (DiD)

Layered security approach — no single point of failure.

```
Physical → Network → Host → Application → Data
```

If one layer fails, others continue to protect.

---

#### e) Principle of Least Privilege (PoLP)

- Users/systems get **only** the minimum permissions required
- Reduces attack surface significantly
- Example: Database admin should NOT have internet browsing access

---

#### f) Separation of Duties (SoD)

- Critical tasks require more than one person
- Prevents fraud and insider threats
- Example: Developer cannot also deploy to production

---

#### g) Security Through Obscurity (STO)

- Hiding system details as a security measure
- **NOT a standalone strategy** — must be combined with real controls
- Example: Hiding a login page URL

---

#### h) Zero Trust Architecture (ZTA) — 2026 Standard

> [!IMPORTANT]
> **"Never Trust, Always Verify"** — Every access request is authenticated, authorized, and continuously validated regardless of network location.

**Core Principles:**

- Verify explicitly (always authenticate and authorize)
- Use least privilege access
- Assume breach (design for containment)

**Key Technologies:** MFA, IAM, Micro-segmentation, PAM, SIEM

---

### 3. Information Security Frameworks & Standards

| Framework | Purpose |
|---|---|
| **ISO/IEC 27001** | ISMS — Information Security Management System |
| **NIST CSF 2.0** | Govern, Identify, Protect, Detect, Respond, Recover |
| **PCI DSS v4.0** | Payment Card Industry Data Security Standard |
| **HIPAA** | Health Insurance Portability & Accountability Act |
| **SOX** | Sarbanes-Oxley Act — Financial data integrity |
| **GDPR** | EU General Data Protection Regulation |
| **DPDPA 2023** | India's Digital Personal Data Protection Act |
| **IT Act 2000** | India's primary cyber law (amended 2008) |
| **COBIT 2019** | Governance of enterprise IT |
| **MITRE ATT&CK v15** | Adversary tactics, techniques, and procedures (TTPs) |

---

### 4. Information Assurance (IA)

Practice of ensuring information and information systems are protected from attack while ensuring authorized users can access data.

**5 Pillars of IA:** Integrity · Availability · Confidentiality · Authentication · Non-Repudiation

---

### 5. Threat Intelligence Lifecycle

| Phase | Activity |
|---|---|
| **1 — Direction** | Define intelligence requirements |
| **2 — Collection** | Gather raw data (OSINT, HUMINT, TECHINT) |
| **3 — Processing** | Normalize and filter raw data |
| **4 — Analysis** | Identify patterns, TTPs, threat actors |
| **5 — Dissemination** | Share intel with stakeholders |
| **6 — Feedback** | Refine based on consumer feedback |

**Threat Intelligence Feeds (2026):**
- STIX/TAXII (Structured Threat Info Expression)
- MISP (Malware Information Sharing Platform)
- VirusTotal, AlienVault OTX, Recorded Future

---

### 6. Why Humans Are the Weakest Link

> [!NOTE]
> Over 82% of data breaches involve a human element (Verizon DBIR 2025).
> Social engineering attacks increased by 43% in 2024–2025.
> Average cost of a human-caused breach: **USD $4.9 million**.

---

### 7. Insider Threats

A security threat originating from within the organization — typically a current or former employee, contractor, or business associate.

| Type | Description | Example |
|---|---|---|
| **Malicious Insider** | Intentionally causes harm | Employee selling customer data to a competitor |
| **Negligent Insider** | Unintentionally causes harm through carelessness | Clicking phishing emails, weak passwords |
| **Compromised Insider** | Account taken over by external attacker | Appears as legitimate user — detected by UEBA |
| **Third-Party/Vendor Risk** | Contractors with excessive access | Target breach (2013) — entry via HVAC vendor |

---

### 8. Social Engineering — The Human Attack

Psychological manipulation of people into performing actions or divulging confidential information.

| Attack Type | Description & Example |
|---|---|
| **Phishing** | Fraudulent emails to steal credentials — fake bank email asking to "verify account" |
| **Spear Phishing** | Targeted phishing at specific individuals — email appearing from CEO to CFO |
| **Whaling** | Phishing targeting C-suite executives |
| **Vishing** | Voice phishing — "I'm from IT support, need your password" |
| **Smishing** | SMS phishing — "Your parcel is held. Click to confirm." |
| **Pretexting** | Fabricated scenario to extract info — impersonating HR to get employee details |
| **Baiting** | Leaving infected USB drives in parking lots |
| **Tailgating/Piggybacking** | Following authorized person into restricted area |
| **Quid Pro Quo** | Offering something in exchange — free tech support for creds |
| **Deepfake Attacks** *(NEW 2024–26)* | AI-generated audio/video to impersonate execs — fake CFO video call authorizing wire transfer |

---

### 9. Psychology of Social Engineering

Attackers exploit these psychological triggers:

| Principle | How It's Used |
|---|---|
| **Authority** | "I'm the CEO/IT Director, do it now" |
| **Urgency** | "Act immediately or your account will be locked" |
| **Scarcity** | "Only 5 minutes before the system shuts down" |
| **Social Proof** | "Everyone in your department has already done this" |
| **Liking** | Building rapport before the actual request |
| **Reciprocity** | "I helped you last week, now I need this favor" |
| **Fear** | "We detected suspicious activity — verify now" |

---

### 10. Security Awareness Training

Effective SAT components:
- Regular phishing simulations
- Mandatory security training modules
- Clear incident reporting procedures
- Acceptable Use Policy acknowledgment
- Executive buy-in and leadership modeling
- Gamification and rewards for security behavior

> [!TIP]
> Security is everyone's responsibility — not just IT's.

---

### 11. Classification of Information

| Classification | Description |
|---|---|
| **Top Secret** | Highest protection — national security level |
| **Confidential** | Serious damage if disclosed — business critical |
| **Internal/Private** | For internal use — not for public |
| **Public** | No restriction — available to everyone |

**Data Handling Requirements:**

| State | Protection |
|---|---|
| Data at Rest | Encrypted storage (AES-256) |
| Data in Transit | TLS 1.3, VPN, HTTPS |
| Data in Use | Trusted Execution Environments (TEE), DLP tools |

---

### 12. Threats to Information Systems — Classification

#### By Origin
- **Internal** — Insider attacks, accidental data loss
- **External** — Hackers, nation-state actors, competitors

#### By Intent
- **Intentional** — Targeted attacks, espionage, sabotage
- **Unintentional** — Human error, misconfiguration, natural disaster

#### By Target

| Target | Examples |
|---|---|
| Network | DDoS, packet sniffing, MITM |
| System | Malware, rootkits, privilege escalation |
| Application | SQL injection, XSS, CSRF |
| Physical | Theft, unauthorized access, hardware damage |
| Human | Social engineering, insider threat |

#### By Nature — STRIDE Model

| Category | Description |
|---|---|
| **S**poofing | Impersonating another entity (IP spoofing, ARP spoof) |
| **T**ampering | Modifying data without authorization |
| **R**epudiation | Denying performing an action (no audit trail) |
| **I**nformation Disclosure | Exposing info to unauthorized persons |
| **D**enial of Service | Making systems unavailable |
| **E**levation of Privilege | Gaining unauthorized elevated access |

---

### 13. Threat Actors in 2026

| Threat Actor | Motivation & Capability |
|---|---|
| **Script Kiddies** | Limited skills, use pre-built tools, show-off |
| **Hacktivists** | Political/social agenda (Anonymous, etc.) |
| **Cybercriminals** | Financial gain — ransomware, fraud, theft |
| **Nation-State Actors** | Espionage, sabotage, warfare (APT groups) |
| **Insider Threats** | Revenge, financial gain, ideological |
| **Competitors** | Corporate espionage, IP theft |
| **Terrorist Groups** | Disruption of critical infrastructure |
| **AI-Powered Attackers** *(NEW 2026)* | Using LLMs to automate attacks |

**Notable APT Groups (2026):**

| Group | Origin | Specialty |
|---|---|---|
| APT29 (Cozy Bear) | Russia | Government espionage |
| APT41 | China | Dual espionage + financial crime |
| Lazarus Group | North Korea | Financial theft, WannaCry |
| Sandworm | Russia | Critical infrastructure attacks |

---

### 14. Types of Attacks — Classification

#### By Attack Vector

| Vector | Examples |
|---|---|
| Network-based | Sniffing, MITM, DDoS, DNS poisoning |
| Host-based | Trojans, rootkits, keyloggers |
| Application | XSS, SQL injection, buffer overflow |
| Social | Phishing, pretexting, deepfakes |

#### By Attack Phase — MITRE ATT&CK Kill Chain v15

| Phase | Description |
|---|---|
| 1 — Reconnaissance | Passive/active info gathering |
| 2 — Resource Development | Setting up C2, malware, accounts |
| 3 — Initial Access | Phishing, exploit public-facing app |
| 4 — Execution | Running malicious code |
| 5 — Persistence | Backdoors, scheduled tasks, registry |
| 6 — Privilege Escalation | Gaining admin/root access |
| 7 — Defense Evasion | AV bypass, obfuscation, rootkits |
| 8 — Credential Access | Password cracking, credential dumping |
| 9 — Discovery | Mapping network, finding assets |
| 10 — Lateral Movement | Moving through the network |
| 11 — Collection | Gathering data of interest |
| 12 — Command & Control | Communication with infected hosts |
| 13 — Exfiltration | Stealing data out of target network |
| 14 — Impact | Ransomware, data destruction, disruption |

#### Lockheed Martin Cyber Kill Chain (Classic)

```
Recon → Weaponize → Deliver → Exploit → Install → C&C → Act on Objectives
```

#### By Nature

| Type | Description |
|---|---|
| **Active Attacks** | Modify system/data (MITM, replay, DoS, masquerade) |
| **Passive Attacks** | Monitor/collect without modification (eavesdropping, traffic analysis, shoulder surfing) |

---

### 15. Incident Management Overview

**NIST 800-61 Incident Response Lifecycle:**

| Step | Activity |
|---|---|
| 1 — Preparation | Policies, tools, team, training |
| 2 — Detection | SIEM alerts, IDS/IPS, user reports |
| 3 — Containment | Isolate affected systems |
| 4 — Eradication | Remove malware, close vulnerabilities |
| 5 — Recovery | Restore systems, verify integrity |
| 6 — Lessons Learned | Post-incident analysis and reporting |

**Key Metrics:**

| Metric | Meaning |
|---|---|
| MTTD | Mean Time To Detect |
| MTTR | Mean Time To Respond/Recover |
| MTTC | Mean Time To Contain |

---

### ✅ Session 6 — Key Takeaways

- [x] CIA Triad is the foundation of all security decisions
- [x] Zero Trust is the 2026 security architecture standard
- [x] Humans remain the most exploited vulnerability in any system
- [x] STRIDE and MITRE ATT&CK are the primary threat modeling frameworks
- [x] Threat actors range from script kiddies to nation-states
- [x] Attacks are classified by origin, intent, target, nature, and phase
- [x] Incident Response follows the NIST 800-61 lifecycle

---

<details>
<summary>📖 Session 6 — Glossary</summary>

| Term | Definition |
|---|---|
| CIA Triad | Confidentiality, Integrity, Availability |
| Zero Trust | Never trust, always verify — network model |
| STRIDE | Threat modeling framework (6 categories) |
| MITRE ATT&CK | Framework mapping adversary TTPs |
| APT | Advanced Persistent Threat — sophisticated attacker |
| DPDPA 2023 | India's Digital Personal Data Protection Act |
| Social Engineering | Psychological manipulation for security breach |
| Insider Threat | Security risk from within the organization |
| Defense in Depth | Layered security with no single point of failure |
| Least Privilege | Minimum permissions principle |
| Threat Actor | Any individual/group posing a security threat |
| TTP | Tactics, Techniques, and Procedures of attackers |
| SIEM | Security Information & Event Management system |
| UEBA | User and Entity Behavior Analytics |
| Kill Chain | Model describing stages of a cyberattack |

</details>

---

## Session 7 — Protecting Info Systems, Wireless & Mobile Security

### 1. Layered Protection Model

The OSI Security Architecture (X.800) defines three layers:

**a) Security Services:**
Authentication · Access Control · Data Confidentiality · Data Integrity · Non-Repudiation · Availability

**b) Security Mechanisms:**
Encryption · Digital Signatures · Access Controls · Traffic Padding · Routing Control · Notarization

**c) Security Attacks:**
As classified in Session 6 (active/passive, STRIDE, etc.)

---

### 2. Network Security Controls

#### a) Firewalls

| Type | What It Does |
|---|---|
| **Packet Filtering** | Examines packet headers (Layer 3/4) |
| **Stateful Inspection** | Tracks connection states |
| **Application Layer** | Deep packet inspection (Layer 7) |
| **NGFW** | IPS + App awareness + TLS inspection |

**Firewall Rule Principles:**
- Default Deny (whitelist — deny all, allow only what's needed)
- Least privilege applied to network traffic
- Regular rule review and cleanup (remove stale rules)

---

#### b) IDS vs IPS

| Aspect | IDS (Intrusion Detection) | IPS (Intrusion Prevention) |
|---|---|---|
| Mode | Passive — monitors | Inline — actively blocks |
| Action | Alert/Log | Block/Alert/Log |
| Position | Out-of-band | In-band (inline) |
| False Positive | Less critical | Can block legitimate traffic |
| Examples | Snort (IDS mode) | Snort (IPS mode), Suricata |

**IDS Detection Methods:**

| Method | How It Works |
|---|---|
| Signature-based | Pattern matching (known attacks only) |
| Anomaly-based | Deviation from baseline (detects unknown attacks) |
| Heuristic | Rule-based behavioral analysis |
| Stateful Protocol | Protocol behavior analysis |

---

#### c) VPN

- Creates encrypted tunnel over public network
- **Types:** Site-to-Site VPN, Remote Access VPN
- **Protocols:** IPSec (IKEv2), SSL/TLS (OpenVPN), WireGuard

> [!WARNING]
> VPN alone is no longer sufficient for security in 2026. Zero Trust needs to complement it.

---

#### d) DMZ (Demilitarized Zone)

Network segment between public internet and internal network — houses public-facing servers.

```
Internet → Outer Firewall → DMZ → Inner Firewall → LAN
```

Attacker reaching DMZ does **NOT** automatically reach LAN.

---

#### e) Honeypots

Decoy systems designed to attract and trap attackers.

| Type | Description |
|---|---|
| **Low-interaction** | Simulates limited services (easy to deploy) |
| **High-interaction** | Real systems (higher risk, more intel) |
| **Honeynet** | Network of honeypots |

---

#### f) DLP (Data Loss Prevention)

- Monitors and controls data in use, in transit, at rest
- Prevents unauthorized data exfiltration
- Tools: Symantec DLP, Microsoft Purview, Forcepoint

---

#### g) SIEM

Aggregates and correlates logs from multiple sources.

- **Functions:** Log management, real-time alerts, compliance reporting
- **Modern SIEM + SOAR** = automated threat response
- **Tools:** Splunk, IBM QRadar, Microsoft Sentinel, Elastic SIEM

---

### 3. Mobile Security Landscape (2026)

> [!NOTE]
> Over 6.8 billion smartphone users globally. 60%+ of corporate network access comes from mobile devices. Mobile banking trojans increased 200% in 2024–2025.

---

### 4. Mobile Threats

| Threat | Description |
|---|---|
| **Malicious Apps** | Apps masquerading as legitimate software |
| **Rooting/Jailbreaking** | Bypassing OS security restrictions |
| **Spyware** | Covert surveillance software (e.g., Pegasus) |
| **SMS/Smishing Attacks** | Phishing via text messages |
| **Mobile RATs** | Remote Access Trojans on mobile |
| **Juice Jacking** | Malicious charging stations |
| **Evil Twin Attack** | Rogue Wi-Fi hotspot impersonating a legitimate one |
| **Bluetooth Attacks** | Bluesnarfing, Bluebugging, Bluejacking |
| **SS7 Attacks** | Exploiting telecom signaling protocols |
| **Deepfake Caller ID** *(2025–26)* | AI-generated voice to spoof identity |
| **Mobile MDM Bypass** | Circumventing Mobile Device Management |

---

### 5. Wireless Security

#### a) IEEE 802.11 Standards

802.11a/b/g/n/ac/ax (Wi-Fi 6/6E) · 802.11be (Wi-Fi 7 — 2024+)

---

#### b) Wireless Encryption Standards

| Protocol | Year | Encryption | Status (2026) |
|---|---|---|---|
| WEP | 1997 | RC4 (40/104-bit key) | 🔴 BROKEN — Never use |
| WPA | 2003 | TKIP (RC4-based) | 🔴 DEPRECATED |
| WPA2-Personal | 2004 | AES-CCMP (128-bit) | 🟡 Acceptable minimum |
| WPA2-Enterprise | — | AES + 802.1X/RADIUS | 🟢 Recommended |
| WPA3-Personal | 2018 | SAE (Dragonfly Handshake) | 🟢 RECOMMENDED 2026 |
| WPA3-Enterprise | — | 192-bit security suite | 🟢 BEST PRACTICE 2026 |
| Wi-Fi 7 | 2024 | MLD + enhanced security | ⚪ EMERGING |

---

#### c) Common Wireless Attacks

| Attack | Description |
|---|---|
| **War Driving** | Searching for Wi-Fi networks from a moving vehicle |
| **Evil Twin** | Rogue AP mimicking legitimate SSID |
| **SSID Spoofing** | Creating a network with same/similar SSID |
| **WEP Cracking** | Using aircrack-ng to crack WEP key |
| **WPA2 PMKID Attack** | Modern WPA2 cracking (no client needed) |
| **Deauthentication** | Flooding deauth frames to disconnect users |
| **Rogue AP** | Unauthorized access point on the network |
| **KRACK Attack** | Key Reinstallation Attack (WPA2 vulnerability) |
| **Dragonblood** | WPA3 SAE vulnerabilities (partially patched) |
| **Karma Attack** | Responding to all Wi-Fi probe requests |

---

#### d) Wireless Security Best Practices

- [x] Use WPA3-Enterprise where possible
- [x] Disable WPS (vulnerable to brute force)
- [x] Change default SSID and admin credentials
- [x] Enable MAC address filtering (weak but adds a layer)
- [x] Use a separate guest network
- [x] Deploy WIDS (Wireless Intrusion Detection System)
- [x] Regular wireless audits with Aircrack-ng, Kismet

---

#### e) Bluetooth Security

| Attack | Description |
|---|---|
| **Bluejacking** | Sending unsolicited messages |
| **Bluesnarfing** | Unauthorized access to Bluetooth device |
| **Bluebugging** | Full control of device via Bluetooth |
| **BIAS Attack** | Bluetooth Impersonation Attack (2020+, still relevant) |

**Mitigation:** Disable Bluetooth when not in use · Use device pairing PIN · Keep firmware updated

---

### 6. Credit Card Fraud Types

| Fraud Type | Description |
|---|---|
| **Card Not Present (CNP)** | Online fraud using stolen card details — no physical card needed |
| **Card Skimming** | Device placed on ATM/POS to clone card data |
| **Shimming** | Thin device inserted into chip card readers |
| **Phishing CNP** | Stealing card details via fake websites/emails |
| **Account Takeover (ATO)** | Taking over a banking account via credential stuffing, phishing, SIM swap |
| **SIM Swap Attack** | Porting victim's phone number to attacker's SIM — bypasses SMS 2FA |
| **NFC/RFID Attack** | Contactless card data theft using NFC reader |
| **Man-in-the-App** | Malware intercepting data inside banking app |
| **Deepfake Fraud** *(2024–26)* | AI voice/video to authorize fraudulent transfers |

---

### 7. Payment Card Industry Data Security Standard (PCI DSS v4.0)

**6 Goals, 12 Requirements:**

| Goal | Requirements |
|---|---|
| Build & maintain secure network | R1: Firewall config · R2: No vendor-supplied default passwords |
| Protect cardholder data | R3: Protect stored data · R4: Encrypt data in transit |
| Vulnerability management | R5: Use/update anti-virus · R6: Secure systems and apps |
| Strong access control | R7: Restrict access by need-to-know · R8: Unique IDs per person · R9: Restrict physical access |
| Monitor & test networks | R10: Track all network access · R11: Regularly test systems |
| Maintain security policy | R12: Maintain an InfoSec policy |

**New in PCI DSS v4.0 (2024+):**
- Stronger password requirements (minimum 12 characters)
- MFA required for all admin access
- Greater focus on targeted risk analysis

---

### 8. Mobile Payment Security

#### EMV Chip Technology
- Dynamic authentication codes for each transaction
- Significantly harder to clone than magnetic stripe

#### Tokenization
- Replaces Primary Account Number (PAN) with a unique token
- Token is useless to attackers even if intercepted
- Used in Apple Pay, Google Pay, Samsung Pay

#### 3DS (3D Secure) v2.0
- Additional authentication layer for online transactions
- Frictionless flow with risk-based authentication
- Supports biometric authentication

---

### 9. Information Security Management System (ISMS)

A systematic approach to managing sensitive company information (ISO/IEC 27001).

**PDCA Cycle for ISMS:**

| Phase | Activity |
|---|---|
| **Plan** | Establish ISMS scope, risk assessment, policies |
| **Do** | Implement controls, training, risk treatment |
| **Check** | Monitor, audit, measure performance |
| **Act** | Take corrective action, continual improvement |

**Key Roles:**

| Role | Responsibility |
|---|---|
| CISO | Overall security strategy |
| Security Manager | Day-to-day management |
| Security Analyst | Monitoring and analysis |
| Penetration Tester | Security testing |
| SOC Team | 24/7 monitoring |

---

### 10. Security Operations Center (SOC) — 2026

Centralized unit that continuously monitors and improves an organization's security posture.

**SOC Analyst Tiers:**

| Tier | Focus |
|---|---|
| Tier 1 — Alert Monitoring | Triage incoming alerts from SIEM |
| Tier 2 — Incident Analysis | Deep-dive investigation, context |
| Tier 3 — Threat Hunting | Proactive hunting, forensics |

**Modern SOC Technologies (2026):**

| Technology | Purpose |
|---|---|
| SIEM + SOAR | Automated detection and response |
| XDR | Extended Detection & Response (cross-platform) |
| UEBA | Behavioral analytics to detect insider threats |
| Threat Intel | Integration with MISP, STIX/TAXII feeds |
| AI/ML Detection | Anomaly detection using machine learning |

---

### 11. Business Continuity Planning (BCP) & Disaster Recovery (DR)

- **BCP** — Ensures critical business functions continue during/after disruption
- **DR** — Technical plan for recovering IT systems after a disaster

**Key Metrics:**

| Metric | Meaning |
|---|---|
| **RTO** | Recovery Time Objective — maximum acceptable downtime |
| **RPO** | Recovery Point Objective — maximum acceptable data loss |
| **MTBF** | Mean Time Between Failures — average system reliability |
| **MTTR** | Mean Time To Repair — average repair time |

**Backup Strategies:**

| Strategy | Description |
|---|---|
| Full Backup | Complete copy of all data |
| Incremental Backup | Only changes since last backup |
| Differential Backup | Changes since last full backup |
| **3-2-1 Rule** | 3 copies · 2 different media · 1 offsite |

---

### 12. Cryptography Fundamentals

#### a) Symmetric Encryption

- Same key for encrypt/decrypt — fast, efficient, used for bulk data
- Algorithms: AES-128/256, DES *(legacy)*, 3DES *(legacy)*, ChaCha20
- Key challenge: Secure key exchange

#### b) Asymmetric Encryption

- Public/private key pair — slower but solves key exchange problem
- Algorithms: RSA-2048/4096, ECC (ECDSA, Ed25519)
- Use: Digital signatures, key exchange, certificate signing

#### c) Hash Functions

- One-way function — fixed-length output
- Algorithms: MD5 *(broken)*, SHA-1 *(deprecated)*, SHA-256, SHA-3
- Use: Password storage, file integrity verification
- **Salting** — Adding random value to password before hashing

#### d) PKI (Public Key Infrastructure)

- Framework for managing digital certificates and keys
- Components: CA, RA, CRL, OCSP
- TLS/SSL certificates use PKI

#### e) TLS 1.3

- Current standard for securing web communications
- TLS 1.0/1.1 — deprecated · TLS 1.2 — acceptable · TLS 1.3 — recommended
- **Perfect Forward Secrecy (PFS)** — each session uses a unique key

#### f) Post-Quantum Cryptography (PQC) — Emerging 2026

> [!IMPORTANT]
> Quantum computers can break RSA and ECC. NIST PQC Standards (2024): CRYSTALS-Kyber (key exchange), CRYSTALS-Dilithium (digital signatures). Start planning PQC migration now.

---

### 13. Authentication Mechanisms

**Authentication Factors:**

| Factor | Type | Examples |
|---|---|---|
| Factor 1 | Something you **KNOW** | Password, PIN, security questions |
| Factor 2 | Something you **HAVE** | Smart card, hardware token, phone |
| Factor 3 | Something you **ARE** | Fingerprint, face, iris, voice |

**MFA Types (weakest → strongest):**
OTP via SMS → TOTP (Google Auth) → Push notification → **FIDO2/WebAuthn** *(phishing-resistant)*

**Password Best Practices (2026):**
- Minimum 12–16 characters (PCI DSS v4.0 requires 12+)
- Use passphrases instead of complex rules
- No periodic changes unless compromised
- Check against breach databases (Have I Been Pwned)
- Use a password manager + unique passwords per site

---

### 14. Access Control Models

| Model | Description & Example |
|---|---|
| **DAC** | Discretionary — owner sets permissions (Windows NTFS) |
| **MAC** | Mandatory — system enforces labels (military, SELinux) |
| **RBAC** | Role-Based — permissions based on job role (most common) |
| **ABAC** | Attribute-Based — fine-grained, context-aware policies |
| **ReBAC** | Relationship-Based — Google Zanzibar, social graphs |
| **PAM** | Privileged Access Management — for admin accounts |

---

### ✅ Session 7 — Key Takeaways

- [x] WPA3 is the minimum standard for wireless security in 2026 — WEP is completely broken
- [x] Mobile devices are now the primary attack surface for most organizations
- [x] PCI DSS v4.0 governs payment card security globally
- [x] SIM swap attacks can defeat SMS-based 2FA
- [x] Tokenization and 3DS v2.0 are standard defenses for mobile payments
- [x] ISMS (ISO 27001) provides a systematic approach to security management
- [x] TLS 1.3 and AES-256 are the 2026 encryption standards
- [x] Post-Quantum Cryptography planning should start now
- [x] FIDO2/WebAuthn is the strongest MFA option available

---

<details>
<summary>📖 Session 7 — Glossary</summary>

| Term | Definition |
|---|---|
| WPA3 | Wi-Fi Protected Access 3 — current Wi-Fi standard |
| Evil Twin | Rogue AP mimicking legitimate Wi-Fi hotspot |
| SIM Swap | Porting victim's phone number to attacker's SIM |
| PCI DSS | Payment Card Industry Data Security Standard |
| Tokenization | Replacing sensitive data with a non-sensitive token |
| ISMS | Information Security Management System |
| IDS/IPS | Intrusion Detection/Prevention System |
| DMZ | Demilitarized Zone — network security segment |
| SIEM | Security Information & Event Management |
| TLS 1.3 | Current standard for transport layer security |
| FIDO2/WebAuthn | Phishing-resistant authentication standard |
| PQC | Post-Quantum Cryptography |
| RBAC | Role-Based Access Control |
| PAM | Privileged Access Management |
| Honeypot | Decoy system to attract and study attackers |
| EMV | Europay, Mastercard, Visa chip standard |

</details>

---

## Session 8 — Cyber Crimes & Introduction to Ethical Hacking

### 1. Definition of Cybercrime

Any criminal activity that involves a computer, network, or networked device. The computer may be the tool, the target, or both.

| Category | Examples |
|---|---|
| Computer as a Target | Hacking, DDoS, malware infection |
| Computer as a Tool | Fraud, identity theft, online harassment |
| Computer as Incidental | Drug trafficking records stored on computer |

---

### 2. Types of Cybercrimes (2026)

| Crime Type | Description |
|---|---|
| **Hacking** | Unauthorized access to systems |
| **Phishing** | Credential theft via deceptive communications |
| **Identity Theft** | Stealing PII to impersonate victim |
| **Online Fraud** | Fake shopping sites, investment scams |
| **Ransomware** | Encrypting data and demanding payment |
| **Cyberstalking** | Using tech to stalk/harass individuals |
| **Cyberbullying** | Harassment via digital platforms |
| **Online Child Exploitation** | CSAM (Child Sexual Abuse Material) |
| **Corporate Espionage** | Stealing trade secrets/IP via cyber means |
| **Cryptocurrency Crime** | Crypto theft, darknet transactions, mixing |
| **AI-Powered Fraud** *(NEW 2026)* | Deepfakes, AI phishing, automated fraud |
| **Supply Chain Attack** | Compromising software build/distribution |
| **Insider Trading via Hacking** | Stock manipulation through hacked systems |

---

### 3. Cybercrime in Context of the Internet

**Internet-specific factors amplifying cybercrime:**

| Factor | Why It Matters |
|---|---|
| Anonymity | Difficult to trace actual identity |
| Global reach | Attack from any country against any target |
| Low cost | Massive attacks with minimal investment |
| Speed | Near-instantaneous attack execution |
| Automation | Botnets automate attacks at scale |
| Jurisdiction | Cross-border crimes complicate prosecution |
| Dark Web | Marketplace for criminal tools and services |

**Web Layers:**

| Layer | Description |
|---|---|
| Surface Web | Indexed content (~4% of internet) |
| Deep Web | Non-indexed content (medical records, databases) |
| Dark Web | Encrypted overlay networks (Tor, I2P) |

**Dark Web Use in Crime:** Stolen data markets · Ransomware-as-a-Service · Weapons · CSAM · Hacking-for-hire services

---

### 4. Legal Aspects of Open Communications

**Legal Challenges in Internet Communications:**

| Challenge | Description |
|---|---|
| Jurisdiction | Which country's law applies when attacker/server/victim are in different countries? |
| Attribution | Proving WHO conducted the attack |
| Evidence | Digital evidence collection and preservation |
| ISP Liability | When is an ISP responsible? |
| Encryption | Law enforcement vs privacy rights debate |

**Key Legal Concepts:**

| Concept | Description |
|---|---|
| Computer Forensics | Legally admissible digital evidence collection |
| Chain of Custody | Maintaining integrity of evidence |
| Digital Signatures | Non-repudiation in digital communications |
| Wiretapping Law | Legal interception of communications |
| Safe Harbor Doctrine | ISP protection for user-generated content |

---

### 5. Information Technology Act 2000 (IT Act)

India's primary legislation for cybercrimes and electronic commerce.

| Section | Offense & Penalty |
|---|---|
| **S. 43** | Unauthorized access, downloading data, damage — Compensation up to ₹1 crore |
| **S. 43A** | Corporate negligence — failure to protect sensitive data |
| **S. 65** | Tampering with computer source documents — Up to 3 yrs / ₹2 lakh |
| **S. 66** | Computer-related offenses (hacking, data theft) — Up to 3 yrs / ₹5 lakh |
| **S. 66A** | Sending offensive messages — *(struck down by SC in Shreya Singhal v. Union of India, 2015)* |
| **S. 66B** | Receiving stolen computer resource — Up to 3 yrs / ₹1 lakh |
| **S. 66C** | Identity theft — Up to 3 yrs / ₹1 lakh |
| **S. 66D** | Cheating by personation using computer resource — Up to 3 yrs / ₹1 lakh |
| **S. 66E** | Violation of privacy — Up to 3 yrs / ₹2 lakh |
| **S. 66F** | **CYBER TERRORISM** — threatening national security — **LIFE IMPRISONMENT** |
| **S. 67** | Publishing obscene material electronically — Up to 3 yrs / ₹5 lakh (first offense) |
| **S. 67A** | Publishing sexually explicit material — Up to 5 yrs / ₹10 lakh (first offense) |
| **S. 67B** | Child pornography (CSAM) — Up to 5 yrs / ₹10 lakh (first offense) |
| **S. 69** | Government power to intercept, monitor, or decrypt information |
| **S. 72** | Breach of confidentiality and privacy — Up to 2 yrs / ₹1 lakh |

---

### 6. Indian Penal Code (IPC) Sections Applicable to Cybercrime

| Section | Applicability |
|---|---|
| S. 415 | Cheating — online fraud, fake e-commerce sites |
| S. 420 | Cheating & dishonestly inducing delivery of property (fraud) |
| S. 383 | Extortion — ransomware demands |
| S. 499 | Defamation — online reputation damage |
| S. 500 | Punishment for defamation |
| S. 503 | Criminal intimidation — cyber threats |
| S. 506 | Punishment for criminal intimidation |
| S. 292 | Sale of obscene material — applies to online pornography |
| S. 293 | Obscene material to young persons |
| S. 354C | Voyeurism — recording/watching without consent |
| S. 354D | Stalking — includes online/cyber stalking |
| S. 509 | Word/gesture intending to insult modesty of a woman |

---

### 7. Digital Personal Data Protection Act 2023 (DPDPA)

India's comprehensive data privacy law (effective 2024–2025).

**Rights of Data Principals (individuals):**
- Right to access information
- Right to correction and erasure
- Right of grievance redressal
- Right to nominate (digital inheritance)

**Obligations of Data Fiduciaries (organizations):**
- Lawful processing, purpose limitation, data minimization
- Security safeguards and breach notification
- Appointing a Data Protection Officer (DPO)

> [!IMPORTANT]
> Penalties: Up to **INR 250 crore** for major violations.

---

### 8. Fraud, Hacking, Mischief in Cyber Law

| Offense | Law | Notes |
|---|---|---|
| **Fraud** | IPC S. 420 + IT Act S. 66D | Fake bank sites, UPI fraud, KYC fraud |
| **Hacking** | IT Act S. 66 | Unauthorized access with criminal intent — 3 yrs + ₹5 lakh |
| **Mischief** | IT Act S. 65 & S. 66 + IPC S. 425-440 | Destroying/altering data, cyber vandalism |

> [!WARNING]
> Ethical hacking requires **written authorization**. Without it, even "testing" is illegal under the IT Act.

---

### 9. International Cyber Law Framework

#### a) Budapest Convention on Cybercrime (2001)
- First international treaty on cybercrime
- Covers: Unauthorized access, data interference, system interference, computer-related fraud/forgery
- 68+ signatory countries — **India is NOT a signatory**

#### b) United Nations (UN) Initiatives
- UN Group of Governmental Experts (GGE) on cyber norms
- UN Open-Ended Working Group (OEWG) on cybersecurity
- UN Resolution 73/27: Responsible state behavior in cyberspace

#### c) Tallinn Manual 2.0
- Academic study applying international law to cyberspace
- Addresses state-sponsored attacks and cyber warfare
- **NOT binding law** — but an influential reference

#### d) GDPR (EU)
- Applies to any organization processing EU citizens' data
- Key rights: Access · Erasure · Portability · Objection
- Penalties: Up to €20 million or 4% of global annual revenue
- Data breach notification: Within 72 hours

#### e) CFAA (USA)
- Primary US federal cyber law
- Criminalizes unauthorized computer access
- Used in major hacking prosecutions (Aaron Swartz case)

#### f) NIS2 Directive (EU — 2024)
- Mandatory cybersecurity requirements for critical sectors
- Stricter than the original NIS directive

---

### 10. Jurisdiction Challenges in Cyber Law

**Principles for Determining Jurisdiction:**

| Principle | Description |
|---|---|
| Territoriality | Where did the crime occur? |
| Nationality | Citizenship of the criminal or victim |
| Passive Personality | Victim's country asserts jurisdiction |
| Effects Doctrine | Where were the effects felt? |
| Universality | Some crimes are prosecutable anywhere |

**MLATs (Mutual Legal Assistance Treaties)** — Agreements between countries to share evidence and assist in investigations. Challenge: Many cybercrime havens have no MLAT agreements.

---

### 11. Obscenity and Pornography on the Internet

**Legal Framework in India:**

| Law | Coverage |
|---|---|
| IT Act S. 67 | Obscene content online — up to 3 yrs / ₹5 lakh |
| IT Act S. 67A | Sexually explicit material — up to 5 yrs / ₹10 lakh |
| IT Act S. 67B | CSAM — up to 5 yrs / ₹10 lakh |
| IPC S. 292–294 | Obscene publications and acts |
| POCSO Act | Protection of Children from Sexual Offenses (2012) |

**Platform Responsibilities (IT Rules 2021):**
Significant Social Media Intermediaries must appoint:
- **Grievance Officer** (India-based)
- **Nodal Contact Person** (law enforcement liaison)
- **Chief Compliance Officer** (legal responsibility)

---

### 12. What is Ethical Hacking?

The **authorized** practice of bypassing system security to identify potential data breaches and threats in a network.

| Characteristic | Description |
|---|---|
| ✔ Authorized | Written permission required (Rules of Engagement) |
| ✔ Legal | Operating within defined legal boundaries |
| ✔ Bounded | Defined scope — what can and cannot be tested |
| ✔ Documented | Everything must be documented |
| ✔ Reported | Findings reported to organization, not exploited |

**Why organizations need ethical hackers:**
- Identify vulnerabilities before real attackers do
- Test effectiveness of existing security controls
- Satisfy compliance requirements (PCI DSS, ISO 27001)
- Reduce risk of data breaches (avg. cost $4.45M in 2025)

---

### 13. Ethical Hacking Terminology

| Term | Definition |
|---|---|
| **Hacker** | Person who gains unauthorized/authorized access to systems |
| **Ethical Hacker** | Authorized security professional testing for weaknesses |
| **Cracker** | Malicious hacker who BREAKS INTO systems illegally |
| **Penetration Test** | Authorized simulated attack to find vulnerabilities |
| **Vulnerability** | A weakness in a system/application/process |
| **Exploit** | Code/technique that takes advantage of a vulnerability |
| **Threat** | Potential danger that could exploit a vulnerability |
| **Payload** | Malicious code that runs after an exploit succeeds |
| **Zero-Day** | Vulnerability unknown to vendor — no patch exists |
| **CVE** | Common Vulnerabilities and Exposures — vulnerability ID |
| **CVSS** | Common Vulnerability Scoring System (0–10 severity) |
| **Attack Surface** | All possible points where attacker can try to enter |
| **Attack Vector** | The path/means used to gain unauthorized access |
| **Footprinting** | Information gathering about target (passive/active) |
| **Reconnaissance** | Initial phase of information collection |
| **Enumeration** | Extracting usernames, shares, services from target |
| **Privilege Escalation** | Gaining higher access than authorized |
| **Lateral Movement** | Moving from one system to another within a network |
| **Persistence** | Maintaining access after initial compromise |
| **Exfiltration** | Extracting data from a compromised network |
| **C2/C&C** | Command and Control — attacker's remote control channel |
| **Rootkit** | Malware hiding its presence at OS/kernel level |
| **Backdoor** | Secret method to bypass normal authentication |
| **Botnet** | Network of compromised machines controlled by attacker |
| **OSINT** | Open Source Intelligence — publicly available data |
| **Bug Bounty** | Program rewarding researchers for finding vulnerabilities |
| **PoC** | Proof of Concept — code demonstrating an exploitable vuln |
| **Threat Modeling** | Structured process to identify and prioritize threats |
| **TTPs** | Tactics, Techniques, and Procedures (of threat actors) |
| **IoC** | Indicator of Compromise — evidence of a potential breach |

---

### 14. Types of Hackers — Comprehensive Classification

| Hacker Type | Description |
|---|---|
| ⬜ **White Hat** | Authorized security professionals — work WITH organizations |
| ⬛ **Black Hat** | Malicious hackers — unauthorized, criminal intent |
| 🩶 **Grey Hat** | Moral ambiguity — sometimes authorized, sometimes not |
| 🟢 **Green Hat** | Beginner/aspiring hackers learning their craft |
| 🔵 **Blue Hat** | External security testers contracted by organizations |
| 🔴 **Red Hat** | Aggressive white hats who attack black hat infrastructure |
| **Script Kiddie** | Unskilled attackers using pre-built tools without understanding them |
| **Hacktivist** | Hackers with political/social agenda (Anonymous, etc.) |
| **Nation-State** | Government-sponsored hackers (APT groups) — most sophisticated |
| **Suicide Hacker** | Willing to face consequences to achieve their goal |
| **Cyber Warrior** | Military/defense-focused hackers in cyberwarfare |

---

### 15. Identifying Different Types of Hacking Technologies

#### a) Password Cracking

| Technique | Description |
|---|---|
| Brute Force | Trying all possible combinations |
| Dictionary Attack | Using a wordlist of common passwords |
| Rainbow Table | Precomputed hash lookups |
| Credential Stuffing | Using leaked credentials from other breaches |

#### b) Spoofing

| Type | Description |
|---|---|
| IP Spoofing | Falsifying source IP address |
| MAC Spoofing | Changing hardware address |
| Email Spoofing | Forging sender address |
| DNS Spoofing | Redirecting DNS queries to malicious IPs |

#### c) Network-Based

| Attack | Description |
|---|---|
| Packet Sniffing | Capturing network traffic |
| MITM | Intercepting and altering communications |
| Session Hijacking | Taking over an authenticated session |
| DNS Poisoning | Corrupting DNS cache entries |

#### d) Malware

| Type | Description |
|---|---|
| Viruses | Self-replicating code attached to files |
| Worms | Self-propagating without user action |
| Trojans | Malware disguised as legitimate software |
| Ransomware | Encrypts files, demands payment |
| Spyware | Covert surveillance and data collection |
| Rootkits | Hides malware/processes from OS |
| Fileless Malware | Lives in memory — no file on disk (hard to detect) |

#### e) Web Application

| Attack | Description |
|---|---|
| **SQL Injection** | Injecting malicious SQL into input fields |
| **XSS** | Injecting client-side scripts into web pages |
| **CSRF** | Forcing browser to make unauthorized requests |
| **SSRF** | Server-Side Request Forgery |
| **XXE** | XML External Entity injection |

#### f) Social Engineering Tools

| Tool | Use |
|---|---|
| GoPhish, Evilginx2 | Phishing toolkits |
| Deepfake tools | AI-generated audio/video for impersonation |
| AI-Assisted OSINT | LLM-powered reconnaissance automation |

---

### 16. The Five Phases of Ethical Hacking

> [!NOTE]
> This is the core methodology. Every phase needs written authorization before execution.

---

#### 🔍 Phase 1 — Reconnaissance (Information Gathering)

Gather as much information as possible about the target before directly interacting with it.

**Passive Recon (no direct contact):**
- OSINT, Google Dorking, WHOIS lookups
- DNS enumeration, subdomain discovery
- Social media profiling (LinkedIn, Twitter, Instagram)
- Job postings analysis (reveals tech stack)
- Shodan, Netcraft, dark web monitoring

**Active Recon (limited interaction):**
- Ping sweeps, traceroute
- Port scanning *(with authorization only)*
- Banner grabbing, network sniffing
- Social engineering calls/emails

**Key Tools:** Maltego · Recon-Ng · theHarvester · Shodan · WHOIS · Netcraft · SpiderFoot · FOCA · Google Dorks

**MITRE ATT&CK:** `TA0043` (Reconnaissance)

---

#### 🔎 Phase 2 — Scanning & Enumeration

Identify live hosts, open ports, services, OS details, and specific vulnerabilities.

**Types of Scanning:**

| Type | Purpose |
|---|---|
| Network Scanning | Identify active hosts on network |
| Port Scanning | Find open ports and listening services |
| Vulnerability Scanning | Identify known vulnerabilities in services |

**Key Scan Types (TCP-based):**

| Scan | Description |
|---|---|
| TCP Connect Scan | Full 3-way handshake — noisy, easily detected |
| SYN Scan (Half Open) | Only SYN → SYN-ACK — stealth scan |
| NULL Scan | No TCP flags set |
| FIN Scan | FIN flag only |
| XMAS Scan | FIN+PSH+URG flags — looks like a Xmas tree |
| IDLE Scan | Uses zombie host — hard to trace |
| UDP Scan | Finds UDP services |

**Enumeration:** Extracting usernames, group names, shared resources, services via NetBIOS, LDAP, SNMP, DNS, NTP

**Key Tools:** NMAP · Nessus · OpenVAS · Nikto · Masscan · Zmap · enum4linux · SNMPwalk

**MITRE ATT&CK:** `TA0007` (Discovery) · `TA0043` (Reconnaissance)

---

#### 💥 Phase 3 — Gaining Access (Exploitation)

Exploit identified vulnerabilities to gain access — always within authorized scope.

**Methods:**

| Method | Tools |
|---|---|
| Password cracking | Hydra, Hashcat, John the Ripper |
| Exploitation frameworks | Metasploit, Cobalt Strike, Sliver |
| Web app exploits | SQLmap, Burp Suite |
| Buffer overflow attacks | Custom shellcode |
| Social engineering | Phishing, pretexting |
| Physical access | Bypassing locks, USB drops |

**MITRE ATT&CK:** `TA0001` (Initial Access) · `TA0002` (Execution)

---

#### 🔐 Phase 4 — Maintaining Access (Post-Exploitation)

Demonstrate how an attacker could maintain persistence over time.

**Techniques:**

| Technique | Description |
|---|---|
| Installing backdoors | Netcat, Metasploit Meterpreter |
| Privilege escalation | Gaining admin/root from limited user |
| Creating new accounts | Hidden admin accounts |
| Scheduled tasks/cron | Persistence mechanisms |
| Registry run keys | Windows persistence |
| Rootkit installation | Hiding presence from detection |
| Lateral movement | Pivoting to other systems |
| Data exfiltration | Demonstrating what could be stolen |

**MITRE ATT&CK:** `TA0003` (Persistence) · `TA0004` (Priv. Escalation) · `TA0008` (Lateral Movement) · `TA0010` (Exfiltration)

---

#### 📋 Phase 5 — Covering Tracks (Reporting in Ethical Context)

In ethical hacking this is about **documenting what an attacker could hide** — not actually hiding your own activity.

**Attacker Techniques to Understand:**

| Technique | Description |
|---|---|
| Log clearing/manipulation | Removing traces of activity |
| Timestomping | Modifying file timestamps |
| Steganography | Hiding data in images/audio |
| Encrypting C&C traffic | Evading detection |
| Living off the Land | Using built-in tools: PowerShell, WMI |
| Anti-forensics | File shredding, disk wiping |

**What I must do as an ethical hacker:**
- RESTORE systems to original state post-testing
- DOCUMENT all actions taken during engagement
- SUBMIT comprehensive report to client
- NEVER retain access after engagement ends

**MITRE ATT&CK:** `TA0005` (Defense Evasion) · `TA0006` (Credential Access)

---

### ✅ Session 8 — Key Takeaways

- [x] IT Act 2000 S. 66 & S. 66F are the primary hacking offenses in India
- [x] DPDPA 2023 is India's new data privacy law — penalties up to ₹250 crore
- [x] Hacking WITHOUT written authorization is **always illegal**
- [x] Ethical hacking has 5 phases: Recon → Scan → Exploit → Persist → Report
- [x] MITRE ATT&CK maps every attack phase to known adversary behaviors
- [x] Budapest Convention is the key international cybercrime treaty — India is NOT a signatory
- [x] India's IT Act + IPC together cover most cyber offense scenarios
- [x] Obscenity laws (S. 67, 67A, 67B) carry significant penalties
- [x] Understanding TTPs is as important as understanding tools

---

<details>
<summary>📖 Session 8 — Glossary</summary>

| Term | Definition |
|---|---|
| IT Act 2000 | Information Technology Act — India's primary cyber law |
| DPDPA 2023 | Digital Personal Data Protection Act — India |
| GDPR | EU General Data Protection Regulation |
| Budapest Conv. | First international treaty on cybercrime |
| CVE | Common Vulnerabilities and Exposures |
| CVSS | Common Vulnerability Scoring System (0–10) |
| Zero-Day | Vulnerability with no existing patch |
| Ethical Hacker | Authorized security professional |
| Reconnaissance | Phase 1 of ethical hacking — information gathering |
| Enumeration | Extracting service/user details from target |
| Exploitation | Gaining access through vulnerabilities |
| Persistence | Maintaining access post-compromise |
| OSINT | Open Source Intelligence |
| Deepfake | AI-generated media for impersonation |
| IoC | Indicator of Compromise |
| Rules of Engagement | Authorized scope and boundaries of a pentest |
| Chain of Custody | Preserving evidence integrity in digital forensics |

</details>

---

## 📅 Topics Coming Up

| Session | Topics |
|---|---|
| Session 9 | Types of Hacker Classes · Red/Blue/Grey Teams · Skills for Ethical Hackers · Security Triangle |
| Session 10 | Security Evaluation Plan · Footprinting in Depth · Social Engineering · Scanning Methodologies |
| Session 11 | TCP Flags · Banner Grabbing · Proxy Attacks · IP Spoofing · Enumeration · SMB Attacks · DDoS Overview |
| Session 12 | Password Cracking · Active/Passive/Offline Attacks · Keyloggers · Trojans & Backdoors · Netcat |
| Session 13 | Trojan Construction · Countermeasures · Evasion Techniques |
| Session 14 | Virus vs Worm · Malware Types · AV Evasion · Detection Methods |
| Session 15 | Sniffing (Active/Passive) · ARP Poisoning · DNS Spoofing · MAC Flooding |
| Session 16 | DoS/DDoS · Botnets · Smurf Attacks · SYN Flooding · Session Hijacking |
| Session 17 | Web Server Hacking · OWASP Top 10 · Web Passwords · Wireless Hacking |
| Session 18 | Backdoors · Linux Hacking · IDS/Honeypots/Firewalls · DMZ Setup |
| Session 19 | Physical Security · Penetration Testing Methodologies (PTES, OSSTMM) |
| Session 20 | Malware Reverse Engineering · Static & Dynamic Analysis · Ransomware-as-a-Service · AI-Powered Malware |

---

## 🛠️ Tools & Practice Platforms

<details>
<summary>🔧 Tools to Install (Practice Environment Only)</summary>

| Tool | Purpose |
|---|---|
| Kali Linux 2024.4+ | Primary pentesting OS |
| VirtualBox / VMware | Virtualization for safe lab environment |
| NMAP | Network scanner |
| Burp Suite Community | Web app security testing |
| Wireshark | Packet capture and analysis |
| Metasploit Framework | Exploitation framework |
| Nessus Essentials | Vulnerability scanner (free tier) |
| OWASP ZAP | Web app scanner (open source) |
| Ghidra | NSA's reverse engineering tool (free) |

</details>

<details>
<summary>🎯 Practice Platforms (Legal & Safe)</summary>

| Platform | Level |
|---|---|
| [TryHackMe](https://tryhackme.com) | Beginner-friendly guided rooms |
| [Hack The Box](https://hackthebox.com) | Intermediate/advanced CTF-style |
| OWASP WebGoat | Intentionally vulnerable web app |
| DVWA | Damn Vulnerable Web Application |
| VulnHub | Downloadable vulnerable VMs |
| picoCTF | Beginner CTF (Carnegie Mellon) |

</details>

---

## 🏆 Certifications Pathway

```
┌─────────────────────────────────────────────────────────┐
│  Level 4 — Expert      OSED · OSEP · CISSP · CISM       │
├─────────────────────────────────────────────────────────┤
│  Level 3 — Advanced    OSCP · PNPT (TCM Security)       │
├─────────────────────────────────────────────────────────┤
│  Level 2 — Ethical Hack  CEH v13 · eJPT                 │
├─────────────────────────────────────────────────────────┤
│  Level 1 — Foundation  CompTIA Security+ · Network+     │
└─────────────────────────────────────────────────────────┘
```

---