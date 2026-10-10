---
name: szymon-stack
description: Review a GitHub pull request or a stack of dependent PRs, one layer at a time, and report a verdict, a simple explanation with diagrams, a design judgment, and prioritized comments with verified line anchors and a copy-paste version of each comment. Use when the user runs /szymon-stack, or asks to review a PR or PR stack in this format.
---

# Stack review

Review one PR at a time. Start with the PR the user gives. If none is given, use the PR for the current branch (`gh pr view`).

This skill only reads and reports. Never post, approve, comment, or request changes on GitHub unless the user explicitly asks for that specific action.

## 1. Collect facts

Do not change the current branch or worktree. Get the PR head as a separate ref.

```bash
gh pr view <n> --json title,body,author,baseRefName,headRefName,headRefOid,files,reviews,comments
gh api repos/<owner>/<repo>/pulls/<n>/comments      # inline review comments
gh pr checks <n>
git fetch -q origin pull/<n>/head:pr-<n> <default-branch>
git diff origin/<default-branch>...pr-<n>            # or the base branch for stacked PRs
```

- **Find the stack.** Follow `baseRefName` down to the default branch. Find the PRs whose base is this PR's head branch (`gh pr list --base <headRefName>`). The PR body often lists the stack. Review from the bottom of the stack upward.
- **Read full files, not only diff hunks.** Read each new or changed file at `pr-<n>`. For code that moved, compare the old and new versions and look for lost comments, guards, or behavior. Read the callers of changed APIs.
- **Read the conventions.** Read `CLAUDE.md`, `AGENTS.md`, package-level instruction files, `CONTRIBUTING`, and the PR template. Read any saved user feedback or memory about code style. Look at the code next to the change to learn the local idioms.
- **Verify external claims.** Examples: "requires release X of package Y" (check the registry or the tarball), "companion PR merged" (check it), "CI passes" (check `gh pr checks`).
- **Existing reviews.** Do not repeat what reviewers already said, unless you add something new.

Use only facts you observed. When you infer something (for example, from a later PR's title), label it as an inference.

## 2. Analyze

- **Correctness:** error paths, races, idempotency, cleanup on failure, timeouts, security (tokens, public exposure), backward compatibility, and rollout order.
- **Design:** Is the abstraction at the right level? Is ownership and lifetime clear? Is there duplicated code? Is the change larger than it needs to be?
- **Style and practices:** Compare with the repo conventions and the code nearby. This includes error types, logging (no noise, no internal paths), error reporting and monitoring, temp files, tests, changelog, commit message format, and types. Check the conventions that apply; do not invent new ones.
- **Stack context:** If a later PR in the stack appears to fix a finding, check that PR's diff. Then say "fixed in #N (verified)" or "#N's title suggests a fix (not verified)". Keep a list of deferred findings, and check them when you review that PR.

## 3. Priorities

| Priority | Meaning |
|---|---|
| **P1** | Must fix before merge: a bug, data loss, a security issue, a broken rollout, or a user-facing regression. |
| **P2** | Should fix: a real risk, a missing monitoring or error-reporting signal, a slow or confusing failure path, or a maintainability problem. |
| **P3** | Optional: a nit, a style point, naming, or a small cleanup. |

## 4. Output format

Use these sections in this order.

### Verdict

One line: **Approve**, **Approve with comments**, **Request changes**, or **Needs discussion**. Then 1–3 sentences on why, and on what blocks the merge, if anything. Mention whether CI passes.

### How it works

Explain the change very simply, for a reader who has not seen the code.

- Use ASCII diagrams in fenced code blocks, because they render in every terminal. Use Mermaid only if the user's viewer renders it.
- Useful diagram types:
  - **Before / after**: ownership or data flow.
  - **Numbered steps**: a lifecycle or a shutdown order.
  - **Parallel vs. sequential**: concurrency.
- Add images only if they help (for example, UI changes). Use screenshots from the PR, or run the app. Never invent an image.
- Add a short "Checked and correct" list with the risky parts you verified. This tells the author what is fine.

### Design judgment

3–6 bullets. Label each **Good**, **Acceptable**, or **Watch**. Give a recommendation, not a list of every option.

### Comments

Sort the comments by priority (P1 first). For each comment:

1. A heading: `### P<n> — <number>. <short title>`
2. **Where:** a verified anchor, placed outside any code block. For GitHub PRs, use a permalink pinned to the reviewed head commit: `https://github.com/<owner>/<repo>/blob/<headRefOid>/<path>#L<x>-L<y>`. Also show the short form `path:x-y`. Get the line numbers from the PR head (for example, `git show pr-<n>:<path> | grep -n ...`). Never guess them.
3. **Problem:** 2–4 short sentences or bullets. Say what happens, when, and why it matters.
4. The copy-paste version, in its own fenced `text` block. Rules for this block:
   - Only this one comment. No location links, no numbering, no summaries of the whole review.
   - It must make sense without this conversation.
   - Write it in a friendly peer-review voice. Start P3 comments with `nit:`.
   - Suggest a concrete fix. Show a small code snippet if it makes the fix clearer.
   - If a later stack PR may fix the problem, say so, and offer to resolve the comment.

If there are no findings, say so. Do not add empty blocks.

### Style and practices check

A table: `| Area | Result |`, with ✅ or ⚠️ and a reference to the related comment number.

### Questions for the author

Only questions whose answer you could not find yourself.

### Next

Name the next PR in the stack, and ask whether to continue.

## Writing style

- Use simple words and short sentences, with one idea per sentence. Use active voice.
- Use the same term for the same thing every time.
- Be concrete: name the file, the function, the value, and the time or size.
- No filler, no praise without substance, and no hedging on facts you verified.
