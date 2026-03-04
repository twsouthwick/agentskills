# GitHub Copilot CLI Plugin Management

Manage plugins for GitHub Copilot CLI using terminal commands.

## Commands

### Install a Plugin

```bash
copilot plugin install SPECIFICATION
```

**Plugin Specification Formats:**

| Type | Format | Example |
|------|--------|---------|
| Marketplace | `plugin@marketplace` | `my-plugin@company-marketplace` |
| GitHub Repository | `OWNER/REPO` | `octocat/my-plugin` |
| GitHub Subdirectory | `OWNER/REPO:PATH/TO/PLUGIN` | `octocat/monorepo:plugins/my-plugin` |
| Git URL | `https://github.com/o/r.git` | `https://github.com/octocat/plugin.git` |
| Local Path | `./my-plugin` or `/abs/path` | `./local-plugins/my-tool` |

### Uninstall a Plugin

```bash
copilot plugin uninstall NAME
```

### List Installed Plugins

```bash
copilot plugin list
```

### Update Plugins

```bash
# Update a specific plugin
copilot plugin update NAME

# Update all plugins
copilot plugin update --all
```

### Enable/Disable Plugins

```bash
# Temporarily disable a plugin without uninstalling
copilot plugin disable NAME

# Re-enable a disabled plugin
copilot plugin enable NAME
```

## Getting Help

```bash
copilot plugin [SUBCOMMAND] --help
```

## File Locations

- **Installed plugins (via marketplace):** `~/.copilot/state/installed-plugins/MARKETPLACE/PLUGIN-NAME`
- **Installed plugins (direct):** `~/.copilot/state/installed-plugins/PLUGIN-NAME`

## Loading Order and Precedence

Agents and skills use **first-found-wins** precedence:
1. `~/.copilot/agents/` (user, .github convention)
2. `<project>/.github/agents/` (project)
3. `<parents>/.github/agents/` (inherited, monorepo)
4. `~/.claude/agents/` (user, .claude convention)
5. `<project>/.claude/agents/` (project)
6. `<parents>/.claude/agents/` (inherited, monorepo)
7. Plugin `agents/` directories (by install order)
8. Remote org/enterprise agents (via API)

Built-in tools and agents are always present and cannot be overridden.
