# 03 · Context dynamics and in-context learning

[Home](../../README.md) · [LLM roadmap](../README.md)

## Learning objectives

- Explain behavior changes under text conditioning while model parameters remain fixed.
- Analyze demonstrations as evidence about a task, latent rule, label mapping, or output convention.
- Distinguish nominal context capacity from effective use of relevant information.
- Relate order, position, interference, and truncation to possible mechanisms and alternative explanations.
- Distinguish contextual state, information encoded in parameters, and external retrieval or persistent memory.

## Content checklist

- [ ] Formalize the distinction between conditioning on a context and updating parameters through training.
- [ ] Analyze in-context demonstrations as task/rule inference, separating empirical behavior from proposed mechanistic explanations.
- [ ] Present implicit Bayesian inference as a theory with explicit assumptions, not a universal account of all LLM behavior.
- [ ] Explain label priors, demonstration composition, ordering, and distribution mismatch as competing influences.
- [ ] Distinguish nominal context windows, retained information, and empirically usable context length.
- [ ] Analyze position effects, distractor interference, retrieval cues, and conflicting evidence without assuming a universal positional curve.
- [ ] Compare transient activations/KV state, parameter-encoded knowledge, and externally retrieved or stored information.
- [ ] Explain the effects of demonstration mappings and positions when content and token budget are controlled.
- [ ] Identify which observations establish conditional adaptation and which would require stronger mechanistic evidence.

## References

- [Brown et al. — Language Models are Few-Shot Learners](https://arxiv.org/abs/2005.14165): empirical task conditioning with demonstrations and no gradient updates at evaluation time.
- [Xie et al. — An Explanation of In-context Learning as Implicit Bayesian Inference](https://arxiv.org/abs/2111.02080): a theory and controlled experiments under stated generative assumptions.
- [Liu et al. — Lost in the Middle](https://arxiv.org/abs/2307.03172): evidence that information position can affect performance on long-context tasks in the studied models.

Sources checked on 2026-11-15. Historical findings motivate controls; their quantitative effects are not assumed to hold for every later model.

---

[← Previous: 02 · Transformer architecture](../02-transformer-architecture/README.md) · [Next: 04 · Training dynamics and scaling →](../04-training-dynamics-scaling/README.md)
