---
author: ['nove-b']
title: 'Golangのnet/httpでホットリロードの恩恵を受けたい'
date: 2024-03-07
description: 'Golangのnet/httpでホットリロードしたい'
tags: ['golang']
ShowToc: true
draft: true
---

## ホットリロードが欲しい

普段`react`とか`angular`を使用しているので標準でホットリロードが搭載しているので、あるのが当然だと思っていた。

しかし`Go`の`net/http`にはない。

ということで、何とかできないか調べてみた。


## DevContainerを使ってみる（ホットリロードができることは確認した）

[Go net/httpサーバーのホットリロードにAirを使ってみた](https://qiita.com/Domao/items/03858530067b52986ca9)

> Devcontainerに airをインストールして、DevContainer上で実行する。

色々調べた結果上記が一番楽そうだったので、やってみる。

やり方は上記の記事を引用する。

> - リポジトリ直下に .devcontainer フォルダ作成
> - .devcontainerフォルダ内に 下記内容のdevcontainer.json を作成。
> ```
> {
>	"name": "Go",
>	"image": "mcr.microsoft.com/devcontainers/go:0-1-bullseye",
>	"features": {
>		"ghcr.io/devcontainers/features/docker-outside-of-docker:1": {
>			"moby": true,
>			"installDockerBuildx": true,
>			"version": "latest",
>			"dockerDashComposeVersion": "v2"
>		}
>	},
>	"postCreateCommand": "go install github.com/cosmtrek/air@latest"
>}
> ```
> - 保存し、プロジェクトを再度開き直す
> - DevContainerを開くかどうかVSCodeに確認されるので、DevContainerとして開き直す
> - インストール完了後 プロンプト上で air と打って Airを立ち上げる

順序通りやったところ、
> DevContainerを開くかどうかVSCodeに確認されるので、DevContainerとして開き直す

の箇所で、

```
[+] Building 903.3s (2/3)
 => [internal] load build definition from Dockerfile.extended              0.3s
 => => transferring dockerfile: 2.76kB                                     0.1s
 => [internal] load .dockerignore                                          0.3s
 => => transferring context: 2B                                            0.0s
 => resolve image config for docker.io/docker/dockerfile:1.4             902.4s
 ```
 上記のようにとんでもなく時間がかかった結果諦めた。

 これは`Windows`と`Docker`問題🤔?

 ということで`WSL`上に移して実行してみる。

`Windows`上で実行するよりは早いけど、それでもめちゃくちゃ時間がかかった。

で、実行してみたところ

```bash
go.mod:3: invalid go version 'v1.21.4': must match format 1.23
```

というエラーが出たので、バージョンを`go 1.21.4`から`go 1.21`に変更し再度挑戦。

```
building...
no Go files in /workspaces/ProjectName
failed to build, error: exit status 1
running...
/bin/sh: 1: /workspaces/ProjectName/tmp/main: not found
```

次に上記エラーが出たので、`main.go`を`/src`から`root`に移動した結果、ホットリロードが動いていることが確認できた。

ただデーターベースに接続できなくなったし、`/src`の下に開発ファイルを置きたい。

ホットリロードが動くことは確認できたので、そのエラーを解消するくらいなら他の方法を探すことにした。

