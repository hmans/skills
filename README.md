# Agent Skills

A small collection of reusable agent skills. Each skill is packaged as a
directory containing a `SKILL.md` file and can be installed with Vercel's
`skills` CLI.

## Install

List the available skills:

```bash
npx skills add hmans/skills --list
```

Install one skill:

```bash
npx skills add hmans/skills --skill technical-writing
```

Install all skills globally for Codex:

```bash
npx skills add hmans/skills --skill '*' --agent codex --global
```

Install all skills for every detected agent:

```bash
npx skills add hmans/skills --all
```

## Available Skills

| Skill | Purpose |
| --- | --- |
| `adr` | Maintain Architecture Decision Records in `docs/adr/`. |
| `bazinga` | Run a full feature workflow from setup through PR and CI follow-up. |
| `code-review` | Review local changes, branches, or PRs for bugs and risks. |
| `fdr` | Maintain Feature Decision Records in `docs/fdr/`. |
| `fix-branch-name` | Rename the current branch to better match its changes. |
| `postmortems` | Create, update, and audit structured incident postmortems. |
| `svelte-guidance` | Apply project preferences when working in Svelte or SvelteKit. |
| `technical-writing` | Create, update, review, and audit technical documentation. |
| `todo-list` | Maintain a lightweight project task list in `docs/TODO.md`. |

## Repository Layout

The `skills` CLI discovers skills from `skills/<name>/SKILL.md`:

```text
skills/
  technical-writing/
    SKILL.md
  todo-list/
    SKILL.md
    agents/
      openai.yaml
```

Every `SKILL.md` must include YAML frontmatter with a unique `name` and a
clear `description`:

```markdown
---
name: technical-writing
description: Create, update, review, and audit technical documentation.
---
```

## Local Verification

From this repository, verify discovery with:

```bash
npx skills add . --list
```
