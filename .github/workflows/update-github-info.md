---
name: update-github-info
description: Keep Mona's GitHub Info page current with practical, sourced updates from GitHub Blog and Changelog.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
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
safe-outputs:
  create-pull-request:
    allowed-files:
      - site/content/github-info.md
    draft: false
    max: 1
---

# Update GitHub Info

Read `notes/mona-notes.md` using the GitHub repository API. Fetch both
https://github.blog/latest/ and https://github.blog/changelog/ with the web-fetch
tool. Compare relevant new information with `site/content/github-info.md`.

Update only that page with concise, practical guidance that helps developers
learn GitHub faster. Preserve useful existing content, include source links for
any information drawn from the GitHub Blog or Changelog, and do not add claims
that the fetched sources do not support. Use the edit tool to make the change.

When there is a worthwhile update, open one pull request for Mona to review.
Describe the update and cite its sources in the pull request body. Use the
configured `create-pull-request` safe output; do not push directly to `main` or
write any other file. If the sources contain no useful new information, leave
the page unchanged and call `noop` with a brief reason.
