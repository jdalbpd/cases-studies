---
title: "Turismo Roma"
subtitle: "Concept project: a B2B trust layer that verifies licensed operators before they touch scarce inventory"
role: "Product Designer"
tools: ["Figma", "Figma Make", "Claude (AI-assisted)"]
tags: ["trust-architecture", "credential-verification", "b2b", "compliance", "exception-states", "design-systems"]
status: "concept"
date: "2026-11"
summary: "A concept for real-time credential verification in a B2B platform. A two-axis state model separates system failures from verification results, and graduated access limits abuse without blocking honest operators."
---

# Turismo Roma

A B2B platform has to decide, in real time, whether to trust the holder of a credential. If it trusts the wrong person, an impostor gets access to scarce inventory. If it distrusts the right person, an honest operator loses a working day. This project is a design for that decision, built as a concept from market research. There was no client and no access to production data.

The instance I worked on is Rome's licensed tour guides, the agencies that hire them, and official Colosseum tickets as the scarce inventory. The pattern is broader: verify an operator against an official registry, then tie what they can do to the result.

## Contents

- [Product Reality](#product-reality)
- [Trust architecture](#trust-architecture)
- [Exception states](#exception-states)
- [Real-time data constraints](#real-time-data-constraints)
- [Flows and screens](#flows-and-screens)
- [Design system](#design-system)
- [Outcomes](#outcomes)
- [Tools](#tools)
- [What I learned](#what-i-learned)
- [What I'd do differently as a real product](#what-id-do-differently-as-a-real-product)

## Product Reality

### Business reality

Why the product exists. Verifying a guide today is manual and informal. Unlicensed guides work next to licensed ones, and bots empty official ticket allocations within seconds. In 2026 the ticket problem reached Italy's competition authority (Antitrust) and its anti-corruption authority (ANAC).

What it solves. An agency gets a fast way to confirm a credential before relying on a guide. The platform also links ticket quota to verified status, so quota does not go to someone who should not hold it.

Risk it reduces. Two risks: impersonation (operating with no valid license) and overselling (quota assigned to the wrong person).

Business metric. The share of an agency's inventory handled by verified guides. I have not measured it. It is the number I would track first.

Buyer. The agency pays. The guide is a user, not a payer. Small and medium businesses are about 80% of the tour-software customer base, which matches a typical independent Roman agency. Existing booking tools run from free tiers up to about USD 300 a month, plus commissions of roughly 1% to 6%. None of them verify credentials. Attraction-side ticketing systems sell to institutions, not to the agencies waiting outside them. That gap is where this product sits.

### Operational reality

These are the failure modes I designed for first, before any visual work.

| Scenario | What the system does |
|---|---|
| Bad input (a typo in a license number) | Shows "No match". After 4 failed tries in 24 hours, adds a message about the official licensing process. It does not accuse anyone. The counter resets every 24 hours. |
| Registry unavailable | Shows a neutral "query failed" state. The guide keeps the last known status. The system re-verifies the next day. |
| Status changes mid-session | Open question. Every scan re-verifies, and the dashboard shows the date of the last check. A recheck at ticket-use time is left for engineering to decide. |
| Abandoned renewal | The grace window ends and quota drops to zero. |
| Expired license | Reduced quota for 15 days. A renewal case code keeps full access while the official process is still running. |
| Actors see different information | The registry result is the single source of truth. The tourist sees a simplified version of the same state. The platform never overrides the registry. |

## Trust architecture

The structure is familiar from fintech onboarding. This is an analogy for how I framed the problem. It is not production experience.

| In this product | Fintech equivalent |
|---|---|
| Agency onboarding with Partita IVA (Italian VAT number) | KYB, business verification |
| Guide check against the national tourist guide registry | KYC, credential check |
| Ticket quota per guide | Transaction or exposure limit |
| Grace window | Remediation period |
| Case code on a revoked license | Re-screening request |
| Internal log of failed lookups | Audit trail |

The central decision is a two-axis state model. Axis A is the query outcome: did the system reach the registry? Axis B is the license status: what did the registry say? Keeping them apart stops an outage from reading as "this guide is not licensed". That would be a false block caused by the platform, not by the person.

Strictness is not the same everywhere. Revoked and no-match states have no exceptions. Expired and suspended states get a grace window. A false block costs an honest guide a working day. A false pass lets an impostor sell. The access rules reflect that imbalance.

## Exception states

Five license states, each with its own severity, behavior, and way out.

| State | Severity | Access | Way out |
|---|---|---|---|
| Valid | Positive | Full | None needed |
| Expired | Mild | Reduced quota, 15-day window | Renew, or enter a renewal case code |
| Suspended | Moderate | Reduced quota, 2-day window | Resolve the suspension |
| Revoked | High | Full block | Enter a new case code, which triggers a fresh registry check |
| No match | Maximum | Full block | Re-check the data, or start the official licensing process |

Reduced quota is shown in the design as 200 tickets down to 50. That figure is an illustration, not real allocation data. The suspended window is shorter than the expired one on purpose. A suspension is the guide's most urgent problem. An expiry is often a missed deadline. If a window closes with no resolution, quota goes to zero and the state behaves like a block.

A case code never unlocks anything by itself. For a revoked license, it only triggers a new registry check. Access returns only if the registry confirms a valid license. How those codes are issued and validated belongs to backend engineering.

The "no match" copy points toward action without alarm: "No encontramos ningún registro con estos datos, te recomendamos verificar." A typo and an impersonation attempt look the same on the first try. The message has to work for both.

## Real-time data constraints

- The registry is the source of truth. The platform stores the last known state and the time of the last verification.
- During an outage, the guide keeps the last known state. The system retries the next day.
- A revocation can happen after the last check. Re-verifying on every scan and showing the last verification date reduces that gap. It does not remove it.
- Failed lookups are logged internally in v1: scanned identifier, time, and location when relevant. Escalation to a review team or a guides' association is planned for a later version.

Three assumptions are not validated. I do not know whether the registry exposes suspension and revocation as separate states. I do not know whether third parties can integrate with it. I do not know how fast status changes appear in it. The national registry does issue a digital card with a QR code, so a verification path exists. The rest needs a conversation with the registry's owner.

## Flows and screens

Five flows, designed as one product with one shared state system.

1. On-the-spot verification. QR or NFC scan, or manual search for people without camera access. One primary action, "scan again". Recovery actions only appear in states that need them.
2. Trust dashboard. An agency sees every guide it works with, grouped by severity so problems surface first. Each row shows the state, the last verification date, and available quota. The tax code is partly masked in the list and shown in full only on the profile.
3. Guide onboarding. Four fields: name, surname, tax code, license number. The result comes back instantly in the same state system.
4. Agency onboarding. Registration with Partita IVA, resolving to the same states.
5. Ticket availability panel. Read-only in v1. An agency's quota is the sum of its verified guides' individual quotas, so the total always explains itself. Only the Colosseum is functional. The other sites are placeholders.

Tourists get a simplified result with no recovery actions. Agencies get the full version.

## Design system

The visual language follows Design Italia, the design system used across Italian public administration, with an institutional blue and Titillium Web. The goal was for the product to look like part of the ecosystem it verifies against.

Two rules keep the color system honest. Severity colors are used only for license state and never mixed with the brand blue. The color scale for ticket availability is separate from the severity scale, so a low-quota guide never looks like a revoked one.

The system is documented through the state specification and one prompt per flow, with shared components for every state. I did not build a token pipeline for this project. That is a gap I would close first in a real handoff.

## Outcomes

This is a concept project, so there are no production results. These are the hypotheses I would test, and how I would measure each one.

| Hypothesis | Measure |
|---|---|
| Verification is fast enough to use on the spot | Time from scan to displayed state |
| Honest operators are rarely blocked by mistake | Share of blocks later reversed by a valid registry check |
| The grace window leads to regularization | Share of expired or suspended guides who resolve within the window |
| The retry limit separates typos from abuse | Failed lookups per credential, per 24 hours |
| Quota follows verified status | Share of agency quota assigned to verified guides |

## Tools

Figma, Figma Make, Claude (AI-assisted)

## What I learned

Reframing guide verification as an identity-trust problem was the most useful move. It gave me a known structure to work with: onboarding checks, limits, remediation, audit trail.

The harder part was the middle of the system. Valid and revoked are easy to design. Expired and suspended need rules that stay firm on abuse and still allow for ordinary administrative delay.

Writing the operational reality early changed the design. The query-failed state and the case-code exception both came from asking what happens when something goes wrong, before drawing screens.

## What I'd do differently as a real product

- Start with registry access: available fields, latency, and whether third parties can integrate. Several rules in this design depend on those answers.
- Test the 2-day and 15-day windows with real guides and agencies before fixing them.
- Replace the message-only response to repeated no-match attempts with a manual review queue.
- Add an immutable audit trail with a named reviewer for any quota override.
- Design the scan flow as a mobile experience. Scanning a badge in the field is a phone task, and this concept stayed on desktop.