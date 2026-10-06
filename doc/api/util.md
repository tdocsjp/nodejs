---
title: Utilities（概要）
source: https://nodejs.org/api/util.html
---

# Utilities（概要）

> この記事は概要（要約）です。原文の全文翻訳ではありません。

`node:util` モジュールは、Node.js 内部 API を支えるとともに、アプリケーション・モジュール開発者が型チェックやフォーマット、Promise化、デバッグなどの共通作業を行うためのユーティリティ関数を提供します。

## よく使う関数

| 関数 | 概要 |
|---|---|
| `util.promisify(original)` | コールバック形式の関数を、Promise を返す関数に変換する。`async`/`await` と組み合わせやすくなる |
| `util.callbackify(original)` | `async` 関数や Promise を返す関数を、`(err, value)` 形式のコールバックスタイルに変換する |
| `util.inspect(object[, options])` | デバッグ用にオブジェクトを文字列表現に変換する。フォーマットや色付けをオプションで指定できる |
| `util.format(format[, ...args])` | `%s`・`%d`・`%j`・`%o` などの printf 風フォーマット指定子を使って文字列を整形する |
| `util.deprecate(fn, msg[, code[, options]])` | 関数を呼び出し時に非推奨警告を出すようにラップする |
| `util.isDeepStrictEqual(val1, val2)` | 2つの値を厳密な深い等価性で比較する |
| `util.types` | `isPromise`・`isArrayBuffer`・`isDate`・`isRegExp`・`isMap` など、詳細な型チェック関数群を提供する名前空間 |
| `util.TextEncoder` / `util.TextDecoder` | WHATWG 標準に準拠した、文字列と UTF-8 バイト列の相互変換クラス |

## 基本的な使い方

```js
const util = require('node:util');
const fs = require('node:fs');

// コールバック形式の関数を Promise 化
const readFile = util.promisify(fs.readFile);
readFile('file.txt', 'utf8').then((data) => console.log(data));

// オブジェクトを整形して表示
console.log(util.inspect({ a: 1, b: { c: 2 } }, { colors: true, depth: null }));

// 文字列のフォーマット
console.log(util.format('こんにちは %s さん、%d 歳ですね', 'Alice', 25));
```

## 未翻訳

各関数の詳細な引数・オプション仕様、`util.inspect` のカスタムフォーマッタ（`util.inspect.custom`）、`util.parseArgs` などは未翻訳。

---

本ページは [nodejs.org/api/util](https://nodejs.org/api/util.html)（[nodejs/node](https://github.com/nodejs/node) の `doc/api/util.md`）の概要を日本語でまとめた非公式訳です。原文の著作権は Node.js contributors に帰属し、MIT License で提供されています。
