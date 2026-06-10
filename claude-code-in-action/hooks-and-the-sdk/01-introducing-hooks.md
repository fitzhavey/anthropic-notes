# Introducing hooks

Course: [Claude Code in Action](https://anthropic.skilljar.com/claude-code-in-action) · Section: Hooks and the SDK

Hooks let you run commands before or after Claude attempts to use a tool. They're useful for automated workflows like running code formatters after file edits, executing tests when files change, or blocking access to specific files.

## How hooks work

Normally when you ask Claude something, your query is sent to the model along with tool definitions. Claude might decide to use a tool by returning a formatted response, and Claude Code then executes that tool and returns the result.

Hooks insert themselves into this process, letting you execute code just before or just after the tool runs. Two of the most common hook types (others appear in a later lesson):

- **PreToolUse** — runs before a tool is called
- **PostToolUse** — runs after a tool is called

## Hook configuration

Hooks are defined in Claude settings files. You can add them to:

- **Global** — `~/.claude/settings.json` (affects all projects)
- **Project** — `.claude/settings.json` (shared with team)
- **Project (not committed)** — `.claude/settings.local.json` (personal settings)

Write hooks by hand in these files, or use the `/hooks` command inside Claude Code.

## PreToolUse hooks

PreToolUse hooks run before a tool is executed. They include a `matcher` that specifies which tool types to target:

```json
"PreToolUse": [
  {
    "matcher": "Read",
    "hooks": [
      {
        "type": "command",
        "command": "node /home/hooks/read_hook.js"
      }
    ]
  }
]
```

Before the `Read` tool runs, this configuration executes the specified command. Your command receives details about the tool call Claude wants to make, and you can:

- Allow the operation to proceed normally
- Block the tool call and send an error message back to Claude

## PostToolUse hooks

PostToolUse hooks run after a tool has executed. This example triggers after write or edit operations:

```json
"PostToolUse": [
  {
    "matcher": "Write|Edit",
    "hooks": [
      {
        "type": "command",
        "command": "node /home/hooks/edit_hook.js"
      }
    ]
  }
]
```

Since the tool call has already happened, PostToolUse hooks can't block it. However, they can:

- Run follow-up operations (like formatting a file that was just edited)
- Provide additional feedback to Claude about the tool use

## Practical applications

- **Code formatting** — automatically format files after Claude edits them
- **Testing** — run tests automatically when files change
- **Access control** — block Claude from reading or editing specific files
- **Code quality** — run linters or type checkers and provide feedback to Claude
- **Logging** — track what files Claude accesses or modifies
- **Validation** — check naming conventions or coding standards

The key insight: hooks let you extend Claude Code by integrating your own tools and processes into the workflow. PreToolUse hooks give you control over what Claude can do; PostToolUse hooks let you enhance what Claude has done.
