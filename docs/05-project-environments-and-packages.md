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

- `uv` - [Watch an overview](https://www.youtube.com/watch?v=5rTwOt9Qgik)
- `pyenv` - [Watch an overview](https://www.youtube.com/watch?v=h2azrD35EYA)

### Python Virtual Environments

- `venv` + `pip` — built-in, simple, universal. The "old" way to manage Python environments.
- `uv` — fast, modern, recommended default.
- `pipenv` — modern, handles both env and packages
- `conda` / `mamba` — best when you need non-Python binaries (GDAL, CUDA, etc.)
- `poetry`, `pdm` — alternatives worth knowing

### R

- `renv` for project-scoped package libraries
- CRAN vs. Posit Package Manager vs. GitHub installs

### Reproducibility checklist

- A lockfile is committed (`uv.lock`, `requirements.txt`, `Pipfile.lock`, `renv.lock`)
- The `README` states the language version
- A new clone can run one command to get a working environment
