# Example: Positioning sharpening in Claude.ai

A common workflow. You've got a rough positioning statement. You want a senior PMM to tell you where it's soft and how to fix it.

## The setup

- Claude.ai Pro/Max/Team/Enterprise
- PMM Sherpa connector added (see [README → Claude.ai](../README.md#claude-ai))
- PMM Sherpa skill uploaded (recommended, otherwise toggle the connector ON manually)

## The prompt

```
Here's the rough positioning we have for [Product Name]:

"[Product Name] is the [category] for [audience] who [pain].
Unlike [competitor], we [differentiator] so you can [outcome]."

Concrete: "Loop is the customer feedback platform for B2B SaaS PMs
who waste time stitching together survey tools, support tickets,
and sales call notes. Unlike SurveyMonkey, we automatically cluster
themes across all three sources so you can ship features customers
actually asked for."

Help me sharpen this. Where is it soft? What would a senior PMM
tear apart? Don't rewrite it yet, diagnose first.
```

## What the skill does

- Detects keywords: `positioning` triggers `pmm-sherpa` skill
- Routes to `ask_sherpa` (diagnostic, not artifact generation)
- Bundles the draft into the call so Sherpa has context

## What Sherpa returns

A diagnostic in Layer 4 voice. Roughly:

> Your positioning has three weak spots that a senior PMM would push back on immediately.
>
> First, "B2B SaaS PMs" is too broad. The product marketer at a 10-person Series A and the one at a 500-person Series D have completely different pain. The first is overwhelmed by tooling chaos. The second is overwhelmed by signal noise. Same words, different problem. Pick one.
>
> Second, "stitching together" is the symptom your buyer feels. The cause is that none of those three sources speak the same language. SurveyMonkey gives you NPS scores. Zendesk gives you ticket categories. Gong gives you transcripts. The buyer feels stitching pain. The actual job to be done is "give me one taxonomy for what customers want, regardless of where they said it."
>
> Third, the differentiator collapses your moat. "Automatically cluster themes" is something every survey tool will claim by Q3. The thing competitors will copy slowest is the *taxonomy* itself. If you've got a taxonomy that maps to common B2B SaaS feature buckets out of the box, that's the moat. Lead with that.
>
> Where do you want to start: pick the audience first, or sharpen the differentiator first?

## Why this works

- **Diagnostic, not generative.** You asked for analysis, not a rewrite. Sherpa respects the ask.
- **Story before framework.** The diagnosis surfaces specific weak spots before naming "audience definition" or "differentiator durability".
- **One closing question.** Never a menu of options.
- **Layer 4 voice throughout.** No em-dashes, no "Great question", no "leverage" or "at the end of the day".

## Follow-up

Once you've decided on the diagnosis, you can call `draft_artifact` with `artifact_type: positioning_statement` and pass the sharpened inputs. That returns the structured artifact with framework baked in.

```
Call draft_artifact for a positioning statement. Audience: PM at
Series B-D B2B SaaS, 50-200 employees. Pain: signal noise, not
tooling chaos. Differentiator: opinionated B2B SaaS feature taxonomy
that maps customer language to product roadmap categories
out-of-the-box.
```

## Common mistakes

- **Asking Sherpa to rewrite without diagnosing first.** You miss the analysis that would have made the rewrite better.
- **Skipping the skill and toggling the connector manually.** You forget to toggle in 1 of 3 conversations and get default ChatGPT-style prose.
- **Pasting too much context.** Sherpa works best with one focused draft, not a Notion doc dump.
