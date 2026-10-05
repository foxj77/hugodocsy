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
- Sample sections: `getting-started/` (incl. tabbed install guide), `tutorials/` (numbered walkthrough), `navigation/` (ordering, titles, nesting to 4 levels), `content-examples/` (shortcodes, formatting, Mermaid diagrams), `reference/` (CLI and config tables, `api/v1/` deep nesting), plus top-level `troubleshooting.md` (FAQ with collapsible `<details>`) and `changelog.md`
- `cascade: type: docs` in `content/_index.md` applies the docs layout to every page. Without it, pages outside a folder named `docs/` render blank
- No blog section; to add one back, create `content/blog/_index.md` and a `[[menu.main]]` entry
- `layouts/_partials/sidebar-args.html` - one-line override of Docsy's partial so the sidebar shows the whole tree (upstream limits it to the current top-level folder). Re-diff against the theme's copy when upgrading Docsy
- `assets/`, `static/` - empty; put files here to override Docsy's (same path wins)

## Gotchas hit while building this

- Docsy >= 0.16 publishes the theme as `github.com/google/docsy/theme` (not `github.com/google/docsy`, which has no layouts).
- Hugo shells out to `sass --embedded`. The npm scripts put `node_modules/.bin` (from `sass-embedded`) on `PATH`; running bare `hugo server` fails with a SCSS error unless Dart Sass is on your PATH another way.
- Content lives directly in `content/`, not `content/en/`: with Hugo 0.167 `content/en/` made every URL `/en/...`.
- `markup.goldmark.renderer.unsafe = true` is required by Docsy shortcodes that emit HTML.

## Publishing (GitHub Pages)

`.github/workflows/pages.yml` builds the site with Hugo on every push to `main` and deploys
it to GitHub Pages: https://foxj77.github.io/hugodocsy/. The workflow overrides `baseURL`
with the Pages URL, so `hugo.toml` keeps `http://localhost:1313/` for local development.
Pages source is set to "GitHub Actions" (repo Settings > Pages). The Hugo version is pinned
by `HUGO_VERSION` in the workflow. For a custom domain, add it in Settings > Pages and a
DNS `CNAME` to `foxj77.github.io`.

### Sidebar options (`[params.ui]` in `hugo.toml`)

- `sidebar_menu_compact = false` (current): show siblings of the current section, not only its children
- `sidebar_menu_foldable = true` (current): arrows to expand/collapse sections
- `ul_show = 1` (current): levels expanded by default; raise it to open more of the tree
- `sidebar_menu_compact = true`: Docsy's compact mode, showing only the current section's branch
