# Business Associate and Vendor Risk Scorecard

**Northgate Behavioral Health Clinic** — Security Risk Assessment
Addresses **R-12** · Supports **R-01**, **R-05**, **R-06**, **R-10**

> Fictional clinic and fictional vendors. Vendor names below are generic placeholders, not real companies.

---

## The requirement, in plain terms

Northgate may only let an outside company handle patient information if it first gets **written satisfactory assurances** that the company will protect it. That written agreement is called a **Business Associate Agreement**, usually shortened to BAA.

The Security Rule sets this out at §164.308(b)(1), and documenting the assurances in a written contract is a **Required** implementation specification at §164.308(b)(3), pointing to the contract requirements at §164.314(a). Required means there is no alternative route.

**A business associate is any outside party that creates, receives, maintains or transmits patient information on the clinic's behalf.** The test is what they touch, not what they are called. A shredding company that hauls away boxes of charts is a business associate. A landlord who never touches records is not.

The practical failure at most small clinics is not refusing to sign agreements. It is not knowing who all the vendors are.

---

## Scoring method

Each vendor gets scored on four factors, 1 to 5, and the total sets the oversight tier.

| Factor | 1 | 3 | 5 |
|---|---|---|---|
| **Data sensitivity** — what do they touch? | No patient information | Names and appointments only | Full clinical records, including any substance use disorder information |
| **Access depth** — how far do they reach? | One-off, supervised | Scheduled access to defined systems | Standing administrative access |
| **Volume** — how many patients? | Under 50 | Hundreds | All patients |
| **Substitutability** — how fast could we replace them? | Days | Weeks | Months, or not realistically |

**Total 4–20.** Substitutability is included because it measures operational dependence: a vendor you cannot leave is one whose security you must verify rather than merely contract for.

| Total | Tier | Oversight |
|---|---|---|
| 16–20 | **Tier 1 — Critical** | BAA plus annual security review, evidence of independent assessment, named contacts, breach notification terms confirmed |
| 10–15 | **Tier 2 — Significant** | BAA plus annual questionnaire and attestation |
| 4–9 | **Tier 3 — Routine** | BAA on file, reviewed at contract renewal |

---

## Vendor register

| # | Vendor / service | Business associate? | Sens. | Access | Vol. | Subst. | **Total** | Tier | BAA | Last reviewed |
|---|---|---|---|---|---|---|---|---|---|---|
| V-01 | EHR hosting and support (EPIC environment) | **Yes** | 5 | 5 | 5 | 5 | **20** | 1 | ✅ Signed | Not since signing |
| V-02 | Billing and revenue cycle company | **Yes** | 4 | 4 | 5 | 4 | **17** | 1 | ✅ Signed | Not since signing |
| V-03 | Telehealth platform | **Yes** | 5 | 3 | 4 | 4 | **16** | 1 | ⚠️ Unconfirmed | Never |
| V-04 | Contracted IT support company | **Yes** | 4 | 5 | 5 | 3 | **17** | 1 | ❌ **Not on file** | Never |
| V-05 | Claims clearinghouse | **Yes** | 4 | 3 | 5 | 4 | **16** | 1 | ✅ Signed | Not since signing |
| V-06 | Transcription service | **Yes** | 5 | 2 | 3 | 2 | **12** | 2 | ⚠️ Unconfirmed | Never |
| V-07 | After-hours answering service | **Yes** | 3 | 2 | 3 | 2 | **10** | 2 | ❌ **Not on file** | Never |
| V-08 | Secure document shredding | **Yes** | 4 | 1 | 3 | 1 | **9** | 3 | ✅ Signed | Not since signing |
| V-09 | Off-site backup / disaster recovery | **Yes** | 5 | 2 | 5 | 3 | **15** | 2 | ✅ Signed | Not since signing |
| V-10 | Security camera vendor (managed) | **No** — see note | 1 | 3 | 1 | 2 | **7** | 3 | N/A | Never |
| V-11 | HVAC / building management vendor | **No** | 1 | 3 | 1 | 2 | **7** | 3 | N/A | Never |
| V-12 | Copier / multifunction printer lease and service | **Yes** — see note | 3 | 2 | 3 | 2 | **10** | 2 | ❌ **Not on file** | Never |
| V-13 | Interpreter / language services | **Yes** | 4 | 1 | 2 | 2 | **9** | 3 | ⚠️ Unconfirmed | Never |
| V-14 | Patient appointment reminder service | **Yes** | 2 | 2 | 5 | 2 | **11** | 2 | ⚠️ Unconfirmed | Never |

---

## Three classification calls worth explaining

**V-10 and V-11 are not business associates — and are still a problem.**
The camera and HVAC vendors never touch patient information, so no BAA is required. But both have standing remote access to devices sitting on the same flat network as clinical workstations (**R-05**). The control needed here is not a BAA — it is network segmentation and vendor remote-access management. Demanding a BAA from them would be the wrong instrument, and would create false comfort. Getting this distinction right in both directions is the point.

**V-12, the copier vendor, *is* a business associate,** and this is the one most often missed. Multifunction printers store scanned and printed documents on internal drives. When the lease ends and the machine is collected, those documents leave with it. That makes the vendor a handler of patient information, and it connects directly to §164.310(d)(2)(i) disposal and §164.310(d)(2)(ii) media re-use — both **Required** specifications.

**V-14, the reminder service, touches the least sensitive information and reaches the most patients.**
Appointment reminders carry only a name, a time and a clinic identity. In most specialties that is low-sensitivity. **In behavioral health, a reminder message that identifies the clinic by name, going to a phone another household member can see, discloses the one fact patients most want protected.** This is scored 2 for sensitivity because the data field is thin — but the mitigation is a content decision, not a data-volume decision, and it belongs in the vendor conversation.

---

## Findings

| # | Finding | Vendors | Severity |
|---|---|---|---|
| VF-1 | **No BAA on file for three business associates**, one of them Tier 1 with standing administrative access | V-04, V-07, V-12 | **Critical** |
| VF-2 | **BAA status unconfirmed for four vendors** — records incomplete, cannot say either way | V-03, V-06, V-13, V-14 | High |
| VF-3 | **No BAA has been reviewed since signature.** Several predate the clinic's EPIC migration | V-01, V-02, V-05, V-08, V-09 | High |
| VF-4 | **No single vendor register existed** before this assessment | All | High |
| VF-5 | **Non-BAA vendors with network access are unmanaged** — no inventory of remote access paths, no segmentation | V-10, V-11 | High |
| VF-6 | **No breach notification terms confirmed** with any Tier 1 vendor beyond the BAA's default language | V-01–V-05 | Moderate |
| VF-7 | **No vendor has been asked for evidence** of independent security assessment | All Tier 1 | Moderate |

**VF-1 is the finding that would hurt most in an investigation.** V-04, the IT support company, has standing administrative access to every workstation in the building, and there is no written agreement. §164.308(b)(3) does not offer a flexible alternative.

---

## What to do

**Within 30 days**
1. Execute BAAs with V-04, V-07 and V-12. Do not wait for the wider programme.
2. Confirm BAA status for V-03, V-06, V-13 and V-14, and execute wherever one is missing.
3. Adopt this register as the clinic's vendor inventory, with the practice administrator as named owner.

**Within 90 days**
4. Inventory every vendor remote-access path, including V-10 and V-11, and remove any that isn't needed.
5. Confirm breach notification terms with all Tier 1 vendors — specifically how fast they will tell Northgate, and what they will provide.
6. Review the content of V-14's reminder messages against the disclosure concern above.

**Within 12 months**
7. Request evidence of independent security assessment from all Tier 1 vendors.
8. Set a standing annual review date for every Tier 1 and Tier 2 agreement.
9. Add "confirm business associate status and BAA" as a required step before any new vendor touches clinic systems.

---

## Keeping it current

A vendor register decays fast. Three triggers should force an update:

- **Any new vendor**, before they get access — not after.
- **Any change in what a vendor touches** — a billing company that starts handling records requests has changed tier.
- **Annually**, as part of the risk analysis refresh under **R-02**.

The register is also the first document OCR tends to ask for in an investigation, alongside the risk analysis. It is worth keeping in a state you could hand over the same day.

---

**Related:** `iot-medical-device-risk-review.md` covers the connected devices V-10 and V-11 manage · `../02-framework-crosswalk/hipaa-hitech-hitrust-nist-mapping.md` maps R-12 to its citations
