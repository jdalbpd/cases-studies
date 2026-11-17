---
title: Targhino
subtitle: Redesigning a mandatory regulatory procedure without removing the friction the law requires
role: Senior Product Designer, sole contributor
type: Concept Project
tools:
  - Figma Make
  - NEXIA Design System
tags:
  - regulatory-compliance
  - service-design
  - govtech
  - data-minimization
  - design-systems
status: prototype
date: 2026-08
summary: A redesign of Italy's new electric scooter registration procedure. It keeps the checks the law requires, removes the friction it does not, and treats rejection, review and failure states as core design work.
---

# Targhino

Product Designer · Concept Project

---

## Impact and metrics (estimated)

Nothing in this section is measured. Targhino is a concept project with no live users and no access to the real platform's data. The numbers below are hypotheses built from public benchmarks.

The benchmarks come from two secondary sources: a UX consultancy article and a KYC vendor's blog. The consultancy reports that up to 60% of users abandon digital onboarding before identity verification is done, and that asking for identity document uploads can cut conversion by around 29%. The vendor describes a "good" KYC conversion rate as 60% to 90%, depending on the sector. Vendors have a reason to publish high drop-off figures, and none of this comes from a government service. I use it only to set a reasonable range.

| Metric | Where the design acts | Working hypothesis |
| --- | --- | --- |
| Completion rate by applicant profile (adult EU, minor, non-EU, business) | The conditional tree shows only the documents that apply to that profile | 75% or more, the upper half of the vendor range, because users are motivated and the procedure is mandatory |
| First-pass approval rate (approved without any correction) | Each field explains why it is asked, before submission | Higher than the real procedure's rate. I could not find that rate published, so I set no number |
| Correction recovery rate (rejected applicants who resubmit successfully) | A rejection points to the failing field, with no restart | Most rejected applicants recover. This is the metric I would watch first |
| Time from first screen to payment receipt | No duplicate data entry, no manual receipt upload | Shorter than the current multi-system path. The baseline is unmeasured |
| Fields and documents shown per profile, against the current procedure | Conditional blocks instead of one flat list | Not counted yet. It is the one figure I can compute from the prototypes without users |

## Context

In 2026 Italy made a personal identification tag, the "targhino" (officially the contrassegno identificativo), mandatory for privately owned electric scooters. Liability insurance becomes mandatory from July 2026. The tag is tied to the owner's tax code, not to the scooter. Fines run from €100 to €400, and up to €800 plus seizure when technical requirements are not met. It is a national rule, not a city one.

I found the project through a data ethics course and traced the real procedure from start to finish. It runs across three disconnected systems: an information portal, a generic payment module, and a case management system. The applicant downloads one of two PDF forms (one for adults, one for minors), fills it in outside the platform, and uploads it. The payment is found by searching a fee code by hand. The receipt is downloaded and uploaded again in a third system. The result arrives by email. Then the applicant books an in-person appointment at a motorization office, where agendas were full in the weeks before the rule took effect.

One community blog documented, with a screenshot, a section meant to explain how to request the tag that uses the word "cancel" at a key point. That is a real example of the interface working against its own purpose.

The problem is structural, not cosmetic. Every applicant gets the same undifferentiated list of documents, whatever their age, citizenship or legal status. Payment and application feel like two unrelated events. Nobody classified which data the law requires and which data the form simply asks for.

### Constraints

This is a self-directed project. There was no client brief, no access to real applicants, and no way to test against the live platform. The research is real and public. Every decision was checked against documented friction and against GDPR text, not against users.

The official procedure asks the applicant to sign in with the national digital identity (SPID or CIE). I assume this step exists and I do not prototype it. Four edge cases are documented and left out of scope: filing through a delegated third party, legal guardians who are not parents, tag renewal or expiry, and non-resident applicants.

## Product Reality

### Who carries the risk

The applicant carries the legal risk. A wrong "you are fine" can end in a fine. A slow "not yet" only costs time. That asymmetry shaped the status labels. The product separates submitted, under review, approved and active, and it never shows "active" before the physical tag is collected.

### Friction kept on purpose

- Identity check through the official channel. It is a legal requirement, and I assume it without designing it.
- Guardian data and signature for applicants aged 14 to 17. The real procedure requires it.
- One migratory document for non-EU applicants, because eligibility depends on it.
- Payment before review. The real procedure works in this order and I did not change it. What happens to the fee after a rejection is an open question (see below).
- In-person pickup of the physical tag.

### Friction removed

- Three disconnected systems became one flow with a persistent state.
- The manual receipt download and re-upload disappeared. The receipt is generated inside the flow.
- One flat document list became conditional blocks, based on age, citizenship and applicant type.
- A silent email result became three visible states: approved, rejected, under review.
- A rejection stopped being a dead end. It points to the failing field.

### Data protection

I read GDPR as a design input, not as a final check. Article 5(1)(c) (data minimization) drove every required, conditional and optional label. Articles 12 to 14 (transparency) drove the one-line reason shown next to each field. Article 25 (data protection by design) is the argument for putting the conditional tree in the architecture. The legal basis for most of this data is probably legal obligation under Article 6(1)(c), not consent. That matters: a field cannot be called "optional" in the copy if the law requires it. I read the regulation myself. A privacy lawyer has not reviewed it.

### Business reality

The procedure is a public service, so the buyer depends on the model. A public agency could adopt the design as a service redesign. A third-party assistance product would need official sign-in and delegation rules that I have not solved. A B2B layer for fleet operators who register many scooters at once is supported by the batch registration in the design. Which of these is real depends on access to the official platform, which I do not have. I have no price or willingness-to-pay data.

### What I would do differently as a real product

First, confirm how a third party can connect to the official platform at all, and get a privacy review of the data classification. Second, test the rejection and review states with real applicants before anything else. Those are the states where trust is lost.

## Worst-case states

The happy path is the easy part of a regulated flow. This table lists the states that decide whether people trust it, and it says plainly which ones I designed.

| Situation | What the system does | Status |
| --- | --- | --- |
| A document is rejected (unreadable, or does not match the data) | Shows the specific reason in plain language, links to the failing field, keeps all other data | Designed and prototyped |
| The same document is rejected a second time | Proposal: stop the loop and offer an assisted path, such as an appointment at the office | Proposed, not prototyped |
| Application stays under manual review | A dedicated "under review" state with a placeholder estimate. The real review time is unknown | State designed. Behavior after a missed estimate is open |
| Payment fails | Keeps all onboarding data, allows a retry, disables "back" during the transaction to avoid double payment | Designed. Server-side duplicate protection is an engineering task |
| Application is rejected after payment | The fee and any refund path are not defined, because the sources do not say | Open |
| Upload times out or the session expires mid-application | Progress survives going back and a failed payment. Timeouts and expiry are not specified | Open |
| Offices have no free appointments | Suggests another nearby office or the next available dates | Designed and prototyped |

## What I designed

### Data classification before screens

I built a taxonomy of every field the procedure could ask for. It has five categories: applicant identity, applicant status, vehicle, payment and contact. Each field is marked required, conditional or optional, with a reason. The conditional branches in that taxonomy became the navigation logic of the onboarding.

### A conditional tree, not one flat form

The flow asks how many scooters are registered, then whether the applicant is a person or a business. For a person, age and citizenship decide what comes next. An applicant aged 14 to 17 sees the guardian step. An adult EU citizen never does. A non-EU applicant picks one migratory document out of three, not all three. This was the decision with the most effect on the project.

### Payment inside the same flow

The amount is calculated and shown line by line, including the multiplier when several scooters are registered together. The payment reference is generated from data the system already has. The receipt appears in the flow. Nothing leaves the user's hands and comes back.

### Confirmation with three states

Approved, rejected and under review each have their own screen and next action. For an approved application, the user picks an office and a time. If the office is full, the system suggests alternatives instead of leaving the user stuck.

### Status as a living view

The real procedure ends at pickup. The status view keeps going. It shows the state of the tag, the state of the insurance link and early warnings before the insurance expires, because the fine risk does not end with the application.

### Transfer and cancellation with less data

When a scooter is sold, the seller cancels their own tag and gets a reference code. The buyer starts an independent application with that code. I considered linking the two applications through the buyer's email and rejected it. It would make one person handle another person's data without any need.

### A fines history that is documented, not designed

I considered a history of fines and checks in the status view. I did not design it. There is no evidence that this data exists in the real procedure, and a location-linked enforcement log carries the highest regulatory exposure in the project, close to behavioral profiling. It is documented as a data decision only: what would be stored, why, and what control the user would have over visibility and retention.

## Tools

Figma Make, NEXIA Design System (extended, not rebuilt). Five Italian-language, mobile-first prototypes: onboarding, payment, confirmation, status, and transfer.

## What I learned

Data minimization is not a paragraph in a privacy notice. It is a branching decision that has to exist before the first screen. The conditional tree, more than the visual layer, is where the ethics of this project sit.

I also learned to read a compliance flow from its worst states backwards. Writing the table above showed me three gaps I had not seen while designing the happy path: the refund after a rejection, the second rejection, and the session timeout. Naming them in the case study is more useful than hiding them. I also stopped treating all friction as the enemy. Some of it is the law, and the design job is to keep that part clear and remove the rest.