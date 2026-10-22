---
title: "MyINPS Bacheca Redesign"
subtitle: "Turning a public-sector dashboard from a directory of departments into a status page for the user's own case"
role: "Senior Product Designer, sole contributor"
type: "Self-initiated redesign concept"
tools: ["Figma Make"]
tags: ["concept-project", "information-architecture", "ux-audit", "public-sector", "gov-tech", "welfare-benefits"]
status: "concept"
date: "2026-10"
summary: "An information architecture audit and redesign of the MyINPS personal area home page, reorganized around what a NASpI recipient needs to know first: payment status, required actions and deadlines."
prototype_url: ""
---

# MyINPS Bacheca Redesign

*Turning a public-sector dashboard from a directory of departments into a status page for the user's own case.*

## Table of contents

- [Role and scope](#role-and-scope)
- [Context](#context)
- [Problem statement](#problem-statement)
- [Constraints](#constraints)
- [Process and decisions](#process-and-decisions)
- [Artifacts](#artifacts)
- [Outcomes](#outcomes)
- [Product reality](#product-reality)
- [Learnings](#learnings)

---

## Role and scope

I worked on this project alone, as a self-initiated concept. I owned every stage in the scope. Validation was not part of it.

| Stage | My involvement | What it included |
|---|---|---|
| Research | Led (expert review only) | Heuristic and IA audit of the live interface, with screenshots of the current state. No interviews, surveys or analytics. |
| Information architecture | Led | New content hierarchy for the home page, task-based navigation, removal of duplicated entry points. |
| Interaction design | Led | States and variants (active, processing, suspended), empty and error states, required-action flow, session expiry and logout behavior. |
| Prototyping | Led | Detailed specification for a clickable prototype in Figma Make: frames, content order, components, interactions and content rules. |
| Validation | Not done | No usability testing with real users. I name this as the main open gap below. |

---

## Context

INPS is the Italian national social security institute. Citizens use MyINPS, its personal area, to manage pensions, benefits and requests. One of those benefits is NASpI, the unemployment allowance paid every month to people who have lost their job.

The Bacheca is the first page users see after logging in. INPS describes it as the heart of the personal area. A NASpI recipient opens it with a very practical question: is my money coming, and is there anything I need to do?

I noticed that the page didn't answer either question. It showed a greeting, a promotional banner, empty notification cards, a list of services used by "people with your profile", and contact information. The user's actual benefit was not on the page.

## Problem statement

At first sight the page looks clean and friendly. The typography is consistent, the illustrations are soft, and the style is familiar for an Italian public administration site. The problem is not visual. It's structural.

The page is organized around INPS's departments and channels, not around the user's situation. For a benefit recipient, this has real consequences:

- There's no payment status, next payment date, amount or remaining duration anywhere on the page.
- Required actions are buried. "Richieste da INPS" is the only card that can mean "you must act", and it sits mid-page, inside the "INPS Risponde" section. That section is about the opposite direction of communication.
- Empty states reassure without proof. "Non ci sono eventi prossimi" reads as "all clear", even though monthly payments and deadlines are upcoming events. With no timestamp, users can't tell an empty list from a failed load.
- The most visually dominant element is a promotional banner, placed above anything related to the user's case.

The obvious fixes don't work. A "NASpI" shortcut tile keeps the status one click away, and it still competes with everything else. A restyle would make the page prettier without changing what users can find. The hierarchy itself had to change.

## Constraints

- This is an expert review and a design proposal, with no validation loop with real users. Every finding comes from the interface and from established principles, not from observed behavior.
- I had no access to data or analytics. I don't know which tasks users perform most, why they call the contact center, or how often benefits get suspended for missed obligations.
- I also had no access to the backend, so I can't confirm that real-time payment or deadline data is available to the front end. The design assumes it is. Product Reality below names this as a risk.
- Italian public administration sites follow the Designers Italia guidelines. I stayed inside that visual language on purpose, so the proposal is about structure, not about a new identity.
- Only one user type is in scope: a citizen receiving NASpI. Pensioners, employers and intermediaries would each need their own version of the status area.

## Process and decisions

### 1. Rank findings by risk to the user, not by heuristic

**Decided:** I sorted the 14 audit findings into three levels. Critical means it could cost the user money or their benefit. Moderate means friction, confusion or wasted time. Minor means polish and consistency.

**Why:** For a benefit recipient, the question that matters is "could this make me miss a payment or a deadline?" A risk-based scale makes that visible and gives a clear order for fixing things.

**Rejected:** A standard list grouped by Nielsen heuristic. It's good for coverage, but it gives a missing payment status and a capitalization issue the same level of attention.

### 2. Make the Bacheca a status page, not a directory

**Decided:** The first element after the greeting is a "La tua NASpI" card. It shows the benefit status, the next payment date and amount, the last payment, the weeks remaining and the end date. It has variants for active, processing and suspended states.

**Why:** It answers the user's main question in a few seconds. It also fixes the most serious problem in the audit: the most important state of the system wasn't visible at all.

**Rejected:** Keeping the current structure and adding a NASpI tile to "I tuoi servizi". It's cheaper, but the status stays behind a click and the page still says nothing about the user's case.

### 3. Merge requests, deadlines and profile gaps into one action list

**Decided:** An "Azioni richieste" block sits directly under the status card. It combines document requests from INPS, upcoming obligations like reporting new income, and missing profile data like a mobile number. Each item shows what's needed, the deadline, what happens if it's missed, and one primary action.

**Why:** Today, the things that need action are spread across three areas with the same visual weight. One prioritized list puts urgency in a single place.

**Rejected:** Keeping notifications and INPS requests as separate sections. It's closer to how INPS is organized internally, but the user has to check several places to know if they're at risk.

### 4. Empty states must show scope and freshness

**Decided:** While the benefit is active, "Prossime scadenze" always shows the upcoming payments. Empty states say what was checked and when ("Nessuna nuova comunicazione · aggiornato oggi alle 12:12") and link to the archive. A failed load has its own error state.

**Why:** On a page about money and deadlines, a silent "nothing here" is risky. Users need to trust that empty really means empty.

**Rejected:** Generic empty messages with an illustration. They look friendly, but they give false reassurance.

### 5. Replace the public navigation inside the personal area

**Decided:** Inside MyINPS, a compact personal header replaces the public mega-menu. It has the logo, a search scoped to the user's cases and services, notifications with an unread count, and a profile menu. The sidebar follows tasks instead of departments: Home, Le tue pratiche, Pagamenti, Comunicazioni, Documenti, I tuoi dati, Assistenza.

**Why:** The current page offers more than 20 navigation choices before the user reaches their case, and most of them mirror INPS's departments. A personal area should feel private and task-oriented.

**Rejected:** Keeping the public navigation for consistency with inps.it. Consistency matters, but here it brings the organization's structure into a space where users only care about their own situation. One "Vai a inps.it" link is enough to go back.

### 6. Remove duplicates and demote promotions, without deleting them

**Decided:** Each destination appears only once on the page. INPS Risponde lives in the "Assistenza" block. Promotions like "INPS per i giovani" move to a small "Per te" slot at the bottom, and users can dismiss it.

**Why:** Duplicates compete for attention, and users start to wonder if they're different things. The banner was the most visible element on the page and the least relevant one.

**Rejected:** Removing promotions completely. INPS has good reasons to inform citizens about its programs. A slot the user can dismiss respects that goal without taking their attention first.

### 7. Rename labels that promise the wrong thing

**Decided:** I split "I tuoi servizi", which listed services used by people with a similar profile, into two sections. "Le tue pratiche" shows the user's real cases with their status. "Servizi suggeriti" shows recommendations, clearly labeled as such.

**Why:** A label that says "yours" but shows other people's habits breaks trust. It also sends users to the wrong place.

**Rejected:** Keeping the label and adding an explanation below it. If a label needs a paragraph to be correct, the label is wrong.

## Artifacts

- IA and UX audit: 14 findings on a three-level severity scale. Each one lists the principles it violates (Nielsen heuristics, Hick's Law, Tesler's Law, Jakob's Law, Conway's Law and others) and a proposed solution.
- Screenshots of the current interface: Bacheca, notifications, services, contacts, footer and logout page. Personal data is redacted.
- Figma Make prototype specification. It covers desktop (1440px) and mobile (390px) frames, the new content order, status variants, empty and error states, and the header, sidebar and mobile tab bar. It also defines the interactions (notifications panel, payment detail, document upload, profile switch, session expiry warning, logout), WCAG 2.2 AA requirements, and content rules for Italian copy, dates and amounts. All data in it is fictional.

## Outcomes

This is a concept. Nothing was shipped or tested, so there are no measured results.

In structural terms, the project produced:

- A new hierarchy for the home page: status, required actions, deadlines and messages, the user's cases, assistance, and optional promotions at the end.
- One entry point per destination, instead of up to three.
- A navigation model that keeps the personal area separate from the public site.
- A state model for the benefit card, and for empty, error and session expiry situations.

Possible impact, not measured: if the redesign worked as intended, NASpI recipients would find their payment status without navigating. They would see required actions before the deadline, and they would have fewer reasons to call the contact center about their status. Real data would need to confirm all three.

## Product reality

### Business reality

**Why this product exists.** INPS has to pay benefits correctly and keep citizens informed about their obligations. The Bacheca is where this relationship happens online.

**What problem it would solve.** When users can't see their status, they look for it somewhere else: the contact center, local offices, or intermediaries like CAF and patronati. My hypothesis is that payment-status questions are a big part of that volume. I can't verify it without contact reason data.

**What risk it reduces.** Missed obligations can lead to a suspended or lost benefit. That's a cost for the citizen. It also creates extra work for INPS, like appeals, reactivations and more support contacts.

**Which metrics would matter.** I don't have a baseline for any of these. They're the first ones I would ask for:
- Share of required actions completed before the deadline.
- Contact center volume for payment-status questions.
- Time a user needs to find the next payment date after logging in.

**Who decides.** This is not a purchase. A change like this would sit with INPS's digital services leadership, inside public procurement and accessibility rules. I don't know their internal decision process, so I won't guess more than that.

### Operational reality

- If the payment service doesn't respond, the status card shows the last known state with its timestamp and a "dati non aggiornati" message. It doesn't show an empty card or a misleading "nothing to show".
- A benefit can get suspended while the user is logged in. After a refresh, the card and the action list must both update, and the suspension appears as an action with a reason, not only as a red badge.
- Users abandon flows. A half-finished document upload should keep its progress, and the item stays in "Azioni richieste" until it's done.
- Today the logout page is a dead end. The redesign warns users before the session expires, lets them stay connected, and adds "Accedi di nuovo" to the logout page.
- What happens when the contact center, the app and the website show different payment dates? Users stop trusting all of them. The status card only works if every channel reads from the same source.
- A missing mobile number means SMS alerts can't reach the user, so the redesign treats it as an action instead of a blank field.

### What I'd do differently as a real product

With a real team and real access, I wouldn't start from the interface. First I'd look at contact center reason codes and analytics, to confirm which tasks matter most. Then I'd interview NASpI recipients and CAF or patronato operators, who see this confusion every day. I'd also check with engineering that real-time payment and deadline data exists, because the whole status card depends on it. Finally, I'd test early with older users and non-native Italian speakers. Many people who depend on this page belong to these groups, and they're the most exposed to the risks it should prevent.

## Learnings

Risk works better than heuristics for sorting problems. When I started from "what could this cost the user?", the order of everything changed. A page can pass most heuristics and still fail the one question its users care about.

A visual problem is often an IA problem in disguise. My first impression was that the page looked fine. The real issues only appeared when I asked what each section was for, and who it served.

Public-sector interfaces tend to copy the organization. This project made Conway's Law concrete for me. The navigation follows how INPS is structured internally, and the user pays the cost of translating it.

Writing a prototype spec forces decisions. To describe the prototype for Figma Make in enough detail, I had to decide every state, label and empty case up front. It worked like a design review with myself.

Expert review has a limit. I'm confident about the structural problems, but I can't say which ones hurt users the most. Only real users and real data can answer that.