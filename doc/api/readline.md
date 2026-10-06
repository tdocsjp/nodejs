---
title: Readline（概要）
source: https://nodejs.org/api/readline.html
---

# Readline（概要）

> この記事は概要（要約）です。原文の全文翻訳ではありません。

`node:readline` モジュールは、Readable ストリーム（例えば `process.stdin`）から1行ずつデータを読み取るためのインターフェースを提供します。対話的なコマンドラインアプリケーションや、ファイルを1行ずつ処理する用途に使われます。

## 主な関数・クラス

| 名前 | 概要 |
|---|---|
| `readline.createInterface(options)` | 入力ストリームから行を読み取る `readline.Interface` を作成する（コールバック形式） |
| `readlinePromises.createInterface(options)`（`node:readline/promises`） | 同じ機能を Promise ベースの API として提供する |
| `Interface` クラス | 入出力ストリームを管理し、行イベント・履歴・カーソル位置・プロンプトを扱うクラス |

```js
const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});
```

## `Interface` の主なメソッド

* `rl.question(query, callback)` — ユーザーに入力を促す（コールバック版は `callback` を、Promise 版は戻り値を使う）
* `rl.prompt()` — 設定済みのプロンプトを表示する
* `rl.close()` — インターフェースを閉じる
* `rl.pause()` / `rl.resume()` — 入力ストリームを一時停止／再開する

## 主なイベント

* `'line'` — ユーザーが Enter を押したときに発火
* `'close'` — インターフェースが閉じたときに発火
* `'SIGINT'` — Ctrl+C が押されたときに発火

## ユーティリティ関数

`readline.clearLine()`、`readline.cursorTo()`、`readline.moveCursor()`、`readline.emitKeypressEvents()` など、TTY のカーソル制御や keypress イベントを扱う関数も提供されています。

## 未翻訳

各メソッドの詳細な引数・補完（`completer`）機能、履歴の扱いなどは未翻訳。

---

本ページは [nodejs.org/api/readline](https://nodejs.org/api/readline.html)（[nodejs/node](https://github.com/nodejs/node) の `doc/api/readline.md`）の概要を日本語でまとめた非公式訳です。原文の著作権は Node.js contributors に帰属し、MIT License で提供されています。
