# Retrieval-augmented generation (RAG)

## Method

Index repository chunks/symbols/docs, retrieve a small evidence set per task, then read source on demand. Combine lexical filename/symbol search with semantic and structural signals when appropriate.

## Caution

Naive chunking loses call relations and can retrieve stale, semantically similar but wrong code. Include index/update cost and retrieval-model tokens in the end-to-end measurement. Code maps and Graphify are specialized alternatives.
