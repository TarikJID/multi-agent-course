# Module 03 — Key Concepts (Glossary)

<!-- INSTRUCTOR: Short, accurate definitions Claude uses to stay precise.
     The explain-eli5 skill reads from here to simplify without becoming wrong. -->

- **Agentic RAG** — A retrieval-augmented generation system where the model reasons about
  *where* (or whether) to retrieve before retrieving, rather than always running one fixed
  retrieval path regardless of the query.
- **Query router** — A dedicated LLM call that classifies an incoming query and outputs a
  structured decision (an action + reason) naming which retrieval backend to use.
- **Chunking** — Splitting a document into smaller passages before embedding, so retrieval
  returns focused, relevant text instead of whole documents.
- **Vector embedding** — A dense numeric representation of a piece of text's meaning, used to
  find semantically similar content via distance (cosine/L2) rather than exact keyword match.
- **Vector database** — A store (e.g. Qdrant) that holds embeddings and returns the
  nearest-neighbor chunks to a query's embedding.
- **Grounded generation** — Generating an answer using only the retrieved context, with inline
  citations tying each claim back to a specific source chunk.
- **Semantic cache** — A store of past queries/answers, keyed by embedding similarity, that
  returns a cached answer instantly when a new query is close enough to one already seen.
- **Time-sensitivity guard** — A check (keyword/pattern-based) that runs before the cache lookup
  and forces a live answer for time-sensitive queries, overriding the cache entirely.
- **Knowledge Graph** — A structured retrieval backend modeling entities and relationships as
  nodes and edges (e.g. in Neo4j), suited to precise structural/relationship questions.
- **Text-to-Cypher** — An LLM translating a natural-language question into a Cypher query that
  runs directly against a Knowledge Graph, instead of an embedding-similarity search.
- **Hybrid retrieval** — Combining multiple retrieval backends (vector, graph, cache, live
  search) behind one routing decision, choosing the right one per query.
- **LLM-as-judge** — An LLM that independently scores competing answers (e.g. RAG vs. Knowledge
  Graph) against explicit criteria and picks a winner, rather than trusting whichever responded
  first.
