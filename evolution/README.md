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
