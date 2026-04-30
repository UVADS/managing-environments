---
layout: default
title: Home
nav_order: 1
description: "A practical guide for data science students on managing local development environments."
permalink: /
last_modified_date: "2026-04-30 09:30AM"
---

# Managing Your Development Environment
{: .fs-9 }

How to set up, understand, and maintain a local development environment — for data science students.
{: .fs-6 .fw-300 }

[The Mental Model](#1-the-mental-model){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }
[Bootstrap a Machine](#9-bootstrapping-a-new-machine){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }
[Bootstrap a Project](#10-bootstrapping-a-new-project){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }
[Troubleshooting](#11-troubleshooting){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }

---

The goal here is not to memorize commands, but to build a mental model of what lives where on your machine and why.

## Who this is for

Students who can open a terminal but feel uncertain about:

- Where Python (or R, or Node) actually lives on their laptop
- Why one project's packages break another project
- What an environment variable is and where to set it
- How to recover when "it worked yesterday"

## Learning goals

By the end of this guide, you should be able to:

1. Describe the layers of your environment: OS → shell → language runtimes → package managers → project environments → IDE.
2. Install and switch between language versions without breaking your system.
3. Create isolated, reproducible project environments.
4. Manage secrets and configuration through environment variables.
5. Bootstrap a brand-new machine in under an hour.

---

## 1. The mental model

Before installing anything, understand the stack:

```
Operating System (macOS / Windows / Linux)
   └── Shell (zsh, bash, PowerShell)
        └── System package manager (Homebrew, apt, winget)
             └── Language runtimes (Python, R, Node, Julia)
                  └── Language package managers (pip, uv, conda, renv, npm)
                       └── Project environments (.venv, conda env, renv)
                            └── Editor / IDE (VS Code, RStudio, JupyterLab)
```

Each layer is replaceable, and better tools within each layer continually emerge. Problems usually come from confusing which layer you are working on.

## 2. The shell

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

## 3. System package managers

Install once, used by everything below.

- **macOS:** Homebrew (`brew`)
- **Windows:** winget or Chocolatey; consider WSL2 for a Linux-like experience
- **Linux:** `apt`, `yum`, `dnf`, or your distro's native manager

Use these for system-level tools (`git`, `curl`, `jq`, `ffmpeg`), not for project dependencies.

### Examples

**macOS — Homebrew**

Install Homebrew (one-time):

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Install, search, and update packages:

```bash
brew install git jq ffmpeg     # install several tools at once
brew search postgres           # find a package
brew info uv                   # see version, dependencies, caveats
brew list                      # everything you've installed
brew upgrade                   # update all installed packages
brew uninstall ffmpeg          # remove a package
```

GUI apps (browsers, editors, Docker Desktop) install via `--cask`:

```bash
brew install --cask visual-studio-code rstudio docker
```

**Windows — winget**

```powershell
winget search git
winget install --id Git.Git -e
winget install --id Python.Python.3.12 -e
winget upgrade --all
```

**Linux — apt (Debian/Ubuntu)**

```bash
sudo apt update                # refresh the package index first
sudo apt install git curl jq ffmpeg
sudo apt upgrade               # upgrade installed packages
apt list --installed | grep -i python
```

**What belongs here vs. a language package manager**

| Install with the system manager        | Install with a language manager        |
|----------------------------------------|----------------------------------------|
| `git`, `curl`, `wget`, `jq`            | `pandas`, `numpy`, `scikit-learn`      |
| `ffmpeg`, `imagemagick`, `graphviz`    | `dplyr`, `ggplot2`, `tidyverse`        |
| Compilers and build tools (`gcc`, `make`) | `express`, `react`, `next`           |
| Database clients (`postgresql`, `sqlite`) | Project-specific libraries           |

## 4. Languages and version managers

Never rely on the system Python (or R, or Node). Use a version manager so you can install, switch, and remove versions cleanly.

| Language | Recommended version manager |
|----------|-----------------------------|
| Python   | `uv` or `pyenv`             |
| R        | `rig`                       |
| Node     | `nvm` or `fnm`              |
| Julia    | `juliaup`                   |

Cover for each:

- How to install the manager
- How to install a specific version
- How to set a global default vs. a per-project version
- How to verify (`python --version`, `which python`)

## 5. Project environments and packages

The single most important habit: **one isolated environment per project.**

### Python options

- `venv` + `pip` — built-in, simple, universal
- `uv` — fast, modern, recommended default
- `pipenv` — modern, handles both env and packages
- `conda` / `mamba` — best when you need non-Python binaries (GDAL, CUDA, etc.)
- `poetry`, `pdm` — alternatives worth knowing

### R

- `renv` for project-scoped package libraries
- CRAN vs. Posit Package Manager vs. GitHub installs

### Reproducibility checklist

- A lockfile is committed (`uv.lock`, `requirements.txt`, `renv.lock`)
- The README states the language version
- A new clone can run one command to get a working environment

## 6. Editors and IDEs

Pick one primary editor and learn it well.

- **VS Code / Cursor** — general-purpose, strong Python and notebook support
- **JupyterLab** — notebook-first workflows
- **RStudio / Positron** — first-class R; Positron also handles Python
- **PyCharm** — heavyweight, strong refactoring

For each, cover:

- How to point the editor at the *project* environment, not the system interpreter
- Recommended extensions (linter, formatter, Jupyter, Git)
- Opening a project as a folder vs. a workspace

## 7. Environment variables and secrets

What an environment variable is, and the three places they typically live:

1. **Shell rc files** (`~/.zshrc`) — for things you want everywhere
2. **Project `.env` files** — for per-project config; loaded by `python-dotenv`, `direnv`, or your framework
3. **Secret managers** — 1Password CLI, AWS Secrets Manager, etc., for anything sensitive

Rules:

- Never commit `.env` files. Add them to `.gitignore`.
- Provide a committed `.env.example` showing required keys with empty values.
- Treat API keys, database URLs, and tokens as secrets even in coursework.

## 8. Git and GitHub

- `git` config: name, email, default branch, editor
- SSH keys vs. HTTPS + credential helper
- `.gitignore` patterns every DS project should have (`.env`, `.ipynb_checkpoints/`, `data/`, `.venv/`)
- GitHub CLI (`gh`) for cloning, PRs, and auth

See [**Git Basics**](https://uvads.github.io/git-basics/) to learn more about `git` and GitHub for data science.

## 9. Bootstrapping a new machine

A checklist students can run top-to-bottom on a fresh laptop:

1. Install system updates and Xcode Command Line Tools (macOS) / build-essential (Linux)
2. Install Homebrew (or equivalent)
3. Install git, configure name/email, set up SSH keys
4. Install your version manager(s) and one default language version
5. Install your editor and sign in to sync settings
6. Clone a known-good project and verify the full setup works end-to-end

## 10. Bootstrapping a new project

The minimum a new project should have on day one:

- A README describing what it does and how to run it
- A pinned language version
- A lockfile-producing package manager configured
- A `.gitignore`
- A `.env.example`
- One command (or short script) that creates the environment from scratch

> **Write an AI Agent for this?** Most modern IDEs (Claude, VSCode, Claude Code) allow you to write your own agent(s) for specific tasks. Create an agent that sets up all new projects for you according to your requirements and standards. This could include all the items above, plus a new GitHub repository linked to the project.

## 11. Troubleshooting

When something breaks, work down the stack:

- `which <tool>` — am I running what I think I am?
- `echo $PATH` — is the right directory first?
- `<tool> --version` — is it the version I expect?
- Is the editor using the project environment, or the system one?
- Did a recent shell-rc edit shadow something?

Common traps:

- Two Pythons on `PATH`, system one wins
- Editor terminal uses a different shell than your system terminal
- `.env` not loaded because it lives one directory up from where the program runs
- `pip install` ran outside the activated environment

## 12. Going further

- Containers (Docker, Dev Containers) for fully portable environments
- Cloud notebooks (Colab, SageMaker, Posit Cloud) as fallbacks, not replacements
- Dotfiles repos for sharing your config across machines
