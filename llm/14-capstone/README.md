# 14 · Capstone: Vietnamese QA over AI Documents

[Home](../../README.md) · [LLM Roadmap](../README.md)

**Estimated core time:** 16 hours, assuming reuse of the evaluation, serving, and RAG artifacts from modules 07, 10, and 11.

**Prerequisites:** [Model Evaluation](../07-evaluation/README.md), [Inference Systems and Serving](../10-inference-serving/README.md), [Retrieval Architectures and RAG](../11-retrieval-rag/README.md). Add [SFT and PEFT](../08-sft-peft/README.md) for adaptation or [Tool Use and Agent Architectures](../12-tool-use-agents/README.md) for an adaptive tool policy.

**Status:** Content scaffold; unchecked items are awaiting authoring or review.

Checkboxes track shared content readiness.

## Learning objectives

After this module, learners will be able to:

- Specify an integrated evidence-based QA architecture with explicit retrieval, context, generation, and serving contracts.
- Reuse a fixed benchmark to isolate failures and select one technically justified intervention.
- Evaluate the intervention's supported-answer quality, citation behavior, latency, and resource/cost tradeoffs.
- Defend an acceptance decision using a usable system, reproducible artifacts, and a clear account of remaining limitations.

## Content checklist

- [ ] Define the target Vietnamese AI-document workload, supported evidence types, abstention behavior, and operating constraints.
- [ ] Map reusable evaluation, serving, and RAG artifacts to a baseline architecture and identify only the missing integration work.
- [ ] Specify source/index versions, component contracts, context budgets, decoding settings, and traceable request/output identifiers.
- [ ] Preserve the development/test split and scoring protocol; group duplicates or paraphrases and keep test results out of intervention selection.
- [ ] Define baseline quality, citation, latency, error, and resource/cost measurements with component-level diagnostics where available.
- [ ] Build a failure decomposition linking retrieval misses, evidence selection, context loss, unsupported generation, and optional tool errors.
- [ ] Specify one intervention with a mechanism, affected error cohort, predicted tradeoff, fixed controls, and a falsifying outcome.
- [ ] Prepare an acceptance comparison covering overall and cohort results, operational usability, and unresolved confounders.
- [ ] Define the handoff: usable demo, configuration manifests, raw evidence, comparison report, and rerun instructions.

## Proposed lab

Integrate the existing artifacts into a usable Vietnamese QA system, then evaluate one intervention selected from development-set failures.

**Responsibilities:** The learner owns technical design, evidence, and the intervention decision; the implementation agent integrates, executes, and packages the system.

### Experiment specification for an implementation agent

| Element | Specification |
| --- | --- |
| Question | Can one targeted intervention improve supported-answer quality while satisfying the serving and cost constraints? |
| Prediction | State affected and unaffected cohorts before execution; for example, evidence-preserving context packing should help truncation failures more than candidate-pool misses. |
| Intervention | Implement the single selected change; retain the reusable baseline and record exactly which component or policy changed. |
| Controls | Freeze corpus/index snapshot, evaluation split, model, decoding, scoring, and relevant serving budgets except the declared intervention. |
| Execution | Integrate the baseline, verify the demo, run the controlled comparison, and export component traces, answers, citations, and systems measurements. |

### Inspectable artifacts

- A technical design and source/index manifest linking the reused modules, component contracts, and operating constraints.
- A usable demo with source-resolvable citations, insufficient-evidence behavior, and informative failure states.
- Baseline/modified configurations, raw predictions, retrieved and packed evidence, scores, error records, and latency/cost measurements.
- A decision report containing cohort analysis, verified examples, remaining confounders, and an independently usable rerun procedure.

### Acceptance criteria

- The baseline is usable on the specified workload; inspect representative correct, incorrect, unanswerable, and resource-limit cases.
- Choose the intervention from development evidence, then compare frozen systems on the same held-out test set and report sample counts.
- Test the stated mechanism against affected and unaffected cohorts; retain negative or inconclusive results and audit examples behind aggregate scores.
- The final decision accounts for supported-answer quality, citations, latency, and cost; another contributor can rerun the main evaluation from the handoff.

## Self-check questions

1. Which observation would falsify the proposed explanation for an intervention's apparent improvement?

   **Hint:** Identify the expected error cohort, an unaffected comparison cohort, and other components that may have changed.

2. How should an intervention be judged if overall accuracy is unchanged but citation support improves and tail latency worsens?

   **Hint:** Apply the workload's acceptance criteria, inspect cohort effects, and quantify the operational tradeoff.

3. What evidence would separate a retrieval regression from a serving or context-budget regression?

   **Hint:** Trace the same request through candidate retrieval, context packing, truncation, generation, timing, and failure records.

## Completion checklist

- [ ] Add a technical design and comparison example with explicit controls, source evidence, and clearly labeled measured results.
- [ ] Validate artifact reuse and rerun the integrated evaluation from the documented handoff.
- [ ] Write answer guidance and rubrics for technical design, causal limits, cohort analysis, and acceptance decisions.
- [ ] Document pitfalls including test-set tuning, uncontrolled component changes, citation mismatch, hidden retries, and incomplete resource accounting.
- [ ] Check sources and versions, and ask another contributor to review the demo and evidence against the acceptance criteria.

## Optional technical deep dive

- Add targeted adaptation, an adaptive tool policy, or a broader evaluation only when the observed failure modes justify it.
- Explore serving optimization, alternative retrieval architectures, or custom component implementations.
- Extend to production monitoring, changing corpora, distributed deployment, and reliability under sustained load.

## References

- [Retrieval-Augmented Generation](https://arxiv.org/abs/2005.11401) — retrieval-conditioned system design.
- [Official vLLM Documentation](https://docs.vllm.ai/en/latest/) — serving configuration and measurement interfaces.
- [EleutherAI Language Model Evaluation Harness](https://github.com/EleutherAI/lm-evaluation-harness) — reproducible evaluation structure; retain task-specific QA and citation scoring.

## Completion criteria

Deliver the usable system, its technical design, and a controlled comparison supporting an explicit acceptance or rejection of the intervention.
The evidence must connect component behavior to task quality and operating cost; an honest negative result is valid when the baseline and analysis meet the criteria.

**Previous:** [13 · Research Frontiers and Claim Assessment](../13-research-frontiers/README.md) · **End of roadmap:** [LLM Overview](../README.md) · [Home](../../README.md)
