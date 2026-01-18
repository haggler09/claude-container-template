# Claude Code + Python Development Environment
FROM mcr.microsoft.com/devcontainers/python:3.11

# Install Node.js 20 LTS
RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash - \
    && apt-get install -y nodejs \
    && npm install -g npm@latest

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

# Install Neovim 0.11+ (required for vim.lsp.config API)
RUN ARCH=$(uname -m) && \
    if [ "$ARCH" = "aarch64" ]; then \
      NVIM_ARCH="arm64"; \
    else \
      NVIM_ARCH="x86_64"; \
    fi && \
    curl -LO "https://github.com/neovim/neovim/releases/download/v0.11.0/nvim-linux-${NVIM_ARCH}.tar.gz" && \
    tar -xzf "nvim-linux-${NVIM_ARCH}.tar.gz" && \
    mv "nvim-linux-${NVIM_ARCH}" /opt/nvim && \
    ln -s /opt/nvim/bin/nvim /usr/local/bin/nvim && \
    rm "nvim-linux-${NVIM_ARCH}.tar.gz"

# Create neovim config that loads project-specific config
RUN mkdir -p /home/vscode/.config/nvim && \
    cat <<'EOF' > /home/vscode/.config/nvim/init.lua
local project_config = vim.fn.getcwd() .. "/.nvim/init.lua"
if vim.fn.filereadable(project_config) == 1 then
  dofile(project_config)
end
EOF
RUN chown -R vscode:vscode /home/vscode/.config

# Install Claude Code
RUN npm install -g @anthropic-ai/claude-code

# Switch to non-root user
USER vscode

# Install uv (fast Python package manager) as vscode user
RUN curl -LsSf https://astral.sh/uv/install.sh | sh

# Set PATH for uv and configure link mode for Docker volumes
ENV PATH="/home/vscode/.local/bin:${PATH}"
ENV UV_LINK_MODE=copy
