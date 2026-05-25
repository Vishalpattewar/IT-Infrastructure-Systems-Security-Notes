```
================================================================================
         PGCP-ITISS — ETHICAL HACKING & SECURITY CONCEPTS
         THEORY SESSION NOTES — 2026 EDITION
         ACTS, Pune | Aligned with CEH v13 | MITRE ATT&CK | AI-Powered Security
================================================================================
         Prepared for: Post Graduate Certificate Program — IT Infrastructure,
                       Systems & Security
         Reference Standard: CEH v13 (EC-Council), NIST SP 800-115,
                             MITRE ATT&CK v15, OWASP Top 10 (2021/2025),
                             DPDPA 2023, IT Act 2000 (Amended)
================================================================================
```

## `NOTE TO STUDENT:` 

```
----------------
```

```
These notes are session-by-session theory references. Each session builds
upon the previous. Do NOT skip sessions. Practical labs reinforce every
theory concept covered here. Read, understand, then practice.
```

```
Legal Reminder: "Using any offensive technique against systems you do not
own or have EXPLICIT WRITTEN PERMISSION to test is ILLEGAL under the
IT Act 2000, IPC, and equivalent international laws."
Always operate within authorized boundaries only.
```

```
================================================================================
SESSION 6 — SECURITY MANAGEMENT CONCEPTS & PRINCIPLES +
            HUMAN SIDE OF INFORMATION SECURITY
            Theory: 2 Hours
================================================================================
```

```
-----------------------------------------------------------------------
PART A: SECURITY MANAGEMENT CONCEPTS & PRINCIPLES
```

```
-----------------------------------------------------------------------
```

## `1. WHAT IS INFORMATION SECURITY?` 

```
---------------------------------
```

```
Information Security (InfoSec) is the practice of protecting information
and information systems from unauthorized access, use, disclosure,
disruption, modification, or destruction.
```

```
The three core pillars of Information Security are known as the
CIA Triad:
```

```
  +----------------+--------------------------------------------------+
  | PILLAR         | DEFINITION                                       |
  +----------------+--------------------------------------------------+
  | Confidentiality| Information is accessible only to those          |
  |                | authorized to have access.                        |
  |                | Example: Encrypted emails, access control lists   |
  +----------------+--------------------------------------------------+
  | Integrity      | Accuracy and completeness of data is maintained. |
  |                | Example: Hash verification (MD5, SHA-256)         |
  +----------------+--------------------------------------------------+
  | Availability   | Systems and data are accessible when needed.     |
  |                | Example: Load balancers, backups, DDoS protection |
  +----------------+--------------------------------------------------+
Extended Model (2026 — Beyond CIA Triad):
  - Authentication   : Verifying identity of user or system
  - Non-Repudiation  : Cannot deny having performed an action (digital sig)
  - Authorization    : Granting appropriate permissions post-authentication
  - Accountability   : Tracing actions back to individuals (audit logs)
  - Privacy          : Protecting personal data (DPDPA 2023, GDPR)
```

```
2. KEY SECURITY MANAGEMENT CONCEPTS
```

```
-------------------------------------
```

## `a) Risk Management:` 

```
   - Risk = Threat × Vulnerability × Asset Value
   - Risk Assessment → Identify, Analyze, Evaluate, Treat, Monitor
   - Risk Treatment Options:
       * Accept  : Live with the risk (low impact)
       * Mitigate: Reduce risk with controls
       * Transfer: Insurance, outsourcing
       * Avoid   : Stop the risky activity
```

## `b) Security Policies:` 

```
   - Organizational Security Policy: High-level directives from management
   - System Security Policy: Rules for specific systems
   - Issue-Specific Policy: Password policy, email policy, BYOD policy
   - Acceptable Use Policy (AUP): Rules on how systems may be used
```

## `c) Security Controls:` 

```
   +-------------------+--------------------------------------------------+
   | TYPE              | EXAMPLES                                         |
   +-------------------+--------------------------------------------------+
   | Preventive        | Firewalls, encryption, access controls            |
   | Detective         | IDS, audit logs, SIEM alerts                      |
   | Corrective        | Patch management, incident response               |
   | Deterrent         | Warning banners, security cameras, penalties      |
   | Compensating      | Backup controls when primary controls fail        |
   | Recovery          | Backups, disaster recovery plans (DRP)            |
   +-------------------+--------------------------------------------------+
```

- `d) Defense in Depth (DiD): - Layered security approach — no single point of failure - Layers: Physical → Network → Host → Application → Data - Concept: If one layer fails, others continue to protect` 

- `e) Principle of Least Privilege (PoLP): - Users/systems get ONLY the minimum permissions required - Reduces attack surface significantly - Example: Database admin should NOT have internet browsing access` 

```
f) Separation of Duties (SoD):
   - Critical tasks require more than one person
   - Prevents fraud and insider threats
   - Example: Developer cannot also deploy to production
```

- `g) Security Through Obscurity (STO): - Hiding system details as a security measure - NOT a standalone strategy — must be combined with real controls - Example: Hiding a login page URL — security through obscurity alone` 

- `h) Zero Trust Architecture (ZTA) — 2026 Standard:` 

- `"Never Trust, Always Verify" - Every access request is authenticated, authorized, and continuously validated regardless of network location - Core Principles: * Verify explicitly (always authenticate and authorize)` 

   - `Use least privilege access` 

```
       * Assume breach (design for containment)
   - Key Technologies: MFA, IAM, Micro-segmentation, PAM, SIEM
```

## `3. INFORMATION SECURITY FRAMEWORKS & STANDARDS` 

```
------------------------------------------------
+------------------+-------------------------------------------------------+
| FRAMEWORK        | PURPOSE                                               |
+------------------+-------------------------------------------------------+
| ISO/IEC 27001    | ISMS (Information Security Management System)        |
```

```
| NIST CSF 2.0     | Cybersecurity Framework — Govern, Identify, Protect,  |
|                  | Detect, Respond, Recover                              |
| PCI DSS v4.0     | Payment Card Industry Data Security Standard          |
| HIPAA            | Health Insurance Portability & Accountability Act     |
| SOX              | Sarbanes-Oxley Act — Financial data integrity          |
| GDPR             | EU General Data Protection Regulation                 |
| DPDPA 2023       | India's Digital Personal Data Protection Act          |
| IT Act 2000      | India's primary cyber law (amended 2008)              |
| COBIT 2019       | Governance of enterprise IT                           |
| MITRE ATT&CK v15 | Adversary tactics, techniques, and procedures (TTPs)  |
+------------------+-------------------------------------------------------+
```

## `4. INFORMATION ASSURANCE (IA)` 

```
------------------------------
- Practice of ensuring that information and information systems are
  protected from attack while ensuring authorized users can access data
- 5 Pillars of IA: Integrity, Availability, Confidentiality,
                   Authentication, Non-Repudiation
```

## `5. THREAT INTELLIGENCE LIFECYCLE (2026)` 

```
-----------------------------------------
Phase 1 — Direction   : Define intelligence requirements
Phase 2 — Collection  : Gather raw data (OSINT, HUMINT, TECHINT)
Phase 3 — Processing  : Normalize and filter raw data
Phase 4 — Analysis    : Identify patterns, TTPs, threat actors
Phase 5 — Dissemination: Share intel with stakeholders
Phase 6 — Feedback    : Refine based on consumer feedback
```

```
Threat Intelligence Feeds in 2026:
```

- `STIX/TAXII (Structured Threat Info Expression)` 

- `MISP (Malware Information Sharing Platform)` 

- `VirusTotal, AlienVault OTX, Recorded Future` 

```
-----------------------------------------------------------------------
```

## `PART B: HUMAN SIDE OF INFORMATION SECURITY` 

```
-----------------------------------------------------------------------
```

## `6. WHY HUMANS ARE THE WEAKEST LINK` 

```
------------------------------------
```

```
Statistics (2025-2026):
```

- `Over 82% of data breaches involve a human element (Verizon DBIR 2025)` 

- `Social engineering attacks increased by 43% in 2024-2025` 

- `Average cost of a human-caused data breach: USD $4.9 million` 

## `7. INSIDER THREATS` 

```
-------------------
```

```
Definition: A security threat that originates from within the organization —
typically a current or former employee, contractor, or business associate.
```

```
Types of Insider Threats:
```

- `a) Malicious Insider: Intentionally causes harm (data theft, sabotage)` 

- `Motivations: Financial gain, revenge, ideology` 

- `Example: Employee selling customer data to competitor` 

- `b) Negligent Insider: Unintentionally causes harm through carelessness - Example: Clicking phishing emails, using weak passwords, leaving workstations unlocked` 

- `c) Compromised Insider: Account taken over by external attacker` 

- `Most dangerous — appears as legitimate user` 

- `Detected by behavioral analytics (UEBA)` 

- `d) Third-Party/Vendor Risk: Contractors with excessive access` 

- `Example: The Target breach (2013) — entry via HVAC vendor` 

## `8. SOCIAL ENGINEERING — THE HUMAN ATTACK` 

```
------------------------------------------
```

```
Definition: Psychological manipulation of people into performing actions
or divulging confidential information.
```

## `Social Engineering Attack Types:` 

```
+----------------------+------------------------------------------------------+
| ATTACK TYPE          | DESCRIPTION & EXAMPLE                               |
+----------------------+------------------------------------------------------+
| Phishing             | Fraudulent emails to steal credentials               |
|                      | Example: Fake bank email asking to "verify account"  |
+----------------------+------------------------------------------------------+
| Spear Phishing       | Targeted phishing at specific individuals/org        |
|                      | Example: Email appearing from CEO to CFO             |
+----------------------+------------------------------------------------------+
| Whaling              | Phishing targeting high-level executives (C-suite)   |
+----------------------+------------------------------------------------------+
| Vishing              | Voice phishing — phone calls to extract info         |
|                      | Example: "I'm from IT support, need your password"   |
+----------------------+------------------------------------------------------+
| Smishing             | SMS-based phishing                                   |
|                      | Example: "Your parcel is held. Click to confirm."    |
+----------------------+------------------------------------------------------+
| Pretexting           | Fabricating a scenario to extract information        |
|                      | Example: Impersonating HR to get employee details    |
+----------------------+------------------------------------------------------+
| Baiting              | Leaving infected USB drives in parking lots          |
+----------------------+------------------------------------------------------+
| Tailgating/Piggybacking| Following authorized person into restricted area   |
+----------------------+------------------------------------------------------+
| Quid Pro Quo         | Offering something in exchange for information       |
|                      | Example: Free tech support in exchange for creds     |
+----------------------+------------------------------------------------------+
| Deepfake Attacks     | AI-generated audio/video to impersonate executives  |
| (NEW — 2024-2026)    | Example: Fake CFO video call authorizing wire transfer|
+----------------------+------------------------------------------------------+
```

## `9. PSYCHOLOGY OF SOCIAL ENGINEERING` 

```
--------------------------------------
```

```
Attackers exploit psychological principles:
```

- `Authority    : "I'm the CEO/IT Director, do it now"` 

- `Urgency      : "Act immediately or your account will be locked"` 

- `Scarcity     : "Only 5 minutes before the system shuts down"` 

- `Social Proof : "Everyone in your department has already done this"` 

- `Liking       : Building rapport before the request` 

- `Reciprocity  : "I helped you last week, now I need this favor"` 

- `Fear         : "We detected suspicious activity — verify now"` 

## `10. SECURITY AWARENESS TRAINING (SAT)` 

```
---------------------------------------
```

```
Effective SAT components:
```

- `Regular phishing simulations` 

- `Mandatory security training modules` 

- `Clear incident reporting procedures` 

- `Acceptable Use Policy acknowledgment` 

- `Executive buy-in and leadership modeling` 

- `Gamification and rewards for security behavior` 

```
Key Principle: "Security is everyone's responsibility, not just IT's"
```

## `11. CLASSIFICATION OF INFORMATION` 

```
-----------------------------------
```

```
Organizations classify data to apply appropriate protection:
```

```
+------------------+-------------------------------------------------------+
| CLASSIFICATION   | DESCRIPTION                                           |
+------------------+-------------------------------------------------------+
| Top Secret       | Highest protection — national security level          |
| Confidential     | Serious damage if disclosed — business critical       |
| Internal/Private | For internal use — not for public                    |
| Public           | No restriction — available to everyone               |
+------------------+-------------------------------------------------------+
```

## `Data Handling Requirements:` 

```
  - Data at Rest     : Encrypted storage (AES-256)
  - Data in Transit  : TLS 1.3, VPN, HTTPS
  - Data in Use      : Trusted Execution Environments (TEE), DLP tools
```

## `12. THREATS TO INFORMATION SYSTEMS — CLASSIFICATION` 

```
------------------------------------------------------
```

## `A) By Origin:` 

```
   - Internal Threats: Insider attacks, accidental data loss
```

```
   - External Threats: Hackers, nation-state actors, competitors
```

## `B) By Intent:` 

```
   - Intentional: Targeted attacks, espionage, sabotage
```

```
   - Unintentional: Human error, misconfiguration, natural disaster
```

## `C) By Target:` 

```
   - Network threats   : DDoS, packet sniffing, MITM
```

```
   - System threats    : Malware, rootkits, privilege escalation
   - Application threats: SQL injection, XSS, CSRF
   - Physical threats  : Theft, unauthorized access, hardware damage
   - Human threats     : Social engineering, insider threat
```

## `D) By Nature (STRIDE Model):` 

```
+-------------------+-------------------------------------------------------+
| STRIDE CATEGORY   | DESCRIPTION                                           |
+-------------------+-------------------------------------------------------+
| Spoofing          | Impersonating another entity (IP spoofing, ARP spoof) |
| Tampering         | Modifying data without authorization                  |
| Repudiation       | Denying performing an action (no audit trail)         |
| Information Disc. | Exposing information to unauthorized persons          |
| Denial of Service | Making systems unavailable                            |
| Elevation of Priv | Gaining unauthorized elevated access                  |
+-------------------+-------------------------------------------------------+
```

## `13. THREAT ACTORS IN 2026` 

```
---------------------------
```

```
+------------------------+--------------------------------------------------+
| THREAT ACTOR           | MOTIVATION & CAPABILITY                          |
+------------------------+--------------------------------------------------+
| Script Kiddies         | Limited skills, use pre-built tools, show-off    |
| Hacktivists            | Political/social agenda (Anonymous, etc.)        |
| Cybercriminals         | Financial gain — ransomware, fraud, theft        |
| Nation-State Actors    | Espionage, sabotage, warfare (APT groups)        |
| Insider Threats        | Revenge, financial gain, ideological             |
| Competitors            | Corporate espionage, IP theft                    |
| Terrorist Groups       | Disruption of critical infrastructure            |
| AI-Powered Attackers   | NEW 2026 — Using LLMs to automate attacks        |
+------------------------+--------------------------------------------------+
```

## `Notable APT Groups (2026):` 

```
  - APT29 (Cozy Bear) — Russia — Government espionage
```

```
  - APT41 — China — Dual cyber espionage + financial crime
```

- `Lazarus Group — North Korea — Financial theft, WannaCry` 

- `Sandworm — Russia — Critical infrastructure attacks` 

```
14. TYPES OF ATTACKS — CLASSIFICATION
```

```
---------------------------------------
```

```
A) By Attack Vector:
```

- `Network-based: Sniffing, MITM, DDoS, DNS poisoning` 

- `Host-based   : Trojans, rootkits, keyloggers` 

```
   - Application  : XSS, SQL injection, buffer overflow
```

- `Social       : Phishing, pretexting, deepfakes` 

```
B) By Attack Phase (MITRE ATT&CK Kill Chain v15):
   Phase 1 — Reconnaissance        : Passive/active info gathering
   Phase 2 — Resource Development  : Setting up C2, malware, accounts
   Phase 3 — Initial Access        : Phishing, exploit public-facing app
   Phase 4 — Execution             : Running malicious code
   Phase 5 — Persistence           : Backdoors, scheduled tasks, registry
   Phase 6 — Privilege Escalation  : Gaining admin/root access
   Phase 7 — Defense Evasion       : AV bypass, obfuscation, rootkits
   Phase 8 — Credential Access     : Password cracking, credential dumping
   Phase 9 — Discovery             : Mapping network, finding assets
   Phase 10 — Lateral Movement     : Moving through network
   Phase 11 — Collection           : Gathering data of interest
   Phase 12 — Command & Control    : Communication with infected hosts
   Phase 13 — Exfiltration         : Stealing data out of target network
   Phase 14 — Impact               : Ransomware, data destruction, disruption
```

```
C) Lockheed Martin Cyber Kill Chain (Classic Model):
```

```
   Recon → Weaponize → Deliver → Exploit → Install → C&C → Act on Objectives
```

```
D) By Nature of Attack:
```

- `Active Attacks  : Modify system/data (MITM, replay, DoS, masquerade)` 

- `Passive Attacks : Monitor/collect without modification (eavesdropping, traffic analysis, shoulder surfing)` 

## `15. INCIDENT MANAGEMENT OVERVIEW` 

```
----------------------------------
NIST 800-61 Incident Response Lifecycle:
  Step 1 — Preparation      : Policies, tools, team, training
  Step 2 — Detection        : SIEM alerts, IDS/IPS, user reports
  Step 3 — Containment      : Isolate affected systems
  Step 4 — Eradication      : Remove malware, close vulnerabilities
  Step 5 — Recovery         : Restore systems, verify integrity
  Step 6 — Lessons Learned  : Post-incident analysis and reporting
```

```
Key Metrics:
```

- `MTTD (Mean Time To Detect)` 

- `MTTR (Mean Time To Respond/Recover)` 

- `MTTC (Mean Time To Contain)` 

```
-----------------------------------------------------------------------
SESSION 6 — KEY TAKEAWAYS
```

```
-----------------------------------------------------------------------
```

- `CIA Triad is the foundation of all security decisions✔` 

- `Zero Trust is the 2026 security architecture standard✔` 

- `Humans remain the most exploited vulnerability in any system✔` 

- `STRIDE and MITRE ATT&CK are the primary threat modeling frameworks✔` 

- `Threat actors range from script kiddies to nation-states✔` 

- `Attacks are classified by origin, intent, target, nature, and phase✔` 

- `Incident Response follows the NIST 800-61 lifecycle✔` 

```
-----------------------------------------------------------------------
```

## `SESSION 6 — SELF-ASSESSMENT QUESTIONS` 

```
-----------------------------------------------------------------------
```

- `Q1. Define the CIA Triad and give one real-world example for each pillar. Q2. What is the difference between a threat, vulnerability, and risk?` 

- `Q3. Explain Zero Trust Architecture with its core principles.` 

- `Q4. Describe five types of social engineering attacks with examples.` 

- `Q5. What is the STRIDE threat model? List all 6 categories.` 

- `Q6. Differentiate between active and passive attacks with examples.` 

- `Q7. What is the MITRE ATT&CK framework? Name any 5 phases.` 

- `Q8. Explain the principle of least privilege and separation of duties.` 

- `Q9. What is Defense in Depth? Draw and explain the layered model.` 

- `Q10. How do deepfake attacks differ from traditional social engineering?` 

```
-----------------------------------------------------------------------
SESSION 6 — KEY TERMS GLOSSARY
```

```
-----------------------------------------------------------------------
CIA Triad          : Confidentiality, Integrity, Availability
Zero Trust         : Never trust, always verify — network model
STRIDE             : Threat modeling framework (6 categories)
MITRE ATT&CK       : Framework mapping adversary TTPs
APT                : Advanced Persistent Threat — sophisticated attacker
DPDPA 2023         : India's Digital Personal Data Protection Act
Social Engineering : Psychological manipulation for security breach
Insider Threat     : Security risk from within the organization
Defense in Depth   : Layered security with no single point of failure
Least Privilege    : Minimum permissions principle
Threat Actor       : Any individual/group posing a security threat
TTP                : Tactics, Techniques, and Procedures of attackers
SIEM               : Security Information & Event Management system
UEBA               : User and Entity Behavior Analytics
Kill Chain         : Model describing stages of a cyberattack
```

```
================================================================================
SESSION 7 — PROTECTING INFORMATION SYSTEM SECURITY
            Mobile & Wireless Security | Credit Card Fraud |
            Information Security Management | InfoSec Fundamentals
            Theory: 2 Hours
================================================================================
```

```
-----------------------------------------------------------------------
```

```
PART A: PROTECTING INFORMATION SYSTEMS
```

```
-----------------------------------------------------------------------
```

## `1. LAYERED PROTECTION MODEL` 

```
-----------------------------
Protecting an information system requires multiple layers of controls.
The OSI Security Architecture (X.800) defines:
```

- `a) Security Services:` 

- `Authentication, Access Control, Data Confidentiality, Data Integrity, Non-Repudiation, Availability` 

- `b) Security Mechanisms:` 

- `Encryption, Digital Signatures, Access Controls, Traffic Padding, Routing Control, Notarization` 

- `c) Security Attacks:` 

- `As classified in Session 6 (active/passive, STRIDE, etc.)` 

## `2. NETWORK SECURITY CONTROLS` 

```
------------------------------
```

```
a) Firewalls:
```

```
   Types:
```

- `Packet Filtering     : Examines packet headers (Layer 3/4)` 

- `Stateful Inspection  : Tracks connection states` 

- `Application Layer    : Deep packet inspection (Layer 7)` 

- `NGFW (Next-Gen)      : IPS + App awareness + TLS inspection` 

```
   Firewall Rule Principles:
     - Default Deny (whitelist approach — deny all, allow only needed)
     - Principle of least privilege applied to network traffic
     - Regular rule review and cleanup (remove stale rules)
```

## `b) IDS vs IPS:` 

```
+------------------+------------------------+----------------------------+
| ASPECT           | IDS (Intrusion         | IPS (Intrusion Prevention  |
|                  | Detection System)      | System)                    |
+------------------+------------------------+----------------------------+
| Mode             | Passive — monitors     | Inline — actively blocks   |
| Action           | Alert/Log              | Block/Alert/Log            |
| Position         | Out-of-band            | In-band (inline)           |
| False positive   | Less critical          | Can block legitimate traffic|
| Examples         | Snort (IDS mode)       | Snort (IPS mode), Suricata |
+------------------+------------------------+----------------------------+
IDS Detection Methods:
  - Signature-based  : Pattern matching (known attacks only)
  - Anomaly-based    : Deviation from baseline (detects unknown attacks)
  - Heuristic        : Rule-based behavioral analysis
  - Stateful Protocol: Protocol behavior analysis
```

## `c) VPN (Virtual Private Network):` 

- `Creates encrypted tunnel over public network - Types: Site-to-Site VPN, Remote Access VPN - Protocols: IPSec (IKEv2), SSL/TLS (OpenVPN), WireGuard - Zero Trust Note: VPN alone is no longer sufficient in 2026` 

## `d) DMZ (Demilitarized Zone):` 

- `Network segment between public internet and internal network` 

- `Houses public-facing servers (web servers, mail servers, DNS) - Topology: Internet → Outer Firewall → DMZ → Inner Firewall → LAN - Benefit: Attacker reaching DMZ does NOT automatically reach LAN` 

## `e) Honeypots:` 

- `Decoy systems designed to attract and trap attackers` 

- `Purpose: Gather threat intelligence, detect intrusions` 

- `Types:` 

```
       * Low-interaction: Simulates limited services (easy to deploy)
```

```
       * High-interaction: Real systems (higher risk, more intel)
   - Honeynet: Network of honeypots
```

## `f) DLP (Data Loss Prevention):` 

- `Monitors and controls data in use, in transit, at rest` 

- `Prevents unauthorized data exfiltration` 

- `Tools: Symantec DLP, Microsoft Purview, Forcepoint` 

## `g) SIEM (Security Information & Event Management):` 

- `Aggregates and correlates logs from multiple sources` 

- `Functions: Log management, real-time alerts, compliance reporting` 

- `Modern SIEM + SOAR = automated threat response` 

- `Tools: Splunk, IBM QRadar, Microsoft Sentinel, Elastic SIEM` 

```
-----------------------------------------------------------------------
PART B: SECURITY IN MOBILE AND WIRELESS COMPUTING
```

```
-----------------------------------------------------------------------
```

## `3. MOBILE SECURITY LANDSCAPE (2026)` 

```
--------------------------------------
```

```
Mobile devices are the fastest-growing attack surface in 2026.
Key Statistics:
```

- `Over 6.8 billion smartphone users globally` 

- `60%+ of corporate network access from mobile devices` 

- `Mobile banking trojans increased 200% (2024-2025)` 

## `4. MOBILE THREATS` 

```
------------------
```

```
+-------------------------------+------------------------------------------+
| THREAT                        | DESCRIPTION                              |
+-------------------------------+------------------------------------------+
| Malicious Apps                | Apps masquerading as legitimate software  |
| Rooting/Jailbreaking          | Bypassing OS security restrictions        |
| Spyware                       | Covert surveillance software (Pegasus)    |
| SMS/Smishing Attacks          | Phishing via text messages                |
| Mobile RATs                   | Remote Access Trojans on mobile           |
| Juice Jacking                 | Malicious charging stations               |
| Evil Twin Attack              | Rogue Wi-Fi hotspot impersonating legit   |
| Bluetooth Attacks             | Bluesnarfing, Bluebugging, Bluejacking    |
| SS7 Attacks                   | Exploiting telecom signaling protocols    |
| Deepfake Caller ID (2025-26)  | AI-generated voice to spoof identity      |
| Mobile MDM Bypass             | Circumventing Mobile Device Management   |
+-------------------------------+------------------------------------------+
```

## `5. WIRELESS SECURITY` 

```
---------------------
```

## `a) IEEE 802.11 Standards (Wi-Fi):` 

```
   - 802.11a/b/g/n/ac/ax (Wi-Fi 6/6E), 802.11be (Wi-Fi 7 — 2024+)
```

## `b) Wireless Encryption Standards (Evolution):` 

```
+-------------+----+----------------------------------+-------------------+
| PROTOCOL    | YR | ENCRYPTION                       | STATUS 2026       |
+-------------+----+----------------------------------+-------------------+
| WEP         |1997| RC4 (40/104-bit key)              | BROKEN — Never use|
| WPA         |2003| TKIP (RC4-based)                  | DEPRECATED        |
| WPA2-Personal|2004| AES-CCMP (128-bit)               | Acceptable minimum|
| WPA2-Enterprise|  | AES + 802.1X/RADIUS               | Recommended       |
| WPA3-Personal|2018| SAE (Dragonfly Handshake)         | RECOMMENDED 2026  |
| WPA3-Enterprise|  | 192-bit security suite            | BEST PRACTICE 2026|
| Wi-Fi 7    |2024 | MLD + enhanced security           | EMERGING          |
+-------------+----+----------------------------------+-------------------+
```

## `c) Common Wireless Attacks:` 

- `War Driving         : Searching for Wi-Fi networks from moving vehicle - Evil Twin           : Rogue AP mimicking legitimate SSID - SSID Spoofing       : Creating network with same/similar SSID - WEP Cracking        : Using aircrack-ng to crack WEP key` 

- `WPA2 PMKID Attack   : Modern WPA2 cracking (no client needed)` 

- `Deauthentication    : Flooding deauth frames to disconnect users - Rogue AP            : Unauthorized access point on network` 

- `KRACK Attack        : Key Reinstallation Attack (WPA2 vulnerability)` 

- `Dragonblood         : WPA3 SAE vulnerabilities (partially patched)` 

- `Karma Attack        : Responding to all Wi-Fi probe requests` 

## `d) Wireless Security Best Practices:` 

- `Use WPA3-Enterprise where possible✔ Disable WPS (Wi-Fi Protected Setup) — vulnerable to brute force✔ Change default SSID and admin credentials✔ Enable MAC address filtering (weak — but adds layer)✔ Use separate guest network✔ Deploy WIDS (Wireless Intrusion Detection System)✔ Regular wireless audits with tools like Aircrack-ng, Kismet✔` 

```
e) Bluetooth Security:
```

- `Bluetooth modes: Classic, BLE (Bluetooth Low Energy)` 

- `Attacks:` 

- `Bluejacking  : Sending unsolicited messages` 

- `Bluesnarfing : Unauthorized access to Bluetooth device` 

```
       * Bluebugging  : Taking full control of device via Bluetooth
```

```
       * BIAS Attack  : Bluetooth Impersonation Attack (2020+, still relevant)
   - Mitigation: Disable Bluetooth when not in use, use device pairing PIN,
                 keep firmware updated
```

```
-----------------------------------------------------------------------
PART C: CREDIT CARD FRAUD IN MOBILE & WIRELESS COMPUTING
```

```
-----------------------------------------------------------------------
```

## `6. CREDIT CARD FRAUD TYPES` 

```
----------------------------
```

```
+--------------------+----------------------------------------------------+
| FRAUD TYPE         | DESCRIPTION                                        |
+--------------------+----------------------------------------------------+
| Card Not Present   | Online fraud using stolen card details             |
| (CNP) Fraud        | (No physical card needed)                          |
+--------------------+----------------------------------------------------+
| Card Skimming      | Device placed on ATM/POS to clone card data        |
+--------------------+----------------------------------------------------+
| Shimming           | Thin device inserted into chip card readers        |
+--------------------+----------------------------------------------------+
| Phishing CNP       | Stealing card details via fake websites/emails     |
+--------------------+----------------------------------------------------+
| Account Takeover   | Attacker takes over banking account via credential |
| (ATO)              | stuffing, phishing, SIM swap                      |
+--------------------+----------------------------------------------------+
| SIM Swap Attack    | Port victim's phone number to attacker's SIM       |
|                    | Bypasses SMS-based 2FA                             |
+--------------------+----------------------------------------------------+
| NFC/RFID Attack    | Contactless card data theft using NFC reader       |
+--------------------+----------------------------------------------------+
| Man-in-the-App     | Malware intercepting data inside banking app       |
+--------------------+----------------------------------------------------+
| Deepfake Fraud     | AI voice/video to authorize fraudulent transfers   |
| (2024-2026)        |                                                    |
+--------------------+----------------------------------------------------+
```

## `7. PAYMENT CARD INDUSTRY DATA SECURITY STANDARD (PCI DSS v4.0)` 

```
----------------------------------------------------------------
```

```
PCI DSS is the security standard for organizations handling credit cards.
```

## `6 Goals, 12 Requirements:` 

```
  Goal 1: Build and maintain a secure network
    Req 1: Install/maintain firewall configuration
    Req 2: Do not use vendor-supplied defaults for passwords
```

```
  Goal 2: Protect cardholder data
    Req 3: Protect stored cardholder data
    Req 4: Encrypt transmission of cardholder data across public networks
```

```
  Goal 3: Maintain vulnerability management program
    Req 5: Use and regularly update anti-virus
```

```
    Req 6: Develop and maintain secure systems and applications
```

```
  Goal 4: Implement strong access control
```

```
    Req 7: Restrict access to cardholder data by business need-to-know
    Req 8: Assign unique ID to each person with computer access
    Req 9: Restrict physical access to cardholder data
```

```
  Goal 5: Regularly monitor and test networks
    Req 10: Track and monitor all access to network resources
    Req 11: Regularly test security systems and processes
```

```
  Goal 6: Maintain information security policy
```

```
    Req 12: Maintain a policy that addresses information security
```

```
New in PCI DSS v4.0 (2024+):
```

```
  - Stronger password requirements (minimum 12 characters)
```

```
  - MFA required for all admin access
```

- `Greater focus on targeted risk analysis` 

## `8. MOBILE PAYMENT SECURITY` 

```
----------------------------
```

```
EMV (Europay, Mastercard, Visa) Chip Technology:
```

```
  - Dynamic authentication codes for each transaction
```

```
  - Significantly harder to clone than magnetic stripe
```

## `Tokenization:` 

```
  - Replaces Primary Account Number (PAN) with a unique token
```

```
  - Token is useless to attackers even if intercepted
```

```
  - Used in Apple Pay, Google Pay, Samsung Pay
```

```
3DS (3D Secure) v2.0:
```

```
  - Additional authentication layer for online transactions
```

```
  - Frictionless flow with risk-based authentication
```

```
  - Supports biometric authentication
```

```
-----------------------------------------------------------------------
PART D: INFORMATION SECURITY MANAGEMENT
```

```
-----------------------------------------------------------------------
```

## `9. INFORMATION SECURITY MANAGEMENT SYSTEM (ISMS)` 

```
--------------------------------------------------
```

```
An ISMS (ISO/IEC 27001) is a systematic approach to managing sensitive
company information so it remains secure.
```

```
PDCA (Plan-Do-Check-Act) Cycle for ISMS:
```

```
  PLAN    : Establish ISMS scope, risk assessment, policies
  DO      : Implement controls, training, risk treatment
  CHECK   : Monitor, audit, measure performance
  ACT     : Take corrective action, continual improvement
```

```
Key Roles:
```

```
  - CISO (Chief Information Security Officer): Overall security strategy
  - Security Manager                         : Day-to-day management
  - Security Analyst                         : Monitoring and analysis
  - Penetration Tester                       : Security testing
  - SOC Team                                 : 24/7 monitoring
```

## `10. SECURITY OPERATIONS CENTER (SOC) — 2026` 

```
---------------------------------------------
```

```
A SOC is a centralized unit that continuously monitors and improves
an organization's security posture.
```

```
SOC Analyst Tiers:
```

```
  Tier 1 — Alert Monitoring  : Triage incoming alerts from SIEM
  Tier 2 — Incident Analysis : Deep-dive investigation, context
  Tier 3 — Threat Hunting    : Proactive threat hunting, forensics
```

## `Modern SOC Technologies (2026):` 

```
  - SIEM + SOAR     : Automated detection and response
```

```
  - XDR             : Extended Detection & Response (cross-platform)
  - UEBA            : Behavioral analytics to detect insider threats
```

```
  - Threat Intel    : Integration with MISP, STIX/TAXII feeds
```

```
  - AI/ML Detection : Anomaly detection using machine learning
```

```
11. BUSINESS CONTINUITY PLANNING (BCP) & DISASTER RECOVERY (DR)
```

```
-----------------------------------------------------------------
```

```
BCP: Ensures critical business functions continue during/after disruption
DR : Technical plan for recovering IT systems after a disaster
```

```
Key Metrics:
```

```
  - RTO (Recovery Time Objective)  : Maximum acceptable downtime
```

- `RPO (Recovery Point Objective) : Maximum acceptable data loss` 

- `MTBF (Mean Time Between Failures): Average system reliability` 

- `MTTR (Mean Time To Repair)     : Average repair time` 

```
Backup Strategies:
```

- `Full Backup       : Complete copy of all data` 

- `Incremental Backup: Only changes since last backup` 

- `Differential Backup: Changes since last full backup` 

- `3-2-1 Rule       : 3 copies, 2 different media, 1 offsite` 

```
-----------------------------------------------------------------------
PART E: FUNDAMENTALS OF INFORMATION SECURITY (Revisited & Extended)
```

```
-----------------------------------------------------------------------
```

## `12. CRYPTOGRAPHY FUNDAMENTALS` 

```
-------------------------------
```

- `a) Symmetric Encryption: Same key for encrypt/decrypt` 

- `Fast, efficient — used for bulk data` 

- `Algorithms: AES-128/256, DES (legacy), 3DES (legacy), ChaCha20` 

- `Key challenge: Secure key exchange` 

## `b) Asymmetric Encryption: Public/private key pair` 

- `Slower but solves key exchange problem` 

- `Algorithms: RSA-2048/4096, ECC (ECDSA, Ed25519)` 

- `Use: Digital signatures, key exchange, certificate signing` 

- `c) Hash Functions: One-way function — fixed length output` 

- `Algorithms: MD5 (broken), SHA-1 (deprecated), SHA-256, SHA-3` 

- `Use: Password storage, file integrity verification` 

- `Salting: Adding random value to password before hashing` 

## `d) PKI (Public Key Infrastructure):` 

- `Framework for managing digital certificates and keys` 

- `Components: CA (Certificate Authority), RA, CRL, OCSP` 

- `TLS/SSL certificates use PKI` 

- `e) TLS 1.3 (Transport Layer Security):` 

- `Current standard for securing web communications` 

- `TLS 1.0/1.1 — deprecated; TLS 1.2 — acceptable; TLS 1.3 — recommended` 

- `Perfect Forward Secrecy (PFS): Each session uses unique key` 

- `f) Post-Quantum Cryptography (PQC) — Emerging 2026:` 

- `Threat: Quantum computers can break RSA and ECC` 

- `NIST PQC Standards (2024): CRYSTALS-Kyber (key exchange), CRYSTALS-Dilithium (digital signatures)` 

- `Organizations should begin PQC migration planning NOW` 

## `13. AUTHENTICATION MECHANISMS` 

```
-------------------------------
```

```
Authentication Factors:
```

```
  Factor 1 — Something you KNOW    : Password, PIN, security questions
  Factor 2 — Something you HAVE    : Smart card, hardware token, phone
  Factor 3 — Something you ARE     : Fingerprint, face, iris, voice
```

```
Multi-Factor Authentication (MFA):
```

- `Combining 2+ factors dramatically reduces account compromise` 

- `Types: OTP via SMS (weakest), TOTP (Google Auth), Push notification, FIDO2/WebAuthn (strongest — phishing-resistant)` 

```
Password Best Practices 2026:
```

- `Minimum 12-16 characters (PCI DSS v4.0 requires 12+)` 

- `No complexity rules — use passphrases instead` 

- `No periodic password changes unless compromised` 

- `Check against breach databases (Have I Been Pwned)` 

- `Use password manager + unique passwords per site` 

## `14. ACCESS CONTROL MODELS` 

## `---------------------------` 

```
+-------------+----------------------------------------------------------+
| MODEL       | DESCRIPTION & EXAMPLE                                    |
+-------------+----------------------------------------------------------+
| DAC         | Discretionary — owner sets permissions (Windows NTFS)   |
| MAC         | Mandatory — system enforces labels (military, SELinux)  |
| RBAC        | Role-Based — permissions based on job role (most common)|
| ABAC        | Attribute-Based — fine-grained, context-aware policies  |
| ReBAC       | Relationship-Based — Google Zanzibar, social graphs     |
| PAM         | Privileged Access Management — for admin accounts       |
+-------------+----------------------------------------------------------+
```

```
-----------------------------------------------------------------------
SESSION 7 — KEY TAKEAWAYS
```

```
-----------------------------------------------------------------------
```

- `Wireless security requires WPA3 minimum in 2026 — WEP is completely broken✔ Mobile devices are now the primary attack surface for most organizations✔` 

- `PCI DSS v4.0 governs payment card security globally✔` 

- `SIM swap attacks can defeat SMS-based 2FA✔` 

- `Tokenization and 3DS v2.0 are standard defenses for mobile payments✔` 

- `ISMS (ISO 27001) provides systematic approach to security management✔` 

- `TLS 1.3 and AES-256 are the 2026 encryption standards✔` 

- `Post-Quantum Cryptography planning should start now✔` 

- `FIDO2/WebAuthn is the strongest MFA option available✔` 

```
-----------------------------------------------------------------------
```

## `SESSION 7 — SELF-ASSESSMENT QUESTIONS` 

```
-----------------------------------------------------------------------
```

- `Q1. Compare WEP, WPA2, and WPA3 — why was each replaced?` 

- `Q2. What is an Evil Twin attack? How do you defend against it?` 

- `Q3. Explain SIM Swap Attack and why SMS 2FA can fail against it.` 

- `Q4. What is PCI DSS? List the 6 goals and 12 requirements.` 

- `Q5. Compare IDS and IPS — when would you use each?` 

- `Q6. What is tokenization in payment systems? How does it work?` 

- `Q7. Explain symmetric vs asymmetric cryptography with examples.` 

- `Q8. What is Zero Trust Architecture? Give 3 core principles.` 

- `Q9. Define RTO and RPO in business continuity planning.` 

- `Q10. What is Post-Quantum Cryptography and why does it matter in 2026?` 

```
-----------------------------------------------------------------------
SESSION 7 — KEY TERMS GLOSSARY
```

```
-----------------------------------------------------------------------
WPA3              : Wi-Fi Protected Access 3 — current Wi-Fi standard
Evil Twin         : Rogue AP mimicking legitimate Wi-Fi hotspot
SIM Swap          : Porting victim's phone number to attacker's SIM
PCI DSS           : Payment Card Industry Data Security Standard
Tokenization      : Replacing sensitive data with non-sensitive token
ISMS              : Information Security Management System
IDS/IPS           : Intrusion Detection/Prevention System
DMZ               : Demilitarized Zone — network security segment
SIEM              : Security Information & Event Management
TLS 1.3           : Current standard for transport layer security
FIDO2/WebAuthn    : Phishing-resistant authentication standard
PQC               : Post-Quantum Cryptography
RBAC              : Role-Based Access Control
PAM               : Privileged Access Management
```

```
Honeypot          : Decoy system to attract and study attackers
EMV               : Europay, Mastercard, Visa chip standard
```

```
================================================================================
SESSION 8 — CYBER CRIMES + INTRODUCTION TO ETHICAL HACKING
            Legal Aspects | Indian Laws | International Law |
            Ethical Hacking Terminology | Hacking Phases
            Theory: 2 Hours
```

```
================================================================================
```

```
-----------------------------------------------------------------------
PART A: CYBER CRIMES
```

```
-----------------------------------------------------------------------
```

## `1. DEFINITION OF CYBERCRIME` 

```
-----------------------------
```

```
Cybercrime: Any criminal activity that involves a computer, network, or
networked device. The computer may be the tool, the target, or both.
```

```
Categories:
```

```
  a) Computer as a Target   : Hacking, DDoS, malware infection
  b) Computer as a Tool     : Fraud, identity theft, online harassment
  c) Computer as Incidental : Drug trafficking records stored on computer
```

## `2. TYPES OF CYBERCRIMES (2026)` 

```
--------------------------------
+-----------------------------+----------------------------------------------+
| CRIME TYPE                  | DESCRIPTION & EXAMPLE                        |
+-----------------------------+----------------------------------------------+
| Hacking                     | Unauthorized access to systems               |
| Phishing                    | Credential theft via deceptive communications|
| Identity Theft              | Stealing PII to impersonate victim           |
| Online Fraud                | Fake shopping sites, investment scams        |
| Ransomware                  | Encrypting data and demanding payment        |
| Cyberstalking               | Using tech to stalk/harass individuals       |
| Cyberbullying               | Harassment via digital platforms             |
| Online Child Exploitation   | CSAM (Child Sexual Abuse Material)           |
| Corporate Espionage         | Stealing trade secrets/IP via cyber means    |
| Cryptocurrency Crime        | Crypto theft, darknet transactions, mixing   |
| AI-Powered Fraud (NEW 2026) | Deepfakes, AI phishing, automated fraud      |
| Supply Chain Attack         | Compromising software build/distribution     |
| Insider Trading via Hacking | Stock manipulation through hacked systems    |
+-----------------------------+----------------------------------------------+
```

## `3. UNDERSTANDING CYBER CRIMES IN CONTEXT OF INTERNET` 

```
------------------------------------------------------
Internet-specific factors amplifying cybercrime:
  - Anonymity       : Difficult to trace actual identity
  - Global reach    : Attack from any country against any target
  - Low cost        : Massive attacks with minimal investment
  - Speed           : Near-instantaneous attack execution
  - Automation      : Botnets automate attacks at scale
  - Jurisdiction    : Cross-border crimes complicate prosecution
  - Dark Web        : Marketplace for criminal tools and services
```

## `Dark Web in Context:` 

```
  - Surface Web    : Indexed content (~4% of internet)
  - Deep Web       : Non-indexed content (medical records, databases)
  - Dark Web       : Encrypted overlay networks (Tor, I2P)
  - Use in crime   : Stolen data markets, ransomware-as-a-service,
                     weapons, CSAM, hacking-for-hire services
```

## `4. LEGAL ASPECTS OF OPEN COMMUNICATIONS` 

```
-----------------------------------------
```

```
Legal Challenges in Internet Communications:
```

```
  a) Jurisdiction : Which country's law applies when attacker is in
```

```
  b) Attribution  : Proving WHO conducted the attack
```

```
  c) Evidence     : Digital evidence collection and preservation
```

```
  d) ISP Liability: When is an Internet Service Provider responsible?
```

```
  e) Encryption   : Law enforcement vs privacy rights debate
```

```
Key Legal Concepts:
```

- `Computer Forensics   : Legally admissible digital evidence collection` 

- `Chain of Custody     : Maintaining integrity of evidence` 

```
  - Digital Signatures   : Non-repudiation in digital communications
  - Wiretapping Law      : Legal interception of communications
```

- `Safe Harbor Doctrine : ISP protection for user-generated content` 

```
-----------------------------------------------------------------------
PART B: INDIAN PENAL LAW & CYBER CRIMES
```

```
-----------------------------------------------------------------------
```

## `5. INFORMATION TECHNOLOGY ACT 2000 (IT ACT)` 

```
---------------------------------------------
```

```
India's primary legislation for cybercrimes and electronic commerce.
```

```
Key Sections:
```

```
+----------+------------------------------------------------------------------+
| SECTION  | OFFENSE & PENALTY                                               |
+----------+------------------------------------------------------------------+
| S. 43    | Unauthorized access, downloading data, damage to computer      |
|          | Penalty: Compensation up to 1 crore INR                         |
+----------+------------------------------------------------------------------+
| S. 43A   | Corporate negligence — failure to protect sensitive data        |
|          | Penalty: Compensation for affected persons                       |
+----------+------------------------------------------------------------------+
| S. 65    | Tampering with computer source documents                        |
|          | Penalty: Up to 3 years imprisonment / 2 lakh fine              |
+----------+------------------------------------------------------------------+
| S. 66    | Computer-related offenses (hacking, data theft)                 |
|          | Penalty: Up to 3 years imprisonment / 5 lakh fine              |
+----------+------------------------------------------------------------------+
| S. 66A   | Sending offensive messages (struck down by SC in Shreya Singhal|
|          | v. Union of India, 2015 — FREE SPEECH implications)            |
+----------+------------------------------------------------------------------+
| S. 66B   | Dishonestly receiving stolen computer resource                  |
|          | Penalty: Up to 3 years / 1 lakh fine                           |
+----------+------------------------------------------------------------------+
| S. 66C   | Identity theft — fraudulently using electronic signature/password|
|          | Penalty: Up to 3 years / 1 lakh fine                           |
+----------+------------------------------------------------------------------+
| S. 66D   | Cheating by personation using computer resource                 |
|          | Penalty: Up to 3 years / 1 lakh fine                           |
+----------+------------------------------------------------------------------+
| S. 66E   | Violation of privacy — capturing/publishing private images      |
|          | Penalty: Up to 3 years / 2 lakh fine                           |
+----------+------------------------------------------------------------------+
| S. 66F   | CYBER TERRORISM — threatening national security via cyber attack|
|          | Penalty: LIFE IMPRISONMENT                                      |
+----------+------------------------------------------------------------------+
| S. 67    | Publishing obscene material in electronic form                  |
|          | Penalty: Up to 3 years / 5 lakh fine (first offense)           |
+----------+------------------------------------------------------------------+
| S. 67A   | Publishing sexually explicit material electronically            |
|          | Penalty: Up to 5 years / 10 lakh fine (first offense)          |
+----------+------------------------------------------------------------------+
| S. 67B   | Child pornography — publishing/transmitting CSAM                |
```

```
|          | Penalty: Up to 5 years / 10 lakh fine (first offense)          |
+----------+------------------------------------------------------------------+
| S. 69    | Power to intercept, monitor, or decrypt information             |
|          | (Government surveillance powers)                                |
+----------+------------------------------------------------------------------+
| S. 72    | Breach of confidentiality and privacy                           |
|          | Penalty: Up to 2 years / 1 lakh fine                           |
+----------+------------------------------------------------------------------+
6. INDIAN PENAL CODE (IPC) SECTIONS APPLICABLE TO CYBERCRIME
--------------------------------------------------------------
+----------+------------------------------------------------------------------+
| SECTION  | APPLICABILITY                                                   |
+----------+------------------------------------------------------------------+
| S. 415   | Cheating — online fraud, fake e-commerce sites                  |
| S. 420   | Cheating & dishonestly inducing delivery of property (fraud)    |
| S. 383   | Extortion — ransomware demands                                  |
| S. 499   | Defamation — online reputation damage                          |
| S. 500   | Punishment for defamation                                       |
| S. 503   | Criminal intimidation — cyber threats                           |
| S. 506   | Punishment for criminal intimidation                            |
| S. 292   | Sale of obscene books/material — applies to online pornography  |
| S. 293   | Obscene material to young persons                               |
| S. 354C  | Voyeurism — recording/watching women without consent            |
| S. 354D  | Stalking — includes online/cyber stalking                       |
| S. 509   | Word/gesture intending to insult modesty of woman               |
+----------+------------------------------------------------------------------+
7. DIGITAL PERSONAL DATA PROTECTION ACT 2023 (DPDPA) — NEW
------------------------------------------------------------
India's comprehensive data privacy law (effective 2024-2025):
  - Applies to digital personal data processed in India
  - Rights of Data Principals (individuals):
      * Right to access information
      * Right to correction and erasure
      * Right of grievance redressal
```

- `Right to nominate (digital inheritance)` 

- `Obligations of Data Fiduciaries (organizations):` 

- `Lawful processing, purpose limitation, data minimization` 

- `Security safeguards and breach notification` 

- `Appointing Data Protection Officer (DPO)` 

- `Significant Data Fiduciaries: Subject to additional obligations` 

- `Penalties: Up to INR 250 crore for major violations` 

## `8. FRAUD, HACKING, MISCHIEF IN CYBER LAW` 

```
------------------------------------------
```

```
Fraud:
```

- `Definition: Intentional deception for financial/personal gain` 

- `Cyber fraud examples: Fake bank websites, UPI fraud, KYC fraud` 

- `IPC S. 420 + IT Act S. 66D applicable` 

```
Hacking:
```

- `Legal definition (IT Act S. 66): Unauthorized access with criminal intent` 

- `Note: ETHICAL HACKING requires WRITTEN AUTHORIZATION` 

- `Without authorization, even "testing" is illegal` 

- `Penalties: 3 years imprisonment + 5 lakh fine` 

## `Mischief:` 

- `IT Act S. 65 & S. 66 cover destroying/altering data` 

- `IPC S. 425-440: Criminal mischief applies to cyber vandalism` 

```
-----------------------------------------------------------------------
PART C: INTERNATIONAL LAW & CYBER CRIMES
```

```
-----------------------------------------------------------------------
```

```
9. INTERNATIONAL CYBER LAW FRAMEWORK
```

```
--------------------------------------
```

```
a) Budapest Convention on Cybercrime (2001):
```

- `First international treaty on cybercrime` 

- `Addresses computer crimes: unauthorized access, data interference, system interference, computer-related fraud/forgery` 

- `68+ signatory countries (India is NOT a signatory)` 

## `b) United Nations (UN) Initiatives:` 

- `UN Group of Governmental Experts (GGE) on cyber norms` 

- `UN Open-Ended Working Group (OEWG) on cybersecurity` 

- `UN Resolution 73/27: Responsible state behavior in cyberspace` 

## `c) Tallinn Manual 2.0:` 

- `Academic study applying international law to cyberspace` 

- `Addresses state-sponsored attacks, cyber warfare` 

- `NOT binding law — but influential reference` 

## `d) GDPR (EU General Data Protection Regulation):` 

- `Applies to any organization processing EU citizens' data` 

- `Key rights: Access, erasure, portability, objection` 

- `Penalties: Up to €20 million or 4% of global annual revenue` 

- `Data breach notification: Within 72 hours to supervisory authority` 

## `e) CFAA (Computer Fraud and Abuse Act — USA):` 

- `Primary US federal cyber law` 

- `Criminalizes unauthorized computer access` 

- `Used in major hacking prosecutions (Aaron Swartz case)` 

## `f) NIS2 Directive (EU — 2024):` 

- `Network and Information Security Directive` 

- `Mandatory cybersecurity requirements for critical sectors` 

- `Stricter than original NIS directive` 

## `10. JURISDICTION CHALLENGES IN CYBER LAW` 

```
------------------------------------------
```

```
Key Principles for Determining Jurisdiction:
```

- `a) Territoriality   : Where did the crime occur?` 

- `b) Nationality      : Citizenship of the criminal or victim` 

- `c) Passive Personality: Victim's country asserts jurisdiction` 

- `d) Effects Doctrine : Where were the effects felt?` 

- `e) Universality     : Some crimes are prosecutable anywhere` 

```
Mutual Legal Assistance Treaties (MLATs):
```

- `Agreements between countries to assist in criminal investigations` 

- `Evidence sharing, server data requests` 

- `Challenge: Many cybercrime havens have no MLAT agreements` 

## `11. OBSCENITY AND PORNOGRAPHY ON THE INTERNET` 

```
-----------------------------------------------
```

```
Legal Framework in India:
```

- `IT Act S. 67: Obscene content online (up to 3 yrs/5 lakh)` 

- `IT Act S. 67A: Sexually explicit material (up to 5 yrs/10 lakh)` 

- `IT Act S. 67B: CSAM — Child Sexual Abuse Material (5 yrs/10 lakh)` 

- `IPC S. 292-294: Obscene publications and acts` 

- `POCSO Act: Protection of Children from Sexual Offenses (2012)` 

```
Global Platforms' Responsibility:
```

- `IT (Intermediary Guidelines and Digital Media Ethics Code) Rules 2021` 

- `Platforms required to remove harmful content within 24-36 hours` 

- `Significant Social Media Intermediaries must appoint: * Grievance Officer (India-based)` 

- `Nodal Contact Person (law enforcement liaison)` 

```
      * Chief Compliance Officer (legal responsibility)
```

```
-----------------------------------------------------------------------
PART D: INTRODUCTION TO ETHICAL HACKING
```

```
-----------------------------------------------------------------------
```

## `12. WHAT IS ETHICAL HACKING?` 

```
------------------------------
```

```
Definition: The authorized practice of bypassing system security to
identify potential data breaches and threats in a network.
```

```
Key Characteristics:
```

- `AUTHORIZED   — Written permission required (Rules of Engagement)✔` 

- `LEGAL        — Operating within defined legal boundaries✔` 

- `BOUNDED      — Defined scope (what can and cannot be tested)✔` 

- `DOCUMENTED   — Everything must be documented✔` 

- `REPORTED     — Findings reported to organization, not exploited✔` 

## `Ethical hacker role:` 

```
  "The ethical hacker thinks and acts like an attacker, but with legal
   authorization and the mission to improve security — not exploit it."
```

```
Why Organizations Need Ethical Hackers:
```

- `Identify vulnerabilities before real attackers do` 

- `Test effectiveness of existing security controls` 

- `Satisfy compliance requirements (PCI DSS, ISO 27001)` 

- `Demonstrate security posture to stakeholders` 

- `Reduce risk of data breaches (avg. cost $4.45M in 2025)` 

## `13. ETHICAL HACKING TERMINOLOGY (MASTER GLOSSARY)` 

```
----------------------------------------------------
```

```
+------------------+----------------------------------------------------------+
| TERM             | DEFINITION                                               |
+------------------+----------------------------------------------------------+
| Hacker           | Person who gains unauthorized/authorized access to systems|
| Ethical Hacker   | Authorized security professional testing for weaknesses  |
| Cracker          | Malicious hacker who BREAKS INTO systems illegally       |
| Penetration Test | Authorized simulated attack to find vulnerabilities       |
| Vulnerability    | A weakness in a system/application/process               |
| Exploit          | Code/technique that takes advantage of a vulnerability   |
| Threat           | Potential danger that could exploit a vulnerability      |
| Payload          | Malicious code that runs after an exploit succeeds       |
| Zero-Day         | Vulnerability unknown to vendor — no patch exists        |
| CVE              | Common Vulnerabilities and Exposures — vulnerability ID  |
| CVSS             | Common Vulnerability Scoring System (0-10 severity scale)|
| Attack Surface   | All possible points where attacker can try to enter      |
| Attack Vector    | The path/means used to gain unauthorized access          |
| Footprinting     | Information gathering about target (passive/active)      |
| Reconnaissance   | Initial phase of information collection                  |
| Enumeration      | Extracting usernames, shares, services from target       |
| Privilege Escal. | Gaining higher access than authorized                    |
| Lateral Movement | Moving from one system to another within a network       |
| Persistence      | Maintaining access after initial compromise              |
| Exfiltration     | Extracting data from compromised network                 |
| C2/C&C           | Command and Control — attacker's remote control channel  |
| Rootkit          | Malware hiding its presence at OS/kernel level           |
| Backdoor         | Secret method to bypass normal authentication            |
| Botnet           | Network of compromised machines controlled by attacker   |
| Social Engineering| Manipulating humans to bypass technical controls        |
| OSINT            | Open Source Intelligence — publicly available data       |
| Bug Bounty       | Program rewarding researchers for finding vulnerabilities|
| PoC (Proof of    | Code demonstrating a vulnerability is exploitable        |
| Concept)         |                                                          |
| Threat Modeling  | Structured process to identify and prioritize threats    |
```

```
| TTPs             | Tactics, Techniques, and Procedures (of threat actors)   |
| IoC (Indicator   | Evidence of a potential breach (IP, hash, domain)        |
| of Compromise)   |                                                          |
+------------------+----------------------------------------------------------+
```

```
14. TYPES OF HACKERS — COMPREHENSIVE CLASSIFICATION
-----------------------------------------------------
By Intent and Authorization:
+---------------+--------------------------------------------------------------+
| HACKER TYPE   | DESCRIPTION                                                  |
+---------------+--------------------------------------------------------------+
| White Hat     | Authorized security professionals — ethical hackers          |
|               | Work WITH organizations to find and fix vulnerabilities      |
+---------------+--------------------------------------------------------------+
| Black Hat     | Malicious hackers — unauthorized, criminal intent            |
|               | Goal: Financial gain, espionage, destruction                 |
+---------------+--------------------------------------------------------------+
| Grey Hat      | Sometimes authorized, sometimes not — moral ambiguity        |
|               | May disclose vulnerabilities without permission              |
+---------------+--------------------------------------------------------------+
| Green Hat     | Beginner/aspiring hackers learning their craft               |
+---------------+--------------------------------------------------------------+
| Blue Hat      | External security testers contracted by organizations        |
|               | Also: Microsoft's Blue Hat conference participants           |
+---------------+--------------------------------------------------------------+
| Red Hat       | Aggressive white hats who attack black hat infrastructure    |
+---------------+--------------------------------------------------------------+
| Script Kiddie | Unskilled attackers using pre-built tools without understand |
+---------------+--------------------------------------------------------------+
| Hacktivist    | Hackers with political/social agenda (Anonymous, etc.)       |
+---------------+--------------------------------------------------------------+
| Nation-State  | Government-sponsored hackers (APT groups)                    |
|               | Most sophisticated, best-resourced threat actors             |
+---------------+--------------------------------------------------------------+
| Suicide Hacker| Willing to face consequences to achieve their goal          |
+---------------+--------------------------------------------------------------+
| Cyber Warrior | Military/defense-focused hackers in cyberwarfare             |
+---------------+--------------------------------------------------------------+
```

## `15. IDENTIFYING DIFFERENT TYPES OF HACKING TECHNOLOGIES` 

```
---------------------------------------------------------
```

- `a) Password Cracking Technologies:` 

- `Brute Force      : Trying all possible combinations` 

- `Dictionary Attack: Using wordlist of common passwords` 

- `Rainbow Table    : Precomputed hash lookups` 

- `Credential Stuffing: Using leaked credentials from other breaches` 

## `b) Spoofing Technologies:` 

- `IP Spoofing      : Falsifying source IP address` 

- `MAC Spoofing     : Changing hardware address` 

- `Email Spoofing   : Forging sender address` 

- `DNS Spoofing     : Redirecting DNS queries to malicious IPs` 

- `c) Network-Based Technologies:` 

- `Packet Sniffing  : Capturing network traffic` 

- `MITM             : Intercepting and altering communications` 

- `Session Hijacking: Taking over an authenticated session - DNS Poisoning    : Corrupting DNS cache entries` 

## `d) Malware Technologies:` 

- `Viruses          : Self-replicating code attached to files` 

- `Worms            : Self-propagating without user action` 

- `Trojans          : Malware disguised as legitimate software` 

- `Ransomware       : Encrypts files, demands payment` 

```
   - Spyware          : Covert surveillance and data collection
```

```
   - Rootkits         : Hides malware/processes from OS
   - Fileless Malware : Lives in memory — no file on disk (hard to detect)
```

## `e) Web Application Technologies:` 

- `SQL Injection    : Injecting malicious SQL into input fields` 

```
   - XSS              : Injecting client-side scripts into web pages
```

```
   - CSRF             : Forcing browser to make unauthorized requests
```

- `SSRF             : Server-Side Request Forgery` 

```
   - XXE              : XML External Entity injection
```

## `f) Social Engineering Technologies:` 

- `Phishing toolkits  : GoPhish, Evilginx2` 

- `Deepfake tools     : AI-generated audio/video for impersonation` 

- `AI-Assisted OSINT  : LLM-powered reconnaissance automation` 

## `16. THE FIVE PHASES OF ETHICAL HACKING` 

```
----------------------------------------
This is the CORE METHODOLOGY used by ethical hackers:
```

```
PHASE 1 — RECONNAISSANCE (Information Gathering)
  Purpose: Gather as much information as possible about the target
  WITHOUT directly interacting with target systems (passive)
  OR with limited interaction (active).
```

## `Passive Recon:` 

- `OSINT (Open Source Intelligence)` 

- `Google Dorking (advanced Google search operators)` 

- `WHOIS lookups (domain registration info)` 

- `DNS enumeration (subdomain discovery)` 

- `Social media profiling (LinkedIn, Twitter, Instagram)` 

- `Job postings analysis (reveals technologies used)` 

- `Shodan (IoT/internet-connected device search engine)` 

- `Netcraft (web server info, hosting history)` 

- `Dark web monitoring (leaked credentials, mentions)` 

```
  Active Recon:
```

- `Ping sweeps, traceroute` 

- `Port scanning (with authorization only!)` 

- `Banner grabbing` 

- `Network sniffing` 

- `Social engineering calls/emails` 

```
  Key Tools: Maltego, Recon-Ng, theHarvester, Shodan, WHOIS,
             Netcraft, SpiderFoot, FOCA, Google Dorks
```

```
  MITRE ATT&CK Mapping: TA0043 (Reconnaissance)
```

## `PHASE 2 — SCANNING & ENUMERATION` 

```
  Purpose: Identify live hosts, open ports, services, OS details,
           and specific vulnerabilities in identified services.
```

## `Types of Scanning:` 

- `a) Network Scanning : Identify active hosts on network` 

- `b) Port Scanning    : Find open ports and listening services` 

- `c) Vulnerability Scanning: Identify known vulnerabilities in services` 

## `Key Scan Types (TCP-based):` 

- `TCP Connect Scan  : Full 3-way handshake (noisy, easily detected)` 

- `SYN Scan (Half Open): Only SYN → SYN-ACK (stealth scan)` 

- `NULL Scan         : No TCP flags set` 

- `FIN Scan          : FIN flag only` 

- `XMAS Scan         : FIN+PSH+URG flags set (looks like Xmas tree)` 

- `IDLE Scan         : Uses zombie host (hard to trace)` 

```
    - UDP Scan          : Finds UDP services
```

```
  Enumeration:
```

```
    - Extracting usernames, group names, shared resources, services
```

```
    - Protocols: NetBIOS, LDAP, SNMP, DNS, NTP
```

```
    - Tools: NMAP, Nessus, OpenVAS, enum4linux, SNMPwalk
```

```
  Key Tools: NMAP, Nessus, OpenVAS, Nikto, Masscan, Zmap
  MITRE ATT&CK Mapping: TA0007 (Discovery), TA0043 (Reconnaissance)
```

```
PHASE 3 — GAINING ACCESS (Exploitation)
  Purpose: Exploit identified vulnerabilities to gain unauthorized
           access to systems (always within authorized scope).
```

```
  Methods:
```

```
    - Password cracking      : Hydra, Hashcat, John the Ripper
```

```
    - Exploitation frameworks: Metasploit, Cobalt Strike, Sliver
```

```
    - Web app exploits       : SQLmap, Burp Suite
```

```
    - Buffer overflow attacks: Custom shellcode
```

```
    - Social engineering     : Phishing, pretexting
```

- `Physical access        : Bypassing locks, USB drops` 

```
  MITRE ATT&CK Mapping: TA0001 (Initial Access), TA0002 (Execution)
```

```
PHASE 4 — MAINTAINING ACCESS (Post-Exploitation)
  Purpose: Demonstrate how an attacker could maintain persistence
           within a compromised system over time.
```

```
  Techniques:
```

- `Installing backdoors  : Netcat, Metasploit Meterpreter` 

- `Privilege escalation  : Gaining admin/root from limited user` 

- `Creating new accounts : Hidden admin accounts` 

- `Scheduled tasks/cron  : Persistence mechanisms` 

- `Registry run keys     : Windows persistence` 

- `Rootkit installation  : Hiding presence from detection` 

- `Lateral movement      : Pivoting to other systems` 

- `Data exfiltration     : Demonstrating what could be stolen` 

```
  MITRE ATT&CK Mapping: TA0003 (Persistence), TA0004 (Priv. Escalation),
                         TA0008 (Lateral Movement), TA0010 (Exfiltration)
```

```
PHASE 5 — COVERING TRACKS (Reporting in Ethical Context)
  Purpose: In ethical hacking, this phase is about DOCUMENTING what
           an attacker could hide — not actually hiding your own activity.
           Understanding evasion helps defenders improve detection.
```

```
  Attacker Techniques to Understand:
```

- `Log clearing/manipulation` 

- `Timestomping (modifying file timestamps)` 

- `Steganography (hiding data in images/audio)` 

- `Encryption of C&C traffic` 

- `Living off the Land (using built-in tools: PowerShell, WMI)` 

- `Anti-forensics: File shredding, disk wiping` 

```
  Ethical Hacker's Responsibility:
```

- `RESTORE systems to original state post-testing` 

- `DOCUMENT all actions taken during engagement` 

- `SUBMIT comprehensive report to client` 

- `NEVER retain access after engagement ends` 

```
  MITRE ATT&CK Mapping: TA0005 (Defense Evasion), TA0006 (Credential Access)
```

```
-----------------------------------------------------------------------
```

```
SESSION 8 — KEY TAKEAWAYS
```

```
-----------------------------------------------------------------------
```

- `IT Act 2000 S. 66 & 66F are primary hacking offenses in India✔` 

- `DPDPA 2023 is India's new data privacy law — understand it well✔` 

- `Hacking WITHOUT written authorization is ILLEGAL — always✔` 

- `Ethical hacking has 5 phases: Recon → Scan → Exploit → Persist → Report✔` 

- `MITRE ATT&CK maps every attack phase to known adversary behaviors✔` 

- `Budapest Convention is the key international cybercrime treaty✔` 

- `India's IT Act + IPC together cover most cyber offense scenarios✔` 

- `Obscenity laws (S. 67, 67A, 67B) carry significant penalties✔` 

- `Understanding TTPs is as important as understanding tools✔` 

```
-----------------------------------------------------------------------
SESSION 8 — SELF-ASSESSMENT QUESTIONS
```

```
-----------------------------------------------------------------------
```

- `Q1. What are the key sections of the IT Act 2000 related to hacking?` 

- `Q2. Explain the 5 phases of ethical hacking with their MITRE ATT&CK mapping.` 

- `Q3. What is DPDPA 2023? What rights does it give data principals?` 

- `Q4. Differentiate between white hat, black hat, and grey hat hackers.` 

- `Q5. What is the Budapest Convention? Why is India not a signatory?` 

- `Q6. Define zero-day vulnerability and CVE. How is CVSS used?` 

- `Q7. What is the difference between passive and active reconnaissance?` 

- `Q8. Explain the legal requirements for conducting ethical hacking.` 

- `Q9. What are the key challenges of internet jurisdiction in cybercrime?` 

- `Q10. What are the penalties under IT Act S. 67B for CSAM?` 

```
-----------------------------------------------------------------------
SESSION 8 — KEY TERMS GLOSSARY
```

```
-----------------------------------------------------------------------
IT Act 2000       : Information Technology Act — India's primary cyber law
DPDPA 2023        : Digital Personal Data Protection Act — India
GDPR              : EU General Data Protection Regulation
Budapest Conv.    : First international treaty on cybercrime
CVE               : Common Vulnerabilities and Exposures
CVSS              : Common Vulnerability Scoring System (0-10)
Zero-Day          : Vulnerability with no existing patch
Ethical Hacker    : Authorized security professional
Reconnaissance    : Phase 1 of ethical hacking — information gathering
Enumeration       : Extracting service/user details from target
Exploitation      : Gaining access through vulnerabilities
Persistence       : Maintaining access post-compromise
OSINT             : Open Source Intelligence
Deepfake          : AI-generated media for impersonation
IoC               : Indicator of Compromise
Rules of Engagement: Authorized scope and boundaries of pentest
Chain of Custody  : Preserving evidence integrity in digital forensics
```

```
================================================================================
                    *** END OF SESSIONS 6, 7 & 8 NOTES ***
================================================================================
```

```
UPCOMING SESSIONS PREVIEW:
```

```
---------------------------------------------------------------------------
SESSION 9  : Types of Hacker Classes | Red/Blue/Grey Teams | Skills for
             Ethical Hackers | Security Triangle
SESSION 10 : Security Evaluation Plan | Footprinting in Depth |
             Social Engineering | Scanning Methodologies in Detail
SESSION 11 : TCP Flags | Banner Grabbing | Proxy Attacks | IP Spoofing |
             Enumeration Techniques | SMB Attacks | DDoS Overview
SESSION 12 : Password Cracking Countermeasures | Active/Passive/Offline Attacks
|
```

```
             Keyloggers | Trojans & Backdoors | Netcat Trojan
SESSION 13 : Trojan Construction | Countermeasures | Evasion Techniques
SESSION 14 : Virus vs Worm | Malware Types | AV Evasion | Detection Methods
```

```
SESSION 15 : Sniffing (Active/Passive) | ARP Poisoning | DNS Spoofing | MAC
Flooding
SESSION 16 : DoS/DDoS | Botnets | Smurf Attacks | SYN Flooding | Session
Hijacking
SESSION 17 : Web Server Hacking | OWASP Top 10 | Web Passwords | Wireless
Hacking
```

```
SESSION 18 : Backdoors | Linux Hacking | IDS/Honeypots/Firewalls | DMZ Setup
SESSION 19 : Physical Security | Penetration Testing Methodologies (PTES,
OSSTMM)
```

```
SESSION 20 : Malware Reverse Engineering | Static & Dynamic Analysis |
             Ransomware-as-a-Service | AI-Powered Malware
```

```
LEARNING RESOURCES (2026 Recommended):
```

```
---------------------------------------------------------------------------
TOOLS TO INSTALL (Practice Environment Only):
```

```
  - Kali Linux 2024.4+      : Primary pentesting OS
  - VirtualBox/VMware       : Virtualization for safe lab
```

```
  - NMAP                    : Network scanner
```

```
  - Burp Suite Community    : Web app security testing
  - Wireshark               : Packet capture and analysis
```

```
  - Metasploit Framework    : Exploitation framework
```

```
  - Nessus Essentials       : Vulnerability scanner (free tier)
  - OWASP ZAP               : Web app scanner (open source)
  - Ghidra                  : NSA's reverse engineering tool (free)
```

```
PRACTICE PLATFORMS (Legal & Safe):
```

```
  - TryHackMe (tryhackme.com)   : Beginner-friendly guided rooms
```

```
  - Hack The Box (hackthebox.com): Intermediate/advanced CTF-style
```

```
  - OWASP WebGoat              : Intentionally vulnerable web app
```

```
  - DVWA                       : Damn Vulnerable Web Application
```

```
  - VulnHub                    : Downloadable vulnerable VMs
```

```
  - picoCTF                    : Beginner CTF (Carnegie Mellon)
```

```
CERTIFICATIONS PATHWAY (2026 Recommended):
  Level 1 (Foundation) : CompTIA Security+, CompTIA Network+
  Level 2 (Ethical Hack): CEH v13 (EC-Council), eJPT (eLearnSecurity)
  Level 3 (Advanced)   : OSCP (Offensive Security), PNPT (TCM Security)
  Level 4 (Expert)     : OSED, OSEP, CISSP, CISM
```

```
IMPORTANT LEGAL REMINDER (Repeated for Emphasis):
```

```
---------------------------------------------------------------------------
"Performing any hacking technique on systems you do not own or do not
have EXPLICIT WRITTEN PERMISSION to test is a CRIMINAL OFFENSE under:
  - IT Act 2000 (India)    : Sections 43, 65, 66 — imprisonment + fines
  - IPC (India)            : Sections 415, 420, 425 as applicable
  - CFAA (USA)             : Federal criminal prosecution
  - Computer Misuse Act    : UK criminal law
  - Budapest Convention    : International framework
```

```
Always obtain written authorization. Always define the scope. Always
document everything. Always restore systems after testing.
Your integrity as a security professional depends on it."
```

```
================================================================================
               PGCP-ITISS | ACTS, Pune | February 2026 Edition
          Compiled & Enhanced for 2026+ Curriculum | CEH v13 Aligned
               MITRE ATT&CK v15 | DPDPA 2023 | PCI DSS v4.0 | ISO 27001
================================================================================
```

