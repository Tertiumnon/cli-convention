# CLI Convention

CLI conventions for Tertium tools: commands, short and long flags, one- and two-dash meaning, errors and output.

Conventions for command-line tools in the Tertium projects. This repo is documentation only; individual tools may need updates to follow these rules.

## Commands

- A command is one lowercase word: `create`, `merge`, `release`.
- Commands take flags, not positional options: `gith create --release=1.2.0`, not `gith create release 1.2.0`.
- `help` is a command, not a flag. Use `<tool> help` for general usage and `<tool> help <command>` for a command's usage. For nested commands, give the full command path after `help`.

## Flags

Every flag has a descriptive name. A switch may also have a one-letter alias for common use.

The dash count sets how the flag takes its value:

| Form | Meaning |
| --- | --- |
| `-name` | Switch or automatic selection; takes no value. |
| `--name=<value>` | Option with an explicit value; the equals sign and value are required when the option is supplied. |
| `--name`, `--name <value>` | Invalid: an option requires `=<value>`. |

An option can itself be optional or required by a command; either way, it needs a value when supplied. A switch and an option may share a name when the command supports both automatic and explicit selection.

Examples of the convention:

```bash
gith create --release=1.2.0  # explicit version
gith create -release         # version picked from the latest tag
gith create --branch=login   # explicit branch name
gith release -patch          # switch
```

When flags are mutually exclusive, giving more than one is an error.

## Errors

- Print one line starting with `❌`, then exit with code 1.
- Name the bad input, and where it helps, show the valid form: `--branch needs a value; use --branch=<name>.`
- A missing required flag prints the usage line for that command, not the whole help text.
- Never print a stack trace for an input mistake.

## Output

- Print each git or shell step as it runs (`> git push ...`), so a failure can be traced.
- Finish with one `✅` line that says what happened.

## Scope

These rules describe how tools are used on the command line. Git branch and commit naming is covered in [git-convention](https://github.com/Tertiumnon/git-convention).

## Support

If this project is useful to you, you can support its development on [Ko-fi](https://ko-fi.com/tertiumnon).
