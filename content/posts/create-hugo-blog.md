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

## 環境
- windws11
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
`Windows`なので[Windowsのインストール方法](https://gohugo.io/installation/windows/)通りに行った。

パッケージ管理システムの[Chocolatey](https://chocolatey.org/)、[Scoop](https://scoop.sh/)と[Winget](https://learn.microsoft.com/en-us/windows/package-manager/)を使うインストール方法が提供されていた。他にも2つインストール方法が記載されている。比較表があるのでわかりやすい。

### パッケージ管理システム

ちなみにパッケージ管理システムとは、

> コンピュータのプログラムを一貫した方法でインストールやアンインストール、ライブラリなどの依存関係を解決する流れをツールによって管理を自動化するシステム

のこと。

`npm`とか`Composer`とかも言語のパッケージ管理ツールにあたる。


`Chocolatey`が有名っぽいけど、インストール方法がぱっと見わからなかったので、`Scoop`を使用することにした。

調べると`Mac`では`Homebrew`一択っぽい。Windowsでは`winget`が公式っぽく、インストールも必要なく使えて便利そうだった。

インストール情報をエクスポートすることもできるので、パソコンの買い替え時とかにも重宝できそうだった。

[Windowsのパッケージマネージャー「winget」を使ってみた](https://dev.classmethod.jp/articles/use_windows_package_manager_winget/)

今思えば`winget`にすれば良かったと思うけど、`Scoop`を選択したので、それで進めていく。

### Scoopでインストールする

```
scoop install hugo-extended
```

上記コマンドを使用すれば、`hugo`の拡張版をインストールすることができる。

```
'hugo-extended' (0.122.0) was installed successfully!
```
---

##　Hugoでサイトを構築する