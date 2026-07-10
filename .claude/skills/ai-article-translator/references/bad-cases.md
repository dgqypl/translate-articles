# 反面样例（Bad cases）

## Case 1：往 SingleFile 保存的原页面 HTML 里注入译文

**场景：** 用户给了一个 SingleFile 从 x.com/twitter 保存的博客文章 HTML（6MB，内嵌 base64 图片、Twitter UI、评论树、多层 draft.js 嵌套）。翻译方案是「找到每段英文，在其后插入一个 `<div>` 装中文译文」。

**症状：** 成品浏览器打开完全没法读——译文被 Twitter 的评论区、侧边栏、UI 元素挤压变形，DOM 层级太深导致 CSS 覆盖失效，视觉上像散落各处的乱码。

**根因：** SingleFile 导出的 X/Twitter 页面（以及 Notion、Medium 等类 SPA）结构不是内容优先，是 UI 优先。文章正文可能被切成 73 个 draft.js 块，散落在评论、通知、按钮之间。这类 DOM 天然不适合注入外部节点。

**正确做法：** 忽略原页面结构，只从中提取正文段落（通常在 `<article>`, `.longform-*`, `[data-testid=tweetText]`, `<h1>`/`<h2>`/`<p>` 等语义节点里），然后**新建一个干净的双语 HTML 文件**，套用 `assets/template.html`。

**判别标志：** 只要源 HTML 是 SingleFile 导出的类 SPA 页面（x.com, twitter.com, notion.so, medium.com, substack.com, linkedin.com 等），或体积 > 1MB，一律走"新建干净文件"路径，永远不要 in-place 注入。

## Case 2：生造 "克劳德" 这类音译

**症状：** 通用翻译插件把 Claude → 克劳德, Cursor → 光标, agent → 代理人, Sonnet → 十四行诗。

**根因：** 没有 AI Agent 领域背景。

**正确做法：** 遵守 `glossary.md` 第一类"保留英文原样"。

## Case 3：翻译代码块

**症状：** 把 `git commit -m "feat: add foo"` 里的英文单词也译成中文，或把 Python 变量名译成拼音。

**正确做法：** 代码块整块跳过，内联代码保留。用户看不懂会追问。
