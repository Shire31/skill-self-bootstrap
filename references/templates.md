# Skill Memory Bootstrapper Templates

This file contains the canonical shapes used by `skill-self-bootstrap`.
Adapt wording to the target skill's primary language.

---

## Protocol block template (English)

```md
## Skill Memory and Iteration Protocol

This skill is paired with `references/LESSONS.md`.
That file stores this skill's recurring failure cases, hard constraints, and validated best practices.

### Before execution
Before using this skill, read `references/LESSONS.md` and focus on:

- `Hard Constraints`: rules that must not be violated
- `Common Failure Cases`: recurring mistakes, detours, and misjudgments from prior runs
- `Best Practices`: validated approaches that should be preferred by default

If the file does not exist yet, follow the main skill workflow first, then decide after the task whether the lessons file should be initialized or expanded.

### During execution
Actively use `references/LESSONS.md` while working so you avoid repeating known mistakes rather than only reviewing it after failure.

If this execution reveals any of the following, and `references/LESSONS.md` does not already cover it, add it after the task:

- a clear failure, rework loop, misjudgment, or avoidable detour
- a newly discovered boundary condition that materially affects result quality
- a stable, reusable best practice that is better than the old default

Do not dump one-off noise, incidental details, or raw task logs into the lessons file.

### After user feedback
If the user clearly says the result is bad, incorrect, or not aligned with expectations, do a short reflection and check whether `references/LESSONS.md` should be updated.

At minimum, answer:

1. What was the root cause?
2. Was the failure caused by misunderstanding, execution error, or missed boundary conditions?
3. How should the same issue be detected and avoided earlier next time?
4. Does this lesson have reuse value across future tasks?

If the answer has reuse value, record it in `references/LESSONS.md`.

### Update principles
When updating `references/LESSONS.md`, follow these rules:

- record only reusable, generalizable lessons
- prefer merging or rewriting existing entries instead of piling up duplicates
- write lessons in the form of “scenario + risk/problem + correct approach + scope/boundary”
- do not record sensitive data, irrelevant detail, emotional commentary, or unverified guesses
- `LESSONS.md` is for distilled experience, not task logging

### Goal
The purpose of this mechanism is to help the skill reduce repeat mistakes, reduce avoidable detours, and steadily reuse methods that have already been validated.
```

---

## LESSONS.md skeleton (English)

```md
# LESSONS.md

> This is the failure-case and best-practices file for this skill.
> The goal is to reduce repeated mistakes and preserve reusable experience, not to keep a running log.

## 1. How to Use This File
## 2. Hard Constraints
## 3. Common Failure Cases
## 4. Best Practices
## 5. Update Rules
## 6. Maintenance Notes
```

---

## Minimal worked example

Target request:
- “Give `customer-account-research-feishu` self-bootstrap capability and initialize its lessons from prior memory.”

Good first-pass outcome:
- protocol block exists near the top of `SKILL.md`
- `references/LESSONS.md` exists and is non-empty
- memory search covers:
  - exact skill name
  - aliases like `account research`, `Power Map`, `procurement chain`, `verified / probable / unknown`
  - workspace memory files that mention prior Singer-style research lessons
- resulting lesson types include:
  - `Hard Constraints`: do not present inferred contact details as verified facts
  - `Common Failure Cases`: drift into generic company intro; return raw card JSON as normal text
  - `Best Practices`: keep the fixed outreach-intelligence skeleton; grade evidence strength explicitly

---

## Special case example: updating `skill-creator`

Target request:
- “Modify `skill-creator` so every new skill it creates includes self-bootstrap capability by default.”

Good first-pass outcome:
- `skill-creator` explicitly states that newly created skills should normally include:
  - a `Skill Memory and Iteration Protocol` block
  - a `references/LESSONS.md` file
  - a first-pass lessons initialization
- the instruction is framed as a default creation standard, not an optional enhancement
- `skill-self-bootstrap` itself documents this as a special-case upgrade path when the target skill is `skill-creator`

What to check after editing:
- can another agent read `skill-creator` and unambiguously understand that new skills must ship with self-bootstrap support?
- does the wording specify where lessons come from for the initial seed?
- is the rule scoped to **newly created skills by default** rather than all skills everywhere?

---

## Extraction rule of thumb

When migrating memory into lessons:
- a stable must-not-break rule → `Hard Constraints`
- a repeated mistake or avoidable detour → `Common Failure Cases`
- a reusable preferred method → `Best Practices`

If an item is only project state, temporary logistics, or conversation residue, do not keep it.
