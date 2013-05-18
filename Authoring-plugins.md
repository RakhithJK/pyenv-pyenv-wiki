pyenv plugins provide new commands and/or hook into existing functionality of
pyenv. The following file naming scheme should be followed in a plugin project:

1. `bin/pyenv-COMMAND` for commands
2. `etc/pyenv.d/HOOK_NAME/*.bash` for hooks


## pyenv commands

An pyenv command is an executable named like `pyenv-COMMAND`. It will get
executed when a user runs `pyenv COMMAND`. Its help will be displayed when a
user runs `pyenv help COMMAND`. It can be written in any interpreted language,
but bash script is recommended for portability.

**A plugin command can't override any of the pyenv's built-in commands.**

### Environment

Each pyenv command runs with the following environment:

* `$PYENV_ROOT` - where pyenv versions & user data is placed, typically `~/.pyenv`
* `$PYENV_DIR` - the current directory of the caller
* `$PATH` - constructed to contain:
  1. pyenv's `libexec` dir with core commands
  1. `$PYENV_ROOT/plugins/*/bin` for plugin commands
  1. `$PATH` (external value)

### Calling other commands

When calling other commands from a command, use the `pyenv-COMMAND` form (with
dash) instead of `pyenv COMMAND` (with space).

Use pyenv's core low-level commands to inspect the environment instead of doing
it manually. For example, read the result of `pyenv-prefix` instead of
constructing it like `$PYENV_ROOT/versions/$version`.

A plugin command shouldn't have too much knowledge of pyenv's internals.

### Help text

An pyenv command should provide help text in the topmost comment of its source
code. The help format is described in `pyenv help help`.

Here is a template for an executable called `pyenv-COMMAND`:

```sh
#!/usr/bin/env bash
#
# Summary: One line, short description of a command
#
# Usage: pyenv COMMAND [--optional-flag] <required-argument>
#
# More thorough help text wrapped at 70 characters that spans
# multiple lines until the end of the comment block.

set -e
[ -n "$PYENV_DEBUG" ] && set -x

# Optional: Abort with usage line when called with invalid arguments
# (replace COMMAND with the name of this command)
if [ -z "$1" ]; then
  pyenv-help --usage COMMAND >&2
  exit 1
fi
```

### Completions

A command can optionally provide tab-completions in the shell by outputting
completion values when invoked with the `--complete` flag.

``` sh
# Provide pyenv completions
if [ "$1" = "--complete" ]; then
  echo hello
  exit
fi
```

Note: **it's important to keep the above comment intact**. This is how pyenv
detects if a command is capable of providing completion values.


## pyenv hooks

Hooks are bash scripts named like `HOOK_NAME/*.bash`, where "HOOK_NAME" is one
of:

* `exec`
* `rehash`
* `which`

Hooks are looked for in `$PYENV_HOOK_PATH`, which is composed of:

1. `$PYENV_HOOK_PATH` (external value)
1. `$PYENV_ROOT/pyenv.d`
1. `/usr/local/etc/pyenv.d`
1. `/etc/pyenv.d`
1. `/usr/lib/pyenv/hooks`
1. `$PYENV_ROOT/plugins/*/etc/pyenv.d`

Hook scripts are executed at specific points during pyenv operation. They
provide a low-level entry point for integration with pyenv's functionality. To
get a better understanding of the possibilities with hooks, read the source
code of pyenv's hook-enabled commands listed above.
