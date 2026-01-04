<!--
title: Confluence Integration Test
space: YOUR_SPACE_KEY
parent_id: PARENT_PAGE_ID
-->

# Confluence Integration Test

This project tests syncing README markdown files to Confluence using mark.

## Overview

This repository contains documentation that will be synced to Confluence. The main documentation is organized in the `docs/` folder.

## Documentation Pages

- [Getting Started](./docs/getting-started.md) - Introduction and setup guide
- [API Reference](./docs/api-reference.md) - API documentation and examples
- [Configuration](./docs/configuration.md) - Configuration options and settings
- [Troubleshooting](./docs/troubleshooting.md) - Common issues and solutions

## Quick Start

### Installation

1. Install the `mark` tool from [GitHub](https://github.com/kovetskiy/mark)
2. Run the setup script to create the configuration file:
   ```bash
   ./setup.sh
   ```
   Or manually copy `.mark.conf.example` to `.mark.conf`:
   ```bash
   cp .mark.conf.example .mark.conf
   ```
3. Edit `.mark.conf` with your:
   - Confluence base URL
   - Username (email)
   - API token (password field)
   - Space key
   - Parent page ID (optional)
4. Update the metadata headers in each markdown file (replace `YOUR_SPACE_KEY` and `PARENT_PAGE_ID` with your values)

### Syncing to Confluence

#### Manual Sync

Run the following command to sync all markdown files:

```bash
mark
```

This will read the configuration and metadata from each markdown file, then sync them to Confluence.

#### Automatic Sync with GitHub Actions

This repository includes a GitHub Actions workflow that automatically syncs documentation to Confluence whenever changes are pushed to the `main` branch.

**Setup GitHub Secrets:**

1. Go to your repository on GitHub
2. Navigate to **Settings** → **Secrets and variables** → **Actions**
3. Add the following secrets:
   - `CONFLUENCE_BASE_URL` - Your Confluence instance URL (e.g., `https://your-domain.atlassian.net`)
   - `CONFLUENCE_USERNAME` - Your Confluence username (email)
   - `CONFLUENCE_API_TOKEN` - Your Confluence API token
   - `CONFLUENCE_SPACE` - Your Confluence space key
   - `CONFLUENCE_PARENT_ID` - (Optional) Parent page ID

**How it works:**

- The workflow triggers automatically on push to `main` branch
- Only runs when markdown files (`.md`) are changed
- Installs the `mark` tool in the GitHub Actions runner
- Syncs `README.md` and all files in the `docs/` folder to Confluence
- Uses the metadata headers in each markdown file for page configuration

**View workflow runs:**

Check the **Actions** tab in your GitHub repository to see sync status and logs.

## Project Structure

```
.
├── README.md                              # This file (root documentation)
├── .mark.conf.example                     # Example configuration file
├── .mark.conf                             # Your actual config (create from example)
├── .gitignore                             # Git ignore file
├── setup.sh                               # Setup script
├── .github/
│   └── workflows/
│       └── sync-to-confluence.yml         # GitHub Actions workflow
└── docs/                                  # Sub-pages documentation
    ├── getting-started.md
    ├── api-reference.md
    ├── configuration.md
    └── troubleshooting.md
```
