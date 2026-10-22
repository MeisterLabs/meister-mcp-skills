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
6. Offer to save the review as Notes, one per project, so each project's weekly reviews stay with that project and don't reach members of the others:
   - Each project gets one parent Note for its weekly reviews (for example "Website relaunch weekly reviews"). Look for it in the project's Documents tab (`mt_projects_documents_list`), then with `mt_search` (types: ["NOTES"]). If that finds more than one candidate, or only finds one outside the project's Documents tab that the user didn't create, ask which to use. Otherwise create it with `mt_notes_create` on first use.
   - Create a child note under that parent (`mt_notes_create` with `parentToken`) holding only that project's part of the review.
   - If the parent isn't in the project's Documents tab yet, offer to add it with `mt_projects_documents_create`, so the tab holds one entry rather than one per review. Only project admins can add documents; if the call fails, say so and carry on.
   - If the note was added: adding a note to a project doesn't share it. Ask the user whether project members should be able to read it. If so, list them with `mt_projects_members_list` and ask the user to share the note with them in MeisterTask, since the MCP can't change note sharing.

## Important

If the user has many projects, ask which ones to include before fetching everything. Keep the output scannable — bullet points grouped by project, not a wall of text.
