---
name: Weekly Report Status
description: Publish a concise weekly activity report for the repository.
on:
  schedule:
    - cron: "0 9 * * 1"
  workflow_dispatch:
permissions:
  contents: read
  issues: read
  pull-requests: read
  copilot-requests: write
engine: copilot
tools:
  github:
    mode: gh-proxy
    toolsets: [default]
safe-outputs:
  create-issue:
    title-prefix: "[weekly-report] "
    max: 1
---

# Weekly Report Status

Create a concise activity report for the previous seven full days ending at workflow start time in UTC.

Use the GitHub tools to review repository activity during that window:

- commits
- issues opened, closed, or otherwise materially updated
- pull requests opened, closed, merged, or otherwise materially updated

Publish the report as one new issue using the safe output. Use a clear title beginning with `[weekly-report] ` and include the UTC reporting window in the report. Organize the body with `###` headings for a brief summary and separate commit, issue, and pull request sections. Include counts and concise links or identifiers for notable items, while keeping the report easy to scan.

If the reporting window contains no commits, issue activity, or pull request activity, do not create an issue. Call `noop` and state clearly that no repository activity occurred during the evaluated seven-day UTC window.
