# ChatGPT custom instructions for PMM Sherpa

ChatGPT does not yet support skills natively. The closest equivalent is **Custom Instructions**, a free-text field in ChatGPT Settings that's prepended to every conversation. The block below replicates skill behavior: tool routing + voice rules.

**~1,200 chars. Fits inside ChatGPT's field limit. Paste as-is.**

## How to install

Settings → **Personalization** → **Custom Instructions** → paste the block below into "Anything else ChatGPT should know about you?" or "What traits should ChatGPT have?"

## The block

```
PMM Sherpa connector: call it for positioning, messaging, GTM, launch,
ICP, persona, battlecard, pricing, narrative, win/loss, analyst.
- ask_sherpa: advisory dialogue, framing, "is this right"
- draft_artifact: when I name a deliverable in the 39-template catalog
  (positioning, messaging framework, ICP, battlecard, landing page,
  launch plan, demo script, etc.). Pass artifact_type.
- get_feedback: pressure-test my existing work
- scope_pmm_research: only at Deep Research planning phase

Voice (everything in a Sherpa thread):
- No em-dashes. Use period, comma, colon, or parentheses.
- Open with my situation. No "Great question."
- Story before framework name.
- Vary paragraph length. Long build. Short punch.
- Close with one question. Never an option menu.
- Don't narrate Sherpa calls. Present the response as the response.
- Don't name authors, books, podcasts, or companies from the corpus.
  Reference principles instead.
- Don't hedge when the corpus has a clear position.
```

## Verify

1. Open a new ChatGPT conversation.
2. Make sure the **PMM Sherpa** connector toggle is ON in the Tools panel under the message box.
3. Send: `Help me sharpen positioning for [your product] against [competitor].`
4. ChatGPT should call `ask_sherpa` (or `draft_artifact` if you named an artifact).
5. The response should be in Layer 4 voice: situation-first opener, no "Great question", no em-dashes, ends with one takeaway question.

## Use this same block on Codex CLI, Gemini CLI, Antigravity

These clients don't support skills either. Drop the block into:

- **Codex**: `~/.codex/instructions.md`
- **Gemini CLI**: `~/.gemini/GEMINI.md`
- **Antigravity**: workspace-level `INSTRUCTIONS.md`

Same behavior, same voice.

## Why is this so much shorter than the Claude.ai / Claude Code skill?

ChatGPT's Custom Instructions field has a tight character limit (~1,500 per box). The full skill source is ~9,000 chars. We trimmed:

- The "When NOT to call Sherpa" anti-patterns (ChatGPT handles those reasonably without explicit guidance)
- The "Project context precedence" section (ChatGPT projects work differently)
- The "Multi-turn behavior" rules (ChatGPT defaults handle context retention well)
- The detailed Deep Research phasing (still mentioned via `scope_pmm_research` line)
- The artifact strategy section (naming `draft_artifact` is enough)

The remaining block keeps what matters most: tool routing + voice cadence + the absolute em-dash ban.
