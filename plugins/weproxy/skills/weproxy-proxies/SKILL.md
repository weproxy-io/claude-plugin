---
name: weproxy-proxies
description: Use when the user needs proxies for scraping, crawling, geo-testing or any HTTP requests through residential IPs, asks about their WeProxy quota, IP whitelist or usage, or wants code that uses WeProxy proxies. Uses the WeProxy MCP tools.
---

# Using WeProxy proxies

The `weproxy` MCP server gives access to one WeProxy order (Premium Rotating Residential).
Its tools appear as `mcp__plugin_weproxy_weproxy__<tool>`.

## Tools

| Tool | Use it for |
|---|---|
| `get_order_info` | Which order/product this key belongs to and its status. |
| `get_quota` | Remaining / used / total traffic (GB). |
| `get_proxies` | Proxy lines. Args: `country` (ISO-2 or `random`), `state`, `session` (`rotating`/`sticky`), `sticky_minutes` (1–1440), `format`, `count` (1–1000). |
| `list_countries`, `list_states` | Valid targeting values. |
| `list_whitelist`, `add_whitelist_ip`, `remove_whitelist_ip` | IP whitelist (needed only for the `host:port` format). |
| `get_usage` | Daily usage for `day`/`week`/`month`/`3months`/`6months`. |

## How to work

1. Before a large scraping job, call `get_quota` and tell the user the remaining traffic. Traffic is only consumed when data flows through a proxy; generating lines is free.
2. For code, request `format: "http_url"`. It returns `http://user:pass@host:port`, which works directly with requests, httpx, aiohttp, curl, and Playwright (Playwright: split into server/username/password, or use `host:port:user:pass`).
3. Use `session: "rotating"` (a new IP per request) for crawling many pages, and `session: "sticky"` with `sticky_minutes` when a site needs the same IP across a login or a multi-step flow.
4. For geo-targeting, check codes with `list_countries` / `list_states` instead of guessing. Use `country: "random"` when location does not matter.
5. Do not hardcode credentials the user did not ask to embed. Prefer reading proxies at runtime from the WeProxy REST API (`POST https://mcp.weproxy.io/v1/proxies` with `Authorization: Bearer $WEPROXY_KEY`), or put them in environment variables.
6. If a tool returns an error about an inactive order or an invalid key, tell the user to check the order in the WeProxy client area (or regenerate the key there).

Docs: https://mcp.weproxy.io
