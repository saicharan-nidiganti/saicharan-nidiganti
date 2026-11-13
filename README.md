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

[![CI](https://github.com/saicharan-nidiganti/local-ai-benchmark/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/saicharan-nidiganti/local-ai-benchmark/actions/workflows/ci.yml)
[![Release](https://img.shields.io/github/v/release/saicharan-nidiganti/local-ai-benchmark)](https://github.com/saicharan-nidiganti/local-ai-benchmark/releases)

Which small language model should run on a laptop with a 4 GB GPU? An offline benchmark that
answers by measurement: three models served by Ollama, scored on 45 support-ticket tasks
(classification, JSON extraction, summaries) and timed on the same machine and settings; and
an offline app that runs the winner.

- **Result:** phi4-mini is the best tradeoff: quality 0.89, level with qwen3:4b-instruct, at
  34.6 tokens/s, 14% faster and with 23% less GPU energy per task. llama3.2:3b is the fastest
  at 53 tokens/s but writes weaker summaries (0.81 overall).
  [Full results](https://github.com/saicharan-nidiganti/local-ai-benchmark/tree/main/results/2026-11-13-three-model-comparison).
- **Measurement:** warm-ups excluded, a fixed seed and settings, and an environment manifest
  for every run (model digest, Ollama version, power state, harness commit), with the raw
  JSONL kept so every summary can be rebuilt.
- **Findings:** sending the JSON schema as Ollama's structured-output format took JSON
  validity from 0% to 100% on a thinking model; every model over-escalates ticket priority.
- **Privacy, latency and cost, measured offline:** with networking off, 0 connections to
  another machine in 150 runs and the same replies byte for byte; every model meets the
  latency targets for interactive use (first token in 92 to 203 ms); GPU electricity costs
  INR 2 to 4 per million tokens against INR 19 to 31 for the same models hosted.
  [Tradeoffs](https://github.com/saicharan-nidiganti/local-ai-benchmark#tradeoffs-privacy-latency-and-cost).
- **The app:** paste a support ticket, get its category, priority, order number, customer and
  a summary from phi4-mini in about 3 s, as a command or a local web page that listens on
  127.0.0.1 only, keeps nothing, and works with networking off.
- **Engineering:** 224 offline tests at 97% coverage, `mypy --strict`, 7 required CI checks on
  Python 3.11 to 3.14 and Windows, 12 architecture decision records, and a tagged
  [v1.0.0 release](https://github.com/saicharan-nidiganti/local-ai-benchmark/releases/tag/v1.0.0).

`Python` `Ollama` `Small language models` `Pydantic` `LLM evaluation` `Benchmarking` `uv` `GitHub Actions`

---

## Technical skills

| Area | Skills |
| --- | --- |
| Languages | Python, TypeScript, JavaScript, Swift, SQL |
| Full-stack development | FastAPI, Pydantic, REST API design, React, Vite, SwiftUI |
| Databases | MongoDB, MongoDB Compass, SQLite, Alembic migrations |
| AI / LLM | RAG, hybrid search, embeddings, reranking, LLM evaluation, structured output, local inference with Ollama and quantized models, Claude API |
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
