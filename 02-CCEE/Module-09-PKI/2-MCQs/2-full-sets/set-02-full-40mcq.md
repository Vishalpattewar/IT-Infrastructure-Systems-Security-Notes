# Full MCQ Set 02 — PKI Module
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

**Q1.** Which of the following CORRECTLY
maps a CIA property to the attack that
violates it?

- A) Website defacement → Availability
- B) Ransomware encrypting files → Confidentiality
- C) DDoS attack → Integrity
- D) Unauthorized modification of a
     database record → Integrity

---

**Q2.** EFS (Encrypting File System) uses
a two-key architecture. The actual file
content is encrypted with which type of key?

- A) The user's RSA private key directly
- B) A random symmetric key called the
     File Encryption Key (FEK)
- C) A hash of the user's Windows login
     password
- D) The user's Kerberos session ticket

---

**Q3.** Shannon's property of DIFFUSION
states that the influence of a single
plaintext bit should spread across many
ciphertext bits. Which operation in AES
primarily implements diffusion?

- A) SubBytes — S-Box lookup
- B) AddRoundKey — XOR with round key
- C) ShiftRows and MixColumns
- D) KeyExpansion — round key generation

---

**Q4.** RC5 was designed by Ron Rivest
in 1994. What is its most distinctive
and novel feature compared to other
ciphers of its era?

- A) It was the first cipher to use
     S-Boxes for non-linear substitution
- B) It uses data-dependent rotations —
     the rotation amount depends on the
     actual data being encrypted
- C) It uses 256-bit keys — far larger
     than any contemporary cipher
- D) It applies both encryption and
     digital signing in a single pass

---

**Q5.** In the Diffie-Hellman key exchange,
public parameters are p = 23, g = 5.
Bob's private key is b = 15 and Alice
sends her public value A = 8. What is
the shared secret S that Bob computes?

- A) 15
- B) 2
- C) 19
- D) 7

---

**Q6.** HMAC uses two constants — ipad
and opad — in its construction. What
are the correct hexadecimal values?

- A) ipad = 0xFF, opad = 0x00
- B) ipad = 0x5C, opad = 0x36
- C) ipad = 0x36, opad = 0x5C
- D) ipad = 0xAA, opad = 0x55

---

**Q7.** A Root CA certificate has the
property that its Issuer field and Subject
field contain the same Distinguished Name.
What is a certificate with this property
called?

- A) A cross-certificate
- B) A self-signed certificate
- C) An intermediate certificate
- D) A proxy certificate

---

**Q8.** OCSP Stapling solves two problems
with standard OCSP. What are they?

- A) Certificate forgery and chain
     validation failures
- B) Privacy (CA tracks browsing) and
     performance (extra round-trip per
     connection)
- C) Certificate expiry and weak
     cipher suite negotiation
- D) Revocation list size and
     CA key compromise detection

---

**Q9.** In Aadhaar e-KYC, what does UIDAI
return to an authorized KUA (KYC User
Agency) after successful authentication —
in addition to the YES/NO response?

- A) The resident's biometric data —
     fingerprints and iris scans
- B) The resident's Aadhaar number and
     registered mobile number
- C) Demographic data including name,
     address, photo, and date of birth
     — with resident's explicit consent
- D) A signed certificate bound to
     the resident's identity

---

**Q10.** PKCS#5 defines PBKDF2. In WPA2,
PBKDF2 is used with HMAC-SHA1. What
specific output does it produce in
WPA2-Personal (PSK) mode?

- A) The Wi-Fi session encryption key
     used directly for AES-CCMP
- B) The Pairwise Master Key (PMK)
     derived from the Wi-Fi passphrase
     and SSID
- C) The SSID broadcast identifier
     derived from the router's
     MAC address
- D) The Pre-Shared Key (PSK) that
     replaces the user's password
     in the handshake

---

**Q11.** OAuth 2.0 defines four roles.
Which role is the server that hosts
the user's protected resources and
validates access tokens?

- A) Authorization Server
- B) Resource Owner
- C) Client
- D) Resource Server

---

**Q12.** In 802.1X authentication, before
a supplicant successfully authenticates,
what is the state of the network port?

- A) Fully open — all traffic allowed
     until authentication times out
- B) UNAUTHORIZED — only EAPOL
     traffic is permitted
- C) Half-open — only HTTPS traffic
     is allowed through
- D) Quarantine — traffic is allowed
     but routed through an IDS

---

**Q13.** PGP follows a "sign-then-encrypt"
convention. Why is "encrypt-then-sign"
considered weaker?

- A) Encrypting first makes the hash
     longer than RSA can sign directly
- B) If you sign the ciphertext, anyone
     could strip your signature and
     re-sign it — falsely claiming
     authorship of the ciphertext
- C) Encryption uses more battery
     power so signing should happen
     first to save resources
- D) The TLS transport layer requires
     signing before encryption for
     compatibility

---

**Q14.** The Aadhaar Act 2016 was
challenged in the Supreme Court of India.
What was the KEY restriction placed on
Aadhaar use by the Puttaswamy judgment
in 2018?

- A) Aadhaar was declared completely
     unconstitutional and banned
- B) Aadhaar was upheld but private
     companies cannot mandate it —
     it remains valid for government
     services
- C) Aadhaar was restricted to
     biometric use only — OTP
     authentication was prohibited
- D) Aadhaar was declared valid only
     for citizens — not for residents
     of India

---

**Q15.** The Parkerian Hexad extends the
CIA Triad by adding three properties.
You have an encrypted USB drive but
you left it in a taxi. Which Parkerian
property is violated even though the
data remains encrypted?

- A) Utility — the key might be lost
- B) Authenticity — the drive's origin
     cannot be verified
- C) Possession — physical control
     of the medium has been lost
- D) Confidentiality — it could be
     decrypted by someone else

---

**Q16.** In RSA key generation, the
private exponent d is calculated as:

- A) d = e × φ(n) mod n
- B) d = e⁻¹ mod φ(n)
     (modular multiplicative inverse
     of e with respect to φ(n))
- C) d = p × q mod e
- D) d = (p-1) × (q-1) mod e

---

**Q17.** Which of the following is the
CORRECT formula that expresses the
relationship between the DH shared
secret and both parties' contributions?

- A) S = (A + B) mod p
- B) S = gᵃᵇ mod p — Alice computes
     Bᵃ mod p and Bob computes
     Aᵇ mod p — both arrive at
     the same value
- C) S = HMAC-SHA256(A, B)
- D) S = A × B mod g

---

**Q18.** AES performs 10 rounds for
AES-128. In EVERY round EXCEPT the
final round, four operations are
performed. Which operation is
deliberately OMITTED from the
final round?

- A) SubBytes
- B) AddRoundKey
- C) ShiftRows
- D) MixColumns

---

**Q19.** The CRIME attack (2012)
exploited which TLS feature to
leak plaintext session data?

- A) CBC padding in TLS 1.0
- B) Weak DHE parameters in TLS 1.2
- C) TLS-level data compression —
     ciphertext length leaks
     information about plaintext
- D) RSA key transport without
     Perfect Forward Secrecy

---

**Q20.** SHA-1 was broken by a practical
collision attack in 2017. Who demonstrated
this attack, what was it called, and
approximately how much did it cost?

- A) Bruce Schneier and NSA —
     "HashBreak" — $1 million
- B) Google and CWI Amsterdam —
     "SHAttered" — ~$110,000
- C) Researchers at MIT —
     "HashClash" — ~$50,000
- D) NIST and DHS — "SHA-FAIL" —
     classified budget

---

**Q21.** An X.509 v3 certificate has a
Basic Constraints extension marked as
CRITICAL with `CA:TRUE` and
`pathLenConstraint=0`. What does
this mean?

- A) This is an end-entity certificate
     that cannot sign anything
- B) This is a CA certificate that
     can sign other CA certificates
     to any depth
- C) This is a CA certificate but it
     can ONLY sign end-entity
     certificates — not other
     CA certificates
- D) This certificate has an expired
     path and must be renewed

---

**Q22.** CRL and OCSP both serve certificate
revocation checking. Which statement
correctly describes a LIMITATION of CRL?

- A) CRL cannot handle RSA certificates
     — only ECDSA certificates
- B) CRL grows over time and can become
     very large — downloading it for
     every TLS connection adds
     significant latency
- C) CRL is updated in real-time so
     it cannot handle high-volume
     revocation events
- D) CRL is only available on port
     443 which conflicts with HTTPS

---

**Q23.** RFC 3161 defines the Time Stamp
Protocol (TSP). What specific value
in the Time Stamp Token (TST) records
the exact time of timestamping?

- A) issuerTime
- B) certTime
- C) genTime
- D) signingTime

---

**Q24.** PKCS#8 and PKCS#1 both define
formats for private keys. When you see
a file starting with:
`-----BEGIN PRIVATE KEY-----`
which format is this?

- A) PKCS#1 — RSA-specific key
- B) PKCS#8 — algorithm-independent
     private key format
- C) PKCS#12 — certificate and key
     bundle
- D) PKCS#10 — Certificate Signing
     Request

---

**Q25.** In OpenID Connect, the ID Token
is a JWT containing claims about the
authenticated user. Which claim
uniquely identifies the user at
the Identity Provider?

- A) iss — the issuer of the token
- B) aud — the audience the token
     is intended for
- C) sub — the subject identifier
     (unique user ID at the IdP)
- D) exp — the expiry time of
     the token

---

**Q26.** FIDO2 consists of two components.
WebAuthn is the W3C browser API standard.
What does CTAP2 define?

- A) The format for storing FIDO2
     credentials in a password manager
- B) The protocol for communication
     between the browser/OS platform
     and the FIDO2 authenticator
     (hardware key, phone)
- C) The JWT format used to transmit
     FIDO2 assertion responses to
     the server
- D) The certificate format used
     for FIDO2 attestation in
     enterprise deployments

---

**Q27.** S/MIME uses PKCS#7 / CMS for its
message structure. When a user sends
a digitally signed email using S/MIME,
what file extension is used for the
detached signature attachment?

- A) .p12
- B) .p7b
- C) .p7s
- D) .csr

---

**Q28.** Under the IT Act 2000,
Section 66C defines identity theft.
What is the punishment?

- A) Up to 3 years imprisonment
     OR fine up to ₹1 lakh
- B) Up to 3 years imprisonment
     AND fine up to ₹1 lakh
- C) Up to 5 years imprisonment
     AND fine up to ₹5 lakh
- D) Up to 10 years imprisonment
     with no option of fine

---

**Q29.** In the ECC key generation process,
the public key P is computed from the
private key k and the generator point G.
What operation produces the public key?

- A) P = k + G (point addition)
- B) P = k × G (scalar multiplication
     of the generator point by the
     private key)
- C) P = Hash(k || G)
- D) P = G^k mod p

---

**Q30.** In the Kerberos authentication
flow, why does the protocol require
all participating systems to have
clocks synchronized within 5 minutes?

- A) The AES-256 encryption used in
     Kerberos requires synchronized
     seeds to generate consistent keys
- B) Timestamps in Kerberos tickets
     prevent replay attacks — an
     out-of-sync clock could cause
     valid tickets to be rejected or
     allow replayed tickets to be
     accepted
- C) DNS resolution for Kerberos
     realm lookups requires NTP
     to be running on all systems
- D) The KDC's load balancing
     algorithm distributes requests
     based on client system time

---

**Q31.** TLS 1.3 defines exactly 5
cipher suites — all using AEAD. Which
of the following is NOT one of the
5 TLS 1.3 cipher suites?

- A) TLS_AES_128_GCM_SHA256
- B) TLS_CHACHA20_POLY1305_SHA256
- C) TLS_AES_256_GCM_SHA384
- D) TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256

---

**Q32.** Active Directory stores its
database in a specific file on each
Domain Controller. What is the name
of this file?

- A) SYSVOL.dat
- B) NTDS.dit
- C) AD-Store.mdb
- D) schema.ldf

---

**Q33.** Bitcoin's blockchain uses
a Merkle tree to organize transactions
within each block. What is stored
in the block header that represents
ALL transactions in the block?

- A) The full list of transaction IDs
     concatenated together
- B) The hash of the last transaction
     in the block
- C) The Merkle Root — a single hash
     value derived from hashing all
     transactions through the tree
- D) The digital signature of the
     miner who created the block

---

**Q34.** RADIUS and TACACS+ are both
AAA protocols used in enterprise
network access. Which transport
protocol does TACACS+ use, and what
encryption advantage does it have
over RADIUS?

- A) UDP — TACACS+ encrypts only
     the password field
- B) TCP — TACACS+ encrypts the
     entire packet payload
- C) TLS — TACACS+ uses mutual
     certificate authentication
- D) SCTP — TACACS+ provides
     multi-path packet delivery

---

**Q35.** Zero Trust Architecture has
three core principles per NIST SP
800-207. Which of the following is
one of those three principles?

- A) Trust internal users — verify
     only external users
- B) Encrypt all data at rest using
     AES-256 minimum
- C) Assume Breach — design and
     operate as if the network is
     already compromised
- D) Use perimeter firewalls as the
     primary defense mechanism

---

**Q36.** SNI (Server Name Indication)
is a TLS extension. What privacy
concern does SNI introduce?

- A) SNI exposes the server's private
     key to any client that connects
- B) SNI includes the target hostname
     in the TLS ClientHello in
     plaintext — network observers
     can see which domain you are
     connecting to before encryption
- C) SNI allows the server to
     identify the user by their
     IP address without consent
- D) SNI bypasses certificate
     validation allowing MITM attacks

---

**Q37.** ECC provides equivalent security
to RSA with much smaller key sizes.
According to NIST, what ECC key size
provides equivalent security to
RSA-3072?

- A) 128-bit ECC
- B) 192-bit ECC
- C) 256-bit ECC
- D) 384-bit ECC

---

**Q38.** In the blockchain Proof of Work
consensus, what is the purpose of the
NONCE field in the block header?

- A) It identifies the miner who
     successfully solved the puzzle
- B) It is a variable value that miners
     change repeatedly until the
     block header hash meets the
     target difficulty (starts with
     enough zeros)
- C) It stores the transaction count
     to prevent duplicate blocks
     with identical content
- D) It is the cryptographic random
     seed used to generate the
     previous block's hash

---

**Q39.** HSTS (HTTP Strict Transport
Security) has a "preload" directive.
What does the preload list enable?

- A) The server pre-loads all TLS
     certificates at startup to
     avoid connection delays
- B) The browser pre-loads JavaScript
     from HTTPS sources only —
     blocking HTTP scripts
- C) The domain is included in a
     built-in browser list — enforcing
     HTTPS from the very FIRST visit
     even before the HSTS header
     is received
- D) The CA pre-loads the domain's
     certificate into CT logs before
     issuance to prevent delays

---

**Q40.** FIPS 140-2 defines the concept
of "zeroization." When does zeroization
occur in a FIPS 140-2 Level 3 module,
and what is zeroized?

- A) At power-on, all memory is
     zeroed to ensure clean startup
- B) When physical tampering is
     detected, all Critical Security
     Parameters (keys, passwords)
     are immediately overwritten
     with zeros to prevent extraction
- C) When the module is decommissioned,
     the certificate database is
     cleared by replacing entries
     with zeros
- D) After each cryptographic
     operation, the session keys
     are zeroed to prevent caching

---

&nbsp;

&nbsp;

&nbsp;

---

## PART 2 — ANSWERS AND EXPLANATIONS

---

**Q1. Answer: D**

> **D** is correct. Unauthorized modification
> of a database record violates **Integrity** —
> the assurance that data is accurate and has
> not been altered without authorization.
>
> - ❌ **A** is wrong — website defacement
>   violates **Integrity** (the content was
>   modified), not Availability (the site is
>   still accessible, just with different
>   content).
> - ❌ **B** is wrong — ransomware primarily
>   violates **Availability** (files are
>   inaccessible), not Confidentiality (data
>   is not necessarily disclosed, just
>   encrypted by the attacker).
> - ❌ **C** is wrong — a DDoS attack violates
>   **Availability** (prevents legitimate
>   access to the service), not Integrity.

---

**Q2. Answer: B**

> **B** is correct. EFS uses a two-key hybrid
> architecture: a random symmetric key called
> the **FEK (File Encryption Key)** encrypts
> the actual file content — using AES in modern
> Windows versions. The FEK itself is then
> encrypted with the user's RSA public key and
> stored in the DDF (Data Decryption Field) in
> the file's metadata. This hybrid model (AES
> for data, RSA for key protection) is efficient
> and secure.
>
> - ❌ **A** is wrong — the RSA private key
>   is used to decrypt the FEK, not to encrypt
>   file content directly. Encrypting file
>   content with RSA directly would be
>   impractically slow.
> - ❌ **C** is wrong — EFS does not derive
>   its encryption key from the Windows login
>   password. The FEK is randomly generated;
>   the user's certificate-based public key
>   protects it.
> - ❌ **D** is wrong — Kerberos session tickets
>   are used for network authentication, not
>   for local file encryption keys.

---

**Q3. Answer: C**

> **C** is correct. In AES, **Shannon's
> Diffusion** is implemented by **ShiftRows**
> (moves bytes across rows ensuring they land
> in different columns) and **MixColumns**
> (multiplies each column by a fixed polynomial
> in GF(2⁸), ensuring each output byte depends
> on all 4 input bytes of the column). Together
> they spread the influence of one plaintext
> byte across the entire state.
>
> - ❌ **A** is wrong — **SubBytes** (S-Box
>   lookup) implements **Confusion** — making
>   the relationship between key and ciphertext
>   complex, not spreading plaintext influence.
> - ❌ **B** is wrong — **AddRoundKey** provides
>   key mixing via XOR — it is neither Confusion
>   nor Diffusion in Shannon's specific sense;
>   it is the keyed step.
> - ❌ **D** is wrong — KeyExpansion generates
>   round keys from the original key; it is a
>   key schedule operation, not a data
>   transformation implementing Diffusion.

---

**Q4. Answer: B**

> **B** is correct. RC5's defining innovation
> was its use of **data-dependent rotations** —
> the amount of bit rotation applied to data
> in each round depends on the actual data
> values being encrypted, not a fixed schedule.
> This makes algebraic cryptanalysis and
> differential attacks significantly harder
> because the operations are unpredictable
> from the key alone.
>
> - ❌ **A** is wrong — S-Boxes for non-linear
>   substitution were used by DES (1977) —
>   17 years before RC5. In fact, RC5 uses
>   NO S-Boxes — only XOR, addition, and
>   rotation (ARX design).
> - ❌ **C** is wrong — RC5 supports variable
>   key sizes from 0 to 2040 bits, but
>   256-bit keys were not its defining
>   innovation. The data-dependent rotation
>   is what made RC5 notable.
> - ❌ **D** is wrong — combined encryption
>   and signing is not a feature of RC5. RC5
>   is a symmetric block cipher only.

---

**Q5. Answer: B**

> **B** is correct. Bob computes the shared
> secret using Alice's public value A = 8:
> S = Aᵇ mod p = 8¹⁵ mod 23.
> Computing 8¹⁵ mod 23:
> 8¹ = 8, 8² = 64 mod 23 = 18,
> 8⁴ = 18² mod 23 = 324 mod 23 = 2,
> 8⁸ = 2² mod 23 = 4,
> 8¹⁵ = 8⁸ × 8⁴ × 8² × 8¹
> = 4 × 2 × 18 × 8 mod 23
> = 4 × 2 = 8; 8 × 18 = 144 mod 23 = 6;
> 6 × 8 = 48 mod 23 = 2.
> Shared secret S = **2**.
> (Verify: Alice computes Bᵃ = 19⁴ mod 23 =
> 130321 mod 23 = 2 ✅ — same shared secret.)
>
> - ❌ **A (15)** is Bob's private key — never
>   the shared secret.
> - ❌ **C (19)** is Bob's public value B —
>   not the shared secret.
> - ❌ **D (7)** is not the result of 8¹⁵ mod 23.

---

**Q6. Answer: C**

> **C** is correct. The HMAC specification
> (RFC 2104) defines:
> **ipad = 0x36** repeated to block size
> (XORed with key for inner hash).
> **opad = 0x5C** repeated to block size
> (XORed with key for outer hash).
> Memory hook: **i** comes before **o**
> alphabetically, and **3** (0x36) comes
> before **5** (0x5C) numerically.
>
> - ❌ **A** is wrong — 0xFF and 0x00 are
>   not HMAC constants. These are not defined
>   anywhere in the HMAC specification.
> - ❌ **B** is wrong — this swaps ipad and
>   opad. 0x5C is the OUTER padding (opad)
>   and 0x36 is the INNER padding (ipad).
>   Swapping them is the direct exam trap.
> - ❌ **D** is wrong — 0xAA and 0x55 are
>   alternating bit patterns common in memory
>   testing — not HMAC padding constants.

---

**Q7. Answer: B**

> **B** is correct. When the **Issuer** field
> (who signed the certificate) and the
> **Subject** field (who the certificate
> belongs to) contain the same Distinguished
> Name, the certificate is **self-signed**.
> Root CA certificates are self-signed because
> there is no higher authority to sign them.
> This is also why they must be manually trusted
> (pre-installed in trust stores) rather than
> automatically trusted through chain validation.
>
> - ❌ **A** is wrong — a cross-certificate is
>   issued when one CA signs another CA's
>   certificate to establish cross-organizational
>   trust. Issuer and Subject are different CAs.
> - ❌ **C** is wrong — an intermediate
>   certificate is signed by the Root CA —
>   issuer (Root CA) ≠ subject (Intermediate CA).
> - ❌ **D** is wrong — a proxy certificate is
>   issued by an end-entity (for Grid computing
>   delegation) — issuer (user) ≠ subject
>   (proxy identity).

---

**Q8. Answer: B**

> **B** is correct. Standard OCSP has two
> significant problems:
> (1) **Privacy** — every TLS connection
> requires the client to query the CA's OCSP
> responder, revealing which websites the user
> visits to the CA.
> (2) **Performance** — each TLS handshake
> incurs an extra network round-trip to the
> OCSP server, adding latency.
> OCSP Stapling solves both: the server pre-fetches
> its own OCSP response and attaches it to the
> TLS handshake — the client never contacts the CA.
>
> - ❌ **A** is wrong — certificate forgery is
>   prevented by the CA's signature on the cert,
>   not by OCSP. Chain validation is a separate
>   certificate path validation step.
> - ❌ **C** is wrong — certificate expiry is
>   checked via the validity period fields;
>   cipher suite negotiation is part of the
>   TLS handshake. Neither is what OCSP Stapling
>   specifically addresses.
> - ❌ **D** is wrong — CRL size is a limitation
>   of CRL (not OCSP). CA key compromise
>   detection is not what OCSP Stapling solves.

---

**Q9. Answer: C**

> **C** is correct. Aadhaar **e-KYC** goes
> beyond basic authentication (YES/NO). After
> successful authentication AND with the
> resident's **explicit consent**, UIDAI returns
> **demographic data** to the authorized KUA —
> typically: name, address, date of birth,
> gender, and photograph. This enables banks
> and telecom operators to complete customer
> KYC entirely digitally without physical
> document submission.
>
> - ❌ **A** is wrong — biometric data (fingerprints,
>   iris scans) NEVER leaves UIDAI's CIDR. The
>   architecture is designed so AUAs/KUAs submit
>   biometrics for matching and receive only the
>   result — raw biometric data is never shared.
> - ❌ **B** is wrong — the Aadhaar number and
>   mobile number are not what e-KYC returns.
>   e-KYC returns demographic identity data to
>   enable the KYC process.
> - ❌ **D** is wrong — UIDAI does not issue
>   certificates as part of e-KYC. Certificate
>   issuance is the ESP's function in e-Sign,
>   not in e-KYC.

---

**Q10. Answer: B**

> **B** is correct. In WPA2-Personal (PSK mode),
> PBKDF2-HMAC-SHA1 is used with the Wi-Fi
> passphrase and the SSID (as salt) with 4096
> iterations to derive the **PMK (Pairwise
> Master Key)**:
> `PMK = PBKDF2(HMAC-SHA1, passphrase, SSID,
> 4096, 256 bits)`.
> The SSID acting as salt means pre-computed
> rainbow tables built for one SSID are useless
> for a different SSID — which is why unique
> SSIDs improve WPA2 security.
>
> - ❌ **A** is wrong — the session encryption
>   key (PTK — Pairwise Transient Key) for
>   AES-CCMP is derived from the PMK through a
>   4-way handshake with additional nonces —
>   PBKDF2 does not directly produce the session
>   key.
> - ❌ **C** is wrong — the SSID is a human-
>   configured network name; it is not derived
>   from MAC address using PBKDF2.
> - ❌ **D** is wrong — the PMK IS the
>   Pre-Shared Key equivalent in WPA2-PSK mode.
>   PBKDF2 converts the human-readable passphrase
>   into a 256-bit PMK — this is the PSK.

---

**Q11. Answer: D**

> **D** is correct. In OAuth 2.0, the four
> roles are:
> **Resource Owner** — the user who owns data.
> **Client** — the app requesting access.
> **Authorization Server** — issues tokens.
> **Resource Server** — hosts protected resources
> and **validates access tokens** when clients
> present them to access data (e.g., Google
> Photos API).
>
> - ❌ **A** is wrong — the **Authorization
>   Server** issues the access token after
>   the user grants consent; it does NOT host
>   the protected resources.
> - ❌ **B** is wrong — the **Resource Owner**
>   is the user who owns the data and grants
>   consent — not the server hosting resources.
> - ❌ **C** is wrong — the **Client** is the
>   third-party application requesting access
>   — it receives and uses the access token
>   but does not validate it.

---

**Q12. Answer: B**

> **B** is correct. Before successful 802.1X
> authentication, the network port is in the
> **UNAUTHORIZED state**. In this state, all
> traffic is blocked EXCEPT **EAPOL (EAP over
> LAN)** packets — which carry the EAP
> authentication exchange between the supplicant
> and the authenticator. Only after the RADIUS
> server returns Access-Accept does the port
> transition to AUTHORIZED state and allow
> normal traffic.
>
> - ❌ **A** is wrong — 802.1X's entire purpose
>   is to block network access until
>   authentication succeeds. Allowing all
>   traffic until timeout would defeat
>   the access control objective.
> - ❌ **C** is wrong — 802.1X does not filter
>   by protocol (HTTPS vs HTTP) in the
>   unauthorized state. Only EAPOL authentication
>   traffic passes through — not HTTPS.
> - ❌ **D** is wrong — quarantine VLANs are
>   a post-authentication feature for non-
>   compliant devices in some NAC solutions.
>   The basic 802.1X unauthorized state is
>   EAPOL-only, not a monitored quarantine.

---

**Q13. Answer: B**

> **B** is correct. If you **encrypt first**
> then sign the ciphertext, a malicious
> recipient could strip your signature from
> the ciphertext and replace it with their own
> signature — effectively claiming they created
> the ciphertext. This is a known attack called
> "surreptitious forwarding." **Signing first**
> (signing the plaintext) then encrypting means
> the signature proves you created the specific
> plaintext — stripping and re-signing is not
> meaningful because the signature is over the
> plaintext content, not arbitrary ciphertext.
>
> - ❌ **A** is wrong — hash size is not the
>   issue. The hash of the plaintext or ciphertext
>   both fit within RSA's signing capacity.
> - ❌ **C** is wrong — battery consumption is
>   not a cryptographic security consideration;
>   this is an implementation concern, not a
>   security vulnerability.
> - ❌ **D** is wrong — TLS transport layer
>   requirements have nothing to do with the
>   sign-then-encrypt convention in PGP/S/MIME.

---

**Q14. Answer: B**

> **B** is correct. In the landmark
> **Puttaswamy judgment (2018)**, the Supreme
> Court of India upheld Aadhaar as constitutionally
> valid but struck down the provision allowing
> **private companies** to mandate Aadhaar for
> their services. Aadhaar remains mandatory for
> specific government benefits (PDS, income tax
> PAN linking) but private entities (banks,
> telecom) cannot mandate it — only voluntary
> use with consent is permitted (clarified by
> the 2019 Amendment).
>
> - ❌ **A** is wrong — Aadhaar was NOT declared
>   unconstitutional. The Supreme Court upheld
>   its constitutional validity for government
>   purposes.
> - ❌ **C** is wrong — the ruling did not
>   restrict OTP authentication. All Aadhaar
>   authentication modes (OTP, biometric)
>   remain valid for government services.
> - ❌ **D** is wrong — Aadhaar is designed for
>   ALL RESIDENTS of India (not just citizens),
>   which was a deliberate policy choice for
>   inclusive identity coverage.

---

**Q15. Answer: C**

> **C** is correct. The Parkerian Hexad adds
> **Possession/Control** to the CIA Triad.
> Possession is violated when you lose physical
> control of a medium — even if the data remains
> encrypted and unread. You no longer control
> who has the physical device, creating risk even
> if the encryption is strong. This is distinct
> from Confidentiality (which might remain intact
> if the encryption holds) and Utility (which
> could be intact if you have the key elsewhere).
>
> - ❌ **A** is wrong — Utility is violated when
>   data becomes unusable (e.g., encryption key
>   is lost and the data cannot be decrypted).
>   If you still have the key, Utility is intact.
> - ❌ **B** is wrong — Authenticity refers to
>   data being genuine and from a claimed source —
>   not about physical possession of a medium.
> - ❌ **D** is wrong — Confidentiality may still
>   be intact if the encryption is strong and
>   the key has not been compromised. The
>   question specifically notes the data "remains
>   encrypted."

---

**Q16. Answer: B**

> **B** is correct. The private exponent d
> in RSA is computed as the **modular
> multiplicative inverse of the public exponent
> e with respect to Euler's totient φ(n)**:
> `d = e⁻¹ mod φ(n)`
> This means: `d × e ≡ 1 (mod φ(n))`.
> Given e and φ(n), d is computed using the
> extended Euclidean algorithm. The security of
> RSA relies on the fact that without knowing
> p and q (and therefore φ(n)), computing d
> from e alone is infeasible.
>
> - ❌ **A** is wrong — multiplying e by φ(n)
>   and taking mod n produces a meaningless
>   value, not the private exponent.
> - ❌ **C** is wrong — p × q = n (the modulus),
>   not d. The private exponent is derived from
>   φ(n) = (p-1)(q-1), not from p × q.
> - ❌ **D** is wrong — (p-1) × (q-1) = φ(n),
>   not d. φ(n) is used to COMPUTE d but is
>   not d itself.

---

**Q17. Answer: B**

> **B** is correct. In Diffie-Hellman:
> Alice computes S = Bᵃ mod p =
> (gᵇ)ᵃ mod p = gᵃᵇ mod p.
> Bob computes S = Aᵇ mod p =
> (gᵃ)ᵇ mod p = gᵃᵇ mod p.
> Both arrive at gᵃᵇ mod p — the shared
> secret. An eavesdropper sees A = gᵃ mod p
> and B = gᵇ mod p but computing gᵃᵇ mod p
> from this requires solving the Discrete
> Logarithm Problem (finding a from A or
> b from B) — computationally infeasible
> for large p.
>
> - ❌ **A** is wrong — (A + B) mod p has no
>   relationship to DH shared secret derivation.
>   DH uses modular exponentiation, not addition.
> - ❌ **C** is wrong — HMAC is not involved
>   in DH key exchange. The shared secret is
>   derived purely from modular arithmetic.
> - ❌ **D** is wrong — A × B mod g inverts
>   the roles of g and the values; this is
>   not the DH formula.

---

**Q18. Answer: D**

> **D** is correct. **MixColumns is omitted
> from the final AES round**. The designers
> of Rijndael (AES) made this deliberate choice
> because: (1) Adding MixColumns in the final
> round provides no additional security —
> there is no subsequent SubBytes to benefit
> from the mixing; and (2) Omitting it
> simplifies the implementation of the
> inverse cipher (decryption).
>
> - ❌ **A** is wrong — SubBytes IS performed
>   in the final round. The S-Box substitution
>   continues to provide non-linearity in the
>   last round.
> - ❌ **B** is wrong — AddRoundKey is the
>   LAST operation in every round including
>   the final round, and also the FIRST
>   operation (initial round key addition).
>   It is never omitted.
> - ❌ **C** is wrong — ShiftRows IS performed
>   in the final round. Row shifting continues
>   to provide diffusion in the last round.

---

**Q19. Answer: C**

> **C** is correct. The **CRIME (Compression
> Ratio Info-Leak Made Easy)** attack (2012)
> exploited **TLS-level data compression**.
> When data is compressed before encryption,
> the resulting ciphertext length leaks
> information about the plaintext — because
> identical or similar strings compress more
> efficiently, producing shorter output. An
> attacker who can inject chosen content and
> observe ciphertext lengths can recover secret
> values (like session cookies) character by
> character.
>
> - ❌ **A** is wrong — CBC padding exploitation
>   in TLS 1.0 is the **BEAST attack (2011)**.
>   CRIME targeted compression, not padding.
> - ❌ **B** is wrong — weak DHE parameters
>   are exploited by the **Logjam attack (2015)**.
> - ❌ **D** is wrong — RSA key transport
>   without PFS is the concern addressed by
>   requiring ECDHE in TLS 1.3; it is not
>   what CRIME exploited.

---

**Q20. Answer: B**

> **B** is correct. The **SHAttered** attack
> was demonstrated by **Google (Project Zero)
> and CWI Amsterdam** in **2017**. They produced
> the first practical SHA-1 collision — two
> different PDF files with identical SHA-1 hashes.
> The cost was approximately **$110,000** in
> cloud computing resources (9.2 × 10¹⁸ SHA-1
> computations). This definitively proved SHA-1's
> collision resistance was broken in practice.
>
> - ❌ **A** is wrong — Bruce Schneier did not
>   lead the SHAttered research. The NSA was
>   not involved in publishing this. The name
>   "HashBreak" is fabricated.
> - ❌ **C** is wrong — MIT was not involved in
>   SHAttered. "HashClash" is a related research
>   project for chosen-prefix collisions (Marc
>   Stevens) but not the 2017 practical collision
>   demonstration.
> - ❌ **D** is wrong — SHAttered was academic/
>   industry research, not a government classified
>   project. NIST and DHS were not the authors.

---

**Q21. Answer: C**

> **C** is correct. The Basic Constraints
> extension with `CA:TRUE` indicates this is
> a CA certificate (can sign other certificates).
> `pathLenConstraint=0` means this CA can sign
> **end-entity certificates only** — it cannot
> issue certificates to other CAs (path length
> 0 means zero more CA certificates are allowed
> in the chain below this one). This is the
> typical setting for an Issuing CA at the
> bottom of a three-tier hierarchy.
>
> - ❌ **A** is wrong — `CA:TRUE` specifically
>   identifies this as a CA certificate — an
>   end-entity certificate would have `CA:FALSE`
>   or no Basic Constraints extension.
> - ❌ **B** is wrong — if pathLen were absent
>   or set to a higher value, it could sign
>   more CA levels. `pathLenConstraint=0`
>   specifically prohibits issuing more CA certs.
> - ❌ **D** is wrong — pathLenConstraint has
>   nothing to do with certificate expiry or
>   renewal; it is a structural constraint on
>   the CA hierarchy depth.

---

**Q22. Answer: B**

> **B** is correct. A significant limitation
> of CRL is that it **grows continuously** as
> more certificates are revoked and never shrinks
> (expired certs are typically kept until they
> expire). For large CAs, CRLs can grow to
> several megabytes. Downloading the full CRL
> for every TLS connection adds substantial
> overhead — both in data transfer and latency.
> This is one reason OCSP was developed as a
> per-certificate alternative.
>
> - ❌ **A** is wrong — CRL supports all
>   certificate types regardless of algorithm
>   (RSA, ECDSA, DSA). Algorithm type is not
>   a CRL limitation.
> - ❌ **C** is wrong — CRL is NOT updated
>   in real-time. It is published periodically
>   (daily, weekly) which means there is a
>   gap between revocation and CRL publication.
>   This is actually another limitation of CRL.
> - ❌ **D** is wrong — CRL is distributed over
>   HTTP (specified in the CDP extension) —
>   port 80, not 443. There is no port conflict
>   with HTTPS.

---

**Q23. Answer: C**

> **C** is correct. The **genTime** field in
> a Time Stamp Token (TST) contains the
> exact time the TSA generated the timestamp,
> expressed in UTC (Coordinated Universal Time)
> with accuracy typically to the millisecond or
> second. This field, combined with the hash of
> the document and the TSA's digital signature,
> creates the cryptographic proof of existence
> at that specific time.
>
> - ❌ **A** is wrong — "issuerTime" is not
>   a field in the TST structure defined in
>   RFC 3161. This is a fabricated term.
> - ❌ **B** is wrong — "certTime" is not
>   a standard TST field. Certificate validity
>   times (notBefore, notAfter) are in the TSA's
>   certificate — not in the TST itself.
> - ❌ **D** is wrong — "signingTime" is a
>   CMS (PKCS#7) signed attribute used in
>   S/MIME — not the standard time field in
>   RFC 3161 Time Stamp Tokens.

---

**Q24. Answer: B**

> **B** is correct. The PEM header
> `-----BEGIN PRIVATE KEY-----` identifies
> a **PKCS#8** formatted private key —
> algorithm-independent format. The `PRIVATE KEY`
> header (without specifying the algorithm)
> is the standard PKCS#8 unencrypted format.
> Contrast with `-----BEGIN RSA PRIVATE KEY-----`
> which is the older **PKCS#1** RSA-specific
> format.
>
> - ❌ **A** is wrong — PKCS#1 RSA-specific
>   private keys use the header
>   `-----BEGIN RSA PRIVATE KEY-----`.
>   The generic `PRIVATE KEY` header
>   specifically indicates PKCS#8.
> - ❌ **C** is wrong — PKCS#12 is a binary
>   format (.pfx/.p12) — it does not use PEM
>   headers. It contains both the certificate
>   and private key in an encrypted binary
>   container.
> - ❌ **D** is wrong — PKCS#10 (Certificate
>   Signing Request) uses the header
>   `-----BEGIN CERTIFICATE REQUEST-----`.
>   It contains the public key and identity —
>   not the private key.

---

**Q25. Answer: C**

> **C** is correct. The **sub (subject)** claim
> in an OpenID Connect ID Token is the unique
> identifier for the user at the Identity
> Provider — a stable, persistent identifier
> that the relying party (application) uses to
> recognize the user across sessions. The sub
> claim is mandatory in all OIDC ID Tokens.
>
> - ❌ **A** is wrong — **iss (issuer)** identifies
>   the Identity Provider that issued the token
>   (e.g., `https://accounts.google.com`) —
>   not the individual user.
> - ❌ **B** is wrong — **aud (audience)**
>   identifies the intended recipient of the
>   token — the client application's client_id —
>   not the user.
> - ❌ **D** is wrong — **exp (expiry)** is
>   a timestamp indicating when the token
>   expires — not a user identifier.

---

**Q26. Answer: B**

> **B** is correct. **CTAP2 (Client to
> Authenticator Protocol 2)** is the FIDO
> Alliance standard defining how the
> **browser/OS platform communicates with the
> authenticator** — the hardware key, platform
> authenticator (Windows Hello, Face ID),
> or phone. It specifies the commands, data
> formats, and transport mechanisms (USB HID,
> NFC, Bluetooth LE) used for authentication
> operations. WebAuthn handles the browser-to-
> server API; CTAP2 handles the browser-to-
> authenticator communication.
>
> - ❌ **A** is wrong — CTAP2 does not define
>   credential storage in password managers.
>   FIDO2 credentials are stored in the
>   authenticator itself (hardware key) or in
>   the platform's secure storage (TPM/Secure
>   Enclave) — not in password managers.
> - ❌ **C** is wrong — The assertion response
>   format sent to the server is defined by
>   WebAuthn — not CTAP2. CTAP2 is between
>   the platform and the authenticator.
> - ❌ **D** is wrong — FIDO2 attestation uses
>   standard X.509 certificates (or CBOR-encoded
>   attestation objects) defined by FIDO specs —
>   CTAP2 is the communication protocol, not the
>   certificate format standard.

---

**Q27. Answer: C**

> **C** is correct. In S/MIME, when the
> email is digitally signed with a **detached
> signature** (the email body remains readable
> even without S/MIME support), the signature
> is attached as a MIME attachment with the
> extension **.p7s** — a PKCS#7 SignedData
> structure containing only the signature
> (not the message body). Recipients with S/MIME
> support can verify the signature; others
> see the email body plus an attachment.
>
> - ❌ **A** is wrong — **.p12** (or .pfx) is
>   a PKCS#12 file containing a certificate
>   AND private key — not an S/MIME signature.
> - ❌ **B** is wrong — **.p7b** is a PKCS#7
>   file containing a certificate chain (for
>   distributing CA certificates) — not a
>   detached email signature.
> - ❌ **D** is wrong — **.csr** is a Certificate
>   Signing Request (PKCS#10) — submitted to
>   a CA to request a certificate. Nothing to
>   do with S/MIME email signatures.

---

**Q28. Answer: B**

> **B** is correct. Section 66C of the IT Act
> 2000 (added by the 2008 Amendment) covers
> identity theft using electronic means
> (fraudulently using another person's electronic
> signature, password, or unique identification
> feature). The punishment is:
> Up to **3 years imprisonment AND fine up to
> ₹1 lakh** — note it is AND (both penalties
> apply) — not OR (either/or).
>
> - ❌ **A** is wrong — Section 66 (hacking)
>   uses OR — "imprisonment OR fine up to
>   ₹5 lakh." Section 66C uses AND — both
>   imprisonment AND fine.
> - ❌ **C** is wrong — 5 years and ₹5 lakh is
>   not the Section 66C penalty. Cyber terrorism
>   (Section 66F) carries up to life imprisonment
>   — far more severe than 66C.
> - ❌ **D** is wrong — 10 years without fine
>   option describes Section 70 (unauthorized
>   access to protected government systems) —
>   not identity theft.

---

**Q29. Answer: B**

> **B** is correct. In ECC key generation,
> the public key P is computed by **scalar
> multiplication** of the generator point G
> by the private scalar k:
> `P = k × G`
> This means G is added to itself k times
> using elliptic curve point addition rules.
> The security (ECDLP) relies on the fact that
> given G and P, finding k is computationally
> infeasible for properly chosen curves.
>
> - ❌ **A** is wrong — P = k + G (point
>   addition of the scalar to the point) is
>   not how ECC public key derivation works.
>   Scalar multiplication (repeated addition)
>   is the operation, not adding k and G once.
> - ❌ **C** is wrong — hashing private key
>   material with G is not the ECC public key
>   derivation formula. This would not provide
>   the algebraic properties required for
>   ECDH or ECDSA.
> - ❌ **D** is wrong — P = G^k mod p is the
>   **Diffie-Hellman** formula (discrete log
>   over integers), not the ECC formula.
>   ECC uses elliptic curve point multiplication
>   — not modular exponentiation.

---

**Q30. Answer: B**

> **B** is correct. Kerberos tickets contain
> **timestamps** that define their validity
> window. When a client presents a ticket,
> the server checks that the timestamp is
> within the acceptable window (default: ±5
> minutes). If clocks are out of sync beyond
> this window, valid tickets appear expired
> (causing authentication failures) OR an
> attacker could replay a captured ticket that
> appears "fresh" to an out-of-sync server.
> NTP synchronization enforces this security
> requirement.
>
> - ❌ **A** is wrong — AES key generation
>   in Kerberos uses Kerberos-specific key
>   derivation, not time-seeded random generation.
>   Clock sync is not required for AES key
>   consistency.
> - ❌ **C** is wrong — DNS resolution for
>   Kerberos realms does not require NTP.
>   DNS and NTP are separate services; Kerberos
>   DNS lookups work regardless of clock accuracy.
> - ❌ **D** is wrong — KDC load balancing is
>   not based on client time. Load balancing
>   uses network metrics — not timestamp
>   comparison.

---

**Q31. Answer: D**

> **D** is correct. `TLS_ECDHE_RSA_WITH_
> AES_128_GCM_SHA256` is a **TLS 1.2** cipher
> suite format — it includes the key exchange
> algorithm (ECDHE), authentication algorithm
> (RSA), and uses the `_WITH_` separator.
> TLS 1.3 cipher suite names do NOT include
> key exchange or authentication algorithms
> (always ECDHE in TLS 1.3) and do not use
> `_WITH_`. The 5 valid TLS 1.3 suites are:
> TLS_AES_128_GCM_SHA256,
> TLS_AES_256_GCM_SHA384,
> TLS_CHACHA20_POLY1305_SHA256,
> TLS_AES_128_CCM_SHA256,
> TLS_AES_128_CCM_8_SHA256.
>
> - ❌ **A, B, C** are all valid TLS 1.3 cipher
>   suites — they follow the TLS 1.3 naming
>   format with no key exchange algorithm
>   specified in the name.

---

**Q32. Answer: B**

> **B** is correct. **NTDS.dit** (NT Directory
> Services) is the Active Directory database
> file stored on every Domain Controller.
> It contains all directory objects, attributes,
> user accounts, computer accounts, group
> memberships, and password hashes. It is
> located in `%SystemRoot%\NTDS\NTDS.dit`.
> Protecting NTDS.dit is critical — if an
> attacker obtains it, they can extract all
> domain password hashes offline.
>
> - ❌ **A** is wrong — SYSVOL is a shared
>   folder on Domain Controllers that stores
>   Group Policy templates and logon scripts —
>   not the AD database file.
> - ❌ **C** is wrong — "AD-Store.mdb" is a
>   fabricated filename. Active Directory uses
>   NTDS.dit, not an .mdb file format.
> - ❌ **D** is wrong — schema.ldf is a
>   Lightweight Directory Interchange Format
>   file used to import schema definitions;
>   it is not the active AD database.

---

**Q33. Answer: C**

> **C** is correct. The **Merkle Root** is
> the root hash of the Merkle tree built from
> all transactions in the block. Each transaction
> is hashed, pairs of hashes are hashed together,
> and this continues up the tree until a single
> root hash remains — the Merkle Root. It is
> stored in the block header and allows efficient
> verification of any transaction: a Merkle proof
> requires only O(log n) hashes, not the full
> transaction list.
>
> - ❌ **A** is wrong — concatenating all
>   transaction IDs would produce a very large,
>   variable-length value — not a compact root
>   hash. The Merkle tree specifically produces
>   a fixed 32-byte root regardless of how many
>   transactions are in the block.
> - ❌ **B** is wrong — the hash of only the
>   last transaction would not represent all
>   transactions. The Merkle Root covers ALL
>   transactions through the tree structure.
> - ❌ **D** is wrong — miners do not sign
>   blocks with digital signatures. In PoW,
>   the proof of work (finding the right nonce)
>   IS the miner's "contribution" — there is
>   no separate digital signature field.

---

**Q34. Answer: B**

> **B** is correct. TACACS+ uses **TCP** (port
> 49) — more reliable than UDP. Its key security
> advantage over RADIUS: TACACS+ **encrypts
> the ENTIRE packet payload** (authentication,
> authorization, and accounting data). RADIUS
> uses **UDP** and only encrypts the password
> field in authentication packets — all other
> attributes (username, accounting data) are
> sent in cleartext. This makes TACACS+ more
> suitable for sensitive network device
> management.
>
> - ❌ **A** is wrong — this inverts the
>   description: RADIUS uses UDP with
>   password-only encryption. TACACS+ uses
>   TCP with full payload encryption.
> - ❌ **C** is wrong — TACACS+ does not use
>   TLS or mutual certificate authentication.
>   It uses a shared secret for its proprietary
>   encryption of the packet payload.
> - ❌ **D** is wrong — SCTP (Stream Control
>   Transmission Protocol) is not used by
>   TACACS+. It is used by Diameter (RADIUS
>   successor for mobile networks) — not
>   TACACS+.

---

**Q35. Answer: C**

> **C** is correct. The three core Zero Trust
> principles per NIST SP 800-207 are:
> (1) **Verify Explicitly** — authenticate and
> authorize based on all available data points.
> (2) **Use Least Privilege Access** — JIT, JEA.
> (3) **Assume Breach** — microsegment, encrypt,
> monitor as if attackers are already inside.
> **Assume Breach** directly states that the
> architecture should be designed assuming the
> network has already been compromised.
>
> - ❌ **A** is wrong — Zero Trust explicitly
>   REJECTS the idea of trusting internal users.
>   "Never trust, always verify" applies to
>   EVERYONE — inside and outside the perimeter.
> - ❌ **B** is wrong — AES-256 encryption is
>   a security best practice but it is not one
>   of the three named ZTA principles in NIST
>   SP 800-207.
> - ❌ **D** is wrong — perimeter firewalls as
>   primary defense is the OLD perimeter model
>   that Zero Trust replaces. Zero Trust moves
>   away from relying on the perimeter.

---

**Q36. Answer: B**

> **B** is correct. **SNI** is included in the
> TLS **ClientHello** message — which is sent
> **before** the TLS encryption is established.
> The ClientHello is in plaintext, meaning any
> network observer (ISP, on the same Wi-Fi,
> government) can see WHICH domain you are
> connecting to — even though the actual HTTP
> content is encrypted by TLS. This is a
> significant privacy concern addressed by
> ECH (Encrypted Client Hello) in newer TLS
> implementations.
>
> - ❌ **A** is wrong — SNI never exposes the
>   server's private key. Private keys never
>   leave the server and are not part of any
>   TLS message. This describes a completely
>   different (and catastrophic) security failure.
> - ❌ **C** is wrong — SNI contains a hostname,
>   not the user's IP address. The server uses
>   SNI to select the correct certificate —
>   it already knows the client's IP from the
>   TCP connection.
> - ❌ **D** is wrong — SNI does not bypass
>   certificate validation. Certificate
>   verification happens after the server
>   sends the (SNI-selected) certificate —
>   SNI only tells the server which cert to send.

---

**Q37. Answer: C**

> **C** is correct. According to NIST SP 800-57
> key size equivalence table:
> **256-bit ECC ≈ 3072-bit RSA ≈ AES-128**
> (all provide approximately 128-bit security level).
> This is one of the most important key size
> equivalences to memorize — ECC provides
> equivalent security to RSA with dramatically
> shorter keys (256-bit vs 3072-bit).
>
> - ❌ **A** is wrong — 128-bit ECC is
>   deprecated; it provides only about 64-bit
>   security — far below the 128-bit security
>   level provided by RSA-3072.
> - ❌ **B** is wrong — 192-bit ECC provides
>   approximately 96-bit security — equivalent
>   to RSA-1536, not RSA-3072.
> - ❌ **D** is wrong — 384-bit ECC provides
>   approximately 192-bit security — equivalent
>   to RSA-7680 (AES-192 level). This EXCEEDS
>   RSA-3072 equivalence.

---

**Q38. Answer: B**

> **B** is correct. The **nonce** (number used
> once) in the block header is the variable
> that miners increment to find a valid block
> hash. Miners try different nonce values until:
> `SHA256(SHA256(block_header_with_nonce)) <
> difficulty_target`
> The difficulty target requires the hash to
> start with a specific number of zero bits.
> On average, quadrillions of nonce attempts
> are required — this is the computational
> "work" in Proof of Work.
>
> - ❌ **A** is wrong — the nonce does not
>   identify the miner. Miner identity/reward
>   address is in the coinbase transaction
>   in the block body, not in the header nonce.
> - ❌ **C** is wrong — transaction count is
>   tracked via the transaction list in the
>   block body and the Merkle Root. The nonce
>   has nothing to do with preventing duplicate
>   blocks.
> - ❌ **D** is wrong — the previous block's
>   hash is computed from that block's complete
>   data — not from a random seed. The nonce
>   is for current block validation, not for
>   generating the previous block's hash.

---

**Q39. Answer: C**

> **C** is correct. The HSTS **preload**
> directive requests that the domain be included
> in **browser preload lists** (maintained by
> Google, Mozilla, Apple, Microsoft at
> hstspreload.org). Domains on the preload list
> are treated as HTTPS-only from the very
> **first ever visit** — even before the browser
> has ever seen the HSTS header from that server.
> This eliminates the "first visit" vulnerability
> where an SSL stripping attack could intercept
> the initial HTTP connection before the HSTS
> header is received.
>
> - ❌ **A** is wrong — "pre-loading certificates"
>   at server startup describes TLS session
>   ticket caching or certificate pre-loading
>   in memory — not HSTS preload. These are
>   completely different mechanisms.
> - ❌ **B** is wrong — blocking HTTP scripts
>   describes Content Security Policy (CSP) with
>   the `upgrade-insecure-requests` or
>   `block-all-mixed-content` directive — not
>   HSTS preload.
> - ❌ **D** is wrong — CAs submit certificates
>   to CT logs — not through HSTS preload.
>   CT log pre-submission is a separate process
>   in the certificate issuance workflow.

---

**Q40. Answer: B**

> **B** is correct. In FIPS 140-2 Level 3,
> **zeroization** is the automatic overwriting
> of all **Critical Security Parameters (CSPs)**
> — including encryption keys, private keys,
> passwords, and PINs — with zeros or random
> data when **physical tampering is detected**.
> This ensures that even if an attacker
> physically breaks open the HSM, all key
> material is destroyed before it can be
> extracted. The physical tamper detection
> mechanism (voltage sensors, temperature
> sensors, mesh wires) triggers this automatic
> zeroization.
>
> - ❌ **A** is wrong — power-on initialization
>   is not zeroization in the FIPS security
>   sense. Zeroization is specifically a
>   SECURITY RESPONSE to detected threats —
>   not a startup procedure.
> - ❌ **C** is wrong — certificate databases
>   are not CSPs; they contain public
>   certificates which are public data.
>   Zeroization targets private keys and
>   secret values — not public certificate
>   stores.
> - ❌ **D** is wrong — post-operation session
>   key clearing is good practice but not what
>   FIPS 140-2 specifically defines as zeroization.
>   The defined trigger is physical tamper
>   detection — not routine key lifecycle
>   management.

---

&nbsp;

&nbsp;

&nbsp;

---

## PART 3 — QUICK ANSWER KEY

| Q | A | Q | A | Q | A | Q | A |
|---|---|---|---|---|---|---|---|
| 1 | D | 11 | D | 21 | C | 31 | D |
| 2 | B | 12 | B | 22 | B | 32 | B |
| 3 | C | 13 | B | 23 | C | 33 | C |
| 4 | B | 14 | B | 24 | B | 34 | B |
| 5 | B | 15 | C | 25 | C | 35 | C |
| 6 | C | 16 | B | 26 | B | 36 | B |
| 7 | B | 17 | B | 27 | C | 37 | C |
| 8 | B | 18 | D | 28 | B | 38 | B |
| 9 | C | 19 | C | 29 | B | 39 | C |
| 10 | B | 20 | B | 30 | B | 40 | B |

---

## PART 4 — SESSION COVERAGE MAP

| Session | Topic | Questions |
|---------|-------|-----------|
| 01 | Information Security, Attacks & Threats | Q1, Q15 |
| 02 | Encryption Concepts, File Encryption | Q2, Q3 |
| 03 | Cryptographic Fundamentals, Ciphers | Q6, Q17 |
| 04 | Symmetric & Asymmetric Algorithms | Q4, Q16, Q18, Q29 |
| 05 | Diffie-Hellman, Attacks, Crypto Issues | Q5, Q19 |
| 06 | Hashing: SHA & HMAC | Q20 |
| 07 | PKI Fundamentals, Digital Signatures | Q7, Q13 |
| 08 | CA, Trust Models, Revocation, Cert Types | Q8, Q21, Q22 |
| 09 | Aadhaar, e-Sign, Timestamping | Q9, Q14, Q23 |
| 10 | PKCS & FIPS 140-2 | Q10, Q24, Q40 |
| 11 | Authentication, MFA, SSO, OAuth, OpenID | Q11, Q25 |
| 12 | Authentication Protocols, FIDO, Zero Trust | Q12, Q26, Q34, Q35 |
| 13 | SSL, TLS, PGP, S/MIME | Q27, Q31, Q36, Q37, Q39 |
| 14 | IT Act, LDAP, Active Directory, Blockchain | Q28, Q30, Q32, Q33, Q38 |

---

## PART 5 — SCORE INTERPRETATION

| Score | Meaning |
|-------|---------|
| **38–40** | ✅ Excellent — Exam ready. Strong foundation across all sessions. |
| **34–37** | ✅ Good — Review the sessions where you lost marks. |
| **28–33** | ⚠️ Fair — Revisit session notes for weak areas before the next set. |
| **Below 28** | ❌ Re-read session notes before attempting Set 03. |

---

### Difficulty Distribution Used in This Set

| Level | % | MCQs | Questions |
|-------|---|------|-----------|
| Foundation | 40% | 16 | Q1,Q4,Q6,Q7,Q10,Q12,Q14,Q16,Q20,Q23,Q24,Q28,Q32,Q33,Q35,Q40 |
| Fundamental | 40% | 16 | Q2,Q3,Q5,Q8,Q9,Q11,Q13,Q17,Q18,Q19,Q22,Q25,Q29,Q30,Q38,Q39 |
| Basic Concepts | 20% | 8 | Q15,Q21,Q26,Q27,Q31,Q34,Q36,Q37 |

---
