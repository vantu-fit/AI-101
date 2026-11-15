# 04 · Training dynamics and scaling

[Home](../../README.md) · [LLM roadmap](../README.md)

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
- [ ] Interpret parameter/token allocation evidence and the limits of the measured scaling regime.

## References

- [Kaplan et al. — Scaling Laws for Neural Language Models](https://arxiv.org/abs/2001.08361): empirical relationships among loss, model size, data, and training compute in the studied regime.
- [Hoffmann et al. — Training Compute-Optimal Large Language Models](https://arxiv.org/abs/2203.15556): parameter/token allocation under a fixed training-compute budget.
- [Meta — The Llama 3 Herd of Models](https://arxiv.org/abs/2407.21783): a concrete large-scale training and deployment-oriented model-family case study.

Sources checked on 2026-11-15. Treat fitted laws and recommended allocations as conditional on the study's data, architecture, optimization, and objective.

---

[← Previous: 03 · Context dynamics and in-context learning](../03-context-and-in-context-learning/README.md) · [Next: Module 05 →](../05-decoding-model-behavior/README.md)
