<p align="center">
  <img src="https://img.shields.io/badge/Claude_Code-Multi_Agent-blueviolet?style=for-the-badge&logo=anthropic" alt="Claude Code"/>
  <img src="https://img.shields.io/badge/Orchestration-Template-ff6b6b?style=for-the-badge" alt="Orchestration"/>
  <img src="https://img.shields.io/badge/Version-1.0-success?style=for-the-badge" alt="Version"/>
</p>

<h1 align="center">
  🤖 RW-Kit
</h1>

<h3 align="center">
  <em>Multi-Agent Orchestration Template for Claude Code</em>
</h3>

<p align="center">
  Transform your software development with autonomous AI agents that collaborate<br/>
  from requirements analysis to production-ready code.
</p>

<p align="center">
  <a href="#-quick-start">Quick Start</a> •
  <a href="#-commands">Commands</a> •
  <a href="#-agents">Agents</a> •
  <a href="#-workflow">Workflow</a> •
  <a href="#-best-practices">Best Practices</a>
</p>

---

## ✨ Features

<table>
<tr>
<td width="50%">

### 🎯 Smart Orchestration
- **5 Custom Agents** - SA, Tech Lead, Team Lead, Tester, QA
- **9 Slash Commands** - Full development lifecycle
- **Batch Scheduling** - Prevents context overflow

</td>
<td width="50%">

### 🚀 Production Ready
- **99% Context Savings** - Minimal output template
- **Mandatory Smoke Testing** - Build ≠ Working
- **4 Knowledge Bases** - Best practices built-in

</td>
</tr>
</table>

```
┌──────────────────────────────────────────────────────────────────┐
│                                                                  │
│   User Request                                                   │
│        │                                                         │
│        ▼                                                         │
│   ┌─────────┐    ┌───────────┐    ┌───────────┐                 │
│   │   SA    │───▶│ Tech Lead │───▶│ Team Lead │                 │
│   └─────────┘    └───────────┘    └─────┬─────┘                 │
│                                         │                        │
│              ┌──────────────────────────┼──────────────────┐    │
│              ▼                          ▼                  ▼    │
│         ┌─────────┐              ┌─────────┐        ┌─────────┐ │
│         │Frontend │              │ Backend │        │Database │ │
│         └────┬────┘              └────┬────┘        └────┬────┘ │
│              │                        │                  │      │
│              └────────────────────────┴──────────────────┘      │
│                                       │                          │
│                                       ▼                          │
│                              ┌─────────────────┐                 │
│                              │  Lead Tester    │                 │
│                              └────────┬────────┘                 │
│                                       │                          │
│                                       ▼                          │
│                              ┌─────────────────┐                 │
│                              │    QA Lead      │───▶  Done! ✅   │
│                              └─────────────────┘                 │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

---

## 🚀 Quick Start

### 1️⃣ Copy Template

```bash
# Copy .claude folder and CLAUDE.md to your project
cp -r rw-kit/.claude your-project/
cp rw-kit/CLAUDE.md your-project/
```

### 2️⃣ Create Required Folders

```bash
mkdir -p your-project/plans
mkdir -p your-project/docs/reports
```

### 3️⃣ Customize Configuration

Edit `CLAUDE.md` to match your tech stack.

### 4️⃣ Start Building

```bash
cd your-project
claude

# Use commands
/project:implement user-auth feature
```

---

## 📁 Project Structure

```
your-project/
│
├── 📂 .claude/
│   ├── 📂 commands/project/          # 🎮 Slash Commands
│   │   ├── plan-module.md
│   │   ├── plan-to-todolist.md
│   │   ├── execute.md
│   │   ├── implement.md
│   │   ├── create-tests.md
│   │   ├── create-e2e.md
│   │   ├── test-coverage.md
│   │   ├── uat-test.md
│   │   └── qa-review.md
│   │
│   ├── 📂 agents/                    # 🤖 Custom Agents
│   │   ├── sa-analyst.md
│   │   ├── tech-lead.md
│   │   ├── team-lead.md
│   │   ├── lead-tester.md
│   │   └── qa-lead.md
│   │
│   └── 📂 kbs/                       # 📚 Knowledge Base
│       ├── scheduling-pattern.md
│       ├── context-management-guide.md
│       ├── qa-checklist.md
│       └── test-writing-guide.md
│
├── 📄 CLAUDE.md                      # ⚙️ Project Configuration
├── 📂 plans/                         # 📋 Plans & Todolists
└── 📂 docs/reports/                  # 📊 Execution Reports
```

---

## 🎮 Commands

### Core Workflow

| Command | Description |
|:--------|:------------|
| `/project:plan-module` | 📝 Analyze requirements → Create development plan |
| `/project:plan-to-todolist` | ✅ Convert plan → Actionable todolist |
| `/project:execute` | ⚡ Execute todolist with batch scheduling |
| `/project:uat-test` | 🧪 Run UAT testing with Lead Tester |
| `/project:qa-review` | ✨ Final QA review with smoke test |

### Additional Commands

| Command | Description |
|:--------|:------------|
| `/project:implement` | 🔄 Full workflow (feature/fix/enhancement) |
| `/project:create-tests` | 🧬 Generate unit tests (80%+ coverage) |
| `/project:create-e2e` | 🎭 Generate Playwright E2E tests |
| `/project:test-coverage` | 📈 Analyze & improve test coverage |

### Usage Examples

```bash
# 🚀 Full workflow for a feature
/project:implement user-auth feature

# 📋 Step-by-step approach
/project:plan-module requirements/project-spec.md
/project:plan-to-todolist plans/1-1-auth-plan.md
/project:execute plans/1-1-auth-todolist.md
/project:uat-test plans/1-1-auth-todolist.md
/project:qa-review 1-1-auth

# 🧪 Testing commands
/project:create-tests apps/api/src/auth/auth.service.ts
/project:create-e2e plans/1-1-auth-todolist.md
/project:test-coverage 85
```

---

## 🤖 Agents

### Custom Project Agents

<table>
<tr>
<td align="center" width="20%">
<img src="https://img.shields.io/badge/-SA-4c1d95?style=for-the-badge" alt="SA"/><br/>
<b>sa-analyst</b><br/>
<sub>System Analyst</sub><br/>
<sub>Requirements & Logic</sub>
</td>
<td align="center" width="20%">
<img src="https://img.shields.io/badge/-Tech-0891b2?style=for-the-badge" alt="Tech"/><br/>
<b>tech-lead</b><br/>
<sub>Tech Lead</sub><br/>
<sub>Architecture & Design</sub>
</td>
<td align="center" width="20%">
<img src="https://img.shields.io/badge/-Team-059669?style=for-the-badge" alt="Team"/><br/>
<b>team-lead</b><br/>
<sub>Team Lead</sub><br/>
<sub>Orchestration</sub>
</td>
<td align="center" width="20%">
<img src="https://img.shields.io/badge/-Test-ea580c?style=for-the-badge" alt="Test"/><br/>
<b>lead-tester</b><br/>
<sub>Lead Tester</sub><br/>
<sub>UAT Testing</sub>
</td>
<td align="center" width="20%">
<img src="https://img.shields.io/badge/-QA-dc2626?style=for-the-badge" alt="QA"/><br/>
<b>qa-lead</b><br/>
<sub>QA Lead</sub><br/>
<sub>Final Review</sub>
</td>
</tr>
</table>

### Built-in Claude Code Agents

| Agent | Specialty |
|:------|:----------|
| `multi-platform-apps:frontend-developer` | React, Next.js, UI Components |
| `backend-development:backend-architect` | NestJS, API Design, Services |
| `full-stack-orchestration:security-auditor` | Security Review & Hardening |
| `full-stack-orchestration:test-automator` | Test Automation Strategies |
| `javascript-typescript:typescript-pro` | TypeScript Advanced Patterns |
| `unit-testing:debugger` | Debugging & Test Failures |
| `Explore` | Codebase Exploration |
| `Plan` | Implementation Planning |

> 💡 Check all available agents with `/agents` command

---

## 🔄 Workflow

```
╔═══════════════════════════════════════════════════════════════════╗
║                                                                   ║
║   📝 STEP 1: Planning                                             ║
║   ───────────────────                                             ║
║   Command: /project:plan-module                                   ║
║   Agents:  sa-analyst + tech-lead (parallel)                      ║
║   Output:  plans/*-plan.md                                        ║
║                                                                   ║
╠═══════════════════════════════════════════════════════════════════╣
║                           ⬇️                                       ║
╠═══════════════════════════════════════════════════════════════════╣
║                                                                   ║
║   ✅ STEP 2: TodoList                                             ║
║   ───────────────────                                             ║
║   Command: /project:plan-to-todolist                              ║
║   Agent:   team-lead                                              ║
║   Output:  plans/*-todolist.md (dependency-driven)                ║
║                                                                   ║
╠═══════════════════════════════════════════════════════════════════╣
║                           ⬇️                                       ║
╠═══════════════════════════════════════════════════════════════════╣
║                                                                   ║
║   ⚡ STEP 3: Execute (Batch Scheduling)                           ║
║   ─────────────────────────────────────                           ║
║   Command: /project:execute                                       ║
║                                                                   ║
║   📦 Batch 0 (5-7 agents) ────▶ /compact                          ║
║   📦 Batch 1 (5-7 agents) ────▶ /compact                          ║
║   📦 Batch N (5-7 agents) ────▶ /compact                          ║
║   🧪 Unit Tests ──────────────▶ Fix ──▶ /compact                  ║
║   🎭 E2E Tests ───────────────▶ Fix ──▶ /compact                  ║
║   🚀 Smoke Test (MANDATORY)                                       ║
║                                                                   ║
╠═══════════════════════════════════════════════════════════════════╣
║                           ⬇️                                       ║
╠═══════════════════════════════════════════════════════════════════╣
║                                                                   ║
║   🧪 STEP 4: UAT Testing                                          ║
║   ──────────────────────                                          ║
║   Command: /project:uat-test                                      ║
║   Agent:   lead-tester                                            ║
║   🚀 Smoke Test First (MANDATORY)                                 ║
║   Output:  Test Report, Bug Fixes                                 ║
║                                                                   ║
╠═══════════════════════════════════════════════════════════════════╣
║                           ⬇️                                       ║
╠═══════════════════════════════════════════════════════════════════╣
║                                                                   ║
║   ✨ STEP 5: QA Review                                            ║
║   ────────────────────                                            ║
║   Command: /project:qa-review                                     ║
║   Agent:   qa-lead                                                ║
║                                                                   ║
║   🚀 Phase 0: Smoke Test (MANDATORY)                              ║
║   ✅ Pass ───▶ Done!                                              ║
║   ❌ Fail ───▶ Back to Step 3                                     ║
║                                                                   ║
╚═══════════════════════════════════════════════════════════════════╝
```

---

## 🧠 Context Management

### The Problem

> Running many parallel agents causes main context to fill up quickly, making `/compact` impossible.

### The Solution: Batch-Based Execution

```
📦 Batch 0 (5-7 agents + MINIMAL OUTPUT) ────▶ /compact
📦 Batch 1 (5-7 agents + MINIMAL OUTPUT) ────▶ /compact
📦 Batch N (5-7 agents + MINIMAL OUTPUT) ────▶ /compact
🧪 Unit Tests ────▶ Fix ────▶ /compact
🎭 E2E Tests ────▶ Fix ────▶ /compact
✅ Final Checks ────▶ Commit ────▶ Report
```

### Minimal Output Template

> ⚠️ **CRITICAL**: Always add this to subagent prompts

```markdown
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

<table>
<tr>
<th>Method</th>
<th>Context Used</th>
<th>Savings</th>
</tr>
<tr>
<td>Full agent output</td>
<td>~5,000-20,000 tokens</td>
<td>-</td>
</tr>
<tr>
<td><b>With minimal template</b></td>
<td><b>~50-100 tokens</b></td>
<td><b>99%+ 🎉</b></td>
</tr>
</table>

---

## 🛠️ Tech Stack (Default)

<table>
<tr>
<td>

| Category | Technology |
|:---------|:-----------|
| **Frontend** | Next.js / React |
| **UI Library** | Shadcn/ui |
| **State** | Zustand |
| **Backend** | NestJS |
| **Language** | TypeScript |

</td>
<td>

| Category | Technology |
|:---------|:-----------|
| **Database** | PostgreSQL / MySQL |
| **ORM** | Prisma |
| **Monorepo** | Turborepo |
| **Unit Test** | Jest |
| **E2E Test** | Playwright |

</td>
</tr>
</table>

> 💡 Customize in `CLAUDE.md` for your project

---

## ✅ Quality Gates

> ⚠️ **CRITICAL**: Build passing ≠ Application working!

### Before Module Completion

- [ ] 🚀 **Smoke test passed** - `npm run dev` starts without errors
- [ ] 🏥 **API health check** - `/api/health` responds
- [ ] 🖥️ **Frontend responds** - Main page loads
- [ ] ✅ All tasks in todolist completed
- [ ] 📊 Unit test coverage >80%
- [ ] 🎭 E2E tests passing
- [ ] 🔨 Build and lint passing

### Common Runtime Errors

| Error | Cause | Fix |
|:------|:------|:----|
| `Nest can't resolve dependencies` | Missing module import | Add to `imports: []` |
| `Cannot find module` | Missing package | `npm install` |
| `ECONNREFUSED` | Database not running | Start PostgreSQL/MySQL |

---

## 📚 Knowledge Base

| File | Description |
|:-----|:------------|
| `scheduling-pattern.md` | 📦 Batch execution pattern with minimal output |
| `context-management-guide.md` | 🧠 200k token limit strategies |
| `qa-checklist.md` | ✅ Comprehensive QA with smoke test |
| `test-writing-guide.md` | 🧪 Jest & Playwright templates |

---

## 💡 Best Practices

<table>
<tr>
<td width="50%">

### 📖 Always Read First
All agents read existing code before implementing to avoid duplicates.

### 📦 Use Batch Execution
Maximum 5-7 agents per batch, compact after each.

### 📝 Minimal Output Template
Always use for subagents to save 99% context.

</td>
<td width="50%">

### 🚀 Smoke Test First
Run `npm run dev` before any other QA checks.

### 💾 Commit Frequently
Changes committed after each completed task.

### 🧪 Test Everything
Unit tests (80%+) + E2E tests, no mocking for UAT.

</td>
</tr>
</table>

---

## 🔧 Customization

### Adding New Commands

Create `.claude/commands/project/your-command.md`:

```markdown
---
description: Your command description
argument-hint: <arguments>
model: sonnet
---

Your prompt here with $ARGUMENTS placeholder.

> **Reference**: See `.claude/kbs/scheduling-pattern.md`
```

### Adding New Agents

Create `.claude/agents/your-agent.md`:

```markdown
---
name: your-agent
description: When to use. Use PROACTIVELY for auto-delegation.
model: sonnet
---

Your agent's system prompt and instructions.
```

---

## ❓ Troubleshooting

<details>
<summary><b>Commands Not Working</b></summary>

1. Check YAML frontmatter has `---` at start and end
2. Ensure files are in correct directory
3. Restart Claude Code

</details>

<details>
<summary><b>Context Too Large</b></summary>

Use `/compact` command to summarize and reduce context.

</details>

<details>
<summary><b>Smoke Test Fails</b></summary>

1. Check for `Nest can't resolve dependencies` errors
2. Verify all modules are properly imported
3. Check database is running

</details>

<details>
<summary><b>Agents Not Auto-Delegating</b></summary>

1. Include "PROACTIVELY" in agent description
2. Make description clear about when to use

</details>

---

<p align="center">
  <sub>Built with ❤️ by <a href="https://github.com/rawinlab">Rawinlab</a></sub>
</p>

<p align="center">
  <a href="https://github.com/rawinlab/rw-kit/issues">Report Bug</a> •
  <a href="https://github.com/rawinlab/rw-kit/issues">Request Feature</a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square" alt="License"/>
</p>
