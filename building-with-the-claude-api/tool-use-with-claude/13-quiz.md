# Quiz on Tool use with Claude

Course: [Building with the Claude API](https://anthropic.skilljar.com/claude-with-the-anthropic-api) · Module: Tool use with Claude

Correct answers are marked **✓**.

**1. How can you tell if Claude wants to make another tool call in a conversation?**
- Check if the response contains the word "tool"
- Check if the response is longer than usual
- **Look at the stop_reason field for "tool_use" ✓**
- Count the number of message blocks

**2. When Claude uses a tool, what type of message structure does it return?**
- **Multi-block messages with text and tool use blocks ✓**
- Simple text-only responses
- JSON data without any text
- Error messages only

**3. What is the main purpose of a JSON schema when working with Claude tools?**
- To format the final response for users
- **To tell Claude what arguments your function expects and how to use it ✓**
- To store the results of tool function calls
- To encrypt data between Claude and your server

**4. What problem does the batch tool solve?**
- It makes tools run faster
- It translates tool results into different languages
- **It reduces the number of back-and-forth communications when multiple tools are needed ✓**
- It automatically fixes errors in tool responses

**5. What is the correct sequence of steps in the tool use workflow?**
- **Initial Request → Tool Request → Data Retrieval → Final Response ✓**
- Tool Request → Initial Request → Final Response → Data Retrieval
- Final Response → Initial Request → Tool Request → Data Retrieval
- Data Retrieval → Tool Request → Initial Request → Final Response

**6. Claude can only access information from its training data by default. What allows Claude to get current, real-time information?**
- Making educated guesses based on patterns
- Searching through its training data more carefully
- Asking the user to provide more details
- **Using tools to access external information ✓**

**7. What makes Claude's built-in text editor and web search tools different from custom tools?**
- **Claude provides the schema, but you may still need to implement some functionality ✓**
- They require special API keys
- They only work with specific file types
- They cost more to use
