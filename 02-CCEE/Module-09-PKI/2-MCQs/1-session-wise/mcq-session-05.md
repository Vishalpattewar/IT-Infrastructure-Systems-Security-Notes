# MCQ Session 05 — Diffie-Hellman Key Exchange, Attacks
Against Encryption & Cryptographic Issues

## 📑 Table of Contents
- [Instructions](#instructions)
- [MCQs 1–6 — Diffie-Hellman Key Exchange](#mcqs-16--diffie-hellman-key-exchange)
- [MCQs 7–13 — Attacks Against Encryption](#mcqs-713--attacks-against-encryption)
- [MCQs 14–18 — Cryptographic Issues](#mcqs-1418--cryptographic-issues)
- [MCQs 19–25 — Extra Notes: Protocol Attacks,
  Password Storage, Salt](#mcqs-1925--extra-notes-protocol-attacks-password-storage-salt)
- [Answer Key](#-answer-key--quick-reference)
- [Topic Coverage Map](#-topic-coverage-map)

---

## Instructions

- 25 MCQs — drawn from core syllabus AND
  📌 Extra Notes of Session 05
- Foundation + Fundamental + Basic Concepts ONLY
- 4 options per question
- ✅ marks the correct answer
- Full explanation after every question including
  why each wrong option is wrong
- Wrong options look reasonable to someone unprepared
- Correct answer is clear to someone with solid basics

---

## MCQs 1–6 — Diffie-Hellman Key Exchange

---

**Q1. Diffie-Hellman was published in 1976 by Whitfield
Diffie and Martin Hellman. What is the PRIMARY purpose
of the Diffie-Hellman protocol?**

- A) To encrypt large amounts of data quickly using
     a shared symmetric key
- B) To establish a shared secret key over an insecure
     channel without prior communication ✅
- C) To digitally sign messages and provide
     non-repudiation
- D) To generate public and private key pairs for
     asymmetric encryption

> **Explanation:**
> - ✅ **B:** Diffie-Hellman is a **key exchange
>   protocol** — its sole purpose is to allow two
>   parties to establish a shared secret over an
>   insecure (public) channel without having met
>   beforehand. The shared secret is then used as a
>   symmetric encryption key for actual data encryption.
> - ❌ **A:** DH does not encrypt data — it only
>   establishes the shared key. A separate symmetric
>   algorithm (like AES) does the actual encryption.
> - ❌ **C:** DH does not provide digital signatures
>   or non-repudiation. DSA and ECDSA are used for
>   digital signatures.
> - ❌ **D:** DH does not generate public/private key
>   pairs for asymmetric encryption. RSA and ECC do
>   that. DH generates temporary values for key
>   agreement purposes only.

---

**Q2. The security of Diffie-Hellman key exchange
relies on which mathematical problem?**

- A) The Integer Factorization Problem — difficulty
     of factoring large numbers into prime factors
- B) The Elliptic Curve Discrete Logarithm Problem —
     finding k given P = k × G
- C) The Discrete Logarithm Problem — difficulty of
     finding x given gˣ mod p ✅
- D) The Knapsack Problem — difficulty of finding
     subset sums in large integer sets

> **Explanation:**
> - ✅ **C:** DH security rests on the **Discrete
>   Logarithm Problem (DLP)** — given g, p, and
>   y = gˣ mod p, finding x is computationally
>   infeasible for large prime p. Computing gˣ mod p
>   is easy; reversing it to find x is hard.
> - ❌ **A:** Integer Factorization is the hard problem
>   behind **RSA** — not DH. These are two different
>   mathematical problems.
> - ❌ **B:** ECDLP is the hard problem behind **ECC
>   and ECDH** — not classical DH over Zp. ECDH is a
>   variant of DH that uses elliptic curves instead.
> - ❌ **D:** The Knapsack Problem was used in early
>   asymmetric cryptography (Merkle-Hellman, 1978)
>   but was broken — it is not the basis of DH.

---

**Q3. In a Diffie-Hellman key exchange, Alice chooses
private key a = 6, uses public parameters p = 23 and
g = 5. What value does Alice send to Bob?**

- A) 6
- B) 23
- C) 5
- D) 8 ✅

> **Explanation:**
> - ✅ **D — 8:** Alice computes her public value:
>   A = gᵃ mod p = 5⁶ mod 23 = 15625 mod 23 = 8.
>   (15625 ÷ 23 = 679 remainder 8)
>   She sends 8 to Bob — NOT her private key a = 6.
> - ❌ **A — 6:** This is Alice's **private key** —
>   it must never be sent. The whole point of DH is
>   that private keys stay private and are never
>   transmitted.
> - ❌ **B — 23:** p is the public prime modulus —
>   already known to both parties as a public
>   parameter. It is not what Alice computes and sends.
> - ❌ **C — 5:** g is the generator — another public
>   parameter already known to both parties. Alice
>   sends her computed public value, not g itself.

---

**Q4. What does the "E" in DHE stand for, and what
security benefit does it provide?**

- A) Extended — DHE uses a longer key than standard DH
     for stronger security
- B) Encrypted — DHE encrypts the DH parameters before
     sending them
- C) Ephemeral — DHE generates a fresh key pair for
     every session, providing Perfect Forward Secrecy ✅
- D) Embedded — DHE embeds authentication inside the
     DH computation

> **Explanation:**
> - ✅ **C — Ephemeral:** The E in DHE stands for
>   **Ephemeral** — meaning temporary. DHE generates
>   a brand new DH key pair for every session and
>   discards it immediately after. This provides
>   **Perfect Forward Secrecy (PFS)** — even if
>   the long-term private key is stolen later, past
>   session keys cannot be recovered because the
>   ephemeral keys no longer exist.
> - ❌ **A:** DHE does not necessarily use longer keys
>   than standard DH — the key size is a separate
>   parameter. "Extended" is not what E stands for.
> - ❌ **B:** DHE does not encrypt DH parameters —
>   those are sent in the clear (they are public
>   values). The security comes from DLP, not from
>   encrypting the parameters.
> - ❌ **D:** Authentication is not built into DHE —
>   authentication requires certificates or signatures
>   added on top of DHE (as in TLS). DHE itself
>   is not authenticated.

---

**Q5. Basic Diffie-Hellman key exchange is vulnerable
to which attack because it provides no authentication?**

- A) Brute Force Attack — attacker tries all possible
     values of the shared secret
- B) Man-in-the-Middle Attack — attacker intercepts
     and substitutes both parties' public values ✅
- C) Replay Attack — attacker retransmits a previously
     captured DH exchange
- D) Birthday Attack — attacker finds two DH public
     values that produce the same shared secret

> **Explanation:**
> - ✅ **B — Man-in-the-Middle:** Basic DH has no
>   authentication — it establishes a shared secret
>   but does NOT verify who you are sharing it with.
>   An attacker in the middle can intercept Alice's
>   public value A, replace it with their own value,
>   and do the same with Bob's — ending up with two
>   separate shared secrets, one with Alice and one
>   with Bob, while both believe they are talking
>   directly to each other.
> - ❌ **A:** Brute Force against DH means solving
>   the Discrete Logarithm Problem — not practical
>   for large key sizes. This is the general attack
>   on DH's mathematical security, not the specific
>   vulnerability of unauthenticated DH.
> - ❌ **C:** Replay attack captures and retransmits
>   messages — while possible in poorly designed
>   systems, it is not the PRIMARY known vulnerability
>   of basic DH specifically.
> - ❌ **D:** Birthday attack targets hash collisions
>   — it is not relevant to DH public value
>   computation. DH shared secrets are derived
>   mathematically, not through hashing.

---

**Q6. TLS 1.3 requires a specific DH variant for all
key exchange. Which variant is mandatory in TLS 1.3
and why?**

- A) Static DH — because it is the most established
     and compatible variant
- B) DHE — because it provides the best performance
     with 2048-bit parameters
- C) ECDHE — because it provides Perfect Forward
     Secrecy with efficient elliptic curve keys ✅
- D) RSA key transport — because RSA authentication
     and key exchange are combined in one step

> **Explanation:**
> - ✅ **C — ECDHE:** TLS 1.3 (RFC 8446, 2018)
>   mandates ECDHE for all key exchange. ECDHE
>   provides Perfect Forward Secrecy (ephemeral keys
>   per session) using efficient elliptic curve
>   mathematics (shorter keys than DHE with equivalent
>   security). TLS 1.3 removed all non-PFS cipher
>   suites including static RSA and static DH.
> - ❌ **A:** Static DH was explicitly removed from
>   TLS 1.3 because it provides no PFS — the same
>   private key is reused, so past sessions become
>   decryptable if the key is compromised.
> - ❌ **B:** DHE (classical DH) is supported in
>   TLS 1.3 but ECDHE is the preferred and dominant
>   variant due to smaller key sizes and better
>   performance. DHE alone is not the answer here.
> - ❌ **D:** RSA key transport was removed from
>   TLS 1.3 precisely because it has no PFS. This
>   was one of the most significant changes TLS 1.3
>   made from TLS 1.2.

---

## MCQs 7–13 — Attacks Against Encryption

---

**Q7. An attacker systematically tries every possible
key value until the correct one is found. What type
of attack is this?**

- A) Dictionary Attack
- B) Rainbow Table Attack
- C) Brute Force Attack ✅
- D) Side-Channel Attack

> **Explanation:**
> - ✅ **C — Brute Force Attack:** A brute force
>   attack tries every possible key in the key space
>   exhaustively — no shortcuts, no intelligence
>   about the key. It is guaranteed to eventually
>   find the key but is only practical when the
>   key space is small.
> - ❌ **A:** A dictionary attack uses a pre-compiled
>   list of likely passwords or keys — NOT every
>   possible combination. It is smarter and faster
>   than brute force but less exhaustive.
> - ❌ **B:** A rainbow table attack uses pre-computed
>   hash-to-password mappings for instant lookup —
>   it does not try keys one by one.
> - ❌ **D:** A side-channel attack exploits physical
>   information leakage (timing, power consumption,
>   EM) — not key enumeration.

---

**Q8. Why is AES-128 considered practically immune
to brute force attacks?**

- A) AES-128 uses a special algorithm that detects
     and blocks brute force attempts automatically
- B) AES-128 keys are generated using a process that
     makes all but one key invalid
- C) The AES-128 key space is 2¹²⁸ — so large that
     exhaustive search is computationally infeasible
     with any foreseeable technology ✅
- D) AES-128 changes its key automatically every
     few milliseconds making brute force impossible

> **Explanation:**
> - ✅ **C:** AES-128 has a key space of 2¹²⁸ —
>   approximately 340 undecillion possible keys.
>   Even with all the computing power on earth, trying
>   every key would take longer than the age of the
>   universe. This makes brute force computationally
>   infeasible — not prevented by the algorithm but
>   by the sheer size of the search space.
> - ❌ **A:** AES has no built-in brute force
>   detection — it is a pure mathematical cipher
>   that processes input without any awareness of
>   how many times it has been called.
> - ❌ **B:** All 2¹²⁸ possible AES-128 keys are
>   valid — any 128-bit value can be used as an
>   AES-128 key. There is no invalid key filtering.
> - ❌ **D:** AES does not rotate keys automatically
>   — key management is handled at the protocol
>   level (e.g., TLS session keys), not by AES itself.

---

**Q9. An attacker obtains a database of hashed
passwords and uses a pre-computed table that maps
known passwords to their hash values for instant
lookup. What is this attack called?**

- A) Dictionary Attack
- B) Brute Force Attack
- C) Rainbow Table Attack ✅
- D) Timing Attack

> **Explanation:**
> - ✅ **C — Rainbow Table Attack:** A rainbow table
>   is a pre-computed lookup table of
>   password → hash mappings. Once an attacker has
>   the table, cracking a hash is an instant lookup
>   operation — no computation needed at attack time.
>   The pre-computation is done once and reused
>   for any number of attacks.
> - ❌ **A:** A dictionary attack computes hashes
>   live during the attack — it does not use a
>   pre-computed table. Rainbow tables are faster
>   because the computation is done in advance.
> - ❌ **B:** Brute force tries all possible
>   combinations live — it is the slowest method
>   and does not use pre-computed tables.
> - ❌ **D:** A timing attack measures time taken
>   by cryptographic operations to leak key
>   information — it has nothing to do with
>   password hash databases.

---

**Q10. What is the most effective countermeasure
against rainbow table attacks on password databases?**

- A) Using a longer password hashing algorithm
     such as SHA-512 instead of SHA-256
- B) Encrypting the password database with AES-256
     before storing it
- C) Adding a unique random salt to each password
     before hashing ✅
- D) Hashing the password multiple times (e.g.,
     MD5(MD5(password)))

> **Explanation:**
> - ✅ **C — Salt:** A unique random salt per user
>   makes every hash unique — even if two users have
>   the same password. Pre-computed rainbow tables
>   are built for unsalted hashes and become completely
>   useless because the attacker would need to rebuild
>   the entire table for every unique salt value.
> - ❌ **A:** Using SHA-512 instead of SHA-256 does
>   not defeat rainbow tables — rainbow tables can
>   be built for SHA-512 just as easily. The length
>   of the hash output is not the issue; uniqueness
>   per user is.
> - ❌ **B:** Database encryption protects against
>   some attack scenarios but does not defeat rainbow
>   tables — if the attacker has the decryption key
>   or the database is decrypted (e.g., in a running
>   application), the unsalted hashes are still
>   vulnerable to table lookup.
> - ❌ **D:** Hashing multiple times (MD5(MD5(x)))
>   does not add uniqueness — the same password still
>   produces the same final hash for every user.
>   Rainbow tables can be adapted for chained hashes.
>   This is security through complexity, not through
>   proper design.

---

**Q11. An attacker secretly positions themselves
between two communicating parties, intercepting and
possibly modifying all messages while each party
believes they are communicating directly. What is
this attack called?**

- A) Replay Attack
- B) Man-in-the-Middle (MITM) Attack ✅
- C) Side-Channel Attack
- D) Downgrade Attack

> **Explanation:**
> - ✅ **B — MITM:** Man-in-the-Middle describes
>   exactly this scenario — the attacker inserts
>   themselves between two parties, relaying
>   communications while potentially reading or
>   altering content. Neither party is aware of
>   the attacker's presence.
> - ❌ **A:** Replay attack involves capturing a
>   valid message and retransmitting it later —
>   the attacker does not position themselves in
>   the middle of an ongoing conversation. The
>   attack is about reuse of captured data, not
>   interception.
> - ❌ **C:** Side-channel attack exploits physical
>   leakage (timing, power, EM) from a device —
>   it is not about intercepting network communications
>   between two parties.
> - ❌ **D:** Downgrade attack forces the use of
>   a weaker protocol version — it is a specific
>   type of manipulation but the broader category
>   of secretly intercepting all communication
>   between two parties is MITM.

---

**Q12. A valid authentication token is captured by
an attacker and submitted to a server again at a
later time to gain unauthorized access. What type
of attack is this?**

- A) Man-in-the-Middle Attack
- B) Brute Force Attack
- C) Replay Attack ✅
- D) Dictionary Attack

> **Explanation:**
> - ✅ **C — Replay Attack:** A replay attack
>   captures a valid credential or message and
>   retransmits it — exploiting the fact that the
>   server cannot distinguish between the original
>   legitimate transmission and the replayed copy.
>   The attacker does not need to know the password
>   or break the encryption — just replay what was
>   already valid.
> - ❌ **A:** MITM involves actively intercepting
>   an ongoing conversation between two parties —
>   a replay attack is simpler: capture once,
>   replay later. No ongoing interception required.
> - ❌ **B:** Brute force tries all possible keys
>   or passwords — it does not involve capturing
>   and reusing existing valid tokens.
> - ❌ **D:** Dictionary attack uses a wordlist of
>   probable passwords to crack credentials — it
>   does not involve reusing captured valid tokens.

---

**Q13. An attacker measures the exact time a server
takes to perform RSA decryption operations and uses
these timing differences to deduce the private key.
What category of attack is this?**

- A) Cryptanalytic Attack — targeting the RSA
     mathematical algorithm directly
- B) Side-Channel Attack — exploiting physical
     information leaked by the implementation ✅
- C) Protocol Attack — exploiting a weakness in
     the TLS protocol design
- D) Brute Force Attack — trying all possible
     RSA private key values

> **Explanation:**
> - ✅ **B — Side-Channel Attack:** A timing attack
>   is a classic side-channel attack — it does not
>   attack the RSA algorithm mathematically. Instead
>   it exploits the fact that RSA modular
>   exponentiation takes different amounts of time
>   depending on the bits of the private key — a
>   physical property of the implementation, not
>   a flaw in the algorithm itself.
> - ❌ **A:** Cryptanalytic attacks target the
>   mathematical structure of the algorithm (e.g.,
>   differential cryptanalysis on DES). A timing
>   attack does not analyze the mathematics of RSA
>   — it analyzes the physical behavior of the
>   machine running it.
> - ❌ **C:** Protocol attacks target the design
>   of communication protocols (e.g., POODLE against
>   SSL 3.0). Measuring a server's RSA timing is an
>   attack on the implementation, not the protocol.
> - ❌ **D:** Brute forcing RSA would mean trying
>   all possible private key values — computationally
>   infeasible for 2048-bit RSA. This is a targeted,
>   intelligent attack using timing measurements,
>   not exhaustive search.

---

## MCQs 14–18 — Cryptographic Issues

---

**Q14. Which of the following is the MOST common
real-world cause of cryptographic system failures?**

- A) The underlying mathematical algorithms
     being broken by cryptanalysts
- B) Attackers using quantum computers to solve
     hard mathematical problems
- C) Poor key management — weak generation, reuse,
     insecure storage, or no rotation ✅
- D) Insufficient computing power to run strong
     encryption algorithms

> **Explanation:**
> - ✅ **C — Poor key management:** The vast majority
>   of real-world cryptographic failures are NOT due
>   to broken algorithms. They result from poor key
>   management — hardcoded keys, keys stored in
>   plaintext, keys committed to GitHub, weak random
>   number generation, or keys never rotated. AES
>   and RSA themselves are not broken — but poor
>   key handling breaks the security they provide.
> - ❌ **A:** Modern algorithms like AES-128 and
>   RSA-2048 have no known practical cryptanalytic
>   attacks. Algorithm breaks are rare and typically
>   take years of academic research.
> - ❌ **B:** Cryptographically relevant quantum
>   computers do not yet exist in 2026. Quantum
>   threats are a future concern — not the current
>   dominant cause of real-world failures.
> - ❌ **D:** Modern hardware is more than sufficient
>   to run AES, RSA, and ECC. Performance is rarely
>   a limiting factor in deploying strong encryption.

---

**Q15. A developer encrypts a file using AES-CBC
mode and reuses the same Initialization Vector (IV)
every time with the same key. What is the security
consequence?**

- A) The encryption becomes faster but less random
- B) The same plaintext always produces the same
     ciphertext — revealing patterns in the data ✅
- C) The decryption key is automatically revealed
     after several encryptions
- D) AES-CBC requires a fixed IV — reuse is
     the correct implementation

> **Explanation:**
> - ✅ **B:** In CBC mode, the IV randomizes the
>   first block so that the same plaintext encrypted
>   twice produces different ciphertext. If the IV
>   is reused with the same key, two identical
>   plaintexts produce identical ciphertext — leaking
>   information about the data. An attacker can
>   detect when the same message is sent again and
>   may recover plaintext through chosen plaintext
>   attacks.
> - ❌ **A:** Speed and randomness are not the issue
>   — security is. IV reuse is a critical security
>   flaw, not a performance trade-off.
> - ❌ **C:** IV reuse does not directly reveal the
>   decryption key. The damage is pattern leakage
>   in the ciphertext — not immediate key disclosure.
> - ❌ **D:** AES-CBC absolutely requires a fresh
>   random IV for every encryption — reuse is
>   explicitly wrong and violates the security
>   requirements of CBC mode.

---

**Q16. Which of the following block cipher modes
should NEVER be used because identical plaintext
blocks always produce identical ciphertext blocks?**

- A) CBC (Cipher Block Chaining)
- B) GCM (Galois/Counter Mode)
- C) CTR (Counter Mode)
- D) ECB (Electronic Codebook) ✅

> **Explanation:**
> - ✅ **D — ECB:** In ECB mode, every plaintext
>   block is encrypted independently with the same
>   key — so identical plaintext blocks always
>   produce identical ciphertext blocks. This reveals
>   data patterns. The famous "ECB penguin" — where
>   an image encrypted with ECB still shows the
>   outline of the original — demonstrates this flaw.
> - ❌ **A:** CBC XORs each plaintext block with the
>   previous ciphertext block before encrypting —
>   identical plaintext blocks produce different
>   ciphertext. CBC is secure with a random IV.
> - ❌ **B:** GCM is one of the most secure modes —
>   it uses a counter and provides both encryption
>   and authentication. No pattern leakage.
> - ❌ **C:** CTR mode uses an incrementing counter
>   for each block — identical plaintext blocks
>   produce different ciphertext. Secure and
>   parallelizable.

---

**Q17. A security audit finds that a web application
stores user passwords as plain MD5 hashes with no
salt. What are the TWO primary risks of this approach?**

- A) MD5 is too slow — causing login performance
     issues; no salt means the database is unencrypted
- B) MD5 hashes are reversible — any attacker can
     directly convert them back to passwords
- C) MD5 is a fast hash vulnerable to GPU-based
     cracking; without salt, rainbow tables provide
     instant password recovery ✅
- D) MD5 is an asymmetric algorithm — it requires
     a public key to verify passwords correctly

> **Explanation:**
> - ✅ **C:** Two problems: (1) MD5 is a fast general-
>   purpose hash — modern GPUs compute billions of
>   MD5 hashes per second, enabling rapid brute
>   force or dictionary attacks. (2) Without salt,
>   every user with the same password has the same
>   hash — pre-computed rainbow tables provide
>   instant lookup. Password hashing requires slow,
>   salted functions like bcrypt, scrypt, or Argon2.
> - ❌ **A:** MD5 is actually extremely fast — not
>   slow. The speed is the problem, not a benefit.
>   And lack of salt is about pre-computation
>   vulnerability, not encryption of the database.
> - ❌ **B:** MD5 is a one-way hash — it is NOT
>   directly reversible in the mathematical sense.
>   Attackers crack it through brute force, dictionary
>   attacks, and rainbow tables — not by reversing
>   the function.
> - ❌ **D:** MD5 is a hash function — it is not
>   asymmetric and requires no key at all. This
>   option confuses hash functions with asymmetric
>   encryption.

---

**Q18. What is a cryptographic nonce and what
attack does it prevent in authentication protocols?**

- A) A nonce is a secret key used once for symmetric
     encryption — it prevents brute force attacks
- B) A nonce is a Number Used Once — a unique random
     value included in authentication exchanges to
     prevent replay attacks ✅
- C) A nonce is a hash of the user's password
     used to prevent rainbow table attacks
- D) A nonce is an initialization vector used
     in block cipher modes to prevent pattern leakage

> **Explanation:**
> - ✅ **B — Nonce:** A nonce (Number Used Once) is
>   a unique, typically random value generated by
>   a server and included in an authentication
>   challenge. The client must include this nonce
>   in their response. Since the nonce is unique per
>   session and expires quickly, a captured response
>   cannot be replayed — the nonce will no longer
>   be valid.
> - ❌ **A:** A nonce is not a secret key — it is
>   typically sent in the clear as part of a
>   challenge. Its security property comes from
>   uniqueness and expiration, not secrecy.
> - ❌ **C:** A nonce is not a password hash —
>   nonces are server-generated random values for
>   challenges, not derived from user passwords.
>   Salts (not nonces) defeat rainbow tables.
> - ❌ **D:** An IV (Initialization Vector) is used
>   in block cipher modes — it is a different concept.
>   Both IVs and nonces are random values, but they
>   serve different purposes in different contexts.
>   Conflating them is a common mistake.

---

## MCQs 19–25 — Extra Notes: Protocol Attacks,
Password Storage, Salt

---

**Q19. The POODLE attack (2014) forced connections
to fall back to which deprecated protocol, and
what flaw did it exploit?**

- A) TLS 1.0 — exploited predictable IV in CBC mode
- B) SSL 3.0 — exploited undefined CBC padding
     in SSL 3.0 ✅
- C) TLS 1.1 — exploited weak DHE key parameters
- D) SSL 2.0 — exploited weak export-grade
     RC4 cipher suites

> **Explanation:**
> - ✅ **B — SSL 3.0 / CBC padding:** POODLE
>   (Padding Oracle On Downgraded Legacy Encryption)
>   forced TLS connections to downgrade to SSL 3.0
>   (by triggering connection failures that caused
>   browsers to retry with older protocols). SSL 3.0
>   used CBC mode with undefined/random padding —
>   creating a padding oracle that allowed recovery
>   of plaintext (session cookies) with ~256 requests
>   per byte.
> - ❌ **A:** TLS 1.0 / predictable IV describes
>   the **BEAST attack (2011)** — not POODLE.
>   BEAST and POODLE are two separate attacks with
>   different targets and mechanisms.
> - ❌ **C:** TLS 1.1 weak DHE parameters describes
>   aspects of the **Logjam attack (2015)** — not
>   POODLE. Logjam forced downgrade to export-grade
>   DH, not SSL 3.0.
> - ❌ **D:** SSL 2.0 export RC4 attacks describe
>   aspects of the **FREAK/DROWN** family of attacks
>   — not POODLE. POODLE specifically targets
>   SSL 3.0's CBC padding behavior.

---

**Q20. The BEAST attack (2011) targeted which
specific TLS version and what vulnerability
did it exploit?**

- A) SSL 3.0 — undefined padding in CBC mode
- B) TLS 1.2 — weak AES-GCM authentication tag
- C) TLS 1.0 — predictable IV in CBC mode ✅
- D) TLS 1.1 — weak DHE key parameters

> **Explanation:**
> - ✅ **C — TLS 1.0 / predictable IV:** BEAST
>   (Browser Exploit Against SSL/TLS) targeted
>   TLS 1.0. In TLS 1.0, the IV for each record's
>   CBC encryption is the last ciphertext block of
>   the previous record — making it predictable.
>   An attacker who can inject chosen plaintext and
>   observe ciphertext can exploit this predictable
>   IV to recover plaintext (session cookies).
> - ❌ **A:** SSL 3.0 / undefined CBC padding is
>   **POODLE (2014)** — not BEAST. Easy to confuse
>   because both target CBC mode, but they attack
>   different protocol versions with different
>   specific flaws.
> - ❌ **B:** TLS 1.2 with AES-GCM has no known
>   practical attacks — GCM provides authenticated
>   encryption that detects tampering. BEAST predates
>   widespread GCM deployment.
> - ❌ **D:** TLS 1.1 / weak DHE is associated with
>   **Logjam** — not BEAST. TLS 1.1 actually fixed
>   BEAST's vulnerability by using a random IV.

---

**Q21. The CRIME attack (2012) exploited which
TLS feature to recover plaintext session cookies?**

- A) TLS certificate validation weakness
- B) TLS compression — ciphertext length leaks
     information about plaintext content ✅
- C) TLS CBC padding oracle
- D) TLS RSA key transport without PFS

> **Explanation:**
> - ✅ **B — TLS compression:** CRIME (Compression
>   Ratio Info-leak Made Easy) exploited TLS-level
>   data compression. When data is compressed before
>   encryption, the length of the ciphertext reveals
>   information about the plaintext — because
>   matching strings compress to shorter output.
>   An attacker who controls part of the request and
>   can observe ciphertext length can guess secret
>   cookie values character by character.
> - ❌ **A:** Certificate validation weaknesses
>   describe MITM scenarios where certificates are
>   not properly verified — a completely different
>   attack vector unrelated to CRIME.
> - ❌ **C:** CBC padding oracle describes POODLE
>   and Bleichenbacher attacks — not CRIME. CRIME
>   exploits compression length, not padding errors.
> - ❌ **D:** RSA key transport without PFS is the
>   issue addressed by requiring DHE/ECDHE — not
>   related to the CRIME compression attack.

---

**Q22. The FREAK attack (2015) forced TLS to use
export-grade cryptography. What was the maximum
RSA key size for export-grade RSA under 1990s
US export regulations?**

- A) 1024-bit
- B) 768-bit
- C) 512-bit ✅
- D) 256-bit

> **Explanation:**
> - ✅ **C — 512-bit:** US export regulations in
>   the 1990s limited RSA keys to **512 bits** for
>   software exported outside the US. FREAK
>   (Factoring RSA Export Keys) exploited servers
>   that still supported these legacy export cipher
>   suites — a 512-bit RSA key can be factored in
>   approximately 7 hours on modern hardware.
> - ❌ **A — 1024-bit:** 1024-bit RSA is considered
>   deprecated today but was never an "export-grade"
>   limit — it is far stronger than what export
>   regulations allowed.
> - ❌ **B — 768-bit:** 768-bit RSA has been factored
>   (2010) but was not the specific export limit.
>   The regulation capped at 512 bits.
> - ❌ **D — 256-bit:** 256-bit RSA does not exist
>   as a practical key size — RSA at 256 bits would
>   be trivially broken. The export limit was
>   512 bits, not 256.

---

**Q23. What is the purpose of a salt in password
storage, and does it need to be kept secret?**

- A) Salt is a secret key that encrypts the password
     hash — it must be kept secret
- B) Salt is a unique random value added to each
     password before hashing — it does not need
     to be secret, only unique ✅
- C) Salt is a fixed application-wide value that
     speeds up hash computation — it should be
     secret
- D) Salt is the second round of hashing applied
     to the password — it replaces the need for
     a strong hash function

> **Explanation:**
> - ✅ **B:** A salt is a unique random value
>   generated per user and added to their password
>   before hashing. Its purpose is uniqueness — not
>   secrecy. The salt is stored alongside the hash
>   in the database (in plaintext) so it can be
>   used during login verification. Its security
>   benefit comes from making pre-computation
>   (rainbow tables) infeasible — not from being
>   hidden.
> - ❌ **A:** A salt is not a secret key and does
>   not encrypt anything. If salts needed to be
>   secret, they would be called "peppers" —
>   which are a separate concept (secret,
>   application-wide, stored separately from DB).
> - ❌ **C:** A fixed application-wide value
>   describes a **pepper** — not a salt. Salt must
>   be unique per user — a shared fixed value
>   does not defeat rainbow tables for users with
>   the same password.
> - ❌ **D:** Salt is not a second round of hashing
>   — it is additional input data. Using a better
>   hash function (bcrypt, Argon2) is separate from
>   salting — both are needed together.

---

**Q24. Which password hashing function won the
Password Hashing Competition (PHC) in 2015 and
is currently considered the best practice for
storing passwords?**

- A) bcrypt
- B) PBKDF2
- C) scrypt
- D) Argon2id ✅

> **Explanation:**
> - ✅ **D — Argon2id:** Argon2 won the Password
>   Hashing Competition (PHC) in 2015 — a competition
>   run by cryptographers to select a modern password
>   hashing standard. Argon2id (the hybrid variant)
>   is the recommended choice — it is both memory-hard
>   (resists GPU/ASIC attacks) and resistant to
>   side-channel attacks. It is specified in RFC 9106.
> - ❌ **A — bcrypt:** bcrypt (1999) is a good
>   adaptive password hash widely used in web
>   applications — but it is NOT memory-hard and
>   did not win the PHC. Argon2 is the modern
>   successor and current best practice.
> - ❌ **B — PBKDF2:** PBKDF2 is NIST-approved and
>   widely used (WPA2, PKCS#5) — but it is not
>   memory-hard, making it more vulnerable to
>   GPU-based attacks than Argon2 or scrypt.
>   It did not win the PHC.
> - ❌ **C — scrypt:** scrypt (2009) is memory-hard
>   and strong — but Argon2 was selected over it
>   in the PHC for its cleaner design and better
>   flexibility. scrypt is still a good choice but
>   Argon2id is the current recommendation.

---

**Q25. A TLS client that supports TLS 1.3 is tricked
into connecting with TLS 1.0 by an attacker.
What mechanism in TLS specifically prevents this
type of downgrade attack?**

- A) Certificate Pinning — the client only accepts
     certificates from specific CAs
- B) HSTS (HTTP Strict Transport Security) —
     forces HTTPS connections
- C) TLS_FALLBACK_SCSV — a signaling value the
     client includes when downgrading that tells
     the server to reject inappropriate fallbacks ✅
- D) OCSP Stapling — the server provides a
     certificate revocation proof

> **Explanation:**
> - ✅ **C — TLS_FALLBACK_SCSV:** RFC 7507 (2015)
>   defines TLS_FALLBACK_SCSV (Signaling Cipher Suite
>   Value). When a client retries a connection at a
>   lower protocol version (downgrade), it includes
>   TLS_FALLBACK_SCSV in its ClientHello. If the
>   server supports a higher version than what the
>   client is requesting, it sends an "inappropriate
>   fallback" alert and aborts — preventing an
>   attacker from forcing a downgrade to a weaker
>   protocol.
> - ❌ **A:** Certificate Pinning restricts which
>   certificates a client will accept — it prevents
>   fraudulent certificate MITM attacks, not
>   protocol version downgrade attacks. Different
>   problem, different solution.
> - ❌ **B:** HSTS forces all connections to use
>   HTTPS instead of HTTP — it prevents protocol
>   downgrade from HTTPS to HTTP, not downgrade
>   from TLS 1.3 to TLS 1.0. Different layer,
>   different attack.
> - ❌ **D:** OCSP Stapling provides certificate
>   revocation status — it verifies that a
>   certificate has not been revoked. It has no
>   role in preventing TLS version downgrade attacks.

---

## 📊 Answer Key — Quick Reference

| Q | Answer | Topic |
|---|--------|-------|
| 1 | B | DH purpose — key exchange only |
| 2 | C | DH security basis — Discrete Logarithm Problem |
| 3 | D | DH public value calculation — gᵃ mod p = 8 |
| 4 | C | DHE — Ephemeral → PFS |
| 5 | B | Basic DH vulnerable to MITM — no authentication |
| 6 | C | TLS 1.3 mandates ECDHE |
| 7 | C | Brute force — tries all possible keys |
| 8 | C | AES-128 immune to brute force — 2¹²⁸ key space |
| 9 | C | Rainbow table — pre-computed hash lookup |
| 10 | C | Salt defeats rainbow tables |
| 11 | B | MITM — attacker between two parties |
| 12 | C | Replay attack — captured token retransmitted |
| 13 | B | Timing attack — side-channel not cryptanalytic |
| 14 | C | Key management = most common crypto failure |
| 15 | B | IV reuse in CBC — same plaintext → same ciphertext |
| 16 | D | ECB — identical blocks → identical ciphertext |
| 17 | C | MD5 fast + no salt → GPU cracking + rainbow tables |
| 18 | B | Nonce — Number Used Once → prevents replay |
| 19 | B | POODLE — SSL 3.0 CBC padding oracle (2014) |
| 20 | C | BEAST — TLS 1.0 predictable IV (2011) |
| 21 | B | CRIME — TLS compression length side-channel |
| 22 | C | FREAK — export RSA limited to 512-bit |
| 23 | B | Salt — unique per user, not secret |
| 24 | D | Argon2id — PHC winner 2015 |
| 25 | C | TLS_FALLBACK_SCSV — prevents downgrade attack |

---

## 📋 Topic Coverage Map

| Q | Concept Tested | Source |
|---|----------------|--------|
| 1 | DH is key exchange only — not encryption | Core |
| 2 | DH security = Discrete Logarithm Problem | Core |
| 3 | DH public value = gᵃ mod p calculation | Core |
| 4 | DHE = Ephemeral → Perfect Forward Secrecy | Core |
| 5 | Unauthenticated DH vulnerable to MITM | Core |
| 6 | TLS 1.3 mandates ECDHE | Core |
| 7 | Brute force attack definition | Core |
| 8 | AES-128 key space — brute force infeasible | Core |
| 9 | Rainbow table attack — pre-computed lookups | Core |
| 10 | Salt defeats rainbow tables | Core |
| 11 | Man-in-the-Middle attack | Core |
| 12 | Replay attack — captured token reuse | Core |
| 13 | Side-channel timing attack vs cryptanalytic | Core |
| 14 | Key management = primary real-world failure | Core |
| 15 | IV reuse in CBC mode — security consequence | Core |
| 16 | ECB mode — pattern leakage flaw | Core |
| 17 | MD5 unsalted — dual risk (speed + rainbow) | Core |
| 18 | Nonce definition and purpose | Core |
| 19 | POODLE — SSL 3.0, year, exploit | Extra Notes |
| 20 | BEAST — TLS 1.0, year, predictable IV | Extra Notes |
| 21 | CRIME — TLS compression length side-channel | Extra Notes |
| 22 | FREAK — export RSA 512-bit limit | Extra Notes |
| 23 | Salt purpose — unique not secret | Extra Notes |
| 24 | Argon2id — PHC winner, best practice | Extra Notes |
| 25 | TLS_FALLBACK_SCSV — downgrade prevention | Extra Notes |

---