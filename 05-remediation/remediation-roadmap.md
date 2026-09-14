# Remediation Roadmap

**Northgate Behavioral Health Clinic** — Security Risk Assessment
NIST SP 800-30 Rev. 1, Step 3: Communicate Results · Step 4: Maintain Assessment

> Fictional clinic. Cost and effort figures are planning estimates for a clinic of this size, not quotes.

---

## What this is

A risk assessment that ends at a list of problems is half a deliverable. This is the other half: what to do, in what order, who owns it, and what it costs.

It is also the document that satisfies **§164.308(a)(1)(ii)(B) risk management** — a **Required** implementation specification distinct from the risk analysis itself. The Security Rule asks for both: find the risks, then implement measures sufficient to reduce them to a reasonable and appropriate level. A clinic with an assessment and no plan has done half of a required thing.

**Sequencing logic.** Three principles drove the order:

1. **Regulatory exposure first.** R-02 is the most-cited finding in recent enforcement and closing it takes a signature, not a budget.
2. **Prerequisites before dependents.** Unique logins (R-03) must land before log review (R-09) can mean anything.
3. **Impact reduction beats likelihood reduction where it's cheap.** Encryption reduces the *consequence* of an incident rather than its probability, and it does so sharply — which is why R-04 sits in Phase 1 despite being addressable rather than required.

---

## Phase 1 — Days 0 to 30 · Close the regulatory gaps

Low cost, high effect. Mostly decisions and documentation.

| # | Action | Risk | Owner | Effort | Cost |
|---|---|---|---|---|---|
| 1.1 | **Adopt this assessment as the clinic's current risk analysis.** Date it, sign it, file it. | R-02 | Practice administrator | 2 hrs | — |
| 1.2 | **Adopt this roadmap as the risk management plan** and assign every owner below by name. | R-02 | Practice administrator | 2 hrs | — |
| 1.3 | **Enable multi-factor authentication** on email and all remote access. | R-01 | IT support (V-04) | 1 day | Usually included in existing licensing |
| 1.4 | **Execute the three missing business associate agreements** — IT support, answering service, copier vendor. | R-12 | Practice administrator | 1 week | — |
| 1.5 | **Confirm agreement status** for the four unconfirmed vendors. | R-12 | Practice administrator | 1 week | — |
| 1.6 | **Write the 42 CFR Part 2 applicability determination.** Whichever way it lands, put it in writing. | R-06 | Administrator + clinical director | 1 day | — |
| 1.7 | **Start an incident log**, including incidents judged not to be breaches. | R-01 | Practice administrator | 1 hr to set up | — |
| 1.8 | **Reposition reception monitors and fit privacy filters.** Replace the shared paper sign-in sheet with individual slips. | R-07 | Office manager | 1 day | ~$300 |

**Phase 1 total: under $500 and about two weeks of part-time effort.** It closes the clinic's single largest enforcement exposure.

---

## Phase 2 — Days 31 to 90 · Fix the technical fundamentals

| # | Action | Risk | Owner | Effort | Cost |
|---|---|---|---|---|---|
| 2.1 | **Issue unique named logins to every workforce member.** Disable all shared accounts. Pair with shorter screen-lock timeouts and badge-tap where the front desk workflow needs the speed. | R-03 | IT support | 2 weeks | Minimal |
| 2.2 | **Enable full-disk encryption** on all 14 laptops and all 28 workstations. Require encrypted removable media. | R-04 | IT support | 1 week | Built into current operating systems |
| 2.3 | **Document the addressable-specification analysis** for encryption — the decision, the reasoning, the date. | R-04 | Practice administrator | 2 hrs | — |
| 2.4 | **Build the joiner / mover / leaver checklist** covering every system. Make HR the trigger. | R-08 | Administrator + HR | 3 days | — |
| 2.5 | **Reconcile all active accounts** against the current staff roster. Disable anything unmatched. | R-08 | IT support | 2 days | — |
| 2.6 | **Begin monthly EPIC access review** — same-surname matches, staff-as-patient records, unusual volume. Keep dated records. | R-09 | Practice administrator | 4 hrs/month | — |
| 2.7 | **Perform a documented full restore test** to an isolated environment. | R-10 | IT support + backup vendor | 2 days | — |
| 2.8 | **Run the first phishing simulation** and deliver short role-specific follow-up training. | R-01 | Administrator + IT | 1 week | ~$500–1,500/yr |
| 2.9 | **Move scheduling calls out of earshot** of the waiting area. | R-07 | Office manager | Workflow change | — |

**Note on 2.1 → 2.6.** Unique logins must be in place before access review is meaningful. If Phase 2 slips, keep that order.

**Phase 2 total: roughly $500–1,500, mostly the phishing platform.** The technical work uses capability the clinic already owns and is not paying to use.

---

## Phase 3 — Days 91 to 180 · Structural work

| # | Action | Risk | Owner | Effort | Cost |
|---|---|---|---|---|---|
| 3.1 | **Segment the network into four zones** — clinical, staff general, building and facilities, guest. Isolate guest Wi-Fi completely. | R-05 | IT support | 2–3 weeks | $2,000–5,000 |
| 3.2 | **Inventory every vendor remote-access path.** Remove what isn't needed; make the rest on-request. | R-05, R-12 | IT support | 1 week | — |
| 3.3 | **If Part 2 applies:** verify EPIC's record segregation and consent configuration against it. | R-06 | Administrator + EPIC vendor | 3–4 weeks | Vendor time |
| 3.4 | **Move fax to a verified recipient directory** with a second-person check for anything outside it. Start an outbound release log. | R-11 | Office manager | 2 weeks | Minimal |
| 3.5 | **Apply the pre-network-admission checklist** to all existing connected devices retrospectively. | R-05 | IT support | 2 weeks | — |
| 3.6 | **Confirm breach notification terms** with all Tier 1 vendors. | R-12 | Practice administrator | 2 weeks | — |
| 3.7 | **Run a tabletop incident response exercise** using the breach decision tree. | R-01 | All leadership | 1 day | — |

**Phase 3 total: roughly $2,000–5,000**, nearly all of it network segmentation — the only item in this roadmap that needs real capital.

---

## Phase 4 — Ongoing · Keep it alive

NIST SP 800-30's fourth step is *Maintain Assessment*. Everything above decays without this.

| Cadence | Activity | Risk |
|---|---|---|
| **Monthly** | EPIC access review, documented | R-09 |
| **Monthly** | Incident log reviewed for patterns | R-01 |
| **Quarterly** | Account reconciliation against staff roster | R-08 |
| **Quarterly** | Phishing simulation and follow-up training | R-01 |
| **Annually** | Full risk analysis refresh — reuse this structure | R-02 |
| **Annually** | Restore test | R-10 |
| **Annually** | Vendor register review; Tier 1 evidence requests | R-12 |
| **Annually** | Role-specific workforce training | R-01 |
| **On any material change** | Re-run the risk analysis — new system, new site, new service line | R-02 |

That last trigger is what failed at Northgate the first time. The existing assessment was not wrong when written; it was never revisited after the EPIC migration.

---

## Where the register lands

| Risk | Now | After Phase 2 | After Phase 3 |
|---|---|---|---|
| R-01 Phishing | 20 Very High | 8 Moderate | 8 Moderate |
| R-02 Risk analysis | 20 Very High | 5 Moderate | 5 Moderate |
| R-03 Shared logins | 16 High | 8 Moderate | 8 Moderate |
| R-04 Encryption | 15 High | 6 Moderate | 6 Moderate |
| R-05 Flat network | 15 High | 15 High | 10 High |
| R-06 Part 2 | 15 High | 10 High | 5 Moderate |
| R-07 Front-of-house | 12 High | 6 Moderate | 6 Moderate |
| R-08 Access removal | 12 High | 6 Moderate | 6 Moderate |
| R-09 Log review | 12 High | 6 Moderate | 6 Moderate |
| R-10 Backup testing | 12 High | 4 Low | 4 Low |
| R-11 Fax and releases | 9 Moderate | 9 Moderate | 6 Moderate |
| R-12 Vendor register | 9 Moderate | 3 Low | 3 Low |

**From 2 Very High and 8 High, to 0 Very High and 1 High.**

R-05 stays High even after segmentation, and that is deliberate. Segmentation makes it harder for a compromised camera or thermostat to reach clinical systems, so likelihood falls — but the impact does not, because anything that *does* get through still stops the clinic operating that day. Connected devices the clinic does not patch remain connected devices the clinic does not patch. Marking it resolved would be the kind of optimism that makes a register useless.

---

## Cost summary

| Phase | Duration | Cost | Main constraint |
|---|---|---|---|
| 1 | 30 days | Under $500 | Administrator attention |
| 2 | 60 days | $500–1,500 | IT support scheduling |
| 3 | 90 days | $2,000–5,000 | Capital + EPIC vendor availability |
| 4 | Ongoing | ~$1,500/yr | Discipline |
| **Total year one** | | **$4,000–7,000** | |

For context: the settlement in the enforcement case that most closely resembles Northgate's highest risk was **$103,000**, plus two years of federally monitored corrective action requiring substantially this same work — done to someone else's deadlines, with a public announcement attached.

The comparison is the argument. Not because a penalty is likely, but because the corrective action plan OCR imposes looks almost exactly like Phase 1 and Phase 2 of this roadmap. The clinic does this work either way. Doing it voluntarily is cheaper, faster, and does not come with a press release.

---

## What the clinic should do on Monday

If only one thing happens this week: **1.1 and 1.2** — sign and date the risk analysis, and adopt this roadmap as the risk management plan.

It costs nothing, takes an afternoon, and closes the gap most likely to turn an incident into an enforcement action.

---

**Related:** `../01-risk-assessment/risk-register.md` · `../04-breach-readiness/ocr-audit-prep-checklist.md` · `../02-framework-crosswalk/hipaa-hitech-hitrust-nist-mapping.md`
