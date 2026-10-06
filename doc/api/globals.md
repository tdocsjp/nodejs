---
title: Globals（概要）
source: https://nodejs.org/api/globals.html
---

# Globals（概要）

> この記事は概要（要約）です。原文の全文翻訳ではありません。

このページでは、import/require なしで Node.js のどこからでも利用できるグローバルオブジェクト・関数を説明します。ただし `__dirname`・`__filename`・`exports`・`module`・`require` などは CommonJS モジュールのスコープ内でのみ使える、厳密にはモジュールスコープの値です。

## 主なグローバル

| グローバル | 概要 |
|---|---|
| `__dirname` / `__filename` | 現在のモジュールのディレクトリ名／ファイル名（CommonJS のみ） |
| `console` | 標準出力・標準エラー出力へ書き込むためのオブジェクト |
| `process` | 環境変数・引数・ライフサイクル管理などを持つ Node.js のプロセスオブジェクト |
| `Buffer` | バイナリデータを扱うためのユーティリティクラス |
| `global` / `globalThis` | グローバル名前空間オブジェクト（現代的なコードでは `globalThis` を推奨） |
| `module` / `exports` / `require()` | CommonJS のモジュールシステム（厳密にはモジュールスコープ） |
| `setTimeout`/`setInterval`/`setImmediate` と対応する `clear*` | 非同期タイマー関数 |
| `URL` / `URLSearchParams` | WHATWG 準拠の URL 解析・クエリ文字列ユーティリティ |
| `TextEncoder` / `TextDecoder` | WHATWG 準拠のテキストエンコード・デコード |
| `structuredClone()` | 構造化データのディープクローンを行う |
| `fetch()` | ブラウザ互換の HTTP クライアント（v17.5.0 以降） |
| `performance` | パフォーマンス計測 API（mark、measure、observer） |
| `crypto` | 暗号処理のための Web Crypto API |
| `AbortController` / `AbortSignal` | Promise ベースの API のキャンセル用シグナル |
| `EventTarget` / `Event` | ブラウザ互換のイベントシステム |
| `ReadableStream` / `WritableStream` / `TransformStream` | Web Streams API の実装 |
| `WebSocket` | ブラウザ互換の WebSocket クライアント |
| `queueMicrotask()` | マイクロタスクのコールバックをキューに入れる |
| `navigator` | ハードウェア・プラットフォーム情報を一部提供する Navigator API |

## 未翻訳

各グローバルの詳細な仕様、非推奨・実験的なものの区別、CommonJS と ESM での利用可否の違いなどは未翻訳。

---

本ページは [nodejs.org/api/globals](https://nodejs.org/api/globals.html)（[nodejs/node](https://github.com/nodejs/node) の `doc/api/globals.md`）の概要を日本語でまとめた非公式訳です。原文の著作権は Node.js contributors に帰属し、MIT License で提供されています。
