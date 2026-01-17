# Claude Code Marketplace

A collection of plugins for Claude Code.

## Available Plugins

| Plugin                                     | Description                                                                                                                                      | Category     |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------ | ------------ |
| [claude-md-sync](./plugins/claude-md-sync) | Automatically keeps CLAUDE.md synchronized with project state. Detects project type, analyzes current state, and proposes documentation updates. | Productivity |
| [claude-mem0](./plugins/claude-mem0)       | Persistent memory for Claude Code using mem0 cloud API. Automatically captures and retrieves global user-level and project-level memories.       | Productivity |
| [gui-agent-dev](./plugins/gui-agent-dev)   | Development toolkit for GUI automation agents with `/dev` command (6-step workflow), 8 agents (5 domain + 3 workflow), and code review skill.    | Development  |

## Installation

### 1. Add this marketplace

```
/plugin marketplace add https://github.com/james-heidi/developer-kits.git
```

### 2. Install a plugin

```
/plugin install claude-md-sync@developer-kits
/plugin install claude-mem0@developer-kits
/plugin install gui-agent-dev@developer-kits
```

## License

MIT
