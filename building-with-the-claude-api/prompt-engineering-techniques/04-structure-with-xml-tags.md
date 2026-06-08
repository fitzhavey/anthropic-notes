# Structure with XML tags

Course: [Building with the Claude API](https://anthropic.skilljar.com/claude-with-the-anthropic-api) · Module: Prompt engineering techniques

When you're building prompts that include a lot of content, Claude can sometimes struggle to understand which pieces of text belong together or what different sections represent. XML tags provide a simple way to add structure and clarity, especially when interpolating large amounts of data.

## Why structure matters

Consider a prompt where you need to analyze 20 pages of sales records. Without clear boundaries, Claude might have trouble distinguishing between your instructions and the actual data you want analyzed. By wrapping the sales records in XML tags like `<sales_records>` and `</sales_records>`, you create clear delimiters that help Claude understand the structure of your prompt.

## Practical example: code and documentation

If you ask Claude to debug code using provided documentation, mixing everything together creates confusion — it's nearly impossible to tell what's code versus documentation. A better version uses `<my_code>` and `<docs>` tags to create clear boundaries.

## Custom tag names

You don't need to use official XML tags. Create descriptive names that make sense for your content:

- `<sales_records>` is better than `<data>`
- `<athlete_information>` clearly identifies user details
- `<my_code>` and `<docs>` separate different types of content

The more specific and descriptive your tag names, the better Claude can understand the purpose of each section.

## When to use XML tags

XML tags are most useful when:

- Including large amounts of context or data
- Mixing different types of content (code, documentation, data)
- You want to be extra clear about content boundaries
- Working with complex prompts that interpolate multiple variables

Even for shorter content, XML tags can serve as delimiters that make your prompt structure more obvious to Claude.

## Real-world application

```
<athlete_information>
- Height: 6'2"
- Weight: 180 lbs
- Goal: Build muscle
- Dietary restrictions: Vegetarian
</athlete_information>

Generate a meal plan based on the athlete information above.
```

This makes it crystal clear that the height, weight, goal, and restrictions are all related athlete data that should be considered together when generating the meal plan.

While you might not see dramatic improvements with simple prompts, XML tags become increasingly valuable as your prompts grow more complex and include larger amounts of varied content.
