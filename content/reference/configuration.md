---
title: Configuration
weight: 2
description: Configuration options with a field table, examples in two formats and a deprecation note.
---

The tool reads `app.yaml` from the project directory.

## Fields

| Field | Type | Required | Default | Description |
|---|---|---|---|---|
| `name` | string | yes | | Service name; lowercase letters, digits and `-` |
| `region` | string | no | `eu-west-1` | Where to deploy |
| `replicas` | integer | no | `1` | Number of instances |
| `port` | integer | no | `8080` | Port the app listens on |
| `env` | map | no | `{}` | Environment variables |

## Example

{{< tabpane text=true >}}
{{% tab header="YAML" %}}
```yaml
name: my-app
replicas: 3
env:
  LOG_LEVEL: info
```
{{% /tab %}}
{{% tab header="JSON" %}}
```json
{
  "name": "my-app",
  "replicas": 3,
  "env": { "LOG_LEVEL": "info" }
}
```
{{% /tab %}}
{{< /tabpane >}}

{{% alert title="Deprecated" color="warning" %}}
`instances` was renamed to `replicas` in 1.3. The old name still works but prints a warning
and will be removed in 2.0.
{{% /alert %}}

{{% alert title="Secrets" %}}
Do not put secrets in `env`. Reference them from your secret store instead.
{{% /alert %}}
