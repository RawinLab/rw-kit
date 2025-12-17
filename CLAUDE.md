# Project Context - Rawinlab Claude Template

## Overview

This is a multi-agent orchestration template for software development. It enables autonomous collaboration between specialized AI agents (SA, Tech Lead, Team Lead, Frontend, Backend, Tester, QA) to complete development tasks from requirements to production-ready code.

## Tech Stack

> **IMPORTANT**: All agents MUST follow this tech stack. Do not use alternative technologies unless explicitly specified in the project.

### Frontend
- **Framework**: Next.js or React (project-specific)
- **UI Library**: Shadcn/ui (MUST USE - do not substitute)
- **State Management**: Zustand
- **Language**: TypeScript

### Backend
- **Framework**: NestJS
- **Language**: TypeScript
- **API Style**: REST

### Database
- **Database**: PostgreSQL or MySQL (project-specific)
- **ORM**: Prisma (MUST USE)

### Monorepo
- **Tool**: Turborepo
- **Structure**: Frontend, Backend, Database, and shared packages in single repository

### Testing
- **Unit Tests**: Jest (80%+ coverage required)
- **E2E Tests**: Playwright

### Authentication
- Custom authentication via Backend API

## Critical Rules for All Agents

### 1. ALWAYS Read Existing Code First
Before implementing anything:
- Search for existing implementations with `Explore` agent
- Understand current patterns and structures
- Avoid duplicate code
- Follow established conventions

### 2. Use Specialized Subagents
Leverage Claude Code's built-in agents:

| Task Type | Agent Full Name |
|-----------|-----------------|
| Database/Prisma | `backend-development:backend-architect` |
| API/NestJS | `backend-development:backend-architect` |
| UI/React/Next.js | `multi-platform-apps:frontend-developer` |
| Security Review | `full-stack-orchestration:security-auditor` |
| Unit/E2E Tests | `full-stack-orchestration:test-automator` |
| Performance | `full-stack-orchestration:performance-engineer` |
| TypeScript | `javascript-typescript:typescript-pro` |
| Debugging | `unit-testing:debugger` |
| Codebase Search | `Explore` |
| Implementation Plan | `Plan` |

Check available agents with `/agents` command.

### 3. Context-Aware Batch Scheduling (CRITICAL)

> **Reference**: See `.claude/kbs/scheduling-pattern.md` for full details.

#### The Problem
Running many parallel agents causes main context to fill up, making `/compact` impossible.

#### The Solution: Batch-Based Execution with Compaction + Minimal Output

```
📦 Batch 0 (5-7 agents + MINIMAL OUTPUT) → Poll → Complete → /compact
📦 Batch 1 (5-7 agents + MINIMAL OUTPUT) → Poll → Complete → /compact
📦 Batch N (5-7 agents + MINIMAL OUTPUT) → Poll → Complete → /compact
🧪 Unit Tests → Fix → /compact
🎭 E2E Tests → Fix → /compact
✅ Final Checks → Commit → Report
```

#### Key Rules:
1. **Maximum 5-7 agents per batch** - prevents context overflow
2. **Compact after each batch** - use `/compact` to free context
3. **ALWAYS use Minimal Output Template** - 99% context savings!
4. **Use subagents** - each agent has isolated context
5. **Verify via files** - check created files, don't parse agent output

#### Minimal Output Template (MUST USE)

**EVERY subagent prompt MUST end with this:**

```
---
RESPONSE FORMAT (CRITICAL):
When complete, respond with ONLY:
DONE: [1-2 sentence summary]
Files: [comma-separated list of files created/modified]

Do NOT include:
- Code snippets
- Full file contents
- Detailed explanations
- Logs or debug output
---
```

**Context Savings:**
| Method | Context Used |
|--------|--------------|
| Full agent output | ~5,000-20,000 tokens |
| With minimal template | ~50-100 tokens |
| **Savings per agent** | **99%+** |

### 4. Commit Frequently
- Commit after each completed task
- Write clear, descriptive commit messages
- Never commit broken code

### 5. Testing is Mandatory
- Run tests after implementation
- Fix failing tests before moving on
- No mock data for passing tests (be honest)

## Workflow Commands

| Command | Description |
|---------|-------------|
| `/project:plan-module` | Analyze requirements and create development plan |
| `/project:plan-to-todolist` | Convert plan to actionable todolist |
| `/project:execute` | Execute todolist with batch scheduling |
| `/project:implement` | Full workflow for feature/fix/enhancement |
| `/project:create-tests` | Generate unit tests (80%+ coverage) |
| `/project:create-e2e` | Generate Playwright E2E tests |
| `/project:test-coverage` | Analyze & improve test coverage |
| `/project:uat-test` | Run UAT testing with Lead Tester |
| `/project:qa-review` | Final QA review with smoke test |

## Knowledge Base References

| File | Description |
|------|-------------|
| `.claude/kbs/scheduling-pattern.md` | Batch execution pattern with minimal output |
| `.claude/kbs/context-management-guide.md` | 200k token limit strategies |
| `.claude/kbs/qa-checklist.md` | Comprehensive QA with mandatory smoke test |
| `.claude/kbs/test-writing-guide.md` | Jest & Playwright test templates |

## Custom Agents

| Agent | Role | Model |
|-------|------|-------|
| `sa-analyst` | Requirements analysis, business logic design | sonnet |
| `tech-lead` | Technical architecture, code design decisions | sonnet |
| `team-lead` | Task orchestration, agent assignment | opus |
| `lead-tester` | UAT testing, test case execution | sonnet |
| `qa-lead` | Final quality review, release approval | opus |

## File Naming Conventions

### Plan Files
```
plans/{main}-{sub}-{modulename}-plan.md
```
Example: `plans/1-1-user-registration-plan.md`

### TodoList Files
```
plans/{main}-{sub}-{modulename}-todolist.md
```
Example: `plans/1-1-user-registration-todolist.md`

### Report Files
```
docs/reports/yyyyMMddHHmm-{module}-{type}.md
```
Example: `docs/reports/202512171830-auth-execution-summary.md`

## Project Structure (Turborepo)

```
project-root/
├── apps/
│   ├── web/          # Next.js frontend
│   └── api/          # NestJS backend
├── packages/
│   ├── ui/           # Shared UI components (Shadcn)
│   ├── database/     # Prisma schema and client
│   ├── config/       # Shared configurations
│   └── types/        # Shared TypeScript types
├── plans/            # Plans and todolists
├── docs/reports/     # Execution reports
├── e2e/              # Playwright E2E tests
├── turbo.json
└── package.json
```

## Quality Gates

> **CRITICAL**: Build passing ≠ Application working!
> Always run `npm run dev` as the FIRST QA step!

### Before Module Completion:
- [ ] **Smoke test passed** - `npm run dev` starts without errors
- [ ] **API health check** - `/api/health` responds
- [ ] **Frontend responds** - Main page loads
- [ ] All tasks in todolist completed
- [ ] Unit test coverage >80%
- [ ] E2E tests passing
- [ ] Build and lint passing
- [ ] Changes committed

### Common Runtime Errors:
| Error | Cause | Fix |
|-------|-------|-----|
| `Nest can't resolve dependencies` | Missing module import | Add module to `imports: []` |
| `Cannot find module` | Missing package | Run `npm install` |
| `ECONNREFUSED` | Database not running | Start PostgreSQL/MySQL |

> **Reference**: See `.claude/kbs/qa-checklist.md` for comprehensive QA checklist

## Agent Collaboration Flow

```
User Request
     │
     ▼
┌─────────────────────────────────────────┐
│  SA / Tech Lead (Parallel Analysis)     │
│  - Analyze requirements                 │
│  - Break down into modules              │
│  - Create development plan              │
└─────────────────┬───────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────┐
│  Team Lead (Orchestrator)               │
│  - Convert plan to dependency-driven    │
│    todolist                             │
│  - Assign tasks to specialized agents   │
│  - Monitor progress with batch          │
│    scheduling                           │
└─────────────────┬───────────────────────┘
                  │
     ┌────────────┼────────────┐
     ▼            ▼            ▼
┌─────────┐ ┌─────────┐ ┌─────────┐
│Frontend │ │Backend  │ │Database │
│Developer│ │Architect│ │Engineer │
└────┬────┘ └────┬────┘ └────┬────┘
     │           │           │
     └───────────┼───────────┘
                 │
                 ▼ /compact after each batch
                 │
┌─────────────────────────────────────────┐
│  Lead Tester                            │
│  - Smoke Test First (MANDATORY)         │
│  - Run UAT tests (Playwright)           │
│  - Report bugs to developers            │
│  - Verify fixes                         │
└─────────────────┬───────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────┐
│  QA Lead                                │
│  - Phase 0: Smoke Test (MANDATORY)      │
│  - Review quality                       │
│  - Pass → Document & Complete           │
│  - Fail → Return to Team Lead           │
└─────────────────────────────────────────┘
```

## Quick Reference: Context Management

```bash
# Check current context usage
/context

# Compact conversation (summarize history)
/compact

# Clear and start fresh
/clear

# List running tasks
/tasks
```

## Batch Execution Quick Reference

```
📦 Batch 0 (5-7 agents) → Poll → ✅ → /compact
📦 Batch 1 (5-7 agents) → Poll → ✅ → /compact
📦 Batch N (5-7 agents) → Poll → ✅ → /compact
🧪 Unit Tests → Fix → /compact
🎭 E2E Tests → Fix → /compact
🚀 Smoke Test (MANDATORY) → npm run dev → Health checks
✅ Final Checks → Commit → Report
```
