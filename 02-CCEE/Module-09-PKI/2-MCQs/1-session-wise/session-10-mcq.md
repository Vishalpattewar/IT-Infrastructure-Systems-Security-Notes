# MCQ Session 10 — Public Key Cryptography
Standards (PKCS) & FIPS 140-2

## 📑 Table of Contents
- [Instructions](#instructions)
- [MCQs 1–8 — PKCS Standards](#mcqs-18--pkcs-standards)
- [MCQs 9–14 — Key PKCS Deep Dives](#mcqs-914--key-pkcs-deep-dives)
- [MCQs 15–20 — FIPS 140-2](#mcqs-1520--fips-140-2)
- [MCQs 21–25 — Extra Notes: Padding,
  Encoding, CMVP](#mcqs-2125--extra-notes-padding-encoding-cmvp)
- [Answer Key](#-answer-key--quick-reference)
- [Topic Coverage Map](#-topic-coverage-map)

---

## Instructions

- 25 MCQs — drawn from core syllabus AND
  📌 Extra Notes of Session 10
- Foundation + Fundamental + Basic Concepts ONLY
- 4 options per question
- ✅ marks the correct answer
- Full explanation after every question including
  why each wrong option is wrong
- Wrong options look reasonable to someone unprepared
- Correct answer is clear to someone with solid basics

---

## MCQs 1–8 — PKCS Standards

---

**Q1. What does PKCS stand for, and who
originally developed these standards?**

- A) Private Key Cryptographic Suite — developed
     by NIST as US federal standards
- B) Public Key Cryptography Standards —
     developed by RSA Security, now maintained
     as IETF RFCs ✅
- C) Public Key Certificate System — developed
     by ITU-T as X.500 directory standards
- D) Protected Key Communication Specification —
     developed by the NSA for government use

> **Explanation:**
> - ✅ **B:** PKCS stands for **Public Key
>   Cryptography Standards**. They were originally
>   developed by **RSA Security** (the company)
>   starting in 1991 to establish a common
>   framework for public key cryptography
>   interoperability. Most PKCS standards have
>   since been adopted and updated by IETF as
>   RFC documents.
> - ❌ **A:** PKCS was not developed by NIST —
>   it was developed by RSA Security. NIST
>   develops FIPS standards (like FIPS 197 for
>   AES) — separate from PKCS. "Private Key"
>   is also wrong — it's "Public Key."
> - ❌ **C:** ITU-T develops X.500 directory
>   services and X.509 certificate standards —
>   not PKCS. "Certificate System" is also
>   incorrect — PKCS covers more than just
>   certificates.
> - ❌ **D:** The NSA designs cryptographic
>   algorithms (SHA family, DES S-Boxes) —
>   not the PKCS format standards. "Protected
>   Key Communication Specification" is a
>   fabricated expansion.

---

**Q2. Which PKCS standard defines the format
for a Certificate Signing Request (CSR)
submitted to a CA?**

- A) PKCS#7
- B) PKCS#8
- C) PKCS#12
- D) PKCS#10 ✅

> **Explanation:**
> - ✅ **D — PKCS#10:** PKCS#10 (RFC 2986) defines
>   the **Certificate Signing Request** format —
>   the document an applicant sends to a CA
>   containing their public key, identity
>   information (DN), and a self-signature
>   (proof of possession). The PEM header is
>   `-----BEGIN CERTIFICATE REQUEST-----`.
> - ❌ **A — PKCS#7:** PKCS#7 (CMS) defines the
>   format for signed and encrypted messages —
>   used in S/MIME email and for distributing
>   certificate chains (.p7b files). It is NOT
>   the CSR format.
> - ❌ **B — PKCS#8:** PKCS#8 defines the format
>   for storing **private keys** (algorithm-
>   independent). PEM header: `BEGIN PRIVATE KEY`.
>   Not the CSR format.
> - ❌ **C — PKCS#12:** PKCS#12 defines the file
>   format for bundling a certificate + private
>   key + chain into a single password-protected
>   file (.pfx/.p12). Not the CSR format.

---

**Q3. A server administrator needs to export
a server's certificate AND its private key
together into a single file for backup.
Which PKCS standard defines this file format?**

- A) PKCS#7 (.p7b)
- B) PKCS#10 (.csr)
- C) PKCS#12 (.pfx / .p12) ✅
- D) PKCS#8 (.key)

> **Explanation:**
> - ✅ **C — PKCS#12:** PKCS#12 (RFC 7292)
>   defines the `.pfx` / `.p12` format that
>   bundles the certificate, private key, and
>   certificate chain into a single binary file.
>   It is always password-protected because it
>   contains the private key. This is the
>   standard format for certificate portability
>   across systems (Windows IIS, macOS, Java).
> - ❌ **A — PKCS#7 (.p7b):** A .p7b file
>   contains certificates and certificate chains
>   — but NO private key. It cannot be used to
>   back up or transfer a private key.
> - ❌ **B — PKCS#10 (.csr):** A CSR contains
>   the public key and identity information for
>   requesting a certificate — it does NOT
>   contain a certificate or private key.
> - ❌ **D — PKCS#8 (.key):** PKCS#8 stores
>   the private key only — not the certificate.
>   PKCS#12 is needed when both the certificate
>   AND the private key must be in one file.

---

**Q4. Which PKCS standard defines a standard
API for applications to interact with hardware
cryptographic tokens such as HSMs and smart
cards?**

- A) PKCS#5
- B) PKCS#11 ✅
- C) PKCS#12
- D) PKCS#3

> **Explanation:**
> - ✅ **B — PKCS#11:** PKCS#11 (also called
>   **Cryptoki** — Cryptographic Token Interface)
>   defines a standard programming interface
>   (API) that allows applications to communicate
>   with hardware cryptographic devices — HSMs,
>   smart cards, and USB tokens — without needing
>   device-specific code. Every major HSM vendor
>   (Thales, nCipher, SafeNet) provides a PKCS#11
>   library for their device.
> - ❌ **A — PKCS#5:** PKCS#5 defines
>   password-based cryptography — specifically
>   PBKDF1 and PBKDF2 for deriving encryption
>   keys from passwords. It is not an API for
>   hardware tokens.
> - ❌ **C — PKCS#12:** PKCS#12 is a file format
>   (.pfx/.p12) for bundling certificates and
>   private keys — not an API for hardware
>   cryptographic devices.
> - ❌ **D — PKCS#3:** PKCS#3 defines
>   Diffie-Hellman Key Agreement domain
>   parameters — not a hardware token API.

---

**Q5. PKCS#12 (.pfx) files must always be
password-protected. Why?**

- A) Because password protection speeds up
     the certificate verification process
- B) Because the CA requires a password when
     signing the certificate bundle
- C) Because PKCS#12 files contain the private
     key — without a password anyone who
     obtains the file can extract the key ✅
- D) Because PKCS#12 is a compressed format —
     the password is used as the compression key

> **Explanation:**
> - ✅ **C:** PKCS#12 files contain the
>   **private key** — the most sensitive
>   cryptographic material. If the .pfx file
>   has no password (or a weak password), any
>   attacker who obtains the file can immediately
>   extract the private key and impersonate
>   the certificate holder — signing malicious
>   content or performing MITM attacks on TLS.
>   The password triggers PKCS#5 PBKDF2
>   encryption of the private key inside the file.
> - ❌ **A:** Password protection does not speed
>   up anything — it actually adds a small
>   decryption overhead when importing the file.
>   Speed is not the reason for password
>   protection.
> - ❌ **B:** The CA has no involvement in
>   PKCS#12 creation — the administrator creates
>   the .pfx file themselves (e.g., using OpenSSL
>   `pkcs12 -export`). The CA only issues the
>   certificate — it does not package it into
>   PKCS#12.
> - ❌ **D:** PKCS#12 uses encryption (PKCS#5
>   PBKDF2 + AES) — not compression. The
>   password derives an encryption key — it is
>   not a compression parameter.

---

**Q6. Which PKCS standard defines PBKDF2 —
the function for deriving cryptographic keys
from passwords?**

- A) PKCS#1
- B) PKCS#3
- C) PKCS#5 ✅
- D) PKCS#11

> **Explanation:**
> - ✅ **C — PKCS#5:** PKCS#5 (RFC 8018) defines
>   **Password-Based Cryptography** — including
>   PBKDF1 (legacy) and **PBKDF2** (current
>   standard). PBKDF2 uses an HMAC-based pseudo-
>   random function, a password, a salt, and an
>   iteration count to derive a cryptographic key
>   of any length. Used in WPA2, PKCS#12, LUKS,
>   and many other applications.
> - ❌ **A — PKCS#1:** PKCS#1 defines RSA
>   cryptography — key formats, OAEP encryption
>   padding, and PSS signature padding. It has
>   nothing to do with password-based key
>   derivation.
> - ❌ **B — PKCS#3:** PKCS#3 defines
>   Diffie-Hellman Key Agreement parameters —
>   domain parameters for DH key exchange.
>   Not related to passwords.
> - ❌ **D — PKCS#11:** PKCS#11 is the API for
>   hardware cryptographic tokens. While HSMs
>   may implement PBKDF2 internally through
>   PKCS#11 calls, PKCS#11 itself does not
>   define PBKDF2 — that definition belongs
>   to PKCS#5.

---

**Q7. A certificate chain file containing
server certificate and Intermediate CA
certificate — but NO private key — is
distributed in which file format?**

- A) PKCS#12 (.pfx)
- B) PKCS#8 (.key)
- C) PKCS#7 (.p7b) ✅
- D) PKCS#10 (.csr)

> **Explanation:**
> - ✅ **C — PKCS#7 (.p7b):** A .p7b file uses
>   the PKCS#7 (CMS — Cryptographic Message
>   Syntax) format to distribute a certificate
>   or certificate chain. It can contain one or
>   more certificates (and optionally CRLs) but
>   does NOT contain a private key. Commonly
>   used on Windows to import a certificate chain.
> - ❌ **A — PKCS#12 (.pfx):** PKCS#12 DOES
>   contain the private key — which is exactly
>   what we want to avoid in this scenario. If
>   the goal is distributing only certificates
>   (no private key), PKCS#7 is the correct
>   format.
> - ❌ **B — PKCS#8 (.key):** PKCS#8 stores
>   a single private key — not a certificate
>   chain. It is the opposite of what is needed
>   here.
> - ❌ **D — PKCS#10 (.csr):** A CSR is a
>   certificate REQUEST — not an issued
>   certificate or a chain. It is submitted
>   TO a CA, not distributed as a certificate
>   chain.

---

**Q8. Which PKCS standard defines an
algorithm-independent format for storing
private keys — working for RSA, ECC, DSA,
and any other algorithm?**

- A) PKCS#1 — RSA Cryptography Standard
- B) PKCS#8 — Private Key Information Syntax ✅
- C) PKCS#10 — Certification Request Syntax
- D) PKCS#7 — Cryptographic Message Syntax

> **Explanation:**
> - ✅ **B — PKCS#8:** PKCS#8 (RFC 5958) defines
>   a generic, algorithm-independent private key
>   format. It stores the algorithm identifier
>   (OID) alongside the key data — so the same
>   PKCS#8 format works for RSA, ECDSA, DSA, or
>   any other asymmetric algorithm. The PEM header
>   `-----BEGIN PRIVATE KEY-----` indicates an
>   unencrypted PKCS#8 key.
> - ❌ **A — PKCS#1:** PKCS#1 is RSA-SPECIFIC —
>   it defines the RSA private key format
>   (PEM header: `BEGIN RSA PRIVATE KEY`). It
>   cannot be used for ECC or DSA keys. This
>   is the key difference between PKCS#1 (RSA
>   only) and PKCS#8 (any algorithm).
> - ❌ **C — PKCS#10:** PKCS#10 defines the CSR
>   format — a certificate REQUEST, not a
>   private key storage format.
> - ❌ **D — PKCS#7:** PKCS#7 defines signed/
>   encrypted message formats — not private
>   key storage.

---

## MCQs 9–14 — Key PKCS Deep Dives

---

**Q9. What is the purpose of the self-signature
in a PKCS#10 Certificate Signing Request (CSR)?**

- A) It allows the CSR to be used as a temporary
     self-signed certificate before the CA
     issues the real one
- B) It proves to the CA that the applicant
     controls the private key corresponding
     to the public key in the CSR ✅
- C) It encrypts the CSR so that only the CA
     can read its contents
- D) It allows the CA to skip identity
     verification for trusted applicants

> **Explanation:**
> - ✅ **B — Proof of Possession (PoP):** The
>   applicant signs the CSR with their private
>   key. The CA verifies this self-signature
>   using the public key WITHIN the CSR. If the
>   signature is valid, the CA knows the applicant
>   possesses the private key matching the public
>   key they are requesting a certificate for —
>   preventing someone from submitting a CSR
>   with someone else's public key.
> - ❌ **A:** A CSR is NOT a certificate — it
>   cannot be used as a temporary certificate.
>   Browsers and servers reject CSRs as certificates.
>   A self-signed certificate is a separate concept
>   — the CSR self-signature is specifically for
>   proof of possession.
> - ❌ **C:** The CSR is NOT encrypted — it is
>   submitted in plaintext (or PEM/Base64) to the
>   CA. The CA needs to read all of its contents
>   to process the request. Encryption is not the
>   purpose of the self-signature.
> - ❌ **D:** The self-signature does not bypass
>   identity verification. The CA still performs
>   its full validation process (DV/OV/EV) —
>   the self-signature only proves key possession,
>   not identity.

---

**Q10. PKCS#11 is described as an API standard
for cryptographic tokens. What is the practical
benefit of this standardization?**

- A) It allows applications to work with any
     PKCS#11-compliant hardware token without
     needing device-specific code ✅
- B) It standardizes the physical dimensions
     and connectors of USB crypto tokens
- C) It allows cryptographic keys to be
     transferred between different hardware
     tokens securely
- D) It defines a standard file format for
     storing certificates on smart cards

> **Explanation:**
> - ✅ **A:** The key benefit of PKCS#11 is
>   **interoperability**. Any application that
>   speaks PKCS#11 (OpenSSL, Firefox, Java) can
>   work with ANY hardware token that provides
>   a PKCS#11 library — HSMs, smart cards, USB
>   tokens — without needing custom integration
>   code for each device. The application calls
>   standard PKCS#11 functions; the vendor's
>   driver translates them to hardware-specific
>   commands.
> - ❌ **B:** PKCS#11 is a software API standard —
>   it has nothing to do with physical dimensions
>   or connector types. Physical form factor
>   standards are handled by ISO/IEC 7816 (smart
>   cards) and USB-IF specifications.
> - ❌ **C:** PKCS#11 does have key wrapping/
>   unwrapping functions but the standard's
>   PRIMARY benefit is application interoperability —
>   not key transfer between devices. Secure
>   key transfer between HSMs typically uses
>   proprietary mechanisms or well-defined
>   key ceremony procedures.
> - ❌ **D:** PKCS#15 (not PKCS#11) defines the
>   Cryptographic Token Information Format —
>   the data structures stored ON the smart card.
>   PKCS#11 is the API for ACCESSING the card,
>   not for defining its data structure.

---

**Q11. Where is PBKDF2 (from PKCS#5) used in
the Wi-Fi security protocol WPA2?**

- A) To generate the SSID broadcast name from
     the router's MAC address
- B) To derive the Pairwise Master Key (PMK)
     from the Wi-Fi passphrase and SSID ✅
- C) To encrypt the data frames transmitted
     between the device and access point
- D) To create the digital certificate used
     for WPA2-Enterprise authentication

> **Explanation:**
> - ✅ **B — PMK derivation:** In WPA2-Personal
>   (WPA2-PSK), **PBKDF2-HMAC-SHA1** is used to
>   derive the **PMK (Pairwise Master Key)** from
>   the Wi-Fi passphrase. The formula:
>   `PMK = PBKDF2(HMAC-SHA1, passphrase, SSID,
>   4096 iterations, 256-bit output)`.
>   The SSID acts as the salt — which is why
>   using a unique, non-common SSID improves
>   WPA2 security (prevents rainbow tables
>   precomputed against common SSIDs).
> - ❌ **A:** The SSID is a human-configured name —
>   it is not derived from the MAC address using
>   PBKDF2. SSID naming has no cryptographic
>   derivation process.
> - ❌ **C:** Data frame encryption in WPA2 uses
>   **AES-CCMP** (or TKIP in older WPA) — not
>   PBKDF2. PBKDF2 is used at the key setup
>   phase, not for per-packet data encryption.
> - ❌ **D:** WPA2-Enterprise uses 802.1X and
>   EAP protocols with digital certificates for
>   authentication — not PBKDF2. PBKDF2 is
>   specific to WPA2-Personal (PSK mode).

---

**Q12. What is the key difference between a
PKCS#1 formatted RSA private key and a PKCS#8
formatted private key?**

- A) PKCS#1 keys are always encrypted —
     PKCS#8 keys are never encrypted
- B) PKCS#1 is RSA-specific with PEM header
     `BEGIN RSA PRIVATE KEY` — PKCS#8 is
     algorithm-independent with PEM header
     `BEGIN PRIVATE KEY` ✅
- C) PKCS#1 keys are binary only — PKCS#8
     keys can be Base64-encoded
- D) PKCS#1 keys have stronger encryption
     than PKCS#8 because they include the
     prime factors p and q

> **Explanation:**
> - ✅ **B:** The key distinction is scope and
>   PEM header:
>   **PKCS#1** = RSA ONLY → `BEGIN RSA PRIVATE KEY`
>   **PKCS#8** = ANY algorithm → `BEGIN PRIVATE KEY`
>   PKCS#8 stores an algorithm identifier (OID)
>   alongside the key, making it portable across
>   RSA, ECDSA, DSA, etc. Modern OpenSSL defaults
>   to PKCS#8 format.
> - ❌ **A:** Both formats support encrypted and
>   unencrypted versions. PKCS#8 has an explicit
>   encrypted form (`BEGIN ENCRYPTED PRIVATE KEY`)
>   using PKCS#5 PBKDF2. PKCS#1 can also be
>   encrypted (with headers like `Proc-Type: 4,
>   ENCRYPTED`). Neither is exclusively encrypted
>   or unencrypted.
> - ❌ **C:** Both PKCS#1 and PKCS#8 can be stored
>   as binary (DER) or Base64-encoded (PEM).
>   The encoding choice is independent of the
>   key format standard.
> - ❌ **D:** PKCS#1 RSA private keys do include
>   prime factors p, q, and CRT parameters for
>   fast RSA operations — but this is about the
>   RSA key content, not about "encryption
>   strength." PKCS#8 wrapping does not remove
>   or add mathematical security to the key.

---

**Q13. Which PKCS standard is commonly used to
protect a private key file with a password
when exporting it for storage or transfer?**

- A) PKCS#7 — using signed envelope format
- B) PKCS#10 — using the CSR self-signature
- C) PKCS#5 (PBKDF2) — to derive an encryption
     key from the password before encrypting
     the private key ✅
- D) PKCS#3 — using Diffie-Hellman for
     password-based key exchange

> **Explanation:**
> - ✅ **C — PKCS#5:** When a private key is
>   exported with password protection, the
>   password is NOT used directly as the
>   encryption key (passwords are too short and
>   predictable). Instead, **PKCS#5 PBKDF2**
>   derives a strong cryptographic key from the
>   password (using a random salt and many
>   iterations), and this derived key encrypts
>   the private key. This is how PKCS#8
>   encrypted private keys and PKCS#12 .pfx
>   files work internally.
> - ❌ **A:** PKCS#7 provides signed/encrypted
>   message formats — it is not used to
>   password-protect private key files. PKCS#7
>   encryption uses certificate-based key
>   transport (asymmetric), not password-based.
> - ❌ **B:** The CSR self-signature proves key
>   possession — it is not a mechanism for
>   password-protecting a private key file.
> - ❌ **D:** PKCS#3 is for Diffie-Hellman key
>   agreement parameters — not for password-based
>   private key protection.

---

**Q14. Which two PKCS standards work TOGETHER
when a PKCS#12 (.pfx) file is created with
password protection?**

- A) PKCS#1 and PKCS#7
- B) PKCS#5 and PKCS#12 ✅
- C) PKCS#8 and PKCS#10
- D) PKCS#3 and PKCS#11

> **Explanation:**
> - ✅ **B — PKCS#5 and PKCS#12:** When a .pfx
>   file is created with a password:
>   **PKCS#12** defines the container format
>   (how the cert, key, and chain are bundled).
>   **PKCS#5 (PBKDF2)** is used INTERNALLY by
>   PKCS#12 to derive the encryption key from
>   the password — which then encrypts the
>   private key within the bundle. PKCS#12
>   uses PKCS#5 — they work together.
> - ❌ **A — PKCS#1 and PKCS#7:** PKCS#1 defines
>   RSA key formats and PKCS#7 defines signed/
>   encrypted message formats. Neither defines
>   the .pfx container format or the password-
>   based key derivation for it.
> - ❌ **C — PKCS#8 and PKCS#10:** PKCS#8 is the
>   private key format (which PKCS#12 may contain
>   internally) and PKCS#10 is the CSR format.
>   While PKCS#12 may store a PKCS#8-formatted
>   key inside, the password protection mechanism
>   is PKCS#5 — not PKCS#10.
> - ❌ **D — PKCS#3 and PKCS#11:** PKCS#3 is DH
>   parameters; PKCS#11 is the HSM API. Neither
>   is involved in creating a password-protected
>   .pfx file.

---

## MCQs 15–20 — FIPS 140-2

---

**Q15. What does FIPS 140-2 evaluate — and
how is this different from FIPS 197?**

- A) FIPS 140-2 evaluates cryptographic algorithms;
     FIPS 197 evaluates the security of cryptographic
     modules that use those algorithms
- B) FIPS 140-2 evaluates the security of
     cryptographic MODULES; FIPS 197 is the
     AES ALGORITHM standard ✅
- C) FIPS 140-2 and FIPS 197 both evaluate
     cryptographic algorithms — just for
     different purposes
- D) FIPS 140-2 evaluates network security
     devices; FIPS 197 evaluates encryption
     software

> **Explanation:**
> - ✅ **B:** This is the most fundamental
>   distinction in FIPS:
>   **FIPS 140-2** = evaluates how secure the
>   **MODULE** is that implements cryptography
>   (physical security, key management, tamper
>   resistance).
>   **FIPS 197** = defines the **AES algorithm**
>   itself (the mathematical specification).
>   A module running AES must comply with FIPS 197
>   (right algorithm) AND optionally get FIPS 140-2
>   validated (right module security).
> - ❌ **A:** This completely inverts the
>   relationship. FIPS 140-2 is about the MODULE
>   (implementation quality) — not the algorithm
>   specification. FIPS 197 defines the AES
>   algorithm — not module security.
> - ❌ **C:** FIPS 140-2 does NOT evaluate
>   algorithms — it evaluates modules. Algorithm
>   standards are separate FIPS documents
>   (FIPS 197 for AES, FIPS 186-4 for DSA/RSA/
>   ECDSA, FIPS 180-4 for SHA).
> - ❌ **D:** FIPS 140-2 is about cryptographic
>   modules specifically — not general network
>   security devices. And FIPS 197 defines AES —
>   not general encryption software categories.

---

**Q16. FIPS 140-2 defines four security levels
for cryptographic modules. What is the key
distinguishing feature of Level 2 compared
to Level 1?**

- A) Level 2 requires identity-based
     authentication and key zeroization
- B) Level 2 adds tamper-evidence — physical
     seals or pick-resistant enclosures showing
     evidence of tampering ✅
- C) Level 2 requires HSM hardware —
     software-only modules are not permitted
- D) Level 2 adds protection against
     environmental attacks like voltage
     fluctuations

> **Explanation:**
> - ✅ **B — Tamper-evidence:** Level 2 adds
>   **tamper-evidence** over Level 1 — physical
>   seals, locks, or pick-resistant enclosures
>   that show visible evidence if someone has
>   physically tampered with the module. If seals
>   are broken, operators know the module was
>   physically accessed. Level 1 has no physical
>   security requirements.
> - ❌ **A:** Identity-based authentication and
>   key zeroization on tamper are features of
>   **Level 3** — not Level 2. Level 2 uses
>   role-based authentication (weaker than
>   identity-based).
> - ❌ **C:** Software-only modules are still
>   permitted at Level 2 — the tamper-evidence
>   requirement applies to hardware components
>   where hardware is present. Pure software
>   modules can achieve Level 2 through other
>   means. Level 3 effectively requires hardware
>   for meaningful tamper resistance.
> - ❌ **D:** Environmental attack protection
>   (voltage, temperature) is a **Level 4**
>   requirement — the highest level. Level 2
>   adds only tamper-evidence, not environmental
>   protection.

---

**Q17. Which FIPS 140-2 security level is
required by the CA/Browser Forum for
protecting Intermediate CA private keys in
Hardware Security Modules?**

- A) FIPS 140-2 Level 1
- B) FIPS 140-2 Level 2
- C) FIPS 140-2 Level 3 ✅
- D) FIPS 140-2 Level 4

> **Explanation:**
> - ✅ **C — Level 3:** The CA/Browser Forum
>   Baseline Requirements reference **FIPS 140-2
>   Level 3** as the standard for protecting CA
>   private keys. Level 3 HSMs provide tamper
>   resistance (active tamper detection + key
>   zeroization), identity-based authentication,
>   and protection of Critical Security Parameters
>   — ensuring that CA keys cannot be extracted
>   even with physical access to the HSM.
> - ❌ **A — Level 1:** Level 1 allows software-
>   only implementations with no physical security.
>   This is entirely insufficient for protecting
>   CA private keys that establish trust for
>   millions of certificates.
> - ❌ **B — Level 2:** Level 2 adds tamper-
>   evidence — physical seals that show tampering
>   occurred. But it does NOT actively resist
>   or respond to tampering (no zeroization).
>   This is insufficient for the highest-security
>   CA key protection.
> - ❌ **D — Level 4:** Level 4 is extremely rare
>   and used only for the most critical
>   infrastructure (classified government, central
>   bank core). While it exceeds Level 3, the
>   CA/Browser Forum specifically references
>   Level 3 — not Level 4.

---

**Q18. What is the purpose of "zeroization" in
FIPS 140-2 Level 3 cryptographic modules?**

- A) Setting all internal counters to zero
     during initialization to prevent replay
     attacks
- B) Overwriting all Critical Security Parameters
     (keys, passwords) with zeros when tamper is
     detected — preventing key extraction ✅
- C) Zeroing out all network buffers when the
     module enters an error state
- D) Resetting the module's certificate database
     to factory state when a tamper alert occurs

> **Explanation:**
> - ✅ **B — Overwriting CSPs:** Zeroization is
>   the FIPS 140-2 mechanism where a Level 3
>   module **automatically overwrites all Critical
>   Security Parameters** (keys, passwords, seeds)
>   with zeros or random data when physical
>   tampering is detected. This ensures that even
>   if an attacker physically breaks open the HSM,
>   they cannot recover any cryptographic keys —
>   the keys were destroyed the instant tampering
>   was detected.
> - ❌ **A:** Counters being set to zero during
>   initialization is an initialization procedure —
>   not zeroization in the FIPS sense. FIPS
>   zeroization is a SECURITY RESPONSE to tampering,
>   not an initialization routine.
> - ❌ **C:** Network buffers have no relevance
>   to cryptographic key protection. Zeroization
>   is specifically about destroying cryptographic
>   key material — not general memory management.
> - ❌ **D:** Certificate databases are not what
>   is zeroized — certificates are public data
>   anyway. Zeroization targets the most sensitive
>   data: **private keys and secret passwords**
>   that must never be recoverable.

---

**Q19. FIPS 140-2 was published in 2001.
Which standard supersedes it, and in
what year was it published?**

- A) FIPS 140-3 — published in 2019 ✅
- B) FIPS 140-3 — published in 2015
- C) FIPS 200 — published in 2006
- D) FIPS 140-4 — published in 2022

> **Explanation:**
> - ✅ **A — FIPS 140-3 (2019):** FIPS 140-3 was
>   published in **March 2019** and supersedes
>   FIPS 140-2. It is based on ISO/IEC 19790:2012
>   and ISO/IEC 24759 — aligning US government
>   cryptographic module standards with international
>   standards. FIPS 140-2 sunset (no new submissions
>   accepted) is scheduled for September 2026.
> - ❌ **B:** The year 2015 is incorrect —
>   FIPS 140-3 was published in 2019. 2015 is
>   when SHA-3 (FIPS 202) was published —
>   a different FIPS document.
> - ❌ **C:** FIPS 200 (2006) is a separate
>   standard about "Minimum Security Requirements
>   for Federal Information and Information
>   Systems" — part of the FISMA framework.
>   It does NOT supersede FIPS 140-2.
> - ❌ **D:** FIPS 140-4 does not exist. The
>   progression is FIPS 140-1 → FIPS 140-2
>   → FIPS 140-3. There is no FIPS 140-4
>   as of the current standards landscape.

---

**Q20. The FIPS 140-2 validation process is
administered by a joint program. Which two
organizations jointly run the CMVP?**

- A) NIST (USA) and ANSSI (France)
- B) NIST (USA) and BSI (Germany)
- C) NIST (USA) and CCCS (Canada) ✅
- D) NIST (USA) and ENISA (European Union)

> **Explanation:**
> - ✅ **C — NIST + CCCS:** The **Cryptographic
>   Module Validation Program (CMVP)** is jointly
>   administered by **NIST** (National Institute
>   of Standards and Technology, USA) and
>   **CCCS** (Canadian Centre for Cyber Security
>   — formerly CSEC). This Canada-US partnership
>   means FIPS 140-2/3 validated products are
>   acceptable for both US and Canadian government
>   use.
> - ❌ **A:** ANSSI is France's national
>   cybersecurity agency — it runs Common Criteria
>   evaluations in France but is NOT a partner
>   in the CMVP.
> - ❌ **B:** BSI is Germany's Federal Office for
>   Information Security — it conducts Common
>   Criteria evaluations in Germany but is NOT
>   a CMVP partner.
> - ❌ **D:** ENISA is the European Union Agency
>   for Cybersecurity — it plays a policy and
>   coordination role in EU cybersecurity but
>   does NOT co-administer the CMVP with NIST.

---

## MCQs 21–25 — Extra Notes: Padding,
Encoding, CMVP

---

**Q21. For RSA encryption in a new system,
which padding scheme should be used and why?**

- A) PKCS#1 v1.5 — because it is the most
     widely compatible padding scheme
- B) PSS — because it provides probabilistic
     signatures for RSA encryption
- C) No padding (raw RSA) — because additional
     padding reduces the security of RSA
- D) OAEP — because it is CCA2-secure and
     resistant to the Bleichenbacher attack ✅

> **Explanation:**
> - ✅ **D — OAEP:** OAEP (Optimal Asymmetric
>   Encryption Padding) is the recommended padding
>   for RSA **encryption** in all new systems.
>   It is proven secure against Chosen Ciphertext
>   Attacks (CCA2-secure) and specifically
>   designed to prevent the Bleichenbacher attack
>   that exploits PKCS#1 v1.5 padding.
>   OAEP randomizes the encryption — the same
>   plaintext encrypted twice produces different
>   ciphertext.
> - ❌ **A:** PKCS#1 v1.5 is widely used for
>   legacy compatibility but is **vulnerable to
>   the Bleichenbacher attack** (1998) and the
>   ROBOT attack (2017). "Widely compatible"
>   does not mean secure — OAEP should be used
>   for new systems despite requiring slightly
>   more setup.
> - ❌ **B:** PSS (Probabilistic Signature Scheme)
>   is used for RSA **signatures** — NOT for
>   encryption. Using PSS for encryption would
>   be incorrect — OAEP is specifically for
>   encryption, PSS is specifically for signing.
> - ❌ **C:** Raw RSA (no padding) is fundamentally
>   insecure — it is deterministic (same plaintext
>   → same ciphertext), malleable, and vulnerable
>   to small-exponent attacks when messages are
>   small. Padding IMPROVES security — removing
>   it makes RSA weaker.

---

**Q22. What does the PEM header `-----BEGIN
ENCRYPTED PRIVATE KEY-----` indicate about
the file format and the key protection?**

- A) The file is in PKCS#1 format encrypted
     with AES-256
- B) The file is in PKCS#8 format with the
     private key encrypted using a password
     (PKCS#5 PBKDF2) ✅
- C) The file is in PKCS#12 format containing
     both the certificate and encrypted key
- D) The file is in PKCS#7 format with the
     private key signed by a CA

> **Explanation:**
> - ✅ **B — PKCS#8 encrypted:** The PEM header
>   `-----BEGIN ENCRYPTED PRIVATE KEY-----`
>   specifically identifies an **encrypted PKCS#8**
>   (EncryptedPrivateKeyInfo) structure. The
>   private key data inside is encrypted using
>   a key derived from a password via **PKCS#5
>   PBKDF2** — protecting the private key at rest.
>   The contrast: `BEGIN PRIVATE KEY` = unencrypted
>   PKCS#8; `BEGIN ENCRYPTED PRIVATE KEY` =
>   password-protected PKCS#8.
> - ❌ **A:** PKCS#1 encrypted private keys use
>   the header `BEGIN RSA PRIVATE KEY` with
>   `Proc-Type: 4,ENCRYPTED` lines — a different
>   legacy format. `BEGIN ENCRYPTED PRIVATE KEY`
>   is specifically the PKCS#8 encrypted format.
> - ❌ **C:** PKCS#12 (.pfx/.p12) is a binary
>   format — it does not use PEM headers like
>   `BEGIN ENCRYPTED PRIVATE KEY`. PKCS#12 files
>   are not presented in PEM format with standard
>   certificate-style headers.
> - ❌ **D:** PKCS#7 contains signed or encrypted
>   MESSAGES — not private keys. Private keys are
>   never distributed via PKCS#7. The header for
>   PKCS#7 is `BEGIN PKCS7`.

---

**Q23. What is the difference between a FIPS
140-2 VALIDATED module and a FIPS 140-2
COMPLIANT module?**

- A) They are the same — "validated" and
     "compliant" are interchangeable terms
     in FIPS documentation
- B) A validated module has completed independent
     CMVP testing and appears on the NIST list
     — compliant is a vendor claim without
     independent verification ✅
- C) A validated module is approved for Level 3
     — a compliant module is only approved for
     Level 1
- D) Validated modules are approved for commercial
     use — compliant modules are approved for
     government use only

> **Explanation:**
> - ✅ **B — Critical distinction:** A FIPS 140-2
>   **VALIDATED** module has been tested by a
>   CMVP-accredited Cryptographic and Security
>   Testing (CST) laboratory, reviewed by NIST,
>   and assigned a certificate number — it
>   appears on the CMVP Validated Modules List.
>   A **COMPLIANT** or **compatible** module is a
>   vendor's self-claim — no independent
>   verification was done. For US federal
>   government procurement, only VALIDATED
>   modules are acceptable.
> - ❌ **A:** They are absolutely NOT the same —
>   this is one of the most important distinctions
>   in the FIPS ecosystem. "Validated" has legal
>   and contractual significance for government
>   procurement; "compliant" is unverified
>   marketing language.
> - ❌ **C:** Validation and compliance are not
>   level-specific terms — a module at any level
>   (1 through 4) can be validated or merely
>   claimed compliant. The distinction is about
>   whether independent testing was performed,
>   not about which security level was achieved.
> - ❌ **D:** Both validated and compliant
>   designations can apply to commercial products.
>   The difference is not commercial vs government
>   use — it is tested vs untested. Validated
>   modules are required for government use;
>   commercial use may accept either.

---

**Q24. ASN.1, DER, and PEM are three related
concepts used in cryptographic file formats.
What is the correct relationship between them?**

- A) ASN.1 is the binary format, DER is the
     text description, and PEM is the compressed
     version
- B) ASN.1 defines the data structure, DER
     encodes it as binary bytes, and PEM is
     Base64-encoded DER with header/footer lines ✅
- C) DER is the data structure definition,
     ASN.1 is the binary encoding, and PEM is
     an alternative to DER
- D) PEM is the most secure format, DER is
     intermediate, and ASN.1 is the least secure

> **Explanation:**
> - ✅ **B — Three-layer relationship:** This is
>   the exact layering:
>   **ASN.1** (Abstract Syntax Notation One) =
>   language for DEFINING data structures
>   (certificates, keys, CRLs are defined in ASN.1).
>   **DER** (Distinguished Encoding Rules) =
>   canonical BINARY encoding of ASN.1 structures
>   — results in .der/.cer files.
>   **PEM** = Base64 encoding of DER bytes +
>   `-----BEGIN-----` header and footer lines
>   — results in .pem/.crt text files.
>   The chain: ASN.1 definition → DER bytes →
>   Base64 → PEM text.
> - ❌ **A:** This inverts several relationships.
>   ASN.1 is not binary — it is a notation
>   language. DER is the binary encoding (not a
>   text description). PEM is not compressed —
>   Base64 actually INCREASES size by ~33%.
> - ❌ **C:** This swaps ASN.1 and DER. ASN.1
>   is the DEFINITION language; DER is the
>   BINARY ENCODING of that definition. PEM
>   is not an alternative to DER — it IS DER
>   but Base64-encoded.
> - ❌ **D:** Security has nothing to do with
>   the ASN.1/DER/PEM relationship. All three
>   represent the same data — just in different
>   representations. DER and PEM carry identical
>   cryptographic content; neither is "more secure."

---

**Q25. Which of the following algorithms is
NOT approved for use in FIPS 140-2 compliant
(validated) modules?**

- A) AES-256-GCM
- B) SHA-256
- C) RC4 ✅
- D) RSA-2048

> **Explanation:**
> - ✅ **C — RC4:** RC4 is a broken stream cipher
>   that is **NOT approved** for use in FIPS 140-2
>   validated modules. FIPS mode explicitly
>   prohibits RC4 along with other broken
>   algorithms (DES single, MD5 for security,
>   MD4, RC2, RC5). When a module operates in
>   FIPS mode, RC4 must not be available as
>   an option.
> - ❌ **A — AES-256-GCM:** AES-256-GCM is
>   **fully approved** under FIPS 140-2. AES
>   (FIPS 197) with GCM mode (NIST SP 800-38D)
>   is one of the primary recommended encryption
>   modes. It is approved and widely used.
> - ❌ **B — SHA-256:** SHA-256 is **fully approved**
>   under FIPS 140-2. SHA-256 (FIPS 180-4) is
>   one of the core approved hash functions —
>   widely used for digital signatures, HMAC,
>   and integrity checking in FIPS-validated
>   systems.
> - ❌ **D — RSA-2048:** RSA-2048 is **approved**
>   under FIPS 140-2 — it meets the minimum 2048-bit
>   key size requirement for RSA in FIPS 186-4.
>   RSA below 1024 bits would not be approved,
>   but RSA-2048 is the current minimum standard.

---

## 📊 Answer Key — Quick Reference

| Q | Answer | Topic |
|---|--------|-------|
| 1 | B | PKCS = Public Key Crypto Standards — RSA Security / IETF |
| 2 | D | PKCS#10 = CSR format |
| 3 | C | PKCS#12 (.pfx) = cert + private key bundle |
| 4 | B | PKCS#11 = HSM/token API (Cryptoki) |
| 5 | C | PKCS#12 must be password-protected — contains private key |
| 6 | C | PKCS#5 = PBKDF2 definition |
| 7 | C | PKCS#7 (.p7b) = cert chain without private key |
| 8 | B | PKCS#8 = algorithm-independent private key format |
| 9 | B | CSR self-signature = proof of possession |
| 10 | A | PKCS#11 benefit = application interoperability with any token |
| 11 | B | PBKDF2 in WPA2 = derives PMK from passphrase + SSID |
| 12 | B | PKCS#1 (RSA-specific) vs PKCS#8 (any algorithm) |
| 13 | C | PKCS#5 PBKDF2 used to derive encryption key from password |
| 14 | B | PKCS#5 + PKCS#12 work together for .pfx password protection |
| 15 | B | FIPS 140-2 = module security; FIPS 197 = AES algorithm |
| 16 | B | FIPS Level 2 adds tamper-evidence |
| 17 | C | FIPS Level 3 = CA HSM standard (CA/B Forum) |
| 18 | B | Zeroization = overwrite CSPs with zeros on tamper |
| 19 | A | FIPS 140-3 published 2019 supersedes FIPS 140-2 |
| 20 | C | CMVP = joint NIST (USA) + CCCS (Canada) |
| 21 | D | OAEP = recommended RSA encryption padding |
| 22 | B | `BEGIN ENCRYPTED PRIVATE KEY` = PKCS#8 encrypted |
| 23 | B | Validated = CMVP-tested; Compliant = vendor claim only |
| 24 | B | ASN.1 (define) → DER (binary) → PEM (Base64) |
| 25 | C | RC4 = NOT FIPS approved |

---

## 📋 Topic Coverage Map

| Q | Concept Tested | Source |
|---|----------------|--------|
| 1 | PKCS meaning, origin, maintainer | Core |
| 2 | PKCS#10 = CSR format | Core |
| 3 | PKCS#12 = cert + private key bundle | Core |
| 4 | PKCS#11 = HSM API (Cryptoki) | Core |
| 5 | PKCS#12 must be password-protected — private key | Core |
| 6 | PKCS#5 = PBKDF2 | Core |
| 7 | PKCS#7 (.p7b) = cert chain, no private key | Core |
| 8 | PKCS#8 = algorithm-independent private key | Core |
| 9 | CSR self-signature = proof of possession | Core |
| 10 | PKCS#11 interoperability benefit | Core |
| 11 | PBKDF2 in WPA2 key derivation | Core |
| 12 | PKCS#1 vs PKCS#8 — RSA-specific vs general | Core |
| 13 | PKCS#5 PBKDF2 for password-protecting keys | Core |
| 14 | PKCS#5 + PKCS#12 work together | Core |
| 15 | FIPS 140-2 = module security, not algorithm | Core |
| 16 | FIPS Level 2 = tamper-evidence | Core |
| 17 | FIPS Level 3 = CA HSM standard | Core |
| 18 | Zeroization = destroy CSPs on tamper | Core |
| 19 | FIPS 140-3 supersedes FIPS 140-2 (2019) | Core |
| 20 | CMVP = NIST + CCCS (Canada) | Core |
| 21 | OAEP for encryption; PSS for signatures | Extra Notes |
| 22 | PEM header identification — PKCS#8 encrypted | Extra Notes |
| 23 | FIPS validated vs FIPS compliant distinction | Extra Notes |
| 24 | ASN.1 → DER → PEM encoding chain | Extra Notes |
| 25 | FIPS approved vs non-approved algorithms | Extra Notes |

---