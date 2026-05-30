# 🎯 MCQ — Session 06: SOX & SOC Reports

> 30 MCQs | Raw Fundamentals | 4 Options Each | Full Explanations
> Covers: SOX Overview, Key Sections, ITGCs, ITACs, COSO, SOC Reports,
> SOC 1/2/3, Trust Services Criteria, Type I vs Type II,
> Auditor Process + Extra Notes

---

## MCQ Set

---

**Q1. SOX (Sarbanes-Oxley Act) was passed in response to which
corporate scandals?**

A) Lehman Brothers and Bear Stearns collapses
B) Bernie Madoff Ponzi scheme and AIG fraud
C) Enron and WorldCom accounting scandals ✅
D) Tyco and HealthSouth insider trading cases

> **Explanation:** **SOX was directly triggered by Enron (2001) and
> WorldCom (2002)**. Enron hid billions in debt and WorldCom committed
> an $11 billion accounting fraud — the largest in US history at the
> time. These scandals destroyed investor trust and forced Congress to
> act. Tyco was also involved but Enron and WorldCom are the primary
> triggers cited in SOX history.

---

**Q2. SOX (Sarbanes-Oxley Act) was signed into law on which date
and by which mechanism?**

A) 15 July 2001 — Executive Order
B) 30 July 2002 — US Federal Law ✅
C) 25 May 2002 — SEC Regulation
D) 1 January 2003 — PCAOB Standard

> **Explanation:** SOX was **signed into law on 30 July 2002** as a
> **US Federal Law** — not an executive order, SEC regulation, or
> PCAOB standard. It was passed by Congress and signed by President
> George W. Bush. Its full name is the Sarbanes-Oxley Act of 2002,
> named after Senator Paul Sarbanes and Representative Michael Oxley.

---

**Q3. SOX applies to which category of organizations?**

A) All US-based companies regardless of size
B) Only US government agencies and departments
C) All healthcare organizations handling patient data
D) Publicly traded companies listed on US stock exchanges ✅

> **Explanation:** SOX applies specifically to **publicly traded
> companies listed on US stock exchanges** — including foreign companies
> listed in the USA. It does NOT apply to private companies, government
> agencies, or sector-specific organizations like healthcare. Size does
> not matter — if a company is publicly traded on a US exchange, SOX
> applies.

---

**Q4. Which US federal agency is responsible for enforcing SOX
compliance?**

A) PCAOB
B) AICPA
C) SEC ✅
D) NIST

> **Explanation:** The **SEC (Securities and Exchange Commission)**
> enforces SOX — it issues rules, regulations, and enforcement actions.
> **PCAOB** was created BY SOX to oversee auditors — it does not enforce
> SOX directly. AICPA governs the SOC reporting framework — a completely
> different thing. NIST creates cybersecurity frameworks.

---

**Q5. Which SOX section is MOST relevant to IT auditors and
cybersecurity professionals?**

A) Section 302
B) Section 404 ✅
C) Section 409
D) Section 802

> **Explanation:** **Section 404** requires management to assess and
> report on the effectiveness of **Internal Controls over Financial
> Reporting (ICFR)** — this drives all SOX IT compliance work including
> ITGCs, ITACs, and COSO-based assessments. Section 302 covers CEO/CFO
> certifications. Section 409 covers real-time disclosures. Section 802
> covers document preservation.

---

**Q6. Under SOX Section 302, who is personally required to certify
the accuracy of financial statements?**

A) The Chief Information Security Officer (CISO)
B) The Internal Audit team
C) The CEO and CFO ✅
D) The PCAOB-registered external auditor

> **Explanation:** **Section 302** requires **CEO and CFO** to personally
> certify the accuracy of financial statements. They cannot blame IT
> failures or subordinates for inaccuracies. This personal accountability
> was one of SOX's most significant reforms — executives can face criminal
> charges for false certifications under Section 906.

---

**Q7. SOX Section 802 makes which activity a criminal offense
punishable by up to 20 years imprisonment?**

A) Failing to appoint a Data Protection Officer
B) Sharing financial data with competitors
C) Destroying, altering, or falsifying financial records ✅
D) Missing a quarterly financial reporting deadline

> **Explanation:** **Section 802** criminalizes **destroying, altering,
> concealing, or falsifying records** with intent to obstruct a federal
> investigation. Up to **20 years imprisonment** for individuals. This
> is why organizations must implement strict document preservation and
> audit trail controls — violating 802 is a serious criminal offense,
> not just a compliance failure.

---

**Q8. The Public Company Accounting Oversight Board (PCAOB) was
created by:**

A) The SEC as a regulatory body before SOX
B) The AICPA to oversee service organization audits
C) SOX Section 101 to oversee public company auditors ✅
D) The US Department of Commerce to regulate accounting standards

> **Explanation:** **PCAOB was created by SOX Section 101** — it is
> a direct product of the Sarbanes-Oxley Act. Before SOX, auditors
> of public companies were self-regulated through the AICPA. SOX
> removed self-regulation and created PCAOB as an independent
> oversight body. PCAOB reports to the SEC.

---

**Q9. IT General Controls (ITGCs) in SOX compliance are best
described as:**

A) Controls built into specific financial applications like ERP systems
B) Foundational IT controls that apply across all systems supporting
   financial reporting ✅
C) Physical security controls for data center access
D) Automated controls that validate input data in financial systems

> **Explanation:** **ITGCs are foundational controls** applying across
> ALL IT systems that support financial reporting — not just specific
> applications. They cover access controls, change management, computer
> operations, program development, and physical security. ITACs (not
> ITGCs) are controls built into specific applications. If ITGCs fail,
> all ITACs built on top of them are unreliable.

---

**Q10. Which of the following is an example of an IT Application
Control (ITAC) rather than an IT General Control (ITGC)?**

A) Change management process requiring testing before deployment
B) Logical access control restricting who can log into financial systems
C) Backup and recovery procedures for financial data
D) Automated validation rejecting negative invoice amounts ✅

> **Explanation:** **Automated input validation** (rejecting negative
> invoice amounts) is an **ITAC** — a control built into a specific
> financial application. ITGCs include change management (A), logical
> access across systems (B), and backup procedures (C). The key
> distinction: ITGCs are broad/foundational; ITACs are specific to
> an application.

---

**Q11. The primary framework organizations use to assess Internal
Controls over Financial Reporting (ICFR) under SOX Section 404 is:**

A) NIST SP 800-53
B) ISO/IEC 27001
C) COSO ✅
D) COBIT

> **Explanation:** **COSO (Committee of Sponsoring Organizations)**
> is the **primary framework for SOX 404 ICFR assessment**. COBIT is
> used alongside COSO specifically for IT controls within the SOX
> program. NIST SP 800-53 and ISO 27001 are information security
> frameworks — not the primary SOX internal control framework.

---

**Q12. COSO defines how many components of internal control?**

A) 3
B) 4
C) 5 ✅
D) 7

> **Explanation:** COSO defines exactly **5 components** of internal
> control: Control Environment, Risk Assessment, Control Activities,
> Information and Communication, and Monitoring Activities. These
> five components work together to provide reasonable assurance of
> achieving financial reporting objectives.

---

**Q13. In the COSO framework, "tone at the top" — management's
commitment to integrity and ethical values — refers to which
component?**

A) Risk Assessment
B) Control Activities
C) Monitoring Activities
D) Control Environment ✅

> **Explanation:** The **Control Environment** is the foundation of
> the COSO framework and represents the "tone at the top" — the
> culture, values, and commitment to integrity set by management and
> the board. It influences all other components. Without a strong
> control environment, the other four components cannot function
> effectively.

---

**Q14. SOC stands for and was developed by which organization?**

A) Security Operations Center — developed by NIST
B) System and Organization Controls — developed by AICPA ✅
C) Service Oversight Controls — developed by SEC
D) Security Oversight Committee — developed by ISO

> **Explanation:** **SOC = System and Organization Controls** (formerly
> Service Organization Controls) and was developed by the **AICPA
> (American Institute of Certified Public Accountants)**. NIST develops
> cybersecurity frameworks. SEC enforces SOX. ISO publishes international
> standards. SOC reports are produced under AICPA's SSAE 18 standard.

---

**Q15. The fundamental difference between SOX and SOC is:**

A) SOX applies to service organizations; SOC applies to public companies
B) SOX is a US law for public companies; SOC is an AICPA audit
   reporting framework for service organizations ✅
C) SOX produces audit reports; SOC is enforced by the SEC
D) SOX and SOC are different names for the same compliance requirement

> **Explanation:** This is the **#1 confusion in this session**:
> **SOX = US Federal Law** (2002) — applies to publicly traded
> companies — enforced by SEC.
> **SOC = Audit reporting framework** — created by AICPA — used by
> service organizations to demonstrate control effectiveness.
> They are connected (SOX may require SOC 1 from service providers)
> but are completely different things.

---

**Q16. SOC 1 reports focus specifically on:**

A) Cybersecurity risk management programs
B) Controls relevant to user entities' financial reporting ✅
C) Security, availability, and privacy controls
D) General public disclosure of security posture

> **Explanation:** **SOC 1** covers controls at a service organization
> that are **relevant to user entities' financial reporting**. It is
> used by payroll processors, loan servicers, and other organizations
> whose services affect their clients' financial statements. SOC 2
> covers security and TSC. SOC 3 is the public summary.

---

**Q17. Which SOC report is designed for general public distribution
and can be posted on an organization's website?**

A) SOC 1 Type II
B) SOC 2 Type I
C) SOC 2 Type II
D) SOC 3 ✅

> **Explanation:** **SOC 3 is the only publicly distributable SOC
> report** — it contains the same scope as SOC 2 but with significantly
> less detail, making it appropriate for general public consumption.
> Organizations can display an AICPA SOC 3 seal on their website.
> SOC 1 and SOC 2 are restricted reports — typically shared only
> under NDA with customers and regulators.

---

**Q18. In SOC 2, which of the 5 Trust Services Criteria is the ONLY
mandatory one?**

A) Availability
B) Confidentiality
C) Privacy
D) Security ✅

> **Explanation:** **Security is the ONLY mandatory Trust Services
> Criteria** in SOC 2. All other four — Availability, Processing
> Integrity, Confidentiality, and Privacy — are optional and included
> based on the nature of the service. This is one of the most tested
> facts in this session. A SOC 2 report MUST include Security; it
> may or may not include the others.

---

**Q19. A payment processing company wants a SOC 2 report that also
covers whether transactions are complete, valid, accurate, and
timely. Which Trust Services Criteria should they include?**

A) Availability
B) Privacy
C) Processing Integrity ✅
D) Confidentiality

> **Explanation:** **Processing Integrity** covers whether system
> processing is complete, valid, accurate, timely, and authorized —
> exactly what a payment processor needs to demonstrate. Availability
> covers uptime. Confidentiality covers protection of confidential
> information. Privacy covers personal data handling per AICPA
> privacy principles.

---

**Q20. The key difference between SOC 2 Type I and SOC 2 Type II
is:**

A) Type I covers security only; Type II covers all 5 Trust Services
   Criteria
B) Type I is public; Type II is restricted to customers only
C) Type I tests design at a point in time; Type II tests design
   AND operating effectiveness over a minimum 6-month period ✅
D) Type I is conducted by internal auditors; Type II by external
   CPA firms

> **Explanation:** The critical distinction:
> **Type I = design of controls at a SINGLE POINT IN TIME** — does
> the control exist and is it designed correctly?
> **Type II = design AND operating effectiveness OVER A PERIOD** —
> minimum 6 months — do the controls actually work consistently?
> Type II provides significantly stronger assurance and is preferred
> by enterprise customers. Both are conducted by external CPA firms.

---

**Q21. Most enterprise customers requiring assurance about a cloud
provider's security controls would request which report?**

A) SOC 1 Type I
B) SOC 2 Type I
C) SOC 3
D) SOC 2 Type II ✅

> **Explanation:** **SOC 2 Type II** is the gold standard for enterprise
> customers evaluating cloud providers and service organizations. It
> covers security (and relevant TSC) AND proves controls operated
> effectively over a minimum 6-month period — not just that they
> were designed correctly. SOC 2 Type I only proves design, not
> effectiveness. SOC 3 lacks sufficient detail for enterprise due
> diligence.

---

**Q22. The current AICPA auditing standard governing SOC 1 and
SOC 2 reports is:**

A) SAS 70
B) SSAE 16
C) SSAE 18 ✅
D) SSAE 20

> **Explanation:** **SSAE 18** (Statement on Standards for Attestation
> Engagements No. 18) is the **current standard** — effective from
> May 2017. The evolution is: **SAS 70 (1992–2011) → SSAE 16
> (2011–2017) → SSAE 18 (2017–present)**. SAS 70 was the original
> standard. SSAE 16 created the SOC framework. SSAE 18 enhanced
> requirements including subservice organization obligations.

---

**Q23. SAS 70 was the predecessor to the current SOC auditing
framework. When was it replaced and by what?**

A) Replaced in 2005 by SSAE 16
B) Replaced in 2011 by SSAE 16 ✅
C) Replaced in 2011 by SSAE 18
D) Replaced in 2017 by SSAE 16

> **Explanation:** **SAS 70 was replaced by SSAE 16 in 2011.**
> SSAE 16 then created the formal SOC 1 framework. SSAE 16 itself
> was later replaced by **SSAE 18 in May 2017**. So the complete
> evolution is: SAS 70 → SSAE 16 (2011) → SSAE 18 (2017). Knowing
> these transition years is directly tested in MCQs.

---

**Q24. SOX Section 404 has two sub-requirements — 404(a) and 404(b).
Which correctly describes 404(b)?**

A) Management's annual assessment of ICFR effectiveness
B) The requirement to use COSO framework for internal control
C) External auditor's attestation to management's 404(a) assessment ✅
D) The CEO and CFO personal certification of financial statements

> **Explanation:** **Section 404(b)** requires the **external auditor
> (PCAOB-registered)** to independently attest to management's
> Section 404(a) assessment of ICFR. This means TWO opinions on
> internal controls: management's own assessment (404a) AND the
> external auditor's independent attestation (404b). Section 302
> covers CEO/CFO certifications.

---

**Q25. Which classification of SOX control deficiency is the MOST
serious and requires PUBLIC DISCLOSURE in the annual report?**

A) Control Deficiency
B) Significant Deficiency
C) Material Weakness ✅
D) Critical Finding

> **Explanation:** **Material Weakness** is the most serious
> classification — it means there is a reasonable possibility of a
> material misstatement in financial statements. It MUST be publicly
> disclosed in the company's annual report (Form 10-K). This public
> disclosure can devastate investor confidence and stock price.
> Significant Deficiency is reported to the audit committee but
> not publicly disclosed. Control Deficiency is internal only.

---

**Q26. An organization's SOC 2 audit results in a report stating
that controls are suitably designed and operating effectively with
no exceptions noted. This is classified as which type of auditor
opinion?**

A) Qualified Opinion
B) Adverse Opinion
C) Disclaimer of Opinion
D) Unqualified (Clean) Opinion ✅

> **Explanation:** **Unqualified (Clean) Opinion** = controls are
> suitably designed AND operating effectively with no material
> exceptions — the best possible outcome. Qualified = generally
> effective but with specific exceptions noted. Adverse = controls
> are NOT effective — serious red flag. Disclaimer = auditor could
> not form an opinion due to insufficient evidence.

---

**Q27. Which of the following correctly describes the relationship
between SOX and SOC 1 reports?**

A) SOC 1 was created by SOX as a mandatory requirement for all
   public companies
B) SOC 1 replaced SOX as the primary financial controls framework
C) A company subject to SOX may require its service providers to
   produce SOC 1 reports to satisfy Section 404 requirements ✅
D) SOC 1 and SOX have no relationship — they are completely
   independent frameworks

> **Explanation:** SOX and SOC are different but **connected** — a
> company subject to **SOX Section 404** needs to understand controls
> at its service providers (payroll, cloud, etc.) that affect its
> financial reporting. A **SOC 1 report** from those service providers
> gives the SOX-subject company and its auditors the evidence they
> need. SOC 1 was not created by SOX and SOX does not mandate SOC 1
> specifically — but SOC 1 is the standard way to satisfy SOX
> requirements for service organization controls.

---

**Q28. A cloud SaaS company that processes HR data including salaries
and personal information for its clients wants to demonstrate both
security and privacy controls. Which SOC 2 criteria combination
is most appropriate?**

A) Security only — it is the only mandatory criteria
B) Security + Availability
C) Security + Processing Integrity + Confidentiality
D) Security + Privacy ✅

> **Explanation:** For a company processing **HR data including
> personal information**, **Security** (mandatory) PLUS **Privacy**
> (for personal data handling) is the most appropriate combination.
> Availability would be relevant for uptime commitments. Processing
> Integrity is more relevant for transaction processors. The Privacy
> TSC specifically covers personal information collection, use,
> retention, and disclosure — directly relevant to HR data.

---

**Q29. Which of the following is a SOX violation related to
Segregation of Duties (SOD)?**

A) Using encryption for financial data at rest
B) Allowing the same person to initiate AND approve financial
   transactions ✅
C) Conducting quarterly vulnerability scans of financial systems
D) Implementing multi-factor authentication for financial system
   access

---

> **Explanation:** **Allowing the same person to both initiate AND
> approve financial transactions** violates **Segregation of Duties**
> — a fundamental SOX internal control requirement. SOD ensures no
> single person has end-to-end control over a financial process,
> preventing undetected fraud. The other options are good security
> practices that SUPPORT SOX compliance — not violations.

---

**Q30. Which combination of SOX/SOC facts is entirely correct?**

A) SOX enforced by AICPA / SOC 2 Security criteria optional /
   PCAOB created before SOX / Type II = point in time
B) SOX enforced by SEC / SOC 2 Security mandatory / PCAOB created
   by SOX / Type II = min 6 months operating effectiveness ✅
C) SOX enforced by SEC / SOC 2 Security optional / PCAOB created
   by AICPA / Type I = min 6 months
D) SOX enforced by PCAOB / SOC 2 Security mandatory / SSAE 18
   replaced by SSAE 16 / Type II = point in time

> **Explanation:** The fully correct combination is:
> **SOX enforced by SEC** ✅ (not AICPA or PCAOB)
> **SOC 2 Security criteria is MANDATORY** ✅ (not optional)
> **PCAOB created BY SOX** ✅ (not before SOX, not by AICPA)
> **Type II = minimum 6 months operating effectiveness** ✅
> (not point in time — that's Type I)
> All four facts correct = Option B.

---

## 📊 Quick Answer Key

| Q | Ans | Q | Ans | Q | Ans |
|---|---|---|---|---|---|
| 1 | C | 11 | C | 21 | D |
| 2 | B | 12 | C | 22 | C |
| 3 | D | 13 | D | 23 | B |
| 4 | C | 14 | B | 24 | C |
| 5 | B | 15 | B | 25 | C |
| 6 | C | 16 | B | 26 | D |
| 7 | C | 17 | D | 27 | C |
| 8 | C | 18 | D | 28 | D |
| 9 | B | 19 | C | 29 | B |
| 10 | D | 20 | C | 30 | B |

---

## 🎯 Topic Coverage Map

| Topic | MCQs Covered |
|---|---|
| SOX triggers — Enron/WorldCom | Q1 |
| SOX signed into law — date and type | Q2 |
| SOX applicability — public companies | Q3 |
| SEC enforces SOX | Q4 |
| Section 404 — most IT-relevant | Q5 |
| Section 302 — CEO/CFO certification | Q6 |
| Section 802 — document destruction | Q7 |
| PCAOB created by SOX | Q8 |
| ITGCs — foundational controls | Q9 |
| ITGCs vs ITACs distinction | Q10 |
| COSO — primary SOX 404 framework | Q11 |
| COSO — 5 components count | Q12 |
| COSO — Control Environment = tone at top | Q13 |
| SOC — full name, created by AICPA | Q14 |
| SOX vs SOC — fundamental distinction | Q15 |
| SOC 1 — financial reporting controls | Q16 |
| SOC 3 — public distribution | Q17 |
| Security = only mandatory TSC | Q18 |
| Processing Integrity TSC | Q19 |
| Type I vs Type II — key difference | Q20 |
| SOC 2 Type II — enterprise standard | Q21 |
| SSAE 18 — current standard | Q22 |
| SAS 70 → SSAE 16 transition (2011) | Q23 |
| Section 404(b) — external auditor | Q24 |
| Material Weakness — public disclosure | Q25 |
| Unqualified opinion — best outcome | Q26 |
| SOX and SOC 1 — connection | Q27 |
| SOC 2 TSC selection — scenario | Q28 |
| SOX violation — SOD breach | Q29 |
| Combined facts — all key concepts | Q30 |

---