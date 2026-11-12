# SpotCam for AI agents

Connects your AI assistant to your SpotCam cameras through the SpotCam MCP
server (`https://mcp.myspotcam.com/mcp`). You sign in with your SpotCam
email and password in the browser; no API key is needed.

## Claude Code (recommended)

```
/plugin marketplace add SpotCam-Cloud/spotcam-plugins
/plugin install spotcam@spotcam
```

Then run `/reload-plugins`, open `/mcp`, choose `plugin:spotcam:spotcam` and
select **Authenticate**. Ask: "List my SpotCam cameras" or "Show me the front
door camera".

Without the plugin, one command does the same:

```
claude mcp add --transport http --scope user spotcam https://mcp.myspotcam.com/mcp
```

Or paste this into Claude Code and let it set everything up:

```
Connect me to the SpotCam MCP server:
1. Run: claude mcp add --transport http --scope user spotcam https://mcp.myspotcam.com/mcp
   (if it already exists, check `claude mcp get spotcam` shows the same URL)
2. Run: claude mcp login spotcam — it opens my browser to sign in to SpotCam; wait until I finish.
   Do not add any headers, tokens or API keys.
3. Ask me to type /mcp and confirm "spotcam" is connected (restart with `claude -c` if it is missing).
4. List my cameras to confirm it works.
```

## Other clients

| Client | Setup |
|---|---|
| claude.ai / Claude Desktop | Settings → Connectors → Add custom connector → `https://mcp.myspotcam.com/mcp` → "Use Claude's published identity" → Connect |
| VS Code + GitHub Copilot | [Install in VS Code](https://insiders.vscode.dev/redirect/mcp/install?name=spotcam&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fmcp.myspotcam.com%2Fmcp%22%7D), or `code --add-mcp '{"name":"spotcam","type":"http","url":"https://mcp.myspotcam.com/mcp"}'` |
| GitHub Copilot CLI | `copilot mcp add --transport http spotcam https://mcp.myspotcam.com/mcp` |
| OpenAI Codex CLI | `codex mcp add spotcam --url https://mcp.myspotcam.com/mcp` |
| Gemini CLI | `gemini extensions install https://github.com/SpotCam-Cloud/spotcam-plugins`, then `/mcp auth spotcam` |
| opencode | `opencode mcp add spotcam --url https://mcp.myspotcam.com/mcp` |

`mcp.myspotcam.com` is the production SpotCam MCP server.

## More

- [User guide](docs/user-guide.md): what you can ask, which cameras are visible, revoking access, troubleshooting.
- [Privacy policy](https://mcp.myspotcam.com/privacy) (draft, pending legal review; source: [PRIVACY.md](PRIVACY.md)).
- License: MIT ([LICENSE](LICENSE)); the SpotCam name and logo are not covered.
