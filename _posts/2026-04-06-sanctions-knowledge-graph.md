---
title: "Sanctions Knowledge Graph: Entity Resolution and Agentic Retrieval"
date: 2026-04-06
categories:
  - projects
tags:
  - knowledge-graphs
  - nlp
  - neo4j
  - langgraph
  - entity-resolution
  - python
excerpt: "Building an agentic knowledge base over public sanctions data using graph modeling, semantic search, and multi-hop reasoning."
header:
  teaser: /assets/images/sanctions-kg-teaser.png
toc: true
toc_label: "Contents"
---

## Overview

This project builds a Knowledge Base over public sanctions data from three jurisdictions — OFAC (US), UN, and EU — modelling entities and their relationships as a property graph, and layering semantic search on top for fuzzy entity resolution across sources.

The system is designed to answer questions that require multi-hop reasoning: *"Is this vessel ultimately controlled by a sanctioned individual?"* or *"What do we know about this entity across all three sanctions lists?"* — the kind of questions a compliance analyst asks daily but that no single structured query can answer.

The full repository is available at [github.com/kgiannako/sanctions-knowledge-graph](https://github.com/kgiannako/sanctions-knowledge-graph).

---

## Motivation

Sanctions screening is a genuinely hard information retrieval problem. The same real-world entity — a person, a company, a vessel — appears across multiple lists under different name spellings, transliterations, and formats. OFAC lists "PUTIN, Vladimir". The UN lists "Vladimir Vladimirovich Putin". The EU lists "Vladimir Putin". Each has a different internal ID and different supporting attributes. Without resolution, a screening system that checks one list misses coverage from the others.

The standard approach is exact or fuzzy string matching, which breaks on transliterations and name variants. The knowledge graph approach — embedding names semantically, scoring structured attributes, and drawing explicit resolution edges — handles this more robustly and produces an auditable evidence trail for every match decision.

---

## Architecture

The pipeline has six layers:

**Data ingestion** — Three public XML sources (OFAC SDN, UN Consolidated List, EU Financial Sanctions Files) are parsed into a canonical entity model covering Person, Organisation, and Vessel types. Each parser handles a different XML schema and namespace structure. Entity attributes include IMO numbers, vessel flags, call signs, MMSI, date of birth, nationality, country, and sanctions programs.

**Graph storage** — Entities are loaded into Neo4j as property graph nodes using MERGE for idempotent ingestion. A uniqueness constraint on entity ID prevents duplicates and creates an automatic index for fast lookups.

**Semantic indexing** — All entity names and aliases are embedded using `all-MiniLM-L6-v2` and stored in a FAISS `IndexFlatIP` index (60k vectors, 384 dimensions, cosine similarity via L2 normalisation). Aliases are embedded separately from primary names so a query for a known alias hits directly rather than being diluted by the full name string.

**Entity resolution** — A two-stage pipeline identifies cross-source matches. Stage one uses semantic search to find candidates above a 0.75 cosine similarity threshold. Stage two scores structured attributes — IMO number exact match (+0.50, mismatch = hard reject), DOB match (+0.20 full, +0.05 year only), call sign match (+0.30), nationality match (+0.10). Confirmed matches are written as `SAME_AS` edges in Neo4j, storing semantic score, attribute score, combined score, and evidence reasons on each edge.

**Agent layer** — A LangGraph ReAct agent wraps the knowledge base into a reasoning system with five tools: semantic entity search, consolidated profile retrieval (merging SAME_AS links), graph traversal, program-based filtering, and country-based filtering. The agent selects tools autonomously and chains calls for multi-hop queries.

**Evaluation and observability** — Every agent run is logged to JSONL with full tool call traces. A keyword-based evaluation framework benchmarks the agent against five ground truth queries, achieving 100% pass rate. Results are saved to JSON for tracking across runs.

---

## Entity Resolution Design

The resolution pipeline handles three entity types differently because the available corroborating signals differ:

For **vessels**, IMO number is a near-certain identifier — a mismatch is a hard reject regardless of name similarity. Secondary signals (call sign, MMSI, flag, vessel type, tonnage) are used when IMO is absent for one or both candidates. Sister vessels — same owner, same flag, similar tonnage — are a known false positive risk and are handled by ensuring IMO mismatch always overrules secondary signal combinations.

For **persons**, DOB is the strongest signal but requires fuzzy year extraction since formats vary widely across lists (`1973`, `01-03-1973`, `Mar 1973`). Nationality alone cannot push a borderline semantic score over the threshold — this prevents common-name false positives where two different people share a nationality and approximate birth year.

For **organisations**, business term normalisation before embedding is critical. Stripping terms like "Bank", "Ltd", "International", "Group" before the semantic search query prevents "Bank Keshavarzi Iran" and "Bank Melli Iran" from appearing semantically similar just because they share three common words. UN reference ID exact match is a near-certain signal (+0.45) since both OFAC and EU sometimes store the original UN listing ID.

---

## Results

Across 25,568 entities and 24,378 evaluated pairs:

| Metric | Value |
|--------|-------|
| SAME_AS edges written | 4,076 |
| Person matches | 3,553 |
| Organisation matches | 523 |
| Hard rejects | 307 |
| High confidence matches (score ≥ 1.0) | 81% |

Sample agent queries and reasoning:

- *"What do we know about Bin Laden across all sanctions lists?"* — agent made 6 parallel tool calls, consolidated aliases from OFAC and EU, identified three family members, surfaced SDGT program designation.
- *"How many vessels are sanctioned under the Iran program?"* — single `find_by_sanctions_program` call returned 547 vessels, followed by parallel profile lookups on representative examples.
- *"Are there North Korean entities sanctioned across multiple lists?"* — agent self-corrected from failed country search to program search, then identified KOMID and Reconnaissance General Bureau appearing across OFAC, UN, and EU via semantic search.

---

## Production Considerations

Several deliberate simplifications were made for this prototype that would change at production scale:

**Ingestion throughput** — currently one entity per Neo4j transaction. Production would use batched `UNWIND` transactions of 500–1000 records, reducing round trips by 3 orders of magnitude.

**Multilingual coverage** — `all-MiniLM-L6-v2` is English-primary. Arabic and Cyrillic name transliterations have degraded similarity scores. A multilingual model (`paraphrase-multilingual-MiniLM-L12-v2`) would improve cross-script resolution.

**Vector store** — flat FAISS files loaded into RAM work at 60k vectors. Production would use a managed vector store (Pinecone, pgvector) for concurrent access, incremental upserts, and metadata filtering.

**Evaluation** — keyword matching is deterministic and free but can't catch well-written wrong answers. Production evaluation would include LLM-as-judge scoring and a labelled ground truth set for threshold calibration.

**Monitoring** — JSONL trace logging covers auditability. Production would add latency tracking, tool call frequency analysis, and integration with a proper observability stack.

---

## Stack

- Neo4j 5 (Docker) — graph database
- Python 3.11 — all pipeline code
- sentence-transformers (`all-MiniLM-L6-v2`) — semantic embeddings
- FAISS — vector similarity search
- LangGraph + Claude Sonnet — ReAct agent
- LangChain Anthropic — LLM interface

---

## Repository

[github.com/kgiannako/sanctions-knowledge-graph](https://github.com/kgiannako/sanctions-knowledge-graph)
