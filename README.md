# szymon-stack

Skills for reviewing GitHub pull requests and stacks of dependent PRs.

Version: 1.0.1

## szymon-stack skill

The [szymon-stack skill](skills/szymon-stack/SKILL.md) reviews one PR at a time, follows stack dependencies, and reports:

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

Install the **szymon-stack** plugin from the plugin directory of your agent.

To install by hand, clone this repository and copy `skills/szymon-stack` into your agent's skills directory. For Codex, the default user skills directory is `~/.codex/skills`.

## Use

Invoke `/szymon-stack` with a GitHub PR URL or number. Without a PR, the skill uses the PR for the current branch.

## Example prompts

Run these in a local clone of a repository that you can access with `gh`.

### Review one pull request

```text
/szymon-stack https://github.com/OWNER/REPO/pull/123
```

### Review a stack of dependent pull requests

```text
Use szymon-stack to review the PR stack that starts at #120.
Review from the bottom of the stack upward and stop after each PR.
```

### Review the current branch

```text
Use szymon-stack to review the pull request for my current branch.
Do not post anything on GitHub.
```

## Privacy

Effective date: 9 October 2026

This notice covers the **szymon-stack** plugin and its skill. It is published by Szymon Dziedzic.

### What the plugin does

The plugin contains one instruction-only skill. The skill tells your coding agent how to review a GitHub pull request or a stack of dependent pull requests.

To do this, the agent runs commands on your own computer with your own tools, such as Git and the GitHub CLI (`gh`). It reads data that your GitHub account can access: pull request titles, descriptions, authors, comments, reviews, CI status, and source code. This data can include names, usernames, and other personal information of the people who worked on the pull request.

The skill only reads and reports. It posts a review, a comment, an approval, or a change request on GitHub only when you explicitly ask for that specific action.

### Data handling

The plugin contains no executable scripts, hooks, network tools, or servers. The publisher does not operate any service for this plugin. The publisher does not collect, store, or receive your prompts, your code, the pull request data, or the generated review.

Other parties process this data under their own terms:

- **The host assistant provider** processes your prompts, the data that the agent reads, and the generated output. For Claude, see [Anthropic's privacy policy](https://www.anthropic.com/legal/privacy). For ChatGPT and Codex, see [OpenAI's privacy policy](https://openai.com/policies/privacy-policy/).
- **GitHub** processes the requests that the agent makes with your GitHub credentials, and any comment that you ask the agent to post. See [GitHub's privacy statement](https://docs.github.com/site-policy/privacy-policies/github-general-privacy-statement).

This notice makes no promise about the retention, training, or other data practices of these providers.

### Support and reports

For questions, bugs, or a security concern, use [the repository issue tracker](https://github.com/szdziedzic/s-stack/issues). Issues are public. Do not post secrets, access tokens, personal information, private source code, or sensitive exploit details. Use a minimal example with invented data.

## Changes

- 1.0.1: The skill is now named `szymon-stack`. Invoke it with `/szymon-stack`.

## Support and security reports

Use [GitHub issues](https://github.com/szdziedzic/s-stack/issues) for questions, bugs, or an initial security report. This is a public channel. Do not include secrets, personal information, private source code, or sensitive exploit details. Use a minimal example with invented data.
