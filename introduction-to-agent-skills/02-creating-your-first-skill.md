# Introduction to Agent Skills — Lesson 2

Course: [Introduction to Agent Skills](https://anthropic.skilljar.com/introduction-to-agent-skills) (Anthropic Academy / Skilljar)
Lesson: Creating your first skill · Estimated time: 20 minutes

## What you'll learn

By the end of this lesson you'll be able to:

- Create a skill from scratch with proper frontmatter structure
- Test and verify that a skill loads correctly in Claude Code
- Explain how Claude Code matches incoming requests to available skills
- Describe the skill priority hierarchy (Enterprise, Personal, Project, Plugins)

## Key takeaways

- A skill is a directory containing a `SKILL.md` file with metadata (name, description) in frontmatter and instructions below.
- Claude loads only skill names and descriptions at startup, then matches incoming requests against those descriptions using semantic matching.
- You get a confirmation prompt before Claude loads the full skill content into context.
- Priority for name conflicts: Enterprise → Personal → Project → Plugins.
- To update a skill, edit its `SKILL.md`. To remove one, delete its directory. Always restart Claude Code for changes to take effect.

## Creating a skill

We'll build a personal skill that teaches Claude how to write PR descriptions in a consistent format. Since it's a personal skill, it lives in your home directory and works across all your projects.

First, create a directory for your skill inside the skills folder. The directory name should match your skill name:

```bash
mkdir -p ~/.claude/skills/pr-description
```

Then create a `SKILL.md` file inside that directory. The file has two parts separated by frontmatter dashes:

```markdown
---
name: pr-description
description: Writes pull request descriptions. Use when creating a PR, writing a PR, or when the user asks to summarize changes for a pull request.
---

When writing a PR description:

1. Run `git diff main...HEAD` to see all changes on this branch
2. Write a description following this format:

## What
One sentence explaining what this PR does.

## Why
Brief context on why this change is needed

## Changes
- Bullet points of specific changes made
- Group related changes together
- Mention any files deleted or renamed
```

The name identifies your skill. The description tells Claude when to use it — this is the matching criteria. Everything after the second set of dashes is the instructions Claude follows when the skill is activated.

## Testing your skill

Claude Code loads skills at startup, so restart your session after creating one. You can verify it's available by checking the available skills list.

You should see your skill listed. To test it, make some changes on a branch and say something like "write a PR description for my changes." Claude will indicate it's using the PR description skill, check your diff, and write a description following your template — same format every time.

## How skill matching works

When Claude Code starts, it scans four locations for skills but only loads the name and description — not the full content. This is an important detail.

When you send a request, Claude compares your message against the descriptions of all available skills. For example, "explain what this function does" would match a skill described as "explain code with visual diagrams" because the intent overlaps.

Once a match is found, Claude asks you to confirm loading the skill. This confirmation step keeps you aware of what context Claude is pulling in. After you confirm, Claude reads the complete `SKILL.md` file and follows its instructions.

## Skill priority

If you clone a repository that has a skill with the same name as one of your personal skills, which one wins? There's a clear priority order:

1. **Enterprise** — managed settings, highest priority
2. **Personal** — your home directory (`~/.claude/skills`)
3. **Project** — the `.claude/skills` directory inside a repository
4. **Plugins** — installed plugins, lowest priority

This lets organizations enforce standards through enterprise skills while still allowing individual customization. If your company has an enterprise "code-review" skill and you create a personal "code-review" skill with the same name, the enterprise version takes precedence.

To avoid conflicts, use descriptive names. Instead of just "review," use something like "frontend-review" or "backend-review."

## Updating and removing skills

To update a skill, edit its `SKILL.md` file. To remove one, delete its directory. Restart Claude Code after any changes for them to take effect.

## Lesson reflection

- What's one task in your daily workflow that you could turn into a skill right now? What would the description look like?
- How might the priority hierarchy affect your team's skill management strategy? Would you rely more on personal or project-level skills?

## What's next

In the next lesson, you'll learn about advanced configuration options including metadata fields, tool restrictions with `allowed-tools`, and how to structure larger skills using progressive disclosure and multi-file organization.
