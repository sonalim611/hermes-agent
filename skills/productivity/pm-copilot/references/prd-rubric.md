# PRD Review Rubric (pm-copilot)

Use this rubric for **Workflow 2: PRD Review**. Score each PRD section **1–5**, document gaps, flag assumptions and edge cases, and write **actionable** improvement suggestions.

Load with: `skill_view("pm-copilot", "references/prd-rubric.md")`

---

## Scoring scale (all sections)

| Score | Label | Meaning |
|-------|-------|---------|
| **5** | Excellent | Complete, specific, testable, stakeholder-ready; no material gaps |
| **4** | Good | Minor gaps only; ship with small edits |
| **3** | Adequate | Usable but vague in places; needs clarification before build |
| **2** | Weak | Major gaps, untestable requirements, or missing persona/goals linkage |
| **1** | Missing / unusable | Section absent, placeholder-only, or contradicts other sections |
| **N/A** | Not applicable | Section intentionally omitted with stated reason (e.g. no launch yet) |

**Section score** = holistic judgment using the criteria below, not an average of sub-bullets.

---

## How to review (agent procedure)

For **each section** of the PRD under review, produce:

1. **Score (1–5 or N/A)**
2. **Missing information** — what a Senior PM would expect but is not stated
3. **Unvalidated assumptions** — claims presented as fact without evidence
4. **Edge cases** — failure modes, empty states, permissions, offline, abuse not addressed
5. **Measurability** — whether success can be verified (for metrics & requirements)
6. **Improvement suggestions** — specific, actionable edits (not "be clearer")

Record findings in `templates/prd-review-template.md`. Cite PRD section headings in every finding.

---

## Section-by-section criteria

### 1. Executive Summary

**Looks for:** what / who / why now / outcome in ≤4 sentences; aligns with rest of doc.

| Score | Criteria |
|-------|----------|
| 5 | Crisp, accurate, no jargon; reader needs nothing else for a go/no-go gut check |
| 3 | Present but vague ("improve UX") or omits audience or outcome |
| 1 | Missing or contradicts Problem Statement / Goals |

**Probe:** Would an exec understand the bet without reading further? Is launch timing mentioned if claimed elsewhere?

---

### 2. Problem Statement

**Looks for:** specific pain, frequency/severity, why now, current workarounds, evidence.

| Score | Criteria |
|-------|----------|
| 5 | Quantified or well-sourced pain; clear urgency; current state described |
| 3 | Pain named but not evidenced; "users want" without who/how many |
| 1 | Solution disguised as problem ("we need an app") |

**Missing info checklist:** Who hurts? How often? Cost of inaction? Data/research links?

**Assumption flags:** Market size, churn impact, competitive threat without citation.

**Edge cases:** Different user segments with different pain; enterprise vs consumer.

---

### 3. User Persona

**Looks for:** primary persona with goals, frustrations, context; secondary if multi-audience.

| Score | Criteria |
|-------|----------|
| 5 | Persona drives requirements; stories reference persona labels |
| 3 | Generic persona ("end user"); weak link to requirements |
| 1 | Missing or personas don't match stated problem |

**Missing info:** Role, environment, frequency, constraints (mobile, low literacy, admin).

**Edge cases:** Admin vs end user; new vs power user; locale/accessibility needs.

---

### 4. Goals & Non-goals

**Looks for:** measurable product goals; explicit non-goals preventing scope creep.

| Score | Criteria |
|-------|----------|
| 5 | Each goal has "how we will know"; non-goals are concrete |
| 3 | Goals are directional only; thin or missing non-goals |
| 1 | No non-goals; goals are output metrics without user/business outcome |

**Measurability:** Every goal should tie to Success Metrics or state measurement method.

**Improvement example:** Replace "Increase engagement" → "Increase weekly active check-ins per member by 15% within 90 days of GA."

---

### 5. User Stories

**Looks for:** standard format; IDs; priority; traceability to functional requirements.

| Score | Criteria |
|-------|----------|
| 5 | Stories cover core journeys; prioritized; map to FR IDs |
| 3 | Stories exist but orphan requirements or duplicate FRs |
| 1 | Missing or bullet wishes without persona/outcome |

**Edge cases:** Error paths, cancellation, empty lists, first-time vs returning user.

**Improvement:** Add story for failure/recovery when FR implies happy path only.

---

### 6. Functional Requirements

**Looks for:** testable FRs with acceptance criteria; priorities (P0/P1); IDs.

| Score | Criteria |
|-------|----------|
| 5 | Given/When/Then or equivalent; engineer can estimate without clarification |
| 3 | Requirements list features but acceptance criteria vague |
| 1 | Marketing copy or untestable adjectives ("fast", "easy") |

**Missing info:** Auth rules, data fields, error messages, limits, integrations.

**Assumption flags:** Third-party API behavior, existing system capabilities.

**Edge cases (mandatory scan):**

- Permissions / roles denied
- Empty input, max length, invalid input
- Concurrent use, race conditions
- Migration / backward compatibility
- Rollback / feature-flag off state

**Improvement format:** "FR-3: Add acceptance criterion for timeout after 30s and retry limit of 3."

---

### 7. Non-functional Requirements

**Looks for:** performance, security, privacy, a11y, scale, compatibility, offline.

| Score | Criteria |
|-------|----------|
| 5 | Targets are numeric or explicitly N/A with reason |
| 3 | Categories listed without targets |
| 1 | Missing for a customer-facing or data-touching feature |

**Measurability:** "Fast" → p95 latency < X ms; "Secure" → specific controls (encryption, auth).

**Edge cases:** Peak load, degraded mode, regional compliance (GDPR, etc.).

---

### 8. Success Metrics

**Looks for:** definition, baseline, target, measurement method, review cadence.

| Score | Criteria |
|-------|----------|
| 5 | Metrics link to goals; baseline + target + owner + dashboard |
| 3 | Metrics named without baseline or measurement plan |
| 1 | Missing or vanity metrics only (page views without outcome) |

**Missing info:** How measured, when reviewed, guardrail metrics (errors, support volume).

**Assumption flags:** Expected lift without baseline; attribution unclear.

**Improvement:** Add guardrail metric (e.g. support tickets per 1k users) for launch.

---

### 9. Risks

**Looks for:** likelihood, impact, mitigation, owner; top risks for this feature class.

| Score | Criteria |
|-------|----------|
| 5 | Risks are specific; mitigations actionable; owners named |
| 3 | Generic risk list (delay, bugs) without feature-specific items |
| 1 | Missing for non-trivial scope |

**Edge cases:** Technical unknowns, legal, dependency slip, adoption risk.

---

### 10. Dependencies

**Looks for:** team/API/legal/vendor deps with owner, status, needed-by date.

| Score | Criteria |
|-------|----------|
| 5 | Critical path dependencies identified with status |
| 3 | Dependencies named without dates or owners |
| 1 | Missing external blockers obvious from FRs |

**Improvement:** "Add dependency on Identity team for SSO — needed before beta."

---

### 11. Open Questions

**Looks for:** honest unknowns; owners; due dates; not smuggled into requirements.

| Score | Criteria |
|-------|----------|
| 5 | All material unknowns listed; none hidden in FRs as decided |
| 3 | Short list; some conflicts in doc left unresolved |
| 1 | Empty while PRD contains TBDs in requirements |

**Assumption flags:** Any FR that reads as decided but appears in Open Questions elsewhere.

---

### 12. Launch Plan

**Looks for:** tier, milestones, rollout, rollback, comms, post-launch metric review.

| Score | Criteria |
|-------|----------|
| 5 | Staged rollout, rollback triggers, owners for comms/support |
| 3 | Dates only; no rollback or success review |
| 1 | Missing for a committed launch date in Executive Summary |
| N/A | Explicitly pre-discovery; no launch claimed |

**Edge cases:** Partial rollout failure, kill switch, support surge.

---

## Cross-cutting review (all sections)

After scoring sections, complete these passes:

### Assumptions audit

List every statement that assumes:

- User behavior without evidence
- Technical feasibility without spike
- Third-party availability or SLA
- Organizational capacity or priority
- Metric uplift without baseline

Format: `| Assumption | Where in PRD | Risk if wrong | Validate by |`

### Edge-case coverage

List gaps not tied to a single section:

| Area | Covered in PRD? | Gap | Suggested FR or OQ |
|------|-----------------|-----|-------------------|
| Error handling | | | |
| Permissions | | | |
| Empty / max states | | | |
| Offline / degraded | | | |
| Abuse / security | | | |
| Accessibility | | | |

### Measurability audit

| Goal / metric | Measurable? | Issue | Fix |
|---------------|-------------|-------|-----|
| | Yes / Partial / No | | |

---

## Overall score and verdict

### Weighted overall (guidance)

| Section | Weight |
|---------|--------|
| Problem Statement | 15% |
| Functional Requirements | 20% |
| Success Metrics | 15% |
| Goals & Non-goals | 10% |
| User Stories + Persona | 10% |
| Non-functional Requirements | 10% |
| Launch Plan | 10% |
| Risks + Dependencies + Open Questions | 10% |
| Executive Summary | 5% |

Compute approximate **overall score (1–5)** rounded to one decimal. Explain in one sentence.

### Verdict rules

| Verdict | When |
|---------|------|
| **Ready** | Overall ≥ 4.0 AND no section below 3 AND no critical FR/metric gaps |
| **Revise** | Overall 3.0–3.9 OR any section at 2 that is fixable without new discovery |
| **Blocked** | Overall < 3.0 OR Problem/Persona/FR at 1–2 OR critical open questions unanswered |

---

## Improvement suggestions (required format)

Every suggestion must be **actionable**:

**Bad:** "Clarify requirements."  
**Good:** "FR-2: Add acceptance criterion — when QR scan fails network check, show offline queue message and sync within 60s of reconnect."

Use this table in the review report:

| Priority | Section | Issue | Suggested change | Owner (if known) |
|----------|---------|-------|------------------|------------------|
| P0 | Functional Requirements | Missing offline behavior | Add FR-4 with criteria … | Eng + PM |
| P1 | Success Metrics | No baseline | Pull 90-day check-in rate from analytics | PM |

**Priority:** P0 = blocks build/launch; P1 = should fix before GA; P2 = polish.

---

## Quick reference: minimum bar for "Ready"

- [ ] Problem and persona are specific and aligned
- [ ] Every P0 FR has testable acceptance criteria
- [ ] Non-goals exist
- [ ] Success metrics have baseline, target, and measurement
- [ ] Top risks and dependencies have owners
- [ ] Open questions do not duplicate hidden TBDs in FRs
- [ ] Launch plan includes rollback and post-launch metric review (if shipping)

---

_Extend this rubric with org-specific compliance (SOC2, HIPAA, WCAG level) when reviewing regulated products._
