---
title: Console（概要）
source: https://nodejs.org/api/console.html
---

# Console（概要）

> この記事は概要（要約）です。原文の全文翻訳ではありません。

`node:console` モジュールは、ブラウザの JavaScript コンソールと似た、シンプルなデバッグ用コンソールを提供します。任意の Node.js ストリームに書き込める `Console` クラスをエクスポートしており、`process.stdout`/`process.stderr` に書き込むグローバルな `console` インスタンスも用意されています。

## よく使うメソッド

| メソッド | 概要 |
|---|---|
| `console.log()` | 改行付きで標準出力へ出力する。printf 風のフォーマットに対応 |
| `console.error()` | 改行付きで標準エラー出力へ出力する |
| `console.warn()` | `console.error()` のエイリアス |
| `console.info()` | `console.log()` のエイリアス |
| `console.debug()` | `console.log()` のエイリアス |
| `console.table()` | 表形式のデータを ASCII テーブルとして整形して出力する |
| `console.time()` / `console.timeEnd()` | ラベル付きタイマーを開始／終了し、経過時間を出力する |
| `console.timeLog()` | タイマーを止めずに、経過時間と追加情報を出力する |
| `console.group()` / `console.groupEnd()` | 以降の出力のインデントを増減させる |
| `console.assert()` | 値が falsy の場合に "Assertion failed" から始まるメッセージを出力する |
| `console.trace()` | "Trace:" に続けてメッセージとスタックトレースを標準エラー出力へ出力する |
| `console.count()` / `console.countReset()` | ラベルごとの呼び出し回数を数える／リセットする |

## 基本的な使い方

```js
console.log('count: %d', 5);        // count: 5
console.error('error #%d', 5);      // error #5（標準エラー出力）
console.time('timer');
// ...何らかの処理...
console.timeEnd('timer');           // timer: 225.438ms
```

## 未翻訳

`Console` クラスのコンストラクタオプション、各メソッドの詳細な引数仕様、Inspector 連携時の挙動などは未翻訳。

---

本ページは [nodejs.org/api/console](https://nodejs.org/api/console.html)（[nodejs/node](https://github.com/nodejs/node) の `doc/api/console.md`）の概要を日本語でまとめた非公式訳です。原文の著作権は Node.js contributors に帰属し、MIT License で提供されています。
