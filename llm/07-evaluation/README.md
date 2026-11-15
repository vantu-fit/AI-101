# 07 · Evaluation and experimental design

[Home](../../README.md) · [LLM roadmap](../README.md)

**Estimated core time:** 14 hours. Optional technical extensions and long experiment runs are outside this estimate.

**Prerequisites:** [04 · Training dynamics and scaling](../04-training-dynamics-scaling/README.md), [05 · Decoding, uncertainty and model behavior](../05-decoding-model-behavior/README.md) and [06 · Data pipelines and pretraining design](../06-data-pretraining/README.md).

**Status:** Content scaffold; unchecked items still need to be written or reviewed.

Checkboxes track shared content readiness. Basic ML evaluation literacy is assumed; this module concentrates on the validity and reproducibility of claims about LLM capabilities and systems.

## Learning objectives

- Translate a capability claim into an evaluation construct, comparison protocol, and falsifiable success criterion.
- Design paired comparisons and distinguish variability across tasks, training runs, generations, and judges.
- Diagnose contamination, scorer failures, judge biases, and mismatched evaluation conditions.
- Interpret quality–cost tradeoffs, subgroup regressions, and uncertainty before accepting an improvement claim.

## Content checklist

- [ ] Explain construct validity using cases where benchmark score, human preference, factual correctness, and deployment utility measure different things.
- [ ] Define the unit of evaluation, dataset population, source-group structure, and how they constrain generalization claims.
- [ ] Specify paired comparisons with frozen example IDs, prompts/context, extraction rules, model revisions, and generation settings.
- [ ] Separate uncertainty from sampled tasks, training randomness, stochastic decoding, and judge variability; plan repeated runs for the relevant source.
- [ ] Analyze contamination and adaptive benchmark selection, including semantic overlap and limitations of overlap checks.
- [ ] Audit scorers and normalization using edge cases, per-example inspection, and rescoring of saved outputs.
- [ ] Examine LLM-judge position, verbosity, and self-preference biases; include blinded manual review and order checks where relevant.
- [ ] Design subgroup and regression analyses that remain visible alongside aggregate metrics and uncertainty summaries.
- [ ] Report quality–cost frontiers using actual generation budgets, latency distributions, resource conditions, and failed requests.

## Proposed lab

### Audit and test an improvement claim

**Research question:** Does an intervention from the decoding or data module improve the claimed capability under a defensible comparison, and does the result survive inspection of costs, regressions, and uncertainty?

**Hypothesis:** State one primary claim, its operational metric, a minimally useful effect chosen for the task, and the outcomes that would weaken or reject the claim. Identify where the metric is only a proxy for the intended capability.

**Controls:** Pair results on the same evaluation items, preserve source-group identities, freeze the scoring protocol before the final comparison, and record differences in compute or model configuration. Repeat the stochastic component relevant to the claim rather than duplicating runs mechanically.

**Learner analysis:**

- Select the construct and experimental unit, justify the baseline, and identify the most plausible confounders.
- Review a diverse sample and cases driving the result, including disagreements between scorers or judges.
- Determine whether the effect is meaningful for the target use and whether subgroup regressions change the conclusion.

**Agent execution:**

- Implement the protocol, save predictions and scoring intermediates, and run the specified repeated comparisons.
- Generate paired effect summaries, uncertainty estimates appropriate to the grouping and randomness, and quality–cost reports.
- Execute judge-order checks or blinded review exports where relevant, retaining failures and disagreements.

**Artifacts to verify:**

- A claim-to-measurement specification, experimental unit definition, frozen protocol, and contamination audit.
- Paired predictions with item/group IDs, raw and normalized answers, scores, run IDs, and review annotations.
- Effect and uncertainty summaries with subgroup regressions, scorer/judge diagnostics, and actual compute costs.
- A conclusion identifying supported claims, invalid comparisons, unresolved confounders, and required follow-up evidence.

**Acceptance criteria:**

- Saved outputs can be rescored, and examples that determine the main conclusion are inspectable.
- Repeated generations are not treated as independent task draws; grouping and repeated-run assumptions are documented.
- Judge preference is not silently relabeled as factual correctness, and benchmark improvements are not generalized beyond their evaluated population.
- The conclusion accounts for paired differences, uncertainty, failure costs, and regressions rather than only aggregate rank.

**Experiment specification for an implementation agent:**

```text
Implement the frozen claim-to-measurement protocol and preserve item/group identifiers.
Compare the baseline and intervention on paired examples with recorded model and generation settings.
Repeat only the stochastic components specified in the design; retain all outputs and failed cases.
Audit extraction/scoring edge cases and relevant judge biases; export samples for blinded review.
Report paired effects, justified uncertainty summaries, subgroup regressions, and actual quality-cost tradeoffs.
Distinguish observations, proxy measures, and claims that the experiment cannot establish.
```

## Self-check questions

### 1. Why can a statistically clear benchmark gain still fail to support the intended capability claim?

**Answer guidance:** The benchmark or scorer may measure a proxy, exploit contamination, omit important subgroups, or differ from the intended use. Precision about an effect does not establish that the measurement captures the desired construct.

### 2. Why do more generations for the same questions not substitute for a broader evaluation set?

**Answer guidance:** They help characterize decoding variability on those questions, but do not add independent task coverage. Keep the task-sampling and generation-sampling sources of uncertainty distinct.

### 3. What must be checked when an LLM judge prefers a new system but human factual review does not?

**Answer guidance:** Check the rubric, position and length effects, task knowledge, and the examples causing disagreement. The two evaluations may measure different constructs or one may be unreliable.

## Optional technical deep dive

- Derive or implement paired bootstrap procedures, clustered resampling, or other uncertainty estimators justified by the design.
- Study calibration, proper scoring rules, multiple comparisons, and adaptive evaluation mathematically.
- Build custom harness integrations or scorer tests for a specific research protocol.

## Completion checklist

- [ ] Include a worked claim audit with construct validity, paired evidence, and a qualified conclusion.
- [ ] Provide runnable evaluation specifications or traceable artifacts with saved outputs and scoring intermediates.
- [ ] Provide rubrics for baseline fairness, uncertainty assumptions, judge/scorer diagnostics, and claim scope.
- [ ] Include contamination, pseudoreplication, judge bias, and hidden-regression cases to diagnose.
- [ ] Verify primary sources, versioned tooling, and all reported evidence; separate implementation extensions.

## References

- [EleutherAI — Language Model Evaluation Harness](https://github.com/EleutherAI/lm-evaluation-harness): task configuration, model backends, scoring, and reproducible evaluation artifacts.
- [Zheng et al. — Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena](https://arxiv.org/abs/2306.05685): judge behavior, agreement, and evaluation biases.
- [Stanford CS336](https://cs336.stanford.edu/): evaluation within empirical language-model development.

References checked on **2026-11-15**.

## Completion criteria

- You can turn a capability claim into a defensible paired experiment with appropriate controls and uncertainty assumptions.
- You can locate a scorer, judge, contamination, or design flaw and specify the correction needed.
- You can judge whether a result supports a practical or research decision, including regressions and quality–cost tradeoffs.

**Previous:** [06 · Data pipelines and pretraining design](../06-data-pretraining/README.md) · **Next:** [08 · Fine-tuning and parameter-efficient adaptation](../08-sft-peft/README.md)
