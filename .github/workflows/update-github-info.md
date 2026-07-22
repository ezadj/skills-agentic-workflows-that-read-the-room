---
name: update-github-info
on:
  workflow_dispatch:
  schedule:
    - cron: "15 9 * * *"
permissions:
  contents: read
  pull-requests: read
  issues: read
  actions: read
  copilot-requests: write
tools:
  github:
    mode: gh-proxy
    toolsets: [default]
  edit: true
  web-fetch: {}
network:
  allowed:
    - github
safe-outputs:
  create-pull-request:
    title-prefix: "[ai] "
    draft: true
    base-branch: main
    allowed-files:
      - site/content/github-info.md
---

Update Mona's GitHub updates content for review.

When this workflow runs:

1. Read notes/mona-notes.md to understand Mona's editorial style and priorities.
2. Fetch and review these sources for the latest updates:
   - https://github.blog/latest/
   - https://github.blog/changelog/
3. Update site/content/github-info.md by adding or refreshing concise, reader-friendly updates under the "Latest GitHub Updates" section.
4. Propose the change using the configured safe output by creating a pull request for Mona to review.

Requirements:

- Keep updates concise, clear, and useful for general readers.
- Do not make unrelated file changes.
- If there is no meaningful update to make, call noop and explain why.
