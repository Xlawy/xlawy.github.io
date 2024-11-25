---
title: 「macOS技巧」加快macOS光标按键移动速度
date: 2024-11-25 02:47 +0800
categories: [macOS]
tags: [macOS, 技巧]
description: 加快macOS光标按键移动速度。
---
1. 在设置中修改案件重复和重复前延迟
2. 想要更快?

```shell
# KeyRepeat
# 0/1/2 -> SLOWER
# 1 RECOMMENDED
defaults write NSGlobalDomain KeyRepeat -int 1

# InitialKeyRepeat
# 15 10 -> FASTER
# 15 RECOMMENDED
defaults write NSGlobalDomain InitialKeyRepeat -int 15
```
