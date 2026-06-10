# Another useful hook

Course: [Claude Code in Action](https://anthropic.skilljar.com/claude-code-in-action) · Section: Hooks and the SDK

There are more hook types beyond the PreToolUse and PostToolUse hooks covered so far:

- **Notification** — runs when Claude Code sends a notification (when it needs permission to use a tool, or after being idle for 60 seconds)
- **Stop** — runs when Claude Code has finished responding
- **SubagentStop** — runs when a subagent (displayed as a "Task" in the UI) has finished
- **PreCompact** — runs before a compact operation occurs, manual or automatic
- **UserPromptSubmit** — runs when the user submits a prompt, before Claude processes it
- **SessionStart** — runs when starting or resuming a session
- **SessionEnd** — runs when a session ends

## The confusing part

Two things vary in your hook's stdin input:

- The stdin input changes based on the **hook type** (PreToolUse, PostToolUse, Notification, etc.)
- The `tool_input` within it differs based on the **tool that was called** (for PreToolUse and PostToolUse hooks)

For example, here's sample stdin to a PostToolUse hook watching for uses of the `TodoWrite` tool (the tool Claude uses to track to-do items):

```json
{
  "session_id": "9ecf22fa-edf8-4332-ae85-b6d5456eda64",
  "transcript_path": "<path_to_transcript>",
  "hook_event_name": "PostToolUse",
  "tool_name": "TodoWrite",
  "tool_input": {
    "todos": [{ "content": "write a readme", "status": "pending", "id": "1" }]
  },
  "tool_response": {
    "oldTodos": [],
    "newTodos": [{ "content": "write a readme", "status": "pending", "id": "1" }]
  }
}
```

And for comparison, the input to a Stop hook:

```json
{
  "session_id": "af9f50b6-f042-4773-b3e2-c3a4814765ce",
  "transcript_path": "<path_to_transcript>",
  "hook_event_name": "Stop",
  "stop_hook_active": false
}
```

The stdin differs significantly based on the hook and the matcher used. This can make writing hooks challenging — you might not know the exact structure of the input.

## A helper hook for inspecting input

To handle this, make a helper hook that logs the input:

```json
"PostToolUse": [ // Or "PreToolUse" or "Stop", etc
  {
    "matcher": "*",
    "hooks": [
      {
        "type": "command",
        "command": "jq . > post-log.json"
      }
    ]
  }
]
```

This command writes the hook's input to `post-log.json`, letting you inspect exactly what would have been fed into your command. That makes it much easier to understand what data your real command should inspect.
