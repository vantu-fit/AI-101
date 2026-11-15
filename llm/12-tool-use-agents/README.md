# 12 · Tool Use and Agent Architectures

[Home](../../README.md) · [LLM Roadmap](../README.md)

**Estimated core time:** 10 hours. Optional technical extensions are outside this budget.

**Prerequisites:** [Model Evaluation](../07-evaluation/README.md), [Retrieval Architectures and RAG](../11-retrieval-rag/README.md). Add [Inference Systems and Serving](../10-inference-serving/README.md) when serving models locally.

**Status:** Content scaffold; unchecked items are awaiting authoring or review.

Checkboxes track shared content readiness.

## Learning objectives

After this module, learners will be able to:

- Separate the model's action-selection policy from orchestration, execution, application state, and authority.
- Design context and memory boundaries, tool contracts, and termination/reliability budgets.
- Diagnose policy, state, tool, and recovery failures from observable action traces and outcomes.
- Compare an adaptive agent architecture with a fixed workflow under matched resource constraints.

## Content checklist

- [ ] Distinguish model policy from the orchestrator's state transitions, validation, tool dispatch, and stopping rules.
- [ ] Compare model-visible context, persisted memory, and authoritative application state; cover stale observations and lossy context compaction.
- [ ] Specify tool contracts with schemas, preconditions, authorization, error semantics, and idempotency; separate valid syntax from valid actions.
- [ ] Analyze budgets for model calls, tool calls, tokens, retries, and deadlines, including how failures accumulate across dependent steps.
- [ ] Develop fault cases for malformed calls, timeouts, duplicate execution, missing results, and inconsistent state.
- [ ] Explain trust boundaries around tool outputs, retrieved content, and stored memory; include prompt injection and permission enforcement.
- [ ] Define traces of actions, state changes, results, and costs; distinguish emitted rationales from evidence about internal model computation.
- [ ] Design a fixed-workflow versus adaptive-policy comparison with task-level outcomes, repeated trials, and explicit reliability criteria.

## Proposed lab

Compare fixed retrieval orchestration with adaptive search/read decisions on single-source and multi-source document questions.

**Responsibilities:** The learner defines architecture, contracts, budgets, and hypotheses; the implementation agent builds both systems and executes normal and fault-injection trials.

### Experiment specification for an implementation agent

| Element | Specification |
| --- | --- |
| Question | Does adaptive tool selection improve evidence-complete answers enough to justify its extra model calls and failure opportunities? |
| Prediction | Benefits should concentrate on multi-source cases; single-source cases may gain little while incurring additional latency and cost. |
| Intervention | Compare a fixed retrieve/read workflow with a bounded adaptive policy using the same read-only search and fetch tools. |
| Controls | Match task sets, model version, corpus, tool interfaces, scoring, and maximum tool/token/time budgets; report actual consumption separately. |
| Execution | Repeat trials under normal operation and specified timeout, missing-result, injected-instruction, and permission-denial conditions; retain all outcomes. |

### Inspectable artifacts

- Architecture/state diagrams, tool contracts, memory/context rules, and resource/retry limits.
- Trial manifests and observable action traces containing tool arguments, results, state changes, errors, and stopping reasons.
- Task outcomes stratified by question type and fault condition, with repeated-trial consistency and actual resource consumption.
- A failure attribution report separating policy choices, orchestration defects, tool failures, and inadequate evidence.

### Acceptance criteria

- The comparison uses matched limits and identifies actual cost differences; interpret results as evidence about the evaluated architecture and policy.
- Verify contracts, permissions, termination, and retry behavior from observed normal and failure cases.
- Score evidence-supported task outcomes and consistency across trials; plausible action sequences or rationales alone do not establish success.
- Explain which task cohort benefits and which failure modes remain; passing the included injection cases does not establish general robustness.

## Self-check questions

1. Which failures can be corrected by changing the model policy, and which require orchestration or tool-contract changes?

   **Hint:** Separate action selection from state integrity, authorization, execution semantics, and recovery.

2. How can persisted memory degrade an agent even when every stored entry was originally correct?

   **Hint:** Consider stale facts, changed authority, retrieval of irrelevant history, and context-budget competition.

3. Why is equal maximum call budget insufficient to establish that two agent architectures have equal cost or reliability?

   **Hint:** Inspect actual calls, token lengths, retries, dependency chains, and repeated-trial outcomes.

## Completion checklist

- [ ] Add architectural examples that separate policy, context, memory, state, contracts, and authority.
- [ ] Execute the experiment specification and fault cases with recorded configurations, traces, and repeated outcomes.
- [ ] Write answer guidance and rubrics for architecture comparison, failure attribution, and resource accounting.
- [ ] Document pitfalls including hidden retries, repeated side effects, stale memory, leaked secrets, and rationale-based success judgments.
- [ ] Check primary references and ask another contributor to review state transitions and fault handling.

## Optional technical deep dive

- Study durable execution, concurrent branches, transactional tool operations, and formal state-machine properties.
- Explore learned tool policies, planning/search, memory selection, and evaluation under distribution shifts.
- Extend adversarial evaluation, tool isolation, and reliability analysis to systems with external side effects.

## References

- [ReAct](https://arxiv.org/abs/2210.03629) — interleaving model-generated actions with environment observations.
- [tau-bench](https://arxiv.org/abs/2406.12045) — task-state evaluation and consistency across repeated tool-agent interactions.

## Completion criteria

Defend the policy/orchestration split, explain observed state and tool failures, and compare architectures at explicit resource and reliability budgets.
Deliver a reproducible outcome comparison supported by action traces and fault-injection evidence.

**Previous:** [11 · Retrieval Architectures and RAG](../11-retrieval-rag/README.md) · **Next:** [13 · Research Frontiers and Claim Assessment](../13-research-frontiers/README.md)
