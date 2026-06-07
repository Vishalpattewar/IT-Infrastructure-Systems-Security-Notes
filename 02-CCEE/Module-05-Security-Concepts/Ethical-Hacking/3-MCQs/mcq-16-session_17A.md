# MCQ Set — Session 17A: Hacking Web Servers · Web App Vulnerabilities · Web-Based Password Cracking 🌐

> 28 MCQs · 4 options each · Full explanations · Covers core + extra notes

---

## 📑 Table of Contents

- [Questions 01–06 — Web Server Attacks](#questions-0106--web-server-attacks)
- [Questions 07–13 — SQL Injection](#questions-0713--sql-injection)
- [Questions 14–19 — Web Application Vulnerabilities](#questions-1419--web-application-vulnerabilities)
- [Questions 20–24 — Web Password Cracking](#questions-2024--web-password-cracking)
- [Questions 25–28 — Extra Notes & Real-World](#questions-2528--extra-notes--real-world)
- [Answer Key](#answer-key)

---

## Questions 01–06 — Web Server Attacks

---

### Q01

**A web application accepts a filename parameter and includes the file in its response. An attacker submits the following value:**

    ../../../../etc/passwd

**Which attack is being performed, and what are the THREE alternative names for this attack?**

- A) Web cache poisoning — also called CDN injection, cache splitting, and response tampering
- B) HTTP response splitting — also called CRLF injection, header injection, and cache deception
- C) ✅ Directory traversal — also called path traversal, dot-dot-slash attack, and file path traversal
- D) Parameter tampering — also called HTTP parameter pollution, value injection, and form manipulation

**Explanation:**

- **A** is incorrect — web cache poisoning injects malicious content into a cache server using unkeyed request headers. It does not use `../` sequences in file path parameters.
- **B** is incorrect — HTTP response splitting injects CRLF characters (`\r\n`) into HTTP response headers to create fake responses. It targets headers — not file path parameters.
- **C** ✅ is correct — using `../` sequences to navigate above the intended web root directory is called **directory traversal**, **path traversal**, or **dot-dot-slash attack**. The sequence `../../../../etc/passwd` attempts to go four directory levels above the current location to reach the root filesystem and read `/etc/passwd` — the Unix user account list. All three names describe the same technique and may appear on exams interchangeably.
- **D** is incorrect — parameter tampering modifies HTTP parameter values (price, role, ID) to alter application logic. While both use user-controlled parameters, tampering changes VALUE semantics — traversal exploits PATH resolution.

---

### Q02

**An Apache web server responds to all HTTP requests with the following header:**

    Server: Apache/2.4.49 (Ubuntu)

**Why is this a security risk, and what is the correct Apache directive to mitigate it?**

- A) The header reveals the OS — attacker can socially engineer the Ubuntu community; fix with `ServerName Off`
- B) The header allows the attacker to count active connections — fix with `MaxClients 0`
- C) ✅ The exact version reveals which known CVEs apply — attacker looks up Apache 2.4.49 vulnerabilities (e.g., CVE-2021-41773) and directly exploits the specific version; fix with `ServerTokens Prod`
- D) The header enables session prediction — attacker uses version number as seed for session token generation; fix with `ServerSignature Off` only

**Explanation:**

- **A** is incorrect — while OS disclosure is also undesirable, the primary risk is version-specific CVE targeting. `ServerName` sets the server's hostname — not its version disclosure behaviour.
- **B** is incorrect — the `Server` header contains software identification — not connection count. `MaxClients` is a performance directive unrelated to version disclosure.
- **C** ✅ is correct — revealing the exact version (`Apache/2.4.49`) is called **banner grabbing** risk or **version disclosure**. An attacker immediately searches exploit databases (NVD, Exploit-DB) for that precise version. Apache 2.4.49 had **CVE-2021-41773** — a path traversal + RCE vulnerability (CVSS 9.8) actively exploited within hours of disclosure. The fix is **`ServerTokens Prod`** — which causes Apache to respond with only `Server: Apache` (no version number). Combined with `ServerSignature Off` to suppress version from error pages.
- **D** is incorrect — session token generation does not use the server version number as a seed. `ServerSignature Off` only removes the version from error page footers — not from response headers. Both directives are needed together.

---

### Q03

**An attacker sends the following HTTP request to a web server and receives a directory listing of files in response:**

    GET /uploads/ HTTP/1.1
    Host: example.com

**What misconfiguration caused this and what is the Apache directive to prevent it?**

- A) The server has PUT method enabled — disable with `LimitExcept GET POST`
- B) The server has TRACE method enabled — disable with `TraceEnable Off`
- C) The server is missing an SSL certificate — install TLS to encrypt directory contents
- D) ✅ Directory listing (Options Indexes) is enabled — the absence of an index file causes the server to display directory contents; fix with `Options -Indexes` in Apache configuration

**Explanation:**

- **A** is incorrect — the PUT method allows clients to upload files — it does not cause directory listing. Disabling PUT is a separate security hardening step.
- **B** is incorrect — the TRACE method echoes HTTP requests back to the client (Cross-Site Tracing risk). It does not cause directory listing behaviour.
- **C** is incorrect — TLS/SSL encrypts the transmission channel but has no effect on whether the server displays directory contents. An HTTPS server can still show directory listings.
- **D** ✅ is correct — when Apache has `Options +Indexes` (or `Options Indexes`) configured and no `index.html`/`index.php` exists in a directory, the server generates an automatic HTML listing of all files and subdirectories. This exposes files that should not be publicly visible (backups, configuration files, uploaded documents). The fix is `Options -Indexes` in `httpd.conf` or `.htaccess` — the `-` sign explicitly disables the index feature. For Nginx: `autoindex off;`.

---

### Q04

**An attacker injects the following string into a URL redirect parameter:**

    https://example.com/redirect?url=https://trusted.com%0d%0aSet-Cookie:%20session=attacker_value

**What attack is this, what do `%0d` and `%0a` represent, and what is the primary consequence?**

- A) SQL injection — `%0d%0a` are SQL comment characters; consequence is database manipulation
- B) Directory traversal — `%0d%0a` are path separator encodings; consequence is file system access
- C) XSS — `%0d%0a` are JavaScript comment characters; consequence is script injection
- D) ✅ HTTP response splitting (CRLF injection) — `%0d` is carriage return `\r` and `%0a` is line feed `\n`; consequence includes injecting headers like Set-Cookie to perform session fixation or cache poisoning

**Explanation:**

- **A** is incorrect — SQL comment characters in MySQL are `--` or `/* */`. CRLF sequences have no special meaning in SQL queries. The attack targets HTTP headers — not database queries.
- **B** is incorrect — path separators are `/` and `\` (URL-encoded as `%2f` and `%5c`). CRLF sequences are line terminators — they have no role in filesystem path resolution.
- **C** is incorrect — JavaScript comment characters are `//` and `/* */`. CRLF sequences are not JavaScript-related. The injected content appears in HTTP response headers — not in a script execution context.
- **D** ✅ is correct — **HTTP Response Splitting** (also called CRLF injection) injects carriage return (`%0d` = `\r`) and line feed (`%0a` = `\n`) characters into HTTP response headers. HTTP headers are terminated by CRLF sequences — injecting them allows the attacker to terminate an existing header and add new ones. Consequences: injecting `Set-Cookie` headers (session fixation), splitting the response into two (cache poisoning with malicious second response), or injecting arbitrary headers. Countermeasure: sanitize `%0d` and `%0a` from all values included in HTTP response headers.

---

### Q05

**A web server has the HTTP TRACE method enabled. An attacker combines this with an XSS vulnerability on the same site. What attack is made possible and what security boundary does it bypass?**

- A) SQL injection amplification — TRACE allows the attacker to reflect SQL payloads through the server
- B) Directory traversal bypass — TRACE reveals the web root path enabling more precise traversal
- C) DNS cache poisoning — TRACE responses are cached by DNS resolvers as fake resource records
- D) ✅ Cross-Site Tracing (XST) — TRACE echoes the full request including HttpOnly cookies in the response body — XSS uses XMLHttpRequest to send a TRACE request — the response reveals HttpOnly cookies that JavaScript cannot read via document.cookie

**Explanation:**

- **A** is incorrect — TRACE has no relationship to SQL injection. It is a diagnostic method that echoes the request — it does not amplify or process SQL queries.
- **B** is incorrect — TRACE does not reveal filesystem paths. It echoes the HTTP request as received — containing HTTP headers and the original URL — not the filesystem structure.
- **C** is incorrect — DNS resolvers cache DNS records — not HTTP TRACE responses. DNS and HTTP operate at different layers with different caching mechanisms.
- **D** ✅ is correct — **Cross-Site Tracing (XST)** is a technique that bypasses the `HttpOnly` cookie protection. Normally, `document.cookie` cannot read HttpOnly cookies. However, the HTTP TRACE method echoes the FULL request back — including ALL cookies (including HttpOnly ones) in the response body. An attacker with XSS can use `XMLHttpRequest` to send a TRACE request to the server — the response body contains the HttpOnly session cookie — which the script can then read and exfiltrate. Fix: `TraceEnable Off` (Apache) or equivalent in Nginx/IIS.

---

### Q06

**Which of the following CORRECTLY describes the security risk of a `robots.txt` file containing the following content:**

    User-agent: *
    Disallow: /admin/
    Disallow: /backup/
    Disallow: /config/

- A) The robots.txt file prevents search engines from indexing sensitive directories — eliminating the risk entirely
- B) The robots.txt file is encrypted — attackers cannot read it without the private key
- C) The robots.txt file only affects robots — human attackers are automatically redirected away from disallowed paths
- D) ✅ The robots.txt file advertises sensitive directories to attackers — while it instructs crawlers not to index them, it does not block access — attackers read robots.txt specifically to identify unprotected high-value paths

**Explanation:**

- **A** is incorrect — `robots.txt` is a **convention** — it instructs compliant web crawlers (Googlebot, Bingbot) not to index listed paths. It provides ZERO technical access restriction. A web browser or tool can access `/admin/` directly — robots.txt does not prevent this.
- **B** is incorrect — `robots.txt` is a plaintext file served publicly over HTTP. Any person or tool accessing `https://example.com/robots.txt` reads it in full. There is no encryption.
- **C** is incorrect — `robots.txt` has no mechanism to redirect or block human users or attacker tools. `Disallow` is a directive to cooperative robots — not an access control mechanism.
- **D** ✅ is correct — attackers routinely check `robots.txt` as one of the first steps in web application reconnaissance — specifically because it maps out directories the site owner considers sensitive enough to hide from search engines. Finding `/backup/` and `/config/` in Disallow entries immediately tells the attacker where to look for database backups or configuration files containing credentials. The correct approach: do not list sensitive paths in robots.txt — instead enforce access control on those directories directly.

---

## Questions 07–13 — SQL Injection

---

### Q07

**A login form processes credentials with the following PHP code:**

    $query = "SELECT * FROM users WHERE username='" . $_POST['username'] . "' AND password='" . $_POST['password'] . "'";

**An attacker enters `admin'--` as the username and anything as the password. What does the resulting SQL query look like and what is the outcome?**

- A) `SELECT * FROM users WHERE username='admin'--' AND password='anything'` → syntax error — attack fails
- B) `SELECT * FROM users WHERE username='' AND password='admin'--'` → password field bypassed — partial access
- C) ✅ `SELECT * FROM users WHERE username='admin'--' AND password='anything'` → `--` comments out the password check → query returns admin user → authentication completely bypassed
- D) `SELECT * FROM users WHERE username='admin' AND password=''--'` → both fields empty → all users returned

**Explanation:**

- **A** is incorrect — this option correctly identifies the resulting query but incorrectly states it causes a syntax error. In SQL, `--` is a valid single-line comment delimiter (MySQL, MSSQL, PostgreSQL). Everything after `--` is ignored — the query is syntactically valid and executes successfully.
- **B** is incorrect — the injection is in the USERNAME field. `admin'--` closes the username string after `admin` and comments out the rest. The password field is in the commented-out portion — not processed.
- **C** ✅ is correct — when `admin'--` is injected as the username: the resulting query is `SELECT * FROM users WHERE username='admin'--' AND password='anything'`. The `--` starts a SQL comment — everything after it (` AND password='anything'`) is ignored by the database engine. The effective query is simply `SELECT * FROM users WHERE username='admin'` — which returns the admin user record without any password validation. The application receives a valid result → grants access as admin.
- **D** is incorrect — the structure of the injection does not produce an empty password comparison. The `--` comment operator removes everything after it — not just the password value.

---

### Q08

**An attacker is testing a web application for SQL injection. They submit the following payloads and observe:**

    Payload 1: ' AND 1=1 --    →  Normal page content returned
    Payload 2: ' AND 1=2 --    →  Empty page / different content

**Which SQL injection type does this confirm and why?**

- A) Union-based SQL injection — the UNION keyword combines the results of both conditions
- B) Error-based SQL injection — the different responses indicate database error messages are being returned
- C) Time-based blind SQL injection — the response delay indicates the SLEEP function executed
- D) ✅ Boolean-based blind SQL injection — no data is visible in output — but the application returns different responses for true (1=1) and false (1=2) conditions — confirming injected SQL affects query logic

**Explanation:**

- **A** is incorrect — Union-based injection uses the `UNION SELECT` statement to append additional query results to the original. The payloads shown (`AND 1=1`, `AND 1=2`) are boolean condition tests — not UNION statements. Union-based injection produces extra data in the response — not just a different/empty page.
- **B** is incorrect — error-based injection produces actual database error messages in the response (table names, column names, version strings in error text). The scenario describes different content/empty page — not error messages. No error text is mentioned.
- **C** is incorrect — time-based blind injection uses `SLEEP()` or `WAITFOR DELAY` — the indicator is response TIME delay, not content difference. The payloads shown have no sleep function.
- **D** ✅ is correct — **Boolean-based blind SQL injection** is confirmed when: (1) the application returns different responses for true vs false injected conditions, AND (2) no actual data from the database is visible in the output. `AND 1=1` is always TRUE — normal response. `AND 1=2` is always FALSE — different/empty response. This proves the injected SQL is being processed and affects the query. The attacker can now extract data one bit at a time by replacing `1=1` with conditions like `SUBSTRING(username,1,1)='a'`.

---

### Q09

**A penetration tester confirms SQL injection in a parameter and wants to extract the contents of the `users` table without any visible error messages or direct output. The database is MySQL. Which payload technique would they use to extract data column by column?**

- A) `' DROP TABLE users --` — deletes the users table to confirm write access
- B) `' INSERT INTO users VALUES('hacker','hacked') --` — adds a test record
- C) `'; EXEC xp_cmdshell('whoami') --` — executes an OS command via SQL Server
- D) ✅ `' UNION SELECT username, password FROM users --` — appends a second SELECT statement whose results are returned alongside the original query's results

**Explanation:**

- **A** is incorrect — `DROP TABLE` would destroy the data — not extract it. This is destructive and would immediately be detected. Also, the web application's database user typically has SELECT privilege — not DROP privilege (if least privilege is implemented).
- **B** is incorrect — `INSERT` adds a record — it does not extract existing data. This might be used to test write access but is not a data extraction technique.
- **C** is incorrect — `xp_cmdshell` is a **Microsoft SQL Server** stored procedure for OS command execution. The question specifies **MySQL** — which does not have `xp_cmdshell`. Also, EXEC syntax differs between database engines.
- **D** ✅ is correct — **UNION-based SQL injection** appends a second `SELECT` statement using the `UNION` keyword. The results of both SELECT statements are returned together in the HTTP response. Prerequisites: the injected UNION SELECT must have the same number of columns as the original query, and data types must be compatible. The attacker first determines column count (via `ORDER BY` testing), then injects `UNION SELECT username, password FROM users --` to retrieve credential data alongside the intended query results.

---

### Q10

**An application does not display any query results or error messages. A tester injects:**

    '; IF (1=1) WAITFOR DELAY '0:0:5' --

**The response arrives 5 seconds later than normal. Then they inject:**

    '; IF (1=2) WAITFOR DELAY '0:0:5' --

**The response arrives immediately. What SQL injection type is confirmed and which database is likely in use?**

- A) Boolean-based blind SQLi — confirmed by different page content; database is MySQL
- B) Error-based SQLi — the delay is caused by a database error being generated; database is PostgreSQL
- C) Union-based SQLi — WAITFOR combines results from two queries; database is Oracle
- D) ✅ Time-based blind SQL injection — conditional delay confirms injected SQL executes; `WAITFOR DELAY` is Microsoft SQL Server syntax — MSSQL is confirmed

**Explanation:**

- **A** is incorrect — boolean-based blind uses DIFFERENT PAGE CONTENT to indicate true/false — not response timing. Also, `WAITFOR DELAY` is MSSQL-specific — not MySQL. MySQL uses `SLEEP(5)`.
- **B** is incorrect — error-based injection produces error messages in the response content — not timing differences. The scenario describes timing as the indicator — no errors are mentioned.
- **C** is incorrect — `WAITFOR DELAY` is not a UNION operation — it is a time delay function. Oracle uses `dbms_pipe.receive_message` or `EXECUTE IMMEDIATE 'begin dbms_lock.sleep(5); end;'` for time-based injection.
- **D** ✅ is correct — **Time-based blind SQL injection** uses the database's sleep/delay function to confirm injection when there is NO visible output difference. `IF (1=1) WAITFOR DELAY '0:0:5'` → condition is TRUE → 5-second delay → confirmed. `IF (1=2) WAITFOR DELAY '0:0:5'` → condition is FALSE → no delay → confirmed conditional execution. **`WAITFOR DELAY`** is specific to **Microsoft SQL Server (MSSQL)**. MySQL equivalent: `SLEEP(5)`. PostgreSQL: `pg_sleep(5)`. The database engine is identified by the sleep function syntax.

---

### Q11

**A developer argues that their application is safe from SQL injection because it uses a Web Application Firewall (WAF) that filters all SQL keywords. An attacker bypasses the WAF using:**

    SeLeCt%09username,password%09FrOm%09users--

**What TWO WAF bypass techniques are used here?**

- A) URL encoding of SQL keywords + Unicode substitution of table names
- B) Double URL encoding + null byte injection
- C) ✅ Case variation (`SeLeCt` instead of `SELECT`) + whitespace substitution (tab `%09` instead of space) — SQL keywords are case-insensitive and tabs are valid whitespace in SQL syntax
- D) Base64 encoding + comment-based obfuscation

**Explanation:**

- **A** is incorrect — URL encoding of SQL keywords (e.g., `%53%45%4c%45%43%54` for SELECT) is a valid technique but is not what is shown. The keywords are in mixed case — not URL-encoded. Unicode substitution of table names is a different technique.
- **B** is incorrect — double URL encoding would show `%25XX` patterns (encoding the `%` sign itself). The payload shows `%09` which is single URL encoding of a tab character. Null byte injection would be `%00` — not present here.
- **C** ✅ is correct — two bypass techniques: **(1) Case variation** — SQL keywords are case-insensitive in all major database engines (`SeLeCt` = `SELECT`). Simple WAF rules matching exact case patterns like `SELECT` miss `SeLeCt`. **(2) Whitespace substitution** — `%09` is the URL-encoded horizontal tab character. SQL parsers accept tabs, newlines, and carriage returns as whitespace between keywords. WAFs filtering on `SELECT username` (space between keywords) miss `SeLeCt%09username` (tab between keywords).
- **D** is incorrect — Base64 encoding would produce `U0VMRUNUdXNlcm5hbWUscGFzc3dvcmQgRlJPTSB1c2Vycw==` — not the pattern shown. Comment-based obfuscation uses `/*comment*/` — not present in this payload.

---

### Q12

**What is the ONLY complete technical solution to prevent SQL injection, and why do all other mitigations fall short as standalone defences?**

- A) Input validation — reject any input containing SQL characters; other methods are insufficient because they don't inspect user input
- B) Web Application Firewall — filters known SQL patterns; other methods don't inspect traffic at the network level
- C) Stored procedures — all SQL is pre-compiled; other methods don't pre-compile queries
- D) ✅ Parameterized queries (prepared statements) — user data is always treated as a value, never as SQL syntax — making injection structurally impossible; input validation and WAFs can be bypassed with novel syntax; stored procedures are parameterized by nature but can still be vulnerable if built with concatenation internally

**Explanation:**

- **A** is incorrect — input validation (blacklisting SQL characters like `'`, `--`, `;`) can be bypassed with encoding (`%27` for `'`), alternative syntax, or injection via fields that don't appear suspicious. Attackers continuously discover new ways to inject without triggering blacklists. Validation is a useful secondary control — not a primary fix.
- **B** is incorrect — WAFs filter based on KNOWN signatures. Novel injection payloads, obfuscated syntax, encoding variations, or HTTP parameter pollution can bypass WAF rules. WAFs are a defence-in-depth layer — not a substitute for fixing the underlying code.
- **C** is partially correct — stored procedures are typically safer because SQL is pre-compiled and parameters are passed separately. However, if a stored procedure INTERNALLY concatenates parameters into a dynamic SQL string (`EXEC('SELECT * FROM users WHERE id=' + @id)`), it remains vulnerable. Stored procedures are not inherently safe — it depends on implementation.
- **D** ✅ is correct — **parameterized queries (prepared statements)** separate the SQL STRUCTURE from the DATA. The SQL command template is compiled first: `SELECT * FROM users WHERE username = ?`. The `?` placeholder tells the database this position is a DATA value — not SQL syntax. User input is then bound as data: `stmt.bind(username)`. Even if the user enters `admin'--`, the database treats the ENTIRE string as a literal username value — the `'` and `--` have no SQL meaning. Injection is architecturally impossible — not just filtered.

---

### Q13

**Which sqlmap command correctly performs SQL injection detection on a URL parameter AND attempts to enumerate all databases?**

- A) `sqlmap -u "https://example.com/product?id=1" --tables --current-db`
- B) `sqlmap -u "https://example.com/product?id=1" --passwords --dump-all`
- C) `sqlmap --host example.com --port 3306 --dbs --enumerate`
- D) ✅ `sqlmap -u "https://example.com/product?id=1" --dbs`

**Explanation:**

- **A** is incorrect — `--tables` lists tables within a specific database (requires `-D database_name`), and `--current-db` retrieves only the name of the current database. This combination does not enumerate ALL databases. It performs limited enumeration within the current database context.
- **B** is incorrect — `--passwords` attempts to retrieve password hashes from database user tables (not application user tables). `--dump-all` dumps all data from all tables — this goes beyond database enumeration and is an aggressive, noisy option that should not be the first step.
- **C** is incorrect — `sqlmap` does not use `--host` and `--port` for web application testing (those are for direct database connection mode). Web application testing uses `-u` with the full URL. `--enumerate` is not a valid sqlmap option.
- **D** ✅ is correct — `sqlmap -u "https://example.com/product?id=1" --dbs` is the correct syntax for: detecting SQL injection in the `id` parameter of the given URL (`-u`), then enumerating all accessible databases (`--dbs`). This is the standard first enumeration step after confirming injection. Follow-up commands: `-D dbname --tables` (list tables), `-D dbname -T users --dump` (dump specific table contents).

---

## Questions 14–19 — Web Application Vulnerabilities

---

### Q14

**In the OWASP Top 10 2021, which category moved to position A01 (the most critical), what was its ranking in the 2017 list, and what is the primary vulnerability type within this category?**

- A) Injection moved from A2 to A01 — primary vulnerability: SQL injection
- B) Cryptographic Failures moved from A6 to A01 — primary vulnerability: cleartext transmission
- C) Broken Authentication moved from A1 to A01 — primary vulnerability: password reuse
- D) ✅ Broken Access Control moved from A5 to A01 — primary vulnerability: IDOR (Insecure Direct Object Reference) and path traversal — found in 94% of tested applications

**Explanation:**

- **A** is incorrect — Injection was A1 in the 2017 OWASP Top 10. In 2021, it moved DOWN to A03 (not up to A01). SQL injection is now grouped within the broader Injection category at position 3.
- **B** is incorrect — Sensitive Data Exposure (renamed Cryptographic Failures in 2021) was A3 in 2017 and moved to A02 in 2021 — not A01.
- **C** is incorrect — Broken Authentication was A2 in 2017 and moved to A07 (renamed Identification and Authentication Failures) in 2021. It moved DOWN significantly, not to A01.
- **D** ✅ is correct — **Broken Access Control** was A5 in the OWASP Top 10 2017 and moved to **A01 in 2021** — reflecting that it is now found in 94% of tested applications (the most widespread vulnerability class). The primary sub-vulnerabilities are **IDOR** (accessing other users' objects by changing identifiers) and **path traversal** (escaping intended directory scope). Both represent failures to enforce proper authorization on individual objects/resources — as distinct from authentication (proving identity).

---

### Q15

**An e-commerce application displays order details at:**

    GET /api/orders/10042

**A logged-in customer changes the order ID to 10043 and receives another customer's complete order details including name, address, and payment method. Which vulnerability is this and what is the PRECISE server-side fix?**

- A) SQL injection — fix by using parameterized queries when fetching order records
- B) Session hijacking — fix by regenerating session token on every request
- C) Parameter tampering — fix by encrypting order ID values before sending to client
- D) ✅ Insecure Direct Object Reference (IDOR) — fix by adding a server-side authorization check confirming the requesting user owns the requested order before returning it

**Explanation:**

- **A** is incorrect — SQL injection involves manipulating SQL query structure through malicious input. Changing `10042` to `10043` in the URL is a numeric substitution — not SQL syntax injection. The query `SELECT * FROM orders WHERE id=10043` is valid SQL — the problem is missing authorization, not injection.
- **B** is incorrect — session hijacking steals another user's session token. The attacker here is using THEIR OWN valid session — they are authenticated — but accessing data that belongs to a different user. The session is not compromised — the authorization is.
- **C** is incorrect — encrypting the order ID would make it harder to guess other values but is security through obscurity — not a true fix. An attacker could still enumerate if they obtain any valid encrypted IDs. Also, the vulnerability is missing authorization — not predictable IDs.
- **D** ✅ is correct — this is a textbook **IDOR** vulnerability. The application authenticates the user but fails to check whether the authenticated user is AUTHORIZED to access the specific object being requested. The correct fix is a server-side authorization check on every request: `if (order.customer_id != current_user.id) { return HTTP 403 Forbidden; }`. Using random UUIDs instead of sequential integers makes guessing harder but is NOT a substitute for authorization — it must be combined with proper access control.

---

### Q16

**A web application receives user input in an XML document and processes it with an XML parser. An attacker submits:**

    <?xml version="1.0"?>
    <!DOCTYPE foo [
      <!ENTITY xxe SYSTEM "file:///etc/shadow">
    ]>
    <user><name>&xxe;</name></user>

**What vulnerability is this, what does it expose, and what is the fix?**

- A) SQL injection via XML — the DOCTYPE declaration contains SQL syntax; fix with parameterized queries
- B) XSS via XML — the entity expands to JavaScript that executes in the browser; fix with output encoding
- C) CSRF via XML — the DOCTYPE tricks the browser into sending cross-site requests; fix with CSRF tokens
- D) ✅ XML External Entity (XXE) injection — the external entity `xxe` references `/etc/shadow` — the XML parser resolves and includes its contents in the response; fix by disabling external entity processing in the XML parser

**Explanation:**

- **A** is incorrect — this is not SQL injection. The payload contains XML-specific syntax (`<!DOCTYPE>`, `<!ENTITY>`). SQL injection targets database queries — not XML parsers. The fix for SQL injection (parameterized queries) has no relevance to XML processing.
- **B** is incorrect — XXE does not inject JavaScript into browser execution. The entity `&xxe;` is resolved SERVER-SIDE by the XML parser — it reads the specified file and includes its content in the parsed XML. No browser execution is involved.
- **C** is incorrect — CSRF forces the victim's browser to make cross-site requests. XXE is a server-side vulnerability where the SERVER'S XML parser reads local files. No cross-site request or browser interaction is involved.
- **D** ✅ is correct — **XXE (XML External Entity) injection** exploits XML parsers that allow external entity declarations. `<!ENTITY xxe SYSTEM "file:///etc/shadow">` defines an entity that references a local file. `&xxe;` instructs the parser to replace itself with the file's contents. The parser reads `/etc/shadow` (Linux hashed password file — root-readable only, but if the web process runs as root or shadow group member...) and includes it in the response. Fix: disable external entity processing in the XML library configuration (e.g., in PHP: `libxml_disable_entity_loader(true)`; in Java: `factory.setFeature("http://apache.org/xml/features/disallow-doctype-decl", true)`).

---

### Q17

**A web application passes user input from a network diagnostic tool to the OS:**

    $output = shell_exec("ping -c 4 " . $_GET['host']);

**An attacker submits `host=8.8.8.8%3B%20cat%20%2Fetc%2Fpasswd`. After URL decoding, this becomes `8.8.8.8; cat /etc/passwd`. What attack is this, what does the `;` character do, and how should the code be fixed?**

- A) SQL injection — `;` terminates a SQL statement; fix with parameterized queries
- B) XSS injection — `;` separates JavaScript statements; fix with output encoding
- C) Directory traversal — `;` separates path components; fix with path canonicalization
- D) ✅ OS command injection — `;` is a shell command separator that runs a second command regardless of the first's success; fix by never passing user input to shell functions — use a native PHP network library instead

**Explanation:**

- **A** is incorrect — `;` terminates SQL statements in some contexts but this code uses `shell_exec()` — an OS shell function, not a database query. SQL injection targets database engines — not OS shells.
- **B** is incorrect — `;` does separate JavaScript statements but this input is processed by `shell_exec()` on the SERVER — it never reaches the browser's JavaScript engine. XSS requires output that is reflected to a victim's browser.
- **C** is incorrect — `;` has no special meaning in filesystem path resolution. Directory traversal uses `../` sequences. The vulnerability here is in OS command execution — not file path handling.
- **D** ✅ is correct — **OS command injection** (also called shell injection). The `;` character is a shell command separator — it tells the shell: "execute the first command, then execute the second regardless of the first's result." The resulting shell command is: `ping -c 4 8.8.8.8; cat /etc/passwd`. Ping runs normally, then `cat /etc/passwd` executes and its output is returned. The fix: **never pass user input to shell execution functions** (`shell_exec`, `system`, `exec`, `popen`). Use native PHP functions instead: `socket_create()`, `curl`, or pre-validated IP addresses with strict whitelist validation (only allow `[0-9.]` characters matching an IP pattern).

---

### Q18

**A web application allows file uploads for profile pictures and only validates the file extension. An attacker uploads a file named `shell.php` but renames it to `shell.jpg` before submitting. The server stores it as `shell.jpg`. The attacker then accesses `https://example.com/uploads/shell.jpg` and achieves remote code execution. What two failures allowed this?**

- A) Missing HTTPS + missing Content-Security-Policy — the file should only be served over encrypted connections
- B) SQL injection in the filename field + missing antivirus scanning
- C) ✅ Extension-only validation (missed PHP content inside a .jpg file) + the upload directory has PHP execution permissions enabled — both failures combined allow the malicious file to execute as PHP despite the .jpg extension
- D) Missing CSRF token on the upload form + session fixation in the file storage path

**Explanation:**

- **A** is incorrect — HTTPS encrypts transmission but does not validate file content or prevent execution of uploaded files. CSP restricts what scripts browsers execute — it does not affect server-side file execution.
- **B** is incorrect — the scenario describes extension renaming — not SQL injection through the filename. Antivirus would be a useful control but is not one of the two PRIMARY failures described.
- **C** ✅ is correct — two failures: **(1) Extension-only validation** — checking only that the filename ends in `.jpg` without inspecting the file's actual content (magic bytes, MIME type, or file structure). PHP content inside a `.jpg`-named file passes the extension check. **(2) PHP execution enabled in the upload directory** — if the web server is configured to execute PHP files in the `uploads/` directory, accessing `shell.jpg` may trigger PHP execution (depending on Apache configuration — `AddType application/x-httpd-php .jpg`). Proper fix: validate by MAGIC BYTES (first bytes of file identifying its true type), store uploads OUTSIDE the web root, rename files randomly, and ensure upload directories have `php_admin_flag engine Off` (no PHP execution).
- **D** is incorrect — CSRF tokens protect against unauthorized form submissions from other sites — not against malicious file content uploaded by the attacker themselves. Session fixation is unrelated to file upload vulnerabilities.

---

### Q19

**An online shopping cart sends the following POST request at checkout:**

    POST /checkout HTTP/1.1
    Content-Type: application/x-www-form-urlencoded

    product_id=789&quantity=2&unit_price=49.99&total=99.98

**An attacker intercepts this with Burp Suite and modifies it to:**

    product_id=789&quantity=2&unit_price=0.01&total=0.02

**The order is processed at £0.02. Which vulnerability is this, which OWASP 2021 category does it fall under, and what is the correct fix?**

- A) SQL injection (OWASP A03) — the price value contains SQL syntax; fix with parameterized queries
- B) XSS (OWASP A03) — the modified price injects a script into the order confirmation; fix with CSP
- C) Broken Authentication (OWASP A07) — the attacker bypassed the pricing authentication; fix with MFA
- D) ✅ Parameter tampering / Broken Access Control (OWASP A01) — the server trusted client-submitted price values instead of recalculating server-side; fix by ignoring all client-sent pricing and computing total from server-side product catalog

**Explanation:**

- **A** is incorrect — the attacker changed `49.99` to `0.01` — a numeric substitution. No SQL syntax was injected. The server processed a legitimate-looking checkout request — the database query for this price was valid.
- **B** is incorrect — the modified price is a numeric value affecting the order total. It does not inject JavaScript into any response. XSS requires script code in output displayed to a victim's browser.
- **C** is incorrect — authentication was not bypassed. The attacker was legitimately authenticated (they had a valid session to reach checkout). The vulnerability is in WHAT the server trusts from the authenticated client — not in whether the client authenticated.
- **D** ✅ is correct — **parameter tampering** — the server trusted `unit_price` and `total` values submitted by the client in the HTTP request. The fundamental rule violated: **never trust client-side data for security-sensitive values**. Prices, discounts, and totals MUST be calculated server-side from the authoritative product database: `total = quantity × lookup_price(product_id)`. This falls under **OWASP A01 — Broken Access Control** (server fails to enforce business logic controls — client can manipulate values it should not control).

---

## Questions 20–24 — Web Password Cracking

---

### Q20

**What is the PRECISE technical reason why password spraying evades standard per-account lockout policies — and which account lockout counter does it specifically avoid incrementing above the threshold?**

- A) Password spraying uses encrypted connections — lockout policies only count plaintext login attempts
- B) Password spraying uses valid session tokens — lockout counters only increment for unauthenticated requests
- C) Password spraying rotates source IP addresses — lockout policies only track attempts from single IPs
- D) ✅ Password spraying submits ONE password per account — the per-account failed attempt counter never exceeds the lockout threshold (e.g., 5 attempts) because each account only sees a single failure before the attacker moves to the next account

**Explanation:**

- **A** is incorrect — lockout policies count failed authentication attempts regardless of whether the connection uses TLS. The encryption of the transport layer has no effect on server-side attempt counting.
- **B** is incorrect — failed login attempts are counted BECAUSE the session token is invalid or not yet issued. Lockout counters operate at the pre-authentication stage — they specifically track failed credential submissions.
- **C** is incorrect — while password spraying often distributes across IPs (using residential proxies) to evade IP-based rate limiting, the SPECIFIC reason it evades ACCOUNT LOCKOUT (per-account) is about attempt COUNT per account — not source IP. IP rotation is a separate evasion technique for IP-based controls.
- **D** ✅ is correct — standard account lockout (e.g., "lock after 5 failed attempts") counts FAILED ATTEMPTS PER ACCOUNT. Password spraying tests only ONE password against each account before moving to the next. Account 1: try `Summer2024!` → fail (count: 1/5) → move on. Account 2: try `Summer2024!` → fail (count: 1/5) → move on. No individual account ever reaches the lockout threshold of 5. After cycling through all accounts, the attacker starts again with a new common password — still only incrementing each account's counter by 1 per cycle.

---

### Q21

**What is credential stuffing and why does it achieve significantly higher success rates than traditional brute force or dictionary attacks against web applications?**

- A) Credential stuffing uses faster hardware — GPU acceleration makes it 1000× faster than CPU-based brute force
- B) Credential stuffing uses rainbow tables — pre-computed hash chains make online cracking faster
- C) Credential stuffing bypasses HTTPS — it works at the network layer before TLS decryption
- D) ✅ Credential stuffing uses REAL username/password pairs from previous data breaches — these are actual passwords users chose, achieving 0.1–2% success rates because many users reuse the same password across multiple services

**Explanation:**

- **A** is incorrect — credential stuffing is an ONLINE attack — submitting credentials to a live web application. GPU acceleration is used for OFFLINE hash cracking (not for online HTTP requests, which are rate-limited by network latency and server response time). Hardware speed does not significantly help online attacks.
- **B** is incorrect — rainbow tables are used for OFFLINE hash cracking (comparing a stolen hash against pre-computed hash chains). Credential stuffing submits plaintext username/password pairs to live web application login forms — no hashing or pre-computation is involved.
- **C** is incorrect — credential stuffing is an application-layer attack. It makes normal HTTPS login requests to the web application — TLS is used correctly (the attacker sees only their own traffic). It does not bypass or break HTTPS.
- **D** ✅ is correct — credential stuffing's effectiveness comes from using **REAL stolen credentials**. When `user@email.com:Password123!` was the actual password on BreachedSite.com, there is a meaningful probability it is ALSO the password on BankSite.com (due to password reuse). Research consistently shows 0.1–2% of breach credential pairs work on other services — far higher than random guessing. With 2.7 billion credential pairs from "Collection #1", a 0.1% success rate yields 2.7 million valid account accesses on target services.

---

### Q22

**An attacker uses Hydra to perform a brute force attack against a web application login form at `https://example.com/login`. The login form sends POST requests with `username` and `password` fields, and displays "Invalid credentials" on failure. Which Hydra command correctly configures this attack?**

- A) `hydra -l admin -P rockyou.txt https://example.com ssh`
- B) `hydra -L users.txt -P pass.txt https://example.com http-get /login`
- C) `hydra -l admin -P rockyou.txt example.com http-get-form "/login:user=^USER^&pass=^PASS^:F=Invalid"`
- D) ✅ `hydra -l admin -P rockyou.txt example.com https-post-form "/login:username=^USER^&password=^PASS^:F=Invalid credentials"`

**Explanation:**

- **A** is incorrect — `ssh` specifies SSH protocol — not a web form attack. This would attempt SSH login on port 22, not an HTTP form submission on port 443. The syntax does not include form field specifications required for HTTP form attacks.
- **B** is incorrect — `http-get` specifies an HTTP GET request. Login forms typically use POST to submit credentials (POST body, not URL parameters). Using GET would append credentials to the URL — unusual and often incorrect for modern login forms.
- **C** is incorrect — `http-get-form` specifies GET-based form submission. The form uses POST (as stated in the question). Also, the field names are wrong — the question specifies `username` and `password`, but this option uses `user` and `pass`.
- **D** ✅ is correct — `https-post-form` specifies HTTPS + POST method + web form. The format: `"/login:username=^USER^&password=^PASS^:F=Invalid credentials"` has three colon-separated parts: the path (`/login`), the POST body with placeholders (`^USER^` and `^PASS^` are replaced by Hydra), and the failure string (`F=Invalid credentials` — if response contains this text → attempt failed). `-l admin` sets a single username, `-P rockyou.txt` provides the password wordlist.

---

### Q23

**HTTP Basic Authentication sends credentials as `Authorization: Basic YWRtaW46cGFzc3dvcmQ=`. A security tester runs:**

    echo "YWRtaW46cGFzc3dvcmQ=" | base64 -d

**The output is `admin:password`. What does this demonstrate about HTTP Basic Auth and under what condition is it acceptable to use?**

- A) HTTP Basic Auth is secure — the Base64 encoding provides strong encryption equivalent to AES-128
- B) HTTP Basic Auth is insecure in all circumstances — even over HTTPS the credentials can be decoded
- C) HTTP Basic Auth is only insecure on wireless networks — wired networks protect against decoding
- D) ✅ HTTP Basic Auth uses Base64 encoding (not encryption) — credentials are trivially decodable by anyone who captures the header — it is only acceptable over HTTPS where TLS encrypts the HTTP headers preventing interception

**Explanation:**

- **A** is incorrect — Base64 is an **encoding scheme** — not encryption. It has no key, no cryptographic strength, and is completely reversible by anyone using any Base64 decoder tool. AES-128 is a symmetric encryption algorithm requiring a key — fundamentally different from Base64.
- **B** is incorrect — over HTTPS (TLS), the entire HTTP request including the `Authorization: Basic` header is encrypted by TLS. A network-level attacker cannot intercept the header in transit. HTTP Basic Auth IS acceptable over HTTPS — TLS provides the confidentiality that Base64 lacks.
- **C** is incorrect — the wire medium (wireless vs wired) does not protect Base64 encoding. Any attacker on the same wired segment who can capture packets (e.g., via ARP poisoning + sniffing) can read Base64-encoded credentials just as easily as a wireless attacker. The protection comes from TLS — not the wire medium.
- **D** ✅ is correct — Base64 is purely a representation change (binary data → ASCII text) with no security properties. It is designed for data transport compatibility — not confidentiality. The decoded output `admin:password` demonstrates that any attacker with packet capture capability can immediately read the credentials. The ONLY condition under which HTTP Basic Auth is acceptable: **must be used exclusively over HTTPS** where TLS encrypts the Authorization header before transmission, preventing any network-level interception.

---

### Q24

**Which of the following combinations provides the MOST comprehensive defence against all four web password attack types (brute force, dictionary attack, credential stuffing, and password spraying)?**

- A) Strong password policy + account lockout after 5 attempts
- B) CAPTCHA on login form + IP-based rate limiting
- C) HTTPS everywhere + server-side password hashing (bcrypt)
- D) ✅ Multi-factor authentication + account lockout + rate limiting per username + breach password check (HaveIBeenPwned API) + CAPTCHA

**Explanation:**

- **A** is incorrect — strong password policy reduces dictionary attack success. Account lockout stops brute force against one account. But lockout does NOT stop password spraying (one attempt per account), and neither control stops credential stuffing (real passwords bypass complexity checks). MFA is missing — the only control that stops ALL four even if password is known.
- **B** is incorrect — CAPTCHA slows automated attacks. IP rate limiting slows attacks from single IPs. But modern credential stuffing uses residential proxy networks (thousands of IPs) — IP rate limiting is ineffective. CAPTCHA can be bypassed with CAPTCHA-solving services. MFA and per-username rate limiting are missing.
- **C** is incorrect — HTTPS protects credentials in transit (good). bcrypt hashing protects stored passwords from database breach cracking (good). But neither stops online brute force, spraying, stuffing, or dictionary attacks against the live login form. These are SERVER-SIDE storage/transport controls — they do not prevent online authentication attacks.
- **D** ✅ is correct — layered defence addressing each attack: **MFA** — even with correct password (stuffing, spraying, dictionary success), second factor required. **Account lockout** — stops high-rate brute force. **Rate limiting per username** — slows spraying and dictionary attacks. **Breach password check** — block registration/use of known compromised passwords (stops credential stuffing before it starts). **CAPTCHA** — forces human interaction for each attempt — slows/stops automated tools. No single control stops all four — only layered defence does.

---

## Questions 25–28 — Extra Notes & Real-World

---

### Q25

**The Equifax data breach (2017) resulted in 147 million people's personal data being stolen. Which specific OWASP vulnerability category caused this breach, and what was the attacker's exploitation method?**

- A) SQL injection (OWASP A03) — attackers injected malicious SQL through Equifax's credit check web form
- B) Broken Authentication (OWASP A07) — attackers used credential stuffing to access the admin panel
- C) Security Misconfiguration (OWASP A05) — Equifax left default credentials on their Apache server
- D) ✅ Vulnerable and Outdated Components (OWASP A06) — attackers exploited CVE-2017-5638, a known Remote Code Execution vulnerability in Apache Struts 2 that Equifax had not patched despite a patch being available for 2 months

**Explanation:**

- **A** is incorrect — the Equifax breach was not caused by SQL injection through a credit check form. The initial access was through a framework-level vulnerability — not application-level input validation.
- **B** is incorrect — credential stuffing was not the attack vector. The attacker gained initial access through a remote code execution vulnerability — no credentials were required for initial compromise.
- **C** is incorrect — the issue was an unpatched software vulnerability — not default credentials. Equifax had the correct credentials on their system — the attacker exploited a code vulnerability that bypassed authentication entirely.
- **D** ✅ is correct — the Equifax breach exploited **CVE-2017-5638** — a critical RCE vulnerability in the Apache Struts 2 web framework used by Equifax's dispute resolution portal. The vulnerability allowed attackers to execute OS commands via the `Content-Type` HTTP header in multipart form uploads. Apache released a patch in March 2017; Equifax failed to apply it. Attackers exploited the unpatched system in May 2017. This is the textbook example of **OWASP A06 — Vulnerable and Outdated Components** — demonstrating that failing to patch critical third-party components can be catastrophic. The $700 million FTC settlement was partly attributed to negligent patching practices.

---

### Q26

**In Burp Suite, what is the difference between the Intruder module's "Sniper" attack type and the "Cluster Bomb" attack type — and when would each be used in web password cracking?**

- A) Sniper uses one wordlist for both username and password simultaneously; Cluster Bomb uses separate wordlists for each and tests them sequentially
- B) Sniper works only on GET requests; Cluster Bomb works on POST forms — the HTTP method determines which to use
- C) ✅ Sniper uses one payload position and tests it with a single wordlist — used for single-field attacks like password-only brute force on a known username; Cluster Bomb uses multiple payload positions with separate wordlists and tests ALL combinations — used for username + password enumeration simultaneously
- D) Sniper sends one request per second for stealth; Cluster Bomb sends maximum requests for speed — the difference is purely throttling behaviour

**Explanation:**

- **A** is incorrect — Sniper tests ONE position with ONE wordlist — not both simultaneously. When it has multiple positions marked, it tests each position separately (one at a time) while keeping others constant — not simultaneously combining both with one wordlist.
- **B** is incorrect — both Sniper and Cluster Bomb work with any HTTP method (GET, POST, or others). The attack type is about payload position strategy — not the HTTP method used.
- **C** ✅ is correct — **Sniper**: one payload list, ONE active position at a time. If you mark `§username§` and `§password§`, Sniper tests all wordlist values in position 1 (username) while keeping position 2 constant, then tests all values in position 2 while keeping position 1 constant. Use case: known username + password wordlist (one position active). **Cluster Bomb**: multiple positions with SEPARATE wordlists — tests ALL COMBINATIONS. If username list has 100 entries and password list has 10,000 entries → 1,000,000 requests. Use case: unknown username AND unknown password — enumerate both simultaneously. Cluster Bomb is the most comprehensive but generates exponentially more requests.
- **D** is incorrect — Sniper and Cluster Bomb are not distinguished by request rate or throttling. Rate control in Burp Intruder is configured separately in the options — both attack types can be throttled or run at maximum speed.

---

### Q27

**Content Security Policy (CSP) is the primary browser-side defence against XSS. What does the following CSP header specifically permit and deny:**

    Content-Security-Policy: default-src 'self'; script-src 'self' https://cdn.trusted.com; img-src *

- A) Permits scripts from anywhere; denies images from all external sources; permits everything else from same origin
- B) Permits all resources from same origin; denies scripts from external CDNs; permits images from all sources
- C) ✅ Permits scripts ONLY from the same origin and cdn.trusted.com; permits images from any source; all other resources (CSS, fonts, frames, media) default to same-origin only — inline scripts and event handlers are denied by default
- D) Permits all resources from cdn.trusted.com; denies everything from the same origin; permits images from trusted sources only

**Explanation:**

- **A** is incorrect — `script-src 'self' https://cdn.trusted.com` explicitly limits script sources to SAME ORIGIN and cdn.trusted.com — not anywhere. Scripts from any other domain are blocked.
- **B** is incorrect — `img-src *` permits images from ALL sources (wildcard) — not just same-origin. Scripts from cdn.trusted.com are specifically PERMITTED (not denied) — the CSP allows that CDN as a trusted script source.
- **C** ✅ is correct — parsing the CSP: **`default-src 'self'`** — fallback for all resource types not explicitly specified: CSS, fonts, frames, media, objects → same origin only. **`script-src 'self' https://cdn.trusted.com`** — JavaScript can only be loaded from same origin OR cdn.trusted.com. Any `<script src="https://attacker.com/evil.js">` is blocked. Inline `<script>` tags and `onclick=` event handlers are ALSO blocked by default (inline scripts require `'unsafe-inline'` to allow). **`img-src *`** — images can be loaded from ANY domain (wildcard). This CSP significantly limits XSS impact — even if an attacker injects `<script>` tags, external scripts cannot load and inline scripts are blocked.
- **D** is incorrect — `default-src 'self'` permits same-origin resources (not denies them). cdn.trusted.com is an additional ALLOWED source — not the primary one. The CSP does not deny same-origin content.

---

### Q28

**Under Indian IT Act 2000, which section specifically covers financial fraud committed by exploiting a web application (such as manipulating prices via parameter tampering or using SQL injection to transfer funds) — and what is the maximum penalty?**

- A) Section 66C — identity theft — maximum 3 years + ₹1 lakh
- B) Section 66F — cyberterrorism — maximum life imprisonment
- C) Section 43(a) — unauthorized access — maximum civil compensation ₹1 crore
- D) ✅ IPC Section 420 — cheating and dishonestly inducing delivery of property — maximum 7 years imprisonment + fine; combined with IT Act Section 66 (3 years + ₹5 lakh) for criminal computer access

**Explanation:**

- **A** is incorrect — Section 66C covers identity theft (fraudulently using another person's digital identity/signature). Price manipulation via parameter tampering uses the attacker's OWN identity — it is financial fraud through technical manipulation, not identity impersonation. 66C would apply if the attacker used someone else's credentials, not their own tampered parameters.
- **B** is incorrect — Section 66F covers cyberterrorism — specifically attacks on critical infrastructure with intent to threaten national sovereignty or security. Price manipulation on an e-commerce site, while criminal, does not constitute cyberterrorism against national security infrastructure.
- **C** is incorrect — Section 43(a) covers unauthorized access (civil liability). While it applies, it is a civil provision (compensation) — not criminal prosecution. The question asks about financial fraud prosecution, and the maximum civil compensation under 43(a) is ₹1 crore — this is not the most specifically applicable provision for financial fraud.
- **D** ✅ is correct — **IPC Section 420** (Cheating and dishonestly inducing delivery of property) is the most directly applicable provision for financial fraud via web exploitation. Purchasing goods at £0.02 by tampering with pricing parameters, or using SQL injection to manipulate financial records, constitutes cheating — inducing the victim (merchant/bank) to deliver property (goods, money) through deception. Maximum penalty: **7 years imprisonment + fine**. This is combined with **IT Act Section 66** (criminal unauthorized access / computer fraud) for an additional 3 years + ₹5 lakh. In complex web fraud cases, multiple provisions apply simultaneously — IPC 420 provides the highest imprisonment term for the fraud itself.

---

## Answer Key

| Q# | Answer | Topic Area |
|---|---|---|
| Q01 | C | Directory traversal — three alternative names |
| Q02 | C | Server version disclosure — ServerTokens Prod |
| Q03 | D | Directory listing — Options -Indexes |
| Q04 | D | HTTP response splitting — CRLF injection |
| Q05 | D | Cross-Site Tracing — TRACE + XST + HttpOnly bypass |
| Q06 | D | robots.txt — advertises sensitive paths to attackers |
| Q07 | C | SQL injection — authentication bypass with `admin'--` |
| Q08 | D | Boolean-based blind SQL injection — true/false response |
| Q09 | D | Union-based SQL injection — data extraction |
| Q10 | D | Time-based blind SQLi — WAITFOR DELAY — MSSQL identified |
| Q11 | C | WAF bypass — case variation + tab whitespace substitution |
| Q12 | D | Parameterized queries — only complete SQLi fix |
| Q13 | D | sqlmap `--dbs` — correct database enumeration command |
| Q14 | D | OWASP 2021 A01 — Broken Access Control — from A5 in 2017 |
| Q15 | D | IDOR — server-side authorization check per request |
| Q16 | D | XXE injection — file disclosure — disable external entities |
| Q17 | D | OS command injection — `;` separator — never use shell_exec with input |
| Q18 | C | File upload — extension-only check + PHP execution in upload dir |
| Q19 | D | Parameter tampering — OWASP A01 — recalculate server-side |
| Q20 | D | Password spraying — one attempt per account — lockout evasion |
| Q21 | D | Credential stuffing — real breach passwords — 0.1-2% success |
| Q22 | D | Hydra https-post-form — correct syntax |
| Q23 | D | HTTP Basic Auth — Base64 not encryption — acceptable over HTTPS |
| Q24 | D | MFA + lockout + rate limiting + breach check + CAPTCHA |
| Q25 | D | Equifax — OWASP A06 — CVE-2017-5638 — Apache Struts 2 |
| Q26 | C | Burp Suite Intruder — Sniper vs Cluster Bomb |
| Q27 | C | CSP header parsing — script-src, img-src, default-src |
| Q28 | D | IPC S.420 + IT Act S.66 — web financial fraud |

---
