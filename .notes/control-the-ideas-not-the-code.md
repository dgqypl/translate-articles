# Control the ideas, not the code

- **文件**：`Control the ideas, not the code - 双语.html`
- **作者 / 来源**：antirez（Salvatore Sanfilippo，Redis 作者），发布于 antirez.com/news/169
- **主题**：AI 时代程序员应该盯"想法"而不是"代码"

## 核心观点

1. **反 vibe coding 声明前置**：不是让你只丢一句话让 AI 出成品；前提是你 *掌控* 软件的想法(ideas)。掌控想法之后,再盯代码就是次优、往往无意义。
2. **为什么盯代码没意义**：
   - **量的问题**：LLM 一天能生成上千行,加上冗长,没法每天审 5k 行。
   - **结构错位**：LLM 局部最优很强,大想法差(但在进步);逐行扫过去意义不大,不如把心里的设计 prompt 出来,或反过来问它"这部分设计是什么"来核对模型。
   - **机会成本**:8 小时工作日里读代码就没时间做真正重要的事——想方向、想新特性、想优化技巧、做 QA。
3. **回到《人月神话》**:"controlling the ideas" 是 70 年代就有的说法,反而比 2000-2020 年间讲的很多话更贴当下。过去十年软件的 slop 水平已经烂到令人发指,现在反 AI 的人当年却不愤怒——很大程度是意识形态,不是工程判断。
4. **slop 案例:本地 LLM 推理**:antirez 用 DwarfStar 全自动实现了 DeepSeek v4 和 GLM 5.2 的推理,对比后发现其他实现里错误更多(带索引的 attention 实现是坏的,上下文过某长度后有性能陡坡等)。这类领域"严谨设计 + 测试"远好过手写/手读 GPU kernel——AI 帮了大忙。
5. **回应 Matteo Collina 的质疑**:是的,他还在人工审阅 Redis 的 AI 生成代码,但他自己认为**这已经大多没意义**——GPT 5.5 后开始如此,Fable 和 GPT 5.6 Sol 之后更明显。他挑出的都是口味问题,而 Fable/GPT 5.6 的审阅能找到远比他自己更多的错和竞态。他继续人审只是"对用户的尊重"(因为很多人还会打开文件手改)。
6. **理想工作流:写 DESIGN.md**:如果放开手,他会把审阅时间拿去做 QA、想下一个优化、并**让 LLM 写一份 DESIGN.md**,用人类语言描述每种数据结构的想法、实现技巧、设计。未来的读者应该"打开 DESIGN.md → 掌握想法(own the ideas) → 带正确的心智模型让 agent 干活",而不是读代码。
7. **对年轻程序员的例外/保留**:经验不足、还没建心智模型的年轻人,他不确定审 LLM 输出是否合适。更有用可能是**自己实现一个小解释器、小数据库、小哈希表**来学编程。"给客户审前端 JS?去他的,别把时间浪费在那种破烂上。"
8. **金句**:"Focus on controlling the ideas, instead. Focus on quality, testing, and having an idea of the software you want to ship."
