# Prompt evaluation

Course: [Building with the Claude API](https://anthropic.skilljar.com/claude-with-the-anthropic-api) · Module: Prompt evaluation

When working with Claude, writing a good prompt is just the beginning. To build reliable AI applications, you need two critical concepts: prompt engineering and prompt evaluation. Prompt engineering gives you techniques for writing better prompts; prompt evaluation helps you measure how well those prompts actually work.

## Prompt engineering vs. prompt evaluation

**Prompt engineering** is your toolkit for crafting effective prompts. It includes techniques like multishot prompting, structuring with XML tags, and many other best practices. These help Claude understand exactly what you're asking for and how you want it to respond.

**Prompt evaluation** takes a different approach. Instead of focusing on how to write prompts, it's about measuring their effectiveness through automated testing. You can test against expected answers, compare different versions of the same prompt, and review outputs for errors.

## Three paths after writing a prompt

Once you've drafted a prompt, you typically face three options:

1. **Test once and decide it's good enough.** This carries significant risk of breaking in production when users provide unexpected inputs.
2. **Test a few times and tweak it to handle a corner case or two.** Better than option 1, but users will often provide very unexpected inputs you haven't considered.
3. **Run the prompt through an evaluation pipeline** to score it, then iterate based on objective metrics. This requires more work and cost, but gives much more confidence in reliability.

## Why most engineers fall into testing traps

Options 1 and 2 are common traps that all engineers fall into. It's natural to write a prompt for a serious application and not test it thoroughly enough — we tend to underestimate how many edge cases real users will encounter. When you deploy a prompt to production, users will interact with it in ways you never anticipated, and what seemed solid during limited testing can quickly break down.

## The evaluation-first approach

Option 3 is a more systematic approach. By running your prompt through an evaluation pipeline, you get objective metrics about its performance across a broader range of test cases. This data-driven approach lets you:

- Identify weaknesses before they become production issues
- Compare different prompt versions objectively
- Iterate with confidence based on measurable improvements
- Build more reliable AI applications

It requires more upfront investment in time and testing infrastructure, but pays dividends in reliability and robustness. The goal is to catch problems during development rather than after your users encounter them.
