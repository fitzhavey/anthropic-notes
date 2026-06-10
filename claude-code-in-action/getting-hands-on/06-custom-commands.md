# Custom commands

Course: [Claude Code in Action](https://anthropic.skilljar.com/claude-code-in-action) · Section: Getting hands on

Claude Code comes with built-in commands you access by typing a forward slash, but you can also create your own custom commands to automate repetitive tasks you run frequently.

## Creating custom commands

Set up a specific folder structure in your project:

1. Find the `.claude` folder in your project directory
2. Create a new directory called `commands` inside it
3. Create a markdown file with your desired command name (like `audit.md`)

The filename becomes your command name — so `audit.md` creates the `/audit` command. After creating the file, Claude Code picks it up automatically; no restart needed.

## Example: audit command

A custom `/audit` command that audits project dependencies for vulnerabilities might:

1. Run `npm audit` to find vulnerable installed packages
2. Run `npm audit fix` to apply updates
3. Run tests to verify the updates didn't break anything

## Commands with arguments

Custom commands can accept arguments using the `$ARGUMENTS` placeholder, making them more flexible and reusable. For example, a `write_tests.md` command might contain:

```
Write comprehensive tests for: $ARGUMENTS

Testing conventions:
* Use Vitest with React Testing Library
* Place test files in a __tests__ directory in the same folder as the source file
* Name test files as [filename].test.ts(x)
* Use @/ prefix for imports

Coverage:
* Test happy paths
* Test edge cases
* Test error states
```

You can then run this command with a file path:

```
/write_tests the use-auth.ts file in the hooks directory
```

The arguments don't have to be file paths — they can be any string you want to pass to give Claude context and direction.

## Key benefits

- **Automation** — Turn repetitive workflows into single commands
- **Consistency** — Ensure the same steps are followed every time
- **Context** — Provide Claude with specific instructions and conventions for your project
- **Flexibility** — Use arguments to make commands work with different inputs

Custom commands are particularly useful for project-specific workflows like running test suites, deploying code, or generating boilerplate following your team's conventions.
