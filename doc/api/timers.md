---
title: Timers（概要）
source: https://nodejs.org/api/timers.html
---

# Timers（概要）

> この記事は概要（要約）です。原文の全文翻訳ではありません。

`node:timers` モジュールは、Node.js のイベントループを中心に、将来の時点で関数を実行するためのグローバル API を提供します。タイマー関数は import/require なしでグローバルに利用できます。

## コールバック形式のタイマー

| 関数 | 概要 |
|---|---|
| `setTimeout(callback[, delay[, ...args]])` | `delay` ミリ秒後（デフォルト1ms）に1回だけ callback を実行する |
| `clearTimeout(timeout)` | `setTimeout()` で作成したタイマーを取り消す |
| `setInterval(callback[, delay[, ...args]])` | `delay` ミリ秒ごとに callback を繰り返し実行する |
| `clearInterval(timeout)` | `setInterval()` で作成したタイマーを取り消す |
| `setImmediate(callback[, ...args])` | 現在のイベントループの反復の終わり（I/O イベントの後）に callback を実行する |
| `clearImmediate(immediate)` | `setImmediate()` で作成した immediate を取り消す |

## Promise 版（`node:timers/promises`）

| 関数 | 概要 |
|---|---|
| `setTimeout([delay[, value[, options]]])` | `delay` ミリ秒後に（任意で `value` を伴って）解決する Promise を返す |
| `setImmediate([value[, options]])` | 現在のイベントループの反復の終わりに解決する Promise を返す |
| `setInterval([delay[, value[, options]]])` | `delay` ミリ秒ごとに値を生成する非同期イテレータを返す |
| `scheduler.wait(delay[, options])` | （実験的）`delay` ミリ秒後に解決する Promise を返す |
| `scheduler.yield()` | （実験的）現在のイベントループの反復の終わりに解決する Promise を返す |

## 補足

* Promise 版タイマーは `AbortSignal` でキャンセルできる
* タイマーはイベントループをアクティブに保つかどうかを `ref()`/`unref()` で制御できる
* `Symbol.dispose()` による破棄にも対応（v24.2.0 以降）

## 未翻訳

各関数の詳細な引数仕様、タイマーの `ref()`/`unref()`/`hasRef()` の挙動詳細などは未翻訳。

---

本ページは [nodejs.org/api/timers](https://nodejs.org/api/timers.html)（[nodejs/node](https://github.com/nodejs/node) の `doc/api/timers.md`）の概要を日本語でまとめた非公式訳です。原文の著作権は Node.js contributors に帰属し、MIT License で提供されています。
