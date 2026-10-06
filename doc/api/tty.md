---
title: TTY（概要）
source: https://nodejs.org/api/tty.html
---

# TTY（概要）

> この記事は概要（要約）です。原文の全文翻訳ではありません。

`node:tty` モジュールは、ターミナル（TTY）ストリームを扱うためのクラスを提供します。テキスト端末の入出力を処理するもので、Node.js が内部的に `process.stdin`・`process.stdout`・`process.stderr` を初期化する際に使われます。

```js
const tty = require('node:tty');
```

## `tty.isatty(fd)`

指定したファイルディスクリプタが TTY に関連付けられているかどうかを返します。

```js
tty.isatty(0); // stdin が TTY かを確認
tty.isatty(1); // stdout が TTY かを確認
```

## 主なクラス

### `tty.ReadStream`

TTY の読み取り側（通常は `process.stdin`）を表します。

* `readStream.isTTY` — TTY インスタンスでは常に `true`
* `readStream.isRaw` — raw モードで動作しているかを示す
* `readStream.setRawMode(mode)` — raw 入力モードを設定する（`true`/`'raw'`、`'io'`、`false`）

### `tty.WriteStream`

TTY の書き込み側（通常は `process.stdout`/`process.stderr`）を表します。

* `writeStream.isTTY` — 常に `true`
* `writeStream.columns` / `writeStream.rows` — 現在の列数・行数
* イベント `'resize'` — ターミナルのサイズが変わったときに発火
* `writeStream.getColorDepth([env])` — 対応する色数（1・4・8・24）を返す
* `writeStream.hasColors([count][, env])` — 指定した色数以上に対応しているかを確認する
* `writeStream.getWindowSize()` — `[列数, 行数]` を返す
* `writeStream.cursorTo(x, y, [callback])` / `writeStream.moveCursor(dx, dy, [callback])` — カーソルを移動する
* `writeStream.clearLine(dir, [callback])` / `writeStream.clearScreenDown([callback])` — 行や画面をクリアする

## 基本的な使い方

```js
if (process.stdout.isTTY) {
  console.log('対話的なターミナルで実行中です');
  console.log(`ターミナルサイズ: ${process.stdout.columns}x${process.stdout.rows}`);
}
```

## 未翻訳

各メソッドの詳細な引数仕様や raw モードの挙動の詳細などは未翻訳。

---

本ページは [nodejs.org/api/tty](https://nodejs.org/api/tty.html)（[nodejs/node](https://github.com/nodejs/node) の `doc/api/tty.md`）の概要を日本語でまとめた非公式訳です。原文の著作権は Node.js contributors に帰属し、MIT License で提供されています。
