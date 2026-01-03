# Project Context for Claude Code

## Environment

This project runs inside a Docker devcontainer with the following tools:

- **Python**: 3.11
- **Package Manager**: uv (use `uv add <package>` to add dependencies)
- **Node.js**: 20 LTS
- **GitHub CLI**: gh (authenticated via GITHUB_TOKEN)

## Available Commands

```bash
# Python package management
uv add <package>        # Add a dependency
uv sync                 # Install all dependencies
uv run <command>        # Run a command in the virtual environment

# GitHub CLI
gh repo clone <repo>    # Clone a repository
gh pr create            # Create a pull request
gh issue list           # List issues

# Claude Code
claude                  # Start Claude Code CLI
```

## Project Structure

- `pyproject.toml` - Python project configuration and dependencies
- `.devcontainer/` - Docker development environment configuration

## Notes

- This environment runs inside a Docker container
- The workspace is mounted at `/workspaces/project`
- Use `uv` instead of `pip` for package management
- GITHUB_TOKEN is available for GitHub operations
