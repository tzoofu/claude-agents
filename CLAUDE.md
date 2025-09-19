# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a Claude Code agents repository containing specialized agent definitions for various software engineering tasks. Each agent is defined in a markdown file with YAML frontmatter specifying its metadata and a detailed description of its capabilities and behavior.

## Commands

This repository contains only markdown files and has no build, test, or development commands. It serves as a configuration repository for Claude Code agents.

## High-Level Architecture

### Agent Definition Structure

Each agent is defined in a markdown file with the following structure:

1. **YAML Frontmatter** (lines 1-6):
   - `name`: The agent identifier
   - `description`: Usage guidelines including example scenarios with `<example>` tags
   - `model`: AI model to use (e.g., `sonnet`, `opus`)
   - `color`: UI color for the agent

2. **Agent Instructions** (after frontmatter):
   - Role description and expertise
   - Core responsibilities
   - Specific approach and methodology
   - Best practices and guidelines
   - Output format expectations

### Available Agents

The repository contains the following specialized agents:

**Core Development & Architecture:**
- **agent-orchestrator**: Coordinates multiple agents for complex tasks
- **backend-api-architect**: API design and backend architecture
- **code-reviewer**: Comprehensive code reviews focusing on security, performance, and best practices
- **database-architect**: Database design and optimization
- **debug-performance-expert**: Debugging and performance optimization
- **fullstack-frontend-expert**: Frontend development with full-stack awareness
- **secure-backend-architect**: Security-focused backend development
- **solution-architect**: Technology stack and architecture pattern guidance
- **system-surgeon**: Rapid diagnosis and surgical fixes of complex system issues

**Security & Quality Assurance:**
- **appsec-vulnerability-analyst**: Security assessments and vulnerability analysis
- **qa-automation-expert**: Quality assurance and test automation
- **test-strategy-architect**: Comprehensive testing strategies

**DevOps & Infrastructure:**
- **cicd-pipeline-optimizer**: CI/CD pipeline optimization and DevOps
- **cloud-devops-architect**: Cloud infrastructure and DevOps practices
- **platform-engineering-specialist**: Developer experience and internal platforms

**Specialized Domains:**
- **data-engineering-architect**: Data pipelines, ETL processes, and big data systems
- **mcp-integration-specialist**: Model Context Protocol servers, clients, and ecosystem management
- **mlops-ai-engineer**: Machine learning operations and AI model deployment
- **mobile-development-expert**: Mobile app development (React Native, Flutter, native)
- **technical-documentation-expert**: Technical writing and docs-as-code practices

**Product & Management:**
- **product-manager-expert**: Product management and task breakdown

### Working with Agent Definitions

When modifying or creating agent definitions:

1. Maintain the consistent YAML frontmatter format
2. Ensure descriptions include clear example scenarios with `<example>` tags
3. Provide detailed role descriptions and responsibilities
4. Include specific methodologies and best practices
5. Define clear output expectations for the agent

Each agent should be self-contained with all necessary context for its specialized domain.