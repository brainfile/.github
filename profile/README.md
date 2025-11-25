# Brainfile

**Task management in your repo.** One markdown file. Full kanban board.

Your tasks live in a `brainfile.md` file alongside your code. No SaaS. No accounts. No sync issues. Works offline. Version-controlled with git. AI assistants can read and update it directly.

```yaml
---
title: My Project
columns:
  - id: todo
    title: To Do
    tasks:
      - id: task-1
        title: Implement user authentication
        priority: high
  - id: in-progress
    title: In Progress
    tasks: []
  - id: done
    title: Done
    tasks: []
---
```

That's the entire format. Human-readable. Machine-parseable. Git-friendly.

## Why Brainfile?

- **Lives in your repo** — Branch tasks with code. Merge them together. Roll back if needed.
- **Works offline** — It's a file. No internet required.
- **AI integration** — MCP server lets Claude, Cursor, and other AI tools update tasks directly.
- **No vendor lock-in** — Plain markdown. Use any editor. Build your own tools.
- **Free forever** — Not freemium. Just free.

## Repository Structure

| Repository | Description | Links |
|------------|-------------|-------|
| **[protocol](https://github.com/brainfile/protocol)** | JSON Schema, specification, and documentation | [Schema](https://brainfile.md/v1) |
| **[core](https://github.com/brainfile/core)** | TypeScript/JavaScript library for parsing and validation | [npm](https://npmjs.com/package/@brainfile/core) |
| **[cli](https://github.com/brainfile/cli)** | Command-line interface for task management | [npm](https://npmjs.com/package/@brainfile/cli) |
| **[vscode](https://github.com/brainfile/vscode)** | Visual Studio Code extension with kanban UI | [Marketplace](#) |

## Quick Start

```bash
# Install
npm install -g @brainfile/cli

# Create a brainfile
brainfile init

# Open the TUI
brainfile
```

That's it. You have a kanban board in your terminal.

### AI Integration (Optional)

Add this to your MCP settings (`.mcp.json`):

```json
{
  "mcpServers": {
    "brainfile": {
      "command": "npx",
      "args": ["@brainfile/cli", "mcp"]
    }
  }
}
```

Now Claude Code, Cursor, and other MCP-compatible assistants can list, add, move, and update tasks directly.

## Who It's For

- **Solo devs** who want simplicity without paying for Linear or setting up Jira
- **AI-assisted developers** using Claude Code, Cursor, or similar tools
- **Developers tired of freemium tools** that slowly gate features behind pricing tiers
- **Builders** who want a library to build custom task management tools
- **Anyone** who wants local-first task management without cloud dependencies

## Documentation

- **Website**: [brainfile.md](https://brainfile.md)
- **Quick Start**: [brainfile.md/quick-start](https://brainfile.md/quick-start)
- **CLI Reference**: [brainfile.md/tools/cli](https://brainfile.md/tools/cli)
- **MCP Integration**: [brainfile.md/tools/mcp](https://brainfile.md/tools/mcp)

## Contributing

Contributions welcome. Each repository is independent:

| Repo | Purpose |
|------|---------|
| [protocol](https://github.com/brainfile/protocol) | Spec, schema, docs |
| [core](https://github.com/brainfile/core) | TypeScript library |
| [cli](https://github.com/brainfile/cli) | CLI & MCP server |
| [vscode](https://github.com/brainfile/vscode) | VSCode extension |

## Philosophy

> **The protocol is the product.**

The `brainfile.md` format is the core. Tools are conveniences. You can write a brainfile by hand with any text editor and never install anything else.

---

MIT License

