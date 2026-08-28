---
title: Turismo Roma
subtitle: Concept project. B2B trust and availability platform for Rome's tourism sector
role: Product Designer
tools:
  - Figma
  - Figma Make
  - Claude (AI-assisted)
tags:
  - design-systems
  - concept-project
  - b2b
  - trust-and-identity
  - fintech-adjacent
status: concept
date: 2026-08
summary: A B2B platform that verifies licensed tour guides in real time and gives agencies visibility into official ticket availability. Designed to counter guide impersonation and ticket scalping in Rome.
---

# Turismo Roma

**Product Designer · Concept Project**

---

## Context

Rome received 27.7 million visitors in 2025, and growth continued into 2026 (+3.8% year-over-year). That volume surfaced two operational problems the tourism sector has not been able to solve on its own:

- **Guide impersonation.** Unlicensed guides operate actively, particularly in high season. They undercut licensed professionals and produce inconsistent, sometimes fraudulent, experiences for tourists. The one direct precedent, GimmeGuide (an Italian platform that only admits licensed guides, presented to the Senate), has limited territorial adoption and no dominant presence in Rome.
- **Digital ticket scalping.** Bots exhaust official Colosseum ticket allocations within seconds. This forces legitimate agencies and individual tourists into resale markets at inflated prices. The issue reached Italy's competition authority (Antitrust) and anti-corruption authority (ANAC) in 2026.

Both problems share the same root cause: no reliable verification or access mechanism exists in an ecosystem where trust is currently handled manually, informally, or not at all.

**Market context.** The global tour-operator software market sits between USD 0.9 and 1.1 billion in 2026, growing at a double-digit CAGR. SaaS/cloud adoption reaches 78%, and small-to-medium businesses represent 80.6% of the customer base, close to a typical independent Roman agency. The dominant players (Bókun, Rezdy, Regiondo, TrekkSoft, FareHarbor) compete on generic tour inventory and booking, not on the identity-verification and availability problems specific to Rome. Local Italian software (SferaNET, X-Travel, SiteForTravel) covers backoffice and accounting, not experience operators. Attraction-side ticketing platforms (Tiqets, vivenu, ROLLER) sell timed-entry systems to institutions, not to the agencies and guides who depend on getting into that inventory. That gap, a trust and availability layer for the professional demand side, is where this project sits.

**Scoping the audience.** The underlying needs split into two groups by buyer. One is a B2B toolset for agencies and guides: guide verification, ticket availability, a lightweight backoffice/CRM, WhatsApp integration, regulatory alerts, one product with several modules for the same daily user. The other is a separate institutional tool for redistributing tourist flow across the city, sold to Roma Capitale or Zètema, with a different buyer and sales cycle entirely. This project scopes to the first group. A single, pitchable value proposition beats a scattered set of concepts.

## What I designed

**MVP scope.** Guide verification and ticket availability form the core. They offer the clearest differentiation, the least direct competition, and a natural bridge to fintech-style identity verification. A lightweight backoffice/CRM is documented as a future expansion module, not part of v1, since that segment is already served, if imperfectly, by existing players.

**A two-axis verification state system.** Instead of a single pass/fail check, verification separates *query outcome* (did the system reach the official registry?) from *license status* (what did it find?). This distinction matters in practice. A registry outage should never read as "guide not licensed." That's a system problem, not the guide's. Five license states carry their own severity and behavior:

| State     | Severity | Access behavior                                           |
| --------- | -------- | ----------------------------------------------------------|
| Valid     | Positive | Full access                                               |
| Expired   | Mild     | Reduced quota, 15-day grace window                        |
| Suspended | Moderate | Reduced quota, 2-day grace window                         |
| Revoked   | High     | Full block, requires a new official inquiry via case code |
| No match  | Maximum  | Full block, escalating messaging after repeated attempts  |

**A graduated access model, not a binary switch.** Expired and suspended guides don't lose access outright. They keep a reduced ticket quota (illustrated in design as 200 to 50) while a grace window runs. The suspended window is shorter on purpose (2 days versus 15 for expired), on the logic that a suspension is the guide's own most urgent problem to resolve, while an expiration is often just administrative delay. An active-renewal case code lets a guide who is already mid-process keep full access past the 15-day mark, so the system doesn't penalize someone waiting on the administration rather than on their own inaction. If the window closes with no resolution, quota drops to zero, which is functionally the same as a hard block.

**A non-accusatory path out of "no match."** Repeated failed lookups (4 attempts within 24 hours) don't end in a dead end. They surface a message pointing toward the official licensing process, without asserting impersonation. The attempt counter resets every 24 hours, so a legitimate guide who mistyped their own credentials or hit a system fault isn't penalized permanently.

**Five core flows**, designed as one coherent product, not five disconnected apps:

1. **On-the-spot verification.** QR/NFC scan or manual lookup, resolving instantly to one of the six states above.
2. **Trust dashboard.** An agency's aggregate view of every guide it works with, grouped by severity so issues surface first.
3. **Guide onboarding.** Registration verified instantly against Italy's national tourist guide registry (Elenco Nazionale delle Guide Turistiche), which already issues a QR-based digital tesserino. This is real infrastructure the design deliberately builds on, not around.
4. **Agency onboarding.** Registration verified via Partita IVA (Italian VAT number), resolving to the same state system.
5. **Ticket availability panel.** Read-only in v1. It aggregates each agency's real quota as the sum of its verified guides' individual allocations, using the Colosseum as the pilot site.

**Visual language.** The interface borrows from Design Italia, the official design system used across Italian public administration sites, including the Ministero del Turismo and the national electronic ID platform. The goal: the product should read as part of the same trusted ecosystem it verifies against, not as a third-party startup layered on top of it.

## Tools

Figma, Figma Make, Claude (AI-assisted)

## Product Reality

**Business reality.** The buyer is the agency, not the tourist or the guide. An agency owner or operations lead decides whether to route guide checks and ticket-quota visibility through this platform instead of doing both informally, which is what most agencies do today. The economic argument is risk and revenue protection, not growth. Working with an unlicensed guide is a reputational and potentially legal exposure the agency currently has no reliable way to check. A sold-out ticket allocation the agency didn't see coming means lost bookings it can't recover mid-season. Given the market context above, SMBs at 80.6% of the customer base and 78% SaaS/cloud adoption, a per-agency subscription tiered by guide count is a plausible model. That's a hypothesis from market data, not a validated price or willingness to pay. I don't know what an agency would actually pay, or how that compares to the cost of verifying guides manually today.

**Operational reality.** Three failure modes are worth naming beyond the registry-outage handling already built into the state system:

- **Stale ticket data.** The availability panel is read-only in v1 and aggregates verified guides' quotas. If the national registry or the Colosseum system updates slower than real sales move, an agency could see quota that no longer exists. The design doesn't yet specify a staleness indicator or a refresh guarantee.
- **A guide disputes their own state.** The system separates query failure from license status cleanly, but there's no designed path for a guide who believes a "Revoked" or "Suspended" reading is simply wrong, a registry data error rather than a real sanction. Right now the only route back in is the same official case-code process used for active renewals, and that may not fit a dispute at all.
- **Case-code abuse.** The active-renewal case code exists to protect guides genuinely mid-process from losing access at day 15. The design doesn't specify how a case code gets verified as real and current. An unverified or expired code accepted at face value would quietly reopen the exact loophole the grace-window model was built to close.

**What I'd do differently as a real product.** I'd validate willingness to pay and actual registry data-access terms before building further. The whole quota and verification model assumes the national registry will expose suspension and expiration data to a third party, and I don't know if that's actually permitted. I'd also design the dispute path before shipping the license-state system. A false "Revoked" reading with no appeal is the kind of failure that erodes trust in the verification layer faster than any uptime problem would.

## What I learned

Treating guide verification as an identity-trust problem, the same logic used in fintech KYC flows, was the most useful reframe in this project. It's a pattern that transfers cleanly to a domain that has never applied it before. The harder design problem wasn't the clean states like Valid or Revoked. It was building enough nuance into the graduated-access model so the system stays firm on abuse (no quiet exceptions for Revoked or No match) without punishing ordinary administrative delay. Some of the underlying assumptions, quota distribution logic, real renewal timelines, and whether the national registry exposes suspension data to third parties, are explicitly flagged as unvalidated in the project documentation. This was built from market research, not from access to the actual licensing infrastructure.