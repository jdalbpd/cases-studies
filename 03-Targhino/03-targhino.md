---
title: "Targhino"
subtitle: "Redesigning a national compliance procedure for electric scooter riders in Italy, with data minimization as the load-bearing principle"
role: "Senior Product Designer — sole contributor"
type: "Concept Project"
tools: ["Figma Make"]
tags: ["concept-project", "govtech", "regulatory-ux", "data-ethics", "design-systems"]
status: "prototype"
date: August, 2026.
summary: "An end-to-end redesign of Italy's new electric scooter registration procedure, built around GDPR-grounded data minimization rather than faster form-filling."
---

# Targhino

## Context

In 2026, Italy introduced a new legal requirement for private electric scooters: every owner must obtain a personal identification tag — the "targhino" — linked to their tax code, not to the vehicle itself, along with mandatory liability insurance. The rule is a reasonable public-safety response to over a million unregistered scooters on Italian streets. Its digital implementation is not.

I came across this while taking a data ethics course and decided to trace the actual procedure end-to-end, rather than assume it was well designed because it was mandatory. What I found was a request that spans three disconnected systems: a general information portal, a generic payment module, and a separate case-management system — stitched together with downloadable PDF forms and manual re-uploads. One community blog documented, with a screenshot, a section meant to explain how to *request* the tag instead using the word "cancel" at a key point — a real, not hypothetical, instance of the interface working against its own purpose.

This project treats that procedure as a systems problem: what is the minimum set of data this process actually needs, who needs to provide it and when, and how does a service built on that minimum look and feel — rather than a faster version of the same form.

## Problem statement

The surface-level framing — "this government form is confusing" — undersells the actual problem. The friction isn't cosmetic; it's structural. The current procedure never classifies which data is legally required versus merely requested "to be safe," never adapts to the applicant's actual situation (minor vs. adult, EU vs. non-EU citizen, individual vs. business) before asking for documents, and separates payment from the request it belongs to so completely that a successful payment and a completed application are, from the user's point of view, two unrelated events.

The real problem is a service designed with no information architecture behind it — every applicant profile is handled by the same undifferentiated wall of text and file uploads, regardless of what actually applies to them. Fixing the copy without fixing that structure would still leave people uploading documents they don't need.

## Constraints

This is a self-directed project with no client brief, no access to real applicants, and no way to usability-test against the live government platform. The regulatory research is real — sourced directly from the Portale dell'Automobilista, government-published decree summaries, and Italian mobility/insurance publications covering the rule as it rolled out — but every design decision was validated against that documented friction and against GDPR text, not against user testing. There is no validation loop with real users behind any of the flows in this project, and I'm naming that plainly rather than implying otherwise.

A second constraint was deliberate scope discipline: the regulation itself opens up several edge cases (delegated third-party filing, non-parental legal guardianship, tag renewal/expiry, non-resident applicants) that this project documents but does not design for, to keep the core system legible rather than exhaustive.

## Process & decisions

**Data classification as the starting point, not a copy pass.** Before any screen existed, I built a data taxonomy for every field the real procedure could plausibly request, grouped by category (identity, applicant status, vehicle, payment, contact), each tagged required / conditional / optional with a rationale. I rejected treating this as a documentation exercise done after the UI — the conditional branches this taxonomy produced (age, citizenship, applicant type) became the actual navigation logic of the onboarding flow, not an afterthought layered on top of static screens.

**A four-branch conditional tree instead of one flat form.** The real procedure presents every possible document requirement to every applicant at once. I rejected that in favor of a decision tree: number of scooters being registered → applicant type (individual/business) → for individuals, age and citizenship → each branch surfacing only the fields and documents that actually apply. A 14–17-year-old applicant sees a parental-responsibility step; an adult EU citizen never does. This was the single highest-leverage decision in the project — it's the direct, structural answer to the "wall of undifferentiated requirements" problem named above.

**Removing the pay-then-re-upload cycle.** The current system requires the applicant to pay in one system, download a receipt, and manually re-upload it in a third, unrelated system to complete their application. I rejected replicating that pattern even in simplified form — the redesigned payment flow generates the payment reference and the receipt automatically within the same flow, with no file leaving the user's hands and coming back.

**Turning administrative silence into a visible, recoverable state.** The real confirmation step is an email with a pass/fail outcome and no further detail — a rejection gives the applicant no way back into their own application. I rejected a simple "approved/rejected" binary in favor of three explicit states (approved, rejected, under review), where rejection links directly back to the specific field or document that failed, instead of forcing a restart.

**Treating the transfer/cancellation case as a data-minimization exercise, not a feature to skip.** The real system offers no assisted path when a scooter changes hands: the seller cancels, the buyer starts over, with no link between the two. I considered a more "helpful" version where the seller enters the buyer's email to link both applications, and rejected it — it would mean one party handling another party's personal data for no functional necessity. The tag holder instead cancels their own registration and receives a reference code to hand off; the buyer starts an independent application using that code. Less connected, but no personal data crosses between two people who don't need to share any.

**Deliberately not designing a fines/enforcement history feature.** Early in the project I considered a violation/zone-monitoring history as part of the ongoing status view. I rejected building it out as a designed flow — there's no evidence this data exists in the real procedure today, and a feature that logs a user's location-tied enforcement history carries meaningfully more regulatory exposure (verging on behavioral profiling) than anything else in this project. It's documented as a data-architecture decision — what would be logged, for what purpose, with what user control over visibility and retention — without being given screens, so the reasoning is on record without inventing a speculative feature.

**GDPR as design input, not a compliance afterthought.** Three articles shaped concrete decisions rather than staying abstract: Article 5(1)(c) (data minimization) underwrote every required/optional classification in the taxonomy; Articles 12–14 (transparency, plain-language information) shaped the requirement that every field explain, in one line, why it's being asked for; Article 25 (data protection by design) is the argument for why the conditional tree exists at the architecture level rather than as a UI convenience.

## Artifacts

- A complete data taxonomy across five categories (applicant identity, applicant status, vehicle data, payment, contact), each field marked required / conditional / optional with rationale.
- A conditionality tree covering: applicant type, age-triggered parental consent (14–17 range), EU/non-EU citizenship documentation branching, batch registration for multiple scooters, and the transfer/cancellation sub-flow.
- Screen-grouping maps for five flows: onboarding & data classification, payment, confirmation, ongoing status, and transfer/cancellation.
- Five Figma Make prototypes (Italian-language interface, mobile-first), one per flow, built as an extension of the NEXIA design system rather than as new components.
- A documented before/after comparison, flow by flow, tracing each redesigned decision back to a specific, sourced friction point in the real Portale dell'Automobilista procedure.

## Outcomes

This is a concept project: there is no live product, no deployment, and no usage data. What it produced is a structurally complete, GDPR-grounded redesign of a real, currently-live government procedure — validated against documented friction in that procedure, not against user testing. Any claim about reduced applicant anxiety, completion time, or error rates would be a hypothesis, not a result, and I'm treating it as one rather than stating it as fact.

## Product Reality

**Business reality.** This project has no commercial buyer in its current form — it's self-initiated, not commissioned. If it existed as a real product, the plausible business case is a B2C compliance-assistance service (a paid or freemium layer over a free government process, similar to how private services already exist around PagoPA-based procedures in Italy), or a B2B layer for scooter-sharing/fleet operators who need to register many units at once and would value the batch-registration path built into this system. The risk it reduces for an individual user is financial (avoiding a €100–800 fine) and administrative (avoiding a rejected, restart-from-zero application); I don't have a defensible metric for either without real usage data, so I'm not inventing one.

**Operational reality.** A few real failure modes were designed for explicitly: a failed payment does not discard onboarding data already entered — the user resumes rather than restarts; a rejected application links back to the specific failing field rather than forcing a full resubmission; a booking attempt against a saturated UMC office schedule (a documented real-world problem in the weeks before the law took effect) surfaces alternative offices or dates instead of leaving the user stuck. I have not designed for concurrent-actor conflicts (e.g., a seller and buyer both acting on the same tag at once) or for what happens if a user abandons the flow mid-application and returns days later — both are open questions a real implementation would need to resolve.

**What I'd do differently as a real product.** With a real team and funding, the first thing I'd change is validation: none of the conditional logic in this project has been tested against an actual applicant, and edge cases in Italian bureaucracy tend to be more numerous and more particular than any solo research pass will surface. I'd also want direct confirmation from a legal/compliance advisor on the GDPR basis-of-processing distinction between the current form (largely legal-obligation-based, not consent-based) and my redesign's transparency copy, rather than relying on my own reading of the regulation.

## Learnings

Working through this project sharpened something I'd only partially internalized before: data minimization isn't a principle you apply at the end of a form, in a privacy notice — it's a branching decision that has to exist before the first screen does. The conditional tree, not the UI polish, is where the actual ethics of this project live, and that's the part I'd point to first if asked what's load-bearing here. I also became more comfortable naming what a project doesn't cover, and why, as a legitimate part of the deliverable — the "documented but out of scope" edges (delegated filing, guardianship, renewal, non-residents) taught me that scope discipline reads as maturity, not as a gap, when it's stated on purpose instead of discovered by omission.