# Prompt engineering

Course: [Building with the Claude API](https://anthropic.skilljar.com/claude-with-the-anthropic-api) · Module: Prompt engineering techniques

> Lesson download: `[001_prompting.ipynb](../notebooks/001_prompting.ipynb)`, `[002_prompting_completed.ipynb](../notebooks/002_prompting_completed.ipynb)`

Prompt engineering is about taking a prompt you've written and improving it to get more reliable, higher-quality outputs. This process involves iterative refinement — starting with a basic prompt, evaluating its performance, then systematically applying engineering techniques to improve it.

## The iterative improvement process

1. **Set a goal** — Define what you want your prompt to accomplish
2. **Write an initial prompt** — Create a basic first attempt
3. **Evaluate the prompt** — Test it against your criteria
4. **Apply prompt engineering techniques** — Use specific methods to improve performance
5. **Re-evaluate** — Verify that your changes actually improved the results

Repeat the last two steps until you're satisfied with performance. Each iteration should show measurable improvement in your evaluation scores.

## Setting up your evaluation pipeline

The practical example: a prompt that generates one-day meal plans for athletes. It needs to take into account an athlete's height, weight, goals, and dietary restrictions, then produce a comprehensive meal plan.

The setup uses a `PromptEvaluator` class that handles dataset generation and model grading. Control concurrency with `max_concurrent_tasks`:

```python
evaluator = PromptEvaluator(max_concurrent_tasks=5)
```

Start with a low concurrency value (like 3) to avoid rate limit errors. Increase it if your API quota allows faster processing.

## Generating test data

```python
dataset = evaluator.generate_dataset(
    task_description="Write a compact, concise 1 day meal plan for a single athlete",
    prompt_inputs_spec={
        "height": "Athlete's height in cm",
        "weight": "Athlete's weight in kg",
        "goal": "Goal of the athlete",
        "restrictions": "Dietary restrictions of the athlete"
    },
    output_file="dataset.json",
    num_cases=3
)
```

Keep the number of test cases low (2–3) during development to speed up your iteration cycle. Increase this for final validation.

## Writing your initial prompt

Start with a simple, naive prompt to establish a baseline:

```python
def run_prompt(prompt_inputs):
    prompt = f"""
What should this person eat?

- Height: {prompt_inputs["height"]}
- Weight: {prompt_inputs["weight"]}
- Goal: {prompt_inputs["goal"]}
- Dietary restrictions: {prompt_inputs["restrictions"]}
"""

    messages = []
    add_user_message(messages, prompt)
    return chat(messages)
```

This basic prompt will likely produce poor results, but it gives you a starting point to measure improvement against.

## Adding evaluation criteria

When running your evaluation, you can specify additional criteria the grading model should consider:

```python
results = evaluator.run_evaluation(
    run_prompt_function=run_prompt,
    dataset_file="dataset.json",
    extra_criteria="""
The output should include:
- Daily caloric total
- Macronutrient breakdown
- Meals with exact foods, portions, and timing
"""
)
```

This helps ensure your prompt is evaluated against the specific requirements that matter for your use case.

## Analyzing results

After running an evaluation, you'll get both a numerical score and a detailed HTML report showing exactly how each test case performed, including the model's reasoning for each score.

Don't be discouraged by low initial scores — a score of 2.3 out of 10 is typical for a first attempt. The goal is consistent improvement as you apply engineering techniques. The detailed report helps you understand exactly where your prompt is failing and what improvements are needed.

## Next steps

With your baseline established, you're ready to start applying specific prompt engineering techniques. Each technique should result in measurable improvement in your evaluation scores. The key is to make one change at a time, evaluate the impact, and build on what works — this systematic approach ensures you understand which techniques provide the most value for your specific use case.
