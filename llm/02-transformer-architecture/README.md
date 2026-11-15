# 02 · Transformer architecture and information flow

[Home](../../README.md) · [LLM roadmap](../README.md)

**Estimated core time:** 12 hours; machine runtime is separate.

**Prerequisites:** [01 · Language modeling and representations](../01-language-modeling-representations/README.md), established neural-network knowledge, and familiarity with model configuration and inference.

**Status:** Content outline; unchecked items track shared authoring and review work.

## Learning objectives

- Explain how Q/K/V attention, causal masking, positional mechanisms, feed-forward layers, residual paths, and normalization interact.
- Distinguish properties of the original Transformer from choices made by a specific decoder-only model.
- Explain what KV caching reuses, why causal structure makes reuse possible, and which invariants must be preserved.
- Connect multi-head, multi-query, and grouped-query attention to KV storage and inference tradeoffs.
- Interpret architectural interventions without confusing changed computation, changed weights, and changed runtime behavior.

## Content checklist

- [ ] Trace information flow through a decoder block, including attention and feed-forward contributions to the residual stream.
- [ ] Explain Q/K/V projections, head specialization limits, causal masking, and output mixing as mechanisms.
- [ ] Compare learned/absolute positional representations with RoPE and discuss limits of length extrapolation.
- [ ] Explain feed-forward expansion and gating, residual paths, pre/post normalization, and architecture-specific norm choices.
- [ ] Distinguish encoder, encoder–decoder, and decoder-only information-access patterns.
- [ ] Explain prefill, incremental decoding, cached keys/values, position IDs, and mask invariants.
- [ ] Compare MHA, MQA, and GQA, including their effects on logical KV payload and checkpoint compatibility.
- [ ] Separate attention computation, logical cache storage, allocator behavior, and kernel-dependent runtime costs.
- [ ] Develop a cache-equivalence experiment and identify why attention displays alone do not prove causal importance.

## Proposed lab

**Experimental question:** Does incremental KV-cached decoding preserve the conditional distribution computed from a full prefix, and how does the cache grow for the selected architecture?

**Hypothesis:** A correct cache path agrees with full-prefix computation within a justified numerical tolerance when token histories, positions, masks, weights, and precision are matched. For an ordinary dense append-only KV cache, logical storage grows with retained sequence length and KV-head count.

Choose one inspectable decoder checkpoint, preferably using GQA. For fixed teacher-forced sequences, compare each selected position through full-prefix recomputation and incremental cached execution. Measure logical cache payload at several prefix lengths, separately from allocated device memory.

**Controls:** Token history, checkpoint, dtype, evaluation mode, backend, positional handling, masks, and cache policy. Document sliding windows, quantized caches, or other mechanisms that change the expected storage model.

**Learner role:** State the mechanism-level predictions and interpret mismatches. **Agent role:** Instrument both execution paths, inspect the architecture/configuration, and collect numerical and memory evidence.

**Artifacts:** An architecture map tied to the actual config; per-position distribution comparisons; cache metadata and payload measurements; device-memory observations; recorded tolerances and failure diagnoses.

**Acceptance criteria:**

- The comparison uses the same teacher-forced token history so sampled divergence cannot masquerade as a cache error.
- Observed distribution differences are reported against a declared tolerance with any precision/backend limitations.
- Logical KV payload is distinguished from allocator-reserved or total device memory.
- GQA/MHA storage counterfactuals are labeled analytical; changing KV-head count in a trained checkpoint is not treated as a valid quality-preserving toggle.

**Experiment specification for an implementation agent:**

```text
Instrument full-prefix and incremental cached execution for one fixed decoder checkpoint.
Use the same teacher-forced token histories, masks, positions, dtype, backend, and evaluation mode.
Export per-position distribution differences and logical KV payload across prefix lengths.
Map the actual attention-head, positional, FFN, residual, and normalization configuration.
Record device-memory observations separately and diagnose any failed equivalence checks.
```

This is an experiment specification; no execution results are claimed here.

## Self-check questions

1. Why can a causal decoder reuse earlier keys and values, and which positional or masking mistakes would break equivalence?
2. What changes when query heads share KV heads, and why does this not justify editing a trained checkpoint's head count arbitrarily?
3. Why are feed-forward and residual computations essential when interpreting an attention-based explanation of an output?

**Answer guidance:**

- Question 1: Earlier representations do not depend on subsequently appended tokens in the causal computation. Incorrect position offsets, masks, or history reuse can invalidate the cached state.
- Question 2: KV projections and stored state are shared across query groups, changing capacity and cache requirements. Learned parameterization and any conversion/training procedure must remain valid.
- Question 3: Attention mixes information within a larger computation; other transformations and paths affect the final state. A weight pattern is not a complete causal explanation.

## Completion checklist

- [ ] An architecture walkthrough connects the actual checkpoint configuration to its information flow.
- [ ] The lab specifies cache invariants, numerical tolerances, and separate logical/device-memory measurements.
- [ ] Answer criteria cover RoPE/position handling, KV reuse, GQA, and the surrounding block mechanisms.
- [ ] Failure cases include cache-position errors, sampled-history mismatch, unsupported head conversions, and allocator confusion.
- [ ] Primary sources, architecture claims, and reported measurements have been independently reviewed.

## References

- [Vaswani et al. — Attention Is All You Need](https://arxiv.org/abs/1706.03762): the original attention-based architecture and its encoder–decoder setting.
- [Su et al. — RoFormer](https://arxiv.org/abs/2104.09864): rotary positional embeddings and position-dependent attention.
- [Ainslie et al. — GQA](https://arxiv.org/abs/2305.13245): grouped-query attention and trained conversion from multi-head checkpoints.
- [Meta — The Llama 3 Herd of Models](https://arxiv.org/abs/2407.21783): a concrete modern decoder-family reference for architecture and runtime choices.

Sources checked on 2026-11-15. Architecture variants must be traced to the selected checkpoint rather than assumed from a model-family name.

## Completion criteria

- Explain the selected decoder's information flow and positional/cache invariants.
- Interpret cached versus full-prefix results and localize at least one plausible failure mechanism.
- Explain the observed cache scaling and the limits of any architectural counterfactual.

Personal completion is separate from the shared authoring checklist.

## Optional technical deep dive

Derive attention and RoPE identities, trace tensor layouts, implement attention kernels, or reproduce GQA conversion and uptraining. These extend the core's architecture analysis; hand derivations and manual component implementation are not completion requirements.

---

[← Previous: 01 · Language modeling and representations](../01-language-modeling-representations/README.md) · [Next: 03 · Context dynamics and in-context learning →](../03-context-and-in-context-learning/README.md)
