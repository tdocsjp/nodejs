---
title: String decoder
source: https://nodejs.org/api/string_decoder.html
---

# String decoder

<!--introduced_in=v0.10.0-->

> Stability: 2 - Stable

<!-- source_link=lib/string_decoder.js -->

`node:string_decoder` モジュールは、エンコードされたマルチバイトの UTF-8 および UTF-16 文字を保持したまま `Buffer` オブジェクトを文字列にデコードするための API を提供します。次のようにアクセスできます。

```mjs
import { StringDecoder } from 'node:string_decoder';
```

```cjs
const { StringDecoder } = require('node:string_decoder');
```

以下の例は、`StringDecoder` クラスの基本的な使い方を示しています。

```mjs
import { StringDecoder } from 'node:string_decoder';
import { Buffer } from 'node:buffer';
const decoder = new StringDecoder('utf8');

const cent = Buffer.from([0xC2, 0xA2]);
console.log(decoder.write(cent)); // 出力: ¢

const euro = Buffer.from([0xE2, 0x82, 0xAC]);
console.log(decoder.write(euro)); // 出力: €
```

```cjs
const { StringDecoder } = require('node:string_decoder');
const decoder = new StringDecoder('utf8');

const cent = Buffer.from([0xC2, 0xA2]);
console.log(decoder.write(cent)); // 出力: ¢

const euro = Buffer.from([0xE2, 0x82, 0xAC]);
console.log(decoder.write(euro)); // 出力: €
```

`Buffer` インスタンスが `StringDecoder` インスタンスに書き込まれると、デコードされた文字列に不完全なマルチバイト文字が含まれないように、内部バッファが使われます。これらは次に `stringDecoder.write()` が呼ばれるまで、または `stringDecoder.end()` が呼ばれるまでバッファ内に保持されます。

以下の例では、ユーロ記号（`€`）を表す3バイトの UTF-8 エンコードされたバイト列が、3回の別々の操作で書き込まれています。

```mjs
import { StringDecoder } from 'node:string_decoder';
import { Buffer } from 'node:buffer';
const decoder = new StringDecoder('utf8');

decoder.write(Buffer.from([0xE2]));
decoder.write(Buffer.from([0x82]));
console.log(decoder.end(Buffer.from([0xAC]))); // 出力: €
```

```cjs
const { StringDecoder } = require('node:string_decoder');
const decoder = new StringDecoder('utf8');

decoder.write(Buffer.from([0xE2]));
decoder.write(Buffer.from([0x82]));
console.log(decoder.end(Buffer.from([0xAC]))); // 出力: €
```

## クラス: `StringDecoder`

### `new StringDecoder([encoding])`

<!-- YAML
added: v0.1.99
-->

* `encoding` {string} `StringDecoder` が使用する文字[エンコーディング][encoding]。**デフォルト:** `'utf8'`。

新しい `StringDecoder` インスタンスを作成します。

### `stringDecoder.end([buffer])`

<!-- YAML
added: v0.9.3
-->

* `buffer` {string|Buffer|TypedArray|DataView} デコード対象のバイト列。
* 戻り値: {string}

内部バッファに残っている入力を文字列として返します。不完全な UTF-8 および UTF-16 文字を表すバイトは、その文字エンコーディングに適した代替文字に置き換えられます。

`buffer` 引数が指定された場合、残りの入力を返す前に、最後にもう一度 `stringDecoder.write()` の呼び出しが実行されます。
`end()` が呼ばれた後、`stringDecoder` オブジェクトは新しい入力のために再利用できます。

### `stringDecoder.write(buffer)`

<!-- YAML
added: v0.1.99
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/9618
    description: Each invalid character is now replaced by a single replacement
                 character instead of one for each individual byte.
-->

* `buffer` {string|Buffer|TypedArray|DataView} デコード対象のバイト列。
* 戻り値: {string}

デコードされた文字列を返します。この際、`Buffer`、`TypedArray`、または `DataView` の末尾にある不完全なマルチバイト文字は、返される文字列からは除外され、次の `stringDecoder.write()` または `stringDecoder.end()` の呼び出しのために内部バッファに保持されます。

[encoding]: buffer.md#buffers-and-character-encodings

---

本ページは [nodejs.org/api/string_decoder](https://nodejs.org/api/string_decoder.html)（[nodejs/node](https://github.com/nodejs/node) の `doc/api/string_decoder.md`）の非公式日本語訳です。原文の著作権は Node.js contributors に帰属し、MIT License で提供されています。
