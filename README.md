<div align="center">
  <img src="assets/logo.jpg" alt="build-your-own-rag-oci logo" width="160"/>

  # build-your-own-rag-oci

  **Step-by-step guide to building a RAG pipeline from scratch on OCI**

  ![License](https://img.shields.io/badge/license-MIT-blue)
  ![Python](https://img.shields.io/badge/python-3.11%2B-blue)
  ![OCI](https://img.shields.io/badge/OCI-Generative_AI-C74634)
</div>

---

## About

This repository documents, screenshot by screenshot, how to build a Retrieval-Augmented Generation (RAG) pipeline on **Oracle Cloud Infrastructure (OCI) Generative AI Agents**, from an empty tenancy to a working, evaluated chatbot.

No shortcuts, no "trust me it works": every step is captured live from a real OCI console, redacted where needed, and every design decision is explained.

## Table of Contents

- [Features](#features)
- [Architecture](#architecture)
- [Prerequisites](#prerequisites)
- [Guide / Chapters](#guide--chapters)
- [Corpus & Data Disclaimer](#corpus--data-disclaimer)
- [Roadmap](#roadmap)
- [License](#license)

## Features

- Fully managed RAG pipeline on OCI (Object Storage, Knowledge Base, Generative AI Agent)
- Real console screenshots for every step, no abstract diagrams standing in for reality
- Prompt engineering and guardrail configuration explained with before/after comparisons
- Evaluation methodology: one variable per iteration, measured against a fixed question set
- Documented failures and platform limitations, not just the happy path

## Architecture

```mermaid
flowchart LR
    A[Object Storage<br/>Bucket] --> B[Knowledge Base<br/>Ingestion and Indexing]
    B --> C[RAG Tool]
    C --> D[Generative AI Agent<br/>Llama 3.3 70B]
    D --> E[Guardrails]
    E --> F[User]

    classDef storage fill:#0B5FFF,stroke:#083d99,color:#fff
    classDef kb fill:#009688,stroke:#00695c,color:#fff
    classDef agent fill:#C74634,stroke:#8f2f22,color:#fff
    classDef guard fill:#6b7280,stroke:#374151,color:#fff
    classDef user fill:#22c55e,stroke:#15803d,color:#fff

    class A storage
    class B,C kb
    class D agent
    class E guard
    class F user
```

High-level flow:

1. Source documents go into an **OCI Object Storage** bucket
2. The bucket feeds a **Knowledge Base** (managed ingestion, no separate vector DB to run)
3. The Knowledge Base connects to a **Generative AI Agent** through a RAG tool (routing and generation LLM)
4. Guardrails (content moderation, prompt injection, PII) sit between the agent and the user
5. The agent is exposed via the OCI Runtime API for evaluation and app integration

## Prerequisites

- An OCI tenancy with access to **Generative AI Agents** (available in `eu-frankfurt-1`)
- Basic familiarity with the OCI Console
- Python 3.11+ (for later evaluation scripts)
- A GitHub account

## Guide / Chapters

| # | Chapter | Status |
|---|---|---|
| 1 | [Repo Setup](docs/01-repo-setup.md) | Complete |
| 2 | [OCI Account & Tenancy Setup](docs/02-oci-account-setup.md) | Complete |
| 3 | [Object Storage & Corpus](docs/03-object-storage-corpus.md) | Complete |
| 4 | [Knowledge Base & Agent](docs/04-knowledge-base-agent.md) | Complete |
| 5 | [Prompt Engineering & Guardrails](docs/05-prompt-engineering-guardrails.md) | Complete |
| 6 | [Evaluation](docs/06-evaluation-results.md) | Complete |

## Corpus & Data Disclaimer

All documents used in this project are **fictional**, created specifically for this demo. No real company data, internal documents, or proprietary information appear anywhere in this repository. Any resemblance to real pricing, catalogues, or business terms is coincidental and for illustrative purposes only.

## Roadmap

- [x] Repository structure and README
- [x] OCI tenancy setup and Generative AI enablement
- [x] Object Storage bucket + fictional corpus
- [x] Knowledge Base + Agent creation
- [x] Guardrails configuration
- [x] Prompt engineering iterations
- [x] Evaluation harness + results

## License

Licensed under the [MIT License](LICENSE).
