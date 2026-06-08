---
name: mt-task-breakdown
description: Break a high-level goal into a structured set of tasks in an existing MeisterTask project.
---

# Task Breakdown

Use the MeisterTask MCP to decompose a goal or feature into a concrete task list in MeisterTask.

## Workflow

1. Gather the input:
   - The goal, feature, or deliverable to break down
   - Target project and section (or offer to create a new section)
   - Optional: due date, assignee, sub-task depth
2. Identify the target project and section:
   - Use `mt_projects_list` and `mt_sections_list`.
   - If no section is specified, suggest an appropriate one or ask.
3. Generate the breakdown:
   - Propose 5–10 concrete, actionable tasks.
   - For complex tasks, suggest a checklist rather than creating separate sub-tasks.
   - Confirm the list with the user before creating anything.
4. Create tasks:
   - Try `mt_batch_execute` first (preferred for 3+ tasks).
   - If the batch call fails, fall back to individual `mt_tasks_create` calls.
5. For tasks needing checklists, use `mt_checklists_create` followed by `mt_checklist_items_create`.
6. Return a summary with task names and the project URL.

## Important

Aim for tasks completable in a single work session. Push back on vague tasks like "research X" — prompt the user to define a specific deliverable.
