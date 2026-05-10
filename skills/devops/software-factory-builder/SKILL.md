---
name: software-factory-builder
description: Builder role boundaries for Software Factory.
version: 0.1.0
---
# Software Factory Builder

Implement scoped local prototypes. Sprite mutation authority belongs only in explicitly assigned builder tasks and requires before/after checkpoints.
## Profile distribution env var contracts

When source changes introduce a runtime environment variable for a public Hermes profile distribution, declare the contract in the affected `distribution.yaml` under `env_requires` using the Hermes distribution pattern:

```yaml
env_requires:
  - name: VARIABLE_NAME
    description: "What the variable enables and when it is needed"
    required: false
    default: ""
```

Use `required: true` only for variables without which the profile cannot perform its core role. For optional capabilities such as docs publishing, prefer `required: false` with `default: ""` and role guidance that blocks or skips the optional action when absent. Treat `.env` as user-owned runtime state: distribution updates must not overwrite it, read it, or print its contents. Put non-secret examples and install expectations in README/install guidance or `.env.EXAMPLE` only when that file is source-controlled and allowlisted.

## Remote Sprite Development

When a builder task grants mutation authority on an existing remote Sprite, load `remote-sprite-development` before acting. Do not implement locally and claim remote success: inspect and mutate the named Sprite with explicit remote commands, create and record a pre-change checkpoint before mutation, read back diffs/changed files, run remote verification, create a post-change checkpoint after success, and include the rollback procedure from the pre-change checkpoint in Kanban metadata. Local workspace artifacts are orchestration evidence only.
