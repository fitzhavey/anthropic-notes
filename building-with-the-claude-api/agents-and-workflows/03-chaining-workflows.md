# Chaining workflows

Course: [Building with the Claude API](https://anthropic.skilljar.com/claude-with-the-anthropic-api) · Module: Agents and workflows

Chaining workflows might seem obvious at first, but they're actually one of the most useful patterns you'll encounter when working with Claude. This approach becomes especially valuable when you're dealing with complex tasks or long prompts that Claude struggles to handle consistently.

## What is workflow chaining?

A chaining workflow breaks down a large, complex task into smaller, sequential subtasks. Instead of asking Claude to do everything at once, you split the work into focused steps that build on each other.

For example, imagine building a social media marketing tool that creates and posts videos automatically. Rather than one massive prompt, you could break it down:

1. Find related trending topics on Twitter
2. Select the most interesting topic (using Claude)
3. Research the topic (using Claude)
4. Write a script for a short format video (using Claude)
5. Use an AI avatar and text-to-speech to create a video
6. Post the video to social media

## Why chain instead of one big prompt?

You might wonder why not just combine all the Claude tasks into a single prompt. The key benefit is focus — when you give Claude one specific task at a time, it can concentrate on doing that task well rather than juggling multiple requirements simultaneously. The chaining approach lets you:

- Split large tasks into smaller, non-parallelizable subtasks
- Optionally do non-LLM processing between each task
- Keep Claude focused on one aspect of the overall task

## The long prompt problem

Chaining becomes really valuable when you need Claude to write content with many specific constraints. Say you want Claude to write a technical article that should:

- Not mention that it's written by an AI
- Avoid using emojis
- Skip clichéd or overly casual language
- Write in a professional, technical tone

Even with all these constraints clearly stated, Claude might still produce content that violates some of your rules — an article that still uses emojis, mentions AI authorship, or sounds unprofessional.

## The chaining solution

Instead of fighting with one massive prompt, use a two-step chaining approach:

**Step 1:** Send your initial prompt and accept that the first result might not be perfect. Claude will generate an article, but it might violate some of your constraints.

**Step 2:** Make a follow-up request that focuses specifically on fixing the issues. Provide the article Claude just wrote and give it targeted revision instructions:

```
Revise the article provided below. Follow these steps to rewrite the article:
1. Identify any location where the text identifies the author as an AI and remove them
2. Find and remove all emojis
3. Locate any cringey writing and replace it with text that would be written by a technical writer
```

This works because Claude can focus entirely on the revision task rather than trying to balance content creation with constraint adherence.

## When to use chaining

Chaining workflows are particularly useful when:

- You have complex tasks with multiple requirements
- Claude consistently ignores some constraints in long prompts
- You need to process or validate outputs between steps
- You want to keep each interaction focused and manageable

While chaining might seem like extra work, it often produces better results than trying to cram everything into a single prompt. The key is recognizing when a task is complex enough to benefit from being broken down into focused, sequential steps.
