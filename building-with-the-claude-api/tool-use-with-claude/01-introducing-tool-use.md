# Introducing tool use

Course: [Building with the Claude API](https://anthropic.skilljar.com/claude-with-the-anthropic-api) · Module: Tool use with Claude

Tools allow Claude to access information from the outside world, extending its capabilities beyond what it learned during training. By default, Claude only knows information from its training data and can't access current events, real-time data, or external systems. Tool use solves this limitation by creating a structured way for Claude to request and receive fresh information.

## The problem without tools

When users ask Claude for current information, it hits a wall. If someone asks "What's the weather in San Francisco, California?" Claude has to respond with something like "I'm sorry, but I don't have access to up-to-date weather information." This creates a frustrating user experience when people need real-time data.

## How tool use works

Tool use follows a specific back-and-forth pattern between your application and Claude:

1. **Initial request** — You send Claude a question along with instructions on how to get extra data from external sources
2. **Tool request** — Claude analyzes the question, decides it needs additional information, then asks for specific details about what data it needs
3. **Data retrieval** — Your server runs code to fetch the requested information from external APIs or databases
4. **Final response** — You send the retrieved data back to Claude, which generates a complete response using both the original question and the fresh data

## Weather example in practice

When a user asks about current weather, you include instructions in your prompt about how to retrieve weather data. Claude recognizes it needs current information and requests weather data for the specific location. Your server calls a weather API to get real-time conditions and sends that data back to Claude. Finally, Claude combines the fresh weather data with the user's question to provide an accurate, current response.

## Key benefits

- **Real-time information** — Access current data that wasn't available during Claude's training
- **External system integration** — Connect Claude to databases, APIs, and other services
- **Dynamic responses** — Provide answers based on the latest available information
- **Structured interaction** — Claude knows exactly what information it needs and how to ask for it

Tool use transforms Claude from a static knowledge base into a dynamic assistant that can work with live data. This opens up possibilities for building applications that need current information — whether that's weather data, stock prices, database queries, or any other real-time information your users might need.
