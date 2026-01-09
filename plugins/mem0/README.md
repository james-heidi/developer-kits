# mem0 Plugin for Claude Code

Persistent memory for Claude Code using [mem0.ai](https://mem0.ai) - remembers context across conversations.

## Features

- **Automatic Memory Retrieval**: Relevant memories injected before each prompt
- **Conversation Storage**: Conversations saved to mem0 when sessions end
- **Semantic Search**: Vector-based search for intelligent memory retrieval

## Setup

### 1. Install dependency

```bash
pip install mem0ai
```

### 2. Get API key

Get your API key from [app.mem0.ai](https://app.mem0.ai)

### 3. Configure environment

Add to your shell profile (`~/.zshrc` or `~/.bashrc`):

```bash
export MEM0_API_KEY=your-api-key-here
```

Then reload: `source ~/.zshrc`

## Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `MEM0_API_KEY` | Your mem0 API key **(required)** | - |
| `MEM0_USER_ID` | User identifier for memory scoping | `claude-code-user` |
| `MEM0_TOP_K` | Number of memories to retrieve | `5` |
| `MEM0_THRESHOLD` | Minimum similarity score (0-1) | `0.3` |
| `MEM0_SAVE_MESSAGES` | Messages to save per session | `10` |
| `MEM0_AUTO_SAVE` | Auto-save each prompt to memory | `true` |

## How It Works

### Memory Retrieval (UserPromptSubmit Hook)

When you submit a prompt:
1. Searches mem0 for semantically related memories
2. Retrieves top K memories above similarity threshold
3. Injects them into Claude's context

### Memory Storage (Stop Hook)

When a session ends:
1. Extracts recent messages from conversation
2. Sends to mem0 for processing
3. mem0 extracts key facts and stores as memories

## Commands

| Command | Description |
|---------|-------------|
| `/mem0:save` | Manually save memories from current conversation |
| `/mem0:configure` | Configuration wizard for mem0 setup |
| `/mem0:status` | Check configuration and test connection |

## Troubleshooting

**Memories not being retrieved?**
```bash
# Verify API key is set
echo $MEM0_API_KEY

# Check mem0ai is installed
pip show mem0ai
```

**Test connection:**
```bash
python3 -c "
from mem0 import MemoryClient
import os
client = MemoryClient(api_key=os.environ['MEM0_API_KEY'])
print('Connection successful!')
"
```

## License

MIT
