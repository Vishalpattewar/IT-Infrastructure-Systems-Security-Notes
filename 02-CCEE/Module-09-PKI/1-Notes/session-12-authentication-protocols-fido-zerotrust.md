# Session 12 — Authentication Protocols, FIDO
Authentication & Zero Trust Architecture

## 📑 Table of Contents

- [1. Authentication Protocols](#1-authentication-protocols)
  - [1.1 What is an Authentication
    Protocol?](#11-what-is-an-authentication-protocol)
  - [1.2 PAP — Password Authentication
    Protocol](#12-pap--password-authentication-protocol)
  - [1.3 CHAP — Challenge Handshake
    Authentication Protocol](#13-chap--challenge-handshake-authentication-protocol)
  - [1.4 EAP — Extensible Authentication
    Protocol](#14-eap--extensible-authentication-protocol)
  - [1.5 EAP Methods](#15-eap-methods)
  - [1.6 802.1X — Port-Based Network Access
    Control](#16-8021x--port-based-network-access-control)
  - [1.7 LDAP Authentication](#17-ldap-authentication)
  - [1.8 NTLM — NT LAN Manager](#18-ntlm--nt-lan-manager)
  - [1.9 Protocol Comparison Table](#19-protocol-comparison-table)
- [2. FIDO Authentication](#2-fido-authentication)
  - [2.1 What is FIDO?](#21-what-is-fido)
  - [2.2 FIDO Alliance](#22-fido-alliance)
  - [2.3 FIDO U2F — Universal 2nd
    Factor](#23-fido-u2f--universal-2nd-factor)
  - [2.4 FIDO2 — The Modern Standard](#24-fido2--the-modern-standard)
  - [2.5 WebAuthn — Web Authentication
    API](#25-webauthn--web-authentication-api)
  - [2.6 CTAP2 — Client to Authenticator
    Protocol](#26-ctap2--client-to-authenticator-protocol)
  - [2.7 FIDO2 Authentication Flow](#27-fido2-authentication-flow)
  - [2.8 FIDO2 Authenticator Types](#28-fido2-authenticator-types)
  - [2.9 Why FIDO2 is Phishing-Resistant](#29-why-fido2-is-phishing-resistant)
  - [2.10 FIDO2 vs TOTP vs SMS OTP](#210-fido2-vs-totp-vs-sms-otp)
- [3. Zero Trust Architecture](#3-zero-trust-architecture)
  - [3.1 What is Zero Trust?](#31-what-is-zero-trust)
  - [3.2 The Traditional Perimeter Model —
    Why It Failed](#32-the-traditional-perimeter-model--why-it-failed)
  - [3.3 Zero Trust Core Principles](#33-zero-trust-core-principles)
  - [3.4 Zero Trust Components](#34-zero-trust-components)
  - [3.5 NIST Zero Trust Architecture —
    SP 800-207](#35-nist-zero-trust-architecture--sp-800-207)
  - [3.6 Zero Trust vs Traditional
    Perimeter Security](#36-zero-trust-vs-traditional-perimeter-security)
  - [3.7 Zero Trust Implementation
    Pillars](#37-zero-trust-implementation-pillars)
  - [3.8 Zero Trust and PKI](#38-zero-trust-and-pki)
- [4. 📌 Extra Notes](#4--extra-notes)
  - [4.1 EAP-TLS — The Gold Standard](#41-eap-tls--the-gold-standard)
  - [4.2 RADIUS and 802.1X — How They
    Work Together](#42-radius-and-8021x--how-they-work-together)
  - [4.3 FIDO2 Resident Keys
    (Discoverable Credentials)](#43-fido2-resident-keys-discoverable-credentials)
  - [4.4 Attestation in FIDO2](#44-attestation-in-fido2)
  - [4.5 Passkeys vs Hardware Security
    Keys](#45-passkeys-vs-hardware-security-keys)
  - [4.6 BeyondCorp — Google's Zero Trust
    Implementation](#46-beyondcorp--googles-zero-trust-implementation)
  - [4.7 Zero Trust Maturity Model —
    CISA](#47-zero-trust-maturity-model--cisa)
  - [4.8 Microsegmentation](#48-microsegmentation)
  - [4.9 Software-Defined Perimeter (SDP)](#49-software-defined-perimeter-sdp)
  - [4.10 NTLM Attacks](#410-ntlm-attacks)
  - [4.11 Kerberos vs NTLM](#411-kerberos-vs-ntlm)
  - [4.12 LDAP vs Active Directory](#412-ldap-vs-active-directory)
  - [4.13 PAM — Privileged Access
    Management](#413-pam--privileged-access-management)
- [5. Abbreviations Table](#5-abbreviations-table)
- [6. Keywords + Concept Map](#6-keywords--concept-map)
- [7. Quick Reference Cheatsheet](#7-quick-reference-cheatsheet)
- [8. Session Revision Snapshot](#8-session-revision-snapshot)

---

## 1. Authentication Protocols

### 1.1 What is an Authentication Protocol?

An **authentication protocol** is a set of rules
and message exchanges that define how one entity
proves its identity to another over a network —
specifying the format, sequence, and cryptographic
mechanisms used.

**Why protocols matter:**
An algorithm like HMAC-SHA1 is a primitive.
An authentication protocol specifies:
- Who sends what message to whom
- What challenges/responses are exchanged
- How the identity proof is verified
- What happens if verification fails

---

### 1.2 PAP — Password Authentication Protocol

**PAP (Password Authentication Protocol)** is the
simplest — and least secure — authentication
protocol used in dial-up and PPP (Point-to-Point
Protocol) connections.

| Property | Detail |
|----------|--------|
| **Standard** | RFC 1334 (1992) |
| **Used in** | PPP connections, legacy VPN, older RADIUS configurations |
| **Security** | ❌ Very weak — sends password in cleartext |
| **Status** | Deprecated — never use on untrusted networks |

**PAP Authentication Flow:**
```
Client                          Server
  │                               │
  │── Username + Password ───────→│
  │   (plaintext — no encryption) │
  │                               │ Checks against password DB
  │←── ACK (success) or NAK ─────│
  │    (failure)                  │
```

> [!IMPORTANT]
> PAP sends the actual password in **plaintext**
> over the network. An eavesdropper can capture
> the password with a simple packet capture.
> PAP should NEVER be used on any network where
> confidentiality matters.

---

### 1.3 CHAP — Challenge Handshake
Authentication Protocol

**CHAP (Challenge Handshake Authentication
Protocol)** improves on PAP by using a
challenge-response mechanism — the password
is NEVER sent over the network.

| Property | Detail |
|----------|--------|
| **Standard** | RFC 1994 (1996) |
| **Used in** | PPP, older VPNs, some RADIUS deployments |
| **Security** | Better than PAP — password not transmitted |
| **Mechanism** | Challenge-response using MD5 HMAC |
| **Status** | Functional but aging — MD5 weakness noted |

**CHAP Authentication Flow:**
```
Client                          Server
  │                               │
  │←── Challenge (random nonce) ──│
  │    (server sends random value) │
  │                               │
  │ Client computes:               │
  │ Response = MD5(ID + Secret + Challenge)
  │                               │
  │── Response ──────────────────→│
  │                               │ Server computes same MD5
  │                               │ Compares with received response
  │←── Success or Failure ────────│
```

**CHAP security properties:**
- Password never sent over the network ✅
- Challenge is different each time — prevents
  replay attacks ✅
- Uses MD5 — MD5 is cryptographically weak ⚠️
- Server must store password in recoverable form
  (to recompute the MD5) — cannot use salted
  hashing ❌

**MS-CHAPv2:**
Microsoft's enhanced version — used in PPTP VPN
and older WPA Enterprise. Uses MS-specific
challenge-response but was broken by
CloudCracker in 2012 — avoid in new deployments.

---

### 1.4 EAP — Extensible Authentication Protocol

**EAP (Extensible Authentication Protocol)** is
NOT a single authentication protocol — it is a
**framework** that allows multiple authentication
methods to be negotiated and used over the same
transport (PPP, 802.1X, etc.).

| Property | Detail |
|----------|--------|
| **Standard** | RFC 3748 (2004) — updated by RFC 5247 |
| **Type** | Authentication framework — not a method itself |
| **Used in** | Wi-Fi (WPA2/WPA3 Enterprise), 802.1X, VPN |
| **Extensibility** | New EAP methods can be added without changing the framework |

**EAP message types:**

| Type | Description |
|------|-------------|
| **EAP Request** | Authenticator asks for identity or authentication |
| **EAP Response** | Peer responds to request |
| **EAP Success** | Authentication succeeded |
| **EAP Failure** | Authentication failed |

**EAP roles:**
```
Supplicant (client) ←→ Authenticator (switch/AP) ←→ Authentication Server (RADIUS)

Supplicant:    The device requesting network access
Authenticator: The network device controlling access
               (Wi-Fi AP, 802.1X switch)
Auth Server:   RADIUS server verifying credentials
```

> [!NOTE]
> EAP messages between the Supplicant and
> Authenticator are transported as
> **EAPOL (EAP over LAN)** — defined in
> IEEE 802.1X. The Authenticator relays EAP
> messages to the RADIUS server.

---

### 1.5 EAP Methods

EAP is a framework — these are the authentication
methods that run WITHIN the EAP framework:

| EAP Method | Security | Basis | Use Case |
|-----------|---------|-------|---------|
| **EAP-MD5** | ❌ Weak | MD5 hash | Legacy — no server auth |
| **EAP-TLS** | ✅ Strongest | TLS with client cert | Enterprise Wi-Fi, most secure |
| **EAP-TTLS** | ✅ Strong | TLS tunnel + inner auth | Enterprise — no client cert needed |
| **PEAP** | ✅ Strong | TLS tunnel + MSCHAPv2 inside | Most common enterprise Wi-Fi |
| **EAP-FAST** | ✅ Good | Cisco — PAC-based TLS | Cisco environments |
| **EAP-SIM** | ✅ Good | SIM card | Mobile carrier auth |
| **EAP-AKA** | ✅ Good | USIM card | 3G/4G/5G networks |
| **EAP-PWD** | ✅ Good | Password-based | RFC 5931 |

> [!IMPORTANT]
> **EAP-TLS is the gold standard** — it uses
> mutual TLS authentication (both client AND
> server present certificates). It is the most
> secure EAP method but requires a PKI
> infrastructure to issue client certificates
> to all devices.
>
> **PEAP (Protected EAP)** is the most widely
> deployed method — it creates a TLS tunnel
> for server authentication, then uses MSCHAPv2
> inside the tunnel for client authentication.
> No client certificates needed — easier to
> deploy.

---

### 1.6 802.1X — Port-Based Network Access Control

**IEEE 802.1X** is a network access control
standard that requires authentication before
granting access to a network port (wired or
wireless).

| Property | Detail |
|----------|--------|
| **Standard** | IEEE 802.1X (2001, updated 2010, 2020) |
| **Type** | Port-based Network Access Control (PNAC) |
| **Uses** | EAP as the authentication framework |
| **Transport for EAP** | EAPOL (EAP over LAN) |
| **Common deployment** | WPA2/WPA3 Enterprise Wi-Fi, 802.1X wired ports |

**802.1X roles:**

| Role | IEEE term | Description |
|------|-----------|-------------|
| **Supplicant** | Peer | The device wanting network access |
| **Authenticator** | Authenticator | Wi-Fi AP or network switch controlling port |
| **Authentication Server** | Authentication Server | RADIUS server with user database |

**802.1X flow:**
```
1. Device connects to Wi-Fi AP or Ethernet port

2. Port is in UNAUTHORIZED state —
   only EAPOL traffic allowed

3. Authenticator → Supplicant: EAP-Request Identity

4. Supplicant → Authenticator: EAP-Response Identity
   (username)

5. Authenticator → RADIUS Server: Access-Request
   (EAP payload forwarded via RADIUS)

6. RADIUS ↔ Supplicant: EAP method exchange
   (EAP-TLS handshake / PEAP / etc.)

7. RADIUS → Authenticator: Access-Accept or
   Access-Reject

8. If Accept → Port moves to AUTHORIZED state
   → Device gets network access ✅

9. If Reject → Port stays UNAUTHORIZED
   → No network access ❌
```

> [!NOTE]
> **WPA2-Enterprise vs WPA2-Personal:**
> WPA2-Personal (PSK) — one shared passphrase
> for all users — simpler but less secure.
> WPA2-Enterprise (802.1X/EAP) — each user has
> their own credentials — enterprise-grade,
> centrally managed, no shared secret.

---

### 1.7 LDAP Authentication

**LDAP (Lightweight Directory Access Protocol)**
is a protocol for accessing and maintaining
directory information — and is commonly used
as a backend authentication source.

| Property | Detail |
|----------|--------|
| **Standard** | RFC 4511 (2006) — LDAPv3 |
| **Port** | 389 (plaintext), 636 (LDAPS — over TLS) |
| **Based on** | X.500 Directory Services standard |
| **Used for** | User authentication, directory lookup, group membership |
| **Common implementations** | Microsoft Active Directory, OpenLDAP, Oracle LDAP |

**LDAP authentication process:**
```
Application needs to verify user credentials:

1. Application sends LDAP BIND request to
   LDAP server (Active Directory)
   BIND request = username (DN) + password

2. LDAP server verifies credentials

3. If valid: BIND succeeds → user authenticated
   If invalid: BIND fails → access denied

4. Application may then query user attributes
   (groups, email, permissions) from directory
```

**LDAP vs LDAPS:**
- **LDAP (port 389):** Credentials sent in
  cleartext — MUST be protected by TLS (STARTTLS)
  or upgraded to LDAPS
- **LDAPS (port 636):** LDAP over TLS —
  encrypted connection — recommended

**LDAP Directory Structure:**
```
dc=example,dc=com          ← Domain Component (root)
  └── ou=Users             ← Organizational Unit
        ├── cn=Alice        ← Common Name (user entry)
        └── cn=Bob
  └── ou=Groups
        └── cn=Admins
```

---

### 1.8 NTLM — NT LAN Manager

**NTLM (NT LAN Manager)** is Microsoft's legacy
authentication protocol — a challenge-response
mechanism based on NTLM hashes.

| Property | Detail |
|----------|--------|
| **Developer** | Microsoft |
| **Versions** | NTLMv1, NTLMv2 |
| **Current version** | NTLMv2 (more secure than v1) |
| **Used for** | Windows authentication when Kerberos is not available |
| **Status** | ⚠️ Legacy — use Kerberos instead where possible |
| **Security issues** | Pass-the-Hash, NTLM relay attacks |

**NTLM Authentication Flow:**
```
Client                          Server
  │                               │
  │── NEGOTIATE ─────────────────→│
  │                               │
  │←── CHALLENGE (8-byte nonce) ──│
  │                               │
  │ Client computes:               │
  │ Response = HMAC-MD5(NTLM_hash, challenge)
  │                               │
  │── AUTHENTICATE ──────────────→│
  │   (username + response)       │
  │                               │ Server verifies
  │←── Success or Failure ────────│
```

**NTLM vs Kerberos:**

| Property | NTLM | Kerberos |
|----------|------|---------|
| **Mutual auth** | ❌ No (v1) / ✅ NTLMv2 partial | ✅ Yes |
| **Password sent** | Hash-derived — not plaintext | Never |
| **Ticket-based** | ❌ No | ✅ Yes |
| **Domain controller contact** | Every authentication | Only for TGT |
| **Preferred** | Fallback only | Primary in Windows AD |

---

### 1.9 Protocol Comparison Table

| Protocol | Security | Password Sent | Challenge-Response | Modern? |
|----------|---------|--------------|-------------------|---------|
| **PAP** | ❌ Weakest | Plaintext | ❌ No | ❌ No |
| **CHAP** | ⚠️ Weak | Never (MD5 response) | ✅ Yes | ❌ No |
| **MS-CHAPv2** | ⚠️ Broken | Never | ✅ Yes | ❌ No |
| **EAP-MD5** | ❌ Weak | Never | ✅ Yes | ❌ No |
| **EAP-TLS** | ✅ Strongest | Never (cert-based) | ✅ Mutual TLS | ✅ Yes |
| **PEAP** | ✅ Strong | Never (tunneled) | ✅ Yes | ✅ Yes |
| **NTLM** | ⚠️ Legacy | Hash-derived | ✅ Yes | ❌ Avoid |
| **Kerberos** | ✅ Strong | Never | ✅ Ticket-based | ✅ Yes |
| **802.1X + EAP** | ✅ Strong | Depends on EAP method | ✅ Yes | ✅ Yes |

---

## 2. FIDO Authentication

### 2.1 What is FIDO?

**FIDO (Fast IDentity Online)** is a set of open
standards for strong authentication — designed
to replace passwords and weak MFA methods with
cryptography-based authentication that is:
- **Phishing-resistant** — credentials are
  bound to specific websites
- **Passwordless** — no shared secret ever
  leaves the user's device
- **Privacy-preserving** — no common identifier
  across services

> [!IMPORTANT]
> FIDO is the answer to both the password problem
> and the phishing problem simultaneously.
> Unlike OTP codes (which can be phished in
> real-time), FIDO credentials are mathematically
> bound to the exact website domain — a fake
> phishing site will NEVER get a valid FIDO
> response from the authenticator.

---

### 2.2 FIDO Alliance

| Property | Detail |
|----------|--------|
| **Organization** | FIDO Alliance |
| **Founded** | 2012 |
| **Type** | Open industry consortium |
| **Key members** | Google, Microsoft, Apple, Amazon, Intel, Qualcomm, PayPal, Yubico, VISA |
| **Specifications** | FIDO U2F, FIDO2 (WebAuthn + CTAP2) |
| **Website** | fidoalliance.org |
| **Mission** | Reduce reliance on passwords through open, scalable, interoperable authentication standards |

---

### 2.3 FIDO U2F — Universal 2nd Factor

**FIDO U2F** was the first FIDO standard —
designed as a simple hardware-based second factor
to add to existing username/password login.

| Property | Detail |
|----------|--------|
| **Full name** | Universal 2nd Factor |
| **Introduced** | 2014 by FIDO Alliance |
| **Successor** | FIDO2 (CTAP2 supersedes CTAP1/U2F) |
| **Hardware** | USB or NFC security keys (e.g., YubiKey) |
| **How used** | After username + password → insert key and press button |
| **Phishing-resistant** | ✅ Yes — origin bound |

**U2F flow:**
```
1. User enters username + password (first factor)
2. Server sends challenge + website origin
3. User taps hardware key button
4. Key computes ECDSA signature over
   (challenge + origin + counter)
5. Signature sent to server
6. Server verifies signature → grants access ✅
```

**Why U2F prevents phishing:**
The origin (website URL) is cryptographically
included in the signed data. A phishing site
at `g00gle.com` ≠ `google.com` — the signature
for `g00gle.com` will not be accepted by
`google.com`'s server.

---

### 2.4 FIDO2 — The Modern Standard

**FIDO2** is the evolution of FIDO — enabling
full **passwordless authentication** (not just
a second factor).

| Property | Detail |
|----------|--------|
| **Introduced** | 2018 by FIDO Alliance + W3C |
| **Components** | WebAuthn (W3C) + CTAP2 (FIDO Alliance) |
| **Backward compatible** | Supports U2F devices (CTAP1) |
| **Modes** | Second factor MFA OR full passwordless |
| **Phishing-resistant** | ✅ Yes — origin bound |
| **Key type** | Asymmetric (ECDSA P-256 or Ed25519) |

**FIDO2 = WebAuthn + CTAP2:**
```
Browser/App
  │
  │ WebAuthn API (W3C standard)
  ▼
Platform / Browser
  │
  │ CTAP2 (Client to Authenticator Protocol)
  ▼
Authenticator (hardware key, phone, laptop TPM)
  │
  → Private key stored in authenticator
  → Never exported — signing happens inside
```

---

### 2.5 WebAuthn — Web Authentication API

**WebAuthn (Web Authentication)** is the W3C and
IETF standard that defines the browser API for
FIDO2 authentication.

| Property | Detail |
|----------|--------|
| **Standard** | W3C WebAuthn Level 1 (2019), Level 2 (2021) |
| **Type** | Browser JavaScript API |
| **Supported by** | Chrome, Firefox, Safari, Edge (all major browsers) |
| **Supported OS** | Windows, macOS, Linux, iOS, Android |

**WebAuthn operations:**

| Operation | API Call | Purpose |
|-----------|---------|---------|
| **Registration** | `navigator.credentials.create()` | Create new credential — generates key pair |
| **Authentication** | `navigator.credentials.get()` | Authenticate — sign challenge with private key |

**Registration flow (creating a FIDO2 credential):**
```
1. Server generates random challenge
2. Server sends: challenge + relying party ID
   (RP ID = website domain)
3. Browser calls create() → activates authenticator
4. User verifies (tap key button / biometric)
5. Authenticator generates key pair:
   - Private key stored securely in authenticator
   - Public key returned to browser
6. Browser sends public key + attestation to server
7. Server stores public key
   → Registration complete ✅
```

**Authentication flow (using a FIDO2 credential):**
```
1. Server generates random challenge
2. Server sends: challenge + allowed credentials
3. Browser calls get() → activates authenticator
4. User verifies (tap button / biometric)
5. Authenticator signs: challenge + RP ID + counter
   using private key (ECDSA or Ed25519)
6. Browser sends signature to server
7. Server verifies signature using stored public key
   → Authentication complete ✅
```

---

### 2.6 CTAP2 — Client to Authenticator Protocol

**CTAP2 (Client to Authenticator Protocol 2)**
defines how the client platform (browser, OS)
communicates with the FIDO2 authenticator.

| Property | Detail |
|----------|--------|
| **Full name** | Client to Authenticator Protocol 2 |
| **Defined by** | FIDO Alliance |
| **Transport** | USB HID, NFC, Bluetooth LE |
| **Predecessor** | CTAP1 / U2F |
| **Key improvement** | Supports resident keys (stored on authenticator), passwordless, user verification |

**CTAP2 vs CTAP1:**

| Feature | CTAP1 (U2F) | CTAP2 (FIDO2) |
|---------|------------|--------------|
| Second factor only | ✅ | ✅ |
| Passwordless | ❌ | ✅ |
| Resident keys | ❌ | ✅ |
| PIN protection | ❌ | ✅ |
| Biometric | ❌ | ✅ |

---

### 2.7 FIDO2 Authentication Flow

**Complete FIDO2 passwordless login:**

```
REGISTRATION (first time):
─────────────────────────
User: "Register my security key for this site"

1. Site (Relying Party) → Browser:
   Challenge + RP_ID (domain) + User_ID

2. Browser → Authenticator (CTAP2):
   "Create credential for RP_ID"

3. User verification:
   Touch key button / fingerprint / PIN on key

4. Authenticator generates:
   Key pair (ECDSA P-256 or Ed25519)
   - Private key stored IN authenticator
   - Public key exported + credential ID

5. Authenticator → Browser → Site:
   Public key + Credential ID + Attestation

6. Site stores: User_ID → Public key mapping
   Registration complete ✅

─────────────────────────────────────────────
AUTHENTICATION (every subsequent login):
─────────────────────────
1. Site → Browser:
   Challenge + RP_ID + Allowed Credential IDs

2. Browser → Authenticator (CTAP2):
   "Sign challenge for RP_ID"

3. User verification:
   Touch key button / fingerprint / PIN

4. Authenticator:
   Finds private key for RP_ID
   Signs: Challenge + RP_ID + Counter
   Increments counter (replay prevention)

5. Authenticator → Browser → Site:
   Signature + Counter + Authenticator data

6. Site verifies:
   Signature valid? ✅
   Counter > last seen counter? ✅ (replay prevention)
   RP_ID matches? ✅

   → Login granted ✅
```

> [!IMPORTANT]
> **The counter** in FIDO2 is a monotonically
> increasing value — each successful authentication
> increments it. The server rejects any authentication
> where the counter is NOT greater than the last
> seen value. This prevents cloned credential attacks.

---

### 2.8 FIDO2 Authenticator Types

| Type | Description | Example | Portability |
|------|-------------|---------|------------|
| **Roaming authenticator** | External device — works across multiple devices | YubiKey (USB/NFC), Google Titan Key | ✅ Portable |
| **Platform authenticator** | Built into the device | Windows Hello (TPM), Face ID, Touch ID | ❌ Device-specific |
| **Hybrid authenticator** | Phone used as authenticator via Bluetooth | Passkeys on iPhone/Android | ✅ Portable (CTAP2 hybrid) |

**Roaming authenticator transports:**
- **USB HID** — YubiKey inserted into USB port
- **NFC** — Tap key on NFC reader or phone
- **Bluetooth LE (BLE)** — Wireless proximity

**Platform authenticators (Passkeys):**
- Windows Hello — TPM-backed FIDO2
- Apple Face ID / Touch ID — Secure Enclave
- Android fingerprint — StrongBox / TEE

---

### 2.9 Why FIDO2 is Phishing-Resistant

This is the most important property of FIDO2:

```
Standard OTP-based MFA (phishable):
  Attacker site: g00gle.com
  User visits phishing site
  Enters username + password → attacker gets them
  Attacker relays to real google.com → gets OTP challenge
  Attacker site asks user for OTP → user enters it
  Attacker relays OTP → logs into real google.com
  ❌ PHISHED — even with OTP 2FA

FIDO2 (phishing-resistant):
  Attacker site: g00gle.com (RP_ID = g00gle.com)
  User visits phishing site
  Browser calls get() → Authenticator checks RP_ID
  Authenticator has NO key for g00gle.com
  → Returns error → No credential found
  → Login fails at authenticator level
  ✅ CANNOT BE PHISHED — RP_ID mismatch
```

**The RP_ID is set during REGISTRATION:**
- Registration at `google.com` → key bound to `google.com`
- At `g00gle.com` → RP_ID = `g00gle.com`
- Authenticator has no key for `g00gle.com`
- Authentication fails automatically

---

### 2.10 FIDO2 vs TOTP vs SMS OTP

| Property | SMS OTP | TOTP (App) | FIDO2 |
|----------|---------|-----------|-------|
| **Phishing-resistant** | ❌ No | ❌ No | ✅ Yes |
| **SIM swap / SS7** | ❌ Vulnerable | ✅ Immune | ✅ Immune |
| **Real-time phishing** | ❌ Vulnerable | ❌ Vulnerable | ✅ Immune |
| **MFA fatigue** | ❌ Possible | ❌ Possible (relay) | ✅ Immune |
| **Hardware required** | Phone only | Phone only | Key or device |
| **Password still used?** | Usually yes | Usually yes | ❌ No (passwordless) |
| **Usability** | Easy | Easy | Easy (touch) |
| **Standard** | Carrier-dependent | RFC 6238 | FIDO2/WebAuthn |
| **Cost** | Free | Free | Key ~$25–$50 |

---

## 3. Zero Trust Architecture

### 3.1 What is Zero Trust?

**Zero Trust** is a security model and architecture
based on the principle:

> *"Never trust, always verify."*

Originally coined by **John Kindervag** at
Forrester Research in **2010**.

```
Traditional Model: "Trust but verify"
  → Trust everyone inside the network perimeter
  → Only verify outsiders

Zero Trust Model: "Never trust, always verify"
  → Trust NO ONE by default — insider or outsider
  → Verify EVERY request, EVERY user, EVERY device
     before granting ANY access
  → Assume breach is inevitable (or already happened)
```

> [!IMPORTANT]
> Zero Trust is NOT a product or technology you
> buy — it is a **security philosophy and
> architectural approach** that requires changes
> to processes, policies, and technology across
> the organization.
>
> Zero Trust fundamentally challenges the
> assumption that "inside = trusted."

---

### 3.2 The Traditional Perimeter Model —
Why It Failed

**The castle-and-moat model:**
```
OLD PERIMETER MODEL:
  Outside (Internet) = UNTRUSTED
  Firewall / VPN
  Inside (Corporate Network) = TRUSTED
  
  Once inside the perimeter:
    → Full access to internal resources
    → Assumed trusted — minimal verification
```

**Why it failed:**

| Failure Reason | Description |
|----------------|-------------|
| **Cloud adoption** | Resources moved outside the perimeter — no single boundary |
| **Remote work** | Users work from home, coffee shops, hotels |
| **Mobile devices** | Corporate data accessed from personal phones |
| **SaaS applications** | Apps like Salesforce, Office 365 live outside perimeter |
| **Insider threats** | Trusted users inside perimeter abuse access |
| **Lateral movement** | Attacker who breaches perimeter has wide access |
| **VPN limitations** | VPN gives excessive network access once connected |

> [!NOTE]
> **The 2013 Target breach** is a classic example
> of perimeter failure — attackers compromised
> a HVAC vendor's VPN credentials → gained access
> to Target's internal network (inside = trusted)
> → pivoted to payment card systems → stole
> 40 million credit card numbers.
>
> Zero Trust would have prevented lateral
> movement by requiring explicit verification
> for every resource access.

---

### 3.3 Zero Trust Core Principles

**The three core principles of Zero Trust
(from NIST SP 800-207):**

#### Principle 1 — Verify Explicitly
```
Every access request must be authenticated and
authorized based on ALL available data points:
  → Identity (who)
  → Location (where)
  → Device health (how)
  → Service/resource being accessed (what)
  → Data classification (sensitivity)
  → Behavioral anomalies (normal for this user?)
```

#### Principle 2 — Use Least Privilege Access
```
Grant ONLY the minimum access required for the
specific task — for the minimum time needed.
  → Just-In-Time (JIT) access provisioning
  → Just-Enough-Access (JEA) permissions
  → Session-limited access (expire after task)
  → No standing privileged access
```

#### Principle 3 — Assume Breach
```
Design and operate as if the network is already
compromised:
  → Microsegment networks — limit blast radius
  → Encrypt all data in transit and at rest
  → Monitor all traffic for anomalies
  → Minimize implicit trust zones
  → Incident response readiness always active
```

---

### 3.4 Zero Trust Components

A Zero Trust architecture includes these logical
components:

| Component | Abbreviation | Function |
|-----------|-------------|---------|
| **Policy Decision Point** | PDP | Evaluates access requests against policy — grants or denies |
| **Policy Enforcement Point** | PEP | Enforces the PDP's decision — allows or blocks traffic |
| **Policy Engine** | PE | Core decision logic — evaluates risk, identity, context |
| **Policy Administrator** | PA | Establishes/terminates communication paths |
| **Trust Algorithm** | TA | Calculates trust score for each access request |

**Data flows in Zero Trust:**
```
Subject (User/Device)
       │
       │ Access Request
       ▼
Policy Enforcement Point (PEP)
       │ Forward request for evaluation
       ▼
Policy Decision Point (PDP)
  ├── Policy Engine: Apply policy rules
  ├── Trust Algorithm: Calculate risk score
  ├── CDM System: Device health status
  ├── SIEM: Threat intelligence
  └── Identity Provider: Verify identity
       │
       │ Decision: Grant / Deny / Step-up auth
       ▼
Policy Enforcement Point (PEP)
       │ Enforce decision
       ▼
Enterprise Resource (Application / Data / Service)
```

---

### 3.5 NIST Zero Trust Architecture —
SP 800-207

**NIST SP 800-207** is the authoritative Zero Trust
Architecture document published by NIST in 2020.

| Property | Detail |
|----------|--------|
| **Publication** | NIST Special Publication 800-207 |
| **Title** | Zero Trust Architecture |
| **Published** | August 2020 |
| **Authors** | Scott Rose, Oliver Borchert, Stu Mitchell, Sean Connelly |

**NIST ZTA tenets (7 tenets from SP 800-207):**

1. All data sources and computing services are
   considered **resources**
2. All communication is secured **regardless of
   network location**
3. Access to individual enterprise resources is
   granted on a **per-session basis**
4. Access to resources is determined by **dynamic
   policy** including observable client identity,
   application, and requesting asset state
5. The enterprise monitors and measures the
   **integrity and security posture of all owned
   and associated assets**
6. All resource authentication and authorization
   are **dynamic and strictly enforced** before
   access is allowed
7. The enterprise collects as much information
   as possible about the **current state of
   assets, network infrastructure, and
   communications** and uses it to improve security

---

### 3.6 Zero Trust vs Traditional Perimeter
Security

| Dimension | Traditional Perimeter | Zero Trust |
|-----------|----------------------|-----------|
| **Trust model** | Trust inside, distrust outside | Never trust — verify everything |
| **Access control** | Location-based (inside network = trusted) | Identity + device + context based |
| **Network** | Flat — wide internal access once in | Microsegmented — limited blast radius |
| **VPN** | VPN grants full network access | VPN minimized / replaced by ZTNA |
| **User experience** | Smooth inside perimeter | More verification — adaptive friction |
| **Insider threat** | High risk — trusted by default | Mitigated — every action verified |
| **Cloud/SaaS** | Difficult to integrate | Natively suited |
| **Default stance** | Allow unless blocked (default allow) | Deny unless verified (default deny) |

---

### 3.7 Zero Trust Implementation Pillars

Modern Zero Trust frameworks (CISA, Microsoft,
Google BeyondCorp) define these implementation
pillars:

| Pillar | Description | Key Technologies |
|--------|-------------|----------------|
| **Identity** | Verify who is accessing | MFA, IAM, FIDO2, PAM |
| **Device** | Verify device health and compliance | MDM, EDR, device certificates |
| **Network** | Microsegment and monitor traffic | ZTNA, SD-WAN, firewall rules |
| **Application** | Secure app access and behavior | App proxy, WAF, API gateway |
| **Data** | Classify and protect data | DLP, encryption, data governance |
| **Visibility & Analytics** | Monitor everything | SIEM, UEBA, logging |
| **Automation & Orchestration** | Respond to threats automatically | SOAR, automated policy enforcement |

---

### 3.8 Zero Trust and PKI

PKI plays a critical role in Zero Trust:

| PKI Component | Zero Trust Role |
|--------------|----------------|
| **Device certificates** | Prove device identity — only certificate-bearing devices access resources |
| **User certificates** | Strong identity proof — beyond username/password |
| **mTLS (mutual TLS)** | Authenticate both client AND server in every connection |
| **Short-lived certificates** | Limit certificate validity — reduce standing trust |
| **Certificate transparency** | Detect unauthorized certificates in the environment |
| **OCSP/CRL** | Verify certificate validity at every access |

> [!NOTE]
> In a mature Zero Trust environment, every
> device has a machine certificate (issued by
> an internal CA) that proves it is a managed,
> compliant corporate device. Unmanaged devices
> are denied access regardless of valid user
> credentials — "right user on wrong device =
> deny."

---

## 4. 📌 Extra Notes

> [!NOTE]
> Everything in this section goes beyond the core
> syllabus but is directly MCQ-relevant.

---

### 4.1 EAP-TLS — The Gold Standard

> [!NOTE]
> **EAP-TLS** is considered the most secure EAP
> method — but also the most complex to deploy.

**Why EAP-TLS is strongest:**
```
EAP-TLS performs MUTUAL TLS authentication:
  → Server presents its certificate
     (client verifies server identity)
  → Client presents its certificate
     (server verifies client identity)
  → Both sides authenticated with PKI
  → No shared secrets — entirely certificate-based
  → Immune to credential stuffing (no passwords)
  → Immune to password spraying
```

**Why PEAP is more commonly deployed:**
```
PEAP:
  → Server presents certificate only
  → Client authenticates inside TLS tunnel
    using MSCHAPv2 (username + password)
  → No client certificate needed
  → Simpler to deploy (no PKI for client certs)
  → But vulnerable to MSCHAPv2 weaknesses
```

**Deployment comparison:**

| Property | EAP-TLS | PEAP-MSCHAPv2 |
|----------|---------|----------------|
| Client cert required | ✅ Yes | ❌ No |
| Server cert required | ✅ Yes | ✅ Yes |
| Password used | ❌ No | ✅ Yes (tunneled) |
| PKI required | ✅ Full PKI | Partial (server only) |
| Security | Highest | High |
| Deployment complexity | High | Medium |

---

### 4.2 RADIUS and 802.1X — How They Work
Together

> [!NOTE]

```
802.1X defines the port-based access control
mechanism and uses EAP as the authentication
framework.

RADIUS is the backend Authentication Server
protocol used to carry EAP messages from the
Authenticator to the Authentication Server.

Together:

Device ──EAPOL──→ Wi-Fi AP ──RADIUS──→ RADIUS Server
       (802.1X)            (EAP over  (Active Directory /
        EAP                 RADIUS)    LDAP / local user DB)

The Wi-Fi AP (Authenticator) never actually
processes the EAP authentication — it just
relays EAP messages between the device and
RADIUS using RADIUS Access-Request/Accept/Reject.
```

---

### 4.3 FIDO2 Resident Keys (Discoverable
Credentials)

> [!NOTE]
> **Resident keys** (also called Discoverable
> Credentials) are FIDO2 credentials stored
> ON the authenticator device — enabling
> completely passwordless login WITHOUT entering
> a username.

```
Without resident keys (server-side credentials):
  User enters username first
  → Server sends allowed credential IDs
  → Authenticator finds matching private key
  → Signs challenge

With resident keys (discoverable credentials):
  User presents authenticator (tap key)
  → Authenticator has stored:
    credential_id + public key RP mapping
    + user handle (user identifier)
  → Authenticator sends user identifier
    as part of the authentication assertion
  → Server identifies user from assertion
  → No username entered — fully passwordless ✅
```

**YubiKey 5 series** — stores up to 25 resident
keys. Platform authenticators (phone TPM) store
more.

---

### 4.4 Attestation in FIDO2

> [!NOTE]
> **Attestation** is FIDO2's mechanism for
> proving the TYPE and MODEL of the authenticator
> to the relying party.

```
Without attestation:
  Server knows a valid key pair was created
  But doesn't know if it's a genuine YubiKey,
  a software-only key, or a compromised device

With attestation:
  During registration, the authenticator includes:
    Attestation statement = signed proof of
    authenticator model using attestation key
  Server can verify: "This credential was created
  by a genuine, certified FIDO2 device"
```

**Attestation types:**

| Type | Description |
|------|-------------|
| **Basic attestation** | Authenticator signs with a batch attestation key (shared by all devices of same model) |
| **Self attestation** | Credential key used for attestation — no separate attestation key |
| **None attestation** | No attestation — server cannot verify authenticator type |
| **AAGUID** | Authenticator Attestation Globally Unique Identifier — identifies authenticator model |

---

### 4.5 Passkeys vs Hardware Security Keys

> [!NOTE]

| Property | Hardware Security Key (YubiKey) | Passkey (Phone/Platform) |
|----------|--------------------------------|--------------------------|
| **Storage** | Hardware key (tamper-resistant chip) | Device (Secure Enclave / TPM) |
| **Portability** | ✅ Physical — carry with you | ✅ Cloud-synced across devices |
| **Backup** | ❌ Only if explicitly duplicated | ✅ Auto-synced (iCloud, Google, etc.) |
| **Account recovery** | ❌ Loss = lockout | ✅ Recover via cloud account |
| **Security level** | Highest (no cloud sync) | High (synced = small risk) |
| **Loss scenario** | New key + manual re-enrollment | Recovery from cloud backup |
| **Recommended for** | High-risk accounts (admin, financial) | Everyday passwordless login |

> [!NOTE]
> **Cloud-synced passkeys** (Apple iCloud Keychain,
> Google Password Manager) are convenient but
> introduce cloud sync risk — if the cloud account
> is compromised, all passkeys may be exposed.
> Hardware keys (YubiKey) never sync to any cloud.

---

### 4.6 BeyondCorp — Google's Zero Trust
Implementation

> [!NOTE]
> **BeyondCorp** is Google's internal Zero Trust
> initiative — published in a series of
> academic papers starting 2014 — that moved
> away from VPN-based access to device and
> user identity-based access.

**Core BeyondCorp principle:**
```
Old Google: VPN → Internal network → Trust
BeyondCorp: No VPN. Every request evaluated.
  Access based on:
    → Device certificate (managed device?)
    → User identity + MFA
    → Device health (patched? compliant?)
    → Access policy for the resource
```

**BeyondCorp components:**
- **Device inventory** — all managed devices known
- **Device certificate** — each device has a cert
- **Access proxy** — all internal apps behind proxy
- **Identity-aware proxy** — IAP evaluates every request

BeyondCorp inspired Google Cloud's
**Identity-Aware Proxy (IAP)** — a commercial
product implementing Zero Trust for web apps.

---

### 4.7 Zero Trust Maturity Model — CISA

> [!NOTE]
> **CISA (Cybersecurity and Infrastructure
> Security Agency)** published the
> **Zero Trust Maturity Model** (2021, updated 2023)
> defining five maturity levels across
> five pillars.

**Five pillars:** Identity, Device, Network/
Environment, Application/Workload, Data

**Three maturity levels per pillar:**

| Level | Description |
|-------|-------------|
| **Traditional** | Manual configurations, siloed, minimal sharing |
| **Advanced** | Some automation, cross-pillar integration |
| **Optimal** | Fully automated, dynamic, continuous verification |

---

### 4.8 Microsegmentation

> [!NOTE]
> **Microsegmentation** is a network security
> technique that divides the network into small,
> isolated segments with strict access controls —
> limiting lateral movement if a breach occurs.

```
Traditional flat network:
  Server A ──────── Server B ──────── Server C
  (All servers can communicate freely)
  Attacker breaches Server A → can reach B and C

Microsegmented network:
  Server A ↔ Server B: Only port 443 allowed
  Server A ↔ Server C: No direct access
  Attacker breaches Server A → cannot reach C
  Blast radius is minimized ✅
```

**Microsegmentation implementations:**
- **Network-based** — VLANs, ACLs, firewall rules
- **Host-based** — OS firewall rules per host
- **SDN-based** — Software-defined networking policies
- **Service mesh** — mTLS between microservices
  (Istio, Linkerd)

---

### 4.9 Software-Defined Perimeter (SDP)

> [!NOTE]
> **SDP (Software-Defined Perimeter)** is a
> security architecture approach where the
> network perimeter is defined dynamically
> based on authenticated identity — rather
> than static network boundaries.

```
Traditional perimeter:
  Fixed firewall + VPN = perimeter

SDP:
  No network access until identity + device
  verified → then network dynamically "opened"
  for that specific user to specific resources
  → "Black cloud" — resources invisible until
    authenticated
```

**SDP vs VPN:**

| Property | VPN | SDP |
|----------|-----|-----|
| **Access granted** | To full network segment | To specific resources only |
| **Perimeter** | Static | Dynamic — per user/device |
| **Default** | Implicit network trust after VPN | Deny until verified |
| **Zero Trust aligned** | ❌ Poor | ✅ Good |

---

### 4.10 NTLM Attacks

> [!NOTE]

| Attack | Description | Mitigation |
|--------|-------------|-----------|
| **Pass-the-Hash (PtH)** | Steal NTLM hash → authenticate as user without knowing password | Credential Guard, Protected Users group |
| **NTLM Relay** | Intercept NTLM auth request → relay to another server | SMB signing mandatory, EPA |
| **Responder** | Tool that poisons LLMNR/NBNS to capture NTLM hashes | Disable LLMNR/NBNS |
| **NTLMv1 downgrade** | Force weaker NTLMv1 → crack with rainbow tables | Enforce NTLMv2 minimum |

> [!IMPORTANT]
> **NTLM should be disabled where Kerberos is
> available.** Microsoft is progressively
> deprecating NTLM — Windows 11 and Windows
> Server 2025 allow admins to disable NTLM
> entirely and rely on Kerberos.

---

### 4.11 Kerberos vs NTLM

> [!NOTE]

| Property | Kerberos | NTLM |
|----------|---------|------|
| **Mutual authentication** | ✅ Both sides verified | ❌ NTLMv1 only server verifies client |
| **Domain controller contact** | Once (TGT) | Every authentication |
| **Offline auth** | ✅ Cached TGT | ✅ Cached hash |
| **Delegation** | ✅ Supported | ❌ Limited |
| **Security** | ✅ Stronger | ⚠️ Weaker |
| **Used when** | Domain-joined, mutual DNS resolution | Workgroup, non-domain, fallback |

---

### 4.12 LDAP vs Active Directory

> [!NOTE]

| Property | LDAP | Active Directory |
|----------|------|----------------|
| **Type** | Protocol (RFC 4511) | Microsoft's directory service |
| **Relationship** | Active Directory implements LDAP | Uses LDAP as its access protocol |
| **Authentication** | Simple BIND (plaintext or TLS) | Kerberos (primary), NTLM, LDAP |
| **OS dependency** | Open standard — any OS | Windows Server |
| **Used for** | General directory queries | Full Windows domain authentication + GPO |

> Active Directory is essentially Microsoft's
> implementation of LDAP with additional
> services: Kerberos authentication, Group
> Policy, DNS, certificate services (ADCS).

---

### 4.13 PAM — Privileged Access Management

> [!NOTE]
> **PAM (Privileged Access Management)** is the
> set of technologies and processes for
> controlling, monitoring, and auditing access
> by privileged users (admins, root, service
> accounts).

**PAM principles align with Zero Trust:**
- **Just-in-Time (JIT) access:** Admin rights
  granted only when needed — auto-revoked after task
- **Just-enough access:** Minimal privileges
  for the specific task
- **Session recording:** All privileged sessions
  recorded for audit
- **Credential vaulting:** Admin passwords stored
  in vault — admins never see the actual password

**PAM tools:** CyberArk, HashiCorp Vault,
BeyondTrust, Delinea (formerly Thycotic)

---

## 5. Abbreviations Table

| Abbreviation | Full Form | One-Line Technical Meaning |
|---|---|---|
| PAP | Password Authentication Protocol | Legacy PPP auth — sends password in plaintext — RFC 1334 |
| CHAP | Challenge Handshake Authentication Protocol | Challenge-response auth — password never sent — MD5 based |
| EAP | Extensible Authentication Protocol | Authentication framework for multiple methods — RFC 3748 |
| PEAP | Protected EAP | EAP method — TLS tunnel + inner MSCHAPv2 — most common Wi-Fi enterprise |
| EAP-TLS | EAP Transport Layer Security | Strongest EAP — mutual TLS with client + server certificates |
| EAPOL | EAP over LAN | Transport for EAP between supplicant and authenticator (802.1X) |
| 802.1X | IEEE 802.1X | Port-based network access control standard |
| LDAP | Lightweight Directory Access Protocol | Directory access protocol — RFC 4511 — port 389/636 |
| LDAPS | LDAP over SSL/TLS | Encrypted LDAP — port 636 |
| NTLM | NT LAN Manager | Microsoft legacy challenge-response auth — replaced by Kerberos |
| FIDO | Fast IDentity Online | Open standards for strong phishing-resistant authentication |
| FIDO2 | FIDO2 | Modern FIDO standard — WebAuthn + CTAP2 — enables passwordless auth |
| U2F | Universal 2nd Factor | FIDO standard for hardware security key as second factor |
| WebAuthn | Web Authentication | W3C browser API standard for FIDO2 authentication |
| CTAP2 | Client to Authenticator Protocol 2 | FIDO Alliance protocol between platform and authenticator |
| RP | Relying Party | Website or application using FIDO2 for authentication |
| RP_ID | Relying Party ID | Website domain — cryptographically bound to FIDO2 credential |
| ZTA | Zero Trust Architecture | Security model — never trust, always verify — NIST SP 800-207 |
| PDP | Policy Decision Point | Zero Trust component that evaluates access requests |
| PEP | Policy Enforcement Point | Zero Trust component that enforces PDP decisions |
| ZTNA | Zero Trust Network Access | Technology replacing VPN with identity-based access |
| SDP | Software-Defined Perimeter | Dynamic network perimeter based on authenticated identity |
| PAM | Privileged Access Management | Controls and audits privileged user access |
| JIT | Just-In-Time | Access provisioned only when needed — auto-revoked after |
| mTLS | Mutual TLS | Both client and server authenticate with certificates in TLS |
| AAGUID | Authenticator Attestation Globally Unique Identifier | FIDO2 value identifying authenticator model |
| UEBA | User and Entity Behavior Analytics | Security analytics detecting anomalous user/device behavior |

---

## 6. Keywords + Concept Map

| Term | Definition | Connections | Use Cases |
|------|-----------|-------------|-----------|
| **PAP** | Sends password in plaintext | RFC 1334, PPP, avoid always | Legacy dial-up context only |
| **CHAP** | Challenge-response — MD5-based | RFC 1994, PPP, no password sent | Legacy VPN, PPP |
| **EAP** | Authentication framework — not a method | RFC 3748, 802.1X, RADIUS, Wi-Fi enterprise | Foundation for enterprise Wi-Fi auth |
| **EAP-TLS** | Strongest EAP — mutual TLS + client certs | PKI required, gold standard | High-security enterprise Wi-Fi |
| **PEAP** | TLS tunnel + MSCHAPv2 — no client cert | Most deployed enterprise Wi-Fi | Corporate Wi-Fi |
| **802.1X** | Port-based NAC — EAPOL + EAP + RADIUS | Supplicant, Authenticator, RADIUS | Enterprise network access control |
| **FIDO2** | Passwordless phishing-resistant auth | WebAuthn + CTAP2, RP_ID binding | Modern authentication standard |
| **WebAuthn** | W3C browser API for FIDO2 | create(), get(), challenge, RP_ID | Browser-based FIDO2 auth |
| **Phishing-resistant** | RP_ID binding prevents fake site auth | FIDO2, U2F, hardware keys | Anti-phishing authentication |
| **Zero Trust** | Never trust, always verify | NIST SP 800-207, PDP/PEP, least privilege | Modern enterprise security |
| **Microsegmentation** | Divide network — limit lateral movement | Zero Trust, blast radius, SDN | Network security architecture |
| **ZTNA** | Identity-based access replacing VPN | Zero Trust, SDP, BeyondCorp | Modern remote access |
| **PAM** | Control and audit privileged access | JIT, JEA, credential vaulting | Admin account security |
| **mTLS** | Both sides authenticate via certificates | Zero Trust, service mesh, PKI | Zero Trust inter-service auth |
| **Resident keys** | FIDO2 credentials stored on authenticator | Discoverable credentials, passwordless | Fully passwordless login |
| **NTLM** | Microsoft legacy challenge-response | Pass-the-Hash, relay attacks, Kerberos preferred | Windows legacy context |

---

## 7. Quick Reference Cheatsheet

### 🔸 Authentication Protocols — Security Summary

| Protocol | Sends Password? | Modern? | Use |
|----------|----------------|---------|-----|
| PAP | ✅ Plaintext | ❌ | Never — legacy only |
| CHAP | ❌ MD5 response | ❌ | Legacy PPP |
| EAP-MD5 | ❌ | ❌ | Avoid |
| EAP-TLS | ❌ Cert-based | ✅ | Gold standard |
| PEAP | ❌ Tunneled | ✅ | Common enterprise |
| NTLM | ❌ Hash-based | ❌ | Legacy Windows fallback |
| Kerberos | ❌ Never | ✅ | Windows AD standard |

---

### 🔸 FIDO2 Key Facts

| Property | Value |
|----------|-------|
| Full standard | WebAuthn (W3C) + CTAP2 (FIDO Alliance) |
| Year introduced | 2018 |
| Key security property | Phishing-resistant — RP_ID bound to domain |
| Private key | Never leaves authenticator |
| Phishing-resistant because | RP_ID mismatch → authenticator fails |
| Types | Roaming (YubiKey), Platform (Windows Hello), Hybrid (Passkey) |

---

### 🔸 802.1X Roles

| Role | IEEE Term | Example |
|------|-----------|---------|
| Device requesting access | Supplicant | Laptop, phone |
| Network device controlling port | Authenticator | Wi-Fi AP, switch |
| Server verifying credentials | Auth Server | RADIUS + AD |

---

### 🔸 Zero Trust Core Principles

```
1. Verify Explicitly — use all available signals
2. Use Least Privilege — JIT, JEA
3. Assume Breach — microsegment, monitor, encrypt
```

---

### 🔸 Zero Trust vs Perimeter

| | Perimeter | Zero Trust |
|---|-----------|-----------|
| Default | Allow inside | Deny until verified |
| Trust | Location-based | Identity + device + context |
| Network | Flat | Microsegmented |
| VPN | Full network access | Specific resource access |

---

### 🔸 FIDO2 Authentication Flow Summary

```
Registration:
  Browser → create() → Authenticator generates key pair
  Private key stays in authenticator
  Public key + credential ID → Server stores

Authentication:
  Server → Challenge → Browser → get() → Authenticator signs
  Signature + counter → Server verifies → Access granted
```

---

### 🔸 NIST SP 800-207 — Key Reference

| Property | Value |
|----------|-------|
| Title | Zero Trust Architecture |
| Published | August 2020 |
| Organization | NIST |
| Core tenets | 7 |
| Three principles | Verify Explicitly, Least Privilege, Assume Breach |

---

## 8. Session Revision Snapshot

### ⚡ TL;DR — 5 Bullets

- ✅ Authentication protocols — PAP (plaintext
  password, worst, RFC 1334), CHAP (challenge-
  response MD5, no password sent, RFC 1994), EAP
  (framework for multiple methods — EAP-TLS is
  strongest — requires client cert; PEAP is most
  deployed — no client cert); 802.1X = port-based
  NAC using EAP over RADIUS
- ✅ FIDO2 (2018) = WebAuthn (W3C browser API) +
  CTAP2 (FIDO Alliance authenticator protocol) —
  phishing-resistant because credentials are bound
  to RP_ID (exact domain) — fake site has different
  RP_ID — authenticator finds no matching key —
  authentication fails automatically
- ✅ FIDO2 private key NEVER leaves the
  authenticator — registration creates key pair on
  device, public key sent to server — authentication
  signs a challenge with private key inside device —
  this is why FIDO2 is unphishable and passwordless
- ✅ Zero Trust = "Never trust, always verify" —
  coined by John Kindervag (Forrester, 2010) —
  NIST SP 800-207 (August 2020) is the authoritative
  document — three principles: Verify Explicitly,
  Least Privilege Access, Assume Breach — PDP makes
  decisions, PEP enforces them
- ✅ Zero Trust vs Perimeter: Perimeter model
  trusts location (inside = trusted); Zero Trust
  trusts nothing by default — every request verified
  by identity + device + context — microsegmentation
  limits blast radius — ZTNA replaces VPN — assume
  attackers are already inside

---

### 🎯 MCQ-Likely Concepts — Everything Examiners Love

| Concept | Why It's Tricky |
|---------|----------------|
| PAP sends password in PLAINTEXT | Worst protocol — students may think it uses hashing |
| CHAP uses MD5 — but password never sent | Better than PAP but still weak (MD5) |
| EAP is a FRAMEWORK not a protocol | Students treat it as an authentication method |
| EAP-TLS requires CLIENT certificates | The distinguishing feature of EAP-TLS vs PEAP |
| PEAP is most commonly deployed | EAP-TLS is strongest but PEAP is most common |
| 802.1X = port-based NAC (PNAC) | Specific IEEE standard name |
| EAPOL = EAP over LAN (used in 802.1X) | Specific transport name |
| FIDO2 = WebAuthn + CTAP2 | Both components needed together |
| Phishing-resistant because RP_ID is bound | Mechanism must be understood, not just stated |
| FIDO2 private key never leaves authenticator | Key security property |
| FIDO U2F was 2014; FIDO2 was 2018 | Year distinction sometimes tested |
| Zero Trust coined by John Kindervag (Forrester, 2010) | Author and year |
| NIST SP 800-207 = ZTA document (August 2020) | Document number and year |
| PDP = decides; PEP = enforces | ZTA component roles |
| Three ZT principles — Verify Explicitly, Least Privilege, Assume Breach | All three must be known |
| Microsegmentation limits lateral movement | Specific security benefit |
| NTLM = Pass-the-Hash vulnerability | Most notable NTLM attack |
| LDAPS uses port 636 (LDAP = 389) | Port numbers tested |
| Kerberos preferred over NTLM in Windows AD | Kerberos is primary; NTLM is fallback |
| 802.1X roles: Supplicant, Authenticator, Auth Server | Three specific role names |

---

<details>
<summary>🔬 Lab Content (Session 12 — No Lab Assigned)</summary>

No lab is assigned for Session 12 in the syllabus.

Session 12 theory concepts (FIDO2, Zero Trust)
are primarily conceptual and policy-level —
they connect to the following labs:

**FIDO2 practical demonstration:**
- No dedicated lab, but FIDO2 can be observed by
  registering a security key (YubiKey or phone
  passkey) on any FIDO2-capable website
  (GitHub, Google, Microsoft) — observe the
  WebAuthn API calls in browser developer tools

**Zero Trust and PKI connection:**
The OpenSSL PKI hierarchy lab (Session 13) directly
demonstrates a core Zero Trust component:
- Device/server certificates = identity proof
  for Zero Trust access decisions
- mTLS between services = Zero Trust inter-service
  authentication

**Authentication protocol observation:**
- 802.1X + EAP is observable by connecting to
  a WPA2-Enterprise network and monitoring
  the EAPOL handshake in Wireshark

Session 12 concepts connect directly to:
- **Session 13** — TLS/SSL which is the transport
  for WebAuthn, OIDC, LDAPS, and mTLS (Zero Trust)
- **Session 14** — LDAP/AD which is the backend
  for 802.1X/EAP enterprise authentication

</details>

---