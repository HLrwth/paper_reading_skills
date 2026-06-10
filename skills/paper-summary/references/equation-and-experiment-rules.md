# Equation And Experiment Rules

## Equation Fidelity

- Include only equations that are central to the paper's method, objective, inference, or theoretical claim.
- Use renderable Markdown math:

```markdown
$$
\mathcal{L}(\theta) = \sum_{t=1}^{T} \ell(f_\theta(x_t), y_t)
$$
```

- Define every paper-specific symbol before or immediately after the equation.
- Preserve the paper's notation where practical. If you simplify notation, say "using simplified notation".
- Do not invent equations that are not in the paper. If the paper is conceptual or empirical and has no core equations, write "The paper does not introduce a central mathematical objective."
- For multi-term losses, list each term and explain what behavior it encourages.

## Training Setup Rules

For ML/robotics/CV papers, extract these fields explicitly:

- **Input:** observations, images, video, text, states, point clouds, actions, proprioception, camera views, time windows, or latent variables.
- **Target/label:** class labels, next tokens, actions, trajectories, denoising targets, reconstruction targets, rewards, preferences, success labels, pseudo-labels, or self-supervised labels.
- **Supervision type:** supervised, self-supervised, imitation learning, behavior cloning, reinforcement learning, offline RL, preference learning, synthetic supervision, distillation, contrastive learning, or no training.
- **Architecture:** encoder/backbone, fusion module, planner, decoder, policy head, world model, action tokenizer, diffusion/flow head, auxiliary heads.
- **Loss/objective:** exact loss terms when available; otherwise describe the objective and mark missing mathematical details.
- **Inference:** how the trained model is used after training, including decoding, sampling, MPC/planning loops, policy rollout, or post-processing.

If the paper separates pretraining, finetuning, and evaluation, make separate rows or bullets for each stage.

## Experiment Rules

- Extract benchmark names exactly as written.
- For common benchmarks, include the metric and whether higher or lower is better.
- Compare against named baselines, not just "prior work".
- Include numbers when available. If the paper only gives qualitative claims, state that.
- Call out whether experiments are real robot, simulation, offline benchmark, synthetic, human study, or ablation-only.
- Identify the strongest baseline and the main ablation.
- Do not overclaim: "outperforms on X" only when the reported metric supports it.

## Common Failure Checks

- A summary that says "the method improves generalization" but never explains the input/output mapping is not acceptable.
- A summary that includes a loss without saying what the labels/targets are is incomplete.
- A summary that lists benchmarks but not baselines or metrics is incomplete.
- A summary of a robotics paper should distinguish training data, evaluation environment, embodiment, action space, and real-vs-sim evidence when the paper provides them.
