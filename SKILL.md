---
name: skill-self-bootstrap
description: Give one or more existing skills self-bootstrap capability: make the target skill read `references/LESSONS.md` before execution, preserve hard constraints / failure cases / best practices, and seed or refresh those lessons from Mem0, workspace memory files, and the skill's own documentation. Use this whenever the user asks to give a skill 自举能力, 自迭代能力, 错题集, lessons, best practices, LESSONS.md 初始化, 历史经验迁移, or wants an existing skill to learn from past mistakes, remember corrective knowledge, and keep improving through prior lessons—even if they do not explicitly mention `LESSONS.md`.
compatibility:
  required_tools: ["read", "write", "edit", "exec", "memory_search", "memory_get"]
metadata:
  openclaw:
    emoji: "🧠"
---

# Skill Self Bootstrap

Use this skill to retrofit existing skills with a localized memory system so they can:
- read prior lessons before execution,
- reuse known hard constraints and best practices,
- avoid repeating historical mistakes,
- and initialize or refresh `references/LESSONS.md` from real memory rather than empty boilerplate.

This skill is for **upgrading other skills**, not for doing the target business task itself.

## What this skill owns

This skill helps other skills gain a structured self-improvement loop by:
1. adding or normalizing a `Skill Memory and Iteration Protocol` section in `SKILL.md`
2. creating or updating `references/LESSONS.md`
3. searching long-term and workspace memory for relevant historical knowledge
4. converting that knowledge into reusable `Hard Constraints`, `Common Failure Cases`, and `Best Practices`
5. keeping `SKILL.md` workflow-oriented while moving historical corrective knowledge into `LESSONS.md`

## When to use this skill

Use this skill when the user asks to:
- give a skill 自举能力 / 自迭代能力
- add a 错题集 / best practices / LESSONS.md to a skill
- initialize lessons for one or more skills from prior memory
- migrate historical failures / constraints / best practices out of `SKILL.md`
- make an existing skill remember what went wrong before
- standardize how skills read memory and preserve reusable lessons

Do **not** use this skill for ordinary task execution. Use it only when the job is to upgrade skill infrastructure or skill memory.

## Core principle

`SKILL.md` is the primary workflow interface.
`references/LESSONS.md` is the corrective-memory layer.

That means:
- `SKILL.md` should tell the model **how to do the task**
- `LESSONS.md` should tell the model **what has historically gone wrong, what must not be violated, and what should be preferred based on prior evidence**

Do not collapse these into one giant document.

## Special case: upgrading `skill-creator`

If the target skill is `skill-creator`, do not treat it like an ordinary one-off retrofit.
You are changing the factory that creates future skills.

So the required outcome is stronger:

1. `skill-creator` must explicitly require that **newly created skills include self-bootstrap capability by default** unless the user explicitly opts out.
2. Its creation workflow should instruct the agent to:
   - add a `Skill Memory and Iteration Protocol` block to new skills
   - create `references/LESSONS.md`
   - seed a first-pass lessons file from the current conversation, user corrections, nearby memory, and known pitfalls already visible during skill drafting
3. The rule should be framed as a default creation standard, not a nice-to-have extra.

When upgrading `skill-creator`, verify not only that its own files are changed, but also that its instructions now make future skills inherit this pattern automatically.

## Required outputs

For each target skill, aim to produce:
1. a normalized `Skill Memory and Iteration Protocol` block in `SKILL.md`
2. a non-empty or intentionally empty `references/LESSONS.md`
3. a short operator summary describing:
   - what was added or changed
   - whether memory was found
   - which reusable lessons were seeded
   - what remains unknown

If you modify files, commit the relevant changes.

## Standard workflow

### Step 1 — Identify the target skill set
Determine exactly which skills are being upgraded.

For each target skill, capture:
- skill path
- skill name
- whether `SKILL.md` exists
- whether `references/LESSONS.md` already exists
- whether the user wants initialization, refresh, migration, or cleanup

If the target is ambiguous, resolve that first.

### Step 2 — Detect the target skill's primary language
Match the primary language of the target skill documentation.

Rules:
- if the target `SKILL.md` is mostly English, write the protocol and `LESSONS.md` in English
- if the target `SKILL.md` is mostly Chinese, write them in Chinese
- if the skill is mixed, follow the dominant language of the body, not just trigger keywords
- do not inject a new language that makes the file internally inconsistent

### Step 3 — Normalize the protocol block in `SKILL.md`
Ensure the skill body includes a `Skill Memory and Iteration Protocol` section.

Hard rules:
- put it in the main body of `SKILL.md`, not in frontmatter
- keep it near the top, before detailed workflow instructions
- make it instruct the skill to read `references/LESSONS.md` before execution
- make it instruct the skill to reflect and update lessons after failure or explicit negative feedback

If the protocol already exists, normalize or refine it rather than duplicating it.

### Step 4 — Search memory broadly before writing lessons
Before writing or revising `references/LESSONS.md`, search memory from multiple directions.

Use all three sources where available:

1. **Mem0 / long-term memory**
   - start with the exact skill name
   - then search aliases, endpoint names, domain names, related projects, and key jargon

2. **Workspace memory files**
   - search `memory/*.md`
   - search `MEMORY.md` when appropriate for the session/context
   - search for both exact skill name and operational aliases

3. **The skill's own documentation**
   - inspect `SKILL.md`
   - look for sections like known pitfalls, safety rules, anti-patterns, output contracts, hard rules, and troubleshooting notes

Do not stop after one low-recall search.
If exact-name search is weak, broaden the search with:
- endpoint URLs
- product names
- domain names
- internal SOP labels
- commit-linked phrases
- user-facing trigger phrases

### Step 5 — Convert raw memory into reusable lesson types
Translate retrieved material into one of three buckets:

#### Hard Constraints
Use when the rule is stable and violating it causes real damage.
Examples:
- wrong delivery mode
- wrong protocol/encoding
- violating a canonical routing rule
- presenting inferred data as verified

#### Common Failure Cases
Use when the pattern is a recurring mistake, detour, or rework loop.
Examples:
- retried the wrong blocked path repeatedly
- overused browser too early
- confused draft with sent state
- drifted into the wrong output mode

#### Best Practices
Use when a method has been validated and should usually be preferred.
Examples:
- native-first rendering
- layered evidence escalation
- real-query-first with disclosed fallback
- overview/evidence separation in structured output

### Step 6 — Filter aggressively
Only keep material that is reusable.

Do **not** copy raw conversation history into `LESSONS.md`.
Do **not** include:
- one-off project state
- interpersonal commentary
- temporary logistics
- vague motivational text
- duplicate restatements of the whole `SKILL.md`

A good lesson should feel like a reusable operational correction.

### Step 7 — Seed or refresh `references/LESSONS.md`
Use this default structure unless the user wants a different schema:
- `How to Use This File`
- `Hard Constraints`
- `Common Failure Cases`
- `Best Practices`
- `Update Rules`
- `Maintenance Notes`

When seeding a new file:
- prefer a few strong entries over many weak entries
- it is acceptable to leave a section short if evidence is thin
- do not invent lessons just to make sections look full

When refreshing an existing file:
- merge duplicates
- tighten vague wording
- promote repeated notes into stronger reusable rules
- preserve good existing entries unless they are obsolete or redundant

### Step 8 — Keep `SKILL.md` and `LESSONS.md` cleanly separated
If the target `SKILL.md` contains large historical pitfall sections, consider moving or compressing them after seeding `LESSONS.md`.

Use this rule:
- workflow and active operating instructions stay in `SKILL.md`
- historical corrective knowledge and stable lessons belong in `LESSONS.md`

Do not remove essential workflow instructions just because similar ideas now exist in lessons.
The goal is cleaner separation, not destructive slimming.

### Step 9 — Report what was actually found
When you finish, say:
- which memory sources were searched
- whether useful prior memory was found
- which lessons were added
- which skills had thin memory and therefore lighter lessons

Be explicit if the initialization is only a first pass.

### Step 10 — Commit if files changed
If you edited workspace files, commit the relevant changes with a clear message.

Good commit examples:
- `Add memory bootstrap support to five skills`
- `Seed reusable lessons for account-research and Feishu-card skills`
- `Normalize skill lessons protocol for data-access skills`

## Search playbook

When exact-name search is weak, expand your query set.

For a target skill, search combinations like:
- exact skill name
- abbreviated skill name
- main endpoint URL
- product/vendor name
- major workflow labels
- common user request phrases
- known failure terms like `Cloudflare`, `double-encoded`, `native-first`, `verified/probable/unknown`

Example categories:
- **API skill** → endpoint URL, HTTP method, header requirements, payload quirks
- **card skill** → JSON v2, native table, image_key, send vs draft, schema-safe
- **research skill** → SOP labels, evidence grading, power map, procurement chain
- **warehouse skill** → table names, query adapter, business guide, read-only rule, type limitations

## Quality bar for generated lessons

A strong `LESSONS.md` should:
- make the target skill safer and sharper immediately
- preserve prior corrections without bloating
- reflect real historical evidence
- reduce future detours
- stay shorter and more operational than a long narrative memo

A weak `LESSONS.md`:
- repeats the whole skill
- contains generic “be careful” filler
- stores raw logs
- invents lessons not supported by history
- mixes current workflow with historical correction in a confusing way

## Anti-patterns

Avoid these mistakes:
- inserting the protocol into frontmatter instead of body
- adding duplicate protocol blocks
- writing lessons in a different language from the skill's main language
- stopping after one memory search query
- copying entire memory entries verbatim into lessons
- turning `LESSONS.md` into a second `SKILL.md`
- leaving obviously reusable historical mistakes trapped inside `SKILL.md`
- committing unrelated workspace changes together

## Minimal completion checklist

Before you finish, confirm:
1. Did I identify the exact target skill(s)?
2. Did I match the target skill's primary language?
3. Did I search both Mem0 and workspace memory files?
4. Did I inspect the skill's own documentation for embedded lessons?
5. Did I convert findings into reusable constraints / failures / best practices?
6. Did I avoid raw-log bloat?
7. Did I commit the relevant file changes?

## Minimal example

Use this pattern when upgrading an existing skill.

### Example request
> Give `feishu-card-advanced` self-bootstrap capability. Add the protocol block, create or refresh `references/LESSONS.md`, search prior memory, and seed reusable hard constraints / failure cases / best practices.

### Expected execution pattern
1. Read `skills/feishu-card-advanced/SKILL.md`
2. Check whether `references/LESSONS.md` already exists
3. Search memory using:
   - exact skill name: `feishu-card-advanced`
   - aliases / concepts: `Feishu card JSON v2`, `native-first`, `table-first`, `image_key`, `send vs draft`
   - workspace memory files and skill-local notes
4. Normalize the protocol block in `SKILL.md`
5. Seed or refresh `references/LESSONS.md`
6. Report what memory was found and what lessons were added
7. Commit the relevant file changes

### Expected lesson shape
A good first pass should usually produce entries like:
- `Hard Constraints`:
  - native-first rendering is mandatory
  - send mode and draft mode must not be blurred
- `Common Failure Cases`:
  - misreading “one main focus” as “only one component allowed”
  - under-specifying table-first / column-first patterns
- `Best Practices`:
  - use overview vs evidence separation
  - harden delivery mechanics, not just visual design

The exact content will vary by target skill, but the structure should stay stable.

## Suggested final summary format

Use this structure when reporting back:

### Updated skills
- `skill-name` — protocol inserted/normalized; lessons seeded/refreshed

### Memory sources searched
- Mem0 search queries
- workspace memory files searched
- skill-local files inspected

### Seeded lesson themes
- hard constraints:
- failure cases:
- best practices:

### Gaps / next pass
- where memory was thin
- where `SKILL.md` still contains historical material worth slimming later
