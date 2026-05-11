# Nebula Haze — oh-my-posh Prompt Design

**Date:** 2026-05-11  
**Tool:** oh-my-posh (JSON config)  
**Shells:** PowerShell 7+, Bash (Fedora)  
**Font required:** JetBrains Mono NF (or any Nerd Font)

---

## Overview

A minimal two-line prompt with a galaxy-scatter divider line replacing the blank line between command blocks. Colors are hardcoded hex values inspired by the Nebula Haze palette — independent of `nebula-haze.xml` at runtime.

---

## Layout

Every command block is three lines:

```
⋆·- ⋅ ⊹ · ⋆ - · + ·· -         ← galaxy scatter (replaces blank line)
⚡ CommissionFactory/src/Button · 󰘬 feature/ds-4151-new-op…   ← info line
╰❯ _                              ← prompt line
```

---

## Segments

### 1. Galaxy scatter (divider line)

Appears as the first block in the prompt, replacing the blank line between command blocks.

**Pattern:** `⋆·- ⋅ ⊹ · ⋆ - · + ·· -`

| Char | Color | Hex | Role |
|------|-------|-----|------|
| `⋆` (1st) | s-mid | `#606480` | medium star |
| `·` (1st) | s-near | `#9480c8` | near/bright dot |
| `-` (1st) | s-far | `#414868` | dim dash |
| ` ` | — | — | space |
| `⋅` | s-far | `#414868` | dim dot operator |
| ` ` | — | — | space |
| `⊹` | s-core | `#c2c0e8` | brightest — focal point |
| ` ` | — | — | space |
| `·` (2nd) | s-mid | `#606480` | medium dot |
| ` ` | — | — | space |
| `⋆` (2nd) | s-far | `#414868` | far/dim star |
| ` ` | — | — | space |
| `-` (2nd) | s-mid | `#606480` | medium dash |
| ` ` | — | — | space |
| `·` (3rd) | s-far | `#414868` | far dot |
| ` ` | — | — | space |
| `+` | s-near | `#9480c8` | near cross |
| ` ` | — | — | space |
| `·` (4th, first of pair) | s-near | `#9480c8` | near dot |
| `·` (5th, second of pair) | s-far | `#414868` | far dot — contrast in pair |
| ` ` | — | — | space |
| `-` (3rd) | s-mid | `#606480` | medium dash |

Depth rationale: most chars are far/mid; one `⊹` is the single brightest point; `+` and the near dots create secondary highlights. No `✶` or other large chars.

---

### 2. Shell icon

Segment type: `shell`

All shells share the same color (`#6ec4b6`, teal-mid).

| Shell | Glyph | NF name |
|-------|-------|---------|
| `pwsh` / `powershell` | `󰨊` | `nf-md-powershell` |
| `bash` | `󱆃` | `nf-md-bash` |
| `zsh` | `󱆃` | `nf-md-bash` (no dedicated zsh glyph) |
| `fish` | `󱐋` | `nf-md-fish` |
| `cmd` | `󰖳` | `nf-md-windows` |
| `nu` (Nushell) | `󰬦` | `nf-md-nushell` |
| anything else | `󰣛` | `nf-md-fedora` (Linux/unknown fallback) |

---

### 3. Path

Segment type: `path`

- **Style:** `agnoster_short` — shows the last `max_depth` folder names; when deeper, a single `folder_icon` (`…`) replaces all truncated ancestors
- **Max depth:** 4 — renders up to 4 folders before the `…` prefix appears; example: `E:/…/ProjectRoot/src/Components/Button`
- **Folder separator:** `/` (dim `#606480` via `folder_separator_template`)
- **Truncation icon:** `…` (set via `folder_icon` property)
- **Config key:** `options` (oh-my-posh path segment uses `options`, not `properties`)

> `agnoster_full` was considered but rejected — it has no truncation support and always renders the complete path.
> A git-root-relative style (`../ProjectRoot/sub/path`) is not natively available in oh-my-posh.

**Color rules:**

| Context | Color | Hex |
|---------|-------|-----|
| Repo root folder (bold) | plain text | `#c0caf5` |
| Sub-path folders + separators | comments | `#606480` |
| Outside any git repo | green | `#8ab896` |

---

### 4. Path → git separator

A `·` character between the path segment and the git segment.

- Color: `#606480` (comments)
- Only rendered when the git segment is visible (i.e., not in IDE terminal)

---

### 5. Git branch

Segment type: `git`

| Property | Value |
|----------|-------|
| Branch icon | `󰘬` (`nf-md-source_branch`) — rendered manually in template |
| Icon color | `#7494c8` (blue-dim) |
| Branch name color | `#8aabe6` (blue-mid) |
| Max length | 20 characters |
| Truncation suffix | `…` |
| Show only | branch name — no dirty/ahead/behind indicators |
| `branch_icon` property | `""` (empty) — oh-my-posh prepends `BranchIcon` to `.HEAD`; setting empty prevents duplicate icon |

**Visibility condition — hidden when either env var is set:**

| IDE | Env var | Value |
|-----|---------|-------|
| JetBrains Rider | `TERMINAL_EMULATOR` | `JetBrains-JediTerm` |
| VS Code | `TERM_PROGRAM` | `vscode` |

---

### 6. Prompt connector

Two-character string rendered as the prompt character line.

**Normal state:**
```
╰❯
```
Both `╰` and `❯` color: `#9480c8` (violet-dim)

**Error state (exit code ≠ 0):**
```
╰❯  <code>
```
`╰`, `❯`, `󰅚` (nf-cod-error), and the numeric exit code all color: `#e07891` (error red)

The exit code display disappears on the next successful command.

---

## Features

| Feature | Config |
|---------|--------|
| Transient prompt | Enabled — full prompt collapses to bare `╰❯` in scrollback; collapsed `╰❯` uses dim color `#414868` (not violet) |
| Blank line before prompt | Replaced by galaxy scatter divider |
| Execution time | Disabled |

---

## Color reference

All values are hardcoded in the oh-my-posh JSON. No runtime dependency on `nebula-haze.xml`.

| Token | Hex | Source |
|-------|-----|--------|
| `#21243a` | Background | Nebula Haze base |
| `#6ec4b6` | Shell icon (all shells) | teal-mid |
| `#c0caf5` | Path text | plain text |
| `#606480` | Path separators, mid scatter | comments |
| `#414868` | Far scatter | chrome-mid |
| `#9480c8` | Near scatter, connector, `+` | violet-dim |
| `#c2c0e8` | Core scatter (`⊹`) | violet-whisper |
| `#8ab896` | Path outside repo | between green-dim and green-mid |
| `#7494c8` | Branch icon | blue-dim |
| `#8aabe6` | Branch name | blue-mid |
| `#e07891` | Error state | diagnostic error |

---

## Files to create

All prompt files live under `prompt/` — separate from the JetBrains/Rider theme at the project root.

| File | Purpose |
|------|---------|
| `prompt/nebula-haze.omp.json` | oh-my-posh theme config |
| `prompt/README.md` | Install instructions (font, oh-my-posh, shell profile setup) |
