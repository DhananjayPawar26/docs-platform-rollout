---
name: project-docs-bootstrap
description: Create production-grade project documentation structure and baseline content for any codebase. Use when users ask to document a project end-to-end, standardize docs across teams, or bootstrap docs folders (overview, architecture, reference, operations, ADRs, quality, contributing, business requirements).
metadata:
  short-description: Bootstrap full project docs
---

# Project Docs Bootstrap

Use this skill to create a reusable, production documentation foundation inside a repository.

## When to use

- User asks to "document the entire project".
- Team needs standard docs layout for engineering onboarding and operations.
- Organization wants consistent docs across multiple repos.

## Output standard

Create a `docs/` tree with these sections:

- `00-overview`
- `01-getting-started`
- `02-architecture`
- `03-reference`
- `04-how-to`
- `05-operations`
- `06-decisions`
- `07-quality`
- `08-contributing`
- `09-theme` (or domain-specific section)
- `10-business-requirement` (if business workflows are required)

Also create `docs/README.md` as index and governance entry point.

## Document metadata

Every critical doc should include:

- Owner
- Reviewers
- Last Updated (YYYY-MM-DD)
- Last Reviewed (YYYY-MM-DD)
- Status (Draft, Approved, Deprecated)

## Execution workflow

1. Inventory project structure (`pages`, `components`, `queries`, `config`, runtime/build files).
2. Create docs folders and starter files.
3. Fill architecture docs from real code (entry points, data flow, module boundaries).
4. Fill reference docs from actual file inventories.
5. Add how-to runbooks for common tasks.
6. Add operations, rollback, incident, quality docs.
7. Add ADR template and at least one accepted ADR for docs strategy.
8. Add known risks and validation checks.
9. Run markdown/build validation if docs site is present.

## Required quality rules

- No invented architecture; extract from repository files.
- Explicitly record known gaps and missing scripts.
- Prefer deterministic inventories (generated from filesystem).
- Keep doc names lowercase with `.md` extension only.

## Acceptance criteria

- Complete docs tree exists and is internally linked.
- Reference docs map to actual source directories.
- ADR and quality docs are present.
- No broken markdown links in local validation.

