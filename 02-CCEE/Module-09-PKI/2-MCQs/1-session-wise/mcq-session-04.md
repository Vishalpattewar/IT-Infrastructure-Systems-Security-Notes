# MCQ Session 04 — Symmetric & Asymmetric Algorithms

## 📑 Table of Contents
- [Instructions](#instructions)
- [MCQs 1–7 — DES and 3DES](#mcqs-17--des-and-3des)
- [MCQs 8–14 — AES](#mcqs-814--aes)
- [MCQs 15–17 — RC5](#mcqs-1517--rc5)
- [MCQs 18–23 — RSA](#mcqs-1823--rsa)
- [MCQs 24–28 — ECC](#mcqs-2428--ecc)
- [MCQs 29–30 — Extra Notes: Attacks and Standards](#mcqs-2930--extra-notes-attacks-and-standards)
- [Answer Key](#-answer-key--quick-reference)

---

## Instructions

- 30 MCQs — drawn from core syllabus AND 📌 Extra Notes of Session 04
- 4 options per question
- ✅ marks the correct answer
- Full explanation after every question — including **why each wrong option is wrong**
- Deliberately tricky — number traps, structure inversions, formula tests

---

## MCQs 1–7 — DES and 3DES

---

**Q1. What is the effective key length of DES, and why does it differ from the actual key input size?**

- A) 64-bit effective — all 64 bits are used for encryption
- B) 56-bit effective — 8 bits are parity bits used for error checking, not encryption ✅
- C) 48-bit effective — 16 bits are used for the initial permutation only
- D) 52-bit effective — 12 bits are discarded during the PC-1 permutation step

> **Explanation:**
> - ✅ **B — 56-bit effective:** DES accepts a 64-bit key input, but every 8th bit (bits 8, 16, 24, 32, 40, 48, 56, 64) is a parity bit used for error detection — not for encryption. The PC-1 step in the key schedule drops all 8 parity bits, leaving exactly 56 bits of actual key material. The security of DES is therefore only 2⁵⁶.
> - ❌ **A:** "All 64 bits are used" is wrong — the 8 parity bits are explicitly removed by PC-1 before any encryption occurs.
> - ❌ **C:** 48-bit is wrong. 48 bits is the size of each **round subkey**, not the effective key length. The key schedule produces 16 × 48-bit subkeys from the 56-bit key.
> - ❌ **D:** 52-bit is a fabricated number. PC-1 drops exactly 8 bits (the parity bits) — leaving 56 bits, not 52.

---

**Q2. In DES, the 64-bit plaintext block is processed through 16 Feistel rounds. Before these rounds begin, which operation is applied to the plaintext?**

- A) S-Box substitution using the first round key
- B) PC-1 permutation to remove parity bits
- C) Initial Permutation (IP) — a fixed bit rearrangement ✅
- D) XOR with the 64-bit master key

> **Explanation:**
> - ✅ **C — Initial Permutation (IP):** Before the 16 Feistel rounds begin, the 64-bit plaintext undergoes a fixed Initial Permutation (IP) that rearranges the bit positions. It has no cryptographic security value — it is a historical artifact from the original IBM hardware design — but it is part of the DES specification.
> - ❌ **A:** S-Box substitution is part of the Feistel round function F — it occurs inside each round, not before all rounds.
> - ❌ **B:** PC-1 is applied to the **key**, not the plaintext. It removes parity bits from the 64-bit key to produce the 56-bit key used in the key schedule.
> - ❌ **D:** The 64-bit master key is never XORed directly with the plaintext. The key is used indirectly through the key schedule to generate 48-bit round subkeys, which are XORed inside the round function F.

---

**Q3. Which component of the DES round function F provides non-linearity and is considered the ONLY source of confusion in DES?**

- A) Expansion permutation E (32-bit → 48-bit)
- B) XOR with the round subkey Kᵢ
- C) The 8 S-Boxes (Substitution Boxes) ✅
- D) The final permutation P after S-Boxes

> **Explanation:**
> - ✅ **C — The 8 S-Boxes:** The S-Boxes are the only non-linear component in DES. They implement Shannon's Confusion — making the relationship between key and ciphertext complex. Each S-Box maps a 6-bit input to a 4-bit output using a non-linear lookup table. Without S-Boxes, DES would be entirely linear and breakable trivially.
> - ❌ **A:** The Expansion E function is a linear operation — it simply copies and repeats certain bits to expand 32 bits to 48 bits. Linear operations provide no security on their own.
> - ❌ **B:** XOR with the round subkey is a linear operation — XOR is a bitwise linear function. It provides key mixing but no non-linearity.
> - ❌ **D:** The final permutation P (after S-Boxes) is a linear bit rearrangement — it contributes to Diffusion but is not non-linear. S-Boxes are the sole source of non-linearity.

---

**Q4. In Triple DES (3DES), the standard operation sequence is Encrypt-Decrypt-Encrypt (E-D-E) rather than Encrypt-Encrypt-Encrypt (E-E-E). What is the PRIMARY reason for the E-D-E design?**

- A) E-D-E is faster than E-E-E because the Decrypt step is cheaper computationally
- B) E-D-E provides backward compatibility with single DES when all three keys are equal ✅
- C) E-D-E provides triple the security of E-E-E due to the mixing of encrypt and decrypt operations
- D) E-D-E was chosen because E-E-E with three keys is vulnerable to differential cryptanalysis

> **Explanation:**
> - ✅ **B — Backward compatibility:** When K1 = K2 = K3 in E-D-E: Encrypt(K) → Decrypt(K) → Encrypt(K) = the middle Decrypt undoes the first Encrypt, leaving only the final Encrypt(K) — which is equivalent to single DES. This allowed organizations to migrate to 3DES-capable hardware without immediately changing all their existing DES keys. E-E-E with K1=K2=K3 would compute DES three times — still single DES but with no backward compat benefit.
> - ❌ **A:** The Decrypt step in DES is essentially the same computational cost as Encrypt (same Feistel structure, subkeys in reverse order). There is no speed advantage.
> - ❌ **C:** E-D-E does NOT triple the security. With 2 keys, effective security is only 112 bits (not 168). The E-D-E pattern's security benefit is resisting Meet-in-the-Middle attacks, not tripling security.
> - ❌ **D:** Differential cryptanalysis applies to the S-Box structure — using E-E-E vs E-D-E has no meaningful difference in resistance to differential cryptanalysis. The reason is specifically backward compatibility.

---

**Q5. The Sweet32 attack (2016) affected Triple DES (3DES). What is the fundamental weakness that Sweet32 exploits?**

- A) 3DES uses a 56-bit key that can be brute-forced with modern hardware
- B) 3DES S-Boxes were found to have a backdoor inserted by the NSA
- C) 3DES uses a 64-bit block size — birthday attack finds collisions after approximately 2³² blocks of data ✅
- D) 3DES key schedule generates weak subkeys that repeat after 32 rounds

> **Explanation:**
> - ✅ **C — 64-bit block size / Birthday attack:** Sweet32 is a birthday attack against 3DES's 64-bit block size. After encrypting approximately 2³² blocks (~32 GB of data) with the same key, the probability of two blocks having identical ciphertext exceeds 50% (birthday paradox). A collision reveals the XOR of the two corresponding plaintexts. This is why 128-bit block sizes (AES) are essential for modern ciphers.
> - ❌ **A:** 3DES with 3 independent keys has a 168-bit key — brute force is not feasible. The weakness is the block size, not the key size.
> - ❌ **B:** There is no confirmed NSA backdoor in DES or 3DES S-Boxes. Later analysis showed the S-Box design was actually strengthened against differential cryptanalysis.
> - ❌ **D:** The DES key schedule does not produce repeating subkeys after 32 rounds. It generates 16 unique 48-bit subkeys per DES instance — three DES applications in 3DES produce 48 unique subkeys total.

---

**Q6. In the Meet-in-the-Middle attack against 2DES, what is the EFFECTIVE security level achieved — and why is it not the expected 112 bits?**

- A) 112-bit security — Meet-in-the-Middle doesn't apply to 2DES
- B) 56-bit security — 2DES is identical to single DES
- C) Approximately 57-bit security — MitM requires 2×2⁵⁶ operations and 2⁵⁶ storage, barely more than DES ✅
- D) 84-bit security — MitM reduces security to exactly 3/4 of the combined key length

> **Explanation:**
> - ✅ **C — ~57-bit effective security:** MitM works by encrypting from the left (all 2⁵⁶ K1 values → build lookup table) and decrypting from the right (all 2⁵⁶ K2 values → find match in table). Total work = 2×2⁵⁶ ≈ 2⁵⁷ operations with 2⁵⁶ storage. This is barely better than brute-forcing single 56-bit DES. The expected 112-bit security is completely negated.
> - ❌ **A:** MitM absolutely applies to 2DES — this is precisely why 2DES was never standardized. Dismissing MitM here is factually wrong.
> - ❌ **B:** 2DES is not identical to single DES — single DES has 2⁵⁶ brute-force cost; 2DES MitM has 2⁵⁷ cost. Marginally better, but not equivalent.
> - ❌ **D:** 84-bit (3/4 of 112) is a fabricated number with no mathematical basis in the MitM attack model.

---

**Q7. NIST deprecated 3DES in which year, and what was the primary replacement standard?**

- A) NIST deprecated 3DES in 2005 — replaced by RC5
- B) NIST deprecated 3DES in 2017 and disallowed it for new applications after 2023 — replaced by AES ✅
- C) NIST deprecated 3DES in 2001 — simultaneously with adopting AES
- D) NIST deprecated 3DES in 2015 — replaced by ChaCha20

> **Explanation:**
> - ✅ **B:** NIST SP 800-131A Rev. 2 deprecated 3DES (TDEA) in 2017 and disallowed it for new applications after 2023. The replacement is AES (FIPS 197, adopted 2001). 3DES continued in legacy systems (banking, SWIFT) between 2001 and 2023.
> - ❌ **A:** 2005 was when DES (single) was officially withdrawn — not 3DES. RC5 was never a NIST replacement standard.
> - ❌ **C:** AES was adopted in 2001, but 3DES deprecation happened years later — not simultaneously. 2001 is the AES adoption date, not 3DES deprecation date.
> - ❌ **D:** 2015 is incorrect for 3DES. ChaCha20 is a stream cipher — it does not replace 3DES as a general symmetric block cipher standard.

---

## MCQs 8–14 — AES

---

**Q8. AES-256 is selected for encrypting a large dataset. What is the block size used for this encryption?**

- A) 256 bits — matching the key size
- B) 192 bits — midpoint between 128-bit and 256-bit
- C) 128 bits ✅
- D) 512 bits — doubled for higher security

> **Explanation:**
> - ✅ **C — 128 bits:** AES ALWAYS uses a 128-bit block size regardless of key size. AES-128, AES-192, and AES-256 all operate on 128-bit blocks. Only the key length and number of rounds change between variants.
> - ❌ **A:** This is the most common MCQ trap — "AES-256 must use 256-bit blocks." The 256 in AES-256 refers to the KEY size only. Block size is fixed at 128 bits for all AES variants by the FIPS 197 specification.
> - ❌ **B:** 192-bit blocks do not exist in AES. The original Rijndael algorithm supported variable block sizes (128/192/256), but NIST standardized AES with ONLY 128-bit blocks.
> - ❌ **D:** 512-bit blocks do not exist in AES. This would describe a completely different cipher.

---

**Q9. How many rounds does AES-192 perform during encryption?**

- A) 10
- B) 12 ✅
- C) 14
- D) 16

> **Explanation:**
> - ✅ **B — 12 rounds:** AES round counts: AES-128 = 10 rounds, AES-192 = 12 rounds, AES-256 = 14 rounds. The pattern: larger key → more rounds.
> - ❌ **A — 10:** This is AES-128's round count — not AES-192.
> - ❌ **C — 14:** This is AES-256's round count — not AES-192.
> - ❌ **D — 16:** 16 rounds is DES's round count — not any AES variant. A classic cross-cipher trap.

---

**Q10. In AES, which operation is deliberately OMITTED from the FINAL round, and why?**

- A) AddRoundKey — the key should not be mixed in the final round to prevent reverse engineering
- B) SubBytes — the S-Box is only needed for intermediate rounds to build up confusion
- C) ShiftRows — the final shift would undo the previous round's shift
- D) MixColumns — it provides no additional security in the final round and complicates the inverse ✅

> **Explanation:**
> - ✅ **D — MixColumns:** MixColumns is skipped in the final AES round. Adding MixColumns in the last round would not increase security (there is no subsequent SubBytes/ShiftRows to benefit from the mixing), but it would complicate the decryption inverse operation needlessly. The designers of Rijndael made this deliberate optimization.
> - ❌ **A:** AddRoundKey is the LAST operation in every round including the final round — and also the FIRST operation (initial round). It is never omitted. Without AddRoundKey in the final round, the output would not be key-dependent.
> - ❌ **B:** SubBytes IS present in the final round — substitution continues to provide confusion in the last round.
> - ❌ **C:** ShiftRows IS present in the final round — it provides byte-level diffusion and is maintained. Only MixColumns is removed.

---

**Q11. Which AES operation implements Shannon's property of CONFUSION, and what mathematical structure does it use?**

- A) ShiftRows — cyclic row shifts using modular arithmetic
- B) MixColumns — polynomial multiplication in GF(2⁸)
- C) AddRoundKey — XOR with round key provides key-dependent confusion
- D) SubBytes — non-linear S-Box lookup using multiplicative inverse in GF(2⁸) ✅

> **Explanation:**
> - ✅ **D — SubBytes:** SubBytes replaces each byte with its multiplicative inverse in GF(2⁸) followed by an affine transformation — this creates a highly non-linear substitution. Non-linearity = Confusion (Shannon). It makes the relationship between the key and ciphertext complex and non-predictable.
> - ❌ **A:** ShiftRows is a linear byte rearrangement — it implements Diffusion, not Confusion. It spreads bytes across columns.
> - ❌ **B:** MixColumns is a linear operation (polynomial multiplication in GF(2⁸) is linear) — it also implements Diffusion (maximum mixing within each column), not Confusion.
> - ❌ **C:** AddRoundKey provides key mixing via XOR — XOR is linear. It ensures the output depends on the key but does not provide the non-linear Confusion that SubBytes provides.

---

**Q12. AES key expansion for AES-128 generates how many round keys in total (including the initial round key)?**

- A) 10
- B) 11 ✅
- C) 12
- D) 16

> **Explanation:**
> - ✅ **B — 11:** AES-128 performs 10 rounds, but requires one round key for the **initial AddRoundKey** (before Round 1) PLUS one round key for each of the 10 rounds = **11 round keys total** (each 128 bits = 1408 bits total).
> - ❌ **A — 10:** 10 is the number of ROUNDS — not the number of round keys. The initial AddRoundKey (Round 0) needs its own key — making it 10 + 1 = 11.
> - ❌ **C — 12:** 12+1 = 13 round keys applies to AES-192 (12 rounds + 1 initial = 13 total). 11 is correct for AES-128.
> - ❌ **D — 16:** 16 is DES's number of rounds. For AES-128, the correct answer is 11 round keys.

---

**Q13. AES was selected from a 5-year open competition. Which algorithm was the RUNNER-UP known for being the most conservative/secure design — though slower?**

- A) Twofish
- B) RC6
- C) MARS
- D) Serpent ✅

> **Explanation:**
> - ✅ **D — Serpent:** Serpent (by Anderson, Biham, and Knudsen) was the runner-up in the AES competition. It was widely considered the most conservatively secure design — using 32 rounds compared to Rijndael's 10. However, it was significantly slower than Rijndael, which cost it the selection. Many cryptographers believe Serpent has a higher security margin than AES.
> - ❌ **A — Twofish:** Twofish (Bruce Schneier et al.) was another finalist — it was a strong, well-designed Feistel cipher but not the runner-up known specifically for conservative security. Twofish came 3rd in the final evaluation.
> - ❌ **B — RC6:** RC6 (Ron Rivest, RSA Security) was a Feistel-like finalist — not known as the most conservative design. It was efficient but had a more complex key schedule.
> - ❌ **C — MARS:** MARS (IBM) was a finalist with a complex, heterogeneous structure — not recognized as the most conservative. It had mixed security evaluations.

---

**Q14. A developer needs to encrypt data where BOTH confidentiality and message integrity must be guaranteed simultaneously by the encryption operation. Which AES mode should be chosen?**

- A) AES-CBC (Cipher Block Chaining)
- B) AES-ECB (Electronic Codebook)
- C) AES-CTR (Counter Mode)
- D) AES-GCM (Galois/Counter Mode) ✅

> **Explanation:**
> - ✅ **D — AES-GCM:** GCM (Galois/Counter Mode) is an Authenticated Encryption with Associated Data (AEAD) mode — it provides both confidentiality (via CTR encryption) and integrity/authentication (via GMAC, a Galois Message Authentication Code) simultaneously in a single operation. It is the standard in TLS 1.3.
> - ❌ **A — AES-CBC:** CBC provides confidentiality only — no built-in integrity. A separate MAC (e.g., HMAC) must be added to detect tampering. CBC alone does not detect if ciphertext has been modified.
> - ❌ **B — AES-ECB:** ECB provides neither security nor integrity — it is fundamentally broken (identical plaintext blocks produce identical ciphertext). It should never be used.
> - ❌ **C — AES-CTR:** CTR mode provides confidentiality (and is parallelizable) — but like CBC, it has no built-in authentication. Tampering with CTR ciphertext produces predictable plaintext changes that go undetected.

---

## MCQs 15–17 — RC5

---

**Q15. RC5 is described as RC5-w/r/b. In the standard reference configuration RC5-32/12/16, what do the three parameters represent respectively?**

- A) 32-bit key, 12 S-Boxes, 16 rounds
- B) 32-bit word size (64-bit block), 12 rounds, 16-byte (128-bit) key ✅
- C) 32-bit block size, 12-bit key segment, 16 initialization rounds
- D) 32 rounds, 12-bit key, 16-byte initialization vector

> **Explanation:**
> - ✅ **B — RC5-w/r/b:** w = word size in bits (32 → block = 2w = 64-bit), r = number of rounds (12), b = key length in bytes (16 bytes = 128 bits). RC5-32/12/16 is therefore: 64-bit block, 12 rounds, 128-bit key.
> - ❌ **A:** The first parameter (w) is word size — not key size. RC5 key size is the third parameter (b), not the first.
> - ❌ **C:** 32-bit block size is wrong — w=32 means 32-bit WORD, making the BLOCK 2×32 = 64 bits. A 12-bit key segment has no meaning in this context.
> - ❌ **D:** The parameters are in order w/r/b (word/rounds/key bytes) — 32 rounds would put rounds first, contradicting the notation. The format is fixed: word size first, rounds second, key bytes third.

---

**Q16. What is the DISTINCTIVE feature of RC5 that was novel at the time of its design in 1994?**

- A) RC5 was the first cipher to use S-Boxes for non-linear substitution
- B) RC5 was the first cipher designed exclusively for 64-bit processors
- C) RC5 uses data-dependent rotations — the rotation amount in each round depends on the actual data being processed ✅
- D) RC5 introduced the concept of key whitening — XORing the data with the key before and after all rounds

> **Explanation:**
> - ✅ **C — Data-dependent rotations:** RC5's defining innovation was its use of variable rotations where the amount of rotation in each round is determined by the actual data values being encrypted. This makes algebraic cryptanalysis and differential/linear attacks significantly harder because the operations are data-dependent and therefore unpredictable from the key alone.
> - ❌ **A:** S-Boxes were used in DES (1977) — 17 years before RC5. RC5 actually uses NO S-Boxes — it operates only with XOR, addition, and rotation. S-Box introduction as a novel feature applies to DES, not RC5.
> - ❌ **B:** RC5 was not designed exclusively for 64-bit processors — its variable word size means it can run on 16-bit, 32-bit, or 64-bit architectures. Platform exclusivity was never part of its design.
> - ❌ **D:** Key whitening (XOR before and after rounds) is associated with other ciphers like DESX and Twofish — not a distinctive feature of RC5. RC5's novelty is specifically data-dependent rotations.

---

**Q17. RC5 uses only three primitive operations. Which set correctly identifies all three?**

- A) Substitution (S-Box), Permutation, XOR
- B) XOR, Addition modulo 2^w, Data-dependent left rotation ✅
- C) XOR, Multiplication modulo 2^w, Fixed rotation
- D) Addition modulo 2^w, Subtraction, Bitwise AND

> **Explanation:**
> - ✅ **B:** RC5's design philosophy was simplicity and elegance — using ONLY three operations: XOR (⊕), modular addition (+), and data-dependent left rotation (<<<). These three primitives together provide the confusion and diffusion needed for security. This is the ARX (Add-Rotate-XOR) design paradigm.
> - ❌ **A:** RC5 uses NO S-Boxes and no permutation tables — these are DES/AES operations. RC5's simplicity explicitly avoids lookup tables.
> - ❌ **C:** RC5 uses data-dependent rotation (variable), not fixed rotation. Fixed rotation would be much weaker. Multiplication is used in RC6 (not RC5).
> - ❌ **D:** Subtraction is the inverse of modular addition and is used in RC5 decryption — but it is not listed as a separate primitive. Bitwise AND is not an RC5 operation at all.

---

## MCQs 18–23 — RSA

---

**Q18. In RSA key generation, p = 11 and q = 13 are chosen. What is the value of Euler's totient φ(n)?**

- A) 143
- B) 132
- C) 120 ✅
- D) 110

> **Explanation:**
> - ✅ **C — 120:** φ(n) = (p-1)(q-1) = (11-1)(13-1) = 10 × 12 = 120.
> - ❌ **A — 143:** This is n = p × q = 11 × 13 = 143. Confusing n with φ(n) is the trap.
> - ❌ **B — 132:** 132 = 11 × 12 = (p)(q-1) — this uses p directly instead of (p-1). Both terms must be decremented.
> - ❌ **D — 110:** 110 = 10 × 11 = (p-1)(q) — this uses q directly instead of (q-1). Same partial error as option B.

---

**Q19. Given RSA parameters p=11, q=13, e=7. What is the private exponent d?**

- A) 7
- B) 103 ✅
- C) 17
- D) 77

> **Explanation:**
> - ✅ **B — 103:** d = e⁻¹ mod φ(n) = 7⁻¹ mod 120. We need d such that 7d ≡ 1 (mod 120). Testing: 7 × 103 = 721 = 6 × 120 + 1 = 721. So 721 mod 120 = 1 ✅. Therefore d = 103.
> - ❌ **A — 7:** d = e = 7 would mean the public and private keys are identical — this would completely break RSA. d is computed as the modular inverse of e, which is a different value.
> - ❌ **C — 17:** 7 × 17 = 119 = 120 - 1 ≡ -1 (mod 120). This gives -1, not 1. Close trap.
> - ❌ **D — 77:** 7 × 77 = 539 = 4 × 120 + 59. 539 mod 120 = 59 ≠ 1. Not the modular inverse.

---

**Q20. Using the RSA public key (e=7, n=143) from Q18-Q19, encrypt the plaintext message M=2. What is the ciphertext C?**

- A) 14
- B) 128 ✅
- C) 107
- D) 42

> **Explanation:**
> - ✅ **B — 128:** C = Mᵉ mod n = 2⁷ mod 143 = 128 mod 143 = 128. (2⁷ = 128, and since 128 < 143, no modular reduction needed.)
> - ❌ **A — 14:** 14 = 2 × 7 — this is M × e (simple multiplication), not Mᵉ (exponentiation). RSA uses modular exponentiation, not multiplication.
> - ❌ **C — 107:** 2⁷ = 128, not 107. This is an arithmetic error.
> - ❌ **D — 42:** 42 has no basis in 2⁷ mod 143. Possibly confused with other parameters.

---

**Q21. Why is the RSA public exponent e almost universally set to 65537 in practice?**

- A) 65537 is the largest prime smaller than 2¹⁶ — maximizing security
- B) 65537 = 2¹⁶ + 1 is a Fermat prime with only two set bits in binary — providing fast exponentiation while being large enough to avoid small-exponent attacks ✅
- C) 65537 was mandated by NIST as the only permissible RSA public exponent in FIPS 186
- D) 65537 ensures that gcd(e, φ(n)) = 1 for all possible RSA key pairs

> **Explanation:**
> - ✅ **B:** 65537 = 2¹⁶ + 1 = Fermat prime F₄. In binary: 10000000000000001 — only 2 set bits. The square-and-multiply algorithm for computing Mᵉ needs only 16 squarings + 1 multiplication = 17 operations total — extremely fast. It is large enough to avoid small-exponent attacks (e=3 is vulnerable with small messages). And it is coprime with φ(n) for virtually all practical RSA key pairs.
> - ❌ **A:** 65537 is NOT the largest prime below 2¹⁶. It is 2¹⁶ + 1 = 65537, which is just above 2¹⁶ (= 65536). The characterization "largest prime smaller than 2¹⁶" is wrong.
> - ❌ **C:** NIST guidelines recommend e = 65537 but do not mandate it as the ONLY permissible value. FIPS 186-4 allows other values subject to constraints.
> - ❌ **D:** 65537 does not guarantee coprimality with ALL possible φ(n) — it is coprime with φ(n) for virtually all practical cases, but "all possible" is too strong. If p ≡ 1 (mod 65537) or q ≡ 1 (mod 65537), then gcd(65537, φ(n)) > 1. This is extremely rare but not impossible.

---

**Q22. Which RSA padding scheme is currently recommended for RSA ENCRYPTION operations, and what attack does it prevent?**

- A) PKCS#1 v1.5 — prevents timing attacks
- B) PSS — prevents existential forgery in signatures
- C) OAEP — provides CCA2 security, preventing Bleichenbacher's chosen ciphertext attack ✅
- D) No padding — raw RSA is the most mathematically pure and secure form

> **Explanation:**
> - ✅ **C — OAEP:** Optimal Asymmetric Encryption Padding (OAEP) is the recommended padding for RSA encryption. It is CCA2-secure (secure against adaptive chosen ciphertext attacks) and specifically prevents the Bleichenbacher attack — which exploited the structure of PKCS#1 v1.5 formatted ciphertext via padding oracle.
> - ❌ **A:** PKCS#1 v1.5 is the OLDER padding scheme that is VULNERABLE to the Bleichenbacher attack (1998). The 2017 ROBOT attack showed that many TLS servers were still vulnerable to this. PKCS#1 v1.5 is used for legacy compatibility, not recommended for new systems.
> - ❌ **B:** PSS (Probabilistic Signature Scheme) is the recommended padding for RSA SIGNATURES — not encryption. Mixing up PSS (signatures) and OAEP (encryption) is a common exam trap.
> - ❌ **D:** Raw (textbook) RSA with no padding is fundamentally insecure. It is deterministic (same plaintext always produces same ciphertext), malleable (modifying ciphertext produces predictable plaintext changes), and vulnerable to small-exponent attacks with small messages.

---

**Q23. Sony PlayStation 3 (2010) had its firmware signing private key compromised. What specific cryptographic mistake caused this?**

- A) Sony used RSA-512 which was brute-forced by a distributed computing project
- B) Sony used the same ECDSA nonce k for every signature — allowing algebraic recovery of the private key ✅
- C) Sony stored the private key in plaintext on the PS3 hardware without TPM protection
- D) Sony used DES instead of AES for firmware encryption — making it trivially decryptable

> **Explanation:**
> - ✅ **B — Reused ECDSA nonce k:** Sony used a constant k = a fixed random value (effectively constant) for ALL PS3 firmware signatures. In ECDSA, if k is reused in two different signatures (r₁ = r₂ because same k → same point k×G), the private key can be algebraically solved from the two signatures and their messages. Fail0verflow and George Hotz demonstrated this publicly at CCC 2010.
> - ❌ **A:** Sony used ECC (not RSA) for PS3 firmware signing. RSA-512 brute-forcing is a different historical attack on a different system (RSA Factoring Challenge). PS3 used ECDSA.
> - ❌ **C:** The issue was not physical storage of the key — it was a cryptographic implementation flaw in the signing code that reused the random nonce. No TPM extraction was involved.
> - ❌ **D:** The firmware signing issue was about ECDSA signature verification — not firmware encryption. DES vs AES is irrelevant to this specific breach.

---

## MCQs 24–28 — ECC

---

**Q24. In ECC, the private key is a randomly chosen scalar integer k, and the public key is the point P = k × G. What operation makes this system secure?**

- A) Multiplying k × G is computationally infeasible — making key generation impossible to scale
- B) Given P and G, finding k is computationally infeasible — this is the Elliptic Curve Discrete Logarithm Problem (ECDLP) ✅
- C) Given k and G, computing P = k × G is computationally infeasible — making public key derivation hard
- D) The elliptic curve equation y² = x³ + ax + b cannot be solved for real numbers — making reversal impossible

> **Explanation:**
> - ✅ **B — ECDLP hardness:** ECC security rests entirely on the ECDLP — given the public key P and generator point G, finding the private scalar k is computationally infeasible. Forward computation (k × G = P) is easy using the double-and-add algorithm. The reverse (finding k from P and G) has no known polynomial-time algorithm for properly chosen curves.
> - ❌ **A:** Computing k × G is fast and efficient — this is the EASY direction. Key generation is practical and fast (one of ECC's major advantages). If key generation were infeasible, ECC would be unusable.
> - ❌ **C:** This inverts the asymmetry. Computing P = k × G given k and G is the EASY direction (this is what everyone does to generate a public key). It is finding k from P and G that is hard.
> - ❌ **D:** ECC operates over finite fields (Fp or F2^m) — not real numbers. The equation has well-defined solutions in finite fields. Irreversibility comes from the ECDLP mathematical hardness, not from the inability to solve the curve equation.

---

**Q25. Which ECC named curve is used by Bitcoin for its key pairs and ECDSA transaction signatures?**

- A) P-256 (secp256r1)
- B) P-384 (secp384r1)
- C) Curve25519
- D) secp256k1 ✅

> **Explanation:**
> - ✅ **D — secp256k1:** Bitcoin uses secp256k1 — a 256-bit curve standardized by SECG (Standards for Efficient Cryptography Group). It is different from NIST's P-256 (secp256r1) despite both being 256-bit curves. secp256k1 uses a Koblitz curve form (a=0, b=7) which has specific computational advantages for Bitcoin's needs. Ethereum also uses secp256k1.
> - ❌ **A — P-256 (secp256r1):** P-256 is the most widely deployed ECC curve for TLS, ECDSA in certificates, Android, and iOS — but NOT Bitcoin. The names "secp256r1" (NIST random) and "secp256k1" (Koblitz) are easily confused — the exam specifically tests this distinction.
> - ❌ **B — P-384:** P-384 is used for higher-security government and enterprise applications. It is not used by Bitcoin.
> - ❌ **C — Curve25519:** Curve25519 is used by Signal, WhatsApp, OpenSSH, and modern TLS — not by Bitcoin. Curve25519 is a different mathematical form (Montgomery curve) optimized for key exchange (X25519).

---

**Q26. A security architect compares key sizes for equivalent security. Which of the following correctly maps a 128-bit security level across all three algorithm families?**

- A) AES-128 = RSA-2048 = ECC-192
- B) AES-128 = RSA-3072 = ECC-256 ✅
- C) AES-128 = RSA-2048 = ECC-256
- D) AES-128 = RSA-4096 = ECC-384

> **Explanation:**
> - ✅ **B:** Per NIST SP 800-57, 128-bit security level corresponds to: AES-128 (symmetric), RSA-3072 (asymmetric factoring), ECC-256 / P-256 (elliptic curve). This three-way equivalence is one of the most important exam facts in this session.
> - ❌ **A:** RSA-2048 provides only 112-bit security — not 128-bit. ECC-192 provides 96-bit security. Both are below the 128-bit target.
> - ❌ **C:** RSA-2048 gives 112-bit security (not 128-bit). ECC-256 is correct for 128-bit, but the RSA component is wrong. This is the most common trap — many assume RSA-2048 = AES-128 security, but it is actually closer to AES-112.
> - ❌ **D:** RSA-4096 provides 140-bit security and ECC-384 provides 192-bit security — both overshoot 128-bit significantly. Correct for higher security levels but wrong for 128-bit equivalence.

---

**Q27. ECDH is used between Alice and Bob to establish a shared secret. Alice's private key is `a`, Bob's private key is `b`, and the generator point is G. What is the shared secret, and why can an eavesdropper not compute it?**

- A) Shared secret = a + b; eavesdropper cannot add private keys without knowing both
- B) Shared secret = ab × G; eavesdropper sees aG and bG but computing abG requires solving the ECDLP ✅
- C) Shared secret = a × b (integer product); eavesdropper would need to factor the product
- D) Shared secret = G; both parties independently derive G using their private keys

> **Explanation:**
> - ✅ **B:** Alice computes shared secret S = a × (bG) = abG. Bob computes S = b × (aG) = abG. Both arrive at the same point. An eavesdropper sees A = aG and B = bG publicly, but computing abG from aG and bG requires solving the ECDLP — computationally infeasible. This is the Computational Diffie-Hellman (CDH) problem on elliptic curves.
> - ❌ **A:** The shared secret is a point on the elliptic curve (abG) — not a scalar sum a+b. Adding private keys is meaningless in this context and would require both private keys to be known — defeating the purpose.
> - ❌ **C:** The shared secret is the elliptic curve POINT abG — not the integer product a×b. Integer factoring applies to RSA, not ECDH. ECDH security rests on the ECDLP, not factoring.
> - ❌ **D:** G is the generator point — publicly known to everyone including the eavesdropper. If the shared secret were simply G, it would provide zero security. The shared secret must be a unique, private point derived from both private keys.

---

**Q28. What is the key advantage of Curve25519 over NIST P-256 that has made it increasingly preferred for new protocol implementations?**

- A) Curve25519 provides 512-bit security — significantly stronger than P-256's 128-bit level
- B) Curve25519 parameters are transparently chosen for performance and security proofs, with built-in side-channel resistance — unlike NIST curves whose constants have opaque origins ✅
- C) Curve25519 is standardized by NIST — making it mandatory for US government use unlike P-256
- D) Curve25519 uses RSA key exchange internally — making it compatible with existing RSA infrastructure

> **Explanation:**
> - ✅ **B:** Curve25519 (designed by Daniel J. Bernstein, 2005) was specifically designed with transparent, mathematically justified parameter choices. Its Montgomery curve form provides inherent resistance to certain side-channel attacks and implementation errors. NIST P-256 uses random-looking constants whose selection process (influenced by NSA) has never been fully explained — leading some cryptographers to distrust it. Signal, WhatsApp, OpenSSH, WireGuard, and TLS 1.3 all use Curve25519/X25519.
> - ❌ **A:** Curve25519 provides approximately 128-bit security — the same level as P-256. It is not stronger in security level; it is preferred for transparency and implementation safety reasons.
> - ❌ **C:** Curve25519 is NOT standardized by NIST (NIST standardized P-256, P-384, P-521). Curve25519 is standardized in RFC 7748 (IETF). NIST P-256 is the one mandatory for US government use — not Curve25519.
> - ❌ **D:** Curve25519 is an elliptic curve Diffie-Hellman protocol — it has nothing to do with RSA internally. It is a completely separate cryptographic system.

---

## MCQs 29–30 — Extra Notes: Attacks and Standards

---

**Q29. A penetration tester discovers that a server is using RSA encryption where two different servers share the SAME modulus n but have DIFFERENT public exponents e₁ and e₂. What attack is applicable, and what is the outcome?**

- A) Timing attack — the tester measures response times to recover the private key
- B) Common modulus attack — if gcd(e₁, e₂) = 1, the attacker can recover plaintext without the private key ✅
- C) Birthday attack — the shared modulus creates hash collisions between the two ciphertext outputs
- D) Bleichenbacher attack — the shared modulus creates PKCS#1 v1.5 padding vulnerabilities

> **Explanation:**
> - ✅ **B — Common modulus attack:** If the same message M is encrypted with two different public exponents e₁ and e₂ that share the same modulus n, AND gcd(e₁, e₂) = 1 (which is almost always true for standard exponents), an attacker can recover M using the extended Euclidean algorithm: find integers a, b such that a×e₁ + b×e₂ = 1, then M = C₁ᵃ × C₂ᵇ mod n. The private key is never needed. This is why sharing an RSA modulus between entities is strictly forbidden.
> - ❌ **A:** Timing attacks measure the time taken for private key operations (modular exponentiation) — they require access to the server processing decryption requests, not just knowledge that moduli are shared. A different attack model entirely.
> - ❌ **C:** Birthday attacks target hash function collisions — they have no relation to shared RSA moduli. RSA moduli are not hash function inputs.
> - ❌ **D:** Bleichenbacher attacks exploit PKCS#1 v1.5 padding oracles — they target ciphertext format parsing, not modulus sharing. The vulnerability here is algebraic (common modulus), not padding-based.

---

**Q30. NIST SP 800-57 defines security levels for cryptographic algorithms. What is the minimum RSA key size recommended by NIST for systems that need to remain secure BEYOND 2030?**

- A) RSA-1024
- B) RSA-2048
- C) RSA-3072 ✅
- D) RSA-4096

> **Explanation:**
> - ✅ **C — RSA-3072:** NIST SP 800-57 defines RSA-2048 as providing 112-bit security — acceptable currently but planned for deprecation. For systems needing security **beyond 2030**, NIST recommends transitioning to RSA-3072 (128-bit security level) — equivalent to AES-128 and ECC-256. This is the NIST transition guidance documented in SP 800-131A.
> - ❌ **A — RSA-1024:** RSA-1024 provides only ~80-bit security — it has been deprecated and must not be used for any new system. NIST deprecated RSA-1024 in 2013.
> - ❌ **B — RSA-2048:** RSA-2048 is the CURRENT minimum (112-bit security) — acceptable today but not recommended for systems requiring long-term security beyond 2030. The question specifically asks about post-2030 requirements.
> - ❌ **D — RSA-4096:** RSA-4096 provides ~140-bit security — higher than required for 2030 compliance. While secure, NIST's specific recommendation for the 128-bit security level (the post-2030 target) is RSA-3072, not RSA-4096. Using RSA-4096 is not wrong, but it exceeds the minimum recommendation and is significantly slower.

---

## 📊 Answer Key — Quick Reference

| Q | Answer | Topic |
|---|--------|-------|
| 1 | B | DES effective key = 56-bit (8 parity bits removed) |
| 2 | C | DES Initial Permutation (IP) before rounds |
| 3 | C | DES S-Boxes = only non-linear component |
| 4 | B | 3DES E-D-E = backward compatibility with DES |
| 5 | C | Sweet32 = birthday attack on 64-bit block size |
| 6 | C | 2DES MitM = ~57-bit effective security |
| 7 | B | 3DES deprecated 2017/2023 — replaced by AES |
| 8 | C | AES block size = always 128-bit regardless of key size |
| 9 | B | AES-192 = 12 rounds |
| 10 | D | MixColumns omitted from AES final round |
| 11 | D | SubBytes = Confusion via GF(2⁸) S-Box |
| 12 | B | AES-128 = 11 round keys (10 rounds + 1 initial) |
| 13 | D | Serpent = AES runner-up (most conservative) |
| 14 | D | AES-GCM = confidentiality + integrity simultaneously |
| 15 | B | RC5-32/12/16 = 64-bit block, 12 rounds, 128-bit key |
| 16 | C | RC5 distinctive feature = data-dependent rotations |
| 17 | B | RC5 three primitives = XOR + addition + rotation (ARX) |
| 18 | C | φ(n) = (11-1)(13-1) = 10×12 = 120 |
| 19 | B | d = 7⁻¹ mod 120 = 103 |
| 20 | B | C = 2⁷ mod 143 = 128 |
| 21 | B | e = 65537 = 2¹⁶+1 = Fermat prime, 2 set bits, fast |
| 22 | C | OAEP = recommended RSA encryption padding |
| 23 | B | PS3 breach = ECDSA nonce k reused |
| 24 | B | ECC security = ECDLP hardness (find k from P=kG) |
| 25 | D | secp256k1 = Bitcoin's curve (not NIST P-256) |
| 26 | B | 128-bit security = AES-128 = RSA-3072 = ECC-256 |
| 27 | B | ECDH shared secret = abG; ECDLP prevents eavesdropping |
| 28 | B | Curve25519 = transparent parameters + side-channel safety |
| 29 | B | Common modulus attack — shared n, different e values |
| 30 | C | Post-2030 minimum = RSA-3072 (NIST SP 800-57) |

---