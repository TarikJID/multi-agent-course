# Learner Progress

<!-- Claude reads this at the start of each session and updates it at the end.
     Learners: you don't need to touch this — Claude maintains it. -->

## Learner profile
- Name: [unset]
- Preferred learning style: Socratic
- Started: 2026-09-04
- Last session: 2026-09-15
- Learner-stated accommodation: has trouble retaining precise vocabulary / exact file paths
  (e.g. `.claude/agents/<name>.md` vs `CLAUDE.md` mixed up twice across two sessions).
  Conceptual reasoning is consistently strong — the gap is specifically exact names/locations.
  **Claude: give this its own emphasis** — in the cheat sheet, keep a dedicated "exact names &
  commonly confused" reference (not just definitions), and use mnemonics.
  **Do NOT re-quiz the learner on terms logged as RESOLVED below.** On 2026-09-15 they pointed
  out they had answered the subagent-path question "5 or 6 times now" and that the repetition
  made it feel like the progress file wasn't working. They were right: the file kept recording
  *the instruction to check* without ever letting a correct answer close the item. Trust the
  RESOLVED entries. Only re-check a term if they actually get it wrong in the course of normal
  work — never as an opener.

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
| 04 — Evaluation & Guardrails | in progress | **Concepts 1, 2, 3, 6, 7 landed well. Concepts 4 (retrieval metrics) and 5 (generation metrics) did NOT — re-teach them from scratch.** See the session log below: Claude skipped 4 and 5 entirely, taught 3 without naming its metrics, then quizzed on all three. The learner caught it twice, correctly. Quiz abandoned after Q2; do not count it. |
| 05 — Multi-Agent Systems (MCP · A2A · ADK) | not started | |
| 06 — Voice Agents | not started | |

Status values: not started · in progress · completed · needs review

## Weak spots to revisit
- Naming "observation" as its own explicit loop step — resolved, did not resurface in Module 02.
- Distinguishing "a sub-step is done" from "the whole task is done" — resolved, did not resurface.
- Isolated context = "where the noise lives," not "shorter prompt" — resolved, answered correctly unprompted on the fresh Module 02 quiz.
- **RESOLVED — subagent definition path (`.claude/agents/<name>.md`). Closed 2026-09-15.**
  Clean cold recall on 2026-09-14 *and* again on 2026-09-15, after three earlier misses. On
  2026-09-15 the learner also volunteered the conceptual split unprompted: `CLAUDE.md` = purpose
  and rules of the whole project / orchestration; `.claude/agents/<name>.md` = one specific
  subagent's job, tools, inputs, outputs, do's and don'ts. Mnemonic that landed: "one file, one
  hire". Almost certainly cemented by building the Certification Trainer repo, which has exactly
  that shape. Two clean recalls plus an unprompted conceptual account is enough. **Do not ask
  this again.**
- **Open (conceptual, not vocabulary): context isolation as a reason for separate agent files.**
  On 2026-09-14, pushed on *why* the split matters, the learner independently produced identity
  collision and invocation ("half tutor, half subagent waiting for instructions that would never
  come, since there is no orchestrator above you" — their words) but did not reach for **context
  isolation** — that a subagent has its own context window and hands back only the conclusion, so
  merging it into `CLAUDE.md` puts all the intermediate noise in the parent's window. They had the
  Module 02 framing ("isolated context = where the noise lives") right on that quiz, so it is
  recallable when cued but not yet automatic. **Do not test this with a direct question.** It will
  come up naturally during the Certification Trainer run — the four agents exist partly for this
  reason — so surface it there, in context.

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

## Session log — 2026-09-16: the run finished, and Module 04 half-landed

**1. The first end-to-end run completed.** It was never a failure — it was blocked on an
`AskUserQuestion` the learner hadn't seen. Once they granted the extra round, the pipeline ran to
completion and shipped a full course: `courses/claude-certified-architect-foundations/`, 6 modules ×
(lesson + exercises + quiz), ~3,880 lines, 115 concepts, none dropped. `course-builder` synthesised a
Module 1 Foundations that wasn't in the domain map (pulling every `prerequisite`-tagged concept across
all five research files) and sequenced by dependency rather than exam weight, explaining its reasoning
in the outline. The evaluator also caught the build stage (`Add three missing prerequisites to course
Module 6`). The sourcing guardrail held all the way through: the one unsourceable concept was taught
with a visible sourcing note in the learner-facing lesson, not fabricated.

**2. Two root causes found and pushed** to `TarikJID/certification-trainer` `main` (commit `57d61a4`):
- `domain-researcher` and `domain-mapper` had `Write` but no `Read`. Invisible on the first pass (web
  tools return content directly) but every rework round forced regenerate-from-scratch or a full paste
  through the orchestrator's context. Most of the run's $28.78. Both now have `Read`.
- `domain-mapper` summarised the exam guide and dropped the source. Only 3 task statements survive
  anywhere in ~5,000 lines; `domain-map.md` has zero. Spec now requires archiving the source and
  reproducing every task statement **verbatim**, with an auditable escape hatch.

**3. Concepts the learner derived unprompted** (before being taught them): ground truth and its
absence; that you can't fix the evaluator-regress by stacking another evaluator; that an escape hatch
is safe exactly when using it is auditable; that a system can fail with every component behaving
correctly. Strong session on the conceptual side.

**4. TEACHING ERROR — read this before the next Module 04 session.** Claude taught Concepts 1, 2, 6, 7
properly, gave Concept 3 only as an analogy without ever naming its metrics, and **skipped Concepts 4
and 5 entirely** — then ran the quiz, whose Q1 and Q2 depend on exactly that material. The learner
said "I don't feel like we've seen these concepts before" (correct) and then "we're going over these
concepts too fast, I don't really ingest them" (also correct). Both times they were right and Claude
was wrong. **Trust these signals immediately — they are reliable and they are not a confidence
problem.** Diagnosis that seemed to fit: the material that landed was material the learner derived
from their own run; Concepts 4/5 are abstract metrics for a system they don't have (no vector store,
no index), delivered as a vocabulary list and tested immediately. Re-teach 4 and 5 slowly, anchored to
something concrete — the module's `AI_Eval_Metrics.ipynb` has real numbers, or frame it as
"did the researcher pull the right pages?" = Precision@K over web-search results.

Partial credit worth keeping: on Q1 the learner correctly identified that no efficiency standard was
defined to fail against (a real Module 01-flavoured insight), but missed the generalisation point.
On the retrieval check they named MRR correctly; the "what the user experiences" half was muddled.

## Next step

**DEADLINE: the learner has a $100 claude.ai promotional credit expiring 19 Sept.** (Not API credit —
console.anthropic.com holds only $1.55. It applies to claude.ai usage, most likely funding overage
once a 5-hour window is exhausted.) Agreed plan, and a `send_later` reminder is armed for
**18 Sept 07:00 UTC** carrying the pre-run checklist (`trig_019FPHLgheKC4msgYZYhRwDz`):

| When | What |
|---|---|
| 17 Sept | Implement improvements — **trajectory logging is the big one** |
| 17 eve / 18 am | **Pilot: `domain-mapper` alone.** Cents. Proves the new verbatim-task-statement spec works |
| 18 Sept | Full fresh run off `main` |
| 19 Sept | **Buffer. Nothing scheduled.** Re-run day if the 18th breaks |

Never let the run slip to the 19th — a failure there loses the credit entirely.

**Improvements still to make before that run:**
1. **Trajectory logging** — the evaluator's verdicts must be written to disk per stage. Today they
   exist only in the run session's context; the repo holds outcomes (`Apply rework to X`) and no
   record of *what was wrong*. This is the single highest-value change: without it the learner spends
   $100 and gets another unauditable run.
2. **Task-statement coverage check** — every task statement has ≥1 concept teaching it.
3. **Source-precedence rule** in `domain-researcher.md` — official exam guide > official product docs >
   reputable secondary, guide valid on its own, **plus a terminal rule**: if no source exists at any
   tier, include the concept with an explicit `UNSOURCED` flag and carry it downstream. Missing sources
   must never block. (The learner reasoned this one out: the hatch is safe because the evaluator audits
   the *search*, not the outcome, and the search log is more work to fake than to do.)
4. **Verify the phrasing guess.** `domain-mapper.md` says task statements are the numbered
   *"the candidate can ..."* items. Claude guessed that convention without seeing the CCAR-F guide.
   Check it against the real PDF — a wrong parenthetical costs a round.

**Teaching thread:** finish Module 04 — Concepts 4 and 5 only, re-taught slowly and anchored to
something concrete (see the teaching-error note in the session log). Then a fresh quiz; today's was
abandoned at Q2 and does not count.

## Session log — 2026-09-15 (lunch): the blocked first run

Not a teaching session, but three things worth carrying forward.

**1. The tutor session had no web access, and that blocked the pipeline.** The `Default` cloud
environment ran at **Trusted** network access — an allowlist covering GitHub, npm and PyPI but no
general web. Every outside domain tested came back blocked, so the cert choice was never the
problem. Three of the four agents (`domain-mapper`, `domain-researcher`, `evaluator`) need the
web; only `course-builder` could run, because the learner had deliberately given it no web tools.
The agent restricted for safety was the only one immune to the outage.

**Fixed during the session.** The learner edited the environment to **Full** network access and
renamed it `Web enabled` (`env_01Ps6PQcbUzwzN7xmkQxciRd`) — the rename being the way to tell it
apart from a second, identically-named environment. **The change applied to the already-running
session; no restart was needed.** (Claude had predicted a new session would be required. It was
not. Don't repeat that claim.)

**2. The learner asked for an ELI5 and it was warranted.** The first explanation of the blocker
was too compressed and leaned on a clever line rather than the mechanism. A sealed-room analogy
(four workers, three need to go out and look things up, the door is locked) landed immediately.
Signal to keep: they say plainly when an explanation hasn't worked, rather than nodding along.
Treat that as reliable.

**3. Identity collision showed up for real, and settled where the run happens.** Running the
pipeline in the tutor session would have put two conflicting `CLAUDE.md` identities in one place
("you are the tutor" / "you are the orchestrator"), and the four agent definitions would not have
loaded, since they live in the other repo. Claude would have ended up doing the work the
orchestrator explicitly forbids it to do. Hence the separate session.

**Teaching opportunity not yet used:** this is a live instance of the **context isolation** point
the learner had not reached unprompted on 2026-09-14 (see Weak spots). It was explained here, not
elicited. When the run is discussed next session, come back to it *through what actually
happened* — why the pipeline needed its own session, its own context, its own identity — rather
than asking the concept cold.

**Also worth a cheat-sheet card eventually:** the environment's network policy is part of the
harness in the Module 01 sense — it constrains what the loop can do, independently of any prompt.
That is the same prompt-layer vs. tool-layer split the learner generalised in Module 02, one level
further out. Not yet added to the artifact.
