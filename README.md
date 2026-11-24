# Bloom MCP

Public packaging and install docs for [Bloom](https://www.usebloom.com)’s remote MCP server.

This repository does **not** host the MCP service. Production endpoint:

```text
https://api.usebloom.com/mcp
```

Use it from Cursor, Claude, ChatGPT, and other MCP clients that support remote Streamable HTTP + OAuth.

## What you get

After connecting with a Bloom account in an org that has MCP enabled, agents can work with your coaching data (goals, actions, vision, check-ins, summaries, DISC, Relatability colleagues, and related tools).

Effective access is the intersection of your OAuth scopes (`bloom:mcp:read` / `write` / `edit`) and your organisation’s MCP policy.

## Cursor

### Option A — Marketplace (when listed)

Install **Bloom** from the [Cursor Marketplace](https://cursor.com/marketplace), then **Connect** / authenticate.

### Option B — Manual `mcp.json`

Add to `~/.cursor/mcp.json` (or a project `.cursor/mcp.json`):

```json
{
  "mcpServers": {
    "Bloom": {
      "url": "https://api.usebloom.com/mcp",
      "auth": {
        "CLIENT_ID": "EqYKhTce3nKjkJN8UedoX4D1LK5724T3",
        "scopes": [
          "bloom:mcp:read",
          "bloom:mcp:write",
          "bloom:mcp:edit"
        ]
      }
    }
  }
}
```

1. Open **Cursor Settings → Tools & MCP**
2. Find **Bloom** → **Connect** / **Authenticate**
3. Complete Bloom passwordless login in the browser

`CLIENT_ID` is the public Auth0 **Bloom MCP Cursor Client** (PKCE; no client secret).

## Claude (claude.ai / Claude Desktop)

Prefer Claude Desktop or claude.ai connectors (not Claude Code with random loopback ports).

1. **Settings → Connectors** → add a custom / remote MCP server
2. **URL:** `https://api.usebloom.com/mcp`
3. **OAuth Client ID:** `j9fXRMRyY0fHzPnYMhqiRYzUMkY6dZgJ`  
   (Auth0 **Bloom MCP Claude Client**)
4. Scopes if prompted: `bloom:mcp:read` `bloom:mcp:write` `bloom:mcp:edit`
5. Connect and finish passwordless login

Directory listing (one-click discoverability) is separate and requires a Claude org **Owner** to submit at [claude.ai/directory/manage](https://claude.ai/directory/manage).

## ChatGPT

1. Add a custom MCP / connector with URL `https://api.usebloom.com/mcp`
2. Use Auth0 **Bloom MCP ChatGPT Client** (Prod) when a client ID is required
3. If OpenAI issues a per-connection callback URL, that exact URI must be allowlisted on the Auth0 client

## First-time signup

If Bloom needs more profile details (name, phone, org / limited eligibility), Auth0 redirects to a short signup interstitial, then resumes OAuth so your client finishes connecting.

## Requirements

- Bloom Production account
- Parent organisation with MCP policy enabled (otherwise tools may auth but return `mcp_unavailable_for_org`)
- Client that supports remote MCP over HTTPS and OAuth 2.0 (PKCE)

## Privacy & support

- Product: [https://www.usebloom.com](https://www.usebloom.com)
- Support: support@usebloom.com
- Link your organisation’s privacy policy in store listings (Claude directory / Cursor Marketplace)

## Development note

The MCP implementation lives in Bloom’s private `service-app-gateway` service. This repo is only the public plugin manifest, logo, and install documentation for store distribution.
