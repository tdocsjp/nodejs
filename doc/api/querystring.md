---
title: Query string
source: https://nodejs.org/api/querystring.html
---

# Query string

<!--introduced_in=v0.1.25-->

> Stability: 2 - Stable

<!--name=querystring-->

<!-- source_link=lib/querystring.js -->

`node:querystring` モジュールは、URL のクエリ文字列を解析・整形するためのユーティリティを提供します。次のようにアクセスできます。

```js
const querystring = require('node:querystring');
```

`querystring` は {URLSearchParams} よりパフォーマンスが高いですが、標準化された API ではありません。パフォーマンスが重要でない場合や、ブラウザのコードとの互換性が望ましい場合は {URLSearchParams} を使ってください。

## `querystring.decode()`

<!-- YAML
added: v0.1.99
-->

`querystring.decode()` 関数は `querystring.parse()` のエイリアスです。

## `querystring.encode()`

<!-- YAML
added: v0.1.99
-->

`querystring.encode()` 関数は `querystring.stringify()` のエイリアスです。

## `querystring.escape(str)`

<!-- YAML
added: v0.1.25
-->

* `str` {string}

`querystring.escape()` メソッドは、与えられた `str` に対して、URL クエリ文字列特有の要件に最適化された方法で URL パーセントエンコーディングを行います。

`querystring.escape()` メソッドは `querystring.stringify()` によって使われるもので、通常は直接使用されることを想定していません。主にアプリケーションコードが `querystring.escape` を別の関数に割り当てることで、パーセントエンコーディングの実装を置き換えられるようにするために公開されています。

## `querystring.parse(str[, sep[, eq[, options]]])`

<!-- YAML
added: v0.1.25
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/10967
    description: Multiple empty entries are now parsed correctly (e.g. `&=&=`).
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/6055
    description: The returned object no longer inherits from `Object.prototype`.
  - version:
    - v6.0.0
    - v4.2.4
    pr-url: https://github.com/nodejs/node/pull/3807
    description: The `eq` parameter may now have a length of more than `1`.
-->

* `str` {string} 解析対象の URL クエリ文字列
* `sep` {string} クエリ文字列内でキーと値のペアを区切るために使われる部分文字列。**デフォルト:** `'&'`。
* `eq` {string} クエリ文字列内でキーと値を区切るために使われる部分文字列。**デフォルト:** `'='`。
* `options` {Object}
  * `decodeURIComponent` {Function} クエリ文字列内のパーセントエンコードされた文字をデコードする際に使われる関数。**デフォルト:** `querystring.unescape()`。
  * `maxKeys` {number} 解析するキーの最大数を指定する。`0` を指定するとキー数の制限がなくなる。**デフォルト:** `1000`。

`querystring.parse()` メソッドは、URL クエリ文字列（`str`）をキーと値のペアの集合に解析します。

例えば、クエリ文字列 `'foo=bar&abc=xyz&abc=123'` は次のように解析されます。

```json
{
  "foo": "bar",
  "abc": ["xyz", "123"]
}
```

`querystring.parse()` メソッドが返すオブジェクトは、JavaScript の `Object` をプロトタイプとして継承し*ません*。つまり、`obj.toString()` や `obj.hasOwnProperty()` といった一般的な `Object` のメソッドは定義されておらず、*動作しません*。

デフォルトでは、クエリ文字列内のパーセントエンコードされた文字は UTF-8 エンコーディングであると想定されます。別の文字エンコーディングを使用する場合は、代替の `decodeURIComponent` オプションを指定する必要があります。

```js
// gbkDecodeURIComponent 関数が既に存在すると仮定...

querystring.parse('w=%D6%D0%CE%C4&foo=bar', null, null,
                  { decodeURIComponent: gbkDecodeURIComponent });
```

## `querystring.stringify(obj[, sep[, eq[, options]]])`

<!-- YAML
added: v0.1.25
-->

* `obj` {Object} URL クエリ文字列にシリアライズするオブジェクト
* `sep` {string} クエリ文字列内でキーと値のペアを区切るために使われる部分文字列。**デフォルト:** `'&'`。
* `eq` {string} クエリ文字列内でキーと値を区切るために使われる部分文字列。**デフォルト:** `'='`。
* `options`
  * `encodeURIComponent` {Function} クエリ文字列内で URL に使えない文字をパーセントエンコーディングに変換する際に使われる関数。**デフォルト:** `querystring.escape()`。

`querystring.stringify()` メソッドは、与えられた `obj` の「自身のプロパティ」を反復処理して、URL クエリ文字列を生成します。

`obj` に渡された次の型の値をシリアライズします。
{string|number|bigint|boolean|string\[]|number\[]|bigint\[]|boolean\[]}
数値は有限の値である必要があります。その他の入力値は空文字列に変換されます。

```js
querystring.stringify({ foo: 'bar', baz: ['qux', 'quux'], corge: '' });
// 戻り値: 'foo=bar&baz=qux&baz=quux&corge='

querystring.stringify({ foo: 'bar', baz: 'qux' }, ';', ':');
// 戻り値: 'foo:bar;baz:qux'
```

デフォルトでは、クエリ文字列内でパーセントエンコーディングが必要な文字は UTF-8 としてエンコードされます。別のエンコーディングが必要な場合は、代替の `encodeURIComponent` オプションを指定する必要があります。

```js
// gbkEncodeURIComponent 関数が既に存在すると仮定、

querystring.stringify({ w: '中文', foo: 'bar' }, null, null,
                      { encodeURIComponent: gbkEncodeURIComponent });
```

## `querystring.unescape(str)`

<!-- YAML
added: v0.1.25
-->

* `str` {string}

`querystring.unescape()` メソッドは、与えられた `str` に対して URL パーセントエンコードされた文字のデコードを行います。

`querystring.unescape()` メソッドは `querystring.parse()` によって使われるもので、通常は直接使用されることを想定していません。主にアプリケーションコードが `querystring.unescape` を別の関数に割り当てることで、デコードの実装を置き換えられるようにするために公開されています。

デフォルトでは、`querystring.unescape()` メソッドは JavaScript 組み込みの `decodeURIComponent()` メソッドを使ってデコードを試みます。それが失敗した場合、不正な URL でも例外をスローしない、より安全な代替実装が使われます。

[encoding]: buffer.md#buffers-and-character-encodings

---

本ページは [nodejs.org/api/querystring](https://nodejs.org/api/querystring.html)（[nodejs/node](https://github.com/nodejs/node) の `doc/api/querystring.md`）の非公式日本語訳です。原文の著作権は Node.js contributors に帰属し、MIT License で提供されています。
