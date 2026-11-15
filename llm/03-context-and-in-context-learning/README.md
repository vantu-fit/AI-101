# 03 · Context dynamics and in-context learning

[Home](../../README.md) · [LLM roadmap](../README.md)

**Estimated core time:** 10 hours; machine runtime is separate.

**Prerequisites:** [01 · Language modeling and representations](../01-language-modeling-representations/README.md) and [02 · Transformer architecture](../02-transformer-architecture/README.md); assume established experimental-design and evaluation practice.

**Status:** Content outline; unchecked items track shared authoring and review work.

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
- [ ] Design interventions that change demonstration mappings or positions while controlling their content and token budget.
- [ ] Identify which observations establish conditional adaptation and which would require stronger mechanistic evidence.

## Proposed lab

**Experimental question:** Do predictions track a context-supplied label mapping, and does moving the same demonstrations within a longer context change that adaptation?

**Hypothesis:** If demonstrations contribute to task inference, predictions should respond to a consistent label permutation. Their influence may depend on placement even when the entire sequence fits the advertised context window; the shape and magnitude are empirical questions.

Use a synthetic classification task with a known rule, balanced nonce labels, and query instances absent from the demonstrations. Cross consistent label permutations with demonstration-block positions at two fixed context lengths. Include a zero-demonstration baseline and preserve the distractor contents when moving the block.

**Controls:** Checkpoint, task rule, example identities, class balance, label token lengths, total token budget, query location, decoding, and context reset. Verify that no silent truncation occurs. Keep label permutations consistent within each context.

**Learner role:** Specify competing hypotheses about priors, mapping inference, and effective context. **Agent role:** Generate the controlled conditions, execute them with fixed weights, and export per-condition predictions and positional metadata.

**Artifacts:** Task generator/specification; demonstration and query identities; label mappings; tokenized contexts with block positions; accuracy and mapping-consistency results; contrasts across positions, lengths, and permutations.

**Acceptance criteria:**

- Results distinguish following the supplied mapping from succeeding under a model's preferred label convention.
- Position comparisons preserve example and distractor content and explicitly record any unavoidable token-layout differences.
- Nominal capacity, absence of truncation, and measured task success are reported as different properties.
- Conditional adaptation is not presented as a parameter update or proof that one theoretical account fully explains the model.

**Experiment specification for an implementation agent:**

```text
Implement the specified synthetic task with balanced nonce labels and held-out query instances.
Cross consistent label permutations with demonstration-block positions at two context lengths.
Keep example identities and distractor content fixed; record token lengths and verify no truncation.
Add a zero-demonstration baseline, reset context state, and leave model weights unchanged.
Return per-query predictions, mapping-consistency contrasts, and position/length effects with uncertainty.
```

This is an experiment specification; no execution results are claimed here.

## Self-check questions

1. What does successful adaptation to a permuted label mapping establish, and what does it leave unresolved?
2. Why can a sequence fit within the supported context window while the model still fails to use its relevant evidence?
3. How does retrieving a passage differ from information stored in parameters or retained in the current contextual state?

**Answer guidance:**

- Question 1: It supports a causal role for the supplied mapping under the tested conditions. It does not identify the complete internal algorithm or demonstrate general task learning.
- Question 2: Capacity to accept tokens does not ensure effective information use; positional interactions, interference, task difficulty, and learned behavior may matter.
- Question 3: Retrieval selects external information to condition the computation; parameters encode learned structure, while contextual state depends on the current sequence and execution policy.

## Completion checklist

- [ ] The conceptual treatment separates conditional behavior, task inference hypotheses, and weight adaptation.
- [ ] The lab specifies label, content, position, length, and truncation controls.
- [ ] Answer criteria distinguish nominal context, effective context, label priors, and externally supplied information.
- [ ] Failure cases include inconsistent permutations, unmatched label lengths, query leakage, silent truncation, and universalizing one observed positional pattern.
- [ ] Primary evidence and the scope of each theoretical interpretation have been independently reviewed.

## References

- [Brown et al. — Language Models are Few-Shot Learners](https://arxiv.org/abs/2005.14165): empirical task conditioning with demonstrations and no gradient updates at evaluation time.
- [Xie et al. — An Explanation of In-context Learning as Implicit Bayesian Inference](https://arxiv.org/abs/2111.02080): a theory and controlled experiments under stated generative assumptions.
- [Liu et al. — Lost in the Middle](https://arxiv.org/abs/2307.03172): evidence that information position can affect performance on long-context tasks in the studied models.

Sources checked on 2026-11-15. Historical findings motivate controls; their quantitative effects are not assumed to hold for every later model.

## Completion criteria

- Explain in-context adaptation without conflating it with parameter learning.
- Interpret the label-permutation and position contrasts against the competing hypotheses.
- Design a follow-up intervention that separates an effective-context limitation from a task, prior, or retrieval issue.

Personal completion is separate from the shared authoring checklist.

## Optional technical deep dive

Work through the assumptions of the Bayesian account, study induction-head hypotheses, inspect intermediate activations, or implement causal representation interventions. Formal proofs and internal tensor analyses are optional; they require evidence beyond behavior alone.

---

[← Previous: 02 · Transformer architecture](../02-transformer-architecture/README.md) · [Next: 04 · Training dynamics and scaling →](../04-training-dynamics-scaling/README.md)
