---
name: mm-lesson-plan
description: Create a structured lesson plan mind map following a 5-branch pedagogical framework.
---

# Lesson plan map

Use the MindMeister MCP to build a lesson plan as a mind map. Searches existing notes for context first, then creates a structured map using a fixed 5-branch framework.

## Workflow

1. Gather lesson details:
   - Subject and topic
   - Year group or level
   - Duration
   - Any specific requirements or constraints
2. Search for existing content:
   - If the MeisterTask MCP is available, use `mt_search` (types: ["NOTES"]) to find existing lesson plans or notes on this topic. If not, ask the user if there are any existing plans to build on.
   - Use relevant content to inform the new plan — avoid duplicating work already done.
3. Build the lesson plan map using `mm_maps_create` and `mm_changes_apply` with this fixed 5-branch structure:
   - **Learning outcome** — the end goal: what students will know or be able to do by the end
   - **Assessment** — how success is measured; checks and success indicators
   - **Lesson flow** — stages from opener through core activity to reflection, each with a time allocation as a sub-node
   - **Resources** — links, questions, reading materials, support resources, extension tasks
   - **Post-class notes** — space for reflection after the lesson; what worked, what to change
4. Optionally:
   - Share with students: `mm_share_links_create` with `permission: "read"`
   - If they want a PDF to print or pass to a coordinator, tell them to export it from the MindMeister app. There's no export tool in the MCP.
5. Return the map URL.

## Important

Always confirm the lesson structure with the user before creating the map. For the Lesson flow branch, include time allocations on each stage even if approximate. The Post-class notes branch should be created empty — it's a placeholder to fill in after the lesson runs.
