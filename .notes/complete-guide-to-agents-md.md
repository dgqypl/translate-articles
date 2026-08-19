# A Complete Guide To AGENTS.md

## 元信息

- **作者**：Matt Pocock
- **来源**：AI Hero（aihero.dev）
- **原文**：https://www.aihero.dev/a-complete-guide-to-agents-md
- **译文**：`A Complete Guide To AGENTS.md - 双语.html`
- **主题**：如何为 AI 编码 agent 优化 AGENTS.md 文件

## 核心观点

### 什么是 AGENTS.md
- 提交进 Git 的 markdown 文件，定制 AI 编码 agent 在仓库中的行为。位于对话历史顶端，就在 system prompt 正下方。
- 两类内容：个人范畴（commit 风格、编码偏好）+ 项目范畴（项目做什么、包管理器、架构决策）。
- 开放标准，多数工具支持但非全部。Claude Code 例外——用 CLAUDE.md 不用 AGENTS.md，可 `ln -s AGENTS.md CLAUDE.md` 建符号链接统一。

### 超大文件为何是问题
- 反馈循环：agent 犯错 → 加规则 → 重复几百次 → 长成"烂泥球"（ball of mud）。不同人塞冲突意见，没人做完整梳理，反而拖累表现。
- 禁止用 init 脚本自动生成 AGENTS.md：会灌入一堆"对多数场景有用"的东西，把面面俱到摆在克制之上。
- **指令预算（instruction budget）**（引 Humanlayer 的 Kyle）：前沿 thinking LLM 能以合理一致性遵循约 150–200 条指令；小模型和 non-thinking 模型能关注的更少。每个 token 每次请求都加载，不管相不相关。结论：理想的 AGENTS.md 应尽可能小。
- **过时文档毒化上下文**：文档很快过时，人有内置怀疑能力，agent 每次读文档会被过时信息主动毒化。尤其别记文件路径（会被重命名/移动，agent 信心满满找错地方）。与其记结构不如描述能力，让 agent 规划时按需生成文档。领域概念（organization vs group vs workspace）比路径稳定，但快速演进的库里也会漂移，下手要轻。

### 瘦身：绝对下限只放三样
1. 一句话项目描述（作用类似基于角色的 prompt，锚定每个决策）。例：`This is a React component library for accessible data visualization.`
2. 包管理器（非 npm 时明说，否则 agent 默认 npm 生成错命令）。也可用 corepack 自动处理告警省预算。
3. 非标准的 build / typecheck 命令。
- 其他一切放别处。

### 渐进式披露（progressive disclosure）
- 只给 agent 此刻需要的，其余指向别处。agent 在文档层级里穿行很快。
- 语言专属规则拆到独立文件：根 AGENTS.md 里只写 `For TypeScript conventions, see docs/TYPESCRIPT.md`。注意轻口吻——不要 "always"、不要全大写强制。好处：规则只在写 TS 时加载、其他任务不浪费 token、换模型时可移植。
- 可嵌套：docs/TYPESCRIPT.md 引用 docs/TESTING.md，搭可发现的资源树，甚至链外部文档（Prisma、Next.js）。
- agent skills 是渐进式披露的又一形式：只在需要时把知识拉进来。

### Monorepo
- 不限于根目录单个 AGENTS.md，子目录的会与根合并。
- 分工：根放 monorepo 目的 / 如何导航 package / 共享工具；package 级放该包目的 / 技术栈 / 专属约定。
- 别让任一层超载，agent 会看到所有合并后的文件。

### 修坏文件的 prompt
让 agent 按五步重构：① 找矛盾（逐个问保留哪版）② 抽核心（只留该进根的）③ 分组其余成独立 md ④ 建文件结构（精简根 + 各文件 + 建议 docs/ 结构）⑤ 标删除项（冗余 / 太模糊 / 过于显而易见如"写干净代码"）。

### 结论
理想 AGENTS.md 小巧聚焦并指向别处，给 agent 刚够开工的上下文加面包屑。其余存于渐进式披露（独立文件、嵌套 AGENTS.md、skill）。这让指令预算高效、agent 聚焦、配置经得起工具与最佳实践演进。
