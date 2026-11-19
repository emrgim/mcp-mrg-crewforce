# mcp-mrg-crewforce

Cursor connector for **Crewforce** (https://crewforce.xyz): productions, work days, contacts,
venues, rate cards and your public profile, from any MCP client.

The server is remote and hosted by Crewforce at `https://crewforce.xyz/mcp` (Streamable HTTP).
This repo holds only the connector manifest and logo — no server code, no secrets.

## Cursor plugin

```
.cursor-plugin/plugin.json   # manifest, logo = absolute URL (renders in Marketplace / Customize)
mcp.json                     # remote server, OAuth sign-in on first use
assets/logo.svg              # square 1:1 logo (also logo.png 512×512)
```

Local test: copy this folder to `~/.cursor/plugins/local/mcp-mrg-crewforce`, then
**Developer: Reload Window** and open **Customize → MCPs / Plugins**. Local plugins show the
default cube icon; the logo appears once listed in the Marketplace.

## Sign-in

- **OAuth (default):** the client discovers `https://crewforce.xyz/.well-known/oauth-authorization-server`
  and opens the Crewforce login (Google or email).
- **Personal key (clients without OAuth):** copy the key from Crewforce → Settings → MCP and send it as
  `Authorization: Bearer <key>`:

```json
{
  "mcpServers": {
    "crewforce": {
      "url": "https://crewforce.xyz/mcp",
      "headers": { "Authorization": "Bearer ${CREWFORCE_API_KEY}" }
    }
  }
}
```

## Other clients

| Client | Setup |
|---|---|
| Claude (connector) | Add custom connector → `https://crewforce.xyz/mcp` |
| Claude Code | `claude mcp add --transport http crewforce https://crewforce.xyz/mcp` |
| Grok / ChatGPT / Gemini | Remote MCP URL `https://crewforce.xyz/mcp` (OAuth) |
