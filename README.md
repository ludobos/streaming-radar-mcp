# Streaming Radar MCP

[![smithery badge](https://smithery.ai/badge/lbostral/streaming-radar)](https://smithery.ai/servers/lbostral/streaming-radar)

Streaming and media intelligence MCP server. Vertical drama, Africa streaming, piracy, sports, creator economy. **155 tools, 4,000+ sourced datapoints**, OAuth 2.1 + Bearer auth, multi-AI client (Claude, ChatGPT, Cursor, Copilot, Perplexity, Grok).

This repository is the **public listing** for the Streaming Radar MCP server. The server itself is a Cloudflare Worker hosted at `https://streaming-radar-mcp.streamingradar.workers.dev`. Source code is private.

- Live page: https://lens.streaming-radar.com/mcp
- Stats endpoint: https://streaming-radar-mcp.streamingradar.workers.dev/stats
- Author: Ludovic Bostral, Bostral & Co
- Newsletter: https://www.streaming-radar.com

## What is this?

Streaming Radar exposes the data, models, and editorial output of [Streaming Lens](https://lens.streaming-radar.com) through Model Context Protocol. Connect your AI client and query in natural language. Every answer is sourced, dated, confidence-scored.

The server backs:

- 5 report data silos: Vertical Invasion 2026, Africa Streaming 2026, Piracy Streaming 2026, Creator Economy 2026, Sports Streaming 2026
- The Streaming Radar newsletter (70+ articles, 35+ podcasts, expert directory)
- In-house analytical models: P&L, DCF, ASRI scores, market scenarios, unit economics

## Capabilities

| Surface | Tools | Tier |
|---------|-------|------|
| Newsletter | 8 | Free |
| Dataviz aggregation (Plotly-ready JSON) | 1 | Free |
| Per-report silos | 6 each | Paid |
| Strategic models | 10 | Paid |
| CRM, leads, webhooks, analytics, admin | 25+ | Admin |

## Authentication

Two paths, both supported by the same worker:

1. **OAuth 2.1 + PKCE** (recommended for Claude.ai, ChatGPT Custom Connectors). The worker implements RFC 8414 and RFC 7591.
2. **Bearer token** (recommended for Cursor, scripts, server-side integrations): `Authorization: Bearer sl_live_<32hex>`.

Free keys grant access to newsletter tools only. The Professional tier (299 EUR / month) unlocks the report silos plus analytical models.

## Connect

### Claude Desktop

```json
{
  "mcpServers": {
    "streaming-radar": {
      "command": "npx",
      "args": [
        "-y", "mcp-remote",
        "https://streaming-radar-mcp.streamingradar.workers.dev",
        "--header", "Authorization: Bearer sl_live_YOUR_KEY"
      ]
    }
  }
}
```

### Claude.ai (OAuth)

Settings → Connectors → Add Custom Connector → URL: `https://streaming-radar-mcp.streamingradar.workers.dev`

### ChatGPT Developer Mode

Settings → Profile → enable Developer Mode → Connectors → Add Custom Connector → URL above → OAuth or Bearer.

### ChatGPT standard mode (Deep Research, Company Knowledge)

Settings → Connectors → Add Custom Connector → URL: `https://streaming-radar-mcp.streamingradar.workers.dev/chatgpt` → Bearer. Exposes only `search` and `fetch` (the surface ChatGPT standard mode accepts).

### Other clients

Cursor, Continue.dev, Zed, Microsoft Copilot, Perplexity, Grok: same URL, Bearer token.

## Example prompts

```
What did Streaming Radar publish about Holywater this year?
Compare ReelShort and DramaBox unit economics, latest quarter.
What is the DCF valuation of the vertical drama market, base scenario?
What is the ASRI score for Nigeria and Kenya in 2026?
Mobile-money penetration in Kenya per GSMA, latest figure.
Which markets show both high piracy and low ARPU?
Compare creator economy revenue in France vs Brazil.
```

## Pricing

- **Free**: 8 newsletter tools, 1 dataviz tool, 100 requests / day soft cap.
- **Professional**: 299 EUR / month, all silos plus analytical models, 60 requests / minute, monthly cancellation, Stripe billing. Subscribe at https://lens.streaming-radar.com/mcp
- **Advisory**: tailored entitlements and on-call analyst time. Contact for quote.

## Live counters

`GET https://streaming-radar-mcp.streamingradar.workers.dev/stats` returns a JSON with `tools_count`, `datapoints_count`, `requests_7d`, `active_clients`, `last_updated`. Public, CORS-permissive, KV-cached 5 minutes, refreshed by a daily cron at 02:00 UTC.

## Versions

- Worker: v1.3.2 (May 2026)
- MCP spec: 2024-11-05

## Author

Ludovic Bostral, founder of Streaming Lens (Bostral & Co), former CTO at Afrostream, 25 years in media and streaming.

- LinkedIn: https://www.linkedin.com/in/ludovicbostral/
- Newsletter: https://www.streaming-radar.com
- Contact: ludovic@streaming-radar.com

## License

MIT for this listing repository (README + manifests). The MCP server source code is proprietary.
