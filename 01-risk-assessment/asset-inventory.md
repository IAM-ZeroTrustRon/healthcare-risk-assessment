# Asset Inventory

**Northgate Behavioral Health Clinic** — Security Risk Assessment
NIST SP 800-30 Rev. 1, Step 1: Prepare for Assessment

> Fictional clinic. No real patient information, organizations, or systems.

---

## Why this file exists

You cannot protect what you cannot list. Before scoring any risk, a risk assessment has to establish what the clinic actually has, where patient information lives, and how it moves.

The Security Rule doesn't use the phrase "asset inventory," but it requires an *accurate and thorough* assessment of risks to patient information the clinic "creates, receives, maintains, or transmits." Those four verbs are the inventory instruction. OCR's own post-settlement guidance puts it plainly: identify where electronic patient information is located, including how it enters, moves through, and leaves the organisation.

Throughout this repo, **ePHI** means electronic protected health information — patient information in electronic form that identifies someone and relates to their health, care, or payment for care.

---

## The clinic

| | |
|---|---|
| **Type** | Outpatient behavioral health — individual and group therapy, psychiatric medication management |
| **Size** | ~45 workforce members; roughly 3,000 active patients |
| **Sites** | One main clinic, one satellite office open three days a week |
| **EHR** | EPIC Ambulatory (clinical record) and EPIC Cadence (scheduling), vendor-hosted |
| **Regulatory status** | HIPAA covered entity. Part 2 applicability assessed separately — see R-06 and `TECHNICAL-DEEP-DIVE.md` |

---

## Where patient information lives

Ranked by how much harm its loss would cause.

| ID | Asset | What it holds | Criticality |
|---|---|---|---|
| A-01 | **EPIC Ambulatory** (vendor-hosted) | The clinical record — assessments, progress notes, diagnoses, medication history, treatment plans | Critical |
| A-02 | **EPIC Cadence** (vendor-hosted) | Scheduling. Names, appointment times, provider, visit type | Critical |
| A-03 | **Clinic email** (cloud-hosted) | Unstructured patient information in ordinary staff correspondence | Critical |
| A-04 | **Telehealth platform** | Live session video, session metadata, waiting-room presence | High |
| A-05 | **Billing and clearinghouse interface** | Claims, diagnosis codes, insurance and payment information | High |
| A-06 | **Clinical workstations** (28 desktops) | Cached files, local downloads, active EPIC sessions | High |
| A-07 | **Clinician laptops** (14) | Documentation drafts, exports, offline work, carried off-site | High |
| A-08 | **Network file share** | Group programme rosters, intake packets, historical scanned records | High |
| A-09 | **Paper records at reception** | Sign-in sheets, intake forms, fax output, release-of-information requests | Moderate |
| A-10 | **Backup repository** | Full copies of everything above | Critical |
| A-11 | **Multifunction printers / fax** (4) | Spooled documents, stored scan history, inbound fax queue | Moderate |
| A-12 | **Removable media** | Ad hoc exports to USB for vendors and reporting | Moderate |

---

## Connected devices that are not clinical systems

Listed separately and deliberately. These hold no patient information — which is exactly why they get forgotten, and exactly why they matter. Each one is a computer on the same network as the systems that do hold patient information.

| ID | Device group | Count | Why it's in scope |
|---|---|---|---|
| D-01 | IP security cameras | 8 | Vendor-managed, rarely patched, internet-reachable by default |
| D-02 | Door badge controller | 1 | Controls physical access to record storage and clinical space |
| D-03 | HVAC / building management controller | 1 | Remote vendor access, typically unmonitored |
| D-04 | Smart TVs — group and waiting rooms | 3 | Consumer devices, no patch discipline, network-attached |
| D-05 | Multifunction printers | 4 | Store documents; often have web interfaces with default credentials |
| D-06 | Guest Wi-Fi access points | 6 | Patient-facing, untrusted by definition |
| D-07 | Vitals station (blood pressure, pulse, weight) | 2 | Semi-clinical; may be a regulated medical device |
| D-08 | Point-of-care drug screening analyser | 1 | Regulated medical device if network-connected |

**Scoping note.** Only D-07 and D-08 are plausibly FDA-regulated medical devices, and both may well be standalone rather than networked. The larger connected-device exposure at an outpatient behavioral health clinic is D-01 through D-06 — ordinary building and office technology. `03-vendor-risk/iot-medical-device-risk-review.md` explains why this assessment scoped it that way rather than reaching for medical device cybersecurity guidance that mostly binds manufacturers.

---

## Who has access

| Role | Headcount | Reaches |
|---|---|---|
| Therapists / counsellors | 18 | EPIC Ambulatory, telehealth, email |
| Prescribers (psychiatrist, nurse practitioners) | 4 | EPIC Ambulatory, e-prescribing, telehealth, email |
| Intake coordinators | 5 | EPIC Ambulatory + Cadence, email, fax |
| Front desk / scheduling | 6 | EPIC Cadence, email, fax, payments |
| Billing | 4 | EPIC billing module, clearinghouse, email |
| Case managers | 5 | EPIC Ambulatory, email, external referral portals |
| Practice administrator | 1 | All systems, plus vendor relationships |
| Contracted IT support | external | Infrastructure, workstations, network |
| Interns / trainees on rotation | 2–6, varies | EPIC Ambulatory under supervision |

**The access risk here is turnover shape, not headcount.** Per-diem clinicians, rotating interns and contracted prescribers have fuzzy end dates. That's what drives R-08.

---

## How information moves

Understanding the flows is what turns a list into an assessment.

**Into the clinic**
Referrals arrive by fax and by phone → intake coordinator creates the record in EPIC → insurance verified through the clearinghouse → intake paperwork completed on paper at reception and scanned in.

**Inside the clinic**
Clinicians document in EPIC. Staff discuss patients by email — the flow nobody designs and everybody uses, and the reason A-03 is rated Critical. Group rosters and programme materials sit on the shared drive. Front desk works from Cadence all day on shared workstations.

**Out of the clinic**
Claims go to the clearinghouse. Records requests go out by fax under a signed release. Clinicians carry laptops to the satellite site and home. Telehealth sessions leave the building by definition. Backups replicate to the vendor's environment.

**The flow that matters most:** email. It is the only asset where patient information accumulates without anyone deciding it should, it has the weakest controls, and it is the route in the enforcement case that most closely resembles this clinic.

---

## Assumptions this inventory makes

Stated openly, because a real engagement would verify each one:

1. EPIC is vendor-hosted, so the clinic's exposure is at the access and endpoint layer rather than the server layer.
2. All 45 workforce members have email; not all have EPIC.
3. The connected-device list is what a clinic of this size and age typically has. In a real engagement this would come from a network scan, not from experience.
4. No on-premises domain controller or self-hosted clinical server.
5. The satellite site connects over a site-to-site VPN.

---

**Next:** `threat-vulnerability-matrix.md` pairs these assets with what could realistically go wrong.
