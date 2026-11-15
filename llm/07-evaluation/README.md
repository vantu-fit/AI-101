# 07 · Evaluation and experimental design

[Home](../../README.md) · [LLM roadmap](../README.md)

## Learning objectives

- Translate a capability claim into an evaluation construct, comparison protocol, and falsifiable success criterion.
- Explain paired comparisons and distinguish variability across tasks, training runs, generations, and judges.
- Diagnose contamination, scorer failures, judge biases, and mismatched evaluation conditions.
- Interpret quality–cost tradeoffs, subgroup regressions, and uncertainty before accepting an improvement claim.

## Content checklist

- [ ] Explain construct validity using cases where benchmark score, human preference, factual correctness, and deployment utility measure different things.
- [ ] Define the unit of evaluation, dataset population, source-group structure, and how they constrain generalization claims.
- [ ] Specify paired comparisons with frozen example IDs, prompts/context, extraction rules, model revisions, and generation settings.
- [ ] Separate uncertainty from sampled tasks, training randomness, stochastic decoding, and judge variability; explain which repeated observations address each source.
- [ ] Analyze contamination and adaptive benchmark selection, including semantic overlap and limitations of overlap checks.
- [ ] Audit scorers and normalization using edge cases, per-example inspection, and rescoring of saved outputs.
- [ ] Examine LLM-judge position, verbosity, and self-preference biases; include blinded manual review and order checks where relevant.
- [ ] Explain why subgroup results and regressions must remain visible alongside aggregate metrics and uncertainty summaries.
- [ ] Interpret quality–cost frontiers using actual generation budgets, latency distributions, resource conditions, and failed requests.

## References

- [EleutherAI — Language Model Evaluation Harness](https://github.com/EleutherAI/lm-evaluation-harness): task configuration, model backends, scoring, and reproducible evaluation artifacts.
- [Zheng et al. — Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena](https://arxiv.org/abs/2306.05685): judge behavior, agreement, and evaluation biases.
- [Stanford CS336](https://cs336.stanford.edu/): evaluation within empirical language-model development.

References checked on **2026-11-15**.

---

**Previous:** [06 · Data pipelines and pretraining design](../06-data-pretraining/README.md) · **Next:** [08 · Fine-tuning and parameter-efficient adaptation](../08-sft-peft/README.md)
