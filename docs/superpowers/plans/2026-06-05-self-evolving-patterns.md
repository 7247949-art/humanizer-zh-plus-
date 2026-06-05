# Self-Evolving Patterns Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add a semi-automatic rule and example evolution workflow to `humanizer-zh-plus`.

**Architecture:** Keep `SKILL.md` as the formal rule source, and add an `evolution/` documentation layer for candidates, examples, and review decisions. Use Markdown files with YAML front matter so humans can read records and future scripts can count thresholds.

**Tech Stack:** Markdown, YAML front matter, Git, shell verification with `rg`, `find`, and Ruby YAML parsing.

---

## File Structure

- Create `evolution/README.md`: explains the semi-automatic evolution workflow, thresholds, statuses, and merge guardrails.
- Create `evolution/candidates/_template.md`: reusable candidate Pattern template with YAML front matter.
- Create `evolution/examples/_template.md`: reusable rewrite example template with YAML front matter.
- Create `evolution/review-log.md`: review decision log with the accepted decision template.
- Modify `SKILL.md`: add a "自我进化流程" section that tells the assistant how to maintain `evolution/` after rewrite tasks.
- Modify `README.md`: document the new self-evolution capability and update the file tree.
- Keep `docs/superpowers/specs/2026-06-05-self-evolving-patterns-design.md`: already written design spec; do not modify unless the implementation uncovers a contradiction.

---

### Task 1: Add Evolution Directory And Templates

**Files:**
- Create: `evolution/README.md`
- Create: `evolution/candidates/_template.md`
- Create: `evolution/examples/_template.md`
- Create: `evolution/review-log.md`

- [ ] **Step 1: Create the evolution directories**

Run:

```bash
mkdir -p evolution/candidates evolution/examples
```

Expected: command exits with code 0.

- [ ] **Step 2: Add `evolution/README.md`**

Create `evolution/README.md` with this content:

````markdown
# 自我进化工作区

这里记录 `humanizer-zh-plus` 在真实改写中发现的新 AI 写作痕迹。

正式 Pattern 仍以 `SKILL.md` 为准。这里的内容只用于观察、积累证据和等待人工审核。

## 进化原则

- 先服务当前改写，再做复盘记录。
- 候选 Pattern 自动积累，正式 Pattern 人工确认。
- 新规则必须来自多个案例，不靠单次感觉。
- 能并入现有 Pattern 的，不新增编号。
- 规则库宁可慢一点，也不要长歪。

## 工作流

1. 完成中文文本改写。
2. 对照 `SKILL.md` 的 34 个正式 Pattern 和 `evolution/candidates/` 的候选 Pattern。
3. 在 `evolution/examples/` 记录一条案例。
4. 如果发现新的稳定 AI 味句式，创建或更新候选 Pattern。
5. 候选达到 `occurrences >= 3` 且 `example_count >= 2` 时，将状态改为 `ready_for_review`。
6. 维护者确认后，才把候选升级进 `SKILL.md`。
7. 每次合并、拒绝或延后，都写入 `evolution/review-log.md`。

## 候选状态

- `observing`：还在观察，证据不足。
- `ready_for_review`：达到合并门槛，等待维护者审核。
- `merged`：已经升级为正式 Pattern。
- `rejected`：确认不是稳定 Pattern。
- `merged_into_existing`：并入已有 Pattern，不新增编号。

## 合并门槛

候选 Pattern 必须同时满足：

- 至少 3 次独立出现。
- 至少 2 个改写案例。
- 能清楚命名。
- 有稳定触发词、句式、结构或节奏特征。
- 有明确改写原则。
- 不与现有 Pattern 重复。

## 文件命名

候选 Pattern：

```text
evolution/candidates/pattern-035-short-name.md
```

改写案例：

```text
evolution/examples/2026-06-05-short-name.md
```

命名用英文小写短横线，内容可以写中文。
````

- [ ] **Step 3: Add the candidate template**

Create `evolution/candidates/_template.md` with this content:

```markdown
---
id: pattern-035
title: ""
status: observing
occurrences: 1
example_count: 1
merge_threshold:
  occurrences: 3
  example_count: 2
first_seen: 2026-06-05
last_seen: 2026-06-05
related_examples:
  - 2026-06-05-example
---

# Pattern 35：

## 识别方法

写清楚如何判断它出现了。不要只写“读起来像 AI”。

## 常见触发词/结构

- 待补充

## 为什么像 AI 写的

说明它为什么不像自然中文写作。

## 改写原则

说明遇到这类句式时应该怎么改。

## 观察记录

- 2026-06-05：第一次观察到，关联案例 `2026-06-05-example`。

## 是否建议合并

当前状态：`observing`。
```

- [ ] **Step 4: Add the rewrite example template**

Create `evolution/examples/_template.md` with this content:

```markdown
---
id: 2026-06-05-example
related_candidates:
  - pattern-035
source_type: article
tone: platform-natural
created_at: 2026-06-05
---

# 案例：示例标题

## 原文

粘贴能代表问题的原文片段。

## 改写后

粘贴最终采用的改写版本。

## 复盘

说明这次改写主要处理了哪些 AI 痕迹。

## 新发现的 AI 味

说明是否出现了正式 Pattern 之外的新句式。

## 可复用改写策略

总结下次遇到同类问题时可以复用的处理方式。
```

- [ ] **Step 5: Add the review log**

Create `evolution/review-log.md` with this content:

````markdown
# Pattern 审核记录

这里记录候选 Pattern 的合并、拒绝、延后观察和并入已有规则的决定。

## 记录格式

```text
## 2026-06-05 pattern-035

Decision: merged / rejected / observing / merged_into_existing

Reason:

Evidence:

Next action:
```
````

- [ ] **Step 6: Verify the files exist**

Run:

```bash
find evolution -maxdepth 3 -type f | sort
```

Expected output includes:

```text
evolution/README.md
evolution/candidates/_template.md
evolution/examples/_template.md
evolution/review-log.md
```

- [ ] **Step 7: Verify YAML front matter parses**

Run:

```bash
ruby -ryaml -e 'Dir["evolution/{candidates,examples}/*.md"].each { |path| text = File.read(path); fm = text[/\A---\n(.*?)\n---/m, 1]; raise "missing front matter: #{path}" unless fm; YAML.safe_load(fm, permitted_classes: [Date]); puts "#{path}: ok" }'
```

Expected output:

```text
evolution/candidates/_template.md: ok
evolution/examples/_template.md: ok
```

- [ ] **Step 8: Commit Task 1**

Run:

```bash
git add evolution
git commit -m "feat: add evolution workspace templates"
```

Expected: commit succeeds.

---

### Task 2: Add The Self-Evolution Workflow To The Skill

**Files:**
- Modify: `SKILL.md`

- [ ] **Step 1: Insert the self-evolution section**

In `SKILL.md`, insert this section after the "基本流程（10 步）" list and before "五大核心原则":

```markdown
---

## 自我进化流程

完成中文改写任务后，执行一次轻量复盘，用于积累规则和案例。

### 复盘顺序

1. **先完成用户任务** — 不要为了记录案例打断当前改写。
2. **对照正式 Pattern** — 先判断问题是否已属于 34 个正式 Pattern。
3. **对照候选 Pattern** — 再检查 `evolution/candidates/` 是否已有相似候选。
4. **记录案例** — 将有代表性的"原文 -> 改写后 -> 复盘"写入 `evolution/examples/`。
5. **更新候选** — 如果发现正式 Pattern 之外的新 AI 味，创建或更新候选 Pattern。
6. **检查门槛** — 当候选达到 3 次独立出现且至少 2 个案例，将状态改为 `ready_for_review`。
7. **等待确认** — 只有维护者确认后，才能把候选升级为正式 Pattern 35、36……

### 候选合并标准

候选 Pattern 必须同时满足：

- 可复现：至少 3 次独立出现。
- 可命名：能用一个清楚名称概括。
- 可识别：有稳定触发词、句式、结构或节奏特征。
- 可改写：有明确改写原则。
- 不重复：不是现有 Pattern 的轻微变体。

### 记录边界

- 如果只是现有 Pattern 的新例子，补充案例，不新增候选。
- 如果候选证据不足，保持 `observing`。
- 如果达到门槛，在回复中提醒维护者审核，不要自行合并。
- 每次合并、拒绝、延后或并入已有规则，都写入 `evolution/review-log.md`。
```

- [ ] **Step 2: Extend the output format**

In `SKILL.md`, under "输出格式", replace the current numbered list with:

```markdown
1. **改写后的文字**（如来自文件，展示具体修改的 diff 或关键段落）
2. **"哪里还像 AI 写的？"** — 简短列举剩余的 AI 痕迹
3. **最终版本** — 经过再次改写后的版本
4. **进化提示**（可选）— 如果发现新候选或候选达到审核门槛，提醒维护者
5. **改动摘要**（可选，如改动较大）
```

- [ ] **Step 3: Verify the workflow text is present**

Run:

```bash
rg -n "自我进化流程|ready_for_review|evolution/examples|进化提示" SKILL.md
```

Expected: each searched phrase appears at least once.

- [ ] **Step 4: Verify the skill front matter still parses**

Run:

```bash
ruby -ryaml -e 'text = File.read("SKILL.md"); fm = text[/\A---\n(.*?)\n---/m, 1]; data = YAML.safe_load(fm); puts data.fetch("name"); puts data.fetch("version")'
```

Expected output:

```text
humanizer-zh-plus
1.0.0
```

- [ ] **Step 5: Commit Task 2**

Run:

```bash
git add SKILL.md
git commit -m "feat: add skill self-evolution workflow"
```

Expected: commit succeeds.

---

### Task 3: Document The Feature In README

**Files:**
- Modify: `README.md`

- [ ] **Step 1: Add a feature section**

In `README.md`, after the "中文特有 Pattern 说明" table and before "安装", insert:

```markdown
### 半自动自我进化

本项目支持轻量的规则进化与案例进化：

- **规则进化**：发现新的 AI 味句式后，先记录为候选 Pattern。
- **案例进化**：保存"原文 -> 改写 -> 复盘"，让后续规则有证据。
- **人工合并**：候选达到 3 次独立出现且至少 2 个案例后，才建议升级为正式 Pattern。

候选和案例存放在 `evolution/` 目录，正式规则仍以 `SKILL.md` 为准。

```

- [ ] **Step 2: Update the file tree**

Replace the current file tree with:

````markdown
```text
humanizer-zh-plus/
├── SKILL.md                         # 技能定义文件（34种Pattern完整清单）
├── README.md                        # 项目说明
├── LICENSE                          # MIT License
├── references/
│   └── chinese-patterns.md          # 5种中文特有Pattern详解
└── evolution/
    ├── README.md                    # 自我进化流程说明
    ├── candidates/
    │   └── _template.md             # 候选Pattern模板
    ├── examples/
    │   └── _template.md             # 改写案例模板
    └── review-log.md                # Pattern审核记录
```
````

- [ ] **Step 3: Add a version note**

Under "版本历史", add this entry above v1.0.0:

```markdown
### v1.1.0（未发布）
- 增加半自动自我进化工作区
- 增加候选 Pattern 与改写案例模板
- 增加候选达到门槛后的人工审核流程
```

- [ ] **Step 4: Verify README references the new workflow**

Run:

```bash
rg -n "半自动自我进化|evolution/|v1.1.0|references/" README.md
```

Expected: all phrases appear.

- [ ] **Step 5: Commit Task 3**

Run:

```bash
git add README.md
git commit -m "docs: document self-evolution workflow"
```

Expected: commit succeeds.

---

### Task 4: Final Verification

**Files:**
- Inspect: `README.md`
- Inspect: `SKILL.md`
- Inspect: `evolution/README.md`
- Inspect: `evolution/candidates/_template.md`
- Inspect: `evolution/examples/_template.md`
- Inspect: `evolution/review-log.md`

- [ ] **Step 1: Check repository status**

Run:

```bash
git status --short --branch
```

Expected: clean working tree, branch ahead of origin by the new commits.

- [ ] **Step 2: Check all expected files**

Run:

```bash
find evolution docs/superpowers -maxdepth 4 -type f | sort
```

Expected output includes the design spec, implementation plan, and all four `evolution/` files.

- [ ] **Step 3: Parse all YAML front matter**

Run:

```bash
ruby -ryaml -e 'files = ["SKILL.md"] + Dir["evolution/{candidates,examples}/*.md"]; files.each { |path| text = File.read(path); fm = text[/\A---\n(.*?)\n---/m, 1]; raise "missing front matter: #{path}" unless fm; YAML.safe_load(fm, permitted_classes: [Date]); puts "#{path}: ok" }'
```

Expected output:

```text
SKILL.md: ok
evolution/candidates/_template.md: ok
evolution/examples/_template.md: ok
```

- [ ] **Step 4: Check required workflow terms**

Run:

```bash
rg -n "自我进化流程|ready_for_review|occurrences >= 3|example_count >= 2|merged_into_existing|进化提示|半自动自我进化" SKILL.md README.md evolution
```

Expected: each term appears in at least one relevant file.

- [ ] **Step 5: Review the final diff summary**

Run:

```bash
git log --oneline -n 5
git diff origin/main...HEAD --stat
```

Expected: shows the design commit plus implementation commits, with changes limited to docs, `SKILL.md`, `README.md`, and `evolution/`.

---

## Self-Review Checklist

- Spec coverage: Task 1 implements `evolution/`, templates, statuses, thresholds, and review log. Task 2 implements `SKILL.md` workflow and review reminder. Task 3 implements user-facing docs. Task 4 verifies the document model and final state.
- Placeholder scan: no task relies on deferred placeholder wording; all new file contents and inserted sections are specified.
- Type consistency: candidate statuses are consistent across design, templates, skill workflow, and review log.
