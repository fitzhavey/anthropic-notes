# Implementing a hook

Course: [Claude Code in Action](https://anthropic.skilljar.com/claude-code-in-action) · Section: Hooks and the SDK

Let's build a hook that prevents Claude from reading sensitive files — a practical example of a PreToolUse hook intercepting tool calls before they run.

## What this exercise covers

You'll write a hook that blocks the `Read` tool from opening `.env`, protecting your environment variables during a session.

This hook covers `Read` only. Blocking `Grep` or `Bash` from reaching the same file requires checking each tool's input shape separately, since each tool sends different fields. For comprehensive file protection, combine a hook with a `permissions.deny` rule like `"Read(**/.env)"`.

## Configure the hook

Open `.claude/settings.local.json` and add a PreToolUse hook that matches the `Read` tool:

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Read",
        "hooks": [
          { "type": "command", "command": "node $PWD/hooks/read_hook.js" }
        ]
      }
    ]
  }
}
```

## Write the hook script

Create `hooks/read_hook.js`:

```javascript
process.stdin.setEncoding("utf8");
let input = "";
process.stdin.on("data", (d) => (input += d));
process.stdin.on("end", () => {
  const toolArgs = JSON.parse(input);
  const readPath = toolArgs.tool_input?.file_path || "";
  if (readPath.includes(".env")) {
    console.error("You cannot read the .env file");
    process.exit(2);
  }
  process.exit(0);
});
```

The hook reads the tool call from stdin as JSON, checks `tool_input.file_path`, and exits with code 2 to block the call. Anything written to stderr becomes the message Claude sees.

## Test it

In a Claude Code session, ask Claude to read your `.env` file. You should see:

```
You cannot read the .env file
```

That's the hook blocking the `Read` call. Ask Claude to read a different file and it works normally.

## Why Read only?

Each tool sends a different input shape:

- `Read` sends `{"file_path": "..."}`
- `Grep` sends `{"pattern": "...", "path": "..."}`, where `path` is a search directory, not a file
- `Bash` sends `{"command": "..."}`

A check on `file_path` catches `Read` but won't catch a project-wide grep for `API_KEY` or a `cat .env` in Bash. To cover those, write separate matchers per tool and inspect each one's specific fields — or use `permissions.deny` rules, which apply uniformly across tools.
