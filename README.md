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

This repository documents, screenshot by screenshot, how to build a Retrieval-Augmented Generation (RAG) pipeline on **Oracle Cloud Infrastructure (OCI) Generative AI Agents** — from an empty tenancy to a working, evaluated chatbot.

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

- Fully managed RAG pipeline on OCI (Object Storage → Knowledge Base → Generative AI Agent)
- Real console screenshots for every step, no abstract diagrams standing in for reality
- Prompt engineering and guardrail configuration explained with before/after comparisons
- Evaluation methodology: one variable per iteration, measured against a fixed question set
- Documented failures and platform limitations, not just the happy path

## Architecture

*Diagram coming once the pipeline is fully built — see [Roadmap](#roadmap) for current status.*

High-level flow:

1. Source documents → **OCI Object Storage** bucket
2. Bucket → **Knowledge Base** (managed ingestion, no separate vector DB to run)
3. Knowledge Base → **Generative AI Agent** (routing + generation LLM, RAG tool)
4. Guardrails (content moderation, prompt injection, PII) sit between the agent and the user
5. Agent exposed via the OCI Runtime API for evaluation and app integration

## Prerequisites

- An OCI tenancy with access to **Generative AI Agents** (available in `eu-frankfurt-1`)
- Basic familiarity with the OCI Console
- Python 3.11+ (for later evaluation scripts)
- A GitHub account

## Guide / Chapters

| # | Chapter | Status |
|---|---|---|
| 1 | [Repo Setup](docs/01-repo-setup.md) | ✅ |
| 2 | [OCI Account & Tenancy Setup](docs/02-oci-account-setup.md) | 🚧 |
| 3 | [Object Storage & Corpus](docs/03-object-storage-corpus.md) | 🚧 |
| 4 | [Knowledge Base & Agent](docs/04-knowledge-base-agent.md) | 🚧 |
| 5 | [Prompt Engineering & Guardrails](docs/05-prompt-engineering-guardrails.md) | 🚧 |
| 6 | [Evaluation](docs/06-evaluation-results.md) | 🚧 |

## Corpus & Data Disclaimer

All documents used in this project are **fictional**, created specifically for this demo. No real company data, internal documents, or proprietary information appear anywhere in this repository. Any resemblance to real pricing, catalogues, or business terms is coincidental and for illustrative purposes only.

## Roadmap

- [x] Repository structure and README
- [ ] OCI tenancy setup and Generative AI enablement
- [ ] Object Storage bucket + fictional corpus
- [ ] Knowledge Base + Agent creation
- [ ] Guardrails configuration
- [ ] Prompt engineering iterations
- [ ] Evaluation harness + results

## License

Licensed under the [MIT License](LICENSE).
