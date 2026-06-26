---
name: "svelte-guidance"
description: "Invoke this skill every time you work in a Svelte or SvelteKit codebase; it contains valuable guidance and preferences for how to structure things in such applications."
---

## General Rules

- Avoid $effect. In almost all cases the thing you want to do can be done with $derived or an attachment.

## Components

- Structure the application into reusable Svelte components.
- Make use of CSS utility classes (and specifically Tailwind utilities, if the project is using Tailwind.)
- Build a design library of:
  - Utility classes (`.button`, `.link` etc.)
  - Low-level UI components (`<Button>`, `<Card>` etc.)
  - Higher-level application-specific components (`<ArticleTeaser>`, `<BlockComment>` etc.)
- Use Storybook! If the app is not yet using Storybook, encourage the user to consider installing it. Document all components and utilities in Storybook, grouped by function/category.
- Avoid "table-driven"-style code; this is not Go. Just use components directly.

## CSS

- If the application uses Tailwind, **make use of it**. Don't litter a Tailwind-enabled app with style blocks!
- The the application doesn't use Tailwind, style blocks are, of course, perfectly fine.
