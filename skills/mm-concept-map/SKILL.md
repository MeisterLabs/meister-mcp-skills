---
name: mm-concept-map
description: Build a concept map showing how topics relate to each other through explicitly labeled connections.
---

# Concept map

Use the MindMeister MCP to create a concept map with labeled relationships between topics — showing not just what the concepts are, but how they connect.

## Concept map vs. mind map

A mind map radiates ideas from a central topic. A concept map shows the *relationships* between any set of topics using labeled links ("causes", "is part of", "leads to", "requires"). Use this skill when the goal is to understand or explain a system of connected ideas, not just explore a single topic.

## Workflow

1. Gather the topic and scope:
   - What is the domain or central concept?
   - Who is the audience? (student revision, team onboarding, stakeholder explainer)
2. Search for existing content:
   - If the MeisterTask MCP is available, use `mt_search` (types: ["NOTES"]) to find existing notes or documents on this topic. If not, ask the user to describe any existing material to draw from.
   - Extract key concepts and any relationships already described in the found content.
3. Identify concepts and relationships:
   - Aim for 6–15 concepts relevant to the topic.
   - For each meaningful connection between concepts, define a short relationship label (1–4 words, active form: "causes", "enables", "is part of").
   - Confirm the concept list and relationship labels with the user before building.
4. Build the map using `mm_maps_create` and `mm_changes_apply`:
   - Place the central concept as the root node.
   - Group related concepts under shared parent branches.
   - Model relationships as labeled intermediate nodes or branches — the MindMeister API creates hierarchical maps, so free-form cross-branch arrows between non-sibling nodes aren't available. Acknowledge this if the user expects a traditional concept map layout.
5. Return the map URL.

## Important

Keep relationship labels short and active. Push back on vague connections — if the user can't name the relationship, the link probably shouldn't be in the map. For dense webs of relationships, suggest starting with the 5–6 most important connections rather than mapping everything at once.
