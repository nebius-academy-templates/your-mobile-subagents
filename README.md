# PR Review Agent — practice project

You are building a PR Review Agent for the mobile team. It reviews Swift and Kotlin pull
requests for style, security, and architecture issues, organizes findings per file with
`[SEVERITY]` tags, ends with a `## Summary`, and always asks for confirmation before posting
a comment to GitHub.

## Files to complete in this task

- `.claude/agents/style-reviewer.md` — sub-agent that reviews Swift and Kotlin diffs for style.
- `.claude/agents/security-reviewer.md` — sub-agent that reviews diffs for security issues.
- `.claude/agents/architecture-reviewer.md` — sub-agent that reviews diffs against the
  architecture guidelines.
- `.claude/skills/architecture-guidelines/SKILL.md` — guidelines preloaded by the architecture
  reviewer.
- `.claude/skills/review-pr/SKILL.md` — update the workflow to delegate to the three sub-agents
  in sequence and consolidate their findings.
- `results/test-session-4.md` — a transcript of the run showing all three sub-agents firing and the
  consolidated output.
