# navy-site

Plain, fast, Quarto-based personal site. Three sections — Research,
Writing, Projects — plus a Home page and an About page. No database, no
admin panel: everything is a text file.

## 1. One-time setup

1. Install Quarto: https://quarto.org/docs/get-started/ (just the CLI,
   you don't need RStudio or VS Code, though either works fine as an
   editor).
2. From this folder, preview the site locally:

   ```
   quarto preview
   ```

   This opens a live-reloading browser preview. Leave it running while
   you write — every time you save a `.qmd` file, the browser updates.

### If preview won't start (Windows + VS Code)

1. **Open the right folder.** In VS Code use *File → Open Folder* and pick
   the folder that directly contains `_quarto.yml`. If you unzipped into
   Downloads you may have `navy-site\navy-site\`. Open the inner one, or
   better, move it somewhere simple like `C:\Users\HP\Documents\navy-site`.
2. **Check Quarto is visible to VS Code.** Open the terminal in VS Code
   (Ctrl + `) and run `quarto --version`. If it says "not recognized",
   quit VS Code completely and reopen it (it only reads PATH at startup).
   Still failing? Reinstall Quarto from quarto.org.
3. **Clear the cache.** Close any running preview, then delete the hidden
   `.quarto` folder in the project (it's safe; Quarto rebuilds it). A
   crashed preview can leave a lock file there that blocks the next one.
4. **Run it from the terminal**, not the play button:

   ```
   quarto preview
   ```

   If the port is busy, use `quarto preview --port 4321`.
5. Don't open `docs/index.html` by double-clicking it. Search and some
   links don't work from `file://`. Always look at the site through
   `quarto preview`.

## 2. Adding a new piece of work (research / writing / projects)

Each section is just a folder (`research/`, `writing/`, `projects/`) full
of `.qmd` files. The section's `index.qmd` auto-lists everything in that
folder, newest first — you never touch the listing yourself.

To add something new:

1. Copy any existing `.qmd` file in that folder as a starting template.
2. Change the frontmatter at the top:

   ```yaml
   ---
   title: "Your Title Here"
   subtitle: "One line, optional"
   date: 2026-08-09          # controls sort order — use today's date
   ---
   ```

3. Write the content below the frontmatter in normal Markdown. Use
   `$...$` for inline math and `$$...$$` for display math (LaTeX syntax,
   rendered automatically). Tables are plain Markdown tables.
4. Save. It appears on the section's index page and the homepage's
   "Recently added" list automatically — nothing else to configure.

To mark something as still in progress, add this near the top of the
body (already used on a couple of pages as an example):

```
::: {.status}
status: in progress
:::
```

## 3. Editing the navbar, colors, or fonts

- Navbar links, footer, and the outbound "Art" link: edit
  `_quarto.yml`.
- Colors, fonts, spacing: edit `styles.css` — the color/font choices are
  all defined as CSS variables near the top of the file, so you can
  change the whole palette by editing a handful of lines.

## 4. Building and publishing

The plan is two GitHub repositories on the same account, so both sites
share one address:

| Repo | What's in it | Live at |
|---|---|---|
| `NavyBlueCheese.github.io` | this Quarto site | https://navybluecheese.github.io/ |
| `art` | the hand-coded art site | https://navybluecheese.github.io/art/ |

**Main site, once:**

1. Create a public repo named exactly `NavyBlueCheese.github.io`.
2. Push this folder to it (including `docs/`).
3. Repo Settings → Pages → Source: *Deploy from a branch*, branch `main`,
   folder `/docs`.

**Art site, once:**

1. Create a public repo named `art` and push the art folder to it.
2. Settings → Pages → branch `main`, folder `/ (root)`.

**Every time you change the main site:** run `quarto render`, then commit
and push. Pages updates within a minute or two.

**Custom domain later:** add it under Settings → Pages on the
`NavyBlueCheese.github.io` repo. The art repo then appears at
`yourdomain.com/art/` by itself. Update `site-url` in `_quarto.yml` and
the two art links (navbar and `about.qmd`) to the new domain.

## 5. Structure

```
navy-site/
├── _quarto.yml          site config: navbar, footer, theme
├── styles.css            all colors/fonts/layout
├── index.qmd              homepage
├── about.qmd              about + the link out to the art site
├── favicon.svg
├── research/
│   ├── index.qmd          auto-listing, don't edit by hand
│   ├── fx-vol-surface.qmd
│   └── cip-em-deviations.qmd
├── writing/
│   ├── index.qmd
│   └── senate-ballot-matching.qmd
└── projects/
    ├── index.qmd
    ├── fx-vrp.qmd
    ├── tsmom-band.qmd
    ├── pairs-trading-backtest.qmd
    ├── g10-fx-analysis.qmd
    └── figures/           images used on project pages
```
