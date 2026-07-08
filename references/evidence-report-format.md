# Evidence Report Format

Use this format for default findings in Chinese review output.

```markdown
## [P1] 问题标题

问题位置：
- src/example.ts:42

工程证据：
- ...

涉及对象：
- ...

问题说明：
...

建议修法：
...
```

## Field Rules

### 问题标题

State the defect or risk directly. Avoid vague titles like "logic issue" or "code can be improved".

Good:

- `[P1] 保存流程只更新前端状态，没有写入真实数据源`
- `[P2] 项目状态集中在单个 hook 中，后续功能容易互相影响`

### 问题位置

Include file paths and line numbers when available. If the issue spans a flow, list the main locations in flow order.

If no exact line is available, cite the closest file, function, or config key.

### 工程证据

Use concrete observations:

- What function calls what.
- What parameter is missing or unchecked.
- What state is updated.
- What API is or is not called.
- What command fails.
- What config is absent.
- What branch swallows an error.

Do not write broad conclusions here. Save interpretation for `问题说明`.

### 涉及对象

Explain technical objects only as much as needed for this finding:

- `handleSave`: 保存按钮的事件处理函数。
- `projectId`: 当前项目的唯一 ID，后端靠它决定更新哪条记录。
- `setProjects`: 只更新当前浏览器内存里的列表，不等于写入后端。
- `isSaving`: 保存请求是否正在进行，通常用来禁用按钮并防止重复提交。

Skip this field only when the finding is already obvious and has no specialized technical objects.

### 问题说明

Must include both cause and impact.

Cause:

- Explain why the evidence constitutes a problem.
- Ground the explanation in the code facts above.

Impact:

- Explain what can break, become unreliable, or become costly.
- Name the affected dimension: runtime, data correctness, user experience, launch readiness, security, cost, or maintainability.

Avoid empty statements like:

- "这里逻辑不清晰。"
- "这会影响维护。"
- "建议优化。"

Write:

- "这里的问题不是按钮完全无效，而是保存流程只更新了前端状态，没有写入真实数据源。因此用户短时间内会看到修改结果，但刷新页面后数据会恢复，属于核心功能的假成功。"

### 建议修法

Give a direction, not necessarily a full patch unless the user asked for implementation.

Include:

- What to change.
- Where to change it.
- What behavior to verify afterward.

## Summary Format

After findings, add a short priority section:

```markdown
优先修：
1. [P1] ...
2. [P1] ...

可以稍后修：
1. [P2] ...
2. [P3] ...
```

Keep summaries short. The findings are the main output.

