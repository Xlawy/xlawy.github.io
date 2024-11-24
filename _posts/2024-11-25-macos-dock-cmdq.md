---
title: 【macOS实用教程】让Finder也可以通过CMDQ来关闭
date: 2024-11-25 02:47 +0800
categories: [macOS]
tags: [macOS, 技巧]
---

```shell
defaults write com.apple.finder QuitMenuItem -bool YES
killall Finder
```
