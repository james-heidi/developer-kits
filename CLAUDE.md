# Claude Code Marketplace

This repository contains Claude Code plugins for the marketplace.

## Adding a New Plugin

When adding a new plugin, follow these guidelines:

### Directory Structure

```
plugins/
└── plugin-name/
    ├── .claude-plugin/
    │   └── plugin.json      # Plugin manifest (required)
    ├── README.md            # Plugin documentation (required)
    ├── CLAUDE.md            # Plugin-specific Claude instructions (optional)
    ├── .mcp.json            # MCP server config (if using MCP)
    ├── agents/              # Agent definitions
    ├── commands/            # Slash commands
    ├── hooks/               # Hook configurations
    ├── skills/              # Skill definitions
    └── scripts/             # Utility scripts
```

### plugin.json Format

```json
{
  "name": "plugin-name",
  "version": "1.0.0",
  "description": "Brief description of what the plugin does",
  "author": {
    "name": "Author Name",
    "url": "https://github.com/author"
  },
  "repository": "https://github.com/org/repo/tree/main/plugin-name",
  "license": "MIT",
  "keywords": ["keyword1", "keyword2"]
}
```

---

## README.md Template for Plugins

Every plugin MUST have a README.md with the following sections:

### Required Sections

```markdown
# plugin-name

One-line description of what the plugin does.

## Features

- **Feature 1**: Brief description
- **Feature 2**: Brief description

## Installation

\`\`\`bash
/plugin install plugin-name
\`\`\`

## Usage

[How to use the plugin - automatic triggers and manual commands]
```

### Recommended Sections

Add these sections based on plugin complexity:

| Section | When to Include |
|---------|-----------------|
| **Prerequisites** | If external dependencies required (API keys, tools) |
| **Configuration** | If environment variables or settings needed |
| **Components** | If plugin has multiple agents/commands/skills |
| **How It Works** | For complex plugins with non-obvious behavior |
| **Usage Examples** | Always helpful, especially with sample output |
| **Architecture** | For complex plugins with multiple files |
| **Troubleshooting** | If common issues are known |
| **License** | Always include (MIT recommended) |
| **Credits** | If based on or inspired by other projects |

### README.md Best Practices

1. **Start with a clear one-liner** describing the plugin's purpose
2. **Use tables** for structured information (config vars, components, options)
3. **Show installation first** - users want to know how to get started
4. **Include concrete examples** with actual commands and expected output
5. **Document all components** - agents, commands, skills, hooks
6. **Keep it scannable** - use headers, bullet points, code blocks
7. **Add troubleshooting** for known issues

### Example: Components Table

```markdown
## Components

| Component | Type | Description |
|-----------|------|-------------|
| `do-something` | command | Manually trigger the action |
| `auto-doer` | agent | Proactively suggests actions |
| `thing-knowledge` | skill | Best practices for things |
```

### Example: Configuration Table

```markdown
## Configuration

| Variable | Required | Description |
|----------|----------|-------------|
| `API_KEY` | Yes | Your API key from [service](https://...) |
| `USER_ID` | No | Custom identifier (default: `$USER`) |
```

### Example: Hook Documentation

```markdown
## Hooks

| Hook | Trigger | Action |
|------|---------|--------|
| **SessionStart** | Session begins | Load relevant context |
| **Stop** | Task completes | Prompt to save learnings |
```

---

## Version Bumping

When modifying a plugin:
1. Update version in `.claude-plugin/plugin.json`
2. Use semantic versioning:
   - **PATCH** (x.x.X): Bug fixes, typos, minor improvements
   - **MINOR** (x.X.0): New features, non-breaking changes
   - **MAJOR** (X.0.0): Breaking changes

---

## Reference Examples

- **Simple plugin**: `plugins/claude-md-sync/` - Skills, agent, command
- **Complex plugin with hooks**: `plugins/claude-mem0/` - MCP server, hooks, scripts
