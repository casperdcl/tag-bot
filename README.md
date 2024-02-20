# Tag Comment Bot

## Example Usage

Add to `.github/workflows/comment-bot.yml`:

```yml
# runs on any comment matching the format `/tag <tagname> <commit>`
name: Comment Bot
on:
  issue_comment: {types: [created]}
  pull_request_review_comment: {types: [created]}
jobs:
  tag:
    runs-on: ubuntu-latest
    permissions: {contents: write, pull-requests: write, issues: write}
    steps:
    - uses: actions/checkout@v4
      with:
        fetch-depth: 0
        token: ${{ secrets.GH_TOKEN | github.token }}
    - uses: casperdcl/comment-bot@v1
      with:
        token: ${{ secrets.GH_TOKEN | github.token }}
```

Then comment on an issue or pull request with `/tag <tagname> <commit>` (e.g. `/tag v1.33.7 d34db33`).

> [!NOTE]
> The created tag will NOT trigger any `on.tag` workflow runs if using the default `github.token`. Instead, use a [personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens) to trigger `on.tag` workflow runs.
