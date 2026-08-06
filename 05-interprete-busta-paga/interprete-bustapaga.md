---
title: "Intérprete di Busta Paga"
subtitle: "A tool that reads an Italian payslip, verifies it against fiscal logic, and explains it in plain language"
role: "Product Designer"
type: "Concept Project"
tools: ["Figma", "Figma Make", "Claude"]
tags: ["concept-project", "fintech", "design-systems", "italian-admin"]
status: "prototype"
date: "2026"
summary: "A concept tool that verifies Italian payslips against fiscal logic and explains errors in plain language — designed for someone with zero prior knowledge of the topic."
---

# Intérprete di Busta Paga

**Product Designer · Concept Project**

---

## Context

This project started from a real case. A manual review of 19 monthly payslips (*cedolini*) for an Italian dependent worker revealed that a legally owed tax deduction (*detrazione fiscale*) had been missing for 11 consecutive months — a real, unclaimed error of roughly €2,600-2,900 in the employee's favor.

Most Italian workers have no accessible way to verify their own payslip. The math is opaque, the terminology is technical, and errors like this one go unnoticed for months or years. Intérprete di Busta Paga is a concept for a tool that reads a payslip, checks it against the underlying fiscal logic, and explains what it finds in plain language — built for someone with zero prior knowledge of the topic.

## What I designed

- A two-axis state model (data completeness vs. analysis result) that lets the system communicate partial or uncertain results without resorting to technical jargon or a binary pass/fail
- A dual-ingestion flow — photo/PDF with OCR, single or batch upload — with an in-place, field-level correction fallback, avoiding a separate "enter your data" screen that would add friction for a non-expert user
- A non-blocking urgency system for missing data: critical gaps are visually prominent but never interrupt navigation, a deliberate product principle carried through every screen
- A multi-language system (Spanish, English, Italian) that keeps official fiscal terminology untranslated across all languages, so users can still recognize those terms on their real payslip, while translating every explanatory layer around them
- An end-to-end flow mapped across six screens, from first upload through a multi-month historical comparison, with type-specific chart logic (line chart for net income, accumulated-area chart for severance pay/TFR, balance-first cards for leave/PTO)

## Tools

Figma, Figma Make, Claude

## What I learned

Designing for someone who understands nothing about the subject forced a discipline I didn't fully expect: nearly every state, label, and chart choice had to be re-justified from "does this help someone unfamiliar" rather than "does this look clear to me." The two-axis state model only became simple once I stopped trying to name every possible technical cause and instead asked what the user actually needed to do next.