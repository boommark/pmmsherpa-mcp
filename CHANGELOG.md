# Changelog

All notable changes to the PMM Sherpa MCP server, skills, and docs are recorded here.

The server itself is versioned independently. This file tracks user-visible changes across the server, the skills, the docs, and the public repo.

The format is loosely based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [Unreleased]

## [1.2.0] — 2026-05-08

### Added

- **MCP credit system** is live. 2 credits per tool call, flat across all four tools. Free tier gets 10 monthly credits, Starter gets 200 monthly + topup packs ($5 / 50, $10 / 125, $15 / 200). Topups never expire. Founders are unmetered.
- **`scope_pmm_research`** tool. Senior PMM scoping for the planning phase of a Deep Research run. Returns angle, sub-questions, sources to weight, anti-patterns, success criteria.
- **Streaming default** for `ask_sherpa`. Perceived TTFB drops from ~14s warm to ~3s.
- **Phase-triggered tool descriptions**. Tools now self-describe when to use them across regular chat vs Deep Research planning vs Deep Research synthesis.
- **Public docs site** at `https://pmmsherpa.com/docs` with per-client setup pages.
- **Public GitHub repo** (this one) with hand-crafted README, skill files, examples, issue templates, and corpus request flow.
- **Skill files** for Claude.ai (zip), Claude Code (folder), and ChatGPT (custom instructions).

### Changed

- ChatGPT setup now includes the tightened ~1,200-char custom-instructions block. Previous version was too long for ChatGPT's field limit.
- Layer 4 voice rule on em-dashes is now absolute: never, anywhere. Prior version said "use sparingly".

### Fixed

- Langfuse trace name for MCP calls now uses `mcp.tool.<tool_name>` so traffic is filterable by tool at the trace level (was being set on a child span only).

## [1.1.0] — 2026-05-01

### Added

- **MCP server Phase 1 + 2** shipped to production at `https://pmmsherpa.com/api/mcp`.
- OAuth 2.1 with PKCE for Claude.ai, Claude Code, ChatGPT, Codex, Gemini CLI, and Antigravity.
- Three tools at launch: `ask_sherpa`, `draft_artifact`, `get_feedback`.
- 39-template artifact catalog for `draft_artifact`.

## [1.0.0] — 2025-Q4

### Added

- PMM Sherpa web app at `https://pmmsherpa.com`.
- 38,000+ chunk corpus across 9 knowledge layers.
- Hybrid RAG retrieval (70% semantic + 30% keyword).
- Free tier and Starter ($9.99/mo) plan.
