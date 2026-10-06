---
title: Errors（概要）
source: https://nodejs.org/api/errors.html
---

# Errors（概要）

> この記事は概要（要約）です。原文の全文翻訳ではありません。

このページは、Node.js ランタイムおよびそのエコシステム全体で使われるエラーの仕組み、エラーの型、エラーコードについて説明しています。

## エラーハンドリングの考え方

Node.js アプリケーションで発生するエラーは、API の種類によって異なる形で伝播します。

* **同期 API** は JavaScript 標準の `throw` を使う

  ```js
  try {
    const m = 1;
    const n = m + z; // ReferenceError をスロー
  } catch (err) {
    // エラー処理
  }
  ```

* **非同期 API** では複数のパターンが使われる
  * Promise — `.catch()` や `try...await` で捕捉する
  * コールバック — 第一引数にエラーを渡す「エラーファースト」の形式
  * EventEmitter — `'error'` イベントとして発火する

  ```js
  fs.readFile('file.txt', (err, data) => {
    if (err) console.error(err); // エラーファーストコールバック
  });
  ```

## 主なエラークラス

| クラス | 概要 |
|---|---|
| `Error` | すべての Node.js エラーの基底となる汎用クラス |
| `TypeError` | 型に関連するエラー |
| `RangeError` | 値が許容範囲外であることを示すエラー |
| `ReferenceError` | 未定義の変数参照によるエラー |
| `SyntaxError` | 無効なコード構文によるエラー |
| `SystemError` | OS の制約によるエラー（ファイルが見つからない、ソケットが閉じているなど） |
| `AssertionError` | `node:assert` によって検出される論理違反 |

## `error.code` という考え方

バージョン間で変化する可能性がある `error.message` に頼る代わりに、エラーの識別には `error.code` を使うことが推奨されている。`error.code` は `ERR_MODULE_NOT_FOUND` や `ENOENT` のような、安定した機械可読の識別子を提供する。

## 未翻訳

個別のエラーコード一覧（数百種類）、各エラークラスの詳細なプロパティ、非推奨エラーコードの一覧などは未翻訳。

---

本ページは [nodejs.org/api/errors](https://nodejs.org/api/errors.html)（[nodejs/node](https://github.com/nodejs/node) の `doc/api/errors.md`）の概要を日本語でまとめた非公式訳です。原文の著作権は Node.js contributors に帰属し、MIT License で提供されています。
