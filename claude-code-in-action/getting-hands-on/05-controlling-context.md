# Controlling context

Course: [Claude Code in Action](https://anthropic.skilljar.com/claude-code-in-action) · Section: Getting hands on

> **Note:** The video shows an older `#` shortcut for adding memories. Use `/memory` instead.

When working with Claude on complex tasks, you'll often need to guide the conversation to keep it focused and productive. Several techniques help you control the flow.

## Interrupting Claude with Escape

Sometimes Claude starts heading in the wrong direction or tries to tackle too much at once. Press the **Escape** key to stop Claude mid-response, allowing you to redirect. This is useful when you want Claude to focus on one specific task instead of handling multiple things simultaneously — e.g. if you ask for tests across multiple functions and it starts a comprehensive plan for all of them, interrupt and ask it to focus on one at a time.

## Combining Escape with memories

A powerful application of the escape technique is fixing repetitive errors. When Claude makes the same mistake across conversations:

1. Press **Escape** to stop the current response
2. Run `/memory` (or edit `CLAUDE.md` directly) to add a note about the correct approach
3. Continue the conversation with the corrected information

This prevents Claude from making the same error in future conversations on your project.

## Rewinding conversations

During long conversations, you might accumulate context that becomes irrelevant or distracting (e.g. a debugging back-and-forth that isn't useful for the next task). Rewind by pressing **Escape twice** or typing `/rewind`. This shows all the messages you've sent, letting you jump back to an earlier point and continue from there. This helps you:

- Maintain valuable context (like Claude's understanding of your codebase)
- Remove distracting or irrelevant conversation history
- Keep Claude focused on the current task

## Context management commands

### `/compact`

Summarizes your entire conversation history while preserving the key information Claude has learned. Ideal when:

- Claude has gained valuable knowledge about your project
- You want to continue with related tasks
- The conversation has become long but contains important context

### `/clear`

Starts a new conversation with fresh context. Most useful when:

- You're switching to a completely different, unrelated task
- The current context might confuse Claude for the new task
- You want to start over without any previous context

You can still go back to the previous conversation later with `/resume` — `/clear` does not remove the conversation from your session history.

## When to use these techniques

These conversation control techniques are particularly valuable during:

- Long-running conversations where context can become cluttered
- Task transitions where previous context might be distracting
- Situations where Claude repeatedly makes the same mistakes
- Complex projects where you need to maintain focus on specific components

Used strategically, escape, double-tap escape, `/compact`, and `/clear` aren't just conveniences — they're essential tools for maintaining effective AI-assisted development sessions.
