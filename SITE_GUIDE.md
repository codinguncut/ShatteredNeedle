# Shattered Needle v1 Website Guide

This file is the durable editorial and implementation contract for future `index.html` updates.

## Identity

- The public benchmark name is **Shattered Needle v1**.
- Do not expose internal project names, experiment labels, or generation identifiers.
- Keep the site terse, neutral, and results-first.
- Preserve the canonical opening copy from the repository README: "A needle-in-a-haystack task
  turned inside out..."

## Data

- `results.json` is the single source of truth for every displayed run.
- The main table, score chart, detailed breakdown, and displayed-run count must be rendered from it.
- Store exact scores and seconds in JSON. Round only in presentation.
- Retain exact cost and accounting basis in JSON, but show only a neutral approximate amount in the
  primary table, rounded to the nearest $0.10.
- Keep incomplete timing and cost measurements marked as incomplete.
- Do not add a scored bar for a run whose `weighted_score` is `null`.

## Results Presentation

- Weighted score is the primary metric.
- Show a horizontal score bar chart sorted by exact weighted score descending.
- Distinguish portable, historical, and query-only results by color.
- Keep diagnostic and failed statuses visible; never imply they are portable end-to-end scores.
- Show the recorded model variant and a concise run note. Use `default` when no named variant was
  selected and `not recorded` when historical evidence cannot establish the setting.
- Include interrupted or failed model attempts as unscored rows when they consumed meaningful runtime
  or cost; keep them out of the score chart.
- Retain the sortable table for approximate cost, time, and status information. Protocol is encoded
  by chart color and belongs in chart tooltips and methodology notes, not the primary table.
- Display weighted scores as whole percentages in the chart and table while sorting by exact values.

## Copy And Methodology

- Describe the two isolated same-model phases as WEAVE and QUERY.
- State that QUERY receives the frozen knowledge base and no source corpus.
- State that grading is mechanical and representation-agnostic.
- Describe this release as one frozen instance, not a population-level model ranking.
- Avoid claims broader than the measured capability: anticipatory knowledge organization under
  compression, cross-document synthesis, provenance recovery, and long-horizon coherence.

## Implementation

- Keep the site usable on desktop and mobile.
- Use the pinned Chart.js version already referenced by `index.html` unless deliberately upgrading it.
- Keep chart tooltips informative but the visible chart uncluttered.
- Preserve accessible table headings, status text, chart labels, and reduced-motion behavior.
- Validate JSON parsing, HTML structure, internal links, JavaScript syntax, row order, and the absence
  of internal naming before publishing.
