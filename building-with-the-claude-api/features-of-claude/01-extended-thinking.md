# Extended thinking

Course: [Building with the Claude API](https://anthropic.skilljar.com/claude-with-the-anthropic-api) · Module: Features of Claude

> Lesson downloads: [001_thinking.ipynb](../.resources/001_thinking.ipynb), [001_thinking_complete.ipynb](../.resources/001_thinking_complete.ipynb)
>
> **Note:** Extended thinking is not compatible with some other features, notably message pre-filling and temperature. See the full list of restrictions at <https://docs.anthropic.com/en/docs/build-with-claude/extended-thinking#feature-compatibility>

Extended thinking is Claude's advanced reasoning feature that gives the model time to work through complex problems before generating a final response. Think of it as Claude's "scratch paper" — you can see the reasoning process that leads to the answer, which helps with transparency and often results in better quality responses.

## How extended thinking works

When extended thinking is enabled, Claude's response changes from a simple text block to a structured response containing both the reasoning process and the final answer.

Key benefits:

- Better reasoning capabilities for complex tasks
- Increased accuracy on difficult problems
- Transparency into Claude's thought process

Important trade-offs:

- Higher costs (you pay for thinking tokens)
- Increased latency (thinking takes time)
- More complex response handling in your code

## When to use extended thinking

The decision is straightforward: use your prompt evaluations. Run your prompts without thinking first, and if the accuracy isn't meeting your requirements after you've already optimized your prompt, then consider enabling extended thinking. It's a tool for when standard prompting isn't quite getting you there.

## Response structure and security

Extended thinking responses include a special signature system for security. The signature is a cryptographic token that ensures you haven't modified the thinking text. This prevents developers from tampering with Claude's reasoning process, which could potentially lead the model in unsafe directions.

## Redacted thinking

Sometimes you'll receive a redacted thinking block instead of readable reasoning text. This happens when Claude's thinking process gets flagged by internal safety systems. The redacted content contains the actual thinking in encrypted form, allowing you to pass the complete message back to Claude in future conversations without losing context.

## Implementation

To enable extended thinking, add two parameters to your chat function:

```python
def chat(
    messages,
    system=None,
    temperature=1.0,
    stop_sequences=[],
    tools=None,
    thinking=False,
    thinking_budget=1024
):
```

The thinking budget sets the maximum tokens Claude can use for reasoning. The minimum value is 1024 tokens, and your `max_tokens` parameter must be greater than your thinking budget.

Add the thinking configuration to your API parameters:

```python
if thinking:
    params["thinking"] = {
        "type": "enabled",
        "budget": thinking_budget
    }
```

Then call it with thinking enabled:

```python
chat(messages, thinking=True)
```

## Testing redacted responses

For testing purposes, you can force Claude to return a redacted thinking block by sending a special trigger string. This helps ensure your application handles redacted responses gracefully without crashing.

Extended thinking is a powerful feature when you need Claude to tackle complex reasoning tasks, but use it judiciously given the cost and latency implications. Start with standard prompting, optimize thoroughly, then add thinking when you need that extra reasoning capability.
