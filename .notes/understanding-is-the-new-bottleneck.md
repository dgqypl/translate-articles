# Understanding is the new bottleneck

- **文件**：`Understanding is the new bottleneck - 双语.html`
- **作者 / 来源**：Geoffrey Litt（Notion 设计工程师）· 2026 年 7 月于 AI Engineer 大会演讲的书面版
- **形式**：博客文章 + X 推特长贴双发；文章按讲稿逐页配 slide 图
- **链接**：见 `Understanding is the new bottleneck.link.txt`
- **主题**：为什么在 agent 写代码的时代人类仍要理解代码 / 三种理解手段（讲解 / 微世界 / 共享空间）/ 从教育学借灵感

## 核心观点

1. **理解不是为了验证，是为了参与**：验证代码是「点赞 / 点踩」问题，agent 自己验自己会越来越擅长；但一个项目是无数个循环，人对系统的理解决定了他能否想出下一步怎么演进。
2. **认知债（cognitive debt）**：借用 Margaret Storey 和 Simon Willison 的概念——短期不懂能蒙过去，长期一定会反噬，跟技术债同理。
3. **技巧一：讲解（explanations）**：为 agent 的每次交付产出一份精心结构化的 explainer artifact。两条原则：**先讲背景**、**先建直觉再进细节**；把线性 diff 改写成散文式的 "literate diff"。作者做了 `/explain-diff` skill（输出 HTML 或 Notion 页），每天用。
4. **小测（quiz）是限速器**：读讲解的问题在于「读了 ≠ 懂了」（Andy Matuschak「books don't work」）。借鉴 Michael Nielsen 的间隔重复思路，讲解末尾放五道交互式小测。**规矩**：小测过不了，代码不发别人；审别人代码同理。
5. **技巧二：微世界（micro-worlds）**：来自 Seymour Papert「住在数学国」的思想——想学数学就搬去数学国住。让 agent 造出你可以「住进去」的调试器 / 迁移指挥中心，你亲手操作，自然形成直觉。**关键区别**：让 agent 造工具给「你去用」，跟让 agent 自己去 debug，是两回事。
6. **agent 可以写代码来帮人类理解代码**——这个反身能力非常重要。
7. **技巧三：共享空间（shared spaces）**：团队协作时要共享心智模型才能高效沟通。Notion 现在支持在里面跑 Claude / Cursor agent，让 agent 写的技术方案默认落在协作页面上，团队直接评论讨论。
8. **点睛：the point was always to augment, not just automate**——重点始终是「增强」而不只是「自动化」。呼应 50 年前 Alan Kay 的愿景：让计算机成为教人思考世界的媒介。
9. 未来的选项不是「把自己从循环里剥离」，而是「更深地扎进循环里（deeper in the loop）」。
