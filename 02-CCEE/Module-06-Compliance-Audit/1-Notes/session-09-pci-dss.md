# 💳 Session 09 — PCI DSS

## 📑 Table of Contents
- [What is PCI DSS](#what-is-pci-dss)
- [PCI DSS Overview](#pci-dss-overview)
- [History of PCI DSS](#history)
- [PCI SSC — The Governing Body](#pci-ssc)
- [Who Must Comply](#who-must-comply)
- [PCI DSS Levels](#pci-dss-levels)
  - [Merchant Levels](#merchant-levels)
  - [Service Provider Levels](#service-provider-levels)
- [PCI DSS 12 Requirements](#12-requirements)
  - [6 Goals and 12 Requirements](#6-goals)
- [PCI DSS Compliance Validation](#compliance-validation)
  - [SAQ — Self Assessment Questionnaire](#saq)
  - [ROC — Report on Compliance](#roc)
  - [AOC — Attestation of Compliance](#aoc)
- [Cardholder Data](#cardholder-data)
- [Cardholder Data Environment (CDE)](#cde)
- [📌 Extra Notes](#extra-notes)
  - [PCI DSS Version History](#version-history)
  - [PCI DSS v4.0 — Key Changes](#v4)
  - [Scoping and Network Segmentation](#scoping)
  - [QSA and ISA](#qsa-isa)
  - [PCI DSS vs HIPAA vs GDPR](#comparison)
  - [Card Brand Programs](#card-brands)
  - [Compensating Controls](#compensating-controls)
  - [Common PCI DSS Violations](#violations)
  - [PAN — Primary Account Number](#pan)
  - [SAD — Sensitive Authentication Data](#sad)
- [Abbreviations](#abbreviations)
- [Keywords & Concept Map](#keywords)
- [Quick Reference Cheatsheet](#cheatsheet)
- [Session Revision Snapshot](#snapshot)

---

## 🔰 What is PCI DSS <a name="what-is-pci-dss"></a>

- **PCI DSS = Payment Card Industry Data Security Standard**
- A **set of security standards** designed to ensure all companies
  that accept, process, store, or transmit **credit card information**
  maintain a secure environment
- Developed and maintained by the **PCI Security Standards Council
  (PCI SSC)**
- NOT a law — a **contractual requirement** enforced through payment
  card brand agreements
- Applies to **any organization** that handles cardholder data —
  regardless of size, location, or industry
- Non-compliance can result in **fines, increased transaction fees,
  or loss of ability to process card payments**

> [!IMPORTANT]
> PCI DSS is NOT a government law like HIPAA or GDPR — it is a
> **private industry standard** enforced contractually through
> agreements with payment card brands (Visa, Mastercard, etc.).
> However, non-compliance consequences are very real — organizations
> can lose the ability to accept card payments entirely.

---

## 🏢 PCI DSS Overview <a name="pci-dss-overview"></a>

### Key Facts

| Attribute | Detail |
|---|---|
| **Full Name** | Payment Card Industry Data Security Standard |
| **Governed By** | PCI Security Standards Council (PCI SSC) |
| **Founded** | PCI SSC founded **September 7, 2006** |
| **Founding Members** | Visa, Mastercard, American Express, Discover, JCB |
| **Type** | Private industry standard — contractual, NOT law |
| **Applies To** | Any entity that stores, processes, or transmits cardholder data |
| **Current Version** | PCI DSS v4.0 (March 2022) |
| **Previous Version** | PCI DSS v3.2.1 (May 2018) — retired March 2024 |
| **Requirements** | 12 requirements organized under 6 goals |
| **Enforcement** | Through payment card brand agreements |

### Why PCI DSS Was Created
- Massive growth in credit card fraud and data breaches in the late
  1990s and early 2000s
- Each card brand had its own security program — no standardization
- Merchants and service providers faced multiple, conflicting security
  requirements
- Need for a **unified, industry-wide standard** to protect cardholder
  data
- Protect consumers, merchants, and financial institutions from card
  fraud losses

---

## 📜 History of PCI DSS <a name="history"></a>

```
Late 1990s → Individual card brand security programs emerge:
              Visa → Cardholder Information Security Program (CISP)
              Mastercard → Site Data Protection (SDP)
              American Express → Data Security Operating Policy (DSOP)
              Discover → Information Security and Compliance (DISC)
              JCB → Data Security Program

2000 → Visa launches CISP — first major card brand security program

2001 → Visa publishes first version of CISP requirements

2004 → PCI DSS 1.0 published
        First unified standard — collaboration between Visa and
        Mastercard
        Combined CISP and SDP into one standard

2006 → PCI Security Standards Council (PCI SSC) founded
        September 7, 2006
        Founded by Visa, Mastercard, American Express, Discover, JCB
        PCI DSS 1.1 released

2008 → PCI DSS 1.2 released
        Clarifications and enhancements

2010 → PCI DSS 2.0 released
        Clarifications — no major structural changes

2013 → PCI DSS 3.0 released
        Enhanced guidance on penetration testing,
        risk assessments, and third-party management

2015 → PCI DSS 3.1 released
        SSL and early TLS removed — security vulnerabilities

2016 → PCI DSS 3.2 released
        Multi-factor authentication requirements expanded
        New requirements for service providers

2018 → PCI DSS 3.2.1 released
        Minor updates — clarifications only

2022 → PCI DSS v4.0 released (March 2022)
        Major revision — most significant update since v3.0
        Customized approach introduced
        March 2024 — v3.2.1 retired, v4.0 mandatory
```

> [!TIP]
> **Key version history for MCQs:**
> - **PCI DSS 1.0 (2004)** = First unified standard
> - **PCI SSC founded 2006** = The governing body
> - **PCI DSS 3.2.1 (2018)** = Previous version
> - **PCI DSS v4.0 (2022)** = Current version

---

## 🏛️ PCI SSC — The Governing Body <a name="pci-ssc"></a>

- **PCI SSC = PCI Security Standards Council**
- Founded: **September 7, 2006**
- Headquarters: **Wakefield, Massachusetts, USA**
- A **global open body** — open to participation from merchants,
  banks, processors, and technology vendors
- Responsible for:
  - Developing and maintaining PCI DSS
  - Managing training and qualification programs for assessors
  - Publishing supporting documents and guidance
  - Operating the QSA and PA-QSA programs

### PCI SSC Founding Members

| Card Brand | Origin |
|---|---|
| **Visa** | USA |
| **Mastercard** | USA |
| **American Express** | USA |
| **Discover** | USA |
| **JCB (Japan Credit Bureau)** | Japan |

> [!NOTE]
> The **5 founding members** of PCI SSC are Visa, Mastercard,
> American Express, Discover, and JCB. These same 5 card brands
> are also the ones that **enforce PCI DSS compliance** through
> their individual merchant and acquirer agreements. PCI SSC sets
> the standard but does NOT enforce it directly.

---

## 🎯 Who Must Comply <a name="who-must-comply"></a>

**Any entity that stores, processes, or transmits cardholder data:**

| Entity Type | Examples |
|---|---|
| **Merchants** | Retailers, e-commerce sites, restaurants, hotels |
| **Service Providers** | Payment processors, hosting providers, managed security providers |
| **Financial Institutions** | Banks, credit unions that issue cards |
| **Acquirers** | Banks that process card transactions for merchants |
| **Payment Processors** | Companies processing card transactions |

> [!WARNING]
> Even if an organization **outsources** all payment processing —
> if they access cardholder data for even one transaction, they
> are in scope for PCI DSS. Outsourcing reduces scope but does NOT
> eliminate compliance responsibility.

---

## 📊 PCI DSS Levels <a name="pci-dss-levels"></a>

PCI DSS compliance requirements vary by **transaction volume** —
higher volume = stricter requirements:

### 🏪 Merchant Levels <a name="merchant-levels"></a>

| Level | Transaction Volume | Validation Requirement |
|---|---|---|
| **Level 1** | More than **6 million** Visa/Mastercard transactions per year | Annual **ROC** by QSA + quarterly network scans by ASV |
| **Level 2** | **1 million to 6 million** transactions per year | Annual **SAQ** + quarterly network scans by ASV |
| **Level 3** | **20,000 to 1 million** e-commerce transactions per year | Annual SAQ + quarterly network scans by ASV |
| **Level 4** | Fewer than **20,000** e-commerce transactions OR up to 1 million other transactions | Annual SAQ + quarterly network scans recommended |

> [!IMPORTANT]
> **Level 1 merchants** face the most stringent requirements —
> they must have an annual **on-site audit** conducted by a
> **QSA (Qualified Security Assessor)**. All other levels can
> use the **SAQ (Self-Assessment Questionnaire)**. Level 1 is
> the highest risk category.

---

### 🏢 Service Provider Levels <a name="service-provider-levels"></a>

| Level | Transaction Volume | Validation Requirement |
|---|---|---|
| **Level 1** | More than **300,000** transactions per year | Annual ROC by QSA + quarterly network scans |
| **Level 2** | Fewer than **300,000** transactions per year | Annual SAQ + quarterly network scans |

> [!NOTE]
> Service Provider thresholds are **lower** than merchant thresholds —
> 300,000 vs 6 million. This is because service providers handle
> data for multiple merchants, making their risk profile higher
> even at lower transaction volumes.

---

## 📋 PCI DSS 12 Requirements <a name="12-requirements"></a>

### 🎯 6 Goals and 12 Requirements <a name="6-goals"></a>

PCI DSS organizes its **12 requirements** under **6 goals**:

| Goal | Requirements | Description |
|---|---|---|
| **Goal 1: Build and Maintain a Secure Network and Systems** | Req 1, 2 | Firewalls and secure configurations |
| **Goal 2: Protect Cardholder Data** | Req 3, 4 | Data storage and transmission protection |
| **Goal 3: Maintain a Vulnerability Management Program** | Req 5, 6 | Anti-malware and secure systems |
| **Goal 4: Implement Strong Access Control Measures** | Req 7, 8, 9 | Access restriction and physical controls |
| **Goal 5: Regularly Monitor and Test Networks** | Req 10, 11 | Logging and security testing |
| **Goal 6: Maintain an Information Security Policy** | Req 12 | Security policy management |

### All 12 Requirements — Detail

| Req | Description |
|---|---|
| **1** | Install and maintain network security controls (firewalls) |
| **2** | Apply secure configurations to all system components |
| **3** | Protect stored account data |
| **4** | Protect cardholder data with strong cryptography during transmission over open networks |
| **5** | Protect all systems and networks from malicious software |
| **6** | Develop and maintain secure systems and software |
| **7** | Restrict access to system components and cardholder data by business need to know |
| **8** | Identify users and authenticate access to system components |
| **9** | Restrict physical access to cardholder data |
| **10** | Log and monitor all access to system components and cardholder data |
| **11** | Test security of systems and networks regularly |
| **12** | Support information security with organizational policies and programs |

> [!TIP]
> **Memory trick for 6 PCI DSS Goals:**
> **"Build Protect Maintain Implement Monitor Maintain"**
> Build network → Protect data → Maintain vuln mgmt →
> Implement access control → Monitor/test → Maintain policy

---

## ✅ PCI DSS Compliance Validation <a name="compliance-validation"></a>

### 📝 SAQ — Self Assessment Questionnaire <a name="saq"></a>

- Used by **Level 2, 3, and 4 merchants** and **Level 2 service
  providers**
- A **self-assessment tool** — the organization assesses its own
  compliance
- Multiple SAQ types (A, A-EP, B, B-IP, C, C-VT, D, P2PE) based
  on how the organization processes cards

| SAQ Type | Applicable To |
|---|---|
| **SAQ A** | Card-not-present merchants — fully outsourced |
| **SAQ A-EP** | E-commerce merchants — partially outsourced |
| **SAQ B** | Merchants using imprint machines or standalone dial-out terminals |
| **SAQ B-IP** | Merchants using standalone IP-connected terminals |
| **SAQ C** | Merchants with payment application systems connected to internet |
| **SAQ C-VT** | Merchants using web-based virtual payment terminals |
| **SAQ D** | All other merchants and service providers |
| **SAQ P2PE** | Merchants using validated P2PE solutions |

---

### 📊 ROC — Report on Compliance <a name="roc"></a>

- **ROC = Report on Compliance**
- Required for **Level 1 merchants** and **Level 1 service providers**
- A detailed **on-site assessment** conducted by a **QSA (Qualified
  Security Assessor)**
- Most comprehensive validation method
- Results in a formal report documenting compliance status for every
  PCI DSS requirement
- Must be completed **annually**

---

### 📄 AOC — Attestation of Compliance <a name="aoc"></a>

- **AOC = Attestation of Compliance**
- A **summary document** signed by the merchant/service provider
  AND the QSA (if applicable)
- Confirms the results of the ROC or SAQ
- Submitted to acquirer banks or card brands as proof of compliance
- Required for ALL compliance validation types — both SAQ and ROC

> [!NOTE]
> Think of it as:
> **ROC** = the detailed audit report (full assessment)
> **SAQ** = the self-assessment questionnaire
> **AOC** = the summary attestation (sign-off document for both)
> Every organization needs an AOC — only Level 1 needs a full ROC.

---

## 💳 Cardholder Data <a name="cardholder-data"></a>

### What is Cardholder Data

| Data Element | Storage Permitted? | Protection Required? |
|---|---|---|
| **PAN (Primary Account Number)** | Yes — if protected | Yes — encrypt, mask, or tokenize |
| **Cardholder Name** | Yes | Only if stored with PAN |
| **Service Code** | Yes | Only if stored with PAN |
| **Expiration Date** | Yes | Only if stored with PAN |

### Sensitive Authentication Data (SAD) — NEVER Store

| SAD Element | Description |
|---|---|
| **Full magnetic stripe data** | Track 1 and Track 2 data |
| **CAV2/CVC2/CVV2/CID** | Card verification codes (3-4 digit security code) |
| **PIN/PIN Block** | Personal Identification Number |

> [!IMPORTANT]
> **SAD (Sensitive Authentication Data) must NEVER be stored after
> authorization** — even if encrypted. This is one of the most
> absolute requirements in PCI DSS. The CVV2/CVC2 security code
> on the back of cards is SAD and cannot be stored under any
> circumstances.

### PAN Display Rules
- When displaying PAN, mask all digits except the **first 6 and
  last 4** digits
- Example: 4111 1111 1111 1111 → 411111**XXXXXX**1111
- Only authorized personnel with legitimate need can see the full PAN

---

## 🖥️ Cardholder Data Environment (CDE) <a name="cde"></a>

- **CDE = Cardholder Data Environment**
- The **people, processes, and technology** that store, process,
  or transmit cardholder data or SAD
- Also includes systems that are connected to or could impact the
  security of the CDE
- **Scope of PCI DSS** = the CDE and connected systems
- Reducing the CDE scope = reducing PCI DSS compliance effort

### CDE Scoping Categories

| Category | Description |
|---|---|
| **In Scope** | Systems that store, process, or transmit cardholder data |
| **Connected** | Systems connected to in-scope systems — also in scope |
| **Out of Scope** | Systems with no connectivity to CDE — can be excluded |
| **Segmented** | Systems isolated from CDE via network segmentation |

> [!TIP]
> **Network segmentation** is the most effective way to **reduce
> PCI DSS scope** — isolating the CDE from other systems through
> firewalls and network controls means fewer systems need to comply.
> This is not required by PCI DSS but is strongly recommended to
> reduce compliance costs.

---

## 📌 Extra Notes <a name="extra-notes"></a>

> [!NOTE]
> Everything in this section goes beyond the core syllabus but is
> directly MCQ-relevant. Cross-referenced from PCI SSC official
> documentation and payment security literature. Zero internet
> needed after reading this.

---

### 📜 PCI DSS Version History <a name="version-history"></a>

| Version | Year | Key Change |
|---|---|---|
| **PCI DSS 1.0** | 2004 | First unified standard — Visa + Mastercard |
| **PCI DSS 1.1** | 2006 | Released with PCI SSC founding |
| **PCI DSS 1.2** | 2008 | Clarifications and enhancements |
| **PCI DSS 2.0** | 2010 | Clarifications — no major structural changes |
| **PCI DSS 3.0** | 2013 | Enhanced pen testing, risk, third-party |
| **PCI DSS 3.1** | 2015 | SSL/early TLS removed as secure protocols |
| **PCI DSS 3.2** | 2016 | MFA expanded, new service provider requirements |
| **PCI DSS 3.2.1** | 2018 | Minor updates — clarifications |
| **PCI DSS v4.0** | 2022 | Major revision — customized approach introduced |

---

### 🆕 PCI DSS v4.0 — Key Changes <a name="v4"></a>

PCI DSS v4.0 (March 2022) introduced significant changes:

| Change | Detail |
|---|---|
| **Customized Approach** | NEW — organizations can achieve requirement objectives using their own controls if they demonstrate equivalent security |
| **Defined Approach** | Traditional method — implement specific controls as defined |
| **MFA expanded** | Multi-factor authentication now required for ALL access to the CDE — not just remote access |
| **Password requirements updated** | Minimum 12 characters (up from 7), or MFA as alternative |
| **Targeted risk analysis** | Some requirements now support organization-specific frequency based on risk |
| **E-commerce security** | New requirements for scripts on payment pages |
| **Encryption** | Disk-level encryption no longer sufficient for protecting stored PAN |
| **Roles and responsibilities** | Each requirement now has explicit roles and responsibilities |

> [!IMPORTANT]
> **Customized Approach** is the most significant new concept in
> v4.0. It allows mature organizations with advanced security
> programs to use alternative controls to meet the intent of
> PCI DSS requirements — rather than following the prescriptive
> defined controls. This requires a QSA to validate the custom
> controls and much greater documentation.

---

### 🔍 Scoping and Network Segmentation <a name="scoping"></a>

- **Scoping** = determining which systems, people, and processes
  are in the PCI DSS scope
- Correct scoping is critical — too broad = more compliance work,
  too narrow = compliance gaps

#### Network Segmentation Benefits

| Benefit | Detail |
|---|---|
| **Reduces scope** | Systems isolated from CDE are out of scope |
| **Reduces cost** | Fewer systems to assess and secure |
| **Reduces risk** | Limits blast radius of a breach |
| **Reduces complexity** | Simpler compliance program |

#### Segmentation Methods
- **Firewalls** — most common segmentation method
- **VLANs (Virtual LANs)** — can provide segmentation if properly
  configured
- **Air gaps** — physical separation
- **Tokenization** — replaces PAN with non-sensitive token — removes
  data from scope

> [!WARNING]
> **VLANs alone are NOT always sufficient** for PCI DSS scope
> reduction — they must be properly configured and tested. Poorly
> configured VLANs that allow traffic between segments do NOT
> provide effective scope reduction.

---

### 🔍 QSA and ISA <a name="qsa-isa"></a>

| Role | Full Name | Who They Are | What They Do |
|---|---|---|---|
| **QSA** | Qualified Security Assessor | External assessor from PCI SSC-certified company | Conducts Level 1 ROC assessments — independent third party |
| **ISA** | Internal Security Assessor | Employee of the assessed organization — PCI SSC certified | Conducts internal assessments — not eligible for Level 1 ROC |
| **ASV** | Approved Scanning Vendor | PCI SSC-approved vendor | Conducts required quarterly external vulnerability scans |

> [!NOTE]
> **QSA vs ISA distinction:**
> - **QSA** = external — required for Level 1 ROC
> - **ISA** = internal — can do SAQ assessments but NOT Level 1 ROC
> - **ASV** = separate role — only for external network scanning
> All three are certified/approved by PCI SSC.

---

### ⚖️ PCI DSS vs HIPAA vs GDPR <a name="comparison"></a>

| Feature | PCI DSS | HIPAA | GDPR |
|---|---|---|---|
| **Type** | Private industry standard | US federal law | EU regulation |
| **Data Protected** | Cardholder data (PAN, etc.) | Protected Health Information (PHI) | All personal data |
| **Enforced By** | Card brands (Visa, Mastercard) | OCR/HHS | National DPAs |
| **Mandatory** | Contractual — not law | Yes — law | Yes — regulation |
| **Applies To** | Any org handling card data | Covered entities + BAs | Any org processing EU data |
| **Certification** | Compliance validation (SAQ/ROC) | No certification | No certification |
| **Breach Notification** | Not prescriptive — notify card brands | 60 days | 72 hours |
| **Max Penalty** | Loss of card processing ability | $1.5M/year | €20M or 4% turnover |
| **Governing Body** | PCI SSC | HHS/OCR | European Commission/DPAs |
| **Current Version** | v4.0 (2022) | Omnibus Rule (2013) | 2016/679 (2018) |

---

### 💳 Card Brand Programs <a name="card-brands"></a>

Each card brand has its own compliance program but all use PCI DSS:

| Card Brand | Compliance Program | Notes |
|---|---|---|
| **Visa** | Visa Cardholder Information Security Program (CISP) | First major card brand program — 2000 |
| **Mastercard** | Site Data Protection (SDP) | Early card brand program |
| **American Express** | Data Security Operating Policy (DSOP) | AXP compliance program |
| **Discover** | Discover Information Security and Compliance (DISC) | Discover compliance program |
| **JCB** | Data Security Program | Japan Credit Bureau program |

> [!NOTE]
> Even though all five brands use PCI DSS, each brand **enforces
> compliance independently** through its agreements with acquiring
> banks. Fines for non-compliance are levied by the card brands —
> not by PCI SSC. PCI SSC sets the standard but does NOT fine
> merchants directly.

---

### 🔄 Compensating Controls <a name="compensating-controls"></a>

- **Compensating controls** in PCI DSS = alternative security
  measures used when an organization cannot meet a specific PCI
  DSS requirement as stated
- Must meet the **intent and rigor** of the original requirement
- Must provide a **similar level of defense** as the original
- Must be **above and beyond** other PCI DSS requirements
- Must document and have approved by a QSA

#### When Compensating Controls Apply
- **Technical constraint** — legacy system cannot support the
  required control
- **Business constraint** — documented business reason prevents
  implementation
- **NOT** acceptable: cost alone is not a sufficient reason

> [!TIP]
> Compensating controls in PCI DSS are similar in concept to
> **Addressable specifications** in HIPAA — both allow alternatives
> when the primary control is not feasible. But PCI DSS compensating
> controls must be approved by a QSA, making them more rigorous.

---

### 🚨 Common PCI DSS Violations <a name="violations"></a>

| Violation | Description |
|---|---|
| **Storing SAD after authorization** | Storing CVV2, full magnetic stripe, or PIN — NEVER permitted |
| **Storing unencrypted PAN** | PAN stored in plaintext — direct violation of Requirement 3 |
| **Weak encryption** | Using outdated protocols (SSL, early TLS) — deprecated in v3.1 |
| **No network segmentation** | CDE not isolated — entire network in scope |
| **Default passwords** | Using vendor default passwords on systems — Requirement 2 |
| **Missing firewall rules** | No firewall between internet and CDE — Requirement 1 |
| **No logging** | Not logging access to cardholder data — Requirement 10 |
| **No penetration testing** | Not conducting required pen tests — Requirement 11 |
| **Inadequate access control** | Users with more access than needed — Requirement 7 |
| **No security awareness training** | Staff not trained on cardholder data security — Requirement 12 |

---

### 💳 PAN — Primary Account Number <a name="pan"></a>

- **PAN = Primary Account Number** — the 16-digit number on a
  payment card
- The most sensitive cardholder data element
- PCI DSS scope is triggered by the **presence of PAN**
- PAN must be:
  - **Encrypted** when stored
  - **Masked** when displayed (show only first 6 and last 4 digits)
  - **Encrypted** when transmitted over open networks
  - **Tokenized** when possible — replaces PAN with a non-sensitive
    token

### PAN Tokenization
- **Tokenization** = replacing PAN with a randomly generated token
- Token has no mathematical relationship to the PAN
- Token can be used for transaction references without exposing PAN
- PAN is stored only in a secure **token vault**
- Tokenization **removes PAN from scope** — significantly reduces
  PCI DSS scope

> [!TIP]
> **Tokenization vs Encryption:**
> - **Encryption** = transforms PAN mathematically — still in scope
>   (encrypted PAN is still PAN)
> - **Tokenization** = replaces PAN with a token — can remove from
>   scope (token is not PAN)
> This distinction is MCQ-worthy.

---

### 🔐 SAD — Sensitive Authentication Data <a name="sad"></a>

Full detail on SAD elements:

| SAD Element | Description | Storage |
|---|---|---|
| **Full Track Data** | Complete data from magnetic stripe (Track 1 + Track 2) | ❌ Never — even encrypted |
| **CAV2** | Card Authentication Value 2 (Discover) | ❌ Never |
| **CVC2** | Card Validation Code 2 (Mastercard) | ❌ Never |
| **CVV2** | Card Verification Value 2 (Visa) | ❌ Never |
| **CID** | Card Identification Number (Amex) | ❌ Never |
| **PIN** | Personal Identification Number | ❌ Never |
| **PIN Block** | Encrypted form of PIN | ❌ Never |

> [!IMPORTANT]
> SAD **cannot be stored after authorization — EVER** — even in
> encrypted form. This is absolute in PCI DSS. The card verification
> codes (CVV2/CVC2/CAV2/CID) are specifically designed to prove
> the physical card is present — storing them defeats their entire
> security purpose.

---

## 🔤 Abbreviations <a name="abbreviations"></a>

| Abbreviation | Full Form | One-line Meaning |
|---|---|---|
| **PCI DSS** | Payment Card Industry Data Security Standard | Industry standard for protecting cardholder data |
| **PCI SSC** | Payment Card Industry Security Standards Council | Governing body that develops and maintains PCI DSS |
| **PAN** | Primary Account Number | The 16-digit payment card number — most sensitive cardholder data |
| **SAD** | Sensitive Authentication Data | Card data that CANNOT be stored after authorization — CVV, PIN, track data |
| **CDE** | Cardholder Data Environment | Systems and people that store, process, or transmit cardholder data |
| **QSA** | Qualified Security Assessor | PCI SSC-certified external assessor — conducts Level 1 ROC |
| **ISA** | Internal Security Assessor | Employee certified by PCI SSC — conducts internal assessments |
| **ASV** | Approved Scanning Vendor | PCI SSC-approved company for required quarterly external scans |
| **ROC** | Report on Compliance | Full audit report required for Level 1 merchants/service providers |
| **SAQ** | Self-Assessment Questionnaire | Self-evaluation tool for Level 2-4 merchants |
| **AOC** | Attestation of Compliance | Summary sign-off document confirming SAQ or ROC results |
| **CVV2** | Card Verification Value 2 | 3-digit Visa security code — SAD — cannot be stored |
| **CVC2** | Card Validation Code 2 | 3-digit Mastercard security code — SAD |
| **CID** | Card Identification Number | 4-digit Amex security code — SAD |
| **P2PE** | Point-to-Point Encryption | Encrypts cardholder data from point of interaction to secure endpoint |
| **CISP** | Cardholder Information Security Program | Visa's original card security program — predecessor to PCI DSS |
| **SDP** | Site Data Protection | Mastercard's original security program |
| **JCB** | Japan Credit Bureau | Japanese card brand — one of 5 PCI SSC founders |

---

## 🗝️ Keywords & Concept Map <a name="keywords"></a>

**PCI DSS**
→ Private industry standard — NOT a law — contractual requirement
→ Governed by PCI SSC (founded 2006) — 5 founding card brands
→ 12 requirements under 6 goals
→ Current version: v4.0 (2022) — introduced Customized Approach
→ Enforced by card brands — not PCI SSC directly

**PCI DSS Levels**
→ 4 merchant levels based on transaction volume
→ Level 1 (6M+ transactions) = strictest — requires ROC by QSA
→ Level 4 (<20K e-commerce) = least strict — SAQ recommended
→ Service providers: Level 1 (300K+), Level 2 (<300K)

**Cardholder Data**
→ PAN, cardholder name, service code, expiration date
→ PAN = most sensitive — triggers PCI DSS scope
→ Must be encrypted at rest and in transit
→ Display: show only first 6 + last 4 digits

**SAD (Sensitive Authentication Data)**
→ Track data, CVV2/CVC2/CID, PIN/PIN Block
→ NEVER store after authorization — even encrypted
→ This is absolute — no exceptions

**CDE (Cardholder Data Environment)**
→ Scope of PCI DSS — systems handling cardholder data
→ Network segmentation reduces CDE scope
→ Connected systems are also in scope

**12 Requirements**
→ Organized under 6 goals
→ Req 1-2: Build secure network
→ Req 3-4: Protect cardholder data
→ Req 5-6: Vulnerability management
→ Req 7-8-9: Access control
→ Req 10-11: Monitor and test
→ Req 12: Security policy

---

## ⚡ Quick Reference Cheatsheet <a name="cheatsheet"></a>

### PCI DSS 6 Goals + 12 Requirements

| Goal | Requirements | Focus |
|---|---|---|
| Build Secure Network | 1, 2 | Firewalls, secure configs |
| Protect Cardholder Data | 3, 4 | Storage, transmission encryption |
| Vulnerability Management | 5, 6 | Anti-malware, secure software |
| Strong Access Control | 7, 8, 9 | Need-to-know, authentication, physical |
| Monitor and Test | 10, 11 | Logging, pen testing, scanning |
| Security Policy | 12 | Policies and programs |

### Merchant Levels

| Level | Transactions | Validation |
|---|---|---|
| **1** | 6M+ per year | ROC by QSA + ASV scans |
| **2** | 1M–6M per year | SAQ + ASV scans |
| **3** | 20K–1M e-commerce | SAQ + ASV scans |
| **4** | <20K e-commerce or <1M other | SAQ + scans recommended |

### Service Provider Levels

| Level | Transactions | Validation |
|---|---|---|
| **1** | 300K+ per year | ROC by QSA + ASV scans |
| **2** | <300K per year | SAQ + ASV scans |

### Cardholder Data — Storage Rules

| Data | Store? | Protection |
|---|---|---|
| PAN | ✅ Yes | Encrypt/mask/tokenize |
| Cardholder Name | ✅ Yes | If with PAN |
| Expiration Date | ✅ Yes | If with PAN |
| Service Code | ✅ Yes | If with PAN |
| Full Track Data | ❌ Never | — |
| CVV2/CVC2/CID | ❌ Never | — |
| PIN/PIN Block | ❌ Never | — |

### PAN Display Rule

```
Full PAN:  4111 1111 1111 1111
Displayed: 411111XXXXXX1111
           (First 6 + Last 4 visible)
```

### Compliance Validation Methods

| Method | Who Uses It | Conducted By |
|---|---|---|
| **ROC** | Level 1 merchants + SP Level 1 | External QSA |
| **SAQ** | Level 2, 3, 4 merchants + SP Level 2 | Organization itself |
| **AOC** | ALL organizations | Merchant/SP (+ QSA if ROC) |
| **ASV Scan** | All levels (quarterly) | Approved Scanning Vendor |

### PCI SSC 5 Founding Members

| Card Brand | Origin |
|---|---|
| Visa | USA |
| Mastercard | USA |
| American Express | USA |
| Discover | USA |
| JCB | Japan |

### PCI DSS vs HIPAA vs GDPR

| | PCI DSS | HIPAA | GDPR |
|---|---|---|---|
| Type | Industry standard | US law | EU regulation |
| Data | Card data | Health data (PHI) | All personal data |
| Breach notification | Not prescriptive | 60 days | 72 hours |
| Max penalty | Card processing loss | $1.5M/year | €20M/4% |

### QSA vs ISA vs ASV

| Role | External/Internal | Does What |
|---|---|---|
| QSA | External | Level 1 ROC audit |
| ISA | Internal | SAQ assessments |
| ASV | External | Quarterly network scans |

---

## 🔁 Session Revision Snapshot <a name="snapshot"></a>

### TL;DR — 5 Bullets
- ✅ PCI DSS = private industry standard (NOT law) — governed by
  PCI SSC (founded 2006) — 5 founding card brands — enforced by
  card brands contractually
- ✅ 4 merchant levels based on transaction volume — Level 1 (6M+)
  = strictest — requires ROC by QSA — Levels 2–4 use SAQ
- ✅ 12 requirements under 6 goals — organized from building secure
  network → protecting data → vulnerability mgmt → access control
  → monitoring → security policy
- ✅ SAD (CVV2, track data, PIN) = **NEVER store after authorization**
  — even encrypted — this is absolute — PAN can be stored but must
  be encrypted
- ✅ PCI DSS v4.0 (2022) introduced **Customized Approach** —
  organizations can use alternative controls if they demonstrate
  equivalent security — validated by QSA

### 🎯 Top MCQ-Likely Concepts from This Session
1. **PCI DSS = industry standard NOT law** — enforced contractually
2. **PCI SSC founded 2006** — 5 founding members
3. **4 merchant levels** — Level 1 (6M+) requires ROC by QSA
4. **12 requirements under 6 goals** — know the groupings
5. **SAD cannot be stored** — CVV2, track data, PIN — ever
6. **PAN display rule** — first 6 + last 4 only
7. **QSA vs ISA vs ASV** — who does what
8. **ROC vs SAQ vs AOC** — which level uses which
9. **CDE = Cardholder Data Environment** — scope of PCI DSS
10. **Network segmentation reduces PCI DSS scope**
11. **Customized Approach** — new in v4.0
12. **Tokenization removes PAN from scope** — encryption does not

---