# Skill: weekly-digest

## Use this when

The user asks "what's new this week" / "anything new on startups|product|design." Not on demand for a single topic — that's `go-deeper` with "anything newer."

## Source priority

1. **BuildFeed MCP** — the only source. The digest is about content newer than the field guides.
2. **Knowledge layer** — map an item to a flavor/lane and skip videos already in a guide.
3. General knowledge — not a source.

## Steps

1. Establish the window: since the last digest (a short convention if one exists), or the last seven days.
2. Decide categories. If the user named a flavor, use only that flavor's categories (`startups` → `"Startup"` and `"VC"`; `product` → `"Product"`; `design` → `"Design"`). If they didn't, run all four.
3. For each category, call `list_videos` with `since: <ISO date>`, `sort: "recent"`, `limit: 50`. `since` reads the archive index. Merge and de-duplicate by `videoId`.
4. If `since` is rejected, fall back to `list_videos` without it and keep only items whose `publishedDate` falls inside the window.
5. Drop anything already linked in any of the three field guides (match `videoId`).
6. **Filter to the lanes** in `buildfeed`. A tag is not a lane. Keep an item only if its title and `channelName` place it in a named lane. This should cut the list.
7. For each remaining item, one `search_transcript_passages` call with the title as the query, `limit: 3`. **Keep only a passage whose `videoId` equals this item's `videoId`** and whose `youtubeUrl` has a non-zero `&t=`. Never call `get_transcript`. If nothing matches, list the item **without a link**.
8. Order by flavor (startups, product, design), then by lane, then by date. Cap at ten items. Prefer items with offsets, then recency.
9. Write it. Store today's date as the last-digest convention.

## Validation

- Every item's `publishedDate` is inside the window.
- Every item maps to a named lane.
- Every link is a `youtubeUrl` from a passage whose `videoId` matches, with a non-zero offset. Otherwise unlinked.
- Ten items or fewer. One line each.
- Zero qualifying items → **no message.** Not "nothing new." Silence.

## Output

A short header with the window, then items grouped by flavor and lane. One line per item: **the title as the link** (or the title alone if unlinked), em dash, channel (and the guest if the title names one). No summaries.

## Failure behavior

- **Nothing in the window, or nothing survives the lane filter:** send nothing.
- **429 or MCP unreachable on a background/routine run:** send nothing, retry next run. Never deliver the budget notice from a routine.
- **429 on an on-demand ask:** one sentence with `upgrade_url`, then stop. Do not invent a digest from the guides.
- **Items without `publishedDate`:** treat as empty; do not guess from `generatedAt`.

## Approval

Read-only besides delivering the digest the user asked for. No third-party sends, no posts, no changes.
