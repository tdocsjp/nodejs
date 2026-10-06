---
title: File system（概要）
source: https://nodejs.org/api/fs.html
---

# File system（概要）

> この記事は概要（要約）です。原文の全文翻訳ではありません。

`node:fs` モジュールは、POSIX の標準関数をモデルにしたファイルシステム操作を提供します。ほぼすべての操作に対して3種類の API が用意されています。

* **Promise ベース**（`node:fs/promises`）— 現代的な非同期コードで推奨
* **コールバックベース**（`node:fs`）— 最大のパフォーマンスが必要な場合向け
* **同期版**（`*Sync`）— イベントループをブロックするため慎重に使う

## インポート方法

```js
// Promise API
import * as fs from 'node:fs/promises';

// コールバック / 同期 API
import * as fs from 'node:fs';
```

## よく使う関数

| 関数 | 概要 |
|---|---|
| `readFile` | ファイル全体の内容を非同期に読み込む |
| `writeFile` | ファイルにデータを書き込む（新規作成または上書き） |
| `appendFile` | ファイル末尾にデータを追記する |
| `mkdir` | ディレクトリを作成する |
| `readdir` | ディレクトリの内容一覧を取得する |
| `stat` | ファイル・ディレクトリのメタ情報（サイズ、権限、タイムスタンプなど）を取得する |
| `unlink` | ファイルを削除する |
| `rename` | ファイルの名前を変更・移動する |
| `copyFile` | ファイルを別の場所にコピーする |
| `createReadStream` / `createWriteStream` | ファイルの内容をストリームとして読み書きする（大きいファイルでもメモリ効率が良い） |
| `watch` | ファイルシステムの変更を監視する |

## 基本的な使い方

Promise ベース（推奨）:

```js
import { readFile, writeFile } from 'node:fs/promises';

try {
  const data = await readFile('/tmp/hello', 'utf8');
  console.log(data);
} catch (error) {
  console.error('エラー:', error.message);
}
```

コールバックベース:

```js
const { readFile } = require('node:fs');

readFile('/tmp/hello', 'utf8', (err, data) => {
  if (err) throw err;
  console.log(data);
});
```

同期版:

```js
const { readFileSync } = require('node:fs');

try {
  const data = readFileSync('/tmp/hello', 'utf8');
  console.log(data);
} catch (err) {
  console.error('エラー:', err.message);
}
```

## 未翻訳

各関数の詳細な引数・オプション（フラグ、モード、エンコーディングなど）、`FileHandle` クラス、`fs.Dir`、glob 関連 API などは未翻訳。この要約は `fs`（約300KB・数千行規模）の冒頭概要のみをまとめたもの。

---

本ページは [nodejs.org/api/fs](https://nodejs.org/api/fs.html)（[nodejs/node](https://github.com/nodejs/node) の `doc/api/fs.md`）の概要を日本語でまとめた非公式訳です。原文の著作権は Node.js contributors に帰属し、MIT License で提供されています。
