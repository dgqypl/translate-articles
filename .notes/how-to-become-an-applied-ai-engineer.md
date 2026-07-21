# How to become an applied AI engineer

- **文件**：`How to become an applied AI engineer - 双语.html`
- **作者 / 来源**：Eyad Khrais（@eyad_khrais，varickagents COO；X 长文，发布于 2026-07-07）
- **主题**：从 SWE 转型应用型 AI 工程师的入门指南 / eval + harness engineering + 多 agent 系统

## 核心观点

1. **确定性 vs 概率性思维**：SWE 训练你确定性思考（同输入同输出）；应用 AI 强迫你概率性思考（围绕一次非确定性 API 调用搭系统，同输入每次可能不同）。工作重心从"造软件"变成"衡量系统是否按应有方式运行"。
2. **应用 AI 工程 = eval + harness + 多 agent 系统设计** 三大块，模型本身不算（那是模型厂做的事）。
3. **Eval 的两个维度必须分开打分**：
   - **Outcome 打分**：最终结果对不对（最容易，拿结果比对预期）。
   - **Trajectory 打分**：轨迹路径，即调了哪些工具、动了哪些字段、传了什么参数——agent 完全可以答案对但过程干了危险的事（如改了银行账户、审批前付款）。
   - 确定性检查抓安全违规（如 `send_payment` 绝不能出现在 approval 之前）；judge model + rubric 打质量分。
   - **分开报**：95% 结果正确 + 4% 越权触碰禁写字段，融合分好看，生产会炸。
4. **Harness = 模型周围的一切**：tool execution / context management / state & memory / guardrails / agent loop 五部分。模型只读写文本，harness 负责校验请求、执行动作、把结果回传。Context 是模型此刻在看的，state 是它记得但没在看的。
5. **应用型 AI 工程师大部分时间在做 harness**——搭一个操作环境，让概率性系统能在确定性软件内部干活。
6. **多 agent 部署是分布式系统问题**（不是 prompt 问题）。设计单位从"agent"变成"系统"：多个循环作用于同一环境，A 刚改完 state B 就基于旧 state 往下写。
7. **四条分布式系统方案直接套用**：
   - **单写者原则（Single-writer）**：每块重要 state 只一个 agent 有写权，其他只读或提改动请求；在工具层落实。
   - **幂等键（Idempotency keys）**：给每次 mutating 工具调用挂唯一键，重试时工具看到同键直接返上次结果，不再执行。Stripe API 就这套。
   - **写入前置条件（Preconditions on writes）**：mutating 工具动手前要求条件（"仅当状态仍是 Pending 才置为 Approved"），失败要明确报错，不要静默覆盖。
   - **显式交接（Explicit hand-offs）**：任务以带 schema 的消息传递、由 orchestrator 定序；agent 应是"被交付"任务，而不是"自己发现"任务。
8. **TL;DR**：模型提供智能，让它可靠的一切（测量层、操作环境、协调规则）都是你工程出来的。SWE 转型是已有技能的自然延伸。
9. **推荐资源**：Anthropic 的 eval 课 / Lenny 的 eval 完整指南 / Hamel 的 eval FAQ（先看后两者，再上手 Anthropic 课）；OpenAI + Anthropic 的 context management/engineering 指南；Arize 工程师关于 context management 的 talk。
