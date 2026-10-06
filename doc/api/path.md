---
title: Path
source: https://nodejs.org/api/path.html
---

# Path

<!--introduced_in=v0.10.0-->

> Stability: 2 - Stable

<!-- source_link=lib/path.js -->

`node:path` モジュールは、ファイルパスやディレクトリパスを扱うためのユーティリティを提供します。次のようにアクセスできます。

```cjs
const path = require('node:path');
```

```mjs
import path from 'node:path';
```

## Windows と POSIX

`node:path` モジュールのデフォルトの動作は、Node.js アプリケーションが実行されているオペレーティングシステムによって異なります。具体的には、Windows オペレーティングシステム上で実行している場合、`node:path` モジュールは Windows 形式のパスが使われていると仮定します。

そのため、`path.basename()` を使うと POSIX と Windows で異なる結果になることがあります。

POSIX の場合:

```js
path.basename('C:\\temp\\myfile.html');
// 戻り値: 'C:\\temp\\myfile.html'
```

Windows の場合:

```js
path.basename('C:\\temp\\myfile.html');
// 戻り値: 'myfile.html'
```

どのオペレーティングシステム上でも Windows のファイルパスを扱う際に一貫した結果を得るには、[`path.win32`][] を使います。

POSIX と Windows の場合:

```js
path.win32.basename('C:\\temp\\myfile.html');
// 戻り値: 'myfile.html'
```

どのオペレーティングシステム上でも POSIX のファイルパスを扱う際に一貫した結果を得るには、[`path.posix`][] を使います。

POSIX と Windows の場合:

```js
path.posix.basename('/tmp/myfile.html');
// 戻り値: 'myfile.html'
```

Windows 上では、Node.js はドライブごとの作業ディレクトリという概念に従います。この動作は、バックスラッシュのないドライブパスを使用する際に確認できます。例えば `path.resolve('C:\\')` は `path.resolve('C:')` とは異なる結果を返す可能性があります。詳しくは [この MSDN のページ][MSDN-Rel-Path] を参照してください。

## `path.basename(path[, suffix])`

<!-- YAML
added: v0.1.25
changes:
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/5348
    description: Passing a non-string as the `path` argument will throw now.
-->

* `path` {string}
* `suffix` {string} 削除する任意の拡張子
* 戻り値: {string}

`path.basename()` メソッドは、Unix の `basename` コマンドと同様に、`path` の最後の部分を返します。末尾の [ディレクトリ区切り文字][`path.sep`] は無視されます。

```js
path.basename('/foo/bar/baz/asdf/quux.html');
// 戻り値: 'quux.html'

path.basename('/foo/bar/baz/asdf/quux.html', '.html');
// 戻り値: 'quux'
```

Windows は通常、ファイル拡張子を含むファイル名を大文字小文字を区別せずに扱いますが、この関数はそれを行いません。例えば `C:\\foo.html` と `C:\\foo.HTML` は同じファイルを指しますが、`basename` は拡張子を大文字小文字を区別する文字列として扱います。

```js
path.win32.basename('C:\\foo.html', '.html');
// 戻り値: 'foo'

path.win32.basename('C:\\foo.HTML', '.html');
// 戻り値: 'foo.HTML'
```

`path` が文字列でない場合、または `suffix` が指定されていて文字列でない場合、[`TypeError`][] がスローされます。

## `path.delimiter`

<!-- YAML
added: v0.9.3
-->

* Type: {string}

プラットフォーム固有のパス区切り文字を提供します。

* Windows では `;`
* POSIX では `:`

例えば、POSIX の場合:

```js
console.log(process.env.PATH);
// 出力: '/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin'

process.env.PATH.split(path.delimiter);
// 戻り値: ['/usr/bin', '/bin', '/usr/sbin', '/sbin', '/usr/local/bin']
```

Windows の場合:

```js
console.log(process.env.PATH);
// 出力: 'C:\Windows\system32;C:\Windows;C:\Program Files\node\'

process.env.PATH.split(path.delimiter);
// 戻り値 ['C:\\Windows\\system32', 'C:\\Windows', 'C:\\Program Files\\node\\']
```

## `path.dirname(path)`

<!-- YAML
added: v0.1.16
changes:
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/5348
    description: Passing a non-string as the `path` argument will throw now.
-->

* `path` {string}
* 戻り値: {string}

`path.dirname()` メソッドは、Unix の `dirname` コマンドと同様に、`path` のディレクトリ名を返します。末尾のディレクトリ区切り文字は無視されます。[`path.sep`][] を参照してください。

```js
path.dirname('/foo/bar/baz/asdf/quux');
// 戻り値: '/foo/bar/baz/asdf'
```

`path` が文字列でない場合、[`TypeError`][] がスローされます。

## `path.extname(path)`

<!-- YAML
added: v0.1.25
changes:
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/5348
    description: Passing a non-string as the `path` argument will throw now.
-->

* `path` {string}
* 戻り値: {string}

`path.extname()` メソッドは、`path` の最後の部分にある `.`（ピリオド）文字の最後の出現位置から文字列の末尾までを拡張子として返します。`path` の最後の部分に `.` が存在しない場合、または `path` のベース名（`path.basename()` を参照）の最初の文字以外に `.` が存在しない場合は、空文字列が返されます。

```js
path.extname('index.html');
// 戻り値: '.html'

path.extname('index.coffee.md');
// 戻り値: '.md'

path.extname('index.');
// 戻り値: '.'

path.extname('index');
// 戻り値: ''

path.extname('.index');
// 戻り値: ''

path.extname('.index.md');
// 戻り値: '.md'
```

`path` が文字列でない場合、[`TypeError`][] がスローされます。

## `path.format(pathObject)`

<!-- YAML
added: v0.11.15
changes:
  - version: v19.0.0
    pr-url: https://github.com/nodejs/node/pull/44349
    description: The dot will be added if it is not specified in `ext`.
-->

* `pathObject` {Object} 次のプロパティを持つ任意の JavaScript オブジェクト:
  * `dir` {string}
  * `root` {string}
  * `base` {string}
  * `name` {string}
  * `ext` {string}
* 戻り値: {string}

`path.format()` メソッドは、オブジェクトからパス文字列を返します。これは [`path.parse()`][] の逆の操作です。

`pathObject` にプロパティを指定する際は、あるプロパティが他のプロパティより優先される組み合わせがあることに注意してください。

* `pathObject.dir` が指定されている場合、`pathObject.root` は無視されます
* `pathObject.base` が存在する場合、`pathObject.ext` と `pathObject.name` は無視されます

例えば、POSIX の場合:

```js
// `dir`、`root`、`base` が指定されている場合、
// `${dir}${path.sep}${base}` が返されます。
// `root` は無視されます。
path.format({
  root: '/ignored',
  dir: '/home/user/dir',
  base: 'file.txt',
});
// 戻り値: '/home/user/dir/file.txt'

// `dir` が指定されていない場合、`root` が使われます。
// `root` のみが指定されている場合、または `dir` が `root` と等しい場合は、
// プラットフォームの区切り文字は含まれません。`ext` は無視されます。
path.format({
  root: '/',
  base: 'file.txt',
  ext: 'ignored',
});
// 戻り値: '/file.txt'

// `base` が指定されていない場合、`name` + `ext` が使われます。
path.format({
  root: '/',
  name: 'file',
  ext: '.txt',
});
// 戻り値: '/file.txt'

// `ext` にドットが指定されていない場合は、ドットが追加されます。
path.format({
  root: '/',
  name: 'file',
  ext: 'txt',
});
// 戻り値: '/file.txt'
```

Windows の場合:

```js
path.format({
  dir: 'C:\\path\\dir',
  base: 'file.txt',
});
// 戻り値: 'C:\\path\\dir\\file.txt'
```

## `path.matchesGlob(path, pattern)`

<!-- YAML
added:
  - v22.5.0
  - v20.17.0
changes:
  - version:
    - v24.8.0
    - v22.20.0
    pr-url: https://github.com/nodejs/node/pull/59572
    description: Marking the API stable.
-->

* `path` {string} glob パターンと照合するパス。
* `pattern` {string} パスと照合する glob。
* 戻り値: {boolean} `path` が `pattern` にマッチしたかどうか。

`path.matchesGlob()` メソッドは、`path` が `pattern` にマッチするかどうかを判定します。`pattern` が受け付ける構文については [Glob patterns][] を参照してください。

例:

```js
path.matchesGlob('/foo/bar', '/foo/*'); // true
path.matchesGlob('/foo/bar*', 'foo/bird'); // false
```

`path` または `pattern` が文字列でない場合、[`TypeError`][] がスローされます。

## `path.isAbsolute(path)`

<!-- YAML
added: v0.11.2
-->

* `path` {string}
* 戻り値: {boolean}

`path.isAbsolute()` メソッドは、リテラルの `path` が絶対パスかどうかを判定します。したがって、パストラバーサルを軽減する目的で使用するのは安全ではありません。

指定された `path` が長さ 0 の文字列の場合、`false` が返されます。

例えば、POSIX の場合:

```js
path.isAbsolute('/foo/bar');   // true
path.isAbsolute('/baz/..');    // true
path.isAbsolute('/baz/../..'); // true
path.isAbsolute('qux/');       // false
path.isAbsolute('.');          // false
```

Windows の場合:

```js
path.isAbsolute('//server');    // true
path.isAbsolute('\\\\server');  // true
path.isAbsolute('C:/foo/..');   // true
path.isAbsolute('C:\\foo\\..'); // true
path.isAbsolute('bar\\baz');    // false
path.isAbsolute('bar/baz');     // false
path.isAbsolute('.');           // false
```

`path` が文字列でない場合、[`TypeError`][] がスローされます。

## `path.join([...paths])`

<!-- YAML
added: v0.1.16
-->

* `...paths` {string} パスセグメントの連続
* 戻り値: {string}

`path.join()` メソッドは、指定されたすべての `path` セグメントをプラットフォーム固有の区切り文字を使って結合し、その結果のパスを正規化します。

長さ 0 の `path` セグメントは無視されます。結合されたパス文字列が長さ 0 の文字列になる場合は、現在の作業ディレクトリを表す `'.'` が返されます。

```js
path.join('/foo', 'bar', 'baz/asdf', 'quux', '..');
// 戻り値: '/foo/bar/baz/asdf'

path.join('foo', {}, 'bar');
// スロー: 'TypeError: Path must be a string. Received {}'
```

パスセグメントのいずれかが文字列でない場合、[`TypeError`][] がスローされます。

## `path.normalize(path)`

<!-- YAML
added: v0.1.23
-->

* `path` {string}
* 戻り値: {string}

`path.normalize()` メソッドは、指定された `path` を正規化し、`'..'` と `'.'` のセグメントを解決します。

複数の連続するパスセグメント区切り文字（例えば POSIX の `/`、Windows の `\` または `/`）が見つかった場合、プラットフォーム固有のパスセグメント区切り文字（POSIX では `/`、Windows では `\`）1 つに置き換えられます。末尾の区切り文字は保持されます。

`path` が長さ 0 の文字列の場合、現在の作業ディレクトリを表す `'.'` が返されます。

POSIX では、この関数が適用する正規化の種類は、厳密には POSIX の仕様に準拠していません。例えば、この関数は先頭の 2 つのスラッシュを通常の絶対パスと同様に 1 つのスラッシュに置き換えますが、一部の POSIX システムではちょうど 2 つのスラッシュで始まるパスに特別な意味を持たせています。同様に、この関数が行う `..` セグメントの削除などの他の置換も、基盤となるシステムがパスを解決する方法を変える可能性があります。

例えば、POSIX の場合:

```js
path.normalize('/foo/bar//baz/asdf/quux/..');
// 戻り値: '/foo/bar/baz/asdf'
```

Windows の場合:

```js
path.normalize('C:\\temp\\\\foo\\bar\\..\\');
// 戻り値: 'C:\\temp\\foo\\'
```

Windows は複数のパス区切り文字を認識するため、どちらの区切り文字も Windows が優先する区切り文字（`\`）に置き換えられます。

```js
path.win32.normalize('C:////temp\\\\/\\/\\/foo/bar');
// 戻り値: 'C:\\temp\\foo\\bar'
```

`path` が文字列でない場合、[`TypeError`][] がスローされます。

## `path.parse(path)`

<!-- YAML
added: v0.11.15
-->

* `path` {string}
* 戻り値: {Object}

`path.parse()` メソッドは、`path` の重要な要素を表すプロパティを持つオブジェクトを返します。末尾のディレクトリ区切り文字は無視されます。[`path.sep`][] を参照してください。

返されるオブジェクトは次のプロパティを持ちます。

* `dir` {string}
* `root` {string}
* `base` {string}
* `name` {string}
* `ext` {string}

例えば、POSIX の場合:

```js
path.parse('/home/user/dir/file.txt');
// 戻り値:
// { root: '/',
//   dir: '/home/user/dir',
//   base: 'file.txt',
//   ext: '.txt',
//   name: 'file' }
```

```text
┌─────────────────────┬────────────┐
│          dir        │    base    │
├──────┬              ├──────┬─────┤
│ root │              │ name │ ext │
"  /    home/user/dir / file  .txt "
└──────┴──────────────┴──────┴─────┘
（"" の行のすべての空白は無視してください。表示のためだけのものです。）
```

Windows の場合:

```js
path.parse('C:\\path\\dir\\file.txt');
// 戻り値:
// { root: 'C:\\',
//   dir: 'C:\\path\\dir',
//   base: 'file.txt',
//   ext: '.txt',
//   name: 'file' }
```

```text
┌─────────────────────┬────────────┐
│          dir        │    base    │
├──────┬              ├──────┬─────┤
│ root │              │ name │ ext │
" C:\      path\dir   \ file  .txt "
└──────┴──────────────┴──────┴─────┘
（"" の行のすべての空白は無視してください。表示のためだけのものです。）
```

`path` が文字列でない場合、[`TypeError`][] がスローされます。

## `path.posix`

<!-- YAML
added: v0.11.15
changes:
  - version: v15.3.0
    pr-url: https://github.com/nodejs/node/pull/34962
    description: Exposed as `require('path/posix')`.
-->

* Type: {Object}

`path.posix` プロパティは、`path` メソッドの POSIX 固有の実装へのアクセスを提供します。

この API には `require('node:path').posix` または `require('node:path/posix')` でアクセスできます。

## `path.relative(from, to)`

<!-- YAML
added: v0.5.0
changes:
  - version: v6.8.0
    pr-url: https://github.com/nodejs/node/pull/8523
    description: On Windows, the leading slashes for UNC paths are now included
                 in the return value.
-->

* `from` {string}
* `to` {string}
* 戻り値: {string}

`path.relative()` メソッドは、現在の作業ディレクトリを基準として `from` から `to` への相対パスを返します。`from` と `to` が（それぞれに `path.resolve()` を呼んだ後）同じパスに解決される場合、長さ 0 の文字列が返されます。

`from` または `to` に長さ 0 の文字列が渡された場合、その長さ 0 の文字列の代わりに現在の作業ディレクトリが使われます。

例えば、POSIX の場合:

```js
path.relative('/data/orandea/test/aaa', '/data/orandea/impl/bbb');
// 戻り値: '../../impl/bbb'
```

Windows の場合:

```js
path.relative('C:\\orandea\\test\\aaa', 'C:\\orandea\\impl\\bbb');
// 戻り値: '..\\..\\impl\\bbb'
```

`from` または `to` のいずれかが文字列でない場合、[`TypeError`][] がスローされます。

## `path.resolve([...paths])`

<!-- YAML
added: v0.3.4
-->

* `...paths` {string} パスまたはパスセグメントの連続
* 戻り値: {string}

`path.resolve()` メソッドは、パスまたはパスセグメントの連続を絶対パスに解決します。

指定されたパスの連続は右から左へ処理され、絶対パスが構成されるまで後続の各 `path` が先頭に追加されます。例えば、パスセグメントの連続 `/foo`、`/bar`、`baz` が与えられた場合、`path.resolve('/foo', '/bar', 'baz')` は `/bar/baz` を返します。これは `'baz'` が絶対パスではないものの、`'/bar' + '/' + 'baz'` が絶対パスであるためです。

指定されたすべての `path` セグメントを処理した後も絶対パスが生成されない場合、現在の作業ディレクトリが使われます。

結果のパスは正規化され、パスがルートディレクトリに解決される場合を除き、末尾のスラッシュは削除されます。

長さ 0 の `path` セグメントは無視されます。

`path` セグメントが渡されない場合、`path.resolve()` は現在の作業ディレクトリの絶対パスを返します。

```js
path.resolve('/foo/bar', './baz');
// 戻り値: '/foo/bar/baz'

path.resolve('/foo/bar', '/tmp/file/');
// 戻り値: '/tmp/file'

path.resolve('wwwroot', 'static_files/png/', '../gif/image.gif');
// 現在の作業ディレクトリが /home/myself/node の場合、
// これは '/home/myself/node/wwwroot/static_files/gif/image.gif' を返します
```

いずれかの引数が文字列でない場合、[`TypeError`][] がスローされます。

## `path.sep`

<!-- YAML
added: v0.7.9
-->

* Type: {string}

プラットフォーム固有のパスセグメント区切り文字を提供します。

* Windows では `\`
* POSIX では `/`

例えば、POSIX の場合:

```js
'foo/bar/baz'.split(path.sep);
// 戻り値: ['foo', 'bar', 'baz']
```

Windows の場合:

```js
'foo\\bar\\baz'.split(path.sep);
// 戻り値: ['foo', 'bar', 'baz']
```

Windows では、フォワードスラッシュ（`/`）とバックスラッシュ（`\`）の両方がパスセグメント区切り文字として受け付けられますが、`path` のメソッドはバックスラッシュ（`\`）のみを追加します。

## `path.toNamespacedPath(path)`

<!-- YAML
added: v9.0.0
-->

* `path` {string}
* 戻り値: {string}

Windows システムでのみ、指定された `path` に対応する [namespace-prefixed path][] を返します。`path` が文字列でない場合、`path` は変更されずに返されます。

このメソッドは Windows システムでのみ意味を持ちます。POSIX システムでは、このメソッドは何も行わず、常に `path` を変更せずに返します。

## `path.win32`

<!-- YAML
added: v0.11.15
changes:
  - version: v15.3.0
    pr-url: https://github.com/nodejs/node/pull/34962
    description: Exposed as `require('path/win32')`.
-->

* Type: {Object}

`path.win32` プロパティは、`path` メソッドの Windows 固有の実装へのアクセスを提供します。

この API には `require('node:path').win32` または `require('node:path/win32')` でアクセスできます。

[Glob patterns]: fs.md#glob-patterns
[MSDN-Rel-Path]: https://docs.microsoft.com/en-us/windows/desktop/FileIO/naming-a-file#fully-qualified-vs-relative-paths
[`TypeError`]: errors.md#class-typeerror
[`path.parse()`]: #pathparsepath
[`path.posix`]: #pathposix
[`path.sep`]: #pathsep
[`path.win32`]: #pathwin32
[namespace-prefixed path]: https://docs.microsoft.com/en-us/windows/desktop/FileIO/naming-a-file#namespaces

---

本ページは [nodejs.org/api/path](https://nodejs.org/api/path.html)（[nodejs/node](https://github.com/nodejs/node) の `doc/api/path.md`）の非公式日本語訳です。原文の著作権は Node.js contributors に帰属し、MIT License で提供されています。
