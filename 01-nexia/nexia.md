---
title: Nexia
subtitle: Decentralized identity wallet with granular on-chain permissions - Concept project.
role: Product Designer, sole contributor
tools:
  - Figma
  - Figma Make
  - Claude (AI-assisted)
tags:
  - design-systems
  - concept-project
  - b2c
  - trust-and-identity
status: 0→1, MVP in definition.
date: 2026-01
summary: A B2C platform, self-directed investigation into how a design system holds up under real complexity.
---

## Content

- [Context](#context)
- [Problem Statement](#problem-statement)
- [Process & Desitions](#process-&-decisions)
- [Artifacts](#artifacts)
- [Outcomes](#outcomes)
- [Product Reality](#product-reality)
- [Learnings](#learnings)

---

# Nexia - prototype

- [Check the repo here!](#context)

---

## Context

NEXIA is a self-directed investigation into how a design system holds up when the product is truly complex. It is multi-actor, multi-chain, and multi-state. It has irreversible actions and compliance needs that cannot be added later.

I built it alone, outside any client work, to test one question. What changes when a design system works as a contract between design and engineering, not as a component library?

Digital identity forces every hard question at once. Sovereignty and legibility. Asynchronous on-chain operations. Three actors with conflicting agendas: the identity holder, the consumer organization, and the developer integrator. Exception states that are daily reality, not edge cases.

The output is a full system specification, not a visual concept. It includes a strategic diagnosis, a permission data model, a synchrony model, a token architecture, and a ten-state Permission Card contract. It also covers three priority flows, a three-layer audit panel, and a governance model. Eleven Figma frames render the contract. I document each decision with the alternative I rejected, and I name the debt I left.

<br/>

## Problem statement

### The real problem

Digital identity is usually framed as fragmentation: too many passwords, accounts, and silos. That is accurate but shallow. The real problem is that users cannot see the risk they carry.

Each time someone clicks "Sign in with," accepts a cookie banner, or sends a scanned ID, they accept consequences they cannot inspect. What was shared, for how long, with what scope, and when it gets revoked. The answers live in the verifier's backend, and the user has no way to audit it.

Three solution archetypes hit a ceiling. Password managers custody secrets, not verifiable attributes, and the provider stays a single point of failure. Corporate SSO ends when the contract ends, so the user never owned the identity. Crypto wallets get sovereignty right but expose protocol complexity, which limits adoption to technical users.

The gap is clear. Users need Web3 sovereignty without its complexity. Organizations need a verification surface that does not force them to store sensitive data.

### Why this is a design problem, not a technical one

The technical pieces already exist: decentralized identifiers, verifiable credentials, on-chain permission registries, derived attributes. The bottleneck is legibility. A permission means nothing if the person does not understand it. An audit log means nothing if they cannot tell authorized from denied. A recovery flow means nothing if nobody completes it.

So the product is a legibility layer over a sovereignty protocol. The design system decides whether that legibility survives real states: pending transactions, expired permissions, unverifiable credentials, congested networks, denied access.

### What NEXIA is betting on

Three things can be true at once. The holder controls what they share, in plain language. The organization gets instant verification and an auditable trail, without custody of the data. The developer gets predictable APIs without managing blockchain edge cases.

Each one is easy alone. Delivering all three from one design contract is the design problem.

<br/>

## Constraints

This was self-directed. There was no client brief, no deadline, no engineering pushback, and no budget ceiling. The constraints came from the domain itself.

### Asynchrony is not optional

On-chain writes take from fifteen seconds to five minutes, and longer under congestion. This is not a loading state to design around. It is how the medium works. I modeled every action as synchronous (off-chain reads) or asynchronous (on-chain writes), and I never block navigation while an action is in flight.

### Irreversibility must be visible before the action

Revoking a permission can be undone. Some on-chain records cannot. If the system treats both the same way, users learn to ignore warnings. So the token layer has two separate tokens: color.action.destructive and color.action.irreversible.

### Compliance cannot be added later

GDPR's right to erasure does not fit a system that stores personal data on an immutable ledger. Permission hashes and audit events live on-chain. The actual attributes stay off-chain, under holder control. This split shaped the data model, the audit panel, and the governance layer.

### Three actors, one system

All three actors had to use the same design system. No forked products, no separate visual languages, no separate permission models. The same components had to work for a holder on a mobile wallet and for a compliance officer scanning twelve hundred verifications a day on desktop.

### No validation with real users

This is the most important constraint to name. I had no users to test with. Every decision rests on reasoning from the domain, adjacent products, and published research on consent flows. None of it has been tested against real usage. The debt roadmap exists because of this.

### Scope I chose not to reduce

I could have designed only the holder's mobile flow. That would have been faster to present. I built the full contract instead: mobile and desktop, three actors, governance, and the debt roadmap. The goal was to see whether one system could hold across all of it.

---

## Process & decisions

Three flows carry the product: granting permissions, reading the audit, and onboarding. Permissions is where NEXIA creates its value. The audit is where trust becomes checkable. Onboarding decides whether a user gets to the other two at all.

Below are two decisions per flow. Each shows what I decided, why, and what I rejected. The rest are documented in Figma and the extended version on Behance.

---

### Flow 1: Granting granular permissions

The holder does not see DIDs and schemas, they see a sentence: "Banco Santander wants to verify that you are over 18 and resident of Spain, for the next twelve months." The system does the translation, not the user.
<br/>

![Granting granular permissions](/01-nexia/img/F1.png "Image of the screen")

**Why?:** a permission the user does not understand is only recorded consent. It protects the organization on paper and weakens trust in practice.

**Rejected:** a technical view and a plain view with a toggle. A toggle creates two classes of users, and the technical detail becomes invisible. I kept it as secondary disclosure inside the flow.

> Permission requests use consequence language, not technical language

#### Granularity is the default

Every requested attribute appears on its own. There is no prominent "Accept all." The "Accept with recommended configuration" button shows what it implies before the user commits.

**Why?:** in a sovereignty product, the default is the ethical position. "Accept all" as the easy path would contradict the thesis on the most-used screen.

**Rejected:** a summary first, with granular controls on tap. It optimizes for completion speed. Here, a user who pauses and adjusts scope is the better outcome.

---

### Flow 2: Audit panel and on-chain traceability

#### The audit panel has three reading layers

Layer one is a plain summary: "On March 4th, Banco Santander verified that you are over 18. Authorized." Layer two shows which attributes were queried, which credential version was used, and why a check failed. Layer three is the technical record: transaction hash, chain, block, and verification ID. It can be exported and verified independently.

![Audit panel and on-chain traceability](/01-nexia/img/F2.png "Image of the screen")

**Why?:** holders, compliance reviewers, and auditors read the same events at different depths. Separate tools would split the source of truth.

**Rejected:** role-based views. The real axis is depth of inquiry, not role. A holder may need layer three for a legal process. A compliance officer may start at layer one to scan volume.

#### Denied events are as visible as authorized ones

Every denied attempt appears in the main view with the same weight as an authorized one. Denied events can be filtered, exported, and counted.

**Why?:** a log of successes only is an activity log, not an audit. A pattern of denied attempts is often the strongest warning a user can get.

**Rejected:** showing denied events only above a threshold. Thresholds hide low-volume patterns. One denied attempt from an unknown organization can matter more than fifty from a misconfigured API.

---

### Flow 3: Onboarding and credential incorporation

#### Onboarding starts with a question

The first screen asks "What would you like to do first?" The options are real tasks: connect with a service that asked for verification, store identity documents, or see which apps have access.

![Onboarding and credential incorporation](/01-nexia/img/F3.png "Image of the screen")

**Why?:** users arrive with a goal, either an organization's request or a need for control. A goal-driven start shortens the time to first value.

**Rejected:** a guided tour with a skip option. If the tour is worth watching, it should not be skippable. If it can be skipped, it should not exist.

#### Recovery is proven before onboarding ends

After writing down the recovery phrase, the user enters three specific words in order. Onboarding is not complete until this succeeds.

**Why?:** if a user loses their device and cannot recover, no support team can fix it. An untested recovery flow gives a false sense of safety.

**Rejected:** confirming recovery within seven days after onboarding. Deferred confirmation almost never happens. The cost then moves to the worst moment, when recovery is needed.

#### The remaining decisions

Each flow holds more decisions that I did not expand here: default validity windows by service type, derived attributes as the preferred option, confirmation for irreversible actions, question-based audit filters, credentials added after onboarding, and managed wait time for institutional credentials. They follow the same pattern as the six above.

## Artifacts

Everything listed here exists.

- **Strategic diagnosis.** It reframes the problem from fragmentation to legibility, maps the three archetypes, and explains why permissions come before identity management and audit before dApp interoperability.
- **Multi-actor tension map.** Three actors and five tensions, each with its design resolution: sovereignty vs convenience, trust vs verifiability, privacy vs compliance, simplicity vs granularity, sovereignty vs recovery.
- **Information architecture and interaction model.** Three spaces (identity, permissions, audit), a permission data model with thirteen fields, and a synchrony model for every operation.
- **Semantic token architecture.** Three collections: primitives, semantics, and component tokens. Eleven semantic tokens cover permission states, credential states, and action categories.
- **Permission Card contract.** Ten states: active, expiring, expired, revoked, pending, suspended, loading, empty, error, disabled. No state shows interactive elements until the system confirms it.
- **Attribute Disclosure contract.** Five states: full, derived, masked, pending verification, unverifiable. Derived disclosure, such as "over 18" without a birth date, is the first-class variant.
- **Transaction Status contract.** Six states, from initiating to cancelled. It never blocks navigation and stays visible as a minimized notification.
- **Accessibility acceptance criteria.** WCAG 2.1 AA per component, including screen-reader announcements and no state shown by color alone.
- **Three priority flows in Figma.** Eleven frames across mobile and desktop.
- **Organization-side architecture.** A compliance dashboard with the same tokens and the same data model, but a different information architecture.
- **Governance model.** Three stability layers: stable by contract, guided iteration, and free iteration.
- **Design debt roadmap.** Five items, each with an impact level and a resolution window.
---
 
## Outcomes
 
This project did not ship, did not enter a pilot, and has no adoption data. Any result framed that way would be invented. What follows is what the project produced.
 
It produced a complete design contract for a complex product, from diagnosis to component states. The strongest test of the contract is the organization-side dashboard. Same tokens, same components, same state model, shown as a mobile wallet for holders and as a compliance dashboard for organizations, without forking the system.
 
At the design layer, it resolves four tensions that most identity products leave open. Sovereignty and convenience: the right default does the work. Trust and verifiability: one three-layer audit panel instead of three tools. Privacy and compliance: on-chain hashes, off-chain data. Simplicity and granularity: the holder sees permissions, not network transactions.
 
The project is evidence that I can reason through a multi-actor product from diagnosis to component states and treat exception states as first-class. It is not evidence of shipping, of working inside a team, or of adapting a system to a real engineering organization.
 
---
 
## Product Reality
 
The sections above judge the contract on its own terms. This section asks two harder questions. Does it hold up as a business? Does it hold up when real actors misbehave?
 
### Business reality
 
The buyer is the consumer organization, not the holder. Most likely it is a compliance, risk, or identity lead deciding whether to route KYC-equivalent checks through NEXIA instead of storing the data.
 
The argument is risk transfer, not growth. An attribute the organization does not store is one it cannot leak, cannot be forced to hand over beyond the audit trail, and does not need to delete under GDPR. The exportable layer-three record gives auditors evidence without personal data. The metric that plausibly matters is less data-custody liability per verification.
 
I have not established pricing, unit economics, or willingness to pay. I do not know if organizations would pay per verification, pay a platform fee, or expect free infrastructure. This project was never set up to answer those questions.
 
### Operational reality
 
Four gaps remain open.
 
A credential can verify technically and still be misused, for example one issued for a different purpose. The state layer can show "unverifiable" but not "verifiable but misused." That is a policy question as much as a design one.
 
Two actors can see different states. After a holder revokes a permission, the organization's system may show the old state until the chain confirms. The holder's side shows this honestly. The organization's dashboard does not yet define what it shows, or what the organization owes if it acts on stale data.
 
An identity can be created and never confirmed. The design does not say if it stays in limbo or expires. That is a policy decision I assumed someone would make.
 
A transaction can stay in "confirming" for hours. The synchrony model gives expected times but no hard timeout or escalation path.
 
### What I'd do differently as a real product
 
I would validate the business case first: who pays, for what unit, at what price. The design is more mature than the commercial model, and that gap would not survive a real budget conversation. I would also resolve the cross-actor state problem before writing another state contract. In production, it becomes a support and trust incident. The governance model, token architecture, and accessibility criteria I would keep mostly as they are.
 
---
 
## Learnings
 
### Governance comes from structure
 
I assumed governance was a rule set written on top of a finished system. It is the opposite. The three stability layers work because the tokens and components were built to make them visible. A token that mixes meaning and raw value cannot be stable by contract. Writing governance down is documentation. Building the system so it can be written down is the real work.
 
### It stopped being a UI problem early
 
I started by designing a wallet interface. During the architecture phase, I saw that the real problem was the data model: what a permission is, which states it has, and how it relates to on-chain transactions. Tokens came from the data model, components from its states, and flows from its decisions. The screens came last. They render the contract. They are not its source.
 
### I think in contracts, and that has a cost
 
Data models, state taxonomies, and governance layers are where my decisions hold up best. I also over-engineer. I reached for abstraction before testing a simpler option. In NEXIA, I elaborated governance before the components were stable and defined states that are rarely needed. I am still learning to separate structural rigor from structural excess.
 
### What I have not resolved
 
I have not tested the contract against real engineering or real user behavior. If an engineering team negotiates it down, with fewer states or exceptions for happy paths, I do not know if the system survives. I also do not know if consequence language works on users tired of consent flows. These are hypotheses, not validated results. Testing them is the reason I am pushing toward an MVP. The goal is not to prove the design is right. It is to find where it is wrong.
 
---
 
*NEXIA: Case study*
*José David Albarrán Velásquez · jdalbpd.me*