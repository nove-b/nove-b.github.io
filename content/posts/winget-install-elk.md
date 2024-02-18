---
author: ["nove-b"]
title: "WingetでWindowsにアプリをインストールする"
date: "2024-02-17 16:38:21"
description: "パッケージマネージャーを使用しアプリを管理する"
tags: ["winget", "package manager"]
ShowToc: true
# draft: true
---

## 環境
- windws11
- winget => v1.6.3482
---


## パッケージマネージャーを使用する

この前、`Hugo`をインストールする際にパッケージマネージャーである`Scoop`を使用した。

> Chocolateyが有名っぽいけど、インストール方法がぱっと見わからなかったので、Scoopを使用することにした。
> 調べるとMacではHomebrew一択っぽい。Windowsではwingetが公式っぽく、インストールも必要なく使えて便利そうだった。
> [Hugoでブログを立ち上げるまでにやったこと](https://nove-b.github.io/posts/create-hugo-blog/)

その際に、パッケージマネージャー（`Winget`）の便利さを初めて知った。

なんとインストールしたソフトウェアの情報を`json`にして出力することができるらしい。

だけでなく、インポートをすることで記載されたツールをインストールすることができるらしい。

つまりこれを管理しておけば、パソコンを変えた時にソフトウェアの引継ぎができるとのこと。

今更だけど、そろそろパソコンを買い替えたと思ったので、少しでも引き継げるように使用してみることにした。

## Elkをインストールする

ちょうどマストドンの`Windows`クライアントが欲しかったので、`Elk`をインストールすることにした。

### Wingetのバージョン確認

WingetはWindowsに標準でインストールされているので、

```powershell
winget -v
v1.6.3482
```

特に何もせずともバージョンを確認できる。

### インストールしたいソフトウェアを検索

```powershell
 winget search "Elk"

 名前         ID                  バージョン 一致              ソース
---------------------------------------------------------------------
TagIt CO Elk 9PCGNR99HGKQ        Unknown                      msstore
Elk          Elk.Elk             0.4.0                        winget
LDCad        RolandMelkert.LDCad 1.6d2                        winget
Obsidian     Obsidian.Obsidian   1.5.3      Tag: zettelkasten winget
```

### インストールする

```powershell
winget install Elk.Elk
見つかりました Elk [Elk.Elk] バージョン 0.4.0
このアプリケーションは所有者からライセンス供与されます。
Microsoft はサードパーティのパッケージに対して責任を負わず、ライセンスも付与しません。
ダウンロード中 https://github.com/elk-zone/elk-native/releases/download/elk-native-v0.4.0/Elk_0.4.0_windows_x86_64.msi
  ██████████████████████████████  7.31 MB / 7.31 MB
インストーラーハッシュが正常に検証されました
パッケージのインストールを開始しています..
インストーラーハッシュが正常に検証されました
インストールが完了しました
```

`ID`を使用してインストールする。

ここから結構時間がかかったのは自身のパソコンの性能か、通信環境か、結構な時間がかかった。


### アップグレードする

```powershell
winget upgrade
```

で、現在のバージョンと、利用可能なバージョンが表示される。

```powershell
winget upgrade --all
```

上記のコマンドですべてのソフトウェアをアップグレードできる。

### インストール情報をエクスポートする

```powershell
winget export --output C:{path}
```

<mark>2024-02-18 09:24:38：追記</mark>

エクスポートされなくて、色々試行錯誤した結果、ファイル名を指定していないことに気が付いた。

正しくは、下記で無事に`json`が作成された。

```powershell
winget export --output C:{path}\{file-name}.json
```


これで、インストールした情報をエクスポートできる。

### エクスポート情報をインポートする

```powershell
winget import --import-file C:{path}
```

これを実行すると、インストールされていないソフトウェアは自動的にインストールされらしい。
また既にインストールされていてもバージョンが古い場合はアップグレードされるらしい。

ただ、試していないのでわからない。

## 設定ファイルをGithubに

`Winget`でエクスポートした`json`を`Github`に置いておけば、いろんな環境で情報を共有できるし、パソコンの買い替えも不便がなくなるかもしれない。


この前聞いていいなあと思っていた盆栽とはこれのことだったのか。

<iframe style="border-radius:12px" src="https://open.spotify.com/embed/episode/3EE3uyFP2yxhud21L0l1jc?utm_source=generator" width="100%" height="352" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>