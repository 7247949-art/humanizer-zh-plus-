# humanizer-zh-pro

**中文文本去 AI 味增强 Skill。**

`humanizer-zh-pro` 用 34 种 AI 写作 Pattern 扫描中文文本，并通过半自动自我进化机制持续沉淀新的候选 Pattern 和改写案例。它适合用在公众号、博客、企业文档、产品说明、知识文章和其他中文长文本改写场景。

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![humanizer](https://img.shields.io/badge/based%20on-humanizer%202.5.1-blue.svg)](https://github.com/blader/humanizer)
[![version](https://img.shields.io/badge/version-1.1.0-blue.svg)](SKILL.md)

---

## 项目定位

这个项目不是一个普通的命令行工具，也不是 npm/Python 包。它是一个可以被支持 Skills 的 AI 助手加载的写作技能包。

它做三件事：

- **识别 AI 味**：用 34 种 Pattern 检查模板腔、翻译腔、公文腔、机械排比、套路结尾等问题。
- **改写中文表达**：保留原意，但让句子更像真实中文作者写出来的。
- **积累新规则**：把新发现的 AI 味句式先记录为候选 Pattern，等证据足够后再人工合并。

---

## 核心能力

### 34 种 AI 写作模式

| 类别 | 数量 | 说明 |
|------|------|------|
| 内容模式 | 6 种 | 夸大意义、媒体强调、-ing 肤浅分析、宣传语言、模糊归因、公式化挑战 |
| 语言与语法模式 | 6 种 | AI 词汇、系动词回避、否定式排比、三段式、同义词循环、虚假范围 |
| 风格模式 | 6 种 | 破折号滥用、粗体滥用、内联标题列表、标题大写、表情符号、弯引号 |
| 交流模式 | 3 种 | 协作交流痕迹、知识截止免责声明、谄媚语气 |
| 填充词与回避 | 7 种 | 填充短语、过度限定、通用积极结论、连字符过度使用、权威修辞、宣告式引导、碎片化标题 |
| 中文特有模式 | 5 种 | 四字格堆砌、文言虚词滥用、中文排比句式、套路结尾词、段落节奏均匀 |

### 中文特有 Pattern

| Pattern | 问题 | 示例 |
|---------|------|------|
| 四字格堆砌 | 连续堆叠四字短语，显得像公文模板 | "与此同时、众所周知、毋庸置疑" |
| 文言虚词滥用 | 用"其、而、则、之"制造不自然的正式感 | "其强大的功能"、"而非…" |
| 中文排比句式 | "是…是…是…"、"在于…在于…在于…"机械三连 | "AI 的价值在于…在于…在于…" |
| 套路结尾词 | 用模板化短语收尾 | "综上所述"、"总而言之"、"希望有所帮助" |
| 段落节奏均匀 | 每段长度和句式过分整齐 | 连续多段都是 2-3 句、长度接近 |

### 半自动自我进化

`humanizer-zh-pro` 增加了一个轻量的自我进化工作区：

- **规则进化**：发现新的 AI 味句式后，先记录为候选 Pattern。
- **案例进化**：保存"原文 -> 改写 -> 复盘"，让规则有证据。
- **人工合并**：候选达到 3 次独立出现且至少 2 个案例后，才建议升级为正式 Pattern。

候选和案例存放在 `evolution/` 目录，正式规则仍以 `SKILL.md` 为准。

---

## 安装

### 方式一：通过 npx 安装

```bash
npx skills add https://github.com/7247949-art/humanizer-zh-pro
```

### 方式二：安装到 Claude Code

```bash
git clone https://github.com/7247949-art/humanizer-zh-pro.git ~/.claude/skills/humanizer-zh-pro
```

### 方式三：安装到 Codex

```bash
git clone https://github.com/7247949-art/humanizer-zh-pro.git ~/.codex/skills/humanizer-zh-pro
```

安装后重启对应工具，让它重新加载 Skills。

---

## 使用方法

在支持 Skills 的 AI 助手中调用：

```text
/humanizer-zh-pro

请帮我人性化以下文本：

[粘贴你的 AI 生成文本]
```

你也可以直接描述目标：

```text
用 humanizer-zh-pro 帮我把这篇公众号文章去 AI 味，保留原意，但写得更像真人作者。
```

---

## 适用场景

- 公众号、百家号、头条号等中文内容平台文章
- 博客、Newsletter、专栏文章
- 产品介绍、营销文案、活动文案
- 企业报告、方案说明、知识库文档
- AI 初稿的人性化改写和二次编辑

不建议把它当成“洗稿工具”。它的目标是降低模板感和机器味，不是绕开原创要求。

---

## 改写示例

### 营销文案

**输入：**

> 坐落在风景如画的杭州市中心，这家咖啡馆拥有丰富的文化底蕴和令人叹为观止的装饰。它作为城市咖啡文化的焦点，为顾客提供无缝、直观和充满活力的体验。

**输出：**

> 这家咖啡馆在杭州市中心开了三年，以手冲咖啡和老建筑改造的空间出名。

### 博客文章

**输入：**

> 人工智能不仅仅是一种技术，它是我们思考未来的方式的革命。行业专家认为这将对整个社会产生持久影响。

**输出：**

> 我一直在想 AI 会怎么改变我们的工作方式。上周和几个做产品的朋友聊，有人觉得兴奋，有人担心失业。真相大概率在中间某个不太戏剧化的位置。

### 企业报告

**输入：**

> 综上所述，企业在数字化转型过程中应充分评估自身条件，循序渐进，避免盲目跟风。只有这样，才能真正实现数字化转型的目标。

**输出：**

> 上这些系统之前，先把自己的数据、预算和团队习惯想清楚。很多项目不是死在技术上，是死在准备不足上。

---

## 核心原则

1. **删除填充短语**：直接说观点，不用"值得注意的是"、"首先"、"综上所述"撑场面。
2. **打破公式结构**：少用"不仅…而且…"、"一方面…另一方面…"这类模板。
3. **变化节奏**：句子长短要有变化，必要时允许单句成段。
4. **信任读者**：不要每一步都解释，能直接说就直接说。
5. **删除金句**：听起来像海报标语的句子，通常需要重写。

---

## 自我进化工作流

每次完成改写后，可以做一次轻量复盘：

1. 对照 `SKILL.md` 的正式 Pattern。
2. 如果发现新 AI 味，写入 `evolution/candidates/`。
3. 将代表性案例写入 `evolution/examples/`。
4. 候选达到 `occurrences >= 3` 且 `example_count >= 2` 后，标记为 `ready_for_review`。
5. 维护者确认后，再把候选升级为正式 Pattern。

这样做的好处是：规则会进化，但不会失控。

---

## 文件结构

```text
humanizer-zh-pro/
├── SKILL.md                         # 技能定义文件
├── README.md                        # 项目说明
├── LICENSE                          # MIT License
├── references/
│   └── chinese-patterns.md          # 5 种中文特有 Pattern 详解
└── evolution/
    ├── README.md                    # 自我进化流程说明
    ├── candidates/
    │   └── _template.md             # 候选 Pattern 模板
    ├── examples/
    │   └── _template.md             # 改写案例模板
    └── review-log.md                # Pattern 审核记录
```

---

## 版本历史

### v1.1.0（2026-06-05）

- 项目更名为 `humanizer-zh-pro`
- 增加半自动自我进化工作区
- 增加候选 Pattern 与改写案例模板
- 增加候选达到门槛后的人工审核流程

### v1.0.0（2026-05-14）

- 初始版本
- 34 种 AI 写作模式（29 种原版 + 5 种中文特有）
- 完整中文改写示例
- 五大核心原则
- 10 步执行流程

---

## 上游与致谢

本项目基于 [RobinZorro86/humanizer-zh-plus](https://github.com/RobinZorro86/humanizer-zh-plus) 更新而来，并延续其对上游项目的整理。

感谢以下项目和资料：

- [RobinZorro86/humanizer-zh-plus](https://github.com/RobinZorro86/humanizer-zh-plus)
- [blader/humanizer](https://github.com/blader/humanizer)
- [op7418/humanizer-zh](https://github.com/op7418/humanizer-zh)
- [Wikipedia: Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing)
- [WikiProject AI Cleanup](https://en.wikipedia.org/wiki/Wikipedia:WikiProject_AI_Cleanup)

本仓库在 `humanizer-zh-plus` 的基础上，继续增加半自动自我进化机制，用于沉淀候选 Pattern、改写案例和审核记录。

---

## License

MIT License。保留 attribution 即可自由使用、修改和分发。
