# skill-self-bootstrap

Retrofit existing OpenClaw skills with **self-bootstrap memory capability**.

This skill upgrades a target skill so it can:
- read `references/LESSONS.md` before execution,
- preserve reusable **Hard Constraints / Common Failure Cases / Best Practices**,
- and continuously improve from prior memory instead of repeating known mistakes.

> In short: this is a **meta skill for skill infrastructure**, not for business task execution.

---

## What this skill does

Given one or more target skills, `skill-self-bootstrap` will typically:

1. Normalize/add a `Skill Memory and Iteration Protocol` section in target `SKILL.md`
2. Create or refresh `references/LESSONS.md`
3. Pull prior signal from memory sources (Mem0 + workspace memory files + target skill docs)
4. Distill findings into reusable lesson categories
5. Keep `SKILL.md` workflow-focused and move corrective memory into `LESSONS.md`

---

## When to use

Use this skill when the user asks for things like:

- “给这个 skill 加自举能力 / 自迭代能力”
- “加错题集 / lessons / best practices”
- “初始化或刷新 `LESSONS.md`”
- “把历史踩坑经验沉淀到 skill 里”
- “让这个 skill 能记住之前错误并避免重复”

Do **not** use it for normal domain work (e.g. data query, design, copywriting). It is specifically for upgrading skill memory architecture.

---

## Repository structure

```text
skill-self-bootstrap/
├── SKILL.md
└── references/
    └── templates.md
```

- `SKILL.md`: the runnable skill instructions
- `references/templates.md`: reusable protocol/LESSONS template snippets

---

## Requirements

From `SKILL.md` compatibility:

- `read`
- `write`
- `edit`
- `exec`
- `memory_search`
- `memory_get`

These are required because the skill must inspect/modify files and retrieve memory evidence.

---

## Install for OpenClaw

### Option A — Local workspace clone (recommended)

From your OpenClaw workspace root:

```bash
git clone https://github.com/Shire31/skill-self-bootstrap.git skills/skill-self-bootstrap
```

Or if directory exists, update:

```bash
cd skills/skill-self-bootstrap
git pull
```

### Option B — Git submodule (for pinned version control)

```bash
git submodule add https://github.com/Shire31/skill-self-bootstrap.git skills/skill-self-bootstrap
git submodule update --init --recursive
```

---

## How agents should invoke this skill

This skill is auto-triggered via `SKILL.md` frontmatter description, but agents can also invoke it intentionally when users request lesson/bootstrap enhancements.

### Typical operator intent examples

- “给 `customer-account-research-feishu` 加自举能力并初始化 lessons”
- “把 `xxx` skill 的历史失败经验整理到 `references/LESSONS.md`”
- “刷新 `yyy` skill 的 protocol + lessons，按最新记忆修正”

---

## Expected output after a successful run

For each target skill, agents should produce:

1. Updated `SKILL.md` with `Skill Memory and Iteration Protocol`
2. Updated `references/LESSONS.md` with reusable entries
3. A short summary including:
   - what changed,
   - where memory was sourced,
   - what was seeded,
   - and any known gaps for next pass

---

## Special case: `skill-creator`

When target is `skill-creator`, this skill should enforce that:

- **newly created skills include self-bootstrap capability by default**, unless user opts out;
- new skills should include protocol block + `references/LESSONS.md` + first-pass lessons initialization.

This turns self-bootstrap into a default factory standard for future skills.

---

## Quick verification checklist

After installation, verify:

- `skills/skill-self-bootstrap/SKILL.md` exists
- `skills/skill-self-bootstrap/references/templates.md` exists
- agent has access to required tools (`memory_search`, `memory_get`, file tools)

Then run a small test prompt:

> “帮我给某个已有 skill 补自举 protocol，并生成 first-pass LESSONS.md”

If target skill files are updated with protocol + lessons structure, installation is valid.

---

## Versioning and updates

Suggested release flow:

```bash
git tag v0.1.0
git push origin main --tags
```

For consumers:

```bash
cd skills/skill-self-bootstrap
git fetch --tags
git checkout v0.1.0
```

---

## License

MIT (see `LICENSE`).
