# Roadmap

**NEXUS TwinLoop Legal Lab** is an early laboratory prototype for legal AI safety boundaries.

Project context: **AiLawyer.world**  
Developed by **EN-DO Technology**

---

## Current status

The current repository contains a minimal, dependency-free Python prototype.

It demonstrates:

- legal-intent detection;
- jurisdiction-boundary refusal;
- service-boundary refusal;
- source-grounded answer behavior;
- `UNVERIFIED` response behavior;
- QA metrics;
- Active/Shadow update concepts;
- snapshot and rollback concepts.

The prototype is intentionally small.

It does not claim legal correctness.  
It does not contain verified legal sources.  
It does not provide legal advice.  
It is not a production legal engine.

---

## Guiding principle

Legal AI should start with boundaries, not promises.

A legal AI system should know when to stop before it tries to answer.

The core safety principle is:

> No source, no legal claim.  
> No verified jurisdiction, no jurisdiction-specific answer.  
> No service authority, no attorney-like action.

---

## Phase 1: Repository packaging

Goal: make the laboratory prototype understandable and transparent.

Planned or completed items:

- publish the Python prototype;
- create a clear README;
- document limitations;
- document safety boundaries;
- add REG container schema draft;
- add roadmap;
- prepare article draft;
- link the repository to AiLawyer.world when the site is ready.

Status: in progress.

---

## Phase 2: Public explanation

Goal: explain the project clearly before building a production system.

Planned items:

- publish an article on Medium under the En Doa author identity;
- explain why legal AI needs boundaries before promises;
- explain the difference between safety and retrieval coverage;
- explain why refusal can be a safety feature;
- link the article to this GitHub repository;
- later publish or mirror the article on AiLawyer.world.

Status: planned.

---

## Phase 3: REG containers

Goal: move from placeholder legal text to structured legal knowledge units.

A REG container is a structured legal unit that may include:

- jurisdiction;
- authority;
- official citation;
- effective date;
- applicability;
- exceptions;
- red flags;
- required user facts;
- source excerpts;
- review status;
- retrieval metadata.

Planned items:

- define a stable REG container schema;
- create sample REG containers;
- separate draft containers from reviewed containers;
- add source hashes and versioning;
- add applicability and red-flag fields;
- add review status values such as `machine_draft`, `source_checked`, `human_reviewed`, `attorney_reviewed`, `active`, `deprecated`, and `rejected`.

Status: research draft.

---

## Phase 4: REG Factory

Goal: build a pipeline that turns official legal sources into structured REG container drafts.

Possible pipeline:

1. source intake;
2. source fetcher;
3. legal text parser;
4. chunker;
5. structured REG draft generator;
6. schema validator;
7. citation grounding checker;
8. human review queue;
9. embedding generator;
10. publisher;
11. QA runner;
12. Active/Shadow promotion.

Important: automatically generated REG containers should begin as drafts, not verified legal content.

Status: planned.

---

## Phase 5: Retrieval layer

Goal: improve retrieval beyond the current lexical baseline.

Possible steps:

- metadata search by jurisdiction, category, topic, and status;
- keyword search;
- chunk-level embeddings;
- hybrid retrieval;
- reranking;
- citation relevance checks.

Important: embeddings should not replace legal metadata.

The safer order is:

1. legal intent detection;
2. jurisdiction detection;
3. service-boundary detection;
4. metadata filtering;
5. retrieval;
6. answer generation;
7. verification.

Status: planned.

---

## Phase 6: Firebase / cloud prototype

Goal: connect the legal safety architecture to a real application backend.

Possible components:

- Firebase Hosting or App Hosting;
- Firebase Authentication;
- Cloud Functions;
- Firestore;
- Firestore Vector Search;
- App Check;
- audit logs;
- QA run storage;
- model or corpus version records.

Possible API endpoint:

- `legalAnswer`

Status: planned.

---

## Phase 7: Verifier layer

Goal: check generated answers before they reach the user.

The verifier should check:

- whether every legal claim is supported by a retrieved source;
- whether jurisdiction is correctly stated;
- whether the answer avoids attorney-client relationship language;
- whether the answer avoids guaranteed outcomes;
- whether the answer avoids filing, representation, or document-submission promises;
- whether the answer respects red flags from REG containers.

Status: planned.

---

## Phase 8: Human and legal review

Goal: prevent machine-generated legal containers from becoming active without review.

Possible review levels:

- machine draft;
- source checked;
- human reviewed;
- attorney reviewed;
- active;
- deprecated;
- rejected.

For production use, jurisdiction-specific legal content should be reviewed by qualified humans or legal professionals.

Status: planned.

---

## Non-goals of the current prototype

The current prototype is not intended to be:

- a replacement for a lawyer;
- a legal advice engine;
- a complete RAG framework;
- a LangChain or LlamaIndex replacement;
- a production legal database;
- a benchmark of legal correctness;
- a complete Firebase application.

It is a small reference artifact for legal AI safety architecture.

---

## Long-term direction

The long-term goal is not just to connect a large language model to legal text.

The long-term goal is to build a structured legal AI operating layer:

- legal safety gates;
- jurisdiction-aware retrieval;
- REG containers;
- verified legal sources;
- citation grounding;
- red-flag handling;
- human review;
- QA metrics;
- Active/Shadow update discipline;
- rollback capability.

This direction supports the broader AiLawyer.world vision:

> a legal information system that is useful because it is careful, not because it pretends to know everything.

---

## Status note

This roadmap is exploratory.

It may change as the project evolves.
