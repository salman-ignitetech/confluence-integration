# GitHub Actions Setup Guide

This guide explains how to configure GitHub Actions to automatically sync your markdown documentation to Confluence using [mark](https://github.com/kovetskiy/mark).

## Required GitHub Secrets

Configure these secrets in your repository settings:

1. Go to **Settings** → **Secrets and variables** → **Actions**
2. Click **New repository secret** for each of the following:

### Required Secrets

- **`CONFLUENCE_BASE_URL`**

  - Your Confluence instance URL
  - Example: `https://your-domain.atlassian.net`
  - For Confluence Cloud, include `/wiki` suffix: `https://your-domain.atlassian.net/wiki`
  - Do not include trailing slash

- **`CONFLUENCE_USERNAME`**

  - Your Confluence username (usually your email address)
  - Example: `user@example.com`

- **`CONFLUENCE_API_TOKEN`**

  - Your Confluence API token
  - Generate at: [Atlassian Account](https://id.atlassian.com/manage-profile/security/api-tokens) → Security → API tokens
  - **Important:** Use API token, not your password

## How It Works

1. **Trigger:** The workflow runs automatically when:

   - Code is pushed to the `main` branch
   - Any `.md` file is changed
   - The workflow file itself is updated

2. **Process:**

   - Installs the `mark` tool from GitHub releases
   - Sets environment variables (`MARK_USERNAME`, `MARK_PASSWORD`, `MARK_BASE_URL`) from GitHub secrets
   - Syncs `README.md` to Confluence
   - Syncs all files in `docs/` folder to Confluence

3. **Metadata:** Each markdown file must have metadata headers:
   ```markdown
   <!-- Space: YOUR_SPACE_KEY -->
   <!-- Title: Page Title -->
   ```

   Optional - to nest under a parent page (uses page **title**, not ID):
   ```markdown
   <!-- Space: YOUR_SPACE_KEY -->
   <!-- Parent: Parent Page Title -->
   <!-- Title: Page Title -->
   ```

## Testing

1. Make a small change to any `.md` file
2. Commit and push to `main` branch
3. Check the **Actions** tab in GitHub to see the workflow run
4. Verify pages appear in your Confluence space

## Troubleshooting

- **Workflow fails at install:** Check if the mark release URL has changed
- **Authentication errors:** Double-check your API token is valid and username is correct
- **Pages not appearing:** Verify you have write permissions to the target space
- **Wrong space:** Check the `space:` value in each markdown file's metadata header
