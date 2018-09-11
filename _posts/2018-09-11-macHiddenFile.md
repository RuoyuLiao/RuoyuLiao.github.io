---
layout: post
title: Mac hide or display Hidden files with terminal
tags: mac
---

显示Mac隐藏文件的命令：
```
defaults write com.apple.finder AppleShowAllFiles -bool true
```
隐藏Mac隐藏文件的命令：
```
defaults write com.apple.finder AppleShowAllFiles -bool false
```