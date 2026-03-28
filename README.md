# 🛍️ Vinted MCP Server — Search, Compare Prices & Analyze Sellers

[![npm version](https://img.shields.io/npm/v/vinted-mcp-server.svg)](https://www.npmjs.com/package/vinted-mcp-server)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**The first MCP server for the Vinted marketplace.**

Give your AI assistant reliable access to Vinted listings, seller profiles, cross-country price comparison, and trend discovery across 19 countries without building and maintaining your own Vinted integration.

This server is ideal for Claude Desktop, Cursor, Windsurf, Cline, and any MCP-compatible client that needs structured Vinted data for shopping, sourcing, resale research, or marketplace intelligence workflows.

---

## ⚡ Quick Start

### Option 1: npx (zero install)

```json
{
  "mcpServers": {
    "vinted": {
      "command": "npx",
      "args": ["-y", "vinted-mcp-server"]
    }
  }
}
```

### Option 2: Global install

```bash
npm install -g vinted-mcp-server
```

Then add to your MCP client config:

```json
{
  "mcpServers": {
    "vinted": {
      "command": "vinted-mcp-server"
    }
  }
}
```

## Why This Exists

Vinted is a valuable marketplace for sourcing, price analysis, and resale research, but building a reliable integration is painful.

Most DIY approaches break because of anti-bot protection, unstable scraping methods, or the complexity of supporting multiple countries consistently.

This MCP server gives your AI tools a clean way to search, compare, and analyze Vinted data without rebuilding the same fragile infrastructure from scratch.

---

## 🔧 Client Configuration

### Claude Desktop

Add to `~/Library/Application Support/Claude/claude_desktop_config.json` (macOS) or `%APPDATA%\Claude\claude_desktop_config.json` (Windows):

```json
{
  "mcpServers": {
    "vinted": {
      "command": "npx",
      "args": ["-y", "vinted-mcp-server"]
    }
  }
}
```

### Cursor

Settings → MCP Servers → Add:

```json
{
  "mcpServers": {
    "vinted": {
      "command": "npx",
      "args": ["-y", "vinted-mcp-server"]
    }
  }
}
```

---

## 🛠️ Tools (5)

### `search_items`

Search Vinted listings with powerful filters.

| Parameter | Type | Description |
|-----------|------|-------------|
| `query` | string | Search keywords (required) |
| `country` | string | Country code — `fr`, `de`, `uk`, `it`, `es`, `nl`, `pl`, `pt`, `be`, `at`, `lt`, `cz`, `sk`, `hu`, `ro`, `hr`, `fi`, `dk`, `se` |
| `priceMin` | number | Minimum price |
| `priceMax` | number | Maximum price |
| `brandIds` | number[] | Filter by brand IDs |
| `categoryId` | number | Vinted category ID |
| `condition` | string[] | `new_with_tags`, `new_without_tags`, `very_good`, `good`, `satisfactory` |
| `sortBy` | string | `relevance`, `price_low_to_high`, `price_high_to_low`, `newest_first` |
| `limit` | number | Max results (up to 100) |

**Example prompt:** *"Search for Nike Air Max on Vinted France under 50€, sort by price"*

---

### `get_item`

Get full details for a specific Vinted item by ID.

| Parameter | Type | Description |
|-----------|------|-------------|
| `itemId` | number | Vinted item ID (required) |
| `country` | string | Country code |

**Example prompt:** *"Get details for Vinted item 4283719503"*

---

### `get_seller`

Analyze a Vinted seller's profile, ratings, and recent items.

| Parameter | Type | Description |
|-----------|------|-------------|
| `sellerId` | number | Vinted seller ID (required) |
| `country` | string | Country code |

**Example prompt:** *"Show me the profile of seller 12345678 on Vinted Germany"*

---

### `compare_prices`

Compare prices for an item across multiple Vinted countries.

| Parameter | Type | Description |
|-----------|------|-------------|
| `query` | string | Search keywords (required) |
| `countries` | string[] | Countries to compare (default: all) |
| `limit` | number | Items per country |

**Example prompt:** *"Compare prices for 'Levi's 501' across France, Germany, and Italy"*

---

### `get_trending`

Discover trending items on Vinted.

| Parameter | Type | Description |
|-----------|------|-------------|
| `country` | string | Country code |
| `categoryId` | number | Optional category filter |
| `limit` | number | Number of trending items |

**Example prompt:** *"What's trending on Vinted Netherlands right now?"*

---

## 📚 Resources (2)

### `vinted://countries`

Returns the full list of 19 supported Vinted countries with domain, currency, and language info.

### `vinted://categories`

Returns the Vinted category tree for filtering searches.

## What Your AI Agent Can Do With This

With this MCP server, your AI assistant can:

- find underpriced listings in specific countries
- compare prices for the same query across Europe
- analyze seller reputation and inventory
- discover trending products and categories
- support sourcing, shopping, arbitrage, and resale workflows
- act as a Vinted research layer inside larger agent systems

---

## Who This Is For

This MCP server is built for:

- AI builders creating shopping or sourcing assistants
- resale operators who want faster market intelligence
- developers building marketplace copilots
- researchers analyzing listings, prices, sellers, and trends
- teams who want Vinted data inside Claude, Cursor, or MCP-compatible tools

---

## 🌍 Supported Countries (19)

| Code | Country | Currency |
|------|---------|----------|
| `fr` | France | EUR |
| `de` | Germany | EUR |
| `uk` | United Kingdom | GBP |
| `it` | Italy | EUR |
| `es` | Spain | EUR |
| `nl` | Netherlands | EUR |
| `be` | Belgium | EUR |
| `at` | Austria | EUR |
| `pl` | Poland | PLN |
| `pt` | Portugal | EUR |
| `lt` | Lithuania | EUR |
| `cz` | Czech Republic | CZK |
| `sk` | Slovakia | EUR |
| `hu` | Hungary | HUF |
| `ro` | Romania | RON |
| `hr` | Croatia | EUR |
| `fi` | Finland | EUR |
| `dk` | Denmark | DKK |
| `se` | Sweden | SEK |

---

## 💡 Use Cases

- **🛒 AI Shopping Assistant** — "Find me a winter jacket under 30€ in good condition"
- **📊 Price Analysis** — "What's the average price for PS5 controllers across Europe?"
- **💰 Arbitrage** — "Find items priced lower in Poland that I can buy from France"
- **👤 Seller Research** — "Is this seller trustworthy? Show me their ratings and history"
- **📈 Trend Watching** — "What's trending in fashion on Vinted Germany?"

---

## Run the Same Engine at Scale

This MCP server is powered by the same core engine used in the cloud version.

If you need higher volume, direct cloud execution, scheduling, or production-scale runs, use the underlying actor on Apify:

👉 [Vinted Smart Scraper on Apify](https://apify.com/kazkn/vinted-smart-scraper)

If you want direct coding integrations instead of MCP, see the wrappers below.

## Related Projects

Programmatic wrappers:
- [vinted-scraper-python](https://github.com/KinderCN/vinted-scraper-python)
- [vinted-scraper-js](https://github.com/KinderCN/vinted-scraper-js)

Cloud-scale engine:
- [Vinted Smart Scraper on Apify](https://apify.com/kazkn/vinted-smart-scraper)

---

## 📄 License

MIT © KazKN
