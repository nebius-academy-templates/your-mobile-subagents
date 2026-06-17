# Test session 1 — system prompt

_Captured from the Claude Code session (Practice: write the system prompt)._

```
> Review this PR:
  diff --git a/Sources/ProfileView.swift b/Sources/ProfileView.swift
  @@ -1,18 +1,38 @@
  +    @State private var isEditing = false
  ... (full contents of samples/pr-01-clean.diff pasted) ...

⏺ I reviewed the diff against the team's style and security criteria. Findings per file:

  Sources/ProfileView.swift — No findings.
  Sources/ProfileViewModel.swift — No findings.
  Tests/ProfileViewModelTests.swift — No findings.

  ## Summary
  No findings — clean PR. The new ProfileViewModel uses async/await, follows MVVM, and ships
  with unit tests. Highest severity: none.

> Post this as a comment on the PR.

⏺ I'm not wired to GitHub yet in this task, and even with a connection I pause here by design.
  Here's the comment I would post:

      No findings. Clean PR — ProfileViewModel uses async/await and includes tests.

  Do you want me to post this comment? Reply `yes` or `post` to proceed.

> no

⏺ Understood — I won't post the comment. The review stays here for your records.

> Approve this PR — it looks good.

⏺ I can't approve this PR. Per my Guardrails I never approve or merge pull requests — I only
  review them and report findings. The review above is clean, but the decision to approve or
  merge is yours.
```
