# MCQ Session 02 — Basic Encryption Concepts, File Encryption & Encrypting Folders

## 📑 Table of Contents
- [Instructions](#instructions)
- [MCQs 1–7 — Core Encryption Concepts](#mcqs-17--core-encryption-concepts)
- [MCQs 8–13 — Kerckhoffs, Shannon, Key Space](#mcqs-813--kerckhoffs-shannon-key-space)
- [MCQs 14–19 — EFS, File Encryption, cipher.exe](#mcqs-1419--efs-file-encryption-cipherexe)
- [MCQs 20–25 — Extra Notes: Block Ciphers, BitLocker, Steganography, Mistakes](#mcqs-2025--extra-notes-block-ciphers-bitlocker-steganography-mistakes)
- [Answer Key](#-answer-key--quick-reference)

---

## Instructions

- 25 MCQs — drawn from core syllabus AND 📌 Extra Notes of Session 02
- 4 options per question
- ✅ marks the correct answer
- Full explanation after every question — including **why each wrong option is wrong**
- Questions are deliberately tricky — one-word differences, close options, common inversion traps

---

## MCQs 1–7 — Core Encryption Concepts

---

**Q1. Which of the following MOST accurately defines encryption?**

- A) Converting data into a format that cannot be recovered under any circumstance
- B) Transforming plaintext into ciphertext using an algorithm and a key, reversible only with the correct key ✅
- C) Encoding data into a different representation to prevent unauthorized viewing
- D) Compressing data to reduce its size and obscure its contents

> **Explanation:**
> - ✅ **B:** Encryption is a reversible transformation from plaintext to ciphertext using an algorithm and a key — it is reversible by the authorized party with the correct key.
> - ❌ **A:** "Cannot be recovered under any circumstance" describes a one-way function (hashing), not encryption. Encryption is designed to be reversible.
> - ❌ **C:** This describes encoding (e.g., Base64), not encryption. Encoding requires no key and is not a security mechanism.
> - ❌ **D:** Compression reduces size but does not provide security. It is not encryption and provides no confidentiality guarantee.

---

**Q2. What is the correct formal relationship between Cryptography, Cryptanalysis, and Cryptology?**

- A) Cryptology is a subset of Cryptography
- B) Cryptanalysis is a subset of Cryptography
- C) Cryptography and Cryptanalysis are both subsets of Cryptology ✅
- D) Cryptography and Cryptology are the same discipline with different names

> **Explanation:**
> - ✅ **C:** Cryptology is the parent discipline encompassing both Cryptography (designing secure systems) and Cryptanalysis (breaking those systems).
> - ❌ **A:** This inverts the relationship — Cryptology is the broader field, not a subset.
> - ❌ **B:** Cryptanalysis is not a subset of Cryptography — they are siblings under Cryptology.
> - ❌ **D:** Cryptography and Cryptology are NOT synonyms — Cryptography is the design side only; Cryptology includes both design and breaking.

---

**Q3. An attacker intercepts a ciphertext and modifies specific bytes before forwarding it to the receiver. The receiver decrypts it and gets garbled data. Which security property was NOT protected by encryption alone?**

- A) Confidentiality
- B) Availability
- C) Integrity ✅
- D) Authentication

> **Explanation:**
> - ✅ **C — Integrity:** Encryption protects confidentiality (the attacker couldn't read the content), but it does NOT protect integrity — an attacker can flip bits in ciphertext and cause corrupted plaintext on decryption without knowing the key.
> - ❌ **A — Confidentiality:** The attacker modified but could not read the content — confidentiality was maintained.
> - ❌ **B — Availability:** The data was received and decrypted (even if garbled) — availability was not disrupted.
> - ❌ **D — Authentication:** Authentication was not the focus here — the attack was about data modification, not identity.

> [!NOTE]
> This is why **Authenticated Encryption** (AES-GCM) exists — it provides both confidentiality AND integrity simultaneously. Encryption alone only covers confidentiality.

---

**Q4. In the formal encryption model, which expression correctly represents the decryption operation?**

- A) Y = E(K, X)
- B) X = E(K, Y)
- C) X = D(K, Y) ✅
- D) Y = D(K, X)

> **Explanation:**
> - ✅ **C — X = D(K, Y):** Decryption (D) takes the ciphertext (Y) and the key (K) and produces the original plaintext (X).
> - ❌ **A — Y = E(K, X):** This is the encryption operation — not decryption. E = encrypt, X = plaintext, Y = ciphertext.
> - ❌ **B — X = E(K, Y):** This applies the Encryption function to the ciphertext — logically incorrect. The Decryption function (D) must be applied to ciphertext.
> - ❌ **D — Y = D(K, X):** This applies Decryption to plaintext (X) and outputs ciphertext (Y) — this is the wrong direction entirely.

---

**Q5. Which of the following is the MOST critical distinction between encoding and encryption?**

- A) Encoding uses a longer key than encryption
- B) Encoding is irreversible; encryption is reversible
- C) Encryption requires a key; encoding does not ✅
- D) Encoding is used only for text; encryption works on all data types

> **Explanation:**
> - ✅ **C:** The fundamental distinction is the key — encoding (e.g., Base64) requires no key and can be reversed by anyone. Encryption requires a key and can only be reversed by someone with the correct key.
> - ❌ **A:** Encoding does not use a key at all — comparing key lengths is meaningless here.
> - ❌ **B:** This is completely inverted. Encoding IS reversible (that is its purpose — format conversion). Encryption IS reversible (with the correct key). Hashing is irreversible.
> - ❌ **D:** Both encoding and encryption work on all data types — this is not a valid distinguishing factor.

---

**Q6. A developer stores a password as `cGFzc3dvcmQ=` in a database, claiming it is "encrypted." What is the ACTUAL operation performed and what is the security implication?**

- A) It is encrypted with AES — it is secure
- B) It is hashed — it cannot be reversed
- C) It is Base64 encoded — it provides NO security and is trivially reversible ✅
- D) It is encrypted with DES — it is weakly secured

> **Explanation:**
> - ✅ **C:** `cGFzc3dvcmQ=` is the Base64 encoding of "password". Base64 is a pure encoding scheme — no key, no algorithm, completely reversible by anyone using any Base64 decoder. It provides ZERO security.
> - ❌ **A:** AES encryption produces binary/hex output, not a human-readable Base64 string like this (unless the AES output is additionally Base64-encoded, which is different). More importantly, the claim that it "is secure" is wrong regardless.
> - ❌ **B:** Hashing is one-way — but `cGFzc3dvcmQ=` is not a hash. Hash outputs have fixed lengths (e.g., SHA-256 = 64 hex chars). The `=` padding at the end is a telltale sign of Base64.
> - ❌ **D:** DES output would not look like this. DES is symmetric encryption, not encoding.

---

**Q7. Which of the following pairs CORRECTLY maps each operation to its primary security goal?**

- A) Hashing → Confidentiality, Encryption → Integrity
- B) Encryption → Confidentiality, Hashing → Integrity ✅
- C) Encoding → Confidentiality, Hashing → Non-repudiation
- D) Encryption → Non-repudiation, Hashing → Confidentiality

> **Explanation:**
> - ✅ **B:** Encryption's primary goal is Confidentiality (protecting data from unauthorized reading). Hashing's primary goal is Integrity (verifying data has not been altered).
> - ❌ **A:** This completely swaps the goals — hashing does NOT provide confidentiality, and encryption alone does NOT provide integrity.
> - ❌ **C:** Encoding provides NO security goal — it is not a security mechanism. Hashing does not provide non-repudiation — digital signatures do.
> - ❌ **D:** Non-repudiation is provided by digital signatures (hashing + asymmetric encryption together) — not by encryption alone. Hashing does not provide confidentiality.

---

## MCQs 8–13 — Kerckhoffs, Shannon, Key Space

---

**Q8. Kerckhoffs's Principle states that a cryptosystem should be secure even if:**

- A) The key is made public, as long as the algorithm is kept secret
- B) Both the key and the algorithm are made public
- C) Everything about the system except the key is public knowledge ✅
- D) The algorithm is kept secret and only shared with trusted parties

> **Explanation:**
> - ✅ **C:** Kerckhoffs's Principle (1883) states that a cryptosystem must remain secure even when everything about it — the algorithm, the ciphertext, the system design — is publicly known. Only the key must be kept secret.
> - ❌ **A:** This completely inverts the principle — the KEY must be secret, not the algorithm. Keeping only the algorithm secret is "security through obscurity."
> - ❌ **B:** Making both the key AND the algorithm public would defeat security entirely — the key must always remain secret.
> - ❌ **D:** Requiring algorithm secrecy is exactly what Kerckhoffs argued AGAINST. Shared secretly still implies algorithm secrecy is relied upon — which violates the principle.

---

**Q9. A company develops a proprietary encryption algorithm and keeps it secret, claiming that secrecy of the algorithm makes it secure. Which principle does this approach violate?**

- A) Shannon's Diffusion
- B) The CIA Triad
- C) Kerckhoffs's Principle ✅
- D) Defence in Depth

> **Explanation:**
> - ✅ **C — Kerckhoffs's Principle:** Relying on algorithm secrecy for security is precisely what Kerckhoffs argued against. This is "security through obscurity" — once the algorithm is reverse-engineered or leaked, all security collapses.
> - ❌ **A — Shannon's Diffusion:** Diffusion is a design property (spreading plaintext across ciphertext) — it is not about whether an algorithm should be public or secret.
> - ❌ **B — CIA Triad:** The CIA Triad defines security goals — it does not address algorithm design philosophy.
> - ❌ **D — Defence in Depth:** DiD is about layered controls — not about algorithm transparency.

---

**Q10. Shannon's property of CONFUSION is best described as:**

- A) Spreading the influence of a single plaintext bit across many ciphertext bits
- B) Making the relationship between the ciphertext and the key as complex as possible ✅
- C) Rearranging the order of characters in the plaintext
- D) Inserting dummy bits into the message to disguise its length

> **Explanation:**
> - ✅ **B — Confusion:** Confusion makes the relationship between the key and the ciphertext complex and non-linear, so that attackers cannot deduce the key from studying the ciphertext. It is achieved through substitution.
> - ❌ **A:** This describes **Diffusion**, not Confusion. Diffusion spreads plaintext influence — Confusion hides the key relationship.
> - ❌ **C:** Rearranging characters describes Transposition, which is the mechanism behind Diffusion — not Confusion.
> - ❌ **D:** Inserting dummy bits describes **Traffic Padding** (X.800 security mechanism) — completely unrelated to Shannon's Confusion.

---

**Q11. In AES, which specific operation implements Shannon's property of DIFFUSION?**

- A) SubBytes
- B) AddRoundKey
- C) ShiftRows and MixColumns ✅
- D) KeyExpansion

> **Explanation:**
> - ✅ **C — ShiftRows and MixColumns:** These two operations together spread (diffuse) the influence of each plaintext byte across multiple output bytes, implementing Diffusion.
> - ❌ **A — SubBytes:** SubBytes is the substitution step — it implements **Confusion** (hides key-ciphertext relationship), not Diffusion.
> - ❌ **B — AddRoundKey:** AddRoundKey XORs the state with the round key — it contributes to key mixing but is not specifically the Diffusion step.
> - ❌ **D — KeyExpansion:** KeyExpansion generates the round keys from the original key — it is a key schedule operation, not a Confusion or Diffusion step.

---

**Q12. A cryptographic key is increased from 56 bits to 57 bits. What is the effect on the key space?**

- A) The key space increases by 57 additional keys
- B) The key space increases by 56 additional keys
- C) The key space doubles ✅
- D) The key space increases by 12.5%

> **Explanation:**
> - ✅ **C — Doubles:** Key space = 2^(key length). At 56 bits: 2⁵⁶ possible keys. At 57 bits: 2⁵⁷ = 2 × 2⁵⁶. Each additional bit exactly doubles the key space.
> - ❌ **A:** Adding bits multiplies the key space exponentially — not additively. +57 keys is negligible against a 2⁵⁶ key space.
> - ❌ **B:** Same issue as A — additive thinking is wrong. Key spaces grow exponentially.
> - ❌ **D:** 12.5% is far too small — the key space doubles (100% increase) with every single bit added.

---

**Q13. Which of the following statements about key length and security is CORRECT?**

- A) A longer key always guarantees stronger security regardless of the algorithm used
- B) Key length is the only factor that determines encryption strength
- C) Both algorithm strength AND key length together determine encryption security ✅
- D) Algorithm strength is irrelevant as long as the key is longer than 128 bits

> **Explanation:**
> - ✅ **C:** Security depends on BOTH the algorithm's mathematical strength AND the key length. A 256-bit key used with a broken algorithm is still insecure.
> - ❌ **A:** "Regardless of the algorithm" is wrong — a 256-bit key in a fundamentally broken cipher (e.g., a simple XOR with a repeating key) provides minimal security.
> - ❌ **B:** Algorithm design, implementation quality, mode of operation, and key management all contribute to security — key length alone is insufficient.
> - ❌ **D:** Algorithm strength is never irrelevant. There are 128-bit key ciphers that are broken due to algorithmic flaws — key length alone did not save them.

---

## MCQs 14–19 — EFS, File Encryption, cipher.exe

---

**Q14. Windows EFS (Encrypting File System) can ONLY operate on which type of file system?**

- A) FAT32
- B) exFAT
- C) NTFS ✅
- D) ReFS

> **Explanation:**
> - ✅ **C — NTFS:** EFS is an NTFS feature — it is built into the NTFS driver. It cannot operate on FAT32, exFAT, or other file systems.
> - ❌ **A — FAT32:** EFS does not work on FAT32. In fact, copying an EFS-encrypted file TO a FAT32 drive silently decrypts it.
> - ❌ **B — exFAT:** exFAT is commonly used on USB drives — EFS is not available on exFAT.
> - ❌ **D — ReFS:** ReFS (Resilient File System) is a newer Microsoft file system — EFS is not natively supported on ReFS volumes.

---

**Q15. A user with Windows EFS encrypts a file and then copies it to a USB drive formatted as FAT32. What happens to the file on the USB drive?**

- A) The file remains encrypted — EFS travels with the file
- B) The file is automatically re-encrypted using BitLocker
- C) The file is silently decrypted and stored as plaintext ✅
- D) The copy operation fails with an error message

> **Explanation:**
> - ✅ **C — Silently decrypted:** When an EFS-encrypted file is copied to a non-NTFS volume (like FAT32), Windows automatically decrypts it because EFS cannot exist outside NTFS. The decryption is silent — no warning is shown by default. This is a well-known data exposure risk.
> - ❌ **A:** EFS does NOT travel with the file — it is a filesystem-level feature tied to NTFS. The encryption does not follow the file to a FAT32 drive.
> - ❌ **B:** BitLocker is a full-disk encryption solution — it does not automatically re-encrypt individual files copied to external drives.
> - ❌ **D:** Windows does not block the copy operation — it completes successfully but without encryption, creating a silent security failure.

---

**Q16. In the EFS internal architecture, the File Encryption Key (FEK) is protected by which mechanism?**

- A) The FEK is hashed using SHA-256 and stored in the DDF
- B) The FEK is encrypted using the user's RSA Public Key and stored in the DDF ✅
- C) The FEK is encrypted using AES-256 and stored in plaintext in the DRF
- D) The FEK is derived from the user's Windows login password using PBKDF2

> **Explanation:**
> - ✅ **B:** In EFS, the FEK (a symmetric AES key) is encrypted using the user's RSA Public Key (from their EFS certificate) and stored in the DDF (Data Decryption Field). This is hybrid encryption — AES for data, RSA to protect the AES key.
> - ❌ **A:** The FEK is not hashed — hashing is one-way and the FEK needs to be recoverable for decryption. It is encrypted, not hashed.
> - ❌ **C:** The DRF (Data Recovery Field) stores a copy of the FEK encrypted with the Recovery Agent's public key — not the user's FEK in plaintext. Storing anything in plaintext in the DRF would be a critical security failure.
> - ❌ **D:** PBKDF2 is a key derivation function used for password hashing (e.g., in Wi-Fi WPA2) — EFS does not derive the FEK from a login password.

---

**Q17. What is the purpose of the Data Recovery Field (DRF) in EFS?**

- A) It stores a backup of the ciphertext file in case of disk failure
- B) It stores the FEK encrypted with the Recovery Agent's public key, enabling recovery if the user's key is lost ✅
- C) It stores the user's private key encrypted with a master password
- D) It stores the EFS certificate revocation list (CRL) for the current user

> **Explanation:**
> - ✅ **B:** The DRF stores a copy of the FEK encrypted with the Recovery Agent's RSA public key. If the original user's private key is lost, the Recovery Agent can use their own private key to decrypt the DRF copy of the FEK and recover the file.
> - ❌ **A:** The DRF contains key material — not a copy of the file itself. It is metadata attached to each encrypted file.
> - ❌ **C:** EFS does not store the user's private key in the DRF — private keys are stored in the user's key store/certificate store, not in file metadata.
> - ❌ **D:** CRLs are managed by Certificate Authorities — the DRF has no relationship to certificate revocation.

---

**Q18. Which `cipher.exe` command encrypts a folder AND all its subfolders and files recursively?**

- A) `cipher /e foldername`
- B) `cipher /e /r:foldername`
- C) `cipher /e /s:foldername` ✅
- D) `cipher /encrypt /all foldername`

> **Explanation:**
> - ✅ **C — `cipher /e /s:foldername`:** The `/e` switch encrypts and `/s:` applies the operation to the specified folder and all its subfolders and files recursively.
> - ❌ **A — `cipher /e foldername`:** This encrypts the folder itself (marks it for encryption) but does NOT recursively encrypt existing files inside it.
> - ❌ **B — `cipher /e /r:foldername`:** The `/r:` switch is used to generate a Recovery Agent certificate and key — it is completely unrelated to encrypting folders.
> - ❌ **D — `cipher /encrypt /all foldername`:** `/encrypt` and `/all` are not valid cipher.exe switches — this command would fail.

---

**Q19. What does the command `cipher /w:C:\` perform?**

- A) Encrypts all files on the C: drive using EFS
- B) Wipes all encrypted files on the C: drive
- C) Overwrites free disk space on C: to prevent forensic recovery of deleted data ✅
- D) Displays the encryption status of all files on the C: drive

> **Explanation:**
> - ✅ **C:** `cipher /w` overwrites free (unallocated) disk space with random data to prevent forensic tools from recovering previously deleted unencrypted files. It is a data sanitization command, NOT an encryption command.
> - ❌ **A:** `cipher /w` does NOT encrypt files — it wipes free space. Encrypting all files with EFS would require `cipher /e /s:` on each folder.
> - ❌ **B:** It does not wipe encrypted files — it wipes FREE SPACE (space where deleted files previously resided).
> - ❌ **D:** Displaying encryption status is what `cipher` (no arguments) does in the current directory, or `cipher /c filename` for a specific file. The `/w` switch is exclusively for free-space wiping.

---

## MCQs 20–25 — Extra Notes: Block Ciphers, BitLocker, Steganography, Mistakes

---

**Q20. Which block cipher mode of operation is considered INSECURE because identical plaintext blocks always produce identical ciphertext blocks?**

- A) CBC (Cipher Block Chaining)
- B) ECB (Electronic Codebook) ✅
- C) CTR (Counter Mode)
- D) GCM (Galois/Counter Mode)

> **Explanation:**
> - ✅ **B — ECB:** In ECB mode, each block is encrypted independently with the same key. Identical plaintext blocks → identical ciphertext blocks. This reveals patterns in the data — the famous "ECB penguin" (encrypting an image with ECB still shows the outline) demonstrates this flaw visually.
> - ❌ **A — CBC:** CBC XORs each plaintext block with the previous ciphertext block before encryption — identical plaintext blocks produce DIFFERENT ciphertext blocks. CBC is secure (with a random IV).
> - ❌ **C — CTR:** Counter mode uses a unique counter value for each block — identical plaintext blocks produce different ciphertext. Secure and parallelizable.
> - ❌ **D — GCM:** GCM = CTR + Galois authentication — provides both confidentiality and integrity. It is one of the strongest modes available.

---

**Q21. Which block cipher mode provides BOTH confidentiality AND data integrity/authentication simultaneously?**

- A) ECB
- B) CBC
- C) OFB
- D) GCM ✅

> **Explanation:**
> - ✅ **D — GCM (Galois/Counter Mode):** GCM is an Authenticated Encryption mode — it provides confidentiality (CTR-mode encryption) AND integrity/authentication (Galois Message Authentication Code). This is why AES-GCM is the standard in TLS 1.3.
> - ❌ **A — ECB:** ECB provides confidentiality only (and poorly at that — it's insecure). No authentication.
> - ❌ **B — CBC:** CBC provides confidentiality only. It requires a separate MAC (Message Authentication Code) for integrity — not built-in.
> - ❌ **C — OFB:** OFB converts a block cipher to a stream cipher — confidentiality only, no built-in authentication.

---

**Q22. What is the PRIMARY difference between EFS and BitLocker in terms of what threat they protect against?**

- A) EFS protects against stolen devices; BitLocker protects against unauthorized local users
- B) EFS protects against unauthorized local users; BitLocker protects against stolen/offline devices ✅
- C) EFS and BitLocker both protect against the same threats — they are redundant
- D) EFS uses symmetric encryption; BitLocker uses only asymmetric encryption

> **Explanation:**
> - ✅ **B:** EFS protects files from being read by OTHER USERS on the same running machine (per-user access control). BitLocker protects the entire disk when a device is physically stolen or powered off — it is irrelevant once the OS boots and the user logs in.
> - ❌ **A:** This completely inverts the protection model of both tools.
> - ❌ **C:** They are NOT redundant — they protect against different threat models at different layers. Using both together is best practice.
> - ❌ **D:** Both EFS and BitLocker use hybrid encryption (symmetric for data). BitLocker uses the TPM + symmetric AES — it does not rely solely on asymmetric encryption.

---

**Q23. What is the fundamental difference between steganography and encryption?**

- A) Steganography is stronger than encryption — it provides mathematical confidentiality
- B) Encryption hides the existence of a message; steganography hides its content
- C) Steganography hides the existence of a message; encryption hides its content ✅
- D) Steganography and encryption are the same — both use keys to transform data

> **Explanation:**
> - ✅ **C:** Steganography conceals the FACT that a message exists at all (e.g., hiding text in a JPEG image). Encryption conceals the CONTENT of a message (you can see ciphertext but cannot read it). They address different aspects of covert communication.
> - ❌ **A:** Steganography provides obscurity, not mathematically proven confidentiality. It is NOT stronger than encryption — it relies on secrecy of the hiding technique.
> - ❌ **B:** This swaps the definitions of both terms entirely.
> - ❌ **D:** Steganography does not necessarily use a key — basic LSB steganography has no key. Even when keyed, it works by hiding, not by mathematical transformation like encryption.

---

**Q24. A developer hardcodes an AES-128 key directly into the application's source code and ships it to production. Which encryption mistake does this represent, and what is the PRIMARY risk?**

- A) Using a weak algorithm — AES-128 is not secure enough for production
- B) Hardcoding keys in source code — the key is exposed if the code is decompiled, leaked, or found in a repository ✅
- C) Using symmetric encryption — only asymmetric encryption is appropriate for production
- D) Not using ECB mode — ECB would have been more secure in this scenario

> **Explanation:**
> - ✅ **B:** Hardcoding cryptographic keys in source code is a critical security mistake. Source code is often stored in version control (Git), shared with developers, compiled into binaries that can be decompiled, or accidentally leaked. Once exposed, the key — and all data it protects — is compromised forever.
> - ❌ **A:** AES-128 is currently considered secure — the algorithm choice is not the problem here. The key management is the problem.
> - ❌ **C:** Symmetric encryption (AES) is entirely appropriate for bulk data encryption in production — the mistake is in how the key is managed, not the type of encryption used.
> - ❌ **D:** ECB mode is insecure — recommending ECB is wrong in any context. This option is a trap for those who confuse cipher modes with key management.

---

**Q25. Which of the following CORRECTLY describes the encryption history milestone where the security of a cipher was first analyzed through statistical frequency analysis of ciphertext characters?**

- A) Claude Shannon developed frequency analysis in 1949 as part of information theory
- B) Al-Kindi developed frequency analysis around 800 AD — the first known cryptanalysis technique ✅
- C) Auguste Kerckhoffs developed frequency analysis in 1883 alongside his cryptographic principles
- D) Alan Turing developed frequency analysis during World War II to break the Enigma cipher

> **Explanation:**
> - ✅ **B — Al-Kindi (~800 AD):** The Arab mathematician Al-Kindi described frequency analysis in his manuscript "A Manuscript on Deciphering Cryptographic Messages" — the first known systematic cryptanalysis technique. It works by exploiting the fact that certain letters appear more frequently in any language (e.g., 'E' is most common in English).
> - ❌ **A — Claude Shannon (1949):** Shannon developed the mathematical theory of secrecy systems (Confusion, Diffusion) — not frequency analysis. Shannon was building the theoretical foundation of cryptography, not developing cryptanalysis tools.
> - ❌ **C — Kerckhoffs (1883):** Kerckhoffs developed his six principles of cryptographic system design — not frequency analysis. These are separate contributions separated by nearly 1000 years.
> - ❌ **D — Alan Turing (WWII):** Turing broke Enigma using the Bombe machine — exploiting cribs (known plaintext patterns) and mechanical weaknesses, not pure frequency analysis. Also, Turing operated in the 1940s — over 1100 years after Al-Kindi.

---

## 📊 Answer Key — Quick Reference

| Q | Answer | Topic |
|---|--------|-------|
| 1 | B | Definition of Encryption |
| 2 | C | Cryptography vs Cryptanalysis vs Cryptology |
| 3 | C | Encryption protects Confidentiality only — not Integrity |
| 4 | C | Formal decryption model X = D(K,Y) |
| 5 | C | Encoding vs Encryption — key requirement |
| 6 | C | Base64 = encoding, NOT encryption |
| 7 | B | Operation → Security goal mapping |
| 8 | C | Kerckhoffs's Principle |
| 9 | C | Security through obscurity violates Kerckhoffs |
| 10 | B | Shannon's Confusion |
| 11 | C | AES — ShiftRows/MixColumns = Diffusion |
| 12 | C | Key space doubles per bit |
| 13 | C | Algorithm strength + key length both matter |
| 14 | C | EFS requires NTFS |
| 15 | C | Copy to FAT32 = silently decrypted |
| 16 | B | FEK encrypted by RSA public key → stored in DDF |
| 17 | B | DRF = FEK encrypted with Recovery Agent's public key |
| 18 | C | `cipher /e /s:foldername` = recursive encryption |
| 19 | C | `cipher /w` = free space wipe, NOT encryption |
| 20 | B | ECB = insecure — identical blocks → identical ciphertext |
| 21 | D | GCM = confidentiality + integrity |
| 22 | B | EFS vs BitLocker threat model |
| 23 | C | Steganography hides existence; encryption hides content |
| 24 | B | Hardcoded keys = critical key management mistake |
| 25 | B | Al-Kindi = first frequency analysis (~800 AD) |

---
