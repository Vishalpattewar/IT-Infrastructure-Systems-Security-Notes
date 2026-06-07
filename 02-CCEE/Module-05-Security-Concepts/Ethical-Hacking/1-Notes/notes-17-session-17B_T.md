# Session 17B — Wireless Hacking · WEP/WPA Cracking · Wireless Sniffers · SSID/MAC Spoofing · Securing Wireless 📡

> Personal study notes | Ethical Hacking Module | CCEE Prep

---

## 📑 Table of Contents

- [🗺️ Where This Session Fits](#️-where-this-session-fits)
- [⚠️ Exam Traps & Misconceptions](#️-exam-traps--misconceptions)
- [🧱 Foundation Knowledge](#-foundation-knowledge)
- [Section 1 — Wireless Networking Fundamentals](#section-1--wireless-networking-fundamentals)
  - [1.1 IEEE 802.11 Standards](#11-ieee-80211-standards)
  - [1.2 Wireless Network Components](#12-wireless-network-components)
  - [1.3 Wireless Network Modes](#13-wireless-network-modes)
  - [1.4 How Wireless Authentication Works](#14-how-wireless-authentication-works)
- [Section 2 — WEP Authentication and Cracking](#section-2--wep-authentication-and-cracking)
  - [2.1 What Is WEP](#21-what-is-wep)
  - [2.2 WEP Encryption Mechanism](#22-wep-encryption-mechanism)
  - [2.3 WEP Vulnerabilities](#23-wep-vulnerabilities)
  - [2.4 WEP Cracking — Step by Step](#24-wep-cracking--step-by-step)
  - [2.5 WEP Cracking Tools](#25-wep-cracking-tools)
- [Section 3 — WPA and WPA2 Authentication and Cracking](#section-3--wpa-and-wpa2-authentication-and-cracking)
  - [3.1 What Is WPA](#31-what-is-wpa)
  - [3.2 WPA2 — CCMP and AES](#32-wpa2--ccmp-and-aes)
  - [3.3 WPA/WPA2 Personal — PSK Mode](#33-wpawpa2-personal--psk-mode)
  - [3.4 WPA/WPA2 Enterprise — 802.1X Mode](#34-wpawpa2-enterprise--8021x-mode)
  - [3.5 The Four-Way Handshake](#35-the-four-way-handshake)
  - [3.6 WPA/WPA2 Cracking — Step by Step](#36-wpawpa2-cracking--step-by-step)
  - [3.7 PMKID Attack](#37-pmkid-attack)
  - [3.8 WPS Vulnerability](#38-wps-vulnerability)
- [Section 4 — WPA3](#section-4--wpa3)
  - [4.1 WPA3 Personal — SAE](#41-wpa3-personal--sae)
  - [4.2 WPA3 Enterprise](#42-wpa3-enterprise)
  - [4.3 WPA3 Vulnerabilities](#43-wpa3-vulnerabilities)
- [Section 5 — Wireless Sniffers and Locating SSIDs](#section-5--wireless-sniffers-and-locating-ssids)
  - [5.1 Wireless Sniffing — Monitor Mode](#51-wireless-sniffing--monitor-mode)
  - [5.2 Passive vs Active Wireless Discovery](#52-passive-vs-active-wireless-discovery)
  - [5.3 Wireless Sniffing Tools](#53-wireless-sniffing-tools)
  - [5.4 Locating SSIDs — Hidden Networks](#54-locating-ssids--hidden-networks)
  - [5.5 Wardriving](#55-wardriving)
- [Section 6 — MAC Spoofing on Wireless Networks](#section-6--mac-spoofing-on-wireless-networks)
  - [6.1 What Is MAC Spoofing](#61-what-is-mac-spoofing)
  - [6.2 MAC Spoofing Attack Flow](#62-mac-spoofing-attack-flow)
  - [6.3 MAC Spoofing Tools](#63-mac-spoofing-tools)
  - [6.4 MAC Filtering — False Security](#64-mac-filtering--false-security)
- [Section 7 — Wireless Attack Techniques](#section-7--wireless-attack-techniques)
  - [7.1 Evil Twin Attack](#71-evil-twin-attack)
  - [7.2 Rogue Access Point](#72-rogue-access-point)
  - [7.3 Deauthentication Attack](#73-deauthentication-attack)
  - [7.4 KRACK Attack](#74-krack-attack)
  - [7.5 Wireless DoS Attacks](#75-wireless-dos-attacks)
- [Section 8 — Methods to Secure Wireless Networks](#section-8--methods-to-secure-wireless-networks)
  - [8.1 Encryption Standards Comparison](#81-encryption-standards-comparison)
  - [8.2 Authentication Controls](#82-authentication-controls)
  - [8.3 Network-Level Controls](#83-network-level-controls)
  - [8.4 Physical and Administrative Controls](#84-physical-and-administrative-controls)
- [📌 Extra Notes](#-extra-notes)
  - [E1 — RC4 Stream Cipher and IV Weakness Deep Dive](#e1--rc4-stream-cipher-and-iv-weakness-deep-dive)
  - [E2 — TKIP vs CCMP vs GCMP](#e2--tkip-vs-ccmp-vs-gcmp)
  - [E3 — 802.1X EAP Methods](#e3--8021x-eap-methods)
  - [E4 — Aircrack-ng Suite — Full Reference](#e4--aircrack-ng-suite--full-reference)
  - [E5 — Evil Twin vs Rogue AP vs Karma Attack](#e5--evil-twin-vs-rogue-ap-vs-karma-attack)
  - [E6 — Dragonblood — WPA3 Vulnerabilities](#e6--dragonblood--wpa3-vulnerabilities)
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
        ├── Session 16A     : DoS · DDoS · BOTs/BOTNETs · Smurf · SYN Flood
        ├── Session 16B     : Spoofing vs Hijacking · Session Hijacking
        ├── Session 17A     : Web Server Hacking · Web App Vulnerabilities
        ├── ▶ SESSION 17B   : Wireless Hacking · WEP/WPA Cracking
        │                     Wireless Sniffers · SSID/MAC Spoofing
        │                     Securing Wireless Networks
        │                                          ← YOU ARE HERE
        └── Sessions 18–20  : Backdoors · IDS · Physical Security · Malware RE

**Phase position:** Session 17B extends the attack surface to the
**physical radio layer** — 802.11 wireless networks. While Session 17A
attacked web servers and applications over wired/internet connections,
wireless attacks exploit the radio broadcast nature of Wi-Fi — where
any device within radio range can potentially intercept, inject, or
disrupt communications without any physical network access.

The sniffing knowledge from Session 15 (promiscuous mode, monitor
mode) and the password cracking knowledge from Session 17A (wordlists,
brute force) both converge here — wireless cracking is fundamentally
a captured-handshake + offline-dictionary-attack process.

---

## ⚠️ Exam Traps & Misconceptions

| ❌ Misconception | ✅ Reality |
|---|---|
| WEP is weak only because of short key length | WEP is broken due to the FLAWED RC4 IV implementation — the 24-bit IV is too short, reused frequently, and the way IVs are incorporated into RC4 creates statistical patterns that reveal the key. Key length (64-bit or 128-bit) is irrelevant — the IV weakness exists regardless. |
| WPA and WPA2 can be cracked by directly decrypting captured traffic | WPA/WPA2 cannot be directly decrypted. The attack captures the FOUR-WAY HANDSHAKE, then performs OFFLINE DICTIONARY ATTACK against the handshake to guess the Pre-Shared Key. Without a correct dictionary entry, the PSK cannot be recovered. |
| Hiding the SSID makes a network secure | SSID hiding is security through obscurity — it is NOT a security control. Wireless scanners (airodump-ng, Kismet) detect hidden networks. The SSID is transmitted in probe requests/responses — easily discovered by passive monitoring. |
| MAC filtering is an effective security control | MAC addresses are transmitted in PLAINTEXT in 802.11 frames — visible to any passive sniffer. An attacker sniffs the MAC of an authorized device and spoofs it. MAC filtering provides ZERO security against a motivated attacker. |
| WPA2 with a strong password is uncrackable | WPA2-PSK with a strong password (random 20+ character) is computationally infeasible to crack via dictionary attack. However, WPA2 is vulnerable to: KRACK (key reinstallation), PMKID attack (no handshake capture needed), deauthentication attacks, and evil twin attacks — password strength does not protect against these. |
| WPA3 is completely secure | WPA3 was found vulnerable to the Dragonblood attacks (2019) — timing and cache side-channel attacks against the SAE handshake allow offline dictionary attacks similar to WPA2. WPA3 significantly raises the bar but is not invulnerable. |
| A deauthentication attack disconnects the attacker from the network | Deauthentication attacks target VICTIM CLIENTS — not the attacker. The attacker sends forged 802.11 deauthentication frames impersonating the AP to force victim clients to disconnect, then reconnect — capturing the WPA handshake during reconnection. |
| Evil twin and rogue AP are identical attacks | An EVIL TWIN specifically clones an existing legitimate AP (same SSID, BSSID spoof, higher signal power). A ROGUE AP is any unauthorized AP connected to a network — it may not impersonate any specific existing AP. Different attack goals and mechanisms. |
| WPS PIN brute force requires knowing the SSID first | WPS PIN brute force can be performed against any AP with WPS enabled — the SSID is discovered during the attack process. The Pixie Dust attack doesn't even require brute forcing all 11,000 combinations — it recovers the PIN in seconds from the WPS exchange. |

---

## 🧱 Foundation Knowledge

<details>
<summary>Click to expand — Must-know before this session</summary>

**Radio Frequency Basics**

- Wi-Fi operates on two primary frequency bands:
  - **2.4 GHz**: Channels 1–14 (1, 6, 11 are non-overlapping in most regions)
    - Longer range, more interference (microwaves, Bluetooth, other Wi-Fi)
  - **5 GHz**: Channels 36–165 (many non-overlapping channels)
    - Shorter range, less interference, faster speeds
  - **6 GHz** (Wi-Fi 6E): Newest band — 802.11ax — minimal interference

**802.11 Frame Types**

| Frame Type | Sub-types | Purpose |
|---|---|---|
| **Management** | Beacon, Probe Req/Resp, Auth, Assoc, Deauth | Network discovery, connection setup |
| **Control** | ACK, RTS, CTS | Flow control and error recovery |
| **Data** | Data, Null, QoS Data | Actual data transmission |

**Key 802.11 Identifiers**

- **SSID** (Service Set Identifier): Network name — up to 32 characters
- **BSSID** (Basic Service Set Identifier): MAC address of the AP radio
- **ESSID** (Extended SSID): SSID across multiple APs in same network
- **Channel**: Frequency channel the AP operates on (1–14 for 2.4GHz)

**Beacon Frames**
- APs broadcast beacon frames approximately every 100ms
- Contains: SSID, BSSID, channel, supported rates, security capabilities
- Visible to any device in range — even without association

**MITRE ATT&CK Reference**
- T1040 — Network Sniffing (wireless context)
- T1110 — Brute Force (WPA handshake cracking)
- T1557 — Adversary-in-the-Middle (evil twin)
- T1598 — Phishing for Information (evil twin portal)
- T1499 — Endpoint DoS (wireless deauthentication)

</details>

---

## Section 1 — Wireless Networking Fundamentals

### 1.1 IEEE 802.11 Standards

| Standard | Frequency | Max Speed | Security Era | Notes |
|---|---|---|---|---|
| **802.11** | 2.4 GHz | 2 Mbps | WEP (1999) | Original — obsolete |
| **802.11b** | 2.4 GHz | 11 Mbps | WEP | Widely deployed — all broken |
| **802.11a** | 5 GHz | 54 Mbps | WEP | 5GHz — less interference |
| **802.11g** | 2.4 GHz | 54 Mbps | WEP → WPA | Backward compatible with b |
| **802.11n** | 2.4/5 GHz | 600 Mbps | WPA2 | MIMO — multiple antennas |
| **802.11ac** | 5 GHz | 6.9 Gbps | WPA2/WPA3 | Wi-Fi 5 — MU-MIMO |
| **802.11ax** | 2.4/5/6 GHz | 9.6 Gbps | WPA3 | Wi-Fi 6/6E — OFDMA |
| **802.11be** | 2.4/5/6 GHz | 46 Gbps | WPA3 | Wi-Fi 7 — MLO (2024+) |

> [!NOTE]
> For exam purposes: 802.11b/g = WEP era. 802.11n/ac = WPA2 era.
> 802.11ax/be = WPA3 era. The security protocol and the 802.11
> physical standard are independent — a modern 802.11ax AP can
> still be configured with WEP (though no modern device supports it).

---

### 1.2 Wireless Network Components

| Component | Function | Attack Relevance |
|---|---|---|
| **Access Point (AP)** | Provides wireless connectivity — bridges wireless to wired | Target for impersonation (evil twin) |
| **Wireless Client (STA)** | End-user device connecting to AP | Target for deauthentication, credential theft |
| **SSID** | Network name broadcast in beacons | Discovered by sniffers — hidden SSIDs still revealed |
| **BSSID** | MAC address of AP radio | Spoofed in evil twin attacks |
| **WDS** | Wireless Distribution System — AP-to-AP links | Extends attack range |
| **Wireless Router** | AP + router + switch combined | Most common home target |
| **Wireless Controller** | Centralized management of enterprise APs | High-value target — controls all APs |

---

### 1.3 Wireless Network Modes

| Mode | Description | Security Notes |
|---|---|---|
| **Infrastructure mode** | Clients connect to AP — all traffic via AP | Standard mode — AP enforces policy |
| **Ad-hoc (IBSS) mode** | Peer-to-peer — no AP required | No centralized authentication — weaker |
| **Monitor mode** | NIC captures all 802.11 frames — no association needed | Used by attackers and analysts for passive sniffing |
| **Master mode** | NIC acts as an AP | Used in evil twin/rogue AP attacks |

---

### 1.4 How Wireless Authentication Works

**Open System Authentication (No security):**

    Client → AP: Authentication Request
    AP → Client: Authentication Response (success)
    Client → AP: Association Request
    AP → Client: Association Response
    Connected — no credentials required

**Shared Key Authentication (WEP — broken):**

    Client → AP: Authentication Request
    AP → Client: Challenge text (cleartext)
    Client → AP: Challenge encrypted with WEP key
    AP: Decrypts and verifies → sends success/failure
    VULNERABILITY: Both plaintext challenge AND encrypted response
    are transmitted — attacker captures both → derives keystream

**WPA/WPA2 Personal — Four-Way Handshake (see Section 3.5)**

**WPA/WPA2 Enterprise — 802.1X/EAP (see Section 3.4)**

---

## Section 2 — WEP Authentication and Cracking

### 2.1 What Is WEP

**WHAT:**
WEP (Wired Equivalent Privacy) was the original wireless security
protocol introduced with the IEEE 802.11 standard in 1997 and
ratified in 1999. Its goal was to provide wireless networks with
security equivalent to a wired LAN.

**WHY it failed:**
WEP was designed by a committee of hardware engineers — not
cryptographers. Critical design flaws were identified by security
researchers (Fluhrer, Mantin, and Shamir — "FMS attack") in 2001
and the protocol was completely broken by 2004.

**Key WEP parameters:**

| Parameter | Value |
|---|---|
| Key lengths | 64-bit (40-bit key + 24-bit IV) OR 128-bit (104-bit key + 24-bit IV) |
| Encryption algorithm | RC4 stream cipher |
| Integrity check | CRC-32 (ICV — Integrity Check Value) |
| IV (Initialization Vector) | 24-bit — transmitted in plaintext with each frame |

> [!IMPORTANT]
> WEP key lengths are misleading: **64-bit WEP** has only a
> **40-bit secret key** + 24-bit IV. **128-bit WEP** has a
> **104-bit secret key** + 24-bit IV. The IV is not secret —
> it is sent in plaintext in every frame header.

---

### 2.2 WEP Encryption Mechanism

    Encryption process:
    1. Take plaintext data (packet payload)
    2. Compute CRC-32 of plaintext → ICV (4 bytes) — appended to plaintext
    3. Choose a 24-bit IV (random or sequential)
    4. Concatenate: IV + WEP Key → input to RC4 PRNG
    5. RC4 generates a keystream
    6. XOR plaintext+ICV with keystream → ciphertext
    7. Transmitted frame: [IV (plaintext)] [Ciphertext]

    Decryption process:
    1. Extract IV from frame header (plaintext)
    2. Concatenate: IV + WEP Key → input to RC4 PRNG
    3. RC4 generates same keystream
    4. XOR ciphertext with keystream → plaintext + ICV
    5. Verify CRC-32 of plaintext matches ICV

**The fatal flaw:**
The IV is only 24 bits → 2²⁴ = 16,777,216 possible IVs.
On a busy network, all possible IVs are exhausted in minutes.
**IV reuse with RC4 = same keystream = cryptographic disaster.**

---

### 2.3 WEP Vulnerabilities

**Vulnerability 1 — IV Reuse (Birthday Problem):**

    24-bit IV = 16,777,216 values
    Busy AP: ~500 frames/second
    Time to IV collision: 16,777,216 / 500 = ~9.3 hours maximum
    In practice: probabilistic collision much sooner (~1 hour)
    Same IV + same key = SAME keystream
    XOR two ciphertexts encrypted with same keystream = XOR of plaintexts
    → Cryptanalysis possible without key

**Vulnerability 2 — Weak IVs (FMS Attack — 2001):**

    Fluhrer, Mantin & Shamir discovered specific "weak IVs"
    that leak key bytes through RC4 key scheduling algorithm
    Collecting ~250,000–400,000 packets containing weak IVs
    allows statistical derivation of the WEP key byte by byte
    First practical WEP cracking method — enabled aircrack-ng

**Vulnerability 3 — CRC-32 is Not Cryptographic:**

    CRC-32 detects accidental errors — NOT intentional modification
    Attacker can flip bits in ciphertext AND update CRC-32 correctly
    → Modified packet passes integrity check
    → Bit flipping attack — enables traffic injection

**Vulnerability 4 — Shared Key Authentication Flaw:**

    WEP shared key auth transmits both challenge plaintext and
    encrypted challenge → attacker learns keystream for that IV
    → Attacker can authenticate without knowing the WEP key

**Vulnerability 5 — No Per-Frame Authentication:**
Any device that knows the WEP key can inject arbitrary frames.
No mechanism to verify that frames came from legitimate sources.

> [!IMPORTANT]
> WEP is considered completely and irrevocably broken.
> It can be cracked in under 5 minutes with modern tools
> regardless of key length (64-bit or 128-bit).
> No version of WEP provides meaningful security.
> The Wi-Fi Alliance stopped certifying WEP devices in 2004.

---

### 2.4 WEP Cracking — Step by Step

**Requirements:**
- Wireless adapter supporting monitor mode and packet injection
- Linux system with aircrack-ng suite installed
- Access to the target AP's radio range

**Methodology:**

    STEP 1 — Enable monitor mode:
      airmon-ng start wlan0
      → Creates wlan0mon (monitor mode interface)

    STEP 2 — Discover target AP:
      airodump-ng wlan0mon
      → Lists all APs: BSSID, Channel, Encryption, SSID
      → Identify target: BSSID=AA:BB:CC:DD:EE:FF, CH=6, ENC=WEP

    STEP 3 — Capture packets on target AP:
      airodump-ng -c 6 --bssid AA:BB:CC:DD:EE:FF -w capture wlan0mon
      -c 6         → lock to channel 6
      --bssid      → filter to target AP only
      -w capture   → save to capture.cap file

    STEP 4 — Accelerate packet collection (ARP replay attack):
      aireplay-ng -3 -b AA:BB:CC:DD:EE:FF -h CLIENT_MAC wlan0mon
      → Capture one ARP packet from legitimate client
      → Replay it at high rate → AP generates thousands of
        new encrypted responses with different IVs
      → Rapidly accumulates the 40,000–100,000 IVs needed

    STEP 5 — Crack the key:
      aircrack-ng capture.cap
      → Statistical analysis of IV patterns (PTW/FMS attack)
      → Recovers WEP key
      → With 40,000+ IVs: typically succeeds in seconds

**Minimum IVs needed:**
- 40-bit WEP: ~20,000–40,000 unique IVs
- 104-bit WEP: ~40,000–85,000 unique IVs

**Without traffic (no clients connected):**

    aireplay-ng -1 0 -a AA:BB:CC:DD:EE:FF wlan0mon
    → Fake authentication with AP (associate without key)

    aireplay-ng -2 -p 0841 -c FF:FF:FF:FF:FF:FF \
                -b AA:BB:CC:DD:EE:FF wlan0mon
    → Interactive packet replay — inject crafted frames

---

### 2.5 WEP Cracking Tools

| Tool | Purpose |
|---|---|
| **airmon-ng** | Enable/disable monitor mode on wireless interface |
| **airodump-ng** | Passive wireless packet capture and AP/client discovery |
| **aireplay-ng** | Packet injection — ARP replay, deauthentication, fake auth |
| **aircrack-ng** | Statistical WEP key recovery from captured IVs |
| **besside-ng** | Automated WEP cracking — minimal user interaction |
| **Wireshark** | Packet analysis of captured wireless traffic |
| **CommView for WiFi** | Windows-based wireless capture and analysis |

---

## Section 3 — WPA and WPA2 Authentication and Cracking

### 3.1 What Is WPA

**WHAT:**
WPA (Wi-Fi Protected Access) was introduced in 2003 as an
**interim replacement for WEP** — designed to be deployable on
existing WEP hardware via firmware update while fixing the
critical WEP vulnerabilities.

**WPA improvements over WEP:**

| Feature | WEP | WPA |
|---|---|---|
| **Encryption** | RC4 with static key | RC4 with TKIP (per-packet key mixing) |
| **IV size** | 24-bit | 48-bit (extended via TKIP) |
| **Key management** | Static — never changes | Dynamic per-packet keys |
| **Integrity** | CRC-32 (broken) | Michael MIC (Message Integrity Code) |
| **Authentication** | Shared key or open | PSK or 802.1X/EAP |
| **Key changes** | Never | Every packet (per-packet keying) |

**TKIP (Temporal Key Integrity Protocol):**
- Generates a new encryption key for EVERY packet
- 48-bit IV (extended from WEP's 24-bit) — prevents IV reuse
- Michael MIC — detects forged packets (replaces broken CRC-32)
- Still uses RC4 underneath — inherits RC4 weaknesses

**WPA was itself deprecated in 2012 — RC4/TKIP weaknesses discovered.**

---

### 3.2 WPA2 — CCMP and AES

**WHAT:**
WPA2 (Wi-Fi Protected Access 2) was introduced in 2004 and
became mandatory for Wi-Fi Alliance certification in 2006.
It replaced TKIP+RC4 with **CCMP+AES** — a genuinely strong
cryptographic implementation.

**WPA2 improvements over WPA:**

| Feature | WPA (TKIP) | WPA2 (CCMP) |
|---|---|---|
| **Encryption algorithm** | RC4 (stream cipher) | AES-128 (block cipher) |
| **Mode of operation** | TKIP (per-packet keying) | CCMP (Counter Mode + CBC-MAC) |
| **IV size** | 48-bit | 48-bit packet number |
| **Integrity protection** | Michael MIC (128-bit) | CBC-MAC (integrated into CCMP) |
| **Header protection** | No | Yes — AAD |
| **Cryptographic strength** | Moderate (RC4 weaknesses) | Strong (AES-128) |

**CCMP (Counter Mode with CBC-MAC Protocol):**
- **Counter Mode (CTR)**: Encrypts data using AES in counter mode
- **CBC-MAC**: Provides authentication/integrity of header + data
- Combined: provides confidentiality AND integrity in one operation
- Uses a 128-bit AES key derived from the PMK

> [!IMPORTANT]
> WPA2's encryption (AES-CCMP) is NOT broken. WPA2-PSK attacks
> exploit the key ESTABLISHMENT process (four-way handshake)
> and weak PASSWORDS — not the AES encryption itself.
> A WPA2 network with a strong random PSK is effectively
> uncrackable by dictionary attack.

---

### 3.3 WPA/WPA2 Personal — PSK Mode

**WHAT:**
WPA-Personal (also called WPA-PSK) uses a single **Pre-Shared Key**
— a password known to all authorized users — for authentication.
Designed for home and small business environments.

**Key derivation from PSK:**

    PSK (password, up to 63 chars)
            ↓
    PBKDF2 function:
    PMK = PBKDF2(HMAC-SHA1, PSK, SSID, 4096 iterations, 256 bits)
            ↓
    PMK (Pairwise Master Key) — 256-bit
    This derivation is done once — same PSK + SSID always yields same PMK

    During connection (four-way handshake):
    PMK + ANonce + SNonce + BSSID + Client MAC
            ↓
    PTK (Pairwise Transient Key) — used to encrypt actual traffic
    PTK is unique per session — provides forward secrecy in WPA2
    (WPA3 provides perfect forward secrecy — see Section 4)

**The PMK and SSID relationship:**
The SSID is part of the PMK derivation. This means the PMK
(and therefore the cracking process) is SSID-dependent.
Precomputed rainbow tables for WPA must be specific to a particular
SSID. Changing the SSID (even to the same password) changes the PMK.

---

### 3.4 WPA/WPA2 Enterprise — 802.1X Mode

**WHAT:**
WPA-Enterprise uses **802.1X port-based authentication** with an
**EAP (Extensible Authentication Protocol)** and a **RADIUS server**
for centralized, per-user authentication — instead of a shared key.

**Architecture:**

    Client (Supplicant)  →  AP (Authenticator)  →  RADIUS Server (Auth Server)

    Client provides individual credentials:
    - Username + password (EAP-PEAP, EAP-TTLS)
    - Digital certificate (EAP-TLS)
    - Smart card (EAP-TLS with card)

**Advantages over PSK:**
- No shared secret — compromise of one user's credentials
  does not expose the network password to all users
- Centralized user management — revoke individual access
- Per-user session keys — each user has unique encryption keys
- Full audit trail — who connected, when, from where

**Common EAP methods:**

| EAP Method | Credential Type | Security Level |
|---|---|---|
| **EAP-TLS** | Client + Server certificates | Highest — mutual certificate authentication |
| **EAP-PEAP** | Server cert + username/password | High — widely deployed |
| **EAP-TTLS** | Server cert + various inner methods | High — flexible |
| **EAP-MD5** | Username + MD5 hash | Low — deprecated — no server auth |
| **LEAP** | Username + password (Cisco) | Low — broken — do not use |

---

### 3.5 The Four-Way Handshake

**WHAT:**
The four-way handshake is the key exchange process used in WPA
and WPA2 Personal to establish session keys between a client
and AP after the initial connection. **Capturing this handshake
is the prerequisite for offline WPA/WPA2 password cracking.**

**HOW — Four-Way Handshake Process:**

    Prerequisite: Both AP and Client independently computed PMK
    (from the same PSK + SSID)

    STEP 1 — AP → Client: ANonce (random 256-bit number from AP)

    STEP 2 — Client → AP: SNonce + MIC
      Client generates SNonce (random 256-bit number)
      Client computes PTK:
        PTK = PRF(PMK, ANonce, SNonce, AP_MAC, Client_MAC)
      Client computes MIC over message 2 using PTK
      Client sends: SNonce + MIC (proving it knows PMK without revealing it)

    STEP 3 — AP → Client: GTK + MIC
      AP also computes PTK (has all needed values now)
      AP sends Group Temporal Key (for multicast/broadcast)
      AP sends MIC proving it computed correct PTK

    STEP 4 — Client → AP: ACK
      Client confirms receipt of GTK
      Both sides now have PTK — encrypted communication begins

**Why the handshake enables offline cracking:**

    The attacker captures messages 1–4 (MIC is in message 2)
    Attacker has: ANonce, SNonce, AP_MAC, Client_MAC, MIC

    Cracking process:
    For each password in wordlist:
      1. Compute PMK = PBKDF2(candidate_password, SSID, 4096, 256)
      2. Compute PTK = PRF(PMK, ANonce, SNonce, AP_MAC, Client_MAC)
      3. Compute expected MIC from PTK
      4. Compare computed MIC with captured MIC
      5. If match → password found!
      6. If no match → try next password

**The handshake never contains the password or PMK directly —
only the MIC which is derived from them. Cracking is purely
an offline computation problem — no further network access needed.**

---

### 3.6 WPA/WPA2 Cracking — Step by Step

    STEP 1 — Enable monitor mode:
      airmon-ng check kill      ← kill processes that interfere
      airmon-ng start wlan0
      → wlan0mon created

    STEP 2 — Discover target:
      airodump-ng wlan0mon
      → Identify: BSSID, Channel, ESSID
      → Note connected clients (STATION column)

    STEP 3 — Capture on target channel:
      airodump-ng -c 6 --bssid AA:BB:CC:DD:EE:FF -w wpa_capture wlan0mon
      → Wait for a client to naturally connect (may take time)
      → OR force reconnection via deauthentication (Step 4)

    STEP 4 — Force handshake capture (deauthentication attack):
      aireplay-ng -0 5 -a AA:BB:CC:DD:EE:FF -c CLIENT_MAC wlan0mon
      -0 5       → send 5 deauthentication frames
      -a         → target AP BSSID
      -c         → target client MAC
      → Client disconnects → reconnects → handshake captured
      → airodump-ng shows: "WPA handshake: AA:BB:CC:DD:EE:FF"

    STEP 5 — Verify handshake captured:
      aircrack-ng wpa_capture.cap
      → Should show: "1 handshake"

    STEP 6 — Dictionary attack against captured handshake:
      aircrack-ng -w /usr/share/wordlists/rockyou.txt \
                  -b AA:BB:CC:DD:EE:FF wpa_capture.cap
      -w     → wordlist path
      -b     → target AP BSSID
      → Tests each password from rockyou.txt
      → If password is in wordlist: "KEY FOUND! [password]"

    STEP 7 — GPU-accelerated cracking (much faster):
      hashcat -m 2500 wpa_capture.hccapx rockyou.txt
      -m 2500   → WPA/WPA2 hash mode
      → GPU processes millions of candidates per second

**Converting cap to hashcat format:**

    hcxpcapngtool -o hash.hc22000 wpa_capture.cap
    hashcat -m 22000 hash.hc22000 rockyou.txt

---

### 3.7 PMKID Attack

**WHAT:**
The PMKID attack (discovered by Jens Steube in 2018) is a
method of cracking WPA2-PSK **without capturing the four-way
handshake** — requiring only a single EAPOL frame from the AP.

**HOW:**

    PMKID = HMAC-SHA1(PMK, "PMK Name" || AP_MAC || Client_MAC)

    The PMKID is included by the AP in the RSNE of the
    first EAPOL frame (Message 1 of the four-way handshake)
    Attacker requests association → receives EAPOL frame → extracts PMKID

    Cracking:
    For each candidate password:
      PMK = PBKDF2(password, SSID, 4096, 256)
      PMKID_candidate = HMAC-SHA1(PMK, "PMK Name" || AP_MAC || Client_MAC)
      If PMKID_candidate == captured_PMKID → password found

**Why PMKID attack is significant:**
- No need to wait for a client to connect
- No deauthentication needed
- Works even when no clients are currently connected
- Single frame from AP is sufficient
- Faster to obtain than full four-way handshake capture

**Tools:**

    hcxdumptool -i wlan0mon -o pmkid_capture.pcapng \
                --enable-status=1
    hcxpcapngtool -o hash.hc22000 pmkid_capture.pcapng
    hashcat -m 22000 hash.hc22000 rockyou.txt

---

### 3.8 WPS Vulnerability

**WHAT:**
WPS (Wi-Fi Protected Setup) was introduced in 2007 to simplify
connecting devices to WPA/WPA2 networks without entering the
full password — using either a physical push button or an 8-digit PIN.

**The WPS PIN Vulnerability (2011 — Stefan Viehböck):**

    WPS PIN: 8 digits = 10^8 = 100,000,000 combinations
    BUT: AP validates PIN in TWO HALVES:
      First 4 digits validated separately → 10^4 = 10,000 combinations
      Last 3 digits validated separately (last digit is checksum) → 10^3 = 1,000 combinations
      Total: 10,000 + 1,000 = 11,000 attempts maximum

    Most APs process WPS in 1–2 seconds per attempt
    11,000 attempts × 2 seconds = ~6 hours maximum to recover PIN
    Once PIN found → recover full WPA2 password

**Pixie Dust Attack (2014 — Dominique Bongard):**
Many AP chipsets generate weak random numbers for WPS nonce values.
Pixie Dust exploits this — recovers WPS PIN in **seconds** by
solving for the offline computation rather than brute forcing.

**Tools:**

    reaver -i wlan0mon -b AP_BSSID -vv          ← WPS PIN brute force
    wash -i wlan0mon                              ← Discover WPS-enabled APs
    bully -b AP_BSSID -c 6 wlan0mon             ← Alternative to reaver
    pixiewps                                      ← Pixie Dust offline attack

**WPS countermeasure:**
**Disable WPS entirely** on all access points — there is no
security patch that fully resolves the fundamental design flaw.

---

## Section 4 — WPA3

### 4.1 WPA3 Personal — SAE

**WHAT:**
WPA3 Personal (introduced 2018, mandatory for Wi-Fi 6 devices)
replaces WPA2-PSK's Pre-Shared Key exchange with **SAE
(Simultaneous Authentication of Equals)** — also called
**Dragonfly Key Exchange**.

**WPA3-SAE improvements over WPA2-PSK:**

| Property | WPA2-PSK | WPA3-SAE |
|---|---|---|
| **Key exchange** | Pre-Shared Key (static) | SAE (Dragonfly) |
| **Offline dictionary attack** | ✅ Possible (capture handshake) | ❌ Much harder (see Dragonblood) |
| **Forward secrecy** | ❌ No — one key compromise decrypts all past traffic | ✅ Yes — per-session unique keys |
| **PMKID attack** | ✅ Vulnerable | ❌ Not applicable |
| **Deauth capture attack** | ✅ Captures handshake | ❌ SAE handshake resistant |
| **Password visible over air** | ❌ (captured handshake reveals password via offline attack) | ❌ (SAE is zero-knowledge proof) |

**How SAE/Dragonfly works (simplified):**

    Both AP and client independently derive a shared secret
    using the password — without transmitting any value
    that allows offline computation

    Uses Elliptic Curve Diffie-Hellman Ephemeral (ECDHE):
    - Each session generates fresh ephemeral keys
    - Even capturing multiple SAE exchanges does not enable offline dictionary attack
    - Even if attacker learns future key → cannot decrypt past sessions (forward secrecy)

**Forward Secrecy:**
WPA3's most critical improvement. If an attacker records encrypted
WPA2 traffic today, and later discovers the WPA2 password, they
can decrypt ALL previously recorded traffic. WPA3's per-session
fresh keys mean past traffic cannot be decrypted even with the password.

---

### 4.2 WPA3 Enterprise

- Uses **192-bit security suite** (compared to WPA2 Enterprise's minimum 128-bit)
- Requires GCMP-256 encryption, HMAC-SHA384 for key derivation
- Mandatory mutual authentication (AP must authenticate to client too)
- Suitable for government and high-security enterprise environments

---

### 4.3 WPA3 Vulnerabilities

**Dragonblood Attacks (2019 — Vanhoef and Ronen):**
Despite SAE's theoretical strength, implementation flaws were found:

| Attack | Mechanism | Impact |
|---|---|---|
| **Cache-based side-channel** | Observe cache access patterns during SAE → infer password bits | Offline dictionary attack possible |
| **Timing-based side-channel** | Measure computation time during SAE → infer password bits | Offline dictionary attack possible |
| **SAE Downgrade** | Force device to use WPA2 instead of WPA3 (in transition mode) | WPA2 attacks now applicable |
| **EAP Downgrade** | Force weaker EAP method in Enterprise mode | Reduces authentication strength |

**Status:** Wi-Fi Alliance released patches in April 2019.
Updated implementations address most Dragonblood vulnerabilities.
WPA3 remains significantly stronger than WPA2 when properly implemented.

---

## Section 5 — Wireless Sniffers and Locating SSIDs

### 5.1 Wireless Sniffing — Monitor Mode

**WHAT:**
Wireless sniffing captures 802.11 frames from the air — including
frames not addressed to the sniffer's device. Requires the wireless
adapter to be placed in **monitor mode** (also called RFMON mode).

**Monitor mode vs Promiscuous mode:**

| Property | Promiscuous Mode (wired) | Monitor Mode (wireless) |
|---|---|---|
| **Layer** | Layer 2 (Ethernet) | Layer 1/2 (802.11 radio) |
| **Association required?** | N/A — wired | ❌ No — captures without joining network |
| **What is captured** | All Ethernet frames on segment | ALL 802.11 frames — management, control, data |
| **Includes management frames?** | N/A | ✅ Beacons, probes, deauth frames |
| **Enable command** | `ifconfig eth0 promisc` | `airmon-ng start wlan0` |

**Enable monitor mode:**

    airmon-ng check kill         ← stop interfering processes (NetworkManager, wpa_supplicant)
    airmon-ng start wlan0        ← create wlan0mon in monitor mode

    Alternative (iw):
    ip link set wlan0 down
    iw wlan0 set monitor control
    ip link set wlan0 up

**Lock to specific channel:**

    iwconfig wlan0mon channel 6
    OR
    airodump-ng --channel 6 wlan0mon

---

### 5.2 Passive vs Active Wireless Discovery

| Approach | Method | Legality | What It Finds |
|---|---|---|---|
| **Passive** | Capture beacon frames — no transmission | Lower legal risk | APs broadcasting SSID, BSSID, channel, encryption |
| **Active (Probe Requests)** | Send broadcast probe requests | Some legal risk | All APs including those not currently beaconing |
| **Active (Directed Probes)** | Send probe request for specific SSID | Used by clients normally | Hidden APs with known SSID |

**Passive discovery via beacons:**
Every AP broadcasts beacon frames ~10 times per second.
Simply listening in monitor mode reveals all non-hidden SSIDs
in range — no transmission required.

**Active discovery for hidden SSIDs:**

    Hidden AP still sends beacons — but with SSID field empty or zeroed
    Hidden AP reveals SSID in:
    - Probe Response frames (when client sends directed probe)
    - Association Request frames (client must know SSID to associate)

    To discover hidden SSID:
    1. Passive: wait for existing client to probe/associate
       airodump-ng wlan0mon → shows "<length: 10>" for hidden SSID
       Wait for station to send probe → SSID revealed in capture

    2. Active: send deauthentication to force client to re-probe
       aireplay-ng -0 1 -a HIDDEN_AP_BSSID -c CLIENT_MAC wlan0mon
       → Client reconnects → probe request reveals SSID

---

### 5.3 Wireless Sniffing Tools

| Tool | Platform | Purpose |
|---|---|---|
| **airodump-ng** | Linux | AP/client discovery and packet capture — part of aircrack-ng suite |
| **Wireshark** | Cross-platform | Deep packet analysis of captured 802.11 frames |
| **Kismet** | Linux/macOS | Passive wireless sniffer + IDS — no transmission |
| **inSSIDer** | Windows/macOS | Wi-Fi scanner — channel visualization |
| **NetStumbler** | Windows | Legacy wireless scanner (active probing) |
| **Ekahau** | Cross-platform | Professional wireless site survey tool |
| **hcxdumptool** | Linux | PMKID and handshake capture — modern replacement |
| **tcpdump** | Linux | Command-line packet capture (wireless with monitor mode) |

**Kismet — Key features:**
- Completely passive — no transmission
- Detects hidden SSIDs by monitoring probe responses
- Client tracking — which clients probe for which SSIDs
- Detects rogue APs and evil twins
- GPS integration for wardriving

**airodump-ng output explained:**

     BSSID              PWR  Beacons  #Data  CH   MB   ENC   CIPHER  AUTH ESSID
     AA:BB:CC:DD:EE:FF  -45    1200     543   6   54e  WPA2  CCMP    PSK  HomeNetwork
     11:22:33:44:55:66  -72     890      12   1   54   WEP   WEP     OPN  OldOffice
     77:88:99:AA:BB:CC  -65     200       0  11  130   WPA2  CCMP    PSK  <length: 8>

    PWR = Signal strength (closer to 0 = stronger)
    #Data = Encrypted data packets captured
    ENC = Encryption type
    <length: 8> = Hidden SSID with 8 characters

---

### 5.4 Locating SSIDs — Hidden Networks

**WHAT:**
SSID hiding (also called SSID cloaking) suppresses the SSID
from AP beacon frames — the AP does not advertise its name.
This is a common misconfigured "security measure."

**Why it fails as a security control:**

    Problem 1: AP still responds to directed probe requests
    Any client that knows the SSID can still associate normally.

    Problem 2: Existing clients reveal the SSID
    When a client searches for the hidden network, it sends
    directed probe requests containing the SSID in plaintext.
    airodump-ng captures these → SSID revealed.

    Problem 3: Association requests contain SSID
    When any client joins the hidden network, the association
    request frame contains the SSID in plaintext.

    Problem 4: Tools detect empty beacon as hidden network
    airodump-ng shows "<length: N>" immediately — alerting
    attackers that a hidden network exists.

> [!NOTE]
> Hiding an SSID is equivalent to hiding your house address
> by removing it from maps — but still telling everyone you
> visit where your house is. The address is hidden from
> casual observers but revealed every time you use it.

---

### 5.5 Wardriving

**WHAT:**
Wardriving is the act of driving (or walking — warwalking)
through an area while scanning for wireless networks —
using a laptop, smartphone, or dedicated device with GPS
and wireless capture software.

**Purpose:**
- **Attacker:** Map vulnerable networks (WEP, open, default passwords)
  in an area before targeting specific locations
- **Researcher:** Survey wireless security landscape — academic studies
- **Administrator:** Audit own organization's wireless footprint

**Tools:**
- **Kismet** — passive capture + GPS logging
- **airodump-ng** — with GPS (gpsd integration)
- **WiGLE** (Wireless Geographic Logging Engine) — crowd-sourced
  global wireless network database at wigle.net
- **Vistumbler** — Windows wardriving tool

**Legal status:**
Wardriving itself (passive scanning) is generally legal in most
jurisdictions — it is passive reception of broadcast signals.
Connecting to or accessing any discovered network without
authorization is illegal under:
- India: IT Act 2000 Section 43(a), 66
- USA: CFAA
- UK: Computer Misuse Act

---

## Section 6 — MAC Spoofing on Wireless Networks

### 6.1 What Is MAC Spoofing

**WHAT:**
MAC spoofing is changing the hardware MAC address of a network
interface to a different value — typically to impersonate an
authorized device, bypass MAC filtering, or anonymize network activity.

**Why MAC addresses are easily spoofed:**
MAC addresses were never designed as security identifiers —
they are hardware labels for device identification. The OS allows
changing the MAC in software at any time. No cryptographic
binding exists between a device and its MAC address.

**Critical wireless MAC spoofing insight:**
On wireless networks, MAC addresses are **transmitted in cleartext
in every 802.11 frame header** — even when data is WPA2-encrypted.
A passive sniffer can extract the MAC addresses of all authorized
clients without associating with or decrypting the network.

---

### 6.2 MAC Spoofing Attack Flow

    SCENARIO: Target network uses MAC filtering — only allows
    devices whose MACs are in the allowed list.

    STEP 1 — Enable monitor mode:
      airmon-ng start wlan0

    STEP 2 — Discover target network and its clients:
      airodump-ng --bssid TARGET_AP_BSSID wlan0mon
      → STATION column shows all client MACs: 11:22:33:44:55:66

    STEP 3 — Identify an authorized client MAC:
      Observe which clients are connected to the target AP
      Note their MAC addresses from STATION column

    STEP 4 — Change attacker's MAC to match authorized client:
      ip link set wlan0 down
      ip link set wlan0 address 11:22:33:44:55:66
      ip link set wlan0 up
      → Attacker's NIC now presents as authorized device

    STEP 5 — Connect to network:
      AP sees MAC 11:22:33:44:55:66 → checks allowed list → grants access
      MAC filtering completely bypassed

**Note:** If the legitimate client is still connected, both devices
will have the same MAC — causing a collision. Attacker may first
deauthenticate the legitimate client.

---

### 6.3 MAC Spoofing Tools

| Method | Command |
|---|---|
| **ip command (Linux)** | `ip link set wlan0 address XX:XX:XX:XX:XX:XX` |
| **ifconfig (Linux)** | `ifconfig wlan0 hw ether XX:XX:XX:XX:XX:XX` |
| **macchanger** | `macchanger -m XX:XX:XX:XX:XX:XX wlan0` |
| **macchanger (random)** | `macchanger -r wlan0` |
| **Windows Device Manager** | Network adapter properties → Advanced → Network Address |

---

### 6.4 MAC Filtering — False Security

**Why MAC filtering is not a security control:**

| Claim | Reality |
|---|---|
| "Only authorized MACs can connect" | MAC addresses are transmitted in plaintext — any passive sniffer collects all authorized MACs |
| "Attackers cannot see authorized MACs without joining" | False — 802.11 frames are always in plaintext at Layer 2 — monitor mode reveals all MACs |
| "Changing MAC requires physical device access" | False — MAC can be changed in software in seconds with a single command |
| "MAC filtering adds a layer of security" | It adds an inconvenience of ~30 seconds to a motivated attacker — not meaningful security |

> [!IMPORTANT]
> **MAC filtering provides ZERO security against any attacker
> with basic wireless tools.** It only prevents accidental
> unauthorized access (e.g., a neighbor who doesn't know how
> to spoof MACs). Do not rely on MAC filtering for security.
> Use WPA3 or WPA2 with a strong password instead.

---

## Section 7 — Wireless Attack Techniques

### 7.1 Evil Twin Attack

**WHAT:**
An evil twin attack creates a **rogue AP with the same SSID**
(and optionally same BSSID) as a legitimate AP — typically with
a stronger signal — causing clients to connect to the attacker's
AP instead of the real one.

**HOW:**

    STEP 1 — Discover target AP:
      airodump-ng wlan0mon
      → Target: SSID="CoffeeShop_WiFi" BSSID=AA:BB:CC:DD:EE:FF CH=6

    STEP 2 — Create evil twin AP (hostapd):
      hostapd config:
        interface=wlan1
        ssid=CoffeeShop_WiFi      ← same SSID
        channel=6                  ← same channel
        bssid=AA:BB:CC:DD:EE:FF   ← spoofed BSSID (optional)

    STEP 3 — Boost signal power:
      Evil twin AP broadcasts at higher power than real AP
      Clients prefer strongest signal → connect to evil twin

    STEP 4 — Deauthenticate clients from real AP (optional):
      aireplay-ng -0 0 -a REAL_AP_BSSID wlan0mon
      → Continuous deauth → clients cannot stay on real AP
      → Only evil twin available → clients connect to evil twin

    STEP 5 — DHCP and internet routing:
      Evil twin runs DHCP server → assigns IP to client
      Routes client traffic through attacker → internet
      Client has internet → doesn't suspect anything

    STEP 6 — Capture credentials:
      All HTTP traffic visible to attacker
      DNS can be spoofed → redirect to phishing pages
      HTTPS: attacker deploys captive portal
      → Victim sees login page asking for Wi-Fi password
      → Victim enters password → attacker captures it

**Captive portal attack:**
Evil twin may not know the WPA2 password. After connecting clients:
- Redirect all traffic to a fake login page claiming "re-enter Wi-Fi password to continue"
- Victim enters real WPA2 password → attacker captures it
- Attacker now has the real network password + real-time MITM position

**Tools:**
- **hostapd** — create software AP
- **airbase-ng** — alternative AP creation
- **Bettercap** — evil twin + MITM automation
- **Wifiphisher** — automated evil twin + phishing attack framework
- **MANA** toolkit — advanced evil twin attack

---

### 7.2 Rogue Access Point

**WHAT:**
A rogue AP is any **unauthorized wireless access point** connected
to an organization's wired network — providing wireless access
to the network without IT approval or security controls.

**Distinction from Evil Twin:**

| Property | Evil Twin | Rogue AP |
|---|---|---|
| **Impersonates legitimate AP?** | ✅ Yes — same SSID/BSSID | ❌ Not necessarily |
| **Connected to wired network?** | ❌ Usually not | ✅ Yes — key characteristic |
| **Purpose** | Intercept wireless client traffic | Unauthorized wireless access to wired network |
| **Planted by** | External attacker | Insider, negligent employee |
| **Threat** | Client credential theft | Bypass perimeter security → access internal network |

**Rogue AP scenario:**
Employee plugs a cheap wireless router into an ethernet port →
creates an open wireless network → external attacker in parking lot
connects → has direct access to internal corporate network —
bypassing all perimeter firewalls and VPN requirements.

**Detection:**
- Wireless IDS (Kismet, Cisco WCS) monitoring for unauthorized BSSIDs
- 802.1X port authentication on all switch ports
- Regular wireless site surveys
- SNMP monitoring of switch port activity

---

### 7.3 Deauthentication Attack

**WHAT:**
A deauthentication attack sends **forged 802.11 deauthentication
management frames** impersonating the legitimate AP — causing
victim clients to disconnect from the network.

**WHY it works:**
802.11 management frames (including deauthentication and
disassociation frames) are **NOT authenticated or encrypted**
in WPA/WPA2. Any device can forge these frames — there is no
cryptographic verification that a deauthentication frame came
from the real AP.

**Uses:**
1. **Handshake capture**: Deauth forces client to reconnect →
   captures WPA handshake during reconnection
2. **Evil twin preparation**: Force all clients off real AP →
   clients connect to evil twin with stronger signal
3. **Wireless DoS**: Continuously deauthenticate clients → deny service
4. **Hidden SSID discovery**: Deauth client → client sends probe
   request with hidden SSID → SSID revealed

**Command:**

    aireplay-ng -0 5 -a AP_BSSID -c CLIENT_MAC wlan0mon
    -0   → deauthentication attack
    5    → number of deauth frames to send
    -a   → target AP BSSID (source of spoofed frames)
    -c   → target client MAC (unicast) — omit for broadcast

    Broadcast deauth (affects all clients):
    aireplay-ng -0 0 -a AP_BSSID wlan0mon
    -0 0 → continuous deauth (0 = infinite)

**Fix — 802.11w (Management Frame Protection):**
802.11w (PMF — Protected Management Frames) — optional in WPA2,
mandatory in WPA3 — cryptographically protects management frames
including deauthentication. Forged deauth frames are detected and
discarded. WPA3 makes deauthentication attacks largely ineffective.

---

### 7.4 KRACK Attack

**WHAT:**
KRACK (Key Reinstallation Attack) was disclosed in October 2017
by Mathy Vanhoef. It exploits a vulnerability in the **four-way
handshake** of WPA2 — forcing nonce (random number) reuse in the
cryptographic key derivation process.

**HOW:**

    Normal four-way handshake:
    ANonce and SNonce are used ONCE → fresh PTK derived → encrypted comms

    KRACK manipulation:
    Attacker positions as MITM between client and AP
    Attacker retransmits Message 3 of handshake (encrypted GTK)
    Client receives retransmitted message → reinstalls PTK
    → Resets nonce counter to previously used value
    → Nonce reuse with same key → cryptographic weakness

    Impact:
    - AES-CCMP: Replay and decryption of traffic
    - TKIP: Replay, decryption, AND forgery of packets
    - GCMP: Bidirectional key recovery

**Severity and patching:**
- CVSS: 8.1 (High)
- ALL WPA2 implementations were vulnerable (protocol-level flaw)
- Patches released October 2017 by Microsoft, Apple, Linux, Android
- Fully patched devices are not vulnerable
- WPA3 SAE is not vulnerable to KRACK (different handshake design)

---

### 7.5 Wireless DoS Attacks

| Attack | Mechanism | Layer |
|---|---|---|
| **Deauthentication flood** | Continuous forged deauth frames | Layer 2 management |
| **Disassociation flood** | Continuous forged disassoc frames | Layer 2 management |
| **Beacon flood** | Flood fake AP beacons → overwhelm client AP scanning | Layer 2 management |
| **RF jamming** | Transmit on same frequency → radio interference | Layer 1 physical |
| **SSID conflict** | Multiple APs same SSID on same channel → interference | Layer 2 |
| **Authentication flood** | Flood AP with auth requests → exhaust association table | Layer 2 management |
| **CTS attack** | Forge CTS frames → all devices defer → channel unusable | Layer 2 control |

**RF jamming note:**
Physical radio jamming (transmitting continuous interference signal
on 2.4GHz or 5GHz) is illegal in virtually all jurisdictions —
it constitutes interference with licensed radio spectrum.
In India: Wireless Telegraphy Act 1933 — unauthorized radio
transmission is a criminal offence regardless of intent.

---

## Section 8 — Methods to Secure Wireless Networks

### 8.1 Encryption Standards Comparison

| Protocol | Year | Encryption | Key Exchange | Status |
|---|---|---|---|---|
| **WEP** | 1997 | RC4 + 24-bit IV | Shared static key | ❌ Broken — do not use |
| **WPA (TKIP)** | 2003 | RC4 + TKIP | PSK or 802.1X | ❌ Deprecated — do not use |
| **WPA2 (CCMP)** | 2004 | AES-128 CCMP | PSK or 802.1X | ⚠️ Acceptable with strong PSK |
| **WPA3 Personal** | 2018 | AES-128/256 | SAE (Dragonfly) | ✅ Recommended |
| **WPA3 Enterprise** | 2018 | AES-256 GCMP | 802.1X + EAP-TLS | ✅ Highest security |

> [!IMPORTANT]
> Security hierarchy (strongest to weakest):
> **WPA3 Enterprise > WPA3 Personal > WPA2 Enterprise > WPA2 Personal > WPA > WEP > Open**

---

### 8.2 Authentication Controls

| Control | Implementation | What It Prevents |
|---|---|---|
| **WPA3 Personal (SAE)** | Configure on AP — all devices need WPA3 support | Offline dictionary attack, PMKID attack |
| **WPA2 Personal + Strong PSK** | Minimum 20 random characters — not dictionary words | Dictionary attack (makes it infeasible) |
| **WPA2/WPA3 Enterprise (802.1X)** | RADIUS server — per-user certificates or credentials | Shared password risk — individual credential management |
| **EAP-TLS** | Client + server certificates | Phishing, credential theft — mutual auth required |
| **Disable WPS** | AP admin panel → disable WPS | WPS PIN brute force, Pixie Dust |
| **802.11w (PMF)** | Enable Protected Management Frames on AP | Deauthentication attacks, management frame forgery |
| **MFA for wireless access** | RADIUS + MFA integration | Credential-only compromise |

---

### 8.3 Network-Level Controls

| Control | What It Does |
|---|---|
| **Wireless IDS (Kismet, Cisco WCS)** | Detect rogue APs, evil twins, deauth floods, unusual probe patterns |
| **Rogue AP detection** | Monitor for unauthorized BSSIDs on corporate network |
| **802.1X on switch ports** | Authenticate wired devices — prevents unauthorized AP plugging |
| **Network segmentation (VLAN)** | Isolate wireless from wired internal network — DMZ for Wi-Fi |
| **VPN over Wi-Fi** | Encrypt all traffic at VPN layer — protects even on evil twin |
| **DNS filtering** | Block malicious domains even if MITM redirects DNS |
| **HTTPS everywhere + HSTS** | Protect against MITM even if connected to evil twin |
| **Certificate pinning** | Mobile apps reject unexpected certificates — evil twin detection |
| **Site surveys** | Regular audits of wireless coverage — detect unauthorized APs |

---

### 8.4 Physical and Administrative Controls

| Control | Detail |
|---|---|
| **Reduce AP transmit power** | Limit signal to necessary coverage area — reduce exposure beyond building |
| **AP placement** | Position APs centrally — minimize signal leakage outside controlled area |
| **Faraday cage / RF shielding** | Block radio signals from leaving sensitive areas |
| **Acceptable use policy** | Prohibit connecting personal APs to corporate network |
| **Regular security audits** | Wardriving / wireless site surveys quarterly |
| **Employee awareness** | Train users to verify SSID before connecting — report suspicious portals |
| **Guest network isolation** | Separate SSID and VLAN for guests — no access to corporate resources |
| **AP firmware updates** | Patch KRACK, WPS, and other firmware vulnerabilities regularly |
| **Physical AP security** | Lock AP in ceiling/wall mount — prevent physical reset/tampering |

---

## 📌 Extra Notes

### E1 — RC4 Stream Cipher and IV Weakness Deep Dive

> [!NOTE]
> Understanding WHY RC4+IV is broken explains all WEP attacks —
> essential for exam questions asking about the root cause.

**RC4 Stream Cipher:**
RC4 generates a pseudorandom keystream from an input key.
XOR of plaintext with keystream = ciphertext.
Same key → same keystream → XOR of two same-key ciphertexts
= XOR of plaintexts (key cancels out) — catastrophic if key reused.

**The IV problem in WEP:**

    WEP encryption key: IV (24-bit) || WEP_KEY (40 or 104 bit)
    24-bit IV = only 16,777,216 unique values

    On a busy network generating 1,500 packets/second:
    Time to exhaust all IVs: 16,777,216 / 1,500 = ~3 hours
    But birthday collision (50% probability): ~√(2 × 16,777,216) ≈ 4,096 packets

    Once two packets share same IV:
    C1 = P1 XOR RC4(IV || KEY)
    C2 = P2 XOR RC4(IV || KEY)
    C1 XOR C2 = P1 XOR P2
    → XOR of two known-format plaintexts (IP headers are predictable) → both recovered

**FMS Attack (Fluhrer, Mantin, Shamir — 2001):**
Certain IVs (called "weak IVs") of the form (A+3, 255, X) in RC4
cause the first bytes of the keystream to leak information about
the secret key. Statistical analysis of ~400,000 frames containing
weak IVs recovers the WEP key byte by byte. This is the basis of
aircrack-ng's PTW (Pyshkin, Tews, Weinmann) attack — which is
even more efficient (requires only ~35,000 frames with ARP packets).

---

### E2 — TKIP vs CCMP vs GCMP

> [!NOTE]
> TKIP, CCMP, and GCMP are the three cipher suites used across
> WPA generations — frequently tested in MCQs.

| Property | TKIP | CCMP | GCMP |
|---|---|---|---|
| **Used in** | WPA (also WPA2 backward compat) | WPA2 (mandatory), WPA3 | WPA3 Enterprise, Wi-Fi 6 |
| **Base cipher** | RC4 | AES | AES |
| **Mode** | Per-packet key mixing | Counter Mode + CBC-MAC | Galois/Counter Mode |
| **Key size** | 128-bit (per-packet derived) | 128-bit | 128 or 256-bit |
| **IV size** | 48-bit | 48-bit packet number | 48-bit |
| **Integrity** | Michael MIC (64-bit) | CBC-MAC (integrated) | GHASH (integrated) |
| **Security** | Moderate — RC4 weaknesses | Strong | Strongest |
| **Status** | Deprecated (2012) | Current standard | Latest — WPA3 Enterprise |

> [!IMPORTANT]
> CCMP is the mandatory cipher for WPA2 certification.
> TKIP is only included for backward compatibility with WPA devices.
> A WPA2 network configured to allow TKIP clients is vulnerable
> to TKIP-specific attacks — configure WPA2 to CCMP-only.

---

### E3 — 802.1X EAP Methods

> [!NOTE]
> EAP method comparison is tested when questions ask which method
> provides the strongest enterprise wireless authentication.

| Method | Client Auth | Server Auth | Tunnel | Strength | Use Case |
|---|---|---|---|---|---|
| **EAP-TLS** | Certificate | Certificate | TLS | ⭐⭐⭐⭐⭐ | Enterprise — highest security |
| **EAP-PEAP** | Password | Certificate | TLS | ⭐⭐⭐⭐ | Enterprise — most common |
| **EAP-TTLS** | Password/cert | Certificate | TLS | ⭐⭐⭐⭐ | Enterprise — flexible |
| **EAP-FAST** | PAC or cert | PAC or cert | TLS | ⭐⭐⭐ | Cisco alternative to LEAP |
| **LEAP** | Password | Password | None | ⭐ | Broken — Cisco legacy |
| **EAP-MD5** | MD5 hash | None | None | ⭐ | Deprecated — no server auth |

> [!IMPORTANT]
> **EAP-TLS** is the gold standard — requires BOTH client AND server
> certificates — provides mutual authentication. Even if the RADIUS
> server is compromised, EAP-TLS prevents phishing because clients
> will not authenticate to servers without valid certificates.
>
> **LEAP** (Cisco's proprietary EAP) is completely broken — use of
> ASLEAP tool recovers credentials from captured LEAP exchanges.
> Never deploy LEAP.

---

### E4 — Aircrack-ng Suite — Full Reference

> [!NOTE]
> The aircrack-ng suite is the primary wireless attack toolkit —
> know each tool's specific function.

| Tool | Function | Key Options |
|---|---|---|
| **airmon-ng** | Enable/disable monitor mode | `start wlan0`, `stop wlan0mon`, `check kill` |
| **airodump-ng** | Packet capture + AP/client discovery | `-c channel`, `--bssid`, `-w file` |
| **aireplay-ng** | Packet injection attacks | `-0` deauth, `-1` fake auth, `-2` replay, `-3` ARP replay |
| **aircrack-ng** | WEP/WPA key cracking | `-w wordlist`, `-b bssid` |
| **airbase-ng** | Create software AP (evil twin) | `--essid`, `-c channel` |
| **airdecap-ng** | Decrypt captured WEP/WPA traffic | `-w key` (WEP), `-p password` (WPA) |
| **airtun-ng** | Create virtual tunnel interface | Virtual network testing |
| **airserv-ng** | Network-accessible card sharing | Remote wireless card sharing |
| **besside-ng** | Automated WEP/WPA cracking | Minimal user interaction |
| **packetforge-ng** | Craft arbitrary 802.11 packets | Custom frame injection |

**Key aireplay-ng attack modes:**

| Mode | Flag | Attack |
|---|---|---|
| Deauthentication | `-0` | Force client disconnection |
| Fake authentication | `-1` | Associate with AP without key |
| Interactive replay | `-2` | Replay captured packets |
| ARP request replay | `-3` | Replay ARP to generate IVs (WEP) |
| Chopchop attack | `-4` | Decrypt WEP packet without key |
| Fragmentation attack | `-5` | Obtain PRGA from single packet |
| Café latte attack | `-6` | WEP attack against isolated client |
| Deauthentication (directed) | `-7` | Inject deauth to disconnect client |
| WPA MIC exploitation | `-9` | WPA TKIP Michael MIC exploit |

---

### E5 — Evil Twin vs Rogue AP vs Karma Attack

> [!NOTE]
> These three related attacks are frequently confused in MCQs.

| Property | Evil Twin | Rogue AP | Karma Attack |
|---|---|---|---|
| **SSID** | Clones legitimate AP SSID | Any SSID (may not match existing) | Responds to ANY client probe request SSID |
| **Target** | Wireless clients of specific network | Wired network access | Any client probing for any remembered network |
| **Physical connection** | No wired connection needed | Connected to wired network | No wired connection needed |
| **Goal** | MITM client traffic | Bypass perimeter into wired network | MITM any nearby mobile device |
| **How clients connect** | Same SSID + higher signal | Clients connect by choice | Clients auto-connect to "remembered" network |
| **Tools** | hostapd, Wifiphisher | Standard wireless router | MANA toolkit, hostapd-wpe |

**Karma Attack detail:**
Mobile devices continuously send probe requests for networks they
have previously connected to ("Home_WiFi", "Starbucks", "Airport_Free").
The Karma attack creates an AP that responds positively to ANY
probe request — regardless of the SSID requested. The client's
phone believes it found its remembered "Home_WiFi" or "Starbucks" →
connects automatically → MITM without any specific targeting.

---

### E6 — Dragonblood — WPA3 Vulnerabilities

> [!NOTE]
> Dragonblood is the significant WPA3 vulnerability disclosure —
> know the mechanism and current status.

**Researchers:** Mathy Vanhoef (discovered KRACK) and Eyal Ronen
**Year:** April 2019

**Vulnerability 1 — Timing Side-Channel:**

    SAE commit phase involves operations on elliptic curve points
    The time taken varies based on the password being tested
    An attacker observing response timing can determine IF a
    password candidate is "close" to the real password
    → Allows offline dictionary attack with ~8× fewer guesses
    than brute force

**Vulnerability 2 — Cache Side-Channel:**

    On systems with shared CPU cache (e.g., shared hosting, VMs):
    SAE implementation accesses memory in password-dependent pattern
    Attacker on same system observes cache access patterns
    → Leaks information about password structure
    → Enables offline dictionary attack

**Vulnerability 3 — Downgrade Attack:**

    WPA3 Transition Mode (supports both WPA2 and WPA3 clients):
    Attacker forces WPA3 client to use WPA2 protocol
    → WPA2 four-way handshake exposed
    → Normal WPA2 offline dictionary attack now applicable

**Response:**
Wi-Fi Alliance released security advisories and patches.
Updated aircrack-ng and hostapd implementations mitigate the
side-channel attacks. Dragonblood raises WPA3's bar significantly
but does not completely eliminate offline cracking possibility
against weak passwords on unpatched implementations.

---

### E7 — Predecessor / Successor Chains

> [!NOTE]
> Understanding the evolution of wireless security shows why
> each successor protocol was developed.

**Wireless Encryption Evolution:**

    No security (open networks) — 802.11 original (1997)
            ↓
    WEP (Wired Equivalent Privacy) — 1997
    → Broken by FMS attack (2001)
    → Broken by PTW attack (2004) — aircrack-ng
            ↓
    WPA (Wi-Fi Protected Access) — 2003
    → TKIP+RC4 — firmware-upgradeable fix for WEP hardware
    → TKIP cracking attacks (Beck-Tews, 2008)
    → Deprecated 2012
            ↓
    WPA2 — 2004 (mandatory certification 2006)
    → AES-CCMP — genuinely strong encryption
    → KRACK attack (2017) — key reinstallation
    → PMKID attack (2018) — no handshake capture needed
    → Still widely deployed — acceptable with strong PSK
            ↓
    WPA3 — 2018 (mandatory for Wi-Fi 6 certification)
    → SAE (Dragonfly) — replaces PSK for Personal mode
    → Dragonblood vulnerabilities (2019) — side-channel
    → 802.11w PMF — mandatory — protects management frames
            ↓
    Wi-Fi Enhanced Open (OWE) — 2018
    → Opportunistic Wireless Encryption for open networks
    → Encrypts open Wi-Fi without authentication
            ↓
    WPA3 with 802.11be (Wi-Fi 7) — 2024+

**Wireless Hacking Tool Evolution:**

    NetStumbler (2000) — Windows AP scanner (active)
            ↓
    Kismet (2001) — Linux passive wireless IDS
            ↓
    Aircrack (2004) → Aircrack-ng (2006) — WEP/WPA suite
            ↓
    Reaver (2011) — WPS PIN brute force
            ↓
    Wifiphisher (2015) — evil twin automation
            ↓
    hcxdumptool + hcxpcapngtool (2018) — PMKID capture
            ↓
    Bettercap (2019+) — modern MITM framework

---

### E8 — Terminology Traps

| Term | Trap | Clarification |
|---|---|---|
| **WEP 128-bit is stronger than WEP 64-bit** | "More bits = more security for WEP" | BOTH ARE BROKEN. The IV weakness affects all WEP variants equally regardless of key length. 128-bit WEP is cracked only marginally slower than 64-bit. |
| **WPA2 cracking breaks AES** | "WPA2 was cracked — AES is broken" | WPA2 cracking attacks the KEY ESTABLISHMENT (four-way handshake) and PSK password — NOT the AES cipher. AES itself remains unbroken. |
| **Hiding SSID prevents network discovery** | "Hidden SSID = invisible network" | Hidden SSIDs are revealed in probe requests from existing clients and association requests. airodump-ng shows them immediately as `<length: N>`. |
| **MAC filtering is a valid security control** | "MAC filtering adds a layer of security" | MAC addresses are transmitted in plaintext in every 802.11 frame — trivially captured and spoofed in under 30 seconds. Provides no meaningful security. |
| **WPA3 is uncrackable** | "Upgrade to WPA3 = no more cracking" | Dragonblood (2019) demonstrated timing and cache side-channel attacks against WPA3 SAE. Weak passwords are still vulnerable on unpatched implementations. |
| **Evil twin and rogue AP are the same** | "Any unauthorized AP = evil twin" | Evil twin CLONES a specific legitimate AP (same SSID/BSSID). Rogue AP is ANY unauthorized AP — may not impersonate anything. |
| **Deauthentication attacks require knowing the WPA key** | "Only authorized users can deauth" | 802.11 management frames including deauth are UNAUTHENTICATED — any device can send deauth frames impersonating any AP. No key needed. 802.11w (PMF) fixes this. |
| **WPS provides alternative secure authentication** | "WPS is safe if you use the button method" | WPS push-button method is safer than PIN method but WPS as a whole is problematic — many implementations still expose the PIN attack surface. Disable entirely. |
| **Monitor mode is the same as promiscuous mode** | "Both modes capture all traffic" | Promiscuous mode: wired Ethernet — captures all Ethernet frames regardless of destination MAC. Monitor mode: wireless only — captures all 802.11 frames including management/control — no network association required. |
| **KRACK broke WPA2 permanently** | "WPA2 is now broken" | KRACK was a patchable vulnerability in the four-way handshake implementation — NOT the AES-CCMP cipher. All patched implementations (2017+) are not vulnerable to KRACK. |

---

### E9 — Current Landscape 2026

> [!NOTE]
> Current state of wireless security threats in 2025–2026.

**Wi-Fi 6 and Wi-Fi 7 Adoption:**
- Wi-Fi 6 (802.11ax) is now mainstream — most new devices and
  enterprise APs support WPA3 as default.
- Wi-Fi 7 (802.11be) arriving 2024–2025 — multi-link operation
  (MLO) across 2.4/5/6 GHz simultaneously.
- WPA3 adoption accelerating but WPA2 still dominant in
  existing deployments — estimated 60–70% of enterprise Wi-Fi
  still WPA2 as of 2025.

**OWE (Opportunistic Wireless Encryption):**
Wi-Fi Enhanced Open / OWE encrypts open wireless networks without
requiring a password — prevents passive sniffing of coffee shop
Wi-Fi. Firesheep-style attacks no longer work against OWE-enabled
open networks. Adoption increasing in public hotspots.

**AI-Assisted Wireless Cracking (2024–2025):**
- ML models trained on password patterns generate targeted
  wordlists based on SSID name, location data, and corporate
  naming conventions — dramatically improving dictionary attack
  success rates against WPA2-PSK networks.
- GPU cluster rental (AWS, Azure) enables processing of
  billions of WPA2 password candidates for under $10/hour —
  lowering the cost barrier for intensive cracking operations.

**Relevant CVEs:**
- **CVE-2023-52160 (wpa_supplicant — 2024):**
  Authentication bypass in WPA2-Enterprise — clients would
  connect to a rogue AP with matching SSID without verifying
  the AP's certificate. Affected Android, Linux.
  CVSS 6.5. Patched February 2024.
- **CVE-2022-47522 (MacStealer — 2023):**
  Logic flaw in 802.11 power-saving queue mechanism allowing
  interception of frames destined for other clients on same AP.
  Affects all WPA2/WPA3 implementations.
- **CVE-2019-9494 / CVE-2019-9496 (Dragonblood — 2019):**
  WPA3 SAE timing and cache side-channel vulnerabilities.
  Patched in updated implementations.

**5G and Private Networks:**
Organizations increasingly deploy private 5G networks alongside
or replacing corporate Wi-Fi — different attack surface:
SIM-based authentication, stronger encryption by default,
no WEP/WPA legacy concerns. However, IMSI catchers and
SS7 attacks emerge as wireless security challenges in 5G context.

---

### E10 — Indian Legal Context

> [!NOTE]
> Indian law applicable to wireless network attacks.

| Law | Section | Offence | Penalty |
|---|---|---|---|
| **IT Act 2000** | **S.43(a)** | Unauthorized access to computer network via wireless hacking | Civil compensation up to ₹1 crore |
| **IT Act 2000** | **S.66** | Criminal unauthorized access — WEP/WPA cracking to access network | Up to 3 years + ₹5 lakh fine |
| **IT Act 2000** | **S.66B** | Using compromised wireless network to intercept and receive data | Up to 3 years + ₹1 lakh fine |
| **IT Act 2000** | **S.66C** | Using stolen credentials captured via evil twin / wireless sniffing | Up to 3 years + ₹1 lakh fine |
| **IT Act 2000** | **S.66F** | Wireless attack on critical infrastructure networks | **Life imprisonment** |
| **IT Act 2000** | **S.69B** | Unauthorized monitoring / interception of wireless network traffic | Up to 3 years + ₹5 lakh fine |
| **Indian Telegraph Act 1885** | **S.4** | Unauthorized establishment or use of wireless transmitter | Up to 3 years + fine |
| **Indian Wireless Telegraphy Act 1933** | **S.6** | Operating wireless transmitter (evil twin AP, rogue AP, RF jammer) without license | Up to 3 years + ₹1,000 fine |
| **DPDPA 2023** | — | Personal data exposed via wireless network breach | Penalty up to ₹250 crore |

> [!IMPORTANT]
> The **Indian Wireless Telegraphy Act 1933** specifically
> applies to operating unauthorized wireless transmitters —
> directly applicable to evil twin attacks, rogue AP deployment,
> and RF jamming. Setting up an evil twin AP is simultaneously
> illegal under the IT Act (unauthorized access facilitation)
> AND the Wireless Telegraphy Act (unlicensed transmission).
>
> **Wardriving** (passive scanning only) is generally not
> illegal under current Indian law — but the moment any
> connection or data capture from an unauthorized network
> occurs, IT Act S.43(a) and S.66 apply.

---

## Abbreviations Table

| Abbreviation | Full Form | One-Line Technical Meaning |
|---|---|---|
| **AES** | Advanced Encryption Standard | Symmetric block cipher — 128/256-bit — WPA2/WPA3 encryption |
| **ANonce** | Authenticator Nonce | Random value generated by AP in WPA four-way handshake Message 1 |
| **AP** | Access Point | Wireless network infrastructure device — base station |
| **BSSID** | Basic Service Set Identifier | MAC address of the AP radio interface |
| **CCMP** | Counter Mode with CBC-MAC Protocol | AES-based encryption protocol used in WPA2 |
| **EAP** | Extensible Authentication Protocol | Framework for network authentication — multiple method types |
| **EAPOL** | EAP over LAN | Layer 2 encapsulation of EAP messages — used in 802.1X |
| **ESSID** | Extended Service Set Identifier | SSID spanning multiple APs in same network |
| **FMS** | Fluhrer, Mantin, Shamir | Authors of 2001 RC4 weak IV attack — basis of WEP cracking |
| **GCMP** | Galois/Counter Mode Protocol | AES-based cipher used in WPA3 Enterprise — stronger than CCMP |
| **GTK** | Group Temporal Key | Encryption key for multicast/broadcast traffic — sent in handshake |
| **HMAC** | Hash-based Message Authentication Code | Keyed hash for message integrity verification |
| **ICV** | Integrity Check Value | CRC-32 appended to WEP plaintext for integrity — not cryptographic |
| **IEEE** | Institute of Electrical and Electronics Engineers | Standards body — publishes 802.11 wireless standards |
| **IV** | Initialization Vector | Random value combined with key before encryption — 24-bit in WEP |
| **KRACK** | Key Reinstallation Attack | WPA2 four-way handshake nonce reuse vulnerability (2017) |
| **MANA** | MANA Toolkit | Advanced evil twin/Karma attack framework |
| **MIC** | Message Integrity Code | Cryptographic integrity check in WPA (Michael MIC) |
| **MIMO** | Multiple Input Multiple Output | Multi-antenna technology in 802.11n/ac/ax |
| **OWE** | Opportunistic Wireless Encryption | Encrypts open Wi-Fi without requiring a password |
| **PBKDF2** | Password-Based Key Derivation Function 2 | Converts WPA2 passphrase + SSID → PMK (4096 iterations) |
| **PMF** | Protected Management Frames | 802.11w — cryptographic protection for management frames |
| **PMK** | Pairwise Master Key | 256-bit key derived from PSK+SSID — basis for session key generation |
| **PMKID** | Pairwise Master Key Identifier | Hash derived from PMK — allows WPA2 cracking without handshake |
| **PRF** | Pseudorandom Function | Cryptographic function for key derivation in WPA |
| **PSK** | Pre-Shared Key | Shared password used in WPA/WPA2 Personal mode |
| **PTK** | Pairwise Transient Key | Per-session encryption key derived from PMK + nonces |
| **PTW** | Pyshkin, Tews, Weinmann | Improved WEP attack (2007) — requires only ~35,000 frames |
| **RADIUS** | Remote Authentication Dial-In User Service | Centralized authentication server for 802.1X/EAP |
| **RC4** | Rivest Cipher 4 | Stream cipher used in WEP and WPA TKIP — broken |
| **RFMON** | Radio Frequency Monitor Mode | Wireless NIC mode capturing all 802.11 frames |
| **SAE** | Simultaneous Authentication of Equals | WPA3 key exchange (Dragonfly) — replaces PSK |
| **SNonce** | Supplicant Nonce | Random value generated by client in WPA four-way handshake |
| **SSID** | Service Set Identifier | Wireless network name — up to 32 characters |
| **STA** | Station | Wireless client device |
| **TKIP** | Temporal Key Integrity Protocol | Per-packet key mixing for WPA — deprecated |
| **WDS** | Wireless Distribution System | AP-to-AP wireless link protocol |
| **WEP** | Wired Equivalent Privacy | Original broken wireless security protocol (1997) |
| **WPA** | Wi-Fi Protected Access | Interim WEP replacement (2003) — TKIP+RC4 |
| **WPA2** | Wi-Fi Protected Access 2 | Current standard (2004) — AES-CCMP |
| **WPA3** | Wi-Fi Protected Access 3 | Latest standard (2018) — SAE/Dragonfly |
| **WPS** | Wi-Fi Protected Setup | Simplified device pairing — PIN brute-force vulnerable |
| **XOR** | Exclusive OR | Bitwise operation — WEP encryption uses XOR with RC4 keystream |

---

## 🔑 Keywords + Concept Map

**Core Keywords:**

`WEP` · `WPA` · `WPA2` · `WPA3` · `RC4` · `TKIP` · `CCMP` · `AES` ·
`GCMP` · `SAE` · `Dragonfly` · `PSK` · `PMK` · `PTK` · `PBKDF2` ·
`Four-Way Handshake` · `PMKID` · `WPS` · `Pixie Dust` · `IV` ·
`FMS Attack` · `PTW Attack` · `aircrack-ng` · `airmon-ng` ·
`airodump-ng` · `aireplay-ng` · `hashcat` · `SSID` · `BSSID` ·
`Hidden SSID` · `Monitor Mode` · `Promiscuous Mode` · `Wardriving` ·
`Kismet` · `MAC Spoofing` · `MAC Filtering` · `Evil Twin` · `Rogue AP` ·
`Karma Attack` · `Deauthentication Attack` · `KRACK` · `Dragonblood` ·
`802.11w` · `PMF` · `802.1X` · `EAP-TLS` · `EAP-PEAP` · `RADIUS` ·
`T1040` · `T1110` · `T1557`

---

**Concept Map:**

    WIRELESS HACKING
    │
    ├── ENCRYPTION PROTOCOLS
    │   ├── WEP ────────── RC4 + 24-bit IV → BROKEN (FMS/PTW attack)
    │   ├── WPA ────────── RC4 + TKIP → Deprecated (2012)
    │   ├── WPA2 ──────── AES + CCMP → Acceptable (strong PSK)
    │   │   ├── Personal (PSK) → four-way handshake → offline crack
    │   │   └── Enterprise (802.1X + EAP) → per-user → no PSK
    │   └── WPA3 ──────── AES + SAE/Dragonfly → Forward secrecy
    │       └── Dragonblood (2019) → side-channel → patched
    │
    ├── CRACKING METHODS
    │   ├── WEP ────────── Capture IVs → statistical (aircrack-ng)
    │   │   └── ARP replay (aireplay-ng) → generate IVs fast
    │   ├── WPA/WPA2 ──── Capture four-way handshake → offline dict
    │   │   ├── Deauth → force reconnect → capture handshake
    │   │   ├── PMKID → no handshake needed → single EAPOL frame
    │   │   └── hashcat / aircrack-ng + rockyou.txt
    │   └── WPS ────────── PIN brute force (11,000 max) / Pixie Dust
    │
    ├── DISCOVERY & SNIFFING
    │   ├── Monitor mode → capture all 802.11 frames
    │   ├── airodump-ng → AP/client discovery
    │   ├── Hidden SSID → revealed by probe requests / deauth trick
    │   └── Wardriving → map wireless networks with GPS
    │
    ├── IDENTITY ATTACKS
    │   ├── MAC Spoofing → bypass MAC filtering → 30 seconds
    │   │   └── MAC filtering = security theater (MACs in plaintext)
    │   ├── Evil Twin → clone AP → higher signal → MITM
    │   ├── Rogue AP → unauthorized AP on wired network
    │   └── Karma → respond to any probe → auto-connect MITM
    │
    ├── OTHER ATTACKS
    │   ├── Deauthentication → forged mgmt frames → disconnect client
    │   │   └── Fix: 802.11w PMF
    │   ├── KRACK (2017) → nonce reuse in handshake → patchable
    │   └── RF Jamming → physical layer interference → illegal
    │
    └── SECURING WIRELESS
        ├── Encryption: WPA3 > WPA2 (CCMP only) > WPA > WEP
        ├── Auth: 802.1X + EAP-TLS > PSK
        ├── Disable: WPS | SSID hiding (false security) | MAC filtering
        ├── Enable: 802.11w PMF | Guest VLAN | Wireless IDS
        └── Physical: Reduce power | AP placement | Firmware updates

---

## ⚡ Quick Reference Cheatsheet

### 🔐 Wireless Security Protocol Comparison

| Protocol | Encryption | Key Exchange | Status | Cracking Method |
|---|---|---|---|---|
| Open | None | None | ❌ Never use | Passive sniff |
| WEP 64-bit | RC4 + 24-bit IV | Static shared | ❌ Broken | FMS/PTW — ~5 minutes |
| WEP 128-bit | RC4 + 24-bit IV | Static shared | ❌ Broken | FMS/PTW — marginally slower |
| WPA (TKIP) | RC4 + TKIP | PSK or 802.1X | ❌ Deprecated | Handshake + dict |
| WPA2 Personal | AES-CCMP | PSK | ⚠️ Acceptable | Handshake/PMKID + dict |
| WPA2 Enterprise | AES-CCMP | 802.1X + EAP | ✅ Good | EAP method dependent |
| WPA3 Personal | AES-SAE | SAE | ✅ Recommended | Dragonblood (patched) |
| WPA3 Enterprise | AES-256 GCMP | 802.1X + EAP-TLS | ✅ Best | Extremely difficult |

---

### 🛠️ Aircrack-ng Attack Commands Reference

**WEP Cracking:**

    airmon-ng start wlan0
    airodump-ng -c 6 --bssid TARGET_BSSID -w capture wlan0mon
    aireplay-ng -3 -b TARGET_BSSID -h CLIENT_MAC wlan0mon
    aircrack-ng capture.cap

**WPA/WPA2 Cracking:**

    airmon-ng check kill
    airmon-ng start wlan0
    airodump-ng -c 6 --bssid TARGET_BSSID -w wpa_cap wlan0mon
    aireplay-ng -0 5 -a TARGET_BSSID -c CLIENT_MAC wlan0mon
    aircrack-ng -w rockyou.txt -b TARGET_BSSID wpa_cap.cap

**PMKID Attack:**

    hcxdumptool -i wlan0mon -o pmkid.pcapng
    hcxpcapngtool -o hash.hc22000 pmkid.pcapng
    hashcat -m 22000 hash.hc22000 rockyou.txt

**WPS Brute Force:**

    wash -i wlan0mon
    reaver -i wlan0mon -b TARGET_BSSID -vv

**MAC Spoofing:**

    ip link set wlan0 down
    ip link set wlan0 address 11:22:33:44:55:66
    ip link set wlan0 up

---

### 🆚 WEP vs WPA vs WPA2 vs WPA3

| Property | WEP | WPA | WPA2 | WPA3 |
|---|---|---|---|---|
| Year | 1997 | 2003 | 2004 | 2018 |
| Cipher | RC4 | RC4+TKIP | AES-CCMP | AES-SAE |
| IV size | 24-bit | 48-bit | 48-bit (PN) | N/A (SAE) |
| Key mgmt | Static | Dynamic (TKIP) | Dynamic (CCMP) | SAE/Dragonfly |
| Forward secrecy | ❌ | ❌ | ❌ | ✅ |
| Crackable? | ✅ Always | ✅ Dict attack | ✅ Dict (weak PSK) | Harder |
| Status | Broken | Deprecated | Current | Recommended |

---

### 🎭 Evil Twin vs Rogue AP vs Karma

| Property | Evil Twin | Rogue AP | Karma |
|---|---|---|---|
| Clones existing SSID | ✅ Yes | ❌ Optional | ✅ Any requested SSID |
| Wired network access | ❌ No | ✅ Yes | ❌ No |
| Target | Wireless clients | Internal network | Any mobile device |
| Primary tool | hostapd/Wifiphisher | Physical router | MANA toolkit |
| Fix | Wireless IDS + PMF | 802.1X on switch ports | PMF + certificate validation |

---

### 📡 Key Attack Commands

| Attack | Command |
|---|---|
| Enable monitor mode | `airmon-ng start wlan0` |
| Discover APs | `airodump-ng wlan0mon` |
| Capture on target | `airodump-ng -c 6 --bssid BSSID -w out wlan0mon` |
| Deauthenticate client | `aireplay-ng -0 5 -a AP_BSSID -c CLIENT_MAC wlan0mon` |
| ARP replay (WEP) | `aireplay-ng -3 -b AP_BSSID -h CLIENT_MAC wlan0mon` |
| Crack WEP | `aircrack-ng capture.cap` |
| Crack WPA dict | `aircrack-ng -w rockyou.txt -b BSSID cap.cap` |
| GPU crack WPA | `hashcat -m 22000 hash.hc22000 wordlist.txt` |
| WPS scan | `wash -i wlan0mon` |
| WPS crack | `reaver -i wlan0mon -b BSSID -vv` |
| MAC spoof | `ip link set wlan0 address NEW:MAC:ADDRESS` |

---

### ⚖️ Indian Legal Reference

| Law | Section | Offence | Penalty |
|---|---|---|---|
| IT Act 2000 | S.43(a) | Unauthorized wireless network access | Civil ₹1 crore |
| IT Act 2000 | S.66 | Criminal wireless hacking | 3 yrs + ₹5L |
| IT Act 2000 | S.66B | Intercepting wireless data | 3 yrs + ₹1L |
| IT Act 2000 | S.69B | Unauthorized wireless traffic monitoring | 3 yrs + ₹5L |
| IT Act 2000 | S.66F | Wireless attack on critical infrastructure | Life imprisonment |
| Wireless Telegraphy Act 1933 | S.6 | Unlicensed wireless transmission (evil twin, rogue AP, jammer) | 3 yrs + fine |
| DPDPA 2023 | — | Data breach via wireless attack | ₹250 crore |

---

## ✅ Session Revision Snapshot

### ⚡ TL;DR — 5 Bullets

1. **WEP is broken because of the 24-bit IV + RC4 combination —
   not key length.** IV exhaustion occurs in hours on busy networks;
   the FMS attack exploits weak IVs to recover the key byte by byte;
   PTW attack needs only ~35,000 ARP-replay-generated frames.
   128-bit WEP is cracked just as reliably as 64-bit WEP.
   WEP provides zero meaningful security regardless of configuration.

2. **WPA2-PSK cracking captures the four-way handshake, then performs
   offline dictionary attack.** The handshake contains a MIC derived
   from the PSK — attacker tests each dictionary word through PBKDF2
   (PSK+SSID→PMK) → PRF (PMK+nonces→PTK) → MIC comparison.
   PMKID attack (2018) skips handshake capture — works without any
   client connected. WPS reduces the effective keyspace to 11,000.

3. **Hiding SSID and MAC filtering are both security theater.**
   Hidden SSIDs are revealed in probe requests from existing clients —
   discoverable in seconds with airodump-ng.
   MAC addresses are in cleartext in every 802.11 frame — copied
   by passive sniffing and spoofed in 30 seconds with one command.
   Neither provides meaningful security against a motivated attacker.

4. **The deauthentication attack sends forged 802.11 management frames
   (no authentication needed) to disconnect clients — used to force
   WPA handshake capture, enable evil twin connections, or deny service.**
   Fixed by 802.11w (PMF — Protected Management Frames) — mandatory
   in WPA3. Evil twin clones a legitimate AP's SSID for MITM.
   Rogue AP connects to the wired network for unauthorized access.
   Karma attack responds to any probe request for auto-connect MITM.

5. **WPA3 introduced SAE (Dragonfly) replacing PSK — providing
   forward secrecy and resistance to offline dictionary attacks.**
   Dragonblood (2019) found timing/cache side-channels in SAE —
   patched in updated implementations. WPA3 Enterprise uses AES-256
   GCMP and mandatory EAP-TLS for highest security. Security hierarchy:
   WPA3 Enterprise > WPA3 Personal > WPA2 Enterprise > WPA2 Personal.**

---

### 🎯 MCQ-Likely Concepts

- [ ] WEP — 24-bit IV — 16,777,216 values — IV reuse → broken
- [ ] FMS attack — weak IVs — statistical WEP key recovery
- [ ] WEP key lengths: 64-bit = 40-bit key + 24-bit IV; 128-bit = 104-bit key + 24-bit IV
- [ ] WEP broken regardless of key length — IV flaw is fundamental
- [ ] TKIP — WPA — per-packet key mixing — still RC4 — deprecated
- [ ] CCMP — WPA2 — AES-128 — Counter Mode + CBC-MAC
- [ ] WPA2-PSK cracking = capture four-way handshake + offline dictionary
- [ ] Four-way handshake — ANonce, SNonce, MIC — no password in handshake
- [ ] PBKDF2 — PSK + SSID → PMK — SSID is part of derivation
- [ ] PMKID attack — no handshake needed — works without connected clients
- [ ] WPS PIN — 11,000 effective combinations — not 100,000,000
- [ ] Pixie Dust — offline WPS PIN recovery — seconds
- [ ] WPA3 — SAE / Dragonfly — forward secrecy
- [ ] Dragonblood — WPA3 timing + cache side-channel — 2019
- [ ] KRACK — key reinstallation — nonce reuse — 2017 — patchable
- [ ] Monitor mode vs promiscuous mode — wireless vs wired distinction
- [ ] Hidden SSID — not security — revealed in probe requests
- [ ] MAC filtering — not security — MACs in plaintext — spoofed in 30 seconds
- [ ] Evil twin — same SSID + higher signal — MITM
- [ ] Rogue AP — connected to wired network — bypasses perimeter
- [ ] Karma attack — responds to any probe SSID — auto-connect MITM
- [ ] Deauthentication attack — forged management frames — no key needed
- [ ] 802.11w PMF — protects management frames — fixes deauth attack
- [ ] airmon-ng — enable monitor mode
- [ ] airodump-ng — AP/client discovery + packet capture
- [ ] aireplay-ng -0 — deauthentication attack
- [ ] aireplay-ng -3 — ARP replay (WEP IV generation)
- [ ] hashcat -m 22000 — WPA2 GPU cracking
- [ ] EAP-TLS — strongest — mutual certificate authentication
- [ ] LEAP — broken Cisco EAP — do not deploy
- [ ] Wardriving — passive = legal; connecting unauthorized = illegal
- [ ] Wireless Telegraphy Act 1933 S.6 — unlicensed transmission
- [ ] IT Act S.66F — wireless attack on critical infrastructure = life

---

### 💼 Interview-Likely

- Why is WEP broken — specifically what is the IV weakness?
- Explain the WPA2 four-way handshake and how it enables offline cracking.
- What is the PMKID attack and why is it significant compared to handshake capture?
- Why does the SSID matter in WPA2 PSK cracking?
- Explain the difference between evil twin and rogue AP attacks.
- Why does hiding the SSID not provide security?
- Why is MAC filtering not a security control?
- What is the WPS PIN vulnerability and what makes it exploitable?
- What is WPA3 SAE and how does it improve over WPA2 PSK?
- What is KRACK and is WPA2 still safe after it?
- What is 802.11w and what attack does it prevent?
- What is the Karma attack and how does it differ from evil twin?

---

## Next Session Bridge

Session 17B completed the wireless hacking sub-phase — covering
the evolution of wireless security from broken WEP through WPA2
to WPA3, the specific cracking techniques for each, and the
full range of wireless attack vectors from sniffing and MAC
spoofing to evil twin and deauthentication attacks.

Session 18 shifts from attacking communications channels to
attacking **systems and defences** — covering backdoor devices,
advanced distributed DoS, biometric spoofing, Linux hacking and
Linux backdoors, and finally the defensive infrastructure itself:
IDS, Honeypots, and Firewalls. The wireless knowledge from this
session (particularly rogue APs and traffic interception)
connects directly to IDS detection requirements in Session 18.

---

<details>
<summary>📖 Glossary</summary>

| Term | Definition |
|---|---|
| **802.11** | IEEE standard family for wireless LAN — 802.11b/g/n/ac/ax/be |
| **802.11w** | IEEE amendment adding Protected Management Frames (PMF) — prevents deauth attacks |
| **802.1X** | IEEE port-based network access control standard — used in WPA Enterprise |
| **aircrack-ng** | Suite of wireless security tools for monitoring, attacking, and cracking wireless networks |
| **airmon-ng** | aircrack-ng tool for enabling/disabling monitor mode on wireless interfaces |
| **airodump-ng** | aircrack-ng tool for passive wireless packet capture and AP/client discovery |
| **aireplay-ng** | aircrack-ng tool for wireless packet injection — deauth, ARP replay, fake auth |
| **ANonce** | Authenticator Nonce — random value generated by AP in WPA four-way handshake |
| **ARP replay** | aireplay-ng attack replaying captured ARP packets to generate WEP IV traffic |
| **Beacon frame** | 802.11 management frame broadcast by AP every ~100ms advertising network presence |
| **Besside-ng** | aircrack-ng tool for automated WEP/WPA cracking |
| **BSSID** | Basic Service Set Identifier — MAC address of the access point radio |
| **CCMP** | Counter Mode with CBC-MAC Protocol — AES-based WPA2 encryption protocol |
| **Deauthentication attack** | Sending forged 802.11 deauth frames to disconnect wireless clients |
| **Dragonblood** | 2019 WPA3 SAE vulnerability — timing and cache side-channel attacks |
| **Dragonfly** | Elliptic curve key exchange underlying WPA3 SAE |
| **EAP** | Extensible Authentication Protocol — framework for network authentication |
| **EAP-PEAP** | Protected EAP — server certificate + username/password — most common enterprise |
| **EAP-TLS** | EAP with TLS — client + server certificates — highest security EAP method |
| **ESSID** | Extended Service Set Identifier — SSID spanning multiple APs |
| **Evil twin** | Rogue AP cloning legitimate AP SSID to perform MITM against wireless clients |
| **FMS attack** | Fluhrer, Mantin, Shamir 2001 — RC4 weak IV statistical WEP key recovery |
| **Forward secrecy** | Property ensuring past sessions cannot be decrypted if future key is compromised |
| **Four-way handshake** | WPA/WPA2 key establishment exchange — capture enables offline cracking |
| **GCMP** | Galois/Counter Mode Protocol — AES cipher used in WPA3 Enterprise |
| **GTK** | Group Temporal Key — shared key for multicast/broadcast traffic |
| **hashcat** | GPU-accelerated password cracking tool — supports WPA2 (-m 22000) |
| **hcxdumptool** | Modern wireless capture tool — PMKID and handshake capture |
| **hostapd** | Linux software AP daemon — used in evil twin and rogue AP attacks |
| **ICV** | Integrity Check Value — CRC-32 appended to WEP plaintext — not cryptographic |
| **IV** | Initialization Vector — 24-bit random value in WEP — too small — reused |
| **Karma attack** | Evil twin variant responding to any probe SSID — targets roaming clients |
| **Kismet** | Passive wireless network detector and IDS — no transmission |
| **KRACK** | Key Reinstallation Attack — WPA2 four-way handshake nonce reuse (2017) |
| **MANA toolkit** | Advanced evil twin and Karma attack framework |
| **Michael MIC** | WPA TKIP integrity algorithm replacing broken CRC-32 |
| **Monitor mode** | Wireless NIC mode capturing all 802.11 frames without association |
| **NetStumbler** | Legacy Windows wireless network scanner |
| **OWE** | Opportunistic Wireless Encryption — encrypts open Wi-Fi without password |
| **PBKDF2** | Password-Based Key Derivation Function 2 — converts WPA2 passphrase+SSID to PMK |
| **Pixie Dust** | WPS attack exploiting weak randomness to recover PIN offline in seconds |
| **PMF** | Protected Management Frames — 802.11w — cryptographic management frame protection |
| **PMK** | Pairwise Master Key — 256-bit key derived from PSK+SSID |
| **PMKID** | Pairwise Master Key Identifier — 2018 attack — WPA2 cracking without handshake |
| **Probe request** | 802.11 management frame sent by client searching for a network |
| **PSK** | Pre-Shared Key — shared wireless password in WPA/WPA2 Personal mode |
| **PTK** | Pairwise Transient Key — per-session encryption key derived from PMK + nonces |
| **PTW attack** | Pyshkin, Tews, Weinmann — improved WEP attack requiring ~35,000 frames |
| **RADIUS** | Remote Authentication Dial-In User Service — centralized 802.1X auth server |
| **RC4** | Rivest Cipher 4 — stream cipher — used in WEP and WPA TKIP — broken in WEP |
| **Reaver** | WPS PIN brute force tool |
| **Rogue AP** | Unauthorized AP connected to wired network — provides unauthorized wireless access |
| **SAE** | Simultaneous Authentication of Equals — WPA3 Dragonfly key exchange |
| **SNonce** | Supplicant Nonce — random value generated by client in WPA four-way handshake |
| **SSID** | Service Set Identifier — wireless network name |
| **TKIP** | Temporal Key Integrity Protocol — per-packet key mixing — WPA — deprecated |
| **Wardriving** | Driving through area scanning for wireless networks with GPS logging |
| **Wifiphisher** | Automated evil twin + captive portal attack framework |
| **WEP** | Wired Equivalent Privacy — original broken wireless security protocol |
| **Wifiphisher** | Automated evil twin framework for credential phishing |
| **WPA** | Wi-Fi Protected Access — WEP replacement using TKIP+RC4 |
| **WPA2** | Wi-Fi Protected Access 2 — uses AES-CCMP — current standard |
| **WPA3** | Wi-Fi Protected Access 3 — uses SAE/Dragonfly — latest standard |
| **WPS** | Wi-Fi Protected Setup — PIN-based pairing — 11,000 effective combinations |

</details>

---