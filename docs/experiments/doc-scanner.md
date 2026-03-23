---
title: Doc-Scanner
description: AI-powered documentation analysis and style guide enforcement.
---

An AI-powered documentation analysis tool I built to solve real problems 
in my own writing workflow.

## The problem it solves

Style guide enforcement is manual and inconsistent. Readability checks happen 
too late. Feedback loops between writers and reviewers are slow.

Doc-Scanner automates this — analyzing documents against style rules, 
measuring readability, and suggesting rewrites in real time.

## Stack

- **Python + Flask** — backend and blueprint architecture
- **ChromaDB** — vector storage for style rules
- **RAG** — retrieves relevant rules per document segment
- **spaCy** — NLP for sentence analysis and rewriting
- **Readability metrics** — Flesch-Kincaid and similar

## What I learned

- How to structure a Flask app with dynamic rule loading via blueprints
- RAG works best when your knowledge base is well-structured — the retrieval 
  is only as good as what you put in
- Raw LLM function-calling APIs give you more control than LangChain, 
  at the cost of more setup

## Current focus

Productizing this end-to-end — proper UI, exportable reports, and a 
deployable version others can actually use.

## Key decision

I deliberately chose raw LLM APIs over LangChain. The abstraction LangChain 
provides wasn't worth the loss of control for what I needed.