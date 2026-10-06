---
title: Buffer（概要）
source: https://nodejs.org/api/buffer.html
---

# Buffer（概要）

> この記事は概要（要約）です。原文の全文翻訳ではありません。

`Buffer` クラスは、固定長のバイト列を表す Node.js のクラスです。JavaScript の `Uint8Array` のサブクラスであり、バイナリデータを直接扱うために使われます。ファイルシステムやネットワーク通信など、生のバイナリデータを扱う I/O 処理には欠かせません。

## よく使う静的メソッド

| メソッド | 概要 |
|---|---|
| `Buffer.from(...)` | 配列・文字列・ArrayBuffer・既存の Buffer などから新しい Buffer を作成する。最も汎用的な生成方法 |
| `Buffer.alloc(size[, fill[, encoding]])` | 指定サイズのゼロ初期化された Buffer を確保する。`allocUnsafe()` より安全だが遅い |
| `Buffer.concat(list[, totalLength])` | Buffer の配列を1つの新しい Buffer に連結する |
| `Buffer.isBuffer(obj)` | 対象が Buffer かどうかを判定する |

## よく使うインスタンスメソッド

| メソッド | 概要 |
|---|---|
| `buf.toString([encoding[, start[, end]]])` | Buffer の内容を指定エンコーディング（デフォルト `'utf8'`）で文字列に変換する |
| `buf.write(string[, offset[, length]][, encoding])` | 指定オフセットに文字列を書き込み、書き込んだバイト数を返す |
| `buf.subarray([start[, end]])` | Buffer の一部を参照する view を作成する（コピーではない）。`slice()` より推奨される |
| `buf.length` | Buffer 全体のバイト数を示すプロパティ |

## 基本的な使い方

```js
import { Buffer } from 'node:buffer';

// Buffer の作成
const buf1 = Buffer.from('hello');
const buf2 = Buffer.alloc(10);

// 文字列への変換
console.log(buf1.toString()); // 'hello'

// Buffer への書き込み
buf2.write('world', 0, 'utf8');

// 連結
const combined = Buffer.concat([buf1, buf2]);
```

## 未翻訳

各メソッドの詳細仕様（エンコーディングの種類、`Blob`・`File` との関係、`Buffer.allocUnsafe()` の注意点など）は未翻訳。

---

本ページは [nodejs.org/api/buffer](https://nodejs.org/api/buffer.html)（[nodejs/node](https://github.com/nodejs/node) の `doc/api/buffer.md`）の概要を日本語でまとめた非公式訳です。原文の著作権は Node.js contributors に帰属し、MIT License で提供されています。
