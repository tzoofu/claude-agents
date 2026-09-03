# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

A pure configuration repository of Claude Code agent definitions — one markdown file per agent, no build, test, or run commands. This directory is `~/.claude/agents`, so every file here is live: saving a change immediately affects which agents the main session can spawn and how they behave.

Quick sanity check after editing frontmatter (each file must start with a `---` fence and declare `name` and `description`):

```bash
for f in *.md; do [ "$f" = CLAUDE.md ] && continue; head -1 "$f" | grep -q '^---$' && grep -q '^name:' "$f" && grep -q '^description:' "$f" || echo "BAD: $f"; done
```

Commits in this repo must use the personal `tzoofu` identity (repo-local git config), not the work identity, and carry no co-author trailers.

## Agent Definition Structure

Each agent is a single `.md` file with YAML frontmatter followed by free-form instructions:

```
---
name: <agent-identifier>        # used to invoke the agent
description: <usage guidelines> # must include <example> tags with Context/user/assistant/<commentary>
model: fable | opus | sonnet | haiku | inherit
effort: xhigh | high | medium | low   # optional; omit to inherit the session level
tools: <comma-separated allowlist>    # optional; omit for "all tools"
skills: [<skill-name>, ...]           # optional; skills preloaded into the agent
maxTurns: <n>                         # optional; only on bounded workflow agents
color: <any CSS color name>
---

<Agent instructions body>
```

The `description` field is what Claude reads to decide *when* to spawn the agent. Every description should include at least two `<example>` blocks, each with `Context:`, `user:`, `assistant:`, and `<commentary>` elements.

Two body shapes exist:

- **Advisory/expert agents** (the majority): role statement, core responsibilities, methodology, then a closing `## Report` section.
- **Workflow agents** (`anticipate-review`, `audit-and-stage`, `cache-leak-investigator`, `mr-review-resolver`): an `## Input contract` section stating what the caller must pass, numbered `## Step N:` sections, and a final report step. These are the ones that carry `maxTurns` and tight `tools` lists.

## Available Agents

**Core Development & Architecture:**
- **agent-orchestrator**: Coordinates multiple agents for complex, multi-domain tasks
- **backend-api-architect**: API design, microservices, REST/GraphQL
- **code-reviewer**: Security, performance, and best-practice code reviews (holds the Wiz scanner)
- **database-architect**: Schema design, query optimization, data modeling
- **debug-performance-expert**: Debugging, memory leaks, performance bottlenecks
- **fullstack-frontend-expert**: Frontend with backend-integration awareness
- **legacy-modernization-architect**: Legacy migration, strangler fig, monolith decomposition
- **secure-backend-architect**: Security-first backend development (holds the Wiz scanner)
- **solution-architect**: Tech stack selection and architecture patterns
- **system-surgeon**: Rapid diagnosis and surgical fixes of production issues

**Review & Investigation Workflows (GitLab-oriented):**
- **anticipate-review**: Read-only audit of an MR or local diff against a project's `.claude/rules/` tree; predicts reviewer findings
- **audit-and-stage**: Pre-commit pass — rules audit, library doc check via Context7/Ref, validation run, then selective `git add` of only this session's files
- **mr-review-resolver**: Sequentially fixes and replies to every open GitLab MR review thread
- **cache-leak-investigator**: Layer-by-layer forensics for stale/shared-data bugs across CDN, framework, and browser caches, with live Playwright reproduction

**AI & ML:**
- **ai-model-developer**: ML model development, training, and evaluation
- **llm-integration-architect**: RAG systems, prompt engineering, vector databases
- **mlops-ai-engineer**: ML pipelines, model deployment, MLOps practices

**Security & Quality Assurance:**
- **appsec-vulnerability-analyst**: Security assessments, auth systems, vulnerability analysis (holds the Wiz scanner)
- **qa-automation-expert**: QA automation strategy and test frameworks
- **test-strategy-architect**: Unit/integration/e2e testing across languages

**DevOps & Infrastructure:**
- **cicd-pipeline-optimizer**: CI/CD pipelines, build optimization, deployment strategies
- **cloud-devops-architect**: Cloud infrastructure, monitoring, deployment architecture
- **observability-sre-specialist**: Observability, SLOs, incident response, reliability
- **platform-engineering-specialist**: Internal developer platforms, self-service infrastructure

**Specialized Domains:**
- **accessibility-specialist**: WCAG compliance, ARIA, screen reader support
- **computer-use-specialist**: Browser and desktop GUI automation via Claude computer use
- **data-engineering-architect**: Data pipelines, ETL/ELT, big data systems
- **mcp-integration-specialist**: MCP server development, client integration, ecosystem management
- **mobile-development-expert**: React Native, Flutter, native iOS/Android
- **technical-documentation-expert**: Technical writing, API docs, docs-as-code

**Product & Design:**
- **product-manager-expert**: Product management, feature planning, task breakdown
- **ui-ux-designer**: UI/UX design, design systems, visual improvements, accessibility

## Working with Agent Definitions

When modifying or creating agent definitions:

1. Keep `description` focused on *when to use*, not *what the agent does* — it drives automatic agent selection
2. `<example>` tags in the description must include `<commentary>` explaining the selection rationale
3. The instructions body should be self-contained — agents have no shared context
4. Match `model` to task complexity: `fable` (top tier, ~2× opus cost) for the hardest long-horizon reasoning — multi-agent orchestration, architecture decisions, complex migrations, production surgery, and investigation or code-changing review agents (debugging, cache forensics, MR-comment resolution); `opus` for deep reasoning; `sonnet` for most tasks; `haiku` for lightweight ones (product-manager, tech-docs). Omit or use `inherit` (the default) to follow the main session's model
5. Set `effort` alongside `model`: `xhigh` for investigations and orchestration, `high` for security review and architecture, `low` for grep-and-verify loops and writing agents. Omit to inherit the session level
6. Restrict `tools` on advisory agents to Read, Grep, Glob, Write, WebSearch plus the Context7/Ref docs tools — only agents that change code get Edit and Bash. Agents that read code get `LSP` in `tools` and `lsp-code-navigation` in `skills`; React-touching agents get `vercel:react-best-practices`. Never hardcode model version strings (e.g. `claude-sonnet-4-...`) — use the tier names only
7. Security-capable agents (`appsec-vulnerability-analyst`, `code-reviewer`, `secure-backend-architect`) must keep the `mcp__wiz__*` tools in their `tools` list — the global CLAUDE.md delegates Wiz scans to them when the main session lacks the scanner
8. Every agent body ends with a `## Report` section defining the ≤300-word output shape
