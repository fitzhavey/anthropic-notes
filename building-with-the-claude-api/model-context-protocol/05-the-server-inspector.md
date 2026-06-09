# The server inspector

Course: [Building with the Claude API](https://anthropic.skilljar.com/claude-with-the-anthropic-api) · Module: Model Context Protocol

When building MCP servers, you need a way to test your functionality without connecting to a full application. The Python MCP SDK includes a built-in browser-based inspector that lets you debug and test your server in real-time.

## Starting the inspector

First, make sure your Python environment is activated (check your project's README for the exact command). Then run the inspector with:

```bash
mcp dev mcp_server.py
```

This starts a development server on port 6277 and gives you a local URL to open in your browser. The inspector interface loads, showing the MCP Inspector dashboard.

> **Note:** The MCP inspector is actively being developed, so the interface you see might look different from current screenshots. The core functionality for testing tools, resources, and prompts should remain similar.

## Connecting and testing tools

Click the "Connect" button on the left side to start your MCP server. Once connected, you'll see a navigation bar with sections for Resources, Prompts, Tools, and other features. To test your tools:

1. Navigate to the Tools section
2. Click "List Tools" to see all available tools
3. Select a tool to open its testing interface
4. Fill in the required parameters
5. Click "Run Tool" to execute and see results

## Testing document operations

For example, to test a document reading tool, you'd enter a document ID (like "deposition.md") and run the tool. The inspector shows the result, including any returned content or success messages.

You can chain operations to verify functionality. For instance, after editing a document by replacing text, you can immediately run the read tool again to confirm the changes were applied correctly.

## Development workflow

The inspector creates an efficient development loop:

1. Make changes to your MCP server code
2. Test individual tools through the inspector
3. Verify results without needing a full application setup
4. Debug issues in isolation

This tool becomes essential as you build more complex MCP servers. It eliminates the need to wire up your server to Claude or another application just to test basic functionality, making development much faster and more focused.
