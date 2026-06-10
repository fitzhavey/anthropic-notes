# Making changes

Course: [Claude Code in Action](https://anthropic.skilljar.com/claude-code-in-action) · Section: Getting hands on

> **Note:** The video shows older "think harder" keywords that no longer have an effect. Use `/effort` instead.

When working with Claude in your development environment, you'll often need to make changes to existing projects. This covers practical techniques for implementing changes effectively, including visual communication with screenshots and leveraging Claude's advanced reasoning.

## Using screenshots for precise communication

One of the most effective ways to communicate with Claude is through screenshots. When you want to modify a specific part of your interface, a screenshot helps Claude understand exactly what you're referring to. To paste a screenshot into Claude, use **Ctrl+V** (not Cmd+V on macOS) — this shortcut is specifically designed for pasting screenshots into the chat. Once pasted, you can ask Claude to make specific changes to that area of your app.

## Planning Mode

For complex tasks that require extensive research across your codebase, enable Planning Mode by typing `/plan` or pressing **Shift+Tab twice** (or once if you're already auto-accepting edits). In this mode, Claude will:

- Read more files in your project
- Create a detailed implementation plan
- Show you exactly what it intends to do
- Wait for your approval before proceeding

This gives you the opportunity to review the plan and redirect Claude if it missed something important.

> **Tip:** When reviewing the plan, press **Ctrl+G** to open it in your text editor. You can make precise edits before approving, and Claude will see the final version you submit.

## Effort level: how hard Claude thinks

By default, Claude reasons through problems before answering (you'll see hints like "still thinking"). Press **Ctrl+O** to expand the actual reasoning steps. You can control how Claude reasons by setting an effort level — run `/effort` to see your current level and adjust it: **low** is faster and cheaper, **max** reasons longest on hard problems. The default depends on your model and plan.

To signal extra thinking on a single prompt, use the keyword **`ultrathink`** in your prompt. This makes Claude reason more on that turn without adjusting the session's effort level.

## When to use Planning vs. Effort

**Planning Mode** is best for:

- Tasks requiring broad understanding of your codebase
- Multi-step implementations
- Changes that affect multiple files or components

**Higher effort level** is best for:

- Complex logic problems
- Debugging difficult issues
- Algorithmic challenges

You can combine both for tasks requiring breadth and depth. Both features consume additional tokens, so there's a cost consideration.
