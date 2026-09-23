# API pricing audit — 23 September 2026

Prices below are USD per million tokens, at standard/short-context rates unless marked Flex. Actual reported bills
remain the displayed cost when available. Subscription runs use a token-rate API equivalent.
GLM coding-plan runs use **OpenRouter → Friendli**, selected at the median input-price tier;
GPT estimates use **first-party OpenAI** prices.
The recorded execution provider is retained, with GLM's pricing provider identified separately in
`results.json`. Muse's contributor and commercial scenarios use the same measured token usage.

## Current roster

| Model | Pricing source | Input | Output | Cached input |
| --- | --- | ---: | ---: | ---: |
| Claude Fable 5.1 | Anthropic | 10 | 50 | 0.25 |
| Claude Opus 5 | Anthropic | 5 | 25 | 0.50 |
| Claude Sonnet 5 | Anthropic | 2 | 10 | 0.20 |
| GPT-6 Astra | OpenAI | 10 | 50 | 1 |
| GPT-6 Luna | OpenAI | 0.10 | 0.50 | 0.01 |
| GPT-5.6 Sol | OpenAI | 4 | 20 | 0.40 |
| GPT-5.6 Terra | OpenAI | 2 | 12 | 0.20 |
| GPT-5.6 Luna | OpenAI | 0.20 | 1.20 | 0.02 |
| Muse Spark 1.3 Contributor | OpenRouter | 0.10 | 0.20 | 0.002 |
| Muse Spark 1.3 (commercial comparison) | OpenRouter | 1.25 | 4.25 | 0.15 |
| GLM-5.3 | OpenRouter → Friendli (median-input provider) | 1.26 | 3.96 | 0.234 |
| GLM-5.3 Flash | OpenRouter → Friendli (median-input provider) | 0.15 | 0.50 | 0.03 |
| Grok 4.6 | xAI | 2 | 6 | 0.50 |
| Gemini 3.8 Flash | OpenRouter | 0.75 | 3.75 | 0.075 |
| Qwen 3.8 Max (0902) | OpenRouter | 2 | 6 | 0.25 |
| Qwen 3.8 Flash | OpenRouter | 0.15 | 0.47 | 0.016 |
| DeepSeek V4.1 Flash | OpenRouter | 0.15 | 0.60 | 0.003 |
| MiniMax M3 (paid equivalent) | MiniMax / OpenRouter | 0.30 | 1.20 | 0.06 |
| Inkling | OpenRouter | 1 | 4.05 | 0.17 |
| Kimi K3 | OpenRouter | 1.70 | 8.50 | 0.17 |
| Kimi K3 (first-party, archived only) | Kimi | 3 | 15 | 0.30 |
| MiMo V2.6 Flash | OpenRouter | 0.14 | 0.28 | 0.0028 |
| MiMo V2.6 Pro | OpenRouter | 0.435 | 0.87 | 0.0036 |

Failed or interrupted models remain outside the scored leaderboard. The free MiniMax route is
estimated at its paid equivalent, rather than interpreting unmetered usage as a zero-cost API.

## OpenAI Flex comparison

The leaderboard's **Flex estimate** column reprices the recorded GPT usage at these first-party
OpenAI **Flex / short-context** rates, verified 23 September 2026:

| Model | Input | Output | Cached input | Cache writes |
| --- | ---: | ---: | ---: | ---: |
| GPT-6 Astra | 5 | 25 | 0.50 | 6.25 |
| GPT-6 Luna | 0.05 | 0.25 | 0.005 | 0.0625 |
| GPT-5.6 Sol | 2 | 10 | 0.20 | 2.50 |
| GPT-5.6 Terra | 1 | 6 | 0.10 | 1.25 |
| GPT-5.6 Luna | 0.10 | 0.60 | 0.01 | 0.125 |

Each bucket is 50% below its corresponding standard rate. Calculate from each run's captured
uncached input, cache reads, cache writes, output, and separately reported reasoning, then average
across the same draws as the main row. Do not halve a provider bill or rounded display value.
`results.json` retains `flex_usd`, `flex_model_id`, `flex_provider`, and `flex_basis`; a missing estimate
renders as a dash. This comparison is limited to the five verified first-party routes above.

These are **same-usage cost scenarios, not measured Flex runs**. Scores and wall times describe the
original runs. Flex can be slower or return resource-unavailable errors, and different delays may
change cache hit rates. Calls that fall back to standard processing incur standard rates. As with
standard estimates, aggregate usage cannot reconstruct per-request long-context surcharges, so the
figures can be lower bounds. Long-context Flex input/cache rates are 2× and output rates 1.5× the
listed short-context rates.

Flex estimates appear only in the table. They do not add scored runs, chart points, frontier members,
or values to the cost comparison band. See [OpenAI Flex processing](https://developers.openai.com/api/docs/guides/flex-processing)
and the [Flex pricing table](https://developers.openai.com/api/docs/pricing?latest-pricing=flex).

## GLM provider selection

Select a **single provider by input price**, then use that provider's complete input/output/cache
rate card. These are actual published rates from one endpoint, not independently calculated medians
of the three token buckets, and not a median of workload-specific total costs.

- Count every listed provider once, including providers with temporarily degraded endpoint health.
  Use the published prices, including any advertised discount already embedded in them.
- Deduplicate repeated endpoint tags. For a provider with multiple variants, take its upper-middle
  input-price endpoint and retain that endpoint's entire rate card.
- Sort the representative input prices across providers. For an even count, choose the upper-middle
  price so the result is an actual provider price rather than an average of two rate cards.
- Prefer a common provider when it lies at the selected price tier for both models.

The 21 September snapshot contains **30 providers for GLM-5.3**: Friendli is 16th by input price,
at $1.26/MTok. For **GLM-5.3 Flash, 29 providers** give a middle (15th) price of $0.15/MTok;
Friendli is one of the providers tied at that price. Both use the `friendli` endpoint tag.
The complete per-provider snapshot is retained with the benchmark pricing table.

Provider prices and discounts may change. The benchmark ran on Z.AI's coding plan; these are
API-equivalent estimates, not bills or measurements from a Friendli rerun.

## Changes from the previous rate table

- **GLM-5.3:** the median-input provider's rates are **10% below** Z.AI direct
  ($1.40 input / $4.40 output / $0.26 cached input).
- **GLM-5.3 Flash:** the median-input provider's rates **match** Z.AI direct
  ($0.15 / $0.50 / $0.03).
- This replaces the earlier OpenRouter catalogue-price estimates of $3.4330 and $0.3915 per run.
  Those earlier 35%/40% differences compared provider prices, not a confirmed price drop over time.
  The refreshed mean run estimates are **$4.7534 for GLM-5.3** (displayed $4.8) and
  **$0.6525 for GLM-5.3 Flash** (displayed $0.7).

- **Qwen 3.8 27B:** input $0.42 → $0.20 (**−52.4%**), output $3 → $2.50 (−16.7%),
  cached input $0.085 → $0.05 (−41.2%). Historical model, not on the current scored leaderboard.
- **DeepSeek V4 Pro 0813:** input $0.5795 → $0.66 (+13.9%), output $1.7384 → $1.98 (+13.9%),
  cached input $0.0579 → $0.022 (**−62.0%**). Historical model.
- **DeepSeek V4 Flash 0731:** input $0.065 → $0.04 (−38.5%), output $0.18 → $0.16 (−11.1%);
  cached input remains $0.016. Historical model.
- **Claude Fable 5 cache correction:** $0.25 → $1 (**+300%**). The $0.25 cache rate belongs
  to **Fable 5.1**, which is the version on the current leaderboard and was already priced correctly.
  This corrects the table; it is not evidence of an announced price increase.
- Qwen token cache-write rates corrected: Max $2 → $2.50; Flash $0.15 → $0.20.
  Captured runs have no cache-write tokens, so this does not change their estimates.
- MiniMax's permanent 50% discount is already reflected in the previous table's $0.30/$1.20/$0.06.
  Sonnet 5's $2/$10 introductory prices are now permanent; its planned $3/$15 increase was cancelled.
  Neither announcement causes another reduction in the stored benchmark estimates.

Catalogue differences do not establish when a provider changed its prices. GLM's comparison uses
the selected median-input-price provider. GPT uses first-party rates even where OpenRouter advertises less.

## Cache writes and context tiers

- Claude runs use one-hour cache writes: Fable 5.1 $20, Opus 5 $10, Sonnet 5 $4.
  Only Fable 5.1 has the special 0.025× cache-hit rate; Fable 5 uses 0.1×.
- OpenAI short-context cache writes: Astra $12.50, Sol $5, Terra $2.50, Luna $0.25.
  Published long-context rates double input and cache prices and multiply output by 1.5.
- Grok 4.6 charges double across the request when prompt tokens reach 200k.
  MiniMax M3's standard tier doubles above 512k input tokens.
- Claude 4.6 and later include their full context window at standard pricing.
- Kimi first-party cache writes use the default five-minute rate ($3); one-hour writes cost $6.
- Where no token cache-write price is published, the estimator retains its input-rate fallback.
  Captured OpenCode runs have zero cache-write tokens. Gemini's duration-based cache storage charge
  is not treated as a one-off token cache-write price.
- Aggregate token totals cannot reconstruct per-request context tiers or storage duration.
  Estimates can therefore be lower bounds. Reasoning tokens are added at the output rate only
  when the adapter reports them separately.

## Other supported historical rates

| Model | Pricing source | Input | Output | Cached input |
| --- | --- | ---: | ---: | ---: |
| Claude Fable 5 | Anthropic | 10 | 50 | 1 |
| Claude Opus 4.8 / 4.7 | Anthropic | 5 | 25 | 0.50 |
| Claude Sonnet 4.6 | Anthropic | 3 | 15 | 0.30 |
| Claude Haiku 4.5 | Anthropic | 1 | 5 | 0.10 |
| Qwen 3.8 2.4T A95B | OpenRouter | 2 | 6 | 0.25 |
| Qwen 3.8 27B | OpenRouter | 0.20 | 2.50 | 0.05 |
| DeepSeek V4 Pro 0813 | OpenRouter | 0.66 | 1.98 | 0.022 |
| DeepSeek V4 Flash 0731 | OpenRouter | 0.04 | 0.16 | 0.016 |

## Sources

Checked 23 September 2026:

- [OpenAI API pricing](https://developers.openai.com/api/docs/pricing)
- [Anthropic pricing and cache rules](https://platform.claude.com/docs/en/about-claude/pricing)
- [OpenRouter models API](https://openrouter.ai/api/v1/models) — `prompt`, `completion`,
  `input_cache_read`, and token-based `input_cache_write`, converted from USD/token.
- [GLM-5.3 provider endpoints](https://openrouter.ai/api/v1/models/z-ai/glm-5.3/endpoints)
  and [GLM-5.3 Flash provider endpoints](https://openrouter.ai/api/v1/models/z-ai/glm-5.3-flash/endpoints)
  — provider selection and the complete Friendli rate cards.
- [Z.AI pricing](https://docs.z.ai/guides/overview/pricing)
- [MiniMax pay-as-you-go pricing](https://platform.minimax.io/docs/guides/pricing-paygo)
- [xAI models and pricing](https://docs.x.ai/developers/models)
- [Kimi pricing](https://platform.kimi.ai/docs/pricing/chat)
