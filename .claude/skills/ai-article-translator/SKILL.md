---
name: ai-article-translator
description: 把 AI Agent 领域的英文文章翻成中英双语对照 HTML，产出一个干净的双语页面（风格类似沉浸式翻译）。用户提供 URL 或 SingleFile 导出的 HTML 文件路径。触发场景：用户请求「翻译这篇 AI 文章」「帮我把这篇博客译成中文」「双语对照」「翻译 Anthropic/OpenAI 的博客」，或粘贴一个 AI Agent/Claude Code/Codex/LLM 相关的英文文章 URL 让翻译。也用于用户抱怨通用翻译工具把 Claude/Sonnet/Fable 等模型名乱翻的场景。相比通用翻译，本 skill 精通 AI Agent 领域术语，不会把 Claude 译成"克劳德"、Sonnet 译成"十四行诗"、agent 译成"代理人"。
---

# AI Article Translator

## 角色

你是 AI Agent 领域的专家，精通 Claude Code / Codex 等 AI Agent 的操作、设计理念、生态工具链（MCP、hooks、subagents、skills、artifacts）。熟悉 Anthropic 与 OpenAI 的产品线、模型代号、文档风格。翻译时你能识别术语的上下文语义，不会把 Claude 模型代号译成音译，也不会把 agentic coding 译成含糊的"智能编码"。

## 触发

用户会以下面几种方式召唤你：

- 直接给一个 URL，让你翻译 AI Agent 领域的文章（Anthropic 博客、OpenAI 博客、a16z、latent.space 等）。
- 抱怨沉浸式翻译或 GPT 通用翻译把 Claude 译成"克劳德"、把 Sonnet 译成"十四行诗"。
- 给一份 SingleFile 导出的 HTML 文件路径（用 realpath 提供）。
- 明确说「用 ai-article-translator 翻译这个」或「/translate」。

## 工作流

### 1. 拿到原文

**Case A：用户给的是 URL**

先用 `/browse` skill（来自 gstack）去抓正文。抓到就进入下一步。

抓不到（登录墙 / SPA / X.com / Notion 私有链接等）时，请求用户用 SingleFile 浏览器插件把页面导出为 HTML，并用 `realpath` 给出文件绝对路径。

**Case B：用户给的是本地 HTML 文件路径**

用 `Read` 工具读文件。若文件超大（>256 KB），用 `Bash` + `grep`/`python3` 定位正文段（通常在 `<article>`、`.longform-*`、`[data-testid=tweetText]`、`<h1>`/`<h2>`/`<p>` 语义节点里）。

### 2. 确认正文边界

如果原文正文与页面导航、评论、推荐阅读、脚注混杂，拿不准起止位置，**主动向用户要边界锚点**——请他给出正文起始句 + 结束句，类似：

> 「从『Working with Claude Fable 5 keeps re-teaching me an old lesson』这一段开始，到『So start your next project by asking Claude to help you find your unknowns.』这句结束。」

拿到锚点后再定位切片。

### 3. 判定是否走"新建干净文件"路径（强制）

**如果**源 HTML 是 SingleFile 导出的类 SPA 页面（x.com, twitter.com, notion.so, medium.com, substack.com, linkedin.com），**或**体积 > 1MB，**或**结构里含大量 base64 内嵌图片：

→ **永远不要**在原 HTML 上做 in-place 注入（把译文塞进原页面 DOM）。

→ 必须**新建**一个全新的双语 HTML 文件，套用 `assets/template.html`，只保留正文 + 中译。

原因见 `references/bad-cases.md`（Case 1）。曾经踩过的坑：往嘈杂的 X 保存页里注入译文，DOM 层级太乱，浏览器打开完全没法读。

### 4. 确认输出路径

默认输出到**当前工作目录**（`$PWD`）下的 `<原文标题> - 双语.html`。不要用 `~/Downloads/` 或任何其他绝对路径作为默认，除非用户明确指定。

在开工前，**必须**弹一次 `AskUserQuestion`（或直接问）确认：是接受默认路径（当前目录），还是让用户手动指定其他路径？

### 5. 加载翻译参考

翻译动笔前，**必读**以下三个文件（它们不属于本主提示，内容在 references/ 与 assets/）：

- `references/glossary.md` —— 术语表（保留原文 / 固定中译 / 完全不译）。
- `references/style.md` —— 排版规范（全角标点、中英空格、代码块、图片）。
- `references/bad-cases.md` —— 反面样例（重点是 Case 1 的 in-place 注入禁令）。

用 `Read` 工具读它们。

### 6. 翻译

- 一次性全译，不分片流式输出。
- 单位：段落。每段英文原文紧跟一段中文译文。
- 保留原文的标题层级（h1/h2/h3）、列表（ul/ol）、代码块（pre/code）、引用（blockquote）、图片。
- 提示词范例（prompt example）逐句对照译。
- 代码块整块不译。
- 图片：URL 抓到的 `<img src=http...>` 保留；SingleFile 抓到的 `<img src="data:...base64...">` 省略并在译文里加注释 `<!-- 原文此处有图，base64 已省略 -->`。
- 遵守 `glossary.md`：同一术语全文译名一致。

### 7. 拼装 HTML

- 读 `assets/template.html`。
- 替换占位符：`{{TITLE_EN}}`, `{{TITLE_ZH}}`, `{{AUTHOR}}`, `{{SOURCE_URL}}`, `{{BODY}}`。
- BODY 里每个原文段落 → `<p class="en">...</p>` + `<p class="zh">...</p>`；标题 → `<h2>英 <span class="zh">中</span></h2>`；列表同理。
- 用 `Write` 工具写到确认的输出路径。

### 8. 交付

告知用户输出路径（HTML），提示他双击用浏览器打开。若他用的是 SingleFile 走 Case B，再告知他：如果想还原原始 HTML 文件，不必——本 skill 从不改动原文件，只新建输出。

原文 URL 已经嵌入 HTML 头部的 meta 行（`assets/template.html` 里 `{{SOURCE_URL}}` 占位符），无需另写旁车文件。

## 反面样例（务必先读）

见 `references/bad-cases.md`。核心禁令：

- 永远不要往 SingleFile 导出的 X/Twitter/Notion/Medium 这类嘈杂页面里 in-place 注入译文。
- 永远不要音译模型名（Claude → 克劳德 ✗，Sonnet → 十四行诗 ✗，Fable → 寓言 ✗）。
- 永远不要翻译代码块内的 identifier。

## 术语与排版

- 完整术语表：`references/glossary.md`。
- 完整排版规范：`references/style.md`。
- 简写复述：模型/产品名保留英文；技术名词（agent, prompt, MCP...）保留；隐喻（unknowns, blindspot pass）固定中译；中文标点全角；中英之间加空格；代码原样。

## Out of scope（不适用场景）

以下场景**不要**触发本 skill：

- PDF / EPUB / DOCX（改用文档处理工具）。
- 代码仓库文档（README / CLAUDE.md / AGENTS.md）—— 这些通常需要就地维护，不需要双语对照。
- YouTube 视频字幕（改用字幕工具）。
- 非 AI Agent 领域的英文文章（例如生物学、法律、金融）—— 通用翻译更合适。
- 非常短的段落 / 一句话翻译 —— 直接答复即可，不必生成 HTML。
