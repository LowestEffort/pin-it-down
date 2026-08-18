# Document profiles

Use these profiles as adaptable defaults. Preserve an established project convention and omit sections that would be empty or irrelevant.

## `SPEC.md`

Describe what the product or change must accomplish.

- Background and problem
- Goals
- Non-goals
- Users and use cases
- Scope
- Functional requirements
- Non-functional requirements
- Constraints
- Observable acceptance criteria
- Open questions and `TBD` items

Keep technical implementation choices out unless they are genuine requirements or constraints.

## `DESIGN.md`

Describe how the confirmed specification will be implemented.

- Design goals and current state
- Architecture and component responsibilities
- Interfaces, events, and data structures
- Main flows and state transitions
- Error handling and recovery
- Security and privacy considerations
- Alternatives and recorded decisions
- Test strategy
- Open technical questions

Tie design decisions to requirements. Label implementation-derived facts separately from proposed changes.

## `PLAN.md`

Describe a verifiable implementation sequence.

- Goal and non-goals
- Prerequisites
- Phases and bounded tasks
- Dependencies and ordering
- Verification for each phase
- Risks and mitigations
- Rollback or recovery where relevant
- Completion criteria

Keep tasks concrete enough to execute, but do not restate the entire specification or design.

## Status language

Use explicit labels when provenance or certainty matters:

- **Confirmed**: Explicitly accepted by the user.
- **Current behavior**: Supported by repository evidence.
- **Provisional**: Usable for now but not final.
- **Recommended**: Proposed by Codex and not yet accepted.
- **TBD**: Materially unresolved.

Do not add labels mechanically to every sentence. Use them where ambiguity could change implementation or acceptance.
