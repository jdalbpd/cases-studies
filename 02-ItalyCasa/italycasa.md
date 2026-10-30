---
title: "ItalyCasa"
subtitle: "Owning the design system of an Italian real estate platform, from Figma to production code"
role: "Senior Product Designer, design system owner"
type: "Client engagement (ongoing)"
tools: ["Figma", "Figma Make", "Figma MCP connector", "Claude", "Next.js", "Tailwind CSS v4", "shadcn/ui", "lucide-react", "GitHub"]
tags: ["design-systems", "design-tokens", "design-engineering", "governance", "proptech", "shadcn-ui", "client-work"]
status: "mvp"
date: "2026-10"
summary: "Design system ownership for ItalyCasa, an Italian property listings platform. I designed the core product flows, reconciled two conflicting token systems in a live Next.js codebase, and started migrating a 120+ component custom library onto shadcn/ui."
---

# ItalyCasa

Owning the design system of an Italian real estate platform, from Figma to production code.

## Contents

- [Context](#context)
- [Problem statement](#problem-statement)
- [Constraints](#constraints)
- [Process & decisions](#process--decisions)
- [Artifacts](#artifacts)
- [Outcomes](#outcomes)
- [Product Reality](#product-reality)
- [Learnings](#learnings)

---

## Context

#### ItalyCasa is an Italian proptech platform for property listings.

It serves two kinds of users: Private owners publish one property, usually once and Agencies and professionals manage many listings and need more control. It's important to point the fact that the Italian market is led by Immobiliare.it and Idealista, and both portals treat agencies as their key paying customer.

I joined this project as the product designer and became the owner of the design system. The core team is two people: me and a partner who gave me authority over the whole design product, that included changing the repo documentation and constraints when my design needed it. A PM also works on the same repository, using an AI coding agent for site-build tasks.

The engagement started in May 2026 and is still active. Over that time I worked on competitive research, the listing creation wizard, the user profile and dashboard, the login and signup flows, the home hero, a B2B landing page for agencies, and Google Ads display creative.

This case study focuses on the design system. It connects every other piece of work, and it is the part that changed the most. <br/> 
In October 2026 I started moving it onto the shadcn/ui Figma kit, which replaced a large part of my earlier custom library.
<br/>

## Problem statement

On the surface, the job looked like "design the screens." The real problem was different. The product was already being built in code, by several people and AI agents, faster than design could be handed off.

The handoff method was screenshots. Agents and developers interpreted values from images, so every new screen added small differences. When I audited the CSS, I found the result of that drift:

- Two parallel semantic token systems: my own (`semantics.css`) and shadcn's (`:root` variables in `globals.css`). Five values conflicted, and six pairs had the same value without being connected.
- Hardcoded hex values in the shadcn block. The admin palette panel only updated my primitives, so palette changes never reached shadcn components.
- A third, disconnected radius system.
- A font declaration that kept coming back in different files after each `git pull`, likely restored by merge conflicts. Plus Jakarta Sans was referenced in CSS but never registered in the font loader.

The obvious alternatives all had a weak point. Continuing with screenshots meant more drift with every screen. Building a complete custom library and handing it over meant duplicating shadcn/ui, which the repo already used. Letting AI generate a system produces surfaces quickly, but it does not hold decisions over time or notice when two layers disagree.

So the real problem was governance: one source of truth that Figma, code and agents all follow, and a record of why each decision was made.
<br/> 

## Constraints

- Small team. No dedicated front-end developer for design work, so I implemented many changes myself.
- An existing codebase with fixed rules: Next.js, Tailwind CSS v4, stock shadcn/ui, tokens in `globals.css` through `@theme inline`, icons limited to lucide-react. UI copy in Italian, code and docs in English.
- A shared repository. The PM's AI agent could change the same files I was governing.
- The backend (Supabase) is owned by someone else. Some flows depend on a schema I don't control.
- No user research and no usability testing. Decisions came from competitive analysis, UX heuristics, reference research and the team's product knowledge. Nothing in this case study is validated with real users.
- A brand color with an accessibility limit. The lime green #A8F20B has roughly 1.4:1 contrast on white, far below the 3:1 that WCAG requires for focus indicators and UI boundaries.
- A personal choice: I did not give Claude direct repo access. I implemented changes by hand so I would understand each one.
- Tokens written by hand. Tokens Studio with GitHub sync is the planned pipeline, but it is not in use yet.
<br/> 

## Process & decisions

The work moved through three phases: product design (May to July), the system in code (August and September), and the migration to shadcn/ui (October).

### Phase 1: Product design

#### 1. Route the listing wizard by who publishes, not by how complex

The first version offered "Semplice" or "Completa" listing modes. I replaced it with one opening question: "Chi pubblica questo annuncio?" A private owner gets a 6-step flow. An agency or professional gets 7 steps.

The field differences follow the publisher's identity, not the length of the form. Only agencies can list at auction, add a neighborhood zone, set energy class and commission, or choose which agent appears as the contact. A private owner's contact data comes from the profile, so that step disappears.

I rejected the Semplice/Completa model because it asks users to predict which form they need before they see it. A private owner choosing "Completa" would meet agency-only fields with no meaning for them. In code, the wizard infrastructure is parameterized by user type, so the Agenzia flow can be added later without a refactor.
<br/> 

#### 2. Treat the wizard frame as one component: WizardChrome

Every step shares the same frame: logo, "Salva bozza", progress, and back/next navigation. I defined `WizardChrome` as a single wrapper made of `WizardTopBar` and `WizardNavigationBar`. Each step then only contains its own content.

The alternative was a header and footer per screen. That would let small differences appear between steps, which is the same drift problem at a smaller scale. Later I reused WizardChrome as the base for a proposed multi-step agency signup.
<br/> 

#### 3. Split the profile and the dashboard by state

The user profile got a dual mode: "Cerco casa" for people searching and "Pubblico annunci" for people publishing.

The dashboard ("Panoramica") was split into two states. A new user sees an onboarding checklist first, two quick actions, and no stats. An active user sees an activity summary, then listings, messages, favorites and saved searches. Primary navigation (Panoramica, Annunci, Messaggi, Preferiti) is separated from account actions (Impostazioni, Esci).

One open question was where saved searches ("Le mie ricerche") should live. I kept them inside Panoramica for now. Moving them into a combined Favorites and Alerts tab is possible, but I didn't want to make that change without usage data.
<br/> 

#### 4. One accent color for action, status colors only for status

Lime is the only primary CTA color. Status colors (success, warning, danger) are reserved for data-state badges. I took this pattern from reference research on finance dashboards, where a single accent makes the main action easy to find.

Because of the 1.4:1 contrast problem, lime is never used as text on white or as a focus ring. The ring token stays navy. I rejected using lime as a general highlight color, since it would fail accessibility in most of the places where a highlight is needed.
<br/> 

### Phase 2: The system in code

#### 5. One semantic layer, not two

The audit showed I had been building my semantic layer without accounting for the one shadcn already had. The fix was a single chain: primitive → my semantic token → shadcn variable → component. Every shadcn variable now references a semantic token instead of a hardcoded value (ADR-0005). The shadcn `--radius` now points to my radius scale (ADR-0007).

I rejected two options. Replacing shadcn's variables completely would break the components, because they expect those names. Keeping both systems in parallel was the cause of the drift in the first place. With the chain in place, the admin palette panel finally reached every component.

In the same pass, the font declaration got one canonical home in `globals.css`, with the admin hook, and Plus Jakarta Sans was registered properly (ADR-0006).
<br/> 

#### 6. One master spacing scale

`primitives.css` had three overlapping numeric scales: SIZING, SPACING and PADDING. I made SIZING the single master scale and turned the other two into aliases. Existing code kept working, and new values only need to be added in one place.
<br/>

#### 7. Keep the 14px base, add text roles

The live site had `--text-base` set to 14px instead of Tailwind's 16px, and some text looked inconsistent. Changing the base site-wide would affect every screen at once and contradict an earlier decision (ADR-0002). I kept 14px and added role-based tokens instead: `text-body`, `text-body-sm`, `text-meta`, `text-caption`. Each UI element now uses a named role, not a size.
<br/>

#### 8. Hand off rules, not screenshots

The handoff method changed several times:

1. "Agent C", an early build assistant that turned Figma screenshots into code. It stated its assumptions and marked each value as exact, approximated, or needing confirmation.
2. Rule files for coding agents, like `STYLES.md`, which I rewrote so agents follow the system instead of guessing it. I also planned a root `CLAUDE.md` with limits, so the PM's agent doesn't change the token layer.
3. Section-by-section prompts for the project's "Master Agent", built from annotated Figma specs. For the home hero I extracted values from 22 screenshots and raised 23 open questions before writing anything. Each prompt ends with the list of judgment calls I made, so they can be checked.

Every change follows the same discipline. One commit per decision, in the format `<type>(<scope>): <message>`. Tokens are committed before components, and components before page wiring. Decisions go into a numbered ADR series, now past 25 records.

I rejected screenshot handoff because the agent ends up deciding values that should be design decisions. I also rejected giving an AI agent direct repo access for my own work. It would be faster, but I would lose the understanding of why each change exists, and I need that to defend the system.
<br/>

### Phase 3: Migration to shadcn/ui

#### 9. Adopt the primitives, build the composites

By September my Figma library had more than 120 documented components. Each had a kebab-case Figma name and a PascalCase code name, generated with a naming plugin prompt I wrote ("DS Namer"). But the repo ran stock shadcn/ui. Every custom component needed translation, and the translation was where drift came back.
<br/>

In October I rebuilt the Figma library on a shadcn/ui kit, themed at the variable level ("ItalyCasa Core UI Kit v0.1"). The code follows three layers:

| Layer | Folder | Contains | Rule |
|---|---|---|---|
| Primitives | `components/ui/` | shadcn files as installed | Tokens and variants only, changes through ADR |
| Composites | `components/ic/` | `WizardChrome`, listing cards, loading button, confirm dialog | Built only from primitives |
| Features | `features/` or `app/` | Panoramica, Nuovo annuncio, Login | Never import Radix directly |

Pure out-of-the-box shadcn doesn't cover ItalyCasa's own patterns, like WizardChrome or the listing cards. Rebuilding primitives from zero would throw away the accessibility that Radix gives for free. Composition sits between the two.

The kit I chose is not identical to stock shadcn. Its button is 32px, icon buttons are a separate component, focus uses a different token, and destructive has three tokens. Each gap needs an explicit decision: the code adopts it, or Figma drops it.
<br/>

#### 10. Add a brand ramp and cut the token set

I audited the 116 color tokens in the kit file through the Figma MCP connector. I found broken hover and disabled states, invisible borders, inverted contrast and raw hex values. There were also three structural problems. Brand variations pointed to hue names (`blue`, `slime`) instead of roles. Some shadcn base tokens were duplicated or not connected. And naming was inconsistent.

The fix was a brand ramp layer between primitives and semantics: primitives → `brand/primary`, `brand/secondary` → semantic tokens → components. If the brand color changes, only the ramp changes. Component tokens follow one pattern, `{component}/{variant}/{property}/{state}`, based on Nathan Curtis's EightShapes article on token naming. I worked through the mapping with my own table, component by component.

The result is 40 base tokens plus component recipes. I then generated a `globals.css` that mirrors all four Figma layers and checked that it compiles with Tailwind v4. Utilities like `bg-primary` and `hover:bg-primary-hover` work.

The check also found mismatches still open in Figma. shadcn code expects `muted-foreground`, but the Figma token is `muted-fg`. Two typos (`bg-succes`, `bg-brand-subtile`) would become literal class names. A temporary compatibility block covers the first issue until Figma is fixed.
<br/>

#### 11. Supersede the old work, don't delete it

The migration makes much of my earlier work obsolete: the 120+ components, part of the naming convention, and many ADRs. The plan is to mark affected ADRs as superseded without editing them, write one new ADR for the shadcn adoption, and add a migration map that gives each old component a status: replaced, extended, kept custom, or removed.

The parts that survive are the three-layer token logic, the brand colors, typography, the logo naming convention, and custom patterns like WizardChrome. Deleting the old records would hide why the system changed. Superseding them keeps the history readable.
<br/>

## Artifacts

| Artifact | State |
|---|---|
| Competitive analysis of Immobiliare.it and Idealista (business models, product, Italian market) | Complete |
| Listing wizard flows, Privato (6 steps) and Agenzia (7 steps), with WizardChrome | Designed in Figma; Privato built first |
| User profile with dual mode (Cerco casa / Pubblico annunci) | Designed |
| Panoramica dashboard, New and Active states, with Figma Make prompts for both | Designed |
| Login redesign: day/night panel styles, social sign-in buttons (no auth wiring) | Specified for implementation |
| Signup account-type cards and forgot-password page, with token additions and ADRs | Specified and delivered to the repo |
| Home hero spec and Master Agent prompt | Delivered |
| B2B landing page for agencies, with Master Agent prompt | Designed |
| Custom Figma library, 120+ components, with DS Namer naming prompt | Superseded by the shadcn migration |
| Logo asset naming convention (lockup × treatment × background), documented in Italian | Complete |
| Token files: `primitives.css`, `semantics.css`, `globals.css` | Live in the repo |
| ItalyCasa Core UI Kit v0.1 (shadcn-based Figma library) with brand ramp | In progress |
| `globals.css` generated from the Figma variables, four layers | Generated and compile-checked |
| Figma ↔ Code Alignment Guide (architecture, kit gaps, states, accessibility, governance) | Complete |
| ADR series (25+ records) and commit conventions | Ongoing |
| Agent rules and prompts: Agent C, `STYLES.md`, Master Agent prompts, Phase 0 project setup | In use |
<br/>

## Outcomes

These are structural outcomes. There is no measured product impact yet: no usage analytics and no testing data are part of this work.

- The codebase has one semantic token chain instead of two. Admin palette changes now reach every component.
- Duplicate scales and declarations were removed: one spacing scale, one radius source, one font declaration.
- The listing wizard routes by publisher identity, and the code is ready for the Agenzia flow without a refactor.
- Handoff moved from screenshots to written rules and specs that agents follow, with stated assumptions.
- Every system change since August has a commit and, when it's a new decision, an ADR.
- The Figma library now starts from the same shadcn/ui components the repo runs, with a 40-token base mirrored in code.

Hypothesis, not measured: the shadcn migration should make