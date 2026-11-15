# 10 · Inference Systems and Serving

[Home](../../README.md) · [LLM Roadmap](../README.md)

**Estimated core time:** 10 hours. Optional technical extensions are outside this budget.

**Prerequisites:** [Transformer Architecture](../02-transformer-architecture/README.md), [Decoding and Model Behavior](../05-decoding-model-behavior/README.md), [Model Evaluation](../07-evaluation/README.md).

**Status:** Content scaffold; unchecked items are awaiting authoring or review.

Checkboxes track shared content readiness.

## Learning objectives

After this module, learners will be able to:

- Explain the different compute, memory traffic, and scheduling demands of prefill and autoregressive decode.
- Relate KV cache growth, GQA, precision, and batching to capacity and latency constraints.
- Distinguish architectural changes, runtime optimizations, and workload effects in serving comparisons.
- Design a controlled measurement and justify a configuration from quality, latency, throughput, and memory evidence.

## Content checklist

- [ ] Map prefill, decode, and queueing to compute and memory traffic; explain why the dominant bottleneck depends on hardware and workload.
- [ ] Relate KV cache growth to sequence length, layer count, KV heads, and dtype; separate request state from weights, activations, and temporary workspaces.
- [ ] Compare MHA, MQA, and GQA as architectural choices; explain why changing the KV head count is not a generic serving toggle.
- [ ] Explain continuous batching, sequence scheduling, padding, and paged KV allocation through their effects on utilization and latency.
- [ ] Compare weight and KV cache quantization, memory savings, kernel support, and output quality; distinguish reduced storage from measured speedup.
- [ ] Define TTFT, inter-token latency, request latency, throughput, latency percentiles, and failure rates with explicit measurement boundaries.
- [ ] Specify workload distributions, arrival/concurrency conditions, warm-up, repetitions, stop rules, and quality checks for a fair benchmark.
- [ ] Prepare a vLLM profiling exercise that links configuration changes to exposed measurements and labels unavailable metrics or unresolved bottlenecks.

## Proposed lab

Measure how concurrency interacts with input length for one fixed model and serving runtime.

**Responsibilities:** The learner owns the hypothesis, controls, and interpretation; the implementation agent configures, profiles, and executes the benchmark.

### Experiment specification for an implementation agent

| Element | Specification |
| --- | --- |
| Question | How does increasing concurrency change throughput, TTFT, and KV memory for short versus long inputs? |
| Prediction | Throughput should rise before saturation; the long-input cohort should reach memory or latency constraints earlier. Treat this as a hypothesis to test. |
| Intervention | Compare at least two concurrency settings within each of two fixed input-length cohorts. |
| Controls | Hold model, tokenizer, hardware, runtime version, precision, decoding, output limits, request order, and repetition policy fixed within each comparison. |
| Execution | Record warm-up separately; capture actual input/output token counts, stopping reasons, failures, timings, and available memory/profile data for every condition. |

### Inspectable artifacts

- A configuration manifest with model architecture, KV head count, precision, hardware, runtime, and workload definitions.
- Per-request logs, actual token lengths, stopping reasons, error records, and available profiler or memory traces.
- Condition-level latency distributions, throughput, peak memory, and output quality checks with units and sample counts.
- A bottleneck assessment separating observed evidence, estimates, and alternative explanations.

### Acceptance criteria

- Compare conditions using the recorded workload and controls; explain deviations such as unequal generated lengths or early stopping.
- Account for failures and queueing, and distinguish TTFT from decode latency; client timing alone cannot establish a server-side bottleneck.
- Relate at least one observed tradeoff to batching, KV capacity, or runtime behavior without claiming architectural causality from unmatched models.
- A configuration choice is supported by both output quality and systems measurements; the main comparison can be rerun from the manifest.

## Self-check questions

1. Why can prefill optimization improve TTFT while barely affecting completion time for long outputs?

   **Hint:** Separate queueing, prefill, and repeated decode costs, then consider the workload's input/output ratio.

2. Why does a model with fewer KV heads not automatically provide a fair measurement of GQA's isolated speed benefit?

   **Hint:** Check weights, architecture, training, kernels, and hardware; distinguish capacity estimates from a controlled causal comparison.

3. How can a quantized configuration use less memory yet fail to improve latency?

   **Hint:** Consider kernel support, conversion overhead, batch size, the active bottleneck, and quality-preserving settings.

## Completion checklist

- [ ] Verify architecture, memory, and metric examples against their assumptions and primary sources.
- [ ] Run the experiment specification with pinned configurations and retain raw timings, errors, and profile artifacts.
- [ ] Add answer guidance and a rubric for bottleneck reasoning, measurement controls, and quality/performance tradeoffs.
- [ ] Document pitfalls including warm-up leakage, unmatched output lengths, hidden failures, cache effects, and unsupported causal claims.
- [ ] Check reference versions and ask another contributor to review the benchmark and its interpretation.

## Optional technical deep dive

- Derive KV storage and attention cost formulas; inspect tensor layouts, kernel fusion, and memory access patterns.
- Profile PagedAttention or other attention kernels and implement a targeted runtime optimization.
- Explore tensor/pipeline parallelism, prefill/decode disaggregation, and distributed serving under realistic arrival processes.

## References

- [PagedAttention / vLLM](https://arxiv.org/abs/2309.06180) — KV allocation, fragmentation, and serving design.
- [GQA](https://arxiv.org/abs/2305.13245) — grouped-query attention and its architectural quality/inference tradeoffs.
- [Official vLLM Documentation](https://docs.vllm.ai/en/latest/) — runtime configuration and measurement interfaces; pin the version used.

## Completion criteria

Explain the measured serving regime, defend a configuration choice, and identify which bottleneck claims the evidence does and does not support.
Submit the controlled comparison, its raw artifacts, and a reproducible configuration manifest.

**Previous:** [09 · Alignment and Reasoning](../09-alignment-reasoning/README.md) · **Next:** [11 · Retrieval Architectures and RAG](../11-retrieval-rag/README.md)
