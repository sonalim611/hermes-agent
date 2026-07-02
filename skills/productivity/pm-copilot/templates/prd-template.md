# [Product / Feature Name] — Product Requirements Document

> **Status:** Draft  
> **Author:** _(name)_  
> **Last updated:** YYYY-MM-DD  
> **Version:** 0.1  
> **Stakeholders:** _(names or roles)_  
> **Workspace path:** `.hermes/prds/YYYY-MM-DD_HHMMSS-<slug>.md`  
> **Based on:** _(prior PRD path, if revision — else omit)_  

---

## Executive Summary

_2–4 sentences for leadership: what we are building, for whom, why now, and the expected outcome. Include target launch window if known._

---

## Problem Statement

### The problem

_Describe the user or business pain in concrete terms. Who experiences it, how often, and what it costs them today._

### Why now

_Market, competitive, regulatory, or internal drivers that make this the right time to solve it._

### Current state

_How users work around the problem today. Link to data, support tickets, or research if available._

---

## User Persona

### Primary persona

| Attribute | Detail |
|-----------|--------|
| **Name / label** | _(e.g. "Gym member — frequent visitor")_ |
| **Role** | |
| **Goals** | |
| **Frustrations** | |
| **Context** | _(device, environment, frequency of use)_ |

### Secondary persona(s)

_(Optional. Repeat table or bullet list for additional audiences.)_

---

## Goals

### Product goals

| # | Goal | How we will know |
|---|------|------------------|
| G1 | | |
| G2 | | |

### Non-goals

_Explicitly out of scope for this release. Prevents scope creep._

- 
- 

---

## User Stories

_Format: As a **[persona]**, I want **[capability]**, so that **[outcome]**._

| ID | Story | Priority |
|----|-------|----------|
| US-1 | As a **…**, I want **…**, so that **…**. | Must have |
| US-2 | | Should have |
| US-3 | | Nice to have |

---

## Functional Requirements

_Testable behaviors the product must support. Use "The system shall …" or "The user can …"._

| ID | Requirement | Acceptance criteria | Priority |
|----|-------------|---------------------|----------|
| FR-1 | | Given … When … Then … | P0 |
| FR-2 | | | P0 |
| FR-3 | | | P1 |

### User flows (optional)

_Brief step-by-step for critical paths (e.g. happy path, error path)._

**Flow: [name]**

1. 
2. 
3. 

---

## Non-functional Requirements

| Category | Requirement | Target / notes |
|----------|-------------|----------------|
| **Performance** | _(e.g. page load, API latency)_ | |
| **Availability** | _(e.g. uptime SLA)_ | |
| **Security & privacy** | _(auth, PII handling, compliance)_ | |
| **Accessibility** | _(WCAG level if applicable)_ | |
| **Scalability** | _(expected load)_ | |
| **Compatibility** | _(browsers, devices, locales)_ | |
| **Offline / resilience** | _(degraded mode behavior)_ | |

---

## Success Metrics

_Define how we measure success after launch. Prefer metrics tied to goals._

| Metric | Definition | Baseline | Target | Measurement method | Review cadence |
|--------|------------|----------|--------|-------------------|----------------|
| | | | | | _(e.g. weekly for 4 weeks post-launch)_ |

### Leading indicators (optional)

_Early signals during beta or rollout._

| Indicator | Target |
|-----------|--------|
| | |

---

## Risks

| ID | Risk | Likelihood | Impact | Mitigation | Owner |
|----|------|------------|--------|------------|-------|
| R-1 | | Low / Med / High | Low / Med / High | | |
| R-2 | | | | | |

---

## Dependencies

| Dependency | Type | Owner | Status | Needed by |
|------------|------|-------|--------|-----------|
| | _(Team / API / Legal / Vendor)_ | | _(Blocked / In progress / Done)_ | |

---

## Open Questions

_Unresolved items that block or weaken the PRD. Do not bury these in requirements._

| # | Question | Owner | Due date | Resolution |
|---|----------|-------|----------|------------|
| OQ-1 | | | | |
| OQ-2 | | | | |

---

## Launch Plan

### Launch tier

_(e.g. internal dogfood → beta cohort → staged rollout → GA)_

### Milestones

| Milestone | Target date | Exit criteria |
|-----------|-------------|---------------|
| Spec approved | | PRD signed off by stakeholders |
| Dev complete | | All P0 requirements met in staging |
| Beta | | |
| GA | | |

### Rollout strategy

- **Audience:** _(who gets it first)_
- **Feature flags:** _(yes/no, cohort rules)_
- **Rollback plan:** _(triggers and steps)_

### Comms and enablement

| Audience | Message / artifact | Owner | Date |
|----------|-------------------|-------|------|
| Engineering | | | |
| Support | | | |
| Customers | | | |

### Post-launch

- **Metric review:** _(when and who)_
- **Retro:** _(scheduled date)_

---

## Appendix (optional)

- Research links
- Mockups or wireframes
- Related PRDs or epics

---

## Revision history (optional)

| Date | File | Summary |
|------|------|---------|
| YYYY-MM-DD | `.hermes/prds/YYYY-MM-DD_HHMMSS-<slug>.md` | Initial draft |

---

_Document generated with pm-copilot. Replace bracketed placeholders with source-backed content._
