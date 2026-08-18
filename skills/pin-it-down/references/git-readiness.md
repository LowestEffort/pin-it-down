# Local Git readiness

Prepare a real project for local version control and create task-scoped checkpoint commits after successful document writes. Keep initialization, ignore rules, staging, and commits bounded to the resolved project, and leave history rewriting or external operations to separate explicit requests.

## Applicability

Perform this workflow only when all of the following are true:

- the mode authorizes document writes;
- a real project root was resolved instead of the session fallback;
- the user did not opt out of Git preparation;
- the current operation is not Review.

## Capture the pre-write baseline

When an existing repository owns the project, capture `git status --short` and the relevant target diffs before changing managed documents or project instructions. Record which target paths were already dirty or untracked so later staging can distinguish task-owned changes. Do not stash, discard, reset, or otherwise alter pre-existing work.

## Discover the repository boundary

1. Verify Git availability with `git --version`. If unavailable, report the missing prerequisite without installing anything.
2. From the resolved project path, use `git rev-parse --show-toplevel` and related read-only checks to detect an existing repository, worktree, submodule, or parent repository.
3. Treat an existing owner repository as authoritative. Do not run `git init` inside it.
4. If the detected repository root is above the resolved project root, keep changes bounded to the resolved project and report the owner repository path.
5. Do not reinitialize an existing repository or change its branch.

## Initialize when needed

If no repository owns the resolved real project path, run:

```text
git init -b main
```

Verify that the resulting repository root equals the resolved project root and that the unborn initial branch is `main`. If initialization fails, report the exact error and do not attempt destructive recovery.

## Maintain `.gitignore`

Use a `.gitignore` at the resolved project root. Preserve existing comments, ordering, negations, and project-specific rules.

- Add only patterns supported by detected manifests, tools, generated directories, or confirmed project conventions.
- Before adding a pattern, identify existing untracked files that it would newly hide. Ask for direction rather than hiding those files automatically.
- Prefer narrow patterns over broad wildcards.
- Do not ignore dependency lockfiles, source files, maintained project documents, example configuration, or release artifacts without explicit project evidence.
- Do not assume common build directories are disposable; Chrome extensions and other packaged applications may intentionally maintain built artifacts.
- Include likely local secrets such as `.env` only when doing so does not hide an existing file without review, and preserve tracked example files such as `.env.example`.

Typical evidence-backed patterns may include:

- Node.js: `node_modules/`
- Python: `.venv/`, `__pycache__/`, `*.py[cod]`
- .NET: `bin/`, `obj/`
- Local OS metadata: `.DS_Store`, `Thumbs.db`

Treat these as candidates, not a universal template.

## Verify readiness

After initialization or ignore maintenance:

1. Confirm the repository root and current branch.
2. Run `git status --short` and retain its output as verification evidence.
3. Inspect ignored paths when `.gitignore` changed.
4. Confirm that maintained documents and the effective project AGENTS file remain visible to Git.
5. Report whether the repository was created or already existed, whether `.gitignore` changed, and which operations were deliberately not performed.

## Create a verified local checkpoint

Create one local checkpoint commit after the requested document write, project-instruction integration, and Git-readiness validation succeed. Skip the commit and report the reason when there is no task-owned change, validation failed, a likely secret is present, or task-owned changes cannot be separated confidently from pre-existing work.

1. Build an explicit list containing only files created or changed by this skill. Never use `git add .`, `git add -A`, or another repository-wide staging command.
2. Exclude unrelated user changes and unexpected untracked files. If a target file contained pre-existing changes whose ownership is ambiguous, do not stage that file automatically.
3. Stage only the verified explicit paths with `git add -- <paths>`.
4. Inspect `git diff --cached --name-only`, `git diff --cached --stat`, and `git diff --cached --check`. Review the staged content needed to confirm that no unrelated data or likely secret is included.
5. Commit with a concise message describing the completed documentation checkpoint.
6. Verify the new commit with `git show --stat --oneline -1` and run `git status --short` again. Report the commit hash and any remaining unrelated changes.

If staging or committing fails, do not bypass hooks, auto-configure identity, or attempt destructive recovery. Report the exact error and resulting index and working-tree status.

Do not amend, rebase, reset, switch or create branches, configure identity, add or change remotes, install Git LFS, or push unless the user explicitly requests that separate operation.
