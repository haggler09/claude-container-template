# Claude Code Python Development Template

Docker devcontainer template for Python development with Claude Code.

## Features

- Python 3.11
- uv (fast Python package manager)
- Claude Code CLI
- GitHub CLI (gh)
- VS Code extensions (Python, Pylance, Ruff)

## Prerequisites

- Docker Desktop
- VS Code with Dev Containers extension
- GitHub Personal Access Token (for gh commands)

## Quick Start

### Using as Template

1. Click "Use this template" on GitHub
2. Create a new repository from this template
3. Clone your new repository
4. Open in VS Code
5. Click "Reopen in Container" when prompted
6. Run `claude` to start Claude Code

### Environment Setup

Set your GitHub token before opening the container:

```bash
export GITHUB_TOKEN="ghp_xxxxxxxxxxxx"
```

### First Run

When you first run `claude`, you'll need to authenticate:

1. Run `claude` in the terminal
2. Follow the OAuth flow to sign in with claude.ai
3. Start coding with Claude Code!

## Usage

### Package Management

```bash
uv add requests          # Add a package
uv add --dev pytest      # Add a dev package
uv sync                  # Install all packages
uv run python script.py  # Run a script
```

### GitHub CLI

```bash
gh auth status           # Check auth status
gh repo clone owner/repo # Clone a repository
gh pr create             # Create a pull request
```

## Customization

- Edit `pyproject.toml` to add project dependencies
- Modify `.devcontainer/Dockerfile` for additional tools
- Update `CLAUDE.md` with project-specific context
