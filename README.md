# vibecoding-review

`vibecoding-review` 是一个面向半技术型 vibe coding 用户的 Codex skill，用来对 AI 辅助生成或大幅修改的软件项目做工程证据型 code review。

它会保留专业判断、文件位置、函数、参数、状态流、调用链和配置证据，同时补充必要上下文，让使用者能看懂每个 finding 为什么成立、会造成什么影响、应该先修什么。也可以根据读者来调整输出结果，例如面向开发者、老板、客户、设计师或非技术协作者。

## 适合场景

- Review 一个由 Cursor、Claude Code、GitHub Copilot 或其他 AI coding agent vibe coding 出来的项目。
- 判断项目能不能跑、能不能上线、核心功能是否可靠。
- 检查某个功能是否只是“看起来完成了”，实际没有接上数据、API 或持久化。
- 识别 AI 生成代码中常见的状态混乱、重复实现、假成功、错误吞掉、环境变量缺失等问题。
- 给半技术用户提供能看懂的工程证据，而不是泛泛的“代码质量建议”。

## 模块编排

这个 agent 按模块执行 review：

1. `Review Orchestrator`：识别用户意图并选择 review 模式。
2. `Project Intake`：识别项目类型、入口、命令、环境变量和部署假设。
3. `Review Scope Selector`：控制审查范围，避免无边界扫描。
4. `Engineering Review Layer`：做专业代码审查，发现真实问题。
5. `Evidence Extractor`：提取文件、函数、参数、调用链、状态流等证据。
6. `Technical Context Explainer`：解释 finding 里关键技术对象的角色。
7. `Impact Bridge`：写入 `问题说明`，连接原因和影响。
8. `Prioritized Fix Planner`：按 P0-P3 排序，并给出修复方向。
9. `Audience Adapter`：仅在用户明确要求转述给老板、客户、设计师或协作者时启用。

## 默认输出结构

中文 review 默认使用以下 finding 格式：

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

其中 `问题说明` 必须同时包含：

- 原因：基于工程证据解释问题为什么成立。
- 影响：说明它会导致什么运行、数据、用户体验、上线、安全、成本或维护后果。

## 文件结构

```text
vibecoding-review/
  SKILL.md
  references/
    orchestration.md
    review-modules.md
    evidence-report-format.md
    severity-rubric.md
    technical-context-explainer.md
    audience-adapter.md
```

## 安装方式

这个仓库现在是标准 Codex skill 格式。仓库根目录包含 `SKILL.md`，Codex 可以直接按 skill 读取，并按需加载 `references/` 里的模块说明。

安装到 Codex：

```bash
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py --repo sanozz31/vibecoding-review --path . --name vibecoding-review
```

最简单的用法：

```text
请用 vibecoding-review 帮我 review 这个 vibe coding 项目。
```

中文也可以直接说：

```text
按 vibecoding-review 的流程帮我 review 这个 vibe coding 项目，重点看工程证据和优先级。
```

## 设计原则

- 专业 review 不降级。
- 默认保留工程证据。
- 不主动输出小白类比或老板汇报版。
- 每个问题都要说明证据、涉及对象、原因、影响和修法。
- 少列泛泛建议，多列高信号问题。
- 只有用户明确要求转述时，才启用受众适配。
