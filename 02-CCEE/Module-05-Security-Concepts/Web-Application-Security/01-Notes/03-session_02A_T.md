# DoS · Buffer Overflows · Format String · Integer Overflow
# Input Validation Bypass · ROP · CVEs 2023–2025

---

## 📑 Table of Contents

- [1. Denial of Service at the Web Layer](#1-denial-of-service-at-the-web-layer)
  - [1.1 HTTP Flood](#11-http-flood)
  - [1.2 Slowloris](#12-slowloris)
  - [1.3 ReDoS — Regular Expression DoS](#13-redos--regular-expression-dos)
  - [1.4 XML Bomb (Billion Laughs Attack)](#14-xml-bomb-billion-laughs-attack)
  - [1.5 DoS vs DDoS — Key Distinction](#15-dos-vs-ddos--key-distinction)
  - [1.6 Web-Layer DoS Countermeasures](#16-web-layer-dos-countermeasures)
- [2. Stack Buffer Overflow](#2-stack-buffer-overflow)
  - [2.1 Stack Memory Layout](#21-stack-memory-layout)
  - [2.2 How Stack Buffer Overflow Works](#22-how-stack-buffer-overflow-works)
  - [2.3 Stack Overflow Exploitation Chain](#23-stack-overflow-exploitation-chain)
  - [2.4 Stack Overflow Countermeasures](#24-stack-overflow-countermeasures)
- [3. Heap Buffer Overflow](#3-heap-buffer-overflow)
  - [3.1 Heap Memory Layout](#31-heap-memory-layout)
  - [3.2 How Heap Overflow Works](#32-how-heap-overflow-works)
  - [3.3 Stack vs Heap Overflow Comparison](#33-stack-vs-heap-overflow-comparison)
  - [3.4 Heap Overflow Countermeasures](#34-heap-overflow-countermeasures)
- [4. Format String Attacks](#4-format-string-attacks)
  - [4.1 How Format String Vulnerabilities Work](#41-how-format-string-vulnerabilities-work)
  - [4.2 Reading Memory with Format Strings](#42-reading-memory-with-format-strings)
  - [4.3 Writing Memory with %n](#43-writing-memory-with-n)
  - [4.4 Format String Countermeasures](#44-format-string-countermeasures)
- [5. Integer Overflow](#5-integer-overflow)
  - [5.1 How Integer Overflow Works](#51-how-integer-overflow-works)
  - [5.2 Integer Overflow Leading to Buffer Overflow](#52-integer-overflow-leading-to-buffer-overflow)
  - [5.3 Integer Underflow and Signedness Bugs](#53-integer-underflow-and-signedness-bugs)
  - [5.4 Integer Overflow Countermeasures](#54-integer-overflow-countermeasures)
- [6. Input Validation Bypass Techniques](#6-input-validation-bypass-techniques)
  - [6.1 Encoding-Based Bypasses](#61-encoding-based-bypasses)
  - [6.2 Case Manipulation](#62-case-manipulation)
  - [6.3 Null Byte Injection](#63-null-byte-injection)
  - [6.4 HTTP Parameter Pollution](#64-http-parameter-pollution)
  - [6.5 Unicode / Homoglyph Attacks](#65-unicode--homoglyph-attacks)
  - [6.6 Boundary and Edge Case Inputs](#66-boundary-and-edge-case-inputs)
  - [6.7 Content-Type and MIME Bypass](#67-content-type-and-mime-bypass)
- [7. 📌 Extra Notes](#7--extra-notes)
  - [7.1 Return-Oriented Programming (ROP)](#71-return-oriented-programming-rop)
  - [7.2 Additional Memory Exploitation Techniques](#72-additional-memory-exploitation-techniques)
  - [7.3 Buffer Overflow CVEs 2023–2025 — NVD Examples](#73-buffer-overflow-cves-20232025--nvd-examples)
  - [7.4 OWASP API4:2023 Unrestricted Resource Consumption](#74-owasp-api42023-unrestricted-resource-consumption)
  - [7.5 DVWA Input Validation Exercises — Lab Reference](#75-dvwa-input-validation-exercises--lab-reference)
  - [7.6 Memory Protection Mechanisms — Full Reference](#76-memory-protection-mechanisms--full-reference)
  - [7.7 Exploit Development Stages — Full Chain](#77-exploit-development-stages--full-chain)
- [8. Abbreviations Table](#8-abbreviations-table)
- [9. Keywords + Concept Map](#9-keywords--concept-map)
- [10. Quick Reference Cheatsheet](#10-quick-reference-cheatsheet)
- [11. Session Revision Snapshot](#11-session-revision-snapshot)

---

## 1. Denial of Service at the Web Layer

**Definition:** A Denial of Service (DoS) attack makes a system,
service, or network resource unavailable to its intended users by
overwhelming it with requests, exploiting resource consumption
vulnerabilities, or crashing it via malformed input.

**Web-layer DoS** specifically targets the **application layer
(Layer 7)** or the connection handling layer (Layer 4/5) rather
than exhausting raw network bandwidth (Layer 3). Web-layer attacks
are more efficient — a small number of requests can cause
disproportionate server resource consumption.

> [!IMPORTANT]
> Web-layer DoS maps to **A05:2025 Injection** (for ReDoS, XML bomb)
> and **API4:2023 Unrestricted Resource Consumption** in the API
> Security Top 10. Classic volumetric DDoS (network layer) is
> distinct from web-layer application DoS.

---

### 1.1 HTTP Flood

**Type:** Layer 7 (Application Layer) volumetric attack

**Mechanism:**
An attacker sends a massive volume of legitimate-looking HTTP
GET or POST requests to a web server, exhausting:
- Thread pool — server runs out of worker threads to handle new requests
- Memory — each connection consumes RAM for buffers, session state
- CPU — request processing, TLS handshakes, database queries
- Database connections — POST floods triggering expensive DB operations

```
Normal server capacity: 1,000 requests/second
HTTP flood rate:        500,000 requests/second (via botnet)
Result:                 Server queue overflows → new legitimate
                        requests rejected (HTTP 503 / timeout)
```

**GET flood vs POST flood:**

| Type | Target | Why POST is worse |
|---|---|---|
| **GET flood** | Web server / CDN | Can be cached by CDN — partially mitigated |
| **POST flood** | Application server / DB | Cannot be cached — each request hits app server + DB |

**HTTP/2 Rapid Reset (CVE-2023-44487):**
A specific HTTP/2 amplification technique discovered in 2023 where
an attacker repeatedly sends a HEADERS frame (initiating a stream)
immediately followed by a RST_STREAM frame (cancelling it).
The server spends CPU processing each stream initiation before the
cancel arrives — the attacker can generate far more cancelled
streams per second than the server can handle. This attack broke
records with peaks of **398 million requests per second** — far
exceeding all previous DDoS records.

> [!NOTE]
> CVE-2023-44487 (HTTP/2 Rapid Reset) is directly listed in your
> syllabus. It affected all major HTTP/2 implementations: nginx,
> Apache, IIS, Node.js, Go net/http, AWS, Cloudflare, Google. All
> vendors released patches in October 2023.

**Countermeasures:**
- Rate limiting per IP and per session
- CDN / DDoS mitigation services (Cloudflare, AWS Shield, Akamai)
- CAPTCHA on POST-heavy endpoints
- Connection limits per IP at the load balancer
- Patch HTTP/2 implementations (for CVE-2023-44487)
- Disable HTTP/2 stream prioritization features if not needed

---

### 1.2 Slowloris

**Type:** Layer 7 low-and-slow connection exhaustion attack

**Created by:** Robert "RSnake" Hansen — 2009

**Mechanism:**
Slowloris keeps HTTP connections to the target server open as long
as possible by sending **partial HTTP requests** — headers one at a
time, very slowly — without ever completing the request. The server
keeps the connection thread open waiting for the request to complete.

```
Normal HTTP request:
  GET / HTTP/1.1\r\n
  Host: target.com\r\n
  \r\n               ← blank line = end of headers → request complete

Slowloris attack:
  GET / HTTP/1.1\r\n
  Host: target.com\r\n
  X-a: b\r\n         ← partial header sent
  [pause 10 seconds]
  X-b: c\r\n         ← another header — never sends final \r\n
  [pause 10 seconds]
  ... repeats indefinitely

Result:
  Server thread held open for each connection
  With enough connections → all server threads exhausted
  New legitimate connections: Connection refused
```

**Why Slowloris is dangerous:**
- Requires very little bandwidth — **a single machine can take
  down a server**
- Specifically effective against Apache, which uses a
  **thread-per-connection model** (maximum threads = maximum simultaneous connections)
- Servers like Nginx (event-driven, handles many connections
  asynchronously) are far less vulnerable

**Variants:**
- **Slow POST / RUDY (R-U-Dead-Yet):** Sends HTTP POST with a
  large `Content-Length` but delivers the POST body one byte at
  a time — very slowly. Same thread exhaustion but via request
  body instead of headers.
- **Slow Read:** Sends a valid request but reads the response
  extremely slowly — keeps server send buffer full, tying up
  the connection from the response side.

**Countermeasures:**
- Set **minimum request rate thresholds** — close connections
  sending below X bytes/second
- Set aggressive **connection timeout** values — drop
  incomplete requests after N seconds
- Limit concurrent connections per source IP
- Use **Nginx or event-driven servers** (less susceptible due
  to async I/O model)
- Reverse proxy / load balancer to absorb slow connections
- `mod_reqtimeout` Apache module — enforces minimum transfer rates

---

### 1.3 ReDoS — Regular Expression DoS

**Type:** Application Layer CPU exhaustion via algorithmic complexity

**Mechanism:**
ReDoS exploits **catastrophic backtracking** in regular expression
engines. Certain regex patterns with **nested quantifiers** or
**alternation** cause the regex engine to explore an exponentially
growing number of paths when matching certain inputs.

**How backtracking works:**
```
Vulnerable regex: (a+)+$
Input: "aaaaaaaaaaaaaaaaab"

The regex engine tries:
  - Match all 'a's as one group → fails at 'b'
  - Backtrack → split into two groups → fails
  - Try every possible split → 2^N combinations for N 'a' chars

N=20 chars → ~1,000,000 operations
N=30 chars → ~1,000,000,000 operations
N=40 chars → ~1,000,000,000,000 operations

Result: Single request → 100% CPU → server unresponsive
```

**Classic vulnerable regex patterns:**

| Vulnerable Pattern | Reason |
|---|---|
| `(a+)+` | Nested quantifier — catastrophic backtracking |
| `(a\|a?)+` | Nested alternation with overlap |
| `(a\|aa)+` | Overlapping alternation |
| `([a-zA-Z]+)*` | Nested quantifier on character class |
| `^(a+)+$` | Anchored nested quantifier |

**Real-World Example:**

**npm `ua-parser-js` (2021):** A ReDoS vulnerability in a
User-Agent string parsing regex. Since `ua-parser-js` had
**~7 million weekly downloads**, a single malicious HTTP request
with a crafted User-Agent could freeze any Node.js server using
the library.

**Stack Overflow ReDoS (2016):** A single crafted post caused
Stack Overflow's post validation regex to consume 100% CPU for
~34 seconds — taking the site down. The regex `^[\s\u200c\u200d]*(…)`
was vulnerable to catastrophic backtracking on certain inputs.

**Countermeasures:**
- Audit all regular expressions for nested quantifiers and
  overlapping alternation
- Use **non-backtracking regex engines** (RE2, Rust's `regex`
  crate — linear time guarantee)
- Set **regex timeout limits** — abort matching after N milliseconds
- Use a **regex complexity analysis tool** (OWASP recommends
  safe-regex, vuln-regex-detector)
- Rate-limit endpoints that process user-supplied patterns
- Prefer simple character class matching over complex alternation

> [!NOTE]
> ReDoS is classified under **A05:2025 Injection** (algorithmic
> injection into the regex interpreter) and **A06:2025 Insecure
> Design** (vulnerable regex is a design-level flaw). It is also
> a specific sub-case of **API4:2023 Unrestricted Resource
> Consumption** when the DoS occurs on an API endpoint.

---

### 1.4 XML Bomb (Billion Laughs Attack)

**Type:** Application Layer memory exhaustion via entity expansion

**Mechanism:**
An XML bomb exploits the XML specification's support for
**entity expansion** to create exponentially expanding content
from a tiny input. A small XML document containing nested entity
references can expand to **gigabytes or terabytes** of data in
memory — exhausting the server's RAM and causing DoS.

```xml
<?xml version="1.0"?>
<!DOCTYPE lolz [
  <!ENTITY lol "lol">
  <!ENTITY lol2 "&lol;&lol;&lol;&lol;&lol;&lol;&lol;&lol;&lol;&lol;">
  <!ENTITY lol3 "&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;">
  <!ENTITY lol4 "&lol3;&lol3;&lol3;&lol3;&lol3;&lol3;&lol3;&lol3;&lol3;&lol3;">
  <!ENTITY lol5 "&lol4;&lol4;&lol4;&lol4;&lol4;&lol4;&lol4;&lol4;&lol4;&lol4;">
  <!ENTITY lol6 "&lol5;&lol5;&lol5;&lol5;&lol5;&lol5;&lol5;&lol5;&lol5;&lol5;">
  <!ENTITY lol7 "&lol6;&lol6;&lol6;&lol6;&lol6;&lol6;&lol6;&lol6;&lol6;&lol6;">
  <!ENTITY lol8 "&lol7;&lol7;&lol7;&lol7;&lol7;&lol7;&lol7;&lol7;&lol7;&lol7;">
  <!ENTITY lol9 "&lol8;&lol8;&lol8;&lol8;&lol8;&lol8;&lol8;&lol8;&lol8;&lol8;">
]>
<lolz>&lol9;</lolz>
```

**Expansion calculation:**
- `lol` = 3 bytes ("lol")
- `lol2` = 10 × lol = 30 bytes
- `lol3` = 10 × lol2 = 300 bytes
- `lol9` = 10^9 × 3 bytes = **~3 GB** in memory
- With deeper nesting: 10^10 levels = **30 GB**; easily tunable
  to terabytes

**Why it works:**
XML parsers are required by the XML specification to expand all
entity references before processing. A compliant parser has no
choice but to expand `&lol9;` — exhausting available memory
before the application even sees the content.

**Variants:**
- **Quadratic Blowup:** A single entity defined as a long string,
  referenced thousands of times — grows quadratically rather than
  exponentially but still effective
- **External Entity DoS (XXE-DoS):** Uses external entity
  references to cause DoS via file reads or network requests
  in a loop

**OWASP Classification:**
- **A02:2025 Security Misconfiguration** — XML parser external
  entity and DTD processing enabled when it should be disabled
- **A04:2023 / API4:2023 Unrestricted Resource Consumption** —
  single request consumes unbounded memory

**Countermeasures:**
- **Disable DTD processing entirely** — most effective
  (`FEATURE_DISALLOW_DOCTYPE_DECL = true` in Java SAX parser)
- **Disable external entity expansion** — prevents XXE and
  external entity DoS
- Set **entity expansion limits** in parser configuration
  (most modern parsers support `entityExpansionLimit`)
- Set **maximum document size** limits
- Validate XML structure before deep parsing

> [!IMPORTANT]
> The XML bomb and XXE (from Session 01B) both exploit XML entity
> processing — but for different goals: **XXE exfiltrates data**
> (reads files, SSRF); the **XML bomb causes DoS** (memory
> exhaustion). Both are prevented by disabling DTD/entity
> processing. Both fall under **A02:2025 Security
> Misconfiguration**.

---

### 1.5 DoS vs DDoS — Key Distinction

| Property | DoS | DDoS |
|---|---|---|
| **Source** | Single machine / IP | Multiple machines (botnet) |
| **Volume** | Limited by single host | Can reach terabits/sec |
| **Attribution** | Easier — single source IP | Harder — thousands of IPs |
| **Mitigation** | Block single IP | Requires DDoS mitigation service |
| **Web-layer relevance** | Slowloris, ReDoS, XML bomb | HTTP flood botnets, DNS amplification |

**Amplification attacks (DDoS specific):**
Attacker sends small spoofed requests to third-party servers
with the victim's IP as source — servers send large responses
to victim. Bandwidth amplification factor = response size ÷
request size.

| Protocol | Amplification Factor |
|---|---|
| DNS | Up to 50×–70× |
| NTP (Monlist) | Up to 556× |
| SSDP | Up to 30× |
| Memcached | Up to **50,000×** (largest known) |

---

### 1.6 Web-Layer DoS Countermeasures

| Defense | Targets | How It Helps |
|---|---|---|
| **Rate limiting** | HTTP flood, ReDoS endpoints | Throttle requests per IP/session/endpoint |
| **Connection timeout** | Slowloris | Drop incomplete requests after N seconds |
| **Request size limits** | XML bomb, HTTP flood | Reject oversized payloads before parsing |
| **CDN / Anycast** | HTTP flood, DDoS | Distribute traffic across global PoPs |
| **WAF** | Application layer DoS | Block malformed requests, enforce rules |
| **DDoS scrubbing** | Volumetric DDoS | Cloud scrubbing services (Cloudflare, AWS Shield) |
| **Auto-scaling** | HTTP flood | Absorb spikes by adding capacity |
| **Disable DTD processing** | XML bomb | Prevent entity expansion before parsing |
| **RE2 / linear regex engine** | ReDoS | Guaranteed linear-time matching |
| **Nginx / async servers** | Slowloris | Event-driven I/O — not thread-per-connection |
| **HTTP/2 patch** | CVE-2023-44487 | Close RST_STREAM abuse window |

---

## 2. Stack Buffer Overflow

### 2.1 Stack Memory Layout

The **call stack** is a region of memory used for:
- Local variables of the current function
- Function arguments
- Control flow information (saved return address, frame pointer)

**Stack growth direction:** On most architectures (x86/x64),
the stack grows **downward** — toward lower memory addresses.
Buffer allocations grow **upward** (toward higher addresses).
This collision is what makes buffer overflows dangerous.

**Typical stack frame layout (x86, high→low address):**
```
High address
┌─────────────────────────────┐
│  Function arguments         │  ← passed by caller
├─────────────────────────────┤
│  Return Address (RET)       │  ← ← ← PRIMARY TARGET
├─────────────────────────────┤
│  Saved Frame Pointer (SFP)  │  ← caller's %ebp
├─────────────────────────────┤
│  Local Variables            │
├─────────────────────────────┤
│  Buffer (e.g., char buf[64])│  ← data written here grows upward ↑
└─────────────────────────────┘
Low address
```

> [!IMPORTANT]
> The **return address** is stored on the stack adjacent to local
> buffers. If a buffer overflow writes past the buffer boundary,
> it can overwrite the return address — redirecting execution to
> attacker-controlled code when the function returns.

---

### 2.2 How Stack Buffer Overflow Works

**Vulnerable C code:**
```c
#include <string.h>
void vulnerable_function(char *input) {
    char buffer[64];           // 64-byte local buffer on stack
    strcpy(buffer, input);     // No length check — copies until \0
}

int main() {
    char attacker_input[256];
    // Attacker supplies 256 bytes of input
    vulnerable_function(attacker_input);
    return 0;
}
```

**What happens:**
```
Buffer is 64 bytes.
Input is 256 bytes.
strcpy() copies all 256 bytes starting at buffer[0].

Bytes 0–63:   Fill the buffer
Bytes 64–67:  Overwrite Saved Frame Pointer (SFP)
Bytes 68–71:  Overwrite Return Address ← CRITICAL
Bytes 72+:    Overwrite further stack data

When function returns:
  CPU pops overwritten return address from stack
  Execution jumps to attacker-controlled address
```

**Dangerous C functions (no bounds checking):**

| Function | Safe Alternative |
|---|---|
| `strcpy(dst, src)` | `strncpy(dst, src, n)` or `strlcpy()` |
| `strcat(dst, src)` | `strncat(dst, src, n)` |
| `gets(buffer)` | `fgets(buffer, size, stdin)` |
| `scanf("%s", buf)` | `scanf("%63s", buf)` (length limiter) |
| `sprintf(buf, fmt, ...)` | `snprintf(buf, size, fmt, ...)` |
| `memcpy(dst, src, len)` | Validate `len` before calling |

> [!NOTE]
> `gets()` is so dangerous it was **removed from the C11 standard**
> entirely. Any code using `gets()` is automatically vulnerable to
> stack buffer overflow. This is a common MCQ fact.

---

### 2.3 Stack Overflow Exploitation Chain

**Classic exploitation (pre-mitigations):**
```
Step 1 — Find buffer size
  Crash the application with increasing input lengths
  Identify exact offset where return address is overwritten

Step 2 — Determine return address
  Find a reliable address pointing to attacker's shellcode
  Original technique: Jump to NOP sled → shellcode

Step 3 — Construct payload
  [padding: N bytes] + [new return address] + [NOP sled] + [shellcode]

  NOP sled: sequence of 0x90 (NOP instruction) bytes
  → gives a landing zone — any address in the NOP sled
    slides execution down to shellcode

Step 4 — Trigger the overflow
  Supply crafted payload as input → function returns →
  execution redirected to shellcode
```

**NOP sled visualization:**
```
Memory:
[AAAA...AAAA][NEW_RET_ADDR][0x90 0x90 0x90 0x90...][SHELLCODE]
 ^ padding   ^ overwrites   ^ NOP sled               ^ executes
              return addr    any address here works
```

**Shellcode:**
Position-independent machine code that the attacker wants to
execute — typically spawns a shell (`/bin/sh`) or establishes
a reverse TCP connection back to the attacker.

---

### 2.4 Stack Overflow Countermeasures

| Mitigation | Mechanism | Bypasses |
|---|---|---|
| **Stack Canary (SSP)** | Random value placed between buffer and return address — checked before function returns — abort if changed | Canary leak needed; format string attacks can leak canary |
| **ASLR (Address Space Layout Randomization)** | Randomizes base addresses of stack, heap, libraries on each execution | Information leaks, brute force (32-bit), partial overwrites |
| **NX / DEP (No-Execute / Data Execution Prevention)** | Marks stack and heap memory as non-executable — shellcode in data region cannot execute | Return-to-libc, ROP chains bypass this |
| **PIE (Position Independent Executable)** | Randomizes executable's own base address (requires ASLR) | Information leaks, partial overwrites |
| **SafeStack / Shadow Stack** | Separate stack for return addresses — hardware-enforced (Intel CET) | Complex to exploit; emerging standard |
| **Bounds checking (compiler)** | `-fstack-protector`, AddressSanitizer | Not enabled by default in production |
| **Safe string functions** | `strncpy`, `fgets`, `snprintf` | Developer discipline required |

> [!IMPORTANT]
> The standard modern mitigation stack is **Canary + ASLR + NX +
> PIE** — all four together. Bypassing all four simultaneously
> requires information leaks + ROP chains. This is why ROP is the
> dominant modern exploitation technique (covered in Extra Notes).

---

## 3. Heap Buffer Overflow

### 3.1 Heap Memory Layout

The **heap** is a region of memory used for **dynamic memory
allocation** — memory requested at runtime via `malloc()`,
`calloc()`, `new` (C++).

Unlike the stack, heap memory:
- Does not grow/shrink with function calls
- Is managed by a **heap allocator** (dlmalloc, tcmalloc,
  jemalloc)
- Contains allocator **metadata** (chunk headers) interspersed
  with data

**Heap chunk structure (glibc malloc):**
```
┌──────────────────────────────────┐
│  prev_size (8 bytes)             │ ← size of previous chunk if free
├──────────────────────────────────┤
│  size (8 bytes)                  │ ← size of this chunk + flags
├──────────────────────────────────┤
│  User data (application data)    │ ← malloc() returns pointer here
│                                  │
│  [If free: fd + bk pointers]     │ ← forward/back pointers for free list
└──────────────────────────────────┘
```

---

### 3.2 How Heap Overflow Works

**Vulnerable C code:**
```c
char *buf1 = malloc(64);    // Allocate 64 bytes
char *buf2 = malloc(64);    // Allocate another 64 bytes (adjacent)
strcpy(buf1, user_input);   // No length check — can overflow into buf2
```

**What happens:**
```
Heap layout after malloc:
[chunk_header][buf1: 64 bytes][chunk_header][buf2: 64 bytes]

If input > 64 bytes:
  Overflow writes past buf1 into:
  1. buf2's chunk header (corrupts allocator metadata)
  2. buf2's data (overwrites adjacent object's content)

Consequences:
  1. Heap metadata corruption → controlled free() → arbitrary write
  2. Object data corruption → if buf2 holds a function pointer,
     overwriting it → arbitrary code execution
  3. Use-After-Free setup → manipulate allocation patterns
```

**Heap exploitation targets:**
- **Function pointers** stored in heap objects — overwrite to
  redirect execution
- **vtable pointers** (C++) — overwrite virtual function table
  pointer in heap object → method call → attacker function
- **Heap metadata** — corrupt `prev_size`/`size` fields to
  manipulate `free()` behavior → arbitrary write
- **GOT (Global Offset Table)** — overwrite entries via heap
  corruption to redirect function calls

---

### 3.3 Stack vs Heap Overflow Comparison

| Property | Stack Overflow | Heap Overflow |
|---|---|---|
| **Memory region** | Stack (function frames) | Heap (dynamic allocations) |
| **Primary target** | Return address | Function pointers, vtables, heap metadata, adjacent objects |
| **Trigger** | Exceeding fixed local buffer | Exceeding dynamically allocated buffer |
| **Typical vulnerable functions** | `strcpy`, `gets`, `scanf` | `strcpy` into malloc'd buf, `memcpy` without length check |
| **Canary protection** | ✅ Canary between buffer and RET address | ❌ Canary doesn't protect heap objects |
| **Exploitation complexity** | Lower (classic; well-understood) | Higher (heap layout must be controlled) |
| **Heap-specific technique** | N/A | Heap spraying, tcache poisoning, house of force |
| **Modern relevance** | Still found in C/C++ code | Dominant in browser exploitation, kernel exploits |

---

### 3.4 Heap Overflow Countermeasures

- **Bounds-checking wrappers:** Always validate sizes before
  `memcpy()`, `strcpy()` into malloc'd buffers
- **Heap metadata protection:**
  - Modern glibc uses hardened `free()` — validates chunk metadata
    before processing
  - Safe unlinking — checks forward/back pointers for consistency
- **Heap canaries** — some allocators place guard values around
  heap chunks
- **ASLR** — randomizes heap base address — harder to predict
  target addresses
- **AddressSanitizer (ASan)** — compiler instrumentation detecting
  heap overflows at runtime (used in testing/fuzzing)
- **Memory-safe languages** — Rust, Go — bounds checking enforced
  by language runtime eliminates class of vulnerabilities

---

## 4. Format String Attacks

### 4.1 How Format String Vulnerabilities Work

**Definition:** A format string vulnerability occurs when
user-controlled input is passed **directly as the format string
argument** to functions like `printf()`, `sprintf()`, `fprintf()`,
`snprintf()`. The format string functions interpret `%` format
specifiers in the input — allowing an attacker to read or write
arbitrary memory.

**Vulnerable vs safe code:**
```c
// VULNERABLE:
printf(user_input);          // user_input is the format string
sprintf(buf, user_input);    // user_input controls format

// SAFE:
printf("%s", user_input);    // Format string is literal "%s"
                              // user_input treated as data only
```

**Why this is dangerous:**
Format specifiers in `printf()` cause the function to consume
arguments from the stack. When no actual arguments were passed,
`printf()` reads whatever is on the stack — attacker-controlled
format specifiers can read arbitrary stack data.

```c
// Function call with no arguments but format specifiers in input:
printf("%x %x %x %x");
// printf reads 4 values from stack (where arguments should be)
// Outputs: stack contents as hex values
```

---

### 4.2 Reading Memory with Format Strings

**Format specifiers used in attacks:**

| Specifier | Action | Attack Use |
|---|---|---|
| `%x` | Print next stack value as hex | Read stack contents |
| `%d` | Print next stack value as decimal | Read stack contents |
| `%s` | Print string at address on stack | Read arbitrary memory as string |
| `%p` | Print pointer value | Read and leak pointers (ASLR defeat) |
| `%n` | Write count of chars printed so far to address | Write to arbitrary memory ← most dangerous |
| `%Nd$` | N = argument position, $ = direct parameter access | Access Nth argument directly |

**Reading stack values:**
```c
// Input: "%x.%x.%x.%x"
// printf() reads 4 consecutive stack values as hex
// Output: "bffffa94.bffffaa0.4.6c6c6548"
//                                       ^ "Hell" in ASCII — stack content

// Reading specific stack position (direct parameter access):
// Input: "%7$x"   → reads 7th argument position on stack
```

**Leaking canary values:**
```c
// If canary is on the stack at position 15:
// Input: "%15$x"  → leaks canary value
// Attacker knows canary → can include correct canary in overflow payload
```

---

### 4.3 Writing Memory with %n

`%n` is the most dangerous format specifier. It **writes** the
number of characters printed so far to the memory address pointed
to by the corresponding argument.

**Mechanism:**
```c
int written;
printf("AAAA%n", &written);
// After executing: written = 4 (4 chars printed before %n)
```

**Attack using %n:**
```c
// Input: "AAAA\xAA\xBB\xCC\xDD%x%x%n"
// \xAA\xBB\xCC\xDD = target memory address to write to
// %x %x = consume stack values (adjust written count)
// %n = write current char count to the address on stack
//       that points to 0xDDCCBBAA

// With careful crafting:
// Use padding to control exact value written
// printf("%" + target_value + "x%n") writes target_value to address
```

**What can be overwritten:**
- Return address (redirect execution)
- GOT (Global Offset Table) entries (hijack function calls)
- Function pointers
- `.dtors` section (destructors — run at program exit)

> [!NOTE]
> `%n` is disabled or restricted in some environments:
> - Windows `printf()` ignores `%n` by default (secure by default)
> - glibc `printf()` still supports it but adds FORTIFY_SOURCE checks
> - Many modern compilers warn on format strings with `%n`

---

### 4.4 Format String Countermeasures

- **Never pass user input as the format string:**
  ```c
  // Always use:
  printf("%s", user_input);    // user_input treated as data
  syslog(LOG_INFO, "%s", msg); // Same principle for logging functions
  ```
- **Compiler warnings:** `-Wformat` and `-Wformat-security` in GCC
  flag potentially dangerous format string usage
- **FORTIFY_SOURCE:** `_FORTIFY_SOURCE=2` adds compile-time and
  runtime checks against format string attacks
- **Static analysis (SAST):** Tools like Coverity, Fortify flag
  `printf(var)` patterns
- **Position Independent Executables (PIE) + ASLR:** Makes
  target addresses harder to predict for `%n` writes
- **Disable `%n`:** On Windows, `_set_printf_count_output(0)`
  disables `%n` globally

---

## 5. Integer Overflow

### 5.1 How Integer Overflow Works

**Definition:** Integer overflow occurs when an arithmetic
operation produces a value **outside the range representable
by the integer data type**. The result wraps around silently
— no exception is thrown in C/C++.

**Integer type ranges (C, 32-bit):**

| Type | Min | Max | Size |
|---|---|---|---|
| `unsigned int` | 0 | **4,294,967,295** (2³² - 1) | 4 bytes |
| `int` (signed) | -2,147,483,648 | **2,147,483,647** (2³¹ - 1) | 4 bytes |
| `unsigned short` | 0 | **65,535** (2¹⁶ - 1) | 2 bytes |
| `signed char` | -128 | **127** | 1 byte |
| `unsigned char` | 0 | **255** | 1 byte |

**Overflow example:**
```c
unsigned int x = 4294967295;  // MAX_UINT (0xFFFFFFFF)
x = x + 1;                   // Wraps to 0 (overflow)

unsigned char c = 255;
c = c + 1;                   // Wraps to 0

int y = 2147483647;           // MAX_INT
y = y + 1;                   // Wraps to -2147483648 (underflow)
```

---

### 5.2 Integer Overflow Leading to Buffer Overflow

The most dangerous consequence of integer overflow in security
is **incorrect buffer size calculation** — leading to an
undersized allocation that is then overflowed.

**Classic pattern:**
```c
// Vulnerable code — size calculation overflows:
void process_data(unsigned int len1, unsigned int len2) {
    unsigned int total = len1 + len2;  // Integer overflow possible!
    char *buf = malloc(total);         // Allocate undersized buffer
    memcpy(buf, data1, len1);          // First copy OK
    memcpy(buf + len1, data2, len2);   // Second copy OVERFLOWS heap!
}

// Attack:
// len1 = 0xFFFFFFFF (4294967295)
// len2 = 1
// total = 0xFFFFFFFF + 1 = 0x100000000 → truncated to 0x00000000 = 0
// malloc(0) → tiny allocation (implementation-defined, often returns 8 bytes)
// memcpy copies len1 (4GB) bytes into 0-byte buffer → massive heap overflow
```

**Length truncation via type casting:**
```c
// Vulnerability via signed/unsigned mismatch:
int get_input(int len) {
    if (len > 256) return -1;     // Check against signed int
    char buf[256];
    read(fd, buf, len);           // read() takes size_t (unsigned)
}

// Attack: pass len = -1
// -1 as signed int passes the > 256 check
// -1 cast to size_t = 0xFFFFFFFF = 4294967295
// read() reads 4GB into 256-byte buffer → stack overflow
```

---

### 5.3 Integer Underflow and Signedness Bugs

**Integer Underflow:**
Subtracting from an unsigned integer below zero wraps to
the maximum value:
```c
unsigned int x = 0;
x = x - 1;   // Wraps to 4294967295 (0xFFFFFFFF)
```

**Signedness bugs:**
```c
// Comparison between signed and unsigned:
int len = user_supplied_length;   // Could be negative
unsigned int buf_size = 256;

if (len < buf_size) {             // DANGEROUS: -1 (signed) vs 256 (unsigned)
    // -1 is promoted to unsigned: -1 → 0xFFFFFFFF > 256
    // Condition is FALSE for negative len — unexpected behavior
    // OR:
    memcpy(dest, src, len);       // len = -1 cast to size_t = 4GB
}
```

**Off-by-one:**
A specific boundary error — the calculation is off by exactly
one unit:
```c
char buf[256];
// Loop copies 0 to 256 inclusive — 257 iterations:
for (int i = 0; i <= 256; i++) {
    buf[i] = input[i];  // buf[256] writes 1 byte past end of buffer
}
```

---

### 5.4 Integer Overflow Countermeasures

- **Use safe integer libraries:**
  - C: `safe_add()` wrappers, `__builtin_add_overflow()` (GCC/Clang)
  - C++: Microsoft `SafeInt`, CERT SafeInt library
  - Rust: Overflow panics by default in debug mode; `checked_add()`
    returns `Option` in release mode
- **Validate sizes before use:**
  ```c
  // Check before computation:
  if (len1 > SIZE_MAX - len2) {  // Would overflow
      return ERROR;
  }
  size_t total = len1 + len2;   // Safe
  ```
- **Use size_t consistently** for sizes and lengths — avoid
  mixing signed and unsigned
- **Enable compiler sanitizers:**
  - `-fsanitize=integer` (UBSan — Undefined Behavior Sanitizer)
  - Detects overflow, shift errors, signedness bugs at runtime
- **Static analysis:** Coverity, Fortify, CodeQL — detect integer
  arithmetic vulnerabilities
- **Fuzzing:** Generate boundary-value inputs (0, MAX, MAX-1,
  MAX+1) to trigger integer edge cases

---

## 6. Input Validation Bypass Techniques

**Definition:** Input validation bypass techniques are methods
attackers use to make malicious input **pass through filters,
WAFs, or application-level validation** that would normally
reject it. The key insight: a filter sees one representation
of input while the backend interpreter sees another.

> [!IMPORTANT]
> Input validation failures map to **A05:2025 Injection** and
> **A02:2025 Security Misconfiguration** depending on whether
> the root cause is code-level injection or configuration of
> security controls. Understanding bypass techniques is essential
> for building robust defenses — allowlists beat denylists
> because bypasses target denylist gaps.

---

### 6.1 Encoding-Based Bypasses

**URL Encoding:**
```
Original: <script>alert(1)</script>
Encoded:  %3Cscript%3Ealert(1)%3C%2Fscript%3E

Filter blocks: <script>
URL decoded:   <script>       ← filter applied before decode
Double encoded: %253Cscript%253E  → first decode: %3Cscript → second decode: <script
```

**Double Encoding:**
```
< → %3C → %253C
  First decode (WAF):  %253C → %3C   (WAF sees %3C, not <, passes)
  Second decode (app): %3C   → <     (app sees <, vulnerability triggers)
```

**HTML Entity Encoding:**
```
<script> → &lt;script&gt;  (may bypass filters looking for literal <)
<        → &#60;  or &#x3C; or &#x003C;
```

**Base64 Encoding:**
Used to bypass filters in contexts where Base64 is decoded
before processing:
```
' OR '1'='1  → Base64: JyBPUiAnMSc9JzE=
```

**Unicode Encoding:**
```
/  → %c0%af   (overlong UTF-8 encoding — decoded to / on backend)
.  → %c0%2e   (overlong encoding)

Classic path traversal bypass:
../  → ..%c0%af  (IIS and older Apache decoded this to ../)
```

---

### 6.2 Case Manipulation

Many filters are case-sensitive and only block exact-case patterns:
```
Filter blocks: <script>
Bypass:        <ScRiPt>
               <SCRIPT>
               <Script>

Filter blocks: SELECT in SQL
Bypass:        sElEcT
               SeLeCt

Filter blocks: alert
Bypass:        Alert()
               ALERT()  (in some JS engines/contexts)
```

---

### 6.3 Null Byte Injection

Inserting null bytes (`\0`, `%00`) to terminate strings in
C-based languages while passing through higher-level language
filters:

```
PHP (< 5.3.4): filename.php%00.txt
  High-level:  sees filename.php%00.txt (passes .txt check)
  C layer:     sees filename.php (null terminates)
  Result:      PHP file executes

SQL null byte:
  input%00ignore_rest
  Some SQL parsers stop at \0 — remainder of input ignored
```

---

### 6.4 HTTP Parameter Pollution (HPP)

Sending the **same parameter multiple times** in an HTTP request.
Different servers/frameworks handle duplicate parameters
differently — some use first, some use last, some concatenate:

```http
GET /search?q=legitimate&q=<script>alert(1)</script>

Server behavior:
  PHP:     $_GET['q'] = last value  → uses <script>alert(1)</script>
  ASP.NET: Request["q"] = all values comma-joined → "legitimate,<script>..."
  JSP:     getParameter("q") = first value → uses "legitimate"

WAF checks: first parameter only → sees "legitimate" → passes
Backend:    uses last parameter  → sees XSS payload → fires
```

**HPP in API contexts:**
```
POST /api/transfer?amount=100&amount=10000
If API uses last value → transfers 10000 instead of 100
```

---

### 6.5 Unicode / Homoglyph Attacks

Using Unicode characters that look identical or similar to ASCII
characters to bypass string-matching filters:

```
Filter blocks: "admin"
Bypass:        "ɑdmin"  (ɑ = Latin alpha, U+0251, looks like 'a')
               "аdmin"  (а = Cyrillic 'a', U+0430 — identical appearance)

Filter blocks: "script"
Unicode zero-width:
  scr\u200Bipt  (U+200B = zero-width space, invisible, bypasses string match)
  scr\u00ADipt  (U+00AD = soft hyphen, invisible in many renderers)

IDN Homograph attacks (domain spoofing):
  аpple.com (Cyrillic 'а') vs apple.com (Latin 'a')
  — visually identical in browser URL bar
```

---

### 6.6 Boundary and Edge Case Inputs

Testing the limits of what the application handles:

```
Length limits:
  Empty string: ""
  Maximum length: 65535 chars, 2^31-1 chars, 2^32 chars
  Exactly N+1 bytes (where N = buffer size)
  Zero: 0, -0, 0.0

Numeric edges:
  0, -1, MAX_INT, MIN_INT, MAX_INT+1, MAX_UINT
  Negative values for length/index parameters

Special characters (filter bypass + injection):
  ' " ; < > & | \ / . : @ # $ % ^ * ? ! ` ~ = + ( ) { } [ ]

Whitespace variants:
  Space (0x20), Tab (0x09), Newline (0x0A), CR (0x0D)
  Non-breaking space (0xA0), Em space (0x2003)
  Used to break keyword detection: SE LECT, sel%09ect

Format string test:
  %s %d %n %x %%
  → If application reflects these back unescaped → format string vuln

Path traversal:
  ../
  ..\
  ..%2f (URL encoded)
  ..%5c (URL encoded backslash)
  ....// (filter evasion)
```

---

### 6.7 Content-Type and MIME Bypass

**Bypassing file upload validation:**
```
Upload a PHP webshell but trick the server into accepting it:

Technique 1: Extension bypass
  shell.php        → blocked
  shell.php5       → may be accepted + executed by PHP
  shell.pHp        → case bypass if filter is case-sensitive
  shell.php.jpg    → double extension (some servers execute leftmost)
  shell.php%00.jpg → null byte truncation (PHP < 5.3.4)

Technique 2: MIME type bypass
  Content-Type: image/jpeg  (spoofed)
  [actual content is PHP code]
  → Server validates Content-Type header, not file content
  → PHP code stored and executed via direct access

Technique 3: Magic bytes
  Prepend JPEG magic bytes to PHP:
  FF D8 FF E0 (JPEG header) + <?php system($_GET['cmd']); ?>
  → File passes magic-byte check
  → PHP still executes remaining content as code

Technique 4: .htaccess upload
  Upload .htaccess with: AddType application/x-httpd-php .jpg
  → All .jpg files now execute as PHP
  → Upload any .jpg containing PHP code → RCE
```

> [!NOTE]
> File upload bypass is a common vector for remote code execution.
> Correct defense: validate on **server-side using file content
> analysis** (not just extension or Content-Type header), store
> uploaded files **outside the web root**, and serve them through
> a separate process that never executes their content.

---

## 7. 📌 Extra Notes

---

### 7.1 Return-Oriented Programming (ROP)

> [!NOTE]
> ROP is the dominant modern exploitation technique for bypassing
> NX/DEP (non-executable stack/heap). It chains together existing
> code fragments from the program's own binary and loaded libraries
> — no shellcode injection needed.

**The problem ROP solves:**
With NX/DEP enabled, attacker-injected shellcode in data regions
(stack, heap) **cannot execute** — the CPU raises an exception
if execution reaches a non-executable page.

**ROP solution:**
Instead of injecting new code, ROP reuses **existing executable
code** already present in the binary and loaded libraries
(libc, libssl, etc.). These fragments are called **gadgets**.

**What is a ROP gadget:**
A short sequence of instructions ending in a **`RET`
instruction** (`0xC3` on x86). Since `RET` pops the next
value from the stack and jumps to it, chaining gadgets means:
```
Stack layout for ROP chain:
┌─────────────────────┐
│  addr of gadget_1   │ ← initial overwritten return address
├─────────────────────┤
│  data for gadget_1  │ ← arguments / values consumed by gadget_1
├─────────────────────┤
│  addr of gadget_2   │ ← gadget_1 ends in RET → pops this
├─────────────────────┤
│  data for gadget_2  │
├─────────────────────┤
│  addr of gadget_3   │
└─────────────────────┘

Execution flow:
gadget_1 executes → RET pops addr of gadget_2 → jumps there
gadget_2 executes → RET pops addr of gadget_3 → jumps there
... chain continues until final payload executes
```

**Common gadget types:**

| Gadget Type | Assembly | Purpose |
|---|---|---|
| **pop; ret** | `pop eax; ret` | Load value into register |
| **mov; ret** | `mov [eax], ebx; ret` | Write value to memory |
| **add; ret** | `add eax, ebx; ret` | Arithmetic |
| **xor; ret** | `xor eax, eax; ret` | Zero a register |
| **syscall; ret** | `syscall; ret` | Trigger system call |
| **jmp; ret** | `jmp esp; ret` | Jump to stack |

**ROP attack chain example — calling `execve("/bin/sh")`:**
```
Goal: call execve("/bin/sh", NULL, NULL) via system call

Step 1: Find gadgets in libc using ROPgadget, pwntools, Ropper
Step 2: Build chain to:
  - Load "/bin/sh" string address into rdi (first argument)
  - Zero out rsi, rdx (second and third args)
  - Load syscall number 59 (execve on x64 Linux) into rax
  - Execute syscall gadget

All addresses come from libc — which is mapped executable
→ NX/DEP is bypassed: we never execute data, only existing code
```

**Tools for ROP:**
- **ROPgadget:** Find all gadgets in a binary
- **pwntools:** Python exploit development framework — has ROP module
- **Ropper:** GUI and CLI gadget finder
- **angr:** Symbolic execution + ROP chain generation

**ROP variants:**

| Technique | Description |
|---|---|
| **ret2libc** | Call `system("/bin/sh")` using libc's `system()` function — simplest ROP |
| **ret2plt** | Return to PLT (Procedure Linkage Table) entry — used before ASLR bypass |
| **SROP (Sigreturn-Oriented Programming)** | Uses `sigreturn` syscall to set all registers at once from a fake signal frame |
| **JOP (Jump-Oriented Programming)** | Uses `JMP` dispatcher gadgets instead of `RET` — bypasses CFI (Control Flow Integrity) |
| **COP (Call-Oriented Programming)** | Uses `CALL` dispatcher gadgets |

**How ASLR complicates ROP:**
With ASLR, library base addresses are randomized per execution.
Gadget addresses change each run. Bypasses:
1. **Information leak** — use another vulnerability (format string,
   read primitive) to leak a pointer from libc → calculate base
   → all gadget addresses known
2. **Partial overwrite** — overwrite only low bytes of return
   address (known) — ASLR only randomizes high bytes
3. **Heap spray** — fill large memory regions with ROP chains
   — hope one lands at a predictable address
4. **Brute force** (32-bit only) — ASLR has only 2¹⁶ possible
   positions on 32-bit → ~65,536 attempts

**Intel CET (Control-flow Enforcement Technology):**
Hardware-level defense against ROP introduced in Intel Tiger
Lake (11th gen) processors:
- **Shadow Stack (SS):** Separate read-only stack storing return
  addresses — CPU checks that `RET` matches shadow stack value
- **IBT (Indirect Branch Tracking):** Marks valid branch targets
  with `ENDBRANCH` instruction — prevents jumping to arbitrary
  gadgets mid-function
- CET makes ROP significantly harder — `ENDBRANCH` must be
  present at every gadget entry, and shadow stack prevents
  return address manipulation

> [!IMPORTANT]
> For exams: **NX/DEP breaks classic shellcode injection** →
> attacker switches to **ret2libc/ROP** (reuses existing code) →
> **ASLR** randomizes library addresses → attacker needs an
> **information leak** to de-randomize → **Stack Canary**
> detects stack corruption before function return → attacker
> needs to leak canary too. This is why modern exploitation
> requires **chaining multiple vulnerabilities**.

---

### 7.2 Additional Memory Exploitation Techniques

> [!NOTE]
> These techniques appear in MCQs and CVE descriptions related
> to buffer overflows.

**Use-After-Free (UAF):**
```c
char *buf = malloc(64);     // Allocate
free(buf);                  // Free — buf pointer still valid!
// ... some code ...
strcpy(buf, user_input);    // Write to freed memory ← UAF

// If another allocation reused buf's memory for a different object,
// the write corrupts that object
```
UAF is one of the most exploited vulnerability classes in modern
browsers (Chrome, Firefox V8/SpiderMonkey engine). Maps to
**CWE-416**.

**Heap Spray:**
Filling large portions of heap memory with NOP sleds + shellcode
(or ROP chains). When a pointer is corrupted to an unpredictable
heap address, the probability of landing in the spray is high.
Common in browser exploitation.

**Double Free:**
Calling `free()` on the same pointer twice — corrupts heap
allocator's free list metadata → exploitable for arbitrary write.
```c
free(buf);
// ...
free(buf);  // Double free — heap corruption
```
Maps to **CWE-415**.

**Stack Pivot:**
A ROP gadget that moves the stack pointer (`rsp/esp`) from
the original stack to an attacker-controlled memory region
(heap spray, data section). Allows ROP chains to be stored
in heap rather than being constrained to stack layout.
```asm
; Stack pivot gadget example:
xchg eax, esp   ; swap eax (attacker-controlled) with esp
ret             ; now ROP chain continues from attacker's fake stack
```

---

### 7.3 Buffer Overflow CVEs 2023–2025 — NVD Examples

> [!NOTE]
> These CVEs are exam-relevant because your syllabus explicitly
> requires "latest buffer overflow CVEs 2023–2025." Know the
> affected component, CVE ID, type, and impact.

**CVE-2023-44487 — HTTP/2 Rapid Reset (DoS)**
- **Component:** All major HTTP/2 implementations (nginx, Apache
  httpd, IIS, Go, Node.js)
- **Type:** Application-layer DoS — stream exhaustion, not
  classic buffer overflow, but a resource consumption attack
- **Impact:** Record-breaking DDoS amplification — 398 Mrps
  peak; all services using HTTP/2 vulnerable
- **Patch:** October 2023 — all major vendors released updates
- **CWE:** CWE-400 Uncontrolled Resource Consumption

**CVE-2023-4911 — Looney Tunables (glibc Buffer Overflow)**
- **Component:** GNU C Library (glibc) — `ld.so` dynamic linker
- **Type:** Heap buffer overflow in `GLIBC_TUNABLES` environment
  variable parsing
- **Impact:** Local privilege escalation to root — affects
  Fedora, Ubuntu, Debian (all using glibc with SUID binaries)
- **CVSS v3.1 Score:** 7.8 (High)
- **CWE:** CWE-122 Heap-based Buffer Overflow
- **Significance:** Affects essentially all mainstream Linux
  distributions; SUID binaries inherit the environment variable

**CVE-2023-20569 — AMD Inception (Speculative Execution)**
- **Component:** AMD EPYC, Ryzen processors
- **Type:** Speculative execution side-channel — not a
  classic buffer overflow but a CPU microarchitectural attack
- **Impact:** Information disclosure — kernel memory leak
  across privilege boundaries
- **Note:** In same family as Spectre/Meltdown

**CVE-2024-3094 — XZ Utils Backdoor**
- **Component:** XZ Utils / liblzma compression library
- **Type:** Supply chain attack (not buffer overflow) — malicious
  code injected by compromised maintainer
- **Impact:** Backdoored SSH authentication in affected Linux
  distributions (Debian unstable, Fedora 41)
- **CVSS v3.1 Score:** 10.0 (Critical)
- **Significance:** Near-miss — caught before reaching stable
  distributions. Canonical A03:2025 Supply Chain example.

**CVE-2024-6387 — regreSSHion (OpenSSH RCE)**
- **Component:** OpenSSH server (sshd) — versions < 4.4p1
  and 8.5p1 to < 9.8p1
- **Type:** Signal handler race condition — async signal safety
  violation leading to heap corruption → RCE
- **Impact:** Unauthenticated Remote Code Execution as root
  on glibc-based Linux systems; affects ~14 million exposed
  servers
- **CVSS v3.1 Score:** 8.1 (High)
- **CWE:** CWE-362 Race Condition; CWE-122 Heap-based Buffer
  Overflow
- **Significance:** Regression of CVE-2006-5051 — a vulnerability
  that was fixed in 2006 and reintroduced in 2020. Shows
  importance of regression testing. Unauthenticated RCE on SSH
  = critical severity.

**CVE-2024-21762 — Fortinet FortiOS Out-of-Bounds Write**
- **Component:** Fortinet FortiOS / FortiProxy SSL VPN
- **Type:** Out-of-bounds write vulnerability
- **Impact:** Unauthenticated Remote Code Execution
- **CVSS v3.1 Score:** 9.6 (Critical)
- **CWE:** CWE-787 Out-of-Bounds Write
- **Significance:** Actively exploited in the wild — used by
  nation-state threat actors. Patches required immediately.

**CVE-2025-0282 — Ivanti Connect Secure Stack Overflow**
- **Component:** Ivanti Connect Secure (VPN appliance)
- **Type:** Stack-based buffer overflow
- **Impact:** Unauthenticated Remote Code Execution — exploited
  as zero-day in the wild before patch availability
- **CVSS v3.1 Score:** 9.0 (Critical)
- **CWE:** CWE-121 Stack-based Buffer Overflow
- **Significance:** Zero-day exploitation of VPN appliances;
  CISA issued emergency directive for federal agencies.

> [!TIP]
> CVE exam pattern: know **component + type + impact + CWE**
> for each major CVE. You don't need exploitation details —
> but knowing "regreSSHion = OpenSSH = heap corruption race
> condition = unauthenticated RCE" is exactly what MCQs test.

---

### 7.4 OWASP API4:2023 Unrestricted Resource Consumption

> [!NOTE]
> API4:2023 directly relates to DoS at the web/API layer and
> was renamed from API4:2019 "Lack of Resources & Rate Limiting"
> to focus on the root cause. Full detail in Session 01B — this
> section cross-references the DoS attacks in this session.

**Mapping of this session's DoS attacks to API4:2023:**

| Attack | API4:2023 Relevance |
|---|---|
| HTTP Flood | Missing rate limiting → API overwhelmed by request volume |
| Slowloris | No connection timeout → thread pool exhausted by slow connections |
| ReDoS | Compute-intensive regex endpoint with no timeout → CPU exhaustion |
| XML Bomb | No payload size limit or entity expansion limit → memory exhaustion |

**API4:2023 specific attack vectors:**
- No rate limiting on authentication endpoints → credential stuffing DoS
- No pagination on list endpoints → single request returns entire DB
- No request payload size limits → oversized POST bodies
- No timeout on expensive operations → DB query DoS
- Webhook endpoints without rate limiting → trigger expensive downstream processing
- SMS/email OTP endpoints → financial DoS by flooding paid messaging

**CVSS scoring dimension for API4:**
API4:2023 primarily impacts **Availability (A)** in the CIA triad.
When resource exhaustion leads to data leakage, it also impacts
**Confidentiality (C)**.

**Countermeasures (API4:2023 specific):**
- Implement **per-endpoint rate limits** — not just global limits
- Return **HTTP 429 Too Many Requests** with `Retry-After` header
  when rate limit exceeded
- Enforce **pagination** on all collection endpoints
- Set **maximum payload size** in API gateway and application
- Set **query timeout** for all database operations
- Implement **circuit breakers** for downstream service calls
- Monitor and alert on abnormal resource consumption patterns

---

### 7.5 DVWA Input Validation Exercises — Lab Reference

> [!NOTE]
> This section maps DVWA modules directly to the input validation
> and buffer overflow concepts in this session — for MCQs
> referencing lab exercises.

**DVWA Relevant Modules (Session 02A context):**

**Command Injection module:**
- Security Level Low: No filtering — direct OS command injection
  via `;`, `&&`, `||`
- Security Level Medium: Blacklists `&&` and `;` — bypass with
  `|` or `%0a` (newline)
- Security Level High: Stronger blacklist — bypass via `| id`
  (pipe with space) or encoded characters
- Security Level Impossible: allowlist — only valid IP format
  accepted — cannot be bypassed

**SQL Injection (Blind) module:**
- Uses time-based and boolean-based techniques — same underlying
  concepts as input validation bypass
- Tests whether input reaches SQL interpreter

**File Upload module:**
- Level Low: Any file type accepted — upload PHP webshell directly
- Level Medium: Checks Content-Type header — bypass by spoofing
  to `image/jpeg`
- Level High: Checks file extension and magic bytes — bypass by
  embedding PHP in valid JPEG or using `.php5` extension
- Level Impossible: Resizes image using GD library — PHP code in
  image data is destroyed by the resize operation

**DVWA Security Level behavior:**
```
Low     → No input validation at all
Medium  → Denylist-based filtering (bypassable)
High    → Stronger denylist + some allowlist elements (harder to bypass)
Impossible → Strict allowlist + parameterized queries (correct approach)
```

> [!IMPORTANT]
> The DVWA progression from Low → Impossible mirrors the
> **defense-in-depth** principle — and the key exam lesson is
> that **denylist validation (Medium, High) is always bypassable**
> while **allowlist validation (Impossible) is not**. MCQs test
> this distinction.

**Burp Suite integration with DVWA:**
- Proxy DVWA traffic through Burp
- Use Intruder to test input validation bypass payloads at scale
- Use Repeater to manually test encoding variations
- Active Scanner can auto-detect SQLi, XSS, command injection
  in DVWA modules
(Full Burp Suite coverage in Session 03B)

---

### 7.6 Memory Protection Mechanisms — Full Reference

> [!NOTE]
> MCQs frequently ask about which mitigation defeats which attack,
> and which attacks bypass which mitigation. This table is the
> complete cross-reference.

| Mitigation | What It Does | Defeats | Bypassed By |
|---|---|---|---|
| **Stack Canary (SSP)** | Random value between buffer and return address — abort if modified | Classic stack overflow + shellcode | Format string leak of canary value; heap overflow (canary not present) |
| **NX / DEP** | Stack + heap marked non-executable | Shellcode injection in data regions | Return-to-libc, ROP chains (reuse existing code) |
| **ASLR** | Randomizes addresses of stack, heap, libraries | Fixed-address exploitation (ROP, ret2libc) | Information leaks, brute force (32-bit), partial overwrite |
| **PIE** | Randomizes executable's own base address | Fixed-address gadgets in the binary itself | Information leaks from binary itself |
| **RELRO (Partial)** | Makes `.got` read-only after dynamic linking resolves | Partial GOT overwrite during startup | Still exploitable after startup (Full RELRO needed) |
| **RELRO (Full)** | Entire GOT read-only at runtime | GOT overwrite via format string / heap | Requires other write targets |
| **SafeStack** | Separates return addresses onto a separate protected stack | Stack overflow + ROP chain | Complex — very recent hardware/compiler feature |
| **Intel CET / IBT** | Hardware: shadow stack + indirect branch tracking | ROP chains (must use ENDBRANCH gadgets only) | JOP with valid ENDBRANCH targets (rare, complex) |
| **AddressSanitizer (ASan)** | Runtime bounds checking (development/testing only) | Overflows, UAF, double free (in test/dev) | Not used in production — performance overhead |
| **FORTIFY_SOURCE** | Replaces unsafe string functions with bounded versions at compile time | Some `strcpy`/`gets` overflows | Doesn't help with correct-seeming but oversized input |

---

### 7.7 Exploit Development Stages — Full Chain

> [!NOTE]
> Understanding the full exploitation chain from vulnerability
> to shell is important for MCQs about what each technique
> achieves and in what order.

**Stage 1 — Vulnerability Discovery:**
- Fuzzing (AFL, libFuzzer) — generate random/mutated inputs
- Static analysis — review source code for dangerous functions
- Dynamic analysis — debugger observation (GDB, WinDbg, x64dbg)
- CVE/NVD research — known vulnerabilities in components

**Stage 2 — Crash Confirmation:**
```
Cyclic pattern (pwntools cyclic(200)):
  Send unique cyclic string → application crashes
  Read crash register (EIP/RIP) → find pattern offset
  Calculate exact overwrite offset
```

**Stage 3 — Control EIP/RIP:**
```
Send: [padding: N bytes] + [controlled address: 4/8 bytes]
Confirm: EIP/RIP contains controlled value in debugger
```

**Stage 4 — Defeat Mitigations:**
- Leak canary (via format string or read primitive)
- Leak libc address (via format string, %p, or GOT read)
- Calculate ASLR base from leaked address
- Build ROP chain using correct addresses

**Stage 5 — Payload Delivery:**
```
Classic (no mitigations):
  [NOP sled] + [shellcode] → redirect EIP to NOP sled

Modern (all mitigations):
  [canary value] + [fake saved rbp] + [ROP chain]
  → ROP calls mprotect() to make stack executable → shellcode
  or
  → ROP calls execve("/bin/sh") directly via syscall gadget
```

**Stage 6 — Post-Exploitation:**
- Privilege escalation (if low-priv shell obtained)
- Persistence (cron, service, startup)
- Lateral movement
- Data exfiltration

---

## 8. Abbreviations Table

| Abbreviation | Full Form | Technical Meaning |
|---|---|---|
| DoS | Denial of Service | Making a system/service unavailable to intended users |
| DDoS | Distributed Denial of Service | DoS using multiple distributed sources (botnet) |
| ReDoS | Regular Expression Denial of Service | DoS via catastrophic backtracking in vulnerable regex |
| DTD | Document Type Definition | XML schema mechanism that enables entity declarations — exploited in XML bombs and XXE |
| ROP | Return-Oriented Programming | Exploit technique chaining existing code gadgets ending in RET to bypass NX/DEP |
| NX | No-Execute | CPU/OS feature marking memory pages as non-executable |
| DEP | Data Execution Prevention | Windows implementation of NX |
| ASLR | Address Space Layout Randomization | OS feature randomizing memory base addresses to prevent hardcoded-address exploitation |
| PIE | Position Independent Executable | Binary compiled to run at randomized base address (requires ASLR to be effective) |
| SSP | Stack Smashing Protector | Compiler feature inserting stack canary to detect overflow |
| CET | Control-flow Enforcement Technology | Intel hardware feature providing shadow stack + indirect branch tracking against ROP |
| IBT | Indirect Branch Tracking | Component of Intel CET — requires ENDBRANCH instruction at valid jump targets |
| UAF | Use-After-Free | Accessing memory after it has been freed — heap exploitation primitive |
| GOT | Global Offset Table | ELF binary structure mapping function names to runtime addresses — target for overwrites |
| PLT | Procedure Linkage Table | ELF stub code resolving external function addresses at first call — target for ret2plt |
| SROP | Sigreturn-Oriented Programming | ROP variant using sigreturn syscall to populate all registers at once |
| JOP | Jump-Oriented Programming | ROP variant using JMP dispatchers — bypasses some CFI implementations |
| CFI | Control Flow Integrity | Security mechanism restricting valid control flow transitions |
| HPP | HTTP Parameter Pollution | Sending duplicate HTTP parameters to confuse WAF vs backend handling |
| UAF | Use-After-Free | CWE-416 — accessing freed heap memory |
| ASan | AddressSanitizer | Compiler instrumentation detecting memory errors at runtime (dev/test use) |
| UBSan | Undefined Behavior Sanitizer | Compiler instrumentation detecting integer overflow and undefined behavior |
| CVSS | Common Vulnerability Scoring System | Standardized vulnerability severity scoring (v3, v4) |
| NVD | National Vulnerability Database | NIST database of CVEs with CVSS scores and analysis |
| CWE | Common Weakness Enumeration | MITRE catalog of software weakness types — root cause classification |
| SFP | Saved Frame Pointer | Caller's base pointer saved on stack in function prologue |
| SUID | Set User ID | Linux file permission bit causing executable to run as owner (usually root) |
| CTF | Capture The Flag | Security competition using exploit challenges — common format for buffer overflow practice |

---

## 9. Keywords + Concept Map

| Term | Definition | Connects To | Use Case / Context |
|---|---|---|---|
| **HTTP Flood** | Volumetric GET/POST request flood to exhaust server resources | DDoS, botnet, CDN mitigation | Layer 7 DoS — most common web DoS |
| **Slowloris** | Partial HTTP request DoS — holds connections open with slow headers | Thread exhaustion, Apache vs Nginx | Low-bandwidth, single-machine DoS |
| **ReDoS** | CPU exhaustion via catastrophic regex backtracking | Nested quantifiers, RE2 engine | Any endpoint using complex regex on user input |
| **XML Bomb** | Entity expansion DoS — small XML → gigabytes in memory | DTD, XXE, entity expansion | SOAP APIs, XML-processing services |
| **Stack Buffer Overflow** | Writing past fixed local buffer on stack → overwrite return address | Return address, NOP sled, shellcode, canary | Classic memory corruption in C/C++ |
| **Heap Buffer Overflow** | Writing past malloc'd buffer → corrupt adjacent heap objects | UAF, vtable, function pointers, heap metadata | Browser engines, kernel exploits |
| **Stack Canary** | Random value on stack protecting return address | SSP, GCC `-fstack-protector` | Detect overflow before function return |
| **NX / DEP** | Non-executable stack/heap — shellcode can't run in data | ret2libc, ROP bypass | Post-2004 OS/CPU feature |
| **ASLR** | Randomized memory layout — addresses unpredictable | Information leaks, brute force bypass | Linux/Windows/macOS standard |
| **ROP** | Chain existing executable code gadgets ending in RET | NX bypass, gadget, ret2libc | Modern exploitation of compiled code |
| **Format String** | User input as printf format string → read/write arbitrary memory | %n, %x, GOT overwrite, canary leak | C programs with printf(user_input) |
| **Integer Overflow** | Arithmetic wraps around type boundary → incorrect size calculation | Buffer overflow, signedness bugs, off-by-one | C/C++ size calculations, allocation |
| **Off-by-One** | Loop/buffer calculation is exactly 1 unit wrong | Stack/heap corruption, boundary errors | Index errors, `<` vs `<=` |
| **Double Encoding** | Encode twice — WAF decodes once, app decodes twice | Input validation bypass, URL encoding | WAF bypass, path traversal |
| **HPP** | Duplicate HTTP parameters — WAF vs backend handle differently | XSS bypass, parameter confusion | WAF evasion, API logic flaws |
| **Null Byte** | `\0` terminates C strings — bypasses extension checks | LFI bypass, PHP < 5.3.4, SQL | File inclusion, upload bypass |
| **Use-After-Free** | Access freed memory — heap corruption exploit primitive | CWE-416, browser exploits, UAF chains | Chrome V8, kernel exploitation |
| **Heap Spray** | Fill heap with NOP+payload — increase probability of landing | Browser exploits, ASLR bypass | When exact address unknown |
| **Stack Pivot** | ROP gadget moving rsp to attacker-controlled region | Complex ROP chains, heap spray | When stack space limited |
| **Looney Tunables** | CVE-2023-4911 — glibc heap overflow in TUNABLES parsing | Local privilege escalation, CWE-122 | All mainstream Linux distros |
| **regreSSHion** | CVE-2024-6387 — OpenSSH signal handler race condition → RCE | CWE-362, CWE-122, unauthenticated RCE | ~14M exposed SSH servers |
| **Allowlist vs Denylist** | Allowlist: permit known good; Denylist: block known bad | Input validation, DVWA levels | Allowlist always stronger |

---

## 10. Quick Reference Cheatsheet

### 📊 Web-Layer DoS — Full Comparison

| Attack | Type | Layer | Resource Targeted | Bandwidth Needed | Tool/Technique |
|---|---|---|---|---|---|
| HTTP GET Flood | Volumetric | L7 | CPU, threads, connections | High (botnet) | LOIC, HTTP flood scripts |
| HTTP POST Flood | Volumetric | L7 | CPU, DB, threads | Medium-High | More damaging than GET |
| Slowloris | Low-and-slow | L7 | Server threads (connection pool) | Very low | Slowloris.py, PyLoris |
| Slow POST (RUDY) | Low-and-slow | L7 | Server threads | Very low | RUDY tool |
| ReDoS | Algorithmic | L7 | CPU (single thread) | Minimal (1 request) | Crafted string input |
| XML Bomb | Algorithmic | L7 | RAM | Minimal (1 request, KB) | Crafted XML payload |
| HTTP/2 Rapid Reset | Protocol | L4/L7 | CPU (stream processing) | Low (amplified) | CVE-2023-44487 |

---

### 📊 Buffer Overflow Types — Comparison

| Property | Stack Overflow | Heap Overflow | Format String (as overflow) |
|---|---|---|---|
| **Region** | Stack | Heap | Stack (via %n write) |
| **Primary target** | Return address | Adjacent objects, function pointers, vtable | GOT, return address, arbitrary memory |
| **Canary protection** | ✅ Yes | ❌ No | ❌ Canary can be leaked |
| **NX bypass** | ROP / ret2libc | ROP / heap spray | ROP / GOT overwrite |
| **Detection tool** | GDB, ASan, Valgrind | Valgrind, ASan, Heaptrack | GDB, ASan, static analysis |
| **Safe coding fix** | `strncpy`, `fgets`, `snprintf` | Validate malloc size, safe_add | `printf("%s", var)` |

---

### 📊 Memory Mitigations — Defeats and Bypasses

| Mitigation | Defeats | Bypassed By |
|---|---|---|
| Stack Canary | Stack overflow (direct RET overwrite) | Format string canary leak, heap overflow (different region) |
| NX / DEP | Shellcode in data pages | ROP chains, ret2libc |
| ASLR | Fixed-address exploitation | Information leak, brute force (32-bit), partial byte overwrite |
| PIE | Binary-specific gadgets | Binary leak/info disclosure |
| Full RELRO | GOT overwrites | Other write targets (data section, stack) |
| Intel CET | ROP chains (shadow stack blocks fake RET) | JOP with valid ENDBRANCH targets (complex) |

---

### 📊 Integer Types — Overflow Boundaries (C, 32-bit)

| Type | Max Value | Overflow To | Attack Value |
|---|---|---|---|
| `unsigned int` | 4,294,967,295 | 0 | 0xFFFFFFFF |
| `int` (signed) | 2,147,483,647 | −2,147,483,648 | 0x7FFFFFFF |
| `unsigned short` | 65,535 | 0 | 0xFFFF |
| `signed char` | 127 | −128 | 0x7F |
| `unsigned char` | 255 | 0 | 0xFF |

---

### 📊 Input Validation Bypass — Quick Reference

| Technique | Example | Defeats |
|---|---|---|
| URL encoding | `%3Cscript%3E` for `<script>` | Case-sensitive string filters |
| Double URL encoding | `%253C` for `<` | Single-decode WAFs |
| HTML entity encoding | `&lt;script&gt;` | Literal character filters |
| Null byte | `shell.php%00.jpg` | Extension-only validation |
| Case variation | `<ScRiPt>` | Case-sensitive filters |
| HTTP Parameter Pollution | `?q=safe&q=<xss>` | WAF checking first param only |
| Unicode overlong | `%c0%af` for `/` | ASCII-only path traversal filters |
| Whitespace variants | `SE%09LECT` | Keyword matching without space normalization |
| Double extension | `shell.php.jpg` | Single extension check |
| Magic byte spoofing | JPEG bytes + PHP code | Content-Type / header-only checks |

---

### 📊 Key CVEs — Session 02A Reference

| CVE | Year | Component | Type | CWE | Impact | CVSS |
|---|---|---|---|---|---|---|
| CVE-2023-44487 | 2023 | HTTP/2 (all impls) | DoS — stream exhaustion | CWE-400 | DDoS amplification (398 Mrps) | High |
| CVE-2023-4911 | 2023 | glibc (Looney Tunables) | Heap buffer overflow | CWE-122 | Local privilege escalation → root | 7.8 |
| CVE-2024-3094 | 2024 | XZ Utils / liblzma | Supply chain backdoor | CWE-506 | SSH auth bypass (near-miss) | 10.0 |
| CVE-2024-6387 | 2024 | OpenSSH (regreSSHion) | Signal handler race → heap | CWE-362/122 | Unauthenticated RCE as root | 8.1 |
| CVE-2024-21762 | 2024 | Fortinet FortiOS | Out-of-bounds write | CWE-787 | Unauthenticated RCE | 9.6 |
| CVE-2025-0282 | 2025 | Ivanti Connect Secure | Stack buffer overflow | CWE-121 | Unauthenticated RCE (zero-day) | 9.0 |

---

### 📊 ROP Chain — Technique Comparison

| Technique | How It Works | Bypasses | Complexity |
|---|---|---|---|
| ret2libc | Return to `system("/bin/sh")` in libc | NX/DEP | Low |
| Basic ROP | Chain gadgets to call syscall directly | NX/DEP + (partial ASLR) | Medium |
| SROP | Sigreturn syscall to set all regs from fake frame | NX/DEP | Medium |
| JOP | JMP-dispatcher gadgets | NX/DEP + some CFI | High |
| Heap spray + pivot | Fill heap → stack pivot into spray | NX/DEP + ASLR (probabilistic) | High |

---

### 📊 DVWA Security Levels — Input Validation Model

| Level | Approach | Bypassable? | Example (File Upload) |
|---|---|---|---|
| Low | No validation | ✅ Trivially | Upload `.php` directly |
| Medium | Denylist (block known bad) | ✅ Usually | Spoof Content-Type header |
| High | Stronger denylist + some allowlist | ✅ With effort | Use `.php5` or magic byte prepend |
| Impossible | Strict allowlist + parameterized ops | ❌ No | GD library resize destroys injected code |

---

## 11. Session Revision Snapshot

### 🎯 TL;DR — 5-Bullet Summary

1. **Web-layer DoS has four distinct attack types** — HTTP Flood
   (volumetric, threads/CPU), Slowloris (low-and-slow, thread
   exhaustion via partial requests), ReDoS (single-request CPU
   exhaustion via catastrophic regex backtracking), and XML Bomb
   (single-request RAM exhaustion via entity expansion) — each
   requires a different countermeasure.
2. **Stack overflows overwrite the return address; heap overflows
   corrupt adjacent objects and function pointers** — canaries
   protect the stack but not the heap; NX/DEP blocks shellcode
   in both; modern exploitation chains canary leak + ASLR defeat
   + ROP to bypass all protections.
3. **Format string attacks exploit `printf(user_input)` directly**
   — `%x` reads stack memory, `%n` writes to arbitrary addresses —
   the fix is always `printf("%s", user_input)` — one format
   specifier separating user input from the format string argument.
4. **Integer overflow silently wraps — leading to wrong size
   calculations → undersized allocations → buffer overflow** —
   the signedness bug pattern (`int` vs `size_t`) is especially
   dangerous because a negative length passes a `> 0` check then
   becomes 4GB when cast to unsigned.
5. **Input validation bypasses all exploit the gap between what
   the filter sees and what the backend executes** — encoding
   (URL, double, unicode, null byte), case manipulation, HPP,
   and MIME spoofing — allowlists defeat all bypass categories
   while denylists are always eventually bypassed.

---

### 📌 MCQ-Likely Concepts — Full List

| Concept | Why It's MCQ-Relevant |
|---|---|
| Slowloris only needs partial headers — never sends final `\r\n` | Mechanism detail — frequently tested |
| Slowloris effective against Apache (threaded) not Nginx (event-driven) | Architecture-specific impact |
| ReDoS = catastrophic backtracking in nested quantifiers `(a+)+` | Pattern recognition — what makes a regex vulnerable |
| RE2 engine guarantees linear-time matching — prevents ReDoS | Correct countermeasure |
| XML Bomb = Billion Laughs — `lol9` entity = ~3GB expansion | Exact mechanism and scale |
| XML Bomb + XXE both prevented by disabling DTD processing | Shared defense — MCQ trap |
| Stack grows downward; buffer fills upward — collision overwrites RET | Memory layout direction — frequently tested |
| `gets()` removed from C11 standard | Standard factoid — common MCQ |
| `strcpy`, `gets`, `scanf("%s")` — no bounds check | Dangerous function list |
| Canary between buffer and RET address | Exact canary position on stack |
| NX/DEP breaks shellcode → attacker switches to ROP | Mitigation bypass chain |
| ASLR randomizes addresses → attacker needs info leak to defeat | ASLR bypass requirement |
| All 4 mitigations together: Canary + ASLR + NX + PIE | Modern protection stack |
| ROP chains existing executable code — no new code injected | ROP definition |
| ret2libc = simplest ROP — calls `system()` in libc | ROP variant name |
| Intel CET = shadow stack + IBT — hardware ROP mitigation | Hardware mitigation |
| Format string vulnerability = `printf(var)` not `printf("%s", var)` | Root cause — one-character fix |
| `%n` writes to memory — most dangerous format specifier | Specifier function |
| `%x` reads from stack — used to leak canary | Specifier function |
| Windows `printf()` ignores `%n` by default | Platform-specific behavior |
| Integer overflow in C wraps silently — no exception | Language behavior |
| `unsigned int` max = 4,294,967,295 = 0xFFFFFFFF | Exact boundary value |
| `int` max = 2,147,483,647 — +1 wraps to negative | Signed overflow |
| Signed -1 cast to `size_t` = 0xFFFFFFFF = 4GB | Signedness bug |
| Off-by-one = exactly 1 unit boundary error | Term definition |
| Double encoding bypasses single-decode WAFs | Encoding bypass mechanic |
| Null byte `%00` terminates C strings mid-path | Null byte injection mechanic |
| HPP — PHP uses last param, ASP.NET joins, JSP uses first | Per-platform HPP behavior |
| MIME bypass — Content-Type is spoofable, not trustworthy | File upload bypass |
| `.htaccess` upload → `AddType application/x-httpd-php .jpg` | .htaccess upload bypass |
| CVE-2023-44487 = HTTP/2 Rapid Reset = 398 Mrps peak | DoS CVE — key fact |
| CVE-2023-4911 = Looney Tunables = glibc heap overflow | Linux LPE CVE |
| CVE-2024-6387 = regreSSHion = OpenSSH unauthenticated RCE | SSH CVE — regression |
| CVE-2024-3094 = XZ Utils = supply chain backdoor | Supply chain CVE |
| CVE-2025-0282 = Ivanti = stack overflow zero-day | 2025 CVE |
| Use-After-Free = CWE-416; Double Free = CWE-415 | CWE numbers |
| DVWA Low=no filter, Medium=denylist, Impossible=allowlist | DVWA level model |
| Allowlist always stronger than denylist | Core input validation principle |
| API4:2023 renamed from "Lack of Resources & Rate Limiting" to "Unrestricted Resource Consumption" | Rename trap from Session 01B |
| HTTP 429 = rate limit response code; `Retry-After` header | Correct rate-limit response |
| `open_basedir` = PHP defense against LFI path traversal | PHP configuration defense |

---
