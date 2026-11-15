# 01 · Language modeling and representations

[Home](../../README.md) · [LLM roadmap](../README.md)

**Estimated core time:** 8 hours; machine runtime is separate.

**Prerequisites:** [00 · LLM systems map](../00-llm-systems-map/README.md), basic probability, and familiarity with ML objectives and learned representations.

**Status:** Content outline; unchecked items track shared authoring and review work.

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
- [ ] Develop a context-budget experiment that distinguishes retained information from language-dependent model behavior.

## Proposed lab

**Experimental question:** How much of a bilingual performance gap under a fixed token budget is associated with unequal retention of source information?

**Hypothesis:** Tokenization can cause semantically matched passages to retain different facts under the same token limit. Restoring full source coverage may reduce that component of the gap; any remaining difference cannot be attributed to tokenization alone.

Create paired English/Vietnamese passages with aligned facts and held-out questions. Use one multilingual checkpoint with its native tokenizer. Evaluate several fixed input-token budgets plus a full-content condition that retains every fact in both languages. Record which source facts survive truncation.

**Controls:** Semantics and question IDs, translation review, checkpoint/tokenizer revisions, truncation policy, answer scoring, output budget, and decoding. The full-content condition controls information coverage, not equal sequence length or inference cost.

**Learner role:** Define the causal comparison and interpret language, coverage, and likelihood effects. **Agent role:** Instrument tokenization and scoring, run the budget conditions, and export aligned results and model representation metadata.

**Artifacts:** Paired source/answer records; a vocabulary and embedding/unembedding manifest, including whether weights are tied; per-condition retained facts, token lengths, answer scores, and conditional target likelihoods where available.

**Acceptance criteria:**

- Each token-budget result identifies the source information actually available to the model.
- Likelihood comparisons hold the scored target and unit fixed within each language; token-level perplexity is not used as a direct cross-tokenizer quality ranking.
- The analysis distinguishes matched-token and matched-content comparisons and acknowledges their different cost controls.
- Residual language differences are not described as a causal tokenizer effect without an additional valid intervention.

**Experiment specification for an implementation agent:**

```text
Use one fixed multilingual checkpoint and its native tokenizer on aligned English/Vietnamese passages.
Run the predefined token budgets and a full-content condition; preserve question and fact identities.
Export retained facts, token lengths, answers, per-case scores, and target likelihoods if exposed.
Inspect vocabulary, input/output embeddings, and weight tying without changing the checkpoint.
Separate within-language likelihood comparisons from cross-language task and coverage comparisons.
```

This is an experiment specification; no execution results are claimed here.

## Self-check questions

1. What differs between a token's input embedding and its contextual representation, and where does the unembedding act?
2. Why can two tokenizers make token-level perplexity incomparable even when both models score the same text?
3. What does the full-content control resolve in the bilingual experiment, and which alternative explanations remain?

**Answer guidance:**

- Question 1: The lookup supplies a learned token representation; contextual layers transform it using the prefix. The output projection maps the resulting state to vocabulary scores, including in weight-tied designs.
- Question 2: Segmentation changes the number and identity of prediction events. Comparable units and scoring conventions must be defined rather than treating all tokens as equivalent.
- Question 3: It tests whether unequal information retention explains part of the gap. Language exposure, model competence, translation fidelity, and sequence-length effects remain possible influences.

## Completion checklist

- [ ] The module connects the autoregressive objective to representation choices and observable behavior.
- [ ] The lab specifies aligned facts, budget conditions, likelihood units, and representation metadata.
- [ ] Answer criteria distinguish embeddings, contextual states, output projection, and valid scoring comparisons.
- [ ] Failure cases include incompatible tokenizer/checkpoint pairs, misleading perplexity comparisons, and unsupported multilingual causal claims.
- [ ] Primary sources and experimental interpretations have been reviewed by another contributor.

## References

- [Brown et al. — Language Models are Few-Shot Learners](https://arxiv.org/abs/2005.14165): autoregressive language modeling and evaluation under text conditioning.
- [Press and Wolf — Using the Output Embedding to Improve Language Models](https://arxiv.org/abs/1608.05859): output embeddings and input/output weight tying.
- [Petrov et al. — Language Model Tokenizers Introduce Unfairness Between Languages](https://arxiv.org/abs/2305.15425): empirical evidence about unequal encoding lengths and their consequences.
- [Hugging Face — Tokenizers](https://huggingface.co/learn/llm-course/chapter6/1): implementation details and segmentation algorithms to consult as needed.

Sources checked on 2026-11-15. Published findings motivate the experiment; they do not predetermine its result on another checkpoint or language pair.

## Completion criteria

- Explain the language-model objective and the representation path from text to vocabulary scores.
- Interpret the controlled bilingual result using the correct units and information-coverage comparison.
- Propose a follow-up intervention that distinguishes tokenization from another plausible source of the observed gap.

Personal completion is separate from the shared authoring checklist.

## Optional technical deep dive

Derive sequence likelihood and byte-normalized scoring, implement a tokenizer, inspect embedding geometry, or reproduce weight-tying gradients. Tensor tracing and mathematical derivations are optional extensions; the core assesses mechanism and experimental interpretation.

---

[← Previous: 00 · LLM systems map](../00-llm-systems-map/README.md) · [Next: 02 · Transformer architecture →](../02-transformer-architecture/README.md)
