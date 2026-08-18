[English](README.md) | [日本語](README.ja.md)

# Pin It Down

Turn evolving decisions into maintained project documents and safe local Git checkpoints.

Pin It Down is an explicitly invoked Codex skill for creating, reconciling, reviewing, and revising Markdown specifications, technical designs, and implementation plans. It can capture a rough idea through an adaptive interview or turn decisions already made in a conversation into durable project documentation.

## What it does

- Creates only the development documents that are relevant to the request.
- Keeps confirmed requirements, repository evidence, recommendations, and unresolved items distinct.
- Updates existing documents with bounded diffs instead of rewriting unrelated content.
- Maintains a lean project-root `AGENTS.md` or `AGENTS.override.md` when document changes require durable routing guidance.
- Prepares local Git when working in a real project and creates a verified, task-scoped checkpoint commit after successful document writes.
- Supports read-only reviews that report contradictions, omissions, and stale decisions without changing files.

## Modes

| Mode | Use it when |
| --- | --- |
| Discovery | You have a rough idea and want Codex to ask the decisions that materially shape it. |
| Capture | The important decisions already exist in the current conversation. |
| Sync | Existing managed documents need a small update after later decisions. |
| Review | You want an audit or proposal without file changes. |

## Managed files

Pin It Down follows an existing project documentation convention when one exists. Otherwise, it uses:

```text
docs/SPEC.md
docs/DESIGN.md
docs/PLAN.md
```

For real projects, a document-write operation may also create or minimally update the effective project-root `AGENTS.md` or `AGENTS.override.md`, initialize a local Git repository, extend `.gitignore` from project evidence, and create a local checkpoint commit. These integrations are skipped in Review mode and when the session directory is used as a fallback.

## Installation

Ask Codex to install the skill from this repository:

```text
Use $skill-installer to install https://github.com/LowestEffort/pin-it-down/tree/main/skills/pin-it-down
```

Alternatively, copy `skills/pin-it-down` into `$CODEX_HOME/skills/pin-it-down` (normally `~/.codex/skills/pin-it-down`). Start a new Codex task after installation so the skill is discovered.

## Usage

Invoke the skill explicitly. It does not run for ordinary planning, implementation, debugging, or brainstorming requests.

```text
$pin-it-down Start from this rough product idea and help me create the specification, design, and implementation plan.

$pin-it-down Capture the decisions from this conversation in the project documents.

$pin-it-down Sync the existing documents with the decisions we just made.

$pin-it-down Review the project documents for contradictions and omissions. Do not change files.
```

Generated documents follow the language of the request and the established language and terminology of existing project documents.

## Safety boundaries

- Explicit invocation only.
- Review requests are read-only and proposal-only.
- Application code, tests, dependencies, hooks, and unrelated configuration are out of scope.
- Existing user-authored documents and project instructions are preserved outside the requested diff.
- Global Codex instructions under `CODEX_HOME` or `~/.codex` are never modified.
- Git staging is limited to explicit task-owned files and is inspected before committing.
- The skill never rewrites Git history, configures identity or remotes, or pushes.
- It never publishes to GitHub, issue trackers, or other external services.

## Acknowledgements

The interview-first idea was inspired by Matt Pocock's [`grill-me`](https://github.com/mattpocock/skills/tree/main/skills/productivity/grill-me) and [`grill-with-docs`](https://github.com/mattpocock/skills/tree/main/skills/engineering/grill-with-docs) skills. Pin It Down is an independent implementation and does not depend on or bundle those skills.

## License

[MIT](LICENSE)
