---
title: 从 Markdown 到博客
published: 2026-11-12
description: 用一篇示例记录博客的写作与发布流程。
category: 技术笔记
tags: [Astro, Markdown]
---

## 写作与预览

把文章保存到 `src/content/posts/`，填写标题、日期和分类。运行以下命令在本地预览文章。

```sh
pnpm dev
```

## 构建与发布

运行 `pnpm build` 生成静态页面和站内搜索索引。GitHub Pages 设置好后，推送更新即可触发部署。
