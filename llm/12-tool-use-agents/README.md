# 12 · Tool Use and Agent Architectures

[Home](../../README.md) · [LLM Roadmap](../README.md)

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
- [ ] Analyze malformed calls, timeouts, duplicate execution, missing results, and inconsistent state as distinct failure mechanisms.
- [ ] Explain trust boundaries around tool outputs, retrieved content, and stored memory; include prompt injection and permission enforcement.
- [ ] Define traces of actions, state changes, results, and costs; distinguish emitted rationales from evidence about internal model computation.
- [ ] Explain fixed-workflow versus adaptive-policy comparisons using task-level outcomes, repeated trials, and explicit reliability criteria.

## References

- [ReAct](https://arxiv.org/abs/2210.03629) — interleaving model-generated actions with environment observations.
- [tau-bench](https://arxiv.org/abs/2406.12045) — task-state evaluation and consistency across repeated tool-agent interactions.

---

**Previous:** [11 · Retrieval Architectures and RAG](../11-retrieval-rag/README.md) · **Next:** [13 · Research Frontiers and Claim Assessment](../13-research-frontiers/README.md)
