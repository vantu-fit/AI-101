# 11 · Retrieval Architectures and RAG

[Home](../../README.md) · [LLM Roadmap](../README.md)

## Learning objectives

After this module, learners will be able to:

- Analyze evidence flow through indexing, candidate retrieval, reranking, context assembly, generation, and citation.
- Compare lexical, dense, and hybrid retrieval under explicit candidate and context budgets.
- Isolate missing-evidence, selection, context-packing, and generation failures using controlled diagnostics.
- Choose a retrieval intervention from measured errors and evaluate its quality, latency, and cost effects.

## Content checklist

- [ ] Trace evidence flow and provenance across corpus snapshots, chunks, candidate pools, selected context, answers, and citations.
- [ ] Analyze chunk granularity, overlap, document structure, duplicate evidence, and metadata filtering as retrieval design choices.
- [ ] Compare lexical matching and dense representations, including exact identifiers, paraphrases, domain shift, and embedding/index compatibility.
- [ ] Explain hybrid candidate generation and score/rank fusion; distinguish candidate recall from final-context evidence coverage.
- [ ] Explain reranker placement, candidate-pool limits, and compute cost, including why comparisons need fixed candidates and generator settings.
- [ ] Analyze context ordering, truncation, evidence conflicts, and citation attribution under a fixed token budget.
- [ ] Define separate retrieval and generation diagnostics, including oracle-evidence conditions, unanswerable queries, and incomplete relevance labels.
- [ ] Explain controlled retrieval interventions and distinguish evidence-access problems from generator behavior that might justify adaptation.

## References

- [Retrieval-Augmented Generation](https://arxiv.org/abs/2005.11401) — retrieval-conditioned generation.
- [Dense Passage Retrieval](https://arxiv.org/abs/2004.04906) — dense passage representations and retrieval evaluation.
- [Lost in the Middle](https://arxiv.org/abs/2307.03172) — evaluating how evidence position affects long-context use.

---

**Previous:** [10 · Inference Systems and Serving](../10-inference-serving/README.md) · **Next:** [12 · Tool Use and Agent Architectures](../12-tool-use-agents/README.md)
