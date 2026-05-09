# Example: Launch deck via skill in Claude Code

You're prepping for a launch. You have product specs in `~/notes/launch-spec.md` and competitor analysis in `~/notes/competitive.md`. You want a launch deck outline you can hand to design.

## The setup

- Claude Code v2.1.83 or newer
- PMM Sherpa MCP connector added: `claude mcp add pmm-sherpa --transport http https://pmmsherpa.com/api/mcp`
- PMM Sherpa skill installed globally:

```bash
git clone https://github.com/boommark/pmmsherpa-mcp.git ~/.pmm-sherpa
mkdir -p ~/.claude/skills
ln -s ~/.pmm-sherpa/skills/claude-code ~/.claude/skills/pmm-sherpa
```

## The prompt

```
> Read ~/notes/launch-spec.md and ~/notes/competitive.md. Then build
> me a launch deck outline for the [Product Name] launch on [date].
> Audience is the customer base, not internal sales enablement.
```

## What happens (terminal output, abbreviated)

```
● Skill(pmm-sherpa)
  └ Successfully loaded skill

● Read(~/notes/launch-spec.md)
  └ Read 487 lines

● Read(~/notes/competitive.md)
  └ Read 142 lines

● I'll structure this around the launch deck framework: hook, the
  shift, the product, the proof, the path. Let me draft the
  outline via Sherpa so the framework comes from the corpus, not
  generic templates.

● mcp__pmm-sherpa__draft_artifact(
    artifact_type: "launch_deck",
    audience: "customer base",
    inputs: { ...specs and competitive distilled... }
  )
  └ Generated 14-slide outline

● Outline below. Key calls I made on your behalf:
  1. Slide 2 leads with the customer's old workflow, not your
     product. The deck needs the customer's "before" before they
     care about your "after".
  2. Competitive table (slide 9) shows you on three axes you win
     on. Skipped the axes you lose on. That's not the deck's job.
  3. Closing slide is one ask: book a demo. Not three CTAs.

  [outline rendered as markdown table here]
```

## What the skill does

- Detects `launch deck` keyword → loads `pmm-sherpa` skill
- Routes to `mcp__pmm-sherpa__draft_artifact` with `artifact_type: "launch_deck"` from the 39-template catalog
- Bundles file contents into the call as context
- Layers in framework reasoning before showing the outline

## Why this works

- **Skill auto-fires.** You didn't have to specify "use Sherpa". The keyword `launch deck` triggered it.
- **`draft_artifact`, not `ask_sherpa`.** Launch deck is in the 39-template catalog. The right tool was picked.
- **Framework named mid.** The reasoning happens in plain English, then the framework labels show up in the structure (slides 2, 9, closing).
- **No naming.** Sherpa references the launch deck pattern without naming books, podcasts, or authors that taught it.

## Follow-up: pressure-test the deck

Once you've got an outline, ask Sherpa to critique it:

```
> Pressure-test slides 2, 5, and 9 of that outline. Where would a
> senior PMM say "this is going to lose the room"?
```

This routes to `mcp__pmm-sherpa__get_feedback` with the deck as context.

## What you avoid by using the skill

- Generic "executive launch deck" prose with bullet salads
- Em-dashes everywhere
- "It depends" hedging on slide structure
- A closing slide with three CTAs and no clear ask
