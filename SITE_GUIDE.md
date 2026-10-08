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
- Retain exact cost and accounting basis in JSON. In the primary API cost column, prefer actual provider
  billing, otherwise show the token-rate equivalent without a special suffix. Round displayed costs
  to the nearest $0.10.
- Add a separate sortable **Flex estimate** column for supported first-party GPT models. Generate it
  from each run's captured token buckets and the verified OpenAI Flex rate card, then average across
  the same draws; never halve an actual bill or an already rounded displayed cost. Retain the pricing
  model, provider, and counterfactual basis in JSON. Omit estimates if any contributing draw lacks usage.
  Show a dash for missing estimates, sorted last in either direction. These are same-usage cost scenarios,
  not measured Flex runs: do not imply that the displayed wall time was achieved on Flex. Document slower
  responses, resource unavailability, and potentially different cache hit rates.
- For GLM coding-plan runs, use one OpenRouter provider at the median input-price tier and take its
  entire rate card (input, output, cache); do not combine independently calculated bucket medians.
  Count each provider once and use the upper-middle price for an even count. Record the pricing model
  and selected provider separately from the execution model. Keep GPT estimates at first-party OpenAI rates. Record the pricing check date
  in `results.json` and document verified rates and changes in `PRICING.md`.
- Show wall-clock time in minutes, never mixed hour/minute notation.
- Keep incomplete timing and cost measurements marked as incomplete.
- Keep carry-forward projections explicitly separate from measured rows in the internal
  consolidated board. Public results include completed v3.3 draws only: omit zero-run
   Opus 5 and Sonnet 5 projections, the retired GPT-5.6 Sol row, and GPT-6 Sol
   (superseded by GPT-6.1 Sol) from both table and chart. Preserve their historical
   runs in the consolidated board. GPT-6.1 Sol's run variant is `high` (owner-confirmed).
- Do not add a scored bar for a run whose `weighted_score` is `null`.
- Retiring or superseding a public row is a generator curation decision, never a file move
  in the benchmark repo's `runs/` archive (that archive does not feed this site). Regenerate
  `results.json` after changing the public selection; retain the internal result. Do this only
  on a deliberate decision — a within-version corpus fix that leaves the gold answer key,
  question set, and accepted answers unchanged does not by itself retire prior runs.

## Results Presentation

- Weighted score is the primary metric.
- Show a performance-versus-cost scatter plot above the results table, with API cost on the horizontal
  axis and weighted score on the vertical axis. Use a logarithmic cost axis and a linear score axis
  from 80% to 100%; disclose that choice beside the chart. Leave headroom above 100% so point
  labels stay readable. Lower-scoring runs remain in the table but are outside the plot. Higher and farther left is better. Connect the nondominated points
  with a restrained dotted Pareto-frontier line; do not add quadrant overlays. Plot the measured Muse
  result twice, once at contributor pricing and once repriced from the same token usage at standard
  commercial rates. Include both pricing scenarios in the frontier calculation; either may be dominated
  by a cheaper, higher-scoring model.
- Label the measured ~$0.4 table row `Muse Spark 1.3 Contributor`. Name both Muse chart
  points simply `Muse Spark 1.3`; explain contributor versus commercial pricing in the
  tooltip and chart description.
- Keep Flex scenarios in the table only; the chart and frontier use the primary API costs and the
   existing Muse commercial comparison.
- Use filled provider-colored points for models with at least three completed scored runs
  (`runs >= 3`); show models with one or two as unfilled, provider-colored outlines. Keep
  these measured low-count models in the chart and table. Explain the distinction beside
  the chart and include the completed scored run count in tooltips. Both Muse pricing
  scenarios use the same measured run count; incomplete attempts never count toward it.
- Use short visible point labels (model name only, without the leading `Claude `); retain full
  model names and reasoning variants in table rows and chart tooltips.
- Color chart points by model provider using the Artificial Analysis palette: Anthropic
  terracotta, OpenAI black, Meta/Kimi/GLM blue, xAI violet, Google green, Alibaba orange, and
  DeepSeek royal blue. Do not color points by protocol.
- Keep diagnostic and failed rows clearly described in notes; never imply they are completed scores.
- Show the execution harness beneath the model name in small secondary type: Claude Code for Anthropic
  Claude models (`claude*`), OpenCode for all other models.
- Show the recorded model variant in parentheses after the model name, not in a separate column.
   Generate notes from finalized unscored attempt artifacts, distinguishing interruptions,
   provider errors and setup blocks. Omit WEAVE/QUERY output-limit and quota/credit stops
   from table notes, including their contribution to displayed attempt counts; retain their
   classifications internally. Do not describe setup or provider failures as model-performance failures.
   Exclude the owner-voided Kimi Code invalid-endpoint attempts and Opus 5.5 outdated-client
   attempts from the generated record and all notes; keep genuine quota stops recorded.
   Do not infer a timeout/operator cause from an interruption alone. Count each failed execution
   once, not each child session, retry, or copied transcript; completed/resumed cells are not
   unscored attempts. Omit Kimi's OpenRouter/related Kimi Code route annotation from table notes;
   never merge those routes' scores, costs, or times. Keep notes blank when no publicly
   displayed attempt reasons remain. Do not expose private paths or raw errors, or
   resume history on the website. `variant` is the
  reasoning-effort profile used for the run (e.g. `high`, `xhigh`, or a named thinking budget).
- Omit interrupted or failed attempts from the table and chart. List them under Failed and
  interrupted runs from `results.json` `incomplete`, with a short reason (did not complete,
  failed to produce results, or aborted after running too long). Use captured terminal provider
  errors/capacity stops when available, rather than describing them as slow model runs.
  A query that exits without answers
  is "failed to produce results". A weave interrupt, usage-limit rejection, or operator stop is not.
- Keep all carried-forward rows out of the public results; they belong on the internal board.
- Retain the sortable table for approximate cost and time information. Protocol belongs in
   chart tooltips and methodology notes, not in bar color or the primary table.
- Owner policy, October 5: **one rolling leaderboard**, with no historical/matched dropdown.
  Average all eligible completed draws for each model across execution-setting changes,
  including completed mixed-setting resumes. Recompute scores, costs, times and counts
  from individual executions, never from rounded cohort means. Retain settings metadata
  internally. Models do not need blanket reruns; selective reruns can inform a later
  model-specific archival decision if a meaningful deviation is observed.
- Five past GPT-6.1 Sol draws are explicitly owner-invalidated because the required 200k
  context clamp was absent. Exclude those executions and their copies from every average
  and draw count, retain their raw artifacts and internal archive, and show their public
  count/reason under Archived runs. A future compliant run may restore the model's scored
  row. Do not use a permanent model exclusion or misclassify these as failed attempts.
- On October 6 the owner also archived the single legacy Gemini 3.8 Flash draw and
  single legacy MiMo V2.6 Pro draw, plus all five legacy MiMo V2.6 Flash draws.
  Exclude each execution and its copies from all averages and completed-run counts;
  keep current-setting draws scored and display
  the archived counts (Gemini Flash: 1; MiMo Pro: 1; MiMo Flash: 5).
  This is owner-directed curation, not a claim that the small-sample comparison
  proves a causal execution-window effect.
- The owner subsequently archived five legacy DeepSeek V4.1 Flash draws and all four
  legacy Muse Spark v3.3 draws. After the October 7 refresh, DeepSeek retains five draws
  at 84.37% and returns to the chart above its 80% floor. After the October 8 refresh,
  Muse's scored table/breakdown row averages 62.00% over four eligible runs. The first
  submitted 22 of 76 answers; missing answers receive zero credit over the full question
  set. The three latest scored runs each submitted all 76 answers. Both Muse
  pricing scenarios stay outside the chart because its score is below 80%; retain the
  commercial equivalent in JSON and the cost comparison band. Its four older archives
  and three unscored attempts (two backend-overload capacity stops and one query without
  answers) remain separate from the scored runs.
- Recent OpenRouter transcripts record gateway/model IDs, not serving-provider or precision
  metadata. Keep that distinction in Run comparability; never infer a historical backend
  from the current config, endpoint list, or price estimate. Claude Code has no OpenCode
  context clamp; unknown historical windows are not confirmed violations. Keep private
  paths and internal profile IDs out of public copy. The earlier derived comparison is an
  audit snapshot, not the current publication policy.
- For all displayed rows, calculate a ±1 population standard
  deviation comparison band. Calculate cost in log space and include both Muse pricing scenarios in its
  population; calculate mean wall time on the ordinary arithmetic scale. Mark values below the band in
  green and values above it in red. Do not add arrows or other markers that disrupt numeric alignment.
  Describe these as values outside the comparison band rather than statistical outliers.
  Flex estimates neither contribute to the comparison band nor receive its color highlighting.
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
