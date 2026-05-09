# Claude Code skill

This is the PMM Sherpa skill for Claude Code (the CLI and IDE extensions). Once installed, Claude Code auto-triggers Sherpa on PMM keywords and enforces Layer 4 voice across the session.

## What's in this folder

| File | Purpose |
|---|---|
| [`SKILL.md`](SKILL.md) | The skill itself. Claude Code loads it from `.claude/skills/pmm-sherpa/SKILL.md`. |
| [`README.md`](README.md) | This file. |

## Install

### Prerequisites

- Claude Code v2.1.83 or newer (skills support required)
- The PMM Sherpa MCP server already added:

```bash
claude mcp add pmm-sherpa --transport http https://pmmsherpa.com/api/mcp
```

OAuth flow opens on first call. Sign in with the same Google account as pmmsherpa.com.

### Per-project install

```bash
mkdir -p .claude/skills
git clone https://github.com/boommark/pmmsherpa-mcp.git /tmp/pmm-sherpa-repo
cp -r /tmp/pmm-sherpa-repo/skills/claude-code .claude/skills/pmm-sherpa
rm -rf /tmp/pmm-sherpa-repo
```

The skill loads automatically on the next Claude Code session in that project.

### Global install (recommended)

Cleaner. The skill is available across every project.

```bash
git clone https://github.com/boommark/pmmsherpa-mcp.git ~/.pmm-sherpa
mkdir -p ~/.claude/skills
ln -s ~/.pmm-sherpa/skills/claude-code ~/.claude/skills/pmm-sherpa
```

This symlinks the skill into your global `~/.claude/skills/` directory. Updates land instantly when you `git pull` in `~/.pmm-sherpa`.

### Verify

In a Claude Code session, type:

```
> /mcp
```

You should see `pmm-sherpa` listed as a connected MCP server with four tools.

Then prompt:

```
> See pmmsherpa.com. Help me create a battlecard against its top competitor.
```

You should see:

- `Skill(pmm-sherpa)` line in the output
- `Calling PMM Sherpa…` tool call with `mcp__pmm-sherpa__ask_sherpa` or `mcp__pmm-sherpa__draft_artifact`
- A response in Layer 4 voice

## Update

```bash
cd ~/.pmm-sherpa && git pull
```

The symlink picks up changes immediately. Restart your Claude Code session if a session was already running.

## What the skill does

The skill is a calling guide. It tells Claude Code:

- **When to call Sherpa** vs handle directly (file parsing, web fetch, image gen → Claude's native tools)
- **Which of the four tools** to pick by intent (`mcp__pmm-sherpa__ask_sherpa`, `draft_artifact`, `get_feedback`, `scope_pmm_research`)
- **How to phase Sherpa** across a Deep Research run (planning → search → synthesis)
- **How to preserve project context** when in a project with brand guidelines or ICP definitions
- **Voice rules**: never em-dashes, story before framework, single-question close, no consultant-speak, no naming corpus authors

## Tool namespace difference vs Claude.ai

In Claude Code, the tools are namespaced as `mcp__pmm-sherpa__<tool>`:

- `mcp__pmm-sherpa__ask_sherpa`
- `mcp__pmm-sherpa__draft_artifact`
- `mcp__pmm-sherpa__get_feedback`
- `mcp__pmm-sherpa__scope_pmm_research`

The skill handles this transparently. You don't need to type the full namespace.
