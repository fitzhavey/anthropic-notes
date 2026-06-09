# Tool functions

Course: [Building with the Claude API](https://anthropic.skilljar.com/claude-with-the-anthropic-api) · Module: Tool use with Claude

> Lesson download: [001_tools.ipynb](../.resources/001_tools.ipynb)

When building AI applications with Claude, you'll often need to give it access to real-time information or the ability to perform actions. This is where tool functions come in — they're Python functions that Claude can call when it needs additional data to help users.

The three essential tools for this project: getting the current date/time, adding duration to dates, and setting reminders. We start with the first.

## What are tool functions?

A tool function is a plain Python function that gets executed automatically when Claude decides it needs extra information to help a user. For example, if someone asks "What time is it?", Claude would call your date/time tool to get the current time.

## Best practices for tool functions

- **Use descriptive names** — Both your function name and parameter names should clearly indicate their purpose
- **Validate inputs** — Check that required parameters aren't empty or invalid, and raise errors when they are
- **Provide meaningful error messages** — Claude can see error messages and might retry the function call with corrected parameters

Validation is particularly important because Claude learns from errors. If you raise a clear error like "Location cannot be empty", Claude might try calling the function again with a proper location value.

## Building your first tool function

A function to get the current date and time, accepting a date format parameter so Claude can request the time in different formats:

```python
def get_current_datetime(date_format="%Y-%m-%d %H:%M:%S"):
    if not date_format:
        raise ValueError("date_format cannot be empty")
    return datetime.now().strftime(date_format)
```

This uses Python's `datetime` module to get the current time and format it according to the provided format string. The default format gives year-month-day hour:minute:second.

Test it with different formats:

```python
# Default format: "2024-01-15 14:30:25"
get_current_datetime()

# Just hour and minute: "14:30"
get_current_datetime("%H:%M")
```

The validation check ensures Claude can't pass an empty string for the date format. While this specific error is unlikely, it demonstrates the pattern of validating inputs and providing helpful error messages that Claude can learn from.

## Next steps

Creating the function is just the first step. Next, you'll write a JSON schema that describes the function to Claude, then integrate it into your chat system. This tool function approach gives Claude powerful capabilities while keeping your code organized and maintainable.
