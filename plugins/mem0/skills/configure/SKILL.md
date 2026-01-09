---
name: configure
description: Configure mem0 API key and settings for this project. Use when the user wants to set up mem0, configure memory settings, or add their API key.
---

# mem0 Configuration Skill

Help the user configure their mem0 integration.

## Steps

1. **Check current configuration**
   - Run `echo $MEM0_API_KEY` to check if API key is set
   - Report current configuration status

2. **Guide API key setup**
   - Direct user to https://app.mem0.ai to get their API key
   - Explain they need to add it to their shell profile (`~/.zshrc` or `~/.bashrc`)

3. **Provide configuration instructions**
   - Show the export commands to add to shell profile
   - Explain each configuration option

4. **Test the connection**
   - Run a simple test to verify the API key works
   - Report success or any errors

## Configuration Options

Add to `~/.zshrc` or `~/.bashrc`:

```bash
# Required
export MEM0_API_KEY=your-api-key

# Optional
export MEM0_USER_ID=claude-code-user
export MEM0_TOP_K=5
export MEM0_THRESHOLD=0.3
export MEM0_SAVE_MESSAGES=10
```

Then run `source ~/.zshrc` to reload.

## Example Flow

```
User: /mem0:configure
```
