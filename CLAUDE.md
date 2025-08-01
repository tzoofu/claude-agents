# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a Claude Code agents repository containing specialized agent definitions for various software engineering tasks. Each agent is defined in a markdown file with YAML frontmatter specifying its metadata and a detailed description of its capabilities and behavior.

## Commands

This repository contains only markdown files and has no build, test, or development commands. It serves as a configuration repository for Claude Code agents.

## High-Level Architecture

### Agent Definition Structure

Each agent is defined in a markdown file with the following structure:

1. **YAML Frontmatter** (lines 1-5):
   - `name`: The agent identifier
   - `description`: Usage guidelines including example scenarios
   - `color`: UI color for the agent

2. **Agent Instructions** (after frontmatter):
   - Role description and expertise
   - Core responsibilities
   - Specific approach and methodology
   - Best practices and guidelines
   - Output format expectations

### Available Agents

The repository contains the following specialized agents:

- **agent-orchestrator**: Coordinates multiple agents for complex tasks
- **appsec-vulnerability-analyst**: Security assessments and vulnerability analysis
- **backend-api-architect**: API design and backend architecture
- **cicd-pipeline-optimizer**: CI/CD pipeline optimization and DevOps
- **cloud-devops-architect**: Cloud infrastructure and DevOps practices
- **code-refactoring-architect**: Code refactoring and modernization
- **database-architect**: Database design and optimization
- **debug-performance-expert**: Debugging and performance optimization
- **fullstack-frontend-expert**: Frontend development with full-stack awareness
- **product-manager-expert**: Product management and task breakdown
- **qa-automation-expert**: Quality assurance and test automation
- **secure-backend-architect**: Security-focused backend development
- **test-strategy-architect**: Comprehensive testing strategies

### Working with Agent Definitions

When modifying or creating agent definitions:

1. Maintain the consistent YAML frontmatter format
2. Ensure descriptions include clear example scenarios with `<example>` tags
3. Provide detailed role descriptions and responsibilities
4. Include specific methodologies and best practices
5. Define clear output expectations for the agent

Each agent should be self-contained with all necessary context for its specialized domain.