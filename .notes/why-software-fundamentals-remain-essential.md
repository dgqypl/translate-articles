# Why Software Fundamentals Remain Essential for AI Developers

## 元信息

- **作者**：Andrew Ng
- **出处**：DeepLearning.AI《The Batch》通讯 / X 长文（AI Engineering Skills Map 系列第三篇 · Fundamentals）
- **原文 URL**：https://x.com/AndrewYNg/status/2093388974194872781 （长文实际托管在 X article 2093384274372419585，全文经 DeepLearning.AI 转载）
- **日期**：2026-08-28
- **译文文件**：`AI Engineering Skills Map - Software Engineering Fundamentals - 双语.html`
- **正文形态**：Andrew Ng 招牌 "Dear friends... Keep building! Andrew" 通讯体，纯文字，无正文配图

## 核心观点

**主论点**：agentic coding 时代，软件工程基本功不但没过时，反而是引导 agent 的关键。就算 coding agent 写下全部代码，你也要懂基本功才能引导它做出你想要的取舍，甚至才知道有哪些取舍存在。构建 AI 应用时，AI 内核往往通过更大的软件应用来呈现，这个应用要靠有本事的工程师塑造。

**反例**：不懂基本功、只会 vibe coding 的新手能做简单应用，但常导致 agent 在 latency / availability / consistency / reliability / maintainability / simplicity / cost 上做糟糕取舍——开发者根本不知道这些取舍存在。

**五大最重要技能**（Ng 团队 AI Engineering Skills 研究结论）：

1. **构建全栈应用**：agentic coding 让前端/移动端专才转向全栈。要理解 UI 组件、缓存、页面渲染、API 选型与设计、认证、状态与会话管理、异步处理、数据持久化、测试、安全、无障碍。

2. **管理数据**：数据是软件的地基、相对难改（即便 agent 帮做迁移）。懂访问模式→决定存什么存多久；选数据模型、存储类型（关系表/文档/键值/图）、基础设施，影响速度可扩展性可用性可靠性成本；懂事务并发、数据干净一致新鲜、隐私治理合规、数据生命周期。数据架构选得差，"AI 不知道自己不知道什么"。为 agent（而非仅传统软件或人）建数据基础设施是快速演进领域。

3. **设计系统架构**：理解全栈组件后才能决定如何拼装。要理解软件目标（多少用户？延迟成本多重要？），据此选应用平台、前后端边界、系统拆分、状态放置、架构粒度（单体 vs 微服务）、技术栈（有时跑实验评估）。正确架构是移动靶：原型架构 ≠ 首个生产系统架构 ≠ 扩容后架构。

4. **让系统安全可靠**：测试策略（单元/集成测试搭配、框架、覆盖率）；围绕故障设计（处理 rate limit、优雅降级、最小化 blast radius）；"shift left" 安全左移——开发者也在变半个安全工程师，可用 AI 扫漏洞/查供应链注入/审攻击面，但仍需安全知识。

5. **扩容并在生产运维**：懂部署到生产、SDLC（配置部署环境、发布策略、CI/CD、IaaS）；可观测性、告警、事故处理；扩容（横向扩服务器、负载均衡、分片索引复制、改架构）；编码最佳实践（版本控制、代码评审、依赖维护、技术债管理）。

**收尾金句**：coding agent 改变了构建软件的方式（含不含 AI 的软件）。死记编程语法正在过时，但深懂软件运作的开发者「大幅胜过」只会 vibe coding 不求理解的人。懂基本功还帮你搞清软件能做/不能做——这是使用 coding agent、塑造 build 的重要上下文。系列后两封信将谈"使用 coding agent"与"塑造 build（shaping the build）"。
