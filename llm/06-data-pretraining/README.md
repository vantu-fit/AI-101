# 06 · Data pipelines and pretraining design

[Home](../../README.md) · [LLM roadmap](../README.md)

**Estimated core time:** 12 hours. Optional technical extensions and long training runs are outside this estimate.

**Prerequisites:** [04 · Training dynamics and scaling](../04-training-dynamics-scaling/README.md).

**Status:** Content scaffold; unchecked items still need to be written or reviewed.

Checkboxes track shared content readiness. The focus is on data interventions, training exposure, and the evidence needed to justify a pretraining design choice.

## Learning objectives

- Analyze curation, deduplication, mixture proportions, and sampling as interventions on the training distribution.
- Design a data comparison that accounts for token budgets, repetition, provenance, and contamination.
- Interpret dataset audits and model evaluations as different kinds of evidence.
- Decide which data intervention to test next and state the limits of transferring results across model scales or domains.

## Content checklist

- [ ] Map an operational pipeline from source collection and extraction to filtering, deduplication, mixing, tokenization, and versioned training shards.
- [ ] Analyze quality filters as distribution-changing decisions, including domain/language coverage and useful examples removed by mistake.
- [ ] Compare exact, near-duplicate, and semantic overlap concepts; explain the limits of practical overlap detectors.
- [ ] Explain data mixtures, sampling proportions, repeated exposure, and why equal document counts do not imply equal training conditions.
- [ ] Examine tokenizer choice, document boundaries, packing, context length, and the distinction between available and consumed tokens.
- [ ] Define provenance, usage-rights records, contamination checks, and grouping rules for related sources and evaluation examples.
- [ ] Design matched-budget data ablations, stating which quantities are controlled and which distribution changes are part of the intervention.
- [ ] Interpret domain-specific loss, downstream capability, and regression results without substituting a data-cleanliness metric for model evidence.
- [ ] Use FineWeb and DoReMi as case studies in empirical data design, including the limits of proxy models and extrapolation.

## Proposed lab

### Test one data intervention under an explicit training budget

**Research question:** Does a selected filter, deduplication rule, or mixture adjustment improve the targeted capabilities at a defined training budget, and what does it cost in coverage or retained capability?

**Hypothesis:** Specify the error family or domain expected to benefit, the proposed mechanism, and a possible adverse effect. A reduction in duplicates or higher filter scores is an intermediate observation, not the final model-quality claim.

**Controls:** Use the same model initialization or base checkpoint, tokenizer, optimization recipe, training-token budget, and evaluation suite for a bounded pair of runs where feasible. Record repetition, realized domain exposure, and any controls that cannot be matched.

**Learner analysis:**

- Choose one intervention and inspect its effect on data coverage before committing compute.
- Audit retained and removed examples, near-duplicate matches, and potential overlap with evaluation sources.
- Interpret domain-level and downstream results together, separating direct observations from a hypothesized mechanism.

**Agent execution:**

- Implement the versioned data pipeline and produce audit samples, mixture statistics, overlap reports, and consumed-token records.
- Execute a bounded comparison or assemble attributable matched-run artifacts for review; mark remaining mismatches and never present unexecuted runs as completed.

**Artifacts to verify:**

- A data manifest with provenance, usage rights, processing decisions, versions, and grouping rules.
- Before-and-after coverage, duplication, mixture, and token-exposure reports with representative examples.
- Paired run configurations and evaluation outputs, including domain-specific results and capability regressions.
- A claim ledger distinguishing data-only findings, measured model effects, and untested transfer to other scales or distributions.

**Acceptance criteria:**

- The intervention is reproducible and its intended distribution change is distinguished from uncontrolled changes.
- Contamination checks report detector scope and limitations rather than claiming that a clean scan proves absence of overlap.
- Model-improvement claims are supported by actual runs or clearly attributed artifacts; a data-only audit supports only data-level conclusions.
- The recommendation accounts for lost coverage, repetition, budget differences, and negative or inconclusive results.

**Experiment specification for an implementation agent:**

```text
Implement the specified single data intervention and preserve a versioned control corpus.
Audit provenance, coverage, duplicate groups, evaluation overlap, and token exposure.
Prepare matched training/evaluation configurations and disclose unmatched quantities.
Run within the agreed budget or provide attributable existing artifacts for review.
Return domain-level results, regressions, retained/removed examples, and a claim-to-evidence table.
Keep data-only findings separate from measured model improvements.
```

## Self-check questions

### 1. Why can an apparently stronger quality filter reduce downstream capability?

**Answer guidance:** The filter can remove useful domains, languages, or difficult examples and change mixture proportions or repeated exposure. Inspect the realized distribution and task results rather than assuming its quality score matches the downstream objective.

### 2. Why is fixing training tokens helpful but insufficient for a perfectly controlled data comparison?

**Answer guidance:** Sequence lengths, packing, repetitions, domain exposure, and optimization dynamics may still differ. State which differences are intended parts of the intervention and which remain confounders.

### 3. When does a successful small-model data experiment justify changing a larger-model training mixture?

**Answer guidance:** It provides evidence for a candidate intervention, not guaranteed transfer. Consider scale, token budget, optimization, evaluation coverage, and the cost of a confirmation run before making the larger commitment.

## Optional technical deep dive

- Implement or inspect MinHash-based deduplication, document grouping, and token-packing logic.
- Study data-mixture objectives, proxy-model assumptions, and compute-sensitive experimental designs mathematically.
- Reproduce a limited filtering or mixture ablation with additional seeds or scales when the remaining uncertainty justifies it.

## Completion checklist

- [ ] Include a worked data intervention with a distribution audit and clearly scoped model evidence.
- [ ] Provide bounded run specifications or attributable comparison artifacts with explicit control limitations.
- [ ] Provide rubrics for provenance, contamination checks, budget matching, and claim-to-evidence reasoning.
- [ ] Include harmful filtering, residual overlap, repetition, and proxy-transfer failures to diagnose.
- [ ] Verify primary sources, data rights, versions, and result provenance; label technical extensions separately.

## References

- [FineWeb — technical report by the authors](https://huggingfacefw-blogpost-fineweb-v1.static.hf.space/index.html): empirical filtering and deduplication decisions and their tradeoffs.
- [Xie et al. — DoReMi](https://arxiv.org/abs/2305.10429): data-mixture optimization through a proxy model and subsequent training experiments.
- [Stanford CS336](https://cs336.stanford.edu/): data, scaling, and pretraining systems; implementation assignments are optional extensions.

References checked on **2026-11-15**.

## Completion criteria

- You can specify a data intervention, its intended distribution change, and the controls needed to evaluate it.
- You can audit contamination, provenance, coverage, and consumed-token evidence in a comparison.
- You can recommend a next data experiment while distinguishing observed model effects from assumptions about transfer.

**Previous:** [05 · Decoding, uncertainty and model behavior](../05-decoding-model-behavior/README.md) · **Next:** [07 · Evaluation and experimental design](../07-evaluation/README.md)
