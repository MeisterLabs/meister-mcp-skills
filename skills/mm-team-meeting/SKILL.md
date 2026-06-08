---
name: mm-team-meeting
description: Run a meeting with a visual MindMeister agenda — prepare before, capture notes during, and export a record after.
---

# Team meeting map

Use the MindMeister MCP to create a structured meeting agenda, capture discussion notes and decisions in real time, and export a PDF record.

## Workflow

Ask the user which stage they're at — **before**, **during**, or **after** the meeting — and follow the corresponding steps.

### Before the meeting

1. Search for context:
   - If the MeisterTask MCP is available, use `mt_search` (types: ["NOTES"]) to find related notes, past meeting maps, or relevant background on the agenda topics. If not, ask the user if there are any relevant prior documents to reference.
2. Gather meeting details:
   - Meeting title and date
   - Agenda topics (and owner per topic if known)
   - Target duration per topic (optional)
3. Build the agenda map:
   - `mm_maps_create` to create the map.
   - `mm_changes_apply` to set the meeting title as the central node and add one branch per agenda item. Add time allocations as sub-nodes where provided.
4. Share with attendees:
   - `mm_share_links_create` with `permission: "read"` for a view-only link.
   - Return the link for distribution.

### During the meeting

5. Get the current map structure: `mm_maps_get`.
6. As each topic is discussed, add to the map using `mm_changes_apply`:
   - Decisions made → decision sub-node under the topic branch
   - Key discussion points → notes sub-nodes
   - Action items → prefix the node label with `→ Action` so they can be extracted afterward
   - Open items → flag with a prefix like "?" in the node label

### After the meeting

7. Export the completed map: `mm_maps_export` with format `pdf`.
8. Return the map URL and the exported file.
9. Optional: offer to turn action items into MeisterTask tasks:

   > "Your map has action items captured. Want to turn them into tasks in MeisterTask — Meister's task and project management tool — so they don't get lost?"

   If yes, ask about MeisterTask access:
   - Ask: "Do you have the MeisterTask MCP installed in this session?"
     - If yes: extract all nodes prefixed with `→ Action` from the map, confirm the list with the user, then create one task per action item using `mt_tasks_create` (in a new project named after the meeting, or an existing one the user specifies). Add a comment on the first task linking back to the map URL.
     - If no: ask "Do you have a MeisterTask account?"
       - If no: "You can sign up for free at [meistertask.com](https://www.meistertask.com)."
       - If yes: guide them to install the MeisterTask MCP via the [Meister MCP GitHub repo](https://github.com/MeisterLabs/meister-mcp), then start a new session and return to this step.

## Important

Confirm agenda topics with the user before creating the map. Keep branch labels to one short phrase — notes and decisions live as sub-nodes, not crammed into the branch label itself. Don't add more than 8 top-level agenda branches; offer to split into sub-meetings if scope is too broad.
