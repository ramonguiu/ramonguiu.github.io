# ramonguiu.com

Personal site. Plain Jekyll on GitHub Pages: one layout, one stylesheet, no theme, no JS.

## Where things live

| What | File |
|---|---|
| Home page copy | `index.html` |
| Resume | `_data/experience.yml`, `_data/education.yml` (rendered by `resume.html`) |
| Products / work (data only; page not built yet) | `_data/work.yml` |
| Talks | `_data/talks.yml` |
| Writing hosted elsewhere | `_data/writing_external.yml` |
| Writing hosted here | `_posts/YYYY-MM-DD-slug.md` |
| Styles | `assets/css/site.css` |
| LLM summary (hand-written, update when the home page changes) | `llms.txt` |
| LLM full profile (generated from `_data/` and posts) | `llms-full.txt` |
| Structured data for search engines and LLMs | `_includes/person-jsonld.html` |
| Crawler rules | `robots.txt` |

## Republishing a recovered post

Create `_posts/YYYY-MM-DD-slug.md`, using the **original** publication date:

```markdown
---
title: From Waterfall to Agile: A Product Manager Transition
publication: Name of the blog it first appeared in
original_url: https://original.example.com/post      # optional, dead link is fine
archive_url: https://web.archive.org/web/2016.../...  # optional
---

Post body in Markdown...
```

When `publication` is set, the post shows "originally published in X" plus a note linking to the archived copy.
Put images in `assets/images/writing/`.

## Local preview

Needs Ruby 3.x (macOS system Ruby is too old): `brew install ruby@3.3`.

```sh
export PATH="/opt/homebrew/opt/ruby@3.3/bin:$PATH"
bundle config set --local path vendor/bundle
bundle install
bundle exec jekyll serve
```

Then open http://localhost:4000. Pushing to `gh-pages` deploys.

## Drafts

`_unpublished/` is a local-only folder for drafts. It's in `.gitignore` (never committed) and
Jekyll skips folders starting with `_`, so nothing in it is published.
