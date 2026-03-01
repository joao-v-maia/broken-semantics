# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Hugo static site blog called "Broken Semantics" (joaomaia.dev) using the hugo-theme-stack theme. The site is configured for English content with Portuguese-Brazilian locale fallback, featuring Disqus comments and a personal blog aesthetic.

## Essential Commands

### Development
- `hugo server` or `hugo server -D` - Start local development server (add -D to include draft posts)
- `hugo` - Build the site to the `public/` directory

### Theme Management
The theme is managed as a git submodule. If the `themes/hugo-theme-stack/` directory is empty:
- `git submodule update --init --recursive` - Initialize and fetch the theme submodule

### Content Creation
- `hugo new posts/<post-name>.md` - Create a new blog post using the archetype template
- New posts are created with `draft = true` by default; set to `false` to publish

## Updating Hugo and Theme

### Update Hugo
On macOS with Homebrew:
```bash
brew update
brew upgrade hugo
```

For other systems, download the latest version from https://github.com/gohugoio/hugo/releases

### Update Theme (hugo-theme-stack)
The theme is a git submodule pointing to https://github.com/CaiJimmy/hugo-theme-stack/

```bash
# Update to the latest commit on the default branch
git submodule update --remote themes/hugo-theme-stack

# Review changes
cd themes/hugo-theme-stack
git log --oneline -10
cd ../..

# Test the site locally
hugo server -D

# Commit the submodule update
git add themes/hugo-theme-stack
git commit -m "chore: update hugo-theme-stack to latest version"
```

**To pin to a specific theme version:**
```bash
cd themes/hugo-theme-stack
git fetch
git checkout v4.0.0  # Replace with desired version tag
cd ../..
git add themes/hugo-theme-stack
git commit -m "chore: pin hugo-theme-stack to v4.0.0"
```

**Important:** Always test the site after updating the theme, as theme updates may introduce breaking changes to configuration or layout.

## Architecture

### Configuration Structure
Hugo configuration is split across multiple files in `config/_default/`:
- `config.toml` - Base configuration (baseURL, language, pagination, Disqus)
- `params.toml` - Theme-specific parameters (widgets, sidebar, comments, date formats)
- `menu.toml` - Main navigation and social media links
- `languages.toml` - Multilingual support configuration
- `markup.toml` - Markdown rendering settings
- `permalinks.toml` - URL structure configuration
- `related.toml` - Related content configuration

The root `hugo.toml` contains basic site metadata that may duplicate some settings in `config/_default/config.toml`.

### Content Organization
- `content/posts/` - Blog posts (markdown files with front matter)
- `archetypes/default.md` - Template for new content with title, date, and draft status
- `static/images/` - Static images (including avatar.jpg)
- `assets/images/` - Images processed by Hugo pipelines

### Build Artifacts
- `public/` - Generated static site (should be deployed to web server)
- `resources/` - Hugo's processing cache for images and assets
- `.hugo_build.lock` - Hugo build lock file

### Theme Customization
The Stack theme is in `themes/hugo-theme-stack/` as a git submodule. Theme customization is done through configuration files rather than modifying the theme directly.

## Key Configuration Details

- **Base URL**: https://joaomaia.dev/
- **Main sections**: Posts (shown on homepage and archive)
- **Comments**: Disqus enabled with shortname "broken-semantics"
- **Sidebar**: Includes avatar, emoji (🍥), and custom subtitle
- **Widgets**: Search, archives (5 items), categories (10 items), tag cloud (10 items)
- **RSS**: Full content in feed
- **Color scheme**: Toggle enabled, defaults to auto-detect
