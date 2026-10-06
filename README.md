# tdocsjp/nodejs

Node.js 公式 API リファレンス（[nodejs.org/api](https://nodejs.org/api/)、ソースは [nodejs/node](https://github.com/nodejs/node) の `doc/api/`）の非公式日本語訳。[tdocsjp/website](https://github.com/tdocsjp/website) の submodule として取り込まれる想定。

ページは nodejs.org の URL パスをそのままミラーする（`doc/api/path.md` → `nodejs.org/api/path.html` → このリポジトリの `doc/api/path.md`）。`index.md` はトップページ（翻訳済みページへの目次）。

- 原文: https://github.com/nodejs/node の `doc/api/`
- ライセンス: 原文（コード・ドキュメントともに）は MIT License。著作権は Node.js contributors に帰属する
- 本訳は非公式であり、Node.js プロジェクトによる承認を受けたものではない

## 翻訳済み

- `doc/api/documentation.md` — [nodejs.org/api/documentation](https://nodejs.org/api/documentation.html)（全文翻訳）
- `doc/api/index.md` — [nodejs.org/api/index](https://nodejs.org/api/index.html)（全文翻訳、API 索引）
- `doc/api/path.md` — [nodejs.org/api/path](https://nodejs.org/api/path.html)（全文翻訳）
- `doc/api/events.md` — [nodejs.org/api/events](https://nodejs.org/api/events.html)（概要・要約。`EventEmitter` の主要メソッドレベル）
- `doc/api/process.md` — [nodejs.org/api/process](https://nodejs.org/api/process.html)（概要・要約）
- `doc/api/http.md` — [nodejs.org/api/http](https://nodejs.org/api/http.html)（概要・要約）
- `doc/api/util.md` — [nodejs.org/api/util](https://nodejs.org/api/util.html)（概要・要約）
- `doc/api/buffer.md` — [nodejs.org/api/buffer](https://nodejs.org/api/buffer.html)（概要・要約）
- `doc/api/fs.md` — [nodejs.org/api/fs](https://nodejs.org/api/fs.html)（概要・要約。原文は約300KB・数千行規模のため冒頭概要のみ）

「全文翻訳」は原文の段落・コード例をそのまま翻訳したもの。「概要・要約」は、原文が非常に大きい（数万〜数十万文字）モジュールについて、主要なクラス・メソッドを表形式で日本語にまとめたもので、各メソッドの詳細な引数・エッジケースの説明はまだない。

## 未翻訳

`doc/api/` の残り（約64ファイル）はすべて未着手。特に優先度が高いもの:

- `fs`・`http`・`util`・`buffer`・`process`・`events` の各メソッド単位の詳細翻訳（現在は概要のみ）
- `stream`、`net`、`child_process`、`os`、`url`、`querystring`、`crypto`、`errors`、`cli` などの頻用モジュール
- `assert`、`console`、`timers`、`modules`/`esm`（CommonJS/ESM）
- その他すべての個別モジュールページ

必要になったページ・深さから追加していく。
