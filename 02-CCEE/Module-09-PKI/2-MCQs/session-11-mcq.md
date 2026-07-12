# MCQ Session 11 — Strong Authentication, MFA, SSO,
OpenID, OAuth & Graphical Passwords

## 📑 Table of Contents
- [Instructions](#instructions)
- [MCQs 1–6 — Authentication Factors and MFA](#mcqs-16--authentication-factors-and-mfa)
- [MCQs 7–11 — OTP, TOTP, HOTP](#mcqs-711--otp-totp-hotp)
- [MCQs 12–16 — SSO, Kerberos, SAML](#mcqs-1216--sso-kerberos-saml)
- [MCQs 17–21 — OAuth 2.0 and OpenID Connect](#mcqs-1721--oauth-20-and-openid-connect)
- [MCQs 22–25 — Extra Notes: AAA, JWT,
  MFA Fatigue, Graphical Passwords](#mcqs-2225--extra-notes-aaa-jwt-mfa-fatigue-graphical-passwords)
- [Answer Key](#-answer-key--quick-reference)
- [Topic Coverage Map](#-topic-coverage-map)

---

## Instructions

- 25 MCQs — drawn from core syllabus AND
  📌 Extra Notes of Session 11
- Foundation + Fundamental + Basic Concepts ONLY
- 4 options per question
- ✅ marks the correct answer
- Full explanation after every question including
  why each wrong option is wrong
- Wrong options look reasonable to someone unprepared
- Correct answer is clear to someone with solid basics

---

## MCQs 1–6 — Authentication Factors and MFA

---

**Q1. A user logs in with their username and
password. Which authentication factor category
does a password belong to?**

- A) Something you ARE — inherence factor
- B) Something you HAVE — possession factor
- C) Something you KNOW — knowledge factor ✅
- D) Somewhere you ARE — location factor

> **Explanation:**
> - ✅ **C — Something you KNOW:** A password is
>   a piece of secret information that only the
>   user should know. This is the knowledge
>   factor — the most common authentication
>   factor. Other examples: PIN, passphrase,
>   security question answers.
> - ❌ **A — Something you ARE:** This is the
>   inherence factor — physical or behavioral
>   characteristics unique to the person:
>   fingerprint, iris, face, voice. A password
>   is not a physical characteristic.
> - ❌ **B — Something you HAVE:** This is the
>   possession factor — a physical or digital
>   object: USB token, smart card, mobile phone,
>   hardware key. A password is not a physical
>   object.
> - ❌ **D — Somewhere you ARE:** This is the
>   location factor — geographic or network
>   context: GPS location, IP address, known
>   Wi-Fi network. A password is not a location.

---

**Q2. A bank login requires a password AND a
fingerprint scan. Is this Multi-Factor
Authentication (MFA)?**

- A) No — both factors must be text-based for
     MFA to count
- B) No — MFA requires at least three factors,
     not two
- C) Yes — but only if the password and
     fingerprint use the same algorithm
- D) Yes — password is something you KNOW and
     fingerprint is something you ARE — two
     different factor categories ✅

> **Explanation:**
> - ✅ **D:** This is genuine MFA. Password =
>   knowledge factor (something you know).
>   Fingerprint = inherence factor (something
>   you are). Two factors from two DIFFERENT
>   categories = Multi-Factor Authentication.
>   The security benefit: even if someone steals
>   the password, they still cannot pass the
>   fingerprint check.
> - ❌ **A:** There is no requirement for factors
>   to be text-based. MFA is about using different
>   CATEGORIES of factors — text vs biometric is
>   a valid combination.
> - ❌ **B:** MFA means TWO OR MORE factors from
>   different categories. Two factors are
>   sufficient for MFA — 2FA is a specific case
>   of MFA. Three is not the minimum.
> - ❌ **C:** Factors do not need to use the same
>   algorithm. A password hashing algorithm and a
>   fingerprint matching algorithm are completely
>   different — that is entirely expected and
>   does not affect MFA validity.

---

**Q3. A user authenticates with both a password
AND a security question ("What is your mother's
maiden name?"). Does this constitute Multi-Factor
Authentication?**

- A) Yes — two inputs were provided so this is
     two-factor authentication
- B) No — both are "something you know" — same
     factor category — this is still
     single-factor authentication ✅
- C) Yes — security questions add biometric
     verification which qualifies as a second
     factor
- D) No — MFA is only valid when a hardware
     token is one of the factors

> **Explanation:**
> - ✅ **B:** This is one of the most important
>   MFA distinctions. Both a password AND a
>   security question are "something you know" —
>   the SAME factor category. Using two instances
>   of the same factor type is NOT multi-factor
>   authentication — it is just two knowledge
>   factors. True MFA requires factors from
>   DIFFERENT categories (e.g., know + have,
>   or know + are).
> - ❌ **A:** Providing two inputs does not make
>   something MFA. Both inputs must come from
>   DIFFERENT factor categories. This is a
>   common misconception — more inputs ≠ more
>   factors.
> - ❌ **C:** Security questions have no biometric
>   component — they are text-based knowledge
>   factors. Biometrics are "something you are"
>   (fingerprint, iris, face) — completely
>   different from answering a question.
> - ❌ **D:** Hardware tokens are one common
>   second factor but are not the only valid
>   second factor. Biometrics, location,
>   behavior, or any other different category
>   factor can constitute a valid second factor.

---

**Q4. Which of the following is an example of
genuine Two-Factor Authentication (2FA)?**

- A) Username + Password + Hint question
- B) Password + PIN (6-digit number)
- C) Password + OTP sent to registered mobile ✅
- D) Passphrase + Security image recognition

> **Explanation:**
> - ✅ **C — Password + OTP on mobile:** Password
>   = something you KNOW. OTP sent to your
>   registered mobile = something you HAVE
>   (your phone). Two different factor categories
>   = genuine 2FA. This is the most widely
>   deployed form of 2FA today.
> - ❌ **A:** All three are knowledge factors —
>   password, hint question, username all rely
>   on things you know. Adding a username to a
>   password does not add a new factor category.
> - ❌ **B:** Both password and PIN are knowledge
>   factors — both "something you know." Changing
>   from one text secret to two text secrets does
>   not add a new category.
> - ❌ **D:** Passphrase = something you know.
>   Security image recognition (recognizing an
>   image you selected) = also something you know
>   (or possibly something you recognize — still
>   knowledge-based). Both fall under the
>   knowledge category — not genuinely different
>   factors.

---

**Q5. What does "Adaptive Authentication" do
that standard MFA does not?**

- A) Adaptive authentication uses stronger
     encryption algorithms than standard MFA
- B) Adaptive authentication dynamically adjusts
     the authentication requirements based on
     risk signals like location, device, and
     behavior ✅
- C) Adaptive authentication replaces passwords
     entirely with biometrics
- D) Adaptive authentication requires all five
     factor categories to be verified simultaneously

> **Explanation:**
> - ✅ **B:** Adaptive (risk-based) authentication
>   evaluates context signals — location, device
>   fingerprint, time of day, IP reputation —
>   and adjusts the required authentication level
>   accordingly. Low risk = password only. High
>   risk (new country, unknown device) = password
>   + OTP + possibly admin review. Standard MFA
>   applies the same level every time.
> - ❌ **A:** Encryption algorithms are unrelated
>   to adaptive authentication. Both standard MFA
>   and adaptive authentication transmit data
>   over TLS — the authentication mechanism
>   (OTP, push, biometric) does not change the
>   encryption used.
> - ❌ **C:** Adaptive authentication does not
>   necessarily eliminate passwords — it may
>   reduce or increase authentication requirements
>   based on risk. Password replacement is
>   achieved by passwordless technologies like
>   FIDO2/Passkeys — a separate concept.
> - ❌ **D:** Requiring all five factor categories
>   simultaneously would be impractical for
>   normal use. Adaptive authentication might
>   require more factors in high-risk scenarios —
>   but "all five simultaneously" is not a
>   definition or requirement.

---

**Q6. An attacker intercepts SMS messages on a
cellular network using Signaling System 7 (SS7)
protocol vulnerabilities to receive OTP codes
meant for a victim. What is this attack
called and what is the recommended mitigation?**

- A) Man-in-the-Middle attack — use longer
     passwords to prevent interception
- B) SS7 attack against SMS OTP — switch to
     TOTP authenticator app or hardware key
     instead of SMS ✅
- C) SIM swapping attack — use a different
     mobile carrier for OTP delivery
- D) Replay attack — add timestamps to SMS
     messages to prevent reuse

> **Explanation:**
> - ✅ **B — SS7 attack / Switch to TOTP:**
>   SS7 (Signaling System 7) is the protocol
>   that connects mobile networks globally —
>   its security weaknesses allow attackers with
>   access to SS7 infrastructure to intercept
>   SMS messages. The mitigation is to move away
>   from SMS-based OTP entirely — use TOTP apps
>   (Google Authenticator) or FIDO2 hardware
>   keys which do not rely on SMS transmission.
> - ❌ **A:** Longer passwords do not protect
>   against SMS interception. The attack targets
>   the SMS delivery channel — not the password
>   itself. Password length is unrelated to
>   SS7 vulnerability.
> - ❌ **C:** SIM swapping is a different attack
>   where the attacker convinces the mobile
>   carrier to transfer the victim's number to
>   a new SIM. SS7 attacks intercept SMS at the
>   network protocol level — no SIM transfer
>   is involved. Different attack, different
>   carrier does not help against SS7.
> - ❌ **D:** Replay attack involves reusing a
>   captured valid message. SS7 attacks intercept
>   live SMS messages in real-time — timestamps
>   in the SMS content would not prevent SS7
>   interception.

---

## MCQs 7–11 — OTP, TOTP, HOTP

---

**Q7. Google Authenticator generates a new
6-digit code every 30 seconds. Which OTP
standard does it implement?**

- A) HOTP — HMAC-based OTP using an incrementing
     counter
- B) SMS OTP — delivered via cellular network
- C) TOTP — Time-based OTP using HMAC-SHA1
     and the current Unix timestamp ✅
- D) OCSP — Online Certificate Status Protocol
     for OTP validation

> **Explanation:**
> - ✅ **C — TOTP (RFC 6238):** Google Authenticator
>   implements **TOTP (Time-based One-Time Password)**
>   — defined in RFC 6238. It computes:
>   `TOTP = HOTP(shared_secret, floor(time/30))`
>   using HMAC-SHA1. Every 30 seconds the timestamp
>   counter changes, generating a new 6-digit code.
>   Both the app and the server compute the same
>   value independently without any network
>   communication.
> - ❌ **A:** HOTP (RFC 4226) uses an incrementing
>   counter — not time. HOTP codes are valid until
>   used and do not expire after 30 seconds. Physical
>   hardware tokens often use HOTP; smartphone
>   authenticator apps typically use TOTP.
> - ❌ **B:** SMS OTP is delivered via the cellular
>   network by the service provider — it is not
>   generated by a local app. Google Authenticator
>   works completely offline — no SMS, no network.
> - ❌ **D:** OCSP (Online Certificate Status
>   Protocol) is for checking certificate
>   revocation status — it has nothing to do
>   with one-time passwords or authentication
>   codes.

---

**Q8. Under which RFC is the TOTP (Time-based
One-Time Password) algorithm standardized?**

- A) RFC 4226
- B) RFC 6238 ✅
- C) RFC 7519
- D) RFC 6749

> **Explanation:**
> - ✅ **B — RFC 6238:** TOTP is defined in
>   **RFC 6238** (2011) — "TOTP: Time-Based
>   One-Time Password Algorithm." It extends
>   HOTP (RFC 4226) by replacing the counter
>   with the current Unix time divided by a
>   time step (default 30 seconds).
> - ❌ **A — RFC 4226:** This defines **HOTP**
>   — the HMAC-based One-Time Password algorithm.
>   TOTP is built on top of HOTP but uses time
>   instead of a counter. HOTP = RFC 4226;
>   TOTP = RFC 6238.
> - ❌ **C — RFC 7519:** This defines **JWT**
>   (JSON Web Token) — the compact signed token
>   format used in OAuth/OIDC. Unrelated to
>   OTP algorithms.
> - ❌ **D — RFC 6749:** This defines **OAuth 2.0**
>   — the authorization framework. Unrelated
>   to OTP algorithms.

---

**Q9. What is the key functional difference
between TOTP and HOTP?**

- A) TOTP uses RSA encryption; HOTP uses
     symmetric AES encryption
- B) TOTP generates a new code based on the
     current time (every 30 seconds); HOTP
     generates a new code based on an
     incrementing counter ✅
- C) TOTP requires internet connectivity to
     verify; HOTP works completely offline
- D) TOTP codes are 8 digits; HOTP codes
     are always 6 digits

> **Explanation:**
> - ✅ **B:** The core difference is the variable
>   input to the HMAC:
>   **TOTP** = HMAC-SHA1(Secret, Time/30) —
>   input changes every 30 seconds → code expires
>   automatically → low replay risk.
>   **HOTP** = HMAC-SHA1(Secret, Counter) —
>   counter increments each use → code valid
>   until used → higher replay risk if codes
>   accumulate unused.
>   Both use HMAC-SHA1 with a shared secret.
> - ❌ **A:** Both TOTP and HOTP use HMAC-SHA1
>   as their underlying algorithm — not RSA
>   or AES. They are symmetric HMAC operations,
>   not public-key or block-cipher operations.
> - ❌ **C:** Both TOTP and HOTP verify offline.
>   The server and client independently compute
>   the same value — no network communication
>   is needed for the OTP calculation. Both
>   work offline.
> - ❌ **D:** Both TOTP and HOTP typically
>   generate 6-digit codes (though 8-digit is
>   possible in some configurations). The number
>   of digits is not what distinguishes them
>   — the input variable (time vs counter) is
>   the fundamental difference.

---

**Q10. A hardware OTP token generates a new
code only when the user presses a button —
each button press increments the code. Which
OTP standard does this implement?**

- A) TOTP — time-based, synchronized with
     server clock
- B) SMS OTP — server-generated and transmitted
- C) HOTP — counter-based, increments on
     each use ✅
- D) Push notification — server-initiated
     approval request

> **Explanation:**
> - ✅ **C — HOTP:** The hardware token increments
>   a counter each time the button is pressed —
>   this is the **HOTP (HMAC-based One-Time
>   Password)** model defined in RFC 4226. The
>   server maintains a synchronized counter
>   and accepts codes within a look-ahead window
>   to accommodate counter drift. RSA SecurID
>   hardware tokens are a classic example.
> - ❌ **A:** TOTP generates codes based on time —
>   not button presses. A TOTP device would show
>   a new code every 30 seconds automatically
>   (no button press needed). The button-press-
>   to-generate behavior is specific to counter-
>   based HOTP.
> - ❌ **B:** SMS OTP is generated by the server
>   and sent to the user's phone via SMS — the
>   user does not press a button on a hardware
>   token. SMS OTP has no hardware token
>   component.
> - ❌ **D:** Push notification sends an approval
>   request to a mobile app — the user taps
>   approve/deny. A hardware token with button
>   presses is a fundamentally different
>   mechanism with no network communication
>   during code generation.

---

**Q11. Why is SMS-based OTP considered weaker
than TOTP app-based OTP for multi-factor
authentication?**

- A) SMS OTP codes are shorter (4 digits vs
     6 digits) making them easier to guess
- B) SMS OTP requires internet connectivity
     which makes it unavailable in some areas
- C) SMS OTP is vulnerable to SIM swapping
     and SS7 attacks — attackers can intercept
     SMS messages without touching the user's
     phone ✅
- D) SMS OTP expires too quickly — users
     often cannot enter the code in time

> **Explanation:**
> - ✅ **C:** SMS OTP's weakness is in the delivery
>   channel — not the OTP itself. Two attacks
>   target SMS delivery:
>   (1) **SIM swapping** — convince the carrier
>   to transfer the number to attacker's SIM.
>   (2) **SS7 attacks** — exploit weaknesses in
>   mobile network protocols to intercept SMS.
>   TOTP app codes are generated locally, never
>   transmitted over the phone network — immune
>   to both attacks.
> - ❌ **A:** SMS OTP codes are typically 6 digits
>   — same as TOTP. The length is not the
>   distinguishing weakness. The transmission
>   channel is the problem.
> - ❌ **B:** TOTP apps also work without internet
>   — they compute codes locally using the shared
>   secret and device clock. Both SMS and TOTP
>   have availability considerations, but lack
>   of internet is not why SMS is weaker than TOTP.
> - ❌ **D:** SMS OTP validity windows are
>   typically 3–10 minutes — plenty of time for
>   normal users. If anything, SMS codes have
>   LONGER validity than TOTP (30 seconds). The
>   expiry time is not SMS OTP's primary weakness.

---

## MCQs 12–16 — SSO, Kerberos, SAML

---

**Q12. What is the PRIMARY benefit of
Single Sign-On (SSO)?**

- A) SSO stores all user passwords in a single
     encrypted database for easy management
- B) SSO allows a user to authenticate once
     and access multiple services without
     re-authenticating for each one ✅
- C) SSO automatically generates stronger
     passwords for each service a user accesses
- D) SSO eliminates the need for any
     authentication by trusting all users
     on a network

> **Explanation:**
> - ✅ **B:** The core benefit of SSO is that
>   users authenticate ONCE with the Identity
>   Provider (IdP) and can then access all
>   connected Service Providers (SPs) without
>   entering credentials again. This reduces
>   password fatigue, simplifies user experience,
>   and centralizes authentication management.
> - ❌ **A:** SSO does not store passwords for
>   multiple services. The user authenticates
>   with the IdP — the connected SPs trust the
>   IdP's token. User passwords for individual
>   services are not collected or stored by SSO.
> - ❌ **C:** Password generation is the function
>   of a password manager — not SSO. SSO is
>   about session sharing and token-based trust,
>   not credential generation.
> - ❌ **D:** SSO absolutely requires authentication
>   — just once, at the IdP. Eliminating all
>   authentication would be a zero-trust
>   violation. SSO is "one authentication,
>   many services" — not "no authentication."

---

**Q13. Kerberos was developed at which
university, and what type of encryption does
it use for ticket operations?**

- A) Stanford University — uses RSA asymmetric
     encryption for all ticket operations
- B) MIT (Massachusetts Institute of Technology)
     — uses AES symmetric encryption ✅
- C) Cambridge University — uses DES encryption
     as originally designed
- D) Carnegie Mellon University — uses ECC
     for efficient ticket generation

> **Explanation:**
> - ✅ **B — MIT / AES:** Kerberos was developed
>   at **MIT (Massachusetts Institute of
>   Technology)** in the 1980s. The current
>   version (Kerberos v5, RFC 4120) uses **AES
>   symmetric encryption** — it is a purely
>   symmetric cryptography system. No public
>   key / asymmetric cryptography is used in
>   the core Kerberos protocol (PKINIT is an
>   extension that adds asymmetric auth for
>   initial authentication, but the core uses AES).
> - ❌ **A:** Stanford did not develop Kerberos —
>   MIT did. RSA is asymmetric encryption —
>   Kerberos uses symmetric AES. RSA in the
>   core Kerberos protocol would make it
>   much slower and was not part of the design.
> - ❌ **C:** Cambridge did not develop Kerberos —
>   MIT did. Original Kerberos did use DES, but
>   modern Kerberos v5 uses AES-128/AES-256
>   (DES was deprecated due to weakness).
> - ❌ **D:** Carnegie Mellon developed related
>   security work but NOT Kerberos. ECC is not
>   used in the core Kerberos ticket operations
>   (it is symmetric-key based).

---

**Q14. In Kerberos, what is a Ticket Granting
Ticket (TGT) and what is it used for?**

- A) A TGT is the final access credential
     that grants direct access to a specific
     network service
- B) A TGT is a proof of authentication issued
     by the AS — used to request service
     tickets without re-entering credentials ✅
- C) A TGT is a digital certificate issued
     by the CA that identifies the user
     on the network
- D) A TGT is a temporary password that
     replaces the user's actual password
     during a Kerberos session

> **Explanation:**
> - ✅ **B:** The TGT (Ticket Granting Ticket) is
>   issued by the Authentication Server (AS)
>   after the user proves their identity. It is
>   encrypted with the TGS's secret key — the
>   client cannot read it but presents it to
>   the TGS. The TGS validates the TGT and
>   issues Service Tickets for specific
>   services — all without the user entering
>   their password again. The TGT is the
>   "proof of authentication" for the session.
> - ❌ **A:** The Service Ticket (not TGT) is
>   what grants direct access to a specific
>   service. The TGT is one level above —
>   it is used to obtain Service Tickets.
>   TGT → Request → Service Ticket → Access.
> - ❌ **C:** Kerberos tickets are not X.509
>   digital certificates — they are different
>   data structures. Digital certificates use
>   PKI infrastructure; Kerberos tickets use
>   symmetric encryption with shared secrets.
>   They serve similar authentication purposes
>   but are technically different.
> - ❌ **D:** A TGT is not a temporary password —
>   it is an encrypted ticket containing
>   authentication information. The user's actual
>   password is never sent over the network in
>   Kerberos — it is used locally to decrypt
>   the AS's response.

---

**Q15. SAML 2.0 is an SSO standard maintained
by which organization, and in what data format
are SAML messages exchanged?**

- A) IETF — JSON format
- B) W3C — HTML format
- C) OASIS — XML format ✅
- D) OpenID Foundation — JWT format

> **Explanation:**
> - ✅ **C — OASIS / XML:** SAML (Security
>   Assertion Markup Language) 2.0 was developed
>   and is maintained by **OASIS (Organization
>   for the Advancement of Structured Information
>   Standards)**. SAML messages (Assertions,
>   AuthnRequests, Responses) are all formatted
>   as **XML** documents — making SAML verbose
>   compared to modern JSON-based alternatives
>   like OIDC.
> - ❌ **A:** IETF maintains OAuth 2.0 (RFC 6749)
>   and HOTP/TOTP — not SAML. SAML uses XML,
>   not JSON. IETF protocols (OAuth, OIDC) use
>   JSON/JWT.
> - ❌ **B:** W3C (World Wide Web Consortium)
>   maintains web standards like HTML, CSS,
>   and WebAuthn — not SAML. SAML is not in
>   HTML format.
> - ❌ **D:** The OpenID Foundation maintains
>   OpenID Connect — not SAML. OIDC uses JWT
>   (JSON) format. SAML predates OIDC and uses
>   XML.

---

**Q16. What is the PRIMARY security risk of
Single Sign-On (SSO)?**

- A) SSO is weaker than individual logins
     because it uses a simpler password
- B) SSO creates a single point of compromise —
     if the Identity Provider is breached,
     all connected services are compromised ✅
- C) SSO increases the number of passwords
     users must remember
- D) SSO is incompatible with Multi-Factor
     Authentication so MFA cannot be enforced

> **Explanation:**
> - ✅ **B — Single point of compromise:** SSO's
>   greatest risk is the flip side of its
>   greatest benefit. Because all services
>   trust the IdP, a successful attack on the
>   IdP credentials (or the IdP system itself)
>   gives the attacker access to ALL connected
>   services simultaneously. This is why IdP
>   protection with strong MFA and close
>   monitoring is critical.
> - ❌ **A:** SSO does not inherently use simpler
>   passwords — in fact, users can use one
>   STRONG password for the IdP rather than
>   many weak passwords for each service.
>   SSO can improve password strength.
> - ❌ **C:** SSO reduces the number of passwords
>   users must remember — ideally to one (the
>   IdP password). This is a benefit, not a risk.
> - ❌ **D:** SSO is entirely compatible with MFA —
>   in fact, one of SSO's benefits is that MFA
>   can be enforced ONCE at the IdP and applies
>   to all connected services. Most enterprise
>   SSO solutions (Okta, Azure AD, Ping Identity)
>   have built-in MFA.

---

## MCQs 17–21 — OAuth 2.0 and OpenID Connect

---

**Q17. What is the fundamental purpose of
OAuth 2.0?**

- A) To authenticate users — confirming who
     they are before granting access
- B) To encrypt data transmitted between
     applications and authorization servers
- C) To allow users to grant third-party
     applications limited access to their
     resources without sharing credentials ✅
- D) To replace username and password
     authentication with token-based logins

> **Explanation:**
> - ✅ **C:** OAuth 2.0 (RFC 6749) is an
>   **authorization** framework — it allows a
>   user (Resource Owner) to grant a third-party
>   application (Client) limited access to
>   their resources hosted on another service
>   (Resource Server) — WITHOUT sharing their
>   credentials (password). The app gets an
>   access token with a defined scope — it
>   never sees the user's password.
> - ❌ **A:** OAuth 2.0 is explicitly NOT an
>   authentication protocol — it is an
>   authorization framework. It does not
>   confirm who the user is. OpenID Connect
>   (built on OAuth 2.0) adds authentication.
>   This is the most important distinction
>   in this session.
> - ❌ **B:** Data encryption in transit is
>   handled by TLS/HTTPS — not by OAuth 2.0.
>   OAuth relies on TLS for transport security
>   but does not define encryption mechanisms.
> - ❌ **D:** OAuth 2.0 does not replace
>   username/password authentication — it allows
>   delegation of access to third-party apps.
>   The user still authenticates with the
>   Authorization Server using their credentials;
>   OAuth just prevents sharing those credentials
>   with third-party apps.

---

**Q18. In OAuth 2.0, which entity issues the
access token that a client application uses
to access protected resources?**

- A) The Resource Server — where the protected
     data is stored
- B) The Resource Owner — the user who owns
     the data
- C) The Client Application — the app
     requesting access
- D) The Authorization Server — after the
     user grants consent ✅

> **Explanation:**
> - ✅ **D — Authorization Server:** The
>   Authorization Server (e.g., Google's OAuth
>   server) is responsible for authenticating
>   the user, presenting the consent screen, and
>   issuing the access token after the user
>   grants permission. The client app exchanges
>   its authorization code for this access token
>   (in Authorization Code flow).
> - ❌ **A:** The Resource Server (e.g., Google
>   Photos API) hosts the protected resources
>   and validates access tokens — but it does
>   NOT issue tokens. Token issuance is the
>   Authorization Server's responsibility.
> - ❌ **B:** The Resource Owner (the user) grants
>   consent but does not issue tokens — that is
>   a technical function of the Authorization
>   Server. The user clicks "Allow" — the server
>   generates and issues the token.
> - ❌ **C:** The Client Application requests
>   tokens — it does not issue them. If the
>   client could issue its own tokens, it would
>   defeat the entire purpose of OAuth's delegated
>   authorization model.

---

**Q19. What is the CORE difference between
OAuth 2.0 and OpenID Connect?**

- A) OAuth 2.0 works over HTTPS; OpenID Connect
     works over HTTP only
- B) OAuth 2.0 is for mobile apps; OpenID
     Connect is for desktop apps
- C) OAuth 2.0 handles authorization (what the
     app can do); OpenID Connect adds
     authentication (who the user is) via an
     ID Token ✅
- D) OAuth 2.0 uses XML tokens; OpenID Connect
     uses JSON tokens

> **Explanation:**
> - ✅ **C:** This is the most critical distinction
>   in this session:
>   **OAuth 2.0** = Authorization framework —
>   "What can this app access on your behalf?"
>   → Issues Access Tokens.
>   **OpenID Connect** = Authentication layer
>   built ON TOP of OAuth 2.0 — "Who is the
>   user?" → Adds ID Token (JWT) containing
>   user identity claims (sub, email, name).
>   "Sign in with Google" uses OIDC — not plain
>   OAuth 2.0.
> - ❌ **A:** Both OAuth 2.0 and OpenID Connect
>   require HTTPS/TLS for transport security.
>   Neither works securely over plain HTTP.
>   The transport protocol is not what
>   distinguishes them.
> - ❌ **B:** Both OAuth 2.0 and OpenID Connect
>   are used across mobile apps, desktop apps,
>   single-page apps, and server-side web apps.
>   Platform targeting is not the distinction.
> - ❌ **D:** Both OAuth 2.0 and OpenID Connect
>   use JSON-based messages and tokens. OAuth
>   access tokens can be opaque strings or JWTs.
>   SAML uses XML — not OAuth or OIDC.

---

**Q20. "Sign in with Google" on a third-party
website uses which protocol to verify the
user's identity?**

- A) OAuth 2.0 — which provides direct identity
     verification through access tokens
- B) SAML 2.0 — XML-based enterprise SSO
     with Google as the IdP
- C) OpenID Connect — authentication layer
     on OAuth 2.0 that provides the ID Token ✅
- D) Kerberos — MIT's ticket-based enterprise
     protocol used by Google

> **Explanation:**
> - ✅ **C — OpenID Connect:** "Sign in with
>   Google" (and "Sign in with Apple/Facebook/
>   Microsoft") uses **OpenID Connect** — which
>   extends OAuth 2.0 with an ID Token (JWT).
>   The ID Token contains the user's identity
>   claims (sub, email, name) — the app reads
>   these to identify the user without the user
>   creating a separate account on that app.
>   Google is the IdP; the third-party app is
>   the Relying Party (SP).
> - ❌ **A:** Plain OAuth 2.0 does NOT provide
>   identity — it only provides authorization.
>   An access token tells you "this user authorized
>   access" but does NOT tell you WHO the user
>   is. OpenID Connect's ID Token is what
>   provides the identity claim.
> - ❌ **B:** SAML 2.0 is an enterprise SSO
>   protocol — XML-based and primarily used
>   for corporate application integration. It is
>   not what consumer-facing "Sign in with Google"
>   buttons use. SAML is heavy and not mobile-
>   friendly; OIDC is modern and lightweight.
> - ❌ **D:** Kerberos is used within enterprise
>   networks (Windows Active Directory) for
>   employee authentication to internal services.
>   Google does not use Kerberos for public
>   "Sign in with Google" — which is internet-
>   facing and requires a web-based protocol.

---

**Q21. Which OAuth 2.0 grant type is recommended
for mobile applications and single-page
applications (SPAs) that cannot securely store
a client_secret?**

- A) Implicit Grant
- B) Resource Owner Password Credentials Grant
- C) Client Credentials Grant
- D) Authorization Code with PKCE ✅

> **Explanation:**
> - ✅ **D — Authorization Code + PKCE:** Mobile
>   apps and SPAs are "public clients" — they
>   cannot securely store a `client_secret`
>   (it would be embedded in app code and could
>   be extracted). **PKCE (Proof Key for Code
>   Exchange, RFC 7636)** extends the Authorization
>   Code flow to work securely without a
>   `client_secret` — using a dynamically
>   generated code verifier and challenge to
>   prevent authorization code interception.
> - ❌ **A:** The Implicit grant was previously
>   used for SPAs — it returned tokens directly
>   in the URL fragment. It is now **deprecated**
>   because tokens in URLs are visible in browser
>   history, referrer headers, and server logs.
>   PKCE replaces Implicit for all public clients.
> - ❌ **B:** Resource Owner Password Credentials
>   grant requires the app to collect the user's
>   actual username and password — which
>   completely defeats OAuth's purpose of NOT
>   sharing credentials. It is **deprecated** and
>   should never be used for new applications.
> - ❌ **C:** Client Credentials grant is for
>   machine-to-machine communication where there
>   is NO user involved (e.g., a backend service
>   accessing an API). It is not appropriate
>   for mobile apps with a human user.

---

## MCQs 22–25 — Extra Notes: AAA, JWT,
MFA Fatigue, Graphical Passwords

---

**Q22. RADIUS and TACACS+ are both AAA
protocols. What is the key difference in
how they handle encryption?**

- A) RADIUS encrypts the entire payload; TACACS+
     encrypts only the password
- B) RADIUS encrypts only the password; TACACS+
     encrypts the entire payload ✅
- C) Both RADIUS and TACACS+ encrypt only
     usernames and passwords
- D) Neither RADIUS nor TACACS+ use encryption —
     they rely on TLS for security

> **Explanation:**
> - ✅ **B — RADIUS password-only, TACACS+ full:**
>   **RADIUS** uses UDP and encrypts ONLY the
>   password field in the authentication packet —
>   other attributes (username, accounting data)
>   are sent in cleartext. **TACACS+** uses TCP
>   and encrypts the **entire payload** — providing
>   stronger confidentiality for all authentication,
>   authorization, and accounting data. This is
>   one reason TACACS+ is preferred for network
>   device management.
> - ❌ **A:** This inverts the reality. RADIUS
>   does NOT encrypt the entire payload — only
>   the password is encrypted. TACACS+ encrypts
>   the full body.
> - ❌ **C:** TACACS+ encrypts the full payload —
>   not just usernames and passwords. RADIUS
>   does encrypt only passwords — but TACACS+
>   does much more.
> - ❌ **D:** Both RADIUS and TACACS+ have their
>   own built-in encryption. They do not simply
>   rely on TLS — they have protocol-level
>   encryption (even if RADIUS's is limited to
>   the password field). Modern deployments may
>   add TLS on top, but the protocols themselves
>   include encryption.

---

**Q23. A JWT (JSON Web Token) is used as an
ID Token in OpenID Connect. Is the payload
of a JWT encrypted by default?**

- A) Yes — JWT payloads are always encrypted
     with the recipient's public key
- B) Yes — JWT payloads are encrypted using
     AES-256 by the issuer
- C) No — JWT payloads are only Base64URL
     encoded — anyone with the token can read
     the payload contents ✅
- D) No — JWT payloads are hashed with SHA-256
     and therefore unreadable

> **Explanation:**
> - ✅ **C — Base64URL encoded, not encrypted:**
>   A standard JWT is NOT encrypted — its
>   header and payload are only **Base64URL
>   encoded** (which is trivially reversible by
>   anyone). The signature (third part) proves
>   the token was issued by the expected party
>   and has not been tampered with — but the
>   CONTENTS are readable. This is why JWTs
>   should never contain sensitive secrets
>   (passwords, SSNs). JWE (JSON Web Encryption)
>   adds actual encryption if confidentiality
>   is needed.
> - ❌ **A:** Standard JWT (JWS — JSON Web
>   Signature) is signed but NOT encrypted.
>   JWE (JSON Web Encryption) is the separate
>   standard that adds public-key-based
>   encryption — it is not the default.
> - ❌ **B:** AES-256 encryption is not applied
>   to standard JWT payloads. The payload is
>   Base64URL-encoded — all bytes are accessible.
>   JWE would use AES, but standard JWTs do not.
> - ❌ **D:** SHA-256 hashing (one-way) is not
>   applied to the payload — if it were, the
>   payload could not be read at all (hashing
>   is one-way). The payload is Base64URL
>   encoded (fully reversible). The SIGNATURE
>   is computed over the header+payload using
>   a signing algorithm — but the payload
>   itself remains readable.

---

**Q24. The Uber breach (2022) involved an
attacker who stole an employee's credentials
and then bypassed MFA. What specific MFA
attack technique was used?**

- A) SS7 attack — intercepting the employee's
     SMS OTP over the cellular network
- B) SIM swapping — transferring the employee's
     phone number to attacker's SIM
- C) MFA fatigue (push bombing) — sending
     repeated push notifications until the
     employee approved one ✅
- D) Phishing — creating a fake login page
     that captured OTP codes in real-time

> **Explanation:**
> - ✅ **C — MFA fatigue / Push bombing:**
>   In the Uber 2022 breach, the attacker
>   obtained the employee's password (via
>   credential buying) and then bombarded the
>   employee with MFA push notifications.
>   After many requests, the employee eventually
>   approved one — either out of fatigue,
>   confusion, or hoping it would stop the
>   notifications. The attacker then had full
>   access to Uber's internal systems.
>   This attack is called **MFA fatigue** or
>   **push bombing**.
> - ❌ **A:** SS7 attacks target SMS OTP interception
>   at the cellular network level. The Uber
>   breach used push notification MFA — not
>   SMS-based OTP. SS7 would not apply to app-
>   based push notifications.
> - ❌ **B:** SIM swapping involves social
>   engineering a mobile carrier to transfer
>   the victim's number. The Uber attack did
>   not involve SIM swapping — it used push
>   notification fatigue to get a legitimate
>   approval click from the employee.
> - ❌ **D:** Real-time phishing captures OTP
>   codes from a fake login page and relays
>   them instantly. The Uber attack used push
>   notifications (not OTP codes) — the employee
>   had to click approve/deny directly in the
>   authenticator app, not enter a code on a
>   webpage.

---

**Q25. Android's pattern lock uses a 3×3 grid
of 9 dots. Which category of graphical password
does this represent, and what is a known
attack against it?**

- A) Recognition-based — vulnerable to
     dictionary attacks on image databases
- B) Cued recall — vulnerable to hotspot
     attacks on commonly clicked image areas
- C) Recall-based / cued recall — vulnerable
     to smudge attacks where grease traces on
     the screen reveal the pattern ✅
- D) Knowledge-based — vulnerable to brute
     force across all possible dot sequences

> **Explanation:**
> - ✅ **C — Recall-based / Smudge attack:**
>   Android's 9-dot pattern lock is a recall-
>   based graphical password — the user must
>   remember and reproduce a specific path
>   through the dots without any image cue.
>   A well-known attack is the **smudge attack**
>   — the grease/oil residue left by a finger
>   on the touchscreen reveals the pattern path
>   when light is shone at an angle on the
>   screen. Studies show most users choose
>   simple, predictable patterns starting from
>   corner dots.
> - ❌ **A:** Recognition-based graphical passwords
>   (like Passfaces) ask users to recognize
>   images they previously selected. Android
>   pattern lock is NOT recognition-based — the
>   user draws a path, they do not select from
>   displayed options.
> - ❌ **B:** Cued recall (like PassPoints) uses
>   an image as a cue — users click specific
>   points ON an image. Android pattern lock
>   uses a blank dot grid, not an image. Hotspot
>   attacks apply to cued recall systems (users
>   predictably click eyes/faces on images) —
>   not to pattern lock specifically.
> - ❌ **D:** "Knowledge-based" is not a category
>   of graphical passwords in the classification
>   framework. The categories are recognition-
>   based, recall-based, and cued recall. Brute
>   force is a concern (389,112 maximum patterns)
>   but smudge attack is the specific, well-known
>   attack for pattern lock.

---

## 📊 Answer Key — Quick Reference

| Q | Answer | Topic |
|---|--------|-------|
| 1 | C | Password = something you KNOW |
| 2 | D | Password + fingerprint = genuine MFA |
| 3 | B | Password + security question = still SFA |
| 4 | C | Password + mobile OTP = genuine 2FA |
| 5 | B | Adaptive auth = risk-based dynamic requirements |
| 6 | B | SS7 attack + mitigation = switch to TOTP |
| 7 | C | Google Authenticator = TOTP (RFC 6238) |
| 8 | B | TOTP = RFC 6238 |
| 9 | B | TOTP = time-based; HOTP = counter-based |
| 10 | C | Button-press hardware token = HOTP |
| 11 | C | SMS OTP weak due to SIM swap + SS7 attacks |
| 12 | B | SSO = authenticate once, access many services |
| 13 | B | Kerberos = MIT, AES symmetric |
| 14 | B | TGT = proof of auth, used to get service tickets |
| 15 | C | SAML = OASIS, XML format |
| 16 | B | SSO risk = single point of compromise |
| 17 | C | OAuth 2.0 = authorization, not authentication |
| 18 | D | Access token issued by Authorization Server |
| 19 | C | OIDC adds authentication (ID Token) to OAuth |
| 20 | C | "Sign in with Google" = OpenID Connect |
| 21 | D | Mobile/SPA = Authorization Code + PKCE |
| 22 | B | RADIUS = password-only; TACACS+ = full payload |
| 23 | C | JWT payload = Base64URL encoded — not encrypted |
| 24 | C | Uber 2022 = MFA fatigue / push bombing |
| 25 | C | Android pattern = recall-based, smudge attack |

---

## 📋 Topic Coverage Map

| Q | Concept Tested | Source |
|---|----------------|--------|
| 1 | Password = knowledge factor | Core |
| 2 | MFA requires different factor categories | Core |
| 3 | Same category twice = still SFA | Core |
| 4 | Password + mobile OTP = genuine 2FA | Core |
| 5 | Adaptive authentication — risk-based | Core |
| 6 | SS7 attack on SMS OTP + mitigation | Core |
| 7 | Google Authenticator = TOTP | Core |
| 8 | TOTP RFC = 6238 | Core |
| 9 | TOTP (time) vs HOTP (counter) | Core |
| 10 | Button-press token = HOTP | Core |
| 11 | SMS OTP weakness — SIM swap + SS7 | Core |
| 12 | SSO primary benefit | Core |
| 13 | Kerberos — MIT, AES symmetric | Core |
| 14 | TGT purpose in Kerberos | Core |
| 15 | SAML = OASIS + XML | Core |
| 16 | SSO primary risk — single point of compromise | Core |
| 17 | OAuth 2.0 = authorization not authentication | Core |
| 18 | Authorization Server issues access token | Core |
| 19 | OIDC adds authentication to OAuth | Core |
| 20 | Sign in with Google = OIDC | Core |
| 21 | Authorization Code + PKCE for mobile | Core |
| 22 | RADIUS vs TACACS+ encryption | Extra Notes |
| 23 | JWT payload not encrypted — Base64URL only | Extra Notes |
| 24 | Uber 2022 = MFA fatigue attack | Extra Notes |
| 25 | Android pattern = recall-based + smudge attack | Extra Notes |

---