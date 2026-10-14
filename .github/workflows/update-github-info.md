---
name: update-github-info
description: Keep Mona's GitHub Info page current with practical, sourced updates from GitHub Blog, Changelog, and Awesome Copilot workflows.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
model: gpt-5-mini
engine:
  id: copilot
  copilot-sdk: true
tools:
  github:
    toolsets: [repos]
  edit:
  web-fetch:
  bash: ["cat"]
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

Read `notes/mona-notes.md` with the GitHub repository `get_file_contents` tool
before making changes.

Use `web-fetch` for these public sources:
- GitHub Blog: https://github.blog/latest/
- GitHub Changelog: https://github.blog/changelog/
- Awesome Copilot: https://awesome-copilot.github.com/workflows/

Do not use shell commands (python, curl, etc.) to fetch web content.

Do the work yourself. Do not delegate to sub-agents or the `task` tool.

Update `site/content/github-info.md` with concise,
practical updates for readers and include source context when content comes
from the GitHub Blog or GitHub Changelog.

Open a pull request for Mona to review. 
Use a pull request title that mentions Mona or GitHub Info. 
Do not write directly to `main`;
rely on `safe-outputs` with `create-pull-request`.