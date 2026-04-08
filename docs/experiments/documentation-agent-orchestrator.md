---
title: Documentation Agent Orchestrator
description: A governance layer for AI-driven documentation generation in VS Code.
---


## Overview

**Documentation Agent Orchestrator** is a VS Code extension that acts as a **governance layer** between raw content and AI. It enforces a strict **Zero-Invention Policy**, prioritizing factual correctness over fluency to ensure AI never "invents" features or steps not present in the source.

### Key Capabilities
- **Active Gap Detection**: Scans source content using **40+ rule-based checkers** to identify structural ambiguities before the AI is called.
- **Three-Phase Pipeline**: Employs an **Analyse → Question → Generate** workflow to resolve gaps via human input instead of AI guesswork.
- **Traceability**: All remaining uncertainties are explicitly labeled in a generated **"Preserved Ambiguities"** section.
- **Automated Validation**: Integrated commands to paste AI responses and trigger side-by-side **governance diff previews**.

---

## Architecture

### High-Level Design
```txt
┌─────────────────────┐
│   User Content      │ (Rough notes, code comments, specs)
└──────────┬──────────┘
           ▼
┌─────────────────────┐
│  Extension Layer    │ (extension.ts)
└──────────┬──────────┘
           ▼
┌─────────────────────┐
│   Engine Layer      │ (Gap Detection, Rules, Logic)
└──────────┬──────────┘
           ▼
┌─────────────────────────┐
│  Generated Prompt       │ (Constrained & Governed)
└─────────────────────────┘
```

---

## Gap Detection System

The core of the extension is the `questionDetector.ts` engine. It scans the source line-by-line for 9 classes of structural ambiguity that typically trigger AI hallucination:

| Ambiguity Class | Description |
|---|---|
| **Location** | Step has no UI location (e.g., "Upload files") |
| **Actor** | No named performer (Passive voice) |
| **Value** | No value, unit, or default given (e.g., "Set timeout") |
| **Branch Logic** | Conditional with no defined outcome |
| **Temporal** | Action with no timing or schedule |
| **Data Contract** | Format, scope, or count unspecified |
| **Navigation** | Destination exists but path does not |
| **Verification** | Step has no method or success criteria |
| **Incompleteness** | Placeholder, TBD, or collapsed multi-step action |

**Zero-Invention Contract**: If a gap is detected, the user is prompted to answer a clarification question. The answer is injected as an **authoritative fact**. If no answer is provided, the AI is forbidden from guessing and must document it as a "Preserved Ambiguity."

---

## The Three-Phase Pipeline

No AI call is made until every blocking gap in the source has been addressed.

```txt
┌─────────────────────────────────────────────────────────┐
│  PHASE 1 — GAP ANALYSIS                                 │
│  Source is scanned for 40+ structural weaknesses.       │
└───────────────────────────┬─────────────────────────────┘
                            ▼
┌─────────────────────────────────────────────────────────┐
│  PHASE 2 — INTERACTIVE QUESTIONING                      │
│  User answers gaps via VS Code input boxes.             │
└───────────────────────────┬─────────────────────────────┘
                            ▼
┌─────────────────────────────────────────────────────────┐
│  PHASE 3 — GOVERNED PROMPT GENERATION                   │
│  Prompt = Source + Human Answers + Governance Rules.    │
└─────────────────────────────────────────────────────────┘
```

---

## Governance Rules

These rules are injected into every AI prompt to constrain behavior:
- **No Feature Invention**: Do not add behavior not stated in the source.
- **Terminology Preservation**: Do not change established terms from the source.
- **No Invented Steps**: Every procedure step must be traceable to the source.
- **Preserve Ambiguity**: If the source is vague, document it as-is—do not guess.
- **No Style Rewriting**: Focus entirely on correctness over elegant phrasing.

---

## Command Reference

| Command | Action |
|---|---|
| `Generate Documentation Prompt` | Triggers Gap Analysis and builds the governed prompt. |
| `Provide Clarifications` | Answer AI questions to resolve remaining gaps. |
| `Paste AI Response & Check` | One-tap command to paste AI output and trigger diff validation. |
| `Preview Rewrite Diff` | Side-by-side comparison of source vs. AI output. |

---

## Summary

The **Doc Agent Orchestrator** doesn't try to make AI smarter—it makes AI behavior **constrained, observable, and defensible.**

By proactively resolving structural gaps before generation and enforcing strict zero-invention rules, the extension transforms AI from an "assistant that often lies" into a "constrained agent that preserves truth."