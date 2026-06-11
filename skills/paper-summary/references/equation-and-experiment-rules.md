# Equation And Experiment Rules

## Equation Fidelity

- Include only equations that are central to the paper's method, objective, inference, or theoretical claim.
- Use `$...$` for inline symbols and short inline expressions. Avoid `\(...\)` in OmegaWiki notes because it may not render.
- Use renderable Markdown math:

```markdown
$$
\mathcal{L}(\theta) = \sum_{t=1}^{T} \ell(f_\theta(x_t), y_t)
$$
```

- Define every paper-specific symbol before or immediately after the equation.
- Preserve the paper's notation where practical. If you simplify notation, say "using simplified notation".
- Do not invent equations that are not in the paper. Do not convert a prose-only method into pseudo-math just to make the summary look technical. If the paper is conceptual or empirical and has no core equations, write "The paper does not introduce a central mathematical objective."
- If the paper's contribution is an algorithm, tokenizer, planner, sampler, optimizer, or other math-heavy procedure, include the actual algorithm steps or pseudocode in addition to prose. The algorithm block should list inputs, outputs, and the key transformation at each step.
- If the paper gives equations for an algorithmic step, include them near the step they explain. Do not hide paper-specific math in prose-only paraphrase.
- For multi-term losses, list each term and explain what behavior it encourages.

## Training Setup Rules

Before extracting labels or losses, decide whether the paper actually trains or optimizes a model as part of its contribution. If it does not, do not fabricate a training setup. State that the method is inference-only, planning-only, conceptual, or a system composition method, then describe the runtime pipeline and any separately trained/pretrained dependencies.

For ML/robotics/CV papers that actually train a model, extract these fields explicitly:

- **Input:** observations, images, video, text, states, point clouds, actions, proprioception, camera views, time windows, or latent variables.
- **Target/label:** class labels, next tokens, actions, trajectories, denoising targets, reconstruction targets, rewards, preferences, success labels, pseudo-labels, or self-supervised labels.
- **Supervision type:** supervised, self-supervised, imitation learning, behavior cloning, reinforcement learning, offline RL, preference learning, synthetic supervision, distillation, contrastive learning, or no training.
- **Architecture:** encoder/backbone, fusion module, planner, decoder, policy head, world model, action tokenizer, diffusion/flow head, auxiliary heads.
- **Loss/objective:** exact loss terms when available; otherwise describe the objective and mark missing mathematical details.
- **Inference:** how the trained model is used after training, including decoding, sampling, MPC/planning loops, policy rollout, or post-processing.

If the paper separates pretraining, finetuning, and evaluation, make separate rows or bullets for each stage.

For inference-only or system-composition papers:

- Replace `Target/label` with `Input at inference` or `Runtime signal`.
- Replace `Loss/objective` with `Decision rule`, `Planner score`, `Controller objective`, or `System pipeline`.
- Say when a score is a decision rule rather than a training loss.
- Treat pretrained models, skill libraries, solvers, and separately trained value functions as dependencies unless the paper trains them.

## Experiment Rules

- Extract benchmark names exactly as written.
- For common benchmarks, include the metric and whether higher or lower is better.
- Compare against named baselines, not just "prior work".
- Include numbers when available. If the paper only gives qualitative claims, state that.
- Never use placeholder result rows like `Paper-reported evaluation`, `See paper`, `Named baselines`, or `Use the full paper for exact tables`.
- If the paper defines its own evaluation set instead of using a public benchmark, describe that dataset/task set precisely: number of tasks, environments, task families, metrics, and whether it is real robot, simulation, offline, or human-rated.
- If the paper does not compare against external prior work, write `No external baseline reported` and only list in-paper ablations or internal variants.
- Keep bibliographic metadata out of experiments: venue, year, citation count, Semantic Scholar snapshots, DOI, project page, and code URL should be in frontmatter or a separate metadata block.
- Call out whether experiments are real robot, simulation, offline benchmark, synthetic, human study, or ablation-only.
- Identify the strongest baseline and the main ablation.
- Do not overclaim: "outperforms on X" only when the reported metric supports it.
- Include concrete examples or case studies that the paper uses to compare against previous methods. State what the previous method does in the example, what failure or limitation appears, and how the proposed method changes the outcome.
- If the paper includes qualitative examples because exact numbers are not the main evidence, summarize those examples with the task, input, output, and comparison method.

## Common Failure Checks

- A summary that says "the method improves generalization" but never explains the input/output mapping is not acceptable.
- A summary that fabricates equations for a paper with no equations is incorrect.
- A summary that includes a loss without saying what the labels/targets are is incomplete.
- A summary that invents labels or losses for an inference-only method is incorrect.
- A summary that lists benchmarks but not baselines or metrics is incomplete.
- A summary that replaces experiment details with placeholder text is incomplete.
- A summary of an algorithmic paper that only names the algorithm but omits the steps or equations is incomplete.
- A summary that drops the paper's own comparison examples may miss the main intuition behind the method.
- A summary that puts citation counts or venue snapshots in the experiments section is poorly organized.
- A summary of a robotics paper should distinguish training data, evaluation environment, embodiment, action space, and real-vs-sim evidence when the paper provides them.
