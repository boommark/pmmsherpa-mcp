# Claude.ai skill

This is the PMM Sherpa skill for Claude.ai. Once uploaded, Claude.ai auto-triggers Sherpa on PMM keywords (positioning, messaging, GTM, launch, ICP, persona, battlecard, pricing, narrative, win/loss, analyst relations) and enforces Layer 4 voice across the conversation.

## What's in this folder

| File | Purpose |
|---|---|
| [`pmm-sherpa-skill.zip`](pmm-sherpa-skill.zip) | Upload this to Claude.ai |
| [`SKILL.md`](SKILL.md) | Source of the skill (same content, unzipped, for review) |

## Install

### Prerequisites

- Claude.ai Pro, Max, Team, or Enterprise (skills are gated to paid tiers)
- The PMM Sherpa MCP connector already added (see [the README](../../README.md#claude-ai))

### Steps

1. Download `pmm-sherpa-skill.zip` from this folder
2. Open Claude.ai → **Settings** → **Capabilities** → **Skills**
3. Click **Upload skill** → select the zip
4. Toggle the **PMM Sherpa** skill ON

### Verify

Open a new conversation. Type:

```
Help me sharpen positioning for [your product] against [competitor].
```

You should see:

- The skill name `pmm-sherpa` appear at the top of the response
- A `mcp__pmm-sherpa__ask_sherpa` (or `draft_artifact`) tool call render
- The response in Layer 4 voice (no "Great question", no em-dashes, one closing question)

If the skill doesn't auto-fire, the MCP connector may not be toggled ON for that conversation. Check the Tools panel in the input bar.

## What the skill does

The skill is a calling guide. It tells Claude.ai:

- **When to call Sherpa** vs handle directly (file parsing, web fetch, image gen → Claude's native tools)
- **Which of the four tools** to pick by intent (`ask_sherpa`, `draft_artifact`, `get_feedback`, `scope_pmm_research`)
- **How to phase Sherpa** across a Deep Research run (planning → search → synthesis)
- **How to preserve project context** when in a Claude project with brand guidelines or ICP definitions
- **Voice rules**: never em-dashes, story before framework, single-question close, no consultant-speak, no naming corpus authors

## Update

We update the skill alongside server changes. To update:

1. Pull this repo (or download the latest zip from the latest [release](https://github.com/boommark/pmmsherpa-mcp/releases))
2. Re-upload the new zip to Claude.ai (it replaces the old version)
3. Old conversations keep using the version that was active when they started; new conversations pick up the latest

## Source

The skill source is in [`SKILL.md`](SKILL.md). It's the same file inside the zip. Read it to understand exactly what Sherpa instructs Claude.ai to do.
