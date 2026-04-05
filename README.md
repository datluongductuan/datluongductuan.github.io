# Dat Luong Blog

Personal blog built with [Hugo](https://gohugo.io/) and the [Paper](https://github.com/nanxiaobei/hugo-paper) theme. Deployed to GitHub Pages via GitHub Actions.

Live at: https://datluongductuan.github.io/

## Prerequisites

- [Hugo](https://gohugo.io/installation/) (extended edition)

## Setup

```bash
git clone --recurse-submodules git@github.com:datluongductuan/datluong-blog.git
cd datluong-blog
```

If you already cloned without `--recurse-submodules`:

```bash
git submodule update --init --recursive
```

## Local Development

```bash
# Start dev server with draft posts visible
hugo server -D
```

Open http://localhost:1313 to preview.

## Writing a New Post

```bash
# Create a new post (page bundle)
mkdir content/post/my-post-slug
touch content/post/my-post-slug/index.md
```

Add front matter to `index.md`:

```toml
+++
date = '2026-01-01'
draft = true
title = 'My Post Title'
tags = ['tag1', 'tag2']
+++

Your content here...
```

Place images in the same folder and reference them with `![alt](filename.png)`.

Set `draft = false` when the post is ready to publish.

## Publishing

1. Set `draft = false` in your post's front matter
2. Commit and push to `main`:
   ```bash
   git add content/post/my-post-slug/
   git commit -m "Add new post: my post title"
   git push origin main
   ```
3. GitHub Actions automatically builds and deploys to https://datluongductuan.github.io/

You can monitor the deploy status in the [Actions tab](https://github.com/datluongductuan/datluong-blog/actions).

## Project Structure

```
content/post/       # Blog posts (page bundles with index.md + images)
themes/paper/       # Paper theme (git submodule, do not edit)
hugo.toml           # Site configuration
archetypes/         # Templates for new content
.github/workflows/  # GitHub Actions deploy pipeline
```
