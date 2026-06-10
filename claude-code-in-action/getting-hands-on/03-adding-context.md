# Adding context

Course: [Claude Code in Action](https://anthropic.skilljar.com/claude-code-in-action) · Section: Getting hands on

> **Note:** The video shows an older `#` "memory mode" shortcut that has been removed. Use `/memory` and direct `CLAUDE.md` edits instead.

When working with Claude on coding projects, context management is crucial. Your project might have dozens or hundreds of files, but Claude only needs the right information to help effectively. Too much irrelevant context actually decreases Claude's performance, so learning to guide it toward relevant files and documentation is essential.

## The /init command

When you first start Claude in a new project, run `/init`. This tells Claude to analyze your entire codebase and understand:

- The project's purpose and architecture
- Important commands and critical files
- Coding patterns and structure

After analyzing your code, Claude writes a summary to a `CLAUDE.md` file. When Claude asks for permission to create this file, you can hit Enter to approve each write, or press Shift+Tab to let Claude write files freely throughout your session.

## The CLAUDE.md file

The `CLAUDE.md` file serves two main purposes:

- Guides Claude through your codebase, pointing out important commands, architecture, and coding style
- Allows you to give Claude specific or custom directions

This file gets included in every request you make to Claude — it's like having a persistent system prompt for your project.

## CLAUDE.md file locations

Claude recognizes three `CLAUDE.md` files in three common locations:

- **`CLAUDE.md`** — Generated with `/init`, committed to source control, shared with other engineers
- **`CLAUDE.local.md`** — Not shared with other engineers; contains personal instructions and customizations
- **`~/.claude/CLAUDE.md`** — Used across all projects on your machine

## Adding custom instructions

You can customize how Claude behaves by adding instructions to your `CLAUDE.md` file. For example, if Claude is adding too many comments, edit `CLAUDE.md` directly in your editor, or run `/memory` inside Claude Code to open the file, and add an instruction like "Use comments sparingly. Only comment complex code." Claude reads this file at the start of every conversation, so changes apply to your next message.

## File mentions with `@`

When you need Claude to look at specific files, use the `@` symbol followed by the file path. This automatically includes that file's contents in your request. For example:

```
How does the auth system work? @auth
```

Claude will show a list of auth-related files to choose from, then include the selected file in your conversation.

## Referencing files in CLAUDE.md

You can also mention files directly in your `CLAUDE.md` using the same `@` syntax — particularly useful for files relevant to many aspects of your project. For example:

```
The database schema is defined in the @prisma/schema.prisma file. Reference it anytime you need to understand the structure of data stored in the database.
```

When you mention a file this way, its contents are automatically included in every request, so Claude can answer questions about your data structure immediately without searching for the schema file each time.

This is also useful if your repo already has an `AGENTS.md` file for another tool. You don't need to duplicate the instructions — add `@AGENTS.md` on the first line of your `CLAUDE.md`, and Claude will load that file first. Then add any Claude-specific instructions below the import.
