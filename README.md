# s-stack

Skills for reviewing GitHub pull requests and stacks of dependent PRs.

## s-stack-review

The [s-stack-review skill](skills/s-stack-review/SKILL.md) reviews one PR at a time, follows stack dependencies, and reports:

- A verdict and CI status
- A simple explanation with diagrams
- A design judgment
- Prioritized findings with verified commit and line anchors
- A copy-paste version of each review comment
- A style and practices check

The skill reads and reports. It posts reviews or comments on GitHub only when explicitly requested.

## Install

Clone this repository and copy `skills/s-stack-review` into your agent's skills directory. For Codex, the default user skills directory is `~/.codex/skills`.

## Use

Invoke `/s-stack-review` with a GitHub PR URL or number. Without a PR, the skill uses the PR for the current branch.

Requires Git, the GitHub CLI (`gh`), and authenticated access to the repository being reviewed.
