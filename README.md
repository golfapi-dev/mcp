<img src="assets/birdie.png" alt="Birdie, the GolfAPI.dev mascot" width="72" align="right" />

# GolfAPI.dev MCP server

Golf club specifications as each maker published them, for AI assistants and agents. The server reads the GolfAPI.dev catalog: lofts, lies, head volume, hands, adjustable hosels, release dates and US launch prices for 2,700+ club models released 2000 to 2026, from drivers to putters. A field the maker did not publish is left out, not guessed.

- Server URL: `https://mcp.golfapi.dev` (Streamable HTTP, read-only)
- Setup guide for every client: [golfapi.dev/mcp](https://golfapi.dev/mcp?ref=github)
- Reference: [golfapi.dev/docs/mcp](https://golfapi.dev/docs/mcp/?ref=github)
- Free API key: [console.golfapi.dev](https://console.golfapi.dev/?plan=free&ref=github)

This repository holds the plugin package that the Cursor Marketplace and other agent-plugin directories read: [`plugin.json`](plugin.json), [`mcp.json`](mcp.json) and the logo. The server itself runs at the URL above.

## Connect

Clients that support OAuth (Claude, ChatGPT and Grok connectors, VS Code) open a GolfAPI.dev page that asks for your API key once. Paste the full `sk_live_` or `sk_test_` secret.

Clients that send headers can pass the key directly. Set it in your shell first:

```sh
export GOLFDEV_API_KEY='sk_live_...'
```

| Client | Setup |
| --- | --- |
| Claude | Settings, Connectors, Add custom connector, URL `https://mcp.golfapi.dev` |
| Claude Code | `claude mcp add --transport http golfapi https://mcp.golfapi.dev --header "Authorization: Bearer $GOLFDEV_API_KEY"` |
| Cursor | Install from the Cursor Marketplace, or add the block below to `~/.cursor/mcp.json` |
| VS Code | Add `{"servers": {"golfapi": {"type": "http", "url": "https://mcp.golfapi.dev"}}}` to `.vscode/mcp.json` |
| ChatGPT | Settings, Connectors, add a custom connector with the server URL |

Cursor, with the key from your environment:

```json
{
  "mcpServers": {
    "golfapi": {
      "url": "https://mcp.golfapi.dev",
      "headers": { "Authorization": "Bearer ${env:GOLFDEV_API_KEY}" }
    }
  }
}
```

Step-by-step setup for Claude, ChatGPT, Gemini, Grok, Claude Code, Cursor, VS Code and Codex is at [golfapi.dev/mcp](https://golfapi.dev/mcp?ref=github).

## Tools

Every tool is a read. Each call is one request on your plan and reads only what your key can read.

| Tool | What it does |
| --- | --- |
| `describe_api` | Club types, routes, what this key can read and the catalog build it reads now. Call it first |
| `search_clubs` | Clubs of one type, newest first, filtered by text, maker, family, release year, hand, loft, women's designation or adjustable hosel |
| `get_club` | One club's document by `clb_` id or slug, optionally narrowed to one hand or loft |
| `get_coverage` | Clubs per maker and release year, and how many clubs carry each field |
| `get_changes` | Catalog releases after a build you already read, with each club added, updated, corrected or removed |
| `api_get` | A GET to any API path the other tools do not cover |

## Example prompts

- Which 2025 drivers come in 10.5 degrees left-handed?
- Compare the lofts and head volume of two drivers I name.
- What club types can my GolfAPI.dev key read?
- How many drivers does the catalog hold for each maker and release year?

## Plans

| Plan | Reads |
| --- | --- |
| Free | A fixed sample: 20 drivers from 10 makers released in 2025, 2 mini-drivers and 2 fairway woods, specifications only |
| Hobby | All seven club types, 2,700+ models, specifications only |
| Pro | Adds US launch prices and allows commercial use |

Prices and limits: [golfapi.dev/pricing](https://golfapi.dev/pricing/?ref=github).

## Support

hello@golfapi.dev. Terms: [golfapi.dev/terms](https://golfapi.dev/terms/). Privacy: [golfapi.dev/privacy](https://golfapi.dev/privacy/).

## License

The files in this repository are MIT licensed. Catalog data read through the server is covered by the [GolfAPI.dev Terms](https://golfapi.dev/terms/) and data license.
