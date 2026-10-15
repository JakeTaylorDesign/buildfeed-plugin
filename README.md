# BuildFeed Plugin

[![MIT License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Grok Bot Compatible](https://img.shields.io/badge/Grok%20Bot-Compatible-purple)](https://x.ai/bot)
[![Cursor Compatible](https://img.shields.io/badge/Cursor-Compatible-brightgreen)](https://cursor.com)

> Ask startup, product, or design questions. Get answers from people who have actually done the work—not a mashup of the internet.

BuildFeed is a curated library plugin that connects AI agents to transcripts from top startup, product, and design content creators on YouTube. Instead of generic advice, you get specific perspectives from practitioners, with direct links to the moment they made the point.

## What You Get

### 🎯 Three Curated Field Guides
Pre-compiled knowledge bases covering the most common questions in each domain:

- **Startups Field Guide** — Founding, fundraising, market/PMF, GTM, pricing, hiring
- **Product Field Guide** — Discovery, roadmaps, shipping, metrics, experiments, the PM role
- **Design Field Guide** — Visual craft, design process, systems, research, the design role

Each guide captures who said what, where they disagree, and which frameworks they use.

### 🔌 Live MCP Server
Real-time access to the full BuildFeed transcript library via [Model Context Protocol](https://modelcontextprotocol.io):

- **`search_videos`** — Find episodes by topic, guest, or channel
- **`search_transcript_passages`** — Search across all transcript text with timestamp precision
- **`get_transcript`** — Retrieve full episode transcripts
- **`list_videos`** — Browse by channel, topic, category, or date
- **`get_weekly_roundup`** — See what's new in the library
- **`list_channels`**, **`list_topics`**, **`list_categories`** — Explore the catalog
- **`get_stats`** — Library metrics and coverage

**Endpoint:** `https://buildfeed.tech/api/mcp` (public, no authentication required)

### 📚 Skills Included
Seven specialized agent skills that know how to use the library effectively:

| Skill | Purpose |
|-------|---------|
| `buildfeed` | Router that picks the right field guide and category |
| `answer-question` | Default handler — checks guides first, then live library |
| `go-deeper` | Follow-up handler for "tell me more" requests |
| `weekly-digest` | Summary of new content since a given date |
| `startups-field-guide` | Compiled startup knowledge (founders, VCs, operators) |
| `product-field-guide` | Compiled product knowledge (PMs, growth leads) |
| `design-field-guide` | Compiled design knowledge (designers, researchers) |

## Installation

### For Grok Bot

1. Visit the [Grok Bot plugin marketplace](https://x.ai/bot/marketplace)
2. Search for "BuildFeed"
3. Click "Install" — no configuration needed

### For Cursor

1. Open Cursor Settings
2. Navigate to **Plugins** or **Extensions**
3. Search for "BuildFeed" in the marketplace
4. Click "Install"

### Manual Installation (Advanced)

Clone this repository to your local plugins directory:

```bash
# For Cursor
git clone https://github.com/JakeTaylorDesign/buildfeed-plugin.git ~/.cursor/plugins/buildfeed

# For Grok Bot
git clone https://github.com/JakeTaylorDesign/buildfeed-plugin.git ~/.grok-bot/plugins/buildfeed
```

## Example Prompts

Once installed, try asking questions like:

- *"What do founders say about finding product-market fit?"*
- *"How should I think about pricing my SaaS product?"*
- *"What's the debate on per-seat vs usage-based pricing?"*
- *"Tell me more about Jason Cohen's views on pricing"*
- *"What design patterns do people recommend for onboarding?"*
- *"What's new in the BuildFeed library this week?"*

The plugin will:
1. Route your question to the right domain (startup/product/design)
2. Check the relevant field guide first (fast, curated)
3. Search the live library if needed (comprehensive, up-to-date)
4. Return attributed perspectives with timestamp links to the source videos

## How It Works

**Source Priority:**
1. **Field guides first** — Pre-compiled knowledge for common questions (fast, curated, covers 80% of queries)
2. **Live MCP when needed** — Real-time search when guides are silent, question is very recent, or you ask for more voices

**Attribution Rules:**
- Every claim links to the specific moment in the source video (YouTube `?t=` timestamp)
- Names only the channel or guest from the video title
- Never invents composite views ("what the community thinks")
- Never quotes at length—paraphrases with attribution

**Read-Only:**
- This plugin only retrieves and presents information
- It never posts, publishes, or modifies anything
- No approval prompts, no side effects

## Configuration

### Optional: BuildFeed API Key

The plugin works without authentication. If you hit rate limits (HTTP 429), you can add a BuildFeed API key:

1. Visit [buildfeed.tech](https://buildfeed.tech) to get an API key
2. In your agent settings, add:
   - **Setting name:** `BUILDFEED_API_KEY`
   - **Value:** `bf_live_...`

The plugin will automatically use it when provided.

## Repository Structure

```
buildfeed-plugin/
├── .cursor-plugin/
│   └── marketplace.json      # Cursor marketplace manifest
├── .grok-plugin/
│   └── plugin.json            # Grok Bot plugin manifest
├── skills/
│   ├── buildfeed/             # Router skill
│   ├── answer-question/       # Default Q&A handler
│   ├── go-deeper/             # Follow-up handler
│   ├── weekly-digest/         # New content summary
│   ├── startups-field-guide/  # Compiled startup knowledge
│   ├── product-field-guide/   # Compiled product knowledge
│   └── design-field-guide/    # Compiled design knowledge
├── logo.png                   # Plugin logo (retro TV)
├── mcp.json                   # MCP server configuration
├── plugin.json                # Plugin metadata
├── LICENSE                    # MIT License
└── README.md                  # This file
```

## Contributing

This is the public marketplace package maintained by BuildFeed. The library itself is curated and maintained at [buildfeed.tech](https://buildfeed.tech).

For issues with:
- **Plugin behavior or skills** — Open an issue in this repository
- **Library content or coverage** — Contact [BuildFeed](https://buildfeed.tech)
- **MCP server or API** — Check [buildfeed.tech/docs](https://buildfeed.tech) or contact support

## Related Resources

- **BuildFeed Website:** [buildfeed.tech](https://buildfeed.tech)
- **Grok Bot Marketplace:** [x.ai/bot/marketplace](https://x.ai/bot/marketplace)
- **Cursor Marketplace:** [cursor.com/marketplace](https://cursor.com/marketplace)
- **Model Context Protocol:** [modelcontextprotocol.io](https://modelcontextprotocol.io)

## License

MIT License — see [LICENSE](LICENSE) for details.

Copyright (c) 2026 BuildFeed

---

**Made by [BuildFeed](https://buildfeed.tech)** — Curated startup, product, and design knowledge from the practitioners who built it.
