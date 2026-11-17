# Intérprete di Busta Paga
*Concept project*

## Context

Italian employees receive a monthly payslip (cedolino) that they cannot check. The terms are technical, the math has many layers, and a small error can stay hidden for a year. In the real case behind this project, a manual review of 19 payslips found a tax deduction (detrazione fiscale) missing for 11 months in a row. About €2,600 to €2,900 went unclaimed.

Intérprete di Busta Paga is a concept for a consumer fintech and financial literacy dashboard. It reads a payslip, checks the numbers, and explains each result in plain language. The target user knows nothing about payroll or taxes, and may feel anxious about both. The design goal was trust: show what the system found, why it found it, and what the person can do next.

## Product Reality

### Business reality

- Why it exists: workers cannot audit payroll, so they rely on numbers they cannot read. An error like the missing detrazione only appears if someone checks by hand.
- The problem it solves is not missing data. It is the lack of clarity in a very personal financial document.
- Risk reduced: for the worker, losing money they are legally owed. For a CAF or a union, spending review time on payslips that were already correct.
- Business metric: confirmed missing detrazioni per user per year, checked against a real CAF review. This is a hypothesis, nothing has been measured.
- Buyer: still open. A worker may pay for peace of mind, but a CAF or a union looks like the more realistic buyer.

For trust and comprehension, I would watch three signals, all unmeasured so far. First, how many users open the info button on the detrazione alert and then take a next step. Second, how many users fix a missing vital field after the prompt. Third, how many return to upload the following month.

### Operational reality

A few failure cases need real answers before this could ship:

- A blurry photo that OCR reads with false confidence instead of flagging it as unreadable
- An OCR provider outage in the middle of a batch upload covering several months
- A user closing the app mid-upload, with some months processed and others still waiting
- A user leaving right after being asked for a missing vital field
- Last year's detrazione threshold still active after the yearly fiscal update, so the tool applies the wrong rule to a new payslip
- A manual correction that disagrees with what OCR extracted, with no clear rule for which value wins

### What I'd do differently as a real product

I would start from these failure cases, not from the happy path. Finding a real fiscal error only has value if the system is honest about when it is not sure. The verification logic did well on clean test data, but the OCR tests were not fully blind. Real OCR reliability is still unproven, so the interface shows confidence levels instead of assuming perfect extraction.

## What I designed

- Alerts that explain themselves. The detrazione alert checks the legal income threshold before it fires, and the screen shows that reasoning in plain words. A small info button explains the term for users who have never heard it.
- A two-axis state model: one axis for data completeness, one for the analysis result. The system can show a partial or uncertain outcome without jargon and without a simple pass or fail.
- Error handling for the calculations. When data is missing, the system does not guess. The user fixes the field inside the result screen, not in a separate form, and a missing vital field is marked as urgent.
- A rule that nothing blocks navigation. Even a critical gap shows as a clear marker, and the user keeps moving through the rest of the app.
- Spanish, English, and Italian. Terms like detrazione or TFR stay in Italian in every language, so the user can find them on the real payslip. Only the explanations around them are translated.
- A component set that can scale. Leave and PTO balances get separate cards, because one counts days and the other hours. A third color is reserved for states that are normal but worth a look, like a negative leave balance, so they never look like an error. The same card pattern is reused for the missing-month notice.
- Six screens, from first upload to a multi-month history. Each data type gets its own chart: a line for net income, an accumulated area for severance pay (TFR), and balance cards for leave and PTO. Exact numbers stay visible next to every chart.

## Tools

Figma, Figma Make, Claude

## What I learned

Designing for someone who knows nothing about the subject forced a discipline I did not expect. Almost every state, label, and chart choice had to pass one test: does this help someone unfamiliar with the topic, not does this look clear to me. The two-axis state model only got simple once I stopped trying to name every technical cause and just asked what the user needed to do next.