---
title: "TraceQ"
subtitle: "An informational screening tool for autism-associated traits, built with regulated-product rigor"
role: "Product Designer"
type: "Concept Project"
tools: ["Figma", "Figma Make", "Figma Motion", "Claude"]
tags: ["concept-project", "design-systems", "regulated-ux", "healthtech-adjacent"]
status: "prototype"
date: null
summary: "A responsibly-scoped screening tool built on the validated AQ-10 instrument — framed as an informational starting point, never a diagnosis."
---

# TraceQ

**Product Designer · Concept Project**

---

## Context

Self-assessment tools for sensitive traits are often designed like generic quizzes — cheerful, gamified, indifferent to the regulatory and ethical weight of what they're actually measuring. TraceQ started as an exploration of that gap: what does it look like to design an informational screening tool for autism-associated traits with the same rigor you'd apply to a regulated product, without pretending to be a clinical instrument?

TraceQ is built around the AQ-10, a short, validated screening instrument developed by Baron-Cohen et al. at the Autism Research Centre, Cambridge. It's explicitly framed as an informational starting point — never a diagnosis, never a conclusion — designed to support a conversation with a professional, not replace one.

## What I designed

- Compared existing validated instruments (AQ-10, AQ-50, RAADS-R, CAT-Q) and selected the AQ-10 as the right fit for a first iteration: short, validated, and low-risk to prototype responsibly.
- Designed the full product architecture across 7 screens — landing, GDPR consent, minimal context, questionnaire, result, resources, and data management.
- Worked through the regulatory boundary explicitly: kept the tool outside EU MDR classification by surfacing only a raw score with no clinical interpretation, and built separate, explicit consent for health-adjacent data under GDPR Art. 9.
- Rejected a traffic-light color scheme for the questionnaire's response options. The AQ-10 includes reverse-scored items, so a fixed color per option would imply a "correct answer" that shifts inconsistently between questions — the visual system had to follow the instrument's actual scoring logic, not a default pattern.
- Built a `choice-item` component with idle, hover, focused, and pressed states, kept conceptually separate from Button — it answers a selection pattern, not an action.
- Prototyped single-select logic using Figma variables bound to variant properties, so choosing one option deselects the others.

## Tools

Figma, Figma Make, Figma Motion, Claude

## Product Reality

**Business reality.** Unlike a B2B tool with a clear procurement owner, TraceQ has no obvious single buyer — it sits closer to B2C or B2B2C, and the case for each is different. As a standalone consumer tool, the plausible model is free access with a referral path to paid or public professional evaluation, monetized (if at all) through partnership or referral arrangements with clinicians or telehealth providers rather than the individual using it. As a B2B2C component, it could plausibly be licensed to institutions that already sit upstream of a diagnostic pathway — a university student health service, an employer wellness benefit, a telehealth platform's intake flow — where the value is a low-friction, non-clinical first touchpoint that reduces the entry barrier to the institution's own paid or clinical services. Both are hypotheses drawn from adjacent market patterns, not validated by any conversation with a real institution or clinician, and I want to be explicit that no pricing, partnership, or distribution channel has been tested.

**Operational reality.** Three things worth naming that the current design doesn't yet resolve:

- **A user reacts strongly to the result.** The result screen is deliberately non-diagnostic, and a resources screen exists — but neither is designed around the possibility that a high score lands emotionally hard for someone. The flow assumes a calm reader ready to consider next steps; it doesn't yet account for a user who needs the resources screen to do more than list options.
- **The result gets used outside its intended purpose.** Nothing currently stops a result from being shared, screenshotted, or presented to a third party — a parent, a school, an employer — as though it were more conclusive than an informational score. The product's framing is correct on the screen itself; it has no way to carry that framing with it once the result leaves the product.
- **Consent withdrawal after the fact.** GDPR Art. 9 consent is designed at the point of entry, but the data-management screen's actual deletion mechanics — what happens to a result already generated, whether it's retained anywhere for product analytics — aren't specified in enough detail to say the withdrawal path is complete.

**What I'd do differently as a real product.** Before adding any feature, I'd validate the distribution question first — whether this lives as a standalone consumer tool or as a licensed component inside an institution's existing pathway, since that choice changes the consent model, the liability posture, and who's responsible for the result-in-distress scenario above. I'd also treat the "result travels beyond the product" gap as a launch blocker rather than a debt item, given the domain — an informational score being mistaken for a diagnosis outside the context that correctly frames it is the failure mode this project was designed specifically to avoid.

## What I learned

Designing responsibly in a sensitive domain isn't a tone decision — it's a series of specific, checkable constraints: instrument licensing, consent scope, classification boundaries, and scoring logic. The best interface decisions came from understanding the AQ-10 itself, not from styling conventions.

TraceQ remains in exploration/prototype phase.
