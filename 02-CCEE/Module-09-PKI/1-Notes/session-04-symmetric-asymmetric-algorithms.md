# Session 04 — Symmetric & Asymmetric Algorithms

## 📑 Table of Contents

- [1. Symmetric Key Encryption](#1-symmetric-key-encryption)
  - [1.1 Recap — Symmetric Model](#11-recap--symmetric-model)
  - [1.2 DES — Data Encryption Standard](#12-des--data-encryption-standard)
  - [1.3 DES Internal Structure](#13-des-internal-structure)
  - [1.4 DES Key Schedule](#14-des-key-schedule)
  - [1.5 Triple DES (3DES)](#15-triple-des-3des)
  - [1.6 AES — Advanced Encryption Standard](#16-aes--advanced-encryption-standard)
  - [1.7 AES Internal Structure — Four Operations](#17-aes-internal-structure--four-operations)
  - [1.8 AES Key Schedule](#18-aes-key-schedule)
  - [1.9 AES vs DES — Full Comparison](#19-aes-vs-des--full-comparison)
  - [1.10 RC5](#110-rc5)
- [2. Asymmetric Key Encryption](#2-asymmetric-key-encryption)
  - [2.1 Recap — Asymmetric Model](#21-recap--asymmetric-model)
  - [2.2 RSA — Rivest Shamir Adleman](#22-rsa--rivest-shamir-adleman)
  - [2.3 RSA Key Generation — Step by Step](#23-rsa-key-generation--step-by-step)
  - [2.4 RSA Encryption and Decryption](#24-rsa-encryption-and-decryption)
  - [2.5 RSA Worked Example](#25-rsa-worked-example)
  - [2.6 RSA Security and Key Sizes](#26-rsa-security-and-key-sizes)
  - [2.7 RSA Use Cases](#27-rsa-use-cases)
  - [2.8 ECC — Elliptic Curve Cryptography](#28-ecc--elliptic-curve-cryptography)
  - [2.9 ECC Mathematical Foundation](#29-ecc-mathematical-foundation)
  - [2.10 ECC Key Generation](#210-ecc-key-generation)
  - [2.11 ECC Named Curves](#211-ecc-named-curves)
  - [2.12 ECC vs RSA — Full Comparison](#212-ecc-vs-rsa--full-comparison)
- [3. 📌 Extra Notes](#3--extra-notes)
  - [3.1 DES — S-Box Deep Dive](#31-des--s-box-deep-dive)
  - [3.2 Why DES Was Broken — EFF Deep Crack](#32-why-des-was-broken--eff-deep-crack)
  - [3.3 2DES and Meet-in-the-Middle Attack](#33-2des-and-meet-in-the-middle-attack)
  - [3.4 AES Competition History](#34-aes-competition-history)
  - [3.5 AES Modes — Which to Use When](#35-aes-modes--which-to-use-when)
  - [3.6 AES-NI — Hardware Acceleration](#36-aes-ni--hardware-acceleration)
  - [3.7 RC Family — RC2, RC4, RC5, RC6](#37-rc-family--rc2-rc4-rc5-rc6)
  - [3.8 RSA — Why e = 65537](#38-rsa--why-e--65537)
  - [3.9 RSA Padding Schemes — PKCS#1 v1.5 vs OAEP](#39-rsa-padding-schemes--pkcs1-v15-vs-oaep)
  - [3.10 RSA Attacks](#310-rsa-attacks)
  - [3.11 ECC — ECDH and ECDSA](#311-ecc--ecdh-and-ecdsa)
  - [3.12 ECC Curves — NIST vs Curve25519](#312-ecc-curves--nist-vs-curve25519)
  - [3.13 Symmetric Algorithm Comparison Table — All Algorithms](#313-symmetric-algorithm-comparison-table--all-algorithms)
  - [3.14 Asymmetric Algorithm Comparison Table — All Algorithms](#314-asymmetric-algorithm-comparison-table--all-algorithms)
  - [3.15 NIST Recommended Key Sizes — 2024](#315-nist-recommended-key-sizes--2024)
- [4. Abbreviations Table](#4-abbreviations-table)
- [5. Keywords + Concept Map](#5-keywords--concept-map)
- [6. Quick Reference Cheatsheet](#6-quick-reference-cheatsheet)
- [7. Session Revision Snapshot](#7-session-revision-snapshot)

---

## 1. Symmetric Key Encryption

### 1.1 Recap — Symmetric Model

```
Same key used for both encryption and decryption.

Sender:   Plaintext + Key K → Algorithm → Ciphertext
Receiver: Ciphertext + Key K → Algorithm → Plaintext
```

**Core challenge:** Secure key distribution — how do both parties
get the same key without an attacker intercepting it?

**Two structural types:**
- **Block Cipher** — encrypts fixed-size blocks of data
- **Stream Cipher** — encrypts one bit/byte at a time

DES, AES, RC5 are all **block ciphers.**

---

### 1.2 DES — Data Encryption Standard

**DES (Data Encryption Standard)** was developed by IBM in the early
1970s, adopted as a US federal standard (FIPS 46) by **NIST (then NBS)
in 1977**. It was the dominant symmetric cipher for over two decades.

**Core Parameters:**

| Parameter | Value |
|-----------|-------|
| **Block size** | 64 bits |
| **Key size** | 64 bits (56 bits effective + 8 parity bits) |
| **Effective key length** | 56 bits |
| **Number of rounds** | 16 |
| **Structure** | Feistel cipher |
| **Key space** | 2⁵⁶ ≈ 72 quadrillion keys |
| **Status** | ❌ Broken — deprecated |

> [!IMPORTANT]
> The key in DES is 64 bits long but only **56 bits are used for
> encryption** — every 8th bit is a parity bit used for error checking.
> MCQ trap: "DES uses a 64-bit key" is technically true in terms of
> input length, but its **effective security is only 56 bits.**

**Why DES is broken:**
- 56-bit key space is too small for modern computing
- In 1998, the **EFF (Electronic Frontier Foundation)** built
  **"Deep Crack"** — a dedicated hardware machine — and broke
  DES in **56 hours** for under $250,000
- In 1999, **distributed.net + Deep Crack** broke DES in
  **22 hours 15 minutes**
- Today, a modern GPU cluster can break DES in **hours to days**

---

### 1.3 DES Internal Structure

DES is a **Feistel cipher** operating on 64-bit blocks over 16 rounds.

**High-level flow:**

```
64-bit Plaintext
      │
      ▼
┌─────────────┐
│ Initial     │  ← IP (Initial Permutation) — rearranges 64 bits
│ Permutation │    (fixed table — no security value, historical)
└─────────────┘
      │
      ▼
  Split into:
  L₀ (32 bits left half)  |  R₀ (32 bits right half)
      │
      ▼
┌─────────────────────────────────────────────────────┐
│  16 Feistel Rounds (i = 1 to 16)                    │
│                                                     │
│  Lᵢ = Rᵢ₋₁                                         │
│  Rᵢ = Lᵢ₋₁ XOR F(Rᵢ₋₁, Kᵢ)                       │
│                                                     │
│  Where F = Feistel Round Function (see below)       │
│  Kᵢ = 48-bit subkey for round i                     │
└─────────────────────────────────────────────────────┘
      │
      ▼
  Combine L₁₆ and R₁₆
      │
      ▼
┌─────────────┐
│ Final       │  ← FP (Final Permutation) — inverse of IP
│ Permutation │
└─────────────┘
      │
      ▼
64-bit Ciphertext
```

**DES Round Function F(R, K):**

```
R (32-bit)
   │
   ▼
Expansion (E)      ← 32 bits → 48 bits (some bits repeated)
   │
   ▼
XOR with Kᵢ        ← 48-bit subkey
   │
   ▼
S-Box Substitution ← 8 S-boxes × 6-bit input → 4-bit output each
   │               (48 bits → 32 bits)
   ▼
Permutation (P)    ← Final permutation of 32 bits
   │
   ▼
Output (32 bits)   → XOR with Lᵢ₋₁
```

**The 8 S-Boxes are the ONLY non-linear component in DES.**
They are what provides **Confusion** (Shannon's property).

> [!NOTE]
> The S-Boxes in DES were designed by the NSA — this caused
> controversy at the time (fear of backdoor).
> Later analysis showed the S-Boxes were actually designed to
> resist **differential cryptanalysis** — a technique the NSA
> knew about but had not publicly disclosed in 1977.

---

### 1.4 DES Key Schedule

The 64-bit input key generates **16 round subkeys of 48 bits each.**

```
64-bit Key Input
      │
      ▼
PC-1 (Permuted Choice 1)
→ Drops 8 parity bits → 56-bit key
→ Splits into C₀ (28 bits) and D₀ (28 bits)
      │
      ▼
For each round i:
  Cᵢ = Left circular shift of Cᵢ₋₁ (by 1 or 2 positions)
  Dᵢ = Left circular shift of Dᵢ₋₁ (by 1 or 2 positions)
      │
      ▼
PC-2 (Permuted Choice 2)
→ Selects 48 bits from Cᵢ + Dᵢ (56 bits)
→ Output: 48-bit subkey Kᵢ
```

**Shift schedule per round:**

| Rounds | Left Shifts |
|--------|------------|
| 1, 2, 9, 16 | 1 bit |
| All others | 2 bits |

> [!NOTE]
> For decryption in DES, the same key schedule is used but
> subkeys are applied in **reverse order** (K₁₆ → K₁).
> This is the elegance of the Feistel structure — same hardware
> for both encrypt and decrypt.

---

### 1.5 Triple DES (3DES)

**Triple DES (3DES)** was introduced as a stopgap when DES was found
to be too weak — applying DES three times with two or three
different keys.

**3DES Variants:**

| Variant | Keys Used | Effective Key Length | Security |
|---------|-----------|---------------------|---------|
| **3TDEA (3-key 3DES)** | K1, K2, K3 (all different) | 168 bits | ✅ Secure but slow |
| **2TDEA (2-key 3DES)** | K1, K2 (K3 = K1) | 112 bits | ⚠️ Acceptable |
| **1-key 3DES** | K1 = K2 = K3 | 56 bits (= DES) | ❌ No improvement |

**3DES Encrypt-Decrypt-Encrypt (EDE) pattern:**
```
Plaintext
   │
   ▼
DES Encrypt (K1)
   │
   ▼
DES Decrypt (K2)     ← Decrypt with K2 (not K1)
   │
   ▼
DES Encrypt (K3)
   │
   ▼
Ciphertext
```

> [!NOTE]
> The E-D-E (Encrypt-Decrypt-Encrypt) pattern instead of E-E-E was
> chosen for **backward compatibility** — if K1=K2=K3, 3DES reduces
> to single DES. This made migration easier.
>
> **Why not just E-E-E?**
> E-E-E with two keys is vulnerable to
> **Meet-in-the-Middle attack** (see Extra Notes 3.3).
> E-D-E resists this attack.

**3DES Status:**
- **NIST deprecated 3DES in 2017 (NIST SP 800-131A Rev. 2)**
- **NIST disallowed 3DES for new applications after 2023**
- Main reasons: slow speed, 64-bit block size (Sweet32 attack),
  practical deprecation in TLS

> [!IMPORTANT]
> **Sweet32 Attack (2016):** Birthday attack against 64-bit block
> ciphers (DES, 3DES, Blowfish). After 2³² blocks (~32GB of data
> with the same key), collision probability exceeds 50%.
> This is why 64-bit block size ciphers are deprecated — AES uses
> 128-bit blocks.

---

### 1.6 AES — Advanced Encryption Standard

**AES (Advanced Encryption Standard)** was selected by NIST in 2001
(FIPS 197) after a 5-year public competition (1997–2001) to replace
DES. The winning algorithm was **Rijndael**, designed by Belgian
cryptographers **Joan Daemen and Vincent Rijmen**.

**Core Parameters:**

| Parameter | AES-128 | AES-192 | AES-256 |
|-----------|---------|---------|---------|
| **Key size** | 128 bits | 192 bits | 256 bits |
| **Block size** | 128 bits | 128 bits | 128 bits |
| **Number of rounds** | 10 | 12 | 14 |
| **Structure** | SPN (not Feistel) | SPN | SPN |
| **Status** | ✅ Secure | ✅ Secure | ✅ Quantum-safe candidate |

> [!IMPORTANT]
> AES always uses a **128-bit block size** regardless of key size.
> Only the **key size and number of rounds** change between
> AES-128, AES-192, and AES-256.
> MCQ trap: "AES-256 uses a 256-bit block size" → **FALSE.**
> Block size is always 128 bits.

**AES State:**
AES operates on a **4×4 matrix of bytes** called the **State**.

```
128-bit block = 16 bytes arranged as:

┌────┬────┬────┬────┐
│ b₀ │ b₄ │ b₈ │ b₁₂│
├────┼────┼────┼────┤
│ b₁ │ b₅ │ b₉ │ b₁₃│
├────┼────┼────┼────┤
│ b₂ │ b₆ │ b₁₀│ b₁₄│
├────┼────┼────┼────┤
│ b₃ │ b₇ │ b₁₁│ b₁₅│
└────┴────┴────┴────┘
4 rows × 4 columns = 16 bytes = 128 bits
```

---

### 1.7 AES Internal Structure — Four Operations

AES uses a **Substitution-Permutation Network (SPN)** — NOT Feistel.

Each round consists of **4 operations** applied to the State:

#### Operation 1 — SubBytes (Confusion)
- Each byte in the State is replaced by a corresponding byte
  from the **AES S-Box** (a fixed 256-entry lookup table)
- S-Box values are derived from the **multiplicative inverse in GF(2⁸)**
- Provides **non-linearity** → implements **Shannon's Confusion**
- Makes the relationship between key and ciphertext complex

```
Before SubBytes:     After SubBytes:
┌──┬──┬──┬──┐       ┌──┬──┬──┬──┐
│19│a0│9a│e9│  →    │d4│e0│b8│1e│
│3d│f4│c6│f8│  →    │27│bf│b4│41│
│e3│e2│8d│48│  →    │11│98│5d│52│
│be│2b│2a│08│  →    │ae│f1│e5│30│
└──┴──┴──┴──┘       └──┴──┴──┴──┘
```

#### Operation 2 — ShiftRows (Diffusion)
- Each row of the State is cyclically shifted left by a different
  number of positions:
  - Row 0: No shift
  - Row 1: Shift left by 1
  - Row 2: Shift left by 2
  - Row 3: Shift left by 3
- Provides **Diffusion** — bytes from different columns mix

```
Before ShiftRows:    After ShiftRows:
Row 0: d4 e0 b8 1e  → d4 e0 b8 1e  (no shift)
Row 1: 27 bf b4 41  → bf b4 41 27  (shift 1)
Row 2: 11 98 5d 52  → 5d 52 11 98  (shift 2)
Row 3: ae f1 e5 30  → 30 ae f1 e5  (shift 3)
```

#### Operation 3 — MixColumns (Diffusion)
- Each column of the State is multiplied by a fixed polynomial
  in **GF(2⁸)** (Galois Field arithmetic)
- Each output byte depends on ALL 4 input bytes of the column
- Provides **maximum Diffusion** — strongest mixing operation

```
Each column is treated as a polynomial and multiplied:
┌──┐   ┌────────────┐   ┌──┐
│d4│   │ 2  3  1  1 │   │04│
│bf│ × │ 1  2  3  1 │ = │66│
│5d│   │ 1  1  2  3 │   │81│
│30│   │ 3  1  1  2 │   │e5│
└──┘   └────────────┘   └──┘
(multiplication is in GF(2⁸))
```

> [!NOTE]
> **MixColumns is skipped in the LAST round** of AES — adding it
> in the final round would provide no additional security and
> would complicate the inverse operation.

#### Operation 4 — AddRoundKey (Key Mixing)
- Each byte of the State is XORed with the corresponding byte
  of the **round key** (derived from key schedule)
- This is the ONLY operation that uses the key
- Provides the key-dependent transformation

```
State XOR Round Key = New State

┌──┬──┬──┬──┐   ┌──┬──┬──┬──┐   ┌──┬──┬──┬──┐
│04│66│81│e5│XOR│a0│88│23│2a│ = │a4│ee│a2│cf│
│...              ...              ...         │
└──┴──┴──┴──┘   └──┴──┴──┴──┘   └──┴──┴──┴──┘
```

**Full AES Round Summary:**

| Round | Operations |
|-------|-----------|
| **Initial** | AddRoundKey only |
| **Rounds 1 to N-1** | SubBytes → ShiftRows → MixColumns → AddRoundKey |
| **Final Round (N)** | SubBytes → ShiftRows → AddRoundKey (NO MixColumns) |

Where N = 10 (AES-128), 12 (AES-192), 14 (AES-256)

> [!IMPORTANT]
> Shannon mapping in AES:
> - **Confusion** → SubBytes (S-Box substitution)
> - **Diffusion** → ShiftRows + MixColumns (spreading + mixing)
> - **Key mixing** → AddRoundKey (XOR with round key)

---

### 1.8 AES Key Schedule

AES expands the original key into multiple **round keys** using
**Rijndael's Key Schedule.**

| AES Variant | Original Key | Round Keys Generated | Total Round Key Bits |
|-------------|-------------|---------------------|---------------------|
| AES-128 | 128 bits (16 bytes) | 11 round keys | 1408 bits |
| AES-192 | 192 bits (24 bytes) | 13 round keys | 1664 bits |
| AES-256 | 256 bits (32 bytes) | 15 round keys | 1920 bits |

Key expansion uses:
- **SubWord** — apply S-Box to each byte of a word
- **RotWord** — cyclic left shift of a 4-byte word
- **XOR with Rcon** — round constant (prevents symmetry)

> [!NOTE]
> AES-128 needs 11 round keys (1 initial + 10 rounds).
> AES-256 needs 15 round keys (1 initial + 14 rounds).
> The key schedule ensures every round key is different —
> even if the original key has repeated patterns.

---

### 1.9 AES vs DES — Full Comparison

| Property | DES | AES |
|----------|-----|-----|
| **Published** | 1977 | 2001 |
| **Designer** | IBM + NSA | Joan Daemen + Vincent Rijmen |
| **Block size** | 64 bits | 128 bits |
| **Key size** | 56 bits (effective) | 128, 192, or 256 bits |
| **Rounds** | 16 | 10, 12, or 14 |
| **Structure** | Feistel | SPN (Substitution-Permutation Network) |
| **S-Boxes** | 8 fixed S-Boxes (6-bit in, 4-bit out) | 1 S-Box (8-bit in, 8-bit out) |
| **Key schedule** | 16 × 48-bit subkeys | 11/13/15 × 128-bit round keys |
| **Security status** | ❌ Broken | ✅ Secure |
| **Speed** | Slow (software) | Fast (especially with AES-NI) |
| **Standardization** | FIPS 46 (1977, withdrawn 2005) | FIPS 197 (2001, current) |

> [!IMPORTANT]
> **DES was officially withdrawn by NIST in 2005 (FIPS 46-3).**
> AES (FIPS 197) is the current standard and has no known
> practical attacks against full AES.

---

### 1.10 RC5

**RC5** was designed by **Ron Rivest** (the 'R' in RSA) in **1994**.
RC stands for **Rivest Cipher** (also said to stand for
**Ron's Code**).

**Core Parameters:**

| Parameter | Value / Range |
|-----------|--------------|
| **Designer** | Ron Rivest (RSA Security) |
| **Year** | 1994 |
| **Block size (w)** | 32, 64, or 128 bits (word size w) |
| **Key size (b)** | 0 to 2040 bits (variable) |
| **Rounds (r)** | 0 to 255 (variable) |
| **Standard notation** | RC5-w/r/b (e.g., RC5-32/12/16) |
| **Structure** | Feistel-like with data-dependent rotations |
| **Type** | Block cipher |

**RC5 Notable Features:**

| Feature | Description |
|---------|-------------|
| **Data-dependent rotations** | The shift amount in each round depends on the data being encrypted — makes differential/linear cryptanalysis harder |
| **Simplicity** | Uses only three operations: XOR, addition, rotation |
| **Flexibility** | Word size, rounds, and key size are all configurable |
| **Magic constants** | Uses constants Pw and Qw derived from mathematical constants (e and φ) |

**RC5 Round Operations (three primitives only):**
```
⊕  → XOR
+  → Addition mod 2^w
<<<→ Left rotation (data-dependent)
```

**RC5-32/12/16** is the most commonly referenced configuration:
- 32-bit word size → 64-bit block
- 12 rounds
- 16-byte (128-bit) key

> [!NOTE]
> RC5's **data-dependent rotations** were a novel feature at the
> time of design. The shift amount is determined by the actual
> data — unlike DES where shifts are fixed. This makes it harder
> for attackers to build algebraic models of the cipher.

> [!IMPORTANT]
> RC5 is rarely used today in new systems — AES has replaced it.
> However, RC5 is important historically and conceptually — it
> directly inspired **RC6**, which was an AES candidate.

---

## 2. Asymmetric Key Encryption

### 2.1 Recap — Asymmetric Model

```
Two mathematically linked keys:
  Public Key  (KU) — freely distributed
  Private Key (KR) — kept secret by owner

Encryption:  C = E(KU_receiver, P)
Decryption:  P = D(KR_receiver, C)

Signing:     S = E(KR_sender, Hash(M))
Verification: Hash(M) = D(KU_sender, S)
```

**Mathematical hardness problems:**

| Algorithm | Hard Problem |
|-----------|-------------|
| RSA | Integer Factorization |
| Diffie-Hellman | Discrete Logarithm |
| ECC | Elliptic Curve Discrete Logarithm (ECDLP) |

---

### 2.2 RSA — Rivest Shamir Adleman

**RSA** was published in **1977** by **Ron Rivest, Adi Shamir, and
Leonard Adleman** at MIT. It was the **first practical public-key
cryptosystem** for both encryption and digital signatures.

**Historical note:** Clifford Cocks at GCHQ (UK) independently
discovered an equivalent system in 1973 — but it was classified as
top secret and not published until 1997.

**Core Parameters:**

| Parameter | Value |
|-----------|-------|
| **Designer** | Rivest, Shamir, Adleman (MIT, 1977) |
| **Type** | Asymmetric |
| **Mathematical basis** | Integer Factorization Problem |
| **Key sizes** | 1024, 2048, 3072, 4096 bits |
| **Recommended minimum** | 2048 bits (current); 3072 bits (post-2030) |
| **Block size** | Variable — depends on key size |
| **Primary uses** | Encryption, Key Exchange, Digital Signatures |
| **Status** | ✅ Secure (2048-bit+), ⚠️ 1024-bit deprecated |

---

### 2.3 RSA Key Generation — Step by Step

```
Step 1: Choose two large, distinct prime numbers p and q
        p ≈ q in size, both randomly generated
        Example (small): p = 61, q = 53

Step 2: Compute n = p × q
        n = 61 × 53 = 3233
        n is the MODULUS — part of both public and private key

Step 3: Compute Euler's totient φ(n) = (p-1)(q-1)
        φ(3233) = (61-1)(53-1) = 60 × 52 = 3120

Step 4: Choose public exponent e such that:
        • 1 < e < φ(n)
        • gcd(e, φ(n)) = 1  (e and φ(n) are coprime)
        Common choice: e = 65537 (in practice)
        Example: e = 17  (gcd(17, 3120) = 1 ✅)

Step 5: Compute private exponent d:
        d × e ≡ 1 (mod φ(n))
        d = e⁻¹ mod φ(n)  (modular multiplicative inverse)
        d × 17 ≡ 1 (mod 3120)
        d = 2753  (since 17 × 2753 = 46801 = 15 × 3120 + 1 ✅)

Step 6: Discard p, q, φ(n) — keep secret or destroy

Result:
  Public Key  = (e, n) = (17, 3233)
  Private Key = (d, n) = (2753, 3233)
```

> [!IMPORTANT]
> RSA security comes from the fact that:
> - **n is public** — everyone knows it
> - **Factoring n back to p and q is infeasible** for large n
> - Without p and q, **φ(n) cannot be computed**
> - Without φ(n), **d cannot be computed** from e
> - The entire private key derivation chain breaks without the ability to factor n

---

### 2.4 RSA Encryption and Decryption

**Encryption (sender uses receiver's public key):**
```
C = Mᵉ mod n
```

**Decryption (receiver uses their private key):**
```
M = Cᵈ mod n
```

Where:
- M = plaintext message (as a number, M < n)
- C = ciphertext
- e, d, n = RSA key components
- All operations are **modular arithmetic**

**Why decryption recovers M:**
```
C = Mᵉ mod n
Cᵈ = (Mᵉ)ᵈ = Mᵉᵈ mod n

Since d × e ≡ 1 (mod φ(n)):
  Mᵉᵈ = M¹ = M (mod n)    ← Euler's Theorem
```

---

### 2.5 RSA Worked Example

Using the keys generated in 2.3: Public (17, 3233), Private (2753, 3233)

**Encrypt M = 65:**
```
C = 65¹⁷ mod 3233
C = 2790
```

**Decrypt C = 2790:**
```
M = 2790²⁷⁵³ mod 3233
M = 65  ✅
```

> [!NOTE]
> In practice, RSA never encrypts raw numbers like this.
> Padding schemes (PKCS#1 v1.5, OAEP) are applied before RSA
> encryption — covered in Extra Notes 3.9.
> Also, RSA is never used to encrypt large data directly —
> **hybrid encryption** is always used in practice.

---

### 2.6 RSA Security and Key Sizes

**Current status of RSA key sizes:**

| Key Size | Security Level | Status |
|----------|---------------|--------|
| 512-bit | ~56-bit equivalent | ❌ Broken (1999) |
| 768-bit | ~76-bit equivalent | ❌ Broken (2010) |
| 1024-bit | ~80-bit equivalent | ❌ Deprecated — do not use |
| 2048-bit | ~112-bit equivalent | ✅ Current standard |
| 3072-bit | ~128-bit equivalent | ✅ Recommended post-2030 |
| 4096-bit | ~140-bit equivalent | ✅ High security |

> [!IMPORTANT]
> NIST recommendation:
> - **Minimum today:** RSA-2048
> - **Recommended for data needing long-term security:** RSA-3072
> - RSA-1024 must not be used for new systems
>
> **RSA vs AES security equivalence:**
> RSA-2048 ≈ AES-112 (not AES-128!)
> RSA-3072 ≈ AES-128
> RSA-15360 ≈ AES-256
> This is why ECC is preferred — 256-bit ECC ≈ RSA-3072 ≈ AES-128

---

### 2.7 RSA Use Cases

| Use Case | How RSA Is Used |
|----------|----------------|
| **Encryption** | Encrypt small data or symmetric keys (hybrid model) |
| **Digital Signatures** | Sign hash with private key; verify with public key |
| **Key Exchange** | RSA key transport — sender encrypts session key with receiver's RSA public key |
| **TLS/HTTPS** | RSA certificates authenticate the server; RSA or ECDH used for key exchange |
| **SSH** | RSA key pairs for user authentication |
| **Code signing** | Software publishers sign code with RSA private key |
| **S/MIME and PGP** | RSA for key wrapping in email encryption |
| **Certificate signing (CA)** | CA signs certificate with its RSA private key |

---

### 2.8 ECC — Elliptic Curve Cryptography

**ECC (Elliptic Curve Cryptography)** was proposed independently by
**Neal Koblitz** and **Victor Miller** in **1985**. It is based on
the mathematics of **elliptic curves over finite fields.**

**Why ECC?**
ECC provides the same security level as RSA but with **dramatically
shorter key lengths** — making it faster, lighter on battery, and
ideal for constrained environments.

**Core Parameters:**

| Parameter | Value |
|-----------|-------|
| **Proposed by** | Neal Koblitz + Victor Miller (1985) |
| **Mathematical basis** | Elliptic Curve Discrete Logarithm Problem (ECDLP) |
| **Key sizes** | 160–521 bits (common: 256, 384, 521) |
| **Primary uses** | Key Exchange (ECDH), Digital Signatures (ECDSA), Encryption (ECIES) |
| **Status** | ✅ Current standard — preferred over RSA for new systems |

---

### 2.9 ECC Mathematical Foundation

**An elliptic curve** is defined by the equation:
```
y² = x³ + ax + b  (over a finite field Fp or F2^m)
```

**Conditions for a valid elliptic curve:**
```
4a³ + 27b² ≠ 0  (no repeated roots — no cusps or self-intersections)
```

**Visual (over real numbers — for conceptual understanding):**
```
      y
      │         ╭────╮
      │       ╭─╯    ╰─╮
      │      ─╯         ╰─
      │──────────────────── x
      │      ─╮         ╭─
      │       ╰─╮    ╭─╯
      │         ╰────╯
```

The curve is **symmetric about the x-axis** — for every point (x, y)
on the curve, (x, −y) is also on the curve.

**Elliptic Curve Point Operations:**

#### Point Addition (P + Q = R)
Given two distinct points P and Q on the curve:
```
Draw a line through P and Q
→ The line intersects the curve at a third point R'
→ Reflect R' across the x-axis → R = P + Q
```

#### Point Doubling (P + P = 2P)
When P = Q:
```
Draw the tangent line to the curve at point P
→ The tangent intersects the curve at a second point R'
→ Reflect R' across the x-axis → 2P
```

#### Point at Infinity (O)
- The **identity element** of the group
- P + O = P for any point P
- If a line through P and Q is vertical → P + Q = O

---

### 2.10 ECC Key Generation

```
Step 1: Select a named curve (e.g., P-256, Curve25519)
        The curve defines:
        - The equation (a, b parameters)
        - The finite field Fp (prime p)
        - Generator point G (publicly known, fixed for the curve)
        - Order n (number of points on the curve)

Step 2: Choose private key k
        k = random integer, 1 ≤ k ≤ n-1
        This is the PRIVATE KEY

Step 3: Compute public key P
        P = k × G  (scalar multiplication of G by k)
        This is the PUBLIC KEY

Security:
  Given G and P = k × G → finding k is the ECDLP
  (computationally infeasible for proper curve/key size)
```

**Scalar Multiplication (k × G):**
```
k × G means:
  k = 1 → G
  k = 2 → G + G = 2G
  k = 3 → G + G + G = 3G
  ...
  k = n → G + G + ... (k times) = P (public key)
```

This is computed efficiently using **double-and-add** algorithm
(analogous to square-and-multiply for modular exponentiation).

> [!IMPORTANT]
> **The critical asymmetry:**
> - Computing P = k × G: **easy** (efficient double-and-add)
> - Finding k given P and G: **computationally infeasible** (ECDLP)
>
> This is the trapdoor in ECC — k is the private key (trapdoor).

---

### 2.11 ECC Named Curves

Named curves are pre-defined elliptic curves with carefully chosen
parameters that are widely trusted and standardized.

| Curve | Also Known As | Key Size | Standardized By | Usage |
|-------|--------------|---------|----------------|-------|
| **P-192** | secp192r1, prime192v1 | 192-bit | NIST | Legacy |
| **P-256** | secp256r1, prime256v1 | 256-bit | NIST | Most common — TLS, ECDSA |
| **P-384** | secp384r1 | 384-bit | NIST | High security — US government |
| **P-521** | secp521r1 | 521-bit | NIST | Highest NIST security level |
| **Curve25519** | X25519 (for DH) | 255-bit | Bernstein | Modern — fast, resistant to side-channels |
| **Curve448** | X448 | 448-bit | Bernstein | Very high security |
| **secp256k1** | — | 256-bit | SECG | Bitcoin, Ethereum blockchain |

> [!NOTE]
> **P-256 (secp256r1)** is the most widely deployed ECC curve —
> used in TLS certificates, Android, iOS, Chrome, Firefox.
>
> **Curve25519** is increasingly preferred for new systems —
> designed by Daniel J. Bernstein specifically to avoid potential
> NSA influence in NIST curve parameters.
>
> **secp256k1** is rarely used in traditional security but is
> famous as the curve used by **Bitcoin** for its key pairs
> and ECDSA signatures.

---

### 2.12 ECC vs RSA — Full Comparison

| Property | RSA | ECC |
|----------|-----|-----|
| **Mathematical basis** | Integer Factorization | ECDLP |
| **Key size for 128-bit security** | 3072-bit | 256-bit |
| **Key size for 112-bit security** | 2048-bit | 224-bit |
| **Key size for 192-bit security** | 7680-bit | 384-bit |
| **Computation speed** | Slower | Faster |
| **Key/Signature size** | Larger | Smaller |
| **Power consumption** | Higher | Lower |
| **Ideal for** | Legacy systems, wide compatibility | Mobile, IoT, TLS, modern systems |
| **Quantum vulnerability** | ❌ Broken by Shor's | ❌ Broken by Shor's |
| **PQC replacement** | CRYSTALS-Kyber (key exchange) | CRYSTALS-Dilithium (signatures) |
| **Maturity** | High — 1977, widely analyzed | Medium-High — 1985, well analyzed |
| **NIST recommendation** | RSA-2048 min (now) | P-256 min (now) |

> [!TIP]
> **Memory hook for key size equivalence:**
> - 256-bit ECC ≈ 3072-bit RSA ≈ 128-bit AES (security level)
> - 384-bit ECC ≈ 7680-bit RSA ≈ 192-bit AES
> These equivalences are critical for exam MCQs on key sizes.

---

## 3. 📌 Extra Notes

> [!NOTE]
> Everything in this section goes beyond the core syllabus but is
> directly MCQ-relevant. Cross-referenced from Stallings,
> NIST publications, and cryptographic standards.

---

### 3.1 DES — S-Box Deep Dive

> [!NOTE]
> The 8 S-Boxes in DES are the heart of its security — the only
> source of non-linearity.

**S-Box operation:**
```
Input:  6 bits  → row (bits 1,6) + column (bits 2,3,4,5)
Output: 4 bits  → value from S-Box table

Row selection:   bits 1 and 6 (outer bits)
Column selection: bits 2,3,4,5 (inner 4 bits)

Example — S-Box 1, input 011011:
  Row    = bit1, bit6 = 0,1 → row 01 = 1
  Column = bits 2-5 = 1101  = 13
  S1[1][13] = 5 → output = 0101
```

**Why S-Box design matters:**
- S-Boxes provide **non-linearity** — without it, DES would be
  vulnerable to linear cryptanalysis
- NIST S-Boxes were designed to resist **differential** and
  **linear cryptanalysis** — attacks the public didn't know
  about in 1977 but NSA did

---

### 3.2 Why DES Was Broken — EFF Deep Crack

> [!NOTE]

| Event | Year | Details |
|-------|------|---------|
| DES Challenge I | 1997 | distributed.net broke DES in 96 days |
| DES Challenge II-1 | 1998 | EFF Deep Crack broke DES in 56 hours — cost ~$250,000 |
| DES Challenge II-2 | 1998 | Deep Crack + distributed.net — 39 days |
| DES Challenge III | 1999 | Deep Crack + distributed.net — **22 hours 15 minutes** |

**Deep Crack design:**
- Custom-built hardware with 1,856 chips running in parallel
- Each chip tested 2.5 million keys per second
- Total: ~90 billion keys per second

> This demonstrated that a well-funded attacker (at the time
> requiring ~$250K) could break DES — today it would cost
> orders of magnitude less with cloud GPU computing.

---

### 3.3 2DES and Meet-in-the-Middle Attack

> [!NOTE]
> **Why not use 2DES (double DES)** instead of 3DES?
> Because it is vulnerable to a **Meet-in-the-Middle (MitM) attack.**

**2DES:**
```
C = DES_K2(DES_K1(P))
```

**Naive expectation:** 2 × 56 bits = 112-bit effective key space.

**Meet-in-the-Middle attack:**
```
Step 1: For all 2⁵⁶ possible K1 values:
        Compute X = DES_K1(P)
        Store (K1, X) in a lookup table

Step 2: For all 2⁵⁶ possible K2 values:
        Compute X' = DES⁻¹_K2(C)
        If X' matches any X in the table:
        → K1, K2 pair found

Cost: 2 × 2⁵⁶ operations and 2⁵⁶ storage
Effective security: ≈ 57 bits (barely better than single DES!)
```

> [!IMPORTANT]
> 2DES effectively provides only ~57 bits of security due to
> Meet-in-the-Middle — this is why it was never standardized.
> 3DES (with E-D-E) resists this attack because the middle
> Decrypt operation breaks the algebraic structure that
> MitM exploits.

---

### 3.4 AES Competition History

> [!NOTE]

| Year | Event |
|------|-------|
| 1997 | NIST issues call for AES submissions |
| 1998 | 15 algorithms submitted for Round 1 |
| 1999 | 5 finalists selected for Round 2 |
| 2001 | **Rijndael** selected as AES — FIPS 197 published |

**AES Round 2 Finalists:**

| Algorithm | Designers | Origin | Structure |
|-----------|-----------|--------|-----------|
| **Rijndael** ✅ | Joan Daemen, Vincent Rijmen | Belgium | SPN |
| **Serpent** | Anderson, Biham, Knudsen | UK/Israel/Norway | SPN — most conservative |
| **Twofish** | Bruce Schneier et al. | USA | Feistel |
| **RC6** | RSA Security (Ron Rivest) | USA | Feistel-like |
| **MARS** | IBM | USA | Mixed |

> Rijndael won primarily for its **speed, efficiency, and elegant
> mathematical structure.** Serpent was considered the most secure
> but was slower. Twofish was a strong all-rounder.

---

### 3.5 AES Modes — Which to Use When

> [!NOTE]
> (Introduced in Session 02 — expanded here in symmetric algorithm context)

| Mode | Parallelizable? | IV Needed? | Authentication? | Use Case |
|------|----------------|-----------|----------------|---------|
| **ECB** | ✅ Encrypt + Decrypt | ❌ No | ❌ No | ❌ Never use |
| **CBC** | ✅ Decrypt only | ✅ Yes | ❌ No | File encryption, TLS 1.2 |
| **CFB** | ✅ Decrypt only | ✅ Yes | ❌ No | Stream-like file encryption |
| **OFB** | ❌ Neither | ✅ Yes | ❌ No | Satellite comms (error tolerance) |
| **CTR** | ✅ Both | ✅ Yes (nonce) | ❌ No | High-speed encryption, disk |
| **GCM** | ✅ Both | ✅ Yes (nonce) | ✅ Yes | TLS 1.3, HTTPS, authenticated encryption |
| **CCM** | ❌ No | ✅ Yes | ✅ Yes | IoT, 802.11i (Wi-Fi) |

> [!IMPORTANT]
> **GCM (Galois/Counter Mode)** is the gold standard for modern
> encryption — provides both encryption (CTR mode) and
> authentication (GMAC). AES-256-GCM is the cipher suite
> used in TLS 1.3.
>
> **Never use ECB** — identical plaintext blocks produce identical
> ciphertext blocks, revealing data patterns.

---

### 3.6 AES-NI — Hardware Acceleration

> [!NOTE]
> **AES-NI (AES New Instructions)** — introduced by Intel in 2010,
> AMD in 2011. A set of CPU instructions that implement AES
> operations directly in hardware.

| Instruction | Operation |
|-------------|-----------|
| `AESENC` | Perform one AES encryption round |
| `AESENCLAST` | Perform final AES encryption round |
| `AESDEC` | Perform one AES decryption round |
| `AESDECLAST` | Perform final AES decryption round |
| `AESKEYGENASSIST` | Assist in key schedule generation |
| `AESIMC` | Inverse Mix Columns for decryption key schedule |

**Performance impact:**
- Software AES: ~100–200 MB/s
- AES-NI hardware: **~1–4 GB/s** — 10–20× faster
- Also resists **cache-timing side-channel attacks**

> [!NOTE]
> AES-NI is available on virtually all modern x86/x64 CPUs
> (Intel Core i-series, AMD Ryzen).
> OpenSSL, Windows CNG, and all major TLS libraries
> automatically use AES-NI when available.

---

### 3.7 RC Family — RC2, RC4, RC5, RC6

> [!NOTE]
> All RC algorithms were designed by **Ron Rivest** at RSA Security.

| Algorithm | Year | Type | Key Size | Block Size | Status |
|-----------|------|------|---------|-----------|--------|
| **RC2** | 1987 | Block | 8–128-bit | 64-bit | ❌ Deprecated |
| **RC4** | 1987 | Stream | 40–2048-bit | N/A (stream) | ❌ Broken — deprecated |
| **RC5** | 1994 | Block | 0–2040-bit | 32/64/128-bit | ⚠️ Secure but obsolete |
| **RC6** | 1998 | Block | 128/192/256-bit | 128-bit | ⚠️ AES finalist — rarely used |

**RC4 — Why It's Broken:**
- RC4 was used in WEP (Wi-Fi), SSL 3.0, TLS 1.0
- Weak key scheduling: first bytes of keystream are biased
- **BEAST attack (2011)** and **RC4 NOMORE attack (2015)**
  demonstrated practical plaintext recovery
- RFC 7465 (2015) **prohibits RC4 in TLS**
- WEP (which used RC4) was completely broken — replaced by WPA2 (AES)

> [!IMPORTANT]
> RC4 must NOT be used in any new system.
> Its deprecation in TLS is mandated by RFC 7465.

---

### 3.8 RSA — Why e = 65537

> [!NOTE]
> In practice, the RSA public exponent **e is almost always 65537.**

**Why 65537?**

| Reason | Explanation |
|--------|-------------|
| **Fermat prime** | 65537 = 2¹⁶ + 1 — a Fermat prime |
| **Binary representation** | 65537 in binary = 10000000000000001 — only two 1-bits |
| **Fast exponentiation** | Square-and-multiply needs only 17 squarings and 1 multiplication — very fast |
| **Security** | Large enough to avoid small-exponent attacks (e=3 is vulnerable) |
| **Coprime guarantee** | For virtually all practical key pairs, gcd(65537, φ(n)) = 1 |

**Why NOT use e = 3?**
- Small exponent attack: If M³ < n (small message), C = M³ mod n = M³
  (no modular reduction) → cube root of C directly gives M
- RSA with e=3 and no padding is vulnerable

---

### 3.9 RSA Padding Schemes — PKCS#1 v1.5 vs OAEP

> [!NOTE]
> Raw RSA (textbook RSA) without padding is insecure.
> Padding schemes add randomness and structure to prevent attacks.

| Padding | Full Name | Year | Security | Use |
|---------|-----------|------|---------|-----|
| **PKCS#1 v1.5** | Public Key Cryptography Standard #1 v1.5 | 1993 | ⚠️ Vulnerable to Bleichenbacher attack | Legacy TLS, email |
| **OAEP** | Optimal Asymmetric Encryption Padding | 1994 | ✅ Secure — CCA2 secure | Recommended for new systems |
| **PSS** | Probabilistic Signature Scheme | 1996 | ✅ Secure | RSA signatures (recommended) |
| **PKCS#1 v1.5 (sig)** | — | 1993 | ⚠️ Secure but older | Legacy signatures |

**Bleichenbacher Attack (1998):**
- Exploits PKCS#1 v1.5 padding format in RSA encryption
- An attacker sends modified ciphertext to a server and
  observes whether the server accepts or rejects the padding
- Through millions of such queries → recovers the plaintext
- **SSL/TLS ROBOT attack (2017)** — rediscovered that many
  HTTPS servers were still vulnerable to Bleichenbacher

> [!IMPORTANT]
> **OAEP** is the recommended padding for RSA encryption.
> **PSS** is the recommended padding for RSA signatures.
> Both are specified in PKCS#1 v2.x (RFC 8017).

---

### 3.10 RSA Attacks

> [!NOTE]

| Attack | Description | Countermeasure |
|--------|-------------|---------------|
| **Brute force / Factoring** | Factor n to find p and q | Use n ≥ 2048 bits |
| **Small exponent attack** | e=3 with small M → C = M³ (no mod reduction) | Use e=65537 + padding |
| **Bleichenbacher attack** | PKCS#1 v1.5 padding oracle | Use OAEP padding |
| **Timing attack** | Measure decryption time to infer d | Constant-time implementation |
| **Common modulus attack** | Two users share same n but different e → private key recoverable | Never share modulus |
| **Low private exponent** | Small d → vulnerable to Wiener's attack | d must be large |
| **Chosen ciphertext attack** | RSA without padding is malleable | Always use padding |

---

### 3.11 ECC — ECDH and ECDSA

> [!NOTE]
> ECC is the mathematical framework — ECDH and ECDSA are its
> two primary protocol applications.

#### ECDH — Elliptic Curve Diffie-Hellman
**Use:** Key Exchange — establishing a shared secret

```
Parameters: Both parties agree on curve and generator point G

Alice:
  Private key: a (random integer)
  Public key:  A = a × G

Bob:
  Private key: b (random integer)
  Public key:  B = b × G

Key Exchange:
  Alice sends A to Bob; Bob sends B to Alice

Shared Secret:
  Alice: S = a × B = a × (b × G) = ab × G
  Bob:   S = b × A = b × (a × G) = ab × G
  S is the same for both → shared secret ✅

Attacker:
  Sees A and B but needs a or b to compute ab × G
  → ECDLP → infeasible
```

**ECDHE (Ephemeral ECDH):** New key pairs per session → PFS

#### ECDSA — Elliptic Curve Digital Signature Algorithm
**Use:** Digital Signatures — authentication + non-repudiation

```
Signing (Alice):
  1. Compute hash e = Hash(message)
  2. Choose random k (nonce) — k must be unique per signature
  3. Compute point (x, y) = k × G
  4. Compute r = x mod n
  5. Compute s = k⁻¹(e + r × privateKey) mod n
  6. Signature = (r, s)

Verification (Bob):
  1. Compute hash e = Hash(message)
  2. Compute w = s⁻¹ mod n
  3. Compute u₁ = e × w mod n, u₂ = r × w mod n
  4. Compute point (x, y) = u₁ × G + u₂ × PublicKey
  5. Verify: r ≡ x (mod n) ✅ → signature valid
```

> [!IMPORTANT]
> **ECDSA nonce k must NEVER be reused.**
> If the same k is used in two signatures (r₁ = r₂):
> → The private key can be algebraically recovered.
> **Real-world breach:** Sony PlayStation 3 (2010) — reused k=1
> in all ECDSA signatures → private key extracted → all PS3
> firmware signing keys compromised.

---

### 3.12 ECC Curves — NIST vs Curve25519

> [!NOTE]

| Property | NIST Curves (P-256, P-384) | Curve25519 |
|----------|--------------------------|------------|
| **Standardized by** | NIST (NSA-influenced selection) | Daniel J. Bernstein (2005) |
| **Parameters** | Random-looking constants | Chosen for performance + security proofs |
| **NSA influence suspicion** | ⚠️ Some cryptographers suspicious of constants | ✅ Transparent, verifiable |
| **Side-channel resistance** | Requires careful implementation | ✅ Built-in by design |
| **Performance** | Fast | Faster |
| **Adoption** | TLS certificates, ECDSA | Signal, WhatsApp, SSH (OpenSSH default), TLS 1.3 |
| **RFC** | RFC 5480 | RFC 7748 (X25519), RFC 8032 (Ed25519) |

> Curve25519 (for key exchange, X25519) and Ed25519 (for
> signatures) are increasingly recommended as the modern
> default for new system designs.

---

### 3.13 Symmetric Algorithm Comparison Table — All Algorithms

> [!NOTE]

| Algorithm | Year | Block | Key Size | Rounds | Structure | Status |
|-----------|------|-------|---------|--------|-----------|--------|
| **DES** | 1977 | 64-bit | 56-bit | 16 | Feistel | ❌ Broken |
| **2DES** | — | 64-bit | 112-bit | 32 | Feistel | ❌ MitM attack |
| **3DES** | 1999 | 64-bit | 112/168-bit | 48 | Feistel | ⚠️ Deprecated 2023 |
| **AES-128** | 2001 | 128-bit | 128-bit | 10 | SPN | ✅ Current standard |
| **AES-192** | 2001 | 128-bit | 192-bit | 12 | SPN | ✅ Secure |
| **AES-256** | 2001 | 128-bit | 256-bit | 14 | SPN | ✅ Quantum-safe candidate |
| **RC2** | 1987 | 64-bit | 8–128-bit | 18 | Feistel | ❌ Deprecated |
| **RC4** | 1987 | Stream | 40–2048-bit | — | Stream | ❌ Broken |
| **RC5** | 1994 | 64-bit (var) | 0–2040-bit | 0–255 | Feistel-like | ⚠️ Obsolete |
| **RC6** | 1998 | 128-bit | 128/192/256-bit | 20 | Feistel-like | ⚠️ Rarely used |
| **Blowfish** | 1993 | 64-bit | 32–448-bit | 16 | Feistel | ⚠️ Aging — Sweet32 |
| **Twofish** | 1998 | 128-bit | 128/192/256-bit | 16 | Feistel | ✅ Secure — rarely used |
| **ChaCha20** | 2008 | Stream | 256-bit | 20 | ARX | ✅ Modern — TLS 1.3 |

---

### 3.14 Asymmetric Algorithm Comparison Table — All Algorithms

> [!NOTE]

| Algorithm | Year | Hard Problem | Key Exchange | Encryption | Signature | Status |
|-----------|------|-------------|-------------|-----------|----------|--------|
| **RSA** | 1977 | Factoring | ✅ (key transport) | ✅ | ✅ | ✅ 2048+ |
| **Diffie-Hellman** | 1976 | DLP | ✅ | ❌ | ❌ | ✅ 2048+ |
| **DSA** | 1991 | DLP | ❌ | ❌ | ✅ only | ⚠️ Aging |
| **ElGamal** | 1984 | DLP | ✅ | ✅ | ✅ | ⚠️ Rarely direct |
| **ECC** | 1985 | ECDLP | ✅ (ECDH) | ✅ (ECIES) | ✅ (ECDSA) | ✅ Current |
| **ECDH** | 1992 | ECDLP | ✅ | ❌ | ❌ | ✅ Current |
| **ECDSA** | 1992 | ECDLP | ❌ | ❌ | ✅ only | ✅ Current |
| **Ed25519** | 2011 | ECDLP | ❌ | ❌ | ✅ only | ✅ Modern |
| **X25519** | 2005 | ECDLP | ✅ | ❌ | ❌ | ✅ Modern |

---

### 3.15 NIST Recommended Key Sizes — 2024

> [!NOTE]
> From NIST SP 800-57 Part 1 Rev. 5

| Security Level | Symmetric | RSA/DH | ECC |
|---------------|-----------|--------|-----|
| **80-bit** | 2TDEA (deprecated) | 1024-bit | 160-bit |
| **112-bit** | 3TDEA (deprecated 2023) | 2048-bit | 224-bit |
| **128-bit** | AES-128 | 3072-bit | 256-bit |
| **192-bit** | AES-192 | 7680-bit | 384-bit |
| **256-bit** | AES-256 | 15360-bit | 512-bit |

> [!IMPORTANT]
> The **112-bit security level** (RSA-2048, 3TDEA) is the current
> minimum. However, NIST recommends transitioning to
> **128-bit security** (AES-128, RSA-3072, P-256) for
> systems needing security beyond 2030.
>
> The enormous RSA key size needed to match AES-256 security
> (15360-bit RSA = 512-bit ECC = AES-256) demonstrates why
> RSA is impractical at high security levels and why ECC
> is the preferred asymmetric algorithm for modern systems.

---

## 4. Abbreviations Table

| Abbreviation | Full Form | One-Line Technical Meaning |
|---|---|---|
| DES | Data Encryption Standard | 56-bit symmetric block cipher — 64-bit blocks, 16 Feistel rounds — broken |
| 3DES | Triple DES | DES applied three times with E-D-E pattern — deprecated 2023 |
| AES | Advanced Encryption Standard | 128/192/256-bit block cipher — 128-bit blocks — SPN structure — current standard |
| SPN | Substitution-Permutation Network | Block cipher structure using alternating S-Box and permutation layers — used by AES |
| RC5 | Rivest Cipher 5 | Variable block/key/round block cipher by Ron Rivest — uses data-dependent rotations |
| NBS | National Bureau of Standards | Former name of NIST — standardized DES in 1977 |
| FIPS | Federal Information Processing Standard | US government cryptographic standards issued by NIST |
| RSA | Rivest-Shamir-Adleman | Asymmetric algorithm based on integer factorization — encryption and signatures |
| ECC | Elliptic Curve Cryptography | Asymmetric cryptography based on ECDLP — smaller keys than RSA |
| ECDH | Elliptic Curve Diffie-Hellman | ECC-based key exchange protocol |
| ECDHE | Elliptic Curve Diffie-Hellman Ephemeral | ECDH with temporary keys — provides Perfect Forward Secrecy |
| ECDSA | Elliptic Curve Digital Signature Algorithm | ECC-based digital signature algorithm |
| ECDLP | Elliptic Curve Discrete Logarithm Problem | Hard math problem: find k given P = k×G — basis of ECC security |
| OAEP | Optimal Asymmetric Encryption Padding | Secure RSA padding scheme — CCA2-secure — recommended over PKCS#1 v1.5 |
| PSS | Probabilistic Signature Scheme | Secure RSA signature padding scheme — recommended for new RSA signatures |
| MitM | Meet-in-the-Middle | Attack against 2DES — reduces effective key length from 112 to ~57 bits |
| EDE | Encrypt-Decrypt-Encrypt | 3DES operation order — provides backward compatibility with single DES |
| GCM | Galois/Counter Mode | AES mode providing authenticated encryption — used in TLS 1.3 |
| CCM | Counter with CBC-MAC | AES authenticated encryption mode — used in IoT and Wi-Fi |
| AES-NI | AES New Instructions | CPU hardware instructions for accelerating AES — 10–20× faster than software |
| ARX | Add-Rotate-XOR | Stream cipher design using only addition, rotation, and XOR — used in ChaCha20 |
| KDF | Key Derivation Function | Derives cryptographic key from password or shared secret |
| EFF | Electronic Frontier Foundation | Organization that built Deep Crack and broke DES in 56 hours (1998) |

---

## 5. Keywords + Concept Map

| Term | Definition | Connections | Use Cases |
|------|-----------|-------------|-----------|
| **DES** | 56-bit symmetric block cipher — 16 Feistel rounds | Broken, replaced by AES, basis of 3DES | Historical reference, 3DES context |
| **3DES** | DES applied 3× with E-D-E pattern | Resists MitM attack, deprecated 2023 | Legacy banking, SWIFT |
| **AES** | 128-bit block SPN cipher — 10/12/14 rounds | Replaced DES, FIPS 197, Session 05 CrypTool | All modern encryption |
| **SubBytes** | AES S-Box byte substitution | Shannon Confusion, non-linearity | AES round operation |
| **ShiftRows** | AES row cyclic shift | Shannon Diffusion, spreads bytes | AES round operation |
| **MixColumns** | AES column polynomial multiplication | Shannon Diffusion, maximum mixing | AES round operation (not in last round) |
| **AddRoundKey** | AES XOR with round key | Key mixing, Kerckhoffs | AES round operation — only keyed step |
| **RC5** | Variable parameter block cipher | Data-dependent rotations, RC family | Historical, CrypTool lab |
| **RSA** | Asymmetric cipher — integer factorization | Hybrid encryption, PKI, TLS, S/MIME | Encryption, signatures, key transport |
| **e = 65537** | Standard RSA public exponent | Fermat prime, fast, secure | All practical RSA implementations |
| **OAEP** | RSA padding — CCA2 secure | Replaces PKCS#1 v1.5, RFC 8017 | RSA encryption |
| **ECC** | Asymmetric crypto — ECDLP basis | Smaller keys than RSA, ECDH, ECDSA | Mobile, TLS, IoT, blockchain |
| **P-256** | Most common NIST ECC curve | TLS, ECDSA, Android, iOS | Web security, code signing |
| **Curve25519** | Bernstein's modern ECC curve | Signal, WhatsApp, SSH, TLS 1.3 | Modern secure communications |
| **ECDH** | ECC-based key exchange | Hybrid encryption, PFS when ephemeral | TLS session key establishment |
| **ECDSA nonce** | Random k in signature — must be unique | PS3 breach (reused k=1), private key recovery | Secure signature implementation |
| **Sweet32** | Birthday attack on 64-bit block ciphers | Breaks 3DES/Blowfish over long sessions | Reason for AES 128-bit block size |
| **Meet-in-Middle** | Attack reducing 2DES to ~57-bit security | Why 2DES was never standardized | 3DES uses E-D-E to resist this |

---

## 6. Quick Reference Cheatsheet

### 🔸 DES vs AES — Critical Numbers

| Property | DES | AES-128 | AES-192 | AES-256 |
|----------|-----|---------|---------|---------|
| Block size | 64-bit | 128-bit | 128-bit | 128-bit |
| Key size | 56-bit eff. | 128-bit | 192-bit | 256-bit |
| Rounds | 16 | 10 | 12 | 14 |
| Structure | Feistel | SPN | SPN | SPN |
| Status | ❌ Broken | ✅ Secure | ✅ Secure | ✅ Secure |

---

### 🔸 AES Round Operations — Shannon Mapping

| Operation | Shannon Property | Mechanism |
|-----------|----------------|-----------|
| SubBytes | Confusion | S-Box lookup |
| ShiftRows | Diffusion | Row cyclic shift |
| MixColumns | Diffusion | Polynomial multiplication |
| AddRoundKey | Key mixing | XOR with round key |

> MixColumns is **skipped in the final round.**

---

### 🔸 RSA Key Generation — Critical Steps

```
1. Choose primes p, q
2. n = p × q  (modulus)
3. φ(n) = (p-1)(q-1)
4. Choose e: gcd(e, φ(n)) = 1, e = 65537 (standard)
5. d = e⁻¹ mod φ(n)  (private exponent)
6. Public Key = (e, n)  |  Private Key = (d, n)
7. Discard p, q, φ(n)

Encrypt: C = Mᵉ mod n
Decrypt: M = Cᵈ mod n
```

---

### 🔸 Security Equivalence — Key Size Cross-Reference

| Security Level | AES | RSA | ECC |
|---------------|-----|-----|-----|
| 80-bit | — | 1024-bit ❌ | 160-bit |
| 112-bit | — | 2048-bit | 224-bit |
| 128-bit | AES-128 | 3072-bit | P-256 (256-bit) |
| 192-bit | AES-192 | 7680-bit | P-384 (384-bit) |
| 256-bit | AES-256 | 15360-bit | 512-bit |

---

### 🔸 ECC Named Curves Quick Reference

| Curve | Size | Use | Standardized By |
|-------|------|-----|----------------|
| P-256 / secp256r1 | 256-bit | TLS, ECDSA | NIST |
| P-384 / secp384r1 | 384-bit | High security | NIST |
| P-521 / secp521r1 | 521-bit | Highest NIST | NIST |
| Curve25519 / X25519 | 255-bit | Key exchange — modern | Bernstein |
| Ed25519 | 255-bit | Signatures — modern | Bernstein |
| secp256k1 | 256-bit | Bitcoin/Ethereum | SECG |

---

### 🔸 Symmetric Algorithm Status Summary

| Algorithm | Status | Replaced By |
|-----------|--------|------------|
| DES | ❌ Broken | AES |
| 2DES | ❌ Never standardized | AES |
| 3DES | ⚠️ Deprecated 2023 | AES |
| RC4 | ❌ Broken | ChaCha20 |
| RC5 | ⚠️ Obsolete | AES |
| AES-128/192/256 | ✅ Current standard | — |
| ChaCha20 | ✅ Modern | — |

---

### 🔸 RSA Padding Schemes

| Scheme | Purpose | Security | Recommended? |
|--------|---------|---------|-------------|
| No padding (textbook RSA) | — | ❌ Insecure | Never |
| PKCS#1 v1.5 | Encryption | ⚠️ Bleichenbacher | Legacy only |
| OAEP | Encryption | ✅ CCA2-secure | ✅ Yes |
| PKCS#1 v1.5 sig | Signature | ⚠️ Acceptable | Legacy |
| PSS | Signature | ✅ Secure | ✅ Yes |

---

## 7. Session Revision Snapshot

### ⚡ TL;DR — 5 Bullets

- ✅ DES = 56-bit key, 64-bit block, 16 Feistel rounds — broken in 1998 by Deep Crack in 56 hours — replaced by AES
- ✅ AES = 128/192/256-bit key, ALWAYS 128-bit block, 10/12/14 rounds, SPN structure (NOT Feistel) — SubBytes (confusion) + ShiftRows/MixColumns (diffusion) + AddRoundKey (key mix)
- ✅ RSA security = hardness of factoring n = p×q — key generation requires modular inverse: d = e⁻¹ mod φ(n) — minimum 2048-bit today
- ✅ ECC security = ECDLP hardness — P = k×G easy, finding k from P and G is infeasible — 256-bit ECC ≈ 3072-bit RSA ≈ 128-bit AES security
- ✅ 3DES uses E-D-E (not E-E-E) to resist Meet-in-the-Middle attack — deprecated by NIST in 2023 due to Sweet32 and 64-bit block size limitation

---

### 🎯 MCQ-Likely Concepts — Everything Examiners Love

| Concept | Why It's Tricky |
|---------|----------------|
| AES block size is ALWAYS 128-bit | AES-256 uses 256-bit KEY but 128-bit BLOCK — very commonly confused |
| AES structure = SPN not Feistel | DES = Feistel, AES = SPN — exact opposite of what some expect |
| MixColumns skipped in AES final round | Almost no one remembers this specific detail |
| DES effective key = 56-bit not 64-bit | 8 parity bits — key input is 64 bits but security is 56 bits |
| 3DES uses E-D-E not E-E-E | The decode step in the middle is deliberate — backward compat |
| 2DES reduces to ~57-bit via MitM attack | Naive expectation of 112 bits is wrong |
| RSA public exponent e = 65537 = 2¹⁶ + 1 | Fermat prime, fast, secure — specific value commonly tested |
| d = e⁻¹ mod φ(n) | Modular inverse — private exponent derivation formula |
| 256-bit ECC ≈ 3072-bit RSA ≈ AES-128 | Key equivalence table — three-way mapping |
| ECDSA nonce k reuse → private key recovery | PS3 breach is the canonical example |
| OAEP for encryption, PSS for signatures | Many students confuse which padding serves which purpose |
| RC4 broken — deprecated by RFC 7465 | Specific RFC number for TLS prohibition |
| Sweet32 = birthday attack on 64-bit blocks | Affects 3DES and Blowfish — 128-bit AES blocks immune |
| AES-NI = hardware CPU instructions for AES | 10-20× performance boost — available Intel 2010, AMD 2011 |
| secp256k1 = Bitcoin's curve (not NIST P-256) | Similar names — commonly confused |

---

<details>
<summary>🔬 Lab Content (Session 04 — No Lab Assigned)</summary>

No lab is assigned for Session 04 in the syllabus.

Lab work for symmetric and asymmetric algorithms begins in
**Session 05 using CrypTool**, which covers:

**Symmetric algorithms from this session:**
- DES encryption/decryption
- AES (128/256) encryption/decryption
- 3DES encryption/decryption
- RC5 encryption/decryption

**Asymmetric algorithms from this session:**
- RSA key generation and encryption
- ECC key generation

The full step-by-step CrypTool lab guide will be in:
`3-Labs/lab-session-05-cryptool.md`

The mathematical foundations covered in Session 04 (DES rounds,
AES operations, RSA key generation formula, ECC scalar
multiplication) are essential for understanding what CrypTool
is demonstrating in that lab.

</details>

---