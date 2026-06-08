---
name: mt-note-to-project
description: Convert an existing MeisterTask Note — a spec, brief, or proposal — into a structured MeisterTask project with sections and tasks.
---

# Note to project

Use the MeisterTask MCP to read an existing Note and scaffold it into a MeisterTask project. The Note is the spec; this skill turns it into something executable.

## Workflow

1. Identify the source note:
   - Ask the user for the Note URL or title.
   - If no URL is provided, use `mt_search` (types: ["NOTES"]) to find it.
   - Fetch the full content with `mt_notes_get`.
2. Parse the note for project structure:
   - Extract: goal or objective, key workstreams or phases, specific tasks or action items, stakeholders, timeline indicators.
   - Identify natural section groupings (phases, workstreams, or a standard Backlog / In Progress / Review / Done structure if the note doesn't suggest otherwise).
3. Propose the project structure to the user:
   - Proposed project name
   - Proposed sections (3–5) with brief rationale
   - Proposed initial tasks per section (summarised, not exhaustive)
   - **Confirm before creating anything.**
4. Create the project:
   - `mt_projects_create` with the proposed name.
   - `mt_sections_create` for each section (one call per section).
   - `mt_tasks_create` for each task. Try `mt_batch_execute` first for 3+ tasks; fall back to individual calls if it fails.
5. Link the source note back to the project:
   - `mt_tasks_comments_create` on the first task with the Note URL, so the source document is always one click away.
6. Return the project URL and a summary of what was created.

## Important

Always confirm the proposed structure before creating anything. If the note is ambiguous or underspecified, ask the user to clarify scope rather than guessing. Don't create more than 20 tasks without confirming first. This skill pairs well with `mt-project-proposal` — use that to write the Note, then this skill to execute it.
