---
author: ["nove-b"]
title: "Hugoでブログを立ち上げるまでにやったこと"
date: "2024-02-15 23:30:37"
description: "Hugoでブログを立ち上げるまでにやったこと"
tags: ["blog", "hugo"]
ShowToc: true
# draft: true
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

```powershell
scoop install hugo-extended
```

上記コマンドを使用すれば、`hugo`の拡張版をインストールすることができる。

```powershell
'hugo-extended' (0.122.0) was installed successfully!
```
---

## Hugoでサイトを構築する

`Hugo`でサイトを構築するのは簡単で、下記コマンドを叩くだけでいい。

```hugo
hugo new site site-name
```
上記を実行した後に、

```hugo
hugo -D serve
```

で、サイトを確認することができる。

---

## テーマを選んで適応する

`Hugo`は沢山のテーマが提供されている。`Wordpress`に通ずるものがある。

[Hugo Themes](https://themes.gohugo.io/)

今回は一番上にあった[PaperMod](https://themes.gohugo.io/themes/hugo-papermod/)を採用することにした。

[hugo-PaperMod](https://github.com/adityatelange/hugo-PaperMod)

### テーマを導入する

```powershell
git submodule add https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
```
#### サブモジュールって？

> 外部の git リポジトリを、自分の git リポジトリのサブディレクトリとして登録し、特定の commit を参照する仕組み

どういうこと🤔?

とりあえず、上記コマンドで`themes`の中に`PaperMod`がインストールされた。

最後に`hugo.yaml`に

```yaml
theme: PaperMod
```
を追加すればテーマが適用される。

できたサイトが[🦥 nove-b](https://nove-b.github.io/)でリポジトリが[こちら](https://github.com/nove-b/nove-b.github.io)。

---