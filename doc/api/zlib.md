---
title: Zlib（概要）
source: https://nodejs.org/api/zlib.html
---

# Zlib（概要）

> この記事は概要（要約）です。原文の全文翻訳ではありません。

`node:zlib` モジュールは、Gzip・Deflate/Inflate・Brotli・Zstd アルゴリズムを使った圧縮・解凍機能を提供します。Node.js の Streams API を中心に構築されており、大きなデータを効率よく扱えます。

## 簡易関数

| 関数 | 概要 |
|---|---|
| `zlib.gzip()` / `zlib.gzipSync()` | gzip 形式で圧縮する（非同期／同期） |
| `zlib.gunzip()` / `zlib.gunzipSync()` | gzip 圧縮されたデータを解凍する（非同期／同期） |
| `zlib.deflate()` / `zlib.inflate()` | deflate アルゴリズムで圧縮／解凍する |
| `zlib.brotliCompress()` / `zlib.brotliDecompress()` | Brotli アルゴリズムで圧縮／解凍する |
| `zlib.zstdCompress()` / `zlib.zstdDecompress()` | Zstandard アルゴリズムで圧縮／解凍する |

## ストリームクラス・生成関数

| 名前 | 概要 |
|---|---|
| `zlib.Gzip` / `zlib.Gunzip` | gzip 圧縮／解凍を行う Transform ストリーム |
| `zlib.Deflate` / `zlib.Inflate` | deflate 圧縮／解凍を行う Transform ストリーム |
| `zlib.BrotliCompress` / `zlib.BrotliDecompress` | Brotli 圧縮／解凍を行う Transform ストリーム |
| `zlib.Unzip` | gzip か deflate かを自動判別して解凍するストリーム |
| `createGzip()` / `createGunzip()` / `createDeflate()` / `createInflate()` など | 対応するストリームを作成する関数 |

## 基本的な使い方

```js
import { createGzip } from 'node:zlib';
import { createReadStream, createWriteStream } from 'node:fs';
import { pipeline } from 'node:stream';

const source = createReadStream('input.txt');
const destination = createWriteStream('input.txt.gz');
const gzip = createGzip();

pipeline(source, gzip, destination, (err) => {
  if (err) console.error('エラー:', err);
});
```

## 未翻訳

各関数・ストリームの詳細なオプション（圧縮レベル、辞書、ZIP アーカイブ関連クラスなど）は未翻訳。

---

本ページは [nodejs.org/api/zlib](https://nodejs.org/api/zlib.html)（[nodejs/node](https://github.com/nodejs/node) の `doc/api/zlib.md`）の概要を日本語でまとめた非公式訳です。原文の著作権は Node.js contributors に帰属し、MIT License で提供されています。
