# Global User Instructions

## Task size & workflow
- Trivial (single-line fix, direct answer, simple read): act directly. No skills, subagents, or plan mode.
- Small (single-file edit, focused bug fix): use built-in tools only. No Superpowers, subagents, or plan mode.
- Medium (multi-file change, debugging, moderate feature): ask before invoking Superpowers skills or subagents.
- Large (architecture changes, complex features, broad exploration): propose a plan first; ask before Superpowers, subagents, or plan mode.

## Commands and tests
- For small commands or quick tests, ask the user to run them and paste the results instead of running them yourself.
- Run commands or tests yourself only when they are necessary, long/complex, or the user explicitly asks you to.

## Token efficiency
- Avoid re-reading files already seen in the current conversation.
- Batch related file reads and edits.
- Keep responses concise; avoid unnecessary narration.
- Don't run heavy test/build suites without asking.

## Subagents
- Use subagents only for parallel independent tasks or isolated deep dives.
- Always ask before spawning a subagent.

## Plan mode
- Enter plan mode only for multi-file or architectural changes.
- Skip plan mode for single-file fixes.

## Permissions & destructive actions
- Stay in manual permission mode.
- Ask before destructive commands, long-running background tasks, or actions that modify shared state.

## Product Development Principles

Apply these principles to every codebase you touch, regardless of project:

- **Build for users first.** Before writing code, be able to answer: who is the end user, what does the business user/operator need, and how would a competitor review this?
- **Three-perspective audit.** Evaluate features and gaps from the end user, business user/operator, and competitor perspectives.
- **Robust minimal features first.** Make the smallest useful feature set production-ready before expanding. Avoid scope creep.
- **Config-driven.** No `localhost`, ports, URLs, credentials, or environment-specific values in source code. Put them in `.env.example`, `.dev.vars`, or YAML configs.
- **Documentation as deliverable.** Produce/update `architecture.md`, `code_map.md`, `future_plan.md`, `next_steps.md`, `operations.md`, and `marketing_strategy.md` for meaningful changes.
- **Security by default.** Fail closed, validate inputs at boundaries, never leak internal errors or secrets, design for privacy and deletion.
- **Tests are necessary but not sufficient.** Write persona-based tests (end user, operator, competitor) and add design review, edge-case analysis, and manual validation.
- **Observability is a feature.** Structured logs, dependency-aware health checks, and business-critical metrics are required.
- **Backward compatibility & migrations.** Breaking changes need a migration path; database migrations must be idempotent.
- **Idempotency & graceful degradation.** Mutations should be idempotent; external dependencies can fail—handle it cleanly.
- **API contract discipline.** No breaking API changes without versioning; commit OpenAPI specs; generate SDKs from specs where applicable.
- **Incident-ready services.** Every service exposes `/health`, failure modes are documented, and runbooks/on-call playbooks exist.
- **No production data in tests.** Use synthetic fixtures only.
- **Dependency hygiene.** Pin versions, audit before adding, and justify new dependencies.
- **Code review gate.** Every meaningful change requires spec review, security review, and code quality review.
- **Localization & accessibility.** If user-facing, design for i18n and a11y from the start.
- **Performance budgets.** Define p95 latency and resource limits per endpoint/feature.

