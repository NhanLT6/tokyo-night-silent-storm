# Nebula Haze

A cold, deep-space dark theme for JetBrains Rider built around muted nebula syntax, dark chrome, and sparse warm stellar accents.

**Nebula Haze identity:** most syntax reads as cold mist and gas, while numbers and markup tags provide the only warm highlights.

![preview](preview.html)

## Features

- Full **ReSharper semantic highlighting** — structs, enums, delegates, events, extension methods, generic type parameters, mutable locals, format strings
- **Dimmed inlay hints** — subordinate to code, won't compete with LINQ chains or parameter names
- Extends **Islands Dark** cleanly — no chrome overrides that cause tab/border glitches
- Languages: C#, HTML, Razor, JSON, XML, YAML, Markdown, CSS

## Palette

| Role | Color |
|---|---|
| Background | `#22253a` |
| Chrome | `#1a1d30` |
| Foreground | `#c0caf5` |
| Keywords | `#afa4e5` |
| Functions | `#85a7f5` |
| Strings | `#90d89f` |
| Numbers | `#d8c383` |
| Types | `#b1d0e6` |
| Enums / Structs | `#73daca` |
| Operators | `#7ab8d8` |
| Parameters | `#c6afa9` |
| Comments | `#5e6590` |

## Install

**From JetBrains Marketplace** *(once published)*: Settings → Plugins → search "Nebula Haze"

**From release JAR**: Settings → Plugins → ⚙ → Install Plugin from Disk → pick the `.jar`

## Build from source

```bash
npm install
node build.js        # outputs releases/nebula-haze-x.x.x.jar
```

Open `preview.html` in a browser to see all colors without installing.
