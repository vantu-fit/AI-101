# 08 · Fine-tuning and parameter-efficient adaptation

[Home](../../README.md) · [LLM roadmap](../README.md)

## Learning objectives

- Explain how SFT targets, serialization, and loss masks determine the behavior being optimized.
- Compare full fine-tuning, LoRA, and QLoRA in terms of update constraints, memory use, and deployment implications.
- Explain how adaptation comparisons distinguish data, objective, optimization, and parameterization effects.
- Assess specialization gains, retained capabilities, and cost using actual runs or attributable experimental artifacts.

## Content checklist

- [ ] Connect continued pretraining, task SFT, and instruction SFT to their data distributions, target positions, and intended adaptation.
- [ ] Analyze prompt/completion and conversation objectives, assistant-only versus broader loss masks, EOS handling, truncation, and packing boundaries.
- [ ] Explain adaptation as a change in the model's conditional distribution and distinguish useful specialization from memorization or capability regression.
- [ ] Describe LoRA's frozen base and constrained trainable updates, including rank, scaling, target modules, and their interaction with the task.
- [ ] Explain QLoRA's quantized frozen base and trainable adapters; distinguish parameter savings from activation memory and total training resources.
- [ ] Compare full updates and adapters, including mergeability, base-revision compatibility, precision, and potential serving overhead.
- [ ] Explain the controls needed to isolate one adaptation choice, including shared data, token exposure, optimization settings, and tuning budget.
- [ ] Interpret loss curves, checkpoints, in-domain results, out-of-domain retention, and calibration changes without treating lower SFT loss as sufficient evidence.
- [ ] Interpret matched before/after comparisons using example-level errors and resource measurements, including the limits of small-run conclusions.

## References

- [Hu et al. — LoRA](https://arxiv.org/abs/2106.09685): constrained low-rank adaptation and empirical comparisons.
- [Dettmers et al. — QLoRA](https://arxiv.org/abs/2305.14314): adaptation through a quantized frozen base and its memory-design choices.
- [Hugging Face TRL — SFT Trainer](https://huggingface.co/docs/trl/en/sft_trainer): dataset formats, target masking, and SFT implementation behavior; check the relevant software version.

References checked on **2026-11-15**.

---

**Previous:** [07 · Evaluation and experimental design](../07-evaluation/README.md) · **Next:** [09 · Alignment, reasoning and inference-time compute](../09-alignment-reasoning/README.md)
