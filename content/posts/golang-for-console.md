author: ['nove-b']
title: 'JavascriptのConsoleはGoLangでどう表現するのか'
date: 2024-03-04
description: 'Golangで出力の方法がいくつかあるようなので、どれが最適化調べてみた。'
tags: ['golang']
ShowToc: true
draft: true

## Golangの出力方法がたくさんある

いつも`Javascript`をメインで使用している。`Javascript`で最も使用するのは`Console`オブジェクトに間違いない。

[console](https://developer.mozilla.org/ja/docs/Web/API/console)

デバックの際には本当にお世話になっている。なかでも`console.table`には本当に感謝している。いつもありがとう。

もう`Console`がなくては生きていけない体になってしまったので、`Golang`でも同様に出力しようとしたら、何やら書き方がたくさんあって困惑した。