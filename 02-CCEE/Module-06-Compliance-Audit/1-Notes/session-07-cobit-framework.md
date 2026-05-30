# 🏛️ Session 07 — COBIT Framework

## 📑 Table of Contents
- [What is COBIT](#what-is-cobit)
- [COBIT Overview](#cobit-overview)
- [History of COBIT](#history)
- [COBIT Components](#cobit-components)
  - [Principles](#principles)
  - [Governance System Components](#governance-system)
  - [Goals Cascade](#goals-cascade)
- [COBIT Domains](#cobit-domains)
  - [COBIT 4.1 Domains](#cobit41)
  - [COBIT 5 Domains](#cobit5)
  - [COBIT 2019 Domains](#cobit2019)
- [COBIT Design Factors](#design-factors)
- [COBIT Focus Areas](#focus-areas)
- [COBIT vs ITIL](#cobit-vs-itil)
- [📌 Extra Notes](#extra-notes)
  - [COBIT Governance vs Management](#gov-vs-mgmt)
  - [COBIT 5 Principles — All 5](#cobit5-principles)
  - [COBIT 2019 Principles — All 6](#cobit2019-principles)
  - [PAM — Performance Assessment Model](#pam)
  - [COBIT and Other Frameworks](#cobit-others)
  - [ISACA — The Organization Behind COBIT](#isaca)
  - [COBIT Implementation Phases](#implementation)
  - [COBIT Maturity Model](#maturity)
- [Abbreviations](#abbreviations)
- [Keywords & Concept Map](#keywords)
- [Quick Reference Cheatsheet](#cheatsheet)
- [Session Revision Snapshot](#snapshot)

---

## 🔰 What is COBIT <a name="what-is-cobit"></a>

- **COBIT = Control Objectives for Information and Related Technologies**
- A **framework for IT governance and management**
- Developed and maintained by **ISACA (Information Systems Audit and
  Control Association)**
- Provides a comprehensive set of **best practices, tools, and models**
  for IT governance
- Bridges the gap between **business objectives and IT goals**
- Helps organizations ensure that **IT creates value** while managing
  risk and optimizing resources
- Used globally by organizations of all sizes and sectors

> [!NOTE]
> COBIT is NOT just a security framework — it is an **IT governance
> framework**. Security is one part of what COBIT covers. Its primary
> focus is ensuring IT is aligned with business goals and delivers value
> while managing risk effectively.

---

## 🏢 COBIT Overview <a name="cobit-overview"></a>

### Key Facts

| Attribute | Detail |
|---|---|
| **Full Name** | Control Objectives for Information and Related Technologies |
| **Developed By** | ISACA (Information Systems Audit and Control Association) |
| **Type** | IT Governance and Management Framework |
| **First Published** | 1996 |
| **Current Version** | COBIT 2019 |
| **Purpose** | Align IT with business goals, manage IT risk, optimize IT resources |
| **Applicability** | Any organization — any size, sector, country |
| **Certification** | ❌ No organization certification — individual certifications available |
| **Key Relationship** | Works alongside ISO 27001, NIST, ITIL, COSO |

### Why COBIT Matters
- Organizations need IT to deliver business value — not just function
- IT must be **governed** (strategic direction) AND **managed**
  (operational execution)
- COBIT provides the **bridge** between business leadership and IT
- Helps answer: *"Is our IT doing what it should? Is it creating value?
  Is it managing risk properly?"*
- Used by IT auditors, CISOs, CIOs, compliance officers, and boards

---

## 📜 History of COBIT <a name="history"></a>

```
1996 → COBIT 1 published by ISACA
        Focus: IT audit — control objectives for auditors
        Based on existing standards and practices

1998 → COBIT 2 published
        Expanded to include management guidelines
        Added maturity models

2000 → COBIT 3 published
        Added management guidelines and maturity model
        Introduced IT governance concepts

2005 → COBIT 4.0 published
        Major expansion of governance focus
        Added IT governance framework

2007 → COBIT 4.1 published
        Refined version of 4.0
        Most widely adopted version historically
        4 Domains, 34 processes, 210 control objectives

2012 → COBIT 5 published
        Complete redesign
        Merged with Val IT and Risk IT frameworks
        5 Principles, 37 processes, 5 domains
        Separated governance from management formally

2019 → COBIT 2019 published
        Updated from COBIT 5
        6 Principles, flexible design factors
        40 governance and management objectives
        More customizable and prescriptive
```

> [!TIP]
> **Key version facts for MCQs:**
> - **COBIT 4.1** = 4 domains, 34 processes, 210 control objectives
> - **COBIT 5** = 5 principles, 5 domains, 37 processes
> - **COBIT 2019** = 6 principles, 40 governance and management
>   objectives — current version

---

## 🧩 COBIT Components <a name="cobit-components"></a>

### 🏛️ Principles <a name="principles"></a>

COBIT 2019 is built on **6 principles** (COBIT 5 had 5 principles —
covered in Extra Notes):

**COBIT 2019 — 6 Principles:**

| # | Principle | Meaning |
|---|---|---|
| **1** | Provide Stakeholder Value | IT governance must deliver value to all stakeholders |
| **2** | Holistic Approach | Use all components of the governance system — not just one |
| **3** | Dynamic Governance System | Governance system must adapt to changing context |
| **4** | Governance Distinct from Management | Clear separation between governance (board) and management (executives) |
| **5** | Tailored to Enterprise Needs | Customize COBIT to the specific organization — no one-size-fits-all |
| **6** | End-to-End Governance System | Cover the entire enterprise — not just IT department |

---

### 🏗️ Governance System Components <a name="governance-system"></a>

COBIT 2019 defines **7 components** of the governance system:

| # | Component | Description |
|---|---|---|
| **1** | **Processes** | Structured activities to achieve governance/management objectives |
| **2** | **Organizational Structures** | Key decision-making entities (board, committees, management) |
| **3** | **Principles, Policies, and Frameworks** | Rules and guidelines for behavior |
| **4** | **Information** | Data needed for governance and management |
| **5** | **Culture, Ethics, and Behavior** | Values and behaviors of individuals and the organization |
| **6** | **People, Skills, and Competencies** | Human capabilities required to operate the governance system |
| **7** | **Services, Infrastructure, and Applications** | IT services and infrastructure enabling governance |

> [!IMPORTANT]
> In COBIT 5, these were called **Enablers** — there were also 7 of them
> but with slightly different names. COBIT 2019 renamed them to
> **Components**. MCQs may use either term depending on which version
> they reference.

---

### 🎯 Goals Cascade <a name="goals-cascade"></a>

The **Goals Cascade** is one of COBIT's most important concepts — it
shows how stakeholder needs translate down to actionable IT goals:

```
Stakeholder Needs
        ↓
Enterprise Goals
(17 goals across 4 BSC perspectives)
        ↓
Alignment Goals
(13 goals — IT-related)
        ↓
Governance & Management Objectives
(40 objectives in COBIT 2019)
```

### BSC Perspectives for Enterprise Goals

| Perspective | Focus |
|---|---|
| **Financial** | Value delivery, risk optimization, resource optimization |
| **Customer** | Customer-oriented service, business continuity |
| **Internal** | Process efficiency, innovation, compliance |
| **Learning & Growth** | Staff competency, culture, technology capability |

> [!NOTE]
> The **Goals Cascade** answers the fundamental question:
> *"Why should a business care about IT goals?"*
> By showing the chain from stakeholder needs → enterprise goals →
> IT goals → COBIT processes, it justifies every IT governance activity
> in business terms.

---

## 🗂️ COBIT Domains <a name="cobit-domains"></a>

### 📋 COBIT 4.1 Domains — 4 Domains <a name="cobit41"></a>

COBIT 4.1 had **4 domains** with **34 processes** and **210 control
objectives**:

| Domain | Abbreviation | Processes | Focus |
|---|---|---|---|
| **Plan and Organise** | PO | 10 | Strategy, architecture, direction setting |
| **Acquire and Implement** | AI | 7 | Solutions acquisition, change management |
| **Deliver and Support** | DS | 13 | Service delivery, security, continuity |
| **Monitor and Evaluate** | ME | 4 | Performance monitoring, compliance |

> [!TIP]
> **Memory trick for COBIT 4.1 domains:**
> **"Please All Dogs Move"**
> Plan and Organise → Acquire and Implement → Deliver and Support →
> Monitor and Evaluate

### COBIT 4.1 Key Facts Summary

| Metric | Count |
|---|---|
| Domains | 4 |
| Processes | 34 |
| Control Objectives | 210 |

---

### 📋 COBIT 5 Domains — 5 Domains <a name="cobit5"></a>

COBIT 5 reorganized into **5 domains** — split between **Governance**
and **Management**:

#### Governance Domain (1 domain)

| Domain | Abbreviation | Processes | Focus |
|---|---|---|---|
| **Evaluate, Direct, and Monitor** | EDM | 5 | Board-level governance — strategic direction |

#### Management Domains (4 domains)

| Domain | Abbreviation | Processes | Focus |
|---|---|---|---|
| **Align, Plan, and Organise** | APO | 13 | Strategy, enterprise architecture, risk |
| **Build, Acquire, and Implement** | BAI | 10 | Solutions delivery, change management |
| **Deliver, Service, and Support** | DSS | 6 | Operations, service management, security |
| **Monitor, Evaluate, and Assess** | MEA | 3 | Performance, compliance, assurance |

### COBIT 5 Key Facts Summary

| Metric | Count |
|---|---|
| Total Domains | 5 (1 governance + 4 management) |
| Total Processes | 37 |
| Principles | 5 |

> [!IMPORTANT]
> **COBIT 5 formally separated Governance (EDM) from Management
> (APO, BAI, DSS, MEA)**. This was the most significant structural
> change from COBIT 4.1. The EDM domain sits at the governance level
> (board), while the four management domains are operational (executives).

---

### 📋 COBIT 2019 Domains <a name="cobit2019"></a>

COBIT 2019 kept the same **5 domain structure** as COBIT 5 but with
updated terminology and **40 governance and management objectives**
(increased from 37 processes):

| Domain | Abbreviation | Objectives | Level |
|---|---|---|---|
| **Evaluate, Direct, and Monitor** | EDM | 6 | Governance |
| **Align, Plan, and Organise** | APO | 14 | Management |
| **Build, Acquire, and Implement** | BAI | 11 | Management |
| **Deliver, Service, and Support** | DSS | 6 | Management |
| **Monitor, Evaluate, and Assess** | MEA | 4 | Management |
| **Total** | | **40** | |

> [!NOTE]
> COBIT 2019 renamed "processes" to "governance and management
> objectives" — reflecting a more outcome-focused approach. The domain
> abbreviations (EDM, APO, BAI, DSS, MEA) remained the same as
> COBIT 5.

---

## 🎨 COBIT Design Factors <a name="design-factors"></a>

- COBIT 2019 introduced **Design Factors** — factors that influence
  the design of an organization's governance system
- Organizations use design factors to **tailor COBIT** to their
  specific context

| Design Factor | Examples |
|---|---|
| **Enterprise Strategy** | Growth, innovation, cost leadership, compliance |
| **Enterprise Goals** | From the Goals Cascade |
| **Risk Profile** | Current risk issues and risk appetite |
| **IT-Related Issues** | Current pain points and problems |
| **Threat Landscape** | External threat environment |
| **Compliance Requirements** | Regulatory and legal requirements |
| **Role of IT** | Support, factory, turnaround, or strategic |
| **Sourcing Model** | Insourced, outsourced, cloud |
| **IT Implementation Methods** | Agile, DevOps, traditional |
| **Enterprise Size** | Small, medium, large |
| **Sector/Industry** | Finance, healthcare, government, etc. |

> [!TIP]
> Design Factors are what make COBIT 2019 **more flexible** than
> COBIT 5. Instead of a one-size-fits-all approach, organizations
> analyze their design factors and prioritize the governance objectives
> most relevant to them.

---

## 🎯 COBIT Focus Areas <a name="focus-areas"></a>

COBIT 2019 introduced **Focus Areas** — specialized guidance for
particular governance topics:

| Focus Area | Description |
|---|---|
| **Information Security** | Specific guidance for IT security governance |
| **DevOps** | Governance for DevOps environments |
| **Digital Transformation** | Governance during digital change |
| **Cloud Computing** | Governance for cloud environments |
| **Privacy** | Privacy governance aligned to regulations like GDPR |
| **Cybersecurity** | Specific cybersecurity governance guidance |
| **Agile** | Governance for agile development environments |
| **Small and Medium Enterprises** | Scaled-down COBIT for SMEs |

---

## 🔄 COBIT vs ITIL <a name="cobit-vs-itil"></a>

This is one of the most tested comparisons in this session:

| Feature | COBIT | ITIL |
|---|---|---|
| **Full Name** | Control Objectives for Information and Related Technologies | Information Technology Infrastructure Library |
| **Developed By** | ISACA | AXELOS (originally UK government OGC) |
| **Focus** | IT **governance** — strategic direction and oversight | IT **service management** — operational delivery |
| **Level** | Strategic and governance | Operational and tactical |
| **Question It Answers** | *"Is IT doing the right things?"* | *"Is IT doing things right?"* |
| **Scope** | Entire IT governance — risk, compliance, value, resources | IT service lifecycle — design, transition, operation |
| **Audience** | Board, CIO, IT auditors, compliance officers | IT managers, service desk, operations teams |
| **Certification** | Individual certifications (ISACA) | Individual certifications (AXELOS — ITIL 4) |
| **Organization Certification** | ❌ No | ❌ No |
| **Relationship** | Complementary — COBIT provides governance context | Complementary — ITIL provides operational processes |
| **Mandatory** | Voluntary | Voluntary |
| **Current Version** | COBIT 2019 | ITIL 4 (2019) |

> [!IMPORTANT]
> **COBIT and ITIL are complementary — not competitors.**
> COBIT governs WHAT IT should do and WHY (strategic).
> ITIL defines HOW IT services should be delivered (operational).
> Many organizations use BOTH together — COBIT for governance,
> ITIL for operations. This relationship is a very common MCQ topic.

### The Classic One-Line Distinction

```
COBIT → "Are we doing the RIGHT things?" (Governance)
ITIL  → "Are we doing things RIGHT?"    (Operations)
```

---

## 📌 Extra Notes <a name="extra-notes"></a>

> [!NOTE]
> Everything in this section goes beyond the core syllabus but is
> directly MCQ-relevant. Cross-referenced from ISACA COBIT
> documentation and IT governance literature. Zero internet needed
> after reading this.

---

### 🏛️ COBIT Governance vs Management <a name="gov-vs-mgmt"></a>

One of COBIT's most fundamental concepts — formally introduced in
COBIT 5:

| Aspect | Governance | Management |
|---|---|---|
| **Who** | Board of Directors / Owners | CEO, CIO, Executives |
| **What** | Sets direction, evaluates, monitors | Plans, builds, runs, monitors |
| **Domain (COBIT 5/2019)** | EDM | APO, BAI, DSS, MEA |
| **Question** | Are we achieving stakeholder value? | How do we achieve it? |
| **Activities** | Evaluate options, direct strategy, monitor performance | Plan, organize, build, acquire, deliver, support |
| **Accountability** | Accountable for outcomes | Responsible for execution |

> [!IMPORTANT]
> **Governance ≠ Management** — this is COBIT's most fundamental
> distinction. Governance is about setting direction and oversight
> (board level). Management is about execution (operational level).
> Confusing these two is a very common MCQ trap.

---

### 📋 COBIT 5 Principles — All 5 <a name="cobit5-principles"></a>

COBIT 5 was built on **5 principles**:

| # | Principle |
|---|---|
| **1** | Meeting Stakeholder Needs |
| **2** | Covering the Enterprise End-to-End |
| **3** | Applying a Single Integrated Framework |
| **4** | Enabling a Holistic Approach |
| **5** | Separating Governance from Management |

> [!TIP]
> **Memory trick for COBIT 5 principles:**
> **"Most Cats Always Handle Separating"**
> Meeting Stakeholder Needs → Covering Enterprise → Applying Single
> Framework → Enabling Holistic → Separating Governance

---

### 📋 COBIT 2019 Principles — All 6 <a name="cobit2019-principles"></a>

COBIT 2019 updated to **6 principles**:

| # | Principle | Change from COBIT 5 |
|---|---|---|
| **1** | Provide Stakeholder Value | Updated from "Meeting Stakeholder Needs" |
| **2** | Holistic Approach | Updated from "Enabling a Holistic Approach" |
| **3** | Dynamic Governance System | **NEW** — recognizes governance must adapt |
| **4** | Governance Distinct from Management | Updated from "Separating Governance from Management" |
| **5** | Tailored to Enterprise Needs | **NEW** — recognizes no one-size-fits-all |
| **6** | End-to-End Governance System | Updated from "Covering Enterprise End-to-End" |

> [!NOTE]
> COBIT 2019 added **2 new principles** compared to COBIT 5:
> **Dynamic Governance System** (Principle 3) and **Tailored to
> Enterprise Needs** (Principle 5). These reflect the increasing
> need for adaptability and customization in IT governance.

---

### 📊 PAM — Performance Assessment Model <a name="pam"></a>

- **PAM = Process Assessment Model**
- Used in COBIT to **measure the capability/maturity** of governance
  and management processes
- Based on **ISO/IEC 33000 series** (process assessment standards)
- Defines **capability levels** for each COBIT process/objective

### Capability Levels

| Level | Name | Description |
|---|---|---|
| **0** | Incomplete | Process not implemented or not achieving its purpose |
| **1** | Performed | Process achieves its purpose — basic level |
| **2** | Managed | Process is planned, monitored, and adjusted |
| **3** | Established | Process uses a defined standard process — organization-wide |
| **4** | Predictable | Process operates within defined limits — quantitatively managed |
| **5** | Optimizing | Process continuously improved to meet current and future goals |

> [!TIP]
> **0 to 5 capability levels** — similar concept to CMMI levels.
> Level 0 = broken, Level 5 = world-class continuous improvement.
> Most organizations target **Level 3 (Established)** as a realistic
> goal for critical processes.

---

### 🔗 COBIT and Other Frameworks <a name="cobit-others"></a>

COBIT is designed to **integrate with** other frameworks —
not replace them:

| Framework | Relationship to COBIT |
|---|---|
| **ITIL** | COBIT governs IT service management; ITIL operationalizes it |
| **ISO 27001** | COBIT provides governance context; ISO 27001 specifies security controls |
| **NIST CSF** | COBIT provides enterprise governance; NIST provides cybersecurity framework |
| **COSO** | Both address internal controls; COSO focuses on financial; COBIT on IT |
| **CMMI** | COBIT covers governance; CMMI covers software/process maturity |
| **ISO 38500** | Both address IT governance; ISO 38500 is principles-only; COBIT is comprehensive |
| **TOGAF** | COBIT governs enterprise architecture; TOGAF provides the EA methodology |
| **PRINCE2/PMBOK** | COBIT governs project portfolio; PRINCE2/PMBOK manage individual projects |

> [!NOTE]
> **ISO 38500** is specifically worth remembering — it is the
> international standard for IT governance (ISO/IEC 38500:2015).
> COBIT and ISO 38500 address the same domain (IT governance) but
> ISO 38500 is a high-level principles standard while COBIT is
> a comprehensive practical framework.

---

### 🏢 ISACA — The Organization Behind COBIT <a name="isaca"></a>

- **ISACA = Information Systems Audit and Control Association**
- Founded: **1969** as EDP Auditors Association
- Renamed to ISACA in 1994 (though retains original name as just "ISACA")
- Headquarters: **Schaumburg, Illinois, USA**
- Global membership: **over 165,000 members** in 180+ countries
- Develops and maintains **COBIT**
- Also maintains key certifications:

| Certification | Full Name | Focus |
|---|---|---|
| **CISA** | Certified Information Systems Auditor | IS audit, control, assurance |
| **CISM** | Certified Information Security Manager | Information security management |
| **CRISC** | Certified in Risk and Information Systems Control | IT risk management |
| **CGEIT** | Certified in the Governance of Enterprise IT | IT governance |
| **CDPSE** | Certified Data Privacy Solutions Engineer | Data privacy |

> [!TIP]
> **ISACA certifications are frequently tested** in MCQs related to
> COBIT. CISA is the most widely recognized — it is specifically
> for IS auditors. CGEIT is the most directly COBIT-related
> certification.

---

### 🚀 COBIT Implementation Phases <a name="implementation"></a>

COBIT 2019 defines a **continual improvement lifecycle** for
implementation using 7 phases:

```
Phase 1 → What are the Drivers?
           Understand why COBIT implementation is needed
           Identify pain points and opportunities

Phase 2 → Where are we Now?
           Assess current state of IT governance
           Identify gaps using capability assessment

Phase 3 → Where do we Want to Be?
           Define target state — desired capability levels
           Prioritize improvement areas

Phase 4 → What Needs to be Done?
           Plan improvements — projects and initiatives

Phase 5 → How do we Get There?
           Implement the improvement plan
           Execute projects

Phase 6 → Did we Get There?
           Monitor and evaluate results
           Measure actual vs target capability levels

Phase 7 → How do we Keep the Momentum Going?
           Embed improvements into operations
           Review and update the governance system
```

> [!NOTE]
> The **7-phase implementation lifecycle** reflects the **continual
> improvement** philosophy central to COBIT — similar to PDCA in
> ISO 27001. The cycle then restarts — governance improvement is
> never "done."

---

### 📈 COBIT Maturity Model <a name="maturity"></a>

- COBIT 4.1 used a **Maturity Model** — rated processes on a scale
  of **0 to 5**
- COBIT 5 and 2019 replaced this with the **Capability Model**
  (also 0–5 levels) based on ISO/IEC 15504 (now ISO/IEC 33000)

### COBIT 4.1 Maturity Levels

| Level | Name | Description |
|---|---|---|
| **0** | Non-Existent | Complete lack of process — organization unaware |
| **1** | Initial / Ad Hoc | Processes exist but unorganized and reactive |
| **2** | Repeatable but Intuitive | Processes follow a regular pattern but undocumented |
| **3** | Defined Process | Processes documented and communicated |
| **4** | Managed and Measurable | Processes monitored and measured — management reviews |
| **5** | Optimised | Processes refined to best practice level — continuous improvement |

> [!IMPORTANT]
> MCQs may ask about **maturity levels** (COBIT 4.1 term) vs
> **capability levels** (COBIT 5/2019 term). Both use 0–5 scale but
> the names and the underlying model differ. The concept is similar —
> higher number = more mature/capable process.

---

## 🔤 Abbreviations <a name="abbreviations"></a>

| Abbreviation | Full Form | One-line Meaning |
|---|---|---|
| **COBIT** | Control Objectives for Information and Related Technologies | ISACA's IT governance and management framework |
| **ISACA** | Information Systems Audit and Control Association | Organization that develops and maintains COBIT |
| **EDM** | Evaluate, Direct, and Monitor | COBIT governance domain — board-level strategic direction |
| **APO** | Align, Plan, and Organise | COBIT management domain — strategy and enterprise architecture |
| **BAI** | Build, Acquire, and Implement | COBIT management domain — solutions delivery and change |
| **DSS** | Deliver, Service, and Support | COBIT management domain — operations and security |
| **MEA** | Monitor, Evaluate, and Assess | COBIT management domain — performance and compliance |
| **ITIL** | Information Technology Infrastructure Library | IT service management framework — complementary to COBIT |
| **PAM** | Process Assessment Model | Model for measuring COBIT process capability levels (0–5) |
| **BSC** | Balanced Scorecard | Strategic planning framework — used in COBIT Goals Cascade |
| **CISA** | Certified Information Systems Auditor | ISACA certification for IS audit professionals |
| **CISM** | Certified Information Security Manager | ISACA certification for security managers |
| **CGEIT** | Certified in the Governance of Enterprise IT | ISACA certification most directly related to COBIT |
| **CRISC** | Certified in Risk and Information Systems Control | ISACA certification for IT risk management |
| **Val IT** | Value IT | Former ISACA framework merged into COBIT 5 |
| **Risk IT** | Risk IT | Former ISACA framework merged into COBIT 5 |
| **PO** | Plan and Organise | COBIT 4.1 domain |
| **AI** | Acquire and Implement | COBIT 4.1 domain |
| **DS** | Deliver and Support | COBIT 4.1 domain |
| **ME** | Monitor and Evaluate | COBIT 4.1 domain |

---

## 🗝️ Keywords & Concept Map <a name="keywords"></a>

**COBIT**
→ IT governance and management framework by ISACA
→ Bridges business objectives and IT goals
→ Versions: 4.1 (34 processes) → 5 (37 processes) → 2019 (40 objectives)
→ Complementary to ITIL, ISO 27001, NIST, COSO

**IT Governance**
→ Setting strategic direction for IT — board/ownership level
→ COBIT domain: EDM (Evaluate, Direct, Monitor)
→ Answers: "Are we doing the RIGHT things?"
→ Different from management — which is operational

**IT Management**
→ Executing the strategy set by governance
→ COBIT domains: APO, BAI, DSS, MEA
→ Answers: "Are we doing things RIGHT?"
→ Different from governance — which is strategic

**COBIT 5 Domains**
→ 5 domains: EDM (governance) + APO, BAI, DSS, MEA (management)
→ 37 processes total
→ First version to formally separate governance from management

**COBIT 2019**
→ Current version — 40 governance and management objectives
→ 6 principles (added Dynamic and Tailored)
→ Introduced Design Factors for customization
→ Introduced Focus Areas for specialized guidance

**Goals Cascade**
→ Chain from stakeholder needs → enterprise goals → alignment goals
  → governance and management objectives
→ Justifies IT governance in business terms
→ Uses Balanced Scorecard (BSC) perspective for enterprise goals

**COBIT vs ITIL**
→ COBIT = governance (WHAT and WHY)
→ ITIL = service management operations (HOW)
→ Complementary — not competing
→ COBIT by ISACA / ITIL by AXELOS

---

## ⚡ Quick Reference Cheatsheet <a name="cheatsheet"></a>

### COBIT Version History

| Version | Year | Key Feature | Domains | Processes/Objectives |
|---|---|---|---|---|
| COBIT 1 | 1996 | Audit focus | — | — |
| COBIT 4.1 | 2007 | Most widely adopted historically | 4 | 34 processes, 210 control objectives |
| COBIT 5 | 2012 | Separated governance from management | 5 | 37 processes |
| COBIT 2019 | 2019 | Design factors, focus areas | 5 | 40 objectives |

### COBIT 4.1 — 4 Domains

| Domain | Abbr | Processes |
|---|---|---|
| Plan and Organise | PO | 10 |
| Acquire and Implement | AI | 7 |
| Deliver and Support | DS | 13 |
| Monitor and Evaluate | ME | 4 |
| **Total** | | **34** |

### COBIT 5 / 2019 — 5 Domains

| Domain | Abbr | Level | COBIT 5 | COBIT 2019 |
|---|---|---|---|---|
| Evaluate, Direct, Monitor | EDM | Governance | 5 | 6 |
| Align, Plan, Organise | APO | Management | 13 | 14 |
| Build, Acquire, Implement | BAI | Management | 10 | 11 |
| Deliver, Service, Support | DSS | Management | 6 | 6 |
| Monitor, Evaluate, Assess | MEA | Management | 3 | 4 |
| **Total** | | | **37** | **40** |

### COBIT 5 vs COBIT 2019 — Key Differences

| Feature | COBIT 5 | COBIT 2019 |
|---|---|---|
| Principles | 5 | 6 |
| Processes/Objectives | 37 | 40 |
| Design Factors | ❌ No | ✅ Yes |
| Focus Areas | ❌ No | ✅ Yes |
| Customization | Limited | High |

### COBIT 5 — 5 Principles

| # | Principle |
|---|---|
| 1 | Meeting Stakeholder Needs |
| 2 | Covering the Enterprise End-to-End |
| 3 | Applying a Single Integrated Framework |
| 4 | Enabling a Holistic Approach |
| 5 | Separating Governance from Management |

### COBIT 2019 — 6 Principles

| # | Principle |
|---|---|
| 1 | Provide Stakeholder Value |
| 2 | Holistic Approach |
| 3 | Dynamic Governance System |
| 4 | Governance Distinct from Management |
| 5 | Tailored to Enterprise Needs |
| 6 | End-to-End Governance System |

### COBIT Capability Levels (COBIT 5/2019)

| Level | Name |
|---|---|
| 0 | Incomplete |
| 1 | Performed |
| 2 | Managed |
| 3 | Established |
| 4 | Predictable |
| 5 | Optimizing |

### COBIT vs ITIL — Complete Comparison

| Feature | COBIT | ITIL |
|---|---|---|
| Developed by | ISACA | AXELOS |
| Focus | IT Governance | IT Service Management |
| Level | Strategic | Operational |
| Question | Doing right things? | Doing things right? |
| Current version | COBIT 2019 | ITIL 4 |
| Relationship | Governance context | Operational processes |

### ISACA Certifications

| Certification | Focus |
|---|---|
| CISA | IS Audit |
| CISM | Security Management |
| CRISC | IT Risk |
| CGEIT | IT Governance (most COBIT-related) |
| CDPSE | Data Privacy |

### Governance vs Management in COBIT

| | Governance | Management |
|---|---|---|
| Who | Board / Owners | Executives / Managers |
| Domain | EDM | APO, BAI, DSS, MEA |
| Question | Right things? | Things right? |
| Focus | Strategy + Oversight | Planning + Execution |

---

## 🔁 Session Revision Snapshot <a name="snapshot"></a>

### TL;DR — 5 Bullets
- ✅ COBIT = IT governance framework by ISACA — bridges business
  objectives and IT goals — versions: 4.1 (4 domains/34 processes)
  → 5 (5 domains/37 processes) → 2019 (5 domains/40 objectives)
- ✅ COBIT formally separates **Governance (EDM)** from **Management
  (APO, BAI, DSS, MEA)** — governance = board/strategic,
  management = operational
- ✅ COBIT 5 has **5 principles** — COBIT 2019 has **6 principles**
  (added Dynamic Governance System + Tailored to Enterprise Needs)
- ✅ COBIT vs ITIL: COBIT = governance ("right things?") by ISACA /
  ITIL = service management ("things right?") by AXELOS —
  complementary not competing
- ✅ COBIT 2019 added **Design Factors** (customization) and
  **Focus Areas** (specialized guidance) — making it more flexible
  than COBIT 5

### 🎯 Top MCQ-Likely Concepts from This Session
1. **COBIT = ISACA** — full names of both, always tested
2. **COBIT vs ITIL** — governance vs operations — complementary
3. **Governance vs Management** — EDM vs APO/BAI/DSS/MEA
4. **4.1 vs 5 vs 2019** — domain counts and process/objective counts
5. **COBIT 5 principles (5)** vs **COBIT 2019 principles (6)**
6. **EDM domain** = governance level — board responsibility
7. **Goals Cascade** — stakeholder needs → enterprise → IT goals
8. **COBIT 2019 Design Factors** — what they are and why added
9. **ISACA certifications** — especially CISA and CGEIT
10. **Val IT + Risk IT merged into COBIT 5** — historical fact
11. **Capability levels 0–5** — names and meanings

---