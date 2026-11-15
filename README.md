# AI-101

Understand how AI works, starting with **large language models (LLMs)**. This repository uses English throughout.

**Start with the [six-stage LLM roadmap](llm/README.md).** Learn how models learn, understand LLM internals, build a small GPT, evaluate data and results, adapt a pretrained model, and build a document question-answering application.

The core has **six stages and three practical outputs**. The 15 numbered topic folders are a supporting reference library; completing every folder or advanced experiment is not required.

## What you will produce

1. **A small GPT:** explain its training and generation, inspect its results, and diagnose a basic failure.
2. **A fine-tuned model with a comparison report:** evaluate the baseline and adapted model on held-out data, including regressions.
3. **A document QA application:** retrieve evidence, answer with citations, and distinguish retrieval failures from answer failures.

See the [project briefs and completion criteria](llm/README.md#three-practical-outputs).

## Background and learning approach

The path assumes solid programming and machine-learning foundations. Stage 1 is a short diagnostic and refresher. Review mathematics or PyTorch only when a gap blocks the next explanation or experiment.

Implementation agents may prepare environments, write code, and execute experiments. The learner defines the question and controls, inspects the evidence, explains failures, and makes the technical decision. Detailed derivations and writing every component from scratch are optional.

Plan for approximately **12–16 weeks at 8–10 hours per week**, adjusted to your starting point. Long machine runtimes and optional study are outside this estimate. Advance when you meet a stage's completion criteria.

**Content status:** the repository contains a learning plan, topic outlines, and experiment specifications. Complete lessons and verified project artifacts are still being developed.

## Repository structure

| Path | Purpose |
| --- | --- |
| [llm/README.md](llm/README.md) | The main six-stage path, three project briefs, and optional reading map. |
| `llm/<number>-<topic>/README.md` | Supporting explanations to develop, experiment specifications, primary references, and contributor checklists. |

Keep notes, notebooks, code, figures, and reports in the relevant topic folder and link them from its README. Use the roadmap to choose what to study; the folders' numbering and previous/next links organize the reference library.

## Contribution workflow

**Checkboxes track shared content readiness.** Personal learning progress belongs in a learner's own notes or fork.

1. Choose an unchecked content item in a submodule.
2. Add the explanation, controlled experiment, worked analysis, or verification material.
3. Link supporting files and cite primary papers or official documentation.
4. Check the material against the stated assumptions and acceptance criteria.
5. Change `- [ ]` to `- [x]` only after the deliverable exists and has been verified.
6. Describe the change and verification in a commit or pull request.

A title, placeholder, or reference link alone does not complete an authoring item.

## Contribution standards

- Use English, Markdown, and relative links within the repository.
- Keep the core focused; place lengthy derivations, advanced systems work, and research extensions in the reference library.
- Connect each mechanism to a question, controlled comparison, or useful system decision.
- Record assumptions, controls, model/data/code/configuration versions, raw results, failures, and resource limits with executable artifacts.
- Cite primary research or official documentation. Distinguish illustrative examples, source-reported results, and experiments that actually ran.
- Separate data, architecture, training, and inference effects where the evidence permits. Generated explanations alone do not establish a model's internal computation.

## Before submitting a contribution

Copy this checklist into a pull request when useful; leave the template unchanged here.

- [ ] The contribution addresses a specific LLM mechanism or system decision in its submodule.
- [ ] It respects the assumed background and avoids repeating beginner material.
- [ ] The experiment has explicit hypotheses, controls, inspectable artifacts, and acceptance criteria.
- [ ] Technical claims, links, examples, and reported execution status have been checked.
- [ ] Questions include answer guidance, and limitations follow from the available evidence.
- [ ] Only completed and verified content items are checked in the submodule README.

Updated **15 November 2026**. Recheck version-dependent documentation when adding executable instructions.
