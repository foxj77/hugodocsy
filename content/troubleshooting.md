---
title: Troubleshooting
weight: 5
description: Common errors with causes and fixes, plus collapsible FAQ entries.
---

## Common errors

| Error | Cause | Fix |
|---|---|---|
| `command not found: example-tool` | Install directory not on `PATH` | Restart the shell or add it to `PATH` |
| `invalid configuration (exit 2)` | Typo or missing required field | Run `example-tool deploy --dry-run` to see the message |
| `deployment timed out (exit 3)` | Health check failing | Check `example-tool logs <name>` |

## FAQ

<details>
<summary>Can I deploy to more than one region?</summary>

Not in a single config file. Create one project per region and pass `--region`.

</details>

<details>
<summary>How do I see debug output?</summary>

Add `-v` to any command, for example `example-tool deploy -v`.

</details>

<details>
<summary>Where are logs stored?</summary>

Logs are kept for 7 days. Stream them with `example-tool logs <name>`.

</details>

## Still stuck?

{{% pageinfo %}}
Open an issue and include the output of `example-tool version` and `example-tool deploy -v`.
{{% /pageinfo %}}
