# Introduction to Model Context Protocol

[Course on Anthropic Academy / Skilljar](https://anthropic.skilljar.com/introduction-to-model-context-protocol)

**Status:** ✅ Complete (14 of 14 lessons)

Learn how to build modular AI applications using MCP to connect Claude with external tools and data sources. 16 lectures · ~1 hour of video · 1 quiz · Certificate of completion.

## About this course

This course covers MCP, a protocol for connecting Claude to external services and data sources without manually writing tool schemas. You'll learn to build both MCP servers that expose tools, resources, and prompts, and MCP clients that consume them. The course includes a hands-on project where you implement a document management system using MCP.

## Learning objectives

By the end of this course, you'll be able to:

- Understand MCP architecture and the client-server communication model
- Build MCP servers that expose tools using the Python SDK
- Implement MCP clients to connect your applications to MCP servers
- Create resources for exposing data and prompts for pre-defined workflows
- Test and debug MCP servers using the MCP Inspector
- Choose between tools, resources, and prompts based on control patterns
- Handle resource cleanup and async communication in MCP implementations

## Prerequisites

- Basic Python programming experience
- Understanding of async/await patterns
- Familiarity with API concepts

## Who this course is for

Engineers who want to integrate Claude with external tools and services without writing tons of boilerplate integration code.

## Course sections

### MCP fundamentals & server development (8 lessons)

Start with understanding MCP's architecture and why it exists. Build your first MCP server with tools using the Python SDK, then test it with the built-in inspector.

### MCP client implementation & advanced features (8 lessons)

Build the client side to communicate with MCP servers. Implement resources for direct data access and prompts for pre-built instructions. See how everything connects in a complete application flow.

## Curriculum

**Status:** ✅ Complete (14 of 14 lessons)

> **Note:** This course is essentially identical to the Model Context Protocol module in [Building with the Claude API](../building-with-the-claude-api/model-context-protocol/), so the lessons below link to those existing notes rather than duplicating them.

### Introduction
- Welcome to the course _(video only — no notes)_
- [Introducing MCP](../building-with-the-claude-api/model-context-protocol/01-introducing-mcp.md)
- [MCP clients](../building-with-the-claude-api/model-context-protocol/02-mcp-clients.md)

### Hands-on with MCP servers
- [Project setup](../building-with-the-claude-api/model-context-protocol/03-project-setup.md)
- [Defining tools with MCP](../building-with-the-claude-api/model-context-protocol/04-defining-tools-with-mcp.md)
- [The server inspector](../building-with-the-claude-api/model-context-protocol/05-the-server-inspector.md)
- Course satisfaction survey _(survey — no notes)_

### Connecting with MCP clients
- [Implementing a client](../building-with-the-claude-api/model-context-protocol/06-implementing-a-client.md)
- [Defining resources](../building-with-the-claude-api/model-context-protocol/07-defining-resources.md)
- [Accessing resources](../building-with-the-claude-api/model-context-protocol/08-accessing-resources.md)
- [Defining prompts](../building-with-the-claude-api/model-context-protocol/09-defining-prompts.md)
- [Prompts in the client](../building-with-the-claude-api/model-context-protocol/10-prompts-in-the-client.md)

### Assessment and wrap up
- [Final assessment on MCP](final-assessment.md)
- [MCP review](mcp-review.md)
