---
title: 【Android】常用控件
date: 2018-07-11 10:25 +0800
categories: [Android]
tags: [android, gui]
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