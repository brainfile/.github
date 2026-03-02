# Brainfile

**An open protocol for agentic task coordination.**

Brainfile is a file-based task management system that keeps project coordination inside your codebase, where your agents live and work.

### Architecture

- **Board**: Active tasks live in `.brainfile/board/` as individual markdown files.
- **Logs**: Completion records are appended to `.brainfile/logs/ledger.jsonl` for permanent history.
- **Rules**: Configuration and promoted ADRs inject context into every agent interaction.

### Key Features

- **Strict Types**: Tasks, Epics, and ADRs with schema validation.
- **Contracts**: Define deliverables and validation for AI agents.
- **ADR Promotion**: Turn architectural decisions into active rules.
- **Agent Tools**: CLI, MCP server, and Python/TypeScript libraries.

### Packages

| Package | Description |
|---------|-------------|
| [@brainfile/cli](https://github.com/brainfile/cli) | CLI with TUI and MCP server |
| [@brainfile/core](https://github.com/brainfile/core) | TypeScript library |
| [brainfile](https://github.com/brainfile/py) | Python library |
| [Protocol](https://github.com/brainfile/protocol) | Specification and JSON schemas |

### Links

- [Documentation](https://brainfile.md)
- [NPM Packages](https://www.npmjs.com/search?q=%40brainfile)
- [PyPI Package](https://pypi.org/project/brainfile/)
