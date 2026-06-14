# Blog Customization Design

**Date:** 2026-06-14
**Template:** astro-navfolio
**Goal:** 将模板从 navfolio demo 改造成 samuisi 的个人技术博客

---

## 背景

samuisi.github.io 使用 astro-navfolio 模板搭建，当前所有内容均为模板占位数据。目标是通过最小改动将其改造成真实可用的个人技术博客，上线后完全体现博主身份，不留模板痕迹。

---

## 定位

**个人技术博客** — 面向开发者，写技术文章、学习笔记（重点：AI / 深度学习 / C++）、项目展示。

---

## 改动范围

### 1. `src/config/site.toml`

**站点元信息**
```toml
[config.site]
title = "samuisi"
description = "对技术祛魅的最好方式就是掌握它"
pageTitle = "samuisi | Software Engineer"
pageDescription = "一个正在努力转行AI的C++ developer"
repository = "https://github.com/samuisi/samuisi.github.io"
footerNote = "Built with Astro · navfolio"
```

**主题**
```toml
[config.theme]
palette = "green-soft"   # 不变，保留默认
```

**评论**
```toml
[config.comments]
enabled = false   # 关闭，待有读者后再配置 Giscus
```

**Profile 卡片**
```toml
[config.profile]
name = "samuisi"
handle = "@samuisi"
role = "Software Engineer"
meta = "对技术祛魅的最好方式就是掌握它"
github = "https://github.com/samuisi"
company = ""
location = ""
email = ""
website = ""
```

**首页 Quote**
```toml
[config.home.quote]
text = ["追寻能让自己感到快乐的东西"]
image = "/images/logo-with-name.png"
```

**首页 Intro**
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

**首页 Doing 状态**
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

**导航栏**（去掉 Vibe）
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

**首页 Navigation 卡片**
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

**首页 Connect 链接**
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

---

### 2. 内容文件

**`src/content/about.mdx`** — 替换为个人简介骨架
```mdx
---
title: About
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

**`src/content/projects/index.mdx`** — 替换为空白占位
```mdx
---
title: Projects
---

> 项目整理中，敬请期待。
```

**`src/content/blog/hello-world.md`** — 编辑原文件（不删除重建，保持 slug 不变）
```md
---
title: "Hello World"
description: "第一篇博文，博客搭建记录。"
pubDate: 2026-06-14
---

博客上线了。

用 Astro + navfolio 模板搭的，部署在 GitHub Pages。

接下来会写 AI 学习笔记、C++ 技术文章，以及一些不知道该放哪里的想法。
```

**`src/content/vibe/`** — 保留不动。Vibe 页面 (`/vibe`) 仍可访问，只是从导航和首页移除。需要时改 TOML 加回来即可。

---

## 不在本次范围内

- avatar / logo 图片替换（`/public/images/`）
- Giscus 评论配置（待有读者后再做）
- 自定义字体
- 新博文内容

---

## 验收标准

1. 首页显示 samuisi 的 profile、quote、intro、doing 状态
2. 导航栏无 Vibe 入口
3. About 页显示个人简介（非模板内容）
4. Projects 页显示占位文字（非模板内容）
5. Blog 列表只有 Hello World 一篇（非模板示例文章）
6. 评论区不显示
7. Footer 显示正确的 repository 链接
8. 本地 `npm run build` 无报错
