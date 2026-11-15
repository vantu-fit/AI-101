# 09 · Alignment, reasoning and inference-time compute

[Home](../../README.md) · [LLM roadmap](../README.md)

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
- [ ] Explain how task- and difficulty-sensitive compute comparisons depend on fixed evaluation rules, actual token/runtime budgets, and explicit generalization limits.

## References

- [Ouyang et al. — Training language models to follow instructions with human feedback](https://arxiv.org/abs/2203.02155): demonstrations, preference data, and RLHF in an empirical post-training pipeline.
- [Rafailov et al. — Direct Preference Optimization](https://arxiv.org/abs/2305.18290): preference objectives and the relationship to reward-based alignment.
- [DeepSeek-AI et al. — DeepSeek-R1](https://arxiv.org/abs/2501.12948): a primary case study of reasoning-oriented reinforcement learning and verifiable tasks.
- [Turpin et al. — Language Models Don't Always Say What They Think](https://arxiv.org/abs/2305.04388): evidence on limitations of treating generated explanations as faithful accounts.

References checked on **2026-11-15**.

---

**Previous:** [08 · Fine-tuning and parameter-efficient adaptation](../08-sft-peft/README.md) · **Next:** [10 · Inference and serving](../10-inference-serving/README.md)
