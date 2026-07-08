# Orchestration

Use this reference to select review modules and depth.

## Intent Routing

If the user says only "review", "帮我 review", or similar:

- Use `Quick Health Check`.
- Focus on high-confidence correctness, data, launch, and maintainability risks.
- Produce an evidence-first report, not a full audit.

If the user asks whether the project can run:

- Use `Runability Review`.
- Inspect install scripts, start scripts, build scripts, environment variables, local services, and error output.
- Explain whether failures are caused by dependencies, config, code, or missing services.

If the user asks whether the project can launch:

- Use `Launch Readiness`.
- Include build, environment variables, secrets, persistence, auth, deployment config, CORS, storage, and core flows.

If the user asks about one feature:

- Use `Feature Reliability`.
- Trace the feature from UI event to state update, API call, persistence, error handling, and reload behavior.

If the user asks whether the code is "AI-written", "messy", or hard to maintain:

- Use `Code Health`.
- Focus on responsibility boundaries, duplication, dead code, split-brain implementations, over-large files, unclear state ownership, and fragile coupling.

If the user asks for a version to send to someone else:

- First produce or preserve the evidence-first findings.
- Then run `Audience Adapter`.

## Review Modes

### Quick Health Check

Run:

- Project Intake
- Engineering Review Layer
- Evidence Extractor
- Technical Context Explainer as needed
- Prioritized Fix Planner

### Runability Review

Run:

- Project Intake
- Dependency and script inspection
- Build/start/test command review when feasible
- Environment variable review
- Error interpretation
- Prioritized Fix Planner

### Launch Readiness

Run:

- Project Intake
- Build and typecheck review when feasible
- Security and secret review
- Persistence and data integrity review
- User journey review
- Deployment config review
- Prioritized Fix Planner

### Feature Reliability

Run:

- Project Intake only as much as needed
- Feature file discovery
- UI event tracing
- State and data flow review
- API/persistence review
- Error and loading state review
- Evidence Extractor

### Code Health

Run:

- Project Intake
- Structure and ownership review
- Duplication and dead-code review
- State ownership review
- Type and interface review
- Maintainability impact review

