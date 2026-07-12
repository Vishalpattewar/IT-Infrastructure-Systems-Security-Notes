# Session 13 — Securing Websites and Emails:
SSL, TLS, PGP & S/MIME

## 📑 Table of Contents

- [1. SSL — Secure Sockets Layer](#1-ssl--secure-sockets-layer)
  - [1.1 What is SSL?](#11-what-is-ssl)
  - [1.2 SSL History and
    Versions](#12-ssl-history-and-versions)
  - [1.3 Why SSL is Deprecated](#13-why-ssl-is-deprecated)
- [2. TLS — Transport Layer Security](#2-tls--transport-layer-security)
  - [2.1 What is TLS?](#21-what-is-tls)
  - [2.2 TLS Version History](#22-tls-version-history)
  - [2.3 TLS Protocol
    Architecture](#23-tls-protocol-architecture)
  - [2.4 TLS 1.2 Handshake — Step by
    Step](#24-tls-12-handshake--step-by-step)
  - [2.5 TLS 1.3 Handshake — Step by
    Step](#25-tls-13-handshake--step-by-step)
  - [2.6 TLS 1.2 vs TLS 1.3 —
    Comparison](#26-tls-12-vs-tls-13--comparison)
  - [2.7 TLS Cipher Suites](#27-tls-cipher-suites)
  - [2.8 TLS Record Protocol](#28-tls-record-protocol)
  - [2.9 HTTPS — HTTP over TLS](#29-https--http-over-tls)
  - [2.10 TLS Certificate
    Validation](#210-tls-certificate-validation)
- [3. PGP — Pretty Good Privacy](#3-pgp--pretty-good-privacy)
  - [3.1 What is PGP?](#31-what-is-pgp)
  - [3.2 PGP Key Concepts](#32-pgp-key-concepts)
  - [3.3 PGP Encryption —
    How It Works](#33-pgp-encryption--how-it-works)
  - [3.4 PGP Digital Signature](#34-pgp-digital-signature)
  - [3.5 PGP Web of Trust](#35-pgp-web-of-trust)
  - [3.6 OpenPGP and GPG](#36-openpgp-and-gpg)
  - [3.7 PGP Key Servers](#37-pgp-key-servers)
- [4. S/MIME — Secure/Multipurpose Internet
  Mail Extensions](#4-smime--securemultipurpose-internet-mail-extensions)
  - [4.1 What is S/MIME?](#41-what-is-smime)
  - [4.2 S/MIME vs PGP](#42-smime-vs-pgp)
  - [4.3 S/MIME Operations](#43-smime-operations)
  - [4.4 S/MIME Certificate
    Requirements](#44-smime-certificate-requirements)
  - [4.5 S/MIME in Email Clients](#45-smime-in-email-clients)
- [5. 📌 Extra Notes](#5--extra-notes)
  - [5.1 SSL/TLS Attack
    History](#51-ssltls-attack-history)
  - [5.2 TLS Certificate
    Pinning](#52-tls-certificate-pinning)
  - [5.3 HSTS — HTTP Strict Transport
    Security](#53-hsts--http-strict-transport-security)
  - [5.4 SNI — Server Name
    Indication](#54-sni--server-name-indication)
  - [5.5 Certificate Transparency
    in TLS](#55-certificate-transparency-in-tls)
  - [5.6 TLS 1.3 — Removed and
    Added Features](#56-tls-13--removed-and-added-features)
  - [5.7 ALPN — Application Layer
    Protocol Negotiation](#57-alpn--application-layer-protocol-negotiation)
  - [5.8 mTLS — Mutual TLS](#58-mtls--mutual-tls)
  - [5.9 PGP Fingerprint and Key
    Verification](#59-pgp-fingerprint-and-key-verification)
  - [5.10 DKIM, SPF, DMARC — Email
    Authentication](#510-dkim-spf-dmarc--email-authentication)
  - [5.11 OpenSSL Commands —
    Reference](#511-openssl-commands--reference)
  - [5.12 TLS in Modern
    Applications](#512-tls-in-modern-applications)
- [6. Abbreviations Table](#6-abbreviations-table)
- [7. Keywords + Concept Map](#7-keywords--concept-map)
- [8. Quick Reference Cheatsheet](#8-quick-reference-cheatsheet)
- [9. Session Revision Snapshot](#9-session-revision-snapshot)

---

## 1. SSL — Secure Sockets Layer

### 1.1 What is SSL?

**SSL (Secure Sockets Layer)** was the original
protocol for encrypting communications between
a web browser and a web server — developed by
**Netscape Communications** in the early 1990s.

SSL introduced the concept of securing HTTP
traffic (creating HTTPS) — binding server
identity (via certificates) to an encrypted
channel.

> [!IMPORTANT]
> **ALL versions of SSL are deprecated and broken.**
> SSL should never be used in any system today.
> The successor — TLS — replaced SSL and is
> the current standard.
>
> However, people often say "SSL certificate"
> colloquially when they mean a TLS certificate.
> The certificate format (X.509) is the same —
> the protocol is TLS.

---

### 1.2 SSL History and Versions

| Version | Year | Status | Notes |
|---------|------|--------|-------|
| **SSL 1.0** | 1994 | Never released | Design flaws found before release |
| **SSL 2.0** | 1995 | ❌ Broken | First public release — had serious vulnerabilities |
| **SSL 3.0** | 1996 | ❌ Broken (POODLE) | Widely deployed — broken by POODLE attack (2014) |

**SSL 2.0 vulnerabilities:**
- Weak MAC construction — MD5 based
- No protection against cipher downgrade
- Same key used for authentication and encryption
- Easily attacked by DROWN attack

**SSL 3.0 vulnerabilities:**
- POODLE attack (2014) — padding oracle on
  CBC mode in SSL 3.0
- RC4 weakness when RC4 used as workaround
- Disabled by all major browsers by 2015

---

### 1.3 Why SSL is Deprecated

| RFC | Action | Year |
|-----|--------|------|
| **RFC 6176** | Prohibits SSL 2.0 in TLS implementations | 2011 |
| **RFC 7568** | Deprecates SSL 3.0 | June 2015 |
| **RFC 8996** | Formally deprecates TLS 1.0 and TLS 1.1 | 2021 |

> [!IMPORTANT]
> All versions of SSL are broken.
> TLS 1.0 and TLS 1.1 are deprecated (RFC 8996).
> **Currently accepted versions: TLS 1.2 and TLS 1.3**
> TLS 1.3 is the recommended standard.

---

## 2. TLS — Transport Layer Security

### 2.1 What is TLS?

**TLS (Transport Layer Security)** is the
cryptographic protocol that provides:
- **Confidentiality** — encrypts data in transit
- **Integrity** — detects data tampering
- **Authentication** — verifies server (and
  optionally client) identity via certificates

TLS is the direct successor to SSL and is used
in virtually every secure internet protocol:
HTTPS, IMAPS, SMTPS, LDAPS, FTPS, VoIP, etc.

| Property | Detail |
|----------|--------|
| **Successor to** | SSL 3.0 |
| **Current standard** | TLS 1.3 (RFC 8446, 2018) |
| **OSI Layer** | Session / Transport Layer boundary |
| **Port (HTTPS)** | 443 |
| **Defined by** | IETF (Internet Engineering Task Force) |

---

### 2.2 TLS Version History

| Version | RFC | Year | Status |
|---------|-----|------|--------|
| **TLS 1.0** | RFC 2246 | 1999 | ❌ Deprecated — RFC 8996 (2021) |
| **TLS 1.1** | RFC 4346 | 2006 | ❌ Deprecated — RFC 8996 (2021) |
| **TLS 1.2** | RFC 5246 | 2008 | ✅ Current — widely deployed |
| **TLS 1.3** | RFC 8446 | 2018 | ✅ Current — recommended |

> [!NOTE]
> **TLS 1.0 relationship to SSL 3.0:**
> TLS 1.0 was essentially SSL 3.1 — so similar
> to SSL 3.0 that it could fall back to SSL 3.0,
> inheriting its vulnerabilities (POODLE TLS
> variant). TLS 1.1 and 1.2 fixed these issues
> progressively.
>
> **Why browsers deprecated TLS 1.0/1.1:**
> BEAST attack (TLS 1.0), POODLE for TLS
> (1.0/1.1), and general weakness of the
> cipher suites supported. From 2020, all
> major browsers require TLS 1.2 minimum.

---

### 2.3 TLS Protocol Architecture

TLS consists of two layers of sub-protocols:

```
TLS Protocol Stack:
┌────────────────────────────────────────────┐
│         TLS Handshake Protocol             │ ← Negotiates params
│         TLS ChangeCipherSpec Protocol      │ ← Signals new keys
│         TLS Alert Protocol                 │ ← Error signaling
│         TLS Application Data Protocol     │ ← Carries app data
├────────────────────────────────────────────┤
│              TLS Record Protocol           │ ← Underlying transport
└────────────────────────────────────────────┘
                     │
              TCP (Port 443 for HTTPS)
```

**TLS Record Protocol** — the foundation:
- Fragments application data into records
- Optionally compresses (disabled in TLS 1.3)
- Applies MAC for integrity
- Encrypts with negotiated cipher

**TLS Handshake Protocol** — session setup:
- Negotiates TLS version
- Negotiates cipher suite
- Authenticates server (and optionally client)
- Establishes session keys

---

### 2.4 TLS 1.2 Handshake — Step by Step

```
CLIENT                              SERVER
  │                                    │
  │── ClientHello ───────────────────→ │
  │   TLS version, random,             │
  │   supported cipher suites,         │
  │   extensions (SNI, ALPN etc.)      │
  │                                    │
  │ ←── ServerHello ─────────────────  │
  │     TLS version, random,           │
  │     selected cipher suite,         │
  │     session ID                     │
  │                                    │
  │ ←── Certificate ─────────────────  │
  │     Server's X.509 certificate(s)  │
  │                                    │
  │ ←── ServerKeyExchange ───────────  │
  │     DH/ECDH params (if needed)     │
  │                                    │
  │ ←── ServerHelloDone ─────────────  │
  │                                    │
  │── ClientKeyExchange ─────────────→ │
  │   Pre-master secret (RSA encrypted)│
  │   OR DH public key                 │
  │                                    │
  │── ChangeCipherSpec ──────────────→ │
  │   "I will now use negotiated keys" │
  │                                    │
  │── Finished ──────────────────────→ │
  │   Verify all handshake messages    │
  │                                    │
  │ ←── ChangeCipherSpec ─────────────  │
  │ ←── Finished ────────────────────  │
  │                                    │
  │←──── Application Data (encrypted)──│
  │────── Application Data (encrypted)→│
```

**Key derivation in TLS 1.2:**
```
Pre-Master Secret (from RSA or DH)
         ↓
Master Secret = PRF(PreMasterSecret,
                    "master secret",
                    ClientRandom || ServerRandom)
         ↓
Key Material = PRF(MasterSecret,
                   "key expansion",
                   ServerRandom || ClientRandom)
         ↓
Split into:
  Client write MAC key
  Server write MAC key
  Client write encryption key
  Server write encryption key
  Client write IV
  Server write IV
```

> [!NOTE]
> **The two randoms (ClientRandom + ServerRandom)**
> are critical — they ensure unique session keys
> even if the same certificate and pre-master
> secret were used (which prevents replay attacks
> across sessions).

---

### 2.5 TLS 1.3 Handshake — Step by Step

TLS 1.3 dramatically simplifies the handshake —
reducing latency from 2 round-trips to **1 RTT**
(and 0-RTT for session resumption).

```
CLIENT                              SERVER
  │                                    │
  │── ClientHello ───────────────────→ │
  │   TLS 1.3,                         │
  │   supported cipher suites,         │
  │   key_share (ECDHE public key)     │
  │   psk_key_exchange (if resuming)   │
  │                                    │
  │ ←── ServerHello ─────────────────  │
  │     selected cipher suite,         │
  │     key_share (server ECDHE key)   │
  │                                    │
  │   *** Both sides compute shared    │
  │       secret from ECDHE here ***   │
  │   *** All subsequent messages ***  │
  │   *** encrypted from this point ** │
  │                                    │
  │ ←── EncryptedExtensions ─────────  │
  │ ←── Certificate ─────────────────  │
  │ ←── CertificateVerify ───────────  │
  │     Server proves it owns cert     │
  │ ←── Finished ────────────────────  │
  │                                    │
  │── Finished ──────────────────────→ │
  │                                    │
  │←──── Application Data ───────────→│
  │     (1 RTT total ✅)               │
```

**TLS 1.3 key improvements:**
- **1-RTT handshake** (vs 2-RTT in TLS 1.2)
- **0-RTT session resumption** (with PSK)
- All crypto after ServerHello is **encrypted**
- **ECDHE mandatory** for all key exchanges
- **Perfect Forward Secrecy mandatory**
- Removed legacy and insecure features

---

### 2.6 TLS 1.2 vs TLS 1.3 — Comparison

| Feature | TLS 1.2 | TLS 1.3 |
|---------|---------|---------|
| **RFC** | RFC 5246 (2008) | RFC 8446 (2018) |
| **Handshake RTT** | 2 RTT | 1 RTT |
| **0-RTT** | ❌ No | ✅ Yes (PSK resumption) |
| **Key exchange** | RSA or (EC)DHE | ECDHE only |
| **PFS** | Optional | ✅ Mandatory |
| **Static RSA** | ✅ Allowed | ❌ Removed |
| **Cipher suites** | Many (inc. weak) | 5 secure ones only |
| **Compression** | Optional | ❌ Removed |
| **Renegotiation** | ✅ Allowed | ❌ Removed |
| **RC4** | Technically possible | ❌ Removed |
| **3DES** | Technically possible | ❌ Removed |
| **SHA-1 in PRF** | ✅ Allowed | ❌ Removed |
| **Session IDs** | ✅ Supported | Replaced by PSK |
| **Encrypt-then-MAC** | Optional | Always AEAD |
| **Certificate hiding** | ❌ No (visible) | ✅ Encrypted |

> [!IMPORTANT]
> **TLS 1.3 cipher suites (only 5):**
> 1. TLS_AES_128_GCM_SHA256
> 2. TLS_AES_256_GCM_SHA384
> 3. TLS_CHACHA20_POLY1305_SHA256
> 4. TLS_AES_128_CCM_SHA256
> 5. TLS_AES_128_CCM_8_SHA256
>
> All use AEAD (Authenticated Encryption with
> Associated Data) — providing both
> confidentiality AND integrity simultaneously.
> Key exchange algorithm and certificate type
> are NOT part of the TLS 1.3 cipher suite name
> (unlike TLS 1.2).

---

### 2.7 TLS Cipher Suites

A **cipher suite** is a named combination of
algorithms specifying how TLS will:
1. Exchange keys
2. Authenticate the server
3. Encrypt data
4. Verify integrity

**TLS 1.2 cipher suite naming format:**
```
TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
 │    │     │         │    │      │
 │    │     │         │    │      └── HMAC hash (PRF)
 │    │     │         │    └──── MAC/AEAD mode
 │    │     │         └── Key size
 │    │     └── Authentication algorithm
 │    └── Key exchange algorithm
 └── Protocol
```

**TLS 1.3 cipher suite naming format:**
```
TLS_AES_128_GCM_SHA256
 │    │    │    │    │
 │    │    │    │    └── HKDF hash function
 │    │    │    └── AEAD mode
 │    │    └── Key size
 │    └── Cipher
 └── Protocol
(No key exchange or auth in name — always ECDHE)
```

**Cipher suite strength ranking (TLS 1.2):**

| Cipher Suite | PFS | Strength |
|-------------|-----|---------|
| TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 | ✅ | ✅✅ Best |
| TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 | ✅ | ✅✅ Best |
| TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305 | ✅ | ✅✅ Best |
| TLS_RSA_WITH_AES_256_GCM_SHA384 | ❌ | ⚠️ No PFS |
| TLS_RSA_WITH_AES_128_CBC_SHA | ❌ | ⚠️ Weak |
| TLS_RSA_WITH_3DES_EDE_CBC_SHA | ❌ | ❌ Broken |
| TLS_RSA_WITH_RC4_128_MD5 | ❌ | ❌ Broken |

---

### 2.8 TLS Record Protocol

The **TLS Record Protocol** is the underlying
transport layer of TLS — it takes application
data and processes it:

```
Application Data (plaintext)
        │
        ▼
Fragment into records (≤ 16KB each)
        │
        ▼
Compress (DISABLED in TLS 1.3 — CRIME attack)
        │
        ▼
Apply MAC / AEAD encryption
  TLS 1.2: MAC-then-Encrypt (CBC) or AEAD (GCM)
  TLS 1.3: AEAD only (GCM, ChaCha20-Poly1305)
        │
        ▼
Add TLS Record Header:
  Content Type (1 byte): Handshake/Alert/AppData
  Version (2 bytes): 0x0303 for TLS 1.2/1.3
  Length (2 bytes): record length
        │
        ▼
Send over TCP
```

> [!NOTE]
> In TLS 1.3, the **Content Type** in the
> outer TLS record header is always
> `application_data (23)` — the actual content
> type is encrypted inside the record.
> This hides whether a record contains
> handshake data, alert, or application data —
> reducing information leakage to observers.

---

### 2.9 HTTPS — HTTP over TLS

**HTTPS** is simply HTTP transported over a
TLS connection.

| Property | HTTP | HTTPS |
|----------|------|-------|
| **Port** | 80 | 443 |
| **Transport** | TCP | TCP + TLS |
| **Confidentiality** | ❌ | ✅ |
| **Integrity** | ❌ | ✅ |
| **Server authentication** | ❌ | ✅ |
| **Certificate required** | ❌ | ✅ |

**HTTPS workflow:**
```
1. DNS resolution → IP address for domain
2. TCP 3-way handshake (SYN, SYN-ACK, ACK)
3. TLS handshake (server authentication +
   session key establishment)
4. HTTP request/response over encrypted TLS channel
5. TLS closure (close_notify alert)
6. TCP teardown
```

**Browser padlock indicators:**
- 🔒 Padlock = valid HTTPS (TLS 1.2 or 1.3)
- ⚠️ Warning = expired cert, wrong domain,
  untrusted CA, or TLS 1.0/1.1
- ❌ "Not Secure" = HTTP (no TLS)

---

### 2.10 TLS Certificate Validation

When a browser connects to an HTTPS site, it
performs all certificate validation steps
(covered in Session 07/08) PLUS:

**TLS-specific checks:**

| Check | Description |
|-------|-------------|
| **Protocol version** | Server must use TLS 1.2+ |
| **Cipher suite** | Must not use broken ciphers |
| **Certificate name** | CN or SAN must match the hostname |
| **Certificate validity** | Not expired, not premature |
| **Certificate chain** | Full chain to trusted Root CA |
| **Revocation** | CRL or OCSP check |
| **CT log** | Signed Certificate Timestamp (Chrome requires) |
| **HSTS** | If previously visited, enforce HTTPS |

---

## 3. PGP — Pretty Good Privacy

### 3.1 What is PGP?

**PGP (Pretty Good Privacy)** is a data
encryption and decryption program that provides
cryptographic privacy and authentication for
data communication — primarily used for
email encryption and file encryption.

| Property | Detail |
|----------|--------|
| **Created by** | Phil Zimmermann |
| **Year** | 1991 |
| **Type** | Hybrid encryption (symmetric + asymmetric) |
| **Trust model** | Web of Trust (decentralized) |
| **Open standard** | OpenPGP (RFC 4880) |
| **Free implementation** | GnuPG (GPG) |
| **Primary use** | Email encryption, file encryption, key signing |

**Historical note:**
Phil Zimmermann released PGP for free on the
internet in 1991 — making strong encryption
accessible to the public for the first time.
The US government investigated him for three
years under Arms Export Control Act regulations
(strong crypto was classified as a munition).
The investigation was dropped in 1996.

---

### 3.2 PGP Key Concepts

**PGP key pair:**
- **Public key** — shared openly on key servers
  or via email
- **Private key** — kept secret by the owner
- **Key ID** — short identifier for the key
  (last 8/16/40 hex characters of fingerprint)
- **Fingerprint** — SHA-1 or SHA-256 hash of
  the public key — used for key verification

**PGP uses asymmetric algorithms:**
- **Older PGP:** RSA, DSA/ElGamal
- **Modern PGP (OpenPGP):** RSA, DSA, ECDSA,
  Ed25519, ECDH, Curve25519

**PGP symmetric algorithms (for data):**
- AES-128, AES-192, AES-256 (recommended)
- Legacy: 3DES, CAST5, Blowfish

---

### 3.3 PGP Encryption — How It Works

PGP uses **hybrid encryption** — symmetric key
for data, asymmetric for key protection:

```
ENCRYPTION (Alice sends encrypted message to Bob):

Step 1: Alice generates a random session key
        (symmetric — e.g., AES-256 key)

Step 2: Alice encrypts the message with the
        session key
        Message_enc = AES256_Encrypt(SessionKey, Message)

Step 3: Alice encrypts the session key with
        BOB's PUBLIC KEY
        SessionKey_enc = RSA_Encrypt(Bob_PubKey, SessionKey)

Step 4: Alice sends:
        → Message_enc + SessionKey_enc

─────────────────────────────────────────────

DECRYPTION (Bob decrypts):

Step 5: Bob decrypts the session key with
        his PRIVATE KEY
        SessionKey = RSA_Decrypt(Bob_PrivKey, SessionKey_enc)

Step 6: Bob decrypts the message with
        the recovered session key
        Message = AES256_Decrypt(SessionKey, Message_enc)

Step 7: Bob reads Alice's message ✅
```

**Multi-recipient PGP:**
If Alice sends to multiple recipients, she
encrypts the session key multiple times — once
with each recipient's public key:
```
Message_enc = AES256(SessionKey, Message)  ← one copy
SessionKey_enc_Bob = RSA(Bob_PubKey, SessionKey)
SessionKey_enc_Carol = RSA(Carol_PubKey, SessionKey)
```
Each recipient decrypts with their own private
key to get the session key — then decrypts the
message.

---

### 3.4 PGP Digital Signature

```
SIGNING (Alice signs a message):

Step 1: Alice computes hash of the message
        H = SHA256(Message)

Step 2: Alice signs the hash with her PRIVATE KEY
        Signature = RSA_Sign(Alice_PrivKey, H)

Step 3: Alice sends:
        Message + Signature

─────────────────────────────────────────────

VERIFICATION (Bob verifies):

Step 4: Bob computes hash of received message
        H = SHA256(Message)

Step 5: Bob verifies signature using Alice's
        PUBLIC KEY
        H' = RSA_Verify(Alice_PubKey, Signature)

Step 6: If H == H' → Signature VALID ✅
        (message from Alice, not altered)
        If H ≠ H'  → Signature INVALID ❌
```

**PGP sign + encrypt (both together):**
```
Sign first, then encrypt:
  1. Hash message → Sign with sender's private key
  2. Encrypt (message + signature) with
     recipient's public key via hybrid encryption
```

> [!NOTE]
> The order matters: **Sign then Encrypt**
> (not Encrypt then Sign). If you encrypt
> first, then sign the ciphertext — a recipient
> could strip the signature and re-sign with
> their own key, falsely claiming they created
> the ciphertext.

---

### 3.5 PGP Web of Trust

**Web of Trust** is PGP's decentralized trust
model — replacing the need for a central CA.

```
Alice's key is signed by Bob (Bob trusts Alice's key)
Bob's key is signed by Carol
Carol is in Dave's trust list

→ Dave can trust Alice's key TRANSITIVELY
  (through Carol → Bob → Alice)
```

**Trust levels in PGP:**

| Level | Meaning |
|-------|---------|
| **Unknown** | No information about key owner |
| **None** | Explicitly distrust this key owner's endorsements |
| **Marginal** | Partially trust — need 3 marginal trusts to validate |
| **Full** | Fully trust — 1 full trust validates a key |
| **Ultimate** | Complete trust — your own keys only |

**PGP validity calculation:**
```
A key K is considered VALID if:
  → You have directly signed K (ultimate/full trust)
  → OR: 1 person with FULL trust has signed K
  → OR: 3 persons with MARGINAL trust have signed K
```

---

### 3.6 OpenPGP and GPG

**OpenPGP** (RFC 4880, 2007) — the open standard
for PGP-compatible implementations. Defines:
- Message formats
- Key formats
- Signature formats
- Encryption algorithms
- Trust model mechanisms

**GnuPG (GPG)** — GNU Privacy Guard:
- Free, open-source implementation of OpenPGP
- Command-line tool — available on Linux, macOS,
  Windows
- Used by Thunderbird (Enigmail/built-in),
  ProtonMail, Signal (key exchange)

**GPG key generation:**
```bash
# Generate a new key pair
gpg --gen-key

# List public keys
gpg --list-keys

# List private keys
gpg --list-secret-keys

# Export public key
gpg --export --armor user@example.com > pubkey.asc

# Import a public key
gpg --import bobkey.asc

# Encrypt a file for Bob
gpg --encrypt --recipient bob@example.com file.txt

# Sign a file
gpg --sign file.txt

# Verify a signature
gpg --verify file.txt.gpg

# Decrypt a file
gpg --decrypt file.txt.gpg
```

---

### 3.7 PGP Key Servers

**PGP Key Servers** are public repositories
where users upload their PGP public keys for
others to discover and download.

| Key Server | URL | Notes |
|-----------|-----|-------|
| **SKS Keyserver Pool** | pool.sks-keyservers.net | Legacy — largely abandoned |
| **OpenPGP Keyserver** | keys.openpgp.org | Modern — requires email verification |
| **Ubuntu Keyserver** | keyserver.ubuntu.com | Widely used |
| **keys.mailvelope.com** | keys.mailvelope.com | Browser-based PGP |

**Key server problem:**
The old SKS keyserver pool had no verification
— anyone could upload keys for any email address,
including adding fake keys for others' addresses.
The **OpenPGP keyserver (keys.openpgp.org)**
requires email verification before publishing.

**Key poisoning attack (2019):**
Attackers flooded the SKS keyservers with
thousands of fake signatures on prominent
OpenPGP keys — making those keys so large
that GnuPG could not process them (denial
of service on key verification).

---

## 4. S/MIME — Secure/Multipurpose Internet
Mail Extensions

### 4.1 What is S/MIME?

**S/MIME (Secure/Multipurpose Internet Mail
Extensions)** is a standard for public key
encryption and signing of MIME data (email
content) — the email security standard used
by enterprise email clients (Outlook, Apple Mail).

| Property | Detail |
|----------|--------|
| **Current version** | S/MIME v4.0 (RFC 8551, 2019) |
| **Previous versions** | v3.2 (RFC 5751), v3.1 (RFC 3851) |
| **Based on** | PKCS#7 / CMS (Cryptographic Message Syntax) |
| **Trust model** | Hierarchical PKI (CA-based) |
| **Certificate type** | X.509 certificate with emailProtection EKU |
| **Used in** | Microsoft Outlook, Apple Mail, Thunderbird |

---

### 4.2 S/MIME vs PGP

| Property | S/MIME | PGP |
|----------|--------|-----|
| **Trust model** | Hierarchical PKI (CA) | Web of Trust (decentralized) |
| **Certificate/Key** | X.509 certificate from CA | PGP key pair (self-signed) |
| **Setup** | CA issues certificate (costs money) | User generates key (free) |
| **Key verification** | CA vouches (trusted automatically) | Manual verification required |
| **Enterprise use** | ✅ Preferred — integrates with AD | ⚠️ Complex for enterprise |
| **Personal use** | Harder (need CA cert) | Easier (GPG free) |
| **Message format** | PKCS#7 / CMS (ASN.1) | OpenPGP (RFC 4880) |
| **Algorithm agility** | Via CMS | Via OpenPGP |
| **Non-repudiation** | ✅ Strong (CA-backed cert) | ✅ Strong (key-backed) |
| **Interoperability** | High — all major clients | Limited — requires GPG support |

> [!IMPORTANT]
> **Enterprise choice: S/MIME**
> CA-issued certificates integrate with
> Active Directory and corporate PKI.
> Outlook, Exchange, and Apple Mail all support
> S/MIME natively.
>
> **Individual/activist choice: PGP/GPG**
> Free, no CA needed, decentralized.
> More privacy-preserving for journalists
> and activists.

---

### 4.3 S/MIME Operations

**S/MIME supports three main operations:**

#### Signing Only (Clear Signing)
```
Email body (plaintext, readable)
+
Digital Signature (PKCS#7 SignedData)
     ↓
Recipient can read email WITHOUT S/MIME support
Recipient WITH S/MIME support can VERIFY signature
```
File type: `.p7s` (detached signature)
or `multipart/signed` MIME type

#### Encryption Only
```
Email body encrypted with recipient's public key
(Hybrid: AES session key encrypted with RSA)
     ↓
PKCS#7 EnvelopedData structure
     ↓
Recipient MUST have S/MIME support to read
```

#### Sign and Encrypt (Both)
```
Sign first (with sender's private key)
→ Encrypt the signed message
  (with recipient's public key)
     ↓
PKCS#7 SignedAndEnvelopedData structure
```

> [!NOTE]
> The convention is always **Sign then Encrypt**
> — same as PGP. Signing inside the encryption
> envelope proves the signer created the specific
> plaintext (not the ciphertext).

---

### 4.4 S/MIME Certificate Requirements

For S/MIME to work, both parties need:

**Sender's requirements (for signing):**
- X.509 certificate with
  `emailProtection` EKU (Extended Key Usage)
- Private key corresponding to the certificate

**Recipient's requirements (for encryption):**
- Sender must have recipient's certificate
  (with recipient's public key) to encrypt

**How S/MIME certificates are obtained:**
1. Purchase from a commercial CA (DigiCert,
   Sectigo, Comodo)
2. Issue from an internal CA (ADCS)
3. Free options: Actalis, Let's Encrypt
   (no email certs yet), some CAs offer free S/MIME

**S/MIME certificate validation levels:**

| Type | Verification | Cost |
|------|-------------|------|
| **MPKI / Basic** | Email address only | Free / Low |
| **Individual validation** | Name + email | Low |
| **Organization validation** | Organization + email | Medium |

---

### 4.5 S/MIME in Email Clients

**Microsoft Outlook:**
```
Certificate import:
  File → Options → Trust Center → Email Security
  → Import/Export → Import certificate (.pfx/.p12)
  → Set as default certificate for email account

Signing: New Email → Options → Sign (S/MIME icon)
Encrypting: New Email → Options → Encrypt
```

**Apple Mail (macOS/iOS):**
- Import certificate via Keychain Access
- Mail automatically uses S/MIME certificate
  for associated email address
- Sign/Encrypt icons appear automatically
  when composing

**Thunderbird:**
- Originally required Enigmail extension for PGP
- Since Thunderbird 78 (2020): built-in support
  for both S/MIME AND OpenPGP

---

## 5. 📌 Extra Notes

> [!NOTE]
> Everything in this section goes beyond the core
> syllabus but is directly MCQ-relevant.

---

### 5.1 SSL/TLS Attack History

> [!NOTE]

| Attack | Year | Target | Mechanism | Fix |
|--------|------|--------|-----------|-----|
| **BEAST** | 2011 | TLS 1.0 CBC | Predictable IV | Use TLS 1.2+, GCM |
| **CRIME** | 2012 | TLS compression | Length side-channel | Disable compression |
| **BREACH** | 2013 | HTTP compression | Length side-channel | Disable HTTP compression |
| **Lucky Thirteen** | 2013 | TLS CBC | MAC timing oracle | Use AEAD (GCM) |
| **Heartbleed** | 2014 | OpenSSL | Buffer over-read | Update OpenSSL |
| **POODLE** | 2014 | SSL 3.0 | CBC padding oracle | Disable SSL 3.0 |
| **FREAK** | 2015 | TLS | Export RSA downgrade | Disable export suites |
| **Logjam** | 2015 | TLS DHE | Export DH downgrade | Use 2048-bit+ DH |
| **DROWN** | 2016 | TLS | SSLv2 exposure | Disable SSLv2 everywhere |
| **ROBOT** | 2017 | TLS RSA | Bleichenbacher redux | OAEP / TLS 1.3 |
| **Raccoon** | 2020 | TLS DH | Timing on DH | Use ECDHE |

> [!NOTE]
> **Heartbleed (CVE-2014-0160)** was NOT a
> TLS protocol flaw — it was a bug in the
> OpenSSL implementation of the TLS Heartbeat
> extension. A missing bounds check allowed
> up to 64KB of server memory to be read —
> potentially exposing private keys, session
> tokens, and passwords.

---

### 5.2 TLS Certificate Pinning

> [!NOTE]
> **Certificate Pinning** — see also Session 07/08.
> In TLS context:

**HTTP Public Key Pinning (HPKP) — deprecated:**
- RFC 7469 — sent as an HTTP header
- Browser stores the pinned public key hash
- Subsequent connections reject any cert with
  a different key hash — even if CA-signed
- **Deprecated in 2018** — too risky
  (misconfiguration = permanent lockout)

**Modern alternative — Certificate Transparency:**
- All certificates logged publicly
- Domain owners monitor CT logs for unauthorized
  certs
- Chrome requires SCT in certificates since 2018

**Application-level pinning (mobile apps):**
- App hardcodes expected certificate/public key
- Rejects any other cert during TLS — preventing
  MITM even with trusted CA
- Still used in mobile apps (iOS, Android)

---

### 5.3 HSTS — HTTP Strict Transport Security

> [!NOTE]
> **HSTS (HTTP Strict Transport Security)** is
> an HTTP response header that tells browsers
> to ONLY connect to this site over HTTPS —
> never HTTP — for a specified period.

```
Strict-Transport-Security:
  max-age=31536000;
  includeSubDomains;
  preload

max-age:         Seconds browser must remember to
                 use HTTPS (31536000 = 1 year)
includeSubDomains: Apply to all subdomains
preload:         Request inclusion in browser's
                 built-in HSTS preload list
```

**HSTS prevents:**
- SSL stripping attacks (downgrading HTTPS to HTTP)
- Accidental HTTP connections

**HSTS preload list:**
- Chrome, Firefox, Safari, Edge maintain a built-in
  list of HSTS domains (hstspreload.org)
- First connection to a preloaded domain is
  ALWAYS HTTPS — even first ever visit
- Added permanently — difficult to remove

---

### 5.4 SNI — Server Name Indication

> [!NOTE]
> **SNI (Server Name Indication)** is a TLS
> extension that allows a client to specify
> which hostname it is connecting to during the
> TLS handshake — BEFORE the server sends its
> certificate.

**Problem SNI solves:**
```
One IP address hosts multiple HTTPS websites:
  192.168.1.1 → www.example.com
  192.168.1.1 → www.other.com

Without SNI:
  Server sees TCP connection to port 443
  Server doesn't know WHICH certificate to send
  → Can only send one certificate → wrong site

With SNI:
  Client includes hostname in ClientHello:
  server_name = "www.example.com"
  → Server selects correct certificate ✅
```

**SNI privacy concern:**
The SNI extension is sent in **plaintext**
in the TLS ClientHello — even for HTTPS.
Network observers can see which hostname
you are connecting to before encryption starts.

**ESNI / ECH — Encrypted Client Hello:**
A newer TLS extension that encrypts the
ClientHello (including SNI) using a public
key published in DNS — hiding the hostname
from network observers. Chrome and Firefox
support ECH.

---

### 5.5 Certificate Transparency in TLS

> [!NOTE]
> CT (covered in Sessions 07/08) is enforced
> in TLS specifically through the SCT mechanism:

**How SCT is delivered in TLS:**

| Method | Description |
|--------|-------------|
| **Embedded in cert** | CA embeds SCT from CT log during signing |
| **TLS extension** | Server sends SCT in TLS handshake extension |
| **OCSP stapling** | SCT delivered via stapled OCSP response |

**Chrome CT policy:**
Since April 2018, Chrome requires either:
- 2 SCTs from independent CT logs (Certificates
  valid > 180 days)
- 1 SCT for short-lived certs

Certificates without SCTs are rejected by
Chrome with `ERR_CERTIFICATE_TRANSPARENCY_REQUIRED`.

---

### 5.6 TLS 1.3 — Removed and Added Features

> [!NOTE]
> A detailed breakdown of what TLS 1.3
> specifically added and removed:

**Removed from TLS 1.3:**

| Removed Feature | Reason |
|----------------|--------|
| Static RSA key exchange | No PFS |
| Static DH key exchange | No PFS |
| CBC mode cipher suites | POODLE, Lucky 13, BEAST |
| RC4 | Broken |
| DES, 3DES | Too weak |
| MD5, SHA-1 in PRF | Weak hash |
| TLS compression | CRIME attack |
| Renegotiation | Security issues |
| Custom DHE groups | Logjam |
| Export cipher suites | FREAK, Logjam |
| SSLv2 Hello compatibility | DROWN |

**Added/Changed in TLS 1.3:**

| Feature | Detail |
|---------|--------|
| Reduced to 1-RTT | Faster connection |
| 0-RTT resumption | Session tickets (PSK) |
| Encrypted handshake | Certificate hidden from observers |
| Only AEAD ciphers | GCM, CCM, ChaCha20-Poly1305 |
| HKDF key schedule | RFC 5869 HKDF for all key derivation |
| New alert types | More specific error reporting |
| Downgrade protection | Sentinal values in ServerRandom |

---

### 5.7 ALPN — Application Layer Protocol
Negotiation

> [!NOTE]
> **ALPN (Application Layer Protocol Negotiation)**
> is a TLS extension that allows the client and
> server to negotiate which application protocol
> to use over TLS — during the TLS handshake.

**Why ALPN is needed:**
Without ALPN, the server would need separate
ports for HTTP/1.1 and HTTP/2 over TLS. ALPN
lets both use port 443 with the same TLS
connection — the application protocol is
negotiated inside TLS.

**Common ALPN identifiers:**

| Protocol | ALPN ID |
|----------|---------|
| HTTP/1.1 | `http/1.1` |
| HTTP/2 | `h2` |
| HTTP/3 (QUIC) | `h3` |
| SPDY | `spdy/3.1` |
| WebRTC | `webrtc`, `c-webrtc` |

---

### 5.8 mTLS — Mutual TLS

> [!NOTE]
> **mTLS (Mutual TLS)** extends standard TLS
> by requiring BOTH the client AND the server
> to present X.509 certificates — both sides
> authenticate each other.

```
Standard TLS:
  Client verifies SERVER certificate only
  Server trusts any connected client

Mutual TLS (mTLS):
  Client verifies SERVER certificate ✅
  Server verifies CLIENT certificate ✅
  Both sides authenticated
```

**mTLS in TLS 1.2 handshake additions:**
```
...after ServerHelloDone...
  ←── CertificateRequest (server requests client cert)
  ──→ Certificate (client sends its cert)
  ──→ CertificateVerify (client proves key possession)
...then Finished exchange...
```

**Where mTLS is used:**

| Use Case | Why |
|----------|-----|
| **Zero Trust** | Every service authenticates every other service |
| **API authentication** | Client proves identity via certificate |
| **Service mesh** | Istio/Linkerd use mTLS between microservices |
| **EAP-TLS** | Wi-Fi — client and server both present certs |
| **Banking APIs** | High-security client authentication |
| **IoT devices** | Device identity via certificate |

---

### 5.9 PGP Fingerprint and Key Verification

> [!NOTE]
> **PGP key fingerprint** is a hash of the
> public key — used to verify key authenticity
> out-of-band.

```
Example PGP fingerprint (SHA-1 based, 40 hex chars):
  D8FF BE88 9146 3201 61F3  4AE7 1B05 2735 3A19 6E7C
  (20 bytes = 160-bit SHA-1 hash of public key)

Modern keys use SHA-256 fingerprints (v5 keys).
```

**Why fingerprint verification matters:**
```
Alice uploads her PGP key to a keyserver.
Bob downloads a key claiming to be Alice's.

Without fingerprint verification:
  → Bob might download a fake key from an attacker
  → Encrypt message → attacker reads it

With fingerprint verification:
  → Alice tells Bob her fingerprint via phone/Signal
  → Bob verifies downloaded key's fingerprint matches
  → Only correct key has that fingerprint ✅
```

**Key signing parties:**
Physical meetings where people verify each
other's key fingerprints in person and sign
each other's keys — building the Web of Trust.

---

### 5.10 DKIM, SPF, DMARC — Email Authentication

> [!NOTE]
> While S/MIME and PGP provide end-to-end
> message-level security, these DNS-based
> mechanisms provide **domain-level email
> authentication** at the mail server level.

| Mechanism | Full Name | Purpose |
|-----------|-----------|---------|
| **SPF** | Sender Policy Framework | Specifies which mail servers are authorized to send email for a domain |
| **DKIM** | DomainKeys Identified Mail | Adds a cryptographic signature to outgoing email — verifiable by recipient's server |
| **DMARC** | Domain-based Message Authentication, Reporting & Conformance | Policy specifying what to do with emails failing SPF/DKIM checks |

**SPF (RFC 7208):**
```
DNS TXT record for example.com:
  v=spf1 include:_spf.google.com ~all
  ↑ This email came from Google's servers

Receiving server checks:
  Does sender IP match SPF record? Yes → pass
                                    No → fail/softfail
```

**DKIM (RFC 6376):**
```
Sending server:
  Signs email headers+body with domain's private key
  Adds DKIM-Signature: header

Receiving server:
  Retrieves DKIM public key from DNS
  Verifies signature → email unmodified ✅
  Failed signature → possible forgery ❌
```

**DMARC (RFC 7489):**
```
DNS TXT record _dmarc.example.com:
  v=DMARC1; p=reject; rua=mailto:reports@example.com
             ↑ What to do with failing emails:
               none (monitor only)
               quarantine (spam folder)
               reject (refuse delivery)
```

> [!NOTE]
> DKIM, SPF, and DMARC protect against
> **email spoofing and phishing** at the
> domain level. They are complementary to
> S/MIME and PGP — which protect the message
> content. Many modern organizations deploy
> all three PLUS S/MIME for comprehensive
> email security.

---

### 5.11 OpenSSL Commands — Reference

> [!NOTE]
> OpenSSL is used in the Session 13 lab.
> These commands are essential for understanding
> the theory in practice.

```bash
# Generate RSA private key
openssl genrsa -out ca.key 4096

# Generate self-signed Root CA certificate
openssl req -new -x509 -days 3650 \
  -key ca.key -out ca.crt \
  -subj "/C=IN/ST=Maharashtra/L=Pune/O=DITISS/CN=DITISS Root CA"

# Generate Sub CA private key and CSR
openssl genrsa -out subca.key 4096
openssl req -new -key subca.key -out subca.csr \
  -subj "/C=IN/O=DITISS/CN=DITISS Sub CA"

# Sign Sub CA CSR with Root CA
openssl x509 -req -days 1825 \
  -in subca.csr -CA ca.crt -CAkey ca.key \
  -CAcreateserial -out subca.crt \
  -extensions v3_ca

# Generate server key and CSR
openssl genrsa -out server.key 2048
openssl req -new -key server.key -out server.csr \
  -subj "/C=IN/O=DITISS/CN=www.pgditiss.local"

# Sign server CSR with Sub CA
openssl x509 -req -days 365 \
  -in server.csr -CA subca.crt -CAkey subca.key \
  -CAcreateserial -out server.crt

# Create full certificate chain
cat server.crt subca.crt ca.crt > chain.crt

# Verify the certificate chain
openssl verify -CAfile ca.crt -untrusted subca.crt server.crt

# View certificate details
openssl x509 -in server.crt -text -noout

# Test TLS connection
openssl s_client -connect www.pgditiss.local:443 \
  -CAfile ca.crt

# Create PKCS#12 bundle
openssl pkcs12 -export \
  -in server.crt -inkey server.key \
  -certfile subca.crt \
  -out server.pfx

# Check what TLS versions a server supports
openssl s_client -connect example.com:443 -tls1_2
openssl s_client -connect example.com:443 -tls1_3

# Generate DH parameters (for TLS DHE)
openssl dhparam -out dhparam.pem 2048
```

---

### 5.12 TLS in Modern Applications

> [!NOTE]

**TLS everywhere — modern deployment:**

| Application | TLS Version | Notes |
|-------------|------------|-------|
| **HTTPS (web)** | TLS 1.2/1.3 | 443 |
| **SMTP submission** | TLS 1.2+ | Port 587 (STARTTLS) |
| **IMAPS** | TLS 1.2+ | Port 993 (implicit TLS) |
| **LDAPS** | TLS 1.2+ | Port 636 |
| **FTPS** | TLS 1.2+ | Port 990/21 |
| **DoT (DNS over TLS)** | TLS 1.2+ | Port 853 |
| **MQTT (IoT)** | TLS 1.2+ | Port 8883 |

**QUIC and HTTP/3:**
HTTP/3 uses QUIC (UDP-based transport) with
TLS 1.3 integrated. QUIC handles both
transport and TLS — eliminating the TCP +
TLS handshake overhead and improving
performance on lossy networks.

**STARTTLS vs Implicit TLS:**

| Type | Behavior |
|------|---------|
| **STARTTLS** | Start plaintext → upgrade to TLS via STARTTLS command |
| **Implicit TLS** | TLS from the very first byte — no plaintext at all |
| **Recommendation** | Implicit TLS preferred — STARTTLS has downgrade risks |

---

## 6. Abbreviations Table

| Abbreviation | Full Form | One-Line Technical Meaning |
|---|---|---|
| SSL | Secure Sockets Layer | Original Netscape protocol for HTTPS — all versions deprecated |
| TLS | Transport Layer Security | Current successor to SSL — provides confidentiality, integrity, auth |
| HTTPS | HTTP Secure | HTTP over TLS — port 443 — encrypted web traffic |
| PGP | Pretty Good Privacy | Phil Zimmermann's hybrid encryption for email — 1991 |
| GPG | GNU Privacy Guard | Free open-source implementation of OpenPGP (RFC 4880) |
| S/MIME | Secure/Multipurpose Internet Mail Extensions | CA-based email signing and encryption — PKCS#7/CMS |
| SNI | Server Name Indication | TLS extension — client specifies hostname in ClientHello |
| ALPN | Application Layer Protocol Negotiation | TLS extension — negotiate HTTP/1.1 vs HTTP/2 |
| HSTS | HTTP Strict Transport Security | HTTP header forcing HTTPS-only connections |
| mTLS | Mutual TLS | Both client and server authenticate with certificates |
| ECH | Encrypted Client Hello | TLS extension encrypting SNI for privacy |
| ESNI | Encrypted Server Name Indication | Predecessor to ECH |
| AEAD | Authenticated Encryption with Associated Data | Encryption providing confidentiality + integrity in one operation |
| PFS | Perfect Forward Secrecy | Past session keys safe even if long-term key compromised |
| RTT | Round-Trip Time | Network latency measure — TLS 1.3 reduces handshake to 1 RTT |
| PSK | Pre-Shared Key | Session resumption mechanism in TLS 1.3 (replaces session IDs) |
| SCT | Signed Certificate Timestamp | Proof a cert was submitted to a CT log |
| HKDF | HMAC-based Key Derivation Function | TLS 1.3 key schedule — RFC 5869 |
| PRF | Pseudo-Random Function | TLS 1.2 key derivation function |
| SPF | Sender Policy Framework | DNS record specifying authorized mail servers for a domain |
| DKIM | DomainKeys Identified Mail | Cryptographic email signing at domain level |
| DMARC | Domain-based Message Auth, Reporting & Conformance | Policy for handling SPF/DKIM failures |
| STARTTLS | STARTTLS | Email protocol command to upgrade plaintext to TLS |
| ECDHE | Elliptic Curve Diffie-Hellman Ephemeral | Key exchange providing PFS — mandatory in TLS 1.3 |

---

## 7. Keywords + Concept Map

| Term | Definition | Connections | Use Cases |
|------|-----------|-------------|-----------|
| **SSL** | Deprecated Netscape protocol — all versions broken | POODLE, BEAST, DROWN, TLS replaced it | Historical context only |
| **TLS 1.2** | Current standard — RFC 5246, 2008 | Optional PFS, HMAC or AEAD | Most web servers today |
| **TLS 1.3** | Latest standard — RFC 8446, 2018 | Mandatory PFS, AEAD only, 1-RTT | Modern HTTPS |
| **Cipher suite** | Named algorithm combination for TLS | Key exchange + auth + encryption + hash | TLS negotiation |
| **PGP** | Hybrid encryption for email — Web of Trust | RFC 4880, OpenPGP, GPG, Zimmermann | Email, file encryption |
| **S/MIME** | CA-based email security — PKCS#7/CMS | RFC 8551, Outlook, X.509, emailProtection EKU | Enterprise email |
| **mTLS** | Both sides authenticate with certs | Zero Trust, EAP-TLS, service mesh | API security, Zero Trust |
| **HSTS** | Forces HTTPS-only browser connections | SSL stripping prevention, preload list | Web security |
| **SNI** | Client sends hostname in TLS ClientHello | Virtual hosting HTTPS, ECH privacy | Multi-tenant HTTPS |
| **Web of Trust** | PGP's decentralized trust — user vouching | 1 full / 3 marginal trust = valid | PGP key trust |
| **ALPN** | Negotiate HTTP version inside TLS | HTTP/2, HTTP/3 selection | Modern web performance |
| **DKIM/SPF/DMARC** | DNS-based domain email authentication | Complements S/MIME at server level | Anti-phishing, anti-spoofing |

---

## 8. Quick Reference Cheatsheet

### 🔸 SSL/TLS Version Status

| Version | RFC | Year | Status |
|---------|-----|------|--------|
| SSL 1.0 | — | 1994 | Never released |
| SSL 2.0 | — | 1995 | ❌ Broken |
| SSL 3.0 | — | 1996 | ❌ Broken (POODLE) |
| TLS 1.0 | 2246 | 1999 | ❌ Deprecated (RFC 8996) |
| TLS 1.1 | 4346 | 2006 | ❌ Deprecated (RFC 8996) |
| TLS 1.2 | 5246 | 2008 | ✅ Current |
| TLS 1.3 | 8446 | 2018 | ✅ Recommended |

---

### 🔸 TLS 1.2 vs TLS 1.3

| Feature | TLS 1.2 | TLS 1.3 |
|---------|---------|---------|
| RTT | 2 | 1 |
| PFS | Optional | Mandatory |
| Static RSA | ✅ | ❌ Removed |
| Cipher suites | Many | 5 (all AEAD) |
| Compression | Optional | ❌ Removed |
| Certificate visible | Yes | Encrypted |

---

### 🔸 PGP vs S/MIME

| | PGP | S/MIME |
|---|-----|--------|
| Trust model | Web of Trust | CA Hierarchy |
| Standard | RFC 4880 | RFC 8551 |
| Key type | PGP key pair | X.509 certificate |
| Cost | Free | CA cert cost |
| Enterprise | Complex | Easy (AD integration) |
| Format | OpenPGP | PKCS#7/CMS |

---

### 🔸 TLS 1.3 Cipher Suites (All 5)

```
TLS_AES_128_GCM_SHA256
TLS_AES_256_GCM_SHA384
TLS_CHACHA20_POLY1305_SHA256
TLS_AES_128_CCM_SHA256
TLS_AES_128_CCM_8_SHA256
```
All use AEAD — no separate MAC needed.

---

### 🔸 TLS Handshake RTT Comparison

```
TLS 1.2:  Client → Server (1 RTT)
           Server → Client (2 RTT)
           Data begins after 2 RTT

TLS 1.3:  Client → Server (1 RTT — includes key share)
           Server → Client + Certificate
           Data begins after 1 RTT ✅

TLS 1.3 0-RTT:  Client sends data with first message
                (session resumption — replay risk)
```

---

### 🔸 OpenSSL Key Commands

```bash
# Root CA
openssl genrsa -out ca.key 4096
openssl req -new -x509 -days 3650 -key ca.key -out ca.crt

# Sub CA
openssl genrsa -out subca.key 4096
openssl req -new -key subca.key -out subca.csr
openssl x509 -req -CA ca.crt -CAkey ca.key -in subca.csr -out subca.crt

# Server cert
openssl genrsa -out server.key 2048
openssl req -new -key server.key -out server.csr
openssl x509 -req -CA subca.crt -CAkey subca.key -in server.csr -out server.crt

# Verify chain
openssl verify -CAfile ca.crt -untrusted subca.crt server.crt

# Test TLS
openssl s_client -connect domain:443 -CAfile ca.crt
```

---

### 🔸 Email Security Stack

| Layer | Technology | Protects |
|-------|-----------|---------|
| Transport | TLS/STARTTLS | Server-to-server encryption |
| Domain | SPF | Authorized senders |
| Domain | DKIM | Message integrity (server-signed) |
| Domain | DMARC | Policy for failures |
| End-to-end | S/MIME | Message confidentiality + signature |
| End-to-end | PGP | Message confidentiality + signature |

---

## 9. Session Revision Snapshot

### ⚡ TL;DR — 5 Bullets

- ✅ SSL is dead — all SSL versions broken; TLS
  1.0/1.1 deprecated (RFC 8996, 2021); TLS 1.2
  (RFC 5246, 2008) is current minimum; TLS 1.3
  (RFC 8446, 2018) is the recommended standard —
  1-RTT handshake, mandatory PFS (ECDHE), AEAD
  ciphers only, encrypted certificate exchange
- ✅ TLS 1.3 removed: static RSA, static DH,
  CBC ciphers, RC4, 3DES, MD5/SHA-1 in PRF,
  compression, renegotiation, export suites —
  only 5 cipher suites remain, all AEAD (GCM
  or ChaCha20-Poly1305)
- ✅ PGP (Phil Zimmermann, 1991) = hybrid
  encryption for email using Web of Trust
  (decentralized, 1 full / 3 marginal = valid);
  OpenPGP = RFC 4880; GPG = free implementation;
  sign-then-encrypt convention
- ✅ S/MIME (RFC 8551) = CA-based email security
  using PKCS#7/CMS — needs X.509 certificate
  with emailProtection EKU — enterprise standard
  integrating with Outlook/AD; always
  sign-then-encrypt
- ✅ PGP vs S/MIME: PGP uses Web of Trust +
  OpenPGP format + free; S/MIME uses CA hierarchy
  + PKCS#7 format + CA cert cost — both provide
  email signing and encryption but different
  trust models make them suitable for different
  contexts

---

### 🎯 MCQ-Likely Concepts — Everything Examiners Love

| Concept | Why It's Tricky |
|---------|----------------|
| TLS 1.3 RFC = 8446 (2018) | Specific RFC number tested |
| TLS 1.2 RFC = 5246 (2008) | Specific RFC number tested |
| TLS 1.0/1.1 deprecated by RFC 8996 | Year and RFC number |
| POODLE attacks SSL 3.0 (2014) | Year + specific target |
| BEAST attacks TLS 1.0 (2011) | Year + specific target |
| TLS 1.3 = 1-RTT; TLS 1.2 = 2-RTT | Specific handshake difference |
| TLS 1.3 has only 5 cipher suites — all AEAD | No non-AEAD ciphers |
| PFS mandatory in TLS 1.3 — optional in 1.2 | Version-specific |
| Static RSA removed from TLS 1.3 | Key PFS enforcement |
| PGP created by Phil Zimmermann, 1991 | Year + creator |
| OpenPGP = RFC 4880; GPG = implementation | Standard vs tool distinction |
| PGP trust: 1 full OR 3 marginal = valid | Specific trust calculation |
| S/MIME = RFC 8551 (latest version) | Specific RFC |
| S/MIME uses PKCS#7/CMS format | Format name tested |
| Sign-then-encrypt (both PGP and S/MIME) | Order matters |
| emailProtection EKU needed for S/MIME cert | Specific EKU |
| HTTPS = HTTP over TLS, port 443 | Port number tested |
| SNI = hostname in ClientHello (plaintext) | Privacy implication |
| HSTS prevents SSL stripping attacks | Specific attack prevented |
| mTLS = both client and server authenticate | vs standard TLS (server only) |
| DKIM = cryptographic email signature (server) | vs S/MIME (end-to-end) |
| Heartbleed = OpenSSL buffer over-read (not TLS flaw) | Common misclassification |

---

<details>
<summary>🔬 Lab — Session 13 (OpenSSL PKI Hierarchy)</summary>

**Lab file:** `3-Labs/lab-session-13-openssl-pki.md`

**Tool:** OpenSSL (command-line)

**Lab Tasks:**
1. Create a Root CA on Debian Linux
   (`rtca.pgditiss.local`)
2. Create a Sub CA on Debian Linux
   (`sbca.pgditiss.local`)
3. Sign the Sub CA certificate with the Root CA
4. Issue a server certificate for
   `www.pgditiss.local` signed by the Sub CA
5. Set up Apache HTTPS website with the
   issued certificate and certificate chain
6. Configure DNS/hosts resolution for
   `www.pgditiss.local`
7. Access `https://www.pgditiss.local` from
   Windows machine
8. Import the Root CA certificate into the
   Windows browser to remove the certificate
   warning

**Theory ↔ Lab Connection:**

| Session 13 Theory Concept | Lab Demonstration |
|--------------------------|------------------|
| TLS certificate chain (Root → Sub CA → End Entity) | Built step-by-step in lab |
| X.509 certificate structure | OpenSSL `x509 -text` shows all fields |
| CSR creation (PKCS#10) | `openssl req -new` creates CSR |
| CA signing a CSR | `openssl x509 -req -CA` signs it |
| Certificate chain validation | `openssl verify -CAfile` confirms chain |
| HTTPS server setup | Apache + TLS cert configuration |
| Browser trust store import | Importing Root CA removes warning |
| Self-signed vs CA-signed | Before import: warning; After: trusted |
| TLS in practice | `openssl s_client` connects and shows cert |
| PEM format in use | All certs in `.crt` (PEM) format |

**Key OpenSSL commands used:**
```bash
# Create Root CA
openssl genrsa -out rootca.key 4096
openssl req -new -x509 -days 3650 \
  -key rootca.key -out rootca.crt

# Create Sub CA (signed by Root CA)
openssl genrsa -out subca.key 4096
openssl req -new -key subca.key -out subca.csr
openssl x509 -req -days 1825 \
  -in subca.csr \
  -CA rootca.crt -CAkey rootca.key \
  -CAcreateserial -out subca.crt \
  -extensions v3_ca

# Create server cert (signed by Sub CA)
openssl genrsa -out server.key 2048
openssl req -new -key server.key -out server.csr \
  -subj "/CN=www.pgditiss.local"
openssl x509 -req -days 365 \
  -in server.csr \
  -CA subca.crt -CAkey subca.key \
  -CAcreateserial -out server.crt

# Create cert chain file for Apache
cat server.crt subca.crt > server_chain.crt

# Verify chain
openssl verify -CAfile rootca.crt \
  -untrusted subca.crt server.crt

# Test HTTPS connection
openssl s_client \
  -connect www.pgditiss.local:443 \
  -CAfile rootca.crt
```

**Full step-by-step lab guide:**
`3-Labs/lab-session-13-openssl-pki.md`

</details>

---