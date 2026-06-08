---
name: mt-weekly-review
description: Surface overdue tasks, tasks due this week, and recently completed tasks across MeisterTask projects for a weekly review.
---

# Weekly Review

Use the MeisterTask MCP to run a structured weekly review across your MeisterTask projects.

## Workflow

1. Ask the user which projects to include — don't fetch all projects by default.
2. Fetch tasks per project using `mt_tasks_list`:
   - Identify overdue tasks (due date in the past, status open)
   - Identify tasks due within the next 7 days
   - Identify tasks completed in the last 7 days
   - Note: `mt_tasks_list` can time out on projects with 200+ tasks — use `mt_tasks_search` with a due date range filter for those instead.
3. Organize findings into three sections:
   - **Overdue** — past-due open tasks grouped by project
   - **Due this week** — upcoming tasks grouped by project
   - **Completed last week** — recently closed tasks grouped by project
4. Flag any projects with no activity in the last 7 days.
5. Offer to reschedule overdue tasks or create a Note to capture review notes.

## Important

If the user has many projects, ask which ones to include before fetching everything. Keep the output scannable — bullet points grouped by project, not a wall of text.
