---
title: "Turismo Roma"
subtitle: "Concept project — B2B trust and availability platform for Rome's tourism sector"
role: "Product Designer"
tools: ["Figma", "Figma Make", "Claude (AI-assisted)"]
tags: ["design-systems", "concept-project", "b2b", "trust-and-identity", "fintech-adjacent"]
status: "concept"
date: "2026-08"
summary: "A B2B platform that verifies licensed tour guides in real time and gives agencies visibility into official ticket availability, designed to counter guide impersonation and ticket scalping in Rome."
---

## Context

Rome received 27.7 million visitors in 2025. Growth continued into 2026, up 3.8% year-over-year. That volume surfaced two operational problems the tourism sector has not been able to solve on its own.

- **Guide impersonation.** Unlicensed guides operate actively, especially in high season. This undercuts licensed professionals and produces inconsistent experiences for tourists, sometimes fraudulent ones. The one direct precedent, GimmeGuide, is an Italian platform that admits only licensed guides and was presented to the Senate. It has limited territorial adoption and no dominant presence in Rome.
- **Digital ticket scalping.** Bots exhaust official Colosseum ticket allocations within seconds. This forces legitimate agencies and individual tourists into resale markets at inflated prices. The issue escalated to Italy's competition authority (Antitrust) and its anti-corruption authority (ANAC) in 2026.

Both problems share the same root cause. No reliable verification or access mechanism exists in an ecosystem where trust is handled manually, informally, or not at all.

**Market context.** The global tour-operator software market sits between USD 0.9 and 1.1 billion in 2026, growing at a double-digit CAGR. Adoption is 78% SaaS/cloud, and small-to-medium businesses make up 80.6% of the customer base. That profile matches a typical independent Roman agency closely. The dominant players (Bókun, Rezdy, Regiondo, TrekkSoft, FareHarbor) compete on generic tour inventory and booking. None of them address the identity-verification and availability problems specific to Rome. Local Italian software (SferaNET, X-Travel, SiteForTravel) covers backoffice and accounting, not experience operators. Attraction-side ticketing platforms (Tiqets, vivenu, ROLLER) sell timed-entry systems to institutions, not to the agencies and guides who depend on getting into that same inventory. That gap, a trust and availability layer for the professional demand side, is where this project sits.

**Scoping the audience.** The underlying needs split into two groups by buyer. One is a B2B toolset for agencies and guides: guide verification, ticket availability, a lightweight backoffice/CRM, WhatsApp integration, regulatory alerts. These live under one product with several modules, used by the same person every day. The other is a separate institutional tool for redistributing tourist flow across the city, sold to Roma Capitale or Zètema, with a different buyer and a different sales cycle entirely. This project scopes to the first group. A single, pitchable value proposition made more sense than a scattered set of concepts.

## What I designed

**MVP scope.** Guide verification and ticket availability form the core of the product. They have the clearest differentiation, the least direct competition, and a natural connection to fintech-style identity verification. A lightweight backoffice/CRM is documented as a future expansion module, not part of v1, since that segment is already served, if imperfectly, by existing players.

**A two-axis verification state system.** Instead of a single pass/fail check, verification separates *query outcome* (did the system reach the official registry?) from *license status* (what did it find?). This distinction matters in practice. A registry outage should never read as "guide not licensed." That is a system problem, not the guide's. Five license states each carry their own severity and access behavior:

| State | Severity | Access behavior |
|---|---|---|
| Valid | Positive | Full access |
| Expired | Mild | Reduced quota, 15-day grace window |
| Suspended | Moderate | Reduced quota, 2-day grace window |
| Revoked | High | Full block, requires a new official inquiry via case code |
| No match | Maximum | Full block, escalating messaging after repeated attempts |

**A graduated access model, not a binary switch.** Expired and suspended guides don't lose access outright. They keep a reduced ticket quota (illustrated in the design as 200 down to 50) while a grace window runs. The suspended window is shorter on purpose, 2 days against 15 for expired. The reasoning: a suspension is the guide's own most urgent problem to fix, while an expiration is often just administrative oversight. An active-renewal case code lets a guide who already started the process keep full access past the 15-day mark. That way, the system doesn't penalize someone who is waiting on the administration, not on their own inaction. If the window closes with no resolution, the quota drops to zero. At that point it works the same as a hard block.

**A non-accusatory path out of "no match."** Instead of a dead end, repeated failed lookups (4 attempts within 24 hours) surface a message pointing toward the official licensing process, without accusing anyone of impersonation. The attempt counter resets every 24 hours, so a legitimate guide who mistypes their own credentials, or hits a system fault, isn't punished permanently for it.

**Five core flows**, designed as one coherent product instead of five separate apps:
1. **On-the-spot verification**: QR/NFC scan or manual lookup, resolving instantly to one of the six states above.
2. **Trust dashboard**: an agency's aggregate view of every guide it works with, grouped by severity so issues surface first.
3. **Guide onboarding**: registration verified instantly against Italy's national tourist guide registry, the Elenco Nazionale delle Guide Turistiche. That registry already issues a QR-based digital tesserino, real infrastructure this design builds on rather than around.
4. **Agency onboarding**: registration verified through Partita IVA (Italian VAT number), resolving to the same state system.
5. **Ticket availability panel**: read-only in v1, aggregating each agency's real quota as the sum of its verified guides' individual allocations, using the Colosseum as the pilot site.

**Visual language.** The interface borrows from Design Italia, the official design system used across Italian public administration sites, including the Ministero del Turismo and the national electronic ID platform. The goal was for the product to read as part of the same trusted ecosystem it verifies against. Not as a third-party startup layered on top of it.

## Tools

Figma, Figma Make, Claude (AI-assisted)

## What I learned

Treating guide verification as an identity-trust problem, the same logic used in fintech KYC flows, was the most useful reframe in this project. It's a pattern that transfers cleanly to a domain that has never used it before.

The harder design problem wasn't the clean states, like Valid or Revoked. It was building enough nuance into the graduated-access model so the system stays firm on abuse. No quiet exceptions for Revoked or No match. At the same time, it shouldn't punish ordinary administrative delay.

Some of the underlying assumptions are explicitly flagged as unvalidated in the project documentation: how quota gets distributed in practice, real renewal timelines, and whether the national registry even exposes suspension data to third parties. This was built from market research, not from access to the actual licensing infrastructure, so those gaps are honest ones.