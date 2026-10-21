# Ecommerce Store Discovery MCP Server

[![Smithery](https://smithery.ai/badge/mambabuilt/mcp-ecommerce-store-discovery)](https://smithery.ai/servers/mambabuilt/mcp-ecommerce-store-discovery) [![Glama score](https://glama.ai/mcp/servers/mambalabsdev/mcp-ecommerce-store-discovery/badges/score.svg)](https://glama.ai/mcp/servers/mambalabsdev/mcp-ecommerce-store-discovery) [![MCP Registry](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fregistry.modelcontextprotocol.io%2Fv0%2Fservers%3Fsearch%3Dcom.mambabuilt%252Fmcp-ecommerce-store-discovery%26limit%3D1&query=%24.servers%5B0%5D._meta%5B%22io.modelcontextprotocol.registry%2Fofficial%22%5D.status&label=mcp%20registry&color=blue)](https://registry.modelcontextprotocol.io/v0/servers?search=com.mambabuilt/mcp-ecommerce-store-discovery&limit=1) [![npm version](https://img.shields.io/npm/v/@mambalabsdev/mcp-ecommerce-store-discovery)](https://www.npmjs.com/package/@mambalabsdev/mcp-ecommerce-store-discovery) [![npm downloads](https://img.shields.io/npm/dm/@mambalabsdev/mcp-ecommerce-store-discovery)](https://www.npmjs.com/package/@mambalabsdev/mcp-ecommerce-store-discovery) [![license](https://img.shields.io/github/license/mambalabsdev/mcp-ecommerce-store-discovery)](https://github.com/mambalabsdev/mcp-ecommerce-store-discovery/blob/main/LICENSE) [![mcpservers.org](https://img.shields.io/badge/mcpservers.org-listed-blue)](https://mcpservers.org/servers/mambalabsdev/mcp-ecommerce-store-discovery)

An MCP server for the Mamba Labs Ecommerce Store Discovery actor on Apify. Give it product keywords and a platform. Each run finds stores through Google, confirms each one on its own homepage, and returns one row per store.

## What's Inside

- [What it does](#what-it-does)
- [Quick start](#quick-start)
- [Prerequisites](#prerequisites)
- [Example prompts](#example-prompts)
- [Tool](#tool)
- [Inputs](#inputs)
- [Pricing](#pricing)
- [Your keys](#your-keys)
- [Full actor documentation](#full-actor-documentation)
- [License](#license)

## What it does

- Searches Google with each keyword plus a footprint the platform prints on its stores, and drops marketplaces, social networks, and reference sites.
- Reads each candidate's robots.txt and homepage, and returns the store only when the homepage carries the platform's marks, with the evidence and a confidence.
- Per store: payment methods, subscription apps, currencies, Shopify product count, Tranco rank band and trend, contact emails, phone, and Instagram, Facebook, and TikTok links from the homepage.
- Unconfirmed sites are skipped and not charged.

All of the work runs on Apify. This package is a thin client that starts the actor run, waits for it, and hands back the dataset rows.

## Quick start

You need Node.js 18 or newer and an Apify account with an API token.

Add this to your Claude Desktop config (`claude_desktop_config.json`), Cursor, or any MCP client:

```json
{
  "mcpServers": {
    "mamba-ecommerce-store-discovery": {
      "command": "npx",
      "args": [
        "-y",
        "@mambalabsdev/mcp-ecommerce-store-discovery"
      ],
      "env": {
        "APIFY_TOKEN": "your-apify-token"
      }
    }
  }
}
```

Restart the client. The `discover_ecommerce_stores` tool appears.

## Prerequisites

- Node.js 18 or newer.
- An Apify API token from [console.apify.com/account/integrations](https://console.apify.com/account/integrations), set as `APIFY_TOKEN`. The server lists its tool without a token; a call needs one.

## Example prompts

- "Find 30 Shopify stores that sell coffee beans and show their product counts and contact emails."
- "Which WooCommerce stores in the UK sell dog treats?"
- "List BigCommerce stores selling auto parts, with their payment providers."

## Tool

`discover_ecommerce_stores`. One tool. Example arguments:

```json
{
  "keywords": ["coffee beans"],
  "platform": "shopify",
  "max_stores": "25"
}
```

## Inputs

Every buyer facing input of the actor, unchanged. Omitted inputs take the actor's own defaults. Numbers and booleans are sent as strings.

| Input | Type | Description |
|---|---|---|
| `keywords` | array | What the stores sell. Required |
| `platform` | string | shopify (default), woocommerce, bigcommerce, or any |
| `max_stores` | string | Confirmed stores to return, up to 500. Default 25 |
| `country` | string | Google market. Default US |
| `location_term` | string | Word added to every search |
| `language` | string | Google interface language. Default en |
| `include_product_count` | string | true or false. Default true |
| `include_traffic_rank` | string | true or false. Default true |
| `include_unconfirmed` | string | true or false. Default false |
| `exclude_domains` | array | Domains to skip |
| `max_search_pages` | string | Cap on Google pages read |
| `max_charge_usd` | string | Optional cost cap for the run |

## Pricing

Pay per event on Apify, billed to your Apify account. Prices in USD.

| Event | Free plan | Bronze | Silver | Gold |
|---|---|---|---|---|
| `store-found`, one confirmed store | $0.005 | $0.00475 | $0.0045 | $0.00425 |
| `search-page`, one Google result page read | $0.019 | $0.01805 | $0.0171 | $0.01615 |
| `apify-actor-start`, per run start | $0.002 | $0.002 | $0.002 | $0.002 |

Unconfirmed, refused, and failed sites are free.

## Your keys

The actor needs no key. It reads Google result pages through the Apify Google SERP proxy and the stores' own public pages, and holds no key of any kind. Mamba Labs pays the platform and proxy costs of the run.

## Full actor documentation

[apify.com/mambalabs/ecommerce-store-discovery](https://apify.com/mambalabs/ecommerce-store-discovery)

## License

MIT. See [LICENSE](LICENSE).
