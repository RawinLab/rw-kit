# Rawinlab Claude Template

Multi-Agent Orchestration Template for Software Development with Claude Code.

## Overview

This template enables autonomous collaboration between specialized AI agents to complete development tasks from requirements to production-ready code.

```
User → SA → Tech Lead → Team Lead → Developers → Tester → QA → Done!
```

## Quick Start

### 1. Copy Template to Your Project

```bash
# Copy .claude folder and CLAUDE.md to your project
cp -r rawinlab-claude-template/.claude your-project/
cp rawinlab-claude-template/CLAUDE.md your-project/
```

### 2. Customize CLAUDE.md

Edit `CLAUDE.md` to match your project's tech stack.

### 3. Create Requirements Folder

```bash
mkdir -p your-project/requirements
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
│   ├── commands/           # Custom slash commands
│   │   ├── plan-module.md
│   │   ├── plan-to-todolist.md
│   │   ├── execute.md
│   │   ├── uat-test.md
│   │   └── qa-review.md
│   └── agents/             # Custom agents
│       ├── sa-analyst.md
│       ├── tech-lead.md
│       ├── team-lead.md
│       ├── lead-tester.md
│       └── qa-lead.md
├── CLAUDE.md               # Project context
├── requirements/           # Requirements & plans
└── README.md
```

## Commands

| Command | Description |
|---------|-------------|
| `/project:plan-module <file>` | Analyze requirements → create plan |
| `/project:plan-to-todolist <file>` | Convert plan → todolist |
| `/project:execute <file>` | Execute todolist with agents |
| `/project:uat-test <file>` | Run UAT testing |
| `/project:qa-review <module>` | Final QA review |

### Usage Examples

```bash
# Step 1: Create development plan
/project:plan-module requirements/project-spec.md

# Step 2: Convert to todolist
/project:plan-to-todolist requirements/1-1-auth-plan.md

# Step 3: Execute (implement code)
/project:execute requirements/1-1-auth-todolist.md

# Step 4: UAT Testing
/project:uat-test requirements/1-1-auth-todolist.md

# Step 5: QA Review
/project:qa-review 1-1-auth
```

## Custom Agents

### Project-Specific Agents

| Agent | Role | Description |
|-------|------|-------------|
| `sa-analyst` | System Analyst | Requirements analysis, feature specification |
| `tech-lead` | Tech Lead | Architecture, API design, technical decisions |
| `team-lead` | Team Lead | Task orchestration, agent assignment |
| `lead-tester` | Lead Tester | UAT testing, bug coordination |
| `qa-lead` | QA Lead | Final review, release approval |

### Built-in Agents (Claude Code)

| Agent | Specialty |
|-------|-----------|
| `frontend-developer` | React, Next.js, UI |
| `backend-architect` | NestJS, API, services |
| `security-auditor` | Security review |
| `test-automator` | Test automation |
| `Explore` | Codebase exploration |
| `Plan` | Implementation planning |

Check all agents: `/agents`

## Workflow

```
┌─────────────────────────────────────────────────────────────┐
│  STEP 1: Planning                                           │
│  /project:plan-module                                       │
│  Agents: sa-analyst, tech-lead                              │
│  Output: *-plan.md                                          │
└─────────────────────────────┬───────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│  STEP 2: TodoList                                           │
│  /project:plan-to-todolist                                  │
│  Agents: sa-analyst, tech-lead                              │
│  Output: *-todolist.md                                      │
└─────────────────────────────┬───────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│  STEP 3: Execute                                            │
│  /project:execute                                           │
│  Agents: team-lead → frontend-developer, backend-architect  │
│  Output: Code + Tests                                       │
└─────────────────────────────┬───────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│  STEP 4: UAT Testing                                        │
│  /project:uat-test                                          │
│  Agents: lead-tester                                        │
│  Output: Test Report, Bug Fixes                             │
└─────────────────────────────┬───────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│  STEP 5: QA Review                                          │
│  /project:qa-review                                         │
│  Agents: qa-lead                                            │
│  ✅ Pass → Done!                                            │
│  ❌ Fail → Back to Step 3                                   │
└─────────────────────────────────────────────────────────────┘
```

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

## File Naming Convention

| Type | Pattern | Example |
|------|---------|---------|
| Plan | `{main}-{sub}-{name}-plan.md` | `1-1-auth-plan.md` |
| TodoList | `{main}-{sub}-{name}-todolist.md` | `1-1-auth-todolist.md` |

## Best Practices

### 1. Always Read Existing Code
All agents are configured to read existing code before implementing.

### 2. Use Parallel Execution
The `team-lead` agent runs independent tasks in parallel.

### 3. Commit Frequently
Changes are committed after each completed task.

### 4. Test Everything
- Unit tests with Jest
- E2E tests with Playwright
- No mock data for UAT

### 5. Use /compact
When context becomes large, use `/compact` to reduce hallucination.

## Customization

### Adding New Commands

Create `.claude/commands/your-command.md`:

```markdown
---
description: Your command description
argument-hint: <arguments>
model: sonnet
---

Your prompt here with $ARGUMENTS placeholder.
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
```

## Troubleshooting

### Commands Not Working
1. Check YAML frontmatter has `---` at start and end
2. Ensure files are in correct directory
3. Restart Claude Code

### Agents Not Auto-Delegating
1. Include "PROACTIVELY" in agent description
2. Make description clear about when to use

### Context Too Large
Use `/compact` command to summarize and reduce context.

## License

MIT
