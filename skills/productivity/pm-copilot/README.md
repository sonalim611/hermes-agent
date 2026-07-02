# PM Copilot — Product Manager AI Agent

**PM Copilot** is a Hermes skill that turns meeting notes into stakeholder-ready product artifacts. It ships as a bundled skill in this fork — no core agent changes required.

Built on [Hermes Agent](https://github.com/NousResearch/hermes-agent) by [sonalim611](https://github.com/sonalim611).

## What it does

| Workflow | Command example | Output |
|----------|-----------------|--------|
| Meeting → PRD | `/pm-copilot transcript → PRD` + notes | Timestamped PRD in `.hermes/prds/` |
| PRD review | `/pm-copilot review the wishlist PRD` | Rubric scorecard in `.hermes/prds/reviews/` |
| RICE prioritization | `/pm-copilot RICE prioritize …` | Ranked table in `.hermes/pm-priorities/` |
| Launch checklist | `/pm-copilot launch checklist for …` | Checklist in `.hermes/launch-checklists/` |
| Resume / list PRDs | `/pm-copilot list my PRDs` | Finds prior work via `search_files` + `read_file` |

### Design principles

- **Clarify before draft** — asks for missing required inputs instead of inventing business facts
- **Workspace persistence** — artifacts live under `.hermes/` in your project directory with `YYYY-MM-DD_HHMMSS-<slug>` filenames
- **Skill, not core** — uses Hermes file tools (`read_file`, `write_file`, `patch`, `search_files`, `clarify`) only; zero new model-tool footprint

## Quick start

### 1. Install Hermes

```bash
git clone https://github.com/sonalim611/hermes-agent.git
cd hermes-agent
python -m pip install -e .
```

### 2. Configure a model provider

Set an API key (e.g. OpenRouter) and provider in `~/.hermes/config.yaml`. See [Hermes setup docs](https://github.com/NousResearch/hermes-agent).

### 3. Sync bundled skills

```bash
python -c "from tools.skills_sync import sync_skills; sync_skills(quiet=False)"
```

### 4. Create a PM workspace and run Hermes

```bash
mkdir ~/pm-workspace && cd ~/pm-workspace
python -m hermes_cli.main
```

In chat: `/reload-skills`, then confirm with `/skills list --source builtin` (look for `pm-copilot`).

## Example session

**Generate a PRD:**

```
/pm-copilot transcript → PRD

The team discussed adding a wishlist feature for an e-commerce app. Users currently
lose products between sessions. The goal is to improve retention. Success will be
measured by a 15% increase in repeat visits. Launch is planned for Q4.
```

**Review, prioritize, and launch:**

```
/pm-copilot review the wishlist PRD we just created in .hermes/prds/
/pm-copilot RICE prioritize the wishlist feature for our e-commerce app
/pm-copilot launch checklist for the e-commerce wishlist feature
```

**Persistence across turns:**

```
What PRD did we create earlier?
```

The agent uses `search_files` and `read_file` under `.hermes/prds/` — not chat memory alone.

## Workspace layout

```
.hermes/
├── prds/YYYY-MM-DD_HHMMSS-<slug>.md
├── prds/reviews/YYYY-MM-DD_HHMMSS-<slug>-review.md
├── pm-priorities/YYYY-MM-DD_HHMMSS-<slug>-rice.md
└── launch-checklists/YYYY-MM-DD_HHMMSS-<slug>-launch.md
```

Paths are relative to the **active workspace** (where you start Hermes), not `~/.hermes` config home.

## Skill structure

```
skills/productivity/pm-copilot/
├── SKILL.md                          # Agent instructions (v1.3.0)
├── README.md                           # This file
├── references/
│   ├── prd-required-inputs.md        # Clarify gate + no-invention rules
│   ├── prd-workspace.md              # Paths, retrieval, resume workflow
│   └── prd-rubric.md                 # PRD quality rubric
└── templates/
    ├── prd-template.md
    ├── prd-review-template.md
    ├── rice-template.md
    └── launch-checklist-template.md
```

## Verification checklist

After a full test run you should see:

- [ ] PRD saved under `.hermes/prds/` with timestamp filename
- [ ] Review report with **Ready / Revise / Blocked** verdict
- [ ] RICE output with labeled assumptions
- [ ] Launch checklist saved
- [ ] Agent can locate prior PRDs via file tools

## Related Hermes skills

- [`plan`](../../software-development/plan/) — engineering implementation plans (not PRDs)
- [`teams-meeting-pipeline`](../teams-meeting-pipeline/) — optional upstream for Teams transcripts
- [`ocr-and-documents`](../ocr-and-documents/) — scanned meeting notes

## License

MIT — same as Hermes Agent.
