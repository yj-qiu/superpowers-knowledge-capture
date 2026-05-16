# Knowledge Capture

> A knowledge persistence skill for the **Superpowers** ecosystem.
> Superpowers 生态的知识持久化技能

Extract valuable information from temporary workflow artifacts (design specs, implementation plans, development session memory) into the project's permanent record system: ADR, knowledge base, session history, and TODO tracking.

将临时性工作流产物中的有价值信息提取到项目的持久化记录体系：架构决策记录（ADR）、领域知识库、项目史书和待办追踪。

---

## Prerequisites / 前提条件

- **Superpowers users**: This skill requires [Superpowers](https://github.com/yj-qiu/superpowers) skill framework. Clone this repo into your skills directory.
- **Standalone users**: No framework needed. Use the templates directly with your own directory structure.

---

## Quick Start / 快速使用

### As a Superpowers skill

```bash
# Clone into your Superpowers skills directory
cd your-project/skills/
git clone https://github.com/yj-qiu/superpowers-knowledge-capture.git knowledge-capture
```

Then invoke the skill at the end of a work cycle:
> "Use knowledge-capture to persist the design decisions from this brainstorming session."

### Standalone usage

```bash
# Clone anywhere
git clone https://github.com/yj-qiu/superpowers-knowledge-capture.git
cd superpowers-knowledge-capture

# Create the output directories in your project
mkdir -p docs/adr docs/sessions docs/knowledge

# Use templates manually
cp templates/adr-template.md docs/adr/ADR-001-my-decision.md
```

---

## Workflow / 工作流

```
Input                            →  Output
specs/ (design documents)        →  ADR (Architecture Decision Records)
plans/ (implementation plans)    →  TODO.md (task tracking)
code changes                     →  docs/knowledge/ (domain knowledge)
development session memory       →  docs/sessions/ (project history)
```

### When to use

Use the knowledge-capture skill when:
- A brainstorming or design session completes
- An implementation plan is finished
- A development phase or milestone is reached
- New team members need onboarding context

### What it produces

| Artifact | Purpose | Template |
|----------|---------|----------|
| ADR | Record architecture decisions with rationale | [templates/adr-template.md](./templates/adr-template.md) |
| Session | Narrate what was done and lessons learned | [templates/session-template.md](./templates/session-template.md) |
| Knowledge | Define domain concepts and conventions | [templates/knowledge-template.md](./templates/knowledge-template.md) |
| TODO.md | Track follow-up tasks | Generated from session output |

---

## Templates / 模板说明

Three templates are provided in the `templates/` directory:

- **[adr-template.md](./templates/adr-template.md)** — For documenting architecture decisions. Each ADR captures the context, options considered, the decision, rationale, and impact.
- **[session-template.md](./templates/session-template.md)** — For recording development sessions. Focuses on outcomes and lessons learned, with cross-references to ADRs.
- **[knowledge-template.md](./templates/knowledge-template.md)** — For defining domain concepts, naming conventions, and architectural rules.

---

## Relationship with Superpowers / 与 Superpowers 的关系

This project is a skill within the **Superpowers** framework. It is designed to be the final step in a Superpowers work cycle:

```
brainstorming → writing-plans → implementation → knowledge-capture
```

When used within Superpowers, the SKILL.md file is read by the AI assistant to automatically execute the knowledge capture workflow. The templates directory provides standalone access to the same artifacts for non-Superpowers users.

---

## Mirror Repository / 镜像仓库

This repository is available on both GitHub and Gitee:

- **GitHub**: `https://github.com/yj-qiu/superpowers-knowledge-capture`
- **Gitee**: `https://gitee.com/buming_j/superpowers-knowledge-capture`

---

## License / 许可证

MIT — see [LICENSE](./LICENSE).
