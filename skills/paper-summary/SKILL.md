---
name: paper-summary
description: Create self-contained deep paper summaries for deep learning, robotics, and computer vision papers. Use when the user asks to summarize, deeply read, rewrite an unhelpful wiki/papers page, explain the core of a paper, extract motivation/method/equations/training setup/experiments/limitations, or produce a markdown note that lets them understand the paper without rereading the PDF.
---

# Paper Summary

## Overview

Produce a paper summary that is useful for understanding, not just indexing. The output should let the user grasp the motivation, method, math, training or inference setup, experiments, limitations, and relationship to nearby methods by reading one markdown note.

Use this skill for:

- "Summarize this paper deeply."
- "Rewrite this wiki/papers page so I can understand the paper."
- "Extract the core equations and training or inference objective."
- "Explain the method, inputs, labels if any, architecture, loss if any, and experiments."
- "Create a paper reading note from this arXiv/PDF/wiki paper page."

## Workflow

### 1. Get The Real Paper Text

Do not summarize only from an existing `wiki/papers/*.md` page unless the user explicitly wants a quick rewrite. Those pages are often index-card summaries and may omit the math, labels, architecture, and benchmark details.

Preferred source order:

1. Paper source `.tex` if available.
2. Paper PDF if source is unavailable.
3. arXiv abstract/project page/S2 metadata only as secondary context, not the main source.
4. Existing wiki page only for title, local links, and prior wiki context.

In OmegaWiki, locate likely sources from the paper page frontmatter and body: `arxiv`, `Local source`, `Hosted PDF`, `raw/discovered/`, and `raw/tmp/`.

### 2. Read For The Five Required Questions

Read the paper with these targets:

1. **Motivation/problem:** why the authors wrote it, what prior work could not solve, and whether this is a new problem, a better solution, or a different angle.
2. **Method/math:** core mechanism and core equations in renderable LaTeX only when the paper actually contains central equations, objectives, or explicit decision rules. If the paper has no core equations, say so and explain the mechanism in prose, algorithm steps, or a system pipeline instead. Do not invent equations to make the note look mathematical.
3. **Training or inference setup:** first decide whether the paper actually trains or optimizes a model. If it does, explicitly list inputs, targets/labels, supervision type, architecture, objective/loss, and inference procedure. If it does not, say so clearly and replace labels/loss with the inference-time decision rule, system pipeline, or conceptual pipeline. Do not invent targets, labels, or losses to fill a template.
4. **Experiments:** benchmarks, tasks, baselines, metrics, and especially how the paper performs on common benchmarks relative to prior methods. If the paper does not use a standard benchmark or does not compare to prior work, say that explicitly. Do not write placeholder rows such as `See paper`, `paper-reported evaluation`, or `named baselines`.
5. **Conclusion:** limitations, failure modes, assumptions, and connections to related methods.

Use `references/summary-template.md` for the output structure and `references/equation-and-experiment-rules.md` for math/experiment fidelity.

### 3. Write The Summary

Write in dense, direct prose. Use simple, clear phrases. Avoid vague "the paper proposes a framework" wording unless immediately followed by what the framework actually does.

### Clarity Rules

Assume the reader is smart but busy. Write so they can understand the paper without guessing what your shorthand means.

- Prefer concrete subject-verb-object sentences: `GR00T trains a DiT to denoise action chunks`, not `GR00T performs dual-system embodied reasoning`.
- For every paper-specific method component, explain four things: what it is, where it appears in the system, why the authors use it, and what evidence or ablation supports it. For example, do not merely write `DCT+BPE`; explain what DCT changes in the action sequence and why BPE is needed afterward.
- If a paper-specific component is an algorithm or math-heavy module, include the algorithmic steps, pseudocode, or paper equations needed to understand it. Use prose as the companion explanation, not as a replacement for the algorithm when the paper's contribution is algorithmic.
- When the paper gives a concrete example or case study to compare its method with a previous method, include that example in the summary. Explain what the previous method does, what fails or changes in the example, and what the proposed method changes.
- Replace vague claims with the mechanism and evidence. Do not write `low-data advantage`; write `after pretraining, the model fine-tunes better than Diffusion Policy when both use 100 demos/task`.
- Define every non-obvious label the first time it appears, including model variants, dataset splits, task families, and abbreviations.
- Avoid broad words unless they are immediately grounded: `framework`, `paradigm`, `pipeline`, `reasoning`, `semantic`, `hierarchical`, `embodied`, `robust`, `generalization`, `sample-efficient`, `strong`, `good`, `improves`, `outperforms`.
- If using one of those words, add the concrete meaning in the same sentence or the next sentence. Example: `sample-efficient` means `higher success with 10% of the demonstrations`.
- Do not compress multiple ideas into one phrase. Split `hierarchical data helps train the model` into: what the hierarchy is, where it enters the dataset, what the supervised target is, and what the paper actually measures.
- Separate what the paper **does**, what the paper **claims**, and what you **infer**. Mark inference with phrasing such as `The safest interpretation is...` or `This suggests...`.
- When the paper is ambiguous, say exactly what is ambiguous. Do not smooth it over with a confident-sounding summary.

The summary must be self-contained:

- Define paper-specific symbols before equations when equations are present.
- Use `$...$` for inline math in OmegaWiki notes, for example `$o_t$` or `$\theta$`. Do not use `\(...\)` because the local renderer may leave it unrendered.
- Only include equations that appear in the paper or are faithful simplified notation for an equation/decision rule the paper explicitly states. If there is no central equation, omit `Notation` and `Core Equations` unless they are genuinely useful, and write that the paper does not introduce a central mathematical objective.
- For algorithmic papers, include a short algorithm block when it is clearer than prose. The block should name inputs, outputs, training-time steps if any, and inference-time steps if different.
- Name the input/output objects and their dimensions when the paper makes them clear.
- Separate training-time from inference-time behavior.
- For inference-only, planning-only, position, or survey papers without new training, say so and replace the training section with the paper's system pipeline, decision rule, conceptual pipeline, or taxonomy. Do not keep `Label / target` or `Loss / objective` rows unless the paper really has them.
- For missing details, write `Not specified in the paper` rather than guessing.
- Experiment tables must contain concrete task names, datasets/benchmarks, metrics, numbers or explicit qualitative outcomes, and named comparisons only when the paper actually reports them. If no comparison exists, write `No external baseline reported` rather than inventing one.
- Bibliographic facts such as venue, year, citation count, Semantic Scholar snapshot, DOI, project URL, and code URL belong in frontmatter or a metadata section, not in `Experiments And Results`.
- When comparing task groups, name the actual groups and metrics. Avoid vague labels such as `simpler tasks` or `harder tasks` unless they are defined immediately.
- Introduce named system variants, model backends, and abbreviations before using them in result tables. For example, state which LLM or policy backbone a name refers to before writing rows such as `PaLM-SayCan` or `FLAN-SayCan`.
- When a paper uses shorthand dataset/task-family names, define what they mean in plain language before using them. If a label is potentially misleading, keep the paper's name in parentheses and use a clearer phrase in prose.
- Before saving, run a confusion audit: for every important sentence, ask "Could the user reasonably ask what this means?" If yes, rewrite it with concrete mechanisms, inputs/outputs, labels, losses, datasets, baselines, or numbers.

### 4. Save Or Update

Default behavior:

- If the user asks for a standalone summary, output markdown in the response.
- If inside OmegaWiki and the user asks to save it, create `wiki/outputs/paper-summary-{paper-slug}.md`.
- If the user asks to improve a `wiki/papers/*.md` page, preserve frontmatter and local wiki links, then replace the body with the deep-summary structure.

Do not modify graph files. If writing to `wiki/log.md`, use `tools/research_wiki.py log`.

## Quality Bar

Before finishing, check:

- A reader can answer "what problem, what method, what evidence, what limitations?" without opening the PDF.
- A reader does not need to decode vague phrases. Important claims name the mechanism, setup, baseline, metric, or limitation.
- Algorithmic or math-heavy contributions include the paper's algorithm steps, equations, or decision rules when the paper provides them.
- Paper-provided examples or case studies are included when they explain why the method is needed or how it differs from prior work.
- Inline math uses `$...$`, and display equations use `$$ ... $$`.
- Every included equation is valid Markdown/LaTeX inside `$$ ... $$`; no equations are fabricated for conceptual or empirical papers that do not have them.
- Inputs, labels, architecture, and loss are explicit for papers that actually train models; for papers that do not train models, the absence of training is explicit and no labels/losses are fabricated.
- Benchmark claims include baseline names, metrics, and direction of comparison.
- No experiment table contains placeholder cells like `See paper`, `named baselines`, or `use the full paper`.
- The experiments section contains empirical evidence only, not citation counts or venue metadata.
- The conclusion connects the paper to at least two nearby methods or research lines when available.

## References

- `references/summary-template.md` - canonical markdown structure.
- `references/equation-and-experiment-rules.md` - math, training, and benchmark extraction rules.
