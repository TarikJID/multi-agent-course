# Learner Progress

<!-- Claude reads this at the start of each session and updates it at the end.
     Learners: you don't need to touch this — Claude maintains it. -->

## Learner profile
- Name: [unset]
- Preferred learning style: Socratic
- Started: 2026-09-04
- Last session: 2026-09-06
- Learner-stated accommodation: has trouble retaining precise vocabulary / exact file paths
  (e.g. `.claude/agents/<name>.md` vs `CLAUDE.md` mixed up twice across two sessions).
  Conceptual reasoning is consistently strong — the gap is specifically exact names/locations.
  **Claude: give this its own emphasis** — in the cheat sheet, keep a dedicated "exact names &
  commonly confused" reference (not just definitions), use mnemonics, and re-verify recall of
  exact terms/paths periodically rather than assuming a past correction stuck.

## Companion cheat sheet
- Artifact: "Bootcamp Blueprint" — https://claude.ai/code/artifact/e02cd05e-da98-4cb3-9cbf-e82e66bee081
- **Claude: update this artifact at the end of every teaching session** — add new concept
  cards + 2-4 condensed Q&A field notes to the relevant sheet (or add a new sheet section
  for a newly started module), append one row to its Revision Log table, and bump the
  masthead's session count / last-revision date. Republish to the same URL above (do not
  create a new artifact).

## Module status

| Module | Status | Notes / weak spots |
|--------|--------|--------------------|
| 01 — Agents, ReAct & the Harness | completed | Quiz 4/4 + both exercises done. Recurring pattern to watch: folds "observation" into surrounding actions instead of naming it explicitly (showed up in quiz Q2 and again in Exercise 2 loop trace); also initially conflated "this sub-step is done" with "the whole task is done" (domain-listing ≠ finished; one domain passing its checklist ≠ overall stop_reason) — self-corrected once flagged both times. Strong grasp of agent def, loop, arch levels, ReAct, harness, and defining "good enough" as an explicit checklist rather than a vibe. |
| 02 — Skills, Subagents & Multi-Agent Orchestration | in progress | All 7 concepts taught (agent def, isolated context windows, orchestrator pattern, subagent files, specialization, failure modes, Sprint Zero). Quiz.md done 5/5, but needed retries on Q1 (isolation vs. length) and Q5 (subagent file location/what it becomes) — learner does not yet feel confident despite passing. Exercises not yet done. Two genuine misconceptions surfaced and were self-corrected once flagged: (1) proposed parallel agents "asking each other" for mid-task tweaks, which breaks the whole point of independence via a shared spec; (2) confused CLAUDE.md (project-wide instructions) with a subagent definition file. One excellent beyond-the-lesson insight: correctly reasoned that ticket-level/incremental QA (dispatched via the orchestrator per completed unit) is a valid finer-grained variant of the same orchestrator pattern, not a violation of "agents don't talk mid-task" — and independently connected this to why Sprint Zero still needs a *separate* end-to-end QA pass (integration bugs invisible to per-ticket checks). |
| 03 — Agentic RAG, Semantic Cache & Knowledge Graphs | not started | |
| 04 — Evaluation & Guardrails | not started | |
| 05 — Multi-Agent Systems (MCP · A2A · ADK) | not started | |
| 06 — Voice Agents | not started | |

Status values: not started · in progress · completed · needs review

## Weak spots to revisit
- Naming "observation" as its own explicit loop step, rather than folding it into the surrounding action — recurred twice in Module 01, self-corrected both times when flagged. Did not resurface in Module 02.
- Distinguishing "a sub-step/part is done" from "the whole task is done" (premature stop_reason). Same self-correction pattern as above.
- Module 02: isolated context = "where the noise lives," not "shorter prompt" (needed a nudge on Quiz Q1).
- Module 02: exact file location for subagent definitions (`.claude/agents/<name>.md`) didn't stick on first or second try — worth a quick recall check next session before moving on.
- Learner explicitly flagged low confidence on Module 02 despite passing the quiz 5/5 — treat that as signal, not just the score. Requested a *fresh, non-reused* quiz next session (not quiz.md verbatim, since they've now seen those questions) to properly test retention.

## Side project: "Teacher Claude"
- Learner's own case study (an agent that takes a topic/exam, researches the domains,
  and builds a course + exercises from it) — originally used as a hypothetical for
  Module 01's exercises, now upgraded to an **actual side project** we build for real,
  using each module's exercise as the concrete vehicle rather than one-off toy examples.
- Planned trajectory: prototype the researcher/builder/evaluator agent team as Module 02's
  exercise (design an agent team + write a real subagent file); revisit with Agentic RAG
  (Module 03) for real knowledge retrieval instead of live search each time; revisit with
  Evaluation & Guardrails (Module 04) to turn the "good enough per domain" checklist from
  Module 01 into an actual automated check.
- **Claude: when starting Module 02's exercise next session, use this project as the
  concrete example** unless the learner says otherwise.

## Next step
- Start next session with a freshly-generated Module 02 quiz (from lesson.md/key-concepts.md, not quiz.md) to verify confidence before moving on.
- Then do Module 02's hands-on exercise (design an agent team + write a real subagent file) using "Teacher Claude" as the concrete project, if the fresh quiz goes well.
