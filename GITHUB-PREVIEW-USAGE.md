# GitHub HTML Preview Utility - Usage Guide

## Overview

The GitHub HTML Preview utility (`github-preview.html`) is a tool that allows you to preview HTML files stored in GitHub repositories. It fetches raw HTML content from GitHub and renders it in a sandboxed iframe.

## How It Works

1. Takes a GitHub file URL (e.g., `https://github.com/user/repo/blob/main/file.html`)
2. Converts it to a raw GitHub URL (`https://raw.githubusercontent.com/user/repo/main/file.html`)
3. Fetches the HTML content via CORS
4. Renders it in a sandboxed iframe with `allow-scripts`, `allow-same-origin`, and `allow-forms` permissions

## Two Modes of Operation

### Interactive Mode

Access the tool directly:
```
https://michaelbanfield.github.io/electricity-usage-viewer/github-preview.html
```

Users can:
- Paste any GitHub HTML file URL
- Click "Load Preview" or press Enter
- View the rendered HTML with a header showing the source URL

### URL Parameter Mode (Full-Screen)

Access with a URL parameter for automatic, full-screen preview:
```
https://michaelbanfield.github.io/electricity-usage-viewer/github-preview.html?url=GITHUB_URL
```

**Important:** The GitHub URL must be URL-encoded if it contains special characters.

Example:
```
https://michaelbanfield.github.io/electricity-usage-viewer/github-preview.html?url=https://github.com/user/repo/blob/main/index.html
```

When using URL parameter mode:
- The page automatically loads in full-screen
- The input section and header are hidden
- Only the preview header and iframe are visible
- The preview takes up the entire viewport
- Perfect for embedding or sharing direct links to previews

## Using This Tool for Your HTML Utilities

### Scenario: You're developing an HTML utility in a GitHub repo

**Step 1:** Push your HTML file to a GitHub repository

**Step 2:** Get the GitHub URL to your file
```
https://github.com/your-username/your-repo/blob/main/your-utility.html
```

**Step 3:** Create a preview link using the GitHub Preview utility
```
https://michaelbanfield.github.io/electricity-usage-viewer/github-preview.html?url=https://github.com/your-username/your-repo/blob/main/your-utility.html
```

**Step 4:** Share the preview link
- The preview link will render your HTML file in full-screen
- Users see your utility without any wrapper UI
- Perfect for testing, sharing, or embedding

### URL Encoding

If your GitHub URL contains special characters, URL-encode it:

JavaScript:
```javascript
const githubUrl = 'https://github.com/user/repo/blob/main/file.html';
const previewUrl = `https://michaelbanfield.github.io/electricity-usage-viewer/github-preview.html?url=${encodeURIComponent(githubUrl)}`;
```

Command line:
```bash
# Use an online URL encoder or this Python one-liner:
python3 -c "import urllib.parse; print(urllib.parse.quote('YOUR_GITHUB_URL'))"
```

## Benefits for Development Workflow

1. **No GitHub Pages Setup Required**: Preview any HTML file from any branch without enabling GitHub Pages
2. **Cross-Repository**: Preview HTML files from any public GitHub repository
3. **Branch Flexibility**: Test different branches by changing the branch name in the URL
4. **Instant Updates**: Changes to your HTML file in GitHub are immediately visible (after cache clears)
5. **Shareable**: Send preview links to others for testing or review
6. **Full-Screen Mode**: URL parameter mode provides distraction-free viewing

## Example Use Cases

### Testing a feature branch
```
# Your HTML file
https://github.com/user/repo/blob/feature-branch/index.html

# Preview link
https://michaelbanfield.github.io/electricity-usage-viewer/github-preview.html?url=https://github.com/user/repo/blob/feature-branch/index.html
```

### Sharing a quick prototype
```
# Quick prototype in a public repo
https://github.com/user/experiments/blob/main/calculator.html

# Send this link to colleagues
https://michaelbanfield.github.io/electricity-usage-viewer/github-preview.html?url=https://github.com/user/experiments/blob/main/calculator.html
```

### Comparing versions
Open multiple tabs with different branches:
- Tab 1: `?url=...blob/main/app.html`
- Tab 2: `?url=...blob/feature-a/app.html`
- Tab 3: `?url=...blob/feature-b/app.html`

## Limitations

- Only works with **public** GitHub repositories
- HTML file must be on GitHub (not local files)
- Subject to CORS policies
- External resources in your HTML (CSS, JS, images) must either:
  - Be inline in the HTML
  - Use absolute URLs
  - Be hosted on CORS-enabled servers
  - Also be in the same GitHub repo (relative paths work)

## Security

The iframe uses sandbox attributes:
- `allow-scripts`: JavaScript can run
- `allow-same-origin`: Same-origin requests work
- `allow-forms`: Forms can be submitted

This provides a safe preview environment while allowing interactive HTML utilities to function.

## Tips for Claude (AI Assistant)

When a user asks to preview or share an HTML utility:

1. **Check if the file is in a GitHub repo** - If yes, create a preview link
2. **Use URL parameter mode** - Add `?url=` parameter for full-screen preview
3. **Encode the URL** - Remember to URL-encode the GitHub URL
4. **Construct the full preview URL** - Format: `https://michaelbanfield.github.io/electricity-usage-viewer/github-preview.html?url=ENCODED_GITHUB_URL`
5. **Suggest both modes** - Interactive mode for general use, URL parameter mode for sharing

Example response:
```
Here's your preview link:
https://michaelbanfield.github.io/electricity-usage-viewer/github-preview.html?url=https%3A%2F%2Fgithub.com%2Fuser%2Frepo%2Fblob%2Fmain%2Ffile.html

You can also use the interactive mode:
https://michaelbanfield.github.io/electricity-usage-viewer/github-preview.html
```
