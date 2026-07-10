# A Field Guide to Fable

- **文件**：`A Field Guide to Fable - 双语.html`
- **作者 / 来源**：Thariq Shihipar (Anthropic)
- **主题**：Claude Fable 5 使用指南 / agentic coding 方法论 / 如何和 Claude 协作

## 核心观点

1. **地图不是疆域**：提示词、技能、上下文是地图；代码库和真实约束是疆域。二者之间的差距 = **未知项 (unknowns)**。
2. **Fable 是第一个瓶颈在「我澄清未知项的能力」而不是模型能力的模型**。产出质量取决于用户对齐未知项的水平。
3. **未知项的四分类**（Rumsfeld 矩阵变体）：已知的已知 / 已知的未知 / 未知的已知（"见到才知道"）/ 未知的未知（盲点）。
4. **agentic 编码的核心技艺，是减少未知项并为剩余的未知项预先规划**。顶尖 agentic 编码者（Boris、Jarred）对自己想要什么了如指掌，但也为未知项留空间。
5. **指令太具体 vs 太模糊都会翻车**；关键是交代**起点**——现在思路走到哪、经验深浅、把 Claude 当思考伙伴。
6. **实现之前**用的招式：
   - **Blind Spot Pass 盲点扫查** — 让 Claude 找「未知的未知」
   - **头脑风暴 + 原型** — 对付「未知的已知」，尤其视觉设计这种"见到才知道"的
   - **Interviews 访谈** — 让 Claude 就模糊点反过来采访你
   - **References 参照** — 最好的参照是**源代码**，直接把 Fable 指向目录（Claude Design 同理，可指向喜欢的网站模块让它读底层代码）
   - **Implementation Plans 实现计划** — 审阅最容易变动的部分（数据模型、类型接口、UX 流程）
7. **实现之中**：维护 `implementation-notes.md`，让 Claude Code 记录决策，方便下一次尝试吸取教训。
8. **实现之后**：交付时嵌入 pitch 和讲解性 artifact，帮助拿到认同和批准。
9. **HTML 是可视化几乎所有这些 artifact 的最佳格式**（呼应作者之前那篇 HTML+Claude 的文章）。
