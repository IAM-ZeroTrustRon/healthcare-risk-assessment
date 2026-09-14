# Framework Crosswalk

**Northgate Behavioral Health Clinic** — Security Risk Assessment
Mapping every risk-register finding to HIPAA, HITRUST CSF and NIST CSF 2.0

> Fictional clinic. All regulatory citations are real and were verified against primary sources — see *Sources and verification* at the end.

---

## Why a crosswalk is worth building

A clinic this size will be asked the same question by four different audiences in four different vocabularies:

- **A regulator** asks: which requirement did you fail?
- **A cyber insurer or health-system partner** asks: where do you sit against a recognised control framework?
- **A security lead** asks: what capability is missing?
- **The clinic administrator** asks: what do I actually have to go and do?

A crosswalk lets one piece of work answer all four. Fix R-03 by issuing unique logins and you have simultaneously satisfied a required HIPAA implementation specification, a HITRUST control category, and a NIST CSF outcome — and you can say so, with citations, without doing the work three times.

**The honest part:** the frameworks do not line up perfectly. Where a join is imperfect, this document says so rather than forcing the table to look tidy. Those notes are in *Where the frameworks don't map cleanly* below, and the reasoning is expanded in `../TECHNICAL-DEEP-DIVE.md`.

---

## The three frameworks in one paragraph each

**HIPAA Security Rule** (45 CFR Part 164, Subpart C) — the law. Binding on Northgate. Organised into administrative safeguards (§164.308), physical safeguards (§164.310) and technical safeguards (§164.312), plus general rules (§164.306), organisational requirements (§164.314) and documentation requirements (§164.316). Each standard contains implementation specifications marked either **Required** or **Addressable**.

**NIST Cybersecurity Framework 2.0** (NIST CSWP 29, February 2024) — voluntary. Organises cybersecurity outcomes into six Functions: **Govern, Identify, Protect, Detect, Respond, Recover**, subdivided into 22 Categories. Govern is new in version 2.0 and matters here, because HIPAA's most-cited requirements are governance requirements that had no clean home in the previous version.

**HITRUST CSF** (version 11.8.0, May 2026) — proprietary and certifiable. A control library built on ISO/IEC 27001 and 27002 that harmonises 75 authoritative sources, including all three HIPAA rules and NIST CSF 2.0. Organised into **14 control categories**, 49 control objectives and 156 control specifications.

> **A deliberate limitation.** HITRUST control references and requirement statements are licensed content. This crosswalk uses **control category names only** and does not reproduce or invent control IDs. Anyone doing this work commercially would map to specific references from a licensed copy of the CSF. Inventing plausible-looking IDs for a public portfolio would be both wrong and easy to catch.

---

## Required vs. Addressable — the distinction that gets misstated most

This matters enough to state before the tables.

- **Required** means implement it. No alternative.
- **Addressable** means: assess whether it is reasonable and appropriate for your environment; then **either** implement it, **or** document why it isn't reasonable and appropriate **and** implement an equivalent alternative measure if one is reasonable and appropriate.

Addressable is not optional. The documentation is itself the obligation, and the absence of that documentation is the finding.

**Encryption is addressable.** Both encryption of stored information (§164.312(a)(2)(iv)) and encryption of transmitted information (§164.312(e)(2)(ii)) are addressable specifications under the Security Rule as it currently stands. This is widely misreported as "required," including in a fair amount of published commentary.

A proposed rule published in the *Federal Register* on 6 January 2025 (issued by HHS on 27 December 2024) would remove that addressable designation and mandate encryption and multi-factor authentication among other changes. **As of this assessment it has not been finalised, and the current Security Rule remains in effect.** This assessment is written against the rule as it stands, and flags where the proposal would raise the bar.

---

## Master crosswalk

| Risk | Score | HIPAA Security Rule | R/A | NIST CSF 2.0 | HITRUST CSF category |
|---|---|---|---|---|---|
| **R-01** Phishing compromise of staff mailbox | 20 | §164.308(a)(5)(ii)(B) malicious software protection · §164.308(a)(5)(ii)(C) log-in monitoring · §164.308(a)(5)(ii)(D) password management · §164.312(d) person or entity authentication · §164.308(a)(6)(ii) response and reporting | A · A · A · Std · **R** | PR.AA · PR.AT · DE.CM · RS.MA | Access Control · Human Resources Security · Information Security Incident Management |
| **R-02** Risk analysis not current or thorough | 20 | §164.308(a)(1)(ii)(A) risk analysis · §164.308(a)(1)(ii)(B) risk management · §164.308(a)(8) evaluation · §164.316(b)(2)(i) six-year retention | **R** · **R** · Std · **R** | GV.RM · ID.RA · ID.IM | Risk Management · Information Security Management Program |
| **R-03** Shared and generic logins | 16 | §164.312(a)(2)(i) unique user identification · §164.312(a)(2)(iii) automatic logoff · §164.308(a)(4)(ii)(B) access authorization · §164.308(a)(4)(ii)(C) access establishment and modification | **R** · A · A · A | PR.AA | Access Control |
| **R-04** Unencrypted laptops and removable media | 15 | §164.312(a)(2)(iv) encryption and decryption · §164.310(d)(1) device and media controls · §164.310(d)(2)(i) disposal · §164.310(d)(2)(ii) media re-use · §164.306(d)(3) addressable-specification analysis | **A** · Std · **R** · **R** · Std | PR.DS | Communications and Operations Management · Asset Management |
| **R-05** Flat network | 15 | §164.312(a)(1) access control · §164.312(e)(1) transmission security · §164.308(a)(1)(ii)(A) risk analysis · §164.308(a)(1)(ii)(B) risk management | Std · Std · **R** · **R** | PR.IR · PR.PS · ID.AM | Communications and Operations Management · Asset Management |
| **R-06** Part 2 applicability and EPIC segregation | 15 | §164.308(a)(4)(i) information access management · §164.312(a)(1) access control · §164.316(a) policies and procedures — **plus 42 CFR Part 2, see below** | Std · Std · Std | GV.OC · GV.PO · PR.AA · PR.DS | Access Control · Compliance · Privacy Practices |
| **R-07** Front-of-house exposure | 12 | §164.310(b) workstation use · §164.310(c) workstation security · §164.310(a)(2)(iii) access control and validation procedures | Std · Std · A | PR.AA | Physical and Environmental Security |
| **R-08** Access not removed on departure | 12 | §164.308(a)(3)(ii)(C) termination procedures · §164.308(a)(3)(ii)(B) workforce clearance procedure · §164.308(a)(4)(ii)(C) access establishment and modification | A · A · A | PR.AA · GV.RR | Human Resources Security · Access Control |
| **R-09** EPIC logs not reviewed | 12 | §164.308(a)(1)(ii)(D) information system activity review · §164.312(b) audit controls | **R** · Std | DE.CM · DE.AE | Communications and Operations Management · Information Security Incident Management |
| **R-10** Backups never restore-tested | 12 | §164.308(a)(7)(ii)(A) data backup plan · (B) disaster recovery plan · (C) emergency mode operation plan · (D) testing and revision procedures · (E) applications and data criticality analysis | **R** · **R** · **R** · A · A | PR.DS · RC.RP | Business Continuity Management |
| **R-11** Misdirected fax and releases | 9 | §164.312(e)(1) transmission security · §164.312(e)(2)(i) integrity controls · §164.308(a)(5)(i) security awareness and training | Std · A · Std | PR.DS · PR.AT | Communications and Operations Management · Privacy Practices |
| **R-12** Incomplete vendor and agreement register | 9 | §164.308(b)(1) business associate contracts and other arrangements · §164.308(b)(3) written contract or other arrangement · §164.314(a) business associate contracts | Std · **R** · Std | GV.SC · ID.AM | Organization of Information Security · Compliance |

**Key:** **R** = Required · A = Addressable · Std = Standard (the requirement itself, with no separate implementation specification)

---

## 42 CFR Part 2 overlay — R-06 only

Substance use disorder confidentiality sits outside HIPAA and outside all three frameworks above. It is listed separately rather than jammed into the table, because forcing it in would misrepresent how it works.

| Element | Citation |
|---|---|
| Statute | 42 U.S.C. 290dd-2 |
| Regulation | 42 CFR Part 2 (§§2.1–2.68) |
| Definitions | §2.11 |
| Applicability | §2.12 |
| Confidentiality restrictions and safeguards | §2.13 |
| **Security for records and notification of breaches** | §2.16 |
| Relationship to state laws | §2.20 |
| Notice to patients of federal confidentiality requirements | §2.22 |
| Requirements for intermediaries | §2.24 |
| Consent requirements | §2.31 |

**Status.** The 2024 final rule aligning Part 2 with HIPAA took effect 16 April 2024, with **compliance required from 16 February 2026** — so it is a live obligation, not a forthcoming one. The HHS Secretary delegated administration and enforcement of Part 2 to the Director of the Office for Civil Rights on 25 August 2025, and the enforcement provisions applied are those of the HIPAA Enforcement Rule at 45 CFR Part 160, subparts C, D and E. OCR began accepting Part 2 complaints on 16 February 2026.

**§2.16 is the section that makes this a security question** rather than purely a consent question — it covers security for records and notification of breaches. This assessment cites the section by title and placement; a real engagement would read its operative text and test against it directly.

**Applicability is not assumed.** See `../TECHNICAL-DEEP-DIVE.md` for the full walkthrough.

---

## Framework coverage view

The same information, inverted — useful for answering "how do we look against NIST CSF 2.0?"

### By NIST CSF 2.0 function

| Function | Categories touched | Risks | Assessment |
|---|---|---|---|
| **GOVERN** | GV.OC, GV.RM, GV.RR, GV.PO, GV.SC | R-02, R-06, R-08, R-12 | **Weakest area.** No current risk analysis, no owner, no vendor oversight. Governance gaps are also the ones regulators cite. |
| **IDENTIFY** | ID.AM, ID.RA, ID.IM | R-02, R-05, R-12 | Weak. No asset inventory existed before this assessment; no lessons-learned loop. |
| **PROTECT** | PR.AA, PR.AT, PR.DS, PR.PS, PR.IR | R-01, R-03, R-04, R-05, R-06, R-07, R-08, R-10, R-11 | Broadest exposure by count, but also where the quick wins are. |
| **DETECT** | DE.CM, DE.AE | R-01, R-09 | Weak. Logs exist and are never read. |
| **RESPOND** | RS.MA | R-01 | Untested. Procedures exist on paper. |
| **RECOVER** | RC.RP | R-10 | Untested. Backups run, restores never attempted. |

Two categories carry no findings: **GV.OV** (oversight) and **RS.AN / RS.CO / RS.MI** (incident analysis, communication, mitigation). That is not because they are strong — it is because with no incident response exercise on record there was nothing to assess. Recorded as a scope limitation, not a pass.

### By HIPAA safeguard type

| Safeguard | Risks | Count |
|---|---|---|
| Administrative — §164.308 | R-01, R-02, R-05, R-06, R-08, R-09, R-10, R-11, R-12 | 9 |
| Physical — §164.310 | R-04, R-07 | 2 |
| Technical — §164.312 | R-01, R-03, R-04, R-05, R-06, R-09, R-11 | 7 |
| Organisational — §164.314 | R-12 | 1 |
| Documentation — §164.316 | R-02, R-06 | 2 |

Administrative safeguards dominate. That is typical and worth saying out loud to a clinic administrator: **most of what HIPAA requires is decisions, documentation and routines, not technology purchases.**

### By HITRUST control category

| HITRUST category | Risks |
|---|---|
| Information Security Management Program | R-02 |
| Access Control | R-01, R-03, R-06, R-08 |
| Human Resources Security | R-01, R-08 |
| Risk Management | R-02 |
| Organization of Information Security | R-12 |
| Compliance | R-06, R-12 |
| Asset Management | R-04, R-05 |
| Physical and Environmental Security | R-07 |
| Communications and Operations Management | R-04, R-05, R-09, R-11 |
| Information Security Incident Management | R-01, R-09 |
| Business Continuity Management | R-10 |
| Privacy Practices | R-06, R-11 |

Two of the 14 categories carry no findings — Security Policy and Information Systems Acquisition, Development and Maintenance. The second is genuinely low-relevance for a clinic that develops no software. The first is a gap in this assessment's scope, not a clean bill of health.

---

## One control, three frameworks

The practical payoff. Three examples of single pieces of work satisfying multiple obligations at once.

**Turn on multi-factor authentication** (R-01)
→ HIPAA §164.312(d) person or entity authentication, and supports §164.308(a)(5)(ii)(C) log-in monitoring and §164.308(a)(5)(ii)(D) password management
→ NIST CSF 2.0 PR.AA
→ HITRUST Access Control
→ *Also* pre-positions the clinic for the pending Security Rule proposal, which would make this mandatory.

**Issue unique named logins** (R-03)
→ HIPAA §164.312(a)(2)(i), a **Required** specification — no substitution available
→ NIST CSF 2.0 PR.AA
→ HITRUST Access Control
→ *Also* makes §164.308(a)(1)(ii)(D) information system activity review (R-09) possible at all. You cannot review activity meaningfully when three people share an account. **R-03 is a prerequisite for R-09, and the roadmap sequences them accordingly.**

**Build the vendor register** (R-12)
→ HIPAA §164.308(b)(1), §164.308(b)(3) **Required**, and §164.314(a)
→ NIST CSF 2.0 GV.SC and ID.AM
→ HITRUST Organization of Information Security, Compliance
→ *Also* produces the document OCR asks for first in almost every investigation.

---

## Where the frameworks don't map cleanly

Four genuine mismatches. A crosswalk where everything aligns neatly has usually been smoothed.

**1. HIPAA's addressable/required split has no equivalent anywhere else.**
NIST CSF 2.0 describes outcomes, not obligations — it has no concept of a control you may decline if you document why. HITRUST uses three progressive implementation levels driven by risk factors, which is a different mechanism again. So when this crosswalk says R-04 maps to NIST PR.DS, that mapping tells you *what capability is involved* but carries none of the legal weight. **Only the HIPAA column establishes what Northgate must do.** The other two columns are for communication and benchmarking.

**2. NIST CSF 2.0 GOVERN absorbed requirements that previously had no home.**
HIPAA's §164.308(a)(2) assigned security responsibility and §164.316(a) policies and procedures are core obligations that mapped awkwardly to CSF 1.1's five functions. Version 2.0's Govern function fixes this, and GV.SC in particular gives business associate oversight a proper destination. Any crosswalk built against CSF 1.1 will have forced these into Identify. Worth knowing if comparing against older documents.

**3. HITRUST maps to an older version of OCR's audit protocol than the one HHS publishes.**
HITRUST CSF v11.8.0 lists the **April 2016** OCR Audit Protocol among its authoritative sources. HHS currently publishes an **Audit Protocol updated July 2018**. The difference is unlikely to change any conclusion here, but a crosswalk that silently treats them as the same document is overstating its precision.

**4. 42 CFR Part 2 doesn't fit the model at all.**
It is not a security framework. It is a confidentiality statute with consent mechanics, redisclosure rules and litigation protections that have no counterpart in HIPAA, NIST or HITRUST. Its security requirements are a small part of it. Mapping it into the main table would have made it look like one more control family, which would misrepresent what it does — hence the separate overlay above.

---

## Sources and verification

Every citation in this document was checked against primary sources. Regulatory text was read on eCFR; framework structures were taken from the publishers' own documents.

**Regulation**
- 45 CFR §§164.306, 164.308, 164.310, 164.312, 164.316 — eCFR, Title 45 Subpart C
- 45 CFR §164.314(a) — cited at standard level only, as business associate contracts
- 42 CFR Part 2, §§2.1–2.68 — eCFR section titles and structure
- 45 CFR Part 160, subparts C, D, E — HIPAA Enforcement Rule, applied to Part 2

**Frameworks**
- NIST Cybersecurity Framework 2.0 — NIST CSWP 29, 26 February 2024. Six functions and 22 categories taken verbatim.
- HITRUST CSF v11.8.0 — *Introduction to the HITRUST CSF*, May 2026. 14 control categories, 49 control objectives, 156 control specifications; 75 authoritative sources.
- NIST SP 800-30 Rev. 1, September 2012 — assessment methodology.

**Rulemaking status**
- HIPAA Security Rule NPRM — issued by HHS 27 December 2024, published in the *Federal Register* 6 January 2025. Not finalised as of this assessment. HHS states the current Security Rule remains in effect during the rulemaking.
- 42 CFR Part 2 final rule — effective 16 April 2024, compliance required 16 February 2026.

**Deliberately not cited:** NIST CSF 2.0 subcategory identifiers, HITRUST control reference numbers, and the numeric bins in NIST SP 800-30's appendix scoring tables. Each would have strengthened the presentation; none was verified to the standard the rest of this document holds to.
