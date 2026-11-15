# 00 · LLM systems map

[Home](../../README.md) · [LLM roadmap](../README.md)

## Learning objectives

- Map the interfaces connecting corpus construction, tokenization, model objectives, checkpoints, post-training, inference, and downstream systems.
- Distinguish changes to learned parameters from changes to conditioning, serialization, decoding, and external state.
- Identify which subsystem can explain an observed quality, latency, or memory change.
- Convert a broad LLM research question into a specific intervention and an observable consequence.

## Content checklist

- [ ] Define the lifecycle and artifact dependencies of a language model, from data mixture to deployed checkpoint.
- [ ] Map representation, objective, architecture, post-training, inference, and retrieval/tool interfaces.
- [ ] Distinguish checkpoint identity, tokenizer revision, chat serialization, runtime configuration, and application state.
- [ ] Explain which interfaces expose tokens, logits, generated text, cached state, and resource measurements.
- [ ] Contrast parameter adaptation, in-context conditioning, decoding changes, and external retrieval as interventions.
- [ ] Map research questions to mechanisms: representation efficiency, context use, data allocation, alignment, and serving constraints.
- [ ] Identify observations that require instrumented model access versus those available from a hosted endpoint.
- [ ] Explain how interface-equivalence reasoning reveals wrapper behavior that can be mistaken for a model change.
- [ ] Define the assumptions and evidence boundaries carried into the later modules.

## References

- [Meta — The Llama 3 Herd of Models](https://arxiv.org/abs/2407.21783): a technical report connecting pretraining, post-training, model variants, and evaluation.
- [Hugging Face — Chat templates](https://huggingface.co/docs/transformers/main/en/chat_templating): official documentation for the serialization boundary between message objects and model token sequences.
- [Stanford CS336 — Language Modeling from Scratch](https://cs336.stanford.edu/): a reference map spanning data, architecture, training, systems, and alignment.

Sources checked on 2026-11-15. Implementation details depend on the library and artifact revisions; moving documentation may describe a different version.

---

[← LLM roadmap](../README.md) · [Next: 01 · Language modeling and representations →](../01-language-modeling-representations/README.md)
