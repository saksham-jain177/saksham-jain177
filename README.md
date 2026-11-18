# Saksham Jain

**AI Engineer — agentic systems and LLM evaluation**

I build agents, and then I build the harness that decides whether they work. The part I care about
most is the second one: most portfolios show a demo. Mine shows a score, the command that reproduces
it, and the coverage it was measured over.

## What I'm working on

**[agentic-deep-research](https://github.com/saksham-jain177/agentic-deep-research)** — a LangGraph
deep-research pipeline (parallel sub-query planning, cross-encoder reranking, evidence-table
extraction, section-level drafting with a model fallback chain, contradiction surfacing) and, more
importantly to me, the offline evaluation harness it is gated by:

- a **40-query stratified gold set** — verifiable fact, multi-source synthesis, contested, and
  deliberately unanswerable, because an agent that invents an answer should score worse than one
  that abstains;
- **three-tier citation verification** — the link resolves, the page is on-topic, the page actually
  establishes the claim — so a failure is diagnosable rather than just a low number;
- **Cohen's κ calibration** of the LLM judge against hand labels, and an `eval compare` ablation CLI
  that diffs two runs on exactly one changed variable;
- **every pull request replays the gold set against `main` and posts the measured delta as a
  comment** — deterministically, with no API key and no spend — so "no regression" is something you
  can read instead of take on trust;
- **346 offline tests** that run without a key, plus a poisoned-page adversarial fixture that pins
  what the prompt-injection defences do *and* documents the case where they do not hold.

First release: [`v0.5.0`](https://github.com/saksham-jain177/agentic-deep-research/releases/tag/v0.5.0).
Deliberately not `1.0.0`: 4 of the 40 gold queries have replay recordings, so the headline numbers
describe a tenth of the benchmark, and the repo's own pitch is that it does not publish numbers it
cannot reproduce. `1.0.0` waits for full coverage plus a published benchmark page.

**[fastapi-llm-inference](https://github.com/saksham-jain177/fastapi-llm-inference)** — serving layer
over quantized local models: hybrid routing between internal endpoints and external retrieval,
agentic RAG with an internal knowledge base, moderation and judge layers, Prometheus/Grafana
observability, and a [quantization benchmark harness](https://github.com/saksham-jain177/fastapi-llm-inference/blob/main/docs/quantization_benchmark.md).
CI asserts the routing and confidence-gating invariants rather than just running the suite.

## Elsewhere

- 14 merged pull requests across 13 repositories I do not own — Ollama plugins, local-RAG agents, a
  QGIS LLM plugin, Home-Assistant orchestration — each merged after review by that project's
  maintainer. Checkable: `is:pr is:merged author:saksham-jain177`.
- One open PR on [simonw/llm](https://github.com/simonw/llm/pull/1344) making model backends
  resilient to provider-discovery failures.
- Day job: guardrails, model routing and document-pipeline evaluation on a production enterprise AI
  workflow.

## How to read my repos

I would rather you look at the eval results, the CI output and `SECURITY.md` than at the architecture
diagram. The interesting question is not which framework an agent uses; it is how you know it is
right, what it costs, and where it fails.
