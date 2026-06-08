# Generating test datasets

Course: [Building with the Claude API](https://anthropic.skilljar.com/claude-with-the-anthropic-api) · Module: Prompt evaluation

Building a custom prompt evaluation workflow starts with creating a solid prompt and then generating test data to see how well it performs. This walks through setting up an evaluation system for a prompt that helps users write AWS-specific code.

## Setting up the goal

Our prompt needs to assist users in writing three specific types of output for AWS use cases: Python code, JSON configuration files, and regular expressions. The key requirement: when a user requests help, we return clean output in one of these formats without any extra explanations, headers, or footers.

Starting prompt (version 1):

```python
prompt = f"""
Please provide a solution to the following task:
{task}
"""
```

## Creating an evaluation dataset

An evaluation dataset contains inputs we'll feed into our prompt. For each combination of prompt and input, we run the prompt and analyze the results. Our dataset will be an array of JSON objects, where each object contains a `task` property describing what we want Claude to accomplish. We can create this by hand or generate it automatically using Claude.

Since we're generating test data, this is a perfect opportunity to use a faster model like Haiku instead of the full Claude model.

## Generating test data with code

First, the helper functions for working with Claude:

```python
def add_user_message(messages, text):
    user_message = {"role": "user", "content": text}
    messages.append(user_message)

def add_assistant_message(messages, text):
    assistant_message = {"role": "assistant", "content": text}
    messages.append(assistant_message)

def chat(messages, system=None, temperature=1.0, stop_sequences=[]):
    params = {
        "model": model,
        "max_tokens": 1000,
        "messages": messages,
        "temperature": temperature
    }
    if system:
        params["system"] = system
    if stop_sequences:
        params["stop_sequences"] = stop_sequences

    response = client.messages.create(**params)
    return response.content[0].text
```

Then the dataset generation function:

````python
def generate_dataset():
    prompt = """
Generate an evaluation dataset for a prompt evaluation. The dataset will be used to evaluate prompts that generate Python, JSON, or Regex specifically for AWS-related tasks. Generate an array of JSON objects, each representing task that requires Python, JSON, or a Regex to complete.

Example output:
```json
[
  {
    "task": "Description of task",
  },
  ...additional
]
```

* Focus on tasks that can be solved by writing a single Python function, a single JSON object, or a single regex
* Focus on tasks that do not require writing much code

Please generate 3 objects.
"""
````

To properly parse the JSON response, use prefilling and stop sequences:

````python
    messages = []
    add_user_message(messages, prompt)
    add_assistant_message(messages, "```json")
    text = chat(messages, stop_sequences=["```"])
    return json.loads(text)
````

## Testing the dataset generation

```python
dataset = generate_dataset()
print(dataset)
```

This should return three different test cases covering our target outputs — Python functions, JSON configurations, and regular expressions for AWS-specific tasks.

## Saving the dataset

Save it to a file so you can easily load it later during evaluation:

```python
with open('dataset.json', 'w') as f:
    json.dump(dataset, f, indent=2)
```

This creates a `dataset.json` file in the same directory as your notebook, containing your list of tasks ready for prompt evaluation. With this foundation, you have a systematic way to generate test data for evaluating how well your prompts perform across different types of AWS-related coding tasks.
