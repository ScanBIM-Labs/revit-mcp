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
