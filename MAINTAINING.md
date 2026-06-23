# Maintaining the district-magnitude website

This guide is for current and future officers who need to update the website. It
assumes **no prior web-development experience** — just follow the steps in order.

- **Live site:** https://district-magnitude.github.io/
- **Code repository:** https://github.com/district-magnitude/district-magnitude.github.io

---

## 1. How the website works (the 30-second version)

The site is built with [**Quarto**](https://quarto.org), a tool that turns simple
text files into web pages.

- You **edit plain-text files** ending in `.qmd` (e.g. `events.qmd`). These hold the
  content — you write in [Markdown](https://quarto.org/docs/authoring/markdown-basics.html),
  which is just text with light formatting.
- When you **save your changes to GitHub**, a robot (a "GitHub Action") automatically
  rebuilds the site and publishes it. **You do not need to build or upload anything by hand.**

There are two important branches in the repository:

| Branch | What it holds | Do you touch it? |
|-----------|------------------------------------------------|---------------------------------|
| `main` | The source files you edit (`.qmd`, config) | **Yes** — this is your workspace |
| `gh-pages` | The finished web pages (auto-generated) | **No** — never edit by hand |

---

## 2. One-time setup

You only do this once on your computer.

1. **Install Git** — https://git-scm.com/downloads
2. **Install Quarto** — https://quarto.org/docs/get-started/ (lets you preview changes)
3. *(Recommended)* Install a text editor such as
   [VS Code](https://code.visualstudio.com/) or [RStudio](https://posit.co/download/rstudio-desktop/).
4. **Get access:** ask a current officer to add your GitHub account to the
   `district-magnitude` organization so you can save changes.
5. **Download (clone) the repository** — open a terminal and run:

   ```bash
   git clone https://github.com/district-magnitude/district-magnitude.github.io.git
   cd district-magnitude.github.io
   ```

You now have a copy of the website on your computer.

---

## 3. The everyday workflow

Every time you want to make a change, follow these four steps:

### Step 1 — Get the latest version

Before editing, pull down anyone else's recent changes:

```bash
git pull
```

### Step 2 — Make your edits

Edit the `.qmd` files (see the [common tasks](#4-common-tasks) below).

### Step 3 — Preview locally (optional but recommended)

See your changes in a web browser **before** publishing:

```bash
quarto preview
```

This opens the site on your own computer and refreshes as you edit. Press `Ctrl+C`
in the terminal to stop it.

### Step 4 — Publish

Save and upload your changes. The site rebuilds automatically:

```bash
git add -A
git commit -m "Short description of what you changed"
git push
```

Wait 1–2 minutes, then refresh https://district-magnitude.github.io/. You can watch
the build progress under the **Actions** tab on GitHub:
https://github.com/district-magnitude/district-magnitude.github.io/actions
(a green ✓ means it published successfully).

---

## 4. Common tasks

### Edit text on an existing page

Each tab on the site is one file:

| Tab on the site | File to edit |
|-----------------|----------------|
| Home | `index.qmd` |
| Events | `events.qmd` |
| People | `people.qmd` |
| Resources | `resources.qmd` |
| Connect | `connect.qmd` |

Open the file, change the text, save, and follow [Step 4 — Publish](#step-4--publish).

**Markdown quick reference:**

```markdown
## A section heading
### A smaller heading

**bold text**  and  *italic text*

- a bullet point
- another bullet

1. a numbered item
2. another item

[Link text](https://example.com)
```

More formatting: https://quarto.org/docs/authoring/markdown-basics.html

### Add new materials (PDFs, images, slides, etc.)

1. Create a folder for files if it doesn't exist — a common choice is `files/`
   (for documents) and `images/` (for pictures).
2. Put your file there, e.g. `files/2026-report.pdf`.
3. Link to it from a page (e.g. in `resources.qmd`):

   ```markdown
   [Download the 2026 report](files/2026-report.pdf)
   ```

   To show an image:

   ```markdown
   ![A caption for the image](images/photo.jpg)
   ```

4. Publish (Step 4). The files upload automatically with your changes.

### Add a brand-new page and tab

1. **Create the page.** Make a new `.qmd` file, e.g. `news.qmd`, starting with a title:

   ```markdown
   ---
   title: "News"
   ---

   Your content goes here.
   ```

2. **Add it to the navigation bar.** Open `_quarto.yml` and add an entry under
   `navbar: > left:` (keep the indentation exactly as shown):

   ```yaml
       - href: news.qmd
         text: News
   ```

3. Publish (Step 4). The new tab appears automatically.

### Remove a page from the menu

Delete (or comment out) its entry in `_quarto.yml` under `navbar:`. You can leave the
`.qmd` file in place or delete it.

---

## 5. Changing the look (advanced)

- **Colors, fonts, logo:** edit `_brand.yml` (if present) and `styles.css`.
- **Site title, theme, table of contents:** edit `_quarto.yml`.
- The theme is `cosmo` from [Bootswatch](https://bootswatch.com/) — you can swap it for
  another theme name in `_quarto.yml`.

Make small changes, preview with `quarto preview`, and publish when happy.

---

## 6. Troubleshooting

**My change isn't showing up on the live site.**
- Did you run `git push`? Changes only publish after pushing.
- Check the **Actions** tab for a red ✗ (a failed build). Click it to read the error.
- Try a hard refresh in your browser (`Ctrl+Shift+R`) — the old page may be cached.

**The build failed (red ✗ in Actions).**
- Usually a typo in `_quarto.yml`. Indentation matters in YAML — use spaces, not tabs,
  and match the existing layout exactly.
- Run `quarto render` on your computer to see the same error locally.

**"Permission denied" when I push.**
- Your GitHub account may not be in the `district-magnitude` organization yet, or you
  need to sign in to GitHub. Ask a current officer for access.

**I broke something and want to undo my local edits (before pushing).**

```bash
git restore .
```

This discards un-pushed changes and returns files to the last saved version.

---

## 7. Who to ask

If you get stuck, contact the list owner at
[district-magnitude+owner@groups.io](mailto:district-magnitude+owner@groups.io) or a
current officer. When asking for help, copy the exact error message — it makes problems
much faster to solve.
