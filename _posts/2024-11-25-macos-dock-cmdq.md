---
title: 「macOS技巧」让Finder也可以通过CMD+Q快捷键来关闭
date: 2024-11-25 02:47 +0800
categories: [macOS]
tags: [macOS, 技巧]
description: 通过CMD+Q来关闭Finder
---
```shell
defaults write com.apple.finder QuitMenuItem -bool YES
killall Finder
```
