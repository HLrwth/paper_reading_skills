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

Explain the mechanism in prose first. Then give the core equations.

### Notation

- `{symbol}`: {meaning}

### Core Equations

$$
{renderable equation}
$$

After each equation, explain what it does in one or two sentences.

## 3. Training / Optimization Setup

Use this section for neural-network, optimization, and learning papers.

| Item | Description |
| --- | --- |
| Input | {model inputs at training and inference} |
| Label / target | {supervised labels, self-supervised target, reward, preference, reconstruction target, etc.} |
| Supervision type | {supervised / self-supervised / imitation / RL / offline RL / synthetic / human feedback / none} |
| Architecture | {backbone, heads, decoders, action representation, modules} |
| Loss / objective | {loss terms and final objective} |
| Inference | {how predictions/actions/samples are produced} |

If the paper is not a learning/optimization paper, replace this table with "Conceptual Pipeline" or "System Pipeline".

## 4. Experiments And Results

### Benchmarks And Tasks

- `{benchmark}`: {task, metric, why it matters}

### Main Results

| Benchmark / task | Metric | Paper result | Compared to | Takeaway |
| --- | --- | --- | --- | --- |
| {name} | {metric} | {number or qualitative result} | {baseline} | {better/worse/tie and why} |

Mention common benchmarks explicitly when they appear. If the paper does not compare against strong baselines, say so.

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
- Use short paragraphs and tables for technical facts.
- Do not explain well-known background concepts such as Transformers, diffusion, MLE, Gaussian splatting, ResNets, or standard attention unless the paper modifies them in a nonstandard way.
- Do explain paper-specific concepts, symbols, modules, data representations, rewards, and evaluation protocols.
