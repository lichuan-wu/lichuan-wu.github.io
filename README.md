# lichuan-wu.github.io

Personal research website for Lichuan Wu, Associate Professor (Docent) in
Meteorology at the Department of Earth Sciences, Uppsala University. Live at
<https://lichuan-wu.github.io>.

Built with [Jekyll](https://jekyllrb.com/) on a reduced fork of the
[al-folio](https://github.com/alshedivat/al-folio) theme (via
[jsjol.github.io](https://github.com/jsjol/jsjol.github.io)). Pushing to `main`
triggers the `Deploy site` workflow, which builds the site, purges unused CSS
and publishes `_site` to the `gh-pages` branch.

## Publishing on GitHub Pages

1. Create a public repository named **`lichuan-wu.github.io`** on GitHub.
2. Push this folder to its `main` branch.
3. In the repository, open **Settings → Actions → General** and allow
   _Read and write permissions_ for workflows.
4. After the first `Deploy site` run, open **Settings → Pages** and set the
   source to _Deploy from a branch_, branch **`gh-pages`**, folder `/ (root)`.

## Local development

Requires Ruby with Bundler, and ImageMagick for the responsive image variants:

```bash
brew install imagemagick   # provides `magick`
bundle install
bundle exec jekyll serve    # http://localhost:4000
```

The build needs nothing else — no Python, no Node. A clean build takes about
five seconds and should print no warnings; treat any warning as a defect.

Before committing, format the sources:

```bash
npm install                 # first time only
npx prettier . --write
```

## Where the content lives

| What            | Where                                                |
| --------------- | ---------------------------------------------------- |
| About page      | `_pages/about.md` (photo: `assets/img/prof_pic.jpg`) |
| News items      | `_news/`                                             |
| Publications    | `_bibliography/papers.bib`                           |
| Research themes | `_projects/`                                         |
| Courses         | `_teachings/`                                        |
| Group members   | `_data/people.yml`                                   |
| Social links    | `_data/socials.yml`                                  |
| CV              | `_pages/cv.md`, PDF in `assets/pdf/cv.pdf`           |
| Link preview    | `assets/img/og-preview.png` (1200×630)               |

### Adding a news item

Create `_news/YYYY-MM-DD-slug.md` whose only front matter is its date:

```markdown
---
date: 2026-10-19
---

New paper in [Journal]: [**Title**](https://doi.org/...). Work led by [Author].
```

### Adding a publication

Append a BibTeX entry to `_bibliography/papers.bib`. Beyond the standard fields,
the templates understand `abbr`, `abstract`, `award`, `bibtex_show`, `code`,
`html`, `pdf`, `preview`, `selected`, `slides`, `supp`, `video` and `website`.
`selected={true}` puts the entry on the front page; `preview={file.png}` looks
for that file in `assets/img/publication_preview/`.

### Updating the CV

Replace `assets/pdf/cv.pdf` with the new PDF and update `_pages/cv.md`.

## Keeping the publication list current (optional)

`bin/sync_publications.py` compares a Google Scholar profile with
`_bibliography/papers.bib` and can append missing papers. It needs
`scholar_userid` in `_data/socials.yml`; once that is set, uncomment the
schedule in `.github/workflows/update-publications.yml`.

## Local changes to the theme

This fork has diverged from upstream al-folio deliberately, so updates have to
be cherry-picked rather than merged. The substantive differences:

- The blog, bookshelf, CV-from-JSON, distill, repository-trophy, comment,
  newsletter and search features are removed, along with their layouts,
  includes, Sass partials, data files, assets and CDN libraries.
- MDBootstrap is gone. It cost 277 kB of CSS and 288 kB of JS to supply four
  shadow rules, which now live in `_sass/_utilities.scss`.
- `_plugins/cache-bust.rb` replaces the `jekyll-cache-bust` gem, whose CSS
  digest hashed a directory that does not exist in this repository, so the
  `?v=` query string never changed and browsers served stale CSS.
- An empty `title:` in `_config.yml` names the site after its owner.
  Upstream requires the literal string `blank` for this and renders an empty
  `<h1>` and an empty navbar brand otherwise.
- `_pages/people.md` uses a CSS grid defined in `_sass/_people.scss` rather
  than Bootstrap row/column utilities.
