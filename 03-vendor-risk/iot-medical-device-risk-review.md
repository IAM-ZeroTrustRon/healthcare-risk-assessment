# Connected Device and IoT Risk Review

**Northgate Behavioral Health Clinic** — Security Risk Assessment
Addresses **R-05** · Supports **R-12**

> Fictional clinic. No real devices, vendors, or configurations.

---

## A scoping decision, stated up front

The obvious move in a healthcare risk assessment is to reach for FDA medical device cybersecurity guidance. This assessment deliberately did not lead with it, for two reasons.

**First, that guidance binds manufacturers, not clinics.** The FDA's premarket cybersecurity guidance and section 524B of the Federal Food, Drug, and Cosmetic Act govern what device makers must submit when they seek approval — vulnerability management plans, a software bill of materials, commitments to postmarket patching. A clinic cannot be non-compliant with section 524B. Northgate's lever is **procurement**: requiring those artifacts as a condition of purchase and network admission. Framing a clinic as subject to manufacturer obligations would be a category error, and an interviewer who knows the space would spot it immediately.

**Second, an outpatient behavioral health clinic has very few regulated medical devices.** There is no imaging suite, no infusion pump fleet, no patient monitoring network. Northgate has a couple of vitals stations and possibly a point-of-care drug screening analyser — and both may be standalone rather than networked.

**The real connected-device exposure here is ordinary building and office technology:** security cameras, the door badge controller, the HVAC unit, multifunction printers, smart TVs in group rooms, and guest Wi-Fi. None of these hold patient information. All of them are computers on the same network as the workstations that reach EPIC.

This review is scoped accordingly. An inflated medical-device section would have produced more impressive-looking citations and worse security advice.

---

## What Northgate actually has

| ID | Device group | Count | Holds patient info? | Managed by | Network | Concern |
|---|---|---|---|---|---|---|
| D-01 | IP security cameras | 8 | No | Vendor (V-10) | Clinical — flat | Standing vendor remote access; rarely patched; default credentials common |
| D-02 | Door badge controller | 1 | No | Vendor | Clinical — flat | Controls physical access to records and clinical space |
| D-03 | HVAC / building management | 1 | No | Vendor (V-11) | Clinical — flat | Remote vendor access, unmonitored |
| D-04 | Smart TVs, group and waiting rooms | 3 | No | Nobody | Clinical — flat | Consumer devices, no patch discipline, microphones |
| D-05 | Multifunction printers | 4 | **Yes** — stored scans and print jobs | Vendor (V-12) | Clinical — flat | Internal storage; web admin interfaces; documents leave with the device at lease end |
| D-06 | Guest Wi-Fi access points | 6 | No | Contracted IT | **Same network** | Patient-facing and untrusted, with a path to clinical systems |
| D-07 | Vitals stations | 2 | Transiently | Clinic | Standalone or clinical | Possibly an FDA-regulated device; verify whether networked |
| D-08 | Point-of-care drug screening analyser | 1 | Transiently | Clinic | Standalone or clinical | Likely an FDA-regulated device; verify whether networked |

**Two of eight groups are plausibly regulated medical devices. Six are not.** That ratio is what drove the scoping decision.

---

## The core finding

**Everything is on one network.** A patient on guest Wi-Fi, a camera the clinic does not administer, and the workstation a prescriber uses to open a chart all sit in the same space with nothing between them.

Individually none of D-01 to D-06 is interesting to an attacker. Collectively they are the entry point, because each is a computer that someone else patches — or doesn't — and each has an unobstructed path to the systems that matter. This is how small-clinic ransomware incidents typically begin: not with a sophisticated attack on the clinical system, but with a forgotten device that shouldn't have been able to reach it.

Printers deserve a specific note. D-05 is the only group here that holds patient information, and it is the one most often left off inventories entirely. Multifunction printers store scanned and printed documents on internal drives, and those drives leave the building when the lease ends — which engages §164.310(d)(2)(i) disposal and §164.310(d)(2)(ii) media re-use, both **Required** specifications.

---

## Recommended segmentation

Four zones, minimum:

| Zone | Contains | Rules |
|---|---|---|
| **Clinical** | Workstations, laptops, printers | Reaches EPIC and the internet. Not reachable from any other zone. |
| **Staff general** | Non-clinical admin devices | Internet only. No path to clinical. |
| **Building and facilities** | Cameras, badge controller, HVAC, smart TVs | No internet except specific vendor management addresses. No path to clinical. |
| **Guest** | Patient Wi-Fi | Internet only. Fully isolated, including from other guest devices. |

**Why four and not more:** this is achievable on the equipment a 45-person clinic already owns, using VLANs and firewall rules, without new hardware or a full-time network engineer. A twelve-zone design would be better on paper and would not get implemented. The right answer for this clinic is the one that actually gets built.

---

## Pre-network-admission checklist

Run before any connected device joins a Northgate network — medical or not. Designed for a practice administrator to work through with a vendor, not for a network engineer.

### 1 · Identify
- [ ] What is this device and what does it do?
- [ ] Is it an FDA-regulated medical device? If unsure, ask the vendor in writing.
- [ ] Does it store, transmit or display patient information — even transiently?
- [ ] Who owns it: the clinic, or the vendor?
- [ ] Added to the asset inventory?

### 2 · Decide the zone
- [ ] Which of the four zones does it belong in?
- [ ] Does it genuinely need to reach the internet? Most building devices do not.
- [ ] Does it need to reach any clinical system? If yes, why — in writing.

### 3 · Access and accounts
- [ ] Default credentials changed, and the new ones recorded in the clinic's password manager.
- [ ] Does the vendor need remote access? If yes: how, how often, and can it be turned on only when needed?
- [ ] Is vendor access logged, and can the clinic revoke it unilaterally?
- [ ] Any account that is not needed — disabled.

### 4 · Maintenance and lifespan
- [ ] Who patches it: clinic or vendor? Named in writing.
- [ ] How are security updates delivered, and how often?
- [ ] **What is the end-of-support date?** Ask before purchase. A device the vendor will stop patching in two years is a two-year device.
- [ ] Is there a security contact to report a problem to?

### 5 · Vendor and contract
- [ ] Is the vendor a business associate? If the device touches patient information, probably yes — see `baa-vendor-risk-scorecard.md`.
- [ ] BAA executed where required.
- [ ] **For regulated medical devices:** request the manufacturer's cybersecurity documentation — vulnerability handling plan, software bill of materials, patch commitment. These are things manufacturers now produce for FDA submissions. A clinic cannot compel them, but it can make them a purchasing condition.
- [ ] Ask for a completed **MDS2** form — a voluntary industry standard (ANSI/NEMA HN 1-2019) through which manufacturers disclose a device's security features in a consistent format. Useful when available; not a certification, and self-reported by the manufacturer.

### 6 · Decommissioning — decide now, not later
- [ ] Does it store anything that must be wiped before disposal or lease return?
- [ ] Who performs the wipe, and who documents it?
- [ ] For leased equipment: what does the contract say happens to stored data at end of term?

### 7 · Record the decision
- [ ] Zone assignment and justification written down.
- [ ] Any accepted risk recorded, with who accepted it and when.

That last step is the one most often skipped and the one that matters under §164.306(d)(3): where a safeguard isn't reasonable and appropriate, the clinic has to document why and implement an equivalent alternative where one is reasonable and appropriate. An undocumented decision is indistinguishable from no decision.

---

## Where this maps

| Element | HIPAA | NIST CSF 2.0 | HITRUST |
|---|---|---|---|
| Device inventory | §164.308(a)(1)(ii)(A) risk analysis (**R**) | ID.AM | Asset Management |
| Network segmentation | §164.312(a)(1) access control · §164.312(e)(1) transmission security | PR.IR, PR.PS | Communications and Operations Management |
| Vendor remote access | §164.308(b)(1) · §164.314(a) | GV.SC | Organization of Information Security |
| Printer storage and disposal | §164.310(d)(2)(i) disposal (**R**) · §164.310(d)(2)(ii) media re-use (**R**) | PR.DS | Asset Management |
| Documented decisions | §164.306(d)(3) · §164.316(b)(1) | GV.PO | Information Security Management Program |

---

## What this review could not establish

Stated plainly, because a real engagement would resolve all four:

1. **Whether D-07 and D-08 are actually networked.** This determines whether any FDA-regulated device is in scope at all. A network scan would answer it in an afternoon.
2. **The actual device population.** The list above reflects what a clinic of this size and age typically has, not a discovered inventory.
3. **Existing vendor remote-access paths.** Nobody at Northgate currently knows how many there are.
4. **Whether the printers' internal storage is encrypted** and what the lease says about end-of-term data handling.

---

**Related:** `baa-vendor-risk-scorecard.md` · `../01-risk-assessment/risk-register.md` (R-05) · `../05-remediation/remediation-roadmap.md`
