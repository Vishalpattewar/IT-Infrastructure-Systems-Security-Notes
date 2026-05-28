# 🎯 MCQ — Session 03: NIST Framework

> 30 MCQs | Raw Fundamentals | 4 Options Each | Full Explanations
> Covers: NIST Overview, CSF Components, 5 Functions, Implementation Tiers,
> Profiles, Use of Framework, RMF, SP 800 Series + Extra Notes

---

## MCQ Set

---

**Q1. NIST stands for and operates under which US government department?**

A) National Information Security Technology — Department of Defense
B) National Institute of Standards and Technology — Department of Commerce ✅
C) National Institute of Security and Technology — Department of Homeland Security
D) National Information Systems Technology — Department of Justice

> **Explanation:** **NIST = National Institute of Standards and Technology**
> and it operates under the **US Department of Commerce** — not Defense, not
> Homeland Security, not Justice. This exact full form + department combination
> is a very common MCQ question.

---

**Q2. The NIST Cybersecurity Framework (CSF) was originally created in
response to which trigger?**

A) The 9/11 terrorist attacks in 2001
B) The NSA surveillance revelations in 2013
C) Executive Order 13636 — Improving Critical Infrastructure Cybersecurity ✅
D) The GDPR regulation in Europe

> **Explanation:** **Executive Order 13636** signed in February 2013 directed
> NIST to develop a framework for reducing cyber risks to critical
> infrastructure — resulting in **CSF 1.0 published in February 2014**. GDPR
> is European legislation unrelated to CSF creation.

---

**Q3. Which of the following correctly lists the THREE main components of
the NIST Cybersecurity Framework?**

A) Functions, Categories, Subcategories
B) Tiers, Controls, Profiles
C) Framework Core, Implementation Tiers, Framework Profiles ✅
D) Identify, Protect, Detect

> **Explanation:** The **three main components** of NIST CSF are:
> **Framework Core** (WHAT — 5 functions), **Implementation Tiers** (HOW WELL
> — 4 levels), and **Framework Profiles** (WHERE — current vs target). A
> describes the internal structure of the Core only. D lists three of the five
> functions.

---

**Q4. The NIST CSF Framework Core answers which fundamental question?**

A) How well does the organization manage cybersecurity risk?
B) Where is the organization now versus where it wants to be?
C) What cybersecurity activities should the organization perform? ✅
D) Who is responsible for cybersecurity decisions?

> **Explanation:** The **Framework Core** answers **WHAT** — what activities
> an organization should perform across the 5 functions. Implementation Tiers
> answer HOW WELL. Framework Profiles answer WHERE (current vs target).

---

**Q5. Which of the following is the correct order of the 5 NIST CSF
Core Functions?**

A) Protect → Identify → Detect → Respond → Recover
B) Identify → Protect → Detect → Respond → Recover ✅
C) Identify → Detect → Protect → Respond → Recover
D) Identify → Protect → Respond → Detect → Recover

> **Explanation:** The correct sequence is **Identify → Protect → Detect →
> Respond → Recover** (IPDRR). The logical flow is: know your assets → protect
> them → watch for threats → react when hit → bounce back. Detect must come
> before Respond — you can't respond to something you haven't detected.

---

**Q6. Which CSF function is responsible for developing understanding of
assets, risks, and the organization's cybersecurity posture?**

A) Protect
B) Detect
C) Respond
D) Identify ✅

> **Explanation:** **Identify** is the foundation function — it covers asset
> management, risk assessment, governance, and business environment
> understanding. It answers: *"What do we have and what are the risks?"*
> Without Identify, you cannot effectively do any of the other four functions.

---

**Q7. An organization implements firewalls, encryption, and access controls.
These activities fall under which CSF function?**

A) Identify
B) Protect ✅
C) Detect
D) Respond

> **Explanation:** **Protect** covers implementing safeguards — firewalls,
> encryption, access control, training, and protective technology all fall
> under Protect. These are preventive measures. Identify is about discovery
> and assessment. Detect is about monitoring.

---

**Q8. A Security Operations Center (SOC) continuously monitors systems for
anomalies and unusual activity. This primarily falls under which CSF
function?**

A) Identify
B) Protect
C) Detect ✅
D) Respond

> **Explanation:** **Detect** covers continuous monitoring, anomaly detection,
> and detection processes — exactly what a SOC does. Protect implements
> safeguards. Respond is what happens AFTER detection. Identify is about
> inventory and risk assessment.

---

**Q9. During a ransomware attack, the security team activates the incident
response plan, coordinates with stakeholders, and works to contain the
spread. These activities fall under which CSF function?**

A) Detect
B) Protect
C) Recover
D) Respond ✅

> **Explanation:** **Respond** covers activities taken after a detected
> cybersecurity event — incident response planning, communications,
> analysis, mitigation, and improvements. Recover comes AFTER Respond —
> it focuses on restoring normal operations once the incident is contained.

---

**Q10. After a cybersecurity incident is resolved, the organization restores
affected systems and communicates recovery status to stakeholders. These
activities fall under which CSF function?**

A) Respond
B) Identify
C) Recover ✅
D) Protect

> **Explanation:** **Recover** covers restoring capabilities after an incident
> — recovery planning, implementing improvements based on lessons learned,
> and communications about recovery status. Respond is the active containment
> phase. Recover is the restoration phase that comes after.

---

**Q11. NIST CSF Implementation Tier 1 is named:**

A) Risk Informed
B) Repeatable
C) Adaptive
D) Partial ✅

> **Explanation:** **Tier 1 = Partial** — characterized by ad hoc, reactive
> security practices with no formal risk management process. The four tiers
> are: Partial (1) → Risk Informed (2) → Repeatable (3) → Adaptive (4).

---

**Q12. Which Implementation Tier describes an organization that has formally
approved cybersecurity policies consistently applied across the entire
organization?**

A) Tier 1 — Partial
B) Tier 2 — Risk Informed
C) Tier 3 — Repeatable ✅
D) Tier 4 — Adaptive

> **Explanation:** **Tier 3 = Repeatable** — characterized by formally
> approved policies and procedures that are consistently implemented
> organization-wide. Tier 2 has risk awareness but it's informal and not
> org-wide. Tier 4 goes further — proactively adapting based on lessons
> learned.

---

**Q13. Which Implementation Tier describes an organization that proactively
adapts its cybersecurity practices based on lessons learned and changing
threats?**

A) Tier 2 — Risk Informed
B) Tier 3 — Repeatable
C) Tier 4 — Adaptive ✅
D) Tier 1 — Partial

> **Explanation:** **Tier 4 = Adaptive** — the highest tier, characterized
> by continuous improvement, proactive adaptation to threats, and
> organization-wide integration of cybersecurity into risk decisions.
> Tier 3 is consistent but not proactively adaptive.

---

**Q14. A common misconception about NIST CSF Implementation Tiers is that
organizations should always aim for Tier 4. This statement is:**

A) True — Tier 4 represents the best possible security posture
B) True — all critical infrastructure must achieve Tier 4
C) False — the right tier depends on the organization's risk tolerance
   and business objectives ✅
D) False — Tier 3 is the maximum recommended tier

> **Explanation:** NIST explicitly states that **Tiers are NOT maturity
> levels** and higher is not always the goal. The appropriate tier is
> determined by the organization's **risk tolerance, business needs, and
> available resources**. A small organization with low risk may be perfectly
> appropriate at Tier 2.

---

**Q15. A Framework Profile that represents where an organization currently
IS in its cybersecurity posture is called:**

A) Target Profile
B) Baseline Profile
C) Current Profile ✅
D) Reference Profile

> **Explanation:** **Current Profile = AS-IS state** — documenting what
> cybersecurity outcomes the organization is currently achieving. **Target
> Profile = TO-BE state** — the desired outcomes. The gap between them drives
> the improvement roadmap.

---

**Q16. The gap between an organization's Current Profile and Target Profile
in NIST CSF serves as:**

A) Evidence for a compliance audit
B) The cybersecurity improvement roadmap and prioritization guide ✅
C) Proof of Tier 4 achievement
D) The final CSF certification document

> **Explanation:** The **gap between Current and Target Profile** is exactly
> what drives prioritization and improvement planning. It tells the
> organization what needs to be done, in what order, to reach its desired
> cybersecurity state. There is no NIST CSF certification.

---

**Q17. In which year was NIST CSF version 1.0 originally published?**

A) 2011
B) 2012
C) 2013
D) 2014 ✅

> **Explanation:** **NIST CSF 1.0 was published in February 2014** in
> response to Executive Order 13636 (February 2013). CSF 1.1 came in April
> 2018. CSF 2.0 came in February 2024.

---

**Q18. NIST CSF 2.0 released in February 2024 added which new function to
the Framework Core?**

A) Authorize
B) Manage
C) Govern ✅
D) Comply

> **Explanation:** **CSF 2.0 added GOVERN** as the 6th function — making the
> framework **G-IPDRR** instead of just IPDRR. Govern is an overarching
> function that provides context and direction for all other five functions,
> covering organizational context, risk strategy, roles, policies, and
> oversight.

---

**Q19. In NIST CSF 2.0, the GOVERN function is best described as:**

A) A sequential first step before Identify
B) An overarching function that provides context and direction for all
   other functions ✅
C) A replacement for the Identify function
D) A technical control function covering governance tools

> **Explanation:** **GOVERN in CSF 2.0 is overarching** — it sits above and
> around the other five functions rather than being sequential. It covers
> organizational context, risk management strategy, policies, roles, and
> supply chain risk management that informs how all other functions operate.

---

**Q20. NIST SP 800-37 defines which NIST framework?**

A) Cybersecurity Framework (CSF)
B) Privacy Framework
C) Risk Management Framework (RMF) ✅
D) Secure Software Development Framework

> **Explanation:** **SP 800-37 = Risk Management Framework (RMF)** — the
> structured process for integrating security into the system development
> lifecycle. SP 800-53 defines the security controls catalog. The CSF is
> defined in a separate document (not an SP 800 number).

---

**Q21. NIST SP 800-53 provides:**

A) Guidelines for incident response handling
B) The Risk Management Framework steps
C) A catalog of security and privacy controls for federal information
   systems ✅
D) Guidelines for penetration testing

> **Explanation:** **SP 800-53 = Security and Privacy Controls** — it provides
> a comprehensive catalog of controls organized into 20 families. It is used
> in **RMF Step 3 (Select)** to choose appropriate controls. SP 800-61 covers
> incident response. SP 800-37 covers RMF. SP 800-115 covers security testing.

---

**Q22. The correct order of the NIST RMF 7 steps is:**

A) Categorize → Prepare → Select → Implement → Assess → Authorize → Monitor
B) Prepare → Select → Categorize → Implement → Assess → Authorize → Monitor
C) Prepare → Categorize → Select → Implement → Assess → Authorize → Monitor ✅
D) Prepare → Categorize → Implement → Select → Assess → Authorize → Monitor

> **Explanation:** The correct RMF order is **Prepare → Categorize → Select
> → Implement → Assess → Authorize → Monitor**. Prepare sets context first.
> Categorize classifies the system. Select chooses controls. Implement deploys
> them. Assess verifies them. Authorize grants ATO. Monitor is ongoing.

---

**Q23. In NIST RMF, which step involves classifying the information system
based on impact level — Low, Moderate, or High?**

A) Prepare
B) Select
C) Assess
D) Categorize ✅

> **Explanation:** **Step 2 = Categorize** — the system is classified based
> on potential impact using **FIPS 199**. The three impact levels are Low,
> Moderate, and High — evaluated against Confidentiality, Integrity, and
> Availability. The highest impact level across all three determines the
> overall system category.

---

**Q24. In NIST RMF, the step where a senior official formally accepts
residual risk and grants permission for the system to operate is:**

A) Assess
B) Implement
C) Monitor
D) Authorize ✅

> **Explanation:** **Step 6 = Authorize** — a senior official (Authorizing
> Official) reviews the security assessment results, accepts any residual risk,
> and issues an **ATO (Authority to Operate)**. Without an ATO, the system
> cannot operate in a federal environment.

---

**Q25. NIST SP 800-171 specifically focuses on protecting:**

A) Classified government information in federal data centers
B) Controlled Unclassified Information (CUI) in non-federal systems ✅
C) Personal health information in hospitals
D) Payment card data in retail environments

> **Explanation:** **SP 800-171 = CUI protection for non-federal
> organizations** — it applies to contractors, suppliers, and any non-federal
> organization that handles CUI (sensitive but unclassified federal
> information). It is the basis for **CMMC** requirements for US defense
> contractors.

---

**Q26. A key difference between NIST CSF and ISO 27001 is:**

A) NIST CSF can be certified; ISO 27001 cannot
B) ISO 27001 can be certified; NIST CSF cannot ✅
C) NIST CSF is mandatory globally; ISO 27001 is voluntary
D) ISO 27001 is free to use; NIST CSF requires a paid license

> **Explanation:** **ISO 27001 offers formal third-party certification** —
> organizations can be audited and certified against it. **NIST CSF has no
> formal certification** — it is a guidance framework. Also, NIST CSF is
> **free** to use; ISO 27001 is a **paid standard document**.

---

**Q27. For which type of organization is NIST CSF MANDATORY rather than
voluntary?**

A) All US-based private companies
B) All healthcare organizations globally
C) US Federal Government Agencies ✅
D) All financial institutions worldwide

> **Explanation:** **NIST CSF is mandatory for US Federal Agencies** — via
> Executive Orders and federal policies. For everyone else (private sector,
> international organizations, healthcare, finance) it is voluntary — though
> strongly recommended. This distinction is a very common MCQ trap.

---

**Q28. Which NIST SP 800 publication provides guidance specifically for
conducting risk assessments?**

A) SP 800-12
B) SP 800-30 ✅
C) SP 800-61
D) SP 800-92

> **Explanation:** **SP 800-30 = Guide for Conducting Risk Assessments.**
> SP 800-12 = Introduction to Computer Security. SP 800-61 = Incident
> Handling Guide. SP 800-92 = Log Management Guide. Knowing the key SP 800
> numbers is directly tested in MCQs.

---

**Q29. The NIST CSF category that covers inventory and management of all
hardware, software, and data assets belongs to which function?**

A) Protect
B) Detect
C) Recover
D) Identify ✅

> **Explanation:** **Asset Management falls under Identify** — you must first
> know what assets you have before you can protect, detect, respond, or
> recover. Asset inventory is a foundational Identify activity. Protect would
> cover protecting those assets once identified.

---

**Q30. An organization maps its current security activities to the NIST CSF
and then defines where it wants to be in 12 months. It uses the gap to
build a prioritized action plan. Which CSF components is this organization
using?**

A) Framework Core and Implementation Tiers only
B) Implementation Tiers and Framework Profiles only
C) Framework Core and Framework Profiles only
D) All three — Framework Core, Implementation Tiers, and Framework
   Profiles ✅

> **Explanation:** This scenario uses **all three components**: The
> **Framework Core** (the functions/activities being mapped), **Framework
> Profiles** (current state mapped, target defined, gap identified), and
> implicitly **Implementation Tiers** (describing how well practices are
> integrated). A complete CSF implementation uses all three together.

---

## 📊 Quick Answer Key

| Q | Ans | Q | Ans | Q | Ans |
|---|---|---|---|---|---|
| 1 | B | 11 | D | 21 | C |
| 2 | C | 12 | C | 22 | C |
| 3 | C | 13 | C | 23 | D |
| 4 | C | 14 | C | 24 | D |
| 5 | B | 15 | C | 25 | B |
| 6 | D | 16 | B | 26 | B |
| 7 | B | 17 | D | 27 | C |
| 8 | C | 18 | C | 28 | B |
| 9 | D | 19 | B | 29 | D |
| 10 | C | 20 | C | 30 | D |

---

## 🎯 Topic Coverage Map

| Topic | MCQs Covered |
|---|---|
| NIST — full name, department | Q1 |
| CSF origin — Executive Order 13636 | Q2 |
| 3 CSF Components | Q3, Q30 |
| Framework Core — WHAT | Q4 |
| 5 Functions — correct order | Q5 |
| Identify function | Q6, Q29 |
| Protect function | Q7 |
| Detect function | Q8 |
| Respond function | Q9 |
| Recover function | Q10 |
| Tier names — all 4 | Q11, Q12, Q13 |
| Tiers ≠ Maturity levels | Q14 |
| Current vs Target Profile | Q15, Q16 |
| CSF version history | Q17 |
| CSF 2.0 — Govern function | Q18, Q19 |
| SP 800-37 = RMF | Q20 |
| SP 800-53 = Controls | Q21 |
| RMF 7 Steps — correct order | Q22 |
| RMF Step — Categorize | Q23 |
| RMF Step — Authorize / ATO | Q24 |
| SP 800-171 — CUI | Q25 |
| NIST vs ISO 27001 | Q26 |
| Voluntary vs Mandatory | Q27 |
| SP 800 series numbers | Q28 |

---