# Nebula Haze Color Refinements Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Apply six targeted color adjustments to `nebula-haze.xml` and `nebula-haze.theme.json` as defined in the design spec.

**Architecture:** Pure find-and-replace editing on two theme files. Safe global replaces where a hex value is used exclusively for one token family; targeted edits where a value is shared across token families with different destinations. Line numbers are already fixed (committed separately).

**Tech Stack:** XML, JSON — no build step needed to verify. Load theme in Rider or open `preview.html` in a browser to confirm visually.

---

## Files Modified

| File | Changes |
|---|---|
| `nebula-haze.xml` | All syntax token changes (tasks 1–6) |
| `nebula-haze.theme.json` | Background + git modified UI keys (tasks 1, 5) |

---

### Task 1: Editor Background — `#22253a` → `#1e2235`

Global replace. This hex appears exclusively as the editor/panel/widget background in both files.

**Files:**
- Modify: `nebula-haze.theme.json` (13 occurrences)
- Modify: `nebula-haze.xml` (21 occurrences — console BG, hints, scrollbars, diagrams, etc.)

- [ ] **Step 1: Replace in theme.json**

  In `nebula-haze.theme.json`, replace all `#22253a` with `#1e2235`.

  Verify count before replacing — expect **13 occurrences**:
  ```bash
  grep -c "22253a" nebula-haze.theme.json
  ```
  Expected output: `13`

  Apply:
  ```bash
  sed -i 's/#22253a/#1e2235/g' nebula-haze.theme.json
  ```

- [ ] **Step 2: Replace in XML**

  In `nebula-haze.xml`, replace all `22253a` (no `#` prefix in XML values) with `1e2235`.

  Verify count:
  ```bash
  grep -c "22253a" nebula-haze.xml
  ```
  Expected output: `21`

  Apply:
  ```bash
  sed -i 's/22253a/1e2235/g' nebula-haze.xml
  ```

- [ ] **Step 3: Verify no `22253a` remains**

  ```bash
  grep -c "22253a" nebula-haze.xml nebula-haze.theme.json
  ```
  Expected: both return `0`.

- [ ] **Step 4: Commit**

  ```bash
  git add nebula-haze.xml nebula-haze.theme.json
  git commit -m "Darken editor background 22253a → 1e2235"
  ```

---

### Task 2: Keywords — `#afa4e5` → `#b09ce8`

Global replace. `afa4e5` is used exclusively for keyword tokens in `nebula-haze.xml`. Does not appear in `theme.json`.

**Files:**
- Modify: `nebula-haze.xml`

- [ ] **Step 1: Verify count**

  ```bash
  grep -c "afa4e5" nebula-haze.xml
  ```
  Expected: multiple (all keyword tokens). If it appears in `theme.json`, investigate before replacing.

  ```bash
  grep -c "afa4e5" nebula-haze.theme.json
  ```
  Expected: `0`

- [ ] **Step 2: Replace**

  ```bash
  sed -i 's/afa4e5/b09ce8/g' nebula-haze.xml
  ```

- [ ] **Step 3: Verify**

  ```bash
  grep -c "afa4e5" nebula-haze.xml
  ```
  Expected: `0`

  ```bash
  grep -c "b09ce8" nebula-haze.xml
  ```
  Expected: matches previous count of `afa4e5`.

- [ ] **Step 4: Commit**

  ```bash
  git add nebula-haze.xml
  git commit -m "Shift keywords from blue-purple afa4e5 to violet b09ce8"
  ```

---

### Task 3: Class / Type — `#b1d0e6` → `#cabae4`

Global replace. `b1d0e6` is used exclusively for class/type/interface tokens in `nebula-haze.xml`.

**Files:**
- Modify: `nebula-haze.xml`

- [ ] **Step 1: Verify count and exclusivity**

  ```bash
  grep -c "b1d0e6" nebula-haze.xml
  grep -c "b1d0e6" nebula-haze.theme.json
  ```
  Expected: several in XML, `0` in theme.json.

- [ ] **Step 2: Replace**

  ```bash
  sed -i 's/b1d0e6/cabae4/g' nebula-haze.xml
  ```

- [ ] **Step 3: Verify**

  ```bash
  grep -c "b1d0e6" nebula-haze.xml
  ```
  Expected: `0`

- [ ] **Step 4: Commit**

  ```bash
  git add nebula-haze.xml
  git commit -m "Shift class/type from ice blue b1d0e6 to soft amethyst cabae4"
  ```

---

### Task 4: Comments — `#5e6590` → `#7880a8`

Global replace. `5e6590` appears only in the four comment token entries in `nebula-haze.xml`. Inlay hints use the distinct value `565f89` and are unaffected.

**Files:**
- Modify: `nebula-haze.xml`

- [ ] **Step 1: Verify count and distinguish from inlay hints**

  ```bash
  grep -c "5e6590" nebula-haze.xml
  grep -c "565f89" nebula-haze.xml
  ```
  Expected: `5e6590` appears 4 times (line comment, block comment, doc comment, doc markup). `565f89` count is separate — do not touch.

- [ ] **Step 2: Replace**

  ```bash
  sed -i 's/5e6590/7880a8/g' nebula-haze.xml
  ```

- [ ] **Step 3: Verify inlay hints untouched**

  ```bash
  grep -c "5e6590" nebula-haze.xml   # expect 0
  grep -c "565f89" nebula-haze.xml   # expect same as before step 2
  grep -c "7880a8" nebula-haze.xml   # expect 4
  ```

- [ ] **Step 4: Commit**

  ```bash
  git add nebula-haze.xml
  git commit -m "Lift comment color 5e6590 → 7880a8, distinct from inlay hints"
  ```

---

### Task 5: Git Modified — `#bba586` → `#a89e5c`

Global replace across both files. `bba586` is used exclusively for "modified" VCS state.

**Files:**
- Modify: `nebula-haze.xml`
- Modify: `nebula-haze.theme.json`

- [ ] **Step 1: Verify counts**

  ```bash
  grep -c "bba586" nebula-haze.xml
  grep -c "bba586" nebula-haze.theme.json
  ```
  Expected: several in XML (gutter, filestatus, GitToolbox), 1 in theme.json (`Tree.modifiedItemForeground`).

- [ ] **Step 2: Replace in both files**

  ```bash
  sed -i 's/bba586/a89e5c/g' nebula-haze.xml
  sed -i 's/#bba586/#a89e5c/g' nebula-haze.theme.json
  ```

- [ ] **Step 3: Verify**

  ```bash
  grep -c "bba586" nebula-haze.xml nebula-haze.theme.json
  ```
  Expected: both `0`.

- [ ] **Step 4: Commit**

  ```bash
  git add nebula-haze.xml nebula-haze.theme.json
  git commit -m "Shift git-modified from amber bba586 to sand gold a89e5c"
  ```

---

### Task 6: Operators — `#7ab8d8` → `#e09a68` (targeted)

`7ab8d8` is shared across many token families. **Do not global replace.** Strategy: global replace all, then restore exceptions.

**Files:**
- Modify: `nebula-haze.xml`

**Tokens that SHOULD become `e09a68` (Solar Wind orange — operators/punctuation):**
`DEFAULT_OPERATION_SIGN`, `DEFAULT_BRACES`, `DEFAULT_BRACKETS`, `DEFAULT_PARENTHS`, `DEFAULT_COMMA`, `DEFAULT_DOT`, `DEFAULT_SEMICOLON`, `Closure braces`, `CSHARP_OPERATOR_SIGN`, `CSS.COLOR`, `HTTP_REQUEST_PORT`, `IGNORE.BRACKET`, `IGNORE.NEGATION`

**Tokens that stay `7ab8d8` (cold plasma — not operator syntax):**
`DEFAULT_VALID_STRING_ESCAPE`, `CONSOLE_USER_INPUT`, `CUSTOM_KEYWORD4_ATTRIBUTES`, `YAML_SCALAR_LIST`, `MARKDOWN_LINK_DEFINITION`

**Tokens that become `b09ce8` (keyword violet — JS keyword variants):**
`JS.IF_ELSE`, `JS.MODULE_KEYWORD`, `JS.TRY_CATCH`, `JS.YIELD`

- [ ] **Step 1: Record baseline count of `7ab8d8`**

  ```bash
  grep -c "7ab8d8" nebula-haze.xml
  ```
  Save this number — call it `TOTAL`.

- [ ] **Step 2: Global replace all `7ab8d8` → `e09a68`**

  ```bash
  sed -i 's/7ab8d8/e09a68/g' nebula-haze.xml
  ```

  Verify:
  ```bash
  grep -c "7ab8d8" nebula-haze.xml   # expect 0
  grep -c "e09a68" nebula-haze.xml   # expect TOTAL
  ```

- [ ] **Step 3: Restore cold-plasma exceptions to `7ab8d8`**

  Edit `nebula-haze.xml` — for each of these option blocks, change `e09a68` back to `7ab8d8`:

  - `DEFAULT_VALID_STRING_ESCAPE` (string escape sequences like `\n`)
  - `CONSOLE_USER_INPUT` (terminal user input)
  - `CUSTOM_KEYWORD4_ATTRIBUTES` (keyword family)
  - `YAML_SCALAR_LIST` (YAML list marker)
  - `MARKDOWN_LINK_DEFINITION` (markdown link syntax)

  After editing, verify the 5 exceptions are restored:
  ```bash
  grep -A3 "VALID_STRING_ESCAPE\|CONSOLE_USER_INPUT\|CUSTOM_KEYWORD4\|YAML_SCALAR_LIST\|MARKDOWN_LINK_DEF" nebula-haze.xml | grep "FOREGROUND"
  ```
  All 5 should show `7ab8d8`.

- [ ] **Step 4: Redirect JS keyword variants to `b09ce8`**

  Edit `nebula-haze.xml` — for each of these option blocks, change `e09a68` to `b09ce8`:

  - `JS.IF_ELSE`
  - `JS.MODULE_KEYWORD`
  - `JS.TRY_CATCH`
  - `JS.YIELD`

  Verify:
  ```bash
  grep -A3 "JS.IF_ELSE\|JS.MODULE_KEYWORD\|JS.TRY_CATCH\|JS.YIELD" nebula-haze.xml | grep "FOREGROUND"
  ```
  All 4 should show `b09ce8`.

- [ ] **Step 5: Final count sanity check**

  ```bash
  grep -c "7ab8d8" nebula-haze.xml   # expect 5 (the restored exceptions)
  grep -c "e09a68" nebula-haze.xml   # expect TOTAL - 5 - 4
  grep -c "b09ce8" nebula-haze.xml   # should have increased by 4 vs after task 2
  ```

- [ ] **Step 6: Commit**

  ```bash
  git add nebula-haze.xml
  git commit -m "Warm operators to solar wind e09a68, realign JS keywords to violet"
  ```

---

### Task 7: Visual Verification

No automated tests exist for theme files — verification is visual.

**Files:**
- Read: `preview.html`

- [ ] **Step 1: Open preview in browser**

  Open `preview.html` in a browser and visually confirm:
  - Background is noticeably darker than before
  - Class/type names appear violet-soft (`#cabae4`), clearly distinct from local variables (blue `#a0c5e9`)
  - Keywords are clearly purple (`#b09ce8`), not blue-purple
  - Operators/punctuation are warm orange (`#e09a68`)
  - Comments read clearly, visibly brighter than surrounding gutter hints
  - Line numbers visible (`#454d74`) with active-line number brighter (`#737aa2`)

- [ ] **Step 2: Verify git-modified color in file tree (Rider)**

  If Rider is available: load the theme, open a project with modified files in the file tree. Modified file names should appear in muted sandy gold (`#a89e5c`), not amber.

- [ ] **Step 3: Confirm no unintended color bleed**

  Check these token pairs are still visually distinct in `preview.html`:
  - Comments `#7880a8` vs inlay hints `#565f89` — comments clearly brighter
  - Class `#cabae4` vs keywords `#b09ce8` — class lighter/softer
  - Operators `#e09a68` vs numbers `#d8c383` — operator is orange, number is gold
  - Operators `#e09a68` vs error/deleted `#c7778a` — operator is orange, error is rose-red

- [ ] **Step 4: Commit if preview.html was updated**

  If `preview.html` needed any CSS variable updates to reflect the new colors:
  ```bash
  git add preview.html
  git commit -m "Update preview.html CSS vars for color refinements"
  ```
  Otherwise skip.
