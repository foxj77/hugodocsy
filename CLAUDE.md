# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

Example Hugo site using the Docsy theme, as a Hugo Module. See `README.md` for the full explanation.

## Commands

- `npm install` - once, installs Docsy's front-end deps (bootstrap, fontawesome, sass-embedded)
- `npm run serve` - dev server at http://localhost:1313/ with live reload
- `npm run build` - production build to `public/`
- Always use the npm scripts, not bare `hugo`: they put `node_modules/.bin` on `PATH` so Hugo can find `sass --embedded`.
- Requires brew-installed `hugo` (extended, >= 0.160.1), plus Go and Node. No test/lint suite.

## Architecture

- Docsy is not vendored: `hugo.toml` `[[module.imports]]` pulls `github.com/google/docsy/theme` (pinned in `go.mod`). The theme path is `/theme`, not the repo root. Update with `hugo mod get -u github.com/google/docsy/theme`.
- Docsy mounts Bootstrap and Font Awesome from the *project's* `node_modules`, so they must stay in `package.json`.
- Project `layouts/`, `assets/`, `static/` override same-path Docsy files.
- The docs are the site root: `content/_index.md` has `type: docs`, so there is no splash page or blog. Add pages as folders under `content/`. `cascade: type: docs` in `content/_index.md` is required: without it pages outside a `docs/` folder render with no content area.
- Sample content under `content/` demonstrates sidebar behaviour (weight ordering, `linkTitle`, nested sections, shortcodes). Keep it in sync with the README layout list.
- Use `{{< relref "/path" >}}` for internal links (there is no `ref` shortcode).
- Content is in `content/` directly (not `content/en/`; that forces `/en/` URLs on Hugo 0.167). Sidebar order comes from `weight` front matter.
- Keep top-level keys in `hugo.toml` above any `[table]`, or TOML scopes them into the table.
- `markup.goldmark.renderer.unsafe = true` is needed for Docsy shortcodes.
- After removing/moving content, `rm -rf public resources` and restart the server: stale `public/` output keeps serving deleted pages.
