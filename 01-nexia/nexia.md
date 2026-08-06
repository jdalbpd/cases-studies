---
title: "NEXIA"
subtitle: "Decentralized identity wallet with granular on-chain permissions"
role: "Senior Product Designer — sole contributor"
type: "Self-directed design systems investigation"
stage: "0→1, MVP in definition"
platforms: ["Mobile-first", "Desktop"]
business_model: "B2B2C"
tools: ["Figma"]
tags: ["design-systems", "digital-identity", "web3", "concept-project"]
status: "concept"
date: "2026"
summary: "A self-directed investigation into what a design system looks like when treated as a contract between design and engineering — tested against a genuinely complex, multi-actor identity product."
---

# NEXIA

**Decentralized identity wallet with granular on-chain permissions**

---

## Context

NEXIA is a self-directed investigation into how a design system holds up when the product underneath it is genuinely complex — multi-actor, multi-chain, multi-state, with irreversible actions and compliance surfaces that cannot be faked later.

I built it as a sole contributor, outside of any client engagement, to answer a specific question: what does a design system look like when it is treated as a contract between design and engineering rather than a component library? Digital identity was the domain I chose because it forces every hard question at once. Sovereignty. Legibility. Asynchronous on-chain operations. Three actors with partially conflicting agendas — the identity holder, the consumer organization, and the developer integrator. Exception states that are not edge cases but daily operational reality.

The output is not a visual concept. It is a full system specification: a strategic diagnosis, a permission data model, an interaction model that separates synchronous from asynchronous operations, a semantic token architecture, a ten-state component contract for the core Permission Card, three documented priority flows with explicit decision rationale, a three-layer audit panel serving end users and legal auditors through the same system, and a governance model that defines what changes without review and what does not. Eleven frames in Figma, produced as a complete contract rather than a set of screens.

The case study documents the reasoning behind each decision. Where I made trade-offs, I say what I traded. Where I left debt, I named it and scheduled it.

---

## Problem statement

### The real problem

Digital identity is usually framed as a fragmentation problem: too many passwords, too many accounts, too many silos. That framing is accurate but shallow. It describes a symptom and calls it the disease.

The structural problem is not fragmentation. It is that users cannot see the risk they are carrying.

Every time someone clicks "Sign in with…", accepts a cookie banner, or hands over a scanned ID to onboard into a service, they transfer consequences they cannot inspect. What data was actually shared. For how long. With what scope. Under what conditions it gets revoked, or whether it gets revoked at all. The mechanism that should answer those questions does not exist at the user's layer — it lives in the backend of whoever is verifying them, and the user is asked to trust that backend without any way to audit it.

The three dominant solution archetypes each hit a structural ceiling before solving this:

Password managers solve authentication but not identity. They custody secrets, not verifiable attributes — and the provider itself remains a single point of failure. Corporate SSO solves identity inside an organizational perimeter, but the moment the contractual relationship ends, so does the identity. The user never owned it. Crypto wallets with identity layers solve sovereignty correctly but expose protocol complexity to the end user, which collapses the adoption curve to a technical audience.

The gap is at the intersection: a product that adopts the Web3 sovereignty model without exposing its complexity, and that offers organizations a reliable verification surface without forcing them to custody sensitive data.

### Why this becomes a design problem, not a technical one

The technical ingredients to solve this already exist. Decentralized identifiers, verifiable credentials, on-chain permission registries, derived attributes with zero-knowledge properties — the protocol layer is not the bottleneck.

The bottleneck is legibility.

A permission is useless if the person granting it does not understand what they are granting. An audit log is useless if the person reading it cannot tell an authorized access from a denied one. A recovery flow is useless if it is technically sound but nobody completes it. Sovereignty, in a product like this, is not a backend property. It is a property that has to be rendered — in language the user uses, in states the user can distinguish, in default behaviors that do the right thing before the user has to ask.

This reframes the problem. The product is not "a blockchain-based identity wallet." The product is **a legibility layer over a sovereignty protocol** — and the design system is the mechanism that decides whether that legibility survives contact with real operational states: pending transactions, expired permissions, unverifiable credentials, congested networks, denied access attempts, delegated recoveries.

### What NEXIA is betting on

NEXIA's bet is that three things can be true at the same time:

The identity holder gets real control over what they share, rendered in language they actually use. The consumer organization gets an instant verification surface with an auditable trail it can present to a regulator, without custodying the underlying data. The developer gets predictable APIs and abstractions that let them build without managing blockchain edge cases.

None of those three is hard to deliver in isolation. Delivering all three from the same system, with one coherent design contract underneath, is the design problem.

That is what this case study documents.

---

## Constraints

This was a self-directed project. There was no client brief, no timeline pressure, no engineering team pushing back on scope, no budget ceiling. The conventional constraints of a commercial engagement did not apply, and I will not pretend they did.

What did apply were the structural constraints imposed by the domain itself. Digital identity on a sovereign protocol is not a greenfield — it is a space with hard edges that the design has to respect from the first decision, or it collapses under its own assumptions later.

### Asynchrony is not optional

On-chain operations are not instantaneous. A permission grant, a revocation, a credential registration — each one involves network confirmation times that range from fifteen seconds to five minutes under normal conditions, and longer under congestion. This is not a loading state to be designed around. It is the physics of the medium.

Any design that treats asynchronous operations as a special case rather than the default case will produce UI that breaks as soon as it meets real network conditions. That constraint forced a specific architectural decision early: model every action as either synchronous (off-chain reads) or asynchronous (on-chain writes), expose the intermediate state as a normal operational state, and never block navigation while an action is in flight. Every subsequent component decision flows from that.

### Irreversibility has to be communicated before the action, not after

Some actions in NEXIA are reversible (revoking a permission can be followed by re-granting it). Some are not (certain on-chain records cannot be rewritten). A design system that does not distinguish between those two categories at the token level — before components, before flows — will produce interfaces that treat all destructive actions the same way, and users will learn to ignore the warnings.

This is why the semantic color system has two separate tokens: `color.action.destructive` and `color.action.irreversible`. That distinction is not cosmetic. It is a constraint the domain imposes, rendered as a primitive.

### Compliance cannot be retrofitted

GDPR's right to erasure is incompatible with a system where identity attributes live fully on-chain. An architecture that stores complete personal data on an immutable ledger cannot be made compliant later — it has to be structured from the start to separate what lives on-chain (permission hashes, audit events) from what lives off-chain (the actual attributes under holder control).

This is a structural constraint, not a feature. It shaped the permission data model, the audit panel architecture, and the governance layer. Designing the system to be compliance-compatible from the ground up was non-negotiable.

### Three actors, one system

The product serves three actors with partially conflicting agendas: the identity holder, the consumer organization, and the developer integrator. The constraint was that all three had to be served from the same design system — not three forked products, not three visual languages, not three permission models.

This ruled out certain shortcuts. I could not design the holder experience first and retrofit the organization's compliance view later. The data model had to work for both from the beginning. The component contract had to render coherently for a consumer using a mobile wallet and for a compliance officer scanning twelve hundred verifications a day from a desktop dashboard. The conflict matrix between actors (documented in the case study) exists because the constraint forced it to exist.

### No validation loop with real users

This is the most important constraint to name honestly. I had no users to test with. No compliance officers reviewing the audit panel. No developers stress-testing the API abstractions. No holders trying to recover from a lost device.

That constraint has consequences I want to be explicit about. Every design decision in this project is defensible on the basis of reasoning — from first principles of the domain, from established patterns in adjacent products, from documented usability research on consent flows and asynchronous interfaces. None of it is validated by contact with real usage. The known design debt roadmap at the end of the case study exists precisely because I treated this constraint seriously rather than pretending it was not there.

### What I chose not to constrain

One decision I want to name: I did not artificially restrict scope to make the project easier to complete. I could have designed only the holder's mobile experience, only the onboarding flow, only the token architecture. That would have been faster and easier to present.

Instead, I chose to build the full contract — both mobile and desktop, all three actors, the governance layer, the debt roadmap. The point of the exercise was to see whether a design system could hold up across that surface. Narrowing the scope would have defeated the purpose.

---

## Process & decisions

Three flows carry the weight of this product: granting granular permissions, reading the on-chain audit, and onboarding. I chose these three deliberately, and not because they were the hardest to design.

Granular permissions is where NEXIA delivers its differential value — if the holder genuinely understands what they are granting, the product wins; if it reads like another cookie banner, the product fails regardless of backend correctness. The audit panel is where systemic trust becomes verifiable rather than promised — without it, sovereignty is a slogan. Onboarding is where the user decides whether any of this is worth the initial effort — the only flow with the power to foreclose the other two.

What follows are two decisions per flow, chosen because they best illustrate how I reasoned — what I decided, why, and what I rejected. The remaining decisions are documented in the Figma system and the extended case study on Behance.

Each decision is written in the same structure: the call I made, the reasoning behind it, and the alternative I deliberately did not choose.

### Flow 1 — Granting granular permissions

**Decision: permission requests are presented in consequence language, not technical language.**

What the consumer organization requests internally is a set of attributes with access parameters: DIDs, schemas, validity windows, attribute types. What the holder sees is a sentence. "Banco Santander wants to verify that you are over 18 and resident of Spain, for the next twelve months." The translation from technical to consequential is the system's responsibility, not the user's.

The reasoning is that a permission the user does not understand is not a permission — it is recorded consent. Recorded consent protects the organization on paper and erodes the product's trust surface in practice. In an identity product, that trust surface is the product. Users who read what they authorize are more likely to keep trusting the system over time, even if the flow is marginally longer. Genuine comprehension is the defensible end state; recorded consent is the fragile one.

What I rejected was the dual-view pattern — a technical view and a plain-language view with a toggle between them. It is the obvious pattern for this kind of product and I considered it seriously. I rejected it because a toggle creates a two-class system: the default view becomes the one most users stay in, and any information in the other view becomes invisible. If the technical detail matters, it needs to be accessible without being promoted to a first-class reading mode. The design resolves this by keeping technical detail available as secondary disclosure within the flow — not behind a toggle that competes with the primary view.

**Decision: granularity is the default, not an advanced option.**

Every requested attribute appears individually on the grant screen, with the option to expand or reduce scope before confirming. There is no prominent "Accept all" button. There is an "Accept with recommended configuration" button, and tapping it reveals what that configuration implies before committing.

The reasoning is that in a sovereignty product, the default behavior is the product's ethical position. A design that makes "Accept all" the path of least resistance is a design that has decided the user's sovereignty is worth less than the organization's conversion rate. I was not willing to design a product that contradicted its own thesis in the most-used screen.

What I rejected was the progressive-disclosure alternative — show a summary by default, expose granular controls on tap. That pattern works in many consent contexts and I considered it carefully. I rejected it because it optimizes for a metric NEXIA does not want to optimize for: completion speed. In a permissions flow where actions have on-chain consequences and validity windows that persist for months, a user who moved through the flow faster is not a better outcome. A user who paused, understood, and adjusted scope is the better outcome. The interaction model had to make the slower path the normal path, not the optional one.

### Flow 2 — Audit panel and on-chain traceability

**Decision: the audit panel has three reading layers with explicit navigation between them.**

Layer one is a human-language summary. "On March 4th, Banco Santander verified that you are over 18. Authorized." No hashes, no network names, no technical IDs. Layer two is contextual detail — which specific attributes were queried, which credential version was used, whether verification succeeded or failed and why. Layer three is the technical record — transaction hash, chain, block, verification ID — exportable and independently verifiable.

The reasoning is that an audit log serves three actors simultaneously: the holder who wants to see what happened with their data, the legal or compliance reviewer who needs to reconstruct a specific event, and the developer or external auditor who needs to verify the event against the chain. These are not three different products. They are the same events read at three different depths. Forking the system into separate tools would have fragmented the source of truth; flattening it into a single view would have produced either technical noise that loses the holder or oversimplified summaries that lose the auditor.

What I rejected was the role-based view — a holder view, a compliance view, a developer view, switched by account type. It is the pattern most enterprise audit tools use, and it is wrong for this product. Role-based views assume the actor is the primary axis of variation. In NEXIA, the primary axis is depth of inquiry. A holder may occasionally need to read at layer three (exporting a record for a legal process). A compliance officer may start at layer one to scan volume before drilling into layer three on a specific event. Binding the reading depth to the actor's role would have forced all three into workflows that did not match how they actually use the information.

**Decision: denied events are as visible as authorized ones.**

Every denied access attempt — because the permission did not exist, was expired, or the requested attribute did not match the presented credential — is surfaced in the main audit view with the same visual weight as an authorized event. Denied events are filterable, exportable, and countable.

The reasoning is that an audit log that only shows successful accesses is not an audit log. It is an activity log, and activity logs are what organizations show users to create the appearance of transparency without exposing the pattern of attempts the user would actually want to see. A high volume of denied attempts from a specific organization is one of the strongest signals a user can have that something is wrong — a misconfigured integration on the organization's side, a service probing beyond its authorization scope, or an active security event. Making denied events invisible protects the organization from scrutiny; making them visible protects the user.

What I rejected was the "attention-first" pattern — showing only denied events when they cross a threshold, hiding them under a counter otherwise. It is a defensible compromise and I considered it because it reduces cognitive load in the default view. I rejected it because thresholds create a gray zone where low-volume denied patterns go unnoticed, and low-volume denied patterns are often the most informative — a single denied attempt from an organization the user has no relationship with is a signal that matters more than fifty denied attempts from an organization with a misconfigured API. The design treats all denied events as first-class and uses filtering, not hiding, to manage volume.

### Flow 3 — Onboarding and credential incorporation

**Decision: onboarding is organized around a question, not around features.**

The first screen after identity creation asks "What would you like to do first?" The options are real-use scenarios, not feature descriptions. "Connect with a service that has already requested it." "Store my identity documents securely." "See which apps have access to my information." Each option triggers a contextual flow that surfaces only the capabilities relevant to that goal.

The reasoning is that users arrive at a sovereignty product with one of two mental states: an external trigger (an organization requested verification) or a latent need (they want more control over their data). In both cases, they have a specific objective. A feature tour optimizes for the designer's model of the product — the things the designer wants the user to know exist. A goal-driven entry optimizes for the user's reason for being there. Time-to-first-perceived-value is the metric that matters at this stage, and feature tours do not reduce it; they defer it.

What I rejected was the guided tour with skip option. It is the lowest-risk pattern and the one most consumer apps still default to. I rejected it because "skip" is the feature tour's admission that it was not worth watching. If the tour is valuable, it should not be skippable. If it is skippable, it should not exist. Neither version is defensible. A goal-driven entry has no skip button because there is nothing to skip — the user is already doing the thing they came to do.

**Decision: recovery is proven before onboarding completes.**

After the user generates their identity and writes down their recovery phrase, they complete a confirmation step — entering three specific words from the phrase in the correct order. If they cannot, the flow explains the error and offers to re-reveal the phrase. Onboarding is not considered complete until the confirmation succeeds.

The reasoning is that in a sovereign identity system, recovery is the product's most consequential failure mode. If the user loses their device and cannot recover their identity, no customer support process can restore it — that is what sovereignty means. A recovery flow that the user did not actually complete is worse than no recovery flow at all, because it creates the illusion of a safety net where none exists. The confirmation step converts recovery from a promise the system makes to the user into evidence the user makes for themselves. That shift is structural, not cosmetic.

What I rejected was the deferred-confirmation pattern — let the user complete onboarding, then prompt them to verify recovery within the next seven days. It is the pattern most products use because it reduces onboarding abandonment, and onboarding abandonment is the easiest metric to show a growth team. I rejected it because deferred confirmation is reliably never completed. Users dismiss the prompt, forget, and proceed to use the product with unverified recovery — exactly the scenario the flow was supposed to prevent. The friction of verifying recovery up front is the price of the product actually working when it matters. Deferring that friction transfers the cost from onboarding to the worst possible moment: the moment recovery is needed.

### A note on the remaining decisions

Each flow contains additional decisions that I have not expanded here — default validity windows justified by service type, derived attributes surfaced as the preferred option when available, intentional confirmation for irreversible actions, question-oriented filtering in the audit panel, credential incorporation separated from initial onboarding, institutional credential wait-time managed explicitly rather than left ambiguous.

They are documented with the same structure in the extended case study on Behance and rendered in the Figma system. I left them out here because the six decisions above carry the reasoning that matters — the rest reinforce the pattern rather than extend it.

---

## Artifacts

Everything listed here exists. Nothing below describes work that is planned, sketched, or partial.

### Strategic diagnosis

A written diagnosis that reframes the problem from fragmentation to legibility, maps the structural ceilings of the three dominant solution archetypes (password managers, corporate SSO, crypto wallets with identity layers), and locates NEXIA's bet at the intersection the archetypes leave empty. The diagnosis also documents the prioritization rationale — why granular permissions comes before identity management, why on-chain audit comes before dApp interoperability — as an explicit strategic argument rather than a roadmap assumption.

### Multi-actor tension map

A three-actor model (identity holder, consumer organization, developer integrator) with a documented conflict matrix. The matrix captures five structural tensions — sovereignty versus convenience, trust versus verifiability, privacy versus compliance, simplicity versus granularity, full sovereignty versus recovery from access loss — and states the adopted design resolution for each. This artifact does what most persona work does not: it treats the actors as a system with internal conflict, not as three separate targets to optimize for in isolation.

### Information architecture and interaction model

A three-space model of the wallet — identity space, permissions space, audit space — with a full permission data model (thirteen fields, each with defined types and state taxonomies) that functions as the design contract between UI components and backend records. Alongside it, a synchrony model that classifies every user operation as synchronous, asynchronous, or semi-synchronous, with expected duration and required intermediate state. This model is the decision upstream of every component that renders a permission, a credential, or a transaction.

### Semantic token architecture

A token system organized in three collections: primitives (raw values), semantics (meaning-bound variables), and component tokens (scoped applications). Eleven semantic tokens across three categories — permission states (active, expiring, expired, revoked, pending, suspended), credential states (verified, self-issued, unverifiable), and action categories (primary, destructive, irreversible). The deliberate distinction between `color.action.destructive` and `color.action.irreversible` is encoded at the token layer because the domain requires it, not because the visual design called for it.

### Component contract — Permission Card

A ten-state specification for the core component of the system: active, expiring, expired, revoked, pending, suspended, loading, empty, error, disabled. Each state defines what it communicates, what actions are available within it, and what visually distinguishes it from adjacent states. The contract also defines the rules that govern state transitions — no state may render interactive elements until the system has confirmed the permission is effectively in that state — which is a contract between design and engineering, not a styling decision.

### Component contract — Attribute Disclosure

A five-state specification for how attributes are shared within a permission: full, derived, masked, pending verification, unverifiable. The component renders the distinction between what is shared and what is protected by being shared in that form. Derived disclosure — sharing "over 18" without revealing birth date — is the highest-value capability of the product and is designed as the first-class variant rather than an advanced option.

### Component contract — Transaction Status

A six-state specification for asynchronous on-chain operations: initiating, broadcasting, confirming, confirmed, failed, cancelled. The component is non-blocking by contract — it never prevents the user from navigating away, it persists across screens as a minimized notification, and it communicates progress through both visual and text-equivalent channels for screen readers.

### Accessibility acceptance criteria

Accessibility baseline defined as acceptance criteria for every component, not as a post-hoc audit layer. WCAG 2.1 Level AA contrast ratios, minimum touch targets, screen-reader announceability for permission states, text equivalents for all progress indicators, prefers-reduced-motion respected across animations, and a rule that no state badge may communicate through color alone. Each criterion is listed per component in the system documentation.

### Three priority flows — Figma

Eleven frames across mobile and desktop covering the three priority flows. Flow 1 (granular permissions) includes entry from wallet home, incoming request, scope configuration, duration customization, and final confirmation. Flow 2 (audit panel) includes the activity list, filters oriented around user questions, export options in both PDF and JSON, and detail views across the three reading layers. Flow 3 (onboarding) includes identity creation, recovery phrase generation, recovery confirmation with verification test, and the goal-driven entry point after completion.

### Organization-side architecture

A separate architecture for the consumer organization — rendered as a compliance operations dashboard rather than a mobile wallet. Same design tokens. Same semantic colors. Same permission data model. Completely different information architecture, because the organization does not manage one identity — it manages volume, compliance posture, and evidence. The dashboard reuses the token system and component contract without forking the design system, which is the test of whether the system actually works as a contract.

### Governance model

A three-layer stability model that defines what changes under what process. Layer 1 — stable by contract — contains elements that do not change without formal multi-team review: Permission Card state taxonomy, semantic color tokens, permission data model, three audit reading layers, accessibility acceptance criteria. Layer 2 — guided iteration — changes with documented justification: copy, default values, contextual flows, communication metaphors. Layer 3 — free iteration — changes without process: illustrations, microcopy on non-critical states, transition animations, layout within defined margins. This model exists because ungoverned design degrades, and documenting the governance before launch is the only way to prevent that degradation from being discovered after it has already happened.

### Known design debt roadmap

Five items of debt named at launch rather than discovered later: identity recovery flow requires real-user usability testing, delegated permission management is not modeled, the organization-side audit panel has less design detail than the holder's, component internationalization is not validated, and accessibility testing with users who have visual or motor disabilities is pending. Each item is documented with impact level and suggested resolution window. Documenting debt at launch is not a failure — it is the honesty exercise that enables informed decisions about when and how to address each item.

---

## Outcomes

This project did not ship to users, did not enter a pilot, and was not validated by adoption data. Any outcome framed in those terms would be invented. What follows is what the project produced in terms of artifacts, reasoning, and structural decisions that can be evaluated on their own terms.

### What the project produced

A complete design contract for a product with unusually high systemic complexity — multi-actor, multi-chain, asynchronous by default, with irreversible actions and compliance surfaces that cannot be retrofitted. The contract includes a strategic diagnosis, an actor model with documented conflict resolution, a full permission data model, a synchrony model that classifies every operation before it reaches a component, a semantic token architecture with eleven tokens across three categories, component contracts for the three most load-bearing components (Permission Card with ten states, Attribute Disclosure with five, Transaction Status with six), eleven Figma frames across mobile and desktop, a separate organization-side architecture that reuses the same token system without forking it, a three-layer governance model, and a documented debt roadmap.

### What the system resolves at the structural level

The project demonstrates that a design system can serve three actors with partially conflicting agendas from a single contract. Same tokens, same component taxonomy, same state model — rendered as a mobile wallet for the identity holder and as a compliance operations dashboard for the consumer organization, without forking the system. This is the load-bearing test of whether the contract actually functions as a contract rather than a styling guide.

The project resolves, at the design layer, the four tensions most identity products fail to reconcile. Sovereignty and convenience are reconciled by doing the right thing by default — derived attributes as the preferred option, granularity as the default disclosure level, recovery verified before onboarding completes. Trust and verifiability are reconciled by making the audit panel a three-layer system rather than three separate tools. Privacy and compliance are reconciled by separating on-chain hashes from off-chain attributes at the data-model level, which makes GDPR's right to erasure structurally possible rather than retrofitted. Simplicity and granularity are reconciled by abstracting the protocol complexity at the system layer — the holder sees permissions, not network transactions, and the chain on which a permission is registered is available as technical detail rather than primary information.

### What the documentation makes defensible

Every design decision in the project is written with its reasoning and the alternative it rejected. That structure is the project's real outcome for a reader evaluating it. A case study that documents only the final decisions presents conclusions; a case study that documents the rejected alternatives presents the reasoning behind them. The difference is the difference between showing a design and showing a designer.

The governance model and the debt roadmap serve a related function. A portfolio project that does not name its limits is asking the reader to trust that the limits do not exist. A project that documents its debt at launch — recovery flow untested with real users, delegated permissions unmodeled, internationalization unvalidated, accessibility testing pending — is asking the reader to trust the designer's self-assessment instead. For a reviewer evaluating seniority, that shift is the signal.

### What the project is evidence of

The project is evidence of a specific capability: designing a system of sufficient complexity that the design system has to function as a contract between design and engineering, not as a library of components. It is evidence that I can reason through a multi-actor product from strategic diagnosis to component state specification without losing coherence. It is evidence that I treat exception states as first-class operational states, not as edge cases to resolve later. It is evidence that I document what I decide, why I decided it, and what I chose not to build.

It is not evidence of shipping. It is not evidence of working inside a team. It is not evidence of adapting a design system to a real engineering organization's constraints. Those are different capabilities, demonstrated by different kinds of projects.

### What a reader is asked to evaluate

Whether the reasoning is sound. Whether the decisions hold up against the alternatives they rejected. Whether the contract described is the kind of contract the reader would want their own design system to operate under. Whether the capability the project demonstrates is the capability the reader is hiring for.

The project does not ask to be evaluated on outcomes it did not produce.

---

## Learnings

### Governance was the hardest part, not the most visible one

The part of the project that cost me the most was the governance model. Not because I did not know what governance meant — I understood the concept from the start — but because I could not see at first how well-constructed tokens and components would actually produce governance. I assumed governance was something you wrote on top of a finished system: a set of rules, a review process, a changelog template.

What I found in practice was the inverse. Governance is not written on top of the system. It is made possible by how the system is structured underneath. The three stability layers — stable by contract, guided iteration, free iteration — do not work as an afterthought rule set; they work because the tokens and components were built to make the distinction renderable in the first place. A token that mixes semantic meaning with primitive value cannot belong to Layer 1 no matter what the governance document says. A component with undefined states cannot be stable by contract because there is nothing to stabilize against.

Governance, I now understand, is the name we give to a property the system already has or does not have. Writing it down is documentation. Building the system so that the documentation is possible is the actual work.

### The project stopped being a UI problem before I finished the first flow

I started this project thinking I was designing a wallet interface for a protocol-level product. Somewhere during the architecture phase, I realized I was not. The real problem was not how the screens looked or how the interactions felt. It was the data model underneath — what a permission is, what states it can be in, how those states relate to on-chain transactions, how the model serves three actors without forking.

Once I understood that, the rest of the project reorganized itself. The tokens came from the data model, not from the visual language. The components came from the states the data model permitted, not from a screen inventory. The flows came from the decisions the data model forced users to make, not from a user journey map.

The screens, in the end, were the last thing I designed. They were the rendering of the contract. Not the source of it.

### I think in engineering when I design, and that is both the strength and the risk

This project confirmed something I already suspected about how I work: I reason in contracts. Data models, state taxonomies, interaction primitives, governance layers — that is where I feel most confident, and it is the layer where my decisions hold up best under pressure. That is why the case study reads the way it does, and why the system documentation is the part of the project I trust most.

The same tendency has a cost I want to name honestly. I over-engineer. When a problem presents itself, my first instinct is to reach for structural abstraction — another layer of the token system, a governance rule, a new state on a component — before testing whether a simpler solution was already available. In NEXIA, I caught myself doing this several times: elaborating the governance model before the components it was meant to govern were fully stable, defining component states that were theoretically necessary but practically rare, designing for scenarios that the product at its current stage would not encounter for years.

What I am learning to watch for is the difference between structural rigor and structural excess. The first is what makes a design system into a contract. The second is what makes a design system into a document nobody on the engineering team wants to read. I am still calibrating that line.

### The question I have not resolved

This project does two things it was designed to do. It produces a defensible design contract, and it documents the reasoning behind every decision. What it does not do, and what I have not been able to do yet, is test the contract against the two forces that would actually stress it: real engineering constraints and real user behavior.

I do not know what happens when this design system meets an engineering team that treats the contract as a suggestion rather than a contract. Some of the decisions in this project — the separation between destructive and irreversible actions at the token level, the ten-state Permission Card, the non-blocking Transaction Status — assume that engineering will honor the contract as written. If engineering negotiates the contract downward (fewer states, reduced specificity, convenience exceptions for happy paths), the system degrades fast. I have no way of knowing yet whether the contract is robust enough to resist that negotiation or whether it depends on a team culture I cannot design from outside.

I also do not know whether the language I used — permission requests in consequence form, audit events in plain language, recovery explained with metaphor instead of cryptography — works with users who are fatigued by consent flows and pattern-match past the content. The hypotheses behind those decisions are defensible. They are not validated. A holder who has granted a thousand permissions before mine may read the carefully written request the same way they read every cookie banner they have accepted without reading — not because the design failed, but because the design was meeting a user who had already given up on reading.

Both of those questions require the project to exist in the conditions it was designed for. That is the next phase of the work, and it is the reason I am pushing toward an MVP. Not to prove the design is correct. To find out where it is not.

---

*NEXIA — Case study, extended version*
*José David Albarrán Velásquez · jdalbpd.me*