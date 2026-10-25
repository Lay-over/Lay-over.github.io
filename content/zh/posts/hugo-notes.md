---
title: "Hugo 博客搭建手记"
date: "2026-10-24T21:30:00+08:00"
tags: ["Hugo", "建站", "教程"]
title-images: ["/photo6.png"]
ending-images: []
author: "站长"
draft: false
table-of-contents: true
toc-auto-numbering: true
---
<!-- 摘要 -->
本文记录我使用 Hugo 静态网站生成器搭建个人博客的完整过程，包括安装、建站、安装主题、编写文章和本地预览。
<!--more-->
<!-- 正文 -->
## 什么是 Hugo

Hugo 是基于 Go 语言开发的静态网站生成器。它最大的优点是**速度快、零依赖**：官方直接提供编译好的单个可执行文件，不需要在电脑上安装 Go 语言环境，也不需要数据库，下载后即可使用。

与 Hexo 相比，Hugo 的构建速度明显更快，缺点是官方文档以英文为主，新手刚开始可能需要适应。

## 搭建步骤

### 下载 Hugo

到 Hugo 的 GitHub Releases 页面下载 **hugo extended** 版本（Windows 选择 `hugo_extended_*_windows-amd64.zip`）。解压后得到 `hugo.exe`，建议把它放进一个固定的文件夹，并把该文件夹加入系统环境变量 PATH，这样在任意目录都能使用 `hugo` 命令。

### 新建站点

在命令行中执行：

```bash
hugo new site 博客文件夹名
```

Hugo 会在当前目录生成一个标准的站点目录，包含 `content`、`themes`、`static`、`hugo.yaml` 等文件夹和配置文件。

### 安装主题

到 [Hugo 主题站](https://themes.gohugo.io) 挑选喜欢的主题，下载源码后解压到站点的 `themes/` 目录下，并把文件夹名改成简洁的名字（例如 `neopost`）。

再把主题 `exampleSite`（示例站点）里的 `content` 目录和配置文件复制到站点根目录，作为起步内容。注意配置文件里 `theme` 一项要与 `themes/` 下的主题文件夹名完全一致。

### 编写文章

文章放在 `content/posts/` 目录下，每篇文章是一个 Markdown 文件。可以用命令快速创建：

```bash
hugo new content posts/my-first-post.md
```

文章开头的 `---` 之间是元信息（标题、日期、标签、作者等），正文使用 Markdown 语法编写。

### 本地预览

执行：

```bash
hugo server -D
```

然后在浏览器打开 `http://localhost:1313`，就能实时预览博客；修改文件并保存后，页面会自动刷新。

## 中文化要点

主题示例默认是英文和日文双语，要做成纯中文博客，需要：

1. 在 `hugo.yaml` 的 `languages` 中只保留 `zh` 语言，`contentDir` 指向 `content/zh`；
2. 把示例文章、侧边栏、欢迎语全部翻译为中文；
3. 把主题模板中硬编码的英文（如 `Tags`、`all tags`、`read more`）改成中文；
4. 把日期格式从 `02/01/2006` 改成 `2006年01月02日`。

## 小结

整个过程的核心可以概括为：**下载 Hugo → 新建站点 → 安装主题 → 写文章 → 本地预览**。下一步是把构建产物部署到 GitHub Pages，实现免费托管与自动部署。
