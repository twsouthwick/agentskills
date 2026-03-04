# GitHub Copilot CLI Marketplace Configuration (marketplace.json)

Configure a plugin marketplace using the `marketplace.json` file.

## File Location

Save the marketplace manifest at:
- `.github/plugin/marketplace.json`
- `.claude-plugin/marketplace.json`

## Top-Level Fields

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `name` | string | Yes | Kebab-case marketplace name. Max 64 chars. |
| `owner` | object | Yes | `{ name, email? }` — marketplace owner info. |
| `plugins` | array | Yes | List of plugin entries. |
| `metadata` | object | No | `{ description?, version?, pluginRoot? }` |

## Plugin Entry Fields

Each object in the `plugins` array can contain:

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `name` | string | Yes | Kebab-case plugin name. Max 64 chars. |
| `source` | string \| object | Yes | Where to fetch the plugin (relative path, GitHub, or URL). |
| `description` | string | No | Plugin description. Max 1024 chars. |
| `version` | string | No | Plugin version. |
| `author` | object | No | `{ name, email?, url? }` |
| `homepage` | string | No | Plugin homepage URL. |
| `repository` | string | No | Source repository URL. |
| `license` | string | No | License identifier. |
| `keywords` | string[] | No | Search keywords. |
| `category` | string | No | Plugin category. |
| `tags` | string[] | No | Additional tags. |
| `commands` | string \| string[] | No | Path(s) to command directories. |
| `agents` | string \| string[] | No | Path(s) to agent directories. |
| `skills` | string \| string[] | No | Path(s) to skill directories. |
| `hooks` | string \| object | No | Path to hooks config or inline hooks object. |
| `mcpServers` | string \| object | No | Path to MCP config or inline server definitions. |
| `lspServers` | string \| object | No | Path to LSP config or inline server definitions. |
| `strict` | boolean | No | When `true` (default), plugins must conform to full schema. When `false`, relaxed validation is used. |

## Example marketplace.json

```json
{
  "name": "my-marketplace",
  "owner": {
    "name": "Your Organization",
    "email": "plugins@example.com"
  },
  "metadata": {
    "description": "Curated plugins for our team",
    "version": "1.0.0"
  },
  "plugins": [
    {
      "name": "frontend-design",
      "description": "Create a professional-looking GUI",
      "version": "2.1.0",
      "source": "./plugins/frontend-design"
    },
    {
      "name": "security-checks",
      "description": "Check for potential security vulnerabilities",
      "version": "1.3.0",
      "source": "./plugins/security-checks"
    }
  ]
}
```

## Source Path Notes

The `source` field value is relative to the repository root:
- `"./plugins/plugin-name"` and `"plugins/plugin-name"` resolve to the same directory
- The `./` prefix is optional

## Marketplace Structure Example

```
my-marketplace/
├── .github/
│   └── plugin/
│       └── marketplace.json    # Marketplace manifest
└── plugins/
    ├── frontend-design/
    │   ├── plugin.json
    │   └── skills/
    └── security-checks/
        ├── plugin.json
        └── skills/
```

## Registering the Marketplace

After creating the manifest:

```bash
# From a local directory
copilot plugin marketplace add /PATH/TO/my-marketplace

# From a GitHub repository
copilot plugin marketplace add OWNER/REPO
```
