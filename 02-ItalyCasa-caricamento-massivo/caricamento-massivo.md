---
title: "ItalyCasa: Caricamento massivo"
subtitle: "Redesigning a bulk listing upload so partial failures, missing data and legal fields are never silent"
role: "Senior Product Designer"
type: "Client engagement (ongoing)"
tools: ["Figma", "Figma Make", "Claude"]
tags: ["bulk-operations", "data-integrity", "error-handling", "compliance", "accessibility", "b2b", "proptech", "client-work"]
status: "concept"
date: "2026-11"
summary: "Bulk upload is how a real estate agency moves its whole portfolio onto ItalyCasa. An audit of the live code found silent data loss, a legal field filled by the system, and no feedback after publishing. I redesigned it as one import flow with two sources, one status vocabulary, and a result screen built for partial failure."
impact_headline: "Found eight listing fields shown in the UI but dropped on publish, and designed a flow where every field shown is saved."
---

# ItalyCasa: Caricamento massivo

Redesigning a bulk listing upload so partial failures, missing data and legal fields are never silent.

## Contents

- [Impact](#impact)
- [Context](#context)
- [Problem statement](#problem-statement)
- [Constraints](#constraints)
- [Process & decisions](#process--decisions)
- [Artifacts](#artifacts)
- [Outcomes](#outcomes)
- [Product Reality](#product-reality)
- [Learnings](#learnings)

---

## Impact

### Business stakes

Agencies are ItalyCasa's paying customers, and bulk upload is how an agency brings its whole portfolio onto the platform. For many agencies, it is the first real experience with the product, and if that first import loses data or publishes something the agency never declared, the agency stops trusting the platform before it pays.

> The redesign treats bulk upload as a trust and compliance problem first, and an efficiency problem second.

### Evidence

Measured, from an audit of the current code (2 November 2026):

| | Today | Redesign |
|---|---|---|
| Fields shown but not saved on publish | 8 | 0 (a field is shown only if it is saved) |
| Status vocabularies for the same job | 2 (3 words in the grid, 4 in XML) | 1 (3 main states, 2 XML-only) |
| Energy class when left empty | Silently set to "G" | Never filled by the system |
| Feedback after publishing (spreadsheet path) | None | Shared result screen with per-row reasons |
| Steps shown vs steps that exist (import dialog) | 3 shown, 2 real | Only real steps shown |
| Paths that end in the same place | 0 of 2 | 2 of 2 |

**Projected**: I didn't find a reliable public benchmark for bulk import redesigns, so I don't use one here. I'd rather show no projection than a weak one.

### Hypothesis, with how each would be measured:

| Metric | Expected direction | Why |
|---|---|---|
| Share of rows ready at first review | Up | Suggested addresses and column matching remove most "incomplete" rows on import |
| Time from upload to first publish | Down | Bulk fixes replace cell-by-cell edits |
| Sessions abandoned with zero published listings | Down | Clear status and next steps reduce confusion |
| Drafts still incomplete after 7 days | Down | Each draft says what's missing |
| Support requests about bulk upload | Down | The result screen answers "what happened?" |

None of these has a baseline yet. Adding the tracking events is part of the redesign scope.

### Risk removed

- **Silent data loss**. Agents typed parking, discount, rent duration, 3D tour, internal notes and three more fields, and the system dropped them on publish without any message.
- A **compliance risk**. An empty energy class became "G" on publish, so the agency declared a class it never chose.
- **Accessibility gaps**. Status was shown with emoji and color. In the redesign every status has an icon and a word, and the grid works with a keyboard.

---

## Context

"Caricamento massivo" is the page where ItalyCasa agencies put many listings online at once, instead of using the single-listing wizard. I own ItalyCasa's design system (see the [main ItalyCasa case study](../02-ItalyCasa/italycasa.md)), and in November 2026 I took on the redesign of this page.

The page had two paths built as separate tools:

| | Spreadsheet (CSV/Excel) and manual grid | Gestionale (XML) |
|---|---|---|
| Model | Edit everything now, in a saved session | Review, import, finish drafts later |
| Status words | Pronto / Incompleto / Errore | Pronto / Bozza / Non modificato / Da correggere |
| Re-upload | Creates new listings | Updates existing listings |
| Feedback after commit | None | Full result screen |
| Missing energy class | Silently set to "G" | Agency chooses a legal value |

I started from a functional inventory of the live code, written to make sure the redesign wouldn't lose any existing behavior.

## Problem statement

On the surface, the page looked like a **usability problem**: a dense grid, too many dialogs, no mobile layout. The audit showed something more serious: the users were losing data they had typed, the system was declaring legal information for them, and nothing told them what happened after they clicked "Pubblica."

Bulk operations **make this worse**: In a single-listing flow, one error affects one listing. In a batch of 200, an error can affect some rows and not others, and the user needs to know exactly which ones and why.

The **obvious fixes were not enough**. A visual refresh of the grid would keep the data loss, and adding a toast after publishing is too small for a batch that can partly fail. Merging the two paths into one technical flow would ignore that a spreadsheet agency and a gestionale agency do different jobs, so the real problem was to make one import model that tells the truth: what will happen before publishing?, what happened after?, and what still needs a decision from the agency?.

## Constraints

- **No user research**. The user profiles below are assumptions from the code and product context. They should be validated with 3 to 5 agency interviews before the final UI.
- **No analytics** baseline: I don't know how many agencies use each path today, so success metrics have no targets yet.
- Backend owned by someone else. Two fixes are blockers that only engineering can solve: saving every field, and accepting legal energy class values in the grid.
- Fixed limits in the current system: 200 rows per spreadsheet, 1,000 listings per XML file.
- The XML path is behind a feature flag that is off in production.
- **Design system rules**: lime is the only primary CTA color and never text on white, status colors are separate from brand colors, icons are lucide-react only, UI copy is in Italian.

### Who uses it (assumptions, not validated)

| Profile | Source | Typical volume | What they fear |
|---|---|---|---|
| Spreadsheet agency | CSV or Excel kept by hand | Tens to 200 listings | Retyping everything, publishing wrong data |
| Gestionale agency | XML export (OpenImmo, Immobiliare.it) | Up to 1,000 listings | Duplicates, losing what is already online |
| Manual agency | Types rows by hand | A handful | A grid that feels like a spreadsheet exam |

A fourth group, agencies already connected through the API, shouldn't need this page at all. The design points them to the integration instead.

## Process & decisions

I wrote six principles first, one for each problem in the audit, so they could work as acceptance criteria during review:

1. **One model, two sources**. The source changes how data enters, never what the user gets at the end.
2. **Consequences before commitment**. Nothing goes public without a summary of what will happen to every listing.
3. What you see is what gets saved.
4. **Fix in bulk, not cell by cell**. Effort should grow with the number of problems, not the number of rows.
5. **Compliance by design**. Legal fields never get a silent default.
6. Closure on every consequential action.

Then twelve decisions. The most important ones follow.

### 1. Design for partial failure, not for success

This is the core of the redesign. After "Pubblica," the spreadsheet path closed the dialog with no message. If 3 rows of 200 failed, the agency had no way to know.

The flow now has two checkpoints around the commit:

- **Before**: a summary modal that states what happens to every row. "5 pronti: vanno online subito. 4 da completare: salvati come bozza. 3 da correggere: salvati come bozza."
- **After**: a result screen ("Esito"), shared by both paths. It shows counts per outcome, a "Da sistemare" table with each failed row's reference, reason and a direct link to fix it, and three next steps.

**Failed rows don't disappear**. They stay in the grid as "Da correggere," and "Continua a sistemare" returns the user to only the rows that still need work. Published rows leave the grid, so the remaining list is always the real to-do list.

**I rejected a toast**. It disappears after a few seconds, it can't hold a list of failures, and it gives the user nothing to act on later. The extra screen replaces silence, so it adds clarity rather than steps.

This decision depends on engineering returning publish errors per row. I listed it as a **high-priority dependency**, because without it the result screen can only say that something failed, not what.

### 2. One status vocabulary, named by the action it asks for

The grid said 'Pronto' / 'Incompleto' / 'Errore'. The XML review said 'Pronto' / 'Bozza' / 'Non modificato' / 'Da correggere'. Users had to learn two systems for one job.

The redesign uses three main states: 'Pronto', 'Da completare', 'Da correggere'. Two secondary states exist only for XML updates: 'Invariato' and 'Da mettere in pausa'. "Da completare" tells the user what to do. "Incompleto" and "Bozza" only describe.

This was also a design system decision, one vocabulary maps to one set of status tokens: green, amber and red for the three main states, neutral for the XML-only ones. Each badge has a lucide icon and a word, so status is never color alone. Status tokens stay separate from brand colors, so lime never means "success."

"Bozza" stays as the technical name of a saved draft where the two meet, the UI says "Da completare (salvato come bozza)."

### 3. Every field shown is a field saved

Eight fields in the grid's detail panel were never saved on publish. The redesign shows the same field set as the agency listing wizard, and every field is saved. If engineering can't save a field at launch, it is removed from the UI, not disabled.

A disabled field invites questions nobody can answer. The trade-off is that the first release may show fewer fields than today and I think that's the honest version, and the dependency list makes the gap visible to the team.

### 4. No silent default for a legal field

An empty energy class became "G." The XML path already offered legal alternatives, the grid did not. Now both paths use the same options: A4 to G, plus "In attesa di certificazione," "Non classificabile" and "Immobile esente." Empty means "Da completare."

The agency is responsible for what it declares, so the product should never declare for it. More listings start as incomplete, but a bulk control ("Applica a tutti quelli senza classe") keeps the cost to one decision. In the XML review, this becomes a "Decisione richiesta" card above the list, because the choice changes the counts.

### 5. Choose by source, not by file format

The old entry asked "CSV or XML?", a technical question that hid the real difference. The new entry asks "Da dove arrivano i tuoi annunci?" with two cards, Foglio di calcolo and Gestionale. Each card states three facts: where fixes happen, what happens to photos, and what re-uploading does. This way agencies or agents know exactly where their data lives and few know what OpenImmo is. Stating the consequences up front removes the surprise later. Manual entry became a secondary link, because the single-listing wizard already serves small volumes.

### 6. Fix in bulk, with suggested addresses

With 200 rows, fixing one cell at a time was the main cost of the spreadsheet path. Users can now select many rows and set type, category, energy class, condition or furnishing in one action. Status filter chips with counts replace the passive summary bar, and "Prossimo da sistemare" jumps to the next row with issues.

> Bulk edit can overwrite good data, so the action shows how many rows already have a different value, and offers undo.

**Addresses were the biggest friction**: every imported row started as incomplete because no address was confirmed. The redesign geocodes each address on import. High-confidence matches are marked "Suggerito" and can be accepted all together. Ambiguous ones open the address dialog with candidates already loaded. If batch geocoding isn't available, the fallback is the current dialog with a "Conferma e vai al prossimo" button.

### 7. A grid that answers one question

The old grid had 11 fixed columns and an inline panel that pushed rows down when opened. The new grid shows only what decides publication: required fields, status and photos, with status in the first column. Clicking a row opens a side drawer with every field, grouped like the agency listing wizard, so agents edit in a structure they already know.

> The grid answers "what blocks publication?" The drawer answers "what does this listing say?"

### Other decisions

- **Destructive actions sized to their cost**: Deleting a session (rare, expensive) opens a confirmation modal with its row count. Deleting rows (frequent, cheap) happens immediately, with an "Annulla" toast for 8 seconds.
- **Photos**: the naming rule is shown before the upload, with an example built from the agency's own first reference code. Unmatched photos stay in a tray, with a keyboard alternative to drag and drop.
- **Desktop-first by decision**. The grid editor works from 1,024 px. On smaller screens, users see the session list, the counts and a clear message to continue on a computer. The XML review and the result screen work from 360 px, because they are lists, not tables.
- **An honest stepper**: Carica, Abbina colonne (spreadsheet only), Controlla, Esito only shows steps that exist.

## Artifacts

| Artifact | State |
|---|---|
| Functional inventory and gap audit of the current page | ✅ Complete |
| Redesign rationale: users, jobs to be done, six principles, twelve decisions | ✅ Complete |
| Information architecture and flow diagram (Mermaid) | ✅ Complete |
| Ten-screen specification with Italian UI copy | ✅ Complete |
| Edge case table, five states per screen, WCAG 2.2 AA requirements | ✅ Complete |
| Engineering dependency list with priorities and blockers | ✅ Complete |
| Success metrics without targets (no baseline yet) | ✅ Complete |
| Figma Make prompt for a functional prototype of both paths | ✅ Complete |

The Figma Make prompt was written as a clean handoff, not only a visual brief. All status logic lives in one function (`getRowStatus`) with explicit rules and Italian issue messages, all mock data lives in one file, and the stepper is one shared component. The same structure can move into the real codebase with little translation.

## Outcomes

The numbers are in [Impact](#impact). Structurally, the redesign turns two unrelated tools into one import model with two sources. This way, it gives the team a list of what engineering must fix before launch, separated from what design can solve. And it makes partial failure a designed state with its own screen, instead of an error nobody sees.

## Product Reality

### Business reality

**The buyer is the agency**: A smooth first import shortens the time from signup to a full portfolio online, which is when an agency starts getting value from the platform. A bad first import, with lost fields or wrong legal data, is a reason to leave or to call support.

The same problems exist in fintech, under other names:

| ItalyCasa | Fintech equivalent |
|---|---|
| Bulk listing upload with per-row results | Bulk payouts or batch payments with per-transaction status |
| Partial failure with a "Da sistemare" table | Failed transfers listed with reasons and a retry path |
| XML re-upload updates instead of duplicating | Idempotent requests, so a retry never creates a second payment |
| Energy class never filled by the system | KYC or tax declarations the user must make, never the product |
| Every field shown is saved | Data integrity in onboarding forms and KYB document uploads |

### Operational reality

What happens with bad input? Duplicate reference codes mark both rows "Da correggere" and name the other row ("Uguale alla riga 14"). A negative price or a non-integer room count is "Da correggere" with a clear message. A file over 200 rows is blocked at upload, with a suggestion to split it or use the XML path.

What happens when an external service fails? If batch geocoding isn't available, the address dialog becomes the fallback. If autosave fails, the indicator turns red with "Riprova," and leaving the page warns about unsaved changes. If some rows fail to publish, the result screen lists them and they stay in the grid.

What happens when the user abandons the flow? Spreadsheet sessions are saved and appear in "Caricamenti in corso," named from the file and date. Drafts from the XML path are finished later in "I miei annunci." Drafts still incomplete after 7 days is one of the proposed metrics, because "finish later" often means never.

What happens when two actors see conflicting information? Today only the creator can open a session, so a colleague can't continue it whether colleagues should share sessions is an open question. A second conflict is between the paths themselves: spreadsheet re-upload creates new listings while XML updates them. Unifying both by reference code would remove that conflict, but it changes backend logic, so I left it as an open question for the team.

### What I'd do differently as a real product

I would interview 3 to 5 agencies before the final UI, one per profile, to confirm the volumes and fears in the user table. I would set up the analytics events first, so the redesign launches with a baseline and the metrics have real targets. And I would push for unifying re-upload behavior by reference code in the first release, because two different re-upload rules will keep confusing agencies that use both paths.

## Learnings

Starting from an inventory of the live code, not from the screens, changed the whole project. The most important problems (lost fields, the "G" default) were invisible in the UI. I would have missed them with a visual audit.

I learned to separate design problems from engineering bugs early. Some findings were not design decisions at all, and flagging them to the team separately made the redesign easier to discuss.

Designing the failure state first made the success state simpler. Once the result screen could explain any mix of outcomes, the rest of the flow only had to lead there honestly.

Writing principles before decisions helped me in review. When a detail was unclear, I could check it against the six principles instead of starting the discussion again.