# MCP clients

Course: [Building with the Claude API](https://anthropic.skilljar.com/claude-with-the-anthropic-api) · Module: Model Context Protocol

The MCP client serves as the communication bridge between your server and MCP servers. Think of it as your access point to all the tools that an MCP server provides. When you need to use external tools or services, the client handles all the message passing and protocol details for you.

## Transport agnostic communication

One of MCP's key strengths is being transport agnostic — the client and server can talk to each other using different communication methods. The most common setup runs both the MCP client and server on the same machine, where they communicate through standard input/output. But you're not limited to that approach. MCP clients and servers can also connect over:

- HTTP
- WebSockets
- Various other network protocols

## Message types

Once connected, the client and server exchange specific message types defined in the MCP specification. The main ones:

- **ListToolsRequest / ListToolsResult** — The client asks the server "what tools do you provide?" and gets back a list of available tools.
- **CallToolRequest / CallToolResult** — The client asks the server to run a specific tool with certain arguments, then receives the results.

## Complete flow example

Here's how all the pieces work together when a user asks "What repositories do I have?":

1. A user submits a query to your server. Your server realizes it needs to provide Claude with a list of available tools before making the request.
2. Your server asks the MCP client for tools, which sends a `ListToolsRequest` to the MCP server and receives a `ListToolsResult` back.
3. Now your server has everything needed to make the initial request to Claude — both the user's question and the available tools.
4. Claude examines the tools and decides it needs to call one to answer the question. It responds with a tool use request.
5. Your server asks the MCP client to execute the tool Claude requested. The MCP client sends a `CallToolRequest` to the MCP server, which then makes the actual request to GitHub.
6. GitHub returns the repository data, which flows back through the MCP server as a `CallToolResult`, then to the MCP client, and finally to your server.
7. Your server sends the tool results back to Claude in a follow-up message. Claude now has all the information it needs to formulate a complete response.
8. Claude responds with the formatted answer, which your server passes back to the user.

This flow involves many steps, but each component has a clear responsibility. The MCP client abstracts away the complexity of server communication, letting you focus on building your application logic.
