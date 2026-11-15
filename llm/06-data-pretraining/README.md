# 06 · Data pipelines and pretraining design

[Home](../../README.md) · [LLM roadmap](../README.md)

## Learning objectives

- Analyze curation, deduplication, mixture proportions, and sampling as interventions on the training distribution.
- Explain how data comparisons account for token budgets, repetition, provenance, and contamination.
- Interpret dataset audits and model evaluations as different kinds of evidence.
- Decide which data intervention to test next and state the limits of transferring results across model scales or domains.

## Content checklist

- [ ] Map an operational pipeline from source collection and extraction to filtering, deduplication, mixing, tokenization, and versioned training shards.
- [ ] Analyze quality filters as distribution-changing decisions, including domain/language coverage and useful examples removed by mistake.
- [ ] Compare exact, near-duplicate, and semantic overlap concepts; explain the limits of practical overlap detectors.
- [ ] Explain data mixtures, sampling proportions, repeated exposure, and why equal document counts do not imply equal training conditions.
- [ ] Examine tokenizer choice, document boundaries, packing, context length, and the distinction between available and consumed tokens.
- [ ] Define provenance, usage-rights records, contamination checks, and grouping rules for related sources and evaluation examples.
- [ ] Explain matched-budget data comparisons, distinguishing controlled quantities from distribution changes that are part of the intervention.
- [ ] Interpret domain-specific loss, downstream capability, and regression results without substituting a data-cleanliness metric for model evidence.
- [ ] Use FineWeb and DoReMi as case studies in empirical data design, including the limits of proxy models and extrapolation.

## References

- [FineWeb — technical report by the authors](https://huggingfacefw-blogpost-fineweb-v1.static.hf.space/index.html): empirical filtering and deduplication decisions and their tradeoffs.
- [Xie et al. — DoReMi](https://arxiv.org/abs/2305.10429): data-mixture optimization through a proxy model and subsequent training experiments.
- [Stanford CS336](https://cs336.stanford.edu/): data, scaling, and pretraining systems; implementation assignments are optional extensions.

References checked on **2026-11-15**.

---

**Previous:** [05 · Decoding, uncertainty and model behavior](../05-decoding-model-behavior/README.md) · **Next:** [07 · Evaluation and experimental design](../07-evaluation/README.md)
