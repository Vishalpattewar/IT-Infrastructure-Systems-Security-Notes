# Session 02 — Basic Encryption Concepts, File Encryption & Encrypting Folders

## 📑 Table of Contents

- [1. Basic Encryption Concepts](#1-basic-encryption-concepts)
  - [1.1 What is Encryption?](#11-what-is-encryption)
  - [1.2 Core Terminology](#12-core-terminology)
  - [1.3 How Encryption Works — The Basic Model](#13-how-encryption-works--the-basic-model)
  - [1.4 Kerckhoffs's Principle](#14-kerckhoffss-principle)
  - [1.5 Shannon's Properties — Confusion and Diffusion](#15-shannons-properties--confusion-and-diffusion)
  - [1.6 Key Space and Key Length](#16-key-space-and-key-length)
  - [1.7 Types of Encryption — Overview](#17-types-of-encryption--overview)
  - [1.8 Encoding vs Encryption vs Hashing](#18-encoding-vs-encryption-vs-hashing)
  - [1.9 Steganography vs Encryption](#19-steganography-vs-encryption)
- [2. File Encryption](#2-file-encryption)
  - [2.1 What is File Encryption?](#21-what-is-file-encryption)
  - [2.2 File Encryption vs Full Disk Encryption vs Folder Encryption](#22-file-encryption-vs-full-disk-encryption-vs-folder-encryption)
  - [2.3 Windows EFS — Encrypting File System](#23-windows-efs--encrypting-file-system)
  - [2.4 How EFS Works Internally](#24-how-efs-works-internally)
  - [2.5 EFS Key Components](#25-efs-key-components)
  - [2.6 EFS Limitations and Risks](#26-efs-limitations-and-risks)
- [3. Encrypting Folders](#3-encrypting-folders)
  - [3.1 Graphical Method — Windows EFS via Properties](#31-graphical-method--windows-efs-via-properties)
  - [3.2 Command Line — cipher.exe](#32-command-line--cipherexe)
  - [3.3 cipher.exe Command Reference](#33-cipherexe-command-reference)
- [4. 📌 Extra Notes](#4--extra-notes)
  - [4.1 History of Encryption — Brief Timeline](#41-history-of-encryption--brief-timeline)
  - [4.2 Security Through Obscurity — Why It Fails](#42-security-through-obscurity--why-it-fails)
  - [4.3 Substitution and Transposition — Foundational Cipher Types](#43-substitution-and-transposition--foundational-cipher-types)
  - [4.4 Block Cipher vs Stream Cipher](#44-block-cipher-vs-stream-cipher)
  - [4.5 BitLocker vs EFS — Detailed Comparison](#45-bitlocker-vs-efs--detailed-comparison)
  - [4.6 VeraCrypt — Cross-Platform Encryption Tool](#46-veracrypt--cross-platform-encryption-tool)
  - [4.7 OpenPGP File Encryption](#47-openpgp-file-encryption)
  - [4.8 Key Management Basics](#48-key-management-basics)
  - [4.9 Encryption in the CIA Context](#49-encryption-in-the-cia-context)
  - [4.10 Common Encryption Mistakes — MCQ Traps](#410-common-encryption-mistakes--mcq-traps)
- [5. Abbreviations Table](#5-abbreviations-table)
- [6. Keywords + Concept Map](#6-keywords--concept-map)
- [7. Quick Reference Cheatsheet](#7-quick-reference-cheatsheet)
- [8. Session Revision Snapshot](#8-session-revision-snapshot)

---

## 1. Basic Encryption Concepts

### 1.1 What is Encryption?

**Encryption** is the process of transforming readable data (**plaintext**) into an unreadable format (**ciphertext**) using a mathematical algorithm and a key — so that only authorized parties with the correct key can reverse the process and read the original data.

> [!IMPORTANT]
> Encryption protects **Confidentiality**.
> It does NOT inherently protect Integrity or Availability.
> A message can be encrypted AND tampered with — encryption alone does not guarantee the message was not altered in transit.

The reverse process — converting ciphertext back to plaintext — is called **Decryption**.

```
Plaintext  ──[Encryption Algorithm + Key]──▶  Ciphertext
Ciphertext ──[Decryption Algorithm + Key]──▶  Plaintext
```

---

### 1.2 Core Terminology

| Term | Definition |
|------|-----------|
| **Plaintext (P)** | Original readable data before encryption — also called *cleartext* |
| **Ciphertext (C)** | Scrambled, unreadable output after encryption |
| **Encryption** | The transformation process: Plaintext → Ciphertext |
| **Decryption** | The reverse transformation: Ciphertext → Plaintext |
| **Key (K)** | A secret value used by the algorithm to encrypt and/or decrypt |
| **Algorithm / Cipher** | The mathematical function used to perform encryption/decryption |
| **Cryptography** | The science of designing secure encryption systems |
| **Cryptanalysis** | The science of breaking encryption systems |
| **Cryptology** | The broader field encompassing both Cryptography and Cryptanalysis |
| **Cipher** | An algorithm for performing encryption and decryption |
| **Key Length** | The size of the key in bits — larger = more secure |
| **Key Space** | The total number of possible keys for a given key length |

> [!NOTE]
> **Cryptography ≠ Cryptology**
> Cryptology = Cryptography (creating) + Cryptanalysis (breaking)
> This distinction is tested in MCQs.

---

### 1.3 How Encryption Works — The Basic Model

The formal encryption model (from Stallings / Symmetric key context):

```
Sender Side:
  Plaintext (X) + Encryption Key (K) → Algorithm → Ciphertext (Y)
  Y = E(K, X)

Receiver Side:
  Ciphertext (Y) + Decryption Key (K) → Algorithm → Plaintext (X)
  X = D(K, Y)
```

For **symmetric encryption**: The same key K is used for both E and D.
For **asymmetric encryption**: Different keys are used — Public Key for E, Private Key for D (covered in Session 03 and 04).

---

### 1.4 Kerckhoffs's Principle

**Kerckhoffs's Principle** (Auguste Kerckhoffs, 1883) is one of the most foundational principles in cryptography:

> *"A cryptosystem should be secure even if everything about the system, except the key, is public knowledge."*

In simple terms: **The security of a cipher must rest entirely in the key — NOT in the secrecy of the algorithm.**

| What Should Be Secret | What Can Be Public |
|-----------------------|--------------------|
| The Key | The Algorithm |
| The Plaintext | The Ciphertext (can be intercepted) |
| | The System design |

**Why this matters:**
- Algorithms that are publicly scrutinized by cryptographers are stronger — flaws get found and fixed.
- Secret algorithms that no one reviews are often weaker — "security by obscurity" fails.
- Modern algorithms (AES, RSA) are all publicly known — their security lies entirely in key secrecy.

> [!IMPORTANT]
> Kerckhoffs's Principle is one of the **most frequently tested** concepts in cryptography MCQs.
> MCQ trap: "The algorithm must be kept secret" → **WRONG** — this violates Kerckhoffs's Principle.

---

### 1.5 Shannon's Properties — Confusion and Diffusion

Claude Shannon (1949) defined two essential properties that every strong cipher must implement. These appear in Stallings extensively.

| Property | Definition | Purpose | How Achieved |
|----------|-----------|---------|-------------|
| **Confusion** | Makes the relationship between the key and ciphertext as complex and non-linear as possible | Prevents attackers from deducing the key from the ciphertext | Substitution operations (S-boxes) |
| **Diffusion** | Spreading the influence of a single plaintext bit across many ciphertext bits | Prevents attackers from finding patterns between plaintext and ciphertext | Permutation / transposition operations |

> [!NOTE]
> **Memory hook:**
> - **Confusion** = hides the key → uses **Substitution**
> - **Diffusion** = spreads the plaintext → uses **Permutation/Transposition**
> 
> Modern ciphers like **AES** implement both confusion (SubBytes step) and diffusion (ShiftRows + MixColumns steps).

---

### 1.6 Key Space and Key Length

| Key Length | Total Possible Keys (Key Space) | Practical Security |
|-----------|--------------------------------|-------------------|
| 1-bit | 2¹ = 2 | None |
| 8-bit | 2⁸ = 256 | Trivially broken |
| 56-bit | 2⁵⁶ ≈ 72 quadrillion | DES — broken by brute force |
| 128-bit | 2¹²⁸ ≈ 3.4 × 10³⁸ | AES-128 — currently secure |
| 256-bit | 2²⁵⁶ ≈ 1.16 × 10⁷⁷ | AES-256 — quantum-resistant candidate |
| 2048-bit | 2²⁰⁴⁸ | RSA-2048 — current standard for asymmetric |

> [!IMPORTANT]
> Key space grows **exponentially** — adding 1 bit **doubles** the key space.
> A 57-bit key has DOUBLE the combinations of a 56-bit key.
>
> **Brute Force Attack** = trying every possible key in the key space.
> The larger the key space, the longer brute force takes.

> [!NOTE]
> Key length alone doesn't determine security — a 256-bit key used with a broken algorithm is still insecure. Both algorithm strength AND key length matter.

---

### 1.7 Types of Encryption — Overview

This is a high-level map — deep dives happen in Sessions 03 and 04.

```
Encryption
├── Symmetric Key Encryption
│   ├── Same key for encryption and decryption
│   ├── Fast, efficient for large data
│   └── Examples: DES, AES, RC4, RC5, 3DES
│
└── Asymmetric Key Encryption
    ├── Key pair: Public Key (encrypt) + Private Key (decrypt)
    ├── Slower, used for key exchange and digital signatures
    └── Examples: RSA, ECC, Diffie-Hellman
```

| Property | Symmetric | Asymmetric |
|----------|-----------|-----------|
| Keys used | 1 (shared) | 2 (public + private) |
| Speed | Fast | Slow |
| Key distribution | Difficult (key must be shared securely) | Easy (public key is openly shared) |
| Use case | Bulk data encryption | Key exchange, digital signatures |
| Example | AES | RSA |

---

### 1.8 Encoding vs Encryption vs Hashing

This is one of the **most commonly tested conceptual distinctions** in any security exam.

| Property | Encoding | Encryption | Hashing |
|----------|---------|-----------|---------|
| **Purpose** | Data representation / format conversion | Confidentiality | Data integrity verification |
| **Key required?** | ❌ No | ✅ Yes | ❌ No |
| **Reversible?** | ✅ Yes (easily) | ✅ Yes (with correct key) | ❌ No (one-way) |
| **Security goal** | None — not a security mechanism | Confidentiality | Integrity |
| **Examples** | Base64, ASCII, URL encoding | AES, RSA, DES | MD5, SHA-1, SHA-256 |
| **Output size** | Variable | Same or slightly larger than input | Fixed (regardless of input size) |

> [!IMPORTANT]
> **Encoding is NOT encryption.**
> Base64 encoded text is NOT secure — anyone can decode it with zero key knowledge.
> This is a critical MCQ trap: "Base64 is a form of encryption" → **FALSE**.

> [!NOTE]
> **Digital Signatures** use both hashing AND asymmetric encryption together — covered in Session 07.

---

### 1.9 Steganography vs Encryption

| Property | Steganography | Encryption |
|----------|--------------|-----------|
| **What it does** | Hides the **existence** of a message | Hides the **content** of a message |
| **Output** | Appears as an innocent carrier (image, audio, video) | Clearly looks like ciphertext |
| **Security model** | Security through hiding (obscurity) | Security through mathematical complexity |
| **Key required?** | Sometimes | Always |
| **Example** | Hiding text inside a JPEG image's LSBs | Encrypting a file with AES |
| **Combined use** | Steganography + Encryption = strongest covert communication | — |

> [!NOTE]
> **Steganography** comes from Greek: *steganos* (covered) + *graphos* (writing).
> It is NOT a substitute for encryption — it is a complementary technique.
> MCQ trap: "Steganography provides confidentiality" — **partially true** but it primarily provides **obscurity**, not mathematically proven confidentiality.

---

## 2. File Encryption

### 2.1 What is File Encryption?

**File Encryption** is the process of encrypting individual files so that only authorized users (holding the correct key or certificate) can access the file contents — even if they physically possess the storage medium.

Key characteristics:
- Operates at the **file level** — individual files are encrypted independently
- The rest of the system (OS, other files) remains unencrypted
- Encrypted files look like random data to anyone without the key

---

### 2.2 File Encryption vs Full Disk Encryption vs Folder Encryption

| Type | Scope | Granularity | Example Tools |
|------|-------|------------|--------------|
| **File Encryption** | Individual files only | Very fine — per file | GPG, AES Crypt, 7-Zip |
| **Folder Encryption** | All files inside a specific folder | Medium — per folder | Windows EFS, VeraCrypt |
| **Full Disk Encryption (FDE)** | Entire storage device | Coarse — entire disk | BitLocker, VeraCrypt, LUKS |
| **Volume Encryption** | A specific partition or volume | Medium — per volume | BitLocker, VeraCrypt |

> [!IMPORTANT]
> **Full Disk Encryption** protects data when a device is **powered off or stolen** — but once the OS boots and the user logs in, files are decrypted transparently. It does NOT protect against a logged-in malicious user.
> **File/Folder Encryption (EFS)** can protect files even from other logged-in users on the same machine.

---

### 2.3 Windows EFS — Encrypting File System

**EFS (Encrypting File System)** is a built-in Windows feature (available since Windows 2000) that provides **transparent file-level encryption** on NTFS volumes.

Key facts:
- Part of the **NTFS** filesystem — only works on NTFS, not FAT32 or exFAT
- Encryption is **transparent** to the file owner — they open files normally
- Other users on the same machine **cannot** read EFS-encrypted files
- Available on: Windows Professional, Enterprise, and Ultimate editions (NOT Home editions)
- Uses a combination of **symmetric encryption (AES)** for file data and **asymmetric encryption (RSA)** for key protection

> [!IMPORTANT]
> EFS is **NOT available** on Windows Home editions — this is a frequently tested fact.
> EFS requires **NTFS** — it does NOT work on FAT32 formatted drives.

---

### 2.4 How EFS Works Internally

EFS uses a two-key architecture:

```
Step 1: A random symmetric key is generated for each file
        → This is called the FEK (File Encryption Key)

Step 2: The file content is encrypted using the FEK
        (AES-256 in modern Windows versions)

Step 3: The FEK itself is encrypted using the user's
        RSA Public Key (from their EFS certificate)

Step 4: The encrypted FEK is stored in the file's
        DDF (Data Decryption Field) in file metadata

Step 5: When the user opens the file:
        → EFS retrieves the encrypted FEK from DDF
        → Decrypts FEK using user's RSA Private Key
        → Uses FEK to decrypt the file content
        → User sees plaintext transparently
```

> [!NOTE]
> This two-layer design (symmetric key for data + asymmetric key to protect the symmetric key) is called **Hybrid Encryption**.
> This pattern is used everywhere in security — SSL/TLS uses the same concept.
> **Why hybrid?** Asymmetric encryption is slow — encrypting large files with RSA is impractical. Symmetric encryption (AES) is fast for bulk data. So: AES encrypts the data, RSA protects the AES key.

---

### 2.5 EFS Key Components

| Component | Full Form | Role |
|-----------|-----------|------|
| **FEK** | File Encryption Key | Random symmetric key generated per-file; actually encrypts file content |
| **DDF** | Data Decryption Field | Stores the FEK encrypted with the user's public key |
| **DRF** | Data Recovery Field | Stores the FEK encrypted with the Recovery Agent's public key |
| **EFS Certificate** | — | X.509 certificate containing the user's RSA public key for EFS |
| **Recovery Agent** | — | A designated account (usually Administrator) that can decrypt any EFS file using DRF |

> [!IMPORTANT]
> The **DRF** and **Recovery Agent** concept is critical for MCQs:
> If a user leaves an organization or loses their private key, the **Recovery Agent** can still decrypt the files using the DRF.
> This is why organizations must configure a Recovery Agent BEFORE encrypting files.

---

### 2.6 EFS Limitations and Risks

| Limitation / Risk | Explanation |
|-------------------|-------------|
| **NTFS only** | Cannot encrypt files on FAT32 or exFAT drives |
| **Copy to FAT = decrypted** | If an EFS-encrypted file is copied to a FAT32 drive, it is automatically decrypted |
| **Not available on Windows Home** | Only Professional/Enterprise/Ultimate |
| **No protection when logged in** | EFS transparently decrypts for the file owner — malware running as that user gets plaintext |
| **Certificate loss = data loss** | If EFS certificate and private key are lost with no Recovery Agent, files are permanently inaccessible |
| **No network share encryption** | EFS does not encrypt files in transit over a network — only at rest |
| **No protection against admin** | A domain admin can configure Recovery Agent and decrypt files |

> [!TIP]
> Copying an EFS-encrypted file to a USB drive formatted as FAT32 **silently decrypts** the file — this is a major real-world security risk and a common exam scenario.

---

## 3. Encrypting Folders

### 3.1 Graphical Method — Windows EFS via Properties

To encrypt a folder using the Windows GUI:

```
Step 1: Right-click the folder → Properties
Step 2: Click the [General] tab → Advanced button
Step 3: Check ✅ "Encrypt contents to secure data"
Step 4: Click OK → Apply
Step 5: Windows asks:
        ○ Apply changes to this folder only
        ○ Apply changes to this folder, subfolders and files ← recommended
Step 6: Click OK
```

Visual indicators:
- Encrypted files/folders appear with a **green filename** in Windows Explorer (when configured to show colors)
- A lock icon overlay may appear depending on Windows version

> [!NOTE]
> Encrypting a folder in EFS means **new files added to that folder are automatically encrypted**.
> Existing files must be explicitly included when applying encryption.

---

### 3.2 Command Line — cipher.exe

**cipher.exe** is the Windows built-in command-line tool for managing EFS encryption. It is part of Windows since Windows 2000.

> [!TIP]
> The `cipher` command works on files and folders on **NTFS volumes only**.
> It is the command-line equivalent of the EFS graphical interface.

---

### 3.3 cipher.exe Command Reference

| Command | Action |
|---------|--------|
| `cipher /e foldername` | Encrypt a folder (marks it for encryption) |
| `cipher /e /s:foldername` | Encrypt folder + all subfolders and files recursively |
| `cipher /d foldername` | Decrypt a folder |
| `cipher /d /s:foldername` | Decrypt folder + all subfolders and files recursively |
| `cipher /c filename` | Display encryption information for a specific file |
| `cipher` (no args) | Display encryption status of all files in current directory |
| `cipher /w:C:\` | Wipe free space on C: drive (overwrite deleted unencrypted data) |
| `cipher /r:filename` | Generate EFS Recovery Agent certificate and private key |
| `cipher /x:filename` | Back up EFS certificate and keys to a file |
| `cipher /u` | Update encrypted files with current EFS certificate (after cert renewal) |

**Output indicators in cipher listing:**
```
U = Unencrypted file
E = Encrypted file
```

Example output:
```
C:\SecureFolder\
  U  report_draft.txt      ← Unencrypted
  E  salary_data.xlsx      ← Encrypted
  E  contracts.docx        ← Encrypted
```

> [!NOTE]
> `cipher /w` does NOT encrypt files — it overwrites free disk space to prevent recovery of previously deleted unencrypted files using forensic tools.
> This is a **data sanitization** feature, not an encryption feature — commonly tested in MCQs.

---

## 4. 📌 Extra Notes

> [!NOTE]
> Everything in this section goes beyond the core syllabus but is directly MCQ-relevant. Cross-referenced from Stallings, NIST publications, and Windows security documentation.

---

### 4.1 History of Encryption — Brief Timeline

> [!NOTE]

| Era | Development |
|-----|-------------|
| **~1900 BC** | Egyptians used non-standard hieroglyphs — earliest known encryption |
| **~600 BC** | **Scytale** — Spartan military cipher (transposition using a rod) |
| **~58 BC** | **Caesar Cipher** — Julius Caesar's substitution cipher (shift of 3) |
| **~800 AD** | Al-Kindi (Arab mathematician) developed **frequency analysis** — first known cryptanalysis technique |
| **1466** | Leon Alberti — **polyalphabetic cipher** (Vigenère predecessor) |
| **1917** | **Vernam Cipher (One-Time Pad)** — Gilbert Vernam; theoretically unbreakable |
| **1939–1945** | **Enigma Machine** (Germany) — electromechanical rotor cipher; broken by Alan Turing at Bletchley Park |
| **1949** | Claude Shannon — "Communication Theory of Secrecy Systems" — mathematical foundation of cryptography |
| **1977** | **DES** published as US federal standard (NIST/NBS) |
| **1976** | **Diffie-Hellman** key exchange published — revolutionized cryptography |
| **1978** | **RSA** published (Rivest, Shamir, Adleman) |
| **2001** | **AES** adopted as US federal standard, replacing DES |

---

### 4.2 Security Through Obscurity — Why It Fails

> [!NOTE]
> **Security through obscurity** = relying on the secrecy of the system design, algorithm, or implementation details (rather than the key) as the primary security mechanism.

Why it fails:
- Systems are eventually reverse-engineered, leaked, or discovered
- Once the "secret design" is exposed, there is NO remaining security
- It prevents external review, so flaws go undetected longer
- Real-world failures: DVD CSS encryption (cracked), GSM A5/1 cipher (cracked after algorithm leaked)

> [!IMPORTANT]
> This directly connects to **Kerckhoffs's Principle** — security should never depend on algorithm secrecy.
> "Security through obscurity is not security at all" — widely accepted principle in modern cryptography.

---

### 4.3 Substitution and Transposition — Foundational Cipher Types

> [!NOTE]
> These are the two **atomic building blocks** of all classical and modern ciphers.

#### Substitution Ciphers
Replace each plaintext symbol with a different symbol according to a fixed rule.

| Type | Description | Example |
|------|-------------|---------|
| **Caesar Cipher** | Each letter shifted by a fixed number | A→D, B→E (shift 3) |
| **ROT13** | Special case of Caesar cipher — shift of 13 | A→N, B→O |
| **Monoalphabetic** | Each letter mapped to one fixed replacement letter | A→Q, B→Z (random mapping) |
| **Polyalphabetic** | Multiple substitution alphabets used in rotation | Vigenère Cipher |
| **Playfair Cipher** | Substitution on pairs of letters (digrams) | Encrypts 2 letters at a time |

#### Transposition Ciphers
Rearrange the positions of plaintext characters without changing them.

| Type | Description | Example |
|------|-------------|---------|
| **Rail Fence Cipher** | Write plaintext in a zigzag across rows | "HELLO" → "HLOEL" |
| **Columnar Transposition** | Write in rows, read off in column order | Key determines column order |
| **Double Transposition** | Apply columnar transposition twice | More secure than single |

> [!NOTE]
> **Shannon's Confusion = Substitution**, **Shannon's Diffusion = Transposition/Permutation**
> Modern ciphers use BOTH in multiple rounds — this is called a **Product Cipher**.
> AES is a product cipher implementing both confusion and diffusion in each round.

---

### 4.4 Block Cipher vs Stream Cipher

> [!NOTE]
> This distinction is fundamental to understanding how encryption algorithms work — and is tested directly.

| Property | Block Cipher | Stream Cipher |
|----------|-------------|--------------|
| **Encryption unit** | Fixed-size blocks of data (e.g., 64-bit, 128-bit) | One bit or one byte at a time |
| **Speed** | Slower | Faster |
| **Error propagation** | An error in one block may affect subsequent blocks | An error affects only the current bit/byte |
| **Use case** | File encryption, disk encryption, database encryption | Real-time streams, wireless communication, VoIP |
| **Examples** | DES (64-bit block), AES (128-bit block), 3DES | RC4, Salsa20, ChaCha20 |
| **Key stream** | Does not use key stream | Uses a pseudo-random key stream XORed with plaintext |

**Block Cipher Modes of Operation:**

| Mode | Full Name | Key Property |
|------|-----------|-------------|
| **ECB** | Electronic Codebook | Same plaintext block = same ciphertext block — **INSECURE** — shows patterns |
| **CBC** | Cipher Block Chaining | Each block XORed with previous ciphertext before encryption — most widely used |
| **CFB** | Cipher Feedback | Converts block cipher to stream cipher |
| **OFB** | Output Feedback | Key stream is independent of plaintext — error doesn't propagate |
| **CTR** | Counter | Uses a counter value — parallelizable — used in AES-GCM |
| **GCM** | Galois/Counter Mode | CTR + authentication — provides both encryption and integrity |

> [!IMPORTANT]
> **ECB mode is insecure** because identical plaintext blocks produce identical ciphertext blocks — revealing patterns.
> The famous **ECB penguin** (Linux Tux image encrypted with ECB still shows the penguin outline) is the standard illustration of this flaw.
> AES-**CBC** and AES-**GCM** are the recommended modes.

---

### 4.5 BitLocker vs EFS — Detailed Comparison

> [!NOTE]
> Both are Windows encryption features but they operate at completely different levels — a very common MCQ area.

| Property | EFS (Encrypting File System) | BitLocker |
|----------|------------------------------|-----------|
| **Scope** | Individual files and folders | Entire drive/volume |
| **Type** | File-level encryption | Full disk encryption (FDE) |
| **Keys tied to** | User account / certificate | Machine + TPM chip (or PIN/USB) |
| **Protection against** | Other users on same machine | Stolen/lost device (offline attack) |
| **OS needed** | Windows NTFS volume | Windows Vista and later |
| **Editions** | Pro, Enterprise, Ultimate | Pro, Enterprise, Education |
| **Transparency** | Transparent to file owner | Transparent after OS boot/login |
| **Recovery** | Recovery Agent certificate | BitLocker Recovery Key (48-digit) |
| **TPM required?** | No | Recommended (can work without) |
| **Protection when logged in?** | Partial (per-user isolation) | No (drive is decrypted once booted) |

> [!TIP]
> **Best practice = use both together:**
> BitLocker protects the disk if the device is stolen (powered off).
> EFS protects specific files even from other users on the same machine.
> They are complementary, not competing.

---

### 4.6 VeraCrypt — Cross-Platform Encryption Tool

> [!NOTE]

| Property | Details |
|----------|---------|
| **Type** | Open-source disk encryption software |
| **Successor to** | TrueCrypt (abandoned in 2014) |
| **Platforms** | Windows, macOS, Linux |
| **Encryption algorithms** | AES, Serpent, Twofish (and combinations) |
| **Modes** | File containers, encrypted partitions, full disk encryption (including system drive) |
| **Special feature** | **Plausible deniability** — hidden volumes within outer volumes |
| **Key feature** | Can create an encrypted container file that mounts as a virtual drive |

**Plausible Deniability:**
VeraCrypt supports **hidden volumes** — a secret encrypted volume hidden inside an outer encrypted volume. If forced to reveal the password, you reveal the outer volume password (which contains decoy data), while the hidden volume remains undetected.

---

### 4.7 OpenPGP File Encryption

> [!NOTE]
> **PGP (Pretty Good Privacy)** — created by Phil Zimmermann in 1991 — is a widely used encryption program for files and emails.

| Property | Details |
|----------|---------|
| **OpenPGP** | Open standard (RFC 4880) based on PGP |
| **GPG / GnuPG** | GNU Privacy Guard — free, open-source implementation of OpenPGP |
| **Key type** | Uses hybrid encryption (symmetric for data + asymmetric for key) |
| **Use cases** | File encryption, email encryption, software signing |
| **Web of Trust** | PGP uses a decentralized trust model — peers vouch for each other's keys (unlike PKI's CA-based hierarchy) |

> [!NOTE]
> PGP's **Web of Trust** vs PKI's **Hierarchical Trust (CA model)** is a key comparison tested in Session 13 (SSL/TLS/PGP). Note it here as context.

---

### 4.8 Key Management Basics

> [!NOTE]
> Key management is one of the hardest problems in cryptography — encryption is only as strong as its key management.

**Key Lifecycle stages:**

```
Key Generation → Key Distribution → Key Storage → Key Use → Key Rotation → Key Revocation → Key Destruction
```

| Stage | Key Management Concern |
|-------|----------------------|
| **Generation** | Must use cryptographically secure random number generators (CSPRNG) — not pseudo-random |
| **Distribution** | How do two parties securely share a symmetric key? (Solved by Diffie-Hellman — Session 05) |
| **Storage** | Keys must be stored encrypted or in Hardware Security Modules (HSM) |
| **Rotation** | Keys must be changed periodically — old keys increase exposure window |
| **Revocation** | Compromised keys must be revoked immediately |
| **Destruction** | Keys must be securely destroyed (not just deleted) — otherwise recoverable |

> [!IMPORTANT]
> **Key escrow** = a copy of the key is held by a trusted third party (e.g., government, organization) for recovery purposes.
> Controversial because it creates a high-value target for attackers.

---

### 4.9 Encryption in the CIA Context

> [!NOTE]
> Encryption is often misunderstood as solving all security problems. Map it correctly:

| CIA Property | Does Encryption Help? | How |
|-------------|----------------------|-----|
| **Confidentiality** | ✅ Yes — directly | Encrypted data is unreadable without the key |
| **Integrity** | ⚠️ Partially | Encryption alone does NOT verify data wasn't altered — need hashing or MACs additionally |
| **Availability** | ❌ No | Encryption can actually harm availability if keys are lost — ransomware exploits this |

> [!IMPORTANT]
> Encryption ≠ Integrity protection.
> An attacker can modify ciphertext (causing garbled plaintext on decryption) without knowing the key.
> **Authenticated Encryption** (e.g., AES-GCM) provides both confidentiality AND integrity simultaneously.

---

### 4.10 Common Encryption Mistakes — MCQ Traps

> [!NOTE]
> These are documented real-world implementation mistakes — MCQs are often set on these.

| Mistake | Why It's Wrong |
|---------|----------------|
| **Using ECB mode** | Reveals plaintext patterns in ciphertext |
| **Hardcoding keys in source code** | Keys are exposed if code is decompiled or leaked |
| **Using weak/short keys** | Small key space → brute force feasible (e.g., 40-bit keys) |
| **Reusing IV (Initialization Vector)** | Makes CBC/CTR modes predictable and attackable |
| **Using MD5/SHA-1 for security** | Both are cryptographically broken — collision attacks exist |
| **Encrypting without authenticating** | Attacker can flip ciphertext bits without detection |
| **Using custom/home-grown algorithms** | "Don't roll your own crypto" — custom ciphers almost always have flaws |
| **Base64 as encryption** | Base64 is encoding — completely reversible without a key |
| **Weak random number generation** | Predictable keys/IVs → breaks encryption |

---

## 5. Abbreviations Table

| Abbreviation | Full Form | One-Line Technical Meaning |
|---|---|---|
| EFS | Encrypting File System | Windows NTFS built-in file/folder level encryption tied to user certificates |
| FEK | File Encryption Key | Per-file symmetric key used by EFS to encrypt file content |
| DDF | Data Decryption Field | EFS metadata field storing FEK encrypted with user's public key |
| DRF | Data Recovery Field | EFS metadata field storing FEK encrypted with Recovery Agent's public key |
| FDE | Full Disk Encryption | Encryption of an entire storage device/volume |
| AES | Advanced Encryption Standard | Current US federal symmetric block cipher standard (128/192/256-bit keys) |
| DES | Data Encryption Standard | Older 56-bit symmetric block cipher — now considered insecure |
| RSA | Rivest–Shamir–Adleman | Widely used asymmetric encryption algorithm based on prime factorization |
| TPM | Trusted Platform Module | Hardware chip storing cryptographic keys — used by BitLocker |
| PGP | Pretty Good Privacy | Hybrid encryption program for files and email — Phil Zimmermann, 1991 |
| GPG | GNU Privacy Guard | Free open-source implementation of the OpenPGP standard |
| ECB | Electronic Codebook | Insecure block cipher mode — identical plaintext → identical ciphertext |
| CBC | Cipher Block Chaining | Block cipher mode — each block XORed with previous ciphertext |
| GCM | Galois/Counter Mode | Authenticated encryption mode providing both confidentiality and integrity |
| IV | Initialization Vector | Random value used in block cipher modes to ensure unique ciphertext per encryption |
| HSM | Hardware Security Module | Physical device for secure cryptographic key storage and operations |
| CSPRNG | Cryptographically Secure Pseudo-Random Number Generator | RNG suitable for cryptographic key and IV generation |
| CTR | Counter Mode | Block cipher mode using an incrementing counter — parallelizable |
| OTP | One-Time Pad | Theoretically unbreakable cipher using a key as long as the message, used only once |
| LUKS | Linux Unified Key Setup | Standard for Linux disk encryption |

---

## 6. Keywords + Concept Map

| Term | Definition | Connections | Use Cases |
|------|-----------|-------------|-----------|
| **Plaintext** | Original readable data | Encryption input, Ciphertext output | Any data before securing |
| **Ciphertext** | Encrypted unreadable data | Decryption input, Plaintext output | Data in storage/transit after encryption |
| **Key** | Secret value controlling encryption/decryption | Key space, Key length, Key management | All encryption operations |
| **Kerckhoffs's Principle** | Security rests in key, not algorithm secrecy | Algorithm transparency, Security through obscurity (opposite) | Cipher design, policy |
| **Confusion** | Hides relationship between key and ciphertext | Substitution, S-boxes, Shannon | AES SubBytes step |
| **Diffusion** | Spreads plaintext influence across ciphertext | Permutation, Transposition, Shannon | AES ShiftRows/MixColumns |
| **EFS** | Windows file-level transparent encryption | NTFS, FEK, DDF, DRF, RSA, AES, Recovery Agent | Enterprise data protection |
| **BitLocker** | Windows full-disk encryption | TPM, FDE, EFS (complementary) | Laptop theft protection |
| **Hybrid Encryption** | Symmetric key for data + asymmetric key to protect symmetric key | EFS, SSL/TLS, PGP, RSA+AES | Industry standard pattern |
| **Block Cipher** | Encrypts fixed-size data blocks | ECB, CBC, GCM, AES, DES | File and disk encryption |
| **Stream Cipher** | Encrypts bit/byte at a time | RC4, ChaCha20, XOR | Real-time communications |
| **Steganography** | Hides existence of message | LSB insertion, carrier files | Covert communication |
| **Key Escrow** | Third-party copy of keys | Key management, Government access | Legal compliance, recovery |

---

## 7. Quick Reference Cheatsheet

### 🔸 Encoding vs Encryption vs Hashing

| Property | Encoding | Encryption | Hashing |
|----------|---------|-----------|---------|
| Key needed | No | Yes | No |
| Reversible | Yes | Yes (with key) | No |
| Security goal | None | Confidentiality | Integrity |
| Example | Base64 | AES | SHA-256 |
| Output size | Variable | ~Same as input | Fixed |

---

### 🔸 EFS Quick Facts

| Property | Value |
|----------|-------|
| Filesystem required | NTFS only |
| File content encrypted with | AES (symmetric) |
| FEK protected by | RSA public key (asymmetric) |
| Recovery mechanism | DRF + Recovery Agent |
| Windows editions | Pro, Enterprise, Ultimate (NOT Home) |
| Copy to FAT32 result | File is silently decrypted |
| Green filename = | EFS encrypted |

---

### 🔸 cipher.exe Key Commands

| Command | Action |
|---------|--------|
| `cipher /e /s:folder` | Encrypt folder recursively |
| `cipher /d /s:folder` | Decrypt folder recursively |
| `cipher /c file` | Show encryption info for file |
| `cipher /w:C:\` | Wipe free space (NOT encryption) |
| `cipher /r:filename` | Generate Recovery Agent cert |
| `cipher` (no args) | Show encryption status of current dir |
| E = encrypted, U = unencrypted | Output legend |

---

### 🔸 Block Cipher Modes — Security Ranking

| Mode | Security Level | Key Feature |
|------|---------------|-------------|
| ECB | ❌ Insecure | Reveals patterns — NEVER use |
| CBC | ✅ Secure | XOR chaining — most widely used |
| CFB | ✅ Secure | Block cipher as stream cipher |
| OFB | ✅ Secure | Key stream independent of plaintext |
| CTR | ✅ Secure | Parallelizable |
| GCM | ✅✅ Best | Encryption + Authentication |

---

### 🔸 EFS vs BitLocker Comparison

| Property | EFS | BitLocker |
|----------|-----|-----------|
| Scope | File/Folder | Full Disk |
| Protects against | Other local users | Stolen/offline device |
| Tied to | User certificate | Machine + TPM |
| NTFS required | Yes | No |
| Available on Home? | No | No |
| Use together? | ✅ Recommended | ✅ Recommended |

---

### 🔸 Substitution vs Transposition

| Property | Substitution | Transposition |
|----------|-------------|--------------|
| What changes | The symbols | The positions |
| What stays same | The positions | The symbols |
| Shannon property | Confusion | Diffusion |
| Example | Caesar Cipher | Rail Fence Cipher |

---

## 8. Session Revision Snapshot

### ⚡ TL;DR — 5 Bullets

- ✅ Encryption = Plaintext + Key + Algorithm → Ciphertext — security rests in the KEY, not the algorithm (Kerckhoffs's Principle)
- ✅ Encoding (Base64) is NOT encryption — it requires no key and is fully reversible by anyone
- ✅ EFS = Windows NTFS file-level encryption using hybrid model (AES for data + RSA for FEK) — NOT available on Home editions or FAT32
- ✅ Block ciphers encrypt fixed blocks — ECB is insecure (reveals patterns), CBC/GCM are the standard modes
- ✅ Confusion (substitution) hides the key; Diffusion (transposition/permutation) spreads plaintext — both are required in strong ciphers (Shannon, 1949)

---

### 🎯 MCQ-Likely Concepts — Everything Examiners Love

| Concept | Why It's Tricky |
|---------|----------------|
| Kerckhoffs's Principle | Algorithm must be public — NOT secret. Many students invert this |
| Base64 = NOT encryption | It's encoding — no key, fully reversible |
| EFS not available on Windows Home | Edition-specific — commonly forgotten |
| Copy EFS file to FAT32 = silently decrypted | Quiet data exposure risk |
| `cipher /w` = wipes free space, NOT encryption | Command purpose confusion |
| ECB mode is insecure | Identical plaintext → identical ciphertext → reveals patterns |
| EFS uses hybrid encryption | AES for file content, RSA for FEK — both used together |
| Confusion = substitution, Diffusion = permutation | Students often swap these |
| Steganography hides existence, encryption hides content | Both are different goals |
| Encryption protects confidentiality ONLY — not integrity | Authenticated Encryption (GCM) needed for both |
| McCumber Cube — data in use = Processing state | Encryption at rest vs in transit vs in use |
| Key space doubles with every additional bit | 57-bit = double the combinations of 56-bit |
| DRF = Recovery Agent's copy of FEK | Without this, lost EFS key = data permanently gone |
| Block cipher + CBC needs IV | Same key + same IV in CBC = same ciphertext = attack surface |

---

<details>
<summary>🔬 Lab Content (Session 02 — No Lab Assigned)</summary>

No lab is assigned for Session 02 in the syllabus.

Lab work for encryption topics begins in Session 05 using **CrypTool**, which covers:
- Symmetric encryption: Caesar, Vernam, DES, RC4, AES, Triple DES, XOR
- Asymmetric encryption: RSA, ECC

The concepts covered in Session 02 (encryption model, key types, EFS, cipher.exe) form the theoretical foundation for those lab exercises.

</details>

---