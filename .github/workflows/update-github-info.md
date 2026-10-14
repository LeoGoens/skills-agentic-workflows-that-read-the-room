---
name: update-github-info
description: Keep Mona's GitHub Info page current with practical, sourced updates from GitHub Blog, Changelog, and Awesome Copilot workflows.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
model: gpt-5-mini
tools:
  github:
    toolsets: [repos]
  edit: true
  web-fetch: {}
  bash: false
  cli-proxy: false
network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com
safe-outputs:
  create-pull-request:
    allowed-files:
      - site/content/github-info.md
    draft: false
    max: 1
---

# Update Mona's GitHub Info website

Read `notes/mona-notes.md` before making changes.

Use these sources:
- `notes/mona-notes.md`
- GitHub Blog: https://github.blog/latest/
- GitHub Changelog: https://github.blog/changelog/
- Awesome Copilot: https://awesome-copilot.github.com/workflows/

Fetch the sources above only with the `web-fetch` tool. Shell commands
(python, curl, etc.) are not available and will be denied.

Update `site/content/github-info.md` with concise,
practical updates for readers and include source context when content comes
from the GitHub Blog or GitHub Changelog.

Open a pull request for Mona to review. 
Use a pull request title that mentions Mona or GitHub Info. 
Do not write directly to `main`;
rely on `safe-outputs` with `create-pull-request`.