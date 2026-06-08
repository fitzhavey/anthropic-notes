# Temperature

Course: [Building with the Claude API](https://anthropic.skilljar.com/claude-with-the-anthropic-api) · Module: Accessing Claude with the API

Temperature is a parameter that controls how predictable or creative Claude's responses will be. Understanding how to use it effectively can dramatically improve your AI applications.

## How Claude generates text

When you send Claude a prompt like "What do you think?", it goes through three key steps:

1. **Tokenization** — Breaking your input into smaller chunks
2. **Prediction** — Calculating probabilities for possible next words
3. **Sampling** — Choosing a token based on those probabilities

For example, Claude might assign a 30% probability to "about", 20% to "would", 10% to "of", and so on. The model selects one token and repeats the process to build complete sentences.

## What temperature does

Temperature is a decimal value between 0 and 1 that directly influences these selection probabilities — like adjusting the "creativity dial" on Claude's responses.

- **Low temperatures (near 0):** Claude becomes very deterministic — it almost always picks the highest probability token.
- **High temperatures (near 1):** Claude distributes probability more evenly across options, leading to more varied and creative outputs.

At temperature 0.0, "about" might get 100% probability — completely deterministic. At temperature 1.0, probabilities spread more evenly across all possible tokens, introducing randomness and creativity.

## Choosing the right temperature

**Low (0.0 – 0.3)** — factual responses, coding assistance, data extraction, content moderation.

**Medium (0.4 – 0.7)** — summarization, educational content, problem-solving, creative writing with constraints.

**High (0.8 – 1.0)** — brainstorming, creative writing, marketing content, joke generation.

## Implementing temperature in code

```python
def chat(messages, system=None, temperature=1.0):
    params = {
        "model": model,
        "max_tokens": 1000,
        "messages": messages,
        "temperature": temperature
    }

    if system:
        params["system"] = system

    message = client.messages.create(**params)
    return message.content[0].text
```

The key changes are adding `temperature=1.0` as a parameter and including `"temperature": temperature` in the params dictionary.

## Testing temperature effects

```python
# Low temperature - more predictable
answer = chat(messages, temperature=0.0)

# High temperature - more creative
answer = chat(messages, temperature=1.0)
```

At temperature 0.0, you might consistently get responses like "A time-traveling archaeologist must prevent ancient artifacts from being stolen." At temperature 1.0, you'll see much more variety in themes, characters, and plot elements.

## Key takeaways

Temperature doesn't guarantee different outputs — it just changes the probability of getting them. Even at high temperatures, Claude might occasionally produce similar responses. Match your temperature choice to your use case:

- Need consistent, factual responses? Use low temperature.
- Want creative brainstorming? Dial up the temperature.
- Somewhere in between? Medium temperatures work well for most general tasks.
