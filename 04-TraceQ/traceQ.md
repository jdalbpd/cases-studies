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

Self-assessment tools for sensitive traits are often designed like generic quizzes <br/> — cheerful, gamified, indifferent to the regulatory and ethical weight of what they're actually measuring. 
<br/>
**TraceQ started as an exploration of that gap:** what does it look like to design an informational screening tool for autism-associated traits with the same rigor you'd apply to a regulated product, without pretending to be a clinical instrument?

TraceQ is built around the AQ-10, a short, validated screening instrument developed by Baron-Cohen et al. at the Autism Research Centre, Cambridge.<br/> 
It's explicitly framed as an informational starting point — never a diagnosis, never a conclusion — designed to support a conversation with a professional, not replace one.
<br/>
<br/>

## What I designed

- Compared existing validated instruments (AQ-10, AQ-50, RAADS-R, CAT-Q) and selected the AQ-10 as the right fit for a first iteration: short, validated, and low-risk to prototype responsibly.
- Designed the full product architecture across 7 screens — landing, GDPR consent, minimal context, questionnaire, result, resources, and data management.
- Worked through the regulatory boundary explicitly: kept the tool outside EU MDR classification by surfacing only a raw score with no clinical interpretation, and built separate, explicit consent for health-adjacent data under GDPR Art. 9.
- Rejected a traffic-light color scheme for the questionnaire's response options. The AQ-10 includes reverse-scored items, so a fixed color per option would imply a "correct answer" that shifts inconsistently between questions — the visual system had to follow the instrument's actual scoring logic, not a default pattern.
- Built a `choice-item` component with idle, hover, focused, and pressed states, kept conceptually separate from Button — it answers a selection pattern, not an action.
- Prototyped single-select logic using Figma variables bound to variant properties, so choosing one option deselects the others.
<br/>
<br/>

## Tools

Figma, Figma Make, Figma Motion, Claude
<br/>
<br/>

## What I learned

> ## Designing responsibly in a sensitive domain isn't a tone decision
> — it's a series of specific, checkable constraints: instrument licensing, consent scope, classification boundaries, and scoring logic.
> The best interface decisions came from understanding the AQ-10 itself, not from styling conventions.
>> TraceQ remains in exploration/prototype phase.