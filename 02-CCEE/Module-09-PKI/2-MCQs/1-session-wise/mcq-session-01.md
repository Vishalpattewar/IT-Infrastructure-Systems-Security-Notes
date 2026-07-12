
# MCQ Session 01 — Information Security, Security Attacks & Threats

## 📑 Table of Contents
- [Instructions](#instructions)
- [MCQs 1–10 — CIA, Properties, Models](#mcqs-110--cia-properties-models)
- [MCQs 11–17 — Attacks Classification](#mcqs-1117--attacks-classification)
- [MCQs 18–22 — Controls, Risk, Frameworks](#mcqs-1822--controls-risk-frameworks)
- [MCQs 23–25 — Extra Notes: STRIDE, CVE/CVSS, X.800](#mcqs-2325--extra-notes-stride-cvecvss-x800)

---

## Instructions

- 25 MCQs — drawn from core syllabus AND 📌 Extra Notes of Session 01
- 4 options per question
- ✅ marks the correct answer
- Full explanation after every question — including **why each wrong option is wrong**
- Questions are deliberately tricky — read every option carefully

---

## MCQs 1–10 — CIA, Properties, Models

---

**Q1. Which property of the CIA Triad is PRIMARILY violated when an attacker performs a Denial of Service (DoS) attack?**

- A) Confidentiality
- B) Integrity
- C) Non-repudiation
- D) Availability ✅

> **Explanation:**
> - ✅ **D — Availability:** DoS attacks flood a system with requests, preventing legitimate users from accessing the service — directly targeting Availability.
> - ❌ **A — Confidentiality:** No data is disclosed in a DoS attack. Confidentiality is violated by sniffing or unauthorized access.
> - ❌ **B — Integrity:** Integrity is violated by data modification or tampering. DoS does not alter data.
> - ❌ **C — Non-repudiation:** Non-repudiation is about denying participation in communication — not about service disruption.

---

**Q2. A hospital's patient records database is encrypted and access-controlled, but the backup server fails during a ransomware attack. Which CIA property is ultimately compromised?**

- A) Confidentiality
- B) Integrity
- C) Availability ✅
- D) Non-repudiation

> **Explanation:**
> - ✅ **C — Availability:** Even though confidentiality and integrity may be intact (data is encrypted), the inability to access records when needed is a direct Availability failure. Ransomware primarily targets Availability by making data inaccessible.
> - ❌ **A — Confidentiality:** The data is encrypted — no unauthorized disclosure occurred.
> - ❌ **B — Integrity:** Ransomware encrypts but does not necessarily alter the logical content of the data.
> - ❌ **D — Non-repudiation:** No communication denial is involved here.

---

**Q3. An attacker modifies a financial transaction record in a database without authorization. Which CIA property is violated?**

- A) Availability
- B) Confidentiality
- C) Integrity ✅
- D) Authentication

> **Explanation:**
> - ✅ **C — Integrity:** Unauthorized modification of data directly violates Integrity — the assurance that data remains accurate and unaltered.
> - ❌ **A — Availability:** The database is still accessible; no disruption occurred.
> - ❌ **B — Confidentiality:** The attacker modified, not disclosed, the data.
> - ❌ **D — Authentication:** Authentication is not a CIA property — it is an extended security property. Even if authentication was bypassed to reach the database, the CIA property violated by the modification itself is Integrity.

---

**Q4. Donn Parker's Parkerian Hexad extends the CIA Triad by adding three additional properties. Which of the following is NOT one of those three additions?**

- A) Possession
- B) Utility
- C) Non-repudiation ✅
- D) Authenticity

> **Explanation:**
> - ✅ **C — Non-repudiation:** Non-repudiation is a widely recognized security property but it is NOT one of the three additions in the Parkerian Hexad. The Hexad adds Possession/Control, Authenticity, and Utility to the CIA Triad.
> - ❌ **A — Possession:** Possession (also called Control) IS one of the three additions — it refers to ownership/control of the physical medium.
> - ❌ **B — Utility:** Utility IS one of the three additions — data in an unusable form (e.g., encrypted with a lost key) has no utility.
> - ❌ **D — Authenticity:** Authenticity IS one of the three additions — it refers to data being genuine and unforged.

---

**Q5. You have lost an encrypted USB drive containing sensitive data. The encryption is strong and unbroken. Which Parkerian Hexad property is violated even though Confidentiality remains intact?**

- A) Utility
- B) Integrity
- C) Authenticity
- D) Possession ✅

> **Explanation:**
> - ✅ **D — Possession:** Losing physical control of a medium violates Possession, regardless of whether the data can be read. The organization no longer controls the physical asset.
> - ❌ **A — Utility:** Utility is violated when data cannot be used (e.g., encryption key lost). The encryption here is intact and keys are presumably held — the data remains usable IF recovered.
> - ❌ **B — Integrity:** No modification of data occurred — Integrity is intact.
> - ❌ **C — Authenticity:** Authenticity refers to data being genuine — not about physical possession of the medium.

---

**Q6. The McCumber Cube has three axes: Security Goals, Information States, and Security Countermeasures. How many total cells does the McCumber Cube contain?**

- A) 9
- B) 12
- C) 18
- D) 27 ✅

> **Explanation:**
> - ✅ **D — 27:** Each axis has exactly 3 values: Goals (CIA = 3), Information States (Storage, Transmission, Processing = 3), Countermeasures (Policy, Human Factors, Technology = 3). 3 × 3 × 3 = **27 cells**.
> - ❌ **A — 9:** 9 would be 3 × 3 — this ignores the third axis entirely.
> - ❌ **B — 12:** Not a valid product of any combination of the three axes.
> - ❌ **C — 18:** 18 = 3 × 3 × 2 — incorrect; all three axes have 3 values each.

---

**Q7. Which of the following correctly represents the three Information States in the McCumber Cube?**

- A) Confidentiality, Integrity, Availability
- B) Storage, Transmission, Processing ✅
- C) Policies, Human Factors, Technology
- D) Prevention, Detection, Correction

> **Explanation:**
> - ✅ **B — Storage, Transmission, Processing:** These are the three information states in the McCumber Cube — data at rest, data in transit, and data being actively used.
> - ❌ **A — CIA:** This is the Security Goals axis of the cube, not the Information States axis.
> - ❌ **C — Policies, Human Factors, Technology:** This is the Security Countermeasures axis.
> - ❌ **D — Prevention, Detection, Correction:** These are Security Control functions — not McCumber Cube axes.

---

**Q8. Which of the following BEST describes the relationship between Threat, Vulnerability, and Risk?**

- A) Risk = Threat + Vulnerability
- B) Risk = Threat × Vulnerability × Impact ✅
- C) Risk = Vulnerability / Impact
- D) Risk = Threat × Impact

> **Explanation:**
> - ✅ **B:** The complete risk formula includes all three components — a threat alone or a vulnerability alone does not constitute risk. Impact determines the magnitude of harm. Risk = Threat × Vulnerability × Impact.
> - ❌ **A:** Addition is incorrect — risk is a multiplicative relationship. If any factor is zero, risk is zero.
> - ❌ **C:** Division by Impact is logically wrong — higher impact means higher risk, not lower.
> - ❌ **D:** This formula omits Vulnerability — a system with no vulnerability cannot be attacked regardless of threat.

---

**Q9. An organization has applied security controls to reduce risk but acknowledges some risk still remains. What is the term for this remaining risk?**

- A) Accepted Risk
- B) Transferred Risk
- C) Residual Risk ✅
- D) Inherent Risk

> **Explanation:**
> - ✅ **C — Residual Risk:** After applying all controls, the risk that remains is called Residual Risk. It cannot be fully eliminated.
> - ❌ **A — Accepted Risk:** Accepted Risk is a risk treatment decision — the organization deliberately chooses to accept it. Residual risk may exist even without a deliberate acceptance decision.
> - ❌ **B — Transferred Risk:** Transfer means shifting risk to a third party (e.g., insurance). This is a treatment strategy, not the remaining risk after controls.
> - ❌ **D — Inherent Risk:** Inherent Risk is the raw risk BEFORE any controls are applied. Residual Risk is what is left AFTER controls.

---

**Q10. Which of the following correctly maps the DAD Triad to the CIA Triad?**

- A) Disclosure → Integrity, Alteration → Confidentiality, Destruction → Availability
- B) Disclosure → Confidentiality, Alteration → Integrity, Destruction → Availability ✅
- C) Disclosure → Availability, Alteration → Integrity, Destruction → Confidentiality
- D) Disclosure → Confidentiality, Alteration → Availability, Destruction → Integrity

> **Explanation:**
> - ✅ **B:** The DAD Triad is the attacker's mirror of CIA — Disclosure attacks Confidentiality, Alteration attacks Integrity, Destruction/Denial attacks Availability.
> - ❌ **A:** This swaps Disclosure and Alteration — Disclosure is about revealing information (Confidentiality), not modifying it (Integrity).
> - ❌ **C:** Disclosure has nothing to do with Availability.
> - ❌ **D:** Alteration modifies data (Integrity), not disrupts access (Availability).

---

## MCQs 11–17 — Attacks Classification

---

**Q11. Which of the following is a PASSIVE attack?**

- A) Replay Attack
- B) Masquerade Attack
- C) Traffic Analysis ✅
- D) Denial of Service

> **Explanation:**
> - ✅ **C — Traffic Analysis:** Traffic Analysis is a passive attack — the attacker observes communication patterns (timing, volume, source/destination) without modifying any data.
> - ❌ **A — Replay Attack:** A replay attack resends previously captured valid data — this is an ACTIVE attack that affects integrity/authentication.
> - ❌ **B — Masquerade Attack:** Pretending to be a legitimate entity is an ACTIVE attack.
> - ❌ **D — Denial of Service:** Disrupting service availability is clearly an ACTIVE attack.

---

**Q12. An attacker encrypts all traffic between two parties but still determines that heavy communication occurs between a CEO and a lawyer every Friday. Which attack is this?**

- A) Eavesdropping
- B) Traffic Analysis ✅
- C) Session Hijacking
- D) MitM Attack

> **Explanation:**
> - ✅ **B — Traffic Analysis:** Even with encrypted content, the attacker extracts intelligence from communication patterns — timing, frequency, endpoints, volume. This is the textbook definition of Traffic Analysis.
> - ❌ **A — Eavesdropping:** Eavesdropping requires capturing the actual content of communication. Here the content is encrypted and unread.
> - ❌ **C — Session Hijacking:** This involves taking over an active session — no session takeover is happening here.
> - ❌ **D — MitM:** MitM requires intercepting and potentially altering messages — the attacker here is only observing metadata.

---

**Q13. Which X.800 security mechanism is specifically designed to counter traffic analysis attacks?**

- A) Encipherment
- B) Routing Control
- C) Traffic Padding ✅
- D) Notarization

> **Explanation:**
> - ✅ **C — Traffic Padding:** Traffic Padding inserts dummy bits/messages into communications to mask real traffic patterns, directly countering traffic analysis.
> - ❌ **A — Encipherment:** Encryption hides content but does NOT hide the fact that communication is occurring — it does not stop traffic analysis.
> - ❌ **B — Routing Control:** Routing Control selects secure transmission paths — it does not mask traffic patterns.
> - ❌ **D — Notarization:** Notarization involves a trusted third party to assure communication properties — unrelated to traffic analysis.

---

**Q14. Passive attacks are generally considered:**

- A) Easy to detect, hard to prevent
- B) Hard to detect, hard to prevent
- C) Easy to detect, easy to prevent
- D) Hard to detect, easy to prevent ✅

> **Explanation:**
> - ✅ **D:** Passive attacks leave no trace in system logs (hard to detect) because data is only observed, not modified. However, encryption makes them easy to prevent by making intercepted data unreadable.
> - ❌ **A:** Passive attacks are the opposite — hard to detect, not easy.
> - ❌ **B:** Prevention via encryption is straightforward — "hard to prevent" is incorrect.
> - ❌ **C:** Passive attacks are specifically notable for being difficult to detect — not easy.

---

**Q15. A valid authentication token captured from a previous login session is reused by an attacker to gain unauthorized access. Which type of attack is this?**

- A) Masquerade Attack
- B) Replay Attack ✅
- C) Session Hijacking
- D) Privilege Escalation

> **Explanation:**
> - ✅ **B — Replay Attack:** A replay attack specifically involves capturing and retransmitting previously valid data (tokens, credentials) to trick a system into granting access.
> - ❌ **A — Masquerade:** A masquerade involves impersonating a legitimate entity, typically by forging identity — not by replaying a captured token.
> - ❌ **C — Session Hijacking:** Session hijacking takes over an ACTIVE, live session. A replay attack uses a previously captured token — the original session is already over.
> - ❌ **D — Privilege Escalation:** This is about gaining higher access rights than authorized — not about replaying tokens.

---

**Q16. Which of the following attacks violates BOTH Confidentiality AND Integrity simultaneously?**

- A) DoS Attack
- B) Traffic Analysis
- C) Man-in-the-Middle Attack ✅
- D) Shoulder Surfing

> **Explanation:**
> - ✅ **C — MitM:** A Man-in-the-Middle attack intercepts communication (violates Confidentiality) AND can alter the messages in transit (violates Integrity) — simultaneously.
> - ❌ **A — DoS:** Only targets Availability — no data is read or altered.
> - ❌ **B — Traffic Analysis:** Only targets Confidentiality (metadata exposure) — data is not modified.
> - ❌ **D — Shoulder Surfing:** Only targets Confidentiality — no data modification occurs.

---

**Q17. Which of the following is NOT a valid risk treatment option?**

- A) Risk Avoidance
- B) Risk Transfer
- C) Risk Elimination ✅
- D) Risk Acceptance

> **Explanation:**
> - ✅ **C — Risk Elimination:** Risk CANNOT be completely eliminated — only reduced to an acceptable level. "Risk Elimination" is not a valid treatment option. This is a fundamental principle of risk management.
> - ❌ **A — Risk Avoidance:** Valid — stop doing the risky activity entirely.
> - ❌ **B — Risk Transfer:** Valid — shift risk to a third party (insurance, outsourcing).
> - ❌ **D — Risk Acceptance:** Valid — acknowledge and accept the consequences of a risk.

---

## MCQs 18–22 — Controls, Risk, Frameworks

---

**Q18. An Intrusion Detection System (IDS) is BEST classified as which type of security control?**

- A) Preventive + Administrative
- B) Corrective + Technical
- C) Detective + Technical ✅
- D) Deterrent + Physical

> **Explanation:**
> - ✅ **C — Detective + Technical:** An IDS monitors and identifies attacks in progress or after the fact (Detective function) using software/hardware mechanisms (Technical type).
> - ❌ **A — Preventive + Administrative:** IDS does not prevent attacks — it detects them. And it is a technical tool, not an administrative policy.
> - ❌ **B — Corrective + Technical:** Corrective controls restore systems after an attack. IDS does not restore anything — it only identifies.
> - ❌ **D — Deterrent + Physical:** Deterrent controls discourage attacks (like warning banners). IDS does not discourage — it detects.

---

**Q19. A security awareness training program that teaches employees to recognize phishing emails is BEST classified as:**

- A) Technical + Preventive
- B) Administrative + Directive ✅
- C) Physical + Deterrent
- D) Technical + Detective

> **Explanation:**
> - ✅ **B — Administrative + Directive:** Security awareness training is a management-level control (Administrative) that guides people toward compliant behavior (Directive function).
> - ❌ **A — Technical + Preventive:** Training is not a software/hardware tool — it is a human-facing administrative measure.
> - ❌ **C — Physical + Deterrent:** Physical controls deal with physical access — training is not a physical control.
> - ❌ **D — Technical + Detective:** Training is neither technical nor detective in nature.

---

**Q20. In the context of information security scope, which of the following is the MOST accurate statement?**

- A) Cybersecurity and Information Security are the same thing
- B) Network Security is broader than Cybersecurity
- C) Information Security is a subset of Cybersecurity
- D) Cybersecurity is a subset of Information Security ✅

> **Explanation:**
> - ✅ **D:** The correct hierarchy is: Network Security ⊂ Cybersecurity ⊂ Information Security. Information Security is the broadest domain, covering digital and non-digital information in any form.
> - ❌ **A:** They are not the same — Cybersecurity focuses on digital systems only; InfoSec also covers physical and verbal information.
> - ❌ **B:** Network Security is narrower than Cybersecurity — not broader.
> - ❌ **C:** This inverts the relationship entirely.

---

**Q21. ISO/IEC 27001:2022 reduced its Annex A controls from the 2013 version. Which numbers are correct for these two versions respectively?**

- A) 127 controls (2013) → 100 controls (2022)
- B) 114 controls (2013) → 93 controls (2022) ✅
- C) 100 controls (2013) → 85 controls (2022)
- D) 114 controls (2013) → 100 controls (2022)

> **Explanation:**
> - ✅ **B:** ISO/IEC 27001:2013 had **114 controls** across 14 domains. The 2022 revision consolidated these to **93 controls** organized across 4 themes (Organizational, People, Physical, Technological).
> - ❌ **A:** 127 and 100 are both incorrect numbers for either version.
> - ❌ **C:** 100 and 85 are both incorrect.
> - ❌ **D:** 100 is incorrect for the 2022 version — the correct number is 93.

---

**Q22. Which of the following correctly lists the five NIST Cybersecurity Framework (CSF) core functions in the RIGHT order?**

- A) Protect → Identify → Detect → Respond → Recover
- B) Identify → Detect → Protect → Respond → Recover
- C) Identify → Protect → Detect → Respond → Recover ✅
- D) Identify → Protect → Respond → Detect → Recover

> **Explanation:**
> - ✅ **C:** The correct order is **Identify → Protect → Detect → Respond → Recover** — this reflects the logical flow: first understand your assets, then protect them, then detect issues, then respond, then recover.
> - ❌ **A:** Protect before Identify makes no sense — you cannot protect what you haven't identified.
> - ❌ **B:** Detect before Protect is out of order — you build defences before you monitor for breaches.
> - ❌ **D:** Respond before Detect is logically impossible — you cannot respond to what you haven't detected.

---

## MCQs 23–25 — Extra Notes: STRIDE, CVE/CVSS, X.800

---

**Q23. In the STRIDE threat model, which threat category maps to a violation of Non-repudiation?**

- A) Spoofing
- B) Tampering
- C) Repudiation ✅
- D) Information Disclosure

> **Explanation:**
> - ✅ **C — Repudiation:** In STRIDE, Repudiation refers to a user performing an action and then denying it — this directly violates Non-repudiation.
> - ❌ **A — Spoofing:** Spoofing violates Authentication — pretending to be someone else.
> - ❌ **B — Tampering:** Tampering violates Integrity — modifying data without authorization.
> - ❌ **D — Information Disclosure:** This violates Confidentiality — unauthorized exposure of data. A common trap because "disclosure" sounds like it could relate to repudiation.

---

**Q24. Which of the following statements CORRECTLY distinguishes CVE, CWE, and CVSS?**

- A) CVE scores severity, CWE identifies instances, CVSS classifies weakness types
- B) CVE classifies weakness types, CVSS scores severity, CWE identifies instances
- C) CVE identifies specific vulnerability instances, CWE classifies weakness types, CVSS scores severity ✅
- D) CVE and CWE are the same — both identify vulnerability instances; CVSS scores them

> **Explanation:**
> - ✅ **C:** CVE = specific known vulnerability instances (e.g., CVE-2021-44228 for Log4Shell). CWE = categories/types of weaknesses (e.g., CWE-79 for XSS). CVSS = the scoring system that rates severity from 0.0 to 10.0.
> - ❌ **A:** CVE does not score — CVSS does. This option completely mixes up roles.
> - ❌ **B:** CVE does not classify types — CWE does. CWE does not identify instances — CVE does.
> - ❌ **D:** CVE and CWE are NOT the same. CVE = instances; CWE = root-cause categories. A single CWE can map to thousands of CVEs.

---

**Q25. A vulnerability is assigned a CVSS base score of 9.3. Which severity level does this fall under, and what is the correct CVSS range for that level?**

- A) High — 7.0 to 9.9
- B) Critical — 9.0 to 10.0 ✅
- C) High — 8.0 to 9.5
- D) Critical — 8.5 to 10.0

> **Explanation:**
> - ✅ **B — Critical, 9.0–10.0:** CVSS scores of 9.0 to 10.0 are classified as Critical. A score of 9.3 falls squarely in this range.
> - ❌ **A:** The High range is 7.0–8.9, not 7.0–9.9. This option incorrectly extends the High range into Critical territory.
> - ❌ **C:** 8.0–9.5 is an invented range that does not match any official CVSS severity band.
> - ❌ **D:** Critical starts at 9.0, not 8.5. A score of 8.5 is actually High, not Critical.

---

## 📊 Answer Key — Quick Reference

| Q | Answer | Topic |
|---|--------|-------|
| 1 | D | CIA — Availability |
| 2 | C | CIA — Availability (Ransomware) |
| 3 | C | CIA — Integrity |
| 4 | C | Parkerian Hexad |
| 5 | D | Parkerian Hexad — Possession |
| 6 | D | McCumber Cube — 27 cells |
| 7 | B | McCumber Cube — Information States |
| 8 | B | Risk Formula |
| 9 | C | Residual Risk |
| 10 | B | DAD Triad mapping |
| 11 | C | Passive Attack |
| 12 | B | Traffic Analysis |
| 13 | C | X.800 — Traffic Padding |
| 14 | D | Passive attack characteristics |
| 15 | B | Replay Attack |
| 16 | C | MitM — CIA violation |
| 17 | C | Risk Treatment |
| 18 | C | IDS — Control classification |
| 19 | B | Awareness training — Control classification |
| 20 | D | InfoSec vs Cybersecurity scope |
| 21 | B | ISO 27001 version control counts |
| 22 | C | NIST CSF — 5 functions order |
| 23 | C | STRIDE — Repudiation |
| 24 | C | CVE vs CWE vs CVSS |
| 25 | B | CVSS — Critical range |

---