# Module 03 — Quiz

<!-- INSTRUCTOR: The quiz-me skill uses these. Answers are here so Claude can check,
     but the rule is Claude NEVER shows them before the learner attempts. Hint first. -->

## Q1. What makes RAG "agentic" rather than a static, fixed pipeline?
- Type: explain-why
- **Answer:** The LLM reasons about *where* (or whether) to retrieve before retrieving — routing
  between possible backends based on the query — rather than always running the same fixed
  retrieval step no matter what was asked.
- **Hint:** Think back to Module 01's ReAct loop — what is the "Thought" step doing here,
  specifically?

## Q2. A user asks "What's breaking in production right now?" A very similar question was
cached 10 minutes ago. Should this be served from cache?
- Type: application
- **Answer:** No. This is time-sensitive — the time-sensitivity guard should force a live
  answer regardless of cache similarity, since a cached "what's broken" answer can go stale
  within minutes and give a dangerously wrong picture.
- **Hint:** What's the one category of query that bypasses the cache check entirely, no matter
  how close the match is?

## Q3. You need "How many products cost more than $50 and were reviewed by more than 3 people?"
Vector RAG or Knowledge Graph — and why?
- Type: application
- **Answer:** Knowledge Graph (Text-to-Cypher). This is a precise structural/aggregation
  question over counts and relationships, which graph queries answer exactly; vector similarity
  search is built for fuzzy semantic matching, not exact filtering and counting.
- **Hint:** Which retrieval shape is designed for "explanations and fuzzy questions" vs.
  "precise counts and relationships"?

## Q4. Why does grounding an answer in retrieved chunks with inline citations make it more
trustworthy than just asking the model to answer from its training knowledge?
- Type: explain-why
- **Answer:** Citations tie each claim to a specific, checkable source rather than the model's
  possibly outdated or hallucinated internal knowledge — the same "never guess, document only"
  guardrail from Module 01, now enforced structurally instead of only being a prompt request.
- **Hint:** What's the automated, architecture-level version of Module 01's "never guess,
  document only" rule?

## Q5. In a RAG-vs-Knowledge-Graph comparison, what is the LLM-as-judge actually doing, and why
not just trust whichever system responded first?
- Type: recall
- **Answer:** It independently scores both answers against the same question using explicit
  criteria (accuracy, completeness, precision) and picks a winner — evaluating quality
  objectively, since responding first only measures speed, not correctness.
- **Hint:** Speed and correctness are two different axes — which one does "responded first"
  actually tell you about?
