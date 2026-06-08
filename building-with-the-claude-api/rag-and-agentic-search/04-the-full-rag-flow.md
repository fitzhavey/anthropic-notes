# The full RAG flow

Course: [Building with the Claude API](https://anthropic.skilljar.com/claude-with-the-anthropic-api) · Module: RAG and Agentic Search

Now that we've covered the basics of RAG, text chunking, and embeddings, let's walk through the complete RAG pipeline step by step.

## Step 1: Chunk your source text

Take the source document and break it into manageable chunks. For this example, two simple sections:

- **Section 1: Medical Research** — "This year saw significant strides in our understanding of XDR-47, a 'bug' we have not seen before."
- **Section 2: Software Engineering** — "This division dedicated significant effort to studying various infection vectors in our distributed systems"

## Step 2: Generate embeddings

Convert each text chunk into numerical embeddings. To make this easier to understand, imagine a perfect embedding model that always returns exactly two numbers and we know what each represents:

- The first number represents how much the text talks about the medical field
- The second number represents how much the text talks about software engineering

For the medical research section, we might get `[0.97, 0.34]` — very medical-focused but with some software elements due to the word "bug". For the software engineering section, `[0.30, 0.97]` — heavily software-focused but with medical undertones from "infection vectors".

### Normalization

The embedding API typically performs a normalization step that scales each vector to have a magnitude of 1.0. This is handled automatically, giving normalized vectors like `[0.944, 0.331]` and `[0.295, 0.955]`. You can visualize these on a unit circle, where each point represents one chunk.

## Step 3: Store in vector database

Store these embeddings in a vector database — a specialized database optimized for storing, comparing, and searching through long lists of numbers like our embeddings.

At this point, we pause. All the work so far has been preprocessing that happens ahead of time. Now we wait for a user to submit a query.

## Step 4: Process user query

When a user asks a question like "I'm curious about the company. In particular, what did the software engineering dept do this year?", we run their query through the same embedding model. This query gets embedded as something like `[0.1, 0.89]` — low medical score, high software engineering score. After normalization, `[0.112, 0.993]`.

## Step 5: Find similar embeddings

We send the user's query embedding to the vector database and ask it to find the most similar stored embeddings. The database returns the software engineering section because it's the closest match.

### How similarity works: cosine similarity

The vector database uses cosine similarity to determine which embeddings are most similar. This measures the cosine of the angle between two vectors:

- Results range from -1 to 1
- Values close to 1 mean high similarity
- Values close to -1 mean very different
- 0 means perpendicular (no relationship)

In this example, the cosine similarity between the user query and the software engineering chunk is 0.983 — very high. The similarity with the medical research chunk is only 0.398 — much lower.

### Cosine distance

You'll often see "cosine distance" in vector database documentation. This is simply `(1 - cosine similarity)`:

- Values close to 0 mean high similarity
- Larger values mean less similarity

This adjustment makes the numbers easier to interpret in many contexts.

## Step 6: Create the final prompt

Take the user's question and the most relevant text chunk found, combine them into a prompt, and send it to Claude:

```
Answer the user's question about the financial document.

<user_question>
How many bugs did engineers fix this year?
</user_question>

<report>
## Section 2: Software Engineering
This division dedicated significant effort to studying various infection vectors in our distributed systems
</report>
```

And that's the complete RAG pipeline! The system successfully retrieved the most relevant information based on semantic similarity and provided it as context for generating an accurate response.
