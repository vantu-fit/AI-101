# LLM Learning Roadmap

[AI-101 home](../README.md)

**Six stages, three practical outputs.** The goal is to explain how an LLM learns and generates text, understand a small working model, evaluate an adaptation, and build a useful application.

The path assumes solid programming and machine-learning foundations. Stage 1 is a brief refresher; fill gaps in mathematics or PyTorch as needed. Implementation may be delegated to an agent, while explanation, experimental judgment, and interpretation remain with the learner.

## The six-stage path

Follow these stages in order, skipping a stage when you can already demonstrate its outcome. Use the numbered topic folders for selected explanations and examples; their full checklists and advanced experiments are not requirements for the core path.

| Stage | Essential scope | Evidence that you understand |
| --- | --- | --- |
| **1. How models learn** | Parameters, a training objective, gradient updates, training versus inference, and overfitting. Establish train/validation/test separation from the first experiment. | Explain what training changes inside a model and why a lower training loss can coexist with worse results on new examples. |
| **2. How an LLM works** | Tokens and embeddings; attention, position, feed-forward layers, residual connections and normalization; the next-token distribution and sampling. | Trace one input through a Transformer to a generated token. Distinguish using context from updating model parameters. |
| **3. Build and explain a small GPT** | Combine a tokenizer, decoder-only Transformer, training loop, checkpoint, and generation loop in a bounded experiment. | Produce the small-GPT artifact below, explain its components and learning curves, and diagnose one implementation or training failure. |
| **4. Data and evaluation** | Data quality, filtering, duplicates and contamination; baselines, task metrics, held-out evaluation, and error analysis. | Fix an evaluation set and scoring procedure, inspect per-example failures, and identify a misleading comparison. |
| **5. Improve a pretrained model** | Pretraining versus fine-tuning; supervised fine-tuning (SFT), learning from example responses; LoRA, adapting a small set of trainable parameters; a brief overview of learning from feedback. | Compare a baseline and adapted model on held-out examples. Explain gains, regressions, and the limits of the evidence. |
| **6. Build an application** | Inference latency and memory; context assembly; retrieval-augmented generation (RAG), retrieving documents to support an answer. | Deliver a document QA application with inspectable evidence, cited answers, and an evaluation that separates retrieval and generation errors. |

Evaluation begins in stage 1 and becomes systematic in stage 4, before fine-tuning. Stage 3 uses a small model to expose the mechanism; stage 5 uses a pretrained model to study useful adaptation.

## Three practical outputs

These are project specifications, not reports of completed runs. Keep each project small enough to inspect, and reuse its artifacts in later stages.

### 1. Small GPT

Build or direct the implementation of a small decoder-only language model on a bounded text dataset. A reference implementation is allowed; explain any reused components. The [Raschka repository](https://github.com/rasbt/LLMs-from-scratch) is the main implementation reference.

**Produce:** a runnable configuration, data split, checkpoint, training/validation curves, and generated examples.

**Completion:** explain the input and shifted targets, causal masking, the training loss, and the generation loop. Investigate one failure, such as misaligned targets or an excessive learning rate, and show evidence for the diagnosis. Writing every component personally is optional.

Use [architecture](02-transformer-architecture/README.md) and [training dynamics](04-training-dynamics-scaling/README.md) for help. Their full scaling experiments are optional; one bounded model is sufficient for this project.

### 2. Fine-tuning comparison

Choose one task and a manageable pretrained model. Establish its baseline using the evaluation designed in stage 4, then run a small SFT experiment using full fine-tuning or LoRA.

**Produce:** the data and configuration, saved adaptation, per-example baseline and adapted outputs, and a short comparison report.

**Completion:** use the same held-out examples and scoring procedure for both models, check for leakage, inspect regressions, and explain what changed. A well-diagnosed negative result is valid; an improved score is not assumed.

Use [evaluation](07-evaluation/README.md) and [fine-tuning](08-sft-peft/README.md) as needed. Choose a model and configuration that fit the available memory and compute budget.

### 3. Document question answering

Build a small application that retrieves relevant passages and uses them to answer questions with source citations. Reuse the evaluation workflow and an appropriate pretrained model; the fine-tuned model is optional if it does not help this task.

**Produce:** an inspectable retrieval-to-answer pipeline, a small question set, retrieved passages, cited answers, and basic latency measurements.

**Completion:** compare with a no-retrieval baseline, check answer correctness and citation support, separate missing-evidence failures from poor use of retrieved evidence, and test questions the documents cannot answer. Explain the chosen behavior when evidence is insufficient.

Use [RAG](11-retrieval-rag/README.md) and [serving](10-inference-serving/README.md) for help. The full [capstone specification](14-capstone/README.md) is an optional extension, not a fourth required project.

## How to study

For each concept: **start with a concrete question, form an intuitive explanation, use only the mathematics needed, inspect a small implementation or experiment, and explain the result in your own words.**

Move on when you can explain the mechanism, predict one effect of changing it, and diagnose a failure. An agent may write and run the code; you must check that the comparison answers your question. Reviewing source-provided results can support learning, but label them as reviewed evidence rather than your own execution.

Plan for approximately **12–16 weeks at 8–10 hours per week**. This is a planning window, not a fixed total or a guarantee. It covers the bounded core projects and active study, excluding long machine runtimes, extensive prerequisite repair, and optional extensions.

## Optional topic library

Open a topic when it helps with the current stage. The numbered folders retain their deeper outlines, local prerequisites, and contributor checklists. Those prerequisites apply to the full topic; they do not turn all 15 folders into a required sequence.

<details>
<summary>Show supporting topics and later specializations</summary>

| Use | Supporting topics |
| --- | --- |
| Stages 1 and 3: model learning | [00 Systems map](00-llm-systems-map/README.md); selected sections of [04 Training dynamics and scaling](04-training-dynamics-scaling/README.md). |
| Stages 2 and 3: model computation | [01 Language modeling and representations](01-language-modeling-representations/README.md); [02 Transformer architecture](02-transformer-architecture/README.md); [05 Decoding and model behavior](05-decoding-model-behavior/README.md). |
| Stage 4: trustworthy comparisons | [06 Data and pretraining](06-data-pretraining/README.md); [07 Evaluation](07-evaluation/README.md). |
| Stage 5: adaptation | [08 SFT and parameter-efficient adaptation](08-sft-peft/README.md); the overview in [09 Alignment and reasoning](09-alignment-reasoning/README.md). |
| Stage 6: practical systems | [10 Inference and serving](10-inference-serving/README.md); [11 Retrieval and RAG](11-retrieval-rag/README.md). |
| Later specializations | [03 Context and in-context learning](03-context-and-in-context-learning/README.md); advanced [09 Alignment and reasoning](09-alignment-reasoning/README.md); [12 Tool use and agents](12-tool-use-agents/README.md); [13 Research frontiers](13-research-frontiers/README.md); [14 Extended capstone](14-capstone/README.md). |

Detailed scaling studies, mixture-of-experts architectures, advanced reinforcement learning, multi-GPU training, kernel work, and lengthy derivations are optional follow-up topics.

</details>

## References and content status

Use [Raschka's LLMs from Scratch](https://github.com/rasbt/LLMs-from-scratch) as the main implementation reference. Consult the primary sources linked inside a topic when a question needs more depth; completing an entire external course is not required.

The repository contains the roadmap, topic outlines, and project specifications. Full lessons and verified project artifacts remain under development. **Checkboxes record shared content readiness, not personal learning progress.** Follow the [contribution workflow](../README.md#contribution-workflow), and mark content complete only after it exists and has been verified.

Updated **15 November 2026**. Record model, tokenizer, dataset, code, and configuration versions with each experiment, and recheck version-dependent documentation when implementing it.
