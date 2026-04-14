---
name: team
description: Break a task into parallel subtasks and dispatch multiple Claude agents simultaneously. Works like a dev team — architect, builder, reviewer, etc. all working at once.
disable-model-invocation: true
argument-hint: [task description]
allowed-tools: Agent, Read, Write, Edit, Bash, Glob, Grep, WebSearch, WebFetch
---

# Team Mode — Parallel Agent Dispatcher

You are a **team lead** coordinating multiple Claude agents to complete a task efficiently. The user's request is:

**$ARGUMENTS**

## Your Process

### Step 1: Analyze & Decompose

Read the task carefully. Break it into **independent, parallelizable subtasks**. Think about:

- What parts can be done simultaneously without depending on each other?
- What specialist roles are needed? (researcher, architect, builder, reviewer, designer, etc.)
- What's the critical path — what must happen first vs. what can happen in parallel?

Typical team compositions (pick what fits the task):

| Role | Good for |
|------|----------|
| **Researcher** | Finding info, reading docs, exploring codebases |
| **Architect** | Planning structure, designing systems, making decisions |
| **Builder** | Writing code, creating files, implementing features |
| **Reviewer** | Checking quality, finding bugs, security review |
| **Designer** | UI/UX, styling, layout, visual decisions |
| **Writer** | Documentation, README, comments, copy |
| **Tester** | Writing tests, running tests, edge cases |

### Step 2: Dispatch Agents in Parallel

**CRITICAL: Launch ALL independent agents in a SINGLE message using multiple Agent tool calls.** This is what makes them run in parallel. Do NOT launch them one at a time.

For each agent:
- Give it a clear, self-contained prompt with ALL the context it needs
- Tell it exactly what to produce (code, analysis, plan, etc.)
- Tell it where to write output if creating files
- Set `run_in_background: true` for agents whose results don't block other agents

Use the right subagent_type:
- `Explore` for research/codebase exploration
- `Plan` for architecture/design decisions
- `general-purpose` for implementation, writing, and everything else

### Step 3: Coordinate & Combine

After agents complete:
1. Review each agent's output
2. Resolve any conflicts between agents' work
3. Combine results into the final deliverable
4. If agents produced code in different files, make sure they integrate properly

### Step 4: Report

Give the user a brief summary:
- What each agent did
- What was produced
- Any decisions made or conflicts resolved
- Next steps if applicable

## Rules

- **Maximize parallelism.** The whole point is speed through parallel work. If 3 things can happen at once, launch 3 agents at once.
- **Keep agents focused.** Each agent should have ONE clear job. Don't give an agent 5 different tasks.
- **Provide full context.** Agents don't share memory. Each one needs all the info it requires in its prompt.
- **Use background agents** (`run_in_background: true`) when you don't need results before launching the next step.
- **2-5 agents is the sweet spot.** More than 5 has diminishing returns. Less than 2 defeats the purpose.
- **Sequential when necessary.** If step B depends on step A's output, run A first, then launch B. Don't force parallelism where it doesn't fit.

## Example Decomposition

**Task:** "Build a landing page for my SaaS product"

Parallel agents:
1. **Researcher** (Explore) — Look at the existing codebase, find the tech stack, check for existing components
2. **Designer** (general-purpose) — Design the layout, choose colors/fonts, plan sections
3. **Writer** (general-purpose) — Write the copy: headline, features, CTA, testimonials

Then sequential:
4. **Builder** (general-purpose) — Take outputs from all 3 and build the actual page

**Task:** "Review this PR for bugs and security issues"

Parallel agents:
1. **Bug Hunter** (Explore) — Look for logic errors, edge cases, race conditions
2. **Security Reviewer** (Explore) — Check for injection, auth issues, data leaks
3. **Performance Analyst** (Explore) — Check for N+1 queries, memory leaks, slow paths

Then:
4. **Summarizer** (general-purpose) — Combine all findings into a single review
