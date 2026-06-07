# MCQ Set — Session 17B: Wireless Hacking · WEP/WPA Cracking · SSID/MAC Spoofing · Securing Wireless 📡

> 28 MCQs · 4 options each · Full explanations · Covers core + extra notes

---

## 📑 Table of Contents

- [Questions 01–06 — WEP Vulnerabilities and Cracking](#questions-0106--wep-vulnerabilities-and-cracking)
- [Questions 07–12 — WPA/WPA2 and Four-Way Handshake](#questions-0712--wpawpa2-and-four-way-handshake)
- [Questions 13–17 — WPA3 · WPS · PMKID](#questions-1317--wpa3--wps--pmkid)
- [Questions 18–22 — Wireless Sniffing · SSID · MAC Spoofing](#questions-1822--wireless-sniffing--ssid--mac-spoofing)
- [Questions 23–26 — Wireless Attack Techniques](#questions-2326--wireless-attack-techniques)
- [Questions 27–28 — Securing Wireless & Extra Notes](#questions-2728--securing-wireless--extra-notes)
- [Answer Key](#answer-key)

---

## Questions 01–06 — WEP Vulnerabilities and Cracking

---

### Q01

**WEP uses a 24-bit Initialization Vector (IV) combined with the WEP key before input to the RC4 cipher. What is the PRECISE reason this 24-bit IV is the root cause of WEP's complete cryptographic failure?**

- A) 24 bits is too short to encrypt a full Ethernet frame — the frame is only partially encrypted
- B) The IV is stored encrypted inside the frame — attackers must brute force 24 bits to find it
- C) The IV changes the TCP/IP port used for transmission — allowing firewall bypass
- D) ✅ 24 bits provides only 16,777,216 unique values — on a busy network these exhaust within hours — IV reuse with RC4 produces the same keystream — XOR of two same-keystream ciphertexts cancels the key and reveals the XOR of plaintexts — enabling cryptanalysis

**Explanation:**

- **A** is incorrect — the IV is not a length parameter for the frame. It is combined with the WEP key to initialize the RC4 stream cipher — the encryption covers the entire payload regardless of IV length. The problem is IV REUSE, not payload coverage.
- **B** is incorrect — the IV is transmitted in **plaintext** in the frame header — it is deliberately unencrypted so the receiver can use it to reconstruct the RC4 keystream for decryption. There is no brute force needed to find the IV.
- **C** is incorrect — the IV operates at the cryptographic layer — it has no relationship to TCP/IP ports or firewall behaviour. Port information is in the IP/TCP headers above the encryption layer.
- **D** ✅ is correct — 2²⁴ = 16,777,216 unique IV values. On a busy network generating ~500 frames/second, all IVs are theoretically exhausted in under 10 hours. In practice, the birthday paradox means collision probability reaches 50% after far fewer frames. When two frames share the same IV with the same key, they use the **identical RC4 keystream**. XOR'ing the two ciphertexts: `C1 XOR C2 = (P1 XOR KS) XOR (P2 XOR KS) = P1 XOR P2` — the keystream cancels. Since IP headers have predictable structure, both plaintexts can be recovered. The FMS attack further exploits specific "weak IVs" to statistically recover the WEP key byte by byte.

---

### Q02

**WEP is available in 64-bit and 128-bit configurations. A network administrator argues that 128-bit WEP is acceptable for their legacy hardware because "it would take twice as long to crack." Which statement CORRECTLY refutes this?**

- A) 128-bit WEP uses a different cipher algorithm — but that algorithm (AES) is also broken
- B) 128-bit WEP eliminates IV collisions by using a larger IV space
- C) ✅ Both 64-bit and 128-bit WEP use the same 24-bit IV regardless of key length — the IV weakness affects both identically — 128-bit WEP is cracked only marginally slower than 64-bit because the attack targets IV patterns, not key length
- D) 128-bit WEP is actually weaker because the longer key creates more predictable RC4 keystream patterns

**Explanation:**

- **A** is incorrect — WEP uses RC4 (not AES) at all key lengths. AES is not involved in WEP at any configuration. Both 64-bit and 128-bit WEP use the same broken RC4+IV mechanism.
- **B** is incorrect — this is the critical misconception. The IV remains **24 bits** in BOTH 64-bit and 128-bit WEP. The key length only changes the secret key portion: 64-bit = 40-bit key + 24-bit IV; 128-bit = 104-bit key + 24-bit IV. The IV space is identical — 2²⁴ — in both configurations.
- **C** ✅ is correct — the FMS and PTW attacks target statistical patterns in RC4 keystream outputs associated with specific IV values (weak IVs). The attack exploits the interaction between the 24-bit IV and the RC4 key scheduling algorithm. Since the IV is the same size (24 bits) in all WEP variants, the attack requires approximately the same number of captured frames regardless of key length. 128-bit WEP requires slightly more frames (~85,000 vs ~40,000 for 64-bit) but is cracked in the same timeframe — both in under 5 minutes with modern tools and ARP replay injection.
- **D** is incorrect — longer WEP keys are not weaker due to keystream predictability. The weakness is entirely in the IV reuse mechanism — not RC4 keystream predictability per se.

---

### Q03

**During a WEP cracking exercise, an attacker runs `aireplay-ng -3 -b AA:BB:CC:DD:EE:FF -h CLIENT_MAC wlan0mon` while simultaneously running airodump-ng. What is the specific purpose of aireplay-ng attack mode `-3` and why does it dramatically accelerate WEP cracking?**

- A) Mode -3 sends deauthentication frames to disconnect clients — forcing them to re-associate and generate new IVs naturally
- B) Mode -3 performs a fake authentication — associating the attacker with the AP to enable subsequent attacks
- C) Mode -3 floods the AP with connection requests — causing it to broadcast IVs in error messages
- D) ✅ Mode -3 is ARP request replay — it captures one ARP packet from the legitimate client and replays it at high rate — the AP re-encrypts each replayed ARP with a new IV — rapidly generating thousands of unique IV-containing frames needed for statistical WEP key recovery

**Explanation:**

- **A** is incorrect — deauthentication is aireplay-ng mode `-0`. Deauthentication is used in WPA cracking (to capture handshake) — not in WEP cracking, where the goal is to generate many IV-containing frames from the AP.
- **B** is incorrect — fake authentication is mode `-1`. It associates the attacker's MAC with the AP but does not by itself generate IV traffic. It is often a prerequisite before ARP replay on networks that filter unassociated stations.
- **C** is incorrect — connection request flooding is not the mechanism. The AP does not broadcast IVs in error messages. The AP generates new IVs by encrypting and transmitting legitimate-looking data packets.
- **D** ✅ is correct — ARP request replay (mode `-3`) works as follows: the attacker passively waits for one ARP request packet from a legitimate client. This ARP packet, when replayed to the AP, triggers the AP to forward it (because ARP requests are broadcast) — and the AP re-encrypts it with a **new IV** for each retransmission. The attacker replays at thousands of packets per second — the AP generates thousands of differently-IV'd encrypted responses — each captured by airodump-ng. This rapidly accumulates the 40,000–85,000 unique IVs needed for statistical key recovery, reducing cracking time from hours to minutes.

---

### Q04

**The FMS attack (Fluhrer, Mantin, Shamir — 2001) and PTW attack (Pyshkin, Tews, Weinmann — 2007) are both WEP cracking methods. What distinguishes the PTW attack as superior?**

- A) PTW attack uses GPU acceleration — FMS is CPU-only — PTW is faster due to hardware
- B) PTW attack cracks 128-bit WEP while FMS only works against 64-bit WEP
- C) PTW attack requires zero captured packets — it derives the key purely from the SSID
- D) ✅ PTW attack uses all captured packets (not just weak IVs) and is specifically optimized for ARP packets — requiring only ~35,000 frames compared to FMS which needs ~250,000–400,000 frames with weak IVs

**Explanation:**

- **A** is incorrect — GPU acceleration is a separate implementation detail of cracking tools like hashcat — not an inherent property of PTW vs FMS. Both attacks are statistical algorithms that can be implemented on CPU or GPU.
- **B** is incorrect — both FMS and PTW work against all WEP key lengths. The IV weakness affects 64-bit and 128-bit WEP equally. PTW's advantage is efficiency — not scope.
- **C** is incorrect — all WEP cracking methods require captured traffic containing IVs. The SSID alone provides no cryptographic material for WEP key recovery.
- **D** ✅ is correct — the FMS attack relies on identifying specific "weak IVs" of the form (A+3, 255, X) that cause RC4 key scheduling to leak key bytes. Only a fraction of IVs are weak — requiring collection of 250,000–400,000 total frames to get enough weak IVs. PTW improved on FMS by developing a statistical attack that works on ALL captured packets — not just weak IVs — and is specifically tuned for ARP packet structure (known plaintext — ARP has predictable content). With ARP replay injection, PTW needs only ~35,000 frames for 64-bit WEP — approximately 10× fewer than FMS — dramatically reducing attack time.

---

### Q05

**A penetration tester runs `aircrack-ng capture.cap` after capturing WEP traffic and receives the message "Not enough IVs. Try capturing more packets." The tester has captured 8,000 packets. What is the MOST efficient next step?**

- A) Run `aircrack-ng` with the `-z` flag to enable PTW mode on the existing 8,000 packets
- B) Wait passively for more traffic — eventually enough IVs will accumulate naturally
- C) Switch to WPA cracking mode — WEP cannot be cracked with fewer than 1,000,000 packets
- D) ✅ Run `aireplay-ng -3` (ARP request replay) to inject ARP packets at high rate — the AP re-encrypts each with a new IV — rapidly generating the additional 30,000–80,000 unique IVs needed

**Explanation:**

- **A** is incorrect — while `aircrack-ng` does use PTW by default (flag `-z` enables it explicitly on older versions), running it again on the same 8,000 packets does not generate more IVs. The issue is insufficient data — not the analysis algorithm. More captured packets are needed.
- **B** is incorrect — waiting passively on a lightly-used network could take hours or days to accumulate sufficient IVs. Active injection is far more efficient.
- **C** is incorrect — WEP and WPA are completely different protocols with different cracking methodologies. WEP cracking does not have a million-packet requirement — the PTW attack needs approximately 35,000–85,000 frames. The issue here is insufficient current count, not an impossible threshold.
- **D** ✅ is correct — ARP replay injection (`aireplay-ng -3`) is specifically designed to solve this problem. By replaying one captured ARP request repeatedly, the AP generates new encrypted responses with different IVs at high speed — potentially thousands per minute. The airodump-ng capture running simultaneously accumulates these IVs rapidly. This is the standard technique to accelerate WEP IV collection from hours of passive waiting to minutes of active injection.

---

### Q06

**The WEP Shared Key Authentication process transmits BOTH the challenge text and the encrypted response across the air. Why is this a critical vulnerability beyond the WEP encryption weakness?**

- A) Transmitting the challenge text reveals the WEP key directly to passive observers
- B) The encrypted response uses DES instead of RC4 — making it trivially reversible
- C) ✅ An attacker observing both the plaintext challenge and its RC4-encrypted form can XOR them to derive the RC4 keystream for that IV — enabling authentication to the AP without knowing the WEP key by replaying a frame using that captured keystream
- D) Transmitting the challenge enables man-in-the-middle relay attacks using TCP session hijacking

**Explanation:**

- **A** is incorrect — the challenge text does not contain the WEP key. It is random data generated by the AP. The WEP key is never transmitted — only used locally for encryption. Observing the challenge reveals nothing about the key directly.
- **B** is incorrect — WEP Shared Key Authentication encrypts the challenge using RC4 (the same cipher as WEP data encryption) — not DES. The encryption is RC4-based in all WEP operations.
- **C** ✅ is correct — this is the known-plaintext attack against WEP Shared Key Authentication. The attacker sees: plaintext challenge `P` and encrypted challenge `C = P XOR RC4(IV || KEY)`. XOR'ing them: `C XOR P = RC4(IV || KEY)` — the attacker now has the full RC4 keystream for that specific IV value. The attacker stores: `(IV, keystream)`. When the attacker later needs to authenticate to the AP, they construct a fake authentication by using the captured IV + keystream pair to encrypt the AP's challenge — without ever knowing the WEP key. This means WEP Shared Key Authentication is **less secure than Open System Authentication** with WEP — open system does not expose keystream material.
- **D** is incorrect — WEP authentication occurs at Layer 2 (802.11) — TCP session hijacking operates at Layer 4. The challenge-response is a Layer 2 wireless authentication mechanism — TCP is not involved.

---

## Questions 07–12 — WPA/WPA2 and Four-Way Handshake

---

### Q07

**In WPA2-PSK, the PMK (Pairwise Master Key) is derived using PBKDF2. What TWO inputs to PBKDF2 mean that an attacker using a precomputed rainbow table for one network CANNOT use it against a different network — even if both networks use the same password?**

- A) The client's MAC address and the AP's firmware version
- B) ✅ The SSID and the passphrase — PBKDF2(HMAC-SHA1, passphrase, SSID, 4096 iterations, 256 bits) — the SSID acts as a salt — same passphrase on different SSID produces a completely different PMK
- C) The channel number and the geographic region code stored in the AP
- D) The AP's serial number and the date of first connection

**Explanation:**

- **A** is incorrect — the client MAC address is used in the four-way handshake for PTK derivation but is NOT part of PBKDF2 PMK computation. AP firmware version plays no role in cryptographic key derivation.
- **B** ✅ is correct — `PMK = PBKDF2(HMAC-SHA1, passphrase, SSID, 4096, 256)`. Both the **passphrase** and the **SSID** are inputs. The SSID functions as a **cryptographic salt** in this derivation. If network A has SSID "HomeNetwork" and network B has SSID "OfficeWiFi", even the identical passphrase "password123" produces completely different PMKs. This means precomputed rainbow tables (precomputing PMKs for common passwords) must be SSID-specific — a table for "HomeNetwork" is useless against "OfficeWiFi". Organizations with non-default SSIDs gain additional protection against precomputed attacks.
- **C** is incorrect — channel number and geographic region are RF configuration parameters — they have no involvement in cryptographic key generation. Changing channel does not change the PMK.
- **D** is incorrect — serial numbers and connection timestamps are not part of WPA2's cryptographic key derivation. The PMK is derived purely from passphrase + SSID through PBKDF2.

---

### Q08

**During WPA2 four-way handshake capture with airodump-ng, the attacker needs the client to (re)connect to the AP. Rather than waiting, the attacker runs:**

    aireplay-ng -0 5 -a AA:BB:CC:DD:EE:FF -c 11:22:33:44:55:66 wlan0mon

**What does this command do and why does it cause the client to reconnect?**

- A) It sends 5 EAPOL frames containing decoy handshake data — confusing the client into retransmitting the real handshake
- B) It injects 5 ARP packets toward the client — causing the client to refresh its IP configuration and reconnect
- C) It sends 5 beacon frames from the AP — reminding the client to stay associated
- D) ✅ It sends 5 forged deauthentication management frames impersonating the AP (using AP's BSSID as source) to the specific client — the client disconnects and automatically reconnects — the four-way handshake occurs during reconnection and is captured by airodump-ng

**Explanation:**

- **A** is incorrect — EAPOL frames are used in the four-way handshake itself — sending fake EAPOL frames would not cause a client to retransmit its real handshake. EAPOL injection is not aireplay-ng's `-0` mode function.
- **B** is incorrect — ARP packet injection is mode `-3` (ARP request replay) used for WEP IV generation — not deauthentication. ARP packets do not cause client disconnection or handshake retransmission.
- **C** is incorrect — beacon frames keep clients associated — they would prevent disconnection, not cause it. Sending extra beacons would not trigger a handshake.
- **D** ✅ is correct — aireplay-ng mode `-0` sends **deauthentication frames**. The `-0 5` means send 5 frames. `-a AA:BB:CC:DD:EE:FF` specifies the AP BSSID as the SOURCE (spoofed — frame appears to come from the legitimate AP). `-c 11:22:33:44:55:66` specifies the target client MAC. The client receives what looks like a legitimate deauthentication from its AP — disconnects immediately. The client's supplicant then automatically attempts to reconnect to the same SSID — initiating a new four-way handshake. airodump-ng captures this handshake and displays "WPA handshake: AA:BB:CC:DD:EE:FF" in the top right corner. 802.11 management frames are unauthenticated in WPA2 — any device can forge them.

---

### Q09

**What does the WPA2 four-way handshake MIC (Message Integrity Code) in Message 2 contain, and why does capturing it enable offline password cracking without further network access?**

- A) The MIC contains the plaintext PMK — attackers extract it directly to recover the PSK
- B) The MIC contains the client's password hash — attackers run it through a rainbow table
- C) The MIC contains the AP's certificate — attackers forge a matching certificate for evil twin
- D) ✅ The MIC is computed over handshake data using a key derived from the PMK — an offline attacker tests each dictionary word through PBKDF2(word+SSID)→PMK→PTK→MIC and compares the computed MIC with the captured MIC — a match reveals the correct password

**Explanation:**

- **A** is incorrect — the PMK is NEVER transmitted in any form during the four-way handshake. The entire design goal of WPA2's key exchange is to prove knowledge of the PMK without transmitting it. The MIC is a verification value — not the PMK itself.
- **B** is incorrect — the MIC is not a hash of the password. It is a keyed HMAC computed using the PTK (which is derived from the PMK, nonces, and MAC addresses) over handshake message fields. It cannot be reversed through a rainbow table.
- **C** is incorrect — WPA2 Personal mode does not use certificates. Certificate-based authentication is WPA Enterprise (EAP-TLS). The MIC is a symmetric HMAC — not a certificate signature.
- **D** ✅ is correct — the four-way handshake captures: ANonce, SNonce, AP MAC, Client MAC, and the MIC. These values are all an attacker needs for offline cracking. For each password candidate: `PMK = PBKDF2(candidate, SSID, 4096, 256)` → `PTK = PRF(PMK, ANonce, SNonce, AP_MAC, Client_MAC)` → `MIC_computed = HMAC-SHA1(PTK, handshake_data)`. Compare `MIC_computed` with `MIC_captured`. If equal → password found. This entire computation happens OFFLINE — no further Wi-Fi access needed after capturing the handshake. hashcat processes millions of candidates per second with GPU acceleration.

---

### Q10

**An attacker captures a WPA2 handshake and runs aircrack-ng with the rockyou.txt wordlist — but the password is not found. What ADDITIONAL cracking techniques can extend the attack without capturing a new handshake?**

- A) Capture a second handshake — the second handshake contains additional key material that makes cracking easier
- B) Switch to WEP cracking mode — WPA2 handshakes can be re-analyzed as WEP frames
- C) ✅ Use rule-based mutation in hashcat (append numbers/symbols, leetspeak substitutions, capitalize first letter) AND create a custom wordlist with CeWL targeting the organization's website — the same captured handshake file can be cracked indefinitely with different wordlists and rules
- D) Perform a PMKID attack — it generates a new hash type that aircrack-ng can crack faster than the handshake

**Explanation:**

- **A** is incorrect — multiple handshakes from the same network all derive MICs from the same underlying PSK. Capturing more handshakes does not provide additional key material or simplify cracking. Each handshake is independently crackable with the same wordlist approach.
- **B** is incorrect — WPA2 and WEP use completely different encryption and key exchange mechanisms. A WPA2 handshake cannot be converted to or analyzed as WEP traffic.
- **C** ✅ is correct — the captured `.cap` file is a fixed artifact. Cracking can be attempted repeatedly with different approaches: **(1) Rule-based attacks** in hashcat apply transformations to each wordlist entry (`-r rules/best64.rule`) — appending `123`, `!`, year numbers, capitalizing letters — covering passwords like `Password1!` or `Summer2024` derived from dictionary base words. **(2) CeWL** (`cewl https://company.com`) generates a custom wordlist from the organization's website — capturing company-specific terminology employees might use as passwords. **(3) Hybrid attacks** — combine dictionary word + brute force suffix. All of these use the same captured handshake file.
- **D** is incorrect — PMKID is an alternative CAPTURE method (no handshake needed) but it produces the same underlying PMK cracking problem. It does not generate a "new hash type" that makes cracking faster — both require the same PBKDF2 computation per password candidate.

---

### Q11

**Which of the following CORRECTLY describes why WPA2-Enterprise (802.1X) is more secure than WPA2-Personal (PSK) for a large organization with 500 employees?**

- A) WPA2-Enterprise uses AES-256 while WPA2-Personal uses AES-128 — the key length difference provides security
- B) WPA2-Enterprise eliminates the four-way handshake entirely — there is no handshake to capture
- C) ✅ WPA2-Enterprise uses per-user credentials authenticated via RADIUS — no shared password exists — compromise of one employee's credentials does not expose the network to all — and individual access can be revoked without changing network-wide keys
- D) WPA2-Enterprise uses a different frequency band — attackers cannot capture enterprise traffic on standard 2.4GHz equipment

**Explanation:**

- **A** is incorrect — the cipher suite (AES-128 CCMP) is the same for both WPA2 Personal and WPA2 Enterprise in standard WPA2. Enterprise mode does not automatically upgrade the cipher to AES-256 (that is WPA3 Enterprise). The security improvement is in authentication architecture — not cipher strength.
- **B** is incorrect — WPA2-Enterprise still uses a four-way handshake (EAPOL) after 802.1X authentication completes. The 802.1X phase establishes a per-user PMK, then the four-way handshake uses that PMK to derive session keys. The handshake still occurs — but the PMK is unique per user and per session — making offline dictionary attacks against the handshake impractical without knowing the individual user's credentials.
- **C** ✅ is correct — WPA2-Enterprise's key advantages for large organizations: **(1) No shared secret** — 500 employees do not all know a single Wi-Fi password that, if leaked, exposes the entire network. **(2) Per-user authentication** — each user authenticates with their individual credentials (certificate, username+password) against a RADIUS server. **(3) Individual revocation** — when an employee leaves, their RADIUS account is disabled — no network-wide password change needed. **(4) Audit trail** — RADIUS logs show who connected when. **(5) Per-session unique keys** — derived from individual authentication — one user's session cannot decrypt another's traffic.
- **D** is incorrect — 802.1X authentication operates at Layer 2 over the same 2.4GHz and 5GHz radio frequencies as Personal mode. Monitor mode on standard equipment captures Enterprise traffic identically to Personal mode traffic. The frequency band is not different.

---

### Q12

**During WPA2 cracking with hashcat, a tester uses `-m 22000` mode. What does this mode number represent and what file format is required?**

- A) Mode 22000 is for WEP 128-bit key recovery — requires a `.cap` file from airodump-ng
- B) Mode 22000 is for MD5 hash cracking — requires a file of MD5 hashes extracted from the web server
- C) Mode 22000 is for WPA3-SAE cracking — requires EAPOL frames from WPA3 authentication
- D) ✅ Mode 22000 is for WPA-PBKDF2-PMKID+EAPOL (unified WPA/WPA2 format) — requires a `.hc22000` file generated by `hcxpcapngtool` from a raw `.pcapng` or `.cap` capture file

**Explanation:**

- **A** is incorrect — WEP cracking is handled by aircrack-ng directly from `.cap` files using statistical IV analysis — not GPU-accelerated hashcat PBKDF2 computation. Hashcat mode 22000 is not for WEP.
- **B** is incorrect — MD5 hash cracking uses hashcat mode `-m 0` (MD5). Mode 22000 is specifically for WPA/WPA2 wireless password recovery.
- **C** is incorrect — WPA3-SAE uses a fundamentally different key exchange (Dragonfly/SAE) that is not vulnerable to the same offline dictionary attack model. Hashcat does not have a standard mode for cracking WPA3-SAE handshakes in the same way. The Dragonblood attacks use side-channel techniques — not direct hashcat processing.
- **D** ✅ is correct — hashcat mode `-m 22000` is the **unified WPA/WPA2 PBKDF2** cracking mode introduced in 2019 — replacing the older `-m 2500` (HCCAPX format). The workflow: raw `.cap` or `.pcapng` file from airodump-ng or hcxdumptool → `hcxpcapngtool -o hash.hc22000 capture.pcapng` → `hashcat -m 22000 hash.hc22000 wordlist.txt`. Mode 22000 handles both PMKID hashes and EAPOL four-way handshake hashes in the same file — the tester does not need to separate them.

---

## Questions 13–17 — WPA3 · WPS · PMKID

---

### Q13

**The WPS PIN authentication has an effective keyspace of only 11,000 combinations despite the PIN being 8 digits. What specific design flaw creates this reduction from 100,000,000 to 11,000?**

- A) WPS compresses the PIN using a proprietary algorithm that reduces it to 14-bit representation
- B) WPS PINs are generated from the AP's serial number — serial numbers follow predictable patterns
- C) WPS transmits the PIN over an unencrypted channel — attackers read it directly without guessing
- D) ✅ The AP validates the PIN in two independent halves — the first 4 digits (10,000 combinations) are validated separately before the last 3 digits (1,000 combinations, as the 8th digit is a checksum) — allowing the attacker to brute force each half independently: 10,000 + 1,000 = 11,000 maximum attempts

**Explanation:**

- **A** is incorrect — WPS does not use a compression algorithm on the PIN. The PIN is transmitted as part of the WPS EAP exchange — the reduction in keyspace is due to the validation protocol design, not encoding.
- **B** is incorrect — while some AP manufacturers do derive WPS PINs from serial numbers or MAC addresses (enabling even faster attacks), this is a secondary weakness. The fundamental 11,000-combination flaw described in Stefan Viehböck's 2011 paper exists in the protocol itself — regardless of how the PIN was generated.
- **C** is incorrect — WPS exchanges occur inside encrypted WPS EAP messages. The PIN itself is not transmitted in cleartext — the vulnerability is in the validation splitting logic, not plaintext transmission.
- **D** ✅ is correct — the WPS authentication EAP exchange validates the PIN in two separate M4 and M6 messages: first the AP confirms whether digits 1–4 are correct, then confirms whether digits 5–7 are correct (digit 8 is a checksum computed from digits 1–7 — not independently guessable). The AP sends a different error message for wrong first half vs wrong second half. This means: try 10,000 combinations for first half (find correct first half) → try 1,000 combinations for second half = **11,000 maximum attempts** total. At ~2 seconds per attempt: 11,000 × 2 = ~6 hours maximum.

---

### Q14

**The PMKID attack (discovered 2018) fundamentally changed WPA2-PSK cracking methodology. What makes it superior to the traditional four-way handshake capture approach?**

- A) PMKID attack breaks the AES-CCMP encryption directly — it does not require any key exchange capture
- B) PMKID attack works only against WPA3 — it is not applicable to WPA2
- C) PMKID attack requires the attacker to be inside the building to receive the PMKID value
- D) ✅ PMKID attack requires only ONE EAPOL frame from the AP obtained by requesting association — no connected client is needed and no deauthentication/reconnection timing is required — the PMKID is derived from the PMK and thus crackable offline with the same dictionary approach

**Explanation:**

- **A** is incorrect — PMKID does not break AES-CCMP encryption. It is an alternative way to obtain a crackable value derived from the PMK — functionally equivalent to capturing a handshake MIC but requiring less network interaction. AES itself is not broken.
- **B** is incorrect — PMKID attack specifically targets **WPA2-PSK**. WPA3-SAE does not use PMKIDs in the same way and is not vulnerable to this attack. The PMKID is specific to the RSN (Robust Security Network) element in WPA2 association frames.
- **C** is incorrect — the PMKID attack requires radio range contact with the AP — same as any wireless attack. It does not require physical access inside the building beyond being within Wi-Fi range (which can extend to parking lots, adjacent buildings, etc.).
- **D** ✅ is correct — the PMKID formula is: `PMKID = HMAC-SHA1(PMK, "PMK Name" || AP_MAC || Client_MAC)`. The AP includes the PMKID in the RSNE (RSN Information Element) of the first EAPOL frame (Message 1) during association. The attacker sends an association request → receives EAPOL Message 1 → extracts PMKID. No legitimate client needs to be connected. No deauthentication timing is needed. No waiting for a client to naturally authenticate. The extracted PMKID is then cracked offline: `PBKDF2(candidate, SSID) → PMK → HMAC-SHA1(PMK, "PMK Name" || APs || Client) == PMKID?`.

---

### Q15

**WPA3 Personal introduces SAE (Simultaneous Authentication of Equals). What property does SAE provide that WPA2-PSK fundamentally lacks — and why does this matter for historical traffic capture?**

- A) SAE provides stronger AES encryption — WPA2 uses AES-128 while WPA3 uses AES-256
- B) SAE eliminates the need for any encryption — authentication alone is sufficient for security
- C) SAE uses a RADIUS server for authentication — eliminating the shared password entirely
- D) ✅ SAE provides forward secrecy via ephemeral key pairs — each session generates unique keys — an attacker who records encrypted WPA3 traffic today and later learns the password CANNOT decrypt the historical traffic, unlike WPA2 where past traffic can be decrypted with the recovered PSK

**Explanation:**

- **A** is incorrect — WPA3 Personal uses AES-128 CCMP (same as WPA2) by default. WPA3 Enterprise uses AES-256 GCMP. Cipher strength improvement is not the primary advantage of SAE over PSK. The key advancement is forward secrecy.
- **B** is incorrect — SAE provides authentication AND key establishment for encryption. Encryption is still required and applied. SAE replaces the PSK-based key exchange — it does not eliminate encryption.
- **C** is incorrect — SAE is the WPA3 **Personal** mode — specifically for home/small office without RADIUS infrastructure. WPA3 Enterprise uses RADIUS + EAP-TLS. SAE itself replaces the shared password mechanism with a zero-knowledge proof — the password still exists but is never transmitted in any form that enables offline attack.
- **D** ✅ is correct — **forward secrecy** (also called Perfect Forward Secrecy, PFS) means each session uses freshly generated ephemeral cryptographic keys. In WPA2-PSK: `PMK = PBKDF2(PSK, SSID)` — this PMK is static. If an attacker records WPA2 traffic today and later cracks or steals the PSK, they can recalculate the PTK for any captured session (they have the nonces from the handshake) and decrypt all historical traffic. In WPA3-SAE: ephemeral ECDHE keys ensure that even with the password, previously used session keys cannot be reconstructed — historical traffic cannot be decrypted.

---

### Q16

**The Dragonblood vulnerabilities (2019) affected WPA3-SAE. Which of the following CORRECTLY describes the PRIMARY attack mechanism and its practical impact?**

- A) Dragonblood directly breaks the elliptic curve mathematics underlying SAE — WPA3 is permanently broken
- B) Dragonblood requires physical access to the access point to install malware on its firmware
- C) Dragonblood only affects WPA3 Enterprise — WPA3 Personal SAE is not vulnerable
- D) ✅ Dragonblood exploits timing and cache side-channels during the SAE commit phase — the processing time varies based on the password — an attacker measuring response times can narrow down password candidates enabling offline dictionary attack on patched-but-weak implementations

**Explanation:**

- **A** is incorrect — Dragonblood did not break the underlying elliptic curve mathematics. The vulnerability is in the IMPLEMENTATION of SAE — specifically timing and cache access patterns in how the password is processed. The math itself is sound. Fully patched implementations significantly mitigate the attack.
- **B** is incorrect — Dragonblood is a remote/wireless attack requiring only radio range access — no physical access to AP hardware. It is a protocol-level implementation vulnerability exploitable by any attacker within Wi-Fi range.
- **C** is incorrect — Dragonblood specifically targets WPA3 **Personal** SAE (the Dragonfly handshake). WPA3 Enterprise uses a different authentication mechanism (802.1X + EAP) and faces different vulnerabilities. The cache/timing side-channels are specific to the SAE commit phase used in Personal mode.
- **D** ✅ is correct — SAE's commit phase performs password-dependent operations on elliptic curve points. In vulnerable (unpatched) implementations, the TIME taken for these operations and the CACHE ACCESS PATTERNS vary based on bits of the password being processed. An attacker who can measure these timing differences across multiple authentication attempts can gain information about the password structure — reducing the search space for an offline dictionary attack. The attack does not reveal the password directly but enables distinguishing "closer" from "farther" password candidates. Patches implement constant-time operations to eliminate the timing signal.

---

### Q17

**A network administrator notices that their WPA2 router has a "WPS" button and WPS is enabled in the router configuration. What is the MOST appropriate security action and why?**

- A) Enable WPS PIN mode exclusively — the push-button method is less secure than PIN
- B) Update the WPS firmware — updated firmware patches the WPS PIN vulnerability completely
- C) Limit WPS to specific MAC addresses — restricting WPS to authorized devices eliminates the attack
- D) ✅ Disable WPS entirely — the PIN vulnerability (11,000 effective combinations) is a design flaw in the WPS protocol that cannot be fully patched — the only reliable fix is disabling WPS on all access points

**Explanation:**

- **A** is incorrect — WPS PIN mode is exactly the vulnerable mode. The Viehböck attack (11,000 combinations) and Pixie Dust attack target the PIN exchange specifically. Push-button (PBC) mode is significantly safer because it requires physical proximity to press the button — but the PIN mode attack surface exists as long as WPS is enabled.
- **B** is incorrect — while some firmware updates implement rate limiting and lockout for WPS PIN attempts (slowing brute force), the fundamental protocol design flaw (split PIN validation) cannot be eliminated through firmware. Some routers have been patched to lock WPS after repeated failures, but bypass techniques exist and physical resets often re-enable WPS. Complete disabling remains the only reliable mitigation.
- **C** is incorrect — MAC filtering for WPS access has the same weakness as general MAC filtering — MAC addresses are visible in plaintext in 802.11 frames. An attacker observing an authorized device's MAC can spoof it before initiating the WPS PIN attack. MAC filtering does not protect WPS.
- **D** ✅ is correct — the WPS PIN vulnerability is a **protocol-level design flaw** — not a bug in specific implementations. The split validation (first 4 digits, then last 3 digits) is inherent to the WPS specification (Wi-Fi Alliance). The Pixie Dust attack further demonstrates that many AP chipsets generate predictable WPS nonces — enabling offline PIN recovery in seconds. The Wi-Fi Alliance's own guidance recommends disabling WPS PIN functionality. The safest action is complete WPS disablement — users can connect normally by entering the WPA2 password.

---

## Questions 18–22 — Wireless Sniffing · SSID · MAC Spoofing

---

### Q18

**What is the key technical difference between placing a wired NIC in promiscuous mode and placing a wireless NIC in monitor mode?**

- A) Promiscuous mode requires root privileges; monitor mode works without elevated permissions
- B) Monitor mode only captures encrypted frames; promiscuous mode captures both encrypted and plaintext
- C) Promiscuous mode captures all IP packets on the subnet; monitor mode captures only 802.11 data frames
- D) ✅ Promiscuous mode (wired) disables MAC address filtering — capturing all Ethernet frames on the segment while remaining associated to the network; monitor mode (wireless) captures ALL 802.11 frame types (management, control, data) from any SSID without association to any network

**Explanation:**

- **A** is incorrect — both modes typically require elevated privileges (root on Linux, administrator on Windows). Privilege requirement is not the distinguishing technical difference.
- **B** is incorrect — both modes capture frames regardless of encryption status. A monitor mode interface captures encrypted WPA2 data frames and unencrypted management frames alike. Neither mode performs decryption — they capture what is transmitted.
- **C** is incorrect — promiscuous mode captures all Ethernet FRAMES at Layer 2 — not just IP packets. Monitor mode captures ALL 802.11 frame types — not just data frames. Monitor mode specifically captures management frames (beacons, probe requests, deauth frames) that are critical for wireless attack and analysis — wired promiscuous mode has no equivalent management frame concept.
- **D** ✅ is correct — the defining differences: **(1) Association**: promiscuous mode operates while connected to the network (associated); monitor mode captures frames without associating to any network. **(2) Frame types**: monitor mode captures management frames (beacons, probes, deauth), control frames (ACK, RTS, CTS), and data frames — giving complete 802.11 visibility. Promiscuous mode captures Ethernet frames — no management frame equivalent exists on wired networks. **(3) Scope**: monitor mode captures from ALL SSIDs/BSSIDs in radio range simultaneously — not just from one associated network.

---

### Q19

**A security analyst runs airodump-ng and sees the following entry:**

    BSSID              ESSID
    77:88:99:AA:BB:CC  <length: 8>

**What does `<length: 8>` indicate, and what technique reveals the actual SSID?**

- A) The SSID is 8 characters of random noise — the AP is malfunctioning and broadcasting corrupt beacons
- B) The SSID contains 8 special characters — airodump-ng cannot display them but they do not affect connectivity
- C) The AP is using WPA3 encryption — the length field indicates 256-bit key usage
- D) ✅ The AP has SSID hiding enabled — the beacon frames have an empty/null SSID field — airodump-ng detects the hidden network and shows the SSID's character count (8) — the actual SSID is revealed when any client sends a probe request or association request containing the hidden SSID

**Explanation:**

- **A** is incorrect — `<length: 8>` is airodump-ng's specific notation for a **hidden SSID network** — it is not a malfunction indicator. The AP is functioning correctly but has SSID broadcast disabled. The character count is determined from the length field in the beacon's SSID information element.
- **B** is incorrect — special characters would be displayed by airodump-ng (possibly as hex or Unicode representations) — they would not cause the `<length: N>` notation. The `<length:>` display specifically indicates a null/empty SSID in the beacon frame.
- **C** is incorrect — WPA3 encryption type is shown in the ENC/CIPHER/AUTH columns of airodump-ng — not as ESSID content. SSID hiding is independent of the encryption protocol used.
- **D** ✅ is correct — when SSID hiding is enabled, the AP's beacon frames contain an empty SSID information element (or null bytes). airodump-ng detects the network exists (from beacons, BSSID, signal strength) but shows `<length: 8>` instead of the SSID name — indicating a hidden network with an 8-character SSID. Reveal methods: **(1) Passive**: wait for an existing client to send a directed probe request (contains SSID) or association request — both are captured by airodump-ng revealing the SSID. **(2) Active**: deauthenticate a connected client with `aireplay-ng -0 1` — it reconnects and probe requests reveal the SSID.

---

### Q20

**Why is SSID hiding (SSID cloaking) considered security theater rather than a genuine security control?**

- A) SSID hiding only works on 2.4GHz networks — 5GHz networks always broadcast SSIDs
- B) SSID hiding is disabled automatically when WPA2 is enabled — the protocols are incompatible
- C) SSID hiding prevents connections — legitimate users also cannot connect to hidden networks
- D) ✅ The SSID is transmitted in plaintext in probe requests (when clients search for the network), association requests (when clients join), and probe responses — passive monitoring with airodump-ng reveals hidden SSIDs within seconds of any client activity, making the "hiding" purely superficial

**Explanation:**

- **A** is incorrect — SSID hiding operates identically on 2.4GHz and 5GHz bands. Both suppress the SSID from beacon frames. The radio frequency band does not affect SSID hiding behaviour.
- **B** is incorrect — SSID hiding and WPA2 are independent features. A network can be WPA2-encrypted with hidden SSID, WPA2-encrypted with visible SSID, open with hidden SSID, or any other combination. There is no incompatibility.
- **C** is incorrect — hidden networks are fully connectable by legitimate users. The client must know the SSID and enter it manually instead of seeing it in the network list. The connection process (authentication, handshake) is identical to visible SSIDs.
- **D** ✅ is correct — SSID hiding only removes the SSID from **beacon frames** — the periodic broadcasts the AP sends proactively. The SSID remains present in: **(1) Probe requests**: mobile devices that previously connected to the network continuously broadcast probe requests containing the SSID as they search for it. **(2) Probe responses**: when an AP responds to any probe request (including directed probes from clients that know the SSID). **(3) Association requests**: when any client joins the network. airodump-ng captures all three frame types — the hidden SSID appears immediately when any client is active or when deauthentication forces reconnection.

---

### Q21

**A target network uses MAC address filtering — only allowing specific MAC addresses to connect. An attacker has captured the following from airodump-ng:**

    STATION            Associated BSSID
    11:22:33:44:55:66  AA:BB:CC:DD:EE:FF

**What two commands accomplish MAC spoofing to bypass this filter?**

- A) `iptables -t nat -A OUTPUT -m mac --mac-source 11:22:33:44:55:66 -j MASQUERADE` followed by `iwconfig wlan0 ap AA:BB:CC:DD:EE:FF`
- B) `aircrack-ng --spoof-mac 11:22:33:44:55:66 wlan0` followed by `aireplay-ng -1 0 -a AA:BB:CC:DD:EE:FF wlan0mon`
- C) `wpa_supplicant -mac 11:22:33:44:55:66 wlan0` followed by connecting normally through NetworkManager
- D) ✅ `ip link set wlan0 down` followed by `ip link set wlan0 address 11:22:33:44:55:66` followed by `ip link set wlan0 up` — this changes the NIC's presented MAC to the captured authorized client MAC — the AP sees an allowed MAC and permits connection

**Explanation:**

- **A** is incorrect — `iptables` is a packet filter operating at Layer 3/4 — it cannot change the Layer 2 MAC address presented in 802.11 frames. `iwconfig ap` sets the AP to connect to (BSSID) — not the local MAC address. These commands do not accomplish MAC spoofing.
- **B** is incorrect — `aircrack-ng` is a cracking tool — it does not have a `--spoof-mac` flag for interface configuration. `aireplay-ng -1` performs fake authentication — a separate step. Neither command changes the local interface MAC address.
- **C** is incorrect — `wpa_supplicant` does not have a `-mac` flag for MAC address spoofing. wpa_supplicant manages WPA authentication — not MAC address configuration. NetworkManager may randomize MACs but cannot be directed to a specific target MAC this way.
- **D** ✅ is correct — the standard Linux MAC spoofing procedure: **(1)** `ip link set wlan0 down` — take the interface down (required to change MAC). **(2)** `ip link set wlan0 address 11:22:33:44:55:66` — set the MAC to the captured authorized client MAC. **(3)** `ip link set wlan0 up` — bring the interface back up. The NIC now presents `11:22:33:44:55:66` in all frames. The AP checks this against its allowed list, finds a match, and grants connection. Alternative: `macchanger -m 11:22:33:44:55:66 wlan0`. Total time: under 30 seconds — demonstrating why MAC filtering is not a security control.

---

### Q22

**Which statement MOST accurately explains why MAC filtering provides no meaningful security against a motivated wireless attacker?**

- A) Modern wireless routers do not actually enforce MAC filtering — it is a cosmetic setting only
- B) MAC filtering only works on 2.4GHz — an attacker using 5GHz bypasses the filter automatically
- C) MAC filtering requires the attacker to physically unplug an authorized device first
- D) ✅ 802.11 frame headers — including source and destination MAC addresses — are transmitted unencrypted in every frame, even on WPA2-encrypted networks — any device in monitor mode passively reads all authorized client MACs and can spoof any of them with a single command in under 30 seconds

**Explanation:**

- **A** is incorrect — MAC filtering is an actual enforced feature on all consumer and enterprise wireless routers that support it. The AP genuinely checks association requests against the allowed MAC list. The problem is not that it is unenforced — it is that it is trivially bypassed.
- **B** is incorrect — MAC filtering operates at Layer 2 and applies identically on both 2.4GHz and 5GHz bands. The frequency band does not affect MAC address handling. Dual-band APs enforce MAC filtering on all configured bands simultaneously.
- **C** is incorrect — MAC spoofing does not require unplugging or disrupting the legitimate device. The attacker simply spoofs the MAC and connects. If the legitimate device is also connected, a MAC collision occurs — which the attacker resolves by first deauthenticating the legitimate device. Physical access is never required.
- **D** ✅ is correct — this is the fundamental reason MAC filtering fails. WPA2 encrypts the DATA payload but the 802.11 frame **header** — including MAC addresses — is always in plaintext. Even on a fully encrypted WPA2 network, `airodump-ng` in monitor mode displays every client MAC address in the STATION column. An attacker identifies an authorized MAC (`11:22:33:44:55:66`) and clones it with `ip link set wlan0 address 11:22:33:44:55:66`. The entire attack takes under 30 seconds from observation to bypass.

---

## Questions 23–26 — Wireless Attack Techniques

---

### Q23

**An attacker sets up a wireless AP with the SSID "AirportFreeWiFi" on channel 1 with a transmit power higher than the legitimate airport AP. The attacker also runs a captive portal showing "Enter your Wi-Fi password to continue browsing." What attack is this and what TWO pieces of information does the attacker aim to capture?**

- A) Rogue AP attack — attacker captures the corporate VPN credentials and employees' Active Directory passwords
- B) WPS brute force — the captive portal collects device serial numbers used to compute WPS PINs
- C) ✅ Evil twin attack — the attacker aims to capture (1) the WPA2 passphrase when victims enter it into the captive portal believing they need to "re-authenticate" and (2) all HTTP/HTTPS traffic for credential harvesting via MITM
- D) KRACK attack — the captive portal enables key reinstallation by tricking clients into repeating handshake message 3

**Explanation:**

- **A** is incorrect — while an evil twin in a corporate environment could capture corporate credentials, the scenario describes a public airport setting with a social engineering captive portal. The immediate targets are the Wi-Fi password and browsing credentials — not specifically VPN/AD credentials (though those may be captured too).
- **B** is incorrect — WPS brute force requires no captive portal — it directly targets the AP's WPS PIN exchange via reaver/bully. Captive portals have no relationship to WPS PIN computation.
- **C** ✅ is correct — this is a textbook **evil twin attack** with captive portal social engineering. The evil twin broadcasts the same SSID as the legitimate AP with higher power — causing clients to prefer and connect to it. The captive portal claiming "enter your Wi-Fi password to continue" is social engineering targeting the WPA2 password — users who have just connected expect to need authentication. Captured information: **(1) WPA2 passphrase** — when victims enter it in the fake portal — giving the attacker the real network password. **(2) All cleartext traffic** — all HTTP requests, DNS queries, and any unencrypted content flowing through the evil twin's internet connection.
- **D** is incorrect — KRACK attacks the four-way handshake by retransmitting Message 3 — this is a protocol-level cryptographic attack executed invisibly. It does not involve a user-visible captive portal. KRACK does not require user interaction beyond normal connection.

---

### Q24

**The 802.11 deauthentication attack exploits a fundamental weakness in the 802.11 protocol. What specifically makes forging deauthentication frames possible — and what IEEE amendment addresses this vulnerability?**

- A) Deauthentication frames are encrypted but the encryption key is always the same default value; 802.11i introduced AES for management frames
- B) Deauthentication frames use a predictable sequence number that attackers can calculate; 802.11n increased the sequence number space to prevent prediction
- C) Deauthentication frames are transmitted on a reserved channel that APs must accept from any source; 802.11ac sealed this channel
- D) ✅ 802.11 management frames including deauthentication are unauthenticated and unencrypted by default in WPA2 — any station can forge them using any BSSID as source — IEEE 802.11w (Protected Management Frames / PMF) cryptographically protects management frames — mandatory in WPA3

**Explanation:**

- **A** is incorrect — management frames in WPA2 are not encrypted at all — there is no default encryption key that could be "always the same." 802.11i (the security amendment underlying WPA2) addressed data frame encryption — not management frame authentication. 802.11w (a separate amendment) addressed management frame protection.
- **B** is incorrect — sequence number prediction is not the attack mechanism. Even if sequence numbers were unpredictable, the deauthentication attack works because management frames lack any authentication mechanism — not because of sequence number predictability.
- **C** is incorrect — there is no "reserved channel" for management frames in 802.11. Management frames use the same radio channel as data frames. 802.11ac improved throughput and spectrum usage — it did not add management frame security.
- **D** ✅ is correct — the root cause: in standard 802.11 (through WPA2), **management frames have no source authentication**. Any 802.11 device can construct a deauthentication frame with any arbitrary source BSSID and transmit it. The receiving client cannot verify whether the deauthentication came from the real AP or from an attacker. **IEEE 802.11w** (Management Frame Protection, also called Protected Management Frames / PMF) adds cryptographic integrity protection to unicast management frames including deauthentication and disassociation. 802.11w is optional in WPA2 but **mandatory in WPA3** — making WPA3 networks resistant to deauthentication attacks.

---

### Q25

**The KRACK (Key Reinstallation Attack) vulnerability was disclosed in October 2017. Which component of WPA2 was vulnerable and what was the cryptographic consequence of the attack?**

- A) KRACK broke the AES-CCMP cipher — attackers could decrypt any WPA2-encrypted frame without knowing the key
- B) KRACK exploited the WPS PIN validation flaw — it recovered the PIN in 11,000 attempts
- C) KRACK poisoned the PMKID — causing the AP to generate predictable session keys
- D) ✅ KRACK exploited the four-way handshake by retransmitting Message 3 — forcing the client to reinstall an already-used PTK and reset nonce counters — nonce reuse with AES-CCMP allows replay and decryption of frames; with TKIP also allows forgery

**Explanation:**

- **A** is incorrect — KRACK did not break the AES-CCMP cipher itself. AES remains cryptographically unbroken. The vulnerability was in the handshake state machine — not the encryption algorithm. AES-CCMP is vulnerable to nonce reuse (all CTR-mode ciphers are) but breaking AES itself is different from exploiting nonce reuse.
- **B** is incorrect — the WPS PIN flaw is a separate vulnerability (Viehböck 2011). KRACK targets the four-way handshake — a completely different aspect of WPA2. They are independent vulnerabilities.
- **C** is incorrect — KRACK does not affect PMKID. PMKID is a value derived from the PMK for identification purposes. KRACK targets the key installation phase of the four-way handshake — not the PMKID or PMK derivation.
- **D** ✅ is correct — KRACK's mechanism: an attacker positions as MITM, intercepts the four-way handshake, and **retransmits Message 3** (which contains the encrypted GTK). The WPA2 specification requires clients to reinstall the PTK upon receiving a retransmitted Message 3 — resetting the nonce (packet number) counter to zero. With the same PTK and a reused nonce, AES-CCMP's counter-mode encryption produces the same keystream — enabling frame decryption and replay. With TKIP (used in WPA), nonce reuse additionally allows packet forgery. The fix: clients should track whether PTK installation already occurred and reject retransmitted Message 3 after first installation. All major platforms patched within weeks of October 2017 disclosure.

---

### Q26

**A Karma attack differs from a standard evil twin. Which scenario CORRECTLY describes a Karma attack and identifies which device behaviour it exploits?**

- A) Karma attacks only work against WPA3 networks — they exploit the SAE dragonfly commit phase to extract passwords
- B) Karma attacks require physical proximity to the target device — the attacker must be within Bluetooth range
- C) Karma attacks target network switches — the attacker sends gratuitous ARP replies with spoofed MAC addresses
- D) ✅ Karma attacks respond to ANY probe request SSID — when a mobile device probes for previously connected networks ("HomeWiFi", "CoffeeShop") the Karma AP responds claiming to be that network — the device auto-connects — enabling MITM without knowing the victim's specific target SSID in advance

**Explanation:**

- **A** is incorrect — Karma attacks are not specific to WPA3. They exploit the 802.11 probe request mechanism — applicable to any 802.11 network. WPA3's SAE dragonfly is targeted by Dragonblood (a separate vulnerability class).
- **B** is incorrect — Karma attacks operate over 802.11 Wi-Fi radio — the same range as standard Wi-Fi (tens of metres). Bluetooth range (~10m) and protocol are irrelevant. Karma requires only being within Wi-Fi radio range of the target device.
- **C** is incorrect — Karma attacks are wireless attacks on 802.11 probe requests. Gratuitous ARP is a Layer 2 wired Ethernet technique used in ARP poisoning attacks. These are completely different attack vectors.
- **D** ✅ is correct — mobile devices (phones, laptops) continuously send 802.11 **probe request frames** broadcasting the SSIDs of every network they have ever connected to — trying to automatically reconnect to known networks. In a standard environment, only the real AP with matching SSID responds to directed probes. The **Karma attack** configures an AP to **respond positively to ANY probe request** — regardless of the SSID requested. When a victim's phone probes for "HomeWiFi", the Karma AP claims to be "HomeWiFi" → the phone connects automatically without user interaction → MITM. The attacker does not need to know the victim's specific SSIDs in advance.

---

## Questions 27–28 — Securing Wireless & Extra Notes

---

### Q27

**A security consultant recommends the following wireless security configuration to a company. Rank the four options from MOST to LEAST secure and identify the correct order:**

    1. WPA3 Enterprise with EAP-TLS
    2. WPA2 Personal with passphrase "Summer2024!"
    3. WPA2 Enterprise with EAP-PEAP
    4. WEP 128-bit with MAC filtering enabled

- A) 4 → 3 → 2 → 1 (WEP is most secure because it adds MAC filtering)
- B) 2 → 1 → 3 → 4 (WPA2 Personal is more practical than Enterprise)
- C) 1 → 2 → 3 → 4 (WPA3 Enterprise first but WPA2 Personal beats WPA2 Enterprise)
- D) ✅ 1 → 3 → 2 → 4 (WPA3 Enterprise with mutual cert auth is strongest; WPA2 Enterprise with server cert + per-user credentials next; WPA2 Personal with weak common password next; WEP with MAC filtering is completely broken and least secure)

**Explanation:**

- **A** is incorrect — MAC filtering provides zero additional security (MACs in plaintext — spoofable in 30 seconds). WEP is completely broken regardless of key length or supplementary controls. WEP + MAC filtering is the WEAKEST option.
- **B** is incorrect — WPA2 Personal with a weak password ("Summer2024!" is a common password-spray target and likely in rockyou.txt) is weaker than WPA2 Enterprise. Enterprise eliminates the shared password risk entirely, provides per-user credentials, and maintains central revocation capability.
- **C** is incorrect — WPA2 Personal with "Summer2024!" is weaker than WPA2 Enterprise because: the password is a common pattern (season + year + punctuation — high probability of dictionary attack success), all 500 employees share the same credential (one leak exposes all), and individual access cannot be revoked. WPA2 Enterprise beats Personal for organizational use regardless of password strength.
- **D** ✅ is correct — security ranking: **(1) WPA3 Enterprise + EAP-TLS**: strongest — AES per WPA3 standards, mandatory mutual certificate authentication (both client AND server must present valid certificates), per-user unique keys, forward secrecy, 192-bit security suite. **(2) WPA2 Enterprise + EAP-PEAP**: strong — server certificate prevents connection to evil twins, per-user username/password via RADIUS, individual revocation, audit trail — no shared password. **(3) WPA2 Personal + "Summer2024!"**: acceptable cipher (AES-CCMP) but weak shared password that may be dictionary-crackable and is shared among all users. **(4) WEP 128-bit + MAC filtering**: completely broken — cracckable in under 5 minutes regardless of key length — MAC filtering adds no security.

---

### Q28

**Under the Indian Wireless Telegraphy Act 1933 and IT Act 2000, an attacker sets up an evil twin AP (unauthorized wireless transmitter) and uses it to capture banking credentials from victims connecting to the fake AP. Which combination of legal provisions applies and what are the respective penalties?**

- A) Only IT Act Section 66 applies — penalty up to 3 years + ₹5 lakh fine
- B) Only Wireless Telegraphy Act Section 6 applies — penalty up to 3 years + ₹1,000 fine
- C) Only DPDPA 2023 applies — penalty up to ₹250 crore for data breach
- D) ✅ Multiple provisions apply simultaneously: Wireless Telegraphy Act 1933 S.6 (unlicensed transmitter — up to 3 years + fine), IT Act S.66 (criminal unauthorized access), IT Act S.66C (identity theft via captured credentials), IT Act S.66D (cheating by personation), and IPC S.420 (fraud from captured banking credentials — up to 7 years + fine)

**Explanation:**

- **A** is incorrect — IT Act Section 66 applies but is not the only provision. Operating an unauthorized wireless transmitter (the evil twin AP itself) is an additional and separate offence under the Wireless Telegraphy Act 1933 — independent of the IT Act provisions for the access and fraud aspects.
- **B** is incorrect — the Wireless Telegraphy Act addresses the unlicensed transmission offence but does not cover the unauthorized computer access, identity theft, or financial fraud aspects of the attack. Multiple laws are violated by different aspects of the same attack.
- **C** is incorrect — DPDPA 2023 applies when personal data is breached, which is relevant here, but it is a civil/regulatory penalty applied to the DATA FIDUCIARY (the organization holding data) — not directly to the criminal attacker. The criminal offences under IT Act and IPC are the primary provisions against the attacker.
- **D** ✅ is correct — the evil twin attack violates multiple provisions simultaneously: **(1) Wireless Telegraphy Act 1933 S.6**: operating an unauthorized wireless transmitter (the evil twin AP) without a licence — up to 3 years + ₹1,000 fine. **(2) IT Act S.66**: criminal unauthorized access to computer systems of victims connecting through the evil twin — up to 3 years + ₹5 lakh. **(3) IT Act S.66C**: using captured session tokens/credentials to steal victims' digital identity — up to 3 years + ₹1 lakh. **(4) IT Act S.66D**: using the captured credentials/sessions to cheat by personation (impersonating victim at their bank) — up to 3 years + ₹1 lakh. **(5) IPC S.420**: financial fraud via captured banking credentials — up to **7 years + fine** (highest imprisonment term among these provisions). In Indian law, multiple sections can be charged simultaneously for a single complex attack.

---

## Answer Key

| Q# | Answer | Topic Area |
|---|---|---|
| Q01 | D | WEP IV weakness — 24-bit IV — IV reuse — root cause |
| Q02 | C | WEP 64-bit vs 128-bit — same 24-bit IV — both broken equally |
| Q03 | D | aireplay-ng -3 — ARP request replay — IV generation |
| Q04 | D | PTW attack vs FMS — all packets vs weak IVs — 35,000 frames |
| Q05 | D | Insufficient IVs — ARP replay injection as solution |
| Q06 | C | WEP Shared Key Auth — known plaintext — keystream derivation |
| Q07 | B | PBKDF2 PMK derivation — SSID as salt — rainbow table SSID-specific |
| Q08 | D | aireplay-ng -0 — deauthentication — forces reconnect — handshake capture |
| Q09 | D | Four-way handshake MIC — offline cracking — no further network access |
| Q10 | C | Extended cracking — hashcat rules + CeWL — same captured handshake |
| Q11 | C | WPA2 Enterprise vs Personal — per-user credentials — no shared secret |
| Q12 | D | hashcat -m 22000 — unified WPA format — hcxpcapngtool |
| Q13 | D | WPS PIN split validation — 10,000 + 1,000 = 11,000 combinations |
| Q14 | D | PMKID attack — no client needed — single EAPOL frame |
| Q15 | D | WPA3 SAE forward secrecy — past traffic cannot be decrypted |
| Q16 | D | Dragonblood — timing + cache side-channel — SAE commit phase |
| Q17 | D | Disable WPS entirely — protocol design flaw — no patch fixes it |
| Q18 | D | Monitor mode vs promiscuous mode — all frame types vs Ethernet frames |
| Q19 | D | Hidden SSID — `<length: 8>` — revealed by probe/association requests |
| Q20 | D | SSID hiding failure — probe/association requests reveal SSID |
| Q21 | D | MAC spoofing commands — ip link set address — bypass MAC filtering |
| Q22 | D | MAC filtering failure — 802.11 headers in plaintext — passive capture |
| Q23 | C | Evil twin + captive portal — captures WPA2 password + traffic |
| Q24 | D | Deauthentication attack — unauthenticated management frames — 802.11w PMF |
| Q25 | D | KRACK — Message 3 retransmission — nonce reuse — patchable |
| Q26 | D | Karma attack — responds to any probe — auto-connect exploitation |
| Q27 | D | Security hierarchy — WPA3 Enterprise > WPA2 Enterprise > WPA2 PSK > WEP |
| Q28 | D | Multiple provisions — Wireless Telegraphy Act + IT Act + IPC |

---