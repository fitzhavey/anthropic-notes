# Building with the Claude API

[Course on Anthropic Academy / Skilljar](https://anthropic.skilljar.com/claude-with-the-anthropic-api)

**Status:** 3 of 85 lessons completed (3%) ◐ In progress

## About this course

This comprehensive video course teaches developers how to integrate Claude AI into applications using the Anthropic API. The curriculum covers fundamental API operations, advanced prompting techniques, tool integration, and architectural patterns for building AI-powered systems. Through hands-on exercises and practical examples, participants will learn to implement conversational AI, retrieval-augmented generation, automated workflows, and leverage Claude's multimodal capabilities for processing text, images, and documents.

## What you'll learn

- Set up and authenticate with the Anthropic API, including API key management and request configuration
- Implement single and multi-turn conversations with proper message formatting and context handling
- Configure system prompts and control model behavior using temperature, response streaming, and structured output formats
- Design and execute prompt evaluation workflows with test dataset generation and automated grading systems
- Apply prompt engineering techniques including XML tag structuring, example-based learning, and clear directive formulation
- Integrate Claude's tool use capabilities to extend functionality with custom tools, batch operations, and web search
- Build retrieval-augmented generation (RAG) systems with text chunking, embeddings, BM25 search, and contextual retrieval
- Utilize Claude's extended features including extended thinking mode, image analysis, PDF processing, and citation generation
- Implement prompt caching strategies to optimize API usage and reduce latency
- Develop Model Context Protocol (MCP) servers and clients for standardized tool and resource integration
- Deploy Anthropic Apps including Claude Code for automated development tasks and Computer Use for UI automation
- Architect agent-based systems with parallelization, chaining, and routing workflows

## Prerequisites

- Proficiency in Python programming
- Basic knowledge of handling JSON data

## Who this course is for

Backend developers building AI-powered APIs and services; full-stack engineers integrating conversational AI into web applications; data engineers implementing document processing and knowledge retrieval systems; DevOps professionals automating workflows with AI assistance; technical architects designing scalable AI-integrated systems; software engineers transitioning to AI/ML application development; and developers working on chatbots, virtual assistants, or content generation tools.

## Curriculum

### Introduction
- Welcome to the course _(video only — no notes)_

### Anthropic overview
- Overview of Claude models _(video only — no notes)_

### Accessing Claude with the API
- [Accessing the API](accessing-claude-with-the-api/01-accessing-the-api.md)
- [Getting an API key](accessing-claude-with-the-api/02-getting-an-api-key.md)
- [Making a request](accessing-claude-with-the-api/03-making-a-request.md)
- [Multi-Turn conversations](accessing-claude-with-the-api/04-multi-turn-conversations.md)
- Chat exercise _(exercise — no notes)_
- [System prompts](accessing-claude-with-the-api/05-system-prompts.md)
- System prompts exercise _(exercise — no notes)_
- [Temperature](accessing-claude-with-the-api/06-temperature.md)
- Course satisfaction survey _(survey — no notes)_
- [Response streaming](accessing-claude-with-the-api/07-response-streaming.md)
- [Structured data](accessing-claude-with-the-api/08-structured-data.md)
- Structured data exercise _(exercise — no notes)_
- [Quiz on accessing Claude with the API](accessing-claude-with-the-api/09-quiz.md)

### Prompt evaluation
- [Prompt evaluation](prompt-evaluation/01-prompt-evaluation.md)
- [A typical eval workflow](prompt-evaluation/02-a-typical-eval-workflow.md)
- [Generating test datasets](prompt-evaluation/03-generating-test-datasets.md)
- [Running the eval](prompt-evaluation/04-running-the-eval.md)
- [Model based grading](prompt-evaluation/05-model-based-grading.md)
- [Code based grading](prompt-evaluation/06-code-based-grading.md)
- Exercise on prompt evals _(exercise — no notes)_
- [Quiz on prompt evaluation](prompt-evaluation/07-quiz.md)

### Prompt engineering techniques
- [Prompt engineering](prompt-engineering-techniques/01-prompt-engineering.md)
- [Being clear and direct](prompt-engineering-techniques/02-being-clear-and-direct.md)
- [Being specific](prompt-engineering-techniques/03-being-specific.md)
- [Structure with XML tags](prompt-engineering-techniques/04-structure-with-xml-tags.md)
- [Providing examples](prompt-engineering-techniques/05-providing-examples.md)
- Exercise on prompting _(exercise — no notes)_
- [Quiz on prompt engineering techniques](prompt-engineering-techniques/06-quiz.md)

### Tool use with Claude
- [Introducing tool use](tool-use-with-claude/01-introducing-tool-use.md)
- [Project overview](tool-use-with-claude/02-project-overview.md)
- [Tool functions](tool-use-with-claude/03-tool-functions.md)
- [Tool schemas](tool-use-with-claude/04-tool-schemas.md)
- [Handling message blocks](tool-use-with-claude/05-handling-message-blocks.md)
- [Sending tool results](tool-use-with-claude/06-sending-tool-results.md)
- [Multi-turn conversations with tools](tool-use-with-claude/07-multi-turn-conversations-with-tools.md)
- [Implementing multiple turns](tool-use-with-claude/08-implementing-multiple-turns.md)
- [Using multiple tools](tool-use-with-claude/09-using-multiple-tools.md)
- [Fine grained tool calling](tool-use-with-claude/10-fine-grained-tool-calling.md)
- [The text edit tool](tool-use-with-claude/11-the-text-edit-tool.md)
- [The web search tool](tool-use-with-claude/12-the-web-search-tool.md)
- [Quiz on tool use with Claude](tool-use-with-claude/13-quiz.md)

### RAG and Agentic Search
- [Introducing Retrieval Augmented Generation](rag-and-agentic-search/01-introducing-retrieval-augmented-generation.md)
- [Text chunking strategies](rag-and-agentic-search/02-text-chunking-strategies.md)
- [Text embeddings](rag-and-agentic-search/03-text-embeddings.md)
- [The full RAG flow](rag-and-agentic-search/04-the-full-rag-flow.md)
- [Implementing the RAG flow](rag-and-agentic-search/05-implementing-the-rag-flow.md)
- [BM25 lexical search](rag-and-agentic-search/06-bm25-lexical-search.md)
- [A Multi-Index RAG pipeline](rag-and-agentic-search/07-a-multi-index-rag-pipeline.md)

### Features of Claude
- [Extended thinking](features-of-claude/01-extended-thinking.md)
- [Image support](features-of-claude/02-image-support.md)
- [PDF support](features-of-claude/03-pdf-support.md)
- [Citations](features-of-claude/04-citations.md)
- [Prompt caching](features-of-claude/05-prompt-caching.md)
- [Rules of prompt caching](features-of-claude/06-rules-of-prompt-caching.md)
- [Prompt caching in action](features-of-claude/07-prompt-caching-in-action.md)
- [Code execution and the Files API](features-of-claude/08-code-execution-and-the-files-api.md)
- [Quiz on features of Claude](features-of-claude/09-quiz.md)

### Model Context Protocol
- Introducing MCP
- MCP clients
- Project setup
- Defining tools with MCP
- The server inspector
- Implementing a client
- Defining resources
- Accessing resources
- Defining prompts
- Prompts in the client
- MCP review
- Quiz on Model Context Protocol

### Anthropic apps — Claude Code and computer use
- Anthropic apps
- Claude Code setup
- Claude Code in action
- Enhancements with MCP servers

### Agents and workflows
- Agents and workflows
- Parallelization workflows
- Chaining workflows
- Routing workflows
- Agents and tools
- Environment inspection
- Workflows vs agents
- Quiz on Agents and Workflows

### Final assessment
- Final Assessment

### Wrapping up!
- Course Wrap Up
