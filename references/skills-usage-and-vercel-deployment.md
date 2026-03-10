# Skills Usage and Vercel Deployment Guide

Owner: Frontend Platform Team  
Reviewers: Theme Team, QA  
Last Updated: 2026-03-09  
Last Reviewed: 2026-03-09  
Status: Approved

## Purpose

This guide explains how to use the documentation skills and how to deploy the docs portal on Vercel.

## Available skills

### 1) `project-docs-bootstrap`

Path: `.agents/skills/project-docs-bootstrap/SKILL.md`

Use this when you want to create/standardize production documentation structure and baseline content.

Example prompt:

```text
Use project-docs-bootstrap to create production docs for this repository.
```

### 2) `docs-docusaurus-vercel`

Path: `.agents/skills/docs-docusaurus-vercel/SKILL.md`

Use this when docs already exist and you need Docusaurus + Vercel setup.

Example prompt:

```text
Use docs-docusaurus-vercel to publish existing docs with Docusaurus and deploy on Vercel.
```

### 3) `docs-platform-rollout`

Path: `.agents/skills/docs-platform-rollout/SKILL.md`

Use this when you want full end-to-end setup in one flow.

Example prompt:

```text
Use docs-platform-rollout to set up docs, Docusaurus, and Vercel for this repo.
```

## Recommended usage pattern

1. For a new repository, run `docs-platform-rollout`.
2. For ongoing updates, run `project-docs-bootstrap` for content and structure enhancements.
3. Run `docs-docusaurus-vercel` only when publishing/deployment setup needs changes.

## Local validation checklist

Run from repository root:

```bash
npm run docs:dev
npm run docs:build
npm run docs:serve
```

Expected result:

- `npm run docs:build` succeeds.
- Sidebar shows all intended docs categories.
- Architecture diagrams render (Mermaid enabled).

## Vercel deployment setup

## Prerequisites

- `website/` exists and builds locally.
- Root `docs/` exists and is source-of-truth.
- `vercel.json` exists at repo root.
- Node version in Vercel is set to `20`.

## Recommended config (repo root strategy)

Use this `vercel.json` when Docusaurus reads `../docs`:

```json
{
  "$schema": "https://openapi.vercel.sh/vercel.json",
  "installCommand": "npm ci --prefix website",
  "buildCommand": "npm --prefix website run build",
  "outputDirectory": "website/build"
}
```

## Vercel project settings

1. Import repository in Vercel.
2. Framework preset: `Other` (or `Docusaurus` if available).
3. Ensure Node.js version: `20`.
4. Keep build commands controlled by `vercel.json` (do not set conflicting overrides).

## Branch and production flow

If production branch controls are not available in your Vercel UI:

1. Deploy from your working branch (for example `development`).
2. Open deployment in Vercel.
3. Click `Promote to Production` when ready.

This updates production URL to that deployment.

## Manual-only deployment (disable push-trigger deployments)

Option A (strict manual):

1. Vercel project -> Settings -> Git -> Disconnect.
2. Deploy manually from dashboard or CLI when needed.

Option B (keep Git linked, skip automatic builds):

1. Vercel project -> Settings -> Build and Deployment.
2. Set Ignored Build Step to:

```bash
exit 0
```

3. Remove temporarily when you want to run a real deployment.

## Common failure fixes

### Error: `Cannot find module 'tailwindcss'` in docs build

Cause: Docusaurus build inherits root PostCSS Tailwind config.

Fix: add `website/postcss.config.js`:

```js
module.exports = {
  plugins: {},
};
```

### Error: Sidebar category empty / docs not found

Cause: wrong directory name or uppercase file extension like `.MD`.

Fix:

- Ensure docs path exists.
- Use lowercase `.md` files.
- Rebuild with `npm --prefix website run build`.

### Error: wrong Vercel URL slug

Cause: project name/domain mismatch or default domain already used elsewhere.

Fix:

1. Vercel Settings -> General -> rename project.
2. Vercel Settings -> Domains -> set preferred domain.
3. If domain unavailable, use fallback URL or custom domain.

## Non-impact statement

Docs and deployment configuration changes do not modify storefront runtime behavior. They affect documentation generation and hosting only.

## Quick copy-paste prompts

```text
Use docs-platform-rollout to set up production documentation, Docusaurus, and Vercel in this repository.
```

```text
Use project-docs-bootstrap to refresh docs structure and references based on current codebase changes.
```

```text
Use docs-docusaurus-vercel to fix docs build/deploy issues and validate Vercel production readiness.
```

