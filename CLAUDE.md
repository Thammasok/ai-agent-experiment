# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This is a **skill definition system** for AI-driven software development workflows. It contains markdown files that define how AI agents should operate when assisting with software engineering tasks. This is not an executable application.

## Commands

No build, lint, or test commands exist. This repository contains skill definitions (markdown files), not executable code.

## Architecture

### Workflow Overview

The system implements an agentic software development workflow based on:
- **Shift-Left Testing** — Design tests before implementation
- **TDD (Red-Green-Refactor)** — Write failing test first, implement minimum code to pass
- **Just-Enough Architecture** — Design per scenario, not upfront
- **Human-in-the-Loop** — Human review is a mandatory gate before completion

### Skill System

Skills are defined in `.opencode/skills/[skill-name]/SKILL.md`. Each skill has a YAML frontmatter with `name` and `description`, followed by step-by-step guidance.

| Skill | Purpose |
|-------|---------|
| `business-analysis` | Requirements elicitation, user story mapping, FR/NFR specs |
| `software-tester-design` | Test scenario and test case design (SC-xxx, TC-xxx) |
| `project-management` | Iteration planning, task breakdown, release notes |
| `software-architecture` | API contracts, DB schemas, OpenAPI specs |
| `ai-orchestrator` | TDD development loop execution |
| `technical-writer` | User documentation after UAT passes |
| `software-tester-automation` | Automated test code implementation |
| `software-engineer` | General coding, debugging, code review |

### Workflow Stages

1. **Product Discovery** → BA gathers requirements, SWT designs test cases
2. **Iteration Planning** → PM breaks scenarios into iterations with Definition of Done (TC-xxx)
3. **Architecture** → Just-enough API/DB design per scenario
4. **Development Loop** → AI Orchestrator runs TDD: Red → Green → Refactor → Integrate → Test All
5. **UAT & Human Review** → Mandatory approval gate
6. **Documentation** → User docs after UAT, release notes at retrospect

### Key Artifacts

- **US-xxx** — User stories from business-analysis
- **SC-xxx** — Test scenarios from software-tester-design
- **TC-xxx** — Test cases (Definition of Done for implementation)
- **DEV-xxx** — Developer tasks from project-management
- **FR-xxx / NFR-xxx** — Functional and non-functional requirements

## Key Files

- `idea.md` — Workflow diagram and design decisions
- `AGENTS.md` — Code style guidelines for projects using these skills
- `.opencode/skills/*/SKILL.md` — Individual skill definitions

## Code Style (for projects using these skills)

When implementing in projects that use these skills:

- **TypeScript** preferred, `async/await` over callbacks
- **React**: Functional components + hooks, Server Components by default in Next.js 13+
- **API**: REST with Zod validation, consistent `{ data, error }` response format
- **Database**: Prisma ORM, snake_case tables, always include timestamps
- **Testing**: AAA pattern (Arrange-Act-Assert), test names include TC-ID
- **Naming**: kebab-case files, PascalCase components, camelCase functions
