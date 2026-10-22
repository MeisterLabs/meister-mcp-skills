---
name: mt-weekly-review
description: Surface overdue tasks, tasks due this week, and recently completed tasks across MeisterTask projects for a weekly review.
---

# Weekly review

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
5. Offer to reschedule overdue tasks.
6. Offer to save the review as a Note:
   - Keep every review under one "Weekly reviews" parent Note. Look for it with `mt_search` (types: ["NOTES"]); create it with `mt_notes_create` on first use. If the search finds more than one, or one the user didn't create, ask which to use before creating the child.
   - Create the review as a child note with `mt_notes_create` and `parentToken` set to the parent's token.
   - Offer to add the parent Note to the Documents tab of each project the review covers, using `mt_projects_documents_create`. Check `mt_projects_documents_list` first, so it's only added once. Only project admins can add documents; if the call fails, say so and carry on.
   - If the note was added: adding a note to a project doesn't share it. Ask the user whether project members should be able to read it. If so, list them with `mt_projects_members_list` and ask the user to share the note with them in MeisterTask, since the MCP can't change note sharing.

## Important

If the user has many projects, ask which ones to include before fetching everything. Keep the output scannable — bullet points grouped by project, not a wall of text.
