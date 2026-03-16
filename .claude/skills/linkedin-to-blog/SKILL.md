---
name: linkedin-to-blog
description: Convert a LinkedIn post (pasted text + images saved to Downloads) into a Hugo blog post. Creates a page bundle under content/post/, finds recently downloaded images, renames and copies them correctly.
allowed-tools: Read, Write, Edit, Bash, Glob, Grep
---

# LinkedIn → Hugo Blog Post

## Workflow

The user will paste LinkedIn post content (plain text, no markdown) and has already saved images to `~/Downloads`. Your job:

1. **Parse the content** — extract a suitable slug and title from the text
2. **Find images** — look for the most recently modified files in `~/Downloads` that are images (PNG, JPG, JPEG, WEBP). Use `ls -lt ~/Downloads/ | head -20` to find them, then use `sips` to create small thumbnails to visually identify each one
3. **Create page bundle** — `content/post/<slug>/index.md`
4. **Convert text to markdown** — format headings, bold, code, bullet lists properly. Preserve Vietnamese text exactly as-is
5. **Copy and name images** — copy each image from Downloads to the page bundle directory with a descriptive filename (kebab-case, .png extension). Use `cp` via Bash
6. **Reference images in markdown** — use `![alt text](filename.png)` with relative paths, placed at logical positions matching where they appeared in the original post

## Hugo front matter format

```toml
+++
date = 'YYYY-MM-DD'
draft = false
title = 'Post title here'
tags = ['tag1', 'tag2']
+++
```

Use today's date. Infer 3–5 relevant tags from the content.

## Image identification

```bash
# Find recent files
ls -lt ~/Downloads/ | head -20

# Check file type
file ~/Downloads/Unknown-X

# Create thumbnail to visually inspect
sips -s format jpeg -z 100 200 ~/Downloads/Unknown-X --out /tmp/thumb-X.jpg

# Then Read /tmp/thumb-X.jpg to see the image
```

## Rules

- Slug must be lowercase kebab-case, derived from the post title, Vietnamese-friendly (transliterate if needed)
- Do NOT add commentary or explanation — just create the files
- Set `draft = false` (posts are ready to publish)
- After finishing, print a short summary: post path + list of images copied
