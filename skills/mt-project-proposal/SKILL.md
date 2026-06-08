---
name: mt-project-proposal
description: Create a structured project proposal Note from a brief, ready for stakeholder review and handoff to note-to-project.
---

# Project proposal

Use the MeisterTask MCP to turn a project idea or brief into a structured proposal Note. Searches existing context first, drafts a structured document, and creates a Note ready for review. Designed to feed directly into the `mt-note-to-project` skill once approved.

## Workflow

1. Gather the brief:
   - What is the project or initiative?
   - Who is sponsoring or requesting it?
   - Any known constraints: budget, timeline, team size?
2. Search for existing context:
   - Use `mt_search` (types: ["NOTES", "PROJECTS"]) to find related prior decisions, existing projects, or OKR notes.
   - Use `mt_notes_get` on any relevant notes to extract useful context.
   - Surface conflicts or dependencies with existing work before drafting — not after.
3. Confirm the proposal outline with the user:
   - Present the 7 sections below and flag any gaps or conflicts found in step 2.
   - Get sign-off on scope before writing the full Note.
4. Create the proposal Note using `mt_notes_create` with this structure:
   - **Problem** — what problem or opportunity does this address?
   - **Proposed solution** — what will be built or done?
   - **Scope** — what's in scope, and what's explicitly out of scope?
   - **Timeline** — key milestones or phases with indicative dates
   - **Resources needed** — team, tools, budget
   - **Risks** — top 2–3 risks and proposed mitigations
   - **Open questions** — what needs to be decided before work can start?
5. Return the Note URL.

## Important

Don't skip the context search in step 2. Surface conflicts with existing work before drafting, not after. The proposal is designed to feed directly into `mt-note-to-project` — write scope and task descriptions with implementation in mind. If the brief is too vague to write a meaningful scope section, ask the user to clarify before proceeding.
