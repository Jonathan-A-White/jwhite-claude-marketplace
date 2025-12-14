# jwhite-claude-marketplace

Personal Claude Code plugin marketplace.

## Available Plugins

| Plugin | Description |
|--------|-------------|
| [jwhite-claude-plugin](https://github.com/Jonathan-A-White/jwhite-claude-plugin) | Socratic issue creation and HumanLayer thoughts integration |

## Installation

Add this marketplace to Claude Code:

```bash
/plugin marketplace add Jonathan-A-White/jwhite-claude-marketplace
```

Then install plugins:

```bash
/plugin install jwhite-claude-plugin@jwhite-marketplace
```

## Team Configuration

Add to your project's `.claude/settings.json`:

```json
{
  "extraKnownMarketplaces": {
    "jwhite-marketplace": {
      "source": {
        "source": "github",
        "repo": "Jonathan-A-White/jwhite-claude-marketplace"
      }
    }
  },
  "enabledPlugins": {
    "jwhite-claude-plugin@jwhite-marketplace": true
  }
}
```

## License

MIT
