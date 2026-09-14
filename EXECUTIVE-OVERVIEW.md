# Security Risk Assessment — Executive Overview

**Northgate Behavioral Health Clinic**
Prepared by Ron Richardson

---

> **About this document.** Northgate Behavioral Health Clinic is a fictional organisation, created to demonstrate how a healthcare security risk assessment is done. No real patients, no real clinic, no real incident. The rules described are real.
>
> This overview is written to stand on its own. You do not need to read anything else to understand what was assessed, what it found, and what it means.

---

## In one paragraph

Northgate is a 45-person outpatient behavioral health clinic serving about 3,000 patients. This assessment looked at how well the clinic protects patient information — in its records system, its email, its building, and through the outside companies it works with. It found twelve problems. Two need attention immediately, eight need attention this year, and two can be planned. Most of them are not technology failures. They are missing routines, undocumented decisions, and workarounds that grew up because the proper way was slower than the busy way. The full fix costs somewhere between four and seven thousand dollars in the first year, and most of the important parts cost nothing at all.

---

## What "risk assessment" actually means here

It is not a scan, and it is not a test of whether someone could break in.

It is a structured look at three questions:

1. **What could realistically go wrong here?**
2. **How likely is each thing, and how bad would it be?**
3. **What should we do about it, and in what order?**

Federal healthcare privacy law requires clinics to do this, keep it current, and act on what it finds. Most small clinics do it once and never return to it. Northgate did exactly that — the clinic has an assessment on file, but it was written before the current records system was installed and nobody has looked at it since.

---

## Why this matters, in business terms

Three consequences follow from getting this wrong. They are not equally likely, and they are not equally visible.

### Patient trust

This is the one that matters most and gets measured least.

In most medical settings, the sensitive information is the diagnosis. **In behavioral health, the sensitive fact is often simply that someone is a patient at all.** A person receiving treatment for depression, or for a substance use disorder, frequently has not told their employer, their family, or their neighbours. The clinic's most basic promise is that they do not have to.

That promise is broken in small, quiet ways long before anything a lawyer would call a breach. A waiting-room sign-in sheet where each person reads the names above theirs. A reception screen angled toward the seating area. A scheduling call taken at the front desk within earshot. An appointment reminder text that names the clinic, arriving on a phone someone else in the household can see.

Nobody files a complaint about these. People simply stop coming, and do not say why. For a behavioral health clinic, that is both a clinical harm and a revenue problem, and neither shows up in any report.

### Regulatory exposure

Federal regulators investigate clinics after a complaint or after a breach report. What they ask for first is the risk assessment and the record of what was done about it.

In February 2026, a substance use disorder treatment provider settled with federal regulators after a phishing email compromised a staff member's mailbox, exposing information on about 2,000 patients. The settlement was $103,000 plus two years of federally monitored corrective work.

The detail worth sitting with: the regulator's finding was **not** that the clinic had weak passwords, or no encryption, or a poorly designed network. It was that the clinic had not done a proper risk assessment. That was the whole finding.

Northgate is the same kind of provider, of similar size, with the same gap and the same unprotected email.

### Operational disruption

An outpatient clinic that loses access to its schedule and its charts does not operate that day. Patients are turned away. Clinicians cannot document. Billing stops.

Northgate's backups run every night and report success. Nobody has ever tried restoring from them. Until someone does, the clinic does not have a backup — it has a belief about a backup.

---

## What was found

Twelve issues, in plain terms.

### Deal with these now

**1 · Staff email is unprotected, and it is full of patient information.**
Everyone at the clinic emails about patients all day — referral questions, scheduling, insurance chases. That means mailboxes hold patient information whether or not anyone intended them to. Right now a stolen password is enough to open one, because there is no second check at login. This is exactly what happened to the provider in the settlement described above.

**2 · The clinic's risk assessment is out of date, and there is no plan attached to it.**
The existing assessment predates the current records system and does not cover telehealth. No one owns it, and no one has scheduled a review. This is the single most commonly cited problem in federal enforcement — and it is the cheapest of all twelve to fix.

### Deal with these this year

**3 · Front desk staff share logins.**
Several people use the same account across a shift. When something goes wrong, the clinic cannot say who did it — and "who accessed this record?" is the first question in every complaint and every investigation.

**4 · Laptops and USB drives are not encrypted.**
Encryption scrambles information so it is unreadable without a key. It matters enormously here for one reason: if an encrypted laptop is stolen, it generally is not a reportable breach at all. The same laptop unencrypted means notifying every affected patient, reporting to the federal government, and a permanent public listing. The clinic already owns this capability. It is switched off.

**5 · Everything is on one network.**
The security cameras, the thermostat, the printers, the smart TV in the group room and the patient guest Wi-Fi all share a network with the computers that open patient charts. Each of those devices is a small computer that somebody else updates — or doesn't. A problem with any one of them has a clear path to the records.

**6 · Nobody has established which confidentiality rules apply to substance use records.**
Records about substance use treatment can carry federal protections stricter than the usual healthcare privacy rules. Whether they apply to Northgate depends on specific facts about what services the clinic holds itself out as providing. **Nobody has ever answered the question.** The deadline for complying with the current version of that rule passed in February 2026. The fix is a written determination that takes about a day.

**7 · The waiting room gives people away.**
Reception screens face the seating area, the sign-in sheet is shared, and scheduling calls happen at the desk. See *Patient trust* above — in this setting, this is not a minor privacy point.

**8 · Access is not removed when people leave.**
There is no single checklist connecting a departure to the records system, email, building badge and remote access. The clinic uses per-diem clinicians and rotating interns, whose end dates are often vague, so accounts simply linger.

**9 · Nobody looks at the records system access logs.**
The system records who opened which chart. No one reviews it unless a patient complains. In a small community where staff and patients know each other, inappropriate curiosity is a realistic and recurring risk — and it is invisible without review.

**10 · Backups have never been tested.**
Covered above under operational disruption.

### Plan these

**11 · Faxing is error-prone and unlogged.**
Referrals and records requests go out by fax, with numbers typed by hand from an outdated list, no second check, and no record of what was sent where.

**12 · The clinic does not have a complete list of its vendors.**
Northgate cannot currently say which outside companies handle patient information or which have signed the required agreements. Three companies that should have one do not — including the IT support firm, which has full administrative access to every computer in the building.

---

## The pattern worth noticing

**Most of these are not attacks.** Seven of the twelve involve no outsider at all. They are ordinary clinic operations under time pressure — a shared login because the queue is long, a fax sent from a stale number, an account nobody closed.

**The front desk carries more risk than any other position.** Three of the twelve sit at reception. It is the busiest, most interrupted, least trained position in the building, and it touches scheduling, intake paperwork, payments and fax. It is also where security rules most reliably get worked around, which is why the recommended fixes are designed to be *faster* than the workaround rather than just stricter.

**Very little of this is a technology problem.** Most of what the law requires is decisions, documentation and routines. The clinic already owns nearly all the technology it needs. It is largely switched off, unconfigured, or unreviewed.

---

## What to do, and what it costs

### First 30 days — under $500

Sign and date the assessment. Adopt the fix-it plan and put a name against each item. Switch on the second login check for email. Sign the three missing vendor agreements. Write the one-page determination about substance use records. Start an incident log. Move the reception screens and replace the shared sign-in sheet.

Most of this is decisions and paperwork. It closes the clinic's largest regulatory exposure.

### Days 31 to 90 — $500 to $1,500

Give every person their own login and turn off the shared ones. Turn on encryption across laptops and desktops. Build a leaver checklist. Start reviewing records access monthly. Actually test a backup restore. Run a practice phishing exercise.

Nearly all of this uses capability the clinic already pays for.

### Days 91 to 180 — $2,000 to $5,000

Separate the network so cameras, thermostats and guest Wi-Fi cannot reach clinical systems. Tighten the fax process. Check which vendors have remote access and remove what isn't needed. Run a practice incident exercise.

This is the only part that needs real spending.

### Then keep it going

Monthly access review. Quarterly account clean-up and phishing practice. Annual reassessment, backup test and training. Reassess whenever something material changes — a new system, a new site, a new service.

That last one is what failed before. The old assessment was not wrong when it was written. It was never revisited after the records system changed.

---

## The number that frames the decision

**Fixing everything: roughly $4,000 to $7,000 in the first year.**

**The settlement paid by a comparable clinic with the same gap: $103,000**, plus two years of federally monitored corrective work.

The comparison is not really about the penalty. It is that the corrective work regulators imposed on that clinic — do a proper risk assessment, write a plan, update the policies, train the staff — is almost exactly the first two phases of Northgate's plan.

**The clinic does this work either way.** Doing it now is cheaper, runs on the clinic's own schedule, and does not come with a public announcement.

---

## If you only do one thing this week

Sign and date the risk assessment, and adopt the remediation plan with a name against each item.

It costs nothing, takes an afternoon, and closes the exact gap that turned a phishing email into a six-figure settlement for a clinic much like this one.

---

## A closing note on why this was worth doing

It would be easy to read twelve findings as a poor report card. It isn't one.

Northgate is a clinic where people are busy doing clinical work, where the technology mostly works, and where nothing has gone visibly wrong. That describes most small healthcare organisations. The gaps here are not negligence — they are what accumulates when nobody's job is to look.

The value of an assessment like this is that it converts a vague, permanent background anxiety into twelve specific things with owners, dates and costs. Ten of the twelve can be closed for under fifteen hundred dollars.

The clinic's obligation is not to be perfect. It is to know where it stands and to act reasonably on what it knows. This document is the first half of that. The plan is the second.

---

*Fictional clinic, prepared as a demonstration of healthcare security and compliance work. Ron Richardson — CompTIA Security+, Per Scholas Cybersecurity, with prior clinical case management experience.*
