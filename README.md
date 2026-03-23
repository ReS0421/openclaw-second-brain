# openclaw-second-brain

> OpenClaw-based Second Brain — Obsidian + Notion dual-layer knowledge system

A collection of skills for running a second brain with OpenClaw as your AI operator, Obsidian as the source of truth, and Notion as the publishing layer.

## Structure

```
openclaw (AI operator)
├── knowledge-ops         ← Top-level rules for Obsidian ↔ Notion dual system
├── obsidian-governance   ← Obsidian vault internal rules
├── notion-portfolio-api  ← Notion structure reference (DB schema, IDs)
├── second-brain-operator ← Active second brain agent
├── openclaw-secretary    ← Memory distillation, daily logs, session wrap-up
└── notion-general        ← Notion General workspace rules (internal layer)
```

## Core Principles

- **Obsidian is the source of truth** — all original content lives in Obsidian
- **Notion General = internal refined layer** — team-shareable, process-preserving
- **Notion Portfolio Hub = publishing layer** — selected content published and restructured for readers
- **AI operates the system** — organizing, publishing, backups, and memory management are handled by the system

## Installation

```bash
# Assumes OpenClaw is already installed

# Clone the repo
git clone https://github.com/ReS0421/openclaw-second-brain.git

# Copy skills
cp -r openclaw-second-brain/skills/* ~/.openclaw/workspace/skills/
```

## Customization

Replace all `YOUR_*` placeholders in each `SKILL.md` with your own values.

| Placeholder | Replace with |
|---|---|
| `YOUR_NAME` | Your display name for portfolio (e.g. `John · Portfolio`) |
| `YOUR_USERNAME` | Your GitHub username |
| `YOUR_OBSIDIAN_VAULT` | Path to your Obsidian vault |
| `YOUR_GENERAL_ROOT_PAGE_ID` | Notion General root page ID |
| `YOUR_PORTFOLIO_HOME_PAGE_ID` | Notion portfolio home page ID |
| `YOUR_PORTFOLIO_HOME_DB_ID` | Notion portfolio home DB ID |
| `YOUR_PROJECTS_DB_ID` | Notion Projects database ID |
| `YOUR_CASE_STUDIES_DB_ID` | Notion Case Studies database ID |
| `YOUR_DOMAINS_DB_ID` | Notion Domains database ID |
| `YOUR_RESEARCH_NOTES_DB_ID` | Notion Research/Notes database ID |

To find a Notion ID: open a page in Notion and copy from the URL — `notion.so/YOUR_ID`

## Skill Details

### `knowledge-ops`
Top-level rules for the dual Obsidian + Notion system. Defines publishing flow, content routing (what goes to General vs Portfolio Hub), and the principle that Obsidian is the origin. Takes precedence when other skills conflict.

### `obsidian-governance`
Internal vault rules. Covers folder placement (PARA + system folders), note types, frontmatter schema, and link conventions. Keeps the vault consistent when AI creates or modifies files.

### `notion-portfolio-api`
Reference skill for your Notion portfolio structure. Contains DB schemas, page IDs, and block syntax so the AI doesn't need to look them up every time. Personal IDs are replaced with `YOUR_*` placeholders in this public version.

### `notion-general`
Rules for the Notion General workspace — the internal layer between raw Obsidian notes and the public Portfolio Hub. Used for team-shareable project records and refined process documentation.

### `second-brain-operator`
The active agent for second brain tasks. Handles vault organization, note structuring, and Notion publishing. Includes a permission model defining what can be done autonomously vs. what requires reporting back.

### `openclaw-secretary`
The AI's own assistant. Handles session wrap-up, MEMORY.md distillation, daily log writing, ticket management, and channel state updates. Updated to include the full wrap-up workflow with immediate vs. INBOX memory routing.

## Related Article

[Article link coming soon]

## License

MIT
