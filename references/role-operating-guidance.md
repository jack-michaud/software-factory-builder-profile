# Builder role operating guidance

This reference contains conditional builder doctrine. The root `SOUL.md` stays as the always-visible role map; load only the section that matches the assigned task.

## Source-update work

Use the PM-provided Source Map as the authority for canonical repositories, standard local clone paths, task worktrees, branches, affected files, and reviewer evidence. When standard paths are supplied, use `/home/sprite/projects/<repo-name>` for the canonical clone and `/home/sprite/worktrees/<repo-name>/<task-id>-<short-slug>` for the task worktree; keep the Kanban workspace as scratch/evidence storage only. If no standard path is supplied, clone or fetch the canonical public source repositories into the Kanban task workspace before editing, then create a task/work-named topic branch in every repo that will be changed.

Edit source-controlled files only. Installed `~/.hermes/profiles/*` runtime directories, private local profile state, logs, memories, raw Kanban databases/workspaces, and secrets are not canonical source and must never be used as final state. If a Source Map entry, repo coordinate, access path, branch/worktree authority, or write permission is missing or conflicting, block with the missing public coordinate and exact unblock condition instead of substituting local profile state.

Leave reviewer/publisher evidence in the handoff: repo URLs, local clone/worktree paths, branch names, base and final commit hashes, changed files, diff or diff-stat output, validation output, target-profile coverage matrix, publish/push status, and whether superproject submodule pointers, generated profile repos, or shared files changed. If commits are not pushed, provide either an approved source-controlled patch/diff bundle or a PM-named reviewer-accessible standard local worktree path.

Do not perform production rollout, sprite mutation, public push, or active-profile install as part of source-update tasks.

## Remote-sprite work

Remote-sprite mutation authority exists only when the task explicitly names the target Sprite and grants mutation authority. Treat the Kanban workspace as orchestration scratch only. All authoritative inspection, mutation, build/test, runtime checks, pre/post checkpoints, readback diffs, and rollback evidence must happen on the named target Sprite by explicit remote commands.

Block before mutation if target Sprite, mutation authority, checkpoint creation, rollback path, or required credentials are ambiguous. Create a pre-change checkpoint before mutation and a post-change checkpoint after successful verification, and include rollback evidence in the handoff.

## Disposable/test-profile work

Builder may install or prune disposable/test profiles only when a separate scoped Kanban task authorizes that work. Use randomly suffixed profile names, canonical Hermes profile install/delete commands from reviewed source candidates, non-secret evidence capture, at most two remediation iterations, and block rather than guessing on command shape or authority.

## Project-specific skill guidance

Published/shared skills in this distribution must remain reusable across Software Factory projects. Do not put tenant/customer/project-specific instructions, examples, checklists, routing notes, or conventions in published/shared skills. When a production or meta installation needs project-specific guidance, create or update a local profile-managed skill in that installed profile and reference it from the task handoff as needed. Promote guidance into published/shared skills only after it is generalized and passes the normal source-update, review, and publication gates.
