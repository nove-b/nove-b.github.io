---
author: ['nove-b']
title: 'GitBashが日本語を受け付けなかったので対応させた'
date: 2024-03-16 00:20:03
description: 'GitBashが日本語を受け付けなかったので対応させた'
tags: ['GitBash']
ShowToc: false
draft: false
---

会社のPCで`Git Bash`に日本語を打つと何も表示されない。

そのため、毎回毎回`export LC_ALL=ja_JP.utf8`と記入していた。

面倒なので起動時に日本語を受け付けるようにしたい。

## .bash_profileを変更する

`user/username/.bash_profile`に`export LC_ALL=ja_JP.utf8`を追記すると実現できる。

