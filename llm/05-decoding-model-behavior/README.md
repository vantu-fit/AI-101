# 05 · Decoding, uncertainty and model behavior

[Home](../../README.md) · [LLM roadmap](../README.md)

**Estimated core time:** 10 hours. Optional technical extensions and long experiment runs are outside this estimate.

**Prerequisites:** [Language modeling and representations](../01-language-modeling-representations/README.md), [Transformer architecture](../02-transformer-architecture/README.md), and [Context and in-context learning](../03-context-and-in-context-learning/README.md).

**Status:** Content scaffold; unchecked items still need to be written or reviewed.

Checkboxes track shared content readiness. This module assumes programming and ML proficiency and focuses on how decoding changes the behavior of a fixed autoregressive model.

## Learning objectives

- Explain how greedy decoding, temperature, top-k, and top-p transform the distribution used to select generated tokens.
- Analyze how conditioning on generated prefixes can propagate errors or change subsequent behavior.
- Distinguish token likelihood, sequence likelihood, answer correctness, and task-defined confidence.
- Design a decoding comparison that separates quality, variability, calibration claims, and compute cost.

## Content checklist

- [ ] Connect autoregressive factorization to sequential generation, stopping conditions, and exposure to the model's own prefixes.
- [ ] Compare greedy selection with temperature scaling, top-k truncation, top-p truncation, and renormalization.
- [ ] Distinguish probabilities under the original model from scores after decoding transformations; document what an inference interface actually exposes.
- [ ] Explain the gap between teacher-forced prediction quality and free-running generation, using error propagation and repetition cases.
- [ ] Analyze length effects, tokenization, and the limits of interpreting sequence scores as confidence in factual correctness.
- [ ] Explain uncertainty measures, explicit predicted events, and why calibration depends on the task, output representation, and evaluation distribution.
- [ ] Prepare controlled decoding interventions with fixed model/input conditions and repeated stochastic generations where relevant.
- [ ] Define observable comparisons of correctness, diversity, repetition, answer consistency, output length, and cost.
- [ ] Include counterexamples where fluent, high-probability, or repeatedly generated answers are wrong; separate measurement from explanations of internal computation.

## Proposed lab

### Decoding intervention on a fixed model

**Research question:** How does changing the sampling policy affect correctness and variability on checkable technical questions, and repetition on a small continuation subset?

**Hypothesis:** A predefined sampling intervention changes output diversity, but any effect on correctness depends on the task. State the expected direction for each measured outcome and an observation that would contradict it.

**Controls:** Fix model/tokenizer revisions, input examples, templates, context, stopping rules, and output limits. Change one decoding factor at a time or explicitly identify a joint intervention. Record repeated-generation settings and actual compute for every condition.

**Learner analysis:**

- Specify the intervention and distinguish the model distribution from the sampling policy being tested.
- Inspect examples where prefixes diverge, and assess whether later errors are consistent with those differences without claiming a complete causal account of internals.
- Define what any reported confidence score predicts, then determine whether the evidence supports a calibration claim.

**Agent execution:**

- Run the fixed comparison, save every generation, and report the distributions of quality, output length, variability, and runtime.
- Collect actual logits or log probabilities only when exposed; identify whether they are before or after decoding transformations. Label teaching numbers as illustrative when those values are unavailable.

**Artifacts to verify:**

- An experiment manifest, hypotheses, input IDs, decoding settings, repeated-run records, and raw outputs.
- Paired example-level comparisons and aggregate summaries that do not treat repeated outputs as independent task examples.
- Optional observed score traces with their exact semantics, plus correctness labels and failure examples.
- A conclusion separating sampling effects, factual accuracy, uncertainty estimates, and unsupported mechanistic claims.

**Acceptance criteria:**

- The comparison identifies what changed and what remained fixed, including differences in total generation budget.
- Claims about probabilities use observed values with documented semantics; generated explanations are not evidence of internal computation.
- Calibration claims specify the predicted event and evaluation population; token likelihood alone is not treated as a probability of factual correctness.
- The interpretation includes failures, stochastic variability, and the limits of the sample and task coverage.

**Experiment specification for an implementation agent:**

```text
Run the preregistered decoding comparison on the fixed model and input set.
Preserve all non-intervention settings and record generation counts and actual compute.
Save raw outputs, example IDs, stopping behavior, quality labels, and repeated-run settings.
Expose logits/logprobs only if available and document pre/post-transformation semantics.
Return paired comparisons, variability summaries, failure cases, and evidence provenance.
Do not invent probabilities or present generated explanations as internal measurements.
```

## Self-check questions

### 1. Does a high-probability generated sequence imply that its factual claims are likely correct?

**Answer guidance:** Sequence likelihood concerns a particular token sequence under a model and context. Factual correctness is a different event; length, wording, tokenization, and the task distribution affect any relationship between them.

### 2. Why can two runs diverge substantially after a small difference early in generation?

**Answer guidance:** Each new token becomes part of the conditioning prefix. Later predictions therefore condition on different histories; the full divergence cannot be attributed only to the probability of the first differing token.

### 3. What evidence is missing when a system calls its answers calibrated because its token probabilities are available?

**Answer guidance:** It needs an explicit predicted event, a defensible mapping to a confidence value, observed correctness outcomes, and evaluation on the relevant distribution. Access to scores does not establish calibration.

## Optional technical deep dive

- Derive temperature scaling and truncation/renormalization, or inspect a tensor-level decoding implementation.
- Study entropy, sequence scoring, reliability diagrams, and proper scoring rules in more mathematical detail.
- Implement samplers or a controlled prefix-intervention experiment to investigate a specific behavior.

## Completion checklist

- [ ] Include a worked comparison linking the sampling intervention to observable behavior and a qualified interpretation.
- [ ] Provide a runnable experiment or traceable run artifacts with complete settings and score semantics.
- [ ] Provide answer guidance and rubrics for decoding, uncertainty, and calibration claims.
- [ ] Include misleading likelihood, repetition, confidence, and repeated-sample interpretations to diagnose.
- [ ] Verify primary references, version-specific behavior, and result provenance; keep technical extensions distinct.

## References

- [Hugging Face — Generation strategies](https://huggingface.co/docs/transformers/main/en/generation_strategies): decoding behavior and implementation terminology; pin the version used in experiments.
- [Holtzman et al. — The Curious Case of Neural Text Degeneration](https://arxiv.org/abs/1904.09751): decoding, degeneration, and nucleus sampling.
- [Kadavath et al. — Language Models (Mostly) Know What They Know](https://arxiv.org/abs/2207.05221): task-dependent self-evaluation and calibration findings and limitations.

References checked on **2026-11-15**.

## Completion criteria

- You can explain how a decoding intervention changes generation while model weights stay fixed.
- You can interpret paired outputs and available scores without conflating likelihood, correctness, and calibration.
- You can defend a decoding choice using measured quality, variability, cost, and task-specific limitations.

**Previous:** [04 · Training dynamics and scaling](../04-training-dynamics-scaling/README.md) · **Next:** [06 · Data pipelines and pretraining design](../06-data-pretraining/README.md)
