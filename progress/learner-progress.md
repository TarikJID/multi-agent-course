# Learner Progress

<!-- Claude reads this at the start of each session and updates it at the end.
     Learners: you don't need to touch this — Claude maintains it. -->

## Learner profile
- Name: [unset]
- Preferred learning style: Socratic
- Started: 2026-09-04
- Last session: 2026-09-22
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
| 04 — Evaluation & Guardrails | completed (+ both exercises, 2026-09-21) | All seven concepts taught. MRR, Answer Relevance and Context Utilisation were delivered plainly on 2026-09-20 after the learner asked for them before the quiz. **Fresh quiz (not the abandoned one, and not reusing quiz.md Q1–Q5): 5/5**, with one hint on Q2 and one retry on Q5(b). Standout: on faithfulness-vs-relevance the learner went past the lesson unprompted — a misnamed metric routes to the wrong remediation (re-source vs re-scope), and under a retry cap of 2 that wastes a round on a problem you do not have. Also declined to call Precision@8 = 0.75 a failure because no threshold had been defined — the same "no standard to fail against" instinct logged on 2026-09-16, now deliberate. Residual: metric *names* are not yet automatic (reached for trajectory when the answer was precision; needed a second pass on input-side vs output-side guarding). Concepts are solid; vocabulary needs reps. |
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
- **Status: RUNNING AND VERIFIED.** A complete course was built 18 Sept for $28.09 with
  240/240 bullet coverage and 11 verdict files, on branch `claude/confident-davinci-5nplxt`.
  Earlier note kept for history: All four agent definitions written this session,
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
- **Milestone ACHIEVED 2026-09-18.** After that, a separate **tutor agent** (decided this session to keep teaching separate
  from building — the tutor is a separate entry point, not a 7th pipeline step).
- **Claude: keep using this project as the concrete example for module exercises.** The first
  real run is long done; the live milestone now is the tutor's first real teaching session.
- **The tutor exists as of 2026-09-22.** `tutor-template/` in the pipeline repo — `CLAUDE.md`,
  five skills (`teach-module`, `quiz-me`, **`drill`**, `explain-eli5`, `build-along`), `/start`
  and `/progress`, and a progress-file format tracking `recall` and `application` separately.
  `drill` is new, not copied from the bootcamp: fast cold checks on `recall: shaky` items only,
  and forbidden from touching anything closed.
- **Three repos now:** `multi-agent-course` (the bootcamp), `certification-trainer` (the
  pipeline), `claude-certified-architect-foundations` (public — the course it produced, with its
  audit trail and now the tutor).
- **Project purpose (decided 2026-09-17): Certification Trainer is a GENERIC tool.** It must
  work on any certification. Learning agent engineering is why it is being built this way;
  the CCAR-F course is a by-product, not the objective. Nothing certification-specific goes
  in the pipeline's definitions. Treat this as settled unless the learner reopens it.

## Next step

**Certification Trainer's milestone is DONE.** A complete, coverage-verified course was
built on 18 Sept for $28.09, on branch `claude/confident-davinci-5nplxt` of
`TarikJID/certification-trainer`. The pipeline on `main` is the version that produced it —
no overrides, no hybrid state. Stop treating "get a first real run working" as the open
thread; it closed.

**Open, small, and the learner's to do:** read one lesson
(`courses/claude-certified-architect-foundations/Module_1_.../lesson.md`) and judge whether
it *teaches* rather than recites. Coverage and citation faithfulness are verified; pedagogy
is not, and counts cannot settle it.

**Module 04 is fully complete** — all seven concepts, quiz 5/5 (2026-09-20), and both
exercises done 2026-09-21. `AI_Eval_Metrics.ipynb` remains untouched; it is optional now that the
metrics have been exercised against real run data, but its real numbers would still be good
repetition if the vocabulary slips again.

**The live thread: the learner is starting a course with the tutor.** They ended 2026-09-22
saying "I'll try starting a course" — meaning a session rooted at
`TarikJID/claude-certified-architect-foundations`, opening
`courses/claude-certified-architect-foundations/` and running `/start`.

**Ask how that went at the start of the next session.** What to ask for, specifically:
- Did `/start` work — did it read `course-outline.md` and set up a profile?
- Did the progress file's **concept tracker** actually get written, or did the tutor revert to
  prose notes? That is the format's first contact with a real session.
- Did `drill` fire? (It only fires once something is `recall: shaky`, so probably not on session 1.)
- Did it ever hand over a quiz answer without logging the attempt first?

The structure is tested; the behaviour is not. That run is the test.

**Next module: 05 — Multi-Agent Systems (MCP · A2A · ADK).** The learner already has hands-on
MCP exposure through Certification Trainer, so this should connect to something real rather than
start cold.

**And now there is finally a concrete anchor for them.** Two runs of the same certification
exist, with eleven verdict files between them:
- *Precision@K* over the researcher's sources: of the pages it cited, how many were
  relevant? The evaluator's faithfulness findings are exactly this failure.
- *Faithfulness* is no longer abstract: three reworks in run 2 were citation-faithfulness
  failures, each one written up in a verdict file the learner can open and read.
- *Recall* is the 240-bullet coverage check they already understand.

Teach them against those files, not against a definition list. That was the whole diagnosis
on the 16th and the material now exists.

**Then Module 05 (MCP · A2A · ADK) and Module 06 (Voice Agents)** remain untaught.

**Possible side-project thread, if the learner wants it:** the real test of Certification
Trainer as a *generic* tool is a second certification — a different one, with no answer key
in `reference/` and an unknown guide format. Not urgent, no credit for it now, but that is
the run that would prove goal 1 rather than assume it.

## Session logs

Newest first.

## Session log — 2026-09-22: the tutor, built and tested

No module taught. Product work, plus one piece of course archaeology.

**1. Why our module list differs from the upstream course — answered from the git history.**
The learner asked. Upstream commit `0334cd5`, 4 Sept 2026: *"Cohort 2026-03: rename modules to the
new 7-week outline. Previous cohort preserved on branch `2026-02`."* The rename list in that commit
is literally our module names, so **ours are the originals** — this repo's first commit is 25 June
and it froze the pre-rename structure. Two consequences worth remembering:
- **Evaluation was demoted, not promoted.** `Module_4_AI_Evaluation` *was* a module; upstream folded
  it into `Module_3_.../Evaluation_and_Guardrails`. We then treated it as a full module and authored
  five teaching files, so ours is now the more developed version of that content.
- **We are missing upstream's new Modules 6 and 7** — *Leading AI Systems Across Teams* and
  *Demo Day* — plus a reorganised root. Upstream is still active (last commit 21 Sept). Offered to
  look at the two new modules after 05 and 06; the learner has not taken that up.

**2. Three repos now, each with a README.**
- `certification-trainer` — README written, then revised twice on the learner's instructions: first
  made generic (the run-history table and cost figures "don't really make sense for anyone except
  you and me" — correct), then `Design notes` and `Guardrails` cut and the repo layout fixed. It had
  listed `runs/` and `courses/` as repo contents; neither exists on `main`.
- **`claude-certified-architect-foundations` — new public repo**, created this session. The run-2
  course plus its `runs/` audit trail. Directory paths preserved exactly as generated so the path
  citations inside the verdict files still resolve — flattening would have silently broken the audit
  trail the repo exists to preserve.
- `multi-agent-course` — unchanged.

**3. `GUARDRAILS.md` was stale, and the learner caught it** by asking whether the agent definitions
had actually been updated. They had. But the file still said policy 4 was `not built` and still
listed the `Fetched:` requirement as an open gap — both had shipped in the same PR. **A policy file
that misreports its own status is worse than none.** Fixed, and the "what is missing" table replaced
with **"Where each policy actually lives"**, mapping every policy to the file and line enforcing it.
Nothing in the repo reads `GUARDRAILS.md` — agents obey checklists — so that link had to be written
down or it existed nowhere.

**4. The tutor: designed, built, tested.** All three open decisions settled:
- **Who emits it — nobody.** A static `tutor-template/` copied in by the orchestrator at step 12.
  Nothing in it varies by certification, and the module list is not duplicated: the tutor reads
  `course-outline.md`. Zero generation, nothing to go stale.
- **The comprehension log — two axes, closed independently.** `recall` (can name it cold) and
  `application` (can use it correctly). The learner insisted vocabulary matters too, which is the
  right call *for them specifically*: their profile is strong reasoning, weak exact names, so
  collapsing the axes would let the strong one mask the weak one. Conditions are recorded
  (`just-taught` / `cued` / `cold`), and only **cold** closes recall — two clean cold recalls on
  **separate days**, which is the rule this very progress file used.
- **Answer keys — gated on a logged attempt**, with answers in their own file so they are not in
  context during the question.

**5. The verb argument, and the learner was half right.** Asked to apply the GUARDRAILS test to
their own attempt-gating design, they said **measure**. Precisely: at the moment of answering it is
the same model consulting its own log, which is a **request**; the record it leaves makes a leak
detectable afterwards, which *would* be a measure — **but only once something reads the log looking
for one, and nothing does.** Writing "measures" today would be the exact thing the file exists to
prevent. Good instinct, and the correction is a concrete to-do rather than a quibble.

**6. Testing the template found a real defect immediately.** Copied into the CCAR-F course and
structure-checked: `quiz-answers.md found in 0 module folders (expect 10)`. `course-builder` had
been emitting answers **inline in `quiz.md`**, inside `<details>` blocks, under a note reading *"the
tutor must never reveal an answer before the learner attempts."* Two failures in one:
- That note is a **prompt instruction sitting in a data file** — already failed by the time anything
  reads it.
- `<details>` collapses **in a browser**, not in a model's context. A tutor opening `quiz.md` to ask
  Q1 holds every answer for that module.

The whole guardrail rested on a file split the pipeline never produced. Fixed in both places: 128
answers split out mechanically across 10 modules (questions untouched, zero leakage on re-grep), and
`course-builder`'s spec **and checklist** updated — the checklist because a rule in prose is one the
evaluator never sees, which is the learner's own insight from Module 02.

**Teaching note.** The pattern from 2026-09-21 held all session: short answers, and clarification
requested whenever a word was overloaded. Two of my claims were corrected by the learner asking a
precise question rather than by review — the stale `GUARDRAILS.md` and the verb. **Their questions
are a better defect-finder than my checking.** Keep answering them literally and at length only when
asked.

## Session log — 2026-09-21: both Module 04 exercises, and a real defect found

**Exercise 1 — an eval plan for Certification Trainer.** All four steps plus the reasoning
behind them:
- **Layers.** All five present, but only 3/4/5 are *actionable*. The test that settled it: if
  this layer scored badly, what would I change? Layer 1 fails → nothing in the repo moves that
  number, the only lever is a different model. Layers 1–2 are bought from Anthropic, not built.
- **Researcher stage.** Outcome = hallucination rate (measurable today from archived sources).
  Trajectory = Observation Utilization, which needs a `Fetched:` log that does not exist.
- **Retrieval metrics.** Precision applies, given a definition of "relevant" — and the learner
  noted unprompted that if "relevant" collapses to "got cited", precision and Observation
  Utilization become the same number. Recall is impossible: the web is not enumerable. MRR is
  computable but predicts nothing without a cutoff.
- **First to instrument: hallucination rate**, on severity. *"Hallucinations threaten the course's
  correctness, unused pages just cost tokens."*

**Two corrections of mine, both forced by a precise question from the learner.**
1. *"Reading a `.md` another agent produced isn't covered by RAG?"* — my stated reason
   ("`course-builder` has no web tools") was wrong. The web is not what makes something layer 3.
   **The real rule: layer 3 exists wherever there is a selection step that can select wrongly.**
   `course-builder` is handed N files and uses all N — no query, no candidate pool, no ranking,
   so there is no K for Precision@K to range over.
2. *"What is the full list exactly?"* — I had said the researcher sees titles **and snippets**.
   It sees titles and URLs only. Verified by running a real `WebSearch` rather than describing it.

**That second check surfaced a live defect in the pipeline.** `WebSearch` returns a synthesised
summary alongside the result list. A researcher can write a concept from that summary and cite a
URL it never opened — output indistinguishable from properly sourced work, and the same shape as
run 2's three citation-faithfulness reworks. Confirmed nothing records it:
`grep -c "Searched:" research/*.md` returns 0 across all five files.

**Exercise 2 — GUARDRAILS.md, shipped as a PR.** Four policies, each labelled input/output/both,
assigned to one of four mechanisms (tool scope / runtime guardrail / evaluator checklist /
prompt), and marked block / request / measure. Learner chose to scope it to the whole product
rather than the pipeline alone. Notable:
- Two of the four policies they proposed were **tutor** behaviours, not pipeline ones — which
  forced the scope decision explicitly rather than by accident.
- Policy 4 (never quiz on untaught material) has a build-time home: `course-builder` writes the
  quizzes, so the defect is created before the tutor ever sees it. Verified its checklist has no
  such item today.
- Policy 3 (never abandon a concept that hasn't landed) has **no structural backstop at all** —
  no capability to withhold, no classifier with enough history, nothing decidable from the files.
  That is the stretch answer and it is stated plainly in the file rather than papered over.
- The PR also installs the two cheap ones: a quiz-coverage checklist item on `course-builder`,
  and a `Fetched:` requirement on `domain-researcher`.

**Identity collision, avoided in real time and worth reusing as a teaching moment.** The
`add_repo` clone instructions told me to call `register_repo_root` so certification-trainer's
`CLAUDE.md` would load into this session. That file is the **orchestrator**; this session is the
**tutor**. Registering it would have put both identities in one context — precisely what sent the
pipeline run to its own session on 15 Sept. Skipped deliberately, and explained to the learner at
the time. **The tooling's default advice was the wrong call here**, which is a better instance of
the lesson than any hypothetical.

**Process notes.**
- The learner twice asked for **less text** ("that's way too much text", "no no"). Both times they
  were right; the fix that worked was answering the literal question in four lines and stopping.
  Long structured answers are welcome when they *asked* for a recap; they are not welcome as the
  default reply to a narrow question.
- Several clarification requests came from **overloaded words** — "placement", "each of the four"
  (four policies vs. four mechanisms), "input/output" reused across two different steps. Name
  things distinctly the first time rather than relying on context to disambiguate.
- The learner **does not know git** and has never merged anything. Hence the PR route, chosen so
  the merge is two clicks and the diff is visible. Do not assume git fluency in future sessions.

**Blueprint:** restructured at the learner's request — cards stacking three or four levels of
information were split one-idea-per-card ("Outcome vs. trajectory" → two cards; "guardrail vs.
evaluation" → two cards; the six-metric list trimmed to a name list). Four new cards and three
field notes from today. Now at v19.

## Session log — 2026-09-20: a stale file, and a teaching method that backfired

**1. The session opened on a stale progress file, and the learner had to correct it.** The
checkout was four commits behind `origin/claude/sharp-sagan-gtayfl` — the logs for 2026-09-16,
-17 and -18 existed on the remote and had never been pulled. Claude greeted the learner asking
how the *first* run went, when two runs had happened and Module 04 was already underway. The
learner's reply: "we've been through this already, run 2 went well, we reviewed it together, and
we started module 4." **Fix applied: `git fetch` + fast-forward before reading the file. Do this
at the start of every session** — the file is only the source of truth if it is the current file.
This is the second time a lost or unseen session state has cost the learner time.

**2. Concepts 4 and 5 were re-taught, and the first two-thirds of the attempt failed.** Claude
ran a chain of Socratic questions where the answer to the final one had already been stated in
the setup. The learner: "I don't understand your question", then "I don't understand your
questions and your answers. I give up: give me the answer and try to explain it simply without
mysterious sentences." **They were right.** What worked immediately afterwards was dropping the
questioning entirely and stating the mechanism:

> The researcher does two jobs. Job 1: go find pages. Job 2: read them and write the concepts.
> Concept 4 measures Job 1 (Precision@K, Recall@K, MRR). Concept 5 measures Job 2
> (Faithfulness, Answer Relevance, Context Utilisation).
> **Concept 4 = did it find the right pages? Concept 5 = did it tell the truth about them?**

**Method note, and it generalises beyond this module.** Socratic is the recorded preference, but
it fails on material the learner has never been taught. Questions are for *retrieving* and
*extending* something known; they cannot deliver a definition. Concepts 4 and 5 were new
vocabulary for a system with no vector store — the same diagnosis as 2026-09-16, and Claude
repeated the mistake in a different costume. **For genuinely new abstract material: explain
plainly first, then check. Save the questions for after the ground is solid.** Also: never ask a
question whose answer appears in the preceding paragraph — it reads as a trick and destroys trust
in the question.

**3. What the learner got right, unprompted.** Given "the researcher missed a good official page
and used a weaker one instead — what would the evaluator need to catch that?", they worked to the
answer under their own steam: examining the sources that *were* cited can never reveal one that
was never opened, so the evaluator needs "a list of all sources that were supposed to be used" to
compare against. That is ground truth, re-derived at the retrieval layer — the same concept they
derived unprompted on 2026-09-16. The reasoning is solid; it is the vocabulary that is not.

**4. Two errors worth re-checking later (not now).**
- Mapped recall onto "failure to use the source correctly". Both precision and recall are
  *retrieval* metrics — two ways of being wrong about which documents you pulled. Misuse is
  faithfulness.
- Called the coverage check's "zero invented" direction faithfulness. It is set membership — an
  ID either is in the exam guide or it is not, and `comm` can decide it. Faithfulness needs
  someone to read two texts and judge whether one supports the other.

**5. The quiz ran, fresh, and scored 5/5** — see the module table. Worth keeping: the learner
asked to cover MRR / Answer Relevance / Context Utilisation *before* being quizzed rather than
after, which was the right call and their own. The three were delivered plainly, no questions,
and all three held up under test minutes later. **Plain-explanation-then-check is now evidenced,
not just asserted.**

**6. The anchor material is now local and it is good.** `TarikJID/certification-trainer` branch
`claude/confident-davinci-5nplxt` is cloned at `/home/user/tarikjid/certification-trainer`; all
11 verdict files are in `runs/claude-certified-architect-foundations/evaluations/`. The
tool-design round-1 verdict is the best single teaching object in the repo: the researcher
invented a quote *and* a "40% decrease in task completion time" statistic, attributed both to a
real, official, on-topic Anthropic page; the evaluator fetched that page twice, full-text
searched for "40%", "task completion time", "tool-testing agent" and the quote, found none of it,
and returned REWORK. Round 2 shows the corrected text quoting the page verbatim. Same concept,
same URL, honest version and dishonest version side by side. **Use round-1 vs round-2 of that
file for any future faithfulness teaching.**

## Session log — 2026-09-18: the pipeline works, and it is provable

**Certification Trainer produced a complete, verifiable course for $28.09.** Run 1 cost
$53.68 and its quality claims could not be checked at all. The difference is the work of
the 17th and 18th.

| | Run 1 (15 Sept) | Run 2 (18 Sept) |
|---|---|---|
| Cost | $53.68 | **$28.09** |
| Concepts | 115 | **186** |
| Course | 6 modules, ~3,880 lines | **10 modules, 5,512 lines** |
| Coverage | unverifiable | **240/240 bullet IDs, exact set match** |
| Verdict files | 0 | **11** |
| Rework cause | source-tier labels | **citation faithfulness** |

**The coverage claim was verified, not trusted:** every one of the 240 bullet IDs in
`domain-map.md` appears in `course-outline.md`, with zero missing and zero invented. That
is the direct answer to the question the learner could not answer on the 16th.

**The strongest single result is what the reworks were about.** All three researcher
reworks in run 2 were **citation-faithfulness failures** — a prerequisite mis-attributed,
a concept whose cited source did not support it, two attributions "not faithful to the
source they cite". That is Module 03's *silent blending* being caught mechanically, three
times, by a machine. In the previous run the rework was "you labelled the source tier
wrong". **The learner's challenge to the tier design is what moved the evaluator's
attention from bookkeeping to substance** — of everything changed across two days, that
fix has the clearest evidence behind it.

**Four challenges from the learner, all correct, all acted on:**
1. **"Isn't the integrity check overkill?"** (17th) — it was. Built, then cut. Git history
   already records tampering after the fact at no runtime cost, and the check put the most
   complex procedure in the file into the one component whose rules nothing enforces.
2. **"Why is Claude product documentation tier 2?"** (18th) — the four-tier precedence put
   the exam guide above the vendor's own docs, so "prefer the highest tier" told researchers
   to prefer a syllabus line over the documentation that defines the thing. Collapsed to
   official / non-official, unranked.
3. **"Why staged?"** (18th) — the three-stage plan was calibrated to price uncertainty that
   no longer existed. Collapsed to one session with a single pause, kept only because
   `domain-mapper`'s output format had changed and five researchers would inherit any
   breakage. The pause then did exactly that job: 240 IDs, all lists numbered 1..n, no gaps.
4. **"The orchestrator talks about 'my' work — is it doing the work?"** (18th) — it was not.
   Every quoted line mapped to an explicit orchestrator duty, three of them added that same
   afternoon. **The test that settles it: counting is not producing.** The line is
   authorship, not activity. Verified from the diff that the rework changed only summary
   counts — not one bullet, not one ID.

**Four defects the two-domain run exposed, fixed and pushed** (`c67575e`): source tiers
collapsed; bullet IDs moved from the orchestrator's dispatch prompts into `domain-mapper`'s
own output, where they cannot vanish with a session; dispatch slices moved from the
scratchpad into the repo so verdicts cite inputs that survive; researcher self-reported
counts now checked against the file.

**Decision worth keeping: restart clean rather than finish the hybrid.** Session A had two
domains under the old spec; finishing would have produced a course and no clean answer to
"does the pipeline on `main` produce this?". The $10.21 already spent was tuition, not
waste. Goal 1 made the call obvious.

**Budget note:** the run crossed into overage mid-flight (`isUsingOverage: true`, 5-hour
window `rejected`) and completed straight through it, because the prompt told the
orchestrator that rate-limit warnings are the credit handover working as designed, not a
reason to stop. Without that line it would probably have halted itself.

**Not verified, and the learner is doing it:** coverage is not quality. Every bullet has a
lesson and the citations survived scrutiny, but whether the course *teaches well* needs a
human reading a lesson.

## Session log — 2026-09-17: build day, and a decision about what this project is

**The project's purpose was settled, and it reframes everything.** The learner asked
directly: is Certification Trainer meant to be a generic tool, or a good run on this one
certification? Named three goals rather than two — (1) a generic product, (2) the CCAR-F
course itself, (3) learning agent engineering. **Chosen: goal 1 primary, goal 3 as the
reason, goal 2 as a by-product.** The deciding argument: if only the course mattered, the
pipeline is a ~30x more expensive route than handing the guide's 240 bullets to one Claude
session. The pipeline is only worth running if the pipeline is the point. Consequence
adopted immediately: nothing certification-specific lives in the pipeline's own
definitions, and the real test of genericity is a *second* certification with no answer
key — not now, but that is the run that would prove it.

**Four changes shipped to `TarikJID/certification-trainer` `main`:**
- `7d0a9b5` Trajectory logging. `evaluator` has `Write`, records a verdict file per stage
  per round at `runs/<cert>/evaluations/<agent>-<unit>-round-<n>.md`, listing every
  checklist item with an evidence column — passes included, since a file recording only
  failures is no evidence the rest was examined. Unverifiable items go in a `Not checked`
  section, never counted as passes. Returns only verdict + path + one line.
- `43f53c5` The live integrity check, built and then cut (see below).
- `7c031fb` + `275efec` Coverage. The exam guide's task statements — and the bullets
  beneath them — are now the coverage target, flowing mapper → researcher → builder, with
  a bullet-to-lesson table required in the outline. Source precedence added, with the exam
  guide itself as tier 1, plus the terminal rule: no source at any tier means the concept
  is still taught, flagged `UNSOURCED`, with a `Searched:` record. Missing sources never
  block and never cause an omission.
- `710fa61` Certification-agnostic hygiene.

**The exam guide was extracted directly this session** (pure-python zlib + ToUnicode CMap
decoding, since no pdf library was installable). Findings: **30 task statements, 240
`Knowledge of:`/`Skills in:` bullets**, weights 27/18/20/20/15. Two corrections came out of
it: Claude had guessed task statements read "the candidate can ..." — CCAR-F actually uses
`Task Statement N.M:` plus an imperative phrase — and the bullets, not the statement lines,
are the real coverage target. Stored at `reference/ccar-f-exam-guide.md`, deliberately
outside `runs/`, as a **test fixture** for grading runs. The mapper is told never to read
from `reference/`, and the file lists its own extraction fingerprints so a mapper that
copies it can be caught. The first run's mapper got the weightings exactly right.

**A control was built, then removed on the learner's call.** An integrity check —
`git status` after each evaluation to catch the evaluator editing the work it judges. The
learner asked whether it was overkill and what it might break. It was: it guarded a failure
that has never occurred, cost a plausible false halt on an expensive run, and put the most
complex procedure in the file into the orchestrator, the one component whose rules nothing
enforces. Committing between stages already records everything, so `git log -p runs/`
detects the same thing afterwards at no runtime cost. Removed. **Keep this as the reference
case for "cut it" being the right engineering call** — the learner was right to push, and
asked for a recommendation with a confidence level, which is a good habit to keep feeding.

**Three catches by the learner, all the same species: what happens when two things run at
once.** (1) The verdict filename did not identify which agent or which domain — fixed to
`<agent>-<unit>-round-<n>`. (2) The first integrity check would have fired on innocent work,
because a researcher writing its own file and a rogue evaluator edit look identical in a
diff. (3) The fix for that was still wrong: researchers run *in parallel*, so "the evaluator
is the only thing running" is false during the fan-out. Claude had over-claimed twice on the
same point and had to drop the identification framing entirely — the check never identified
anyone, it only ever detected that something changed which nobody was assigned to change.

**Teaching note.** One "I don't understand the fix" and one "I don't understand" in
sequence, on the integrity check. The hotel-corridor analogy failed, and the learner killed
it with the right question ("what tells me it's not cleaner B?"). What worked was dropping
the analogy, admitting the over-claim, and stating the mechanism plainly in four lines.
**Pattern worth keeping: when an analogy is challenged on its internals, the analogy is
usually wrong, not the learner.**

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
