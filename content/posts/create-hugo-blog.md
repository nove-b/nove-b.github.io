---
author: ["nove-b"]
title: "Hugoでブログを立ち上げるまでにやったこと"
date: "2024-02-13 23:16:28"
description: "Hugoでブログを立ち上げるまでにやったこと"
tags: ["blog", "hugo"]
ShowToc: true
draft: true
---

`Hugo`でこのブログを立ち上げたので、`Hugo`のインストールから`Github Page`で公開するまで。

---

## Hugo

そもそも`Hugo`のことをよく知らずに技術選定をしてしまったので、ここでしっかり調べておくことにする。

`Hugo`は`Go`で記述された静的サイトジェネレータで **「ウェブサイトを構築するための世界最速のフレームワーク」** らしい。

[The world’s fastest framework for building websites | Hugo](https://gohugo.io/)

### 静的サイトジェネレータ

> 静的サイトジェネレーターとは、生（未加工）データとテンプレート群を基に、完全に静的なHTML Webサイトを生成するツールのことです。静的サイトジェネレーターは、基本的に個々のHTMLページをコーディングする作業を自動化し、それらのページをユーザーがすぐに使えるようにします。これらのHTMLページは事前作成されたものであるため、ユーザーはブラウザで即座に読み込むことができます。
>
> [静的サイトジェネレーターとは？](https://www.cloudflare.com/ja-jp/learning/performance/static-site-generator/)

上記の通り、事前にHTMLを生成するのでパフォーマンスがいいのがメリットのひとつ。

---

## Hugoのインストール

公式サイトに詳しい。
Windowsなので[Windowsのインストール方法](https://gohugo.io/installation/windows/)通りに行った。

---
