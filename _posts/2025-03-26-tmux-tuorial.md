---
title: tmux常用命令
date: 2025-03-26 02:47 +0800
categories: [开发工具]
tags: [工具]
description: tmux常用的命令
---

以下把control+b简称为cb

| 功能                      | 快捷键                                     |
| ------------------------- | ------------------------------------------ |
| 左右分屏                  | cb-%                                       |
| 上下分屏                  | cb-"                                       |
| 切换焦点                  | cb+上下左右                                |
| 调整大小                  | 按住cb+上下左右                            |
| 新建一个window            | cb+c                                       |
| 切换window                | cb+window编号（数字）                      |
| 退出tmux                  | cb+d(detach) 注意，此时session还在后台运行 |
| 查看所有正在运行的session  | tmux ls                                    |
| 删除session               | tmux kill-session -t \<session-name>       |
| 创建session               | tmux new -s \<session-name>                |

