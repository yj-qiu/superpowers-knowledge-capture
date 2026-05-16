# Knowledge Capture

> **Superpowers** 生态的知识持久化技能

将临时性工作流产物（设计文档、实现计划、开发过程记忆）中的有价值信息，提取到项目的持久化记录体系：架构决策记录（ADR）、领域知识库、项目史书和待办追踪。

---

## 前提条件

- **Superpowers 用户**：本技能需要 [Superpowers](https://github.com/yj-qiu/superpowers) 技能框架。将本仓库克隆到你的 skills 目录即可使用。
- **独立用户**：无需框架。直接使用 `templates/` 目录中的模板，配合你自己的目录结构即可。

---

## 快速使用

### 作为 Superpowers 技能

```bash
# 克隆到 Superpowers skills 目录
cd 你的项目/skills/
git clone https://github.com/yj-qiu/superpowers-knowledge-capture.git knowledge-capture
```

然后在工作周期结束时调用技能：
> "使用 knowledge-capture 将本次头脑风暴的设计决策持久化到项目中。"

### 独立使用

```bash
# 克隆到任意位置
git clone https://github.com/yj-qiu/superpowers-knowledge-capture.git
cd superpowers-knowledge-capture

# 在你的项目中创建输出目录
mkdir -p docs/adr docs/sessions docs/knowledge

# 直接使用模板
cp templates/adr-template.md docs/adr/ADR-001-我的决策.md
```

---

## 工作流

```
输入                            →  输出
specs/（设计文档）               →  ADR（架构决策记录）
plans/（实现计划）               →  TODO.md（待办追踪）
代码变更                        →  docs/knowledge/（领域知识库）
开发过程记忆                    →  docs/sessions/（项目史书）
```

### 何时使用

在以下场景调用 knowledge-capture 技能：
- 头脑风暴或设计会议完成时
- 实现计划完成时
- 开发阶段或里程碑达成时
- 新团队成员需要了解项目上下文时

### 产出物

| 产出物 | 用途 | 模板 |
|--------|------|------|
| ADR | 记录架构决策及其论证过程 | [templates/adr-template.md](./templates/adr-template.md) |
| Session | 记录做了什么和踩了什么坑 | [templates/session-template.md](./templates/session-template.md) |
| Knowledge | 定义领域概念和编码约定 | [templates/knowledge-template.md](./templates/knowledge-template.md) |
| TODO.md | 跟踪后续待办任务 | 从 Session 输出中生成 |

---

## 模板说明

`templates/` 目录提供了三个模板：

- **[adr-template.md](./templates/adr-template.md)** — 用于记录架构决策。每个 ADR 包含：触发上下文、考虑过的选项、最终决策、选择理由和影响。
- **[session-template.md](./templates/session-template.md)** — 用于记录开发过程。聚焦于"做成了什么"和"踩了什么坑"，通过交叉引用关联到 ADR。
- **[knowledge-template.md](./templates/knowledge-template.md)** — 用于定义领域概念、命名规范和架构规则。

---

## 与 Superpowers 的关系

本项目是 **Superpowers** 框架中的一个技能。它是 Superpowers 工作周期的收官之作：

```
brainstorming → writing-plans → implementation → knowledge-capture
```

在 Superpowers 中使用时，AI 助手直接读取 `SKILL.md` 自动执行知识捕获工作流。`templates/` 目录为没有安装 Superpowers 的用户提供了访问同一套产出物模板的独立入口。

---

## Gitee 镜像

本仓库已镜像到 Gitee，方便国内用户访问：

- **GitHub**（主仓库）：`https://github.com/yj-qiu/superpowers-knowledge-capture`
- **Gitee**（镜像）：`https://gitee.com/buming_j/superpowers-knowledge-capture`

Issue 和 PR 请提交到 GitHub。

---

## 许可证

MIT — 详见 [LICENSE](./LICENSE)。
