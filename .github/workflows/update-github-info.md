---
name: update-github-info
description: Refresh GitHub information for the site from Mona's notes and GitHub Blog updates.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
strict: true
network:
  allowed:
    - github.blog
    - github.com
tools:
  github:
    mode: local
    toolsets: [repos]
  edit: true
  web-fetch: {}
safe-outputs:
  create-pull-request:
    reviewers: [Mona]
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Information

Read `notes/mona-notes.md` and use GitHub repository API tools to read repository guidance and reference files. Do not use terminal commands, the GitHub CLI, or sandboxed commands for repository reads.

Fetch and review these public sources:

- [GitHub Blog latest](https://github.blog/latest/)
- [GitHub Blog changelog](https://github.blog/changelog/)

Update `site/content/github-info.md` only when the sources contain accurate, relevant GitHub changes that warrant a site update. Preserve the existing content style and avoid speculation.

Use the configured `create-pull-request` safe output to propose the update and request Mona's review. Do not write directly to the default branch. Call `noop` with a short reason when there is no meaningful update, the evidence is insufficient, or the proposed content duplicates the current file.
