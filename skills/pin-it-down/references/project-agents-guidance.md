# Project AGENTS guidance

Use this reference only when a document-write mode integrates maintained documents with the effective project-root instruction file.

## Inclusion test

Add a rule only when all of the following are true:

- it is specific to the confirmed project;
- it will materially affect future project work;
- it is not reliably inferable from the repository;
- equivalent guidance is not already present in the effective instruction chain.

Treat the project instruction file as a routing layer, not as a duplicate specification, design document, plan, or runbook. If removing a generated rule would not materially change future Codex behavior, omit it.

## Write boundaries

- Write only to the effective `AGENTS.md` or `AGENTS.override.md` at the confirmed project root.
- Project-local creation and bounded updates need no separate approval when this skill's document-write integration is active.
- Preserve unrelated, equivalent, and stricter existing guidance.
- Do not broadly rewrite or compact existing content solely for brevity unless the user explicitly requests that cleanup.
- Never modify an AGENTS file outside the confirmed project root, including any global file under `CODEX_HOME` or `~/.codex`.

## Compact generated guidance

Prefer one `## Project workflow` section with two to five dense bullets as a soft target. Adapt document paths to the established project convention and mention only managed documents that exist. Merge semantically with an equivalent existing section instead of duplicating it.

Use this documentation bullet when relevant:

```md
- For planning or changes that may affect behavior or architecture, read the relevant `docs/SPEC.md`, `docs/DESIGN.md`, and `docs/PLAN.md`; report material conflicts and update these documents only when explicitly requested or through `$pin-it-down`.
```

When local Git readiness is enabled, also include these Git bullets unless equivalent or stricter guidance already exists:

```md
- Before editing, inspect `git status --short` and preserve unrelated changes; afterward, review the relevant diff, run `git diff --check`, and include untracked files in the final status.
- Create local commits at coherent, verified milestones; stage only task-related changes, skip commits when verification fails or changes cannot be isolated, and use descriptive messages. Do not amend, rebase, reset, switch branches, add remotes, or push unless explicitly requested.
```

When updating an existing project instruction file, replace the exact legacy generated bullet `Do not stage, commit, amend, switch branches, add remotes, or push unless explicitly requested.` with the current checkpoint bullet. Also recognize the earlier `change branches` wording as a legacy generated variant. Do not replace any other user-authored or uncertain commit policy automatically.

Omit rationale, examples, generic best practices, speculative rules, and empty categories from the generated project instruction file. Never weaken explicit prohibitions merely to reduce length.
