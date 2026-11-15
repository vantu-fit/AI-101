# 11 · Retrieval Architectures and RAG

[Home](../../README.md) · [LLM Roadmap](../README.md)

**Estimated core time:** 12 hours. Optional technical extensions are outside this budget.

**Prerequisites:** [Context and In-Context Learning](../03-context-and-in-context-learning/README.md), [Model Evaluation](../07-evaluation/README.md). Add [Inference Systems and Serving](../10-inference-serving/README.md) when serving the generator locally.

**Status:** Content scaffold; unchecked items are awaiting authoring or review.

Checkboxes track shared content readiness.

## Learning objectives

After this module, learners will be able to:

- Analyze evidence flow through indexing, candidate retrieval, reranking, context assembly, generation, and citation.
- Compare lexical, dense, and hybrid retrieval under explicit candidate and context budgets.
- Isolate missing-evidence, selection, context-packing, and generation failures using controlled diagnostics.
- Choose a retrieval intervention from measured errors and evaluate its quality, latency, and cost effects.

## Content checklist

- [ ] Diagram evidence flow and provenance across corpus snapshots, chunks, candidate pools, selected context, answers, and citations.
- [ ] Analyze chunk granularity, overlap, document structure, duplicate evidence, and metadata filtering as retrieval design choices.
- [ ] Compare lexical matching and dense representations, including exact identifiers, paraphrases, domain shift, and embedding/index compatibility.
- [ ] Explain hybrid candidate generation and score/rank fusion; distinguish candidate recall from final-context evidence coverage.
- [ ] Explain reranker placement, candidate-pool limits, and compute cost; design comparisons with fixed candidates and generator settings.
- [ ] Analyze context ordering, truncation, evidence conflicts, and citation attribution under a fixed token budget.
- [ ] Define separate retrieval and generation diagnostics, including oracle-evidence conditions, unanswerable queries, and incomplete relevance labels.
- [ ] Design controlled interventions and distinguish evidence-access problems from generator behavior that might justify adaptation.

## Proposed lab

Reuse the evaluation protocol to test reranking on Vietnamese AI-document questions with annotated supporting evidence.

**Responsibilities:** The learner specifies evidence labels, diagnostic conditions, and the intervention; the implementation agent builds the pipeline and executes comparisons.

### Experiment specification for an implementation agent

| Element | Specification |
| --- | --- |
| Question | Does reranking a fixed candidate pool improve supported-answer quality under the same final-context budget? |
| Prediction | Gains should concentrate on queries whose evidence is present but poorly ranked; reranking should not repair evidence absent from the pool. |
| Intervention | Compare baseline candidate ordering with reranked ordering; add an oracle-evidence condition on diagnostic cases. |
| Controls | Freeze corpus, chunks, candidate pools, query set, generator, decoding, context budget, scoring rules, and development/test split. |
| Execution | Log candidate membership, ranks, packed context, answers, citations, latency, and costs; choose configuration settings on development data only. |

### Inspectable artifacts

- Corpus/index manifests, stable chunk IDs, query/evidence annotations, and the candidate pool for each query.
- Baseline and reranked lists, packed contexts, generated answers, and resolved citation targets.
- Candidate-recall and final-context evidence measures, answer/citation scores, and oracle-condition results.
- An error decomposition and quality/cost comparison linked to individual queries and source passages.

### Acceptance criteria

- Define relevance labels and metric denominators; report retrieval evidence separately from answer correctness, support, and citation accuracy.
- Test the prediction by separating evidence-present and evidence-absent candidate pools; use oracle evidence to investigate residual generation failures.
- Preserve the intended controls, report context truncation and candidate changes, and evaluate frozen configurations on the held-out test set.
- Explain whether gains came from evidence selection or another changed factor; verify representative source passages and include latency/cost effects.

## Self-check questions

1. Why can high candidate recall coexist with poor evidence-supported answer quality?

   **Hint:** Inspect reranking, context packing, truncation, evidence conflicts, and the generator's use of the selected context.

2. Why can comparing two chunking schemes at the same top-k produce a misleading retrieval comparison?

   **Hint:** The retrieved token budget, evidence fragmentation, duplicates, and relevance-label granularity may all change.

3. What evidence distinguishes a retrieval architecture problem from a generator behavior problem?

   **Hint:** Compare actual and oracle evidence conditions, inspect final context, and separate answer errors from missing information.

## Completion checklist

- [ ] Add examples that expose lexical/dense differences, chunk boundaries, context loss, and citation failures.
- [ ] Execute the specified comparison with versioned corpus, index, models, candidate pools, and raw outputs.
- [ ] Write answer guidance and rubrics for failure isolation, controls, and quality/cost interpretation.
- [ ] Document pitfalls including incomplete labels, duplicate evidence, changing token budgets, leaked answers, and unsupported attribution.
- [ ] Verify primary references and ask another contributor to audit relevance labels and the error decomposition.

## Optional technical deep dive

- Derive dense retrieval objectives and compare learned sparse, dual-encoder, and late-interaction architectures.
- Investigate approximate nearest-neighbor indexes, retrieval training, reranker adaptation, and fusion calibration.
- Extend to multi-hop retrieval, incremental indexing, structured sources, and evidence-sensitive context compression.

## References

- [Retrieval-Augmented Generation](https://arxiv.org/abs/2005.11401) — retrieval-conditioned generation.
- [Dense Passage Retrieval](https://arxiv.org/abs/2004.04906) — dense passage representations and retrieval evaluation.
- [Lost in the Middle](https://arxiv.org/abs/2307.03172) — evaluating how evidence position affects long-context use.

## Completion criteria

Explain the evidence path, isolate the dominant failure stage, and defend a controlled retrieval intervention using query-level evidence.
Deliver the fixed comparison, retrieval/generation diagnostics, and a justified quality/cost decision.

**Previous:** [10 · Inference Systems and Serving](../10-inference-serving/README.md) · **Next:** [12 · Tool Use and Agent Architectures](../12-tool-use-agents/README.md)
