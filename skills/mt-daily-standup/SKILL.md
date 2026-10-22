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
6. Offer to save the standup as a Note:
   - Keep every standup under one "Standups" parent Note. Look for it with `mt_search` (types: ["NOTES"]); create it with `mt_notes_create` on first use. If the search finds more than one, or one the user didn't create, ask which to use before creating the child.
   - Create the standup as a child note with `mt_notes_create` and `parentToken` set to the parent's token.
   - Offer to add the parent Note to the Documents tab of each project the standup covers, using `mt_projects_documents_create`. Check `mt_projects_documents_list` first, so it's only added once. Only project admins can add documents; if the call fails, say so and carry on.
   - If the note was added: adding a note to a project doesn't share it. Ask the user whether project members should be able to read it. If so, list them with `mt_projects_members_list` and ask the user to share the note with them in MeisterTask, since the MCP can't change note sharing.

## Important

If no recent activity is found, say so clearly rather than inventing items. Ask the user to confirm the summary before they send it.
