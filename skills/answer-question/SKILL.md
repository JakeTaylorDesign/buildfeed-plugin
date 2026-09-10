# Skill: answer-question

## Use this when

The user asks what the voices in the library say about something — "what do people think about X," "how should I think about Y," "is it true that Z." This is the default skill; most turns are this.

## Source priority

1. **Knowledge layer** — the field-guide skill for the flavor `buildfeed` selected (`positions`, `disagreements`, `frameworks`, `roster`). Answer from here whenever it covers the topic.
2. **BuildFeed MCP** — only if that guide is silent, or the question is newer than its `knowledge-date`. Not for topics the guide already covers; if the user wants more after a guide-based answer, that's `go-deeper`.
3. **General knowledge** — not a source. If you can't answer from 1 or 2, say so.

## Steps

1. Map the question to a flavor and lane using `buildfeed`. If it is outside all lanes, say so in a sentence and stop.
2. Search that guide's positions for stances on the topic. Note every holder and their link.
3. Check its disagreements for a live debate. If there is one, you will surface it.
4. Check its frameworks for a named model; naming it is often the most useful thing you can do.
5. If steps 2–4 found nothing, or the question mentions something recent (a launch, a round, a name that isn't in that roster, "this month"), call `search_transcript_passages` once with the question as the query and the flavor's `category`. Use only what comes back. Never call `get_transcript`.
6. Write the answer in the house style: lead with the substance, names linked, disagreement as two sides if there is one. No lists, no clocks, no preamble.
7. Offer to go deeper only if there is genuinely more — unused positions in the guide, or a question broad enough that the live library would add voices.

## Validation

- Every person named is in that guide, or came back from the MCP call in this turn, with a link. A name with no link is removed.
- Every video link carries `?t=` or `&t=…s`. A link without an offset is dropped; the sentence stays.
- "Most people agree" needs at least two named people. One person is one person's view.
- Nothing quoted at length. Nothing attributed to an organization.
- Under 250 words, unless the user asked for more.

## Output

Prose. Two or three short paragraphs. Names linked. If the guide has a debate on this topic, one paragraph shows both sides. If a named framework applies, name it.

## Failure behavior

- **Guide silent, MCP returns nothing:** "BuildFeed doesn't have anything on that from the [flavor] roster." Offer one adjacent topic the guide does cover, if there is an obvious one.
- **MCP 429:** one plain sentence with the response `upgrade_url`, once per session, then answer from the guide.
- **MCP unreachable:** answer from the guide if it covers the topic; otherwise say the live library isn't reachable and the guide has nothing on this. Never fabricate a result.

## Approval

Read-only. Never call `get_transcript`. Never send, post, or change anything.

## Example of a correct result

**User:** How should I think about pricing my SaaS product?

**Bot:**

The strongest line in the startups guide is Jason Cohen's, and it's blunt: price on the value the customer already cares about — growth, not savings — because value-based pricing has a much higher ceiling than cost-based [Jason Cohen](https://youtu.be/8xLquwfx6p0?t=2814). His test for whether you're there yet is just as blunt: keep raising the price in steps until demand actually drops. If you multiplied it and nothing observable changed, you weren't near the price [Jason Cohen](https://youtu.be/8xLquwfx6p0?t=2312).

There's a live disagreement on the *structure*, though. Cohen is arguing for pushing conventional contract pricing up until you hit resistance [Jason Cohen](https://youtu.be/8xLquwfx6p0?t=2316), while Greg Isenberg thinks per-seat pricing is losing its appeal and that buyers in the AI era increasingly want to pay per completed task [Greg Isenberg](https://youtu.be/9T1yWEq5kP0?t=1141). Which one applies depends on whether what you sell is a seat or an outcome.

Mark Roberge would add a sequencing caveat: none of this tuning is worth doing until product-market fit is locked, because pricing and quota changes on top of weak retention just move the problem around [Mark Roberge](https://youtu.be/5bnpMYSdqbM?t=2739).

There's more in the library on the per-task side if you want to go deeper.
