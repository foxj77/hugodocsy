---
title: Getting Started
weight: 1
description: What Hugo and Docsy are and how this example is wired together.
---

This section lives in `content/getting-started/_index.md`. A section's
`_index.md` is its landing page; the list of child pages below is generated
automatically by Docsy from each child's `description`.

Hugo is the static site generator. Docsy is a Hugo *theme* that supplies the
layouts, styling and shortcodes. This repo pulls Docsy in as a **Hugo Module**
(see `go.mod` and `[[module.imports]]` in `hugo.toml`).
