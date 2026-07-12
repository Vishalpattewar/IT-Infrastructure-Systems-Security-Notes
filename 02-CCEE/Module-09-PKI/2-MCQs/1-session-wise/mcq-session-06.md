# MCQ Session 06 — Secure Hashing Methods: SHA & HMAC

## 📑 Table of Contents
- [Instructions](#instructions)
- [MCQs 1–6 — Hash Function Fundamentals](#mcqs-16--hash-function-fundamentals)
- [MCQs 7–13 — SHA Family](#mcqs-713--sha-family)
- [MCQs 14–19 — HMAC](#mcqs-1419--hmac)
- [MCQs 20–25 — Extra Notes: Attacks, Constructions,
  Standards](#mcqs-2025--extra-notes-attacks-constructions-standards)
- [Answer Key](#-answer-key--quick-reference)
- [Topic Coverage Map](#-topic-coverage-map)

---

## Instructions

- 25 MCQs — drawn from core syllabus AND
  📌 Extra Notes of Session 06
- Foundation + Fundamental + Basic Concepts ONLY
- 4 options per question
- ✅ marks the correct answer
- Full explanation after every question including
  why each wrong option is wrong
- Wrong options look reasonable to someone unprepared
- Correct answer is clear to someone with solid basics

---

## MCQs 1–6 — Hash Function Fundamentals

---

**Q1. What is the PRIMARY security goal of a
cryptographic hash function?**

- A) Confidentiality — hiding data from unauthorized
     parties
- B) Integrity — verifying that data has not been
     altered ✅
- C) Authentication — confirming the identity of
     the sender
- D) Non-repudiation — preventing the sender from
     denying a message

> **Explanation:**
> - ✅ **B — Integrity:** Hash functions verify that
>   data has not been modified. Given a hash of a
>   file, anyone can recompute the hash and compare
>   — if they match, the data is unchanged. This is
>   integrity verification.
> - ❌ **A:** Hash functions do NOT hide data —
>   they do not encrypt anything. The original input
>   can be seen by anyone. Confidentiality is
>   provided by encryption, not hashing.
> - ❌ **C:** A plain hash provides no authentication
>   — anyone can compute a hash of any message
>   without any key or identity. Authentication
>   requires a key (HMAC) or private key (digital
>   signature).
> - ❌ **D:** Non-repudiation requires a private key
>   that only one party holds — digital signatures
>   provide this. A keyless hash function proves
>   nothing about who created it.

---

**Q2. Which of the following correctly describes
a cryptographic hash function?**

- A) Takes a fixed-length input and produces a
     variable-length output
- B) Takes an input of any length and produces a
     fixed-length output ✅
- C) Takes two inputs — data and a key — and
     produces a fixed-length output
- D) Takes a fixed-length input and produces an
     output of the same length

> **Explanation:**
> - ✅ **B:** A hash function accepts input of ANY
>   size — a single byte or a 10TB file — and always
>   produces the SAME fixed-length output for a given
>   hash algorithm. SHA-256 always outputs exactly
>   256 bits regardless of input size.
> - ❌ **A:** This is backwards — input is variable
>   (any length), output is fixed. Not the other
>   way around.
> - ❌ **C:** A plain hash function takes only the
>   data as input — no key. A function that takes
>   both data and a key is an HMAC or MAC, not a
>   plain hash function.
> - ❌ **D:** Output matching input length describes
>   a block cipher in certain configurations — not
>   a hash function. Hash functions compress variable
>   input to fixed output.

---

**Q3. A cryptographic hash function must be
one-way. What does this mean?**

- A) The hash function can only be applied once
     to any given input
- B) Given a hash output, it is computationally
     infeasible to find the original input ✅
- C) The hash function only processes data in
     one direction — left to right
- D) The same input always produces a different
     output each time the hash is applied

> **Explanation:**
> - ✅ **B — Pre-image resistance (One-Way):** A
>   one-way function means: given H = Hash(M), it is
>   computationally infeasible to find M. You can
>   easily compute H from M, but you cannot reverse
>   the process to recover M from H. This is also
>   called pre-image resistance.
> - ❌ **A:** "Applied only once" has no meaning in
>   cryptography — a hash function can be applied to
>   any input any number of times. The same input
>   always produces the same output (deterministic).
> - ❌ **C:** "Left to right" is a physical description
>   with no cryptographic meaning. One-way refers to
>   computational irreversibility — not direction of
>   data processing.
> - ❌ **D:** Producing different output each time
>   would describe a randomized function — but hash
>   functions are DETERMINISTIC — the same input
>   ALWAYS produces the same output. This is
>   required for verification to work.

---

**Q4. What property of hash functions ensures that
a tiny change in the input produces a completely
different output?**

- A) Pre-image Resistance
- B) Collision Resistance
- C) Avalanche Effect ✅
- D) Second Pre-image Resistance

> **Explanation:**
> - ✅ **C — Avalanche Effect:** The Avalanche Effect
>   means a single bit change in the input causes
>   approximately 50% of the output bits to change
>   unpredictably. Changing "Hello" to "hello" in
>   SHA-256 produces a completely different hash
>   with no visible relationship to the original.
>   This ensures small changes cannot be hidden.
> - ❌ **A:** Pre-image resistance means you cannot
>   find the input from the output — it does not
>   describe how output changes with input changes.
> - ❌ **B:** Collision resistance means it is hard
>   to find two different inputs with the same hash
>   — it does not describe the relationship between
>   small input changes and output changes.
> - ❌ **D:** Second pre-image resistance means given
>   a message, you cannot find another message with
>   the same hash — again, not about how the output
>   changes with small input modifications.

---

**Q5. Which of the following is the CORRECT
relationship between hash functions and encryption?**

- A) Hashing and encryption are the same —
     both hide data from unauthorized parties
- B) Hashing is a form of encryption that uses
     a public key instead of a private key
- C) Hashing is one-way and requires no key —
     encryption is reversible and requires a key ✅
- D) Encryption is a type of hashing that can
     be reversed with the correct algorithm

> **Explanation:**
> - ✅ **C:** The fundamental distinction:
>   Hashing = one-way, no key, fixed output,
>   used for integrity.
>   Encryption = reversible (with key), key required,
>   output similar size to input, used for
>   confidentiality. They serve completely different
>   purposes and work differently.
> - ❌ **A:** Hashing does NOT hide data from
>   unauthorized parties — the original data is
>   still visible. Hashing only creates a
>   fingerprint for integrity checking.
> - ❌ **B:** Hash functions use no key at all —
>   not public, not private. A function that uses
>   a public key would be asymmetric encryption or
>   a digital signature scheme.
> - ❌ **D:** This completely inverts the definitions.
>   Encryption is not a type of hashing — they are
>   separate categories. Hashing is one-way;
>   encryption is two-way (reversible with key).

---

**Q6. An attacker finds two different documents
that produce exactly the same SHA-256 hash value.
Which hash property has been broken?**

- A) Pre-image Resistance
- B) Avalanche Effect
- C) Second Pre-image Resistance
- D) Collision Resistance ✅

> **Explanation:**
> - ✅ **D — Collision Resistance:** A collision is
>   when two different inputs M₁ ≠ M₂ produce the
>   same hash output: Hash(M₁) = Hash(M₂). Finding
>   ANY such pair breaks collision resistance —
>   the attacker did not start with a specific
>   message, they just found any two matching inputs.
> - ❌ **A:** Pre-image resistance is broken when an
>   attacker finds the INPUT given only the HASH
>   OUTPUT — that is not what happened here. The
>   attacker found two inputs with the same output.
> - ❌ **B:** Avalanche Effect describes how output
>   changes with input changes — it is not a security
>   property that can be "broken" in the same sense.
> - ❌ **C:** Second pre-image resistance is broken
>   when given a SPECIFIC M₁, an attacker finds M₂
>   with the same hash. Here no specific starting
>   document was required — they found ANY collision.
>   That is collision resistance, not second
>   pre-image resistance.

---

## MCQs 7–13 — SHA Family

---

**Q7. Which organization designed the SHA family
of hash functions and under which standard body
were they published?**

- A) Designed by RSA Security — published by IEEE
- B) Designed by NSA — published by NIST as FIPS
     standards ✅
- C) Designed by NIST — published by ISO/IEC
- D) Designed by IBM — published by ANSI

> **Explanation:**
> - ✅ **B:** The SHA family was designed by the
>   **NSA (National Security Agency)** and published
>   by **NIST (National Institute of Standards and
>   Technology)** as part of the Federal Information
>   Processing Standard (FIPS) series.
> - ❌ **A:** RSA Security designed the MD series
>   (Ron Rivest), not SHA. IEEE is an engineering
>   standards body — it does not publish FIPS.
> - ❌ **C:** NIST published the standards but did
>   not design the algorithms — NSA did the design.
>   ISO/IEC is an international standards body —
>   FIPS are US government standards, not ISO.
> - ❌ **D:** IBM designed DES and contributed to
>   AES (MARS was an IBM submission) — not SHA.
>   ANSI is a US standards body but not the
>   publisher of FIPS.

---

**Q8. What is the output size of SHA-256 in bits
and in hexadecimal characters?**

- A) 128 bits — 32 hex characters
- B) 160 bits — 40 hex characters
- C) 256 bits — 64 hex characters ✅
- D) 512 bits — 128 hex characters

> **Explanation:**
> - ✅ **C — 256 bits / 64 hex characters:**
>   SHA-256 always produces a 256-bit output.
>   Since each hexadecimal character represents
>   4 bits: 256 ÷ 4 = 64 hex characters.
>   Example: a3f7c1d8...
>   (64 characters long).
> - ❌ **A — 128 bits / 32 hex chars:** This is
>   the output size of **MD5** — not SHA-256.
>   Common trap because MD5 is 128-bit and
>   SHA-256 is 256-bit.
> - ❌ **B — 160 bits / 40 hex chars:** This is
>   the output size of **SHA-1** — not SHA-256.
>   SHA-1's 160-bit output was larger than MD5
>   but smaller than SHA-256.
> - ❌ **D — 512 bits / 128 hex chars:** This is
>   the output size of **SHA-512** — not SHA-256.
>   Both are part of the SHA-2 family but with
>   different output sizes.

---

**Q9. SHA-1 was declared broken after the
SHAttered attack in 2017. What did that attack
demonstrate?**

- A) SHA-1 private keys could be recovered
     from its output values
- B) Two different files could be created with
     identical SHA-1 hash values ✅
- C) SHA-1 passwords could be reversed to
     their original plaintext
- D) SHA-1 encrypted data could be decrypted
     without the key

> **Explanation:**
> - ✅ **B — Collision found:** The SHAttered attack
>   (Google + CWI Amsterdam, 2017) produced the
>   first practical SHA-1 **collision** — two
>   different PDF files that had exactly the same
>   SHA-1 hash value. This demonstrated that
>   SHA-1's collision resistance was broken in
>   practice, not just theory.
> - ❌ **A:** SHA-1 has no private keys — it is a
>   hash function, not an asymmetric algorithm.
>   "Recovering private keys from hash output" is
>   not a relevant concept for hash functions.
> - ❌ **C:** SHA-1 is a one-way hash function —
>   reversing it to recover plaintext is
>   computationally infeasible (pre-image resistance
>   remains intact even for broken SHA-1).
>   SHAttered found a collision, not a reversal.
> - ❌ **D:** SHA-1 does not encrypt data — it hashes
>   it. "Decrypting without a key" has no meaning
>   for a hash function. Encryption and hashing are
>   fundamentally different operations.

---

**Q10. Under which NIST FIPS standard is
SHA-256 defined?**

- A) FIPS 140-2
- B) FIPS 198-1
- C) FIPS 202
- D) FIPS 180-4 ✅

> **Explanation:**
> - ✅ **D — FIPS 180-4:** The SHA-2 family including
>   SHA-256 is defined in **FIPS 180-4** — the
>   current version of the Secure Hash Standard.
>   It covers SHA-1 and the entire SHA-2 family
>   (SHA-224, SHA-256, SHA-384, SHA-512 and variants).
> - ❌ **A — FIPS 140-2:** This is the standard for
>   security requirements of cryptographic modules
>   (hardware and software) — not hash algorithms.
>   FIPS 140-2 is about module security levels
>   (1–4), not about defining specific algorithms.
> - ❌ **B — FIPS 198-1:** This is the **HMAC
>   standard** — defines the HMAC construction for
>   message authentication codes. Not the SHA-256
>   definition.
> - ❌ **C — FIPS 202:** This defines **SHA-3 and
>   SHAKE** — the Keccak-based hash functions.
>   SHA-256 is SHA-2 family — defined in FIPS 180-4,
>   not FIPS 202.

---

**Q11. SHA-3 was selected as a standard in 2015.
Which algorithm did NIST select as the winner of
the SHA-3 competition?**

- A) Serpent
- B) Twofish
- C) Keccak ✅
- D) BLAKE

> **Explanation:**
> - ✅ **C — Keccak:** NIST selected **Keccak**
>   (designed by Guido Bertoni, Joan Daemen, Michaël
>   Peeters, and Gilles Van Assche) as the winner of
>   the SHA-3 competition in 2012, standardized as
>   FIPS 202 in 2015. Keccak uses a Sponge
>   construction — fundamentally different from the
>   Merkle-Damgård construction used by SHA-2.
> - ❌ **A — Serpent:** Serpent was a finalist in the
>   **AES competition** (1997–2001), not the SHA-3
>   competition. Confusing AES finalists with SHA-3
>   finalists is a common trap.
> - ❌ **B — Twofish:** Twofish was also an **AES
>   finalist** — not a SHA-3 finalist. The SHA-3
>   finalists were Keccak, BLAKE, Grøstl, JH, and
>   Skein.
> - ❌ **D — BLAKE:** BLAKE was a SHA-3 finalist
>   (strong second) — but it did not win. BLAKE2
>   and BLAKE3 are widely used modern hash functions
>   but they are NOT SHA-3. Keccak won the
>   competition.

---

**Q12. What is the key structural difference between
SHA-2 and SHA-3 that makes SHA-3 resistant to
length extension attacks?**

- A) SHA-3 uses a larger output size than SHA-2
- B) SHA-3 uses a Sponge construction while SHA-2
     uses Merkle-Damgård construction ✅
- C) SHA-3 processes blocks in parallel while
     SHA-2 processes them sequentially
- D) SHA-3 uses a secret key in its construction
     while SHA-2 does not

> **Explanation:**
> - ✅ **B — Sponge vs Merkle-Damgård:** SHA-2 is
>   built on the Merkle-Damgård construction where
>   the final hash state IS the output — this
>   enables length extension attacks. SHA-3 uses
>   the Sponge construction where internal capacity
>   bits are never directly output — preventing
>   length extension attacks entirely.
> - ❌ **A:** Output size is not what determines
>   length extension vulnerability — SHA-512 (512-bit
>   output, Merkle-Damgård) is still vulnerable to
>   length extension attacks. The construction type
>   is what matters, not output size.
> - ❌ **C:** Both SHA-2 and SHA-3 process data
>   blocks sequentially in their core operation.
>   Parallel processing is not the distinguishing
>   structural feature between them.
> - ❌ **D:** Neither SHA-2 nor SHA-3 uses a secret
>   key — they are both keyless hash functions.
>   Adding a key is the job of HMAC, not the hash
>   function itself.

---

**Q13. MD5 was designed by which person, and what
is its output size?**

- A) Whitfield Diffie — 160-bit output
- B) Ron Rivest — 128-bit output ✅
- C) Joan Daemen — 256-bit output
- D) Bruce Schneier — 128-bit output

> **Explanation:**
> - ✅ **B — Ron Rivest / 128-bit:** MD5 (Message
>   Digest 5) was designed by **Ron Rivest** — the
>   same 'R' in RSA — and published in 1992 (RFC
>   1321). It produces a **128-bit output** (32 hex
>   characters). MD5 is broken for security use due
>   to practical collision attacks (2004).
> - ❌ **A:** Whitfield Diffie co-invented the
>   Diffie-Hellman key exchange — not MD5. SHA-1
>   produces 160-bit output, not MD5.
> - ❌ **C:** Joan Daemen co-designed AES (Rijndael)
>   and SHA-3 (Keccak) — not MD5. SHA-256 produces
>   256-bit output.
> - ❌ **D:** Bruce Schneier designed Blowfish,
>   Twofish, and Skein — not MD5. The output size
>   128-bit is correct for MD5, but the designer
>   attribution is wrong — Schneier designed
>   different algorithms.

---

## MCQs 14–19 — HMAC

---

**Q14. What problem does HMAC solve that a plain
hash function cannot?**

- A) HMAC produces a longer hash output than
     plain hash functions
- B) HMAC is faster than plain hashing for large
     files
- C) HMAC uses a shared secret key — allowing
     verification of both integrity AND the
     sender's identity ✅
- D) HMAC compresses data more efficiently than
     plain hash functions

> **Explanation:**
> - ✅ **C:** A plain hash has no key — anyone can
>   compute a valid hash for any message. An attacker
>   can modify a message and recompute the hash.
>   HMAC involves a shared secret key in the
>   computation — only parties who know the key can
>   produce or verify the MAC. This adds
>   authentication on top of integrity.
> - ❌ **A:** HMAC output size depends on the
>   underlying hash function — HMAC-SHA-256 produces
>   256 bits, same as plain SHA-256. HMAC does not
>   produce a longer output.
> - ❌ **B:** HMAC requires TWO hash computations
>   (inner + outer) — it is slightly slower than
>   plain hashing, not faster.
> - ❌ **D:** HMAC is not a compression algorithm —
>   it does not compress data. It computes a message
>   authentication code for integrity and
>   authentication purposes.

---

**Q15. HMAC was published in which RFC, and it
is also standardized under which NIST FIPS?**

- A) RFC 1321 — FIPS 180-4
- B) RFC 2104 — FIPS 198-1 ✅
- C) RFC 4880 — FIPS 202
- D) RFC 7468 — FIPS 140-2

> **Explanation:**
> - ✅ **B — RFC 2104 / FIPS 198-1:** HMAC was
>   published by Bellare, Canetti, and Krawczyk
>   in **RFC 2104 (1997)** and is also standardized
>   by NIST as **FIPS 198-1**. These are the two
>   authoritative references for the HMAC
>   construction.
> - ❌ **A:** RFC 1321 defines **MD5** (by Ron
>   Rivest, 1992) — not HMAC. FIPS 180-4 defines
>   the SHA-2 family — not HMAC.
> - ❌ **C:** RFC 4880 defines the **OpenPGP
>   message format** — not HMAC. FIPS 202 defines
>   SHA-3 and SHAKE — not HMAC.
> - ❌ **D:** RFC 7468 defines textual encodings of
>   PKIX, PKCS, and CMS structures (PEM format) —
>   not HMAC. FIPS 140-2 defines cryptographic
>   module security requirements — not HMAC.

---

**Q16. In the HMAC construction, what are the
values of the inner padding (ipad) and outer
padding (opad)?**

- A) ipad = 0xFF, opad = 0x00
- B) ipad = 0x5C, opad = 0x36
- C) ipad = 0x36, opad = 0x5C ✅
- D) ipad = 0xAA, opad = 0x55

> **Explanation:**
> - ✅ **C — ipad = 0x36, opad = 0x5C:** These are
>   the fixed constants defined in the HMAC
>   specification (RFC 2104). The key is XORed with
>   ipad (0x36 repeated to block size) for the inner
>   hash, and XORed with opad (0x5C repeated to
>   block size) for the outer hash.
>   Memory hook: **i**pad = 0x**3**6 (i comes
>   before o; 3 comes before 5)
> - ❌ **A:** 0xFF and 0x00 are not HMAC padding
>   constants — these values are not defined anywhere
>   in the HMAC specification.
> - ❌ **B:** This swaps ipad and opad — 0x5C is
>   the **outer** padding (opad) and 0x36 is the
>   **inner** padding (ipad). The swap is a direct
>   exam trap because both values are correct but
>   their assignment is reversed.
> - ❌ **D:** 0xAA and 0x55 are not HMAC constants —
>   these are commonly seen in memory testing and
>   alternating bit patterns but have no role in
>   HMAC.

---

**Q17. Which security property does HMAC provide
that a plain hash function does NOT?**

- A) One-way / Pre-image resistance
- B) Fixed output size
- C) Avalanche Effect
- D) Data Authentication — confirming the sender
     knows the shared key ✅

> **Explanation:**
> - ✅ **D — Authentication:** Both HMAC and plain
>   hash provide integrity (detecting changes).
>   HMAC additionally provides authentication —
>   because only someone who knows the shared secret
>   key can produce a valid HMAC. A plain hash
>   requires no key — anyone can compute it — so it
>   provides no authentication.
> - ❌ **A:** Pre-image resistance is a property of
>   the underlying hash function — both plain hash
>   and HMAC have this property (HMAC inherits it
>   from the hash function used). It is not something
>   HMAC adds over plain hashing.
> - ❌ **B:** Fixed output size is a property of
>   the underlying hash function — not something
>   HMAC specifically adds. HMAC-SHA-256 produces
>   256 bits, same as SHA-256.
> - ❌ **C:** The Avalanche Effect comes from the
>   underlying hash function — both plain SHA-256
>   and HMAC-SHA-256 exhibit the avalanche effect.
>   HMAC does not add this property.

---

**Q18. HMAC provides integrity and authentication.
Which security property does it NOT provide?**

- A) Integrity — detecting data modification
- B) Authentication — confirming sender knows the key
- C) Non-repudiation — proving only one specific
     party created the message ✅
- D) Detection of unauthorized modifications

> **Explanation:**
> - ✅ **C — Non-repudiation:** HMAC uses a
>   **shared secret key** — both the sender and
>   receiver know the same key. Either party could
>   have created the HMAC. If Alice and Bob share
>   an HMAC key, Alice cannot prove to a third party
>   that Bob sent a specific message (Bob could
>   claim Alice created it). Non-repudiation requires
>   an asymmetric private key that only one party
>   holds — that is what digital signatures provide.
> - ❌ **A:** HMAC absolutely provides integrity —
>   any modification to the data will produce a
>   different HMAC value that does not match. This
>   is one of HMAC's core properties.
> - ❌ **B:** HMAC provides authentication — only
>   a party with the correct shared key can produce
>   a valid HMAC. This confirms the sender knows
>   the key.
> - ❌ **D:** Detection of unauthorized modifications
>   is the same as integrity — HMAC provides this.
>   Any tampering with the message or the MAC itself
>   will be detected during verification.

---

**Q19. Which of the following protocols uses
HMAC-SHA-256 for record integrity verification?**

- A) SSL 3.0
- B) TLS 1.2 ✅
- C) HTTP/1.1
- D) DNS

> **Explanation:**
> - ✅ **B — TLS 1.2:** TLS 1.2 uses HMAC-SHA-256
>   (or HMAC-SHA-384 depending on the cipher suite)
>   to provide MAC protection for each TLS record —
>   ensuring integrity of data in transit. This is
>   the MAC in the "MAC-then-Encrypt" or
>   "Encrypt-then-MAC" approach used by TLS 1.2.
> - ❌ **A:** SSL 3.0 uses a weaker and proprietary
>   MAC construction (not standard HMAC) — this
>   contributed to its vulnerability. SSL 3.0 is
>   deprecated and broken (POODLE attack).
> - ❌ **C:** HTTP/1.1 is a plain text protocol —
>   it has no built-in cryptographic integrity
>   mechanism. Security in HTTP is provided by TLS
>   (HTTPS), not by HTTP itself.
> - ❌ **D:** Standard DNS has no cryptographic
>   integrity protection — it is unencrypted and
>   unauthenticated by default. DNSSEC adds digital
>   signatures for integrity, but this uses RSA/ECDSA
>   signatures, not HMAC.

---

## MCQs 20–25 — Extra Notes: Attacks,
Constructions, Standards

---

**Q20. What is a length extension attack and
which type of hash construction is vulnerable
to it?**

- A) An attack that finds collisions by extending
     the birthday paradox — SHA-3 is vulnerable
- B) An attack where an attacker appends data to
     a message and computes a valid MAC without
     knowing the key — affects Merkle-Damgård
     hash functions ✅
- C) An attack that increases key length to
     extend the security of a hash function —
     affects all hash functions equally
- D) An attack that extends the time needed to
     brute force a hash — affects SHA-2 only

> **Explanation:**
> - ✅ **B — Merkle-Damgård vulnerability:** A
>   length extension attack exploits the fact that
>   in Merkle-Damgård hash functions (MD5, SHA-1,
>   SHA-2), the final hash output IS the internal
>   state. An attacker who knows Hash(Key || Message)
>   can compute Hash(Key || Message || padding ||
>   extra_data) without knowing the key — by
>   resuming hashing from the known output state.
>   This breaks naive MAC schemes like
>   MAC = Hash(Key || Message).
> - ❌ **A:** The birthday paradox is used in
>   collision attacks — not length extension attacks.
>   SHA-3 is immune to length extension attacks
>   (Sponge construction) — not vulnerable.
> - ❌ **C:** "Extending key length" has nothing to
>   do with length extension attacks. The attack is
>   about extending the MESSAGE — not the key size.
> - ❌ **D:** Length extension attacks allow
>   forgery of MAC values — they do not affect
>   brute force time. They are about constructing
>   valid MACs without a key, not about cracking
>   hash outputs faster.

---

**Q21. Why is HMAC immune to length extension
attacks even though it uses SHA-256 — a
Merkle-Damgård hash function that is normally
vulnerable?**

- A) HMAC uses SHA-3 internally — which is immune
     to length extension by design
- B) HMAC uses two nested hash operations with
     different key-derived inputs — the outer hash
     prevents state extension ✅
- C) HMAC uses a random salt that changes the
     internal state between computations
- D) HMAC truncates the output — making the
     internal state inaccessible to attackers

> **Explanation:**
> - ✅ **B — Two nested hashes:** HMAC computes
>   an inner hash: Hash(Key XOR ipad || Message),
>   then feeds that result into an outer hash:
>   Hash(Key XOR opad || inner_hash). The outer
>   hash processes a completely different
>   key-derived input — an attacker who knows the
>   inner hash cannot extend it because the outer
>   hash wraps it with additional key material that
>   the attacker does not know.
> - ❌ **A:** HMAC-SHA-256 uses SHA-256 internally
>   — not SHA-3. HMAC was designed to be secure
>   with Merkle-Damgård hash functions specifically.
>   Using SHA-3 in HMAC would also work, but that
>   is not why HMAC-SHA-256 is immune.
> - ❌ **C:** HMAC does not use a random salt —
>   it uses a fixed key. The ipad and opad constants
>   are fixed values, not random. Salts are used in
>   password hashing, not in HMAC.
> - ❌ **D:** HMAC does not truncate output — it
>   produces the full output of the underlying hash
>   function (e.g., 256 bits for HMAC-SHA-256).
>   Truncation is a separate optional step, not a
>   security mechanism against length extension.

---

**Q22. The Merkle Tree is a data structure built
from hash functions. Which of the following
correctly describes how a Merkle Tree works?**

- A) A Merkle Tree stores encrypted copies of
     data in a hierarchical structure
- B) A Merkle Tree is a binary tree where leaf
     nodes contain data hashes and parent nodes
     contain hashes of their children ✅
- C) A Merkle Tree is a key derivation structure
     used to generate multiple encryption keys
     from a single root key
- D) A Merkle Tree is a password storage structure
     that organizes salted hashes hierarchically

> **Explanation:**
> - ✅ **B:** In a Merkle Tree, each leaf node
>   contains the hash of a data block. Each internal
>   (parent) node contains the hash of its two
>   children's hashes combined. The root of the
>   tree is a single hash value that represents
>   the integrity of ALL the data in the tree.
>   Used in Bitcoin, Git, and Certificate
>   Transparency.
> - ❌ **A:** Merkle Trees store hashes — not
>   encrypted copies of data. There is no encryption
>   involved. The structure is for integrity
>   verification, not confidentiality.
> - ❌ **C:** Key derivation from a root key
>   describes a key tree or HKDF-based key hierarchy
>   — not a Merkle Tree. Merkle Trees are for
>   data integrity, not key generation.
> - ❌ **D:** Password storage is unrelated to
>   Merkle Trees. Salted hashes are stored flat
>   in a database — not in a tree structure.

---

**Q23. Which NIST FIPS standard defines the
SHA-3 and SHAKE hash functions?**

- A) FIPS 180-4
- B) FIPS 198-1
- C) FIPS 202 ✅
- D) FIPS 140-2

> **Explanation:**
> - ✅ **C — FIPS 202:** SHA-3 (including SHA3-224,
>   SHA3-256, SHA3-384, SHA3-512) and the SHAKE
>   extendable output functions (SHAKE128, SHAKE256)
>   are all defined in **FIPS 202**, published by
>   NIST in 2015.
> - ❌ **A — FIPS 180-4:** This defines the
>   **SHA-2 family** (SHA-224, SHA-256, SHA-384,
>   SHA-512) and SHA-1. Not SHA-3. Easy to confuse
>   because both cover "SHA" algorithms but they
>   are different FIPS documents for different
>   algorithm families.
> - ❌ **B — FIPS 198-1:** This defines the
>   **HMAC construction** — nothing to do with
>   SHA-3 or hash algorithm definitions.
> - ❌ **D — FIPS 140-2:** This defines security
>   requirements for **cryptographic modules**
>   (hardware/software) — not specific hash
>   algorithms. FIPS 140-2 is about module
>   certification levels 1–4.

---

**Q24. A developer uses the construction
MAC = SHA-256(Key || Message) to authenticate
API requests. What is the security weakness
of this approach?**

- A) SHA-256 is too slow for API authentication —
     a faster hash like MD5 should be used instead
- B) This construction is vulnerable to length
     extension attacks — an attacker can forge
     MACs for extended messages without the key ✅
- C) The key must be placed after the message —
     SHA-256(Message || Key) is the secure form
- D) SHA-256 output is too long for API tokens —
     it should be truncated to 64 bits

> **Explanation:**
> - ✅ **B — Length extension attack:** SHA-256 uses
>   Merkle-Damgård construction — the output IS the
>   internal hash state. An attacker who knows
>   SHA-256(Key || Message) can compute
>   SHA-256(Key || Message || padding || evil_data)
>   without knowing the Key. This allows forging
>   valid MACs for extended messages. The correct
>   solution is to use HMAC-SHA-256 which prevents
>   this through its two-layer construction.
> - ❌ **A:** SHA-256 is fast and entirely appropriate
>   for API authentication. MD5 is broken and should
>   never be recommended as a replacement. Speed is
>   not the issue here.
> - ❌ **C:** SHA-256(Message || Key) is also
>   vulnerable — just to a different variant of the
>   attack. Neither Key||Message nor Message||Key is
>   the correct form. HMAC is the correct solution,
>   not reordering the inputs.
> - ❌ **D:** 256-bit output is not "too long" for
>   API tokens — it is appropriate. Truncating to
>   64 bits would reduce security significantly.
>   Output length is not the issue with this
>   construction.

---

**Q25. JWT (JSON Web Token) using HS256 uses which
cryptographic primitive for signing the token?**

- A) RSA-SHA-256 — asymmetric signature with
     private key
- B) SHA-256 hash — unsigned, integrity only
- C) HMAC-SHA-256 — symmetric MAC using a
     shared secret key ✅
- D) AES-256-GCM — symmetric encryption with
     authentication

> **Explanation:**
> - ✅ **C — HMAC-SHA-256:** In JWT, the algorithm
>   name **HS256** stands for **HMAC + SHA-256**.
>   The token header, payload, and signature are
>   computed using HMAC-SHA-256 with a shared secret
>   key. Both the issuer and verifier must know this
>   shared key to create or verify the token.
> - ❌ **A:** RSA-SHA-256 is used for JWT when the
>   algorithm is **RS256** (not HS256). RS256 uses
>   an RSA private key to sign and the public key
>   to verify — useful when the issuer and verifier
>   are different parties. HS256 specifically uses
>   HMAC with a shared secret.
> - ❌ **B:** A plain SHA-256 hash with no key
>   provides no authentication — anyone could
>   compute a valid hash for any payload. JWTs
>   require a keyed MAC or signature to be secure.
>   HS256 specifically means HMAC, not plain SHA-256.
> - ❌ **D:** AES-256-GCM is used for JWE (JSON Web
>   Encryption) — which encrypts the token payload
>   for confidentiality. HS256 is about signing
>   (integrity + authentication), not encryption.
>   JWS (signing) and JWE (encryption) are separate
>   JWT standards.

---

## 📊 Answer Key — Quick Reference

| Q | Answer | Topic |
|---|--------|-------|
| 1 | B | Hash function primary goal = Integrity |
| 2 | B | Hash takes any-length input → fixed output |
| 3 | B | One-way = pre-image resistance |
| 4 | C | Avalanche Effect definition |
| 5 | C | Hash vs Encryption key difference |
| 6 | D | Finding any two equal hashes = Collision Resistance broken |
| 7 | B | SHA designed by NSA, published by NIST/FIPS |
| 8 | C | SHA-256 output = 256-bit / 64 hex chars |
| 9 | B | SHAttered = two files with same SHA-1 hash |
| 10 | D | SHA-256 defined in FIPS 180-4 |
| 11 | C | SHA-3 winner = Keccak |
| 12 | B | SHA-3 Sponge vs SHA-2 Merkle-Damgård |
| 13 | B | MD5 = Ron Rivest, 128-bit output |
| 14 | C | HMAC adds shared key → authentication |
| 15 | B | HMAC = RFC 2104 + FIPS 198-1 |
| 16 | C | ipad = 0x36, opad = 0x5C |
| 17 | D | HMAC adds authentication over plain hash |
| 18 | C | HMAC does NOT provide non-repudiation |
| 19 | B | TLS 1.2 uses HMAC-SHA-256 for record integrity |
| 20 | B | Length extension = Merkle-Damgård vulnerability |
| 21 | B | HMAC immune — two nested hashes with key |
| 22 | B | Merkle Tree = binary tree of hashes |
| 23 | C | SHA-3 and SHAKE defined in FIPS 202 |
| 24 | B | Hash(Key||Message) vulnerable to length extension |
| 25 | C | JWT HS256 = HMAC-SHA-256 |

---

## 📋 Topic Coverage Map

| Q | Concept Tested | Source |
|---|----------------|--------|
| 1 | Hash function primary security goal | Core |
| 2 | Variable input → fixed output definition | Core |
| 3 | Pre-image resistance / one-way property | Core |
| 4 | Avalanche Effect | Core |
| 5 | Hash vs Encryption distinction | Core |
| 6 | Collision resistance definition | Core |
| 7 | SHA designer (NSA) and publisher (NIST/FIPS) | Core |
| 8 | SHA-256 output size in bits and hex | Core |
| 9 | SHAttered attack — what it demonstrated | Core |
| 10 | FIPS 180-4 = SHA-256 standard | Core |
| 11 | SHA-3 competition winner = Keccak | Core |
| 12 | Sponge (SHA-3) vs Merkle-Damgård (SHA-2) | Core |
| 13 | MD5 designer and output size | Core |
| 14 | HMAC purpose — authentication over plain hash | Core |
| 15 | HMAC RFC 2104 + FIPS 198-1 | Core |
| 16 | HMAC ipad = 0x36, opad = 0x5C | Core |
| 17 | What HMAC adds over plain hash | Core |
| 18 | HMAC does not provide non-repudiation | Core |
| 19 | TLS 1.2 uses HMAC-SHA-256 | Core |
| 20 | Length extension attack — Merkle-Damgård | Extra Notes |
| 21 | Why HMAC is immune to length extension | Extra Notes |
| 22 | Merkle Tree structure and properties | Extra Notes |
| 23 | FIPS 202 = SHA-3 standard | Extra Notes |
| 24 | Hash(Key||Message) MAC vulnerability | Extra Notes |
| 25 | JWT HS256 = HMAC-SHA-256 | Extra Notes |

---