# Changelog

All notable changes to the glim MCP tools are recorded here. The endpoint is
always live at `https://glim.sh/mcp` - these notes track what changed behind it.

## [1.1.0] - 2026-06-29

A tools-focused release: richer responses, fewer follow-up calls, and more
reliable data across every source.

### Reddit

- `glim_reddit_search` and subreddit feeds now return full post text plus the
  top comments inline, instead of metadata-only previews - a single search
  usually answers the question without a follow-up `get`.
- Native pagination: responses carry a next-page cursor and print a ready-to-run
  next-page call.
- `glim_reddit_get` comment threads are dramatically faster.

### Twitter / X

- `glim_twitter_search` now defaults to **Top** sort (most relevant first).
- Richer, more scannable text output: per-tweet quotes, bookmarks, and
  engagement rate; author account age; and search-summary totals (views, time
  span, average engagement).

### GitHub

- `glim_github_search` now speaks GitHub's full search syntax: qualifiers,
  boolean `AND`/`OR`/`NOT` with parentheses, `"exact strings"`, and `/regex/`.
- Code search now spans millions of public repositories with regex and
  symbol-definition search; empty searches auto-recover with concrete retry
  guidance.
- `glim_github_get` gains a lot of reach:
  - commit lookups with diff stats and patches (`/commit/<sha>` URLs)
  - parses raw, blob, and SSH GitHub URLs to the right file/repo
  - follows renamed/transferred repos
  - resolves any README filename (not just `README.md`)
  - fetches up to 100 comments and branches (was 30), with paging hints
  - subtree-scoped directory listings
  - clear not-found errors with browse hints instead of bare `(not found)`

### Amazon

- `glim_amazon_get` reaches full text/JSON parity: tech specs, review titles and
  bodies, description, and category (previously reviews showed metadata only).
- `glim_amazon_search` cards gain delivery date, stock, coupons and deals,
  best-seller and sales-volume signals, and floor price across sellers.
- New `offer_status` signal when no featured offer is available for your region
  - the product is still surfaced (price nullable) rather than silently dropped.
- Accepts a plain product URL as the reference.
- Fixed brand-only titles, false "Amazon's Choice" badges, and stray markup
  leaking into fields.

### Web

- `glim_web_fetch` adds a last-resort live-crawl fallback so hard-blocked pages
  still return content.
- More reliable crawling overall: lighter fetch path, per-domain route memory,
  crawl-budget enforcement, and hardened error handling.

### Across all tools

- Absolute UTC timestamps with a relative hint (e.g. `2026-06-09 14:30Z
  (2d ago)`) on posts, tweets, and comments.
- GitHub repo created/last-pushed and issue/PR created/updated dates.
- Amazon list price plus discount (`was X, -Y%`) and Sponsored flags.
- Web search relevance scores; web fetch title, author, and published date.
- YouTube canonical watch URL in the response.

### Reliability & fixes

- Amazon: recover from soft-blocks and cold-start timeouts; correctly classify
  not-found pages instead of treating them as blocks.
- Reddit: more consistent English-locale results.
- Payments: client-fault settlement failures now return a retryable `402`
  instead of a `502`.

[1.1.0]: https://github.com/glim-sh/glim-mcp/releases/tag/v1.1.0
