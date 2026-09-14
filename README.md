# Healthcare Security Risk Assessment
### Northgate Behavioral Health Clinic — a HIPAA Security Rule risk assessment

**Ron Richardson** · CompTIA Security+ · Per Scholas Cybersecurity

---

> **This is a portfolio project.** Northgate Behavioral Health Clinic is fictional. There is no real patient information, no real organisation, and no real security incident anywhere in this repository. Every regulatory citation is real and was verified against primary sources.

---

## What this is

A complete security risk assessment for a mid-size outpatient behavioral health clinic running EPIC Ambulatory and Cadence — the kind of engagement a healthcare GRC analyst would actually be handed.

It uses **NIST SP 800-30 Rev. 1** as the assessment methodology, frames every finding against the **HIPAA Security Rule**, and maps each one across to **NIST Cybersecurity Framework 2.0** and the **HITRUST CSF**.

**Written to be read by a clinic administrator, not just a security team.** Technical terms appear with their plain-English meaning alongside. The person who has to approve the budget should be able to follow the risk register without looking anything up.

---

## Start here, depending on who you are

| You are… | Read this |
|---|---|
| **Non-technical — clinic administrator, practice manager, hiring manager** | [`EXECUTIVE-OVERVIEW.md`](EXECUTIVE-OVERVIEW.md) — standalone, no jargon, no citations |
| **Skimming in five minutes** | [`01-risk-assessment/risk-register.md`](01-risk-assessment/risk-register.md) |
| **Assessing depth of regulatory knowledge** | [`02-framework-crosswalk/hipaa-hitech-hitrust-nist-mapping.md`](02-framework-crosswalk/hipaa-hitech-hitrust-nist-mapping.md) |
| **Technical — you want to probe the reasoning** | [`TECHNICAL-DEEP-DIVE.md`](TECHNICAL-DEEP-DIVE.md) |
| **A clinic administrator asking "what do I do Monday?"** | [`05-remediation/remediation-roadmap.md`](05-remediation/remediation-roadmap.md) |

---

## The findings, in one table

Twelve risks, scored Likelihood × Impact on a 1–5 scale.

| ID | Risk | Score | Rating |
|---|---|---|---|
| R-01 | Phishing compromise of a staff mailbox containing patient information | 20 | **Very High** |
| R-02 | Security risk analysis is not accurate, thorough, or current | 20 | **Very High** |
| R-03 | Shared and generic logins at the front desk and shared workstations | 16 | High |
| R-04 | Patient information unencrypted on laptops and removable media | 15 | High |
| R-05 | One flat network — cameras, HVAC, printers and guest Wi-Fi alongside clinical systems | 15 | High |
| R-06 | Substance use disorder record handling in EPIC not verified against applicable rules | 15 | High |
| R-07 | Front-of-house exposure — visible screens, shared sign-in, overheard conversations | 12 | High |
| R-08 | Access not removed promptly on departure or role change | 12 | High |
| R-09 | EPIC access logs not routinely reviewed | 12 | High |
| R-10 | Backups never tested by restoring from them | 12 | High |
| R-11 | Misdirected fax and loose release-of-information workflow | 9 | Moderate |
| R-12 | Incomplete inventory of vendors and business associate agreements | 9 | Moderate |

**Remediation: roughly $4,000–7,000 in year one.** For comparison, the public OCR settlement that most closely matches this clinic's highest risk was $103,000 plus two years of federally monitored corrective action.

---

## Repository contents

```
README.md                          You are here
EXECUTIVE-OVERVIEW.md              Standalone, non-technical
TECHNICAL-DEEP-DIVE.md             The reasoning behind the assessment

01-risk-assessment/
  asset-inventory.md               What the clinic has, where patient info lives, how it moves
  threat-vulnerability-matrix.md   Threat sources and events paired with the weaknesses
  risk-register.md                 12 scored risks with mitigations
  risk-heat-map.md                 Visual distribution, plus projected post-remediation

02-framework-crosswalk/
  hipaa-hitech-hitrust-nist-mapping.md   Every risk mapped to HIPAA, NIST CSF 2.0, HITRUST

03-vendor-risk/
  baa-vendor-risk-scorecard.md     14 vendors tiered; business associate status assessed
  iot-medical-device-risk-review.md  Connected devices, honestly scoped

04-breach-readiness/
  breach-notification-decision-tree.md   HIPAA vs FTC, the four-factor test, deadlines
  ocr-audit-prep-checklist.md            Built on a real 2026 enforcement settlement

05-remediation/
  remediation-roadmap.md           Four phases, owners, costs, expected risk movement
```

---

## Three things this project does deliberately

**1 · It treats 42 CFR Part 2 applicability as a question to analyse, not an assumption.**
Substance use disorder records carry federal confidentiality protections stricter than HIPAA. Most write-ups either ignore this or assert it applies. This assessment works through whether Northgate meets the definition, says what facts would settle it, and registers *the unresolved question* as the risk (R-06). The full walkthrough is in the deep dive.

**2 · It scopes connected-device risk honestly.**
The tempting move is to invoke FDA medical device cybersecurity guidance. But that guidance binds manufacturers, and an outpatient behavioral health clinic has almost no regulated devices. The real exposure is cameras, badge readers, HVAC, printers and guest Wi-Fi — ordinary building technology on the same network as clinical systems. The review is scoped to what Northgate would actually have.

**3 · It states what it could not verify.**
Several details that would have made the document look more authoritative were left out because they could not be confirmed against a primary source — NIST's appendix scoring tables, HITRUST control identifiers, NIST CSF subcategory IDs. Where the assessment made its own methodological choice, it says so. The scoring scale in the risk register is labelled as this assessment's scale, not as a NIST-sanctioned structure.

---

## On regulatory currency

Two things commonly get stated wrong, and this assessment gets both right:

**Encryption is *addressable*, not required.** Under the Security Rule as it stands, encryption of stored and transmitted patient information is an addressable implementation specification — meaning the clinic must assess it and either implement it or document why not and implement an equivalent alternative. A proposed rule published in the *Federal Register* on 6 January 2025 would make it mandatory, but has not been finalised, and HHS confirms the current rule remains in effect.

**Notice to HHS for large breaches is "contemporaneous with individual notice," not "within 60 days."** Plain-language summaries — including HHS's own — describe the deadline for breaches affecting 500 or more people as 60 days. The regulation at §164.408(b) says the notice must be contemporaneous with the individual notice required by §164.404(a), which is itself capped at 60 days from discovery. They usually land in the same place. They are not the same instruction.

---

## Methodology

**NIST SP 800-30 Rev. 1** (September 2012), the current revision. Its four steps structure the project:

| Step | Where it lives |
|---|---|
| 1 · Prepare for Assessment | `asset-inventory.md` |
| 2 · Conduct Assessment | `threat-vulnerability-matrix.md`, `risk-register.md`, `risk-heat-map.md` |
| 3 · Communicate Results | `remediation-roadmap.md`, `EXECUTIVE-OVERVIEW.md` |
| 4 · Maintain Assessment | `remediation-roadmap.md`, Phase 4 |

Scoring uses a 1–5 qualitative scale with the five levels NIST names — Very Low through Very High. The band cut-offs are this assessment's own, documented in the register and explained in the deep dive. NIST explicitly leaves break points to the assessing organisation and does not specify an algorithm for combining values.

---

## Primary sources

All regulatory text read on **eCFR**; framework structures taken from publishers' own documents.

- 45 CFR Part 164, Subpart C — HIPAA Security Rule
- 45 CFR §§164.400–414 — HIPAA Breach Notification Rule
- 45 CFR §160.310 — HIPAA Enforcement Rule, entity responsibilities
- 42 CFR Part 2 — Confidentiality of Substance Use Disorder Patient Records
- 16 CFR Part 318 — FTC Health Breach Notification Rule
- NIST CSWP 29 — Cybersecurity Framework 2.0 (February 2024)
- NIST SP 800-30 Rev. 1 — Guide for Conducting Risk Assessments
- *Introduction to the HITRUST CSF*, v11.8.0 (May 2026)
- HHS Office for Civil Rights — enforcement announcements, audit programme, breach notification guidance

---

## About the author

Ron Richardson — CompTIA Security+, Per Scholas cybersecurity cohort, with five years' prior clinical case management experience working in EPIC.

That clinical background shows up in the judgment calls rather than the credentials: which risks a real clinic actually faces, why the front desk carries disproportionate exposure, why a waiting-room sign-in sheet is a bigger problem in behavioral health than in primary care, and why a security control that is slower than the workaround will simply be worked around.

---

*Fictional scenario. Real regulations. Built as a demonstration of healthcare GRC capability.*
