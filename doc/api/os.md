---
title: OS（概要）
source: https://nodejs.org/api/os.html
---

# OS（概要）

> この記事は概要（要約）です。原文の全文翻訳ではありません。

`node:os` モジュールは、システム情報や OS 固有の詳細を取得するためのユーティリティメソッド・プロパティを提供します。

## よく使う関数・プロパティ

| 名前 | 概要 |
|---|---|
| `os.platform()` | OS プラットフォームを返す（`'linux'`、`'darwin'`、`'win32'` など） |
| `os.arch()` | CPU アーキテクチャを返す（`'x64'`、`'arm64'`、`'ia32'` など） |
| `os.cpus()` | 各 CPU コアの情報（モデル、クロック速度、各モードでの使用時間）の配列を返す |
| `os.freemem()` / `os.totalmem()` | 空きメモリ量／全メモリ量（バイト単位）を返す |
| `os.homedir()` | 現在のユーザーのホームディレクトリのパスを返す |
| `os.tmpdir()` | OS のデフォルトの一時ファイルディレクトリを返す |
| `os.hostname()` | OS のホスト名を返す |
| `os.networkInterfaces()` | 割り当てられたネットワークアドレスを含む、ネットワークインターフェースの情報を返す |
| `os.userInfo([options])` | 現在実効ユーザーの情報（ユーザー名、uid、gid、シェル、ホームディレクトリ）を返す |
| `os.EOL` | OS 固有の改行コード（POSIX では `\n`、Windows では `\r\n`） |
| `os.type()` | OS 名を返す（`'Linux'`、`'Darwin'`、`'Windows_NT'` など） |
| `os.release()` | OS のリリースバージョンを返す |
| `os.uptime()` | システムの稼働時間（秒）を返す |

## 基本的な使い方

```js
import os from 'node:os';

console.log('プラットフォーム:', os.platform());  // 'linux'
console.log('アーキテクチャ:', os.arch());         // 'x64'
console.log('空きメモリ:', os.freemem());          // 1024000000
console.log('全メモリ:', os.totalmem());           // 8589934592
console.log('ホームディレクトリ:', os.homedir());  // '/home/user'
console.log('一時ディレクトリ:', os.tmpdir());     // '/tmp'
console.log('稼働時間:', os.uptime());             // 123456
```

## 未翻訳

各関数の詳細な引数仕様、`os.constants`（シグナル・エラーコード定数）、`os.loadavg()`、`os.machine()` などは未翻訳。

---

本ページは [nodejs.org/api/os](https://nodejs.org/api/os.html)（[nodejs/node](https://github.com/nodejs/node) の `doc/api/os.md`）の概要を日本語でまとめた非公式訳です。原文の著作権は Node.js contributors に帰属し、MIT License で提供されています。
