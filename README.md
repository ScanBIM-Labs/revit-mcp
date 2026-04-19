# Revit MCP

**Revit integration via Autodesk Platform Services** — Extract elements, parameters, run schedules, detect clashes, export IFC.

[![Live](https://img.shields.io/badge/status-live-brightgreen)](https://revit-mcp.itmartin24.workers.dev/)
[![MCP](https://img.shields.io/badge/protocol-MCP%202024--11--05-blue)](https://modelcontextprotocol.io)

## Tools (8)

| Tool | Description |
|------|-------------|
| `revit_upload` | Upload Revit file to APS and translate |
| `revit_get_elements` | Get elements by category |
| `revit_get_parameters` | Get element parameters |
| `revit_run_schedule` | Extract schedule data |
| `revit_clash_detect` | Clash detection with VDC rules |
| `revit_export_ifc` | Export model as IFC |
| `revit_get_sheets` | List all sheets |
| `revit_get_views` | List all views |

## Quick Start

```json
{
  "mcpServers": {
    "revit": {
      "url": "https://revit-mcp.itmartin24.workers.dev/mcp"
    }
  }
}
```

## Architecture

- **Runtime**: Cloudflare Workers
- **Auth**: APS OAuth2 (client_credentials)
- **Database**: Cloudflare D1 (usage logging)
- **Cache**: Cloudflare KV (token caching)

## Part of [ScanBIM Labs AEC MCP Ecosystem](https://github.com/ScanBIM-Labs)

MIT — ScanBIM Labs LLC

## Authentication

Two accepted header formats. **Use one, do NOT mix:**

1. `x-scanbim-api-key: <your_user_key>` — value is the user_key verbatim.
2. `Authorization: Bearer sk_scanbim_<your_user_key>` — value is the entire string including the `sk_scanbim_` prefix; the D1 `user_key` column must match this full string.

Mixing formats auto-creates a fresh free-plan row for the alternate key (you'll silently get a new 50-credit account on each switch).

Get your user_key at [scanbim.app/settings/billing](https://scanbim.app/settings/billing).

### Example

```bash
curl -X POST https://mcp.scanbimlabs.io/unified/mcp \
  -H "content-type: application/json" \
  -H "x-scanbim-api-key: $SCANBIM_USER_KEY" \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"list_models","arguments":{}}}'
```

### Response codes

- `200` — tool call proceeded; credits debited.
- `401` — missing or malformed auth header (middleware returns JSON-RPC error code `-32001`).
- `402` — insufficient credits; response body includes `checkout_urls` for all 5 credit packs and `top_up_url` for the billing page.
