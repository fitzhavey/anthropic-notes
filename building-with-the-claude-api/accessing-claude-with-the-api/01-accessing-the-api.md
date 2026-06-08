# Accessing the API

Course: [Building with the Claude API](https://anthropic.skilljar.com/claude-with-the-anthropic-api) · Module: Accessing Claude with the API

When building applications with Claude, understanding the complete request lifecycle helps you make better architectural decisions and debug issues more effectively. This lesson walks through what happens from the moment a user clicks "send" in your chat interface to when Claude's response appears on screen.

## The five-step request flow

Every interaction with Claude follows a predictable pattern with five distinct phases:

1. Request to your server
2. Request to the Anthropic API
3. Model processing
4. Response to your server
5. Response to the client

## Why you need a server

You should never make requests to the Anthropic API directly from client-side code:

- API requests require a secret API key for authentication
- Exposing this key in client code creates a serious security vulnerability
- Anyone could extract the key and make unauthorized requests

Instead, your web or mobile app sends requests to your own server, which then communicates with the Anthropic API using the securely stored key.

## Making API requests

When your server contacts the Anthropic API, you can use either an official SDK or make plain HTTP requests. Anthropic provides SDKs for Python, TypeScript, JavaScript, Go, and Ruby.

Every request must include these essential fields:

- **API Key** — Identifies your request to Anthropic
- **Model** — Name of the model to use (like `claude-3-sonnet`)
- **Messages** — List containing the user's input text
- **Max Tokens** — Limit for how many tokens Claude can generate

## Inside Claude's processing

Once Anthropic receives your request, Claude processes it through four main stages: tokenization, embedding, contextualization, and generation.

### Tokenization

Claude first breaks your input text into smaller chunks called tokens. These can be whole words, parts of words, spaces, or symbols. For simplicity, think of each word as one token.

### Embedding

Each token gets converted into an embedding — a long list of numbers that represents all possible meanings of that word. Think of embeddings as numerical definitions that capture semantic relationships.

Words often have multiple meanings. For example, "quantum" could refer to a discrete unit of physical quantity (physics), quantum mechanics concepts, something extremely small or subatomic, or quantum computing applications.

### Contextualization

Claude refines each embedding based on surrounding words to determine the most likely meaning in context. This process adjusts the numerical representations to highlight the appropriate definition.

### Generation

The contextualized embeddings pass through an output layer that calculates probabilities for each possible next word. Claude doesn't always pick the highest probability word — it uses a mix of probability and controlled randomness to create natural, varied responses. After selecting each word, Claude adds it to the sequence and repeats the entire process for the next word.

## When Claude stops generating

After each token, Claude checks several conditions to decide whether to continue:

- **Max tokens reached** — Has it hit the limit you specified?
- **Natural ending** — Did it generate an end-of-sequence token?
- **Stop sequence** — Did it encounter a predefined stop phrase?

## The API response

When generation completes, the API sends back a structured response containing:

- **Message** — The generated text
- **Usage** — Count of input and output tokens
- **Stop Reason** — Why generation ended

Your server receives this response and forwards the generated text back to your client application, where it appears in the user interface.

## Key takeaways

Understanding this flow helps you:

- Design secure architectures that protect your API keys
- Set appropriate token limits for your use case
- Handle different stop reasons in your application logic
- Debug issues by understanding where they might occur in the pipeline

The goal isn't to memorize every detail — it's to familiarize yourself with the terminology and overall process you'll encounter when working with Claude's API.
