# Severity Rubric

Use severity to reflect user impact and repair priority, not personal code-style preference.

## P0

Use P0 for issues that must be fixed immediately:

- Project cannot start or build for its intended use.
- Core data can be lost, corrupted, overwritten, or exposed.
- Secrets or private credentials are exposed.
- Auth or permission checks are bypassable in a sensitive path.
- A destructive action can run on the wrong target.
- Payment, account, storage, or production infrastructure can be abused.

## P1

Use P1 for launch-blocking or core-flow issues:

- Core feature fails.
- UI shows success when persistence or backend action did not happen.
- Missing required environment validation causes production failure.
- Duplicate submit or race condition can create bad user data.
- Error handling hides failure in a core workflow.
- A major mobile or responsive issue blocks ordinary use.

## P2

Use P2 for medium-risk reliability or maintainability issues:

- State ownership is unclear but current demo still works.
- Large component or hook makes future changes risky.
- Repeated logic can diverge across flows.
- Type definitions are weak enough to allow likely mistakes.
- Loading, empty, or error states are incomplete but not catastrophic.
- Build/deploy setup relies on undocumented manual steps.

## P3

Use P3 for low-risk cleanup:

- Naming inconsistency.
- Small duplication.
- Dead comments.
- Minor style issues.
- Non-critical refactors.

## Downgrade Rules

Downgrade when:

- The issue is purely stylistic.
- The affected code is unused or prototype-only.
- The user asked only for a quick demo readiness check.
- The issue has no clear user, data, security, launch, or maintenance impact.

## Upgrade Rules

Upgrade when:

- The issue affects data persistence.
- The UI can falsely report success.
- The issue is on the main user journey.
- It can appear only after deployment.
- It can cost money, leak secrets, or damage user trust.

