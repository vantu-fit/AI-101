# 04 · Training dynamics and scaling

[Home](../../README.md) · [LLM roadmap](../README.md)

**Estimated core time:** 12 hours; a separately bounded compute budget governs experiment runtime.

**Prerequisites:** [01 · Language modeling and representations](../01-language-modeling-representations/README.md), [02 · Transformer architecture](../02-transformer-architecture/README.md), and strong familiarity with ML optimization, validation, and statistical comparisons.

**Status:** Content outline; unchecked items track shared authoring and review work.

## Learning objectives

- Explain the coupled roles of parameter count, training tokens, data quality, and compute in language-model training.
- Interpret learning curves against token and compute budgets rather than treating steps or wall time as interchangeable units.
- Distinguish empirical scaling relationships, fitted optima, and extrapolations beyond the observed regime.
- Analyze why validation loss and downstream task performance need not rank checkpoints identically.
- Separate a training-compute optimum from a deployment decision that also includes inference cost and constraints.

## Content checklist

- [ ] Define parameter count, processed versus unique tokens, sequence length, training FLOPs, and wall time as distinct accounting quantities.
- [ ] Explain compute/data/model allocation and why a fixed-compute comparison trades model size against training duration or tokens.
- [ ] Compare the assumptions and empirical procedures of early scaling-law and compute-optimal training studies.
- [ ] Analyze LLM learning curves through warm-up/decay schedules, effective batch, precision, data-mixture shifts, and instability.
- [ ] Distinguish data exhaustion, repeated exposure, optimization limits, and architectural capacity as possible causes of flattening loss.
- [ ] Explain iso-compute comparisons, bounded per-size tuning, fit uncertainty, and the dangers of extrapolating a small sweep.
- [ ] Connect aggregate validation loss to domain-specific loss and task behavior without assuming a universal conversion to capability.
- [ ] Distinguish training-optimal allocation from objectives that include serving cost, latency, or many future inference requests.
- [ ] Build an allocation experiment that reports both scaling evidence and the limits of the measured regime.

## Proposed lab

**Experimental question:** Within a small decoder family, does the preferred parameter/token allocation change with the training-compute budget, and do loss and task performance select the same allocation?

**Hypothesis:** At fixed compute, larger models need not win because they receive fewer training tokens. The preferred allocation may move across budgets, and the ordering by validation loss may differ from that of a prespecified task metric.

Run three model sizes at two compute budgets using one tokenizer and corpus, with repeat seeds where the budget permits. Choose feasible scales through a runtime preflight. Use a declared FLOP accounting method to set token allocations and report realized compute, processed/unique tokens, and wall time separately.

**Controls:** Architecture family, corpus/sampling policy, tokenizer, validation/task sets, precision, and a frozen bounded tuning policy for each size. Track learning-rate schedules and tuning cost; a clearly under-optimized or unstable run does not establish a scaling optimum.

**Learner role:** Define the allocation question, expected tradeoffs, and interpretation of the fitted region. **Agent role:** Execute the sweep, retain checkpoints/curves, account for resources, and compare loss with the selected task measure.

**Artifacts:** A size × budget run matrix; data/token/compute accounting; per-run learning curves; validation and task scores; tuning records; a local allocation recommendation with uncertainty and deployment implications.

**Acceptance criteria:**

- Equal-compute claims use the same declared accounting convention and disclose deviations; equal steps or wall time alone are insufficient.
- Repeated data and changes to schedules or tuning effort are visible in the comparison.
- The analysis distinguishes the best measured configuration from a well-supported fitted optimum and from an extrapolated prediction.
- Flat, negative, or inconsistent task results are retained; a tiny sweep is not presented as a universal scaling law.

**Experiment specification for an implementation agent:**

```text
Run the agreed three-size, two-budget decoder sweep within the fixed resource ceiling.
Use one tokenizer/corpus and the frozen per-size tuning policy; account for tuning separately.
Set token allocations with the declared FLOP method and record realized compute, unique/processed tokens, and wall time.
Save checkpoints, schedule metadata, validation curves, and the prespecified task scores; repeat seeds as budgeted.
Report the best measured allocations and uncertainty without extrapolating a universal law from this sweep.
```

This is an experiment specification; no execution results are claimed here.

## Self-check questions

1. Why does a fixed-training-compute comparison usually couple model size to the number of processed tokens?
2. What alternative explanations should be examined before interpreting a flattening validation curve as a model-capacity limit?
3. Why might the allocation preferred for one training run differ from the choice for a heavily used deployed service?

**Answer guidance:**

- Question 1: Per-token training cost depends on the architecture and parameter scale, so holding the compute budget constrains how much data each model can process.
- Question 2: Inspect optimization and schedule choices, data quality/coverage or repetition, precision instability, and the evaluation distribution before assigning the limit to capacity.
- Question 3: Deployment adds inference cost, latency, memory, and expected request volume to the objective; a training-loss optimum does not automatically optimize those terms.

## Completion checklist

- [ ] The module connects training dynamics to parameter, token, data, and compute allocation.
- [ ] The lab provides reproducible accounting, bounded tuning, uncertainty records, and a declared experimental regime.
- [ ] Answer criteria distinguish measured optima, fitted relationships, extrapolation, and deployment objectives.
- [ ] Failure cases cover unstable runs, hidden data repetition, unequal tuning, FLOP/wall-time confusion, and loss/task ranking mismatches.
- [ ] Primary studies and all numerical or causal claims have been independently reviewed.

## References

- [Kaplan et al. — Scaling Laws for Neural Language Models](https://arxiv.org/abs/2001.08361): empirical relationships among loss, model size, data, and training compute in the studied regime.
- [Hoffmann et al. — Training Compute-Optimal Large Language Models](https://arxiv.org/abs/2203.15556): parameter/token allocation under a fixed training-compute budget.
- [Meta — The Llama 3 Herd of Models](https://arxiv.org/abs/2407.21783): a concrete large-scale training and deployment-oriented model-family case study.

Sources checked on 2026-11-15. Treat fitted laws and recommended allocations as conditional on the study's data, architecture, optimization, and objective.

## Completion criteria

- Explain the allocation tradeoff and the accounting behind the controlled sweep.
- Diagnose plausible optimization or data explanations for a learning-curve pattern.
- Interpret loss/task agreement or disagreement and defend a bounded allocation recommendation.
- State what additional evidence would be needed to extrapolate to a larger scale or a deployment objective.

Personal completion is separate from the shared authoring checklist.

## Optional technical deep dive

Derive training-FLOP approximations, fit scaling surfaces with uncertainty, analyze optimizer dynamics, or implement distributed training and profiling. Mathematical derivations, tensor-level debugging, and manual training infrastructure are optional extensions beyond the core interpretation requirements.

---

[← Previous: 03 · Context dynamics and in-context learning](../03-context-and-in-context-learning/README.md) · [Next: Module 05 →](../05-decoding-model-behavior/README.md)
