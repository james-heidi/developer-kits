# mem0 Plugin for Claude Code

Persistent memory for Claude Code using [mem0.ai](https://mem0.ai) - remembers context across conversations.

## Features

- **Automatic Memory Retrieval**: Relevant memories are searched and injected before each prompt
- **Conversation Storage**: Conversations are automatically saved to mem0 when sessions end
- **Semantic Search**: Vector-based search for intelligent memory retrieval
- **User Scoping**: Memories are scoped by user ID for personalized experiences

## Requirements

- Python 3.8+
- Claude Code with plugin support
- mem0 API key ([get one here](https://app.mem0.ai))

## Quick Start

```bash
# 1. Add plugin to ~/.claude/settings.json

# 2. Install dependency
pip install mem0ai

# 3. Set environment variable (add to ~/.zshrc or ~/.bashrc)
export MEM0_API_KEY=your-api-key-here

# 4. Restart your terminal and Claude Code
```

## Installation

### 1. Install the Plugin

Add to your `.claude/settings.json`:

```json
{
  "plugins": [
    "marketplace:mem0"
  ]
}
```

### 2. Install Dependencies

```bash
pip install mem0ai
```

### 3. Configure Environment

Add to your shell profile (`~/.zshrc` or `~/.bashrc`):

```bash
# Required: Get your API key from https://app.mem0.ai
export MEM0_API_KEY=your-api-key-here

# Optional: Custom user identifier (default: claude-code-user)
export MEM0_USER_ID=your-user-id

# Optional: Number of memories to retrieve (default: 5)
export MEM0_TOP_K=5

# Optional: Minimum similarity threshold (default: 0.3)
export MEM0_THRESHOLD=0.3

# Optional: Number of messages to save per session (default: 10)
export MEM0_SAVE_MESSAGES=10
```

Then reload your shell: `source ~/.zshrc`

### 4. Restart Claude Code

The plugin will be active after restart.

## Plugin Structure

```
plugins/mem0/
├── .claude-plugin/
│   └── plugin.json           # Plugin metadata
├── commands/
│   └── save.md               # /mem0:save command
├── hooks/
│   ├── hooks.json            # Hook configuration
│   ├── userpromptsubmit.py   # Memory retrieval before prompts
│   ├── stop.py               # Memory storage on session end
│   ├── save_manual.py        # Manual memory save script
│   └── tests/
│       └── test_hooks.py     # Pytest tests
├── skills/
│   ├── configure/
│   │   └── SKILL.md          # /mem0:configure skill
│   └── status/
│       └── SKILL.md          # /mem0:status skill
└── README.md
```

## How It Works

### Memory Retrieval (UserPromptSubmit Hook)

When you submit a prompt, the plugin:
1. Searches mem0 for memories semantically related to your prompt
2. Retrieves the top K most relevant memories above the similarity threshold
3. Injects them into Claude's context as a system reminder

Example context injection:
```
## Relevant memories from previous conversations:
- User prefers TypeScript over JavaScript
- Working on an e-commerce platform using Next.js
- Database is PostgreSQL with Prisma ORM
```

### Memory Storage (Stop Hook)

When a session ends, the plugin:
1. Extracts the most recent messages from the conversation transcript
2. Sends them to mem0 for asynchronous processing
3. mem0 automatically extracts key facts and stores them as memories

> **Note**: Memory processing happens asynchronously. New memories may take a few seconds to become searchable.

## Configuration Options

| Variable | Description | Default |
|----------|-------------|---------|
| `MEM0_API_KEY` | Your mem0 API key (required) | - |
| `MEM0_USER_ID` | User identifier for memory scoping | `claude-code-user` |
| `MEM0_TOP_K` | Number of memories to retrieve | `5` |
| `MEM0_THRESHOLD` | Minimum similarity score (0-1) | `0.3` |
| `MEM0_SAVE_MESSAGES` | Messages to save per session | `10` |
| `MEM0_AUTO_SAVE` | Auto-save each prompt to memory | `true` |

## Commands & Skills

### `/mem0:save`

Manually save memories from the current conversation. Useful when you want to persist important context without ending the session.

### `/mem0:configure`

Interactive configuration wizard for setting up mem0 credentials.

### `/mem0:status`

Check the current configuration status and test the connection.

## Troubleshooting

### Memories not being retrieved

1. Verify `MEM0_API_KEY` is set: `echo $MEM0_API_KEY`
2. Check that mem0ai is installed: `pip install mem0ai`
3. Ensure you have existing memories in mem0
4. Try lowering `MEM0_THRESHOLD` for broader matches (e.g., `0.1`)

### Memories not being saved

1. Check the console for error messages
2. Verify your API key has write permissions
3. Ensure conversations have meaningful content
4. Remember that memory processing is asynchronous - wait a few seconds

### Testing the connection

```bash
# Set your API key
export MEM0_API_KEY=your-api-key-here

# Test connection and add a memory
python3 -c "
from mem0 import MemoryClient
client = MemoryClient(api_key='$MEM0_API_KEY')
print('Connection successful!')

# Add a test memory
result = client.add(
    messages=[{'role': 'user', 'content': 'Test message'}],
    user_id='test-user'
)
print(f'Add result: {result}')
"
```

## Privacy & Security

- API keys are loaded from system environment variables only
- Never commit API keys to version control
- Memories are scoped by `MEM0_USER_ID` - use unique IDs for different contexts
- Review mem0's [privacy policy](https://mem0.ai/privacy) for data handling

## Testing

Run the test suite:

```bash
pip install pytest
python -m pytest plugins/mem0/hooks/tests/ -v
```

## License

MIT
