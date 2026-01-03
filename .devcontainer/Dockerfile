# Claude Code + Python Development Environment
FROM mcr.microsoft.com/devcontainers/python:3.11

# Install Node.js 20 LTS
RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash - \
    && apt-get install -y nodejs \
    && npm install -g npm@latest

# Install uv (fast Python package manager)
RUN curl -LsSf https://astral.sh/uv/install.sh | sh \
    && echo 'export PATH="$HOME/.local/bin:$PATH"' >> /home/vscode/.bashrc

# Install GitHub CLI
RUN curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg \
    && chmod go+r /usr/share/keyrings/githubcli-archive-keyring.gpg \
    && echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | tee /etc/apt/sources.list.d/github-cli.list > /dev/null \
    && apt-get update \
    && apt-get install -y gh

# Install additional tools
RUN apt-get update && apt-get install -y \
    ripgrep \
    jq \
    && rm -rf /var/lib/apt/lists/*

# Install Claude Code
RUN npm install -g @anthropic-ai/claude-code

# Set PATH for uv
ENV PATH="/home/vscode/.local/bin:${PATH}"

# Switch to non-root user
USER vscode
