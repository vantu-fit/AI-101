# LLM Learning Roadmap

[AI-101 home](../README.md)

A concise path through **six stages**. It assumes solid programming and machine-learning foundations; stage 1 is a short refresher.

## Learning objectives

- Explain how training changes a model and how inference generates tokens.
- Trace the roles of tokenization, embeddings, Transformer blocks, and output probabilities.
- Understand a small GPT's architecture, training objective, and generation process.
- Assess data quality, evaluation validity, and the effects of model adaptation.
- Explain inference and retrieval choices in an LLM application.

## Content checklist

Study the stages in order. Checkboxes record shared learning-content readiness, not completion of labs or personal progress.

### 1. How models learn

- [ ] Parameters, training objectives, gradient updates, training versus inference, and overfitting.
- [ ] Train/validation/test separation and the difference between lower training loss and better generalization.

### 2. How an LLM works

- [ ] Tokens, embeddings, attention, positional information, feed-forward layers, residual connections, and normalization.
- [ ] Next-token prediction, sampling, and the difference between using context and updating parameters.

### 3. How a small GPT fits together

- [ ] The relationship between tokenizer, decoder blocks, output head, training loop, checkpoint, and generation loop.
- [ ] Shifted targets, causal masking, training/validation curves, and common causes of incorrect behavior.

### 4. Data and evaluation

- [ ] Data quality, filtering, mixtures, duplicates, contamination, and held-out data.
- [ ] Baselines, task metrics, error analysis, and the conditions needed for a valid comparison.

### 5. Adapting a pretrained model

- [ ] Pretraining versus supervised fine-tuning (SFT); instruction data, chat templates, and training targets.
- [ ] Full fine-tuning, LoRA, retained capabilities, and an overview of learning from feedback.

### 6. Inference and LLM applications

- [ ] Prefill, decoding, KV caching, memory use, latency, and context assembly.
- [ ] Retrieval-augmented generation (RAG), supporting evidence, citations, and retrieval versus generation errors.

<details>
<summary>Supporting topic index</summary>

| Stage | Supporting topics |
| --- | --- |
| 1. Model learning | [00 Systems map](00-llm-systems-map/README.md); [04 Training dynamics and scaling](04-training-dynamics-scaling/README.md). |
| 2. LLM mechanisms | [01 Language modeling and representations](01-language-modeling-representations/README.md); [02 Transformer architecture](02-transformer-architecture/README.md); [05 Decoding and model behavior](05-decoding-model-behavior/README.md). |
| 3. Small GPT | Selected architecture and training content from [02](02-transformer-architecture/README.md) and [04](04-training-dynamics-scaling/README.md). |
| 4. Data and evaluation | [06 Data and pretraining](06-data-pretraining/README.md); [07 Evaluation](07-evaluation/README.md). |
| 5. Adaptation | [08 Fine-tuning and parameter-efficient adaptation](08-sft-peft/README.md); the overview in [09 Alignment and reasoning](09-alignment-reasoning/README.md). |
| 6. Applications | [10 Inference and serving](10-inference-serving/README.md); [11 Retrieval and RAG](11-retrieval-rag/README.md). |
| Optional depth | [03 Context and in-context learning](03-context-and-in-context-learning/README.md); advanced [09 Alignment and reasoning](09-alignment-reasoning/README.md); [12 Tool use and agents](12-tool-use-agents/README.md); [13 Research frontiers](13-research-frontiers/README.md); [14 Integrated Vietnamese QA](14-capstone/README.md). |

</details>

The numbered folders provide optional detail. Their numbering and previous/next links organize the topic library; they do not add stages to the core path.

## References

- [Sebastian Raschka — LLMs from Scratch](https://github.com/rasbt/LLMs-from-scratch): the main reference for understanding how a small GPT fits together.
- Primary papers and official documentation are listed in each linked topic's **References** section.
