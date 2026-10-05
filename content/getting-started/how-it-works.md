---
title: How It Works
weight: 1
description: The flow from Markdown file to rendered page.
---

1. `hugo.toml` imports the Docsy module.
2. Hugo layers Docsy's `layouts/` and `assets/` under this project's own.
3. Each Markdown file in `content/` is rendered with a layout chosen by its
   `type` (here `docs`, set once with `cascade` in `content/_index.md`).
4. The sidebar is built from the section tree, sorted by `weight`, then title.

Because `weight: 1` here is lower than `first-page.md`'s `weight: 2`, this page
is listed first even though its filename sorts later alphabetically.
