---
title: "ItalyCasa"
subtitle: "A design system as cost infrastructure for a small team building a real estate platform with AI agents"
role: "Senior Product Designer, design system owner"
type: "Client engagement (ongoing)"
tools: ["Figma", "Figma Make", "Figma MCP connector", "Claude", "Next.js", "Tailwind CSS v4", "shadcn/ui", "lucide-react", "GitHub"]
tags: ["design-systems", "design-tokens", "design-engineering", "governance", "accessibility", "proptech", "shadcn-ui", "client-work"]
status: "mvp"
date: "2026-11"
summary: "ItalyCasa had two conflicting token systems and screenshot handoffs to AI agents, so every new screen added drift. I merged the token layers into one chain, moved the library onto shadcn/ui, and replaced screenshots with written rules that agents follow."
impact_headline: "Merged two conflicting token systems into one chain and cut the Figma color tokens from 116 to 40."
---

# ItalyCasa

A design system as cost infrastructure for a small team building a real estate platform with AI agents.

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

> ItalyCasa competes with Immobiliare.it and Idealista for the same paying customer: the real estate agency. </br>
> The core team is two people, and part of the code is written by AI agents. In that setup, the main business risk is simple: the product gets inconsistent faster than anyone can fix it, and each new screen costs more than the last one.

I treated the design system as cost infrastructure, not as a component library. The goal was to make every new screen cheaper to build, and every brand or accessibility change a one-place edit.

### Evidence

#### Measured, from the codebase and the Figma library:

| | Before | After |
|---|---|---|
| Semantic token systems in code | 2, in conflict | 1 chain |
| Shadcn variables with hardcoded values | All of the `:root` block | 0, all reference semantic tokens |
| Radius systems | 3 | 1 |
| Spacing scales | 3 overlapping | 1 master scale + 2 aliases |
| Color tokens in the Figma kit | 116 | 40 base tokens (about 66% fewer) |
| Custom Figma components to translate into code | 120+ | Replaced by the shadcn/ui primitives the repo already runs |

### Projected, from industry benchmarks:

- In Figma's internal experiment, designers with access to a design system finished their task **34%** faster than without one. Figma presents this as the likely maximum in real conditions.
- A 2022 study with IBM's Carbon Design System (Sparkbox) found developers built the same UI **47%** faster with the system than from scratch, with a median of **2 hours** against **4.2**.

> I don't expect a two-person team on a young system to reach those numbers. To measure the real effect, I track time from finished design to merged screen, before and after the token chain.

### Hypothesis, not yet measured:

- Fewer visual regressions after merges, since each value now has one source. Measured by counting style-related fixes per month in the git history.
- Faster agent output, since agents read written rules instead of guessing values from screenshots. Measured by the number of review rounds per screen.

### Risk removed

- A brand-color focus ring that **failed accessibility**. The lime #A8F20B has about **1.4:1 contrast** on white, under the **3:1** that WCAG requires for focus indicators. The ring token is now navy, and lime is never used as text on white.
- An admin palette panel that didn't work, it changed primitives that the shadcn components never read, so brand updates silently failed. Now one change reaches every component.
- Uncontrolled edits by a second AI agent on the same repo: the token layer is now protected by written agent rules and a decision record.

---

## Context

ItalyCasa is an Italian proptech platform for property listings. </br> It serves two kinds of users: Private owners publish one property, usually once, and Agencies + Professionals manage many listings and need more control.

I joined in **May 2026** as the product designer and became the owner of the design system. The core team is two people: me and a partner who gave me authority over the whole design product, including the repo documentation and constraints. A PM also works on the same repository with an AI coding agent. Besides the system, I worked on competitive research, the listing creation wizard, the user profile and dashboards, login and signup, the home hero, a B2B landing page for agencies, Google Ads creative, and the bulk listing upload. The bulk upload has its own case study, because its problems (partial failures, data integrity, a regulated field) deserve a full story.

This case study is about the design system, because it connects all the other work.

## Problem statement

On the surface, the job looked like "design the screens", but the real problem was that the product was being built in code by several people and AI agents, faster than design could be handed off.

The handoff method was screenshots, agents and developers read values from images so every screen added small differences. </br>

My CSS audit found what that drift had produced:

- Two parallel semantic token systems: mine (`semantics.css`) and shadcn's (`:root` in `globals.css`). Five values conflicted, and six pairs had the same value without being connected.
- Hardcoded hex values in the shadcn block, so the admin palette panel never reached shadcn components.
- A third, disconnected radius system.
- A font declaration that came back in different files after each `git pull`, and a heading font referenced in CSS but never registered in the font loader.

The obvious alternatives had weak points, more screenshots meant more drift. A complete custom library meant duplicating shadcn/ui, which the repo already used. AI-generated systems produce surfaces quickly, but they don't hold decisions over time or notice when two layers disagree.

**So the real problem was governance**: one source of truth that Figma, code and agents all follow, and a record of why each decision was made.

## Constraints

- **Small team**: No dedicated front-end developer for design work, so I implemented many changes myself.
- **Fixed technical rules**: Next.js, Tailwind CSS v4, stock shadcn/ui, tokens in `globals.css` through `@theme inline`, icons limited to lucide-react. UI copy in Italian, code and docs in English.
- A **shared repository**, where the PM's AI agent could change the files I was governing.
- A **backend (Supabase)** owned by someone else.
- **No user research**, no usability testing, no product analytics in my scope. Decisions came from competitive analysis, heuristics, reference research and team knowledge.
- A brand color with an **accessibility limit** (lime at about 1.4:1 on white).
- **My own choice**: no direct repo access for Claude, I implemented changes by hand to understand each one.

## Process & decisions

The work moved through three phases: </br>
- Product design (May to July),
- The system in code (August and September), and 
- The migration to shadcn/ui (October and November).

### Phase 1: Product design

#### 1. Route the listing wizard by who publishes, not by how complex

The first version offered "Semplice" or "Completa" modes. I replaced it with one opening question: "Chi pubblica questo annuncio?" A private owner gets 6 steps. An agency gets 7.

The field differences follow the publisher's identity. Only agencies can list at auction, add a neighborhood zone, set energy class and commission, or choose which agent appears as contact, on the other hand a private owner's contact data comes from the profile, so that step disappears.

I rejected "Semplice / Completa" because it asks users to predict which form they need before seeing it. The wizard infrastructure is parameterized by user type, so the Agenzia flow can be added without a refactor.

#### 2. Treat the wizard frame as one component

Every step shares the same frame: logo, "Salva bozza", progress, back and next. I defined `WizardChrome` as one wrapper made of `WizardTopBar` and `WizardNavigationBar`, so each step only contains its own content. A header and footer per screen would let small differences appear between steps, which is the same drift problem at a smaller scale.

#### 3. Split profile and dashboard by state

The profile got a dual mode: "Cerco casa" for searching, "Pubblico annunci" for publishing. The dashboard ("Panoramica") has a New state, with an onboarding checklist and two quick actions, and an Active state ordered by activity, listings, messages, favorites and saved searches. I kept saved searches inside Panoramica for now, because moving them needs usage data I don't have.

#### 4. One accent color for action

Lime is the only primary CTA color. Status colors are reserved for data-state badges. Because of the contrast limit, lime is never text on white or a focus ring. Using lime as a general highlight would fail accessibility in most places where a highlight is needed.

### Phase 2: The system in code

#### 5. One semantic layer, not two

I had been building my semantic layer without accounting for the one shadcn already had. The fix was a single chain: primitive → my semantic token → shadcn variable → component, every shadcn variable now references a semantic token (ADR-0005), and shadcn's `--radius` points to my radius scale (ADR-0007).

Replacing shadcn's variables would break the components, because they expect those names. Keeping both systems was the cause of the drift, in the same pass, the font declaration got one home in `globals.css` and the heading font was registered properly (ADR-0006).

#### 6. One master spacing scale

`primitives.css` had three overlapping scales: SIZING, SPACING and PADDING. SIZING became the master scale and the other two became aliases. Existing code kept working, and new values go in one place only.

#### 7. Keep the 14px base, add text roles

The site's base text was 14px instead of Tailwind's 16px. Changing it site-wide would affect every screen and contradict ADR-0002. I kept 14px and added role tokens: `text-body`, `text-body-sm`, `text-meta`, `text-caption`. Each element now uses a named role, not a size.

#### 8. Hand off rules, not screenshots

The handoff method changed in three steps:

1. "**Agent C**", an early build assistant that turned screenshots into code and marked each value as exact, approximated, or needing confirmation.
2. Rule files for coding agents, like `STYLES.md`, rewritten so agents follow the system instead of guessing it. A root `CLAUDE.md` limits what the PM's agent can change in the token layer.
3. Section-by-section prompts for the project's "Master Agent", built from annotated Figma specs. For the home hero I extracted values from 22 screenshots and raised 23 open questions before writing the prompt. Each prompt ends with the list of judgment calls I made, so they can be reviewed.

Every change follows the same discipline: one commit per decision (`<type>(<scope>): <message>`), tokens before components before page wiring, and a numbered ADR for each new decision, now past 25 records.

Screenshot handoff lets the agent decide values that should be design decisions. Direct AI repo access would be faster for me, but I would lose the understanding I need to defend the system.

### Phase 3: Migration to shadcn/ui

#### 9. Adopt the primitives, build the composites

By September my Figma library had more than 120 custom components, named with a plugin prompt I wrote ("DS Namer"). But the repo ran stock shadcn/ui, and every translation from my components to theirs was a new place for drift.

In October I rebuilt the Figma library on a shadcn/ui kit, themed at the variable level ("ItalyCasa Core UI Kit v0.1"). The code follows three layers:

| Layer | Folder | Contains | Rule |
|---|---|---|---|
| Primitives | `components/ui/` | shadcn files as installed | Tokens and variants only, changes through ADR |
| Composites | `components/ic/` | `WizardChrome`, listing cards, loading button | Built only from primitives |
| Features | `features/` or `app/` | Panoramica, Nuovo annuncio, Login | Never import Radix directly |

Pure shadcn doesn't cover ItalyCasa's own patterns. Rebuilding primitives from zero would throw away the accessibility Radix gives for free. The kit also differs from stock shadcn (a 32px button, separate icon buttons, a different focus token, three destructive tokens), so each gap needs an explicit decision: the code adopts it, or Figma drops it.

#### 10. Add a brand ramp and cut the token set

Through the Figma MCP connector I audited the 116 color tokens in the kit. I found broken hover and disabled states, invisible borders, inverted contrast and raw hex values. Structurally, brand variations pointed to hue names instead of roles, shadcn base tokens were duplicated, and naming was inconsistent.

I added a brand ramp between primitives and semantics: primitives → `brand/primary`, `brand/secondary` → semantic tokens → components. If the brand color changes, only the ramp changes. Component tokens follow `{component}/{variant}/{property}/{state}`, based on Nathan Curtis's EightShapes article on token naming.

The result is 40 base tokens plus component recipes. I generated a `globals.css` that mirrors all four Figma layers and checked that it compiles with Tailwind v4. The check also found mismatches still open in Figma, like `muted-fg` where shadcn expects `muted-foreground`, and two typos that would become literal class names. A temporary compatibility block covers them until Figma is fixed.

#### 11. Supersede the old work, don't delete it

The migration makes much of my earlier work obsolete. The plan is to mark affected ADRs as superseded without editing them, write one ADR for the shadcn adoption, and keep a migration map that gives each old component a status: replaced, extended, kept custom, or removed. The token logic, brand colors, typography, logo naming and custom patterns like WizardChrome survive.

## Artifacts

| Artifact | State |
|---|---|
| Competitive analysis of Immobiliare.it and Idealista | Complete |
| Listing wizard, Privato (6 steps) and Agenzia (7 steps), with WizardChrome | Designed; Privato built first |
| Profile dual mode and Panoramica dashboard (New and Active) | Designed |
| Login, signup and forgot-password redesigns, with token additions and ADRs | Specified and delivered to the repo |
| Home hero spec and B2B landing page, with Master Agent prompts | Delivered |
| Bulk listing upload redesign | Designed, see its own case study |
| Custom Figma library, 120+ components, with DS Namer prompt | Superseded by the shadcn migration |
| Logo asset naming convention, documented in Italian | Complete |
| Token files: `primitives.css`, `semantics.css`, `globals.css` | Live in the repo |
| ItalyCasa Core UI Kit v0.1, with brand ramp | In progress |
| `globals.css` generated from Figma variables, four layers | Compile-checked |
| Figma ↔ Code Alignment Guide | Complete |
| ADR series (25+) and commit conventions | Ongoing |
| Agent rules and prompts: Agent C, `STYLES.md`, Master Agent prompts | In use |

## Outcomes

The numbers are in [Impact](#impact). Structurally, the work produced three things the team didn't have before. A single token chain that Figma and code share. A component architecture with clear layers and owners. And a handoff method based on written rules and recorded decisions, so a new person or a new agent can follow the system without me in the room.

## Product Reality

### Business reality

ItalyCasa earns from agencies, like its competitors. That's why the Agenzia wizard, the B2B landing page and the bulk upload matter: the agency is the buyer, and the product has to handle professional volume. The design system doesn't sell anything directly. It lowers the cost of every screen the business needs to compete.

The same pattern applies in fintech. A payments or banking product needs financial states (positive, negative, pending, failed) to look the same everywhere, accessibility built into tokens, and AI-assisted code that doesn't break the rules. The token chain, the governance model and the agent rules here are that pattern, applied to real estate.

### Operational reality

What happens when two actors change the same thing? This happened inside the team: the PM's agent and I could both edit the token files. Written agent limits, ADRs as the shared record, and one commit per decision make any change traceable.

What happens when the user abandons a flow? The wizard saves drafts between steps, so users come back without losing work.

What happens with bad input? The location step fills region, province, city and postal code from an address search, as read-only fields. Users only type the street and number.

What happens when an external service fails? Geolocation depends on the Google Maps API, and a fallback isn't designed yet. This is an open gap.

What happens when state changes mid-session? The login panel changes with the time of day, so I designed dedicated night styles to keep the form readable in both states.

### What I'd do differently as a real product

With real funding, I would test the wizard and dashboards with owners and agencies before building them. I would adopt the shadcn kit on day one instead of building 120 custom components first. And I would set up the Tokens Studio pipeline early, so Figma and code sync automatically.

## Learnings

The biggest lesson was to read the system I'm joining before adding mine. I spent weeks building a semantic layer next to shadcn's without seeing that shadcn already had one. Most of the bugs came from that.

Deprecated work isn't lost work. The 120 custom components became the map for the migration. Without them, I couldn't decide what shadcn replaces and what stays custom.

Implementing by hand was slower than letting an agent do it. But now I can explain every token in the repo without reading my notes. For a system owner, that matters more than speed.

Writing for AI agents turned out to be a design skill. A good prompt has the same parts as a good spec: exact values, clear limits, and an honest list of what is still a guess.