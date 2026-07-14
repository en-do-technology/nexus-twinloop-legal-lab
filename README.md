# NEXUS TwinLoop Legal Lab

**A minimal laboratory prototype for legal AI safety boundaries.**

Project context: **AiLawyer.world**  
Developed by **EN-DO Technology**

---

## What this is

NEXUS TwinLoop Legal Lab is a small, dependency-free Python prototype that demonstrates how a legal AI system can be designed around **boundaries before promises**.

It is not meant to be a production legal engine.  
It is not legal advice.  
It is not a replacement for an attorney.  
It is a laboratory artifact for exploring safety-first legal AI architecture.

The prototype demonstrates:

- source-grounded legal answers;
- `UNVERIFIED` responses when no supporting source is available;
- jurisdiction-boundary refusal for state-specific or D.C.-specific questions without verified local sources;
- service-boundary refusal for requests such as representation in court, filing lawsuits, drafting legal documents, or guaranteeing outcomes;
- separation between safety metrics and retrieval coverage metrics;
- Active/Shadow update discipline with snapshot and rollback concepts.

---

## Why this exists

Most large language models are designed to answer.

Legal AI must first learn when **not** to answer.

A legal AI system should not make a legal claim just because it sounds plausible.  
It should not confuse general legal information with state-specific law.  
It should not pretend to be a lawyer.  
It should not create the impression of representation, filing, or guaranteed results.

This prototype explores a simple principle:

> No source, no legal claim.  
> No verified jurisdiction, no jurisdiction-specific answer.  
> No service authority, no attorney-like action.

---

## Core safety boundaries

### 1. Source boundary

If the system cannot find a supporting source in the current legal index, it returns `UNVERIFIED`.

This is intentional. In legal AI, a refusal or uncertainty marker can be safer than a confident unsupported answer.

### 2. Jurisdiction boundary

If the user asks about a specific U.S. state or the District of Columbia, but the system has no verified jurisdiction-specific corpus connected, it returns `JURISDICTION_UNRESOLVED`.

The prototype should not use a generic legal placeholder as if it were California, Texas, Nevada, New York, or D.C. law.

### 3. Service boundary

If the user asks the system to represent them, file documents, draft litigation documents, act as their lawyer, or guarantee an outcome, it returns `SERVICE_BOUNDARY`.

The prototype does not create an attorney-client relationship and does not perform legal representation.

### 4. Out-of-scope boundary

If the question is not legal, the prototype returns `OUT_OF_SCOPE`.

---

## What the prototype includes

The current Python file includes:

- `LegalRiskDetector`
- `JurisdictionDetector`
- `ServiceBoundaryDetector`
- `SimpleVectorStore`
- `LexicalEmbeddingProvider`
- `ExtractiveStubLLM`
- `ModelService`
- `CanaryDeployer`
- `QA` metrics runner

The implementation is intentionally simple:

- no external dependencies;
- no production database;
- no real LLM call;
- no real legal corpus;
- no semantic embedding provider;
- no legal correctness benchmark.

This simplicity is intentional. The purpose is to make the safety architecture visible and easy to inspect.

---

## Demo metrics

The included demo test set checks legal detection, service-boundary refusal, jurisdiction-boundary refusal, out-of-scope refusal, retrieval coverage, and unsupported legal claims.

Current demo output is expected to show:

- `legal_detection_accuracy`: 100%
- `subdomain_routing_accuracy`: 100%
- `unsupported_claim_rate`: 0%
- `retrieval_coverage_rate`: about 24%
- `covered_topic_retrieval_rate`: 100%
- `service_boundary_refusal_rate`: 100%
- `jurisdiction_boundary_rate`: 100%
- `out_of_scope_refusal_rate`: 100%
- `legal_correctness`: not measured
- `jurisdiction_coverage`: not measured

Important: low retrieval coverage is expected because the prototype contains only a few placeholder legal documents.

The key safety metric is `unsupported_claim_rate = 0%`.

That means the system should not make a legal assertion without a retrieved supporting source.

---

## Run the demo

Run:

`python nexus_twinloop_legal_us_lab_v33_fix.py`

The script will run the public demo test cases and print the QA report.

---

## Important limitations

This repository does **not** contain a production-ready legal AI system.

It does not include:

- verified legal sources;
- state-specific legal corpora;
- city or county ordinances;
- attorney-reviewed legal content;
- real semantic embeddings;
- real vector database integration;
- production API;
- authentication;
- legal correctness evaluation;
- compliance review.

The seeded legal documents are illustrative placeholders only.

---

## Next research direction

The next step is to build a structured legal knowledge layer:

- official legal sources;
- REG containers;
- jurisdiction-specific metadata;
- applicability rules;
- red flags;
- citations;
- review status;
- embeddings and retrieval;
- verifier;
- safer legal AI answers.

We call this direction **REG Factory**.

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
- verification status;
- retrieval metadata.

---

## Project status

This is an early laboratory prototype.

It is published for research, discussion, and architectural transparency.

The broader project context is **AiLawyer.world**.

The development line is **EN-DO Technology**.

---

## License

Apache License 2.0
