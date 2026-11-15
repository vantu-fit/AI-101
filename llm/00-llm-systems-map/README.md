# 00 · LLM systems map

[Home](../../README.md) · [LLM roadmap](../README.md)

**Estimated core time:** 2 hours; environment setup and machine runtime are separate.

**Prerequisites:** Strong programming skills, Python, established ML training/evaluation practice, and basic probability. This module starts at the LLM system boundary.

**Status:** Content outline; unchecked items track shared authoring and review work.

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
- [ ] Build an interface-equivalence case study showing how wrapper behavior can be mistaken for a model change.
- [ ] Define the assumptions and evidence boundaries carried into the later modules.

## Proposed lab

**Experimental question:** Can two inference interfaces produce different answers while using exactly the same checkpoint, and which interface difference explains the discrepancy?

**Hypothesis:** Different message serialization can change the token sequence and conditional distribution. After equalizing token IDs, position/mask handling, and inference settings in the same runtime, the two paths should agree within a declared numerical tolerance.

Use one inspectable instruction-tuned checkpoint through a direct completion path and a chat-serialization path. First record their actual inputs. Then run an equivalence condition that supplies identical serialized token IDs through both paths; this is an interface test, not a prompt-quality competition.

**Controls:** Checkpoint/tokenizer revisions, precision, runtime/backend, evaluation mode, position IDs, attention masks, decoding settings, and stopping rules. Record any wrapper behavior that cannot be equalized.

**Learner role:** Specify the system boundary, predict the source of divergence, and interpret the equivalence result. **Agent role:** Instrument both paths, run the comparison, and export the input/output evidence.

**Artifacts:** A lifecycle/interface diagram; checkpoint and runtime manifests; serialized text and token IDs; selected logits or log probabilities; generated outputs; a table locating each observed difference.

**Acceptance criteria:**

- The system map distinguishes training artifacts from runtime and application state.
- Any claimed equivalence is supported by matching inputs and settings, not merely similar visible prompts.
- Remaining discrepancies are investigated at the appropriate interface rather than attributed to new model capability.
- The report identifies one follow-up research question and the intervention needed to test it.

**Experiment specification for an implementation agent:**

```text
Instrument direct-completion and chat-serialization paths for one fixed checkpoint and runtime.
Export their serialized text, token IDs, masks/positions, settings, and selected outputs.
Run the initial comparison, then an equivalence condition with identical token inputs and settings.
Report numeric agreement and unresolved interface differences; preserve all artifact revisions.
Return the interface map and evidence needed to localize the discrepancy.
```

This is an experiment specification; no execution results are claimed here.

## Self-check questions

1. Which artifacts must be fixed before a result can reasonably be attributed to a checkpoint change?
2. How do parameter updates, a longer context, and an external retrieval step intervene at different system boundaries?
3. If two endpoints return different text for the same visible request, what can and cannot be inferred about their underlying models?

**Answer guidance:**

- Question 1: Include tokenizer/serialization, runtime precision and kernels, conditioning, decoding, and stopping behavior; checkpoint identity alone is insufficient.
- Question 2: They change learned parameters, the conditional input, and the process that constructs that input, respectively; application state may add further differences.
- Question 3: Different output establishes an observable system difference. Locating it requires input and runtime evidence, especially with hidden endpoint behavior.

## Completion checklist

- [ ] A systems diagram links each interface to its artifacts, observables, and likely failure modes.
- [ ] The lab includes an instrumented comparison and a clearly specified equivalence condition.
- [ ] Acceptance criteria separate interface effects from checkpoint and capability claims.
- [ ] The case study covers serialization, hidden defaults, stopping rules, and numerical differences.
- [ ] Primary sources and all reported observations have been checked by another contributor.

## References

- [Meta — The Llama 3 Herd of Models](https://arxiv.org/abs/2407.21783): a technical report connecting pretraining, post-training, model variants, and evaluation.
- [Hugging Face — Chat templates](https://huggingface.co/docs/transformers/main/en/chat_templating): official documentation for the serialization boundary between message objects and model token sequences.
- [Stanford CS336 — Language Modeling from Scratch](https://cs336.stanford.edu/): a reference map spanning data, architecture, training, systems, and alignment.

Sources checked on 2026-11-15. Pin the actual library and artifact revisions used in the lab; a moving documentation branch is not an execution specification.

## Completion criteria

- Explain the lifecycle and the interfaces responsible for a chosen observed behavior.
- Localize an interface discrepancy using the controlled comparison.
- Formulate a mechanism-level research question with a testable intervention and a bounded conclusion.

Personal completion is separate from the shared authoring checklist.

## Optional technical deep dive

Trace a runtime's request-to-token path, inspect checkpoint loading and cache management code, or reproduce serialization behavior directly. Detailed code tracing is optional; basic programming and ML foundations are assumed throughout the course.

---

[← LLM roadmap](../README.md) · [Next: 01 · Language modeling and representations →](../01-language-modeling-representations/README.md)
