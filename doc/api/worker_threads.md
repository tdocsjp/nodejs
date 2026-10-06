---
title: Worker threads（概要）
source: https://nodejs.org/api/worker_threads.html
---

# Worker threads（概要）

> この記事は概要（要約）です。原文の全文翻訳ではありません。

`node:worker_threads` モジュールは、Node.js でマルチスレッドの JavaScript 実行を可能にし、CPU 負荷の高い処理を並列に実行できるようにします。子プロセスやクラスターとは異なり、ワーカースレッドは `ArrayBuffer` や `SharedArrayBuffer` を介してメモリを共有できます。

## 主なクラス・値

| 名前 | 概要 |
|---|---|
| `Worker` | 独立したイベントループと V8 インスタンスを持つ JavaScript 実行スレッドを表すクラス |
| `parentPort` | ワーカースレッド内で使える、親スレッドとの双方向通信用の MessagePort |
| `workerData` | `Worker` のコンストラクタの `workerData` オプションでワーカースレッドに渡される任意の値 |
| `isMainThread` | メインスレッドで実行中か（`true`）、ワーカースレッドで実行中か（`false`）を示す |
| `threadId` | プロセス内でスレッドを一意に識別する整数 |
| `MessageChannel` | 非同期の双方向通信のための、対になった MessagePort（`port1`・`port2`）を作成する |
| `MessagePort` | 構造化データやメモリ領域をスレッド間で転送する、非同期通信チャンネルの一端 |
| `BroadcastChannel` | 同じチャンネル名を持つすべての `BroadcastChannel` インスタンスへの一対多の非同期通信を実現する |

## 基本的な使い方

```js
import { Worker, isMainThread, parentPort, workerData } from 'node:worker_threads';

if (isMainThread) {
  const worker = new Worker(new URL(import.meta.url), {
    workerData: 'メインスレッドから',
  });
  worker.on('message', (msg) => console.log(msg));
} else {
  parentPort.postMessage(`ワーカーが受信: ${workerData}`);
}
```

## 未翻訳

`SharedArrayBuffer` によるメモリ共有の詳細、`locks`（LockManager）、ワーカーの終了処理・エラーハンドリングの詳細などは未翻訳。

---

本ページは [nodejs.org/api/worker_threads](https://nodejs.org/api/worker_threads.html)（[nodejs/node](https://github.com/nodejs/node) の `doc/api/worker_threads.md`）の概要を日本語でまとめた非公式訳です。原文の著作権は Node.js contributors に帰属し、MIT License で提供されています。
