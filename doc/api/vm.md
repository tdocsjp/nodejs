---
title: VM（概要）
source: https://nodejs.org/api/vm.html
---

# VM（概要）

> この記事は概要（要約）です。原文の全文翻訳ではありません。

`node:vm` モジュールは、V8 の仮想マシンのコンテキスト内で JavaScript コードをコンパイル・実行できるようにします。呼び出し元とは異なるグローバルオブジェクトを持つ、分離されたコンテキストでコードを実行できます。

> **警告:** `node:vm` モジュールはセキュリティ機構では*ありません*。信頼できないコードを実行するために使用しないでください。

## 主なクラス・関数

| 名前 | 概要 |
|---|---|
| `vm.Script` | JavaScript コードをコンパイルし、再パースなしで異なるコンテキストで繰り返し実行できるようにする |
| `vm.createContext([contextObject[, options]])` | オブジェクトをコード実行用のグローバルコンテキストとして使えるように準備する |
| `vm.runInNewContext(code[, contextObject[, options]])` | 新しいコンテキストを作成し、コードをコンパイルして一度に実行する |
| `vm.runInContext(code, contextifiedObject[, options])` | 既存のコンテキスト化されたオブジェクト内で、コンパイル済みまたは新しいコードを実行する |
| `vm.runInThisContext(code[, options])` | 新しいコンテキストを作成せず、現在のグローバルコンテキストでコードを実行する |

## 基本的な使い方

```js
import { createContext, runInContext } from 'node:vm';

const x = 1;
const context = { x: 2 };
createContext(context);

const code = 'x += 40; var y = 17;';
runInContext(code, context);

console.log(context.x); // 42
console.log(context.y); // 17
console.log(x); // 1（変更されない）
```

この例は、コンテキストが変数スコープをメインの実行コンテキストから分離することを示しています。

## 未翻訳

各クラス・関数の詳細なオプション、`vm.SourceTextModule`（ESM 対応）、`vm.measureMemory()` などは未翻訳。

---

本ページは [nodejs.org/api/vm](https://nodejs.org/api/vm.html)（[nodejs/node](https://github.com/nodejs/node) の `doc/api/vm.md`）の概要を日本語でまとめた非公式訳です。原文の著作権は Node.js contributors に帰属し、MIT License で提供されています。
