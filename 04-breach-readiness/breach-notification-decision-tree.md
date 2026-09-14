# Breach Notification Decision Tree

**Northgate Behavioral Health Clinic** — Security Risk Assessment
Supports **R-01**, **R-04**, **R-06**, **R-11**

> Fictional clinic. This is a portfolio demonstration of regulatory analysis, not legal advice. A real clinic facing a suspected breach should involve counsel.

---

## What this is for

When something goes wrong — a laptop disappears, an email goes to the wrong person, a mailbox is compromised — the clinic has a limited window and a sequence of decisions to make. This walks through them in order.

Two things to fix in your head before starting:

**The clock runs from discovery, not from when it happened.** A laptop stolen in March and noticed in June starts its clock in June. Every deadline below counts from discovery.

**Not every incident is a breach.** The rules have a specific definition and specific exceptions. Working through them properly is what separates a defensible decision from a panicked over-notification or a negligent under-notification — and the clinic carries the burden of proving whichever conclusion it reaches.

---

## Step 0 · Which rule even applies?

Answer this first. It takes one question.

> **Is Northgate a HIPAA covered entity?** → **Yes.**

Then the **HIPAA Breach Notification Rule** (45 CFR §§164.400–414) applies, and the **FTC Health Breach Notification Rule** (16 CFR Part 318) does not.

**These two rules cannot both apply to the same organisation.** The FTC rule defines the entities it covers — "vendor of personal health records" and "PHR related entity" — as entities *other than* a HIPAA covered entity, or other than an entity acting as a business associate of one. The boundary is written into the definitions at 16 CFR §318.2. It is not a judgment call and there is no election to make.

**Where the FTC rule does become relevant to Northgate:** indirectly, through apps. If the clinic recommends a mood-tracking or wellness app that is *not* a business associate, that app's breaches fall under the FTC rule, and Northgate has no HIPAA leverage over the vendor at all. That is a vendor-selection consideration, not a notification obligation — see `../03-vendor-risk/baa-vendor-risk-scorecard.md`.

---

## The tree

```
INCIDENT DISCOVERED
        │
        ▼
┌─────────────────────────────────────────────────────────┐
│ Q1. Was protected health information involved?          │
└─────────────────────────────────────────────────────────┘
        │                                    │
       NO                                   YES
        │                                    │
        ▼                                    ▼
  Not a breach.                  ┌──────────────────────────────────┐
  Log it. Consider               │ Q2. Was the information secured  │
  whether it signals             │     — encrypted or destroyed to  │
  a control gap.                 │     the federal standard?        │
                                 └──────────────────────────────────┘
                                        │                    │
                                       YES                   NO
                                        │                    │
                                        ▼                    ▼
                           Generally not a reportable   ┌─────────────────────┐
                           breach — the rules apply     │ Q3. Does one of the │
                           to *unsecured* information.  │ three exceptions    │
                           Document the encryption      │ apply?              │
                           evidence and stop.           └─────────────────────┘
                                                            │            │
                                                           YES           NO
                                                            │            │
                                                            ▼            ▼
                                                   Not a breach.   ┌──────────────────┐
                                                   Document which  │ Q4. Four-factor  │
                                                   exception and   │ risk assessment  │
                                                   why.            └──────────────────┘
                                                                      │           │
                                                              LOW probability   Cannot
                                                              of compromise,    demonstrate
                                                              demonstrated      low probability
                                                                      │           │
                                                                      ▼           ▼
                                                              Not a breach.   ► NOTIFY
                                                              Document the       (go to
                                                              full analysis.     Step 5)
```

---

## Q2 · Was the information secured?

The breach rules apply to **unsecured** protected health information — information not rendered unusable, unreadable or indecipherable to unauthorised people through a technology or methodology specified by the Secretary of HHS. HHS guidance specifies **encryption** and **destruction**.

This is why **R-04** matters more than its score suggests. An encrypted stolen laptop is generally not a reportable breach. The same laptop unencrypted is a notification event, a report to HHS, possible media notice, and a permanent public entry on the federal breach portal. Encryption is the single control with the best ratio of effort to consequence avoided.

Document the evidence — that the device was encrypted, and that the encryption was active at the time.

---

## Q3 · The three exceptions

If any one applies, it is not a breach. Each has conditions that must all hold.

| # | Exception | Conditions |
|---|---|---|
| 1 | **Unintentional acquisition, access or use by a workforce member** | Made in good faith, within scope of authority, and **not further used or disclosed** impermissibly |
| 2 | **Inadvertent disclosure between authorised people** at the same covered entity, business associate, or organised health care arrangement | Both parties authorised to access protected health information, and the information **not further used or disclosed** impermissibly |
| 3 | **Good faith belief the unauthorised recipient could not reasonably have retained** the information | Must be a genuine, documentable belief |

*Everyday example of exception 1:* an intake coordinator opens the wrong chart, realises immediately, closes it, tells no one else. Good faith, within scope, nothing further. Not a breach — but log it, because a pattern of these is a control finding.

Note that exceptions 1 and 2 both collapse if the information travels further. "I accidentally opened it and then mentioned it to a colleague" is no longer covered.

---

## Q4 · The four-factor risk assessment

If no exception applies, the regulation **presumes a breach**. The clinic can rebut that presumption only by demonstrating a **low probability that the information has been compromised**, based on a risk assessment of at least four factors:

| # | Factor | What to actually ask |
|---|---|---|
| 1 | **Nature and extent** of the information, including identifiers and likelihood of re-identification | Was it a name and appointment time, or a diagnosis and treatment history? **For a behavioral health clinic, the fact that someone is a patient here is itself sensitive** — weight it accordingly. |
| 2 | **Who** used it or received it | Another covered entity bound by the same rules? A stranger? An unknown party? |
| 3 | Whether the information was **actually acquired or viewed** | Mailbox forensics, access logs, delivery confirmations. **This is where R-09 bites** — a clinic that never reviews logs often cannot answer this, and "we don't know" does not demonstrate low probability. |
| 4 | Extent to which the risk has been **mitigated** | Confirmed deletion? Signed attestation? Remote wipe? Recovered device? |

Three points worth internalising:

- The burden is on the clinic, not the regulator. Silence defaults to "breach."
- Low probability of **compromise** is the test — not low probability of harm.
- The clinic may skip this analysis and simply notify. Sometimes that is the right call, and it is expressly permitted.

---

## Step 5 · If it is a breach — who gets told, and when

| Who | Citation | Deadline |
|---|---|---|
| **Affected individuals** | §164.404 | Without unreasonable delay, and **no later than 60 days following discovery** |
| **Prominent media** — only if the breach affects more than 500 residents of a State or jurisdiction | §164.406 | Same outer limit as individual notice |
| **HHS Secretary — 500 or more individuals** | §164.408(b) | **Contemporaneously with individual notice, which must itself occur within 60 days of discovery** |
| **HHS Secretary — fewer than 500 individuals** | §164.408(c) | Maintain a log; report **no later than 60 days after the end of the calendar year** in which the breach was discovered |
| **Northgate, if the breach happened at a business associate** | §164.410 | The business associate must notify the clinic without unreasonable delay and no later than 60 days from its discovery |

> **A precision note on the 500-or-more deadline.** It is commonly stated as "within 60 days." The regulation at §164.408(b) actually says notice to the Secretary must be **contemporaneous with the individual notice** required by §164.404(a). Since individual notice is itself capped at 60 days from discovery, the two statements usually land in the same place — but they are not the same instruction, and "contemporaneously with individual notice" is what the rule says. Plain-language summaries, including HHS's own, use the looser phrasing.

**Individual notice mechanics:** written notice by first-class mail, or email if the individual has agreed to electronic notice. Where the clinic has insufficient or out-of-date contact details for 10 or more people, substitute notice is required — either a posting on the home page of the clinic website for at least 90 days, or notice in major print or broadcast media serving the area — together with a toll-free number active for at least 90 days. For fewer than 10 people, an alternative form of written notice, telephone, or other means will do.

**What the notice must contain:** a brief description of what happened, the types of information involved, steps individuals should take to protect themselves, what the clinic is doing to investigate and mitigate, and contact details.

*Mechanics in this section follow HHS's published summary of the Breach Notification Rule. The section-level citations and the §164.408 timing language above were verified against the regulation itself.*

---

## If Part 2 applies

Should the applicability analysis under **R-06** conclude that 42 CFR Part 2 covers Northgate's substance use disorder records, breach notification obligations attach to those records as well. The relevant section is **42 CFR §2.16, "Security for records and notification of breaches."**

Two practical consequences:

1. The clinic would need to notify for breaches of Part 2 records, and HHS confirms this includes notifying affected individuals, the Secretary, and in some cases the media.
2. The same office — OCR — now administers and enforces both HIPAA and Part 2, following a delegation of authority in August 2025. A single incident touching both is handled by one regulator under two rule sets.

A clinic in this position should read §2.16's operative text directly and build its incident procedure around both rules together rather than bolting one onto the other.

---

## Do this in the first 24 hours

Before any of the analysis above:

1. **Contain it.** Disable the account, isolate the device, stop the sending.
2. **Start a written timeline.** Discovery date and time, who found it, what is known. This document becomes the spine of everything that follows.
3. **Preserve evidence.** Do not wipe the mailbox, do not reimage the laptop, do not clear the logs.
4. **Tell the practice administrator** — the named security official.
5. **Do not notify anyone externally yet.** Work the tree first.
6. **Note the 60-day clock start date** prominently at the top of the timeline.

---

## What this exercise reveals about the clinic

Three register findings become visible the moment you try to use this tree:

- **R-09** — without log review, factor 3 of the four-factor assessment often cannot be answered, which forces notification by default.
- **R-03** — with shared logins, the clinic cannot establish *who* accessed something, which undermines factors 2 and 3.
- **R-04** — without encryption, Q2 never terminates the analysis early.

A clinic that fixes those three does not just reduce the chance of a breach. It substantially improves its ability to demonstrate that an incident **wasn't** one.

---

**Related:** `ocr-audit-prep-checklist.md` · `../01-risk-assessment/risk-register.md` · `../02-framework-crosswalk/hipaa-hitech-hitrust-nist-mapping.md`
