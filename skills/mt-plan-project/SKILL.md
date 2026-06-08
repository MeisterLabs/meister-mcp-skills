---
name: mt-plan-project
description: Turn a goal or brief into a new MeisterTask project with sections and an initial set of tasks.
---

# Plan a MeisterTask project

Use the MeisterTask MCP to create a structured project from a goal or brief.

## Workflow

1. Gather the project details:
   - Project name (required)
   - Goal or brief description
   - Key phases or workstreams (to become sections)
   - Known tasks or deliverables
   - Optional: team members to invite, due dates
2. Propose the project structure:
   - Suggest 3–5 sections based on the brief (e.g., Backlog, In Progress, Review, Done — or phase-based names like Discovery, Build, Launch).
   - Confirm with the user before creating.
3. Create the project using `mt_projects_create`.
4. Create sections using `mt_sections_create` (one call per section).
5. Create initial tasks:
   - Try `mt_batch_execute` first — use negative temp IDs for tasks that reference each other.
   - If the batch call fails, fall back to individual `mt_tasks_create` calls (one per task).
6. If team members were specified, invite them using `mt_projects_invite`.
7. Return the project URL and a summary of what was created.

## Important

Don't create more than 20 tasks without confirming scope with the user first. If the brief is vague, propose a structure and wait for approval before writing anything.
