# Technical Context Explainer

Use this reference to decide when and how to explain technical details.

## When To Explain

Explain a technical object when the finding depends on understanding:

- A function's role.
- A parameter's meaning.
- A hook or component's ownership.
- A state variable's relationship to visible UI.
- An API call's persistence behavior.
- An async sequence or race.
- A config value's local or production effect.
- A type/interface's data contract.

Do not explain every syntax detail. Explain only objects needed to understand the finding.

## Explanation Style

Keep explanations compact and engineering-adjacent:

- Define the object's role in the system.
- State why it matters to this finding.
- Avoid metaphors unless the user asks for non-technical phrasing.
- Avoid "for beginners" tone.

## Examples

```markdown
涉及对象：
- `projectId`：当前项目的唯一 ID，后端靠它决定更新哪条记录；缺失时保存请求无法可靠定位目标。
- `setProjects`：React 前端状态更新函数，只影响当前页面内存，不代表数据已经写入数据库。
- `updateProject`：预期的持久化 API；如果保存流程没有调用它，刷新后通常会回到旧数据。
```

```markdown
涉及对象：
- `isSubmitting`：提交请求的进行中标记，通常用来禁用按钮并阻止重复提交。
- `handleSubmit`：表单提交入口；如果这里没有 pending guard，用户快速点击两次会触发两次请求。
```

```markdown
涉及对象：
- `VITE_API_URL`：前端构建时读取的 API 地址；本地缺失可能只影响开发，线上缺失会让所有 API 请求指向错误地址或直接失败。
```

## Common Detail Patterns

### Local State vs Persistence

Clarify whether a function only updates browser memory or writes to a durable source such as backend, database, file, or remote storage.

### False Success

Flag when UI shows success before the real operation finishes, or when errors are swallowed. These are usually P1 on core flows.

### Parameter Propagation

Trace where the parameter originates, where it is passed, and where it is consumed. Explain the failure if it is missing or stale.

### Async Flow

Identify ordering dependencies:

- request starts
- UI updates optimistically
- response succeeds or fails
- error is handled or ignored
- state is reconciled or left stale

