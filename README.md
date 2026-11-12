# papers-dashboard

A personal library of the papers, books, courses and articles I've saved, served by GitHub Pages.

This repo is a public **shell with no data**: one static `index.html` with all HTML, CSS
and JS inline and no build step. The papers live in a separate **private** repo. The page
loads them in your browser through the GitHub REST API, using a fine-grained token that
you paste once and that is stored only in that browser's `localStorage`. Visitors without
a token see only the "connect your repo" screen.

- No third-party scripts, analytics or CDNs (only Google Fonts CSS). A Content-Security-Policy limits network access to `api.github.com`.
- All paper data is rendered as text, never as HTML, and only `http(s)` links are made clickable.

## Setup

1. Set up the private data repo first (data file, scripts, workflow and full instructions live there: `papers/README.md`).
2. **Settings → Pages**: Deploy from a branch, `main`, folder `/ (root)`.
3. Open `https://<user>.github.io/papers-dashboard/`, enter owner, repo and a fine-grained token (only the `papers` repo; **Contents: read/write**, **Actions: read/write**; with an expiry date), then **Save & test**.

## Features

- A type filter (All · Papers · Books · Courses · Articles) that scopes everything below it. Courses use Not started / In progress / Done.
- Stats: total, unread, read (with the number in progress), added this month.
- "Added per month" chart (last 24 months or all time). Click a bar to filter to that month.
- Search across titles, authors, abstracts, tags and notes (press `/` to focus it).
- Filter by status, starred and tags. Sort by date added, publication date or title.
- History grouped by the month each paper was saved.
- Per paper: change status, star, open the PDF, copy BibTeX, edit tags, note and metadata, remove.
- **Add paper** (with a Type field) dispatches the `add-paper.yml` workflow in the data repo and shows its progress.
- Bookmarklet (`?add=<url>` opens the Add dialog with the link filled in), a curl snippet, and export as JSON or BibTeX in Settings.
- Works on phones (one column, floating Add button) and follows the system's dark mode.

## Local preview

```bash
python3 -m http.server 8000
```

Then open http://localhost:8000. The page talks to the real GitHub API, so a token is
needed to see data.
