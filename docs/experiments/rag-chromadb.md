# RAG with ChromaDB

Notes on integrating Retrieval-Augmented Generation into Doc-Scanner 
to store and retrieve writing style rules.

## The problem
Style guides have hundreds of rules. Sending all of them to an LLM every 
time is expensive and noisy. RAG lets me retrieve only the relevant rules 
for a given piece of content.

## How it works
1. Style rules are chunked and embedded into ChromaDB
2. When a document is analyzed, the relevant rules are retrieved by similarity
3. Only those rules are sent to the LLM along with the content

## Key insight
RAG is most powerful when your knowledge base is well-structured. 
Garbage in, garbage out — even with good retrieval.