---
name: linkedin-to-blog
description: Convert a LinkedIn post (pasted text + images saved to Downloads) into a Hugo blog post. Creates a page bundle under content/post/, finds recently downloaded images, renames and copies them correctly.
allowed-tools: Read, Write, Edit, Bash, Glob, Grep
---

# LinkedIn → Hugo Blog Post

## Workflow

The user will paste LinkedIn post content (plain text, no markdown). Images are already saved to `~/Downloads` — the user saves them by copying from LinkedIn and pasting/saving via browser or OS, so filenames are **random timestamps** (e.g. `1742668079290.png`), not descriptive names. Your job:

1. **Parse the content** — extract a suitable slug and title from the text
2. **Find images** — look for the most recently modified PNG/JPG files in `~/Downloads`. Use `ls -lt ~/Downloads/ | head -20` to find them, then use `sips` to create small thumbnails to visually identify each one. Ask the user how many images they saved if unclear.
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

LinkedIn images saved from the browser typically land in `~/Downloads` with **random timestamp filenames** like `1742668079290.png`. Do not expect descriptive names.

```bash
# Find recent PNG/JPG files
ls -lt ~/Downloads/ | head -20

# Create thumbnails to visually inspect all candidates at once
for f in ~/Downloads/1742*.png; do
  name=$(basename "$f" .png)
  sips -s format jpeg -z 100 200 "$f" --out /tmp/thumb_${name}.jpg 2>/dev/null
done

# Then Read each /tmp/thumb_*.jpg to identify what each image shows
```

Match each image to its position in the post based on visual content, then rename descriptively when copying.

## Rules

- Slug must be lowercase kebab-case, derived from the post title, Vietnamese-friendly (transliterate if needed)
- Do NOT add commentary or explanation — just create the files
- Set `draft = false` (posts are ready to publish)
- After finishing, print a short summary: post path + list of images copied
