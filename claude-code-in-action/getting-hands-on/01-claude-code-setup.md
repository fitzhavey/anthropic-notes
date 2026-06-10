# Claude Code setup

Course: [Claude Code in Action](https://anthropic.skilljar.com/claude-code-in-action) · Section: Getting hands on

Time to get Claude Code set up locally. Full setup instructions: <https://code.claude.com/docs/en/quickstart>

## Install Claude Code

- **MacOS, Linux, WSL:** `curl -fsSL https://claude.ai/install.sh | bash`
- **Windows PowerShell:** `irm https://claude.ai/install.ps1 | iex`
- **Windows Command Prompt (cmd.exe):** `curl -fsSL https://claude.ai/install.cmd -o install.cmd && install.cmd && del install.cmd`
- **MacOS (Homebrew):** `brew install --cask claude-code`

## First run

After installation, run `claude` in your terminal. The first time you run this command you'll be prompted to pick a color theme for the terminal and authenticate with your claude.ai credentials.

If you get an error that `claude` isn't found after installing, or you hit a network or permissions error, see "Troubleshoot installation issues" in the docs.

> Using Claude Code through Amazon Bedrock, Google Cloud Vertex AI, or Microsoft Foundry? See third-party provider setup for additional setup instructions.
