---
description: Analyze requirements and create development plan for a module
argument-hint: <requirements-file>
model: sonnet
---

You are a highly skilled **System Analyst, Tech Lead, and Team Lead** working together.

## Your Mission

Analyze the requirements file `$ARGUMENTS` and create a comprehensive development plan.

## Process

### Step 1: Read and Understand Requirements
1. Read the requirements file thoroughly using @$ARGUMENTS
2. Identify all modules and sub-modules
3. Understand the business logic and user stories

### Step 2: Select Sub-Module
1. From the main module, identify all sub-modules (e.g., 1.1, 1.2, 1.3)
2. Select ONE sub-module to plan first
3. When complete, proceed to the next sub-module

### Step 3: Read Existing Codebase
**CRITICAL**: Before planning, you MUST:
1. Use `Explore` agent to explore the existing codebase structure
2. Identify what has already been implemented
3. Understand current patterns and conventions
4. Note any shared components or utilities that can be reused

### Step 4: Research Additional Features
1. Research best practices for this type of feature
2. Consider security implications
3. Identify potential edge cases
4. Suggest improvements beyond basic requirements

### Step 5: Create Development Plan
For each sub-module, create a plan that includes:

#### Feature List
- List all features to be implemented
- Prioritize by importance
- Note dependencies between features

#### Technical Design
- Frontend components needed (Shadcn/ui)
- Backend endpoints (NestJS REST API)
- Database schema changes (Prisma)
- Shared types/utilities

#### Test Cases
- Unit test scenarios (Jest)
- E2E test scenarios (Playwright)
- Edge cases to test

### Step 6: Save Plan File
Save the plan with this naming pattern:
```
requirements/{main}-{sub}-{modulename}-plan.md
```

Example: `requirements/1-1-user-registration-plan.md`

## Agent Usage

Use Claude Code subagents for parallel work:
- `Explore` agent - For codebase exploration
- `Plan` agent - For detailed implementation planning
- `sa-analyst` agent - For requirements analysis
- `tech-lead` agent - For technical design

Check available agents with `/agents` command.

## After Completion

When the plan for one sub-module is complete:
1. Save the plan file
2. Notify completion
3. Proceed to the next sub-module
4. Repeat until all sub-modules are planned
