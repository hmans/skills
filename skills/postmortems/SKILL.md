---
name: "postmortems"
description: "Create, update, and audit structured incident postmortems in a repository. Use when the user asks for an incident postmortem, outage review, retrospective, root-cause writeup, lessons learned document, or wants to establish or maintain a numbered docs/postmortems system with an index."
---

# Incident Postmortems

Manage production or project incident postmortems as structured markdown documents. By default, postmortems live in `docs/postmortems/`, but follow the repository's existing incident documentation layout if one already exists.

Postmortems are reference documents for future incident response. They should explain what happened, how it was detected, how it was mitigated, what evidence supports the conclusions, and what durable follow-up work remains.

## Directory Structure

Default layout:

```text
docs/postmortems/
|-- INDEX.md                                      # Index with TOC (read this first)
|-- PM-001-2026-07-03-nats-jetstream-stall.md    # Individual postmortem
|-- PM-002-2026-08-14-api-rollout-regression.md
`-- ...
```

If no postmortem structure exists yet, prefer `docs/postmortems/` unless the user asks for a different location.

## File Naming

```text
PM-{NNN}-{YYYY-MM-DD}-{kebab-case-slug}.md
```

- `NNN`: zero-padded three-digit number, sequential.
- `YYYY-MM-DD`: incident start date, not necessarily the writeup date.
- Slug: short kebab-case incident summary.

## Postmortem Template

```markdown
# PM-{NNN}: {Incident Title}

**Incident date:** {YYYY-MM-DD}
**Status:** Draft
**Severity:** {SEV-1|SEV-2|SEV-3|SEV-4|Unknown}
**Systems affected:** {systems, services, tenants, regions}
**Authors:** {names or teams}
**Last updated:** {YYYY-MM-DD}

## Summary

One short paragraph describing the customer/user impact, the cause at the level currently known, and the mitigation.

## Impact

- Who or what was affected.
- Duration and scope.
- User-visible symptoms.
- Data loss or correctness impact, if any.

## Timeline

All times should include timezone or UTC.

| Time | Event |
|------|-------|
| {YYYY-MM-DD HH:MM TZ} | {event} |

## Detection

How the incident was noticed: alert, user report, logs, metrics, synthetic check, deployment signal, etc.

## Root Cause

What failed and why. Be specific about evidence and confidence. If root cause is not known, say so and list the leading hypotheses.

## Resolution

What restored service. Include operational commands/actions only at the level needed for future response; avoid secret values.

## What Went Well

- Things that reduced impact or made diagnosis faster.

## What Went Poorly

- Things that delayed detection, diagnosis, mitigation, or recovery.

## Follow-Up Actions

| Owner | Action | Priority | Status |
|-------|--------|----------|--------|
| {owner} | {action} | {P0|P1|P2|P3} | Open |

## References

- Links to incidents, dashboards, PRs, ADRs, FDRs, logs, runbooks, or related postmortems.
```

Status values:

- **Draft**: writeup is incomplete or waiting for evidence.
- **Reviewing**: stakeholders are reviewing accuracy and actions.
- **Final**: root cause, impact, and follow-ups are accepted.
- **Reopened**: new evidence materially changed the incident analysis.

## Workflow

### Before doing anything

1. Read relevant project instructions first: `AGENTS.md`, `CLAUDE.md`, `.agents/`, `.codex/`, or docs notes.
2. Locate `docs/postmortems/INDEX.md`; if absent, search for `PM-*.md`, `postmortem`, `incident`, `outage`, or `retrospective`.
3. Read the index before individual postmortems.
4. Read only postmortems relevant to the current incident or requested audit.
5. If the incident touches architecture or feature behavior, check whether related ADRs or FDRs exist.

### Creating the structure

If no postmortem structure exists and the user asked to establish one:

1. Create `docs/postmortems/`.
2. Create `docs/postmortems/INDEX.md` with the TOC format below.
3. Do not create placeholder incident documents unless the user asked for an actual postmortem.

### Creating a new postmortem

1. Read `docs/postmortems/INDEX.md` to determine the next number.
2. Choose the incident date from the incident start time, not today's date.
3. Use the template above.
4. Set **Status** to `Draft` unless the user explicitly says the analysis is final.
5. Use concrete timestamps and evidence. Mark unknowns explicitly.
6. Add the new entry to `INDEX.md`.
7. Cross-reference related ADRs, FDRs, runbooks, PRs, dashboards, alerts, and prior postmortems.
8. If the incident exposed a missing or stale runbook, recommend creating or updating it.

### Updating a postmortem

1. Read `INDEX.md` and the target postmortem.
2. Rewrite stale sections in place instead of appending "Update:" notes.
3. Bump **Last updated** to today's date.
4. Update index metadata if title, status, severity, or incident date changed.
5. Preserve unresolved questions and open follow-ups unless new evidence closes them.

### Auditing postmortems

When asked to audit or review postmortems:

1. Check whether each postmortem has impact, timeline, detection, root cause, resolution, and follow-up sections.
2. Verify claims against available issue threads, logs, commits, alerts, docs, or code when accessible.
3. Report gaps as actionable edits: missing evidence, vague root cause, unowned follow-ups, stale status, or missing references.
4. Do not silently invent root cause. State confidence and unknowns.

## Writing Style

- Be factual and blameless. Avoid assigning personal fault.
- Prioritize future usefulness over narrative polish.
- Use concrete systems, symptoms, dates, and times.
- Distinguish facts from hypotheses.
- Include enough operational detail to help future responders, but no secrets or credential material.
- Keep implementation details only where they explain cause, mitigation, or prevention.
- Do not overstate certainty. Use "likely" or "unknown" where appropriate.
- Follow-up actions should be owned, specific, and verifiable.

## TOC Format

`INDEX.md` should use a markdown table:

```markdown
# Incident Postmortems

| # | Incident | Date | Severity | Status |
|---|----------|------|----------|--------|
| [PM-001](PM-001-2026-07-03-nats-jetstream-stall.md) | NATS JetStream stall in chatto-eu1 | 2026-07-03 | SEV-1 | Draft |
```

## Verification Checklist

When creating or updating a postmortem, verify:

- [ ] The postmortem directory and numbering match repository convention.
- [ ] The index has the correct title, date, severity, and status.
- [ ] Incident timestamps include timezone or UTC.
- [ ] Impact describes users, systems, duration, and data correctness.
- [ ] Root cause is supported by evidence or explicitly marked unknown.
- [ ] Resolution separates immediate mitigation from durable prevention.
- [ ] Follow-up actions have owners, priorities, and statuses.
- [ ] Related ADRs, FDRs, runbooks, PRs, dashboards, and prior incidents are linked when relevant.
- [ ] No secret values or sensitive credential material are included.
