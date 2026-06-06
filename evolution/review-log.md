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

## 2026-06-06 pattern-035..039

Decision: observing

Reason:

用户反馈改写后仍缺少明确人工创作痕迹。初步判断这不是单个词或句式问题，而是一组更深的写作过程缺失：无作者现场、结论过度完成、证据链不透明、细节贫血、过度工整正确感。

Evidence:

- 候选 Pattern：`pattern-035` 到 `pattern-039`
- 关联案例：`2026-06-06-human-authorship-traces`

Next action:

继续在真实改写中记录独立出现。任一候选达到 `occurrences >= 3` 且 `example_count >= 2` 后，再进入人工审核。
