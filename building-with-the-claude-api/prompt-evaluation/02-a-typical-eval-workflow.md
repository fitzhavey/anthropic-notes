# A typical eval workflow

Course: [Building with the Claude API](https://anthropic.skilljar.com/claude-with-the-anthropic-api) · Module: Prompt evaluation

A typical prompt evaluation workflow follows five key steps that help you systematically improve your prompts through objective measurement. There are many ways to assemble these workflows and various open source and paid tools available, but understanding the core process helps you start small and scale up as needed.

## Step 1: Draft a prompt

Start by writing an initial prompt that you want to improve. This serves as your baseline:

```python
prompt = f"""
Please answer the user's question:

{question}
"""
```

## Step 2: Create an eval dataset

Your evaluation dataset contains sample inputs representing the types of questions or requests your prompt will handle in production. These get interpolated into your prompt template. For this example:

- "What's 2+2?"
- "How do I make oatmeal?"
- "How far away is the Moon?"

In real-world evaluations, you might have tens, hundreds, or even thousands of records. You can assemble these datasets by hand or use Claude to generate them for you.

## Step 3: Feed through Claude

Take each question from your dataset, merge it with your prompt template to create complete prompts, then send each to Claude. For example, the first question becomes:

```
Please answer the user's question:
What's 2+2?
```

Claude might respond with "2 + 2 = 4", provide oatmeal cooking instructions, and give the distance to the Moon for the three questions respectively.

## Step 4: Feed through a grader

The grader evaluates the quality of Claude's responses by examining both the original question and Claude's answer. This provides objective scoring, typically on a scale from 1 to 10, where 10 is a perfect answer.

In our example, the grader might assign:

- Math question: 10 (perfect answer)
- Oatmeal question: 4 (needs improvement)
- Moon question: 9 (very good answer)

The average score gives you an objective measurement: (10 + 4 + 9) ÷ 3 = 7.66.

## Step 5: Change prompt and repeat

With a baseline score, you can modify your prompt and run the whole process again to see if it improves performance. For example, adding more guidance:

```python
prompt = f"""
Please answer the user's question:

{question}

Answer the question with ample detail
"""
```

After running this improved prompt through the same evaluation, you might get a higher average score of 8.7, indicating the additional instruction helped.

## Prompt scoring

The key benefit of this workflow is getting objective measurements of prompt performance. You can compare different prompt versions numerically, use the version with the best score, and continue iterating to find even better approaches. This systematic approach removes guesswork from prompt engineering and gives you confidence that your changes are actually improvements rather than just different variations.
