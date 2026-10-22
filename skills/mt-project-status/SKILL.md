---
name: mt-project-status
description: Summarize a MeisterTask project's current state, or catch you up on it when you're new to it, with the project's goal, key documents, task counts by section, overdue items and recent activity.
---

# Project status

Use the MeisterTask MCP to generate a snapshot of a MeisterTask project's current state. It also works as a catch-up for someone new to the project.

## Workflow

1. Identify the project:
   - Use `mt_projects_list` to find the relevant project.
   - If ambiguous, ask the user to choose.
2. Fetch project structure and tasks:
   - Use `mt_projects_get` for project metadata. It includes a summary of the project's Documents tab; use `mt_projects_documents_list` if the project has more than 20 documents.
   - Use `mt_sections_list` to get all sections.
   - Use `mt_tasks_list` per section to get current tasks.
3. If the user wants context, not just status (for example "catch me up on this project", or they're new to it):
   - Read the key note documents with `mt_notes_get`, such as a brief, spec or plan.
   - For links, try any other tool available in your session that can open them, or a web fetch for public pages. Name any documents you couldn't read.
   - Open the summary with a short overview: the project's goal, key decisions, and where its main documents live.
4. Summarize the project state:
   - **Open tasks by section** — count and key task names per section
   - **Overdue tasks** — open tasks with a past due date
   - **Recently completed** — tasks closed in the last 7 days
   - **Unassigned tasks** — open tasks with no assignee
   - **Documents** — how many, and the key ones by name (only if the project has any)
5. Use `mt_search` with the project ID filter to surface recently active items if needed.
6. Present the summary in a clean, scannable format. Offer to save it as a Note:
   - Keep status updates under one parent Note titled "<project name> status updates". If it's among the documents fetched in step 2, use it. Otherwise search for that title with `mt_search` (types: ["NOTES"]) and ask the user before filing under a note it finds. If there's none, create it with `mt_notes_create`. Ask whether it should sit under a note the team already shares, such as a team note (pass that note's token as `parentToken`), so it's readable without extra sharing.
   - Create the summary as a child note with `mt_notes_create` and `parentToken` set to the parent's token.
   - If the parent isn't in the project's Documents tab yet, offer to add it with `mt_projects_documents_create` and the parent's token, so the tab holds one entry rather than one per update. Only project admins can add documents; if the call fails, say so and return the Note URL.
   - If the parent was added: adding a note to a project doesn't share it. Ask the user whether project members should be able to read it. If so, list them with `mt_projects_members_list` and ask the user to share the parent Note with them in MeisterTask, since the MCP can't change note sharing. Sharing is set on top-level notes only and covers everything under them, so for a nested note, the user shares the top-level note above it.

## Important

For large projects, summarize rather than listing every task. Prioritize overdue items and unassigned blockers — those are the highest-signal items for a status update.
