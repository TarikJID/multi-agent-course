# Learner Progress

<!-- Claude reads this at the start of each session and updates it at the end.
     Learners: you don't need to touch this — Claude maintains it. -->

## Learner profile
- Name: [unset]
- Preferred learning style: Socratic
- Started: 2026-09-04
- Last session: 2026-09-14
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
| 03 — Agentic RAG, Semantic Cache & Knowledge Graphs | completed | Lesson + quiz done. Quiz retaken fresh in this session: 5/5, correct on first attempt for every question, no hints needed (agentic routing incl. "whether not just where" to retrieve; time-sensitivity guard bypasses cache regardless of similarity; KG/Text-to-Cypher for precise count/relationship queries vs. vector RAG for fuzzy semantic match; grounding+citations as the structural version of Module 01's "never guess, document only"; LLM-as-judge scores both answers on explicit criteria rather than trusting whichever responded first). Note: a separate claude.ai work-computer session reportedly covered this module too, but its state was never visible here — this session's record (quiz retaken + Exercise 1 done fresh) is the verified one going forward. Exercise 1 (semantic cache design for Teacher Claude) **completed in this session**, including the optional stretch question: 3 labeled example queries (fundamentals=cacheable, current model list=live, ReAct definition=cacheable); generalized the time-sensitivity rule *unprompted* to be topic-based rather than pure-keyword-based (correctly noted a user might ask about model support without saying "current" — the guard has to flag by subject category, not just wording — a genuinely strong extension beyond the lesson); justified biasing toward false-cache-miss over false-cache-hit for an exam-prep tool (asymmetric cost: stale-wrong knowledge risks the exam, extra latency doesn't); on the stretch (does a reworked domain's old cache entry survive?), correctly split false vs. incomplete rather than treating all evaluator-rejections the same — needed one nudge to see that *any* rework verdict should pull the entry from serving live traffic immediately, with the false/incomplete distinction mattering more for whether it's kept as a fallback than for whether it stays live. Exercise 2 (vector RAG vs. knowledge graph) also **completed with its stretch**: correct backend calls for both queries with sound justification; named the `PREREQUISITE_OF` edge and recognised direction matters; on the stretch, correctly identified that a single vector search can't chain a retrieved fact into a second lookup. **Notable:** pushed back hard on my overclaim that vector search "could never" answer a multi-hop query — correctly argued a chunk *could* contain the full chain, forcing a more precise formulation (retrieval returns existing text and never derives new facts; pre-computing every transitive closure doesn't scale). Excellent critical-thinking signal — did not accept an authoritative-sounding but sloppy claim. Gap surfaced and filled: had no recall of Concept 3 (chunking/embedding) and said so rather than bluffing — re-taught briefly, then applied it correctly (chunk lesson.md by concept) and independently asked why one would ever *not* embed a chunk, which opened the answer-key-exclusion point. Also asked two good unprompted questions: whether vector search and KG are both just RAG with different data structures (yes — umbrella vs. backends), and how KGs are physically stored (answered from general knowledge, flagged as beyond the kit's content). |
| 04 — Evaluation & Guardrails | not started | Teaching files **do exist** (all five, authored session 006) — a prior `Next step` note claiming they needed authoring was stale and has been corrected. Still unbattle-tested with a learner. |
| 05 — Multi-Agent Systems (MCP · A2A · ADK) | not started | |
| 06 — Voice Agents | not started | |

Status values: not started · in progress · completed · needs review

## Weak spots to revisit
- Naming "observation" as its own explicit loop step — resolved, did not resurface in Module 02.
- Distinguishing "a sub-step is done" from "the whole task is done" — resolved, did not resurface.
- Isolated context = "where the noise lives," not "shorter prompt" — resolved, answered correctly unprompted on the fresh Module 02 quiz.
- **Subagent definition path — first clean recall (2026-09-14).** Asked cold at the start of the
  session, the learner answered `.claude/agents/<name>.md` immediately, no hint, no hedging. This
  is the item that had been wrong or unsure **three separate times** across two prior sessions
  (quiz.md Q5, the fresh quiz's Q5). The "one file, one hire" mnemonic appears to have landed.
  **Claude: do not mark this resolved yet** — one clean recall after three misses is encouraging,
  not conclusive. Ask it cold again next session, and once more a session after that.
- **Follow-up on the same check went deeper than asked.** Pushed on *why* it matters ("what would
  you lose if the subagent's instructions went in `CLAUDE.md` instead?"), the learner independently
  produced two of the three points: identity collision (the tutor prompt gets overwritten or
  polluted) and invocation ("half tutor, half subagent waiting for instructions that would never
  come, since there is no orchestrator above you" — their words). Missed the third, **context
  isolation** — that a subagent has its own context window and hands back only the conclusion, so
  merging it into `CLAUDE.md` means all the intermediate noise lands in the parent's window. Was
  re-taught and connected back to the already-resolved Module 02 framing ("isolated context = where
  the noise lives"). Worth re-checking, since they had that framing right on the Module 02 quiz but
  did not reach for it here unprompted — suggests it's recallable when cued, not yet automatic.

## Side project: "Certification Trainer" (renamed from "Teacher Claude")
- Learner's own case study (an agent that takes a certification, researches its domains, and
  builds a course from it) — originally a Module 01 hypothetical, now a **real project with its
  own repo**: https://github.com/TarikJID/certification-trainer
- **Repo decision (2026-09-13):** kept separate from `multi-agent-course` rather than a folder
  inside it — it's a real product, not teaching material, and a dedicated repo makes git the
  single source of truth across sessions/machines (this was prompted by the earlier work-computer
  session whose `domain-researcher.md` never reached any repo and is now lost).
- **Status: pipeline complete and pushed.** All four agent definitions written this session,
  each specced by the learner first and then drafted/iterated together:
  - `.claude/agents/domain-mapper.md` — fetches official cert page, returns structured domains.
  - `.claude/agents/evaluator.md` — checks each stage against that stage's own "Done when"
    checklist. **Learner caught the key design tension themselves**: adding web-verification
    risked hardcoding "the official cert page" and destroying reusability across stages.
    Resolved by naming the *relationship* ("verify against whatever source the checklist
    designates") instead of the source.
  - `.claude/agents/domain-researcher.md` — N parallel instances, one per domain; prerequisite
    tracing capped at one level; source-quality and unsourced-disclosure promoted into the
    checklist so the evaluator can actually catch violations.
  - `.claude/agents/course-builder.md` — assembles the course to disk; deliberately has **no web
    tools** so "use only provided material" is enforced by tool scope, not prompt text.
  - `CLAUDE.md` — orchestrator: user-agreement phase, the pipeline, per-stage retry cap (2) with
    escalation, partial re-run on parallel failures, file-path passing to protect context.
- **Bug caught in review:** the orchestrator's file-passing design was unimplementable — mapper
  and researcher had no `Write`, evaluator had no `Read`. Fixed. Good illustration for the
  learner of their own "prompt layer vs. tool layer" insight failing in the other direction.
- **Next milestone:** the real first end-to-end run against an actual certification. Not yet
  done. After that, a separate **tutor agent** (decided this session to keep teaching separate
  from building — the tutor is a separate entry point, not a 7th pipeline step).
- **Claude: keep using this project as the concrete example for module exercises, and
  proactively push toward that first real run** — it's the agreed milestone and everything is
  now in place for it.

## Next step
**The Certification Trainer's first real end-to-end run** — agreed and recommended, not yet started.

Session 2026-09-14 was a short one: a cold recall check (see Weak spots) and a decision about
sequencing. No module was taught. The learner asked which thread to take first and then went to
sleep before the run could begin.

**Recommendation given, and the reasoning to carry forward:** do the Certification Trainer run
*before* Module 04, even though Module 04's materials are ready. Module 04 is about evaluation, and
the learner has already written an `evaluator.md` with retry caps and escalation. Running the
pipeline first means walking into Module 04 holding a real trajectory — where the evaluator passed
something it shouldn't have, where a retry fired, what `domain-researcher` actually produced.
Evaluation taught against their own live failures beats evaluation taught in the abstract, and it
also gives the untested Module 04 material something concrete to be tested against.

**Open question for next session:** which certification to point it at. Not yet chosen.

**Claude, two practical notes for that run:**
- The learner should be present. They built a **user-agreement phase** as the pipeline's first
  step; starting the run without them bypasses the thing they designed. More importantly, the
  value of a first run is watching *where* it breaks — that doesn't survive being summarized.
- The Certification Trainer lives in a **separate repo**
  (https://github.com/TarikJID/certification-trainer), which is not in this session's repository
  scope by default. It needs to be attached (`add_repo`) and cloned before the run.
