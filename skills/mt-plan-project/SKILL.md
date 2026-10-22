---
name: mt-plan-project
description: Turn a goal or brief into a new MeisterTask project with sections and an initial set of tasks.
---

# Plan a MeisterTask project

Use the MeisterTask MCP to create a structured project from a goal or brief.

## Workflow

1. Gather the project details:
   - Project name (required)
   - Goal or brief, as text, a Note, or links to specs, designs or shared folders
   - Key phases or workstreams (to become sections)
   - Known tasks or deliverables
   - Optional: team members to invite, due dates
2. Propose the project structure:
   - Suggest 3–5 sections based on the brief (e.g., Backlog, In Progress, Review, Done — or phase-based names like Discovery, Build, Launch).
   - Say that the brief and any reference links will be added to the project's Documents tab.
   - Confirm with the user before creating.
3. Create the project using `mt_projects_create`.
4. Create sections using `mt_sections_create` (one call per section).
5. Create initial tasks:
   - Try `mt_batch_execute` first — use negative temp IDs for tasks that reference each other.
   - If the batch call fails, fall back to individual `mt_tasks_create` calls (one per task).
6. If team members were specified, invite them using `mt_projects_invite`.
7. Add the brief and reference material to the project's Documents tab with `mt_projects_documents_create`:
   - If the brief is already a Note, add it by its note token.
   - If the brief was pasted into the chat or lives somewhere else, offer to save it as a Note with `mt_notes_create`, so it has a durable home next to the project. Then add that Note.
   - Add reference links by URL. If adding a link fails because the account has links turned off, say so and offer to list the links in a Note instead.
   - If the note was added: adding a note to a project doesn't share it. Ask the user whether project members should be able to read it. If so, list them with `mt_projects_members_list` and ask the user to share the note with them in MeisterTask, since the MCP can't change note sharing.
8. Return the project URL and a summary of what was created.

## Important

Don't create more than 20 tasks without confirming scope with the user first. If the brief is vague, propose a structure and wait for approval before writing anything. The Documents tab takes notes and links only (files are uploaded in MeisterTask itself) and holds at most 50 documents per project.
