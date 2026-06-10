---
name: paper-quality
description: Score and triage research papers on a 5-to-0 scale for deep learning, robotics, and computer vision. Use when deciding whether a paper is worth reading, ingesting into OmegaWiki, adding to a reading plan, or promoting from a discovery shortlist; combines citation-age signals, top venue checks, author/institution reputation, technical relevance, and evidence quality, with 0 reserved for uncertain or insufficiently verified papers.
---

# Paper Quality

## Overview

Judge whether a paper is actually worth attention in deep learning, robotics, or computer vision. The skill is a scoring layer: it can stand alone for one paper, or sit after `discover` / web search and before `ingest`.

Use this skill for:

- "Is this paper good?"
- "Score these candidate papers."
- "Which of these should I ingest/read first?"
- "Find good papers on this topic."
- "Rank this arXiv/S2/search shortlist."

## Workflow

### 1. Collect Metadata

For each paper, collect:

- title, year, arXiv ID or DOI, venue/publication status
- citation count and influential citation count from Semantic Scholar when available
- authors, author h-index/profile signals when available
- affiliations/labs, verified from the paper, project page, author pages, or institution/lab pages
- abstract/TLDR and claimed contribution
- code/data/project page, if any
- whether the paper already exists in `wiki/papers/`

In this repo, prefer the existing tools when possible:

```bash
python3 tools/fetch_s2.py paper <arxiv-id>
python3 tools/fetch_s2.py search "<title or topic>" 10
python3 tools/discover.py from-topic "<topic>" --wiki-root wiki --limit 20 --output-checkpoint .checkpoints/ --markdown
python3 tools/discover.py from-anchors --id <arxiv-id> --wiki-root wiki --limit 20 --output-checkpoint .checkpoints/ --markdown
```

If the user asks for "famous scholars or institutions", search the internet instead of relying on memory. Verify with at least one concrete source such as Semantic Scholar author pages, Google Scholar profiles/metrics, lab pages, conference award pages, CSRankings, or official institution pages. If web or S2 is unavailable, mark author/institution reputation as provisional.

### 2. Apply The Score

Use `references/scoring-rubric.md` for the detailed native `5..0` rubric. Short version:

- `5`: must read, seminal, field-shaping anchor
- `4`: high-impact paper worth reading/ingesting
- `3`: solid useful paper, good supporting reference
- `2`: narrow/contextual paper, only read for a specific gap
- `1`: weak or low-priority paper
- `0`: not sure / insufficient evidence / too new to judge

The user's hard rule is binding: if a paper is more than 2 years old and has fewer than about 100 citations, it should not be called "good" unless there is a clear field-specific exception. Recent papers less than 1 year old are exempt from the citation threshold, but need stronger venue, author, relevance, or early community signals.

### 3. Interpret The Result

- `5`: read immediately and ingest if absent
- `4`: read/ingest when relevant to the current topic
- `3`: add as supporting context; ingest only if it fills a gap
- `2`: keep as comparison/background only
- `1`: skip unless specifically requested
- `0`: do not rank as good yet; collect more evidence or put on watchlist

### 4. Report Concisely

For one paper, output:

```markdown
**Verdict:** read/ingest/watch/skip
**Score:** N/5, where 0 = not sure / insufficient evidence
**Why:** 2-4 bullets covering citations, venue, people/institution, and technical/evidence fit
**Caveats:** missing metadata, weak evidence, provisional venue status, or citation-age issues
**Next action:** ingest URL, add to reading plan, or ignore
```

For a shortlist, output a ranked table with columns:

`rank | paper | year | venue | citations | author/lab signal | score | action | reason`

## OmegaWiki Integration

Before recommending ingest, dedupe against `wiki/papers/` by arXiv ID and title. If a paper is already present, suggest updating its page or importance rather than ingesting it again.

When the user explicitly asks to ingest good papers, use this skill to select candidates, then hand accepted papers to the repo's `ingest` workflow. Do not auto-ingest from a score-only request.

## References

- `references/scoring-rubric.md` - detailed scoring rules and red flags.
- `references/field-signals.md` - venue tiers, reputation checks, and external sources to consult.
