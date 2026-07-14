# REG Container Schema

**A proposed structured legal knowledge unit for AiLawyer.world.**

Project context: **AiLawyer.world**  
Developed by **EN-DO Technology**

---

## Purpose

A REG container is a structured legal knowledge unit.

It is not just a text chunk for retrieval.  
It is a legal evidence container designed to make legal AI answers more grounded, jurisdiction-aware, and safety-aware.

The goal is to move from generic model memory to structured legal evidence.

A REG container should help the system answer questions such as:

- What jurisdiction does this rule belong to?
- What official source supports it?
- What is the citation?
- What is the effective date?
- What facts are required before the rule can be applied?
- What are the exceptions?
- What red flags should stop or limit the answer?
- Has this content been reviewed?
- Is this rule active, deprecated, or only a draft?

---

## Why REG containers matter

Large language models can often explain legal concepts in general terms.

But legal AI needs more than general knowledge.

It needs:

- jurisdiction-specific sources;
- official citations;
- effective-date awareness;
- applicability boundaries;
- red flags;
- verification status;
- auditability;
- retrieval metadata.

A REG container is designed to be the bridge between raw legal sources and safer AI-generated legal information.

---

## Core idea

The basic principle is:

> The model should not be the source of law.  
> The REG container should carry the source, citation, jurisdiction, applicability, and safety boundaries.  
> The model should explain only what the REG container supports.

---

## Minimal REG container fields

A REG container may include the following top-level sections:

- `reg_id`
- `schema_version`
- `jurisdiction`
- `classification`
- `authority`
- `versioning`
- `applicability`
- `rules`
- `safety`
- `retrieval`
- `verification`

---

## Example structure

{
  "reg_id": "us_ca_tenant_security_deposit_1950_5_v2026_01",
  "schema_version": "1.0",

  "jurisdiction": {
    "country": "US",
    "state": "CA",
    "county": null,
    "city": null,
    "scope": "statewide",
    "code": "US-CA",
    "local_overlay_possible": true
  },

  "classification": {
    "domain": "legal",
    "category": "tenant_landlord",
    "topic": "security_deposits",
    "subtopics": [
      "deposit_return_deadline",
      "lawful_deductions",
      "deposit_limit",
      "itemized_statement"
    ]
  },

  "authority": {
    "official_name": "California Civil Code Section 1950.5",
    "citation_format": "Cal. Civ. Code § 1950.5",
    "source_type": "statute",
    "publisher": "California Legislative Information",
    "official_url": "https://leginfo.legislature.ca.gov/",
    "source_authority_level": "official_primary"
  },

  "versioning": {
    "effective_from": "2026-01-01",
    "effective_to": null,
    "last_source_check_at": "2026-07-12T00:00:00Z",
    "source_hash": "sha256:...",
    "supersedes": null,
    "superseded_by": null,
    "status": "draft"
  },

  "applicability": {
    "applies_to": [
      "residential rental agreements",
      "security deposits in California"
    ],
    "does_not_apply_to": [
      "commercial leases",
      "non-California leases",
      "city-specific rules not included in this container"
    ],
    "requires_user_facts": [
      "state",
      "residential_or_commercial",
      "move_out_date",
      "date_deposit_was_collected",
      "whether local city ordinance may apply"
    ]
  },

  "rules": [
    {
      "rule_id": "return_deadline",
      "plain_english": "A California landlord generally must return the remaining security deposit and provide any required itemized statement within the deadline stated by the cited source.",
      "citation": "Cal. Civ. Code § 1950.5",
      "source_excerpt_ref": "chunk_1950_5_return_deadline",
      "conditions": [
        "tenant has vacated the premises",
        "residential tenancy"
      ],
      "exceptions_or_related_requirements": [
        "lawful deductions may apply",
        "additional city rules may apply"
      ]
    }
  ],

  "safety": {
    "mandatory_disclaimer": "This is legal information, not legal advice. Local ordinances may add requirements.",
    "red_flags": [
      {
        "flag": "commercial_lease",
        "action": "refuse_or_route",
        "message": "This container covers residential rental agreements, not commercial leases."
      },
      {
        "flag": "city_specific_question",
        "action": "jurisdiction_required",
        "message": "City-specific ordinances may apply; local corpus is required."
      },
      {
        "flag": "exact_damages_calculation",
        "action": "service_boundary",
        "message": "The system should not calculate exact court damages in this laboratory mode."
      }
    ]
  },

  "retrieval": {
    "keywords": [
      "security deposit",
      "landlord deposit return",
      "tenant deposit",
      "California tenant rights",
      "itemized deductions"
    ],
    "embedding_model": null,
    "embedding_scope": "chunk_level"
  },

  "verification": {
    "review_status": "machine_draft",
    "reviewed_by": null,
    "reviewed_at": null,
    "requires_attorney_review_before_production": true
  }
}

---

## Field notes

### `jurisdiction`

This section defines where the rule applies.

Legal AI should not use a generic rule as if it were state-specific law.

Examples:

- `US`
- `US-CA`
- `US-TX`
- `US-NY`
- `US-DC`
- `US-CA-LosAngeles`

### `classification`

This section helps route user questions.

Examples:

- `tenant_landlord`
- `consumer_dispute`
- `contract_basics`
- `employment_wages`
- `small_claims`

### `authority`

This section stores the official source and citation.

The model should not invent citations.  
The citation should come from the REG container.

### `versioning`

This section tracks whether the rule is current.

Legal rules can change. A legal AI system needs versioning, source checks, and deprecation logic.

### `applicability`

This section defines when the rule applies and when it does not apply.

This is critical for legal safety.

A correct rule applied to the wrong situation can still produce a dangerous answer.

### `rules`

This section contains one or more structured rule cards.

Each rule should be linked to a source excerpt.

### `safety`

This section stores red flags and required refusal or routing behavior.

Examples:

- commercial lease vs residential lease;
- state-specific question without state corpus;
- request for representation;
- request for filing documents;
- request for guaranteed outcome;
- request for exact damages calculation.

### `retrieval`

This section supports search.

Embeddings may be added later, but metadata and keywords can be used first.

### `verification`

This section tracks review status.

Possible values:

- `machine_draft`
- `source_checked`
- `human_reviewed`
- `attorney_reviewed`
- `active`
- `deprecated`
- `rejected`

---

## Important limitation

This schema is a research proposal.

It is not a legal database.  
It is not a verified legal content library.  
It is not legal advice.

Before production use, REG containers should be built from official sources, checked for currency, grounded in citations, and reviewed by qualified humans or legal professionals.

---

## Relationship to NEXUS TwinLoop Legal Lab

The current Python prototype refuses state-specific questions when no verified jurisdiction-specific corpus is connected.

REG containers are the proposed next step.

The future path is:

1. detect legal intent;
2. detect jurisdiction;
3. detect service boundary;
4. retrieve active REG containers;
5. generate an answer only from supported sources;
6. verify citations and boundaries;
7. log metrics;
8. promote updates through QA and Active/Shadow discipline.

---

## Status

Early research draft.

Published for discussion, experimentation, and architectural transparency.
