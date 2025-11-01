how to use claude code on vscode (ubuntu) . I have an account and a plan with claude ai. give the core instructions rather than words.

To use Claude Code in VSCode on Ubuntu, follow these core steps for installation and integration. This enables Anthropic’s Claude AI code assistant directly in your editor using your paid account and API key[1][2][3].

### System Preparation

- Update your system:
  - `sudo apt update && sudo apt upgrade -y` [1]
- Install Node.js (LTS, recommended v18+):
  - Remove old versions: `sudo apt remove nodejs npm`
  - Install latest LTS:  
    ```
    curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
    sudo apt install -y nodejs
    ```
  - Verify: `node --version` (should show v20.x.x), `npm --version` (should show v10+) [1]

### Claude Code CLI Installation

- Configure npm for global installs:
  ```
  mkdir -p ~/.npm-global
  npm config set prefix ~/.npm-global
  echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.bashrc
  source ~/.bashrc
  ```
- Install CLI (do not use sudo):
  - `npm install -g @anthropic-ai/claude-code` [1][2]
  - Test: `claude --version`

### Authenticate with Anthropic

- Run CLI in your project directory:
  - `cd your-project-directory`
  - `claude`
- On first launch, follow instructions to authenticate using your API key or OAuth to link your Anthropic account[1][2].

### VSCode Integration

- Open VSCode, open integrated terminal.
- Start Claude:
  - Run `claude` in terminal; it will auto-detect VSCode context[3][2].
- (Optional) Install the VSCode Extension:
  - Get latest `.vsix` from Anthropic or Visual Studio Marketplace, then in VSCode:
    - Go to Extensions > More Actions > Install from VSIX, select the file[2][4].
- Keyboard shortcuts:
  - Launch Claude: `Ctrl+Esc`
  - File reference: `Alt+Ctrl+K`
  - Undo: Double tap `Esc`
  - Accept: `Shift+Tab`
- Run `/config` in Claude CLI for configuration[3].

### Usage

- Claude will read open files and selections, offer suggestions, and show diffs in the editor[2][3].
- Share context and use Claude for code completion, edits, explanations, and refactoring via prompt or inline commands.

This workflow gives you deep integration of Claude AI code capabilities in VSCode under Ubuntu, leveraging your claude.ai plan efficiently[1][2][3].

Citations:
[1] How to Install Claude Code on Ubuntu Linux: Complete Guide 2025 https://itecsonline.com/post/how-to-install-claude-code-on-ubuntu-linux-complete-guide-2025
[2] How to Integrate Claude Code with VSCode and JetBrains? https://apidog.com/blog/claude-code-ide-integrations/
[3] Setting Up Claude Code in VS Code https://community.aws/content/2v5sof1SSJ89ke01CbCE6o4GZKz/setting-up-claude-code-in-vs-code?lang=en
[4] Claude Coder https://marketplace.visualstudio.com/items?itemName=kodu-ai.claude-dev-experimental
[5] Integrating Claude AI in VSCode: What You Need to Know https://howik.com/integrate-claude-ai-in-vscode
[6] How To Setup And Use Claude AI In Linux Terminal? [2024] - Claude AI https://claudeai.pro/how-to-setup-and-use-claude-ai-in-linux-terminal/
[7] How to Use Claude AI in VS Code (Claude VS Code Tutorial) https://www.youtube.com/watch?v=gpU4bcqo1yM
[8] Best way to integrate with visual studio code https://www.reddit.com/r/ClaudeAI/comments/1gyl85h/best_way_to_integrate_with_visual_studio_code/
[9] GitHub - Moto/claude-vscode-extension https://github.com/Moto/claude-vscode-extension
[10] Set up Claude Code https://docs.claude.com/en/docs/claude-code/setup
