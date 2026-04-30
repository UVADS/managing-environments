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

[The Mental Model](the-mental-model){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }
[Bootstrap a Machine]({{ site.baseurl }}/bootstrapping-a-new-machine/){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }
[Bootstrap a Project]({{ site.baseurl }}/bootstrapping-a-new-project/){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }
[Troubleshooting]({{ site.baseurl }}/troubleshooting/){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }

---

<img align="right" style="max-width:40%;float:right;" src="https://s3.amazonaws.com/uvasds-systems/images/laptop-illustration-svg-download-png-4543731.png" />

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

## The mental model

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

## Going further

- Containers (Docker, Dev Containers) for fully portable environments
- Cloud notebooks (Colab, SageMaker, Posit Cloud) as fallbacks, not replacements
- Dotfiles repos for sharing your config across machines
