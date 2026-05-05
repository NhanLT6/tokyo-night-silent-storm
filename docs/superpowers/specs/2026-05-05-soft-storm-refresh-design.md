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
| Chrome / main window | `#22253a` | `#242840` |
| Editor / panels | `#2a2d3e` | `#2c2f47` |
| Caret row | `#303450` | `#333758` |
| Selection | `#2d4f67` | `#2d4f67` *(unchanged)* |

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
| `MainWindow.background` | `#22253a` | `#242840` |
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
| `Component.focusColor` | `#bb9af780` | `#b8a4e880` |
| `Component.focusedBorderColor` | `#bb9af7` | `#b8a4e8` |
| `RadioButton.*Selected*` | `#bb9af7` | `#b8a4e8` |
| `ProgressBar.foreground` | `#bb9af7` | `#b8a4e8` |
| `ProgressBar.indeterminate.*` | `#bb9af7 / #cba6f7` | `#b8a4e8 / #c8b8f0` |
| `ToolTip.borderColor` | `#bb9af7` | `#b8a4e8` |
| `Checkbox.*Selected*` | `#bb9af7` | `#b8a4e8` |

All other `theme.json` keys (background colors) follow the same `#22253a→#242840` / `#2a2d3e→#2c2f47` substitution.

---

## Implementation Scope

**Files to edit:**

1. `tokyo-night-silent-storm.theme.json` — background colors + accent color (`#bb9af7` → `#b8a4e8`)
2. `tokyo-night-silent-storm.xml` — all syntax/semantic attribute colors
3. `preview.html` — update CSS variables to reflect new palette

**Strategy:** global find-replace for most colors, but `#e0af68` (amber) is shared by both parameter tokens AND unrelated tokens (VCS indicators, warnings, TODO, CSS class names, events, format strings). It must be handled in two passes — not a single global replace.

**Global substitution map** (safe to replace everywhere):

| Find | Replace | Context |
|---|---|---|
| `22253a` | `242840` | background (chrome) |
| `2a2d3e` | `2c2f47` | background (editor) |
| `303450` | `333758` | caret row |
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
- VCS: `MODIFIED_LINES_COLOR`, `FILESTATUS_MODIFIED`, `FILESTATUS_HIJACKED`, `FILESTATUS_OBSOLETE`, `FILESTATUS_NOT_CHANGED_IMMEDIATE`, `FILESTATUS_NOT_CHANGED_RECURSIVE`, `FILESTATUS_addedOutside`
- Diagnostics: `WARNING_ATTRIBUTES`, `TYPO`
- Editor: `TODO_DEFAULT_ATTRIBUTES`, `CSS.CLASS_NAME`, `MARKDOWN_LINK_LABEL`, `MARKDOWN_STRIKETHROUGH`, `XPATH.KEYWORD`, `MACRONAME`
- ReSharper: `ReSharper.EVENT_IDENTIFIER`, `ReSharper.FORMAT_STRING_ITEM`, `ReSharper.MATCHED_FORMAT_STRING_ITEM`
- Diagrams: `DIAGRAM_GENERALIZATION_EDGE`, `DIAGRAM_HOT_SPOTS`
- Git Toolbox: `GIT_TOOLBOX.CHANGED_COUNT_ATTRIBUTES`

**New token (local variables):** `#a0c5e9` — set on `DEFAULT_LOCAL_VARIABLE`, `DEFAULT_REASSIGNED_LOCAL_VARIABLE`, `ReSharper.MUTABLE_LOCAL_VARIABLE_IDENTIFIER`, `JS.LOCAL_VARIABLE`, `JS.INSTANCE_MEMBER_VARIABLE` (currently all inherit foreground).

---

## Preview HTML

Update CSS variables at the top of `preview.html` to reflect all new values. No structural changes to the preview needed.
