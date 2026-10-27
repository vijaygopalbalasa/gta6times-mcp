# Install the GTA6 Times MCP server

This is a hosted server. There is nothing to download, build or run, and it needs no API key.

1. Add a remote MCP server named `gta6times` that uses Streamable HTTP and this URL: `https://gta6times.com/mcp`
2. Set authentication to none.
3. Confirm it works: list the tools. Eleven read-only tools should come back, among them `get_unlock_time`, `get_price`, `check_claim`
   and `get_latest_news`.

Configuration for clients that read a JSON file:

```json
{
  "mcpServers": {
    "gta6times": {
      "url": "https://gta6times.com/mcp"
    }
  }
}
```

Cline stores remote servers with the transport type:

```json
{
  "mcpServers": {
    "gta6times": {
      "type": "streamableHttp",
      "url": "https://gta6times.com/mcp",
      "disabled": false
    }
  }
}
```

Example first request after install: "What time does GTA 6 unlock in the United Kingdom?" (uses `get_unlock_time` with `country: "UK"`).

Docs: https://gta6times.com/developers
