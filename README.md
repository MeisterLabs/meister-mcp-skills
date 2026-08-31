# MeisterTask and MindMeister skills for AI assistants

Agent skills for [MeisterTask](https://www.meistertask.com) and [MindMeister](https://www.mindmeister.com). Each skill gives your AI agent a ready-made workflow for a common task: planning a project, running a meeting, building a mind map, and more.

Skills follow the [Agent Skills](https://agentskills.io) open standard and work with Claude Code, Claude Desktop, claude.ai, ChatGPT, and other supported agents.

## Prerequisites

These skills need MeisterTask or MindMeister connected to your AI assistant. Set up whichever you need first:

- **Install the official app.** Find MeisterTask or MindMeister in your AI assistant's app directory and connect it. This is the quickest route: you sign in once and there is no connector URL or API key to handle.
- **MeisterTask MCP server** — an alternative route for all `mt-` skills, and the right one for Claude Code, IDE and CLI users. Setup instructions in the [MeisterTask MCP docs](https://support.meistertask.com/hc/en-us/articles/35486711538322).
- **MindMeister MCP server** — the same alternative route for all `mm-` skills. Setup instructions in the [MindMeister MCP docs](https://support.mindmeister.com/hc/en-us/articles/35527359488018).

A MeisterTask or MindMeister account is required.

The apps and these skills are separate things. The app connects your Meister data to your assistant; the skills are optional workflow templates that run on top of that connection. You can install either one without the other, but the skills only do anything useful once MeisterTask or MindMeister is connected.

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

### claude.ai, Claude Cowork, or ChatGPT

Ask your assistant to install the skill from its GitHub URL. For example:

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

Several MindMeister skills can hand off to MeisterTask when both products are connected, for example turning an OKR map into a tracked project, or meeting action items into tasks. These steps are optional and only run if MeisterTask is available in your session.

## License

[MIT](LICENSE.md)
