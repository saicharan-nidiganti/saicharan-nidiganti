# SaiCharan Nidiganti

**Full-Stack Software Engineer · AI Systems** · Hyderabad, India

I build web applications, backend services, and LLM systems the way production software
should be built: typed, covered by automated tests, measured in CI, and documented well
enough that someone else can run them. My recent work is in retrieval-augmented generation,
LLM evaluation, and local model benchmarking, across Python, TypeScript, and Swift.

---

## Featured work

### [Production RAG](https://github.com/saicharan-nidiganti/production-rag)

[![CI](https://github.com/saicharan-nidiganti/production-rag/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/saicharan-nidiganti/production-rag/actions/workflows/ci.yml)
[![Release](https://img.shields.io/github/v/release/saicharan-nidiganti/production-rag)](https://github.com/saicharan-nidiganti/production-rag/releases)

A self-hosted question-answering backend that answers from your documents, cites the exact
passages it used, and abstains when the documents don't contain the answer.

- **Retrieval:** hybrid BM25 + vector search merged with Reciprocal Rank Fusion, then
  cross-encoder reranking. On the held-out split of its 94-question evaluation set: hit
  rate 1.00, MRR 0.946, p95 retrieval latency 75 ms.
- **Quality gates:** retrieval quality is a CI gate, so a regression fails the build. 227
  tests with a 90% coverage floor, `mypy --strict`, and Ruff, run on Python 3.12, 3.13, and 3.14.
- **Security:** document text is passed to the model as data, never as instructions; uploads
  are parsed in isolated processes; gitleaks and pip-audit run on every push.
- **Design:** 8 architecture decision records, background ingestion with crash recovery,
  and a tagged [v0.1.0 release](https://github.com/saicharan-nidiganti/production-rag/releases/tag/v0.1.0).

`Python` `FastAPI` `SQLite FTS5` `Alembic` `fastembed` `Claude API` `uv` `GitHub Actions`

### [Local AI Benchmark](https://github.com/saicharan-nidiganti/local-ai-benchmark)

A reproducible lab for measuring local LLM inference through Ollama: time to first token,
total latency, and throughput, logged as JSONL so runs can be compared under fixed settings.

`Python` `Ollama` `Local LLMs` `Benchmarking`

---

## Technical skills

| Area | Skills |
| --- | --- |
| Languages | Python, TypeScript, JavaScript, Swift, SQL |
| Full-stack development | FastAPI, Pydantic, REST API design, React, Vite, SwiftUI |
| Databases | MongoDB, MongoDB Compass, SQLite, Alembic migrations |
| AI / LLM | RAG, hybrid search, embeddings, reranking, LLM evaluation, Claude API, Ollama |
| Testing | Test automation, performance testing and benchmarking, pytest, Vitest, React Testing Library, CI coverage gates |
| DevOps and infrastructure | Kubernetes, GitHub Actions, Dependabot |
| Code quality and security | mypy, Ruff, ESLint, gitleaks, pip-audit |

---

## How I work

- **Decisions are written down.** Significant choices get an architecture decision record
  with the options considered and the trade-offs accepted.
- **Quality is measured, not claimed.** Retrieval quality, type checking, and test coverage
  are CI gates, so regressions fail the build instead of reaching users.
- **Status is stated honestly.** My READMEs separate what is verified, what is implemented
  but not yet measured, and what is planned.
- **Security is part of the design**, not a final review step.

## Currently

- Preparing the first live evaluation of Claude-generated answers in Production RAG:
  citation accuracy, declining unanswerable questions, and prompt-injection resistance.
- Next up: multi-user isolation on PostgreSQL with pgvector.
- Exploring: LLM observability and fine-tuning with LoRA and DPO.
