# 🎯 MCQ — Session 09: PCI DSS

> 30 MCQs | Raw Fundamentals | 4 Options Each | Full Explanations
> Covers: PCI DSS Overview, History, PCI SSC, Levels, 12 Requirements,
> Compliance Validation, Cardholder Data, SAD, CDE + Extra Notes

---

## MCQ Set

---

**Q1. PCI DSS stands for and is best classified as which type of
requirement?**

A) Payment Card Industry Data Security Standard — a US federal law
B) Payment Card Industry Data Security Standard — a private industry
   standard enforced contractually ✅
C) Payment Card Information Data Security Standard — an international
   regulation
D) Payment Card Industry Data Security System — an EU regulation

> **Explanation:** **PCI DSS = Payment Card Industry Data Security
> Standard** — it is a **private industry standard**, NOT a government
> law. It is enforced through **contractual agreements** between
> merchants, acquirers, and payment card brands. Unlike HIPAA (US law)
> or GDPR (EU regulation), PCI DSS has no legislative authority —
> but non-compliance consequences are very real including loss of
> card processing privileges.

---

**Q2. The PCI Security Standards Council (PCI SSC) was founded in
which year and by how many card brands?**

A) 2004 — founded by 3 card brands
B) 2000 — founded by 2 card brands
C) 2006 — founded by 5 card brands ✅
D) 2008 — founded by 4 card brands

> **Explanation:** **PCI SSC was founded on September 7, 2006 by
> 5 founding card brands**: Visa, Mastercard, American Express,
> Discover, and JCB (Japan Credit Bureau). Before PCI SSC existed,
> each card brand had its own separate security program. PCI DSS 1.0
> was actually published in 2004 before PCI SSC was formally created
> — PCI SSC was formed to take ownership of the standard.

---

**Q3. Which of the following is NOT one of the 5 founding members
of the PCI Security Standards Council?**

A) Visa
B) Mastercard
C) UnionPay ✅
D) JCB (Japan Credit Bureau)

> **Explanation:** The **5 founding members** of PCI SSC are Visa,
> Mastercard, American Express, Discover, and JCB. **UnionPay**
> (Chinese card brand) is NOT a founding member — though it is a
> major global card brand. JCB (Japan Credit Bureau) is the only
> non-US founding member. Knowing all 5 founding members is directly
> tested in MCQs.

---

**Q4. PCI DSS 1.0 — the first unified payment card security standard
— was published in which year?**

A) 2000
B) 2002
C) 2004 ✅
D) 2006

> **Explanation:** **PCI DSS 1.0 was published in 2004** — the first
> unified standard combining Visa's CISP and Mastercard's SDP programs.
> PCI SSC was then founded in 2006 to take ownership. PCI DSS 1.1
> was released alongside PCI SSC's founding in 2006. The year 2000
> marks Visa's CISP launch — the precursor program, not PCI DSS itself.

---

**Q5. The current version of PCI DSS is v4.0, published in which
year, and what was the most significant new concept it introduced?**

A) 2020 — Tokenization Approach
B) 2021 — Zero Trust Architecture
C) 2022 — Customized Approach ✅
D) 2023 — Risk-Based Approach

> **Explanation:** **PCI DSS v4.0 was published in March 2022** and
> its most significant new concept is the **Customized Approach** —
> allowing mature organizations to use alternative controls to meet
> PCI DSS objectives, provided they demonstrate equivalent security
> and have controls validated by a QSA. The previous version
> (v3.2.1) was retired in March 2024.

---

**Q6. Under PCI DSS, which entity directly enforces compliance
and can impose fines on non-compliant merchants?**

A) PCI SSC — directly fines merchants for non-compliance
B) Government regulators — through financial legislation
C) Payment card brands through acquirer bank agreements ✅
D) The Qualified Security Assessor (QSA) firm

> **Explanation:** **PCI SSC sets the standard but does NOT enforce
> it or fine merchants directly.** Enforcement is done by the
> **individual card brands (Visa, Mastercard, etc.) through acquirer
> bank agreements**. Acquirer banks pass fines and requirements to
> merchants. QSAs assess compliance but do not enforce it. This
> distinction — PCI SSC creates standards, card brands enforce —
> is a very common MCQ trap.

---

**Q7. A large online retailer processes 8 million card transactions
per year. Under PCI DSS merchant levels, they are classified as:**

A) Merchant Level 2 — requiring an annual SAQ
B) Merchant Level 3 — requiring quarterly ASV scans only
C) Merchant Level 4 — lowest requirements apply
D) Merchant Level 1 — requiring an annual ROC by a QSA ✅

> **Explanation:** **Merchant Level 1 = more than 6 million
> transactions per year.** 8 million exceeds this threshold —
> placing this retailer at Level 1. Level 1 merchants face the
> strictest requirements: **annual ROC (Report on Compliance)
> conducted by an external QSA** plus quarterly ASV network scans.
> This is the highest risk and most regulated merchant category.

---

**Q8. A small e-commerce business processes 15,000 online card
transactions per year. Under PCI DSS, they are classified as
which merchant level?**

A) Merchant Level 1 — ROC by QSA required
B) Merchant Level 2 — annual SAQ required
C) Merchant Level 3 — annual SAQ required
D) Merchant Level 4 — SAQ and scans recommended ✅

> **Explanation:** **Merchant Level 4 = fewer than 20,000 e-commerce
> transactions per year** (or up to 1 million other transactions).
> 15,000 falls below the 20,000 threshold — placing this business
> at Level 4. Level 4 requirements are the least stringent — SAQ
> and quarterly ASV scans are **recommended** (not always mandatory
> depending on the acquiring bank).

---

**Q9. For PCI DSS service providers, the threshold between Level 1
and Level 2 is:**

A) 6 million transactions per year
B) 1 million transactions per year
C) 500,000 transactions per year
D) 300,000 transactions per year ✅

> **Explanation:** **Service Provider Level 1 = more than 300,000
> transactions per year.** Service Provider Level 2 = fewer than
> 300,000. Note this is significantly lower than the merchant Level 1
> threshold of 6 million — because service providers handle data
> for MULTIPLE merchants, making their risk profile higher even at
> lower transaction volumes.

---

**Q10. PCI DSS organizes its requirements into how many requirements
under how many goals?**

A) 10 requirements under 5 goals
B) 12 requirements under 6 goals ✅
C) 14 requirements under 6 goals
D) 12 requirements under 4 goals

> **Explanation:** PCI DSS has exactly **12 requirements organized
> under 6 goals.** The goals pair with requirements as: Goal 1
> (Req 1–2), Goal 2 (Req 3–4), Goal 3 (Req 5–6), Goal 4 (Req 7–8–9),
> Goal 5 (Req 10–11), Goal 6 (Req 12). Both numbers — 12 requirements
> AND 6 goals — are directly tested in MCQs.

---

**Q11. PCI DSS Requirement 3 specifically addresses which security
objective?**

A) Install and maintain network security controls
B) Protect all systems from malicious software
C) Protect stored account data ✅
D) Restrict physical access to cardholder data

> **Explanation:** **Requirement 3 = Protect stored account data**
> — it defines rules for how cardholder data must be protected when
> stored, including encryption requirements for PAN and the absolute
> prohibition on storing SAD. Requirement 1 covers firewalls.
> Requirement 5 covers anti-malware. Requirement 9 covers physical
> access to cardholder data.

---

**Q12. Under PCI DSS, which goal covers both logging of access to
cardholder data AND regular security testing of systems and
networks?**

A) Goal 2 — Protect Cardholder Data
B) Goal 3 — Maintain a Vulnerability Management Program
C) Goal 4 — Implement Strong Access Control Measures
D) Goal 5 — Regularly Monitor and Test Networks ✅

> **Explanation:** **Goal 5 = Regularly Monitor and Test Networks**
> — it covers Requirements 10 (log and monitor all access to system
> components and cardholder data) and 11 (test security of systems
> and networks regularly). Logging (Req 10) and penetration testing/
> vulnerability scanning (Req 11) both fall under this goal.

---

**Q13. The SAD element that is a 3-digit security code on the back
of Visa cards is called:**

A) CVC2 — Card Validation Code 2
B) CID — Card Identification Number
C) CVV2 — Card Verification Value 2 ✅
D) CAV2 — Card Authentication Value 2

> **Explanation:** **CVV2 (Card Verification Value 2)** is the
> 3-digit security code used by **Visa**. CVC2 is Mastercard's
> equivalent. CAV2 is Discover's equivalent. CID is American
> Express's 4-digit equivalent (on the front of the card).
> All of these are SAD and **cannot be stored after authorization
> under any circumstances** — even encrypted.

---

**Q14. Which of the following statements about Sensitive
Authentication Data (SAD) storage is correct under PCI DSS?**

A) SAD can be stored if it is encrypted with AES-256
B) SAD can be stored for up to 24 hours after authorization
C) SAD can be stored only by Level 1 merchants with QSA approval
D) SAD must NEVER be stored after authorization — even if encrypted ✅

> **Explanation:** **SAD cannot be stored after authorization —
> EVER — even in encrypted form.** This is one of the most absolute
> rules in PCI DSS. The restriction applies to full magnetic stripe
> data (Track 1/2), card verification codes (CVV2/CVC2/CID/CAV2),
> and PINs/PIN blocks. There are NO exceptions — no level of
> encryption makes SAD storage acceptable after authorization.

---

**Q15. When displaying a PAN (Primary Account Number) on a receipt
or screen, PCI DSS requires that:**

A) The full PAN must never be displayed to anyone
B) Only the last 4 digits may be displayed — nothing else
C) Only the first 6 and last 4 digits are visible — all others masked ✅
D) The PAN must be replaced with a token before any display

> **Explanation:** PCI DSS requires that when displaying PAN, only
> the **first 6 and last 4 digits** are visible — all middle digits
> must be masked (e.g., 411111XXXXXX1111). The first 6 digits (BIN —
> Bank Identification Number) identify the card issuer. The last 4
> digits help identify the specific card. Only personnel with a
> legitimate business need may see the full unmasked PAN.

---

**Q16. The Cardholder Data Environment (CDE) is defined as:**

A) Only the database servers that store cardholder data
B) Only the payment terminals used to accept card payments
C) The people, processes, and technology that store, process, or
   transmit cardholder data or SAD — plus connected systems ✅
D) Only the systems directly connected to the internet

> **Explanation:** The **CDE = Cardholder Data Environment** encompasses
> the **people, processes, and technology** that store, process, or
> transmit cardholder data or SAD — AND any systems connected to or
> that could impact the security of those systems. It is NOT limited
> to databases or payment terminals — it includes everything in scope
> for PCI DSS compliance.

---

**Q17. The most effective method for reducing PCI DSS compliance
scope is:**

A) Encrypting all cardholder data at rest
B) Using an SAQ instead of a ROC for compliance validation
C) Implementing network segmentation to isolate the CDE ✅
D) Storing only the last 4 digits of PAN

> **Explanation:** **Network segmentation** is the most effective
> scope reduction technique — isolating the CDE from other systems
> means those other systems are out of scope for PCI DSS. Encryption
> protects data but does NOT remove systems from scope. SAQ vs ROC
> is about validation method, not scope reduction. Storing only last
> 4 digits removes data but the system handling the transaction is
> still in scope.

---

**Q18. A payment processor replaces PAN with a randomly generated
token that has no mathematical relationship to the original card
number. This technique is called:**

A) Encryption — transforms PAN and keeps it in scope
B) Hashing — creates an irreversible representation of PAN
C) Masking — hides portions of PAN for display purposes
D) Tokenization — replaces PAN with a non-sensitive token that can
   remove PAN from scope ✅

> **Explanation:** **Tokenization** replaces PAN with a randomly
> generated token stored in a secure vault. The token has no
> mathematical relationship to the PAN and is useless to attackers.
> Crucially, tokenization can **remove PAN from the scope** of
> systems using the token — unlike encryption which keeps encrypted
> PAN in scope. This is a key MCQ distinction: encryption ≠
> tokenization for scoping purposes.

---

**Q19. Which compliance validation document is required by ALL
PCI DSS merchants and service providers — regardless of level?**

A) ROC — Report on Compliance
B) SAQ — Self-Assessment Questionnaire
C) AOC — Attestation of Compliance ✅
D) QSA Report — Qualified Security Assessor Report

> **Explanation:** The **AOC (Attestation of Compliance)** is required
> by ALL merchants and service providers — it is the summary sign-off
> document confirming the results of either an SAQ or ROC. The ROC
> is only required for Level 1 merchants and Level 1 service providers.
> The SAQ is used by Level 2–4 merchants and Level 2 service providers.
> Everyone needs an AOC.

---

**Q20. A Level 1 merchant's annual PCI DSS compliance assessment
must be conducted by which type of assessor?**

A) ISA — Internal Security Assessor employed by the merchant
B) ASV — Approved Scanning Vendor
C) QSA — Qualified Security Assessor from an external certified firm ✅
D) Any certified cybersecurity professional

> **Explanation:** **Level 1 merchants require an annual ROC conducted
> by an external QSA (Qualified Security Assessor)** — a professional
> from a PCI SSC-certified assessment company. An ISA (Internal
> Security Assessor) is an employee of the organization — they can
> conduct SAQ assessments but NOT Level 1 ROC audits. ASVs perform
> quarterly network scans — not the full ROC audit.

---

**Q21. What is the role of an ASV (Approved Scanning Vendor) in
PCI DSS compliance?**

A) Conducting annual on-site ROC audits for Level 1 merchants
B) Performing required quarterly external vulnerability scans of
   systems in the CDE ✅
C) Issuing the AOC once compliance is confirmed
D) Training internal staff on PCI DSS requirements

> **Explanation:** An **ASV (Approved Scanning Vendor)** is a
> PCI SSC-approved company that conducts required **quarterly
> external vulnerability scans** of internet-facing systems in
> the CDE. ASV scans are required for all merchant levels (Level 1
> mandated, Level 4 recommended by acquirers). ASVs only do
> scanning — QSAs do the full ROC audits and ISAs do internal
> assessments.

---

**Q22. Visa's original card security program that preceded PCI DSS
was called:**

A) SDP — Site Data Protection
B) DSOP — Data Security Operating Policy
C) DISC — Discover Information Security and Compliance
D) CISP — Cardholder Information Security Program ✅

> **Explanation:** **CISP (Cardholder Information Security Program)**
> was **Visa's** original card security program launched around 2000.
> SDP (Site Data Protection) was Mastercard's program. DSOP was
> American Express's program. DISC was Discover's program. CISP
> and SDP were eventually combined into PCI DSS 1.0 in 2004.

---

**Q23. PCI DSS Requirement 11 covers which security activity?**

A) Restricting physical access to cardholder data
B) Identifying users and authenticating system access
C) Protecting all systems from malicious software
D) Testing security of systems and networks regularly ✅

> **Explanation:** **Requirement 11 = Test security of systems and
> networks regularly** — it covers penetration testing, internal
> and external vulnerability scanning, intrusion detection/prevention
> system testing, and wireless network analysis. Requirement 9 covers
> physical access. Requirement 8 covers authentication. Requirement 5
> covers anti-malware protection.

---

**Q24. In PCI DSS v4.0, the Customized Approach allows
organizations to:**

A) Skip PCI DSS requirements if they are too costly to implement
B) Use alternative controls to meet PCI DSS objectives — provided
   equivalent security is demonstrated and validated by a QSA ✅
C) Self-certify compliance without involving a QSA
D) Apply only the requirements relevant to their industry sector

> **Explanation:** The **Customized Approach** in v4.0 allows
> organizations to design their own controls to meet the stated
> objective of each PCI DSS requirement — rather than following
> the prescriptive defined approach. However, it is NOT a way to
> skip requirements. The custom controls must be **validated by
> a QSA**, require extensive documentation, and must demonstrate
> equivalent or better security than the standard approach.

---

**Q25. Which PCI DSS version removed SSL and early TLS as
acceptable security protocols due to known vulnerabilities?**

A) PCI DSS 3.0
B) PCI DSS 3.1 ✅
C) PCI DSS 3.2
D) PCI DSS v4.0

> **Explanation:** **PCI DSS 3.1 (2015)** was the version that
> explicitly removed SSL (Secure Sockets Layer) and early versions
> of TLS (Transport Layer Security) as acceptable security protocols
> — due to well-known vulnerabilities like POODLE and BEAST. This
> required merchants to upgrade to TLS 1.2 or higher. PCI DSS 3.2
> further expanded MFA requirements.

---

**Q26. A compensating control in PCI DSS is used when:**

A) An organization wants to reduce compliance costs
B) A QSA determines a merchant is too small to comply fully
C) An organization cannot meet a specific requirement due to a
   legitimate technical or business constraint ✅
D) An organization fails its annual ROC audit

> **Explanation:** **Compensating controls** are alternative security
> measures used when an organization has a **documented legitimate
> technical or business constraint** preventing implementation of
> the standard PCI DSS control. They must provide equivalent
> security to the original requirement, go above and beyond
> other PCI DSS requirements, and be approved by a QSA.
> Cost alone is NOT an acceptable reason for compensating controls.

---

**Q27. Which of the following data elements CAN be stored after
authorization under PCI DSS — if properly protected?**

A) Full magnetic stripe data (Track 1 and Track 2)
B) PIN Block
C) CVV2 security code
D) PAN (Primary Account Number) ✅

> **Explanation:** **PAN can be stored** after authorization —
> but it must be protected using strong encryption, masking, or
> tokenization. Full magnetic stripe data, PIN/PIN Block, and
> all card verification codes (CVV2/CVC2/CID/CAV2) are **SAD** —
> they can NEVER be stored after authorization regardless of
> protection method. This PAN vs SAD distinction is critical.

---

**Q28. PCI DSS Requirement 12 falls under which of the 6 PCI DSS
goals?**

A) Goal 3 — Maintain a Vulnerability Management Program
B) Goal 4 — Implement Strong Access Control Measures
C) Goal 5 — Regularly Monitor and Test Networks
D) Goal 6 — Maintain an Information Security Policy ✅

> **Explanation:** **Requirement 12 = Support information security
> with organizational policies and programs** — it falls under
> **Goal 6: Maintain an Information Security Policy**. This is the
> only requirement under Goal 6. It covers creating, maintaining,
> and disseminating a security policy, as well as security awareness
> training and an incident response plan.

---

**Q29. Comparing PCI DSS, HIPAA, and GDPR — which combination of
breach notification timelines is correct?**

A) PCI DSS = 72 hours / HIPAA = 60 days / GDPR = 30 days
B) PCI DSS = 60 days / HIPAA = 72 hours / GDPR = 60 days
C) PCI DSS = not prescriptive — notify card brands / HIPAA =
   60 days / GDPR = 72 hours to DPA ✅
D) PCI DSS = 30 days / HIPAA = 60 days / GDPR = 72 hours

> **Explanation:** The correct breach notification comparison:
> **PCI DSS** = No fixed regulatory timeline — organizations must
> notify their acquiring bank and card brands per their agreement.
> **HIPAA** = 60 days to notify individuals and HHS.
> **GDPR** = 72 hours to notify the DPA.
> PCI DSS's lack of a fixed regulatory timeline distinguishes it
> from HIPAA and GDPR — another reminder that PCI DSS is a
> contractual standard, not a law.

---

**Q30. Which combination of PCI DSS facts is entirely correct?**

A) PCI SSC founded 2004 / 6 merchant levels / SAD can be stored
   if encrypted / ROC required for all merchants / v4.0 published 2020
B) PCI SSC founded 2006 / 4 merchant levels / SAD cannot be stored
   ever / ROC required for Level 1 only / v4.0 published 2022 ✅
C) PCI SSC founded 2006 / 4 merchant levels / PAN cannot be stored /
   SAQ required for Level 1 / v4.0 introduced Safe Harbor
D) PCI SSC founded 2008 / 3 merchant levels / SAD can be stored
   encrypted / ROC required for Level 1 / v4.0 published 2022

> **Explanation:** The fully correct combination is:
> **PCI SSC founded 2006** ✅ (not 2004 or 2008)
> **4 merchant levels** ✅ (not 3 or 6)
> **SAD cannot be stored ever** ✅ (even encrypted — absolute rule)
> **ROC required for Level 1 ONLY** ✅ (not all merchants)
> **v4.0 published 2022** ✅ (March 2022)
> Option C fails because PAN CAN be stored (with protection) and
> SAQ is NOT for Level 1 (Level 1 needs ROC). Option A fails
> because PCI SSC was founded in 2006 and SAD cannot be stored
> even encrypted.

---

## 📊 Quick Answer Key

| Q | Ans | Q | Ans | Q | Ans |
|---|---|---|---|---|---|
| 1 | B | 11 | C | 21 | B |
| 2 | C | 12 | D | 22 | D |
| 3 | C | 13 | C | 23 | D |
| 4 | C | 14 | D | 24 | B |
| 5 | C | 15 | C | 25 | B |
| 6 | C | 16 | C | 26 | C |
| 7 | D | 17 | C | 27 | D |
| 8 | D | 18 | D | 28 | D |
| 9 | D | 19 | C | 29 | C |
| 10 | B | 20 | C | 30 | B |

---

## 🎯 Topic Coverage Map

| Topic | MCQs Covered |
|---|---|
| PCI DSS — industry standard not law | Q1 |
| PCI SSC founded 2006 — 5 founders | Q2 |
| 5 founding members — UnionPay trap | Q3 |
| PCI DSS 1.0 published 2004 | Q4 |
| PCI DSS v4.0 — 2022 — Customized Approach | Q5 |
| PCI SSC vs card brands enforcement | Q6 |
| Merchant Level 1 — 6M+ transactions | Q7 |
| Merchant Level 4 — <20K e-commerce | Q8 |
| Service provider threshold — 300K | Q9 |
| 12 requirements under 6 goals | Q10 |
| Requirement 3 — protect stored data | Q11 |
| Goal 5 — monitor and test | Q12 |
| CVV2 = Visa's security code | Q13 |
| SAD cannot be stored — absolute rule | Q14 |
| PAN display — first 6 + last 4 | Q15 |
| CDE definition | Q16 |
| Network segmentation — scope reduction | Q17 |
| Tokenization vs encryption — scope | Q18 |
| AOC — required by all levels | Q19 |
| Level 1 ROC — QSA required | Q20 |
| ASV — quarterly external scans | Q21 |
| CISP — Visa's original program | Q22 |
| Requirement 11 — security testing | Q23 |
| Customized Approach — v4.0 | Q24 |
| SSL/TLS removed in v3.1 | Q25 |
| Compensating controls | Q26 |
| PAN can be stored — SAD cannot | Q27 |
| Requirement 12 — Goal 6 | Q28 |
| PCI DSS vs HIPAA vs GDPR timelines | Q29 |
| Combined PCI DSS facts | Q30 |

---