# Example: Prep for a PMM interview at a target company

You have a final-round PMM interview at a specific company in a few days. You want to show up with a sharp read on their positioning, likely GTM weak spots, and crisp answers to the case-style questions hiring managers ask. Most candidates show up with frameworks. You're going to show up with a teardown.

This is a three-tool flow: `ask_sherpa` to scope the company, `draft_artifact` (`artifact_type: company_teardown`) to build the teardown, `get_feedback` to pressure-test your answers.

## The setup

- Any MCP-capable client (Claude.ai, Claude Code, ChatGPT, Codex, Gemini CLI, Antigravity)
- PMM Sherpa connector added
- (Recommended) PMM Sherpa skill or custom instructions installed so the right tool fires automatically

## Step 1 · Scope the company

The first call gets you the read a senior PMM would walk in with: their *implied* positioning, the moves they'd make in the first 90 days, and the case questions a hiring manager is likely to throw at you.

```
ask_sherpa: I have a Senior PMM interview at [Company]. They sell
[product] to [audience]. Read their site, then give me:

1. The positioning statement they imply (not what they say)
2. The three GTM moves a senior PMM would make in their first 90 days
3. The two questions a hiring manager is likely to ask in a case round
```

What you get back is a tight read of where the company actually sits in the market versus where their copy claims they sit, with concrete first-90-day moves and the case questions you should rehearse.

## Step 2 · Build a teardown you can walk in with

Now you turn the read into a one-page artifact you can present on a whiteboard or screenshare.

```
draft_artifact: artifact_type: company_teardown

Inputs:
- Company URL: [paste]
- Product category: [paste]
- ICP I think they're chasing: [paste]
- Two competitors I noticed: [paste]

Output the teardown the way I'd present it on a whiteboard:
positioning, ICP fit, messaging gaps, one launch they should run,
one they should kill.
```

Sherpa returns a structured teardown you can walk in with: their current positioning vs. where it should be, ICP fit assessment, three messaging gaps with examples, one launch you'd run in your first 60 days, and one in-flight motion you'd kill on day one.

## Step 3 · Pressure-test your answers

Before you walk in, run your strongest case answer through Sherpa as if a senior PMM were reviewing it.

```
get_feedback: Score this answer to "What's the first 30/60/90 you'd
run if we hired you?" on three dimensions:

1. Specificity to *our* business (not generic PMM moves)
2. Evidence behind each move (data, examples, customer quotes)
3. Whether it sounds like a senior PMM or a generalist

Here is the draft: [paste your answer]
```

Sherpa flags the moments your answer slides into generic PMM-speak, identifies where you need a concrete proof point, and tells you whether the level matches the role. Apply the feedback. Re-run if you change anything material.

## Why this phasing matters

- **`ask_sherpa` first, not `draft_artifact` first.** The teardown needs the company-specific read as input. Skipping the scope call means the artifact gets generic.
- **One teardown, not five.** Pick the most likely interview format (whiteboard, take-home, panel case) and build the artifact for that one. Don't build a binder.
- **`get_feedback` on your *answer*, not your resume.** Sherpa is calibrated for PMM judgment, not career coaching. Use a career coach for the resume.

## What you skip if you don't use Sherpa

You walk in with frameworks, not a teardown. You have generic answers to "what would you do in your first 90 days" instead of company-specific moves. You haven't pressure-tested your strongest case answer against senior-PMM heuristics. The interviewer can tell within five minutes whether you've done this prep, and the candidates who have move forward.

## Cost note

A typical interview prep run costs:

- 1 × `ask_sherpa` (2 credits)
- 1 × `draft_artifact` company_teardown (2 credits)
- 1-3 × `get_feedback` on case answers (2-6 credits)
- **Total: ~6-10 credits per interview prep**

Well within Free tier (10 monthly credits) for one interview, or 20+ interviews per month on the Starter plan.

## A note on what to skip

- Do not paste your full resume. Sherpa is calibrated for PMM judgment, not career coaching.
- Do not ask Sherpa to "interview you" with rapid-fire questions. The signal comes from artifact quality, not Q&A volume.
- Do not run the teardown an hour before the interview. Build it 2-3 days out so you can sit with it, edit it, and rehearse the moves out loud.
