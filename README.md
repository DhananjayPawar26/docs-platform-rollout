# docs-platform-rollout

This skill bootstraps a documentation platform for an existing codebase.

Using this skill will create:

1. A `docs/` folder that contains code-related documentation content. This content should be reviewed by humans before it is treated as final.
2. A `website/` folder that contains the code for the documentation website.

It will also create or update a `vercel.json` configuration file. You need to review that file and make sure your Vercel deployment is pointing to the correct directory and build strategy for your repository.

You can also add a rule or CI/CD check in your IDE, repository, or pull request workflow so that every PR verifies whether the documentation was updated when code changes require it.

## Install

```bash
npx skills add DhananjayPawar26/docs-platform-rollout
```
