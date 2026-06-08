# System prompts

Course: [Building with the Claude API](https://anthropic.skilljar.com/claude-with-the-anthropic-api) · Module: Accessing Claude with the API

System prompts are a powerful way to customize how Claude responds to user input. Instead of generic answers, you can shape Claude's tone, style, and approach to match your specific use case.

## Why system prompts matter

Consider building a math tutor chatbot. When a student asks "How do I solve 5x + 2 = 3 for x?", you want Claude to act like a real tutor, not just give the answer. A good math tutor should:

- Initially give hints rather than complete solutions
- Patiently walk students through problems step by step
- Show solutions for similar problems as examples

You don't want Claude to immediately give direct answers, or tell students to just use a calculator.

## How system prompts work

System prompts provide Claude with guidance on how to respond. You define them as plain strings and pass them into the create function call. Key benefits:

- They provide Claude guidance on how to respond
- Claude will try to respond in the same way someone in the specified role would
- They help keep Claude on task

```python
system_prompt = """
You are a patient math tutor.
Do not directly answer a student's questions.
Guide them to a solution step by step.
"""

client.messages.create(
    model=model,
    messages=messages,
    max_tokens=1000,
    system=system_prompt
)
```

## Seeing the difference

Without a system prompt, Claude gives a complete step-by-step solution immediately. This might be helpful, but it doesn't encourage the student to think through the problem themselves.

With the math tutor system prompt, Claude's response changes dramatically. Instead of the full solution, Claude asks guiding questions like "What do you think would be a good first step to isolate x? Consider what operation we might need to perform on both sides to start moving terms around."

## Building a flexible chat function

Rather than hard-coding system prompts, make your chat function reusable by accepting them as a parameter:

```python
def chat(messages, system=None):
    params = {
        "model": model,
        "max_tokens": 1000,
        "messages": messages,
    }

    if system:
        params["system"] = system

    message = client.messages.create(**params)
    return message.content[0].text
```

This handles an important detail: Claude's API doesn't accept `system=None`, so you only include the `system` parameter when it's provided.

```python
# Without system prompt
answer = chat(messages)

# With system prompt
system = """
You are a patient math tutor.
Do not directly answer a student's questions.
Guide them to a solution step by step.
"""
answer = chat(messages, system=system)
```

System prompts are essential for creating AI applications that behave consistently and appropriately for their intended purpose. They transform generic AI responses into specialized, role-appropriate interactions.
