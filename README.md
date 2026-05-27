# Portfolio site (Quarto)

A multi-page Quarto website that publishes to GitHub Pages from the `docs/` folder.

## Files
```
_quarto.yml              site config (theme, navbar, output -> docs/)
index.qmd                landing page
projects.qmd             auto-generated grid of project cards
school_proficiency.qmd   your report (replace the stub with real content)
styles.css               light custom styling
.nojekyll                tells GitHub Pages NOT to run Jekyll (required for Quarto)
docs/                    BUILD OUTPUT — created by `quarto render`, this is what's served
```

## One-time setup

1. **Edit `_quarto.yml`** — replace `YOURUSERNAME` in the GitHub link, adjust title/footer.
2. **Edit `index.qmd`** — your bio, email, GitHub link.
3. **Replace `school_proficiency.qmd`** — paste your real report body under the YAML
   frontmatter (keep the frontmatter so it appears as a project card).

## Build locally

```bash
quarto render          # builds the whole site into docs/
quarto preview         # live preview in browser while editing
```

`quarto render` executes the code chunks, so run it where your data/models live
(it needs torch, your trained model files, df_clean, etc. to reproduce the plots).

**Tip:** if you don't want the public site to re-run heavy code every build, freeze it:
add this to `_quarto.yml` and the chunks run once, then cache:
```yaml
execute:
  freeze: auto
```

## Deploy to GitHub Pages

1. Create a repo (e.g. `yourusername.github.io` for a root site, or any name for a
   project site at `yourusername.github.io/reponame`).
2. Push everything **including the `docs/` folder and `.nojekyll`**:
   ```bash
   git init
   git add .
   git commit -m "portfolio site"
   git branch -M main
   git remote add origin https://github.com/YOURUSERNAME/REPO.git
   git push -u origin main
   ```
3. On GitHub: **Settings → Pages → Source: Deploy from a branch → Branch: `main`,
   Folder: `/docs`** → Save.
4. Wait ~1 minute. Site goes live at the URL shown on that Pages settings page.

## Adding future projects
1. Write a new `myproject.qmd` with the same YAML frontmatter style (title,
   description, date, categories).
2. Add it to the `contents:` list in `projects.qmd`.
3. `quarto render`, commit, push. The card appears automatically.

## Common gotchas
- **Blank / unstyled page on GitHub Pages** → the `.nojekyll` file is missing. It must
  be present (Quarto puts one in `docs/` automatically on render, but keep the root one too).
- **Pages serves an old version** → make sure Settings → Pages points at `/docs`, and
  that you committed the freshly rendered `docs/` folder.
- **Interactive Plotly plots don't show** → they work in website mode automatically;
  just don't set `embed-resources: true` in multi-page site config (it's for single files).
