# AI-101

Understand AI mechanisms, assess evidence, and design useful systems. This repository starts with **large language models (LLMs)** and uses English throughout.

The LLM curriculum is written for learners who already have **solid programming and machine-learning foundations**. It concentrates on what is specific to LLMs: representations, Transformer architecture, context behavior, training and scaling, decoding, adaptation, reasoning, evaluation, and system design.

Implementation agents can write code, prepare environments, and execute experiments. The learner owns the technical question, experimental controls, interpretation, and resulting design decision. Detailed mathematical derivations, tensor exercises, and implementation from scratch are optional extensions.

**Current scope:** 15 LLM submodules, approximately **160 hours of active study and experimental analysis**. Long machine runtimes and optional extensions are outside this estimate.

**Content status:** the repository contains the roadmap, detailed submodule outlines, experiment specifications, and contributor checklists. Full lessons and verified experiment artifacts are still being developed.

## Audience and assumed background

Learners should already be comfortable with:

- Programming, reading technical documentation, and working with software tools.
- Standard ML concepts: training objectives, optimization, generalization, overfitting, and data splits.
- Basic probability and vector representations at the level needed to interpret a technical explanation.
- Comparing experimental results and distinguishing a measurement from an unsupported claim.

The core begins with LLM-specific mechanisms. Introductory programming, generic ML tutorials, chatbot onboarding, and prompt-writing lessons are outside its scope.

## Start here

1. Review the [LLM systems map](llm/00-llm-systems-map/README.md) and identify the mechanisms you cannot yet explain.
2. Use the [full roadmap](llm/README.md) to choose the relevant modules and check their prerequisites.
3. Work through an experiment by stating a hypothesis, fixing the controls, and delegating implementation to an agent.
4. Inspect the artifacts, explain the result, and connect it to a model or system decision.
5. Reuse these artifacts in the [capstone](llm/14-capstone/README.md).

Skip material you can already demonstrate through the module's completion criteria. Time estimates are planning aids, not graduation requirements.

## Repository structure

| Path | Purpose |
| --- | --- |
| [README.md](README.md) | Audience, learning approach, repository organization, and contribution workflow. |
| [llm/README.md](llm/README.md) | Module sequence, prerequisites, estimated time, and competency checkpoints. |
| `llm/<number>-<topic>/README.md` | Learning objectives, contributor checklists, experiment specification, references, and completion criteria. |

Keep supporting explanations, notebooks, code, figures, and reports inside the relevant submodule. Add files when material exists and link them from its README.

## Division of work

| Work | Learner | Implementation agent |
| --- | --- | --- |
| Question and hypothesis | Identify the mechanism, prediction, and competing explanation. | Check feasibility and identify missing experimental details. |
| Experimental design | Choose interventions, controls, data, metrics, and resource limits. | Translate the specification into executable work. |
| Execution | Review material deviations from the design. | Prepare data and environments, implement, run, and record artifacts. |
| Interpretation | Inspect evidence, diagnose confounders, and state the limits of the conclusion. | Organize outputs, measurements, examples, and comparisons. |
| System decision | Choose an architecture, configuration, or next experiment. | Implement the selected change and repeat the agreed evaluation. |

Generated explanations do not establish how a model internally computed an answer. Use observable evidence and distinguish measurements, source-reported results, and hypotheses.

## Contribution workflow

**Checkboxes track shared content readiness.** Personal learning progress belongs in a learner's own notes or fork.

1. Choose an unchecked content item in a submodule.
2. Add the explanation, controlled experiment, worked analysis, or verification material.
3. Link supporting files and cite primary papers or official documentation.
4. Check the material against the stated assumptions and acceptance criteria.
5. Change `- [ ]` to `- [x]` only after the deliverable exists and has been verified.
6. Describe the change and verification in a commit or pull request.

Each submodule's checklist is the record of its development status. A title, placeholder, or reference link alone does not complete an authoring item.

## Contribution standards

- Assume the stated technical background and concentrate on LLM-specific mechanisms.
- Connect each mechanism to a testable prediction or consequential system choice.
- Use equations when they clarify an idea; place lengthy derivations and tensor programming in the optional section.
- Specify the experimental question, hypothesis, controls, artifacts, and acceptance criteria.
- Separate architecture effects, data effects, training effects, and inference effects where the evidence permits.
- Cite original research, author-provided material, or official documentation for technical claims.
- Preserve model/data/configuration versions, raw results, failures, and resource assumptions with executable artifacts.
- Clearly label illustrative examples, reviewed source results, and experiments that actually ran.
- Use English, Markdown, and relative links within the repository.

## Before submitting a contribution

Copy this checklist into a pull request when useful; leave the template unchanged here.

- [ ] The contribution addresses a specific LLM mechanism or system decision in its submodule.
- [ ] It respects the assumed background and avoids repeating beginner material.
- [ ] The experiment has explicit hypotheses, controls, inspectable artifacts, and acceptance criteria.
- [ ] Technical claims, links, examples, and reported execution status have been checked.
- [ ] Questions include answer guidance, and limitations follow from the available evidence.
- [ ] Only completed and verified content items are checked in the submodule README.

## What completion means

A learner can **explain a mechanism**, **predict the effect of a change**, **design a controlled test**, and **justify a model or system decision from evidence**. The implementation may be delegated; responsibility for the conclusion remains with the learner.

The curriculum was revised for this audience on **15 November 2026**. Check version-dependent documentation when adding executable instructions.
