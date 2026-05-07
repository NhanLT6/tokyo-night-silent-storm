# Nebula Haze — Codebase Guide for Claude

## Color work

**Read `PALETTE.md` first** — it contains the full swatch book, token mappings, and governance rules. Do not scan `nebula-haze.xml` to look up colors; the XML is 2000+ lines and PALETTE.md has everything you need.

When changing a color:
1. Identify the palette slot (family + level) in `PALETTE.md`
2. Update the token in `nebula-haze.xml`
3. Update the `Used for` column in `PALETTE.md` if the token mapping changes
4. If the hex value itself changes, update both the XML and `PALETTE.md`

The full design rationale lives at `docs/superpowers/specs/2026-05-07-palette-system-design.md`.

## Theme file

- `nebula-haze.xml` — the JetBrains/Rider color scheme. One file, all tokens.
- `preview.html` — visual preview; open in browser to check changes.
- `META-INF/plugin.xml` — plugin metadata, not color-related.
