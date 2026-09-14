# Risk Heat Map

**Northgate Behavioral Health Clinic** — Security Risk Assessment
NIST SP 800-30 Rev. 1, Step 2, task 5: Determine Risk

> Fictional clinic. No real patient information, organizations, or incidents.

---

## The map

Impact runs up the side. Likelihood runs along the bottom. Each cell shows the risk score and any risks that landed there.

```
            │  VERY LOW  │    LOW     │  MODERATE  │    HIGH    │ VERY HIGH  │
            │    (1)     │    (2)     │    (3)     │    (4)     │    (5)     │
════════════╪════════════╪════════════╪════════════╪════════════╪════════════╡
 VERY HIGH  │     5      │     10     │     15     │     20     │     25     │
    (5)     │            │            │   R-04     │   R-02     │            │
  IMPACT    │            │            │   R-05     │            │            │
            │            │            │   R-06     │            │            │
────────────┼────────────┼────────────┼────────────┼────────────┼────────────┤
   HIGH     │     4      │     8      │     12     │     16     │     20     │
    (4)     │            │            │   R-10     │   R-03     │   R-01     │
            │            │            │            │            │            │
────────────┼────────────┼────────────┼────────────┼────────────┼────────────┤
 MODERATE   │     3      │     6      │     9      │     12     │     15     │
    (3)     │            │            │   R-11     │   R-07     │            │
            │            │            │   R-12     │   R-08     │            │
            │            │            │            │   R-09     │            │
────────────┼────────────┼────────────┼────────────┼────────────┼────────────┤
   LOW      │     2      │     4      │     6      │     8      │     10     │
    (2)     │            │            │            │            │            │
────────────┼────────────┼────────────┼────────────┼────────────┼────────────┤
 VERY LOW   │     1      │     2      │     3      │     4      │     5      │
    (1)     │            │            │            │            │            │
════════════╧════════════╧════════════╧════════════╧════════════╧════════════╛
                              L I K E L I H O O D
```

**Bands**

| Score | Rating | Action |
|---|---|---|
| 17–25 | Very High | Fix now |
| 10–16 | High | Fix this year, named owner and date |
| 5–9 | Moderate | Plan it |
| 3–4 | Low | Accept, revisit annually |
| 1–2 | Very Low | Accept |

---

## Where the risks landed

| Rating | Count | Risks |
|---|---|---|
| **Very High** | 2 | R-01 phishing · R-02 risk analysis |
| **High** | 8 | R-03 shared logins · R-04 encryption · R-05 flat network · R-06 Part 2 · R-07 front-of-house · R-08 access removal · R-09 log review · R-10 backup testing |
| **Moderate** | 2 | R-11 fax and releases · R-12 vendor agreements |
| **Low** | 0 | — |
| **Very Low** | 0 | — |

---

## Reading the shape

**Nothing landed in Low.** That is a finding, not a scoring error. A clinic that has never completed a current risk analysis has, by definition, never deliberately reduced anything — so the register reflects a starting position, not a maintained programme. The comparison worth making is against the *next* assessment: after the roadmap's first two phases, most of these should move down and to the left, and some genuinely should end up in Low.

**The upper-left cluster is the expensive-but-unlikely group.** R-04, R-05 and R-06 all scored Very High impact with Moderate likelihood. These are the "it probably won't happen, and it will be very bad if it does" risks — the ones organisations reliably under-fund because nothing has gone wrong yet.

**The lower-right cluster is the everyday group.** R-07, R-08 and R-09 scored High likelihood with Moderate impact. Each of these is probably happening already, quietly, without anyone noticing. They are also the cheapest to fix.

**R-01 sits alone in the top right** because it is the one risk that is both near-certain and seriously damaging — and because it is the exact pattern that produced a real OCR settlement against a comparable provider in February 2026.

**R-02 is the one that makes the others count.** Even if every other risk here were fixed tomorrow, an absent or stale risk analysis is independently citable, and is the most common single finding in recent enforcement. It scores Very High on impact for that reason alone.

---

## Movement expected after remediation

Projected positions once the roadmap's first two phases are complete. Shown as a target, not a claim.

| Risk | Now | Projected | What moves it |
|---|---|---|---|
| R-01 | 20 Very High | 8 Moderate | Multi-factor authentication drops likelihood from 5 to 2 |
| R-02 | 20 Very High | 5 Moderate | This assessment, adopted and scheduled, drops likelihood from 4 to 1 |
| R-03 | 16 High | 8 Moderate | Unique accounts drop likelihood from 4 to 2 |
| R-04 | 15 High | 6 Moderate | Full-disk encryption drops impact from 5 to 2 — encrypted loss is generally not a reportable breach, though active-session and key-management exposure remain |
| R-05 | 15 High | 10 High | Segmentation cuts the path from building devices to clinical systems, dropping likelihood from 3 to 2. Impact stays at 5, because anything that does reach clinical systems still stops the clinic operating |
| R-06 | 15 High | 5 Moderate | Resolving the applicability question drops likelihood from 3 to 1 |
| R-07 | 12 High | 6 Moderate | Screens, slips and call relocation drop likelihood from 4 to 2 |
| R-08 | 12 High | 6 Moderate | Leaver checklist drops likelihood from 4 to 2 |
| R-09 | 12 High | 6 Moderate | Monthly review drops likelihood from 4 to 2 |
| R-10 | 12 High | 4 Low | A tested restore drops likelihood from 3 to 1 |
| R-11 | 9 Moderate | 6 Moderate | Verified directory drops likelihood from 3 to 2 |
| R-12 | 9 Moderate | 3 Low | A complete vendor register drops likelihood from 3 to 1 |

R-04 is the standout. Encryption is the only control on this list that reduces **impact** rather than likelihood, and it does so sharply — which is why it earns its place in Phase 1 despite being an addressable rather than a required specification.

---

**Next:** `../02-framework-crosswalk/hipaa-hitech-hitrust-nist-mapping.md` maps every risk here to its regulatory and framework citations.
