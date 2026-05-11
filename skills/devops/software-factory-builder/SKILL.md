---
name: software-factory-builder
description: Builder role boundaries for Software Factory.
version: 0.1.2
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

## Disposable/test-profile install and cleanup workflow

Only perform disposable/test-profile installation or pruning in a separate, explicitly scoped Kanban task. Source-update tasks may encode the workflow, but must not mutate production profiles, install runtime profiles, run sprite/fly/pi-sprite commands, push public repos, or edit local-only profile state.

When a PM-required disposable validation chain reaches a builder install/cleanup task:

1. Confirm the reviewed source candidate and affected profile list from parent handoffs.
2. Use a random suffix in each disposable profile name so it cannot collide with production or meta profiles.
3. Install from the reviewed source distribution root with the canonical Hermes profile install flow supplied by the task/source. Verify the root `distribution.yaml` and profile loadability with non-secret output.
4. If the expected Hermes wrapper is broken or the command shape is unclear, use the approved Hermes venv executable when supplied by the task/handoff; otherwise block with the exact non-secret failure and required unblock condition. Do not guess alternate destructive commands.
5. Capture evidence as public-safe task artifacts or handoff metadata only: changed files, commit hashes, profile names, command exit status, and paths to approved validation artifacts. Never copy `.env`, `auth.json`, logs, sessions, memories, Kanban DBs, credentials, or raw profile state.
6. Allow at most two remediation iterations for the same blocker family. After that, block or route to orchestrator/human with evidence.
7. After publication/rollout/docs evidence is preserved, prune disposable profiles with canonical Hermes profile delete and verify absence using non-secret profile-list output unless a human explicitly requests retention.

Performance guardrail: do not request or perform disposable validation for low-risk docs/comment-only edits, typo fixes, or reviewer-static-sufficient work unless PM/human explicitly requires it.

Reusable precedent language: disposable-profile install evidence should verify the source distribution root, including `distribution.yaml` when relevant; wrapper fallback is acceptable when the expected local Hermes wrapper is broken, but evidence should name the approved fallback executable without exposing private profile state; preserve approved non-secret validation artifacts before cleanup; prune disposable profiles with canonical Hermes profile delete only after rollout/docs evidence is preserved.

## Source-update Git Flow

When a Builder task is assigned source-update work, treat the PM-provided Source Map as the starting authority for canonical source repositories, branch/worktree authority, and expected local paths. Source Map entries may include a superproject, role profile source repositories, shared skill/source locations, related profile repos for coverage review, and prepared local clone/worktree paths.

Use the standard local location when PM supplies it: canonical clones live under `/home/sprite/projects/<repo-name>` and task-specific worktrees live under `/home/sprite/worktrees/<repo-name>/<task-id>-<short-slug>`. Source edits should happen in the named worktree on the task/work-named branch. Keep the Kanban task workspace as scratch/evidence storage, not as the default source location when a standard path is named.

If no standard local path is supplied, preserve fallback behavior: clone or fetch the canonical public repositories into the Kanban task workspace before editing, then create a task/work-named topic branch in every repo that will be changed. Edit source-controlled files only. Installed runtime/profile directories such as `~/.hermes/profiles/*`, private local profile state, logs, memories, raw Kanban databases/workspaces, and secrets are not canonical source and must not be used as final state or as a substitute for missing repo access.

Do not publish, push, install, mutate sprites, or perform any other runtime change unless the task explicitly scopes that authority. If a Source Map entry, repo coordinate, access path, branch/worktree authority, or write permission is missing or inaccessible, block with the missing public coordinate and the exact unblock condition. Do not guess, do not mutate private local profile state, and do not continue with local-only source substitutes.

Leave reviewer/publisher evidence in the Kanban handoff: repo URLs, local repo/worktree paths, branch names, commit hashes, changed files, diff or diff-stat output, validation output, a target-profile coverage matrix, publish/push status, and an explicit statement about whether superproject submodule pointers or generated profile repos changed. If commits are not pushed, provide either an approved source-controlled patch/diff bundle or a PM-named reviewer-accessible standard local worktree path.
