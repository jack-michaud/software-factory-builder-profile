# softwarefactorybuilder profile

This is a local-installable role distribution root for current Hermes. It is generated/maintained from the Software Factory profiles monorepo prototype.

Install locally for testing:

```bash
hermes profile install /path/to/software-factory-profiles/profiles/builder --name softwarefactorybuilder-monorepo-test --yes
```

Role boundary: Performs approved local implementation and, in separate explicitly scoped tasks, owns sprite mutations with checkpoint discipline.

## Generated public repository shape

This root is current-Hermes-compatible: `distribution.yaml` is at repository root.

Install after publication:

```bash
hermes profile install https://github.com/jack-michaud/software-factory-builder-profile.git --name softwarefactorybuilder
```

Update after publication:

```bash
hermes profile update softwarefactorybuilder --yes
```

Public/private boundary: credentials, runtime state, logs, memories, sessions, Kanban DB/workspaces, sprite credentials, SSH keys, OAuth tokens, API keys, and private Obsidian notes are not included.

## Runtime configuration

This distribution owns `config.yaml`. The file pins model execution to `gpt-5.5` via provider `openai-codex` using `chat_completions`, enables the public-safe `hermes-cli` toolset, and points `skills.external_dirs` at `../../skills` so controlled installs can reuse shared skill overlays without vendoring private/local skill trees.

Authority for the `softwarefactorybuilder` role is governed by `SOUL.md` plus the role-specific bootstrap skill. This parity wave does not add a `role-capability-manifest.yaml` because the corresponding meta profile also uses SOUL as its authority source; publisher/docs remain the manifest-backed profiles.

## Publication provenance

Version: v0.1.0
Source of truth: https://github.com/jack-michaud/software-factory
Source tag: profiles/v0.1.0
Source commit: 63035a90746ab304b7e8c5f231d9d89c2106e9d8
Generated manifest: GENERATED_METADATA.json
License: MPL-2.0

This repository is generated. File issues and feature requests on https://github.com/jack-michaud/software-factory rather than editing this generated repository directly.
## Env var contract maintenance

When builders add optional profile capabilities that depend on environment variables, update `distribution.yaml` with `env_requires` and document non-secret examples in README/install guidance. `.env` remains user-owned runtime state and must not be overwritten by distribution installs or updates.
