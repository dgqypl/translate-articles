# AI Agent 领域术语表

翻译时必读。三类词处理规则不同。

## 一、保留英文原样（不译）

模型 / 产品名：Claude, Codex, Claude Code, Claude Design, Cursor, Windsurf, Devin, GitHub Copilot, ChatGPT, GPT, o1, o3, Gemini, Llama。

Claude 家族模型：Fable, Opus, Sonnet, Haiku（不译为"寓言 / 作品 / 十四行诗 / 俳句"）。

技术名词：agent, agentic, prompt, skill, MCP, tool use, subagent, LLM, RAG, artifact, spec, diff, PR, commit, worktree, harness, hook, checkpoint, workflow, guardrails, sandbox, eval, benchmark, fine-tune, in-context learning, chain-of-thought, ReAct, function calling, structured output, JSON schema, embedding, vector DB, context window, token, prefix cache, KV cache, streaming, temperature, top-p, retry, backoff, rate limit。

厂商 / 组织：Anthropic, OpenAI, Google DeepMind, xAI, Meta, Hugging Face。

## 二、固定中译（每次都用同一个译名）

| 英文 | 中译 |
|---|---|
| unknowns | 未知项 |
| unknown unknowns | 未知的未知 |
| known unknowns | 已知的未知 |
| unknown knowns | 未知的已知 |
| known knowns | 已知的已知 |
| blindspot / blind spot | 盲点 |
| blindspot pass | 盲点扫查（保留 blindspot pass 括注） |
| context | 上下文 |
| context engineering | 上下文工程 |
| pre-implementation | 实现之前 |
| during implementation | 实现之中 |
| post implementation | 实现之后 |
| implementation plan | 实现计划 |
| implementation notes | 实现笔记 |
| brainstorm | 头脑风暴 |
| interview | 访谈 |
| reference（作名词，指参照物） | 参照 |
| pitch | 卖点介绍 |
| explainer | 讲解 |
| quiz | 小测 |
| the map is not the territory | 地图不是疆域（可加括注：即模型不等于现实） |
| ship | 交付 |
| buy-in | 认同 |
| edge case | 边界情况 |
| pivot | 转向 |
| iterate | 迭代 |
| iteration | 迭代 |
| codebase | 代码库 |
| source code | 源代码 |
| under the hood | 底层 |
| best practice | 最佳实践 |
| out of the box | 开箱即用 |
| long-horizon task | 长跨度任务 |
| roll back / revert | 回滚 |
| ground truth | 真值 / 参考答案 |
| hallucinate / hallucination | 幻觉 |
| jailbreak | 越狱 |
| red team | 红队 |
| alignment | 对齐 |
| RLHF | RLHF（不译） |
| system prompt | 系统提示词 |
| user prompt | 用户提示词 |
| few-shot | 少样本 |
| zero-shot | 零样本 |
| tool call | 工具调用 |
| multi-agent | 多 agent（agent 保留英文） |

## 三、完全不译（原样保留在译文里）

- 代码块整块。
- 命令行（`gh pr view`, `git status`, `pytest ...`）。
- 文件路径（`src/foo.ts`, `~/Downloads`）。
- URL。
- 环境变量名、CLI flag（`--verbose`, `NODE_ENV`）。
- API/函数/方法名、类型标识符。
- JSON 键名与字面值。

## 四、译名一致性

同一篇文章内，同一英文术语只能对应同一中文译名。首次出现某"固定中译"词时，采用"中文（English）"括注；后续可省略括注。
