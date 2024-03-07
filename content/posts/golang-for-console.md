---
author: ['nove-b']
title: 'JavascriptのConsoleはGoLangでどう表現するのか'
date: 2024-03-04
description: 'Golangで出力の方法がいくつかあるようなので、どれが最適化調べてみた。'
tags: ['golang']
ShowToc: true
draft: false
---

## Golangの出力方法がたくさんある

いつも`Javascript`をメインで使用している。`Javascript`で最も使用するのは`Console`オブジェクトに間違いない。

[console](https://developer.mozilla.org/ja/docs/Web/API/console)

デバックの際には本当にお世話になっている。なかでも`console.table`には本当に感謝している。いつもありがとう。

もう`Console`がなくては生きていけない体になってしまったので、`Golang`でも同様に出力しようとしたら、何やら書き方がたくさんあって困惑した。


## Golangで出力する

### fmt.Printf()

第一引数に書式指定文字列を受け取り、第二引数以降に渡した値をフォーマットして出力

``` go
fmt.Printf({書式指定}, {値})
```

### fmt.Println()

値を標準の書式で出力。
`fmt.Printf(%v, {値})`と同じになる。

``` go
fmt.Println({値})
```

調べたらこれくらいしかなかった。
じゃあなんで混乱したかというとコードを書いていて`log.Printf()`というのが出てきたせいである。

### log.Printf() / log.PrintIn()

> パッケージ ログは、単純なログ パッケージを実装します。これは、出力をフォーマットするためのメソッドを備えたタイプLoggerを定義します

つまりどういうことかよくわからないので、実装してみる。

## fmt と log の違いを実装してみる。

```go
func main() {
	fmt.Println("Hello, fmt")
	log.Println("Hello, log")
}
// Hello, fmt
// 2024/03/07 22:25:23 Hello, log
```

`log`の方は日時のデータが付与された。

使い方はよくわかないけど、ひとまず整理はできたので良しとする。