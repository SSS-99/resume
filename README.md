# Resume

https://sss-99.github.io/resume/

A Jekyll site published with GitHub Pages ("Deploy from a branch", `main` / root).

## Editing

All content lives in [`_data/data.yml`](_data/data.yml):

- `sidebar` — name, tagline, contact links, languages, interests
- `experiences` — `company`, `time`, and its projects (`name`, `scale`, `role`, `stack`)
- `skills` — skill groups; an item with its own `items` list expands on the web and shows only its name in the PDF

### Japanese version (`/ja/`)

[`_data/data_ja.yml`](_data/data_ja.yml) holds only the translated text — company names, project names, `scale`, `role`, sidebar text and skill group headings — keyed by the `id` fields in `data.yml`. Tech stacks and skill items are shared, and anything missing falls back to English. UI labels (section titles, "Team", "Role", …) are in [`_data/labels.yml`](_data/labels.yml).

When adding a project, give it an `id` in `data.yml` and add the same key under `projects:` in `data_ja.yml`.

Push to `main` and GitHub Pages rebuilds the site.

## PDF

[`.github/workflows/resume-pdf.yml`](.github/workflows/resume-pdf.yml) runs on pushes to `main` that touch the rendered page (`_data/`, `_includes/`, `_layouts/`, `_sass/`, `assets/css/`, `index.html`, `ja/`, `_config.yml`): it builds the site, prints it with headless Chrome, and commits the results to `assets/resume.pdf` and `assets/resume-ja.pdf`. Run `git pull` before your next edit to pick up that commit.

Print styles are in the `@media print` block of [`_sass/_resume.scss`](_sass/_resume.scss).

## Local preview

```sh
bundle install
bundle exec jekyll serve
# http://localhost:4000/resume/
```

Or with Docker:

```sh
docker run --rm -it -p 4000:4000 -v "$PWD":/srv -w /srv ruby:3.3 \
  sh -c 'bundle install && bundle exec jekyll serve --host 0.0.0.0'
```

## Layout

| Path | Purpose |
|---|---|
| `_layouts/default.html` | Page skeleton |
| `_includes/header.html` | Name, tagline, contact links |
| `_includes/experiences.html` | Experience section |
| `_includes/sidebar.html`, `_includes/skills.html` | Skills, languages, interests |
| `_sass/_resume.scss` | All styles, including print |

Originally based on the [online-cv](https://github.com/sharu725/online-cv) Jekyll theme; the design has since been rewritten.
