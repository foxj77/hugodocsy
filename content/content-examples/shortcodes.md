---
title: Shortcodes
weight: 1
description: Alerts, tabs and page info boxes.
---

## Alerts

{{% alert title="Note" color="primary" %}}A primary alert.{{% /alert %}}
{{% alert title="Warning" color="warning" %}}A warning alert.{{% /alert %}}
{{% alert title="Danger" color="danger" %}}A danger alert.{{% /alert %}}

## Tabs

{{< tabpane text=true >}}
{{% tab header="macOS" %}}
```bash
brew install hugo
```
{{% /tab %}}
{{% tab header="Run" %}}
```bash
npm run serve
```
{{% /tab %}}
{{< /tabpane >}}

## Page info

{{% pageinfo %}}
A highlighted box, handy for status notes such as "draft" or "beta".
{{% /pageinfo %}}
