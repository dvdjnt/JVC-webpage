# devlog · Jekyll Portfolio

Static site built with Jekyll, hosted on GitHub Pages. No local build needed — push and GitHub builds it automatically.

---

## Project Structure

```
/
├── _config.yml              ← site settings (edit baseurl here)
├── _layouts/
│   ├── default.html         ← nav + footer, wraps every page
│   └── post.html            ← week update wrapper (extends default)
├── _includes/
│   ├── nav.html             ← navigation bar
│   └── footer.html          ← footer
├── _posts/                  ← ✏️ one .md file per week update
│   ├── 2025-01-13-week-1.md
│   └── 2025-01-20-week-2.md
├── assets/
│   ├── css/style.css        ← all styles + design tokens
│   └── js/nav.js            ← active nav highlight
├── index.html               ← homepage (shows latest 3 posts)
├── week-updates.html        ← full post index (auto-generated)
├── final-project.html
├── about.html
├── Gemfile                  ← Ruby dependencies (for local preview)
└── _config.yml
```

---

## GitHub Pages Setup (one-time)

1. Push this repo to GitHub
2. Go to **Settings → Pages**
3. Set source to **"Deploy from a branch"** → `main` → `/ (root)`
4. Open `_config.yml` and set:
   ```yaml
   baseurl: ""          # leave empty if using username.github.io repo
                        # set to "/repo-name" for a project repo
   url: "https://yourusername.github.io"
   ```
5. Push — GitHub builds and deploys automatically (~1 min)

> **Tip:** Name your repo `yourusername.github.io` and `baseurl` stays empty, links just work.

---

## Adding a New Week Update

This is the only thing you do repeatedly. **One file, one push.**

### Step 1 — Create the post file

Create a new file in `_posts/` following this exact naming format:

```
_posts/YYYY-MM-DD-week-N.md
```

Example: `_posts/2025-01-27-week-3.md`

### Step 2 — Write the frontmatter + content

```markdown
---
layout: post
title: "Your Title Here"
date: 2025-01-27
week: 3
read_time: "5 min"
summary: "One or two sentences shown on the card preview."
tags: [tag1, tag2, tag3]
---

Your post content here. Standard Markdown works:

## Section heading

Paragraph text...

- bullet list
- another item

\`\`\`python
# code block
print("hello")
\`\`\`
```

### Step 3 — Update the terminal block (optional)

In `index.html`, update the terminal callout to reflect current project status — check off completed tasks, move the `→` arrow to the current task, update the `next` and `blocker` lines.

### Step 4 — Push

```bash
git add .
git commit -m "week 3"
git push
```

GitHub Pages rebuilds in ~60 seconds. The new post appears automatically on the homepage (latest 3) and the full week-updates index.

---

## Local Preview (optional)

If you want to preview before pushing:

```bash
# Install Ruby + Bundler first (one-time)
gem install bundler

# Install dependencies (one-time per project)
bundle install

# Start local server
bundle exec jekyll serve

# Open http://localhost:4000
```

Changes hot-reload automatically. Stop with Ctrl+C.

---

## Updating the Terminal Block

The terminal on the homepage (`index.html`) is the only thing that needs manual updating alongside each post. Pattern:

```html
<div class="term-out"><span class="hl">✓</span>  completed task</div>
<div class="term-out"><span class="acc">→</span>  current task  <span class="dim">[in progress]</span></div>
<div class="term-out"><span class="muted">○</span>  future task</div>
```

- `hl` (green `✓`) = done
- `acc` (orange `→`) = currently working on
- `muted` (dim `○`) = not started

---

## Design Tokens

All colours and fonts in `assets/css/style.css` under `:root`. Change once, affects everything.

| Variable | Value | Role |
|---|---|---|
| `--bg` | `#111010` | Page background |
| `--fg` | `#f0ece0` | Primary text |
| `--accent` | `#e8795f` | Highlights, active states |
| `--green` | `#7abf6a` | Tags, completed items |
| `--font-display` | DM Sans | Headings + body |
| `--font-mono` | IBM Plex Mono | Labels, code, metadata |
