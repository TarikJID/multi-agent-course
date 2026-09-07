# Learner Progress

<!-- Claude reads this at the start of each session and updates it at the end.
     Learners: you don't need to touch this — Claude maintains it. -->

## Learner profile
- Name: [unset]
- Preferred learning style: Socratic
- Started: 2026-09-04
- Last session: 2026-09-07
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
| 02 — Skills, Subagents & Multi-Agent Orchestration | completed | All 7 concepts taught + fresh non-reused quiz (5/5, all correct on substance, no retries needed — confidence concern from session 1 resolved) + both exercises done via the "Teacher Claude" project (agent-team design incl. self-caught parallelization opportunity within the researcher role; wrote a real `.claude/agents/domain-researcher.md` file, iterated twice on feedback, then independently caught and removed its own prompt-drift risk in the final review). Also independently generalized "prompt vs. tool access" as two separate layers (harness/permissions vs. system prompt text) beyond what the lesson states. |
| 03 — Agentic RAG, Semantic Cache & Knowledge Graphs | in progress | |
| 04 — Evaluation & Guardrails | not started | |
| 05 — Multi-Agent Systems (MCP · A2A · ADK) | not started | |
| 06 — Voice Agents | not started | |

Status values: not started · in progress · completed · needs review

## Weak spots to revisit
- Naming "observation" as its own explicit loop step — resolved, did not resurface in Module 02.
- Distinguishing "a sub-step is done" from "the whole task is done" — resolved, did not resurface.
- Isolated context = "where the noise lives," not "shorter prompt" — resolved, answered correctly unprompted on the fresh Module 02 quiz.
- **Persistent, not yet resolved:** exact location of subagent definitions (`.claude/agents/<name>.md` vs `CLAUDE.md`) has now been wrong or unsure **three separate times** across two sessions (quiz.md Q5, the fresh quiz's Q5, both needing the same correction). This is the one item from the "vocabulary/exact-names" accommodation that hasn't budged yet despite repeated correction — give it real priority in the cheat sheet's "exact names" section (mnemonic already given: "one file, one hire") and check it again next session rather than assuming it's fixed.

## Side project: "Teacher Claude"
- Learner's own case study (an agent that takes a topic/exam, researches the domains, and builds
  a course + exercises from it) — originally a Module 01 hypothetical, now an **actual side
  project** built for real, using each module's exercise as the concrete vehicle.
- Progress so far: full orchestrator design done (domain-mapper → evaluator → N parallel
  domain-researchers → evaluator → course-builder → evaluator), including the learner catching
  their own "one researcher role, many parallel instances" refinement. One real agent file
  written and iterated: `.claude/agents/domain-researcher.md`.
- **Build plan agreed with the learner** (they asked directly "when do I actually build this for
  real?"): don't wait for all 6 modules. Once the remaining agent files (`domain-mapper`,
  `evaluator`, `course-builder`) are written the same way, do a real first end-to-end run using
  live web search — as its own dedicated step, not gated on course completion. Module 03
  (Agentic RAG) and Module 04 (Evaluation & Guardrails) then come back and *upgrade* specific
  pieces (a real knowledge base instead of live search; the evaluator's "good enough" checklist
  becoming an actual automated guardrail) rather than blocking the first working version.
- **Claude: use this project as the concrete example for future module exercises by default,
  and proactively flag when a natural moment arrives to write the remaining 3 agent files and
  do that first real run** — don't wait for the learner to ask again.

## Next step
- Begin Module 03 (Agentic RAG, Semantic Cache & Knowledge Graphs).
