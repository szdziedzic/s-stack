# s-stack

Skills for reviewing GitHub pull requests and stacks of dependent PRs.

Version: 1.0.0

## s-stack-review

The [s-stack-review skill](skills/s-stack-review/SKILL.md) reviews one PR at a time, follows stack dependencies, and reports:

- A verdict and CI status
- A simple explanation with diagrams
- A design judgment
- Prioritized findings with verified commit and line anchors
- A copy-paste version of each review comment
- A style and practices check

The skill reads and reports. It posts reviews or comments on GitHub only when explicitly requested.

## Requirements

The skill runs commands on your computer. Use it in a coding agent that can run shell commands, such as Claude Code or Codex. It needs:

- Git
- The GitHub CLI (`gh`), signed in with access to the repository being reviewed

It does not work in a chat-only assistant that cannot run commands.

## Install

Install the **s-stack** plugin from the plugin directory of your agent.

To install by hand, clone this repository and copy `skills/s-stack-review` into your agent's skills directory. For Codex, the default user skills directory is `~/.codex/skills`.

## Use

Invoke `/s-stack-review` with a GitHub PR URL or number. Without a PR, the skill uses the PR for the current branch.

## Example prompts

Run these in a local clone of a repository that you can access with `gh`.

### Review one pull request

```text
/s-stack-review https://github.com/OWNER/REPO/pull/123
```

### Review a stack of dependent pull requests

```text
Use s-stack-review to review the PR stack that starts at #120.
Review from the bottom of the stack upward and stop after each PR.
```

### Review the current branch

```text
Use s-stack-review to review the pull request for my current branch.
Do not post anything on GitHub.
```

## Privacy

See the [privacy notice](PRIVACY.md). The plugin has no server. Your agent reads pull request data with your own GitHub credentials. The host assistant and GitHub process that data under their own terms.

## Support and security reports

Use [GitHub issues](https://github.com/szdziedzic/s-stack/issues) for questions, bugs, or an initial security report. This is a public channel. Do not include secrets, personal information, private source code, or sensitive exploit details. Use a minimal example with invented data.
