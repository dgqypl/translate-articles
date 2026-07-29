# The new rules of context engineering for Claude 5 generation models

## 元信息
- 作者：Thariq Shihipar（Anthropic 技术团队成员）
- 发布日期：2026-07-24
- 原文：https://claude.com/blog/the-new-rules-of-context-engineering-for-claude-5-generation-models
- 双语文件：`The new rules of context engineering for Claude 5 generation models - 双语.html`

## 核心观点

**一句话**：给 Claude 5 代模型（Opus 5、Fable 5）写系统提示词、CLAUDE.md、skill 时，做大幅减法。Anthropic 自己把 Claude Code 系统提示词砍了 80% 以上，编码 eval 无可测损失。

### 现象：过约束
Claude Code 内部日志显示一次请求里常有互相打架的指令："该写文档的地方就写"和"绝对不要加注释"同时出现。旧模型判断力弱，需要硬规矩兜底；新模型能靠上下文和判断力自己处理。

### 六条昔今对比

1. **rules → judgement**
   - 昔：`默认不写注释，禁多行注释块`
   - 今：`match surrounding code's comment density, naming, idiom`（向周边代码看齐）

2. **examples → interface design**
   - 昔：给工具写详细示例
   - 今：例子把模型框在小空间。改设计参数——Todo 里 status 用 pending/in_progress/completed 枚举就已经在暗示用法。

3. **upfront → progressive disclosure（渐进式披露）**
   - 昔：所有指引塞进系统提示词
   - 今：verification、code review 拆成独立 skill 按需调用。工具支持 deferred loading——agent 用 ToolSearch 检索出完整定义才能调用，未被需要时不占上下文。
   - **CLAUDE.md / Skill.md 也应组织成文件树**，不是单个大杂烩。

4. **repeat → simple tool descriptions**
   - 昔：系统提示词和工具描述里都写一遍工具用法
   - 今：说明只放到工具描述里。

5. **CLAUDE.md memory → auto-memory**
   - 昔：# 快捷键写入 CLAUDE.md
   - 今：Claude 自动保存相关 memory。

6. **simple specs → rich references**
   - 昔：markdown 格式的 plan 和 spec
   - 今：HTML artifact、详尽测试用例、别的代码库里的函数、rubric（评分表）都能当参照。rubric + 动态 workflow 拉验证 agent 揣摩用户品味。

### 组装上下文四层的原则

- **系统提示词**：与产品语境强绑定。Claude Code 用户不用改；自建 agent harness 才要重投入。
- **CLAUDE.md**：轻量。简述 repo 用途 + 主写"gotchas"（代码库里的坑，例如 type 集中在一个大文件里）。**不要写 Claude 看文件系统就能知道的显而易见的东西**。有特有的验证方式→抽成 verification skill 从 CLAUDE.md 指过去。
- **Skills**：轻量指南。不要写得管得太死（除非极重要场景）。长 skill 切多文件。承载"属于你/团队/产品的独特观点、知识、最佳实践"。
- **References**：@ 提及文件。**优先代码形式**——Claude 最擅长的语言。**HTML mockup 效果好于设计描述或截图**。spec 可以是测试套件或另一个 codebase 里的函数。

### 工具
`claude doctor` / `/doctor`：自动帮你把 skills 和 CLAUDE.md 调到合适量级。

## 值得记住的原话

> Write code that reads like the surrounding code: match its comment density, naming, and idiom.

> A HTML mockup of a design will generally produce better results than a description of the design or a screenshot.

> Avoid stating 'the obvious' things Claude should know by looking at your file system or your repo.

## 与其他文章的联系

- 与 `[[field-guide-to-fable]]`（同作者 Thariq）互补：那篇讲用户侧怎么用好 Fable，这篇讲产品侧/agent 搭建者怎么写好上下文。文末也直接指向 Fable field guide。
- 与 `[[understanding-is-the-new-bottleneck]]` 的"让 agent 造工具给自己用"思路一致：progressive disclosure 是让 agent 自己去检索工具定义，而不是全部预加载。
