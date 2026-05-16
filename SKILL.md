---
name: knowledge-capture
description: Use when a superpowers work cycle completes and design decisions, domain concepts, or development experience needs to be persisted into the project's permanent record system (ADR, knowledge base, session history, TODO tracking). Also use when reviewing existing sessions/ADR for cross-reference completeness or preparing project knowledge for new team members.
variables:
  specs_dir: docs/superpowers/specs/
  adr_dir: docs/adr/
  sessions_dir: docs/sessions/
  knowledge_dir: docs/knowledge/
  todo_file: TODO.md
---

# knowledge-capture

## 概述

将临时性工作流产物（brainstorming specs/、writing-plans plans/ 以及开发过程记忆）中的有价值信息，提取到项目的持久化记录体系中。

```
输入 → 输出
{specs_dir}（设计文档）          →  ADR（架构决策记录）
{plans_dir}（实现计划）          →  TODO.md（待办追踪）
代码变更                        →  {knowledge_dir}（领域知识库）
开发过程记忆                    →  {sessions_dir}（项目史书）
```

## 前置依赖

此技能假设已按以下顺序完成前置工作流：
1. **brainstorming** — 产生设计文档（写入 {specs_dir}）
2. **writing-plans** — 产生实现计划（写入 {plans_dir}，默认为 `docs/superpowers/plans/`）
3. **implementation** — 产生代码变更

## 核心原则

- **不修改原始 specs/plans** — 它们是本地工作文件，信息提取后保留原始状态
- **不重复记录** — 设计决策的关键论证只入 ADR，session 不重复
- **所有链接可工作** — 检查交叉引用
- **路径可配置** — 通过 YAML front matter 中的 `variables` 调整输出目录

## 执行步骤

### 步骤 1：提取 ADR

扫描 `{specs_dir}` 中的设计文档，识别关键决策点。

**每个关键决策点需同时满足**：
- 有明确的选项对比（至少 2 个有效选项）
- 对后续开发有约束力
- 不是实现细节（如"用 for 还是 while"不算）

将每条 ADR 保存为 `{adr_dir}/ADR-XXX-{简短标题}.md`，格式参见 [templates/adr-template.md](./templates/adr-template.md)。

### 步骤 2：更新知识库

从设计文档和实现代码中提取新的领域概念，写入 `{knowledge_dir}`。

**典型内容**：DSL 语法规范、DDD 架构约定、模块间依赖规则、关键术语定义、命名规范。

格式参见 [templates/knowledge-template.md](./templates/knowledge-template.md)。

### 步骤 3：编写 Session

新建项目史书记录 `{sessions_dir}`（序号 = 当前最大 + 1）。只记录"做成了什么"和"踩了什么坑"，设计论证指向 ADR。

格式参见 [templates/session-template.md](./templates/session-template.md)。

### 步骤 4：更新 TODO.md

将 session 中"产生的待办"汇总到 `{todo_file}`，按模块/优先级分组。已有 TODO 做增量更新：新增待办标记 ⏳，已完成标记 ✅。

### 步骤 5：交叉引用检查

- Session → ADR（session 头部的关键决策字段）
- ADR → Source Spec（ADR 的"来源"字段）
- Knowledge → ADR/Session（知识的"相关参考"字段）

### 步骤 6：Commit

检查当前目录是否在 git 仓库中，如果是则执行：

```bash
git add {adr_dir}/ {sessions_dir}/ {knowledge_dir}/ {todo_file}
git commit -m "docs: 知识捕获 - {阶段描述}"
```

如不在 git 仓库中，提示用户手动执行版本控制。

## 路径配置说明

中的所有路径均通过 SKILL.md 的 YAML front matter 中 `variables` 字段配置。Superpowers 用户可直接使用默认值；非 Superpowers 用户可根据项目结构修改路径变量。

## 常见错误

| 错误 | 后果 | 正确做法 |
|------|------|---------|
| 在 session 中重复记录 ADR 内容 | 多处维护，信息不一致 | session 只叙事，ADR 只决策 |
| 修改 specs/plans 本地文件 | 工作流历史丢失 | 不动 specs/plans，信息提取到持久化体系 |
| 只写 session 不写 ADR | 决策原因不可回溯 | 每个有选项对比的决策都提炼 ADR |
| ADR 缺少"被否决选项" | 不知道为什么否决 B | 明确记录每个选项的被否决原因 |
| 忘记更新 TODO.md | 待办沉底无人跟进 | 每次强制更新 TODO.md |
