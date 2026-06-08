# Running the eval

Course: [Building with the Claude API](https://anthropic.skilljar.com/claude-with-the-anthropic-api) · Module: Prompt evaluation

Now that we have our evaluation dataset ready, it's time to build the core evaluation pipeline. This involves taking each test case, merging it with our prompt, feeding it to Claude, and then grading the results.

The process follows a clear workflow: take the dataset of test cases, combine each with the prompt template, send it to Claude for processing, then evaluate the output using a grader system.

## Building the core functions

The evaluation pipeline consists of three main functions, each with a specific responsibility.

### The `run_prompt` function

Takes a test case and merges it with the prompt template:

```python
def run_prompt(test_case):
    """Merges the prompt and test case input, then returns the result"""
    prompt = f"""
Please solve the following task:

{test_case["task"]}
"""

    messages = []
    add_user_message(messages, prompt)
    output = chat(messages)
    return output
```

The prompt is kept extremely simple for now — no formatting instructions, so Claude will likely return more verbose output than we need. We'll refine this later.

### The `run_test_case` function

Orchestrates running a single test case and grading the result:

```python
def run_test_case(test_case):
    """Calls run_prompt, then grades the result"""
    output = run_prompt(test_case)

    # TODO - Grading
    score = 10

    return {
        "output": output,
        "test_case": test_case,
        "score": score
    }
```

For now, a hardcoded score of 10. The grading logic is where we'll spend significant time in upcoming sections, but this placeholder lets us test the overall pipeline.

### The `run_eval` function

Coordinates the entire evaluation process:

```python
def run_eval(dataset):
    """Loads the dataset and calls run_test_case with each case"""
    results = []

    for test_case in dataset:
        result = run_test_case(test_case)
        results.append(result)

    return results
```

This processes every test case in the dataset and collects all results into a single list.

## Running the evaluation

```python
with open("dataset.json", "r") as f:
    dataset = json.load(f)

results = run_eval(dataset)
```

The first time you run this, expect it to take some time — even with Claude Haiku, it can take around 30 seconds to process a full dataset. Optimization techniques come later.

## Examining the results

The evaluation returns a structured JSON array where each object represents one test case result:

```python
print(json.dumps(results, indent=2))
```

Each result contains three key pieces of information:

- **`output`** — The complete response from Claude
- **`test_case`** — The original test case that was processed
- **`score`** — The evaluation score (currently hardcoded)

Claude generates quite verbose responses since we haven't provided specific formatting instructions yet. This is exactly the kind of issue we'll address as we refine our prompts.

## What we've accomplished

We've successfully built the core evaluation pipeline: take the dataset, process it through Claude, and collect structured results. The major missing piece is the grading system — that hardcoded score of 10 needs to be replaced with actual evaluation logic.

This pipeline is the foundation of most AI evaluation systems. While it may seem simple, you've just built the majority of what an eval pipeline actually does. The complexity comes in the details — better prompts, sophisticated grading, and performance optimizations. Next, we'll dive into graders, which transform hardcoded scores into meaningful evaluations of Claude's performance.
