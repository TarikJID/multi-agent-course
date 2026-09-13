# Module 04 — Quiz

<!-- INSTRUCTOR: The quiz-me skill uses these. Answers are here so Claude can check,
     but the rule is Claude NEVER shows them before the learner attempts. Hint first. -->

## Q1. An agent answers a user's question correctly. The trace shows it called the same search tool
nine times with near-identical queries, ignored the first eight sets of results, and finally
answered from the ninth. Outcome evaluation marks this a success. What's the problem?
- Type: application
- **Answer:** Trajectory evaluation would fail it — poor Trajectory Efficiency and poor Observation
  Utilization. The correct answer was reached despite the path, not because of it, so the success
  doesn't generalize: the same behaviour on a harder query, a slower tool, or a stricter budget will
  produce a wrong or timed-out answer. Outcome tells you whether it worked; trajectory tells you
  whether it will keep working.
- **Hint:** Outcome evaluation treats the system as a black box. What does that specifically hide
  here, and what happens the next time luck isn't on its side?

## Q2. A RAG system retrieves 10 chunks. Three are genuinely relevant, and the first relevant one
appears at position 7. Which metric looks worst, and what does the user actually experience?
- Type: application
- **Answer:** MRR (Mean Reciprocal Rank) — the first relevant result is buried at rank 7, giving a
  reciprocal rank of 1/7. Precision@10 is a mediocre 0.3, but the ranking is the sharper failure:
  six irrelevant chunks occupy the context ahead of anything useful, and since models weight early
  context heavily, the answer is likely to be vague, off-target, or drawn from the noise.
- **Hint:** Two things are being measured here — *how many* of the results are good, and *where* the
  good ones sit. Which of those is the 7 telling you about?

## Q3. Why does putting an evaluator between every stage of a multi-agent pipeline matter more than
one thorough evaluation at the end?
- Type: explain-why
- **Answer:** Error Propagation Rate. In a chained system, a bad output from an early stage is
  consumed as input by every stage after it, so the corruption compounds — overall reliability is
  not the average of the individual agents' reliability. Evaluating only at the end tells you the
  result is wrong but not *where* it went wrong, and wastes all the downstream work built on a bad
  foundation. This is Module 02's cascading-failure mode, now measurable.
- **Hint:** Think about what a wrong domain map does to every researcher downstream of it — and what
  a single end-of-pipeline check could and couldn't tell you about that.

## Q4. A system prompt says "never give medical dosage advice." Why is a Llama Guard-style guardrail
stronger than that instruction, and what does it catch that the prompt doesn't?
- Type: explain-why
- **Answer:** The prompt is a request the model may fail to honour under pressure, unusual phrasing,
  or a jailbreak; the guardrail is a separate classifier in the request path that can actually
  **block**. Crucially it screens **outputs as well as inputs** — so it catches the case where a
  perfectly benign-looking question produces a harmful completion, which input-side prompting can
  never catch. It's the architectural version of a rule, not the requested version — the same
  distinction as enforcing a subagent's limits through its tool scope rather than its prompt text.
- **Hint:** Where in the request path does each one sit, and which direction does each one actually
  inspect?

## Q5. Why can't you measure the quality of a RAG system's generation layer meaningfully if its
retrieval layer is performing badly?
- Type: explain-why
- **Answer:** Because the pyramid stacks — a weakness at a lower layer invalidates measurements
  above it. If retrieval returned the wrong documents, then an answer that is perfectly *faithful*
  to that context is still wrong, and a high faithfulness score is actively misleading: it certifies
  that the model used its sources properly, while saying nothing about whether those sources were
  the right ones. You have to fix layer 3 before layer 4's numbers mean anything.
- **Hint:** Imagine an answer that scores perfectly on faithfulness but is completely wrong. What
  must have happened one layer down for that to be possible?
