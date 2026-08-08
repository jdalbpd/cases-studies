---
title: "Settly"
subtitle: "I designed the tool I needed when I arrived in Italy and it didn't exist."
role: "Product Designer (full cycle: strategy → architecture → system → high-fidelity prototype)"
product_type: "B2C SaaS"
stage: "MVP, in development"
market: "Italy"
structural_requirement: "Multilingual"
tools: ["Figma", "Miro"]
tags: ["product-strategy", "design-systems", "accessibility", "multilingual"]
status: "mvp"
date: "2025"
summary: "A multilingual product for managing Italy's residence-permit process, designed from first-hand navigation of the system's failure points."
---

# Settly

**I designed the tool I needed when I arrived in Italy and it didn't exist.**

| Product type | Current stage | Initial market | Structural requirement |
| :---: | :---: | :---: | :---: |
| B2C SaaS | MVP | Italy | Multilingual |

**Role:** Product Designer (full cycle: strategy → architecture → system → high-fidelity prototype)

**Tools:** Figma (high-fidelity prototypes) · Miro (architecture and flows) · personal initiative

**Honesty note:** Settly is my own product, in MVP development. There is no post-launch data. The success indicators defined in this document are validation hypotheses, formulated with rigor, not retroactive metrics.

---

## Context

### I lived the problem before I designed the solution

This case study doesn't start with a client brief or a company OKR. It starts with a blank postal envelope, a form in Italian I didn't fully understand, and the certainty that if I made a mistake on that paper, my legal status in Italy would be suspended for months.

The *permesso di soggiorno per lavoro* — the residence permit for non-EU workers — is managed in Italy through a process whose user logic hasn't been updated in decades. The *kit postale*: an envelope that must contain exactly the right documents, in the right format, sent to the right address of the right prefecture. No clear guidance. No immediate confirmation. No second chance if you get it wrong.

> "I didn't find any native digital tool for this process. I found WhatsApp groups, outdated forums, and CAF advisors with limited availability and inconsistent results."

That experience built up enough understanding of the system — its rules, its inconsistencies, its points of maximum confusion — to identify where a digital product could intervene with real impact. Settly is my attempt to build it.

> **Why personal experience is valid as a research starting point**
> First-hand domain knowledge is a form of qualitative research. What makes it rigorous isn't whether it was lived or observed from outside, but whether it was analyzed with method. In this case, Italy's bureaucratic process has publicly documented rules, and the gap between those rules and the real user experience is verifiable. The diagnosis presented in this document rests on both pillars.

---

## Problem statement

### A system designed for officials, not for people

**The structural context**

Italy receives between 250,000 and 300,000 new *permesso di soggiorno* applications every year. The current process dates back to its 2007 form: the *kit postale*, a physical envelope system that must be mailed to the prefecture before an in-person appointment can be obtained. It predates widespread digitization and hasn't been replaced.

The consequences of application errors are disproportionate to their cause: incomplete documentation or an incorrectly filled form can generate delays of three to six months in regularization, with the resulting professional and personal uncertainty for the applicant.

| What the system offers today | What the user needs |
| :---- | :---- |
| Instructions in technical-bureaucratic Italian. | Knowing exactly which permit type applies to their situation. |
| Generic printed *kit postale* guidance, not adapted to permit type. | A document list specific to their case, not generic. |
| Informal support groups (Telegram, Facebook) maintained by immigrant communities. | Understandable instructions in their own language, not literal translations of bureaucratic text. |
| CAF advisors with variable availability and fees many users can't afford. | Confirmation they're doing it right before sending the envelope. |

**The three breaking points identified**

Based on my direct experience and analysis of existing touchpoints (prefecture portals, *kit postale* instructions, support group content), I identified three specific moments where the process fails most often and with the most serious consequences.

**Break 1 — Misclassification of permit type.** The application process varies significantly by permit type (*lavoro subordinato*, *attesa occupazione*, *studio*, *ricongiungimento familiare*, among others). A user who starts the process with the wrong type loses time, documentation, and in some cases their place in the appointment queue. The existing interface doesn't help classify: it assumes the user already knows what to apply for.

**Break 2 — The *kit postale* as a black box.** Preparing the postal envelope is the most critical and worst-documented step. The most common errors — wrong number of copies, missing *marca da bollo*, non-compliant photo format — are entirely preventable with clear information. But the official instructions are in legal Italian and don't distinguish between permit types. The result is that a significant share of users repeat this step at least once.

**Break 3 — Multilingualism as equivalence, not translation.** The language problem in this context isn't just translation: it's conceptual equivalence. Terms like *marca da bollo*, *nulla osta*, or *codice fiscale* have no direct equivalent in most applicants' languages. An app that translates literally reproduces the opacity of the original system. A useful app explains.

> **Central problem definition**
> Italy's *permesso di soggiorno* management system is designed for someone who already knows how it works. Settly exists to eliminate that information asymmetry: giving the foreign user the same level of process understanding as an experienced professional advisor, without needing intermediaries, in their own language.

---

## Constraints

### MVP scope decision

Italy's migration process has multiple user profiles with very different flows and complexities: the worker managing their own permit, the company managing its employees' permits, the immigration lawyer, the family going through reunification.

The decision to focus the MVP on the individual user — the person managing their own *permesso per lavoro* without a professional intermediary — wasn't arbitrary. It's the most frequent use case, the worst served by existing alternatives, and the one I can design best from first-hand knowledge. Adding additional profiles is a growth decision that requires its own validation.

> **MVP focus principle**
> A product that tries to serve every migration profile from day one serves none of them well. The *permesso per lavoro* for the individual user is the use case that defines the core architecture. Other cases will be designed once there's evidence the core works.

### No post-launch data

Settly is my own product, in MVP development. There is no post-launch data — no users to measure retention against, no support tickets to mine, no completion funnels to analyze. Every claim about impact in this document is a validation hypothesis, reasoned from documented current behavior, not a retroactive metric. That distinction is treated as load-bearing throughout the case study, not as a disclaimer at the end.

---

## Process & decisions

### The Migration Situation Profile (MSP) model

The biggest architecture risk was building a linear app on top of a process that branches. Permit type, province, contractual situation, and prior income history in the country determine which steps apply, which documents are needed, and which warnings are relevant. A flat architecture would have produced dozens of unmanageable flow variants.

The solution was to model the product around a **Migration Situation Profile (MSP)**: a data entity built during onboarding that dynamically determines which steps, documents, and alerts are relevant to that specific user. The system doesn't offer generic options — it derives the correct path from the user's actual situation.

### Onboarding as diagnosis

Settly's onboarding isn't a registration form. It's a structured classification conversation: 7 to 9 questions that build the MSP and let the system automatically determine the correct permit type, the applicable step sequence, and the specific documents needed. The user doesn't choose between permit types: the system infers from their situation.

This design has a deliberate cost: onboarding is longer than the consumer standard. The justification is that a three-minute onboarding that classifies correctly avoids hours of misdirected process. In a product where errors have real consequences, the time investment in initial diagnosis is justified.

### Complete states before designing components

Settly's design system was defined around one structuring question: what happens when we add permit type n+1, province n+1, or language n+1? If the system doesn't answer without structural redesign, it isn't a system — it's a collection of screens.

The functionally most critical components were specified with all their exception states before a single high-fidelity screen was produced. This process is slower at the start and significantly more efficient during implementation.

### Decision 1 — Simplification vs. legal fidelity

The project's most recurring tension: for the interface to be understandable, it needs to simplify. But in a context where an error has real legal consequences, simplifying incorrectly is more dangerous than not simplifying at all.

The resolution wasn't a compromise: it was a separation of content layers.

- **Primary level:** simple, action-oriented language. "What do you need to do right now, and how."
- **Secondary level (expandable):** the official source — exact wording of the decree or government instruction, with a direct link to the source portal.

The user who needs legal certainty can access it. The user who needs quick action isn't blocked by technical terminology. No simplification replaces the official source: it complements it. Settly is never the legal source of truth — it connects the user to it.

### Decision 2 — Linear progress vs. actual status

The bureaucratic migration process isn't linear: some steps run in parallel, others depend on third parties (the employer, the prefecture, the Comune), and can be interrupted for weeks and reactivated. A 0-to-100% progress bar would have been a false representation of the real process.

I designed a model of progress by independent modules, each with its own status, which can be in different phases simultaneously. The dashboard doesn't show "67% complete": it shows the exact status of each module and the next actionable step.

> **The case against the linear progress bar**
> A user who believes they're at 70% and discovers they must go back to an earlier step is more likely to abandon than one who always saw the process as multidimensional. Honest expectations about the process's complexity reduce abandonment when obstacles arise. The illusion of linearity is a trust debt that gets collected late.

### Decision 3 — Designing the external error state

Settly depends on systems that fail: prefecture portals going down, requirement changes without notice, contradictory responses between offices. The platform can't eliminate those errors. It can — and must — handle them with integrity.

I defined a specific design principle for external errors: Settly doesn't pretend the error doesn't exist, doesn't blame the user, and doesn't promise what it can't guarantee. The external error message always includes three elements: what happened, in understandable language; what the user can do right now; and what Settly will do when the situation changes.

> **External error microcopy example (prefecture portal unavailable)**
> "The Milan prefecture portal is currently unavailable. You can't book your appointment right now, but your application is saved and doesn't lose validity. We'll notify you when the system is back up, usually within 24–48 hours. In the meantime, you can keep preparing your documentation."

---

## Artifacts

Everything listed here exists.

### Navigation architecture

**Layer 1 — My process:** personalized view of the current status of the procedure. This is the real home screen. It doesn't show generic options: it shows the specific next actionable step for that user at that moment.

**Layer 2 — Documents:** dynamic repository of documents required for that MSP, with individual status (pending / ready / expired), instructions for obtaining them, and contextual alerts.

**Layer 3 — Guides and glossary:** permanent explanatory content. The glossary doesn't translate: it explains. "*Marca da bollo*" isn't "tax stamp" — it's "16 euros paid at a *tabaccheria*, not at the bank, following a specific procedure."

### System state map — contract with engineering

| State | Definition and design criterion | Communication principle |
| :---- | :---- | :---- |
| **Pending** | The user hasn't started this step yet. Visible, non-blocking. Includes time estimate and context for why it matters. | Inform without pressuring. |
| **In progress** | The user has started actions but hasn't completed the step. Always shows the exact pending sub-step, never just the general status. | Guide with precision. |
| **Needs attention** | Blocking action: expired document, missed appointment, requirement change. Visual interruption is justified only here. | Urgency without alarm. |
| **Completed** | Verified or confirmed. Shouldn't occupy prominent visual attention once reached. | Acknowledge and release attention. |
| **Not applicable** | This step doesn't apply to the user's MSP. Visible but collapsed, with an explanation. Never hidden: transparency builds trust. | Explain, never ignore. |
| **External error** | The government system fails or returns a known error. Settly can't resolve it, but communicates what to do and what it will do when the situation changes. | Honesty without abandonment. |

### Accessibility as an acceptance criterion

Accessibility in Settly isn't a layer added at the end: it's a technical acceptance criterion in every component's specification. The justification is functional, not just ethical:

- A portion of users operate in variable lighting conditions: outdoors, government offices, mid-range phone screens.
- Users with limited Italian rely more heavily on visual hierarchy and non-verbal cues to navigate. Inadequate contrast amplifies that difficulty.
- The demographic profile includes populations with less historical exposure to complex digital interfaces, where legibility isn't a nice-to-have.

Minimum contrast ratio defined: 4.5:1 for body text, 3:1 for large text and interactive elements. All error and alert states are communicated without relying exclusively on color.

### Multilingualism as a system, not a feature

The finding about conceptual equivalence (not just translation) had direct architectural consequences that I decided to take on from the start, even though they added complexity to the MVP:

- Interface strings were designed to accommodate up to 40% text expansion (Italian to English expands; Italian to Arabic involves RTL with contraction).
- The glossary was designed as a data entity independent of interface text, to allow centralized updates when official requirements change.
- A native-speaker review protocol was defined for the MVP's priority languages: English, Arabic, Spanish, Bengali, and Ukrainian.

> **Retro:** Adapting a monolingual content system to multilingual post-launch has a disproportionate redesign and technical-debt cost. Solving it in the initial architecture is slower at first and correct in the long run.

---

## Outcomes

### What I know for certain (first-hand knowledge)

The advantage of designing from lived experience is that certain hypotheses don't need additional validation: they're verifiable facts about the system.

- The *kit postale* is the step with the highest error rate on a first application. Official instructions don't distinguish between permit types.
- Italian bureaucratic terminology has no semantic equivalent in most applicants' languages. Literal translation reproduces the opacity.
- No native digital product currently exists for this user, for this process, in the Italian market.
- The process has real branches by permit type, province, and contractual situation. A single linear flow can't serve every profile.

### What I assume and need to validate with the MVP

The following statements are reasoned hypotheses, not confirmed data. They're the validation KPIs that define whether the MVP works:

| Onboarding abandonment | First-module completion | *Kit postale* errors per user | Perceived clarity score |
| :---: | :---: | :---: | :---: |
| < 15% (hypothesis) | > 70% | < 1 average | > 4 / 5, post-onboarding |

These numbers aren't arbitrarily aspirational: they're derived from comparing documented current behavior (frequent *kit postale* errors, dependence on informal support, abandonment on government portals) against what Settly's design is trying to resolve. If the product works, these indicators should move in the right direction. If they don't move, something needs to be redesigned.

---

## Learnings

### What I'd change if I started over

Intellectual honesty is part of methodological rigor. There are two decisions that, in hindsight, I'd make differently:

- **The notification system for legal requirement changes** was treated as a Phase 2 feature. It should have been part of the MVP. In the Italian migration system, requirements change frequently and without notice. The ability to alert the user to those changes is a critical source of trust, not an add-on.
- **The glossary data model** was defined later than it should have been. Its actual scope turned out to be broader than initially estimated, which created rework in integrating it with the instruction components. Mapping it before starting component design would have avoided that cycle.

---

*"Design that endures as the product grows."*

*Settly — Design Case Study, Portfolio 2025*
*José David Albarrán Velásquez · jdalbpd.me*