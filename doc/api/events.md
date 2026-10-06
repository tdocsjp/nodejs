---
title: Events（概要）
source: https://nodejs.org/api/events.html
---

# Events（概要）

> この記事は概要（要約）です。原文の全文翻訳ではありません。

`node:events` モジュールは、Node.js のイベント駆動アーキテクチャの基盤となるモジュールです。`EventEmitter` クラスを提供し、オブジェクトが名前付きのイベントを発火（emit）し、登録済みのリスナー関数を呼び出す仕組みを実現します。`fs`・`http`・`stream` など Node.js のコア API の多くがこの `EventEmitter` を継承しています。

## EventEmitter の主なメソッド

| メソッド | 概要 |
|---|---|
| `on(eventName, listener)` | 指定イベントが発火するたびに呼ばれるリスナーを登録する |
| `once(eventName, listener)` | 次の1回だけ発火するリスナーを登録し、呼び出し後は自動的に解除される |
| `emit(eventName[, ...args])` | 登録済みの全リスナーを同期的に呼び出し、引数を渡す |
| `off(eventName, listener)` / `removeListener(eventName, listener)` | 指定したリスナーを解除する |
| `removeAllListeners([eventName])` | 指定イベント（省略時は全イベント）のリスナーをすべて解除する |
| `listenerCount(eventName)` | 登録されているリスナーの数を返す |
| `listeners(eventName)` | 登録されているリスナーの配列のコピーを返す |
| `prependListener(eventName, listener)` / `prependOnceListener(eventName, listener)` | リスナー配列の先頭に追加する |
| `eventNames()` | リスナーが登録されている全イベント名の配列を返す |
| `setMaxListeners(n)` / `getMaxListeners()` | メモリリーク警告が出るまでの最大リスナー数（デフォルト10）を設定/取得する |

## 主なイベント

* `'newListener'` — リスナー追加前に発火
* `'removeListener'` — リスナー解除後に発火
* `'error'` — 特別なイベント。リスナーが登録されていない場合、プロセスがクラッシュする

## 基本的な使い方

```js
import { EventEmitter } from 'node:events';

class MyEmitter extends EventEmitter {}
const myEmitter = new MyEmitter();

myEmitter.on('event', () => {
  console.log('イベントが発生しました');
});

myEmitter.emit('event');
```

## 補足

* リスナーは登録順に同期的に呼び出される
* `'error'` イベントにリスナーがないとプロセスがクラッシュするため、必ず処理するのが安全
* `captureRejections` オプションで、非同期リスナー内の Promise rejection を自動的に処理できる
* DOM 互換の `EventTarget`/`Event` クラスも提供されている

## 未翻訳

各メソッドの引数・返り値の詳細仕様、`EventEmitterAsyncResource`、`events.once()`・`events.on()`（async iterator 版）などの個別 API ページは未翻訳。

---

本ページは [nodejs.org/api/events](https://nodejs.org/api/events.html)（[nodejs/node](https://github.com/nodejs/node) の `doc/api/events.md`）の概要を日本語でまとめた非公式訳です。原文の著作権は Node.js contributors に帰属し、MIT License で提供されています。
