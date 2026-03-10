---
name: docs-docusaurus-vercel
description: Set up Docusaurus for an existing docs-as-code repository and configure Vercel deployment safely. Use when users ask to publish docs, wire docs/ into Docusaurus, configure sidebars/navigation, and deploy on Vercel with manual or controlled production promotion.
metadata:
  short-description: Publish docs with Docusaurus + Vercel
---

# Docs Docusaurus Vercel

Use this skill to convert existing repository docs into a publishable Docusaurus site and deploy it on Vercel.

## When to use

- User asks to host docs on Vercel.
- User has `docs/` and wants a docs portal with sidebar/search/navigation.
- User needs repeatable deployment behavior across branches.

## Target setup

- Docusaurus app in `website/`.
- Root docs remain source-of-truth in `docs/`.
- Docusaurus reads `../docs` from `website/docusaurus.config.ts`.
- Sidebar categories map to docs folder groups (`00...10`).

## Execution workflow

1. Scaffold Docusaurus in `website/`.
2. Configure docs plugin:
   - `path: '../docs'`
   - `routeBasePath: '/docs'` or `'/'` per project decision
   - `sidebarPath: './sidebars.ts'`
3. Add Mermaid support (`@docusaurus/theme-mermaid`).
4. Configure sidebar categories for each docs section.
5. Add root scripts:
   - `docs:dev`
   - `docs:build`
   - `docs:serve`
6. Add `website/postcss.config.js` override to prevent root Tailwind/PostCSS leakage.
7. Add `vercel.json` matching chosen root-directory strategy.
8. Build locally and fix all MDX/route/sidebar errors.

## Critical pitfalls to prevent

- Uppercase `.MD` files are often not detected; use lowercase `.md`.
- If using `path: '../docs'`, ensure Vercel build context can access parent docs directory.
- Avoid mismatched Vercel root directory and build command prefixes.
- CRA framework auto-detection in Vercel can break docs builds; use `Other` or Docusaurus.

## Vercel deployment modes

### Mode A: Repo root build (recommended for `../docs`)

`vercel.json`:

```json
{
  "$schema": "https://openapi.vercel.sh/vercel.json",
  "installCommand": "npm ci --prefix website",
  "buildCommand": "npm --prefix website run build",
  "outputDirectory": "website/build"
}
```

### Mode B: `website` as root directory

`vercel.json`:

```json
{
  "$schema": "https://openapi.vercel.sh/vercel.json",
  "installCommand": "npm ci",
  "buildCommand": "npm run build",
  "outputDirectory": "build"
}
```

## Acceptance criteria

- `npm --prefix website run build` succeeds.
- Sidebar renders all intended sections.
- Vercel deploy succeeds without missing PostCSS/Tailwind plugin errors.
- Production release flow is documented (auto or manual promote).

