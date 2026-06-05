# humanizer-zh-plus

**中文文本去 AI 味增强工具。**

34 种 AI 写作模式检测与改写（29 种原版 Pattern + 5 种中文特有 Pattern），使中文文字听起来自然、有个性，像真实人类书写。

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![humanizer](https://img.shields.io/badge/based%20on-humanizer%202.5.1-blue.svg)](https://github.com/blader/humanizer)

---

## 致谢

本项目基于 **[RobinZorro86/humanizer-zh-plus](https://github.com/RobinZorro86/humanizer-zh-plus)** 更新而来，并延续其对以下开源项目的整理与致谢：

- **[blader/humanizer](https://github.com/blader/humanizer)** — 英文原版，29 种 AI 写作模式检测，MIT License。基于 Wikipedia [Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing)（WikiProject AI Cleanup 维护）。
- **[op7418/humanizer-zh](https://github.com/op7418/humanizer-zh)** — humanizer 的中文翻译版，将英文 Pattern 中文化并添加了中文触发词和示例。

RobinZorro86/humanizer-zh-plus 在上述两个项目的基础上，增加了 **5 种中文 LLM 特有的写作模式**，形成完整的 34 种 Pattern 检测体系，专为中文写作场景优化。本仓库在此基础上继续增加半自动自我进化工作区，用于沉淀候选 Pattern 和改写案例。

---

## 功能特点

### 34 种 AI 写作模式

| 类别 | 数量 | 说明 |
|------|------|------|
| 内容模式 | 6 种 | 夸大意义、媒体强调、-ing 肤浅分析、宣传语言、模糊归因、公式化挑战 |
| 语言与语法模式 | 6 种 | AI 词汇、系动词回避、否定式排比、三段式、同义词循环、虚假范围 |
| 风格模式 | 6 种 | 破折号滥用、粗体滥用、内联标题列表、标题大写、表情符号、弯引号 |
| 交流模式 | 3 种 | 协作交流痕迹、知识截止免责声明、谄媚语气 |
| 填充词与回避 | 7 种 | 填充短语、过度限定、通用积极结论、连字符过度使用、权威修辞、宣告式引导、碎片化标题 |
| **中文特有（新增）** | **5 种** | 四字格堆砌、文言虚词滥用、中文排比句式、套路结尾词、段落节奏均匀 |

### 中文特有 Pattern 说明

| Pattern | 描述 | 示例 |
|---------|------|------|
| 四字格堆砌 | 连续堆叠四字短语 | "与此同时、众所周知、毋庸置疑" |
| 文言虚词滥用 | 过度使用"其、而、则"等 | "其强大的功能"、"而非…" |
| 中文排比句式 | "是…是…是…"机械排比 | "AI的价值在于…在于…在于…" |
| 套路结尾词 | 模板化收尾 | "综上所述"、"总而言之"、"一言以蔽之" |
| 段落节奏均匀 | 连续段落长度结构相似 | 每段都是2-3句，长度相近 |

### 半自动自我进化

本项目支持轻量的规则进化与案例进化：

- **规则进化**：发现新的 AI 味句式后，先记录为候选 Pattern。
- **案例进化**：保存"原文 -> 改写 -> 复盘"，让后续规则有证据。
- **人工合并**：候选达到 3 次独立出现且至少 2 个案例后，才建议升级为正式 Pattern。

候选和案例存放在 `evolution/` 目录，正式规则仍以 `SKILL.md` 为准。

---

## 安装

### 方式一：通过 npx 安装（推荐）

```bash
npx skills add https://github.com/7247949-art/humanizer-zh-plus
```

### 方式二：Git 克隆

```bash
git clone https://github.com/7247949-art/humanizer-zh-plus.git ~/.claude/skills/humanizer-zh-plus
```

### 方式三：手动下载

1. 下载本仓库 ZIP 或克隆到本地
2. 将 `humanizer-zh-plus` 文件夹复制到对应工具的 skills 目录

---

## 使用方法

### 基本用法

在支持 skills 的 AI 助手（如 Claude Code、OpenCode、Hermes Agent）中：

```
/humanizer-zh-plus

请帮我人性化以下文本：

[粘贴你的 AI 生成文本]
```

### 场景示例

#### 改写营销文案

**输入：**
> 坐落在风景如画的杭州市中心，这家咖啡馆拥有丰富的文化底蕴和令人叹为观止的装饰。它作为城市咖啡文化的焦点，为顾客提供无缝、直观和充满活力的体验。

**输出：**
> 咖啡馆在杭州市中心开了三年，以手冲咖啡和老建筑改造的空间出名。

#### 改写博客文章

**输入：**
> 人工智能不仅仅是一种技术，它是我们思考未来的方式的革命。行业专家认为这将对整个社会产生持久影响。

**输出：**
> 我一直在想 AI 会怎么改变我们的工作方式。上周和几个做产品的朋友聊，有人觉得很兴奋，有人担心失业，大概率真相在中间某个无聊的地方。

#### 改写企业报告

**输入：**
> 综上所述，企业在数字化转型过程中应充分评估自身条件，循序渐进，避免盲目跟风。只有这样，才能真正实现数字化转型的目标。

**输出：**
> 就这些。上面的建议不一定全对，但这些问题值得在决定之前先想清楚。

---

## 核心原则

1. **删除填充短语** — 直接说观点，不用拐杖词
2. **打破公式结构** — 避免"不仅…而且…"、戏剧性分段
3. **变化节奏** — 混合句子长度，允许单句成段
4. **信任读者** — 直接陈述，跳过软化和引导
5. **删除金句** — 好文章不依赖可引用的名言

---

## 文件结构

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

---

## 版本历史

### v1.1.0（2026-06-05）
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

## 参考资源

- [Wikipedia: Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing)
- [WikiProject AI Cleanup](https://en.wikipedia.org/wiki/Wikipedia:WikiProject_AI_Cleanup)
- [blader/humanizer](https://github.com/blader/humanizer)
- [op7418/humanizer-zh](https://github.com/op7418/humanizer-zh)
- [RobinZorro86/humanizer-zh-plus](https://github.com/RobinZorro86/humanizer-zh-plus)

---

## License

MIT License — 保留 attribution 即可自由使用、修改和分发。
