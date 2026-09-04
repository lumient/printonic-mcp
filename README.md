<!-- mcp-name: com.printonic/printonic -->

# Printonic

Print-on-demand catalog, listings, orders, and fulfillment for AI agents.

This is a public [Agent Plugin](https://agent-plugins.org/) that connects Cursor (and other Agent Plugin clients) to Printonic's hosted MCP server. The same server also powers the connector in claude.ai, Claude Desktop, and the ChatGPT app.

- **Docs:** [https://platform.printonic.com](https://platform.printonic.com)
- **MCP (Streamable HTTP):** [https://platform.printonic.com/mcp](https://platform.printonic.com/mcp)
- **Official MCP Registry:** `com.printonic/printonic` `1.1.0`
- **Privacy:** [https://printonic.com/privacy](https://printonic.com/privacy)
- **Terms:** [https://printonic.com/tos](https://printonic.com/tos)

## Two ways to connect

| Your client | How it authenticates |
|---|---|
| Cursor, Claude Code, the OpenAI Responses API / Agents SDK, any client that takes a header | A seller API key (`psa_live_...`) sent as `Authorization: Bearer` |
| claude.ai, Claude Desktop, the ChatGPT app | Sign in with your Printonic account. No key is pasted. |

Both paths land on the same account, with the same permissions, quotas, and approval rules. Every action either way is listed in your dashboard under Agent Access, then Activity.

## Claude and ChatGPT apps (sign in, no key)

1. In the app, open Settings, then Connectors, and choose **Add custom connector**.
2. Name it Printonic and paste the address `https://platform.printonic.com/mcp`.
3. Click Connect. You are taken to Printonic to sign in with the email and password you already use.
4. Approve the permissions screen. You are connected.

Creating orders still requires a key rather than a sign-in, because the daily spend cap lives on the key.

## Cursor and other key-based clients

### Get a seller key

1. Sign in at [printonic.com](https://printonic.com).
2. Open [Dashboard, then Agent Access](https://printonic.com/dashboard/agent-access).
3. Create a seller API key and choose what it may do. It starts with `psa_live_` and is shown once.

Do not put a real key in this repo. Replace the placeholder in `mcp.json` locally, or paste the key in your client's MCP settings.

### Option A: add the hosted MCP server in Cursor

1. Open Cursor Settings, then MCP.
2. Add a Streamable HTTP server:
   - **URL:** `https://platform.printonic.com/mcp`
   - **Header:** `Authorization: Bearer psa_live_...` (your key)
3. Or use the [Add to Cursor](https://platform.printonic.com/docs/clients/cursor) deeplink from the docs, then replace `YOUR_PSA_LIVE_KEY`.

Example `mcp.json`:

```json
{
  "mcpServers": {
    "printonic": {
      "url": "https://platform.printonic.com/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_PSA_LIVE_KEY"
      }
    }
  }
}
```

### Option B: load this plugin from disk

1. Clone or copy this directory.
2. In `mcp.json`, replace `YOUR_PSA_LIVE_KEY` with your `psa_live_` key.
3. In Cursor, open **Customize** and add a local plugin pointing at this folder.

### Claude Code

```
claude mcp add --transport http printonic https://platform.printonic.com/mcp \
  --header "Authorization: Bearer psa_live_..."
```

## What agents can do

With access to a seller account, an agent can search the print-on-demand catalog and read product file requirements, list the seller's connected stores and products, create listing drafts, attach art, generate and check 3D mockups, set pricing and listing settings, check publish readiness and publish, create custom listings and gift sets, and, with a key, create orders and read order status and tracking. Two small tools, `printonic_list_pending_actions` and `printonic_get_action_status`, let an agent resume work that is waiting on the seller.

Reads are free. Drafts and mockups are quota-gated by plan. Orders use the same fulfillment pricing as the rest of Printonic.

**The seller stays in control.** Publishing, creating orders, and archiving are held in the seller's Review tab until they approve, unless the seller has switched a class to auto-approve in Settings. Everything an agent does appears under Activity, kept for 180 days.

Partner money-movement tools are not exposed on seller accounts.

## Logo

512x512 PNG: [assets/printonic-icon-512.png](assets/printonic-icon-512.png)

Canonical hosted copy: [https://ifeefhmxlzkekkebteqt.supabase.co/storage/v1/object/public/brand-assets/printonic-icon-512.png](https://ifeefhmxlzkekkebteqt.supabase.co/storage/v1/object/public/brand-assets/printonic-icon-512.png)

## Publish notes (maintainers)

- Official marketplace: [https://cursor.com/marketplace/publish](https://cursor.com/marketplace/publish)
- Community listing: [https://cursor.directory/plugins/printonic](https://cursor.directory/plugins/printonic) (reads `mcp.json` from this repo)
- MCP Registry: republish `server.json` with `mcp-publisher` whenever the version changes.

Do not publish a second MCP Registry namespace (for example `io.github.lumient/printonic`). The canonical name is `com.printonic/printonic`.

## License

MIT
