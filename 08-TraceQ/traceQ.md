---
title: "TraceQ"
subtitle: "An informational screening tool for autism-associated traits, designed with the same state-and-consent discipline as a regulated product"
role: "Product Designer"
type: "Concept Project"
tools: ["Figma", "Figma Make", "Figma Motion", "Claude"]
tags: ["concept-project", "regulated-ux", "design-systems"]
status: "prototype"
date: null
summary: "A screening tool built on the validated AQ-10 instrument, designed around consent, regulatory boundaries, and careful state handling instead of clinical framing." # drafted, please review
---

# TraceQ

## Context

Most of my concept work looks at bureaucratic or fiscal systems in Italy. TraceQ is different on the surface. It is a screening tool for autism-associated traits, not a tax form or a public process. But the design problem is the same one I keep coming back to: a product that lives or dies by how carefully it handles state and sensitive information. Here, the states are questionnaire answers with opposite scoring directions. The sensitive information is a health-adjacent result that must not read as a label or a diagnosis.

TraceQ is built on the AQ-10, a short, validated screening instrument developed by Baron-Cohen et al. at the Autism Research Centre, Cambridge. The tool is explicitly informational. It is a starting point for a conversation with a professional, not a conclusion on its own.

## What I designed

I compared existing validated instruments, AQ-10, AQ-50, RAADS-R, and CAT-Q, before choosing the AQ-10. It is short, validated, and low-risk enough for a first iteration like this one.

From there, I designed the full flow across seven screens: landing, GDPR consent, minimal context, the questionnaire itself, the result, resources, and data management. A few decisions mattered more than the others:

- I kept the tool outside EU MDR classification by showing only a raw score, with no clinical interpretation attached to it.
- I built separate, explicit consent for health-adjacent data, following GDPR Article 9, instead of folding it into a generic terms checkbox.
- I stayed aware of the AQ-10's commercial license and what it would require for any use beyond this exploration.
- I rejected a traffic-light color scheme for the answer options. The AQ-10 has items with reverse-scored direction, so a fixed color per option would mean "correct" on some questions and the opposite on others. The visual system had to follow the instrument's actual scoring logic instead of a common UI convention.
- I built a `choice-item` component, kept conceptually separate from Button. It answers a selection pattern, not an action, so it needed its own state set: idle, hover, focused, pressed.
- I prototyped single-select logic using Figma variables tied to each instance's variant properties, so choosing one option deselects the rest.

## Tools

Figma, Figma Make, Figma Motion, Claude

## Product Reality

**Business reality.** TraceQ has no business model behind it. It is a concept project, not a product I am pitching or planning to monetize. If it existed as a real product, the honest question would be who pays for it and why. A B2C free-to-use version would need a funding source, maybe a health or wellness platform licensing the flow, or a clinic offering it as a pre-screening step for new patients. I do not have a validated answer here. I am naming the gap instead of filling it with a guess.

**Operational reality.** A few real-world cases would need answers that the current prototype does not fully cover:

- A user abandons the flow halfway through the questionnaire. The prototype does not define what happens to a partial answer set. In a real product, this would need a clear decision: discard it, or let the user resume later.
- A user retakes the screening weeks or months apart. Nothing in the current design compares results over time or flags that a second result exists. That comparison logic does not exist yet.
- A user disagrees with or feels alarmed by the result. The result screen shows a raw score with no clinical language, but it does not yet include a clear next step for someone who reacts badly to what they see. This is arguably the most important operational gap in the whole project.

**What I'd do differently as a real product.** With a real team and real funding, I would not try to build this alone as a designer. I would bring in someone with clinical or psychological background early, before any screen design, to review the result-communication flow and the abandonment case. I would also want actual usability testing with people outside my own assumptions before trusting any of these design decisions. Right now, none of this has been tested with real users. It reads as reasoned, not as proven.

## What I learned

Designing for a sensitive domain is not really about tone. It comes down to specific, checkable constraints: what the instrument's license allows, how consent is scoped, where the regulatory line sits, and how the scoring actually works. The strongest interface decisions in this project came from understanding the AQ-10 itself, not from following a styling convention.

TraceQ is still in exploration and prototype phase. It has not been validated with real users.