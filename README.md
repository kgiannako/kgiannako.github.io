# kgiannako.github.io

Personal site of Konstantinos Giannakopoulos: projects, writing and CV. Built with Jekyll and published by the standard GitHub Pages build on every push to `master`.

## Layout

| Path | What it is |
|---|---|
| `index.html` | Home page |
| `_projects/` | Project write-ups, served at `/projects/<file-name>/` |
| `_posts/` | Blog articles, served at `/writing/<slug>/` |
| `_drafts/` | Unpublished articles (includes a template) |
| `cv.md` | CV page |
| `projects.html`, `writing.html`, `tags.html` | Listing pages |
| `_layouts/`, `_includes/site/` | Page templates |
| `assets/css/site.css` | All styling (colours and fonts are tokens at the top) |

## Writing an article

Copy `_drafts/example-post.md` to `_posts/YYYY-MM-DD-slug.md`, edit it, and push.

## Adding a project

Add `_projects/<slug>.md` with `title`, `date`, `description`, `group` (one of `project_groups` in `_config.yml`) and `tags`. Add `featured: <n>` and `image:` to show it as a card on the home page.

## Running locally

With Docker (no Ruby install needed):

```bash
docker run --rm -it -p 4000:4000 -v "$PWD:/src" -w /src ruby:3.3 bash -c "bundle install && bundle exec jekyll serve --host 0.0.0.0"
```

Then open http://localhost:4000.
