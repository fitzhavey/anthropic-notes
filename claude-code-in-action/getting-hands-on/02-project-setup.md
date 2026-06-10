# Project setup

Course: [Claude Code in Action](https://anthropic.skilljar.com/claude-code-in-action) · Section: Getting hands on

> Lesson download: [uigen](../.resources/uigen)

Working with Claude Code is more interesting if you have a project to work with. The course provides a small project to explore — the same UI generation app shown in a previous video. Note: you don't have to run this project; you can follow along with the rest of the course using your own codebase if you wish.

## Setup

1. Ensure you have Node.js installed locally
2. Download the `uigen.zip` file attached to the lecture and extract it
3. In the project directory, run `npm run setup` to install dependencies and set up a local SQLite database
4. **Optional** — The project uses Claude through the Anthropic API to generate UI components. To fully test the app, provide an API key (otherwise it generates static fake code):
   - Get an Anthropic API key at <https://console.anthropic.com/>
   - Place your API key in the `.env` file, replacing the literal text `your-api-key-here` with your key
5. Start the project by running `npm run dev`
