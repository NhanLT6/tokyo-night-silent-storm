# Soft Storm Refresh — Design Spec

**Date:** 2026-05-05
**Author:** Nhan Le

## Overview

A palette refresh of Tokyo Night Silent Storm that shifts the mood from aged/heavy to modern and pastel. The theme identity stays intact (purple-blue Tokyo Night DNA) but every vivid neon is muted one notch, backgrounds are micro-lifted, and two semantic tokens — local variables and parameters — receive distinct colors for the first time.

## Goals

- Soften every saturated syntax color without changing hue family
- Lift background depth just enough to reduce the "heavy" feel
- Give local variables a distinct sky-blue color (was invisible, same as foreground)
- Replace amber parameters with a cooler desaturated rose that fits the palette's temperature
- Reduce Islands chrome/border noise while keeping internal dividers readable
- Make current row and find results easier to see without turning them into accent-heavy UI
- Soften VCS markers so large edit sessions do not pull too much attention
- Keep enums/structs/selection/foreground unchanged — they already read as pastel

## What Does Not Change

- Theme identity: still purple-blue Tokyo Night
- Structural files: `plugin.xml`, `build.js`, `package.json`, `release.sh`
- Parent theme: Islands Dark
- Tokens not listed below: inherit unchanged from existing scheme
- Version bump handled separately

---

## Palette

### Backgrounds

| Role | Original | Soft Storm |
|---|---|---|
| Chrome / main window | `#22253a` | `#20243a` |
| Editor / panels | `#2a2d3e` | `#2c2f47` |
| Caret row | `#303450` | `#25293f` |
| Selection | `#2d4f67` | `#2d4f67` *(unchanged)* |

`#242840` is still used for some secondary chrome surfaces (for example search field and editor-scheme notification/sticky backgrounds), but visible outer IDE chrome uses the darker `#20243a`.

### Syntax

| Token | Original | Soft Storm | Note |
|---|---|---|---|
| Foreground / identifiers | `#c0caf5` | `#c0caf5` | unchanged |
| Keywords | `#bb9af7` | `#b8a4e8` | softer purple |
| Functions / methods | `#7aa2f7` | `#85a7f5` | slightly lighter |
| Strings | `#9ece6a` | `#8fc472` | muted green |
| Numbers | `#ff9e64` | `#d4936a` | softer orange |
| Types / classes | `#2ac3de` | `#4dc4d8` | softer cyan |
| Operators / punctuation | `#89ddff` | `#7ab8d8` | muted |
| HTML / XML tags | `#f7768e` | `#e07891` | softer pink |
| Comments | `#6272a4` | `#5e6590` | minimal change |
| Enums / structs / constants | `#73daca` | `#73daca` | unchanged |

### Semantic Tokens (new / recolored)

| Token | Original | Soft Storm | Note |
|---|---|---|---|
| **Local variables** | `#c0caf5` (= foreground) | `#a0c5e9` | sky-blue, first distinct color |
| **Parameters** | `#e0af68` amber | `#ccb0ba` | desaturated rose, fits cool palette |

The `DEFAULT_LOCAL_VARIABLE`, `DEFAULT_REASSIGNED_LOCAL_VARIABLE`, `ReSharper.MUTABLE_LOCAL_VARIABLE_IDENTIFIER`, and JS/TS local variable tokens all receive `#a0c5e9`. Parameter tokens (`DEFAULT_PARAMETER`, `DEFAULT_REASSIGNED_PARAMETER`, `JS.PARAMETER`, `TS.TYPE_PARAMETER`, `ANNOTATION_ATTRIBUTE_NAME_ATTRIBUTES`, `HTTP_REQUEST_PARAMETER_NAME`, etc.) all receive `#ccb0ba`.

### UI Chrome (theme.json)

| Key | Original | Soft Storm |
|---|---|---|
| `*.background` | `#2a2d3e` | `#2c2f47` |
| `MainWindow.background` | `#22253a` | `#20243a` |
| `ToolWindow.Stripe.background` | `#22253a` | `#20243a` |
| `MainToolbar.background` | `#22253a` | `#20243a` |
| `Toolbar.background` / `NavBar.background` | `#22253a` | `#20243a` |
| `EditorTabs.background` | inherited | `#2c2f47` |
| `EditorTabs.underlinedBorderColor` | `#bb9af7` | `#b8a4e8` |
| `Button.default.startBackground` | `#bb9af7` | `#b8a4e8` |
| `Button.default.endBackground` | `#bb9af7` | `#b8a4e8` |
| `Button.default.startBorderColor` | `#bb9af7` | `#b8a4e8` |
| `Button.default.endBorderColor` | `#bb9af7` | `#b8a4e8` |
| `Button.default.focusedBorderColor` | `#cba6f7` | `#c8b8f0` |
| `Button.focusedBorderColor` | `#bb9af7` | `#b8a4e8` |
| `TabbedPane.underlineColor` | `#bb9af7` | `#b8a4e8` |
| `TabbedPane.selected` | `#bb9af7` | `#b8a4e8` |
| `TabbedPane.hoverColor` | `#cba6f7` | `#c8b8f0` |
| `TabbedPane.focusColor` | `#bb9af7` | `#b8a4e8` |
| `ToolWindow.HeaderTab.underlineColor` | `#bb9af7` | `#b8a4e8` |
| `ToolWindow.Button.selectedBackground` | `#7c5cbf` | `#7060b0` |
| `Island.borderColor` | inherited / theme color | `#2c2f47` |
| `Borders.color` | inherited dark gray | `#3a3f5d` |
| `Separator.foreground` | inherited dark gray | `#3a3f5d` |
| `Component.borderColor` | inherited dark gray | `#3a3f5d` |
| `Component.disabledBorderColor` | inherited dark gray | `#343954` |
| `Component.focusColor` | `#bb9af780` | `#b8a4e880` |
| `Component.focusedBorderColor` | `#bb9af7` | `#b8a4e8` |
| `Component.hoverBorderColor` | inherited dark gray | `#414868` |
| `SearchMatch.startBackground` | inherited | `#b8a4e866` |
| `SearchMatch.endBackground` | inherited | `#b8a4e866` |
| `Editor.SearchField.background` | inherited / blended with editor | `#242840` |
| `Editor.SearchField.borderColor` | inherited | `#454b70` |
| `RadioButton.*Selected*` | `#bb9af7` | `#b8a4e8` |
| `ProgressBar.foreground` | `#bb9af7` | `#b8a4e8` |
| `ProgressBar.indeterminate.*` | `#bb9af7 / #cba6f7` | `#b8a4e8 / #c8b8f0` |
| `ToolTip.borderColor` | `#bb9af7` | `#b8a4e8` |
| `Checkbox.*Selected*` | `#bb9af7` | `#b8a4e8` |

Most `theme.json` panel/background keys follow the same `#2a2d3e→#2c2f47` substitution. Visible outer chrome is intentionally darker (`#20243a`) than the initial lifted chrome color (`#242840`).

### Editor Interaction Tuning (scheme XML)

| Role / key | Final color | Note |
|---|---|---|
| `CARET_ROW_COLOR` | `#25293f` | darker than editor background so the current row reads clearly |
| `SELECTION_BACKGROUND` | `#2d4f67` | unchanged from original palette |
| `SEARCH_RESULT_ATTRIBUTES` background | `#473f68` | stronger normal find match |
| `SEARCH_RESULT_ATTRIBUTES` border | `#8c7ec0` | boxed via `EFFECT_TYPE=0`, visible but not neon |
| `TEXT_SEARCH_RESULT_ATTRIBUTES` background | `#473f68` | same as normal find match |
| `TEXT_SEARCH_RESULT_ATTRIBUTES` border | `#8c7ec0` | boxed via `EFFECT_TYPE=0` |
| `WRITE_SEARCH_RESULT_ATTRIBUTES` background | `#365a78` | current / active find match |
| `WRITE_SEARCH_RESULT_ATTRIBUTES` border | `#85a7f5` | boxed via `EFFECT_TYPE=0`, intentionally more attention-grabbing |

### VCS Marker Tuning

| Role / keys | Final color | Note |
|---|---|---|
| Added gutter and file statuses | `#79ad7b` | softer green for `ADDED_LINES_COLOR`, `FILESTATUS_ADDED`, copied/external-added states |
| Modified gutter and file statuses | `#b79a67` | softer amber-brown for `MODIFIED_LINES_COLOR`, modified/hijacked/obsolete/not-changed states |
| Deleted / unknown / switched file statuses | `#c7778a` | softer rose-red, less distracting than syntax error pink |
| `GIT_TOOLBOX.CHANGED_COUNT_ATTRIBUTES` | `#b79a67` | matches modified marker family |

This supersedes the initial amber split for VCS markers only. Diagnostics, TODOs, CSS class names, events, format strings, diagrams, and similar warm non-parameter tokens continue to use `#c9a55a`.

### Islands Border Model

- Outer island border: `Island.borderColor` is set to `#2c2f47`, matching island/panel background so island outlines visually disappear against the darker outer chrome.
- Internal island borders/dividers: `Borders.color`, `Separator.foreground`, and `Component.borderColor` use `#3a3f5d`, a muted blue-lavender divider that fits the palette better than dark neutral gray.
- Disabled internal borders use `#343954`; hover internal borders use `#414868`.
- Do not make internal borders transparent: they provide necessary structure inside tool windows and editor panels.

---

## Implementation Scope

**Files to edit:**

1. `tokyo-night-silent-storm.theme.json` — background colors + accent color (`#bb9af7` → `#b8a4e8`)
2. `tokyo-night-silent-storm.xml` — all syntax/semantic attribute colors
3. `preview.html` — update CSS variables to reflect new palette

**Strategy:** global find-replace for most colors, but `#e0af68` (amber) is shared by both parameter tokens AND unrelated warm tokens (warnings, TODO, CSS class names, events, format strings, diagrams, and VCS markers). It must be handled in targeted passes — not a single global replace.

**Base substitution map** (safe first pass, followed by the overrides listed above):

| Find | Replace | Context |
|---|---|---|
| `22253a` | `242840` | base chrome hints; visible UI chrome is overridden to `#20243a` |
| `2a2d3e` | `2c2f47` | background (editor) |
| `303450` | `25293f` | caret row |
| `bb9af7` | `b8a4e8` | keywords + accent |
| `cba6f7` | `c8b8f0` | accent hover / lighter purple |
| `7aa2f7` | `85a7f5` | functions |
| `9ece6a` | `8fc472` | strings |
| `ff9e64` | `d4936a` | numbers |
| `2ac3de` | `4dc4d8` | types |
| `89ddff` | `7ab8d8` | operators |
| `f7768e` | `e07891` | HTML/XML tags |
| `6272a4` | `5e6590` | comments |

**Amber split — edit individually in `tokyo-night-silent-storm.xml`:**

Tokens that change to rose `#ccb0ba`:
- `DEFAULT_PARAMETER`, `DEFAULT_REASSIGNED_PARAMETER`
- `JS.PARAMETER`, `TS.TYPE_PARAMETER`
- `ANNOTATION_ATTRIBUTE_NAME_ATTRIBUTES`
- `IMPLICIT_ANONYMOUS_CLASS_PARAMETER_ATTRIBUTES`
- `HTTP_REQUEST_PARAMETER_NAME`
- `MESSAGE_ARGUMENT`

Tokens that change to softened amber `#c9a55a` (keep warm, just muted):
- Diagnostics: `WARNING_ATTRIBUTES`, `TYPO`
- Editor: `TODO_DEFAULT_ATTRIBUTES`, `CSS.CLASS_NAME`, `MARKDOWN_LINK_LABEL`, `MARKDOWN_STRIKETHROUGH`, `XPATH.KEYWORD`, `MACRONAME`
- ReSharper: `ReSharper.EVENT_IDENTIFIER`, `ReSharper.FORMAT_STRING_ITEM`, `ReSharper.MATCHED_FORMAT_STRING_ITEM`
- Diagrams: `DIAGRAM_GENERALIZATION_EDGE`, `DIAGRAM_HOT_SPOTS`

VCS markers use the softer dedicated set from **VCS Marker Tuning** instead of `#c9a55a`.

**New token (local variables):** `#a0c5e9` — set on `DEFAULT_LOCAL_VARIABLE`, `DEFAULT_REASSIGNED_LOCAL_VARIABLE`, `ReSharper.MUTABLE_LOCAL_VARIABLE_IDENTIFIER`, `JS.LOCAL_VARIABLE`, `JS.INSTANCE_MEMBER_VARIABLE` (currently all inherit foreground).

---

## Preview HTML

Update CSS variables at the top of `preview.html` to reflect all final palette values, including `--border-inner`, caret row, search match colors, and the darker outer chrome. No structural changes to the preview content needed.
