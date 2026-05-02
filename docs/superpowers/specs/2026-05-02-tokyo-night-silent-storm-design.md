# Tokyo Night Silent Storm — Design Spec

**Date:** 2026-05-02  
**Author:** Nhan Le

## Overview

A JetBrains Rider theme based on Tokyo Night Storm with a softer "Silent Storm" twist: slightly lighter and warmer backgrounds to reduce harsh contrast in daylight, official Storm syntax colors kept intact, distributed as a `.jar` plugin.

Goals:
- Expand Islands Dark, not fight it — minimal `theme.json`, trust Islands Dark defaults for chrome behavior
- Full Rider semantic highlighting (ReSharper tokens) that VS Code themes lack
- Simple static `preview.html`, no build pipeline for the preview
- Phase-in approach: minimal first, add keys only after failing a visual test in Rider

## Project Structure

```
tokyo-night-silent-storm/
  META-INF/plugin.xml
  tokyo-night-silent-storm.theme.json
  tokyo-night-silent-storm.xml
  preview.html
  build.js
  package.json
  releases/
```

No `shiki/` directory. Preview is a checked-in static file edited by hand.

## Parent Theme Strategy

- `theme.json` → `"parentTheme": "Islands Dark"`
- `editor.xml` → `parent_scheme="Darcula"`
- `theme.json` starts with only backgrounds, accent, selection, and foreground
- No tab/border/chrome micromanagement — Islands Dark owns those
- Accent `#7aa2f7` (Storm blue) cascades to active tab indicator, focus rings, default buttons

## Palette

### Backgrounds

| Role | Color |
|---|---|
| Main window / chrome | `#22253a` |
| Editor / panel background | `#2a2d3e` |
| Caret row | `#303450` |
| Selection | `#2d4f67` |

### Syntax

| Role | Color | Style |
|---|---|---|
| Foreground / identifiers | `#c0caf5` | |
| Keywords | `#bb9af7` | italic |
| Functions / methods | `#7aa2f7` | |
| Strings | `#9ece6a` | |
| Numbers | `#ff9e64` | |
| Types / classes | `#2ac3de` | |
| Enums / structs | `#73daca` | |
| Comments | `#565f89` | italic |
| Operators / punctuation | `#89ddff` | |
| Parameters | `#e0af68` | |
| Namespace | `#c0caf5` | (quiet, foreground) |

### Rider Semantic Tokens (ReSharper)

| Token | Color | Style |
|---|---|---|
| `ReSharper.STRUCT_IDENTIFIER` | `#73daca` | |
| `ReSharper.ENUM_IDENTIFIER` | `#73daca` | |
| `ReSharper.ENUM_MEMBER_IDENTIFIER` | `#73daca` | |
| `ReSharper.DELEGATE_IDENTIFIER` | `#bb9af7` | italic |
| `ReSharper.EVENT_IDENTIFIER` | `#e0af68` | |
| `ReSharper.EXTENSION_METHOD_IDENTIFIER` | `#7aa2f7` | italic |
| `ReSharper.TYPE_PARAMETER_IDENTIFIER` | `#2ac3de` | |
| `ReSharper.MUTABLE_LOCAL_VARIABLE_IDENTIFIER` | `#c0caf5` | underline |
| `ReSharper.FORMAT_STRING_ITEM` | `#e0af68` | |
| `ReSharper.STATIC_CLASS_IDENTIFIER` | `#2ac3de` | italic |
| `ReSharper.NAMESPACE_IDENTIFIER` | `#c0caf5` | |
| `CSHARP_OPERATOR_SIGN` | `#89ddff` | |

### Inlay Hints (dimmer than comments)

| Token | Foreground | Background |
|---|---|---|
| `INLAY_DEFAULT` | `#414868` | `#22253a` |
| `INLAY_TEXT_WITHOUT_BACKGROUND` | `#3b3f5c` | — |

## Languages Covered

C#, HTML, Razor (.cshtml), JSON, XML, YAML — same scope as cyan-harbor-theme.

## Preview HTML

Single `preview.html`, open directly in browser. Single-column layout:
1. IDE chrome mockup (toolbar, tab bar with active/inactive tabs, panel, status bar)
2. Code cards stacked vertically, one per language
3. CSS variables at the top — one variable per palette color for easy updates

Every styled token must appear at least once in the code samples.

## Build

`build.js` — packages theme files into `releases/tokyo-night-silent-storm-x.x.x.jar`. Version read from `package.json`. Run with `node build.js`.
