<!--
title: Configuration
space: YOUR_SPACE_KEY
parent_id: PARENT_PAGE_ID
-->

# Configuration

This document describes all configuration options available for the Confluence integration using the mark tool.

## Configuration File

The mark tool uses a `.mark.conf` file in the project root. Copy `.mark.conf.example` to `.mark.conf` and configure it:

```ini
[default]
base_url = https://your-confluence-instance.atlassian.net
username = your-email@example.com
password = your-api-token
space = YOUR_SPACE_KEY
parent_id = PARENT_PAGE_ID
```

### Configuration Options

- `base_url`: Your Confluence instance URL (e.g., `https://your-domain.atlassian.net`)
- `username`: Your Confluence username (usually your email)
- `password`: Your Confluence API token (not your password)
- `space`: The Confluence space key where pages will be created
- `parent_id`: (Optional) The ID of the parent page under which new pages will be created

### Getting Your API Token

1. Go to your Atlassian account settings
2. Navigate to Security → API tokens
3. Create a new API token
4. Use this token in the `password` field of `.mark.conf`

## Options

### Space Configuration

Specify the target Confluence space for your documentation.

### Page Hierarchy

Configure how pages are organized in Confluence.

## Related Documentation

- [Getting Started](./getting-started.md) - Initial setup
- [Troubleshooting](./troubleshooting.md) - Configuration issues

