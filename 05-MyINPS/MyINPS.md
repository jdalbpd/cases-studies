---
title: "MyINPS Bacheca Redesign"
subtitle: "Restructuring a public benefits dashboard around payment status, deadlines and regulatory obligations"
role: "Senior Product Designer, sole contributor"
type: "Self-initiated redesign concept"
tools: ["Figma Make"]
tags: ["concept-project", "information-architecture", "ux-audit", "public-sector", "regulated-ux", "status-dashboard", "fintech-transfer"]
status: "concept"
date: "2026-10"
summary: "An IA audit and redesign of the MyINPS personal area home page. It puts payment status and required actions first, because status questions are the top reason people contact INPS while their case is open."
impact_headline: ""
prototype_url: ""
---

# MyINPS Bacheca Redesign

*Restructuring a public benefits dashboard around payment status, deadlines and regulatory obligations.*

## Contents

- [Impact](#impact)
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

## Impact

### Business stakes

INPS pays NASpI, the Italian unemployment benefit, to people who have just lost their job. When they can't see the status of their case online, they ask INPS directly. INPS ran a customer survey in 2024. In it, "updates on the status of my case" was the most common reason for contacting INPS while a case was open, with 47.56% of the reasons given.

Each of those contacts is a phone call, a written question or an office visit. The personal area could answer many of them, but its home page doesn't show the benefit at all. The second risk is compliance: NASpI comes with obligations and deadlines, and a missed one can suspend the payment. That costs the citizen money and costs INPS rework.

The same survey shows the size of the audience. NASpI recipients were 52.34% of all respondents, and 93.28% of respondents who used the INPS website used the MyINPS personal area.

### Evidence

This is a concept, so nothing here is measured on real users. The evidence comes in three separate tiers.

#### Measured (counted from the live page and the redesign spec)

| What I counted | Current page | Redesign |
|---|---|---|
| Clicks from the home page to the payment status | Not on the page; no obvious path | 0, it's the first card |
| Entry points to INPS Risponde | 3 | 1 |
| Entry points to notifications | 3 | 1 (header bell with unread count) |
| Navigation menus inside the personal area | 3 menus with 17 links (6 + 4 + 7) | 1 sidebar with 7 task-based items, plus a compact header |
| Where a required action can appear | 1 card, mid-page, inside the INPS Risponde section | 1 list, directly under the status card |
| Audit findings | 14 (4 critical, 5 moderate, 5 minor) | Each one has a proposed solution in the spec |

I counted these from screenshots of the live page (October 2026) and from the Figma Make specification. They describe the design, not user behavior.

#### Projected (public benchmark, not INPS data)

The UK Cabinet Office's Digital Efficiency Report (2012) found that for some government services, a digital transaction costs almost 20 times less than a phone transaction. The example in the report is £0.22 per digital transaction against £4.11 by phone, from Driving Standards Agency data.

If the status card answers questions that today go to the contact center, each answered question moves from the expensive channel to the cheap one. The real effect here is probably smaller, for three reasons. The data is from another country, another decade and one agency. INPS doesn't publish a cost per contact. And a status card answers "when is my money coming", but not always "why is it late". To measure the real effect, I'd track contact center volume tagged as status questions, before and after release.

#### Hypothesis (no data yet)

| Expected effect | How I'd measure it |
|---|---|
| Users find their next payment date without leaving the home page | Task test with 5 NASpI recipients first, then the share of sessions that search for "pagamento" |
| Fewer missed deadlines | Share of required actions completed before the deadline |
| Fewer status contacts | Contact reasons coded as "status update", compared with the same period of the year before |
| Less drop-off in the document upload flow | Start-to-submit rate for uploads opened from "Azioni richieste" |

### Risk removed

These risks are removed in the design, not yet in production:

- The only card that can mean "you must act" was buried mid-page, inside a section about questions to INPS. It's now the second block on the page.
- "Non ci sono eventi prossimi" showed while monthly payments were due. Upcoming payments now always appear, and every empty state shows when it was last updated.
- A missing mobile number meant SMS alerts about deadlines couldn't reach the user, and nothing said so. It's now an action with one tap to fix.
- The logout page was a dead end. It now has "Accedi di nuovo", and users get a warning before the session expires.

---

## Role and scope

I worked on this project alone, as a self-initiated concept. I owned every stage in the scope. Validation was not part of it.

| Stage | My involvement | What it included |
|---|---|---|
| Research | Led (expert review and public data only) | Heuristic and IA audit of the live interface, a content inventory of the home page, and INPS's published customer survey. No interviews, card sorting with users or analytics. |
| Information architecture | Led | Content inventory and regrouping, new content hierarchy, task-based navigation, removal of duplicated entry points. |
| Interaction design | Led | States and variants (active, processing, suspended), empty and error states, required-action flow, escalation rules for missing data, session expiry and logout. |
| Prototyping | Led | Detailed specification for a clickable prototype in Figma Make: frames, content order, components, interactions and content rules. |
| Validation | Not done | No usability testing with real users. I name this as the main open gap below. |

---

## Context

INPS is the Italian national social security institute. Citizens use MyINPS, its personal area, to manage pensions, benefits and requests. NASpI is the unemployment allowance that INPS pays every month to people who have lost their job.

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

- This is an expert review and a design proposal, with no validation loop with real users. Every finding comes from the interface, from established principles and from public data, not from observed behavior.
- I had no access to internal data. INPS publishes a yearly customer survey, and I used it to size the problem. It gives percentages of respondents, but no contact volumes and no cost per contact.
- I also had no access to the backend, so I can't confirm that real-time payment or deadline data is available to the front end. The design assumes it is. Product Reality below names this as a risk.
- Italian public administration sites follow the Designers Italia guidelines. I stayed inside that visual language on purpose, so the proposal is about structure, not about a new identity.
- Only one user type is in scope: a citizen receiving NASpI. Pensioners, employers and intermediaries would each need their own version of the status area.

## Process and decisions

### 1. Rank findings by risk to the user, not by heuristic

**Decided:** I sorted the 14 audit findings into three levels. Critical means it could cost the user money or their benefit. Moderate means friction, confusion or wasted time. Minor means polish and consistency.

**Why:** For a benefit recipient, the question that matters is "could this make me miss a payment or a deadline?" A risk-based scale makes that visible and gives a clear order for fixing things.

**Rejected:** A standard list grouped by Nielsen heuristic. It's good for coverage, but it gives a missing payment status and a capitalization issue the same level of attention.

### 2. Inventory the page before redesigning it

**Decided:** I listed every block on the current home page and gave each one a new place, based on the user task it serves. If it served no task on the home page, I moved it or removed it.

| Current block | New place |
|---|---|
| Greeting, profile label, last access | Greeting row with "what changed since your last access"; profile moves to the header menu |
| Contact card (email, mobile, links to data and consents) | "I tuoi dati" in the sidebar; a missing mobile number becomes a required action |
| Paragraph explaining what the Bacheca is | Removed |
| "INPS per i giovani" banner | "Per te", last on the page, dismissible |
| Centro notifiche: Comunicazioni and Prossimamente | "Comunicazioni" and "Prossime scadenze" cards |
| Richieste da INPS | "Azioni richieste", directly under the status card |
| INPS Risponde section | "Assistenza" block |
| I tuoi servizi | Split into "Le tue pratiche" and "Servizi suggeriti" |
| Scelti da te (favourites and recently used) | One line for favourites under "Servizi suggeriti"; recently used leaves the home page |
| Contatti INPS (contact center, phone PIN, local office) | "Assistenza" block |
| Public navigation and utility menu | Compact personal header with a link back to inps.it |

**Why:** A list of blocks, each with a reason to exist, shows what the page is really made of. In this case, most blocks described INPS's channels, and none described the user's benefit.

**Rejected:** A card sort with NASpI recipients. It's the right method, but I had no access to users. This grouping is my own, so it's a hypothesis. An open card sort and a tree test of the new sidebar would be the first validation steps.

### 3. Make the Bacheca a status page, not a directory

**Decided:** The first element after the greeting is a "La tua NASpI" card. It shows the benefit status, the next payment date and amount, the last payment, the weeks remaining and the end date. It has variants for active, processing and suspended states.

**Why:** It answers the user's main question in a few seconds, and it's the question behind most status contacts. It also fixes the most serious problem in the audit: the most important state of the system wasn't visible at all.

**Rejected:** Keeping the current structure and adding a NASpI tile to "I tuoi servizi". It's cheaper, but the status stays behind a click and the page still says nothing about the user's case.

### 4. Merge requests, deadlines and profile gaps into one action list

**Decided:** An "Azioni richieste" block sits directly under the status card. It combines document requests from INPS, upcoming obligations like reporting new income, and missing profile data like a mobile number. Each item shows what's needed, the deadline, what happens if it's missed, and one primary action.

**Why:** Today, the things that need action are spread across three areas with the same visual weight. One prioritized list puts urgency in a single place.

**Rejected:** Keeping notifications and INPS requests as separate sections. It's closer to how INPS is organized internally, but the user has to check several places to know if they're at risk.

### 5. Handle missing data without creating panic

**Decided:** When data or a document is missing, the item follows four rules:

1. It says who has to act. If INPS is waiting for data from a third party, like the last employer, the item says so and the user has nothing to do: "Stiamo aspettando dei dati dal tuo ultimo datore di lavoro. Non devi fare nulla: ti avvisiamo quando arrivano." Only real user tasks appear as actions.
2. Color follows time, not type. An action is neutral when the deadline is more than 7 days away and amber within 7 days. It's red only when the deadline has passed or a payment is already blocked.
3. The copy has a fixed order: what's missing, why INPS needs it, the deadline, then the consequence in one plain sentence.
4. After the user acts, the item doesn't disappear. It changes to "Inviato" with a date, and then to "Accettato" or "Da correggere".

**Why:** People on unemployment benefit are already under financial stress. A red alert for something that isn't their task, or isn't urgent yet, creates calls and anxiety without helping. Separating "you must act" from "we are waiting" also removes a common reason to contact INPS.

**Rejected:** Showing every missing item as an urgent alert. It looks safer from the institution's side, but when everything is red, users can't see what is really urgent.

### 6. Empty states must show scope and freshness

**Decided:** While the benefit is active, "Prossime scadenze" always shows the upcoming payments. Empty states say what was checked and when ("Nessuna nuova comunicazione · aggiornato oggi alle 12:12") and link to the archive. A failed load has its own error state.

**Why:** On a page about money and deadlines, a silent "nothing here" is risky. Users need to trust that empty really means empty.

**Rejected:** Generic empty messages with an illustration. They look friendly, but they give false reassurance.

### 7. Replace the public navigation inside the personal area

**Decided:** Inside MyINPS, a compact personal header replaces the public mega-menu. It has the logo, a search scoped to the user's cases and services, notifications with an unread count, and a profile menu. The sidebar follows tasks instead of departments: Home, Le tue pratiche, Pagamenti, Comunicazioni, Documenti, I tuoi dati, Assistenza.

**Why:** Today the personal area has three menus with 17 links, and most of them mirror INPS's departments. A personal area should feel private and task-oriented.

**Rejected:** Keeping the public navigation for consistency with inps.it. Consistency matters, but here it brings the organization's structure into a space where users only care about their own situation. One "Vai a inps.it" link is enough to go back.

### 8. Remove duplicates and demote promotions, without deleting them

**Decided:** Each destination appears only once on the page. INPS Risponde lives in the "Assistenza" block. Promotions like "INPS per i giovani" move to a small "Per te" slot at the bottom, and users can dismiss it.

**Why:** Duplicates compete for attention, and users start to wonder if they're different things. The banner was the most visible element on the page and the least relevant one.

**Rejected:** Removing promotions completely. INPS has good reasons to inform citizens about its programs. A slot the user can dismiss respects that goal without taking their attention first.

### 9. Rename labels that promise the wrong thing

**Decided:** I split "I tuoi servizi", which listed services used by people with a similar profile, into two sections. "Le tue pratiche" shows the user's real cases with their status. "Servizi suggeriti" shows recommendations, clearly labeled as such.

**Why:** A label that says "yours" but shows other people's habits breaks trust. It also sends users to the wrong place.

**Rejected:** Keeping the label and adding an explanation below it. If a label needs a paragraph to be correct, the label is wrong.

### Transfer to fintech products

This is a public benefits product, not a fintech one. But the problems are close: money, deadlines, regulation, and users who are worried about getting paid. The same patterns apply directly.

| MyINPS pattern | Fintech equivalent |
|---|---|
| "La tua NASpI" status card | Account or payout status: next payout date, pending vs settled |
| "Azioni richieste" with deadlines | KYC or KYB document requests and periodic reviews, before an account is restricted |
| "Who has to act" labels | Pending on the customer vs pending on the provider, a common source of "where is my money" tickets |
| Freshness timestamp on every list | "Last updated" on balances and transactions, so pending is never confused with missing |
| Suspended state with a reason and an action | Restricted account with a reason code and a clear path to lift it |
| Missing mobile number as an action | Missing SCA or 2FA channel: without it, no alerts and no step-up verification |

## Artifacts

- IA and UX audit: 14 findings on a three-level severity scale. Each one lists the principles it violates (Nielsen heuristics, Hick's Law, Tesler's Law, Jakob's Law, Conway's Law and others) and a proposed solution.
- Content inventory of the current home page, with the new place of each block (decision 2).
- Screenshots of the current interface: Bacheca, notifications, services, contacts, footer and logout page. Personal data is redacted.
- Figma Make prototype specification. It covers desktop (1440px) and mobile (390px) frames, the new content order, status variants, empty and error states, and the header, sidebar and mobile tab bar. It also defines the interactions (notifications panel, payment detail, document upload, profile switch, session expiry warning, logout), WCAG 2.2 AA requirements, and content rules for Italian copy, dates and amounts. All data in it is fictional.

## Outcomes

This is a concept. Nothing was shipped or tested. The design counts and the benchmark are in [Impact](#impact).

In structural terms, the project produced:

- A new hierarchy for the home page: status, required actions, deadlines and messages, the user's cases, assistance, and optional promotions at the end.
- One entry point per destination, instead of up to three.
- A navigation model that keeps the personal area separate from the public site.
- A state model for the benefit card, the action items, and empty, error and session expiry situations.
- Escalation rules that separate "you must act" from "we are waiting".

## Product reality

### Business reality

**Who decides.** This is not a purchase. A change like this would sit with INPS's digital services leadership, inside public procurement and accessibility rules. I don't know their internal decision process, so I won't guess more than that.

**What matters to them.** The service cost per citizen and the rework caused by suspended benefits. The metrics are in the Hypothesis table above. INPS doesn't publish a baseline for any of them, so they're the first data I would ask for.

### Operational reality

- If the payment service doesn't respond, the status card shows the last known state with its timestamp and a "dati non aggiornati" message. It doesn't show an empty card or a misleading "nothing to show".
- A benefit can get suspended while the user is logged in. After a refresh, the card and the action list must both update, and the suspension appears as an action with a reason, not only as a red badge.
- Users upload the wrong file. The upload checks the file type, size and readability before sending, and shows an example of the expected document. If INPS rejects it later, the item goes back to "Da correggere" with the reason.
- Users abandon flows. A half-finished document upload keeps its progress, and the item stays in "Azioni richieste" until it's done.
- A CAF or patronato operator can send a document for the user. The item then shows who sent it and when, so the user doesn't upload it a second time.
- The contact center, the app and the website can show different payment dates. When that happens, users stop trusting all of them. The status card only works if every channel reads from the same source.
- Today the logout page is a dead end. The redesign warns users before the session expires, lets them stay connected, and adds "Accedi di nuovo" to the logout page.

### What the front end needs from the backend

- Benefit status, with a reason code for suspensions.
- Payment schedule: past payments with their state, and the next expected payment.
- Open requests and obligations, with deadline, owner (user, INPS or third party) and state.
- A "last updated" timestamp for each of these data sources.

### What I'd do differently as a real product

With a real team and real access, I wouldn't start from the interface. First I'd look at contact center reason codes and analytics, to confirm which tasks matter most. Then I'd interview NASpI recipients and CAF or patronato operators, who see this confusion every day. I'd also run an open card sort and a tree test on the new navigation. I'd also check with engineering that real-time payment and deadline data exists, because the whole status card depends on it. Finally, I'd test early with older users and non-native Italian speakers. Many people who depend on this page belong to these groups, and they're the most exposed to the risks it should prevent.

## Learnings

Risk works better than heuristics for sorting problems. When I started from "what could this cost the user?", the order of everything changed. A page can pass most heuristics and still fail the one question its users care about.

A visual problem is often an IA problem in disguise. My first impression was that the page looked fine. The real issues only appeared when I listed each block and asked who it served.

Public-sector interfaces tend to copy the organization. This project made Conway's Law concrete for me. The navigation follows how INPS is structured internally, and the user pays the cost of translating it.

Urgency is a design decision. Deciding when something turns red was harder than designing the card itself, because the wrong color sends people to the phone.

Public data makes a concept less of a guess. I had no access to INPS analytics, but its published survey gave me a real problem size to design against.

Expert review has a limit. I'm confident about the structural problems, but I can't say which ones hurt users the most. Only real users and real data can answer that.