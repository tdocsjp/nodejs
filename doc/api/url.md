---
title: URL（概要）
source: https://nodejs.org/api/url.html
---

# URL（概要）

> この記事は概要（要約）です。原文の全文翻訳ではありません。

`node:url` モジュールは、URL の解決・解析のためのユーティリティを提供します。WHATWG URL 標準（ブラウザ互換の現代的な API）と、Node.js 独自の Legacy URL API の両方を実装しています。

## 主なクラス

| クラス | 概要 |
|---|---|
| `URL` | `protocol`・`hostname`・`pathname`・`search`・`hash` などのプロパティと `toString()` などのメソッドを持つ、ブラウザ互換の WHATWG URL クラス |
| `URLSearchParams` | URL のクエリパラメータを読み書きするための WHATWG 準拠 API（`append()`・`delete()`・`get()`・`set()`・`sort()` など） |
| `URLPattern`（実験的） | glob 風の構文で URL やその一部をパターンマッチングする |

```js
const myURL = new URL('https://example.org/foo#bar');
myURL.hash = 'baz'; // https://example.org/foo#baz

const params = new URLSearchParams('user=abc&query=xyz');
params.append('foo', 'bar');
```

## 主な関数

| 関数 | 概要 |
|---|---|
| `url.parse(urlString, ...)`（非推奨） | URL 文字列を legacy の URL オブジェクトに解析する。代わりに WHATWG `URL` を使うこと |
| `url.format(URL\|urlObject\|urlString[, options])` | URL オブジェクトや文字列を整形する |
| `url.fileURLToPath(url[, options])` | `file://` URL をプラットフォーム固有のファイルパスに変換する |
| `url.pathToFileURL(path[, options])` | ファイルシステムのパスを `file://` URL に変換する |
| `url.resolve(from, to)`（非推奨） | 基準 URL からの相対 URL を解決する。代わりに WHATWG `URL` コンストラクタを使うこと |

その他、`url.domainToASCII()`、`url.domainToUnicode()`、`URL.canParse()` などのユーティリティもある。

## 未翻訳

各クラス・関数の詳細な引数・プロパティ仕様、`URLSearchParams` の各メソッドの詳細などは未翻訳。

---

本ページは [nodejs.org/api/url](https://nodejs.org/api/url.html)（[nodejs/node](https://github.com/nodejs/node) の `doc/api/url.md`）の概要を日本語でまとめた非公式訳です。原文の著作権は Node.js contributors に帰属し、MIT License で提供されています。
