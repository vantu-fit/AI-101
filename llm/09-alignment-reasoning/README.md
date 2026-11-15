# 09 · Alignment, reasoning and inference-time compute

[Home](../../README.md) · [LLM roadmap](../README.md)

**Estimated core time:** 12 hours. Optional technical extensions and training experiments are outside this estimate.

**Prerequisites:** [05 · Decoding, uncertainty and model behavior](../05-decoding-model-behavior/README.md), [07 · Evaluation and experimental design](../07-evaluation/README.md), and [08 · Fine-tuning and parameter-efficient adaptation](../08-sft-peft/README.md).

**Status:** Content scaffold; unchecked items still need to be written or reviewed.

Checkboxes track shared content readiness. The focus is on learning signals, objective failures, reasoning evidence, and the allocation of computation during training and inference.

## Learning objectives

- Compare SFT, DPO, RLHF, and reinforcement learning with verifiable rewards (RLVR) by their learning signals and data-generation processes.
- Explain how preference or reward optimization can diverge from intended capability, truthfulness, or retained behavior.
- Distinguish observed reasoning performance from the plausibility or faithfulness of verbalized explanations.
- Evaluate inference-time compute strategies using actual budgets, selection quality, and task-level evidence.

## Content checklist

- [ ] Map demonstrations, preference pairs, learned rewards, and verifiable rewards to the objectives used by SFT, DPO, RLHF, and RLVR.
- [ ] Explain offline preference coverage and distribution mismatch, contrasting fixed-pair learning with online rollout collection and reward evaluation.
- [ ] Describe reward models, reference policies, and constraints on policy drift; distinguish regularization from guarantees of retained capability.
- [ ] Analyze reward hacking, specification errors, noisy preferences, length incentives, verifier loopholes, and overoptimization.
- [ ] Introduce the role of exploration and relative reward signals in reasoning RL, with detailed PPO/GRPO derivations reserved for extension work.
- [ ] Distinguish reasoning capability, generated reasoning traces, and faithfulness; include cases where convincing explanations rationalize incorrect answers.
- [ ] Compare longer trajectories, multiple candidates, self-consistency, verifier-based selection, and distillation as different uses of compute or training data.
- [ ] Separate deployed selection performance from oracle candidate coverage and report the cost of failed or rejected candidates.
- [ ] Design task- and difficulty-sensitive compute comparisons with fixed evaluation rules, actual token/runtime budgets, and explicit generalization limits.

## Proposed lab

### Allocate inference compute and audit the objective

**Research question:** For a checkable reasoning task, is a longer single attempt or selection among several shorter candidates more effective under a defined total budget, and where does the reward or selection rule fail?

**Hypothesis:** Specify which task subset should benefit from each allocation and why. Identify a failure mode in which the verifier, preference rubric, or majority rule favors an incorrect candidate.

**Controls:** Fix model/checkpoint, task examples, context, correctness rules, and development-only selection of settings. Set total budget limits and report actual consumed tokens, calls, and runtime; nominally identical limits do not guarantee identical compute.

**Learner analysis:**

- Map each proposed learning signal or selection score to its intended objective and a possible mismatch.
- Define the budget comparison and distinguish candidate generation, candidate selection, and final correctness.
- Inspect failures and determine whether the evidence concerns inference allocation, a learned capability, or only a plausible verbalization.

**Agent execution:**

- Run the specified allocations and selection rules, preserving all candidates, selections, evaluation outcomes, and actual costs.
- Test the verifier or rubric on deliberate counterexamples and edge cases before the final comparison.
- Prepare attributable examples of SFT/preference/reward objectives for analysis; any additional training experiment is a separate extension.

**Artifacts to verify:**

- An objective map for SFT, DPO, RLHF, and RLVR with signal assumptions and known failure modes.
- The budget specification, hypotheses, task IDs, raw candidates, selection decisions, and correctness labels.
- Quality–cost results by task subset, including failed generations, verifier errors, and any separately labeled oracle analysis.
- A conclusion distinguishing inference improvements, training claims, and unverified accounts of internal reasoning.

**Acceptance criteria:**

- Candidate selection does not use held-out gold answers unavailable at deployment; oracle candidate coverage is reported separately from deployable selection accuracy.
- The comparison includes actual compute and the cost of rejected candidates, with no claim of equal compute based only on nominal limits.
- Longer explanations, higher preference scores, or higher rewards are not treated as sufficient evidence of correctness or faithful reasoning.
- Conclusions identify the evaluated task population, observed objective failures, and what would require an additional training or generalization experiment.

**Experiment specification for an implementation agent:**

```text
Compare the specified inference-compute allocations on a fixed model and paired task set.
Freeze budget and selection settings using development data; preserve all candidates and failures.
Do not use held-out gold answers for candidate selection; label oracle analyses separately.
Record actual tokens, calls, runtime, selections, final correctness, and verifier/rubric failures.
Provide quality-cost and task-subset comparisons with uncertainty appropriate to the runs.
Separate observed inference effects from training claims or explanations of internal reasoning.
```

## Self-check questions

### 1. What changes when moving from fixed preference-pair optimization to online reward-guided rollouts?

**Answer guidance:** The source and coverage of training outputs change along with the objective and optimization process. Examine exploration, current-policy distribution, reward validity, and drift rather than attributing differences solely to the algorithm name.

### 2. Why can a verifiable reward still be an imperfect objective for reasoning?

**Answer guidance:** The verifier may contain bugs, accept accidental shortcuts, or cover only a narrow final-answer criterion. Even correct verification on the training task does not establish broad generalization or faithful explanations.

### 3. Why does high oracle success among many candidates not establish a useful deployed system?

**Answer guidance:** Deployment needs a selection rule that can find the correct candidate without the hidden answer. Include selection errors, all candidate costs, and budget constraints in the evaluated system.

## Optional technical deep dive

- Derive DPO, KL-regularized objectives, policy gradients, PPO, or GRPO for a defined research question.
- Inspect rollout, reward, reference-policy, and optimizer tensors, or implement a small RLVR experiment.
- Study process supervision, distillation, and causal tests of explanation faithfulness beyond the core comparison.

## Completion checklist

- [ ] Include worked objective comparisons and a compute-allocation study with explicit failure cases.
- [ ] Provide bounded inference experiments or attributable artifacts with all candidates, selections, and costs.
- [ ] Provide rubrics for signal assumptions, objective failures, reasoning claims, and deployable selection performance.
- [ ] Include reward loopholes, misleading verbalizations, nominal-budget mismatches, and oracle-selection errors to diagnose.
- [ ] Verify primary references and result provenance; keep mathematical and training extensions distinct.

## References

- [Ouyang et al. — Training language models to follow instructions with human feedback](https://arxiv.org/abs/2203.02155): demonstrations, preference data, and RLHF in an empirical post-training pipeline.
- [Rafailov et al. — Direct Preference Optimization](https://arxiv.org/abs/2305.18290): preference objectives and the relationship to reward-based alignment.
- [DeepSeek-AI et al. — DeepSeek-R1](https://arxiv.org/abs/2501.12948): a primary case study of reasoning-oriented reinforcement learning and verifiable tasks.
- [Turpin et al. — Language Models Don't Always Say What They Think](https://arxiv.org/abs/2305.04388): evidence on limitations of treating generated explanations as faithful accounts.

References checked on **2026-11-15**.

## Completion criteria

- You can explain the signals and assumptions behind SFT, DPO, RLHF, and RLVR and identify an objective failure.
- You can design a compute-allocation comparison that measures deployable selection quality and actual cost.
- You can assess reasoning claims while distinguishing task success, verbalization, inference procedures, and learned behavior.

**Previous:** [08 · Fine-tuning and parameter-efficient adaptation](../08-sft-peft/README.md) · **Next:** [10 · Inference and serving](../10-inference-serving/README.md)
