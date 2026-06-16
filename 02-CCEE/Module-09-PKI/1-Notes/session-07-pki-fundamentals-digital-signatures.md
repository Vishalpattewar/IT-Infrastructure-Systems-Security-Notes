# Session 07 — PKI Fundamentals, Digital Signatures
& Digital Certificates

## 📑 Table of Contents

- [1. PKI Fundamentals](#1-pki-fundamentals)
  - [1.1 What is PKI?](#11-what-is-pki)
  - [1.2 Why PKI Exists — The Problem It Solves](#12-why-pki-exists--the-problem-it-solves)
  - [1.3 PKI Components](#13-pki-components)
  - [1.4 PKI Services](#14-pki-services)
  - [1.5 PKI Trust Models](#15-pki-trust-models)
- [2. Digital Signatures](#2-digital-signatures)
  - [2.1 What is a Digital Signature?](#21-what-is-a-digital-signature)
  - [2.2 Why Digital Signatures — The Problem They
    Solve](#22-why-digital-signatures--the-problem-they-solve)
  - [2.3 How Digital Signatures Work](#23-how-digital-signatures-work)
  - [2.4 Digital Signature — Step by Step](#24-digital-signature--step-by-step)
  - [2.5 Security Properties of Digital Signatures](#25-security-properties-of-digital-signatures)
  - [2.6 Digital Signature Algorithms](#26-digital-signature-algorithms)
  - [2.7 Digital Signature vs Electronic Signature](#27-digital-signature-vs-electronic-signature)
  - [2.8 Digital Signature vs HMAC](#28-digital-signature-vs-hmac)
- [3. Digital Certificates](#3-digital-certificates)
  - [3.1 What is a Digital Certificate?](#31-what-is-a-digital-certificate)
  - [3.2 Why Digital Certificates Are Needed](#32-why-digital-certificates-are-needed)
  - [3.3 X.509 Standard](#33-x509-standard)
  - [3.4 X.509 Certificate Structure](#34-x509-certificate-structure)
  - [3.5 X.509 Certificate Versions](#35-x509-certificate-versions)
  - [3.6 Certificate Fingerprint](#36-certificate-fingerprint)
  - [3.7 How a Certificate is Issued](#37-how-a-certificate-is-issued)
  - [3.8 How a Certificate is Verified](#38-how-a-certificate-is-verified)
  - [3.9 Certificate Chain of Trust](#39-certificate-chain-of-trust)
- [4. 📌 Extra Notes](#4--extra-notes)
  - [4.1 PKI Standards and RFCs](#41-pki-standards-and-rfcs)
  - [4.2 X.509 v3 Certificate Extensions](#42-x509-v3-certificate-extensions)
  - [4.3 Subject Alternative Name (SAN)](#43-subject-alternative-name-san)
  - [4.4 Certificate Encoding Formats](#44-certificate-encoding-formats)
  - [4.5 Self-Signed Certificates](#45-self-signed-certificates)
  - [4.6 DSA — Digital Signature Algorithm](#46-dsa--digital-signature-algorithm)
  - [4.7 RSA Digital Signature vs RSA Encryption —
    Key Direction](#47-rsa-digital-signature-vs-rsa-encryption--key-direction)
  - [4.8 Non-Repudiation in Law](#48-non-repudiation-in-law)
  - [4.9 Web of Trust vs Hierarchical PKI](#49-web-of-trust-vs-hierarchical-pki)
  - [4.10 Certificate Pinning](#410-certificate-pinning)
  - [4.11 Certificate Transparency (CT)](#411-certificate-transparency-ct)
  - [4.12 PKI Roles — RA, VA, Repository](#412-pki-roles--ra-va-repository)
  - [4.13 PKIX — Internet PKI Profile](#413-pkix--internet-pki-profile)
- [5. Abbreviations Table](#5-abbreviations-table)
- [6. Keywords + Concept Map](#6-keywords--concept-map)
- [7. Quick Reference Cheatsheet](#7-quick-reference-cheatsheet)
- [8. Session Revision Snapshot](#8-session-revision-snapshot)

---

## 1. PKI Fundamentals

### 1.1 What is PKI?

**PKI (Public Key Infrastructure)** is the complete
framework of hardware, software, policies, procedures,
and standards needed to create, manage, distribute,
use, store, and revoke digital certificates and
public-private key pairs.

PKI is not a single product or algorithm — it is an
**ecosystem** that makes public key cryptography
practical and trustworthy at scale.

```
PKI = People + Processes + Policies + Technology
      working together to establish TRUST in
      public keys across a network
```

> [!IMPORTANT]
> The fundamental question PKI answers:
> *"How do I know that the public key I have actually
> belongs to the person or server I think it does?"*
>
> Without PKI, anyone could publish a fake public key
> claiming to belong to someone else — enabling MITM
> attacks against every public key operation.

---

### 1.2 Why PKI Exists — The Problem It Solves

**The Public Key Authentication Problem:**

```
Alice wants to send Bob an encrypted message.
She needs Bob's public key.
She finds a key online labeled "Bob's Public Key."

Question: How does Alice KNOW this key really
          belongs to Bob and not an attacker
          pretending to be Bob?
```

Without PKI:
- Alice has no way to verify key ownership
- An attacker (Mallory) could publish her own
  key labeled as "Bob's" and intercept all messages

**PKI solves this with digital certificates:**
- Bob's public key is bundled with his identity
  information (name, organization, domain)
- A trusted third party (Certificate Authority)
  digitally signs this bundle
- Alice verifies the CA's signature to confirm
  the key genuinely belongs to Bob

---

### 1.3 PKI Components

| Component | Role |
|-----------|------|
| **CA (Certificate Authority)** | Trusted entity that issues and signs digital certificates |
| **RA (Registration Authority)** | Verifies identity of certificate applicants before CA issues cert |
| **VA (Validation Authority)** | Checks if a certificate is still valid (OCSP responder) |
| **Repository / Certificate Store** | Stores issued certificates and CRLs for public access |
| **CRL (Certificate Revocation List)** | Published list of revoked certificates |
| **OCSP (Online Certificate Status Protocol)** | Real-time certificate revocation checking |
| **End Entity** | The user, device, or server that holds a certificate |
| **Certificate Policy (CP)** | Document defining how certs are issued and used |
| **CPS (Certification Practice Statement)** | CA's detailed procedures for how it operates |

---

### 1.4 PKI Services

PKI provides the following security services:

| Service | How PKI Provides It |
|---------|-------------------|
| **Authentication** | Digital certificates bind identity to a public key — prove who you are |
| **Integrity** | Digital signatures verify data has not been altered |
| **Confidentiality** | Encrypt data with receiver's public key from their certificate |
| **Non-repudiation** | Digital signature with private key — signer cannot deny signing |
| **Key Management** | Structured issuance, distribution, renewal, and revocation of keys |

> [!NOTE]
> PKI is the infrastructure that makes all five
> security services trustworthy at scale.
> Without PKI, digital signatures and public key
> encryption would be trivially spoofed.

---

### 1.5 PKI Trust Models

A **trust model** defines how entities decide which
certificates to trust.

#### Hierarchical Trust Model (Most Common)

```
Root CA (Self-signed, highest trust)
    │
    ├── Intermediate CA 1
    │       ├── End Entity Cert A
    │       └── End Entity Cert B
    │
    └── Intermediate CA 2
            ├── End Entity Cert C
            └── End Entity Cert D
```

- Root CA is the **trust anchor** — its certificate
  is pre-installed in browsers and operating systems
- Intermediate CAs are signed by the Root CA
- End entity certificates are signed by Intermediate CAs
- Root CA private key is kept OFFLINE for maximum
  security — Intermediate CAs do the day-to-day
  certificate signing

**Why Intermediate CAs exist:**
- If Root CA private key is compromised, all trust
  collapses
- Intermediate CAs add a buffer — if an Intermediate
  CA is compromised, only its certificates are revoked
  (not the entire trust hierarchy)
- Root CA can revoke the Intermediate CA certificate

#### Cross-Certification Model
- Two separate CA hierarchies establish trust with
  each other by signing each other's root certificates
- Used between organizations or between national PKIs

#### Web of Trust (PGP Model)
- No central CA — users vouch for each other's keys
- Trust is cumulative — multiple vouches = higher trust
- Used in PGP/GPG email encryption
- Covered in detail in Session 13

#### Bridge CA Model
- A Bridge CA acts as a hub between multiple
  hierarchical PKIs
- Each PKI trusts the Bridge CA → indirectly trusts
  all other connected PKIs
- Used in US federal government PKI (Federal Bridge CA)

> [!IMPORTANT]
> The **Hierarchical Trust Model** is used by all
> commercial and public web PKI (HTTPS, TLS).
> Browser vendors (Google, Mozilla, Apple, Microsoft)
> maintain a **Root Store** — a curated list of
> trusted Root CAs pre-installed in their software.
> If a CA is removed from root stores → all its
> certificates become untrusted immediately.

---

## 2. Digital Signatures

### 2.1 What is a Digital Signature?

A **digital signature** is a cryptographic mechanism
that binds a signer's identity to a specific piece
of data — proving:

1. **Who** signed it (Authentication)
2. **That it was not altered** after signing (Integrity)
3. **That the signer cannot deny signing** (Non-repudiation)

A digital signature is created using the signer's
**private key** and can be verified by anyone with
the corresponding **public key**.

> [!IMPORTANT]
> A digital signature is NOT:
> - A scanned image of a handwritten signature
> - An electronic signature (typed name, checkbox)
> - Encryption of the entire document
>
> A digital signature IS:
> - A mathematical value computed from the document
>   and the private key
> - A small fixed-size value (attached to the document)
> - Verifiable by anyone with the signer's public key

---

### 2.2 Why Digital Signatures — The Problem They Solve

**Without digital signatures:**
```
Bob sends: "Transfer $1000 to Alice" + his signature
  → How does the bank know Bob really sent this?
  → How does the bank know the amount wasn't changed?
  → Can Bob claim he never sent it?
```

**With digital signatures:**
```
Bob computes Hash("Transfer $1000 to Alice")
Bob encrypts the hash with his PRIVATE KEY → Signature
Bank receives message + signature
Bank decrypts signature with Bob's PUBLIC KEY → Hash'
Bank recomputes Hash("Transfer $1000 to Alice")
If Hash' matches → Bob sent it, amount is unchanged ✅
Bob cannot deny it — only his private key could create
that signature
```

---

### 2.3 How Digital Signatures Work

Digital signatures use **asymmetric cryptography**
combined with **hash functions**:

```
KEY INSIGHT:
  Sign with PRIVATE key → Verify with PUBLIC key

This is the REVERSE of encryption:
  Encrypt with PUBLIC key → Decrypt with PRIVATE key
```

**Why hash the message first?**

| Reason | Explanation |
|--------|-------------|
| **Size** | RSA can only sign data smaller than key size (~256 bytes for RSA-2048). Documents can be megabytes. |
| **Speed** | Hashing is fast; RSA is slow. Sign a 32-byte hash, not a 10MB document. |
| **Integrity** | The hash acts as a compact, fixed-size fingerprint of the entire document. |

---

### 2.4 Digital Signature — Step by Step

#### Signing Process (Sender)

```
Step 1: Signer has:
  - Document / Message M
  - Private Key KR_signer

Step 2: Compute hash of message
  H = SHA-256(M)

Step 3: Encrypt hash with private key
  Signature S = Encrypt(KR_signer, H)
  [In RSA: S = H^d mod n]
  [In ECDSA: S = (r, s) derived from k × G and private key]

Step 4: Attach signature to message
  Send: M + S
```

#### Verification Process (Receiver)

```
Step 1: Receiver has:
  - Message M (received)
  - Signature S (received)
  - Signer's Public Key KU_signer (from certificate)

Step 2: Decrypt signature with public key
  H' = Decrypt(KU_signer, S)
  [In RSA: H' = S^e mod n]

Step 3: Recompute hash of received message
  H = SHA-256(M)

Step 4: Compare
  If H' == H → ✅ Signature VALID
    → Message is authentic (from key owner)
    → Message was not altered after signing

  If H' ≠ H  → ❌ Signature INVALID
    → Either message was tampered OR
    → Wrong public key used (not the actual signer)
```

---

### 2.5 Security Properties of Digital Signatures

| Property | Description |
|----------|-------------|
| **Authentication** | Only the holder of the private key can create a valid signature — proves identity |
| **Integrity** | Any change to the document after signing changes the hash — signature verification fails |
| **Non-repudiation** | Signer cannot deny signing — private key is unique to them — provable in court |
| **Unforgeability** | Without the private key, signature cannot be forged — protected by RSA/ECDSA hardness |

> [!IMPORTANT]
> **Non-repudiation is the UNIQUE property of
> digital signatures** — not provided by:
> - Symmetric encryption alone
> - HMAC (shared key — either party could have
>   created the MAC)
> - Plain hash functions (no key at all)
>
> Non-repudiation requires that ONLY ONE PARTY
> could have created the signature — possible only
> with asymmetric private key cryptography.

---

### 2.6 Digital Signature Algorithms

| Algorithm | Basis | Key Size | Hash Used | Standard |
|-----------|-------|---------|-----------|---------|
| **RSA** | Integer Factorization | 2048–4096-bit | SHA-256/384/512 | PKCS#1 PSS |
| **DSA** | Discrete Logarithm | 1024–3072-bit | SHA-1/256 | FIPS 186-4 |
| **ECDSA** | ECDLP | 256–521-bit | SHA-256/384/512 | FIPS 186-4 |
| **Ed25519** | ECDLP (Edwards curve) | 255-bit | SHA-512 internally | RFC 8032 |
| **Ed448** | ECDLP (Edwards curve) | 448-bit | SHAKE256 | RFC 8032 |

**Naming convention for combined algorithm:**
```
SHA256withRSA    → hash with SHA-256, sign with RSA
SHA256withECDSA  → hash with SHA-256, sign with ECDSA
```

> [!NOTE]
> **Ed25519** is increasingly the preferred
> signature algorithm for new systems:
> - Used by OpenSSH (default since 2018)
> - Used by Signal Protocol
> - Faster than ECDSA P-256
> - Built-in protection against poor nonce
>   generation (unlike ECDSA where nonce reuse
>   is catastrophic — PS3 breach)

---

### 2.7 Digital Signature vs Electronic Signature

| Property | Digital Signature | Electronic Signature |
|----------|------------------|---------------------|
| **Definition** | Cryptographic mechanism using private key + hash | Any electronic indication of agreement — typed name, checkbox, scanned signature, PIN |
| **Security** | Mathematically provable — forgery requires breaking asymmetric crypto | Variable — ranges from none to strong |
| **Non-repudiation** | Strong — private key proof | Weak — depends on implementation |
| **Legal status** | Legally binding in most jurisdictions (India IT Act, eIDAS, ESIGN Act) | May or may not be legally binding |
| **Examples** | RSA/ECDSA signed PDF, code signing certificate | DocuSign checkbox, typed name in email, PIN entry |

> [!NOTE]
> **India IT Act (2000):**
> The Information Technology Act 2000 recognizes
> digital signatures as legally valid for most
> purposes. It defines:
> - **Digital Signature** — cryptographic signature
>   using asymmetric keys issued by licensed CAs
> - **Electronic Signature** — broader term including
>   other electronic authentication methods
>
> India's Controller of Certifying Authorities (CCA)
> licenses and regulates CAs under the IT Act.
> This is covered in detail in Session 14.

---

### 2.8 Digital Signature vs HMAC

| Property | HMAC | Digital Signature |
|----------|------|-----------------|
| **Key type** | Shared secret (symmetric) | Private key (asymmetric) |
| **Who can verify** | Only parties with the shared key | Anyone with the public key |
| **Non-repudiation** | ❌ No — either party could have created it | ✅ Yes — only private key holder |
| **Speed** | Fast | Slower (asymmetric operations) |
| **Scalability** | Requires pre-shared key between every pair | Public key freely available — no pre-sharing |
| **Use case** | API authentication, TLS record integrity | Legal documents, certificates, code signing |

---

## 3. Digital Certificates

### 3.1 What is a Digital Certificate?

A **digital certificate** (also called a
**public key certificate**) is an electronic
document that:

1. Contains a **public key**
2. Binds that key to an **identity** (person,
   server, organization)
3. Is **digitally signed** by a trusted
   **Certificate Authority (CA)**

```
Digital Certificate = Public Key + Identity Info
                      + CA's Digital Signature
```

The CA's signature is the proof of trust —
it says "I, a trusted CA, have verified that
this public key belongs to this identity."

---

### 3.2 Why Digital Certificates Are Needed

Without certificates:
```
Alice wants to use Bob's public key.
She finds "Bob's Public Key" online.
But she has NO WAY to verify it really belongs
to Bob — could be Mallory's key labeled as Bob's.
→ MITM attack succeeds.
```

With certificates:
```
Bob has a certificate signed by TrustCA.
Alice already trusts TrustCA (it is in her
browser's trust store).
She verifies TrustCA's signature on Bob's cert.
If signature is valid → Bob's public key is
genuine → MITM is prevented.
```

---

### 3.3 X.509 Standard

**X.509** is the international standard that
defines the format of digital certificates.

| Property | Detail |
|----------|--------|
| **Standard name** | X.509 |
| **Defined by** | ITU-T (International Telecommunication Union) |
| **First published** | 1988 |
| **Current version** | X.509 v3 (1996, most widely used) |
| **Related RFC** | RFC 5280 — Internet X.509 PKI Profile |
| **Used in** | TLS/HTTPS, S/MIME, code signing, SSH certificates |

> [!IMPORTANT]
> X.509 is the ONLY certificate format used in
> commercial PKI and the Internet (TLS/HTTPS).
> When someone says "SSL certificate" or "TLS
> certificate" — they mean an X.509 v3 certificate.

---

### 3.4 X.509 Certificate Structure

An X.509 v3 certificate contains the following fields:

**TBSCertificate (To Be Signed) fields:**

| Field | Description | Example |
|-------|-------------|---------|
| **Version** | X.509 version (1, 2, or 3) | v3 |
| **Serial Number** | Unique number assigned by the CA | 0x7A4F2C8D1B |
| **Signature Algorithm** | Algorithm used by CA to sign the cert | SHA256withRSA |
| **Issuer** | Distinguished Name (DN) of the CA | CN=DigiCert CA, O=DigiCert Inc |
| **Validity Period** | Not Before + Not After dates | 2024-01-01 to 2025-01-01 |
| **Subject** | Distinguished Name of the cert owner | CN=www.example.com |
| **Subject Public Key Info** | The public key + algorithm | RSA 2048-bit public key |
| **Extensions (v3 only)** | Additional information | SAN, Key Usage, Basic Constraints |

**Certificate signature fields:**
| Field | Description |
|-------|-------------|
| **Signature Algorithm** | Algorithm used for CA's signature |
| **Signature Value** | CA's actual digital signature over TBSCertificate |

**Distinguished Name (DN) fields:**

| Abbreviation | Full Name | Example |
|-------------|-----------|---------|
| **CN** | Common Name | www.example.com |
| **O** | Organization | Example Corp |
| **OU** | Organizational Unit | IT Department |
| **C** | Country | IN (India), US, GB |
| **ST** | State | Maharashtra |
| **L** | Locality | Pune |

---

### 3.5 X.509 Certificate Versions

| Version | Year | Key Addition |
|---------|------|-------------|
| **v1** | 1988 | Basic certificate structure — no extensions |
| **v2** | 1993 | Added Issuer and Subject Unique Identifiers |
| **v3** | 1996 | Added Extensions — most important addition |

> [!IMPORTANT]
> **X.509 v3 extensions** are what make modern PKI
> practical — they add:
> - Subject Alternative Names (multiple domains)
> - Key Usage restrictions
> - CA/end-entity distinction (Basic Constraints)
> - CRL distribution points
> - OCSP responder URL
>
> All modern TLS certificates are **X.509 v3**.

---

### 3.6 Certificate Fingerprint

A **certificate fingerprint** is a hash of the
entire certificate (computed by the relying party —
not by the CA).

```
Fingerprint = SHA-256(entire certificate DER bytes)
```

**Properties:**
- Not part of the certificate itself — computed
  independently
- Used to uniquely identify a certificate
- Easy to compare — two parties compare fingerprints
  to verify they have the same certificate
- Displayed in browser's certificate viewer as
  "SHA-256 Fingerprint"

> [!NOTE]
> When you look at a certificate in a browser and
> see "Fingerprint: 3A:F2:C1:..." — that is the
> SHA-256 hash of the certificate.
> Fingerprints are how certificate pinning works —
> the application hardcodes the expected fingerprint
> and rejects any certificate with a different hash.

---

### 3.7 How a Certificate is Issued

**Certificate Enrollment/Issuance Process:**

```
Step 1: Key Generation (End Entity)
  The applicant generates a public/private key pair
  Applicant keeps private key SECRET

Step 2: CSR Creation (End Entity)
  Applicant creates a Certificate Signing Request (CSR)
  CSR contains:
    - Applicant's public key
    - Applicant's identity information (DN)
    - Signature by applicant's private key
      (proves applicant owns the corresponding private key)

Step 3: Identity Verification (RA/CA)
  CA or RA verifies the applicant's identity
  Verification level depends on certificate type:
    DV (Domain Validation) → verify domain control only
    OV (Organization Validation) → verify organization
    EV (Extended Validation) → thorough legal verification

Step 4: Certificate Issuance (CA)
  CA creates the X.509 certificate:
    - Copies public key and identity from CSR
    - Adds validity period, serial number, extensions
    - Signs the TBSCertificate with CA's private key

Step 5: Certificate Delivery
  CA sends signed certificate to applicant
  CA also publishes certificate in repository

Step 6: Certificate Use
  Applicant installs certificate on server/device
  Certificate is presented during TLS handshake etc.
```

**CSR (Certificate Signing Request):**
- Standardized format: PKCS#10 (RFC 2986)
- Contains public key + identity + applicant's
  self-signature
- The applicant's self-signature on the CSR proves
  they own the private key matching the public key
  in the CSR (proof of possession)

---

### 3.8 How a Certificate is Verified

When a client (browser) receives a server's
certificate, it performs these checks:

```
Step 1: Chain Validation
  Verify the certificate chain from end-entity
  up to a trusted Root CA
  Each certificate in chain must be signed by
  the next higher CA

Step 2: Signature Verification
  Verify CA's digital signature on the certificate
  using the CA's public key
  If signature is invalid → certificate is forged

Step 3: Validity Period
  Check current date is between Not Before and
  Not After dates
  Expired certificates → connection rejected

Step 4: Revocation Check
  Check if certificate has been revoked:
    Method 1: Download CRL (Certificate Revocation List)
    Method 2: OCSP query (Online Certificate Status Protocol)

Step 5: Name Matching
  Verify the certificate's CN or SAN matches the
  hostname being connected to
  Mismatch → browser shows certificate warning

Step 6: Key Usage
  Verify the certificate's Key Usage extension permits
  the intended use (e.g., serverAuth for TLS)
```

> [!IMPORTANT]
> ALL steps must pass for a certificate to be
> considered valid. Browsers reject certificates
> that fail ANY of these checks — showing
> security warnings or blocking the connection.

---

### 3.9 Certificate Chain of Trust

A **certificate chain** (also called a
**certification path**) is the sequence of
certificates from the end-entity certificate
up to a trusted Root CA.

```
Browser's Trust Store contains:
  [Root CA Certificate] ← self-signed, pre-installed

Certificate Chain presented by server:
  [End Entity Cert]     ← signed by Intermediate CA
        ↑ verified by
  [Intermediate CA Cert] ← signed by Root CA
        ↑ verified by
  [Root CA Cert]         ← in browser trust store ✅
```

**Why servers send the Intermediate CA cert
(but not the Root CA cert):**
- Root CA cert is already in the browser trust store
- Intermediate CA cert is needed because the browser
  needs it to verify the chain
- Server must include the full chain (end-entity +
  all intermediate certificates) in its TLS handshake

**Chain verification:**
```
For each cert in chain (bottom to top):
  1. Verify issuer of this cert = subject of next cert
  2. Verify signature using next cert's public key
  3. Check validity dates
  4. Check revocation status
  Until reaching a trusted Root CA in trust store → ✅
```

---

## 4. 📌 Extra Notes

> [!NOTE]
> Everything in this section goes beyond the core
> syllabus but is directly MCQ-relevant.

---

### 4.1 PKI Standards and RFCs

> [!NOTE]

| Standard | Description | Year |
|----------|-------------|------|
| **X.509** | ITU-T certificate format standard | 1988 (v1), 1996 (v3) |
| **RFC 5280** | Internet X.509 PKI Certificate and CRL Profile | 2008 |
| **RFC 2986** | PKCS#10 — Certificate Signing Request format | 2000 |
| **RFC 2459** | Original PKIX profile (superseded by RFC 5280) | 1999 |
| **RFC 6960** | OCSP — Online Certificate Status Protocol | 2013 |
| **RFC 5652** | CMS — Cryptographic Message Syntax | 2009 |
| **RFC 3161** | TSP — Time Stamp Protocol | 2001 |
| **RFC 4880** | OpenPGP Message Format | 2007 |
| **ITU-T X.500** | Directory Services — basis of Distinguished Names | 1988 |

---

### 4.2 X.509 v3 Certificate Extensions

> [!NOTE]
> Extensions were introduced in X.509 v3 (1996)
> and are the most important part of modern
> certificates.

**Critical vs Non-Critical Extensions:**
- **Critical** — if a system does not understand
  this extension, it MUST reject the certificate
- **Non-critical** — if not understood, the
  extension is ignored

**Key extensions:**

| Extension | Critical? | Description |
|-----------|----------|-------------|
| **Basic Constraints** | ✅ Yes | Is this a CA certificate? Max path length? |
| **Key Usage** | ✅ Yes | What the key may be used for |
| **Extended Key Usage (EKU)** | Sometimes | Specific uses: serverAuth, clientAuth, codeSigning |
| **Subject Alternative Name (SAN)** | ✅ Yes (preferred) | Additional identities: DNS names, IPs, emails |
| **Authority Key Identifier** | No | Identifies which CA key signed this cert |
| **Subject Key Identifier** | No | Identifies this certificate's public key |
| **CRL Distribution Points (CDP)** | No | Where to download the CRL |
| **Authority Information Access (AIA)** | No | URL for OCSP and CA certificate download |
| **Certificate Policies** | No | Policy OIDs and CPS URL |

**Key Usage values:**

| Key Usage Bit | Meaning |
|---------------|---------|
| digitalSignature | Signing data (not certificates) |
| contentCommitment (nonRepudiation) | Non-repudiation |
| keyEncipherment | Encrypting keys (RSA key transport) |
| dataEncipherment | Encrypting data directly |
| keyAgreement | Key exchange (DH/ECDH) |
| keyCertSign | Signing certificates — CA use only |
| cRLSign | Signing CRLs — CA use only |

**Extended Key Usage values:**

| EKU OID Name | Purpose |
|-------------|---------|
| serverAuth | TLS server authentication |
| clientAuth | TLS client authentication |
| codeSigning | Software code signing |
| emailProtection | S/MIME email |
| timeStamping | Trusted timestamp service |
| OCSPSigning | OCSP responder certificate |

---

### 4.3 Subject Alternative Name (SAN)

> [!NOTE]
> **SAN (Subject Alternative Name)** is an X.509 v3
> extension that allows a single certificate to be
> valid for multiple identities.

**Why SAN replaced CN for domain matching:**
- Old practice: use the CN (Common Name) field for
  the hostname
- RFC 2818 (HTTPS over TLS, 2000) stated browsers
  should use SAN if present
- Since 2017, major browsers require SAN for domain
  validation — CN-only matching is rejected

**SAN types:**

| SAN Type | Example |
|----------|---------|
| **dNSName** | www.example.com, *.example.com |
| **iPAddress** | 192.168.1.1 |
| **rfc822Name** | user@example.com (email) |
| **uniformResourceIdentifier** | https://example.com |
| **directoryName** | DN for X.500/LDAP |

**Wildcard certificates:**
- `*.example.com` matches `www.example.com`,
  `api.example.com` — but NOT `sub.api.example.com`
- Wildcards only match one level deep
- `*.example.com` does NOT match `example.com` itself

**SAN example in a real cert:**
```
Subject Alternative Name:
  DNS: www.example.com
  DNS: example.com
  DNS: api.example.com
  IP: 203.0.113.1
```

---

### 4.4 Certificate Encoding Formats

> [!NOTE]

| Format | Extension | Encoding | Contains | Common Use |
|--------|-----------|----------|---------|-----------|
| **DER** | .der, .cer | Binary (ASN.1 DER) | Single certificate | Java, Windows |
| **PEM** | .pem, .crt, .cer | Base64 of DER | Cert, key, chain | OpenSSL, Linux, Apache |
| **PFX/PKCS#12** | .pfx, .p12 | Binary | Cert + private key + chain | Windows, IIS, Exchange |
| **P7B/PKCS#7** | .p7b, .p7c | Base64 or binary | Cert chain (no private key) | Windows certificate chain |

**PEM format example:**
```
-----BEGIN CERTIFICATE-----
MIIDXTCCAkWgAwIBAgIJAL4nGQm7xRqiMA0GCSqGSIb3DQEBCwUAMEUxCzAJBgNV
... (Base64 encoded DER) ...
-----END CERTIFICATE-----
```

> [!TIP]
> **Quick format identification:**
> - File starts with `-----BEGIN CERTIFICATE-----` → PEM
> - File is binary → DER or PKCS#12
> - Contains private key → PKCS#12 (.pfx/.p12)
> - Contains cert chain without private key → P7B

---

### 4.5 Self-Signed Certificates

> [!NOTE]
> A **self-signed certificate** is one where the
> issuer and subject are the same — the entity
> signed its own certificate without a CA.

```
Normal certificate:
  Subject: www.example.com
  Issuer:  DigiCert CA     ← different entity

Self-signed certificate:
  Subject: www.example.com
  Issuer:  www.example.com  ← same as subject
```

**When self-signed certs are used:**
- Root CA certificates (Root CAs self-sign their own
  cert — the trust anchor)
- Internal/test environments (not publicly trusted)
- Development servers (localhost)
- Lab environments (XCA lab in Session 10)

**Why browsers reject self-signed certs:**
- No trusted third party has verified the identity
- Anyone can create a self-signed cert for any domain
- MITM attackers use self-signed certs routinely

**Browser behavior:**
```
Self-signed cert encountered:
  → "Your connection is not private"
  → NET::ERR_CERT_AUTHORITY_INVALID
  → User must manually add exception (bypass warning)
```

> [!IMPORTANT]
> **Root CA certificates are technically
> self-signed** — but they are trusted because
> they are manually reviewed and pre-installed
> by OS/browser vendors into trust stores.
> Trust comes from the distribution process —
> not from the signature.

---

### 4.6 DSA — Digital Signature Algorithm

> [!NOTE]
> **DSA (Digital Signature Algorithm)** was proposed
> by NIST in **1991** and adopted as **FIPS 186**
> in **1994**.

| Property | Value |
|----------|-------|
| **Proposed by** | NIST (NSA designed) |
| **Year** | 1991 (proposed), 1994 (FIPS 186) |
| **Standard** | FIPS 186-4 (current) |
| **Mathematical basis** | Discrete Logarithm Problem (DLP) |
| **Purpose** | Digital signatures ONLY — no encryption |
| **Key sizes** | 1024-bit (old), 2048-bit, 3072-bit |
| **Status** | ⚠️ Aging — being replaced by ECDSA |

**DSA vs RSA for signatures:**

| Property | DSA | RSA |
|----------|-----|-----|
| **Purpose** | Signatures ONLY | Signatures + Encryption |
| **Basis** | DLP | Factoring |
| **Key size for 128-bit security** | 3072-bit | 3072-bit |
| **Speed** | Signing fast, verification slower | Both moderate |
| **Modern alternative** | ECDSA (256-bit ECC) | ECDSA (256-bit ECC) |

> [!NOTE]
> DSA requires a random nonce k per signature —
> same vulnerability as ECDSA. If k is reused
> or predictable → private key recovery.
> FIPS 186-4 specifies deterministic k generation
> to prevent this.

---

### 4.7 RSA Digital Signature vs RSA Encryption —
Key Direction

> [!NOTE]
> This is one of the most commonly confused
> concepts — and the most tested MCQ trap.

```
RSA ENCRYPTION (Confidentiality):
  Encrypt   → use RECEIVER'S PUBLIC KEY
  Decrypt   → use RECEIVER'S PRIVATE KEY

  "Only the receiver can read it"
  Anyone can send to receiver.
  Only receiver can open.

RSA DIGITAL SIGNATURE (Authentication):
  Sign      → use SENDER'S PRIVATE KEY
  Verify    → use SENDER'S PUBLIC KEY

  "Only I could have signed this"
  Only signer can create signature.
  Anyone can verify.
```

**Memory hook:**
```
ENCRYPTION: Lock with receiver's public key
            Unlock with receiver's private key

SIGNATURE:  Sign with MY private key
            Anyone verifies with MY public key
```

> [!IMPORTANT]
> The direction of key usage is OPPOSITE for
> encryption vs signatures:
> - Encryption: public key LOCKS; private key UNLOCKS
> - Signature: private key CREATES; public key VERIFIES
>
> Both use the same mathematical operation
> (modular exponentiation) — only the key and
> direction are different.

---

### 4.8 Non-Repudiation in Law

> [!NOTE]
> Non-repudiation has both a **technical** meaning
> and a **legal** meaning.

**Technical non-repudiation:**
The signer cannot deny signing because:
- Only their private key could have created the signature
- The signature is mathematically bound to the document

**Legal non-repudiation:**
Requires additional elements beyond just the
signature:
1. The private key was under the signer's exclusive
   control (not shared or compromised)
2. The signature was created at the time claimed
   (requires trusted timestamping)
3. The signed data has not been altered since signing
4. The CA that issued the signing certificate is
   trusted and the cert was valid at signing time

**Why technical non-repudiation alone is insufficient:**
```
Alice signs document with private key
Alice later claims: "My private key was stolen
  before I signed — it wasn't me!"

Without additional evidence:
  → Technical signature exists
  → But legal non-repudiation requires proving
    the key was under Alice's exclusive control
    at the time of signing
```

**Countermeasures:**
- **HSM (Hardware Security Module)** — private key
  never leaves hardware; creates audit trail
- **Trusted timestamping (RFC 3161)** — third party
  proves WHEN a document was signed
- **Audit logs** — system logs of signing events

---

### 4.9 Web of Trust vs Hierarchical PKI

> [!NOTE]

| Property | Web of Trust (PGP) | Hierarchical PKI (X.509) |
|----------|-------------------|-------------------------|
| **Trust anchor** | Distributed — community vouching | Centralized — Root CA |
| **CA equivalent** | None — users vouch for each other | Certificate Authority |
| **Scalability** | Poor at large scale | Excellent |
| **Central point of failure** | None | Root CA compromise is catastrophic |
| **Identity verification** | Personal — varies widely | Standardized by CA/Browser Forum |
| **Certificate format** | OpenPGP (RFC 4880) | X.509 v3 |
| **Used by** | PGP/GPG email encryption | TLS/HTTPS, S/MIME, code signing |
| **Revocation** | Key servers (informal) | CRL, OCSP (formal) |
| **Trust transitivity** | Alice trusts Bob; Bob trusts Carol → Alice partially trusts Carol | Alice trusts Root CA; Root CA signed Bob's cert → Alice trusts Bob |

---

### 4.10 Certificate Pinning

> [!NOTE]
> **Certificate Pinning** is the practice of
> hardcoding a specific certificate or public key
> in an application — rejecting any other cert
> even if it is signed by a trusted CA.

**Why it exists:**
```
Normal TLS verification:
  Browser trusts any cert signed by any trusted CA
  If a trusted CA issues a fraudulent cert for
  google.com → MITM attack succeeds
  (e.g., DigiNotar breach 2011)

With certificate pinning:
  App only accepts a specific cert/key for google.com
  Even a CA-signed cert for google.com is rejected
  if it does not match the pinned cert
```

**Two types of pinning:**
- **Certificate pinning** — pin the exact certificate
  (must update when cert expires)
- **Public key pinning (HPKP)** — pin the public key
  (survives certificate renewal as long as same key pair)

**HPKP (HTTP Public Key Pinning):**
- RFC 7469 — HTTP header-based pinning mechanism
- DEPRECATED in 2019 — too risky (misconfiguration
  could permanently lock users out of a site)
- Chrome removed HPKP support in 2018

**Certificate Transparency (CT) as alternative:**
CT logs provide a way to detect unauthorized cert
issuance without the risk of HPKP misconfigurations.

---

### 4.11 Certificate Transparency (CT)

> [!NOTE]
> **Certificate Transparency (CT)** is a framework
> for publicly logging all issued TLS certificates
> so that unauthorized or fraudulent certificates
> can be detected.

**Developed by:** Google (2013)
**Standard:** RFC 6962 (2013), RFC 9162 (2021 update)

**How it works:**
```
1. CA issues a certificate
2. CA MUST submit the certificate to one or more
   public CT logs (append-only Merkle tree logs)
3. CT log returns a Signed Certificate Timestamp (SCT)
4. CA embeds SCT in the certificate (or OCSP/TLS ext.)
5. Browsers verify SCT is present
   → If no SCT → certificate rejected (Chrome policy)
6. Anyone can monitor CT logs for unauthorized certs
   issued for their domain
```

**CT log properties:**
- **Append-only Merkle tree** — certificates can
  be added but never deleted or modified
- **Publicly auditable** — anyone can query the log
- **Cryptographically verifiable** — Merkle proofs
  guarantee log integrity

**Impact:**
- DigiNotar breach (2011) would have been detected
  within hours with CT
- Google Chrome requires CT since April 2018 —
  certs without SCTs are rejected

---

### 4.12 PKI Roles — RA, VA, Repository

> [!NOTE]

**Registration Authority (RA):**
- Performs identity verification on behalf of the CA
- Collects and validates applicant documentation
- Does NOT issue or sign certificates — CA does
- In small PKIs, the CA performs RA functions itself
- In enterprise PKIs, RA is a separate entity
  (e.g., HR department, security team)

**Validation Authority (VA):**
- Provides certificate status information
- Runs **OCSP responders** — responds to real-time
  certificate status queries
- Maintains CRL and OCSP infrastructure
- May be operated by the CA or a third-party service

**Certificate Repository:**
- Public directory or database of issued certificates
- Typically an **LDAP** (Lightweight Directory Access
  Protocol) directory
- Also publishes CRLs for download
- End entities and relying parties query the
  repository to obtain certificates

**CA hierarchy roles:**
```
Root CA:
  - Signs Intermediate CA certificates
  - Private key kept OFFLINE (air-gapped hardware)
  - Rarely used — only for CA cert issuance

Intermediate CA (Subordinate CA, Issuing CA):
  - Issues end-entity certificates day-to-day
  - Private key stored in HSM (online but protected)
  - If compromised → Root CA revokes its certificate
  - Limits blast radius of compromise vs Root CA
```

---

### 4.13 PKIX — Internet PKI Profile

> [!NOTE]
> **PKIX (Public Key Infrastructure for X.509)**
> is the IETF working group and profile that
> adapts X.509 for use on the Internet.

**Key PKIX RFCs:**

| RFC | Content |
|-----|---------|
| **RFC 5280** | Internet X.509 PKI Certificate and CRL Profile — the definitive PKIX reference |
| **RFC 6960** | Online Certificate Status Protocol (OCSP) |
| **RFC 3161** | Internet X.509 PKI Time-Stamp Protocol (TSP) |
| **RFC 2986** | PKCS#10 — Certificate Signing Request |
| **RFC 4210** | CMP — Certificate Management Protocol |
| **RFC 5652** | CMS — Cryptographic Message Syntax |

> [!TIP]
> **RFC 5280** is the single most important PKI RFC
> — it is the foundation of all TLS certificate
> validation on the Internet. Every browser follows
> RFC 5280 for certificate path validation.

---

## 5. Abbreviations Table

| Abbreviation | Full Form | One-Line Technical Meaning |
|---|---|---|
| PKI | Public Key Infrastructure | Complete ecosystem for managing public keys and digital certificates |
| CA | Certificate Authority | Trusted entity that issues and signs digital certificates |
| RA | Registration Authority | Verifies applicant identity before CA issues a certificate |
| VA | Validation Authority | Provides real-time certificate status — runs OCSP responders |
| CSR | Certificate Signing Request | Applicant's request to CA containing public key + identity info |
| CRL | Certificate Revocation List | CA-published list of revoked certificate serial numbers |
| OCSP | Online Certificate Status Protocol | Real-time certificate revocation checking protocol |
| DN | Distinguished Name | Hierarchical name format identifying certificate subject/issuer |
| CN | Common Name | Most specific part of DN — typically hostname or person name |
| SAN | Subject Alternative Name | X.509 v3 extension listing additional valid identities for a cert |
| EKU | Extended Key Usage | X.509 v3 extension restricting cert use (serverAuth, codeSigning) |
| DER | Distinguished Encoding Rules | Binary encoding format for X.509 certificates |
| PEM | Privacy Enhanced Mail | Base64 encoding of DER certificate — standard on Linux |
| PFX/P12 | Personal Information Exchange | PKCS#12 — contains cert + private key in one file |
| PKIX | Public Key Infrastructure for X.509 | IETF profile of X.509 for Internet use |
| CMS | Cryptographic Message Syntax | Standard for signed and encrypted messages (S/MIME, PKCS#7) |
| TSP | Time Stamp Protocol | RFC 3161 — trusted timestamping for digital signatures |
| SCT | Signed Certificate Timestamp | Proof that a cert was submitted to a CT log |
| CT | Certificate Transparency | Framework for public logging of all issued TLS certificates |
| HPKP | HTTP Public Key Pinning | Deprecated HTTP header for certificate key pinning |
| TBS | To Be Signed | The portion of an X.509 cert that is hashed and signed by the CA |
| ASN.1 | Abstract Syntax Notation One | Encoding standard used to structure X.509 certificate data |
| ITU-T | International Telecommunication Union — Standardization Sector | Body that defines X.509 standard |
| DSA | Digital Signature Algorithm | NIST/FIPS signature algorithm — DLP-based, signatures only |
| FIPS | Federal Information Processing Standard | US government cryptographic standards published by NIST |
| HSM | Hardware Security Module | Tamper-resistant hardware for secure cryptographic key operations |
| CPS | Certification Practice Statement | CA's document describing its operational procedures |
| CP | Certificate Policy | Document defining intended use and requirements for certificates |

---

## 6. Keywords + Concept Map

| Term | Definition | Connections | Use Cases |
|------|-----------|-------------|-----------|
| **PKI** | Ecosystem for public key trust at scale | CA, certificates, CRL, OCSP | All TLS/HTTPS, email security |
| **Digital Certificate** | CA-signed binding of public key to identity | X.509 v3, CSR, trust chain | TLS, code signing, S/MIME |
| **Digital Signature** | Private key hash signing for auth + integrity + non-repudiation | RSA/ECDSA, SHA-256, PKI | Legal docs, code signing, TLS |
| **Non-repudiation** | Unique to digital signatures — signer cannot deny | Private key, asymmetric only | Legal, financial, audit |
| **X.509 v3** | Current certificate standard — with extensions | ITU-T, RFC 5280, SAN, EKU | All TLS certificates |
| **CA** | Trusted issuer of certificates | Root CA, Intermediate CA, trust store | PKI foundation |
| **Root CA** | Self-signed trust anchor — in browser trust store | Offline private key, cross-certification | Browser/OS trust store |
| **Intermediate CA** | CA signed by Root CA — issues end-entity certs | Limits compromise blast radius | Day-to-day cert issuance |
| **CSR** | Certificate request containing public key + identity | PKCS#10, RFC 2986 | Certificate enrollment |
| **Trust Chain** | Sequence from end-entity cert to trusted Root CA | Chain validation, RFC 5280 | TLS certificate verification |
| **SAN** | Extension listing all valid identities for a cert | Replaced CN matching, wildcard | Multi-domain TLS certs |
| **Certificate Pinning** | Hardcoded cert/key in app — rejects all others | HPKP deprecated, CT preferred | Mobile apps, high-security |
| **Certificate Transparency** | Public append-only log of all issued certs | Merkle tree, SCT, RFC 6962 | Detect fraudulent cert issuance |
| **PEM format** | Base64 of DER cert — standard Linux/Apache format | .pem, .crt extensions | OpenSSL, TLS configuration |
| **PKCS#12** | Bundle of cert + private key | .pfx/.p12, Windows IIS | Certificate import/export |

---

## 7. Quick Reference Cheatsheet

### 🔸 Digital Signature — Key Direction

```
SIGNING:     Use SENDER'S PRIVATE KEY
VERIFYING:   Use SENDER'S PUBLIC KEY

ENCRYPTING:  Use RECEIVER'S PUBLIC KEY
DECRYPTING:  Use RECEIVER'S PRIVATE KEY
```

---

### 🔸 Digital Signature — Properties Table

| Property | Digital Signature | HMAC | Plain Hash |
|----------|-----------------|------|-----------|
| Key type | Private key | Shared secret | None |
| Integrity | ✅ | ✅ | ✅ |
| Authentication | ✅ | ✅ | ❌ |
| Non-repudiation | ✅ | ❌ | ❌ |
| Speed | Slow | Fast | Fast |

---

### 🔸 X.509 Certificate — Key Fields

| Field | Description |
|-------|-------------|
| Version | v3 (current) |
| Serial Number | Unique per CA |
| Issuer | CA's Distinguished Name |
| Subject | Owner's Distinguished Name |
| Valid From / To | Validity period |
| Subject Public Key | The actual public key |
| Signature Algorithm | e.g., SHA256withRSA |
| CA Signature | CA's digital signature over all above |

---

### 🔸 Certificate Verification Steps

```
1. Chain validation → end-entity to trusted Root CA
2. Signature verification → CA's signature valid?
3. Validity period → not expired?
4. Revocation check → CRL or OCSP
5. Name matching → CN/SAN matches hostname?
6. Key Usage → permitted for intended purpose?
```

---

### 🔸 Certificate Encoding Formats

| Format | Extension | Binary/Text | Contains |
|--------|-----------|------------|---------|
| DER | .der, .cer | Binary | Cert only |
| PEM | .pem, .crt | Base64 text | Cert, key, or chain |
| PKCS#12 | .pfx, .p12 | Binary | Cert + key + chain |
| PKCS#7 | .p7b | Base64 or binary | Cert chain (no key) |

---

### 🔸 PKI Trust Models

| Model | Used By | Trust Anchor |
|-------|---------|-------------|
| Hierarchical | TLS/HTTPS, commercial PKI | Root CA in trust store |
| Web of Trust | PGP/GPG email | Users vouch for each other |
| Cross-Certification | Multi-org PKI | Cross-signed roots |
| Bridge CA | US Federal PKI | Bridge CA hub |

---

### 🔸 NIST/FIPS References for This Session

| Standard | Content |
|----------|---------|
| FIPS 186-4 | DSA standard — digital signature algorithms |
| RFC 5280 | Internet X.509 PKI — PKIX profile |
| RFC 2986 | PKCS#10 — Certificate Signing Request format |
| RFC 6960 | OCSP — Online Certificate Status Protocol |
| RFC 6962 | Certificate Transparency |
| ITU-T X.509 | X.509 certificate standard |

---

## 8. Session Revision Snapshot

### ⚡ TL;DR — 5 Bullets

- ✅ PKI = ecosystem of CA, certificates, CRL, OCSP
  that makes public key trust practical at scale —
  it solves the "how do I know whose key this is?"
  problem using trusted third parties (CAs)
- ✅ Digital signature = Hash(message) signed with
  PRIVATE key — verified with PUBLIC key — provides
  Authentication + Integrity + Non-repudiation
  (non-repudiation is ONLY possible with asymmetric
  private keys — NOT with HMAC)
- ✅ Digital certificate = CA-signed X.509 v3 document
  binding a public key to an identity — contains
  subject, issuer, validity, public key, CA signature,
  and v3 extensions (SAN, Key Usage, EKU)
- ✅ Certificate verification requires ALL six checks:
  chain validation, signature, validity period,
  revocation (CRL/OCSP), name matching, key usage —
  failing ANY one check → certificate rejected
- ✅ Trust hierarchy: Root CA (self-signed, in trust
  store, offline key) → Intermediate CA (signed by
  Root, issues end-entity certs) → End Entity Cert
  (signed by Intermediate) — Root CA compromise
  is catastrophic; Intermediate CA compromise
  is limited and recoverable

---

### 🎯 MCQ-Likely Concepts — Everything Examiners Love

| Concept | Why It's Tricky |
|---------|----------------|
| Sign with PRIVATE key; Verify with PUBLIC key | Students say "sign with public key" — wrong |
| HMAC has NO non-repudiation; Digital Sig DOES | Both provide integrity+auth — non-repudiation is the difference |
| Root CA is SELF-SIGNED | All other certs are CA-signed — Root is the exception |
| Root CA private key kept OFFLINE | Security measure — Intermediate CAs are online |
| CSR format = PKCS#10 / RFC 2986 | Specific standard for CSR |
| X.509 v3 introduced extensions | v1 had no extensions — v3 is the current standard |
| SAN replaced CN for hostname matching | CN matching was deprecated in 2017 (Chrome) |
| Wildcard `*.example.com` matches ONE level only | `sub.api.example.com` NOT matched |
| RFC 5280 = PKIX profile (not the X.509 ITU standard itself) | Two separate documents |
| Certificate Transparency required by Chrome since 2018 | SCT must be present |
| DSA = signatures ONLY — no encryption | RSA does both; DSA does signatures only |
| DER = binary; PEM = Base64 of DER | Encoding format distinction |
| PKCS#12 (.pfx) contains private key | PEM cert files don't contain private key by default |
| Non-repudiation requires HSM + timestamp for legal validity | Technical signature alone insufficient in court |
| Intermediate CA limits blast radius of compromise | Key design principle of CA hierarchy |
| DigiNotar 2011 — CA compromise example | Canonical real-world PKI failure |

---

<details>
<summary>🔬 Lab Content (Session 07 — No Lab Assigned)</summary>

No lab is assigned for Session 07 in the syllabus.

Lab work directly related to Session 07 concepts
begins in **Session 09 (XCA tool)** which covers:
- Creating a CA using XCA
- Issuing certificates from that CA
- Digitally signing Word and PDF documents
  using created certificates

And **Session 10 (XCA tool)** which covers:
- Full PKI hierarchy (CA → end-entity cert)
- Creating HTTPS certificates
- Importing into browser trust store

And **Session 13 (OpenSSL)** which covers:
- Root CA + Sub CA hierarchy from command line
- Full certificate chain creation and validation

**Theory ↔ Lab Connection:**

| Session 07 Concept | Lab Demonstration |
|-------------------|------------------|
| X.509 certificate structure | XCA shows all certificate fields visually |
| Certificate chain | Session 10 XCA — Root CA → cert hierarchy |
| CSR creation process | XCA + OpenSSL both create CSRs |
| CA signing a certificate | XCA Session 09/10 — CA signs end-entity cert |
| Self-signed vs CA-signed | Session 09/10 — contrast both in XCA |
| PEM / DER formats | OpenSSL Session 13 — export in both formats |
| Certificate verification | Session 10 — import to browser, remove warning |

All lab guides in `3-Labs/` folder.

</details>

---