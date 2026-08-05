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

## Case 4：用 `browse text` 抓原文丢掉图片位置

**场景：** 翻译 X.com 上一条带 7 张配图的推文。用 `browse text` 拿到纯文本正文，翻译得很顺，结果成品 HTML 里一张图都没有——因为 `text` 命令把所有 `<img>` 都剥离了。

**症状 a（第一次错）：** 直接漏图，用户看不到原帖的曲线图 / 截图。

**症状 b（第二次错）：** 事后补救时用 `browse media --images` 拿到图 URL 列表，但这个列表**没有段落位置信息**——只知道"页面里有这 7 张图"，不知道每张图在哪句话后面。结果只能把图全部堆到文末的"原帖配图"区，谎称"X 推文里图片位置与段落没有精确一一对应"。这是错的：DOM 里图和段落是兄弟节点，顺序明确可读。

**根因：** 偷懒选了返回纯文本的命令。`text` 是给"我只关心正文文字"的场景用的，翻译场景不适用。

**正确做法：** 用 `browse js` 遍历目标容器的 DOM 树，按 DOM 顺序打印 TEXT 节点和 IMG 节点，得到图文交错顺序。翻译时把 `<img>` 按同样顺序嵌回对应段落后。参考代码见 SKILL.md 第 1 步。

**判别标志：** 只要原页面可能有配图（博客、推文长文、Twitter/X thread、Notion 文档、Medium/Substack 文章），第一步就走 DOM walk。只有确认"这篇纯文本、没配图"或用户明说「不要图」时才用 `text`。
