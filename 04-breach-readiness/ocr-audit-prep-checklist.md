# OCR Audit and Investigation Preparation Checklist

**Northgate Behavioral Health Clinic** — Security Risk Assessment
Supports every register finding · Directly addresses **R-02**

> Fictional clinic. The enforcement case referenced below is real and public.

---

## Why this checklist is built around one settlement

On 19 February 2026 the HHS Office for Civil Rights announced a settlement with **Top of the World Ranch Treatment Center**, a substance use disorder treatment provider in Illinois.

The facts, from OCR's own announcement:

- A **phishing attack** succeeded against a **workforce member's email account**.
- An unauthorised third party accessed patient information through that mailbox.
- **1,980 patients** were affected.
- OCR's investigation found the provider had **failed to conduct an accurate and thorough risk analysis** — the requirement at §164.308(a)(1)(ii)(A).
- Settlement: **$103,000** and a corrective action plan monitored for **two years**.
- OCR described it as the **11th enforcement action in its Risk Analysis Initiative**.

Three things make this the right spine for Northgate's preparation.

**It is the same kind of provider.** Behavioral health, substance use disorder services, community scale. Not a hospital system with a security department.

**It is the same attack.** Phishing into a staff mailbox — exactly **R-01**, the highest-scoring risk on Northgate's register.

**The risk analysis failure was the sole finding.** OCR did not cite missing encryption, or weak passwords, or an unsegmented network. It cited the absence of an accurate and thorough risk analysis. That is **R-02** — and it is why R-02 scores Very High on impact despite being a paperwork requirement.

The OCR Director's framing, quoted in the announcement: *"Covered entities and business associates cannot protect electronic protected health information if they haven't identified potential risks and vulnerabilities to that health information."*

---

## What OCR can actually demand

Worth knowing precisely, because it shapes how documentation should be kept.

Under the HIPAA Enforcement Rule at **45 CFR §160.310**, a covered entity must:

- **§160.310(a)** — keep records and submit compliance reports, in the time and manner and containing the information the Secretary determines necessary to establish compliance.
- **§160.310(b)** — cooperate with complaint investigations and compliance reviews.
- **§160.310(c)(1)** — **permit access by the Secretary during normal business hours** to its facilities, books, records, accounts and other sources of information, including protected health information, pertinent to establishing compliance. Where the Secretary determines **exigent circumstances** exist — such as when documents may be hidden or destroyed — access must be permitted **at any time and without notice**.
- **§160.310(c)(2)** — where required information is exclusively held by another party who refuses to provide it, the clinic must certify this and set out what efforts it made to obtain it.

Read alongside **§164.316(b)(2)(i)**, which requires documentation to be retained for **six years** from creation or from when it was last in effect, whichever is later.

The combination is the point: OCR can ask on short notice, and the clinic is expected to have kept six years of it.

**How OCR opens matters.** OCR enforces by investigating complaints, conducting compliance reviews, and through education and outreach. It also refers possible criminal violations to the Department of Justice. Most investigations of a clinic this size begin with a patient complaint or a breach report the clinic filed itself.

---

## The current audit programme

OCR has initiated its **2024–2025 HIPAA Audits**, covering **50 covered entities and business associates**, and reviewing compliance with **selected Security Rule provisions most relevant to hacking and ransomware attacks**. OCR has said it will publish an industry report once complete.

OCR also publishes a public **Audit Protocol, updated July 2018**, organised by Rule and regulatory provision, covering the Privacy, Security and Breach Notification Rules separately. It is searchable and worth reading before an audit rather than during one. Note that it assesses *selected* requirements and may vary by entity type.

---

## The document set to have ready

If OCR contacted Northgate tomorrow, these are what would be asked for. Ordered by how likely they are to be requested first.

### Tier 1 — asked for in nearly every investigation

| # | Document | Northgate status | Register link |
|---|---|---|---|
| 1 | **Current security risk analysis**, dated, covering all systems handling patient information | ⚠️ Exists but predates EPIC migration — this assessment replaces it | **R-02** |
| 2 | **Risk management plan** showing what was done about identified risks | ❌ None | **R-02** |
| 3 | **Complete list of business associates with signed agreements** | ❌ Incomplete — 3 missing, 4 unconfirmed | **R-12** |
| 4 | **Written security policies and procedures** | ⚠️ Partial, not reviewed since adoption | R-02 |
| 5 | **Evidence of workforce security training**, with dates and attendance | ⚠️ Annual general training only, not role-specific | R-01 |
| 6 | **Named security official** — who, and since when | ✅ Practice administrator | — |
| 7 | **Incident and breach log**, including incidents determined not to be breaches | ❌ None maintained | R-01 |

### Tier 2 — asked for when the investigation follows an incident

| # | Document | Northgate status | Register link |
|---|---|---|---|
| 8 | **Evidence of information system activity review** — who reviewed which logs, when | ❌ None | **R-09** |
| 9 | **User access lists** per system, with a current staff roster to reconcile against | ⚠️ Available but never reconciled | R-08 |
| 10 | **Termination records** showing access removal | ❌ No documented process | R-08 |
| 11 | **Encryption status** of laptops and removable media | ❌ Not encrypted | **R-04** |
| 12 | **Documented analysis for every addressable specification** not implemented | ❌ None — this is the gap addressable specifications create | R-04, R-10 |
| 13 | **Contingency plan**, plus evidence it has been tested | ⚠️ Plan exists, never tested | **R-10** |
| 14 | **Sanction policy** and evidence of application | ⚠️ In handbook, never applied | R-02 |
| 15 | **Network diagram** showing segmentation | ❌ None | **R-05** |

### Tier 3 — behavioral health specific

| # | Document | Northgate status | Register link |
|---|---|---|---|
| 16 | **42 CFR Part 2 applicability determination**, in writing | ❌ Never performed | **R-06** |
| 17 | If Part 2 applies: patient notice under §2.22, consent forms under §2.31, and evidence of record segregation | ❌ Not assessed | **R-06** |
| 18 | **Release-of-information log** with the authority for each disclosure | ⚠️ Inconsistent | **R-11** |

**Item 12 is the one that surprises people.** Addressable does not mean skippable. Where the clinic hasn't implemented an addressable specification, §164.306(d)(3) requires written documentation of why it isn't reasonable and appropriate, plus an equivalent alternative where one is. A clinic with no encryption *and* no documented analysis has failed the addressable standard — not because encryption was mandatory, but because the decision was never made.

---

## OCR's own eight recommendations

Published by OCR alongside the settlement described above. Cited here rather than invented, because a checklist drawn from the regulator's own post-enforcement guidance carries more weight than one assembled from general practice.

| # | OCR recommendation | Northgate gap | Register |
|---|---|---|---|
| 1 | Identify where patient information is located, including how it enters, flows through, and leaves the organisation's systems | No asset inventory existed before this assessment | R-02 |
| 2 | Periodically conduct and update a risk analysis, and develop and implement risk management measures | Stale, no management plan | **R-02** |
| 3 | Ensure audit controls are in place to record and examine system activity | Controls exist in EPIC | R-09 |
| 4 | Implement regular review of information system activity | Never performed | **R-09** |
| 5 | Use mechanisms to authenticate users seeking access to patient information | Shared logins, no multi-factor authentication | **R-01, R-03** |
| 6 | Encrypt patient information in transit and at rest to guard against unauthorised access, **when appropriate** | Not encrypted at rest | **R-04** |
| 7 | Incorporate lessons learned from incidents into the overall security management process | No incident log, no feedback loop | R-02 |
| 8 | Provide regular training specific to the organisation and to workforce members' job duties | Generic annual training only | R-01 |

Note OCR's own wording in item 6 — **"when appropriate."** Even the regulator's post-enforcement guidance preserves the addressable standard rather than describing encryption as mandatory. That is a useful corrective to the widespread claim that HIPAA requires encryption.

**Northgate's register covers all eight.** That alignment is not a coincidence — it is the test applied when the register was built.

---

## The corrective action plan to expect

If an investigation goes badly, this is roughly what gets imposed. The four commitments below are those OCR required in the settlement described above.

1. Conduct and complete an accurate and thorough risk analysis.
2. Develop and implement a **risk management plan** addressing the risks identified.
3. Develop, maintain and revise written policies and procedures for the Privacy, Security and Breach Notification Rules.
4. Provide **annual training** for workforce members with access to patient information.

Two years of monitoring, on OCR's schedule and to OCR's satisfaction.

**Every item on that list appears in `../05-remediation/remediation-roadmap.md`.** The argument this project makes is simple: doing this work voluntarily costs a fraction of doing it under a corrective action plan, and the first item on the regulator's list is the first item on the roadmap.

---

## Thirty-day readiness sprint

If Northgate wanted to be defensible quickly, in priority order:

- [ ] **Adopt this assessment as the current risk analysis.** Date it, have the administrator sign it. Closes the single most-cited gap.
- [ ] **Write the risk management plan** — the remediation roadmap, with owners and dates, is the plan.
- [ ] **Complete the vendor register and close the three missing agreements.**
- [ ] **Start an incident log**, including incidents judged not to be breaches. Absence of a log looks like absence of incidents, which nobody believes.
- [ ] **Perform one month of EPIC access review** and keep the record. One month of evidence beats a year of intention.
- [ ] **Write the Part 2 applicability determination**, whichever way it lands.
- [ ] **Document the addressable-specification decisions** for encryption and contingency testing, even where the answer is "we are implementing it next quarter."
- [ ] **Assemble a single indexed folder** with everything above, and keep it current.

That last one is the quiet differentiator. Most small clinics could eventually produce most of these documents. Very few could produce them in a week, indexed, with dates.

---

**Related:** `breach-notification-decision-tree.md` · `../05-remediation/remediation-roadmap.md` · `../01-risk-assessment/risk-register.md`
