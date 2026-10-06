---
title: 環境変数
source: https://nodejs.org/api/environment_variables.html
---

# 環境変数

<!--introduced_in=v20.12.0-->

環境変数とは、Node.js プロセスが実行されている環境に関連付けられた変数です。

## CLI 環境変数

Node.js の動作をカスタマイズするために定義できる環境変数の一式があります。詳しくは [CLI 環境変数のドキュメント][CLI Environment Variables documentation] を参照してください。

## `process.env`

環境変数を操作するための基本的な API は `process.env` です。これは、あらかじめユーザー環境変数が設定されたオブジェクトで、変更や追加が可能です。

詳しくは [`process.env` のドキュメント][`process.env` documentation] を参照してください。

## DotEnv

> Stability: 2 - Stable

`.env` ファイルで定義された追加の環境変数を扱うためのユーティリティ一式です。

### `.env` ファイル

`.env` ファイル（dotenv ファイルとも呼ばれる）は環境変数を定義するファイルで、Node.js アプリケーションがそれを利用できます（[dotenv][] パッケージによって広く知られるようになりました）。

以下は基本的な `.env` ファイルの内容の例です。

```text
MY_VAR_A = "my variable A"
MY_VAR_B = "my variable B"
```

このタイプのファイルは様々なプログラミング言語やプラットフォームで使われていますが、正式な仕様は存在しないため、Node.js は以下で説明する独自の仕様を定義しています。

`.env` ファイルはキーと値のペアを含むファイルで、各ペアは変数名の後に等号（`=`）、続いて変数の値という形式で表されます。

このようなファイルの名前は通常 `.env` か、`.env` で始まる名前です（例えば、`dev` が特定の対象環境を示す `.env.dev` など）。これは推奨される命名規則ですが必須ではなく、dotenv ファイルは任意のファイル名を持つことができます。

#### 変数名

有効な変数名には、文字（大文字または小文字）、数字、アンダースコア（`_`）のみを含めることができ、数字で始めることはできません。

より具体的には、有効な変数名は次の正規表現にマッチする必要があります。

```text
^[a-zA-Z_]+[a-zA-Z0-9_]*$
```

推奨される規則は、必要に応じて数字やアンダースコアを使った大文字を使うことですが、上記の定義を満たす変数名であれば問題なく動作します。

例えば、次は有効な変数名です: `MY_VAR`、`MY_VAR_1`、`my_var`、`my_var_1`、`myVar`、`My_Var123`。一方、次は無効です: `1_VAR`、`'my-var'`、`"my var"`、`VAR_#1`。

#### 変数の値

変数の値は任意のテキストで構成され、任意でシングルクォート（`'`）またはダブルクォート（`"`）で囲むことができます。

クォートされた変数は複数行にまたがることができますが、クォートされていない変数は1行に限られます。

Node.js によって解析される際、すべての値はテキストとして解釈される点に注意してください。つまり、どのような値も Node.js 内では JavaScript の文字列になります。例えば `0`、`true`、`{ "hello": "world" }` という値は、数値のゼロやブール値の `true`、`hello` プロパティを持つオブジェクトではなく、それぞれリテラルの文字列 `'0'`、`'true'`、`'{ "hello": "world" }'` になります。

有効な変数の例:

```text
MY_SIMPLE_VAR = a simple single line variable
MY_EQUALS_VAR = "this variable contains an = sign!"
MY_HASH_VAR = 'this variable contains a # symbol!'
MY_MULTILINE_VAR = '
this is a multiline variable containing
two separate lines\nSorry, I meant three lines'
```

#### 空白

変数のキーや値の前後にある空白文字は、クォートで囲まれていない限り無視されます。

例えば:

```text
   MY_VAR_A   =    my variable a
    MY_VAR_B   =    '   my variable b   '
```

これは次と同じものとして扱われます。

```text
MY_VAR_A = my variable a
MY_VAR_B = '   my variable b   '
```

#### コメント

ハッシュタグ（`#`）文字はコメントの開始を示し、その行の残りの部分は完全に無視されます。

ただし、クォート内にあるハッシュタグは、他の通常の文字と同様に扱われます。

例えば:

```text
# これはコメントです
MY_VAR = my variable # これもコメントです
MY_VAR_A = "# this is NOT a comment"
```

#### `export` プレフィックス

変数宣言の前に `export` キーワードを任意で付けることができ、このキーワードはファイルに対する処理ではすべて無視されます。

これは、ファイルを変更せずにシェルのターミナルで source できるようにするために便利です。

例:

```text
export MY_VAR = my variable
```

### CLI オプション

`.env` ファイルは、次のいずれかの CLI オプションを使って `process.env` オブジェクトに値を設定するために使用できます。

* [`--env-file=file`][]

* [`--env-file-if-exists=file`][]

### プログラムによる API

次の2つの関数により、`.env` ファイルを直接操作できます。

* [`process.loadEnvFile`][] は `.env` ファイルを読み込み、その変数で `process.env` を設定します

* [`util.parseEnv`][] は `.env` ファイルの生の内容を解析し、その値をオブジェクトとして返します

[CLI Environment Variables documentation]: cli.md#environment-variables_1
[`--env-file-if-exists=file`]: cli.md#--env-file-if-existsfile
[`--env-file=file`]: cli.md#--env-filefile
[`process.env` documentation]: process.md#processenv
[`process.loadEnvFile`]: process.md#processloadenvfilepath
[`util.parseEnv`]: util.md#utilparseenvcontent
[dotenv]: https://github.com/motdotla/dotenv

---

本ページは [nodejs.org/api/environment_variables](https://nodejs.org/api/environment_variables.html)（[nodejs/node](https://github.com/nodejs/node) の `doc/api/environment_variables.md`）の非公式日本語訳です。原文の著作権は Node.js contributors に帰属し、MIT License で提供されています。
