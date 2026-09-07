# Module 03 — Exercises

<!-- INSTRUCTOR: Hands-on tasks for the build-along skill. Both exercises use the learner's
     "Teacher Claude" side project as the concrete system, per progress/learner-progress.md,
     unless the learner says otherwise. -->

## Exercise 1 — Design a semantic cache for Teacher Claude

**Goal:** Decide when Teacher Claude's domain-research step should be safe to serve from cache,
and design the time-sensitivity guard that overrides it.

**Steps:**
1. List 3 example domain-research queries Teacher Claude might run repeatedly across different
   certifications (e.g. "explain prompt engineering fundamentals").
2. For each, decide: is this stable knowledge safe to cache, or must it always be answered
   fresh (time-sensitive — e.g. "current supported model list")?
3. Write the time-sensitivity guard's rule in one sentence — what pattern should force a live
   search regardless of how similar the cached match is?
4. Decide your risk tolerance: would you rather risk a **false cache hit** (a stale, wrong
   reused answer) or a **false cache miss** (unnecessary re-research)? Justify the choice for
   a course-prep tool specifically.

**Done when:** You have ≥3 labeled example queries, one clear time-sensitivity rule, and a
justified stance on which failure mode (false hit vs. false miss) is the worse one here.

**Stretch (optional):** The evaluator agent sends a domain's research back for rework. Should
the old cache entry for that domain survive, or must it be invalidated? Why?

## Exercise 2 — Vector store vs. Knowledge Graph for Teacher Claude

**Goal:** For two concrete Teacher Claude questions, decide which retrieval shape (vector RAG or
Knowledge Graph) actually fits, and sketch what that backend would contain.

**Steps:**
1. Take Query A: *"Explain how semantic caching works."*
2. Take Query B: *"Which exam domains must a student master before attempting the Guardrails
   domain?"*
3. For each, pick vector RAG or Knowledge Graph, and justify it using the distinction from
   Concept 6 (fuzzy/explanatory vs. precise/structural).
4. For whichever you picked vector RAG for, name what you'd chunk and embed. For whichever you
   picked Knowledge Graph for, name what the nodes and edges would represent.

**Done when:** Both queries have a justified backend choice and a concrete sketch of what that
backend would actually contain for Teacher Claude.

**Stretch (optional):** In plain English (no real Cypher needed), write one question you'd want
to ask a "prerequisite graph" of exam domains that a vector search could never answer precisely.
