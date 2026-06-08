# MeisterTask and MindMeister MCP skills

Agent skills for [MeisterTask](https://www.meistertask.com) and [MindMeister](https://www.mindmeister.com). Each skill gives your AI agent a ready-made workflow for a common task — planning a project, running a meeting, building a mind map, and more.

Skills follow the [Agent Skills](https://agentskills.io) open standard and work with Claude Code, Claude Desktop, claude.ai, and other supported agents.

## Prerequisites

These skills call the MeisterTask and MindMeister MCP servers. Install the one(s) you need first:

- **MeisterTask MCP** — required for all `mt-` skills. Setup instructions in the [MeisterTask MCP docs](https://support.meistertask.com/hc/en-us/articles/35486711538322).
- **MindMeister MCP** — required for all `mm-` skills. Setup instructions in the [MindMeister MCP docs](https://support.mindmeister.com/hc/en-us/articles/35527359488018).

A MeisterTask or MindMeister account is required.

## Install

### CLI agents (e.g. Claude Code)

We recommend the [skills CLI](https://github.com/vercel-labs/skills).

```bash
# Install all skills
npx skills add MeisterLabs/meister-mcp-skills

# Install a specific skill
npx skills add MeisterLabs/meister-mcp-skills --skill mt-plan-project
```

You can also copy any `SKILL.md` folder directly into your agent's skills directory.

### claude.ai or Claude Cowork

Ask Claude to install it for you from the skill's GitHub URL — for example:

> Use the skill creator to add this skill: https://github.com/MeisterLabs/meister-mcp-skills/blob/main/skills/mt-plan-project/SKILL.md

Organization admins can publish skills account-wide so the whole team gets them without uploading individually.

## MeisterTask skills

| Skill | Description |
|---|---|
| `mt-plan-project` | Turn a goal or brief into a project with sections and initial tasks |
| `mt-task-breakdown` | Break a high-level goal into a structured task list |
| `mt-capture-meeting-notes` | Save meeting notes as a Note and turn action items into tasks |
| `mt-project-status` | Summarize a project's current state: open tasks, overdue items, recent activity |
| `mt-daily-standup` | Generate a standup-ready summary from your recent activity |
| `mt-weekly-review` | Surface overdue, upcoming, and completed tasks across projects |
| `mt-project-proposal` | Create a structured proposal Note from a brief, ready for stakeholder review |
| `mt-note-to-project` | Convert an existing Note — a spec, brief, or proposal — into a project |

## MindMeister skills

| Skill | Description |
|---|---|
| `mm-brainstorm` | Create a new mind map from a topic, seed ideas, or unstructured notes |
| `mm-outline-to-map` | Convert a structured text outline into a mind map |
| `mm-team-meeting` | Run a meeting with a visual agenda map — prepare, capture notes, and export a record |
| `mm-lesson-plan` | Create a structured lesson plan map using a 5-branch pedagogical framework |
| `mm-concept-map` | Build a concept map showing how topics relate through labeled connections |
| `mm-strategic-plan` | Map out a strategy using SWOT, OKR, PESTLE, or a freeform structure |
| `mm-okr-map` | Create an OKR map with Objectives and measurable Key Results |

## Cross-product workflows

Several MindMeister skills can hand off to MeisterTask when both MCPs are installed — for example, turning an OKR map into a tracked project, or meeting action items into tasks. These steps are optional and only run if you have the MeisterTask MCP available.

## License

[MIT](LICENSE.md)
