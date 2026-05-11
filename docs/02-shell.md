---
layout: default
title: The Shell
nav_order: 2
permalink: /shell/
---

# The shell

- Identify your shell (`echo $SHELL`)
- Configuration files: `~/.zshrc`, `~/.bashrc`, `~/.zprofile`, `~/.bash_profile`
- The `PATH` variable: how the shell finds executables
- Useful aliases and functions
- Recommended: a minimal prompt, a working `which`, and `command -v`

### Examples

Find out which shell you are running and where its binary lives:

```bash
echo $SHELL                # /bin/zsh
ps -p $$                   # confirm the running shell, not just the default
```

Inspect your `PATH` — the ordered list of directories the shell searches for executables:

```bash
echo $PATH
echo $PATH | tr ':' '\n'   # one directory per line, easier to read
```

Find out exactly which binary will run when you type a command:

```bash
which python              # first match on PATH
command -v python         # POSIX equivalent
type -a python            # show every match, in order
```

Add a directory to the front of `PATH` in your `~/.zshrc` so a tool you installed manually takes precedence:

```bash
# ~/.zshrc
export PATH="$HOME/.local/bin:$PATH"
```

Reload the file without opening a new terminal:

```bash
source ~/.zshrc
```

Define a few aliases and a small function:

```bash
# ~/.zshrc
alias ll='ls -lah'
alias gs='git status'
alias activate='source .venv/bin/activate'

mkcd() { mkdir -p "$1" && cd "$1"; }
```
