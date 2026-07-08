# Review Modules

## Project Intake

Identify:

- Project type: React, Next.js, Vue, Python, Electron, Tauri, browser extension, backend service, script, or mixed stack.
- Entry points and core source directories.
- Start, build, typecheck, lint, and test commands.
- Environment variables and whether `.env.example` exists.
- Backend, database, storage, auth, and deployment assumptions.
- README drift: instructions that no longer match actual code.

Common files:

- `package.json`
- `README.md`
- `src/`
- `app/`
- `pages/`
- `vite.config.*`
- `next.config.*`
- `tsconfig.json`
- `.env.example`
- `pyproject.toml`
- `requirements.txt`
- `Cargo.toml`

## Engineering Review Layer

Look for real risks, not abstract preference:

- Functions or components with too many responsibilities.
- Missing, wrongly routed, or ambiguous parameters.
- State duplicated across multiple owners.
- Async races, stale closures, missing pending guards, and lost error paths.
- UI actions that only mutate local state when persistence is expected.
- Errors swallowed, logged only, or converted into false success.
- Types that are too broad to protect the workflow.
- Split implementations for the same feature.
- Security and privacy issues: exposed secrets, unsafe input handling, weak auth checks, broad file access, unsafe command or SQL construction.
- Deployment risks: missing env validation, local-only paths, CORS assumptions, server/client boundary mistakes.
- AI-coding artifacts: unused alternative flows, inconsistent naming, unreachable code, mismatched comments, duplicated helpers.

## Evidence Extractor

For each finding, collect:

- Problem location: file and line where possible.
- Related functions, components, hooks, classes, API routes, config keys, or commands.
- Key variables or parameters.
- Current behavior in the code.
- Expected or missing behavior.
- Call chain or data flow when relevant.
- Reproducible result, command failure, or logically inferred consequence.

Mark confidence:

- Proven: directly visible in code or command output.
- Likely: strong inference from local code, but not executed.
- Needs verification: plausible but requires runtime data, credentials, or a missing environment.

## Technical Context Explainer

Use this when a finding depends on a specific function, parameter, hook, state variable, API call, config value, async flow, type, or interface.

Place explanations under `涉及对象`.

## Impact Bridge

Output as `问题说明`.

Always include cause plus impact. Connect code facts to runtime, data, UX, launch, security, cost, or maintainability consequences.

## Prioritized Fix Planner

For each finding:

- Assign P0-P3 severity.
- State whether it should be fixed now, before launch, or later.
- Suggest a repair direction.
- Mention verification after the fix when useful.

