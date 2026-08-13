<!-- mcp-name: com.printonic/printonic -->

# Printonic

Print-on-demand catalog, listings, and fulfillment for AI agents.

This is a public-ready [Agent Plugin](https://agent-plugins.org/) that connects Cursor (and other Agent Plugin clients) to Printonic’s hosted MCP server.

- **Docs:** [https://platform.printonic.com](https://platform.printonic.com)
- **MCP (Streamable HTTP):** [https://platform.printonic.com/mcp](https://platform.printonic.com/mcp)
- **Official MCP Registry:** `com.printonic/printonic` `1.0.0`
- **Privacy:** [https://printonic.com/privacy](https://printonic.com/privacy)
- **Terms:** [https://printonic.com/tos](https://printonic.com/tos)

Auth at launch is **API keys only** (`psa_live_…`). OAuth is off.

## Get a seller key

1. Sign in at [printonic.com](https://printonic.com).
2. Open [Dashboard → Agent Access](https://printonic.com/dashboard/agent-access).
3. Create a seller API key. It starts with `psa_live_`.

Do not put a real key in this repo. Replace the placeholder in `mcp.json` locally, or paste the key in your client’s MCP settings.

## Install in Cursor

### Option A — Add the hosted MCP server

1. Open Cursor Settings → MCP.
2. Add a Streamable HTTP server:
   - **URL:** `https://platform.printonic.com/mcp`
   - **Header:** `Authorization: Bearer psa_live_…` (your key)
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

### Option B — Load this plugin from disk (before Marketplace listing)

1. Clone or copy this directory.
2. In `mcp.json`, replace `YOUR_PSA_LIVE_KEY` with your `psa_live_` key.
3. In Cursor, open **Customize** and add a local plugin pointing at this folder.

## What agents can do

With a seller key, agents can search the print-on-demand catalog, inspect connected stores, and draft listings. Reads are free. Drafts and mockups are quota-gated. Orders use the same fulfillment pricing as the rest of Printonic.

Partner money-movement tools are not exposed on seller keys.

## Logo

512×512 PNG: [assets/printonic-icon-512.png](assets/printonic-icon-512.png)

Canonical hosted copy: [https://ifeefhmxlzkekkebteqt.supabase.co/storage/v1/object/public/brand-assets/printonic-icon-512.png](https://ifeefhmxlzkekkebteqt.supabase.co/storage/v1/object/public/brand-assets/printonic-icon-512.png)

## Publish notes (maintainers)

Cursor’s public Marketplace requires a **public** GitHub repository. This plugin is scaffolded locally only until Printonic approves making it public.

- Official marketplace: [https://cursor.com/marketplace/publish](https://cursor.com/marketplace/publish)
- Community listing: [https://cursor.directory/plugins/new](https://cursor.directory/plugins/new)

Do not publish a second MCP Registry namespace (for example `io.github.lumient/printonic`). The canonical name is `com.printonic/printonic`.

## License

MIT
