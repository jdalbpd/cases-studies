# Intérprete di Busta Paga
*Concept project*

## Context

This project started from a real case. A manual review of 19 monthly payslips (cedolini) for an Italian dependent worker found a legally owed tax deduction, detrazione fiscale, missing for 11 months in a row. That is a real, unclaimed amount of about €2,600 to €2,900 in the employee's favor.

Most Italian workers have no easy way to check their own payslip. The math is hard to follow, the terms are technical, and errors like this one can go unnoticed for months. Intérprete di Busta Paga is a concept for a tool that reads a payslip, checks it against the fiscal logic behind it, and explains the result in plain language. I designed it for someone who knows nothing about the topic going in.

## What I designed

- A two-axis state model, one axis for data completeness and one for the analysis result, so the system can show partial or uncertain outcomes without technical jargon or a simple pass/fail
- An ingestion flow that accepts a photo or PDF through OCR, one file or several at once. When a field cannot be read, the user fixes it right there in the result screen, instead of a separate data-entry form
- A rule that missing data can never block navigation. Critical gaps show up as a clear visual marker, but the user can keep moving through the rest of the app
- A language system with Spanish, English, and Italian. Terms like detrazione or TFR stay in Italian no matter which language is selected, so the user can still recognize them on the real payslip, while everything explaining those terms gets translated
- An end-to-end flow across six screens, from the first upload to a multi-month history view, with a different chart logic for each data type: a line chart for net income, an accumulated area chart for severance pay (TFR), and balance-first cards for leave and PTO

## Tools

Figma, Figma Make, Claude

## Product Reality

### Business reality

This tool solves a real information gap. Workers cannot check their own payslip today, so wage errors like the missing detrazione stay hidden for months or years. The business problem is trust. Without a way to verify their pay, workers depend fully on payroll systems they cannot audit.

In production, the tool would reduce two kinds of risk. For the worker, the risk of losing money they are legally owed. For an employer or CAF partner, the risk of looking unreliable if errors keep surfacing after the fact.

The metric that would matter here is not signups. It is the number of confirmed missing detrazioni per user per year, checked against a real CAF review. A high number early on would mean the tool works. A number close to zero after a year could mean two things: the tool is not finding real cases, or most payslips checked were already correct.

The buyer is not obvious yet. A worker might pay to feel more confident about their own payslip, but it is unclear if people would pay for a fiscal-check tool on its own. A more realistic buyer could be a CAF or a union, using the tool to decide which clients need a full fiscal review first.

### Operational reality

A few failure cases would need real answers before this could ship:

- A blurry or partial photo that OCR reads with false confidence instead of flagging it as unreadable
- An OCR provider outage in the middle of a batch upload covering several months
- A user closing the app mid-upload, with some months processed and others still in queue
- A user abandoning the flow right after being asked to fill in a missing vital field
- Last year's detrazione threshold staying active after the yearly fiscal update, so the tool checks the wrong rule against a new payslip
- A manual correction from the user that disagrees with what OCR extracted, with no clear rule for which value should win

### What I'd do differently as a real product

I would start with these failure cases, not the happy path. The core value here, finding a real fiscal error, only holds if the system is honest about when it is not sure. Right now that honesty is designed in principle, but it has not been tested against a messy, real OCR provider yet.

## What I learned

Designing for someone who knows nothing about the subject forced a discipline I did not expect. Almost every state, label, and chart choice had to pass one test: does this help someone unfamiliar with the topic, not does this look clear to me. The two-axis state model only got simple once I stopped trying to name every technical cause and just asked what the user needed to do next.