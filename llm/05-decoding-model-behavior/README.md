# 05 · Decoding, uncertainty and model behavior

[Home](../../README.md) · [LLM roadmap](../README.md)

## Learning objectives

- Explain how greedy decoding, temperature, top-k, and top-p transform the distribution used to select generated tokens.
- Analyze how conditioning on generated prefixes can propagate errors or change subsequent behavior.
- Distinguish token likelihood, sequence likelihood, answer correctness, and task-defined confidence.
- Explain how decoding comparisons separate quality, variability, calibration claims, and compute cost.

## Content checklist

- [ ] Connect autoregressive factorization to sequential generation, stopping conditions, and exposure to the model's own prefixes.
- [ ] Compare greedy selection with temperature scaling, top-k truncation, top-p truncation, and renormalization.
- [ ] Distinguish probabilities under the original model from scores after decoding transformations; document what an inference interface actually exposes.
- [ ] Explain the gap between teacher-forced prediction quality and free-running generation, using error propagation and repetition cases.
- [ ] Analyze length effects, tokenization, and the limits of interpreting sequence scores as confidence in factual correctness.
- [ ] Explain uncertainty measures, explicit predicted events, and why calibration depends on the task, output representation, and evaluation distribution.
- [ ] Explain why decoding comparisons require fixed model/input conditions and repeated stochastic generations where relevant.
- [ ] Define observable comparisons of correctness, diversity, repetition, answer consistency, output length, and cost.
- [ ] Include counterexamples where fluent, high-probability, or repeatedly generated answers are wrong; separate measurement from explanations of internal computation.

## References

- [Hugging Face — Generation strategies](https://huggingface.co/docs/transformers/main/en/generation_strategies): decoding behavior and implementation terminology; pin the version used in experiments.
- [Holtzman et al. — The Curious Case of Neural Text Degeneration](https://arxiv.org/abs/1904.09751): decoding, degeneration, and nucleus sampling.
- [Kadavath et al. — Language Models (Mostly) Know What They Know](https://arxiv.org/abs/2207.05221): task-dependent self-evaluation and calibration findings and limitations.

References checked on **2026-11-15**.

---

**Previous:** [04 · Training dynamics and scaling](../04-training-dynamics-scaling/README.md) · **Next:** [06 · Data pipelines and pretraining design](../06-data-pretraining/README.md)
