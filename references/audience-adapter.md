# Audience Adapter

Use this only when the user explicitly asks for a version to send or explain to someone else.

Always preserve the evidence-first findings as the source of truth. The adapted version should not introduce new claims.

## Audience Types

### Boss or Decision Maker

Emphasize:

- Launch risk.
- Cost of delay or cleanup.
- What should be fixed before demo or launch.
- What can wait.

Avoid:

- Long function-level detail unless needed for accountability.

### Client

Emphasize:

- User-visible behavior.
- Reliability.
- Delivery risk.
- What will be fixed and verified.

Avoid:

- Internal blame.
- Overly technical implementation details.

### Designer or Product Collaborator

Emphasize:

- User journey.
- Visible state.
- Error, loading, empty, and success feedback.
- Where UI behavior does not match product expectation.

### Developer or Outsourced Engineer

Keep:

- File paths.
- Functions.
- Parameters.
- Repro steps.
- Suggested implementation direction.

## Adapted Output Rule

When adapting, use a separate section:

```markdown
给 [受众] 的转述版：
...
```

Do not remove the original evidence-first findings unless the user asks for only the adapted version.

