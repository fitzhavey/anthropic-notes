# MCP servers with Claude Code

Course: [Claude Code in Action](https://anthropic.skilljar.com/claude-code-in-action) · Section: Getting hands on

You can extend Claude Code's capabilities by adding MCP (Model Context Protocol) servers. These servers run remotely or locally and provide Claude with new tools and abilities it wouldn't normally have. One of the most popular is **Playwright**, which gives Claude the ability to control a web browser.

## Installing the Playwright MCP server

Run this in your terminal (not inside Claude Code):

```bash
claude mcp add playwright npx @playwright/mcp@latest
```

This names the MCP server "playwright" and provides the command that starts the server locally on your machine.

## Managing permissions

When you first use MCP server tools, Claude asks for permission each time. To pre-approve the server, edit `.claude/settings.local.json` and add the server to the `allow` array:

```json
{
  "permissions": {
    "allow": ["mcp__playwright"],
    "deny": []
  }
}
```

Note the double underscores in `mcp__playwright`. This lets Claude use the Playwright tools without asking for permission every time.

## Practical example: improving component generation

A real-world workflow with the Playwright MCP server — instead of manually testing and tweaking prompts, you can have Claude:

1. Open a browser and navigate to your application
2. Generate a test component
3. Analyze the visual styling and code quality
4. Update the generation prompt based on what it observes
5. Test the improved prompt with a new component

For instance:

> "Navigate to localhost:3000, generate a basic component, review the styling, and update the generation prompt at @src/lib/prompts/generation.tsx to produce better components going forward."

Claude uses the browser tools to interact with your app, examines the generated output, and then modifies your prompt file to encourage more original designs.

## Results and benefits

Instead of generic purple-to-blue gradients and standard Tailwind patterns, Claude might update prompts to encourage warm sunset gradients, ocean depth themes, asymmetric designs, and creative spacing. The key advantage is that Claude can see the actual visual output, not just the code, which allows much more informed styling decisions.

## Exploring other MCP servers

Playwright is just one example. The ecosystem includes servers for database interactions, API testing and monitoring, file system operations, cloud service integrations, and development tool automation. Explore MCP servers that align with your specific development needs — they can transform Claude from a code assistant into a comprehensive development partner that interacts with your entire toolchain.
