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

## Overview

Extract valuable information from temporary workflow artifacts (brainstorming specs, writing-plans plans, and development session memory) into the project's permanent record system.

```
Input → Output
{specs_dir} (design documents)          →  ADR (Architecture Decision Records)
{plans_dir} (implementation plans)      →  TODO.md (task tracking)
code changes                            →  {knowledge_dir} (domain knowledge)
development session memory              →  {sessions_dir} (project history)
```

## Prerequisites

This skill assumes the following upstream workflows have been completed in order:
1. **brainstorming** — produces design documents (written to {specs_dir})
2. **writing-plans** — produces implementation plans (written to {plans_dir}, default `docs/superpowers/plans/`)
3. **implementation** — produces code changes

## Core Principles

- **Do not modify original specs/plans** — they are local working files; extract information and leave them untouched
- **No duplicate recording** — key rationale for design decisions goes into ADR only; sessions do not repeat it
- **All links must work** — verify cross-references
- **Paths are configurable** — adjust output directories via `variables` in YAML front matter

## Execution Steps

### Step 1: Extract ADRs

Scan design documents in `{specs_dir}` to identify key decision points.

**Each key decision point must satisfy all of**:
- At least 2 viable options were explicitly compared
- The decision constrains future development
- It is not an implementation detail (e.g., "for vs while" does not count)

Save each ADR as `{adr_dir}/ADR-XXX-{short-title}.md`. Format: see [templates/adr-template.md](./templates/adr-template.md).

### Step 2: Update Knowledge Base

Extract new domain concepts from design documents and implementation code. Write to `{knowledge_dir}`.

**Typical content**: DSL syntax specification, DDD architecture conventions, module dependency rules, key term definitions, naming conventions.

Format: see [templates/knowledge-template.md](./templates/knowledge-template.md).

### Step 3: Write Session

Create a new project history record in `{sessions_dir}` (sequence number = current max + 1). Record only "what was accomplished" and "lessons learned". Point design rationale to ADRs.

Format: see [templates/session-template.md](./templates/session-template.md).

### Step 4: Update TODO.md

Aggregate TODOs generated during the session into `{todo_file}`, grouped by module/priority. For existing TODOs, do incremental updates: add new ones with ⏳, mark completed with ✅.

### Step 5: Cross-reference Check

- Session → ADR (key decision field in session header)
- ADR → Source Spec (ADR's "source" field)
- Knowledge → ADR/Session (knowledge's "related references" field)

### Step 6: Commit

Check if the current directory is a git repository. If yes, execute:

```bash
git add {adr_dir}/ {sessions_dir}/ {knowledge_dir}/ {todo_file}
git commit -m "docs: knowledge capture - {description}"
```

If not in a git repository, prompt the user to manually set up version control.

## Path Configuration

All paths are configured via the `variables` field in the YAML front matter of SKILL.md. Superpowers users can use the defaults directly; non-Superpowers users can modify path variables to match their project structure.

## Common Mistakes

| Mistake | Consequence | Correct Approach |
|---------|------------|------------------|
| Repeating ADR content in sessions | Multiple maintenance points, inconsistent info | Sessions only narrate; ADRs only decide |
| Modifying specs/plans working files | Workflow history lost | Leave specs/plans untouched; extract to permanent system |
| Writing sessions without ADRs | Decision rationale becomes untraceable | Extract every decision with option comparison into ADR |
| ADR missing "rejected options" | Unknown why option B was rejected | Clearly record why each option was rejected |
| Forgetting to update TODO.md | TODOs sink and no one follows up | Force-update TODO.md every time |
