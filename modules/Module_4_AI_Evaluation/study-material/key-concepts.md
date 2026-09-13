# Module 04 — Key Concepts (Glossary)

<!-- INSTRUCTOR: Short, accurate definitions Claude uses to stay precise.
     The explain-eli5 skill reads from here to simplify without becoming wrong. -->

## The discipline

- **Evaluation** — Producing evidence that a system works, separate from how convincing its output
  sounds; usually offline, over a set of examples, yielding a score.
- **Eval pyramid** — The five stacked layers of evaluation: LLM Quality → LLM Reasoning → RAG
  Retrieval → RAG Generation → Agent Evaluation. A weakness at a lower layer invalidates
  measurements above it.
- **Ground truth** — An externally-supplied correct answer used as the reference for scoring. Its
  absence is the core limitation of an LLM-as-judge setup.

## Outcome vs. trajectory

- **Outcome evaluation** — Measures whether the final result was correct, treating the system as a
  black box (e.g. Task Success Rate, correctness, hallucination rate).
- **Trajectory evaluation** — Measures whether the *path* to the result was sound, using the
  execution trace rather than just the final answer.
- **Task Success Rate** — The fraction of tasks where the system delivered the correct end result.
- **Tool Use Accuracy** — Whether the agent selected the appropriate tool for each step.
- **Trajectory Efficiency** — How many steps the agent took relative to the minimum needed.
- **Observation Utilization** — Whether the agent actually used the information a tool returned,
  rather than ignoring it and proceeding regardless.
- **Loop Termination Correctness** — Whether the agent stopped at the right point: neither halting
  early nor looping past the point of completion.

## Retrieval metrics (layer 3)

- **Precision@K** — Of the K retrieved documents, the fraction that are actually relevant. Low
  precision = feeding the model noise.
- **Recall@K** — Of all relevant documents that exist, the fraction retrieved. Low recall = the
  answer isn't in the context at all, and no prompting recovers it.
- **Mean Reciprocal Rank (MRR)** — How high the *first* relevant result appears in the ranked list;
  rank matters because context is finite and early context is weighted heavily.

## Generation metrics (layer 4)

- **Faithfulness / Groundedness** — Whether every claim in the answer is supported by the retrieved
  context. The measurable counterpart to Module 03's grounded generation.
- **Answer Relevance** — Whether the answer addresses the question actually asked, as opposed to
  merely being true.
- **Context Utilisation** — How much of the retrieved context the answer actually drew on; very low
  utilisation suggests over-retrieval or wrong retrieval.

## Multi-agent metrics (layer 5)

- **Coordination Score** — Whether agents hand off correctly, without duplicated or dropped work.
- **Error Propagation Rate** — How often a bad output from one agent survives downstream instead of
  being caught. The measurable form of Module 02's cascading-failure mode.
- **End-to-End Latency** — Total wall-clock time for the whole system; for parallel stages this is
  the slowest branch, not the sum.

## Guardrails

- **Guardrail** — An online safety classifier that runs in the request path and can *block* a
  request or response, as opposed to an evaluation, which only measures.
- **Llama Guard** — A safety classifier model that checks both inputs and outputs against an
  explicit policy and returns safe/unsafe plus the violated category.
- **Input vs. output screening** — Checking both directions; screening only user input misses the
  case where a benign prompt yields a harmful completion.
- **Safety & Guardrail Compliance** — The agent-level metric tracking how often the system's
  behaviour stays within its defined safety policy.

## Supporting vocabulary (from the notebook)

- **Hallucination Rate** — The frequency with which the system states unsupported claims as fact.
- **Chain-of-Thought Faithfulness** — Whether the reasoning the model shows is the reasoning that
  actually produced its answer.
- **Perplexity** — A measure of how "surprised" a model is by text; an efficiency/fluency signal,
  **not** a correctness signal (low perplexity ≠ factually correct).
