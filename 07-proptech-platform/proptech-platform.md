---
title: "Proptech Platform"
subtitle: "Owning the design system of a live product where humans and an AI agent both change the code"
role: "Senior Product Designer, sole designer on the design system"
type: "Client engagement (active)"
tools: ["Figma", "Next.js", "Tailwind CSS v4", "shadcn/ui", "Git"]
tags: ["client-work", "design-systems", "design-tokens", "proptech", "ai-agents", "b2c"]
status: "mvp"
date: null
summary: "Active client engagement on an Italian proptech platform. I own the design system from the Figma library to the production repo, and I write the rules that keep it coherent when a PM changes the code with an AI agent."
---

# Proptech Platform

**Senior Product Designer · Client engagement, in progress**

> This is real client work, not a concept project. The client name stays private in this repo. The document reflects the state of the work as of 24 September 2026 and will change as the engagement continues.

---

## Contents

- [Context](#context)
- [Scope](#scope)
- [Decisions log](#decisions-log)
- [Problems found and fixes](#problems-found-and-fixes)
- [Remaining work](#remaining-work)
- [Open dependencies](#open-dependencies)

---

## Context

The product is a live Italian real estate platform built with Next.js, Tailwind CSS v4, and shadcn/ui. I am the only designer on its design system. I work on the Figma library and I also implement the system in the production repo, by hand.

The repo has a second kind of contributor. The PM builds parts of the site with an AI coding agent. That agent writes code fast, but it does not know which values are allowed and which are not. Without rules, every session can add a raw hex value or a new Tailwind default class, and the system slowly breaks.

In 2026 many teams describe the design system as the control plane for AI-generated UI. This project is a small, real version of that idea. My job is not only to design components. It is also to define the constraints that keep the system coherent when people and an agent both change the code.

---

## Scope

**What I own**
- The design system: the Figma library and its implementation in the repo.
- Token structure, naming, and component specs. I make these decisions.

**What I share**
- Decision records list me as author and as co-decider with my client counterpart.
- Visible site-wide changes also need my counterpart's approval.

**How I work**
- I implement every repo change myself, by hand. I do not give an AI agent write access to the system layer.

---

## Decisions log

The full history lives in 25 numbered decision records (ADRs) plus a template. These are the decisions that shape the rest.

### 1. One token chain from raw value to component

**Decided:** every value follows the same path: primitive, semantic, shadcn variable, component.
**Why:** a brand change made once reaches every component. Nobody has to search the codebase for old values.
**Rejected:** letting components read primitives directly. It is faster at the start, but each component becomes its own source of truth.

### 2. Shared values vs. single-component values

**Decided:** a value used by more than one component becomes a shadcn variable. A value used by one component becomes a component token.
**Why:** it keeps the shadcn layer small and readable, and it gives each component a clear place for its own exceptions.
**Rejected:** putting everything in the shadcn layer, which would mix global and local values in one list.

### 3. Add utilities, don't override Tailwind's

**Decided:** I used `@theme inline` to add new type utilities, for example `text-body-lg`, instead of redefining Tailwind's `text-lg`. There are now 15 role-based font-size utilities.
**Why:** existing pages keep using the native classes until they are migrated. No page changed size when the change merged.
**Rejected:** overriding the native scale. It is cleaner on paper, but it changes the whole live site in one commit.

### 4. One sizing scale

**Decided:** one master sizing scale. Spacing, padding, and radius are aliases of it.
**Why:** before this, three numeric scales described the same steps with different names.

### 5. One font family declaration

**Decided:** the font family is declared once, in the version that supports the admin panel override.
**Why:** the admin panel needs to change the font, so that declaration is the one that has to win.

### 6. How decisions and changes are recorded

- Numbered ADRs from a shared template, with a Superseded status for decisions that get replaced.
- `PROGRESS.md` works as the live dashboard. I rewrite it each session.
- Commits follow `<type>(<scope>): <message>`, one commit per decision, in English, without em dashes or emojis. Each change can be traced back to one decision.

### 7. Rules for the AI agent

**Decided:** `STYLES.md` sets the limits for the PM's AI agent:
- no raw values in components;
- no Tailwind default colors;
- no new or renamed tokens without my approval.

**Why:** the agent reads the repo docs before it writes code. Putting the rules there is the most direct way to keep its output inside the system.

---

## Problems found and fixes

**Two semantic layers that did not talk to each other.** Most shadcn variables pointed to primitives, not to my semantic tokens. An audit on 23 September 2026 found 5 value conflicts, 6 unconnected variables with the same value, and 2 gaps between the layers. Phase 0 rewires them one by one, and each conflict gets its own ADR. So far 2 shadcn color variables are connected to my semantics.

**Three radius systems.** Three unrelated radius scales existed in the code. They are now one, aliased to the master sizing scale.

**A font declaration that kept coming back.** A duplicate font declaration came back three times before its final removal. This is part of why the rule now lives in `STYLES.md` and not only in my head.

**Tailwind's default palette is still active.** I will migrate the existing classes first, then remove the palette.

---

## Remaining work

**Implemented in the repo**
- Token files: `primitives.css` (raw values) and `semantics.css` (semantic and component tokens).
- One master sizing scale with spacing, padding, and radius as aliases.
- Type utilities, font registration, one radius scale.
- Component tokens for button, input, card, and option cards.

**Designed, not implemented yet**
- The user dashboard.
- The "nuovo annuncio" (new listing) flow.
- Part of the Figma component library.

**Next**
- Finish Phase 0: connect the remaining shadcn variables to the semantic layer.
- Migrate classes that use the Tailwind default palette, then remove it.

---

## Open dependencies

- Visible site-wide changes, for example the dashboard redesign, need my client counterpart's approval before they ship.
- The PM keeps building with an AI agent while I rewire the token layers. `STYLES.md` has to stay up to date with each phase so the agent does not add new values to the old layer.