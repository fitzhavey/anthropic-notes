# Multi-Turn conversations

Course: [Building with the Claude API](https://anthropic.skilljar.com/claude-with-the-anthropic-api) · Module: Accessing Claude with the API

A crucial concept when working with the Anthropic API: Claude doesn't store any of your conversation history. Each request is completely independent, with no memory of previous exchanges. If you want a multi-turn conversation where Claude remembers earlier context, you need to handle the conversation state yourself.

## The problem with stateless conversations

Say you ask Claude "What is quantum computing?" and get a good response. Then you follow up with "Write another sentence" — Claude has no idea what you're referring to. It will write a sentence about something random because it has no memory of the earlier discussion.

## How multi-turn conversations work

To maintain conversation context, you need to do two things:

1. Manually maintain a list of all messages in your code
2. Send the complete message history with every request

The flow that works:

1. Send your initial user message to Claude
2. Take Claude's response and add it to your message list as an assistant message
3. Add your follow-up question as another user message
4. Send the entire conversation history to Claude

## Building helper functions

```python
def add_user_message(messages, text):
    user_message = {"role": "user", "content": text}
    messages.append(user_message)

def add_assistant_message(messages, text):
    assistant_message = {"role": "assistant", "content": text}
    messages.append(assistant_message)

def chat(messages):
    message = client.messages.create(
        model=model,
        max_tokens=1000,
        messages=messages,
    )
    return message.content[0].text
```

## Putting it all together

```python
# Start with an empty message list
messages = []

# Add the initial user question
add_user_message(messages, "Define quantum computing in one sentence")

# Get Claude's response
answer = chat(messages)

# Add Claude's response to the conversation history
add_assistant_message(messages, answer)

# Add a follow-up question
add_user_message(messages, "Write another sentence")

# Get the follow-up response with full context
final_answer = chat(messages)
```

Now Claude understands that "Write another sentence" refers to expanding on the quantum computing definition, because you've provided the complete conversation context.

These helper functions are useful throughout your work with Claude, making it much easier to build applications that maintain meaningful conversations over multiple exchanges.
