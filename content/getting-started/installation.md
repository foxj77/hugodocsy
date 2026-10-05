---
title: Installation
weight: 3
description: Install the example tool on each platform, with tabbed per-OS instructions.
---

This page shows the **install guide** pattern: prerequisites, tabbed
per-platform steps, then a verification step.

## Prerequisites

- A 64-bit machine with 2 GB of free disk space
- Network access to your package registry
- Admin rights (Linux and Windows only)

## Install

{{< tabpane text=true >}}
{{% tab header="macOS" %}}
```bash
brew install example-tool
```
{{% /tab %}}
{{% tab header="Linux" %}}
```bash
curl -fsSL https://example.com/install.sh | sudo sh
```
{{% /tab %}}
{{% tab header="Windows" %}}
```powershell
winget install Example.Tool
```
{{% /tab %}}
{{< /tabpane >}}

## Verify

```console
$ example-tool version
example-tool 1.4.0 (build 2026-09-28)
```

{{% alert title="Not working?" color="warning" %}}
See [Troubleshooting]({{< relref "/troubleshooting" >}}) for common install errors.
{{% /alert %}}

## Next steps

{{< cardpane >}}
{{% card header="Tutorial" %}}
Deploy a sample app end to end: [Deploy an app]({{< relref "/tutorials/deploy-an-app" >}}).
{{% /card %}}
{{% card header="Reference" %}}
Look up every command in the [CLI reference]({{< relref "/reference/cli" >}}).
{{% /card %}}
{{< /cardpane >}}
