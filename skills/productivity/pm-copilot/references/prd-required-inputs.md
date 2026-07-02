# PRD Required Inputs (pm-copilot)

Load before **Workflow 1: Meeting transcript → PRD**:

`skill_view("pm-copilot", "references/prd-required-inputs.md")`

Use this checklist after ingesting the transcript. **Do not draft the PRD** until the gate rules below are satisfied.

---

## Required before PRD generation

| # | Required information | Source | If missing |
|---|---------------------|--------|------------|
| R1 | **Feature or initiative name** (working title OK) | Transcript or user | Ask via `clarify` |
| R2 | **Primary user / persona** (who benefits) | Transcript or user | Ask via `clarify` |
| R3 | **Problem or pain** (what is wrong today) | Transcript or user | Ask via `clarify` |
| R4 | **Intended outcome** (what success looks like, even qualitatively) | Transcript or user | Ask via `clarify` |
| R5 | **Source material** (transcript, notes, or summary) | User paste / `read_file` | Ask via `clarify` |

R5 must be present. R1–R4 must be **either** clearly stated in the source **or** answered by the user after `clarify`.

---

## Strongly recommended (ask if absent)

| # | Information | Why |
|---|-------------|-----|
| S1 | Scope boundaries / non-goals | Prevents invented scope |
| S2 | Must-have vs nice-to-have signals | Prioritization |
| S3 | Constraints (date, budget, compliance, platforms) | Realistic requirements |
| S4 | Success metrics or KPIs discussed | Avoid fabricated numbers |
| S5 | Named stakeholders or decision owners | Launch and dependencies |

Bundle missing S1–S5 into the same `clarify` round (max 5 questions total per round).

---

## Never invent (business information)

Do **not** fabricate or guess:

- User counts, revenue, conversion rates, or market size
- Launch dates or deadlines not in source or user answers
- Prioritization decisions ("leadership approved") not evidenced
- Metric baselines or targets
- Persona details (role, demographics, behavior) not in source
- Requirements presented as agreed when the meeting only discussed ideas
- Technical architecture choices unless explicitly decided
- Legal, compliance, or policy commitments

If unknown, leave the PRD section sparse and list the item under **Open Questions** — only after the clarify gate (below) is complete.

---

## What you may infer (structure only)

Without asking, you may:

- Organize messy notes into PRD sections
- Rephrase unclear statements neutrally (preserve meaning)
- Label items as **proposal** vs **decision** when the transcript is ambiguous
- Suggest user-story format for stated needs (not new needs)
- Add standard NFR *categories* as placeholders marked "not discussed"

You may **not** infer business facts to fill those placeholders.

---

## Clarify gate (mandatory)

After ingest + extract, before `write_file`:

1. Compare source against R1–R5 and S1–S5.
2. If **any R-item is missing**, call `clarify` with numbered questions (max 5 per round).
3. **Stop.** Do not generate or save the PRD yet.
4. When the user answers, re-check. Ask a second `clarify` round only if R-items remain missing (max 2 rounds total).
5. **Only then** draft the PRD.

### User override

If the user explicitly says **"draft with what we have"**, **"proceed with open questions"**, or **"skip clarifying"**:

- Draft the PRD with gaps marked in **Open Questions**
- Add banner at top of PRD: `> **DRAFT — INCOMPLETE INPUT:** Critical details were not provided; see Open Questions.`
- Do not invent missing business facts to make sections look complete

---

## Clarify question quality

**Bad:** "Tell me more about the product."  
**Good:** "Who is the primary user for QR check-in — gym members, staff, or both?"

**Bad:** "What are the success metrics?" (then invent 15% uplift in the PRD)  
**Good:** "Did the meeting define a success metric for check-in adoption? If not, should we leave Success Metrics as open questions?"

---

## PRD generation allowed when

- [ ] R1–R5 satisfied (from source and/or user answers), **or** user invoked override
- [ ] No business facts invented to fill gaps
- [ ] Ambiguous items labeled decision vs idea vs open question
- [ ] `skill_view` loaded for `templates/prd-template.md`
