# Rawinlab Claude Template

Multi-Agent Orchestration Template for Software Development with Claude Code.

## Overview

This template enables autonomous collaboration between specialized AI agents to complete development tasks from requirements to production-ready code.

```
User → SA → Tech Lead → Team Lead → Developers → Tester → QA → Done!
```

### Key Features

- **Context-Aware Batch Scheduling** - Prevents context overflow with batched execution
- **Minimal Output Template** - 99% context savings per agent
- **Mandatory Smoke Testing** - Build passing ≠ Application working
- **9 Slash Commands** - Full development lifecycle coverage
- **5 Custom Agents** - Specialized roles for orchestration
- **4 Knowledge Base Files** - Best practices and patterns

## Quick Start

### 1. Copy Template to Your Project

```bash
# Copy .claude folder and CLAUDE.md to your project
cp -r rawinlab-claude-template/.claude your-project/
cp rawinlab-claude-template/CLAUDE.md your-project/
```

### 2. Customize CLAUDE.md

Edit `CLAUDE.md` to match your project's tech stack.

### 3. Create Required Folders

```bash
mkdir -p your-project/plans
mkdir -p your-project/docs/reports
```

### 4. Start Using Commands

```bash
cd your-project
claude  # Start Claude Code

# Then use commands:
/project:plan-module requirements/your-spec.md
```

## Project Structure

```
your-project/
├── .claude/
│   ├── commands/project/     # Slash commands
│   │   ├── plan-module.md
│   │   ├── plan-to-todolist.md
│   │   ├── execute.md
│   │   ├── implement.md        # NEW
│   │   ├── create-tests.md     # NEW
│   │   ├── create-e2e.md       # NEW
│   │   ├── test-coverage.md    # NEW
│   │   ├── uat-test.md
│   │   └── qa-review.md
│   ├── agents/                 # Custom agents
│   │   ├── sa-analyst.md
│   │   ├── tech-lead.md
│   │   ├── team-lead.md
│   │   ├── lead-tester.md
│   │   └── qa-lead.md
│   └── kbs/                    # Knowledge base
│       ├── scheduling-pattern.md
│       ├── context-management-guide.md
│       ├── qa-checklist.md
│       └── test-writing-guide.md
├── CLAUDE.md                   # Project context
├── plans/                      # Plans & todolists
├── docs/reports/               # Reports & summaries
└── README.md
```

## Commands

### Core Workflow Commands

| Command | Description |
|---------|-------------|
| `/project:plan-module <file>` | Analyze requirements → create plan |
| `/project:plan-to-todolist <file>` | Convert plan → todolist |
| `/project:execute <file>` | Execute todolist with batch scheduling |
| `/project:uat-test <file>` | Run UAT testing |
| `/project:qa-review <module>` | Final QA review with smoke test |

### Additional Commands

| Command | Description |
|---------|-------------|
| `/project:implement <feature> <type>` | Full workflow (feature/fix/enhancement) |
| `/project:create-tests <file>` | Generate unit tests (80%+ coverage) |
| `/project:create-e2e <file>` | Generate Playwright E2E tests |
| `/project:test-coverage <target>` | Analyze & improve test coverage |

### Usage Examples

```bash
# Full workflow for a feature
/project:implement user-auth feature

# Step-by-step approach
/project:plan-module requirements/project-spec.md
/project:plan-to-todolist plans/1-1-auth-plan.md
/project:execute plans/1-1-auth-todolist.md
/project:uat-test plans/1-1-auth-todolist.md
/project:qa-review 1-1-auth

# Testing commands
/project:create-tests apps/api/src/auth/auth.service.ts
/project:create-e2e plans/1-1-auth-todolist.md
/project:test-coverage 85
```

## Custom Agents

### Project-Specific Agents

| Agent | Role | Model |
|-------|------|-------|
| `sa-analyst` | System Analyst - Requirements analysis | sonnet |
| `tech-lead` | Tech Lead - Architecture, API design | sonnet |
| `team-lead` | Team Lead - Task orchestration | opus |
| `lead-tester` | Lead Tester - UAT testing | sonnet |
| `qa-lead` | QA Lead - Final review, smoke test | opus |

### Built-in Agents (Claude Code)

| Agent | Specialty |
|-------|-----------|
| `multi-platform-apps:frontend-developer` | React, Next.js, UI |
| `backend-development:backend-architect` | NestJS, API, services |
| `full-stack-orchestration:security-auditor` | Security review |
| `full-stack-orchestration:test-automator` | Test automation |
| `javascript-typescript:typescript-pro` | TypeScript patterns |
| `unit-testing:debugger` | Debugging, test failures |
| `Explore` | Codebase exploration |
| `Plan` | Implementation planning |

Check all agents: `/agents`

## Workflow

```
┌─────────────────────────────────────────────────────────────┐
│  STEP 1: Planning                                           │
│  /project:plan-module                                       │
│  Agents: sa-analyst, tech-lead (parallel)                   │
│  Output: plans/*-plan.md                                    │
└─────────────────────────────┬───────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│  STEP 2: TodoList                                           │
│  /project:plan-to-todolist                                  │
│  Agents: team-lead                                          │
│  Output: plans/*-todolist.md (dependency-driven format)     │
└─────────────────────────────┬───────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│  STEP 3: Execute (Batch Scheduling)                         │
│  /project:execute                                           │
│  📦 Batch 0 (5-7 agents) → /compact                         │
│  📦 Batch 1 (5-7 agents) → /compact                         │
│  🧪 Unit Tests → Fix → /compact                             │
│  🎭 E2E Tests → Fix → /compact                              │
│  🚀 Smoke Test (MANDATORY)                                  │
│  Output: Code + Tests + Updated TodoList                    │
└─────────────────────────────┬───────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│  STEP 4: UAT Testing                                        │
│  /project:uat-test                                          │
│  Agents: lead-tester                                        │
│  🚀 Smoke Test First (MANDATORY)                            │
│  Output: Test Report, Bug Fixes                             │
└─────────────────────────────┬───────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│  STEP 5: QA Review                                          │
│  /project:qa-review                                         │
│  Agents: qa-lead                                            │
│  🚀 Phase 0: Smoke Test (MANDATORY - Do First!)             │
│  ✅ Pass → Done!                                            │
│  ❌ Fail → Back to Step 3                                   │
└─────────────────────────────────────────────────────────────┘
```

## Context Management

### The Problem

Running many parallel agents causes main context to fill up quickly.

### The Solution: Batch-Based Execution

```
📦 Batch 0 (5-7 agents + MINIMAL OUTPUT) → /compact
📦 Batch 1 (5-7 agents + MINIMAL OUTPUT) → /compact
📦 Batch N (5-7 agents + MINIMAL OUTPUT) → /compact
🧪 Unit Tests → Fix → /compact
🎭 E2E Tests → Fix → /compact
✅ Final Checks → Commit → Report
```

### Minimal Output Template

**CRITICAL**: Always add this to subagent prompts:

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

**Context Savings**: ~99% reduction per agent!

> See `.claude/kbs/scheduling-pattern.md` for full details.

## Knowledge Base (kbs)

| File | Description |
|------|-------------|
| `scheduling-pattern.md` | Batch execution pattern with minimal output |
| `context-management-guide.md` | 200k token limit strategies |
| `qa-checklist.md` | Comprehensive QA with smoke test |
| `test-writing-guide.md` | Jest & Playwright templates |

## Tech Stack (Default)

| Category | Technology |
|----------|------------|
| Frontend | Next.js / React |
| UI Library | Shadcn/ui |
| State | Zustand |
| Backend | NestJS |
| Language | TypeScript |
| Database | PostgreSQL / MySQL |
| ORM | Prisma |
| Monorepo | Turborepo |
| Unit Test | Jest |
| E2E Test | Playwright |

Customize in `CLAUDE.md` for your project.

## Quality Gates

> **CRITICAL**: Build passing ≠ Application working!

### Before Module Completion:
- [ ] **Smoke test passed** - `npm run dev` starts without errors
- [ ] **API health check** - `/api/health` responds
- [ ] **Frontend responds** - Main page loads
- [ ] All tasks in todolist completed
- [ ] Unit test coverage >80%
- [ ] E2E tests passing
- [ ] Build and lint passing

### Common Runtime Errors:
| Error | Fix |
|-------|-----|
| `Nest can't resolve dependencies` | Add module to `imports: []` |
| `Cannot find module` | Run `npm install` |
| `ECONNREFUSED` | Start database |

## Best Practices

### 1. Always Read Existing Code
All agents are configured to read existing code before implementing.

### 2. Use Batch Execution
Maximum 5-7 agents per batch, compact after each batch.

### 3. Minimal Output Template
Always use the minimal output template for subagents.

### 4. Smoke Test First
Run `npm run dev` before any other QA checks.

### 5. Commit Frequently
Changes are committed after each completed task.

### 6. Test Everything
- Unit tests with Jest (80%+ coverage)
- E2E tests with Playwright
- No mock data for UAT

### 7. Use /compact
When context exceeds 60%, use `/compact` to free context.

## Customization

### Adding New Commands

Create `.claude/commands/project/your-command.md`:

```markdown
---
description: Your command description
argument-hint: <arguments>
model: sonnet
---

Your prompt here with $ARGUMENTS placeholder.

> **Reference**: See `.claude/kbs/scheduling-pattern.md` for context management.
```

### Adding New Agents

Create `.claude/agents/your-agent.md`:

```markdown
---
name: your-agent
description: When to use this agent. Use PROACTIVELY for auto-delegation.
model: sonnet
---

Your agent's system prompt and instructions.

## Context Management (CRITICAL)

> Follow the batch-based execution pattern from `.claude/kbs/scheduling-pattern.md`
```

## Troubleshooting

### Commands Not Working
1. Check YAML frontmatter has `---` at start and end
2. Ensure files are in correct directory
3. Restart Claude Code

### Context Too Large
Use `/compact` command to summarize and reduce context.

### Smoke Test Fails
1. Check for `Nest can't resolve dependencies` errors
2. Verify all modules are properly imported
3. Check database is running

### Agents Not Auto-Delegating
1. Include "PROACTIVELY" in agent description
2. Make description clear about when to use

## License

MIT
