---
name: mm-outline-to-map
description: Convert a structured text outline or bullet list into a MindMeister mind map.
---

# Outline to mind map

Use the MindMeister MCP to turn a structured outline into a MindMeister mind map.

## Workflow

1. Receive the outline:
   - Accept a plain-text or Markdown-formatted outline (bullet list, numbered list, or indented text).
   - Treat the top-level heading or first item as the central map topic.
2. Parse the hierarchy:
   - Map top-level items to first-level branches.
   - Map nested items to sub-nodes, preserving indentation depth.
   - Flag any items that are too long to work as node labels and suggest shorter versions.
3. Confirm structure with the user:
   - Show the proposed map structure before creating.
   - For outlines under 20 nodes, proceed without confirmation if the structure is unambiguous.
4. Create the map using `mm_maps_create`.
5. Apply the full node tree using `mm_changes_apply`.
6. Optionally apply a theme: use `mm_themes_list` to find options.
7. Return the map URL.

## Important

Node labels should be concise — ideally under 10 words. If an outline item is a full sentence, trim it to a keyword phrase before converting.
