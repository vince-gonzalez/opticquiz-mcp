# OpticQuiz MCP servers

**Two MCP servers that let an assistant check and see color the way a colorblind person does** —
built on a published, open-access color-vision method rather than a rule of thumb.

Both are listed in the official [Model Context Protocol registry](https://registry.modelcontextprotocol.io).

## `cvdsafe-mcp` — check it

| tool | what it does |
| --- | --- |
| `checkPalette` | Whether a set of colors stays distinguishable under protanopia, deuteranopia and tritanopia — with the conflicting pairs named |
| `checkImage` | Extracts an image's dominant colors and flags the pairs that collapse, each weighted by how much of the image they cover. PNG + JPEG |
| `generateSafePalette` | N colorblind-safe colors, seeded with Okabe–Ito. Never returns an unsafe one |
| `fixPalette` | Repairs a failing palette, staying close to the originals |
| `checkContrast` | WCAG contrast ratio, AA/AAA |
| `simulateColor` | One color under a chosen deficiency |

## `colorblind-mcp` — see it

| tool | what it does |
| --- | --- |
| `simulateImage` | Recolors a PNG/JPEG the way a deficiency renders it, and **returns the image** |
| `plate` | Generates an Ishihara-style pseudoisochromatic test plate and returns it |
| `compareVision` | One color under all three deficiencies at once |
| `simulateColor` | A single color under one deficiency, with severity |

## Install

Add to `claude_desktop_config.json` (Settings → Developer → Edit Config):

```json
{
  "mcpServers": {
    "cvdsafe":    { "command": "npx", "args": ["-y", "cvdsafe-mcp"] },
    "colorblind": { "command": "npx", "args": ["-y", "colorblind-mcp"] }
  }
}
```

Restart, then ask: *"Is this palette colorblind-safe: #d7191c, #1a9641, #2166ac?"* or *"Show me
./dashboard.png the way a deuteranope sees it."* Same config shape works in Cursor and other MCP
clients.

## The method

Colors are simulated with the **Machado, Oliveira & Fernandes (2009)** deficiency matrices and
compared with **CIEDE2000**. The method is published open access —
[doi.org/10.5281/zenodo.21310578](https://doi.org/10.5281/zenodo.21310578) — and the same engine
ships as installable packages (`cvdsafe`, `cvdsim` on PyPI and npm), so any answer these servers
give can be reproduced outside them.

Everything runs locally over stdio. Nothing leaves your machine; images are read from your disk and
returned in the response.

## Not a legal audit

These check one axis of accessibility — whether colors stay distinguishable under color-vision
deficiency. That is not a full WCAG or ADA conformance audit, and passing does not make a product
compliant.

Part of [OpticQuiz](https://opticquiz.com) · [methodology & disclosure](https://opticquiz.com/methodology/)
