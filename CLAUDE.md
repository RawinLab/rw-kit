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
- **Unit Tests**: Jest
- **E2E Tests**: Playwright

### Authentication
- Custom authentication via Backend API

## Critical Rules for All Agents

### 1. ALWAYS Read Existing Code First
Before implementing anything:
- Search for existing implementations
- Understand current patterns and structures
- Avoid duplicate code
- Follow established conventions

### 2. Use Specialized Subagents
Leverage Claude Code's built-in agents when available:
- `frontend-developer` - UI/React components
- `backend-architect` - API/Services design
- `security-auditor` - Security review
- `test-automator` - Testing automation
- `Explore` - Codebase exploration
- `Plan` - Implementation planning

Check available agents with `/agents` command.

### 3. Parallel Execution
- Use subagents in parallel when tasks are independent
- Maximize efficiency by running multiple agents simultaneously
- Use `/compact` when context becomes large to reduce hallucination

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
| `/project:execute` | Execute todolist with Team Lead orchestration |
| `/project:uat-test` | Run UAT testing with Lead Tester |

## File Naming Conventions

### Plan Files
```
requirements/{main}-{sub}-{modulename}-plan.md
```
Example: `requirements/1-1-user-registration-plan.md`

### TodoList Files
```
requirements/{main}-{sub}-{modulename}-todolist.md
```
Example: `requirements/1-1-user-registration-todolist.md`

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
├── requirements/     # Requirements, plans, and todolists
├── turbo.json
└── package.json
```

## Agent Collaboration Flow

```
User Request
     │
     ▼
┌─────────────────────────────────────────┐
│  SA / Tech Lead / Team Lead             │
│  - Analyze requirements                 │
│  - Break down into modules              │
│  - Create development plan              │
└─────────────────┬───────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────┐
│  Team Lead (Orchestrator)               │
│  - Convert plan to todolist             │
│  - Assign tasks to specialized agents   │
│  - Monitor progress                     │
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
                 ▼
┌─────────────────────────────────────────┐
│  Lead Tester                            │
│  - Run UAT tests (Playwright)           │
│  - Report bugs to developers            │
│  - Verify fixes                         │
└─────────────────┬───────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────┐
│  QA Lead                                │
│  - Review quality                       │
│  - Pass → Document & Complete           │
│  - Fail → Return to Team Lead           │
└─────────────────────────────────────────┘
```
