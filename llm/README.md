# LLM Learning Roadmap

[AI-101 home](../README.md) · [LLM systems map](00-llm-systems-map/README.md)

A curriculum for learners with strong programming and ML foundations who want to understand **how LLMs work and how their mechanisms shape practical systems**.

The core covers representations, architecture, context, training, decoding, adaptation, reasoning, retrieval, and agents. Implementation can be delegated to an agent. The learner defines the experiment, interprets the evidence, and makes the technical decision.

**Scope:** 15 submodules and approximately **160 hours of active study and analysis**. Machine runtimes, infrastructure delays, and optional technical extensions are excluded.

The main architectural reference is the decoder-only autoregressive Transformer. Encoder-based models, encoder–decoder models, mixture-of-experts architectures, and multimodal variants appear where they clarify a mechanism or research direction.

**Content status:** these READMEs are detailed learning outlines and experiment specifications. Their checklists track the production of complete lessons, examples, and verified artifacts.

## Assumed background

- Comfortable programming and working with technical tools and documentation.
- Familiarity with standard ML training, optimization, generalization, and evaluation workflows.
- Working intuition for probabilities, vectors, and functions.
- Ability to read an experimental comparison and question its assumptions.

This roadmap does not repeat Python fundamentals, introductory ML, chatbot usage, or prompt-writing tutorials. Mathematical derivations and tensor implementation are available as optional depth when they answer a concrete question.

## Learning outcomes

By completing the core, learners should be able to:

- Explain autoregressive language modeling, tokenization effects, representations, and the route from context to output distributions.
- Trace information through a Transformer and connect architectural choices to context use and inference costs.
- Distinguish conditioning, in-context learning, parameter updates, retrieval, and application state.
- Interpret training and scaling evidence while separating effects of data, parameters, compute, and evaluation conditions.
- Explain how decoding, adaptation, preference optimization, and inference-time computation change behavior.
- Design controlled studies and recognize confounding, contamination, scoring problems, and unsupported mechanistic claims.
- Choose serving, retrieval, and agent architectures using measured quality, reliability, latency, and cost.
- Direct implementation work and defend the resulting conclusion using inspectable artifacts.

## How to study each mechanism

1. **State the mechanism:** identify what computation, objective, or system component is being examined.
2. **Predict a consequence:** specify an observable change and a plausible competing explanation.
3. **Design the comparison:** fix the relevant data, model, budget, and evaluation conditions.
4. **Delegate execution:** give an implementation agent the experiment specification and required artifacts.
5. **Inspect the evidence:** check configurations, raw outputs, measurements, and representative failures.
6. **Make the decision:** explain what the result supports, what it leaves unresolved, and what should change next.

Agent-authored code can reduce implementation effort. It does not remove the need to check whether the implemented comparison answers the intended question.

## Submodule layout

Prerequisites refer to concepts, not mandatory seat time. Skip a module when you can already satisfy its completion criteria. After the shared foundation, application branches can be studied according to the problem being solved.

| ID | Submodule | Hours | Main prerequisites | Main question or deliverable |
| --- | --- | ---: | --- | --- |
| 00 | [LLM systems map](00-llm-systems-map/README.md) | 2 | The assumed ML background | Locate the boundary between the model, training pipeline, inference procedure, and application. |
| 01 | [Language modeling and representations](01-language-modeling-representations/README.md) | 8 | 00 | Explain the modeling objective and how tokenization and representations affect behavior. |
| 02 | [Transformer architecture and information flow](02-transformer-architecture/README.md) | 12 | 01 | Trace causal information flow and connect attention, position, and block structure to model behavior. |
| 03 | [Context dynamics and in-context learning](03-context-and-in-context-learning/README.md) | 10 | 01–02 | Distinguish conditioning from learning through parameter updates and test effective context use. |
| 04 | [Training dynamics and scaling](04-training-dynamics-scaling/README.md) | 12 | 01–02 | Interpret learning curves and data/parameter/compute tradeoffs without overstating scaling evidence. |
| 05 | [Decoding, uncertainty and model behavior](05-decoding-model-behavior/README.md) | 10 | 01–03 | Study how decoding changes output distributions and why likelihood, confidence, and correctness differ. |
| 06 | [Data pipelines and pretraining design](06-data-pretraining/README.md) | 12 | 04 | Assess data mixtures, curation, contamination, and controlled data interventions. |
| 07 | [Evaluation and experimental design](07-evaluation/README.md) | 14 | 04–06 | Build an evaluation that can distinguish a useful change from scoring artifacts or confounding. |
| 08 | [Fine-tuning and parameter-efficient adaptation](08-sft-peft/README.md) | 12 | 04, 06–07 | Explain SFT targets and adapter mechanisms, then assess adaptation and preserved capabilities. |
| 09 | [Alignment, reasoning and inference-time compute](09-alignment-reasoning/README.md) | 12 | 05, 07–08 | Compare learning signals and reasoning procedures under explicit quality and compute budgets. |
| 10 | [Inference systems and serving](10-inference-serving/README.md) | 10 | 02, 05, 07 | Explain prefill, decode, KV caching, and serving tradeoffs using measured workloads. |
| 11 | [Retrieval architectures and RAG](11-retrieval-rag/README.md) | 12 | 03, 07 | Separate retrieval and generation failures and evaluate a justified retrieval intervention. |
| 12 | [Tool use and agent architectures](12-tool-use-agents/README.md) | 10 | 07, 11 | Analyze the model policy, orchestration, state, tool contracts, and workflow reliability. |
| 13 | [Research frontiers and claim assessment](13-research-frontiers/README.md) | 8 | 02, 04, 07; topic-specific additions | Assess an LLM research claim and design a discriminating follow-up study. |
| 14 | [Capstone project](14-capstone/README.md) | 16 | 07, 10–11; add 08 for adaptation and 12 for agents | Reuse prior artifacts to deliver a system and defend one measured design intervention. |
| | **Total** | **160** | | |

## Learning stages

| Stage | Modules | Focus |
| --- | --- | --- |
| A. Establish the LLM model | 00–02 | Systems boundaries, language modeling, representations, and Transformer computation. |
| B. Explain behavior and learning | 03–05 | Context, in-context learning, training/scaling, and decoding. |
| C. Establish trustworthy evidence | 06–07 | Data interventions, contamination, evaluation, and experimental validity. |
| D. Change model behavior | 08–09 | SFT, adapters, preference optimization, reasoning, and inference-time compute. |
| E. Design complete systems | 10–12 | Inference infrastructure, retrieval, and agent architectures. |
| F. Integrate and investigate | 13–14 | Research claims, targeted experiments, and a practical system. |

These stages organize the material; they do not postpone experimental work. Each mechanism module includes a controlled study or analysis of clearly attributed run artifacts.

## Four competency checkpoints

| Checkpoint | Evidence of understanding |
| --- | --- |
| After 03 | Explain the route from tokens through Transformer computation to an output distribution; distinguish context conditioning from parameter updates. |
| After 07 | Design and interpret a controlled comparison while identifying data, compute, decoding, and evaluation confounders. |
| After 09 | Explain how an adaptation or reasoning method changes the learning signal or inference procedure and evaluate its tradeoffs. |
| After 14 | Defend a complete system design, trace its reported results to evidence, and explain the limits of one intervention. |

Completion is based on explanation, prediction, experimental judgment, and technical decisions. Writing every implementation personally or reproducing long derivations is not required.

## Experiment contract

Each lab should state:

| Element | Required detail |
| --- | --- |
| Question and hypothesis | The mechanism under study, expected observation, and competing explanation. |
| Intervention and controls | What changes, what stays fixed, and what cannot be controlled or observed. |
| Execution specification | Data, model, configurations, resource limits, and the implementation agent's deliverables. |
| Evidence | Raw outputs, run records, measurements, examples, and provenance for reviewed artifacts. |
| Acceptance and interpretation | Checks that establish a valid comparison, permissible conclusions, and unresolved limitations. |

Use a bounded local model, an appropriate hosted system, or source-provided artifacts according to the question. A black-box API cannot support every claim about model internals; choose an observable setup or narrow the conclusion. Reviewing existing evidence is valid when explicitly identified, but must not be reported as a new execution.

## Core understanding and optional depth

The core keeps the mechanisms needed for sound technical decisions. It uses diagrams, concise equations where useful, controlled interventions, and inspectable results.

| Core understanding | Optional technical extension |
| --- | --- |
| What representations, attention, position, and residual paths do. | Tensor-shape drills, full matrix derivations, and Transformer implementation from scratch. |
| How objectives, data, budgets, and training dynamics shape a model. | Gradient derivations, optimizer implementation, distributed training, and large scaling reproductions. |
| How adapters, quantization, and preference objectives change behavior or resource needs. | Detailed LoRA/QLoRA mathematics and manual training-algorithm implementation. |
| How decoding, caching, batching, retrieval, and tools affect a system. | Kernel implementation, custom serving engines, and framework internals. |
| How evidence supports an architectural or deployment decision. | Advanced statistical derivations, large replication programs, and new-method research. |

Optional depth is outside the 160-hour estimate and does not block progress through the core. Familiarity with a formula is useful when it explains a mechanism; lengthy manipulation is not a learning goal by itself.

## Suggested pacing

| Schedule | Weekly effort | Approximate duration |
| --- | --- | --- |
| Alongside other work | 8–10 hours | 16–20 weeks. |
| Focused study | 12–15 hours | 11–14 weeks. |

These estimates include reading, designing studies, reviewing agent-produced artifacts, and explaining conclusions. They exclude long training runs. The 16-hour capstone assumes reuse of the evaluation and system artifacts from earlier modules.

Experienced learners may move directly to a branch after demonstrating its prerequisites. For practical system work, modules 10–12 can follow the shared foundation and evaluation without first completing every adaptation topic.

## Evidence and reproducibility

- Record model, tokenizer, data, code, and configuration versions with executable artifacts.
- Preserve raw predictions and measurement units, along with failures and resource assumptions.
- Keep decisions based on development evidence separate from final held-out comparisons.
- Distinguish measurement, author-reported result, illustration, and hypothesis.
- Do not use generated rationales or attention displays alone as proof of a model's internal reasoning.
- State what is observable when using a hosted model and avoid guessing hidden implementation details.
- Keep supporting files in their submodule and provide retrieval instructions for large datasets or weights.

## Contributor checklist conventions

Checkboxes record **shared content readiness**, not individual learning progress. Mark an item only after its explanation, experiment, or verification material exists and has been checked. Follow the [root contribution workflow](../README.md).

The roadmap table provides navigation. Each submodule maintains its own authoring checklist and separate learner completion criteria.

## Using references

The primary papers linked in each submodule establish the mechanisms and empirical claims. Read the parts needed to answer that module's question; an entire external course is not a prerequisite.

| Resource | Role |
| --- | --- |
| [Stanford CS336](https://cs336.stanford.edu/) | Selected LLM architecture, data, scaling, systems, and alignment material; from-scratch assignments are optional. |
| [EleutherAI Evaluation Harness](https://github.com/EleutherAI/lm-evaluation-harness) | Evaluation implementation and task definitions to inspect and adapt through an agent. |
| [vLLM documentation](https://docs.vllm.ai/en/latest/) | Serving concepts, configuration behavior, and measurement references for the version in use. |
| [Raschka — LLMs from Scratch](https://github.com/rasbt/LLMs-from-scratch) | Optional implementation detail when a mechanism benefits from examining code. |

Roadmap revised **15 November 2026**. Recheck version-dependent instructions when adding executable material.
