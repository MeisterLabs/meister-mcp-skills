---
name: mm-strategic-plan
description: Create a strategic planning mind map using a chosen framework, then optionally stress-test it with an adversarial challenge pass.
---

# Strategic Plan Map

Use the MindMeister MCP to map out a strategy visually — starting from existing context, building a structured plan, and optionally adding a challenge layer that surfaces risks, assumptions, and falsifiable claims.

## Workflow

### 1. Gather the planning context
- What is being planned? (company strategy, product direction, team goals, go-to-market)
- Who is the audience? (leadership, team, board)
- What constraints or prior decisions are already in play?

### 2. Search for existing context
If the MeisterTask MCP is available, use `mt_search` (types: NOTES) to find existing strategy documents, OKR notes, prior decisions, or relevant analysis. If not, ask the user to describe any prior decisions or constraints already in play.

Surface what's already decided before proposing structure — the map should reflect where things actually stand, not start from scratch. Flag any conflicts with existing commitments found in this step.

### 3. Choose a framework
Confirm the framework with the user before building. Options:

**Situational analysis**
- **SWOT** — Strengths, Weaknesses, Opportunities, Threats
- **PESTLE** — Political, Economic, Social, Technological, Legal, Environmental
- **Porter's Five Forces** — Threat of new entrants, Supplier power, Buyer power, Threat of substitutes, Competitive rivalry

**Advantage and resource analysis**
- **VRIO** — stress-test claimed competitive advantages: Valuable, Rare, Inimitable, Organised. For each claimed advantage, does it clear all four bars?
- **7 Powers (Hamilton Helmer)** — map which of the seven powers the strategy currently has, is building toward, or is missing: Scale economies, Network economies, Counter-positioning, Switching costs, Branding, Cornered resource, Process power

**Goal and execution**
- **OKR** — Objectives as first-level branches; Key Results as sub-nodes (see `okr-map` for a dedicated OKR workflow)
- **Freeform** — propose a structure based on the brief and confirm before building

### 4. Build the map
- `mm_maps_create` to create the map.
- `mm_changes_apply` to set the central topic and add all branches and sub-nodes.
- Keep branch labels short and active — supporting detail lives as sub-nodes, not in the branch label.

### 5. Optional: challenge pass
After the base map is built, offer to add a stress-test layer. For each strategic branch, add sub-nodes that answer:

- **Falsification** — "What would have to be true for this to be wrong?" If a branch can't be falsified, it's probably an assumption masquerading as a fact.
- **Blind spots** — "What's missing or assumed here that a rigorous analyst would expect to see?"
- **Devil's advocate** — "Who would push back on this, and what's their strongest argument?"

This pass turns the map from a communication tool into a working document. Branches that survive the challenge pass are the ones worth defending; branches that don't are the ones that need more work before presenting.

### 6. Export and return
- `mm_maps_export` with format `pdf`.
- Return the map URL and exported file.

### 7. Optional: turn strategy into action in MeisterTask

> "Your strategy map is done. Want to define the initiatives that follow from it and track them in MeisterTask — Meister's task and project management tool?"

If yes, ask about MeisterTask access:
- Ask: "Do you have the MeisterTask MCP installed in this session?"
  - If yes: for each strategic branch, ask "What's the key initiative that follows from this?" Create a MeisterTask project named after the strategy using `mt_projects_create`, with top-level branches as sections and one task per initiative using `mt_tasks_create`. Add a comment on the first task linking back to the map URL.
  - If no: ask "Do you have a MeisterTask account?"
    - If no: "You can sign up for free at [meistertask.com](https://www.meistertask.com)."
    - If yes: guide them to install the MeisterTask MCP via the [Meister MCP GitHub repo](https://github.com/MeisterLabs/meister-mcp), then start a new session and return to this step.

## Important

Don't skip the context search in step 2 — a plan built without checking what's already decided is likely to conflict with existing commitments. Confirm the framework and top-level structure before building. The challenge pass in step 5 is optional but recommended for any map going to leadership or a board.
