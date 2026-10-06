---
title: Process（概要）
source: https://nodejs.org/api/process.html
---

# Process（概要）

> この記事は概要（要約）です。原文の全文翻訳ではありません。

`process` はグローバルオブジェクトで、現在の Node.js プロセスに関する情報を取得したり、プロセスを制御したりするために使われます。`EventEmitter` を継承しており、プロセスのライフサイクルや環境、システムリソースとやり取りできます。

## よく使うプロパティ

| プロパティ | 概要 |
|---|---|
| `process.argv` | Node.js 起動時に渡されたコマンドライン引数の配列 |
| `process.env` | ユーザー環境変数を保持するオブジェクト |
| `process.platform` | OS プラットフォーム（`'linux'`、`'darwin'`、`'win32'` など） |
| `process.arch` | Node.js がビルドされた CPU アーキテクチャ |
| `process.version` / `process.versions` | Node.js 本体および依存コンポーネントのバージョン |
| `process.pid` / `process.ppid` | 現在のプロセス ID / 親プロセスの ID |
| `process.exitCode` | プロセス終了時の終了コード（デフォルト `0`） |
| `process.stdin` / `process.stdout` / `process.stderr` | 標準入力・標準出力・標準エラー出力のストリーム |

## よく使うメソッド

| メソッド | 概要 |
|---|---|
| `process.exit([code])` | 指定した終了コードでプロセスを即座に終了する |
| `process.cwd()` / `process.chdir(dir)` | 現在の作業ディレクトリを取得／変更する |
| `process.nextTick(callback[, ...args])` | 現在の処理が終わった直後（次のイベントループの前）に callback を実行する |
| `process.uptime()` | Node.js プロセスの起動からの経過秒数を返す |
| `process.memoryUsage()` | メモリ使用量（バイト単位）を返す |
| `process.kill(pid[, signal])` | 指定したプロセスにシグナルを送る |

## 主なイベント

| イベント | 概要 |
|---|---|
| `'exit'` | プロセス終了直前に発火。リスナーは同期処理のみ可能 |
| `'beforeExit'` | イベントループが空になったときに発火。非同期処理を追加で仕込める |
| `'uncaughtException'` | 捕捉されなかった例外がイベントループまで伝播したときに発火 |
| `'unhandledRejection'` | ハンドラのない Promise の reject が発生したときに発火 |
| `'warning'` | Node.js がプロセス警告を出したときに発火 |
| `'SIGINT'`・`'SIGTERM'` など | OS シグナルに対応するイベント |

## 基本的な使い方

```js
import process from 'node:process';

console.log(`Node version: ${process.version}`);
console.log(`Platform: ${process.platform}`);
console.log(`Current directory: ${process.cwd()}`);

process.on('exit', (code) => {
  console.log(`終了コード: ${code}`);
});

process.nextTick(() => {
  console.log('次のティックで実行される');
});
```

## 未翻訳

各プロパティ・メソッドの詳細仕様（引数、エッジケース、非推奨 API を含む）、`process.report`、リソース使用量系 API などは未翻訳。

---

本ページは [nodejs.org/api/process](https://nodejs.org/api/process.html)（[nodejs/node](https://github.com/nodejs/node) の `doc/api/process.md`）の概要を日本語でまとめた非公式訳です。原文の著作権は Node.js contributors に帰属し、MIT License で提供されています。
