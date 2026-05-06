# Nebula Haze — Color Refinements

**Date:** 2026-05-06
**Author:** Nhan Le
**Amends:** `2026-05-05-nebula-haze-design.md`

## Overview

Six targeted color adjustments to the Nebula Haze theme. None of these change the theme's identity or philosophy — they sharpen readability and reduce visual noise that emerged during real use.

---

## Changes

### 1. Class / Type — Soft Amethyst

| Token group | Old | New |
|---|---|---|
| `DEFAULT_CLASS_NAME`, `ABSTRACT_CLASS_NAME_ATTRIBUTES`, `Abstract class name`, `DEFAULT_INTERFACE_NAME`, `DEFAULT_CLASS_REFERENCE`, `TYPEDEF` | `b1d0e6` | `cabae4` |
| JS: `JS.GLOBAL_FUNCTION` | `b1d0e6` | `cabae4` |
| TS: `TS.PRIM_TYPE` | `b1d0e6` | `cabae4` |
| Scala: `Scala Predefined types` | `b1d0e6` | `cabae4` |
| ReSharper: `TYPE_PARAMETER_IDENTIFIER`, `STATIC_CLASS_IDENTIFIER`, `ASP_NET_DIRECTIVE_NAME`, `ASP_NET_MVC_VIEW_COMPONENT` | `b1d0e6` | `cabae4` |

**Why:** `#b1d0e6` (ice blue) sat too close to local variable `#a0c5e9` and foreground `#c0caf5` — all three in the same blue band, making types indistinguishable at a glance.

**New value:** `#cabae4` — hsl(268, 48%, 81%). Soft violet, occupying its own hue band clearly distinct from the blue local var, lavender foreground, and function blue. Lighter and more muted than keyword violet `#b09ce8` so the two don't clash.

---

### 2. Operators / Punctuation — Solar Wind

| Token group | Old | New |
|---|---|---|
| `DEFAULT_OPERATION_SIGN`, `DEFAULT_BRACES`, `DEFAULT_BRACKETS`, `DEFAULT_PARENTHS`, `DEFAULT_COMMA`, `DEFAULT_DOT`, `DEFAULT_SEMICOLON`, `Closure braces`, `CSHARP_OPERATOR_SIGN` | `7ab8d8` | `e09a68` |
| `CSS.COLOR`, `HTTP_REQUEST_PORT` | `7ab8d8` | `e09a68` |
| `IGNORE.BRACKET`, `IGNORE.NEGATION` | `7ab8d8` | `e09a68` |

**Excluded from this change** (keep `7ab8d8` cold plasma):
- `DEFAULT_VALID_STRING_ESCAPE` — part of string syntax, not an operator
- `CONSOLE_USER_INPUT` — terminal UI, not editor syntax
- `CUSTOM_KEYWORD4_ATTRIBUTES` — keyword family
- `YAML_SCALAR_LIST` — structured data, not operator
- `JS.IF_ELSE`, `JS.MODULE_KEYWORD`, `JS.TRY_CATCH`, `JS.YIELD` — JS keyword variants, should align with keyword color (`b09ce8`), not operator orange
- `MARKDOWN_LINK_DEFINITION` — markdown structure, not operator

**Why:** Operators were the same cold blue as the rest of the syntax family — no visual energy. Making them warm makes operators feel like "active connective tissue" between cold structural tokens.

**New value:** `#e09a68` — hsl(28, 65%, 64%). Solar Wind orange. Hot but not red (error is `#c7778a`). Clearly distinct from number gold `#d8c383` and param salmon `#c6afa9`.

---

### 3. Editor Background — Slightly Darker

| Key | Old | New |
|---|---|---|
| All occurrences of `22253a` in `nebula-haze.theme.json` and `nebula-haze.xml` | `22253a` | `1e2235` |

**Why:** The editor background was catching the eye — slightly too light relative to the code surface. Darkening it helps it recede so syntax tokens command attention instead.

**Note:** All associated backgrounds that were derived from `22253a` (ToolWindow headers, EditorTabs, etc.) shift together via global replace. Chrome (`1a1d30`) and floating (`13152a`) backgrounds are unchanged.

---

### 4. Keywords — Cleaner Violet

| Token group | Old | New |
|---|---|---|
| All `DEFAULT_KEYWORD` occurrences and keyword-derived tokens | `afa4e5` | `b09ce8` |
| JS keyword variants: `JS.IF_ELSE`, `JS.MODULE_KEYWORD`, `JS.TRY_CATCH`, `JS.YIELD` | `7ab8d8` (was using cold plasma) | `b09ce8` |

**Why:** `#afa4e5` read as blue-purple (hsl ~248°). Shifting to `#b09ce8` (hsl 265°) anchors keywords firmly in violet — clearly distinct from the blue function/local-var family and the space blue UI accent `#84afeb`.

**New value:** `#b09ce8` — hsl(265, 60%, 76%).

---

### 5. Comments — Lifted Above Inlay Hints

| Token | Old | New |
|---|---|---|
| `DEFAULT_LINE_COMMENT`, `DEFAULT_BLOCK_COMMENT`, `DEFAULT_DOC_COMMENT` and related | `5e6590` | `7880a8` |

**Excluded:** `INLAY_DEFAULT`, `INLAY_TEXT_WITHOUT_BACKGROUND` — stay at `565f89`.

**Why:** Comments (`#5e6590`, hsl 234 21% 47%) and inlay hints (`#565f89`, hsl 234 22% 40%) were only 7% lightness apart — visually indistinguishable. Comments should read as intentional author notes, not IDE decorations.

**New value:** `#7880a8` — hsl(232, 23%, 57%). 17% brighter than inlay hints, clearly readable as authored text while still clearly dim compared to active syntax.

---

### 6. Git Modified — Sand Gold (Dimmed)

| Token | Old | New |
|---|---|---|
| `MODIFIED_LINES_COLOR`, `WHITESPACES_MODIFIED_LINES_COLOR` (gutter) | `bba586` | `a89e5c` |
| `FILESTATUS_MODIFIED`, `FILESTATUS_HIJACKED`, `FILESTATUS_OBSOLETE`, `FILESTATUS_NOT_CHANGED_IMMEDIATE`, `FILESTATUS_NOT_CHANGED_RECURSIVE`, `FILESTATUS_modifiedOutside` | `bba586` | `a89e5c` |
| `GIT_TOOLBOX.CHANGED_COUNT_ATTRIBUTES` | `bba586` | `a89e5c` |
| `Tree.modifiedItemForeground` (theme.json) | `bba586` | `a89e5c` |

**Why:** The previous amber `#bba586` (hsl 35°) read too warm and attention-grabbing. The proposal `#c4b86c` shifted hue to sandy gold (48°) but was too bright. Final value reduces saturation and lightness to keep the sandy-gold direction without competing with code focus.

**New value:** `#a89e5c` — hsl(48, 30%, 51%). Sandy yellow-gold, muted enough to recede into the gutter. Hue is clearly sandy rather than amber; saturation (30%) matches the original amber's character (28%) at a cooler hue.

---

## Full Delta Summary

| # | Token family | Old | New | HSL |
|---|---|---|---|---|
| 1 | Class / type | `b1d0e6` | `cabae4` | hsl(268, 48%, 81%) |
| 2 | Operators / punctuation | `7ab8d8` | `e09a68` | hsl(28, 65%, 64%) |
| 3 | Editor background | `22253a` | `1e2235` | — |
| 4 | Keywords | `afa4e5` | `b09ce8` | hsl(265, 60%, 76%) |
| 4b | JS keyword variants | `7ab8d8` | `b09ce8` | same as keywords |
| 5 | Comments | `5e6590` | `7880a8` | hsl(232, 23%, 57%) |
| 6 | Git modified | `bba586` | `a89e5c` | hsl(48, 30%, 51%) |

### 7. Line Numbers — Visible

| Key | Old | New |
|---|---|---|
| `LINE_NUMBERS_COLOR` | `2a2e48` | `454d74` |
| `GUTTER_BACKGROUND` | `22253a` | `1e2235` |

**Why:** `#2a2e48` against the `#22253a` background (now `#1e2235`) had near-zero contrast — line numbers were invisible. Gutter background updated to match the new editor background.

**New value:** `#454d74` — hsl(234, 25%, 37%). Readable at a glance, clearly secondary to syntax tokens. `LINE_NUMBER_ON_CARET_ROW_COLOR` stays `#737aa2` (brighter, marks the active line).

---

## Files Affected

- `nebula-haze.xml` — syntax tokens (changes 1, 2, 4, 5, 6)
- `nebula-haze.theme.json` — UI keys (changes 3, 6)
