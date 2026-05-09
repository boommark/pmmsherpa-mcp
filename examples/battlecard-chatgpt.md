# Example: Battlecard in ChatGPT

You're in ChatGPT. You want a battlecard against a specific competitor for a specific deal context. ChatGPT doesn't have skills, so you've pasted the [custom instructions](../skills/chatgpt/custom-instructions.md) once.

## The setup

- ChatGPT Plus, Pro, Team, or Business
- Developer Mode enabled (Settings → Connectors → Advanced → Developer Mode ON)
- PMM Sherpa connector added (Settings → Connectors → Create → URL `https://pmmsherpa.com/api/mcp` → OAuth)
- Custom instructions pasted (Settings → Personalization → Custom Instructions)
- PMM Sherpa toggle ON in the conversation's Tools panel

## The prompt

```
Build me a battlecard against [Competitor Name] for selling
[Product Name] to [audience].

Deal context: [audience] has been using [Competitor] for 18 months,
hit a scaling wall, and is starting to evaluate alternatives.
Their CFO is asking why they pay [Competitor]'s contract price.

Give me:
1. Three "why we win" angles (tightest first)
2. The two traps Sherpa must not fall into when comparing
3. How to handle the "we'd have to migrate everything" objection
```

## What the custom instructions do

- Trigger ChatGPT to call the **PMM Sherpa** connector (battlecard is a PMM keyword)
- Pick `draft_artifact` with `artifact_type: "competitive_battlecard"` (it's in the 39-template catalog)
- Apply Layer 4 voice rules to ChatGPT's framing prose
- Suppress "Great question", em-dashes, and chat-AI preamble

## What ChatGPT shows you

```
[connector chip: PMM Sherpa]

🛠 Calling PMM Sherpa
  draft_artifact (competitive_battlecard)

Three angles, ranked:

1. The migration cost is a feature, not a bug
   When [Competitor]'s buyer says "we'd have to migrate everything,"
   they're flagging that they're locked in. That lock-in is what made
   them hit the scaling wall. The migration is the path out of the
   trap, not a tax.

   Use this angle when the CFO is asking the question. CFOs hate
   recurring lock-in.

2. [Product] was built for the workload [Competitor] was forced into
   [Competitor] was built for [original use case] and bolted on
   support for [new use case] in 2024. [Product] was built for the
   new use case from day zero. Two years of architecture compounds.

   Use this angle when the technical evaluator is in the room.

3. The CFO question answers itself
   "Why do we pay [Competitor]'s contract price?" is the buyer
   already deciding to leave. Don't argue price. Argue what they're
   getting next year for that price (the answer: less, because their
   roadmap is fragmented).

   Use this angle when the buyer has named the price question first.

Two traps:

- Don't compare on feature parity tables. [Competitor] will publish
  one too, and theirs will be longer.
- Don't say "we're more secure / faster / cheaper" without naming
  the workload. Generic claims read as posturing.

Migration objection:

The buyer isn't asking "is migration hard." They're asking "is it
worth it." Your answer isn't a migration plan, it's the next 18
months. Sketch what they get with [Product] in month 6, 12, 18.
Make migration a means to that end.

What's the buyer's biggest fear about leaving [Competitor] right
now: budget, technical risk, or political risk inside their team?
```

## Why this works

- **`draft_artifact` was picked correctly.** Battlecard is in the 39-template catalog. Custom instructions routed it.
- **Voice held.** No em-dashes. No "Great question". One closing question. Story before framework.
- **No author/source naming.** The principles around competitive positioning come through without "as Tony Ulwick says..." or "April Dunford's framework..."

## Common mistakes

- **Forgetting to toggle the connector ON in the conversation.** ChatGPT silently falls back to non-MCP responses with default prose.
- **Pasting custom instructions twice.** You only need them once in Settings. They're applied to every conversation.
- **Using ChatGPT Free tier.** MCP connectors are gated to paid tiers. Free will not see the connector at all.
