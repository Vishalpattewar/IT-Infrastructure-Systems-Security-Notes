# Session 09 — Aadhaar, e-Sign & Timestamping Services

## 📑 Table of Contents

- [1. Aadhaar — India's Digital Identity
  System](#1-aadhaar--indias-digital-identity-system)
  - [1.1 What is Aadhaar?](#11-what-is-aadhaar)
  - [1.2 Aadhaar Architecture](#12-aadhaar-architecture)
  - [1.3 Aadhaar Authentication Modes](#13-aadhaar-authentication-modes)
  - [1.4 Aadhaar Legal Framework](#14-aadhaar-legal-framework)
  - [1.5 Aadhaar and PKI](#15-aadhaar-and-pki)
- [2. e-Sign — Electronic Signature Service](#2-e-sign--electronic-signature-service)
  - [2.1 What is e-Sign?](#21-what-is-e-sign)
  - [2.2 Why e-Sign Was Created](#22-why-e-sign-was-created)
  - [2.3 e-Sign Architecture](#23-e-sign-architecture)
  - [2.4 e-Sign Workflow — Step by Step](#24-e-sign-workflow--step-by-step)
  - [2.5 e-Sign vs Physical DSC](#25-e-sign-vs-physical-dsc)
  - [2.6 e-Sign Legal Validity](#26-e-sign-legal-validity)
  - [2.7 e-Sign Use Cases](#27-e-sign-use-cases)
- [3. Timestamping Services](#3-timestamping-services)
  - [3.1 What is Timestamping?](#31-what-is-timestamping)
  - [3.2 Why Timestamps Are Needed](#32-why-timestamps-are-needed)
  - [3.3 Trusted Timestamping — How It Works](#33-trusted-timestamping--how-it-works)
  - [3.4 Time Stamp Protocol (TSP)](#34-time-stamp-protocol-tsp)
  - [3.5 TSP Step by Step](#35-tsp-step-by-step)
  - [3.6 Time Stamp Token (TST) Structure](#36-time-stamp-token-tst-structure)
  - [3.7 Timestamping in Practice](#37-timestamping-in-practice)
- [4. 📌 Extra Notes](#4--extra-notes)
  - [4.1 Aadhaar e-KYC](#41-aadhaar-e-kyc)
  - [4.2 Virtual ID (VID) and Aadhaar
    Privacy](#42-virtual-id-vid-and-aadhaar-privacy)
  - [4.3 e-Sign vs eIDAS — Comparison](#43-e-sign-vs-eidas--comparison)
  - [4.4 Long-Term Validation (LTV)](#44-long-term-validation-ltv)
  - [4.5 PAdES, CAdES, XAdES — Signature
    Formats](#45-pades-cades-xades--signature-formats)
  - [4.6 Aadhaar-based e-Sign in DigiLocker](#46-aadhaar-based-e-sign-in-digilocker)
  - [4.7 Timestamping and Non-Repudiation](#47-timestamping-and-non-repudiation)
  - [4.8 RFC 3161 — TSP Standard Details](#48-rfc-3161--tsp-standard-details)
  - [4.9 Trusted Timestamp Authorities in
    India](#49-trusted-timestamp-authorities-in-india)
  - [4.10 Aadhaar Biometric Lock](#410-aadhaar-biometric-lock)
  - [4.11 UIDAI Security Architecture](#411-uidai-security-architecture)
  - [4.12 Common Misconceptions — Aadhaar
    and e-Sign](#412-common-misconceptions--aadhaar-and-e-sign)
- [5. Abbreviations Table](#5-abbreviations-table)
- [6. Keywords + Concept Map](#6-keywords--concept-map)
- [7. Quick Reference Cheatsheet](#7-quick-reference-cheatsheet)
- [8. Session Revision Snapshot](#8-session-revision-snapshot)

---

## 1. Aadhaar — India's Digital Identity System

### 1.1 What is Aadhaar?

**Aadhaar** is India's national biometric
identity system — a 12-digit unique identification
number issued to every resident of India by the
**UIDAI (Unique Identification Authority of India)**.

| Property | Detail |
|----------|--------|
| **Name** | Aadhaar (आधार — means "foundation" in Hindi) |
| **Issuing authority** | UIDAI (Unique Identification Authority of India) |
| **Established by** | Aadhaar (Targeted Delivery of Financial and Other Subsidies, Benefits and Services) Act, 2016 |
| **Number format** | 12-digit unique number |
| **Enrolment data** | Demographic (name, DOB, address, gender) + Biometric (10 fingerprints, 2 iris scans, photograph) |
| **Total enrolled** | 1.4+ billion residents (largest biometric database in the world) |
| **Operator** | UIDAI — a statutory authority under Ministry of Electronics and Information Technology (MeitY) |

> [!IMPORTANT]
> Aadhaar is the foundation of India's digital
> public infrastructure — it enables:
> - **Digital identity verification** without
>   physical documents
> - **e-KYC** (electronic Know Your Customer)
>   for financial services
> - **e-Sign** (electronic signature using
>   Aadhaar authentication)
> - **Direct Benefit Transfer (DBT)** — government
>   subsidies directly to beneficiaries
> - **DigiLocker** — digital document storage
>   linked to Aadhaar

---

### 1.2 Aadhaar Architecture

```
CIDR (Central Identities Data Repository)
│  → Stores all Aadhaar numbers and
│    associated biometric/demographic data
│  → Operated by UIDAI
│  → Most sensitive database in India
│
├── Authentication APIs
│   → Used by AUAs (Authentication User Agencies)
│   → Banks, telecom operators, government depts
│
├── e-KYC APIs
│   → Returns demographic data after
│     successful authentication
│
└── e-Sign APIs
    → Issues one-time digital signature
      certificates after Aadhaar authentication
```

**Key entities in the Aadhaar ecosystem:**

| Entity | Full Name | Role |
|--------|-----------|------|
| **UIDAI** | Unique Identification Authority of India | Operates CIDR, issues Aadhaar, regulates the system |
| **AUA** | Authentication User Agency | Organizations using Aadhaar authentication (banks, telecom) |
| **ASA** | Authentication Service Agency | Technical intermediaries connecting AUAs to CIDR |
| **KUA** | KYC User Agency | Organizations using Aadhaar e-KYC service |
| **ESP** | e-Sign Service Provider | Provides e-Sign service — issues one-time certificates |
| **Sub-AUA** | Sub-Authentication User Agency | Organizations using authentication via an AUA |

---

### 1.3 Aadhaar Authentication Modes

Aadhaar supports multiple authentication modes —
each verifying the person's identity against CIDR:

| Mode | What It Verifies | Use Case |
|------|-----------------|---------|
| **OTP Authentication** | One-time password sent to registered mobile | Bank account opening, SIM registration |
| **Biometric Authentication** | Fingerprint or iris scan against CIDR records | PDS (ration shop), pension disbursement |
| **Demographic Authentication** | Name, DOB, address match against CIDR | Low-assurance verification |
| **Multi-factor Authentication** | Combination of above modes | High-assurance use cases |

**Authentication flow:**
```
Resident → AUA's service
     │
     ▼
AUA captures authentication data
(OTP / biometric / demographic)
     │
     ▼
AUA → ASA → UIDAI CIDR
     │
     ▼
CIDR verifies against stored data
     │
     ▼
UIDAI returns: YES / NO
(+ optional e-KYC data if authorized)
     │
     ▼
AUA grants/denies service access
```

> [!NOTE]
> **UIDAI returns only YES or NO** for basic
> authentication — it does not return the
> resident's biometric data or any sensitive
> personal information to the AUA.
>
> For e-KYC, UIDAI returns demographic data
> (name, address, photo) ONLY if the resident
> has consented and the KUA is authorized.

---

### 1.4 Aadhaar Legal Framework

| Legislation | Detail |
|-------------|--------|
| **Aadhaar Act 2016** | Primary law governing Aadhaar — defines UIDAI, enrollment, authentication, and data protection |
| **IT Act 2000** | Governs digital signatures and electronic records — e-Sign under Aadhaar operates under IT Act |
| **Supreme Court ruling (2018)** | Aadhaar constitutional but restricted to government benefits and services — private companies cannot mandate Aadhaar |
| **Aadhaar (Amendment) Act 2019** | Permitted voluntary use of Aadhaar for private entities with consent |

**Key UIDAI regulatory documents:**
- Aadhaar Authentication Regulations
- Aadhaar (Data Security) Regulations
- Aadhaar e-KYC Regulations

> [!IMPORTANT]
> **Supreme Court ruling (Puttaswamy case, 2018):**
> The Supreme Court upheld Aadhaar as constitutional
> but declared that private companies cannot mandate
> Aadhaar for their services. Aadhaar remains
> mandatory for specific government benefits
> (PDS, pension, income tax PAN linking).
>
> The 2019 amendment allowed VOLUNTARY use of
> Aadhaar for private entities (like banks, telecom)
> with explicit resident consent.

---

### 1.5 Aadhaar and PKI

Aadhaar interacts with PKI in two critical ways:

**1. Aadhaar authentication data security:**
- All data transmitted between AUAs/ASAs and CIDR
  is encrypted and digitally signed
- **AUA request:** Digitally signed with AUA's
  private key + encrypted with UIDAI's public key
- **UIDAI response:** Digitally signed with
  UIDAI's private key — AUAs verify with UIDAI's
  public certificate
- Ensures only authorized AUAs can query CIDR
  and responses cannot be forged

**2. Aadhaar e-Sign (covered in Section 2):**
- Aadhaar authentication triggers on-demand
  issuance of a Digital Signature Certificate
  by an ESP (e-Sign Service Provider)
- Resident signs a document using this one-time
  certificate — without owning a physical DSC

---

## 2. e-Sign — Electronic Signature Service

### 2.1 What is e-Sign?

**e-Sign** is an Aadhaar-based **electronic
signature service** that allows any Aadhaar holder
to digitally sign a document using their Aadhaar
authentication — without needing to purchase or
manage a physical Digital Signature Certificate
(DSC on a USB token).

| Property | Detail |
|----------|--------|
| **Full name** | e-Sign — Electronic Signature Service |
| **Introduced** | 2015 by MeitY and UIDAI |
| **Standard** | e-Sign Online Electronic Signature Service (by CCA India) |
| **Basis** | Aadhaar OTP or biometric authentication |
| **Legal validity** | Recognized under IT Act 2000 as an Electronic Signature |
| **Certificate type** | One-time-use DSC issued by licensed ESP |
| **Key storage** | ESP's HSM — signer never holds the private key |

---

### 2.2 Why e-Sign Was Created

**Problem with traditional DSC:**

```
Traditional DSC (Physical):
  → User must purchase a USB token (~₹500–2000)
  → User must visit CA office for verification
  → USB driver installation required
  → Works only on Windows — not on mobile
  → Certificate valid 1–3 years
  → Complex for non-technical users
  → Impractical for one-time signers

e-Sign Solution:
  → No physical token needed
  → Authentication via Aadhaar OTP or biometric
  → Works on mobile and web browsers
  → One-time certificate generated on demand
  → Instant issuance in seconds
  → Accessible to all 1.4 billion Aadhaar holders
```

**e-Sign enables mass digital signing** at
national scale — making digital governance
accessible to everyone including rural and
non-technical citizens.

---

### 2.3 e-Sign Architecture

```
Key entities:

Application Service Provider (ASP)
│  → The application where signing happens
│    (tax portal, bank app, government service)
│
ESP (e-Sign Service Provider)
│  → Licensed by CCA India
│  → Holds HSM with signing infrastructure
│  → Issues one-time certificates
│  → Verifies Aadhaar authentication result
│
UIDAI
│  → Authenticates the Aadhaar holder
│  → Returns YES/NO to ESP
│
CA (Certifying Authority)
   → Licensed CA integrated with ESP
   → Issues the one-time DSC to ESP for signing
```

---

### 2.4 e-Sign Workflow — Step by Step

```
Step 1: User initiates signing in application (ASP)
  → "Sign with e-Sign" button clicked

Step 2: ASP sends document hash to ESP
  → Document itself is NOT sent to ESP
  → Only the hash (SHA-256) is sent
  → Protects document confidentiality

Step 3: ESP requests Aadhaar authentication
  → User receives OTP on Aadhaar-registered mobile
    OR provides biometric (fingerprint/iris)

Step 4: User provides OTP / biometric to ASP
  → ASP forwards to ESP

Step 5: ESP sends authentication request to UIDAI
  → UIDAI verifies OTP/biometric against CIDR

Step 6: UIDAI returns authentication result to ESP
  → Result: YES (authenticated) or NO

Step 7: If YES — ESP requests one-time certificate
  from licensed CA
  → CA issues DSC (1-year validity)
    bound to Aadhaar holder's name

Step 8: ESP signs the document hash using
  the one-time private key (in HSM)
  → Creates digital signature

Step 9: ESP returns the digital signature to ASP

Step 10: ASP embeds signature in document
  → Document is now digitally signed ✅
  → One-time private key is destroyed after use
```

> [!IMPORTANT]
> **Key security property of e-Sign:**
> The **signer never touches the private key** —
> it is generated, used, and destroyed entirely
> within the ESP's HSM.
>
> The signer's identity is authenticated via
> Aadhaar (OTP or biometric) — binding the
> signature to their Aadhaar-verified identity.
>
> Only the **document hash** is sent to the ESP —
> the document content never leaves the user's
> application. This protects document
> confidentiality.

---

### 2.5 e-Sign vs Physical DSC

| Property | e-Sign | Physical DSC |
|----------|--------|-------------|
| **Token required** | ❌ No — no USB token | ✅ Yes — USB token or smart card |
| **Authentication** | Aadhaar OTP or biometric | PIN/password to USB token |
| **Private key location** | ESP's HSM (never with signer) | USB token held by signer |
| **Key reuse** | One-time (new key per signing event) | Reused for entire certificate validity |
| **Issuance time** | Seconds (real-time, automated) | Hours to days (verification needed) |
| **Cost** | Per-use (~₹20–50 per signature) | One-time (~₹500–2000 for token + cert) |
| **Validity** | One-time use | 1–3 years |
| **Mobile friendly** | ✅ Yes | ❌ No (USB tokens don't work on phones) |
| **Non-repudiation** | Aadhaar-bound — strong | Private key-bound — strong |
| **Legal status** | IT Act 2000 — Electronic Signature | IT Act 2000 — Digital Signature |

> [!NOTE]
> e-Sign is classified as an **Electronic Signature**
> under the IT Act — not a "Digital Signature."
> Physical DSC is a "Digital Signature" under the
> IT Act — considered a higher class.
> For most purposes e-Sign is legally sufficient —
> but some high-value government transactions
> (Class 3 e-tendering) still require physical DSC.

---

### 2.6 e-Sign Legal Validity

**e-Sign is legally recognized under:**

| Law | Recognition |
|-----|-------------|
| **IT Act 2000 (Section 5)** | Electronic signatures using Aadhaar authentication are legally valid for all purposes for which handwritten signature is required (except specific exclusions) |
| **IT (Amendment) Act 2008** | Expanded recognition of electronic signatures |
| **CCA Guidelines (2015)** | Defined e-Sign as an approved electronic signature method |
| **Various sector regulations** | SEBI, RBI, MCA have all recognized e-Sign for specific filings |

**Where e-Sign CANNOT be used (exclusions under IT Act):**
- Negotiable instruments (cheques, promissory notes)
- Powers of attorney
- Trust deeds
- Wills and codicils
- Sale of immovable property (land/real estate)
- Any document requiring registration under
  the Registration Act 1908

> [!NOTE]
> These exclusions apply to both e-Sign AND physical
> DSC — the IT Act excludes these categories from
> electronic signature validity altogether.

---

### 2.7 e-Sign Use Cases

| Application | How e-Sign Is Used |
|-------------|-------------------|
| **Income tax e-filing (ITR)** | Taxpayers sign ITR using Aadhaar OTP |
| **MCA filings** | Directors sign company forms digitally |
| **Bank account opening (KYC)** | Customer signs KYC form via e-Sign |
| **Loan agreements** | Borrowers sign loan documents on mobile |
| **Insurance proposals** | Customers sign proposal forms digitally |
| **Government services** | Citizens sign applications for benefits |
| **DigiLocker** | Documents issued/shared with e-Sign |
| **GSTN (GST filing)** | Taxpayers sign GST returns |
| **CoWIN (vaccination)** | Vaccine certificates signed with e-Sign |

---

## 3. Timestamping Services

### 3.1 What is Timestamping?

**Trusted timestamping** is the process of
securely recording the time at which a document
or data existed — creating a **tamper-proof,
trusted proof** that a specific piece of data
existed at a specific time.

A trusted timestamp:
- Proves a document **existed before** a certain time
- Proves it has **not been altered** since that time
- Is issued by a **Trusted Third Party (TTP)** —
  not by the document's creator

> [!IMPORTANT]
> A regular file's "last modified" timestamp is
> **NOT trusted** — it can be easily changed by
> the file owner or anyone with system access.
>
> A **trusted timestamp** (RFC 3161) is
> cryptographically signed by an independent
> Time Stamp Authority (TSA) — it cannot be
> forged or backdated without breaking the
> TSA's digital signature.

---

### 3.2 Why Timestamps Are Needed

**Scenario 1 — Proving existence before a date:**
```
Inventor Alice creates an invention document.
Six months later, Competitor Bob claims he
invented it first.

With trusted timestamp on Alice's document:
  → Timestamp proves Alice's document existed
    on a specific date — before Bob's claim
  → Legally provable — TSA's signature cannot
    be forged

Without trusted timestamp:
  → Alice can claim any date — unprovable
  → Bob can claim any date — unprovable
  → No objective evidence
```

**Scenario 2 — Digital signature validity after
certificate expiry:**
```
Bob signs a contract with his DSC on Jan 2024.
Bob's DSC expires in Dec 2024.
In Jan 2026, the contract is disputed.

Problem: Verifier checks Bob's DSC — it's expired.
  → Is the signature still valid?
  → Was the DSC valid WHEN he signed?

With trusted timestamp on the signature:
  → Timestamp proves the signature was created
    on Jan 2024 when the DSC was still valid
  → Signature remains legally valid despite
    DSC expiry

Without timestamp:
  → No way to prove when the signature was made
  → Potentially invalid if DSC is expired/revoked
```

---

### 3.3 Trusted Timestamping — How It Works

**Core principle:**
A Time Stamp Authority (TSA) is a trusted third party
that creates a cryptographically signed record
certifying that specific data (identified by its hash)
existed at a specific time.

```
Key insight:
  The TSA never sees the document itself.
  The TSA receives and signs only the HASH of the document.
  This protects document confidentiality.

  If Hash(Document) = H was signed by TSA at time T:
    → Document existed at time T (proven by hash)
    → Document has not changed since (hash integrity)
    → Time T is trustworthy (TSA's signature)
```

---

### 3.4 Time Stamp Protocol (TSP)

**TSP (Time Stamp Protocol)** is defined in
**RFC 3161** (2001) — the standard for trusted
timestamping on the internet.

| Property | Detail |
|----------|--------|
| **RFC** | RFC 3161 (2001) — updated by RFC 5816 (2010) |
| **Protocol type** | Request-Response |
| **Transport** | HTTP or TCP |
| **Data format** | ASN.1 DER encoded |
| **Hash required** | Client sends hash of data (not the data itself) |
| **Response** | TSA returns a Time Stamp Token (TST) |
| **TST signed by** | TSA using its TSA signing certificate |

---

### 3.5 TSP Step by Step

```
CLIENT (Document Signer / Application):

Step 1: Compute hash of the document/data
  H = SHA-256(Document)

Step 2: Create Time Stamp Request (TSQ)
  TSQ contains:
    - Hash algorithm used (SHA-256)
    - Hash value H
    - Optional nonce (random value — prevents replay)
    - Optional policy OID (requesting specific TSA policy)
    - Request for TSA certificate inclusion

Step 3: Send TSQ to TSA (via HTTP POST)

─────────────────────────────────────────────

TSA (Time Stamp Authority):

Step 4: TSA receives TSQ

Step 5: TSA records current trusted time
  (synchronized via NTP to authoritative time sources)

Step 6: TSA creates Time Stamp Token (TST):
  TST contains:
    - TSA policy OID
    - Hash algorithm
    - Hash value H (from client's request)
    - Time of timestamping (genTime)
    - Serial number (unique per TST)
    - Nonce (if provided — echoed back)
    - TSA's digital signature over all above

Step 7: TSA sends Time Stamp Response (TSR) back
  TSR contains: status code + TST

─────────────────────────────────────────────

CLIENT:

Step 8: Client receives TSR

Step 9: Client verifies TSA's signature on TST

Step 10: Client stores TST alongside document
  → Document + TST = timestamped evidence package
```

---

### 3.6 Time Stamp Token (TST) Structure

A TST is a CMS (Cryptographic Message Syntax)
SignedData structure:

```
TimeStampToken (TST):
  │
  ├── TSTInfo (signed content):
  │     ├── version (always 1)
  │     ├── policy (TSA policy OID)
  │     ├── messageImprint:
  │     │     ├── hashAlgorithm (e.g., SHA-256)
  │     │     └── hashedMessage (the hash H)
  │     ├── serialNumber (unique TST identifier)
  │     ├── genTime (EXACT timestamp in UTC)
  │     ├── accuracy (time accuracy ± milliseconds)
  │     ├── nonce (if requested)
  │     └── tsa (TSA's name — optional)
  │
  └── SignerInfo:
        ├── TSA signing certificate
        └── TSA digital signature over TSTInfo
```

> [!NOTE]
> The **genTime** field in the TST is the exact
> time the TSA generated the token — expressed
> in UTC (Coordinated Universal Time) with
> accuracy typically in milliseconds or seconds.
>
> The TSA's signing certificate has an
> **Extended Key Usage (EKU)** of `timeStamping`
> — indicating it is specifically authorized for
> issuing timestamp tokens.

---

### 3.7 Timestamping in Practice

**Where trusted timestamps are used:**

| Use Case | How Timestamp Is Applied |
|----------|-------------------------|
| **PDF document signing (PAdES-T)** | TST embedded in PDF signature — proves when document was signed |
| **Code signing** | Timestamp on code signature — signature remains valid after cert expiry |
| **Legal e-contracts** | Timestamp proves exact time contract was signed |
| **Patent applications** | Timestamp proves invention existed before filing date |
| **Audit logs** | Timestamp proves log entries were not backdated |
| **Blockchain** | Each block header contains timestamp |
| **E-mail archiving** | Timestamp proves email existed at specific time |
| **Court filings** | Timestamped documents have legally admissible time proof |

**Timestamping in code signing:**
```
Developer signs software executable:
  Signature = RSA_Sign(PrivateKey, Hash(Executable))
  + Timestamp from TSA on the signature

When user runs software 3 years later:
  Developer's cert is expired — but:
  Timestamp proves signature was created WHEN
  the cert was still valid → signature still valid
  Software is still trusted ✅

Without timestamp:
  Expired cert → signature invalid → untrusted
  → Security warning or blocked execution
```

> [!IMPORTANT]
> **Timestamping is essential for long-lived
> digital signatures.**
> Without a timestamp, a digital signature
> becomes legally questionable when the
> signing certificate expires or is revoked.
> The timestamp freezes the validity of the
> signature at the moment it was created.

---

## 4. 📌 Extra Notes

> [!NOTE]
> Everything in this section goes beyond the core
> syllabus but is directly MCQ-relevant.

---

### 4.1 Aadhaar e-KYC

> [!NOTE]
> **e-KYC (electronic Know Your Customer)** is an
> Aadhaar-based service that allows organizations
> (banks, telecom) to complete customer KYC
> digitally — without physical documents.

**Types of e-KYC:**

| Type | Description |
|------|-------------|
| **Full e-KYC** | UIDAI returns demographic data (name, address, photo, DOB, gender) after authentication — requires explicit consent |
| **Limited e-KYC** | Returns only specific fields needed by the organization |
| **Offline e-KYC (Aadhaar XML)** | Resident downloads a digitally signed XML from UIDAI portal — shares it with the organization without UIDAI involvement in that transaction |

**Offline e-KYC process:**
```
1. Resident visits UIDAI portal
2. Downloads digitally signed Aadhaar XML
   (contains demographic data — photo encoded)
3. XML is signed by UIDAI's private key
4. Resident shares XML with organization
5. Organization verifies UIDAI's signature on XML
6. No real-time UIDAI query needed — offline
```

**Benefits of Offline e-KYC:**
- Resident controls when and with whom to share data
- Organization gets verified data without real-time
  UIDAI connectivity
- Reduces UIDAI server load
- Privacy-preserving — no real-time tracking

> [!NOTE]
> Offline e-KYC XML is protected by a
> **share phrase** (4-digit code) chosen by the
> resident — organizations need this code to
> parse the XML. This prevents accidental sharing.

---

### 4.2 Virtual ID (VID) and Aadhaar Privacy

> [!NOTE]
> **VID (Virtual ID)** is a temporary, revocable
> 16-digit number mapped to an Aadhaar number —
> introduced in 2018 to enhance privacy.

**The privacy problem VID solves:**
```
Before VID:
  Every time a person used Aadhaar authentication,
  their actual 12-digit Aadhaar number was shared
  with the AUA.
  AUAs could build profiles by correlating
  authentication events across multiple services.
  → Privacy concern: Aadhaar number as universal tracker

With VID:
  Person generates a temporary 16-digit VID from UIDAI portal
  VID is used for authentication instead of Aadhaar number
  AUA receives only VID — never the actual Aadhaar number
  VID can be regenerated — old VID becomes invalid
  → AUAs cannot correlate across services using VID
  → Aadhaar number remains private
```

**VID properties:**
- 16 digits (vs 12 for Aadhaar)
- Temporary and revocable — can be regenerated
- Unique mapping to Aadhaar at UIDAI level
- Can be used in place of Aadhaar number
  for authentication and e-KYC

---

### 4.3 e-Sign vs eIDAS — Comparison

> [!NOTE]

| Property | India e-Sign | EU eIDAS QES |
|----------|-------------|-------------|
| **Legal basis** | IT Act 2000 + CCA Guidelines 2015 | EU Regulation 910/2014 |
| **Authentication basis** | Aadhaar OTP or biometric | Qualified Certificate on QSCD |
| **Identity verification** | Aadhaar enrollment (biometric) | QTSP in-person verification |
| **Certificate type** | One-time DSC via ESP | Qualified Certificate (hardware token) |
| **Key storage** | ESP's HSM | Signer's QSCD (smart card) |
| **Jurisdiction** | India | EU member states (cross-border) |
| **Legal equivalence** | Electronic Signature under IT Act | Handwritten signature under eIDAS |
| **Mobile friendly** | ✅ Yes | ❌ Requires QSCD hardware |

---

### 4.4 Long-Term Validation (LTV)

> [!NOTE]
> **LTV (Long-Term Validation)** is the process
> of embedding all information needed to validate
> a signature in the future — even after
> certificates expire and CRLs become unavailable.

**The problem LTV solves:**
```
Alice signs a PDF in 2024.
By 2030:
  - Alice's signing certificate has expired
  - The CA that issued it may be gone
  - CRLs from 2024 are no longer published
  - OCSP responders for those old certs are offline

How can the 2030 verifier confirm:
  - The signature was created in 2024?
  - Alice's cert was valid in 2024?
  - The cert was not revoked in 2024?

Answer: LTV — embed everything at signing time
```

**LTV embeds at signing time:**
1. The full certificate chain (all CA certs)
2. CRL or OCSP response from the time of signing
   (proving cert was valid when signed)
3. A trusted timestamp (proving when signing occurred)
4. Timestamp TSA's certificate chain

**PAdES-LTV (PDF format):**
```
PDF signature with LTV:
  └── Signature
        ├── Signed hash of document
        ├── Signing certificate
        ├── Certificate chain (all intermediate CAs)
        ├── CRL / OCSP response at time of signing
        └── TST (Timestamp Token — with TSA cert chain)
```

A verifier in 2030 can validate the 2024 signature
entirely from data embedded in the PDF — no
external network queries needed.

---

### 4.5 PAdES, CAdES, XAdES — Signature Formats

> [!NOTE]
> These are standardized formats for **advanced
> electronic signatures** — each designed for
> a specific document type.

| Format | Full Name | Document Type | Standard |
|--------|-----------|--------------|---------|
| **PAdES** | PDF Advanced Electronic Signature | PDF documents | ETSI EN 319 122 |
| **CAdES** | CMS Advanced Electronic Signature | Binary/arbitrary data | ETSI EN 319 122 |
| **XAdES** | XML Advanced Electronic Signature | XML documents | ETSI EN 319 132 |
| **JAdES** | JSON Advanced Electronic Signature | JSON documents | ETSI TS 119 182 |

**Signature profile levels:**

| Level | Description | What It Contains |
|-------|-------------|-----------------|
| **-B (Basic)** | Baseline signature | Signature + cert + signing time |
| **-T (Timestamp)** | With timestamp | -B + trusted timestamp |
| **-LT (Long-Term)** | Long-term | -T + cert chain + revocation data |
| **-LTA (Long-Term Archive)** | Archive | -LT + additional archive timestamp |

> [!NOTE]
> **PAdES-B-LTA** is the highest level for PDF
> signatures — it includes everything needed
> for validation decades into the future.
> Required for legal archiving in many EU
> jurisdictions under eIDAS.

---

### 4.6 Aadhaar-based e-Sign in DigiLocker

> [!NOTE]
> **DigiLocker** is a cloud-based platform by
> MeitY for storing and sharing official documents
> digitally.

**DigiLocker + e-Sign integration:**
```
Issued documents (marksheets, driving licenses,
Aadhaar cards) are stored as issuer-signed
digital documents in DigiLocker.

Citizens can share these documents with
organizations via DigiLocker APIs — the
issuer's digital signature on the document
proves authenticity.

Citizens can sign consent forms, applications
using e-Sign within DigiLocker —
linking Aadhaar identity to the signature.
```

**DigiLocker is integrated with:**
- CBSE, ICSE (educational certificates)
- Transport Ministry (driving licenses, vehicle RC)
- Income Tax Department
- EPFO (employee provident fund statements)
- Health Ministry (vaccination certificates)

---

### 4.7 Timestamping and Non-Repudiation

> [!NOTE]
> A digital signature alone provides technical
> non-repudiation — but a signer can potentially
> claim:
> - "My certificate was already expired when
>   this was signed — signature is invalid"
> - "My key was compromised before I signed this"
> - "I signed this under duress / I don't
>   remember signing this"

**How timestamping strengthens non-repudiation:**

| Claim | Without Timestamp | With Timestamp |
|-------|------------------|---------------|
| "My cert was expired" | Cannot prove cert was valid at signing time | TST proves exact signing time — cert validity can be checked at that time |
| "My key was compromised before signing" | Hard to disprove | TST + key compromise date — if timestamp before compromise → signature valid |
| "I never signed this" | Only signature itself as evidence | Timestamp + signature + certificate chain = comprehensive audit trail |

> [!IMPORTANT]
> For legally binding digital signatures
> (contracts, court submissions), a trusted
> timestamp (RFC 3161) is considered
> **best practice and sometimes mandatory**
> by regulators.

---

### 4.8 RFC 3161 — TSP Standard Details

> [!NOTE]

| Property | Detail |
|----------|--------|
| **RFC number** | RFC 3161 (2001) — updated by RFC 5816 (2010) |
| **Full title** | Internet X.509 Public Key Infrastructure Time-Stamp Protocol (TSP) |
| **Request format** | TimeStampReq (TSQ) |
| **Response format** | TimeStampResp (TSR) containing TimeStampToken (TST) |
| **Token format** | CMS SignedData (defined in RFC 5652) |
| **Hash algorithm** | Client specifies — SHA-256 recommended |
| **TSA cert EKU** | id-kp-timeStamping (OID 1.3.6.1.5.5.7.3.8) |
| **Nonce** | Optional random integer — client can include to prevent replay |
| **Policy OID** | TSA may have multiple policies with different assurance levels |

**RFC 3161 status codes:**

| Status | Meaning |
|--------|---------|
| **granted (0)** | TST successfully issued |
| **grantedWithMods (1)** | TST issued with modifications |
| **rejection (2)** | Request rejected |
| **waiting (3)** | Request not yet processed |
| **revocationWarning (4)** | Certificate may be revoked soon |
| **revocationNotification (5)** | Certificate has been revoked |

---

### 4.9 Trusted Timestamp Authorities in India

> [!NOTE]

**TSA services in India are provided by:**

| Provider | Type |
|----------|------|
| **eMudhra** | Licensed CA + TSA services |
| **Sify SafeScrypt** | Licensed CA + TSA services |
| **(n)Code Solutions** | Licensed CA + TSA services |
| **CDAC** | Government TSA for government documents |

**Requirements for a TSA:**
- Must have a TSA certificate with `timeStamping`
  EKU from a trusted CA
- Must maintain highly accurate clock synchronized
  to NTP (National Time Protocol) / UTC
- Must be audited for time accuracy
- Time accuracy typically ±1 second or better

> [!NOTE]
> TSA clocks are synchronized to authoritative
> time sources — typically national standards
> laboratories (e.g., National Physical Laboratory
> India, NIST in the US) via NTP hierarchy.
> The accuracy of the TSA's time is critical —
> a TSA with inaccurate clocks cannot provide
> legally reliable timestamps.

---

### 4.10 Aadhaar Biometric Lock

> [!NOTE]
> **Biometric Lock / Unlock** is an Aadhaar
> security feature that allows residents to
> lock their biometric data — preventing it
> from being used for authentication.

```
Biometric LOCKED:
  → Fingerprint and iris authentication DISABLED
  → OTP-based authentication still works
  → Prevents unauthorized biometric use
    (e.g., if someone attempts to use a stolen
     fingerprint at a ration shop)

Biometric UNLOCKED (temporary):
  → Biometric authentication enabled temporarily
  → Auto-locks after a short period
  → Resident controls when biometrics are active
```

**How to lock/unlock:**
- UIDAI mAadhaar app
- UIDAI website
- SMS to UIDAI number

> [!NOTE]
> Biometric lock does NOT affect OTP-based
> authentication — which remains functional.
> For e-Sign using OTP mode, biometric lock
> has no impact.

---

### 4.11 UIDAI Security Architecture

> [!NOTE]

**Key security measures in UIDAI's CIDR:**

| Measure | Description |
|---------|-------------|
| **Biometric data encryption** | All biometric data in CIDR encrypted with AES-256 |
| **Distributed storage** | Biometric and demographic data stored separately |
| **One-way API** | CIDR returns only YES/NO — never raw biometric data |
| **AUA authentication** | All AUAs must authenticate with UIDAI using digital certificates |
| **TLS encryption** | All communication between AUAs/ASAs and CIDR over TLS |
| **Audit logging** | All authentication requests logged |
| **Rate limiting** | AUAs throttled to prevent mass verification attacks |
| **Fraud detection** | UIDAI has fraud analytics to detect unusual patterns |

**Data minimization principle:**
UIDAI's architecture is designed so that:
- AUAs get only YES/NO for basic authentication
- AUAs cannot reconstruct biometric data from responses
- e-KYC data sharing requires explicit consent
- Each authentication has a unique transaction ID

---

### 4.12 Common Misconceptions — Aadhaar
and e-Sign

> [!NOTE]

| Misconception | Correct Understanding |
|--------------|----------------------|
| "e-Sign means the signer holds a private key" | The ESP holds the private key in its HSM — signer authenticates via Aadhaar only |
| "Aadhaar authentication returns biometric data to AUA" | UIDAI returns only YES/NO — biometric data never leaves CIDR |
| "e-Sign and Digital Signature are the same under IT Act" | e-Sign is Electronic Signature; DSC is Digital Signature — different legal categories |
| "A trusted timestamp is just the file creation time" | File timestamps are trivially changeable — trusted timestamps are TSA-signed and cryptographically tamper-proof |
| "A signature on an expired certificate is invalid" | If timestamp proves signing occurred during cert validity → signature is valid despite cert expiry |
| "Aadhaar number must be shared for authentication" | VID can be used instead — protects Aadhaar number privacy |
| "e-Sign works like a normal DSC stored on your phone" | e-Sign generates a new one-time certificate per signing event — no persistent key on user's device |

---

## 5. Abbreviations Table

| Abbreviation | Full Form | One-Line Technical Meaning |
|---|---|---|
| UIDAI | Unique Identification Authority of India | Statutory body that operates Aadhaar and CIDR |
| CIDR | Central Identities Data Repository | UIDAI's central database of all Aadhaar numbers and biometrics |
| AUA | Authentication User Agency | Organization authorized to use Aadhaar authentication |
| ASA | Authentication Service Agency | Technical intermediary connecting AUAs to UIDAI CIDR |
| KUA | KYC User Agency | Organization authorized to receive e-KYC data from UIDAI |
| ESP | e-Sign Service Provider | CCA-licensed entity that issues one-time certificates for e-Sign |
| ASP | Application Service Provider | Application/portal where the user initiates e-Sign |
| VID | Virtual ID | Temporary 16-digit privacy-preserving proxy for Aadhaar number |
| TSP | Time Stamp Protocol | RFC 3161 protocol for requesting and issuing trusted timestamps |
| TSA | Time Stamp Authority | Trusted third party that issues cryptographically signed timestamps |
| TST | Time Stamp Token | Signed cryptographic object containing hash + time + TSA signature |
| TSQ | Time Stamp Request | Client's request to TSA containing hash and optional nonce |
| TSR | Time Stamp Response | TSA's response containing status code and TST |
| LTV | Long-Term Validation | Embedding cert chain + revocation + timestamp in signature for future validation |
| PAdES | PDF Advanced Electronic Signature | Advanced signature format for PDF documents — ETSI standard |
| CAdES | CMS Advanced Electronic Signature | Advanced signature format for arbitrary binary data |
| XAdES | XML Advanced Electronic Signature | Advanced signature format for XML documents |
| e-KYC | Electronic Know Your Customer | Aadhaar-based digital identity verification for financial services |
| OTP | One-Time Password | Single-use authentication code sent to registered mobile |
| NTP | Network Time Protocol | Protocol for synchronizing clocks to authoritative time sources |
| MeitY | Ministry of Electronics and Information Technology | Indian government ministry overseeing IT policy |
| DSC | Digital Signature Certificate | Physical USB token-based certificate issued by CCA-licensed CAs in India |
| CMS | Cryptographic Message Syntax | Standard format for signed and encrypted data (RFC 5652) |
| UTC | Coordinated Universal Time | Global standard time reference — used in TST genTime field |
| DBT | Direct Benefit Transfer | Government scheme transferring subsidies directly using Aadhaar |

---

## 6. Keywords + Concept Map

| Term | Definition | Connections | Use Cases |
|------|-----------|-------------|-----------|
| **Aadhaar** | India's 12-digit biometric identity — UIDAI | CIDR, AUA, e-KYC, e-Sign, VID | Identity verification, government services |
| **CIDR** | UIDAI's central biometric database | Encrypted, returns YES/NO only | Foundation of all Aadhaar services |
| **e-Sign** | Aadhaar-authenticated electronic signature | ESP, one-time DSC, HSM, IT Act | Tax filing, bank KYC, government forms |
| **ESP** | Provides e-Sign service — issues one-time certs | CCA-licensed, HSM, CA | e-Sign infrastructure |
| **Trusted Timestamp** | TSA-signed proof of data existence at a time | RFC 3161, TST, TSA cert, non-repudiation | Legal documents, code signing |
| **TSA** | Time Stamp Authority — trusted third party | RFC 3161, NTP, timeStamping EKU | Timestamp issuance |
| **TST** | Signed token containing hash + time + signature | CMS SignedData, genTime, serialNumber | Embedded in signed documents |
| **VID** | 16-digit temporary Aadhaar proxy | Privacy, revocable, UIDAI maps to Aadhaar | Privacy-preserving Aadhaar use |
| **LTV** | Long-term validation — all evidence embedded | PAdES-LTV, cert chain, OCSP, timestamp | Legal archiving of signatures |
| **PAdES** | Advanced PDF signature format | ETSI, -B/-T/-LT/-LTA levels | Legal PDF documents |
| **e-KYC** | Aadhaar-based digital KYC | UIDAI, KUA, consent | Bank/telecom onboarding |
| **AUA** | Organization using Aadhaar authentication | Authorized by UIDAI, ASA, CIDR | Banks, telecom, govt depts |

---

## 7. Quick Reference Cheatsheet

### 🔸 Aadhaar Quick Facts

| Property | Value |
|----------|-------|
| Issuer | UIDAI |
| Number length | 12 digits |
| VID length | 16 digits |
| Biometrics enrolled | 10 fingerprints + 2 iris + photo |
| Legal basis | Aadhaar Act 2016 |
| Authentication result | YES / NO only (basic) |
| e-KYC result | Demographic data (with consent) |

---

### 🔸 e-Sign vs Physical DSC

| | e-Sign | Physical DSC |
|---|--------|-------------|
| Token | None | USB token |
| Key location | ESP HSM | USB token |
| Issuance | Seconds | Days |
| Cost | Per-use ~₹20-50 | One-time ~₹500-2000 |
| Mobile | ✅ Yes | ❌ No |
| Validity | One-time | 1-3 years |

---

### 🔸 e-Sign Workflow Summary

```
User clicks Sign → ASP sends hash to ESP →
ESP requests Aadhaar auth → User provides OTP/biometric →
UIDAI returns YES → ESP issues one-time cert →
ESP signs hash → Returns signature to ASP →
ASP embeds in document → Key destroyed ✅
```

---

### 🔸 TSP (RFC 3161) Flow

```
Client: Hash(doc) → TimeStampRequest (TSQ)
TSA:    Receives TSQ → Records UTC time →
        Signs (Hash + Time) → TimeStampToken (TST)
Client: Receives TSR → Verifies TSA signature →
        Stores TST with document ✅
```

---

### 🔸 Signature Profile Levels

| Level | Contains |
|-------|---------|
| -B | Signature + cert |
| -T | -B + trusted timestamp |
| -LT | -T + cert chain + revocation data |
| -LTA | -LT + archive timestamp |

---

### 🔸 e-Sign Legal Exclusions (IT Act)

Cannot use e-Sign / DSC for:
- Negotiable instruments (cheques)
- Powers of attorney
- Trust deeds
- Wills
- Sale of immovable property
- Documents requiring Registration Act registration

---

### 🔸 Key RFC References

| RFC | Subject |
|-----|---------|
| RFC 3161 | Time Stamp Protocol (TSP) |
| RFC 5816 | Update to RFC 3161 |
| RFC 5652 | CMS — Cryptographic Message Syntax |
| RFC 8555 | ACME (for context) |

---

## 8. Session Revision Snapshot

### ⚡ TL;DR — 5 Bullets

- ✅ Aadhaar is India's biometric identity (UIDAI,
  12-digit number, 1.4B enrolled) — authentication
  returns YES/NO only — CIDR never exposes biometric
  data to AUAs — VID (16-digit) is a privacy-
  preserving temporary proxy for the Aadhaar number
- ✅ e-Sign is an Aadhaar-based electronic signature
  service — the signer authenticates via Aadhaar
  OTP/biometric — ESP issues a one-time DSC from
  its HSM — only the document hash is sent to ESP —
  private key is created and destroyed in ESP's HSM
- ✅ e-Sign vs physical DSC: e-Sign has no USB token,
  works on mobile, issued in seconds, costs per use;
  physical DSC has USB token, takes days to issue,
  costs one-time but valid for 1-3 years; both
  legally valid under IT Act 2000
- ✅ Trusted timestamping (RFC 3161) — client sends
  hash to TSA — TSA returns signed Time Stamp Token
  (TST) containing hash + UTC time + TSA signature —
  proves data existed at that time — essential for
  long-lived signature validity and non-repudiation
- ✅ LTV (Long-Term Validation) embeds the cert chain,
  revocation data, and timestamp in the document at
  signing time — enabling future validation without
  any external queries — PAdES-LTV is the standard
  for legally archivable PDF signatures

---

### 🎯 MCQ-Likely Concepts — Everything Examiners Love

| Concept | Why It's Tricky |
|---------|----------------|
| UIDAI returns only YES/NO for authentication | Many think it returns demographic data for all auth |
| e-Sign private key is in ESP's HSM — not with signer | Key insight — signer never holds the private key |
| Only HASH is sent to ESP — not the document | Document confidentiality protection mechanism |
| e-Sign = Electronic Signature; DSC = Digital Signature | Different legal categories under IT Act |
| TSA returns signed TST — not just a time value | The signature on the TST is what makes it trusted |
| RFC 3161 = Time Stamp Protocol | RFC number tested |
| TST contains hash + genTime + TSA signature | Specific TST content — all three elements |
| VID is 16 digits (Aadhaar is 12) | Specific lengths tested |
| VID protects Aadhaar number privacy — revocable | Purpose and key property |
| LTV = embed chain + revocation + timestamp at signing | Three things that must be embedded |
| PAdES-LTA = highest PDF signature level | Specific level for archive quality |
| Biometric lock disables biometric — OTP still works | Partial lock — not complete lockout |
| e-Sign certificate is one-time only — destroyed after | No persistent key on user device |
| TSA EKU = timeStamping (OID 1.3.6.1.5.5.7.3.8) | Specific EKU for TSA certificate |
| e-Sign cannot be used for wills, property sale | IT Act exclusions |
| Aadhaar Act 2016 + Supreme Court 2018 ruling | Year and outcome |
| UIDAI under MeitY | Ministry relationship |

---

<details>
<summary>🔬 Lab — Session 09 (XCA Tool)</summary>

**Lab file:** `3-Labs/lab-session-09-xca-signing.md`

**Tool:** XCA (X Certificate and Key Management)

**Lab Tasks:**
1. Create a CA certificate using XCA
2. Issue an end-entity certificate from that CA
3. Digitally sign a Word document using the
   created certificate
4. Digitally sign a PDF document using the
   created certificate

**Theory ↔ Lab Connection:**

| Session 09 Theory Concept | XCA Lab Demonstration |
|--------------------------|----------------------|
| Digital certificate structure (X.509 v3) | XCA shows all cert fields in GUI |
| CA issuing an end-entity cert | Create Root CA in XCA → issue cert from it |
| Certificate chain | Issued cert references the CA cert |
| Self-signed vs CA-signed | Root CA in XCA is self-signed |
| Private key management | XCA stores private keys in encrypted database |
| Signing a document with a certificate | Word/PDF signing with exported certificate |

> [!NOTE]
> The e-Sign workflow covered in this session
> (Aadhaar OTP → ESP issues cert → signs hash)
> is conceptually demonstrated by XCA's manual
> process — except XCA uses a pre-existing cert
> (not a one-time ESP-generated cert).
> The lab shows the mechanics of certificate-based
> document signing that underlies e-Sign's operation.

**Full step-by-step lab guide:**
`3-Labs/lab-session-09-xca-signing.md`

</details>

---