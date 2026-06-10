# Useful hooks!

Course: [Claude Code in Action](https://anthropic.skilljar.com/claude-code-in-action) · Section: Hooks and the SDK

Hooks can address common weaknesses in AI-assisted development, particularly on larger projects. These hooks run automatically when Claude makes changes, providing immediate feedback and preventing common issues.

## TypeScript type checking hook

One of the most useful hooks addresses a fundamental problem: when Claude modifies a function signature, it often doesn't update all the call sites throughout your project.

For example, if you ask Claude to add a `verbose` parameter to a function in `schema.ts`, it will update the function definition but miss the call site in `main.ts`, creating type errors Claude doesn't immediately catch.

The solution is a PostToolUse hook that runs the TypeScript compiler after every file edit. It:

1. Runs `tsc --noEmit` to check for type errors
2. Captures any errors found
3. Feeds the errors back to Claude immediately
4. Prompts Claude to fix the issues in other files

This works for any typed language where you can run a type checker. For untyped languages, you could implement similar functionality using automated tests instead.

## Query duplication prevention hook

In larger projects with many database queries, Claude sometimes creates duplicate functionality instead of reusing existing code — especially when database operations are just one component of a complex, multi-step task.

Consider a project with multiple query files, each containing many SQL functions. When you ask Claude to "create a Slack integration that alerts about orders pending longer than 3 days," it might write a new query instead of using the existing `getPendingOrders()` function.

The query duplication hook implements a review process:

1. Triggers when Claude modifies files in the `./queries` directory
2. Launches a separate instance of Claude Code programmatically
3. Asks the second instance to review the changes and check for similar existing queries
4. If duplicates are found, provides feedback to the original Claude instance
5. Prompts Claude to remove the duplicate and use the existing functionality

## Implementation considerations

Both hooks use the PreToolUse or PostToolUse hook system. The TypeScript hook is lightweight and runs quickly. The query duplication hook requires more resources since it launches a separate Claude instance for each review.

For the query hook, consider the trade-offs:

- **Benefits** — cleaner codebase with less duplication
- **Costs** — additional time and API usage for each query directory edit
- **Recommendation** — only monitor critical directories to minimize overhead

The hooks use Claude's Agent SDK to programmatically interact with the AI, enabling sophisticated workflows where one Claude instance can review and provide feedback on another's work.

## Extending these concepts

These hooks demonstrate broader principles you can apply to your own projects:

- Use compiler/linter output to provide immediate feedback
- Implement code review processes using separate AI instances
- Focus monitoring on high-value directories where consistency matters most
- Balance automation benefits against performance costs

The key is identifying the specific pain points in your workflow and creating targeted hooks that address them automatically.
