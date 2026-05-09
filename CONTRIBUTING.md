# Contributing to PMM Sherpa MCP

Thanks for being here. This repo is the **public-facing mirror** for PMM Sherpa: docs, skill files, examples, and issue templates. The MCP server itself, the corpus, and the prompt-engineering are closed-source and live in a private repository.

That means: you can contribute docs, skills, and examples here. Server-side bugs and feature requests live here as issues but are fixed in the private repo.

## What we welcome

### 1. Bug reports

Found something broken in the MCP server, the docs, or a skill file? Open a [bug report](https://github.com/boommark/pmmsherpa-mcp/issues/new?template=bug_report.yml). Include:

- The client you were using (Claude.ai, Claude Code, ChatGPT, Codex, Gemini CLI, Antigravity)
- The tool that misbehaved (`ask_sherpa`, `draft_artifact`, `get_feedback`, `scope_pmm_research`)
- Your prompt and the response you got
- The trace ID if you have one (Sherpa surfaces these in error messages)

### 2. Feature requests

Want a new tool, a new artifact in the catalog, a new client connector documented, or a new feature in the credit system? Open a [feature request](https://github.com/boommark/pmmsherpa-mcp/issues/new?template=feature_request.yml).

### 3. Corpus requests

The corpus is curated, not crawled. We add books, AMAs, podcasts, and essays based on substance density. If you think we're missing something, open a [corpus request](https://github.com/boommark/pmmsherpa-mcp/issues/new?template=corpus_request.yml). Include:

- The source (book title, podcast name, essay URL)
- Why it belongs (one sharp paragraph)
- Where it fits (positioning, messaging, GTM, pricing, narrative, etc.)

### 4. Doc and skill PRs

PRs welcome on:

- `docs/*.mdx` (auto-syncs from `boommark/pmmsherpa` source repo, so PR there if possible)
- `skills/claude-ai/`, `skills/claude-code/`, `skills/chatgpt/`
- `examples/*.md`
- `README.md`, `CONTRIBUTING.md`, `SECURITY.md`

## Voice rules for any text PR

If you're writing copy that will end up in user-facing docs or skill files:

- **Never use em-dashes**. Use period, comma, colon, or parentheses instead.
- Open with the reader's situation, not preamble.
- Tell the story before naming the framework.
- Vary paragraph length. Long build. Short punch.
- Close with one question the reader takes away. Never a menu of options.
- Don't name authors, books, podcasts, or companies from the corpus. Reference principles.

These are the same rules Sherpa speaks by. Drift here breaks voice consistency for users who installed the skills.

## PR checklist

Before submitting:

- [ ] No em-dashes anywhere in the diff
- [ ] Links use markdown `[text](url)` format, never bare URLs
- [ ] Examples include the prompt AND the expected behavior, not just one
- [ ] If you touched a skill file, you tested it in the actual client (Claude.ai, Claude Code, or ChatGPT)
- [ ] `npm run lint` clean if you touched anything in `docs/` (run on the source repo)

## What we won't accept

- Server code or proposed server changes (we can't review what we can't merge)
- Skill files that introduce em-dashes or break Layer 4 voice
- Examples that name the corpus authors or books by name
- "Just for fun" additions that don't help a real PMM use case

## Getting help

Stuck? [Open a Discussion](https://github.com/boommark/pmmsherpa-mcp/discussions). Most questions are faster than an issue.

## License

By contributing, you agree your contributions are licensed under MIT (see [LICENSE](LICENSE)).
