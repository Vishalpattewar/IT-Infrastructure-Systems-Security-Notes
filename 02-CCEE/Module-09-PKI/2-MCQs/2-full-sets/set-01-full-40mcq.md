# Full MCQ Set 01 — PKI Module
### All 14 Sessions · 40 Questions

---

## 📋 Instructions

- Read ALL 40 questions before checking answers
- Write your answers on paper or mentally note them
- Check answers only AFTER completing all 40
- Answers and full explanations are at the END
- Score yourself using the key at the bottom

---

## PART 1 — QUESTIONS (Q1–Q40)

---

**Q1.** Which of the following BEST describes
the difference between a threat and a
vulnerability in information security?

- A) A threat is a weakness in a system —
     a vulnerability is the potential harm
- B) A threat is a potential cause of harm —
     a vulnerability is a weakness that
     can be exploited
- C) A threat and a vulnerability are the
     same concept used interchangeably
- D) A threat is always internal — a
     vulnerability is always external

---

**Q2.** A user encrypts a file on an NTFS
drive using Windows EFS and then copies it
to a USB drive formatted as FAT32. What is
the result?

- A) The file remains encrypted on the USB
     drive — EFS travels with the file
- B) The copy fails with an error —
     EFS prevents copying to non-NTFS drives
- C) The file is silently decrypted and
     stored as plaintext on the USB drive
- D) The file is automatically re-encrypted
     using BitLocker on the USB drive

---

**Q3.** The Avalanche Effect is a desirable
property of cryptographic hash functions
and block ciphers. What does it mean?

- A) A small change in the key causes the
     entire algorithm to slow down
     significantly
- B) A small change in the input (even
     1 bit) causes approximately 50% of
     the output bits to change unpredictably
- C) The output of the cipher cascades
     through multiple rounds making it
     avalanche-proof
- D) Large amounts of data are compressed
     into a smaller output — like an
     avalanche compressing snow

---

**Q4.** DES has an effective key length of
56 bits despite accepting a 64-bit key
input. Why?

- A) 8 bits are used for the Initial
     Permutation and discarded
- B) 8 bits are used for the Final
     Permutation and discarded
- C) Every 8th bit is a parity bit used
     for error checking — not for
     encryption
- D) 8 bits are reserved for the session
     identifier embedded in the key

---

**Q5.** In a Diffie-Hellman key exchange,
both parties agree on public parameters
p = 23 and g = 5. Alice's private key is
a = 4. What value does Alice send to Bob?

- A) 4
- B) 23
- C) 5
- D) 4

Wait — recalculating: 5⁴ mod 23 = 625 mod 23.
625 ÷ 23 = 27 remainder 4. So Alice sends:

- A) 4 ✓ (but let me recalculate to be sure)

Actually: 5^4 = 625. 625 / 23 = 27.17... 
27 × 23 = 621. 625 - 621 = 4. So:

- A) 4
- B) 9
- C) 17
- D) 20

---

**Q6.** SHA-256 produces a 256-bit output.
What is the output size in hexadecimal
characters?

- A) 32 hex characters
- B) 48 hex characters
- C) 64 hex characters
- D) 128 hex characters

---

**Q7.** A digital signature is created by
signing the HASH of a document rather than
signing the document directly. Which of the
following is the PRIMARY reason for hashing
first?

- A) Hashing provides confidentiality —
     the document content is hidden
     from the signer
- B) Asymmetric algorithms can only process
     small data — hashing produces a fixed
     small fingerprint of any-size document
- C) Hashing prevents the signature from
     expiring along with the certificate
- D) Hashing ensures the document is
     compressed before signing to save
     bandwidth

---

**Q8.** A certificate is valid and issued by
a trusted CA but its serial number appears
in the CA's CRL. What should a properly
configured browser do?

- A) Accept the certificate — it was issued
     by a trusted CA so it remains valid
- B) Reject the certificate — it has been
     revoked by the CA before its expiry ✓
- C) Show a warning but allow the user
     to continue — CRL is advisory only
- D) Accept the certificate — the validity
     period has not yet expired

---

**Q9.** In Aadhaar-based e-Sign, which part
of the document is sent to the ESP (e-Sign
Service Provider) for signing?

- A) The full document — so the ESP can
     verify its contents before signing
- B) The document's filename and metadata
     only — the content stays private
- C) Only the hash (SHA-256) of the
     document — the full document is
     never sent to the ESP
- D) An encrypted copy of the document
     wrapped with UIDAI's public key

---

**Q10.** PKCS#11 is also called Cryptoki.
What does it define?

- A) The format for storing private keys
     in encrypted files
- B) The format for Certificate Signing
     Requests submitted to a CA
- C) A standard API for applications to
     interact with hardware cryptographic
     tokens such as HSMs and smart cards
- D) The format for bundling a certificate
     and private key in a single file

---

**Q11.** A developer uses Python's built-in
`random` module to generate a 256-bit AES
encryption key. What is the critical flaw?

- A) Python's `random` module only supports
     128-bit output — it cannot generate
     256-bit values
- B) `random` is a PRNG — it is
     deterministic and not cryptographically
     secure — keys are predictable
- C) AES-256 requires hardware-generated
     keys — software key generation is
     not permitted
- D) 256-bit keys cannot be used with
     Python — only 128-bit is supported

---

**Q12.** PAP (Password Authentication
Protocol) is considered the weakest
authentication protocol. Which feature does
it completely lack?

- A) Support for usernames
- B) Any form of challenge-response —
     it sends the actual password in
     plaintext with no protection
- C) Compatibility with modern operating
     systems
- D) The ability to encrypt the channel
     after authentication

---

**Q13.** TLS 1.3 removed static RSA key
exchange. What is the security reason for
this removal?

- A) RSA keys are too slow for modern
     hardware — ECDHE is faster
- B) Static RSA provides no Perfect Forward
     Secrecy — if the RSA private key is
     later compromised, all past sessions
     can be decrypted
- C) RSA is a patented algorithm — TLS
     1.3 uses only royalty-free algorithms
- D) RSA certificates are larger than
     ECDSA certificates — TLS 1.3 reduces
     handshake size

---

**Q14.** The IT Act 2000 defines two
separate categories of authentication.
Which category does Aadhaar-based e-Sign
fall under?

- A) Digital Signature — under Section 3
     using asymmetric key pairs
- B) Electronic Signature — under
     Section 2(1)(ta) and the Second
     Schedule of the IT Act
- C) Biometric Signature — a third
     category added by the 2008 Amendment
- D) Qualified Signature — the highest
     category under eIDAS regulations

---

**Q15.** The McCumber Cube has three axes.
Which axis represents the states in which
information can exist?

- A) Confidentiality, Integrity,
     Availability
- B) Prevention, Detection, Correction
- C) Storage, Transmission, Processing
- D) Policies, Human Factors, Technology

---

**Q16.** What is the primary security
property that Kerckhoffs's Principle
establishes about cipher design?

- A) The cipher must use keys longer than
     256 bits to be considered secure
- B) The security of a cipher must rest
     entirely in the key — not in the
     secrecy of the algorithm
- C) The cipher must be implemented
     in hardware — software implementations
     are inherently weak
- D) The cipher must use both substitution
     and permutation operations to be
     considered secure

---

**Q17.** A One-Time Pad (Vernam Cipher)
is theoretically unbreakable. Under which
condition does this perfect secrecy fail?

- A) When the key is shorter than the
     message — some characters remain
     unencrypted
- B) When the message contains only
     ASCII characters — binary data
     is required
- C) When the same key is reused to
     encrypt two different messages —
     C1 XOR C2 reveals P1 XOR P2
- D) When MD5 is used as the hash
     function for key verification

---

**Q18.** The AES-256 cipher always uses
which block size?

- A) 256 bits — matching the key size
- B) 192 bits — a compromise between
     128-bit and 256-bit
- C) 128 bits — regardless of key size
- D) 512 bits — doubled for higher
     security with 256-bit keys

---

**Q19.** Which of the following correctly
describes the BEAST attack (2011)?

- A) It targeted SSL 3.0 by exploiting
     undefined CBC padding behavior
- B) It targeted TLS 1.0 by exploiting
     the predictable IV used in
     CBC mode encryption
- C) It targeted TLS 1.2 by exploiting
     weak DHE key parameters
- D) It targeted HTTPS by exploiting
     HTTP compression to leak secrets

---

**Q20.** HMAC provides integrity and
authentication but does NOT provide which
security property?

- A) Integrity — detecting unauthorized
     data modification
- B) Authentication — confirming the
     sender knows the shared key
- C) Non-repudiation — proving only
     one specific party created
     the message
- D) Detection of replay attacks when
     combined with timestamps

---

**Q21.** An X.509 v3 certificate contains a
Subject Alternative Name (SAN) extension
listing `*.example.com`. Which hostname
is NOT covered by this wildcard?

- A) www.example.com
- B) api.example.com
- C) mail.example.com
- D) login.api.example.com

---

**Q22.** The CA/Browser Forum Baseline
Requirements specify the current maximum
TLS certificate validity period. What is it?

- A) 730 days (2 years)
- B) 825 days
- C) 398 days
- D) 365 days (1 year exactly)

---

**Q23.** What is the role of the TSA (Time
Stamp Authority) in a trusted timestamping
operation?

- A) To encrypt the document and store
     it for future verification
- B) To sign the hash of the document
     combined with the current time —
     creating a tamper-proof proof of
     existence
- C) To issue a digital certificate to
     the signer before they sign the
     document
- D) To verify the signer's identity
     using Aadhaar authentication before
     stamping the document

---

**Q24.** A PKCS#12 (.pfx) file is described
as a "certificate bundle." What does it
contain that a standard PEM certificate
file does NOT?

- A) The CA's digital signature on the
     certificate — PEM omits this
- B) The private key — bundled with the
     certificate and chain in an encrypted
     container
- C) The certificate's revocation status
     from the CA's OCSP responder
- D) The Subject Alternative Names —
     PEM format cannot store extensions

---

**Q25.** OAuth 2.0 was published as an IETF
standard in which RFC, and in what year?

- A) RFC 5246 — 2008
- B) RFC 8446 — 2018
- C) RFC 6749 — 2012
- D) RFC 4226 — 2005

---

**Q26.** FIDO2 credentials are bound to
the RP_ID (Relying Party ID). What prevents
a phishing site from triggering a valid
FIDO2 authentication response?

- A) FIDO2 requires an internet connection
     to validate the site certificate before
     responding to any authentication request
- B) The phishing site has a different
     domain from the legitimate site —
     the authenticator has no credential
     registered for that domain
- C) FIDO2 uses a one-time password that
     expires before the phishing site
     can relay it
- D) The user must scan a QR code that
     only appears on the legitimate site's
     verified pages

---

**Q27.** PGP uses hybrid encryption. When
sending an encrypted message, what is
encrypted with the RECIPIENT'S public key?

- A) The entire message — RSA encrypts
     it directly
- B) A digital signature on the message —
     the recipient verifies with their
     private key
- C) The random symmetric session key —
     the message itself is encrypted
     with AES using the session key
- D) The sender's identity information —
     so the recipient can verify the
     sender's key fingerprint

---

**Q28.** Which Section of the IT Act 2000
provides that unauthorized access to a
computer system can result in compensation
payable to the affected person?

- A) Section 5
- B) Section 17
- C) Section 43
- D) Section 79

---

**Q29.** The Feistel cipher structure is
used by DES but NOT by AES. What structure
does AES use instead?

- A) ARX (Add-Rotate-XOR) structure
- B) Substitution-Permutation Network (SPN)
- C) Merkle-Damgård construction
- D) Sponge construction

---

**Q30.** In the Kerberos authentication
system, what is the purpose of the
Ticket Granting Server (TGS)?

- A) It authenticates the user's password
     and issues the initial Ticket Granting
     Ticket (TGT)
- B) It receives a valid TGT from the
     client and issues Service Tickets
     for specific services
- C) It stores the hash of all user
     passwords in the domain
- D) It encrypts all network traffic
     between the client and the requested
     service

---

**Q31.** Which of the following correctly
describes the relationship between OpenPGP
and GPG (GnuPG)?

- A) OpenPGP is a paid product — GPG is
     the free version of the same product
- B) OpenPGP (RFC 4880) is the open
     STANDARD — GPG is a free open-source
     IMPLEMENTATION of that standard
- C) GPG is the standard and OpenPGP is
     a commercial implementation by
     Symantec
- D) They are the same product — OpenPGP
     was renamed to GPG in 2005

---

**Q32.** In the LDAP directory hierarchy,
what does the following Distinguished
Name represent?

`ou=Engineering,dc=company,dc=com`

- A) A user named Engineering in the
     company.com domain
- B) An Organizational Unit called
     Engineering in the company.com domain
- C) A Domain Component for the
     Engineering subdomain of company.com
- D) A computer named Engineering in
     the company domain

---

**Q33.** A blockchain is described as
"append-only." What does this mean?

- A) New data can only be added — existing
     blocks cannot be deleted or modified
- B) Each new block appends the previous
     block's data — blocks grow larger
     with each addition
- C) Only authorized nodes can append
     blocks — others can only read
- D) Blocks are appended in alphabetical
     order based on transaction content

---

**Q34.** Which EAP method is considered the
most secure for WPA2-Enterprise Wi-Fi
because it requires digital certificates
on BOTH the client AND the server?

- A) EAP-MD5
- B) PEAP (Protected EAP)
- C) EAP-TLS
- D) EAP-FAST

---

**Q35.** The NIST Zero Trust Architecture
is defined in which Special Publication?

- A) NIST SP 800-53
- B) NIST SP 800-63
- C) NIST SP 800-207
- D) NIST SP 800-171

---

**Q36.** In TLS 1.3, the server's certificate
is sent in the handshake in an encrypted
state. Which TLS 1.2 weakness does this
address?

- A) In TLS 1.2, the server certificate
     can be forged during the handshake
- B) In TLS 1.2, the server certificate
     is visible in plaintext to network
     observers — leaking server identity
- C) In TLS 1.2, the server certificate
     is not verified by the client until
     after the session is established
- D) In TLS 1.2, the server certificate
     is sent after application data begins
     — creating a race condition

---

**Q37.** RSA encryption and RSA digital
signatures both use the same mathematical
operation. What is the KEY DIFFERENCE
in how the keys are used?

- A) Encryption uses a 2048-bit key —
     signatures require a 4096-bit key
- B) For encryption: public key encrypts,
     private key decrypts. For signatures:
     private key signs, public key verifies
- C) For encryption: private key encrypts,
     public key decrypts. For signatures:
     public key signs, private key verifies
- D) Both encryption and signatures use
     the private key — the difference is
     only the padding scheme applied

---

**Q38.** Bitcoin's blockchain uses
double-SHA256 for PoW mining. What does
this mean?

- A) SHA-256 is applied twice with two
     different secret keys — providing
     double the security
- B) The output of SHA-256 is fed as
     input to SHA-256 again —
     SHA256(SHA256(data))
- C) Two independent SHA-256 instances
     run in parallel and their outputs
     are XORed together
- D) SHA-256 is applied to the first
     half of the block and then to
     the second half separately

---

**Q39.** S/MIME email signing requires
an X.509 certificate with a specific
Extended Key Usage (EKU) value. Which EKU
is required?

- A) serverAuth
- B) codeSigning
- C) timeStamping
- D) emailProtection

---

**Q40.** FIPS 140-2 defines security
requirements for cryptographic modules.
Which security LEVEL requires active
tamper resistance with automatic key
zeroization when tampering is detected —
and is the standard required for CA
private key protection?

- A) FIPS 140-2 Level 1
- B) FIPS 140-2 Level 2
- C) FIPS 140-2 Level 3
- D) FIPS 140-2 Level 4

---

&nbsp;

&nbsp;

&nbsp;

---

## PART 2 — ANSWERS AND EXPLANATIONS

---

**Q1. Answer: B**

> **B** is correct. A **threat** is a potential
> cause of harm — any circumstance or event that
> could negatively impact assets (e.g., a hacker,
> malware, insider). A **vulnerability** is a
> weakness or flaw in a system that can be
> exploited by a threat (e.g., unpatched software,
> weak password policy). Risk arises when a threat
> exploits a vulnerability.
>
> - ❌ **A** inverts the definitions.
> - ❌ **C** is wrong — they are distinct concepts.
> - ❌ **D** is wrong — threats can be internal
>   (insider threat) or external; vulnerabilities
>   can exist in any location.

---

**Q2. Answer: C**

> **C** is correct. EFS (Encrypting File System)
> is an NTFS feature — it cannot exist on FAT32.
> When an EFS-encrypted file is copied to a FAT32
> drive, Windows **silently decrypts** the file
> during the copy operation. No warning is shown —
> the file arrives on the USB drive as plaintext.
> This is a well-known data exposure risk.
>
> - ❌ **A** is wrong — EFS does NOT travel with
>   the file to non-NTFS drives.
> - ❌ **B** is wrong — Windows does not block
>   the copy; it completes silently.
> - ❌ **D** is wrong — BitLocker is a full-disk
>   encryption tool; it does not auto-encrypt
>   individual files copied to USB drives.

---

**Q3. Answer: B**

> **B** is correct. The **Avalanche Effect** means
> a single-bit change in the input produces an
> approximately 50% change in the output bits —
> completely unpredictably. This is a critical
> property because it ensures small plaintext
> changes cannot be hidden and prevents attackers
> from making useful predictions about ciphertext
> changes from small input modifications.
>
> - ❌ **A** describes a performance degradation —
>   not the Avalanche Effect.
> - ❌ **C** confuses rounds with the avalanche
>   property — rounds implement it, they are not
>   the definition.
> - ❌ **D** describes data compression — unrelated
>   to cryptographic avalanche.

---

**Q4. Answer: C**

> **C** is correct. DES accepts a 64-bit key input
> but every 8th bit (bits 8, 16, 24, 32, 40, 48,
> 56, 64) is a **parity bit** used for error
> detection — not for encryption. The PC-1 step
> in the DES key schedule explicitly removes all
> 8 parity bits, leaving 56 bits of actual key
> material. This is why DES has only 2⁵⁶ effective
> key space despite the 64-bit input.
>
> - ❌ **A** and **B** are wrong — the Initial and
>   Final Permutations operate on the data, not
>   the key. They do not discard key bits.
> - ❌ **D** is fabricated — there is no session
>   identifier embedded in the DES key.

---

**Q5. Answer: A**

> **A** is correct. Alice computes her public value:
> A = gᵃ mod p = 5⁴ mod 23.
> 5⁴ = 625.
> 625 ÷ 23 = 27 remainder 4 (27 × 23 = 621;
> 625 − 621 = 4).
> So Alice sends **4** to Bob.
> Her private key (a = 4) is never sent.
>
> - ❌ **B (9)** would be 5² mod 23 = 25 mod 23 = 2.
>   Not the result for a=4.
> - ❌ **C (17)** would be 5³ mod 23 = 125 mod 23.
>   125 = 5×23 + 10 = 10. Not 17 either.
> - ❌ **D (20)** is not 5⁴ mod 23.

---

**Q6. Answer: C**

> **C** is correct. SHA-256 produces a
> **256-bit** output. Since each hexadecimal
> digit represents 4 bits:
> 256 ÷ 4 = **64 hexadecimal characters**.
> For example:
> `a3f7c1d8...` (64 characters total).
>
> - ❌ **A (32 hex chars)** = 128 bits — this is
>   the output size of **MD5**, not SHA-256.
> - ❌ **B (48 hex chars)** = 192 bits — not a
>   standard SHA output size.
> - ❌ **D (128 hex chars)** = 512 bits — this is
>   the output size of **SHA-512**, not SHA-256.

---

**Q7. Answer: B**

> **B** is correct. Asymmetric algorithms (RSA,
> ECDSA) can only process data smaller than their
> key size — approximately 256 bytes for RSA-2048.
> Documents can be megabytes or gigabytes. By
> hashing first, we get a fixed small fingerprint
> (32 bytes for SHA-256) that represents the
> entire document — which can then be signed.
> This is also faster since hashing is cheap
> and RSA operations are expensive.
>
> - ❌ **A** is wrong — hashing does NOT provide
>   confidentiality. The hash is sent with the
>   document in plaintext.
> - ❌ **C** is wrong — certificate expiry is
>   addressed by timestamping (RFC 3161), not
>   by hashing.
> - ❌ **D** is wrong — bandwidth reduction is
>   not the primary reason; the mathematical
>   size constraint of RSA is.

---

**Q8. Answer: B**

> **B** is correct. A revoked certificate is one
> that the CA has invalidated before its natural
> expiry — for reasons like private key compromise
> or cessation of operation. Once a certificate's
> serial number appears in the CRL (Certificate
> Revocation List), it must be treated as
> untrustworthy and **rejected** — regardless of
> whether the validity period has not yet expired.
>
> - ❌ **A** is wrong — CA trust and current
>   validity period do not override revocation.
>   A revoked cert from a trusted CA is still
>   invalid.
> - ❌ **C** is wrong — CRL is not advisory; it
>   is a definitive revocation mechanism.
> - ❌ **D** is wrong — the validity period
>   expiry is a separate check; revocation
>   supersedes it.

---

**Q9. Answer: C**

> **C** is correct. In Aadhaar-based e-Sign,
> only the **SHA-256 hash of the document** is
> sent to the ESP. The full document never leaves
> the user's application. This protects document
> confidentiality — the ESP (and by extension,
> UIDAI or any intermediary) never sees the
> document content. The ESP signs the hash;
> the ASP embeds the returned signature in the
> original document.
>
> - ❌ **A** is wrong — sending the full document
>   to the ESP would violate document
>   confidentiality, especially for sensitive
>   materials like tax returns or loan agreements.
> - ❌ **B** is wrong — metadata alone is not
>   sufficient for a legally valid digital signature.
> - ❌ **D** is wrong — the document is not
>   encrypted and sent; only its hash is sent.

---

**Q10. Answer: C**

> **C** is correct. **PKCS#11 (Cryptoki —
> Cryptographic Token Interface)** defines a
> standard Application Programming Interface
> (API) that allows applications (OpenSSL,
> Firefox, Java) to interact with hardware
> cryptographic tokens — HSMs, smart cards,
> and USB tokens — without needing device-specific
> code. Every major HSM vendor provides a
> PKCS#11 library.
>
> - ❌ **A** describes **PKCS#8** — the format
>   for storing private keys.
> - ❌ **B** describes **PKCS#10** — the
>   Certificate Signing Request format.
> - ❌ **D** describes **PKCS#12** — the
>   .pfx/.p12 bundle format.

---

**Q11. Answer: B**

> **B** is correct. Python's `random` module is a
> **PRNG (Pseudo-Random Number Generator)** — it
> is deterministic and seeded from predictable
> sources. For cryptographic operations, a
> **CSPRNG (Cryptographically Secure PRNG)** is
> required — in Python, this is `secrets` or
> `os.urandom()`. Using `random` for key
> generation makes the keys predictable to
> an attacker who can determine or guess the seed.
>
> - ❌ **A** is wrong — Python's `random` can
>   generate arbitrary-length byte sequences; the
>   bit length is not the issue.
> - ❌ **C** is wrong — AES keys can be generated
>   in software using a proper CSPRNG; hardware
>   generation is not mandatory.
> - ❌ **D** is wrong — Python supports AES-256;
>   key length restriction is not the issue here.

---

**Q12. Answer: B**

> **B** is correct. PAP (Password Authentication
> Protocol, RFC 1334) sends the **actual password
> in plaintext** — there is no challenge-response,
> no hashing, no encryption of the password before
> transmission. It is the most insecure
> authentication protocol and should never be
> used on untrusted networks. Any eavesdropper
> capturing the network traffic immediately
> obtains the password.
>
> - ❌ **A** is wrong — PAP does transmit both
>   username and password.
> - ❌ **C** is wrong — PAP was designed for
>   PPP dial-up connections; compatibility is
>   not its weakness.
> - ❌ **D** is wrong — PAP has no mechanism to
>   upgrade the channel after authentication.

---

**Q13. Answer: B**

> **B** is correct. With **static RSA key
> exchange** in TLS 1.2, the client encrypts the
> pre-master secret directly with the server's
> RSA public key. If the server's RSA private key
> is later stolen (even years later), an attacker
> who recorded past TLS sessions can decrypt ALL
> of them — there is no Perfect Forward Secrecy.
> TLS 1.3 mandates **ECDHE** (ephemeral keys per
> session) — past sessions remain safe even if
> the long-term key is compromised.
>
> - ❌ **A** is partially true (ECDHE is faster)
>   but is not the PRIMARY security reason for
>   removing static RSA.
> - ❌ **C** is wrong — RSA is not patented in
>   a way that affects TLS; the patent expired
>   in 2000.
> - ❌ **D** is a secondary concern — certificate
>   size is not the primary reason static RSA
>   was removed.

---

**Q14. Answer: B**

> **B** is correct. Aadhaar-based e-Sign falls
> under the **Electronic Signature** category —
> Section 2(1)(ta) — added by the IT (Amendment)
> Act 2008. The Second Schedule to the IT Act
> lists approved electronic signature methods,
> which includes Aadhaar-based authentication.
> A **Digital Signature** (Section 2(1)(p) +
> Section 3) specifically requires asymmetric
> key pairs from a licensed CA — that is the
> physical DSC (USB token).
>
> - ❌ **A** is wrong — e-Sign is NOT classified
>   as a Digital Signature under Section 3.
>   Physical DSC is the Digital Signature.
> - ❌ **C** is wrong — "Biometric Signature"
>   is not a legal category in the IT Act.
> - ❌ **D** is wrong — eIDAS is an EU regulation;
>   "Qualified Signature" is an eIDAS term, not
>   an IT Act category.

---

**Q15. Answer: C**

> **C** is correct. The McCumber Cube has three
> axes:
> (1) **Security Goals**: Confidentiality,
>     Integrity, Availability (CIA)
> (2) **Information States**: Storage,
>     Transmission, Processing
> (3) **Security Countermeasures**: Policies
>     & Procedures, Human Factors, Technology
>
> The question asks about the axis representing
> **states in which information can exist** —
> that is Storage, Transmission, Processing.
>
> - ❌ **A** describes the Security Goals axis.
> - ❌ **B** describes security control functions
>   (not a McCumber axis).
> - ❌ **D** describes the Security Countermeasures
>   axis.

---

**Q16. Answer: B**

> **B** is correct. **Kerckhoffs's Principle**
> (Auguste Kerckhoffs, 1883) states that a
> cryptosystem must remain secure even when
> everything about it is publicly known EXCEPT
> the key. Security must rest entirely in the
> key — not in keeping the algorithm secret.
> This is why modern algorithms (AES, RSA) are
> publicly published — their security is
> mathematical, not through obscurity.
>
> - ❌ **A** is wrong — Kerckhoffs's Principle
>   is about algorithm transparency, not specific
>   key lengths.
> - ❌ **C** is wrong — hardware vs software
>   implementation is not what Kerckhoffs
>   addresses.
> - ❌ **D** is wrong — using both substitution
>   and permutation (Shannon's properties) is
>   a separate design principle from Kerckhoffs.

---

**Q17. Answer: C**

> **C** is correct. If the SAME key K is used
> to encrypt two messages P1 and P2:
> C1 = P1 XOR K and C2 = P2 XOR K.
> C1 XOR C2 = P1 XOR P2 (the key cancels out).
> The attacker now has the XOR of both plaintexts
> — from which both messages can be recovered
> using language statistics (crib-dragging).
> This is how the Venona project broke Soviet
> OTP messages — operators reused key material.
>
> - ❌ **A** describes an incomplete OTP (key
>   shorter than message) — a different problem.
> - ❌ **B** is wrong — OTP works on any binary
>   data; ASCII restriction is fabricated.
> - ❌ **D** is wrong — MD5 has nothing to do
>   with OTP key reuse vulnerability.

---

**Q18. Answer: C**

> **C** is correct. **AES always uses a 128-bit
> block size** — regardless of key size.
> AES-128, AES-192, and AES-256 all operate on
> 128-bit (16-byte) blocks. Only the key length
> and number of rounds change between variants
> (AES-128: 10 rounds; AES-192: 12 rounds;
> AES-256: 14 rounds). This is one of the most
> commonly tested facts about AES.
>
> - ❌ **A** is wrong — AES-256 has a 256-bit KEY
>   but NOT a 256-bit block. This is the most
>   common MCQ trap for this topic.
> - ❌ **B** is wrong — 192 bits is not the block
>   size for any AES variant.
> - ❌ **D** is wrong — 512-bit blocks do not
>   exist in AES.

---

**Q19. Answer: B**

> **B** is correct. The **BEAST (Browser Exploit
> Against SSL/TLS)** attack was discovered in
> 2011 by Thai Duong and Juliano Rizzo. It
> targeted **TLS 1.0** specifically. In TLS 1.0,
> the IV for CBC mode was the last ciphertext
> block of the previous record — making it
> predictable. This allowed an attacker who could
> inject chosen plaintext to recover cookie
> values.
>
> - ❌ **A** describes the **POODLE attack (2014)**
>   which targeted SSL 3.0's undefined CBC padding.
> - ❌ **C** describes aspects of the **Logjam
>   attack (2015)** targeting weak DHE params.
> - ❌ **D** describes the **CRIME attack (2012)**
>   which exploited TLS/HTTP compression.

---

**Q20. Answer: C**

> **C** is correct. HMAC uses a **shared secret
> key** — both sender and receiver know the same
> key. This means EITHER party could have created
> the HMAC — there is no way to prove to a third
> party that only the sender created it. This is
> why HMAC provides **no non-repudiation**.
> Non-repudiation requires an asymmetric private
> key held exclusively by the signer — which is
> what digital signatures provide.
>
> - ❌ **A** is wrong — HMAC absolutely provides
>   integrity; any modification to the data
>   produces a different HMAC.
> - ❌ **B** is wrong — HMAC provides
>   authentication because only parties with
>   the shared key can produce a valid HMAC.
> - ❌ **D** is wrong — HMAC combined with
>   timestamps (e.g., in JWT) does help prevent
>   replay attacks.

---

**Q21. Answer: D**

> **D** is correct. A wildcard certificate
> `*.example.com` covers all subdomains at
> **exactly ONE level** below example.com.
> It matches `www.example.com`, `api.example.com`,
> `mail.example.com` (one label replacing `*`).
> It does **NOT** cover `login.api.example.com`
> because that has TWO levels below example.com
> (`login.api` contains a dot — two labels).
> Wildcards only replace a single DNS label
> with no embedded dots.
>
> - ❌ **A, B, C** are all single-level subdomains
>   — all covered by `*.example.com`.

---

**Q22. Answer: C**

> **C** is correct. The CA/Browser Forum Baseline
> Requirements, effective **September 1, 2020**,
> set the maximum TLS certificate validity period
> at **398 days** (approximately 13 months).
> This was driven by Apple's announcement that
> Safari would reject certificates with validity
> exceeding 398 days.
>
> - ❌ **A (730 days)** was the limit from March
>   2018 to September 2020 — now superseded.
> - ❌ **B (825 days)** was the limit before
>   March 2018 — also superseded.
> - ❌ **D (365 days)** is LESS than the limit —
>   a 1-year cert is valid, but the MAXIMUM
>   is 398 days (slightly more than 1 year).

---

**Q23. Answer: B**

> **B** is correct. A **Time Stamp Authority (TSA)**
> receives the hash of the document (not the
> document itself), combines it with the current
> trusted UTC time, and digitally signs the
> combination — producing a **Time Stamp Token
> (TST)**. This creates a tamper-proof,
> cryptographically signed proof that the specific
> document (identified by its hash) existed at
> the stated time. The TSA's signature prevents
> backdating or alteration.
>
> - ❌ **A** is wrong — the TSA does not encrypt
>   or store documents.
> - ❌ **C** is wrong — the TSA does not issue
>   signing certificates to signers; that is
>   the CA's job.
> - ❌ **D** is wrong — Aadhaar authentication
>   is for e-Sign, not timestamping. TSP (RFC
>   3161) is independent of Aadhaar.

---

**Q24. Answer: B**

> **B** is correct. A **PKCS#12 (.pfx/.p12)**
> file bundles the **private key** (encrypted
> with a password), the certificate, and the
> certificate chain together. A standard PEM
> certificate file (`.crt`, `.pem`) contains
> only the public certificate — the private key
> is kept separately. This is why PKCS#12 files
> MUST be password-protected — they contain the
> most sensitive cryptographic material.
>
> - ❌ **A** is wrong — PEM certificates DO
>   contain the CA's signature (it is part of
>   the X.509 structure).
> - ❌ **C** is wrong — revocation status is
>   checked dynamically via OCSP/CRL, not stored
>   inside the certificate bundle.
> - ❌ **D** is wrong — PEM format can store
>   X.509 v3 extensions including SANs.

---

**Q25. Answer: C**

> **C** is correct. OAuth 2.0 is defined in
> **RFC 6749**, published in **2012**. It replaced
> OAuth 1.0 (RFC 5849) and defines the
> authorization framework for delegated access
> to resources without sharing credentials.
>
> - ❌ **A** — RFC 5246 (2008) defines **TLS 1.2**.
> - ❌ **B** — RFC 8446 (2018) defines **TLS 1.3**.
> - ❌ **D** — RFC 4226 (2005) defines **HOTP**
>   (HMAC-based One-Time Password algorithm).

---

**Q26. Answer: B**

> **B** is correct. FIDO2 credentials are
> registered with a specific **RP_ID (Relying
> Party ID)** — the exact domain of the
> legitimate website (e.g., `google.com`). A
> phishing site at `g00gle.com` has a different
> RP_ID. The authenticator checks the RP_ID
> during authentication — finding no credential
> for `g00gle.com`, it returns an error. The
> phishing site receives nothing useful — the
> authentication fails automatically without
> any user awareness needed.
>
> - ❌ **A** is wrong — FIDO2 authentication
>   is local (no internet lookup of site cert);
>   phishing resistance comes from RP_ID binding.
> - ❌ **C** is wrong — FIDO2 uses asymmetric
>   signatures, not OTP codes; relay attacks
>   on OTP are what FIDO2 replaces.
> - ❌ **D** is wrong — QR codes may be used
>   in CTAP2 hybrid transport but are not
>   the mechanism for phishing resistance.

---

**Q27. Answer: C**

> **C** is correct. In PGP hybrid encryption:
> (1) A random **AES session key** is generated.
> (2) The message is encrypted with AES using
>     the session key.
> (3) The **session key is encrypted with the
>     recipient's RSA/ECC public key**.
> Both are sent together. The recipient uses
> their private key to decrypt the session key,
> then decrypts the message with AES.
> RSA is used ONLY to protect the session key —
> not to encrypt the bulk message data.
>
> - ❌ **A** is wrong — RSA cannot encrypt
>   entire messages (size limit ~256 bytes for
>   RSA-2048); hybrid encryption solves this.
> - ❌ **B** is wrong — the session key is NOT
>   a signature; signatures use the SENDER's
>   private key, not the recipient's public key.
> - ❌ **D** is wrong — sender identity is not
>   what is encrypted with the recipient's key.

---

**Q28. Answer: C**

> **C** is correct. **Section 43** of the IT Act
> 2000 provides for penalties for unauthorized
> access to computer systems. It covers accessing
> without permission, downloading/copying data,
> introducing viruses, disrupting computer
> systems, and denial of service. The affected
> person can receive **compensation up to ₹1 crore**
> (civil remedy).
>
> - ❌ **A** — Section 5 deals with legal
>   recognition of digital signatures.
> - ❌ **B** — Section 17 establishes the CCA
>   (Controller of Certifying Authorities).
> - ❌ **D** — Section 79 provides safe harbour
>   for intermediaries.

---

**Q29. Answer: B**

> **B** is correct. AES uses a
> **Substitution-Permutation Network (SPN)**
> structure — alternating layers of substitution
> (SubBytes using S-Boxes) and permutation
> (ShiftRows, MixColumns). DES uses the
> **Feistel structure** — splitting the block
> into halves and applying a round function.
> The SPN vs Feistel distinction is a very
> commonly tested fact about AES vs DES.
>
> - ❌ **A** — ARX (Add-Rotate-XOR) is used by
>   RC5, ChaCha20, and other stream ciphers.
> - ❌ **C** — Merkle-Damgård is a hash function
>   construction (SHA-1, SHA-2) — not a block
>   cipher structure.
> - ❌ **D** — Sponge construction is used by
>   SHA-3 (Keccak) — not a block cipher.

---

**Q30. Answer: B**

> **B** is correct. In Kerberos, after the
> **Authentication Server (AS)** issues the
> initial **TGT (Ticket Granting Ticket)**, the
> **Ticket Granting Server (TGS)** handles
> subsequent service access. The client presents
> the TGT to the TGS and requests a **Service
> Ticket** for a specific service. The TGS
> validates the TGT and issues the Service
> Ticket — which the client then presents to
> the target service for access.
>
> - ❌ **A** describes the **Authentication
>   Server (AS)** role — not TGS.
> - ❌ **C** is wrong — password hashes are
>   stored in the KDC's database, not by the
>   TGS as a separate function.
> - ❌ **D** is wrong — traffic encryption is
>   handled by session keys and TLS/IPSec —
>   the TGS issues tickets; it does not encrypt
>   network traffic.

---

**Q31. Answer: B**

> **B** is correct. **OpenPGP (RFC 4880)** is
> the open **STANDARD** — defining message
> formats, key formats, algorithms, and trust
> model for PGP-compatible systems. **GnuPG
> (GPG — GNU Privacy Guard)** is a free,
> open-source **IMPLEMENTATION** of the OpenPGP
> standard — the actual tool you install and run.
> Multiple implementations can follow OpenPGP
> and interoperate with each other.
>
> - ❌ **A** is wrong — OpenPGP is not a paid
>   product; it is an open IETF standard.
> - ❌ **C** is wrong — GPG was created by Werner
>   Koch, not Symantec. Symantec acquired the
>   commercial PGP brand (PGP Desktop) — not GPG.
> - ❌ **D** is wrong — OpenPGP and GPG remain
>   distinct; OpenPGP is the standard, GPG is
>   one implementation. They were not merged or
>   renamed.

---

**Q32. Answer: B**

> **B** is correct. In LDAP notation:
> - `ou=` = Organizational Unit
> - `dc=` = Domain Component
> `ou=Engineering,dc=company,dc=com` represents
> an **Organizational Unit called "Engineering"**
> in the company.com domain. The full DN reads
> right-to-left for hierarchy: company.com domain
> → Engineering OU.
>
> - ❌ **A** is wrong — a user entry would have
>   `cn=` (Common Name) or `uid=` — not `ou=`.
> - ❌ **C** is wrong — `dc=` denotes Domain
>   Component; `ou=Engineering` is an
>   Organizational Unit within the domain.
> - ❌ **D** is wrong — computers typically use
>   `cn=` entries in an OU like `ou=Computers`.

---

**Q33. Answer: A**

> **A** is correct. **Append-only** means new
> blocks can only be ADDED to the chain — existing
> blocks cannot be deleted or modified. This is
> a fundamental property of blockchain — combined
> with cryptographic chaining (each block contains
> the previous block's hash), it creates an
> immutable record of all historical transactions.
>
> - ❌ **B** is wrong — blocks do not grow in
>   size by including previous block data. Each
>   block contains only its own transactions and
>   the previous block's hash (32 bytes).
> - ❌ **C** is wrong — in public blockchains
>   like Bitcoin, anyone can attempt to add blocks
>   (through mining); it is not restricted to
>   "authorized nodes."
> - ❌ **D** is wrong — block ordering is
>   chronological based on mining time, not
>   alphabetical by transaction content.

---

**Q34. Answer: C**

> **C** is correct. **EAP-TLS** is the gold
> standard for WPA2-Enterprise Wi-Fi security.
> It requires **mutual TLS authentication** —
> both the server presents a certificate to
> the client AND the client presents a certificate
> to the server. This eliminates shared passwords
> entirely — authentication is purely certificate-
> based. No credential-stuffing or password attacks
> are possible.
>
> - ❌ **A** — EAP-MD5 is a legacy, insecure
>   method that does not even authenticate the
>   server — the client cannot verify the
>   server's identity.
> - ❌ **B** — PEAP creates a TLS tunnel but
>   only requires the SERVER certificate.
>   The CLIENT authenticates inside the tunnel
>   using MSCHAPv2 (username + password) —
>   no client certificate needed.
> - ❌ **D** — EAP-FAST uses PAC (Protected
>   Access Credentials) — no client certificate
>   required; Cisco-specific.

---

**Q35. Answer: C**

> **C** is correct. **NIST SP 800-207**
> (Special Publication 800-207), published in
> August 2020, is the authoritative NIST document
> defining Zero Trust Architecture. It defines
> the 7 ZTA tenets, the three core principles
> (Verify Explicitly, Least Privilege, Assume
> Breach), and the ZTA components (PDP, PEP,
> Policy Engine).
>
> - ❌ **A** — NIST SP 800-53 defines security
>   and privacy controls for federal information
>   systems.
> - ❌ **B** — NIST SP 800-63 defines digital
>   identity guidelines (authentication assurance
>   levels).
> - ❌ **D** — NIST SP 800-171 defines protecting
>   Controlled Unclassified Information (CUI)
>   in non-federal systems.

---

**Q36. Answer: B**

> **B** is correct. In TLS 1.2, the server's
> X.509 certificate is sent in the **Certificate**
> message during the handshake — in **plaintext**,
> before the encryption keys are established.
> This means a network observer can see the
> server's certificate (including its hostname,
> organization name, and issuer) — leaking the
> server's identity even for HTTPS connections.
> TLS 1.3 encrypts the certificate exchange
> — the server certificate is hidden from passive
> observers.
>
> - ❌ **A** is wrong — TLS does not allow
>   certificate forgery; the signature is
>   verified before use.
> - ❌ **C** is wrong — in both TLS 1.2 and 1.3,
>   the client verifies the server certificate
>   during the handshake before application
>   data flows.
> - ❌ **D** is wrong — the certificate is sent
>   during the handshake, before application
>   data in both TLS 1.2 and 1.3.

---

**Q37. Answer: B**

> **B** is correct. This is the fundamental
> key direction distinction:
> **RSA Encryption:** Sender uses receiver's
> PUBLIC key → receiver decrypts with PRIVATE key.
> **RSA Digital Signature:** Signer uses their
> OWN PRIVATE key → anyone verifies with
> signer's PUBLIC key.
> Encryption protects confidentiality (only
> receiver can open). Signatures prove identity
> (only signer could have created it).
>
> - ❌ **A** is wrong — key sizes for encryption
>   and signing are the same (2048-bit RSA is
>   standard for both); key size is not the
>   distinguishing factor.
> - ❌ **C** completely inverts both operations.
> - ❌ **D** is wrong — both encryption and
>   signatures use asymmetric key pairs; the
>   DIRECTION of key usage is the difference,
>   not just the padding.

---

**Q38. Answer: B**

> **B** is correct. Bitcoin uses **double-SHA256**
> for block header hashing in Proof of Work —
> meaning SHA-256 is applied to the data, and
> then SHA-256 is applied AGAIN to the output:
> `SHA256(SHA256(block_header))`.
> This double application provides additional
> security against length extension attacks and
> was a design choice by Satoshi Nakamoto.
>
> - ❌ **A** is wrong — only ONE hash function
>   (SHA-256) is used; two keys are not involved.
>   The "double" refers to applying the SAME
>   function twice, not using two different keys.
> - ❌ **C** is wrong — the two applications are
>   sequential (output of first becomes input of
>   second), not parallel with XOR.
> - ❌ **D** is wrong — the block header is
>   hashed as a whole, not split into halves.

---

**Q39. Answer: D**

> **D** is correct. For an X.509 certificate to
> be used for S/MIME email signing and encryption,
> it must have the Extended Key Usage (EKU) value
> **emailProtection** (OID: 1.3.6.1.5.5.7.3.4).
> Email clients (Outlook, Apple Mail, Thunderbird)
> check for this EKU when selecting an S/MIME
> certificate. Without it, the certificate will
> not be available for email security operations.
>
> - ❌ **A** — serverAuth EKU is for TLS server
>   certificates (authenticating websites).
> - ❌ **B** — codeSigning EKU is for software
>   code signing certificates.
> - ❌ **C** — timeStamping EKU is specifically
>   for Time Stamp Authority (TSA) certificates
>   used in RFC 3161 timestamping operations.

---

**Q40. Answer: C**

> **C** is correct. **FIPS 140-2 Level 3** is
> the industry standard for protecting CA private
> keys. Level 3 requires:
> - Physical tamper **resistance** (not just
>   evidence) — the module detects and responds
>   to physical tampering
> - **Automatic key zeroization** — all CSPs
>   (keys, passwords) are overwritten when
>   tampering is detected
> - Identity-based authentication for operators
> The CA/Browser Forum Baseline Requirements
> reference FIPS 140-2 Level 3 for Intermediate
> CA HSMs.
>
> - ❌ **A** — Level 1 is basic; software-only
>   modules are permitted; no physical security.
> - ❌ **B** — Level 2 adds tamper-**evidence**
>   (seals that show tampering occurred) but
>   NOT tamper-resistance with key zeroization.
> - ❌ **D** — Level 4 adds environmental
>   protection (voltage/temperature attacks) —
>   the highest level, used only for the most
>   extreme security requirements.

---

&nbsp;

&nbsp;

&nbsp;

---

## PART 3 — QUICK ANSWER KEY

| Q | A | Q | A | Q | A | Q | A |
|---|---|---|---|---|---|---|---|
| 1 | B | 11 | B | 21 | D | 31 | B |
| 2 | C | 12 | B | 22 | C | 32 | B |
| 3 | B | 13 | B | 23 | B | 33 | A |
| 4 | C | 14 | B | 24 | B | 34 | C |
| 5 | A | 15 | C | 25 | C | 35 | C |
| 6 | C | 16 | B | 26 | B | 36 | B |
| 7 | B | 17 | C | 27 | C | 37 | B |
| 8 | B | 18 | C | 28 | C | 38 | B |
| 9 | C | 19 | B | 29 | B | 39 | D |
| 10 | C | 20 | C | 30 | B | 40 | C |

---

## PART 4 — SESSION COVERAGE MAP

| Session | Topic | Questions |
|---------|-------|-----------|
| 01 | Information Security, Attacks & Threats | Q1, Q15 |
| 02 | Encryption Concepts, File Encryption | Q2, Q16 |
| 03 | Cryptographic Fundamentals, Ciphers | Q3, Q17 |
| 04 | Symmetric & Asymmetric Algorithms | Q4, Q18, Q29 |
| 05 | Diffie-Hellman, Attacks, Crypto Issues | Q5, Q19 |
| 06 | Hashing: SHA & HMAC | Q6, Q20 |
| 07 | PKI Fundamentals, Digital Signatures | Q7, Q37 |
| 08 | CA, Trust Models, Revocation, Cert Types | Q8, Q22 |
| 09 | Aadhaar, e-Sign, Timestamping | Q9, Q14, Q23 |
| 10 | PKCS & FIPS 140-2 | Q10, Q24, Q40 |
| 11 | Authentication, MFA, SSO, OAuth, OpenID | Q11, Q25 |
| 12 | Authentication Protocols, FIDO, Zero Trust | Q12, Q26, Q35 |
| 13 | SSL, TLS, PGP, S/MIME | Q13, Q27, Q31, Q36, Q39 |
| 14 | IT Act, LDAP, Active Directory, Blockchain | Q28, Q30, Q32, Q33, Q34, Q38 |

---

## PART 5 — SCORE INTERPRETATION

| Score | Meaning |
|-------|---------|
| **38–40** | ✅ Excellent — Exam ready. Strong foundation across all sessions. |
| **34–37** | ✅ Good — Review the sessions where you lost marks. |
| **28–33** | ⚠️ Fair — Revisit session notes for weak areas before the next set. |
| **Below 28** | ❌ Re-read session notes before attempting Set 02. |

---

### Difficulty Distribution Used in This Set

| Level | % | MCQs | Questions |
|-------|---|------|-----------|
| Foundation | 40% | 16 | Q1,Q3,Q4,Q6,Q10,Q12,Q13,Q15,Q18,Q19,Q22,Q25,Q31,Q35,Q38,Q40 |
| Fundamental | 40% | 16 | Q2,Q5,Q7,Q8,Q9,Q16,Q17,Q20,Q21,Q23,Q24,Q27,Q29,Q30,Q33,Q37 |
| Basic Concepts | 20% | 8 | Q11,Q14,Q26,Q28,Q32,Q34,Q36,Q39 |

---