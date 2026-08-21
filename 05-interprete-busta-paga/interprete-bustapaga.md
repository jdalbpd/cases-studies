---
title: "Intérprete di Busta Paga"
subtitle: "A concept tool that reads an Italian payslip and explains it in plain language, built to catch real, unclaimed fiscal errors"
role: "Product Designer"
type: "Concept Project"
tools: ["Figma", "Figma Make", "Claude"]
tags: ["concept-project", "fintech-adjacent", "design-systems"]
status: "concept"
date: null
summary: "A payslip-reading tool that verifies an Italian worker's cedolino against the underlying fiscal logic and explains what it finds in plain language."
---

# Intérprete di Busta Paga

**Product Designer · Concept Project**

---

## Context

This project started from a real case. A manual review of 19 monthly payslips (cedolini) for an Italian dependent worker revealed that a legally owed tax deduction (detrazione fiscale) had been missing for 11 consecutive months — a real, unclaimed error of roughly €2,600-2,900 in the employee's favor.

Most Italian workers have no accessible way to verify their own payslip. The math is opaque, the terminology is technical, and errors like this one go unnoticed for months or years. Intérprete di Busta Paga is a concept for a tool that reads a payslip, checks it against the underlying fiscal logic, and explains what it finds in plain language — built for someone with zero prior knowledge of the topic.

## What I designed

- A two-axis state model (data completeness vs. analysis result) that lets the system communicate partial or uncertain results without resorting to technical jargon or a binary pass/fail
- A dual-ingestion flow — photo/PDF with OCR, single or batch upload — with an in-place, field-level correction fallback, avoiding a separate "enter your data" screen that would add friction for a non-expert user
- A non-blocking urgency system for missing data: critical gaps are visually prominent but never interrupt navigation, a deliberate product principle carried through every screen
- A multi-language system (Spanish, English, Italian) that keeps official fiscal terminology untranslated across all languages, so users can still recognize those terms on their real payslip, while translating every explanatory layer around them
- An end-to-end flow mapped across six screens, from first upload through a multi-month historical comparison, with type-specific chart logic (line chart for net income, accumulated-area chart for severance pay/TFR, balance-first cards for leave/PTO)

## Tools

Figma, Figma Make, Claude

## Product Reality

**Business reality.** This tool has no obvious separate buyer — the person checking their own payslip is also the one who benefits directly, which points toward a consumer model: free or freemium access, monetized (if at all) through a paid tier for the fuller multi-month comparison and export features. The founding case makes the value proposition concrete rather than abstract: a real, unclaimed ~€2,600–2,900 found in eleven months of payslips is a stronger pitch than any feature list. A second distribution path exists inside the design itself — the exportable CAF checklist implies a possible B2B2C route where a CAF (consulente fiscale) or patronato adopts the tool as an intake aid for their own clients, which would make the CAF the buyer rather than the individual worker. Neither model is validated; no pricing, partnership, or channel has been tested with a real CAF or a real paying user.

**Operational reality.** A few things worth naming honestly, some of which are already flagged as open in the project's own working notes rather than new:

- **OCR misreads a real, legible document.** The two-axis state model limits the damage — a misread produces a "faltan datos" state rather than a silent wrong number — but real-world OCR reliability on genuinely unseen documents hasn't been proven yet; testing to date hasn't been fully blind. A false "anomalía" on a correct payslip, or a missed one on an actually-wrong payslip, is the failure mode that matters most, given the tool's entire premise is catching errors a human would miss.
- **A missing field with an ambiguous cause.** The system doesn't yet distinguish a field that's legitimately absent that month from one the OCR simply failed to read — both currently collapse to the same missing-data state, which risks either a false alert or a false reassurance depending on which direction the ambiguity resolves.
- **Sensitive personal data, handled without a specified retention policy.** A payslip photo contains real income and fiscal-ID data, stored specifically to enable month-over-month comparison. The case study doesn't yet specify how long that data is kept or how a user would delete it — a gap that matters more here than in a stateless single-use tool, precisely because the multi-month comparison is the differentiating feature.

**What I'd do differently as a real product.** I'd prioritize validating OCR reliability against genuinely blind, real-world documents before letting any user act on the missing-detrazione alert — a false positive costs someone a wasted trip to a CAF, but a false negative costs them the money the tool exists to recover, and that asymmetry matters. I'd also settle the distribution question (direct-to-worker vs. CAF-channel) early, since it changes who's accountable if the tool gets a real payslip wrong.

## What I learned

Designing for someone who understands nothing about the subject forced a discipline I didn't fully expect: nearly every state, label, and chart choice had to be re-justified from "does this help someone unfamiliar" rather than "does this look clear to me." The two-axis state model only became simple once I stopped trying to name every possible technical cause and instead asked what the user actually needed to do next.
