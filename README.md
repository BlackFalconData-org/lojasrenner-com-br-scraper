# Lojas Renner Scraper [💰$2.7]

Extract structured data from [lojasrenner.com.br](https://lojasrenner.com.br) — lojasrenner.com.br — Lojas Renner fashion products by category or keyword with price, discount and installments, plus sizes, colours, stock and images for every colour variant, for price monitoring and catalog tracking, exported as JSON or CSV.

**[Lojas Renner Scraper [💰$2.7] on Apify →](https://apify.com/blackfalcondata/lojasrenner-com-br-scraper?fpr=1h3gvi)**

---

## 🚀 How to use this actor

> ### 💚 $5 free Apify credits — every month
> No credit card required. No commitment. Cancel anytime.

### 👉 [Sign up free on Apify →](https://console.apify.com/sign-up?fpr=1h3gvi)

1. **Click sign up** — pick GitHub, Google, or email; takes ~30 seconds
2. **Open this actor** — input is pre-filled with a working example
3. **Click Start** — export results as JSON, CSV, or Excel

Your **$5 monthly platform credit** is enough to run this actor right away — and again every month — scraping typically several hundred to several thousand results per run, depending on your input.

## Key features

**Search with filters** — Search by keyword and location. Filter by 📝 description format, and more.

**Detail enrichment** — Fetch full descriptions, structured metadata for each product.

**Incremental mode** — Only get new or changed products since your last run. Content hash per product — no duplicates, no re-processing.

**Change classification** — Track unchanged, expired, cross-run duplicate detection across runs. Build audit trails of how products evolve over time.

**Compact output** — Emit core fields only (AI-agent / MCP-friendly). Keeps response size small for LLM workflows.

**Description truncation** — Cap description length per ${NOUN} to control output size and cost.

**Result cap** — Stop after N products (up to 1.000). Set to 0 for the full catalog.

**Export anywhere** — Download as JSON, CSV, or Excel. Stream via Apify API, webhooks, or integrations with Make, Zapier, Airbyte, Keboola.

**Structured data** — Every product returns the same schema with consistent field naming. All fields always present — `null` when unavailable, never omitted.

---

## Use cases

**Data pipeline automation**
Integrate with your ETL pipeline to collect structured products from lojasrenner.com.br on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor products, track trends, and analyze market dynamics with structured, deduplicated data from lojasrenner.com.br.

**Change monitoring**
Run daily or hourly in incremental mode to capture only new, updated, or expired ${NOUNS}. Perfect for price-tracking, churn analysis, and alerting pipelines.

**AI / LLM training data**
Structured JSON per product is ready for RAG pipelines, embeddings, and agent workflows. Compact mode trims tokens for LLM context windows.

---

## Quick start

```json
{
  "query": "camiseta",
  "location": "feminino",
  "maxResults": 100,
  "includeDetails": true,
  "descriptionMaxLength": 0,
  "compact": false,
  "excludeEmptyFields": false,
  "incrementalMode": false,
  "skipReposts": false,
  "notifyOnlyChanges": false,
  "notificationLimit": 5,
  "descriptionFormat": "all"
}
```

---

## Input parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `query` | string | — | Product keyword, searched inside the selected category. Leave empty to browse the whole category. Use a JSON array for several keywords, e.g. ["camiseta","vestido"]. |
| `location` | string | — | Which catalog section to search: `feminino`, `masculino`, `infantil`, a lojasrenner.com.br category URL (…/-/N-<id>), or a bare dimension id. Defaults to `feminino`. Use a JSON array for several categories. |
| `maxResults` | integer | `100` | Maximum total results (0 = unlimited). |
| `startUrls` | array | `[]` | Paste raw search URLs from the target site. Each URL becomes its own search task; results are merged and deduped by listing ID across all URLs. When provided, startUrls REPLACE the query/location fields (each supported URL becomes one task; unsupported URLs are skipped, and if none is supported the run stops with an input error). |
| `includeDetails` | boolean | `true` | Fetch each product's detail page for description, sizes, colors, full image gallery and promotions. |
| `descriptionMaxLength` | integer | `0` | Truncate description to N chars. 0 = no truncation. |
| `compact` | boolean | `false` | Core fields only (for AI-agent/MCP workflows). |
| `excludeEmptyFields` | boolean | `false` | Drop null, empty-string, and empty-array fields from each record before push. Smaller payloads for AI agents and dashboards. |
| `incrementalMode` | boolean | `false` | Compare against previous run state. stateKey is optional — defaults to a value derived from search inputs (queries, locations, startUrls) so different filter sets never share state. |
| `stateKey` | string | — | Optional. Stable identifier for the tracked search universe. Leave empty to auto-generate from search inputs. |
| `emitUnchanged` | boolean | `false` | When incremental, also emit records that haven't changed. |
| `emitExpired` | boolean | `false` | When incremental, also emit records no longer found. |
| `skipReposts` | boolean | `false` | When incremental, skip listings whose content matches an expired listing from a prior run (cross-run duplicate detection). |
| `notifyOnlyChanges` | boolean | `false` | When Incremental Mode is on, only send notifications for NEW and UPDATED listings. Has no effect outside incremental mode. |
| `notificationLimit` | integer | `5` | Maximum number of listings included in each notification message (1–20). |
| `telegramToken` | string | — | Telegram bot token (from @BotFather). Required for Telegram notifications. |
| `telegramChatId` | string | — | Telegram chat or channel ID (e.g. "-100123456789"). Required when telegramToken is set. |
| `discordWebhookUrl` | string | — | Discord incoming webhook URL. Server Settings → Integrations → Webhooks → New Webhook. |
| `slackWebhookUrl` | string | — | Slack incoming webhook URL. api.slack.com/messaging/webhooks. |
| `whatsappPhoneNumberId` | string | — | Your WhatsApp Business phone-number ID (numeric, from Meta dashboard). Required when whatsappAccessToken is set. |
| `whatsappAccessToken` | string | — | WhatsApp Cloud API permanent access token (System User token from Meta Business). Recipient must have messaged the business number within the last 24h (service-conversation window — free since Nov 2024). |
| `whatsappTo` | string | — | Recipient phone in E.164 format without + (e.g. "436641234567"). Recipient must have messaged your business number within last 24h. |
| `webhookUrl` | string | — | Receives a JSON POST with {metadata, items} after each run. Universal escape hatch for n8n / Make / Zapier / custom backends. |
| `webhookHeaders` | object | — | Optional JSON object of custom headers (e.g. {"Authorization":"Bearer ..."}). |
| `appConnector` | string | — | Optional. Pick a connected app under Settings → API & Integrations to receive your results (including any contact details). Best-effort across MCP connectors as Apify expands its catalog. |
| `mcpIssueTeam` | string | — | Only when the connected app is an issue tracker: the team (name or ID) the summary issue is created under, if that app requires one. |
| `descriptionFormat` | enum | `"all"` | Choose which representation of the listing description to include. `all` keeps every variant; the others keep only the selected one. |

---

## Output fields

Every product returns the same 56-field schema. Missing values are `null` — never omitted.

- `status`
- `country`
- `source`
- `search_term`
- `page`
- `rank`
- `product_id`
- `parent_product_id`
- `sku_id`
- `sku_ids`
- `title`
- `brand`
- `category`
- `subcategory`
- `categories`
- `gender`
- `price`
- `list_price`
- `discount_percent`
- `currency`
- `seller_name`
- `available`
- `sizes`
- `colors`
- `installments`
- `installment_price`
- `promotions`
- `image_url`
- `source_url`
- `search_url`
- `scraped_at`
- `error_message`
- `description`
- `thumbnail_url`
- `image_urls`
- `brand_logo_url`
- `category_paths`
- `color_key`
- `variant`
- `stock_status`
- `stock_level`
- `sold_last_15_days`
- `is_on_sale`
- `purchasable`
- `out_of_stock`
- `installments_without_interest`
- `credit_card_installments`
- `virtual_try_on`
- `listingId`
- `portalUrl`
- `searchQuery`
- `contentQuality`
- `detailFetched`
- `scrapedAt`
- `contentHash`
- `changeType`

---

## Sample output

One object per product. Here is a real example from a production run:

```json
{
  "status": "ok",
  "country": "BR",
  "source": "lojasrenner.com.br",
  "search_term": "camiseta",
  "page": 1,
  "rank": 1,
  "product_id": "931448946-COR931448946-11-1006TCX",
  "parent_product_id": "931448946",
  "sku_id": "931518748",
  "sku_ids": [
    "931518713",
    "931518721",
    "931518730",
    "931518748"
  ],
  "title": "Blusa Box em Viscose Floral com Alça Larga",
  "brand": "Marfinno"
}
```

*Truncated — full records contain 56 fields. See Output fields for the complete schema.*

**[Try Lojas Renner Scraper [💰$2.7] now — $5 free credit, no credit card →](https://apify.com/blackfalcondata/lojasrenner-com-br-scraper?fpr=1h3gvi)**

---

## Pricing

Pay only for what you extract. No subscription required — Apify's free $5 credit covers thousands of results.

| Event | Price (USD) |
| --- | --- |
| Actor Start | $0.01 |
| Result | $0.0027 |

See the [actor on Apify](https://apify.com/blackfalcondata/lojasrenner-com-br-scraper?fpr=1h3gvi) for current pricing.

---

## FAQ

**How do I scrape lojasrenner.com.br?**
Use this actor on Apify to extract structured data from lojasrenner.com.br. Configure your search query and filters in the input, then click Start — no coding required.

**How do I get lojasrenner.com.br data as JSON, CSV, or Excel?**
The actor writes each product to Apify's dataset. Download as JSON, CSV, or Excel from the Console, stream via the API, or push to Make, Zapier, Airbyte, or Keboola.

**Is it legal to scrape lojasrenner.com.br?**
Web scraping of publicly available data is generally legal. This actor only accesses publicly visible information. Always check lojasrenner.com.br's terms of service for your specific use case.

**How much does it cost?**
Pay-per-event pricing — you only pay for ${NOUNS} extracted. Apify's free $5 credit is enough to run thousands of results before you pay anything.

**How does incremental mode work?**
Each product gets a content hash. On subsequent runs, only new or changed products are emitted — saving time, compute, and storage. Expired products can be tracked separately.

**Do I need an API key or credentials?**
No. Just sign up for Apify, paste your input, and click Start. No credit card required.

---

## Related products by Black Falcon Data

[Browse all Black Falcon Data actors →](https://apify.com/blackfalcondata?fpr=1h3gvi)

---

## Getting started with Apify

New to Apify? [Create a free account with $5 credit](https://console.apify.com/sign-up?fpr=1h3gvi) — no credit card required.

1. Sign up — $5 platform credit included
2. Open [Lojas Renner Scraper [💰$2.7]](https://apify.com/blackfalcondata/lojasrenner-com-br-scraper?fpr=1h3gvi) and configure your input
3. Click **Start** — export results as JSON, CSV, or Excel

Need more later? [See Apify pricing](https://apify.com/pricing?fpr=1h3gvi).

---

## About Black Falcon Data

Black Falcon Data builds production-grade web scrapers for job boards and marketplace data. Browse our full actor catalog at [www.blackfalcondata.com](https://www.blackfalcondata.com).

---

*Last updated: 2026 10*
