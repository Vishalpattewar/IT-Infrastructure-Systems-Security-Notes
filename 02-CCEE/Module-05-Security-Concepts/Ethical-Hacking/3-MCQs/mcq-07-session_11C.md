# 🔐 MCQ Set — Session 11C

**Module:** Security Concepts — Ethical Hacking
**Coverage:** Password Cracking Techniques · Windows Password Storage (SAM, LM, NT Hash) ·
SAM Extraction · Pass-the-Hash · Responder NTLMv2 Capture · Offline Cracking Pipeline
**Total Questions:** 30
**Format:** Foundation + Fundamental + Basic Concepts only

---

## 📋 Table of Contents

- [Questions — Q1 to Q30](#questions)
- [Answers & Explanations](#answers--explanations)
- [Quick Answer Key](#quick-answer-key)
- [Topic Coverage Map](#topic-coverage-map)

---

## Questions

---

**Q1.** Password cracking is BEST described as:

- A) Decrypting a hash using the encryption key stored alongside it
- B) Reversing the hash function mathematically to recover plaintext
- C) A forward search — hashing candidate passwords and comparing the output
   to the target hash until a match is found
- D) Intercepting plaintext passwords as they travel over the network

---

**Q2.** The `rockyou.txt` wordlist — the universal starting wordlist for
dictionary attacks — originated from which real-world incident?

- A) The 2016 LinkedIn breach that leaked 117 million SHA1 hashes
- B) The 2009 RockYou breach that exposed 32 million passwords stored
   in plain text
- C) The 2017 Equifax breach that exposed 147 million customer records
- D) The 2014 Yahoo breach that exposed 500 million user accounts

---

**Q3.** Analysis of leaked password databases consistently shows that the top
10,000 most common passwords account for approximately what percentage of all
user accounts?

- A) 1–5%
- B) 10–15%
- C) 30–40%
- D) 70–80%

---

**Q4.** In a brute force attack against an NT Hash on a modern GPU capable
of 10 billion attempts per second, an 8-character password using the FULL
ASCII printable character set (95 characters) would take approximately:

- A) 3 minutes
- B) 4.6 hours
- C) 69 years
- D) 640,000 years

---

**Q5.** A tester knows from LDAP enumeration that the target's password policy
requires: "1 uppercase letter, 4 lowercase letters, and 3 digits." Which
Hashcat attack type allows the tester to define a per-position character
pattern like `?u?l?l?l?l?d?d?d` to target ONLY policy-compliant passwords?

- A) Dictionary Attack
- B) Brute Force Attack
- C) Mask Attack
- D) Rainbow Table Attack

---

**Q6.** Rainbow table attacks are precomputed hash-to-plaintext lookups. Which
of the following hash types is VULNERABLE to rainbow table attacks?

- A) bcrypt with per-user salt
- B) Linux `/etc/shadow` with SHA-512 and random salt
- C) Windows NT Hash (no salt — same password always produces same hash)
- D) Argon2id with salt and memory-hard parameters

---

**Q7.** What cryptographic defense completely defeats rainbow table attacks by
ensuring that identical passwords produce DIFFERENT hashes for different users?

- A) Increasing hash output length from 128-bit to 256-bit
- B) Using a faster hash algorithm for quicker verification
- C) Adding a per-user random SALT before hashing
- D) Storing hashes in an encrypted database

---

**Q8.** In rule-based attacks, Hashcat applies transformation rules to dictionary
words to generate variants. Which rule combination would transform `"summer"`
into `"Summer2024!"`?

- A) `l $2$0$2$4 $!` (lowercase all + append 2024!)
- B) `c $2$0$2$4 $!` (capitalize first + append 2024!)
- C) `u $2$0$2$4 $!` (uppercase all + append 2024!)
- D) `r $2$0$2$4 $!` (reverse word + append 2024!)

---

**Q9.** Which attack type is described as the MOST EFFECTIVE in practice for
cracking human-chosen passwords because it mirrors the predictable patterns
people use when forced to add complexity?

- A) Pure Brute Force
- B) Rainbow Table Lookup
- C) Hybrid / Rule-Based Attack
- D) Birthday Attack

---

**Q10.** The Windows SAM (Security Account Manager) database is located at
which path on a Windows system?

- A) `C:\Windows\NTDS\ntds.dit`
- B) `%SYSTEMROOT%\System32\config\SAM`
- C) `C:\Users\Administrator\credentials.db`
- D) `HKLM\SOFTWARE\Microsoft\Credentials`

---

**Q11.** The SAM database is encrypted using SYSKEY — a 128-bit key derived
from which other Windows component?

- A) The user's login password directly
- B) The SYSTEM registry hive
- C) The Active Directory NTDS.DIT file
- D) The Windows Boot Configuration Data (BCD)

---

**Q12.** The LM Hash algorithm has THREE catastrophic weaknesses. Which of the
following is NOT one of LM Hash's weaknesses?

- A) Password is converted to UPPERCASE before hashing — eliminating case sensitivity
- B) Password is split into two independent 7-character halves
- C) The hash uses a per-user random salt making rainbow tables infeasible
- D) DES encryption uses a fixed, publicly known plaintext string (`KGS!@#$%`)

---

**Q13.** When examining an LM Hash dump, the second half shows the value
`AAD3B435B51404EE`. What does this IMMEDIATELY tell the attacker?

- A) The password contains only uppercase letters
- B) The password is exactly 14 characters long
- C) The password is 7 characters or fewer — the second half is all null bytes
- D) LM Hash is disabled and only NT Hash is stored

---

**Q14.** The NT Hash formula is:

- A) `SHA-256(ASCII(password))`
- B) `MD4(UTF-16-LE(password))`
- C) `bcrypt(password, salt, cost=12)`
- D) `DES(password, "KGS!@#$%")`

---

**Q15.** What is the NT Hash value for an EMPTY password (no password set)?

- A) `8846F7EAEE8FB117AD06BDD830B7586C`
- B) `AAD3B435B51404EEAAD3B435B51404EE`
- C) `31D6CFE0D16AE931B73C59D7E0C089C0`
- D) `E52CAC67419A9A224A3B108F3FA6CB6D`

---

**Q16.** NT Hash has two critical weaknesses that make it maximally vulnerable
to cracking. Which pair correctly identifies BOTH weaknesses?

- A) Short output length (64 bits) and case insensitivity
- B) No salt (same password = same hash) and MD4 is extremely fast to compute
- C) Uses DES encryption and splits password into halves
- D) Requires SYSTEM privileges to compute and uses SHA-1

---

**Q17.** Which SAM extraction method bypasses the kernel file lock by copying
the SAM file from a Windows backup snapshot?

- A) Mimikatz `sekurlsa::logonpasswords`
- B) Registry export (`reg save HKLM\SAM`)
- C) Volume Shadow Copy Service (VSS)
- D) Impacket `secretsdump.py` remotely via SMB

---

**Q18.** Mimikatz extracts credentials from which Windows process's memory,
potentially recovering NT Hashes and even cleartext passwords if WDigest
is enabled?

- A) explorer.exe
- B) svchost.exe
- C) lsass.exe (Local Security Authority Subsystem Service)
- D) csrss.exe

---

**Q19.** Windows Credential Guard (2024–2026) protects against Mimikatz by:

- A) Encrypting the SAM file with a stronger algorithm
- B) Moving LSASS into a VBS-protected (Virtualization-Based Security) memory
   region that even SYSTEM-level processes cannot read
- C) Disabling all NTLM authentication on the system
- D) Automatically rotating all user passwords every 24 hours

---

**Q20.** Pass-the-Hash (PtH) works because:

- A) The NT Hash can be reversed to recover the plaintext password for login
- B) NTLM authentication uses the NT Hash as the signing key — an attacker
   with the hash can compute valid responses without knowing the plaintext
- C) Windows stores passwords in plaintext alongside the hash
- D) Pass-the-Hash exploits a buffer overflow in the NTLM protocol

---

**Q21.** An attacker extracts the Administrator's NT Hash from one machine
and uses CrackMapExec to authenticate to 50 other machines on the subnet.
This works because all 50 machines were built from the same cloned image.
What defense would PREVENT this lateral movement?

- A) Enabling Windows Firewall on the Domain Controller only
- B) Deploying Microsoft LAPS — which generates unique random local admin
   passwords per machine
- C) Installing antivirus on all 50 machines
- D) Increasing the password complexity requirement to 12 characters

---

**Q22.** Which Windows security group, when accounts are added to it, blocks
NTLM authentication entirely and forces Kerberos-only — effectively preventing
Pass-the-Hash for those accounts?

- A) Domain Admins
- B) Enterprise Admins
- C) Protected Users
- D) Schema Admins

---

**Q23.** What is captured by Responder when it poisons LLMNR/NBNS broadcasts
on a network?

- A) The user's plaintext password transmitted over SMB
- B) The user's raw NT Hash from the SAM database
- C) An NTLMv2 challenge-response pair — which must be cracked offline to
   recover the password
- D) The user's Kerberos TGT ticket

---

**Q24.** The Hashcat mode number for cracking NTLMv2 hashes captured by
Responder is:

- A) `-m 1000` (NTLM / NT Hash)
- B) `-m 5600` (Net-NTLMv2)
- C) `-m 500` (md5crypt)
- D) `-m 3200` (bcrypt)

---

**Q25.** NTLMv2 cracking is SLOWER than pure NT Hash cracking because each
candidate requires:

- A) One SHA-256 computation instead of MD4
- B) Two operations: MD4 (to compute NT Hash) + HMAC-MD5 (to compute the
   NTLMv2 response)
- C) A rainbow table lookup that adds disk I/O overhead
- D) A network round-trip to the target server for verification

---

**Q26.** After a successful SMB Relay from Session 11B, `ntlmrelayx.py`
automatically runs which Impacket tool to extract all local account hashes
from the relay target?

- A) Mimikatz
- B) Hashcat
- C) secretsdump.py
- D) BloodHound

---

**Q27.** Where does the NTDS.DIT file reside, and what does it contain?

- A) On every workstation — contains local user NT Hashes
- B) On Domain Controllers at `C:\Windows\NTDS\ntds.dit` — contains NT Hashes
   for ALL domain accounts
- C) On the DNS server — contains DNSSEC encryption keys
- D) On the DHCP server — contains IP-to-MAC address mappings

---

**Q28.** In 2026, an AWS `p4d.24xlarge` instance (8× NVIDIA A100 GPUs) can
brute-force an 8-character full ASCII NT Hash in approximately 4.6 hours.
What is the approximate cloud compute cost for this?

- A) $15
- B) $147
- C) $1,500
- D) $15,000

---

**Q29.** PassGAN is an AI-powered password cracking tool. What technology
does it use to generate candidate passwords?

- A) Reinforcement Learning trained on firewall logs
- B) A GAN (Generative Adversarial Network) trained on leaked password
   databases that learns statistical patterns of human password creation
- C) A decision tree classifier that predicts password complexity
- D) A rule-based expert system using manually coded transformation rules

---

**Q30.** Under DPDPA 2023, if a SAM database exposure leaks employee NT Hashes
(username + password hash combinations), this constitutes a data breach. What
is the maximum penalty for such a breach under DPDPA 2023?

- A) ₹10 lakh
- B) ₹1 crore
- C) ₹50 crore
- D) ₹250 crore

---
&nbsp;

&nbsp;

&nbsp;

---

## Answers & Explanations

---

**Q1. Correct Answer: C) A forward search — hashing candidate passwords and
comparing the output to the target hash until a match is found** ✅

**Explanation:**
Cryptographic hash functions are **one-way** — they cannot be reversed or decrypted.
Password cracking does NOT reverse the hash. Instead, it performs a **forward search**:
1. Take a candidate password (e.g., `"password123"`)
2. Hash it using the same algorithm as the target
3. Compare the resulting hash to the target hash
4. Match → password found. No match → try next candidate.

The one-way property is irrelevant because the attacker never attempts reversal —
they guess forward until a match appears.

- **A)** — ❌ Hashes are not encryption — there is no "key" stored alongside them.
  Hashing is one-way; encryption is two-way with a key.
- **B)** — ❌ Hash functions are mathematically one-way — reversing them is
  computationally infeasible. Cracking is forward computation, not reversal.
- **C)** — ✅ Forward search: hash candidates → compare → match = cracked
- **D)** — ❌ Intercepting plaintext over the network is credential sniffing —
  a different technique entirely. Modern auth protocols (NTLM, Kerberos) don't
  transmit plaintext passwords.

---

**Q2. Correct Answer: B) The 2009 RockYou breach that exposed 32 million
passwords stored in plain text** ✅

**Explanation:**
**RockYou**, a social application company, stored 32 million user passwords in
**plain text** — no hashing, no encryption, nothing. When their database was breached
in December 2009, the complete list of 32 million real human-chosen passwords was
dumped publicly. This list became `rockyou.txt` — located at
`/usr/share/wordlists/rockyou.txt` on Kali Linux — and remains the universal
starting wordlist for password cracking because it represents actual password
choices by real users.

- **A)** — ❌ LinkedIn (2012/2016) leaked SHA1 hashes — not plaintext — and is not
  the origin of rockyou.txt
- **B)** — ✅ 2009 RockYou — 32 million plaintext passwords — origin of rockyou.txt
- **C)** — ❌ Equifax (2017) leaked PII — not password lists
- **D)** — ❌ Yahoo (2014) was a massive breach but not the source of rockyou.txt

---

**Q3. Correct Answer: C) 30–40%** ✅

**Explanation:**
Analysis of multiple leaked databases consistently shows that password diversity
among users is extremely low:
- The top 10 passwords account for 1–3% of all accounts
- The top 10,000 passwords account for **30–40%** of all accounts
- Over 70% of passwords are derived from dictionary words

This is why dictionary attacks are so effective — a relatively small wordlist
covers a disproportionately large number of accounts.

- **A) 1–5%** — ❌ This is the coverage of only the top ~10 passwords
- **B) 10–15%** — ❌ Understates the coverage of top 10,000 passwords
- **C) 30–40%** — ✅ Top 10,000 passwords cover 30–40% of accounts
- **D) 70–80%** — ❌ This is approximately the percentage derived from dictionary
  WORDS — but not all crackable by top 10,000 passwords alone

---

**Q4. Correct Answer: C) 69 years** ✅

**Explanation:**
The calculation for brute-forcing 8-character full ASCII (95 printable characters):

Keyspace = 95⁸ = 6,634,204,312,890,625 candidates
At 10 billion attempts/second = ~663,420 seconds ≈ **69 years**

However, the session notes also mention that a cloud GPU cluster (like AWS
p4d.24xlarge with 8× A100 GPUs at ~400 billion/sec) can exhaust this in
~4.6 hours. The 69 years figure is at the specified rate of 10 billion/sec
(a single modern GPU).

- **A) 3 minutes** — ❌ This is approximately correct for 8-char lowercase-only
- **B) 4.6 hours** — ❌ This is the time on a cloud GPU CLUSTER (~400B/sec) — not
  a single GPU at 10B/sec as specified in the question
- **C) 69 years** — ✅ At 10 billion/sec, 95⁸ candidates ≈ 69 years
- **D) 640,000 years** — ❌ This corresponds to a 10-character full ASCII keyspace

---

**Q5. Correct Answer: C) Mask Attack** ✅

**Explanation:**
A **Mask Attack** allows the tester to define a per-position character type pattern
using Hashcat's mask notation:
- `?u` = uppercase · `?l` = lowercase · `?d` = digit · `?s` = special · `?a` = all

Example: `?u?l?l?l?l?d?d?d` = 1 uppercase + 4 lowercase + 3 digits
Candidates: 26 × 26⁴ × 10³ ≈ 11.8 million → cracks in milliseconds.

By leveraging password policy knowledge from LDAP enumeration, a mask attack
collapses the search space by orders of magnitude compared to full brute force.

- **A) Dictionary** — ❌ Dictionary uses a fixed wordlist — cannot enforce per-position
  character type constraints
- **B) Brute Force** — ❌ Pure brute force tries ALL combinations — mask specifically
  constrains per position
- **C) Mask Attack** — ✅ Per-position character type definition — policy-targeted
- **D) Rainbow Table** — ❌ Rainbow tables are precomputed lookups — they don't use
  masks or per-position constraints

---

**Q6. Correct Answer: C) Windows NT Hash (no salt — same password always
produces same hash)** ✅

**Explanation:**
Rainbow tables require that the SAME input ALWAYS produces the SAME hash output.
This is only true for **unsalted** hash algorithms. NT Hash has **no salt** — every
Windows account with the password "password" has the identical NT Hash
`8846F7EAEE8FB117AD06BDD830B7586C`. This makes precomputed rainbow tables effective.

Salted algorithms (bcrypt, Argon2, Linux SHA-512) add a random per-user value
before hashing, so identical passwords produce different hashes — making rainbow
tables useless (each table would need to be rebuilt per salt value).

- **A) bcrypt** — ❌ bcrypt includes a per-user salt — rainbow tables are defeated
- **B) Linux SHA-512** — ❌ Uses random per-user salt — rainbow tables defeated
- **C) NT Hash** — ✅ No salt — vulnerable to rainbow tables
- **D) Argon2id** — ❌ Salted + memory-hard — rainbow tables completely infeasible

---

**Q7. Correct Answer: C) Adding a per-user random SALT before hashing** ✅

**Explanation:**
A **salt** is a random value unique to each user that is combined with the password
before hashing. This ensures that even if two users choose the identical password,
their stored hashes are DIFFERENT (because different salts produce different inputs
to the hash function).

Rainbow tables are precomputed for a SPECIFIC input → hash mapping. When a salt
is added, the rainbow table would need to be rebuilt for EVERY possible salt value
— making the attack computationally infeasible.

- **A)** — ❌ Increasing output length does not prevent identical inputs from
  producing identical outputs — the core rainbow table requirement
- **B)** — ❌ Faster algorithms make cracking EASIER, not harder — opposite of desired
- **C)** — ✅ Per-user salt ensures identical passwords → different hashes → rainbow
  tables defeated
- **D)** — ❌ Encrypting the hash database adds a layer but doesn't address the
  fundamental issue — if the database is accessed, unsalted hashes remain vulnerable

---

**Q8. Correct Answer: B) `c $2$0$2$4 $!` (capitalize first + append 2024!)** ✅

**Explanation:**
Hashcat rule operations:
- `c` = **capitalize** first letter (summer → Summer)
- `$2$0$2$4` = append characters "2024" one at a time (Summer → Summer2024)
- `$!` = append "!" (Summer2024 → Summer2024!)

Result: `"summer"` → `"Summer2024!"`

- **A) `l $2$0$2$4 $!`** — ❌ `l` = lowercase ALL letters → "summer2024!" (no capital S)
- **B) `c $2$0$2$4 $!`** — ✅ Capitalize first + append 2024 + append ! = "Summer2024!"
- **C) `u $2$0$2$4 $!`** — ❌ `u` = UPPERCASE ALL → "SUMMER2024!" (all caps)
- **D) `r $2$0$2$4 $!`** — ❌ `r` = reverse → "remmus2024!" (reversed word)

---

**Q9. Correct Answer: C) Hybrid / Rule-Based Attack** ✅

**Explanation:**
**Rule-based attacks** are the most effective in practice because they mirror exactly
how humans add "complexity" when forced by password policies. Studies consistently
show that users apply predictable transformations:
- `"password"` → `"Password1"` (capitalize + digit)
- `"summer"` → `"Summer2024!"` (capitalize + year + symbol)
- `"company"` → `"Company@123"` (company name + suffix)

Rule-based attacks systematically generate these variants from dictionary words,
achieving high crack rates with far fewer candidates than pure brute force.

- **A) Pure Brute Force** — ❌ Exhaustive but extremely slow for longer passwords —
  not the most effective in practice
- **B) Rainbow Table** — ❌ Only works against unsalted hashes and requires
  precomputation — not universally effective
- **C) Hybrid/Rule-Based** — ✅ Most effective — mirrors human password creation patterns
- **D) Birthday Attack** — ❌ Birthday attacks target hash collisions — a different
  cryptographic concept unrelated to password cracking

---

**Q10. Correct Answer: B) `%SYSTEMROOT%\System32\config\SAM`** ✅

**Explanation:**
The **SAM (Security Account Manager)** database storing NT Hashes for all local
user accounts is located at `%SYSTEMROOT%\System32\config\SAM` — which typically
resolves to `C:\Windows\System32\config\SAM`. It is kernel-locked while Windows
is running — a standard file copy operation will fail. Extraction requires VSS,
registry export, or LSASS memory extraction.

- **A)** — ❌ `ntds.dit` is the Active Directory database on Domain Controllers —
  stores DOMAIN account hashes, not local accounts
- **B)** — ✅ SAM location: `%SYSTEMROOT%\System32\config\SAM`
- **C)** — ❌ This path doesn't exist — Windows doesn't use a `credentials.db` file
- **D)** — ❌ This is a registry path format — but not where SAM data is physically stored

---

**Q11. Correct Answer: B) The SYSTEM registry hive** ✅

**Explanation:**
The SAM database has been encrypted with **SYSKEY** since Windows NT 4.0 SP3 (1997).
The 128-bit SYSKEY encryption key is derived from values stored in the **SYSTEM
registry hive** (`HKLM\SYSTEM\CurrentControlSet\Control\Lsa\`). This means:
- A raw SAM file copy is useless without the SYSTEM hive
- Both SAM AND SYSTEM must be extracted together to decrypt the hashes
- `secretsdump.py` requires BOTH files: `-sam SAM -system SYSTEM LOCAL`

- **A)** — ❌ SYSKEY is NOT derived from the user's login password — it's a system-level
  boot key independent of any user password
- **B)** — ✅ SYSKEY is derived from the SYSTEM registry hive
- **C)** — ❌ NTDS.DIT is the AD database — it's encrypted separately using a boot key
  but is not the source of SYSKEY for the local SAM
- **D)** — ❌ BCD contains boot configuration — not the SYSKEY encryption key

---

**Q12. Correct Answer: C) The hash uses a per-user random salt making rainbow
tables infeasible** ✅

**Explanation:**
LM Hash's three ACTUAL catastrophic weaknesses are:
1. **Case insensitive** — converts to UPPERCASE before hashing
2. **Splits into two 7-character halves** — cracks two short passwords instead of one
3. **DES on known plaintext** — encrypts the fixed string `KGS!@#$%` using password as key

Option C describes a STRENGTH (salting) — which LM Hash does NOT have. LM Hash
has NO salt at all, which is actually a fourth weakness. The question asks what
is NOT one of the three named weaknesses.

- **A)** — ❌ This IS a weakness — case insensitivity reduces the charset
- **B)** — ❌ This IS a weakness — splitting halves the effective length
- **C)** — ✅ LM Hash does NOT use salt — this statement describes a feature LM
  LACKS, not a weakness it has
- **D)** — ❌ This IS a weakness — DES encrypting a known, public plaintext

---

**Q13. Correct Answer: C) The password is 7 characters or fewer — the second
half is all null bytes** ✅

**Explanation:**
LM Hash splits passwords into two 7-character halves. If the password is 7
characters or fewer, the second half consists entirely of null bytes (padding).
When DES encrypts the fixed string `KGS!@#$%` with 7 null bytes as the key,
the result is ALWAYS `AAD3B435B51404EE` — a constant value.

Seeing `AAD3B435B51404EE` as the second half immediately reveals the password
is 7 characters or shorter — one hash comparison tells the attacker the
approximate password length.

- **A)** — ❌ The constant doesn't indicate character type — it indicates length
- **B)** — ❌ A 14-character password would have BOTH halves populated — not showing
  the constant
- **C)** — ✅ `AAD3B435B51404EE` as second half = password ≤ 7 chars
- **D)** — ❌ When LM is disabled, BOTH halves show `AAD3B435B51404EE` — not just
  the second half. The question states only the second half shows this value.

---

**Q14. Correct Answer: B) `MD4(UTF-16-LE(password))`** ✅

**Explanation:**
The NT Hash formula is:
1. Encode password as **UTF-16 Little Endian** Unicode
2. Apply the **MD4** hash function
3. Result: 128-bit output = 32 hexadecimal characters

Example: `NT_Hash("password") = 8846F7EAEE8FB117AD06BDD830B7586C`

- **A)** — ❌ SHA-256 and ASCII encoding are NOT used in NT Hash
- **B)** — ✅ `MD4(UTF-16-LE(password))` — the correct NT Hash formula
- **C)** — ❌ bcrypt with salt is a modern secure hash — NOT what Windows SAM uses
- **D)** — ❌ DES with `KGS!@#$%` is the LM Hash algorithm — not NT Hash

---

**Q15. Correct Answer: C) `31D6CFE0D16AE931B73C59D7E0C089C0`** ✅

**Explanation:**
The NT Hash of an empty password (empty string) is:
`31D6CFE0D16AE931B73C59D7E0C089C0`

Seeing this value in a SAM dump means the account has **no password set** — the
attacker can authenticate with an empty password string. No cracking needed.

Key NT Hash constants:
- `31D6CFE0D16AE931B73C59D7E0C089C0` = empty password
- `8846F7EAEE8FB117AD06BDD830B7586C` = "password"
- `AAD3B435B51404EEAAD3B435B51404EE` = LM Hash disabled (placeholder)

- **A)** — ❌ This is the NT Hash of `"password"` — not empty
- **B)** — ❌ This is the LM Hash disabled placeholder — not an NT Hash of empty
- **C)** — ✅ NT Hash of empty password
- **D)** — ❌ This is not a recognized standard constant

---

**Q16. Correct Answer: B) No salt (same password = same hash) and MD4 is
extremely fast to compute** ✅

**Explanation:**
NT Hash's two critical weaknesses:

1. **No salt:** Every account with the same password produces the IDENTICAL hash.
   This enables Pass-the-Hash (one hash works everywhere the password is reused),
   rainbow table attacks, and identical-hash detection across accounts.

2. **MD4 is extremely fast:** A single RTX 4090 computes 100–150 billion NT Hashes
   per second. Compare to bcrypt (cost-12): ~10,000/sec. NT Hash is 10–15 MILLION
   times faster to crack than bcrypt.

The combination — no salt + fast algorithm — makes NT Hash maximally vulnerable.

- **A)** — ❌ NT Hash output is 128-bit (not 64-bit) and IS case sensitive
- **B)** — ✅ No salt + fast MD4 = maximally vulnerable combination
- **C)** — ❌ DES and splitting into halves are LM Hash weaknesses — not NT Hash
- **D)** — ❌ NT Hash uses MD4 (not SHA-1) and does NOT require SYSTEM privileges
  to compute

---

**Q17. Correct Answer: C) Volume Shadow Copy Service (VSS)** ✅

**Explanation:**
The SAM file is **kernel-locked** while Windows is running — standard copy operations
fail. **Volume Shadow Copy Service (VSS)** creates backup snapshots of the entire
volume. These snapshots contain a copy of the SAM file that is NOT locked. The
attacker accesses the VSS snapshot to copy the SAM (and SYSTEM) files.

```cmd 
copy \\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy1\Windows\System32\config\SAM C:\temp\SAM
```
- **A) Mimikatz** — ❌ Mimikatz extracts from LSASS process memory — it bypasses
  the SAM FILE entirely rather than copying it
- **B) Registry export** — ❌ `reg save HKLM\SAM` exports the live registry hive —
  it works but through a different mechanism (registry API) than VSS
- **C) VSS** — ✅ Copies from backup snapshot — bypasses kernel file lock
- **D) secretsdump remotely** — ❌ Works over SMB remotely — doesn't copy the
  physical SAM file at all

---

**Q18. Correct Answer: C) lsass.exe (Local Security Authority Subsystem Service)** ✅

**Explanation:**
**LSASS (Local Security Authority Subsystem Service)** is the Windows process
responsible for enforcing security policy and handling authentication. It holds
in memory:
- NT Hashes for every currently logged-in user
- Kerberos tickets
- **Cleartext passwords** if WDigest authentication is enabled (Windows 7 / Server
  2008 R2 era, or manually re-enabled via registry)

Mimikatz's `sekurlsa::logonpasswords` command reads LSASS process memory to
extract all of these credentials.

- **A) explorer.exe** — ❌ Windows Explorer shell — does not store credentials
- **B) svchost.exe** — ❌ Generic service host — does not store authentication data
- **C) lsass.exe** — ✅ LSASS holds all logged-in user credentials in memory
- **D) csrss.exe** — ❌ Client/Server Runtime — subsystem process, not auth-related

---

**Q19. Correct Answer: B) Moving LSASS into a VBS-protected (Virtualization-Based
Security) memory region that even SYSTEM-level processes cannot read** ✅

**Explanation:**
**Windows Credential Guard** uses **Virtualization-Based Security (VBS)** to create
an isolated memory region protected by the hypervisor. LSASS (or more precisely,
the credential secrets) are moved into this protected enclave. Even a process
running with SYSTEM privileges cannot read this VBS-protected memory — because the
hypervisor enforces the boundary at a level below the OS kernel. Mimikatz cannot
extract credentials from Credential Guard-protected LSASS.

- **A)** — ❌ Credential Guard protects LSASS memory — not the SAM file encryption
- **B)** — ✅ VBS-protected memory region — hypervisor-enforced isolation
- **C)** — ❌ Credential Guard does not disable NTLM entirely — it protects secrets
  from extraction
- **D)** — ❌ Credential Guard does not rotate passwords — that's a different function

---

**Q20. Correct Answer: B) NTLM authentication uses the NT Hash as the signing
key — an attacker with the hash can compute valid responses without knowing
the plaintext** ✅

**Explanation:**
In NTLM authentication, the client proves identity by computing:NTLMv2_Response = HMAC-MD5(NT_Hash, server_challenge + username + domain + ...)
The **NT Hash IS the authentication secret** — it's the key used to compute the
valid response. An attacker who possesses the NT Hash can compute the exact same
response the legitimate client would produce. The server cannot distinguish between
a legitimate client using the plaintext password (which gets hashed to the same
NT Hash internally) and an attacker using the NT Hash directly.

- **A)** — ❌ NT Hash CANNOT be reversed — PtH doesn't reverse anything
- **B)** — ✅ NT Hash is the auth key — valid responses computed directly from it
- **C)** — ❌ Windows does NOT store plaintext alongside hashes (unless WDigest
  is enabled in LSASS memory)
- **D)** — ❌ PtH is not a buffer overflow — it's using the legitimate auth
  mechanism with a stolen credential

---

**Q21. Correct Answer: B) Deploying Microsoft LAPS — which generates unique
random local admin passwords per machine** ✅

**Explanation:**
**LAPS (Local Administrator Password Solution)** generates a **unique, random**
local administrator password for EACH machine, stored in Active Directory. If
an attacker extracts the Administrator hash from Machine A, that hash will NOT
work on Machine B (different password = different hash). This completely eliminates
PtH lateral movement via shared local admin credentials.

The scenario describes a classic cloned-image problem — identical admin passwords
across all machines. LAPS is the direct solution.

- **A)** — ❌ Windows Firewall on DC only doesn't protect workstations
- **B)** — ✅ LAPS = unique password per machine = PtH from one doesn't work on others
- **C)** — ❌ Antivirus doesn't prevent legitimate NTLM authentication using valid hashes
- **D)** — ❌ Increasing complexity doesn't help if all machines share the SAME password
  — the hash is still identical everywhere

---

**Q22. Correct Answer: C) Protected Users** ✅

**Explanation:**
The **Protected Users** security group in Active Directory applies specific
credential protections to its members:
- NTLM authentication is **blocked** — members can only use Kerberos
- No NTLM hash is cached in LSASS memory
- No WDigest cleartext stored
- No DES or RC4 in Kerberos (AES only)

Since PtH requires NTLM authentication, blocking NTLM for Protected Users
members effectively prevents PtH for those accounts.

- **A) Domain Admins** — ❌ Domain Admins is a privilege group — it grants access,
  doesn't restrict authentication methods
- **B) Enterprise Admins** — ❌ Same — privilege group, not auth restriction
- **C) Protected Users** — ✅ Blocks NTLM, forces Kerberos only = prevents PtH
- **D) Schema Admins** — ❌ Controls AD schema changes — not auth methods

---

**Q23. Correct Answer: C) An NTLMv2 challenge-response pair — which must be
cracked offline to recover the password** ✅

**Explanation:**
Responder poisons LLMNR/NBNS broadcasts, causing victims to authenticate to
Responder's fake SMB/HTTP servers. What is captured is an **NTLMv2
challenge-response pair** — NOT the plaintext password and NOT the raw NT Hash.

The NTLMv2 response contains:HMAC-MD5(NT_Hash, server_challenge + client_challenge + username + domain + timestamp)
To recover the password, this captured response must be cracked **offline** using
Hashcat (`-m 5600`) with wordlists and rules.

- **A)** — ❌ Plaintext passwords are NEVER transmitted in NTLM authentication
- **B)** — ❌ The raw NT Hash from SAM is not transmitted over the network — only
  the challenge-response computed FROM it
- **C)** — ✅ NTLMv2 challenge-response pair — requires offline cracking
- **D)** — ❌ Kerberos tickets are a different authentication protocol — Responder
  captures NTLM, not Kerberos

---

**Q24. Correct Answer: B) `-m 5600` (Net-NTLMv2)** ✅

**Explanation:**
Hashcat mode numbers for Windows credential types:

| Mode | Hash Type | Source |
|---|---|---|
| `-m 1000` | NTLM / NT Hash | SAM dump, NTDS.DIT extraction |
| **`-m 5600`** | **Net-NTLMv2** | **Responder network capture** |

Responder captures are NTLMv2 network authentication responses — NOT raw NT Hashes.
They require different computation (MD4 + HMAC-MD5 per candidate) and use mode 5600.

- **A) `-m 1000`** — ❌ Mode 1000 is for pure NT Hashes from SAM dumps — not
  Responder captures
- **B) `-m 5600`** — ✅ Net-NTLMv2 — correct mode for Responder-captured hashes
- **C) `-m 500`** — ❌ md5crypt — used for Linux `/etc/shadow` MD5 hashes
- **D) `-m 3200`** — ❌ bcrypt — used for bcrypt-hashed passwords

---

**Q25. Correct Answer: B) Two operations: MD4 (to compute NT Hash) + HMAC-MD5
(to compute the NTLMv2 response)** ✅

**Explanation:**
For each candidate password during NTLMv2 cracking, Hashcat must:
1. Compute `NT_Hash(candidate) = MD4(UTF-16-LE(candidate))`
2. Compute `NTLMv2_Response = HMAC-MD5(NT_Hash, challenge_data)`
3. Compare to the captured NTLMv2 response

This is **two cryptographic operations per candidate** — compared to just ONE
(MD4 only) for pure NT Hash cracking from SAM dumps. GPU speed for NTLMv2 is
approximately 3–5 billion/sec versus 100–150 billion/sec for pure NT Hash.

- **A)** — ❌ SHA-256 is not used in NTLM — NT Hash uses MD4
- **B)** — ✅ Two operations (MD4 + HMAC-MD5) per candidate = slower than SAM cracking
- **C)** — ❌ Rainbow tables are a different attack type — not relevant to the speed
  comparison between NT Hash and NTLMv2 cracking
- **D)** — ❌ Offline cracking has NO network round-trips — all computation is local

---

**Q26. Correct Answer: C) secretsdump.py** ✅

**Explanation:**
After `ntlmrelayx.py` successfully relays NTLM authentication to a target server,
it automatically executes **`secretsdump.py`** — an Impacket tool that extracts
all local account hashes from the target's SAM database over SMB. The entire
pipeline from NTLM relay → hash extraction is a single automated operation.

Output format:Administrator:500:aad3b435b51404eeaad3b435b51404ee:[NT_HASH]:::

- **A) Mimikatz** — ❌ Mimikatz extracts from LSASS memory — ntlmrelayx uses
  secretsdump for remote SAM extraction
- **B) Hashcat** — ❌ Hashcat cracks hashes — it doesn't extract them from systems
- **C) secretsdump.py** — ✅ Automatically executed by ntlmrelayx after successful relay
- **D) BloodHound** — ❌ BloodHound maps AD relationships — it doesn't extract SAM hashes

---

**Q27. Correct Answer: B) On Domain Controllers at `C:\Windows\NTDS\ntds.dit` —
contains NT Hashes for ALL domain accounts** ✅

**Explanation:**
**NTDS.DIT** (NT Directory Services - Directory Information Tree) is the Active
Directory database file stored on every **Domain Controller**. It contains the
NT Hashes for ALL domain user accounts — not just local accounts like SAM. If an
attacker compromises a Domain Controller and extracts NTDS.DIT (+ SYSTEM hive),
they have the credentials for every user in the entire domain.

- **A)** — ❌ Workstations store local credentials in SAM — not NTDS.DIT
- **B)** — ✅ Domain Controllers — NTDS.DIT — all domain account hashes
- **C)** — ❌ DNS servers don't store NTDS.DIT — and it doesn't contain DNSSEC keys
- **D)** — ❌ DHCP servers store IP leases — not credential databases

---

**Q28. Correct Answer: B) $147** ✅

**Explanation:**
AWS cost calculation for NT Hash brute force:

| Parameter | Value |
|---|---|
| Instance | p4d.24xlarge (8× NVIDIA A100) |
| Cost | ~$32/hour |
| Speed | ~400 billion NT Hashes/second |
| 8-char full ASCII keyspace | 95⁸ ≈ 6.6 × 10¹⁵ |
| Time | ~4.6 hours |
| **Total cost** | **~$147 (~$32 × 4.6 hours)** |

This demonstrates that in 2026, 8-character passwords of ANY complexity can be
brute-forced for approximately $150 in cloud compute — making 8 characters
effectively dead as a security minimum for NT Hash.

- **A) $15** — ❌ Too low — 4.6 hours at $32/hour ≠ $15
- **B) $147** — ✅ ~$32/hour × ~4.6 hours ≈ $147
- **C) $1,500** — ❌ Too high by approximately 10×
- **D) $15,000** — ❌ Far too high — 100× the actual cost

---

**Q29. Correct Answer: B) A GAN (Generative Adversarial Network) trained on
leaked password databases that learns statistical patterns of human password
creation** ✅

**Explanation:**
**PassGAN** uses a **Generative Adversarial Network (GAN)** — a type of deep
learning architecture — trained on leaked password databases (like RockYou2021
with 8.4 billion entries). Unlike rule-based tools that apply fixed transformation
patterns, PassGAN LEARNS the statistical patterns of how humans create passwords
and generates candidates that follow those patterns — covering combinations that
no fixed ruleset would produce.

A 2023 study found PassGAN cracked 51% of common passwords in under 1 minute
and 81% within 1 month.

- **A)** — ❌ PassGAN is not trained on firewall logs — it's trained on leaked passwords
- **B)** — ✅ GAN trained on leaked password databases — learns human password patterns
- **C)** — ❌ PassGAN is generative (creates candidates) — not a classifier
- **D)** — ❌ PassGAN uses machine learning — the whole point is to go BEYOND
  manually coded rules

---

**Q30. Correct Answer: D) ₹250 crore** ✅

**Explanation:**
Under **DPDPA 2023**, a SAM database exposure that leaks employee NT Hashes
(username + password hash = personal data combination) constitutes a data breach.
The maximum penalty under DPDPA 2023 Section 33 for a data breach is up to
**₹250 crore (₹2.5 billion)**.

Additionally, failure to notify the Data Protection Board of a breach carries
a separate penalty of up to ₹200 crore.

- **A) ₹10 lakh** — ❌ Far below the DPDPA maximum
- **B) ₹1 crore** — ❌ Still far below the maximum
- **C) ₹50 crore** — ❌ Below the maximum — ₹50 crore applies to some lesser violations
- **D) ₹250 crore** — ✅ Maximum penalty under DPDPA 2023 for major data breaches

---

## Quick Answer Key

| Q | Answer | Q | Answer | Q | Answer |
|---|---|---|---|---|---|
| Q1 | C | Q11 | B | Q21 | B |
| Q2 | B | Q12 | C | Q22 | C |
| Q3 | C | Q13 | C | Q23 | C |
| Q4 | C | Q14 | B | Q24 | B |
| Q5 | C | Q15 | C | Q25 | B |
| Q6 | C | Q16 | B | Q26 | C |
| Q7 | C | Q17 | C | Q27 | B |
| Q8 | B | Q18 | C | Q28 | B |
| Q9 | C | Q19 | B | Q29 | B |
| Q10 | B | Q20 | B | Q30 | D |

---

## Topic Coverage Map

| Q | Section | Concept Tested |
|---|---|---|
| Q1 | Section 1 | Password cracking — forward search definition |
| Q2 | Section 1 | rockyou.txt — origin (2009 RockYou breach) |
| Q3 | Section 1 | Dictionary attacks — top 10K passwords coverage (30–40%) |
| Q4 | Section 1 | Brute force — 8-char full ASCII time at 10B/sec |
| Q5 | Section 1 | Mask attacks — per-position character pattern |
| Q6 | Section 1 | Rainbow tables — which hashes are vulnerable (unsalted) |
| Q7 | Section 1 | Salt — defeats rainbow tables |
| Q8 | Section 1 | Rule-based attacks — Hashcat rule syntax |
| Q9 | Section 1 | Hybrid/rule-based — most effective attack type |
| Q10 | Section 2 | SAM database — file path location |
| Q11 | Section 2 | SYSKEY — derived from SYSTEM registry hive |
| Q12 | Section 2 | LM Hash — three weaknesses (what is NOT one) |
| Q13 | Section 2 | LM Hash — AAD3B435B51404EE second half = ≤7 chars |
| Q14 | Section 2 | NT Hash — formula: MD4(UTF-16-LE(password)) |
| Q15 | Section 2 | NT Hash — empty password constant |
| Q16 | Section 2 | NT Hash — two critical weaknesses (no salt + fast MD4) |
| Q17 | Section 2 | SAM extraction — VSS bypasses kernel lock |
| Q18 | Section 2 | Mimikatz — extracts from lsass.exe memory |
| Q19 | Section 2 | Credential Guard — VBS-protected LSASS |
| Q20 | Section 2 | Pass-the-Hash — NT Hash as NTLM signing key |
| Q21 | Section 2 | PtH defense — LAPS (unique per-machine passwords) |
| Q22 | Section 2 | Protected Users group — blocks NTLM, forces Kerberos |
| Q23 | Section 3 | Responder capture — NTLMv2 challenge-response pair |
| Q24 | Section 3 | Hashcat mode — `-m 5600` for NTLMv2 |
| Q25 | Section 3 | NTLMv2 cracking speed — two operations per candidate |
| Q26 | Section 3 | ntlmrelayx auto-runs secretsdump.py after relay |
| Q27 | Section 2 | NTDS.DIT — location and contents (all domain hashes) |
| Q28 | Section 5 | Cloud GPU cracking — 8-char full ASCII cost (~$147) |
| Q29 | Section 5 | PassGAN — GAN trained on leaked passwords |
| Q30 | Section 5 | DPDPA 2023 — maximum penalty ₹250 crore |

---