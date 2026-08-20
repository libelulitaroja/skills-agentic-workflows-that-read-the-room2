---
name: update-github-info
description: Refresh the GitHub Info page with concise, sourced updates from GitHub.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  metadata: read
strict: true
network:
  allowed:
    - github
    - awesome-copilot.github.com
tools:
  github:
    mode: gh-proxy
    toolsets: [repos]
  edit: true
  web-fetch: {}
safe-outputs:
  create-pull-request:
    allowed-files:
      - site/content/github-info.md
    draft: false
    if-no-changes: warn
    protected-files: request_review
---

# Update GitHub Info

Read `notes/mona-notes.md` and `site/content/github-info.md` before making any change.

Use web fetch to retrieve and review all three sources:

- [GitHub Blog latest](https://github.blog/latest/)
- [GitHub Changelog](https://github.blog/changelog/)
- [Awesome Copilot workflows](https://awesome-copilot.github.com/workflows/)

Update only `site/content/github-info.md` with concise, practical items that help developers learn GitHub faster. Preserve the existing editorial angle and headings where possible. Every item based on these sources must name its source and link to the specific source page. Do not invent facts, and do not add general filler when the sources have no useful update.

Use the configured `create-pull-request` safe output to open a pull request for Mona to review. Include a short summary of the changes and the source links in the pull request body. Do not write directly to the default branch. If no meaningful update is available, call `noop` with a brief explanation instead of opening a pull request.
