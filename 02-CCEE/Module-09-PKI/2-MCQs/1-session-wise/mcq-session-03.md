# MCQ Session 03 — Cryptographic Fundamentals, Ciphers & Protocols

## 📑 Table of Contents
- [Instructions](#instructions)
- [MCQs 1–6 — Mathematical Foundations](#mcqs-16--mathematical-foundations)
- [MCQs 7–11 — One-Way Functions, Trapdoor, CSPRNG, Avalanche](#mcqs-711--one-way-functions-trapdoor-csprng-avalanche)
- [MCQs 12–17 — Classical Ciphers and OTP](#mcqs-1217--classical-ciphers-and-otp)
- [MCQs 18–22 — Asymmetric, Hybrid, Protocols](#mcqs-1822--asymmetric-hybrid-protocols)
- [MCQs 23–28 — Extra Notes: PFS, Birthday Attack, Feistel, Quantum, DLP](#mcqs-2328--extra-notes-pfs-birthday-attack-feistel-quantum-dlp)
- [Answer Key](#-answer-key--quick-reference)

---

## Instructions

- 28 MCQs — drawn from core syllabus AND 📌 Extra Notes of Session 03
- 4 options per question
- ✅ marks the correct answer
- Full explanation after every question — including **why each wrong option is wrong**
- Questions are deliberately tricky — one-word differences, formula traps, concept inversions

---

## MCQs 1–6 — Mathematical Foundations

---

**Q1. What is the result of 47 mod 8?**

- A) 5
- B) 6
- C) 7 ✅
- D) 3

> **Explanation:**
> - ✅ **C — 7:** 47 ÷ 8 = 5 remainder 7. So 47 mod 8 = 7. (8 × 5 = 40; 47 − 40 = 7)
> - ❌ **A — 5:** This is the quotient (how many times 8 fits into 47), not the remainder.
> - ❌ **B — 6:** Incorrect remainder. 8 × 5 = 40, and 47 − 40 = 7, not 6.
> - ❌ **D — 3:** 8 × 5 = 40 is the closest multiple below 47 — the remainder is 7, not 3.

---

**Q2. In RSA, the modulus n is computed as n = p × q where p and q are large primes. What is the mathematical reason that factoring n back into p and q is considered computationally infeasible for large values?**

- A) Addition of two primes is a one-way function — subtraction is infeasible
- B) The product of two large primes grows exponentially, requiring infinite memory to store
- C) No polynomial-time algorithm is known for factoring large integers — the best known algorithms run in sub-exponential but super-polynomial time ✅
- D) Prime numbers cannot be stored in binary — only decimal — making computation impossible

> **Explanation:**
> - ✅ **C:** The Integer Factorization Problem has no known polynomial-time solution for classical computers. The General Number Field Sieve (GNFS) — the best known algorithm — runs in sub-exponential time, making it infeasible for 2048-bit numbers.
> - ❌ **A:** This is fabricated. Addition of primes is not a one-way function in any meaningful sense — it is subtraction (n − p = q) that trivially gives the other factor once one is known. The hardness is in finding either factor in the first place.
> - ❌ **B:** Large integers do grow in size but modern computers can store numbers with thousands of digits. The infeasibility is computational — not a memory storage problem.
> - ❌ **D:** This is false. Prime numbers can be stored in binary exactly like any other integer. There is no decimal-only restriction.

---

**Q3. For 1000 users to communicate securely using symmetric encryption (each pair needing a unique key), how many total keys are required?**

- A) 1000
- B) 2000
- C) 499,500 ✅
- D) 1,000,000

> **Explanation:**
> - ✅ **C — 499,500:** The formula is n(n−1)/2. For n = 1000: 1000 × 999 / 2 = 499,500. Every pair of users needs one unique shared key.
> - ❌ **A — 1000:** This would be correct if each user needed only one key total — but every user needs a separate key with every other user.
> - ❌ **B — 2000:** This is 2n — has no mathematical basis in symmetric key pair counting.
> - ❌ **D — 1,000,000:** This would be n² = 1000² — double counts every pair (A→B and B→A counted separately). The correct formula divides by 2.

---

**Q4. Two numbers are described as coprime. What does this mean?**

- A) Both numbers are prime numbers
- B) Both numbers are even and divisible by 2
- C) Their Greatest Common Divisor (GCD) equals 1 ✅
- D) One number is a prime factor of the other

> **Explanation:**
> - ✅ **C:** Coprime (relatively prime) means GCD(a, b) = 1 — the two numbers share no common factors other than 1. Neither number needs to be prime itself.
> - ❌ **A:** Being individually prime is NOT required. For example, GCD(8, 15) = 1 — they are coprime even though neither is prime in relation to the other. And two primes are always coprime, but coprimality doesn't require both to be prime.
> - ❌ **B:** Even numbers are all divisible by 2, so any two even numbers have GCD ≥ 2 — they are never coprime with each other.
> - ❌ **D:** If one number is a prime factor of the other, their GCD > 1 — they would NOT be coprime.

---

**Q5. Which of the following correctly demonstrates the self-inverse property of XOR used in symmetric encryption?**

- A) A XOR 0 = 0
- B) A XOR A = 0, and therefore (A XOR K) XOR K = A ✅
- C) A XOR B = A + B when A and B are both 1
- D) A XOR 1 = 0 for any value of A

> **Explanation:**
> - ✅ **B:** The self-inverse property: A XOR A = 0. Applied to encryption: encrypt by XORing with K, decrypt by XORing with K again. (A XOR K) XOR K = A XOR (K XOR K) = A XOR 0 = A. This is the mathematical basis of XOR-based ciphers.
> - ❌ **A:** A XOR 0 = A (identity property), not 0. XOR with 0 leaves the value unchanged.
> - ❌ **C:** In binary XOR, 1 XOR 1 = 0 (not 2). XOR is not addition — it is bit-level exclusive or. 1 + 1 = 2 in arithmetic, but 1 XOR 1 = 0.
> - ❌ **D:** A XOR 1 = NOT A (bit flip) — it flips the bit. For A=0: 0 XOR 1 = 1. For A=1: 1 XOR 1 = 0. It does not always equal 0.

---

**Q6. GCD(48, 18) is calculated using the Euclidean Algorithm. What is the correct result?**

- A) 3
- B) 6 ✅
- C) 9
- D) 12

> **Explanation:**
> - ✅ **B — 6:** Euclidean Algorithm:
>   48 = 2 × 18 + 12
>   18 = 1 × 12 + 6
>   12 = 2 × 6 + 0 → remainder 0, so GCD = 6.
> - ❌ **A — 3:** 3 divides both 48 and 18, but 6 also does — GCD is the GREATEST common divisor, so 6 is correct.
> - ❌ **C — 9:** 9 divides 18 but does NOT divide 48 evenly (48 / 9 = 5.33...) — so 9 is not a common divisor at all.
> - ❌ **D — 12:** 12 divides 48 but does NOT divide 18 evenly (18 / 12 = 1.5) — not a common divisor.

---

## MCQs 7–11 — One-Way Functions, Trapdoor, CSPRNG, Avalanche

---

**Q7. What is the defining characteristic of a trapdoor function that distinguishes it from a general one-way function?**

- A) A trapdoor function can be computed in both directions without any additional information
- B) A trapdoor function is irreversible under all circumstances — including with a secret key
- C) A trapdoor function is easy to compute forward and infeasible to reverse, UNLESS a specific secret piece of information (the trapdoor) is known ✅
- D) A trapdoor function uses a symmetric key to make both computation directions equally fast

> **Explanation:**
> - ✅ **C:** A trapdoor function is a one-way function with a special property: given the trapdoor (secret), the inverse becomes easy. In asymmetric cryptography, the private key IS the trapdoor — it allows decryption of what the one-way (public key encryption) function computed.
> - ❌ **A:** If computable in both directions without additional information, it is not a one-way function at all — it would be a simple bijective function.
> - ❌ **B:** This describes a pure one-way function (like a hash). A trapdoor function is specifically designed to BE reversible — when the trapdoor is known.
> - ❌ **D:** Trapdoor functions are asymmetric by nature — the two directions are not equally fast even with the trapdoor. The trapdoor makes inversion feasible, not equally fast.

---

**Q8. In the context of asymmetric cryptography, what does the private key represent in terms of mathematical function theory?**

- A) The one-way function itself
- B) The trapdoor that makes the one-way function invertible ✅
- C) The public output of the trapdoor function
- D) A hash of the public key used to verify identity

> **Explanation:**
> - ✅ **B:** The private key is the trapdoor. Anyone can apply the one-way function (encrypt with the public key). Only the holder of the trapdoor (private key) can reverse it (decrypt). This is the mathematical model behind all public-key cryptography.
> - ❌ **A:** The one-way function is the encryption algorithm combined with the public key — not the private key itself.
> - ❌ **C:** The public output of the trapdoor function is the ciphertext — not the private key.
> - ❌ **D:** The private key is not a hash of the public key. They are generated together as a mathematically linked pair — deriving one from the other is computationally infeasible.

---

**Q9. A developer uses Java's `Math.random()` to generate AES encryption keys in a production application. What is the CRITICAL security flaw?**

- A) `Math.random()` only generates floating-point numbers — AES requires integers
- B) `Math.random()` is a PRNG — it is deterministic and predictable, making generated keys guessable ✅
- C) `Math.random()` generates numbers that are too large for AES key sizes
- D) AES does not accept programmatically generated keys — only hardware-generated keys

> **Explanation:**
> - ✅ **B:** `Math.random()` is a standard PRNG — it is deterministic, seeded from a predictable source, and does NOT meet cryptographic unpredictability requirements. An attacker who knows or guesses the seed can reproduce the entire key sequence. The correct choice is `SecureRandom` (Java's CSPRNG).
> - ❌ **A:** This is a distraction about data type — `Math.random()` output can be converted to byte arrays for key material. The type is not the issue; the predictability is.
> - ❌ **C:** `Math.random()` generates values in [0.0, 1.0) — these can be scaled to any size. Size is not the issue here.
> - ❌ **D:** AES absolutely accepts programmatically generated keys — the requirement is that they be generated by a CSPRNG, not any specific hardware device (though hardware TRNGs are ideal).

---

**Q10. Which Linux pseudo-file provides a Cryptographically Secure PRNG (CSPRNG) suitable for key generation and does NOT block when the entropy pool is low?**

- A) `/dev/random`
- B) `/dev/null`
- C) `/dev/urandom` ✅
- D) `/dev/zero`

> **Explanation:**
> - ✅ **C — `/dev/urandom`:** `/dev/urandom` uses a CSPRNG seeded from hardware entropy. It does not block — it generates output continuously using the seeded CSPRNG. For most cryptographic purposes (key generation, IV generation), `/dev/urandom` is the recommended source.
> - ❌ **A — `/dev/random`:** `/dev/random` blocks when the entropy pool is exhausted — waiting for more hardware entropy. This can cause application hangs. It is higher entropy but impractical for high-volume key generation.
> - ❌ **B — `/dev/null`:** `/dev/null` is a discard device — writing to it discards data, reading from it returns nothing. It has no randomness function.
> - ❌ **D — `/dev/zero`:** `/dev/zero` returns an infinite stream of null bytes (0x00) — not random at all. Using it as a key source would create a key of all zeros — completely insecure.

---

**Q11. An input message "SECURITY" is hashed with SHA-256, producing output H1. The message is then changed to "security" (lowercase 's') and hashed again, producing H2. What property of cryptographic hash functions does this demonstrate, and what is the expected relationship between H1 and H2?**

- A) Collision resistance — H1 and H2 will be identical
- B) Pre-image resistance — H2 cannot be reversed to find "security"
- C) Avalanche Effect — H1 and H2 will be completely different despite a one-character input change ✅
- D) Second pre-image resistance — finding H2 given H1 is computationally infeasible

> **Explanation:**
> - ✅ **C — Avalanche Effect:** A single character change (S → s) causes approximately 50% of the output bits to change unpredictably. The two hash outputs will look completely unrelated — this is the Avalanche Effect in action.
> - ❌ **A — Collision resistance:** Collision resistance means it is hard to find ANY two inputs with the same hash. Here we are not finding a collision — the two hashes will be completely different. The property shown is NOT collision resistance.
> - ❌ **B — Pre-image resistance:** Pre-image resistance means given H, it is hard to find the input. The scenario is about how outputs differ with small input changes — this is Avalanche, not pre-image resistance.
> - ❌ **D — Second pre-image resistance:** Second pre-image resistance means given input M1 and H(M1), it is hard to find M2 ≠ M1 such that H(M2) = H(M1). The scenario doesn't involve finding matching hashes — it is specifically demonstrating the sensitivity of hash output to input changes.

---

## MCQs 12–17 — Classical Ciphers and OTP

---

**Q12. Using a Caesar cipher with a key (shift) of 5, what is the encryption of the plaintext letter 'W'?**

- A) A
- B) B ✅
- C) C
- D) Z

> **Explanation:**
> - ✅ **B — B:** Using C = (P + K) mod 26. W is position 22 (A=0). (22 + 5) mod 26 = 27 mod 26 = 1. Position 1 = B. The alphabet wraps around after Z.
> - ❌ **A — A:** A is position 0. (22 + 5) mod 26 = 1, not 0.
> - ❌ **C — C:** C is position 2. (22 + 5) = 27, mod 26 = 1 (B), not 2 (C).
> - ❌ **D — Z:** Z would be position 25. Shift 5 from W would go W→X→Y→Z→A→B. That is 5 steps — landing on B (position 1 after wraparound via mod 26 arithmetic).

---

**Q13. What is the PRIMARY cryptographic weakness of all monoalphabetic substitution ciphers, including the Caesar cipher?**

- A) They use a key that is too short to provide security
- B) Each plaintext letter always maps to the same ciphertext letter — making frequency analysis trivial ✅
- C) They cannot handle uppercase and lowercase letters simultaneously
- D) They require both parties to meet in person to exchange the cipher alphabet

> **Explanation:**
> - ✅ **B:** In any monoalphabetic cipher, a given plaintext letter ALWAYS maps to the SAME ciphertext letter. This preserves the statistical frequency distribution of the language — an attacker simply finds the most frequent ciphertext letter, maps it to 'E' (most common in English), and the shift is revealed.
> - ❌ **A:** While Caesar's key space (25 shifts) is tiny, this describes a brute force vulnerability, not the primary structural weakness. The structural weakness is the one-to-one letter mapping that allows frequency analysis — even a monoalphabetic cipher with a 26! key space (random substitution alphabet) falls to frequency analysis.
> - ❌ **C:** Case handling is an implementation detail — not a cryptographic weakness. The cipher's fundamental flaw is statistical, not typographical.
> - ❌ **D:** Key exchange difficulty is a general problem with symmetric ciphers — not a specific weakness of monoalphabetic substitution. It applies equally to all symmetric systems.

---

**Q14. The Vigenère cipher uses the keyword "LEMON" to encrypt plaintext. The first five letters of the plaintext are "ATTACKAT". What shift is applied to the letter 'A' (first plaintext letter)?**

- A) 4 (corresponding to 'E')
- B) 11 (corresponding to 'L') ✅
- C) 13 (corresponding to 'M')
- D) 14 (corresponding to 'N')

> **Explanation:**
> - ✅ **B — 11 (L):** In the Vigenère cipher, the shift for each plaintext letter is determined by the corresponding key letter's position (A=0, B=1...L=11, E=4, M=12, O=14, N=13). The first key letter is 'L' = position 11. So the first plaintext letter 'A' is shifted by 11.
> A + L(11) = 0 + 11 = 11 → L (ciphertext).
> - ❌ **A — 4 (E):** 'E' is the second letter of "LEMON" — it applies to the SECOND plaintext letter 'T', not the first.
> - ❌ **C — 13 (M):** Wait — M is position 12, not 13. Also 'M' is the THIRD letter of "LEMON" — it applies to the third plaintext letter, not the first.
> - ❌ **D — 14 (O):** 'O' is position 14 and is the FOURTH letter of "LEMON" — it applies to the fourth plaintext letter 'A' (the second 'A' in ATTACK), not the first.

---

**Q15. What method, published in 1863, is used to determine the key length of a Vigenère cipher as the first step in breaking it?**

- A) Index of Coincidence (William Friedman)
- B) Frequency Analysis (Al-Kindi)
- C) Kasiski Test (Friedrich Kasiski) ✅
- D) Differential Cryptanalysis (Biham and Shamir)

> **Explanation:**
> - ✅ **C — Kasiski Test (1863):** Friedrich Kasiski published a method in 1863 to find the key length of a Vigenère cipher by locating repeated sequences in the ciphertext and measuring the distances between them. The GCD of those distances reveals the probable key length. Once the key length is known, the cipher splits into independent Caesar ciphers.
> - ❌ **A — Index of Coincidence:** William Friedman's Index of Coincidence (1920) is a statistical measure also used to estimate key length — but it was published in 1920, not 1863. Kasiski's test came first.
> - ❌ **B — Frequency Analysis (Al-Kindi):** Frequency Analysis (~800 AD) breaks monoalphabetic ciphers directly by letter frequency counting. It is used AFTER the key length is found to break each Caesar sub-stream — but it does not find the Vigenère key length itself.
> - ❌ **D — Differential Cryptanalysis:** Developed by Biham and Shamir in 1990 to attack modern block ciphers like DES. It has no application to classical ciphers like Vigenère.

---

**Q16. Claude Shannon proved that the Vernam Cipher (One-Time Pad) achieves perfect secrecy. Which of the following is NOT one of the four required conditions for this proof to hold?**

- A) The key must be at least as long as the message
- B) The key must be truly random
- C) The key must be kept completely secret
- D) The key must use AES encryption internally to generate the random stream ✅

> **Explanation:**
> - ✅ **D:** AES-based key generation is NOT one of OTP's four conditions. Shannon's four conditions are: (1) Key ≥ message length, (2) Key is truly random, (3) Key is used only once, (4) Key is kept secret. Using AES internally would make it a PRNG-based stream cipher — no longer a true OTP, and no longer provably perfect.
> - ❌ **A:** Key length ≥ message length IS a required condition — if the key is shorter and repeats, statistical patterns emerge.
> - ❌ **B:** True randomness IS required — a pseudo-random key is predictable and breaks the perfect secrecy proof.
> - ❌ **C:** Key secrecy IS required — obviously, if the key is known to the attacker, the cipher is broken immediately.

---

**Q17. During World War II, Soviet intelligence operators occasionally reused One-Time Pad key material under operational pressure. The US Venona project exploited this. What EXACTLY happens when an OTP key K is reused to encrypt two messages P1 and P2?**

- A) Both messages are decrypted immediately because OTP is not truly secure
- B) The attacker obtains C1 XOR C2 = P1 XOR P2 — the key cancels out, exposing the relationship between both plaintexts ✅
- C) The second message is automatically decrypted using the first message as a key
- D) A collision occurs between C1 and C2 — making both ciphertexts identical

> **Explanation:**
> - ✅ **B:** C1 = P1 XOR K and C2 = P2 XOR K. XOR-ing the two ciphertexts: C1 XOR C2 = (P1 XOR K) XOR (P2 XOR K) = P1 XOR P2 (key cancels because K XOR K = 0). The attacker now has P1 XOR P2 — from this, using known language statistics and the "crib-dragging" technique, both plaintexts can be recovered.
> - ❌ **A:** OTP is provably secure when used correctly — the vulnerability arises ONLY from key reuse. The Venona success was entirely due to reuse, not a flaw in the OTP system itself.
> - ❌ **C:** The first message does not become a key for the second. Both messages are XORed with the same key K — the relationship revealed is P1 XOR P2, not a direct decryption using P1 as a key.
> - ❌ **D:** The two ciphertexts will not be identical unless P1 = P2. C1 XOR C2 = P1 XOR P2 — if P1 ≠ P2, the ciphertexts differ. No collision occurs between ciphertexts.

---

## MCQs 18–22 — Asymmetric, Hybrid, Protocols

---

**Q18. Alice wants to send a confidential message to Bob such that ONLY Bob can read it. Which key operation is correct?**

- A) Alice encrypts with Alice's private key; Bob decrypts with Alice's public key
- B) Alice encrypts with Bob's private key; Bob decrypts with Bob's public key
- C) Alice encrypts with Bob's public key; Bob decrypts with Bob's private key ✅
- D) Alice encrypts with Alice's public key; Bob decrypts with Alice's private key

> **Explanation:**
> - ✅ **C:** For confidentiality — the sender encrypts with the RECEIVER'S public key. Only the receiver's private key can decrypt. Bob's public key is freely available to Alice. Bob's private key is known only to Bob — so only Bob can decrypt.
> - ❌ **A:** Encrypting with Alice's private key means ANYONE with Alice's public key can decrypt — this achieves authentication (digital signature), not confidentiality for Bob alone.
> - ❌ **B:** Bob's private key must never leave Bob's possession — Alice does not have access to it and must not. This option is both logically wrong and a key management catastrophe.
> - ❌ **D:** Alice's public key is publicly known — anyone could decrypt a message encrypted with Alice's public key. This provides zero confidentiality.

---

**Q19. Bob digitally signs a document. Which key does Bob use to create the signature, and which key does a verifier use to confirm it?**

- A) Bob signs with Bob's public key; verifier uses Bob's private key
- B) Bob signs with the verifier's private key; verifier uses the verifier's public key
- C) Bob signs with Bob's private key; verifier uses Bob's public key ✅
- D) Bob signs with a shared symmetric key; verifier uses the same symmetric key

> **Explanation:**
> - ✅ **C:** Digital signature = encrypt hash with PRIVATE key. Only Bob has his private key — so only Bob could have created that signature. Anyone with Bob's public key can decrypt the hash and verify it matches the message — confirming authenticity and non-repudiation.
> - ❌ **A:** Using the public key to sign means anyone could create the same signature — it proves nothing about the signer's identity. Public keys are not secrets.
> - ❌ **B:** The verifier's keys have no role in Bob's signing operation. Bob's identity is proven using Bob's own key pair.
> - ❌ **D:** A shared symmetric key for signing cannot provide non-repudiation — both parties know the key, so either could have created the signature. Non-repudiation requires the private key to be exclusively held by the signer.

---

**Q20. In the hybrid encryption model used by TLS, what is the SPECIFIC role of asymmetric encryption (RSA/ECDH)?**

- A) To encrypt the bulk application data because it is stronger than AES
- B) To encrypt the symmetric session key (or establish it) so it can be securely transmitted to the receiver ✅
- C) To replace symmetric encryption entirely once the connection is established
- D) To compress the data before the symmetric cipher encrypts it

> **Explanation:**
> - ✅ **B:** Asymmetric encryption in hybrid systems handles the KEY EXCHANGE problem — RSA encrypts the symmetric session key, or ECDH establishes a shared secret from which the session key is derived. The actual data is always encrypted with the fast symmetric cipher (AES).
> - ❌ **A:** Asymmetric encryption is approximately 1000× slower than AES for bulk data — using RSA to encrypt application data is completely impractical. This is precisely why hybrid encryption was invented.
> - ❌ **C:** Asymmetric encryption does NOT replace symmetric encryption after connection establishment. AES continues to encrypt all data throughout the session — asymmetric's role ends once the session key is established.
> - ❌ **D:** Compression is a separate operation unrelated to the asymmetric/symmetric role division. Neither RSA nor ECDH performs data compression.

---

**Q21. Which of the following correctly represents the FULL step-by-step order when Alice sends a signed and encrypted message to Bob using hybrid encryption?**

- A) Encrypt data with AES → Sign with Alice's public key → Encrypt AES key with Bob's public key
- B) Hash the message → Sign hash with Alice's private key → Encrypt message + signature with AES session key → Encrypt session key with Bob's public key ✅
- C) Hash the message → Encrypt hash with Bob's public key → Encrypt message with AES → Encrypt AES key with Alice's private key
- D) Sign with Bob's public key → Encrypt with AES → Send AES key in plaintext

> **Explanation:**
> - ✅ **B:** Correct full order: (1) Hash message → (2) Sign hash with Alice's PRIVATE key = Signature → (3) Encrypt (message + signature) with AES session key → (4) Encrypt AES session key with Bob's PUBLIC key → (5) Send encrypted bundle + encrypted key. This achieves both confidentiality (only Bob decrypts) and authentication/non-repudiation (Alice's private key proves origin).
> - ❌ **A:** Signing with Alice's PUBLIC key is wrong — the private key must sign. Also, the order places signing after bulk encryption which is incorrect in this model.
> - ❌ **C:** Encrypting the hash with BOB's public key would allow only Bob to verify the signature — but anyone should be able to verify Alice's signature using Alice's PUBLIC key. The hash is signed with Alice's private key, not Bob's public key.
> - ❌ **D:** Sending the AES session key in plaintext completely defeats the purpose of hybrid encryption — any eavesdropper can grab the key and decrypt everything. Bob's public key must protect the session key.

---

**Q22. Which TLS version first introduced mandatory Perfect Forward Secrecy and removed all cipher suites that do not support it?**

- A) TLS 1.0 (RFC 2246, 1999)
- B) TLS 1.1 (RFC 4346, 2006)
- C) TLS 1.2 (RFC 5246, 2008)
- D) TLS 1.3 (RFC 8446, 2018) ✅

> **Explanation:**
> - ✅ **D — TLS 1.3 (2018):** TLS 1.3 mandates PFS by removing all static RSA key exchange cipher suites. Only PFS-providing cipher suites (ECDHE, DHE) are allowed. It also removes weak algorithms (RC4, DES, 3DES, MD5, SHA-1).
> - ❌ **A — TLS 1.0:** TLS 1.0 did not require PFS — it supported both static RSA (no PFS) and DHE (PFS). PFS was optional.
> - ❌ **B — TLS 1.1:** TLS 1.1 added protections against CBC padding oracle attacks but did not mandate PFS. Static RSA key exchange remained available.
> - ❌ **C — TLS 1.2:** TLS 1.2 added AES-GCM and SHA-256 support and is significantly stronger than predecessors — but PFS is still OPTIONAL in TLS 1.2. Static RSA cipher suites are still permitted.

---

## MCQs 23–28 — Extra Notes: PFS, Birthday Attack, Feistel, Quantum, DLP

---

**Q23. An attacker has been recording all TLS-encrypted traffic between users and a server for two years. Today, the attacker successfully steals the server's long-term RSA private key. The server uses TLS 1.2 with static RSA key exchange (no PFS). What is the outcome for past recorded sessions?**

- A) Past sessions remain secure because the session keys were deleted from the server after each session
- B) Past sessions can be decrypted — the attacker uses the RSA private key to recover old session keys from the recorded handshakes ✅
- C) Past sessions remain secure because TLS 1.2 automatically implements Perfect Forward Secrecy
- D) Past sessions cannot be decrypted — RSA private keys only work on future traffic, not recorded ciphertext

> **Explanation:**
> - ✅ **B:** Without PFS, static RSA key exchange means: during each TLS handshake, the client encrypted the pre-master secret using the server's RSA public key. The server's RSA private key decrypts it. If an attacker has the private key AND the recorded handshakes, they can recover every pre-master secret → derive every session key → decrypt all past traffic. This is the "harvest now, decrypt later" threat model.
> - ❌ **A:** Session keys being deleted from the server is irrelevant — the attacker has the recorded ciphertext and the RSA private key that was used during the handshake. They can re-derive session keys from the recorded handshake data.
> - ❌ **C:** TLS 1.2 does NOT automatically implement PFS — PFS is optional. Static RSA cipher suites (e.g., TLS_RSA_WITH_AES_256_CBC_SHA) provide no PFS. Only DHE/ECDHE cipher suites in TLS 1.2 provide PFS.
> - ❌ **D:** RSA private keys work on ANY ciphertext encrypted with the corresponding public key — regardless of when the encryption occurred. Recorded TLS handshakes contain RSA-encrypted key material that remains decryptable years later.

---

**Q24. A hash function produces a 128-bit output. Using the Birthday Attack, approximately how many hash computations does an attacker need to find a collision?**

- A) 2¹²⁸
- B) 2⁶⁴ ✅
- C) 2³²
- D) 2¹⁰⁰

> **Explanation:**
> - ✅ **B — 2⁶⁴:** The Birthday Attack finds collisions in approximately 2^(n/2) operations, where n is the hash output length in bits. For 128-bit output: 2^(128/2) = 2⁶⁴. This is why MD5 (128-bit) is considered broken — 2⁶⁴ operations is feasible for well-funded attackers.
> - ❌ **A — 2¹²⁸:** This is the brute force space for finding a specific pre-image — not a collision. The Birthday Attack exploits probability mathematics to find ANY collision (any two inputs with the same output), which requires far fewer operations than finding a specific target.
> - ❌ **C — 2³²:** This would apply to a 64-bit hash (2^(64/2) = 2³²). For a 128-bit hash the birthday threshold is 2⁶⁴.
> - ❌ **D — 2¹⁰⁰:** 2¹⁰⁰ has no mathematical basis in the Birthday Attack formula. The formula is strictly 2^(n/2).

---

**Q25. Which of the following algorithms uses the Feistel cipher structure?**

- A) AES (Advanced Encryption Standard)
- B) RSA (Rivest–Shamir–Adleman)
- C) DES (Data Encryption Standard) ✅
- D) ECC (Elliptic Curve Cryptography)

> **Explanation:**
> - ✅ **C — DES:** DES is the textbook example of a Feistel cipher — it uses 16 rounds of the Feistel structure, splitting the 64-bit block into two 32-bit halves and applying a round function F with subkeys.
> - ❌ **A — AES:** AES does NOT use Feistel structure — it uses a **Substitution-Permutation Network (SPN)**. This is one of the most commonly tested distinctions. AES operations (SubBytes, ShiftRows, MixColumns, AddRoundKey) are the SPN structure, not Feistel halves.
> - ❌ **B — RSA:** RSA is an asymmetric algorithm based on modular exponentiation and integer factorization. It has no block cipher structure at all — Feistel is a block cipher structural concept.
> - ❌ **D — ECC:** ECC is an asymmetric algorithm based on elliptic curve mathematics. It is not a block cipher and has no Feistel structure.

---

**Q26. What is the key structural property of the Feistel cipher that makes hardware implementation particularly efficient?**

- A) It uses AES's SubBytes operation which is implemented in all modern CPUs
- B) The same circuit/structure is used for both encryption and decryption — only the subkey order is reversed ✅
- C) It only requires XOR gates and no substitution boxes
- D) It splits the data into 4 equal quarters instead of 2 halves — enabling parallel processing

> **Explanation:**
> - ✅ **B:** The Feistel structure's elegant property is that the same hardware/software implementation performs both encryption and decryption — decryption simply applies the round subkeys in reverse order. This halves the hardware cost for devices that need both operations.
> - ❌ **A:** AES's SubBytes is specific to AES (SPN structure) — not part of the Feistel design. Feistel's round function F can be any function — it doesn't need to be SubBytes.
> - ❌ **C:** Feistel ciphers absolutely can and do use substitution boxes (S-boxes). DES, for example, uses 8 S-boxes in its F function. XOR is used in the Feistel round (L[i] XOR F(R[i], K[i])), but S-boxes are a key component of the F function.
> - ❌ **D:** Feistel structure splits data into exactly 2 halves (Left and Right) — not 4 quarters. The 2-half structure is definitional to Feistel.

---

**Q27. Which quantum computing algorithm poses the PRIMARY threat to RSA, Diffie-Hellman, and ECC, and what mathematical problems does it solve efficiently?**

- A) Grover's Algorithm — it searches unstructured databases and breaks symmetric ciphers
- B) Shor's Algorithm — it solves integer factorization and discrete logarithm problems in polynomial time ✅
- C) Grover's Algorithm — it solves integer factorization and discrete logarithm problems
- D) Shor's Algorithm — it searches unstructured databases to find collision attacks on hash functions

> **Explanation:**
> - ✅ **B — Shor's Algorithm:** Shor's Algorithm (Peter Shor, 1994) runs on a quantum computer and solves both the **Integer Factorization Problem** (breaks RSA) and the **Discrete Logarithm Problem** (breaks DH, DSA, ElGamal, ECC) in polynomial time — rendering all these algorithms insecure against a sufficiently powerful quantum computer.
> - ❌ **A — Grover's Algorithm:** Grover's Algorithm speeds up unstructured search — it DOES threaten symmetric ciphers (halves effective key length) and hash functions — but NOT RSA/DH/ECC. Those are broken by Shor's, not Grover's.
> - ❌ **C:** This assigns Shor's problems to Grover's name — the problem descriptions are correct but the attribution is wrong. Grover's algorithm is for unstructured search, not integer factorization or DLP.
> - ❌ **D:** This assigns Grover's capability (unstructured search/collision attacks) to Shor's name — the attribution is completely inverted. Shor's is for factoring and DLP; Grover's is for search problems.

---

**Q28. NIST finalized its first set of Post-Quantum Cryptography (PQC) standards in 2024. Which of the following is a NIST-standardized PQC algorithm intended for KEY ENCAPSULATION (key exchange)?**

- A) CRYSTALS-Dilithium
- B) FALCON
- C) SPHINCS+
- D) CRYSTALS-Kyber ✅

> **Explanation:**
> - ✅ **D — CRYSTALS-Kyber:** CRYSTALS-Kyber is the NIST-standardized Key Encapsulation Mechanism (KEM) — it replaces RSA and ECDH for key exchange. It is based on the hardness of lattice problems (Module-LWE — Module Learning With Errors).
> - ❌ **A — CRYSTALS-Dilithium:** Dilithium is a **Digital Signature** algorithm (not key encapsulation) — it replaces ECDSA/RSA signatures. Also lattice-based, but for signing, not key exchange.
> - ❌ **B — FALCON:** FALCON is also a **Digital Signature** algorithm — lattice-based, designed for use cases requiring compact signatures (e.g., constrained devices). Not for key encapsulation.
> - ❌ **C — SPHINCS+:** SPHINCS+ is a **Digital Signature** algorithm based on **hash functions** (not lattice problems) — making it more conservative but larger in signature size. Not for key encapsulation.

> [!TIP]
> Memory hook for NIST PQC roles:
> - **Kyber** = **K**ey encapsulation (**K** for Key)
> - **Dilithium, FALCON, SPHINCS+** = Digital **S**ignatures

---

## 📊 Answer Key — Quick Reference

| Q | Answer | Topic |
|---|--------|-------|
| 1 | C | Modular arithmetic — 47 mod 8 |
| 2 | C | Integer factorization hardness — RSA |
| 3 | C | Symmetric key count — n(n-1)/2 formula |
| 4 | C | Coprime / GCD = 1 |
| 5 | B | XOR self-inverse property |
| 6 | B | Euclidean Algorithm — GCD(48,18) = 6 |
| 7 | C | Trapdoor function definition |
| 8 | B | Private key = trapdoor |
| 9 | B | PRNG vs CSPRNG — Java Math.random() flaw |
| 10 | C | `/dev/urandom` = CSPRNG, non-blocking |
| 11 | C | Avalanche Effect — SHA-256 |
| 12 | B | Caesar cipher — 'W' + shift 5 = 'B' |
| 13 | B | Monoalphabetic weakness — same letter mapping |
| 14 | B | Vigenère — first key letter 'L' = shift 11 |
| 15 | C | Kasiski Test — 1863 |
| 16 | D | OTP conditions — AES not a condition |
| 17 | B | OTP key reuse — C1 XOR C2 = P1 XOR P2 |
| 18 | C | Asymmetric — encrypt with receiver's public key |
| 19 | C | Digital signature — sign with private, verify with public |
| 20 | B | Hybrid encryption — asymmetric encrypts session key |
| 21 | B | Full sign + encrypt flow order |
| 22 | D | TLS 1.3 — mandatory PFS |
| 23 | B | No PFS + stolen RSA key → all past sessions decryptable |
| 24 | B | Birthday attack — 2^(n/2) = 2⁶⁴ for 128-bit hash |
| 25 | C | DES uses Feistel; AES does NOT |
| 26 | B | Feistel — same structure for encrypt/decrypt |
| 27 | B | Shor's Algorithm — RSA/DH/ECC threat |
| 28 | D | CRYSTALS-Kyber = NIST PQC key encapsulation |

---