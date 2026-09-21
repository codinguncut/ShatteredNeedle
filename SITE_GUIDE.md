# Shattered Needle v3.3 Website Guide

This file is the durable editorial and implementation contract for future `index.html` updates.

## Identity

- The public benchmark name is **Shattered Needle v3.3**.
- Do not expose internal project names, experiment labels, or generation identifiers.
- Keep the site terse, neutral, and results-first.
- Use short, concrete statements that explain the task to a general reader: models read difficult
  documents, organize facts, and answer hidden questions later.

## Data

- `results.json` is the single source of truth for every displayed run.
- Regenerate it from run artifacts with `consolidate_leaderboard.py --site-out`; do not hand-edit scores.
- The main table, score chart, detailed breakdown, and headline inventory must be rendered from it.
- Derive the headline corpus, document, approximate-token, and held-out-question inventory from all
  committed canonical corpus bundles; do not hard-code one corpus's counts.
- Store exact scores and seconds in JSON. Round only in presentation.
- Retain exact cost and accounting basis in JSON. Show one API cost column: prefer actual provider
  billing, otherwise show the token-rate equivalent without a special suffix. Round displayed costs
  to the nearest $0.10.
- For GLM coding-plan runs, use one OpenRouter provider at the median input-price tier and take its
  entire rate card (input, output, cache); do not combine independently calculated bucket medians.
  Count each provider once and use the upper-middle price for an even count. Record the pricing model
  and selected provider separately from the execution model. Keep GPT estimates at first-party OpenAI rates. Record the pricing check date
  in `results.json` and document verified rates and changes in `PRICING.md`.
- Show wall-clock time in minutes, never mixed hour/minute notation.
- Keep incomplete timing and cost measurements marked as incomplete.
- Keep carried-forward rows explicitly separate from completed tests in the generator. On the site,
  identify them through `Runs = 0` and a short source-version note, not special row styling.
- An estimated row has no v3.3 actual cost. Its score, wall time, and estimated cost must name the prior run version used.
- Do not add a scored bar for a run whose `weighted_score` is `null`.
- Retiring or superseding a run is a `results.json` edit, never a file move in the benchmark repo's
  `runs/` archive (that archive does not feed this site). To drop a run from the score chart set its
  `weighted_score` to `null`; to keep it visible but flagged, adjust its note; to
  remove it entirely, delete the row and decrement the displayed run count. Do this only on a
  deliberate decision — a within-version corpus fix that leaves the gold answer key, question set, and
  accepted answers unchanged does not by itself retire prior runs.

## Results Presentation

- Weighted score is the primary metric.
- Show a performance-versus-cost scatter plot above the results table, with API cost on the horizontal
  axis and weighted score on the vertical axis. Use a logarithmic cost axis and a linear score axis
  from 88% to 100%; disclose that choice beside the chart. Leave headroom above 100% so point
  labels stay readable. Lower-scoring runs remain in the table but are outside the plot. Higher and farther left is better. Connect the nondominated points
  with a restrained dotted Pareto-frontier line; do not add quadrant overlays. Plot the measured Muse
  result twice, once at contributor pricing and once repriced from the same token usage at standard
  commercial rates. Include both pricing scenarios in the frontier calculation; either may be dominated
  by a cheaper, higher-scoring model.
- Color chart points by model provider using the Artificial Analysis palette: Anthropic
  terracotta, OpenAI black, Meta/Kimi/GLM blue, xAI violet, Google green, Alibaba orange, and
  DeepSeek royal blue. Do not color points by protocol.
- Keep diagnostic and failed rows clearly described in notes; never imply they are completed scores.
- Show the execution harness beneath the model name in small secondary type: Claude Code for Anthropic
  Claude models (`claude*`, including carried-forward estimates), OpenCode for all other models.
- Show the recorded model variant in parentheses after the model name, not in a separate column.
  Leave ordinary tested-run notes blank; use short notes only for the source version of a
  carried-forward result. Do not expose resume history on the website. `variant` is the
  reasoning-effort profile used for the run (e.g. `high`, `xhigh`, or a named thinking budget).
- Omit interrupted or failed attempts from the table and chart. List them under Failed and
  interrupted runs from `results.json` `incomplete`, with a short reason (did not complete, or
  aborted after running too long).
- Plot carried-forward Claude rows as hollow points in the performance-versus-cost chart and disclose
  their source version in the tooltip. Keep any other carried-forward rows out of the chart. Give all
  carried-forward rows the same table styling and score/time formatting as other models.
- Retain the sortable table for approximate cost and time information. Protocol belongs in
  chart tooltips and methodology notes, not in bar color or the primary table.
- For all displayed rows, including carried-forward Claude entries, calculate a ±1 population standard
  deviation comparison band. Calculate cost in log space and include both Muse pricing scenarios in its
  population; calculate mean wall time on the ordinary arithmetic scale. Mark values below the band in
  green and values above it in red. Do not add arrows or other markers that disrupt numeric alignment.
  Describe these as values outside the comparison band rather than statistical outliers.
- Display weighted scores as whole percentages in the chart and table while sorting by exact values.

## Copy And Methodology

- Describe the two isolated same-model phases as WEAVE and QUERY.
- State that QUERY receives the frozen knowledge base and no source corpus.
- State that grading is mechanical and representation-agnostic.
- Describe this release as one frozen instance, not a population-level model ranking.
- Never cite carry-forward estimates as completed v3.3 performance.
- Avoid claims broader than the measured capability: anticipatory knowledge organization under
  compression, cross-document synthesis, provenance recovery, and long-horizon coherence.

## Implementation

- Keep the site usable on desktop and mobile.
- Use the pinned Chart.js version already referenced by `index.html` unless deliberately upgrading it.
- Keep chart tooltips informative but the visible chart uncluttered.
- Preserve accessible table headings, chart labels, and reduced-motion behavior.
- Validate JSON parsing, HTML structure, internal links, JavaScript syntax, row order, and the absence
  of internal naming before publishing.
