# Layover —— Hugo 纯中文博客

基于 [Hugo](https://gohugo.io) 静态网站生成器与 [neopost](https://github.com/salatine/neopost) 主题搭建的个人博客，全站内容为简体中文。

## 目录结构

```
v/
├── hugo.yaml              # 站点配置文件（站点名、语言、主题、分页等）
├── archetypes/            # 新建文章时使用的模板
├── content/
│   └── zh/                # 中文内容目录
│       ├── posts/         # 博客文章（每篇一个 .md 文件）
│       ├── sidebar/       # 侧边栏（头像、简介、基本信息、友链）
│       └── welcome-header/# 首页欢迎语
├── data/
│   └── custom_themes.yaml # 自定义配色（meow）
├── static/                # 图片、图标等静态资源
├── themes/neopost/        # 主题文件
└── .github/workflows/     # GitHub Pages 自动部署配置
```

## 本地预览

在当前目录打开命令行，执行：

```bash
hugo server -D
```

然后在浏览器打开 <http://localhost:1313>。修改文章保存后，页面会自动刷新。

> 注意：日期在“未来”的文章，生产构建时不会发布；本地预览可用 `hugo server -D -F` 同时预览草稿和未来文章。

## 写新文章

```bash
hugo new content posts/我的新文章.md
```

文章为 Markdown 格式，开头 `---` 之间是标题、日期、标签、作者等信息。
写完后把 `draft: true` 改为 `draft: false`，并确认日期不是未来时间，文章才会正式发布。

## 生成静态文件

```bash
hugo --cleanDestinationDir
```

生成的纯静态网页位于 `public/` 目录，可上传到任意静态托管平台。

## 部署到 GitHub Pages

本仓库已附带 GitHub Actions 工作流（`.github/workflows/deploy.yaml`）：

1. 将本文件夹推送到 GitHub 仓库的 `main` 分支；
2. 在仓库 **Settings → Pages** 中把 Source 改为 **GitHub Actions**；
3. 此后每次 `git push`，GitHub 都会自动构建并部署，无需手动上传 `public/`。

## 修改站点信息

- 站点名称、语言、每页文章数：编辑 `hugo.yaml`
- 侧边栏头像、简介、友链：编辑 `content/zh/sidebar/` 下的文件
- 首页欢迎语：编辑 `content/zh/welcome-header/_index.md`
- 配色：编辑 `data/custom_themes.yaml`，或在 `hugo.yaml` 中把 `theme` 改为
  `light-blue`、`dark-blue`、`light-green`、`light-yellow`、`light-pink`、`light-purple` 等内置配色
