# cloudflare-build-log

Get your Cloudflare Build Logs in PRs.

Put this in your `.github/workflows/action.yml`

```yaml
name: Fetch Deployment Logs

on:
  pull_request:
    types: [opened, synchronize]

jobs:
  fetch-logs:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Poll for Cloudflare Pages Build and Fetch Logs
        uses: JDeepD/cloudflare-build-log@0.1.5
        with:
          CLOUDFLARE_API_TOKEN: ${{ secrets.CLOUDFLARE_API_TOKEN }}
          ACCOUNT_ID: ${{ secrets.CLOUDFLARE_ACCOUNT_ID }}
          PROJECT_NAME: ${{ secrets.CLOUDFLARE_PROJECT_NAME }}
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          COMMIT_SHA: ${{ github.event.pull_request.head.sha }}
```

You need to put the following secrets in your repository:

| SECRET NAME             | SECRET VALUE                                                                                                                                                                                                    |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| CLOUDFLARE_PROJECT_NAME | Your Cloudflare Project Name. Go to Cloudflare Dashboard > Workers and Pages > Overview.                                                                                                                        |
| CLOUDFLARE_API_TOKEN    | [Generate a Cloudflare API Token](https://dash.cloudflare.com/profile/api-tokens) (not API Key) if not generated already with Read Permissions on Pages. Make sure to set the expiration of the token properly. |
| CLOUDFLARE_ACCOUNT_ID   | You will find your Account ID on the Right Panel in Cloudflare Dashboard > Workers and Pages > Overview.                                                                                                        |
