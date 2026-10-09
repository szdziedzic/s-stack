# Privacy notice

Effective date: 9 October 2026

This notice covers the **s-stack** plugin and its skills, including **s-stack-review**. It is published by Szymon Dziedzic.

## What the plugin does

The plugin contains instruction-only skills. The s-stack-review skill tells your coding agent how to review a GitHub pull request or a stack of dependent pull requests.

To do this, the agent runs commands on your own computer with your own tools, such as Git and the GitHub CLI (`gh`). It reads data that your GitHub account can access: pull request titles, descriptions, authors, comments, reviews, CI status, and source code. This data can include names, usernames, and other personal information of the people who worked on the pull request.

The skill only reads and reports. It posts a review, a comment, an approval, or a change request on GitHub only when you explicitly ask for that specific action.

## Data handling

The plugin contains no executable scripts, hooks, network tools, or servers. The publisher does not operate any service for this plugin. The publisher does not collect, store, or receive your prompts, your code, the pull request data, or the generated review.

Other parties process this data under their own terms:

- **The host assistant provider** processes your prompts, the data that the agent reads, and the generated output. For Claude, see [Anthropic's privacy policy](https://www.anthropic.com/legal/privacy). For ChatGPT and Codex, see [OpenAI's privacy policy](https://openai.com/policies/privacy-policy/).
- **GitHub** processes the requests that the agent makes with your GitHub credentials, and any comment that you ask the agent to post. See [GitHub's privacy statement](https://docs.github.com/site-policy/privacy-policies/github-general-privacy-statement).

This notice makes no promise about the retention, training, or other data practices of these providers.

## Support and reports

For questions, bugs, or a security concern, use [the repository issue tracker](https://github.com/szdziedzic/s-stack/issues). Issues are public. Do not post secrets, access tokens, personal information, private source code, or sensitive exploit details. Use a minimal example with invented data.
