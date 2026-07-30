# How to update your GitHub repo

Repo: `lee-kyungho/lee-kyungho.github.io` (branch `main`)

You have two options. **Option A (web browser)** needs no tools installed.
**Option B (git)** is faster if you already have the repo cloned.

---

## Option A — GitHub website, no install

Do this once per file. There are 8 files.

### A1. Replace an existing file

1. Go to `https://github.com/lee-kyungho/lee-kyungho.github.io`
2. Click the file you want to change (e.g. `index.md`).
3. Click the **pencil icon** (top right of the file view) — "Edit this file".
4. Select all the existing text (`Ctrl/Cmd + A`) and delete it.
5. Open my version of the same file from the zip, copy all of it, paste it in.
6. Scroll down, click **Commit changes**.

Files to replace this way:

| File in zip | Where it goes in the repo |
| --- | --- |
| `index.md` | `index.md` |
| `Research.md` | `Research.md` |
| `Teaching.md` | `Teaching.md` |
| `_data/theme.yml` | `_data/theme.yml` |
| `_layouts/default.html` | `_layouts/default.html` |
| `assets/css/custom.css` | `assets/css/custom.css` |

### A2. Add the two new files

1. On the repo home page click **Add file → Create new file**.
2. In the filename box type the full path exactly: `_layouts/landing.html`
   (typing the `/` creates the folder automatically — it already exists here, that's fine).
3. Paste the contents of `_layouts/landing.html` from the zip.
4. Click **Commit changes**.
5. Repeat for `_layouts/page-plain.html`.

### A3. Delete the About page

1. Open `about.md` in the repo.
2. Click the **trash icon** (top right of the file view).
3. Click **Commit changes**.

Its content now lives on the home page, so nothing is lost.

### A4. Wait for the rebuild

Go to the **Actions** tab. A "pages build and deployment" job runs for about
30–60 seconds. When it shows a green check, reload
`https://lee-kyungho.github.io` — hard-refresh with `Ctrl/Cmd + Shift + R`
so you don't see the cached old CSS.

---

## Option B — git on your computer

```bash
cd path/to/lee-kyungho.github.io

# optional but recommended: work on a branch first
git checkout -b redesign

# unzip my files somewhere, then copy them in
# (adjust ~/Downloads/github-changes to wherever you unzipped)
cp ~/Downloads/github-changes/index.md .
cp ~/Downloads/github-changes/Research.md .
cp ~/Downloads/github-changes/Teaching.md .
cp ~/Downloads/github-changes/_data/theme.yml _data/theme.yml
cp ~/Downloads/github-changes/_layouts/default.html _layouts/default.html
cp ~/Downloads/github-changes/_layouts/landing.html _layouts/landing.html
cp ~/Downloads/github-changes/_layouts/page-plain.html _layouts/page-plain.html
cp ~/Downloads/github-changes/assets/css/custom.css assets/css/custom.css

# remove the old About page
git rm about.md

git add -A
git commit -m "Redesign: horizontal nav, new home page, merge About into Home"
git push -u origin redesign
```

Then open the pull request GitHub offers you, and merge it when you're happy.
To skip the branch and publish immediately, use `git checkout main` at the start
and `git push` at the end instead.

---

## Previewing locally before you push (optional)

```bash
bundle install
bundle exec jekyll serve
```

Then open `http://localhost:4000`.

---

## If something looks wrong

- **Old design still showing** — hard-refresh (`Ctrl/Cmd + Shift + R`). GitHub
  Pages also caches CSS for a few minutes.
- **Page is unstyled / plain text** — `assets/css/custom.css` didn't get copied,
  or was pasted into the wrong path.
- **Research or Teaching 404s** — `_layouts/page-plain.html` is missing, or the
  `permalink:` line at the top of `Research.md` / `Teaching.md` got dropped.
- **Home page is blank** — `_layouts/landing.html` is missing.
- **Build failed** in the Actions tab — click the red X to read the error. It is
  almost always a YAML problem in `_data/theme.yml`: check the indentation
  matches my file exactly (spaces, never tabs).

To undo everything: `git revert` the commit, or in the web UI open the repo's
commit history and revert the commit there.

---

## What these changes do

- Sticky horizontal nav (Home / Research / Teaching) replaces the hamburger sidebar.
- Home page rebuilt: PhD-candidate eyebrow, large sans name with an inline
  **View CV** box, job-market line, Primary/Secondary fields, featured-in
  sentence, and your real headshot.
- About page merged into Home and removed from navigation.
- Type: Source Serif 4 headings + Public Sans body and name.
- Colour: authentic Yale blue `#00356b` (~11:1 contrast on the warm background).
- Accessibility: skip link, focus rings sitewide, `aria-current` on the active
  nav item, 44px+ tap targets, print styles.
- Research and Teaching pages restyled; all existing entries kept, including
  Work in Progress and PySDTest.
