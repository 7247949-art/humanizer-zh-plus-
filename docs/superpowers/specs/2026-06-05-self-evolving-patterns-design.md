# Self-Evolving Patterns Design

## Context

`humanizer-zh-plus` is a document-only skill package. Its current core is `SKILL.md`, which defines 34 AI-writing patterns for Chinese rewriting. The project has no runtime code, tests, or data store. The self-evolution feature should therefore start as a lightweight, auditable documentation workflow instead of an automated rule generator.

## Goal

Add a semi-automatic evolution loop for two kinds of learning:

- Rule evolution: when a new recurring AI-flavored phrase, sentence pattern, or rhythm is discovered, record it as a candidate Pattern.
- Case evolution: preserve "original text -> rewritten text -> review notes" examples so future edits become more stable and evidence-based.

Candidates are accumulated automatically during post-rewrite review, but they are not promoted into `SKILL.md` until they meet evidence thresholds and receive human approval.

## Non-Goals

- Do not build a full application, database, or background agent.
- Do not let the skill modify formal Patterns without human confirmation.
- Do not treat every awkward sentence as a new Pattern.
- Do not replace the existing 34 Pattern system; extend it cautiously.

## Recommended Approach

Use a mixed Markdown plus YAML-front-matter design.

Markdown keeps the evolution records readable for writers and maintainers. YAML front matter keeps candidate status, thresholds, counts, and linked examples easy to inspect or automate later.

## Directory Structure

Add an `evolution/` directory:

```text
evolution/
├── README.md
├── candidates/
│   └── pattern-035-xxx.md
├── examples/
│   └── 2026-06-05-xxx.md
└── review-log.md
```

Responsibilities:

- `evolution/README.md`: explains the semi-automatic evolution workflow.
- `evolution/candidates/`: stores one candidate Pattern per Markdown file.
- `evolution/examples/`: stores one rewrite case per Markdown file.
- `evolution/review-log.md`: records merge, rejection, delay, and consolidation decisions.

Candidate observations must live in `evolution/` first. `SKILL.md` is only updated after review.

## Candidate Pattern Template

Each candidate file uses this shape:

```markdown
---
id: pattern-035
title: ""
status: observing
occurrences: 1
example_count: 1
merge_threshold:
  occurrences: 3
  examples: 2
first_seen: 2026-06-05
last_seen: 2026-06-05
related_examples:
  - 2026-06-05-xxx
---

# Pattern 35:

## 识别方法

## 常见触发词/结构

## 为什么像 AI 写的

## 改写原则

## 观察记录

## 是否建议合并
```

Allowed statuses:

- `observing`: evidence is still being collected.
- `ready_for_review`: the candidate reached the merge threshold.
- `merged`: the candidate was promoted into `SKILL.md`.
- `rejected`: the candidate was reviewed and rejected as a stable Pattern.
- `merged_into_existing`: the candidate was judged to be a variant of an existing Pattern.

## Rewrite Example Template

Each example file uses this shape:

```markdown
---
id: 2026-06-05-xxx
related_candidates:
  - pattern-035
source_type: article
tone: platform-natural
created_at: 2026-06-05
---

# 案例：xxx

## 原文

## 改写后

## 复盘

## 新发现的 AI 味

## 可复用改写策略
```

Examples should preserve enough context to explain why a candidate exists. They do not need to store full long articles if a representative excerpt is enough.

## Evolution Workflow

After each Chinese rewrite task:

1. Finish the user-facing rewrite first.
2. Compare the source text and final rewrite against the 34 formal Patterns and existing candidates.
3. Add a new example under `evolution/examples/`.
4. If a new AI-writing smell is found, either create a candidate or update an existing one.
5. For an existing candidate, update `occurrences`, `example_count`, `last_seen`, and `related_examples`.
6. When `occurrences >= 3` and `example_count >= 2`, set `status: ready_for_review`.
7. Ask the human maintainer whether to promote the candidate.
8. Only after approval, add the new Pattern to `SKILL.md` using the next Pattern number.
9. Record the decision in `evolution/review-log.md`.

## Merge Rules

A candidate may become a formal Pattern only if it passes all five checks:

1. Reproducible: appears in at least 3 independent texts.
2. Nameable: can be summarized with a clear Pattern name.
3. Recognizable: has stable trigger words, structures, rhythm, or behavior.
4. Rewriteable: has a concrete rewrite principle.
5. Non-duplicative: is not just a variant of an existing Pattern.

If the candidate fails these checks, mark it as `observing`, `rejected`, or `merged_into_existing`.

## Review Log Template

`evolution/review-log.md` entries use this shape:

```markdown
## 2026-06-05 pattern-035

Decision: merged / rejected / observing / merged_into_existing

Reason:

Evidence:

Next action:
```

The log should explain why the decision was made, not just record the result.

## Skill Updates

`SKILL.md` should gain a short "自我进化流程" section. The section should instruct the assistant to:

- perform a short evolution review after rewrite tasks,
- maintain candidates and examples in `evolution/`,
- avoid direct formal Pattern changes without human approval,
- suggest review when a candidate reaches the threshold.

Formal Pattern additions should continue the current numbering: Pattern 35, Pattern 36, and so on.

## Guardrails

The rule library should not grow for its own sake. New Patterns should improve recognition and rewriting quality. If a candidate overlaps an existing Pattern, add it as an example to the existing Pattern instead of creating a new formal rule.

After every 5 newly merged formal Patterns, maintainers should run a small consolidation review:

- merge overlapping Patterns,
- remove weak rules,
- strengthen examples,
- check that the Pattern list remains usable during real rewriting.

## Success Criteria

- The repository has a clear `evolution/` workflow.
- New AI-writing smells can be captured without immediately changing `SKILL.md`.
- Candidate promotion is evidence-based and human-approved.
- Rewrite examples become reusable learning material.
- The system can later support scripts for counting, status checks, and review reminders without changing the document model.
