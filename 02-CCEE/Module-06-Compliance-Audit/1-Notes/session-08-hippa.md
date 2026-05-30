# 🏥 Session 08 — HIPAA

## 📑 Table of Contents
- [What is HIPAA](#what-is-hipaa)
- [HIPAA Overview](#hipaa-overview)
- [HIPAA Titles — All 5](#hipaa-titles)
- [HIPAA Key Regulations](#hipaa-regulations)
- [HIPAA Rules — Complete Coverage](#hipaa-rules)
  - [Privacy Rule](#privacy-rule)
  - [Security Rule](#security-rule)
  - [Breach Notification Rule](#breach-rule)
  - [Enforcement Rule](#enforcement-rule)
  - [Omnibus Rule](#omnibus-rule)
- [Protected Health Information (PHI)](#phi)
- [Covered Entities](#covered-entities)
- [Business Associates](#business-associates)
- [HIPAA Safeguards](#hipaa-safeguards)
- [📌 Extra Notes](#extra-notes)
  - [HITECH Act — Connection to HIPAA](#hitech)
  - [PHI vs ePHI vs PII](#phi-vs-ephi)
  - [18 HIPAA Identifiers](#18-identifiers)
  - [Minimum Necessary Standard](#minimum-necessary)
  - [HIPAA Penalties — Four Tiers](#penalties)
  - [Notice of Privacy Practices (NPP)](#npp)
  - [HIPAA vs GDPR Comparison](#hipaa-vs-gdpr)
  - [Common HIPAA Violations](#violations)
  - [HIPAA Enforcement — OCR](#ocr)
  - [Safe Harbor vs Expert Determination](#safe-harbor)
- [Abbreviations](#abbreviations)
- [Keywords & Concept Map](#keywords)
- [Quick Reference Cheatsheet](#cheatsheet)
- [Session Revision Snapshot](#snapshot)

---

## 🔰 What is HIPAA <a name="what-is-hipaa"></a>

- **HIPAA = Health Insurance Portability and Accountability Act**
- A **United States federal law** enacted on **21 August 1996**
- Signed into law by **President Bill Clinton**
- Administered and enforced by the **US Department of Health and
  Human Services (HHS)**
- Enforcement specifically handled by the **Office for Civil Rights
  (OCR)** within HHS
- Originally designed to:
  1. Ensure health insurance **portability** — workers could maintain
     coverage when changing jobs
  2. Improve **accountability** in healthcare — reduce fraud, waste,
     and abuse
- Has since evolved to become primarily known for its **data privacy
  and security requirements** for health information

> [!NOTE]
> The word "portability" in HIPAA originally referred to health
> insurance portability between jobs — NOT data portability. This
> is a common misconception. The privacy and security provisions
> were added later as the healthcare industry moved to electronic
> records.

---

## 🏢 HIPAA Overview <a name="hipaa-overview"></a>

### Key Facts

| Attribute | Detail |
|---|---|
| **Full Name** | Health Insurance Portability and Accountability Act |
| **Enacted** | 21 August 1996 |
| **Signed By** | President Bill Clinton |
| **Administered By** | US Department of Health and Human Services (HHS) |
| **Enforced By** | Office for Civil Rights (OCR) within HHS |
| **Applies To** | Covered Entities and Business Associates |
| **Primary Focus** | Protection of Protected Health Information (PHI) |
| **Companion Law** | HITECH Act 2009 — strengthened HIPAA |
| **Current Regulation** | Omnibus Rule 2013 — most comprehensive update |
| **Penalty Range** | $100 to $2,000,000 per violation category per year |

### Why HIPAA Was Enacted
- Healthcare industry moving from paper to **electronic records**
  — creating new privacy risks
- **Insurance portability** — workers losing coverage between jobs
- Massive **healthcare fraud** costing billions annually
- Need to **standardize** electronic healthcare transactions
- Protect **sensitive medical information** from unauthorized disclosure
- Patients needed **rights over their own health information**

---

## 📋 HIPAA Titles — All 5 <a name="hipaa-titles"></a>

HIPAA is organized into **5 Titles**:

| Title | Name | Focus |
|---|---|---|
| **Title I** | Health Care Access, Portability, and Renewability | Protects health insurance coverage for workers and families when changing or losing jobs — limits exclusions for pre-existing conditions |
| **Title II** | Preventing Health Care Fraud and Abuse; Administrative Simplification; Medical Liability Reform | **Most relevant to IT/security** — contains the Privacy Rule, Security Rule, and administrative simplification requirements |
| **Title III** | Tax-Related Health Provisions | Tax provisions related to medical care |
| **Title IV** | Application and Enforcement of Group Health Plan Requirements | Further provisions for health plan portability and coverage |
| **Title V** | Revenue Offsets | Provisions related to company-owned life insurance and treatment of expatriates |

> [!IMPORTANT]
> **Title II is the most important for IT and security professionals.**
> It contains the Administrative Simplification provisions that led
> to the Privacy Rule, Security Rule, Breach Notification Rule, and
> Enforcement Rule — the four HIPAA Rules most tested in MCQs.

> [!TIP]
> **Memory trick for HIPAA Titles:**
> **"Health People Tax Apply Revenue"**
> Title I = Health care portability
> Title II = Preventing fraud + **Administrative Simplification**
> Title III = Tax provisions
> Title IV = Apply group health plan requirements
> Title V = Revenue offsets

---

## 📜 HIPAA Key Regulations <a name="hipaa-regulations"></a>

HIPAA's regulations evolved over time under Title II's
Administrative Simplification provisions:

```
1996 → HIPAA enacted
        Title I — insurance portability
        Title II — administrative simplification framework

2000 → Privacy Rule proposed (effective 2003)
        First comprehensive federal protection for health information

2003 → Privacy Rule effective
        Patient rights over PHI established

2005 → Security Rule effective
        Electronic PHI (ePHI) security requirements

2006 → Enforcement Rule effective
        Civil money penalties for HIPAA violations

2009 → HITECH Act enacted
        Strengthened HIPAA — breach notification added
        Increased penalties
        Extended obligations to Business Associates

2013 → Omnibus Rule effective (January 2013)
        Combined Privacy, Security, Breach Notification updates
        Implemented HITECH requirements
        Most comprehensive HIPAA update to date
```

---

## 🔑 HIPAA Rules — Complete Coverage <a name="hipaa-rules"></a>

### 🔒 Privacy Rule <a name="privacy-rule"></a>

- Established **national standards** for the protection of PHI
- Effective: **April 14, 2003**
- Gives patients **rights over their health information**
- Sets limits on the use and disclosure of PHI

#### Key Privacy Rule Requirements

| Requirement | Detail |
|---|---|
| **Use and Disclosure** | PHI can only be used/disclosed for treatment, payment, healthcare operations, or with patient authorization |
| **Patient Rights** | Right to access, amend, and get accounting of disclosures of their PHI |
| **Notice of Privacy Practices (NPP)** | Covered entities must provide written notice of privacy practices |
| **Minimum Necessary** | Only minimum necessary PHI should be used or disclosed |
| **Authorization** | Written patient authorization required for uses beyond TPO |
| **De-identification** | PHI can be de-identified and used freely — 2 methods: Safe Harbor or Expert Determination |

#### Permitted Uses and Disclosures (No Authorization Needed)
- **Treatment** — providing healthcare
- **Payment** — billing and reimbursement
- **Healthcare Operations (TPO)** — quality assessment, training,
  accreditation
- **Public health activities** — disease reporting, FDA oversight
- **Law enforcement** — limited circumstances
- **Judicial proceedings** — court orders
- **Decedent information** — coroners, funeral directors

> [!NOTE]
> **TPO = Treatment, Payment, Operations** — the three permitted
> uses that do NOT require patient authorization. Any use BEYOND
> TPO requires explicit written patient authorization.

---

### 🛡️ Security Rule <a name="security-rule"></a>

- Establishes national standards for protecting **electronic PHI
  (ePHI)**
- Effective: **April 21, 2005**
- Applies ONLY to **ePHI** — not paper records (Privacy Rule covers
  all PHI)
- Requires covered entities to implement **administrative, physical,
  and technical safeguards**
- Based on **flexibility** — no specific technology mandated

#### Three Categories of Security Safeguards

| Category | Description | Examples |
|---|---|---|
| **Administrative Safeguards** | Policies, procedures, and management processes | Risk analysis, security officer, workforce training, contingency plan |
| **Physical Safeguards** | Physical access controls for systems containing ePHI | Facility access controls, workstation use policies, device controls |
| **Technical Safeguards** | Technology controls protecting ePHI | Access controls, audit controls, encryption, automatic logoff |

#### Required vs Addressable Specifications

| Type | Meaning |
|---|---|
| **Required** | Must be implemented — no exceptions |
| **Addressable** | Must assess whether reasonable and appropriate — if yes implement; if no document why and implement alternative |

> [!IMPORTANT]
> **Addressable ≠ Optional.** Addressable specifications must still
> be assessed and either implemented OR an equivalent alternative
> documented. Organizations cannot simply skip addressable specs —
> they must formally evaluate each one. This is a very common MCQ
> trap.

#### Key Required Administrative Safeguards
- **Risk Analysis** — identify risks to ePHI (required)
- **Risk Management** — reduce risks to reasonable level (required)
- **Security Officer** — designate a HIPAA Security Officer (required)
- **Workforce Training** — train all staff on security policies (required)
- **Sanction Policy** — discipline staff who violate policies (required)

---

### 🚨 Breach Notification Rule <a name="breach-rule"></a>

- Added by **HITECH Act 2009** — formalized in **Omnibus Rule 2013**
- Requires covered entities to notify affected individuals, HHS, and
  sometimes media when a breach of unsecured PHI occurs

#### What Constitutes a Breach
- **Breach** = acquisition, access, use, or disclosure of PHI that:
  - Violates the Privacy Rule AND
  - Compromises the security or privacy of the PHI
- **Presumption of Breach** — any impermissible use/disclosure is
  presumed a breach UNLESS the covered entity demonstrates low
  probability PHI was compromised

#### Notification Requirements

| Notification | To Whom | Timeline |
|---|---|---|
| **Individual Notification** | Affected individuals | **Without unreasonable delay — within 60 days** of breach discovery |
| **HHS Notification (Large)** | HHS Secretary | Within **60 days** if breach affects **500+ individuals** |
| **HHS Notification (Small)** | HHS Secretary | Within **60 days after end of calendar year** if breach affects **<500 individuals** |
| **Media Notification** | Prominent local media | Within **60 days** if breach affects **500+ individuals in a state** |

> [!IMPORTANT]
> **HIPAA breach notification = 60 days** (not 72 hours like GDPR).
> This distinction is a common MCQ trap. GDPR = 72 hours to DPA.
> HIPAA = 60 days to individuals and HHS. Both numbers must be
> memorized.

#### Exceptions — When Breach Notification is NOT Required
- **Unintentional access** by workforce member — acting in good faith,
  within scope of authority, no further disclosure
- **Inadvertent disclosure** between authorized persons at same entity
- **Good faith belief** unauthorized person could not have retained info

#### Breach vs Security Incident
- **Security Incident** = attempted or successful unauthorized access
  to ePHI
- **Breach** = specific type of privacy violation — not all security
  incidents are breaches

---

### ⚖️ Enforcement Rule <a name="enforcement-rule"></a>

- Effective: **March 16, 2006**
- Establishes procedures for **investigations and hearings** related
  to HIPAA violations
- Defines **civil money penalties (CMPs)** for violations
- OCR (Office for Civil Rights) investigates complaints and conducts
  compliance reviews
- Department of Justice (DOJ) handles criminal violations

#### Civil vs Criminal Penalties

| Type | Authority | When | Penalty |
|---|---|---|---|
| **Civil** | OCR/HHS | Unintentional or negligent violations | $100–$50,000 per violation |
| **Criminal** | Department of Justice | Knowingly obtaining or disclosing PHI | Up to $250,000 + 10 years imprisonment |

---

### 📋 Omnibus Rule <a name="omnibus-rule"></a>

- Effective: **March 26, 2013**
- Most comprehensive HIPAA update — implemented HITECH Act provisions
- Key changes:

| Change | Detail |
|---|---|
| **Business Associates directly liable** | BAs now directly subject to HIPAA — not just through contracts |
| **Breach notification updated** | Changed breach definition — presumption of breach |
| **Penalty tiers clarified** | Four-tier penalty structure formalized |
| **Patient rights expanded** | Right to electronic copy of records, restrict disclosure to health plans |
| **Marketing restrictions** | Stricter rules on using PHI for marketing |
| **Sale of PHI** | Prohibited without patient authorization |
| **Research** | Updated provisions for research uses of PHI |

---

## 🏥 Protected Health Information (PHI) <a name="phi"></a>

- **PHI = Protected Health Information**
- Any information that:
  1. Relates to a person's **past, present, or future health condition**,
     provision of healthcare, or payment for healthcare AND
  2. Can **identify** the individual

### Forms of PHI

| Form | Description |
|---|---|
| **PHI** | All forms — paper, oral, electronic |
| **ePHI** | Electronic PHI specifically — covered by Security Rule |
| **De-identified PHI** | PHI with all 18 identifiers removed — NOT protected by HIPAA |

### What PHI Covers

| Category | Examples |
|---|---|
| **Medical Records** | Diagnoses, prescriptions, lab results, medical history |
| **Financial Information** | Payment records, insurance information |
| **Demographic Information** | Name, address, date of birth, SSN |
| **Appointment Information** | Dates of service, provider names |
| **Images** | X-rays, photos used for medical purposes |

---

## 🏢 Covered Entities <a name="covered-entities"></a>

HIPAA applies to **Covered Entities (CEs)** — three categories:

| Category | Examples |
|---|---|
| **Healthcare Providers** | Hospitals, doctors, clinics, pharmacies, nursing homes, dentists — who transmit health information electronically |
| **Health Plans** | Health insurance companies, HMOs, Medicare, Medicaid, employer-sponsored health plans |
| **Healthcare Clearinghouses** | Entities that process nonstandard health information into standard format (or vice versa) |

> [!NOTE]
> Not ALL healthcare providers are covered entities — only those that
> **transmit health information electronically** in connection with
> standard transactions. A doctor who only uses paper records and
> never bills electronically is technically not a covered entity —
> though this is increasingly rare.

---

## 🤝 Business Associates <a name="business-associates"></a>

- **Business Associate (BA)** = A person or organization that performs
  functions involving PHI **on behalf of** a covered entity
- BAs are NOT healthcare providers themselves — they are vendors and
  service providers
- Must sign a **Business Associate Agreement (BAA)** with the covered
  entity

### Examples of Business Associates

| BA Type | Examples |
|---|---|
| **IT Service Providers** | Cloud providers, EHR vendors, data backup services |
| **Administrative Services** | Billing companies, coding services |
| **Legal/Financial** | Law firms, accountants, consultants |
| **Other Services** | Transcription services, shredding companies, data analytics |

### Business Associate Agreement (BAA)
- **Required by HIPAA** when a covered entity shares PHI with a BA
- Specifies:
  - How BA will use and protect PHI
  - BA's obligation to report breaches
  - BA's obligation to ensure subcontractors comply
  - Return or destruction of PHI at end of relationship
- Since Omnibus Rule 2013 — **BAs are directly liable** for HIPAA
  compliance (not just contractually liable through BAA)

---

## 🔐 HIPAA Safeguards <a name="hipaa-safeguards"></a>

### Administrative Safeguards (Security Rule)

| Safeguard | R/A | Description |
|---|---|---|
| Security Management Process | R | Risk analysis and risk management |
| Assigned Security Responsibility | R | Designate Security Officer |
| Workforce Security | A | Authorization, supervision, termination procedures |
| Information Access Management | A | Access authorization and modification |
| Security Awareness and Training | A | Training, reminders, log monitoring, password management |
| Security Incident Procedures | R | Identify and respond to incidents |
| Contingency Plan | R | Data backup, disaster recovery, emergency mode |
| Evaluation | R | Periodic technical and non-technical evaluation |
| BA Contracts | R | Business Associate Agreements |

### Physical Safeguards (Security Rule)

| Safeguard | R/A | Description |
|---|---|---|
| Facility Access Controls | A | Limit physical access to systems |
| Workstation Use | R | Specify proper workstation functions |
| Workstation Security | R | Physical safeguards for workstations |
| Device and Media Controls | R | Disposal, re-use, accountability of media |

### Technical Safeguards (Security Rule)

| Safeguard | R/A | Description |
|---|---|---|
| Access Control | R | Unique user IDs, emergency access, auto logoff, encryption |
| Audit Controls | R | Record and examine activity on systems with ePHI |
| Integrity Controls | A | Protect ePHI from improper alteration or destruction |
| Transmission Security | A | Protect ePHI transmitted over networks — encryption |

> *R = Required, A = Addressable*

---

## 📌 Extra Notes <a name="extra-notes"></a>

> [!NOTE]
> Everything in this section goes beyond the core syllabus but is
> directly MCQ-relevant. Cross-referenced from HHS official HIPAA
> documentation and healthcare compliance literature. Zero internet
> needed after reading this.

---

### 💻 HITECH Act — Connection to HIPAA <a name="hitech"></a>

- **HITECH = Health Information Technology for Economic and Clinical
  Health Act**
- Enacted as part of the **American Recovery and Reinvestment Act
  (ARRA) on February 17, 2009**
- Significantly strengthened and expanded HIPAA

#### Key HITECH Changes to HIPAA

| Change | Detail |
|---|---|
| **Breach Notification** | Required covered entities to notify individuals of PHI breaches |
| **Increased Penalties** | Raised maximum penalties from $25,000 to $1.5 million per violation category |
| **Business Associates** | Extended HIPAA obligations directly to Business Associates |
| **Enforcement** | Required HHS to conduct periodic audits of covered entities |
| **Electronic Records** | Promoted adoption of Electronic Health Records (EHRs) |
| **Patient Rights** | Patients can request electronic copy of records |

> [!IMPORTANT]
> **HITECH is what gave HIPAA real teeth.** Before HITECH, penalties
> were low and enforcement was weak. HITECH dramatically increased
> penalties, created mandatory breach notification, and made Business
> Associates directly liable. The Omnibus Rule 2013 implemented
> HITECH requirements.

---

### 🔑 PHI vs ePHI vs PII <a name="phi-vs-ephi"></a>

| Term | Definition | Covered By |
|---|---|---|
| **PHI** | Protected Health Information — all forms (paper, oral, electronic) | HIPAA Privacy Rule |
| **ePHI** | Electronic PHI — PHI in electronic form only | HIPAA Security Rule |
| **PII** | Personally Identifiable Information — any info identifying a person | No single federal law (various laws — GDPR, state laws) |

### Relationship Between PHI and PII

```
PII (broad)
│
└── Subset: PHI (health-related PII)
            │
            └── Subset: ePHI (electronic PHI)
```

> [!TIP]
> All PHI is PII but not all PII is PHI. ePHI is a subset of PHI.
> The Security Rule only covers ePHI — paper PHI is covered only by
> the Privacy Rule. This hierarchy is tested in MCQs.

---

### 🔢 18 HIPAA Identifiers <a name="18-identifiers"></a>

For PHI to be **de-identified** (and thus no longer protected by
HIPAA), ALL **18 identifiers** must be removed:

| # | Identifier |
|---|---|
| 1 | **Names** |
| 2 | **Geographic data** smaller than state (street, city, county, ZIP) |
| 3 | **Dates** (except year) — birth date, admission, discharge, death |
| 4 | **Phone numbers** |
| 5 | **Fax numbers** |
| 6 | **Email addresses** |
| 7 | **Social Security Numbers (SSN)** |
| 8 | **Medical record numbers** |
| 9 | **Health plan beneficiary numbers** |
| 10 | **Account numbers** |
| 11 | **Certificate/license numbers** |
| 12 | **Vehicle identifiers and serial numbers** (including license plates) |
| 13 | **Device identifiers and serial numbers** |
| 14 | **Web URLs** |
| 15 | **IP addresses** |
| 16 | **Biometric identifiers** (fingerprints, voice prints) |
| 17 | **Full-face photographs** and comparable images |
| 18 | **Any other unique identifying number, code, or characteristic** |

> [!IMPORTANT]
> There are exactly **18 HIPAA identifiers** — this number is
> frequently tested in MCQs. For data to be considered de-identified,
> ALL 18 must be removed or the Expert Determination method must be
> used. Removing only some identifiers does NOT de-identify the data.

---

### ⚖️ Minimum Necessary Standard <a name="minimum-necessary"></a>

- A core Privacy Rule requirement
- Covered entities must make **reasonable efforts** to use, disclose,
  and request only the **minimum amount of PHI** necessary to
  accomplish the intended purpose
- Applies to: uses, disclosures, and requests for PHI
- Does NOT apply to: disclosures to the patient themselves, disclosures
  for treatment purposes (between providers), disclosures required by
  law

> [!NOTE]
> The Minimum Necessary Standard does NOT apply to **treatment
> disclosures between providers** — doctors need full information
> to treat patients. This exception is important and tested in MCQs.

---

### 💰 HIPAA Penalties — Four Tiers <a name="penalties"></a>

HIPAA civil penalties have **4 tiers** based on culpability:

| Tier | Violation Type | Per Violation | Annual Cap |
|---|---|---|---|
| **Tier 1** | Did not know (and could not have known) | $100 – $50,000 | $25,000 |
| **Tier 2** | Reasonable cause (not willful neglect) | $1,000 – $50,000 | $100,000 |
| **Tier 3** | Willful neglect — corrected within 30 days | $10,000 – $50,000 | $250,000 |
| **Tier 4** | Willful neglect — NOT corrected within 30 days | $50,000 | **$1,500,000** |

> [!IMPORTANT]
> The **maximum HIPAA civil penalty = $1,500,000 per violation
> category per year** (Tier 4). This cap was raised by HITECH from
> the original $25,000. The four tiers based on culpability are
> frequently tested in MCQs.

### Criminal Penalties

| Level | Violation | Fine | Imprisonment |
|---|---|---|---|
| **Level 1** | Knowingly obtaining or disclosing PHI | Up to $50,000 | Up to 1 year |
| **Level 2** | Under false pretenses | Up to $100,000 | Up to 5 years |
| **Level 3** | For commercial advantage, personal gain, or malicious harm | Up to $250,000 | Up to 10 years |

---

### 📄 Notice of Privacy Practices (NPP) <a name="npp"></a>

- **NPP = Notice of Privacy Practices**
- Required by the HIPAA Privacy Rule
- Must be provided to patients at **first point of contact** or
  service delivery
- Must be **written in plain language**
- Must explain:
  - How PHI may be used and disclosed
  - Patient rights regarding their PHI
  - How to file a complaint
  - Effective date of the notice

> [!TIP]
> Patients must acknowledge receipt of the NPP — but covered entities
> must **make a good faith effort** to obtain written acknowledgment.
> If the patient refuses to sign, the CE must document the attempt.
> The acknowledgment is NOT required for emergency treatment.

---

### ⚖️ HIPAA vs GDPR Comparison <a name="hipaa-vs-gdpr"></a>

| Feature | HIPAA | GDPR |
|---|---|---|
| **Jurisdiction** | USA | EU + extraterritorial |
| **Enacted** | 1996 (major updates 2009, 2013) | 2016 (enforced 2018) |
| **Scope** | Health information only | All personal data |
| **Applies To** | Covered Entities + Business Associates | Any org processing EU resident data |
| **Breach Notification** | 60 days | 72 hours (to DPA) |
| **Patient/Subject Rights** | Access, amend, accounting of disclosures | 8 rights (access, erasure, portability, etc.) |
| **Enforcement** | OCR (HHS) + DOJ | National DPAs |
| **Max Civil Penalty** | $1.5M per violation category per year | €20M or 4% global turnover |
| **De-identification** | 18 identifiers (Safe Harbor) or Expert Determination | Anonymisation or pseudonymisation |
| **Consent** | Required beyond TPO — opt-in for most | One of 6 lawful bases |
| **Data Portability** | Right to electronic copy | Full portability right |

> [!NOTE]
> **HIPAA 60 days vs GDPR 72 hours** — this comparison appears
> frequently in MCQs. HIPAA gives organizations significantly more
> time for breach notification. GDPR is much stricter on timeline.

---

### 🚨 Common HIPAA Violations <a name="violations"></a>

| Violation | Description |
|---|---|
| **Impermissible disclosures** | Sharing PHI without authorization or TPO basis |
| **No Business Associate Agreement** | Using a BA without a signed BAA |
| **Lack of risk analysis** | Failing to conduct required Security Rule risk analysis |
| **Insufficient ePHI access controls** | Not limiting access to minimum necessary personnel |
| **Failure to encrypt** | Transmitting or storing unencrypted ePHI on portable devices |
| **Lost/stolen devices** | Unencrypted laptops or USB drives with ePHI |
| **Unauthorized employee access** | Employees accessing PHI without legitimate purpose |
| **Improper disposal** | Throwing away PHI without shredding/destroying |
| **Social media violations** | Posting patient info or photos on social media |
| **Mailing errors** | Sending PHI to wrong address |

> [!TIP]
> **Lost or stolen unencrypted devices** is one of the most common
> real-world HIPAA breach causes. Encryption is an addressable
> specification — but organizations that don't encrypt portable
> devices face severe liability when those devices are lost.

---

### 🏛️ HIPAA Enforcement — OCR <a name="ocr"></a>

- **OCR = Office for Civil Rights** (within HHS)
- Primary HIPAA enforcement body
- Investigates complaints from individuals
- Conducts **compliance reviews** (proactive audits)
- Can impose **civil money penalties (CMPs)**
- Negotiates **Resolution Agreements** — settlements with corrective
  action plans

### OCR Investigation Process

```
Step 1 → Complaint filed or OCR initiates review
Step 2 → OCR notifies covered entity
Step 3 → Investigation — document review, interviews
Step 4 → Findings issued
        → If compliant → case closed
        → If violation → attempt resolution
Step 5 → Informal resolution / corrective action
        → OR civil money penalty if resolution fails
Step 6 → For criminal violations → refer to DOJ
```

---

### 🔍 Safe Harbor vs Expert Determination <a name="safe-harbor"></a>

Two methods to **de-identify PHI** under HIPAA:

#### Method 1 — Safe Harbor
- Remove all **18 specified identifiers**
- Covered entity has **no actual knowledge** that remaining information
  could identify the individual
- Most commonly used method — straightforward checklist

#### Method 2 — Expert Determination
- A **qualified statistical expert** certifies that the risk of
  identifying an individual is **very small**
- Expert applies generally accepted statistical and scientific
  principles
- Expert's methods and results are documented
- More complex but allows more data to be retained

| | Safe Harbor | Expert Determination |
|---|---|---|
| **Method** | Remove all 18 identifiers | Statistical expert certifies low re-identification risk |
| **Complexity** | Simple checklist | Complex statistical analysis |
| **Data retained** | Less (all 18 removed) | Potentially more |
| **Certainty** | Rule-based | Risk-based |

> [!NOTE]
> After de-identification using either method, the resulting data
> is **no longer PHI** and is **not subject to HIPAA**. It can be
> used freely for research, analysis, or any other purpose.

---

## 🔤 Abbreviations <a name="abbreviations"></a>

| Abbreviation | Full Form | One-line Meaning |
|---|---|---|
| **HIPAA** | Health Insurance Portability and Accountability Act | US federal law (1996) protecting health information privacy and security |
| **PHI** | Protected Health Information | Health information that identifies an individual — protected by HIPAA Privacy Rule |
| **ePHI** | Electronic Protected Health Information | PHI in electronic form — specifically covered by HIPAA Security Rule |
| **HHS** | Department of Health and Human Services | US federal department administering HIPAA |
| **OCR** | Office for Civil Rights | HHS division that enforces HIPAA — investigates complaints |
| **TPO** | Treatment, Payment, Operations | Three permitted uses of PHI that do not require patient authorization |
| **BA** | Business Associate | Third-party entity performing functions involving PHI on behalf of covered entity |
| **BAA** | Business Associate Agreement | Required contract between covered entity and business associate |
| **CE** | Covered Entity | Healthcare provider, health plan, or clearinghouse subject to HIPAA |
| **NPP** | Notice of Privacy Practices | Written document explaining how PHI may be used — given to patients |
| **CMP** | Civil Money Penalty | Financial penalty imposed by OCR for HIPAA violations |
| **HITECH** | Health Information Technology for Economic and Clinical Health Act | 2009 law that strengthened HIPAA — added breach notification, increased penalties |
| **ARRA** | American Recovery and Reinvestment Act | 2009 law that included HITECH |
| **EHR** | Electronic Health Record | Digital version of patient health records |
| **DOJ** | Department of Justice | US agency handling criminal HIPAA violations |
| **PII** | Personally Identifiable Information | Any information identifying a natural person — broader than PHI |
| **NPI** | National Provider Identifier | Standard identifier for healthcare providers |
| **EDI** | Electronic Data Interchange | Standard electronic format for healthcare transactions |

---

## 🗝️ Keywords & Concept Map <a name="keywords"></a>

**HIPAA**
→ US federal law — August 1996 — HHS/OCR enforces
→ 5 Titles — Title II most important for IT/security
→ 4 main Rules: Privacy, Security, Breach Notification, Enforcement
→ Strengthened by HITECH 2009 → Omnibus Rule 2013

**PHI (Protected Health Information)**
→ Health info that identifies an individual — all forms
→ 18 HIPAA identifiers — remove all for de-identification
→ ePHI = electronic PHI — Security Rule applies
→ TPO = permitted uses without authorization

**Covered Entities**
→ Three types: Healthcare Providers, Health Plans, Clearinghouses
→ Must comply with all HIPAA Rules
→ Must have BAAs with Business Associates

**Business Associates**
→ Third parties performing functions involving PHI
→ Must sign BAA with covered entity
→ Directly liable since Omnibus Rule 2013
→ Examples: cloud providers, billing companies, EHR vendors

**Privacy Rule (2003)**
→ Protects all PHI — paper, oral, electronic
→ Gives patients 8 rights over their PHI
→ TPO = permitted without authorization
→ Minimum Necessary Standard — use only what's needed
→ NPP required at first contact

**Security Rule (2005)**
→ Protects ePHI only — electronic PHI
→ Three safeguards: Administrative, Physical, Technical
→ Required vs Addressable specifications
→ Addressable ≠ Optional — must assess and document

**Breach Notification Rule**
→ Added by HITECH 2009 — 60 days to notify individuals and HHS
→ Media notification if 500+ in a state
→ Presumption of breach — organization must prove otherwise
→ HHS wall of shame — public list of large breaches

---

## ⚡ Quick Reference Cheatsheet <a name="cheatsheet"></a>

### HIPAA 5 Titles

| Title | Name | Key Focus |
|---|---|---|
| **I** | Health Care Access, Portability, Renewability | Insurance portability between jobs |
| **II** | Preventing Fraud — Administrative Simplification | **Privacy + Security Rules — IT focus** |
| **III** | Tax-Related Health Provisions | Tax provisions |
| **IV** | Group Health Plan Requirements | Coverage enforcement |
| **V** | Revenue Offsets | Company insurance provisions |

### HIPAA 4 Main Rules

| Rule | Effective | Focus |
|---|---|---|
| **Privacy Rule** | April 14, 2003 | All PHI — patient rights, TPO, NPP |
| **Security Rule** | April 21, 2005 | ePHI only — 3 safeguards |
| **Breach Notification Rule** | 2009/2013 | 60-day notification requirement |
| **Enforcement Rule** | March 16, 2006 | Penalties, investigations, CMPs |

### Three Security Safeguard Categories

| Category | Focus | Required/Addressable Mix |
|---|---|---|
| **Administrative** | Policies and management | Mix of R and A |
| **Physical** | Physical access | Mix of R and A |
| **Technical** | Technology controls | Mix of R and A |

### HIPAA Breach Notification Timelines

| Notification | To Whom | Timeline |
|---|---|---|
| Individual | Affected patients | Within **60 days** |
| HHS (large breach) | HHS Secretary | Within **60 days** (500+ affected) |
| HHS (small breach) | HHS Secretary | Within **60 days after calendar year end** (<500) |
| Media | Local media | Within **60 days** (500+ in a state) |

### HIPAA vs GDPR — Key Numbers

| | HIPAA | GDPR |
|---|---|---|
| Breach notification | **60 days** | **72 hours** |
| Max civil penalty | **$1.5M/year** | **€20M or 4%** |
| Data identifiers | **18** | No fixed number |
| Enacted | **1996** | **2018** |

### HIPAA Civil Penalty Tiers

| Tier | Culpability | Per Violation | Annual Cap |
|---|---|---|---|
| 1 | Didn't know | $100–$50K | $25K |
| 2 | Reasonable cause | $1K–$50K | $100K |
| 3 | Willful — corrected | $10K–$50K | $250K |
| 4 | Willful — uncorrected | $50K | **$1.5M** |

### Three Covered Entity Types

| Type | Examples |
|---|---|
| Healthcare Providers | Hospitals, doctors, pharmacies, dentists |
| Health Plans | Insurance companies, HMOs, Medicare, Medicaid |
| Healthcare Clearinghouses | Claims processors, billing intermediaries |

### Privacy Rule vs Security Rule

| | Privacy Rule | Security Rule |
|---|---|---|
| Effective | 2003 | 2005 |
| Covers | All PHI (paper, oral, electronic) | ePHI only |
| Focus | Patient rights, use/disclosure | Technical/admin/physical safeguards |
| Authorization | TPO — no auth needed | N/A — security controls |

### De-identification Methods

| Method | How | Used When |
|---|---|---|
| **Safe Harbor** | Remove all 18 identifiers | Standard approach — rule-based |
| **Expert Determination** | Statistician certifies low risk | When more data must be retained |

### HIPAA Timeline

| Year | Event |
|---|---|
| 1996 | HIPAA enacted |
| 2003 | Privacy Rule effective |
| 2005 | Security Rule effective |
| 2006 | Enforcement Rule effective |
| 2009 | HITECH Act enacted |
| 2013 | Omnibus Rule effective |

---

## 🔁 Session Revision Snapshot <a name="snapshot"></a>

### TL;DR — 5 Bullets
- ✅ HIPAA = US federal law 1996 — enforced by OCR/HHS — applies to
  Covered Entities (3 types) and Business Associates — 5 Titles —
  Title II most important for IT
- ✅ 4 main HIPAA Rules: Privacy Rule (2003 — all PHI), Security Rule
  (2005 — ePHI only), Breach Notification (60 days), Enforcement
  (penalties)
- ✅ Security Rule = 3 safeguards: Administrative, Physical, Technical
  — Required vs Addressable — **Addressable ≠ Optional**
- ✅ PHI de-identification: remove all **18 identifiers** (Safe Harbor)
  OR Expert Determination — de-identified data is no longer PHI
- ✅ HITECH 2009 strengthened HIPAA — added breach notification,
  raised penalties to $1.5M max, made Business Associates directly
  liable — Omnibus Rule 2013 implemented HITECH

### 🎯 Top MCQ-Likely Concepts from This Session
1. **HIPAA = 1996** — signed by Clinton — enforced by OCR/HHS
2. **Title II = Administrative Simplification** — most IT-relevant
3. **Privacy Rule = all PHI** / **Security Rule = ePHI only**
4. **TPO = Treatment, Payment, Operations** — no authorization needed
5. **3 safeguards** — Administrative, Physical, Technical
6. **Addressable ≠ Optional** — must assess and document
7. **18 HIPAA identifiers** — all must be removed for de-identification
8. **60 days breach notification** vs GDPR's 72 hours — key difference
9. **4 penalty tiers** — Tier 4 = $1.5M maximum
10. **HITECH 2009** — what it added to HIPAA
11. **Business Associates directly liable** since Omnibus Rule 2013
12. **BAA required** for every business associate relationship
13. **Safe Harbor vs Expert Determination** — two de-identification methods
14. **Minimum Necessary Standard** — does NOT apply to treatment disclosures

---