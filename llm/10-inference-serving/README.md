# 10 · Inference Systems and Serving

[Home](../../README.md) · [LLM Roadmap](../README.md)

## Learning objectives

After this module, learners will be able to:

- Explain the different compute, memory traffic, and scheduling demands of prefill and autoregressive decode.
- Relate KV cache growth, GQA, precision, and batching to capacity and latency constraints.
- Distinguish architectural changes, runtime optimizations, and workload effects in serving comparisons.
- Explain controlled serving measurements and justify a configuration from quality, latency, throughput, and memory evidence.

## Content checklist

- [ ] Map prefill, decode, and queueing to compute and memory traffic; explain why the dominant bottleneck depends on hardware and workload.
- [ ] Relate KV cache growth to sequence length, layer count, KV heads, and dtype; separate request state from weights, activations, and temporary workspaces.
- [ ] Compare MHA, MQA, and GQA as architectural choices; explain why changing the KV head count is not a generic serving toggle.
- [ ] Explain continuous batching, sequence scheduling, padding, and paged KV allocation through their effects on utilization and latency.
- [ ] Compare weight and KV cache quantization, memory savings, kernel support, and output quality; distinguish reduced storage from measured speedup.
- [ ] Define TTFT, inter-token latency, request latency, throughput, latency percentiles, and failure rates with explicit measurement boundaries.
- [ ] Specify workload distributions, arrival/concurrency conditions, warm-up, repetitions, stop rules, and quality checks for a fair benchmark.
- [ ] Explain how vLLM links configuration choices to exposed performance measurements, including unavailable metrics and unresolved bottlenecks.

## References

- [PagedAttention / vLLM](https://arxiv.org/abs/2309.06180) — KV allocation, fragmentation, and serving design.
- [GQA](https://arxiv.org/abs/2305.13245) — grouped-query attention and its architectural quality/inference tradeoffs.
- [Official vLLM Documentation](https://docs.vllm.ai/en/latest/) — runtime configuration and measurement interfaces; pin the version used.

---

**Previous:** [09 · Alignment and Reasoning](../09-alignment-reasoning/README.md) · **Next:** [11 · Retrieval Architectures and RAG](../11-retrieval-rag/README.md)
