# 08 · Fine-tuning and parameter-efficient adaptation

[Home](../../README.md) · [LLM roadmap](../README.md)

**Estimated core time:** 12 hours. Optional technical extensions and long training runs are outside this estimate.

**Prerequisites:** [04 · Training dynamics and scaling](../04-training-dynamics-scaling/README.md), [06 · Data pipelines and pretraining design](../06-data-pretraining/README.md), and [07 · Evaluation and experimental design](../07-evaluation/README.md).

**Status:** Content scaffold; unchecked items still need to be written or reviewed.

Checkboxes track shared content readiness. This module examines adaptation mechanisms, objective specification, and the empirical tradeoffs of full fine-tuning and parameter-efficient methods.

## Learning objectives

- Explain how SFT targets, serialization, and loss masks determine the behavior being optimized.
- Compare full fine-tuning, LoRA, and QLoRA in terms of update constraints, memory use, and deployment implications.
- Design a bounded adaptation comparison that distinguishes data, objective, optimization, and parameterization effects.
- Assess specialization gains, retained capabilities, and cost using actual runs or attributable experimental artifacts.

## Content checklist

- [ ] Connect continued pretraining, task SFT, and instruction SFT to their data distributions, target positions, and intended adaptation.
- [ ] Analyze prompt/completion and conversation objectives, assistant-only versus broader loss masks, EOS handling, truncation, and packing boundaries.
- [ ] Explain adaptation as a change in the model's conditional distribution and distinguish useful specialization from memorization or capability regression.
- [ ] Describe LoRA's frozen base and constrained trainable updates, including rank, scaling, target modules, and their interaction with the task.
- [ ] Explain QLoRA's quantized frozen base and trainable adapters; distinguish parameter savings from activation memory and total training resources.
- [ ] Compare full updates and adapters, including mergeability, base-revision compatibility, precision, and potential serving overhead.
- [ ] Design ablations for one adaptation choice while documenting shared data, token exposure, optimization settings, and tuning budget.
- [ ] Interpret loss curves, checkpoints, in-domain results, out-of-domain retention, and calibration changes without treating lower SFT loss as sufficient evidence.
- [ ] Prepare matched before/after artifacts with example-level errors, resource measurements, and the limits of small-run conclusions.

## Proposed lab

### Compare adaptation choices on a domain capability

**Research question:** How does one adaptation choice change domain-specific capability and retained general capability at a specified training budget?

**Hypothesis:** Choose one comparison, such as two LoRA target-module/rank settings or LoRA versus full fine-tuning when feasible. Predict a task-specific benefit and a possible failure; do not assume that more trainable parameters or a larger rank must win.

**Controls:** Include the unchanged base as a reference. For the main adaptation comparison, fix the training examples, serialization, loss-mask policy, consumed-token budget, and evaluation protocol. Match optimization and tuning budgets where justified and report any unavoidable differences.

**Learner analysis:**

- Select a domain task with independently checkable outputs and a separate retention suite; justify the adaptation variable being tested.
- Inspect serialized examples and marked target regions to determine which behavior each objective rewards.
- Explain observed improvements and regressions, distinguishing objective or data effects from the parameterization claim.

**Agent execution:**

- Prepare and run the bounded adaptation configurations, or assemble clearly attributed matched-run artifacts if fresh training is impractical.
- Record base/tokenizer revisions, trainable modules, target masks, optimization settings, token exposure, checkpoint selection, and resource use.
- Evaluate the base and adapted checkpoints under the frozen protocol, preserving predictions and verifying adapter/base compatibility.

**Artifacts to verify:**

- An adaptation hypothesis and controlled-comparison matrix with an unchanged-base reference.
- Serialized training examples, target-region visualizations, data provenance, and consumed-token records.
- Training summaries, checkpoint provenance, model/adapter configurations, and memory/runtime measurements.
- Paired in-domain and retention results, error examples, and a claim ledger identifying untested mechanisms or confounders.

**Acceptance criteria:**

- The selected targets and masks correspond to the intended adaptation, including truncated and multi-turn cases.
- Claims about LoRA, QLoRA, or full fine-tuning are limited to the controlled comparison; different recipes are not treated as an isolated parameterization effect.
- Target improvements are reported alongside retention, uncertainty, and resource costs; checkpoints are selected without using final test outcomes.
- Reviewed artifacts are attributed, reproduced runs are identified, and missing evidence is not replaced by expected results.

**Experiment specification for an implementation agent:**

```text
Prepare the specified bounded adaptation comparison and an unchanged-base reference.
Keep data, serialization, loss-mask policy, token exposure, and evaluation controlled.
Record update targets, rank/precision choices, optimization settings, tuning budget, and revisions.
Show representative target masks before training and preserve checkpoint-selection evidence.
Return paired task/retention predictions, loss summaries, resource measurements, and failure cases.
If using existing artifacts, attribute their origin and disclose unmatched conditions.
```

## Self-check questions

### 1. Why can two SFT runs on the same examples optimize different behaviors?

**Answer guidance:** Serialization, role boundaries, truncation, and loss masks determine which targets contribute to the objective. Identical source records do not guarantee identical training sequences or gradient signals.

### 2. Why does LoRA's smaller trainable-parameter count not fully determine its memory or serving advantage?

**Answer guidance:** Base weights, activations, optimizer state, precision, sequence length, and execution strategy also matter. Serving depends on whether and how updates are merged or applied, not just the trainable count.

### 3. What is missing if LoRA beats a full-fine-tuning baseline trained with a different recipe?

**Answer guidance:** The result compares complete recipes unless data, exposure, objective, optimization, and tuning differences are controlled or explicitly analyzed. It does not isolate the low-rank update constraint by itself.

## Optional technical deep dive

- Derive the low-rank update and inspect gradient flow through frozen or quantized base weights.
- Trace target tensors, masking, adapter merging, and optimizer-state memory in an implementation.
- Implement a training loop or a broader rank/target-module sweep when a specific unanswered question justifies it.

## Completion checklist

- [ ] Include a worked adaptation comparison linking objective specification, update constraints, and measured outcomes.
- [ ] Provide bounded run configurations or attributable artifacts with target masks, checkpoint provenance, and predictions.
- [ ] Provide rubrics for mechanism claims, control quality, retention analysis, and resource tradeoffs.
- [ ] Include serialization, masking, adapter-compatibility, overfitting, and recipe-confounding failures to diagnose.
- [ ] Verify primary references, data/model licenses, versioned tooling, and result provenance; separate technical extensions.

## References

- [Hu et al. — LoRA](https://arxiv.org/abs/2106.09685): constrained low-rank adaptation and empirical comparisons.
- [Dettmers et al. — QLoRA](https://arxiv.org/abs/2305.14314): adaptation through a quantized frozen base and its memory-design choices.
- [Hugging Face TRL — SFT Trainer](https://huggingface.co/docs/trl/en/sft_trainer): dataset formats, target masking, and SFT implementation behavior; pin the experiment's version.

References checked on **2026-11-15**.

## Completion criteria

- You can explain what an SFT objective trains and how its target specification can differ from the intended behavior.
- You can justify an adaptation configuration using update constraints, available resources, and deployment requirements.
- You can assess a bounded comparison without confusing specialization, recipe differences, and general improvements in model capability.

**Previous:** [07 · Evaluation and experimental design](../07-evaluation/README.md) · **Next:** [09 · Alignment, reasoning and inference-time compute](../09-alignment-reasoning/README.md)
