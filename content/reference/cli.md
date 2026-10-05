---
title: CLI Reference
weight: 1
description: Command, flag and exit-code tables, the typical shape of a reference page.
---

## Commands

| Command | Purpose |
|---|---|
| `init <name>` | Create a new project |
| `deploy` | Build and deploy the current project |
| `status` | Show the state of deployed services |
| `logs <name>` | Stream service logs |
| `destroy <name>` | Delete a service |

## Global flags

| Flag | Default | Description |
|---|---|---|
| `--config <file>` | `app.yaml` | Path to the configuration file |
| `--region <id>` | from config | Override the target region |
| `--yes` | `false` | Skip confirmation prompts |
| `-v, --verbose` | `false` | Print debug output |

## `deploy`

```text
example-tool deploy [--dry-run] [--wait <duration>]
```

`--dry-run`
: Show what would change without applying it.

`--wait <duration>`
: Block until the service is healthy, up to the given time (for example `5m`).

## Exit codes

| Code | Meaning |
|---|---|
| 0 | Success |
| 1 | General error |
| 2 | Invalid configuration |
| 3 | Deployment timed out |
