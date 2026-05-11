# Nebula Haze — oh-my-posh Prompt

Minimal two-line terminal prompt inspired by the Nebula Haze color palette.

## Requirements

- [oh-my-posh](https://ohmyposh.dev/docs/installation/windows) v3+
- A Nerd Font — [JetBrains Mono NF](https://www.nerdfonts.com/font-downloads) recommended

## Install

### Windows — PowerShell

1. Install oh-my-posh:
   ```powershell
   winget install JanDeDobbeleer.OhMyPosh
   ```

2. Set your terminal font to **JetBrains Mono NF** in Windows Terminal settings.

3. Add to your PowerShell profile (`$PROFILE`):
   ```powershell
   oh-my-posh init pwsh --config "C:\path\to\prompt\nebula-haze.omp.json" | Invoke-Expression
   ```
   Replace `C:\path\to` with the actual path to this repo.

### Linux / Fedora — Bash

1. Install oh-my-posh:
   ```bash
   curl -s https://ohmyposh.dev/install.sh | bash -s
   ```

2. Add to `~/.bashrc`:
   ```bash
   eval "$(oh-my-posh init bash --config ~/path/to/prompt/nebula-haze.omp.json)"
   ```

## IDE terminals

Git branch is automatically hidden inside **Rider** and **VS Code** terminals — detected via `TERMINAL_EMULATOR=JetBrains-JediTerm` and `TERM_PROGRAM=vscode`.

## Features

- 3-line layout: scatter divider → info line → connector
- Shell icon: `󰨊` PowerShell · `󰣛` Fedora/bash
- Full path from git root, truncated when deep
- Branch name truncated to 20 chars
- `╰❯` turns red with exit code on failure
- Transient prompt: previous prompts collapse to `╰❯` in scrollback
