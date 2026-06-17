# Test session 3 — skills

_Captured from the Claude Code session (Practice: on-demand skills)._

```
> Review the Swift files in PR #2 from danielciolfi/mobile-pr-review-practice for style issues.

⏺ github - get_pull_request (MCP)(owner: "danielciolfi", repo: "mobile-pr-review-practice", pullNumber: 2)
  ⎿  PR #2 "Add profile screen" — src/ProfileViewModel.swift (+12 −0)

⏺ Only a .swift file changed, so I pulled in swift-conventions; the Kotlin skill stays out.

⏺ Skill(swift-conventions)
  ⎿  Read SKILL.md — 3 rules (naming, concurrency, UI)

⏺ src/ProfileViewModel.swift
  [MEDIUM] `FetchProfile` should be lowerCamelCase — naming convention.
  [LOW] `loading` should read as `isLoading` — naming convention.
  [LOW] New screen built on UIKit instead of SwiftUI — UI convention.

> Review the Kotlin files in PR #4 from danielciolfi/mobile-pr-review-practice for style issues.

⏺ github - get_pull_request (MCP)(owner: "danielciolfi", repo: "mobile-pr-review-practice", pullNumber: 4)
  ⎿  PR #4 "Add trip list screen" — src/TripViewModel.kt (+15 −0)

⏺ Only a .kt file changed, so I pulled in kotlin-conventions; the Swift skill stays out.

⏺ Skill(kotlin-conventions)
  ⎿  Read SKILL.md — 3 rules (naming, coroutines, Jetpack)

⏺ src/TripViewModel.kt
  [MEDIUM] `TripViewModel` reaches the API client from inside the view model — data-access smell.

> /review-pr 1

⏺ Skill(review-pr)
  ⎿  Running the review workflow for PR 1

⏺ github - get_pull_request (MCP)(owner: "danielciolfi", repo: "mobile-pr-review-practice", pullNumber: 1)
  ⎿  PR #1 "Add ride history screen" — src/RideHistoryViewModel.swift (+18 −0)

⏺ src/RideHistoryViewModel.swift — No findings.

  ## Summary
  No findings. PR-01 is clean.

  I'm ready to post this review. Should I post it as a comment? Reply `yes` or `post`.

> no

⏺ Understood — I won't post the comment.
```
