<!-- Space: ENG -->
<!-- Parent: 675545098 -->
<!-- Title: AI Usage Dashboard Confluence Integration Test -->

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

4. Configure each markdown file's metadata header:
   - Set `space:` to your Confluence space key
   - Set `parent_id:` to the parent page ID (optional - see [PARENT_ID_GUIDE.md](./PARENT_ID_GUIDE.md) for how to get it)
   - Each file can have different space and parent_id values

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
3. Add the following secrets (credentials only):
   - `CONFLUENCE_BASE_URL` - Your Confluence instance URL (e.g., `https://your-domain.atlassian.net`)
   - `CONFLUENCE_USERNAME` - Your Confluence username (email)
   - `CONFLUENCE_API_TOKEN` - Your Confluence API token

**Configure Markdown Files:**

Each markdown file must have its metadata header configured manually:

- `space:` - Your Confluence space key
- `parent_id:` - (Optional) Parent page ID - see [PARENT_ID_GUIDE.md](./PARENT_ID_GUIDE.md) for instructions

**How it works:**

- The workflow triggers automatically on push to `main` branch
- Only runs when markdown files (`.md`) are changed
- Installs the `mark` tool in the GitHub Actions runner
- Creates `.mark.conf` with credentials from GitHub secrets
- Syncs `README.md` and all files in the `docs/` folder to Confluence
- Each file uses its own metadata header for space and parent_id configuration

**View workflow runs:**

Check the **Actions** tab in your GitHub repository to see sync status and logs.

## Project Structure

```
.
├── README.md                              # This file (root documentation)
├── PARENT_ID_GUIDE.md                     # Guide on how to get parent IDs
├── .mark.conf.example                     # Example configuration file
├── .mark.conf                             # Your actual config (create from example)
├── .github/
│   └── workflows/
│       └── sync-to-confluence.yml         # GitHub Actions workflow
└── docs/                                  # Sub-pages documentation
    ├── getting-started.md
    ├── api-reference.md
    ├── configuration.md
    └── troubleshooting.md
```
