---
title: RAG with ChromaDB
description: Leveraging vector search to manage complex style rules and context.
---

Notes on using Retrieval-Augmented Generation to store and retrieve 
writing style rules inside Doc-Scanner.

## Why RAG for style rules

A style guide has hundreds of rules. Sending all of them to an LLM 
every time is expensive, slow, and noisy. RAG lets me retrieve only 
the rules relevant to the current piece of content.

## How it works

1. Style rules are chunked and embedded into ChromaDB as vectors
2. When a document segment is analyzed, similar rules are retrieved by cosine similarity
3. Only those rules are passed to the LLM with the content
4. The LLM flags issues and suggests rewrites based on the retrieved rules

## What surprised me

The quality of retrieval depends heavily on how you write the rules themselves. 
Vague rules retrieve poorly. Specific, example-driven rules retrieve well.

## What's next

Experimenting with rule weighting — giving higher priority to critical 
style violations over minor preferences.