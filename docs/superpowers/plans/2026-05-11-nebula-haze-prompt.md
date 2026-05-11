# Nebula Haze Prompt Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Create `prompt/nebula-haze.omp.json` — a complete oh-my-posh theme matching the approved design spec.

**Architecture:** A single oh-my-posh JSON config with three blocks (scatter divider, info line, connector). All hex values hardcoded. No runtime dependency on `nebula-haze.xml`. Works in PowerShell 7+ and Bash.

**Tech Stack:** oh-my-posh v3 (schema version 2), JetBrains Mono NF, PowerShell 7 / Bash

---

### Task 1: Create `prompt/` folder and scaffold the JSON

**Files:**
- Create: `prompt/nebula-haze.omp.json`

- [ ] **Step 1: Create the file with schema + transient prompt**

```json
{
  "$schema": "https://raw.githubusercontent.com/JanDeDobbeleer/oh-my-posh/main/themes/schema.json",
  "version": 2,
  "final_space": true,
  "transient_prompt": {
    "background": "transparent",
    "foreground": "#414868",
    "template": "╰❯ "
  },
  "blocks": []
}
```

- [ ] **Step 2: Validate JSON is well-formed**

```powershell
Get-Content prompt/nebula-haze.omp.json | ConvertFrom-Json
```

Expected: object returned with no errors.

- [ ] **Step 3: Commit**

```bash
git add prompt/nebula-haze.omp.json
git commit -m "feat(prompt): scaffold oh-my-posh config"
```

---

### Task 2: Add block 1 — galaxy scatter divider line

The scatter is a static `text` segment. Each character has its own color using oh-my-posh template markup `<#hex>char</>`.

Pattern: `⋆·- ⋅ ⊹ · ⋆ - · + ·· -`

Depth map (from spec):
| Char | Hex |
|------|-----|
| `⋆` (1st) | `#606480` |
| `·` (1st) | `#9480c8` |
| `-` (1st) | `#414868` |
| `⋅` | `#414868` |
| `⊹` | `#c2c0e8` |
| `·` (2nd) | `#606480` |
| `⋆` (2nd) | `#414868` |
| `-` (2nd) | `#606480` |
| `·` (3rd) | `#414868` |
| `+` | `#9480c8` |
| `·` (4th) | `#9480c8` |
| `·` (5th) | `#414868` |
| `-` (3rd) | `#606480` |

**Files:**
- Modify: `prompt/nebula-haze.omp.json`

- [ ] **Step 1: Replace `"blocks": []` with block 1**

```json
"blocks": [
  {
    "type": "prompt",
    "alignment": "left",
    "segments": [
      {
        "type": "text",
        "style": "plain",
        "background": "transparent",
        "foreground": "transparent",
        "template": "<#606480>⋆</><#9480c8>·</><#414868>-</> <#414868>⋅</> <#c2c0e8>⊹</> <#606480>·</> <#414868>⋆</> <#606480>-</> <#414868>·</> <#9480c8>+</> <#9480c8>·</><#414868>·</> <#606480>-</>"
      }
    ]
  }
]
```

- [ ] **Step 2: Validate**

```powershell
Get-Content prompt/nebula-haze.omp.json | ConvertFrom-Json
```

- [ ] **Step 3: Commit**

```bash
git add prompt/nebula-haze.omp.json
git commit -m "feat(prompt): add galaxy scatter divider segment"
```

---

### Task 3: Add block 2 — info line (shell + path + git)

Three segments on one line. Block uses `"newline": true` to start below the scatter.

**Files:**
- Modify: `prompt/nebula-haze.omp.json`

- [ ] **Step 1: Append block 2 inside `"blocks"`**

```json
{
  "type": "prompt",
  "alignment": "left",
  "newline": true,
  "segments": [
    {
      "type": "shell",
      "style": "plain",
      "background": "transparent",
      "foreground": "#6ec4b6",
      "template": "{{ if or (eq .Name \"pwsh\") (eq .Name \"powershell\") }}󰨊 {{ else }}󰣛 {{ end }}"
    },
    {
      "type": "path",
      "style": "plain",
      "background": "transparent",
      "foreground": "#c0caf5",
      "properties": {
        "style": "agnoster_full",
        "folder_separator_icon": "/",
        "folder_separator_template": "<#606480>/</>",
        "max_depth": 4,
        "truncation_symbol": "…"
      }
    },
    {
      "type": "git",
      "style": "plain",
      "background": "transparent",
      "foreground": "#8aabe6",
      "template": "{{ if and (ne .Env.TERMINAL_EMULATOR \"JetBrains-JediTerm\") (ne .Env.TERM_PROGRAM \"vscode\") }} <#606480>·</> <#7494c8>󰘬 </>{{ if gt (len .HEAD) 20 }}{{ trunc 20 .HEAD }}…{{ else }}{{ .HEAD }}{{ end }}{{ end }}",
      "properties": {
        "fetch_status": false,
        "fetch_upstream_icon": false
      }
    }
  ]
}
```

- [ ] **Step 2: Validate**

```powershell
Get-Content prompt/nebula-haze.omp.json | ConvertFrom-Json
```

- [ ] **Step 3: Commit**

```bash
git add prompt/nebula-haze.omp.json
git commit -m "feat(prompt): add shell, path, and git segments"
```

---

### Task 4: Add block 3 — connector line with exit code

Both `╰` and `❯` turn error-red together on failure. `nf-cod-error` icon (`󰅚`) appears alongside the exit code.

**Files:**
- Modify: `prompt/nebula-haze.omp.json`

- [ ] **Step 1: Append block 3 inside `"blocks"`**

```json
{
  "type": "prompt",
  "alignment": "left",
  "newline": true,
  "segments": [
    {
      "type": "exit",
      "style": "plain",
      "background": "transparent",
      "foreground": "#9480c8",
      "template": "{{ if gt .Code 0 }}<#e07891>╰❯ 󰅚 {{ .Code }}</>{{ else }}╰❯{{ end }}"
    }
  ]
}
```

- [ ] **Step 2: Validate full config**

```powershell
Get-Content prompt/nebula-haze.omp.json | ConvertFrom-Json
```

- [ ] **Step 3: Commit**

```bash
git add prompt/nebula-haze.omp.json
git commit -m "feat(prompt): add connector segment with exit code error state"
```

---

### Task 5: Render and verify

Render the prompt statically using oh-my-posh's CLI. This doesn't require an interactive session.

**Files:** none (read-only verification)

- [ ] **Step 1: Check oh-my-posh is installed**

```powershell
oh-my-posh version
```

Expected: version string like `23.x.x`. If not found, install via winget:
```powershell
winget install JanDeDobbeleer.OhMyPosh
```

- [ ] **Step 2: Render the prompt (success state)**

```powershell
oh-my-posh print primary --config prompt/nebula-haze.omp.json --shell pwsh
```

Expected output (3 lines with ANSI colors):
- Line 1: scatter pattern `⋆·- ⋅ ⊹ · ⋆ - · + ·· -` in violet/dim colors
- Line 2: `󰨊 <path>` with optional branch
- Line 3: `╰❯` in violet

- [ ] **Step 3: Render error state**

```powershell
oh-my-posh print primary --config prompt/nebula-haze.omp.json --shell pwsh --error 1
```

Expected: line 3 shows `╰❯ 󰅚 1` all in error red `#e07891`.

- [ ] **Step 4: Fix any rendering issues, commit fixes**

Common issues to check:
- Scatter line: verify each char has correct color (look for wrong brightness/color)
- Shell icon: `󰨊` should appear in teal, not as a box/`?`
- Path: slashes should be dimmer than folder names
- Git: branch appears only when outside IDE (test by setting env var: `$env:TERMINAL_EMULATOR="JetBrains-JediTerm"` then re-render)
- Connector: `╰❯` in violet in success, full red with icon+code in error

```powershell
# test IDE detection: should hide git segment
$env:TERMINAL_EMULATOR = "JetBrains-JediTerm"
oh-my-posh print primary --config prompt/nebula-haze.omp.json --shell pwsh
Remove-Item Env:TERMINAL_EMULATOR
```

```bash
git add prompt/nebula-haze.omp.json
git commit -m "fix(prompt): adjust rendering issues from preview"
```

---

### Task 6: Write `prompt/README.md`

**Files:**
- Create: `prompt/README.md`

- [ ] **Step 1: Write the install guide**

```markdown
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
```

- [ ] **Step 2: Commit**

```bash
git add prompt/README.md
git commit -m "docs(prompt): add install instructions"
```

---

## Spec coverage check

| Spec requirement | Task |
|-----------------|------|
| oh-my-posh tool | Task 1 |
| Galaxy scatter divider with exact char+color map | Task 2 |
| Shell icon: 󰨊 PowerShell teal, 󰣛 Fedora green | Task 3 |
| Path: agnoster_full, `/` separator in #606480 | Task 3 |
| Path truncation at depth 4 | Task 3 |
| Git: 󰘬 icon, branch truncated 20 chars | Task 3 |
| Git hidden in Rider + VS Code | Task 3 |
| `·` separator between path and git | Task 3 |
| `╰❯` violet-dim normal, full error-red on failure | Task 4 |
| `nf-cod-error` + exit code on failure | Task 4 |
| Transient prompt collapses to `╰❯` | Task 1 (transient_prompt) |
| Files in `prompt/` subfolder | Task 1 |
| README with install instructions | Task 6 |

> **Note:** Outside-repo green path color (`#8ab896`) is not implemented — `foreground_templates` for git-context detection in the path segment requires runtime testing to verify. Deferred to a follow-up once the core prompt is working.
