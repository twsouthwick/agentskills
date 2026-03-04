# GitHub Copilot CLI Plugin Configuration (plugin.json)

Configure a plugin using the `plugin.json` manifest file.

## File Locations

The manifest can be located at:
- `plugin.json` (root)
- `.github/plugin/plugin.json`
- `.claude-plugin/plugin.json`

## Required Field

| Field | Type | Description |
|-------|------|-------------|
| `name` | string | Kebab-case plugin name (letters, numbers, hyphens only). Max 64 chars. |

## Optional Metadata Fields

| Field | Type | Description |
|-------|------|-------------|
| `description` | string | Brief description. Max 1024 chars. |
| `version` | string | Semantic version (e.g., `1.0.0`). |
| `author` | object | `{ name (required), email (optional), url (optional) }` |
| `homepage` | string | Plugin homepage URL. |
| `repository` | string | Source repository URL. |
| `license` | string | License identifier (e.g., `MIT`). |
| `keywords` | string[] | Search keywords. |
| `category` | string | Plugin category. |
| `tags` | string[] | Additional tags. |

## Component Path Fields

Configure where to find plugin components. All are optional with defaults.

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| `agents` | string \| string[] | `agents/` | Path(s) to agent directories (`.agent.md` files). |
| `skills` | string \| string[] | `skills/` | Path(s) to skill directories (`SKILL.md` files). |
| `commands` | string \| string[] | — | Path(s) to command directories. |
| `hooks` | string \| object | — | Path to hooks config file, or inline hooks object. |
| `mcpServers` | string \| object | — | Path to MCP config file (e.g., `.mcp.json`), or inline server definitions. |
| `lspServers` | string \| object | — | Path to LSP config file, or inline server definitions. |

## Example plugin.json

```json
{
  "name": "my-dev-tools",
  "description": "React development utilities",
  "version": "1.2.0",
  "author": {
    "name": "Jane Doe",
    "email": "jane@example.com"
  },
  "license": "MIT",
  "keywords": ["react", "frontend"],
  "agents": "agents/",
  "skills": ["skills/", "extra-skills/"],
  "hooks": "hooks.json",
  "mcpServers": ".mcp.json"
}
```

## Default File Locations

| Component | Default Location |
|-----------|------------------|
| Agents | `agents/` |
| Skills | `skills/` |
| Hooks config | `hooks.json` or `hooks/hooks.json` |
| MCP config | `.mcp.json` or `.github/mcp.json` |
| LSP config | `lsp.json` or `.github/lsp.json` |

## Plugin Structure Example

```
my-plugin/
├── plugin.json          # Plugin manifest (required)
├── agents/              # Custom agents
│   └── reviewer.agent.md
├── skills/              # Custom skills
│   └── my-skill/
│       └── SKILL.md
├── hooks.json           # Hooks configuration
└── .mcp.json            # MCP server definitions
```
