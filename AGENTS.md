# Agent rules

- Before editing, read the Issue, state necessary assumptions, and identify the exact allowed files and acceptance checks. Report missing information rather than inventing it.
- Make the smallest requested change. Do not add speculative features, dependencies, services, or unrelated cleanup.
- Demo task changes are restricted to `docs/` and `.github/ISSUE_TEMPLATE/`. Preserve existing files and rules; do not overwrite unrelated work.
- Work on an independent branch. Open a draft PR that references the Issue and records the baseline SHA, final SHA, changed files, actual checks, and any unverified steps.
- For this documentation-only demo, verify `git diff --check` and the allowed file list. Do not run application or trading code.
- Never merge automatically, deploy, execute real trades, access secrets or sensitive account data, or configure external automation.
- Creating or assigning an Issue is not evidence that Codex executed it. A PR author's summary is not an independent Chat review. Report only actions and checks that actually completed.
