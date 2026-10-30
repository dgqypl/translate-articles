# What is a "harness"?

## 元信息
- 作者：Theo（@theo，T3 / t3.chat、T3 Code 作者）
- 原文：https://x.com/theo/status/2113424203345265053（X Article）
- 译文：`What is a harness - 双语.html`
- 抓取：api.fxtwitter.com，article 为 Draft.js blocks 结构，4 张配图按 atomic 块位置嵌回
- 主题：给非专业读者彻底讲清 harness / agent / MCP 三个概念的边界

## 核心观点

**人类用界面，LLM 用 harness。** 人类不写代码操作电脑，而是通过界面（终端、网站、app，如 Chrome / Claude Code / ChatGPT App）调用底层封装好的代码，通常看不到底层代码。

**harness 是什么。** LLM 默认只会生成文本，做不了事。要做事就需要工具（read_file / edit_file / bash / search）。但 LLM 发出的仍是文本，没法点按钮，所以需要一套文本格式表示「该跑代码了」（如 `<read_file name="README.md">`）。必须有东西解析这些回应并跑对应代码。harness = 五要素：① 能干活的工具；② 调用工具的文本语法；③ 解析消息、识别语法、运行代码的系统；④ 把工具结果回传 LLM 的方式；⑤ 带使用说明的可用工具清单。

**Claude Code 是不是 harness？算是。** 它有两部分：界面 + harness。终端里的 `claude` TUI、桌面 app 的 code 标签 GUI 都是界面，不是 harness。底层 Claude Code 用 Anthropic Agent SDK 对接 agent，ChatGPT 用 Codex App Server（内置 CLI）。Claude Code 和 Codex 都把 harness 烤进了自家 app，所以容易混淆。但同一 harness 可被别的 app 复用：Cursor harness → Grok Bot；Anthropic Agents SDK + Codex App Server → T3 Code；Pi → OpenClaw。harness 是独立部件，几乎不直接暴露给人类。

**工具归谁所有（厨房比喻）。** harness = 厨房，有各种工具但没有哪间厨房备齐所有厨师需要的东西。好 harness 允许用户自带工具。重要工具多由 harness 直接提供（Codex / Claude Code 内置多，Pi 很精简）。关键概念 tool plane（工具平面）：人类和 LLM 都看不到也碰不到工具，是 harness 把工具暴露给 LLM 和界面。

**MCP 让事情更乱。** MCP（Model Context Protocol）是让 harness 访问外部东西的标准。工具 = 「在本地跑代码做事」，MCP = 「向别处发 API 请求做事」。工具直接提供代码，MCP 让代码待在别处但 LLM 仍能发请求。最常见用途：把数据暴露给 LLM（让 ChatGPT 翻邮件、让 Claude 查网站分析）。类比：Chrome 扩展像工具（在本地 Chrome 跑代码改网站），MCP 像网站（不用安装，知道 URL 即可用）。

**T3 Code 为何走 MCP。** T3 Code 向 LLM 暴露 harness 本身没有的自定义功能，比如让 Claude Code 线程在 Codex 里派生 subagent（同类工具还有 Herdr、Orca、Superset）。本可以把这些特性做成适配各 harness（Claude Code / Codex / Antigravity / Pi / Cursor / Muse）的一套套插件，但选择把代码都留在 T3 Code、只暴露一个简单 MCP server。MCP 像菜谱——是做事的方法，不是事本身；T3 Code 是给厨房的菜谱大全，不改厨房运作，厨师可看可不看。

**agent 是什么。** agent = harness + LLM。LLM 只生成文本、harness 只是空厨房，二者组合才成 agent。不同 agent 往往只是不同的 harness 配置（自定义工具、指令、MCP server 等）。

**T3 Code 是 harness 吗？不是。** 不自带 harness 就跑不起来。厨房比喻收尾：厨师 = LLM，厨房 = harness，T3 Code = 餐厅（允许你自带任意厨房，提供自己的菜谱但厨师默认不翻）。
