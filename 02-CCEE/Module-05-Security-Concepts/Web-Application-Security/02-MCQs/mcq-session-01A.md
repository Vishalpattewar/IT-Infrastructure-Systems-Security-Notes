# mcq-01-session_01A.md
# MCQ Set — Session 01A : OWASP Top 10 (2017 · 2021 · 2025)

---

## 📑 Index

- [Instructions](#instructions)
- [MCQs — Q01 to Q30](#mcqs)
- [Quick Answer Key](#quick-answer-key)

---

## Instructions

- 30 questions — covers core syllabus + 📌 Extra Notes from Session 01A
- One correct answer per question
- ✅ marks the correct option
- Full explanation follows every question — including **why each wrong option is wrong**
- Questions are deliberately tricky — watch for one-word differences, position swaps, and version traps

---

## MCQs

---

### Q01
**In OWASP Top 10 2025, which category made the single largest upward jump compared to its position in the 2021 list?**

- A) Injection
- B) Broken Access Control
- C) ✅ Security Misconfiguration
- D) Software Supply Chain Failures

**Explanation:**
- ✅ **C is correct.** Security Misconfiguration moved from **A05:2021 → A02:2025** — a jump of 3 positions — the largest upward move of any retained category in the 2025 edition. This was driven by real-world breach data showing cloud misconfigurations (IAM sprawl, public S3 buckets, default credentials) as a primary attack vector.
- ❌ **A — Injection** actually **dropped** — from A03:2021 to A05:2025.
- ❌ **B — Broken Access Control** stayed at **A01** in both 2021 and 2025 — no movement.
- ❌ **D — Software Supply Chain Failures** is a **new category** in 2025 — it didn't exist in 2021 as the same name, so it doesn't count as a "jump."

---

### Q02
**Which OWASP Top 10 2021 category was completely absorbed into Broken Access Control (A01:2025) in the 2025 edition?**

- A) Insecure Design
- B) XML External Entities (XXE)
- C) Cryptographic Failures
- D) ✅ Server-Side Request Forgery (SSRF)

**Explanation:**
- ✅ **D is correct.** SSRF was a brand-new standalone category at **A10:2021** (added via community survey). In 2025, it was absorbed into **A01:2025 Broken Access Control** because SSRF is fundamentally an access control failure — the server makes requests the attacker should not be able to trigger. CWE-918 (SSRF) now maps under A01:2025.
- ❌ **A — Insecure Design** (A04:2021) was retained in 2025 as **A06:2025** — it moved down but was not absorbed.
- ❌ **B — XXE** was absorbed into **Security Misconfiguration** back in **2021** — it has no standalone existence in either 2021 or 2025.
- ❌ **C — Cryptographic Failures** remained a standalone category — it moved from A02:2021 to A04:2025.

---

### Q03
**What is the precise name of A09 in the OWASP Top 10 2025, and how does it differ from its 2021 name?**

- A) "Security Logging and Monitoring Failures" — no change from 2021
- B) "Security Logging and Auditing Failures" — "Monitoring" replaced by "Auditing"
- C) ✅ "Security Logging and Alerting Failures" — "Monitoring" replaced by "Alerting"
- D) "Security Logging and Detection Failures" — "Monitoring" replaced by "Detection"

**Explanation:**
- ✅ **C is correct.** The exact one-word change is **"Monitoring" → "Alerting"** in 2025. This was deliberate — OWASP emphasized that passively watching logs is insufficient; the system must actively **alert** on anomalies to have security value.
- ❌ **A** is wrong — there **is** a name change, even if subtle.
- ❌ **B — "Auditing"** is not the word used — "Alerting" is the replacement.
- ❌ **D — "Detection"** is not used in the official name.

> [!TIP]
> This is a classic one-word trap. The answer is **"Alerting"** — not "Monitoring," "Auditing," or "Detection."

---

### Q04
**Which of the following categories had the same name AND the same position in both OWASP Top 10 2021 and OWASP Top 10 2025?**

- A) Cryptographic Failures
- B) Injection
- C) Insecure Design
- D) ✅ Software or Data Integrity Failures

**Explanation:**
- ✅ **D is correct.** A08 — Software or Data Integrity Failures — held position **#8 in both 2021 and 2025**, with only a trivial grammatical change ("and" → "or") that does not constitute a rename. Name and position are effectively unchanged.
- ❌ **A — Cryptographic Failures** moved from **A02:2021 → A04:2025** — same name, different position.
- ❌ **B — Injection** moved from **A03:2021 → A05:2025** — same name, different position.
- ❌ **C — Insecure Design** moved from **A04:2021 → A06:2025** — same name, different position.

---

### Q05
**In OWASP Top 10 2017, Cross-Site Scripting (XSS) was listed as a standalone category. What happened to it in 2021?**

- A) It was removed entirely from the Top 10 framework
- B) It was merged into Security Misconfiguration (A05:2021)
- C) It was retained as a standalone category but renamed
- D) ✅ It was merged into the Injection category (A03:2021)

**Explanation:**
- ✅ **D is correct.** XSS (A7:2017) was merged into **A03:2021 Injection** because XSS is fundamentally an injection attack — untrusted data is injected into an output context and interpreted as code by the browser. This consolidation was retained in 2025 (XSS remains under A05:2025 Injection).
- ❌ **A** is wrong — XSS was not removed; it was reclassified as a sub-type of Injection.
- ❌ **B** is wrong — XXE (not XSS) was merged into Security Misconfiguration.
- ❌ **C** is wrong — XSS did not survive as a standalone category after 2017.

---

### Q06
**An attacker sends the following input into a login form: `' OR '1'='1`. What is the correct OWASP 2025 classification and what defense directly prevents this?**

- A) A01:2025 Broken Access Control — implement RBAC
- B) ✅ A05:2025 Injection — use parameterized queries / prepared statements
- C) A02:2025 Security Misconfiguration — disable error messages
- D) A07:2025 Authentication Failures — implement MFA

**Explanation:**
- ✅ **B is correct.** This is a classic SQL injection payload — `' OR '1'='1` makes a WHERE clause always evaluate to true, bypassing authentication. SQL Injection is under **A05:2025 Injection**. The primary and most effective defense is **parameterized queries / prepared statements**, which prevent user input from being interpreted as SQL code.
- ❌ **A** is wrong — RBAC controls what an authenticated user can access; it doesn't prevent SQLi from bypassing authentication in the first place.
- ❌ **C** is wrong — disabling error messages (security hardening) is a defense-in-depth measure, not the primary SQLi defense. It doesn't prevent the injection.
- ❌ **D** is wrong — MFA adds a second factor after authentication, but if SQLi bypasses the first-factor query entirely, MFA placement depends on architecture; regardless, parameterized queries is the direct fix.

---

### Q07
**The Heartland Payment Systems breach (2008) resulted in the exfiltration of over 130 million credit card numbers. What was the initial attack vector?**

- A) Insecure deserialization via a Java gadget chain
- B) Server-Side Request Forgery against the payment processor's internal APIs
- C) ✅ SQL Injection exploited through a vulnerable web form
- D) Broken Authentication via credential stuffing

**Explanation:**
- ✅ **C is correct.** The Heartland breach was initiated via **SQL Injection** through a vulnerable web form, mapping to **A05:2025 Injection**. Attackers used the SQLi to pivot and plant malware on internal payment systems, leading to the massive card data exfiltration.
- ❌ **A** is wrong — insecure deserialization (A08) was not the attack vector; that's associated with the Equifax/Apache Struts breach.
- ❌ **B** is wrong — SSRF was not the vector at Heartland.
- ❌ **D** is wrong — credential stuffing (A07) was not the initial entry point.

> [!NOTE]
> Keep breach-to-attack-type mappings sharp: **Heartland = SQLi**, **Equifax = Deserialization (Apache Struts)**, **SolarWinds = Supply Chain / Build Compromise**, **Capital One = SSRF + Misconfiguration**.

---

### Q08
**Which of the following is the correct position of "Injection" across all three OWASP editions?**

- A) A1:2017 → A01:2021 → A01:2025
- B) A3:2017 → A03:2021 → A05:2025
- C) ✅ A1:2017 → A03:2021 → A05:2025
- D) A1:2017 → A02:2021 → A04:2025

**Explanation:**
- ✅ **C is correct.** Injection was the **#1 risk from 2003 through 2017**. In 2021 it dropped to **A03**, and in 2025 it dropped further to **A05** — due to reduced incidence rates from widespread parameterized query adoption, not reduced severity.
- ❌ **A** — Injection was never #1 in 2021 or 2025.
- ❌ **B** — Injection was #1 in 2017 (A1), not #3 (A3).
- ❌ **D** — Both 2021 and 2025 positions are wrong in this option.

---

### Q09
**The Capital One breach (2019) is commonly cited in OWASP training. Which TWO OWASP 2025 categories does it best illustrate?**

- A) A05 Injection + A07 Authentication Failures
- B) A04 Cryptographic Failures + A08 Software or Data Integrity Failures
- C) ✅ A01 Broken Access Control + A02 Security Misconfiguration
- D) A03 Software Supply Chain Failures + A10 Mishandling of Exceptional Conditions

**Explanation:**
- ✅ **C is correct.** The Capital One breach involved two compounding failures: (1) **SSRF** (now under A01:2025 Broken Access Control) — the misconfigured WAF was exploited via SSRF to reach the EC2 metadata endpoint, and (2) **Security Misconfiguration (A02:2025)** — the IAM role attached to the server had excessively permissive policies (over-privileged role = misconfiguration). Together they enabled full data access.
- ❌ **A** — No SQL injection or authentication bypass was involved.
- ❌ **B** — No cryptographic or integrity failures were the primary vectors.
- ❌ **D** — No supply chain compromise or exception handling failure was involved.

---

### Q10
**Which OWASP Top 10 2025 category is described as covering flaws that "cannot be patched — they require redesign"?**

- A) A02:2025 Security Misconfiguration
- B) A07:2025 Authentication Failures
- C) A01:2025 Broken Access Control
- D) ✅ A06:2025 Insecure Design

**Explanation:**
- ✅ **D is correct.** Insecure Design (A06:2025) specifically addresses architectural and design-level weaknesses that are **baked into the blueprint** before code is written. The OWASP definition explicitly states these cannot be fixed by patching — the design must be changed. Example: a 4-digit PIN reset mechanism is insecure by design regardless of how correctly the PIN validation code is written.
- ❌ **A** — Misconfigurations can often be patched or corrected through configuration changes.
- ❌ **B** — Authentication failures are often implementation-level issues fixable through patching.
- ❌ **C** — Access control failures can often be fixed by adding/correcting authorization checks in code.

---

### Q11
**XML External Entities (XXE) was a standalone OWASP Top 10 category in 2017 at position A4. Into which category was it merged in 2021?**

- A) ✅ A05:2021 Security Misconfiguration
- B) A03:2021 Injection
- C) A08:2021 Software and Data Integrity Failures
- D) A01:2021 Broken Access Control

**Explanation:**
- ✅ **A is correct.** XXE (A4:2017) was merged into **A05:2021 Security Misconfiguration** in 2021 — and remains there in 2025. The rationale: XXE occurs because XML external entity processing is **enabled when it should be disabled** — a configuration failure, not a standalone vulnerability class.
- ❌ **B** — XSS (not XXE) was merged into Injection (A03:2021).
- ❌ **C** — Insecure Deserialization (A8:2017) was merged into A08:2021 Software & Data Integrity Failures — not XXE.
- ❌ **D** — XXE was not merged into Broken Access Control (SSRF was, but in 2025, not 2021).

---

### Q12
**An organization's application auto-downloads and installs software updates without verifying digital signatures. An attacker intercepts the update channel and delivers a backdoored update. Which OWASP 2025 category does this primarily fall under?**

- A) A02:2025 Security Misconfiguration
- B) A01:2025 Broken Access Control
- C) A07:2025 Authentication Failures
- D) ✅ A08:2025 Software or Data Integrity Failures

**Explanation:**
- ✅ **D is correct.** Auto-updating without signature verification is a **software integrity failure** — the application trusts data/code without verifying it hasn't been tampered with. This maps directly to **A08:2025 Software or Data Integrity Failures**, which covers unsigned/unverified update mechanisms. The SolarWinds SUNBURST attack follows this exact pattern.
- ❌ **A** — Misconfiguration (A02) would apply if the update mechanism was misconfigured (e.g., no TLS on the update URL), but the root cause here is the absence of integrity verification, not a configuration error.
- ❌ **B** — Broken Access Control (A01) relates to authorization failures, not integrity of downloaded artifacts.
- ❌ **C** — Authentication Failures (A07) cover identity verification flaws — not artifact integrity.

---

### Q13
**Which of the following statements about OWASP's methodology change between the 2017 and 2021 editions is correct?**

- A) OWASP switched from CWE-based analysis to CVE-based analysis in 2021
- B) OWASP added a practitioner survey for the first time in 2021
- C) ✅ OWASP shifted from measuring raw frequency to measuring incidence rate in 2021
- D) OWASP eliminated community survey data in 2021 to rely solely on tool-generated data

**Explanation:**
- ✅ **C is correct.** In 2021, OWASP changed the primary data metric from **frequency** (how many times a vulnerability appeared) to **incidence rate** (what percentage of tested applications had at least one instance). This made the data more meaningful — an app with 1000 SQLi instances counts the same as an app with 1.
- ❌ **A** — OWASP uses both CWE and CVE data; CWE mapping was a key part of the 2021 methodology but the shift was about frequency vs incidence, not CWE vs CVE.
- ❌ **B** — The practitioner survey was used prior to 2021 as well; it was not new in 2021, though its role was formalized.
- ❌ **D** — OWASP **retained** and valued community survey data in 2021 — it specifically allows up to 2 community-survey-driven categories to enter the list (SSRF entered via survey in 2021).

---

### Q14
**A developer stores user passwords using unsalted MD5 hashes. Which OWASP 2025 category is violated, and what is the recommended replacement hashing approach?**

- A) A07:2025 Authentication Failures — use bcrypt for password hashing
- B) ✅ A04:2025 Cryptographic Failures — use Argon2id (preferred), bcrypt, or scrypt
- C) A01:2025 Broken Access Control — use RBAC to protect the password database
- D) A05:2025 Injection — use parameterized queries to store passwords

**Explanation:**
- ✅ **B is correct.** Storing passwords as unsalted MD5 hashes is a **Cryptographic Failure (A04:2025)** — MD5 is broken, and without salting, rainbow table attacks trivially crack all passwords. The OWASP-recommended replacement is **Argon2id** (the current gold standard), followed by bcrypt or scrypt. These are adaptive Key Derivation Functions (KDFs) designed to be computationally expensive.
- ❌ **A** — Authentication Failures (A07) does reference weak password storage as a contributing factor, but the **root cause** is a cryptographic choice — MD5 is a broken algorithm. Bcrypt alone is also correct, but Argon2id is preferred. This option is partially correct but B is more precise and complete.
- ❌ **C** — RBAC protects access to data; it does not fix the hashing algorithm problem.
- ❌ **D** — Parameterized queries prevent SQL injection; they have nothing to do with how passwords are hashed.

---

### Q15
**The SolarWinds SUNBURST attack (2020) is the canonical real-world example for which OWASP Top 10 2025 category?**

- A) A07:2025 Authentication Failures
- B) A08:2025 Software or Data Integrity Failures
- C) ✅ A03:2025 Software Supply Chain Failures
- D) A02:2025 Security Misconfiguration

**Explanation:**
- ✅ **C is correct.** SolarWinds SUNBURST is the defining example of a **Software Supply Chain attack** — malicious code was injected into the **SolarWinds Orion build process** (not into SolarWinds' own infrastructure after deployment, but into the build/compilation stage). The resulting artifact was cryptographically signed with SolarWinds' legitimate certificate. This is why it maps to **A03:2025 Software Supply Chain Failures** — compromise of the build pipeline itself.
- ❌ **B — A08 Software or Data Integrity Failures** is tempting because the integrity of software was violated. However, A08 covers insecure deserialization and unsigned update mechanisms at the **application level**. SolarWinds was a supply chain / build process compromise — categorically A03.
- ❌ **A** — No authentication bypass was the attack vector.
- ❌ **D** — While misconfigurations may exist in any environment, the attack mechanism was supply chain compromise, not misconfiguration.

---

### Q16
**Which of the following best describes the concept of "fail secure" as it relates to A10:2025 Mishandling of Exceptional Conditions?**

- A) The system logs all errors to a secure remote SIEM before shutting down
- B) The system retries the failed operation using a backup authentication server
- C) ✅ The system defaults to a deny/restricted state when an error or exception occurs
- D) The system encrypts all error messages before sending them to the client

**Explanation:**
- ✅ **C is correct.** "Fail secure" (also called "fail safe" in some contexts) means the system defaults to **the most restrictive, deny state** when encountering an unexpected error. The opposite — **fail open** — is the vulnerability: if an exception is thrown during an authentication check and the code catches it by returning `true` (allow), an attacker can deliberately trigger the exception to bypass authentication.
- ❌ **A** — Logging to SIEM is a good practice for A09, not the definition of fail secure.
- ❌ **B** — Retrying with backup is a resilience/availability pattern (circuit breaker), not fail secure.
- ❌ **D** — Encrypting error messages to clients is a good practice but not what fail secure means; generic (not encrypted) error messages to clients is actually the right practice — detailed errors go only to logs.

---

### Q17
**In OWASP 2025, Broken Access Control (A01) maps to the highest number of CWEs of any single category. How many CWEs does it map to?**

- A) 20
- B) 28
- C) 35
- D) ✅ 40

**Explanation:**
- ✅ **D is correct.** A01:2025 Broken Access Control maps to **40 CWEs** — the largest CWE mapping of any single category in the 2025 edition. This reflects the extremely broad attack surface of access control — covering IDOR, path traversal, CSRF, SSRF, privilege escalation, and more.
- ❌ **A, B, C** — All incorrect numbers. 40 is the published figure for A01:2025.

---

### Q18
**A web application's JWT token is tampered by setting the `alg` header field to `none` — removing the signature. The server accepts the token. Which OWASP 2025 category does this attack fall under?**

- A) A04:2025 Cryptographic Failures
- B) A08:2025 Software or Data Integrity Failures
- C) ✅ A07:2025 Authentication Failures
- D) A01:2025 Broken Access Control

**Explanation:**
- ✅ **C is correct.** The JWT `alg:none` attack is classified under **A07:2025 Authentication Failures**. The server fails to enforce that tokens must be signed — accepting an unsigned (tampered) token allows identity spoofing and authentication bypass. This is a failure of the authentication mechanism.
- ❌ **A** — Cryptographic Failures (A04) could be argued (the server accepts no cryptography), but the OWASP classification puts JWT manipulation — including `alg:none`, algorithm confusion (RS256→HS256), and unsigned token acceptance — under Authentication Failures.
- ❌ **B** — A08 covers insecure deserialization and integrity of software artifacts/updates — not authentication token manipulation.
- ❌ **D** — A01 (Broken Access Control) would apply *after* authentication is bypassed — to what the attacker accesses — not to the bypass mechanism itself.

---

### Q19
**How many total CWEs were mapped across all 10 categories in the OWASP Top 10 2025, compared to 2021?**

- A) 2021: 175 mapped, 2025: 218 mapped
- B) 2021: 218 mapped, 2025: 300 mapped
- C) ✅ 2021: 218 mapped, 2025: 248 mapped
- D) 2021: 248 mapped, 2025: 589 mapped

**Explanation:**
- ✅ **C is correct.** OWASP Top 10 2021 mapped **218 CWEs** across all 10 categories. The 2025 edition increased this to **248 CWEs** — an increase of 30. The number of CWEs **analyzed** (not mapped) jumped to **589** in 2025 (from ~400 in 2021), and the dataset included **175,000+ CVE records**.
- ❌ **A** — 175 mapped is incorrect for 2021.
- ❌ **B** — 300 mapped is not the figure for 2025.
- ❌ **D** — 589 is the number of CWEs **analyzed** in 2025 — not mapped. 248 mapped in 2025 is correct, but 248 was not the 2021 figure.

---

### Q20
**Which of the following statements is TRUE about "Insecure Design" (A06:2025)?**

- A) It was introduced in the OWASP Top 10 2025 as a brand-new category
- B) It was at position A04 in 2017 and moved to A06 in 2021
- C) It covers implementation bugs that can be patched without architectural changes
- D) ✅ It was introduced in 2021 at A04, and moved to A06 in 2025

**Explanation:**
- ✅ **D is correct.** Insecure Design (A04:2021) was **new in 2021** — it had no equivalent in the 2017 list. In 2025, it moved down two positions to **A06:2025**. It was not new in 2025; it was new in 2021.
- ❌ **A** — This is the trap answer — Insecure Design is new to 2021, not to 2025. In 2025 it already existed and simply moved positions.
- ❌ **B** — Insecure Design did not exist in the 2017 list at any position.
- ❌ **C** — This directly contradicts the definition. Insecure Design specifically refers to flaws that **cannot be patched** — they require redesign.

---

### Q21
**An attacker sends a malformed HTTP request where the `Content-Length` header claims 65,535 bytes but the actual body is only 1 byte. The server reads 65,534 bytes of memory beyond the buffer to satisfy the claimed length. Which vulnerability type does this describe, and which CVE is it associated with?**

- A) SQL Injection — CVE-2017-5638
- B) Server-Side Request Forgery — CVE-2019-19781
- C) ✅ Buffer over-read (Heartbleed) — CVE-2014-0160
- D) Insecure Deserialization — CVE-2021-44228

**Explanation:**
- ✅ **C is correct.** This describes the **Heartbleed vulnerability (CVE-2014-0160)** in OpenSSL's TLS heartbeat extension. The handler read up to 64KB of server memory to fulfil a requested length without validating that the actual payload matched — a classic **buffer over-read / exceptional condition not handled**. Maps to **A10:2025 Mishandling of Exceptional Conditions** and **A04:2025 Cryptographic Failures** (the cryptographic library was compromised).
- ❌ **A** — CVE-2017-5638 is Apache Struts (Equifax breach) — a deserialization/injection vulnerability, not Heartbleed.
- ❌ **B** — CVE-2019-19781 is a Citrix path traversal RCE — not SSRF and not Heartbleed.
- ❌ **D** — CVE-2021-44228 is **Log4Shell** — JNDI injection via the logging library — not Heartbleed.

---

### Q22
**PCI DSS 4.0 explicitly references OWASP Top 10 coverage as acceptable evidence of secure coding practices. Under which PCI DSS 4.0 requirement does this reference appear?**

- A) Requirement 8.3.2
- B) Requirement 10.4.1
- C) Requirement 3.5.1
- D) ✅ Requirement 6.2.4

**Explanation:**
- ✅ **D is correct.** PCI DSS 4.0 **Requirement 6.2.4** covers software development practices and specifically references OWASP Top 10 (and SANS Top 25) as accepted frameworks for training and evidence of addressing common vulnerabilities in bespoke/custom software development.
- ❌ **A** — Requirement 8.3.2 relates to MFA configuration.
- ❌ **B** — Requirement 10.4.1 relates to log review processes.
- ❌ **C** — Requirement 3.5.1 relates to primary account number (PAN) protection.

---

### Q23
**Which OWASP Top 10 2017 category was removed without being merged into any existing 2021 category?**

- A) Insecure Deserialization
- B) ✅ Neither — all 2017 categories were either retained or merged; no category was simply deleted
- C) XML External Entities (XXE)
- D) Insufficient Logging and Monitoring

**Explanation:**
- ✅ **B is correct.** Every OWASP Top 10 2017 category was either retained (in some form or renamed), merged into another category, or its concepts absorbed. No category simply disappeared without its concepts being carried forward:
  - A7:2017 XSS → merged into A03:2021 Injection
  - A4:2017 XXE → merged into A05:2021 Security Misconfiguration
  - A8:2017 Insecure Deserialization → merged into A08:2021 Software & Data Integrity Failures
  - All others were retained and renamed/repositioned
- ❌ **A** — Insecure Deserialization was merged into A08:2021 — not deleted.
- ❌ **C** — XXE was merged into Security Misconfiguration — not deleted.
- ❌ **D** — Insufficient Logging was retained and renamed as A09:2021 — not deleted.

---

### Q24
**What distinguishes A03:2025 "Software Supply Chain Failures" from A09:2021 "Vulnerable and Outdated Components" — what was added to the scope?**

- A) The 2025 category specifically focuses on JavaScript npm packages only
- B) The 2025 category additionally covers runtime deserialization of third-party objects
- C) The 2025 category additionally covers server-side request forgery via third-party APIs
- D) ✅ The 2025 category expands scope to the entire build and delivery pipeline — including build tools, CI/CD steps, container base images, package signing, and dependency confusion attacks

**Explanation:**
- ✅ **D is correct.** A09:2021 focused narrowly on **using outdated or vulnerable components** (libraries, frameworks). A03:2025 expands this to the **entire software supply chain** — including build toolchain compromise (SolarWinds model), unsigned packages, CI/CD pipeline integrity, container base image tampering, dependency confusion, and typosquatting. SBOM (Software Bill of Materials) becomes a key countermeasure.
- ❌ **A** — The category is not limited to npm or JavaScript packages.
- ❌ **B** — Runtime deserialization is covered by A08 (Software or Data Integrity Failures), not A03.
- ❌ **C** — SSRF via third-party APIs would fall under A01 (Broken Access Control), not A03.

---

### Q25
**In OWASP Top 10 2025, the Injection category (A05) explicitly includes which vulnerability type that was a SEPARATE, standalone category in OWASP Top 10 2017?**

- A) XML External Entities (XXE)
- B) ✅ Cross-Site Scripting (XSS)
- C) Insecure Deserialization
- D) Server-Side Request Forgery (SSRF)

**Explanation:**
- ✅ **B is correct.** XSS was **A7:2017** as a standalone category. In 2021, it was merged into **A03:2021 Injection**, and this consolidation was retained in 2025 under **A05:2025 Injection**. XSS is classified as a form of injection — malicious script injected into output context, interpreted as code by the browser.
- ❌ **A** — XXE (A4:2017) was merged into **Security Misconfiguration** — not into Injection.
- ❌ **C** — Insecure Deserialization (A8:2017) was merged into **Software or Data Integrity Failures** — not into Injection.
- ❌ **D** — SSRF was **A10:2021** (new in 2021, not standalone in 2017) and was absorbed into **Broken Access Control** (A01:2025) — not into Injection.

---

### Q26
**What is the primary reason Injection (including SQLi) fell from #1 in 2017 to #5 in 2025 in the OWASP Top 10?**

- A) SQL Injection has been fully eliminated by the adoption of NoSQL databases
- B) OWASP removed XSS from the Injection category, reducing its weight
- C) Injection was determined to be less severe than previously thought
- D) ✅ Widespread adoption of ORMs and parameterized queries lowered the incidence rate across tested applications

**Explanation:**
- ✅ **D is correct.** The OWASP Top 10 is ranked by **incidence rate** (how many apps have the issue), not severity. SQLi and other injection flaws are still critically dangerous when present — but developer education, ORM adoption (Hibernate, SQLAlchemy), and parameterized query libraries have significantly reduced how many applications have injectable endpoints. Lower incidence rate = lower ranking.
- ❌ **A** — NoSQL databases have not eliminated injection — NoSQL injection is its own attack class, and SQLi still exists in the overwhelming majority of applications with relational databases.
- ❌ **B** — XSS was **added** to the Injection category in 2021 (merged), which should increase its weight, not reduce it.
- ❌ **C** — OWASP explicitly states Injection "has the greatest number of CVEs" — it is still considered a top-severity risk; the ranking drop is purely incidence-rate-driven.

---

### Q27
**An application's session token is not invalidated on the server side after the user clicks "Logout." The old token continues to work for 8 hours. An attacker who captured this token via XSS continues to use it. Which OWASP 2025 category is the PRIMARY classification for this server-side session management failure?**

- A) A04:2025 Cryptographic Failures
- B) A05:2025 Injection (because XSS was involved)
- C) A08:2025 Software or Data Integrity Failures
- D) ✅ A07:2025 Authentication Failures

**Explanation:**
- ✅ **D is correct.** Failure to invalidate session tokens after logout is explicitly listed as an **Authentication Failure (A07:2025)**. Session management is part of the authentication lifecycle — a token that survives logout is an authentication control failure. The XSS that captured the token is a separate A05 issue, but the question asks about the **server-side session management failure specifically**.
- ❌ **A** — Cryptographic Failures (A04) relate to encryption/hashing issues, not session invalidation logic.
- ❌ **B** — While XSS (A05) was the capture mechanism, the question targets the **session management failure** (non-invalidation), which is A07.
- ❌ **C** — A08 covers software/data integrity and deserialization — not session management.

---

### Q28
**OWASP was founded in which year, and when was the first OWASP Top 10 published?**

- A) Founded 1999 — Top 10 first published 2001
- B) Founded 2001 — Top 10 first published 2001
- C) Founded 2004 — Top 10 first published 2003
- D) ✅ Founded 2001 — Top 10 first published 2003

**Explanation:**
- ✅ **D is correct.** OWASP was founded by **Mark Curphey in 2001**. The OWASP Top 10 project was first published in **2003**. OWASP became a US **501(c)(3) non-profit in 2004**.
- ❌ **A** — 1999 is incorrect for founding year.
- ❌ **B** — Top 10 was not published in 2001 — that was the founding year. Top 10 came in 2003.
- ❌ **C** — 2004 is when OWASP became a registered non-profit, not when it was founded.

---

### Q29
**An attacker triggers a bug in a file download function: between the security check that verifies the user owns the file (check) and the actual file read operation (use), the attacker swaps the filename to point to `/etc/passwd`. This exploit is called:**

- A) Path traversal
- B) Insecure Direct Object Reference (IDOR)
- C) ✅ Time-of-Check Time-of-Use (TOCTOU) race condition
- D) Server-Side Request Forgery (SSRF)

**Explanation:**
- ✅ **C is correct.** This is a **TOCTOU (Time-of-Check Time-of-Use)** race condition — the attacker exploits the **time gap between the security check and the actual use of the checked value** by modifying the target resource in that window. This is a canonical example of **A10:2025 Mishandling of Exceptional Conditions** — the application fails to prevent an unusual timing condition from being exploited.
- ❌ **A** — Path traversal involves crafting a path like `../../../../etc/passwd` in the input — there's no race condition; the malicious path is in the request directly.
- ❌ **B** — IDOR involves accessing another user's resource by changing an object reference (ID, filename) in the request — no race condition timing element.
- ❌ **D** — SSRF involves the server making outbound requests on the attacker's behalf — no local file race condition.

---

### Q30
**Considering all three editions of the OWASP Top 10 (2017, 2021, 2025), which category has appeared in EVERY edition, maintained a top-5 position in ALL three editions, AND has been the #1 ranked category in at least two consecutive editions?**

- A) Cryptographic Failures / Sensitive Data Exposure
- B) Injection
- C) Security Misconfiguration
- D) ✅ Broken Access Control

**Explanation:**
- ✅ **D is correct.** Broken Access Control (A5:2017 → A01:2021 → A01:2025):
  - Present in all three editions ✅
  - Top-5 in all three editions (positions: #5, #1, #1) ✅
  - #1 in **two consecutive editions** (2021 and 2025) ✅
  - No other category matches all three criteria.
- ❌ **B — Injection**: Was #1 in 2017 but fell to #3 in 2021 and #5 in 2025. Top-5 in all three ✅, but #1 in only one edition (2017), not two consecutive.
- ❌ **A — Cryptographic Failures / Sensitive Data Exposure**: Was #3 in 2017, #2 in 2021, #4 in 2025 — top-5 in all three ✅, but never #1 in any edition ❌.
- ❌ **C — Security Misconfiguration**: Was #6 in 2017, #5 in 2021, #2 in 2025 — not top-5 in 2017 ❌ (#6 is outside top 5).

---

## Quick Answer Key

| Q | Answer | Category Tested |
|---|---|---|
| Q01 | C | Security Misconfiguration jumped #5→#2 |
| Q02 | D | SSRF absorbed into A01:2025 |
| Q03 | C | A09 "Monitoring"→"Alerting" rename |
| Q04 | D | A08 unchanged in name + position |
| Q05 | D | XSS merged into Injection (2021) |
| Q06 | B | SQLi → parameterized queries |
| Q07 | C | Heartland = SQLi breach |
| Q08 | C | Injection position: A1→A03→A05 |
| Q09 | C | Capital One = A01 + A02 |
| Q10 | D | Insecure Design = cannot be patched |
| Q11 | A | XXE merged into Security Misconfiguration |
| Q12 | D | Unsigned update = A08 integrity failure |
| Q13 | C | OWASP methodology: frequency→incidence rate |
| Q14 | B | MD5 passwords = A04 Cryptographic Failures |
| Q15 | C | SolarWinds = A03 Supply Chain |
| Q16 | C | Fail secure = deny on error |
| Q17 | D | A01:2025 maps to 40 CWEs |
| Q18 | C | JWT alg:none = A07 Authentication Failures |
| Q19 | C | 2021: 218 CWEs; 2025: 248 CWEs mapped |
| Q20 | D | Insecure Design new in 2021, moved to A06 in 2025 |
| Q21 | C | Heartbleed = CVE-2014-0160 |
| Q22 | D | PCI DSS 4.0 Req 6.2.4 |
| Q23 | B | All 2017 categories retained or merged |
| Q24 | D | A03:2025 = full supply chain scope |
| Q25 | B | XSS (A7:2017) merged into Injection |
| Q26 | D | Injection fell due to lower incidence rate |
| Q27 | D | Session not invalidated = A07 |
| Q28 | D | OWASP founded 2001; Top 10 first 2003 |
| Q29 | C | TOCTOU = A10:2025 |
| Q30 | D | Broken Access Control = only category matching all criteria |

---