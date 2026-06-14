# Blog Customization Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 将 astro-navfolio 模板改造为 samuisi 的个人技术博客，替换所有模板占位内容。

**Architecture:** 所有改动分为两类：(1) `src/config/site.toml` — 集中配置文件，控制站点元信息、profile、首页内容、导航、评论；(2) `src/content/` 下的三个 Markdown 内容文件。两类改动互相独立，按任务顺序执行即可。

**Tech Stack:** Astro, TOML config, Markdown/MDX

---

### Task 1: 更新站点身份与 Profile 配置

**Files:**
- Modify: `src/config/site.toml`

- [ ] **Step 1: 确认当前值**

```bash
grep -n 'title\|description\|pageTitle\|pageDescription\|repository\|footerNote\|name\|handle\|role\|meta\|github\|avatar\|enabled\|palette' src/config/site.toml | head -30
```

Expected: 看到 `navfolio` 相关的占位值。

- [ ] **Step 2: 替换 `[config.site]` 区块**

将 `src/config/site.toml` 中 `[config.site]` 下的字段改为：

```toml
[config.site]
title = "samuisi"
description = "对技术祛魅的最好方式就是掌握它"
pageTitle = "samuisi | Software Engineer"
pageDescription = "一个正在努力转行AI的C++ developer"
repository = "https://github.com/samuisi/samuisi.github.io"
footerNote = "Built with Astro · navfolio"
```

- [ ] **Step 3: 替换 `[config.profile]` 区块**

将 `[config.profile]` 下的字段改为：

```toml
[config.profile]
name = "samuisi"
handle = "@samuisi"
role = "Software Engineer"
company = ""
location = ""
email = ""
website = ""
github = "https://github.com/samuisi"
meta = "对技术祛魅的最好方式就是掌握它"
avatar = "/images/logo.png"
```

- [ ] **Step 4: 关闭评论**

将 `[config.comments]` 下的 `enabled` 改为：

```toml
[config.comments]
enabled = false
```

- [ ] **Step 5: 确认修改**

```bash
grep -n 'samuisi\|enabled' src/config/site.toml | head -20
```

Expected: 看到多行含 `samuisi`，以及 `enabled = false`。

- [ ] **Step 6: 本地构建验证**

```bash
npm run build 2>&1 | tail -10
```

Expected: 末尾出现 `Completed in` 或 `build` 成功字样，无 error。

- [ ] **Step 7: Commit**

```bash
git add src/config/site.toml
git commit -m "feat: update site identity and profile config"
```

---

### Task 2: 更新首页文案与导航配置

**Files:**
- Modify: `src/config/site.toml`

- [ ] **Step 1: 替换 `[config.home.quote]`**

```toml
[config.home.quote]
text = ["追寻能让自己感到快乐的东西"]
image = "/images/logo-with-name.png"
```

- [ ] **Step 2: 替换 `[config.home.intro]`**

```toml
[config.home.intro]
title = "hi, i'm samuisi"
name = "samuisi"
body = [
  "一个正在努力转行 AI 的 C++ developer。",
  "对技术祛魅的最好方式就是掌握它。",
]
image = "/images/logo-cat.png"
```

- [ ] **Step 3: 替换所有 `[[config.home.doing]]` 条目**

删除现有全部 `[[config.home.doing]]` 条目，替换为：

```toml
[[config.home.doing]]
text = "学习 Transformer 原理与实现"
mark = "01"

[[config.home.doing]]
text = "跟进 DLSys Course"
mark = "02"

[[config.home.doing]]
text = "AI 方向求职中"
mark = "03"
```

- [ ] **Step 4: 替换所有 `[[config.topNav.links]]` 条目**

删除现有全部 `[[config.topNav.links]]` 条目（含 Vibe 入口），替换为：

```toml
[[config.topNav.links]]
label = "Home"
href = "/"

[[config.topNav.links]]
label = "Blog"
href = "/blog"

[[config.topNav.links]]
label = "Projects"
href = "/projects"

[[config.topNav.links]]
label = "About"
href = "/about"
```

- [ ] **Step 5: 替换所有 `[[config.home.navigation]]` 条目**

删除现有全部 `[[config.home.navigation]]` 条目，替换为：

```toml
[[config.home.navigation]]
icon = "pen"
title = "Blog"
subtitle = "技术文章与学习笔记"
href = "/blog"

[[config.home.navigation]]
icon = "briefcase"
title = "Projects"
subtitle = "我做过的项目"
href = "/projects"

[[config.home.navigation]]
icon = "github"
title = "GitHub"
subtitle = "代码与开源项目"
href = "https://github.com/samuisi"

[[config.home.navigation]]
icon = "compass"
title = "About"
subtitle = "关于我"
href = "/about"
```

- [ ] **Step 6: 替换所有 `[[config.home.connect]]` 条目**

删除现有全部 `[[config.home.connect]]` 条目，替换为：

```toml
[[config.home.connect]]
label = "GitHub"
href = "https://github.com/samuisi"
icon = "github"

[[config.home.connect]]
label = "Blog"
href = "/blog"
icon = "book"

[[config.home.connect]]
label = "Projects"
href = "/projects"
icon = "repo"
```

- [ ] **Step 7: 确认修改**

```bash
grep -n 'navfolio\|dodolalorc' src/config/site.toml | grep -v 'giscus\|utterances\|waline\|comment'
```

Expected: **无输出**（非评论区块的 navfolio / dodolalorc 引用已清除；giscus 区块的残留值因 `enabled = false` 不影响功能）。

- [ ] **Step 8: 本地构建验证**

```bash
npm run build 2>&1 | tail -10
```

Expected: 构建成功，无 error。

- [ ] **Step 9: Commit**

```bash
git add src/config/site.toml
git commit -m "feat: update home page content and navigation config"
```

---

### Task 3: 替换 About 页内容

**Files:**
- Modify: `src/content/about.mdx`

- [ ] **Step 1: 查看当前文件 frontmatter**

```bash
head -10 src/content/about.mdx
```

Expected: 看到 `title: '关于 navfolio'` 等模板内容。

- [ ] **Step 2: 完整替换文件内容**

将 `src/content/about.mdx` 全部替换为：

```mdx
---
title: 'About'
description: '一个正在努力转行AI的C++ developer'
date: '2026-06-14T00:00:00+08:00'
draft: false
---

## 关于我

一个正在努力转行 AI 的 C++ developer。

对技术祛魅的最好方式就是掌握它。

## 技术背景

- C++ / 系统编程
- 正在学习：深度学习、Transformer、MLSys

## 现在在做

- 学习 Transformer 原理与实现
- 跟进 DLSys Course
- AI 方向求职中

## 联系

- GitHub: [samuisi](https://github.com/samuisi)
```

- [ ] **Step 3: 确认修改**

```bash
head -5 src/content/about.mdx
```

Expected: `title: 'About'`，无 navfolio 字样。

- [ ] **Step 4: 本地构建验证**

```bash
npm run build 2>&1 | tail -5
```

Expected: 构建成功。

- [ ] **Step 5: Commit**

```bash
git add src/content/about.mdx
git commit -m "feat: replace about page with personal bio"
```

---

### Task 4: 替换 Projects 页内容

**Files:**
- Modify: `src/content/projects/index.mdx`

- [ ] **Step 1: 查看当前文件**

```bash
head -10 src/content/projects/index.mdx
```

Expected: 看到模板描述内容。

- [ ] **Step 2: 完整替换文件内容**

将 `src/content/projects/index.mdx` 全部替换为：

```mdx
---
title: 'Projects'
description: '我做过的项目'
date: '2026-06-14T00:00:00+08:00'
draft: false
---

> 项目整理中，敬请期待。
```

- [ ] **Step 3: 确认修改**

```bash
cat src/content/projects/index.mdx
```

Expected: 只有 frontmatter 和一行占位文字。

- [ ] **Step 4: 本地构建验证**

```bash
npm run build 2>&1 | tail -5
```

Expected: 构建成功。

- [ ] **Step 5: Commit**

```bash
git add src/content/projects/index.mdx
git commit -m "feat: replace projects page with placeholder"
```

---

### Task 5: 替换示例博文

**Files:**
- Modify: `src/content/blog/hello-world.md`（编辑原文件，不删除重建，保持 slug 不变）

- [ ] **Step 1: 查看当前文件**

```bash
cat src/content/blog/hello-world.md
```

Expected: 看到模板示例内容。

- [ ] **Step 2: 完整替换文件内容**

将 `src/content/blog/hello-world.md` 全部替换为：

```md
---
title: "Hello World"
description: "第一篇博文，博客搭建记录。"
date: "2026-06-14T00:00:00+08:00"
draft: false
---

博客上线了。

用 Astro + navfolio 模板搭的，部署在 GitHub Pages。

接下来会写 AI 学习笔记、C++ 技术文章，以及一些不知道该放哪里的想法。
```

- [ ] **Step 3: 确认修改**

```bash
head -8 src/content/blog/hello-world.md
```

Expected: `title: "Hello World"`，`description: "第一篇博文，博客搭建记录。"`。

- [ ] **Step 4: 最终全量构建验证**

```bash
npm run build 2>&1 | tail -10
```

Expected: 构建成功，无 error 或 warning（除已知的 Node.js 版本 warning 可忽略）。

- [ ] **Step 5: Commit**

```bash
git add src/content/blog/hello-world.md
git commit -m "feat: replace hello world post with personal first post"
```

---

### Task 6: 推送并验收

- [ ] **Step 1: 推送到 GitHub**

```bash
git push origin main
```

- [ ] **Step 2: 等待 GitHub Actions 部署完成**

在 `https://github.com/samuisi/samuisi.github.io/actions` 确认最新 workflow 运行成功（绿色 ✓）。

- [ ] **Step 3: 逐项验收**

打开 `https://samuisi.github.io` 检查：

| 验收项 | 预期 |
|--------|------|
| 首页 profile | 显示 "samuisi" / "Software Engineer" |
| 首页 quote | "追寻能让自己感到快乐的东西" |
| 首页 intro | "hi, i'm samuisi" |
| 首页 doing | 三条 AI 学习 / 求职状态 |
| 导航栏 | 无 Vibe 入口 |
| About 页 | 个人简介，无 navfolio 字样 |
| Projects 页 | "项目整理中，敬请期待。" |
| Blog 列表 | Hello World 一篇 |
| 评论区 | 不显示 |
| Footer | 含 `samuisi.github.io` 链接 |
