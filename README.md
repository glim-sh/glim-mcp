# glim.sh

### Live data for any agent.

One remote MCP endpoint gives your agent live data from Twitter/X, Reddit, the open web, GitHub, Amazon, YouTube, and public Telegram channels, plus AI-text detection. No API keys, no scraping stack - connect the URL and pay per call.

```
https://glim.sh/mcp
```

---

## Quick Start

```bash
# claude.ai - one click
open "https://claude.ai/customize/connectors?modal=add-custom-connector&connectorName=glim&connectorUrl=https%3A%2F%2Fglim.sh%2Fmcp"

# Claude Code
claude mcp add -s user -t http glim https://glim.sh/mcp

# Claude Code plugin (MCP server + usage skill, auto-updates)
claude plugin marketplace add glim-sh/glim-mcp
claude plugin install glim@glim

# Codex
codex mcp add glim --url https://glim.sh/mcp

# OpenCode (interactive: choose remote, paste the URL)
opencode mcp add

# Agent skill (any skills-aware agent)
npx skills add https://glim.sh --yes

# No account? Pay per call from a local crypto wallet (x402)
npx x402-proxy mcp add glim https://glim.sh/mcp
```

Any other MCP client: add the endpoint to your config.

```json
{
  "mcpServers": {
    "glim": {
      "url": "https://glim.sh/mcp"
    }
  }
}
```

On first use the client runs a browser OAuth sign-in. Manage your balance at [glim.sh/app](https://glim.sh/app). The wallet path needs no account at all: calls auto-pay USDC (Base or Solana) on x402 challenges; MPP on Tempo is accepted on the same endpoint.

## Tools

| Tool | Price | Use for |
| --- | --- | --- |
| `glim_twitter_search` | $0.005 | Search tweets with advanced operators |
| `glim_twitter_get` | $0.005 | Tweet with thread context, or user profile, by URL/id/handle |
| `glim_reddit_search` | $0.01 | Search Reddit posts |
| `glim_reddit_get` | $0.015 | Post + comments, subreddit feed, or user activity |
| `glim_web_search` | $0.01 | Semantic web search |
| `glim_web_fetch` | $0.002 | Clean page extraction (SSR, SPA shells, PDFs) |
| `glim_github_search` | $0.002 | Search GitHub repos, conversations, or code |
| `glim_github_get` | $0.002 | Repo metadata, files, history, PRs, issues |
| `glim_amazon_search` | $0.005 | Search Amazon listings with prices, ratings, ASINs |
| `glim_amazon_get` | $0.01 | Amazon product detail by ASIN |
| `glim_youtube_get` | $0.01 | YouTube subtitles/transcript by video id |
| `glim_telegram_search` | $0.01 | Discover public Telegram channels by name or topic |
| `glim_telegram_get` | $0.005 | Channel posts, in-channel history search, or post + discussion comments |
| `glim_detect_ai` | from $0.06 | Score text for AI authorship, with a per-segment breakdown |

Restrict the tool list per session with `?tools=`:

```
https://glim.sh/mcp?tools=glim_twitter_search,glim_web_fetch
```

## REST API

Every tool is also a plain REST endpoint under `https://glim.sh/api/v1/`, gated by the same payment challenges. Full spec: [glim.sh/openapi.json](https://glim.sh/openapi.json).

```bash
npx x402-proxy https://glim.sh/api/v1/twitter/get/cascade_fyi
```

## Documentation

For full documentation, visit [glim.sh/docs](https://glim.sh/docs).

## About this repo

This repo holds the registry manifests, the Claude Code plugin, and documentation for the glim MCP server - not the server source. Open an issue for listing or documentation fixes, or email [support@glim.sh](mailto:support@glim.sh).

## License

[MIT](LICENSE) (c) 2026 Misha Kolesnik
