# Module 04 — Evaluation & Guardrails

<!-- INSTRUCTOR: This is the teaching content Claude walks the learner through.
     Each ## is roughly one "concept" Claude presents, then checks understanding on.
     Source material: Module_4_AI_Evaluation/README.md and AI_Eval_Metrics.ipynb
     (the metric definitions, the five-layer eval pyramid, and the PM decision guide),
     plus the Llama Guard guardrails material referenced there. Keep chunks short. -->

## Learning objectives

By the end of this module the learner can:
- [ ] Explain why "the output looks right" is not evidence that a system works
- [ ] Place a given system on the five-layer eval pyramid and say which layers it actually needs
- [ ] Distinguish **outcome** evaluation from **trajectory** evaluation, and say when each one lies
- [ ] Pick appropriate retrieval and generation metrics for a RAG system (Precision@K, Recall@K, MRR, faithfulness, context utilisation)
- [ ] Name the metrics specific to multi-agent systems, especially error propagation
- [ ] Explain how a runtime guardrail (e.g. Llama Guard) differs from an evaluation, and why a system needs both

## Prerequisites
- Module 01 (the agent loop, ReAct, "good enough" as an explicit checklist)
- Module 02 (orchestrator + subagents, failure modes including cascading failures)
- Module 03 (retrieval, grounded generation, LLM-as-judge)

---

## Concept 1 — Why evaluation is its own discipline

[Every module so far ended with the same unanswered question: *how do you know it worked?* In
Module 01 "good enough" was a checklist you wrote by hand. In Module 03 an LLM-as-judge scored two
answers — but against its own knowledge, with no ground-truth answer key anywhere in the loop.

That gap is the whole subject of this module. A fluent, confident, well-formatted answer is
evidence of *fluency*, not of correctness — and LLMs are far better at fluency than at being right.
Evaluation is the discipline of producing evidence that a system works, separate from how
convincing its output sounds.

The analogy: tasting a dish tells you it's seasoned. It doesn't tell you the chicken is cooked
through. You need a thermometer, and you need to agree in advance what temperature counts.]

**Check:** In Module 03 you said an LLM-as-judge beats "whichever system answered first." What can
that judge still *not* tell you, no matter how good its reasoning is?

## Concept 2 — The eval pyramid (five layers)

[Evaluation metrics stack into a pyramid, and a weakness low down undermines everything above it:

```
   5. Can we trust the system end-to-end?  → Agent Evaluation      ← most complex
   4. Can we trust the generated output?   → RAG Generation
   3. Can we trust the data source?        → RAG Retrieval
   2. Can we trust the reasoning?          → LLM Reasoning
   1. Can we trust the answer?             → LLM Quality           ← foundational
```

The ordering matters: if retrieval (layer 3) returns the wrong documents, measuring generation
quality (layer 4) tells you almost nothing — a beautifully grounded answer built on the wrong source
is still wrong.

Crucially, **not every product needs all five layers.** A simple chatbot lives in layers 1–2. A RAG
assistant adds 3–4. An autonomous agent needs all five. Measuring layers you don't have is wasted
effort; skipping layers you do have is how systems fail silently in production.]

**Check:** Your Certification Trainer pipeline has researchers doing live web search, a builder
assembling their output, and an evaluator checking each stage. Which layers of the pyramid does it
actually need — and is there one it can genuinely skip?

## Concept 3 — Outcome vs. trajectory evaluation

[This is the central distinction of the module.

**Outcome evaluation** asks: *did it produce the right result?* Task Success Rate, correctness,
hallucination rate. It treats the system as a black box — inputs in, answer out, was the answer
right.

**Trajectory evaluation** asks: *was the path it took sound?* Tool Use Accuracy (did it pick the
right tool?), Trajectory Efficiency (how many steps versus the minimum needed?), Step Reasoning
Accuracy, Observation Utilization (did it actually *use* what the tool returned?), and Loop
Termination Correctness (did it stop at the right moment?).

Why you need both: each one lies in a different direction. An agent can reach the **right answer by
a terrible path** — twelve redundant searches, two tools misused, correct by luck — and outcome
evaluation alone will happily call that a success, right up until the day the luck runs out. An
agent can also follow a **perfectly sensible path to a wrong answer**, and trajectory evaluation
alone will applaud it.

Outcome tells you *whether* it worked. Trajectory tells you *whether it will keep working.*]

**Check:** An agent answers a question correctly, but the trace shows it called the same search
tool nine times with near-identical queries and ignored the first eight results. Outcome evaluation
passes it. What specifically would trajectory evaluation catch, and why should you care if the
answer was right anyway?

## Concept 4 — Retrieval metrics (layer 3)

[These measure whether you found the right documents — before asking what the model did with them.

- **Precision@K** — of the K documents retrieved, what fraction are actually relevant? Low
  precision means you're feeding the model noise.
- **Recall@K** — of all the relevant documents that exist, what fraction did you retrieve? Low
  recall means the answer is missing from the context entirely, and no amount of prompting recovers
  it.
- **Mean Reciprocal Rank (MRR)** — how high up the list does the *first* relevant result appear?
  Rank matters because context windows are finite and models weight early context heavily.

Precision and recall pull against each other: retrieve more documents and recall rises while
precision falls. Which one you optimize depends on the cost of each failure — exactly the
false-hit-versus-false-miss tradeoff from Module 03's caching exercise, reappearing at the retrieval
layer.]

**Check:** A RAG system returns 10 chunks; 3 are relevant, and the first relevant one is at position
7. Which metric looks worst here, and what would a user actually experience?

## Concept 5 — Generation metrics (layer 4)

[Now assume retrieval worked. Did the model use what it was given?

- **Faithfulness / Groundedness** — is every claim in the answer supported by the retrieved
  context? This is the measurable version of Module 03's grounded generation, and it's what catches
  *silent blending* — an ungrounded claim sitting in the same confident sentence as a cited one.
- **Answer Relevance** — does the answer actually address the question asked, rather than being
  merely true?
- **Context Utilisation** — how much of the retrieved context was actually used? Very low
  utilisation suggests you retrieved too much, or the wrong things.

The key point: these are *distinct failures*. An answer can be perfectly faithful to its sources and
still not answer the question. Measuring only one hides the other.]

**Check:** Module 03's grounded generation told the model "answer using only this context." Why is
faithfulness-as-a-metric different from that instruction — what does it add?

## Concept 6 — Multi-agent metrics (layer 5)

[Multi-agent systems add failure modes that single-agent metrics can't see:

- **Task Success Rate** — end-to-end, did the whole system deliver?
- **Coordination Score** — did agents hand off correctly, without duplicating or dropping work?
- **Error Propagation Rate** — when one agent produces a bad output, how often does that corruption
  survive downstream instead of being caught?
- **End-to-End Latency** — total wall-clock time, which for parallel stages is the *slowest branch*,
  not the sum.

Error propagation is the one worth dwelling on. It's the measurable version of Module 02's
**cascading failures** failure mode. A multi-agent system's overall reliability isn't the average of
its agents' reliability — errors compound through the chain, and one weak early stage poisons
everything after it. This is precisely why your Certification Trainer puts an evaluator *between*
every stage rather than only at the end.]

**Check:** Your pipeline evaluates after the domain-mapper, after the researchers, and after the
builder. Which of these four metrics is that design specifically optimizing for, and what would go
wrong with a single evaluation at the very end instead?

## Concept 7 — Guardrails vs. evaluation (Llama Guard)

[Evaluation and guardrails are often confused. They operate at different times, with different
powers.

**Evaluation** is measurement, usually *offline*, over a set of examples, producing a score you use
to decide whether to ship or how to tune. It observes; it does not intervene.

**A guardrail** is an *online* safety classifier that runs in the request path and can **block**.
Llama Guard is the canonical example: a model that classifies both **inputs** and **outputs**
against an explicit safety policy (violence, self-harm, privacy, and so on) and returns safe/unsafe
with the violated category. If it says unsafe, the request or response is stopped before reaching
the user.

Two things to hold onto. First, guardrails check **both directions** — screening user input alone
misses the case where a benign prompt produces a harmful completion. Second, this is the
**architectural** version of a rule you would otherwise merely *ask* for in a prompt — the same
distinction you hit building Certification Trainer, where a subagent's tool scope enforced what its
prompt could only request.

You need both: a guardrail with no evaluation is unmeasured, and evaluation with no guardrail can't
stop anything at 3am.]

**Check:** A system prompt says "never give medical dosage advice." Why is that weaker than a
guardrail classifier, and what class of failure does the guardrail catch that the prompt doesn't?

---

## Summary

The key takeaways from this module:
1. Fluent output is evidence of fluency, not correctness — evaluation is how you get actual evidence.
2. Metrics stack in a five-layer pyramid; weakness at a lower layer invalidates measurements above it, and you only need the layers your system actually has.
3. Outcome evaluation asks whether it worked; trajectory evaluation asks whether it will keep working. Each hides a failure the other catches.
4. Retrieval (Precision@K, Recall@K, MRR) and generation (faithfulness, relevance, context utilisation) measure different things and fail independently.
5. In multi-agent systems, error propagation compounds — reliability is not the average of your agents' reliability, which is why evaluation goes *between* stages.
6. Guardrails run online and block; evaluations run offline and measure. A production system needs both.

## Where to next
- Exercises: `exercises.md` — design an eval plan and a guardrail policy for Certification Trainer.
- Quiz: `quiz.md` — five questions covering the pyramid, the outcome/trajectory split, and guardrails.
- Then Module 05 (Multi-Agent Systems: MCP · A2A · ADK), where the coordination you've been
  hand-rolling gets a real protocol layer.
