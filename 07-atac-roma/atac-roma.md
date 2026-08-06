---
title: "ATAC Roma"
subtitle: "Designing the official ticketing platform — from fragmented channels to a unified digital system"
role: "Senior Product Designer — sole contributor"
type: "Self-directed product strategy investigation"
stage: "0→1, Phase 1 specification"
platforms: ["Progressive Web App (PWA)", "mobile-first with desktop parity"]
context: "Public transit operator, Rome"
tools: []
tags: ["product-strategy", "information-architecture", "design-systems", "concept-project"]
status: "concept"
date: "2026"
summary: "A product strategy reframing of Rome's public transit ticketing — from 'the app is confusing' to 'the operator doesn't own the channel' — carried through into a full PWA specification."
---

# ATAC Roma

**Designing the official ticketing platform — from fragmented channels to a unified digital system**

---

## Context

ATAC is the public transit operator for Rome — one of the densest and most fragmented urban mobility systems in Europe. Buses, metro, tram, regional rail, zone-based fares, multiple ticket categories, a mix of residents and tourists arriving from every language, and a legacy of digital assets scattered across vending machines, tobacco shops, kiosks, third-party apps (Moovit, moovygo, Trenitalia), and an official website that could display fare information but could not sell a ticket.

I built this project as a sole contributor, outside of any client engagement, to answer a specific question: what does a transit product look like when the first design decision is not about the interface, but about who owns the channel?

That question reframed everything downstream. Most digital transit redesigns start with the existing app and ask how to improve it. I started by asking whether the existing app was the right asset to improve at all — and concluded, early in the diagnosis, that it was not. ATAC did not have a product problem. It had a product strategy problem wearing an interface as its symptom. A significant share of ATAC's digital transactions was happening on platforms ATAC did not control, which meant the organization was ceding margins, behavioral data, brand trust, and direct relationship with its users to intermediaries. No amount of interface refinement on the existing app could solve that.

The output is not a redesign. It is a product specification that treats the missing channel as the primary artifact to build — a Progressive Web App positioned as the official ticketing platform, with an information architecture restructured around user mental models rather than fare nomenclature, a component system designed to serve six ticket categories without color-coding its way out of complexity, and three priority flows fully specified: first-time purchase, recurring monthly renewal, and ticket validation. Eight slides in the published Behance case study, plus the extended specification this document presents.

The case study documents the reasoning behind each decision. Where I made trade-offs, I say what I traded. Where the impact is hypothetical rather than measured, I say so — and I say why the hypothesis is defensible anyway.

---

## Problem statement

### The problem as it was usually framed

If you had asked anyone using ATAC's digital channels in the years before this project what the problem was, you would have gotten some version of the same answer. The app is confusing. The vending machines break. The website does not let you buy a ticket. The third-party apps charge a markup. There is no single place to renew a monthly pass.

All of those descriptions are accurate. None of them is the problem.

Those are symptoms of a deeper condition, and designing against them in isolation would produce exactly what the market had already produced: a collection of partial solutions, each addressing a surface complaint, none of them touching the structural fault underneath.

### The real problem

ATAC did not control the channel where a meaningful share of its digital transactions was happening.

That is the sentence the entire project rests on. It is not an interface observation. It is a product strategy observation. A significant portion of the tickets ATAC was effectively selling were being sold through Moovit, moovygo, Trenitalia's commercial layer, tobacco shops with third-party POS systems, and vending machines operated by external contractors. Every one of those channels absorbed margin, captured behavioral data, owned the moment of customer contact, and inserted itself between the operator and its users.

The consequences compound in directions that are not obvious until you trace them.

ATAC could not see how its users actually bought tickets, because the transaction data lived in systems it did not query. It could not improve the purchase experience for recurring users, because the recurring users were loyalty customers of the intermediaries, not of ATAC. It could not respond to service disruptions through its own channel, because its own channel did not have enough of the audience to respond to. And when a user needed a ticket urgently — the bus approaching, the turnstile ahead — the channel they reached for was whichever third-party app was already installed on their phone, not the operator's official route.

The interface was not the problem. The interface was the visible edge of a problem that lived two layers up: the operator had delegated its customer relationship to intermediaries and inherited, as the consequence, a fragmented digital presence that could not be fixed by redesigning any one of its pieces.

### Why improving the existing app would not have worked

The obvious path — improve the existing native app, make it better, close the gap on the third-party experience — was not available. Not because the work was impossible, but because the work was structurally insufficient.

A native app, no matter how well designed, would still carry the installation barrier. Tourists arriving in Rome for three days would not install it. Occasional users would not install it. Lower-income residents on older handsets would face friction installing it. App Store review cycles would slow every operational response. Dual maintenance across iOS and Android would consume resources that the operator needed to spend on the problem one layer up.

More importantly: even a perfect native app would not, by itself, recover the channels ATAC had already ceded. Users already habituated to Moovit would not switch to a better-looking ATAC app. Tobacco shop transactions would not migrate on their own. The vending machine fleet would not become less unreliable because the app improved. Each of those channels required a different lever, and the lever was not a better app — it was a single official channel that could credibly replace them because it was accessible at the exact moment and place the need arose, without prerequisites.

The problem was not one of interface. It was one of ownership. And ownership could not be recovered by polishing an asset; it could only be recovered by building the missing one.

### Why this becomes a design problem, not a business one

At this point a legitimate reader would ask: this sounds like a strategy problem for ATAC's executive team, not a design problem. Why is a designer framing it this way?

Because the strategic decision and the design decision are the same decision. "Build a PWA positioned as the official channel" is simultaneously a product strategy call and an architectural design call — it determines what the digital product is, where it lives, how users reach it, what platforms it can serve, what it can do offline, and how the rest of the system is organized around it. A business stakeholder can declare the strategy; only a designer translates it into a coherent product specification that holds under real operational conditions.

What makes this a design problem rather than a business problem is that the decision cascades through every subsequent choice. If the channel is a PWA, the information architecture cannot rely on "open the app and tap around" as its default interaction model — it has to work for a user arriving via a shared URL at a bus stop. If the channel is a PWA, the component system has to render correctly on lower-end handsets with inconsistent connectivity. If the channel is a PWA, the return-user experience cannot assume the user remembers a state they last saw in a different browser session — it has to reconstruct that state from persisted identity, on demand, in under a minute.

The designer's job, in a reframing of this kind, is to take the strategic insight and prove it is buildable. That proof is the case study.

### What the project is betting on

The project is betting that three claims are simultaneously true. First, that a PWA can serve as the official channel for a public transit operator in a major European capital, with the reliability and trust a civic infrastructure service requires. Second, that information architecture organized around user mental models — tourist, resident, regional traveler, facilitated categories — can replace a decades-old fare taxonomy without losing the coverage the taxonomy provided. Third, that a component system designed for complete state coverage, rather than color-coded variety, can render six ticket categories with one component and still remain readable.

None of those claims is individually radical. Holding all three together, in a single product specification that holds up as a coherent whole, is the design problem this project documents.

---

## Constraints

This was a self-directed project. No client brief, no deadline, no budget, no stakeholder negotiating scope against timeline. The conventional constraints of a commercial engagement did not apply, and I will not pretend they did.

What did apply were the structural constraints the domain imposes on anyone designing a product in this category. Public transit in a major European capital is not a greenfield category. It is a space where the physics of the service, the shape of the user population, the reliability of the infrastructure, and the legal and operational position of the operator all set hard edges that a design has to absorb before the first wireframe.

### The transit system itself is the first constraint

Rome's transit network is buses, metro, tram, and regional rail, operated under ATAC for urban services and Trenitalia for regional connections, with fares organized across multiple zones and categories — time-limited tickets, day passes of several durations, a weekly, monthly and annual passes for residents, reduced fares for qualifying categories (under-19, unemployed, reduced ISEE, seniors, disability), and regional titles with zone-based pricing that changes depending on the origin-destination pair.

A ticketing platform for this system cannot simplify the catalog by removing options. The options exist because the service exists: a tourist on a three-day visit genuinely has different needs than a resident renewing a monthly pass, and a regional commuter coming in from the Castelli Romani genuinely cannot use the same ticket as a city user. The design's job is not to hide the complexity. It is to organize the complexity so that each user encounters only the subset relevant to them.

This constraint ruled out the shortcut most transit apps take — show everything in a flat list and rely on search. Flat lists work when the catalog is homogeneous. This one is not. A tourist scanning a flat list sees twenty-two titles and cannot tell which ones apply to their situation. A resident scanning the same list has to scroll past eighteen options that do not concern them to reach the two that do. The catalog's real structure had to be rendered as the architecture, not left for the user to discover.

### Infrastructure reliability is not a design assumption

A transit product cannot assume continuous connectivity. Users enter the metro and lose signal. Users arrive at bus stops in neighborhoods with patchy coverage. Users open the app on older handsets that negotiate slower network sessions. Users stand in underground corridors where the only thing the device is doing reliably is displaying what was loaded before the signal dropped.

This constraint made the choice of platform non-negotiable. A product that requires a live connection to tell a user what tickets are available, what they cost, and whether a purchase went through is a product that fails at the exact moments transit users need it most. The PWA decision is not an aesthetic preference for web over native — it is the only architecture that supports partial offline functionality as a first-class behavior: critical reference information (ticket types, pricing, validity rules) cached and available, transaction states persisted through connectivity drops, and purchased tickets renderable and validatable without a live connection at the moment of use.

Real-time data — arrival times, service disruptions, live validation status — sits on top of that offline baseline. The product shows real-time information when the network is available, and degrades gracefully to cached state when it is not. That fallback is not a feature. It is the minimum condition for the product to be trustworthy in the environment it operates in.

### The user population is bimodal, and the product serves both poles from the same surface

The constraint most transit redesigns fail at is serving a tourist and a resident from the same product without fragmenting it. The two populations have almost nothing in common from a product standpoint.

A tourist in Rome for three days is in high-novelty, low-frequency mode. They do not know the zone system. They do not have a stored payment method. They do not know which ticket applies to the trip they are about to take. They need the product to answer "how do I get around Rome?" without assuming any prior knowledge, and they will use the product perhaps five times total before they leave.

A resident is in low-novelty, high-frequency mode. They know the zone system, they renew the same monthly pass every thirty days, they have a stored payment method, and the last thing they want is a product that re-explains the catalog every time they open it. The product, for them, is a one-screen task: renew, validate, done, under a minute, preferably without thinking.

These are not two personas to optimize for in sequence. They are two simultaneous realities the same information architecture has to serve — without asking either user to navigate a product designed for the other. This constraint shaped the home screen (contextual entry points tied to user profile rather than a uniform feature tour), the architecture (four top-level categories organized around travel intent rather than fare type), and the return-user experience (persistent identity decoupled from the transit pass, so the system can surface the right primary action the moment a user returns).

### The operator's position is a constraint the design has to respect

ATAC is a public transit operator, not a consumer tech company. That distinction matters at the level of what the product is allowed to do, what legal and accessibility standards it has to meet, what relationships with third parties it cannot unilaterally break, and what the product represents to the city.

The design cannot, for example, simply route users around Trenitalia for regional titles — Trenitalia is a legitimate partner for the rail segment and regional ticketing runs on a shared legal framework. The design cannot drop the tobacco shop channel overnight — tobacco shops are a distribution network with their own contractual relationships and a real role in serving users without smartphones. The design cannot promote itself as "the only legitimate way to buy tickets" when multiple legitimate ways exist. What the design can do is position the official PWA as the canonical channel — the one ATAC controls, the one that works when the others fail, the one the operator can point to as the reference experience — while respecting that the broader ecosystem continues to exist around it.

Accessibility is a related constraint. A public service product is not free to treat accessibility as a post-launch audit layer. WCAG compliance is a legal requirement in Italy and the EU under the EAA (European Accessibility Act) for services of this category. The design has to absorb that from the first component.

### No validation loop with real users

This is the constraint to name honestly, the same way I named it in NEXIA. I had no users to test with. No tourists stumbling through first-time purchase in a non-native language. No residents timing themselves on monthly renewal. No regional commuters trying to understand the zone diagram. No accessibility users navigating the component system with assistive technology.

Every design decision in this project is defensible on the basis of reasoning — from the structure of the fare system, from documented patterns in adjacent transit products, from established research on consent flows, checkout flows, and offline-capable applications. None of it is validated by contact with real usage. The expected impact section later in the case study says explicitly that the impact is hypothetical, based on the problem diagnosis and the design decisions, and I do not claim otherwise.

### What I chose not to constrain

One decision I want to name. I could have scoped this project down to a single flow — just the tourist first-purchase, or just the monthly renewal, or just the ticket validation — and delivered a tighter but narrower artifact. That would have been easier to produce and easier to present.

Instead, I specified the full Phase 1 product: three priority flows, a complete component system, an information architecture that serves four user profiles, a PWA architecture decision with its full rationale, and an expected-impact section that names both what the project claims and what it leaves hypothetical. The point of the exercise was to see whether the ownership reframing actually held up as a coherent product specification, or whether it collapsed when pressure-tested against the full scope of a working transit platform. Narrowing the scope would have made the reframing easier to defend on paper and impossible to defend as a product.

---

## Process & decisions

Three decisions carry the weight of this project: the choice of platform (PWA over native app), the structure of the information architecture (user mental model over fare nomenclature), and the shape of the component system (complete state coverage over visual differentiation). These are not flows. They are architectural calls upstream of every screen.

I chose them deliberately, and not because they were the most visually interesting decisions to present. Each of the three resolves one of the three constraints from the previous section — the PWA choice resolves infrastructure reliability, the information architecture resolves the bimodal user population, and the component system resolves the complexity of the fare catalog. Together they form the structural skeleton of the product. Everything else is the flesh on those bones.

What follows is each decision written the same way: what I decided, why, and what I deliberately did not choose.

### Decision 1 — The PWA as the official channel

A Progressive Web App replaces the native app as ATAC's official digital ticketing platform. The native app is not improved, replaced in place, or kept as a secondary option. The PWA is the canonical channel.

The reasoning operates at three levels. At the product strategy level, the PWA is the only architecture that recovers ownership of the channel — no installation barrier means no user falls out of the funnel before they start, which means no reason for a third-party app to be the default tool in the user's hand when the bus is arriving. At the infrastructure level, the PWA supports partial offline functionality as a first-class behavior: ticket catalog, pricing, validity rules, and purchased-ticket rendering all work without a live connection, which is the minimum condition for a product that operates inside metro tunnels and underserved urban zones. At the economics level, a single codebase removes the dual-maintenance tax of iOS plus Android plus the review cycle latency that slows every operational response.

The PWA also dissolves a secondary problem that is not obvious until you look at the user population. A tourist arriving in Rome for three days will not install a native app for a service they will use five times. A lower-income user on an older handset will face real friction installing one. An occasional user who needs a ticket once a month will not remember whether they already have the app installed. A PWA collapses all three of those frictions into a shared URL that works immediately, everywhere, on any device capable of rendering a modern browser.

What I rejected was the improved-native-app path. It is the obvious move, and it is what most transit operators in ATAC's position would default to. I rejected it because a better-looking native app does not solve the ownership problem — it only makes the existing asset less embarrassing. A user habituated to Moovit does not migrate to a native ATAC app because the ATAC app's interface improved. They migrate because the ATAC app is the only option available at the moment they need a ticket, which requires removing the precondition that would have stopped them from reaching it in the first place. That precondition is installation. The native-app path cannot remove installation, by definition. So the native-app path cannot solve the problem.

I also rejected the dual-track approach — PWA plus native app, running in parallel, user chooses. That approach looks safer and is strictly worse. It splits the development effort, splits the user base, dilutes the message about which channel is canonical, and preserves the exact fragmentation the project was trying to resolve. If the PWA is the official channel, the native app is not. Keeping both is the decision not to decide.

### Decision 2 — Information architecture structured by user mental model, not fare nomenclature

The existing ATAC catalog organized tickets the way the operator organizes its fare management system — by technical codes, administrative categories, and the internal taxonomy that makes sense to someone reading a regulatory document. That structure is correct for back-office operations. It is not the structure the user arrives with.

I replaced it with four categories organized around travel intent: **Tourist** (titles designed for a specific stay with no renewal commitment), **Citizen** (monthly and annual passes for residents of Roma Capitale), **Regionale** (titles with regional coverage, prefaced by an explanatory component on the zone system), and **Facilitated** (reduced fares for qualifying categories — under-19, unemployed, disability, reduced ISEE, seniors). The question that structured the architecture is not "what ticket do you want to buy?" but "how do you move around Rome?"

The reasoning is that the user does not arrive with a ticket category in mind. The user arrives with a trip in mind — or, more often, a pattern of trips over a period of time. The architecture has to meet the user where their decision actually starts: with their profile, their context, and their intended use of the service. Once the user is in the right category, the specific title surfaces. Starting from the title and asking the user to classify themselves backward into the catalog — the way the old structure operated — inverts the decision flow and asks the user to do translation work the system should have done.

This structure also resolves the bimodal population problem at the architecture level. A tourist landing on the home screen sees Tourist as the first category and enters a flow designed for high-novelty, low-frequency use. A resident lands on the same home screen and sees their existing subscription surfaced as the primary action — renewal in one tap, no navigation required — because the system has decoupled user identity from the transit pass and can recognize the returning user before they have chosen a category. Same information architecture, two distinct entry patterns, zero fragmentation.

What I rejected was the flat catalog with search. It is the pattern most transit apps default to, and it fails for exactly the reason it fails in every domain where the catalog has real structure: search requires the user to already know what they are looking for, and the user who does not know is precisely the user who most needs the architecture to help them. A tourist in Rome does not search "time-limited tickets." A tourist searches "day pass" and finds nothing, because the operator calls it "24 hours ticket." The translation friction kills the purchase before the system even renders options.

I also rejected the option to preserve the existing taxonomy and layer a friendlier search or filter on top. It is the least-disruptive path and it is a patch, not a solution. The underlying catalog still reflects the operator's internal model; the user is still being asked to understand that model in order to navigate it; the filter is only reducing the volume of confusion, not removing its source. Replacing the architecture at the root was more work, and it was the only choice that actually changed the product's relationship to the user.

### Decision 3 — One component, six tickets, zero color differentiation

The component system renders all six primary ticket types — time-limited, 24 hours, 48 hours, 72 hours, one week, and the rechargeable multi-use ticket — with a single card component. No ticket category has its own color treatment. No type carries a distinct visual identity. Differentiation happens entirely through content, hierarchy, and state.

The reasoning is a structural one, not a visual one. A component system that assigns a dedicated color to each ticket category collapses the moment a new category is added — either the palette has to expand, risking color drift, or the new category reuses an existing color, confusing the distinction the colors were meant to enforce. More importantly, color differentiation at the category level does not actually help the user. The user does not confuse a 24-hour ticket with a 72-hour ticket because they look similar; they confuse them because they do not yet know which duration applies to their trip. That confusion is solved by information architecture and hierarchy, not chromatic variety.

The harder design problem, and the one the component system actually had to solve, is **complete state coverage**. Each ticket card has to render correctly in default state, in selected state, and in error state. The selected state has to communicate intent before confirmation without triggering the transaction. The error state has to explain what failed — payment declined, session expired, network lost mid-purchase — and offer a recovery action specific to the failure type. A component that renders cleanly in the default state but breaks down in error is a component that fails at the exact moment the user most needs it to hold together.

The return-user flow depends on a related decision that is not an interface decision at all — it is a data architecture decision. User identity and the transit pass are decoupled and linked persistently, so that the system can surface pass renewal as the primary action on return visits without requiring the user to navigate, filter, or re-select. A resident renewing their monthly pass is not exploring options. They are completing a task that should take under a minute. The architecture has to make that task a one-screen interaction, and it can only do so because the user-identity layer knows which pass the user holds and whether it is approaching expiration.

What I rejected was the color-per-category system. It is the pattern most consumer transit apps use, and it feels visually cleaner in early mockups because it creates an immediate visual taxonomy the user can scan. I rejected it because the cleanness is an illusion that breaks under operational reality: when ATAC introduces a new ticket category (the system is designed to absorb one without restructuring), the color system has to accommodate it, and at that point either an existing color gets reused or the palette becomes unmanageable. A component that differentiates by content rather than color does not have that failure mode.

I also rejected the maximalist state-coverage approach — defining every possible state for every possible edge case before shipping Phase 1. It is tempting because it looks rigorous, and it produces design documentation that is easy to show off. I rejected it because Phase 1 does not need twelve states per component; it needs the three states that cover the flows Phase 1 actually ships, designed well enough that Phase 2's additional states can extend them without rework. The discipline is not "specify everything." It is "specify exactly what is needed to make the current scope trustworthy, and design the system so future scope can be added without breaking what was specified."

### A note on the remaining decisions

The project contains additional decisions I have not expanded here — the return-user home screen surfacing subscription as the primary card, the session-ticket validation flow showing both a success confirmation and a revalidation QR code from the same screen, the offline-first pattern for critical reference information, the handling of payment errors that preserves user state rather than restarting the flow. They are documented in the published Behance case study and the Figma file.

I left them out here because the three decisions above carry the reasoning that matters. The rest are applications of the same principles to narrower surfaces.

---

## Artifacts

Everything listed here exists. Nothing below describes work that is planned, sketched, or partial.

### Strategic diagnosis

A written diagnosis that reframes the problem from "ATAC's app is confusing" to "ATAC does not control the channel where its digital transactions happen." The diagnosis maps the existing fragmented landscape — six distinct channels including third-party apps (Moovit, moovygo, Trenitalia), tobacco shops with independent POS systems, out-of-order vending machines, onboard purchase, physical kiosks, and an official website without purchase capability — and traces the structural consequences of that fragmentation on margin, behavioral data, brand trust, and the operator's ability to respond to service conditions. The diagnosis argues that fixing any one of those channels would have been a patch on a structurally broken foundation, and that the correct response was to build the missing canonical channel rather than repair the ceded ones.

### PWA architecture decision rationale

A documented comparison of three candidate architectures — traditional website, Progressive Web App, and native app — evaluated against four criteria: installation friction, offline capability, single codebase, and time-to-access. Each architecture is scored against each criterion with the specific implication for ATAC's user population and operational context. The document concludes with the PWA decision and the reasoning trail that supports it, including the specific offline behaviors the PWA has to support as first-class operations (ticket catalog cached, pricing and validity rules available without connection, purchased tickets renderable for validation offline).

### Information architecture with four user profiles

A four-category catalog structure — Tourist, Citizen, Regionale, Facilitated — built on travel intent and user profile rather than fare taxonomy. Each category is defined by the user it serves and the titles it contains, not by the operator's internal classification system. The architecture includes explicit handling for the Regionale category (which requires a zone-system explainer component because regional fares depend on origin-destination pairs) and for the Facilitated category (which covers five distinct qualifying conditions under one organizational umbrella without fragmenting them into separate top-level entries).

### Home screen architecture for bimodal users

Two distinct home-screen patterns rendered from the same architecture, surfaced contextually. A first-time or unauthenticated user sees the four-category entry point with the question "How do you want to move?" as the primary organizing frame. A returning authenticated user sees their active subscription card as the primary surface, with the category selector demoted to a secondary region and renewal promoted as the default action. Same information architecture, same component vocabulary, two entry experiences — without forking the product.

### Component contract — Ticket Card

A single component renders all six primary ticket types (time-limited, 24 hours, 48 hours, 72 hours, one week, rechargeable multi-use) without category-based color differentiation. Each card is specified across three states: default (the scannable list view), selected (pre-confirmation intent without triggering purchase), and error (payment failed, session expired, or connection lost mid-purchase, each with a specific recovery action). Differentiation between ticket types happens through content hierarchy, not chromatic variety — which is what makes the component extensible to a seventh or eighth category without restructuring the system.

### Data architecture — decoupled user identity and transit pass

A structural decision documented as part of the component system. User identity and the transit pass are stored as persistently linked but independently addressable entities. This allows the return-user experience to surface the correct primary action — renewal of the specific pass the user holds — without requiring the user to navigate, filter, or re-select. The architecture is the condition of possibility for the sub-minute renewal flow; without it, the home screen could not recognize the returning user's pass state on load.

### Three priority flows — PWA specification

**First-time purchase** — tourist or occasional user arrives without prior state, navigates from "How do you want to move?" through category selection, title selection, purchase, and validation. The flow assumes no stored payment method, no prior identity, and no familiarity with the fare system.

**Recurring monthly renewal** — resident returns with an active pass approaching expiration. The home screen surfaces the active subscription as the primary card. Renewal is a single primary action from the home screen, using stored payment credentials, designed to complete in under a minute. No navigation through the category system is required for the task.

**Ticket validation** — user holds a purchased ticket and needs to validate it at the turnstile or on board. The validation screen shows both a success confirmation and the QR code for revalidation, accessible from the same surface. Error states — payment failed, ticket expired, validation unrecognized — are each specified with a specific recovery action, not a generic error message.

### Expected impact framing

A written section that explicitly marks the project's outcome claims as hypothetical — based on the problem diagnosis and the design decisions, not on measured user behavior. The framing distinguishes between the outcomes the design is built to enable (sub-minute renewal, six fragmented channels replaced by one canonical platform, zero installation friction) and outcomes that would require user validation to claim as evidence. This honesty layer is an artifact of the project because the project was designed to be defensible without overclaiming, and that defensibility is itself part of what the case study demonstrates.

### Forward compatibility — features the architecture absorbs without rework

A short section documenting three features that are not part of Phase 1 but that the system was explicitly designed to incorporate without structural rework: a comments section on news items for direct user feedback, a service rating system with aggregated data for ATAC, and pass gifting between users as a social layer. Listing these is not speculation. It is evidence that the architecture was designed as a living system — not as a closed deliverable — and that the decisions made in Phase 1 were made with the shape of Phase 2 already visible.

### Published Behance case study

An 8-slide visual case study published on Behance that renders the strategic diagnosis, PWA rationale, information architecture, component system, priority flows, and expected impact as a coherent visual narrative. The Behance serves as the visual and narrative complement to this extended specification — this document is the reasoning layer, the Behance is the rendering layer. Both exist. They are not duplicates of each other; they are two depths of the same project.

---

## Outcomes

This project did not ship, did not enter a pilot, and was not validated by user behavior in production. Any outcome framed as measured evidence would be invented. What follows is what the project produced — in terms of structural decisions, reasoned claims, and artifacts that can be evaluated on their own terms.

### What the project produced

A complete Phase 1 specification for a public transit product in a major European capital — built from a reframed problem diagnosis, an architectural decision (PWA over native app), an information architecture restructured around user mental models, a component system specified for complete state coverage, a data architecture that decouples user identity from the transit pass, three priority flows fully specified across first-time purchase, monthly renewal, and ticket validation, an explicit forward-compatibility layer for Phase 2 features, and an expected-impact section that distinguishes between claims the design is built to enable and claims that would require user validation. Eight slides in the published Behance case study render the specification visually; this document carries the reasoning.

### What the system resolves at the structural level

The project demonstrates that three structural problems of public transit ticketing can be resolved simultaneously through a single coherent specification rather than through partial fixes to the existing fragmented landscape.

The **ownership problem** is resolved by the PWA decision. Moving the canonical sales channel off the native-app and into the browser removes the installation barrier that had been routing users to third-party intermediaries. The operator recovers the channel, the transaction data, and the direct relationship with users without having to negotiate each channel away from its current intermediary one at a time.

The **bimodal user problem** — tourist and resident served from the same product surface — is resolved by the information architecture and the return-user home screen. Tourists encounter the four-category entry point designed for high-novelty, low-frequency use; residents encounter their active subscription as the primary surface with renewal as the default action. Same information architecture underneath, two distinct entry experiences surfaced contextually, without forking the product into separate apps or modes.

The **fare catalog complexity problem** is resolved by the component system and the architectural choice not to differentiate ticket categories through color. One component renders six ticket types and accommodates a seventh or eighth without restructuring. The complexity that exists in the fare system is preserved because the service requires it; what changes is that the user no longer has to absorb the operator's internal taxonomy in order to navigate it.

### What the design is built to enable

The project's expected impact is explicitly hypothetical, as the final section of the published case study states. The outcomes below are claims about what the design, if built as specified, is architected to support — not measured results.

**Six fragmented channels consolidated into one canonical platform.** The six channels identified in the diagnosis — third-party apps, tobacco shops with independent POS, onboard purchase, out-of-order vending machines, physical kiosks, and the non-transactional official website — are not deprecated by the PWA. They continue to exist within the broader distribution ecosystem. What changes is the existence of a canonical channel the operator controls, designed to function as the reference experience and to work reliably at the moments the other channels fail. The claim is not that fragmentation disappears; it is that the operator now owns an unambiguous answer to "where do I go if I need a ticket right now."

**Monthly pass renewal designed to complete in under a minute.** This target is structural, not measured. It is what the design is architected to enable through the combination of persistent user identity, the decoupled transit pass, stored payment credentials, and a home screen that surfaces the active subscription as the primary action on return. Whether real users complete renewal in under a minute depends on factors the design alone cannot control — network conditions, payment processor latency, user familiarity with the product. What the design does is remove the navigation, filtering, and re-selection steps that would otherwise make sub-minute renewal impossible. Sub-minute is the architectural ceiling the flow is built against, and the flow is built to approach it.

**Zero installation friction.** This claim is not hypothetical. It is a direct consequence of the PWA architecture. A user who types the URL, follows a shared link, or scans a QR code at a bus stop reaches the product with no precondition. No App Store download. No Play Store review cycle. No dual-platform maintenance decision about which OS to support. No installation abandonment at the last step before first use. The claim is architectural fact, not projected metric.

### What the documentation makes defensible

Every decision in this project is documented with its reasoning and the alternative it rejected. The PWA choice is defended against the improved-native-app path and the dual-track path. The information architecture is defended against flat-catalog-with-search and against preserving-the-old-taxonomy-with-a-filter-on-top. The component system is defended against color-per-category differentiation and against maximalist state-coverage-before-shipping. Each rejected alternative is written the way it would be argued by a legitimate reviewer, and each rejection is grounded in why the alternative fails the constraints the project was operating under.

That structure is the project's real outcome for a reader evaluating it. A case study that presents only the final design presents conclusions. A case study that documents the rejected alternatives presents the reasoning that produced those conclusions. The difference is the difference between showing a redesign and showing a designer reframing a problem.

### What the project is evidence of

The project is evidence of a specific capability: reframing a product problem at the strategy level and carrying the reframing through into a coherent product specification without losing it in the details. It is evidence that I can look at a fragmented digital landscape and identify that the problem is structural rather than visual — and that I can then defend that identification with a full set of architectural, informational, and component-level decisions. It is evidence that I document what I decided, why, and what I deliberately chose not to build.

It is not evidence of shipping the product. It is not evidence of negotiating scope with a public-sector stakeholder. It is not evidence of validating the architecture against tourists trying to buy tickets under time pressure at a bus stop. Those are different capabilities, demonstrated by different kinds of projects.

### What a reader is asked to evaluate

Whether the reframing holds up. Whether a product strategy reframing — from "the app is bad" to "the channel is ceded" — is the reframing the diagnosis actually supports. Whether the PWA decision survives scrutiny as the right resolution to the ownership problem, not just a convenient technical call. Whether the information architecture serves both a tourist and a resident without forcing either to work through a product designed for the other. Whether the component system is defensible as structurally extensible rather than merely minimalist.

The project does not ask to be evaluated on outcomes it did not produce. It asks to be evaluated on the reasoning it does produce, and on whether that reasoning would hold up if the design were built.

---

## Learnings

### The reframing did not happen at the start — it happened during the work

I started this project thinking it was a redesign. The existing ATAC app was confusing, the fragmentation across channels was obvious from a surface scan, and the instinct was to build a better version of what already existed. That framing was wrong, and the project taught me it was wrong — not through a single insight but through the slower process of actually mapping the ecosystem.

What changed my understanding was tracing where the value was going. As I documented the diagnosis — third-party apps, tobacco shops, vending machines, onboard purchase, the non-transactional website — a pattern emerged that the surface view had hidden. ATAC was not losing users to a better competitor. ATAC was operating a transit service whose digital revenue, behavioral data, and customer relationship were flowing to intermediaries the operator did not control. The fame, if you want to call it that, belonged to the platforms that had inserted themselves between the operator and its users. ATAC was selling the tickets; someone else was getting credit for the experience.

Once I saw that pattern, the project reorganized itself. The interface was not the problem. The interface was the last thing I needed to decide. The project became a question of ownership before it became a question of design.

I do not think I could have reached the reframing by reasoning from first principles at the start. I reached it by doing the work — by making the diagnosis thorough enough that the structural pattern became visible on its own. That is a method I want to trust more deliberately going forward: the diagnosis is not a preamble to the design work; the diagnosis is where the design problem is actually defined.

### I almost designed the wrong product, and the pull was visual complexity

Every transit redesign in a portfolio context faces the same temptation. Color-coded categories, stylized transit maps, route-pattern illustrations, animated onboarding that walks the user through the zone system. These things look good in Dribbble. They communicate effort at a glance. And they have almost nothing to do with whether the product works.

I caught myself reaching for them early. The impulse was to differentiate each ticket category with its own color, to render the fare catalog with the kind of visual taxonomy that makes design portfolios legible in a three-second scan. I had to stop and ask what the color was doing. The answer was that it was doing nothing for the user. A tourist does not confuse a 24-hour ticket with a 72-hour ticket because the colors look similar. They confuse them because they do not know which duration applies to their trip. That problem is solved by information architecture and content hierarchy, not by chromatic variety.

The lesson is more specific than "avoid visual complexity." The lesson is that in a portfolio project, the designer is serving two audiences at once — the reader evaluating the work and the hypothetical user the work is for — and the first audience's expectations can quietly corrupt the second. Color-per-category would have made the Behance slides look richer. It would have made the component system worse. That trade-off has to be recognized before it is accepted, and in this project I recognized it just in time.

### Without data, I can only be rigorous, not right

This project revealed a limit I had sensed but not articulated clearly. I do not have access to real data. I do not have ATAC's transaction logs, session recordings, or user interviews. I cannot tell you how often tourists abandon the purchase flow at the payment step, or how many residents would use a sub-minute renewal if it existed, or whether the Regionale category is the right level of granularity for the regional commuter population.

What I can do — and what this project shows I can do — is reason from structural evidence to defensible conclusions. The PWA decision is defensible without user testing because the installation barrier is structural, not preferential. The information architecture is defensible without interviews because the old taxonomy was the operator's internal model, and the user's decision flow does not start there. The component system is defensible without usability studies because state coverage is a property of the system, not a property of user behavior.

But defensible is not the same as validated. Every claim in this case study could turn out to be wrong in contact with real usage. The tourist I imagined may not behave like the tourist that actually lands in Rome with a dying phone battery and no Italian. The resident whose renewal I designed to take under a minute may have a payment method their bank rejects on the third retry. The Regionale user I assumed would welcome a zone-system explainer may already know the zones better than any UI can teach.

I am not pretending to have solved what I cannot yet measure. The case study names the gap explicitly, both in the expected-impact section and here. What I want to name in the learnings is the shift in my understanding of what it means to design without data: it does not mean the design is speculative. It means the design is defensible on structural grounds and falsifiable in contact with users. Both of those are true simultaneously, and both of them matter.

### What ATAC taught me that NEXIA did not

NEXIA taught me that I think in contracts and that I tend to over-engineer. ATAC taught me something different — it taught me that when I have an organizing principle clearly held from the beginning, the work compresses.

I spent less time on ATAC than on NEXIA, not because ATAC is smaller, but because I held the ownership reframing consistently from the moment it cristallized. Every subsequent decision — PWA over native, information architecture over fare nomenclature, component system without color differentiation — could be checked against the same question: does this serve ownership, or does it drift from it? Decisions I would have debated for hours in NEXIA were resolved in minutes in ATAC, because the principle was doing the filtering.

What this revealed is that my weakness in NEXIA was not engineering instinct — it was the absence of a principle strong enough to bound the engineering instinct. NEXIA had many good decisions, each locally correct, reasoned through in isolation. ATAC had fewer decisions, all of them anchored to a single structural claim. The result is that ATAC reads tighter, the reasoning lands faster, and the case study requires less defense because the reframing is doing most of the defense on its own.

I want to carry that forward. Not as a formula — not every project has a clean ownership reframing available — but as a practice. Before I reach for the component system, before I start sketching flows, before I even open Figma, I want to ask whether the organizing principle is clearly held. If it is, the work compresses. If it is not, the work expands, and I produce more, and the more is not better — it is just more.

### The question I have not resolved

Three questions this project leaves open, and they are not the ones NEXIA left me with.

First, whether the ownership architecture survives if the operator itself does not have the political mandate to build it. The PWA decision, the information architecture, the component system — none of it matters if ATAC's institutional structure does not support a full migration away from the fragmented status quo. A public-sector operator is not a single decision-maker. It is a network of departments, contracts, and stakeholder relationships that can block a reframing for reasons that have nothing to do with the reframing's correctness. I designed the product. I did not design the political capability to adopt it, and I am not certain what a designer can do about that.

Second, whether the four-category taxonomy — Tourist, Citizen, Regionale, Facilitated — holds for the users who do not fit cleanly into any of them. A resident who is also a regional commuter. A tourist on a long-term stay. A temporary worker who will be in Rome for three months but does not qualify as a resident for the subscription products. These users are not rare. They are the edge of the distribution that most transit architectures either ignore or fragment into awkward intermediate categories. I do not know yet whether the architecture absorbs them gracefully or whether it breaks at the seams.

Third, whether the PWA keeps its architectural advantage over time. In 2026 the PWA decision is defensible because native apps carry installation friction and because offline-first is not yet a solved problem on either iOS or Android. If that changes — if the next generation of native platforms makes offline-first a default and installation a non-issue — the specific rationale I built may need to be re-examined. The ownership reframing would still hold. The platform choice that resolves it might not.

None of these questions has an answer yet. They require the product to exist, the operator to adopt it, and the usage to accumulate. That is the next phase of the work, and it is why — the same way I said at the end of NEXIA — I am pushing toward an MVP. Not to prove the design is correct. To find out where it is not.

---

*ATAC Roma — Case study, extended version*
*José David Albarrán Velásquez · jdalbpd.me*