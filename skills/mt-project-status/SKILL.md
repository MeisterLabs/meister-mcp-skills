---
name: mt-project-status
description: Generate a current-state summary of a MeisterTask project showing task counts by section, overdue items, and recent activity.
---

# Project status

Use the MeisterTask MCP to generate a snapshot of a MeisterTask project's current state.

## Workflow

1. Identify the project:
   - Use `mt_projects_list` to find the relevant project.
   - If ambiguous, ask the user to choose.
2. Fetch project structure and tasks:
   - Use `mt_projects_get` for project metadata.
   - Use `mt_sections_list` to get all sections.
   - Use `mt_tasks_list` per section to get current tasks.
3. Summarize the project state:
   - **Open tasks by section** — count and key task names per section
   - **Overdue tasks** — open tasks with a past due date
   - **Recently completed** — tasks closed in the last 7 days
   - **Unassigned tasks** — open tasks with no assignee
4. Use `mt_search` with the project ID filter to surface recently active items if needed.
5. Present the summary in a clean, scannable format. Offer to save it as a Note.

## Important

For large projects, summarize rather than listing every task. Prioritize overdue items and unassigned blockers — those are the highest-signal items for a status update.
