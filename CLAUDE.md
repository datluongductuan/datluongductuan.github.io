# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a personal blog for Dat Luong built with [Hugo](https://gohugo.io/) using the [Paper theme](https://github.com/nanxiaobei/hugo-paper) as a git submodule.

## Commands

```bash
# Start local dev server with drafts enabled
hugo server -D

# Build the site
hugo

# Create a new post
hugo new content/post/my-post-title.md
```

## Configuration

- `hugo.toml` — site-level config: base URL, title, theme, Disqus comments, social links, avatar, and color scheme (`linen`, `wheat`, `gray`, or `light`)
- `themes/paper/` — the Paper theme, tracked as a git submodule (do not edit directly)
- `archetypes/default.md` — template used when creating new content via `hugo new`

## Content

Posts live in `content/post/`. New posts are created as drafts (`draft = true`) and require `-D` flag to preview locally or setting `draft = false` to publish.

## Theme Customization

To override theme assets without modifying the submodule, place files in the root `assets/` or `layouts/` directories — Hugo's lookup order prioritizes the site root over the theme.
