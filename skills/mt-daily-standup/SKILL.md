---
name: mt-daily-standup
description: Summarize what you worked on yesterday and what's planned for today from your MeisterTask activity.
---

# Daily standup summary

Use the MeisterTask MCP to generate a standup-ready summary from your MeisterTask activity.

## Workflow

1. Identify the relevant projects:
   - Use `mt_search` (with `types: ["TASKS", "PROJECTS"]`) to surface recently active items, or ask the user directly which projects to include.
   - Ask the user to confirm which 1–3 projects to include rather than scanning all of them.
2. Fetch recent activity:
   - Use `mt_tasks_list` on each confirmed project to find tasks updated or completed in the last 24 hours.
   - Note: `mt_tasks_list` can time out on projects with 200+ tasks — if this happens, use `mt_search` filtered by project ID instead.
3. Fetch today's and upcoming tasks:
   - From the task lists, filter for tasks due today or overdue. Alternatively, use `mt_tasks_search` filtered by due date for large projects.
4. Draft the standup summary:
   - **Yesterday**: tasks completed or progressed (with task name and project context)
   - **Today**: tasks due today or planned next
   - **Blockers**: overdue tasks or open questions (only if found)
5. Keep it concise — no more than 5 bullets per section. Offer to post it or copy it.
6. Offer to save the standup as Notes, one per project, so each project's standups stay with that project and don't reach members of the others:
   - Each project gets one parent Note titled "<project name> standups". If it's in the project's Documents tab (`mt_projects_documents_list`), use it. Otherwise search for that title with `mt_search` (types: ["NOTES"]) and ask the user before filing under a note it finds. If there's none, create it with `mt_notes_create`. Ask whether it should sit under a note the team already shares, such as a team note (pass that note's token as `parentToken`), so it's readable without extra sharing.
   - Create a child note under that parent (`mt_notes_create` with `parentToken`) holding only that project's part of the standup.
   - For any parent not yet in its project's Documents tab, make one offer covering all of them, then add each with `mt_projects_documents_create` and the parent's token, so each tab holds one entry rather than one per standup. Only project admins can add documents; if a call fails, say so and carry on.
   - If a parent was added: adding a note to a project doesn't share it. Ask once whether those projects' members should be able to read their parent Note. If so, list them with `mt_projects_members_list` and ask the user to share the parent Note with them in MeisterTask, since the MCP can't change note sharing. Sharing is set on top-level notes only and covers everything under them, so for a nested note, the user shares the top-level note above it.

## Important

If no recent activity is found, say so clearly rather than inventing items. Ask the user to confirm the summary before they send it.
