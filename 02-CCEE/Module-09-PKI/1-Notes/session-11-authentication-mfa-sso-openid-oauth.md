# Session 11 — Strong Authentication, MFA, SSO,
OpenID, OAuth & Graphical Passwords

## 📑 Table of Contents

- [1. Strong Authentication](#1-strong-authentication)
  - [1.1 What is Authentication?](#11-what-is-authentication)
  - [1.2 Authentication Factors](#12-authentication-factors)
  - [1.3 Strong Authentication — Definition](#13-strong-authentication--definition)
  - [1.4 Authentication vs Authorization vs
    Accounting](#14-authentication-vs-authorization-vs-accounting)
- [2. Single Factor and Multi-Factor
  Authentication](#2-single-factor-and-multi-factor-authentication)
  - [2.1 Single Factor Authentication (SFA)](#21-single-factor-authentication-sfa)
  - [2.2 Two-Factor Authentication (2FA)](#22-two-factor-authentication-2fa)
  - [2.3 Multi-Factor Authentication (MFA)](#23-multi-factor-authentication-mfa)
  - [2.4 MFA Methods — OTP, Push, TOTP,
    HOTP](#24-mfa-methods--otp-push-totp-hotp)
  - [2.5 Adaptive Authentication](#25-adaptive-authentication)
  - [2.6 MFA Attack Vectors](#26-mfa-attack-vectors)
- [3. Single Sign-On (SSO)](#3-single-sign-on-sso)
  - [3.1 What is SSO?](#31-what-is-sso)
  - [3.2 How SSO Works — Core Concept](#32-how-sso-works--core-concept)
  - [3.3 SSO Benefits and Risks](#33-sso-benefits-and-risks)
  - [3.4 SSO Protocols — Overview](#34-sso-protocols--overview)
  - [3.5 Kerberos — SSO for Enterprise](#35-kerberos--sso-for-enterprise)
  - [3.6 SAML — SSO for Web Applications](#36-saml--sso-for-web-applications)
- [4. OpenID and OAuth](#4-openid-and-oauth)
  - [4.1 The Problem They Solve](#41-the-problem-they-solve)
  - [4.2 OAuth 2.0 — Authorization
    Framework](#42-oauth-20--authorization-framework)
  - [4.3 OAuth 2.0 — Roles](#43-oauth-20--roles)
  - [4.4 OAuth 2.0 — Authorization Code
    Flow](#44-oauth-20--authorization-code-flow)
  - [4.5 OAuth 2.0 Grant Types](#45-oauth-20-grant-types)
  - [4.6 OpenID Connect (OIDC)](#46-openid-connect-oidc)
  - [4.7 OAuth vs OpenID Connect —
    Core Difference](#47-oauth-vs-openid-connect--core-difference)
  - [4.8 OAuth vs Traditional Authentication](#48-oauth-vs-traditional-authentication)
- [5. Graphical Passwords](#5-graphical-passwords)
  - [5.1 What are Graphical Passwords?](#51-what-are-graphical-passwords)
  - [5.2 Categories of Graphical Passwords](#52-categories-of-graphical-passwords)
  - [5.3 Advantages and Disadvantages](#53-advantages-and-disadvantages)
- [6. 📌 Extra Notes](#6--extra-notes)
  - [6.1 AAA Framework — Authentication,
    Authorization, Accounting](#61-aaa-framework--authentication-authorization-accounting)
  - [6.2 TOTP vs HOTP — Deep Dive](#62-totp-vs-hotp--deep-dive)
  - [6.3 FIDO2 / WebAuthn — Preview](#63-fido2--webauthn--preview)
  - [6.4 Passkeys — Passwordless
    Authentication](#64-passkeys--passwordless-authentication)
  - [6.5 OAuth 2.0 Security Issues](#65-oauth-20-security-issues)
  - [6.6 JWT — JSON Web Token](#66-jwt--json-web-token)
  - [6.7 SAML vs OAuth vs OpenID Connect —
    Full Comparison](#67-saml-vs-oauth-vs-openid-connect--full-comparison)
  - [6.8 Kerberos Deep Dive — Tickets and
    KDC](#68-kerberos-deep-dive--tickets-and-kdc)
  - [6.9 MFA Fatigue Attack](#69-mfa-fatigue-attack)
  - [6.10 Social Login — OAuth in Practice](#610-social-login--oauth-in-practice)
  - [6.11 Step-Up Authentication](#611-step-up-authentication)
  - [6.12 Password Managers and Strong
    Authentication](#612-password-managers-and-strong-authentication)
- [7. Abbreviations Table](#7-abbreviations-table)
- [8. Keywords + Concept Map](#8-keywords--concept-map)
- [9. Quick Reference Cheatsheet](#9-quick-reference-cheatsheet)
- [10. Session Revision Snapshot](#10-session-revision-snapshot)

---

## 1. Strong Authentication

### 1.1 What is Authentication?

**Authentication** is the process of verifying the
identity of a user, device, or system — confirming
that they are who or what they claim to be.

```
Identity claim:  "I am Alice"
Authentication:  "Prove it"
Verification:    Alice provides evidence → system confirms
```

Authentication answers the question:
**"Are you really who you claim to be?"**

> [!IMPORTANT]
> Authentication is different from:
> - **Identification** — stating who you are
>   (no verification)
> - **Authorization** — what you are allowed to
>   do (after authentication)
> - **Accountability** — tracking what you did
>   (after authorization)
>
> All three are distinct steps in access control.

---

### 1.2 Authentication Factors

Authentication is based on one or more of
these five factor categories:

| Factor | Type | Description | Examples |
|--------|------|-------------|---------|
| **Something you KNOW** | Knowledge | Secret information only the user should know | Password, PIN, passphrase, security question |
| **Something you HAVE** | Possession | A physical or digital token | USB token, smart card, OTP app, phone, bank card |
| **Something you ARE** | Inherence | Physical or behavioral characteristic unique to the user | Fingerprint, iris, face, voice, typing rhythm |
| **Somewhere you ARE** | Location | Geographic location or network context | GPS location, IP address range, known Wi-Fi |
| **Something you DO** | Behavior | Behavioral patterns | Typing cadence, mouse movement, gait |

> [!NOTE]
> Traditional security mentions 3 factors
> (know, have, are). Modern authentication adds
> location and behavior (making 5 total).
> Exams primarily test the original 3.

---

### 1.3 Strong Authentication — Definition

**Strong authentication** requires using
MULTIPLE factors from DIFFERENT categories —
so that compromising one factor is not sufficient
to gain access.

```
Weak: Password alone (single factor — something you know)

Strong: Password + OTP from phone
        (something you know + something you have)

Stronger: Password + Fingerprint + Location check
          (know + are + somewhere you are)
```

> [!IMPORTANT]
> **Two factors from the SAME category
> is NOT multi-factor authentication.**
>
> Example: Password + Security Question =
> BOTH are "something you know" =
> This is still SINGLE-FACTOR authentication
> (just two instances of the same factor type).
>
> True MFA requires factors from DIFFERENT
> categories.

---

### 1.4 Authentication vs Authorization vs Accounting

These three are collectively known as **AAA**:

| Concept | Question | Example |
|---------|---------|---------|
| **Authentication (AuthN)** | Who are you? | User logs in with username + password + OTP |
| **Authorization (AuthZ)** | What can you do? | User can read but not write files |
| **Accounting** | What did you do? | System logs every file access by the user |

> [!NOTE]
> In security architecture:
> - **AuthN** comes first — identity verified
> - **AuthZ** comes second — permissions applied
> - **Accounting** runs throughout — actions logged
>
> You cannot authorize without first authenticating.
> You should always account regardless.

---

## 2. Single Factor and Multi-Factor Authentication

### 2.1 Single Factor Authentication (SFA)

**SFA** uses only ONE factor from ONE category
to authenticate a user.

| Factor Used | Example |
|-------------|---------|
| Something you know | Password-only login |
| Something you have | Smart card only (no PIN) |
| Something you are | Fingerprint only |

**Weaknesses of SFA:**
- Password can be guessed, stolen, phished, or
  brute-forced
- Single point of failure — one compromised
  factor = full access lost
- Credentials stolen from one breach reused
  across other sites (credential stuffing)

---

### 2.2 Two-Factor Authentication (2FA)

**2FA** requires exactly TWO factors from
TWO DIFFERENT categories.

**Common 2FA combinations:**

| Factor 1 | Factor 2 | Example |
|----------|----------|---------|
| Password (know) | OTP on phone (have) | Gmail, banking |
| Password (know) | Fingerprint (are) | Windows Hello + password |
| Smart card (have) | PIN (know) | Government ID cards |
| Password (know) | Hardware key (have) | YubiKey + password |

> [!NOTE]
> 2FA is the most widely deployed form of
> strong authentication on the internet today.
> Even adding SMS OTP to a password login
> provides significant security improvement
> over password-only — despite SMS OTP being
> considered weak 2FA (SIM swapping attacks).

---

### 2.3 Multi-Factor Authentication (MFA)

**MFA** uses TWO OR MORE factors from
DIFFERENT categories. 2FA is a subset of MFA.

```
MFA ⊃ 2FA

All 2FA is MFA.
Not all MFA is 2FA (MFA can use 3+ factors).
```

**MFA in high-security contexts:**
- Banking: Password + OTP + Device recognition
- Government: Smart card + PIN + Biometric
- Privileged access: Password + Hardware token
  + IP whitelist (location)

**Why MFA matters statistically:**
```
Microsoft research (2019):
  MFA blocks 99.9% of automated account
  compromise attacks
  → Even weak MFA (SMS OTP) is dramatically
    better than password alone
```

---

### 2.4 MFA Methods — OTP, Push, TOTP, HOTP

**OTP (One-Time Password):**
A password valid for only ONE login attempt or
for a short time period. Cannot be reused.

**Types of OTP:**

| Type | Full Name | Algorithm | Valid Period | Example |
|------|-----------|-----------|-------------|---------|
| **TOTP** | Time-based OTP | HMAC-SHA1 + Unix timestamp | 30 seconds | Google Authenticator |
| **HOTP** | HMAC-based OTP | HMAC-SHA1 + counter | Until used | Hardware tokens |
| **SMS OTP** | SMS delivered OTP | Random | Short window | Bank SMS codes |
| **Push notification** | In-app approval | — | Short window | Duo Security, Microsoft Authenticator |

**TOTP (Time-based OTP):**
```
TOTP = HOTP(Key, T)
Where T = floor(Current Unix Time / Time Step)
Default time step = 30 seconds

Every 30 seconds, a new 6-digit code is generated.
Both the authenticator app AND the server
compute the same TOTP independently.
```

**HOTP (HMAC-based OTP):**
```
HOTP(Key, Counter) = Truncate(HMAC-SHA1(Key, Counter))
Counter increments by 1 each time a new OTP is used.
```

**Push notification 2FA:**
```
User logs in with password
→ Server sends push notification to user's
  registered mobile app
→ User approves or denies the request in the app
→ If approved → server grants access
```

> [!NOTE]
> **TOTP is defined in RFC 6238**
> **HOTP is defined in RFC 4226**
> Both are based on HMAC-SHA1 and are part of
> the **OATH (Initiative for Open Authentication)**
> framework — an industry group for open MFA
> standards.

---

### 2.5 Adaptive Authentication

**Adaptive authentication** (also called
**risk-based authentication**) dynamically
adjusts the authentication requirements based
on context — requiring stronger authentication
when risk is higher.

**Risk signals used:**

| Signal | Example |
|--------|---------|
| **Location** | Login from a new country |
| **Device** | Unrecognized device / new browser |
| **IP address** | Known malicious IP or VPN |
| **Time of day** | Login at 3 AM when normally 9–5 |
| **Behavior** | Typing pattern mismatch |
| **Previous failed attempts** | 3 failed logins before success |
| **Network** | Public Wi-Fi vs corporate network |

**Adaptive authentication flow:**
```
Low risk (known device, normal location, normal time):
  → Password only (no MFA prompt)

Medium risk (new device OR unusual time):
  → Password + OTP required

High risk (new country AND new device AND unusual time):
  → Password + OTP + admin review
  OR
  → Access denied — contact support
```

---

### 2.6 MFA Attack Vectors

| Attack | Description | Mitigation |
|--------|-------------|-----------|
| **SIM swapping** | Attacker convinces telco to transfer victim's SIM to attacker's device — receives SMS OTP | Use TOTP app instead of SMS |
| **SS7 attacks** | Exploiting Signaling System 7 network weaknesses to intercept SMS | Use TOTP/FIDO2 instead of SMS |
| **Real-time phishing** | Attacker relays OTP entered by victim in real-time to legitimate site (man-in-the-browser) | Use hardware keys (phishing-resistant) |
| **MFA fatigue / push bombing** | Attacker sends dozens of MFA push requests hoping victim approves one | Number matching, context-aware push |
| **Malware on authenticator device** | If the OTP app device is compromised | Hardware security keys |
| **Account recovery abuse** | Attacker uses account recovery to bypass MFA | Secure recovery process |

> [!IMPORTANT]
> **SMS OTP weaknesses:**
> SMS-based OTP is considered the weakest
> form of 2FA due to SIM swapping and SS7
> vulnerabilities. However, it is still much
> better than no MFA at all.
>
> **Phishing-resistant MFA** — FIDO2/WebAuthn
> hardware keys (YubiKey) are bound to the
> specific domain — they will not work on
> phishing sites even if victim is tricked.

---

## 3. Single Sign-On (SSO)

### 3.1 What is SSO?

**Single Sign-On (SSO)** is an authentication
scheme that allows a user to authenticate ONCE
and gain access to MULTIPLE applications or
services without re-authenticating for each one.

```
Without SSO:
  User logs into email → authenticates
  User opens project tool → authenticates again
  User opens HR portal → authenticates again
  User opens CRM → authenticates again
  → 4 separate logins — password fatigue

With SSO:
  User logs in ONCE to the organization's
  identity provider
  → Automatically granted access to email,
    project tool, HR portal, CRM
  → One login → all services ✅
```

> [!IMPORTANT]
> SSO does NOT mean "one password for all
> systems." It means ONE AUTHENTICATION SESSION
> — after which all connected services trust
> the user's identity without re-authentication.

---

### 3.2 How SSO Works — Core Concept

**SSO Architecture involves three entities:**

| Entity | Role |
|--------|------|
| **Identity Provider (IdP)** | Authenticates the user — issues proof of authentication (token/assertion) |
| **Service Provider (SP)** | The application the user wants to access — trusts the IdP |
| **User/Principal** | The person authenticating |

**Basic SSO flow:**
```
Step 1: User tries to access Service Provider (SP)
        (e.g., company email)

Step 2: SP redirects user to Identity Provider (IdP)
        (e.g., company's Active Directory / Okta)

Step 3: User authenticates with IdP
        (username + password + MFA)

Step 4: IdP issues authentication token/assertion
        (proves: "Alice authenticated at 10:30 AM")

Step 5: User is redirected back to SP with token

Step 6: SP validates token (via IdP's signature)
        → Grants access without asking for
          credentials again ✅

Step 7: User accesses another SP
        → SP redirects to IdP
        → IdP finds existing session → issues token
        → User gets access WITHOUT re-authenticating
```

---

### 3.3 SSO Benefits and Risks

**Benefits:**

| Benefit | Description |
|---------|-------------|
| **User convenience** | One login for all services — less password fatigue |
| **Reduced password reuse** | Users only need to remember one strong password |
| **Centralized security** | IT manages authentication centrally — easier to enforce policies |
| **Faster access** | No repeated login prompts throughout the day |
| **Simplified provisioning** | Create/disable accounts in one place |
| **Audit trail** | All authentication events logged centrally |

**Risks:**

| Risk | Description |
|------|-------------|
| **Single point of failure** | If IdP goes down → ALL services inaccessible |
| **Single point of compromise** | If IdP credentials are stolen → ALL connected services compromised |
| **Session hijacking** | SSO token stolen = access to all services |
| **Complex setup** | Integration between IdP and all SPs requires careful configuration |

> [!IMPORTANT]
> **The SSO security dilemma:**
> SSO improves usability and can improve security
> (strong central auth + MFA enforced once).
> But it creates a high-value target — the IdP.
>
> Best practice: Protect the IdP with strong MFA
> and monitor it closely — because compromise
> of the IdP = compromise of everything connected.

---

### 3.4 SSO Protocols — Overview

| Protocol | Used For | Era |
|----------|---------|-----|
| **Kerberos** | Enterprise networks (Windows Active Directory) | 1980s–present |
| **SAML 2.0** | Web-based SSO between enterprises | 2005–present |
| **OAuth 2.0** | Authorization delegation on the web | 2012–present |
| **OpenID Connect (OIDC)** | Web authentication built on OAuth 2.0 | 2014–present |
| **CAS (Central Authentication Service)** | University/campus SSO | 2000s–present |

---

### 3.5 Kerberos — SSO for Enterprise

**Kerberos** is a network authentication protocol
that provides SSO for enterprise environments —
the foundation of Windows Active Directory
authentication.

| Property | Detail |
|----------|--------|
| **Developed by** | MIT (Massachusetts Institute of Technology) |
| **Year** | 1980s — Kerberos v5 (RFC 4120, 2005) |
| **Named after** | Cerberus — the three-headed dog guarding Hades |
| **Used in** | Windows Active Directory, Linux (MIT Kerberos) |
| **Key feature** | Mutual authentication — both client and server verify each other |
| **Ticket-based** | Uses tickets (not passwords) for service access |
| **Symmetric key** | Uses AES (symmetric encryption) — no asymmetric crypto |

**Kerberos components:**

| Component | Description |
|-----------|-------------|
| **KDC (Key Distribution Center)** | Central trusted server — AS + TGS |
| **AS (Authentication Server)** | Verifies user identity, issues TGT |
| **TGS (Ticket Granting Server)** | Issues service tickets based on TGT |
| **TGT (Ticket Granting Ticket)** | Proof of authentication — used to request service tickets |
| **Service Ticket (ST)** | Allows access to a specific service |
| **Realm** | Administrative domain (equivalent to a domain) |

**Kerberos authentication flow:**
```
Step 1: Client → AS: "I am Alice, I want to
                     authenticate" (+ timestamp)

Step 2: AS → Client: Encrypted TGT
        (encrypted with TGS's secret key)
        + Session key (encrypted with Alice's key)

Step 3: Client decrypts session key using
        Alice's password-derived key

Step 4: Client → TGS: TGT + request for
                      service ticket for Server X

Step 5: TGS validates TGT → issues Service Ticket
        for Server X (encrypted with Server X's key)

Step 6: Client → Server X: Service Ticket

Step 7: Server X decrypts ticket → verifies
        Alice's identity → grants access ✅
```

> [!NOTE]
> **Key Kerberos security properties:**
> - Passwords are NEVER sent over the network
>   (only ticket-based exchanges)
> - Timestamps prevent replay attacks
>   (tickets valid for ~10 hours by default)
> - Requires accurate clock synchronization
>   (clocks must be within 5 minutes of KDC)
> - AES-256 is the current encryption standard
>   for Kerberos

---

### 3.6 SAML — SSO for Web Applications

**SAML (Security Assertion Markup Language)** is
an XML-based standard for exchanging authentication
and authorization data between an Identity Provider
and a Service Provider.

| Property | Detail |
|----------|--------|
| **Full name** | Security Assertion Markup Language |
| **Current version** | SAML 2.0 |
| **Developed by** | OASIS (Organization for the Advancement of Structured Information Standards) |
| **Published** | SAML 2.0 — March 2005 |
| **Format** | XML-based |
| **Used for** | Web-based enterprise SSO |
| **Common use** | Corporate SSO — logging into Office 365 with corporate credentials |

**SAML flow (SP-initiated):**
```
1. User → SP (tries to access application)
2. SP → User: SAML AuthnRequest (XML redirect to IdP)
3. User → IdP: Credentials (username + password + MFA)
4. IdP: Authenticates user — creates SAML Assertion
   (XML document: "Alice authenticated at 10:30")
5. IdP → User → SP: SAML Response (with signed Assertion)
6. SP: Validates IdP's signature on the Assertion
7. SP: Grants access ✅
```

**SAML Assertion types:**

| Type | Description |
|------|-------------|
| **Authentication Assertion** | States the user authenticated, when, and by what method |
| **Attribute Assertion** | Carries user attributes (name, email, role, group) |
| **Authorization Decision Assertion** | States what the user is permitted to do |

---

## 4. OpenID and OAuth

### 4.1 The Problem They Solve

**The credential sharing problem:**
```
Scenario: A photo printing app wants access
          to your Google Photos.

Old approach: Give the photo app your
              Google username and password
              → App has full Google account access
              → Cannot limit what app can do
              → Cannot revoke without changing password
              → Dangerous

OAuth approach: Google asks you what to authorize
                "Allow photo printing app to access
                 Google Photos only?"
                You click YES
                → App gets a limited access token
                → Only for Google Photos
                → Revocable without changing password
                → Google credentials never shared ✅
```

---

### 4.2 OAuth 2.0 — Authorization Framework

**OAuth 2.0** is an **authorization framework**
(NOT an authentication protocol) that allows
a user to grant third-party applications LIMITED
access to their resources on another service —
WITHOUT sharing their credentials.

| Property | Detail |
|----------|--------|
| **Full name** | Open Authorization 2.0 |
| **Type** | Authorization framework |
| **Standard** | RFC 6749 (2012) |
| **Replaces** | OAuth 1.0 (RFC 5849) |
| **What it enables** | Delegated authorization — granting limited resource access |
| **What it is NOT** | An authentication protocol — cannot prove WHO the user is |

> [!IMPORTANT]
> **OAuth 2.0 is about AUTHORIZATION —
> not AUTHENTICATION.**
>
> OAuth answers: "What can this application do
> on your behalf?" — NOT "Who are you?"
>
> If you need to know WHO the user is
> (authentication), use **OpenID Connect**
> (which is built on top of OAuth 2.0).

---

### 4.3 OAuth 2.0 — Roles

| Role | Description | Example |
|------|-------------|---------|
| **Resource Owner** | The user who owns the protected resource | You (the user) |
| **Client** | The application requesting access | Photo printing app |
| **Authorization Server** | Issues access tokens after user consent | Google's OAuth server |
| **Resource Server** | Hosts the protected resources | Google Photos API |

```
Resource Owner (you) grants consent to Client (app)
Client receives token from Authorization Server (Google)
Client uses token to access Resource Server (Photos API)
```

---

### 4.4 OAuth 2.0 — Authorization Code Flow

The most secure and widely used OAuth 2.0 flow:

```
Step 1: User → Client App: "Connect with Google"

Step 2: Client → Authorization Server:
        Authorization Request
        (includes: client_id, redirect_uri,
         scope, response_type=code, state)

Step 3: Authorization Server → User:
        "Do you authorize Photo App to access
         your Google Photos?"

Step 4: User → Authorization Server: GRANT

Step 5: Authorization Server → Client:
        Authorization Code (via redirect URI)
        (short-lived, single-use code)

Step 6: Client → Authorization Server:
        Exchange code for tokens
        (includes: code, client_secret, grant_type)
        *** This step is server-to-server ***
        *** Never exposed to browser ***

Step 7: Authorization Server → Client:
        Access Token + Refresh Token

Step 8: Client → Resource Server:
        API request + Access Token

Step 9: Resource Server: Validates token
        → Returns protected resource ✅
```

**Key security features of Authorization Code flow:**
- Authorization code is short-lived and single-use
- `state` parameter prevents CSRF attacks
- `client_secret` proves the client's identity to
  the authorization server
- Token exchange happens server-to-server (Step 6)
  — not in the browser — prevents token interception

---

### 4.5 OAuth 2.0 Grant Types

| Grant Type | Use Case | Security |
|-----------|---------|---------|
| **Authorization Code** | Server-side web apps with backend | ✅ Most secure |
| **Authorization Code + PKCE** | Mobile apps and SPAs (no client_secret) | ✅ Secure for public clients |
| **Client Credentials** | Machine-to-machine (no user involved) | ✅ For services |
| **Device Code** | TVs, CLIs — limited input devices | ✅ Appropriate for device |
| **Implicit** (deprecated) | Legacy browser-only apps | ❌ Deprecated — insecure |
| **Resource Owner Password Credentials** (deprecated) | Direct password grant | ❌ Deprecated — share credentials |

> [!IMPORTANT]
> **PKCE (Proof Key for Code Exchange):**
> RFC 7636 — an extension to Authorization Code
> flow that prevents authorization code interception
> attacks in mobile apps (where client_secret
> cannot be kept secret).
>
> **Implicit flow is deprecated** — it returned
> tokens directly in URL fragments which could
> be intercepted by browser history, referrer
> headers, or JavaScript on the page.

---

### 4.6 OpenID Connect (OIDC)

**OpenID Connect (OIDC)** is an authentication
layer built ON TOP OF OAuth 2.0 — it adds
the ability to verify WHO the user is (identity),
not just what they can access.

| Property | Detail |
|----------|--------|
| **Built on** | OAuth 2.0 |
| **Published** | 2014 (OpenID Foundation) |
| **Adds to OAuth** | Identity layer — ID Token (JWT) containing user information |
| **Standard** | OpenID Connect Core 1.0 |
| **Key addition** | ID Token — a signed JWT proving user's identity |

**What OIDC adds to OAuth 2.0:**
```
OAuth 2.0 response:
  Access Token (opaque — just a string)
  Refresh Token

OpenID Connect adds:
  ID Token (JWT containing user identity claims)
  UserInfo Endpoint (returns user profile data)
```

**ID Token structure (JWT):**
```
Header.Payload.Signature

Payload contains claims:
  iss  → Issuer (who issued the token)
  sub  → Subject (unique user identifier)
  aud  → Audience (client app it's intended for)
  exp  → Expiry time
  iat  → Issued at time
  nonce → Replay attack prevention
  email → User's email (if scope includes email)
  name  → User's full name (if scope includes profile)
```

> [!NOTE]
> **OIDC scopes:**
> - `openid` — required scope to get an ID Token
> - `profile` — name, given_name, family_name, picture
> - `email` — email, email_verified
> - `address` — physical mailing address
> - `phone` — phone_number

---

### 4.7 OAuth vs OpenID Connect — Core Difference

This is **the most critical distinction** in this
entire session:

```
OAuth 2.0:
  "I give this app permission to access MY photos"
  ↓
  App gets ACCESS TOKEN
  ↓
  Answers: WHAT can the app do? (Authorization)
  Does NOT answer: WHO is the user?

OpenID Connect (built on OAuth 2.0):
  "I give this app permission to know WHO I AM
   (and optionally access other resources)"
  ↓
  App gets ACCESS TOKEN + ID TOKEN (JWT)
  ↓
  Answers: WHO is the user? (Authentication)
  AND: WHAT can the app do? (Authorization)
```

| Comparison | OAuth 2.0 | OpenID Connect |
|-----------|-----------|----------------|
| **Purpose** | Authorization | Authentication + Authorization |
| **Token type** | Access Token | ID Token (JWT) + Access Token |
| **Answers** | What can the app do? | Who is the user? + What can they do? |
| **Identity info** | ❌ No | ✅ Yes — in ID Token |
| **Standard** | RFC 6749 | OpenID Connect Core 1.0 |
| **Example** | "Allow app to post tweets" | "Sign in with Google" |

---

### 4.8 OAuth vs Traditional Authentication

| Comparison | Traditional Auth | OAuth 2.0 |
|-----------|-----------------|-----------|
| **Credentials shared?** | ✅ Yes — password given to app | ❌ No — only access token |
| **Scope of access** | Full account access | Limited to granted scope |
| **Revocable?** | Only by changing password | ✅ Yes — revoke token anytime |
| **Third-party visibility** | App sees password | App never sees password |
| **Example** | Give app your Gmail username + password | Google issues token with Gmail read scope |

---

## 5. Graphical Passwords

### 5.1 What are Graphical Passwords?

**Graphical passwords** are authentication
mechanisms that use images, patterns, or visual
information instead of (or in addition to)
text-based passwords.

**Motivation:**
Text passwords have well-known weaknesses —
users choose weak, predictable passwords;
they forget them; they reuse them. Graphical
passwords attempt to leverage human memory for
visual information (which tends to be stronger
than memory for arbitrary text strings).

---

### 5.2 Categories of Graphical Passwords

#### Category 1 — Recognition-Based (Cognometric)
User authenticates by recognizing images they
previously selected from a larger set.

**Examples:**

| System | How It Works |
|--------|-------------|
| **Passfaces** | User selects human faces during registration — authenticates by recognizing their chosen faces among decoys |
| **Story** (Microsoft) | User selects a sequence of images that tells a story they can remember |
| **Déjà Vu** | User identifies images they chose during setup from a panel |

**Pros:** Easy to remember; not vulnerable to
dictionary attacks.
**Cons:** Shoulder surfing; limited password space
if few images available.

#### Category 2 — Recall-Based (Pure Recall)
User must recall and reproduce a drawing or
selection without any visual prompt.

**Examples:**

| System | How It Works |
|--------|-------------|
| **Draw-a-Secret (DAS)** | User draws a pattern on a grid — exact drawing is the password |
| **Grid Selection** | User draws freeform on a blank grid |

**Pros:** High password space if users draw
unique patterns.
**Cons:** Difficult to replicate consistently;
smudge attacks on touch screens.

#### Category 3 — Cued Recall (Locimetric)
User must click specific locations on an image
in a specific order.

**Examples:**

| System | How It Works |
|--------|-------------|
| **PassPoints** | User clicks 5 points on an image in a fixed order |
| **Cued Click Points (CCP)** | After each click, a new image appears — user clicks a point on each successive image |
| **Persuasive Cued Click Points (PCCP)** | Guides users away from hotspot areas |

**Pros:** High memorable password space using
the image as a cue.
**Cons:** Hotspot problem — users predictably
click on obvious features (eyes, faces in images).

#### Category 4 — Android Pattern Unlock
User traces a pattern through 9 dots on a grid.

```
[1] [2] [3]
[4] [5] [6]
[7] [8] [9]
```

- Pattern must touch at least 4 of 9 points
- Points can only be used once
- Maximum unique patterns: 389,112

**Known weaknesses:**
- Most users choose simple L-shapes or Z-shapes
  starting from corners
- Smudge attacks — grease traces on screen reveal pattern
- Observable from distance

> [!NOTE]
> **Hotspot problem in graphical passwords:**
> Users predictably choose the same locations
> (eyes of faces, center of images) making
> graphical password spaces effectively smaller
> than their theoretical maximum.
> This is the graphical equivalent of choosing
> "password123" — predictable despite having
> a large theoretical space.

---

### 5.3 Advantages and Disadvantages

| Advantages | Disadvantages |
|-----------|--------------|
| Visual memory is stronger than text memory | Shoulder surfing is more effective |
| No dictionary attack vulnerability | Hotspot attacks reduce entropy |
| More user-friendly for some populations | Smudge attacks on touchscreens |
| No keyboard needed | Slower to authenticate |
| Resistant to keyloggers | Not all systems support them |
| International — not language-dependent | Larger storage requirement for image comparison |

---

## 6. 📌 Extra Notes

> [!NOTE]
> Everything in this section goes beyond the core
> syllabus but is directly MCQ-relevant.

---

### 6.1 AAA Framework — Authentication,
Authorization, Accounting

> [!NOTE]
> **AAA (Authentication, Authorization, Accounting)**
> is a security framework for controlling access
> to network resources.

**AAA implementations:**

| Protocol | Full Name | Transport | Use Case |
|----------|-----------|-----------|---------|
| **RADIUS** | Remote Authentication Dial-In User Service | UDP | Wi-Fi (802.1X), VPN, dial-up |
| **TACACS+** | Terminal Access Controller Access Control System Plus | TCP | Cisco device management |
| **Diameter** | — (successor to RADIUS) | TCP/SCTP | Mobile networks (LTE, 5G) |

**RADIUS vs TACACS+:**

| Property | RADIUS | TACACS+ |
|----------|--------|---------|
| **Transport** | UDP | TCP |
| **Encryption** | Password only encrypted | Full payload encrypted |
| **Separation** | Combines AuthN + AuthZ | Separates AuthN, AuthZ, Accounting |
| **Vendor** | Open standard | Cisco-proprietary (but published) |
| **Use case** | Wi-Fi, VPN | Network device management |

---

### 6.2 TOTP vs HOTP — Deep Dive

> [!NOTE]

| Property | TOTP | HOTP |
|----------|------|------|
| **Algorithm** | HMAC-SHA1 (time-based) | HMAC-SHA1 (counter-based) |
| **Standard** | RFC 6238 | RFC 4226 |
| **Input** | Shared secret + Unix timestamp / 30 | Shared secret + counter value |
| **Validity** | 30 seconds (typical) | Until used (no expiry) |
| **Sync issue** | Clock drift between device + server | Counter desync if OTPs skipped |
| **Replay risk** | Low (30s window) | Higher (unused OTPs pile up) |
| **Examples** | Google Authenticator, Microsoft Authenticator | Physical RSA SecurID tokens |

**TOTP calculation:**
```
T = floor(Unix_Time / 30)  ← time steps since epoch
TOTP = HOTP(Secret, T)
     = Truncate(HMAC-SHA1(Secret, T))
     = 6-digit code
```

---

### 6.3 FIDO2 / WebAuthn — Preview

> [!NOTE]
> **FIDO2** is the successor to FIDO U2F —
> a modern passwordless/phishing-resistant
> authentication standard.
> Covered in depth in Session 12.

| Standard | Components |
|----------|-----------|
| **FIDO2** | WebAuthn + CTAP2 |
| **WebAuthn** | W3C/IETF standard for browser-based authentication |
| **CTAP2** | Client to Authenticator Protocol — phone/hardware key communicates with device |

**Key property:** FIDO2 keys are bound to specific
origins (domains) — they will NOT authenticate
on a phishing site even if the user is deceived.
This is why FIDO2 provides **phishing-resistant MFA**.

---

### 6.4 Passkeys — Passwordless Authentication

> [!NOTE]
> **Passkeys** are FIDO2-based credentials stored
> on your device (phone, laptop) that replace
> passwords entirely.

```
Traditional: Username + Password
Passkey: Username + Device biometric/PIN
         (device uses private key stored securely)

No password transmitted or stored on server
→ Server only stores public key
→ Cannot be phished (device-bound)
→ Cannot be breached (server has no password)
```

**Industry adoption:**
Apple (iOS 16+), Google (Android, Chrome), Microsoft
(Windows 11) all support passkeys.
FIDO Alliance drives the standard.

---

### 6.5 OAuth 2.0 Security Issues

> [!NOTE]

| Issue | Description | Mitigation |
|-------|-------------|-----------|
| **CSRF on redirect URI** | Attacker crafts authorization request — `state` not checked | Always validate `state` parameter |
| **Authorization code interception** | Code intercepted via URL/browser history | Use PKCE (RFC 7636) |
| **Open redirector** | `redirect_uri` not validated → token sent to attacker | Strict redirect_uri validation |
| **Token leakage** | Access token in URL fragment intercepted | Use Authorization Code flow (not Implicit) |
| **Confused Deputy** | App acts on behalf of user in unintended ways | Minimal scope, resource indicators |

---

### 6.6 JWT — JSON Web Token

> [!NOTE]
> **JWT (JSON Web Token)** — RFC 7519 — is a
> compact, self-contained token format used for
> transmitting claims between parties.

```
JWT Structure:
  Header.Payload.Signature

Header (Base64URL encoded JSON):
  {
    "alg": "RS256",  ← algorithm
    "typ": "JWT"
  }

Payload (Base64URL encoded JSON):
  {
    "sub": "alice@example.com",
    "iss": "https://auth.example.com",
    "exp": 1720000000,
    "iat": 1719996400,
    "scope": "photos"
  }

Signature:
  RS256_Sign(Header + "." + Payload, PrivateKey)
  OR
  HMAC-SHA256(Header + "." + Payload, SecretKey)
```

**JWT is NOT encrypted by default** — the payload
is Base64URL encoded (readable by anyone).
JWE (JSON Web Encryption) adds encryption if needed.

**JWT in OAuth/OIDC:**
- **Access Tokens** may be JWTs (or opaque strings)
- **ID Tokens** (OIDC) are always JWTs

---

### 6.7 SAML vs OAuth vs OpenID Connect —
Full Comparison

> [!NOTE]

| Property | SAML 2.0 | OAuth 2.0 | OpenID Connect |
|----------|---------|-----------|----------------|
| **Year** | 2005 | 2012 | 2014 |
| **Purpose** | Authentication (SSO) | Authorization | Authentication + Authorization |
| **Format** | XML | JSON/HTTP | JSON/HTTP (JWT) |
| **Token type** | SAML Assertion | Access Token | ID Token (JWT) + Access Token |
| **Typical use** | Enterprise SSO | API authorization | Social login, modern SSO |
| **Mobile friendly** | ❌ XML heavy | ✅ Yes | ✅ Yes |
| **Identity in token** | ✅ Yes | ❌ No | ✅ Yes (ID Token) |
| **Standard body** | OASIS | IETF | OpenID Foundation |

---

### 6.8 Kerberos Deep Dive — Tickets and KDC

> [!NOTE]

**Kerberos attack types:**

| Attack | Description |
|--------|-------------|
| **Pass-the-Ticket (PtT)** | Attacker steals Kerberos ticket from memory and uses it without knowing password |
| **Pass-the-Hash (PtH)** | Attacker uses stolen NTLM password hash directly (not Kerberos-specific) |
| **Golden Ticket** | Attacker who knows KRBTGT hash can forge any TGT — unlimited domain access |
| **Silver Ticket** | Attacker forges service ticket for a specific service — no KDC interaction |
| **Kerberoasting** | Request service tickets and crack service account passwords offline |
| **AS-REP Roasting** | Attack accounts with pre-authentication disabled — get crackable hash |

> [!NOTE]
> **Golden Ticket attack** is the most severe —
> it requires compromising the KRBTGT account's
> NTLM hash (the account that signs all TGTs).
> With this, an attacker can forge tickets for
> ANY user, including domain admins, with any
> validity period — essentially "god mode" on
> the domain.

---

### 6.9 MFA Fatigue Attack

> [!NOTE]
> **MFA Fatigue (Push Bombing)** — an attacker
> who has stolen a user's password sends
> repeated MFA push notifications to the user
> until they approve one out of annoyance or
> confusion.

**Real-world examples:**
- **Uber (2022):** Attacker sent MFA push requests
  to an Uber employee for hours — employee
  eventually approved → full internal access
- **Microsoft (2022 Lapsus$):** Similar push
  fatigue attacks used against Microsoft employees

**Defenses against MFA fatigue:**
- **Number matching** — Push shows a number that
  user must match in the auth app
- **Context awareness** — Show IP/location in
  push — user can see if location doesn't match
- **Additional context** — "Sign-in from Russia at
  3 AM — was this you?"
- **Limit push attempts** — Block account after N
  failed approvals
- **FIDO2 hardware keys** — No push mechanism —
  immune to push fatigue

---

### 6.10 Social Login — OAuth in Practice

> [!NOTE]
> **Social Login** ("Sign in with Google/Facebook/
> Apple") uses OpenID Connect (built on OAuth 2.0)
> to let users authenticate with an existing
> account rather than creating a new one.

**Flow:**
```
User clicks "Sign in with Google"
→ OpenID Connect Authorization Code flow
→ Google authenticates user
→ Returns ID Token (JWT) to app
→ App reads email/name from ID Token
→ Creates/finds user account → logs in
```

**Privacy concern:**
The Identity Provider (Google, Facebook) knows
every site you log into using their social login.

**Apple Sign In privacy feature:**
Apple Sign In can generate a unique, random relay
email per app — so the app never sees your real
Apple ID email. Apple is the IdP but the app gets
a proxy email.

---

### 6.11 Step-Up Authentication

> [!NOTE]
> **Step-Up Authentication** is when an already-
> authenticated user is prompted for ADDITIONAL
> authentication when attempting a higher-risk
> action.

```
User is logged in with password + OTP (standard MFA)

User tries to:
  → Transfer $50 to saved recipient → allowed ✅
  → View account balance → allowed ✅
  → Transfer $50,000 to new recipient →
     Step-up triggered:
     "Please re-authenticate with your fingerprint
      or hardware key to confirm this transaction"
```

**Common step-up scenarios:**
- Large financial transactions
- Changing account recovery email
- Accessing sensitive HR records
- Privileged admin actions

---

### 6.12 Password Managers and Strong
Authentication

> [!NOTE]
> **Password managers** are tools that generate,
> store, and auto-fill strong unique passwords
> for every service — enabling "something you have"
> (the password vault) + "something you know"
> (master password) authentication.

| Property | Description |
|----------|-------------|
| **What they do** | Store unique, random passwords for every site |
| **Security benefit** | No password reuse — a breach on one site doesn't compromise others |
| **Examples** | 1Password, Bitwarden, LastPass, KeePass |
| **Risk** | Master password compromise → all passwords exposed |
| **Mitigation** | Master password + MFA on the password manager itself |
| **Integration** | Modern password managers integrate with TOTP MFA |

---

## 7. Abbreviations Table

| Abbreviation | Full Form | One-Line Technical Meaning |
|---|---|---|
| MFA | Multi-Factor Authentication | Authentication using 2+ factors from different categories |
| 2FA | Two-Factor Authentication | Authentication using exactly 2 factors from different categories |
| SFA | Single Factor Authentication | Authentication using only one factor |
| OTP | One-Time Password | Single-use password — cannot be reused |
| TOTP | Time-based One-Time Password | OTP generated from HMAC-SHA1 + current Unix time (RFC 6238) |
| HOTP | HMAC-based One-Time Password | OTP generated from HMAC-SHA1 + counter (RFC 4226) |
| SSO | Single Sign-On | Authenticate once — access multiple services |
| IdP | Identity Provider | Entity that authenticates users and issues tokens/assertions |
| SP | Service Provider | Application that relies on IdP for authentication |
| SAML | Security Assertion Markup Language | XML-based SSO standard for web applications (OASIS, 2005) |
| KDC | Key Distribution Center | Kerberos central server — combines AS and TGS |
| TGT | Ticket Granting Ticket | Kerberos proof of authentication — used to request service tickets |
| TGS | Ticket Granting Server | Issues service tickets in exchange for a valid TGT |
| AS | Authentication Server | Kerberos component that verifies user identity and issues TGT |
| JWT | JSON Web Token | Compact signed token format for transmitting claims (RFC 7519) |
| OIDC | OpenID Connect | Authentication layer built on OAuth 2.0 — adds ID Token |
| PKCE | Proof Key for Code Exchange | OAuth 2.0 extension preventing code interception in public clients |
| RADIUS | Remote Authentication Dial-In User Service | AAA protocol — used for Wi-Fi 802.1X, VPN (UDP) |
| TACACS+ | Terminal Access Controller Access Control System Plus | Cisco AAA protocol — separates AuthN/AuthZ/Accounting (TCP) |
| AAA | Authentication Authorization Accounting | Three-component framework for access control |
| AuthN | Authentication | Verifying who someone is |
| AuthZ | Authorization | Determining what someone can do |
| FIDO2 | Fast IDentity Online 2 | Passwordless phishing-resistant authentication standard |
| CTAP2 | Client to Authenticator Protocol 2 | Protocol for communicating with hardware authenticators |
| CCP | Cued Click Points | Graphical password scheme using image sequences |
| DAS | Draw-A-Secret | Graphical password scheme using user-drawn patterns |

---

## 8. Keywords + Concept Map

| Term | Definition | Connections | Use Cases |
|------|-----------|-------------|-----------|
| **Authentication** | Verifying claimed identity | AuthN, AuthZ, Accounting (AAA) | Every access control system |
| **MFA** | Multiple factors from different categories | TOTP, HOTP, biometrics, FIDO2 | Secure login everywhere |
| **TOTP** | Time-based OTP — HMAC-SHA1 + timestamp | RFC 6238, 30-second window | Google Authenticator |
| **HOTP** | Counter-based OTP — HMAC-SHA1 + counter | RFC 4226, hardware tokens | RSA SecurID |
| **SSO** | Authenticate once — access many services | IdP, SP, SAML, OIDC, Kerberos | Enterprise applications |
| **Kerberos** | MIT ticket-based enterprise SSO | KDC, TGT, AS, TGS, Windows AD | Windows domain auth |
| **SAML 2.0** | XML-based enterprise web SSO | OASIS, 2005, IdP, SP, Assertion | Corporate SSO |
| **OAuth 2.0** | Authorization delegation framework | RFC 6749, access token, scopes | "Allow app to access..." |
| **OpenID Connect** | Authentication on top of OAuth 2.0 | ID Token, JWT, "Sign in with Google" | Social login, modern SSO |
| **Graphical passwords** | Visual authentication alternatives | Recognition, recall, cued recall | Mobile pattern lock |
| **MFA Fatigue** | Push bombing attack | Uber 2022, number matching defense | MFA security design |
| **Passkeys** | FIDO2-based passwordless credentials | Device-bound, phishing-resistant | Future of authentication |
| **Adaptive auth** | Risk-based dynamic auth requirements | Location, device, behavior signals | Banking, enterprise |
| **Step-Up auth** | Additional auth for high-risk actions | Financial transactions, admin access | Banking, PAM |
| **PKCE** | Prevents code interception in public clients | RFC 7636, mobile OAuth | Mobile app OAuth |

---

## 9. Quick Reference Cheatsheet

### 🔸 Authentication Factors

| Factor | Type | Example |
|--------|------|---------|
| Something you KNOW | Knowledge | Password, PIN |
| Something you HAVE | Possession | Phone, hardware key |
| Something you ARE | Inherence | Fingerprint, iris |
| Somewhere you ARE | Location | GPS, IP range |
| Something you DO | Behavior | Typing rhythm |

---

### 🔸 TOTP vs HOTP

| | TOTP | HOTP |
|---|------|------|
| RFC | 6238 | 4226 |
| Input | Time (30s steps) | Counter |
| Validity | 30 seconds | Until used |
| Risk | Clock drift | Counter desync |
| Example | Google Authenticator | RSA SecurID |

---

### 🔸 OAuth 2.0 vs OpenID Connect

| | OAuth 2.0 | OpenID Connect |
|---|-----------|----------------|
| Purpose | Authorization | Authentication |
| Token | Access Token | ID Token + Access Token |
| Answers | What can app do? | Who is the user? |
| Standard | RFC 6749 | OIDC Core 1.0 |
| Based on | — | OAuth 2.0 |

---

### 🔸 SAML vs OAuth vs OIDC

| | SAML | OAuth | OIDC |
|---|------|-------|------|
| Year | 2005 | 2012 | 2014 |
| Format | XML | JSON | JSON (JWT) |
| Purpose | AuthN (SSO) | AuthZ | AuthN + AuthZ |
| Identity | Yes | No | Yes |
| Mobile | Poor | Good | Good |

---

### 🔸 Kerberos Components

| Component | Role |
|-----------|------|
| KDC | Key Distribution Center — central trust |
| AS | Authentication Server — issues TGT |
| TGS | Ticket Granting Server — issues service tickets |
| TGT | Proof of authentication — used to get service tickets |
| Service Ticket | Access credential for a specific service |

---

### 🔸 OAuth 2.0 Grant Types Status

| Grant Type | Status |
|-----------|--------|
| Authorization Code | ✅ Use this |
| Authorization Code + PKCE | ✅ Use for mobile/SPA |
| Client Credentials | ✅ Machine-to-machine |
| Device Code | ✅ Limited UI devices |
| Implicit | ❌ Deprecated |
| Resource Owner Password | ❌ Deprecated |

---

### 🔸 SSO Risk — The Tradeoff

```
Benefit: One strong auth → all services secured
Risk:    One compromised auth → all services exposed

Mitigation: Protect the IdP with strong MFA
            + continuous session monitoring
```

---

## 10. Session Revision Snapshot

### ⚡ TL;DR — 5 Bullets

- ✅ Authentication factors: Know / Have / Are /
  Location / Behavior — MFA requires factors from
  DIFFERENT categories — same category twice is
  NOT MFA; TOTP (RFC 6238, time-based, 30s) and
  HOTP (RFC 4226, counter-based) are the two OTP
  standards both using HMAC-SHA1
- ✅ SSO — authenticate once with the IdP — all
  connected SPs trust the session — Kerberos (MIT,
  ticket-based, Windows AD, symmetric AES) and
  SAML 2.0 (OASIS, XML, enterprise web SSO) are
  the two main SSO protocols for enterprises
- ✅ OAuth 2.0 (RFC 6749, 2012) = AUTHORIZATION
  framework — NOT authentication — delegates
  limited resource access using access tokens —
  the app never sees user credentials — most
  secure flow is Authorization Code + PKCE
- ✅ OpenID Connect = Authentication layer built
  ON TOP of OAuth 2.0 — adds ID Token (JWT) proving
  WHO the user is — this is what "Sign in with
  Google/Apple" uses — OAuth handles the "what
  can the app do" part; OIDC handles "who is the user"
- ✅ Graphical passwords use visual memory instead
  of text — categories: recognition (Passfaces),
  recall (DAS), cued recall (PassPoints), pattern
  (Android 9-dot) — main weaknesses: shoulder
  surfing, hotspot problem, smudge attacks

---

### 🎯 MCQ-Likely Concepts — Everything Examiners Love

| Concept | Why It's Tricky |
|---------|----------------|
| Two factors SAME category = still single-factor | Password + security question = both "know" = SFA |
| OAuth 2.0 = Authorization NOT authentication | Most common misconception in this session |
| OpenID Connect ADDS authentication to OAuth | Built on top of OAuth — not a separate system |
| Kerberos never sends passwords over network | Ticket-based — password used only locally to decrypt |
| Kerberos requires clock sync within 5 minutes | Specific requirement for replay prevention |
| TOTP = RFC 6238; HOTP = RFC 4226 | RFC numbers commonly tested |
| SAML = XML; OAuth/OIDC = JSON | Format difference commonly tested |
| SAML from 2005; OAuth 2012; OIDC 2014 | Year order tested |
| JWT is NOT encrypted by default | Base64URL encoded — readable — not secret |
| Implicit grant = deprecated | Modern apps use Authorization Code + PKCE |
| PKCE prevents code interception for mobile apps | Extension for public clients (no client_secret) |
| IdP = authenticates users; SP = relies on IdP | Role distinction in SSO |
| MFA fatigue = Uber 2022 — push bombing | Real-world example + year |
| Number matching mitigates MFA fatigue | Specific defense mechanism |
| Android pattern has max 389,112 combinations | Specific number sometimes tested |
| Hotspot problem = users predictably click faces, center | Graphical password vulnerability |
| Smudge attack = grease trace reveals pattern | Physical attack on graphical passwords |
| Kerberos — KDC = AS + TGS | KDC is the combination of both components |
| Golden Ticket = forge any TGT using KRBTGT hash | Most severe Kerberos attack |
| RADIUS uses UDP; TACACS+ uses TCP | Protocol transport difference |

---

<details>
<summary>🔬 Lab Content (Session 11 — No Lab Assigned)</summary>

No lab is assigned for Session 11 in the syllabus.

Session 11 theory concepts (OAuth, OIDC, SSO,
MFA) are demonstrated through the web browser
and internet-connected services rather than
dedicated lab tools.

**Practical demonstrations that reinforce theory:**
- Observe OAuth flow: Click "Sign in with Google"
  on any site → watch URL parameters (code,
  state, redirect_uri) in browser developer tools
- Configure Google Authenticator or Microsoft
  Authenticator to understand TOTP in practice
- Observe SAML: Corporate SSO portals redirect
  through the IdP before granting access

Session 11 concepts directly connect to:
- **Session 12** — FIDO Authentication and Zero
  Trust Architecture (deep dive on phishing-
  resistant MFA introduced here)
- **Session 13** — SSL/TLS which carries all
  OAuth/OIDC traffic securely

</details>

---