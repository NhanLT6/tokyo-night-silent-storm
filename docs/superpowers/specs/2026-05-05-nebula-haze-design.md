# Nebula Haze — Design Spec

**Date:** 2026-05-05
**Author:** Nhan Le
**Supersedes:** `2026-05-05-soft-storm-refresh-design.md` (Soft Storm Refresh)

## Overview

Nebula Haze is a full identity shift from Tokyo Night Silent Storm. Where Tokyo Night leans warm and urban, Nebula Haze is cold, deep-space, and minimally saturated. The conceptual model: you are looking at a star field through a nebula. Most syntax reads as cosmic mist and cold gas — no neon, no city glow. Numbers are the one warm exception, acting as hot stellar points. The theme renames to **Nebula Haze**.

## Philosophy

- **Cold dominant:** keywords, functions, types, operators, and params all read as variations of cold nebula light
- **Sparse warmth:** only numbers (`hsl(45°)`) and HTML tags (`hsl(338°)`) carry heat — and the tags use cool rose, not red
- **Pastel band:** all syntax sits at S=18–55%, L=67–80% — bright enough to read, never neon
- **Two temperature families:** cold blues/purples for code structure; one warm dust cluster for data tokens
- **Deep backgrounds:** darker than Soft Storm everywhere — editor, chrome, and floats all step down one notch

## Identity

- **Theme name:** Nebula Haze (replaces Tokyo Night Silent Storm)
- **File names:** rename `tokyo-night-silent-storm.*` → `nebula-haze.*`
- **Parent theme:** Islands Dark (unchanged)

---

## Palette

### Backgrounds

| Role | Soft Storm | Nebula Haze | Note |
|---|---|---|---|
| Editor / panels | `#2c2f47` | `#22253a` | primary code surface |
| Chrome (main window, toolbar) | `#20243a` | `#1a1d30` | darker outer shell |
| Floating (tooltips, docs, popups) | `#252836` | `#13152a` | deepest — floats sit above editor |
| Island border | `#2c2f47` (invisible) | `#191c2e` | dark groove style — visible but subtle |
| Caret row | `#25293f` | `#181a2c` | darker than editor BG, no cyan cast |
| Selection | `#2d4f67` (teal) | `#3c3465` | muted purple `hsl(250,32%,30%)` |
| Secondary chrome / sticky / search field | `#242840` | `#1e2138` | search field BG, sticky lines |

### Syntax — Cold Family

| Token | Color | HSL reference | Conceptual name |
|---|---|---|---|
| Foreground / identifiers | `#c0caf5` | — | star haze |
| Local variables | `#a0c5e9` | — | nebula gas |
| **Parameters** | `#c6afa9` | `hsl(12, 20%, 72%)` | warm dust (salmon, barely pink) |
| Keywords | `#afa4e5` | `hsl(250, 55%, 77%)` | violet emission |
| Functions / methods | `#85a7f5` | — | neutron blue |
| Types / classes | `#b1d0e6` | `hsl(205, 52%, 80%)` | ice dwarf |
| Enums / structs / constants | `#73daca` | — | teal cloud (unchanged) |
| Strings | `#90d89f` | — | sulfur green (from ocean-harbor) |
| Operators / punctuation | `#7ab8d8` | — | cold plasma |
| Comments | `#5e6590` | — | dim fog |

### Syntax — Warm (used sparingly)

| Token | Color | HSL reference | Conceptual name |
|---|---|---|---|
| Numbers | `#d8c383` | `hsl(45, 52%, 68%)` | stellar gold |
| HTML / XML tags | `#cc8ea5` | `hsl(338, 38%, 68%)` | cool rose (warm but not red) |

### UI Accent

| Role | Soft Storm | Nebula Haze | Note |
|---|---|---|---|
| Tab underlines, focused borders, buttons | `#b8a4e8` (lavender) | `#84afeb` `hsl(215,72%,72%)` | space blue — distinct from keyword purple |
| Accent hover / lighter | `#c8b8f0` | `#a8c6f0` | lighter space blue |
| Tooltip / float border | `#b8a4e8` | `#84afeb` | space blue accent |

Keywords keep violet/purple in the editor. The UI chrome shifts to space blue so the two roles are never confused.

### Search Highlights

| Match type | Background | Border | Note |
|---|---|---|---|
| Normal find match | `#4a3e00` | `#c9a55a` | gold — reuses warning/number family |
| Current / active match | `#0d4f48` | `#73daca` | teal — reuses enum family |

Gold and teal are already native palette colors, so these highlights feel like they belong rather than being external callouts.

### VCS Markers

| Role | Soft Storm | Nebula Haze | Note |
|---|---|---|---|
| Added | `#79ad7b` | `#79ad7b` | unchanged soft green |
| Modified | `#b79a67` | `#bba586` `hsl(35,28%,63%)` | cosmic sand (cooler than amber) |
| Deleted / error | `#c7778a` | `#c7778a` | unchanged soft red |

---

## Delta from Soft Storm

This section lists only what changes. Everything not mentioned stays as defined in the Soft Storm spec.

| Category | Token / key | Soft Storm | Nebula Haze |
|---|---|---|---|
| **Identity** | Theme name | Tokyo Night Silent Storm | Nebula Haze |
| **Identity** | File prefix | `tokyo-night-silent-storm` | `nebula-haze` |
| **BG** | Editor | `#2c2f47` | `#22253a` |
| **BG** | Chrome | `#20243a` | `#1a1d30` |
| **BG** | Floating (tooltip/doc/lookup) | `#252836` | `#13152a` |
| **BG** | Island border | `#2c2f47` (invisible) | `#191c2e` (groove) |
| **BG** | Caret row | `#25293f` | `#181a2c` |
| **BG** | Selection | `#2d4f67` | `#3c3465` |
| **Syntax** | Params | `#ccb0ba` (cool rose) | `#c6afa9` (warm salmon) |
| **Syntax** | Strings | `#8fc472` | `#90d89f` |
| **Syntax** | Numbers | `#d4936a` (soft orange) | `#d8c383` (stellar gold) |
| **Syntax** | Types | `#4dc4d8` (cyan) | `#b1d0e6` (ice blue) |
| **Syntax** | Keywords | `#b8a4e8` | `#afa4e5` |
| **Syntax** | HTML tags | `#e07891` | `#cc8ea5` (cool rose) |
| **VCS** | Modified | `#b79a67` | `#bba586` |
| **UI accent** | All chrome | `#b8a4e8` (lavender) | `#84afeb` (space blue) |
| **UI accent** | Accent hover | `#c8b8f0` | `#a8c6f0` |
| **UI accent** | Tooltip border | `#b8a4e8` | `#84afeb` |
| **Search** | Normal match BG | `#473f68` | `#4a3e00` |
| **Search** | Normal match border | `#8c7ec0` | `#c9a55a` |
| **Search** | Active match BG | `#365a78` | `#0d4f48` |
| **Search** | Active match border | `#85a7f5` | `#73daca` |

---

## Implementation Scope

**Files to rename and edit:**

1. `tokyo-night-silent-storm.theme.json` → `nebula-haze.theme.json`
2. `tokyo-night-silent-storm.xml` → `nebula-haze.xml`
3. `preview.html` — update CSS variables
4. `plugin.xml` — update theme registration name and file references
5. `build.js` / `release.sh` / `package.json` — update file name references

**Strategy — three passes:**

**Pass 1: Accent color global replace** (theme.json)

Replace all occurrences of old accent with new space blue:

| Find | Replace | Role |
|---|---|---|
| `b8a4e8` | `84afeb` | primary accent |
| `c8b8f0` | `a8c6f0` | accent hover/lighter |
| `b8a4e880` | `84afeb80` | accent with alpha |
| `b8a4e840` | `84afeb40` | accent with low alpha |
| `7060b0` | `3d6fa8` | tool window selected BG (darker accent) |

**Pass 2: Background global replace** (theme.json + xml)

| Find | Replace | Role |
|---|---|---|
| `2c2f47` | `22253a` | editor background |
| `20243a` | `1a1d30` | chrome background |
| `252836` | `13152a` | floating background |
| `242840` | `1e2138` | secondary chrome |
| `25293f` | `181a2c` | caret row |
| `2d4f67` | `3c3465` | selection background |
| `363b54` | `2a2e4a` | inactive selected / progress BG |
| `3a3f5d` | `2a2e4a` | border color |
| `343954` | `252840` | disabled border |
| `3b3f5c` | `2a2e48` | line number / indent guides |
| `1e2030` | `0f1020` | diff separator |

After Pass 2, apply this targeted override in theme.json (Pass 2 sets it to `22253a` which is near-invisible; we want a visible groove):

- `Island.borderColor`: set to `#191c2e`

**Pass 3: Syntax token targeted edits** (xml only)

Apply individually — do not use global replace for syntax:

| Token group | Old value | New value |
|---|---|---|
| Parameters (list in Soft Storm spec) | `ccb0ba` | `c6afa9` |
| Strings (`DEFAULT_STRING`, etc.) | `8fc472` | `90d89f` |
| Numbers (`DEFAULT_NUMBER`, etc.) | `d4936a` | `d8c383` |
| Types (`DEFAULT_CLASS_NAME`, `DEFAULT_INTERFACE_NAME`, etc.) | `4dc4d8` | `b1d0e6` |
| Keywords (`DEFAULT_KEYWORD`, etc.) | `b8a4e8` | `afa4e5` |
| HTML tags (`HTML_TAG_NAME`, etc.) | `e07891` | `cc8ea5` |
| VCS modified (`MODIFIED_LINES_COLOR`, etc.) | `b79a67` | `bba586` |
| Search normal match background | `473f68` | `4a3e00` |
| Search normal match border | `8c7ec0` | `c9a55a` |
| Search active match background | `365a78` | `0d4f48` |
| Search active match border (was `85a7f5`) | `85a7f5` in WRITE_ context | `73daca` |
| Island/island border | `2c2f47` | `191c2e` |
| Tooltip BG | `252836` | `13152a` |

**Name change pass** (all files):

- Replace the string `"Tokyo Night Silent Storm"` with `"Nebula Haze"` everywhere it appears as a display name
- In `nebula-haze.theme.json`, update `"editorScheme"` from `"/tokyo-night-silent-storm.xml"` to `"/nebula-haze.xml"`
- In `plugin.xml`, update the `<editor-scheme>` `file` attribute and the `<name>` display string

---

## Preview HTML

Update CSS variables at the top of `preview.html`:
- All background vars to new darker values
- Accent from lavender to space blue
- Syntax colors to the new Nebula Haze values
- No structural changes needed
