---
name: pin-it-down
description: Create, reconcile, review, or revise local Markdown specifications, technical design documents, and implementation plans from explicit user requirements, confirmed conversation decisions, existing project documents, and scoped repository evidence. For real projects, also maintain bounded project-local AGENTS guidance, prepare local Git readiness, and create verified task-scoped checkpoint commits after document writes. Use only when explicitly invoked as $pin-it-down. Do not use for ordinary implementation, debugging, brainstorming, or planning requests without explicit invocation. Do not publish externally, modify application code, rewrite Git history, configure remotes, or push.
---

# Pin It Down

Turn an explicitly invoked documentation request into maintained local Markdown development documents. Ask only the questions that materially improve the result, and keep confirmed facts, open decisions, and recommendations distinct.

## Operating contract

- Operate only after explicit `$pin-it-down` invocation.
- Limit writes to the requested specification, design, and plan Markdown files plus the bounded project instruction, local Git readiness, and verified checkpoint-commit integrations described below.
- Treat `create`, `write`, `document`, `update`, `revise`, `sync`, and `reflect` as document-write authorization when the requested targets are clear.
- Treat `review`, `check`, `audit`, `inspect`, and `propose` as read-only, proposal-only operations.
- If invocation does not clearly authorize a write, inspect and propose without changing files.
- Do not modify application code, tests, dependencies, hooks, other configuration outside the bounded integrations, or external systems.
- Do not publish to issue trackers, repositories, or other services.
- Do not use subagents unless the user separately approves them.

## Select the mode

Infer the narrowest suitable mode from the request:

- **Discovery**: Start from a rough idea. Ask adaptive questions, then create the requested documents.
- **Capture**: Synthesize decisions already made in the current conversation. Ask only about material gaps.
- **Sync**: Apply later decisions to existing managed documents with a minimal diff.
- **Review**: Inspect documents for omissions, contradictions, or staleness without writing.

Do not restart a full interview in Capture or Sync mode. Allow the user to stop questioning and continue with explicit `TBD` items.

## Resolve the target project

Choose the project root in this order:

1. A project path explicitly supplied by the user.
2. The relevant Git, worktree, or workspace root when the current task is already inside it.
3. A project directory unambiguously identified in the current conversation.
4. The current session directory as a fallback.

Do not scan entire drives to guess a project. If multiple plausible roots remain, ask one concise question before writing.

Prefer an existing project documentation convention. Otherwise use `<project-root>/docs/`. Treat the following as the default managed files:

- `docs/SPEC.md`
- `docs/DESIGN.md`
- `docs/PLAN.md`

When using the session fallback, use `<session-directory>/docs/` and do not propose a project `AGENTS.md`.

## Gather evidence

Before questioning, writing, or reviewing:

1. Read applicable instructions and locate existing documentation conventions.
2. Read the relevant managed documents if they exist.
3. Inspect only the project files needed to establish current behavior, architecture, constraints, and tests.
4. For a real Git-backed project in a document-write mode, capture the pre-write status and relevant target diffs so later checkpoint commits can exclude unrelated changes.
5. Use this evidence order:
   1. Current explicit user instructions.
   2. User-confirmed decisions from the current conversation.
   3. Existing managed documents.
   4. Relevant code, tests, configuration, and manifests in the target project.
   5. Codex suggestions and inferences.

Do not promote suggestions or inferences to confirmed requirements. Surface material conflicts instead of silently choosing a source. Distinguish confirmed, provisional, open, inferred-from-implementation, and recommended content where the distinction matters.

## Interview adaptively

In Discovery mode:

- Ask one material question at a time.
- Offer two or three mutually exclusive options when useful.
- Put the recommended option first and explain its tradeoff briefly.
- Prefer product decisions from the user; investigate repository facts directly.
- Stop when the requested documents can be accurate and actionable.

In Capture or Sync mode, ask only questions whose answers would materially change scope, behavior, architecture, acceptance criteria, or implementation order. If the user says to proceed with unresolved items, record them as `TBD` or open questions.

## Create or update documents

Read [references/document-profiles.md](references/document-profiles.md) before creating, substantially restructuring, or reviewing managed documents.

- Create only the documents relevant to the request; do not create empty boilerplate files.
- Update existing documents in place and preserve their paths, conventions, unaffected structure, and unrelated user-authored content.
- Make the smallest complete diff in Sync mode.
- Avoid duplicating the same requirement or decision across sections. Cross-reference another managed document when appropriate.
- Record acceptance criteria as observable outcomes.
- Keep implementation sequencing out of `SPEC.md`, detailed architecture out of `PLAN.md`, and product requirements out of low-level design sections unless a cross-reference is required.
- If an existing document needs broad restructuring, show the proposed structure or diff and obtain approval before rewriting it.
- Verify paths, headings, internal consistency, unresolved markers, and the requested write scope after changes.

## Maintain project instruction integration

For a real project root, inspect the root `AGENTS.override.md` and `AGENTS.md` after managed documents exist.

Read [references/project-agents-guidance.md](references/project-agents-guidance.md) before creating or updating a project instruction file.

- Perform this integration automatically after a document write unless the user opts out or the current mode is Review.
- Select the effective root instruction file: use a non-empty `AGENTS.override.md` when present, otherwise use `AGENTS.md`; create `AGENTS.md` when neither exists.
- If both files exist, update only the file that Codex will load at the project root.
- Create or update the selected project-local instruction file without separate approval when this integration is in scope.
- Treat the project instruction file as a compact routing layer. Add only project-specific, future-relevant guidance that is not reliably inferable and is not already present in the effective instruction chain.
- Prefer one short section with two to five dense bullets as a soft target. Point to maintained documents instead of restating their contents, and add Git guidance only when local Git readiness is enabled.
- Omit rationale, examples, generic best practices, speculative rules, and empty categories.
- Deduplicate semantically, merge minimally, and never overwrite unrelated instructions.
- Preserve equivalent or stricter existing guidance. Do not broadly rewrite or compact an existing instruction file solely for brevity unless the user explicitly requests that cleanup.
- Replace only an exact legacy commit-prohibition bullet generated by an earlier version of this skill with the current verified-checkpoint policy. Preserve any other stricter or user-authored commit policy and report a material conflict instead of overwriting it.
- Never weaken explicit prohibitions merely to shorten the file.
- If existing project instructions materially conflict with the documentation integration, do not overwrite them. Report the conflict and ask for a decision.
- Treat the confirmed project root as the absolute AGENTS write boundary. Never create, edit, rename, replace, or delete any `AGENTS.md` or `AGENTS.override.md` outside it.
- In particular, never modify global instruction files under `CODEX_HOME`, `~/.codex`, or the user's global Codex configuration as part of this skill. If a global change appears useful, report a proposal only; require a separate explicit request outside this workflow before any such edit.
- Report whether the project instruction file was created, updated, or left unchanged.
- Explain that project instructions are automatically discovered on future runs started within that project; do not assume that accessing the project only by absolute path from another session loads them automatically.

## Prepare local Git readiness

For a real project in a document-write mode, read [references/git-readiness.md](references/git-readiness.md) before the first write to capture any existing Git baseline. After successful document writes and project-instruction integration, prepare local Git readiness and create a verified local checkpoint commit unless the user opts out or the current mode is Review.

- Skip Git initialization for the session-directory fallback.
- Verify that Git is available; do not install it or change global Git configuration.
- Detect an existing repository, worktree, submodule, or parent repository before initializing anything.
- Do not initialize a nested repository when an existing repository already owns the project path.
- If no repository owns the real project path, initialize the project with `git init -b main`.
- Create or minimally extend the project-local `.gitignore` from confirmed stack and repository evidence.
- Before adding ignore patterns, check whether they would hide existing untracked files; ask for direction if they would.
- Preserve existing ignore rules and do not ignore lockfiles, source files, maintained documents, or release artifacts without project evidence.
- Verify the repository root, current branch, `.gitignore` behavior, and `git status --short` after changes.
- Create a local commit only after document, instruction, and Git validation succeeds and the task-owned changes can be isolated from pre-existing work.
- Stage only explicit files changed by this skill; never use repository-wide staging or include unrelated changes. If ownership is ambiguous, validation fails, or no task-owned change remains, skip the commit and report why.
- Inspect the staged names and diff before committing, reject likely secrets or unexpected files, and use a concise message that describes the completed checkpoint.
- If a commit fails, do not bypass hooks or configure Git identity automatically. Report the exact error and resulting status.
- Verify the created commit and final working-tree status.
- Do not amend, rebase, reset, change branches, configure identity, add remotes, install Git LFS, or push unless the user explicitly requests that separate operation.

## Report the result

State:

- selected mode and resolved project root;
- created, modified, and reviewed files;
- confirmed decisions, remaining `TBD` items, and material conflicts;
- project instruction integration, local Git readiness, and checkpoint-commit actions, including the commit hash or the reason a commit was skipped;
- verification performed and its result;
- omitted or blocked AGENTS and Git steps with their reasons.
