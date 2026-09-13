# Module 04 — Recap & Preview (15-Minute Warm-Up)

<!-- INSTRUCTOR: A quick "before class" bridge. Recaps Module 03 and previews Module 04.
     Designed for a ~15-min review with Claude right before the live session. -->

## Last time (Module 03 — Agentic RAG, Semantic Cache & Knowledge Graphs)

The big ideas you should still have in your head:
- **Agentic RAG routes before it retrieves.** A reasoning step decides *where* — or *whether* — to
  retrieve, instead of every query hitting the same vector store. That's ReAct's Thought step,
  applied to picking a knowledge source.
- **Semantic caching reuses past answers, and a time-sensitivity guard overrides it.** The guard
  runs *before* the similarity check, so no similarity score, however high, can save a stale answer.
- **Vector search and Knowledge Graphs are two backends under one umbrella.** Vector = fuzzy,
  explanatory, "find things that mean something similar." Graph = exact, structural, "find things
  that are connected." Retrieval returns existing text; it never *derives* a new fact by chaining
  two retrieved ones.
- **Grounded generation with citations** ties each claim to a checkable source — but it's a
  prompt-level instruction, not a guarantee.

**Quick gut-check:** Why isn't a very high cache-similarity score, on its own, enough to justify
serving a cached answer?

## How it connects

Module 03 ended on an unresolved tension. Grounded generation *asks* the model to stay faithful to
its sources. The LLM-as-judge *scores* competing answers — but against its own knowledge, with no
ground-truth answer key anywhere in the loop. Both are soft: one is a request, the other is an
opinion.

Module 04 is where that gets hardened. Evaluation turns "it looks right" into measured evidence, and
guardrails turn "please don't" into something that can actually block.

## Coming up (Module 04 — Evaluation & Guardrails)

What you'll be able to do after today:
- Place any system on the five-layer eval pyramid and say which layers it actually needs
- Tell outcome evaluation from trajectory evaluation, and say when each one lies to you
- Choose the right retrieval and generation metrics for a RAG system
- Explain why error propagation makes multi-agent reliability worse than the average of its parts
- Say precisely how a runtime guardrail differs from an evaluation, and why you need both

**Watch for:** the outcome/trajectory split is the concept people flatten into "two ways of checking
the same thing." They're not. Each one *passes* a failure the other catches — a right answer reached
by a broken path, and a sound path to a wrong answer. Hold both cases in mind and the distinction
stays sharp.

## If you only remember one thing walking into class

> A fluent answer is evidence of fluency, not of correctness. Evaluation measures; guardrails block;
> a production system needs both, because measurement can't stop anything and blocking tells you
> nothing about how often you were right.
