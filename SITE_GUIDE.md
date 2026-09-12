# Shattered Needle v3.3 Website Guide

This file is the durable editorial and implementation contract for future `index.html` updates.

## Identity

- The public benchmark name is **Shattered Needle v3.3**.
- Do not expose internal project names, experiment labels, or generation identifiers.
- Keep the site terse, neutral, and results-first.
- Preserve the canonical opening copy from the repository README: "A needle-in-a-haystack task
  turned inside out..."

## Data

- `results.json` is the single source of truth for every displayed run.
- Regenerate it from run artifacts with `consolidate_leaderboard.py --site-out`; do not hand-edit scores.
- The main table, score chart, detailed breakdown, and headline inventory must be rendered from it.
- Derive the headline corpus, document, approximate-token, and held-out-question inventory from all
  committed canonical corpus bundles; do not hard-code one corpus's counts.
- Store exact scores and seconds in JSON. Round only in presentation.
- Retain exact cost and accounting basis in JSON. Show one Cost column: prefer actual provider billing,
  otherwise show the token-rate estimate with an `e` suffix.
- Show wall-clock time in minutes, never mixed hour/minute notation.
- Keep incomplete timing and cost measurements marked as incomplete.
- Keep estimated rows explicitly separate from completed tests in the generator and visibly labelled on the site.
- An estimated row has no v3.3 actual cost. Its score, wall time, and estimated cost must name the prior run version used.
- Do not add a scored bar for a run whose `weighted_score` is `null`.
- Retiring or superseding a run is a `results.json` edit, never a file move in the benchmark repo's
  `runs/` archive (that archive does not feed this site). To drop a run from the score chart set its
  `weighted_score` to `null`; to keep it visible but flagged, add or adjust its `status`/note; to
  remove it entirely, delete the row and decrement the displayed run count. Do this only on a
  deliberate decision — a within-version corpus fix that leaves the gold answer key, question set, and
  accepted answers unchanged does not by itself retire prior runs.

## Results Presentation

- Weighted score is the primary metric.
- Show a vertical score bar chart below the results table, sorted by exact weighted score descending,
  with narrow bars and small tilted x-axis labels.
- The score chart is single-series: all bars use one color. Do NOT color bars by protocol
  (portable / historical / query-only) or by any other dimension; there is no chart color legend.
- Keep diagnostic and failed statuses visible; never imply they are portable end-to-end scores.
- Show the execution harness beneath the model name in small secondary type: Claude Code for OpenAI
  models and Claude estimates, OpenCode for all others.
- Show the recorded model variant. Leave ordinary tested-run notes blank; use short notes only for
  noteworthy conditions such as a resumed run or the source version of an estimate. `variant` is the
  reasoning-effort profile used for the run (e.g. `high`, `xhigh`, or a named thinking budget).
- Include interrupted or failed model attempts as unscored rows when they consumed meaningful runtime
  or cost; keep them out of the score chart.
- Keep estimated rows out of the completed-test chart; they may appear in the table with an `est.` score prefix.
- Retain the sortable table for approximate cost, time, and status information. Protocol belongs in
  chart tooltips and methodology notes, not in bar color or the primary table.
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
- Preserve accessible table headings, status text, chart labels, and reduced-motion behavior.
- Validate JSON parsing, HTML structure, internal links, JavaScript syntax, row order, and the absence
  of internal naming before publishing.
