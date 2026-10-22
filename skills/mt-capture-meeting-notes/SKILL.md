---
name: mt-capture-meeting-notes
description: Create a Note in MeisterTask for a meeting, with action items automatically turned into tasks.
---

# Capture meeting notes

Use the MeisterTask MCP to save meeting notes as a Note and convert action items into MeisterTask tasks.

## Workflow

1. Gather the meeting details:
   - Meeting title and date
   - Attendees
   - Notes, decisions, and action items (user pastes or dictates)
   - Whether it's a recurring meeting, and its usual name
   - Optional: target project to link action item tasks to
2. Parse the input to identify:
   - **Notes and decisions** — free-form content to preserve
   - **Action items** — tasks with an owner and/or due date
3. Create a Note using `mt_notes_create` with this structure:
   - **Meeting** — title, date, attendees
   - **Decisions** — key outcomes
   - **Notes** — full notes
   - **Action items** — bulleted list with owner and due date
   - For a recurring meeting, create the Note as a child of a parent Note titled "<meeting name> notes" (for example "Marketing team meeting notes"), using `parentToken`. If a target project was given and the parent is in its Documents tab, use it. Otherwise search for that title with `mt_search` (types: ["NOTES"]) and ask the user before filing under a note it finds. If there's none, create it with `mt_notes_create`. Ask whether it should sit under a note the team already shares, such as a team note (pass that note's token as `parentToken`), so it's readable without extra sharing. A one-off meeting gets a standalone Note.
4. If action items were found and a target project is available:
   - Use `mt_sections_list` to find an appropriate section (e.g., Backlog or To Do).
   - Create tasks using `mt_batch_execute` — fall back to individual `mt_tasks_create` calls if the batch call fails.
   - Add the Note URL as a comment on each task via `mt_tasks_comments_create`.
5. If a target project is available, offer to add the Note to the project's Documents tab. Its title becomes visible to every project member.
   - For a recurring meeting, offer the parent Note, and only if it isn't in the tab yet. For a one-off meeting, offer the Note itself.
   - If the user agrees, use `mt_projects_documents_create` with the project ID and that note's token (the parent's, for a recurring meeting).
   - Only project admins can add documents. If the call fails, tell the user and carry on: any task comments still link the Note, and you return its URL anyway.
   - If the note was added: adding a note to a project doesn't share it. Ask the user whether project members should be able to read it. If so, list them with `mt_projects_members_list` and ask the user to share it (the parent Note, for a recurring meeting) with them in MeisterTask, since the MCP can't change note sharing. Sharing is set on top-level notes only and covers everything under them, so for a nested note, the user shares the top-level note above it.
6. Return the Note URL and a list of any tasks created.

## Important

If no project is specified for action item tasks, ask before creating them. Confirm the action item list with the user before writing anything to MeisterTask.
