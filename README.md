# BuildFeed plugin

Ask a startup, product, or design question. Get the take from people who have done the work, not a mashup of the internet.

This is the public marketplace package. It ships curated field guides (startups, product, design) and a read-only MCP over the channels [BuildFeed](https://buildfeed.tech) already watches. No hooks, no agents, no local binaries, no secrets.

The [Startups bot share](https://x.ai/bot/7tob1iILCQ-5aELPbHSPn) is a named teammate on the same library. Do not submit Startups / Product / Design as separate marketplace listings.

## What it ships

| Component | Path | What it does |
|---|---|---|
| Logo | `logo.png` | Retro TV, white background |
| MCP | `.mcp.json` | `https://buildfeed.tech/api/mcp` — streamable HTTP, no key |
| `buildfeed` | `skills/buildfeed/SKILL.md` | Job, flavor routing, rules |
| `answer-question` | `skills/answer-question/SKILL.md` | Default: guide first, MCP only if silent or newer |
| `go-deeper` | `skills/go-deeper/SKILL.md` | Live library, additional voices |
| `weekly-digest` | `skills/weekly-digest/SKILL.md` | What's new since a date |
| `startups-field-guide` | `skills/startups-field-guide/SKILL.md` | Generated knowledge layer |
| `product-field-guide` | `skills/product-field-guide/SKILL.md` | Generated knowledge layer |
| `design-field-guide` | `skills/design-field-guide/SKILL.md` | Generated knowledge layer |

## Network

- **Endpoint:** `https://buildfeed.tech/api/mcp` (public, no auth)
- **Optional:** `Authorization: Bearer bf_live_…` after a server `429`, stored as a plugin setting, never in this repo
- **Video links** in the field guides: `https://youtu.be/<id>?t=<seconds>`
- Nothing else is called

## Catalog submit

The plugin root is this repository root.

**Cursor / Grok Bot** — [cursor.com/marketplace/publish](https://cursor.com/marketplace/publish)

- GitHub repository: `https://github.com/JakeTaylorDesign/buildfeed-plugin`
- Logo: `https://raw.githubusercontent.com/JakeTaylorDesign/buildfeed-plugin/main/logo.png`
- Website: `https://buildfeed.tech`

**Grok Build** — one remote entry named `buildfeed` against [xai-org/plugin-marketplace](https://github.com/xai-org/plugin-marketplace), homepage `https://buildfeed.tech`, keywords `["buildfeed", "buildfeed mcp", "buildfeed.tech"]`, domains `["buildfeed.tech"]`, pinned to a full commit SHA of this repo.

License: MIT
