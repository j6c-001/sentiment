# sentiment

A server-side sentiment + trend aggregator that monitors a small allowlist of public sources (RSS + Reddit, optionally X) and produces a unified, de-duplicated stream of “items” with sentiment scores and rolling aggregates.

This project is designed to:
- Pull fresh items on a schedule (polling).
- Normalize them into a common schema.
- Score sentiment per item (lexicon/model).
- Store and serve results for a  dashboard/API.

## Features

- **Multi-source ingestion**
  - RSS feeds (e.g., finance/news headlines)
  - Reddit Data API: `/r/{sub}/new` (script app credentials)
  - Optional: X search API
  - Other (confifurable) Public Market feeds

- **Normalization**
  - Converts each source into a single `ScoredItem` schema:
    - `id`, `source`, `text`, `url`, `ts_utc`, `sentiment`, optional `topic`

- **Spam reduction**
  - Reddit: optional `text_only` mode (keeps self-posts only)
  - X: recommended `-has:links` when you want to drop link spam

- **Aggregation**
  - Rolling statistics per topic (mean sentiment, volume, “hotness”)

## Requirements

- C++17+
- `cpp-httplib` (HTTPS enabled)
- `nlohmann/json`

If using HTTPS with `cpp-httplib`, ensure OpenSSL support is enabled.


