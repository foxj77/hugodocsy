---
title: Deploy an App
weight: 1
description: A numbered tutorial with checkpoints, code and expected output.
---

**Goal:** deploy a sample web app and reach it in your browser.
**Time:** about 10 minutes. **You need:** the tool from
[Installation]({{< relref "/getting-started/installation" >}}).

## 1. Create a project

```bash
example-tool init my-app
cd my-app
```

This creates:

```text
my-app/
├── app.yaml
└── src/
    └── main.py
```

## 2. Review the configuration

Open `app.yaml`. The highlighted lines are the ones you will usually change:

```yaml {hl_lines=[2,4]}
name: my-app
region: eu-west-1
replicas: 2
port: 8080
```

## 3. Deploy

```bash
example-tool deploy
```

Expected output:

```console
Building image...      done
Pushing image...       done
Creating service...    done
Available at https://my-app.example.com
```

{{% alert title="Checkpoint" color="success" %}}
Open the URL printed above. You should see **Hello, world**.
{{% /alert %}}

## 4. Clean up

```bash
example-tool destroy my-app
```

{{% alert title="This is destructive" color="danger" %}}
`destroy` deletes the service and its data. It asks for confirmation unless you pass `--yes`.
{{% /alert %}}
