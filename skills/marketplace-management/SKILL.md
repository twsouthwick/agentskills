# GitHub Copilot CLI Marketplace Management

Manage plugin marketplaces for GitHub Copilot CLI.

## Commands

### Register a Marketplace

```bash
copilot plugin marketplace add SPECIFICATION
```

The specification can be:
- A GitHub repository path (e.g., `OWNER/REPO`)
- A local file path (e.g., `/PATH/TO/my-marketplace`)

### List Registered Marketplaces

```bash
copilot plugin marketplace list
```

### Browse Marketplace Plugins

```bash
copilot plugin marketplace browse NAME
```

### Unregister a Marketplace

```bash
copilot plugin marketplace remove NAME
```

## File Locations

- **Marketplace cache:** `~/.copilot/state/marketplace-cache/`
- **Marketplace manifest:** `.github/plugin/marketplace.json` or `.claude-plugin/marketplace.json`

## Creating a Marketplace

To create a plugin marketplace:

1. Create a `marketplace.json` file
2. Save it to `.github/plugin/` directory in your repository
3. Or store locally at `/PATH/TO/my-marketplace/.github/plugin/marketplace.json`

Then register it:

```bash
copilot plugin marketplace add /PATH/TO/my-marketplace
```

## Installing Plugins from Marketplaces

Once a marketplace is registered, install plugins using the `@` syntax:

```bash
copilot plugin install plugin-name@marketplace-name
```

## Example Workflow

```bash
# Add a team marketplace
copilot plugin marketplace add my-org/team-plugins

# Browse available plugins
copilot plugin marketplace browse team-plugins

# Install a plugin from the marketplace
copilot plugin install security-checks@team-plugins

# List all registered marketplaces
copilot plugin marketplace list
```
