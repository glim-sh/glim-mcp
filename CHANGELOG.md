# Changelog

## [1.2.0](https://github.com/glim-sh/glim-mcp/compare/v1.1.0...v1.2.0) - 2026-08-07

### <!-- 1 -->🎉 New Features
- **detect:** new `glim_detect_ai` tool - score any text for AI authorship. Returns an overall verdict (AI / human / mixed) with confidence, AI/human/AI-assisted fractions, and a segment-by-segment breakdown showing exactly which parts read as AI-written. Use it to verify third-party content, or to check a draft before publishing and revise the flagged segments. `tier=premium` uses the highest-accuracy detection class and additionally flags humanized text (AI output run through paraphrasing tools). Priced by length: $0.06 per 1,000 words standard / per 100 words premium (rounded up, minimum $0.06); texts under ~100 words automatically run on the premium detector at the standard price. Also available as REST `POST /api/v1/detect/ai`

**Full Changelog**: https://github.com/glim-sh/glim-mcp/compare/v1.1.0...v1.2.0

## [1.1.0](https://github.com/glim-sh/glim-mcp/compare/v1.0.0...v1.1.0) - 2026-06-29

A tools-focused release: richer responses, fewer follow-up calls, and more reliable data across every source. The endpoint at `https://glim.sh/mcp` picks it all up live - no client changes needed.

### <!-- 1 -->🎉 New Features
- **reddit:** search and subreddit feeds return full post text plus top comments inline (was metadata-only previews), so one search usually answers the question; responses carry a native next-page cursor and print a ready-to-run next-page call
- **twitter:** search defaults to **Top** sort (most relevant first); text output adds per-tweet quotes, bookmarks, and engagement rate, author account age, and search-summary totals (views, time span, average engagement)
- **github:** `glim_github_search` now speaks GitHub's full search syntax - qualifiers, boolean `AND`/`OR`/`NOT` with parentheses, `"exact strings"`, and `/regex/`; code search spans millions of public repos with regex and symbol-definition search
- **github:** `glim_github_get` gains commit lookups with diff stats (`/commit/<sha>`), raw/blob/SSH URL parsing, renamed-repo follow, any-README resolution, up to 100 comments and branches per page (was 30), subtree-scoped directory listings, and not-found errors with browse hints
- **amazon:** `glim_amazon_get` reaches full text/JSON parity - tech specs, review titles and bodies, description, and category (was metadata-only reviews); accepts a plain product URL as the ref
- **amazon:** `glim_amazon_search` cards gain delivery date, stock, coupons and deals, best-seller and sales-volume, and floor price across sellers, plus an `offer_status` signal when no featured offer exists for your region (product still surfaced, price nullable)
- **web:** `glim_web_fetch` adds a last-resort live-crawl fallback so hard-blocked pages still return content
- **all tools:** absolute UTC timestamps with a relative hint (e.g. `2026-06-09 14:30Z (2d ago)`) on posts, tweets, and comments; GitHub repo created/last-pushed and issue/PR created/updated dates; Amazon list price plus discount (`was X, -Y%`) and Sponsored flags; web search relevance scores; web fetch title, author, and published date; YouTube canonical watch URL

### <!-- 2 -->🐛 Bug Fixes
- **amazon:** classify genuinely not-found products correctly instead of retrying them as transient failures; recover gracefully from intermittent upstream blocks and slow first responses; fix brand-only titles, false "Amazon's Choice" badges, stray markup leaking into fields, and an empty-result crash
- **github:** fix silent mis-parse traps and output gaps in `glim_github_get`; auto-recover empty code searches with concrete retry guidance
- **reddit:** more consistent English-locale results
- **web:** harden `glim_web_fetch` error paths
- **payment:** return a retryable `402` instead of a `502` when a payment can't be settled due to a client-side issue

### <!-- 3 -->🚀 Performance
- **reddit:** comment threads and post hydration are dramatically faster (`glim_reddit_get` **~10s -> ~0.4s**), and fetched posts stay warm across requests

**Full Changelog**: https://github.com/glim-sh/glim-mcp/compare/v1.0.0...v1.1.0
