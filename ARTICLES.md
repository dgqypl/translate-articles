# 文章索引

按记忆片段回查文章：先在下方一行摘要里做模糊匹配（关键词密集覆盖），命中后 Read 对应 `.notes/<slug>.md` 查看核心观点全文，必要时再打开 HTML 原文。

新翻译一篇文章后：① 在下面追加一行；② 在 `.notes/` 下新建同名详情文件（元信息 + 核心观点）。保持这里**一行一篇**，避免上下文膨胀。

## 目录

- **Career advice in the age of AI** — Phil Chen · agent-native 招人 / 找问题>解问题 / 扔进新环境快速识别值得解决的问题 / Leetcode 失效 / 时间关系声誉稀缺 / xG 与效率 / bitter lesson / 最后一公里 / 研究员是心态 → `.notes/career-advice-age-of-ai.md`
- **A Field Guide to Fable** — Thariq Shihipar (Anthropic) · Fable 5 使用指南 / 地图不是疆域 / unknowns 未知项 / 盲点扫查 blindspot pass / Rumsfeld 四象限 / agentic coding 核心技艺 / 实现前中后三阶段 / References 用源代码 / implementation-notes.md → `.notes/field-guide-to-fable.md`
- **Understanding is the new bottleneck** — Geoffrey Litt (Notion) · AI Engineer 演讲书面版 / 理解不是为了验证是为了参与 / 认知债 cognitive debt / explain-diff skill / literate diff / 讲解两原则 背景先行 直觉先于细节 / quiz 是限速器 books don't work / 微世界 micro-worlds Seymour Papert Mathland / 让 agent 造工具给自己用 / Prolog 调试器 迁移指挥中心 / 共享空间 shared spaces Notion 协作 / augment not automate / Alan Kay 50 年前愿景 / deeper in the loop → `.notes/understanding-is-the-new-bottleneck.md`
- **Control the ideas, not the code** — antirez (Salvatore Sanfilippo, Redis 作者) · 掌控想法而非代码 / 反 vibe coding 前置声明 / 盯代码次优 / 一天 5k 行审不过来 / LLM 局部最优强大想法弱 / 8 小时机会成本 / 《人月神话》controlling the ideas / 过去十年 slop 已经烂 / DwarfStar 本地推理 DeepSeek v4 GLM 5.2 / attention 索引实现坏 / 严谨设计+测试胜过手写 GPU kernel / Matteo Collina 质疑 / Fable 和 GPT 5.6 Sol 审阅比人强 / 写 DESIGN.md 掌握想法 / own the ideas 心智模型 / 年轻程序员例外 自己写解释器数据库哈希表 / 审前端 JS 别浪费时间 → `.notes/control-the-ideas-not-the-code.md`
- **How to become an applied AI engineer** — Eyad Khrais (varickagents COO) · SWE 转应用 AI 工程师入门 / 确定性 vs 概率性思维 / 围绕非确定 API 搭系统 / eval 两维度 outcome 打分 + trajectory 打分 / 轨迹是工具调用日志 / 确定性检查抓安全违规 judge model 打质量 / 分开报融合分骗人 / harness engineering / 五部分 tool execution + context management + state memory + guardrails + agent loop / context 是当前看的 state 是记得没在看的 / 多 agent 是分布式系统问题 / 单写者原则 single-writer / 幂等键 idempotency keys Stripe / 写入前置条件 preconditions on writes / 显式交接 explicit hand-offs orchestrator / 模型提供智能可靠性靠工程 → `.notes/how-to-become-an-applied-ai-engineer.md`
- **Interviewing Engineers in the AI Era** — Coinbase · 一年重建工程面试流程 / Q1 2025 AI 生成代码 5.7% Q4 破 50% / 人类审阅接近 100% / 高级工程师转向写 spec 指挥 AI 审 PR 抓架构错误 / 从零手写 45 分钟计时题过时 / 传统题 URL 短链 消息队列 考模式记忆已废 / 两种失败模式 false positive 刷题过关 false negative 判断力强的被漏 / 两轮相关性 84% 冗余 / 三阶段重建 前端试点 后端仓库题 全公司 AI Fluency / 打开 AI 直接被解掉必须重写题目 / repo-based 编码调试题 / AI Fluency 三维度 Usage 使用 Application 应用 Understanding Limits 边界 / 三基线信号 repo 编码调试 系统设计结合 AI 领导力行为 / 判断力和品味最重要 / 不加轮次约束 / 工作组模式 季度复盘 / 半衰期问题 题目季度退役 / 45/90 天脉搏调研 / V2 合并前置轮次 A/B 测试 / 招标准=工作标准 → `.notes/interviewing-engineers-in-the-ai-era.md`
