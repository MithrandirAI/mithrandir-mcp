# Mithrandir MCP

<!-- mcp-name: com.trymithrandir/mithrandir -->

**One company memory in your own cloud, for every AI agent your people already use.**

Mithrandir reads the tools where work happens (chat, email, documents, tickets, code, calls and more, 26 sources) and keeps one organized, sourced record of what your company knows. Claude, ChatGPT, Copilot, Cursor and other agents ask it over MCP. Each person gets answers drawn only from what they can already access at work.

This repository holds the public connection guide and the MCP Registry entry. Mithrandir itself is commercial software that runs inside your own cloud account; its source is not published here. See [trymithrandir.com](https://trymithrandir.com).

## How it works

- **Runs in your cloud.** Mithrandir is installed in your own AWS, Azure or GCP account, or on-premises. Your data is not hosted by us.
- **One MCP endpoint.** Your deployment serves MCP over Streamable HTTP at `https://<your-host>/mcp`. By default it is reachable only from your corporate network or VPN.
- **Per-person sign-in.** The first time an agent connects, the person signs in through your company login (SSO or password) in the browser. The agent then holds a short-lived token for that person and refreshes it by itself. No shared key, and no credential in any config file.
- **Answers follow the person.** Every call is checked against that person's access, mirrored from each source tool, with your company hierarchy where a tool has none. Content they cannot access never reaches the model.

## What agents can do with it

- Search the company memory and get short, sourced answers.
- Ask why something was decided, and what replaced it.
- Read records and their history across connected tools.
- Use the company's shared skills and playbooks.

## Connect your agent

Replace `mithrandir.example.com` with your deployment's address. Your administrator can print these entries with the address already filled in by running `mithrandir print-mcp-setup` on the deployment.

**Claude Code**

```bash
claude mcp add --transport http --scope user mithrandir https://mithrandir.example.com/mcp
```

**Cursor** (`~/.cursor/mcp.json`)

```json
{
  "mcpServers": {
    "mithrandir": {
      "url": "https://mithrandir.example.com/mcp"
    }
  }
}
```

**VS Code** (user `mcp.json`, command: *MCP: Open User Configuration*)

```json
{
  "servers": {
    "mithrandir": {
      "type": "http",
      "url": "https://mithrandir.example.com/mcp"
    }
  }
}
```

**Codex CLI** (`~/.codex/config.toml`)

```toml
[mcp_servers.mithrandir]
url = "https://mithrandir.example.com/mcp"
```

Then sign in with `codex mcp login mithrandir`.

**Windsurf** (`mcp_config.json`)

```json
{
  "mcpServers": {
    "mithrandir": {
      "serverUrl": "https://mithrandir.example.com/mcp"
    }
  }
}
```

**Zed** (`settings.json`, under `context_servers`)

```json
{
  "context_servers": {
    "mithrandir": {
      "url": "https://mithrandir.example.com/mcp"
    }
  }
}
```

**claude.ai and ChatGPT in the browser.** Their connectors call from the vendor's cloud, so they need an endpoint reachable from the internet. Mithrandir keeps the endpoint on your network by default; opening it to those vendors is a separate decision for your administrators. [Talk to us](https://trymithrandir.com) about your setup.

## Get Mithrandir

Pricing, security details and a call with the founders: [trymithrandir.com](https://trymithrandir.com).

## License

The contents of this repository (this guide and `server.json`) are MIT licensed. Mithrandir itself is commercial software under its own license.
