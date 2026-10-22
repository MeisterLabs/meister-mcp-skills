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
   - Each project gets one parent Note titled "<project name> weekly reviews". If it's in the project's Documents tab (`mt_projects_documents_list`), use it. Otherwise search for that title with `mt_search` (types: ["NOTES"]) and ask the user before filing under a note it finds. If there's none, create it with `mt_notes_create`. Ask whether it should sit under a note the team already shares, such as a team note (pass that note's token as `parentToken`), so it's readable without extra sharing.
   - Create a child note under that parent (`mt_notes_create` with `parentToken`) holding only that project's part of the review.
   - For any parent not yet in its project's Documents tab, make one offer covering all of them, then add each with `mt_projects_documents_create` and the parent's token, so each tab holds one entry rather than one per review. Only project admins can add documents; if a call fails, say so and carry on.
   - If a parent was added: adding a note to a project doesn't share it. Ask once whether those projects' members should be able to read their parent Note. If so, list them with `mt_projects_members_list` and ask the user to share the parent Note with them in MeisterTask, since the MCP can't change note sharing. Sharing is set on top-level notes only and covers everything under them, so for a nested note, the user shares the top-level note above it.

## Important

If the user has many projects, ask which ones to include before fetching everything. Keep the output scannable — bullet points grouped by project, not a wall of text.
