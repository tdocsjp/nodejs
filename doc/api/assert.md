---
title: Assert（概要）
source: https://nodejs.org/api/assert.html
---

# Assert（概要）

> この記事は概要（要約）です。原文の全文翻訳ではありません。

`node:assert` モジュールは、Node.js アプリケーションで不変条件を検証するためのアサーション関数一式を提供します。主にテストや、値が期待どおりであることの検証に使われます。

## Strict モードと Legacy モード

* **Strict モード**（`require('node:assert/strict')` または `require('node:assert').strict`）— 比較に `===` と `Object.is()` を使う、より厳密なモード
* **Legacy モード**（`require('node:assert')`）— 比較メソッドで緩い等価性（`==`）を使うため、意図しない結果になることがある

## よく使う関数

| 関数 | 概要 |
|---|---|
| `assert(value[, message])` | `assert.ok()` のエイリアス |
| `assert.ok(value[, message])` | 値が truthy かどうかを検証する |
| `assert.equal(actual, expected[, message])` | 浅い等価性を検証する（legacy では `==`、strict では `===`） |
| `assert.strictEqual(actual, expected[, message])` | `Object.is()` による厳密な等価性を検証する |
| `assert.deepStrictEqual(actual, expected[, message])` | 列挙可能な自身のプロパティを再帰的に比較する、深い厳密等価性を検証する |
| `assert.notStrictEqual(actual, expected[, message])` | `Object.is()` による厳密な不等価性を検証する |
| `assert.throws(fn[, error][, message])` | `fn` がエラーをスローすることを期待し、エラーの型やプロパティを検証する |
| `assert.rejects(asyncFn[, error][, message])` | `assert.throws()` の非同期版。Promise の reject を待つ |
| `assert.fail([message])` | 即座に `AssertionError` をスローする |
| `assert.match(string, regexp[, message])` | 文字列が正規表現にマッチするかを検証する |

## 基本的な使い方

```js
import { strict as assert } from 'node:assert';

assert.strictEqual(1, 1); // OK
assert.strictEqual(1, '1'); // AssertionError: 1 !== '1'
assert.deepStrictEqual({ a: 1 }, { a: 1 }); // OK

// 非同期のテスト
await assert.rejects(
  async () => { throw new TypeError('Wrong'); },
  TypeError,
); // OK
```

## 未翻訳

各関数の詳細な引数・エッジケース、`CallTracker`（非推奨）、`assert.partialDeepStrictEqual` などは未翻訳。

---

本ページは [nodejs.org/api/assert](https://nodejs.org/api/assert.html)（[nodejs/node](https://github.com/nodejs/node) の `doc/api/assert.md`）の概要を日本語でまとめた非公式訳です。原文の著作権は Node.js contributors に帰属し、MIT License で提供されています。
