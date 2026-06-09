# Using multiple tools

Course: [Building with the Claude API](https://anthropic.skilljar.com/claude-with-the-anthropic-api) · Module: Tool use with Claude

> Lesson download: [001_tools_009.ipynb](../.resources/001_tools_009.ipynb)

Adding multiple tools to your Claude implementation becomes straightforward once you have the core tool-handling infrastructure in place. This follows a simple pattern.

## The tools we're adding

Three capabilities for the reminder system:

- **Get current date time** — Claude needs to know the current date and time
- **Add duration to date time** — Claude isn't perfect with date-time addition
- **Set a reminder** — A way to set a reminder

Most of the implementation work is already done. The `add_duration_to_datetime` and `set_reminder` functions are provided, along with their corresponding schemas.

## Adding tools to the conversation

Update `run_conversation` to include the new tool schemas in the tools list:

```python
response = chat(messages, tools=[
    get_current_datetime_schema,
    add_duration_to_datetime_schema,
    set_reminder_schema
])
```

This tells Claude about all three available tools it can use during the conversation.

## Updating the tool router

Modify `run_tool` to handle the new tool calls by adding `elif` cases for each:

```python
def run_tool(tool_name, tool_input):
    if tool_name == "get_current_datetime":
        return get_current_datetime(**tool_input)
    elif tool_name == "add_duration_to_datetime":
        return add_duration_to_datetime(**tool_input)
    elif tool_name == "set_reminder":
        return set_reminder(**tool_input)
```

The pattern is simple: check the tool name, call the corresponding function with the provided input, and return the result.

## Testing multiple tool usage

Try a request that requires multiple tools: "Set a reminder for my doctors appointment. Its 177 days after Jan 1st, 2050." This forces Claude to:

1. Calculate the date (using `add_duration_to_datetime`)
2. Set the reminder (using `set_reminder`)

Claude handles this by first explaining what it needs to do, then making the appropriate tool calls in sequence — calculating June 27, 2050 as the target date, then setting the reminder for that date.

## Understanding the message flow

When you examine the conversation history, you'll see the complete message structure:

- User message with the request
- Assistant message containing both text and tool use blocks
- Tool result messages
- Follow-up assistant messages

This demonstrates how Claude can include multiple blocks in a single message — combining explanatory text with tool usage requests.

## The simple pattern for adding tools

Once you have the core tool infrastructure, adding new tools follows this pattern:

1. Create the tool function implementation
2. Define the tool schema
3. Add the schema to the tools list in `run_conversation`
4. Add a case for the tool in `run_tool`

This modular approach makes it easy to expand your AI assistant's capabilities without restructuring existing code. Each new tool integrates seamlessly with the existing conversation flow and tool-handling logic.
