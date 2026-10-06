---
title: Performance hooks（概要）
source: https://nodejs.org/api/perf_hooks.html
---

# Performance hooks（概要）

> この記事は概要（要約）です。原文の全文翻訳ではありません。

`node:perf_hooks` モジュールは、W3C Web Performance API のサブセットと Node.js 独自の拡張を実装した、パフォーマンス計測 API を提供します。

## 主なメソッド

| 名前 | 概要 |
|---|---|
| `performance.now()` | Node.js プロセス起動からの高精度なミリ秒タイムスタンプを返す |
| `performance.mark(name[, options])` | タイムライン上に名前付きのパフォーマンスマークを作成する |
| `performance.measure(name[, startMark[, endMark]])` | 2つのマーク間（または1つのマークから現在まで）の経過時間を計測する |
| `performance.clearMarks([name])` / `performance.clearMeasures([name])` | マーク／計測結果をタイムラインから削除する |

## オブザーバー

`PerformanceObserver` は、パフォーマンスタイムラインに追加された新しい `PerformanceEntry` を監視し、コールバックで通知します。

```js
const obs = new PerformanceObserver((list) => {
  console.log(list.getEntries()[0].duration);
});
obs.observe({ type: 'measure' });
```

## イベントループの監視

`perf_hooks.monitorEventLoopDelay([options])` は、インターバルのタイミングのジッターを計測してイベントループの遅延を追跡し、イベントループの健全性を監視するための `ELDHistogram` を返します。

## ヒストグラム

`perf_hooks.createHistogram([options])` は値の分布を記録・分析する `RecordableHistogram` を作成します。`perf_hooks.timerify(fn[, options])` は関数をラップし、実行時間を自動的にヒストグラムに記録します。

## 未翻訳

`PerformanceEntry`・`PerformanceNodeTiming` などの各クラスの詳細なプロパティ、各種統計メソッド（パーセンタイルなど）の詳細は未翻訳。

---

本ページは [nodejs.org/api/perf_hooks](https://nodejs.org/api/perf_hooks.html)（[nodejs/node](https://github.com/nodejs/node) の `doc/api/perf_hooks.md`）の概要を日本語でまとめた非公式訳です。原文の著作権は Node.js contributors に帰属し、MIT License で提供されています。
