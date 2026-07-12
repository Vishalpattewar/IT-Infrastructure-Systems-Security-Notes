# MCQ Session 08 — CA, Trust Models, Certificate
Issuance, Revocation & Types of Certificates

## 📑 Table of Contents
- [Instructions](#instructions)
- [MCQs 1–6 — Certificate Authority and
  Hierarchy](#mcqs-16--certificate-authority-and-hierarchy)
- [MCQs 7–10 — Trust Models](#mcqs-710--trust-models)
- [MCQs 11–15 — Certificate Issuance and
  Validation](#mcqs-1115--certificate-issuance-and-validation)
- [MCQs 16–20 — Certificate Revocation](#mcqs-1620--certificate-revocation)
- [MCQs 21–25 — Extra Notes: Standards, India
  PKI, Special Topics](#mcqs-2125--extra-notes-standards-india-pki-special-topics)
- [Answer Key](#-answer-key--quick-reference)
- [Topic Coverage Map](#-topic-coverage-map)

---

## Instructions

- 25 MCQs — drawn from core syllabus AND
  📌 Extra Notes of Session 08
- Foundation + Fundamental + Basic Concepts ONLY
- 4 options per question
- ✅ marks the correct answer
- Full explanation after every question including
  why each wrong option is wrong
- Wrong options look reasonable to someone unprepared
- Correct answer is clear to someone with solid basics

---

## MCQs 1–6 — Certificate Authority and Hierarchy

---

**Q1. What is the PRIMARY role of a Certificate
Authority (CA) in a PKI?**

- A) To encrypt all data transmitted between
     users on the network
- B) To generate private keys for all users and
     store them securely
- C) To issue and digitally sign certificates —
     binding a public key to a verified identity ✅
- D) To monitor all certificate usage and report
     suspicious activity

> **Explanation:**
> - ✅ **C:** A CA is a trusted third party that
>   verifies an applicant's identity and then issues
>   a digitally signed X.509 certificate that binds
>   the applicant's public key to their verified
>   identity. The CA's signature is what makes the
>   certificate trustworthy to all parties who trust
>   that CA.
> - ❌ **A:** CAs do not encrypt communications —
>   encryption is performed by the communicating
>   parties themselves using keys from their
>   certificates. A CA's role is identity
>   verification and certification, not encryption.
> - ❌ **B:** CAs must never generate or store
>   users' private keys — private keys must remain
>   exclusively with their owners. The end entity
>   generates their own key pair and submits only
>   the public key to the CA via a CSR.
> - ❌ **D:** Monitoring certificate usage is a
>   security operations function — not the CA's
>   role. CAs maintain certificate status through
>   CRL and OCSP, but active monitoring of usage
>   is separate from the CA function.

---

**Q2. In a PKI hierarchy, which CA is described
as self-signed and serves as the trust anchor?**

- A) Issuing CA
- B) Intermediate CA
- C) Root CA ✅
- D) Registration Authority

> **Explanation:**
> - ✅ **C — Root CA:** The Root CA sits at the top
>   of the PKI hierarchy. Its certificate is
>   **self-signed** — the issuer and subject are the
>   same — because there is no higher authority to
>   sign it. It serves as the **trust anchor** —
>   pre-installed in browser and OS trust stores.
>   All trust in the hierarchy flows from the Root CA.
> - ❌ **A — Issuing CA:** An Issuing CA is signed
>   by an Intermediate CA — it is not self-signed.
>   It issues end-entity certificates but is not
>   the trust anchor.
> - ❌ **B — Intermediate CA:** An Intermediate CA
>   is signed by the Root CA — it is not self-signed.
>   It handles day-to-day certificate issuance and
>   acts as a buffer between the Root CA and
>   end entities.
> - ❌ **D — Registration Authority:** An RA is not
>   a CA at all — it is a separate entity that
>   performs identity verification before the CA
>   issues a certificate. It does not issue or sign
>   certificates.

---

**Q3. Why is the Root CA private key kept offline
(air-gapped) in a PKI system?**

- A) Because online storage would make the key
     too slow to use for certificate signing
- B) Because compromising the Root CA key would
     invalidate every certificate in the entire
     hierarchy ✅
- C) Because RFC 5280 prohibits Root CAs from
     being connected to any network
- D) Because Root CA certificates are too large
     to process on online systems

> **Explanation:**
> - ✅ **B:** The Root CA is the ultimate trust
>   anchor. If its private key is stolen, an
>   attacker can sign fraudulent certificates
>   for ANY identity, and ALL certificates in the
>   hierarchy become suspect. This catastrophic
>   risk justifies keeping the Root CA completely
>   offline — it is only brought online for
>   rare operations like signing Intermediate CA
>   certificates.
> - ❌ **A:** Key size and processing speed have
>   no bearing on whether a CA should be online.
>   RSA-4096 operations complete in milliseconds
>   on modern hardware. Security — not performance
>   — is the reason for offline storage.
> - ❌ **C:** RFC 5280 does not prohibit online Root
>   CAs. The offline practice is a CA/Browser Forum
>   security best practice requirement for publicly
>   trusted CAs — not an RFC prohibition.
> - ❌ **D:** Certificate size is not a factor —
>   X.509 certificates are typically a few kilobytes
>   at most, easily processed by any system. This
>   option is a fabricated distractor.

---

**Q4. What is the key security benefit of using
Intermediate CAs between the Root CA and
end-entity certificates?**

- A) Intermediate CAs allow certificates to be
     issued faster because they are online
- B) Intermediate CAs use stronger encryption
     algorithms than Root CAs
- C) If an Intermediate CA is compromised, only
     its certificates are affected — the Root CA
     and other Intermediate CAs remain trusted ✅
- D) Intermediate CAs store private keys for
     end users — reducing management complexity

> **Explanation:**
> - ✅ **C:** This is the "blast radius" principle.
>   An Intermediate CA compromise is serious but
>   **contained** — the Root CA simply revokes the
>   Intermediate CA's certificate, invalidating all
>   certs from that Intermediate CA but leaving the
>   Root CA and all other Intermediate CAs intact.
>   A Root CA compromise has no such recovery —
>   the entire hierarchy must be rebuilt.
> - ❌ **A:** Speed of issuance is a side benefit
>   (Intermediate CAs are online — Root CA is
>   offline), but it is not the KEY security benefit
>   of the layered hierarchy design. The containment
>   of compromise is the primary security reason.
> - ❌ **B:** There is no rule that Intermediate CAs
>   must use stronger algorithms than Root CAs.
>   Both use the same cryptographic algorithms
>   (RSA, ECDSA). Algorithm strength is independent
>   of CA hierarchy level.
> - ❌ **D:** CAs must never store end users'
>   private keys — this would be a catastrophic
>   security design. Private keys must remain
>   exclusively with their owners.

---

**Q5. What is the CA/Browser Forum and what is
its primary function?**

- A) A government agency that certifies CAs
     and issues legal penalties for violations
- B) A voluntary consortium of CAs and browser
     vendors that establishes minimum standards
     for certificate issuance ✅
- C) An international standards body that defines
     the X.509 certificate format
- D) A group of security researchers that tests
     CA systems for vulnerabilities

> **Explanation:**
> - ✅ **B:** The CA/Browser Forum (CABF, founded
>   2005) is a voluntary consortium of Certificate
>   Authorities (like DigiCert, Sectigo) and browser
>   vendors (like Google, Mozilla, Apple, Microsoft).
>   It establishes the Baseline Requirements (BR)
>   and Extended Validation Guidelines that govern
>   how publicly trusted certificates are issued.
>   Browser vendors enforce compliance by removing
>   non-compliant CAs from their trust stores.
> - ❌ **A:** The CABF is not a government agency —
>   it has no legal enforcement power. Enforcement
>   comes from browser vendors removing non-compliant
>   CAs from trust stores — a market mechanism,
>   not a legal one.
> - ❌ **C:** The X.509 certificate format is defined
>   by **ITU-T** (the international telecommunication
>   standards body) — not the CABF. The CABF sets
>   REQUIREMENTS for how certs are ISSUED — not the
>   technical format of the certificate itself.
> - ❌ **D:** Security research on CA systems is
>   done by independent researchers and academic
>   institutions — not by the CABF. The CABF sets
>   standards and requirements, not vulnerability
>   testing.

---

**Q6. Which Hardware Security Module (HSM)
security level is the industry standard for
protecting Intermediate CA private keys?**

- A) FIPS 140-2 Level 1
- B) FIPS 140-2 Level 2
- C) FIPS 140-2 Level 3 ✅
- D) FIPS 140-2 Level 4

> **Explanation:**
> - ✅ **C — FIPS 140-2 Level 3:** FIPS 140-2 Level
>   3 is the industry standard for protecting CA
>   private keys. Level 3 requires physical tamper
>   resistance and tamper evidence — the HSM
>   automatically destroys keys if tampering is
>   detected. It also requires identity-based
>   authentication for operators accessing the HSM.
>   CA/Browser Forum Baseline Requirements reference
>   this level for CA key protection.
> - ❌ **A — Level 1:** The most basic level —
>   only software security, no physical protection
>   requirements. Entirely insufficient for CA key
>   protection.
> - ❌ **B — Level 2:** Adds tamper-evidence
>   (seals/picks-resistant enclosures) but lacks
>   the active tamper response of Level 3.
>   Intermediate for some uses but not the CA
>   standard.
> - ❌ **D — Level 4:** The highest level —
>   providing environmental protection against
>   voltage and temperature attacks. Used in
>   extremely high-security environments like
>   payment systems. Exceeds typical CA requirements
>   and is more expensive and restrictive.

---

## MCQs 7–10 — Trust Models

---

**Q7. Which PKI trust model is used for
TLS/HTTPS on the public internet?**

- A) Web of Trust — where users validate each
     other's public keys
- B) Bridge CA Model — where a hub CA connects
     multiple PKI hierarchies
- C) Hierarchical Trust Model — where a Root CA
     is pre-installed in browser trust stores ✅
- D) Cross-Certification Model — where two CAs
     sign each other's certificates

> **Explanation:**
> - ✅ **C — Hierarchical Trust Model:** Public web
>   PKI uses a tree-shaped hierarchy with Root CAs
>   at the top. Browser and OS vendors (Google,
>   Mozilla, Apple, Microsoft) pre-install trusted
>   Root CA certificates in their trust stores.
>   Any certificate that chains up to a trusted Root
>   CA is automatically trusted by the browser.
> - ❌ **A — Web of Trust:** Web of Trust is used
>   by PGP/GPG email encryption — it is decentralized
>   with no central CA. It does not scale for
>   billions of HTTPS connections.
> - ❌ **B — Bridge CA:** Bridge CA connects multiple
>   separate PKI hierarchies (used in US Federal
>   Government PKI). It is not the model used for
>   public web PKI.
> - ❌ **D — Cross-Certification:** Two organizations
>   establish mutual trust by signing each other's
>   CA certificates. Used for inter-organizational
>   PKI — not for public HTTPS where a single
>   hierarchy anchored by trusted Root CAs is used.

---

**Q8. In PGP's Web of Trust, how many FULL trust
signatures from trusted parties are needed to
consider a key valid?**

- A) 3 full trust signatures
- B) 1 full trust signature ✅
- C) 2 full trust signatures
- D) 5 full trust signatures

> **Explanation:**
> - ✅ **B — 1 full trust:** In PGP's Web of Trust,
>   **ONE full trust** signature from a fully trusted
>   key owner is sufficient to validate a key.
>   Alternatively, **THREE marginal trust**
>   signatures are also sufficient. The formula:
>   1 full trust OR 3 marginal trusts = key valid.
> - ❌ **A — 3 full trust:** Three signatures are
>   required for MARGINAL trust (not full trust).
>   Confusing full and marginal trust requirements
>   is the classic exam trap for this topic.
> - ❌ **C — 2 full trust:** Two full trust
>   signatures is not the defined threshold. The
>   threshold is exactly 1 full trust OR 3
>   marginal trusts.
> - ❌ **D — 5 full trust:** Five full trust
>   signatures is entirely fabricated — not part
>   of PGP's Web of Trust specification.

---

**Q9. What is a Trust Store (Root Store)?**

- A) An encrypted database where CA private
     keys are stored for safekeeping
- B) A pre-installed collection of trusted Root
     CA certificates on an operating system
     or browser ✅
- C) A server that stores all issued certificates
     for public download
- D) A hardware device that holds user certificates
     and private keys

> **Explanation:**
> - ✅ **B:** A trust store is a collection of
>   trusted Root CA certificates that comes
>   pre-installed with an operating system or
>   browser. When a browser receives a server
>   certificate, it checks if the certificate
>   chains up to any Root CA in the trust store.
>   If yes → trusted automatically. If no →
>   security warning shown.
> - ❌ **A:** CA private keys are stored in
>   Hardware Security Modules (HSMs) — not in a
>   "trust store." A trust store contains PUBLIC
>   certificates (Root CA certs), not private keys.
> - ❌ **C:** A public repository or LDAP directory
>   stores issued certificates for download — this
>   is a Certificate Repository, not a Trust Store.
>   A trust store is LOCAL (on the user's device)
>   and contains only Root CA certificates.
> - ❌ **D:** A device that holds user certificates
>   and private keys is a smart card, USB token,
>   or HSM — not a trust store. Trust stores contain
>   Root CA certificates used for validation.

---

**Q10. The Bridge CA model was designed to solve
a specific scalability problem. What problem
does it address?**

- A) The problem of Root CAs being too slow to
     sign certificates for high-volume issuance
- B) The problem of N PKI hierarchies needing
     N×(N-1)/2 cross-certifications to trust
     each other — Bridge CA reduces this to N ✅
- C) The problem of intermediate CAs being
     compromised and affecting end-entity trust
- D) The problem of certificate revocation being
     too slow in hierarchical PKI systems

> **Explanation:**
> - ✅ **B:** Without a Bridge CA, if N separate
>   PKI hierarchies want to mutually trust each
>   other, every pair needs a cross-certification
>   agreement — N×(N-1)/2 agreements total (the
>   same formula as symmetric keys for N users).
>   With a Bridge CA, each hierarchy cross-certifies
>   only with the Bridge CA — just N agreements
>   total, with transitive trust enabling all
>   hierarchies to trust each other. This is exactly
>   how the US Federal PKI works.
> - ❌ **A:** Root CA signing speed is not a
>   scalability problem — Root CAs sign Intermediate
>   CA certs infrequently (not high volume).
>   Intermediate CAs handle high-volume daily signing.
>   Bridge CA does not address signing speed.
> - ❌ **C:** Intermediate CA compromise is addressed
>   by the layered hierarchy design (Root CA can
>   revoke Intermediate CA) — not by Bridge CA.
>   Bridge CA addresses cross-organizational trust,
>   not internal hierarchy security.
> - ❌ **D:** Certificate revocation speed is
>   addressed by OCSP and OCSP Stapling — not by
>   Bridge CA. Bridge CA is about establishing
>   cross-organizational trust paths efficiently.

---

## MCQs 11–15 — Certificate Issuance and Validation

---

**Q11. A website owner applies for a certificate
and the CA verifies only that the applicant
controls the domain. No company name or
organization details appear in the certificate.
What type of certificate was issued?**

- A) EV (Extended Validation) certificate
- B) OV (Organization Validation) certificate
- C) DV (Domain Validation) certificate ✅
- D) Code Signing certificate

> **Explanation:**
> - ✅ **C — DV:** Domain Validation certificates
>   verify only that the applicant controls the
>   domain — typically via an HTTP challenge or
>   DNS TXT record. No organization name, address,
>   or legal identity is verified or included in
>   the certificate's Subject field. DV certs are
>   the most common type — free via Let's Encrypt,
>   issued in minutes.
> - ❌ **A — EV:** Extended Validation involves
>   thorough legal identity verification —
>   incorporating documents, address verification,
>   authorized representative confirmation. The
>   cert includes organization name, jurisdiction,
>   and registration number. Takes days to weeks.
> - ❌ **B — OV:** Organization Validation verifies
>   both domain control AND the organization's
>   legal existence — the organization name IS
>   included in the certificate Subject field.
>   The question states no organization details
>   appear — ruling out OV.
> - ❌ **D — Code Signing:** Code signing certs
>   are for signing software executables — they
>   are not issued based on domain control. They
>   require organization verification similar to OV.

---

**Q12. Which of the following is an approved
method for Domain Validation (DV) certificate
issuance by the CA/Browser Forum?**

- A) Submitting a government-issued business
     registration document to the CA
- B) Providing a notarized letter confirming
     domain ownership
- C) Placing a specific token file at a URL
     on the domain that the CA retrieves ✅
- D) Sending a certified mail letter to the
     domain registrar

> **Explanation:**
> - ✅ **C — HTTP file challenge (HTTP-01):** The
>   CA instructs the applicant to place a specific
>   token file at a well-known URL on the domain
>   (e.g., `http://example.com/.well-known/acme-challenge/token`).
>   The CA retrieves the file — if it matches the
>   expected token → domain control is proven.
>   This is one of the CA/Browser Forum approved
>   automated domain validation methods.
> - ❌ **A:** Business registration documents are
>   used for **OV** validation — verifying the
>   organization's legal existence. DV only needs
>   domain control proof — no business documents.
> - ❌ **B:** Notarized letters are associated with
>   EV validation for legal identity confirmation —
>   not with automated DV domain validation.
>   DV uses automated technical challenges.
> - ❌ **D:** Certified mail to a registrar is not
>   a CA/Browser Forum approved DV validation method.
>   DV validation is automated and technical —
>   not postal.

---

**Q13. What is the ACME protocol and which
RFC defines it?**

- A) A protocol for CA cross-certification —
     defined in RFC 5280
- B) A protocol for real-time certificate
     revocation checking — defined in RFC 6960
- C) A protocol for automated certificate
     issuance and renewal — defined in RFC 8555 ✅
- D) A protocol for certificate format encoding —
     defined in RFC 2986

> **Explanation:**
> - ✅ **C — RFC 8555:** ACME (Automatic Certificate
>   Management Environment) is the protocol used by
>   Let's Encrypt and other CAs to automate DV
>   certificate issuance and renewal. The client
>   (e.g., Certbot) completes a CA-issued challenge
>   to prove domain control, receives the certificate,
>   and can renew automatically before expiry.
>   RFC 8555 was published in 2019.
> - ❌ **A:** CA cross-certification procedures
>   are described in RFC 5280 (PKIX profile) as
>   part of the broader PKI framework — but ACME
>   is not about cross-certification.
> - ❌ **B:** Real-time certificate revocation
>   checking is the job of **OCSP** — defined in
>   RFC 6960. ACME is about certificate issuance,
>   not revocation.
> - ❌ **D:** RFC 2986 defines **PKCS#10** — the
>   Certificate Signing Request format. Not ACME.
>   ACME manages the full lifecycle including CSR
>   submission, but the CSR format itself is PKCS#10.

---

**Q14. Let's Encrypt issues certificates with
a validity period of 90 days. What is the
PRIMARY reason for this short validity period?**

- A) 90 days is the maximum allowed by the
     CA/Browser Forum Baseline Requirements
- B) Let's Encrypt's free tier restricts
     certificates to 90 days for revenue reasons
- C) Short validity encourages automation,
     reduces exposure from compromised certs,
     and reduces reliance on revocation ✅
- D) 90-day certs use weaker key sizes and
     need frequent renewal to maintain security

> **Explanation:**
> - ✅ **C:** The 90-day validity is an intentional
>   design choice by Let's Encrypt (ISRG) for
>   three reasons: (1) It forces automation via
>   ACME — certificates that expire in 90 days
>   must be renewed automatically; (2) If a private
>   key is compromised, the maximum exposure window
>   is 90 days; (3) Short-lived certs effectively
>   replace revocation — by the time revocation
>   matters, the cert has almost expired anyway.
> - ❌ **A:** The CA/Browser Forum maximum is
>   **398 days** (since September 2020) — not
>   90 days. Let's Encrypt chose 90 days as their
>   own policy, well below the industry maximum.
> - ❌ **B:** Let's Encrypt is operated by ISRG
>   (a non-profit) and offers all certificates
>   for free — there is no paid tier. Revenue is
>   not a factor in the 90-day choice.
> - ❌ **D:** Let's Encrypt certificates use
>   standard RSA-2048 or ECDSA P-256 keys —
>   the same as any other commercially issued
>   certificate. Shorter validity does not imply
>   weaker keys.

---

**Q15. Since September 2020, what is the maximum
certificate validity period allowed by the
CA/Browser Forum Baseline Requirements?**

- A) 730 days (2 years)
- B) 825 days
- C) 398 days ✅
- D) 365 days (1 year)

> **Explanation:**
> - ✅ **C — 398 days:** The CA/Browser Forum
>   reduced the maximum TLS certificate validity
>   to **398 days** (approximately 13 months),
>   effective September 1, 2020. This was driven
>   by Apple's announcement that Safari would
>   reject certificates with validity > 398 days —
>   prompting the CABF to formalize this as a
>   Baseline Requirement.
> - ❌ **A — 730 days:** 730 days (2 years) was the
>   previous maximum before September 2018 when it
>   was reduced to 825 days. By September 2020
>   it was further reduced to 398 days.
> - ❌ **B — 825 days:** 825 days was the maximum
>   from March 2018 to September 2020 — now
>   superseded by the 398-day limit. This is a
>   specific historical value used as a distractor.
> - ❌ **D — 365 days:** 365 days is less than 398
>   days — while a 1-year cert is fine (within the
>   398-day limit), 365 days is NOT the specified
>   maximum. The limit is 398 days to allow for
>   a small buffer beyond exactly one year.

---

## MCQs 16–20 — Certificate Revocation

---

**Q16. What is a Certificate Revocation List (CRL)?**

- A) A list of all certificates currently issued
     by a CA — used to verify certificate
     authenticity
- B) A CA-digitally-signed list of serial numbers
     of certificates that have been revoked
     before their expiry ✅
- C) A list of approved domain names for which
     a CA is allowed to issue certificates
- D) A list of trusted Root CA certificates
     pre-installed in browsers

> **Explanation:**
> - ✅ **B:** A CRL is a digitally signed document
>   published by a CA that lists the **serial
>   numbers** of certificates that have been revoked
>   (invalidated before their expiry date). Clients
>   download the CRL and check if the certificate's
>   serial number appears in it. If found → revoked
>   → reject. Not found → still valid.
> - ❌ **A:** A CRL does NOT list all issued
>   certificates — only REVOKED ones. A full list
>   of all issued certificates would be enormous
>   and is not the purpose of a CRL. A certificate
>   repository or LDAP directory stores all certs.
> - ❌ **C:** A list of approved domain names for
>   certificate issuance is controlled by
>   **CAA (Certificate Authority Authorization)**
>   DNS records — not a CRL. CAA records tell CAs
>   which ones are permitted to issue for a domain.
> - ❌ **D:** A list of trusted Root CA certificates
>   is a **Trust Store** — pre-installed in browsers
>   and operating systems. A CRL is about revoked
>   certificates, not trusted CAs.

---

**Q17. What is the MOST critical reason for
revoking a certificate?**

- A) The certificate holder changed their
     email address
- B) The certificate is approaching its
     expiry date
- C) The private key corresponding to the
     certificate was compromised ✅
- D) The certificate holder wants a certificate
     with a longer validity period

> **Explanation:**
> - ✅ **C — Private key compromise:** If the
>   private key is stolen or exposed, an attacker
>   can use it to impersonate the certificate
>   holder — signing malicious content, performing
>   MITM attacks on TLS connections — for the
>   entire remaining validity period of the cert.
>   Immediate revocation is essential to stop
>   ongoing harm.
> - ❌ **A:** Changing an email address may require
>   a new certificate (if the email is in the cert)
>   but is categorized as "affiliationChanged" or
>   "superseded" — these are valid but not the
>   MOST critical revocation reason. No active
>   security threat is present.
> - ❌ **B:** A certificate approaching expiry
>   simply needs **renewal** — not revocation.
>   Revocation is for invalidating a certificate
>   BEFORE its natural expiry when it is no longer
>   trustworthy. Expiring certificates become
>   invalid automatically.
> - ❌ **D:** Wanting a longer validity period
>   means issuing a new certificate — the existing
>   one would be superseded. This might trigger
>   a "superseded" revocation but is not a
>   critical security concern.

---

**Q18. What is OCSP and how does it differ from
a CRL?**

- A) OCSP is a certificate format — it differs
     from CRL in that CRL is binary while OCSP
     is text-based
- B) OCSP is a real-time protocol for checking
     the status of a SPECIFIC certificate —
     while CRL is a downloaded list of ALL
     revoked certificate serial numbers ✅
- C) OCSP is used only for EV certificates —
     CRL is used for DV and OV certificates
- D) OCSP is operated by browsers — CRL is
     operated by certificate holders

> **Explanation:**
> - ✅ **B:** OCSP (Online Certificate Status
>   Protocol) queries a responder in real-time for
>   the status of ONE specific certificate.
>   The client sends the certificate's serial number
>   and receives a signed GOOD/REVOKED/UNKNOWN
>   response. CRL requires downloading the entire
>   list of revoked serial numbers and searching
>   locally. OCSP is more targeted; CRL is a
>   bulk download.
> - ❌ **A:** Both OCSP and CRL are protocols/
>   data structures defined by standards (not
>   certificate formats). CRL and OCSP responses
>   can both be DER or Base64 encoded — the
>   distinction is not about encoding format.
> - ❌ **C:** OCSP and CRL are used for all
>   certificate types — DV, OV, and EV alike.
>   There is no type-based restriction on which
>   revocation mechanism is used.
> - ❌ **D:** OCSP is operated by the CA or a
>   Validation Authority (VA) on the CA's behalf —
>   not by browsers. CRL is also published by the
>   CA. Both revocation mechanisms are CA-side
>   functions — browsers are the consumers, not
>   the operators.

---

**Q19. What is OCSP Stapling and what problem
does it solve?**

- A) OCSP Stapling is a method where the CA
     attaches the certificate to the OCSP
     response for verification
- B) OCSP Stapling is where the server
     pre-fetches its own OCSP response and
     attaches it to the TLS handshake —
     solving privacy and performance issues ✅
- C) OCSP Stapling is a technique where multiple
     certificates are stapled together into a
     single file for efficient delivery
- D) OCSP Stapling is where the browser stores
     (staples) OCSP responses locally to avoid
     repeated checks

> **Explanation:**
> - ✅ **B:** In OCSP Stapling, the **SERVER**
>   periodically fetches its own OCSP response
>   from the CA's OCSP responder and caches it.
>   During each TLS handshake, the server includes
>   (staples) this pre-fetched OCSP response.
>   Problems solved: (1) **Privacy** — the client
>   never contacts the CA directly, so the CA
>   cannot track which sites users visit;
>   (2) **Performance** — no extra OCSP round-trip
>   during handshake; (3) **Reliability** — works
>   even if OCSP server is temporarily unavailable.
> - ❌ **A:** The CA attaches nothing to the OCSP
>   response in stapling — the OCSP response is
>   a separate document signed by the CA's OCSP
>   signing key. The SERVER does the attaching,
>   not the CA.
> - ❌ **C:** "Stapling certificates together"
>   is a completely different concept — certificate
>   chains are sent as multiple certs in TLS, but
>   this is not OCSP Stapling. OCSP Stapling
>   specifically refers to attaching an OCSP
>   response to the TLS handshake.
> - ❌ **D:** OCSP response caching does happen
>   on some browsers but this is not "stapling."
>   OCSP Stapling is specifically a SERVER-side
>   operation — the server staples the OCSP
>   response into the TLS handshake it sends
>   to clients.

---

**Q20. Most browsers currently implement "soft
fail" for OCSP checks. What does soft fail mean?**

- A) The browser shows a warning but still
     displays the certificate information
- B) The browser accepts the certificate even
     if the OCSP check fails or is unreachable ✅
- C) The browser automatically switches to
     CRL checking when OCSP fails
- D) The browser asks the user whether to
     accept or reject the certificate

> **Explanation:**
> - ✅ **B — Soft fail:** When OCSP is unreachable
>   or returns an error, "soft fail" means the
>   browser **ignores the failure** and accepts
>   the certificate anyway — treating it as valid.
>   This is the current default behavior of all
>   major browsers. The security risk: an attacker
>   can block OCSP traffic to prevent revocation
>   checking — keeping a revoked certificate
>   trusted by browsers.
> - ❌ **A:** Soft fail does not show a warning —
>   the connection proceeds silently as if the
>   OCSP check succeeded. If browsers warned users
>   every time an OCSP check failed, legitimate
>   sites with slow OCSP responders would generate
>   constant false alarms.
> - ❌ **C:** Automatic fallback to CRL is not
>   standard browser behavior for soft fail.
>   Browsers may try CRL if configured, but soft
>   fail means accepting the certificate regardless —
>   not automatically switching mechanisms.
> - ❌ **D:** Presenting a user choice for OCSP
>   failures would generate too many confusing
>   prompts for average users. Soft fail is a
>   silent acceptance — no user interaction.

---

## MCQs 21–25 — Extra Notes: Standards, India
PKI, Special Topics

---

**Q21. Which body licenses and regulates
Certificate Authorities in India under the
Information Technology Act 2000?**

- A) TRAI (Telecom Regulatory Authority of India)
- B) CCA (Controller of Certifying Authorities) ✅
- C) SEBI (Securities and Exchange Board of India)
- D) RBI (Reserve Bank of India)

> **Explanation:**
> - ✅ **B — CCA:** The **Controller of Certifying
>   Authorities (CCA)** is established under the
>   Information Technology Act 2000 as the apex
>   body responsible for licensing and regulating
>   Certifying Authorities (CAs) in India. Licensed
>   CAs issue Digital Signature Certificates (DSCs)
>   used for income tax filing, MCA filings,
>   e-tendering, and other government services.
> - ❌ **A — TRAI:** TRAI regulates
>   telecommunications in India — not digital
>   certificates or PKI. It deals with spectrum,
>   telecom tariffs, and service quality standards.
> - ❌ **C — SEBI:** SEBI regulates securities
>   markets in India (stock exchanges, mutual funds,
>   listed companies). It has no role in digital
>   certificate licensing.
> - ❌ **D — RBI:** RBI regulates banking and
>   monetary policy in India. While RBI issues
>   guidelines for digital payment security, it
>   is not the PKI regulatory body. CCA under
>   the IT Act 2000 has that specific role.

---

**Q22. What is India's Root CA, and which
body operates it?**

- A) DigiCert Root CA — operated by a US company
     under contract with Indian government
- B) Root Certifying Authority of India (RCAI)
     — operated by the CCA ✅
- C) TATA Communications Root CA — operated
     by a private Indian company
- D) National Informatics Centre (NIC) Root CA
     — operated by MEITY

> **Explanation:**
> - ✅ **B — RCAI operated by CCA:** The **Root
>   Certifying Authority of India (RCAI)** is
>   India's national Root CA. It is operated by
>   the **Controller of Certifying Authorities
>   (CCA)** — the apex PKI body under the IT Act
>   2000. The RCAI signs the certificates of all
>   licensed Certifying Authorities in India,
>   establishing the trust hierarchy for Indian
>   PKI.
> - ❌ **A:** India's Root CA is domestically
>   operated — not outsourced to any US company.
>   DigiCert is a major commercial CA but has no
>   role in India's national PKI root.
> - ❌ **C:** TATA Communications is a private
>   telecom company — not India's Root CA. Some
>   private companies are licensed CAs in India
>   but they are Intermediate CAs signed by RCAI —
>   not the Root CA.
> - ❌ **D:** NIC (National Informatics Centre)
>   operates IT infrastructure for the Indian
>   government and does have its own CA for
>   government use — but it is NOT India's Root CA
>   (RCAI). NIC CA is a government CA at a different
>   level in the hierarchy.

---

**Q23. Under the EU eIDAS regulation, which
level of electronic signature is legally
equivalent to a handwritten signature across
all EU member states?**

- A) Electronic Signature (ES)
- B) Advanced Electronic Signature (AdES)
- C) Qualified Electronic Signature (QES) ✅
- D) Digital Signature Certificate (DSC)

> **Explanation:**
> - ✅ **C — QES:** Under EU Regulation 910/2014
>   (eIDAS), a **Qualified Electronic Signature
>   (QES)** has the same legal effect as a
>   handwritten signature across all 27 EU member
>   states. A QES must be created using a Qualified
>   Certificate issued by a Qualified Trust Service
>   Provider (QTSP) on a Qualified Signature
>   Creation Device (QSCD) — such as a smart card
>   or USB token.
> - ❌ **A — Electronic Signature (ES):** The basic
>   level of electronic signature under eIDAS —
>   includes any form of electronic indication
>   of intent (typed name, checkbox). It has the
>   lowest legal standing and is not automatically
>   equivalent to a handwritten signature.
> - ❌ **B — Advanced Electronic Signature (AdES):**
>   AdES is stronger than basic ES — it must be
>   uniquely linked to the signer and capable of
>   identifying them. However, it does NOT have
>   the same automatic legal equivalence to
>   handwritten signatures that QES has.
> - ❌ **D — DSC:** Digital Signature Certificate
>   is a term used in **India's IT Act 2000** —
>   not eIDAS terminology. eIDAS uses QES, AdES,
>   and ES as its signature classification levels.

---

**Q24. A certificate with reason code 6 in its
CRL entry (certificateHold) is different from
other revocations. What makes it unique?**

- A) It permanently revokes the certificate
     and it can never be reinstated
- B) It temporarily suspends the certificate —
     it can be unrevoked if the hold is lifted ✅
- C) It revokes the certificate and all
     certificates issued by the same CA
- D) It is used only for CA certificates —
     not for end-entity certificates

> **Explanation:**
> - ✅ **B — Temporary suspension:** CRL reason code
>   6 (certificateHold) is unique because it is a
>   **temporary** revocation. The certificate is
>   suspended — treated as revoked while on hold —
>   but the CA can remove the hold later using a
>   "removeFromCRL" entry (code 8) in a Delta CRL.
>   This is useful when a certificate needs to be
>   temporarily suspended (e.g., suspected but
>   unconfirmed compromise) without permanently
>   revoking it.
> - ❌ **A:** Permanent revocation uses other reason
>   codes (keyCompromise, affiliationChanged,
>   superseded, etc.). certificateHold is
>   specifically the ONLY revocable revocation —
>   the hold can be lifted. All other reason codes
>   result in permanent revocation.
> - ❌ **C:** CRL entries are per-certificate —
>   not per-CA. Revoking one certificate does not
>   revoke all certificates from the same CA.
>   A CA compromise (reason code 2) would trigger
>   mass revocations, but that is a separate
>   scenario from certificateHold.
> - ❌ **D:** certificateHold can be applied to
>   any certificate — end-entity or CA certs.
>   There is no restriction limiting it to CA
>   certificates only.

---

**Q25. The DigiNotar incident in 2011 is the
most cited example of a CA compromise. What
was the primary real-world harm caused?**

- A) DigiNotar issued fraudulent code-signing
     certificates used to distribute malware
     to Windows users
- B) DigiNotar's fraudulent certificates were
     used to perform MITM attacks on Iranian
     users accessing Gmail ✅
- C) DigiNotar accidentally revoked thousands
     of legitimate certificates — causing
     widespread HTTPS outages
- D) DigiNotar issued certificates with weak
     512-bit RSA keys that were factored by
     researchers

> **Explanation:**
> - ✅ **B — MITM against Iranian Gmail users:**
>   In 2011, attackers compromised DigiNotar's
>   systems and issued 500+ fraudulent certificates
>   including one for google.com. This certificate
>   was used to perform **Man-in-the-Middle attacks
>   against Iranian users** accessing Gmail —
>   intercepting their communications. After
>   discovery, all major browsers removed DigiNotar
>   from their trust stores, making ALL DigiNotar
>   certificates immediately untrusted. DigiNotar
>   subsequently went bankrupt.
> - ❌ **A:** DigiNotar's fraudulent certificates
>   were primarily domain certificates (for HTTPS
>   MITM) — not code-signing certificates. The
>   Flame malware used MD5-based Microsoft code
>   signing — a separate incident involving a
>   different attack vector.
> - ❌ **C:** DigiNotar did not accidentally revoke
>   certificates — it was an attacker who used
>   the fraudulent certificates to harm users.
>   The harm was active MITM interception, not
>   erroneous revocation.
> - ❌ **D:** The DigiNotar breach was about
>   issuance of fraudulent certificates through
>   compromised CA systems — not about weak key
>   sizes. The FREAK attack involved 512-bit RSA
>   export keys — a completely separate incident.

---

## 📊 Answer Key — Quick Reference

| Q | Answer | Topic |
|---|--------|-------|
| 1 | C | CA primary role — issue and sign certificates |
| 2 | C | Root CA = self-signed trust anchor |
| 3 | B | Root CA offline — compromise would collapse hierarchy |
| 4 | C | Intermediate CA — blast radius containment |
| 5 | B | CA/Browser Forum — voluntary consortium |
| 6 | C | FIPS 140-2 Level 3 for CA HSM |
| 7 | C | Hierarchical model for HTTPS |
| 8 | B | Web of Trust — 1 full trust OR 3 marginal |
| 9 | B | Trust Store — pre-installed Root CA certs |
| 10 | B | Bridge CA — reduces cross-certification count |
| 11 | C | DV — domain only, no org info |
| 12 | C | HTTP file challenge — CA/BF approved DV method |
| 13 | C | ACME = RFC 8555 — automated cert issuance |
| 14 | C | Let's Encrypt 90 days — automation + security |
| 15 | C | 398 days max since September 2020 |
| 16 | B | CRL = signed list of revoked serial numbers |
| 17 | C | Private key compromise = most critical reason |
| 18 | B | OCSP = real-time per-cert vs CRL = full list |
| 19 | B | OCSP Stapling = server pre-fetches OCSP response |
| 20 | B | Soft fail = accept cert if OCSP unreachable |
| 21 | B | CCA = India PKI licensing body (IT Act 2000) |
| 22 | B | RCAI = India Root CA, operated by CCA |
| 23 | C | QES = handwritten signature equivalent (eIDAS) |
| 24 | B | certificateHold = temporary — can be unrevoked |
| 25 | B | DigiNotar = MITM against Iranian Gmail users |

---

## 📋 Topic Coverage Map

| Q | Concept Tested | Source |
|---|----------------|--------|
| 1 | CA primary role — issue and sign | Core |
| 2 | Root CA = self-signed trust anchor | Core |
| 3 | Root CA kept offline — catastrophic compromise | Core |
| 4 | Intermediate CA — blast radius containment | Core |
| 5 | CA/Browser Forum — purpose and nature | Core |
| 6 | FIPS 140-2 Level 3 for CA key protection | Core |
| 7 | Hierarchical trust model for public HTTPS | Core |
| 8 | Web of Trust trust calculation | Core |
| 9 | Trust Store definition | Core |
| 10 | Bridge CA — scalability solution | Core |
| 11 | DV certificate — domain only validation | Core |
| 12 | CA/BF approved DV method — HTTP challenge | Core |
| 13 | ACME protocol — RFC 8555 | Core |
| 14 | Let's Encrypt 90-day validity rationale | Core |
| 15 | 398-day maximum validity since Sep 2020 | Core |
| 16 | CRL definition and content | Core |
| 17 | Private key compromise = most critical revocation | Core |
| 18 | OCSP vs CRL comparison | Core |
| 19 | OCSP Stapling — server prefetches | Core |
| 20 | Soft fail — browsers accept if OCSP fails | Core |
| 21 | CCA = India PKI licensing body | Extra Notes |
| 22 | RCAI = India Root CA operated by CCA | Extra Notes |
| 23 | eIDAS QES = legally equivalent to handwritten sig | Extra Notes |
| 24 | certificateHold = temporary revocation | Extra Notes |
| 25 | DigiNotar 2011 — MITM against Iranian users | Extra Notes |

---