---
title: "Soloist"
subtitle: "AI-Powered Onboarding and Conversational Diagnostics"
role: "Product Designer"
type: "Concept Project"
tools: ["Figma", "Figma Make", "Claude"]
tags: ["concept-project", "ai", "fintech", "conversational-design"]
status: "concept"
date: null
summary: "An AI conversational assistant guiding Italian freelancers through fiscal diagnosis — starting with the regime forfettario — without requiring prior expertise."
---

# Soloist

**Product Designer · Concept Project**

---

## Context

In Italy, people who open a Partita IVA often find themselves alone facing complex fiscal and contractual decisions, without easy access to expert guidance. Having closely observed how much uncertainty Italian freelancers face — between the *regime forfettario*, revenue thresholds, and obligations that shift depending on the individual's situation — I developed Soloist as a design response to this problem: an AI conversational assistant meant to offer clear guidance without requiring prior fiscal expertise. This first version covers the fiscal branch exclusively; the architecture was designed from the start to scale toward a broader system (contractual, financial, career), but the priority for this phase was to validate a single domain in depth before expanding.

## What I designed

- A hybrid onboarding architecture: an initial selection via emotional chips, followed by a branching conversation based on the user's context
- A conversational flow branching into three diagnostic paths, each with its own output and differentiated tone
- Escalation logic toward a human accountant, designed as a value deliverable (a brief ready to bring to the professional) rather than an error message
- A dark visual system with a blue-violet palette and an "organized catalog" direction, without traditional chat bubbles
- Mapping of system states — loading, conversation limit, confirmation, diagnosis delivery

## Tools

Figma, Figma Make, Claude (AI-assisted design)

## Product Reality

**Business reality.** As with a self-diagnostic tool used directly by the person it benefits, there's no separate buyer in the simplest reading — the freelancer uses it for themselves, which points toward a B2C model: free or freemium access, a paid tier for deeper or ongoing diagnostics as thresholds shift through the year. But the escalation design suggests a second, more interesting path: the human-accountant handoff is built as a value deliverable, a qualified brief rather than a dead end, which is exactly the shape of a lead-generation mechanic. That opens a B2B2C reading where an accounting firm or a network of commercialisti is the actual paying party, using Soloist as a free-to-the-freelancer triage layer that delivers them pre-qualified, already-diagnosed prospects. Neither model is tested — there's no accountant partnership, no pricing, and no validation of which of the two a real freelancer or a real accounting firm would actually pay for.

**Operational reality.** The domain raises the stakes on a few things worth naming directly:

- **The AI diagnosis is wrong or overconfident.** This is the failure mode that matters most given what's at stake — a freelancer making a real decision about their fiscal regime based on a subtly incorrect diagnosis has real financial and legal consequences, not just a bad product experience. The escalation-to-human path is the right instinct, but nothing in the current design specifies a confidence threshold: what determines whether a diagnosis is presented as an answer versus automatically routed to the accountant instead of stated as settled.
- **Incomplete or contradictory answers inside a three-question limit.** The three-question ceiling is deliberately tight, to keep the flow from feeling like a form — but that same tightness leaves little room to recover from an ambiguous or self-contradicting answer without either guessing past it or breaking the limit that makes the product work in the first place.
- **The user hits the limit before reaching a diagnosis.** It isn't specified whether that's framed as a successful escalation outcome or reads as the product visibly failing to deliver what it promised.

**What I'd do differently as a real product.** I'd validate the confidence/escalation threshold before building anything else, since it's the single decision most directly tied to whether the product could cause real harm rather than just a bad experience. And I'd test the assumption the B2B2C model depends on — whether accounting professionals actually want an AI-generated brief as a qualified lead, or would treat it as unvetted noise — before treating that as the more valuable business model over the direct-to-freelancer one.

## What I learned

I learned that three questions is the limit beyond which a conversation starts to feel like a form to fill out. And that presenting escalation as a concrete service, rather than a system limitation, completely changes the perceived reliability of the product.
