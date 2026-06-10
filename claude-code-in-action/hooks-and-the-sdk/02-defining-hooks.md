# Defining hooks

Course: [Claude Code in Action](https://anthropic.skilljar.com/claude-code-in-action) · Section: Hooks and the SDK

> Lesson downloads: [queries](../.resources/queries), [queries_COMPLETED](../.resources/queries_COMPLETED)

Hooks let you intercept and control tool calls before or after they execute, giving you fine-grained control over what Claude can and cannot do in your development environment.

## Building a hook

Creating a hook involves four main steps:

1. **Decide on a PreToolUse or PostToolUse hook** — PreToolUse hooks can prevent tool calls from executing; PostToolUse hooks run after the tool has already been used.
2. **Determine which tool calls to watch for** — specify exactly which tools should trigger your hook.
3. **Write a command that receives the tool call** — this command gets JSON data about the proposed tool call via standard input.
4. **If needed, provide feedback to Claude** — your command's exit code tells Claude whether to allow or block the operation.

## Available tools

Claude Code provides several built-in tools you can monitor with hooks. To see exactly which tools are available in your current setup, ask Claude directly for a list. This is especially useful since the available tools can change when you add custom MCP servers.

## Tool call data structure

When your hook command executes, Claude sends JSON data through standard input containing details about the proposed tool call:

```json
{
  "session_id": "2d6a1e4d-6...",
  "transcript_path": "/Users/sg/...",
  "hook_event_name": "PreToolUse",
  "tool_name": "Read",
  "tool_input": {
    "file_path": "/code/queries/.env"
  }
}
```

Your command reads this JSON from standard input, parses it, and decides whether to allow or block the operation based on the tool name and input parameters.

## Exit codes and control flow

Your hook command communicates back to Claude through exit codes:

- **Exit code 0** — everything is fine, allow the tool call to proceed
- **Exit code 2** — block the tool call (PreToolUse hooks only)

When you exit with code 2 in a PreToolUse hook, any error messages you write to standard error are sent to Claude as feedback, explaining why the operation was blocked.

## Example use case

A common use case is preventing Claude from reading sensitive files like `.env` files. Since both the `Read` and `Grep` tools can access file contents, you'd monitor both tool types and check whether they're trying to access restricted file paths. This gives you complete control over Claude's file system access while providing clear feedback about why certain operations are restricted.
