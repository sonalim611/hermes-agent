# PRD Workspace Layout (pm-copilot)

Load when saving, finding, or continuing work on PRDs:

`skill_view("pm-copilot", "references/prd-workspace.md")`

All paths are **relative to the active workspace** (Hermes `terminal.cwd` / current project directory). Hermes file tools are backend-aware — the same relative paths work on local, docker, ssh, and remote backends.

---

## Directory layout

```
.hermes/
├── prds/                                    # PRDs (timestamped)
│   ├── YYYY-MM-DD_HHMMSS-<slug>.md
│   ├── YYYY-MM-DD_HHMMSS-<slug>-v2.md       # major revisions (optional suffix)
│   └── reviews/
│       └── YYYY-MM-DD_HHMMSS-<slug>-review.md
├── pm-priorities/
│   └── YYYY-MM-DD_HHMMSS-<slug>-rice.md
└── launch-checklists/
    └── YYYY-MM-DD_HHMMSS-<slug>-launch.md
```

**Slug:** kebab-case from the feature name (e.g. `gym-qr-check-in`).

**Timestamp:** `YYYY-MM-DD_HHMMSS` at save time (24-hour clock). Every new PRD gets a **new** timestamped filename — do not overwrite prior PRDs unless the user explicitly asks to update that exact file.

---

## Filename examples

| Artifact | Path |
|----------|------|
| New PRD | `.hermes/prds/2026-07-01_143022-gym-qr-check-in.md` |
| PRD review | `.hermes/prds/reviews/2026-07-01_150000-gym-qr-check-in-review.md` |
| RICE output | `.hermes/pm-priorities/2026-07-01_151500-gym-backlog-rice.md` |
| Launch checklist | `.hermes/launch-checklists/2026-07-01_160000-gym-qr-check-in-launch.md` |

---

## Find existing PRDs

### List all PRDs (newest first)

```
search_files("*.md", target="files", path=".hermes/prds")
```

Results are sorted by modification time — the first match is usually the latest for that folder.

### Find by feature name (slug or title)

Content search inside PRDs:

```
search_files("gym-qr", target="content", path=".hermes/prds", file_glob="*.md")
```

File name search:

```
search_files("*gym-qr*", target="files", path=".hermes/prds")
```

### Read a specific PRD

```
read_file(".hermes/prds/2026-07-01_143022-gym-qr-check-in.md")
```

If the user gives a partial name, list with `search_files` first, then `read_file` the best match. If ambiguous, `clarify` with the candidate paths.

---

## Continue working on a PRD

**Triggers:** "continue the PRD", "update my gym PRD", "add section to yesterday's PRD", "list my PRDs", "open the latest PRD for X".

### Procedure

1. **Locate** — `search_files` under `.hermes/prds` (by slug, content, or `*.md` list).
2. **Load** — `read_file` on the chosen path. Note **Open Questions** and incomplete sections.
3. **Clarify if needed** — new meeting notes or answers to open questions may require the same no-invention rules as Workflow 1 (`prd-required-inputs.md`).
4. **Edit** — choose one mode:

| Change size | Tool | Output |
|-------------|------|--------|
| Section tweak, typo, fill one open question | `patch` on existing file | Same path; bump `**Last updated:**` in frontmatter |
| Major rewrite, post-review v2, large new scope | `write_file` new timestamped file | `.hermes/prds/YYYY-MM-DD_HHMMSS-<slug>-v2.md` (or new slug) |

5. **Link versions** — for a new file, add near the top:

   `> **Based on:** .hermes/prds/<prior-filename>.md`

   Append a line to the prior file's **Revision history** only if the user asked to update that file in place with a pointer; otherwise the new file's header is enough.

6. **Reply** — path edited or created, what changed, remaining open questions.

### Do not

- Invent business facts when filling gaps (same rules as new PRDs)
- Overwrite an old timestamped PRD with unrelated content
- Guess which PRD the user means when multiple match — list top 3 paths and `clarify`

---

## Cross-workflow retrieval

| User wants | Load with |
|------------|-----------|
| Review existing PRD | `read_file` on PRD path → Workflow 2 |
| RICE from PRD features | `read_file` PRD → extract feature list → Workflow 3 |
| Launch checklist from PRD | `read_file` PRD → Workflow 4 |
| Continue / revise PRD | This doc → `patch` or new `write_file` |

---

## PRD frontmatter (for continuity)

When saving or updating, keep these fields accurate:

```markdown
> **Status:** Draft | In review | Approved
> **Last updated:** YYYY-MM-DD
> **Source PRD:** _(path, if this is a revision)_
```

Optional **Revision history** table at the bottom:

| Date | File | Summary |
|------|------|---------|
| 2026-07-01 | `.hermes/prds/2026-07-01_143022-gym-qr-check-in.md` | Initial draft from meeting |
