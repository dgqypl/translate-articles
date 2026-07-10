# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Purpose

This directory is a personal archive for translated articles in the AI Agent field. Articles are sourced from the web, translated using the `/ai-article-translator` skill, and saved here as bilingual (English-Chinese) HTML files.

## Article Index

Every session loads @ARTICLES.md — a hand-maintained index of every translated article in this directory, each with core points and memory-anchor keywords in Chinese. When the user asks about a past article by fuzzy recall ("我记得有篇文章说……"), match against ARTICLES.md first before searching HTML files. After translating a new article with `/ai-article-translator`, append a new section to ARTICLES.md following the existing structure (元信息 / 核心观点 / 关键词).

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
