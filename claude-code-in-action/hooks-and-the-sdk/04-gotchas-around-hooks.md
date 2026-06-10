# Gotchas around hooks

Course: [Claude Code in Action](https://anthropic.skilljar.com/claude-code-in-action) · Section: Hooks and the SDK

After running `npm run setup` you may notice two `settings.json` files in the `.claude` directory. Here's what's going on.

## Hooks security and absolute paths

The Claude Code documentation recommends using **absolute paths** (rather than relative paths) for hook scripts. This helps mitigate path interception and binary planting attacks.

But this recommendation makes it much harder to share `settings.json` files: the absolute path to a hook script on your machine will differ from the path on someone else's, since you'll likely place the project in different directories.

## The `$PWD` placeholder solution

To solve this, the project includes a `settings.example.json` file whose script references use a `$PWD` placeholder.

When you run `npm run setup`, it installs dependencies and also runs an `init-claude.js` script in the `scripts` directory. This script:

1. Replaces the `$PWD` placeholders with the absolute path to the project on your machine
2. Copies the `settings.example.json` file
3. Renames the copy to `settings.local.json`

This lets the project share a settings template while still using the recommended absolute paths on each machine.
