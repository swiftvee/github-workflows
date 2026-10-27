# github-workflows

Reusable GitHub Actions workflows for the swiftvee repos.

## Post PR status to Slack

Keeps one message per PR in #pull-requests: posted when the PR opens, updated as it moves between draft,
ready for review, approved and changes requested, and deleted when it closes. The message is found by its
PR link in the channel history, so nothing is stored.

Add `.github/workflows/pr_slack_message.yml` to a repo:

```yaml
name: Post PR status to Slack

on:
  pull_request:
    types: [opened, reopened, edited, converted_to_draft, ready_for_review, closed]
  pull_request_review:
    types: [submitted, dismissed]

permissions:
  pull-requests: read

jobs:
  slack_message:
    uses: swiftvee/github-workflows/.github/workflows/pr_slack_message.yml@main
    secrets:
      slack-token: ${{ secrets.SLACK_PR_STATUS_TOKEN }}
```

`slack-token` is the Slack app's Bot User OAuth Token (`xoxb-`). The bot must be a member of #pull-requests.
