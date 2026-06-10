# Paper Quality Scoring Rubric

Score papers directly on a `5..0` scale for deep learning, robotics, and computer vision. Be conservative: a paper can be interesting without being a "good paper" for the user's reading or ingestion queue.

## Score Meanings

- `5` - Must read / seminal. Field-shaping anchor paper, canonical method/dataset/benchmark, or an obvious foundation for the user's current research area.
- `4` - High-impact. Strong paper that is worth reading and usually worth ingesting when relevant; may be a top-venue paper, major open-source model/dataset, or highly cited follow-up.
- `3` - Solid. Useful supporting reference, competent method, benchmark, or comparison paper; read/ingest only when it fills a concrete gap.
- `2` - Contextual/narrow. Interesting for a specific subproblem, but low general priority.
- `1` - Weak/low priority. Probably skip unless the user explicitly needs exhaustive coverage.
- `0` - Not sure. Evidence is insufficient, metadata is missing, or the paper is too new/uncertain to rank. Use this for recent papers that look plausible but do not yet have enough venue, citation, author/lab, adoption, or evidence signal.

## Citation And Age Signal

Binding user preference: if a paper is older than 2 years and has fewer than about 100 citations, do not label it "good" unless there is a clear exception. Exceptions must be explicit: niche robotics subfield with slow citation dynamics, important dataset/codebase, benchmark paper, or direct relevance to the user's current project.

For papers less than 1 year old, do not penalize for low citations. Replace the citation test with venue, author/lab, early community adoption, code release, and technical fit. If those signals are not enough to justify a confident `3`, `4`, or `5`, score it `0` rather than guessing.

Practical citation anchors:

- Older than 2 years and 500+ citations or high influential citations: eligible for `5` if technically central.
- Older than 2 years and 100+ citations: eligible for `4` or `3` depending on relevance and venue.
- Older than 2 years and below 100 citations: usually `2` or lower; only exceed `2` with an explicit exception.
- Less than 1 year old: citations are optional; confidence must come from other signals.

## Venue Signal

- Top-tier venue for the field supports `4` or `5`: NeurIPS, ICML, ICLR, CVPR, ICCV, ECCV, RSS, CoRL, or equivalent top journal/track for the specific contribution.
- Strong but mixed or broad venues support `3` or `4` after inspecting the paper: ICRA, IROS, AAAI, IJCAI, AISTATS, RA-L, T-RO, IJRR, Science Robotics, TPAMI, IJCV. ICRA and IROS are good venues but large and uneven; require paper-specific evidence.
- Workshop, emerging venue, technical report, or arXiv preprint is provisional. Use `0` if the paper is new and lacks enough independent signal.
- Unknown venue, predatory-looking venue, or no credible review signal should usually be `0`, `1`, or `2`.

Venue is not enough by itself. A weak paper at a top venue can still be a skip; a recent arXiv paper can be worth watching if other signals are strong.

## Author And Institution Signal

- Leading authors/labs in the exact area can justify raising a recent paper from `0` to `3` or `4` when the technical evidence is plausible.
- Recognized institutions or labs provide a smaller boost; fame outside the exact topic should not dominate.
- Unknown or unverifiable authors/institutions are not a penalty by themselves, but remove one source of confidence for new papers.

Do not over-weight fame. Strong authors make a recent low-citation paper worth checking, but they do not rescue weak experiments, unclear novelty, or poor relevance.

## Technical Relevance And Novelty

- Direct relevance to the user's active DL/robotics/CV topic is required for `4` or `5`.
- New mechanism, benchmark, dataset, training recipe, architecture, or empirical finding can support a high score if evidence is strong.
- Strongly adjacent work is usually `3`.
- Incremental/contextual work is usually `2`.
- Off-topic, duplicate, or only keyword-similar work is usually `1` or `0`.

For OmegaWiki, prefer papers that connect to existing concepts, claims, open questions, or reading-plan gaps.

## Evidence Quality And Reproducibility

- Strong evidence supports `4` or `5`: solid experiments, strong baselines, ablations, real robot or realistic deployment evidence where relevant, and code/data/model release or enough detail to reproduce.
- Reasonable but limited evidence usually caps the score at `3`.
- Early promise with missing ablations, incomplete comparisons, or only small demos usually caps the score at `2` or `0`.
- Claims that outrun evidence should be `1` or `0`.

## Red Flags

- Older than 2 years with low citations and no niche/benchmark exception.
- ArXiv-only for more than 2 years with little uptake.
- Marketing-style tech report with thin evaluation.
- New acronym for a standard combination of known ideas.
- Robotics paper with no real-world validation when the claim is physical generalization.
- Benchmark paper with unclear data leakage or cherry-picked baselines.
- Claims of "generalist", "foundation", "world model", or "reasoning" without tests that isolate the claimed capability.

## Decision Labels

- `5`: must read; ingest if absent.
- `4`: read/ingest when relevant.
- `3`: support/context; ingest if it fills a specific gap.
- `2`: comparison/background only.
- `1`: skip unless specifically requested.
- `0`: not sure; verify more, watch, or leave unranked.
