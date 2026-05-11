---
layout: default
title: System Package Managers
nav_order: 3
permalink: /system-package-managers/
---

# System package managers

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
