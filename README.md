# borisrapoport.com

Personal site. Hugo static build, deployed to GitHub Pages on push to `main`.

## Local development

    hugo server

Serves at http://localhost:1313.

## Content

- `content/_index.md` — homepage metadata
- `content/about/_index.md` — about page body
- `content/projects/*.md` — one file per project
- `config.toml` — site config

## Deploy

Push to `main`. `.github/workflows/deploy.yml` builds the site and publishes `docs/` to GitHub Pages.

## Theme

Custom theme in `themes/main/`. Layouts under `layouts/`, styles in `static/css/quantum-ascent.css`.

## License

See LICENSE.
