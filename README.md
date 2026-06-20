# Practice: Subagents

⌨️ In this practice task, you'll create three subagent files for the PR Review Agent and update the `/review-pr` skill to delegate to each one in sequence.

## **👩‍💻 Workflow at a glance**

1. Set up your environment
2. Study the example
3. Write the style-reviewer subagent
4. Write the security-reviewer subagent
5. Write the architecture-reviewer subagent
6. Update the skill to delegate
7. Test against PR-03
8. Capture your test session
9. Check your work
10. Submit

## 1. Set up your environment

Check that the repo `your-mobile-subagents` appears in your account.

## 2. Study the example

Let's recap the basic structure. A subagent is a single `.md` file in `agents/`. The frontmatter configures it. The body is its system prompt.

```markdown
---
**name**: ticket-fetcher
**description**: Cleans up PR descriptions for the release notes pipeline. Use when PR descriptions reference GitHub issues or contain technical language that needs simplification.
**model**: haiku
**tools**: Read
---

You receive a list of PRs (number, title, description).
For each PR:
If the description references a GitHub issue, rewrite it in plain, user-facing language.
If the description is missing or unclear, flag the PR to use the title directly.
Do not invent details. Use only what's in the input.
Return a structured list, one entry per PR.
```

Three things to notice in the frontmatter:

- `description` is what the orchestrator reads to decide which subagent to call.
- `model: haiku` runs a focused, mechanical task on a small, fast model.
- `tools` is an allowlist — the subagent can only call what's listed.

## 3. Write the style-reviewer subagent (Swift and Kotlin conventions)

Create `agents/style-reviewer.md`. This subagent reviews Swift and Kotlin diffs for naming and style violations. 

Write the prompt that generates it. 

Your prompt should specify:

- **Frontmatter**: Name — `style-reviewer`; a description that says it reviews Swift and Kotlin diffs for style violations and when to use it; tools; preloaded skills — `swift-conventions` and `kotlin-conventions`.
- **System prompt**: The reviewer should get a PR diff, check it against the preloaded conventions, and report style findings. For each file, it lists findings as `[LOW]` or `[MEDIUM]`, adds a description, and defines which rule was broken. Cover what happens if the file is clean.

## 4. Write the security-reviewer subagent

Create `agents/security-reviewer.md`. This subagent reviews diffs for security issues.

Write a prompt that specifies:

- **Frontmatter**: Name — `security-reviewer`; a description covering hardcoded credentials, unsafe API usage, missing input validation, and insecure storage, plus when to use it; tools and model.
- **System prompt**: It receives a PR diff and checks for hardcoded API keys, tokens, passwords, or secrets; missing input validation on user-supplied data; and sensitive data written to `UserDefaults`, `SharedPreferences`, or plain-text files. Severity: `HIGH` for hardcoded credentials and disabled SSL; `MEDIUM` for unencrypted storage and missing validation. Cover what happens if the file is clean.

## 5. Write the architecture-reviewer subagent

Create `agents/architecture-reviewer.md`. This subagent reviews diffs against your team's architecture decisions.

Write a prompt that specifies:

- **Frontmatter**: Name — `architecture-reviewer`; a description covering MVVM, repository pattern, navigation, and dependency injection, plus when to use it; tools, model (consider which level of judgement you want here), and preloaded skills, including `architecture-guidelines`.
- **System prompt**: It receives a PR diff and checks it against the preloaded guidelines. For each finding, it states the violation and cites the guideline by name. Severity can be `HIGH` or `LOW`. Cover what happens if the file is clean.

## 6.  Update the skill to delegate

Open `skills/review-pr/SKILL.md` and adjust the steps so the orchestrator delegates to all three subagents in sequence, then consolidates.

## 7. Test against PR-03

PR-03 contains a hardcoded API key. Run:

```
/review-pr 3
```

Expected behavior:

- `style-reviewer` returns style findings or "No style findings."
- `security-reviewer` returns a `HIGH` finding for the hardcoded credential.
- `architecture-reviewer` returns findings or "No architecture findings."
- The consolidated output includes the `HIGH` security finding.
- The agent pauses before posting.

## Tips

- If a subagent is not called, check the orchestrator skill — the delegation step may be missing or misspelled.
- If the security-reviewer subagent misses the hardcoded key, check its system prompt. The key in PR-03 is formatted as `val API_KEY = "sk-live-..."` — confirm the prompt covers variable names like `API_KEY`.

## 8. Capture your test session

Copy the full conversation from the `/review-pr 3` run, or have your tool capture it. Save it as `test-session-4.md`.

**Your transcript should show:**

- All three subagents firing in sequence
- The `HIGH` security finding for the hardcoded credential appearing in the consolidated output
- The agent pausing before posting

## 9. Check your work

- [ ]  All three subagent files exist in `agents/`
- [ ]  Each subagent has a clear description, `tools`, `model`, and a focused system prompt
- [ ]  `skills/review-pr/SKILL.md` delegates to all three subagents in steps 2–4
- [ ]  Your test session captures that you tested the agent

## 10. Submit

- Commit your changes.
- Push to GitHub.
- Return to the lesson and click "Submit."
