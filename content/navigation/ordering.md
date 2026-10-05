---
title: Ordering with Weight
weight: 1
description: Lower weight appears higher in the sidebar.
---

Pages and sections are sorted by `weight` (ascending). Items with equal or no
weight fall back to alphabetical order by title.

| Front matter | Effect |
|---|---|
| `weight: 1` | First |
| `weight: 10` | Later |
| *(none)* | After weighted items, alphabetical |

Sections are ordered the same way: **Getting Started** (`weight: 1`) comes
before **Navigation** (`weight: 2`).
