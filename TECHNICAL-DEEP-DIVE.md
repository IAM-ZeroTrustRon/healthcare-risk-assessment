# Technical Deep Dive

**Northgate Behavioral Health Clinic** — Security Risk Assessment
The reasoning behind the assessment

**Ron Richardson** · CompTIA Security+ · Per Scholas Cybersecurity

---

> This document exists for the conversation that happens *after* someone reads the assessment. It covers the methodological choices, the judgment calls, the things that didn't make the register and why, and the places where the work has limits. If the deliverables are the *what*, this is the *why*.

---

## Contents

1. [Why NIST 800-30, and how scoring actually worked](#1)
2. [What made the register, and what didn't](#2)
3. [The 42 CFR Part 2 applicability analysis](#3)
4. [The IoT scoping call](#4)
5. [Crosswalk methodology, including the joins that don't work](#5)
6. [Limitations, assumptions, and what real access would change](#6)

---

<a name="1"></a>
## 1 · Why NIST 800-30, and how scoring actually worked

### Why this framework

Three alternatives were considered.

**ISO 27005** is a capable risk management standard, but it assumes an ISO 27001 information security management system as its context. Northgate has no ISMS and no realistic path to one. The assessment would have spent half its length establishing scaffolding the clinic will never build.

**FAIR** quantifies risk in dollars, which is genuinely superior for budget conversations. It also requires loss-magnitude and frequency data that a 45-person clinic does not have and cannot cheaply obtain. Applying FAIR here would have meant inventing inputs and presenting the output with a false precision — a number to two decimal places derived entirely from guesses.

**NIST SP 800-30 Rev. 1** won on three counts:

1. **Regulatory fit.** OCR's own guidance on the risk analysis requirement points at NIST methodology. An assessment built this way is legible to the regulator that would review it.
2. **Proportionality.** Its four steps — Prepare, Conduct, Communicate, Maintain — scale down to a small clinic without losing rigour. Step 4 in particular matters: the failure at Northgate was not a bad assessment, it was an assessment nobody revisited after the EPIC migration.
3. **Honest about its own limits.** 800-30 explicitly tells you it is not prescribing an algorithm. That made it possible to build a defensible scale without pretending to more authority than the document grants.

The one real trade-off: qualitative output. "R-01 scores 20" does not tell an administrator what 20 costs. That is mitigated in the roadmap by putting remediation cost next to a real public settlement figure — which does the budget-conversation job that a quantitative model would otherwise have done.

### How the scoring scale was built — and the thing I could not verify

**The scale used:** Likelihood 1–5 and Impact 1–5, multiplied for a 1–25 score, banded as Very High 17–25, High 10–16, Moderate 5–9, Low 3–4, Very Low 1–2.

**What's grounded in NIST:** The five qualitative levels — very low, low, moderate, high, very high — are stated in SP 800-30's body text as the standard qualitative vocabulary. The document also distinguishes three assessment approaches (quantitative, qualitative, semi-quantitative) and three analysis approaches (threat-oriented, asset/impact-oriented, vulnerability-oriented). This assessment is **qualitative** and **threat-oriented**.

**What is mine, not NIST's:** the numeric values 1–5, the multiplication, and the band cut-offs.

This distinction matters enough to be explicit about. SP 800-30's appendices contain assessment scales for each risk factor — Appendix G covers Likelihood of Occurrence, Appendix H covers Impact, Appendix I covers Risk Determination. **I could not extract those appendix tables from the source document during research.** The PDF text extraction truncated before the appendices.

There is a widely circulated version of those tables using semi-quantitative bins of 0–4, 5–20, 21–79, 80–95 and 96–100, with representative values of 0, 2, 5, 8 and 10. I have not confirmed that against the source. What I *did* confirm, verbatim from Chapter 2, is a different illustrative set — "bins (e.g., 0-15, 16-35, 36-70, 71-85, 86-100) or scales (e.g., 1-10)" — offered as examples of how semi-quantitative assessment works.

So I did not use either. I built a simple 5×5 scale, documented it in the risk register, and labelled it as this assessment's scale.

**Why this is the right call rather than a shortcoming.** SP 800-30 says organisations "typically define (or select and tailor from the appendices) the assessment scales to be used in their risk assessments... defining break points between bins for semi-quantitative approaches," and states plainly that "this guideline does not specify algorithms for combining semi-quantitative values." A defined, documented, transparent local scale is exactly what the methodology asks for. Reproducing a numeric table from memory and captioning it "per NIST SP 800-30 Appendix I" would have looked more authoritative and been less defensible — and it is precisely the kind of thing that falls apart when someone opens the PDF during an interview.

**What I would do differently with the document in hand:** tailor from Appendix G and H directly, which would let the clinic's scale line up with other NIST-based assessments it might be compared against.

### How individual scores were reasoned

Three worked examples, since the numbers are the part most worth interrogating.

**R-01, phishing — Likelihood 5, Impact 4.**
Likelihood 5 because phishing is continuous, untargeted and cheap, and the clinic has neither multi-factor authentication nor simulation training. Over twelve months the probability that no one clicks is not meaningfully above zero. Impact 4 rather than 5 because a single mailbox, while serious, is bounded — it would be 5 if that account could pivot into the EPIC environment. I deliberately did not score it 25; a register where the top risk maxes out both axes usually signals the assessor scored for emphasis rather than analysis.

**R-02, stale risk analysis — Likelihood 4, Impact 5.**
This one resists the framework slightly, because "likelihood" of a documentation gap is odd phrasing. I scored likelihood as the probability that the gap is *material within the year* — i.e. that something happens which the absent analysis would have caught, or that the clinic is examined. Impact 5 because this is independently citable regardless of whether anything else goes wrong, and because it is the most frequently cited finding in recent OCR enforcement. Noting the awkward fit is more useful than hiding it.

**R-04, encryption — Likelihood 3, Impact 5.**
The only risk in the register where the mitigation reduces *impact* rather than likelihood. Encrypting a laptop does not make it less likely to be stolen. It makes the theft not a reportable breach, because the breach rules apply to *unsecured* information. Likelihood 3 reflects normal device-loss rates for 14 mobile laptops over a year. Impact 5 reflects the full consequence chain of an unencrypted loss: individual notice, HHS report, possible media notice, permanent public entry on the federal breach portal.

That asymmetry is why R-04 sits in Phase 1 of the roadmap despite encryption being an addressable rather than required specification. Cost-to-consequence-avoided is the best ratio in the whole project.

---

<a name="2"></a>
## 2 · What made the register, and what didn't

### The inclusion test

Three questions. A candidate risk needed all three.

1. **Is there a plausible threat source and a matching weakness?** A threat with no corresponding weakness at this clinic is not a risk to this clinic.
2. **Would a mitigation change the score?** Risks with no available action are context, not register entries.
3. **Is it specific to Northgate?** "Ransomware" is a category, not a finding. R-05 and R-10 are what ransomware actually looks like here.

### Considered and excluded

**Nation-state and advanced persistent threat actors.** A 45-person outpatient clinic is not a plausible target. Including them would have raised scores across the board without changing a single recommended control. Excluded, and the exclusion is named in the threat matrix — an assessment that lists every threat source is not demonstrating thoroughness, it is failing to prioritise.

**Insider data theft for financial gain.** Real in healthcare, but the specific behavioral health risk is *curiosity*, not monetisation — staff looking up neighbours, family, former patients in a small community where social circles overlap. That is R-09. Folding both into one entry would have blunted the mitigation, since detecting curiosity-driven access requires different log review than detecting bulk exfiltration.

**Physical intrusion and break-in.** Assessed and scored below the inclusion threshold. The clinic has badge access, the records are primarily electronic and vendor-hosted, and the realistic physical exposure is *observation* rather than intrusion — which is R-07.

**Workforce security awareness training as a standalone entry.** This was the closest call. Training is a Security Rule standard at §164.308(a)(5)(i) and Northgate's is generic and annual. I folded it into R-01's mitigation and gave it its own roadmap line instead.

*The reasoning:* training is not a risk, it is a control. Registering "we have insufficient training" as a risk confuses the two, and produces the common failure mode where training becomes the answer to everything. Every organisation with a breach had training. What Northgate specifically lacks is *role-specific* training and *phishing simulation*, both of which attach naturally to R-01, which is the risk they actually reduce. Reasonable assessors would disagree with this call, which is why it is stated rather than silent.

**Business continuity beyond data recovery.** Pandemic planning, alternate site operations, staffing continuity. Real concerns, genuinely outside the scope of a security risk assessment framed against the Security Rule. Scope boundaries are worth defending.

**Medical device vulnerabilities as a distinct register entry.** Covered in section 4.

### The two that nearly didn't make it

**R-07, front-of-house exposure**, because nothing technical is broken. A reception monitor facing the waiting room is a workflow and furniture problem. It scored 12 and stayed in because of the sensitivity inversion described in section 3 — in behavioral health, the fact of being a patient is frequently the sensitive fact, and a shared sign-in sheet discloses exactly that. This is the risk I would expect an assessor without clinical floor experience to miss entirely, because it doesn't look like a security finding.

**R-11, misdirected fax**, because fax feels anachronistic. It stayed in because behavioral health referrals and records requests still move by fax constantly, and misdirection remains one of the most common ways small clinics disclose information they shouldn't. Scored 9 rather than higher because volume is moderate and each event is small.

---

<a name="3"></a>
## 3 · The 42 CFR Part 2 applicability analysis

The strongest reasoning artifact in the project, and the one I would most want to be asked about.

### Why this is a question at all

Records of substance use disorder treatment can carry federal confidentiality protections separate from and stricter than HIPAA, under 42 U.S.C. 290dd-2 and 42 CFR Part 2. Broadly: the information generally cannot be disclosed without the patient's written consent, and cannot be used against the patient in legal proceedings without a court order.

Most portfolio assessments of behavioral health clinics do one of two things. They ignore Part 2 entirely, or they assert it applies because the clinic is behavioral health. **Both are wrong, and the second is wrong in a way that looks competent** — which makes it the more dangerous error.

Behavioral health is not the same as substance use disorder treatment. Many outpatient mental health clinics are not Part 2 programmes. Some are. The difference turns on facts.

### The test

Part 2 reaches **federally assisted programmes that provide substance use disorder diagnosis, treatment, or referral for treatment.** Two limbs, both required.

**Limb one — federally assisted.** Almost certainly satisfied. The term is construed broadly and reaches well beyond direct federal grants — Medicaid participation and DEA registration to prescribe controlled substances are among the routes. Northgate accepts Medicaid and its prescribers hold DEA registrations for medication management. Assume this limb is met.

**Limb two — provides SUD diagnosis, treatment, or referral.** This is where it turns, and the answer depends on facts this assessment does not have:

- Does Northgate **hold itself out** as providing substance use disorder services — in marketing, intake forms, service listings, payer contracts, licensure?
- Does it have staff **whose function is** SUD diagnosis or treatment?
- Does it run a **medication-assisted treatment programme**? The point-of-care drug screening analyser in the asset inventory is a meaningful signal.
- Does it **bill for SUD-specific services**, or only for mental health services to patients who happen to also have a substance use disorder?
- Does it **refer** patients to SUD treatment as a defined service, rather than incidentally?

The distinction that matters: **a clinic treating depression in a patient who also drinks heavily is not thereby a Part 2 programme. A clinic that identifies, diagnoses, treats or formally refers substance use disorder probably is.** Co-occurring conditions are ubiquitous in behavioral health, which is exactly why the incidental-versus-held-out distinction does the work.

### What changes depending on the answer

**If Part 2 does not apply:** HIPAA alone governs. R-06 closes on the strength of the written determination. Nothing else in the assessment moves.

**If Part 2 does apply, quite a lot changes:**

| Area | What changes |
|---|---|
| **Consent** | Most disclosures need written patient consent meeting §2.31, not HIPAA's treatment/payment/operations permissions. The 2024 rule allows a single consent covering all future TPO uses — which is a substantial relaxation, but it is still a consent regime. |
| **EPIC configuration** | Part 2 records need segregation and consent management inside the EHR. This is the hard technical problem, and it is a vendor conversation, not a clinic one. |
| **Notice** | §2.22 requires a patient notice. A clinic that is both a Part 2 programme and a HIPAA covered entity may issue a combined notice satisfying both. |
| **Breach notification** | §2.16 covers security for records and notification of breaches. The incident procedure has to cover both rule sets together. |
| **Release of information** | R-11's fax workflow becomes materially higher risk — a misdirected Part 2 record carries consent and notice failures on top of the disclosure. |
| **Litigation** | Part 2 records cannot be used in proceedings against the patient without consent or a court order and subpoena. This constrains how the clinic responds to legal process. |
| **Intermediaries** | §2.24 applies if the clinic participates in a health information exchange. |
| **Enforcement** | Same regulator. OCR was delegated Part 2 administration and enforcement on 25 August 2025, applying the HIPAA Enforcement Rule at 45 CFR Part 160 subparts C, D and E. One incident, one regulator, two rule sets. |

### Why the register entry is the *question*, not the answer

R-06 registers the unresolved applicability determination, not a confirmed violation. That is the accurate finding. The clinic does not know whether a federal rule applies to it — and that rule's compliance date passed on **16 February 2026**, with OCR accepting complaints from the same date.

The risk being carried is real and current, and it resolves with a written determination that costs a day of someone's time. That is why the mitigation is "answer the question in writing within 30 days" rather than "implement Part 2 controls."

### The limit of this analysis

I verified Part 2's structure, status, enforcement delegation and compliance date against HHS and eCFR, and I have the section map verbatim. **I did not read the operative text of §2.11 (Definitions) or §2.12 (Applicability).** The two-limb test above comes from HHS's plain-language description of the rule's scope, which is authoritative-adjacent but is a summary.

A real engagement reads §2.11 and §2.12 directly before issuing the determination. The framework of the analysis holds; the precise definitional boundaries should be confirmed at the source. Stated here rather than buried, because an interviewer who knows Part 2 will ask, and "I worked from the HHS summary and flagged that the regulation text should be read" is a much better answer than a confident assertion that turns out to be paraphrased.

---

<a name="4"></a>
## 4 · The IoT scoping call

### The tempting version

There is an obvious, impressive-looking version of this section. It cites FDA's premarket cybersecurity guidance, invokes section 524B of the Federal Food, Drug, and Cosmetic Act, discusses software bills of materials and coordinated vulnerability disclosure, and produces a medical device security programme.

It would have been wrong in two distinct ways.

### Error one: the obligations run to manufacturers

Section 524B and FDA's premarket guidance govern what **device makers** must submit when seeking market authorisation — a plan to monitor and address postmarket vulnerabilities, processes providing reasonable assurance the device is cybersecure, availability of updates and patches, and a software bill of materials.

**A clinic cannot be non-compliant with section 524B.** It has no submissions to make.

What a clinic *can* do is make those artifacts a purchasing condition — require the SBOM, require a patch commitment, require an end-of-support date before signing. That is a procurement control, and it is where the pre-network-admission checklist puts it.

Framing a provider organisation as subject to manufacturer obligations is a category error that reads as competent to a general audience and as a tell to anyone who works in the space. The audience for this portfolio includes the second group.

### Error two: the device population doesn't support it

An outpatient behavioral health clinic has no imaging suite, no infusion pumps, no monitored beds. Northgate has two vitals stations and possibly one point-of-care drug screening analyser — and all three may be standalone rather than networked.

Meanwhile it has eight cameras, a badge controller, an HVAC controller, three smart TVs, four multifunction printers and six guest Wi-Fi access points. **Two of eight device groups are plausibly FDA-regulated. Six are not.**

Building the section around the two would have meant writing at length about the smaller exposure while mentioning the larger one in passing.

### What replaced it

The review scoped to **connected devices generally**, with the finding that all of them share one flat network with clinical workstations (R-05). Recommendation: four-zone segmentation — clinical, staff general, building and facilities, guest.

Four zones, not twelve, and that is a deliberate constraint. Four is achievable with VLANs and firewall rules on hardware a clinic this size already owns, without new capital or a network engineer. A twelve-zone design would be better on paper and would not get built. **The right security architecture for this clinic is the one that actually gets implemented.**

The pre-network-admission checklist covers all devices, medical or not, and asks the medical-device questions only where they apply — including a request for a completed MDS2 form, the voluntary industry disclosure standard (ANSI/NEMA HN 1-2019), described accurately as manufacturer-self-reported and not a certification.

One finding survived from the medical-device framing in modified form: multifunction printers store documents on internal drives that leave the building at lease end, which engages §164.310(d)(2)(i) disposal and §164.310(d)(2)(ii) media re-use — both **Required** specifications. That is a real regulated obligation about a device nobody thinks of as a device.

### The general principle

Scope to the risk, not to the citations available. The version of this section with more regulatory references would have been a worse piece of security advice. Being able to explain *why* a body of guidance was set aside demonstrates more than being able to cite it.

---

<a name="5"></a>
## 5 · Crosswalk methodology, including the joins that don't work

### How the mapping was built

Bottom-up, from the risks, not top-down from the frameworks.

The alternative — walk the 22 NIST CSF categories, walk the 14 HITRUST categories, walk the HIPAA safeguards, then look for findings — produces comprehensive-looking coverage tables and a register full of entries that exist because a framework has a row for them. Starting from risks means every crosswalk entry traces to something actually observed.

The cost: uneven framework coverage. Two NIST CSF categories and two HITRUST categories carry no findings. Rather than manufacture findings to fill them, the crosswalk says so and distinguishes *genuinely low relevance* (HITRUST's systems acquisition and development category, for a clinic that writes no software) from *a gap in this assessment's scope* (NIST's incident analysis and communication categories, unassessed because there was no incident response exercise to assess).

### One control, three frameworks

The practical payoff. Enabling multi-factor authentication satisfies HIPAA §164.312(d), NIST CSF PR.AA and HITRUST Access Control simultaneously — one action, three answers, three audiences. The crosswalk exists so the clinic does the work once and reports it three ways.

There is also a dependency the crosswalk surfaced that the register alone did not: **R-03 is a prerequisite for R-09.** Reviewing information system activity under §164.308(a)(1)(ii)(D) is meaningless while three people share a front-desk login, because the logs cannot attribute action to person. Both map to the same HITRUST and NIST territory, which is what made the dependency visible. The roadmap sequences them accordingly — unique logins in Phase 2 before monthly review begins.

### The four joins that don't work

A crosswalk where everything aligns has usually been smoothed. Four genuine mismatches:

**1 · HIPAA's required/addressable distinction has no equivalent anywhere else.**
NIST CSF 2.0 describes outcomes, not obligations, and has no concept of a control you may decline provided you document why. HITRUST uses three progressive implementation levels driven by organisational, compliance and system risk factors — a different mechanism again.

The consequence: when the crosswalk maps R-04 to NIST PR.DS, that tells you what capability is involved and carries no legal weight whatever. **Only the HIPAA column establishes what Northgate must do.** The other two columns are for communication and benchmarking. A crosswalk that presents three columns as equivalent obligations misleads, and this one says so explicitly.

**2 · NIST CSF 2.0's GOVERN function absorbed requirements that previously had nowhere to go.**
HIPAA §164.308(a)(2) assigned security responsibility and §164.316(a) policies and procedures are core obligations that mapped awkwardly onto CSF 1.1's five functions — they usually got forced into Identify. Version 2.0's Govern function gives them a proper home, and GV.SC specifically gives business associate oversight somewhere to live.

This means any crosswalk built against CSF 1.1 will disagree with this one on placement, without either being wrong. Worth knowing when comparing against older documents.

**3 · HITRUST maps to an older OCR audit protocol than HHS publishes.**
HITRUST CSF v11.8.0 lists the **April 2016** OCR Audit Protocol among its 75 authoritative sources. HHS currently publishes an **Audit Protocol updated July 2018**. The difference almost certainly changes nothing here. Treating them as the same document would overstate the crosswalk's precision, so it is footnoted.

**4 · 42 CFR Part 2 doesn't fit the model at all.**
It is not a security framework. It is a confidentiality statute with consent mechanics, redisclosure rules and litigation protections that have no counterpart in HIPAA, NIST or HITRUST. Its security content is a small fraction of it.

Mapping it into the main table would have made it look like one more control family. It is carried as a separate overlay attached only to R-06, which represents accurately what it is.

### The HITRUST licensing constraint

HITRUST control references and requirement statements are proprietary licensed content. The crosswalk uses **control category names only** — "Access Control," "Business Continuity Management" — and does not reproduce or invent control identifiers.

Fabricating plausible-looking IDs for a public repository would be both a licensing problem and trivially catchable by anyone with a licensed copy. A commercial engagement would map to specific references from a licensed CSF. Category-level mapping is the honest ceiling for public portfolio work, and saying so is better than hoping nobody checks.

### What was deliberately not cited

Three things that would have strengthened the presentation and were left out because they could not be verified to the standard the rest of the document holds:

- **NIST CSF 2.0 subcategory identifiers.** The 22 category IDs were extracted verbatim from CSWP 29. Subcategory IDs were not, so the crosswalk stops at category level.
- **HITRUST control reference numbers.** Licensing, per above.
- **NIST SP 800-30 appendix scoring bins.** Per section 1.

---

<a name="6"></a>
## 6 · Limitations, assumptions, and what real access would change

### What a fictional scenario forced

**The asset inventory is constructed, not discovered.** The device counts, staff numbers and system list reflect what a clinic of this size and age typically has. A real engagement starts with a network scan, an EPIC user export and a walkthrough. Every number in the inventory would change.

**Likelihood scores rest on general patterns, not this clinic's history.** No incident history, no help desk tickets, no prior audit findings. In a real engagement, three years of incident logs would move several scores — probably R-09 up and R-11 down.

**No control testing was performed.** This is a risk assessment, not a penetration test or a control audit. Findings state that a control is absent or undocumented, never that a present control was tested and failed. The distinction is worth defending: "backups are never restore-tested" is a finding; "backups would fail" would be an unsupported claim.

**The Part 2 determination could not be made** — see section 3. That is a data limitation, not an analytical one, and the register reflects it accurately.

### Assumptions, stated so they can be challenged

1. EPIC is vendor-hosted, so exposure concentrates at access, endpoint and vendor-management layers rather than the server layer.
2. All 45 workforce members have email; not all have EPIC.
3. No on-premises domain controller or self-hosted clinical server.
4. The satellite site connects over a site-to-site VPN.
5. The clinic accepts Medicaid and its prescribers hold DEA registrations — which is what makes the "federally assisted" limb of the Part 2 test almost certainly satisfied.
6. Vitals stations and the drug screening analyser may or may not be networked. This is unresolved and determines whether any FDA-regulated device is in scope at all.

Assumption 6 is the one most likely to be wrong in a way that matters.

### What I would request with real access

**Week one**
- Network scan — a real device inventory, which settles assumption 6 in an afternoon
- EPIC user access export, with role and last-login, reconciled against the HR roster
- Existing policies, prior risk assessments, and the current business associate agreement file
- Three years of incident and help desk history
- The EPIC contract and hosting agreement, for the shared-responsibility boundary

**Week two**
- Front desk observation across a full shift. Not an interview — observation. The gap between documented workflow and actual workflow is where R-03 and R-07 live, and nobody describes their own workarounds accurately.
- Walkthroughs of both sites, including the satellite
- Interviews with intake, billing and a per-diem clinician — the per-diem especially, because their access lifecycle is what R-08 is about
- The clinical director on Part 2 applicability and on how substance use disorder information is actually documented in EPIC today

**Week three**
- A restore test, observed
- EPIC audit log extract, to establish whether inappropriate access is already occurring
- Vendor remote-access inventory
- Firewall and switch configuration review

### What a real engagement would add

**Control testing.** Move from "encryption is absent" to "encryption is enabled on 11 of 14 laptops, and the three exceptions are the satellite site machines."

**Quantified impact.** With real patient volumes and payer mix, per-record notification cost and downtime cost become calculable, and the roadmap's business case stops resting on an external settlement figure.

**Evidence of current compromise.** A risk assessment is forward-looking. A clinic in Northgate's position — no log review, no multi-factor authentication, flat network — should assume something may already have happened and look.

**State law analysis.** This assessment is federal-scope only. Behavioral health records carry additional state protections almost everywhere, and 42 CFR §2.20 governs the Part 2/state-law relationship. In a real engagement, state law would be its own section.

**Penetration testing.** Particularly of the flat network hypothesis in R-05. The claim that a compromised camera can reach clinical workstations is architecturally sound and untested.

### What I would do differently next time

**Get the 800-30 appendices.** The single clearest gap. Tailoring from the actual Appendix G and H scales rather than defining a local one would make the scoring comparable to other NIST-based assessments.

**Build the register from a data-flow diagram rather than an asset list.** The strongest findings — R-01, R-07, R-11 — all came from thinking about how information *moves*, not what it sits on. Asset inventories find storage; flow analysis finds exposure.

**Include at least one risk the clinic should accept.** Every entry in this register has a recommended mitigation, which implicitly says everything is worth fixing. A register with a documented accepted risk — this is real, here is why we are living with it, here is who decided — is more mature. Northgate's register doesn't have one, and it should.

---

## Why the honest limitations are here

A portfolio project can present as flawless because nobody can check a fictional clinic. That is exactly what makes stated limitations worth something: they are the only part of a fictional assessment that couldn't have been faked into looking better.

The three things this document admits to — an unverified scoring appendix, a Part 2 analysis built on a summary rather than regulation text, and a constructed asset inventory — are each places where the easy move was available and not taken.

---

*Fictional scenario. Real regulations. All citations verified against primary sources; everything unverified is named as such.*
