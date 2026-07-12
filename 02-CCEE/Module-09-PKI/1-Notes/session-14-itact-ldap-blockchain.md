# Session 14 — IT Act, LDAP / Active Directory
& Introduction to Blockchain

## 📑 Table of Contents

- [1. IT Act — Information Technology Act
  2000](#1-it-act--information-technology-act-2000)
  - [1.1 What is the IT Act?](#11-what-is-the-it-act)
  - [1.2 IT Act — Key
    Objectives](#12-it-act--key-objectives)
  - [1.3 IT Act — Structure and
    Amendments](#13-it-act--structure-and-amendments)
  - [1.4 Digital Signatures Under IT
    Act](#14-digital-signatures-under-it-act)
  - [1.5 Electronic Signatures Under IT
    Act](#15-electronic-signatures-under-it-act)
  - [1.6 Controller of Certifying
    Authorities (CCA)](#16-controller-of-certifying-authorities-cca)
  - [1.7 Certifying Authorities in India](#17-certifying-authorities-in-india)
  - [1.8 Key Offences and Penalties Under
    IT Act](#18-key-offences-and-penalties-under-it-act)
  - [1.9 IT Act — Key Sections
    Reference](#19-it-act--key-sections-reference)
  - [1.10 IT Act Exclusions —
    What Electronic Signatures Cannot
    Do](#110-it-act-exclusions--what-electronic-signatures-cannot-do)
- [2. LDAP and Active Directory](#2-ldap-and-active-directory)
  - [2.1 LDAP — Lightweight Directory Access
    Protocol](#21-ldap--lightweight-directory-access-protocol)
  - [2.2 LDAP Directory
    Structure](#22-ldap-directory-structure)
  - [2.3 LDAP Operations](#23-ldap-operations)
  - [2.4 LDAP Authentication](#24-ldap-authentication)
  - [2.5 Active Directory — Microsoft's
    Directory Service](#25-active-directory--microsofts-directory-service)
  - [2.6 Active Directory
    Components](#26-active-directory-components)
  - [2.7 Active Directory and PKI](#27-active-directory-and-pki)
  - [2.8 LDAP vs Active Directory](#28-ldap-vs-active-directory)
- [3. Introduction to
  Blockchain](#3-introduction-to-blockchain)
  - [3.1 What is Blockchain?](#31-what-is-blockchain)
  - [3.2 Why Blockchain — The Problem It
    Solves](#32-why-blockchain--the-problem-it-solves)
  - [3.3 Blockchain Core
    Concepts](#33-blockchain-core-concepts)
  - [3.4 How a Block is Structured](#34-how-a-block-is-structured)
  - [3.5 How Blockchain Achieves
    Tamper-Resistance](#35-how-blockchain-achieves-tamper-resistance)
  - [3.6 Consensus
    Mechanisms](#36-consensus-mechanisms)
  - [3.7 Types of Blockchain](#37-types-of-blockchain)
  - [3.8 Blockchain and
    Cryptography](#38-blockchain-and-cryptography)
  - [3.9 Blockchain Use
    Cases](#39-blockchain-use-cases)
- [4. 📌 Extra Notes](#4--extra-notes)
  - [4.1 IT Act 2000 vs IT
    (Amendment) Act 2008](#41-it-act-2000-vs-it-amendment-act-2008)
  - [4.2 Sections 43, 65, 66 — Cybercrime
    Provisions](#42-sections-43-65-66--cybercrime-provisions)
  - [4.3 IT Act and Intermediary
    Liability](#43-it-act-and-intermediary-liability)
  - [4.4 LDAP Schema and Object
    Classes](#44-ldap-schema-and-object-classes)
  - [4.5 Active Directory Certificate
    Services (ADCS)](#45-active-directory-certificate-services-adcs)
  - [4.6 Group Policy Objects (GPO)
    and Security](#46-group-policy-objects-gpo-and-security)
  - [4.7 Bitcoin and Blockchain](#47-bitcoin-and-blockchain)
  - [4.8 Ethereum and Smart
    Contracts](#48-ethereum-and-smart-contracts)
  - [4.9 Public vs Private vs Consortium
    Blockchain](#49-public-vs-private-vs-consortium-blockchain)
  - [4.10 Blockchain Attacks and
    Vulnerabilities](#410-blockchain-attacks-and-vulnerabilities)
  - [4.11 Cryptographic Primitives in
    Blockchain](#411-cryptographic-primitives-in-blockchain)
  - [4.12 PKI and Blockchain —
    Comparison](#412-pki-and-blockchain--comparison)
  - [4.13 Digital Signatures in Legal
    Disputes — India](#413-digital-signatures-in-legal-disputes--india)
- [5. Abbreviations Table](#5-abbreviations-table)
- [6. Keywords + Concept Map](#6-keywords--concept-map)
- [7. Quick Reference Cheatsheet](#7-quick-reference-cheatsheet)
- [8. Session Revision Snapshot](#8-session-revision-snapshot)

---

## 1. IT Act — Information Technology Act 2000

### 1.1 What is the IT Act?

The **Information Technology Act 2000** is India's
primary legislation governing electronic commerce,
digital signatures, cybercrime, and the legal
framework for electronic records and transactions.

| Property | Detail |
|----------|--------|
| **Full title** | The Information Technology Act, 2000 |
| **Enacted** | June 9, 2000 |
| **Came into force** | October 17, 2000 |
| **Amended by** | IT (Amendment) Act 2008 (came into force Feb 5, 2009) |
| **Nodal ministry** | Ministry of Electronics and Information Technology (MeitY) |
| **Purpose** | Provide legal recognition for electronic records, digital signatures, and regulate cybercrime |
| **Based on** | UNCITRAL Model Law on Electronic Commerce (1996) |

> [!IMPORTANT]
> The IT Act 2000 is the foundational law for
> all digital PKI operations in India:
> - It gives legal validity to **digital signatures**
> - It establishes the **CCA (Controller of
>   Certifying Authorities)** as the apex PKI
>   regulatory body
> - It defines the legal framework for
>   **Certifying Authorities** to issue DSCs
> - It defines criminal liability for cybercrime

---

### 1.2 IT Act — Key Objectives

| Objective | Description |
|-----------|-------------|
| **Legal recognition** | Give legal validity to electronic records and digital signatures — equivalent to paper documents and handwritten signatures |
| **E-commerce enablement** | Facilitate electronic commercial transactions |
| **PKI framework** | Establish the framework for digital signature certificates and CAs |
| **Cybercrime prevention** | Define offences and penalties for computer-related crimes |
| **Government e-services** | Enable government to issue electronic notifications and records |
| **Data protection** | Basic provisions for protection of sensitive data (expanded in later rules) |

---

### 1.3 IT Act — Structure and Amendments

**IT Act 2000 structure:**
- **94 Sections** organized into 13 Chapters
- **2 Schedules** (First Schedule: documents
  excluded; Second Schedule: electronic signature
  methods)

**Key Chapters:**

| Chapter | Subject |
|---------|---------|
| Chapter II (Sec 3-10) | Digital Signatures |
| Chapter III (Sec 11-15) | Electronic Governance |
| Chapter VI (Sec 35-42) | Regulation of Certifying Authorities |
| Chapter VII (Sec 43-45) | Penalties and Adjudication |
| Chapter IX (Sec 65-74) | Offences |
| Chapter X (Sec 75-78) | Jurisdiction and network service providers |

**IT (Amendment) Act 2008 — key additions:**
- Added **Section 66A** (messaging offences —
  later struck down by Supreme Court in 2015)
- Added **Section 66B–66F** (specific cyber crimes)
- Added **Section 43A** (compensation for failure
  to protect sensitive data)
- Changed "digital signature" provisions to include
  "electronic signatures" (broader category)
- Added intermediary liability provisions

---

### 1.4 Digital Signatures Under IT Act

**Section 2(1)(p) — Definition:**
> "Digital signature" means authentication of
> any electronic record by a subscriber by means
> of an electronic method or procedure in
> accordance with the provisions of Section 3.

**Section 3 — Authentication of Electronic Records:**
Digital signatures under IT Act must:
1. Use asymmetric cryptography (public/private
   key pair)
2. Use a hash function
3. The private key must be unique to the subscriber
4. The key pair must be generated by a licensed
   Certifying Authority
5. The public key must be certified by a licensed CA

**Legal validity (Section 5):**
> Where any law provides that information shall
> be authenticated by affixing a signature, such
> requirement shall be deemed to have been
> satisfied if authenticated by means of a
> digital signature.

**What this means:**
A digital signature on an electronic document
is legally equivalent to a handwritten signature
on a paper document — for all purposes covered
by the IT Act.

> [!IMPORTANT]
> The IT Act defines two separate categories:
>
> **Digital Signature** (Section 2(1)(p) + Section 3):
> Specifically uses asymmetric key pairs from
> a licensed CA → higher legal standing →
> created using physical DSC (USB token)
>
> **Electronic Signature** (Section 2(1)(ta)):
> Broader category → includes Aadhaar-based
> e-Sign → added by 2008 amendment

---

### 1.5 Electronic Signatures Under IT Act

**Section 2(1)(ta) — Electronic Signature:**
> "Electronic signature" means authentication of
> any electronic record by a subscriber by means
> of the electronic technique specified in the
> Second Schedule.

**Second Schedule methods:**

| Method | Description |
|--------|-------------|
| **Aadhaar e-authentication** | Aadhaar-based OTP/biometric verification — basis for e-Sign |
| **PIN/Password-based methods** | Where applicable |
| **Other methods notified** | MeitY may add other approved methods |

**Digital Signature vs Electronic Signature:**

| Property | Digital Signature | Electronic Signature |
|----------|-----------------|---------------------|
| **Section** | 2(1)(p) + Section 3 | 2(1)(ta) + Second Schedule |
| **Key type** | Asymmetric — from licensed CA | Technology defined in Schedule 2 |
| **Example** | DSC on USB token (Class 3) | Aadhaar-based e-Sign |
| **Legal standing** | Highest | Valid for most purposes |
| **Typical use** | e-Tendering, court filing | Tax filing, bank KYC |

---

### 1.6 Controller of Certifying Authorities (CCA)

**CCA (Controller of Certifying Authorities)**
is established under **Section 17** of the IT Act
as the apex regulatory body for PKI in India.

| Property | Detail |
|----------|--------|
| **Established by** | Section 17, IT Act 2000 |
| **Under** | Ministry of Electronics and Information Technology (MeitY) |
| **Headquarters** | New Delhi |
| **Website** | cca.gov.in |
| **Powers** | License CAs, regulate DSC issuance, maintain Root CA (RCAI), investigate violations |

**CCA Functions:**

| Function | Description |
|----------|-------------|
| **Licensing** | Grant licenses to Certifying Authorities to issue DSCs |
| **Regulation** | Audit and monitor CAs for compliance |
| **Root CA** | Operate the Root Certifying Authority of India (RCAI) |
| **Repository** | Maintain national repository of DSC-related information |
| **Revocation** | Direct CAs to revoke certificates |
| **Investigation** | Investigate violations of IT Act related to DSC |

**CCA Hierarchy:**
```
CCA (Controller of Certifying Authorities)
    │
    ├── RCAI (Root Certifying Authority of India)
    │       ← CCA operates RCAI
    │       ← Root CA for all Indian PKI
    │
    └── Licensed CAs (Certifying Authorities)
            ← Signed by RCAI
            ← Issue DSCs to subscribers
            Examples:
              eMudhra, (n)Code Solutions,
              SafeScrypt, Capricorn CA,
              NSDL Database Management Limited
```

---

### 1.7 Certifying Authorities in India

Certifying Authorities (CAs) licensed by CCA
issue **Digital Signature Certificates (DSCs)**
to subscribers.

**DSC Classes (pre-2021):**

| Class | Purpose | Identity Verification |
|-------|---------|----------------------|
| **Class 1** | Personal email — low assurance | Email/username verification |
| **Class 2** | Business use — MCA, income tax filings | Based on submitted documents |
| **Class 3** | High-assurance — e-tendering, e-bidding | In-person physical verification |

> [!NOTE]
> **Post-2021 DSC Simplification:**
> CCA India rationalized the DSC classes in 2021.
> Class 2 certificates were discontinued for
> individual subscribers — all individual DSCs
> now require personal appearance/video-based KYC
> (similar to earlier Class 3 requirements).
>
> Organizations can still issue organization-level
> DSCs through a simplified process.
>
> The classification is now primarily based on
> purpose (individual/organization) rather
> than Class 1/2/3 naming.

**Licensed CAs in India:**

| CA | Full Name | Notes |
|----|-----------|-------|
| **eMudhra** | eMudhra Limited | Largest DSC provider in India |
| **(n)Code Solutions** | (n)Code Solutions CA | GNFC subsidiary |
| **SafeScrypt** | Sify SafeScrypt CA | Sify Technologies subsidiary |
| **Capricorn CA** | Capricorn Identity Services | |
| **NSDL** | NSDL Database Management | For NSDL-related services |
| **CDAC** | Centre for Development of Advanced Computing | Government use |
| **IDRBT** | Institute for Development and Research in Banking Technology | Banking sector |

**Common uses of DSC in India:**
- Income tax e-filing (ITR signing)
- GST return filing
- MCA (Ministry of Corporate Affairs) filings
- e-Tendering / e-Procurement
- Aadhaar e-Sign integration
- Court e-filing (specific courts)
- ROC (Registrar of Companies) filings

---

### 1.8 Key Offences and Penalties Under IT Act

**Chapter VII — Penalties (civil):**

| Section | Offence | Penalty |
|---------|---------|---------|
| **Section 43** | Unauthorized access, damage to computer systems | Compensation up to ₹1 crore |
| **Section 43A** | Failure to protect sensitive personal data (body corporates) | Compensation — no fixed limit |
| **Section 44** | Failure to furnish information to CCA | Up to ₹1.5 lakh per failure |
| **Section 45** | Residual penalty clause | Up to ₹25,000 |

**Chapter IX — Offences (criminal):**

| Section | Offence | Punishment |
|---------|---------|-----------|
| **Section 65** | Tampering with computer source code | Up to 3 years imprisonment OR ₹2 lakh fine OR both |
| **Section 66** | Computer-related offences (hacking) | Up to 3 years imprisonment OR ₹5 lakh fine OR both |
| **Section 66B** | Receiving stolen computer resources | Up to 3 years OR ₹1 lakh fine |
| **Section 66C** | Identity theft | Up to 3 years AND ₹1 lakh fine |
| **Section 66D** | Cheating by personation using computer | Up to 3 years AND ₹1 lakh fine |
| **Section 66E** | Violation of privacy (capturing images) | Up to 3 years OR ₹2 lakh fine |
| **Section 66F** | Cyber terrorism | Up to life imprisonment |
| **Section 67** | Publishing obscene material electronically | Up to 3 years AND ₹5 lakh fine (first offence) |
| **Section 70** | Unauthorized access to protected systems | Up to 10 years AND fine |
| **Section 72** | Breach of confidentiality and privacy by official | Up to 2 years OR ₹1 lakh fine |

> [!IMPORTANT]
> **Section 66F — Cyber terrorism** is the
> most severe offence under IT Act — punishable
> with **up to life imprisonment**.
> It covers attacks on critical infrastructure,
> government computer systems, or any act that
> threatens national security or unity.

---

### 1.9 IT Act — Key Sections Reference

| Section | Subject |
|---------|---------|
| **Section 2** | Definitions — digital signature, electronic record, etc. |
| **Section 3** | Authentication of electronic records using digital signature |
| **Section 4** | Legal recognition of electronic records |
| **Section 5** | Legal recognition of digital signatures |
| **Section 6** | Use of electronic records in government |
| **Section 10A** | Validity of contracts formed electronically |
| **Section 17** | Appointment of Controller and Deputy Controllers |
| **Section 18** | Functions of the Controller |
| **Section 35** | Certifying Authority to issue Digital Signature Certificate |
| **Section 37** | Suspension of Digital Signature Certificate |
| **Section 38** | Revocation of Digital Signature Certificate |
| **Section 43** | Penalty for unauthorized access |
| **Section 43A** | Compensation for failure to protect data |
| **Section 66** | Computer-related offences (hacking) |
| **Section 66C** | Punishment for identity theft |
| **Section 66F** | Punishment for cyber terrorism |
| **Section 70** | Protected system |
| **Section 79** | Exemption of intermediary from liability |
| **Section 84A** | Modes of encryption — notified by Government |
| **Section 84B** | Punishment for publishing false digital signature certificates |

---

### 1.10 IT Act Exclusions — What Electronic
Signatures Cannot Do

**First Schedule to IT Act** — documents excluded
from electronic signature validity:

| Excluded Document | Reason |
|------------------|--------|
| **Negotiable instruments** | Cheques, promissory notes, bills of exchange |
| **Power of attorney** | Requires physical signature for legal validity |
| **Trust deeds** | Must be executed physically |
| **Will or codicil** | Requires physical witnessing |
| **Any contract for sale of immovable property** | Sale deeds must be registered physically |
| **Documents requiring registration** | Under Registration Act 1908 — must be physically registered |

> [!IMPORTANT]
> These exclusions apply to BOTH electronic
> signatures (e-Sign) AND digital signatures
> (physical DSC). The IT Act simply does not
> extend to these categories — they still require
> physical execution.

---

## 2. LDAP and Active Directory

### 2.1 LDAP — Lightweight Directory Access
Protocol

**LDAP (Lightweight Directory Access Protocol)**
is a protocol for accessing and maintaining
distributed directory information services over
an IP network.

| Property | Detail |
|----------|--------|
| **Full name** | Lightweight Directory Access Protocol |
| **Current version** | LDAPv3 — RFC 4511 (2006) |
| **Predecessor** | DAP (Directory Access Protocol) — too heavy |
| **Based on** | X.500 Directory Services |
| **Port** | 389 (unencrypted) |
| **Secure port** | 636 (LDAPS — LDAP over TLS) |
| **Transport** | TCP |
| **Data format** | ASN.1 BER/DER encoded |

**What a directory service stores:**
```
A directory service is a specialized database
optimized for READ operations (rarely written).

Stores information about:
  → Users (name, email, phone, department)
  → Groups (members, permissions)
  → Computers (hostname, OS, location)
  → Printers and resources
  → Certificates and public keys
  → Network services and configurations
```

> [!NOTE]
> **Directory vs Database:**
> A regular relational database (MySQL) is
> optimized for complex queries and frequent
> writes. A directory service (LDAP) is
> optimized for simple lookup queries and
> MANY reads — very few writes.
> LDAP is purpose-built for identity and
> resource lookup in enterprise networks.

---

### 2.2 LDAP Directory Structure

LDAP organizes data as a **hierarchical tree**
called the **DIT (Directory Information Tree)**.

```
DIT Structure Example:

dc=example,dc=com          ← Domain Component (root/suffix)
  │
  ├── ou=Users             ← Organizational Unit
  │     ├── cn=Alice Smith
  │     │     uid: asmith
  │     │     mail: alice@example.com
  │     │     memberOf: cn=Engineering
  │     │
  │     └── cn=Bob Jones
  │
  ├── ou=Groups
  │     └── cn=Engineering
  │           member: cn=Alice Smith,ou=Users,dc=example,dc=com
  │
  ├── ou=Computers
  │     └── cn=LAPTOP001
  │
  └── ou=ServiceAccounts
        └── cn=svc-backup
```

**LDAP naming components:**

| Component | Abbreviation | Example |
|-----------|-------------|---------|
| Domain Component | dc | dc=example, dc=com |
| Organizational Unit | ou | ou=Users |
| Common Name | cn | cn=Alice Smith |
| User ID | uid | uid=asmith |
| Country | c | c=IN |
| Organization | o | o=Example Corp |
| State | st | st=Maharashtra |
| Locality | l | l=Pune |

**Distinguished Name (DN):**
The full unique path to an entry:
```
cn=Alice Smith,ou=Users,dc=example,dc=com
```
Read from most specific (left) to least
specific (right).

**Relative Distinguished Name (RDN):**
The component that distinguishes an entry
from siblings at the same level:
```
cn=Alice Smith  ← RDN within ou=Users
```

---

### 2.3 LDAP Operations

LDAPv3 defines these core operations:

| Operation | Description |
|-----------|-------------|
| **Bind** | Authenticate to the LDAP server |
| **Unbind** | Terminate the LDAP session |
| **Search** | Query the directory for entries |
| **Compare** | Test if an attribute has a specific value |
| **Add** | Create a new entry |
| **Delete** | Remove an entry |
| **Modify** | Change attributes of an entry |
| **ModifyDN** | Rename or move an entry |
| **Abandon** | Cancel a previous operation |
| **Extended** | Extended operations (e.g., password change, StartTLS) |

**LDAP Search — key parameters:**

| Parameter | Description | Example |
|-----------|-------------|---------|
| **Base DN** | Where to start the search | `ou=Users,dc=example,dc=com` |
| **Scope** | How deep to search | Base / One Level / Subtree |
| **Filter** | What to look for | `(uid=asmith)` |
| **Attributes** | Which attributes to return | `cn mail phone` |
| **Size limit** | Max entries to return | 100 |
| **Time limit** | Max seconds for search | 30 |

**LDAP filter examples:**
```
(uid=asmith)                    → exact match
(cn=Alice*)                     → wildcard
(mail=*@example.com)            → domain match
(&(objectClass=user)(enabled=TRUE)) → AND filter
(|(uid=asmith)(uid=bjones))     → OR filter
(!cn=Bob)                       → NOT filter
```

---

### 2.4 LDAP Authentication

**LDAP authentication using BIND operation:**

**Simple BIND (most common):**
```
Application → LDAP Server:
  BIND request:
    version: 3
    name: "cn=Alice Smith,ou=Users,dc=example,dc=com"
    authentication: simple
    password: "AlicePassword123"

LDAP Server checks password against stored hash

LDAP Server → Application:
  BIND response: success (0) or error code
```

> [!WARNING]
> Simple BIND sends the **Distinguished Name
> (DN) and password** to the server. This MUST
> be protected by TLS (LDAPS on port 636 or
> STARTTLS on port 389) — otherwise credentials
> are sent in cleartext!

**SASL BIND (stronger):**
SASL (Simple Authentication and Security Layer)
allows multiple authentication mechanisms:
- SASL/GSSAPI — Kerberos (Windows AD)
- SASL/EXTERNAL — TLS client certificate
- SASL/DIGEST-MD5 — challenge-response

**Anonymous BIND:**
```
BIND with empty DN and empty password
→ Read-only access to public directory entries
→ Used for certificate lookup, CRL retrieval
```

---

### 2.5 Active Directory — Microsoft's
Directory Service

**Active Directory (AD)** is Microsoft's
enterprise directory service — implementing
LDAP plus many additional capabilities.

| Property | Detail |
|----------|--------|
| **Full name** | Active Directory Domain Services (AD DS) |
| **Introduced** | Windows 2000 Server |
| **Protocol** | LDAP (directory access) + Kerberos (authentication) + DNS |
| **Replacement for** | Windows NT 4.0 domains |
| **Authentication** | Kerberos (primary) + NTLM (legacy fallback) |
| **Administration** | Active Directory Users and Computers (ADUC), Group Policy Management |

**Active Directory provides:**
- **Authentication** — Kerberos SSO for all domain users
- **Authorization** — Group Policy for security settings
- **Directory** — User, computer, group management via LDAP
- **Certificate Services** — ADCS for internal PKI
- **Federation** — ADFS for SAML/OIDC integration

---

### 2.6 Active Directory Components

**Logical components:**

| Component | Description |
|-----------|-------------|
| **Domain** | Administrative boundary — single LDAP namespace (e.g., corp.example.com) |
| **Tree** | Multiple domains sharing a contiguous namespace |
| **Forest** | Top-level AD container — one or more trees sharing schema and GC |
| **OU (Organizational Unit)** | Container within a domain for organizing objects and applying GPO |
| **Domain Controller (DC)** | Server running AD DS — stores the AD database (NTDS.dit) |
| **Global Catalog (GC)** | Partial replica of all objects in the forest — for cross-domain lookups |
| **Trust** | Relationship allowing users from one domain to access resources in another |

**Physical components:**

| Component | Description |
|-----------|-------------|
| **NTDS.dit** | Active Directory database file |
| **SYSVOL** | Shared directory for Group Policy files and scripts |
| **Site** | Physical network location — used for optimizing DC replication |
| **Subnet** | IP address range associated with a site |

**AD object types:**

| Object | Description |
|--------|-------------|
| **User** | Individual account |
| **Computer** | Machine account |
| **Group** | Collection of users/computers |
| **Contact** | External person (no login) |
| **Printer** | Shared printer |
| **GPO** | Group Policy Object |
| **Service Principal** | Service account with Kerberos SPN |

---

### 2.7 Active Directory and PKI

**Active Directory Certificate Services (ADCS)**
is Microsoft's PKI solution integrated with AD:

```
AD Forest
  │
  └── Enterprise Root CA (ADCS)
        │ Signed by ADCS Root CA
        ├── Issuing CA 1
        │     └── Issues certs to domain users/computers
        └── Issuing CA 2
              └── Issues certs for specific services
```

**What ADCS provides:**
- **Auto-enrollment** — Computers and users
  automatically receive certificates via Group
  Policy without manual requests
- **Certificate templates** — Pre-defined cert
  types (User, Computer, Web Server, Kerberos)
- **Smart card enrollment** — Issue smart card
  certs to AD users
- **S/MIME certificates** — Issue emailProtection
  certs for Outlook/Exchange
- **OCSP responder** — Integrated revocation
  checking
- **CRL publication** — Automatic CRL publishing
  to AD and HTTP

**AD + EAP-TLS integration:**
```
Corporate laptops automatically receive
machine certificates via ADCS auto-enrollment
     ↓
When connecting to corporate Wi-Fi (WPA2-Enterprise):
EAP-TLS uses the machine certificate
     ↓
RADIUS server validates machine cert against
AD/ADCS
     ↓
Only domain-joined, certificate-bearing devices
get network access ✅
```

---

### 2.8 LDAP vs Active Directory

| Property | LDAP | Active Directory |
|----------|------|----------------|
| **Type** | Open protocol (RFC 4511) | Microsoft proprietary service |
| **Relationship** | Protocol | Service that implements LDAP |
| **Authentication** | Simple BIND, SASL | Kerberos (primary), NTLM, LDAP |
| **OS** | Any (OpenLDAP on Linux) | Windows Server only |
| **GPO** | ❌ Not supported | ✅ Group Policy for centralized config |
| **Auto-enrollment** | ❌ Manual | ✅ Certificate auto-enrollment |
| **Replication** | OpenLDAP syncrepl | AD-specific multi-master replication |
| **Scalability** | Good | Excellent for enterprise |
| **PKI integration** | Manual | Native (ADCS) |

---

## 3. Introduction to Blockchain

### 3.1 What is Blockchain?

A **blockchain** is a distributed, append-only
ledger — a chain of cryptographically linked
blocks of data — maintained across a peer-to-peer
(P2P) network where no single central authority
controls it.

| Property | Detail |
|----------|--------|
| **First described** | Satoshi Nakamoto, "Bitcoin: A Peer-to-Peer Electronic Cash System" (2008) |
| **First implementation** | Bitcoin (launched January 3, 2009) |
| **Type** | Distributed ledger technology (DLT) |
| **Core properties** | Decentralized, immutable, transparent, append-only |

> [!NOTE]
> **Satoshi Nakamoto** is the pseudonymous
> person/group who published the Bitcoin
> whitepaper in October 2008 and launched
> the Bitcoin network in January 2009.
> The true identity of Satoshi Nakamoto
> remains unknown.

---

### 3.2 Why Blockchain — The Problem It Solves

**The Double-Spend Problem (and the need for
trusted third parties):**

```
Digital currency problem:
  Alice has $100 digital token
  Alice sends same $100 to Bob AND Carol
  (copies the digital file — both transactions valid)
  → Double spending → money loses value

Traditional solution: Trust a central authority
  → Bank keeps a ledger
  → Bank says "Alice sent $100 to Bob"
  → Bank prevents double spending
  → BUT: Requires trusting the bank

Blockchain solution:
  → Distributed ledger — everyone has a copy
  → Transactions validated by majority consensus
  → No single authority — no single point of
    trust or failure
  → Cryptographic linking prevents altering history
```

**Blockchain eliminates the need for a
trusted central intermediary** by replacing
institutional trust with **mathematical trust
through cryptography and consensus**.

---

### 3.3 Blockchain Core Concepts

| Concept | Description |
|---------|-------------|
| **Block** | A data structure containing a set of transactions + metadata |
| **Chain** | Each block contains the hash of the previous block — linking them |
| **Node** | A computer participating in the blockchain network |
| **P2P Network** | All nodes communicate directly — no central server |
| **Transaction** | A record of an event (payment, contract execution, data entry) |
| **Ledger** | The complete record of all transactions across all blocks |
| **Distributed** | Identical copies of the ledger exist on all participating nodes |
| **Immutability** | Once a block is added, altering it requires altering all subsequent blocks |
| **Append-only** | New blocks can only be added — never deleted or modified |
| **Consensus** | Mechanism by which all nodes agree on the valid state of the blockchain |
| **Mining** | Process of creating new blocks (in Proof-of-Work systems) |
| **Miner** | Node that creates new blocks by solving cryptographic puzzles |

---

### 3.4 How a Block is Structured

```
┌─────────────────────────────────────────┐
│               BLOCK HEADER              │
│  ┌──────────────────────────────────┐   │
│  │ Version          (block version) │   │
│  │ Previous Hash    (hash of block N-1) │
│  │ Merkle Root      (root hash of all   │
│  │                   transactions)      │
│  │ Timestamp        (Unix time)         │
│  │ Difficulty       (PoW target)        │
│  │ Nonce            (PoW solution)      │
│  └──────────────────────────────────┘   │
│                                         │
│              BLOCK BODY                 │
│  ┌──────────────────────────────────┐   │
│  │ Transaction 1                    │   │
│  │ Transaction 2                    │   │
│  │ Transaction 3                    │   │
│  │ ...                              │   │
│  │ Transaction N                    │   │
│  └──────────────────────────────────┘   │
└─────────────────────────────────────────┘
```

**Block header fields — explained:**

| Field | Purpose |
|-------|---------|
| **Version** | Block format version |
| **Previous Block Hash** | SHA-256 hash of the previous block's header — creates the chain |
| **Merkle Root** | Hash of all transactions in this block via Merkle tree |
| **Timestamp** | Time block was created |
| **Difficulty (Bits)** | Current PoW difficulty target |
| **Nonce** | Variable value miners change to find a valid hash |

**The Genesis Block:**
Block 0 — the very first block in a blockchain.
It has no "previous block hash" (set to zeros).
Bitcoin's Genesis Block was mined on
**January 3, 2009** by Satoshi Nakamoto.

---

### 3.5 How Blockchain Achieves Tamper-Resistance

**Cryptographic chaining:**
```
Block 1:
  Previous Hash: 0000...0000 (genesis)
  Current Hash:  SHA256(Block1_header) = A7F3...

Block 2:
  Previous Hash: A7F3...  ← Hash of Block 1
  Current Hash:  SHA256(Block2_header) = B9C2...

Block 3:
  Previous Hash: B9C2...  ← Hash of Block 2
  Current Hash:  SHA256(Block3_header) = D4E1...
```

**What happens if someone alters Block 1?**
```
Attacker modifies Block 1 transaction data
  ↓
Block 1's hash changes → now X1Y2... (not A7F3...)
  ↓
Block 2's "Previous Hash" no longer matches
  ↓
Block 2 is now INVALID
  ↓
Block 3 is INVALID (because Block 2 is)
  ↓
ALL subsequent blocks are INVALID
  ↓
Attacker must recalculate ALL blocks from
Block 1 onwards — while competing against
the rest of the network computing new blocks
  ↓
In a large network: computationally infeasible
→ Blockchain is tamper-evident and tamper-resistant
```

> [!IMPORTANT]
> Blockchain tamper-resistance relies on:
> 1. **Cryptographic hashing** — changing one
>    byte changes the entire hash (Avalanche Effect)
> 2. **Chain linking** — altering one block
>    invalidates ALL subsequent blocks
> 3. **Consensus + computation** — to alter
>    history, an attacker must redo more work
>    than all honest nodes — infeasible in large
>    networks (Proof-of-Work)

---

### 3.6 Consensus Mechanisms

**Consensus mechanisms** are how all nodes in
the distributed network agree on which blocks
are valid and get added to the chain.

#### Proof of Work (PoW)

| Property | Detail |
|----------|--------|
| **Used by** | Bitcoin, Litecoin |
| **Mechanism** | Miners compete to solve a cryptographic puzzle (find a nonce such that SHA256(block_header) < target value) |
| **Incentive** | Winning miner gets block reward (newly minted coins) + transaction fees |
| **Security** | 51% attack requires >50% of total network hash power |
| **Disadvantage** | Extremely energy-intensive |

**PoW puzzle:**
```
Find a nonce N such that:
SHA256(SHA256(block_header with nonce N)) < difficulty_target

The target hash starts with a certain number of zeros.
Average attempts: 2^difficulty (quadrillions for Bitcoin)
Only way: brute force — try trillions of nonces
```

#### Proof of Stake (PoS)

| Property | Detail |
|----------|--------|
| **Used by** | Ethereum (post-merge 2022), Cardano, Solana |
| **Mechanism** | Validators are chosen to create blocks based on the amount of cryptocurrency they "stake" (lock up) as collateral |
| **Incentive** | Validators earn transaction fees |
| **Security** | Attacker must own >33% (or >50%) of staked coins |
| **Advantage** | Energy efficient vs PoW |

#### Other Consensus Mechanisms

| Mechanism | Full Name | Used By |
|-----------|-----------|---------|
| **DPoS** | Delegated Proof of Stake | EOS, Tron |
| **PBFT** | Practical Byzantine Fault Tolerance | Hyperledger Fabric |
| **PoA** | Proof of Authority | Private/consortium chains |
| **PoH** | Proof of History | Solana |

---

### 3.7 Types of Blockchain

| Type | Description | Access | Examples |
|------|-------------|--------|---------|
| **Public** | Open to anyone — fully decentralized | Anyone can read/write/validate | Bitcoin, Ethereum |
| **Private** | One organization controls — permissioned | Only invited participants | Hyperledger Fabric |
| **Consortium** | Group of organizations control — semi-decentralized | Vetted participants | R3 Corda, Quorum |
| **Hybrid** | Mix of public and private | Configurable | Dragonchain |

**Public vs Private comparison:**

| Property | Public | Private |
|----------|--------|---------|
| **Access** | Open — anonymous | Permissioned |
| **Decentralization** | Full | Limited |
| **Transparency** | Full | Configurable |
| **Speed** | Slower (global consensus) | Faster (fewer nodes) |
| **Energy** | High (PoW) | Low (PoA/PBFT) |
| **Use case** | Cryptocurrency, public trust | Enterprise workflows |

---

### 3.8 Blockchain and Cryptography

Blockchain relies on several cryptographic
primitives covered in earlier sessions:

| Cryptographic Primitive | Blockchain Use |
|------------------------|---------------|
| **SHA-256 (hashing)** | Block hash, transaction hash, Merkle tree nodes |
| **ECDSA (digital signatures)** | Signing transactions — prove ownership without revealing private key |
| **Merkle trees** | Efficient transaction verification — Merkle proof |
| **Public/private key pairs** | Wallet addresses derived from public keys |
| **Hash pointers** | Each block contains hash of previous block — creates chain |
| **Zero-knowledge proofs** | Privacy-preserving transactions (Zcash, zk-SNARKs) |

**Bitcoin address generation:**
```
Private Key (256-bit random)
       ↓
ECDSA secp256k1 scalar multiplication
       ↓
Public Key (33 bytes compressed)
       ↓
SHA-256(Public Key)
       ↓
RIPEMD-160(SHA-256 result)
       ↓
Add version byte + Base58Check encoding
       ↓
Bitcoin Address (e.g., 1BvBMSEYstWetqTFn5Au4m4GFg7xJaNVN2)
```

> [!NOTE]
> Bitcoin uses **secp256k1** elliptic curve —
> a SECG curve different from NIST curves.
> Bitcoin addresses are derived from public keys —
> the private key never appears in any transaction.
> Transactions are signed with ECDSA using the
> private key — the signature proves ownership
> without revealing the private key.

---

### 3.9 Blockchain Use Cases

| Industry | Use Case |
|----------|---------|
| **Finance** | Cryptocurrency, cross-border payments (Ripple/XRP), trade finance |
| **Supply chain** | Track product origin, authenticity, provenance (IBM Food Trust, Maersk TradeLens) |
| **Healthcare** | Patient record sharing, drug supply chain integrity |
| **Government** | Land registry, voting systems, digital identity |
| **Legal** | Smart contracts (self-executing agreements), document notarization |
| **Insurance** | Automated claims processing via smart contracts |
| **Energy** | Peer-to-peer energy trading |
| **Media** | NFTs (Non-Fungible Tokens), digital rights management |
| **Education** | Academic credential verification (MIT digital diplomas) |

---

## 4. 📌 Extra Notes

> [!NOTE]
> Everything in this section goes beyond the
> core syllabus but is directly MCQ-relevant.

---

### 4.1 IT Act 2000 vs IT (Amendment) Act 2008

> [!NOTE]

| Aspect | IT Act 2000 | IT (Amendment) Act 2008 |
|--------|------------|------------------------|
| **Focus** | E-commerce, digital signatures, basic cybercrime | Extended cybercrime provisions, data protection |
| **Electronic signature** | Only "digital signature" recognized | Added broader "electronic signature" category |
| **Data protection** | Minimal — Section 43 only | Added Section 43A — body corporate liability |
| **Section 66A** | Not present | Added (later struck down by SC 2015) |
| **Cyber terrorism** | Not present | Added Section 66F |
| **Identity theft** | Not present | Added Section 66C |
| **Intermediaries** | Not addressed | Added Section 79 — safe harbour |
| **Child pornography** | Not present | Added Section 67B |

---

### 4.2 Sections 43, 65, 66 — Cybercrime Provisions

> [!NOTE]

**Section 43 (Civil) — Unauthorized computer access:**
```
Any person who without permission:
  → Accesses a computer / computer network
  → Downloads, copies, or extracts data
  → Introduces computer viruses / malware
  → Damages or disrupts computer systems
  → Denies access to authorized users (DoS)

Penalty: Compensation to affected person
         up to ₹1 crore
```

**Section 65 (Criminal) — Tampering with source code:**
```
Knowingly or intentionally concealing,
destroying, altering computer source code
(that is required to be kept/maintained by law)

Punishment: Up to 3 years imprisonment
            OR fine up to ₹2 lakh OR both
```

**Section 66 (Criminal) — Hacking:**
```
Whoever with the intent to cause or knowing
that he is likely to cause wrongful loss or
damage to the public or any person, destroys
or deletes or alters any information residing
in a computer resource or diminishes its value
or utility or affects it injuriously by any means

Punishment: Up to 3 years imprisonment
            OR fine up to ₹5 lakh OR both
```

---

### 4.3 IT Act and Intermediary Liability

> [!NOTE]
> **Section 79 — Safe Harbour for Intermediaries:**

An **intermediary** (ISP, social media, email
provider, cloud service) is NOT liable for
third-party content IF:
1. Its function is limited to providing access
2. It does not initiate the transmission
3. It does not select the recipient
4. It does not select or modify the information
5. It observes **due diligence** guidelines
   notified by the Government

**When safe harbour is lost:**
- If the intermediary has actual knowledge of
  illegal content and does not remove it within
  specified time after being notified
- If the intermediary conspires in the illegal act

> [!NOTE]
> **IT (Intermediary Guidelines and Digital Media
> Ethics Code) Rules, 2021** — also called
> IT Rules 2021 — significantly expanded
> intermediary obligations:
> - Significant Social Media Intermediaries (5M+
>   users) must appoint compliance officers
> - Must trace originator of messages (WhatsApp)
> - Must publish grievance reports monthly

---

### 4.4 LDAP Schema and Object Classes

> [!NOTE]

**LDAP Schema** defines what attributes are
valid for each type of object (entry).

**Object Classes:**
Every LDAP entry must have one or more
objectClass attributes defining its type.

| Object Class | Type | Common Attributes |
|-------------|------|------------------|
| `person` | Structural | cn, sn, telephoneNumber |
| `organizationalPerson` | Structural | title, ou, postalAddress |
| `inetOrgPerson` | Structural | uid, mail, jpegPhoto |
| `posixAccount` | Auxiliary | uidNumber, gidNumber, homeDirectory |
| `shadowAccount` | Auxiliary | shadowLastChange, shadowExpire |
| `groupOfNames` | Structural | member |
| `organizationalUnit` | Structural | ou, description |

**Example LDAP entry (LDIF format):**
```
dn: cn=Alice Smith,ou=Users,dc=example,dc=com
objectClass: top
objectClass: person
objectClass: organizationalPerson
objectClass: inetOrgPerson
cn: Alice Smith
sn: Smith
givenName: Alice
uid: asmith
mail: alice@example.com
userPassword: {SHA}W6ph5Mm5Pz8GgiULbPgzG37mj9g=
telephoneNumber: +91 20 12345678
```

---

### 4.5 Active Directory Certificate Services (ADCS)

> [!NOTE]

**ADCS** is the Windows Server role for running
an enterprise PKI integrated with Active Directory.

**ADCS components:**

| Component | Description |
|-----------|-------------|
| **Certification Authority (CA)** | Core service — issues certificates |
| **Certificate Enrollment Policy Web Service** | Web-based enrollment for non-domain devices |
| **Online Responder (OCSP)** | Real-time certificate revocation checking |
| **Network Device Enrollment Service (NDES)** | Issues certs to network devices (SCEP protocol) |
| **Web Enrollment** | Browser-based certificate requests |
| **Certificate Enrollment Web Service** | Allows enrollment across forests/firewalls |

**Auto-enrollment via Group Policy:**
```
ADCS Certificate Template:
  → Defined for Computer, User, or Service
  → Specifies algorithm, key size, validity, EKU
  → Assigned permissions in AD

Group Policy Object (GPO):
  → Computer Configuration → Windows Settings →
    Security Settings → Public Key Policies →
    Certificate Services Client — Auto-Enrollment

Result:
  → When computer starts or user logs in:
  → Certificate is automatically requested
    and installed → zero user interaction ✅
```

---

### 4.6 Group Policy Objects (GPO) and Security

> [!NOTE]
> **GPO (Group Policy Objects)** are a core
> Windows Server/Active Directory feature for
> centralized security configuration management.

**What GPOs can enforce:**

| Category | Examples |
|----------|---------|
| **Password policy** | Minimum length, complexity, expiry |
| **Account lockout** | Lock after N failed attempts |
| **Kerberos policy** | Ticket lifetime, clock skew |
| **Audit policy** | Log logon events, object access |
| **Software deployment** | Install applications automatically |
| **Certificate policy** | Auto-enrollment, trust anchors |
| **BitLocker** | Enable full disk encryption |
| **Windows Firewall** | Centrally managed firewall rules |
| **Script execution** | Run logon/logoff scripts |

**GPO link hierarchy:**
```
Applied in order (last applied wins):
  Local Computer Policy
       ↓
  Site-linked GPO
       ↓
  Domain-linked GPO
       ↓
  OU-linked GPO (most specific — wins)
```

---

### 4.7 Bitcoin and Blockchain

> [!NOTE]

| Property | Bitcoin |
|----------|---------|
| **Created by** | Satoshi Nakamoto |
| **Whitepaper** | October 31, 2008 |
| **Genesis block** | January 3, 2009 |
| **Consensus** | Proof of Work (SHA-256) |
| **Block time** | ~10 minutes |
| **Block size** | 1MB (legacy) / 4MB SegWit |
| **Total supply** | 21 million BTC (hard cap) |
| **Hash function** | SHA-256 (double) |
| **Digital signature** | ECDSA with secp256k1 |
| **Block reward** | Halves every 210,000 blocks (Halving) |
| **Current reward** | 3.125 BTC (post-April 2024 halving) |

**Bitcoin halving:**
Every ~4 years, the block reward is cut in half:
```
2009:  50 BTC per block
2012:  25 BTC per block
2016:  12.5 BTC per block
2020:  6.25 BTC per block
2024:  3.125 BTC per block
```

---

### 4.8 Ethereum and Smart Contracts

> [!NOTE]

| Property | Ethereum |
|----------|---------|
| **Created by** | Vitalik Buterin |
| **Launched** | July 30, 2015 |
| **Consensus** | Proof of Stake (since "The Merge" — September 2022) |
| **Block time** | ~12 seconds |
| **Currency** | Ether (ETH) |
| **Hash function** | Keccak-256 (SHA-3 variant) |
| **Digital signature** | ECDSA with secp256k1 |
| **Smart contracts** | Turing-complete programs on blockchain |

**Smart Contracts:**
```
A smart contract is a self-executing program
stored on the blockchain whose terms are
written in code:

Example: "If Alice pays 1 ETH to this contract
         by date X, release title to property Y
         to Alice's address"

Properties:
  → Immutable once deployed — cannot be changed
  → Transparent — code visible on blockchain
  → Self-executing — no human intervention
  → Trustless — no intermediary needed
```

**Gas:**
Ethereum charges "gas" for every computation —
prevents infinite loops and spam on the network.
Gas fees are paid in ETH.

---

### 4.9 Public vs Private vs Consortium
Blockchain

> [!NOTE]

| Property | Public | Private | Consortium |
|----------|--------|---------|-----------|
| **Access** | Open | Single org controls | Group of orgs |
| **Identity** | Pseudonymous | Known participants | Known participants |
| **Consensus** | PoW / PoS | PoA / PBFT | PBFT / PoA |
| **Decentralization** | Full | None | Partial |
| **Transparency** | Full | Restricted | Restricted |
| **Transaction speed** | Slow | Fast | Fast |
| **Example** | Bitcoin, Ethereum | Hyperledger Fabric | R3 Corda, Quorum |
| **Use case** | Cryptocurrency, DeFi | Supply chain, enterprise | Financial consortia |

---

### 4.10 Blockchain Attacks and Vulnerabilities

> [!NOTE]

| Attack | Description | Target |
|--------|-------------|--------|
| **51% Attack** | Attacker controls >50% hash power → can double-spend, rewrite recent history | Public PoW chains |
| **Sybil Attack** | Attacker creates many fake nodes to control consensus | P2P networks |
| **Eclipse Attack** | Attacker surrounds a node with malicious peers — controls its view of the network | Individual nodes |
| **Smart Contract Exploit** | Bugs in Solidity code — reentrancy, integer overflow | Ethereum contracts |
| **The DAO Hack** | Reentrancy attack on DAO contract — $60M ETH stolen (2016) | Ethereum |
| **Routing Attack** | BGP hijacking to isolate blockchain segments | Mining pools |
| **Selfish Mining** | Miner withholds solved blocks to gain competitive advantage | PoW chains |

> [!NOTE]
> **The DAO Hack (2016)** resulted in Ethereum
> being forked — the community voted to reverse
> the hack by hard-forking. This created:
> - **Ethereum (ETH)** — the forked chain where
>   the hack was reversed
> - **Ethereum Classic (ETC)** — the original
>   chain where the hack stands ("code is law")
>
> This raised fundamental questions about
> immutability vs governance in blockchain.

---

### 4.11 Cryptographic Primitives in Blockchain

> [!NOTE]

| Primitive | How Used in Blockchain |
|-----------|----------------------|
| **SHA-256** | Bitcoin block hashing, transaction IDs, Merkle tree nodes |
| **Keccak-256** | Ethereum addresses, transaction hashing |
| **ECDSA (secp256k1)** | Transaction signing in Bitcoin and Ethereum |
| **Merkle Tree** | Transaction verification — Merkle proof allows verifying 1 transaction without downloading all |
| **Hash pointers** | Block chaining — each block stores previous block's hash |
| **Diffie-Hellman** | Some private blockchains use DH for secure communication between nodes |
| **Zero-Knowledge Proofs** | Privacy coins (Zcash) — prove transaction validity without revealing details |

---

### 4.12 PKI and Blockchain — Comparison

> [!NOTE]

| Property | PKI | Blockchain |
|----------|-----|-----------|
| **Trust model** | Hierarchical — trusted CA at top | Distributed — majority consensus |
| **Central authority** | CA (Certificate Authority) | None — decentralized |
| **Identity binding** | CA verifies identity → issues cert | Key pair = identity — no CA |
| **Revocation** | CRL, OCSP | Transactions cannot be deleted |
| **Immutability** | Certificates can be revoked | Once confirmed, blocks cannot be altered |
| **Scalability** | High | Varies — public chains can be slow |
| **Privacy** | CA knows all certificates issued | Public chains are pseudonymous |
| **Legal recognition** | India IT Act recognizes CA certs | Not yet formally recognized in most jurisdictions |

**Where PKI and Blockchain complement each other:**
- **Blockchain PKI** — Using blockchain as a
  distributed certificate store — eliminates
  single-point-of-failure CA
- **Decentralized Identity (DID)** — W3C standard
  for blockchain-based self-sovereign identity
- **Certificate Transparency** uses a Merkle
  tree (blockchain-like append-only log) for
  public audit of CA-issued certificates

---

### 4.13 Digital Signatures in Legal Disputes —
India

> [!NOTE]
> Section 85B of the IT Act addresses the
> presumption about electronic records:

**Section 85B — Presumption as to electronic records:**
If a secure electronic record is produced as
evidence, the court shall presume:
- The electronic record has not been altered
  since the specific point in time
- The digital signature was created by the
  subscriber

**How digital signatures are used in court:**
```
Document A is signed with DSC by Alice.

In court:
  → Alice claims she never signed document A
  → Plaintiff presents the document + digital signature
  → Court can verify:
    (1) Signature was created with Alice's private key
    (2) Document has not been altered since signing
    (3) Alice's private key cert was valid at signing time
    (4) If trusted timestamp exists: signing time proven

Counterclaim:
  → Alice must prove:
    (a) Her private key was compromised before signing
    (b) The DSC was misused
    → Burden of proof shifts to Alice
```

**Why timestamping is critical for legal validity:**
- A DSC expires after 1-3 years
- If a dispute arises 5 years later:
  - Without timestamp: impossible to prove
    the signature was valid at time of signing
  - With RFC 3161 timestamp: provably valid
    at the specific moment it was signed

---

## 5. Abbreviations Table

| Abbreviation | Full Form | One-Line Technical Meaning |
|---|---|---|
| IT Act | Information Technology Act 2000 | India's primary law for e-commerce, digital signatures, and cybercrime |
| CCA | Controller of Certifying Authorities | India's apex PKI regulatory body under IT Act — licenses CAs |
| RCAI | Root Certifying Authority of India | India's national Root CA — operated by CCA |
| DSC | Digital Signature Certificate | Asymmetric key certificate issued by CCA-licensed CA — IT Act Digital Signature |
| MeitY | Ministry of Electronics and Information Technology | Indian government ministry overseeing IT policy and CCA |
| LDAP | Lightweight Directory Access Protocol | RFC 4511 protocol for directory access — port 389/636 |
| LDAPS | LDAP over SSL/TLS | Encrypted LDAP — port 636 |
| DN | Distinguished Name | Full unique path to an LDAP entry |
| RDN | Relative Distinguished Name | Entry identifier within its parent container |
| DIT | Directory Information Tree | Hierarchical structure of LDAP entries |
| LDIF | LDAP Data Interchange Format | Text format for exporting/importing LDAP data |
| AD | Active Directory | Microsoft's enterprise directory service — LDAP + Kerberos + DNS |
| ADCS | Active Directory Certificate Services | Microsoft's enterprise PKI solution integrated with AD |
| AD DS | Active Directory Domain Services | Core AD directory service role |
| DC | Domain Controller | Windows Server running AD DS — stores NTDS.dit |
| NTDS.dit | NT Directory Services | Active Directory database file |
| GPO | Group Policy Object | AD configuration applied to users/computers centrally |
| GC | Global Catalog | AD partial replica of all forest objects |
| PoW | Proof of Work | Blockchain consensus — miners solve SHA-256 puzzle |
| PoS | Proof of Stake | Blockchain consensus — validators stake cryptocurrency |
| PoA | Proof of Authority | Blockchain consensus — vetted validators sign blocks |
| PBFT | Practical Byzantine Fault Tolerance | Distributed consensus for permissioned blockchains |
| DLT | Distributed Ledger Technology | Broader category — blockchain is one type |
| DID | Decentralized Identifier | W3C standard for blockchain-based self-sovereign identity |
| NFT | Non-Fungible Token | Unique blockchain-based digital asset |
| DeFi | Decentralized Finance | Financial services on public blockchain without intermediaries |
| UNCITRAL | United Nations Commission on International Trade Law | UN body — IT Act based on UNCITRAL Model Law |

---

## 6. Keywords + Concept Map

| Term | Definition | Connections | Use Cases |
|------|-----------|-------------|-----------|
| **IT Act 2000** | India's primary digital law | CCA, DSC, e-Sign, cybercrime sections | All digital signature + cybercrime context |
| **CCA** | India's PKI apex regulator | Section 17, RCAI, licensed CAs | PKI governance in India |
| **DSC** | CA-issued asymmetric key certificate | IT Act Section 3, eMudhra, Class 3 | Tax, MCA, e-tendering |
| **Section 66F** | Cyber terrorism — up to life imprisonment | Most severe IT Act offence | Attacks on critical infrastructure |
| **Section 43A** | Data protection liability for body corporates | GDPR equivalent in India | Data breach penalties |
| **LDAP** | Directory access protocol — RFC 4511 | Port 389/636, DN, DIT, BIND, Active Directory | Enterprise authentication |
| **Active Directory** | Microsoft directory + Kerberos + DNS + GPO | ADCS, auto-enrollment, domain trust | Windows enterprise |
| **ADCS** | Windows enterprise PKI | Auto-enrollment, templates, OCSP | Internal certificate issuance |
| **Blockchain** | Distributed append-only cryptographic ledger | SHA-256, ECDSA, Merkle tree, consensus | Bitcoin, Ethereum, supply chain |
| **Proof of Work** | PoW consensus — SHA-256 mining | Bitcoin, energy-intensive | Cryptocurrency mining |
| **Proof of Stake** | PoS consensus — stake as collateral | Ethereum post-2022 | Energy-efficient consensus |
| **Smart Contract** | Self-executing code on blockchain | Ethereum, Solidity, gas | DeFi, legal automation |
| **51% attack** | Control majority hash power to double-spend | PoW vulnerability | Blockchain security |
| **Genesis block** | Block 0 — first block in chain | Satoshi Nakamoto, January 3, 2009 | Blockchain history |
| **Merkle tree** | Binary hash tree of transactions | SHA-256, Merkle proof, Bitcoin | Efficient transaction verification |

---

## 7. Quick Reference Cheatsheet

### 🔸 IT Act Key Facts

| Property | Value |
|----------|-------|
| Enacted | June 9, 2000 |
| In force | October 17, 2000 |
| Amended | IT (Amendment) Act 2008 |
| Based on | UNCITRAL Model Law 1996 |
| Nodal ministry | MeitY |
| Apex PKI body | CCA (Section 17) |
| India Root CA | RCAI — operated by CCA |
| Cyber terrorism | Section 66F — up to life |
| Hacking | Section 66 — up to 3 years / ₹5 lakh |
| Identity theft | Section 66C — up to 3 years AND ₹1 lakh |
| Data protection | Section 43A — corporate liability |

---

### 🔸 IT Act Sections Quick Reference

| Section | Subject |
|---------|---------|
| 3 | Digital signature authentication |
| 5 | Legal recognition of digital signatures |
| 17 | CCA establishment |
| 43 | Unauthorized access (civil) |
| 43A | Data protection corporate liability |
| 65 | Source code tampering |
| 66 | Hacking |
| 66C | Identity theft |
| 66F | Cyber terrorism — life imprisonment |
| 79 | Intermediary safe harbour |

---

### 🔸 LDAP Quick Reference

| Property | Value |
|----------|-------|
| Standard | LDAPv3 — RFC 4511 |
| Port (plain) | 389 |
| Port (TLS) | 636 (LDAPS) |
| DN example | cn=Alice,ou=Users,dc=example,dc=com |
| Authenticate via | BIND operation |
| Search scope | Base / One Level / Subtree |
| Encrypted via | LDAPS (636) or STARTTLS (389) |

---

### 🔸 Active Directory Components

| Component | Role |
|-----------|------|
| Domain Controller (DC) | Runs AD DS, stores NTDS.dit |
| Global Catalog (GC) | Cross-domain object lookup |
| NTDS.dit | AD database file |
| SYSVOL | GPO files and scripts |
| ADCS | Enterprise PKI for internal certs |
| GPO | Centralized security configuration |

---

### 🔸 Blockchain Block Structure

```
Previous Hash → Block Header → Nonce
                   │
                   └── Merkle Root
                              │
                   Transaction 1 + Transaction 2...
```

---

### 🔸 Blockchain Consensus Comparison

| Mechanism | Energy | Speed | Used By |
|-----------|--------|-------|---------|
| PoW | High | Slow | Bitcoin |
| PoS | Low | Fast | Ethereum (post-2022) |
| PoA | Very Low | Fast | Private chains |
| PBFT | Low | Fast | Hyperledger |

---

### 🔸 PKI vs Blockchain Trust

| | PKI | Blockchain |
|---|-----|-----------|
| Trust model | Hierarchical CA | Distributed consensus |
| Identity | CA-issued cert | Key pair |
| Revocation | CRL/OCSP | Not possible (immutable) |
| Legal recognition | IT Act (India) | Limited |

---

## 8. Session Revision Snapshot

### ⚡ TL;DR — 5 Bullets

- ✅ IT Act 2000 (in force Oct 17, 2000, based on
  UNCITRAL 1996) — CCA (Section 17) is India's
  apex PKI regulator operating RCAI — Section 3
  defines digital signatures using asymmetric
  crypto from licensed CAs — Section 5 gives
  legal equivalence to handwritten signatures —
  Section 66F (cyber terrorism) = life imprisonment
- ✅ LDAP (RFC 4511, LDAPv3) = directory access
  protocol — port 389 (plain), 636 (LDAPS) —
  hierarchical DIT with DN (cn=Alice,ou=Users,
  dc=example,dc=com) — BIND operation authenticates
  — MUST use LDAPS/STARTTLS or credentials are
  cleartext
- ✅ Active Directory = Microsoft's enterprise
  directory service implementing LDAP + Kerberos
  + DNS + GPO + ADCS — Domain Controllers store
  NTDS.dit — ADCS enables PKI auto-enrollment
  via Group Policy — GPOs enforce security
  settings centrally
- ✅ Blockchain (Satoshi Nakamoto, 2008/2009) =
  distributed append-only ledger — each block
  contains Previous Block Hash + Merkle Root +
  Nonce — SHA-256 linking makes tampering require
  recomputing ALL subsequent blocks — consensus
  (PoW for Bitcoin, PoS for Ethereum) prevents
  malicious alterations
- ✅ Blockchain cryptography: SHA-256 for block
  hashing, ECDSA secp256k1 for transaction
  signing, Merkle trees for transaction
  verification — 51% attack = control >50% hash
  power — smart contracts (Ethereum, Solidity)
  are self-executing code — Genesis block =
  January 3, 2009

---

### 🎯 MCQ-Likely Concepts — Everything Examiners Love

| Concept | Why It's Tricky |
|---------|----------------|
| IT Act enacted June 9, 2000 — in force Oct 17, 2000 | Two different dates |
| IT Act based on UNCITRAL Model Law 1996 | International basis |
| CCA established by Section 17 | Specific section tested |
| RCAI operated by CCA | India's Root CA identity |
| Section 66F = cyber terrorism = life imprisonment | Most severe — specific |
| Section 66C = identity theft = 3 yrs + ₹1 lakh | Fine is AND (both) not OR |
| Section 66 = hacking = 3 yrs OR ₹5 lakh fine | Fine is OR (either) |
| Section 43A = corporate data protection liability | No fixed penalty ceiling |
| IT Act First Schedule = excluded documents | Property, wills, PoA cannot use e-sign |
| LDAP port 389 (plain) vs 636 (LDAPS) | Port numbers tested |
| LDAP BIND = authentication operation | Operation name specific |
| DN reads left (specific) to right (general) | Reading direction |
| AD uses Kerberos (primary) + NTLM (fallback) | Two auth protocols |
| ADCS = AD-integrated PKI with auto-enrollment | Microsoft PKI component |
| GPO = centralized security config in AD | What GPO does |
| Blockchain — Satoshi Nakamoto — whitepaper Oct 2008 | Creator and year |
| Genesis block = January 3, 2009 | Specific date |
| Bitcoin uses SHA-256 (double) for PoW | Hash function specific |
| Bitcoin uses ECDSA secp256k1 (not NIST P-256) | Curve distinction |
| Ethereum uses Keccak-256 (SHA-3 variant) | Not SHA-256 like Bitcoin |
| Ethereum switched from PoW to PoS in September 2022 | "The Merge" year |
| 51% attack requires >50% hash power | Specific threshold |
| PoW = energy intensive (Bitcoin); PoS = efficient (Ethereum) | Energy comparison |
| Smart contracts = self-executing — Ethereum, Solidity | Language and platform |
| Blockchain is append-only — cannot delete blocks | Immutability property |
| Merkle Root = hash of all transactions in a block | What's in block header |

---

<details>
<summary>🔬 Lab — Session 14 (Email Encryption)</summary>

**Lab file:** `3-Labs/lab-session-14-email-encryption.md`

**Tool:** Thunderbird (or Windows Mail / Outlook)
with S/MIME certificate

**Lab Tasks:**
1. Import a digital certificate into Thunderbird
   (using the certificate created in Session 09/10
   lab with XCA)
2. Configure Thunderbird to use the certificate
   for S/MIME email signing
3. Send a digitally signed email
4. Send an encrypted email to a recipient whose
   certificate is available
5. Verify received signed email
6. Decrypt a received encrypted email

**Theory ↔ Lab Connection:**

| Session 14 Theory | Lab Demonstration |
|------------------|------------------|
| S/MIME emailProtection EKU | Certificate must have this EKU for Thunderbird to use it |
| Sign-then-encrypt convention | Thunderbird performs in correct order |
| PKCS#7/CMS message format | Signed email generates .p7s attachment |
| X.509 certificate for email | Import cert from Session 09/10 XCA lab |
| CA trust for S/MIME | Importing Root CA makes recipient trust signed email |
| Digital signature non-repudiation | Signed email shows sender identity + signature valid icon |
| IT Act — electronic records | Signed email is a legally valid electronic record under IT Act |

**Active Directory context (if lab environment has AD):**
- ADCS auto-enrollment would eliminate manual
  certificate import step
- GPO could enforce S/MIME signing for all users
- LDAP/AD provides the directory of user certificates
  for email encryption (Global Address List)

**Full step-by-step lab guide:**
`3-Labs/lab-session-14-email-encryption.md`

</details>

---