# Teacher Claude — Design Doc

<!-- Living spec for the learner's side project, built module-by-module through this course's
     hands-on exercises. Narrative progress/history stays in progress/learner-progress.md; this
     file is the accumulating, reusable SPEC — decisions made in an exercise should land here
     verbatim (not just summarized), so the design is directly buildable when the first real
     end-to-end run happens. -->

## What Teacher Claude is

An agent that takes a topic or exam, researches its knowledge domains, and builds a course +
exercises from it — the learner's own concrete case study, used as the vehicle for this
bootcamp's module exercises. Originally a Module 01 hypothetical; now an actual project to be
built for real (agreed plan: don't wait for all 6 modules — see `progress/learner-progress.md`
for the build-order agreement).

## Architecture

Orchestrator pattern (Module 02):

```
orchestrator
 └─ domain-mapper           → lists the exam's knowledge domains
 └─ evaluator                → validates the domain map before fan-out
 └─ N × domain-researcher    → one spawned instance per domain, in parallel
 └─ evaluator                → validates each domain's research
 └─ course-builder            → turns validated research into a course + exercises
 └─ evaluator                → final quality pass
```

The key refinement the learner caught themselves (Module 02, session 003): `domain-researcher`
is **one role, spawned N times** with different task inputs — not N separately written agents.

## Agent files

| File | Status |
|---|---|
| `.claude/agents/domain-researcher.md` | **Written & iterated** (Module 02 exercise) |
| `.claude/agents/domain-mapper.md` | Not yet written |
| `.claude/agents/evaluator.md` | Not yet written |
| `.claude/agents/course-builder.md` | Not yet written |

Once the remaining three are written the same way, the plan is a real first end-to-end run using
live web search, as its own dedicated step — not gated on finishing the course. Module 03 and 04
then come back and *upgrade* specific pieces (a real knowledge base instead of live search; the
evaluator's "good enough" checklist becoming an actual automated guardrail).

## Retrieval & memory (Module 03)

### Semantic cache — domain-research answers

**Cacheable by default.** Domain-research queries like "explain X" (concept explanations,
mechanisms, definitions) are stable knowledge — new details or best practices might surface
later, but they don't invalidate what's cached, they just make it incomplete. Example queries
used to reason this through: *"explain harness engineering,"* *"explain orchestration,"*
*"explain evaluation guardrails."*

**Time-sensitivity guard rule:** regardless of cache-similarity score, always force a live
search for queries touching:
- certification information that can change (content covered by the exam, pricing)
- official documentation (can be revised)
- fast-moving/edge topics (new techniques, recent model or tooling changes)

**Risk tolerance: favor false cache misses over false cache hits.** A false miss just costs
some wasted re-research. A false hit means the learner studies from something **wrong** and
risks that misconception surviving to the actual exam — the failure costs are asymmetric, so
the system should err toward re-researching when in doubt.

**Cache invalidation policy:** invalidate a domain's cache entry whenever the evaluator sends
that domain's research back for rework — regardless of *why* (outdated, incomplete, or
inaccurate). A rejection from the evaluator is itself proof the cached answer shouldn't be
served again as-is; the trigger is the rejection, not the specific reason for it.

### Retrieval backend choice (vector RAG vs. Knowledge Graph)

*To be filled in as Exercise 2 is completed.*

## Evaluation & guardrails (Module 04)

*Not yet started. Planned upgrade target: the evaluator's "good enough" checklist becomes an
actual automated guardrail instead of a prompt-level instruction.*

## Multi-agent protocol layer (Module 05)

*Not yet started.*

## Voice (Module 06)

*Not applicable unless the learner decides to add a voice interface — not currently planned.*

## Decisions log

| Module | Decision |
|---|---|
| 02 | Orchestrator design: domain-mapper → evaluator → N × domain-researcher → evaluator → course-builder → evaluator. `domain-researcher` is one role, spawned N times in parallel, not N separate agents. |
| 02 | Wrote and iterated the real `domain-researcher.md` agent file; caught and removed an ungrounded "frequent mistakes" output section on review since it invited guessing against the file's own anti-hallucination rule. |
| 03 | Domain-research queries ("explain X") are cacheable by default; time-sensitivity guard triggers on cert content/pricing, official docs, and fast-moving topics. Risk stance: favor false cache misses. Cache invalidated on any evaluator rejection, not just staleness. |
