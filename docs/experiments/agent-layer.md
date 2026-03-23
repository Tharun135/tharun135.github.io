# Documentation Agent Orchestrator

*Governance-first AI orchestration for technical documentation.*

## The Problem: AI is too fluent

When AI rewrites documentation, the real risk is silent meaning change — invented features, implied steps, and assumed workflows. It's hard to catch and dangerous for technical correctness.

## The Solution: Strict Governance

This orchestrator is built to stop AI from inventing documentation. It enforces explicit governance on AI rewrites by:

1.  **Preserving Ambiguity** — If the source is vague, the output stays vague. No guessing.
2.  **Zero Hallucination** — Explicitly forbids adding features or steps not in the source.
3.  **Explicit Uncertainty** — Lists exactly what was left ambiguous in a separate report section.
4.  **Questions, Not Inventions** — If the AI needs more info to complete a task, it must stop and ask instead of assuming.

## The Stack

- **Raw LLM Function-Calling** — Built directly on OpenAI/Anthropic APIs for total control, moving away from high-level frameworks like LangChain.
- **VS Code Extension** — Integrated directly into the writer's environment for seamless governed rewrites.
- **Prompt Governance Layer** — A custom engine that wraps every request in strict behavioral constraints.

## Goal: Trust over Polishing

Unlike standard AI writing assistants, this tool deliberately does **not** polish sentences or simplify language. It is designed for one thing: **Trust**. If the output is generated, you know it is technically grounded in your source content.

---

*Current status: Functional orchestration loop in VS Code extension beta.*