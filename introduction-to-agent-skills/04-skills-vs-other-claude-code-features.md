# Introduction to Agent Skills — Lesson 4

Course: [Introduction to Agent Skills](https://anthropic.skilljar.com/introduction-to-agent-skills) (Anthropic Academy / Skilljar)
Lesson: Skills vs. other Claude Code features · Estimated time: 15 minutes

## What you'll learn

By the end of this lesson you'll be able to:

- Compare skills to CLAUDE.md, subagents, hooks, and MCP servers
- Choose the right Claude Code customization feature for a given use case
- Design a complementary setup that combines multiple features effectively

## Key takeaways

- CLAUDE.md loads into every conversation and is best for always-on project standards. Skills load on demand and are best for task-specific expertise.
- Subagents run in isolated execution contexts — use them for delegated work. Skills add knowledge to your current conversation.
- Hooks are event-driven (fire on file saves, tool calls). Skills are request-driven (activate based on what you're asking).
- MCP servers provide external tools and integrations — a different category entirely from skills.
- Each feature handles its own specialty — combine them rather than forcing everything into one approach.

## CLAUDE.md vs. skills

CLAUDE.md loads into every conversation, always. If you want Claude to use TypeScript strict mode in your project, put it in your CLAUDE.md file.

Skills load on demand. When Claude matches a request to a skill, that skill's instructions join the conversation. Your PR review checklist doesn't need to be in context when you're writing new code — it activates when you ask for a review.

Use **CLAUDE.md** for:

- Project-wide standards that always apply
- Constraints like "never modify the database schema"
- Framework preferences and coding style

Use **skills** for:

- Task-specific expertise
- Knowledge that's only relevant sometimes
- Detailed procedures that would clutter every conversation

## Skills vs. subagents

Skills add knowledge to your current conversation. When a skill activates, its instructions join the existing context.

Subagents run in a separate context. They receive a task, work on it independently, and return results. They're isolated from the main conversation.

Use **subagents** when:

- You want to delegate a task to a separate execution context
- You need different tool access than the main conversation
- You want isolation between delegated work and your main context

Use **skills** when:

- You want to enhance Claude's knowledge for the current task
- The expertise applies throughout a conversation

## Skills vs. hooks

Hooks fire on events. A hook might run a linter every time Claude saves a file, or validate input before certain tool calls. They're event-driven.

Skills are request-driven. They activate based on what you're asking.

Use **hooks** for:

- Operations that should run on every file save
- Validation before specific tool calls
- Automated side effects of Claude's actions

Use **skills** for:

- Knowledge that informs how Claude handles requests
- Guidelines that affect Claude's reasoning

## Putting it all together

A typical setup might include:

- **CLAUDE.md** — always-on project standards
- **Skills** — task-specific expertise that loads on demand
- **Hooks** — automated operations triggered by events
- **Subagents** — isolated execution contexts for delegated work
- **MCP servers** — external tools and integrations

Each handles its own specialty. Don't force everything into skills when another option fits better — and you can use multiple at a time. Skills provide automatic task-specific expertise, CLAUDE.md is for always-on instructions, subagents run in isolated contexts, hooks fire on events, and MCP provides external tools.

Use skills when you have knowledge that Claude should apply automatically when the topic is relevant, and combine them with other features for comprehensive customization.

## Lesson reflection

- Look at your current CLAUDE.md file. Is there anything in it that would work better as a skill (loaded only when relevant)?
- Think about your team's development workflow. Which combination of Claude Code features (skills, hooks, subagents, MCP) would address your most common pain points?

## What's next

In the next lesson, you'll learn how to share skills with your team and organization — from committing them to repositories, to distributing via plugins, to enterprise-wide deployment through managed settings.
