# DocScanner — AI Documentation Reviewer

**Type:** Internal tooling / AI experiment  
**Stack:** Python, Flask, ChromaDB, spaCy, RAG  
**Status:** Active development

---

## Overview

DocScanner is an AI-powered documentation analysis tool I built to automate 
style guide enforcement, readability checking, and content rewriting 
in a technical writing workflow.

It addresses a real problem — style reviews are manual, inconsistent, 
and happen too late in the writing process.

---

## How it works

1. A document is uploaded or pasted into the DocScanner interface
2. The content is split into segments and analyzed in parallel:
   - **Style check** — segments are matched against style rules stored in ChromaDB via RAG
   - **Readability check** — Flesch-Kincaid and related metrics are computed
   - **Rewrite suggestions** — spaCy identifies passive voice, complex sentences, 
     and non-imperative steps, and suggests rewrites
3. Results are returned as structured feedback — flagged issues, severity levels, 
   and suggested corrections

---

## Key design decisions

**RAG over static rule injection**  
Sending the full style guide to the LLM on every request is expensive and noisy. 
RAG retrieves only the rules relevant to the current content segment, 
reducing token usage and improving accuracy.

**Raw LLM APIs over LangChain**  
LangChain abstracts the function-calling loop in ways that made debugging 
difficult. Using raw Anthropic API calls gives full visibility into 
what's being sent and returned at each step.

**Flask blueprints for rule modularity**  
Each rule type (style, readability, rewrite) is a separate blueprint 
with dynamic loading. Adding a new rule type doesn't require touching 
existing code.

---

## Sample output
```json
{
  "segment": "The configuration can be updated by the user.",
  "issues": [
    {
      "type": "passive_voice",
      "severity": "medium",
      "suggestion": "Rewrite in active voice: 'Update the configuration.'"
    },
    {
      "type": "style_rule",
      "rule": "Use imperative mood for procedural steps",
      "severity": "high",
      "suggestion": "Start with a verb: 'Update the configuration.'"
    }
  ],
  "readability_score": 62.4,
  "grade_level": "8th grade"
}
```

---

## What I learned

- Retrieval quality depends on how well the source rules are written — 
  vague rules retrieve poorly regardless of embedding quality
- spaCy's dependency parser is reliable for passive voice detection 
  but needs custom rules for domain-specific patterns
- Flask blueprints scale well for this kind of modular rule engine

---

## What's next

- A proper web UI with inline diff view
- Exportable PDF reports
- A deployable version others can use