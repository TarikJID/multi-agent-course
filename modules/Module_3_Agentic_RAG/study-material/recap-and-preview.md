# Module 03 — Recap & Preview (15-Minute Warm-Up)

<!-- INSTRUCTOR: A quick "before class" bridge. Recaps Module 02 and previews Module 03.
     Designed for a ~15-min review with Claude right before the live session. -->

## Last time (Module 02 — Skills, Subagents & Multi-Agent Orchestration)
The big ideas you should still have in your head:
- A subagent's **isolated context window** — not raw horsepower — is why multi-agent beats one
  long prompt.
- The orchestrator pattern: sequential where work depends on prior output, parallel where it
  doesn't; a **shared spec** keeps parallel agents consistent without talking to each other.
- Specialize by **domain, not volume** — and each multi-agent failure mode has a specific
  design fix.

**Quick gut-check:** What's the one artifact that lets Sprint Zero's backend and frontend
agents build in parallel without ever communicating?

## How it connects
Module 02 was about coordinating multiple *agents*. Module 03 is about giving any one of those
agents better *memory* — instead of guessing from training data or blindly calling live search
every time, it reasons about where to actually look: a vector store, a knowledge graph, a
cache, or the live web.

## Coming up (Module 03 — Agentic RAG, Semantic Cache & Knowledge Graphs)
What you'll be able to do after today:
- Explain what makes RAG "agentic" instead of one fixed retrieval path
- Trace embed → vector store → retrieve → grounded, cited generation
- Explain semantic caching, and why a time-sensitivity guard can override it entirely
- Contrast vector retrieval with Knowledge Graph / Text-to-Cypher retrieval — and know when
  each wins
- Use an LLM-as-judge to evaluate, objectively, which retrieval approach actually answered
  better

**Watch for:** the difference between "this looks similar, so serve it from cache" and "this
needs a fresh answer no matter what." Conflating those two is the easiest mistake to make in
this module.

## If you only remember one thing walking into class
> Retrieval isn't one fixed step — it's a decision. The agent should reason about *where* to
> look (vector store? graph? cache? live web?) before it ever runs the search.
