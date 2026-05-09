# Example: Deep Research with Sherpa

You're using Claude.ai Deep Research (or any orchestrator that runs a multi-agent research flow) on a PMM-adjacent question. Sherpa plugs into three of the four phases: planning, search, synthesis. This is where `scope_pmm_research` and `get_feedback` shine.

## The setup

- Claude.ai with Deep Research enabled (Pro/Max/Team/Enterprise)
- PMM Sherpa connector added
- PMM Sherpa skill uploaded (this is critical for Deep Research, the skill tells the lead agent when to call which Sherpa tool at which phase)

## The research question

```
What's the right pricing strategy for an opinionated B2B SaaS
analytics tool aimed at PMs at Series B-D companies (50-200
employees), competing against three free or freemium incumbents?
```

## What the skill does at each phase

### Planning phase (lead agent, once)

Before decomposing the question into sub-questions, the lead agent calls **`scope_pmm_research`**. Sherpa returns a planning brief:

```json
{
  "angle": "Pricing strategy for opinionated B2B SaaS analytics
            against freemium incumbents",
  "sub_questions": [
    "How do PMs at Series B-D companies actually evaluate analytics
     tooling cost (TCO vs sticker)?",
    "What anchor pricing exists in the freemium incumbents that
     constrains the opinionated entrant's room?",
    "What pricing models (seat, usage, value-based, hybrid) work for
     opinionated tools that displace free?",
    "Where does opinionated software extract premium without losing
     the audience to free?",
    "What pricing mistakes do opinionated B2B SaaS analytics tools
     make in their first 18 months?"
  ],
  "sources_to_weight": [
    "Pricing-strategy practitioner essays from operators with B2B
     SaaS experience",
    "Practitioner AMAs from PMMs who've launched against freemium",
    "Books on value-based pricing and opinionated software"
  ],
  "anti_patterns": [
    "Don't assume usage-based wins because it sounds modern. Most B2B
     SaaS analytics buyers prefer predictability.",
    "Don't compare to consumer SaaS pricing. The buying motion is
     different.",
    "Don't conflate 'opinionated' with 'enterprise'. They're different
     pricing posture decisions."
  ],
  "success_criteria": [
    "A recommended pricing model with one alternative",
    "An anchor pricing range with reasoning",
    "Three concrete pricing decisions you should make in the first
     90 days"
  ]
}
```

The lead agent uses this brief to decompose the question into sub-questions. Sub-questions match Sherpa's `sub_questions` array.

### Search/retrieval phase (subagents, optional)

For each sub-question, a subagent runs web search + corpus retrieval. For PMM-flavored sub-questions, the subagent **may** call `ask_sherpa` once for a principle-grounded angle on a specific facet.

Example, sub-question 4 ("Where does opinionated software extract premium without losing the audience to free?") — the subagent calls:

```
ask_sherpa: "How do opinionated B2B SaaS tools price against
freemium incumbents without losing the audience? What's the
principle behind the premium?"
```

Sherpa returns the principle. Web search returns recent operator examples. The subagent synthesizes both into a sub-answer.

**Use sparingly**. One Sherpa call per subagent, scoped tight. Web search is the primary retrieval surface. Sherpa adds judgment, not coverage.

### Synthesis phase (lead agent, once)

Before finalizing the report, the lead agent drafts a tight thesis-level summary (1 to 2K tokens covering the core thesis, key claims, recommendations) and passes it to **`get_feedback`**.

```
get_feedback: "Here's the thesis-level summary of our pricing
research. Pressure-test it. Where would a senior PMM say 'this is
going to fall apart in execution'?"
```

Sherpa returns gaps + recommendations. The lead agent applies the feedback, then finalizes the full report.

**Critical**: do not pass the full report to `get_feedback`. Pass a tight thesis-level draft (1-2K tokens). Sherpa is calibrated for principle-level critique, not section-by-section editing.

## Why this phasing matters

- **`scope_pmm_research` once at planning.** This is where Sherpa's senior judgment shapes what gets researched, not just what gets summarized at the end. Calling it later (mid-search or mid-synthesis) is too late.
- **`ask_sherpa` sparingly during search.** Subagents that call Sherpa for every sub-question burn credits and dilute coverage. One per subagent, scoped tight.
- **`get_feedback` once at synthesis.** Pressure-test the thesis, not the full report. The thesis is where the wrong call would propagate.

## What you skip if you don't use the skill

The lead agent will:

- Skip `scope_pmm_research` entirely (planning brief absent → wrong sub-questions → wrong answers)
- Either ignore Sherpa during search or call it on every sub-question (the latter is expensive and noisy)
- Skip `get_feedback` synthesis pressure-test (final report ships untested against senior PMM heuristics)

## Cost note

A typical PMM Deep Research run with the skill installed costs:

- 1 × `scope_pmm_research` (2 credits)
- 2-4 × `ask_sherpa` from subagents (4-8 credits)
- 1 × `get_feedback` synthesis (2 credits)
- **Total: ~10-14 credits per Deep Research run**

That's well within the Free tier's 10 monthly credits for one run, or ~15-20 runs per month on the Starter plan.
