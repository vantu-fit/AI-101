# 14 · Capstone: Vietnamese QA over AI Documents

[Home](../../README.md) · [LLM Roadmap](../README.md)

## Learning objectives

After this module, learners will be able to:

- Explain an integrated evidence-based QA architecture with explicit retrieval, context, generation, and serving contracts.
- Explain how a fixed benchmark helps isolate failures and select a technically justified intervention.
- Evaluate the intervention's supported-answer quality, citation behavior, latency, and resource/cost tradeoffs.
- Explain how an acceptance decision follows from reproducible system evidence and a clear account of remaining limitations.

## Content checklist

- [ ] Define the target Vietnamese AI-document workload, supported evidence types, abstention behavior, and operating constraints.
- [ ] Map evaluation, serving, and RAG components to a baseline architecture and explain their integration boundaries.
- [ ] Specify source/index versions, component contracts, context budgets, decoding settings, and traceable request/output identifiers.
- [ ] Preserve the development/test split and scoring protocol; group duplicates or paraphrases and keep test results out of intervention selection.
- [ ] Define baseline quality, citation, latency, error, and resource/cost measurements with component-level diagnostics where available.
- [ ] Explain a failure decomposition linking retrieval misses, evidence selection, context loss, unsupported generation, and optional tool errors.
- [ ] Specify one intervention with a mechanism, affected error cohort, predicted tradeoff, fixed controls, and a falsifying outcome.
- [ ] Interpret acceptance comparisons covering overall and cohort results, operational usability, and unresolved confounders.
- [ ] Explain the roles of configuration manifests, raw evidence, comparison reports, and rerun instructions in reproducibility.

## References

- [Retrieval-Augmented Generation](https://arxiv.org/abs/2005.11401) — retrieval-conditioned system design.
- [Official vLLM Documentation](https://docs.vllm.ai/en/latest/) — serving configuration and measurement interfaces.
- [EleutherAI Language Model Evaluation Harness](https://github.com/EleutherAI/lm-evaluation-harness) — reproducible evaluation structure; retain task-specific QA and citation scoring.

---

**Previous:** [13 · Research Frontiers and Claim Assessment](../13-research-frontiers/README.md) · **End of roadmap:** [LLM Overview](../README.md) · [Home](../../README.md)
