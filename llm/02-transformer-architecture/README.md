# 02 · Transformer architecture and information flow

[Home](../../README.md) · [LLM roadmap](../README.md)

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
- [ ] Explain the conditions for cached/full-prefix equivalence and why attention displays alone do not prove causal importance.

## References

- [Vaswani et al. — Attention Is All You Need](https://arxiv.org/abs/1706.03762): the original attention-based architecture and its encoder–decoder setting.
- [Su et al. — RoFormer](https://arxiv.org/abs/2104.09864): rotary positional embeddings and position-dependent attention.
- [Ainslie et al. — GQA](https://arxiv.org/abs/2305.13245): grouped-query attention and trained conversion from multi-head checkpoints.
- [Meta — The Llama 3 Herd of Models](https://arxiv.org/abs/2407.21783): a concrete modern decoder-family reference for architecture and runtime choices.

Sources checked on 2026-11-15. Architecture variants must be traced to the selected checkpoint rather than assumed from a model-family name.

---

[← Previous: 01 · Language modeling and representations](../01-language-modeling-representations/README.md) · [Next: 03 · Context dynamics and in-context learning →](../03-context-and-in-context-learning/README.md)
