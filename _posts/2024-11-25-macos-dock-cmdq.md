---
title: 「macOS技巧」让Finder也可以通过CMD+Q快捷键来关闭
date: 2024-11-25 02:47 +0800
categories: [macOS]
tags: [macOS, 技巧]
description: 让Finder也可以被CMD+Q来关闭。
---
```shell
defaults write com.apple.finder QuitMenuItem -bool YES
killall Finder
```
