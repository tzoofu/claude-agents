# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a Claude Code agents repository containing specialized agent definitions for various software engineering tasks. Each agent is defined in a markdown file with YAML frontmatter specifying its metadata and a detailed description of its capabilities and behavior.

## Repository Overview

No build, test, or run commands — this is a pure configuration repository of Claude Code agent definitions (markdown files only).

## High-Level Architecture

### Agent Definition Structure

Each agent is a single `.md` file with YAML frontmatter followed by free-form instructions:

```
---
name: <agent-identifier>        # used to invoke the agent
description: <usage guidelines> # must include <example> tags with user/assistant/commentary
model: sonnet | opus | haiku
color: <any CSS color name>
---

<Agent instructions body>
```

The `description` field is what Claude reads to decide *when* to spawn the agent. Every description should include at least two `<example>` blocks, each with `Context:`, `user:`, `assistant:`, and `<commentary>` elements.

The instructions body typically covers: role/expertise statement, core responsibilities, approach/methodology, and output format expectations.

### Available Agents

**Core Development & Architecture:**
- **agent-orchestrator**: Coordinates multiple agents for complex, multi-domain tasks
- **backend-api-architect**: API design, microservices, REST/GraphQL
- **code-reviewer**: Security, performance, and best-practice code reviews
- **database-architect**: Schema design, query optimization, data modeling
- **debug-performance-expert**: Debugging, memory leaks, performance bottlenecks
- **fullstack-frontend-expert**: Frontend with backend-integration awareness
- **legacy-modernization-architect**: Legacy migration, strangler fig, monolith decomposition
- **secure-backend-architect**: Security-first backend development
- **solution-architect**: Tech stack selection and architecture patterns
- **system-surgeon**: Rapid diagnosis and surgical fixes of production issues

**AI & ML:**
- **ai-model-developer**: ML model development, training, and evaluation
- **llm-integration-architect**: RAG systems, prompt engineering, vector databases
- **mlops-ai-engineer**: ML pipelines, model deployment, MLOps practices

**Security & Quality Assurance:**
- **appsec-vulnerability-analyst**: Security assessments, auth systems, vulnerability analysis
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
- **mr-review-resolver**: Auto-resolves all open GitLab MR review threads sequentially
- **technical-documentation-expert**: Technical writing, API docs, docs-as-code

**Product & Design:**
- **product-manager-expert**: Product management, feature planning, task breakdown
- **ui-ux-designer**: UI/UX design, design systems, visual improvements, accessibility

### Working with Agent Definitions

When modifying or creating agent definitions:

1. Keep `description` focused on *when to use*, not *what the agent does* — it drives automatic agent selection
2. `<example>` tags in the description must include `<commentary>` explaining the selection rationale
3. The instructions body should be self-contained — agents have no shared context
4. Match `model` to task complexity: `opus` for deep reasoning/architecture, `sonnet` for most tasks