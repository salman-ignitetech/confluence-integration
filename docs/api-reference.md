<!--
title: API Reference
space: YOUR_SPACE_KEY
parent_id: PARENT_PAGE_ID
-->

# API Reference

This document provides detailed information about the API endpoints and methods.

## Authentication

All API requests require authentication using your Confluence credentials.

## Endpoints

### Sync Document

Sync a markdown document to Confluence.

**Method:** `POST /sync`

**Parameters:**
- `file`: Path to the markdown file
- `space`: Confluence space key
- `title`: Page title in Confluence

### Get Status

Check the sync status of a document.

**Method:** `GET /status`

## Examples

### Basic Sync

Run mark from the project root to sync all configured markdown files:

```bash
mark
```

The tool will read metadata from each markdown file and sync them to Confluence based on the configuration in `.mark.conf`.

## Related Documentation

- [Configuration](./configuration.md) - Configure API settings
- [Troubleshooting](./troubleshooting.md) - Common API issues

