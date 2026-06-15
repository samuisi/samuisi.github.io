---
title: "我的Linux工作流"
description: "离职前梳理了一下用了两年的 Linux 工作流，记录几个真正改变效率的工具"
date: "2026-06-15T08:27:21.554Z"
draft: false
showHeroImage: false
tags: []
categories: ["Linux"]
series: []
comments: true
sidebar:
  enable: true
  toc: true
  relatedPosts: true
---

要离职了，趁着还记得，把这工作几年用下来的 Linux 工作流整理一遍。工具不多，但从零配到顺手确实花了不少时间——希望这篇文章能对喜欢命令行的读者有所启发。

## Zsh shell

相较于 `bash`，`zsh` 的可玩性高了不少。

先装好 `zsh`，再套上 `oh-my-zsh` 框架，选一个 `powerlevel10k` 主题，基本上就能得到一个看起来比较现代化的命令行了。但光好看没用，真正提效的是下面这几个插件：

1. `git`: 显示当前git分支

2. `z`: 目录的瞬间移动。比如之前访问过的深路径 `~/a/b/c/d/e/very-long-name-directory-example`，只需 `z very-long` 就能跳过去——前提是你曾经 `cd` 过这里，它会记住

3. `zsh-syntax-highlighting`: 输入命令时实时高亮——命令存不存在、路径对不对，颜色一眼就看出来，在按回车之前就能发现低级错误。

4. `zsh-autosuggestions`: 根据历史命令自动给出灰色补全提示。想重跑一条很长的命令？输前几个字符，按右方向键直接补全，用过就回不去了。

## CLI工具

Shell 配好之后，再装几个 CLI 工具，效率可以再上一个台阶：

1. `fzf`: 模糊搜索神器。想编辑某个路径很深的文件，以前要先 `z` 跳目录、`ls` 看文件名、再手敲文件名；现在直接 `vim $(fzf)`，输几个关键字搜到文件直接打开。<br>
但 `fzf` 的玩法远不止找文件——凡是**在列表里模糊搜索**的需求它都能接。把 `Ctrl-R` 历史命令搜索替换成 `fzf`，搜进程、搜 git 分支，都是同一套逻辑。装完之后会感叹为什么这个工具不是默认自带的。

2. `neovim`: 我的主力编辑器。基于命令的编辑模式上手有门槛，但熟练之后双手不用离开键盘，效率确实不一样。插件生态极其庞大，老手可以把它打造成全功能 IDE。不想折腾插件配置的（比如我），直接 clone 现成方案 [NvChad](https://nvchad.com)，全局搜索、终端、目录树、代码高亮和跳转都开箱即用。

3. `tmux`: 终端复用器。本地开发优势不大，毕竟现代终端都支持多 tab。但和 SSH 搭配起来就是另一回事了。<br>
SSH 远程开发最大的痛点是**断连**——网络切换或电脑休眠，neovim 打开的文件、Claude Code 的会话全没了。而 tmux 的 session 跑在远端服务器上，SSH 断开后重连一条 `tmux attach` 就回来了，什么都在，体验非常丝滑。

4. [delta](https://github.com/dandavison/delta): 美化 `git diff` 输出的工具。原生的 diff 输出看久了眼睛会感谢你换掉它——delta 带语法高亮、行内 diff、side-by-side 对比，配置几行就能让 `git diff` / `git log` / `git show` 全部好看起来。

---

以上就是我这几年沉淀下来觉得真正值得装的东西，没有什么花哨的，但每一个都是日常高频在用的。新环境从零配起来大概半天，之后就可以一直带着走了。

