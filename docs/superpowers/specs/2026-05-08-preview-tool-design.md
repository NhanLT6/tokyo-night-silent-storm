# Preview Tool Design

**Date:** 2026-05-08
**Status:** Approved

## Overview

A self-contained `preview.html` that replaces the deleted version. Opens directly in a browser — no server, no build step. Shows Nebula Haze syntax highlighting across all supported languages with a live inspector: click any colored token to see its XML token name, palette slot, and current hex, then edit the value in-place to see the change instantly. A changes panel tracks the diff so edits can be handed back for XML application.

---

## Architecture

### Two-layer color model

Mirrors PALETTE.md exactly:

1. **Palette layer** — a JS object mapping palette slot names to hex values:
   ```js
   const PALETTE = {
     'blue-dim': '#7494c8',
     'blue-mid': '#8aabe6',
     'blue-bright': '#a5bcf0',
     'violet-whisper': '#c2c0e8',
     // ... all slots
   }
   ```

2. **Token layer** — a JS object mapping XML token names to their palette slot:
   ```js
   const TOKEN_SLOTS = {
     KEYWORD: 'violet-mid',
     STRING: 'green-bright',
     CLASS_NAME: 'violet-bright',
     // ... all tokens
   }
   ```

Color resolution: `PALETTE[TOKEN_SLOTS[tokenName]]`. Both layers live at the top of the file as plain JS constants — swapping an entire palette means replacing only the `PALETTE` object.

### CSS custom properties

On load (and after any edit), JS writes all resolved colors into CSS custom properties on `:root`:

```css
:root {
  --token-keyword: #c498ff;
  --token-string: #88dda0;
  /* ... */
}
```

Each `<span>` in the code samples uses `color: var(--token-keyword)` etc. Updating a property updates every span that references it — no DOM walk needed.

### Code samples

Hand-authored HTML spans — no runtime tokenizer. Each span carries:
- `class="t"` — makes it clickable
- `data-token="KEYWORD"` — maps to TOKEN_SLOTS key
- `style="color: var(--token-keyword)"` — or equivalent CSS class

Languages: **C#, TypeScript, TSX/React, Vue, HTML/CSS, JSON, SQL**. Samples are representative, not exhaustive — enough lines to exercise every token type at least once (keywords, class names, functions, parameters, strings, numbers, constants, interfaces, annotations, operators, comments, type params).

---

## Layout

Fixed two-panel layout. No responsive breakpoints needed — this is a dev tool opened on a desktop.

### Left sidebar (230px, fixed)

Three sections stacked top-to-bottom, sidebar scrolls if needed:

**1. Palette**

Seven hue families, each row: `family-name | swatches`. Swatch order within each family: **dim → mid → bright → whisper** (whisper last, as it's the softest and least-used variant). Orange is a singleton. Clicking a swatch opens the inspector focused on that palette slot rather than a specific token.

**2. Inspector** (always visible, empty state when nothing selected)

Appears populated when a token span or palette swatch is clicked:
- Token name (XML key, e.g. `KEYWORD`) — omitted when clicking a swatch directly
- Palette slot (`violet-mid`)
- Color swatch dot + hex input (editable)
- "Also used by" note listing other tokens that resolve to the same palette slot

Editing the hex and pressing Enter (or blurring) records the change and immediately updates all `--token-*` CSS vars that resolve through that palette slot. Edits are always slot-level — changing `violet-mid` updates every token mapped to it (keyword, predefined symbol, delegate, etc.).

**3. Changes panel** (hidden when no changes)

Appears as soon as `changes.length > 0`:
- Header: `● N pending` + **Undo (↩) / Redo (↪)** buttons
- Per-change row: palette slot name | old swatch | → | new swatch | new hex | ✕ revert
- Footer actions: **Copy diff** | **Clear all**

### Right main area (flex: 1)

- Language tab bar at top (C# | TypeScript | TSX | Vue | HTML/CSS | JSON | SQL)
- Code area below: monospace font, theme background (`#21243a`), padded
- Active token span gets a subtle `outline: 2px solid #a5bcf0` ring when selected

---

## Undo / Redo

```
changes: [change₀, change₁, change₂]   ← array of { token, slotOrToken, oldHex, newHex }
cursor:  3                               ← index = length means "at head"
```

- **New edit:** slice `changes` to `cursor`, push new change, advance cursor. This discards any undone items.
- **Undo:** cursor--, revert the change at the new cursor position in CSS vars.
- **Redo:** apply change at cursor, cursor++.
- **✕ on a row:** removes that specific entry from the array and adjusts cursor. Reverts that token to its previous state (or original if it was the only edit for that token).
- **Clear all:** empty array, cursor = 0, reload all CSS vars from original PALETTE.

The `changes` array items store `{ slot, oldHex, newHex }` — always keyed by palette slot name since all edits are slot-level.

---

## Copy Diff Format

Copies to clipboard as plain text — formatted for easy paste into the terminal:

```
violet-mid:   #c498ff → #b87cf0
green-bright: #88dda0 → #96cc9e
```

One line per change, slot name left-padded to align arrows.

---

## Languages & Token Coverage

| Language | Key tokens exercised |
|---|---|
| C# | keyword, class, interface, function, parameter, string, number, constant, annotation, operator, comment, type param |
| TypeScript | keyword, class, function, parameter, string, number, type param, interface, decorator |
| TSX/React | JSX tag name, JSX attribute, JS keyword, string, expression |
| Vue | Vue tag (`<template>`, `<script>`, `<style>`), HTML attr, CSS prop/value, JS keyword |
| HTML/CSS | tag name, attribute, CSS property, CSS value, string, entity |
| JSON | property key, string, number, keyword (true/false/null) |
| SQL | keyword, function, string, number, identifier |

---

## Typography

| Context | Size |
|---|---|
| Code area (monospace) | 14px |
| Sidebar section labels | 10px, uppercase |
| Inspector slot name | 13px |
| Inspector "Also used by" note | 11px |
| Change row slot names / hex values | 10–11px |
| Language tabs | 12px |

UI base (sidebar, tabs, labels): 16px system font. Code line-height: 1.75.

---

## File structure

Single file: `preview.html`. All CSS and JS inline. No external dependencies. Opens by double-click.

Internal structure:
1. `<style>` block — layout, fixed structural styles (not token colors)
2. `<script>` block (top) — `PALETTE`, `TOKEN_SLOTS`, and `applyPalette()` function
3. HTML body — sidebar + code area
4. `<script>` block (bottom) — event wiring, undo/redo state, copy logic

Token colors are never hardcoded in HTML or CSS — always resolved through `var(--token-*)` properties set by `applyPalette()`.
