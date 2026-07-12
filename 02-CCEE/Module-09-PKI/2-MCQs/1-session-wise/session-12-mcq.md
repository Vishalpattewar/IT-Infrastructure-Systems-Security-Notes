# MCQ Session 12 — Authentication Protocols,
FIDO Authentication & Zero Trust Architecture

## 📑 Table of Contents
- [Instructions](#instructions)
- [MCQs 1–6 — Authentication Protocols](#mcqs-16--authentication-protocols)
- [MCQs 7–12 — EAP and 802.1X](#mcqs-712--eap-and-8021x)
- [MCQs 13–18 — FIDO Authentication](#mcqs-1318--fido-authentication)
- [MCQs 19–22 — Zero Trust Architecture](#mcqs-1922--zero-trust-architecture)
- [MCQs 23–25 — Extra Notes: NTLM, LDAP,
  Microsegmentation](#mcqs-2325--extra-notes-ntlm-ldap-microsegmentation)
- [Answer Key](#-answer-key--quick-reference)
- [Topic Coverage Map](#-topic-coverage-map)

---

## Instructions

- 25 MCQs — drawn from core syllabus AND
  📌 Extra Notes of Session 12
- Foundation + Fundamental + Basic Concepts ONLY
- 4 options per question
- ✅ marks the correct answer
- Full explanation after every question including
  why each wrong option is wrong
- Wrong options look reasonable to someone unprepared
- Correct answer is clear to someone with solid basics

---

## MCQs 1–6 — Authentication Protocols

---

**Q1. PAP (Password Authentication Protocol) is
considered the weakest authentication protocol.
What is its PRIMARY security weakness?**

- A) PAP uses MD5 hashing which is
     cryptographically broken
- B) PAP sends the password in plaintext over
     the network — anyone sniffing traffic can
     capture it ✅
- C) PAP does not support usernames — only
     passwords are transmitted
- D) PAP generates predictable challenge values
     that can be precomputed

> **Explanation:**
> - ✅ **B — Plaintext password:** PAP's critical
>   weakness is that it transmits the actual
>   password in **cleartext** — no hashing, no
>   encryption, no challenge-response. Any attacker
>   who can capture network traffic (packet sniffer
>   on the same segment) immediately obtains the
>   password. This is why PAP should never be
>   used on untrusted networks.
> - ❌ **A:** MD5 weakness applies to **CHAP** —
>   not PAP. PAP does not use MD5 at all — it
>   sends the raw password. CHAP improves on PAP
>   by using MD5 challenge-response, but even
>   MD5 has weaknesses. The two protocols have
>   different vulnerabilities.
> - ❌ **C:** PAP transmits BOTH the username AND
>   the password in plaintext. The absence of
>   username is fabricated — this is not PAP's
>   weakness.
> - ❌ **D:** Challenge values are a feature of
>   **CHAP** (Challenge Handshake Authentication
>   Protocol) — not PAP. PAP has no challenge
>   mechanism at all. This option describes a
>   different protocol entirely.

---

**Q2. CHAP (Challenge Handshake Authentication
Protocol) improves on PAP by never sending
the password over the network. What does
CHAP send instead?**

- A) The password encrypted with AES-256
- B) The username only — the password is
     verified locally on the client
- C) An MD5 hash computed from the password,
     the server's random challenge, and an
     identifier ✅
- D) A digital certificate signed by a
     trusted Certificate Authority

> **Explanation:**
> - ✅ **C — MD5 challenge-response:** In CHAP,
>   the server sends a random challenge (nonce).
>   The client computes:
>   `Response = MD5(ID + Password + Challenge)`
>   and sends only this response — never the
>   password itself. The server independently
>   computes the same MD5 value and compares.
>   If they match, the password is verified
>   without the password crossing the network.
> - ❌ **A:** CHAP does not use AES-256 encryption.
>   It uses MD5 — a hash function, not encryption.
>   The result is a one-way hash (response) —
>   not encrypted password data that could be
>   decrypted with a key.
> - ❌ **B:** The username is transmitted (the
>   server needs to know which user is
>   authenticating) but the password is NOT
>   verified locally on the client — the server
>   computes the expected MD5 response and
>   compares it to what the client sent.
> - ❌ **D:** CHAP does not use digital
>   certificates — it is a simple HMAC/MD5
>   challenge-response protocol. Certificate-
>   based authentication describes EAP-TLS —
>   a completely different and more secure
>   protocol.

---

**Q3. What is EAP (Extensible Authentication
Protocol) — and is it an authentication
method or something else?**

- A) EAP is a specific authentication method
     that uses HMAC-SHA256 for enterprise
     Wi-Fi security
- B) EAP is an authentication FRAMEWORK that
     allows multiple authentication methods to
     operate over the same transport — it is
     not a method itself ✅
- C) EAP is an encryption protocol that
     protects Wi-Fi data frames after
     authentication completes
- D) EAP is a digital certificate format used
     in WPA2-Enterprise environments

> **Explanation:**
> - ✅ **B — EAP is a framework:** This is the
>   most important fact about EAP. EAP (RFC 3748)
>   defines a common set of message types
>   (Request, Response, Success, Failure) —
>   but the actual authentication logic is
>   provided by EAP METHODS that plug into this
>   framework (EAP-TLS, PEAP, EAP-MD5, EAP-FAST
>   etc.). New methods can be added without
>   changing the framework — hence "Extensible."
> - ❌ **A:** EAP is not a single method using
>   HMAC-SHA256. HMAC-SHA256 might be used
>   internally by some EAP methods — but EAP
>   itself defines the messaging framework, not
>   a specific cryptographic operation.
> - ❌ **C:** EAP handles authentication —
>   not data frame encryption. After 802.1X/EAP
>   authentication, encryption of Wi-Fi frames
>   is handled by WPA2 (AES-CCMP) or WPA3 —
>   separate from EAP.
> - ❌ **D:** EAP is a protocol — not a certificate
>   format. Certificate formats are defined by
>   X.509 and PKCS standards. EAP-TLS uses
>   X.509 certificates as part of its method —
>   but EAP itself is not a certificate format.

---

**Q4. EAP-TLS is considered the STRONGEST EAP
method for enterprise Wi-Fi. What makes it
stronger than PEAP?**

- A) EAP-TLS uses AES-256 while PEAP uses
     the weaker AES-128 for the tunnel
- B) EAP-TLS requires BOTH the client AND the
     server to present digital certificates —
     providing mutual authentication ✅
- C) EAP-TLS is faster because it skips the
     TLS handshake that PEAP requires
- D) EAP-TLS works without a RADIUS server
     while PEAP requires RADIUS for validation

> **Explanation:**
> - ✅ **B — Mutual authentication with
>   certificates:** EAP-TLS requires BOTH:
>   (1) The server presents its certificate →
>   client verifies server identity.
>   (2) The client presents its certificate →
>   server verifies client identity.
>   This mutual TLS authentication eliminates
>   shared passwords entirely. PEAP requires
>   only the SERVER certificate — the client
>   authenticates inside the TLS tunnel using
>   MSCHAPv2 (username + password). No client
>   certificate = one less layer of security.
> - ❌ **A:** Both EAP-TLS and PEAP use TLS for
>   their transport layer. The cipher suites
>   (AES-128 vs AES-256) used in the TLS tunnel
>   are configuration choices — not a structural
>   difference between the two methods. The
>   distinguishing feature is client certificates,
>   not tunnel encryption strength.
> - ❌ **C:** EAP-TLS actually uses the TLS
>   handshake for both server AND client
>   authentication — it is not faster than PEAP.
>   PEAP also performs a TLS handshake (for the
>   outer tunnel) and then an inner MSCHAPv2
>   exchange. EAP-TLS complexity is the reason
>   it is harder to deploy, not faster.
> - ❌ **D:** Both EAP-TLS and PEAP are used
>   with 802.1X and require a RADIUS server as
>   the authentication server. Neither works
>   without RADIUS in an enterprise 802.1X
>   deployment. The absence of a RADIUS server
>   is not a distinguishing feature of EAP-TLS.

---

**Q5. Which authentication protocol sends
the user's password in cleartext and should
NEVER be used on untrusted networks?**

- A) CHAP
- B) EAP-TLS
- C) PEAP
- D) PAP ✅

> **Explanation:**
> - ✅ **D — PAP:** PAP (Password Authentication
>   Protocol, RFC 1334) is the only protocol
>   among these that transmits the password in
>   plain cleartext with no protection. It was
>   designed for simple dial-up connections where
>   the physical link was considered secure —
>   completely inappropriate for any modern
>   network where eavesdropping is possible.
> - ❌ **A — CHAP:** CHAP uses MD5 challenge-
>   response — the password is NEVER sent.
>   Only an MD5 hash response crosses the
>   network. While MD5 is weak, CHAP is vastly
>   better than PAP for this specific concern.
> - ❌ **B — EAP-TLS:** EAP-TLS uses digital
>   certificates for mutual authentication —
>   no password is involved at all. It is one
>   of the most secure authentication methods
>   available.
> - ❌ **C — PEAP:** PEAP creates a TLS-encrypted
>   tunnel and authenticates the client INSIDE
>   the tunnel — the username and password are
>   protected by TLS encryption. The password
>   is not sent in cleartext.

---

**Q6. MS-CHAPv2 is used inside PEAP for inner
authentication in WPA2-Enterprise. What is
its known security concern?**

- A) MS-CHAPv2 requires a hardware token —
     making it impractical for large deployments
- B) MS-CHAPv2 was cryptographically broken
     in 2012 — the handshake can be cracked
     offline using cloud services ✅
- C) MS-CHAPv2 sends passwords in plaintext —
     similar to PAP
- D) MS-CHAPv2 is incompatible with Active
     Directory — requiring a separate user
     database

> **Explanation:**
> - ✅ **B — Broken in 2012:** MS-CHAPv2 (used
>   inside PEAP and historically in PPTP VPN)
>   was demonstrated to be fully breakable in
>   2012 by Moxie Marlinspike using the
>   CloudCracker service. The MS-CHAPv2
>   challenge-response can be captured and
>   brute-forced offline with 100% certainty —
>   because the DES-based encryption it uses
>   reduces to a manageable keyspace. This
>   is why EAP-TLS is preferred over PEAP-
>   MSCHAPv2 for high-security environments.
> - ❌ **A:** MS-CHAPv2 uses username and
>   password — no hardware token required.
>   It is widely deployed specifically because
>   it requires only standard credentials,
>   not hardware.
> - ❌ **C:** MS-CHAPv2, like CHAP, uses a
>   challenge-response mechanism — the password
>   is NEVER sent in plaintext. Its weakness
>   is that the challenge-response can be
>   cracked offline — not that the password
>   crosses the wire in cleartext.
> - ❌ **D:** MS-CHAPv2 is a Microsoft protocol
>   designed specifically FOR Active Directory
>   integration — it is very compatible with
>   AD. PEAP-MSCHAPv2 with a Windows RADIUS
>   server (NPS) is one of the most common
>   enterprise Wi-Fi deployments.

---

## MCQs 7–12 — EAP and 802.1X

---

**Q7. IEEE 802.1X provides port-based network
access control. What are the three roles
defined in an 802.1X deployment?**

- A) Client, Firewall, and Database Server
- B) Initiator, Responder, and Key Server
- C) Supplicant, Authenticator, and
     Authentication Server ✅
- D) User, Policy Engine, and Policy
     Enforcement Point

> **Explanation:**
> - ✅ **C — Three 802.1X roles:**
>   **Supplicant** = the device wanting network
>   access (laptop, phone).
>   **Authenticator** = the network device
>   controlling the port (Wi-Fi AP or 802.1X
>   switch) — relays EAP between supplicant
>   and auth server.
>   **Authentication Server** = the backend
>   server (RADIUS) that actually verifies
>   credentials and makes the grant/deny
>   decision.
> - ❌ **A:** "Client, Firewall, Database" are
>   general network components — not the specific
>   IEEE 802.1X role names. The 802.1X standard
>   uses precise terminology: Supplicant,
>   Authenticator, Authentication Server.
> - ❌ **B:** "Initiator, Responder, Key Server"
>   are roles in IKE (Internet Key Exchange)
>   for IPSec VPNs — not 802.1X. Mixing these
>   up is a common trap between different
>   authentication framework terminologies.
> - ❌ **D:** "User, Policy Engine, Policy
>   Enforcement Point" are Zero Trust Architecture
>   components (from NIST SP 800-207) — not
>   802.1X roles. These two frameworks have
>   different role terminologies.

---

**Q8. In an 802.1X deployment, what is EAPOL
and what does it transport?**

- A) EAPOL is a certificate format for
     smart cards used in 802.1X authentication
- B) EAPOL is EAP over LAN — the transport
     protocol that carries EAP messages between
     the supplicant and the authenticator ✅
- C) EAPOL is an encryption algorithm used
     by Wi-Fi access points to protect EAP
     messages from eavesdropping
- D) EAPOL is the RADIUS protocol extension
     that carries EAP messages between the
     authenticator and the authentication server

> **Explanation:**
> - ✅ **B — EAP over LAN:** EAPOL (EAP over
>   LAN) is defined in IEEE 802.1X and is the
>   Layer 2 protocol that carries EAP messages
>   between the **supplicant** (device) and
>   the **authenticator** (AP/switch). Before
>   authentication is complete, the port only
>   allows EAPOL traffic — all other traffic
>   is blocked. The authenticator then relays
>   EAP messages to the RADIUS server.
> - ❌ **A:** EAPOL is a transport protocol —
>   not a certificate format. Certificate
>   formats are defined by X.509 (DER, PEM,
>   PKCS#12). EAPOL is purely about carrying
>   EAP messages on a LAN segment.
> - ❌ **C:** EAPOL is not an encryption
>   algorithm — it is a transport mechanism.
>   After 802.1X authentication, Wi-Fi frame
>   encryption is handled by WPA2/WPA3
>   (AES-CCMP/GCMP). EAPOL itself is not
>   an encryption method.
> - ❌ **D:** This describes the RADIUS protocol
>   (Access-Request messages) — not EAPOL.
>   Between the Authenticator and the RADIUS
>   server, EAP messages are carried INSIDE
>   RADIUS packets — not EAPOL. EAPOL is
>   specifically the Layer 2 link between
>   Supplicant and Authenticator.

---

**Q9. WPA2-Enterprise uses 802.1X and EAP
for authentication. How does this differ
from WPA2-Personal (PSK)?**

- A) WPA2-Enterprise uses AES encryption;
     WPA2-Personal uses the weaker TKIP
- B) WPA2-Personal requires a RADIUS server;
     WPA2-Enterprise uses a shared passphrase
- C) WPA2-Enterprise gives each user unique
     credentials via 802.1X/EAP — WPA2-Personal
     uses a single shared passphrase for all
     users ✅
- D) WPA2-Enterprise is for home use; WPA2-
     Personal is for enterprise environments

> **Explanation:**
> - ✅ **C:** The core difference:
>   **WPA2-Personal (PSK):** One shared
>   passphrase for ALL users on the network.
>   If one device is compromised or the password
>   is leaked, ALL users on the network are
>   affected. Simple to set up.
>   **WPA2-Enterprise (802.1X/EAP):** Each user
>   has UNIQUE credentials authenticated via
>   RADIUS. Revoking one user's access is easy.
>   More complex to set up but far more secure
>   and scalable for organizations.
> - ❌ **A:** Both WPA2-Personal and WPA2-
>   Enterprise use AES-CCMP for data encryption.
>   The encryption standard is not what
>   distinguishes them — the authentication
>   mechanism is.
> - ❌ **B:** This completely inverts the truth.
>   WPA2-**Enterprise** uses a RADIUS server;
>   WPA2-**Personal** uses a shared passphrase.
>   Getting these backwards is a common trap.
> - ❌ **D:** This is completely backwards.
>   WPA2-Personal (PSK) is for home and small
>   office use; WPA2-Enterprise (802.1X) is
>   designed for enterprise environments where
>   per-user authentication and centralized
>   management are needed.

---

**Q10. LDAP is used for directory access and
authentication. Which port does LDAPS
(LDAP over TLS) use?**

- A) 389
- B) 443
- C) 636 ✅
- D) 8080

> **Explanation:**
> - ✅ **C — Port 636:** LDAPS (LDAP over SSL/TLS)
>   uses **port 636** for encrypted LDAP
>   connections. The encryption protects the
>   BIND request (which contains the username
>   and password) from eavesdropping. LDAPS
>   is the recommended way to use LDAP in
>   any security-conscious environment.
> - ❌ **A — 389:** Port 389 is for plain
>   **LDAP** — the unencrypted version. Using
>   port 389 without STARTTLS means credentials
>   can be captured in plaintext. Port 389 vs
>   636 is a specific fact frequently tested.
> - ❌ **B — 443:** Port 443 is for **HTTPS**
>   (HTTP over TLS). While TLS is also used for
>   LDAPS, the port number for LDAPS is 636 —
>   not 443.
> - ❌ **D — 8080:** Port 8080 is a common
>   alternative HTTP port used for web proxies
>   and development servers — it has no relation
>   to LDAP or LDAPS.

---

**Q11. An enterprise is setting up WPA2-
Enterprise Wi-Fi using 802.1X. They want the
simplest deployment that does NOT require
issuing digital certificates to every user
device. Which EAP method should they choose?**

- A) EAP-TLS — the strongest and most secure
- B) EAP-MD5 — the simplest legacy method
- C) PEAP (Protected EAP) — uses a server
     certificate only; client authenticates
     with username and password inside the
     TLS tunnel ✅
- D) EAP-SIM — uses mobile SIM cards for
     authentication

> **Explanation:**
> - ✅ **C — PEAP:** PEAP is the most widely
>   deployed EAP method specifically because
>   it does NOT require client-side certificates.
>   The server presents its certificate (client
>   verifies server identity), then creates a
>   TLS tunnel inside which the client sends
>   MSCHAPv2 credentials (username + password).
>   IT departments can deploy it using existing
>   Active Directory user accounts — no PKI
>   infrastructure for client certs needed.
> - ❌ **A — EAP-TLS:** EAP-TLS DOES require
>   client certificates — this is what the
>   question specifically wants to avoid.
>   EAP-TLS is the most secure but the most
>   complex to deploy because every device
>   needs a certificate from the PKI.
> - ❌ **B — EAP-MD5:** EAP-MD5 is a legacy,
>   insecure method — it does not provide
>   server authentication (the client cannot
>   verify the server's identity), making it
>   vulnerable to MITM attacks. It is not
>   used in modern deployments.
> - ❌ **D — EAP-SIM:** EAP-SIM uses mobile
>   SIM cards for authentication — designed
>   for mobile carrier networks. It requires
>   SIM card infrastructure and is not
>   typically used for enterprise Wi-Fi.

---

**Q12. In 802.1X, what happens to network
traffic on a port BEFORE a supplicant
successfully authenticates?**

- A) All traffic is allowed but monitored
     for suspicious activity
- B) Only encrypted HTTPS traffic is allowed
     through the port
- C) The port is in UNAUTHORIZED state —
     only EAPOL (authentication) traffic
     is permitted ✅
- D) All traffic is allowed except for
     traffic to the RADIUS server

> **Explanation:**
> - ✅ **C — UNAUTHORIZED state, EAPOL only:**
>   Before successful authentication, the
>   802.1X port is in the UNAUTHORIZED state.
>   In this state, the port blocks ALL traffic
>   EXCEPT EAPOL (EAP over LAN) messages —
>   which are needed for the authentication
>   exchange itself. Once the RADIUS server
>   returns Access-Accept, the port moves to
>   AUTHORIZED state and normal traffic flows.
> - ❌ **A:** If all traffic were allowed but
>   monitored, 802.1X would provide no access
>   control — just visibility. The entire
>   purpose of 802.1X is to BLOCK access until
>   credentials are verified. Monitoring without
>   blocking is not 802.1X.
> - ❌ **B:** 802.1X does not selectively allow
>   HTTPS while blocking other traffic. The
>   port either passes only EAPOL (unauthorized)
>   or all traffic (authorized). There is no
>   protocol-selective filtering in the 802.1X
>   state machine.
> - ❌ **D:** Allowing all traffic except RADIUS
>   traffic would be completely backwards —
>   RADIUS traffic is what enables authentication.
>   The unauthorized state blocks everything
>   except EAPOL authentication messages.

---

## MCQs 13–18 — FIDO Authentication

---

**Q13. What does FIDO stand for, and in what
year was the FIDO Alliance founded?**

- A) Federated Identity and Data Organization —
     founded in 2010
- B) Fast IDentity Online — founded in 2012 ✅
- C) Federal Internet Data Operations —
     founded in 2014
- D) Fast Integrated Digital Operations —
     founded in 2018

> **Explanation:**
> - ✅ **B — Fast IDentity Online, 2012:**
>   **FIDO** stands for **Fast IDentity Online**.
>   The **FIDO Alliance** was founded in **2012**
>   as an open industry consortium of technology
>   companies (Google, Microsoft, Apple, Intel,
>   Qualcomm, Yubico, PayPal, VISA and others)
>   with the mission to reduce reliance on
>   passwords through open, scalable, interoperable
>   authentication standards.
> - ❌ **A:** "Federated Identity and Data
>   Organization" is fabricated — FIDO stands
>   for Fast IDentity Online. The year 2010 is
>   when Zero Trust was coined (by John Kindervag)
>   — not when FIDO Alliance was founded.
> - ❌ **C:** "Federal Internet Data Operations"
>   is fabricated. 2014 is when FIDO U2F was
>   launched — not when FIDO Alliance was
>   founded (2012).
> - ❌ **D:** "Fast Integrated Digital Operations"
>   is fabricated. 2018 is when FIDO2 was launched
>   — the modern standard — not the founding year.

---

**Q14. FIDO2 is the modern FIDO standard for
passwordless authentication. What are its
two component standards?**

- A) SAML 2.0 (OASIS) + OAuth 2.0 (IETF)
- B) PKCS#11 (FIDO Alliance) + X.509 (ITU-T)
- C) WebAuthn (W3C) + CTAP2 (FIDO Alliance) ✅
- D) OpenID Connect (OpenID Foundation) +
     JWT (IETF)

> **Explanation:**
> - ✅ **C — WebAuthn + CTAP2:**
>   **FIDO2** consists of exactly two components:
>   **WebAuthn** (Web Authentication API) —
>   defined by W3C — the browser-side API that
>   websites use to request authentication.
>   **CTAP2** (Client to Authenticator Protocol 2)
>   — defined by FIDO Alliance — the protocol
>   between the browser/OS and the authenticator
>   (hardware key, phone).
>   Together: Browser (WebAuthn) ← CTAP2 →
>   Authenticator.
> - ❌ **A:** SAML 2.0 and OAuth 2.0 are SSO
>   and authorization standards — not FIDO2
>   components. FIDO2 is specifically about
>   cryptographic authenticator-based login,
>   not XML assertions or access tokens.
> - ❌ **B:** PKCS#11 is the cryptographic token
>   API standard (for HSMs, smart cards) —
>   not a FIDO2 component. X.509 is the
>   certificate format standard. Neither is
>   a FIDO2 component — though FIDO2 uses
>   public key cryptography internally.
> - ❌ **D:** OpenID Connect is an authentication
>   layer on OAuth 2.0 — it uses ID Tokens (JWT)
>   for identity. FIDO2 is a separate, hardware-
>   backed authentication standard. While FIDO2
>   can be used AS the authentication factor
>   within an OIDC flow, they are different
>   standards with different components.

---

**Q15. What is the PRIMARY reason FIDO2 is
described as "phishing-resistant"?**

- A) FIDO2 sends a one-time password that
     expires before a phisher can use it
- B) FIDO2 credentials are cryptographically
     bound to the Relying Party ID (RP_ID —
     the website domain) — a phishing site has
     a different domain so no valid credential
     exists for it ✅
- C) FIDO2 uses hardware encryption that
     phishing sites cannot decrypt
- D) FIDO2 requires the user to scan a QR
     code that only appears on legitimate
     websites

> **Explanation:**
> - ✅ **B — RP_ID domain binding:** During FIDO2
>   REGISTRATION, the credential (key pair) is
>   bound to the **RP_ID** (the exact website
>   domain, e.g., `google.com`). During
>   AUTHENTICATION, the authenticator checks
>   the RP_ID of the requesting site. A phishing
>   site at `g00gle.com` has RP_ID = `g00gle.com`
>   — the authenticator has NO credential for
>   this RP_ID — authentication fails
>   automatically. The user cannot accidentally
>   authenticate to the wrong site.
> - ❌ **A:** FIDO2 does not use OTP codes —
>   it uses asymmetric cryptographic signatures.
>   OTP codes (TOTP) ARE phishable in real-time
>   because they can be relayed. FIDO2's
>   phishing resistance comes from domain
>   binding — not code expiry.
> - ❌ **C:** Phishing resistance is not about
>   encryption that phishing sites cannot
>   decrypt. The protection is architectural —
>   the credential simply does not work on
>   a different domain. There is no "hardware
>   encryption" that phishing sites attempt
>   to break.
> - ❌ **D:** FIDO2 does not require QR code
>   scanning as a phishing prevention mechanism.
>   QR codes are one possible interaction
>   method for CTAP2 hybrid (phone as
>   authenticator) but they are not what
>   makes FIDO2 phishing-resistant.

---

**Q16. In FIDO2, where is the private key
stored and does it ever leave that location?**

- A) The private key is stored on the website's
     server — it is sent to the browser during
     each authentication
- B) The private key is stored in the browser's
     cookie storage — cleared after each session
- C) The private key is stored securely inside
     the authenticator (hardware key, phone
     Secure Enclave, or TPM) and NEVER leaves
     it ✅
- D) The private key is derived from the
     user's password each time — no persistent
     storage needed

> **Explanation:**
> - ✅ **C — Private key stays in authenticator:**
>   The FIDO2 private key is generated INSIDE
>   the authenticator during registration and
>   NEVER exported or transmitted. All signing
>   operations happen inside the authenticator.
>   The server stores ONLY the public key. This
>   is what makes FIDO2 resistant to server-side
>   breaches — stealing the server database
>   only gets you public keys, which are useless
>   for impersonation.
> - ❌ **A:** If the private key were on the
>   server and sent to the browser, it would
>   be trivially stolen during any server breach
>   or network interception. This completely
>   inverts the FIDO2 security model. The server
>   only ever receives and stores the PUBLIC key.
> - ❌ **B:** Browser cookie storage is completely
>   insecure for cryptographic private keys —
>   cookies are accessible to JavaScript,
>   browser extensions, and can be stolen.
>   FIDO2 uses dedicated secure hardware
>   (Secure Enclave, TPM, dedicated security
>   chip) — not browser storage.
> - ❌ **D:** Password-derived keys describe
>   PBKDF2 / password-based KDFs — not FIDO2.
>   FIDO2 generates a RANDOM asymmetric key
>   pair during registration — the key is NOT
>   derived from a password each time. In fact,
>   removing the need for passwords is a core
>   FIDO2 goal.

---

**Q17. FIDO U2F was introduced in 2014 as a
hardware second factor. FIDO2 was introduced
in 2018. What is the key additional
capability FIDO2 provides over U2F?**

- A) FIDO2 supports more websites than
     U2F — U2F only worked with Google
- B) FIDO2 enables fully passwordless
     authentication — U2F was only a
     second factor requiring a password first ✅
- C) FIDO2 uses stronger 4096-bit RSA keys
     compared to U2F's weaker 2048-bit keys
- D) FIDO2 works over Wi-Fi while U2F
     required a wired USB connection

> **Explanation:**
> - ✅ **B — Passwordless capability:**
>   FIDO U2F was designed as a SECOND FACTOR —
>   the user still entered their username and
>   password FIRST, then used the hardware key
>   as the second factor.
>   FIDO2 extends this to support PASSWORDLESS
>   authentication — using resident keys
>   (discoverable credentials), a user can
>   log in by ONLY presenting the authenticator
>   (with biometric/PIN) — NO password required
>   at all. This is the fundamental advancement.
> - ❌ **A:** U2F was supported by all major
>   browsers (Chrome, Firefox, Edge) and websites
>   — not just Google. Website support was broad.
>   FIDO2 is backward compatible with U2F
>   devices — it did not expand to new websites
>   in a way that U2F couldn't handle.
> - ❌ **C:** Both U2F and FIDO2 typically use
>   ECDSA P-256 (256-bit elliptic curve keys)
>   — not 4096-bit or 2048-bit RSA. The
>   cryptographic key type and size are similar
>   between the two. The advancement is
>   architectural (passwordless) — not key size.
> - ❌ **D:** U2F supported USB HID, NFC, and
>   Bluetooth — not just wired USB. FIDO2 added
>   additional transports and the CTAP2 protocol,
>   but the "only wired USB" description of U2F
>   is incorrect. Transport options are not
>   the key advancement.

---

**Q18. During FIDO2 authentication, the
server includes a COUNTER value that the
authenticator increments with each use.
What security threat does this counter
prevent?**

- A) It prevents brute force attacks by
     rate-limiting the number of authentication
     attempts per session
- B) It prevents cloned credential attacks
     — if an authenticator is cloned, the
     cloned device's counter will fall behind
     the legitimate device's counter ✅
- C) It prevents replay attacks by ensuring
     each challenge has a different value
- D) It prevents man-in-the-middle attacks
     by including the server's IP address
     in the counter calculation

> **Explanation:**
> - ✅ **B — Clone detection:** The FIDO2 counter
>   is a monotonically increasing value stored
>   in the authenticator. After each successful
>   authentication, the counter increments.
>   The server stores the last-seen counter
>   value. If a counter value received is EQUAL
>   TO or LESS THAN the stored value, the server
>   rejects the authentication — this indicates
>   the authenticator may have been cloned
>   (the clone's counter lags behind the
>   original). This is the counter's primary
>   security purpose.
> - ❌ **A:** Rate limiting authentication attempts
>   is a server-side or policy-based mechanism —
>   not what the authenticator counter does.
>   The counter is about detecting cloning,
>   not limiting attempt frequency.
> - ❌ **C:** Replay attack prevention in FIDO2
>   is handled by the **challenge** — the server
>   generates a fresh random challenge for each
>   authentication. The counter adds clone
>   detection on top of replay prevention —
>   they are separate mechanisms serving
>   different purposes.
> - ❌ **D:** The counter does not contain or
>   calculate from the server's IP address.
>   It is simply an integer that increments
>   inside the authenticator. MITM protection
>   in FIDO2 comes from the RP_ID binding —
>   not the counter.

---

## MCQs 19–22 — Zero Trust Architecture

---

**Q19. Zero Trust Architecture was originally
coined by which analyst at which organization,
and in what year?**

- A) Scott Rose at NIST — 2020
- B) John Kindervag at Forrester Research — 2010 ✅
- C) Bruce Schneier at Harvard — 2015
- D) Phil Zimmermann at RSA Security — 2008

> **Explanation:**
> - ✅ **B — John Kindervag, Forrester, 2010:**
>   The term and concept of **Zero Trust** was
>   coined by **John Kindervag** while he was
>   a principal analyst at **Forrester Research**
>   in **2010**. His foundational paper introduced
>   the "never trust, always verify" model as
>   a replacement for the perimeter-based trust
>   model. NIST later formalized it in
>   SP 800-207 (August 2020) — but Kindervag
>   is the originator.
> - ❌ **A — Scott Rose, NIST, 2020:** Scott Rose
>   is one of the authors of NIST SP 800-207
>   (Zero Trust Architecture) published in 2020.
>   But NIST formalized Zero Trust — they did
>   not coin the term. Kindervag coined it at
>   Forrester in 2010.
> - ❌ **C:** Bruce Schneier is a prominent
>   security technologist and cryptographer
>   but did NOT coin Zero Trust. 2015 is
>   not the relevant year for either the
>   original coining or NIST formalization.
> - ❌ **D:** Phil Zimmermann created PGP (1991)
>   and co-founded Silent Circle — he is a
>   privacy and encryption expert. He has no
>   connection to Zero Trust Architecture.
>   2008 is also not the correct year.

---

**Q20. What is the CORE principle that
distinguishes Zero Trust from the traditional
perimeter security model?**

- A) Zero Trust uses stronger encryption
     algorithms than perimeter security
- B) Zero Trust replaces firewalls with
     AI-powered intrusion detection systems
- C) Traditional perimeter security trusts
     users inside the network — Zero Trust
     trusts NO ONE by default and verifies
     every access request regardless of
     location ✅
- D) Zero Trust eliminates the need for
     user authentication by using device
     fingerprinting alone

> **Explanation:**
> - ✅ **C — Never trust, always verify:**
>   The traditional perimeter model assumes
>   that once a user or device is INSIDE the
>   network (behind the firewall), they are
>   trusted. Zero Trust rejects this assumption
>   — location (inside vs outside the network)
>   does not grant trust. EVERY request —
>   whether from inside or outside the network —
>   must be authenticated, authorized, and
>   continuously validated based on identity,
>   device health, and context.
> - ❌ **A:** Zero Trust is an architectural
>   philosophy — not an encryption strength
>   upgrade. The same encryption algorithms
>   (AES, TLS) are used in both models. The
>   difference is in WHO is trusted and
>   HOW access is granted — not which
>   cryptographic algorithms are used.
> - ❌ **B:** Replacing firewalls with AI IDS
>   is not a Zero Trust principle. Zero Trust
>   DOES incorporate behavior analytics (UEBA)
>   and automation, but it does not eliminate
>   firewalls — it adds identity-centric access
>   control on top of network controls.
> - ❌ **D:** Zero Trust does not eliminate
>   user authentication — it STRENGTHENS it
>   (requiring MFA, continuous verification).
>   Device fingerprinting is ONE signal used
>   in Zero Trust decisions — but user identity
>   verification is still essential.

---

**Q21. NIST Special Publication 800-207
defines Zero Trust Architecture. When was
it published and what are the three core
principles it describes?**

- A) Published 2018 — Verify Everything,
     Block All Traffic, Encrypt All Data
- B) Published 2020 — Verify Explicitly,
     Use Least Privilege Access, Assume Breach ✅
- C) Published 2019 — Never Authenticate,
     Always Authorize, Monitor Continuously
- D) Published 2021 — Identity First,
     Network Second, Data Always Protected

> **Explanation:**
> - ✅ **B — NIST SP 800-207, August 2020:**
>   NIST SP 800-207 was published in **August
>   2020**. It defines three core Zero Trust
>   principles:
>   (1) **Verify Explicitly** — authenticate
>   and authorize based on all available data.
>   (2) **Use Least Privilege Access** — limit
>   access with JIT, JEA.
>   (3) **Assume Breach** — minimize blast
>   radius, microsegment, monitor everything.
>   These three principles are directly from
>   the NIST and Microsoft Zero Trust framework.
> - ❌ **A:** 2018 is incorrect — NIST SP 800-207
>   was published in 2020. "Block All Traffic"
>   and "Encrypt All Data" are not the three
>   Zero Trust principles — they mischaracterize
>   what Zero Trust means.
> - ❌ **C:** 2019 is incorrect. "Never
>   Authenticate, Always Authorize" contradicts
>   Zero Trust — which requires strong
>   authentication. The correct principle is
>   "Verify Explicitly" which means always
>   authenticate AND authorize.
> - ❌ **D:** 2021 is incorrect. "Identity First,
>   Network Second, Data Always Protected"
>   describes Zero Trust pillars (which are
>   implementation areas) — not the three core
>   principles from SP 800-207.

---

**Q22. In NIST Zero Trust Architecture, which
component makes the ACCESS DECISION (grant or
deny) and which component ENFORCES that
decision?**

- A) Policy Enforcement Point (PEP) decides;
     Policy Decision Point (PDP) enforces
- B) Policy Decision Point (PDP) decides;
     Policy Enforcement Point (PEP) enforces ✅
- C) Policy Engine (PE) decides;
     Policy Administrator (PA) enforces
- D) Trust Algorithm (TA) decides;
     Identity Provider (IdP) enforces

> **Explanation:**
> - ✅ **B — PDP decides, PEP enforces:** In NIST
>   SP 800-207 Zero Trust Architecture:
>   **PDP (Policy Decision Point)** — evaluates
>   the access request against all available
>   signals (identity, device health, context,
>   threat intelligence) and produces a
>   decision: grant, deny, or step-up auth.
>   **PEP (Policy Enforcement Point)** — receives
>   the PDP's decision and ENFORCES it — allowing
>   or blocking the network traffic/connection
>   to the requested resource.
> - ❌ **A:** This completely inverts the roles.
>   PEP enforces — it does NOT decide. PDP
>   decides — it does NOT enforce. Swapping
>   these is the most common mistake with
>   Zero Trust component terminology.
> - ❌ **C:** Policy Engine (PE) and Policy
>   Administrator (PA) are also Zero Trust
>   components from NIST SP 800-207 — the PE
>   is the decision logic WITHIN the PDP, and
>   PA establishes/terminates communication
>   paths. But the question asks specifically
>   about the decision/enforcement pair —
>   that is PDP and PEP respectively.
> - ❌ **D:** The Trust Algorithm (TA) is the
>   scoring mechanism inside the PDP — not
>   a separate component that "decides." The
>   Identity Provider (IdP) provides identity
>   information to support decisions — it does
>   not enforce access decisions. PEP is the
>   enforcer.

---

## MCQs 23–25 — Extra Notes: NTLM, LDAP,
Microsegmentation

---

**Q23. NTLM is Microsoft's legacy authentication
protocol. Which attack specifically exploits
stolen NTLM hashes to authenticate as a
user WITHOUT knowing their actual password?**

- A) Kerberoasting — cracking service account
     passwords from Kerberos tickets
- B) Golden Ticket — forging Kerberos TGTs
     using the KRBTGT hash
- C) Pass-the-Hash (PtH) — using the stolen
     NTLM hash directly to authenticate ✅
- D) AS-REP Roasting — obtaining hashes from
     accounts with pre-auth disabled

> **Explanation:**
> - ✅ **C — Pass-the-Hash:** In NTLM
>   authentication, the actual password is
>   never used directly — an MD4/HMAC-MD5
>   hash of the password is used in the
>   challenge-response. **Pass-the-Hash (PtH)**
>   exploits this: an attacker who steals the
>   NTLM hash (from memory using tools like
>   Mimikatz) can use that hash directly in
>   NTLM authentication — without ever knowing
>   or cracking the actual password.
> - ❌ **A:** Kerberoasting is a Kerberos attack —
>   it requests service tickets for service
>   accounts and cracks the ticket's encryption
>   offline to recover the service account
>   password. It targets Kerberos — not NTLM
>   — and involves actual password cracking
>   (not hash reuse).
> - ❌ **B:** Golden Ticket is also a Kerberos
>   attack — an attacker with the KRBTGT
>   account's NTLM hash can forge ANY Kerberos
>   TGT. While it uses an NTLM hash (KRBTGT),
>   it is a Kerberos attack — not an NTLM
>   authentication attack. The question asks
>   about NTLM protocol exploitation.
> - ❌ **D:** AS-REP Roasting targets Kerberos —
>   specifically user accounts with
>   pre-authentication disabled. The KDC
>   returns an AS-REP encrypted with the
>   user's password hash — attackers crack
>   this offline. This is a Kerberos attack,
>   not an NTLM attack.

---

**Q24. What is the relationship between LDAP
and Microsoft Active Directory?**

- A) LDAP and Active Directory are competing
     standards — organizations must choose
     one or the other
- B) Active Directory IS the LDAP standard —
     Microsoft wrote the RFC for LDAP
- C) Active Directory is Microsoft's directory
     service that implements LDAP as its
     access protocol — LDAP is the open
     standard; AD uses it ✅
- D) LDAP is a security layer added on top
     of Active Directory to protect
     authentication requests

> **Explanation:**
> - ✅ **C — AD implements LDAP:** LDAP
>   (Lightweight Directory Access Protocol,
>   RFC 4511) is an open internet standard
>   for accessing directory services. Microsoft
>   **Active Directory** is Microsoft's
>   implementation of a directory service that
>   uses LDAP as its primary access protocol.
>   When an application performs an LDAP BIND
>   to `ldap://dc.company.com`, it is talking
>   to Active Directory via the LDAP protocol.
>   AD also adds Kerberos authentication, Group
>   Policy, DNS, and other Windows-specific
>   services on top of basic LDAP.
> - ❌ **A:** LDAP and Active Directory are not
>   competing — AD USES LDAP. They are not
>   alternatives to choose between; they work
>   together. Many organizations use AD as their
>   LDAP-accessible directory.
> - ❌ **B:** Microsoft did not write the LDAP
>   RFC. LDAP was developed at the University
>   of Michigan and standardized by IETF. RFC
>   4511 is the current LDAPv3 standard.
>   Microsoft implemented it in Active Directory.
> - ❌ **D:** LDAP is not a security layer ON
>   TOP of Active Directory — LDAP is a
>   protocol that Active Directory IMPLEMENTS.
>   LDAPS (LDAP over TLS) adds security to
>   LDAP connections, but LDAP itself is not
>   a security layer.

---

**Q25. Microsegmentation is a key Zero Trust
network technique. What specific security
benefit does it provide?**

- A) It speeds up network traffic by creating
     dedicated segments for high-priority data
- B) It automatically encrypts all traffic
     between network segments using AES-256
- C) It limits lateral movement — if an
     attacker compromises one segment, they
     cannot freely access other segments ✅
- D) It creates backup network paths so
     that network failures do not disrupt
     authentication services

> **Explanation:**
> - ✅ **C — Limits lateral movement:**
>   Microsegmentation divides the network into
>   small, isolated zones with strict access
>   controls between them. If an attacker
>   compromises one server or workstation, they
>   cannot freely "pivot" (move laterally) to
>   attack other systems because the
>   microsegmentation controls block
>   unauthorized cross-segment traffic. This
>   **limits the blast radius** of any breach —
>   a core Zero Trust "Assume Breach" principle.
>   The Target breach (2013) succeeded partly
>   because the network was flat — no
>   microsegmentation to contain the attacker.
> - ❌ **A:** Microsegmentation is not about
>   traffic speed optimization. It is a security
>   control. Quality of Service (QoS) and
>   network traffic management tools handle
>   priority routing — not microsegmentation.
> - ❌ **B:** Microsegmentation controls WHICH
>   traffic is ALLOWED between segments — it
>   does not automatically encrypt that traffic.
>   Encryption within and between segments may
>   be added separately (mTLS, IPSec) — but
>   microsegmentation itself is access control,
>   not encryption.
> - ❌ **D:** Network redundancy and failover
>   are availability concerns handled by
>   technologies like HSRP, LACP, and redundant
>   links — not microsegmentation. Microsegmentation
>   is a security control for limiting attacker
>   movement — it does not improve network
>   resilience or availability.

---

## 📊 Answer Key — Quick Reference

| Q | Answer | Topic |
|---|--------|-------|
| 1 | B | PAP — sends password in plaintext |
| 2 | C | CHAP — MD5 challenge-response |
| 3 | B | EAP = framework, not a method |
| 4 | B | EAP-TLS = mutual auth with client certificates |
| 5 | D | PAP = only protocol sending cleartext password |
| 6 | B | MS-CHAPv2 broken in 2012 |
| 7 | C | 802.1X = Supplicant, Authenticator, Auth Server |
| 8 | B | EAPOL = EAP over LAN |
| 9 | C | WPA2-Enterprise = per-user creds; Personal = shared |
| 10 | C | LDAPS = port 636 |
| 11 | C | PEAP = no client certificate needed |
| 12 | C | Unauthorized state — EAPOL only |
| 13 | B | FIDO = Fast IDentity Online, 2012 |
| 14 | C | FIDO2 = WebAuthn (W3C) + CTAP2 (FIDO Alliance) |
| 15 | B | Phishing-resistant = RP_ID domain binding |
| 16 | C | Private key stays in authenticator — never leaves |
| 17 | B | FIDO2 enables passwordless; U2F was second factor only |
| 18 | B | Counter prevents cloned credential attacks |
| 19 | B | Zero Trust coined by Kindervag, Forrester, 2010 |
| 20 | C | Zero Trust = never trust, always verify |
| 21 | B | NIST SP 800-207 — August 2020 — 3 principles |
| 22 | B | PDP decides; PEP enforces |
| 23 | C | Pass-the-Hash = NTLM hash reuse attack |
| 24 | C | Active Directory implements LDAP protocol |
| 25 | C | Microsegmentation limits lateral movement |

---

## 📋 Topic Coverage Map

| Q | Concept Tested | Source |
|---|----------------|--------|
| 1 | PAP — plaintext password weakness | Core |
| 2 | CHAP — MD5 challenge-response mechanism | Core |
| 3 | EAP = framework not a method | Core |
| 4 | EAP-TLS requires client certificates | Core |
| 5 | PAP = cleartext password protocol | Core |
| 6 | MS-CHAPv2 broken 2012 | Core |
| 7 | 802.1X three roles — names | Core |
| 8 | EAPOL = EAP over LAN | Core |
| 9 | WPA2-Enterprise vs WPA2-Personal | Core |
| 10 | LDAPS port 636 | Core |
| 11 | PEAP = no client cert — most deployed | Core |
| 12 | 802.1X unauthorized state | Core |
| 13 | FIDO = Fast IDentity Online, founded 2012 | Core |
| 14 | FIDO2 = WebAuthn + CTAP2 | Core |
| 15 | FIDO2 phishing-resistant = RP_ID binding | Core |
| 16 | Private key never leaves authenticator | Core |
| 17 | FIDO2 adds passwordless over U2F | Core |
| 18 | FIDO2 counter = clone detection | Core |
| 19 | Kindervag, Forrester, 2010 | Core |
| 20 | Zero Trust = never trust, always verify | Core |
| 21 | NIST SP 800-207 = August 2020, 3 principles | Core |
| 22 | PDP decides; PEP enforces | Core |
| 23 | Pass-the-Hash = NTLM attack | Extra Notes |
| 24 | Active Directory implements LDAP | Extra Notes |
| 25 | Microsegmentation limits lateral movement | Extra Notes |

---