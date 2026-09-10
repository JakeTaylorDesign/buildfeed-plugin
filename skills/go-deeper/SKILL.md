# Skill: go-deeper

## Use this when

The user says "more," "who else," "anything newer," "what else is there on this," or asks a question the field guide could not answer. It also runs when the user follows an `answer-question` reply with a request to keep going.

## Source priority

1. **BuildFeed MCP** — the point of this skill. `search_transcript_passages` over the flavor's category is the primary call.
2. **Knowledge layer** — used to avoid repeating what the user was already told, and to name a voice consistently if the MCP surfaces someone already in that flavor's roster.
3. **General knowledge** — not a source.

## Steps

1. Establish the flavor from `buildfeed` and what the user has already heard. Names and links from the previous answer are off the table.
2. Call `search_transcript_passages` with the topic as the query, the flavor's `category`, `limit: 8`. If the user asked "anything newer," also call `list_videos` with `sort: "recent"`, that `category`, `limit: 20`, keep items published after that guide's knowledge date, then run one passage search scoped to those titles. Never call `get_transcript`.
3. If the first search is thin or off-topic, widen by **rewording**, not paging — the MCP has no pagination. A second query with lane vocabulary, a synonym, or `audience: "Founder"` / `"Investor"` / `"Product"` / `"Designer"` reaches videos the first one missed. At most three searches per turn.
4. Keep passages that actually make a point (read `text`; drop intros, ads, tangents). Group by video.
5. Speaker is the passage `channel`, or a person named in the `title`. Never a name from the passage text, never a name from memory.
6. Write two to five additional voices or moments. Each name links to that passage's `youtubeUrl`.

## Validation

- Only attribute what the MCP returned in this turn.
- Every link is a returned `youtubeUrl` with `&t=`. A `t=0s` result is named without a link, or dropped.
- No name that isn't the passage `channel` or in its `title`.
- Nothing from the previous answer is repeated as if new.
- Passage text is paraphrased, never pasted.

## Output

Prose, same register as `answer-question`. If the new material disagrees with what the user already heard, say so. If it merely repeats the earlier answer with different names, say that too; don't pad. Close by saying whether there's still more, honestly.

## Failure behavior

- **Empty after up to three reworded searches:** the live library doesn't add anything beyond the guide. Do not manufacture depth.
- **Results all off-topic:** treat as empty.
- **429:** one sentence with `upgrade_url`, once per session, then offer the guide.
- **MCP unreachable:** say so; offer the guide if the user hasn't heard it yet.

## Approval

Read-only. Nothing needs approval.
