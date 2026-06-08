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
   - Optional: target project to link action item tasks to
2. Parse the input to identify:
   - **Notes and decisions** — free-form content to preserve
   - **Action items** — tasks with an owner and/or due date
3. Create a Note using `mt_notes_create` with this structure:
   - **Meeting** — title, date, attendees
   - **Decisions** — key outcomes
   - **Notes** — full notes
   - **Action items** — bulleted list with owner and due date
4. If action items were found and a target project is available:
   - Use `mt_sections_list` to find an appropriate section (e.g., Backlog or To Do).
   - Create tasks using `mt_batch_execute` — fall back to individual `mt_tasks_create` calls if the batch call fails.
   - Add the Note URL as a comment on each task via `mt_tasks_comments_create`.
5. Return the Note URL and a list of any tasks created.

## Important

If no project is specified for action item tasks, ask before creating them. Confirm the action item list with the user before writing anything to MeisterTask.
