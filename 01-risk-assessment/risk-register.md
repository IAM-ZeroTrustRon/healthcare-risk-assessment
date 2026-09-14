# Risk Register

**Northgate Behavioral Health Clinic** — Security Risk Assessment
Methodology: NIST SP 800-30 Rev. 1 · Framed against the HIPAA Security Rule (45 CFR Part 164, Subpart C)

> **This is a fictional clinic.** No real patient information, no real organizations, no real incidents. Built as a portfolio demonstration.

---

## How to read this register

Every risk below has three numbers and a sentence.

- **Likelihood** — how plausible is it that this actually happens here, in the next year?
- **Impact** — if it happens, how bad is it for patients, for the clinic's licence and finances, and for the ability to keep seeing people?
- **Risk score** — Likelihood multiplied by Impact. Higher means deal with it sooner.
- **Mitigation** — the single most useful thing to do about it.

Both scales run 1 to 5, using the wording NIST uses: Very Low, Low, Moderate, High, Very High.

| Score | Rating | What it means in practice |
|---|---|---|
| 17–25 | **Very High** | Fix now. This is the kind of gap that shows up in enforcement actions. |
| 10–16 | **High** | Fix this year, with a named owner and a date. |
| 5–9 | **Moderate** | Plan it. Doesn't need to jump the queue, does need to be on the list. |
| 3–4 | **Low** | Accept and revisit at the next annual assessment. |
| 1–2 | **Very Low** | Accept. |

A note on honesty: the 1–5 scale and the band cut-offs above are **this assessment's scale**, chosen and documented here. NIST SP 800-30 describes qualitative scales using exactly these five words, and explicitly says organisations should define their own break points — it does not hand you a scoring formula. See `TECHNICAL-DEEP-DIVE.md` for the full reasoning.

---

## The register

| ID | Risk | Likelihood | Impact | Score | Rating |
|---|---|---|---|---|---|
| **R-01** | Phishing compromise of a staff mailbox containing patient information | 5 | 4 | **20** | Very High |
| **R-02** | The clinic's security risk analysis is not accurate, thorough, or current | 4 | 5 | **20** | Very High |
| **R-03** | Shared and generic logins at the front desk and on shared clinical workstations | 4 | 4 | **16** | High |
| **R-04** | Patient information stored unencrypted on laptops and removable media | 3 | 5 | **15** | High |
| **R-05** | One flat network — cameras, thermostats, printers and guest Wi-Fi sit alongside clinical systems | 3 | 5 | **15** | High |
| **R-06** | Substance use disorder record handling in EPIC has not been verified against the confidentiality rules that may apply | 3 | 5 | **15** | High |
| **R-07** | Front-of-house exposure — visible screens, shared sign-in, overheard conversations | 4 | 3 | **12** | High |
| **R-08** | Access is not removed promptly when someone leaves or changes role | 4 | 3 | **12** | High |
| **R-09** | EPIC access logs and system activity are not routinely reviewed | 4 | 3 | **12** | High |
| **R-10** | Backups have never been tested by actually restoring from them | 3 | 4 | **12** | High |
| **R-11** | Misdirected fax and loose release-of-information workflow | 3 | 3 | **9** | Moderate |
| **R-12** | Incomplete inventory of vendors and business associate agreements | 3 | 3 | **9** | Moderate |

**Summary:** 2 Very High · 8 High · 2 Moderate · 0 Low

---

## The detail

### R-01 · Phishing compromise of a staff mailbox containing patient information
**Likelihood 5 (Very High) × Impact 4 (High) = 20 · Very High**

Clinical and administrative staff email each other about patients constantly — referral questions, "can we fit this person in Thursday," insurance authorisation chases. That means mailboxes accumulate patient information even where nobody intended them to be a record system. A single successful phishing email against one staff account exposes everything in that mailbox and everything that account can reach.

This is not hypothetical for behavioral health. In February 2026 the HHS Office for Civil Rights settled with a substance use disorder treatment provider after exactly this sequence — a phishing attack, a compromised workforce member's email account, roughly two thousand patients affected.

**Why likelihood is Very High:** phishing attempts are continuous and universal. Over a year, at a clinic with no simulation programme and no multi-factor authentication, the question is not whether someone clicks.

**Why impact is High rather than Very High:** a single mailbox is serious but bounded. It becomes Very High if that account can reach the EPIC environment or a shared drive.

**Mitigation:** Turn on multi-factor authentication for all email and remote access, and run quarterly phishing simulations with short, role-specific follow-up training.

---

### R-02 · The clinic's security risk analysis is not accurate, thorough, or current
**Likelihood 4 (High) × Impact 5 (Very High) = 20 · Very High**

The clinic has a risk assessment on file, but it predates the EPIC migration, does not cover the telehealth platform, and no one has revisited it since. Under the Security Rule, a risk analysis is not a document you produce once — it is a required, recurring activity, and the results have to drive actual decisions.

This matters more than it sounds. Failure to conduct an accurate and thorough risk analysis is the most frequently cited finding in recent OCR enforcement, and OCR is running an explicit enforcement initiative focused on this one requirement. In the behavioral health settlement referenced under R-01, inadequate risk analysis was the **only** finding OCR made.

**Why impact is Very High:** this is the finding that converts an incident into an enforcement action. It also means every other risk on this register is, by definition, unmanaged.

**Mitigation:** Adopt this assessment as the current risk analysis, assign an owner, and commit in writing to refreshing it annually and after any material system change.

---

### R-03 · Shared and generic logins at the front desk and on shared clinical workstations
**Likelihood 4 (High) × Impact 4 (High) = 16 · High**

Front desk is a queue. Three people rotate through two workstations across a shift, patients are waiting, and the path of least resistance is a shared "frontdesk" login that nobody logs out of. The same pattern shows up on the shared workstation in the group therapy room and on the vitals station.

The cost is not just that the wrong person can see things. It is that **you lose the ability to answer the question "who did this?"** — which is the question every breach investigation, every patient complaint, and every OCR data request begins with.

Assigning each person their own login is one of the small number of things the Security Rule requires outright, with no flexibility to substitute something else.

**Mitigation:** Issue unique named accounts to every workforce member, disable shared accounts, and pair this with badge-tap or short screen-lock timeouts so it doesn't slow the front desk down.

---

### R-04 · Patient information stored unencrypted on laptops and removable media
**Likelihood 3 (Moderate) × Impact 5 (Very High) = 15 · High**

Clinicians take laptops to satellite sessions and home for documentation. Reports get exported to USB drives for the billing vendor. None of it is encrypted.

Encryption is worth understanding precisely here, because it is widely misdescribed. Under the Security Rule as it stands today, encryption is **addressable**, not required. Addressable does *not* mean optional. It means the clinic must assess whether encryption is reasonable and appropriate, and then either implement it, or document why it isn't and implement an equivalent alternative. For a clinic that can enable full-disk encryption at no licence cost on hardware it already owns, "not reasonable and appropriate" is not a defensible position.

There is a second reason encryption matters disproportionately: encrypted information that is lost or stolen generally does not trigger breach notification at all, because the breach rules apply to *unsecured* information. Encryption is the single control with the best ratio of effort to consequence-avoided.

**Mitigation:** Enable full-disk encryption on every clinic laptop and require encrypted removable media, and record the decision in writing so the addressable-specification analysis is documented.

---

### R-05 · One flat network — cameras, thermostats, printers and guest Wi-Fi sit alongside clinical systems
**Likelihood 3 (Moderate) × Impact 5 (Very High) = 15 · High**

The clinic runs a single network. The waiting room camera, the door badge controller, the HVAC unit, the multifunction printer, the smart TV in the group room and the patient guest Wi-Fi all share the same space as the workstations that reach EPIC.

Every one of those devices is a small computer that someone else patches, or doesn't. A compromised camera is not interesting in itself; a compromised camera with an unobstructed path to clinical workstations is how a ransomware incident starts.

**Why likelihood is only Moderate:** it takes an attacker getting a foothold first. **Why impact is Very High:** the whole point of a flat network is that there is nothing to stop the spread, and an outpatient clinic that loses its schedule and its charts stops seeing patients that day.

**Mitigation:** Separate the network into at least four zones — clinical, staff general, building and facilities devices, and guest — with guest Wi-Fi fully isolated from everything else.

---

### R-06 · Substance use disorder record handling in EPIC has not been verified
**Likelihood 3 (Moderate) × Impact 5 (Very High) = 15 · High**

Records of substance use disorder treatment can carry confidentiality protections that go beyond HIPAA, under a separate federal rule usually called Part 2. Those protections are stricter — broadly, the information generally cannot be shared without the patient's written consent, and it cannot be used against the patient in legal proceedings.

**This assessment does not assume Part 2 applies to Northgate.** Whether it does is a genuine analytical question, and it is worked through properly in `TECHNICAL-DEEP-DIVE.md`. The short version: the rule reaches federally assisted programmes that provide substance use disorder diagnosis, treatment, or referral for treatment. Northgate almost certainly meets the "federally assisted" half through Medicaid participation. Whether it meets the second half depends on facts this assessment does not have — specifically whether the clinic holds itself out as providing substance use disorder services, or treats co-occurring substance use only incidentally to mental health care.

The risk being registered here is **the unresolved question itself**, not a confirmed violation. If Part 2 applies and EPIC has not been configured to segregate those records and manage consent, the clinic is out of compliance with a rule whose compliance date passed in February 2026 — and the agency that enforces it now also enforces HIPAA.

**Mitigation:** Answer the applicability question in writing within 30 days, and if the rule applies, verify EPIC's record-segmentation and consent configuration against it.

---

### R-07 · Front-of-house exposure — visible screens, shared sign-in, overheard conversations
**Likelihood 4 (High) × Impact 3 (Moderate) = 12 · High**

The reception monitor faces the waiting room. There is a paper sign-in sheet where each person can read the names above theirs. Scheduling calls happen at the desk, three feet from seated patients.

In most medical settings this is a moderate privacy problem. **In behavioral health it is the whole problem.** The sensitive fact is frequently not the diagnosis or the treatment plan — it is simply *that this person is a patient here at all*. A waiting room where patients can see each other's names, or overhear "and that's for the Suboxone follow-up," discloses exactly the thing people most want protected. That is also the reason people quietly stop coming.

This is the risk most likely to be underweighted by an assessor without clinical floor experience, because nothing technical is broken.

**Mitigation:** Fit privacy filters and reposition the reception monitors, replace the paper sign-in sheet with individual slips or a tablet, and move scheduling calls out of earshot of the waiting area.

---

### R-08 · Access is not removed promptly when someone leaves or changes role
**Likelihood 4 (High) × Impact 3 (Moderate) = 12 · High**

There is no single checklist that ties a departure to EPIC deactivation, email disablement, badge collection, VPN removal and the telehealth platform. Behavioral health runs on per-diem clinicians, interns on rotation and contracted prescribers — people whose end dates are fuzzy and whose accounts simply linger.

The same gap applies to role changes, which are easier to miss than departures: someone moves from intake to billing and accumulates both sets of access rather than trading one for the other.

**Mitigation:** Build a one-page joiner/mover/leaver checklist covering every system, make HR the trigger, and reconcile active accounts against the current staff roster quarterly.

---

### R-09 · EPIC access logs and system activity are not routinely reviewed
**Likelihood 4 (High) × Impact 3 (Moderate) = 12 · High**

EPIC produces detailed access logs. Nobody at Northgate looks at them unless there is a complaint.

Reviewing system activity is one of the required elements of the Security Rule — not something to be traded away. The practical consequence of not doing it is that inappropriate access is found only when a patient notices and asks, which in a small community clinic where staff and patients know each other is a real and recurring scenario.

**Mitigation:** Run a monthly EPIC access review covering same-surname matches, staff-as-patient records, and high-volume accesses, and keep a dated record that the review happened.

---

### R-10 · Backups have never been tested by actually restoring from them
**Likelihood 3 (Moderate) × Impact 4 (High) = 12 · High**

Backups run nightly and report success. No one has ever restored from them.

A backup that has not been restored is a belief, not a control. The Security Rule requires a data backup plan, a disaster recovery plan and an emergency mode operation plan — all three outright — and treats testing and revision as an addressable specification the clinic must consciously decide about.

**Mitigation:** Perform a documented full restore test to an isolated environment, and repeat it annually with the result written down.

---

### R-11 · Misdirected fax and loose release-of-information workflow
**Likelihood 3 (Moderate) × Impact 3 (Moderate) = 9 · Moderate**

Referrals, prior authorisations and records requests still move by fax. Numbers are typed manually or pulled from an outdated speed-dial list. Nobody confirms what was actually sent, or to whom.

Misdirected fax is unglamorous and remains one of the more common ways small clinics disclose information they shouldn't. Where Part 2 applies, the consent and notice requirements attached to a release make an error meaningfully worse than a HIPAA-only misfire.

**Mitigation:** Move to a verified recipient directory with a second-person check for anything outside it, and log every outbound release with the authority it was sent under.

---

### R-12 · Incomplete inventory of vendors and business associate agreements
**Likelihood 3 (Moderate) × Impact 3 (Moderate) = 9 · Moderate**

The clinic has agreements with its EPIC hosting partner and its billing company. It does not have a complete list of everyone else who touches patient information — the transcription service, the answering service, the shredding vendor, the IT support company, the telehealth platform — and cannot currently say which of them have signed agreements.

The Security Rule requires the clinic to obtain written satisfactory assurances before letting a vendor handle patient information. You cannot produce those agreements on demand if you don't know who the vendors are.

**Mitigation:** Build a single vendor register recording what each vendor touches, whether an agreement is signed and when it was last reviewed — see `03-vendor-risk/baa-vendor-risk-scorecard.md`.

---

## What comes next

- Where each risk sits visually: `risk-heat-map.md`
- What each risk maps to in HIPAA, HITRUST and NIST: `../02-framework-crosswalk/hipaa-hitech-hitrust-nist-mapping.md`
- What to do and in what order: `../05-remediation/remediation-roadmap.md`
