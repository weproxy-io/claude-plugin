# WeProxy — Claude Code plugin

Use your **WeProxy Premium Rotating Residential** proxies directly in Claude Code: generate country/state-targeted rotating or sticky proxies, check your quota, manage your IP whitelist and see usage — through MCP tools.

## Install

```text
/plugin marketplace add weproxy-io/claude-plugin
/plugin install weproxy@weproxy
```

or from a shell:

```bash
claude plugin marketplace add weproxy-io/claude-plugin
claude plugin install weproxy@weproxy
```

When the plugin is enabled, Claude Code asks for your **WeProxy API key** (`wpk_…`). The key is stored in your OS credential store, not in any file.
Create the key in the WeProxy client area: your order → **Yapay Zeka (MCP) / API** tab → **Create API key**.

## What you get

- MCP server `weproxy` → `https://mcp.weproxy.io/mcp` with the tools `get_order_info`, `get_quota`, `get_proxies`, `list_countries`, `list_states`, `list_whitelist`, `add_whitelist_ip`, `remove_whitelist_ip`, `get_usage`.
- Skill `/weproxy:weproxy-proxies` that teaches Claude how to use them (quota check before big jobs, `http_url` format for code, rotating vs sticky).

Try: *"Give me 5 sticky proxies from Germany for 10 minutes"* or *"Write a scraper for these URLs using US rotating proxies"*.

## Links

- Docs & REST API: https://mcp.weproxy.io
- WeProxy: https://weproxy.io
