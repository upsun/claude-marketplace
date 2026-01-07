# Upsun Claude Code Marketplace

Official marketplace for Upsun integration tools with Claude Code.

## What's Included

This marketplace provides two complementary tools for working with Upsun:

### 1. Upsun CLI Skill
**Repository:** [upsun/claude-skill](https://github.com/upsun/claude-skill)

A comprehensive Claude Code skill for managing Upsun via CLI:
- 130+ CLI commands across 30 namespaces
- Deployment workflows with safe production patterns
- Environment management (branching, merging, sync)
- Backup and restore operations with verification
- Resource scaling and autoscaling configuration
- Database operations (PostgreSQL, MongoDB, Redis, Valkey)
- 7 helper scripts for automation

**Best for:** CLI-based workflows, scripting, local development

### 2. Upsun MCP Server
**Repository:** [upsun/upsun-mcp-server](https://github.com/upsun/upsun-mcp-server)

Model Context Protocol server for direct Upsun API access:
- Direct API integration without CLI dependency
- Real-time platform operations
- Project, environment, and resource management
- Advanced features via Upsun API

**Best for:** API-driven workflows, programmatic access, CI/CD integration

## Installation

### Quick Start (Install Both)

```bash
# Add the Upsun marketplace
/plugin marketplace add upsun/claude-marketplace

# Install both tools
/plugin install upsun-skill
/plugin install upsun-mcp
```

### Individual Installation

**CLI Skill only:**
```bash
/plugin marketplace add upsun/claude-marketplace
/plugin install upsun-skill
```

**MCP Server only:**
```bash
/plugin marketplace add upsun/claude-marketplace
/plugin install upsun-mcp
```

## Prerequisites

### For CLI Skill
- Upsun CLI v5.6.0+ installed and authenticated
- Bash shell for helper scripts

```bash
# Install Upsun CLI
curl -fsSL https://raw.githubusercontent.com/platformsh/cli/main/installer.sh | VENDOR=upsun bash

# Authenticate
upsun auth:browser-login
```

### For MCP Server
- Node.js 18+ (for running the MCP server)
- Upsun API token (configured via environment variables or settings)

## Usage

### Using the CLI Skill

After installation, ask Claude:
- "Deploy my changes to Upsun production"
- "Create a new feature environment"
- "Check the health of my production environment"
- "Backup my database before deploying"

Claude will automatically use the skill and helper scripts.

### Using the MCP Server

The MCP server provides tools that Claude can call directly:
- `upsun__list-projects` - List all your projects
- `upsun__get-environment` - Get environment details
- `upsun__create-backup` - Create environment backups
- And many more...

## When to Use Which Tool?

| Use Case | CLI Skill | MCP Server |
|----------|-----------|------------|
| Local development workflows | ✅ Best | ⚠️ Works |
| Production deployments | ✅ Best | ✅ Good |
| Quick environment checks | ✅ Fast | ✅ Fast |
| Scripting and automation | ✅ Best | ⚠️ Requires setup |
| CI/CD integration | ⚠️ Requires CLI | ✅ Best |
| API-driven operations | ❌ Limited | ✅ Best |
| Multi-project management | ✅ Good | ✅ Best |

**Recommendation:** Install both! They complement each other.

## Permissions

### CLI Skill Permissions

Add to `.claude/settings.local.json`:

```json
{
  "permissions": {
    "allow": [
      "Bash(upsun auth:*)",
      "Bash(upsun environment:*)",
      "Bash(upsun activity:*)",
      "Bash(upsun backup:*)",
      "Bash(upsun project:*)",
      "Bash(upsun logs:*)",
      "Bash(upsun resources:*)",
      "Bash(upsun metrics:*)",
      "Bash(upsun user:*)",
      "Bash(upsun organization:*)"
    ]
  }
}
```

### MCP Server Permissions

The MCP server tools are automatically trusted once the plugin is installed. Configure your Upsun API credentials in the MCP server settings.

## Team Distribution

For teams, add to your project's `.claude/settings.json`:

```json
{
  "extraKnownMarketplaces": {
    "upsun": {
      "source": {
        "source": "github",
        "repo": "upsun/claude-marketplace"
      }
    }
  },
  "enabledPlugins": {
    "upsun-skill@upsun": true,
    "upsun-mcp@upsun": true
  }
}
```

Team members will be prompted to install when opening the project.

## Updates

Keep your tools up to date:

```bash
# Update the marketplace catalog
/plugin marketplace update upsun

# Update individual plugins
/plugin update upsun-skill
/plugin update upsun-mcp

# Or update all
/plugin update --all
```

## Documentation

- **CLI Skill Docs:** [claude-skill repository](https://github.com/upsun/claude-skill)
- **MCP Server Docs:** [upsun-mcp-server repository](https://github.com/upsun/upsun-mcp-server)
- **Upsun Platform:** [docs.upsun.com](https://docs.upsun.com)
- **Claude Code:** [code.claude.com/docs](https://code.claude.com/docs)


## Contributing

Contributions are welcome! Please see individual repositories for contribution guidelines:
- [CLI Skill - CLAUDE.md](https://github.com/upsun/claude-skill/blob/main/CLAUDE.md)
- [MCP Server - CLAUDE.md](https://github.com/upsun/upsun-mcp-server/blob/main/CLAUDE.md)

## License

- Marketplace: Apache 2.0
- CLI Skill: Apache 2.0
- MCP Server: Apache 2.0
