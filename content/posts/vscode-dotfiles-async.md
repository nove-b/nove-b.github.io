---
author: ['nove-b']
title: 'VSCodeのドットファイルをGithubで管理し常に最新を共有する'
date: 2024-03-16  
description: 'VSCode'
tags: ['dotfiles', VSCode]
ShowToc: true
draft: true
---

パソコンがもっさりしている。
どうやら買い替えの時期が近いらしい。

そもそもキーボードもふたつのキーが機能していない。

そういうわけで環境を色々整理し始めた。

[WingetでWindowsにアプリをインストールする](http://localhost:1313/posts/winget-install-elk/)

上の記事もそういう理由。

今回はVSCodeの環境を`dotfiles`で管理できるようにする。

## dotfilesとは

`dotfiles`とは下記のこと。

> dotfilesとは、ホームディレクトリに置いてあるドット(.)から始まる設定ファイル(.bashrcとか)を管理しているリポジトリのことである。シェルやエディタの設定からアプリケーションの設定まで幅広いものが置かれている。
>
> 引用：[ようこそdotfilesの世界へ - Qiita](https://qiita.com/yutkat/items/c6c7584d9795799ee164#dotfiles%E3%81%A8%E3%81%AF)

つまりこれを使用すれば、どのパソコンでも一瞬で同一の環境を作成することができる。

会社のパソコンと自宅のパソコンの設定だって一緒にできる。

## VSCodeでやってみる

そういうわけで、もっともよく使用するVSCodeでやってみることにした。

管理するのは２つ。

1. 拡張機能
2. 環境設定


### 拡張機能

拡張機能は

```bash
code --list-extensions > extensions
```

でインストールした拡張機能の一覧を、

```
  C:\Users\name\.vscode\extensions
```

に一覧で書き出すことができる。


### 環境設定

環境設定は、

```
C:\Users\name\AppData\Roaming\Code\User
> keybindings.json
> settings.json
```

に存在している。

この3つをGit管理するようにする。


https://qiita.com/miiina016/items/018331b36ecf57ed8973