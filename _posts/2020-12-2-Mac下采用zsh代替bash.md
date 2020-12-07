---
layout: post
title: Mac下采用zsh代替bash
date: 2020-12-2
categories: cutomizer
tags: shell
---

## 查看shell
cat /etc/shells
```
Last login: Wed Dec  2 15:04:03 on ttys009
forudev@forudevdeMac-mini ~ % cat /etc/shells
# List of acceptable shells for chpass(1).
# Ftpd will not allow users to connect who are not using
# one of these shells.

/bin/bash
/bin/csh
/bin/dash
/bin/ksh
/bin/sh
/bin/tcsh
/bin/zsh
forudev@forudevdeMac-mini ~ % 

```
## 切换
chsh -s /bin/zsh

## 安装
```
git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh 

# 备份
cp ~/.zshrc ~/.zshrc.orig
# 替换
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
```
## 主题
打开~/.zshrc，添加一行
```
ZSH_THEME="af-magic"

```

## 语法高亮
```
brew install zsh-syntax-highlighting
source /usr/local/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
source ~/.zshrc
```

## 检查环境变量
echo $PATH