# Session 08 — CA, Trust Models, Certificate Issuance,
Revocation & Types of Certificates

## 📑 Table of Contents

- [1. Certificate Authority (CA)](#1-certificate-authority-ca)
  - [1.1 What is a CA?](#11-what-is-a-ca)
  - [1.2 CA Responsibilities](#12-ca-responsibilities)
  - [1.3 CA Hierarchy — Root, Intermediate,
    Issuing](#13-ca-hierarchy--root-intermediate-issuing)
  - [1.4 CA Key Protection](#14-ca-key-protection)
  - [1.5 CA/Browser Forum](#15-cabrowser-forum)
  - [1.6 Real-World CAs](#16-real-world-cas)
- [2. Trust Models](#2-trust-models)
  - [2.1 Hierarchical Trust Model — Deep Dive](#21-hierarchical-trust-model--deep-dive)
  - [2.2 Web of Trust — Deep Dive](#22-web-of-trust--deep-dive)
  - [2.3 Cross-Certification Model](#23-cross-certification-model)
  - [2.4 Bridge CA Model](#24-bridge-ca-model)
  - [2.5 Trust Store](#25-trust-store)
- [3. Certificate Issuance Process](#3-certificate-issuance-process)
  - [3.1 Certificate Lifecycle](#31-certificate-lifecycle)
  - [3.2 Domain Validation (DV)](#32-domain-validation-dv)
  - [3.3 Organization Validation (OV)](#33-organization-validation-ov)
  - [3.4 Extended Validation (EV)](#34-extended-validation-ev)
  - [3.5 DV vs OV vs EV — Full Comparison](#35-dv-vs-ov-vs-ev--full-comparison)
  - [3.6 Automated Certificate Issuance — ACME](#36-automated-certificate-issuance--acme)
- [4. Certificate Revocation](#4-certificate-revocation)
  - [4.1 Why Certificates Are Revoked](#41-why-certificates-are-revoked)
  - [4.2 CRL — Certificate Revocation List](#42-crl--certificate-revocation-list)
  - [4.3 OCSP — Online Certificate Status
    Protocol](#43-ocsp--online-certificate-status-protocol)
  - [4.4 OCSP Stapling](#44-ocsp-stapling)
  - [4.5 CRL vs OCSP vs OCSP Stapling](#45-crl-vs-ocsp-vs-ocsp-stapling)
  - [4.6 Revocation Challenges](#46-revocation-challenges)
- [5. Types and Classes of Certificates](#5-types-and-classes-of-certificates)
  - [5.1 By Validation Level](#51-by-validation-level)
  - [5.2 By Purpose / Use Case](#52-by-purpose--use-case)
  - [5.3 By Subject Type](#53-by-subject-type)
  - [5.4 Special Certificate Types](#54-special-certificate-types)
- [6. 📌 Extra Notes](#6--extra-notes)
  - [6.1 CRL Distribution Points (CDP)](#61-crl-distribution-points-cdp)
  - [6.2 Delta CRL](#62-delta-crl)
  - [6.3 OCSP Must-Staple](#63-ocsp-must-staple)
  - [6.4 Soft Fail vs Hard Fail Revocation](#64-soft-fail-vs-hard-fail-revocation)
  - [6.5 CA Compromise — Real Examples](#65-ca-compromise--real-examples)
  - [6.6 Certificate Pinning vs CT vs OCSP —
    Comparison](#66-certificate-pinning-vs-ct-vs-ocsp--comparison)
  - [6.7 Private PKI vs Public PKI](#67-private-pki-vs-public-pki)
  - [6.8 Let's Encrypt — Free Automated CA](#68-lets-encrypt--free-automated-ca)
  - [6.9 Multi-Domain and Wildcard Certificates](#69-multi-domain-and-wildcard-certificates)
  - [6.10 Certificate Validity Periods —
    History and Current Limits](#610-certificate-validity-periods--history-and-current-limits)
  - [6.11 Qualified Certificates and eIDAS](#611-qualified-certificates-and-eidas)
  - [6.12 India PKI — Controller of Certifying
    Authorities](#612-india-pki--controller-of-certifying-authorities)
- [7. Abbreviations Table](#7-abbreviations-table)
- [8. Keywords + Concept Map](#8-keywords--concept-map)
- [9. Quick Reference Cheatsheet](#9-quick-reference-cheatsheet)
- [10. Session Revision Snapshot](#10-session-revision-snapshot)

---

## 1. Certificate Authority (CA)

### 1.1 What is a CA?

A **Certificate Authority (CA)** is a trusted
entity that issues digital certificates — binding
a public key to a verified identity and digitally
signing that binding with its own private key.

The CA is the cornerstone of PKI.
Without a CA, there is no trusted mechanism to
verify who owns a public key.

> [!IMPORTANT]
> The entire security of PKI rests on trusting the CA.
> If a CA is compromised, all certificates it issued
> become suspect — this is why CA security is
> treated with extreme care.
>
> A CA's value is its **trustworthiness** — earned
> through rigorous audits, secure operations, and
> compliance with industry standards (CA/Browser
> Forum Baseline Requirements).

---

### 1.2 CA Responsibilities

| Responsibility | Description |
|----------------|-------------|
| **Identity Verification** | Verify the identity of certificate applicants before issuing |
| **Certificate Issuance** | Sign and issue X.509 certificates |
| **Certificate Renewal** | Re-issue certificates before expiry |
| **Certificate Revocation** | Invalidate certificates before expiry when needed |
| **CRL Publication** | Publish and maintain Certificate Revocation Lists |
| **OCSP Responses** | Respond to real-time certificate status queries |
| **Repository Maintenance** | Maintain public directory of issued certificates |
| **Key Management** | Securely manage CA private keys (HSM, air-gapped storage) |
| **Audit Compliance** | Submit to annual third-party audits (WebTrust, ETSI) |
| **CPS Publication** | Publish Certification Practice Statement |

---

### 1.3 CA Hierarchy — Root, Intermediate, Issuing

**Three-tier hierarchy (most common in enterprise):**

```
Root CA (Tier 1)
│  → Self-signed certificate
│  → Highest trust level
│  → Private key OFFLINE (air-gapped HSM)
│  → Only used to sign Intermediate CA certs
│  → Certificate validity: 20–40 years
│
├── Intermediate CA (Tier 2) — also called Sub CA
│   │  → Signed by Root CA
│   │  → Private key in ONLINE HSM
│   │  → Issues end-entity certificates (or more Intermediates)
│   │  → Certificate validity: 5–10 years
│   │
│   └── Issuing CA (Tier 3) — optional additional layer
│         → Signed by Intermediate CA
│         → Issues end-entity certs for specific purposes
│         → Certificate validity: 3–5 years

End-Entity Certificates
│  → Signed by Issuing CA (or Intermediate CA)
│  → Installed on servers, devices, or used by people
│  → Certificate validity: 1–2 years (currently)
```

**Why Intermediate CAs exist:**

| Reason | Explanation |
|--------|-------------|
| **Security** | Root CA private key stays offline — minimizes exposure |
| **Compartmentalization** | If Intermediate CA is compromised, only its certs are revoked |
| **Operational efficiency** | Intermediate CA handles high-volume daily issuance |
| **Policy separation** | Different Intermediate CAs for different certificate types |
| **Geographic distribution** | Different Intermediate CAs per region |

> [!IMPORTANT]
> A key design principle:
> **The blast radius of a compromise is contained
> at the level where it occurs.**
>
> Intermediate CA compromise → Root CA revokes
> Intermediate CA certificate → all certs from that
> Intermediate CA are invalidated — but Root CA
> and other Intermediate CAs remain trusted.
>
> Root CA compromise → catastrophic → the entire
> CA is removed from trust stores → all certificates
> from that CA hierarchy become untrusted.

---

### 1.4 CA Key Protection

CA private keys are the most sensitive cryptographic
material in the PKI ecosystem.

**Root CA key protection:**

| Measure | Description |
|---------|-------------|
| **Hardware Security Module (HSM)** | Private key generated and stored in tamper-resistant hardware |
| **Air-gapped storage** | Root CA is kept offline — no network connection |
| **Dual control** | Two or more authorized personnel required to access key |
| **M-of-N key recovery** | Key split across N custodians — M required to reconstruct |
| **Physical security** | CA facilities in secure data centers with biometric access |
| **Ceremony** | Key generation performed as a formal "key ceremony" with witnesses and video |

**Intermediate CA key protection:**

| Measure | Description |
|---------|-------------|
| **Online HSM** | Key stored in HSM — accessible to CA software but not exportable |
| **FIPS 140-2 Level 3 HSM** | Industry standard for CA key protection |
| **Audit logging** | All signing operations logged |
| **Network segmentation** | CA system isolated from public internet |

> [!NOTE]
> **Key Ceremony:**
> When a Root CA is set up, the private key
> generation is performed as a formal ceremony —
> documented, witnessed by internal and external
> auditors, recorded on video, and archived.
> This creates an auditable record proving the key
> was properly generated and handled from day one.

---

### 1.5 CA/Browser Forum

The **CA/Browser Forum (CABF)** is a voluntary
consortium of CAs and browser/OS vendors that
establishes minimum standards for certificate
issuance and management.

| Property | Detail |
|----------|--------|
| **Founded** | 2005 |
| **Members** | CAs (DigiCert, Sectigo, Let's Encrypt) + Browser vendors (Google, Mozilla, Apple, Microsoft) |
| **Key documents** | Baseline Requirements (BR), Extended Validation Guidelines |
| **Enforcement** | Browser vendors enforce compliance — non-compliant CAs removed from trust stores |
| **Website** | cabforum.org |

**Key CA/Browser Forum requirements:**
- Maximum certificate validity: **398 days** (since
  September 2020)
- Domain validation methods must be from approved
  list (CAA records, HTTP challenge, DNS challenge)
- EV guidelines specify strict identity verification
- CT logs required for all publicly trusted certs

> [!IMPORTANT]
> The CA/Browser Forum's Baseline Requirements
> are not optional for publicly trusted CAs.
> Browser vendors will distrust CAs that violate
> these requirements — as demonstrated when Google
> distrusted Symantec CA in 2018 after repeated
> mis-issuances.

---

### 1.6 Real-World CAs

**Major publicly trusted commercial CAs:**

| CA | Owner | Market Notes |
|----|-------|-------------|
| **DigiCert** | DigiCert Inc | Largest CA by volume — acquired Symantec CA business |
| **Sectigo** | Sectigo Ltd | Formerly Comodo CA — very large volume |
| **GlobalSign** | GMO Internet | Strong in enterprise |
| **Entrust** | Entrust Corp | Strong in government/enterprise |
| **Let's Encrypt** | ISRG (non-profit) | Free DV certs — largest by # of certs issued |
| **Google Trust Services** | Google | Issues certs for Google services |
| **Amazon Trust Services** | Amazon | Issues certs for AWS services |

**India-specific CAs (licensed by CCA):**

| CA | Notes |
|----|-------|
| **eMudhra** | Licensed by CCA — issues DSC in India |
| **(n)Code Solutions** | GNFC subsidiary — licensed CA |
| **SafeScrypt** | Sify subsidiary — licensed CA |
| **CDAC** | Government CA for government use |

> [!NOTE]
> India's **Controller of Certifying Authorities
> (CCA)** under the IT Act 2000 licenses and
> regulates CAs in India. These are called
> **Certifying Authorities (CAs)** in Indian
> legal terminology and issue **Digital Signature
> Certificates (DSCs)** used for e-filing,
> e-tendering, and other government services.
> Covered in detail in Session 14.

---

## 2. Trust Models

### 2.1 Hierarchical Trust Model — Deep Dive

The hierarchical trust model forms a tree structure
with the Root CA at the top.

**Trust establishment:**
```
Browser/OS ships with pre-installed Root CA certs
           ↓
Browser trusts anything signed (directly or
transitively) by a trusted Root CA
           ↓
Intermediate CA cert signed by Root CA
→ Intermediate CA is trusted
           ↓
End-entity cert signed by Intermediate CA
→ End-entity cert is trusted
           ↓
User sees no security warning — connection secure ✅
```

**Chain length:**
```
Minimum:  Root CA → End Entity (2 certs, rare)
Typical:  Root CA → Intermediate CA → End Entity (3 certs)
Extended: Root CA → Int CA 1 → Int CA 2 → End Entity (4 certs)
```

**Path Length Constraint (Basic Constraints extension):**
- `pathLenConstraint = 0` → This CA can only sign
  end-entity certs (not other CAs)
- `pathLenConstraint = 1` → This CA can sign one
  more level of CA certs below it
- No constraint → No limit on chain depth

**Advantages of hierarchical model:**

| Advantage | Detail |
|-----------|--------|
| Scalable | Works for billions of certificates globally |
| Clear accountability | Each cert traceable to a responsible CA |
| Revocation manageable | Revoke at the right level |
| Browser compatibility | Universally supported |

---

### 2.2 Web of Trust — Deep Dive

**Web of Trust (WoT)** is the decentralized trust
model used by PGP/GPG — no central CA.

**How it works:**
```
Alice generates her PGP key pair
Alice uploads public key to a keyserver

Bob signs Alice's public key — "I've verified
Alice's identity and this is her key"

Carol trusts Bob → Carol can transitively trust
Alice's key (through Bob's endorsement)
```

**Trust levels in PGP Web of Trust:**

| Trust Level | Meaning |
|-------------|---------|
| **Unknown** | No information about this key |
| **None** | Explicitly do not trust this key owner to verify others |
| **Marginal** | Partially trust — need multiple marginal trusts to validate |
| **Full** | Fully trust this key owner to verify others' keys |
| **Ultimate** | Complete trust — your own keys |

**PGP trust calculation:**
- **1 full trust** OR **3 marginal trusts** from
  trusted parties = key is considered valid

**Advantages vs disadvantages:**

| | Web of Trust | Hierarchical PKI |
|---|------------|-----------------|
| **Centralization** | None | Root CA is central |
| **Single point of failure** | None | Root CA compromise |
| **Scalability** | Poor | Excellent |
| **Ease of use** | Complex | Simple (automatic) |
| **Identity verification** | Community-based | CA-standardized |

---

### 2.3 Cross-Certification Model

**Cross-certification** allows two separate PKI
hierarchies to trust each other by signing each
other's CA certificates.

```
Organization A PKI:          Organization B PKI:
   Root CA-A                    Root CA-B
      │                            │
  Signs cert                   Signs cert
      │                            │
  for Root CA-B               for Root CA-A
      ↓                            ↓
  Now entities under A         Now entities under B
  trust entities under B       trust entities under A
```

**Use cases:**
- Two organizations merging (before full PKI
  consolidation)
- Government agencies establishing inter-agency trust
- International PKI interoperability

**Challenge:**
- Cross-certification creates complex trust webs
  that are difficult to manage and audit
- Revoking a cross-certification affects all
  entities that relied on it

---

### 2.4 Bridge CA Model

A **Bridge CA** acts as a central hub for connecting
multiple PKI hierarchies — each hierarchy establishes
cross-certification with the Bridge CA rather than
with every other hierarchy directly.

```
PKI Hierarchy A ←→ Bridge CA ←→ PKI Hierarchy B
                        ↕
                 PKI Hierarchy C
                        ↕
                 PKI Hierarchy D
```

**Without Bridge CA:**
- N hierarchies need N×(N-1)/2 cross-certifications
  (similar to symmetric key problem)

**With Bridge CA:**
- N hierarchies need only N cross-certifications
  (one each to the Bridge CA)

**Real example:**
- **US Federal PKI** — the Federal Bridge CA
  connects multiple federal agency PKIs, allowing
  government employees across agencies to trust
  each other's certificates

---

### 2.5 Trust Store

A **trust store** (also called a **root store** or
**certificate store**) is a pre-installed collection
of trusted Root CA certificates on an operating
system or browser.

**Trust store locations:**

| Platform | Trust Store Location |
|----------|---------------------|
| **Windows** | Windows Certificate Store — managed via MMC/certmgr |
| **macOS/iOS** | System Keychain — managed via Keychain Access |
| **Linux** | `/etc/ssl/certs/` — managed by ca-certificates package |
| **Firefox** | NSS (Network Security Services) — independent from OS |
| **Chrome** | Uses OS trust store (Windows/macOS) or NSS (Linux) |
| **Java** | `$JAVA_HOME/lib/security/cacerts` — JDK trust store |

**Who controls the trust stores:**

| Vendor | Trust Store | Notes |
|--------|------------|-------|
| **Google** | Chrome Root Store (since 2022) | Independent from OS — own root store |
| **Mozilla** | Mozilla Root Store | Independent — also used by Firefox on all OS |
| **Apple** | Apple Root Store | Used by Safari, macOS, iOS |
| **Microsoft** | Microsoft Root Store | Used by Windows, IE, Edge (legacy) |

> [!IMPORTANT]
> Being included in browser trust stores is
> critical for commercial CAs.
> Inclusion requires passing annual audits
> (WebTrust for CAs, ETSI EN 319 411)
> and complying with CA/Browser Forum requirements.
>
> **Removal from trust stores = instant death for a CA.**
> DigiNotar (2011) and Symantec (2018) were removed
> after repeated trust violations — making all their
> certificates immediately untrusted by browsers.

---

## 3. Certificate Issuance Process

### 3.1 Certificate Lifecycle

```
GENERATION → ISSUANCE → USE → RENEWAL → EXPIRY / REVOCATION
     │            │        │       │
  Key pair    Identity   Install  Before   Certificate
  created    verified  on server  expiry   invalid
  + CSR      by CA
  created
```

**Phases in detail:**

| Phase | Actor | Action |
|-------|-------|--------|
| **Key Generation** | End Entity | Generate key pair — private key stays with entity |
| **CSR Creation** | End Entity | Create PKCS#10 CSR with public key + identity |
| **Submission** | End Entity → RA/CA | Submit CSR to CA (via web portal, API, ACME) |
| **Identity Verification** | RA/CA | Verify domain control, organization, or extended identity |
| **Certificate Issuance** | CA | Sign X.509 certificate with CA private key |
| **Delivery** | CA → End Entity | Certificate returned to applicant |
| **Installation** | End Entity | Install on server/device |
| **Use** | End Entity | Certificate presented in TLS handshakes etc. |
| **Renewal** | End Entity | Request new certificate before current one expires |
| **Revocation** | End Entity or CA | Invalidate certificate before expiry if needed |

---

### 3.2 Domain Validation (DV)

**DV certificates** verify only that the applicant
controls the domain — no identity verification.

**Validation methods (CA/Browser Forum approved):**

| Method | How It Works |
|--------|-------------|
| **HTTP/HTTPS file challenge** | CA instructs applicant to place a specific token file at a specific URL on the domain — CA retrieves and verifies |
| **DNS TXT record** | CA instructs applicant to add a specific TXT record to the domain's DNS — CA queries and verifies |
| **Email to domain contacts** | CA sends verification email to admin@, hostmaster@, postmaster@, webmaster@, etc. — applicant clicks link |
| **CAA record check** | Certificate Authority Authorization DNS record — declares which CAs may issue for the domain |

**DV certificate characteristics:**

| Property | Value |
|----------|-------|
| **Verification** | Domain control only |
| **Issuance time** | Minutes to hours (automated) |
| **Information in cert** | Domain name only — no organization name |
| **Cost** | Free (Let's Encrypt) to low-cost commercial |
| **Use case** | Personal sites, small businesses, internal tools |
| **Browser indicator** | Padlock — no green bar (green bar was EV, now removed in modern browsers) |

---

### 3.3 Organization Validation (OV)

**OV certificates** verify both domain control and
the legal existence of the requesting organization.

**Verification steps:**

| Step | What CA Checks |
|------|---------------|
| Domain control | Same as DV |
| Organization name | Verified against official records (company registration, government databases) |
| Organization address | Verified against official records |
| Phone number | CA may call a verified number to confirm |
| Authorized representative | Confirms person requesting cert has authority |

**OV certificate characteristics:**

| Property | Value |
|----------|-------|
| **Verification** | Domain + Organization identity |
| **Issuance time** | Hours to days |
| **Information in cert** | Organization name included in Subject field |
| **Cost** | Higher than DV |
| **Use case** | Business websites, customer-facing applications |

---

### 3.4 Extended Validation (EV)

**EV certificates** involve the most thorough
identity verification — defined by CA/Browser Forum
EV Guidelines.

**EV verification requirements:**

| Requirement | Detail |
|-------------|--------|
| **Legal existence** | Verified organization incorporation documents |
| **Physical address** | Verified official address |
| **Operational existence** | Business has been operating for ≥ 3 years (or equivalent checks) |
| **Authority to request** | Individual authorized to bind the organization |
| **Domain control** | Same as DV |
| **EV contract** | Subscriber Agreement signed |

**EV certificate characteristics:**

| Property | Value |
|----------|-------|
| **Verification** | Most thorough — full legal identity |
| **Issuance time** | Days to weeks |
| **Information in cert** | Full organization name, jurisdiction, registration number |
| **Cost** | Most expensive |
| **Use case** | Banks, financial institutions, e-commerce |
| **Browser indicator** | Previously showed green address bar with org name — removed by Chrome (2019) and Firefox (2019) |

> [!IMPORTANT]
> **EV green bar removal (2019):**
> Chrome and Firefox removed the EV green address
> bar in 2019 — research showed users did not notice
> it and it provided limited security benefit.
> EV certificates still contain more verified
> information — the enhanced verification process
> remains — but the visual indicator changed.
>
> Modern browsers show a padlock for all valid HTTPS
> connections regardless of DV/OV/EV.
> To see if a cert is EV, users must click the
> padlock and examine the certificate details.

---

### 3.5 DV vs OV vs EV — Full Comparison

| Property | DV | OV | EV |
|----------|----|----|-----|
| **Verifies** | Domain control | Domain + Organization | Domain + Full legal identity |
| **Issuance time** | Minutes | Hours–Days | Days–Weeks |
| **Subject contains** | Domain name | Domain + Org name | Domain + Org + Jurisdiction + Reg# |
| **Cost** | Free – Low | Medium | High |
| **Browser indicator** | Padlock | Padlock | Padlock (was green bar, removed 2019) |
| **Typical use** | Personal sites, blogs | Business sites | Banks, financial, large e-commerce |
| **Identity in cert** | None (domain only) | Organization name | Full verified legal identity |
| **CA/BF requirement** | Baseline Requirements | Baseline Requirements | EV Guidelines |

---

### 3.6 Automated Certificate Issuance — ACME

**ACME (Automatic Certificate Management
Environment)** is a protocol that automates the
certificate issuance and renewal process.

| Property | Detail |
|----------|--------|
| **Protocol** | ACME |
| **Standard** | RFC 8555 (2019) |
| **Used by** | Let's Encrypt — primary implementation |
| **Client tools** | Certbot (EFF), acme.sh, win-acme |
| **Automation** | Fully automated DV cert issuance and renewal |
| **Challenge types** | HTTP-01, DNS-01, TLS-ALPN-01 |

**ACME workflow:**
```
1. Client requests certificate from CA (Let's Encrypt)
2. CA issues a challenge (HTTP-01 or DNS-01)
3. Client proves domain control by completing challenge
4. CA verifies the challenge
5. CA issues certificate
6. Client installs certificate
7. Client renews automatically before expiry
   (Let's Encrypt certs valid for 90 days —
    renewal recommended at 60 days)
```

> [!NOTE]
> **Why Let's Encrypt certs are 90 days:**
> Short validity encourages automation, reduces
> the window of exposure for compromised certs,
> and reduces reliance on revocation mechanisms.
> The intent is that certificates are always
> renewed before expiry — eliminating manual renewal.

---

## 4. Certificate Revocation

### 4.1 Why Certificates Are Revoked

A certificate should be revoked before its expiry
when it is no longer trustworthy.

**Reasons for revocation:**

| Reason | Description |
|--------|-------------|
| **Private key compromise** | The private key corresponding to the certificate was stolen, leaked, or exposed |
| **CA compromise** | The issuing CA's private key was compromised |
| **Affiliation change** | The certificate holder is no longer affiliated with the organization in the cert |
| **Certificate superseded** | A new certificate replaces the current one |
| **Cessation of operation** | The organization or service has shut down |
| **Privilege withdrawn** | The certificate holder's authorization to hold the cert was revoked |
| **Incorrect information** | The certificate was found to contain incorrect information |
| **Key generation weakness** | The key was found to be weak (e.g., Debian OpenSSL bug) |

> [!IMPORTANT]
> The most critical revocation reason is
> **private key compromise** — if an attacker has
> the private key, they can impersonate the cert
> holder until the certificate expires.
> Immediate revocation is essential in this case.

---

### 4.2 CRL — Certificate Revocation List

A **CRL (Certificate Revocation List)** is a
digitally signed file published by a CA that lists
the serial numbers of all revoked certificates
that have not yet expired.

**CRL structure:**

```
CRL (Signed by CA):
  Version
  Signature Algorithm
  Issuer (the CA that issued this CRL)
  This Update (when this CRL was issued)
  Next Update (when the next CRL will be issued)
  Revoked Certificates:
    Serial Number: 0x7A4F2C8D1B
    Revocation Date: 2024-03-15
    Reason Code: keyCompromise
    ─────────────────────
    Serial Number: 0x3E91B6F2A7
    Revocation Date: 2024-02-01
    Reason Code: affiliationChanged
    ...
  CA Digital Signature
```

**CRL revocation reason codes:**

| Code | Meaning |
|------|---------|
| 0 | Unspecified |
| 1 | keyCompromise |
| 2 | cACompromise |
| 3 | affiliationChanged |
| 4 | superseded |
| 5 | cessationOfOperation |
| 6 | certificateHold (temporary — can be unrevoked) |
| 8 | removeFromCRL (used in Delta CRLs) |
| 9 | privilegeWithdrawn |
| 10 | aACompromise |

**CRL operation:**

```
CA publishes CRL at a URL (CDP — CRL Distribution Point)
Client downloads CRL periodically
Client checks if cert serial number is in the CRL
  → Found in CRL → Certificate revoked → Reject
  → Not found → Certificate valid (as far as CRL shows)
```

**CRL properties:**

| Property | Value |
|----------|-------|
| **Published by** | CA |
| **Update frequency** | Daily to weekly (CA-defined) |
| **Format** | Signed ASN.1 DER/PEM file |
| **Distribution** | HTTP or LDAP URL in CDP extension |
| **Size issue** | Grows over time — large CAs have multi-MB CRLs |
| **Latency** | Revocation not immediate — depends on CRL update frequency |

---

### 4.3 OCSP — Online Certificate Status Protocol

**OCSP (Online Certificate Status Protocol)** is
a real-time protocol for checking the revocation
status of a specific certificate.

**Standard:** RFC 6960 (2013)
**Predecessor:** RFC 2560 (1999) — original OCSP

**OCSP operation:**

```
Step 1: Client needs to check cert for example.com

Step 2: Client sends OCSP Request to OCSP responder
  Request contains:
    - Issuing CA's name (hash)
    - Certificate serial number (hash)
    - Nonce (optional — prevents replay)

Step 3: OCSP Responder (VA) checks its database

Step 4: OCSP Responder sends signed OCSP Response:
  Response contains:
    - Certificate status: GOOD / REVOKED / UNKNOWN
    - This Update / Next Update timestamps
    - If REVOKED: revocation time + reason
    - OCSP Responder's digital signature
```

**OCSP response status values:**

| Status | Meaning |
|--------|---------|
| **GOOD** | Certificate is not revoked |
| **REVOKED** | Certificate has been revoked (with reason and time) |
| **UNKNOWN** | OCSP responder has no information about this certificate |

> [!NOTE]
> OCSP responders are typically operated by the CA
> or by a Validation Authority (VA) on behalf of
> the CA. The OCSP responder URL is in the
> **Authority Information Access (AIA)** extension
> of the certificate.

**OCSP privacy concern:**
Standard OCSP requires the client to query the
OCSP responder for each certificate it encounters.
This means the CA (OCSP responder) can track:
- Which websites users are visiting
- How frequently
- From which IP addresses

This is a significant privacy concern — addressed
by OCSP Stapling.

---

### 4.4 OCSP Stapling

**OCSP Stapling** (formally called TLS Certificate
Status Request) is a mechanism where the **server**
periodically fetches its own OCSP response from the
OCSP responder and "staples" (attaches) it to the
TLS handshake.

**How OCSP Stapling works:**

```
WITHOUT OCSP Stapling:
  Client → OCSP Request → CA's OCSP Responder
  Client ← OCSP Response ← CA's OCSP Responder
  (Client reveals its browsing to CA)
  (Adds latency to each TLS handshake)

WITH OCSP Stapling:
  Server fetches OCSP Response from CA (periodically)
  Server caches the signed OCSP Response
  During TLS Handshake:
    Server → Certificate + Stapled OCSP Response → Client
  Client verifies OCSP Response signature (from CA)
  No need for client to contact CA's OCSP server ✅
```

**Benefits of OCSP Stapling:**

| Benefit | Description |
|---------|-------------|
| **Privacy** | Client does not contact CA — CA cannot track browsing |
| **Performance** | One OCSP lookup by server vs one per client |
| **Reliability** | Works even if OCSP server is temporarily down |
| **Reduced CA load** | Server caches response — much fewer OCSP queries to CA |

**Defined in:** RFC 6066 (TLS Extensions) — the
`status_request` TLS extension

**OCSP Response validity:**
- The stapled OCSP response has a `NextUpdate` field
- Server must refresh the OCSP response before it
  expires (typically every few hours to daily)

---

### 4.5 CRL vs OCSP vs OCSP Stapling

| Property | CRL | OCSP | OCSP Stapling |
|----------|-----|------|---------------|
| **Mechanism** | Download list, check serial | Real-time query per cert | Server pre-fetches, attaches to TLS |
| **Latency** | High (download full CRL) | Medium (one query) | Low (already in handshake) |
| **Privacy** | Better (no per-cert query) | Poor (CA sees all queries) | Best (client never queries CA) |
| **Freshness** | Depends on CRL update period | Real-time | Cached — may be hours old |
| **Scalability** | Poor (large CRLs) | Better | Best |
| **Reliability** | Good (local file) | Depends on OCSP server | Good (cached) |
| **Soft-fail risk** | Yes | Yes | Reduced (must-staple) |
| **RFC** | RFC 5280 | RFC 6960 | RFC 6066 |

---

### 4.6 Revocation Challenges

**The "soft fail" problem:**

```
If OCSP server or CRL download is unreachable:
  → Most browsers "soft fail" = ignore the failure
    and accept the certificate anyway
  → This means: a revoked certificate may be
    accepted if the revocation check fails
  → Attacker can block OCSP/CRL access to
    keep using a revoked certificate

Solution: "Hard fail" = reject if revocation
          check cannot be completed
          (but this breaks too many legitimate sites)
```

**Real-world revocation problems:**

| Problem | Description |
|---------|-------------|
| **CRL size** | Large CAs have CRLs with millions of entries |
| **OCSP traffic** | Major CAs serve billions of OCSP queries per day |
| **Latency** | Each TLS handshake waiting for OCSP query adds delay |
| **Privacy** | Standard OCSP reveals browsing habits to CA |
| **Soft-fail** | Browsers accept certs even when revocation check fails |
| **Short-lived certs** | Let's Encrypt 90-day certs make revocation less critical |

> [!NOTE]
> **Google's CRLSets / OneCRL:**
> Chrome uses its own approach — Google fetches CRLs
> from major CAs and pushes a compressed subset
> (high-impact revocations) to browsers via software
> updates. Firefox uses OneCRL for similar purposes.
> This provides faster, offline revocation checking
> for the most important revocations.

---

## 5. Types and Classes of Certificates

### 5.1 By Validation Level

| Type | Verification Level | Typical Validity | Use Case |
|------|-------------------|-----------------|---------|
| **DV (Domain Validation)** | Domain control only | 1 year | Personal sites, blogs, small business |
| **OV (Organization Validation)** | Domain + Organization | 1 year | Business websites, customer portals |
| **EV (Extended Validation)** | Full legal identity | 1 year | Banks, financial institutions |

---

### 5.2 By Purpose / Use Case

| Certificate Type | Purpose | Key Usage EKU |
|----------------|---------|--------------|
| **SSL/TLS Server Certificate** | Authenticate web server for HTTPS | serverAuth |
| **TLS Client Certificate** | Authenticate a client to a server | clientAuth |
| **Code Signing Certificate** | Sign software executables and scripts | codeSigning |
| **Email / S/MIME Certificate** | Sign and encrypt email | emailProtection |
| **Document Signing Certificate** | Sign PDF and other documents | documentSigning |
| **Timestamping Certificate** | Issue trusted timestamps | timeStamping |
| **OCSP Signing Certificate** | Sign OCSP responses | OCSPSigning |
| **CA Certificate** | Sign other certificates | keyCertSign, cRLSign |
| **Object Signing Certificate** | Sign objects (Java applets, ActiveX) | codeSigning |

---

### 5.3 By Subject Type

| Subject Type | Description | Example |
|-------------|-------------|---------|
| **Personal / Individual** | Issued to a specific person — for email signing, document signing, client auth | employee@company.com |
| **Server / Device** | Issued to a server, IoT device, or network equipment — for TLS | www.example.com |
| **Organization** | Issued to an organization entity | Example Corp |
| **Wildcard** | Issued for *.domain.com — covers all subdomains one level deep | *.example.com |
| **Multi-domain (SAN/UCC)** | Single cert covers multiple specific domains via SAN | www.example.com, api.example.com, example.org |
| **CA Certificate** | Issued to a CA — for signing other certificates | DigiCert Intermediate CA |

---

### 5.4 Special Certificate Types

**Self-Signed Certificate:**
- Issuer = Subject (entity signed its own cert)
- Not trusted by public browsers
- Used for Root CAs, test environments, internal use
- Lab use: XCA creates self-signed root CAs

**Cross-Certificate:**
- One CA signs another CA's certificate
- Used in cross-certification to establish mutual trust
- Creates a new trust path between hierarchies

**Attribute Certificate:**
- Does not contain a public key
- Contains attributes/privileges about a subject
- References a public key certificate (by serial number)
- Used for authorization (what a subject is allowed to do)
  rather than authentication (who the subject is)
- Defined in RFC 5755

**Proxy Certificate:**
- Issued by an end-entity certificate (not a CA)
- Used in Grid computing to delegate credentials
- Allows a process to act on behalf of a user
- Defined in RFC 3820

---

## 6. 📌 Extra Notes

> [!NOTE]
> Everything in this section goes beyond the core
> syllabus but is directly MCQ-relevant.

---

### 6.1 CRL Distribution Points (CDP)

> [!NOTE]
> **CRL Distribution Points (CDP)** is an X.509 v3
> extension that contains the URL(s) where the
> CRL for this certificate can be downloaded.

```
CRL Distribution Points:
  Full Name:
    URL=http://crl.digicert.com/DigiCertGlobalRootCA.crl
    URL=ldap://ldap.digicert.com/...
```

**Multiple CDPs** provide redundancy — if one CRL
server is unreachable, clients try the next URL.

**CRL caching:**
Clients cache downloaded CRLs until the
`Next Update` time in the CRL — reducing repeated
downloads. The `This Update` field shows when the
CRL was published.

---

### 6.2 Delta CRL

> [!NOTE]
> A **Delta CRL** contains ONLY the changes since
> the last complete (Base) CRL — much smaller than
> downloading the full CRL every time.

```
Base CRL: Published weekly — contains all revocations
          File size: potentially several MB

Delta CRL: Published daily or hourly — contains only
           NEW revocations since the last Base CRL
           File size: much smaller — KB range
```

**Delta CRL operation:**
1. Client downloads Base CRL (weekly)
2. Client downloads Delta CRLs (daily/hourly)
3. Client merges Base + Delta for complete picture

**Defined in:** RFC 5280 (X.509 CRL profile)

---

### 6.3 OCSP Must-Staple

> [!NOTE]
> **OCSP Must-Staple** is a certificate extension
> (TLS Feature extension, RFC 7633) that instructs
> browsers to require a valid stapled OCSP response
> when connecting to the server.

```
Without Must-Staple:
  Server doesn't send stapled OCSP response
  → Browser soft-fails (accepts anyway)
  → Attacker blocks OCSP → revoked cert accepted

With Must-Staple:
  Certificate declares: "I WILL always staple OCSP"
  Browser must receive valid stapled OCSP response
  If no stapled response → hard fail → reject connection
```

**Benefits:**
- Eliminates soft-fail vulnerability for that cert
- Forces revocation to be effective

**Risks:**
- If server fails to renew OCSP staple → legitimate
  connections fail (hard fail)
- Server administrators must ensure stapling is
  always operational

---

### 6.4 Soft Fail vs Hard Fail Revocation

> [!NOTE]

| Behavior | Soft Fail | Hard Fail |
|----------|-----------|-----------|
| **OCSP unavailable** | Accept certificate (ignore revocation failure) | Reject certificate |
| **CRL download fails** | Accept certificate | Reject certificate |
| **Security** | Poor — revoked certs may be accepted | Strong — no revocation = no connection |
| **Availability** | Good — sites work even if OCSP server is down | Poor — OCSP outages break legitimate sites |
| **Current browser default** | Soft fail (all major browsers) | Not default anywhere |
| **With OCSP Must-Staple** | N/A | Hard fail for that specific cert |

> [!IMPORTANT]
> All major browsers (Chrome, Firefox, Safari,
> Edge) currently implement **soft fail** for
> OCSP and CRL checks by default.
>
> This means: if an attacker blocks the OCSP
> server and prevents clients from checking
> revocation status, browsers will still accept
> the (potentially revoked) certificate.
>
> This is a known weakness in the current
> certificate revocation ecosystem.

---

### 6.5 CA Compromise — Real Examples

> [!NOTE]

| Incident | Year | CA | Impact |
|----------|------|----|--------|
| **Comodo** | 2011 | Comodo | 9 fraudulent certs issued (google.com, yahoo.com, skype.com) — attacker accessed RA partner systems |
| **DigiNotar** | 2011 | DigiNotar (Netherlands) | 500+ fraudulent certs including google.com, cia.gov — used to MITM Iranian Gmail users. DigiNotar went bankrupt after removal from trust stores |
| **Trustwave** | 2012 | Trustwave | Issued subordinate CA cert to a corporation for MITM monitoring — violated CA/B Forum rules |
| **ANSSI (France)** | 2013 | French government CA | Issued fraudulent Google certs for internal network monitoring |
| **Symantec** | 2015–2017 | Symantec | Mis-issued thousands of certificates — test certs for domains not owned by applicants. Google distrusted Symantec CA in 2018. |
| **StartCom/WoSign** | 2016 | StartCom, WoSign (China) | Multiple Baseline Requirement violations — Mozilla and Apple distrusted them |

> [!NOTE]
> **DigiNotar** is the canonical example of CA
> compromise with real-world harm:
> - Attackers compromised DigiNotar's systems
> - Issued 500+ fraudulent certificates
> - Used to perform MITM attacks against Iranian
>   dissidents accessing Gmail
> - All DigiNotar certs were immediately untrusted
>   by all browsers
> - DigiNotar declared bankruptcy shortly after

---

### 6.6 Certificate Pinning vs CT vs OCSP —
Comparison

> [!NOTE]

| Mechanism | Purpose | Granularity | Limitation |
|-----------|---------|------------|-----------|
| **OCSP** | Check if specific cert is revoked | Per certificate | Soft-fail; privacy; latency |
| **CRL** | List all revoked certs from a CA | Per CA | Size; freshness |
| **OCSP Stapling** | Server pre-fetches OCSP — client gets it in TLS | Per connection | Server must refresh; OCSP Must-Staple needed |
| **Cert Pinning** | App hardcodes expected cert/key | Per application | Operational risk (wrong pin = locked out) |
| **Certificate Transparency** | Audit log of ALL issued certs | Per CA/globally | Detection only — does not block fraudulent certs in real-time |

---

### 6.7 Private PKI vs Public PKI

> [!NOTE]

| Property | Private PKI | Public PKI |
|----------|------------|-----------|
| **Root CA** | Internal — not in public trust stores | In public browser/OS trust stores |
| **Trusted by** | Only systems configured to trust it | All standard browsers/OS globally |
| **Audit requirement** | Internal policies only | CA/Browser Forum, WebTrust/ETSI audits |
| **Cost** | One-time setup + maintenance | Per-certificate cost (or free for DV) |
| **Use case** | Internal networks, enterprise VPN, IoT, testing | Public-facing websites, public APIs |
| **Revocation** | Internal CRL/OCSP | Public CRL/OCSP |
| **Tools** | OpenSSL, CFSSL, Microsoft ADCS, HashiCorp Vault | DigiCert, Sectigo, Let's Encrypt |

**Common Private PKI tools:**
- **OpenSSL** — command line (Sessions 13 lab)
- **XCA** — GUI tool (Sessions 09/10 labs)
- **Microsoft Active Directory Certificate Services (ADCS)** — Windows enterprise PKI
- **HashiCorp Vault** — modern secret + certificate management

---

### 6.8 Let's Encrypt — Free Automated CA

> [!NOTE]

| Property | Detail |
|----------|--------|
| **Operator** | Internet Security Research Group (ISRG) — non-profit |
| **Founded** | 2015 |
| **Certificate type** | DV only — no OV or EV |
| **Cost** | Free |
| **Validity** | 90 days |
| **Protocol** | ACME (RFC 8555) |
| **Volume** | 300+ million active certificates (largest by count) |
| **Root CA** | ISRG Root X1 (RSA) + ISRG Root X2 (ECC) |

**Let's Encrypt cross-signing:**
- Initially cross-signed by IdenTrust's DST Root CA X3
  to gain browser trust quickly
- DST Root CA X3 expired October 2021 — caused issues
  on older Android devices that had not updated
  their trust stores
- Now primarily using ISRG Root X1 (widely trusted)

---

### 6.9 Multi-Domain and Wildcard Certificates

> [!NOTE]

**Multi-Domain Certificate (SAN / UCC):**
- A single cert covering multiple specific domains
  listed in SAN extension
- Also called Unified Communications Certificate
  (UCC) — commonly used in Microsoft Exchange

```
Subject: www.example.com
SAN: DNS: www.example.com
     DNS: example.com
     DNS: api.example.com
     DNS: www.example.org
```

**Wildcard Certificate:**
- Covers all subdomains at ONE level
- `*.example.com` covers www, api, mail, etc.
- Does NOT cover example.com itself
- Does NOT cover sub.sub.example.com

**Combining wildcards with multi-domain:**
```
SAN: DNS: *.example.com
     DNS: example.com
     DNS: *.example.org
```
This single cert covers:
- Any subdomain of example.com (one level)
- example.com itself
- Any subdomain of example.org (one level)

---

### 6.10 Certificate Validity Periods —
History and Current Limits

> [!NOTE]

| Period | Validity Limit | Notes |
|--------|---------------|-------|
| Before 2012 | No industry limit | Certs issued for 10+ years |
| 2012 | 5 years max | CA/Browser Forum Baseline Requirements |
| 2015 | 3 years max | CA/B Forum reduced limit |
| 2018 | 2 years max | CA/B Forum further reduction |
| Sep 2020 | **398 days max** | Current limit (CA/B Forum) — ~13 months |
| 2027 (proposed) | 90 days max | Google/Apple pushing for 90-day maximum |

> [!IMPORTANT]
> The **398-day limit** (since September 1, 2020)
> means certificates can be valid for a maximum of
> approximately 13 months.
>
> The trend is clearly toward shorter validity
> periods — driven by the belief that:
> - Shorter certs = more frequent key rotation
> - Automation (ACME) makes short validity practical
> - Revocation is unreliable — short validity
>   is a better solution

---

### 6.11 Qualified Certificates and eIDAS

> [!NOTE]
> **eIDAS (electronic IDentification, Authentication
> and trust Services)** — EU Regulation 910/2014 —
> defines a framework for electronic identification
> and trust services across the European Union.

**eIDAS trust service types:**

| Service | Description |
|---------|-------------|
| **Qualified Electronic Signature (QES)** | Highest level — equivalent to handwritten signature legally — requires qualified certificate on secure device |
| **Advanced Electronic Signature (AdES)** | Uniquely linked to signer, capable of identifying signer — not as strict as QES |
| **Electronic Signature** | Basic level — any form of electronic signing |

**Qualified Certificate:**
- Issued by a Qualified Trust Service Provider (QTSP)
- QTSPs are listed on EU Member State Trusted Lists
- Certificates must meet ETSI EN 319 412 standards
- Must be issued on a Qualified Signature Creation
  Device (QSCD) — e.g., smart card, USB token

**Legal effect:**
- A QES under eIDAS has the same legal effect as a
  handwritten signature across all EU member states
- eIDAS is enforceable law across 27 EU member states

---

### 6.12 India PKI — Controller of Certifying
Authorities

> [!NOTE]
> India's PKI framework is established under the
> **Information Technology Act 2000 (IT Act)**.

| Entity | Role |
|--------|------|
| **CCA (Controller of Certifying Authorities)** | Apex body — licenses and regulates Certifying Authorities in India |
| **Root Certifying Authority of India (RCAI)** | India's Root CA — operated by CCA — signs Intermediate CA certs for licensed CAs |
| **Certifying Authority (CA)** | Licensed by CCA — issues Digital Signature Certificates (DSCs) |

**DSC (Digital Signature Certificate) classes
(pre-2021 classification):**

| Class | Purpose | Verification |
|-------|---------|-------------|
| **Class 1** | Email/personal identity | Email verification only |
| **Class 2** | Business transactions, MCA filings | Based on submitted documents |
| **Class 3** | e-Tendering, e-Bidding, high-value transactions | In-person verification |

> [!NOTE]
> **Post-2021 DSC update:**
> CCA India simplified the classification — from
> Class 1/2/3 to a unified framework where all DSCs
> issued to individuals require face-to-face or
> video-based verification. Class 2 was discontinued
> as a separate category.

**Common uses of DSC in India:**
- Income tax e-filing
- MCA (Ministry of Corporate Affairs) filings
- e-Tendering (government procurement)
- Aadhaar e-Sign (covered in Session 09)
- GST filing
- Court e-filing

---

## 7. Abbreviations Table

| Abbreviation | Full Form | One-Line Technical Meaning |
|---|---|---|
| CA | Certificate Authority | Trusted entity that issues and signs digital certificates |
| CRL | Certificate Revocation List | CA-published list of revoked certificate serial numbers |
| OCSP | Online Certificate Status Protocol | Real-time single-certificate revocation checking protocol |
| CDP | CRL Distribution Point | X.509 extension containing URL where CRL can be downloaded |
| AIA | Authority Information Access | X.509 extension with OCSP URL and CA cert download URL |
| CABF | CA/Browser Forum | Consortium of CAs and browsers setting certificate standards |
| HSM | Hardware Security Module | Tamper-resistant hardware for secure CA key storage |
| DV | Domain Validation | Certificate validating domain control only |
| OV | Organization Validation | Certificate validating domain + organization identity |
| EV | Extended Validation | Certificate validating full legal identity — strictest |
| ACME | Automatic Certificate Management Environment | Protocol for automated DV cert issuance (RFC 8555) |
| SCT | Signed Certificate Timestamp | Proof cert was submitted to Certificate Transparency log |
| CT | Certificate Transparency | Public audit log of all issued certificates (RFC 6962) |
| ISRG | Internet Security Research Group | Non-profit operating Let's Encrypt |
| ADCS | Active Directory Certificate Services | Microsoft Windows enterprise PKI solution |
| UCC | Unified Communications Certificate | Multi-domain SAN cert — common in Microsoft Exchange |
| QES | Qualified Electronic Signature | EU eIDAS highest level — equivalent to handwritten signature |
| eIDAS | Electronic IDentification Authentication and trust Services | EU Regulation 910/2014 for electronic trust services |
| QTSP | Qualified Trust Service Provider | EU eIDAS certified provider of qualified certificates |
| DSC | Digital Signature Certificate | India IT Act term for digital certificates issued by licensed CAs |
| CCA | Controller of Certifying Authorities | India's apex PKI regulatory body under IT Act 2000 |
| RCAI | Root Certifying Authority of India | India's root CA operated by CCA |
| WoT | Web of Trust | PGP decentralized trust model — users vouch for each other |
| BR | Baseline Requirements | CA/Browser Forum minimum requirements for cert issuance |
| CPS | Certification Practice Statement | CA's document describing its operational PKI procedures |

---

## 8. Keywords + Concept Map

| Term | Definition | Connections | Use Cases |
|------|-----------|-------------|-----------|
| **Root CA** | Self-signed trust anchor — offline | Hierarchy top, trust store, air-gapped | All public PKI trust |
| **Intermediate CA** | CA signed by Root — online | Issues end-entity certs, limits blast radius | Day-to-day cert issuance |
| **CRL** | CA-published revocation list | CDP extension, RFC 5280, serial numbers | Certificate revocation checking |
| **OCSP** | Real-time revocation checking | RFC 6960, AIA extension, VA | Per-connection cert status |
| **OCSP Stapling** | Server pre-fetches OCSP response | RFC 6066, privacy, performance | TLS handshake optimization |
| **Soft Fail** | Accept cert if revocation check fails | Browser default, security weakness | Understanding revocation limits |
| **DV Certificate** | Domain-only validation | Let's Encrypt, ACME, automated | HTTPS for all websites |
| **OV Certificate** | Domain + Org validation | Business trust signal | Customer-facing business sites |
| **EV Certificate** | Full legal identity validation | Banks, financial, green bar (removed 2019) | High-trust transactions |
| **ACME** | Automated cert issuance protocol | RFC 8555, Let's Encrypt, Certbot | Auto-renewing DV certs |
| **CA/Browser Forum** | CA + browser consortium — sets standards | Baseline Requirements, 398-day limit | Governing public PKI |
| **Trust Store** | Pre-installed Root CA collection | Browser, OS, NSS, Java cacerts | Foundation of TLS trust |
| **Web of Trust** | PGP decentralized trust — user vouching | PGP/GPG, no central CA | Email encryption trust |
| **Delta CRL** | CRL with only new revocations since last Base | Size optimization, RFC 5280 | Efficient revocation checking |
| **OCSP Must-Staple** | Cert declares hard-fail OCSP required | RFC 7633, eliminates soft-fail | High-security sites |
| **DigiNotar** | Dutch CA compromised 2011 — canonical failure | MITM against Iranians, removed from trust stores | CA security importance |
| **Let's Encrypt** | Free automated DV CA — ISRG, 90-day certs | ACME, RFC 8555, largest by count | Free HTTPS everywhere |
| **DSC India** | Digital Signature Certificate under IT Act | CCA, RCAI, eMudhra | Indian government e-services |

---

## 9. Quick Reference Cheatsheet

### 🔸 CA Hierarchy — Three Tiers

```
Root CA     → Self-signed, OFFLINE, 20–40 yr validity
    ↓ signs
Intermediate CA → Online HSM, 5–10 yr validity
    ↓ signs
End-Entity Cert → Installed on server/device, ≤398 days
```

---

### 🔸 CRL vs OCSP vs OCSP Stapling

| | CRL | OCSP | OCSP Stapling |
|---|-----|------|---------------|
| Freshness | Periodic | Real-time | Cached (hours) |
| Privacy | Better | Poor | Best |
| Performance | Slow (large file) | Medium | Fast |
| RFC | 5280 | 6960 | 6066 |

---

### 🔸 DV vs OV vs EV

| | DV | OV | EV |
|---|----|----|-----|
| Verifies | Domain | Domain + Org | Full legal identity |
| Time | Minutes | Hours–Days | Days–Weeks |
| Cost | Free–Low | Medium | High |
| Subject | Domain only | Domain + Org name | Full legal identity |
| Use | Any site | Business | Banks, finance |

---

### 🔸 Certificate Validity Limit Timeline

```
Pre-2012:   No limit (10+ years possible)
2012:       5 years max
2015:       3 years max
2018:       2 years max
Sep 2020:   398 days max (current)
2027 (proposed): 90 days max
```

---

### 🔸 Revocation Reason Codes

| Code | Reason |
|------|--------|
| 1 | keyCompromise — most critical |
| 2 | cACompromise — CA key stolen |
| 3 | affiliationChanged |
| 4 | superseded |
| 5 | cessationOfOperation |
| 6 | certificateHold (temporary) |
| 9 | privilegeWithdrawn |

---

### 🔸 India PKI Quick Reference

| Entity | Role |
|--------|------|
| CCA | Licensing body — regulates CAs |
| RCAI | India Root CA — operated by CCA |
| DSC | Digital Signature Certificate |
| IT Act 2000 | Legal framework for digital signatures in India |
| eMudhra, (n)Code, SafeScrypt | Licensed CAs in India |

---

### 🔸 Trust Model Summary

| Model | Used By | Key Feature |
|-------|---------|------------|
| Hierarchical | TLS/HTTPS | Root CA = trust anchor in trust store |
| Web of Trust | PGP/GPG | Users vouch for each other — no central CA |
| Cross-Certification | Inter-org PKI | Two CAs sign each other's certs |
| Bridge CA | US Federal PKI | Hub CA connects multiple hierarchies |

---

## 10. Session Revision Snapshot

### ⚡ TL;DR — 5 Bullets

- ✅ CA is the trust anchor of PKI — Root CA is
  self-signed and kept offline; Intermediate CA is
  online and issues end-entity certs — if Root CA
  is compromised the entire hierarchy collapses;
  Intermediate CA compromise is recoverable
- ✅ Certificate revocation: CRL (periodic list of
  revoked serial numbers) vs OCSP (real-time status
  query) vs OCSP Stapling (server pre-fetches and
  staples OCSP response to TLS handshake) — all
  major browsers currently soft-fail on revocation
  check failure
- ✅ Three certificate validation levels: DV (domain
  only — minutes, free), OV (domain + org — hours
  to days), EV (full legal identity — days to weeks);
  current max validity = 398 days (since Sep 2020)
- ✅ Certificate Transparency (CT) requires all
  publicly trusted certs to be logged in public
  append-only Merkle tree logs — Chrome has required
  CT since 2018; CA/Browser Forum governs public PKI
  standards including the 398-day validity limit
- ✅ India PKI: IT Act 2000 → CCA licenses CAs →
  RCAI is India's Root CA → licensed CAs issue DSCs
  used for income tax e-filing, MCA filings,
  e-tendering; eIDAS in EU creates legally recognized
  QES equivalent to handwritten signatures

---

### 🎯 MCQ-Likely Concepts — Everything Examiners Love

| Concept | Why It's Tricky |
|---------|----------------|
| Root CA kept OFFLINE | Security principle — not a performance choice |
| CRL = list of revoked serial numbers | Specific content of CRL — not hashes, not public keys |
| OCSP Stapling = SERVER fetches OCSP, attaches to TLS | Students say "client fetches" — wrong |
| Soft fail = browsers accept cert when OCSP fails | Counter-intuitive security weakness |
| DV issuance in MINUTES via ACME | Extremely fast — automated domain verification |
| EV green bar REMOVED in 2019 | Chrome and Firefox removed it — EV certs still exist |
| 398 days = current max cert validity (since Sep 2020) | Specific date and number — tested |
| Let's Encrypt = 90-day DV certs — free — ISRG | All three facts commonly tested |
| OCSP RFC = 6960; CRL defined in RFC 5280 | RFC number mapping |
| ACME = RFC 8555 | RFC number for ACME protocol |
| DigiNotar 2011 = canonical CA compromise | Year and consequence important |
| Symantec distrusted 2018 by Google | Major modern CA distrusting event |
| Bridge CA used in US Federal PKI | Specific real-world use case |
| Web of Trust = PGP — 1 full OR 3 marginal = valid | Specific trust calculation rules |
| DV = domain only; OV = domain + org; EV = full legal | Core classification — must be memorized |
| Delta CRL = changes since last Base CRL | Specific optimization technique |
| OCSP Must-Staple = hard fail for that cert | Eliminates soft-fail vulnerability |
| CCA India = licensing body; RCAI = Root CA | Indian PKI roles distinction |
| DSC Class 3 = in-person verification (India) | Specific class requirement |
| CA/Browser Forum governs public PKI — not NIST | Standards body distinction |

---

<details>
<summary>🔬 Lab Content (Session 08 — No Lab Assigned)</summary>

No lab is assigned for Session 08 in the syllabus.

Session 08 theory directly connects to the labs
in Sessions 09 and 10 where the CA trust hierarchy,
certificate issuance, and verification processes
are demonstrated hands-on using XCA tool.

**Theory → Lab connections:**

| Session 08 Concept | Lab Demonstration |
|-------------------|------------------|
| CA hierarchy (Root → Intermediate → End Entity) | Session 10 XCA: Create Root CA → Issue cert from it |
| DV validation (domain control) | Session 09/13: Self-signed cert = no third party validation |
| Certificate issuance process (CSR → CA → Cert) | Session 09/10 XCA + Session 13 OpenSSL |
| Self-signed vs CA-signed | Session 10: browser warning removed after importing CA cert |
| CRL / OCSP concepts | Referenced in Session 13 OpenSSL PKI setup |
| X.509 cert structure | XCA shows all fields visually in GUI |

**Lab files:**
- `3-Labs/lab-session-09-xca-signing.md`
- `3-Labs/lab-session-10-xca-certificates.md`
- `3-Labs/lab-session-13-openssl-pki.md`

</details>

---