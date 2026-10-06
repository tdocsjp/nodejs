---
title: Stream（概要）
source: https://nodejs.org/api/stream.html
---

# Stream（概要）

> この記事は概要（要約）です。原文の全文翻訳ではありません。

`node:stream` モジュールは、ストリーミングデータを扱うための API を提供します。ストリームは、データソースから宛先へのデータの流れを扱う抽象的なインターフェースで、効率的なメモリ管理とバックプレッシャー（流量制御）を実現します。

## 主なストリームの種類

| 種類 | 概要 |
|---|---|
| Readable | データを読み取れるストリーム（例: `fs.createReadStream()`、HTTP レスポンス） |
| Writable | データを書き込めるストリーム（例: `fs.createWriteStream()`、サーバー側の HTTP レスポンス） |
| Duplex | Readable と Writable を両方兼ねるストリーム（例: `net.Socket`） |
| Transform | データが流れる際にそれを変換する Duplex ストリーム（例: `zlib.createDeflate()`） |

## よく使うユーティリティ関数

| 関数 | 概要 |
|---|---|
| `stream.pipeline()` | 複数のストリームを接続し、エラー処理とクリーンアップを自動的に行う。`stream/promises` と組み合わせると Promise を返す |
| `stream.finished()` | ストリームが読み取り・書き込み不可になったときに解決する Promise を返す。クリーンアップ処理に便利 |
| `readable.pipe(destination[, options])` | Readable ストリームに Writable ストリームを接続し、バックプレッシャーを自動的に管理する |

## 基本的な概念

* **flowing モードと paused モード** — Readable ストリームは自動的にデータが流れる flowing モードと、`read()` で明示的に読み取る paused モードのいずれかで動作する
* **バックプレッシャー** — 消費側が追いつけない場合、ストリームはデータをバッファする。内部バッファが `highWaterMark` を超えると `write()` は `false` を返す
* **オブジェクトモード** — `objectMode` オプションにより、Buffer や文字列だけでなく JavaScript オブジェクトを流すこともできる

## 未翻訳

`Readable`/`Writable`/`Duplex`/`Transform` 各クラスの詳細な実装方法（`_read`・`_write` のオーバーライドなど）、Web Streams との相互変換、各イベントの詳細仕様などは未翻訳。

---

本ページは [nodejs.org/api/stream](https://nodejs.org/api/stream.html)（[nodejs/node](https://github.com/nodejs/node) の `doc/api/stream.md`）の概要を日本語でまとめた非公式訳です。原文の著作権は Node.js contributors に帰属し、MIT License で提供されています。
