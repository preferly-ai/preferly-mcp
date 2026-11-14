<p align="center"><img src="assets/logo.png" width="96" height="96" alt="Preferly logo"></p>

# Preferly MCP server

Free AI visibility checks for any website, inside Claude, ChatGPT, Cursor, VS Code and any other AI tool that speaks the Model Context Protocol (MCP). Ask your assistant whether AI crawlers can reach a site, whether its llms.txt and business schema are right, and whether AI can read its hours and prices, and it runs [Preferly](https://www.preferly.ai)'s checks for you.

```
https://www.preferly.ai/mcp
```

**Streamable HTTP · No sign-up · No API key · Read-only**

This is a hosted (remote) server, so there is nothing to install or run. This repository holds the documentation and ready-made configs. The server itself runs at preferly.ai.

[![Add to Cursor](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/en/install-mcp?name=preferly&config=eyJ1cmwiOiJodHRwczovL3d3dy5wcmVmZXJseS5haS9tY3A%2FY2xpZW50PWN1cnNvciJ9)
[![Install in VS Code](https://img.shields.io/badge/VS_Code-Install_Preferly-0098FF?logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect/mcp/install?name=preferly&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fwww.preferly.ai%2Fmcp%3Fclient%3Dvscode%22%7D)
[![Install in VS Code Insiders](https://img.shields.io/badge/VS_Code_Insiders-Install_Preferly-24bfa5?logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect/mcp/install?name=preferly&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fwww.preferly.ai%2Fmcp%3Fclient%3Dvscode%22%7D&quality=insiders)

- Server card: https://www.preferly.ai/.well-known/mcp/server-card.json
- Official MCP Registry: [`ai.preferly/preferly`](https://registry.modelcontextprotocol.io/v0/servers?search=ai.preferly/preferly)
- Website: https://www.preferly.ai · Free tools: https://www.preferly.ai/tools

## Tools

Every tool is read-only and works on one public website per call. None of them changes anything on the site.

| Tool | Input | What it does |
|---|---|---|
| `check_ai_crawler_access` | `website` | Whether the site's robots.txt lets 10+ AI crawlers in (GPTBot, OAI-SearchBot, ChatGPT-User, ClaudeBot, PerplexityBot, Google-Extended and more) and which rule decides each one; whether the homepage loads for them or shows a bot check; whether it has /llms.txt; its structured data types. |
| `generate_ai_robots_txt` | `allow_search` (default true), `allow_training` (default false), optional `disallow_paths` | robots.txt lines that let AI search and assistant crawlers in and keep training crawlers out, or any mix. Fetches nothing. |
| `check_llms_txt` | `website` | Whether the site publishes /llms.txt, its size and title, and what doesn't follow the llmstxt.org format, with line numbers. |
| `check_business_schema` | `website` | The business described in the homepage's structured data (JSON-LD): its type, and which fields are present, missing or look off. |
| `check_business_info` | `website` | Whether the site's name, phone, email, address, hours and prices are readable as text without running scripts. |
| `quick_ai_visibility_check` | `website` | Asks 3 AI models 3 typical customer questions about the business, from its public website, and reports whether each named it and where one contradicts the website. |

The live list is always in the [server card](https://www.preferly.ai/.well-known/mcp/server-card.json) and the server's `tools/list`.

## Set up

Most clients only need the URL. Adding `?client=<your tool>` helps us count which tools people use; it's optional.

### Any client, one command

```bash
npx add-mcp https://www.preferly.ai/mcp
```

[add-mcp](https://www.npmjs.com/package/add-mcp) finds the MCP clients on your computer and adds Preferly to them.

### Claude Code

```bash
claude mcp add --transport http preferly "https://www.preferly.ai/mcp?client=claude"
```

### Claude (claude.ai and Claude Desktop)

Open **Settings → Connectors → Add custom connector**.
- Name: `Preferly`
- URL: `https://www.preferly.ai/mcp?client=claude`

Leave authentication empty and save. Then turn Preferly on from the tools menu in a chat. Custom connectors are available on Claude's paid plans.

### ChatGPT (developer mode)

In ChatGPT on the web, open **Settings → Apps → Advanced settings**, turn on **Developer mode**, then choose **Create app**.
- Name: `Preferly`
- MCP server URL: `https://www.preferly.ai/mcp`
- Authentication: **No authentication**

Whether developer mode is available depends on your plan and workspace settings. A listed Preferly app for ChatGPT is in review.

### Cursor

Use the **Add to Cursor** button above, or add this to `~/.cursor/mcp.json` (or `.cursor/mcp.json` in a project):

```json
{
  "mcpServers": {
    "preferly": { "url": "https://www.preferly.ai/mcp?client=cursor" }
  }
}
```

### VS Code (GitHub Copilot)

Use the **Install in VS Code** button above. You can also run **MCP: Add Server** → **HTTP** and paste `https://www.preferly.ai/mcp?client=vscode`, or add this to `.vscode/mcp.json`:

```json
{
  "servers": {
    "preferly": { "type": "http", "url": "https://www.preferly.ai/mcp?client=vscode" }
  }
}
```

### Windsurf

Add to `~/.codeium/windsurf/mcp_config.json`:

```json
{
  "mcpServers": {
    "preferly": { "serverUrl": "https://www.preferly.ai/mcp?client=windsurf" }
  }
}
```

### Cline

Open the MCP Servers panel → **Remote Servers**, name it `preferly` and paste `https://www.preferly.ai/mcp?client=cline`. You can also add this to `cline_mcp_settings.json`:

```json
{
  "mcpServers": {
    "preferly": { "type": "streamableHttp", "url": "https://www.preferly.ai/mcp?client=cline" }
  }
}
```

To let Cline set it up for you, point it at [llms-install.md](llms-install.md).

### Codex

```bash
codex mcp add preferly --url "https://www.preferly.ai/mcp?client=codex"
```

### Gemini CLI

Add to `~/.gemini/settings.json`:

```json
{
  "mcpServers": {
    "preferly": { "httpUrl": "https://www.preferly.ai/mcp?client=gemini" }
  }
}
```

### Goose

Run `goose configure` → **Add Extension** → **Remote Extension (Streamable HTTP)**, name it `preferly` and use `https://www.preferly.ai/mcp?client=goose`.

### Zed

Add to your Zed `settings.json`:

```json
{
  "context_servers": {
    "preferly": { "url": "https://www.preferly.ai/mcp?client=zed" }
  }
}
```

If your Zed version only runs local servers, use the bridge instead: `"command": "npx", "args": ["-y", "mcp-remote", "https://www.preferly.ai/mcp?client=zed"]`.

### Hermes Agent

```bash
hermes plugins install preferly-ai/preferly-hermes --no-enable
hermes plugins enable preferly
```

The plugin ([preferly-ai/preferly-hermes](https://github.com/preferly-ai/preferly-hermes)) adds the server plus a skill that tells Hermes when to use each tool.

### Other clients

Point the client at `https://www.preferly.ai/mcp` (streamable HTTP, no auth). If it only runs local (stdio) servers, use [mcp-remote](https://www.npmjs.com/package/mcp-remote):

```json
{
  "mcpServers": {
    "preferly": { "command": "npx", "args": ["-y", "mcp-remote", "https://www.preferly.ai/mcp"] }
  }
}
```

A generic config is in [mcp.json](mcp.json).

## Try asking

- "Can AI crawlers read example.com?"
- "Does my robots.txt block GPTBot or ClaudeBot?"
- "Write robots.txt lines that let AI search crawlers in, keep training crawlers out, and keep /admin private."
- "Does example.com have a valid llms.txt?"
- "Is the business schema on example.com complete?"
- "Can AI read the phone number, hours and prices on example.com without running scripts?"
- "What do AI assistants say about the business at example.com?"

## Limits, privacy and safety

- Free, no sign-up and no key. Each caller gets 10 calls an hour and 30 website checks a day. Each website gets at most 20 fresh checks a day across all callers. A check for the same website in the last 10 minutes may be reused.
- The website checks fetch only public pages: robots.txt, the homepage, /llms.txt, and at most 2 contact, booking or pricing pages that robots.txt allows. They identify themselves as [PreferlyBot](https://www.preferly.ai/bot). They never log in, submit forms or change anything.
- `generate_ai_robots_txt` fetches nothing.
- Only `quick_ai_visibility_check` calls AI models, and it uses only what the website says publicly.
- Preferly records each check and the client name you pass in `?client=` to apply these limits and count usage. See the [privacy policy](https://www.preferly.ai/privacy).

## What these checks don't do

They check whether AI can reach and read a website, not what AI assistants actually say about a business. For that, Preferly's [full report](https://www.preferly.ai/pricing) asks 10 leading AI models about your business, quotes every place they contradict your website, and gives you the fixes ready to paste, for $99 once. [See an example report](https://www.preferly.ai/example).

## Links

- Preferly: https://www.preferly.ai
- Free tools: https://www.preferly.ai/tools
- Server card: https://www.preferly.ai/.well-known/mcp/server-card.json
- Official MCP Registry entry: `ai.preferly/preferly` (this repo's [server.json](server.json))
- Hermes plugin: https://github.com/preferly-ai/preferly-hermes
- Contact: hello@preferly.ai

## License

The documentation and configs in this repository are MIT licensed (see [LICENSE](LICENSE)). The hosted server is operated by Preferly.
