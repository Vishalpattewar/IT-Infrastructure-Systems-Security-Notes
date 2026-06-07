# 🔍 Cybersecurity Study Notes — Session 10A

Personal notes I'm maintaining while studying ethical hacking and cybersecurity concepts.
This session covers the Security Evaluation Plan, types of ethical hacks, footprinting & OSINT, social engineering in recon, traceroute mechanics, and the OSINT framework.

> [!NOTE]
> Session 10A is about **Phase 1 — Reconnaissance**. Everything in Phases 2–5 depends on how well Phase 1 is done. Professional pentesters spend 30–40% of total engagement time just on reconnaissance.

---

## 📚 Table of Contents

- [Where This Session Fits](#-where-this-session-fits)
- [Section 1 — Creating a Security Evaluation Plan](#section-1--creating-a-security-evaluation-plan)
  - [What is a Security Evaluation Plan?](#11-what-is-a-security-evaluation-plan)
  - [Components of a SEP](#12-components-of-a-security-evaluation-plan)
  - [The "Get Out of Jail Free" Card](#13-the-get-out-of-jail-free-card)
  - [Pentest Frameworks](#14-pentest-frameworks)
- [Section 2 — Types of Ethical Hacks](#section-2--types-of-ethical-hacks)
  - [By Knowledge Level](#21-classification-by-knowledge-level)
  - [By Attack Surface](#22-classification-by-attack-surface)
  - [By Execution Method](#23-classification-by-execution-method)
- [Section 3 — Footprinting](#section-3--footprinting--the-foundation-of-phase-1)
  - [What is Footprinting?](#31-what-is-footprinting)
  - [What Data is Targeted](#32-what-data-is-targeted-in-footprinting)
  - [Passive vs Active Footprinting](#33-passive-vs-active-footprinting)
  - [Footprinting Methodology](#34-the-footprinting-methodology)
  - [Certificate Transparency](#35-certificate-transparency--a-goldmine-for-recon)
- [Section 4 — Social Engineering in Reconnaissance](#section-4--social-engineering-in-reconnaissance)
  - [Why Social Engineering is a Recon Tool](#41-why-social-engineering-is-a-recon-tool)
  - [Passive Social Engineering Recon](#42-passive-social-engineering-recon)
  - [Active Social Engineering Recon](#43-active-social-engineering-recon)
- [Section 5 — Traceroute in Footprinting](#section-5--traceroute-in-footprinting)
  - [What is Traceroute?](#51-what-is-traceroute)
  - [How Traceroute Works — Packet Level](#52-how-traceroute-works--the-packet-level)
  - [Traceroute Variants](#53-traceroute-variants)
  - [What Traceroute Reveals](#54-what-traceroute-reveals-to-an-attacker)
  - [How Defenders Detect Traceroute](#55-how-defenders-detect-traceroute)
- [Section 6 — OSINT Framework](#section-6--osint-framework)
  - [What is OSINT?](#61-what-is-osint)
  - [Categories of OSINT Sources](#62-categories-of-osint-sources)
  - [Google Dorking](#63-google-dorking)
  - [OSINT Framework Tool](#64-osint-framework-tool)
- [Section 7 — MITRE ATT&CK TA0043 Mapping](#section-7--mitre-attck-ta0043--reconnaissance-mapping)
- [Section 8 — 2026 Context: Evolution of Reconnaissance](#section-8--2026-context--the-evolution-of-reconnaissance)
  - [AI-Assisted OSINT](#81-ai-assisted-osint)
  - [Data Brokers](#82-data-brokers)
  - [Digital Footprint Awareness](#83-digital-footprint-awareness--defender-perspective)
- [Key Takeaways](#-session-10a--key-takeaways)
- [Glossary](#-session-10a--glossary)

---

## 🗺️ Where This Session Fits

```
  SESSIONS 6-9      SESSIONS 10-11       SESSIONS 12-14    SESSIONS 15-18
  [FOUNDATIONS]  →  [RECONNAISSANCE  →   [EXPLOITATION] →  [ADVANCED ATTACKS]
                     & SCANNING]
                          ↑
                    YOU ARE HERE
                    (Session 10A)
```

Within the 5 Phases of Ethical Hacking:

| Phase 1 | Phase 2 | Phase 3 | Phase 4 | Phase 5 |
|---|---|---|---|---|
| **RECONNAISSANCE** ← *here* | SCANNING | GAINING ACCESS | MAINTAINING ACCESS | COVERING TRACKS |
| Session 10A | Session 10B, 11 | Sessions 12–17 | Session 18 | Session 20 |

---

## Things to Remember About Recon

| Misconception | Reality |
|---|---|
| "Recon is just Googling the target" | Recon is a structured, multi-layer discipline using dozens of data sources. Google is ONE tool in a large arsenal. |
| "I'll skip recon and go straight to scanning" | Scanning without recon is like navigating a city with no map. Wastes time, makes noise, misses critical attack paths. |
| "Passive recon means doing nothing" | Passive means NOT interacting with the TARGET directly. You ARE actively querying third-party sources. |
| "More data = better recon" | Unprocessed data is useless. The skill is in ANALYZING and CONNECTING data points to build an actionable picture. |
| "Social engineering is only done during exploitation" | Social engineering begins IN reconnaissance — gathering employee names, org structure, tech stack from LinkedIn. |
| "Traceroute just shows network hops — not useful" | Traceroute reveals network topology, ISPs, geographic location, and firewall positions. Critical intelligence. |

---

## Section 1 — Creating a Security Evaluation Plan

### 1.1 What is a Security Evaluation Plan?

A **Security Evaluation Plan (SEP)** — also called a Penetration Testing Plan or Scope of Work (SoW) — is a formal, written document that defines EXACTLY what will be tested, HOW, WHO is authorized, WHEN testing can occur, and WHAT the rules are.

**Without a SEP:**
- Tester doesn't know what's in scope → tests wrong things
- Client doesn't know what to expect → panics when attacks start
- Legal protection disappears → ethical hacker becomes a criminal
- Evidence cannot be collected properly → findings are disputed
- Emergency response is unclear → real incidents confused with tests

**With a SEP:**
- Everyone knows their role
- Legal authorization is documented
- Tester is protected if something breaks
- Client can inform their SOC (or keep it secret for realistic testing)
- Results are defensible in board reports and compliance audits

> [!IMPORTANT]
> A SEP is negotiated and signed BEFORE a single packet is sent. Both parties — client and tester — sign it. It is a **legally binding document**. Violating it (even going out of scope) can be grounds for criminal prosecution.

---

### 1.2 Components of a Security Evaluation Plan

A professional SEP contains ALL of the following:

| Component | What It Defines |
|---|---|
| **1. Parties Involved** | Legal identity of client org (authorized signer) and testing firm/individual (certifications) |
| **2. Objective Statement** | The PURPOSE — what business question are we answering? Not just "hack us and see what happens" |
| **3. Scope Definition** | EXACTLY what is authorized. Included: IP ranges, domains, apps, social engineering targets. Excluded: Production DBs, payment systems, third-party infra. **Out-of-scope = DO NOT TOUCH.** |
| **4. Timeline** | Start/end date/time. Testing windows. E.g., "Mon–Fri 9PM–6AM only" |
| **5. Rules of Engagement (RoE)** | What attack types are ALLOWED and FORBIDDEN. Social engineering: who can be targeted? |
| **6. Testing Methodology** | Black/White/Grey Box. Manual/Automated/Hybrid. Framework: PTES, OWASP, OSSTMM, NIST |
| **7. Emergency Contacts** | Client primary tech + management. Tester lead contact. "Get-out-of-jail" contact for law enforcement confirmation |
| **8. Deliverables** | Executive Summary (C-Level) · Technical Report (IT/Security) · Raw Findings (Appendix) · Remediation Guidance |
| **9. Data Handling** | How sensitive data found during testing is stored, transmitted, and destroyed. E.g., "All data encrypted with AES-256. Destroyed within 30 days." |
| **10. Tester Credentials** | Qualifications, certifications, clearances. Relevant: CEH, OSCP, GPEN, CREST |
| **11. Legal Authorization Statement** | "This document authorizes [Tester] to perform [defined activities] against [defined targets] during [defined period]." Signed by authorized representative. |
| **12. Incident Handling** | What if we accidentally hit out-of-scope? Cause unintended disruption? Discover an active breach mid-test? All scenarios need predefined responses. |

---

### 1.3 The "Get Out of Jail Free" Card

A short letter (authorization letter) carried by the pentester during the engagement — separate from the full SEP, shorter, more portable.

**Why it exists:** Imagine scanning a corporate network at 2AM (authorized). Security guard notices unusual activity. Police arrive. Without this letter, you look like a criminal. WITH it, you can immediately prove authorization.

**What it contains:**
- Client organization name and address
- Statement of authorization
- IP ranges and systems in scope
- Testing dates and times
- Emergency contact name and phone number
- Authorized signature from a senior executive (CTO, CISO, CEO)

> [!WARNING]
> **Coalfire Case (2019):** Two Coalfire Security testers were ARRESTED during a physical pentest of an Iowa courthouse. They had proper authorization letters but were still detained for 11 days before charges were dropped. This case changed how physical pentest authorization letters are structured across the industry.
>
> **Lesson:** The letter must be on company letterhead, signed by someone senior enough that law enforcement respects it, include a 24/7 phone number, and be specific about WHAT you are authorized to do.

---

### 1.4 Pentest Frameworks

Structured methodologies defining HOW a penetration test should be conducted.

| Framework | Focus | Key Details |
|---|---|---|
| **PTES** | Most widely used for commercial pentests | 7 phases: Pre-engagement → Intel Gathering → Threat Modeling → Vuln Analysis → Exploitation → Post-Exploitation → Reporting |
| **OWASP Testing Guide (v4.2)** | Web application security testing | 12 categories covering all aspects of web security. Free, open source. |
| **OSSTMM** | Highly formal, metric-driven | Covers physical, digital, human, wireless. Produces quantifiable security metrics (not just pass/fail). |
| **NIST SP 800-115** | US government standard | 4 phases: Planning → Discovery → Attack → Reporting |
| **MITRE ATT&CK Emulation Plans** | Red Team engagements (2024–2026) | Emulate SPECIFIC known threat actor TTPs. E.g., "Emulate APT29 behavior against our network" |

---

## Section 2 — Types of Ethical Hacks

### 2.1 Classification by Knowledge Level

The amount of information given to a tester before starting affects what they test, how they test, and what they find.

| Type | Knowledge | Simulates | Pros | Cons | Best For |
|---|---|---|---|---|---|
| **Black Box** (Zero Knowledge) | ZERO — no IPs, no architecture, no creds | External attacker with no insider info | Closest to real-world attack | Time-consuming. May miss internal vulns. | External perimeter, new client assessment, demonstrating risk to execs |
| **White Box** (Full Knowledge) | COMPLETE — source code, network diagrams, creds, docs | Insider threat OR trusted audit | Most thorough — widest coverage | Not realistic as external attack sim | Code review, internal audit, compliance, pre-deployment review |
| **Grey Box** (Partial Knowledge) | PARTIAL — e.g., user-level creds + basic architecture | Insider threat / attacker with some data | Most realistic for modern threats | Results depend on what info was shared | Internal network from user perspective, post-phishing breach sim |

**Which is best?** There is no "best" — it depends on the question being asked. Most mature organizations do ALL THREE over a 12-month cycle:

| Quarter | Test Type |
|---|---|
| Q1 | Black Box (external attack simulation) |
| Q2 | Grey Box (insider threat simulation) |
| Q3 | White Box (code + architecture review) |
| Q4 | Red Team (full adversary simulation — all combined) |

---

### 2.2 Classification by Attack Surface

| Hack Type | What is Targeted | Includes |
|---|---|---|
| **Network Hacking** | Routers, switches, firewalls, protocols | Port scanning, MITM, sniffing, DoS, ARP poisoning, VLAN hopping, BGP hijacking |
| **Web App Hacking** | Web applications | SQLi, XSS, CSRF, SSRF, IDOR, broken auth, API attacks. Framework: OWASP Top 10 |
| **System Hacking** | Operating systems and server software | Privilege escalation, password cracking, buffer overflow, kernel exploits, rootkits |
| **Social Engineering** | People — social media, email, phone | Phishing, vishing, pretexting, baiting, tailgating |
| **Wireless Hacking** | Wi-Fi, Bluetooth, cellular networks | WEP/WPA cracking, evil twin, deauth, Bluetooth attacks, rogue APs |
| **Physical Hacking** | Physical security controls | Lock picking, tailgating, badge cloning, USB drops, dumpster diving |
| **Cloud Hacking** *(Critical 2026)* | Cloud infrastructure | IAM exploitation, S3 bucket misconfig, metadata service SSRF, container escapes |
| **Mobile Hacking** | Mobile apps and devices | APK reverse engineering, SSL pinning bypass, insecure data storage, deep link abuse |
| **AI System Hacking** *(NEW 2025–26)* | AI/ML systems | Prompt injection, model poisoning, adversarial examples, training data poisoning, LLM jailbreaking |

---

### 2.3 Classification by Execution Method

| Method | Description | Pros | Cons | Used For |
|---|---|---|---|---|
| **Automated** | Tools run tests automatically (Nessus, OpenVAS) | Fast, consistent, wide surface | High false positives, misses logic flaws, can't chain creatively | Initial discovery, compliance scanning |
| **Manual** | Human tester manually probes and exploits | Finds business logic flaws, creative attack paths | Time-consuming, expensive, tester-dependent | Critical systems, deep application review |
| **Hybrid** | Automated for breadth + manual for depth | **Best practice in 2026** | Requires both tools and skill | Auto scan → human validates and digs deeper |

---

## Section 3 — Footprinting: The Foundation of Phase 1

### 3.1 What is Footprinting?

Footprinting is the process of systematically collecting information about a target organization, its systems, network, and people — BEFORE attempting any form of attack or testing.

It's the **foundation** upon which all subsequent phases are built. Like an architect studying blueprints before construction begins.

**Why footprinting is done FIRST:**

| Reason | Explanation |
|---|---|
| **Efficiency** | Without knowing what's there, you waste time attacking the wrong things |
| **Stealth** | Targeted scanning based on good recon = harder to detect |
| **Attack Surface Discovery** | Reveals systems, people, and relationships that automated scanners would never find |
| **Understanding the Target** | Business, partners, suppliers, employees, tech stack, security posture, regulatory environment |
| **Safety** | Knowing what's in scope vs out of scope becomes easier with full topology |

**How long does professional footprinting take?**

| Context | Time Spent |
|---|---|
| Bug bounty hunter | Hours to days |
| Standard pentest (1 week) | 1–2 days (30% of engagement) |
| Red Team (1 month) | 1–2 weeks (30–40%) |
| APT (nation-state actor) | Months of continuous reconnaissance |

> [!TIP]
> "The more time spent on reconnaissance, the less time wasted on failed attacks."

---

### 3.2 What Data is Targeted in Footprinting

Professional footprinting seeks information across **7 categories**:

<details>
<summary>📡 Category 1 — Network Information</summary>

- IP address ranges (what IPs does the org own?)
- Domain names and subdomains
- DNS records (MX, A, AAAA, CNAME, TXT, SOA, NS)
- Network topology (how are systems connected?)
- Firewall and IDS/IPS identification
- Network protocols in use
- ISP and hosting provider information
- BGP routing information (which ASN does org use?)

</details>

<details>
<summary>💻 Category 2 — System Information</summary>

- Operating systems in use (Windows, Linux, versions)
- Open ports and services running on those ports
- Software versions (web servers, databases, frameworks)
- Patch levels and known vulnerabilities
- Cloud services in use (AWS, Azure, GCP)
- IoT devices visible from internet

</details>

<details>
<summary>🏢 Category 3 — Organizational Information</summary>

- Organization structure and hierarchy
- Employee names, roles, and contact information
- Physical locations of offices and data centers
- Business partners and suppliers (supply chain map)
- Mergers and acquisitions (merged systems often have gaps)
- Regulatory environment (compliance requirements)
- Financial information (publicly available filings)

</details>

<details>
<summary>👤 Category 4 — People Information (Human Intelligence)</summary>

- Employee email format (firstname.lastname@company.com?)
- Social media profiles (LinkedIn, Twitter, Facebook, GitHub)
- Technical skills of employees (what tech do they know?)
- Travel schedules of key personnel (for social engineering)
- Personal email addresses (for targeted phishing)
- Photos of offices/equipment (may reveal tech, access controls)
- Published CVs/resumes (reveals exact tools and systems used)

</details>

<details>
<summary>🌐 Category 5 — Web Information</summary>

- Website technology stack (CMS, frameworks, libraries)
- Web application structure and functionality
- Development and staging environments (often less secured)
- Code repositories (GitHub, GitLab — may contain secrets)
- JavaScript files (may reveal internal API endpoints)
- Comments in HTML source (may reveal sensitive info)
- Historical versions of website (Wayback Machine)
- Login portals and admin interfaces

</details>

<details>
<summary>🛡️ Category 6 — Security Posture Information</summary>

- Email security (SPF, DKIM, DMARC records)
- Certificate details (SSL certs reveal subdomains)
- Job postings for security roles (reveals security tools used)
- Public breach history (HaveIBeenPwned, leaked credentials)
- Bug bounty programs (reveals what they DO and DON'T test)
- Incident reports and press releases about past breaches

</details>

<details>
<summary>🏗️ Category 7 — Physical Information</summary>

- Office locations and maps
- Building access control systems (visible in photos)
- Security camera placement (photos/Google Maps)
- Employee badge systems (from conference photos)
- Parking lot layout (for tailgating planning)
- Delivery entry points (for physical penetration test)

</details>

---

### 3.3 Passive vs Active Footprinting

The line between passive and active: **"Did any of my activity reach the TARGET'S systems?"**

#### Passive Footprinting

No packets reach the target's infrastructure. You query **third-party sources** that hold information ABOUT the target. Target **cannot detect** your reconnaissance.

| Example | What You Query |
|---|---|
| Searching Google for info about target | Google servers |
| WHOIS lookup | WHOIS servers (not target) |
| Checking Shodan for their IP ranges | Shodan database |
| Reading LinkedIn company page | LinkedIn |
| Wayback Machine archived versions | Archive.org |
| Checking job postings | Job sites |
| Certificate transparency logs | crt.sh |
| Reading public GitHub repos | GitHub |
| Checking DNS via third-party resolver | Third-party DNS |

**Legal Status:** Generally legal even without authorization because you're accessing publicly available information. However — even legal recon should be within authorized scope for professional engagements.

---

#### Active Footprinting

Packets **DIRECTLY** reach the target's infrastructure. Target **CAN detect** your activity. **Requires authorization.**

| Example | What Happens |
|---|---|
| Pinging target servers | ICMP packets hit their systems |
| Traceroute to their servers | Packets traverse their network |
| Port scanning their IP ranges | Your scanner hits their servers |
| Banner grabbing | You connect to their services |
| DNS zone transfer attempt | You query THEIR DNS server directly |
| Sending social engineering emails | Reaches their mail server |
| Calling employees | Direct contact |
| Visiting physical location | Direct contact |

**Legal Status:** Requires written authorization in all cases. Unauthorized port scanning is a violation of IT Act 2000 (India) and equivalent laws globally.

---

#### Visual Distinction

```
PASSIVE: YOU → [GOOGLE]        → info about TARGET    (target unaware)
         YOU → [WHOIS servers]  → domain info          (target unaware)
         YOU → [SHODAN]         → device info           (target unaware)

ACTIVE:  YOU → TARGET directly  → information           (target CAN detect)
         YOU → [TARGET server]  → banner/response        (logged in target)
```

---

### 3.4 The Footprinting Methodology

Each step builds on the previous — like assembling a puzzle.

| Step | Activity | Tools |
|---|---|---|
| **1 — Define Objectives & Scope** | What are you trying to achieve? What systems are in scope? | — |
| **2 — Identify Target Organization** | Confirm legal name, domains, IPs. Identify subsidiaries. Understand business model and crown jewel assets. | WHOIS, LinkedIn, company website, corporate filings |
| **3 — Gather Network Intelligence** | IP ranges, domains, DNS records, email security config | WHOIS, nslookup, dig, dnsdumpster, Shodan, Censys |
| **4 — Gather Employee & Org Intelligence** | Who works there? Roles? Technology they use? Org hierarchy? | LinkedIn, Maltego, theHarvester, Hunter.io, OSINT Framework |
| **5 — Gather Web & App Intelligence** | What's the site built on? Dev/staging environments? Public code repos? | Netcraft, Wappalyzer, Wayback Machine, FOCA, Recon-Ng |
| **6 — Gather Security Posture Intelligence** | Email security strength? Known breaches? Security tools from job postings? | MXToolbox, HaveIBeenPwned, Shodan, Google Dorks |
| **7 — Consolidate & Analyze** | Map all data into a coherent picture. Identify gaps and promising attack vectors. | Maltego (visual link analysis), spreadsheets, Dradis Framework |
| **8 — Document & Report** | Record ALL findings with source, date, and relevance. Becomes the intelligence baseline for Phases 2–5. | Dradis, PlexTrac, Notion, CherryTree |

---

### 3.5 Certificate Transparency — A Goldmine for Recon

**Certificate Transparency (CT)** is a public log of ALL SSL/TLS certificates ever issued for any domain. Created for security purposes — but massively useful for reconnaissance.

**Why it matters:**
Every time an organization creates a web server (even internal staging servers), they often get an SSL certificate. That certificate gets logged publicly — **forever**. Attackers search these logs to find:

- Subdomains not visible through normal DNS queries
- Dev/staging environments (dev.company.com)
- Internal systems accidentally given public certificates
- Historical systems (may still exist but not publicized)

**How to use it:**

| Tool | Usage |
|---|---|
| [crt.sh](https://crt.sh) | Search for `%.targetcompany.com` |
| Result | Every subdomain that ever had a certificate issued |
| Reveals | api.company.com, staging.company.com, vpn.company.com, admin.company.com, etc. |

**Real Example:** In 2021, security researchers found Facebook's internal staging and development servers through certificate transparency logs. These servers had different (weaker) security configurations than production — making them valuable initial access points.

---

## Section 4 — Social Engineering in Reconnaissance

### 4.1 Why Social Engineering is a Recon Tool

Most people think social engineering is an attack phase technique. In **reconnaissance**, social engineering is used as an **information gathering** technique — to extract intelligence that no tool can find.

Tools can find IP addresses, open ports, and software versions. But tools CANNOT tell you:
- Which employee is most likely to click a phishing link?
- What is the company's backup schedule?
- Which floor is the server room on?
- Is the CISO on vacation this week?
- What password reset process does help desk use?

This intelligence comes from **people** — and social engineering is how you collect it (with authorization).

---

### 4.2 Passive Social Engineering Recon

Gathering human intelligence from **publicly available sources** without any direct contact with target employees.

#### LinkedIn — The Recon Goldmine

| What to Look For | Intelligence Gained |
|---|---|
| Employee names, roles, reporting structure | Org chart and hierarchy |
| Skills section | Technology stack (if 50 engineers list "Palo Alto Networks" → they use Palo Alto) |
| Recent activity | Projects in progress |
| Job postings | Security gaps ("Looking for Splunk admin" → they USE Splunk) |
| Former employees | May have posted about internal tech they worked on |

#### GitHub / GitLab / Bitbucket

| What to Look For | Intelligence Gained |
|---|---|
| Code with credentials | API keys, database passwords, private keys |
| Repository names | Internal project names and technologies |
| Commit messages | Security incidents ("fix XSS bug", "remove hardcoded password") |
| Fork history | What external code they depend on |
| Developer usernames | Can be linked to personal accounts |

#### Twitter/X, Facebook, Instagram

| What to Look For | Intelligence Gained |
|---|---|
| Office photos | Equipment (server model, badge reader brand), screen contents, security cameras |
| Conference check-ins | Travel schedules |
| Tech conference posts | Technologies employees follow |

#### Glassdoor / Indeed / Naukri

| What to Look For | Intelligence Gained |
|---|---|
| Employee reviews | Internal tools, processes, frustrations |
| Job postings | Entire technology stack |
| Security team postings | Security tools and team composition |

#### Pastebin / Dark Web

| What to Look For | Intelligence Gained |
|---|---|
| Leaked credentials | Passwords from previous breaches |
| Internal documentation | Leaked internal docs |
| Code dumps | Sensitive configuration |

---

#### Real-World Example — The Human Recon Chain

| Step | Source | Intelligence |
|---|---|---|
| 1 | LinkedIn | John Smith is IT Manager at TargetCorp |
| 2 | John's GitHub | He maintains a Cisco ASA config → TargetCorp uses Cisco ASA firewalls |
| 3 | John's Twitter | Tweeted from Black Hat 2024 → he'll be away Aug 3–7 → IT likely understaffed |
| 4 | Glassdoor review | "IT dept uses ServiceNow for tickets" → social engineering pretext available |
| 5 | Job posting | "Senior Exchange Admin" → on-premises Exchange → potentially vulnerable to ProxyLogon |

**None of this required touching a single target system. All of it is legally available public information. All of it builds a devastating intelligence picture.**

---

### 4.3 Active Social Engineering Recon

Direct interaction with target employees to extract intelligence. **Requires authorization.**

| Technique | How It Works | Intelligence Gained |
|---|---|---|
| **Pretexting Calls to Help Desk** | "Hi, this is John from the London office. I'm locked out of my VPN and have a client presentation in 20 minutes. What software are you using for VPN?" | VPN software name and potentially version |
| **Email Confirmation Fishing** | "Please confirm your email address is still active for our directory update." | Which emails are valid (active accounts), confirms email format |
| **Phone Number Harvesting** | "Hi, I'm calling from [Vendor]. I need to speak with someone in your networking team. Could I get their direct number?" | Direct phone numbers of technical staff |
| **Dumpster Diving** | Searching discarded materials outside target premises | Old org charts, printed emails, server inventory lists, network diagrams |

> [!NOTE]
> **Books I want to read on this topic:**
> - *"Catch Me If You Can"* — Frank Abagnale (greatest social engineer in history)
> - *"The Art of Deception"* — Kevin Mitnick
>
> These explain the human side of security better than any technical textbook.

---

## Section 5 — Traceroute in Footprinting

### 5.1 What is Traceroute?

A network diagnostic tool that maps the **path** packets take from your machine to a destination host. Shows every intermediate hop (router/device) and measures round-trip time to each.

**Why attackers use it in footprinting — it reveals:**

| Intelligence | How |
|---|---|
| Network topology | Path mapping reveals infrastructure structure |
| Router count & location | Approximate geographic location per hop (IP geolocation) |
| ISP and hosting provider | The hop just before target is often the ISP |
| Firewall positions | Hops that don't respond (***) indicate firewalls |
| Internal IP addressing | Last hops may reveal internal IPs |
| Load balancer presence | Multiple traceroutes show different paths |

---

### 5.2 How Traceroute Works — The Packet Level

> [!IMPORTANT]
> Traceroute exploits the **TTL (Time To Live)** field in IP packets. This is a fundamental I need to understand completely.

**Understanding TTL:**
- Every IP packet has a TTL field — a number (usually 64, 128, 255)
- Every time a router forwards the packet, it **decreases TTL by 1**
- When TTL reaches **ZERO**, the router DROPS the packet and sends an **ICMP "Time Exceeded"** message back to the source
- This is the mechanism traceroute exploits

**Step-by-Step Mechanics:**

| Probe | What Happens | Result |
|---|---|---|
| TTL=1 | Router 1 receives it → TTL becomes 0 → drops it → sends ICMP Time Exceeded back | Record: "Router 1 is at IP X.X.X.X, RTT = 2ms" |
| TTL=2 | Router 1 forwards (TTL→1) → Router 2 receives it → TTL becomes 0 → drops it | Record: "Router 2 is at IP Y.Y.Y.Y, RTT = 15ms" |
| TTL=3 | Survives Router 1 and 2 → dies at Router 3 | Record Router 3's details |
| ... | Continues until destination reached | Destination sends Echo Reply or Port Unreachable |

**Visual:**

```
YOUR PC (TTL=1) → Router1 [TTL=0, ICMP BACK] → YOU RECORD HOP 1
YOUR PC (TTL=2) → Router1 → Router2 [TTL=0, ICMP BACK] → YOU RECORD HOP 2
YOUR PC (TTL=3) → Router1 → Router2 → Router3 → YOU RECORD HOP 3
... continues until TARGET reached
```

**What each probe sends:**
- 3 packets per TTL value (for min/avg/max round-trip timing)
- Missing responses (***) = firewall blocking ICMP at that hop

---

### 5.3 Traceroute Variants

| Tool | OS | Protocol | Notes |
|---|---|---|---|
| `traceroute` | Linux/Mac | UDP (default) or ICMP with `-I` flag | Standard |
| `tracert` | Windows | ICMP Echo Requests | Windows-native |
| `traceroute -T` / `tcptraceroute` | Linux | **TCP SYN packets** | Many firewalls block ICMP/UDP but allow TCP on 80/443. **More useful for real-world footprinting.** |
| `mtr` (My TraceRoute) | Linux | Combines ping + traceroute | Continuous real-time display. Shows packet loss at each hop. More detailed. |

---

### 5.4 What Traceroute Reveals to an Attacker

| Intelligence | How to Extract It |
|---|---|
| **Network Topology** | Run from multiple vantage points (VPN in different countries, online tools like traceroute.org) |
| **ISP / Hosting Provider** | Reverse DNS lookup of the hop just BEFORE target. Also reveals if CDN is used (Cloudflare, Akamai hide real IP). |
| **Geographic Location** | Each hop's IP can be geolocated — reveals WHERE servers physically are |
| **Firewall Positioning** | Hops showing *** = firewall/router blocking ICMP. Hop before = router before firewall. Hop after = behind firewall. |
| **Load Balancer Detection** | Multiple traceroutes to same target show DIFFERENT final hops if load balancer is present |
| **Internal IP Leakage** | Last few hops may reveal RFC 1918 addresses (192.168.x.x, 10.x.x.x, 172.16.x.x) — internal addressing schema |

---

#### Example Traceroute Analysis

```
Hop 1:  192.168.1.1   — Your home router (private — expected)
Hop 2:  10.x.x.x      — Your ISP's local equipment
Hop 3:  203.x.x.x     — ISP's regional router (India)
Hop 4:  202.x.x.x     — ISP's national backbone
Hop 5:  *  *  *        — FIREWALL (blocks ICMP) ← attacker notes this
Hop 6:  172.x.x.x     — Target's DMZ router ← internal IP leaking!
Hop 7:  192.168.10.5   — TARGET SERVER ← internal IP fully visible
```

**My analysis of this output:**

> "There is a firewall between hop 4 and hop 6. The DMZ uses 172.x.x.x addressing. The server is 192.168.10.5 — possible other servers in 192.168.10.x range. ISP at hop 3–4 is [ISP Name] — research their infrastructure next."

---

### 5.5 How Defenders Detect Traceroute

**Detection Methods:**
- ICMP Time Exceeded flood detection in IDS (Snort/Suricata rule)
- Monitoring for sequential TTL-incrementing packets from same source
- Rate limiting ICMP responses at perimeter firewall
- Firewall logging of blocked ICMP at each hop

**Defender Countermeasures:**

| Countermeasure | Effect |
|---|---|
| Configure edge routers to NOT send ICMP Time Exceeded | Traceroute shows *** for all hops through your network |
| Use CDN/reverse proxy (Cloudflare) | Hides real server IPs behind proxy |
| Don't include internal IPs in reverse DNS | Prevents internal IP leakage |
| Block ICMP at perimeter for sensitive systems | Blocks standard traceroute |
| Alert on high-frequency traceroute patterns | Detects active recon |

---

## Section 6 — OSINT Framework

### 6.1 What is OSINT?

**OSINT** = Open Source Intelligence. The collection, analysis, and use of information from **publicly available sources** to answer intelligence questions.

> [!NOTE]
> "Open Source" does NOT mean open source software. It means information that is **publicly accessible** — no hacking, no breaking in, no authorization needed to VIEW it.

**Why OSINT is powerful:**

| Reason | Detail |
|---|---|
| **80–90% of intel** | Comes from OSINT in professional pentests and red team engagements |
| Legal | Accessing public info |
| Undetectable | No packets hit target systems |
| Free/low-cost | Most tools are free |
| Fast | Good tools aggregate from hundreds of sources |
| Reveals human intel | Things technical tools miss |

---

### 6.2 Categories of OSINT Sources

#### Category 1 — Internet/Web Sources

| Source | What It Provides |
|---|---|
| Search Engines | Google, Bing, DuckDuckGo — indexed public web |
| Google Dorking | Advanced operators to find specific vuln info |
| Shodan/Censys | Internet-connected devices and services |
| Archive.org | Historical versions of websites |
| crt.sh | SSL cert history and subdomains |
| DNSdumpster, SecurityTrails | DNS intelligence |
| WHOIS/RDAP | Domain registration and ownership info |
| BGP Looking Glass | Routing and ASN information |

#### Category 2 — Social Media & Professional Networks

| Source | What It Provides |
|---|---|
| LinkedIn | Employees, org structure, tech stack |
| Twitter/X | Real-time employee activity, tech mentions |
| Facebook | Personal info, office photos, events |
| Instagram | Photos (with metadata), office environment |
| GitHub/GitLab | Code, credentials, internal tools |
| Reddit | Technical discussions, internal frustrations |
| Stack Overflow | Questions reveal tech stack and problems |

#### Category 3 — Documents and Metadata

| Source | What It Provides |
|---|---|
| Company website docs | PDFs, Word docs, Excel files with metadata |
| Job postings | Exact tech stack, security tools, processes |
| Annual reports/filings | Business structure, financials, IT spending |
| Patent filings | Technology innovations, internal systems |
| Conference papers | Technical infrastructure details |
| Press releases | New technology adoptions, partnerships |

#### Category 4 — Breach and Credential Intelligence

| Source | What It Provides |
|---|---|
| HaveIBeenPwned | Which email addresses appear in known breaches |
| DeHashed | Leaked credentials database search |
| LeakCheck | Password breach verification |
| IntelX | Leaked documents, dark web intel |
| Pastebin | Publicly pasted (often leaked) data |

#### Category 5 — Physical and Geographic Intelligence

| Source | What It Provides |
|---|---|
| Google Maps/Street View | Office layout, security cameras, entry points |
| Satellite imagery | Data center locations, physical security |
| Flight trackers | Executive travel (company aircraft) |
| Property records | Office/data center ownership |

---

### 6.3 Google Dorking

Google Dorking (Google Hacking) uses advanced search operators to find information that basic searches miss. Often reveals sensitive files, login pages, and vulnerabilities indexed by Google.

**Why:** Organizations accidentally expose configuration files with passwords, database backups, admin login pages, camera interfaces, and sensitive documents — all publicly accessible and indexed by Google.

#### Key Google Operators

| Operator | What It Does | Example |
|---|---|---|
| `site:` | Limits results to specific domain | `site:targetcompany.com` |
| `filetype:` | Finds specific file types | `site:targetcompany.com filetype:pdf` |
| `intitle:` | Finds pages with specific text in title | `intitle:"index of" site:targetcompany.com` |
| `inurl:` | Finds pages with specific text in URL | `inurl:admin site:targetcompany.com` |
| `intext:` | Finds pages with specific text in body | `intext:"password" filetype:txt` |
| `cache:` | Shows Google's cached version of a page | `cache:targetcompany.com/login` |
| `link:` | Finds pages linking to a specific URL | Reveals business relationships |
| `OR` | Searches for either term | `site:targetcompany.com OR site:subsidiary.com` |
| `-` | Excludes a term | `site:targetcompany.com -www` (finds subdomains excluding www) |
| `" "` | Exact phrase match | `"targetcompany.com" "internal use only"` |

#### Power Dork Examples (Authorized Recon Only)

| Purpose | Dork |
|---|---|
| Find directory listings | `intitle:"index of" site:targetcompany.com` |
| Find exposed config files | `filetype:conf OR filetype:config site:targetcompany.com` |
| Find login pages | `inurl:login OR inurl:signin site:targetcompany.com` |
| Find exposed spreadsheets | `site:targetcompany.com filetype:xls OR filetype:csv` |
| Find exposed cameras | `inurl:"view/index.shtml" intitle:"Live View"` |
| Find exposed phpMyAdmin | `inurl:phpmyadmin intitle:"phpMyAdmin"` |
| Find passwords in text files | `filetype:txt intext:password site:targetcompany.com` |

> [!TIP]
> **Google Hacking Database (GHDB)** at [exploit-db.com/google-hacking-database](https://exploit-db.com/google-hacking-database) contains thousands of pre-built dorks organized by category: Sensitive files, login pages, webcams, vulnerable servers, network devices, etc.

---

### 6.4 OSINT Framework Tool

**[osintframework.com](https://osintframework.com)** is a visual map of OSINT tools organized by data type being sought.

**Top-Level Categories:**

| Category | What You Can Find |
|---|---|
| Username | Accounts across platforms |
| Email Address | Validate, breach check, owner lookup |
| Domain Name | WHOIS, DNS, hosting, history |
| IP Address | Geolocation, ASN, reverse DNS, history |
| Images/Video/Audio | Reverse image search, metadata extraction |
| Social Networks | Platform-specific search tools |
| Instant Messaging | Discord, Telegram, WhatsApp intel |
| People Search | Public records, voter registration |
| Phone Numbers | Carrier, owner, spam reports |
| Business Records | Corporate filings, directors |
| Transportation | Flight, vehicle, maritime tracking |
| Geolocation | GPS EXIF data, location intel |
| Dark Web | Tor services, hidden sites |

---

## Section 7 — MITRE ATT&CK TA0043 — Reconnaissance Mapping

**TA0043** is the MITRE ATT&CK Tactic ID for Reconnaissance — covering all techniques adversaries use to gather information before conducting operations.

**Why mapping matters:**
- Align recon methodology to known attacker behavior
- Defenders can write IDS/SIEM rules using these technique IDs
- Pentest reports mapped to industry-standard framework

### Complete Recon Technique Mapping

| Tech ID | Technique | What It Is | Tools |
|---|---|---|---|
| T1595.001 | Active Scanning: IP Blocks | Scanning target's internet infra for live hosts | NMAP, Masscan, Zmap |
| T1595.002 | Active Scanning: Vulnerability Scanning | Finding vulns on open ports | Nessus, OpenVAS, Nikto |
| T1595.003 | Active Scanning: Wordlist Scanning | Crawling web apps using wordlists | Gobuster, FFUF, dirb |
| T1592.001 | Gather Victim Host Info: Hardware | Hardware info from public sources | Shodan, Censys |
| T1592.002 | Gather Victim Host Info: Software | OS and software versions | Shodan, Netcraft, Wappalyzer |
| T1592.003 | Gather Victim Host Info: Firmware | Firmware versions of network devices | Shodan, custom queries |
| T1592.004 | Gather Victim Host Info: Client Configs | Configuration details from public sources | — |
| T1589.002 | Gather Victim Identity: Email Addresses | Employee email addresses | theHarvester, Hunter.io |
| T1589.001 | Gather Victim Identity: Credentials | Employee creds in paste/breach sites | HaveIBeenPwned, DeHashed |
| T1589.003 | Gather Victim Identity: Employee Names | Employee names and roles | LinkedIn, Maltego |
| T1590.001 | Gather Victim Network: IP Addresses | IP ranges owned by target | WHOIS, ARIN, RIPE |
| T1590.002 | Gather Victim Network: DNS | DNS records for target domain | dig, nslookup, dnsdumpster |
| T1590.004 | Gather Victim Network: Topology | Network topology via traceroute | traceroute, mtr, tcptraceroute |
| T1591.004 | Gather Victim Org: Identify Roles | Employee and team details | LinkedIn, Maltego, OSINT |
| T1591.002 | Gather Victim Org: Business Relations | Business relationships, partners, suppliers | Maltego, LinkedIn |
| T1598.003 | Phishing for Info: Spearphishing Link | Sending phishing to gather intel (not for access — for recon) | — |
| T1593.001 | Search Open Source: Social Media | Searching public social media for intel | Maltego, SpiderFoot |
| T1593.003 | Search Open Source: Code Repositories | Searching repos for secrets and infrastructure | GitDorker, GitHub search |
| T1596.005 | Search Technical DBs: Scan DB | Google Dorks for sensitive info | Google Dorks, GHDB |
| T1596.002 | Search Technical DBs: WHOIS | WHOIS databases for domain registration | WHOIS, RDAP |
| T1596.003 | Search Technical DBs: Digital Certificates | Certificate transparency logs for subdomains | crt.sh, Censys |

> [!IMPORTANT]
> Every technique in this table is something that BOTH attackers AND ethical hackers do. The **only difference** is ethical hackers have **written authorization**. The techniques are identical.

---

## Section 8 — 2026 Context: The Evolution of Reconnaissance

### 8.1 AI-Assisted OSINT

AI tools are fundamentally changing how recon is conducted — making it **faster, deeper**, and accessible to attackers with **less skill**.

| Capability | Traditional | AI-Powered | Impact |
|---|---|---|---|
| **OSINT Aggregation** | Manually search 20 different tools, copy-paste, analyze | Single prompt generates comprehensive intel report across all sources | Massive time savings |
| **Spear Phishing Generation** | Writing convincing emails requires skill | Feed LLM recon data → hyper-personalized phishing referencing boss's name, recent project, tech stack | 3x higher click rates (2024 research) |
| **Voice Cloning (Vishing)** | Limited to impersonation skills | 30-second audio clip from YouTube → AI clones the voice | UK energy company lost $243,000 (2024) |
| **Code Repository Mining** | Manual pattern matching for secrets | AI understands context, not just patterns | TruffleHog, GitLeaks AI-enhanced |
| **Deepfake Video** | Not feasible | Real-time deepfake on video calls | Hong Kong company transferred **$25.6 million** after a deepfake CFO video call (2024) |

**Example Tools (2025–2026):**
SpiderFoot with LLM integration · Maltego AI-enhanced transforms · ChatGPT/Claude for analysis · Perplexity.ai for real-time research synthesis

---

### 8.2 Data Brokers

Companies that **legally** collect, aggregate, and sell personal information about individuals. Sources: public records, purchase histories, social media, apps.

**Why it matters for recon:** An attacker can purchase a comprehensive profile of an employee for **$1–5 USD** including:

| Data Point | Details |
|---|---|
| Personal | Full name, age, addresses (current + historical), phone numbers, email addresses |
| Family | Family members' names |
| Professional | Employment history |
| Digital | Social media accounts |
| Behavioral | Purchase behavior, political/religious affiliation |
| Assets | Vehicle information |

**Major Data Brokers:** Spokeo, Whitepages, BeenVerified, Intelius, ZoomInfo, Clearbit, LexisNexis

> [!NOTE]
> DPDPA 2023 (India) and GDPR (EU) are starting to restrict data broker operations but enforcement is still maturing. Data brokers remain a significant OSINT source for attackers.

---

### 8.3 Digital Footprint Awareness — Defender Perspective

> [!IMPORTANT]
> "You cannot defend what you cannot see." Organizations should conduct their OWN OSINT against themselves. This is called **Attack Surface Management (ASM)**.

**Steps for defenders:**

1. Run all recon tools against your own organization
2. Document what you find
3. Reduce exposure where possible:
   - Remove sensitive files from public web servers
   - Enforce strict GitHub commit policies (no secrets in code)
   - Train employees on social media OPSEC
   - Remove old job postings revealing obsolete tech
   - Request removal from data brokers
   - Monitor certificate transparency logs for your own domains
4. Set up Google Alerts for: company name + "breach", "hacked", "leak", "password"
5. Monitor HaveIBeenPwned for your email domain

**Tools for Continuous ASM (2026):**

| Tool | What It Does |
|---|---|
| Shodan Monitor | Alerts when your IPs appear in Shodan |
| SpiderFoot HX | Automated OSINT against your own org |
| Censys ASM | Enterprise attack surface management |
| Microsoft Defender EASM | External Attack Surface Management |

---

### ✅ Session 10A — Key Takeaways

- [x] A Security Evaluation Plan is a **legal document** — never test without one
- [x] The "get out of jail" letter is a separate portable authorization document
- [x] Black Box = no knowledge, White Box = full knowledge, Grey Box = partial
- [x] Grey Box is most realistic for modern threat simulation
- [x] Footprinting is NOT optional — 30–40% of professional engagements are recon
- [x] Passive recon = no packets touch target — target cannot detect it
- [x] Active recon = packets reach target — requires written authorization
- [x] Footprinting gathers 7 categories: Network, System, Org, People, Web, Security Posture, Physical
- [x] Social engineering in recon phase = intelligence gathering, not attack
- [x] LinkedIn alone reveals technology stack, org structure, and project intel
- [x] Traceroute exploits TTL to map hops, reveal topology, locate firewalls, and expose internal IPs
- [x] TCP traceroute bypasses firewalls that block ICMP-based traceroute
- [x] Google Dorking uses advanced operators to find accidentally exposed info
- [x] OSINT Framework at osintframework.com maps all tools by data type
- [x] MITRE ATT&CK TA0043 maps every recon technique to known adversary behavior
- [x] AI is transforming recon — faster aggregation, voice cloning, deepfakes
- [x] Data brokers are a significant passive intelligence source for attackers
- [x] Organizations MUST perform OSINT against themselves (attack surface management)

---

<details>
<summary>📖 Session 10A — Glossary</summary>

| Term | Definition |
|---|---|
| Security Evaluation Plan | Formal document authorizing and defining scope of pentest engagement |
| Rules of Engagement (RoE) | Specific rules governing what is permitted during testing |
| Black Box Test | Pentest with zero prior knowledge of target |
| White Box Test | Pentest with complete knowledge of target |
| Grey Box Test | Pentest with partial knowledge of target |
| Footprinting | Systematic information gathering about a target before any technical testing |
| Passive Recon | Gathering info without touching target systems |
| Active Recon | Gathering info by directly interacting with target |
| OSINT | Open Source Intelligence — publicly available info |
| Google Dorking | Advanced Google search operators for recon |
| Shodan | Search engine for internet-connected devices |
| Certificate Transparency | Public log of all SSL/TLS certificates issued |
| crt.sh | Website to search certificate transparency logs |
| TTL (Time To Live) | IP packet field decremented at each router hop |
| ICMP Time Exceeded | Message sent when TTL reaches zero — used by traceroute |
| Traceroute | Tool mapping network path using TTL manipulation |
| TCP Traceroute | Traceroute using TCP SYN packets (bypasses ICMP blocks) |
| TA0043 | MITRE ATT&CK Tactic ID for Reconnaissance |
| Social Engineering Recon | Using human manipulation to gather intelligence |
| Data Broker | Company that collects and sells personal data |
| Digital Footprint | Total publicly accessible information about an org |
| Attack Surface | All possible points where attacker can enter |
| Attack Surface Management | Continuous monitoring of your own attack surface |
| PTES | Penetration Testing Execution Standard |
| OSSTMM | Open Source Security Testing Methodology Manual |
| GHDB | Google Hacking Database — repository of dorks |
| Deepfake | AI-generated media impersonating real persons |
| EXIF Data | Metadata embedded in image files (can reveal GPS) |
| DNS Zone Transfer | Technique to retrieve all DNS records from a server |

</details>

---

**What's next — Session 10B** covers port scanning, TCP three-way handshake, all scan types (SYN, Connect, FIN, NULL, XMAS, IDLE/Zombie), vulnerability scanning with Nessus, and Burp Suite proxy mechanics.

---