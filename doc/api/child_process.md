---
title: Child Process（概要）
source: https://nodejs.org/api/child_process.html
---

# Child Process（概要）

> この記事は概要（要約）です。原文の全文翻訳ではありません。

`node:child_process` モジュールは、`popen(3)` に似た方法でサブプロセスを生成できるようにします。親プロセスは標準入出力を設定したり、プロセス間通信（IPC）を行ったりしながら子プロセスを管理できます。

## 主な関数

| 関数 | 概要 |
|---|---|
| `spawn()` | 非同期に新しいプロセスを生成する最も低レベルな方法。デフォルトでパイプ経由で出力をストリーミングする |
| `exec()` | シェルを生成してその中でコマンドを実行し、出力をバッファしてコールバックに渡す。シェルのメタ文字が使える |
| `execFile()` | `exec()` と似ているが、デフォルトではシェルを生成せず実行ファイルを直接起動するため効率がよい。I/O リダイレクトやファイルの glob 展開はできない |
| `fork()` | `spawn()` の特殊版で、Node.js プロセスを生成する。親子間でメッセージをやり取りする IPC チャンネルが組み込みで確立される |

## 使い分け

* シェルを使う: `exec()` は使う、`execFile()`・`spawn()` は使わない（`shell` オプション指定時を除く）
* 出力のバッファ: `exec()`・`execFile()` はコールバック用にバッファする、`spawn()` はパイプでストリーミングする
* IPC: デフォルトで IPC チャンネルを確立するのは `fork()` のみ
* 用途: ストリーミングには `spawn()`、簡単なコマンドには `exec()`/`execFile()`、Node.js のワーカープロセスには `fork()`

## `ChildProcess` クラス

`EventEmitter` を継承したクラスで、上記のいずれの関数からも返される。

* イベント: `'spawn'`、`'exit'`、`'close'`、`'error'`、`'message'`、`'disconnect'`
* プロパティ: `pid`、`exitCode`、`signalCode`、`connected`、`stdin`、`stdout`、`stderr`
* メソッド: `kill()`、`send()`、`disconnect()`、`ref()`、`unref()`

## 未翻訳

各関数の詳細な引数・オプション（`stdio` 設定、環境変数の継承、タイムアウトなど）、Windows でのシェル実行の注意点などは未翻訳。

---

本ページは [nodejs.org/api/child_process](https://nodejs.org/api/child_process.html)（[nodejs/node](https://github.com/nodejs/node) の `doc/api/child_process.md`）の概要を日本語でまとめた非公式訳です。原文の著作権は Node.js contributors に帰属し、MIT License で提供されています。
