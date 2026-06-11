# Paper Summary Template

Use this structure unless the user asks for another format. Keep headings stable so summaries are easy to scan and compare.

```markdown
# {Paper Title}

**One-line thesis:** {the paper's core claim in one sentence}

## 1. Motivation And Problem

- What problem does the paper attack?
- Why did prior work not solve it?
- Is the paper solving a new problem, solving an old problem better, or reframing the problem from a different angle?
- Why does this matter for deep learning, robotics, or computer vision?

## 2. Core Method

Explain the mechanism in prose first. Then give the core equations only if the paper actually has a central equation, objective, scoring rule, or formal decision rule. If not, omit the equation block and write: "The paper does not introduce a central mathematical objective."

If the method is an algorithm, tokenizer, planner, sampler, optimizer, or other step-by-step procedure, add a short `### Algorithm` or `### Procedure` subsection before the equations. Name the inputs, outputs, training-time steps if any, and inference-time steps if different.

### Algorithm / Procedure

1. {paper-grounded step}
2. {paper-grounded step}
3. {paper-grounded step}

### Notation

- `${symbol}$`: {meaning; include only if symbols are used in real equations or a real decision rule}

### Core Equations

$$
{renderable equation}
$$

After each equation, explain what it does in one or two sentences. Do not turn prose descriptions into pseudo-equations just to fill this section.

## 3. Training / Optimization Setup

Use this section only for papers that actually train or optimize a model. Do not invent labels, targets, or losses just to fill the table.

| Item | Description |
| --- | --- |
| Input | {model inputs at training and inference} |
| Label / target | {supervised labels, self-supervised target, reward, preference, reconstruction target, etc.} |
| Supervision type | {supervised / self-supervised / imitation / RL / offline RL / synthetic / human feedback / none} |
| Architecture | {backbone, heads, decoders, action representation, modules} |
| Loss / objective | {loss terms and final objective} |
| Inference | {how predictions/actions/samples are produced} |

If the paper is not a learning/optimization paper, rename the section to `## 3. Inference / System Setup` or `## 3. Conceptual Pipeline` and use a table like this instead:

| Item | Description |
| --- | --- |
| What is trained? | {nothing / no new model / only pre-existing components; be explicit} |
| Pre-existing components | {frozen models, external modules, hand-designed components, skill libraries, solvers, etc.} |
| Input at inference | {runtime inputs} |
| Decision rule / pipeline | {how the method chooses, plans, ranks, retrieves, controls, or reasons} |
| Output | {plans, actions, rankings, predictions, text, analysis, etc.} |

When a paper only uses separately trained components, describe those components as assumptions or dependencies, not as the training setup of the paper's method.

## 4. Experiments And Results

### Benchmarks And Tasks

- `{benchmark}`: {task, metric, why it matters}

### Main Results

| Benchmark / task | Metric | Paper result | Compared to | Takeaway |
| --- | --- | --- | --- | --- |
| {name} | {metric} | {number or qualitative result} | {baseline} | {better/worse/tie and why} |

Mention common benchmarks explicitly when they appear. If the paper does not compare against strong baselines, say so.
Do not use placeholder rows such as `Paper-reported evaluation`, `See paper`, `Named baselines`, or `Use the full paper for exact tables`. If exact numbers are unavailable after checking the paper, write `Not specified in the paper` and explain the missing evidence in prose.

### Paper Examples / Case Studies

Include this subsection when the paper uses examples to compare its method to previous methods or to explain why the method is needed.

- `{example}`: {what the previous method does, what happens in the example, and what the proposed method changes}

## 5. What To Remember

- {core mechanism}
- {main empirical finding}
- {most important limitation}
- {relationship to known methods}

## 6. Limitations And Connections

### Limitations

- {limitation}

### Connections To Other Methods

- Compared with `{method}`: {same problem, different assumption, different architecture, stronger/weaker evidence}
- Builds on or differs from `{method}`: {relationship}
```

## Style

- Prefer concrete nouns over generic phrases.
- Use `$...$` for inline math symbols and `$$...$$` for display equations.
- Use short paragraphs and tables for technical facts.
- Do not explain well-known background concepts such as Transformers, diffusion, MLE, Gaussian splatting, ResNets, or standard attention unless the paper modifies them in a nonstandard way.
- Do explain paper-specific concepts, symbols, modules, data representations, rewards, and evaluation protocols.
