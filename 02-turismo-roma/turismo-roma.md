---
title: "Turismo Roma"
subtitle: "Concept project — B2B trust and availability platform for Rome's tourism sector"
role: "Product Designer"
tools: ["Figma", "Figma Make", "Claude (AI-assisted)"]
tags: ["design-systems", "concept-project", "b2b", "trust-and-identity", "fintech-adjacent"]
status: "concept"
date: "2026-08"
summary: "A B2B platform that verifies licensed tour guides in real time and gives agencies visibility into official ticket availability — designed to counter guide impersonation and ticket scalping in Rome."
---

# Turismo Roma

**Product Designer · Concept Project**

---

## Context

Rome received 27.7 million visitors in 2025, with growth continuing into 2026 (+3.8% year-over-year). That volume has surfaced two operational problems the tourism sector has been unable to solve on its own:

- **Guide impersonation.** Unlicensed guides operate actively, particularly in high season, undercutting licensed professionals and producing inconsistent — sometimes fraudulent — experiences for tourists. The one direct precedent, GimmeGuide (an Italian platform admitting only licensed guides, presented to the Senate), has limited territorial adoption and no dominant presence in Rome.
- **Digital ticket scalping.** Bots exhaust official Colosseum ticket allocations within seconds, forcing legitimate agencies and individual tourists into resale markets at inflated prices. The issue escalated to Italy's competition authority (Antitrust) and anti-corruption authority (ANAC) in 2026.

Both problems share the same root cause: no reliable verification or access mechanism exists in an ecosystem where trust is currently handled manually, informally, or not at all.

**Market context.** The global tour-operator software market sits between USD 0.9–1.1 billion (2026), growing at a double-digit CAGR, with 78% SaaS/cloud adoption and small-to-medium businesses representing 80.6% of the customer base — a close match for a typical independent Roman agency. The dominant players (Bókun, Rezdy, Regiondo, TrekkSoft, FareHarbor) compete on generic tour inventory and booking, not on the identity-verification and availability problems specific to Rome. Local Italian software (SferaNET, X-Travel, SiteForTravel) covers backoffice/accounting, not experience operators. Attraction-side ticketing platforms (Tiqets, vivenu, ROLLER) sell timed-entry systems to institutions, not to the agencies and guides who depend on getting into that inventory. That gap — a trust and availability layer for the professional demand side — is where this project sits.

**Scoping the audience.** The underlying needs split into two groups by buyer: a B2B toolset for agencies and guides (guide verification, ticket availability, lightweight backoffice/CRM, WhatsApp integration, regulatory alerts — one product, several modules, same daily user) and a separate institutional tool for redistributing tourist flow across the city (sold to Roma Capitale / Zètema, a different buyer and sales cycle entirely). This project scopes to the first group, prioritizing a single, pitchable value proposition over a scattered set of concepts.

## What I designed

**MVP scope.** Guide verification and ticket availability form the core — the clearest differentiation, the least direct competition, and a natural bridge to fintech-style identity verification. A lightweight backoffice/CRM is documented as a future expansion module rather than part of v1, since that segment is already well served (if imperfectly) by existing players.

**A two-axis verification state system.** Rather than a single pass/fail check, verification separates *query outcome* (did the system reach the official registry?) from *license status* (what did it find?). This matters in practice: a registry outage should never read as "guide not licensed" — that's a system problem, not the guide's. Five license states carry their own severity and behavior:

| State | Severity | Access behavior |
|---|---|---|
| Valid | Positive | Full access |
| Expired | Mild | Reduced quota, 15-day grace window |
| Suspended | Moderate | Reduced quota, 2-day grace window |
| Revoked | High | Full block, requires a new official inquiry via case code |
| No match | Maximum | Full block, escalating messaging after repeated attempts |

**A graduated access model, not a binary switch.** Expired and suspended guides don't lose access outright — they keep a reduced ticket quota (illustrated in design as 200 → 50) while a grace window runs. The suspended window is intentionally shorter (2 days) than the expired one (15 days), on the logic that a suspension is the guide's own most urgent problem to resolve, while an expiration is often administrative oversight. An active-renewal case code lets a guide who's already mid-process keep full access past the 15-day mark, so the system doesn't penalize someone waiting on the administration rather than their own inaction. If the window closes with no resolution, quota drops to zero — functionally equal to a hard block.

**A non-accusatory path out of "no match."** Rather than a dead end, repeated failed lookups (4 attempts within 24 hours) surface a message pointing toward the official licensing process, without asserting impersonation. The attempt counter resets every 24 hours to avoid permanently penalizing a legitimate guide who mistyped their own credentials or hit a system fault.

**Five core flows**, designed as one coherent product rather than five disconnected apps:
1. **On-the-spot verification** — QR/NFC scan or manual lookup, resolving instantly to one of the six states above.
2. **Trust dashboard** — an agency's aggregate view of every guide it works with, grouped by severity so issues surface first.
3. **Guide onboarding** — registration verified instantly against Italy's national tourist guide registry (Elenco Nazionale delle Guide Turistiche), which already issues a QR-based digital tesserino — a real piece of infrastructure this design deliberately builds on rather than around.
4. **Agency onboarding** — registration verified via Partita IVA (Italian VAT number), resolving to the same state system.
5. **Ticket availability panel** — read-only in v1, aggregating each agency's real quota as the sum of its verified guides' individual allocations, using the Colosseum as the pilot site.

**Visual language.** The interface deliberately borrows from Design Italia, the official design system used across Italian public administration sites (including the Ministero del Turismo and the national electronic ID platform). The goal was for the product to read as part of the same trusted ecosystem it verifies against, rather than as a third-party startup layered on top of it.

## Tools

Figma, Figma Make, Claude (AI-assisted)

## What I learned

Treating guide verification as an identity-trust problem — the same logic used in fintech KYC flows — was the most useful reframe in this project; it's a pattern that transfers cleanly to a domain that has never applied it. The harder design problem wasn't the "clean" states like Valid or Revoked — it was building enough nuance into the graduated-access model that the system stays firm on abuse (no quiet exceptions for Revoked or No match) without punishing ordinary administrative delay. Several of the underlying assumptions — quota distribution logic, real renewal timelines, whether the national registry exposes suspension data to third parties — are explicitly flagged as unvalidated in the project documentation, since this was built from market research rather than access to the actual licensing infrastructure.