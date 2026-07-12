# MCQ Session 09 — Aadhaar, e-Sign &
Timestamping Services

## 📑 Table of Contents
- [Instructions](#instructions)
- [MCQs 1–7 — Aadhaar](#mcqs-17--aadhaar)
- [MCQs 8–14 — e-Sign](#mcqs-814--e-sign)
- [MCQs 15–20 — Timestamping Services](#mcqs-1520--timestamping-services)
- [MCQs 21–25 — Extra Notes: VID, e-KYC,
  LTV, PAdES](#mcqs-2125--extra-notes-vid-e-kyc-ltv-pades)
- [Answer Key](#-answer-key--quick-reference)
- [Topic Coverage Map](#-topic-coverage-map)

---

## Instructions

- 25 MCQs — drawn from core syllabus AND
  📌 Extra Notes of Session 09
- Foundation + Fundamental + Basic Concepts ONLY
- 4 options per question
- ✅ marks the correct answer
- Full explanation after every question including
  why each wrong option is wrong
- Wrong options look reasonable to someone unprepared
- Correct answer is clear to someone with solid basics

---

## MCQs 1–7 — Aadhaar

---

**Q1. What is Aadhaar and which authority
issues it?**

- A) A 10-digit tax identification number issued
     by the Income Tax Department of India
- B) A 12-digit unique identification number
     issued to residents of India by UIDAI ✅
- C) A 16-digit bank account number issued by
     the Reserve Bank of India
- D) A 12-digit passport number issued by the
     Ministry of External Affairs

> **Explanation:**
> - ✅ **B:** Aadhaar is a **12-digit** unique
>   identification number issued to every resident
>   of India by **UIDAI (Unique Identification
>   Authority of India)**. It captures demographic
>   data (name, DOB, address) and biometric data
>   (10 fingerprints, 2 iris scans, photograph).
>   It is the world's largest biometric identity
>   system with 1.4+ billion enrollments.
> - ❌ **A:** The 10-digit tax identification number
>   is the **PAN (Permanent Account Number)** issued
>   by the Income Tax Department — not Aadhaar.
>   Aadhaar is 12 digits and issued by UIDAI.
> - ❌ **C:** A 16-digit number used for banking
>   is a credit/debit card number or similar
>   financial identifier — not Aadhaar. RBI does
>   not issue biometric identity numbers. Also,
>   VID (Virtual ID) is 16 digits but is derived
>   from Aadhaar — not issued by RBI.
> - ❌ **D:** Passport numbers are issued by the
>   Ministry of External Affairs and are alphanumeric
>   (not 12 digits). Aadhaar is entirely numeric
>   and issued by UIDAI — a completely different
>   authority with a different purpose.

---

**Q2. What does UIDAI return to an Authentication
User Agency (AUA) when a resident successfully
completes basic Aadhaar authentication?**

- A) The resident's full biometric data —
     fingerprints and iris scans
- B) The resident's demographic data — name,
     address, date of birth, and photograph
- C) Only a YES or NO response — confirming
     or denying the authentication ✅
- D) The resident's 12-digit Aadhaar number
     along with their registered mobile number

> **Explanation:**
> - ✅ **C — YES or NO only:** For basic Aadhaar
>   authentication, UIDAI returns ONLY a YES
>   (authenticated) or NO (not authenticated)
>   response to the AUA. No biometric data,
>   no demographic data, and no Aadhaar number
>   is sent to the AUA. This data minimization
>   design protects resident privacy.
> - ❌ **A:** Biometric data (fingerprints, iris)
>   NEVER leaves UIDAI's CIDR. The entire
>   architecture is designed so that AUAs submit
>   biometric data for matching and receive only
>   a match result — raw biometric data is never
>   shared with AUAs.
> - ❌ **B:** Demographic data is returned ONLY
>   for **e-KYC** service — a separate, higher-
>   privilege service requiring explicit resident
>   consent and KUA authorization. Basic
>   authentication returns only YES/NO.
> - ❌ **D:** The Aadhaar number itself is not
>   returned by UIDAI to the AUA — the AUA already
>   has the number (the resident provided it to
>   initiate authentication). UIDAI confirms
>   whether the authentication matches — it does
>   not echo back the Aadhaar number.

---

**Q3. Which central database stores all Aadhaar
numbers along with associated biometric and
demographic data?**

- A) NATGRID (National Intelligence Grid)
- B) CIDR (Central Identities Data Repository) ✅
- C) CIBIL (Credit Information Bureau India)
- D) DigiLocker (Digital Document Repository)

> **Explanation:**
> - ✅ **B — CIDR:** The **Central Identities Data
>   Repository (CIDR)** is UIDAI's central database
>   that stores all Aadhaar numbers along with
>   associated biometric (fingerprints, iris, photo)
>   and demographic (name, DOB, address) data. It
>   is operated exclusively by UIDAI and is the
>   most sensitive database in India's digital
>   infrastructure.
> - ❌ **A — NATGRID:** NATGRID is a national
>   intelligence database for law enforcement —
>   not the Aadhaar identity database. It
>   aggregates data from various agencies but
>   is a separate system entirely.
> - ❌ **C — CIBIL:** CIBIL is a credit bureau
>   (Credit Information Bureau India Limited) —
>   it stores credit history and repayment records
>   of individuals and companies. It has nothing
>   to do with biometric identity data.
> - ❌ **D — DigiLocker:** DigiLocker is a cloud
>   platform for storing and sharing digital
>   documents (certificates, licenses). It is
>   linked to Aadhaar for authentication but is
>   NOT the database storing Aadhaar biometric
>   data. DigiLocker stores documents — CIDR
>   stores Aadhaar identity records.

---

**Q4. Which legislation primarily governs the
Aadhaar system in India?**

- A) Information Technology Act 2000
- B) Right to Information Act 2005
- C) Aadhaar (Targeted Delivery of Financial
     and Other Subsidies, Benefits and Services)
     Act 2016 ✅
- D) Personal Data Protection Act 2023

> **Explanation:**
> - ✅ **C — Aadhaar Act 2016:** The **Aadhaar
>   (Targeted Delivery of Financial and Other
>   Subsidies, Benefits and Services) Act 2016**
>   is the primary legislation governing the
>   Aadhaar system. It establishes UIDAI as a
>   statutory authority, defines the purposes
>   for which Aadhaar can be used, and sets the
>   framework for enrollment, authentication,
>   and data protection.
> - ❌ **A — IT Act 2000:** The IT Act governs
>   digital signatures, electronic records, and
>   cybercrime in India. It is relevant to e-Sign
>   (which uses Aadhaar) but it is NOT the primary
>   law governing the Aadhaar system itself.
> - ❌ **B — RTI Act 2005:** The Right to
>   Information Act enables citizens to request
>   government information — it has no relationship
>   to Aadhaar enrollment, authentication, or
>   the UIDAI framework.
> - ❌ **D — PDPA 2023:** India's Personal Data
>   Protection Act is a general data protection
>   law — it applies broadly to personal data
>   processing. While it affects how Aadhaar
>   data must be protected, the primary law
>   governing the Aadhaar system specifically
>   is the Aadhaar Act 2016.

---

**Q5. An Authentication User Agency (AUA) wants
to use Aadhaar authentication for their banking
application. Which entity serves as the technical
intermediary connecting the AUA to UIDAI's CIDR?**

- A) ESP (e-Sign Service Provider)
- B) KUA (KYC User Agency)
- C) ASA (Authentication Service Agency) ✅
- D) TSA (Time Stamp Authority)

> **Explanation:**
> - ✅ **C — ASA:** The **Authentication Service
>   Agency (ASA)** is the technical intermediary
>   that connects AUAs to UIDAI's CIDR. AUAs
>   route their authentication requests through
>   ASAs — which handle the secure connectivity,
>   encryption standards, and technical compliance
>   required to communicate with CIDR. Not all
>   AUAs have direct connectivity to CIDR — they
>   use an ASA as a gateway.
> - ❌ **A — ESP:** An e-Sign Service Provider
>   is specifically involved in the e-Sign service —
>   issuing one-time certificates for digital
>   signing after Aadhaar authentication. It is
>   not a general authentication intermediary
>   between AUAs and CIDR.
> - ❌ **B — KUA:** A KYC User Agency is authorized
>   to receive e-KYC data (demographic information)
>   from UIDAI — it is not the intermediary for
>   basic authentication connectivity. KUA is a
>   separate privilege for organizations that
>   need identity data beyond YES/NO.
> - ❌ **D — TSA:** A Time Stamp Authority issues
>   trusted timestamps for digital documents —
>   it has no role in Aadhaar authentication
>   infrastructure.

---

**Q6. Aadhaar supports multiple authentication
modes. Which mode is used when a resident
receives a code on their registered mobile
number to verify their identity?**

- A) Biometric Authentication — fingerprint scan
- B) Demographic Authentication — name and
     address matching
- C) OTP Authentication — one-time password
     sent to registered mobile ✅
- D) Certificate Authentication — using a
     digital signature certificate

> **Explanation:**
> - ✅ **C — OTP Authentication:** OTP (One-Time
>   Password) authentication sends a time-limited
>   unique code to the resident's Aadhaar-registered
>   mobile number. The resident enters this OTP in
>   the application — which forwards it to UIDAI
>   for verification. This is the most commonly
>   used Aadhaar authentication mode (including
>   for e-Sign).
> - ❌ **A — Biometric Authentication:** Biometric
>   authentication uses fingerprint or iris scans —
>   not a code sent to a mobile. It requires
>   biometric capture hardware (fingerprint scanner
>   or iris scanner) and is used for in-person
>   authentication (ration shops, pension counters).
> - ❌ **B — Demographic Authentication:** Demographic
>   authentication matches name, DOB, or address
>   against CIDR records — it does not involve
>   a mobile OTP. It is used for low-assurance
>   verification scenarios.
> - ❌ **D — Certificate Authentication:** Aadhaar
>   does not have a "certificate authentication"
>   mode — digital certificates are part of DSC/
>   e-Sign infrastructure, not a direct Aadhaar
>   authentication mode.

---

**Q7. The Indian Supreme Court ruled on the
constitutional validity of Aadhaar in which
year, and what was the key restriction placed
on its use?**

- A) 2016 — private companies were permitted to
     mandate Aadhaar for all their services
- B) 2018 — Aadhaar was upheld as constitutional
     but private companies cannot mandate it
     for their services ✅
- C) 2020 — Aadhaar was declared unconstitutional
     but permitted for government services only
- D) 2019 — Aadhaar was fully banned and then
     reinstated with new privacy protections

> **Explanation:**
> - ✅ **B — 2018 Puttaswamy ruling:** The Supreme
>   Court of India in the **Puttaswamy case (2018)**
>   upheld Aadhaar as constitutionally valid but
>   struck down the provision requiring private
>   companies to mandatorily collect Aadhaar.
>   The court ruled that Aadhaar can be mandatory
>   for government subsidies and benefits, income
>   tax PAN linking, and similar government
>   purposes — but private entities (banks, telecom)
>   cannot mandate it. The 2019 amendment later
>   permitted voluntary Aadhaar use by private
>   entities with resident consent.
> - ❌ **A:** This describes the situation BEFORE
>   the ruling — private companies were attempting
>   to mandate Aadhaar. The 2018 ruling restricted
>   this practice.
> - ❌ **C:** Aadhaar was NOT declared
>   unconstitutional — it was upheld. The court
>   only restricted mandatory private sector use.
> - ❌ **D:** Aadhaar was never "fully banned" —
>   the system continued to operate throughout.
>   The 2018 ruling placed restrictions; the
>   2019 amendment added voluntary private use
>   provisions.

---

## MCQs 8–14 — e-Sign

---

**Q8. What is e-Sign in the context of India's
digital services?**

- A) An electronic seal used by government
     departments to authenticate official documents
- B) An Aadhaar-based electronic signature
     service that allows signing documents without
     a physical USB token ✅
- C) A digital signature on emails using an
     S/MIME certificate stored on a smart card
- D) A biometric login system for government
     portals using Aadhaar fingerprint scan

> **Explanation:**
> - ✅ **B:** e-Sign is an **Aadhaar-based
>   electronic signature service** introduced by
>   MeitY and UIDAI in 2015. It allows any Aadhaar
>   holder to digitally sign documents using their
>   Aadhaar authentication (OTP or biometric) —
>   without needing to purchase or carry a physical
>   USB DSC token. A one-time certificate is issued
>   by a licensed ESP, used to sign, and then
>   destroyed.
> - ❌ **A:** Government departments do use digital
>   seals, but e-Sign is specifically a citizen-
>   facing signature service — not an internal
>   government sealing mechanism. e-Sign is for
>   individual signers, not organizational seals.
> - ❌ **C:** S/MIME email signing uses certificates
>   stored on smart cards or in software — this
>   is a traditional PKI mechanism, not e-Sign.
>   e-Sign is India's Aadhaar-specific service
>   using one-time certificates, not persistent
>   S/MIME certificates.
> - ❌ **D:** Biometric login for government portals
>   is Aadhaar authentication — a separate service.
>   e-Sign is specifically about SIGNING documents
>   (creating a digital signature on a file) —
>   not about logging into a portal.

---

**Q9. In the e-Sign workflow, which entity is
responsible for issuing the one-time Digital
Signature Certificate used for signing?**

- A) UIDAI directly — as part of the Aadhaar
     authentication response
- B) The applicant's bank — after verifying
     their bank account details
- C) The ESP (e-Sign Service Provider) —
     a CCA-licensed entity that issues the
     one-time certificate ✅
- D) The ASP (Application Service Provider)
     — the portal where signing takes place

> **Explanation:**
> - ✅ **C — ESP:** The **e-Sign Service Provider
>   (ESP)** is a CCA-licensed entity that:
>   (1) Receives the authentication result from
>   UIDAI, (2) Requests a one-time DSC from a
>   licensed CA, (3) Signs the document hash
>   using a private key generated in its HSM,
>   (4) Returns the digital signature to the ASP,
>   (5) Destroys the one-time private key.
>   The ESP is the core of the e-Sign service.
> - ❌ **A:** UIDAI only performs identity
>   authentication — it returns YES/NO to the ESP.
>   UIDAI does NOT issue digital certificates or
>   perform document signing. Certificate issuance
>   is handled by a CA working with the ESP.
> - ❌ **B:** Banks are AUAs (users of Aadhaar
>   authentication) — they use e-Sign but do not
>   issue certificates. Certificate issuance
>   requires a CCA-licensed CA and ESP — not a bank.
> - ❌ **D:** The ASP (Application Service Provider)
>   is the portal or application where the user
>   initiates signing (e.g., a tax portal). The
>   ASP coordinates the signing workflow but does
>   NOT issue certificates. It sends the document
>   hash to the ESP and embeds the returned
>   signature in the document.

---

**Q10. In the e-Sign process, what is sent from
the Application Service Provider (ASP) to the
ESP — and what is NOT sent?**

- A) The full document is sent — the hash is
     computed by the ESP internally
- B) Only the document hash is sent — the
     full document is NOT sent to the ESP ✅
- C) The document and the user's Aadhaar number
     are both sent to the ESP
- D) The user's private key is sent to the
     ESP for temporary storage during signing

> **Explanation:**
> - ✅ **B — Hash only:** Only the **document hash
>   (SHA-256)** is sent from the ASP to the ESP.
>   The full document NEVER leaves the user's
>   application. This is a critical privacy and
>   confidentiality design — the ESP never sees
>   the document content. The ESP signs the hash;
>   the ASP embeds the returned signature in the
>   original document.
> - ❌ **A:** The document itself is never sent to
>   the ESP. Sending the full document would violate
>   document confidentiality — especially for
>   sensitive personal documents like loan
>   agreements or tax returns. Only the hash is
>   needed for signing.
> - ❌ **C:** The Aadhaar number may be used for
>   authentication purposes, but the DOCUMENT is
>   not sent to the ESP. Sending both document
>   and Aadhaar number to the ESP would be a
>   serious privacy design flaw.
> - ❌ **D:** The user has NO private key to send —
>   in e-Sign, the private key is generated in
>   the ESP's HSM and never leaves it. The user
>   authenticates via Aadhaar OTP/biometric —
>   they are not involved in key management at all.

---

**Q11. Where is the private key stored and used
during an e-Sign operation?**

- A) On the user's smartphone — secured by
     a fingerprint lock
- B) In the ASP's server — encrypted with the
     user's Aadhaar number as the key
- C) In the ESP's Hardware Security Module (HSM)
     — the signer never holds the private key ✅
- D) In UIDAI's CIDR — alongside the resident's
     biometric data for security

> **Explanation:**
> - ✅ **C — ESP's HSM:** In e-Sign, a one-time
>   private key is generated WITHIN the ESP's
>   Hardware Security Module (HSM). The signing
>   operation (computing the digital signature)
>   happens inside the HSM. The private key is
>   then immediately destroyed after the signature
>   is created. The signer authenticates their
>   identity via Aadhaar — they never generate,
>   hold, or touch the private key.
> - ❌ **A:** There is no private key on the user's
>   smartphone. e-Sign was specifically designed
>   to eliminate the need for users to manage
>   private keys or tokens. The smartphone is
>   only used to receive and enter the OTP.
> - ❌ **B:** The ASP is the signing application
>   (e.g., a tax portal) — it does not hold
>   cryptographic keys for signing. The ASP only
>   coordinates the workflow — the ESP does the
>   actual signing.
> - ❌ **D:** CIDR stores biometric and demographic
>   identity data — not signing private keys.
>   UIDAI's role is authentication only; key
>   management is the ESP's responsibility.

---

**Q12. Which of the following correctly identifies
a key difference between e-Sign and a physical
Digital Signature Certificate (DSC)?**

- A) e-Sign uses stronger encryption than a
     physical DSC — making it more secure
- B) A physical DSC requires a USB token and
     works only on Windows — e-Sign works on
     mobile and web without a USB token ✅
- C) e-Sign is valid for 3 years — a physical
     DSC expires after one use
- D) A physical DSC uses Aadhaar authentication
     while e-Sign uses a username and password

> **Explanation:**
> - ✅ **B:** One of the most important practical
>   differences: a physical DSC requires a USB
>   dongle (token), works only on Windows (requires
>   drivers), and cannot be used on mobile devices.
>   e-Sign requires no USB token, works in web
>   browsers and mobile apps, and uses Aadhaar
>   OTP for authentication — making it accessible
>   to all Aadhaar holders regardless of device.
> - ❌ **A:** e-Sign uses the same standard
>   cryptographic algorithms (RSA/ECDSA with
>   SHA-256) as physical DSCs. Neither is
>   inherently "stronger" — they differ in
>   the key management model and accessibility,
>   not in cryptographic strength.
> - ❌ **C:** This completely inverts the facts.
>   e-Sign is a **one-time** signature — the
>   certificate is used once and destroyed.
>   A physical DSC is valid for **1 to 3 years**
>   and can be used repeatedly during that period.
> - ❌ **D:** This also inverts the facts. e-Sign
>   uses **Aadhaar authentication** (OTP or
>   biometric). A physical DSC uses a **PIN or
>   password** to unlock the USB token — Aadhaar
>   is not involved in physical DSC operation.

---

**Q13. Under the IT Act 2000, e-Sign is classified
as which type of signature — and how does this
differ from a physical DSC?**

- A) e-Sign is a Digital Signature — same
     classification as a physical DSC
- B) e-Sign is an Electronic Signature —
     a physical DSC is classified as a
     Digital Signature — different legal
     categories under the IT Act ✅
- C) e-Sign is a Qualified Electronic Signature
     under eIDAS — a physical DSC is a
     standard signature under IT Act
- D) e-Sign and physical DSC have no legal
     classification — both are simply
     "digital marks" under Indian law

> **Explanation:**
> - ✅ **B:** Under the IT Act 2000, these are
>   two distinct legal categories:
>   **Digital Signature** — created using an
>   asymmetric key pair certified by a licensed
>   CA (physical DSC on USB token).
>   **Electronic Signature** — a broader category
>   that includes Aadhaar-based e-Sign. Both
>   are legally valid for most purposes, but
>   physical DSC (Digital Signature) is considered
>   a higher class and required for some specific
>   high-value government transactions like
>   Class 3 e-tendering.
> - ❌ **A:** e-Sign is NOT classified as a Digital
>   Signature under the IT Act — it is an Electronic
>   Signature. Calling them the same ignores the
>   specific legal distinction the IT Act makes.
> - ❌ **C:** QES is an eIDAS (EU) classification —
>   not applicable to India's IT Act framework.
>   India's IT Act has its own signature categories
>   (Electronic Signature, Digital Signature) that
>   are different from eIDAS categories.
> - ❌ **D:** Both have specific legal classifications
>   under the IT Act. The IT Act is precise about
>   these categories — they are not informally
>   termed "digital marks."

---

**Q14. Which of the following transactions CANNOT
use e-Sign or a physical DSC under the IT Act
2000?**

- A) Filing Income Tax Returns (ITR)
- B) Signing a loan agreement with a bank
- C) Signing the sale deed for a property
     transaction ✅
- D) Filing GST returns with the government

> **Explanation:**
> - ✅ **C — Property sale deed:** The IT Act 2000
>   explicitly excludes **sale of immovable property**
>   from the category of transactions that can be
>   completed using electronic or digital signatures.
>   Property sale deeds must be executed on stamp
>   paper with physical signatures and registered
>   under the Registration Act 1908. e-Sign and
>   DSC cannot substitute for this.
> - ❌ **A:** Filing ITR is one of the most common
>   uses of e-Sign in India — taxpayers sign their
>   Income Tax Returns using Aadhaar OTP-based
>   e-Sign. This is a valid and widely used
>   application of e-Sign.
> - ❌ **B:** Loan agreements are legally executable
>   using e-Sign — banks across India use e-Sign
>   for digital loan documentation, making the
>   process fully paperless on mobile.
> - ❌ **D:** GST returns are filed electronically
>   using e-Sign or physical DSC — this is a
>   primary use case for both signature types
>   in India's tax compliance ecosystem.

---

## MCQs 15–20 — Timestamping Services

---

**Q15. What is the purpose of trusted
timestamping in the context of digital
signatures?**

- A) To encrypt the document with a time-based
     key that automatically expires after a
     set period
- B) To speed up the digital signature
     verification process by caching time values
- C) To create a cryptographically signed proof
     that specific data existed at a specific
     point in time ✅
- D) To automatically renew a digital signature
     certificate when it is about to expire

> **Explanation:**
> - ✅ **C:** Trusted timestamping creates a
>   **tamper-proof, cryptographically signed
>   record** (issued by a trusted third party —
>   the TSA) proving that specific data (identified
>   by its hash) existed at the stated time.
>   Unlike a file's "last modified" date (trivially
>   changeable), a trusted timestamp cannot be
>   forged without breaking the TSA's digital
>   signature.
> - ❌ **A:** Timestamping does not encrypt documents
>   with time-based keys — it creates a signed
>   proof of existence. Encryption and timestamping
>   are separate security mechanisms serving
>   different purposes.
> - ❌ **B:** Timestamping does not optimize
>   verification speed — it adds an additional
>   verification step (checking the TSA signature).
>   Speed optimization is not its purpose.
> - ❌ **D:** Certificate renewal is a separate PKI
>   process — the applicant requests a new certificate
>   from the CA before the current one expires.
>   Timestamping does not automate or trigger
>   renewal — it is about proving WHEN a signature
>   was created, not about renewing certificates.

---

**Q16. Which RFC defines the Time Stamp Protocol
(TSP) used for trusted timestamping?**

- A) RFC 2104
- B) RFC 5280
- C) RFC 8555
- D) RFC 3161 ✅

> **Explanation:**
> - ✅ **D — RFC 3161:** The **Time Stamp Protocol
>   (TSP)** is defined in **RFC 3161** (published
>   in 2001), updated by RFC 5816 (2010). It
>   defines the format of timestamp requests
>   (TimeStampReq/TSQ), responses (TimeStampResp/
>   TSR), and the structure of the Time Stamp
>   Token (TST) itself.
> - ❌ **A — RFC 2104:** This defines **HMAC** —
>   the Hash-based Message Authentication Code.
>   Completely unrelated to timestamping.
> - ❌ **B — RFC 5280:** This defines the **Internet
>   X.509 PKI Certificate and CRL Profile (PKIX)**
>   — the foundational reference for X.509
>   certificate validation. Not the timestamp
>   protocol.
> - ❌ **C — RFC 8555:** This defines **ACME** —
>   the Automatic Certificate Management
>   Environment protocol used by Let's Encrypt
>   for automated certificate issuance. Unrelated
>   to timestamping.

---

**Q17. In the Time Stamp Protocol (TSP), what
does the client send to the Time Stamp Authority
(TSA), and why?**

- A) The full document — so the TSA can verify
     its contents before timestamping
- B) The hash of the document — because the
     TSA only needs the hash to create a proof
     of existence, protecting document
     confidentiality ✅
- C) The document's digital signature — so
     the TSA can embed it in the timestamp
- D) The document encrypted with the TSA's
     public key — for secure timestamping

> **Explanation:**
> - ✅ **B — Hash only:** The client sends only the
>   **hash of the document** (e.g., SHA-256) to
>   the TSA — not the document itself. The TSA
>   doesn't need the content — it only needs to
>   sign "this hash existed at this time." This
>   design protects document confidentiality:
>   the TSA never sees the document content.
>   The TSA signs (Hash + current time) to
>   create the Time Stamp Token (TST).
> - ❌ **A:** Sending the full document would violate
>   confidentiality — especially for sensitive
>   contracts, legal documents, or personal files.
>   The TSP specifically requires only the hash
>   to be sent. The TSA has no need to read or
>   process the content.
> - ❌ **C:** The digital signature is created
>   separately from the timestamp — they are
>   two different operations. The client sends
>   the document hash for timestamping; the
>   digital signature is a separate cryptographic
>   operation by the signer.
> - ❌ **D:** There is no document encryption to
>   the TSA. The hash is sent in plain form —
>   it is not a secret (the hash of a public
>   document is not sensitive). The TSA's role
>   is to sign the hash + time, not to decrypt
>   anything.

---

**Q18. What does a Time Stamp Token (TST)
contain that makes it a trusted proof of
existence?**

- A) The full document content + timestamp +
     user's Aadhaar number
- B) The hash of the document + the time of
     timestamping + the TSA's digital signature ✅
- C) The user's private key + timestamp +
     the CA's certificate
- D) An encrypted copy of the document +
     the TSA's public key

> **Explanation:**
> - ✅ **B:** A Time Stamp Token (TST) contains
>   three essential elements that together create
>   tamper-proof evidence:
>   (1) **The hash (messageImprint)** — identifies
>   the specific data being timestamped,
>   (2) **genTime** — the exact UTC time the TSA
>   created the token,
>   (3) **TSA's digital signature** over all the
>   above — cryptographically binding the hash to
>   the time. The signature ensures the TST cannot
>   be forged or altered.
> - ❌ **A:** The full document is NEVER in the
>   TST — only its hash. Aadhaar numbers are
>   unrelated to timestamping — TSP works
>   independently of Aadhaar.
> - ❌ **C:** The user's private key is never
>   included in any certificate or token — this
>   would be a catastrophic security failure.
>   The TST contains the TSA's signature (created
>   with the TSA's private key) — not the signer's
>   private key.
> - ❌ **D:** Encrypted document copies and public
>   keys are not TST content. The TST is a signed
>   data structure — not an encrypted document.
>   Encryption and timestamping serve different
>   purposes.

---

**Q19. Why is trusted timestamping important
for digital signatures on software (code
signing)?**

- A) Timestamps ensure that software cannot
     be executed after a specific date —
     implementing license expiry
- B) Timestamps allow the software to verify
     its own integrity each time it is run
- C) A timestamp proves the code was signed
     while the certificate was valid —
     keeping the signature trusted even after
     the certificate expires ✅
- D) Timestamps encrypt the software so that
     only authorized systems can execute it

> **Explanation:**
> - ✅ **C:** In code signing, if a developer signs
>   software in 2024 and their certificate expires
>   in 2025, a user running the software in 2027
>   would see an "invalid certificate" error —
>   making the software appear untrusted. With a
>   **trusted timestamp** from 2024 (when the cert
>   was valid), the verifier can confirm the
>   signature was created during the certificate's
>   validity period — the signature remains trusted
>   despite the certificate now being expired.
> - ❌ **A:** Timestamps do not implement license
>   expiry or prevent software execution after a
>   date. They serve as backward-looking proof
>   (this was signed at time T) — not forward-
>   looking restrictions (cannot run after time T).
>   Software licensing is a separate mechanism.
> - ❌ **B:** Software integrity checking at runtime
>   uses hash verification — comparing the software's
>   current hash against a known-good value. This
>   is a different mechanism from timestamping
>   which is about WHEN a signature was created.
> - ❌ **D:** Timestamps do not encrypt software.
>   They add a cryptographic time proof to a
>   signature — not encryption. Encrypted software
>   distribution uses DRM or secure delivery
>   mechanisms, not timestamps.

---

**Q20. Which Extended Key Usage (EKU) value in
a certificate indicates it is specifically
authorized to issue trusted timestamps?**

- A) serverAuth — for TLS server authentication
- B) codeSigning — for software code signing
- C) emailProtection — for S/MIME email signing
- D) timeStamping — specifically for TSA
     certificate authorization ✅

> **Explanation:**
> - ✅ **D — timeStamping:** A TSA (Time Stamp
>   Authority) certificate must have the EKU value
>   **timeStamping** (OID: 1.3.6.1.5.5.7.3.8).
>   This EKU specifically designates the certificate
>   as authorized to sign Time Stamp Tokens.
>   Verifiers check this EKU when validating a
>   TST — if the TSA cert doesn't have this EKU,
>   the timestamp is not considered valid.
> - ❌ **A — serverAuth:** serverAuth EKU is for
>   TLS server certificates — it authorizes the
>   certificate to authenticate a web server to
>   browsers. It has no relation to timestamping.
> - ❌ **B — codeSigning:** codeSigning EKU is for
>   software code signing certificates — authorizing
>   signing of executable files and scripts. A TSA
>   certificate for timestamping code signatures
>   uses the timeStamping EKU — not codeSigning.
> - ❌ **C — emailProtection:** emailProtection EKU
>   is for S/MIME certificates used for signing
>   and encrypting emails. It does not authorize
>   a certificate to act as a TSA.

---

## MCQs 21–25 — Extra Notes: VID, e-KYC,
LTV, PAdES

---

**Q21. What is a Virtual ID (VID) in the Aadhaar
system, and what privacy problem does it solve?**

- A) VID is an alternate name for the Aadhaar
     number — a 12-digit identifier used on
     government documents
- B) VID is a temporary 16-digit number generated
     by UIDAI that acts as a proxy for the Aadhaar
     number — preventing AUAs from knowing the
     actual Aadhaar number ✅
- C) VID is a one-time password used in place
     of biometric authentication for high-risk
     transactions
- D) VID is a virtual bank account number linked
     to Aadhaar for Direct Benefit Transfer

> **Explanation:**
> - ✅ **B — VID:** The **Virtual ID (VID)** is a
>   temporary **16-digit** number (compared to
>   Aadhaar's 12 digits) generated by the resident
>   through UIDAI's portal or mAadhaar app. It maps
>   to the Aadhaar number at UIDAI's level — but
>   AUAs only see the VID, not the actual Aadhaar
>   number. Since VID can be regenerated (making the
>   old one invalid), it prevents AUAs from using
>   the Aadhaar number to track a person across
>   multiple services.
> - ❌ **A:** VID is NOT the same as the Aadhaar
>   number — they are different numbers with
>   different lengths (16 vs 12 digits). The VID
>   was specifically created to be different from
>   the Aadhaar number to enhance privacy.
> - ❌ **C:** VID is not a one-time password —
>   it is a persistent (but revocable) identifier
>   that can be used multiple times until the
>   resident regenerates it. OTPs are separate
>   mechanisms used in OTP authentication mode.
> - ❌ **D:** VID has nothing to do with banking
>   or Direct Benefit Transfer. DBT uses the
>   Aadhaar-to-bank-account linking. VID is
>   specifically a privacy tool for Aadhaar
>   authentication — not a financial account number.

---

**Q22. What is Aadhaar e-KYC and how does it
differ from basic Aadhaar authentication?**

- A) e-KYC is the same as basic authentication —
     both return only YES or NO to the requesting
     organization
- B) e-KYC is a service where UIDAI returns
     the resident's demographic data (name,
     address, photo) after successful authentication
     — with consent — unlike basic auth which
     returns only YES/NO ✅
- C) e-KYC involves sending the resident's
     physical ID documents to UIDAI for
     digital verification
- D) e-KYC is an offline process where residents
     visit a UIDAI centre to complete identity
     verification in person

> **Explanation:**
> - ✅ **B — e-KYC returns demographic data:**
>   **e-KYC (electronic Know Your Customer)** goes
>   beyond YES/NO — after successful Aadhaar
>   authentication AND with the resident's explicit
>   consent, UIDAI returns demographic data
>   (name, address, date of birth, gender, photo)
>   to the authorized KUA. This enables banks,
>   telecom operators, and others to complete
>   customer KYC digitally — no physical documents
>   needed. Basic authentication only returns
>   YES/NO with no personal data.
> - ❌ **A:** e-KYC is specifically distinguished
>   from basic authentication by the fact that it
>   returns demographic data — not just YES/NO.
>   If it returned only YES/NO, it would be
>   identical to basic authentication and the
>   separate e-KYC service would be redundant.
> - ❌ **C:** Physical ID documents are not sent to
>   UIDAI in e-KYC — the entire point is to
>   eliminate physical document verification.
>   UIDAI already has the resident's verified data
>   from enrollment — it shares a subset with
>   the KUA after authentication.
> - ❌ **D:** e-KYC is a fully online, real-time
>   service — there is no need to visit a UIDAI
>   center. The resident authenticates from
>   wherever they are (using OTP on their mobile
>   or biometric capture) and the KUA receives
>   the data instantly.

---

**Q23. What is Long-Term Validation (LTV) in the
context of digital signatures?**

- A) LTV is a setting that extends a certificate's
     validity period beyond its original expiry date
- B) LTV is the process of embedding the certificate
     chain, revocation data, and timestamp into a
     signed document at the time of signing —
     enabling future validation without external
     queries ✅
- C) LTV is a backup mechanism that automatically
     re-signs documents if the original signature
     becomes invalid
- D) LTV is a log maintained by the CA of all
     long-term certificates it has issued

> **Explanation:**
> - ✅ **B — Embedding everything at signing time:**
>   LTV (Long-Term Validation) solves the problem
>   that future verifiers may not be able to access
>   old CRLs, OCSP services, or CA certificates
>   that have since gone offline. By embedding
>   at signing time:
>   (1) Full certificate chain (all CA certs),
>   (2) CRL or OCSP response proving cert was
>   valid when signed,
>   (3) Trusted timestamp proving when signing
>   occurred — a verifier decades later can
>   validate the signature purely from data inside
>   the document.
> - ❌ **A:** LTV does NOT extend certificate
>   validity periods — the certificate retains
>   its original expiry. LTV enables the signature
>   to be validated DESPITE the certificate being
>   expired — by proving it was valid at signing
>   time.
> - ❌ **C:** LTV does not automatically re-sign
>   documents — re-signing would be a completely
>   different operation requiring the original
>   signer's new key. LTV preserves the validity
>   of the ORIGINAL signature indefinitely.
> - ❌ **D:** LTV is not a CA log. It is a property
>   of the signed document — data embedded within
>   it. LTV is a format specification, not a
>   CA-maintained registry.

---

**Q24. PAdES signature profiles have levels such
as -B, -T, -LT, and -LTA. What additional
element does the -T level add over the
basic -B level?**

- A) -T adds the full certificate chain of
     all Intermediate CAs
- B) -T adds the revocation status information
     (CRL or OCSP response)
- C) -T adds a trusted timestamp from a TSA ✅
- D) -T adds an archive timestamp covering
     all previously embedded data

> **Explanation:**
> - ✅ **C — Trusted timestamp:** PAdES profile
>   levels build on each other:
>   **-B (Basic):** Signature + signing certificate
>   **-T (Timestamp):** -B + a trusted timestamp
>   from a TSA (proving WHEN the document was signed)
>   **-LT (Long-Term):** -T + certificate chain +
>   revocation data
>   **-LTA (Long-Term Archive):** -LT + additional
>   archive timestamp
>   The -T level adds ONLY the trusted timestamp
>   over the -B baseline.
> - ❌ **A:** The full certificate chain is added
>   at the **-LT level** — not -T. At -T, only
>   the timestamp is added. Certificate chain
>   embedding comes in the next level.
> - ❌ **B:** Revocation data (CRL or OCSP response)
>   is also added at the **-LT level** — alongside
>   the certificate chain. The -T level specifically
>   adds only the trusted timestamp.
> - ❌ **D:** An archive timestamp covering all
>   previously embedded data is the defining
>   feature of the **-LTA level** — the highest
>   profile. This is different from the -T
>   timestamp which only covers the signature.

---

**Q25. Aadhaar's biometric lock feature allows
residents to lock their biometric data. What
happens to OTP-based authentication when
biometric data is locked?**

- A) All Aadhaar authentication is completely
     disabled — both biometric and OTP stop
     working
- B) OTP-based authentication continues to
     work normally — only biometric authentication
     is disabled ✅
- C) OTP authentication requires an additional
     PIN when biometrics are locked
- D) Biometric lock automatically switches
     all authentication to facial recognition

> **Explanation:**
> - ✅ **B — OTP still works:** Aadhaar's biometric
>   lock is a **partial lock** — it specifically
>   disables fingerprint and iris authentication
>   while leaving OTP-based authentication fully
>   functional. This is useful for residents who
>   want to prevent unauthorized biometric use
>   (e.g., at ration shops) while still being
>   able to authenticate using their mobile
>   for online services (banking, e-Sign).
> - ❌ **A:** Biometric lock does NOT disable all
>   authentication. If it completely disabled
>   all authentication, residents with biometric
>   lock enabled could not use any Aadhaar-based
>   service — which would be counterproductive.
>   UIDAI designed it to block only biometric
>   methods while preserving OTP access.
> - ❌ **C:** No additional PIN is required for
>   OTP authentication when biometrics are locked.
>   OTP authentication follows its standard flow —
>   enter Aadhaar/VID number, receive OTP, enter
>   OTP. No extra step is added due to biometric
>   lock status.
> - ❌ **D:** Facial recognition is not an Aadhaar
>   authentication mode (though photo is stored
>   in CIDR). Biometric lock does not redirect
>   authentication to facial recognition —
>   it simply disables fingerprint and iris
>   modalities while preserving OTP.

---

## 📊 Answer Key — Quick Reference

| Q | Answer | Topic |
|---|--------|-------|
| 1 | B | Aadhaar — 12-digit number issued by UIDAI |
| 2 | C | UIDAI returns only YES/NO for basic auth |
| 3 | B | CIDR — central biometric database |
| 4 | C | Aadhaar Act 2016 — primary legislation |
| 5 | C | ASA — technical intermediary for AUAs |
| 6 | C | OTP authentication mode |
| 7 | B | SC ruling 2018 — private companies cannot mandate |
| 8 | B | e-Sign — Aadhaar-based signature without USB token |
| 9 | C | ESP — issues one-time certificate |
| 10 | B | Only hash sent to ESP — not full document |
| 11 | C | Private key in ESP's HSM — signer never holds it |
| 12 | B | Physical DSC needs USB + Windows; e-Sign works on mobile |
| 13 | B | e-Sign = Electronic Signature; DSC = Digital Signature |
| 14 | C | Property sale cannot use e-Sign/DSC |
| 15 | C | Trusted timestamp = signed proof of existence at a time |
| 16 | D | RFC 3161 = Time Stamp Protocol |
| 17 | B | Client sends hash — not full document |
| 18 | B | TST = hash + genTime + TSA signature |
| 19 | C | Timestamp keeps code signature valid after cert expiry |
| 20 | D | timeStamping EKU for TSA certificates |
| 21 | B | VID = 16-digit temporary proxy for Aadhaar number |
| 22 | B | e-KYC returns demographic data with consent |
| 23 | B | LTV embeds chain + revocation + timestamp at signing |
| 24 | C | PAdES -T adds trusted timestamp over -B |
| 25 | B | Biometric lock disables biometric only — OTP still works |

---

## 📋 Topic Coverage Map

| Q | Concept Tested | Source |
|---|----------------|--------|
| 1 | Aadhaar — 12 digits, issued by UIDAI | Core |
| 2 | UIDAI returns YES/NO only for basic auth | Core |
| 3 | CIDR — central Aadhaar database | Core |
| 4 | Aadhaar Act 2016 — primary legislation | Core |
| 5 | ASA — intermediary between AUA and CIDR | Core |
| 6 | OTP authentication mode | Core |
| 7 | SC ruling 2018 — Puttaswamy case | Core |
| 8 | e-Sign definition and purpose | Core |
| 9 | ESP — issues one-time certificate | Core |
| 10 | Only hash sent to ESP — document confidentiality | Core |
| 11 | Private key in ESP HSM — signer never holds it | Core |
| 12 | Physical DSC vs e-Sign practical differences | Core |
| 13 | e-Sign = Electronic Sig; DSC = Digital Sig | Core |
| 14 | IT Act exclusions — property sale | Core |
| 15 | Trusted timestamping purpose | Core |
| 16 | RFC 3161 = TSP | Core |
| 17 | Hash only sent to TSA — document confidentiality | Core |
| 18 | TST contents — hash + time + TSA signature | Core |
| 19 | Timestamp keeps code signature valid after cert expiry | Core |
| 20 | timeStamping EKU for TSA certs | Core |
| 21 | VID — 16-digit privacy proxy | Extra Notes |
| 22 | e-KYC — returns demographic data with consent | Extra Notes |
| 23 | LTV — embed chain + revocation + timestamp | Extra Notes |
| 24 | PAdES -T adds timestamp over -B | Extra Notes |
| 25 | Biometric lock — OTP still works | Extra Notes |

---