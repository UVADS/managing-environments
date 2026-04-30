---
layout: default
title: Troubleshooting
nav_order: 11
---

# Troubleshooting

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
