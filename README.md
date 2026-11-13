# ez-agent

个人 Agent 协作规范与工程 Skill。目标是维护一份个人工程规范，并让不同 Agent 复用同一套内容。

## 使用方式

1. 安装后重启或重新加载对应 Agent。
2. 让 Agent 列出已发现的 Skills，确认加载情况。
3. 对架构设计、实现、重构等任务，可显式要求 Agent 使用相应 Skill；自动触发取决于各 Agent 的发现与调用机制。
4. 项目自身的 `AGENTS.md`、`CLAUDE.md`、Cursor Rules 或 Copilot 项目指令仍然可以定义项目特定约束。发生冲突时，应先明确并解决冲突，不要依赖不同 Agent 未必一致的优先级规则。
