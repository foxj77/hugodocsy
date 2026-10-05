# Hugo + Docsy example

A minimal working docs site showing how **Hugo** and the **Docsy** theme fit together.

## Run it locally

```bash
brew install hugo      # one-off; must be the "extended" build (brew's is)
npm install            # one-off; installs Docsy's front-end deps
npm run serve          # then open http://localhost:1313/
```

The docs are served from `/` (no splash page). Edit any file under `content/` and the browser reloads automatically.
Production build: `npm run build` (output in `public/`).

Requires Hugo >= 0.160.1 (extended), Go (Hugo uses it to fetch modules) and Node.

## How the pieces fit

| Piece | Role | Where |
|---|---|---|
| Hugo | Static site generator: turns Markdown in `content/` into HTML | `hugo` binary |
| Docsy | A Hugo *theme*: layouts, SCSS, shortcodes (`blocks/cover`, `alert`...) | Go module `github.com/google/docsy/theme`, pinned in `go.mod` |
| Hugo Modules | How Hugo downloads Docsy (no git submodule, no `themes/` dir) | `[[module.imports]]` in `hugo.toml` |
| npm packages | Docsy's Bootstrap + Font Awesome assets (Docsy mounts them from `node_modules`) and Dart Sass | `package.json` |

Flow: `hugo.toml` imports the Docsy module -> Hugo overlays Docsy's `layouts/`, `assets/`
etc. underneath this project's own folders (project files win) -> Hugo compiles Docsy's SCSS
via `sass --embedded` -> pages in `content/` render using Docsy's layouts.

## Layout

- `hugo.toml` - site config, menu, Docsy module import
- `content/_index.md` - site root; `type: docs` makes it the docs landing page (no splash page)
- `content/<section>/_index.md` - a folder with an `_index.md` is a section (a sidebar group); other `.md` files are pages. `weight` orders them, `linkTitle` shortens the sidebar label, `description` feeds the section's child list
- Sample sections: `getting-started/`, `navigation/` (ordering, titles, nested sections up to 4 levels), `content-examples/` (shortcodes, formatting), `reference/api/v1/` (deep nesting)
- `cascade: type: docs` in `content/_index.md` applies the docs layout to every page. Without it, pages outside a folder named `docs/` render blank
- No blog section; to add one back, create `content/blog/_index.md` and a `[[menu.main]]` entry
- `layouts/`, `assets/`, `static/` - empty; put files here to override Docsy's (same path wins)

## Gotchas hit while building this

- Docsy >= 0.16 publishes the theme as `github.com/google/docsy/theme` (not `github.com/google/docsy`, which has no layouts).
- Hugo shells out to `sass --embedded`. The npm scripts put `node_modules/.bin` (from `sass-embedded`) on `PATH`; running bare `hugo server` fails with a SCSS error unless Dart Sass is on your PATH another way.
- Content lives directly in `content/`, not `content/en/`: with Hugo 0.167 `content/en/` made every URL `/en/...`.
- `markup.goldmark.renderer.unsafe = true` is required by Docsy shortcodes that emit HTML.
