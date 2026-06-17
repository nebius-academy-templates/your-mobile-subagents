---
name: review-pr
description: "Run the full mobile PR review on a single explicit command: /review-pr <number>. Triggered explicitly, not auto-invoked."
disable-model-invocation: true
---

## Steps

1. **Fetch the PR.** Use the GitHub MCP server (`get_pull_request`) to fetch the diff for the
   PR number in `$ARGUMENTS` from `danielciolfi/mobile-pr-review-practice`.
2. **Review Swift files.** For every changed `.swift` file, apply the `swift-conventions`
   skill and record style findings.
3. **Review Kotlin files.** For every changed `.kt` file, apply the `kotlin-conventions`
   skill and record style findings.
4. **Flag security issues.** Scan all changed files for hardcoded API keys, tokens,
   passwords, or secrets, unsafe API usage, and missing input validation. Mark hardcoded
   credentials `[HIGH]`.
5. **Compile findings** into the output format from `CLAUDE.md`: organized per file with
   `[SEVERITY]` tags, ending with a `## Summary` section.
6. **Present and gate.** Show the complete review and ask: "Post this as a comment? Reply
   `yes` or `post`." Post the comment **only** if the user replies `yes` or `post`; otherwise
   do nothing.
