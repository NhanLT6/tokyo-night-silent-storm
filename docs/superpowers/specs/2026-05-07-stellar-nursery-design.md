# Stellar Nursery — Color Direction Spec

**Date:** 2026-05-07  
**Status:** Approved for implementation  
**Builds on:** `docs/superpowers/specs/2026-05-07-palette-system-design.md`

---

## Summary

Push Nebula Haze from "safe neutral pastel" toward the visual energy of a real nebula —
vivid star-forming regions blazing against cold deep-space darkness — without sacrificing
comfort for long coding sessions or office/daylight use.

Key constraints that shaped every decision:
- Background stays near `#21243a` (comfortable mid-dark navy, not abyss-black)
- Teal/cyan handled conservatively — high eye sensitivity, fatigue risk
- Pink (HTML tag names) appears ~7/10 as often as C# class syntax — treat carefully
- Primary stack: C#, TypeScript, React, Vue — all must look good

---

## Design Decisions

### 1. Cold Anchor — Blue + Teal Locked

Blue and teal families are **unchanged**. They cover the most frequently seen tokens
(functions, methods, parameters, constants) and serve as the "cold deep-space field"
that the nebula accents blaze against.

| Token | Color | Notes |
|-------|-------|-------|
| Function / method calls | `#8aabe6` blue-mid | Also JSX/Vue component names (see §4) |
| Parameters | `#8fd4c8` teal-bright | Also HTML/XML/JSX/Vue attribute names (see §4) |
| Constants, enum members | `#6ec4b6` teal-mid | Unchanged |

### 2. Violet Family — Boosted (+20% S)

Keywords and type names are the semantic events in a line of code. Boosting their
saturation makes them feel like star-formation events against the blue function sea.
Controlled drama — vivid, not neon.

| Token | Before | After | Delta |
|-------|--------|-------|-------|
| Keywords (`class`, `if`, `const`, `async`, ...) | `#b09ce8` | `#c498ff` | S 62→82% |
| Class names, type names, type parameters | `#c9b6ee` | `#dbbeff` | S 52→72% |
| Violet-dim (template variables) | `#9480c8` | unchanged | — |

### 3. Green Family — Lifted

Strings and interface declarations get a modest saturation lift. Strings are the
"background luminosity" of a nebula — they should glow gently, not whisper.

| Token | Before | After | Delta |
|-------|--------|-------|-------|
| String literals, CSS values, module names | `#9fd4ae` | `#88dda0` | S 40→56%, slightly more vivid |
| Interface declarations | `#8ab896` | `#96cc9e` | small lift |

### 4. Markup Semantic Remap — The Core Structural Change

The biggest conceptual shift. Previous pink-for-tags / blue-for-attributes
created a warm/cool temperature clash on every JSX/HTML line. The new model
maps colors to *semantic role* rather than syntax category:

**JSX/Vue component names → blue-mid `#8aabe6`**  
Components appear far more often than raw HTML tags in React/Vue work. They compile
to function calls — `<Badge>` is `createElement(Badge, ...)`. Using function/method
blue is semantically accurate and keeps the most-seen element comfortable.

**HTML/XML attribute names → teal-bright `#8fd4c8`**  
Attributes are named parameters. Teal-bright is already the parameter color for
function calls. Reusing it for attributes unifies the "parameter" concept across
call styles (parens vs JSX props).

**HTML/XML tag names → hot rose `#e888c0`**  
HTML primitives (`div`, `span`, `template`, `script`) are rare structural scaffolding
in React/Vue-heavy work (~3/10 frequency vs C# classes). Being rare, they can afford
to blaze. Hot rose is vivid and distinct without clashing with teal attributes
(different temperature zone) or blue components (different family entirely).

This supersedes the previous pink-mid role. Pink-mid hex changes from `#cc8ea5`
to `#e888c0`.

### 5. Comments — Receded

Comments dimmed one step so code structure surfaces more clearly against them.

| Token | Before | After |
|-------|--------|-------|
| Comments | `#7880a8` | `#606480` |

---

## Complete Hex Delta

| Family | Level | Before | After | Used for |
|--------|-------|--------|-------|---------|
| Violet | mid | `#b09ce8` | `#c498ff` | Keywords |
| Violet | bright | `#c9b6ee` | `#dbbeff` | Class/type names |
| Green | mid | `#8ab896` | `#96cc9e` | Interface declarations |
| Green | bright | `#9fd4ae` | `#88dda0` | Strings |
| Pink | mid | `#cc8ea5` | `#e888c0` | HTML/XML/CSS/Vue tag names |
| — | comments | `#7880a8` | `#606480` | Comments |
| HTML attrs | — | `#8aabe6` → `#8fd4c8` | targeted | Attribute names only |
| JSX components | — | `#c9b6ee` → `#8aabe6` | targeted | JSX/Vue component tag names |

---

## What Does NOT Change

- Background `#21243a`
- Plain text `#c0caf5`
- Blue family (all levels) — cold anchor
- Teal family (all levels) — cold anchor  
- Violet dim `#9480c8`
- Orange `#e09a68` — operators
- Sand family — numbers
- Diagnostic colors (errors, warnings)
- Pink bright `#e0aabf` — git-deleted gutter

---

## Governance Notes

- `#e888c0` is a new hex for pink-mid. Update PALETTE.md accordingly.
- HTML attribute names now map to teal-bright rather than blue-mid. Update the
  "Used for" column in PALETTE.md for both blue-mid and teal-bright.
- The "no new hue families" rule is respected — hot rose is still the pink family
  (H~321°), just more saturated and slightly hue-shifted toward magenta.
