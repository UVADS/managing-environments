---
layout: default
title: Project Environments and Packages
nav_order: 5
permalink: /project-environments-and-packages/
---

# Project environments and packages

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
