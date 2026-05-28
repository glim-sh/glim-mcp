# Glim MCP

[![standard-readme compliant](https://img.shields.io/badge/readme%20style-standard-brightgreen.svg?style=flat-square)](https://github.com/RichardLitt/standard-readme)

Hosted MCP server with data tools for AI agents.

Glim runs a single remote MCP endpoint at `https://glim.sh/mcp`. It exposes tools for Twitter, Reddit, web search and crawl, GitHub, Amazon, YouTube subtitles, and LLM inference. Sign in and top up your balance at [glim.sh/app](https://glim.sh/app); your calls are billed against that balance.

## Install

Add the endpoint to your MCP client config.

```json
{
  "mcpServers": {
    "glim": {
      "url": "https://glim.sh/mcp"
    }
  }
}
```

That is the entire install. Glim hosts the server; clients only need the URL.

## Configuration

Restrict the tool list per session with the `?tools=` query parameter:

```
https://glim.sh/mcp?tools=glim_twitter_search,glim_web_crawl
```

Omit `?tools=` to expose every tool.

## Contributing

This repo holds the registry manifest and documentation for the Glim MCP server, not the server source. Open an issue or PR at [github.com/glim-sh/glim-mcp](https://github.com/glim-sh/glim-mcp) for documentation fixes, registry-metadata changes, or questions.

## License

[MIT](LICENSE) (c) 2026 Misha Kolesnik
