# Doc-Scanner

A Flask-based documentation analysis tool I built to solve real problems 
in my documentation workflow.

## What it does
- Analyzes documents for readability using readability metrics
- Enforces style guide rules via RAG + ChromaDB
- Rewrites content into simple present tense user manual steps using spaCy
- Provides AI suggestions through a dynamic rule engine

## Stack
- Python + Flask
- ChromaDB for vector storage
- spaCy for NLP
- RAG for style rule retrieval

## What I learned
- How to structure a Flask blueprint architecture with dynamic rule loading
- How RAG works in practice — not just in theory
- The difference between using a framework like LangChain vs raw LLM function-calling APIs

## What's next
Productizing this end-to-end — a proper UI, shareable output reports, 
and a deployable version others can use.