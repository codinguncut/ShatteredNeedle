# API pricing audit — 21 September 2026

Prices below are USD per million tokens, at standard/short-context rates. Actual reported bills
remain the displayed cost when available. Subscription runs use a token-rate API equivalent.
GLM coding-plan runs use **OpenRouter** prices; GPT estimates use **first-party OpenAI** prices.
The recorded execution provider is retained, with GLM's pricing provider identified separately in
`results.json`. Muse's contributor and commercial scenarios use the same measured token usage.

## Current roster

| Model | Pricing source | Input | Output | Cached input |
| --- | --- | ---: | ---: | ---: |
| Claude Fable 5.1 | Anthropic | 10 | 50 | 0.25 |
| Claude Opus 5 | Anthropic | 5 | 25 | 0.50 |
| Claude Sonnet 5 | Anthropic | 2 | 10 | 0.20 |
| GPT-6 Astra | OpenAI | 10 | 50 | 1 |
| GPT-5.6 Sol | OpenAI | 4 | 20 | 0.40 |
| GPT-5.6 Terra | OpenAI | 2 | 12 | 0.20 |
| GPT-5.6 Luna | OpenAI | 0.20 | 1.20 | 0.02 |
| Muse Spark 1.3 Contributor | OpenRouter | 0.10 | 0.20 | 0.002 |
| Muse Spark 1.3 (commercial comparison) | OpenRouter | 1.25 | 4.25 | 0.15 |
| GLM-5.3 | OpenRouter equivalent | 0.91 | 2.86 | 0.169 |
| GLM-5.3 Flash | OpenRouter equivalent | 0.09 | 0.30 | 0.018 |
| Grok 4.6 | xAI | 2 | 6 | 0.50 |
| Gemini 3.8 Flash | OpenRouter | 0.75 | 3.75 | 0.075 |
| Qwen 3.8 Max (0902) | OpenRouter | 2 | 6 | 0.25 |
| Qwen 3.8 Flash | OpenRouter | 0.15 | 0.47 | 0.016 |
| DeepSeek V4.1 Flash | OpenRouter | 0.15 | 0.60 | 0.003 |
| MiniMax M3 (paid equivalent) | MiniMax / OpenRouter | 0.30 | 1.20 | 0.06 |
| Inkling | OpenRouter | 1 | 4.05 | 0.17 |
| Kimi K3 | OpenRouter | 1.70 | 8.50 | 0.17 |
| Kimi K3 (first-party, archived only) | Kimi | 3 | 15 | 0.30 |

Failed or interrupted models remain outside the scored leaderboard. The free MiniMax route is
estimated at its paid equivalent, rather than interpreting unmetered usage as a zero-cost API.

## Changes from the previous rate table

- **GLM-5.3: 35% lower** API-equivalent rates, switching from first-party Z.AI
  ($1.40 input / $4.40 output / $0.26 cached input) to OpenRouter.
- **GLM-5.3 Flash: 40% lower** API-equivalent rates, switching from Z.AI
  ($0.15 / $0.50 / $0.03) to OpenRouter.

  Recomputed mean run costs: GLM-5.3 **$5.2816 → $3.4330** (displayed $5.3 → $3.4),
  GLM-5.3 Flash **$0.6525 → $0.3915** (displayed $0.7 → $0.4).

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

Catalogue differences do not establish when a provider changed its prices. GLM's reductions are a
change of comparison provider. GPT uses first-party rates even where OpenRouter advertises less.

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

Checked 21 September 2026:

- [OpenAI API pricing](https://developers.openai.com/api/docs/pricing)
- [Anthropic pricing and cache rules](https://platform.claude.com/docs/en/about-claude/pricing)
- [OpenRouter models API](https://openrouter.ai/api/v1/models) — `prompt`, `completion`,
  `input_cache_read`, and token-based `input_cache_write`, converted from USD/token.
- [Z.AI pricing](https://docs.z.ai/guides/overview/pricing)
- [MiniMax pay-as-you-go pricing](https://platform.minimax.io/docs/guides/pricing-paygo)
- [xAI models and pricing](https://docs.x.ai/developers/models)
- [Kimi pricing](https://platform.kimi.ai/docs/pricing/chat)
