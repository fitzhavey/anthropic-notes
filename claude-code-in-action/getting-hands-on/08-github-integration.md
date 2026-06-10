# Github integration

Course: [Claude Code in Action](https://anthropic.skilljar.com/claude-code-in-action) · Section: Getting hands on

Claude Code offers an official GitHub integration that lets Claude run inside GitHub Actions. It provides two main workflows: mention support for issues and pull requests, and automatic pull request reviews.

## Setting up the integration

Run `/install-github-app` in Claude. This walks you through:

1. Installing the Claude Code app on GitHub
2. Adding your API key
3. Automatically generating a pull request with the workflow files

The generated PR adds two GitHub Actions to your repository. Once merged, you'll have the workflow files in your `.github/workflows` directory.

## Default GitHub Actions

**Mention Action** — Mention Claude in any issue or PR using `@claude`. When mentioned, Claude will analyze the request and create a task plan, execute the task with full access to your codebase, and respond with results directly in the issue or PR.

**Pull Request Action** — Whenever you create a pull request, Claude automatically reviews the proposed changes, analyzes the impact of modifications, and posts a detailed report on the PR.

## Customizing the workflows

After merging the initial PR, you can customize the workflow files.

**Adding project setup** — Steps to prepare the environment before Claude runs:

```yaml
- name: Project Setup
  run: |
    npm run setup
    npm run dev:daemon
```

**Custom instructions** — Provide context about your project setup:

```yaml
custom_instructions: |
  The project is already set up with all dependencies installed.
  The server is already running at localhost:3000. Logs from it
  are being written to logs.txt. If needed, you can query the
  db with the 'sqlite3' cli. If needed, use the mcp__playwright
  set of tools to launch a browser and interact with the app.
```

**MCP server configuration** — Give Claude additional capabilities:

```yaml
mcp_config: |
  {
    "mcpServers": {
      "playwright": {
        "command": "npx",
        "args": [
          "@playwright/mcp@latest",
          "--allowed-origins",
          "localhost:3000;cdn.tailwindcss.com;esm.sh"
        ]
      }
    }
  }
```

**Tool permissions** — When running Claude in GitHub Actions, you must explicitly list all allowed tools (especially important when using MCP servers). Unlike local development, there's no shortcut — each tool from each MCP server must be individually listed:

```yaml
allowed_tools: "Bash(npm:*),Bash(sqlite3:*),mcp__playwright__browser_snapshot,mcp__playwright__browser_click,..."
```

## Best practices

- Start with the default workflows and customize gradually
- Use custom instructions to provide project-specific context
- Be explicit about tool permissions when using MCP servers
- Test your workflows with simple tasks before complex ones
- Consider your project's specific needs when configuring additional steps

The GitHub integration transforms Claude from a development assistant into an automated team member that can handle tasks, review code, and provide insights directly within your GitHub workflow.
