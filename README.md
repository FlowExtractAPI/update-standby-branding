# update-standby-branding

A Claude Code slash command that updates Actor READMEs from the former “Standby” terminology to Apify **Server Actors** branding.

The command updates prose, headings, and link text while preserving code identifiers and configuration examples that intentionally use `standby`.

## What it does

- Rewrites Standby terminology contextually, following the naming rules in the command definition.
- Preserves code-level identifiers, configuration examples, and unresolved documentation URLs.
- If a README has no Standby mentions, can add a section describing the server interface as an alternative way to call the Actor.
- Presents proposed changes for confirmation before applying them.

## Install

Copy `update-standby-branding.md` into the Claude Code commands directory for your project:

```bash
mkdir -p .claude/commands
cp update-standby-branding.md .claude/commands/update-standby-branding.md
```

Or install it for your user account:

```bash
mkdir -p ~/.claude/commands
cp update-standby-branding.md ~/.claude/commands/update-standby-branding.md
```

## Usage

In Claude Code, run the command with the Markdown file or files to update:

```text
/update-standby-branding README.md
```

With no file path, the command searches the current directory tree for README files mentioning “Standby” and asks you to confirm the targets.

## Terminology

| Term | Usage |
|---|---|
| **Actor** | Apify's building block; always capitalized |
| **Server Actor** / **Server Actors** | An Actor with the server interface enabled |
| **server interface** | The HTTP mechanism exposed by a Server Actor; lowercase |
| **input interface** | The classic run-with-input mechanism; lowercase |
| **multi-tenant** / **single-tenant** | Tenancy terms; lowercase and hyphenated in prose |

For the full naming rules and replacement guidance, see [`update-standby-branding.md`](update-standby-branding.md).

## Contributing

Contributions are welcome. To propose a change:

1. Fork the repository.
2. Create a branch for your change.
3. Make and review your changes.
4. Open a pull request describing what changed and why.

For changes to the command, keep replacements contextual rather than using blind find-and-replace. Preserve code identifiers and follow the terminology and workflow guidance in `update-standby-branding.md`.

## Repository contents

- [`update-standby-branding.md`](update-standby-branding.md) — Claude Code slash-command definition
