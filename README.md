# Tokyo Night Silent Storm

A dark theme for JetBrains Rider based on [Tokyo Night Storm](https://github.com/enkia/tokyo-night-vscode-theme), with softer backgrounds tuned for daylight use.

**Silent Storm twist:** backgrounds are slightly lighter and warmer than official Storm, reducing harsh contrast without changing the palette feel. All syntax colors are pure Tokyo Night Storm.

![preview](preview.html)

## Features

- Full **ReSharper semantic highlighting** — structs, enums, delegates, events, extension methods, generic type parameters, mutable locals, format strings
- **Dimmed inlay hints** — subordinate to code, won't compete with LINQ chains or parameter names
- Extends **Islands Dark** cleanly — no chrome overrides that cause tab/border glitches
- Languages: C#, HTML, Razor, JSON, XML, YAML, Markdown, CSS

## Palette

| Role | Color |
|---|---|
| Background | `#2a2d3e` |
| Chrome | `#22253a` |
| Foreground | `#c0caf5` |
| Keywords | `#bb9af7` |
| Functions | `#7aa2f7` |
| Strings | `#9ece6a` |
| Numbers | `#ff9e64` |
| Types | `#2ac3de` |
| Enums / Structs | `#73daca` |
| Operators | `#89ddff` |
| Parameters | `#e0af68` |
| Comments | `#565f89` |

## Install

**From JetBrains Marketplace** *(once published)*: Settings → Plugins → search "Tokyo Night Silent Storm"

**From release JAR**: Settings → Plugins → ⚙ → Install Plugin from Disk → pick the `.jar`

## Build from source

```bash
npm install
node build.js        # outputs releases/tokyo-night-silent-storm-x.x.x.jar
```

Open `preview.html` in a browser to see all colors without installing.
