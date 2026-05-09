# Security Policy

## Reporting a vulnerability

If you've found a security vulnerability in the PMM Sherpa MCP server, the OAuth flow, the docs site, or this public repo, please **do not open a public issue**.

Instead, email **abhishekratna@gmail.com** with the subject line `[SECURITY] PMM Sherpa MCP <short title>`.

Include:

- A clear description of the vulnerability
- Steps to reproduce
- Affected component (server, OAuth, docs site, this repo)
- Your contact info so we can follow up
- Any proof-of-concept code or screenshots (please don't include real credentials)

## What to expect

- We aim to acknowledge within **48 hours** of receipt.
- We aim to ship a fix or mitigation within **7 days** for high-severity issues.
- We will credit you in the changelog and release notes if you'd like public attribution. Anonymous reports are welcome too.

## Scope

In scope:

- The MCP server at `https://pmmsherpa.com/api/mcp`
- The OAuth 2.1 + PKCE flow
- The docs site at `https://pmmsherpa.com/docs/*`
- The skill files, examples, and templates in this repo

Out of scope:

- Issues affecting third-party clients (Claude.ai, ChatGPT, etc.) themselves. Report those upstream.
- Theoretical attacks without a working proof of concept.
- Spam, phishing, or social engineering not involving a code-level vulnerability.
- Automated scanner output without a clear, reproducible exploit.

## Coordinated disclosure

We follow coordinated disclosure. Please give us a reasonable window to fix and ship before any public writeup. We're happy to coordinate timing on disclosure posts and CVEs.

## Bug bounty

We don't currently run a paid bounty program. We'll send a thank-you and credit you publicly (with your consent) if your report leads to a meaningful fix.
