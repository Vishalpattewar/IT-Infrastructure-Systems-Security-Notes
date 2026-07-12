# MCQ Session 13 — Securing Websites and Emails:
SSL, TLS, PGP & S/MIME

## 📑 Table of Contents
- [Instructions](#instructions)
- [MCQs 1–6 — SSL and TLS Versions](#mcqs-16--ssl-and-tls-versions)
- [MCQs 7–12 — TLS Handshake and
  Cipher Suites](#mcqs-712--tls-handshake-and-cipher-suites)
- [MCQs 13–17 — PGP](#mcqs-1317--pgp)
- [MCQs 18–21 — S/MIME](#mcqs-1821--smime)
- [MCQs 22–25 — Extra Notes: HSTS, SNI,
  mTLS, DKIM](#mcqs-2225--extra-notes-hsts-sni-mtls-dkim)
- [Answer Key](#-answer-key--quick-reference)
- [Topic Coverage Map](#-topic-coverage-map)

---

## Instructions

- 25 MCQs — drawn from core syllabus AND
  📌 Extra Notes of Session 13
- Foundation + Fundamental + Basic Concepts ONLY
- 4 options per question
- ✅ marks the correct answer
- Full explanation after every question including
  why each wrong option is wrong
- Wrong options look reasonable to someone unprepared
- Correct answer is clear to someone with solid basics

---

## MCQs 1–6 — SSL and TLS Versions

---

**Q1. SSL was originally developed by which
company, and what protocol directly
replaced it?**

- A) Microsoft — replaced by IPSec
- B) Netscape — replaced by TLS
  (Transport Layer Security) ✅
- C) IBM — replaced by SSH
- D) RSA Security — replaced by HTTPS

> **Explanation:**
> - ✅ **B — Netscape / TLS:** SSL (Secure Sockets
>   Layer) was developed by **Netscape
>   Communications** in the early 1990s to
>   secure HTTP traffic. It was directly replaced
>   by **TLS (Transport Layer Security)** — which
>   is maintained by IETF as a standardized
>   successor. TLS 1.0 was essentially SSL 3.1.
> - ❌ **A:** Microsoft developed NTLM, Kerberos
>   extensions, and contributed to various protocols
>   — but NOT SSL. IPSec is a network-layer VPN
>   protocol — not a successor to SSL.
> - ❌ **C:** IBM developed technologies like
>   DES, and contributed to AES (MARS submission)
>   — but not SSL. SSH is a separate protocol
>   for secure remote shell access — not a
>   successor to SSL.
> - ❌ **D:** RSA Security developed PKCS standards
>   and RSA algorithm tools — not SSL. HTTPS is
>   HTTP over TLS — it is an application of TLS,
>   not a replacement protocol for SSL.

---

**Q2. The POODLE attack (2014) targeted which
protocol version and forced the industry to
deprecate it?**

- A) TLS 1.0 — due to predictable IV in
     CBC mode
- B) TLS 1.2 — due to weak GCM authentication
     tag truncation
- C) SSL 3.0 — due to a CBC padding oracle
     vulnerability ✅
- D) TLS 1.1 — due to insecure DHE key
     parameters

> **Explanation:**
> - ✅ **C — SSL 3.0 / CBC padding oracle:**
>   POODLE (Padding Oracle On Downgraded Legacy
>   Encryption) was discovered in 2014 and
>   targeted **SSL 3.0**. It exploited the
>   undefined/random padding in SSL 3.0's
>   CBC mode as a padding oracle — allowing
>   recovery of plaintext (session cookies)
>   with ~256 requests per byte. This forced
>   RFC 7568 (2015) which formally deprecated
>   SSL 3.0.
> - ❌ **A:** Predictable IV in TLS 1.0 CBC mode
>   is the **BEAST attack (2011)** — not POODLE.
>   BEAST targeted TLS 1.0; POODLE targeted
>   SSL 3.0. These are two different attacks
>   on two different protocol versions.
> - ❌ **B:** TLS 1.2 with GCM is considered
>   secure — there is no known practical attack
>   on TLS 1.2 AES-GCM. Weak GCM tag truncation
>   is a configuration issue, not what POODLE
>   exploited.
> - ❌ **D:** TLS 1.1 DHE weaknesses are
>   associated with the **Logjam attack (2015)**
>   — which targeted export-grade DH parameters.
>   Not POODLE.

---

**Q3. Which two TLS versions were formally
deprecated by RFC 8996 in 2021?**

- A) SSL 3.0 and TLS 1.0
- B) TLS 1.0 and TLS 1.1 ✅
- C) TLS 1.1 and TLS 1.2
- D) TLS 1.2 and TLS 1.3

> **Explanation:**
> - ✅ **B — TLS 1.0 and TLS 1.1:** RFC 8996
>   (published March 2021) formally deprecated
>   both **TLS 1.0** (RFC 2246, 1999) and
>   **TLS 1.1** (RFC 4346, 2006). Both versions
>   have known vulnerabilities (BEAST for TLS 1.0,
>   weak cipher suite support in both) and
>   are no longer accepted by major browsers.
>   The currently accepted minimum is TLS 1.2.
> - ❌ **A:** SSL 3.0 was deprecated by a
>   different RFC — **RFC 7568 (2015)** — not
>   RFC 8996. SSL 3.0 was deprecated six years
>   before RFC 8996 addressed TLS 1.0/1.1.
> - ❌ **C:** TLS 1.2 remains a **current
>   acceptable standard** — it was NOT deprecated
>   by RFC 8996. Deprecating TLS 1.2 would
>   break the vast majority of the internet.
> - ❌ **D:** TLS 1.3 is the **recommended
>   current standard** — it was published in
>   2018 and certainly has not been deprecated.
>   Deprecating the newest and most secure
>   version would make no sense.

---

**Q4. What RFC defines TLS 1.3, and in what
year was it published?**

- A) RFC 5246 — published in 2008
- B) RFC 4346 — published in 2006
- C) RFC 2246 — published in 1999
- D) RFC 8446 — published in 2018 ✅

> **Explanation:**
> - ✅ **D — RFC 8446, 2018:** TLS 1.3 is
>   defined in **RFC 8446**, published in
>   **August 2018**. It introduced the 1-RTT
>   handshake, mandatory PFS (ECDHE only),
>   AEAD-only cipher suites, encrypted
>   certificates in the handshake, and removed
>   all legacy and insecure features.
> - ❌ **A — RFC 5246, 2008:** This defines
>   **TLS 1.2** — the previous current standard.
>   RFC 5246 was published in 2008. TLS 1.2
>   and TLS 1.3 are different versions with
>   different RFC numbers.
> - ❌ **B — RFC 4346, 2006:** This defines
>   **TLS 1.1** — which is now deprecated
>   (RFC 8996, 2021). Not TLS 1.3.
> - ❌ **C — RFC 2246, 1999:** This defines
>   **TLS 1.0** — the first version of TLS
>   (essentially SSL 3.1), also deprecated.
>   Not TLS 1.3.

---

**Q5. What is HTTPS and on which port does
it typically operate?**

- A) HTTP with additional headers for
     security — port 8080
- B) HTTP transported over a TLS connection
     — port 443 ✅
- C) An entirely different protocol from
     HTTP — port 80
- D) HTTP with Base64 encoding of all data
     — port 8443

> **Explanation:**
> - ✅ **B — HTTP over TLS, port 443:** HTTPS
>   is simply standard HTTP transported over
>   a TLS-encrypted connection. TLS handles
>   the encryption, integrity, and server
>   authentication — HTTP carries the actual
>   web content above TLS. The standard port
>   for HTTPS is **443**. Port 80 is for plain
>   HTTP.
> - ❌ **A:** HTTPS is not HTTP with additional
>   headers — it is HTTP over a completely
>   different transport layer (TLS). Port 8080
>   is an alternative HTTP development port —
>   not HTTPS.
> - ❌ **C:** HTTPS uses the same HTTP protocol
>   (same request/response structure, same
>   methods GET/POST etc.) — just with TLS
>   underneath. Port 80 is for plain HTTP,
>   not HTTPS.
> - ❌ **D:** Base64 encoding is not HTTPS.
>   Base64 provides no security — it is just
>   an encoding format. Port 8443 is sometimes
>   used as an alternative HTTPS port for
>   development, but the standard port is 443.

---

**Q6. All SSL versions are deprecated and
broken. Which is the MINIMUM TLS version
that is currently acceptable for production
HTTPS deployments?**

- A) TLS 1.0 — it uses AES which is still
     secure
- B) TLS 1.1 — it fixed the BEAST
     vulnerability from TLS 1.0
- C) TLS 1.2 ✅
- D) Only TLS 1.3 is acceptable — TLS 1.2
     must not be used

> **Explanation:**
> - ✅ **C — TLS 1.2:** TLS 1.2 is the current
>   minimum acceptable version. TLS 1.0 and
>   TLS 1.1 were deprecated by RFC 8996 (2021)
>   and are no longer accepted by major browsers.
>   TLS 1.2 with strong cipher suites (ECDHE +
>   AES-GCM) remains secure and widely deployed.
> - ❌ **A:** TLS 1.0 was deprecated by RFC 8996
>   and is no longer acceptable in production.
>   AES being secure does not save TLS 1.0 —
>   the protocol itself has vulnerabilities
>   (BEAST attack on CBC mode, weak cipher
>   support, IV predictability).
> - ❌ **B:** TLS 1.1 was also deprecated by
>   RFC 8996 alongside TLS 1.0. While it fixed
>   the BEAST predictable IV issue, TLS 1.1
>   still supports weak cipher suites and is
>   not acceptable in production environments.
> - ❌ **D:** TLS 1.2 IS still acceptable and
>   widely deployed — billions of connections
>   still use TLS 1.2 daily. TLS 1.3 is
>   preferred and recommended but TLS 1.2 is
>   not prohibited.

---

## MCQs 7–12 — TLS Handshake and
Cipher Suites

---

**Q7. How many round-trips (RTT) does the
TLS 1.3 handshake require compared to
TLS 1.2?**

- A) TLS 1.3 requires 2 RTT — same as TLS 1.2
- B) TLS 1.3 requires 3 RTT — more than TLS
     1.2 because it exchanges more parameters
- C) TLS 1.2 requires 2 RTT — TLS 1.3
     requires 1 RTT ✅
- D) TLS 1.2 requires 1 RTT — TLS 1.3
     requires 0 RTT because it always resumes

> **Explanation:**
> - ✅ **C — TLS 1.2 = 2 RTT, TLS 1.3 = 1 RTT:**
>   TLS 1.2 handshake requires **2 full round
>   trips** before application data can flow.
>   TLS 1.3 reduces this to **1 RTT** because
>   the client includes its ECDHE key share in
>   the ClientHello — the server can immediately
>   respond with its key share AND the encrypted
>   certificate. This halves connection setup
>   latency — critical for performance on
>   high-latency networks.
> - ❌ **A:** TLS 1.3 does NOT require 2 RTT
>   — reducing to 1 RTT is one of its primary
>   design goals. Both being 2 RTT would mean
>   TLS 1.3 offers no performance improvement.
> - ❌ **B:** TLS 1.3 requires FEWER round
>   trips than TLS 1.2 — not more. The
>   additional parameters in TLS 1.3
>   (ECDHE key shares in ClientHello) are
>   what ENABLE the 1-RTT reduction.
> - ❌ **D:** TLS 1.2 requires 2 RTT for a
>   full handshake. TLS 1.3 supports 0-RTT
>   only for session RESUMPTION (with a
>   pre-shared key from a previous session)
>   — not for new connections. A brand new
>   TLS 1.3 connection requires 1 RTT.

---

**Q8. TLS 1.3 made Perfect Forward Secrecy
(PFS) mandatory. What does this mean in
practice for TLS 1.3?**

- A) TLS 1.3 encrypts session keys with a
     master key that changes every 24 hours
- B) TLS 1.3 only allows ECDHE for key exchange
     — static RSA and static DH key exchange
     were removed ✅
- C) TLS 1.3 generates new certificates for
     every session automatically
- D) TLS 1.3 uses two different encryption
     keys — one for each direction of traffic

> **Explanation:**
> - ✅ **B — ECDHE only, static RSA removed:**
>   PFS in TLS 1.3 is enforced by removing ALL
>   non-PFS key exchange methods. Static RSA
>   key transport (where the client encrypts
>   the pre-master secret with the server's
>   RSA public key) provides no PFS — if the
>   RSA private key is later compromised, all
>   past sessions can be decrypted. TLS 1.3
>   mandates ECDHE (ephemeral key pairs per
>   session) — past sessions remain secure
>   even if the long-term key is later stolen.
> - ❌ **A:** Master keys rotating every 24 hours
>   is a key rotation policy — not TLS PFS.
>   PFS means each session's key is independent
>   and ephemeral — not that a master key
>   periodically rotates.
> - ❌ **C:** TLS 1.3 does not automatically
>   generate new certificates per session —
>   certificates are long-lived (up to 398
>   days). The EPHEMERAL component is the
>   ECDHE key exchange, not the certificate.
> - ❌ **D:** Using separate keys for each
>   traffic direction is standard in all TLS
>   versions (client write key vs server
>   write key in TLS 1.2). This has nothing
>   to do with PFS specifically.

---

**Q9. TLS 1.3 restricts cipher suites to only
5 options — all using AEAD. Which of the
following is a valid TLS 1.3 cipher suite?**

- A) TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
- B) TLS_RSA_WITH_AES_256_GCM_SHA384
- C) TLS_AES_128_GCM_SHA256 ✅
- D) TLS_DHE_RSA_WITH_AES_256_CBC_SHA

> **Explanation:**
> - ✅ **C — TLS_AES_128_GCM_SHA256:**
>   This is one of the 5 valid TLS 1.3 cipher
>   suites. Notice the format: no key exchange
>   algorithm and no authentication algorithm
>   in the name — because TLS 1.3 always uses
>   ECDHE for key exchange (so it is not
>   negotiated as part of the cipher suite).
>   The three components are: cipher (AES_128),
>   mode (GCM — an AEAD mode), and hash for
>   HKDF (SHA256).
> - ❌ **A:** This format
>   `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
>   is a **TLS 1.2** cipher suite format —
>   it includes key exchange (ECDHE), auth
>   (RSA), and uses CBC mode. TLS 1.3 removed
>   CBC cipher suites and does not include
>   key exchange in the cipher suite name.
> - ❌ **B:** `TLS_RSA_WITH_AES_256_GCM_SHA384`
>   is a **TLS 1.2** cipher suite using static
>   RSA key exchange — which was explicitly
>   removed from TLS 1.3 because it provides
>   no PFS. The `RSA_WITH` prefix identifies
>   it as a TLS 1.2-style name.
> - ❌ **D:** `TLS_DHE_RSA_WITH_AES_256_CBC_SHA`
>   is a **TLS 1.2** cipher suite using DHE
>   (classic Diffie-Hellman) and CBC mode —
>   both removed from TLS 1.3. The `_WITH_`
>   format and CBC mode immediately identify
>   this as pre-TLS 1.3.

---

**Q10. In a TLS 1.2 cipher suite name like
`TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256`,
what does the ECDHE component specify?**

- A) The algorithm used to sign the server
     certificate
- B) The hash function used for MAC
     computation
- C) The key exchange algorithm used to
     establish the session keys ✅
- D) The symmetric encryption algorithm
     for protecting application data

> **Explanation:**
> - ✅ **C — Key exchange algorithm:** In a
>   TLS 1.2 cipher suite:
>   `TLS_[KEY EXCHANGE]_[AUTH]_WITH_[CIPHER]_[MAC]`
>   **ECDHE** = Elliptic Curve Diffie-Hellman
>   Ephemeral — the key exchange algorithm
>   that establishes the session's pre-master
>   secret. ECDHE provides PFS because fresh
>   key pairs are generated per session.
> - ❌ **A:** The authentication algorithm
>   (signing the server certificate) is the
>   second component — **RSA** in this cipher
>   suite. ECDHE is the key exchange, not the
>   authentication.
> - ❌ **B:** The hash function for MAC/PRF is
>   the LAST component — **SHA256** in this
>   cipher suite. ECDHE has no relationship
>   to hash functions.
> - ❌ **D:** The symmetric encryption algorithm
>   is after `_WITH_` — **AES_128_GCM** in
>   this cipher suite. ECDHE is the key
>   exchange — AES is the data encryption.

---

**Q11. During the TLS 1.2 handshake, the
server sends its X.509 certificate to the
client. What does the client use this
certificate for?**

- A) To encrypt the application data
     sent back to the server
- B) To verify the server's identity and
     obtain the server's public key for
     the key exchange ✅
- C) To decrypt the server's random nonce
     included in the ServerHello message
- D) To generate the session keys
     independently without server involvement

> **Explanation:**
> - ✅ **B — Verify server identity + public
>   key:** The server's X.509 certificate
>   serves two purposes in the TLS handshake:
>   (1) **Authentication** — the client
>   validates the certificate chain, checks
>   validity period, revocation, and hostname
>   match — confirming the server is who it
>   claims to be. (2) **Key material** —
>   the server's public key from the cert
>   is used in RSA key exchange (to encrypt
>   the pre-master secret) or to verify the
>   ServerKeyExchange signature in DHE/ECDHE.
> - ❌ **A:** Application data is encrypted
>   using the **symmetric session keys**
>   (AES) derived during the handshake —
>   not the server's certificate public key
>   directly. Using RSA to encrypt all
>   application data would be extremely slow.
> - ❌ **C:** The server's random nonce
>   (ServerRandom) is sent in plaintext in
>   the ServerHello — it does not need to be
>   decrypted. Nothing in TLS is encrypted
>   at the ServerRandom stage yet.
> - ❌ **D:** Session keys are derived
>   collaboratively using the negotiated
>   key exchange algorithm — they are NOT
>   generated independently by the client
>   alone. Both the ClientRandom and
>   ServerRandom contribute to key derivation.

---

**Q12. What is a TLS cipher suite?**

- A) A file that stores TLS session keys
     after the handshake completes
- B) A named combination of algorithms
     specifying key exchange, authentication,
     encryption, and integrity for a TLS
     session ✅
- C) A list of trusted Certificate Authorities
     pre-installed in the browser
- D) A configuration file that defines
     which TLS versions a server accepts

> **Explanation:**
> - ✅ **B — Named algorithm combination:**
>   A TLS cipher suite is a standardized name
>   that specifies the complete set of
>   cryptographic algorithms for a TLS
>   connection: how keys are exchanged (ECDHE,
>   RSA), how the server authenticates (RSA,
>   ECDSA), how data is encrypted (AES, ChaCha20),
>   and how integrity is verified (GCM, SHA256).
>   Both client and server advertise their
>   supported suites and negotiate the strongest
>   mutually supported one.
> - ❌ **A:** TLS session keys are stored in
>   memory by the TLS library — not in a "cipher
>   suite file." Cipher suites are algorithm
>   specifications — not key storage mechanisms.
> - ❌ **C:** A list of trusted CAs is a **trust
>   store** (covered in Sessions 07/08) — not
>   a cipher suite. Trust stores and cipher
>   suites serve entirely different purposes
>   in TLS.
> - ❌ **D:** Supported TLS versions are
>   configured separately from cipher suites.
>   A cipher suite specifies algorithms for a
>   specific session — not which protocol
>   versions are enabled.

---

## MCQs 13–17 — PGP

---

**Q13. PGP (Pretty Good Privacy) was created
by which person, and in what year?**

- A) Bruce Schneier — 1993
- B) Phil Zimmermann — 1991 ✅
- C) Whitfield Diffie — 1976
- D) Ron Rivest — 1992

> **Explanation:**
> - ✅ **B — Phil Zimmermann, 1991:**
>   **Pretty Good Privacy (PGP)** was created
>   by **Phil Zimmermann** in **1991**. He
>   released it for free on the internet —
>   making strong encryption accessible to
>   the public for the first time. The US
>   government investigated him for 3 years
>   under Arms Export Control Act regulations
>   before dropping the case in 1996.
> - ❌ **A:** Bruce Schneier created Blowfish
>   (1993), Twofish (AES finalist), and Skein
>   — not PGP. He is a prominent security
>   technologist but did not create PGP.
> - ❌ **C:** Whitfield Diffie (with Martin
>   Hellman) published the Diffie-Hellman key
>   exchange in **1976** — not PGP. DH and
>   PGP are different things; DH is used
>   WITHIN some PGP implementations.
> - ❌ **D:** Ron Rivest co-created RSA (1978)
>   and designed MD5 and RC ciphers — not PGP.
>   1992 is when MD5 was published by Rivest —
>   not when PGP was created.

---

**Q14. PGP uses hybrid encryption for
confidentiality. What is the correct
description of how PGP encryption works?**

- A) PGP encrypts the entire message with
     the recipient's RSA public key directly
- B) PGP generates a random session key,
     encrypts the message with it (AES),
     then encrypts the session key with the
     recipient's public key ✅
- C) PGP derives a key from the recipient's
     email address using PBKDF2 then encrypts
     the message with AES
- D) PGP compresses the message then signs
     it with the sender's private key — no
     encryption is applied

> **Explanation:**
> - ✅ **B — Hybrid encryption:** PGP uses
>   the standard hybrid encryption pattern:
>   (1) Generate a random symmetric session
>   key (e.g., AES-256).
>   (2) Encrypt the message with this fast
>   symmetric key.
>   (3) Encrypt the session key with the
>   recipient's RSA/ECC **public key**.
>   (4) Send both together.
>   The recipient uses their private key to
>   decrypt the session key, then uses the
>   session key to decrypt the message.
>   Pure RSA encryption of large data is
>   impractical — hybrid solves this.
> - ❌ **A:** Encrypting the entire message
>   with RSA directly is impractical —
>   RSA can only encrypt data smaller than
>   its key size (≈ 256 bytes for RSA-2048).
>   A full email could be megabytes. This
>   is why hybrid encryption (AES for data,
>   RSA for key) exists.
> - ❌ **C:** PGP does not derive keys from
>   email addresses. The session key is
>   randomly generated and then protected
>   with the recipient's actual public key
>   from their PGP key pair. Email addresses
>   are used for key lookup — not key
>   derivation.
> - ❌ **D:** This describes only signing
>   (not encryption). PGP can compress before
>   signing — but if encryption is requested,
>   the symmetric session key encrypts the
>   (possibly signed and compressed) data.
>   Compression alone provides no confidentiality.

---

**Q15. In PGP's Web of Trust, how many
FULL trust signatures from trusted parties
are needed to consider a key VALID?**

- A) 3 full trust signatures
- B) 2 full trust signatures
- C) 5 full trust signatures
- D) 1 full trust signature ✅

> **Explanation:**
> - ✅ **D — 1 full trust:** In PGP's Web of
>   Trust, **one person with FULL trust** signing
>   a key is sufficient to consider that key
>   valid. Alternatively, **three people with
>   MARGINAL trust** signing a key is also
>   sufficient. This is the standard PGP
>   validity formula:
>   1 full trust OR 3 marginal trusts = valid.
> - ❌ **A — 3 full trust:** Three signatures
>   are needed for MARGINAL trust signers —
>   not for full trust signers. One full trust
>   signer is sufficient. Requiring 3 full
>   trust signatures would make PGP trust
>   excessively difficult to establish.
> - ❌ **B — 2 full trust:** Two full trust
>   signatures is not the threshold defined
>   in PGP's trust model. The model is binary
>   for full trust: ONE full trust signer
>   suffices.
> - ❌ **C — 5 full trust:** This is entirely
>   fabricated. The PGP Web of Trust thresholds
>   are 1 (full) or 3 (marginal) — not 5.

---

**Q16. What is OpenPGP and how does it
relate to PGP and GPG?**

- A) OpenPGP is a paid enterprise version
     of PGP — GPG is the free version
- B) OpenPGP (RFC 4880) is the open standard
     based on PGP — GPG is a free
     open-source implementation of OpenPGP ✅
- C) OpenPGP is a government-regulated
     version of PGP — GPG is the commercial
     version by RSA Security
- D) OpenPGP is the same as S/MIME — GPG
     is the command-line tool for S/MIME

> **Explanation:**
> - ✅ **B — Standard + Implementation:**
>   **OpenPGP** (RFC 4880, 2007) is the open
>   STANDARD based on Phil Zimmermann's
>   original PGP — it defines the message
>   formats, key formats, algorithms, and
>   trust model in an interoperable way.
>   **GPG (GnuPG — GNU Privacy Guard)** is
>   the FREE, open-source IMPLEMENTATION of
>   the OpenPGP standard — the tool you
>   actually run. Multiple implementations
>   can follow the same OpenPGP standard
>   and interoperate.
> - ❌ **A:** OpenPGP is not a paid version —
>   it is an open standard (RFC). The "Open"
>   in OpenPGP means open/public standard —
>   not a product tier. GPG is free precisely
>   because the standard is open.
> - ❌ **C:** OpenPGP has no government
>   regulation component — it is an IETF
>   standard. RSA Security (the company)
>   created PKCS standards and commercial
>   products — not GPG. GPG was created by
>   Werner Koch as a free software project.
> - ❌ **D:** OpenPGP and S/MIME are DIFFERENT
>   and competing email security standards
>   with different formats and trust models.
>   GPG implements OpenPGP — not S/MIME.
>   This option confuses two distinct
>   email security approaches.

---

**Q17. When PGP is used to BOTH sign AND
encrypt a message, what is the correct
order of operations?**

- A) Encrypt first, then sign the ciphertext
     with the sender's private key
- B) Sign first (with sender's private key),
     then encrypt the signed message
     with the recipient's public key ✅
- C) Encrypt first, then hash the message
     for integrity — signature is not needed
- D) Sign and encrypt simultaneously using
     the same key for both operations

> **Explanation:**
> - ✅ **B — Sign then Encrypt:** The correct
>   order is:
>   (1) **Sign** the plaintext message with
>   the sender's PRIVATE key.
>   (2) **Encrypt** the (message + signature)
>   bundle using hybrid encryption with the
>   recipient's PUBLIC key.
>   This ensures the signature is inside the
>   encrypted envelope — proving the signer
>   created the specific plaintext, not just
>   the ciphertext.
> - ❌ **A:** Signing the ciphertext (encrypt
>   first) would be "Encrypt then Sign" —
>   a known security weakness. Anyone could
>   strip the outer signature and re-sign
>   the ciphertext with their own key —
>   falsely claiming authorship of the
>   ciphertext. Signing the PLAINTEXT (sign
>   first) prevents this attack.
> - ❌ **C:** Encrypting and only hashing
>   provides no authentication — anyone
>   can compute a hash. A digital SIGNATURE
>   (hash signed with private key) is what
>   proves identity. Hashing alone does not
>   prove who created the message.
> - ❌ **D:** PGP uses separate keys for
>   signing (asymmetric private key) and
>   encryption (session key for data,
>   recipient's public key for key wrapping).
>   They are NEVER the same key — using the
>   same key for both purposes would be a
>   serious design flaw.

---

## MCQs 18–21 — S/MIME

---

**Q18. What is S/MIME and which trust model
does it use?**

- A) S/MIME is a PGP-based email standard
     using a Web of Trust for key verification
- B) S/MIME is a CA-based email signing
     and encryption standard using a
     hierarchical PKI trust model ✅
- C) S/MIME is a server-side email scanning
     protocol that checks for malware
- D) S/MIME is a DNS-based mechanism for
     verifying email sender domains

> **Explanation:**
> - ✅ **B — CA-based / Hierarchical PKI:**
>   S/MIME (Secure/Multipurpose Internet Mail
>   Extensions, RFC 8551) is a standard for
>   **signing and encrypting email content**
>   that uses the **hierarchical PKI trust
>   model** — the same CA-based system used
>   in TLS. Users obtain X.509 certificates
>   from a trusted CA (with emailProtection
>   EKU) to sign and encrypt email. This
>   integrates naturally with enterprise PKI
>   (Active Directory, Outlook).
> - ❌ **A:** PGP-based email uses the Web of
>   Trust — a decentralized model. S/MIME
>   specifically uses the hierarchical CA
>   model — NOT Web of Trust. Confusing S/MIME
>   with PGP's trust model is a very common
>   exam trap.
> - ❌ **C:** S/MIME is about message-level
>   cryptographic security — not server-side
>   malware scanning. Anti-malware email
>   scanning is a completely different function
>   performed by email gateways (Secure Email
>   Gateway — SEG).
> - ❌ **D:** DNS-based email domain verification
>   describes SPF, DKIM, and DMARC — completely
>   different mechanisms that operate at the
>   mail server level. S/MIME operates at the
>   message content level (end-to-end).

---

**Q19. What X.509 certificate extension
is specifically required for an S/MIME
signing and encryption certificate?**

- A) serverAuth — for TLS server authentication
- B) codeSigning — for software code signing
- C) emailProtection EKU ✅
- D) timeStamping — for trusted timestamp
     services

> **Explanation:**
> - ✅ **C — emailProtection EKU:** An S/MIME
>   certificate must have the Extended Key
>   Usage (EKU) value **emailProtection**
>   (OID: 1.3.6.1.5.5.7.3.4). This EKU
>   specifically authorizes the certificate
>   for securing email — signing and
>   encrypting email messages. Email clients
>   (Outlook, Apple Mail) check for this
>   EKU when selecting an S/MIME certificate.
> - ❌ **A:** serverAuth EKU is for TLS server
>   certificates — it authorizes a certificate
>   to authenticate a web server to browsers.
>   Using a serverAuth cert for S/MIME would
>   be incorrect — email clients would reject
>   it as not having the right EKU.
> - ❌ **B:** codeSigning EKU is for software
>   code signing certificates — used by
>   developers to sign executables and scripts.
>   Completely different purpose from email
>   security.
> - ❌ **D:** timeStamping EKU is for TSA
>   (Time Stamp Authority) certificates —
>   authorizing the certificate to sign
>   RFC 3161 Time Stamp Tokens. Unrelated
>   to email signing or encryption.

---

**Q20. S/MIME and PGP both secure email.
What is the PRIMARY difference in their
approach to trust?**

- A) S/MIME uses stronger encryption
     algorithms than PGP
- B) PGP works only on Windows — S/MIME
     works cross-platform
- C) S/MIME uses hierarchical PKI (CA issues
     certificates); PGP uses Web of Trust
     (users vouch for each other's keys) ✅
- D) S/MIME encrypts attachments only —
     PGP encrypts both message body and
     attachments

> **Explanation:**
> - ✅ **C — Hierarchical PKI vs Web of Trust:**
>   This is the fundamental distinction:
>   **S/MIME** = CA issues X.509 certificate
>   → automatic trust via CA chain → no manual
>   key verification needed.
>   **PGP** = User generates own key pair →
>   other users sign/vouch for the key →
>   trust built through Web of Trust network.
>   S/MIME is simpler for enterprise (integrates
>   with AD/CA); PGP is free and privacy-focused.
> - ❌ **A:** Both S/MIME and PGP support modern
>   strong algorithms (AES-256, SHA-256,
>   RSA/ECC). The encryption algorithm strength
>   is not the primary distinguishing factor
>   — the TRUST MODEL is.
> - ❌ **B:** Both S/MIME and PGP work
>   cross-platform. GPG (PGP implementation)
>   runs on Linux, macOS, and Windows. S/MIME
>   is supported on Outlook (Windows), Apple
>   Mail (macOS/iOS), and Thunderbird (all
>   platforms). Platform support is not
>   the distinguishing factor.
> - ❌ **D:** Both S/MIME and PGP can encrypt
>   the entire email including the body and
>   attachments. S/MIME does not exclusively
>   encrypt attachments — this is a fabricated
>   distinction with no technical basis.

---

**Q21. Which file format is used by S/MIME
for its signed and encrypted message
structures?**

- A) OpenPGP format (RFC 4880)
- B) PKCS#7 / CMS (Cryptographic Message
     Syntax) ✅
- C) JWT (JSON Web Token)
- D) SAML Assertion (XML format)

> **Explanation:**
> - ✅ **B — PKCS#7 / CMS:** S/MIME is built
>   on top of **PKCS#7** — now updated to
>   **CMS (Cryptographic Message Syntax, RFC
>   5652)**. CMS defines the ASN.1 DER-encoded
>   data structures for SignedData, EnvelopedData,
>   SignedAndEnvelopedData etc. S/MIME email
>   attachments have extensions like `.p7s`
>   (detached signature), `.p7m` (encrypted or
>   opaque signed), and `.p7c` (certificate).
> - ❌ **A:** OpenPGP format (RFC 4880) is used
>   by **PGP/GPG** — not S/MIME. The two
>   standards use entirely different message
>   formats: OpenPGP (PGP) vs PKCS#7/CMS
>   (S/MIME). This is one of the key technical
>   differences between them.
> - ❌ **C:** JWT (JSON Web Token, RFC 7519)
>   is used for web authentication tokens
>   in OAuth/OIDC — not for email encryption
>   or signing. S/MIME predates JWT by decades
>   and uses binary ASN.1 encoding, not JSON.
> - ❌ **D:** SAML Assertions are XML-formatted
>   tokens used in enterprise SSO (Single
>   Sign-On) — not email security. S/MIME
>   uses CMS (ASN.1 binary) — not XML.

---

## MCQs 22–25 — Extra Notes: HSTS, SNI,
mTLS, DKIM

---

**Q22. What does HSTS (HTTP Strict Transport
Security) do, and what specific attack
does it prevent?**

- A) HSTS compresses HTTP traffic to improve
     bandwidth — it prevents DDoS attacks
- B) HSTS tells browsers to ONLY connect
     to this site over HTTPS — preventing
     SSL stripping attacks that downgrade
     HTTPS to HTTP ✅
- C) HSTS encrypts HTTP headers with AES —
     preventing header injection attacks
- D) HSTS pins the server's certificate hash
     — preventing fraudulent certificate
     issuance

> **Explanation:**
> - ✅ **B — Forces HTTPS, prevents SSL
>   stripping:** HSTS is delivered as an HTTP
>   response header:
>   `Strict-Transport-Security: max-age=31536000`
>   Once a browser receives this header, it
>   will ONLY connect to that domain over
>   HTTPS for the specified duration — even
>   if the user types `http://` or clicks an
>   HTTP link. This prevents **SSL stripping
>   attacks** where a MITM attacker downgrades
>   the connection from HTTPS to HTTP.
> - ❌ **A:** HSTS has nothing to do with
>   compression or DDoS prevention. It is
>   a browser security policy mechanism —
>   it affects how the browser initiates
>   connections, not how data is compressed
>   or how servers handle load.
> - ❌ **C:** HSTS does not encrypt HTTP
>   headers with AES — TLS handles encryption.
>   Header injection attacks are prevented
>   by input validation, not HSTS. HSTS
>   forces protocol choice (HTTPS vs HTTP),
>   not header security.
> - ❌ **D:** Certificate hash pinning describes
>   **HTTP Public Key Pinning (HPKP)** — a
>   separate (now deprecated) mechanism.
>   HSTS is about protocol enforcement
>   (HTTPS only) — not certificate pinning.

---

**Q23. SNI (Server Name Indication) is a
TLS extension that solves a specific problem.
What is that problem?**

- A) SNI prevents eavesdroppers from reading
     encrypted TLS traffic
- B) SNI allows one IP address to host
     multiple HTTPS websites by telling
     the server which certificate to send ✅
- C) SNI verifies that the server's
     certificate was issued by a trusted CA
- D) SNI speeds up the TLS handshake by
     caching previously used session keys

> **Explanation:**
> - ✅ **B — Multiple HTTPS sites on one IP:**
>   Without SNI, a server receiving a TLS
>   connection on port 443 does not know
>   WHICH website the client wants — and
>   therefore does not know which certificate
>   to present — before the TLS handshake
>   begins. SNI solves this by having the
>   client include the target **hostname**
>   in the ClientHello message (before
>   encryption starts), allowing the server
>   to select and present the correct certificate
>   for that specific virtual host.
> - ❌ **A:** Preventing eavesdroppers from
>   reading TLS traffic is TLS's core purpose
>   — not SNI's specific function. In fact,
>   SNI has a **privacy concern** because the
>   hostname IS visible to eavesdroppers in
>   the ClientHello (ECH/ESNI was developed
>   to address this).
> - ❌ **C:** Certificate chain validation
>   against trusted CAs is performed by the
>   browser using the trust store — not by
>   SNI. SNI tells the server WHICH cert to
>   send; trust verification happens after
>   the cert is received.
> - ❌ **D:** Session key caching is TLS
>   session resumption (via session IDs or
>   PSK in TLS 1.3) — not SNI. SNI is about
>   virtual host selection, not performance
>   optimization.

---

**Q24. What is mTLS (Mutual TLS) and how
does it differ from standard TLS?**

- A) mTLS uses two separate TLS connections
     simultaneously — one for each direction
     of traffic
- B) mTLS requires BOTH the client AND the
     server to present X.509 certificates —
     while standard TLS only requires the
     server to present a certificate ✅
- C) mTLS uses twice the encryption strength
     of standard TLS — AES-512 instead of
     AES-256
- D) mTLS is an older version of TLS used
     only in legacy banking systems

> **Explanation:**
> - ✅ **B — Both sides authenticate:** In
>   standard TLS, only the **server** presents
>   a certificate (client verifies server
>   identity). In **mTLS (Mutual TLS)**,
>   BOTH parties present certificates —
>   the client also presents a certificate
>   that the server verifies. This is used
>   in Zero Trust architectures, service
>   mesh (Istio), API security, and anywhere
>   both sides need cryptographic identity
>   proof. EAP-TLS also implements mTLS
>   for Wi-Fi authentication.
> - ❌ **A:** mTLS is a single TLS connection
>   where both parties authenticate — not two
>   separate connections. Traffic direction
>   separation is a different concept (client
>   write key vs server write key in TLS
>   key schedule).
> - ❌ **C:** AES-512 does not exist — AES
>   has key sizes 128, 192, and 256 bits.
>   mTLS uses the same cipher suites as
>   standard TLS — the "mutual" refers to
>   authentication of both parties, not
>   doubled encryption strength.
> - ❌ **D:** mTLS is actively used in modern
>   Zero Trust architectures, service meshes
>   (Istio, Linkerd), and cloud-native
>   environments — it is not an obsolete
>   legacy protocol. In fact, mTLS adoption
>   is INCREASING as Zero Trust becomes
>   the dominant security model.

---

**Q25. DKIM (DomainKeys Identified Mail)
provides email authentication at the domain
level. How does DKIM work?**

- A) DKIM scans email content for known
     spam patterns and assigns a trust score
- B) DKIM publishes authorized IP addresses
     in DNS so receiving servers know which
     IPs can send email for a domain
- C) DKIM adds a digital signature to
     outgoing email using the domain's private
     key — the receiving server verifies using
     the domain's public key from DNS ✅
- D) DKIM requires all email between two
     domains to be encrypted with TLS before
     delivery

> **Explanation:**
> - ✅ **C — Domain private key signature:**
>   DKIM (RFC 6376) works by:
>   (1) The sending mail server signs the email
>   headers and body with the domain's PRIVATE
>   key (adds a `DKIM-Signature:` header).
>   (2) The public key is published in DNS as
>   a TXT record.
>   (3) The receiving server retrieves the
>   public key from DNS and verifies the
>   signature → confirms the email was not
>   modified and originated from the claimed
>   domain.
> - ❌ **A:** Spam content scanning describes
>   anti-spam/anti-malware email gateways
>   (using pattern matching, Bayesian filters).
>   DKIM is specifically about cryptographic
>   domain authentication — not spam pattern
>   detection.
> - ❌ **B:** Publishing authorized sending IP
>   addresses in DNS describes **SPF (Sender
>   Policy Framework)** — not DKIM. Both SPF
>   and DKIM use DNS records but serve different
>   purposes: SPF verifies the sending IP;
>   DKIM verifies message integrity via a
>   digital signature.
> - ❌ **D:** DKIM does not require TLS
>   encryption between mail servers — that
>   is handled by STARTTLS. DKIM operates
>   independently of transport encryption —
>   it is a message-level signature that
>   survives even if the transport is
>   unencrypted (though TLS is still
>   recommended for transport).

---

## 📊 Answer Key — Quick Reference

| Q | Answer | Topic |
|---|--------|-------|
| 1 | B | SSL developed by Netscape, replaced by TLS |
| 2 | C | POODLE = SSL 3.0 CBC padding oracle (2014) |
| 3 | B | RFC 8996 deprecated TLS 1.0 and TLS 1.1 |
| 4 | D | TLS 1.3 = RFC 8446, 2018 |
| 5 | B | HTTPS = HTTP over TLS, port 443 |
| 6 | C | TLS 1.2 = minimum acceptable version |
| 7 | C | TLS 1.2 = 2 RTT; TLS 1.3 = 1 RTT |
| 8 | B | TLS 1.3 PFS = ECDHE mandatory, static RSA removed |
| 9 | C | TLS_AES_128_GCM_SHA256 = valid TLS 1.3 suite |
| 10 | C | ECDHE = key exchange algorithm in cipher suite |
| 11 | B | Server cert = verify identity + get public key |
| 12 | B | Cipher suite = named algorithm combination |
| 13 | B | PGP = Phil Zimmermann, 1991 |
| 14 | B | PGP = hybrid encryption (AES + RSA) |
| 15 | D | PGP trust = 1 full OR 3 marginal |
| 16 | B | OpenPGP = RFC 4880; GPG = free implementation |
| 17 | B | PGP sign-then-encrypt convention |
| 18 | B | S/MIME = CA-based, hierarchical PKI |
| 19 | C | S/MIME certificate needs emailProtection EKU |
| 20 | C | S/MIME = CA hierarchy; PGP = Web of Trust |
| 21 | B | S/MIME uses PKCS#7 / CMS format |
| 22 | B | HSTS forces HTTPS — prevents SSL stripping |
| 23 | B | SNI = multiple HTTPS sites on one IP |
| 24 | B | mTLS = both client and server present certs |
| 25 | C | DKIM = domain private key signs email |

---

## 📋 Topic Coverage Map

| Q | Concept Tested | Source |
|---|----------------|--------|
| 1 | SSL origin — Netscape — replaced by TLS | Core |
| 2 | POODLE attack — SSL 3.0 — 2014 | Core |
| 3 | RFC 8996 deprecated TLS 1.0 and 1.1 | Core |
| 4 | TLS 1.3 = RFC 8446, 2018 | Core |
| 5 | HTTPS = HTTP over TLS, port 443 | Core |
| 6 | TLS 1.2 = current minimum standard | Core |
| 7 | TLS 1.2 = 2 RTT vs TLS 1.3 = 1 RTT | Core |
| 8 | TLS 1.3 mandates PFS — ECDHE only | Core |
| 9 | TLS 1.3 cipher suite format | Core |
| 10 | Cipher suite — ECDHE = key exchange | Core |
| 11 | Server certificate purpose in TLS handshake | Core |
| 12 | TLS cipher suite definition | Core |
| 13 | PGP — Phil Zimmermann, 1991 | Core |
| 14 | PGP hybrid encryption mechanism | Core |
| 15 | PGP Web of Trust — 1 full / 3 marginal | Core |
| 16 | OpenPGP (standard) vs GPG (implementation) | Core |
| 17 | PGP sign-then-encrypt order | Core |
| 18 | S/MIME trust model — CA hierarchy | Core |
| 19 | S/MIME emailProtection EKU requirement | Core |
| 20 | S/MIME vs PGP — trust model comparison | Core |
| 21 | S/MIME uses PKCS#7/CMS format | Core |
| 22 | HSTS — forces HTTPS, SSL stripping prevention | Extra Notes |
| 23 | SNI — multiple HTTPS sites on one IP | Extra Notes |
| 24 | mTLS — both sides authenticate | Extra Notes |
| 25 | DKIM — domain key email signing | Extra Notes |

---