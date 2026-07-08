# 202422.github.io

Personal website & portfolio of **COMPAORE Yolemba Harold Judicaël** — Junior GenAI Developer @ Syntax Morocco.

🔗 **Live site:** https://202422.github.io

---

## 🧰 Tech Stack

| Layer      | Tool                                                        |
| ---------- | ----------------------------------------------------------- |
| Generator  | [Hugo](https://gohugo.io/) (extended) — static site builder |
| Theme      | [Congo](https://github.com/jpanther/congo) (git submodule)  |
| Styling    | Tailwind CSS (bundled with the theme)                       |
| Hosting    | [GitHub Pages](https://pages.github.com/) + Fastly CDN      |
| Deployment | GitHub Actions (`.github/workflows/deploy.yml`)             |

---

## 📁 Project Structure

```
my-site/
├── config/_default/        # Site configuration
│   ├── hugo.toml           #   core settings, baseURL, theme
│   ├── languages.en.toml   #   title, author, bio, social links
│   ├── params.toml         #   theme options (homepage layout, footer, appearance switcher)
│   └── menus.en.toml        #   header navigation menu
├── content/                # Site content (Markdown)
│   ├── _index.md           #   homepage
│   ├── blogs/              #   blog posts (one folder per post)
│   └── resume/             #   resume page
├── layouts/                # Template overrides
│   └── _partials/home/profile.html   # custom homepage heading
├── assets/img/             # Images (e.g. author.jpg profile photo)
├── themes/congo/           # Congo theme (git submodule — do not edit directly)
├── .github/workflows/      # CI/CD: build & deploy to GitHub Pages
└── hugo build output → public/  (git-ignored, generated)
```

---

## 🚀 Local Development

**Prerequisites:** [Hugo extended](https://gohugo.io/installation/) and Git.

```bash
# Clone with the theme submodule
git clone --recurse-submodules https://github.com/202422/202422.github.io.git
cd 202422.github.io

# Start the dev server
hugo server
```

Open **http://localhost:1313**. The server live-reloads on file changes. Stop with `Ctrl+C`.

> ⚠️ Always preview via `hugo server`, not by opening files in `public/` directly —
> the asset paths only resolve correctly when served over HTTP.

If styling looks stale, clear the cache and restart:

```bash
rm -rf public resources && hugo server
```

---

## ✍️ Adding a Blog Post

Each post is a **page bundle** (its own folder with an `index.md`):

```bash
mkdir -p content/blogs/my-new-post
```

Create `content/blogs/my-new-post/index.md`:

```markdown
---
title: "My New Post"
date: 2026-07-08
draft: false
tags: ["genai", "tutorial"]
summary: "A one-line description shown in listings."
---

Your content here in **Markdown**.

![diagram](diagram.png)   <!-- images go in the same folder -->
```

Set `draft: false` to publish. Images placed in the post folder are referenced by filename.

---

## 🎨 Customization Cheatsheet

| Change                         | File                                  |
| ------------------------------ | ------------------------------------- |
| Site title / description       | `config/_default/languages.en.toml`   |
| Author name, bio, social links | `config/_default/languages.en.toml`   |
| Homepage heading (greeting)    | `config/_default/params.toml` → `homepage.heading` |
| Header menu items              | `config/_default/menus.en.toml`       |
| Dark/light toggle, footer      | `config/_default/params.toml`         |
| Profile photo                  | `assets/img/author.jpg`               |

---

## 🌐 Deployment

Deployment is **fully automated**. On every push to `main`:

1. GitHub Actions installs Hugo and checks out the theme submodule.
2. Builds the site with `hugo --minify`.
3. Publishes the output to GitHub Pages (served via Fastly CDN).

```bash
git add -A
git commit -m "Describe your change"
git push
```

The site is live at https://202422.github.io within ~1 minute.
Track builds under the repo's **Actions** tab. Pages source must be set to
**GitHub Actions** (Settings → Pages → Source).
