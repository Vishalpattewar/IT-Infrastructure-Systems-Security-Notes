# 📊 Session 06 — SOX & SOC Reports

## 📑 Table of Contents
- [What is SOX](#what-is-sox)
- [SOX Overview](#sox-overview)
- [SOX Key Sections](#sox-key-sections)
- [SOX Compliance and Security Controls](#sox-compliance)
  - [IT General Controls (ITGCs)](#itgcs)
  - [IT Application Controls (ITACs)](#itacs)
  - [SOX Control Frameworks](#sox-frameworks)
- [What is SOC](#what-is-soc)
- [SOC Reports — Overview](#soc-overview)
- [SOC 1 Reports](#soc1)
- [SOC 2 Reports](#soc2)
  - [SOC 2 Trust Services Criteria](#tsc)
- [SOC 3 Reports](#soc3)
- [SOC Report Types — Type I vs Type II](#type1-vs-type2)
- [SOC Auditor Process Overview](#auditor-process)
- [📌 Extra Notes](#extra-notes)
  - [SOX vs SOC — Key Distinction](#sox-vs-soc)
  - [SOC 2+ and SOC for Cybersecurity](#soc2-plus)
  - [SSAE 18 — The Auditing Standard](#ssae18)
  - [PCAOB — Who Oversees SOX Audits](#pcaob)
  - [SOX Section 404 — Deep Dive](#section-404)
  - [Five Trust Services Criteria — Detail](#tsc-detail)
  - [SOX vs ISO 27001 vs NIST](#sox-vs-others)
  - [Common SOX Violations](#sox-violations)
- [Abbreviations](#abbreviations)
- [Keywords & Concept Map](#keywords)
- [Quick Reference Cheatsheet](#cheatsheet)
- [Session Revision Snapshot](#snapshot)

---

## 🏛️ What is SOX <a name="what-is-sox"></a>

- **SOX = Sarbanes-Oxley Act**
- A **United States federal law** passed in **2002**
- Full name: **Sarbanes-Oxley Act of 2002**
- Named after its sponsors: **Senator Paul Sarbanes** and
  **Representative Michael Oxley**
- Enacted in response to major corporate accounting scandals —
  primarily **Enron** and **WorldCom**
- Administered and enforced by the **SEC (Securities and Exchange
  Commission)**
- Applies to **all publicly traded companies** listed on US stock
  exchanges — including foreign companies listed in the USA
- Purpose: Protect investors by improving the **accuracy and
  reliability of corporate financial disclosures**

> [!IMPORTANT]
> SOX is a **financial regulation** — but it has massive **IT and
> cybersecurity implications** because financial data is stored and
> processed in IT systems. This is why SOX appears in a compliance
> audit syllabus.

---

## 🏢 SOX Overview <a name="sox-overview"></a>

### Key Facts

| Attribute | Detail |
|---|---|
| **Full Name** | Sarbanes-Oxley Act of 2002 |
| **Also Known As** | SOX, Sarbox |
| **Type** | US Federal Law |
| **Signed Into Law** | 30 July 2002 |
| **Triggered By** | Enron, WorldCom, Tyco accounting scandals |
| **Administered By** | SEC (Securities and Exchange Commission) |
| **Applies To** | Publicly traded companies listed on US exchanges |
| **Audit Oversight** | PCAOB (Public Company Accounting Oversight Board) |
| **Key IT Focus** | Sections 302, 404, 409, 802 |
| **Purpose** | Improve accuracy and reliability of financial disclosures |

### Why SOX Was Enacted
- **Enron scandal (2001):** Massive accounting fraud — executives
  hid billions in debt, stock collapsed, employees lost pensions
- **WorldCom scandal (2002):** $11 billion accounting fraud — largest
  in US history at the time
- **Tyco International:** CEO misused company funds
- Investors lost trust in corporate financial reporting
- Congress acted to restore confidence and prevent future fraud

---

## 📋 SOX Key Sections <a name="sox-key-sections"></a>

SOX has **11 titles (sections)** — the key ones for IT and security:

| Section | Title | IT/Security Relevance |
|---|---|---|
| **Section 302** | Corporate Responsibility for Financial Reports | CEOs and CFOs must personally certify accuracy of financial statements — cannot blame IT |
| **Section 401** | Disclosures in Periodic Reports | Financial statements must disclose off-balance-sheet transactions |
| **Section 404** | Management Assessment of Internal Controls | **Most important for IT** — management must assess and report on internal controls over financial reporting |
| **Section 409** | Real-Time Issuer Disclosures | Companies must disclose material changes to financial condition rapidly |
| **Section 802** | Criminal Penalties for Altering Documents | Destroying, altering, or falsifying records = criminal offense — up to 20 years imprisonment |
| **Section 906** | Corporate Responsibility for Financial Reports | Criminal penalties for false certifications — up to $5M fine and 20 years imprisonment |

> [!IMPORTANT]
> **Section 404** is the most critical section for IT auditors and
> cybersecurity professionals. It requires management to assess and
> certify the effectiveness of **Internal Controls over Financial
> Reporting (ICFR)**. This drives all SOX IT compliance work.

> [!TIP]
> **Memory trick for key SOX sections:**
> **"3 Fours Make 9 Eights"**
> 302 → 404 → 409 → 802 → 906
> Or remember: **302 (CEO/CFO sign off), 404 (IT controls assessment),
> 802 (no document destruction)**

---

## 🔐 SOX Compliance and Security Controls <a name="sox-compliance"></a>

SOX requires organizations to maintain effective **internal controls
over financial reporting (ICFR)**. In IT terms, this means:

### 🖥️ IT General Controls (ITGCs) <a name="itgcs"></a>

**ITGCs** are foundational controls that apply across all IT systems
supporting financial reporting:

| ITGC Category | Examples |
|---|---|
| **Access Controls** | Who can access financial systems — least privilege, segregation of duties |
| **Change Management** | Controlled process for system changes — tested and approved before deployment |
| **Computer Operations** | Job scheduling, backup and recovery, incident management |
| **Program Development** | SDLC controls — security built into new financial systems |
| **Data Center / Physical Security** | Physical access to servers hosting financial data |

> [!NOTE]
> ITGCs are the **foundation** — if ITGCs fail, all application-level
> controls built on top of them are unreliable. Auditors test ITGCs
> first because weak ITGCs invalidate everything above them.

---

### ⚙️ IT Application Controls (ITACs) <a name="itacs"></a>

**ITACs** are controls built into specific financial applications:

| ITAC Type | Description | Example |
|---|---|---|
| **Input Controls** | Ensure data entered is valid and complete | Validation rules rejecting negative invoice amounts |
| **Processing Controls** | Ensure transactions are processed accurately | Automated reconciliation of transactions |
| **Output Controls** | Ensure outputs are accurate and reach right recipients | Reports distributed only to authorized users |
| **Interface Controls** | Ensure data transferred between systems is complete and accurate | Reconciliation totals between systems |

---

### 📐 SOX Control Frameworks <a name="sox-frameworks"></a>

Organizations use established frameworks to structure their SOX
compliance:

| Framework | Full Name | Use in SOX |
|---|---|---|
| **COSO** | Committee of Sponsoring Organizations | Primary framework for internal control — most widely used for SOX 404 |
| **COBIT** | Control Objectives for Information Technology | IT governance framework used alongside COSO for IT controls |
| **NIST** | NIST SP 800-53 | Used for security control mapping in SOX compliance |

### COSO Framework Components
COSO defines **5 components** of internal control:

| Component | Description |
|---|---|
| **Control Environment** | Tone at the top — management's commitment to integrity |
| **Risk Assessment** | Identifying and analyzing risks to achieving objectives |
| **Control Activities** | Policies and procedures that ensure directives are carried out |
| **Information & Communication** | Relevant information identified, captured, and communicated |
| **Monitoring Activities** | Ongoing assessment of internal control quality |

> [!TIP]
> **COSO = the internal control bible for SOX.** If an exam asks
> which framework is used for SOX internal control assessment —
> the answer is **COSO**. COBIT is used for IT-specific controls
> within the SOX compliance program.

---

## 📄 What is SOC <a name="what-is-soc"></a>

- **SOC = System and Organization Controls**
  *(previously called Service Organization Controls)*
- A framework for reporting on **controls at a service organization**
- Developed and maintained by the **AICPA (American Institute of
  Certified Public Accountants)**
- SOC reports are produced by **independent CPA auditors**
- Used by service organizations to demonstrate their controls to
  customers and their auditors
- Three types: **SOC 1, SOC 2, SOC 3**

> [!WARNING]
> **SOC ≠ SOX** — these are completely different things.
> - **SOX** = Sarbanes-Oxley Act — a US law about financial reporting
> - **SOC** = System and Organization Controls — audit reports about
>   service organization controls
> This is one of the most common confusion traps in MCQs.

---

## 📊 SOC Reports — Overview <a name="soc-overview"></a>

| Report | Focus | Audience | Public? |
|---|---|---|---|
| **SOC 1** | Controls relevant to user entity's financial reporting | User entities and their auditors | ❌ Restricted |
| **SOC 2** | Security, availability, processing integrity, confidentiality, privacy | Management, regulators, business partners | ❌ Restricted |
| **SOC 3** | Same as SOC 2 but summarized | General public | ✅ Public |

> [!NOTE]
> Think of SOC reports as a **trust certificate** for service
> organizations. A cloud provider, payroll processor, or data center
> uses SOC reports to prove to their customers that their controls
> are effective — without giving everyone direct access to their
> systems for audit.

---

## 📋 SOC 1 Reports <a name="soc1"></a>

- **SOC 1 = Controls over Financial Reporting**
- Formerly called **SAS 70 (Statement on Auditing Standards No. 70)**
  — replaced in 2011
- Now governed by **SSAE 18 (Statement on Standards for Attestation
  Engagements No. 18)**
- Relevant for service organizations whose services **affect their
  clients' financial statements**
- Examples of SOC 1 users: payroll processors, loan servicers,
  trust companies, insurance claims processors

### Who Uses SOC 1
- **User entities** — companies that use the service organization
- **User auditors** — auditors of the user entities who need to
  understand controls at the service organization
- Required when a **service organization processes financial
  transactions** on behalf of clients

---

## 🔒 SOC 2 Reports <a name="soc2"></a>

- **SOC 2 = Controls over Security, Availability, Processing
  Integrity, Confidentiality, and Privacy**
- The most **cybersecurity-relevant** SOC report
- Based on the **AICPA Trust Services Criteria (TSC)**
- Relevant for **technology and cloud service providers**
- Examples: cloud hosting providers, SaaS companies, data centers,
  managed security service providers

### SOC 2 Trust Services Criteria (TSC) <a name="tsc"></a>

SOC 2 is organized around **5 Trust Services Criteria**:

| Criteria | Description | Always Required? |
|---|---|---|
| **Security** | Protection against unauthorized access — logical and physical | ✅ Yes — mandatory |
| **Availability** | System is available for operation as agreed | ❌ Optional |
| **Processing Integrity** | System processing is complete, valid, accurate, timely, authorized | ❌ Optional |
| **Confidentiality** | Information designated as confidential is protected | ❌ Optional |
| **Privacy** | Personal information collected, used, retained, disclosed per privacy notice | ❌ Optional |

> [!IMPORTANT]
> **Security is the ONLY mandatory Trust Services Criteria** in SOC 2.
> All others (Availability, Processing Integrity, Confidentiality,
> Privacy) are optional — included based on the nature of the
> service and customer requirements. This is a very common MCQ trap.

### SOC 2 Common Criteria (CC)
The **Security** criteria in SOC 2 is organized into
**Common Criteria (CC)** categories:

| CC Category | Focus |
|---|---|
| **CC1** | Control Environment |
| **CC2** | Communication and Information |
| **CC3** | Risk Assessment |
| **CC4** | Monitoring of Controls |
| **CC5** | Control Activities |
| **CC6** | Logical and Physical Access |
| **CC7** | System Operations |
| **CC8** | Change Management |
| **CC9** | Risk Mitigation |

---

## 📢 SOC 3 Reports <a name="soc3"></a>

- **SOC 3 = Public-facing summary of SOC 2**
- Contains the **same scope** as SOC 2 but with **less detail**
- Designed for **general public distribution** — can be posted on
  website
- Does NOT include the detailed description of system and controls
  (unlike SOC 2)
- Organizations can display a **SOC 3 seal** on their website to
  demonstrate trustworthiness
- Think of SOC 3 as the **marketing version** of SOC 2

| Feature | SOC 2 | SOC 3 |
|---|---|---|
| **Detail Level** | Full detailed report | Summary only |
| **Audience** | Restricted — customers and regulators | General public |
| **Distribution** | Restricted — NDA often required | Freely distributable |
| **Website use** | ❌ Not typically shared publicly | ✅ Can be posted publicly |
| **Seal** | ❌ No seal | ✅ AICPA SOC 3 seal available |

---

## 📝 SOC Report Types — Type I vs Type II <a name="type1-vs-type2"></a>

Both SOC 1 and SOC 2 come in two types:

| | Type I | Type II |
|---|---|---|
| **What it tests** | Design of controls at a **point in time** | Design AND **operating effectiveness** over a period |
| **Time period** | Single date (snapshot) | Minimum **6 months** (typically 12 months) |
| **Assurance level** | Lower — only checks if controls exist | Higher — checks if controls actually work over time |
| **Cost** | Lower | Higher |
| **Customer preference** | Less preferred | **More preferred** — stronger assurance |
| **Analogy** | Checking if a lock exists | Checking if the lock actually keeps people out over time |

> [!IMPORTANT]
> **Type II provides significantly stronger assurance than Type I.**
> Most enterprise customers and regulators require **SOC 2 Type II**
> — not Type I. Type I only proves controls were designed correctly
> at one moment. Type II proves they actually worked consistently
> over a period of at least 6 months.

---

## 🔍 SOC Auditor Process Overview <a name="auditor-process"></a>

### Who Conducts SOC Audits
- SOC audits are conducted by **independent CPA firms** (Certified
  Public Accountants)
- Must be licensed and registered with AICPA
- The auditing standard is **SSAE 18** (for SOC 1 and SOC 2)

### SOC 2 Audit Process — Step by Step

```
Step 1 → Scoping
         Define which Trust Services Criteria apply
         Define the system and services in scope
         Define the audit period (typically 12 months for Type II)

Step 2 → Readiness Assessment (optional but recommended)
         Pre-audit gap analysis
         Identify control weaknesses before formal audit
         Not part of the official report

Step 3 → Controls Documentation
         Service organization documents all relevant controls
         Prepares system description
         Maps controls to Trust Services Criteria

Step 4 → Fieldwork — Evidence Collection
         Auditor interviews key personnel
         Reviews policies and procedures
         Tests controls (for Type II — tests over the period)
         Reviews system logs, configurations, access lists

Step 5 → Auditor Findings
         Identifies exceptions (controls that failed or weren't
         applied consistently)
         Discusses findings with management

Step 6 → Management Response
         Management responds to exceptions
         Explains any remediation taken

Step 7 → Report Issuance
         Auditor issues SOC report
         Report includes:
         - Independent Service Auditor's Report
         - Management's Description of the System
         - Description of Tests and Results (Type II only)
         - Other information provided by management
```

### Auditor's Opinion Types

| Opinion | Meaning |
|---|---|
| **Unqualified (Clean)** | Controls are suitably designed and operating effectively — best outcome |
| **Qualified** | Controls are generally effective but with specific exceptions noted |
| **Adverse** | Controls are NOT suitably designed or operating effectively |
| **Disclaimer** | Auditor was unable to form an opinion — insufficient evidence |

> [!TIP]
> Most organizations aim for an **Unqualified (Clean) Opinion** on
> their SOC 2 Type II report — it is the gold standard that enterprise
> customers require. An adverse opinion is a serious red flag.

---

## 📌 Extra Notes <a name="extra-notes"></a>

> [!NOTE]
> Everything in this section goes beyond the core syllabus but is
> directly MCQ-relevant. Cross-referenced from AICPA standards,
> PCAOB guidelines, and SOX compliance literature. Zero internet
> needed after reading this.

---

### ⚠️ SOX vs SOC — Key Distinction <a name="sox-vs-soc"></a>

This is the **#1 confusion** in this session — must know cold:

| Feature | SOX | SOC |
|---|---|---|
| **Full Name** | Sarbanes-Oxley Act | System and Organization Controls |
| **Type** | US Federal Law | Audit reporting framework |
| **Created by** | US Congress | AICPA |
| **Enforced by** | SEC + PCAOB | AICPA standards (SSAE 18) |
| **Applies to** | Publicly traded companies | Service organizations |
| **Purpose** | Prevent financial fraud | Demonstrate control effectiveness |
| **Output** | Compliance with law | SOC 1 / SOC 2 / SOC 3 reports |
| **Auditor** | PCAOB-registered auditor | AICPA-licensed CPA firm |
| **Year** | 2002 (law passed) | Ongoing framework |
| **Relation** | SOX may REQUIRE SOC 1 from service providers | SOC 1 used to satisfy SOX requirements |

> [!WARNING]
> SOX and SOC are **not interchangeable** — they serve completely
> different purposes. SOX is a law. SOC is a reporting framework.
> However, they are connected: a company subject to SOX may require
> its service providers (payroll, cloud, etc.) to provide a SOC 1
> report to satisfy Section 404 requirements.

---

### 🔐 SOC 2+ and SOC for Cybersecurity <a name="soc2-plus"></a>

#### SOC 2+
- **SOC 2+** is an enhanced SOC 2 that maps controls to an
  additional framework
- Examples: SOC 2 + HITRUST, SOC 2 + ISO 27001, SOC 2 + NIST CSF
- Allows organizations to demonstrate compliance with multiple
  frameworks in a single report
- Reduces audit fatigue for organizations subject to multiple
  compliance requirements

#### SOC for Cybersecurity
- Introduced by AICPA in **2017**
- A newer report type specifically for **cybersecurity risk
  management programs**
- Not tied to a service organization — any organization can get one
- Based on the **AICPA cybersecurity risk management reporting
  framework**
- Broader than SOC 2 — covers the entire organization's
  cybersecurity program

---

### 📜 SSAE 18 — The Auditing Standard <a name="ssae18"></a>

- **SSAE 18 = Statement on Standards for Attestation Engagements
  No. 18**
- The current AICPA standard governing SOC 1 and SOC 2 audits
- Replaced **SSAE 16** in May 2017 (which had replaced SAS 70)

### History of the Auditing Standard

```
SAS 70 (Statement on Auditing Standards No. 70)
  → Original standard — used from 1992 to 2011
  → Replaced by SSAE 16 in 2011

SSAE 16 (Statement on Standards for Attestation Engagements No. 16)
  → Used from 2011 to 2017
  → Created the SOC 1 framework
  → Replaced by SSAE 18 in 2017

SSAE 18 (Statement on Standards for Attestation Engagements No. 18)
  → Current standard — used from May 2017 onwards
  → Covers both SOC 1 and SOC 2
  → Added requirements for subservice organizations
```

> [!TIP]
> **SAS 70 → SSAE 16 → SSAE 18** is the evolution of the SOC
> auditing standard. MCQs may ask about SAS 70 as the predecessor.
> The current standard is **SSAE 18.**

---

### 🏛️ PCAOB — Who Oversees SOX Audits <a name="pcaob"></a>

- **PCAOB = Public Company Accounting Oversight Board**
- Created by **Section 101 of SOX** in 2002
- Oversees the audits of **publicly traded companies**
- Registers, inspects, and disciplines accounting firms that audit
  public companies
- Sets auditing standards for public company audits
- Reports to the **SEC**

| Organization | Role in SOX |
|---|---|
| **SEC** | Enforces SOX — issues rules and regulations |
| **PCAOB** | Oversees auditors of public companies — created BY SOX |
| **Management** | Responsible for internal controls (Section 404) |
| **External Auditor** | Must be PCAOB-registered — attests to management's assessment |
| **Audit Committee** | Board-level committee overseeing the audit process |

> [!NOTE]
> **PCAOB was created by SOX** — it is a direct product of the law.
> Before SOX, auditors were self-regulated through the AICPA.
> SOX created PCAOB to provide independent oversight of auditors
> of public companies — removing self-regulation.

---

### 🔎 SOX Section 404 — Deep Dive <a name="section-404"></a>

Section 404 is the most impactful section for IT professionals:

#### Two Parts of Section 404

| Part | Requirement | Who |
|---|---|---|
| **404(a)** | Management must assess and report on effectiveness of ICFR | CEO + CFO |
| **404(b)** | External auditor must attest to management's assessment | PCAOB-registered auditor |

#### Internal Controls over Financial Reporting (ICFR)
- **ICFR** = the controls designed to ensure financial reporting is
  accurate and reliable
- Includes both **manual controls** and **IT controls (ITGCs + ITACs)**
- Management uses **COSO framework** to assess ICFR

#### Section 404 Process

```
Step 1 → Identify financial reporting processes and systems
Step 2 → Identify risks to accurate financial reporting
Step 3 → Identify and document controls that address those risks
Step 4 → Test controls for design effectiveness
Step 5 → Test controls for operating effectiveness
Step 6 → Identify and remediate deficiencies
Step 7 → Management issues assessment report
Step 8 → External auditor attests to management's assessment
```

#### Control Deficiency Classifications

| Classification | Definition | Action Required |
|---|---|---|
| **Control Deficiency** | Control does not prevent or detect misstatements | Monitor and improve |
| **Significant Deficiency** | Less severe than material weakness — still important | Report to audit committee |
| **Material Weakness** | Reasonable possibility of material misstatement in financial statements | Must be disclosed publicly — very serious |

> [!IMPORTANT]
> **Material Weakness** is the most serious classification — it must
> be publicly disclosed in the annual report. A material weakness
> can devastate investor confidence and stock price. This is why
> SOX 404 compliance is so heavily invested in by public companies.

---

### 🔑 Five Trust Services Criteria — Detail <a name="tsc-detail"></a>

Full detail on all 5 TSC for SOC 2:

#### 1. Security (Common Criteria — CC)
- Protection of the system against unauthorized access
- Covers: logical access, physical access, encryption, firewalls,
  intrusion detection, vulnerability management
- **ONLY mandatory criteria**
- Maps to: CC1 through CC9

#### 2. Availability
- System available for operation as committed or agreed
- Covers: system monitoring, disaster recovery, business continuity,
  capacity management, incident management
- Relevant for: SaaS, cloud hosting, managed services

#### 3. Processing Integrity
- System processing is complete, valid, accurate, timely, authorized
- Covers: data validation, error handling, transaction monitoring,
  output reconciliation
- Relevant for: payment processors, payroll, financial transaction
  systems

#### 4. Confidentiality
- Information designated as confidential is protected
- Covers: encryption, access controls, data classification,
  retention and disposal of confidential data
- Relevant for: organizations handling trade secrets, NDAs,
  sensitive business information

#### 5. Privacy
- Personal information handled per privacy notice and AICPA privacy
  principles
- Covers: notice, choice, collection, use, retention, disclosure,
  access, disposal of personal data
- Relevant for: organizations handling consumer or employee PII
- Relates to GDPR compliance

> [!NOTE]
> The **Privacy TSC aligns with GDPR principles** — organizations
> using SOC 2 Privacy criteria can demonstrate GDPR-relevant controls.
> Similarly, ISO 27701 (Session 05) also maps to privacy controls.
> These frameworks overlap and complement each other.

---

### ⚖️ SOX vs ISO 27001 vs NIST <a name="sox-vs-others"></a>

| Feature | SOX | ISO 27001 | NIST CSF |
|---|---|---|---|
| **Type** | US Law | International Standard | US Framework |
| **Mandatory** | Yes — public companies | Voluntary | Voluntary (US federal mandatory) |
| **Focus** | Financial reporting integrity | Information security | Cybersecurity risk |
| **Created by** | US Congress | ISO/IEC | NIST |
| **Certification** | Compliance — not certification | ✅ Yes | ❌ No |
| **IT Controls** | ITGCs + ITACs (Section 404) | Annex A controls | IPDRR functions |
| **Framework for IT** | COSO + COBIT | ISO 27001 itself | NIST CSF Core |
| **Auditor** | PCAOB-registered CPA | Accredited Certification Body | No formal audit |
| **Applies to** | Public companies in USA | Any organization globally | Any organization |

---

### 🚨 Common SOX Violations <a name="sox-violations"></a>

| Violation Type | Description |
|---|---|
| **Improper access controls** | Unauthorized users accessing financial systems |
| **Inadequate segregation of duties** | Same person can initiate AND approve financial transactions |
| **Poor change management** | Unauthorized changes to financial systems |
| **Insufficient audit trails** | No logs of who accessed or changed financial data |
| **Weak password controls** | Easy-to-guess passwords on financial systems |
| **Inadequate backup and recovery** | Financial data not properly backed up |
| **Document destruction** | Violates Section 802 — criminal offense |
| **False certifications** | CEO/CFO certifying inaccurate statements — violates Section 302 |

---

## 🔤 Abbreviations <a name="abbreviations"></a>

| Abbreviation | Full Form | One-line Meaning |
|---|---|---|
| **SOX** | Sarbanes-Oxley Act | US federal law (2002) requiring financial controls for public companies |
| **SOC** | System and Organization Controls | AICPA framework for service organization control reports |
| **SEC** | Securities and Exchange Commission | US federal agency enforcing SOX and regulating securities markets |
| **PCAOB** | Public Company Accounting Oversight Board | SOX-created body overseeing auditors of public companies |
| **AICPA** | American Institute of Certified Public Accountants | US accounting body that created the SOC reporting framework |
| **ICFR** | Internal Controls over Financial Reporting | Controls ensuring financial statements are accurate — core of SOX 404 |
| **ITGC** | IT General Controls | Foundational IT controls supporting financial systems integrity |
| **ITAC** | IT Application Controls | Controls built into specific financial applications |
| **COSO** | Committee of Sponsoring Organizations | Framework for internal control — primary SOX 404 framework |
| **TSC** | Trust Services Criteria | The 5 criteria used to evaluate controls in SOC 2 reports |
| **SSAE** | Statement on Standards for Attestation Engagements | AICPA auditing standard governing SOC reports — current version is 18 |
| **SAS 70** | Statement on Auditing Standards No. 70 | Predecessor to SSAE 16/18 — original service organization audit standard |
| **CPA** | Certified Public Accountant | Licensed accountant — required to conduct SOC audits |
| **SDLC** | System Development Life Cycle | Development methodology — SOX requires controls throughout SDLC |
| **BCM** | Business Continuity Management | Planning for operations during disruption — relevant to SOC 2 Availability |

---

## 🗝️ Keywords & Concept Map <a name="keywords"></a>

**SOX (Sarbanes-Oxley Act)**
→ US federal law passed 2002 — response to Enron/WorldCom scandals
→ Applies to publicly traded companies listed on US exchanges
→ Enforced by SEC — audit oversight by PCAOB
→ Key sections: 302 (CEO/CFO sign-off), 404 (IT controls), 802
  (document preservation), 906 (criminal penalties)
→ Uses COSO framework for internal control assessment

**Section 404**
→ Most IT-relevant SOX section
→ Management assesses ICFR effectiveness — uses COSO
→ External auditor (PCAOB-registered) attests to management's
  assessment
→ Covers ITGCs and ITACs
→ Material Weakness = most serious deficiency — public disclosure
  required

**SOC Reports**
→ AICPA framework — three types: SOC 1, SOC 2, SOC 3
→ Conducted by independent CPA firms under SSAE 18
→ SOC 1 = financial reporting controls
→ SOC 2 = security + optional: availability, processing integrity,
  confidentiality, privacy
→ SOC 3 = public summary of SOC 2

**SOC 2**
→ Most cybersecurity-relevant SOC report
→ Based on 5 Trust Services Criteria — Security is ONLY mandatory one
→ Type I = point in time / Type II = over minimum 6-month period
→ Type II provides stronger assurance — preferred by enterprise
  customers
→ Auditor can issue: Unqualified, Qualified, Adverse, or Disclaimer

**COSO**
→ Primary internal control framework for SOX 404 compliance
→ 5 components: Control Environment, Risk Assessment, Control
  Activities, Information & Communication, Monitoring
→ Used by management to assess ICFR

**PCAOB**
→ Created by SOX Section 101
→ Oversees auditors of public companies
→ Reports to SEC
→ Removed self-regulation of auditors — key SOX achievement

---

## ⚡ Quick Reference Cheatsheet <a name="cheatsheet"></a>

### SOX Key Sections

| Section | Topic | Key Point |
|---|---|---|
| **302** | Corporate Responsibility | CEO/CFO personally certify financial accuracy |
| **404** | Internal Controls Assessment | Management assesses ICFR — most IT-relevant |
| **409** | Real-Time Disclosures | Rapid disclosure of material changes |
| **802** | Document Preservation | Destroying records = criminal offense (20 yrs) |
| **906** | Criminal Penalties | False certifications = up to $5M + 20 yrs |

### SOC Report Comparison

| | SOC 1 | SOC 2 | SOC 3 |
|---|---|---|---|
| **Focus** | Financial reporting controls | Security + TSC | Summary of SOC 2 |
| **Audience** | User entities + auditors | Management, regulators | General public |
| **Public?** | ❌ No | ❌ No | ✅ Yes |
| **Standard** | SSAE 18 | SSAE 18 | SSAE 18 |
| **Has Type I/II?** | ✅ Yes | ✅ Yes | ❌ No |

### SOC 2 Type I vs Type II

| | Type I | Type II |
|---|---|---|
| Tests | Design only | Design + Operating effectiveness |
| Time | Point in time | Min 6 months |
| Assurance | Lower | Higher |
| Preferred | Less | More (enterprise standard) |

### 5 Trust Services Criteria

| Criteria | Mandatory? | Focus |
|---|---|---|
| **Security** | ✅ Yes | Protection from unauthorized access |
| **Availability** | ❌ No | System uptime as agreed |
| **Processing Integrity** | ❌ No | Accurate, complete processing |
| **Confidentiality** | ❌ No | Protecting confidential info |
| **Privacy** | ❌ No | Personal data handling |

### SOX Control Types

| Type | Scope | Examples |
|---|---|---|
| **ITGC** | Foundation — all IT systems | Access control, change mgmt, backups |
| **ITAC** | Specific applications | Input validation, reconciliation, output controls |

### COSO 5 Components

| # | Component |
|---|---|
| 1 | Control Environment |
| 2 | Risk Assessment |
| 3 | Control Activities |
| 4 | Information and Communication |
| 5 | Monitoring Activities |

### SOC Auditing Standard Evolution

| Standard | Years Active | Key Change |
|---|---|---|
| **SAS 70** | 1992–2011 | Original service org audit standard |
| **SSAE 16** | 2011–2017 | Created SOC 1 framework |
| **SSAE 18** | 2017–present | Current standard — covers SOC 1 + SOC 2 |

### Material Weakness vs Significant Deficiency

| Classification | Severity | Disclosure |
|---|---|---|
| Control Deficiency | Low | Internal only |
| Significant Deficiency | Medium | Audit committee |
| Material Weakness | High | ⚠️ Public disclosure required |

### SOX vs SOC — One-Line Distinction

| | SOX | SOC |
|---|---|---|
| What | US Law | Audit Report Framework |
| Created by | US Congress | AICPA |
| Applies to | Public companies | Service organizations |
| Output | Legal compliance | SOC 1/2/3 reports |

---

## 🔁 Session Revision Snapshot <a name="snapshot"></a>

### TL;DR — 5 Bullets
- ✅ SOX = Sarbanes-Oxley Act (2002) — US law for public companies —
  response to Enron/WorldCom — enforced by SEC — audit oversight by
  PCAOB
- ✅ SOX Section 404 = most IT-relevant — management assesses ICFR
  using COSO — external auditor attests — covers ITGCs and ITACs
- ✅ SOC = System and Organization Controls (AICPA) — three types:
  SOC 1 (financial), SOC 2 (security/TSC), SOC 3 (public summary)
- ✅ SOC 2 has 5 Trust Services Criteria — **Security is the ONLY
  mandatory one** — Type II (6+ months) is stronger than Type I
- ✅ SOX ≠ SOC — completely different: SOX is a law, SOC is a
  reporting framework — but SOX may require SOC 1 from service
  providers

### 🎯 Top MCQ-Likely Concepts from This Session
1. **SOX ≠ SOC** — completely different things — #1 confusion trap
2. **Section 404** — most IT-relevant SOX section — ICFR, COSO, PCAOB
3. **Security is ONLY mandatory TSC** in SOC 2 — all others optional
4. **SOC 2 Type II > Type I** — tests operating effectiveness over
   minimum 6 months
5. **PCAOB created by SOX** — oversight of public company auditors
6. **SAS 70 → SSAE 16 → SSAE 18** — evolution of SOC auditing standard
7. **Material Weakness** = must be publicly disclosed — most serious
8. **COSO = framework for SOX 404** internal control assessment
9. **SOC 3 is public** — SOC 1 and SOC 2 are restricted
10. **ITGCs are foundation** — if ITGCs fail, everything above them
    is unreliable

---