# Module 04 — Exercises

<!-- INSTRUCTOR: Hands-on tasks for the build-along skill. Both exercises use the learner's
     "Certification Trainer" side project (github.com/TarikJID/certification-trainer) as the
     concrete system, per progress/learner-progress.md, unless the learner says otherwise.
     Exercise 2 produces a real file in that repo — treat it as actual project work. -->

## Exercise 1 — An eval plan for Certification Trainer

**Goal:** Turn your existing evaluator — which today checks a hand-written "Done when" checklist —
into a measured system, by deciding what you'd actually track and at which layer.

**Steps:**
1. Place Certification Trainer on the five-layer eval pyramid. Which layers does it genuinely have,
   and is there one it can legitimately skip? Justify the skip.
2. For the **domain-researcher** stage, name one *outcome* metric and one *trajectory* metric you'd
   track. For each, say concretely what you'd have to log during a run to compute it at all.
3. Your researchers do live web search rather than retrieving from a fixed corpus. Which of
   Precision@K / Recall@K / MRR still apply, and which become awkward or meaningless? Say why.
4. Pick the single metric you'd instrument **first** if you could only have one, and defend the
   choice against the obvious alternative.

**Done when:** You have a layer assignment with a justified skip, one outcome + one trajectory
metric for the researcher stage (each with the data you'd need to log), a reasoned verdict on the
three retrieval metrics, and one defended first-metric choice.

**Stretch (optional):** Your evaluator currently returns PASS/REWORK — a binary. What would you gain
by having it return a score per checklist item instead, and what new problem would that create?

## Exercise 2 — A guardrail policy, and where it runs

**Goal:** Write a real safety policy for Certification Trainer and decide where in the pipeline it
gets enforced — then commit it to the repo.

**Steps:**
1. List 3–4 things Certification Trainer should never do or emit. Think about what's specific to a
   *study tool* rather than generic harms — e.g. the quiz-answer-leak problem you identified in
   Module 03, or fabricated exam content presented as official.
2. For each, decide whether it's an **input**-side risk (something a user asks for), an
   **output**-side risk (something the system produces), or both.
3. For each, decide where enforcement belongs: the agent's tool scope, its prompt, the evaluator's
   checklist, or a runtime guardrail classifier. Justify each placement — and note which of these
   can actually *block* versus merely *request* or *measure*.
4. Write the result as `GUARDRAILS.md` in the certification-trainer repo, then commit and push it.

**Done when:** `GUARDRAILS.md` exists in the repo with 3–4 policy items, each labelled
input/output/both and assigned to a specific enforcement point with a justification.

**Stretch (optional):** One of your policy items is almost certainly enforceable *only* by prompt
text, with no structural backstop available. Identify which one, and say what you'd monitor to find
out when it fails, given you can't prevent it.
