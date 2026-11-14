# Installing the Preferly MCP server (for AI agents such as Cline)

Preferly is a **hosted, remote** MCP server. There is nothing to clone, build or install, and it needs no API key, no environment variables and no sign-in.

- URL: `https://www.preferly.ai/mcp`
- Transport: Streamable HTTP
- Authentication: none

## Steps

1. Add a remote MCP server named `preferly` with the URL `https://www.preferly.ai/mcp?client=cline`.
   For Cline, add this entry to `cline_mcp_settings.json` and merge it with any servers already there. Don't remove existing entries.

   ```json
   {
     "mcpServers": {
       "preferly": {
         "type": "streamableHttp",
         "url": "https://www.preferly.ai/mcp?client=cline",
         "disabled": false,
         "autoApprove": []
       }
     }
   }
   ```

2. If the client can't connect to remote servers, use the stdio bridge instead (needs Node.js):

   ```json
   {
     "mcpServers": {
       "preferly": {
         "command": "npx",
         "args": ["-y", "mcp-remote", "https://www.preferly.ai/mcp?client=cline"]
       }
     }
   }
   ```

3. Verify the server: list its tools. You should see `check_ai_crawler_access`, `generate_ai_robots_txt`, `check_llms_txt`, `check_business_schema`, `check_business_info` and `quick_ai_visibility_check`. To test it, call `generate_ai_robots_txt` with `{}`. It fetches nothing and returns robots.txt lines.

4. Tell the user it's ready and suggest a first prompt, such as "Can AI crawlers read example.com?" (use their own website).

## Notes

- All tools are read-only and take one public website per call (`{"website": "example.com"}`). The exception is `generate_ai_robots_txt`, which takes optional `allow_search`, `allow_training` and `disallow_paths`.
- The crawler check covers 10+ AI crawlers, including GPTBot, OAI-SearchBot, ChatGPT-User, ClaudeBot, PerplexityBot and Google-Extended.
- Limits: 10 calls an hour and 30 website checks a day per caller.
- The live tool list is in the server card: https://www.preferly.ai/.well-known/mcp/server-card.json
