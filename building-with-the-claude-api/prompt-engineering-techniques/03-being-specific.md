# Being specific

Course: [Building with the Claude API](https://anthropic.skilljar.com/claude-with-the-anthropic-api) · Module: Prompt engineering techniques

One of the most effective ways to improve your results is to be specific about what you want. Instead of leaving everything up to the model's interpretation, provide clear guidelines or steps that direct Claude toward the kind of output you're looking for.

If you ask Claude to "write a short story about a character who discovers a hidden talent," it could go in countless directions — 200 words or 2,000, one character or five, any type of talent scenario. By adding specific guidelines, you give Claude a clearer target, dramatically improving both consistency and quality.

## Two types of guidelines

There are two main approaches to being specific, and you'll often see them used together.

### Output quality guidelines

Focus on listing qualities your output should have, helping you control:

- Length of the response
- Structure and format
- Specific attributes or elements to include
- Tone or style requirements

For example, a story should be under 1,000 words, include a clear action that reveals the character's talent, and feature at least one supporting character.

### Process steps

Provide specific steps for Claude to follow. Useful when you want Claude to think through a problem systematically or consider multiple perspectives before arriving at a final answer. Instead of jumping straight to writing, you might ask Claude to:

1. Brainstorm three talents that would create dramatic tension
2. Pick the most interesting talent
3. Outline a pivotal scene that reveals the talent
4. Brainstorm supporting character types that could increase the impact

## Real-world impact

The difference specificity makes is dramatic. In testing a meal planning prompt, adding guidelines improved the evaluation score from 3.92 to 7.86 — more than doubling output quality simply by telling Claude exactly what elements to include:

```
Guidelines:
1. Include accurate daily calorie amount
2. Show protein, fat, and carb amounts
3. Specify when to eat each meal
4. Use only foods that fit restrictions
5. List all portion sizes in grams
6. Keep budget-friendly if mentioned
```

## When to use each approach

**Always use output guidelines.** Include quality guidelines in almost every prompt you write — they're your safety net for consistent, useful results.

**Use process steps for complex problems** — troubleshooting, decision-making scenarios, critical thinking tasks, and any situation where you want Claude to consider multiple angles. For instance, analyzing why a sales team's performance dropped: guide it through market metrics, industry changes, individual performance, organizational changes, and customer feedback — rather than letting it focus on just one cause.

## Combining both approaches

In professional prompting, you'll often see both techniques together: guidelines that control format and content, plus steps that ensure Claude thinks through the problem thoroughly before responding. This combination gives you both consistency in results and confidence that Claude has considered all the important factors.
