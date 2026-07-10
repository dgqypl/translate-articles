# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Purpose

This directory is a personal archive for translated articles in the AI Agent field. Articles are sourced from the web, translated using the `/ai-article-translator` skill, and saved here as bilingual (English-Chinese) HTML files.

## Article Index

Two-tier structure to keep session context small as the archive grows:

- **@ARTICLES.md** (auto-loaded every session): one line per article — title + author + dense Chinese keyword hooks + pointer to detail file.
- **`.notes/<slug>.md`** (read on demand): per-article detail — 元信息 + 核心观点.

When the user asks about a past article by fuzzy recall ("我记得有篇文章说……"), match against ARTICLES.md keywords first; on a hit, Read the pointed `.notes/<slug>.md` before answering; only open the HTML if the notes aren't enough. After translating a new article with `/ai-article-translator`: append one line to ARTICLES.md AND create `.notes/<slug>.md` — keep ARTICLES.md strictly one-line-per-article.

@ARTICLES.md

## Workflow

- **Translation**: Use `/ai-article-translator` skill to translate AI Agent domain articles (e.g., from Anthropic, OpenAI, research blogs)
- **Storage**: Generated HTML files are standalone with embedded CSS, using a clean bilingual layout (similar to immersive translation style)
- **Read-only**: Do not modify generated HTML files after creation — they are archival outputs

## Content Focus

Articles focus on:
- AI Agent development and tooling (Claude Code, Codex, agent frameworks)
- Latest developments in the AI Agent field
- Practical engineering with AI Agents

Articles do NOT focus on:
- LLM training or model architecture
- Deep learning theory
- Low-level ML research

## File Handling

- Each HTML file is self-contained with UTF-8 encoding
- Files are named with " - 双语.html" suffix to indicate bilingual content
- This is not a development project — no build system, tests, or dependencies
