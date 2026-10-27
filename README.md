# GTA6 Times MCP server

Free, read-only GTA 6 data for your assistant, from [gta6times.com](https://gta6times.com): the unlock time and price in each
country, which claims are confirmed and which are only rumors, the official trailers, and the latest labeled news.

- Endpoint: `https://gta6times.com/mcp` (Streamable HTTP, no sign-in, no key)
- Docs and example prompts: https://gta6times.com/developers
- Privacy: https://gta6times.com/privacy
- Contact: hello@gta6times.com

GTA6 Times is an independent fan site. It is not affiliated with Rockstar Games or Take-Two Interactive.

## Tools

| Tool | What it answers |
|---|---|
| `get_launch_countdown` | Days to launch and the unlock moments for New Zealand, the UK and the US East Coast |
| `get_unlock_time` | The unlock time in one country, from the PlayStation Store listing |
| `get_price` | Standard and Ultimate price in one country, with how firm the figure is and when it was read |
| `list_markets` | Every tracked market and the status of its price |
| `get_facts` | The fact database: confirmed, likely, unverified, rumor, false, outdated |
| `check_claim` | Whether a specific claim or rumor is true |
| `get_latest_news` | Newest stories with their labels and sources |
| `get_trailers` | The official videos and their dates |
| `search_gta6times`, `search`, `fetch` | Find a page and read it in full |

Every tool is read-only (`readOnlyHint: true`). Nothing is stored and no account is needed. The endpoint speaks MCP revision
2026-07-28 (stateless, `server/discover`) and still answers the earlier revisions on the same URL. It never issues a session id.

## For software that discovers servers

- Server Card: https://gta6times.com/mcp/server-card (also at `/.well-known/mcp/server-card.json`)
- API catalog (RFC 9727): https://gta6times.com/.well-known/api-catalog, AI catalog: https://gta6times.com/.well-known/ai-catalog.json
- OpenAPI description of the open datasets (CC BY 4.0): https://gta6times.com/openapi.json
- Agent skills: https://gta6times.com/.well-known/agent-skills/index.json (short instructions for answering GTA 6 questions with the status of each fact)
- Every page of the site is also available as markdown: send `Accept: text/markdown`, or add `.md` to the address.

## Add it to your assistant

**Claude Code**

```bash
claude mcp add --transport http gta6times --scope user https://gta6times.com/mcp
```

**Claude (claude.ai, Desktop, mobile)**: Customize, Connectors, Add custom connector, paste `https://gta6times.com/mcp`, set
Authentication to "No sign-in".

**ChatGPT**: Plugins, then add a custom MCP server with the URL above (available on plans that allow custom servers).

**Cursor**: [add with one click](cursor://anysphere.cursor-deeplink/mcp/install?name=gta6times&config=eyJ1cmwiOiJodHRwczovL2d0YTZ0aW1lcy5jb20vbWNwIn0=)
or add this to `~/.cursor/mcp.json`:

```json
{ "mcpServers": { "gta6times": { "url": "https://gta6times.com/mcp" } } }
```

**VS Code** (`.vscode/mcp.json`):

```json
{ "servers": { "gta6times": { "type": "http", "url": "https://gta6times.com/mcp" } } }
```

**Gemini CLI**: `gemini extensions install https://github.com/vijaygopalbalasa/gta6times-mcp` or add to `~/.gemini/settings.json`:

```json
{ "mcpServers": { "gta6times": { "httpUrl": "https://gta6times.com/mcp" } } }
```

**Perplexity, Mistral, Copilot Studio**: add a custom remote MCP connector with the URL above and no authentication.

**OpenAI Responses API**

```json
{ "type": "mcp", "server_label": "gta6times", "server_url": "https://gta6times.com/mcp", "require_approval": "never" }
```

**Check it works**

```bash
npx @modelcontextprotocol/inspector --cli https://gta6times.com/mcp --transport http --method tools/list
```

## Try these

- "What time does GTA 6 unlock in India, and what will it cost there?"
- "Is it confirmed that GTA 6 is coming to PC at launch?"
- "What are the latest GTA 6 stories and how firm is each one?"

## Claude Code plugin marketplace

```bash
claude plugin marketplace add vijaygopalbalasa/gta6times-mcp
claude plugin install gta6times@gta6times
```

## License

The files in this repository are MIT. The data served by the endpoint follows https://gta6times.com/terms.
