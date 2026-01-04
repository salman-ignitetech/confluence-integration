# GitHub Actions Setup Guide

This guide explains how to configure GitHub Actions to automatically sync your markdown documentation to Confluence.

## Required GitHub Secrets

Configure these secrets in your repository settings:

1. Go to **Settings** → **Secrets and variables** → **Actions**
2. Click **New repository secret** for each of the following:

### Required Secrets

- **`CONFLUENCE_BASE_URL`**

  - Your Confluence instance URL
  - Example: `https://your-domain.atlassian.net`
  - Do not include trailing slash

- **`CONFLUENCE_USERNAME`**

  - Your Confluence username (usually your email address)
  - Example: `user@example.com`

- **`CONFLUENCE_API_TOKEN`**

  - Your Confluence API token
  - Generate at: Atlassian Account → Security → API tokens
  - **Important:** Use API token, not your password

- **`CONFLUENCE_SPACE`**
  - The Confluence space key where pages will be created
  - Example: `MYSPACE`

### Optional Secrets

- **`CONFLUENCE_PARENT_ID`**
  - The ID of the parent page under which new pages will be created
  - Leave empty if you want pages at the root of the space
  - To find a page ID: View page in Confluence, check the URL: `.../pages/viewpage.action?pageId=123456789`

## How It Works

1. **Trigger:** The workflow runs automatically when:

   - Code is pushed to the `main` branch
   - Any `.md` file is changed
   - The workflow file itself is updated

2. **Process:**

   - Installs the `mark` tool
   - Creates configuration from GitHub secrets
   - Syncs `README.md` to Confluence
   - Syncs all files in `docs/` folder to Confluence

3. **Metadata:** Each markdown file should have metadata headers:
   ```markdown
   <!--
   title: Page Title
   space: YOUR_SPACE_KEY
   parent_id: PARENT_PAGE_ID
   -->
   ```

## Testing

1. Make a small change to any `.md` file
2. Commit and push to `main` branch
3. Check the **Actions** tab in GitHub to see the workflow run
4. Verify pages appear in your Confluence space

## Troubleshooting

- **Workflow fails:** Check the Actions logs for error messages
- **Pages not appearing:** Verify secrets are correct and you have write permissions
- **Authentication errors:** Double-check your API token is valid
- **Wrong space:** Verify `CONFLUENCE_SPACE` secret matches your target space key
