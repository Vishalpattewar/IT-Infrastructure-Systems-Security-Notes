# MCQ Session 07 — PKI Fundamentals, Digital Signatures
& Digital Certificates

## 📑 Table of Contents
- [Instructions](#instructions)
- [MCQs 1–6 — PKI Fundamentals](#mcqs-16--pki-fundamentals)
- [MCQs 7–13 — Digital Signatures](#mcqs-713--digital-signatures)
- [MCQs 14–20 — Digital Certificates](#mcqs-1420--digital-certificates)
- [MCQs 21–25 — Extra Notes: Standards, Formats,
  Extensions](#mcqs-2125--extra-notes-standards-formats-extensions)
- [Answer Key](#-answer-key--quick-reference)
- [Topic Coverage Map](#-topic-coverage-map)

---

## Instructions

- 25 MCQs — drawn from core syllabus AND
  📌 Extra Notes of Session 07
- Foundation + Fundamental + Basic Concepts ONLY
- 4 options per question
- ✅ marks the correct answer
- Full explanation after every question including
  why each wrong option is wrong
- Wrong options look reasonable to someone unprepared
- Correct answer is clear to someone with solid basics

---

## MCQs 1–6 — PKI Fundamentals

---

**Q1. What is the fundamental problem that PKI
solves in public key cryptography?**

- A) PKI solves the problem of slow asymmetric
     encryption by distributing the workload
     across multiple servers
- B) PKI solves the problem of verifying that a
     public key genuinely belongs to the person
     or entity it claims to represent ✅
- C) PKI solves the problem of storing private
     keys securely on user devices
- D) PKI solves the problem of choosing the
     correct encryption algorithm for each
     communication

> **Explanation:**
> - ✅ **B:** The core problem PKI solves is the
>   **public key authentication problem** — without
>   PKI, anyone could publish a fake public key
>   claiming to belong to someone else, enabling
>   MITM attacks. PKI uses trusted Certificate
>   Authorities and digital certificates to bind
>   a public key to a verified identity.
> - ❌ **A:** PKI does not solve encryption speed —
>   the slow nature of asymmetric encryption is
>   addressed by hybrid encryption (combining
>   symmetric + asymmetric). PKI is about trust
>   and identity, not performance.
> - ❌ **C:** Private key storage is a key management
>   concern handled by HSMs and secure storage —
>   not by PKI itself. PKI manages public keys and
>   certificates, not private key storage.
> - ❌ **D:** Algorithm selection is a protocol
>   negotiation concern (e.g., TLS cipher suites) —
>   not what PKI addresses. PKI is specifically
>   about establishing trust in public keys.

---

**Q2. What is the role of a Certificate Authority
(CA) in a PKI?**

- A) To encrypt all communications between
     users on the network
- B) To store private keys for all users in a
     secure centralized database
- C) To issue and digitally sign digital
     certificates — binding a public key to
     a verified identity ✅
- D) To generate public and private key pairs
     for all users

> **Explanation:**
> - ✅ **C:** A CA is a trusted third party that
>   verifies an applicant's identity, then issues
>   a digital certificate that binds their public
>   key to that verified identity. The CA digitally
>   signs the certificate with its own private key —
>   this signature is what makes the certificate
>   trustworthy.
> - ❌ **A:** CAs do not encrypt communications —
>   encryption is done by the communicating parties
>   using keys from their certificates. A CA's
>   role is identity verification and certification.
> - ❌ **B:** CAs absolutely must NOT store users'
>   private keys — private keys must be kept
>   exclusively by their owners. If a CA stored
>   private keys, the entire security model would
>   collapse.
> - ❌ **D:** Key pair generation is the responsibility
>   of the end entity — the user or server generates
>   their own key pair and submits the public key
>   to the CA via a CSR. The CA never generates
>   keys for users.

---

**Q3. In a PKI hierarchy, what is the difference
between a Root CA and an Intermediate CA?**

- A) A Root CA issues certificates to end users —
     an Intermediate CA only issues certificates
     to other CAs
- B) A Root CA is self-signed and is the trust
     anchor — an Intermediate CA is signed by the
     Root CA and issues end-entity certificates ✅
- C) A Root CA uses RSA — an Intermediate CA uses
     ECC for better performance
- D) A Root CA is operated by governments — an
     Intermediate CA is operated by private companies

> **Explanation:**
> - ✅ **B:** The Root CA is **self-signed** (its own
>   certificate is signed by itself) and serves as
>   the **trust anchor** — pre-installed in browser
>   and OS trust stores. The Intermediate CA is
>   signed by the Root CA and handles day-to-day
>   certificate issuance. The Root CA private key
>   is kept offline; Intermediate CA keys are online
>   (in HSMs).
> - ❌ **A:** This inverts the hierarchy. The Root CA
>   signs Intermediate CA certificates. Intermediate
>   CAs issue end-entity certificates to users and
>   servers — not to other CAs (that is Root CA's
>   job).
> - ❌ **C:** There is no rule that Root CAs use RSA
>   and Intermediate CAs use ECC. Both can use any
>   supported algorithm. Algorithm choice is not
>   what distinguishes them.
> - ❌ **D:** Both Root CAs and Intermediate CAs can
>   be operated by private companies (e.g., DigiCert,
>   Sectigo, Let's Encrypt). Government vs private
>   operation is not the defining difference between
>   Root and Intermediate CAs.

---

**Q4. Why is the Root CA private key kept offline
(air-gapped) in a PKI hierarchy?**

- A) Because the Root CA key is too large to be
     used in online systems efficiently
- B) Because keeping it offline makes certificate
     issuance faster by reducing network latency
- C) Because compromising the Root CA private key
     would invalidate all certificates in the
     entire hierarchy ✅
- D) Because online Root CA keys are prohibited
     by RFC 5280

> **Explanation:**
> - ✅ **C:** The Root CA is the trust anchor of
>   the entire PKI hierarchy. If its private key
>   is compromised, an attacker can sign fraudulent
>   certificates for any identity, and ALL
>   certificates in the hierarchy would need to be
>   considered untrusted. Keeping it offline
>   (air-gapped) eliminates remote attack surface.
>   The Root CA is only brought online for
>   infrequent operations (signing Intermediate
>   CA certificates).
> - ❌ **A:** Root CA key size is not why it is
>   kept offline — key size has no impact on whether
>   a system can be online. RSA-4096 works fine
>   in online systems. Security is the reason.
> - ❌ **B:** Keeping the Root CA offline does not
>   speed up certificate issuance — it actually
>   makes Root CA operations slower (physical access
>   required). Intermediate CAs handle fast online
>   issuance. This is the opposite of the real reason.
> - ❌ **D:** RFC 5280 does not prohibit online Root
>   CAs — the offline practice is a security best
>   practice, not an RFC requirement. It is mandated
>   by CA/Browser Forum guidelines for publicly
>   trusted CAs.

---

**Q5. What is the role of a Registration Authority
(RA) in a PKI?**

- A) The RA generates the CA's private key and
     keeps it secure
- B) The RA verifies the identity of certificate
     applicants before the CA issues a certificate ✅
- C) The RA publishes the list of revoked
     certificates (CRL) on behalf of the CA
- D) The RA is another name for the Validation
     Authority — both check certificate status

> **Explanation:**
> - ✅ **B:** The Registration Authority (RA)
>   performs identity verification — checking
>   applicant documentation, domain control,
>   organizational details — before passing the
>   request to the CA for certificate issuance.
>   The RA acts as a front-end verification service;
>   the CA does the actual signing. In small PKIs,
>   the CA performs RA functions itself.
> - ❌ **A:** The CA generates and manages its own
>   private key — typically stored in an HSM. The
>   RA has no role in CA key management.
> - ❌ **C:** CRL publication is a CA function —
>   or sometimes a Validation Authority function.
>   The RA's job is identity verification before
>   issuance — not revocation list management.
> - ❌ **D:** RA and VA are different roles. The RA
>   handles enrollment/verification (before cert
>   issuance). The VA handles validation (after
>   cert issuance — checking if certs are still
>   valid via OCSP). They serve opposite ends
>   of the certificate lifecycle.

---

**Q6. Which PKI trust model is used by HTTPS on
the public internet, where browser vendors maintain
a pre-installed list of trusted Root CAs?**

- A) Web of Trust
- B) Bridge CA Model
- C) Cross-Certification Model
- D) Hierarchical Trust Model ✅

> **Explanation:**
> - ✅ **D — Hierarchical Trust Model:** Public web
>   PKI (TLS/HTTPS) uses a hierarchical model with
>   Root CAs at the top. Browser vendors (Google,
>   Mozilla, Apple, Microsoft) maintain a **Root
>   Store** — a curated list of trusted Root CAs
>   pre-installed in their software. All TLS
>   certificates chain up to one of these Root CAs.
> - ❌ **A — Web of Trust:** Web of Trust is used by
>   PGP/GPG email encryption — users vouch for each
>   other's keys. There is no central CA. This model
>   does not scale well and is not used for HTTPS.
> - ❌ **B — Bridge CA:** Bridge CA connects multiple
>   separate PKI hierarchies — used in government
>   inter-agency PKI (e.g., US Federal Bridge CA).
>   Not what HTTPS uses.
> - ❌ **C — Cross-Certification:** Two separate CA
>   hierarchies sign each other's root certificates
>   to establish mutual trust. Used between
>   organizations, not for public web PKI.

---

## MCQs 7–13 — Digital Signatures

---

**Q7. What is the correct key operation for
creating a digital signature?**

- A) The sender encrypts the message with the
     receiver's public key
- B) The sender encrypts the message hash with
     the sender's private key ✅
- C) The sender encrypts the message hash with
     the receiver's public key
- D) The sender encrypts the message with the
     sender's public key

> **Explanation:**
> - ✅ **B:** Digital signature creation:
>   (1) Compute hash of message
>   (2) Encrypt (sign) the hash using the
>   **sender's OWN PRIVATE KEY**
>   This ensures only the sender (private key holder)
>   could have created the signature — enabling
>   authentication and non-repudiation.
> - ❌ **A:** Encrypting the MESSAGE with the
>   receiver's public key is **encryption for
>   confidentiality** — not a digital signature.
>   This ensures only the receiver can read it,
>   but proves nothing about the sender.
> - ❌ **C:** Using the receiver's public key for
>   signing makes no sense — anyone could do that
>   (public keys are public). Signatures must use
>   the SENDER'S private key — something only the
>   sender possesses.
> - ❌ **D:** Using the sender's PUBLIC key to sign
>   would mean anyone could create the same
>   "signature" — public keys are not secret.
>   Signatures must use the PRIVATE key to prove
>   exclusive possession.

---

**Q8. How does a receiver verify a digital
signature on a received message?**

- A) Decrypt the signature with the sender's
     private key and compare to message hash
- B) Decrypt the signature with the receiver's
     private key and compare to message hash
- C) Decrypt the signature with the sender's
     public key and compare to a recomputed
     message hash ✅
- D) Decrypt the signature with the receiver's
     public key and compare to message hash

> **Explanation:**
> - ✅ **C:** Verification steps:
>   (1) Decrypt the signature using the
>   **sender's PUBLIC key** → recovers H'
>   (2) Independently compute Hash(received message)
>   → H
>   (3) Compare H' and H:
>   Match → signature valid ✅
>   No match → invalid ❌
>   The sender's public key is used because the
>   signature was created with the sender's private
>   key — and what one key encrypts, only the other
>   can decrypt.
> - ❌ **A:** The sender's PRIVATE key must remain
>   secret — the receiver does not have it and must
>   not. Verification uses the PUBLIC key.
> - ❌ **B:** The receiver's private key is used for
>   **decrypting confidential messages** — not for
>   verifying someone else's signature. Signature
>   verification always uses the SIGNER'S public key.
> - ❌ **D:** The receiver's PUBLIC key has no role
>   in signature verification. Only the sender's
>   key pair is involved in signing and verification.

---

**Q9. Why is the message hashed before signing
rather than signing the entire message directly?**

- A) Hashing is required by the X.509 standard
     for all digital signature operations
- B) The hash ensures the signature is different
     every time the same message is signed
- C) Asymmetric algorithms can only sign small
     data — hashing produces a fixed small
     fingerprint of any-size message ✅
- D) Hashing the message keeps it confidential
     during the signing process

> **Explanation:**
> - ✅ **C:** RSA and other asymmetric algorithms
>   can only process data smaller than their key
>   size (~256 bytes for RSA-2048). Documents can
>   be megabytes or gigabytes. Hashing first
>   produces a fixed-size fingerprint (e.g., 32
>   bytes for SHA-256) that can be signed directly.
>   As a bonus, hashing is fast — signing a 32-byte
>   hash is much faster than signing a 10MB document.
> - ❌ **A:** X.509 does specify hash algorithms for
>   certificates — but the reason for hashing is
>   the practical size constraint, not a regulatory
>   requirement. Even without X.509, hashing would
>   be necessary for the same technical reasons.
> - ❌ **B:** Digital signatures are deterministic
>   with standard algorithms (RSA PSS is
>   probabilistic, but basic RSA is deterministic).
>   The hash being different each time is not the
>   purpose — the same message produces the same
>   hash.
> - ❌ **D:** Hashing does NOT provide confidentiality
>   — the hash of a message does not hide the
>   message content. The hash is sent alongside
>   the message. Confidentiality requires encryption,
>   not hashing.

---

**Q10. Which security property is provided by a
digital signature but NOT by HMAC?**

- A) Integrity — verifying data has not been altered
- B) Authentication — confirming who sent the message
- C) Non-repudiation — the signer cannot deny
     having signed ✅
- D) Data validation — confirming the message
     format is correct

> **Explanation:**
> - ✅ **C — Non-repudiation:** HMAC uses a
>   **shared secret key** — both sender and receiver
>   know it, so either could have created the MAC.
>   In a dispute, the receiver cannot prove to a
>   third party that the sender created it. Digital
>   signatures use a **private key** held exclusively
>   by the signer — only they could have produced
>   the signature. This is mathematically provable
>   non-repudiation.
> - ❌ **A:** Both digital signatures AND HMAC
>   provide integrity. Both detect any modification
>   to the signed/MAC'd data. Integrity is not
>   what distinguishes them.
> - ❌ **B:** Both digital signatures AND HMAC
>   provide authentication — digital signatures
>   prove the sender owns the private key; HMAC
>   proves the sender knows the shared secret.
>   Authentication alone is not the distinguishing
>   property.
> - ❌ **D:** Data format validation is an application-
>   level concern — neither digital signatures nor
>   HMAC validate message format. They verify
>   integrity and authenticity, not content schema.

---

**Q11. What does a digital signature actually
prove about a document?**

- A) That the document was encrypted by the signer
     and only the receiver can read it
- B) That the document originated from the private
     key holder and has not been altered since
     signing ✅
- C) That the document was stored securely and has
     not been accessed by unauthorized parties
- D) That the document was created within the
     validity period of the signer's certificate

> **Explanation:**
> - ✅ **B:** A valid digital signature proves two
>   things: (1) **Origin** — the message came from
>   the holder of the private key that corresponds
>   to the verified public key (authentication);
>   (2) **Integrity** — the message has not been
>   altered since signing (any change invalidates
>   the signature). Combined: the exact document
>   you are reading was created by the private key
>   holder.
> - ❌ **A:** A digital signature does NOT encrypt
>   the document — the document remains readable.
>   Signing and encrypting are separate operations.
>   A signed document provides authentication and
>   integrity; an encrypted document provides
>   confidentiality.
> - ❌ **C:** Digital signatures say nothing about
>   storage security or unauthorized access to
>   the stored document. A signature on a document
>   doesn't prevent someone from reading or copying
>   it — it only proves who created it and that
>   it hasn't been altered.
> - ❌ **D:** A signature proves the document was
>   signed at the time of signing — but the
>   signature itself does not contain a verified
>   timestamp by default. For time proof, a
>   separate trusted timestamping service (RFC 3161)
>   is required. The certificate validity period is
>   about when the cert is valid, not when signing
>   occurred.

---

**Q12. Which of the following correctly describes
the difference between a digital signature and an
electronic signature?**

- A) They are the same thing — digital signature
     is simply the technical term for electronic
     signature
- B) A digital signature is a cryptographic
     mechanism using private key and hash —
     an electronic signature is any electronic
     indication of intent or agreement ✅
- C) An electronic signature is stronger than a
     digital signature because it includes
     biometric verification
- D) Digital signatures are used only in emails —
     electronic signatures are used only in
     documents

> **Explanation:**
> - ✅ **B:** A **digital signature** is specifically
>   a cryptographic mechanism — it uses a private
>   key to sign a hash of the document, providing
>   mathematically provable authentication and
>   non-repudiation. An **electronic signature**
>   is a broader legal term — it includes any
>   electronic indication of agreement: typed name,
>   checkbox, PIN, scanned signature image, or
>   cryptographic digital signature. All digital
>   signatures are electronic signatures, but not
>   all electronic signatures are digital signatures.
> - ❌ **A:** They are NOT the same. Using them
>   interchangeably is incorrect. A typed name
>   in an email is an electronic signature but
>   is NOT a digital signature — it has no
>   cryptographic properties.
> - ❌ **C:** Electronic signatures are NOT stronger
>   than digital signatures — it is the reverse.
>   Biometric verification may be part of some
>   electronic signature solutions, but it does
>   not automatically make them cryptographically
>   stronger than RSA/ECDSA digital signatures.
> - ❌ **D:** Both digital and electronic signatures
>   are used across documents, emails, and
>   transactions. There is no medium restriction
>   that separates them. The distinction is
>   technical/legal, not about the medium.

---

**Q13. Which digital signature algorithm is
designed for SIGNATURES ONLY and cannot be
used for encryption?**

- A) RSA
- B) DSA ✅
- C) ECDH
- D) AES

> **Explanation:**
> - ✅ **B — DSA (Digital Signature Algorithm):**
>   DSA was designed exclusively for digital
>   signatures — it cannot be used for encryption
>   or key exchange. It is based on the Discrete
>   Logarithm Problem and is defined in FIPS 186.
>   It is being replaced by ECDSA in modern systems.
> - ❌ **A — RSA:** RSA is a versatile asymmetric
>   algorithm used for both digital signatures AND
>   encryption (and key transport). RSA can do both
>   — DSA can only sign.
> - ❌ **C — ECDH:** ECDH (Elliptic Curve
>   Diffie-Hellman) is used for KEY EXCHANGE only —
>   not signing, not encryption. This option is
>   a trap because ECDH is also "only for one
>   purpose" but that purpose is key exchange,
>   not signatures.
> - ❌ **D — AES:** AES is a symmetric block cipher
>   used for encryption — it has no concept of
>   signing or asymmetric key pairs. AES is
>   completely unrelated to digital signatures.

---

## MCQs 14–20 — Digital Certificates

---

**Q14. What is a digital certificate?**

- A) A file containing a user's encrypted private
     key protected by a password
- B) A CA-signed document that binds a public key
     to a verified identity ✅
- C) An encrypted message that proves a user
     knows their password
- D) A hash of the user's public key used to
     verify certificate integrity

> **Explanation:**
> - ✅ **B:** A digital certificate is an electronic
>   document that contains a public key and identity
>   information, digitally signed by a trusted CA.
>   The CA's signature binds the public key to the
>   verified identity — so anyone who trusts the CA
>   can trust that the public key genuinely belongs
>   to the stated identity.
> - ❌ **A:** A certificate contains a PUBLIC key —
>   not a private key. Private keys must never be
>   inside a certificate. A file containing a
>   private key is a key file (e.g., .key, .pfx),
>   not a certificate.
> - ❌ **C:** Digital certificates do not contain
>   or verify passwords. They bind public keys to
>   identities — password verification is a
>   completely different authentication mechanism.
> - ❌ **D:** A certificate fingerprint is a hash
>   of the certificate — but the certificate itself
>   is not a hash. The certificate is a complete
>   structured document containing many fields,
>   not just a hash value.

---

**Q15. Which international standard defines the
format of digital certificates used in TLS/HTTPS?**

- A) FIPS 186-4
- B) RFC 2104
- C) X.509 ✅
- D) PKCS#10

> **Explanation:**
> - ✅ **C — X.509:** X.509 is the ITU-T standard
>   that defines the format of digital certificates.
>   All TLS/HTTPS certificates, S/MIME certificates,
>   and code-signing certificates use X.509 v3
>   format. It was first published in 1988; v3
>   (with extensions) was published in 1996.
> - ❌ **A — FIPS 186-4:** This is the NIST standard
>   for **digital signature algorithms** (DSA, RSA,
>   ECDSA) — not the certificate format. Confusing
>   the signature algorithm standard with the
>   certificate format standard is a common trap.
> - ❌ **B — RFC 2104:** This defines **HMAC** —
>   the Hash-based Message Authentication Code
>   construction. Nothing to do with certificate
>   format.
> - ❌ **D — PKCS#10:** This defines the format
>   of a **Certificate Signing Request (CSR)** —
>   the request submitted to a CA before a
>   certificate is issued. PKCS#10 is the input
>   to the issuance process; X.509 is the format
>   of the certificate that comes out.

---

**Q16. Which version of X.509 introduced
extensions — enabling features like Subject
Alternative Names and Key Usage restrictions?**

- A) X.509 v1 (1988)
- B) X.509 v2 (1993)
- C) X.509 v3 (1996) ✅
- D) X.509 v4 (2001)

> **Explanation:**
> - ✅ **C — X.509 v3 (1996):** Extensions were
>   introduced in X.509 v3. These extensions enable
>   Subject Alternative Names (multiple domain
>   support), Key Usage restrictions, Basic
>   Constraints (CA vs end-entity), CRL distribution
>   points, and OCSP URLs. All modern TLS
>   certificates are X.509 v3.
> - ❌ **A — X.509 v1 (1988):** v1 had the basic
>   certificate structure (subject, issuer, validity,
>   public key, signature) — NO extensions. It
>   was too rigid for practical internet PKI.
> - ❌ **B — X.509 v2 (1993):** v2 added Issuer
>   and Subject Unique Identifiers — small additions
>   that were rarely used in practice. Extensions
>   were NOT part of v2.
> - ❌ **D — X.509 v4:** There is no X.509 v4.
>   The current version is v3 and has been since
>   1996. This option is a fabricated distractor.

---

**Q17. What document does an applicant submit to
a CA when requesting a certificate, and what
does it contain?**

- A) A CRL (Certificate Revocation List) —
     containing all previously issued certificates
- B) A CSR (Certificate Signing Request) —
     containing the applicant's public key,
     identity information, and a self-signature ✅
- C) A CPS (Certification Practice Statement) —
     describing how the applicant will use the
     certificate
- D) A PEM file — containing the applicant's
     encrypted private key for CA verification

> **Explanation:**
> - ✅ **B — CSR (PKCS#10):** A Certificate Signing
>   Request contains:
>   (1) The applicant's **public key**
>   (2) Identity information (DN — name, org, domain)
>   (3) A **self-signature** using the applicant's
>   private key — proving they control the private
>   key matching the public key in the request
>   (proof of possession).
>   The CA verifies identity and self-signature,
>   then issues a signed certificate.
> - ❌ **A:** A CRL (Certificate Revocation List) is
>   published by the CA — not submitted by
>   applicants. It lists certificates the CA has
>   revoked. Applicants never submit CRLs.
> - ❌ **C:** A CPS is the CA's own operational
>   document describing how it runs its PKI
>   operations. Applicants do not submit a CPS —
>   the CA publishes its own CPS.
> - ❌ **D:** Sending the private key to the CA is
>   a critical security violation — the CA must
>   NEVER receive or see the applicant's private
>   key. The certificate contains only the public
>   key. This option describes the opposite of
>   correct PKI practice.

---

**Q18. When a browser receives a server's TLS
certificate, it performs several validation checks.
Which check confirms the certificate has not been
revoked by the CA?**

- A) Validity period check — verifying the
     certificate is not expired
- B) Name matching — verifying the CN or SAN
     matches the hostname
- C) Revocation check using CRL or OCSP ✅
- D) Signature verification — verifying the
     CA's digital signature on the certificate

> **Explanation:**
> - ✅ **C — Revocation check (CRL/OCSP):**
>   Certificate revocation means the CA has
>   invalidated a certificate before its expiry
>   (e.g., due to private key compromise). The
>   browser checks revocation status via:
>   **CRL** (Certificate Revocation List) —
>   download a list of revoked serial numbers, OR
>   **OCSP** (Online Certificate Status Protocol)
>   — real-time query for a specific certificate's
>   status.
> - ❌ **A:** Validity period check confirms the
>   certificate has not EXPIRED — but a certificate
>   can be within its validity period AND still be
>   revoked. Expiry and revocation are separate
>   checks.
> - ❌ **B:** Name matching confirms the certificate
>   is for the right server — but says nothing about
>   whether it has been revoked. A revoked
>   certificate could still have a matching name.
> - ❌ **D:** Signature verification confirms the
>   certificate was genuinely issued by the CA and
>   not tampered with — but does not check if the
>   CA has since invalidated it. Revocation happens
>   after issuance and requires a separate check.

---

**Q19. In a certificate chain of trust, why does
the server send the Intermediate CA certificate
along with its own certificate during a TLS
handshake?**

- A) Because browsers do not store Intermediate
     CA certificates — the server must provide
     the full chain for verification ✅
- B) Because the Intermediate CA certificate
     contains the encryption key used for the
     TLS session
- C) Because sending multiple certificates
     provides extra authentication security
- D) Because browsers require three certificates
     to establish a TLS connection

> **Explanation:**
> - ✅ **A:** Browser trust stores contain only
>   **Root CA certificates** — not Intermediate CA
>   certificates. To verify the server certificate,
>   the browser must trace the chain up to a trusted
>   Root CA. Since it does not have the Intermediate
>   CA certificate locally, the server must provide
>   it. The browser already has the Root CA cert
>   so the server does not need to send it.
> - ❌ **B:** The Intermediate CA certificate
>   contains the Intermediate CA's PUBLIC key —
>   used for chain verification, not for generating
>   TLS session encryption keys. Session keys are
>   established via ECDHE key exchange during the
>   handshake.
> - ❌ **C:** The number of certificates sent is
>   determined by the chain length — not by a
>   desire for extra security. Sending unnecessary
>   extra certificates would slow down the handshake.
> - ❌ **D:** There is no requirement for exactly
>   three certificates. A chain can be two
>   certificates (Root CA + end-entity, though rare)
>   or more (Root + multiple Intermediates +
>   end-entity). The length depends on the PKI
>   hierarchy, not a fixed rule.

---

**Q20. What is a certificate fingerprint and
how is it used?**

- A) The fingerprint is the CA's digital signature
     on the certificate — used to verify the CA
     issued it
- B) The fingerprint is a hash of the entire
     certificate — used to uniquely identify and
     compare certificates ✅
- C) The fingerprint is the subject's public key
     truncated to 20 bytes for quick comparison
- D) The fingerprint is a password protecting
     the certificate file from unauthorized access

> **Explanation:**
> - ✅ **B:** A certificate fingerprint is computed
>   by hashing the entire certificate (typically
>   with SHA-256) — it is NOT part of the
>   certificate itself but computed independently
>   by anyone who has the certificate. It uniquely
>   identifies the certificate and is used for
>   quick comparison, certificate pinning, and
>   display in browser certificate viewers.
> - ❌ **A:** The CA's digital signature is a field
>   within the certificate structure — it is used
>   to verify the certificate's authenticity and
>   was created by the CA when issuing the cert.
>   The fingerprint is computed by the verifier,
>   not by the CA, and is not part of the cert.
> - ❌ **C:** The fingerprint is a hash of the
>   ENTIRE certificate — not just the public key.
>   The public key itself is available as the
>   Subject Public Key Info field; a fingerprint
>   encompasses all fields.
> - ❌ **D:** Certificate files are not password-
>   protected by a fingerprint. Password protection
>   of certificate files (when the private key is
>   included) uses PKCS#12 encryption with a
>   passphrase — completely separate from the
>   fingerprint concept.

---

## MCQs 21–25 — Extra Notes: Standards, Formats,
Extensions

---

**Q21. Which RFC defines the Internet X.509 PKI
Certificate and CRL Profile (PKIX) and is the
primary reference for TLS certificate validation?**

- A) RFC 2104
- B) RFC 6960
- C) RFC 5280 ✅
- D) RFC 3161

> **Explanation:**
> - ✅ **C — RFC 5280:** RFC 5280 (2008) defines the
>   Internet X.509 PKI Certificate and CRL Profile
>   — commonly called the PKIX profile. It is the
>   definitive reference for how X.509 certificates
>   and CRLs are formatted and validated on the
>   Internet. Every browser follows RFC 5280 for
>   certificate path validation.
> - ❌ **A — RFC 2104:** This defines **HMAC** —
>   the Hash-based Message Authentication Code.
>   Completely unrelated to X.509 certificates
>   or PKI profiles.
> - ❌ **B — RFC 6960:** This defines **OCSP** —
>   the Online Certificate Status Protocol for
>   real-time certificate revocation checking.
>   Important PKI standard but not the certificate
>   format/profile definition.
> - ❌ **D — RFC 3161:** This defines the **Time
>   Stamp Protocol (TSP)** — for trusted
>   timestamping of digital signatures. Important
>   for non-repudiation but not the PKI certificate
>   profile.

---

**Q22. What is the purpose of the Subject
Alternative Name (SAN) extension in an X.509 v3
certificate?**

- A) SAN lists the names of all CAs that have
     previously signed the certificate
- B) SAN specifies the alternative encryption
     algorithms the certificate supports
- C) SAN lists additional identities the certificate
     is valid for — such as multiple domain names
     or IP addresses ✅
- D) SAN contains the backup private key in
     case the primary key is compromised

> **Explanation:**
> - ✅ **C — Additional identities:** The Subject
>   Alternative Name extension allows a single
>   certificate to be valid for multiple identities —
>   for example:
>   `DNS: www.example.com, DNS: example.com,
>   DNS: api.example.com, IP: 203.0.113.1`
>   This is the field browsers use for hostname
>   matching (since 2017, CN is no longer used for
>   this purpose). SAN supports DNS names, IP
>   addresses, email addresses, and URIs.
> - ❌ **A:** SAN has nothing to do with CA names.
>   The **Authority Key Identifier** and **Issuer**
>   fields identify the CA that signed the cert.
>   SAN identifies the SUBJECT's additional names —
>   not the CA.
> - ❌ **B:** Algorithm support is not in SAN —
>   the **Signature Algorithm** field in the cert
>   header specifies the algorithm used. Key usage
>   is in the **Key Usage** extension. SAN is only
>   about identity names.
> - ❌ **D:** Certificates must NEVER contain a
>   private key. SAN contains identity information
>   only — domain names, IP addresses, email
>   addresses. Storing backup private keys in
>   certificates would be a catastrophic security
>   failure.

---

**Q23. A server certificate file starts with
`-----BEGIN CERTIFICATE-----`. What encoding
format is this?**

- A) DER — binary Distinguished Encoding Rules
- B) PEM — Base64-encoded DER certificate ✅
- C) PKCS#12 — binary certificate and key bundle
- D) PKCS#7 — binary certificate chain format

> **Explanation:**
> - ✅ **B — PEM format:** A file beginning with
>   `-----BEGIN CERTIFICATE-----` and ending with
>   `-----END CERTIFICATE-----` is in **PEM
>   (Privacy Enhanced Mail)** format. PEM is simply
>   Base64-encoded DER with header/footer lines.
>   It is the standard format for certificates on
>   Linux systems, Apache, Nginx, and OpenSSL.
> - ❌ **A — DER:** DER is a binary format — it
>   contains raw binary bytes and does NOT have
>   a text header like `-----BEGIN CERTIFICATE-----`.
>   If you open a DER file in a text editor it
>   shows unreadable binary characters.
> - ❌ **C — PKCS#12 (.pfx/.p12):** PKCS#12 is also
>   a binary format and contains BOTH the certificate
>   AND the private key together — it does not use
>   the `-----BEGIN CERTIFICATE-----` header.
>   It is typically protected by a password.
> - ❌ **D — PKCS#7 (.p7b):** PKCS#7 can contain
>   a certificate chain (without private key).
>   While it can be Base64-encoded, its header is
>   `-----BEGIN PKCS7-----` — not
>   `-----BEGIN CERTIFICATE-----`.

---

**Q24. What is Certificate Transparency (CT) and
why was it introduced?**

- A) CT is a system for encrypting certificate
     data in transit to prevent interception
- B) CT is a public append-only log of all issued
     TLS certificates — enabling detection of
     fraudulent certificate issuance ✅
- C) CT is a certificate format that makes
     certificate contents visible to end users
     in plain text
- D) CT is a protocol that allows CAs to
     transparently share their private keys
     with browser vendors

> **Explanation:**
> - ✅ **B — Public certificate log:** Certificate
>   Transparency (developed by Google, RFC 6962,
>   2013) creates publicly auditable, append-only
>   Merkle tree logs of all issued TLS certificates.
>   When a CA issues a certificate, it must submit
>   it to CT logs and receive a Signed Certificate
>   Timestamp (SCT). Anyone — especially domain
>   owners — can monitor these logs to detect
>   unauthorized certificates issued for their
>   domains. Chrome has required CT since 2018.
> - ❌ **A:** CT does not encrypt certificate data —
>   certificates are public documents by design.
>   CT is about logging and auditability, not
>   about protecting cert data in transit.
> - ❌ **C:** "Transparent" in Certificate
>   Transparency means publicly auditable — not
>   that the certificate format displays content
>   in plain text. X.509 certificate format is
>   unchanged by CT.
> - ❌ **D:** CAs absolutely must NOT share their
>   private keys with anyone — including browser
>   vendors. CT requires sharing issued CERTIFICATES
>   (public information) to logs — never private
>   keys. This option describes a complete
>   security catastrophe, not CT.

---

**Q25. A wildcard certificate is issued for
`*.example.com`. Which of the following hostnames
is NOT covered by this wildcard certificate?**

- A) www.example.com
- B) api.example.com
- C) mail.example.com
- D) sub.api.example.com ✅

> **Explanation:**
> - ✅ **D — sub.api.example.com:** Wildcard
>   certificates (`*.example.com`) match EXACTLY
>   ONE level of subdomain. They match:
>   `www.example.com`, `api.example.com`,
>   `mail.example.com` — one label replacing `*`.
>   They do NOT match `sub.api.example.com` because
>   that has TWO levels below `example.com`
>   (`sub.api` has a dot). Wildcards only replace
>   a single DNS label with no dots.
> - ❌ **A — www.example.com:** This IS covered —
>   `www` is a single label replacing `*`.
> - ❌ **B — api.example.com:** This IS covered —
>   `api` is a single label replacing `*`.
> - ❌ **C — mail.example.com:** This IS covered —
>   `mail` is a single label replacing `*`.

---

## 📊 Answer Key — Quick Reference

| Q | Answer | Topic |
|---|--------|-------|
| 1 | B | PKI purpose — public key authentication problem |
| 2 | C | CA role — issues and signs certificates |
| 3 | B | Root CA (self-signed) vs Intermediate CA |
| 4 | C | Root CA offline — prevents hierarchy collapse |
| 5 | B | RA role — identity verification before issuance |
| 6 | D | HTTPS uses Hierarchical Trust Model |
| 7 | B | Signing uses sender's PRIVATE key |
| 8 | C | Verification uses sender's PUBLIC key |
| 9 | C | Hash first — asymmetric algorithms only sign small data |
| 10 | C | Digital signature provides non-repudiation; HMAC does not |
| 11 | B | Signature proves origin + integrity |
| 12 | B | Digital vs electronic signature distinction |
| 13 | B | DSA = signatures only |
| 14 | B | Certificate = CA-signed public key + identity binding |
| 15 | C | X.509 = certificate format standard |
| 16 | C | X.509 v3 (1996) introduced extensions |
| 17 | B | CSR = Certificate Signing Request (PKCS#10) |
| 18 | C | Revocation check = CRL or OCSP |
| 19 | A | Server sends Intermediate CA cert — browser needs it |
| 20 | B | Fingerprint = hash of entire certificate |
| 21 | C | RFC 5280 = PKIX Internet certificate profile |
| 22 | C | SAN = additional identities (domains, IPs) |
| 23 | B | `-----BEGIN CERTIFICATE-----` = PEM format |
| 24 | B | CT = public log of all issued certs (fraud detection) |
| 25 | D | `sub.api.example.com` NOT covered by `*.example.com` |

---

## 📋 Topic Coverage Map

| Q | Concept Tested | Source |
|---|----------------|--------|
| 1 | PKI core purpose — public key trust problem | Core |
| 2 | CA role in PKI | Core |
| 3 | Root CA vs Intermediate CA | Core |
| 4 | Root CA offline — why | Core |
| 5 | RA role | Core |
| 6 | PKI trust models — HTTPS uses Hierarchical | Core |
| 7 | Digital signature — signing key direction | Core |
| 8 | Digital signature — verification key direction | Core |
| 9 | Why hash before signing | Core |
| 10 | Non-repudiation — digital sig vs HMAC | Core |
| 11 | What a digital signature proves | Core |
| 12 | Digital vs electronic signature | Core |
| 13 | DSA = signatures only | Core |
| 14 | Digital certificate definition | Core |
| 15 | X.509 = certificate format standard | Core |
| 16 | X.509 v3 introduced extensions | Core |
| 17 | CSR — what it is and contains | Core |
| 18 | Revocation check — CRL and OCSP | Core |
| 19 | Certificate chain — why server sends Intermediate | Core |
| 20 | Certificate fingerprint | Core |
| 21 | RFC 5280 = PKIX Internet PKI profile | Extra Notes |
| 22 | SAN extension — purpose and content | Extra Notes |
| 23 | PEM format identification | Extra Notes |
| 24 | Certificate Transparency — purpose | Extra Notes |
| 25 | Wildcard certificate scope — one level only | Extra Notes |

---