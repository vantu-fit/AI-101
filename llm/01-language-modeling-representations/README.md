# 01 · Language modeling and representations

[Home](../../README.md) · [LLM roadmap](../README.md)

## Learning objectives

- Explain autoregressive sequence modeling, teacher-forced likelihood, and the distinction between scoring and generation.
- Trace the roles of tokenization, input embeddings, contextual representations, and the output projection or unembedding.
- Analyze how vocabulary and segmentation affect data allocation, context coverage, loss interpretation, and multilingual behavior.
- Distinguish changes to model parameters from changes to conditional activations and externally supplied context.
- Identify what a representation experiment can establish independently of overall model quality.

## Content checklist

- [ ] Present the autoregressive factorization and negative log-likelihood objective, including conditioning and document boundaries.
- [ ] Explain teacher forcing, sequence-level scoring, generation, and why their observed errors can differ.
- [ ] Compare subword, byte-level, and multilingual segmentation choices through their modeling consequences.
- [ ] Trace token IDs through input embeddings, contextual hidden states, and vocabulary logits.
- [ ] Explain output embeddings/unembedding, weight tying, and why a tied output projection is not an inverse of the network.
- [ ] Analyze vocabulary size, sequence expansion, special tokens, normalization, and their effects on training and inference budgets.
- [ ] Distinguish token-level likelihood from byte-normalized quantities and task measures; specify valid comparison units.
- [ ] Analyze multilingual representation effects while separating translation quality, training exposure, and tokenization as confounders.
- [ ] Explain how context-budget comparisons distinguish retained information from language-dependent model behavior.

## References

- [Brown et al. — Language Models are Few-Shot Learners](https://arxiv.org/abs/2005.14165): autoregressive language modeling and evaluation under text conditioning.
- [Press and Wolf — Using the Output Embedding to Improve Language Models](https://arxiv.org/abs/1608.05859): output embeddings and input/output weight tying.
- [Petrov et al. — Language Model Tokenizers Introduce Unfairness Between Languages](https://arxiv.org/abs/2305.15425): empirical evidence about unequal encoding lengths and their consequences.
- [Hugging Face — Tokenizers](https://huggingface.co/learn/llm-course/chapter6/1): implementation details and segmentation algorithms to consult as needed.

Sources checked on 2026-11-15. Published findings do not predetermine behavior on another checkpoint or language pair.

---

[← Previous: 00 · LLM systems map](../00-llm-systems-map/README.md) · [Next: 02 · Transformer architecture →](../02-transformer-architecture/README.md)
