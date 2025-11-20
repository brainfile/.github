# 🧠 Brainfile

**A protocol-first task management system designed for the AI era.**

Brainfile is a simple, human-readable format for managing project tasks that both humans and AI coding assistants can read, write, and collaborate through. Think of it as a shared language for project management between you and your AI pair programmer.

## The Protocol

At its core, Brainfile is just a `brainfile.md` file with YAML frontmatter:

```yaml
---
schema: https://brainfile.md/v1
title: My Project
agent:
  instructions:
    - Update task status as you work (todo → in-progress → done)
    - Make minimal, atomic changes
columns:
  - id: todo
    title: To Do
    tasks:
      - id: task-1
        title: Implement user authentication
        priority: high
  - id: done
    title: Done
    tasks: []
---
```

That's it. No database, no backend, no complex setup. Just a markdown file that lives in your repository.

## Why Brainfile?

### 🤖 **AI-First Design**
- Designed specifically for AI-assisted development
- Optional `agent` instructions guide AI behavior
- Protocol-based: tools are conveniences, the file is the source of truth

### 📝 **Human-Readable**
- Plain text YAML and Markdown
- Easy to edit directly or with tools
- Version control friendly (perfect for git)

### 🔌 **Extensible**
- JSON Schema validation
- Multiple implementations (TypeScript, CLI, VSCode)
- Build your own tools on the protocol

### 🎯 **Simple**
- No dependencies required
- File-based (no database)
- Works offline
- Portable across projects

## Repository Structure

| Repository | Description | Links |
|------------|-------------|-------|
| **[protocol](https://github.com/brainfile/protocol)** | JSON Schema, specification, and documentation | [Schema](https://brainfile.md/v1) |
| **[core](https://github.com/brainfile/core)** | TypeScript/JavaScript library for parsing and validation | [npm](https://npmjs.com/package/@brainfile/core) |
| **[cli](https://github.com/brainfile/cli)** | Command-line interface for task management | [npm](https://npmjs.com/package/@brainfile/cli) |
| **[vscode](https://github.com/brainfile/vscode)** | Visual Studio Code extension with kanban UI | [Marketplace](#) |

## Quick Start

### 1. Install the VSCode Extension

```bash
# Coming soon to VS Code Marketplace
# For now, download from releases
```

### 2. Or use the CLI

```bash
npm install -g @brainfile/cli

# Create a new brainfile
brainfile init

# List tasks
brainfile list

# Add a task
brainfile add "Implement feature" --priority high
```

### 3. Or use the library

```bash
npm install @brainfile/core
```

```typescript
import { Brainfile } from '@brainfile/core';

const brain = new Brainfile();
const board = await brain.parse('./brainfile.md');

// Access tasks
const todoTasks = board.columns.find(c => c.id === 'todo')?.tasks;

// Modify and save
brain.serialize(board, './brainfile.md');
```

## Use Cases

- 🤝 **AI Pair Programming**: Give your AI assistant context about your project's tasks
- 📋 **Project Management**: Simple, version-controlled task tracking
- 🚀 **CI/CD Integration**: Automate task updates in your pipelines
- 📝 **Documentation**: Tasks live alongside your code
- 🔄 **Async Collaboration**: AI and humans work on the same task board

## Example AI Integration

Add this comment to your README to auto-load tasks for AI assistants:

```markdown
<!-- load:brainfile.md -->
```

Now when AI coding assistants read your README, they automatically understand your project's task context.

## Schema & Documentation

- **Schema**: https://brainfile.md/v1
- **Protocol Spec**: [protocol/docs/protocol.md](https://github.com/brainfile/protocol/blob/main/docs/protocol.md)
- **Agent Guide**: [protocol/docs/agents.md](https://github.com/brainfile/protocol/blob/main/docs/agents.md)

## Contributing

We welcome contributions! Each repository has its own contributing guide:

- Protocol changes → [brainfile/protocol](https://github.com/brainfile/protocol)
- Core library → [brainfile/core](https://github.com/brainfile/core)
- CLI tool → [brainfile/cli](https://github.com/brainfile/cli)
- VSCode extension → [brainfile/vscode](https://github.com/brainfile/vscode)

## Philosophy

> **The protocol is the product.**

Brainfile is protocol-first. The `brainfile.md` format is the core, and tools (CLI, VSCode, etc.) are conveniences. You don't need any tools—just the file and an AI assistant that understands it.

This means:
- ✅ No vendor lock-in
- ✅ Your data is portable
- ✅ Build your own tools
- ✅ Works with any editor
- ✅ Compatible with future AI models

## License

MIT License - All repositories are open source.

---

**Get Started**: Check out the [protocol](https://github.com/brainfile/protocol) repository or install the [CLI](https://github.com/brainfile/cli)!

