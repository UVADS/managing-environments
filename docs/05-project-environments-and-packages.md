---
layout: default
title: Project Environments and Packages
nav_order: 5
permalink: /project-environments-and-packages/
last_modified_date: "2026-07-01"
---

# Project environments and packages

The single most important habit: **one isolated environment per project.**

### Python Versions

- `uv`
- `pyenv`

### Python Virtual Environments

- `venv` + `pip` — built-in, simple, universal. The "old" way to manage Python environments, **not recommended**.
- `uv` — fast, modern, recommended default. [Watch an overview](https://www.youtube.com/watch?v=5rTwOt9Qgik)
- `pipenv` — modern, handles both env and packages. [Watch an overview](https://www.youtube.com/watch?v=h2azrD35EYA)
- `conda` / `mamba` — best when you need non-Python binaries (GDAL, CUDA, etc.)
- `poetry`, `pdm` — alternatives worth knowing

{: .highlight }
> **Why not use `venv` and `pip`?**
> 
> Designed to solve the problem of virtual environments and package management, these tools are slow and inconsistent. Some reasons newer tools such as `uv` are better:
> 
> - Speed: `pip`'s dependency resolver is slow and venv creation/installs add up. `uv` (Rust-based) is 10-100x faster via a global cache and parallel installs.
> - Reproducibility: `pip freeze` gives a flat, unpinned list — no lockfile, no hash verification, no distinction between direct vs. transitive deps. `uv` generates a proper cross-platform lockfile (`uv.lock`), so "works on my machine" becomes rare.
> - Fewer tools: `uv` replaces `venv` + `pip` + `pip-tools` (and often `pyenv`) with one binary: `uv venv`, `uv add`, `uv sync`, `uv run`. Less surface area to teach or debug in a lab setting.
> - Standard-aligned: it's built around `pyproject.toml`, the modern packaging standard, rather than `requirements.txt`.

### R

- `renv` for project-scoped package libraries
- CRAN vs. Posit Package Manager vs. GitHub installs

### Reproducibility checklist

- A lockfile is committed (`uv.lock`, `requirements.txt`, `Pipfile.lock`, `renv.lock`)
- The `README` states the language version
- A new clone can run one command to get a working environment
