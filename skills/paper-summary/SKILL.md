---
name: paper-summary
description: Create self-contained deep paper summaries for deep learning, robotics, and computer vision papers. Use when the user asks to summarize, deeply read, rewrite an unhelpful wiki/papers page, explain the core of a paper, extract motivation/method/equations/training setup/experiments/limitations, or produce a markdown note that lets them understand the paper without rereading the PDF.
---

# Paper Summary

## Overview

Produce a paper summary that is useful for understanding, not just indexing. The output should let the user grasp the motivation, method, math, training setup, experiments, limitations, and relationship to nearby methods by reading one markdown note.

Use this skill for:

- "Summarize this paper deeply."
- "Rewrite this wiki/papers page so I can understand the paper."
- "Extract the core equations and training objective."
- "Explain the method, inputs, labels, architecture, loss, and experiments."
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
2. **Method/math:** core mechanism and core equations in renderable LaTeX. Define notation locally unless it is a very standard DL/CV/robotics concept.
3. **Training setup:** for optimization/neural-network papers, explicitly list inputs, targets/labels, supervision type, architecture, objective/loss, and inference procedure.
4. **Experiments:** benchmarks, tasks, baselines, metrics, and especially how the paper performs on common benchmarks relative to prior methods.
5. **Conclusion:** limitations, failure modes, assumptions, and connections to related methods.

Use `references/summary-template.md` for the output structure and `references/equation-and-experiment-rules.md` for math/experiment fidelity.

### 3. Write The Summary

Write in dense, direct prose. Avoid vague "the paper proposes a framework" wording unless immediately followed by what the framework actually does.

The summary must be self-contained:

- Define paper-specific symbols before equations.
- Name the input/output objects and their dimensions when the paper makes them clear.
- Separate training-time from inference-time behavior.
- For position/survey papers without equations or training, say so and replace the training section with the paper's conceptual pipeline or taxonomy.
- For missing details, write `Not specified in the paper` rather than guessing.

### 4. Save Or Update

Default behavior:

- If the user asks for a standalone summary, output markdown in the response.
- If inside OmegaWiki and the user asks to save it, create `wiki/outputs/paper-summary-{paper-slug}.md`.
- If the user asks to improve a `wiki/papers/*.md` page, preserve frontmatter and local wiki links, then replace the body with the deep-summary structure.

Do not modify graph files. If writing to `wiki/log.md`, use `tools/research_wiki.py log`.

## Quality Bar

Before finishing, check:

- A reader can answer "what problem, what method, what evidence, what limitations?" without opening the PDF.
- Every core equation is valid Markdown/LaTeX inside `$$ ... $$`.
- Inputs, labels, architecture, and loss are explicit for ML papers.
- Benchmark claims include baseline names, metrics, and direction of comparison.
- The conclusion connects the paper to at least two nearby methods or research lines when available.

## References

- `references/summary-template.md` - canonical markdown structure.
- `references/equation-and-experiment-rules.md` - math, training, and benchmark extraction rules.
