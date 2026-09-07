# Module 03 — Agentic RAG, Semantic Cache & Knowledge Graphs

<!-- INSTRUCTOR: This is the teaching content Claude walks the learner through.
     Each ## is roughly one "concept" Claude presents, then checks understanding on.
     Source material: Module_3_Agentic_RAG/README.md and its notebooks (Agentic_RAG/,
     Semantic_Cache/, Knowledge_Graphs/, Moment_RAG/). Keep chunks short. -->

## Learning objectives

By the end of this module the learner can:
- [ ] Explain what makes RAG "agentic" rather than a fixed, single-path pipeline
- [ ] Trace how a query gets embedded, stored, and retrieved via a vector database
- [ ] Explain semantic caching and why a time-sensitivity guard can override it entirely
- [ ] Contrast vector-based retrieval with graph-based (Knowledge Graph / Text-to-Cypher)
      retrieval, and know when each wins
- [ ] Describe how an LLM-as-judge objectively evaluates which retrieval approach answered better
- [ ] Reason about hybrid memory: combining retrieval backends behind one routing decision

## Prerequisites
- Module 01 (the agent loop, ReAct — the query router below is that same Thought→Action shape,
  applied specifically to picking a knowledge source). Module 02 is helpful context but not
  required.

---

## Concept 1 — What makes RAG "agentic"

[A plain RAG pipeline is fixed: every query gets embedded, searched against the *same* vector
store, and answered from whatever comes back — no matter what was actually asked. **Agentic
RAG** puts a reasoning step first: the system decides *where* to look (or whether to retrieve
at all) before ever touching a retriever. This is the exact ReAct shape from Module 01 — Thought
("what kind of query is this?") → Action (call the right retrieval tool) → Observation (get
results) → generate — just specialized around choosing a knowledge source instead of a general
tool.]

**Check:** Given "What was Uber's 2021 revenue?" and "What's the weather right now in Paris?" —
would a single fixed retrieval path handle both well? What would an agentic router do
differently?

## Concept 2 — Query routing

[The router is a dedicated LLM call whose only job is classification: given the query, it
outputs a structured decision (an action label + a reason) telling the system which path to
take — search corpus A, search corpus B, or hit live web search. Making this its own explicit,
structured step (rather than leaving the choice implicit inside one big generation call) means
it can be logged, tested, and evaluated on its own — the same way Module 02 separated
*coordination* from *execution*.]

**Check:** Why might you want the routing decision to be a separate, inspectable LLM call with
structured output, rather than letting one big model "figure it out" silently while generating
the final answer?

## Concept 3 — Vector embeddings & retrieval

[To retrieve anything, documents first get **chunked** (split into passages), and each chunk is
converted into a **vector embedding** — a dense numeric representation of its meaning — then
stored in a **vector database** (e.g. Qdrant). At query time, the query itself gets embedded the
same way, and the database returns the chunks whose vectors are closest (by cosine or L2
distance). Chunk size is a real design decision: too large and the relevant sentence drowns in
irrelevant surrounding text; too small and it loses the context needed to make sense of it.]

**Check:** If a 50-page PDF is chunked into one giant chunk per 10 pages, what's likely to go
wrong when the system retrieves the "top 3 chunks" for one specific one-sentence fact?

## Concept 4 — Grounded generation with citations

[Once relevant chunks are retrieved, they're placed directly in the generation prompt, and the
model is instructed to answer using *only* that context — with inline citations pointing back to
which chunk supports each claim. This is Module 01's "never guess, document only" guardrail,
now enforced at the architecture level instead of only being a line in a prompt: the answer is
structurally tied to checkable evidence, not just asked to behave.]

**Check:** Why does citing back to specific retrieved chunks make an answer more trustworthy
than asking the model to "just answer from what you know"?

## Concept 5 — Semantic caching (and the time-sensitivity guard)

[Many incoming queries are similar to ones already answered. A **semantic cache** embeds each
new query and checks whether a sufficiently similar past query exists (distance under a
threshold); if so, it returns the stored answer instantly instead of re-running retrieval and
generation — a huge win for latency and cost. But some queries must **never** be served from
cache: anything time-sensitive ("what's happening right now," "today's outage") needs a live
answer, since a cached response can go stale within minutes. A keyword/pattern check for
time-sensitivity runs *before* the cache lookup and can override it completely.]

**Check:** Why isn't a high cache-similarity score enough on its own to decide whether to serve
from cache — what failure case forces a completely separate time-sensitivity check?

## Concept 6 — Knowledge Graphs & Text-to-Cypher: a different retrieval shape

[Vector search finds semantically *similar* text — excellent for fuzzy, explanatory questions,
poor for precise structural ones ("how many X are connected to Y," "list all Z matching this
relationship"). A **Knowledge Graph** models entities and relationships explicitly as nodes and
edges (e.g. in Neo4j). Instead of embedding-similarity search, an LLM translates the
natural-language question into a **Cypher** query that runs directly against the graph —
producing an exact, structured answer rather than a "closest match."]

**Check:** For "How many companies in our dataset share a headquarters city with their top
competitor?" — vector search over document chunks, or a Knowledge Graph query? Why?

## Concept 7 — Hybrid retrieval and choosing objectively

[No single backend wins every query — a real system routes some questions to vector RAG, some
to a Knowledge Graph, some to live search, some to cache. But how do you know, for a given
question, which backend actually produced the better answer? An **LLM-as-judge** independently
scores a RAG answer and a Knowledge Graph answer against the same question on explicit criteria
(accuracy, completeness, precision) and picks a winner — a preview of the more rigorous
evaluation methodology Module 04 formalizes.]

**Check:** What's the advantage of a separate LLM judge scoring RAG vs. KG answers, instead of
just trusting whichever pipeline responded first?

---

## Summary
1. Agentic RAG reasons about *where* to retrieve before retrieving — the same ReAct shape from
   Module 01, applied to knowledge-source selection.
2. The default path is embed → store → similarity search → grounded generation with citations;
   semantic caching reuses past answers for speed, but a time-sensitivity guard must be able to
   override it entirely.
3. Knowledge Graphs answer precise structural questions vector search can't; hybrid systems
   route between backends and use an LLM-as-judge to evaluate, objectively, which one won.

## Where to next
- Do `exercises.md` (design a semantic cache and a retrieval-backend choice, both using
  "Teacher Claude" as the concrete system), or ask to be quizzed (`quiz.md`).
